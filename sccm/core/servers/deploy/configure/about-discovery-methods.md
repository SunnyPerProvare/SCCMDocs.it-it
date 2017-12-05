---
title: Metodi di individuazione
titleSuffix: Configuration Manager
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed931751-18f2-4230-a09e-a0a329fbfa1c
caps.latest.revision: "8"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 0b2d075d280fd6aa8dc01d20f3f61cf4e0c75203
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/04/2017
---
# <a name="about-discovery-methods-for-system-center-configuration-manager"></a>Informazioni sui metodi di individuazione per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I metodi di individuazione di System Center Configuration Manager consentono di individuare vari dispositivi nella rete o dispositivi e utenti in Active Directory. Per usare un metodo di individuazione in modo efficiente, è importante conoscere le configurazioni disponibili e le rispettive limitazioni.  

##  <a name="bkmk_aboutForest"></a> Individuazione foresta Active Directory  
 **Configurabile:** sì  

 **Abilitata per impostazione predefinita:** no  

 Per eseguire questo metodo è possibile usare gli **account** seguenti:  

-   **Account di individuazione foresta Active Directory** (definito dall'utente)  

-   **Account computer** del server del sito  

A differenza di altri metodi di individuazione Active Directory, Individuazione foresta Active Directory non individua le risorse che è possibile gestire. Questo metodo individua invece i percorsi di rete che sono configurati in Active Directory e li può convertire in limiti da usare in tutta la gerarchia.  

Quando viene eseguito, il metodo effettua ricerche nella foresta Active Directory locale, in ogni foresta trusted e in ogni altra foresta configurata nel nodo **Foreste Active Directory** della console di Configuration Manager.  

Usare Individuazione foresta Active Directory per eseguire queste operazioni:  

-   Individuare siti e subnet Active Directory e creare i limiti di Configuration Manager sulla base dei percorsi di rete individuati.  

-   Identificare le supernet assegnate a un sito Active Directory e convertire ogni supernet in un limite di intervallo di indirizzi IP.  

-   Pubblicare in Active Directory Domain Services in una foresta quando la pubblicazione in tale foresta è abilitata e l'account foresta Active Directory specificato dispone di autorizzazioni per tale foresta.  

È possibile gestire Individuazione foresta Active Directory nella console di Configuration Manager dai nodi seguenti in **Configurazione della gerarchia** nell'area di lavoro **Amministrazione**:  

-   **Metodi di individuazione**: qui è possibile abilitare Individuazione foresta Active Directory affinché venga eseguita nel sito di livello superiore della gerarchia. È inoltre possibile specificare una pianificazione semplice per l'esecuzione dell'individuazione e configurarla per creare automaticamente limiti dalle subnet IP e dai siti di Active Directory individuati. Il metodo Individuazione foresta Active Directory non può essere eseguito in un sito primario figlio o in un sito secondario.  

-   **Foreste Active Directory**: qui è possibile configurare le foreste Active Directory aggiuntive che si desidera individuare, specificare l'account da utilizzare come account foresta Active Directory per ciascuna foresta e configurare la pubblicazione in ciascun foresta. È anche possibile monitorare il processo di individuazione e aggiungere subnet IP e siti Active Directory a Configuration Manager come limiti e membri di gruppi di limiti.  

Per configurare la pubblicazione delle foreste Active Directory per ogni sito della gerarchia, connettere la console di Configuration Manager al sito principale della gerarchia. La scheda **Pubblicazione** nella finestra di dialogo **Proprietà** di un sito Active Directory può mostrare solo il sito corrente e i relativi siti figlio. Quando la pubblicazione è abilitata per una foresta e lo schema della foresta viene esteso per Configuration Manager, per ogni sito abilitato per la pubblicazione in tale foresta Active Directory vengono pubblicate le informazioni seguenti:  

-    **SMS-Site-&lt;codice sito>**

-   **SMS-MP-&lt;codice sito>-&lt;nome del server nel sistema del sito>**  

-   **SMS-SLP-&lt;codice sito>-&lt;nome del server nel sistema del sito>**  

-   **SMS-&lt;codice sito>-&lt;nome sito o subnet Active Directory>**  

> [!NOTE]  
>  I siti secondari usano sempre l'account computer del server del sito secondario per la pubblicazione in Active Directory. Se si vuole che i siti secondari pubblichino in Active Directory, verificare che l'account computer del server del sito secondario disponga delle autorizzazioni per la pubblicazione in Active Directory. Un sito secondario non è in grado di pubblicare dati in una foresta non trusted.  

> [!CAUTION]  
>  Quando si deseleziona l'opzione per la pubblicazione di un sito in una foresta Active Directory, tutte le informazioni pubblicate in precedenza per il sito, compresi i ruoli del sistema del sito disponibili, vengono rimosse da Active Directory.  

Le azioni di individuazione foresta Active Directory vengono registrate nei log seguenti:  

-   Tutte le azioni, tranne quelle relative alla pubblicazione, vengono registrate nel file **ADForestDisc.Log** nella cartella **&lt;PercorsoInstallazione>\Logs** nel server del sito.  

-   Le azioni di pubblicazione di Individuazione foresta Active Directory vengono registrate nei file **hman.log** e **sitecomp.log** nella cartella **&lt;PercorsoInstallazione>\Logs** del server del sito.  

Per altre informazioni su come configurare questo metodo di individuazione, vedere [Configurare i metodi di individuazione per System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="bkmk_aboutGroup"></a> Individuazione gruppo Active Directory  
**Configurabile:** sì  

**Abilitata per impostazione predefinita:** no  

Per eseguire questo metodo è possibile usare gli **account** seguenti:  

-   **Account di individuazione gruppo Active Directory** (definito dall'utente)  

-   **Account computer** del server del sito  

> [!TIP]  
>  Oltre alle informazioni disponibili in questa sezione, vedere [Funzionalità comuni dell'individuazione gruppo, sistema e utente Active Directory](#bkmk_shared).  

Usare questo metodo per eseguire ricerche in Active Directory Domain Services e individuare:  

-   Gruppi di sicurezza locali, globali e universali.  

-   L'appartenenza dei gruppi.  

-   Informazioni limitate sui computer e sugli utenti membri di un gruppo, anche quando un altro metodo non ha precedentemente individuato tali computer e utenti.  

Questo metodo di individuazione ha lo scopo di identificare i gruppi e le relazioni di gruppo dei membri dei gruppi. Per impostazione predefinita, vengono individuati solo i gruppi di protezione. Se si vuole individuare anche l'appartenenza dei gruppi di distribuzione, è necessario selezionare la casella di controllo per l'opzione **Individua l'appartenenza dei gruppi di distribuzione** nella scheda **Opzione** della finestra di dialogo **Individuazione gruppo Active Directory - Proprietà**.  

Individuazione gruppo Active Directory non supporta gli attributi estesi di Active Directory che possono essere identificati con Individuazione sistema Active Directory o Individuazione utente Active Directory. Poiché questo metodo di individuazione non è ottimizzato per l'individuazione di risorse computer e utente, eseguire tale metodo dopo aver eseguito Individuazione sistema Active Directory o Individuazione utente Active Directory. Questo perché il metodo crea un record dei dati di individuazione completo per i gruppi, ma un record limitato per i computer e gli utenti che sono membri di gruppi.  

È possibile configurare gli ambiti di individuazione seguenti per controllare come questo metodo deve ricercare le informazioni:  

-   **Percorso**: usare un percorso se si vuole effettuare la ricerca in uno o più contenitori di Active Directory. Questa opzione dell'ambito supporta una ricerca ricorsiva nei contenitori di Active Directory specificati e in ogni contenitore figlio. Questo processo continua finché non vengono più trovati contenitori figlio.  

-   **Gruppi**: usare i gruppi se si vuole effettuare la ricerca in uno o più gruppi Active Directory specifici. È possibile configurare **Dominio Active Directory** per usare il dominio e la foresta predefiniti o limitare la ricerca a un singolo controller di dominio. Inoltre, è possibile specificare uno o più gruppi in cui effettuare la ricerca. Se non si specifica almeno un gruppo, viene effettuata la ricerca in tutti i gruppi trovati nel percorso specificato del **Dominio Active Directory** .  

> [!CAUTION]  
>  Quando si configura un ambito di individuazione, scegliere solo i gruppi che è necessario individuare. Questo perché Individuazione gruppo Active Directory prova a individuare ogni membro di ciascun gruppo nell'ambito di individuazione. L'individuazione di gruppi di grandi dimensioni può richiedere un uso estensivo della larghezza di banda e di risorse Active Directory.  

> [!NOTE]  
>  Per poter creare raccolte basate sugli attributi estesi di Active Directory e garantire così risultati di individuazione precisi per computer e utenti, è prima necessario eseguire Individuazione sistema Active Directory o Individuazione utente Active Directory, a seconda di quel che si vuole individuare.  

Le azioni di Individuazione gruppo Active Directory vengono registrate nel file **adsgdis.log** nella cartella **&lt;PercorsoInstallazione\>\LOGS** del server del sito.  

Per altre informazioni su come configurare questo metodo di individuazione, vedere [Configurare i metodi di individuazione per System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="bkmk_aboutSystem"></a>Individuazione sistema Active Directory  
**Configurabile:** sì  

**Abilitata per impostazione predefinita:** no  

Per eseguire questo metodo è possibile usare gli **account** seguenti:  

-   **Account di individuazione sistema Active Directory** (definito dall'utente)  

-   **Account computer** del server del sito  

> [!TIP]  
>  Oltre alle informazioni disponibili in questa sezione, vedere [Funzionalità comuni dell'individuazione gruppo, sistema e utente Active Directory](#bkmk_shared).  

Usare questo metodo di individuazione per cercare nei percorsi di Active Directory Domain Services specificati le risorse del computer che possono essere usate per creare raccolte e query. È anche possibile installare il client di Configuration Manager in un dispositivo individuato usando l'installazione push client.  

Per impostazione predefinita, questo metodo individua informazioni di base relative al computer, tra cui:  

-   Nome computer  

-   Il sistema operativo e la sua versione  

-   Il nome del contenitore Active Directory  

-   Indirizzo IP  

-   Sito di Active Directory  

-   Timestamp dell'ultimo accesso  

Per creare correttamente un record dei dati di individuazione per un computer, Individuazione sistema Active Directory deve essere in grado di identificare l'account computer e quindi risolvere il nome del computer in un indirizzo IP.  

Nella finestra di dialogo **Individuazione sistema Active Directory - Proprietà** della scheda **Attributi di Active Directory** è possibile visualizzare l'elenco completo degli attributi di oggetto predefiniti restituiti da Individuazione sistema Active Directory. È anche possibile configurare il metodo per individuare altri attributi (estesi).  

Le azioni di Individuazione sistema Active Directory vengono registrate nel file **adsysdis.log** nella cartella **&lt;PercorsoInstallazione\>\LOGS** del server del sito.  

Per altre informazioni su come configurare questo metodo di individuazione, vedere [Configurare i metodi di individuazione per System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="bkmk_aboutUser"></a> Individuazione utente Active Directory  
**Configurabile:** sì  

**Abilitata per impostazione predefinita:** no  

Per eseguire questo metodo è possibile usare gli **account** seguenti:  

-   **Account di individuazione utente Active Directory** (definito dall'utente)  

-   **Account computer** del server del sito  

> [!TIP]  
>  Oltre alle informazioni disponibili in questa sezione, vedere [Funzionalità comuni dell'individuazione gruppo, sistema e utente Active Directory](#bkmk_shared).  

Usare questo metodo di individuazione per effettuare ricerche in Active Directory Domain Services e identificare gli account utente e gli attributi associati. Per impostazione predefinita, questo metodo individua informazioni di base relative all'account utente, tra cui:  

-   Nome utente  

-   Il nome utente univoco (include il nome di dominio)  

-   Dominio  

-   I nomi dei contenitori Active Directory  

Nella finestra di dialogo **Individuazione utente Active Directory - Proprietà** della scheda **Attributi di Active Directory** è possibile visualizzare l'elenco completo degli attributi di oggetto predefiniti restituiti da Individuazione utente Active Directory. È anche possibile configurare il metodo per individuare altri attributi (estesi).

Le azioni di Individuazione utente Active Directory vengono registrate nel file **adusrdis.log** nella cartella **&lt;PercorsoInstallazione\>\LOGS** del server del sito.  

Per altre informazioni su come configurare questo metodo di individuazione, vedere [Configurare i metodi di individuazione per System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

## <a name="azureaddisc"></a> Individuazione utente Azure Active Directory
A partire dalla versione 1706, è possibile usare Individuazione utente Azure Active Directory (Azure AD) quando si configura l'ambiente per l'uso dei servizi di Azure.
Usare questo metodo di individuazione per cercare in Azure AD gli utenti che eseguono l'autenticazione per l'istanza di Azure AD, in particolare gli attributi seguenti:  
-   objectId
-   displayName
-   mail
-   mailNickname
-   onPremisesSecurityIdentifier
-   userPrincipalName
-   AAD tenantID

Questo metodo supporta la sincronizzazione completa e la sincronizzazione delta dei dati degli utenti da Azure AD. Queste informazioni possono quindi essere usate con i dati di individuazione raccolti con altri metodi di individuazione.

Le azioni per l'individuazione utente Azure Active Directory vengono registrate nel file SMS_AZUREAD_DISCOVERY_AGENT.log nel server del sito di livello superiore della gerarchia.

Per configurare l'individuazione utente Azure AD, si usa la procedura guidata per i servizi di Azure.  Per informazioni su come configurare questo metodo di individuazione, vedere [Configurare l'individuazione utente Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods).





##  <a name="bkmk_aboutHeartbeat"></a> Individuazione heartbeat  
**Configurabile:** sì  

**Abilitata per impostazione predefinita:** sì  

Per eseguire questo metodo è possibile usare gli **account** seguenti:  

-   **Account computer** del server del sito  

Il metodo Individuazione heartbeat è diverso dagli altri metodi di individuazione di Configuration Manager. È infatti abilitato per impostazione predefinita e viene eseguito in ogni computer client, anziché su un server del sito, per creare un record dei dati di individuazione. Per i client di dispositivi mobili, questo record dei dati di individuazione viene creato dal punto di gestione usato dal client di dispositivi mobili. Per gestire il record del database dei client di Configuration Manager, non disabilitare Individuazione heartbeat. Oltre a consentire la gestione del record del database, questo metodo può forzare l'individuazione di un computer come nuovo record di risorse oppure ripopolare il record del database di un computer che è stato eliminato dal database.  

Il metodo Individuazione heartbeat viene eseguito in base a una pianificazione configurata per tutti i client della gerarchia oppure, se chiamato manualmente, in un client specifico tramite l'esecuzione di **Ciclo di recupero dati di rilevamento** nella scheda **Azione** in un programma di Configuration Manager del client. La pianificazione predefinita per Individuazione heartbeat è impostata per l'esecuzione ogni 7 giorni. Se viene modificato l'intervallo di individuazione heartbeat, verificare che l'esecuzione sia più frequente rispetto all'attività di manutenzione del sito **Elimina dati di individuazione obsoleti**, che consente di eliminare i record client inattivi dal database del sito. È possibile configurare l'attività **Elimina dati di individuazione obsoleti** solo per i siti primari.  

Quando viene eseguito, il metodo Individuazione heartbeat crea un record dei dati di individuazione contenente le informazioni correnti del client. Il client copia quindi questo file di piccole dimensioni (di circa 1 KB) in un punto di gestione in modo che un sito primario possa elaborarlo. Il file contiene le informazioni seguenti:  

-   Percorso di rete  

-   Nome NetBIOS  

-   Versione dell'agente client  

-   Dettagli sullo stato operativo  

Individuazione heartbeat è l'unico metodo di individuazione che offre dettagli relativi allo stato di installazione client, in quanto aggiorna l'attributo client delle risorse di sistema impostando il valore su **Yes**.  

> [!NOTE]  
>  Anche se Individuazione heartbeat è disabilitato, i record dei dati di individuazione vengono comunque creati e inviati per i client di dispositivi mobili attivi. In questo modo, l'attività **Elimina dati di individuazione obsoleti** non influisce sui dispositivi mobili attivi. Infatti, quando l'attività **Elimina dati di individuazione obsoleti** elimina un record del database per un dispositivo mobile, revoca anche il certificato del dispositivo e blocca la connessione del dispositivo mobile ai punti di gestione.  

Le azioni di Individuazione heartbeat vengono registrate nei percorsi seguenti:  

-   Per i client computer, le azioni di Individuazione heartbeat vengono registrate nel client, nel file **InventoryAgent.log** nella cartella *%Windir%\CCM\Logs*.  

-   Per i client dispositivi mobili, le azioni di Individuazione heartbeat vengono registrate nel file **DMPRP.log** nella cartella *%Program Files%\CCM\Logs* del punto di gestione usato dal client.  

Per altre informazioni su come configurare questo metodo di individuazione, vedere [Configurare i metodi di individuazione per System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

##  <a name="bkmk_aboutNetwork"></a> Individuazione di rete  
**Configurabile:** sì  

**Abilitata per impostazione predefinita:** no  

Per eseguire questo metodo è possibile usare gli **account** seguenti:  

-   **Account computer** del server del sito  

Usare questo metodo per individuare la topologia della rete e i dispositivi di rete che hanno un indirizzo IP. Individuazione di rete cerca nella rete le risorse con IP abilitato eseguendo query in server che eseguono un'implementazione Microsoft di DHCP, cache ARP (Address Resolution Protocol) nei router, dispositivi con SNMP abilitato e domini Active Directory.  

Per usare Individuazione di rete, è necessario prima specificare il *livello* di individuazione da eseguire. È inoltre possibile configurare uno o più meccanismi di individuazione che consentono a Individuazione di rete di eseguire query relative a dispositivi o segmenti di rete. È inoltre possibile configurare impostazioni che consentono di controllare le azioni di individuazione nella rete. Infine, è possibile definire una o più pianificazioni relative all'esecuzione di Individuazione di rete.  

Perché il metodo possa individuare correttamente una risorsa, Individuazione di rete deve identificare l'indirizzo IP e la subnet mask della risorsa. Per identificare la subnet mask di un oggetto vengono usati i metodi seguenti:  

-   **Cache ARP del router:** Individuazione di rete esegue una query nella cache ARP di un router per ottenere informazioni sulla subnet. In genere i dati nella cache ARP di un router hanno una durata breve. Pertanto, quando Individuazione di rete esegue una query nella cache ARP, è possibile che la cache ARP non contenga più informazioni sull'oggetto richiesto.  

-   **DHCP:** Individuazione di rete esegue una query in ogni server DHCP specificato per individuare i dispositivi per cui il server DHCP ha indicato un lease. Individuazione di rete supporta solo i server DHCP che eseguono l'implementazione Microsoft di DHCP.  

-   **Dispositivo SNMP:** Individuazione di rete può eseguire direttamente una query in un dispositivo SNMP. Individuazione di rete può eseguire query in un dispositivo solo se nel dispositivo è installato un agente SNMP locale. È inoltre necessario configurare Individuazione di rete con il nome della community usato dall'agente SNMP.  

Quando rileva un oggetto indirizzabile tramite IP ed è in grado di determinare la subnet mask dell'oggetto, il metodo di individuazione crea un record dei dati di individuazione per l'oggetto. Dal momento che alla rete possono connettersi diversi tipi di dispositivi, Individuazione di rete consente di individuare risorse che non possono supportare il software client di Configuration Manager. Ad esempio, i dispositivi che è possibile individuare ma non gestire includono stampanti e router.  

Individuazione di rete può restituire vari attributi appartenenti al record di individuazione creato. Sono inclusi:  

-   Nome NetBIOS  

-   Indirizzi IP  

-   Dominio risorse  

-   Ruoli del sistema  

-   Nome comunità SNMP  

-   Indirizzi MAC  

L'attività di Individuazione di rete viene registrata nel file **Netdisc.log** in *&lt;PercorsoInstallazione\>\Logs* sul server del sito che esegue l'individuazione.  

 Per altre informazioni su come configurare questo metodo di individuazione, vedere [Configurare i metodi di individuazione per System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md).  

> [!NOTE]  
>  In caso di reti complesse e connessioni con larghezza di banda limitata, è possibile che Individuazione di rete venga eseguito lentamente e generi un notevole traffico di rete. È consigliabile eseguire Individuazione di rete solo quando gli altri metodi non sono in grado di individuare le risorse necessarie. Usare ad esempio Individuazione di rete se è necessario individuare i computer del gruppo di lavoro. Non è possibile individuare i computer del gruppo di lavoro usando altri metodi di individuazione.  

###  <a name="BKMK_NetDiscLevels"></a> Livelli di Individuazione di rete  
Quando si configura Individuazione di rete, è possibile specificare tre diversi livelli:  

|Livello di individuazione|Dettagli|  
|------------------------|-------------|  
|Topologia|Questo livello consente di individuare i router e le subnet, ma non di individuare una subnet mask per gli oggetti.|  
|Topologia e client|Oltre alla topologia, questo livello individua i potenziali client, come computer, e risorse, come stampanti e router. Questo livello di individuazione prova a identificare la subnet mask degli oggetti rilevati.|  
|Topologia, client e sistema operativo client|Oltre alla topologia e ai potenziali client, questo livello prova a individuare il nome e la versione del sistema operativo del computer. Questo livello utilizza il servizio Browser di Windows e le chiamate di rete Windows.|  

 Con ciascun livello incrementale, Individuazione di rete incrementa l'attività e l'utilizzo della larghezza di banda di rete. Prima di attivare tutte le funzioni di Individuazione di rete, è consigliabile valutare il traffico di rete che potrebbe essere generato.  

 Ad esempio, quando si usa Individuazione di rete per la prima volta, è possibile iniziare con il livello di topologia per identificare l'infrastruttura di rete. È quindi possibile riconfigurare Individuazione di rete per individuare oggetti e sistemi operativi dei dispositivi. È anche possibile configurare le impostazioni che limitano Individuazione di rete a un intervallo specifico di segmenti di rete. In questo modo, è possibile individuare oggetti nei percorsi di rete richiesti ed evitare traffico di rete superfluo. È inoltre possibile individuare oggetti provenienti da router perimetrali o esterni alla rete.  

###  <a name="BKMK_NetDiscOptions"></a> Opzioni di Individuazione di rete  
Per abilitare Individuazione di rete per la ricerca di dispositivi indirizzabili tramite IP, è necessario configurare una o più delle opzioni seguenti che consentono di specificare come eseguire le query relative ai dispositivi.  

> [!NOTE]  
>  Individuazione di rete viene eseguito all'interno dell'account computer del server del sito che esegue l'individuazione. Se l'account computer non dispone delle autorizzazioni per un dominio non trusted, nelle configurazioni del dominio e del server DHCP possono verificarsi errori durante l'individuazione delle risorse.  

**DHCP:**  

Specificare ciascun server DHCP in cui si desidera che Individuazione di rete esegua le query. Individuazione di rete supporta solo i server DHCP che eseguono l'implementazione Microsoft di DHCP.  

-   Individuazione di rete recupera le informazioni mediante chiamate a procedura remota al database nel server DHCP.  

-   Individuazione di rete può eseguire query in server DHCP a 32 bit e 64 bit per un elenco dei dispositivi registrati in ogni server.  

-   Per consentire a Individuazione di rete di eseguire correttamente le query in un server DHCP, l'account computer del server che esegue l'individuazione deve appartenere al gruppo DHCP Users nel server DHCP. Questo livello di accesso esiste ad esempio quando viene soddisfatta una delle seguenti condizioni:  

    -   Il server DHCP specificato è il server DHCP del server che esegue l'individuazione.  

    -   Il computer che esegue l'individuazione e il server DHCP sono nello stesso dominio.  

    -   Esiste un trust bidimensionale tra il computer che esegue l'individuazione e il server DHCP.  

    -   Il server del sito appartiene al gruppo DHCP Users.  

-   Quando Individuazione di rete enumera un server DHCP, non vengono sempre rilevati indirizzi IP statici. Individuazione di rete non individua né indirizzi IP appartenenti a un intervallo di indirizzi IP escluso nel server DHCP né indirizzi IP riservati all'assegnazione manuale.  

**Domini:**  

Specificare ciascun dominio in cui si desidera che Individuazione di rete esegua le query.  

-   L'account computer del server del sito che esegue l'individuazione deve avere le autorizzazioni di lettura per i controller di dominio in ogni dominio specificato.  

-   Per individuare i computer del dominio locale, è necessario abilitare il servizio Browser di computer in almeno un computer presente nella stessa subnet del server del sito che esegue Individuazione di rete.  

-   Individuazione di rete è in grado di individuare qualsiasi computer che è possibile visualizzare dal server del sito durante l'esplorazione della rete.  

-   Individuazione di rete recupera l'indirizzo IP e quindi usa una richiesta echo Internet Control Message Protocol per eseguire il ping di ciascun dispositivo rilevato. Il comando **ping** consente di determinare quali computer sono attualmente attivi.  

**Dispositivi SNMP:**  

Specificare ciascun dispositivo SNMP in cui si desidera che l'individuazione di rete esegua le query.  

-   Individuazione di rete recupera il valore ipNetToMediaTable dai dispositivi SNMP che rispondono alla query. Questo valore restituisce matrici di indirizzi IP che corrispondono a computer client o ad altre risorse, come stampanti, router e altri dispositivi indirizzabili tramite IP.  

-   Per eseguire query in un dispositivo, è necessario specificare l'indirizzo IP o il nome NetBIOS del dispositivo.  

-   Se l'individuazione di rete non viene configurata per l'utilizzo del nome comunità del dispositivo, il dispositivo rifiuta la query basata su SNMP.  

###  <a name="BKMK_LimitNetDisc"></a> Limitazione dell'individuazione della rete  
Quando l'individuazione di rete esegue query in un dispositivo SNMP perimetrale rispetto alla rete, possono essere individuate informazioni relative alle subnet e ai dispositivi SNMP esterni alla rete. Usare le informazioni seguenti per limitare l'individuazione della rete configurando i dispositivi SNMP con cui può comunicare l'individuazione e specificando i segmenti di rete in cui eseguire le query.  

**Subnet:**  

Configurare le subnet in cui l'individuazione di rete esegue le query quando vengono utilizzate le opzioni SNMP e DHCP. Queste due opzioni consentono di eseguire ricerche solo nelle subnet abilitate.  

Una richiesta DHCP può ad esempio restituire dispositivi che si trovano in percorsi di tutta la rete. Se si vuole individuare esclusivamente i dispositivi di una subnet specifica, definire e abilitare tale subnet nella scheda **Subnet** della finestra di dialogo **Individuazione di rete - Proprietà**. Quando si specificano e si abilitano le subnet, è necessario limitare attività future di individuazione DHCP e SNMP per le subnet.  

> [!NOTE]  
>  Le configurazioni subnet non limitano gli oggetti individuati dall'opzione di individuazione **Domini**.  

**Nomi community SNMP:**  

Per consentire a Individuazione di rete di eseguire correttamente le query in un dispositivo SNMP, configurare questo metodo con il nome community del dispositivo. Se Individuazione di rete non è configurato con il nome community del dispositivo SNMP, il dispositivo rifiuta la query.  

**Numero massimo di hop:**  

Quando viene configurato il numero massimo di hop router, è necessario limitare il numero di router e segmenti di rete in cui Individuazione di rete può eseguire query usando SNMP.  

Il numero di hop configurato limita il numero di segmenti di rete e dispositivi aggiuntivi in cui Individuazione di rete può eseguire query.  

Ad esempio, un'individuazione solo per topologia con **0** (zero) hop router individua la subnet in cui risiede il server di origine, inclusi gli eventuali router in tale subnet.  

Il diagramma seguente illustra i risultati di una query di Individuazione di rete solo per topologia eseguita nel server 1 con 0 hop router specificati: subnet D e Router 1.  

 ![Immagine dell'individuazione con zero collegamenti al router](media/Disc-0.gif)  

 Il diagramma seguente illustra i risultati di una query di Individuazione di rete per topologia e per client eseguita nel server 1 con 0 hop router specificati: subnet D e Router 1 e tutti i potenziali client della subnet D.  

 ![Immagine dell'individuazione con un collegamento al router](media/Disc-1.gif)  

 Per capire meglio come gli hop router aggiuntivi possono determinare un aumento del numero di risorse di rete individuate, tenere in considerazione la seguente rete:  

 ![Immagine dell'individuazione con due collegamenti al router](media/Disc-2.gif)  

 Eseguendo un'individuazione di rete solo per topologia dal server 1 con un hop router i risultati sono i seguenti:  

-   Router 1 e subnet 10.1.10.0 (con zero hop)  

-   Subnet 10.1.20.0 e 10.1.30.0, subnet A e router 2 (nel primo hop)  

> [!WARNING]  
>  L'aumento del numero di hop router può determinare un aumento significativo delle risorse che è possibile individuare, nonché della larghezza di banda di rete usata da Individuazione di rete.  

##  <a name="bkmk_aboutServer"></a> Individuazione server  
**Configurabile:** no  

Oltre a questi metodi di individuazione configurabili dall'utente, Configuration Manager usa un processo denominato **Individuazione server** (SMS_WINNT_SERVER_DISCOVERY_AGENT). Questo metodo di individuazione consente di creare record di risorse per i computer che sono sistemi del sito, ad esempio un computer configurato come punto di gestione.  

##  <a name="bkmk_shared"></a> Funzionalità comuni dell'individuazione gruppo, sistema e utente Active Directory  
Questa sezione offre informazioni sulle funzionalità comuni dei metodi di individuazione seguenti:  

-   Individuazione gruppo Active Directory  

-   Individuazione sistema Active Directory  

-   individuazione utenti di Active Directory  

> [!NOTE]  
>  Le informazioni contenute in questa sezione non si applicano a Individuazione foresta Active Directory.  

Questi tre metodi di individuazione sono simili in termini di configurazione e funzionamento. Possono individuare computer, utenti e informazioni sulle appartenenze al gruppo delle risorse memorizzate in Active Directory Domain Services. Il processo di individuazione è gestito da un agente di individuazione in esecuzione sul server del sito su ogni sito in cui l'individuazione è configurata per l'esecuzione. È possibile configurare ciascuno di questi metodi di individuazione per effettuare la ricerca in uno o più percorsi di Active Directory. come le istanze di percorso nella foresta locale o nelle foreste remote.  

Quando l'individuazione effettua la ricerca di risorse in una foresta non trusted, l'agente di individuazione deve essere in grado di risolvere quanto segue per avere esito positivo:  

-   Per individuare una risorsa del computer con Individuazione sistema Active Directory, l'agente di individuazione deve essere in grado di risolvere l'FQDN della risorsa. In caso contrario, proverà a risolvere la risorsa con il nome NetBIOS.  

-   Per individuare una risorsa utente o gruppo con Individuazione utente Active Directory o Individuazione gruppo Active Directory, l'agente di individuazione deve essere in grado di risolvere l'FQDN del nome del controller di dominio specificato nel percorso di Active Directory.  

Per ogni percorso specificato, è possibile configurare singole opzioni di ricerca, come l'abilitazione di una ricerca ricorsiva dei contenitori figlio Active Directory del percorso. È anche possibile configurare un account univoco da usare durante la ricerca in tale percorso. Ciò fornisce flessibilità nella configurazione di un metodo di individuazione in un sito per effettuare la ricerca in più percorsi Active Directory in più foreste, senza dover configurare un account singolo che disponga di autorizzazioni per tutti i percorsi.  

Quando ciascuno di questi tre metodi di individuazione viene eseguito su un sito specifico, il server del sito di Configuration Manager in tale sito contatta il controllo di dominio più vicino nella foresta Active Directory specificata per individuare le risorse Active Directory. Il dominio e la foresta possono trovarsi in qualsiasi modalità Active Directory supportata. L'account che si assegna a ogni istanza di percorso deve avere l'autorizzazione di accesso **Lettura** ai percorsi Active Directory specificati.

L'individuazione effettua la ricerca degli oggetti nei percorsi specificati e quindi prova a raccogliere informazioni su tali oggetti. Viene creato un record dei dati di individuazione quando possono essere individuate sufficienti informazioni su una risorsa. Le informazioni richieste variano a seconda del metodo di individuazione utilizzato.  

Se si configura lo stesso metodo di individuazione per poterlo eseguire su siti diversi di Configuration Manager e poter quindi eseguire una query sui server di Active Directory locali, è possibile configurare ogni sito usando una sola serie di opzioni di individuazione. Poiché i dati di individuazione vengono condivisi con ogni sito della gerarchia, evitare la sovrapposizione tra tali configurazioni per individuare in modo efficiente ogni risorsa una volta sola.

Per ambienti di dimensioni più limitate, si può prendere in considerazione l'esecuzione di ogni metodo di individuazione su un solo sito della gerarchia per ridurre il carico amministrativo e la possibilità che vengano individuate più volte le stesse risorse. Quando si riduce a icona il numero di siti che eseguono l'individuazione, è possibile ridurre la larghezza di banda complessiva usata dall'individuazione. È inoltre possibile ridurre il numero totale di record dei dati di individuazione che vengono creati e devono essere elaborati dai server del sito.  

Molte delle configurazioni del metodo di individuazione sono di chiara interpretazione. Usare le sezioni seguenti per approfondimenti sulle opzioni di individuazione che possono richiedere informazioni aggiuntive prima di essere configurate.  

È possibile usare le opzioni seguenti con più metodi di individuazione Active Directory:  

-   [Individuazione differenziale](#bkmk_delta)  

-   [Filtrare i record del computer non aggiornati usando l'accesso al dominio](#bkmk_stalelogon)  

-   [Filtrare i record non aggiornati usando la password del computer](#bkmk_stalepassword)  

-   [Cercare attributi di Active Directory personalizzati](#bkmk_customAD)  

###  <a name="bkmk_delta"></a> Individuazione differenziale  
Disponibile per:  

-   Individuazione gruppo Active Directory  

-   Individuazione sistema Active Directory  

-   Individuazione utente Active Directory  

L'individuazione differenziale non è un metodo di individuazione indipendente, ma un'opzione disponibile per i metodi di individuazione applicabili. L'individuazione differenziale esegue la ricerca di specifici attributi di Active Directory che sono stati modificati dopo l'ultimo ciclo di individuazione completa del metodo applicabile. Le modifiche degli attributi vengono inviate al database di Configuration Manager per aggiornare il record di individuazione della risorsa.  

Per impostazione predefinita, l'individuazione differenziale viene eseguita in base a un ciclo da cinque minuti, molto più di frequente rispetto alla pianificazione tipica per un ciclo di individuazione completa.  È possibile eseguire questo ciclo in modo frequente perché l'individuazione differenziale usa un numero inferiore di server del sito e di risorse di rete rispetto a un ciclo di individuazione completa. Quando si usa l'individuazione differenziale, è possibile ridurre la frequenza del ciclo di individuazione completa per tale metodo di individuazione.  

Di seguito sono elencale le modifiche più comuni rilevate dall'individuazione differenziale:  

-   Nuovi computer o utenti aggiunti ad Active Directory  

-   Modifiche apportate alle informazioni utente e computer di base  

-   Nuovi computer o utenti aggiunti a un gruppo  

-   Computer o utenti rimossi da un gruppo  

-   Modifiche apportate agli oggetti del gruppo di sistema  

Anche se può rilevare le nuove risorse e le modifiche apportate all'appartenenza al gruppo, l'individuazione differenziale non può determinare se una risorsa è stata eliminata da Active Directory. I record dei dati di individuazione creati dall'individuazione differenziale vengono elaborati in modo simile ai record dei dati di individuazione creati da un ciclo di individuazione completa.  

Configurare l'individuazione differenziale nella scheda **Pianificazione del polling** delle proprietà di ciascun metodo di individuazione.  

###  <a name="bkmk_stalelogon"></a> Filtrare i record del computer non aggiornati usando l'accesso al dominio  
Disponibile per:  

-   Individuazione gruppo Active Directory  

-   Individuazione sistema Active Directory  

È possibile configurare l'individuazione per escludere i computer con record del computer non aggiornati in base all'ultimo accesso al dominio del computer. Quando è abilitata questa opzione, Individuazione sistema Active Directory valuta ogni computer identificato. L'individuazione gruppo Active Directory valuta ogni computer membro di un gruppo rilevato.  

Per usare questa opzione:  

-   I computer devono essere configurati in modo che sia eseguito l'aggiornamento dell'attributo **lastLogonTimeStamp** in Active Directory Domain Services.  

-   Il livello di funzionalità del dominio di Active Directory deve essere impostato su Windows Server 2003 o versione successiva.  

Quando si configura il periodo di tempo dopo l'ultimo accesso per questa impostazione, considerare l'intervallo per la replica tra i controller di dominio.  

È possibile configurare i filtri nella scheda **Opzione** delle finestre di dialogo **Individuazione sistema Active Directory - Proprietà** e **Individuazione gruppo Active Directory - Proprietà**. Scegliere l'opzione **Individua solo computer che hanno effettuato l'accesso a un dominio in un periodo di tempo specifico**.  

> [!WARNING]  
>  Quando si configura questo filtro e si **filtrano i record non aggiornati in base alla password del computer**, i computer che soddisfano i criteri di uno dei due filtri vengono esclusi dall'individuazione.  

###  <a name="bkmk_stalepassword"></a> Filtrare i record non aggiornati usando la password del computer  
Disponibile per:  

-   Individuazione gruppo Active Directory  

-   Individuazione sistema Active Directory  

È possibile configurare l'individuazione per escludere i computer con record del computer non aggiornati in base all'ultimo aggiornamento della password dell'account computer da parte dal computer. Quando è abilitata questa opzione, Individuazione sistema Active Directory valuta ogni computer identificato. L'individuazione gruppo Active Directory valuta ogni computer membro di un gruppo rilevato.  

Per usare questa opzione:  

-   I computer devono essere configurati in modo che sia eseguito l'aggiornamento dell'attributo **pwdLastSet** in Active Directory Domain Services.  

Durante la configurazione di questa opzione, prendere in considerazione l'intervallo di aggiornamento a questo attributo oltre all'intervallo di replica tra i controller di dominio.  

È possibile configurare i filtri nella scheda **Opzione** delle finestre di dialogo **Individuazione sistema Active Directory - Proprietà** e **Individuazione gruppo Active Directory - Proprietà**. Scegliere l'opzione **Individua solo computer che hanno aggiornato la password dell'account computer in un periodo di tempo specifico**.  

> [!WARNING]  
>  Quando si configura questo filtro e si **filtrano i record non aggiornati in base all'accesso al dominio**, i computer che soddisfano i criteri di uno dei due filtri vengono esclusi dall'individuazione.  

###  <a name="bkmk_customAD"></a> Cercare attributi di Active Directory personalizzati  
 Disponibile per:  

-   Individuazione sistema Active Directory  

-   individuazione utenti di Active Directory  

Ogni metodo di individuazione supporta un elenco univoco di attributi di Active Directory che possono essere individuati.  

È possibile visualizzare e configurare l'elenco degli attributi personalizzati nella scheda **Attributi di Active Directory** nelle finestre di dialogo **Individuazione sistema Active Directory - Proprietà** e **Individuazione utente Active Directory - Proprietà**.  

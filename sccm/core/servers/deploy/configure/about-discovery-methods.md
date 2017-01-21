---
title: Metodi di individuazione | Microsoft Docs
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed931751-18f2-4230-a09e-a0a329fbfa1c
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 223ebc3009b33c43818636a9e19b9b482619550b

---
# <a name="about-discovery-methods-for-system-center-configuration-manager"></a>Informazioni sui metodi di individuazione per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Ogni metodo di individuazione di System Center Configuration Manager consente di individuare dispositivi diversi nella rete o dispositivi e utenti Active Directory. Per usare un metodo di individuazione in modo efficiente, è importante sapere quali sono le configurazioni disponibili e le rispettive limitazioni.  

##  <a name="a-namebkmkaboutforesta-active-directory-forest-discovery"></a><a name="bkmk_aboutForest"></a> Individuazione foresta Active Directory  
 **Configurabile:** sì  

 **Abilitata per impostazione predefinita:** no  

 Per eseguire questo metodo è possibile usare gli **account** seguenti:  

-   **Account di individuazione foresta Active Directory** (definito dall'utente)  

-   **Account computer** del server del sito  

A differenza di altri metodi di individuazione Active Directory, l'individuazione foresta Active Directory non individua le risorse che è possibile gestire. Questo metodo individua invece i percorsi di rete che sono configurati in Active Directory e li può convertire in limiti da usare in tutta la gerarchia.  

Durante la sua esecuzione, il metodo cerca la foresta Active Directory locale, tutte le foreste trusted e tutte le altre foreste configurate nel nodo **Foreste Active Directory** della console di Configuration Manager.  

Usare l'individuazione foresta Active Directory per eseguire le operazioni seguenti:  

-   Individuare siti e subnet Active Directory e creare i limiti di Configuration Manager sulla base dei percorsi di rete individuati  

-   Identificare le supernet assegnate a un sito Active Directory e convertire la supernet in un limite di intervallo di indirizzi IP  

-   Pubblicare nei Servizi di dominio Active Directory di una foresta quando la pubblicazione in tale foresta è abilitata e l'account foresta Active Directory specificato dispone di autorizzazioni per quella foresta  

È possibile gestire l'individuazione foresta Active Directory nella console di Configuration Manager dai nodi seguenti in **Configurazione della gerarchia** nell'area di lavoro **Amministrazione**:  

-   **Metodi di individuazione**: qui è possibile abilitare l'individuazione foresta Active Directory affinché venga eseguita nel sito di livello superiore della gerarchia. È inoltre possibile specificare una pianificazione semplice per l'esecuzione dell'individuazione e configurarla per creare automaticamente limiti dalle subnet IP e dai siti di Active Directory individuati. L'individuazione foresta Active Directory non può essere eseguita in un sito primario figlio o in un sito secondario.  

-   **Foreste Active Directory**: qui è possibile configurare le foreste Active Directory aggiuntive che si desidera individuare, specificare l'account da utilizzare come account foresta Active Directory per ciascuna foresta e configurare la pubblicazione in ciascun foresta. È anche possibile monitorare il processo di individuazione e aggiungere subnet IP e siti Active Directory a Configuration Manager come limiti e membri di gruppi di limiti.  

Per configurare la pubblicazione delle foreste Active Directory per ogni sito della gerarchia, connettere la console di Configuration Manager al sito principale della gerarchia. La scheda **Pubblicazione** nella finestra di dialogo **Proprietà** di un sito di Active Directory è in grado di visualizzare esclusivamente il sito corrente e i relativi siti figlio. Quando la pubblicazione è abilitata per una foresta e lo schema di tale foresta viene esteso per Configuration Manager, vengono pubblicate le informazioni seguenti per ogni sito abilitato per la pubblicazione in quella foresta Active Directory:  

-    **SMS-Site-&lt;codice sito>**

-   **SMS-MP-&lt;codice sito>-&lt;nome del server nel sistema del sito>**  

-   **SMS-SLP-&lt;codice sito>-&lt;nome del server nel sistema del sito>**  

-   **SMS-&lt;codice sito>-&lt;nome sito o subnet Active Directory>**  

> [!NOTE]  
>  I siti secondari usano sempre l'account computer del server del sito secondario per la pubblicazione in Active Directory. Se si desidera che i siti secondari pubblichino in Active Directory, verificare che l'account computer del server del sito secondario disponga delle autorizzazioni per la pubblicazione in Active Directory. Un sito secondario non è in grado di pubblicare dati in una foresta non trusted.  

> [!CAUTION]  
>  Quando l'opzione per la pubblicazione di un sito in una foresta Active Directory viene deselezionata, tutte le informazioni pubblicate precedentemente per il sito, compresi i ruoli del sistema del sito disponibili, vengono rimosse da Active Directory della foresta.  

Le azioni di individuazione foresta Active Directory vengono registrate nei log seguenti:  

-   Tutte le azioni, comprese le azioni di eccezione relative alla pubblicazione, vengono registrate nel file **ADForestDisc.Log** nella cartella **&lt;InstallationPath>\Logs** nel server del sito.  

-   Le azioni di pubblicazione dell'individuazione foresta Active Directory vengono registrate nei file **hman.log** e **sitecomp.log** nella cartella **&lt;InstallationPath>\Logs** del server del sito.  

Per altre informazioni su come configurare questo metodo di individuazione, vedere [Configure discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md) (Configurare i metodi di individuazione per System Center Configuration Manager)  

##  <a name="a-namebkmkaboutgroupa-active-directory-group-discovery"></a><a name="bkmk_aboutGroup"></a> Individuazione gruppo Active Directory  
**Configurabile:** sì  

**Abilitata per impostazione predefinita:** no  

Per eseguire questo metodo è possibile usare gli **account** seguenti:  

-   **Account di individuazione gruppo Active Directory** (definito dall'utente)  

-   **Account computer** del server del sito  

> [!TIP]  
>  Oltre alle informazioni disponibili in questa sezione, vedere [Funzionalità comuni dell'individuazione gruppo, sistema e utente Active Directory](#bkmk_shared).  

Usare questo metodo per cercare Active Directory Domain Services (AD DS) e individuare:  

-   Gruppi di sicurezza locali, globali e universali  

-   Appartenenza di gruppi  

-   Informazioni limitate sui computer e utenti di membri di gruppi, anche quando tali computer e utenti non sono stati precedentemente individuati da un altro metodo di individuazione  

Questo metodo di individuazione ha lo scopo di identificare i gruppi e le relazioni di gruppo dei membri dei gruppi. Per impostazione predefinita, vengono individuati solo i gruppi di protezione. Se si vuole individuare anche l'appartenenza dei gruppi di distribuzione, è necessario selezionare la casella di controllo per l'opzione **Individua l'appartenenza dei gruppi di distribuzione** nella scheda **Opzione** della finestra di dialogo Active Directory Group Discovery Properties (Proprietà individuazione gruppo Active Directory).  

L'individuazione gruppo Active Directory non supporta gli attributi estesi di Active Directory che possono essere identificati con l'individuazione sistema Active Directory o l'individuazione utente Active Directory. Poiché questo metodo di individuazione non è ottimizzato per l'individuazione di risorse computer e utente, eseguire tale metodo dopo aver eseguito l'individuazione sistema Active Directory o l'individuazione utente Active Directory. Questo metodo crea infatti un record dei dati di individuazione completo per i gruppi, ma un record dei dati di individuazione limitato per computer e utenti che sono membri di gruppi.  

È possibile configurare gli ambiti di individuazione seguenti per controllare come questo metodo deve ricercare le informazioni:  

-   **Location**: utilizzare un percorso se si desidera effettuare la ricerca di uno o più contenitori di Active Directory. Tale opzione dell'ambito supporta una ricerca ricorsiva dei contenitori di Active Directory specificati che effettua anche la ricerca di ciascun contenitore figlio all'interno del contenitore specificato. Questo processo continua finché non vengono più trovati contenitori figlio.  

-   **Gruppi**: utilizzare i gruppi se si desidera effettuare la ricerca di uno o più gruppi Active Directory specifici. È possibile configurare il **Dominio Active Directory** per utilizzare il dominio e la foresta predefiniti oppure limitare la ricerca a un singolo controller di dominio. Inoltre, è possibile specificare uno o più gruppi in cui effettuare la ricerca. Se non si specifica almeno un gruppo, viene effettuata la ricerca in tutti i gruppi trovati nel percorso specificato del **Dominio Active Directory** .  

> [!CAUTION]  
>  Quando si configura un ambito di individuazione, selezionare solo i gruppi che è necessario individuare. Infatti, l'individuazione gruppo Active Directory tenta di individuare ogni membro di ciascun gruppo nell'ambito di individuazione. L'individuazione di gruppi di grandi dimensioni può richiedere un uso estensivo della larghezza di banda e di risorse Active Directory.  

> [!NOTE]  
>  Per poter creare raccolte basate sugli attributi estesi di Active Directory e garantire così risultati di individuazione precisi per computer e utenti, è prima necessario eseguire l'individuazione sistema o utente Active Directory a seconda di quel che si vuole individuare.  

Le azioni dell'individuazione foresta Active Directory vengono registrate nel file **adsgdis.log** nella cartella **&lt;InstallationPath\>\LOGS** del server del sito.  

Per altre informazioni su come configurare questo metodo di individuazione, vedere [Configure discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md) (Configurare i metodi di individuazione per System Center Configuration Manager)  

##  <a name="a-namebkmkaboutsystema-active-directory-system-discovery"></a><a name="bkmk_aboutSystem"></a>Individuazione sistema Active Directory  
**Configurabile:** sì  

**Abilitata per impostazione predefinita:** no  

Per eseguire questo metodo è possibile usare gli **account** seguenti:  

-   **Account di individuazione sistema Active Directory** (definito dall'utente)  

-   **Account computer** del server del sito  

> [!TIP]  
>  Oltre alle informazioni disponibili in questa sezione, vedere [Funzionalità comuni dell'individuazione gruppo, sistema e utente Active Directory](#bkmk_shared).  

Usare questo metodo di individuazione per cercare i percorsi di Active Directory Domain Services (AD DS) per le risorse del computer che possono essere usate per creare raccolte e query. È anche possibile installare il client di Configuration Manager in un dispositivo individuato usando l'installazione push client.  

Per impostazione predefinita, questo metodo individua informazioni di base relative al computer, tra cui:  

-   Nome computer  

-   Il sistema operativo e la sua versione  

-   Il nome del contenitore Active Directory  

-   Indirizzo IP  

-   Sito di Active Directory  

-   Il timestamp dell'ultimo accesso  

Per creare correttamente un record dei dati di individuazione (DDR) per un computer, l'individuazione sistema Active Directory deve essere in grado di identificare l'account computer e di risolvere correttamente il nome del computer in un indirizzo IP.  

È possibile visualizzare l'elenco predefinito completo degli attributi oggetto restituiti dall'individuazione sistema Active Directory e configurare il metodo affinché vengano individuati altri attributi, come gli attributi estesi, nella finestra di dialogo **Active Directory System Discovery Properties** (Proprietà di individuazione sistema Active Directory) della scheda **Attributi di Active Directory**.  

Le azioni dell'individuazione sistema Active Directory vengono registrate nel file **adsysdis.log** nella cartella **&lt;InstallationPath\>\LOGS** del server del sito.  

Per altre informazioni su come configurare questo metodo di individuazione, vedere [Configure discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md) (Configurare i metodi di individuazione per System Center Configuration Manager)  

##  <a name="a-namebkmkaboutusera-active-directory-user-discovery"></a><a name="bkmk_aboutUser"></a> Individuazione utenti di Active Directory  
**Configurabile:** sì  

**Abilitata per impostazione predefinita:** no  

Per eseguire questo metodo è possibile usare gli **account** seguenti:  

-   **Account di individuazione utente Active Directory** (definito dall'utente)  

-   **Account computer** del server del sito  

> [!TIP]  
>  Oltre alle informazioni disponibili in questa sezione, vedere [Funzionalità comuni dell'individuazione gruppo, sistema e utente Active Directory](#bkmk_shared).  

Usare questo metodo di individuazione per cercare Active Directory Domain Services (AD DS) e identificare gli account utente e gli attributi associati.  Per impostazione predefinita, questo metodo individua informazioni di base relative all'account utente, tra cui:  

-   Nome utente  

-   Il nome utente univoco (include il nome di dominio)  

-   Dominio  

-   I nomi dei contenitori Active Directory  

È possibile visualizzare l'elenco predefinito completo degli attributi oggetto restituiti dall'individuazione utente Active Directory e configurare il metodo affinché vengano individuati altri attributi, come gli attributi estesi, nella finestra di dialogo **Active Directory User Discovery Properties** (Proprietà di individuazione utente Active Directory) nella scheda **Attributi di Active Directory**.  

Le azioni dell'individuazione utente Active Directory vengono registrate nel file **adusrdis.log** nella cartella **&lt;InstallationPath\>\LOGS** del server del sito.  

Per altre informazioni su come configurare questo metodo di individuazione, vedere [Configure discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md) (Configurare i metodi di individuazione per System Center Configuration Manager)  

##  <a name="a-namebkmkaboutheartbeata-heartbeat-discovery"></a><a name="bkmk_aboutHeartbeat"></a> Individuazione heartbeat  
**Configurabile:** sì  

**Abilitata per impostazione predefinita:** sì  

Per eseguire questo metodo è possibile usare gli **account** seguenti:  

-   **Account computer** del server del sito  

L'individuazione heartbeat è diversa dagli altri metodi di individuazione di Configuration Manager. È infatti abilitata per impostazione predefinita e viene eseguita in ogni computer client, anziché sul server del sito, per creare un record dei dati di individuazione. Per i client di dispositivi mobili, il DDR viene creato dal punto di gestione utilizzato dal client di dispositivi mobili.  Per gestire il record del database dei client di Configuration Manager, non disabilitare l'individuazione heartbeat.  Oltre a consentire la gestione del record del database, questo metodo può forzare l'individuazione di un computer come nuovo record di risorse oppure ripopolare il record del database di un computer che è stato eliminato dal database.  

L'individuazione heartbeat viene eseguita in base a una pianificazione configurata per tutti i client della gerarchia oppure, se chiamata manualmente, in un client specifico tramite l'esecuzione del **Ciclo di recupero dati di rilevamento** nella scheda **Azione** in un programma di Configuration Manager del client. La pianificazione predefinita per l'individuazione heartbeat è impostata per l'esecuzione ogni 7 giorni. Se viene modificato l'intervallo di individuazione heartbeat, verificare che l'esecuzione sia più frequente rispetto all'attività di manutenzione del sito **Elimina dati di individuazione obsoleti**, che consente di eliminare i record client inattivi dal database del sito. È possibile configurare l'attività **Elimina dati di individuazione obsoleti** solo per i siti primari.  

Quando viene eseguita l'individuazione heartbeat, viene creato un record dei dati di individuazione contenente le informazioni correnti del client. Il client copia quindi questo file di piccole dimensioni di circa 1 KB in un punto di gestione in modo che sia possibile elaborarlo da un sito primario.  Il file contiene le informazioni seguenti:  

-   Percorso di rete  

-   Nome NetBIOS  

-   Versione dell'agente client  

-   Dettagli sullo stato operativo  

L'individuazione heartbeat è l'unico metodo di individuazione che offre dettagli relativi allo stato di installazione client, in quanto aggiorna l'attributo client di una risorsa di sistema impostando il valore **Sì**.  

> [!NOTE]  
>  Anche se l'individuazione heartbeat è disattivata, i DDR vengono comunque creati e inviati per i client di dispositivi mobili attivi. In questo modo, l'attività **Elimina dati di individuazione obsoleti** non influisce sui dispositivi mobili attivi. Infatti, quando l'attività **Elimina dati di individuazione obsoleti** elimina un record del database per un dispositivo mobile, revoca anche il certificato del dispositivo e blocca la connessione del dispositivo mobile ai punti di gestione.  

Le azioni dell'individuazione heartbeat vengono registrate nei percorsi seguenti:  

-   Per i client computer, le azioni dell'individuazione heartbeat vengono registrate nel client, nel file **InventoryAgent.log** nella cartella *%Windir%\CCM\Logs*.  

-   Per i dispositivi mobili, le azioni dell'individuazione heartbeat vengono registrate nel file **DMPRP.log** della cartella *%Program Files%\CCM\Logs* del punto di gestione utilizzato dal client di dispositivi mobili.  

Per altre informazioni su come configurare questo metodo di individuazione, vedere [Configure discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md) (Configurare i metodi di individuazione per System Center Configuration Manager)  

##  <a name="a-namebkmkaboutnetworka-network-discovery"></a><a name="bkmk_aboutNetwork"></a> Individuazione rete  
**Configurabile:** sì  

**Abilitata per impostazione predefinita:** no  

Per eseguire questo metodo è possibile usare gli **account** seguenti:  

-   **Account computer** del server del sito  

Usare questo metodo per individuare la topologia della rete e i dispositivi di rete che hanno un indirizzo IP. L'individuazione di rete cerca nella rete le risorse con IP abilitato eseguendo query in server che eseguono un'implementazione Microsoft di DHCP, cache ARP (Address Resolution Protocol) nei router, dispositivi con SNMP abilitato e domini Active Directory.  

Per usare l'individuazione della rete, è necessario prima specificare il **livello** di individuazione da eseguire. È inoltre possibile configurare uno o più meccanismi di individuazione che consentono all'individuazione di rete di eseguire query relative a dispositivi o segmenti di rete. È inoltre possibile configurare impostazioni che consentono di controllare le azioni di individuazione nella rete. Infine, è possibile definire una o più pianificazioni relative all'esecuzione dell'individuazione di rete.  

Perché il metodo possa individuare correttamente una risorsa, l'individuazione della rete deve identificare l'indirizzo IP e la subnet mask della risorsa. Per identificare la subnet mask di un oggetto vengono usati i metodi seguenti:  

-   **Cache ARP del router:** l'individuazione della rete esegue una query nella cache ARP di un router per ottenere informazioni sulla subnet. In genere i dati nella cache ARP di un router hanno una durata breve. Quando l'individuazione della rete esegue una query nella cache ARP, è pertanto possibile che la cache ARP non contenga più informazioni sull'oggetto richiesto.  

-   **DHCP:** l'individuazione della rete esegue una query in ogni server DHCP specificato per individuare i dispositivi per cui il server DHCP ha indicato un lease. L'individuazione di rete supporta solo i server DHCP che eseguono l'implementazione Microsoft di DHCP.  

-   **Dispositivo SNMP:** l'individuazione della rete può eseguire direttamente una query in un dispositivo SNMP. L'individuazione di rete può eseguire query in un dispositivo solo se nel dispositivo è installato un agente SNMP locale. È inoltre necessario configurare l'individuazione di rete per l'utilizzo del nome comunità utilizzato dall'agente SNMP.  

Quando l'individuazione rileva un oggetto indirizzabile tramite IP ed è in grado di determinare la subnet mask degli oggetti, viene creato un record dei dati di individuazione (DDR) per l'oggetto. Dal momento che alla rete possono connettersi diversi tipi di dispositivi, l'individuazione della rete consente di individuare risorse che non possono supportare il software client di Configuration Manager. Ad esempio, i dispositivi che è possibile individuare ma non gestire includono stampanti e router.  

L'individuazione di rete può restituire vari attributi appartenenti al record di individuazione creato. Sono inclusi:  

-   Nome NetBIOS  

-   Indirizzi IP  

-   Dominio risorse  

-   Ruoli del sistema  

-   Nome comunità SNMP  

-   Indirizzi MAC  

L'attività di individuazione della rete viene registrata nel file **Netdisc.log** in **&lt;InstallationPath\>\Logs** sul server del sito che esegue l'individuazione.  

 Per altre informazioni su come configurare questo metodo di individuazione, vedere [Configure discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-discovery-methods.md) (Configurare i metodi di individuazione per System Center Configuration Manager).  

> [!NOTE]  
>  Reti complesse e connessioni con larghezza di banda bassa possono provocare un'esecuzione lenta dell'individuazione della rete e generare un traffico di rete notevole. È consigliabile eseguire l'individuazione di rete solo quando gli altri metodi di individuazione non sono in grado di individuare le risorse che è necessario individuare. Utilizzare ad esempio l'individuazione di rete se è necessario individuare i computer del gruppo di lavoro. Non è possibile individuare i computer del gruppo di lavoro mediante altri metodi di individuazione.  

###  <a name="a-namebkmknetdisclevelsa-levels-of-network-discovery"></a><a name="BKMK_NetDiscLevels"></a> Livelli di individuazione della rete  
Quando viene configurata l'individuazione di rete, è possibile specificare tre diversi livelli di individuazione:  

|Livello di individuazione|Dettagli|  
|------------------------|-------------|  
|Topologia|Questo livello consente di individuare i router e le subnet, ma non di individuare una subnet mask per gli oggetti.|  
|Topologia e client|Oltre alla topologia, questo livello individua i potenziali clienti come computer e risorse quali stampanti e router. Questo livello di individuazione tenta di identificare la subnet mask degli oggetti rilevati.|  
|Topologia, client e sistema operativo client|Oltre alla topologia e ai potenziali clienti, questo livello tenta di individuare il nome e la versione del sistema operativo del computer. Questo livello utilizza il servizio Browser di Windows e le chiamate di rete Windows.|  

 Con ciascun livello incrementale, l'individuazione di rete incrementa l'attività e l'utilizzo della larghezza di banda di rete. Prima di attivare tutte le funzioni dell'individuazione di rete è consigliabile valutare il traffico di rete che potrebbe essere generato.  

 Ad esempio, quando si utilizza per la prima volta l'individuazione di rete, è possibile iniziare con il livello di topologia per identificare l'infrastruttura di rete. Quindi, è possibile riconfigurare l'individuazione di rete per individuare oggetti e sistemi operativi dei dispositivi. È inoltre possibile configurare impostazioni per limitare l'individuazione di rete a un intervallo specifico di segmenti di rete, individuare oggetti nei percorsi di rete richiesti ed evitare traffico di rete superfluo o l'individuazione di oggetti provenienti da router perimetrali o esterni alla rete.  

###  <a name="a-namebkmknetdiscoptionsa-network-discovery-options"></a><a name="BKMK_NetDiscOptions"></a> Opzioni di individuazione della rete  
Per abilitare l'individuazione della rete alla ricerca di dispositivi indirizzabili tramite IP, è necessario configurare una o più delle opzioni seguenti che consentono di specificare come eseguire le query relative ai dispositivi.  

> [!NOTE]  
>  L'individuazione di rete viene eseguita all'interno dell'account computer del server del sito che esegue l'individuazione. Se l'account computer non dispone delle autorizzazioni per un dominio non attendibile, nelle configurazioni del dominio e del server DHCP possono verificarsi errori durante l'individuazione delle risorse.  

**DHCP:**  

Specificare ciascun server DHCP in cui si desidera che l'individuazione di rete esegua le query. L'individuazione della rete supporta solo i server DHCP che eseguono l'implementazione Microsoft di DHCP.  

-   L'individuazione di rete recupera le informazioni mediante chiamate a procedura remota al database nel server DHCP.  

-   L'individuazione di rete può eseguire query in server DHCP a 32 bit e 64 bit per un elenco dei dispositivi registrati in ogni server.  

-   Per consentire all'individuazione di rete di eseguire correttamente le query in un server DHCP, l'account computer del server che esegue l'individuazione deve appartenere al gruppo DHCP Users nel server DHCP. Questo livello di accesso esiste ad esempio quando viene soddisfatta una delle seguenti condizioni:  

    -   Il server DHCP specificato è il server DHCP del server che esegue l'individuazione.  

    -   Il computer che esegue l'individuazione e il server DHCP sono nello stesso dominio.  

    -   Esiste un trust bidimensionale tra il computer che esegue l'individuazione e il server DHCP.  

    -   Il server del sito appartiene al gruppo DHCP Users.  

-   Quando l'individuazione di rete enumera un server DHCP, non vengono sempre rilevati indirizzi IP statici. L'individuazione di rete non individua indirizzi IP appartenenti a un intervallo di indirizzi IP escluso nel server DHCP e non individua indirizzi IP riservati all'assegnazione manuale.  

**Domini:**  

Specificare ciascun dominio in cui si desidera che l'individuazione di rete esegua le query.  

-   L'account computer del server del sito che esegue l'individuazione deve avere le autorizzazioni di lettura per i controller di dominio in ogni dominio specificato.  

-   Per individuare i computer del dominio locale, è necessario attivare il servizio Browser di computer in almeno un computer localizzato nella stessa subnet del server del sito che esegue l'individuazione della rete.  

-   L'individuazione della rete può individuare qualsiasi computer che è possibile visualizzare dal server del sito durante l'esplorazione della rete.  

-   L'individuazione di rete recupera l'indirizzo IP e quindi utilizza una richiesta echo Internet Control Message Protocol per eseguire il ping di ciascun dispositivo rilevato. Il comando **ping** consente di determinare quali computer sono attualmente attivi.  

**Dispositivi SNMP:**  

Specificare ciascun dispositivo SNMP in cui si desidera che l'individuazione di rete esegua le query.  

-   L'individuazione della rete recupera il valore ipNetToMediaTable dai dispositivi SNMP che rispondono alla query. Questo valore restituisce matrici di indirizzi IP che corrispondono a computer client o altre risorse, come stampanti, router e altri dispositivi indirizzabili tramite IP.  

-   Per eseguire query in un dispositivo, è necessario specificare l'indirizzo IP o il nome NetBIOS del dispositivo.  

-   Se l'individuazione di rete non viene configurata per l'utilizzo del nome comunità del dispositivo, il dispositivo rifiuta la query basata su SNMP.  

###  <a name="a-namebkmklimitnetdisca-limiting-network-discovery"></a><a name="BKMK_LimitNetDisc"></a> Limitazione dell'individuazione della rete  
Quando l'individuazione di rete esegue query in un dispositivo SNMP perimetrale rispetto alla rete, possono essere individuate informazioni relative alle subnet e ai dispositivi SNMP esterni alla rete. Usare le informazioni seguenti per limitare l'individuazione della rete configurando i dispositivi SNMP con cui può comunicare l'individuazione e specificando i segmenti di rete in cui eseguire le query.  

**Subnet:**  

Configurare le subnet in cui l'individuazione di rete esegue le query quando vengono utilizzate le opzioni SNMP e DHCP. Queste due opzioni eseguono ricerche solo nelle subnet abilitate.  

Una richiesta DHCP può ad esempio restituire dispositivi che si trovano in percorsi di tutta la rete. Se si desidera individuare esclusivamente i dispositivi di una subnet specifica, specificare e abilitare tale subnet nella scheda **Subnet** della finestra di dialogo **Proprietà dell'individuazione della rete** . Quando si specificano e si abilitano le subnet, è necessario limitare operazioni future di individuazione DHCP e SNMP per le subnet.  

> [!NOTE]  
>  Le configurazioni subnet non limitano gli oggetti individuati dall'opzione di individuazione Domini.  

**Nomi community SNMP:**  

Per consentire all'individuazione di rete di eseguire correttamente le query in un dispositivo SNMP, configurare l'individuazione di rete con il nome comunità del dispositivo. Se l'individuazione di rete non è configurata con il nome comunità del dispositivo SNMP, il dispositivo rifiuta la query.  

**Numero massimo di hop:**  

Quando viene configurato il numero massimo di hop router, è necessario limitare il numero di router e segmenti di rete in cui l'individuazione di rete può eseguire query utilizzando SNMP.  

-   Il numero di hop configurato limita il numero di segmenti di rete e dispositivi aggiuntivi in cui l'individuazione di rete può eseguire query.  

 Un'individuazione solo per topologia con **0** (zero) hop router individua ad esempio la subnet in cui risiede il server di origine e comprende tutti i router della subnet.  

Il seguente diagramma illustra i risultati di un'individuazione di rete solo per topologia quando viene eseguita nel server 1 con 0 hop router specificati: subnet D e Router 1.  

 ![Immagine dell'individuazione con zero collegamenti al router](media/Disc-0.gif)  

 Il seguente diagramma illustra i risultati di un'individuazione di rete per topologia e per il client quando viene eseguita nel server 1 con 0 hop router specificati: subnet D e Router 1 e tutti i potenziali client della subnet D.  

 ![Immagine dell'individuazione con un collegamento al router](media/Disc-1.gif)  

 Per capire meglio come gli hop router aggiuntivi possono determinare un aumento del numero di risorse di rete individuate, tenere in considerazione la seguente rete:  

 ![Immagine dell'individuazione con due collegamenti al router](media/Disc-2.gif)  

 Eseguendo un'individuazione di rete solo per topologia dal server 1 con un hop router i risultati sono i seguenti:  

-   Router 1 e subnet 10.1.10.0 (con zero hop).  

-   Subnet 10.1.20.0 e 10.1.30.0, subnet A, e router 2 (nel primo hop).  

> [!WARNING]  
>  L'aumento del numero di hop router può determinare un aumento significativo delle risorse che è possibile individuare, nonché della larghezza di banda di rete utilizzata dall'individuazione di rete.  

##  <a name="a-namebkmkaboutservera-server-discovery"></a><a name="bkmk_aboutServer"></a> Individuazione server  
**Configurabile:** no  

Oltre a questi metodi di individuazione configurabili dall'utente, Configuration Manager usa anche un processo denominato **Individuazione server** (SMS_WINNT_SERVER_DISCOVERY_AGENT). Questo metodo di individuazione consente di creare record di risorse per i computer che sono sistemi del sito, ad esempio un computer configurato come un punto di gestione.  

##  <a name="a-namebkmkshareda-common-features-of-active-directory-group-system-and-user-discovery"></a><a name="bkmk_shared"></a> Funzionalità comuni dell'individuazione gruppo, sistema e utente Active Directory  
Questa sezione offre informazioni sulle funzionalità comuni dei metodi di individuazione seguenti:  

-   Individuazione gruppo Active Directory  

-   Individuazione sistema Active Directory  

-   individuazione utenti di Active Directory  

> [!NOTE]  
>  Le informazioni contenute in questa sezione non si applicano all'individuazione foresta Active Directory.  

Questi tre metodi di individuazione sono simili per configurazione e funzionamento e possono individuare computer, utenti e informazioni sulle appartenenze al gruppo di risorse memorizzate nei Servizi di dominio Active Directory. Il processo di individuazione è gestito da un agente di individuazione in esecuzione sul server del sito su ogni sito in cui l'individuazione è configurata per l'esecuzione. È possibile configurare ciascuno di questi metodi di individuazione per effettuare la ricerca in uno o più percorsi di Active Directory. come le istanze di percorso nella foresta locale o nelle foreste remote.  

Quando l'individuazione effettua la ricerca di risorse in una foresta non trusted, l'agente di individuazione deve essere in grado di risolvere quanto segue per avere esito positivo:  

-   Per individuare una risorsa del computer con l'individuazione sistema Active Directory, l'agente di individuazione deve essere in grado di risolvere l'FQDN della risorsa. Se l'agente di individuazione non è in grado di risolvere l'FQDN, tenterà quindi di risolvere la risorsa con il nome NetBIOS.  

-   Per individuare una risorsa utente o gruppo con l'individuazione utente o gruppo Active Directory, l'agente di individuazione deve saper risolvere l'FQDN del nome del controller di dominio specificato nel percorso di Active Directory.  

Per ogni percorso specificato, è possibile configurare singole opzioni di ricerca, come l'abilitazione di una ricerca ricorsiva dei contenitori figlio Active Directory dei percorsi. È anche possibile configurare un account univoco da usare durante la ricerca in tale percorso. Ciò fornisce flessibilità nella configurazione di un metodo di individuazione in un sito per effettuare la ricerca in più percorsi Active Directory in più foreste, senza dover configurare un account singolo che disponga di autorizzazioni per tutti i percorsi.  

Quando questi tre metodi di individuazione vengono eseguiti su un sito specifico, il server del sito di Configuration Manager in tale sito contatta il controllo di dominio più vicino nella foresta Active Directory specificata per individuare le risorse Active Directory. Il dominio e la foresta possono trovarsi in qualsiasi modalità Active Directory supportata e l'account che si assegna a ciascuna istanza di percorso deve avere l'autorizzazione di accesso di **Lettura** ai percorsi Active Directory specificati. L'individuazione effettua la ricerca degli oggetti nei percorsi specificati, quindi tenta di raccogliere informazioni relative a tali oggetti. Viene creato un record dei dati di individuazione quando è possibile individuare informazioni sufficienti su una risorsa. Le informazioni richieste variano a seconda del metodo di individuazione utilizzato.  

Se si configura lo stesso metodo di individuazione per poterlo eseguire su siti diversi di Configuration Manager e poter quindi eseguire una query sui server di Active Directory locali, è possibile configurare ogni sito usando una sola serie di opzioni di individuazione. Poiché i dati di individuazione vengono condivisi con ogni sito della gerarchia, evitare la sovrapposizione tra tali configurazioni per individuare in modo efficiente ogni risorsa una volta sola. Per ambiente più piccoli, si potrebbe prendere in considerazione l'esecuzione di ciascun metodo di individuazione su un solo sito della gerarchia per ridurre il carico amministrativo e la possibilità che più azioni di individuazione individuino di nuovo le stesse risorse. Quando si riduce al minimo il numero di siti che eseguono l'individuazione, è possibile ridurre la larghezza di banda di rete complessiva utilizzata dall'individuazione, nonché il numero totale di DDR che vengono creati e devono essere elaborati dai server del sito.  

Molte delle configurazioni del metodo di individuazione sono di chiara interpretazione  Utilizzare le sezioni seguenti per ulteriori informazioni sulle opzioni di individuazione che potrebbe richiedere informazioni aggiuntive prima di essere configurate.  

È possibile usare le opzioni seguenti con più metodi di individuazione Active Directory:  

-   [Individuazione differenziale](#bkmk_delta)  

-   [Filtrare i record del computer non aggiornati usando l'accesso al dominio](#bkmk_stalelogon)  

-   [Filtrare i record non aggiornati usando la password del computer](#bkmk_stalepassword)  

-   [Cercare attributi di Active Directory personalizzati](#bkmk_customAD)  

###  <a name="a-namebkmkdeltaa-delta-discovery"></a><a name="bkmk_delta"></a> Individuazione differenziale  
Disponibile per:  

-   Individuazione gruppo Active Directory  

-   Individuazione sistema Active Directory  

-   individuazione utenti di Active Directory  

L'individuazione differenziale non è un metodo di individuazione indipendente, ma un'opzione disponibile per i metodi di individuazione applicabili. L'individuazione differenziale cerca attributi di Active Directory specifici che sono stati modificati dopo l'ultimo ciclo di individuazione completa del metodo di individuazione applicabile.  Questa ricerca usa meno risorse rispetto a un ciclo di individuazione completa e le modifiche degli attributi vengono inviate al database di Configuration Manager per aggiornare il record di individuazione della risorsa.  

Per impostazione predefinita, l'individuazione differenziale viene eseguita in un ciclo da cinque minuti, molto più di frequente rispetto alla pianificazione tipica per un ciclo di individuazione completa.  È possibile eseguire questo ciclo in modo frequente perché l'individuazione differenziale usa un numero inferiore di server del sito e di risorse di rete rispetto a un ciclo di individuazione completa. Quando si usa l'individuazione differenziale, è possibile ridurre la frequenza del ciclo di individuazione completa per tale metodo di individuazione.  

Di seguito sono elencale le modifiche più comuni rilevate dall'individuazione differenziale:  

-   Nuovi computer o utenti aggiunti ad Active Directory  

-   Modifiche apportate alle informazioni utente e computer di base  

-   Nuovi computer o utenti aggiunti a un gruppo  

-   Computer o utenti rimossi da un gruppo  

-   Modifiche apportate agli oggetti del gruppo di sistema  

L'individuazione differenziale, sebbene possa individuare le nuove risorse e le modifiche apportate all'appartenenza al gruppo, non può individuare se una risorsa è stata eliminata da Active Directory. I record dei dati di individuazione creati dall'individuazione differenziale vengono elaborati analogamente ai record dei dati di individuazione creati da un ciclo di individuazione completa.  

Configurare l'individuazione differenziale nella scheda **Pianificazione del polling** delle proprietà di ciascun metodo di individuazione.  

###  <a name="a-namebkmkstalelogona-filter-stale-computer-records-by-domain-logon"></a><a name="bkmk_stalelogon"></a> Filtrare i record del computer non aggiornati usando l'accesso al dominio  
Disponibile per:  

-   Individuazione gruppo Active Directory  

-   Individuazione sistema Active Directory  

È possibile configurare l'individuazione per escludere i computer con record del computer non aggiornati in base all'ultimo accesso al dominio del computer. Quando è abilitata questa opzione, l'individuazione sistema Active Directory valuta ogni computer identificato. L'individuazione gruppo Active Directory valuta ogni computer membro di un gruppo rilevato.  

Per poter usare questa opzione:  

-   I computer devono essere configurati in modo che sia eseguito l'aggiornamento dell'attributo **lastLogonTimeStamp** in Active Directory Domain Services.  

-   Il livello di funzionalità del dominio di Active Directory deve essere impostato su Windows Server 2003 o versione successiva.  

Quando si configura l'orario dopo l'ultimo accesso per questa impostazione, considerare l'intervallo per la replica tra i controller di dominio.  

È possibile configurare il filtro nella scheda **Opzioni** nelle finestre di dialogo **Proprietà individuazione sistema Active Directory** e **Proprietà individuazione gruppo Active Directory** selezionando l'opzione **Individua solo computer che hanno effettuato l'accesso a un dominio in un periodo di tempo specifico**.  

> [!WARNING]  
>  Quando si configurano questo filtro e l'opzione **Filtrare i record non aggiornati usando la password del computer**, i computer che soddisfano i criteri di uno dei due filtri vengono esclusi dall'individuazione.  

###  <a name="a-namebkmkstalepassworda-filter-stale-records-by-computer-password"></a><a name="bkmk_stalepassword"></a> Filtrare i record non aggiornati usando la password del computer  
Disponibile per:  

-   Individuazione gruppo Active Directory  

-   Individuazione sistema Active Directory  

È possibile configurare l'individuazione per escludere i computer con record del computer non aggiornati in base all'ultimo aggiornamento della password dell'account computer da parte dal computer. Quando è abilitata questa opzione, l'individuazione sistema Active Directory valuta ogni computer identificato. L'individuazione gruppo Active Directory valuta ogni computer membro di un gruppo rilevato.  

Per poter usare questa opzione:  

-   I computer devono essere configurati in modo che sia eseguito l'aggiornamento dell'attributo **pwdLastSet** in Active Directory Domain Services.  

Durante la configurazione di questa opzione, si prenda in considerazione l'intervallo di aggiornamento a questo attributo oltre all'intervallo di replica tra i controller di dominio.  

È possibile configurare il filtro nella scheda **Opzioni** nelle finestre di dialogo **Proprietà individuazione sistema Active Directory** e **Proprietà individuazione gruppo Active Directory** selezionando l'opzione **Individua solo computer che hanno aggiornato la password dell'account computer in un periodo di tempo specifico**.  

> [!WARNING]  
>  Quando si configurano questo filtro e l'opzione **Filtrare i record del computer non aggiornati usando l'accesso al dominio**, i computer che soddisfano i criteri di uno dei due filtri vengono esclusi dall'individuazione.  

###  <a name="a-namebkmkcustomada-search-customized-active-directory-attributes"></a><a name="bkmk_customAD"></a> Cercare attributi di Active Directory personalizzati  
 Disponibile per:  

-   Individuazione sistema Active Directory  

-   individuazione utenti di Active Directory  

Ogni metodo di individuazione supporta un elenco univoco di attributi di Active Directory che possono essere individuati.  

È possibile visualizzare e configurare l'elenco degli attributi di Active Directory personalizzati nella scheda **Attributi di Active Directory** nelle finestre di dialogo **Active Directory System Discovery Properties** (Proprietà individuazione sistema Active Directory) e **Active Directory User Discovery Properties** (Proprietà individuazione utente Active Directory).  



<!--HONumber=Dec16_HO3-->



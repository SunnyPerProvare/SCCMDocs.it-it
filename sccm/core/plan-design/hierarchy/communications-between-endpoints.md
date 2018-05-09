---
title: Comunicazioni tra gli endpoint
titleSuffix: Configuration Manager
description: Informazioni sulle modalità di comunicazione dei componenti e sistemi del sito di System Center Configuration Manager in una rete.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 68fe0e7e-351e-4222-853a-877475adb589
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 603adb982f704c462e043d8c0974fc85a0748863
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="communications-between-endpoints-in-system-center-configuration-manager"></a>Comunicazioni tra gli endpoint in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


##  <a name="Planning_Intra-site_Com"></a> Comunicazioni tra sistemi del sito in un sito  
 Quando i sistemi o componenti del sito di Configuration Manager comunicano in rete con altri sistemi del sito oppure con componenti di Configuration Manager nel sito, usano uno dei protocolli seguenti, a seconda della configurazione del sito:  

-   Server Message Block (SMB)  

-   HTTP  

-   HTTPS  

Con l'eccezione della comunicazione dal server del sito a un punto di distribuzione, le comunicazioni tra server in un sito possono verificarsi in qualsiasi momento e non usano meccanismi per controllare la larghezza di banda di rete. Poiché non è possibile controllare la comunicazione tra sistemi del sito, assicurarsi di installare i server del sistema del sito in posizioni che abbiano reti veloci e ben connesse.  

Per gestire il trasferimento di contenuto dal server del sito ai punti di distribuzione:  

-   Configurare il punto di distribuzione per il controllo della larghezza di banda di rete e la pianificazione. Questi controlli sono simili alle configurazioni usate dagli indirizzi intrasito ed è spesso possibile usare questa configurazione invece di installare un altro sito di Configuration Manager quando la larghezza di banda incide soprattutto sul trasferimento di contenuti su percorsi di rete remoti.  

-   È possibile installare un punto di distribuzione come punto di distribuzione pre-installato. Un punto di distribuzione pre-installato consente di usare contenuto che viene messo manualmente sul server del punto di distribuzione e rimuove il requisito di trasferire i file di contenuto sulla rete.  

Per altre informazioni, vedere [Gestire la larghezza di banda di rete per la gestione dei contenuti](manage-network-bandwidth.md).


##  <a name="Planning_Client_to_Site_System"></a> Comunicazioni da client a sistemi e servizi del sito  
I client avviano le comunicazioni con i ruoli del sistema del sito, Active Directory Domain Services e servizi online. Per abilitare queste comunicazioni, i firewall devono consentire il traffico di rete tra i client e gli endpoint delle comunicazioni. Gli endpoint includono:  

-   **Punto per siti Web del Catalogo applicazioni**: supporta la comunicazione HTTP e HTTPS

-   **Risorse basate sul cloud**: include Microsoft Azure e Microsoft Intune  

-   **Modulo criteri di Configuration Manager (NDES)**: supporta la comunicazione HTTP e HTTPS

-   **Punti di distribuzione**: supporta la comunicazione HTTP e HTTPS, e HTTPS è richiesto dai punti di distribuzione basati sul cloud  

-   **Punto di stato di fallback**: supporta la comunicazione HTTP  

-   **Punto di gestione**: supporta la comunicazione HTTP e HTTPS  

-   **Microsoft Update**  

-   **Punti di aggiornamento software**: supporta la comunicazione HTTP e HTTPS  

-   **Punto di migrazione stato**: supporta la comunicazione HTTP e HTTPS  

-   **Vari servizi di dominio**  

Per poter comunicare con un ruolo del sistema del sito, il client usa la posizione del servizio per individuare un ruolo del sistema del sito che supporta il protocollo del client (HTTP o HTTPS). Per impostazione predefinita, i client usano il metodo più sicuro a loro disposizione:  

-   Per usare HTTPS, è necessario disporre di un'infrastruttura a chiave pubblica (PKI) e installare i certificati PKI sui client e sui server. Per informazioni sull'uso dei certificati, vedere [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md) (Requisiti dei certificati PKI per System Center Configuration Manager).  

-   Quando si distribuisce un ruolo del sistema del sito che usa Internet Information Services (IIS) e supporta le comunicazioni dai client, è necessario specificare se i client si connettono al sistema del sito tramite HTTP o HTTPS. Se si usa HTTP, è necessario considerare anche le opzioni di firma e crittografia. Per altre informazioni, vedere [Pianificazione di firma e crittografia](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForSigningEncryption) in [Pianificare la sicurezza in System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md).  

Per informazioni sul processo di posizione del servizio usato dai client, vedere  [Informazioni su come i client trovano i servizi e le risorse del sito per System Center Configuration Manager](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

Per informazioni dettagliate sulle porte e i protocolli usati dai client per la comunicazione con questi endpoint, vedere [Porte usate in System Center Configuration Manager](../../../core/plan-design/hierarchy/ports.md).  

###  <a name="BKMK_clientspan"></a> Considerazioni per le comunicazioni client da Internet o da una foresta non trusted  
I seguenti ruoli del sistema del sito installati nei siti primari supportano connessioni da client che si trovano in percorsi non attendibili, come Internet o una foresta non trusted. I siti secondari non supportano le connessioni client da percorsi non attendibili:  

-   Punto per siti Web del Catalogo applicazioni  

-   Modulo criteri di Configuration Manager  

-   Punto di distribuzione (HTTPS è richiesto dai punti di distribuzione basati sul cloud)  

-   Punto proxy di registrazione  

-   Punto di stato di fallback  

-   Punto di gestione  

-   Punto di aggiornamento software  

**Informazioni sui sistemi del sito con connessione internet:**   
Non è necessario che esista una relazione di trust tra la foresta del client e quella del server del sistema del sito. Quando la foresta che contiene il sistema del sito con connessione Internet considera attendibile la foresta che contiene gli account utente, tuttavia, questa configurazione supporta criteri basati sull'utente per i dispositivi su Internet se si abilita l'impostazione client **Abilitare le richieste dei criteri utente dai client Internet** di **Criteri client**.  

Ad esempio, le configurazioni seguenti illustrano quando la gestione client basata su Internet supporta criteri utente per i dispositivi su Internet:  

-   Il punto di gestione basato su Internet si trova nella rete perimetrale in cui risiede un controller di dominio di sola lettura per autenticare l'utente e un firewall consente pacchetti di Active Directory.  

-   L'account utente si trova nella Foresta A (intranet) e il punto di gestione basato su Internet si trova nella Foresta B (la rete perimetrale). La Foresta B considera attendibile la Foresta A e un firewall consente i pacchetti di autenticazione.  

-   L'account utente e il punto di gestione basato su Internet si trovano nella Foresta A (intranet). Il punto di gestione viene pubblicato su Internet usando un server Web proxy, ad esempio Forefront Threat Management Gateway.  

> [!NOTE]  
>  Se l'autenticazione Kerberos ha esito negativo, sarà automaticamente tentata l'autenticazione NTLM.  

Come mostrato nell'esempio precedente, è possibile posizionare i sistemi del sito basati su Internet nella intranet quando vengono pubblicati su Internet usando un server Web proxy, come ISA Server e Forefront Threat Management Gateway. Questi sistemi del sito possono essere configurati per connessioni client solo da Internet o per connessioni client da Internet e Intranet. Quando si usa un server Web proxy, è possibile configurarlo per il bridging Secure Sockets Layer (SSL) a SSL (più sicuro) o tunneling SSL, come segue:  

-   **Bridging SSL a SSL:**   
    La configurazione consigliata quando si usano server Web proxy per la gestione client basata su Internet è il bridging SSL a SSL, che usa la terminazione SSL con l'autenticazione. I computer client devono essere autenticati usando l'autenticazione computer e i client legacy di dispositivi mobili vengono autenticati usando l'autenticazione utente. I dispositivi mobili che vengono registrati da Configuration Manager non supportano il bridging SSL.  

     Il vantaggio della terminazione SSL sul server Web proxy è che i pacchetti provenienti da Internet sono soggetti alla verifica prima di essere inoltrati alla rete interna. Il server Web proxy autentica la connessione dal client, la termina, quindi apre una nuova connessione autenticata ai sistemi del sito basati su Internet. Quando i client di Configuration Manager usano un server Web proxy, l'identità client (GUID client) viene contenuta in modo protetto all'interno del payload dei pacchetti in modo che il punto di gestione non consideri il server Web proxy come il client. Il bridging HTTP a HTTPS o HTTPS a HTTP non è supportato in Configuration Manager.  

-   **Tunneling**:   
    Se il server Web proxy non può supportare i requisiti per il bridging SSL o se si vuole configurare il supporto Internet per i dispositivi mobili registrati da Configuration Manager, è supportato il tunneling SSL. Si tratta di un'opzione meno sicura perché i pacchetti SSL provenienti da Internet vengono inoltrati ai sistemi del sito senza terminazione SSL e, pertanto, non possono essere verificati per l'eventuale presenza di contenuto dannoso. Quando si usa il tunneling SSL, non sono previsti requisiti di certificato per il server Web proxy.  

##  <a name="Plan_Com_X-Forest"></a> Comunicazioni tra foreste Active Directory  
System Center Configuration Manager supporta siti e gerarchie che si estendono su foreste Active Directory.  

Configuration Manager supporta anche computer del dominio che non si trovano nella stessa foresta Active Directory del server del sito e computer che appartengono a gruppi di lavoro:  

-   **Per supportare i computer di dominio in una foresta considerata non trusted dalla foresta del server del sito**, è possibile:  

    -   Installare i ruoli del sistema del sito in tale foresta non trusted, con la possibilità di pubblicare le informazioni sul sito in tale foresta di Active Directory  

    -   Gestire questi computer come computer di un gruppo di lavoro.  

  Quando si installano i server del sistema del sito in una foresta Active Directory non trusted, la comunicazione tra client e server eseguita dai client della foresta viene mantenuta all'interno di tale foresta e Configuration Manager può autenticare il computer con Kerberos. Quando vengono pubblicate le informazioni del sito sulla foresta del client, i client possono recuperare le informazioni del sito, come ad esempio un elenco di punti di gestione disponibili, dalla relativa foresta Active Directory invece di scaricarle dal punto di gestione assegnato.  

  > [!NOTE]  
  >  Se si desidera gestire i dispositivi su Internet, è possibile installare ruoli del sistema del sito basati su Internet nella rete perimetrale quando i server del sistema del sito si trovano nella foresta Active Directory. In questo scenario non è richiesto un trust bidirezionale tra la rete perimetrale e la foresta del server del sito.  

-   **Per supportare i computer in un gruppo di lavoro**, è necessario:  

    -   Approvare manualmente i computer del gruppo di lavoro quando questi usano connessioni client HTTP ai ruoli del sistema del sito. Ciò avviene perché Configuration Manager non può autenticare questi computer con Kerberos.  

    -   Configurare i client dei gruppi di lavoro per l'uso dell'Account di accesso alla rete in modo che questi computer possano recuperare il contenuto dai punti di distribuzione.  

    -   Fornire ai client del gruppo di lavoro un meccanismo alternativo per trovare i punti di gestione. È possibile usare la pubblicazione DNS o WINS oppure assegnare direttamente un punto di gestione. Questo perché tali client non possono recuperare le informazioni del sito da Servizi di dominio Active Directory.  

    Risorse correlate in questa raccolta contenuto:  

    -   [Gestire i record in conflitto per i client di Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_ConflictingRecords)  

    -   [Account di accesso alla rete](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#accounts-used-for-content-management)  

    -   [Come installare i client di Configuration Manager sui computer del gruppo di lavoro](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)  

###  <a name="bkmk_span"></a> Scenari di supporto di un sito o una gerarchia che si estende su più domini e foreste  

#### <a name="communication-between-sites-in-a-hierarchy-that-spans-forests"></a>Comunicazione tra siti in una gerarchia che si estende su più foreste  
Questo scenario richiede un trust tra foreste bidirezionale che supporti l'autenticazione Kerberos.  Se non è presente un trust tra foreste bidirezionale che supporti l'autenticazione Kerberos, Configuration Manager non supporterà il sito figlio nella foresta remota.  

 **Configuration Manager supporta l'installazione di un sito figlio in una foresta remota che ha il trust bidirezionale richiesto con la foresta del sito padre**  

-   Ad esempio, è possibile inserire un sito secondario in una foresta diversa da quella del sito primario padre a condizione che sia presente il trust necessario.  

> [!NOTE]  
>  Un sito figlio può essere un sito primario (dove il sito di amministrazione centrale è il sito padre) o un sito secondario.  

La comunicazione tra siti in Configuration Manager usa la replica di database e i trasferimenti basati su file. Quando si installa un sito, è necessario specificare un account da usare per l'installazione del sito nel server designato. Inoltre, questo account stabilisce e mantiene la comunicazione tra siti.  

Dopo che il sito è stato installato correttamente e i trasferimenti basati su file e la replica di database sono stati avviati, non sarà necessario eseguire ulteriori configurazioni per la comunicazione con il sito.  

**In presenza di un trust tra foreste bidirezionale, Configuration Manager non richiede altri passaggi di configurazione.**  

Per impostazione predefinita, quando si installa un nuovo sito come figlio di un altro sito, Configuration Manager configura gli elementi seguenti:  

-   Una route di replica basata su file tra siti per ogni sito che usa l'account computer del server del sito. Configuration Manager aggiunge l'account computer di ciascun computer al gruppo **SMS_SiteToSiteConnection_&lt;sitecode\>** nel computer di destinazione.  

-   Replica di database tra il server SQL in ciascun sito.  

È necessario impostare anche le seguenti configurazioni:  

-   I firewall e i dispositivi di rete interessati devono consentire i pacchetti di rete richiesti da Configuration Manager.  

-   La risoluzione dei nomi deve funzionare tra le foreste.  

-   Per installare un sito o un ruolo del sistema del sito, è necessario specificare un account con autorizzazioni di amministratore locale sul computer specificato.  

#### <a name="communication-in-a-site-that-spans-forests"></a>Comunicazione in un sito che si estende su più foreste  
Questo scenario non richiede un trust tra foreste bidirezionale.  

**I siti primari supportano l'installazione dei ruoli del sistema del sito su computer in foreste remote**.  

-   Il punto per servizi Web del Catalogo applicazioni è l'unica eccezione.  È supportato solo nella stessa foresta del server del sito.  

-   Quando un ruolo del sistema del sito accetta connessioni da Internet, la procedura ottimale di protezione prevede l'installazione dei ruoli del sistema del sito in una posizione in cui i limiti della foresta forniscono la protezione per il server del sito, ad esempio in una rete perimetrale.  

**Per installare un ruolo del sistema del sito in un computer in una foresta non trusted:**  

-   È necessario specificare un **account di installazione del sistema del sito** che consente di installare il ruolo del sistema del sito. L'account deve disporre delle credenziali di amministratore locale per la connessione. Installare quindi i ruoli del sistema del sito nel computer specificato.  

-   È necessario selezionare l'opzione del sistema del sito **Richiedi al server del sito di avviare le connessioni al sistema del sito**. In questo modo il server del sito deve stabilire connessioni al server del sistema del sito per il trasferimento di dati. Questo consente di evitare che il computer nella posizione non attendibile avvii un contatto con il server del sito all'interno della rete attendibile. Queste connessioni usano l' **account di installazione del sistema del sito**.  

**Per usare un ruolo del sistema del sito installato in una foresta non trusted,** i firewall devono consentire il traffico di rete, anche quando il server del sito avvia il trasferimento dei dati.  

Inoltre, i seguenti ruoli del sistema del sito richiedono l'accesso diretto al database del sito. È quindi necessario che i firewall consentano il traffico applicabile dalla foresta non trusted a SQL Server dei siti:  

-   Punto di sincronizzazione di Asset Intelligence  

-   Punto di Endpoint Protection  

-   Punto di registrazione  

-   Punto di gestione  

-   Punto di Reporting Services  

-   Punto di migrazione stato  

Per altre informazioni, vedere [Porte usate in System Center Configuration Manager](../../../core/plan-design/hierarchy/ports.md).  

**Potrebbe essere necessario configurare l'accesso del ruolo del sistema del sito al database del sito:**  

Il ruolo del sistema del sito del punto di registrazione e il ruolo del sistema del sito del punto di gestione si connettono entrambi al database del sito.  

-   Per impostazione predefinita, quando questi ruoli vengono installati, Configuration Manager configura l'account computer del nuovo server del sistema del sito come account di connessione per il ruolo del sistema del sito e aggiunge l'account al ruolo del database SQL Server appropriato.  

-   Quando si installano questi ruoli del sistema del sito in un dominio non attendibile, è necessario configurare l'account di connessione del ruolo del sistema del sito per abilitarne la ricezione delle informazioni dal database.  

Se si configura un account utente di dominio come account di connessione per questi ruoli del sistema del sito, assicurarsi che l'account utente di dominio abbia accesso appropriato al database di SQL Server in quel sito:  

-   Punto di gestione: **account di connessione al database del punto di gestione**  

-   Punto di registrazione: **account di connessione del punto di registrazione**  

Considerare le seguenti informazioni aggiuntive per la pianificazione di ruoli del sistema del sito in altre foreste:  

-   Se si esegue Windows Firewall, configurare i profili firewall applicabili per consentire il passaggio delle comunicazioni tra il server di database del sito e i computer installati con i ruoli del sistema del sito remoto. Per informazioni sui profili firewall, vedere [Informazioni sui profili del firewall](http://go.microsoft.com/fwlink/p/?LinkId=233629).  

-   Quando il punto di gestione basato su Internet considera attendibile la foresta che contiene gli account utente, vengono supportati i criteri utente. In caso contrario, sono supportati solo i criteri computer.  

#### <a name="communication-between-clients-and-site-system-roles-when-the-clients-are-not-in-the-same-active-directory-forest-as-their-site-server"></a>Comunicazione tra client e ruoli del sistema del sito quando i client non si trovano nella stessa foresta Active Directory del relativo server del sito  
Configuration Manager supporta i seguenti scenari per i client che non si trovano nella stessa foresta del relativo server del sito:  

-   È presente un trust tra foreste bidirezionale tra la foresta del client e la foresta del server del sito.  

-   Il server del ruolo del sistema del sito si trova nella stessa foresta del client.  

-   Il client si trova in un computer di dominio che non dispone di un trust tra foreste bidirezionale con il server del sito e i ruoli del sistema del sito non sono installati nella foresta del client.  

-   Il client si trova in un computer del gruppo di lavoro.  

I client in un computer aggiunto a un dominio possono usare Active Directory Domain Services per la posizione del servizio quando il relativo sito è pubblicato nella foresta Active Directory.  

Per pubblicare le informazioni di un sito in un'altra foresta Active Directory, è necessario:  

-   Specificare la foresta, quindi abilitare la pubblicazione in tale foresta nel nodo **Foreste Active Directory** dell'area di lavoro **Amministrazione** .  

-   Configurare ogni sito per la pubblicazione dei relativi dati in Servizi di dominio Active Directory. Questa configurazione consente ai client di tale foresta di recuperare le informazioni del sito e trovare punti di gestione. Per i client che non possono usare Servizi di dominio Active Directory per la posizione del servizio, è possibile usare DNS, WINS o il punto di gestione client assegnato.  

###  <a name="bkmk_xchange"></a> Inserire il connettore Exchange Server in una foresta remota  
Per supportare questo scenario, assicurarsi che la risoluzione dei nomi funzioni tra le foreste (ad esempio, configurare inoltri DNS) e quando si configura il connettore Exchange Server specificare il nome FQDN Intranet di Exchange Server. Per altre informazioni, vedere [Gestire i dispositivi mobili con System Center Configuration Manager ed Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

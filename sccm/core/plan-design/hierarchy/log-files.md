---
title: File di log | System Center Configuration Manager
description: Usare i file di log per la risoluzione dei problemi in una gerarchia di System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c1ff371e-b0ad-4048-aeda-02a9ff08889e
caps.latest.revision: 9
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: cb27f2f2a6e0b0e3d6fca2d616d8ab806b74f9df


---
# <a name="log-files-in-system-center-configuration-manager"></a>File di log in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager i componenti client e del server del sito registrano le informazioni di processo in singoli file di log. Per impostazione predefinita, la registrazione dei componenti client e server è abilitata in Configuration Manager. È possibile usare le informazioni contenute nei file di log per risolvere i problemi che potrebbero verificarsi all'interno della gerarchia di Configuration Manager.  

 Nelle sezioni seguenti vengono fornite informazioni dettagliate sui diversi file di log. Usare queste informazioni per visualizzare e monitorare i log dei client e dei server di Configuration Manager per ottenere maggiori dettagli sulle operazioni e identificare le informazioni sugli errori che potrebbero facilitare la risoluzione di eventuali problemi.  

-   [Informazioni sui file di log di Configuration Manager](#BKMK_AboutLogs)  

    -   [Configurare le opzioni di registrazione usando Configuration Manager Service Manager](#BKMK_LogOptions)  

    -   [Individuazione dei log di Configuration Manager](#BKMK_LogLocation)  

-   [Log client di Configuration Manager](#BKMK_ClientLogs)  

    -   [Operazioni client](#BKMK_ClientOpLogs)  

    -   [File di log di installazione client](#BKMK_ClientInstallLog)  

    -   [Client per Linux e UNIX](#BKMK_LogFilesforLnU)  

    -   [Client per computer Mac](#BKMK_LogfilesforMac)  

-   [File di log del server del sito di Configuration Manager](#BKMK_ServerLogs)  

    -   [Log del server del sito e del server di sistema del sito](#BKMK_SiteSiteServerLog)  

    -   [File di log di installazione del server del sito](#BKMK_SiteInstallLog)  

    -   [File di log del punto di stato di fallback](#BKMK_FSPLog)  

    -   [File di log del punto di gestione](#BKMK_MPLog)  

    -   [File di log del punto di aggiornamento software](#BKMK_SUPLog)  

-   [File di log per la funzionalità di Configuration Manager](#BKMK_FunctionLogs)  

    -   [Gestione delle applicazioni](#BKMK_AppManageLog)  

    -   [Asset Intelligence](#BKMK_AILog)  

    -   [Backup e ripristino](#BKMK_BnRLog)  

    -   [Notifica client](#BKMK_BGB)  

    -   [Registrazione certificato](#BKMK_CertificateEnrollment)  

    -   [Impostazioni di conformità e accesso alle risorse aziendali](#BKMK_CompSettingsLog)  

    -   [Console di Configuration Manager](#BKMK_ConsoleLog)  

    -   [Gestione dei contenuti](#BKMK_ContentLog)  

    -   [Individuazione](#BKMK_DiscoveryLog)  

    -   [Endpoint Protection](#BKMK_EPLog)  

    -   [Estensioni](#BKMK_Extensions)  

    -   [Inventario](#BKMK_InventoryLog)  

    -   [Metering](#BKMK_MeteringLog)  

    -   [Migrazione](#BKMK_MigrationLog)  

    -   [Dispositivi mobili](#BKMK_MDMLog)  

    -   [Distribuzione del sistema operativo](#BKMK_OSDLog)  

    -   [Risparmio energia](#BKMK_PowerMgmtLog)  

    -   [Controllo remoto](#BKMK_RCLog)  

    -   [Reporting](#BKMK_ReportLog)  

    -   [Amministrazione basata su ruoli](#BKMK_RBALog)  

    -   [Punto di connessione del servizio](#BKMK_WITLog)  

    -   [Aggiornamenti software](#BKMK_SU_NAPLog)  

    -   [Riattivazione LAN](#BKMK_WOLLog)  

    -   [Agente di Windows Update](#BKMK_WULog)  

    -   [Server WSUS](#BKMK_WSUSLog)  

##  <a name="a-namebkmkaboutlogsa-about-configuration-manager-log-files"></a><a name="BKMK_AboutLogs"></a> Informazioni sui file di log di Configuration Manager  
 Per impostazione predefinita, la maggior parte dei processi in Configuration Manager scrive le informazioni operative in un file di log dedicato al processo. Questi file di log vengono identificati dall’estensione **.LOG** o **.LO_** . Configuration Manager scrive nel file con estensione LOG fino a quando il file non raggiunge la dimensione massima. Quando il log è pieno, il file .LOG viene copiato in un file con lo stesso nome ma con estensione .LO_ e il processo o il componente continua a scrivere nel file .LOG. Quando il file .LOG raggiunge nuovamente la dimensione massima, il file .LO_ viene sovrascritto e il processo si ripete. Alcuni componenti stabiliscono una cronologia per i file di log aggiungendo una data e un timestamp al nome del file di log e mantenendo l'estensione .LOG. Un'eccezione alla dimensione massima e all'utilizzo del file **.LO_** è il client per Linux e UNIX. Per informazioni su come il client per Linux e UNIX usa i file di log, vedere Gestione dei file di log per i client Linux e UNIX nella sezione [Client per Linux e UNIX](#BKMK_LogFilesforLnU) in questo argomento.  

 Per visualizzare i log è possibile usare CMTrace, il visualizzatore log di Configuration Manager, disponibile nella cartella **\SMSSETUP\TOOLS** del supporto di origine di Configuration Manager. Lo strumento CMTrace viene inoltre aggiunto a tutte le immagini di avvio aggiunte alla **Raccolta software**.  

###  <a name="a-namebkmklogoptionsa-configure-logging-options-by-using-the-configuration-manager-service-manager"></a><a name="BKMK_LogOptions"></a> Configurare le opzioni di registrazione usando Configuration Manager Service Manager  
 Configuration Manager supporta opzioni che consentono di modificare il percorso di archiviazione e la dimensione dei file di log.  

 Attenersi alla procedura seguente per usare **Configuration Manager Service Manager** per modificare la dimensione, il nome e il percorso dei file di log e per fare in modo che più componenti scrivano in un unico file di log.  

##### <a name="to-modify-logging-for-a-component"></a>Per modificare la registrazione per un componente:  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**, quindi fare clic su **Stato sistema** e infine fare clic su **Stato sito** o **Stato componente**.  

2.  Nella scheda **Home** , nel gruppo **Componente** , fare clic su **Avvia** e selezionare **Configuration Manager Service Manager**.  

3.  All'apertura di Configuration Manager Service Manager, connettersi al sito che si desidera gestire.  

     Se non si visualizza il sito che si desidera gestire, fare clic su **Sito**, quindi su **Connetti** e infine immettere il nome del server del sito corretto.  

4.  Espandere il sito e passare a **Componenti** o **Server**in base alla posizione dei componenti che si desidera gestire.  

5.  Nel riquadro a destra selezionare uno o più componenti.  

6.  Scegliere **Registrazione** dal menu **Componente**.  

7.  Nella finestra di dialogo **Registrazione componente di Configuration Manager** completare le opzioni di configurazione disponibili per la selezione effettuata.  

8.  Fare clic su **OK** per salvare la configurazione.  

###  <a name="a-namebkmkloglocationa-locating-configuration-manager-logs"></a><a name="BKMK_LogLocation"></a> Individuazione dei log di Configuration Manager  
 Per impostazione predefinita, i file di log di Configuration Manager sono archiviati in percorsi diversi a seconda del processo che li ha creati e della configurazione dei sistemi del sito. Dal momento che la posizione del log su un dato computer può variare, usare la funzionalità di ricerca per individuare i file di log desiderati sui computer di Configuration Manager, in modo da risolvere eventuali problemi relativi a uno specifico scenario.  

##  <a name="a-namebkmkclientlogsa-configuration-manager-client-logs"></a><a name="BKMK_ClientLogs"></a> Log client di Configuration Manager  
 Nelle sezioni seguenti vengono elencati i file di log relativi alle operazioni client e all'installazione del client.  

###  <a name="a-namebkmkclientoplogsa-client-operations"></a><a name="BKMK_ClientOpLogs"></a> Operazioni client  
 Nella tabella seguente sono elencati i file di log trovati nel client di Configuration Manager.  

|Nome registro|Descrizione|  
|--------------|-----------------|  
|CAS.log|Servizio di accesso ai contenuti. Gestisce la cache dei pacchetti locali sul client.|  
|Ccm32BitLauncher.log|Registra le azioni per l'avvio delle applicazioni sul client contrassegnate per l'esecuzione a 32 bit.|  
|CcmEval.log|Registra le attività di valutazione dello stato del client di Configuration Manager oltre a informazioni dettagliate per i componenti richiesti dal client di Configuration Manager.|  
|CcmEvalTask.log|Registra le attività di valutazione dello stato del client di Configuration Manager avviate dall'attività pianificata di valutazione.|  
|CcmExec.log|Registra le attività del client e del servizio host agenti di SMS. Questo file di log include anche informazioni sull'abilitazione e la disabilitazione del proxy di riattivazione.|  
|CcmMessaging.log|Registra le attività relative alle comunicazioni tra il client e i punti di gestione.|  
|CCMNotificationAgent.log|Registra le attività relative alle operazioni di notifica client.|  
|Ccmperf.log|Registra le attività di manutenzione e acquisizione dati correlate ai contatori delle prestazioni dei client.|  
|CcmRestart.log|Registra l'attività di riavvio del servizio client.|  
|CCMSDKProvider.log|Registra le attività per le interfacce dell'SDK client.|  
|CertificateMaintenance.log|Gestisce i certificati per Servizi di dominio Active Directory e i punti di gestione.|  
|CIDownloader.log|Registra informazioni dettagliate sui download di definizioni di elementi di configurazione.|  
|CITaskMgr.log|Registra le attività avviate per ogni applicazione e tipo di distribuzione, ad esempio download di contenuti o azioni di installazione o disinstallazione.|  
|ClientAuth.log|Registra l'attività di firma e autenticazione per il client.|  
|ClientIDManagerStartup.log|Crea e gestisce il GUID del client e identifica le attività eseguite durante l'assegnazione e la registrazione del client.|  
|ClientLocation.log|Registra le attività relative all'assegnazione del sito client.|  
|CMHttpsReadiness.log|Registra i risultati dell'esecuzione dello strumento per la preparazione della comunicazione HTTPS di Configuration Manager. Questo strumento consente di verificare se nei computer è presente un certificato PKI per l'autenticazione client utilizzabile per Configuration Manager.|  
|CmRcService.log|Registra le informazioni per il servizio di controllo remoto.|  
|ContentTransferManager.log|Pianifica il Servizio trasferimento intelligente in background (BITS) o Server Message Block (SMB) per il download o per l'accesso ai pacchetti.|  
|DataTransferService.log|Registra tutte le comunicazioni BITS per l'accesso ai criteri o ai pacchetti.|  
|EndpointProtectionAgent|Registra le informazioni sull'installazione del client di Endpoint Protection e sull'applicazione di criteri antimalware in tale client.|  
|execmgr.log|Registra informazioni dettagliate sui pacchetti e sulle sequenze attività in esecuzione nel client.|  
|ExpressionSolver.log|Registra informazioni dettagliate sui metodi di rilevamento avanzati che vengono usati quando si attiva la registrazione debug o dettagliata.|  
|ExternalEventAgent.log|Registra la cronologia di rilevamento malware di Endpoint Protection e gli eventi relativi allo stato del client.|  
|FileBITS.log|Registra tutte le attività di accesso al pacchetto SMB.|  
|FileSystemFile.log|Registra l'attività del provider Strumentazione gestione Windows (WMI) per l'inventario software e la raccolta file.|  
|FSPStateMessage.log|Registra l'attività per i messaggi di stato inviati dal client al punto di stato di fallback.|  
|InternetProxy.log|Registra l'attività di utilizzo e configurazione proxy di rete per il client.|  
|InventoryAgent.log|Registra le attività di inventario hardware, inventario software e individuazione heartbeat sul client.|  
|LocationCache.log|Registra l'attività per l'utilizzo e la gestione della cache per l'individuazione per il client.|  
|LocationServices.log|Registra l'attività del client per l'individuazione di punti di gestione, punti di aggiornamento software e punti di distribuzione.|  
|MaintenanceCoordinator.log|Registra l'attività per l'attività di manutenzione generale per il client.|  
|Mifprovider.log|Registra l'attività del provider WMI per file .MIF.|  
|mtrmgr.log|Esegue il monitoraggio di tutti i processi di controllo software.|  
|PolicyAgent.log|Registra le richieste di criteri effettuate usando il servizio di trasferimento dei dati.|  
|PolicyAgentProvider.log|Registra le modifiche apportate ai criteri.|  
|PolicyEvaluator.log|Registra informazioni dettagliate sulla valutazione dei criteri nei computer client, inclusi quelli derivanti dagli aggiornamenti software.|  
|PolicyPlatformClient.log|Registra il processo di monitoraggio, aggiornamento e conformità per tutti i provider disponibili in **%Program Files%\Microsoft Policy Platform**, fatta eccezione per il provider di file.|  
|PolicySdk.log|Registra le attività per le interfacce dell'SDK per il sistema dei criteri.|  
|Pwrmgmt.log|Registra le informazioni sull'attivazione o la disattivazione e la configurazione delle impostazioni client proxy di riattivazione.|  
|PwrProvider.log|Registra le attività del provider risparmio energia (PWRInvProvider) ospitato nel servizio Strumentazione gestione Windows (WMI). In tutte le versioni supportate di Windows il provider enumera le impostazioni correnti sui computer durante l'inventario hardware e applica le impostazioni della combinazione per il risparmio di energia.|  
|SCClient_&lt;dominio\>@&lt;nomeutente\>_1.log|Registra l'attività in Software Center per l'utente specificato nel computer client.|  
|SCClient_&lt;dominio\>@&lt;nomeutente\>_2.log|Registra l'attività cronologica in Software Center per l'utente specificato nel computer client.|  
|Scheduler.log|Registra le attività delle attività pianificate per tutte le operazioni client.|  
|SCNotify_&lt;dominio\>@&lt;nomeutente\>_1.log|Registra l'attività per la notifica degli utenti riguardo al software per l'utente specificato.|  
|SCNotify_&lt;dominio\>@&lt;nomeutente\>_1-&lt;data_ora>.log|Registra le informazioni cronologiche per la notifica degli utenti riguardo al software per l'utente specificato.|  
|setuppolicyevaluator.log|Registra la configurazione e la creazione dei criteri dell'inventario in WMI.|  
|SleepAgent_&lt;dominio\>@&lt;@SYSTEM_0.log|File di log principale per il proxy di riattivazione.|  
|smscliui.log|Registra l'utilizzo del client di Configuration Manager nel Pannello di controllo.|  
|SrcUpdateMgr.log|Registra l'attività per le applicazioni di Windows Installer installate che vengono aggiornate con i percorsi di origine per i punti di distribuzione correnti.|  
|StatusAgent.log|Registra i messaggi di stato creati dai componenti client.|  
|SWMTRReportGen.log|Genera un report dei dati di utilizzo raccolto dall'agente di controllo. Tali dati vengono registrati in Mtrmgr.log.|  
|UserAffinity.log|Registra informazioni dettagliate relative all'affinità utente dispositivo.|  
|VirtualApp.log|Registra informazioni specifiche per la valutazione dei tipi di distribuzione di App-V.|  
|Wedmtrace.log|Registra le operazioni relative ai filtri di scrittura sui client Windows Embedded.|  
|wakeprxy-install.log|Registra le informazioni di installazione quando i client ricevono l'opzione di impostazione client per abilitare il proxy di riattivazione.|  
|wakeprxy-uninstall.log|Registra le informazioni sulla disinstallazione del proxy di riattivazione quando i client ricevono l'opzione di impostazione client per disabilitare il proxy di riattivazione, se è stato precedentemente abilitato.|  

###  <a name="a-namebkmkclientinstallloga-client-installation-log-files"></a><a name="BKMK_ClientInstallLog"></a> File di log di installazione client  
 Nella tabella seguente sono elencati i file di log contenenti informazioni correlate all'installazione del client di Configuration Manager.  

|Nome registro|Descrizione|  
|--------------|-----------------|  
|ccmsetup.log|Registra le attività svolte da **ccmsetup** per l'installazione, l'aggiornamento e la rimozione dei client. Può essere usato per la risoluzione dei problemi di installazione dei client.|  
|ccmsetup-ccmeval.log|Registra le attività svolte da **ccmsetup** per lo stato del client e il monitoraggio e l'aggiornamento.|  
|CcmRepair.log|Registra le attività di ripristino dell'agente client.|  
|client.msi.log|Registra le attività di installazione eseguite da client.msi. Può essere usato per la risoluzione dei problemi di installazione o rimozione dei client.|  

###  <a name="a-namebkmklogfilesforlnua-client-for-linux-and-unix"></a><a name="BKMK_LogFilesforLnU"></a> Client per Linux e UNIX  
 Il client di Configuration Manager per Linux e UNIX registra le informazioni nei file di log seguenti.  

> [!TIP]  
>  A partire dai client per Linux e UNIX dall'aggiornamento cumulativo 1, è possibile usare CMTrace per visualizzare i file di log per il client per Linux e UNIX.  

> [!NOTE]  
>  Quando si usa la versione iniziale del client per Linux e UNIX e si fa riferimento alla documentazione in questa sezione, sostituire i riferimenti seguenti per ogni file o processo:  
>   
>  -   Sostituire **omiserver.bin** con **nwserver.bin**  
> -   Sostituire **omi** con **nanowbem**  

|Nome registro|Dettagli|  
|--------------|-------------|  
|scxcm.log|File di log per il servizio principale del client di Configuration Manager per Linux e UNIX (ccmexec.bin). Questo file di log contiene informazioni sull'installazione e le operazioni in corso di ccmexec.bin.<br /><br /> Per impostazione predefinita, questo file di log viene creato nel percorso seguente: **/var/opt/microsoft/scxcm.log**<br /><br /> Per cambiare il percorso del file di log, modificare **/opt/microsoft/configmgr/etc/scxcm.conf** e apportare le modifiche desiderate nel campo **PATH** . Non è necessario riavviare il servizio o il computer client per rendere effettive le modifiche.<br /><br /> È possibile impostare il livello di registrazione su una delle quattro diverse impostazioni seguenti:|  
|scxcmprovider.log|File di log per il servizio CIM del client di Configuration Manager per Linux e UNIX (omiserver.bin). Questo file di log contiene informazioni sulle operazioni in corso di nwserver.bin.<br /><br /> Per impostazione predefinita, questo file di log viene creato nel percorso seguente: **/var/opt/microsoft/configmgr/scxcmprovider.log**<br /><br /> Per cambiare il percorso del file di log, modificare **/opt/microsoft/omi/etc/scxcmprovider.conf** e apportare le modifiche desiderate nel campo **PATH** . Non è necessario riavviare il servizio o il computer client per rendere effettive le modifiche.<br /><br /> È possibile impostare il livello di registrazione su una delle tre diverse impostazioni seguenti:|  

 **Entrambi i file di log supportano diversi livelli di registrazione:**  

-   **scxcm.log**: per cambiare il livello di registrazione, modificare **/opt/microsoft/configmgr/etc/scxcm.conf** e impostare ogni istanza del tag **MODULE** sul livello di log desiderato:  

    -   ERROR: indica i problemi che richiedono attenzione.  

    -   WARNING: indica i possibili problemi per le operazioni del client.  

    -   INFO: registrazione più dettagliata, che indica lo stato di diversi eventi nel client.  

    -   TRACE: registrazione dettagliata che viene generalmente usata per diagnosticare i problemi.  

-   **scxcmprovider.log**: per cambiare il livello di registrazione, modificare **/opt/microsoft/omi/etc/scxcmprovider.conf** e impostare ogni istanza del tag **MODULE** sul livello di log desiderato:  

    -   ERROR: indica i problemi che richiedono attenzione.  

    -   WARNING: indica i possibili problemi per le operazioni del client.  

    -   INFO: registrazione più dettagliata, che indica lo stato di diversi eventi nel client.  

In condizioni operative normali, deve essere usato il livello di registrazione ERRORE. Il livello di registrazione ERRORE crea il file di log più piccolo. Quando il livello di registrazione aumenta da ERRORE, ad AVVISO, a INFORMAZIONI e infine a TRACCIA, ogni passaggio avrà come risultato un file di log più grande, poiché nel file verrà scritta una quantità maggiore di dati.  

####  <a name="a-namebkmkmanagelinuxlogsa-manage-log-files-for-the-client-for-linux-and-unix-client"></a><a name="BKMK_ManageLinuxLogs"></a> Gestire i file di log per i client Linux e UNIX  
Il client per Linux e UNIX non limita la dimensione massima dei file di log client e non copia automaticamente i contenuti dei file **.LOG** in un altro file, ad esempio un file **.LO_** . Se si vuole controllare la dimensione massima dei file di log, implementare un processo per gestire i file di log indipendente dal client di Configuration Manager per Linux e UNIX.  

Ad esempio, è possibile usare il comando standard per Linux e UNIX **logrotate** per gestire la dimensione e la rotazione di file log dei client. Il client di Configuration Manager per Linux e UNIX offre un'interfaccia che consente a **logrotate** di segnalare al client il completamento della rotazione del log, in modo che il client possa riprendere la registrazione nel file di log.  

Per informazioni su **logrotate**, vedere la documentazione per le distribuzioni di Linux e UNIX in uso.  

###  <a name="a-namebkmklogfilesformaca-client-for-mac-computers"></a><a name="BKMK_LogfilesforMac"></a> Client per computer Mac  
Il client di Configuration Manager per computer Mac registra le informazioni nei file di log seguenti.  

|Nome registro|Dettagli|  
|--------------|-------------|  
|CCMClient-*&lt;data_ora>*.log|Registra le attività correlate alle operazioni del client Mac, inclusi Gestione delle applicazioni, inventario e registrazione degli errori.<br /><br /> Questo file di log si trova nella cartella **/Library/Application Support/Microsoft/CCM/Logs** sul computer Mac.|  
|CCMAgent-*&lt;data_ora>*.log|Registra le informazioni relative alle operazioni dei client, incluse le operazioni di accesso e disconnessione dell'utente e le attività del computer Mac.<br /><br /> Questo file di log si trova nella cartella **~/Library/Logs** sul computer Mac.|  
|CCMNotifications-*&lt;data_ora>*.log|Registra le attività correlate alle notifiche di Configuration Manager visualizzate nel computer Mac.<br /><br /> Questo file di log si trova nella cartella **~/Library/Logs** sul computer Mac.|  
|CCMPrefPane-*&lt;data_ora>*.log|Registra le attività correlate alla finestra di dialogo per le preferenze di Configuration Manager nel computer Mac, che include lo stato generale e la registrazione degli errori.<br /><br /> Questo file di log si trova nella cartella **~/Library/Logs** sul computer Mac.|  

 Il file SMS_DM.log nel server di sistema del sito registra inoltre le comunicazioni tra computer Mac e il punto di gestione abilitato per dispositivi mobili e computer Mac.  

##  <a name="a-namebkmkserverlogsa-configuration-manager-site-server-log-files"></a><a name="BKMK_ServerLogs"></a> File di log del server del sito di Configuration Manager  
 Nelle sezioni seguenti sono elencati i file di log disponibili nel server del sito o correlati a specifici ruoli del sistema del sito.  

###  <a name="a-namebkmksitesiteserverloga-site-server-and-site-system-server-logs"></a><a name="BKMK_SiteSiteServerLog"></a> Log del server del sito e del server di sistema del sito  
 Nella tabella seguente sono elencati i file di log disponibili nel server del sito e nei server di sistema del sito di Configuration Manager.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|adctrl.log|Registra le attività di elaborazione delle registrazioni.|Server del sito|  
|ADForestDisc.log|Registra le azioni di individuazione foresta Active Directory.|Server del sito|  
|ADService.log|Registra i dettagli relativi alla creazione di account e ai gruppi di sicurezza in Active Directory.|Server del sito|  
|adsgdis.log|Registra le azioni di individuazione gruppo Active Directory.|Server del sito|  
|adsysdis.log|Registra le azioni di individuazione sistema Active Directory.|Server del sito|  
|adusrdis.log|Registra le azioni di individuazione utente Active Directory.|Server del sito|  
|ccm.log|Registra le attività di installazione push dei client.|Server del sito|  
|CertMgr.log|Registra le attività relative ai certificati per le comunicazioni all'interno del sito.|Server del sistema del sito|  
|chmgr.log|Registra le attività della gestione dell'integrità client.|Server del sito|  
|Cidm.log|Registra le modifiche apportate alle impostazioni del client da Client Install Data Manager (CIDM).|Server del sito|  
|colleval.log|Registra dettagli sul momento in cui le raccolte vengono create, modificate ed eliminate dall'analizzatore di raccolte.|Server del sito|  
|compmon.log|Registra lo stato dei thread di componenti monitorati per il server del sito.|Server del sistema del sito|  
|compsumm.log|Registra le attività del Generatore riepilogo dello stato del componente.|Server del sito|  
|ComRegSetup.log|Registra l'installazione iniziale dei risultati di registrazione COM per un server del sito.|Server del sistema del sito|  
|dataldr.log|Registra le informazioni sull'elaborazione dei file MIF (Management Information Format) e dell'inventario hardware nel database di Configuration Manager.|Server del sito|  
|ddm.log|Registra le attività di Gestione individuazione dati.|Server del sito|  
|despool.log|Registra i trasferimenti delle comunicazioni in arrivo tra siti.|Server del sito|  
|distmgr.log|Registra informazioni dettagliate su creazione del pacchetto, compressione, replica differenziale e aggiornamenti delle informazioni.|Server del sito|  
|EPCtrlMgr.log|Registra le informazioni sulla sincronizzazione di informazioni relative a minacce di tipo malware dal server del ruolo del sistema del sito di Endpoint Protection nel database di Configuration Manager.|Server del sito|  
|EPMgr.log|Registra lo stato del ruolo del sistema del sito di Endpoint Protection.|Server del sistema del sito|  
|EPSetup.log|Fornisce informazioni sull'installazione del ruolo del sistema del sito di Endpoint Protection.|Server del sistema del sito|  
|EnrollSrv.log|Registra le attività relative al processo del servizio di registrazione.|Server del sistema del sito|  
|EnrollWeb.log|Registra le attività relative al processo del sito Web di registrazione.|Server del sistema del sito|  
|fspmgr.log|Registra le attività del ruolo del sistema del sito punto di stato di fallback.|Server del sistema del sito|  
|hman.log|Registra le informazioni sulle modifiche di configurazione del sito e sulla pubblicazione delle informazioni del sito in Servizi di dominio Active Directory.|Server del sito|  
|Inboxast.log|Registra i file che vengono spostati dal punto di gestione alla cartella INBOXES corrispondente nel server del sito.|Server del sito|  
|inboxmgr.log|Registra le attività di trasferimento file tra cartelle Posta in arrivo.|Server del sito|  
|inboxmon.log|Registra l'elaborazione dei file di Posta in arrivo e degli aggiornamenti del contatore delle prestazioni.|Server del sito|  
|invproc.log|Registra l'inoltro dei file MIF da un sito secondario al sito padre corrispondente.|Server del sito|  
|migmctrl.log|Registra le informazioni per le azioni di migrazione riguardanti i processi di migrazione, i punti di distribuzione condivisi e gli aggiornamenti dei punti di distribuzione.|Sito principale della gerarchia di Configuration Manager e ogni sito primario figlio<br /><br /> In una gerarchia che include più siti primari, usare il file di log creato nel sito di amministrazione centrale.|  
|mpcontrol.log|Registra la registrazione del punto di gestione con WINS. Registra la disponibilità del punto di gestione ogni 10 minuti.|Server del sistema del sito|  
|mpfdm.log|Registra le azioni del componente del punto di gestione che sposta i file client nella cartella INBOXES corrispondente nel server del sito.|Server del sistema del sito|  
|mpMSI.log|Registra informazioni dettagliate sull'installazione del punto di gestione.|Server del sito|  
|MPSetup.log|Registra il processo wrapper di installazione del punto di gestione.|Server del sito|  
|netdisc.log|Registra le azioni di individuazione della rete.|Server del sito|  
|ntsvrdis.log|Registra l'attività di individuazione dei server di sistema del sito.|Server del sito|  
|Objreplmgr|Registra l'elaborazione delle notifiche di modifica di oggetti per la replica.|Server del sito|  
|offermgr.log|Registra gli aggiornamenti degli annunci.|Server del sito|  
|offersum.log|Registra il riepilogo dei messaggi di stato di distribuzione.|Server del sito|  
|OfflineServicingMgr.log|Registra le attività di applicazione degli aggiornamenti ai file di immagine del sistema operativo.|Server del sito|  
|outboxmon.log|Registra l'elaborazione dei file di Posta in uscita e degli aggiornamenti del contatore delle prestazioni.|Server del sito|  
|PerfSetup.log|Registra i risultati dell'installazione di contatori delle prestazioni.|Server del sistema del sito|  
|PkgXferMgr.log|Registra le azioni del componente SMS Executive, responsabile per l'invio di contenuto da un sito primario a un punto di distribuzione remoto.|Server del sito|  
|policypv.log|Registra gli aggiornamenti ai criteri del client per riflettere le modifiche apportate alle impostazioni o alle distribuzioni del client.|Server del sito primario|  
|rcmctrl.log|Registra le attività di replica database tra siti nella gerarchia.|Server del sito|  
|replmgr.log|Registra la replica di file tra i componenti server del sito e il componente di utilità di pianificazione.|Server del sito|  
|ResourceExplorer.log|Registra errori, avvisi e informazioni sull'esecuzione di Esplora inventario risorse.|Computer che esegue la console di Configuration Manager|  
|ruleengine.log|Registra le informazioni dettagliate sulle regole di distribuzione automatica per l'identificazione, il download di contenuto e la creazione di gruppi di aggiornamento software e distribuzione.|Server del sito|  
|schedule.log|Registra informazioni dettagliate su processi e replica di file da sito a sito.|Server del sito|  
|sender.log|Registra i file trasferiti tra siti mediante la replica basata su file.|Server del sito|  
|sinvproc.log|Registra le informazioni sull'elaborazione dei dati di inventario del software nel database del sito.|Server del sito|  
|sitecomp.log|Registra informazioni dettagliate sulla manutenzione dei componenti sito installati in tutti i server di sistema del sito nel sito specifico.|Server del sito|  
|sitectrl.log|Registra le modifiche alle impostazioni del sito apportate agli oggetti di controllo sito nel database.|Server del sito|  
|sitestat.log|Registra il processo di monitoraggio di disponibilità e spazio su disco di tutti i sistemi del sito.|Server del sito|  
|SmsAdminUI.log|Registra l'attività della console di Configuration Manager.|Computer che esegue la console di Configuration Manager|  
|SMSAWEBSVCSetup.log|Registra le attività di installazione dei servizi Web del Catalogo applicazioni.|Server del sistema del sito|  
|smsbkup.log|Registra il risultato del processo di backup del sito.|Server del sito|  
|smsdbmon.log|Registra le modifiche apportate al database.|Server del sito|  
|SMSENROLLSRVSetup.log|Registra le attività di installazione dei servizi Web di registrazione.|Server del sistema del sito|  
|SMSENROLLWEBSetup.log|Registra le attività di installazione del sito Web di registrazione.|Server del sistema del sito|  
|smsexec.log|Registra l'elaborazione di tutti i thread di componenti del server del sito.|Server del sito o sistema di server del sito|  
|SMSFSPSetup.log|Registra i messaggi generati dall'installazione di un punto di stato di fallback.|Server del sistema del sito|  
|SMSPORTALWEBSetup.log|Registra le attività di installazione del sito Web del Catalogo applicazioni.|Server del sistema del sito|  
|SMSProv.log|Registra gli accessi del provider WMI al database del sito.|Computer con il provider SMS|  
|srsrpMSI.log|Registra i risultati dettagliati del processo di installazione del punto di reporting dall'output MSI.|Server del sistema del sito|  
|srsrpsetup.log|Registra i risultati del processo di installazione del punto di reporting.|Server del sistema del sito|  
|statesys.log|Registra l'elaborazione dei messaggi di sistema di stato.|Server del sito|  
|statmgr.log|Registra la scrittura di tutti i messaggi di stato nel database.|Server del sito|  
|swmproc.log|Registra l'elaborazione di file e impostazioni di controllo.|Server del sito|  

###  <a name="a-namebkmksiteinstallloga-site-server-installation-log-files"></a><a name="BKMK_SiteInstallLog"></a> File di log di installazione del server del sito  
 Nella tabella seguente sono elencati i file di log contenenti informazioni relative all'installazione del sito.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|ConfigMgrPrereq.log|Registra attività prerequisite di valutazione e installazione di componenti.|Server del sito|  
|ConfigMgrSetup.log|Registra l'output dettagliato dell'installazione del server del sito.|Server del sito|  
|ConfigMgrSetupWizard.log|Registra le informazioni relative all'attività nell'installazione guidata.|Server del sito|  
|SMS_BOOTSTRAP.log|Registra le informazioni sullo stato di avanzamento dell'avvio del processo di installazione del sito secondario. I dettagli del processo di configurazione effettivo sono contenuti in ConfigMgrSetup.log.|Server del sito|  
|smstsvc.log|Registra informazioni su installazione, utilizzo e rimozione di un servizio Windows usato per testare la connettività di rete e le autorizzazioni tra i server, tramite l'account computer del server che ha avviato la connessione.|Server del sito e sistemi del sito|  

###  <a name="a-namebkmkfsploga-fallback-status-point-logs-files"></a><a name="BKMK_FSPLog"></a> File di log del punto di stato di fallback  
 Nella tabella seguente sono elencati i file di log contenenti informazioni correlate al punto di stato di fallback.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|FspIsapi|Registra le comunicazioni verso il punto di stato di fallback da client legacy di dispositivi mobili e da computer client.|Server del sistema del sito|  
|fspMSI.log|Registra i messaggi generati dall'installazione di un punto di stato di fallback.|Server del sistema del sito|  
|fspmgr.log|Registra le attività del ruolo del sistema del sito punto di stato di fallback.|Server del sistema del sito|  

###  <a name="a-namebkmkmploga-management-point-logs-files"></a><a name="BKMK_MPLog"></a> File di log del punto di gestione  
 Nella tabella seguente sono elencati i file di log contenenti informazioni correlate al punto di gestione.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|CcmIsapi.log|Registra l'attività di messaggistica client sull'endpoint.|Server del sistema del sito|  
|MP_CliReg.log|Registra l'attività di registrazione del client elaborata dal punto di gestione.|Server del sistema del sito|  
|MP_Ddr.log|Registra la conversione di record XML.ddr dai client e li copia nel server del sito.|Server del sistema del sito|  
|MP_Framework.log|Registra le attività del punto di gestione principale e dei componenti del framework client.|Server del sistema del sito|  
|MP_GetAuth.log|Registra le attività di autorizzazione del client.|Server del sistema del sito|  
|MP_GetPolicy.log|Registra le attività di richiesta di criteri dai computer client.|Server del sistema del sito|  
|MP_Hinv.log|Registra informazioni dettagliate sulla conversione di record di inventario hardware XML dai client e sulla copia di tali file nel server del sito.|Server del sistema del sito|  
|MP_Location.log|Registra le attività di richiesta per il percorso e di risposta dai client.|Server del sistema del sito|  
|MP_OOBMgr.log|Registra le attività del punto di gestione correlate alla ricezione OTP da un client.|Server del sistema del sito|  
|MP_Policy.log|Registra la comunicazione dei criteri.|Server del sistema del sito|  
|MP_Relay.log|Registra il trasferimento di file che vengono raccolti dal client.|Server del sistema del sito|  
|MP_Retry.log|Registra i processi di nuovi tentativi di inventario hardware.|Server del sistema del sito|  
|MP_Sinv.log|Registra informazioni dettagliate sulla conversione di record di inventario software XML dai client e sulla copia di tali file nel server del sito.|Server del sistema del sito|  
|MP_SinvCollFile.log|Registra informazioni dettagliate sulla raccolta di file.|Server del sistema del sito|  
|MP_Status.log|Registra informazioni dettagliate sulla conversione di file di messaggi di stato XML.svf dai client e sulla copia di tali file nel server del sito.|Server del sistema del sito|  
|mpcontrol.log|Registra la registrazione del punto di gestione con WINS. Registra la disponibilità del punto di gestione ogni 10 minuti.|Server del sito|  
|mpfdm.log|Registra le azioni del componente del punto di gestione che sposta i file client nella cartella INBOXES corrispondente nel server del sito.|Server del sistema del sito|  
|mpMSI.log|Registra informazioni dettagliate sull'installazione del punto di gestione.|Server del sito|  
|MPSetup.log|Registra il processo wrapper di installazione del punto di gestione.|Server del sito|  

###  <a name="a-namebkmksuploga-software-update-point-log-files"></a><a name="BKMK_SUPLog"></a> File di log del punto di aggiornamento software  
 Nella tabella seguente sono elencati i file di log contenenti informazioni correlate al punto di aggiornamento software.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|objreplmgr.log|Registra informazioni dettagliate sulla replica di file di notifica di aggiornamenti software da un sito padre ai siti figlio.|Server del sito|  
|PatchDownloader.log|Registra informazioni dettagliate sul processo di download degli aggiornamenti software dall'origine degli aggiornamenti alla destinazione del download sul server del sito.|Computer che ospita la console di Configuration Manager da cui vengono avviati i download|  
|ruleengine.log|Registra le informazioni dettagliate sulle regole di distribuzione automatica per l'identificazione, il download di contenuto e la creazione di gruppi di aggiornamento software e distribuzione.|Server del sito|  
|SUPSetup.log|Registra informazioni dettagliate sull'installazione del punto di aggiornamento software. Al termine dell'installazione del punto di aggiornamento software, **Installation was successful** viene scritto nel file di log.|Server del sistema del sito|  
|WCM.log|Registra informazioni dettagliate sulla configurazione del punto di aggiornamento software e sulle connessioni al server di Windows Server Update Services (WSUS) per categorie di aggiornamento, classificazioni e lingue sottoscritte.|Server del sito che si connette al server di Windows Server Update Services (WSUS)|  
|WSUSCtrl.log|Registra informazioni dettagliate su configurazione, connettività al database e integrità del server WSUS per il sito.|Server del sistema del sito|  
|wsyncmgr.log|Registra informazioni dettagliate sul processo di sincronizzazione degli aggiornamenti software.|Server del sistema del sito|  
|WUSSyncXML.log|Registra informazioni dettagliate sullo strumento di inventario per il processo di sincronizzazione di Microsoft Update.|Computer client configurato come host di sincronizzazione per lo strumento di inventario per Microsoft Update.|  

##  <a name="a-namebkmkfunctionlogsa-log-files-for-configuration-manager-functionality"></a><a name="BKMK_FunctionLogs"></a> File di log per la funzionalità di Configuration Manager  
 Nelle sezioni seguenti sono elencati i file di log correlati alle diverse funzioni in Configuration Manager.  

###  <a name="a-namebkmkappmanageloga-application-management"></a><a name="BKMK_AppManageLog"></a> Gestione delle applicazioni  
 Nella tabella seguente sono elencati i file di log contenenti informazioni correlate a Gestione applicazioni.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|AppIntentEval.log|Registra informazioni dettagliate sullo stato corrente e previsto delle applicazioni, sulla relativa applicabilità, sulla soddisfazione dei requisiti, sui tipi di distribuzione e sulle dipendenze.|Client|  
|AppDiscovery.log|Registra informazioni dettagliate sull'individuazione o sul rilevamento di applicazioni nei computer client.|Client|  
|AppEnforce.log|Registra informazioni dettagliate sulle azioni di imposizione (installazione e disinstallazione) eseguite per applicazioni sul client.|Client|  
|awebsctl.log|Registra le attività di monitoraggio per il ruolo del sistema del sito punto per servizi Web del Catalogo applicazioni.|Server del sistema del sito|  
|awebsvcMSI.log|Registra informazioni di installazione dettagliate per il ruolo del sistema del sito punto per servizi Web del Catalogo applicazioni.|Server del sistema del sito|  
|CCMSDKProvider.log|Registra le attività di SDK di gestione applicazioni.|Client|  
|colleval.log|Registra dettagli sul momento in cui le raccolte vengono create, modificate ed eliminate dall'analizzatore di raccolte.|Server del sistema del sito|  
|ConfigMgrSoftwareCatalog.log|Registra l'attività del Catalogo applicazioni, che include l'utilizzo di Silverlight.|Client|  
|portlctl.log|Registra le attività di monitoraggio per il ruolo del sistema del sito punto per siti Web del Catalogo applicazioni.|Server del sistema del sito|  
|portlwebMSI.log|Registra l'attività di installazione MSI per il ruolo del sito Web del Catalogo applicazioni.|Server del sistema del sito|  
|PrestageContent.log|Registra informazioni dettagliate sull'utilizzo dello strumento ExtractContent.exe in un punto di distribuzione pre-installazione remoto. Questo strumento consente di estrarre contenuto che è stato esportato in un file.|Server del sistema del sito|  
|ServicePortalWebService.log|Registra le attività di installazione dei servizi Web del Catalogo applicazioni.|Server del sistema del sito|  
|ServicePortalWebSite.log|Registra le attività del sito Web del Catalogo applicazioni.|Server del sistema del sito|  
|SMSdpmon.log|Registra informazioni dettagliate sulle attività pianificate di monitoraggio dell'integrità del punto di distribuzione configurate su un punto di distribuzione.|Server del sito|  
|SoftwareCatalogUpdateEndpoint.log|Registra le attività per la gestione di URL per il Catalogo di applicazioni indicato nel Software Center.|Client|  
|SoftwareCenterSystemTasks.log|Registra le attività per la convalida dei componenti dei prerequisiti di Software Center.|Client|  

 La tabella seguente elenca i file di log contenenti informazioni correlate alla distribuzione di pacchetti e programmi.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|colleval.log|Registra dettagli sul momento in cui le raccolte vengono create, modificate ed eliminate dall'analizzatore di raccolte.|Server del sito|  
|execmgr.log|Registra informazioni dettagliate sui pacchetti e sulle sequenze attività in esecuzione.|Client|  

###  <a name="a-namebkmkailoga-asset-intelligence"></a><a name="BKMK_AILog"></a> Asset Intelligence  
 Nella tabella seguente sono elencati i file di log contenenti informazioni correlate ad Asset Intelligence.  

|Nome log|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|AssetAdvisor.log|Registra le attività delle operazioni di inventario di Asset Intelligence.|Client|  
|aikbmgr.log|Registra informazioni dettagliate sull'elaborazione di file XML da Posta in arrivo per l'aggiornamento del catalogo di Asset Intelligence.|Server del sito|  
|AIUpdateSvc.log|Registra l'interazione del punto di sincronizzazione di Asset Intelligence con SCO (System Center Online), il servizio Web online.|Server del sistema del sito|  
|AIUSMSI.log|Registra informazioni dettagliate sull'installazione del ruolo del sistema del sito punto di sincronizzazione di Asset Intelligence.|Server del sistema del sito|  
|AIUSSetup.log|Registra informazioni dettagliate sull'installazione del ruolo del sistema del sito punto di sincronizzazione di Asset Intelligence.|Server del sistema del sito|  
|ManagedProvider.log|Registra informazioni dettagliate sull'individuazione di software con tag di identificazione software associato. Registra inoltre le attività correlate all'inventario hardware.|Server del sistema del sito|  
|MVLSImport.log|Registra informazioni dettagliate sull'elaborazione di file di licenza importati.|Server del sistema del sito|  

###  <a name="a-namebkmkbnrloga-backup-and-recovery"></a><a name="BKMK_BnRLog"></a> Backup e ripristino  
 Nella tabella seguente sono elencati i file di log contenenti informazioni correlate ad azioni di backup e ripristino, incluse le reimpostazioni di siti e le modifiche apportate al provider SMS.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|ConfigMgrSetup.log|Registra informazioni sulle attività di impostazione e ripristino quando Configuration Manager ripristina un sito dal backup.|Server del sito|  
|Smsbkup.log|Registra informazioni dettagliate sulle attività di backup del sito.|Server del sito|  
|smssqlbkup.log|Registra l'output dal processo di backup del database quando SQL Server è installato in un server diverso dal server del sito.|Server di database del sito|  
|Smswriter.log|Registra informazioni sullo stato del writer VSS di Configuration Manager usato dal processo di backup.|Server del sito|  

###  <a name="a-namebkmkcertificateenrollmenta-certificate-enrollment"></a><a name="BKMK_CertificateEnrollment"></a> Registrazione certificato  
 Nella tabella seguente sono elencati i file di log di Configuration Manager che contengono informazioni sulla registrazione del certificato che usa il punto di registrazione del certificato e il modulo criteri di Configuration Manager nel server che esegue il servizio Registrazione dispositivi di rete.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|Crp.log|Registra le attività di registrazione.|Punto di registrazione certificati|  
|Crpctrl.log|Registra l'integrità operativa del punto di registrazione certificati.|Punto di registrazione certificati|  
|Crpsetup.log|Registra le informazioni sull'installazione e la configurazione del punto di registrazione certificati.|Punto di registrazione certificati|  
|Crpmsi.log|Registra le informazioni sull'installazione e la configurazione del punto di registrazione certificati.|Punto di registrazione certificati|  
|NDESPlugin.log|Registra le attività di richiesta di verifica e registrazione dei certificati.|Modulo criteri di Configuration Manager e servizio Registrazione dispositivi di rete|  

 Oltre ai file di log di Configuration Manager, esaminare i registri Applicazione Windows in Visualizzatore eventi nel server che esegue il servizio Registrazione dispositivi di rete e nel server che ospita il punto di registrazione certificati. Ad esempio, cercare i messaggi provenienti dall'origine **ServizioRegistrazioneDispositiviDiRete** . È inoltre possibile usare i seguenti file di log:  

-   File di log di IIS per il servizio Registrazione dispositivi di rete: **&lt;percorso\>\inetpub\logs\LogFiles\W3SVC1**  

-   File di log di IIS per il punto di registrazione certificati: **&lt;percorso\>\inetpub\logs\LogFiles\W3SVC1**  

-   File di log criteri di registrazione dispositivi di rete: **mscep.log**  

    > [!NOTE]  
    >  Questo file si trova nella cartella del profilo account del servizio Registrazione dispositivi di rete, ad esempio, in C:\Utenti\SCEPSvc. Per altre informazioni su come abilitare la registrazione per il servizio Registrazione dispositivi di rete, vedere la sezione su come [abilitare la registrazione](http://go.microsoft.com/fwlink/?LinkId=320576) nell'articolo relativo al servizio Registrazione dispositivi di rete nei Servizi certificati Active Directory (AD CS) in TechNet wiki.  

###  <a name="a-namebkmkbgba-client-notification"></a><a name="BKMK_BGB"></a> Notifica client  
 Nella tabella seguente sono elencati i file di log contenenti informazioni relative alla notifica client.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|bgbmgr.log|Registra informazioni dettagliate sulle attività del server del sito relative ad attività di notifica client e all'elaborazione di file online e file di stato delle attività.|Server del sito|  
|BGBServer.log|Registra le attività del server di notifica, ad esempio le comunicazioni client-server e il push delle attività ai client. Registra inoltre informazioni sulla generazione di file di stato attività e in linea da inviare al server del sito.|Punto di gestione|  
|BgbSetup.log|Registra le attività del processo wrapper di installazione del server di notifica durante l'installazione e la disinstallazione.|Punto di gestione|  
|bgbisapiMSI.log|Registra informazioni dettagliate sull'installazione e sulla disinstallazione del server di notifica.|Punto di gestione|  
|BgbHttpProxy.log|Registra le attività del proxy HTTP di notifica durante l'inoltro dei messaggi dei client tramite HTTP verso e dal server di notifica.|Client|  
|CCMNotificationAgent.log|Registra le attività dell'agente di notifica, ad esempio le comunicazioni tra client e server e le informazioni sulle attività ricevute e spedite ad altri agenti client.|Client|  

###  <a name="a-namebkmkcompsettingsloga-compliance-settings-and-company-resource-access"></a><a name="BKMK_CompSettingsLog"></a> Impostazioni di conformità e accesso alle risorse aziendali  
 Nella tabella seguente sono elencati i file di registro contenenti informazioni relative alle impostazioni di conformità e all'accesso alle risorse aziendali.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|CIAgent.log|Registra informazioni dettagliate sul processo di monitoraggio e aggiornamento e conformità per impostazioni di conformità, aggiornamenti software e gestione applicazioni.|Client|  
|CITaskManager.log|Registra le informazioni sulla pianificazione della attività degli elementi di configurazione.|Client|  
|DCMAgent.log|Registra le informazioni di alto livello su valutazione, segnalazione dei conflitti e monitoraggio e aggiornamento di applicazioni ed elementi di configurazione.|Client|  
|DCMReporting.log|Registra le informazioni relative al reporting dei risultati della piattaforma criteri in messaggi di stato per gli elementi di configurazione.|Client|  
|DcmWmiProvider.log|Registra le informazioni sulla lettura dei synclet degli elementi di configurazione da Windows Management Instrumentation (WMI).|Client|  

###  <a name="a-namebkmkconsoleloga-configuration-manager-console"></a><a name="BKMK_ConsoleLog"></a> Console di Configuration Manager  
 Nella tabella seguente sono elencati i file di log contenenti informazioni correlate alla console di Configuration Manager.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|ConfigMgrAdminUISetup.log|Registra l'installazione della console di Configuration Manager.|Computer che esegue la console di Configuration Manager|  
|SmsAdminUI.log|Registra informazioni sul funzionamento della console di Configuration Manager.|Computer che esegue la console di Configuration Manager|  
|Smsprov.log|Registra le attività eseguite dal provider SMS. Le attività della console di Configuration Manager usano il provider SMS.|Server del sito o sistema di server del sito|  

###  <a name="a-namebkmkcontentloga-content-management"></a><a name="BKMK_ContentLog"></a> Gestione dei contenuti  
 Nella tabella seguente sono elencati i file di log contenenti informazioni correlate alla gestione dei contenuti.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|CloudDP-&lt;guid\>.log|Registra informazioni dettagliate per un punto di distribuzione specifico basato sul cloud, incluse le informazioni sull'archivio e l'accesso ai contenuti.|Server del sistema del sito|  
|CloudMgr.log|Registra informazioni dettagliate sul provisioning dei contenuti, raccogliendo statistiche sull'archiviazione e la larghezza di banda e azioni avviate dall'amministratore per interrompere o avviare il servizio cloud che esegue un punto di distribuzione basato su cloud.|Server del sistema del sito|  
|DataTransferService.log|Registra tutte le comunicazioni BITS per l'accesso ai criteri o ai pacchetti. Questo registro viene usato anche per la gestione dei contenuti per i punti di distribuzione pull.|Computer configurato come punto di distribuzione pull|  
|PullDP.log|Registra informazioni dettagliate sul contenuto che il punto di distribuzione pull trasferisce dai punti di distribuzione di origine.|Computer configurato come punto di distribuzione pull|  
|PrestageContent.log|Registra informazioni dettagliate sull'utilizzo dello strumento ExtractContent.exe in un punto di distribuzione pre-installazione remoto. Questo strumento consente di estrarre contenuto che è stato esportato in un file.|Ruolo del sistema del sito|  
|SMSdpmon.log|Registra informazioni dettagliate sulle attività pianificate di monitoraggio dell'integrità del punto di distribuzione configurate su un punto di distribuzione.|Ruolo del sistema del sito|  
|smsdpprov.log|Registra informazioni dettagliate sull'estrazione di file compressi ricevuti da un sito primario. Questo registro viene generato dal provider WMI del punto di distribuzione remoto.|Computer di punto di distribuzione che non condivide il percorso con il server del sito.|  

###  <a name="a-namebkmkdiscoveryloga-discovery"></a><a name="BKMK_DiscoveryLog"></a> Individuazione  
Nella tabella seguente sono elencati i file di log contenenti informazioni correlate all'individuazione.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|adsgdis.log|Registra le azioni di Individuazione gruppo di protezione Active Directory.|Server del sito|  
|adsysdis.log|Registra le azioni di individuazione sistema Active Directory.|Server del sito|  
|adusrdis.log|Registra le azioni di individuazione utente Active Directory.|Server del sito|  
|ADForestDisc.log|Registra le azioni di individuazione foresta Active Directory.|Server del sito|  
|ddm.log|Registra le attività di Gestione individuazione dati.|Server del sito|  
|InventoryAgent.log|Registra le attività di inventario hardware, inventario software e individuazione heartbeat sul client.|Client|  
|netdisc.log|Registra le azioni di individuazione della rete.|Server del sito|  

###  <a name="a-namebkmkeploga-endpoint-protection"></a><a name="BKMK_EPLog"></a> Endpoint Protection  
 Nella tabella seguente sono elencati i file di log contenenti informazioni correlate a Endpoint Protection.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|EndpointProtectionAgent.log|Registra informazioni dettagliate sull'installazione del client di Endpoint Protection e sull'applicazione di criteri antimalware in tale client.|Client|  
|EPCtrlMgr.log|Registra informazioni dettagliate sulla sincronizzazione di informazioni relative a minacce di tipo malware dal server del ruolo di Endpoint Protection nel database di Configuration Manager.|Server del sistema del sito|  
|EPMgr.log|Esegue il monitoraggio dello stato del ruolo del sistema del sito di Endpoint Protection.|Server del sistema del sito|  
|EPSetup.log|Fornisce informazioni sull'installazione del ruolo del sistema del sito di Endpoint Protection.|Server del sistema del sito|  

###  <a name="a-namebkmkextensionsa-extensions"></a><a name="BKMK_Extensions"></a> Estensioni  
 Nella tabella seguente sono elencati i file di log contenenti informazioni correlate alle estensioni.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|AdminUI.ExtensionInstaller.log|Registra informazioni sul download di estensioni da Microsoft e sull'installazione e la disinstallazione di tutte le estensioni.|Computer che esegue la console di Configuration Manager|  
|FeatureExtensionInstaller.log|Registra informazioni sull'installazione e la rimozione di singole estensioni quando vengono abilitate o disabilitate nella console di Configuration Manager.|Computer che esegue la console di Configuration Manager|  
|SmsAdminUI.log|Registra l'attività della console di Configuration Manager.|Computer che esegue la console di Configuration Manager|  

###  <a name="a-namebkmkinventoryloga-inventory"></a><a name="BKMK_InventoryLog"></a> Inventario  
 Nella tabella seguente sono elencati i file di log contenenti informazioni correlate all'elaborazione dei dati di inventario.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|dataldr.log|Registra le informazioni sull'elaborazione dei file MIF (Management Information Format) e dell'inventario hardware nel database di Configuration Manager.|Server del sito|  
|invproc.log|Registra l'inoltro dei file MIF da un sito secondario al sito padre corrispondente.|Server del sito secondario|  
|sinvproc.log|Registra le informazioni sull'elaborazione dei dati di inventario del software nel database del sito.|Server del sito|  

###  <a name="a-namebkmkmeteringloga-metering"></a><a name="BKMK_MeteringLog"></a> Metering  
 Nella tabella seguente sono elencati i file di log contenenti informazioni correlate al controllo software.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|mtrmgr.log|Esegue il monitoraggio di tutti i processi di controllo software.|Server del sito|  

###  <a name="a-namebkmkmigrationloga-migration"></a><a name="BKMK_MigrationLog"></a> Migrazione  
 Nella tabella seguente sono elencati i file di log contenenti informazioni correlate alla migrazione.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|migmctrl.log|Registra informazioni sulle azioni di migrazione riguardanti processi di migrazione, punti di distribuzione condivisi e aggiornamenti dei punti di distribuzione.|Sito principale della gerarchia di Configuration Manager e ogni sito primario figlio<br /><br /> In una gerarchia che include più siti primari, usare il file di log creato nel sito di amministrazione centrale.|  

###  <a name="a-namebkmkmdmloga-mobile-devices"></a><a name="BKMK_MDMLog"></a> Dispositivi mobili  
 Nelle sezioni seguenti vengono elencati i file di log contenenti informazioni correlate alla gestione dei dispositivi mobili.  

####  <a name="a-namebkmkenrollmentloga-enrollment"></a><a name="BKMK_EnrollmentLog"></a> Registrazione  
 Nella tabella seguente sono elencati i registri che contengono informazioni correlate alla registrazione dei dispositivi mobili.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|DMPRP.log|Registra le comunicazione tra i punti di gestione abilitati per dispositivi mobili e gli endpoint dei punti di gestione.|Server del sistema del sito|  
|dmpmsi.log|Registra i dati di Windows Installer per la configurazione di un punto di gestione abilitato per i dispositivi mobili.|Server del sistema del sito|  
|DMPSetup.log|Registra la configurazione del punto di gestione quando è abilitato per i dispositivi mobili.|Server del sistema del sito|  
|enrollsrvMSI.log|Registra i dati di Windows Installer per la configurazione di un punto di registrazione.|Server del sistema del sito|  
|enrollmentweb.log|Registra le comunicazioni tra dispositivi mobili e il punto di registrazione.|Server del sistema del sito|  
|enrollwebMSI.log|Registra i dati di Windows Installer per la configurazione di un punto proxy di registrazione.|Server del sistema del sito|  
|enrollmentservice.log|Registra le comunicazioni tra un punto proxy di registrazione e un punto di registrazione.|Server del sistema del sito|  
|SMS_DM.log|Registra le comunicazioni tra dispositivi mobili, computer Mac e il punto di gestione abilitato per dispositivi mobili e computer Mac.|Server del sistema del sito|  

####  <a name="a-namebkmkexchsrvloga-exchange-server-connector"></a><a name="BKMK_ExchSrvLog"></a> Connettore Exchange Server  
 Nella tabella seguente sono elencati i registri che contengono informazioni relative al connettore Exchange Server.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|easdisc.log|Registra le attività e lo stato del connettore Exchange Server.|Server del sito|  

####  <a name="a-namebkmkmdlegloga-mobile-device-legacy"></a><a name="BKMK_MDLegLog"></a> Dispositivo mobile legacy  
 Nella tabella seguente sono elencati i registri che contengono informazioni correlate al client di dispositivi mobili legacy.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|DmCertEnroll.log|Registra informazioni dettagliate sui dati di registrazione del certificato nei client dei dispositivi mobili legacy.|Client|  
|DMCertResp.htm|Registra la risposta HTML ricevuta dal server del certificato quando il programma legacy di registrazione client del dispositivo mobile richiede un certificato PKI.|Client|  
|DmClientHealth.log|Registra i GUID di tutti i client legacy dei dispositivi mobili che comunicano con il punto di gestione abilitato per i dispositivi mobili.|Server del sistema del sito|  
|DmClientRegistration.log|Registra le richieste di registrazione e le relative risposte ricevute e trasmesse dai client legacy dei dispositivi mobili.|Server del sistema del sito|  
|DmClientSetup.log|Registra i dati di installazione dei client legacy dei dispositivi mobili.|Client|  
|DmClientXfer.log|Registra i dati di trasferimento dei client legacy dei dispositivi mobili e delle distribuzioni di ActiveSync.|Client|  
|DmCommonInstaller.log|Registra l'installazione dei file di trasferimento per la configurazione dei file di trasferimento dei client legacy dei dispositivi mobili.|Client|  
|DmInstaller.log|Registra l'esito della chiamata da DMInstaller a DmClientSetup e l'esito dell'esecuzione di DmClientSetup per i client legacy dei dispositivi mobili.|Client|  
|DmpDatastore.log|Registra tutte le connessioni al database del sito e le query eseguite dal punto di gestione abilitato per i dispositivi mobili.|Server del sistema del sito|  
|DmpDiscovery.log|Registra tutti i dati di individuazione ricevuti dai client legacy dei dispositivi mobili nel punto di gestione abilitato per i dispositivi mobili.|Server del sistema del sito|  
|DmpHardware.log|Registra i dati di individuazione hardware ricevuti dai client legacy dei dispositivi mobili nel punto di gestione abilitato per i dispositivi mobili.|Server del sistema del sito|  
|DmpIsapi.log|Registra la comunicazione tra i client legacy dei dispositivi mobili e un punto di gestione abilitato per i dispositivi mobili.|Server del sistema del sito|  
|dmpmsi.log|Registra i dati di Windows Installer per la configurazione di un punto di gestione abilitato per i dispositivi mobili.|Server del sistema del sito|  
|DMPSetup.log|Registra la configurazione del punto di gestione quando è abilitato per i dispositivi mobili.|Server del sistema del sito|  
|DmpSoftware.log|Registra i dati di distribuzione software ricevuti dai client legacy dei dispositivi mobili in un punto di gestione abilitato per i dispositivi mobili.|Server del sistema del sito|  
|DmpStatus.log|Registra i dati dei messaggi di stato ricevuti dai client legacy dei dispositivi mobili in un punto di gestione abilitato per i dispositivi mobili.|Server del sistema del sito|  
|DmSvc.log|Registra la comunicazione tra i client legacy dei dispositivi mobili e un punto di gestione abilitato per i dispositivi mobili.|Client|  
|FspIsapi.log|Registra le comunicazioni verso il punto di stato di fallback da client legacy di dispositivi mobili e da computer client.|Server del sistema del sito|  

###  <a name="a-namebkmkosdloga-operating-system-deployment"></a><a name="BKMK_OSDLog"></a> Distribuzione del sistema operativo  
 Nella tabella seguente sono elencati i file di log contenenti informazioni correlate alla distribuzione del sistema operativo.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|CAS.log|Registra informazioni dettagliate quando vengono rilevati punti di distribuzione per il contenuto a cui si fa riferimento.|Client|  
|ccmsetup.log|Registra le attività svolte da **ccmsetup** per l'installazione, l'aggiornamento e la rimozione dei client. Può essere usato per la risoluzione dei problemi di installazione dei client.|Client|  
|CreateTSMedia.log|Registra informazioni dettagliate sulla creazione del supporto per la sequenza di attività.|Computer che esegue la console di Configuration Manager|  
|DeployToVhd.log|Registra dettagli relativi al processo di creazione e di modifica del disco rigido virtuale|Computer che esegue la console di Configuration Manager|  
|Dism.log|Registra azioni di installazione driver o di applicazione aggiornamenti per la manutenzione offline.|Server del sistema del sito|  
|distmgr.log|Registra informazioni dettagliate sulla configurazione per l'attivazione di un punto di distribuzione per PXE.|Server del sistema del sito|  
|DriverCatalog.log|Registra informazioni dettagliate sui driver di dispositivo importati nel catalogo dei driver.|Server del sistema del sito|  
|mcsisapi.log|Registra informazioni sul trasferimento dei pacchetti multicast e le risposte alle richieste dei client.|Server del sistema del sito|  
|mcsexec.log|Registra le azioni relative a controllo di integrità, spazio dei nomi, creazione delle sessioni e controllo certificati.|Server del sistema del sito|  
|mcsmgr.log|Registra le modifiche alla configurazione, alla modalità di protezione e alla disponibilità.|Server del sistema del sito|  
|mcsprv.log|Registra l'interazione tra il provider multicast e i Servizi di distribuzione Windows (WDS).|Server del sistema del sito|  
|MCSSetup.log|Registra informazioni dettagliate sull'installazione del ruolo server multicast.|Server del sistema del sito|  
|MCSMSI.log|Registra informazioni dettagliate sull'installazione del ruolo server multicast.|Server del sistema del sito|  
|Mcsperf.log|Registra informazioni dettagliate sull'aggiornamento dei contatori delle prestazioni multicast.|Server del sistema del sito|  
|MP_ClientIDManager.log|Registra le risposte del punto di gestione alle sequenze attività di richiesta ID client originate dal supporto di avvio o tramite PXE.|Server del sistema del sito|  
|MP_DriverManager.log|Registra le risposte del punto di gestione alle richieste dell'operazione sequenza di attività Applica automaticamente i driver.|Server del sistema del sito|  
|OfflineServicingMgr.log|Registra informazioni dettagliate sulle pianificazioni della manutenzione offline e sulle azioni di applicazione aggiornamenti sui file WIM del sistema operativo.|Server del sistema del sito|  
|Setupact.log|Registra informazioni dettagliate sui registri di Windows Sysprep e di installazione.|Client|  
|Setupapi.log|Registra informazioni dettagliate sui registri di Windows Sysprep e di installazione.|Client|  
|Setuperr.log|Registra informazioni dettagliate sui registri di Windows Sysprep e di installazione.|Client|  
|smpisapi.log|Registra informazioni dettagliate sulle azioni di acquisizione e ripristino dello stato del client, nonché informazioni sulle soglie.|Client|  
|Smpmgr.log|Registra informazioni dettagliate sui risultati dei controlli di integrità del punto di migrazione stato e delle modifiche della configurazione.|Server del sistema del sito|  
|smpmsi.log|Registra informazioni dettagliate di installazione e configurazione relative al punto di migrazione stato.|Server del sistema del sito|  
|smpperf.log|Registra gli aggiornamenti del contatore delle prestazioni del punto di migrazione stato.|Server del sistema del sito|  
|smspxe.log|Registra informazioni dettagliate sulle risposte ai client avviati tramite PXE e sull'espansione delle immagini di avvio e dei file di avvio.|Server del sistema del sito|  
|smssmpsetup.log|Registra informazioni dettagliate di installazione e configurazione relative al punto di migrazione stato.|Server del sistema del sito|  
|Smsts.log|Registra le attività delle sequenze attività.|Client|  
|TSAgent.log|Registra l'esito delle dipendenze delle sequenze di attività prima di avviare una sequenza di attività.|Client|  
|TaskSequenceProvider.log|Registra informazioni dettagliate sull'importazione, l'esportazione o la modifica delle sequenze attività.|Server del sistema del sito|  
|loadstate.log|Registra informazioni dettagliate sull'Utilità di migrazione stato utente (USMT) e il ripristino dei dati sullo stato dell'utente.|Client|  
|scanstate.log|Registra informazioni dettagliate sull'Utilità di migrazione stato utente (USMT) e l'acquisizione dei dati sullo stato dell'utente.|Client|  

###  <a name="a-namebkmkpowermgmtloga-power-management"></a><a name="BKMK_PowerMgmtLog"></a> Risparmio energia  
 Nella tabella seguente sono elencati i file di log contenenti informazioni correlate al risparmio energia.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|Pwrmgmt.log|Registra informazioni dettagliate sulle attività di risparmio energia sul computer client, che includono il monitoraggio e l'applicazione delle impostazioni da parte dell'agente client di Risparmio energia.|Client|  

###  <a name="a-namebkmkrcloga-remote-control"></a><a name="BKMK_RCLog"></a> Controllo remoto  
 Nella tabella seguente sono elencati i file di log contenenti informazioni correlate al controllo remoto.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|CMRcViewer.log|Registra informazioni dettagliate sull'attività del visualizzatore controllo remoto.|Nella cartella *%temp%* del computer che esegue il visualizzatore controllo remoto.|  

###  <a name="a-namebkmkreportloga-reporting"></a><a name="BKMK_ReportLog"></a> Creazione di report  
 Nella tabella seguente sono elencati i file di log di Configuration Manager contenenti informazioni correlate al reporting.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|srsrp.log|Registra informazioni sulle attività e lo stato del punto di Reporting Services.|Server del sistema del sito|  
|srsrpMSI.log|Registra informazioni dettagliate sui risultati del processo di installazione del punto di Reporting Services dall'output MSI.|Server del sistema del sito|  
|srsrpsetup.log|Registra i risultati del processo di installazione del punto di Reporting Services.|Server del sistema del sito|  

###  <a name="a-namebkmkrbaloga-role-based-administration"></a><a name="BKMK_RBALog"></a> Amministrazione basata su ruoli  
 Nella tabella seguente sono elencati i file di log contenenti informazioni correlate alla gestione dell'amministrazione basata su ruoli.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|hman.log|Registra informazioni sulle modifiche della configurazione del sito e sulla pubblicazione delle informazioni del sito in Servizi di dominio Active Directory.|Server del sito|  
|SMSProv.log|Registra gli accessi del provider WMI al database del sito.|Computer con il provider SMS|  

###  <a name="a-namebkmkwitloga-service-connection-point"></a><a name="BKMK_WITLog"></a> Punto di connessione del servizio  
 La tabella seguente elenca i file di log contenenti informazioni correlate al punto di connessione del servizio.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|CertMgr.log|Registra informazioni sul certificato e sull'account proxy.|Server del sito|  
|CollEval.log|Registra dettagli sul momento in cui le raccolte vengono create, modificate ed eliminate dall'analizzatore di raccolte.|Sito primario e sito di amministrazione centrale|  
|Cloudusersync.log|Registra l'attivazione della licenza per gli utenti.|Computer con il punto di connessione del servizio|  
|Dataldr.log|Registra informazioni sull'elaborazione dei file MIF.|Server del sito|  
|ddm.log|Registra le attività di Gestione individuazione dati.|Server del sito|  
|distmgr.log|Registra informazioni dettagliate sulle richieste di distribuzione del contenuto.|Server del sito principale|  
|Dmpdownloader.log|Registra informazioni dettagliate sui download da Microsoft Intune.|Computer con il punto di connessione del servizio|  
|Dmpuploader.log|Registra informazioni dettagliate sul caricamento delle modifiche del database in Microsoft Intune.|Computer con il punto di connessione del servizio|  
|hman.log|Registra informazioni sull'inoltro dei messaggi.|Server del sito|  
|objreplmgr.log|Registra l'elaborazione di criteri e assegnazione.|Server del sito primario|  
|policypv.log|Registra la generazione di tutti i criteri.|Server del sito|  
|outgoingcontentmanager.log|Registra il contenuto caricato in Microsoft Intune.|Computer con il punto di connessione del servizio|  
|Sitecomp.log|Registra informazioni dettagliate sull'installazione del punto di connessione del servizio.|Server del sito|  
|SmsAdminUI.log|Registra l'attività della console di Configuration Manager.|Computer che esegue la console di Configuration Manager|  
|Smsprov.log|Registra le attività eseguite dal provider SMS. Le attività della console di Configuration Manager usano il provider SMS.|Computer con il provider SMS|  
|SrvBoot.log|Registra informazioni dettagliate sul servizio di installazione del punto di connessione del servizio.|Computer con il punto di connessione del servizio|  
|Statesys.log|Registra l'elaborazione dei messaggi di gestione dei dispositivi mobili.|Sito primario e sito di amministrazione centrale|  

###  <a name="a-namebkmksunaploga-software-updates"></a><a name="BKMK_SU_NAPLog"></a> Aggiornamenti software  
 La tabella seguente elenca i file di log contenenti informazioni correlate agli aggiornamenti software.  Inoltre, alcuni dettagli rimangono correlati a Protezione accesso alla rete, una funzionalità che non è più disponibile in System Center Configuration Manager.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|ccmcca.log|Registra informazioni dettagliate sull'esecuzione della valutazione di conformità basata sull'analisi dei criteri di Protezione accesso alla rete di Configuration Manager e contiene l'elaborazione della correzione per ogni aggiornamento software necessario ai fini della conformità.|Client|  
|ccmperf.log|Registra le attività di manutenzione e acquisizione dati correlate ai contatori delle prestazioni dei client.|Client|  
|PatchDownloader.log|Registra informazioni dettagliate sul processo di download degli aggiornamenti software dall'origine degli aggiornamenti alla destinazione del download sul server del sito.|Computer che ospita la console di Configuration Manager da cui vengono avviati i download|  
|PolicyEvaluator.log|Registra informazioni dettagliate sulla valutazione dei criteri nei computer client, inclusi quelli derivanti dagli aggiornamenti software.|Client|  
|RebootCoordinator.log|Registra informazioni dettagliate sul coordinamento dei riavvii del sistema nei computer client dopo le installazioni degli aggiornamenti software.|Client|  
|ScanAgent.log|Registra informazioni dettagliate sulle richieste di ricerca di aggiornamenti software, sulla posizione di WSUS e sulle azioni correlate.|Client|  
|SdmAgent.log|Registra informazioni dettagliate sul monitoraggio di aggiornamenti e conformità. Il file di log degli aggiornamenti software, Updateshandler.log, fornisce comunque informazioni più dettagliate sull'installazione degli aggiornamenti software necessari per la conformità.<br /><br /> Questo file di log viene condiviso con le impostazioni di conformità.|Client|  
|ServiceWindowManager.log|Registra informazioni dettagliate sulla valutazione delle finestre di manutenzione.|Client|  
|smssha.log|File di log principale del client di Protezione accesso alla rete di Configuration Manager contenente un rendiconto unificato delle informazioni di integrità dei due componenti di Configuration Manager: servizi di posizione (LS) e agente di conformità della configurazione (CCA). Questo file di log contiene inoltre informazioni sulle interazioni tra l'agente integrità sistema di Configuration Manager e l'agente di Protezione accesso alla rete del sistema operativo, oltre che tra l'agente integrità sistema di Configuration Manager e Configuration Compliance Agent, unitamente a Location Services. Offre informazioni sull'esito dell'inizializzazione dell'agente di Protezione accesso alla rete, il rapporto sui dati di integrità e il rapporto sulla risposta di integrità.|Client|  
|Smsshv.log|È il file di log principale per il punto di Convalida integrità sistema e registra le operazioni di base del servizio Convalida integrità sistema, come l'avanzamento dell'inizializzazione.|Server del sistema del sito|  
|Smsshvadcacheclient.log|Registra informazioni dettagliate sul recupero dei riferimenti sullo stato di integrità di Configuration Manager da Active Directory Domain Services.|Server del sistema del sito|  
|SmsSHVCacheStore.log|Registra informazioni dettagliate sull'archivio cache usato per conservare i riferimenti sullo stato di integrità di Protezione accesso alla rete di Configuration Manager recuperati da Active Directory Domain Services, quali la lettura dall'archivio e l'eliminazione delle voci dal file dell'archivio cache locale. L'archivio cache non è configurabile.|Server del sistema del sito|  
|smsSHVQuarValidator.log|Registra il rapporto del client sulle informazioni di integrità e le operazioni di elaborazione. Per ottenere informazioni complete, modificare la chiave del Registro di sistema **LogLevel** da 1 a 0 nel percorso seguente: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMSSHV\Logging\\@GLOBAL**|Server del sistema del sito|  
|smsshvregistrysettings.log|Registra ogni modifica dinamica apportata alla configurazione del componente Convalida integrità sistema mentre il servizio è in esecuzione.|Server del sistema del sito|  
|SMSSHVSetup.log|Registra l'esito positivo o negativo (con il motivo dell'errore) dell'installazione del punto di Convalida integrità sistema.|Server del sistema del sito|  
|SmsWusHandler.log|Registra informazioni dettagliate sul processo di analisi per lo strumento di inventario per Microsoft Updates.|Client|  
|StateMessage.log|Registra informazioni dettagliate sui messaggi di stato dell'aggiornamento software creati e inviati al punto di gestione.|Client|  
|SUPSetup.log|Registra informazioni dettagliate sull'installazione del punto di aggiornamento software. Al termine dell'installazione del punto di aggiornamento software, **Installation was successful** viene scritto nel file di log.|Server del sistema del sito|  
|UpdatesDeployment.log|Registra informazioni dettagliate sulle distribuzioni nel client, comprese l'attivazione, la valutazione e l'applicazione degli aggiornamenti software. La registrazione dettagliata visualizza informazioni aggiuntive sull'interazione con l'interfaccia utente del client.|Client|  
|UpdatesHandler.log|Registra informazioni dettagliate sull'analisi della conformità degli aggiornamenti software e sul download e l'installazione di aggiornamenti software nel client.|Client|  
|UpdatesStore.log|Registra informazioni dettagliate sullo stato di conformità degli aggiornamenti software ottenuto durante il ciclo di analisi della conformità.|Client|  
|WCM.log|Registra informazioni dettagliate sulle configurazioni e le connessioni del punto di aggiornamento software e sulle connessioni al server di Windows Server Update Services (WSUS) per categorie di aggiornamento, classificazioni e lingue sottoscritte.|Server del sito|  
|WSUSCtrl.log|Registra informazioni dettagliate su configurazione, connettività al database e integrità del server WSUS per il sito.|Server del sistema del sito|  
|wsyncmgr.log|Registra informazioni dettagliate sul processo di sincronizzazione degli aggiornamenti software.|Server del sito|  
|WUAHandler.log|Registra informazioni dettagliate sull'agente di Windows Update nel client durante la ricerca di aggiornamenti software.|Client|  

###  <a name="a-namebkmkwolloga-wake-on-lan"></a><a name="BKMK_WOLLog"></a> Riattivazione LAN  
 Nella tabella seguente sono elencati i file di log contenenti informazioni relative all'utilizzo della riattivazione LAN.  

> [!NOTE]  
>  Se si integra la riattivazione LAN usando il proxy di riattivazione, questa attività viene registrata nel client. Ad esempio, vedere CcmExec.log e SleepAgent_&lt;dominio\>@SYSTEM_0.log nella sezione [Operazioni client](#BKMK_ClientOpLogs) di questo argomento.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|wolcmgr.log|Registra informazioni dettagliate sui client ai quali è necessario inviare pacchetti di riattivazione, sul numero di pacchetti di riattivazione inviati e sul numero di pacchetti di riattivazione inviati nuovamente.|Server del sito|  
|wolmgr.log|Registra informazioni dettagliate sulle procedure di riattivazione, ad esempio sul momento in cui riattivare distribuzioni configurate per la riattivazione LAN.|Server del sito|  

###  <a name="a-namebkmkwuloga-windows-update-agent"></a><a name="BKMK_WULog"></a> Agente di Windows Update  
 Nella tabella seguente sono elencati i file di log contenenti informazioni correlate all'agente di Windows Update.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|WindowsUpdate.log|Registra informazioni dettagliate che indicano il momento in cui l'agente di Windows Update si connette al server WSUS e ritenta gli aggiornamenti software per la valutazione della conformità e se vi sono aggiornamenti per i componenti dell'agente.|Client|  

###  <a name="a-namebkmkwsusloga-wsus-server"></a><a name="BKMK_WSUSLog"></a> Server WSUS  
 Nella tabella seguente sono elencati i file di log contenenti informazioni correlate al server WSUS.  

|Nome registro|Descrizione|Computer con file di log|  
|--------------|-----------------|----------------------------|  
|Change.log|Registra informazioni dettagliate sulle informazioni modificate del database del server WSUS.|Server WSUS|  
|SoftwareDistribution.log|Registra informazioni dettagliate sugli aggiornamenti software sincronizzati dall'origine aggiornamenti configurata al database del server WSUS.|Server WSUS|  



<!--HONumber=Nov16_HO1-->



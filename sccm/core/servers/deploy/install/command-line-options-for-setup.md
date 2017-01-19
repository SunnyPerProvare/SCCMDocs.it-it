---
title: Opzioni della riga di comando per la configurazione | Microsoft Docs
description: Usare le informazioni in questo articolo per configurare gli script o installare System Center Configuration Manager dalla riga di comando.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: f2b5a1dfa654a30e03bce2b56100bc876358c9fe

---
# <a name="command-line-options-for-setup-for-system-center-configuration-manager"></a>Opzioni della riga di comando per il programma di installazione in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


 Quando si configurano gli script oppure si installa System Center Configuration Manager dalla riga di comando, usare le informazioni riportate nelle tabelle seguenti.  

##  <a name="a-namebkmksetupa-command-line-options-for-setup"></a><a name="bkmk_setup"></a> Opzioni della riga di comando per il programma di installazione  
 **/DEINSTALL**  
 Consente di disinstallare il sito. È necessario eseguire il programma di installazione dal computer del server del sito.  

 **/DONTSTARTSITECOMP**  
 Consente di installare un sito, ma impedisce l'avvio del servizio Gestione componenti del sito. Fino all'avvio del servizio Gestione componenti del sito, il sito non è attivo. Gestione componenti del sito si occupa dell'installazione e dell'avvio del servizio SMS_Executive, nonché di processi aggiuntivi nel sito. Al termine dell'installazione del sito, in seguito all'avvio del servizio Gestione componenti del sito verranno installati SMS_Executive e processi aggiuntivi necessari per il funzionamento del sito.  

 **/HIDDEN**  
 Consente di nascondere l'interfaccia utente durante l'installazione. Questa opzione deve essere usata in combinazione con l'opzione **/SCRIPT** e il file script di installazione automatica deve fornire tutte le opzioni necessarie. In caso contrario, l'installazione dà esito negativo.  

 **/NOUSERINPUT**  
 Consente di disattivare l'input utente durante l'installazione, ma viene visualizzata l'interfaccia **Installazione guidata** . Questa opzione deve essere usata in combinazione con l'opzione **/SCRIPT** e il file script di installazione automatica deve fornire tutte le opzioni necessarie. In caso contrario, l'installazione dà esito negativo.  

 **/RESETSITE**  
 Consente di eseguire una reimpostazione del sito per reimpostare gli account di servizio e di database per il sito. È necessario eseguire il programma di installazione da **&lt;ConfigMgrInstallationPath\>\BIN\X64** sul server del sito. Per altre informazioni sulla reimpostazione del sito, vedere la sezione [Run a site reset](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_reset) (Eseguire la reimpostazione del sito) nell'argomento [Modify your System Center Configuration Manager infrastructure](../../../../core/servers/manage/modify-your-infrastructure.md) (Modificare l'infrastruttura di System Center Configuration Manager).  

 **/TESTDBUPGRADE &lt;*InstanceName\DatabaseName*>**  
 Consente di eseguire un test in un backup del database del sito per verificare che l'aggiornamento possa essere eseguito. È necessario fornire il nome dell'istanza e il nome del database per il database del sito. Se viene specificato solo il nome del database, il programma di installazione usa il nome dell'istanza predefinita.  

> [!IMPORTANT]  
>  Non è supportata l'esecuzione di questa opzione della riga di comando nel database del sito di produzione. Questa operazione consente di aggiornare il database del sito e potrebbe rendere inutilizzabile il sito.  

 **/UPGRADE**  
 Consente di eseguire l'aggiornamento automatico di un sito. Quando si usa /UPGRADE, è inoltre necessario specificare il codice Product Key, compresi i trattini (-). È inoltre necessario specificare il percorso dei file dei prerequisiti di installazione scaricati in precedenza.  

 Esempio: **setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx &lt;percorso a file componente esterni\>**  

 Per altre informazioni sui file dei prerequisiti di installazione, vedere la sezione  [Downloader di installazione](#bkmk_SetupDownloader) in questo argomento.  

 **/SCRIPT &lt;*SetupScriptPath*>**  
 consente di eseguire installazioni automatiche. Quando si usa l'opzione **/SCRIPT** è richiesto un file di inizializzazione dell'installazione. Per altre informazioni su come eseguire l'installazione automatica, vedere [Install sites using a command line](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md) (Installare siti tramite riga di comando).  

 **/SDKINST &lt;*FQDN*>**  
 Consente di installare il provider SMS nel computer specificato. È necessario specificare l'FQDN per il computer del provider SMS. Per altre informazioni sul provider SMS, vedere [Plan for the SMS Provider for System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) (Pianificare il provider SMS per System Center Configuration Manager).  

 **/SDKDEINST &lt;*FQDN*>**  
 Consente di disinstallare il provider SMS nel computer specificato. È necessario specificare l'FQDN per il computer del provider SMS.  

 **/MANAGELANGS &lt;*LanguageScriptPath*>**  
 gestisce le lingue installate in un sito installato precedentemente. Per usare questa opzione, è necessario eseguire il programma di installazione da **&lt;ConfigMgrInstallationPath\>\BIN\X64** nel server del sito e specificare il percorso del file script delle lingue che contiene le impostazioni relative alle lingue. Per altre informazioni sulle opzioni della lingua disponibili nel file script di configurazione della lingua, vedere la sezione [Opzioni della riga di comando per la gestione delle lingue](#bkmk_Lang) in questo argomento.  

##  <a name="a-namebkmklanga-command-line-options-to-manage-languages"></a><a name="bkmk_Lang"></a> Opzioni della riga di comando per la gestione delle lingue  
 **Identification**  

-   **Nome chiave:** Action  

    -   **Richiesto:** sì  

    -   **Valori:** ManageLanguages  

    -   **Dettagli:** gestisce il supporto lingua di client per dispositivi mobili, client e server in un sito.  

**Opzioni**  

-   **Nome chiave:** AddServerLanguages  

    -   **Richiesto:** no  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** specifica le lingue del server che saranno disponibili per la console di Configuration Manager, i report e gli oggetti di Configuration Manager. L'inglese è disponibile per impostazione predefinita.  

-   **Nome chiave:** AddClientLanguages  

    -   **Richiesto:** no  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** specifica le lingue che saranno disponibili per i computer client. L'inglese è disponibile per impostazione predefinita.  

-   **Nome chiave:** DeleteServerLanguages  

    -   **Richiesto:** no  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** specifica le lingue da rimuovere, che non saranno più disponibili per la console di Configuration Manager, i report e gli oggetti di Configuration Manager. La lingua inglese è disponibile per impostazione predefinita e non può essere rimossa.  

-   **Nome chiave:** DeleteClientLanguages  

    -   **Richiesto:** no  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** specifica le lingue da rimuovere, che non saranno più disponibili per i computer client. La lingua inglese è disponibile per impostazione predefinita e non può essere rimossa.  

-   **Nome chiave:** MobileDeviceLanguage  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = non installare  

         1 = installa  

    -   **Dettagli:** specifica se sono installate le lingue del client del dispositivo mobile.  

-   **Nome chiave:** PrerequisiteComp  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = scarica  

         1 = già scaricato  

    -   **Dettagli:** specifica se i file dei prerequisiti di installazione sono già stati scaricati. Se ad esempio si usa un valore pari a 0, il programma di installazione eseguirà il download dei file.  

-   **Nome chiave:** PrerequisitePath  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Dettagli:** specifica il percorso dei file dei prerequisiti di installazione. A seconda del valore di **PrerequisiteComp** , il programma di installazione usa questo percorso per archiviare i file scaricati oppure per individuare i file scaricati in precedenza.  

##  <a name="a-namebkmkunattendeda-unattended-setup-script-file-keys"></a><a name="bkmk_Unattended"></a> Chiavi di file script di installazione automatica  
 Usare le seguenti sezioni per creare lo script per l'installazione automatica. Nelle tabelle sono elencate le chiavi dello script di installazione, i relativi valori, se richiesti, il tipo di installazione per cui vengono usate e una breve descrizione relativa alla chiave.  

### <a name="unattended-install-for-a-central-administration-site"></a>Installare automaticamente un sito di amministrazione centrale  
 Usare i dettagli seguenti per installare un sito di amministrazione centrale usando un file script di installazione automatica.  

**Identification**  

-   **Nome chiave:** Action  

    -   **Richiesto:** sì  

    -   **Valori:** InstallCAS  

    -   **Dettagli:** consente di installare un sito di amministrazione centrale.  

**Opzioni**  

-   **Nome chiave:** ProductID  

    -   **Richiesto:** sì  

    -   **Valori:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* o *Eval*  

    -   **Dettagli:** specifica il codice Product Key per l'installazione di Configuration Manager, trattini inclusi. Immettere **Eval** per installare la versione di valutazione di Configuration Manager.  

-   **Nome chiave:** SiteCode  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;*SiteCode*>  

    -   **Dettagli:** specifica i tre caratteri alfanumerici che identificano in modo univoco il sito nella gerarchia.  

-   **Nome chiave:** SiteName  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;*SiteName*>  

    -   **Dettagli:** specifica il nome del sito.  

-   **Nome chiave:** SMSInstallDir  

    -   **Richiesto:** sì  

    -   **Valori:** *ConfigMgrInstallationPath*  

    -   **Dettagli:** specifica la cartella di installazione per i file di programma di Configuration Manager.  

-   **Nome chiave:** SDKServer  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;*FQDN del provider SMS*>  

    -   **Dettagli:** specifica l'FQDN del server che ospiterà il provider SMS.  
        Dopo l'installazione iniziale, è possibile configurare altri provider SMS per il sito.  

-   **Nome chiave:** PrerequisiteComp  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = scarica  

         1 = già scaricato  

    -   **Dettagli:** specifica se i file dei prerequisiti di installazione sono già stati scaricati. Se ad esempio si usa un valore pari a 0, il programma di installazione eseguirà il download dei file.  

-   **Nome chiave:** PrerequisitePath  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Dettagli:** specifica il percorso dei file dei prerequisiti di installazione. A seconda del valore di PrerequisiteComp, il programma di installazione usa questo percorso per archiviare i file scaricati oppure per individuare i file scaricati in precedenza.  

-   **Nome chiave:** AdminConsole  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = non installare  

         1 = installa  

    -   **Dettagli:** specifica se installare la console di Configuration Manager.  

-   **Nome chiave:** JoinCEIP  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = non partecipare  

         1 = partecipa  

    -   **Dettagli:** specifica se partecipare al programma Analisi utilizzo software.  

-   **Nome chiave:** AddServerLanguages  

    -   **Richiesto:** no  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** specifica le lingue del server che saranno disponibili per la console di Configuration Manager, i report e gli oggetti di Configuration Manager. L'inglese è disponibile per impostazione predefinita.  

-   **Nome chiave:** AddClientLanguages  

    -   **Richiesto:** no  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** specifica le lingue che saranno disponibili per i computer client. L'inglese è disponibile per impostazione predefinita.  

-   **Nome chiave:** DeleteServerLanguages  

    -   **Richiesto:** no  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** modifica un sito dopo l'installazione.  
        Specifica le lingue da rimuovere che non saranno più disponibili per la console di Configuration Manager, i report e gli oggetti di Configuration Manager. La lingua inglese è disponibile per impostazione predefinita e non può essere rimossa.  

-   **Nome chiave:** DeleteClientLanguages  

    -   **Richiesto:** no  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** modifica un sito dopo l'installazione.  
        Specifica le lingue da rimuovere, che non saranno disponibili per i computer client. La lingua inglese è disponibile per impostazione predefinita e non può essere rimossa.  

-   **Nome chiave:** MobileDeviceLanguage  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = non installare  

         1 = installa  

    -   **Dettagli:** specifica se sono installate le lingue del client del dispositivo mobile.  

**SQLConfigOptions**  

-   **Nome chiave:** SQLServerName  

    -   **Richiesto:** sì  

    -   **Valori:** *NomeSQLServer*  

    -   **Dettagli:** specifica il nome del server o il nome dell'istanza in cluster che esegue SQL Server. Ospiterà il database del sito.  

-   **Nome chiave:** DatabaseName  

    -   **Richiesto:** sì  

    -   **Valori:** *&lt;NomeDatabaseSito\>* o *&lt;NomeIstanza\>\&lt; NomeDatabaseSito\>*  

    -   **Dettagli:**  

         Specifica il nome del database SQL Server da creare o usare per installare il database del sito di amministrazione centrale.  

        > [!IMPORTANT]  
        >  Se non si usa l'istanza predefinita, è necessario specificare il nome dell'istanza e il nome database del sito.  

-   **Nome chiave:** SQLSSBPort  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*NumeroPortaSSB*>  

    -   **Dettagli:** specifica la porta di SQL Server Service Broker (SSB) usata da SQL Server. In genere, SSB è configurato per usare la porta TCP 4022, ma sono supportate anche altre porte.  

-   **Nome chiave:** SQLDataFilePath  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*PercorsoFile per il file del database con estensione MDB*>  

    -   **Dettagli:** specifica un percorso alternativo per creare il file del database con estensione MDB.  

-   **Nome chiave:** SQLLogFilePath  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*PercorsoFile per il file del database con estensione LDF*>  

    -   **Dettagli:** specifica un percorso alternativo per creare il file del database con estensione LDF.  

**CloudConnectorOptions**  

-   **Nome chiave:** CloudConnector  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = non installare  

         1 = installa  

    -   **Dettagli:** specifica se installare un punto di connessione del servizio in questo sito. Visto che il punto di connessione può essere installato solo nel sito di livello superiore di una gerarchia, questo valore deve essere 0 per un sito primario figlio.  

-   **Nome chiave:** CloudConnectorServer  

    -   **Richiesto:** obbligatorio quando CloudConnector è uguale a 1  

    -   **Valori:** &lt;*FQDN server punto di connessione del servizio*>  

    -   **Dettagli:** specifica il nome FQDN del server che ospiterà il ruolo del sistema del sito del punto di connessione del servizio.  

-   **Nome chiave:** UseProxy  

    -   **Richiesto:** obbligatorio quando CloudConnector è uguale a 1  

    -   **Valori:** 0 o 1  

         0 = non installare  

         1 = installa  

    -   **Dettagli:** specifica se il punto di connessione del servizio userà un server proxy.  

-   **Nome chiave:** Nomeproxy  

    -   **Richiesto:** obbligatorio quando UseProxy è uguale a 1  

    -   **Valori:** &lt;*FQDN del server proxy*>  

    -   **Dettagli:** specifica il nome FQDN del server proxy che verrà usato dal ruolo del sistema del sito del punto di connessione del servizio.  

-   **Nome chiave:** ProxyPort  

    -   **Richiesto:** obbligatorio quando UseProxy è uguale a 1  

    -   **Valori:** &lt;*NumeroPorta*>  

    -   **Dettagli:** specifica il numero della porta da usare.  

### <a name="unattended-install-for-a-primary-site"></a>Installare automaticamente un sito primario  
Usare i dettagli seguenti per installare un sito primario usando un file script di installazione automatica.  

Usare i dettagli seguenti per installare un sito di amministrazione centrale usando un file script di installazione automatica.  

**Identification**  

-   **Nome chiave:** Action  

    -   **Richiesto:** sì  

    -   **Valori:** SitoPrimarioInstallazione  

    -   **Dettagli:** installa un sito primario.  

**Opzioni**  

-   **Nome chiave:** ProductID  

    -   **Richiesto:** sì  

    -   **Valori:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* o *Eval*  

    -   **Dettagli:** specifica il codice Product Key per l'installazione di Configuration Manager, trattini inclusi. Immettere **Eval** per installare la versione di valutazione di Configuration Manager.  

-   **Nome chiave:** SiteCode  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;*SiteCode*>  

    -   **Dettagli:** specifica i tre caratteri alfanumerici che identificano in modo univoco il sito nella gerarchia.  

-   **Nome chiave:** SiteName  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;*SiteName*>  

    -   **Dettagli:** specifica il nome del sito.  

-   **Nome chiave:** SMSInstallDir  

    -   **Richiesto:** sì  

    -   **Valori:** *ConfigMgrInstallationPath*  

    -   **Dettagli:** specifica la cartella di installazione per i file di programma di Configuration Manager.  

-   **Nome chiave:** SDKServer  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;*FQDN del provider SMS*>  

    -   **Dettagli:** specifica l'FQDN del server che ospiterà il provider SMS.  
        Dopo l'installazione iniziale, è possibile configurare altri provider SMS per il sito.  

-   **Nome chiave:** PrerequisiteComp  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = scarica  

         1 = già scaricato  

    -   **Dettagli:** specifica se i file dei prerequisiti di installazione sono già stati scaricati. Se ad esempio si usa un valore pari a 0, il programma di installazione eseguirà il download dei file.  

-   **Nome chiave:** PrerequisitePath  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Dettagli:** specifica il percorso dei file dei prerequisiti di installazione. A seconda del valore di **PrerequisiteComp** , il programma di installazione usa questo percorso per archiviare i file scaricati oppure per individuare i file scaricati in precedenza.  

-   **Nome chiave:** AdminConsole  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = non installare  

         1 = installa  

    -   **Dettagli:** specifica se installare la console di Configuration Manager.  

-   **Nome chiave:** JoinCEIP  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = non partecipare  

         1 = partecipa  

    -   **Dettagli:** specifica se partecipare al programma Analisi utilizzo software.  

-   **Nome chiave:** ManagementPoint  

    -   **Richiesto:** no  

    -   **Valori:** &lt;* FQDN server del sito del punto di gestione*>  

    -   **Dettagli:** specifica il nome FQDN del server che ospiterà il ruolo del sistema del sito del punto di gestione.  

-   **Nome chiave:** ManagementPointProtocol  

    -   **Richiesto:** no  

    -   **Valori:** HTTPS o HTTP  

    -   **Dettagli:** specifica il protocollo da usare per il punto di gestione.  

-   **Nome chiave:** DistributionPoint  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*FQDN server del sito del punto di distribuzione*>  

    -   **Dettagli:** specifica il protocollo da usare per il punto di gestione.  

-   **Nome chiave:** DistributionPointProtocol  

    -   **Richiesto:** no  

    -   **Valori:** HTTPS o HTTP  

    -   **Dettagli:** specifica il protocollo da usare per il punto di distribuzione.  

-   **Nome chiave:** RoleCommunicationProtocol  

    -   **Richiesto:** sì  

    -   **Valori:** EnforceHTTPS o HTTPorHTTPS  

    -   **Dettagli:** specifica se configurare tutti i sistemi del sito per l'accettazione delle sole comunicazioni HTTPS dai client oppure se configurare un metodo di comunicazione per ogni ruolo del sistema del sito. Se si seleziona **EnforceHTTPS**, il computer client deve disporre di un certificato PKI valido per l'autenticazione client.  

-   **Nome chiave:** ClientsUsePKICertificate  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = non usare  

         1 = usa  

    -   **Dettagli:** specifica se i client useranno un certificato PKI client per la comunicazione con i ruoli del sistema del sito.  

-   **Nome chiave:** AddServerLanguages  

    -   **Richiesto:** no  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** specifica le lingue del server che saranno disponibili per la console di Configuration Manager, i report e gli oggetti di Configuration Manager. L'inglese è disponibile per impostazione predefinita.  

-   **Nome chiave:** AddClientLanguages  

    -   **Richiesto:** no  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** specifica le lingue che saranno disponibili per i computer client. L'inglese è disponibile per impostazione predefinita.  

-   **Nome chiave:** DeleteServerLanguages  

    -   **Richiesto:** no  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** modifica un sito dopo l'installazione.  
        Specifica le lingue da rimuovere che non saranno più disponibili per la console di Configuration Manager, i report e gli oggetti di Configuration Manager. La lingua inglese è disponibile per impostazione predefinita e non può essere rimossa.  

-   **Nome chiave:** DeleteClientLanguages  

    -   **Richiesto:** no  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** modifica un sito dopo l'installazione.  
        Specifica le lingue da rimuovere, che non saranno disponibili per i computer client. La lingua inglese è disponibile per impostazione predefinita e non può essere rimossa.  

-   **Nome chiave:** MobileDeviceLanguage  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = non installare  

         1 = installa  

    -   **Dettagli:** specifica se sono installate le lingue del client del dispositivo mobile.  

**SQLConfigOptions**  

-   **Nome chiave:** SQLServerName  

    -   **Richiesto:** sì  

    -   **Valori:** *NomeSQLServer*  

    -   **Dettagli:** specifica il nome del server o il nome dell'istanza in cluster che esegue SQL Server. Ospiterà il database del sito.  

-   **Nome chiave:** DatabaseName  

    -   **Richiesto:** sì  

    -   **Valori:** *&lt;NomeDatabaseSito\>* o *&lt;NomeIstanza\>\&lt; NomeDatabaseSito\>*  

    -   **Dettagli:**  

         Specifica il nome del database SQL Server da creare o usare per installare il database del sito primario.  

        > [!IMPORTANT]  
        >  Se non si usa l'istanza predefinita, è necessario specificare il nome dell'istanza e il nome database del sito.  

-   **Nome chiave:** SQLSSBPort  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*NumeroPortaSSB*>  

    -   **Dettagli:** specifica la porta di SQL Server Service Broker (SSB) usata da SQL Server. In genere, SSB è configurato per usare la porta TCP 4022, ma sono supportate anche altre porte.  

-   **Nome chiave:** SQLDataFilePath  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*PercorsoFile per il file del database con estensione MDB*>  

    -   **Dettagli:** specifica un percorso alternativo per creare il file del database con estensione MDB.  

-   **Nome chiave:** SQLLogFilePath  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*PercorsoFile per il file del database con estensione LDF*>  

    -   **Dettagli:** specifica un percorso alternativo per creare il file del database con estensione LDF.  

**HierarchyExpansionOption**  

-   **Nome chiave:** CCARSiteServer  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*FQDN del sito di amministrazione centrale*>  

    -   **Dettagli:** specifica il sito di amministrazione centrale a cui si collegherà il sito primario quando verrà aggiunto alla gerarchia di Configuration Manager. Durante l'installazione, è necessario specificare il sito di amministrazione centrale.  

-   **Nome chiave:** CASRetryInterval  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*Intervallo*>  

    -   **Dettagli:** specifica l'intervallo (in minuti) tra i tentativi di connessione al sito di amministrazione centrale dopo l'errore di connessione. Se ad esempio si verifica un errore di connessione al sito di amministrazione centrale, il sito primario attende il numero di minuti specificato per CASRetryInterval e quindi tenta nuovamente di eseguire la connessione.  

-   **Nome chiave:** WaitForCASTimeout  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*Timeout*>  

         Un valore tra 0 e 100  

    -   **Dettagli:** specifica il valore di timeout massimo (in minuti) per la connessione di un sito primario al sito di amministrazione centrale. Se ad esempio un sito primario non riesce a connettersi al sito di amministrazione centrale, tale sito primario proverà nuovamente a connettersi al sito di amministrazione centrale in base a CASRetryInterval finché non viene raggiunto il periodo di WaitForCASTimeout. È possibile specificare un valore compreso tra 0 e 100.  

**CloudConnectorOptions**  

-   **Nome chiave:** CloudConnector  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = non installare  

         1 = installa  

    -   **Dettagli:** specifica se installare un punto di connessione del servizio in questo sito. Visto che il punto di connessione può essere installato solo nel sito di livello superiore di una gerarchia, questo valore deve essere 0 per un sito primario figlio.  

-   **Nome chiave:** CloudConnectorServer  

    -   **Richiesto:** obbligatorio quando CloudConnector è uguale a 1  

    -   **Valori:** &lt;*FQDN server punto di connessione del servizio*\>  

    -   **Dettagli:** specifica il nome FQDN del server che ospiterà il ruolo del sistema del sito del punto di connessione del servizio.  

-   **Nome chiave:** UseProxy  

    -   **Richiesto:** obbligatorio quando CloudConnector è uguale a 1  

    -   **Valori:** 0 o 1  

         0 = non installare  

         1 = installa  

    -   **Dettagli:** specifica se il punto di connessione del servizio userà un server proxy.  

-   **Nome chiave:** Nomeproxy  

    -   **Richiesto:** obbligatorio quando UseProxy è uguale a 1  

    -   **Valori:** &lt;*FQDN del server proxy*>  

    -   **Dettagli:** specifica il nome FQDN del server proxy che verrà usato dal ruolo del sistema del sito del punto di connessione del servizio.  

-   **Nome chiave:** ProxyPort  

    -   **Richiesto:** obbligatorio quando UseProxy è uguale a 1  

    -   **Valori:** &lt;*NumeroPorta*>  

    -   **Dettagli:** specifica il numero della porta da usare.  

### <a name="unattended-recovery-for-a-central-administration-site"></a>Ripristinare automaticamente un sito di amministrazione centrale  
 Usare i dettagli seguenti per ripristinare un sito di amministrazione centrale usando un file script di installazione automatica.  

**Identification**  

-   **Nome chiave:** Action  

    -   **Richiesto:** sì  

    -   **Valori:** RecoverCCAR  

    -   **Dettagli:** ripristina un sito di amministrazione centrale.  

**RecoveryOptions**  

-   **Nome chiave:** ServerRecoveryOptions  

    -   **Richiesto:** sì  

    -   **Valori:** 1, 2 o 4  

         1 = Ripristina il server del sito e SQL Server.  

         2 = Ripristina solo il server del sito.  

         4 = Ripristina solo SQL Server.  

    -   **Dettagli:** specifica se il programma di installazione ripristinerà il server del sito, SQL Server o entrambi. Le chiavi associate sono necessarie quando si imposta il valore seguente per l'impostazione ServerRecoveryOptions:  

        -   Valore = 1: è possibile specificare un valore per la chiave **SiteServerBackupLocation** per il ripristino del sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

        -   Valore = 2: è possibile specificare un valore per la chiave **SiteServerBackupLocation** per il ripristino del sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

        -   Valore = 4: la chiave **BackupLocation** è richiesta in caso di configurazione del valore **10** per la chiave **DatabaseRecoveryOptions** necessaria per il ripristino del database del sito dal backup.  

-   **Nome chiave:** DatabaseRecoveryOptions  

    -   **Richiesto:** questa chiave è richiesta quando l'impostazione ServerRecoveryOptions ha il valore **1** o **4**.  

    -   **Valori:** 10, 20, 40, 80  

         10 = Ripristina il database del sito dal backup.  

         20 = Usa un database del sito che è stato ripristinato manualmente usando un altro metodo.  

         40 = Crea un nuovo database per il sito. Usare questa opzione quando non è disponibile alcun backup di database del sito. I dati globali e i dati del sito vengono ripristinati tramite la replica da altri siti.  

         80 = Ignora il ripristino del database.  

    -   **Dettagli:** specifica il modo in cui il programma di installazione ripristina il database del sito in SQL Server.  

-   **Nome chiave:** ReferenceSite  

    -   **Richiesto:** questa chiave è richiesta quando l'impostazione **DatabaseRecoveryOptions** ha il valore **40**.  

    -   **Valori:** &lt;*FQDNSitoRiferimento*>  

    -   **Dettagli:** specifica il sito primario di riferimento usato dal sito di amministrazione centrale per il ripristino dei dati globali se il backup del database è antecedente al periodo di conservazione del rilevamento delle modifiche o se il sito viene ripristinato senza backup.  

         Se non viene specificato un sito di riferimento e il backup è antecedente al periodo di memorizzazione del rilevamento delle modifiche, tutti i siti primari vengono reinizializzati con i dati ripristinati dal sito di amministrazione centrale.  

         Se non viene specificato un sito di riferimento e il backup rientra nel periodo di memorizzazione del rilevamento delle modifiche, solo le modifiche apportate dal momento del backup verranno replicate dai siti primari. In caso di modifiche in conflitto provenienti da diversi siti primari, il sito di amministrazione centrale usa la prima modifica ricevuta.  

-   **Nome chiave:** SiteServerBackupLocation  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*PercorsoSetBackupServerSito*>  

    -   **Dettagli:** specifica il percorso del set di backup del server del sito. Questa chiave è facoltativa quando l'impostazione **ServerRecoveryOptions** ha il valore **1** o **2**. Specificare un valore affinché la chiave **SiteServerBackupLocation** ripristini il sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

-   **Nome chiave:** BackupLocation  

    -   **Richiesto:** la chiave è richiesta quando si configura il valore **1** o **4** per la chiave **ServerRecoveryOptions** e il valore **10** per la chiave **DatabaseRecoveryOptions**.  

    -   **Valori:** &lt;*PercorsoSetBackupDatabaseSito*>  

    -   **Dettagli:** specifica il percorso del set di backup del database del sito.  

**Opzioni**  

-   **Nome chiave:** ProductID  

    -   **Richiesto:** sì  

    -   **Valori:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* o *Eval*  

    -   **Dettagli:** specifica il codice Product Key per l'installazione di Configuration Manager, trattini inclusi. Immettere **Eval** per installare la versione di valutazione di Configuration Manager.  

-   **Nome chiave:** SiteCode  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;*SiteCode*>  

    -   **Dettagli:** specifica i tre caratteri alfanumerici che identificano in modo univoco il sito nella gerarchia. È necessario specificare il codice del sito usato dal sito prima dell'errore. Per altre informazioni sulle restrizioni relative al codice del sito, vedere la sezione [Nomi e codici dei siti](#bkmk_codes) in questo argomento.  

-   **Nome chiave:** SiteName  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*SiteName*>  

    -   **Dettagli:** specifica il nome del sito.  

-   **Nome chiave:** SMSInstallDir  

    -   **Richiesto:** sì  

    -   **Values:** &lt;*PercorsoInstallazioneConfigMg*>  

    -   **Dettagli:** specifica la cartella di installazione per i file di programma di Configuration Manager.  

-   **Nome chiave:** SDKServer  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;*FQDN del provider SMS*>  

    -   **Dettagli:** specifica l'FQDN del server che ospiterà il provider SMS. È necessario specificare il server che ospitava il provider SMS prima dell'errore.  

         Dopo l'installazione iniziale, è possibile configurare altri provider SMS per il sito. Per altre informazioni sul provider SMS, vedere [Plan for the SMS Provider for System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) (Pianificare il provider SMS per System Center Configuration Manager).  

-   **Nome chiave:** PrerequisiteComp  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = scarica  

         1 = già scaricato  

    -   **Dettagli:** specifica se i file dei prerequisiti di installazione sono già stati scaricati. Se ad esempio si usa un valore pari a **0**, il programma di installazione eseguirà il download dei file.  

-   **Nome chiave:** PrerequisitePath  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Dettagli:** specifica il percorso dei file dei prerequisiti di installazione. A seconda del valore di **PrerequisiteComp** , il programma di installazione usa questo percorso per archiviare i file scaricati oppure per individuare i file scaricati in precedenza.  

-   **Nome chiave:** AdminConsole  

    -   **Richiesto:** questa chiave è necessaria tranne quando l'impostazione **ServerRecoveryOptions** ha il valore **4**.  

    -   **Valori:** 0 o 1  

         0 = non installare  

         1 = installa  

    -   **Dettagli:** specifica se installare la console di Configuration Manager.  

-   **Nome chiave:** JoinCEIP  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = non partecipare  

         1 = partecipa  

    -   **Dettagli:** specifica se partecipare al programma Analisi utilizzo software.  

**SQLConfigOptions**  

-   **Nome chiave:** SQLServerName  

    -   **Richiesto:** sì  

    -   **Valori:** *NomeSQLServer*  

    -   **Dettagli:** specifica il nome del server o il nome dell'istanza in cluster che esegue SQL Server che ospiterà il database del sito. È necessario specificare lo stesso server in cui era ospitato il database del sito prima dell'errore.  

-   **Nome chiave:** DatabaseName  

    -   **Richiesto:** sì  

    -   **Valori:** *&lt;NomeDatabaseSito\>* o *&lt;NomeIstanza\>\&lt; NomeDatabaseSito\>*  

    -   **Dettagli:**  

         Specifica il nome del database SQL Server da creare o usare per installare il database del sito di amministrazione centrale. È necessario specificare lo stesso nome database usato prima dell'errore.  

        > [!IMPORTANT]  
        >  Se non si usa l'istanza predefinita, è necessario specificare il nome dell'istanza e il nome database del sito.  

-   **Nome chiave:** SQLSSBPort  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;*NumeroPortaSSB*>  

    -   **Dettagli:** specifica la porta di SQL Server Service Broker (SSB) usata da SQL Server. In genere, SSB è configurato per usare la porta TCP 4022. È necessario specificare la stessa porta SSB usata prima dell'errore.  

-   **Nome chiave:** SQLDataFilePath  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*PercorsoFile per il file del database con estensione MDB*>  

    -   **Dettagli:** specifica un percorso alternativo per creare il file del database con estensione MDB.  

-   **Nome chiave:** SQLLogFilePath  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*PercorsoFile per il file del database con estensione LDF*>  

    -   **Dettagli:** specifica un percorso alternativo per creare il file del database con estensione LDF.  

**CloudConnectorOptions**  

-   **Nome chiave:** CloudConnector  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = non installare  

         1 = installa  

    -   **Dettagli:** specifica se installare un punto di connessione del servizio in questo sito. Visto che il punto di connessione può essere installato solo nel sito di livello superiore di una gerarchia, questo valore deve essere 0 per un sito primario figlio.  

-   **Nome chiave:** CloudConnecorServer  

    -   **Richiesto:** obbligatorio quando CloudConnector è uguale a 1  

    -   **Valori:** &lt;*FQDN server punto di connessione del servizio*>  

    -   **Dettagli:** specifica il nome FQDN del server che ospiterà il ruolo del sistema del sito del punto di connessione del servizio.  

-   **Nome chiave:** UseProxy  

    -   **Richiesto:** obbligatorio quando CloudConnector è uguale a 1  

    -   **Valori:** 0 o 1  

         0 = non installare  

         1 = installa  

    -   **Dettagli:** specifica se il punto di connessione del servizio userà un server proxy.  

-   **Nome chiave:** Nomeproxy  

    -   **Richiesto:** obbligatorio quando CloudConnector è uguale a 1  

    -   **Valori:** &lt;*FQDN del server proxy*>  

    -   **Dettagli:** specifica il nome FQDN del server proxy che verrà usato dal ruolo del sistema del sito del punto di connessione del servizio.  

-   **Nome chiave:** ProxyPort  

    -   **Richiesto:** obbligatorio quando CloudConnector è uguale a 1  

    -   **Valori:** &lt;*NumeroPorta*>  

    -   **Dettagli:** specifica il numero della porta da usare.  

### <a name="unattended-recovery-for-a-primary-site"></a>Ripristinare automaticamente un sito primario  
 Usare i dettagli seguenti per ripristinare un sito primario usando un file script di installazione automatica.  

**Identification**  

-   **Nome chiave:** Action  

    -   **Richiesto:** sì  

    -   **Valori:** RecoverPrimarySite  

    -   **Dettagli:** ripristina un sito primario.  

**RecoveryOptions**  

-   **Nome chiave:** ServerRecoveryOptions  

    -   **Richiesto:** sì  

    -   **Valori:** 1, 2 o 4  

         1 = Ripristina il server del sito e SQL Server.  

         2 = Ripristina solo il server del sito.  

         4 = Ripristina solo SQL Server.  

    -   **Dettagli:** specifica se il programma di installazione ripristinerà il server del sito, SQL Server o entrambi. Le chiavi associate sono necessarie quando si imposta il valore seguente per l'impostazione ServerRecoveryOptions:  

        -   Valore = 1: è possibile specificare un valore per la chiave **SiteServerBackupLocation** per il ripristino del sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

        -   Valore = 2: è possibile specificare un valore per la chiave **SiteServerBackupLocation** per il ripristino del sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

        -   Valore = 4: la chiave **BackupLocation** è richiesta in caso di configurazione del valore **10** per la chiave **DatabaseRecoveryOptions** necessaria per il ripristino del database del sito dal backup.  

-   **Nome chiave:** DatabaseRecoveryOptions  

    -   **Richiesto:** questa chiave è richiesta quando l'impostazione ServerRecoveryOptions ha il valore **1** o **4**.  

    -   **Valori:** 10, 20, 40, 80  

         10 = Ripristina il database del sito dal backup.  

         20 = Usa un database del sito che è stato ripristinato manualmente usando un altro metodo.  

         40 = Crea un nuovo database per il sito. Usare questa opzione quando non è disponibile alcun backup di database del sito. I dati globali e i dati del sito vengono ripristinati tramite la replica da altri siti.  

         80 = Ignora il ripristino del database.  

    -   **Dettagli:** specifica il modo in cui il programma di installazione ripristina il database del sito in SQL Server.  

-   **Nome chiave:** SiteServerBackupLocation  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*PercorsoSetBackupServerSito*>  

    -   **Dettagli:**  

         Specifica il percorso per il set di backup del server del sito. Questa chiave è facoltativa quando l'impostazione **ServerRecoveryOptions** ha il valore **1** o **2**. Specificare un valore affinché la chiave **SiteServerBackupLocation** ripristini il sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

-   **Nome chiave:** BackupLocation  

    -   **Richiesto:** la chiave è richiesta quando si configura il valore **1** o **4** per la chiave **ServerRecoveryOptions** e il valore **10** per la chiave **DatabaseRecoveryOptions**.  

    -   **Valori:** &lt;*PercorsoSetBackupDatabaseSito*>  

    -   **Dettagli:** specifica il percorso del set di backup del database del sito.  

**Opzioni**  

-   **Nome chiave:** ProductID  

    -   **Richiesto:** sì  

    -   **Valori:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* o *Eval*  

    -   **Dettagli:** specifica il codice Product Key per l'installazione di Configuration Manager, trattini inclusi. Immettere **Eval** per installare la versione di valutazione di Configuration Manager.  

-   **Nome chiave:** SiteCode  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;*SiteCode*>  

    -   **Dettagli:** specifica i tre caratteri alfanumerici che identificano in modo univoco il sito nella gerarchia. È necessario specificare il codice del sito usato dal sito prima dell'errore. Per altre informazioni sulle restrizioni relative al codice del sito, vedere la sezione [Nomi e codici dei siti](#bkmk_codes) in questo argomento.  

-   **Nome chiave:** SiteName  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*SiteName*>  

    -   **Dettagli:** specifica il nome del sito.  

-   **Nome chiave:** SMSInstallDir  

    -   **Richiesto:** sì  

    -   **Values:** &lt;*PercorsoInstallazioneConfigMg*>  

    -   **Dettagli:** specifica la cartella di installazione per i file di programma di Configuration Manager.  

-   **Nome chiave:** SDKServer  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;*FQDN del provider SMS*>  

    -   **Dettagli:** specifica l'FQDN del server che ospiterà il provider SMS. È necessario specificare il server che ospitava il provider SMS prima dell'errore. Dopo l'installazione iniziale, è possibile configurare altri provider SMS per il sito. Per altre informazioni sul provider SMS, vedere [Plan for the SMS Provider for System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) (Pianificare il provider SMS per System Center Configuration Manager).  

-   **Nome chiave:** PrerequisiteComp  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = scarica  

         1 = già scaricato  

    -   **Dettagli:** specifica se i file dei prerequisiti di installazione sono già stati scaricati. Se ad esempio si usa un valore pari a **0**, il programma di installazione eseguirà il download dei file.  

-   **Nome chiave:** PrerequisitePath  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Dettagli:** specifica il percorso dei file dei prerequisiti di installazione. A seconda del valore di **PrerequisiteComp** , il programma di installazione usa questo percorso per archiviare i file scaricati oppure per individuare i file scaricati in precedenza.  

-   **Nome chiave:** AdminConsole  

    -   **Richiesto:** questa chiave è necessaria tranne quando l'impostazione **ServerRecoveryOptions** ha il valore **4**.  

    -   **Valori:** 0 o 1  

         0 = non installare  

         1 = installa  

    -   **Dettagli:** specifica se installare la console di Configuration Manager.  

-   **Nome chiave:** JoinCEIP  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = non partecipare  

         1 = partecipa  

    -   **Dettagli:** specifica se partecipare al programma Analisi utilizzo software.  

**SQLConfigOptions**  

-   **Nome chiave:** SQLServerName  

    -   **Richiesto:** sì  

    -   **Valori:** *NomeSQLServer*  

    -   **Dettagli:** specifica il nome del server o il nome dell'istanza in cluster che esegue SQL Server che ospiterà il database del sito. È necessario specificare lo stesso server in cui era ospitato il database del sito prima dell'errore.  

-   **Nome chiave:** DatabaseName  

    -   **Richiesto:** sì  

    -   **Valori:**  &lt;*NomeDatabaseSito*\> o                                &lt;*NomeIstanza*\>\\&lt;*NomeDatabaseSito*\>

    -   **Dettagli:**  

         Specifica il nome del database SQL Server da creare o usare per installare il database del sito di amministrazione centrale. È necessario specificare lo stesso nome database usato prima dell'errore.  

        > [!IMPORTANT]  
        >  Se non si usa l'istanza predefinita, è necessario specificare il nome dell'istanza e il nome database del sito.  

-   **Nome chiave:** SQLSSBPort  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;*NumeroPortaSSB*>  

    -   **Dettagli:** specifica la porta di SQL Server Service Broker (SSB) usata da SQL Server. In genere, SSB è configurato per usare la porta TCP 4022. È necessario specificare la stessa porta SSB usata prima dell'errore.  

-   **Nome chiave:** SQLDataFilePath  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*PercorsoFile per il file del database con estensione MDB*>  

    -   **Dettagli:** specifica un percorso alternativo per creare il file del database con estensione MDB.  

-   **Nome chiave:** SQLLogFilePath  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*PercorsoFile per il file del database con estensione LDF*>  

    -   **Dettagli:** specifica un percorso alternativo per creare il file del database con estensione LDF.  

**HierarchyExpansionOptions**  

-   **Nome chiave:** CCARSiteServer  

    -   **Richiesto:** vedere i dettagli.  

    -   **Valori:** &lt;*CodiceSitoPerSitoAmministrazioneCentrale*>  

    -   **Dettagli:** specifica il sito di amministrazione centrale a cui si collega il sito primario quando viene aggiunto alla gerarchia di Configuration Manager. Questa impostazione è necessaria se il sito primario era collegato a un sito di amministrazione centrale prima dell'errore. È necessario specificare il codice del sito usato dal sito di amministrazione centrale prima dell'errore.  

-   **Nome chiave:** CASRetryInterval  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*Intervallo*>  

    -   **Dettagli:** specifica l'intervallo (in minuti) tra i tentativi di connessione al sito di amministrazione centrale dopo l'errore di connessione. Se ad esempio si verifica un errore di connessione al sito di amministrazione centrale, il sito primario attende il numero di minuti specificato per **CASRetryInterval**e quindi tenta nuovamente di eseguire la connessione.  

-   **Nome chiave:** WaitForCASTimeout  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*Timeout*>  

    -   **Dettagli:** specifica il valore di timeout massimo (in minuti) per la connessione di un sito primario al sito di amministrazione centrale. Se ad esempio un sito primario non riesce a connettersi al sito di amministrazione centrale, tale sito primario proverà nuovamente a connettersi al sito di amministrazione centrale in base a **CASRetryInterval** finché non viene raggiunto il periodo di **WaitForCASTimeout** . È possibile specificare un valore compreso tra 0 e 100.  

**CloudConnectorOptions**  

-   **Nome chiave:** CloudConnector  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = non installare  

         1 = installa  

    -   **Dettagli:** specifica se installare un punto di connessione del servizio in questo sito. Visto che il punto di connessione può essere installato solo nel sito di livello superiore di una gerarchia, questo valore deve essere 0 per un sito primario figlio.  

-   **Nome chiave:** CloudConnecorServer  

    -   **Richiesto:** obbligatorio quando CloudConnector è uguale a 1  

    -   **Valori:** &lt;*FQDN server punto di connessione del servizio*>  

    -   **Dettagli:** specifica il nome FQDN del server che ospiterà il ruolo del sistema del sito del punto di connessione del servizio.  

-   **Nome chiave:** UseProxy  

    -   **Richiesto:** obbligatorio quando CloudConnector è uguale a 1  

    -   **Valori:** 0 o 1  

         0 = non installare  

         1 = installa  

    -   **Dettagli:** specifica se il punto di connessione del servizio userà un server proxy.  

-   **Nome chiave:** Nomeproxy  

    -   **Richiesto:** obbligatorio quando CloudConnector è uguale a 1  

    -   **Valori:** &lt;*FQDN del server proxy*>  

    -   **Dettagli:** specifica il nome FQDN del server proxy che verrà usato dal ruolo del sistema del sito del punto di connessione del servizio.  

-   **Nome chiave:** ProxyPort  

    -   **Richiesto:** obbligatorio quando CloudConnector è uguale a 1  

    -   **Valori:** &lt;*NumeroPorta*>  

    -   **Dettagli:** specifica il numero della porta da usare.  



<!--HONumber=Dec16_HO3-->



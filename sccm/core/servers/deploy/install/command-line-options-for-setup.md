---
title: Opzioni della riga di comando per la configurazione
titleSuffix: Configuration Manager
description: Creare script di automazione per installare System Center Configuration Manager dalla riga di comando.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0da167f1-52cf-4dfd-8f73-833ca3eb8478
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 434b53d24d050cc66cbb5e8bec7a681311f945b8
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65498682"
---
# <a name="command-line-options-for-setup-in-system-center-configuration-manager"></a>Opzioni della riga di comando per l'installazione in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


 Usare le informazioni seguenti per configurare gli script o installare System Center Configuration Manager dalla riga di comando.  

##  <a name="bkmk_setup"></a> Opzioni della riga di comando per l'installazione  
 **/DEINSTALL**  
 Consente di disinstallare il sito. Eseguire l'installazione dal computer del server del sito.  

 **/DONTSTARTSITECOMP**  
 Consente di installare un sito, ma impedisce l'avvio del servizio Gestione componenti del sito. Fino all'avvio del servizio Gestione componenti del sito, il sito non è attivo. Gestione componenti del sito si occupa dell'installazione e dell'avvio del servizio SMS_Executive, nonché di processi aggiuntivi nel sito. Al termine dell'installazione del sito, in seguito all'avvio del servizio Gestione componenti del sito verranno installati il servizio SMS_Executive e i processi aggiuntivi necessari per il funzionamento del sito.  

 **/HIDDEN**  
 Consente di nascondere l'interfaccia utente durante l'installazione. Usare questa opzione solo in combinazione con l'opzione **/SCRIPT**. Il file script di installazione automatica deve fornire tutte le opzioni necessarie. In caso contrario, l'installazione avrà esito negativo.  

 **/NOUSERINPUT**  
 Disabilita l'input utente durante l'installazione, ma visualizza l'installazione guidata. Usare questa opzione solo in combinazione con l'opzione **/SCRIPT**. Il file script di installazione automatica deve fornire tutte le opzioni necessarie. In caso contrario, l'installazione avrà esito negativo.  

 **/RESETSITE**  
 Consente di eseguire una reimpostazione del sito per reimpostare gli account di servizio e di database per il sito. Eseguire il programma di installazione dal **<*percorso di installazione di Configuration Manager*>\BIN\X64** nel server del sito. Per altre informazioni sulla reimpostazione del sito, vedere la sezione [Eseguire una reimpostazione del sito](../../../../core/servers/manage/modify-your-infrastructure.md#bkmk_reset) in [Modificare l'infrastruttura di System Center Configuration Manager](../../../../core/servers/manage/modify-your-infrastructure.md).  

 **/TESTDBUPGRADE <*Nome istanza*>\\<*Nome database*>**  
 Consente di eseguire un test in un backup del database del sito per verificare che il database supporti l'aggiornamento. Specificare il nome dell'istanza e il nome del database per il database del sito. Se si specifica solo il nome del database, il programma di installazione usa il nome dell'istanza predefinita.  

> [!IMPORTANT]  
>  Non eseguire questa opzione della riga di comando nel database del sito di produzione. L'esecuzione di questa opzione della riga di comando nel database del sito di produzione comporta l'aggiornamento del database del sito e potrebbe rendere inutilizzabile il sito.  

 **/UPGRADE**  
 Consente di eseguire l'aggiornamento automatico di un sito. Quando si usa **/UPGRADE**, è necessario specificare il codice Product Key, compresi i trattini (-). È anche necessario specificare il percorso dei file di prerequisito dell'installazione scaricati in precedenza.  

 Esempio: `setupwpf.exe /UPGRADE xxxxx-xxxxx-xxxxx-xxxxx-xxxxx <path to external component files>`  

 Per altre informazioni sui file di prerequisito dell'installazione, vedere la sezione [Downloader di installazione](setup-downloader.md).  

 **/SCRIPT <*percorso script installazione*>**  
 Consente di eseguire installazioni automatiche. Quando si usa l'opzione **/SCRIPT** è necessario un file di inizializzazione dell'installazione. Per altre informazioni su come eseguire l'installazione automatica, vedere [Usare una riga di comando per Installare siti tramite la riga di comando](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md).  

 **/SDKINST <*FQDN provider SMS*>**  
 Consente di installare il provider SMS nel computer specificato. Specificare il nome di dominio completo (FQDN) per il computer del provider SMS. Per altre informazioni sul provider SMS, vedere [Pianificare per il provider SMS](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

 **/SDKDEINST <*FQDN provider SMS*>**  
 Consente di disinstallare il provider SMS nel computer specificato. Specificare l'FQDN per il computer del provider SMS.  

 **/MANAGELANGS <*Percorso script lingue*>**  
 Consente di gestire le lingue installate in un sito installato precedentemente. Per usare questa opzione, eseguire il programma di installazione dal **<*percorso di installazione di Configuration Manager*>\BIN\X64** nel server del sito. Specificare il percorso per il file script delle lingue che contiene le impostazioni delle lingue. Per altre informazioni sulle opzioni relative alle lingue disponibili nel file script di configurazione della lingua, vedere la sezione [Opzioni della riga di comando per la gestione delle lingue](#bkmk_Lang).  

##  <a name="bkmk_Lang"></a> Opzioni della riga di comando per la gestione delle lingue  
 **Identification**  

-   **Nome chiave:** Action  

    -   **Richiesto:** Sì  

    -   **Valori:** ManageLanguages  

    -   **Dettagli:** Gestisce il supporto lingua di client per dispositivi mobili, client e server in un sito.  

**Opzioni**  

-   **Nome chiave:** AddServerLanguages  

    -   **Richiesto:** No  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** specifica le lingue del server che saranno disponibili per la console di Configuration Manager, i report e gli oggetti di Configuration Manager. L'inglese è disponibile per impostazione predefinita.  

-   **Nome chiave:** AddClientLanguages  

    -   **Richiesto:** No  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** Specifica le lingue che saranno disponibili per i computer client. L'inglese è disponibile per impostazione predefinita.  

-   **Nome chiave:** DeleteServerLanguages  

    -   **Richiesto:** No  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** Specifica le lingue da rimuovere e che non saranno più disponibili per la console di Configuration Manager, i report e gli oggetti di Configuration Manager. La lingua inglese è disponibile per impostazione predefinita e non può essere rimossa.  

-   **Nome chiave:** DeleteClientLanguages  

    -   **Richiesto:** No  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** Specifica le lingue da rimuovere e che non saranno più disponibili per i computer client. La lingua inglese è disponibile per impostazione predefinita e non può essere rimossa.  

-   **Nome chiave:** MobileDeviceLanguage  

    -   **Richiesto:** Sì  

    -   **Valori:** 0 o 1  

         0 = Non installare  

         1 = Installare  

    -   **Dettagli:** Specifica se le lingue del dispositivo mobile client sono installate.  

-   **Nome chiave:** PrerequisiteComp  

    -   **Richiesto:** Sì  

    -   **Valori:** 0 o 1  

         0 = Scaricare  

         1 = Già scaricato  

    -   **Dettagli:** specifica se i file dei prerequisiti di installazione sono già stati scaricati. Se ad esempio si usa un valore pari a **0**, il programma di installazione esegue il download dei file.  

-   **Nome chiave:** PrerequisitePath  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Percorso dei file dei prerequisiti di installazione*>  

    -   **Dettagli:** specifica il percorso dei file dei prerequisiti di installazione. A seconda del valore di **PrerequisiteComp**, il programma di installazione usa questo percorso per archiviare i file scaricati oppure per individuare file scaricati in precedenza.  

##  <a name="bkmk_Unattended"></a> Chiavi di file script di installazione automatica  
 Usare le sezioni seguenti per facilitare la creazione dello script per l'installazione automatica. Gli elenchi illustrano le chiavi dello script di installazione disponibili, i valori corrispondenti, se sono obbligatorie, il tipo di installazione per cui vengono usate e una breve descrizione di ogni chiave.  

### <a name="unattended-install-for-a-central-administration-site"></a>Installare automaticamente un sito di amministrazione centrale  
 Usare i dettagli seguenti per installare un sito di amministrazione centrale usando un file script di installazione automatica.  

**Identification**  

-   **Nome chiave:** Action  

    -   **Richiesto:** Sì  

    -   **Valori:** InstallCAS  

    -   **Dettagli:** consente di installare un sito di amministrazione centrale.  

-   **Nome chiave:** CDLatest  

    -   **Richiesto:** sì, solo quando si usano supporti dalla cartella CD.Latest.    

    -   **Valori:** 1. Qualsiasi valore diverso da 1 presuppone che non venga usata la cartella CD.Latest.

    -   **Dettagli:** lo script deve includere la chiave e il valore quando si esegue il programma di installazione dal supporto di una cartella CD.Latest allo scopo di installare o ripristinare un sito di amministrazione centrale o primario. Questo valore indica al programma di installazione che viene usato il formato di supporto CD.Latest.

**Opzioni**  

-   **Nome chiave:** ProductID  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *o* Eval  

    -   **Dettagli:** specifica il codice Product Key per l'installazione di Configuration Manager, trattini inclusi. Immettere **Eval** per installare la versione di valutazione di Configuration Manager.  

-   **Nome chiave:** SiteCode  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Codice del sito*>  

    -   **Dettagli:** Specifica i tre caratteri alfanumerici che identificano in modo univoco il sito nella gerarchia.  

-   **Nome chiave:** Nome sito  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Nome del sito*>  

    -   **Dettagli:** Specifica il nome del sito.  

-   **Nome chiave:** SMSInstallDir  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Percorso di installazione di Configuration Manager*>  

    -   **Dettagli:** specifica la cartella di installazione per i file di programma di Configuration Manager.  

-   **Nome chiave:** SDKServer  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*FQDN del provider SMS*>  

    -   **Dettagli:** Specifica il nome FQDN del server che ospiterà il provider SMS. Dopo l'installazione iniziale, è possibile configurare altri provider SMS per il sito.  

-   **Nome chiave:** PrerequisiteComp  

    -   **Richiesto:** Sì  

    -   **Valori:** 0 o 1  

         0 = Scaricare  

         1 = Già scaricato  

    -   **Dettagli:** specifica se i file dei prerequisiti di installazione sono già stati scaricati. Se ad esempio si usa un valore pari a **0**, il programma di installazione esegue il download dei file.  

-   **Nome chiave:** PrerequisitePath  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Percorso dei file dei prerequisiti di installazione*>  

    -   **Dettagli:** specifica il percorso dei file dei prerequisiti di installazione. A seconda del valore di **PrerequisiteComp**, il programma di installazione usa questo percorso per archiviare i file scaricati oppure per individuare file scaricati in precedenza.  

-   **Nome chiave:** AdminConsole  

    -   **Richiesto:** Sì  

    -   **Valori:** 0 o 1  

         0 = Non installare  

         1 = Installare  

    -   **Dettagli:** Specifica se installare la console di Configuration Manager.  

-   **Nome chiave:** JoinCEIP  
    > [!Note]  
    > A partire da Configuration Manager versione 1802 la funzionalità Analisi utilizzo software è stata rimossa dal prodotto.

    -   **Richiesto:** Sì  

    -   **Valori:** 0 o 1  

         0 = Non partecipare  

         1 = Partecipare  

    -   **Dettagli:** Specifica se partecipare all'Analisi utilizzo software (CEIP).  

-   **Nome chiave:** AddServerLanguages  

    -   **Richiesto:** No  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** specifica le lingue del server che saranno disponibili per la console di Configuration Manager, i report e gli oggetti di Configuration Manager. L'inglese è disponibile per impostazione predefinita.  

-   **Nome chiave:** AddClientLanguages  

    -   **Richiesto:** No  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** Specifica le lingue che saranno disponibili per i computer client. L'inglese è disponibile per impostazione predefinita.  

-   **Nome chiave:** DeleteServerLanguages  

    -   **Richiesto:** No  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** Modifica un sito dopo l'installazione. Specifica le lingue da rimuovere e che non saranno più disponibili per la console di Configuration Manager, i report e gli oggetti di Configuration Manager. La lingua inglese è disponibile per impostazione predefinita e non può essere rimossa.  

-   **Nome chiave:** DeleteClientLanguages  

    -   **Richiesto:** No  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** Modifica un sito dopo l'installazione. Specifica le lingue da rimuovere e che non saranno più disponibili per i computer client. La lingua inglese è disponibile per impostazione predefinita e non può essere rimossa.  

-   **Nome chiave:** MobileDeviceLanguage  

    -   **Richiesto:** Sì  

    -   **Valori:** 0 o 1  

         0 = Non installare  

         1 = Installare  

    -   **Dettagli:** Specifica se le lingue del dispositivo mobile client sono installate.  

**SQLConfigOptions**  

-   **Nome chiave:** SQLServerName  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Nome dell'istanza di SQL Server*>  

    -   **Dettagli:** specifica il nome del server o il nome dell'istanza in cluster che esegue SQL Server e che ospiterà il database del sito.  

-   **Nome chiave:** DatabaseName  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Nome del database del sito*> oppure <*Nome dell'istanza*>\\<*Nome del database del sito*>  

    -   **Dettagli:** specifica il nome del database SQL Server da creare o del database SQL Server da usare per l'installazione del database del sito di amministrazione centrale.  

        > [!IMPORTANT]  
        >  Se non si usa l'istanza predefinita, è necessario specificare il nome dell'istanza e il nome del database del sito.  

-   **Nome chiave:** SQLSSBPort  

    -   **Richiesto:** No  

    -   **Valori:**  <*Numero della porta SSB*>  

    -   **Dettagli:** Specifica la porta di SQL Server Service Broker (SSB) usata da SQL Server. SQL Server Service Broker è in genere configurato per l'uso della porta TCP 4022, ma è possibile configurare un'altra porta.  

-   **Nome chiave:** SQLDataFilePath  

    -   **Richiesto:** No  

    -   **Valori:**  <*Percorso del file mdb del database*>  

    -   **Dettagli:** specifica un percorso alternativo per creare il file mdb del database.  

-   **Nome chiave:** SQLLogFilePath  

    -   **Richiesto:** No  

    -   **Valori:**  <*Percorso del file ldf del database*>  

    -   **Dettagli:** specifica un percorso alternativo per creare il file ldf del database.  

**CloudConnectorOptions**  

-   **Nome chiave:** CloudConnector  

    -   **Richiesto:** Sì  

    -   **Valori:** 0 o 1  

         0 = Non installare  

         1 = Installare  

    -   **Dettagli:** specifica se installare un punto di connessione del servizio in questo sito. Dato che il punto di connessione può essere installato solo nel sito di livello superiore di una gerarchia, questo valore deve essere **0** per un sito primario figlio.  

-   **Nome chiave:** CloudConnectorServer  

    -   **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    -   **Valori:**  <*FQDN del server del punto di connessione del servizio*>  

    -   **Dettagli:** specifica il nome FQDN del server che ospiterà il ruolo del sistema del sito del punto di connessione del servizio.  

-   **Nome chiave:** UseProxy  

    -   **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    -   **Valori:** 0 o 1  

         0 = Non installare  

         1 = Installare  

    -   **Dettagli:** specifica se il punto di connessione del servizio usa un server proxy.  

-   **Nome chiave:** ProxyName  

    -   **Richiesto:** obbligatorio quando **UseProxy** è uguale a 1  

    -   **Valori:**  <*FQDN del server proxy*>  

    -   **Dettagli:** specifica il nome FQDN del server proxy usato dal punto di connessione del servizio.  

-   **Nome chiave:** ProxyPort  

    -   **Richiesto:** obbligatorio quando **UseProxy** è uguale a 1  

    -   **Valori:**  <*Numero della porta*>  

    -   **Dettagli:** specifica il numero della porta da usare per la porta del proxy.  

### <a name="unattended-install-for-a-primary-site"></a>Installare automaticamente un sito primario  
Usare i dettagli seguenti per installare un sito primario usando un file script di installazione automatica.  

**Identification**  

-   **Nome chiave:** Action  

    -   **Richiesto:** Sì  

    -   **Valori:** InstallPrimarySite  

    -   **Dettagli:** Installa un sito primario.  

-   **Nome chiave:** CDLatest  

    -   **Richiesto:** sì, solo quando si usano supporti dalla cartella CD.Latest.    

    -   **Valori:** 1. Qualsiasi valore diverso da 1 presuppone che non venga usata la cartella CD.Latest.

    -   **Dettagli:** lo script deve includere la chiave e il valore quando si esegue il programma di installazione dal supporto di una cartella CD.Latest allo scopo di installare o ripristinare un sito di amministrazione centrale o primario. Questo valore indica al programma di installazione che viene usato il formato di supporto CD.Latest.

**Opzioni**  

-   **Nome chiave:** ProductID  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *o* Eval  

    -   **Dettagli:** specifica il codice Product Key per l'installazione di Configuration Manager, trattini inclusi. Immettere **Eval** per installare la versione di valutazione di Configuration Manager.  

-   **Nome chiave:** SiteCode  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Codice del sito*>  

    -   **Dettagli:** Specifica i tre caratteri alfanumerici che identificano in modo univoco il sito nella gerarchia.  

-   **Nome chiave:** SiteName  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Nome del sito*>  

    -   **Dettagli:** Specifica il nome del sito.  

-   **Nome chiave:** SMSInstallDir  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Percorso di installazione di Configuration Manager*>

    -   **Dettagli:** specifica la cartella di installazione per i file di programma di Configuration Manager.  

-   **Nome chiave:** SDKServer  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*FQDN del provider SMS*>  

    -   **Dettagli:** Specifica il nome FQDN del server che ospiterà il provider SMS. Dopo l'installazione iniziale, è possibile configurare altri provider SMS per il sito.  

-   **Nome chiave:** PrerequisiteComp  

    -   **Richiesto:** Sì  

    -   **Valori:** 0 o 1  

         0 = Scaricare  

         1 = Già scaricato  

    -   **Dettagli:** specifica se i file dei prerequisiti di installazione sono già stati scaricati. Se ad esempio si usa un valore pari a **0**, il programma di installazione esegue il download dei file.  

-   **Nome chiave:** PrerequisitePath  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Percorso dei file dei prerequisiti di installazione*>  

    -   **Dettagli:** specifica il percorso dei file dei prerequisiti di installazione. A seconda del valore di **PrerequisiteComp**, il programma di installazione usa questo percorso per archiviare i file scaricati oppure per individuare file scaricati in precedenza.  

-   **Nome chiave:** AdminConsole  

    -   **Richiesto:** Sì  

    -   **Valori:** 0 o 1  

         0 = Non installare  

         1 = Installare  

    -   **Dettagli:** Specifica se installare la console di Configuration Manager.  

-   **Nome chiave:** JoinCEIP  
    > [!Note]  
    > A partire da Configuration Manager versione 1802 la funzionalità Analisi utilizzo software è stata rimossa dal prodotto.

    -   **Richiesto:** Sì  

    -   **Valori:** 0 o 1  

         0 = Non partecipare  

         1 = Partecipare  

    -   **Dettagli:** specifica se partecipare al programma Analisi utilizzo software.  

-   **Nome chiave:** ManagementPoint  

    -   **Richiesto:** No  

    -   **Valori:**  < *FQDN del server del sito del punto di gestione*>  

    -   **Dettagli:** Specifica il nome FQDN del server che ospiterà il ruolo del sistema del sito del punto di gestione.  

-   **Nome chiave:** ManagementPointProtocol  

    -   **Richiesto:** No  

    -   **Valori:** HTTPS *o* HTTP  

    -   **Dettagli:** Specifica il protocollo da usare per il punto di gestione.  

-   **Nome chiave:** DistributionPoint  

    -   **Richiesto:** No  

    -   **Valori:**  <*FQDN del server del sito del punto di distribuzione*>  

    -   **Dettagli:** Specifica il protocollo da usare per il punto di distribuzione.  

-   **Nome chiave:** DistributionPointProtocol  

    -   **Richiesto:** No  

    -   **Valori:** HTTPS *o* HTTP  

    -   **Dettagli:** Specifica il protocollo da usare per il punto di distribuzione.  

-   **Nome chiave:** RoleCommunicationProtocol  

    -   **Richiesto:** Sì  

    -   **Valori:** EnforceHTTPS *o* HTTPorHTTPS  

    -   **Dettagli:** specifica se configurare tutti i sistemi del sito per l'accettazione delle sole comunicazioni HTTPS dai client oppure se configurare un metodo di comunicazione per ogni ruolo del sistema del sito. Se si seleziona **EnforceHTTPS**, il computer client deve disporre di un certificato di infrastruttura a chiave pubblica (PKI) valido per l'autenticazione client.  

-   **Nome chiave:** ClientsUsePKICertificate  

    -   **Richiesto:** Sì  

    -   **Valori:** 0 o 1  

         0 = Non usare  

         1 = Usare  

    -   **Dettagli:** Specifica se i client useranno un certificato PKI client per la comunicazione con i ruoli del sistema del sito.  

-   **Nome chiave:** AddServerLanguages  

    -   **Richiesto:** No  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** specifica le lingue del server che saranno disponibili per la console di Configuration Manager, i report e gli oggetti di Configuration Manager. L'inglese è disponibile per impostazione predefinita.  

-   **Nome chiave:** AddClientLanguages  

    -   **Richiesto:** No  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** Specifica le lingue che saranno disponibili per i computer client. L'inglese è disponibile per impostazione predefinita.  

-   **Nome chiave:** DeleteServerLanguages  

    -   **Richiesto:** No  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** Modifica un sito dopo l'installazione. Specifica le lingue da rimuovere e che non saranno più disponibili per la console di Configuration Manager, i report e gli oggetti di Configuration Manager. La lingua inglese è disponibile per impostazione predefinita e non può essere rimossa.  

-   **Nome chiave:** DeleteClientLanguages  

    -   **Richiesto:** No  

    -   **Valori:** DEU, FRA, RUS, CHS, JPN, CHT, CSY, ESN, HUN, ITA, KOR, NLD, PLK, PTB, PTG, SVE, TRK o ZHH  

    -   **Dettagli:** Modifica un sito dopo l'installazione. Specifica le lingue da rimuovere e che non saranno più disponibili per i computer client. La lingua inglese è disponibile per impostazione predefinita e non può essere rimossa.  

-   **Nome chiave:** MobileDeviceLanguage  

    -   **Richiesto:** Sì  

    -   **Valori:** 0 o 1  

         0 = Non installare  

         1 = Installare  

    -   **Dettagli:** Specifica se le lingue del dispositivo mobile client sono installate.  

**SQLConfigOptions**  

-   **Nome chiave:** SQLServerName  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Nome dell'istanza di SQL Server*>  

    -   **Dettagli:** specifica il nome del server o il nome dell'istanza in cluster che esegue SQL Server e che ospiterà il database del sito.  

-   **Nome chiave:** DatabaseName  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Nome del database del sito*> oppure <*Nome dell'istanza*>\\<*Nome del database del sito*>  

    -   **Dettagli:** specifica il nome del database di SQL Server da creare o del database di SQL Server da usare per l'installazione del database del sito primario.  

        > [!IMPORTANT]  
        >  Se non si usa l'istanza predefinita, è necessario specificare il nome dell'istanza e il nome del database del sito.  

-   **Nome chiave:** SQLSSBPort  

    -   **Richiesto:** No  

    -   **Valori:**  <*Numero della porta SSB*>  

    -   **Dettagli:** specifica la porta SSB usata da SQL Server. SQL Server Service Broker è in genere configurato per l'uso della porta TCP 4022, ma è possibile configurare un'altra porta.  

-   **Nome chiave:** SQLDataFilePath  

    -   **Richiesto:** No  

    -   **Valori:**  <*Percorso del file mdb del database*>  

    -   **Dettagli:** specifica un percorso alternativo per creare il file mdb del database.  

-   **Nome chiave:** SQLLogFilePath  

    -   **Richiesto:** No  

    -   **Valori:**  <*Percorso del file ldf del database*>  

    -   **Dettagli:** specifica un percorso alternativo per creare il file ldf del database.  

**HierarchyExpansionOption**  

-   **Nome chiave:** CCARSiteServer  

    -   **Richiesto:** No  

    -   **Valori:**  <*FQDN del sito di amministrazione centrale*>  

    -   **Dettagli:** specifica il sito di amministrazione centrale a cui si collega il sito primario quando viene aggiunto alla gerarchia di Configuration Manager. Durante l'installazione, specificare il sito di amministrazione centrale.  

-   **Nome chiave:** CASRetryInterval  

    -   **Richiesto:** No  

    -   **Valori:**  <*Intervallo*>  

    -   **Dettagli:** Specifica l'intervallo (in minuti) tra i tentativi di connessione al sito di amministrazione centrale dopo l'errore di connessione. Se ad esempio si verifica un errore di connessione al sito di amministrazione centrale, il sito primario attende il numero di minuti specificato dall'utente per il valore **CASRetryInterval** e quindi tenta nuovamente di eseguire la connessione.  

-   **Nome chiave:** WaitForCASTimeout  

    -   **Richiesto:** No  

    -   **Valori:**  <*Timeout*>  

         Un valore tra **0** e **100**  

    -   **Dettagli:** Specifica il valore di timeout massimo (in minuti) per la connessione di un sito primario al sito di amministrazione centrale. Se ad esempio un sito primario non riesce a connettersi al sito di amministrazione centrale, tale sito primario proverà nuovamente a connettersi al sito di amministrazione centrale in base al valore **CASRetryInterval** finché non viene raggiunto il periodo di **WaitForCASTimeout**. È possibile specificare un valore compreso tra **0** e **100**.  

**CloudConnectorOptions**  

-   **Nome chiave:** CloudConnector  

    -   **Richiesto:** Sì  

    -   **Valori:** 0 o 1  

         0 = Non installare  

         1 = Installare  

    -   **Dettagli:** specifica se installare un punto di connessione del servizio in questo sito. Dato che il punto di connessione può essere installato solo nel sito di livello superiore di una gerarchia, questo valore deve essere **0** per un sito primario figlio.  

-   **Nome chiave:** CloudConnectorServer  

    -   **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    -   **Valori:**  <*FQDN del server del punto di connessione del servizio*\>  

    -   **Dettagli:** specifica il nome FQDN del server che ospiterà il ruolo del sistema del sito del punto di connessione del servizio.  

-   **Nome chiave:** UseProxy  

    -   **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    -   **Valori:** 0 o 1  

         0 = Non installare  

         1 = Installare  

    -   **Dettagli:** specifica se il punto di connessione del servizio usa un server proxy.  

-   **Nome chiave:** ProxyName  

    -   **Richiesto:** obbligatorio quando **UseProxy** è uguale a 1  

    -   **Valori:**  <*FQDN del server proxy*>  

    -   **Dettagli:** specifica il nome FQDN del server proxy usato dal punto di connessione del servizio.  

-   **Nome chiave:** ProxyPort  

    -   **Richiesto:** obbligatorio quando **UseProxy** è uguale a 1  

    -   **Valori:**  <*Numero della porta*>  

    -   **Dettagli:** specifica il numero della porta da usare per la porta del proxy.  

### <a name="unattended-recovery-for-a-central-administration-site"></a>Ripristinare automaticamente un sito di amministrazione centrale  
 Usare i dettagli seguenti per ripristinare un sito di amministrazione centrale usando un file script di installazione automatica.  

**Identification**  

-   **Nome chiave:** Action  

    -   **Richiesto:** Sì  

    -   **Valori:** RecoverCCAR  

    -   **Dettagli:** consente di ripristinare un sito di amministrazione centrale.  

-   **Nome chiave:** CDLatest  

    -   **Richiesto:** sì, solo quando si usano supporti dalla cartella CD.Latest.    

    -   **Valori:** 1. Qualsiasi valore diverso da 1 presuppone che non venga usata la cartella CD.Latest.

    -   **Dettagli:** lo script deve includere la chiave e il valore quando si esegue il programma di installazione dal supporto di una cartella CD.Latest allo scopo di installare o ripristinare un sito di amministrazione centrale o primario. Questo valore indica al programma di installazione che viene usato il formato di supporto CD.Latest.

**RecoveryOptions**  

-   **Nome chiave:** ServerRecoveryOptions  

    -   **Richiesto:** Sì  

    -   **Valori:** 1, 2 o 4  

         1 = Ripristina il server del sito e SQL Server.  

         2 = Ripristina solo il server del sito.  

         4 = Ripristina solo SQL Server.  

    -   **Dettagli:** specifica se il programma di installazione ripristina il server del sito, SQL Server o entrambi. Le chiavi associate sono necessarie quando si imposta il valore seguente per l'impostazione **ServerRecoveryOptions**:  

        -   Valore = 1: È possibile specificare un valore per la chiave **SiteServerBackupLocation** per il ripristino del sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

        -   Valore = 2: È possibile specificare un valore per la chiave **SiteServerBackupLocation** per il ripristino del sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

        -   Valore = 4: La chiave **BackupLocation** è richiesta in caso di configurazione del valore **10** per la chiave **DatabaseRecoveryOptions** necessaria per il ripristino del database del sito dal backup.  

-   **Nome chiave:** DatabaseRecoveryOptions  

    -   **Richiesto:** Questa chiave è richiesta quando l'impostazione **ServerRecoveryOptions** ha il valore **1** o **4**.  

    -   **Valori:** 10, 20, 40 o 80  

         10 = Ripristina il database del sito dal backup.  

         20 = Usa un database del sito che è stato ripristinato manualmente usando un altro metodo.  

         40 = Crea un nuovo database per il sito. Usare questa opzione quando non è disponibile alcun backup di database del sito. I dati globali e i dati del sito vengono ripristinati tramite la replica da altri siti.  

         80 = Ignora il ripristino del database.  

    -   **Dettagli:** specifica le modalità secondo cui il programma di installazione ripristinerà il database del sito in SQL Server.  

-   **Nome chiave:** ReferenceSite  

    -   **Richiesto:** Questa chiave è richiesta quando l'impostazione **DatabaseRecoveryOptions** ha il valore **40**.  

    -   **Valori:**  <*FQDN del sito di riferimento*>  

    -   **Dettagli:** Specifica il sito primario di riferimento usato dal sito di amministrazione centrale per il ripristino dei dati globali se il backup del database è antecedente al periodo di memorizzazione del rilevamento delle modifiche o se il sito viene ripristinato senza backup.  

         Se non viene specificato un sito di riferimento e il backup è antecedente al periodo di memorizzazione del rilevamento delle modifiche, tutti i siti primari vengono reinizializzati con i dati ripristinati dal sito di amministrazione centrale.  

         Se non viene specificato un sito di riferimento e il backup rientra nel periodo di memorizzazione del rilevamento delle modifiche, solo le modifiche apportate dal momento del backup verranno replicate dai siti primari. In caso di modifiche in conflitto provenienti da diversi siti primari, il sito di amministrazione centrale usa la prima modifica ricevuta.  

-   **Nome chiave:** SiteServerBackupLocation  

    -   **Richiesto:** No  

    -   **Valori:**  <*Percorso del set di backup del server del sito*>  

    -   **Dettagli:** Specifica il percorso per il set di backup del server del sito. Questa chiave è facoltativa quando l'impostazione **ServerRecoveryOptions** ha il valore **1** o **2**. Specificare un valore affinché la chiave **SiteServerBackupLocation** ripristini il sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

-   **Nome chiave:** BackupLocation  

    -   **Richiesto:** questa chiave è richiesta quando si configura il valore **1** o **4** per la chiave **ServerRecoveryOptions** e si configura il valore **10** per la chiave **DatabaseRecoveryOptions**.  

    -   **Valori:**  <*Percorso del set di backup del database del sito*>  

    -   **Dettagli:** Specifica il percorso del set di backup del database del sito.  

**Opzioni**  

-   **Nome chiave:** ProductID  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*xxxxx-xxxxx-xxxxx-xxxxx-xxxxx*> *o* Eval  

    -   **Dettagli:** specifica il codice Product Key per l'installazione di Configuration Manager, trattini inclusi. Immettere **Eval** per installare la versione di valutazione di Configuration Manager.  

-   **Nome chiave:** SiteCode  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Codice del sito*>  

    -   **Dettagli:** Specifica i tre caratteri alfanumerici che identificano in modo univoco il sito nella gerarchia. Specificare il codice del sito usato dal sito prima dell'errore.

-   **Nome chiave:** SiteName  

    -   **Richiesto:** No  

    -   **Valori:**  <*Nome del sito*>  

    -   **Dettagli:** Specifica il nome del sito.  

-   **Nome chiave:** SMSInstallDir  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Percorso di installazione di Configuration Manager*>  

    -   **Dettagli:** specifica la cartella di installazione per i file di programma di Configuration Manager.  

-   **Nome chiave:** SDKServer  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*FQDN del provider SMS*>  

    -   **Dettagli:** specifica l'FQDN del server che ospita il provider SMS. Specificare il server che ospitava il provider SMS prima dell'errore.  

         Dopo l'installazione iniziale, è possibile configurare altri provider SMS per il sito. Per altre informazioni sul provider SMS, vedere [Plan for the SMS Provider for System Center Configuration Manager](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) (Pianificare il provider SMS per System Center Configuration Manager).  

-   **Nome chiave:** PrerequisiteComp  

    -   **Richiesto:** Sì  

    -   **Valori:** 0 o 1  

         0 = Scaricare  

         1 = Già scaricato  

    -   **Dettagli:** specifica se i file dei prerequisiti di installazione sono già stati scaricati. Se ad esempio si usa un valore pari a **0**, il programma di installazione esegue il download dei file.  

-   **Nome chiave:** PrerequisitePath  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Percorso dei file dei prerequisiti di installazione*>  

    -   **Dettagli:** specifica il percorso dei file dei prerequisiti di installazione. A seconda del valore di **PrerequisiteComp**, il programma di installazione usa questo percorso per archiviare i file scaricati oppure per individuare file scaricati in precedenza.  

-   **Nome chiave:** AdminConsole  

    -   **Richiesto:** Questa chiave è necessaria tranne quando l'impostazione **ServerRecoveryOptions** ha valore **4**.  

    -   **Valori:** 0 o 1  

         0 = Non installare  

         1 = Installare  

    -   **Dettagli:** Specifica se installare la console di Configuration Manager.  

-   **Nome chiave:** JoinCEIP  
    > [!Note]  
    > A partire da Configuration Manager versione 1802 la funzionalità Analisi utilizzo software è stata rimossa dal prodotto.

    -   **Richiesto:** Sì  

    -   **Valori:** 0 o 1  

         0 = Non partecipare  

         1 = Partecipare  

    -   **Dettagli:** specifica se partecipare al programma Analisi utilizzo software.  

**SQLConfigOptions**  

-   **Nome chiave:** SQLServerName  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Nome dell'istanza di SQL Server*>  

    -   **Dettagli:** specifica il nome del server o il nome dell'istanza in cluster che esegue SQL Server e che ospita il database del sito. Specificare lo stesso server in cui era ospitato il database del sito prima dell'errore.  

-   **Nome chiave:** DatabaseName  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Nome del database del sito*> oppure <*Nome dell'istanza*>\\<*Nome del database del sito*>  

    -   **Dettagli:** Specifica il nome del database di SQL Server da creare o del database di SQL Server da usare per l'installazione del database del sito di amministrazione centrale. Specificare lo stesso nome database usato prima dell'errore.  

        > [!IMPORTANT]  
        >  Se non si usa l'istanza predefinita, è necessario specificare il nome dell'istanza e il nome del database del sito.  

-   **Nome chiave:** SQLSSBPort  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Numero della porta SSB*>  

    -   **Dettagli:** specifica la porta SSB usata da SQL Server. SSB è in genere configurato per usare la porta TCP 4022. Specificare la stessa porta SSB usata prima dell'errore.  

-   **Nome chiave:** SQLDataFilePath  

    -   **Richiesto:** No  

    -   **Valori:**  <*Percorso del file mdb del database*>  

    -   **Dettagli:** specifica un percorso alternativo per creare il file mdb del database.  

-   **Nome chiave:** SQLLogFilePath  

    -   **Richiesto:** No  

    -   **Valori:**  <*Percorso del file ldf del database*>  

    -   **Dettagli:** specifica un percorso alternativo per creare il file ldf del database.  

**CloudConnectorOptions**  

-   **Nome chiave:** CloudConnector  

    -   **Richiesto:** Sì  

    -   **Valori:** 0 o 1  

         0 = Non installare  

         1 = Installare  

    -   **Dettagli:** specifica se installare un punto di connessione del servizio in questo sito. Dato che il punto di connessione può essere installato solo nel sito di livello superiore di una gerarchia, questo valore deve essere **0** per un sito primario figlio.  

-   **Nome chiave:** CloudConnectorServer  

    -   **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    -   **Valori:**  <*FQDN del server del punto di connessione del servizio*>  

    -   **Dettagli:** specifica il nome FQDN del server che ospiterà il ruolo del sistema del sito del punto di connessione del servizio.  

-   **Nome chiave:** UseProxy  

    -   **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    -   **Valori:** 0 o 1  

         0 = Non installare  

         1 = Installare  

    -   **Dettagli:** specifica se il punto di connessione del servizio usa un server proxy.  

-   **Nome chiave:** ProxyName  

    -   **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    -   **Valori:**  <*FQDN del server proxy*>  

    -   **Dettagli:** specifica il nome FQDN del server proxy usato dal punto di connessione del servizio.  

-   **Nome chiave:** ProxyPort  

    -   **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    -   **Valori:**  <*Numero della porta*>  

    -   **Dettagli:** specifica il numero della porta da usare per la porta del proxy.  

### <a name="unattended-recovery-for-a-primary-site"></a>Ripristinare automaticamente un sito primario  
 Usare i dettagli seguenti per recuperare un sito primario usando un file script di installazione automatica.  

**Identification**  

-   **Nome chiave:** Action  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*RecoverPrimarySite*>  

    -   **Dettagli:** Ripristina un sito primario.  

-   **Nome chiave:** CDLatest  

    -   **Richiesto:** sì, solo quando si usano supporti dalla cartella CD.Latest.    

    -   **Valori:** 1. Qualsiasi valore diverso da 1 presuppone che non venga usata la cartella CD.Latest.

    -   **Dettagli:** lo script deve includere la chiave e il valore quando si esegue il programma di installazione dal supporto di una cartella CD.Latest allo scopo di installare o ripristinare un sito di amministrazione centrale o primario. Questo valore indica al programma di installazione che viene usato il formato di supporto CD.Latest.    

**RecoveryOptions**  

-   **Nome chiave:** ServerRecoveryOptions  

    -   **Richiesto:** Sì  

    -   **Valori:** 1, 2 o 4  

         1 = Ripristina il server del sito e SQL Server.  

         2 = Ripristina solo il server del sito.  

         4 = Ripristina solo SQL Server.  

    -   **Dettagli:** specifica se il programma di installazione ripristina il server del sito, SQL Server o entrambi. Le chiavi associate sono necessarie quando si imposta il valore seguente per l'impostazione **ServerRecoveryOptions**:  

        -   Valore = 1: È possibile specificare un valore per la chiave **SiteServerBackupLocation** per il ripristino del sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

        -   Valore = 2: È possibile specificare un valore per la chiave **SiteServerBackupLocation** per il ripristino del sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

        -   Valore = 4: La chiave **BackupLocation** è richiesta in caso di configurazione del valore **10** per la chiave **DatabaseRecoveryOptions** necessaria per il ripristino del database del sito dal backup.  

-   **Nome chiave:** DatabaseRecoveryOptions  

    -   **Richiesto:** Questa chiave è richiesta quando l'impostazione **ServerRecoveryOptions** ha il valore **1** o **4**.  

    -   **Valori:** 10, 20, 40 o 80  

         10 = Ripristina il database del sito dal backup.  

         20 = Usa un database del sito che è stato ripristinato manualmente usando un altro metodo.  

         40 = Crea un nuovo database per il sito. Usare questa opzione quando non è disponibile alcun backup di database del sito. I dati globali e i dati del sito vengono ripristinati tramite la replica da altri siti.  

         80 = Ignora il ripristino del database.  

    -   **Dettagli:** specifica le modalità secondo cui il programma di installazione ripristinerà il database del sito in SQL Server.  

-   **Nome chiave:** SiteServerBackupLocation  

    -   **Richiesto:** No  

    -   **Valori:**  <*Percorso del set di backup del server del sito*>  

    -   **Dettagli:**  

         Specifica il percorso per il set di backup del server del sito. Questa chiave è facoltativa quando l'impostazione **ServerRecoveryOptions** ha il valore **1** o **2**. Specificare un valore affinché la chiave **SiteServerBackupLocation** ripristini il sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

-   **Nome chiave:** BackupLocation  

    -   **Richiesto:** la chiave è richiesta quando si configura il valore **1** o **4** per la chiave **ServerRecoveryOptions** e il valore **10** per la chiave **DatabaseRecoveryOptions**.  

    -   **Valori:**  <*Percorso del set di backup del database del sito*>  

    -   **Dettagli:** Specifica il percorso del set di backup del database del sito.  

**Opzioni**  

-   **Nome chiave:** ProductID  

    -   **Richiesto:** Sì  

    -   **Valori:** *xxxxx-xxxxx-xxxxx-xxxxx-xxxxx* o *Eval*  

    -   **Dettagli:** specifica il codice Product Key per l'installazione di Configuration Manager, trattini inclusi. Immettere **Eval** per installare la versione di valutazione di Configuration Manager.  

-   **Nome chiave:** SiteCode  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Codice del sito*>  

    -   **Dettagli:** Specifica i tre caratteri alfanumerici che identificano in modo univoco il sito nella gerarchia. Specificare il codice del sito usato dal sito prima dell'errore.

-   **Nome chiave:** SiteName  

    -   **Richiesto:** No  

    -   **Valori:**  <*Nome del sito*>  

    -   **Dettagli:** Specifica il nome del sito.  

-   **Nome chiave:** SMSInstallDir  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Percorso di installazione di Configuration Manager*>  

    -   **Dettagli:** specifica la cartella di installazione per i file di programma di Configuration Manager.  

-   **Nome chiave:** SDKServer  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*FQDN del provider SMS*>  

    -   **Dettagli:** specifica l'FQDN del server che ospita il provider SMS. Specificare il server che ospitava il provider SMS prima dell'errore. Dopo l'installazione iniziale, configurare altri provider SMS per il sito. Per altre informazioni sul provider SMS, vedere [Pianificare per il provider SMS](../../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).  

-   **Nome chiave:** PrerequisiteComp  

    -   **Richiesto:** Sì  

    -   **Valori:** 0 o 1  

         0 = Scaricare  

         1 = Già scaricato  

    -   **Dettagli:** specifica se i file dei prerequisiti di installazione sono già stati scaricati. Se ad esempio si usa un valore pari a **0**, il programma di installazione esegue il download dei file.  

-   **Nome chiave:** PrerequisitePath  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Percorso dei file dei prerequisiti di installazione*>  

    -   **Dettagli:** specifica il percorso dei file dei prerequisiti di installazione. A seconda del valore di **PrerequisiteComp**, il programma di installazione usa questo percorso per archiviare i file scaricati oppure per individuare file scaricati in precedenza.  

-   **Nome chiave:** AdminConsole  

    -   **Richiesto:** Questa chiave è necessaria tranne quando l'impostazione **ServerRecoveryOptions** ha valore **4**.  

    -   **Valori:** 0 o 1  

         0 = Non installare  

         1 = Installare  

    -   **Dettagli:** Specifica se installare la console di Configuration Manager.  

-   **Nome chiave:** JoinCEIP  
    > [!Note]  
    > A partire da Configuration Manager versione 1802 la funzionalità Analisi utilizzo software è stata rimossa dal prodotto.

    -   **Richiesto:** Sì  

    -   **Valori:** 0 o 1  

         0 = Non partecipare  

         1 = Partecipare  

    -   **Dettagli:** specifica se partecipare al programma Analisi utilizzo software.  

**SQLConfigOptions**  

-   **Nome chiave:** SQLServerName  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Nome dell'istanza di SQL Server*>  

    -   **Dettagli:** specifica il nome del server o il nome dell'istanza in cluster che esegue SQL Server e che ospita il database del sito. Specificare lo stesso server in cui era ospitato il database del sito prima dell'errore.  

-   **Nome chiave:** DatabaseName  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Nome del database del sito*> oppure <*Nome dell'istanza*>\\<*Nome del database del sito*>

    -   **Dettagli:**  

         Specifica il nome del database di SQL Server da creare o del database di SQL Server da usare per l'installazione del database del sito di amministrazione centrale. Specificare lo stesso nome database usato prima dell'errore.  

        > [!IMPORTANT]  
        >  Se non si usa l'istanza predefinita, è necessario specificare il nome dell'istanza e il nome del database del sito.  

-   **Nome chiave:** SQLSSBPort  

    -   **Richiesto:** Sì  

    -   **Valori:**  <*Numero della porta SSB*>  

    -   **Dettagli:** specifica la porta SSB usata da SQL Server. In genere, SSB è configurato per usare la porta TCP 4022. Specificare la stessa porta SSB usata prima dell'errore.  

-   **Nome chiave:** SQLDataFilePath  

    -   **Richiesto:** No  

    -   **Valori:**  <*Percorso del file mdb del database*>  

    -   **Dettagli:** specifica un percorso alternativo per creare il file mdb del database.  

-   **Nome chiave:** SQLLogFilePath  

    -   **Richiesto:** No  

    -   **Valori:**  <*Percorso del file ldf del database*>  

    -   **Dettagli:** specifica un percorso alternativo per creare il file ldf del database.  

**HierarchyExpansionOptions**  

-   **Nome chiave:** CCARSiteServer  

    -   **Richiesto:** Visualizzare i dettagli.  

    -   **Valori:**  <*Codice del sito per il sito di amministrazione centrale*>  

    -   **Dettagli:** specifica il sito di amministrazione centrale a cui si collega il sito primario quando viene aggiunto alla gerarchia di Configuration Manager. Questa impostazione è necessaria se il sito primario era collegato a un sito di amministrazione centrale prima dell'errore. Specificare il codice del sito usato dal sito di amministrazione centrale prima dell'errore.  

-   **Nome chiave:** CASRetryInterval  

    -   **Richiesto:** No  

    -   **Valori:**  <*Intervallo*>  

    -   **Dettagli:** Specifica l'intervallo (in minuti) tra i tentativi di connessione al sito di amministrazione centrale dopo l'errore di connessione. Se ad esempio si verifica un errore di connessione al sito di amministrazione centrale, il sito primario attende il numero di minuti specificato per **CASRetryInterval** e quindi tenta nuovamente di eseguire la connessione.  

-   **Nome chiave:** WaitForCASTimeout  

    -   **Richiesto:** No  

    -   **Valori:**  <*Timeout*>  

    -   **Dettagli:** Specifica il valore di timeout massimo (in minuti) per la connessione di un sito primario al sito di amministrazione centrale. Se ad esempio un sito primario non riesce a connettersi al sito di amministrazione centrale, tale sito primario proverà nuovamente a connettersi al sito di amministrazione centrale in base al valore **CASRetryInterval** finché non viene raggiunto il periodo di **WaitForCASTimeout**. È possibile specificare un valore compreso tra **0** e **100**.  

**CloudConnectorOptions**  

-   **Nome chiave:** CloudConnector  

    -   **Richiesto:** Sì  

    -   **Valori:** 0 o 1  

         0 = Non installare  

         1 = Installare  

    -   **Dettagli:** specifica se installare un punto di connessione del servizio in questo sito. Dato che il punto di connessione può essere installato solo nel sito di livello superiore di una gerarchia, questo valore deve essere **0** per un sito primario figlio.  

-   **Nome chiave:** CloudConnectorServer  

    -   **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    -   **Valori:**  <*FQDN del server del punto di connessione del servizio*>  

    -   **Dettagli:** specifica il nome FQDN del server che ospiterà il ruolo del sistema del sito del punto di connessione del servizio.  

-   **Nome chiave:** UseProxy  

    -   **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    -   **Valori:** 0 o 1  

         0 = Non installare  

         1 = Installare  

    -   **Dettagli:** specifica se il punto di connessione del servizio usa un server proxy.  

-   **Nome chiave:** ProxyName  

    -   **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    -   **Valori:**  <*FQDN del server proxy*>  

    -   **Dettagli:** specifica il nome FQDN del server proxy usato dal punto di connessione del servizio.  

-   **Nome chiave:** ProxyPort  

    -   **Richiesto:** obbligatorio quando **CloudConnector** è uguale a 1  

    -   **Valori:**  <*Numero della porta*>  

    -   **Dettagli:** specifica il numero della porta da usare per la porta del proxy.  

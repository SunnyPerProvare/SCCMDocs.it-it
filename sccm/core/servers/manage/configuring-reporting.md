---
title: Configurare la creazione di report
titleSuffix: Configuration Manager
description: Informazioni su come configurare la creazione di report nella gerarchia di Configuration Manager, incluse le informazioni su SQL Server Reporting Services.
ms.date: 08/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 55ae86a7-f0ab-4c09-b4da-89cd0e7fa0e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 82e8e5c1e1d4f8d11842a6b625b54e16baafd055
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75795934"
---
# <a name="configure-reporting-in-configuration-manager"></a>Configurare la creazione di report in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Prima di poter creare, modificare ed eseguire report nella console di Configuration Manager, è necessario completare alcune attività di configurazione. Usare questo articolo per configurare la creazione di report nella gerarchia di Configuration Manager.  

Prima di installare e configurare SQL Server Reporting Services nella gerarchia, vedere i seguenti articoli sulla creazione di report in Configuration Manager:  

- [Introduzione alla creazione di report in Configuration Manager](/sccm/core/servers/manage/introduction-to-reporting)  

- [Pianificazione della creazione di report in Configuration Manager](/sccm/core/servers/manage/planning-for-reporting)  

## <a name="BKMK_SQLReportingServices"></a> SQL Server Reporting Services

SQL Server Reporting Services è una piattaforma per la creazione di report basata su server che fornisce funzionalità di creazione di report complete per diversi tipi di origini dati. Il punto di Reporting Services in Configuration Manager comunica con SQL Server Reporting Services per:

- Copiare i report di Configuration Manager in una cartella report specifica
- Configurare le impostazioni di Reporting Services
- Configurare le impostazioni di sicurezza di Reporting Services

Quando si esegue un report, il componente Reporting Services si connette al database del sito di Configuration Manager per il recupero dei dati.  

Prima dell'installazione del punto di Reporting Services in un sito di Configuration Manager, è necessario installare e configurare SQL Server Reporting Services nel sistema del sito di destinazione. Per altre informazioni, vedere [Installare SQL Server Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/install-reporting-services).  

Utilizzare la seguente procedura per verificare che SQL Server Reporting Services sia installato ed eseguito correttamente.  

1. Passare al menu **Start** nel sistema del sito e aprire **Gestione configurazione Reporting Services**, che si trova nella sezione **Strumenti di configurazione** del gruppo **Microsoft SQL Server**.

2. Nella finestra **Connessione configurazione Reporting Services** immettere il nome del server che ospita SQL Server Reporting Services. Selezionare l'istanza di SQL Server in cui è installato SQL Reporting Services. Selezionare quindi **Connetti** per aprire Gestione configurazione Reporting Services.  

3. Nella pagina **Stato server di report** verificare che **Stato servizio di report** sia impostato su **Avviato**. Se non si trova in questo stato, selezionare **Avvia**.  

4. Nella pagina **URL servizio Web** selezionare l'URL in **URL servizio Web Servizio report**. Questa azione consente di testare la connessione alla cartella report. Il browser potrebbe richiedere le credenziali. Verificare che la pagina Web si apra correttamente.

5. Nella pagina **Database** verificare che **Modalità server di report** sia impostato su **Originale**.  

6. Nella pagina **URL Gestione report** selezionare l'URL in **Identificazione sito Gestione report**. Questa azione verifica la connessione alla directory virtuale per Gestione report. Il browser potrebbe richiedere le credenziali. Verificare che la pagina Web si apra correttamente.

    > [!NOTE]  
    > La creazione di report in Configuration Manager non richiede Gestione report di Reporting Services. È necessario solo se si vuole eseguire report nel browser o gestire i report usando Gestione report.  

7. Selezionare **Esci** per chiudere Gestione configurazione Reporting Services.  

## <a name="BKMK_ReportBuilder3"></a> Configurare la creazione di report per l'uso di Generatore report 3.0

1. Nel computer che esegue la console di Configuration Manager aprire l'editor del Registro di sistema di Windows.  

2. Selezionare **HKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/Microsoft/ConfigMgr10/AdminUI/Reporting**.  

3. Aprire la chiave **ReportBuilderApplicationManifestName** per modificare i dati del valore.  

4. Modificare **ReportBuilder_2_0_0_0.application** in **ReportBuilder_3_0_0_0.application** e quindi selezionare **OK**.  

5. Chiudere l'editor del Registro di sistema di Windows.  

## <a name="BKMK_InstallReportingServicesPoint"></a> Installare un punto di Reporting Services

Per gestire i report nel sito, installare il punto di Reporting Services. Il punto di Reporting Services:

- Copia le cartelle report e i report in SQL Server Reporting Services
- Applica i criteri di sicurezza per i report e le cartelle
- Imposta le impostazioni di configurazione in Reporting Services

### <a name="a-namebkmk_requirements--requirements-and-limitations"></a><a name="bkmk_requirements" /> Requisiti e limitazioni

Prima di poter visualizzare o gestire i report nella console di Configuration Manager, è necessario un punto di Reporting Services. Configurare questo ruolo del sistema del sito in un server con Microsoft SQL Server Reporting Services. Per altre informazioni, vedere [Prerequisiti per la creazione di report](/sccm/core/servers/manage/prerequisites-for-reporting).  

- Quando si seleziona un sito per installare il punto di Reporting Services, gli utenti che avranno accesso ai report devono risiedere nello stesso ambito di sicurezza del sito in cui viene installato il ruolo.  

- Al termine dell'installazione di un punto di Reporting Services in un sistema del sito, non modificare l'URL del server di report.

    Se ad esempio si crea il punto di Reporting Services e quindi si modifica l'URL del server di report in Reporting Services Configuration Manager, la console di Configuration Manager continuerà a usare l'URL precedente e non sarà possibile eseguire, modificare o creare report dalla console.

    Se è necessario modificare l'URL del server di report, rimuovere innanzitutto il punto di Reporting Services esistente. Modificare l'URL e quindi reinstallare il punto di Reporting Services.  

- Quando si installa un punto di Reporting Services, è necessario specificare un [account del punto di Reporting Services](/sccm/core/plan-design/hierarchy/accounts#reporting-services-point-account). Per consentire agli utenti di un dominio diverso di eseguire un report, creare un trust bidirezionale tra i domini. In caso contrario, l'esecuzione del report non riesce.

### <a name="a-namebkmk_install--install-the-reporting-services-point-on-a-site-system"></a><a name="bkmk_install" /> Installare il punto di Reporting Services in un sistema del sito  

Per altre informazioni sulla configurazione dei sistemi del sito, vedere [Installare ruoli del sistema del sito](/sccm/core/servers/deploy/configure/install-site-system-roles).  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e quindi selezionare il nodo **Server e ruoli del sistema del sito**.  

1. Aggiungere il punto di Reporting Services a un server del sistema del sito nuovo o esistente:  

    - *Nuovo sistema del sito*: nella scheda **Home** della barra multifunzione nel gruppo **Crea** selezionare **Crea server di sistema sito**. Viene visualizzata la **Creazione guidata server del sistema sito** .  

    - *Sistema del sito esistente*: selezionare il server di destinazione. Nella scheda **Home** della barra multifunzione nel gruppo **Server** selezionare **Aggiungi ruoli del sistema del sito**. Verrà visualizzata la finestra di **Aggiunta guidata ruoli del sistema del sito** .  

1. Nella scheda **Generale** specificare le impostazioni generali per il server del sistema del sito. Quando si aggiunge il punto di Reporting Services a un server esistente, verificare i valori configurati in precedenza.  

1. Nella pagina **Selezione ruolo del sistema** selezionare **Punto di Reporting Services** dall'elenco dei ruoli disponibili e quindi selezionare **Avanti**.  

1. Nella pagina **Punto di Reporting Services** configurare le seguenti impostazioni:  

    - **Nome server di database del sito**: specificare il nome del server che ospita il database del sito di Configuration Manager. In genere, la procedura guidata recupera il nome di dominio completo (FQDN) del server. Per specificare un'istanza di database, usare il formato &lt;*nome server*>\&lt;*nome istanza*>. Ad esempio, `sqlserver\named1`

    - **Nome database**: specificare il nome del database del sito di Configuration Manager. Selezionare **Verifica** per verificare che la procedura guidata abbia accesso al database del sito.  

        > [!IMPORTANT]  
        > L'account utente usato per creare il punto di Reporting Services deve avere l'accesso in **Lettura** al database del sito. Se la prova di connessione non riesce, verrà visualizzata un'icona di avviso rossa. Il testo contestuale visualizzato al passaggio del mouse sull'icona contiene i dettagli dell'errore. Correggere l'errore e quindi selezionare di nuovo **Verifica**.  

    - **Nome cartella**: specificare il nome della cartella da creare e usare per i report di Configuration Manager in Reporting Services.  

    - **Istanza server di Reporting Services**: selezionare l'istanza di SQL Server per Reporting Services. Se questa pagina non elenca alcuna istanza, verificare che SQL Server Reporting Services sia installato, configurato e avviato.  

        > [!IMPORTANT]  
        > Configuration Manager esegue una connessione nell'ambito dell'utente corrente a WMI nel sistema del sito selezionato. Usa questa connessione per recuperare l'istanza di SQL Server per Reporting Services. Se l'utente corrente non ha l'accesso in **Lettura** a WMI nel sistema del sito, la procedura guidata non riesce a recuperare le istanze di Reporting Services.  

    - **Account punto di Reporting Services**: selezionare **Imposta** e quindi selezionare un account da usare. SQL Server Reporting Services nel punto di Reporting Services usa questo account per connettersi al database del sito di Configuration Manager. Questa connessione consente di recuperare i dati per un report. Selezionare **Account esistente** per specificare un account utente di Windows precedentemente configurato come account di Configuration Manager. Selezionare **Nuovo account** per specificare un account utente di Windows non attualmente configurato per l'utilizzo. Configuration Manager concede automaticamente all'utente specificato l'accesso al database del sito.  

        L'account che esegue Reporting Services deve appartenere al gruppo di sicurezza locale del dominio **Gruppo di accesso Windows Authorization**. Deve avere anche l'autorizzazione **Lettura tokenGroupsGlobalAndUniversal** impostata su **Consenti**. Per poter eseguire correttamente i report, gli utenti di un dominio diverso da quello dell'account al punto di Reporting Services devono avere un trust bidirezionale tra i domini.

        La password e l'account utente Windows specificati vengono crittografati e archiviati nel database di Reporting Services. Reporting Services recupera i dati per i report dal database del sito utilizzando l'account e la password.  

        > [!IMPORTANT]  
        > L'account specificato deve avere l'autorizzazione **Accesso locale** nel server che ospita il database di Reporting Services.  

1. Completare la procedura guidata.

Al termine della procedura guidata, Configuration Manager crea le cartelle report in Reporting Services e copia i report nelle cartelle report specificate.  

> [!TIP]  
> Per elencare solo i sistemi del sito che ospitano il ruolo del sito del punto di Reporting Services, fare clic con il pulsante destro del mouse su **Server e ruoli del sistema del sito** e scegliere **Punto di Reporting Services**.  

### <a name="a-namebkmk_languages--languages-for-reports"></a><a name="bkmk_languages" /> Lingue per i report

<!-- SCCMDocs#1067 -->

Dopo aver creato le cartelle report e copiato i report nel server di report, Configuration Manager determina la lingua appropriata per gli oggetti.

- Creare cartelle report, copiare report

  - Creare oggetti usando le impostazioni locali del sistema operativo del server del sito

  - Se il Language Pack specifico non è disponibile, l'impostazione predefinita è Inglese (ENU)

- Visualizzare i report in un Web browser

  - Nomi di cartelle e report: le stesse impostazioni locali del server del sito
  
  - Contenuto del report: dinamico basato sulle impostazioni locali del browser

- Visualizzare i report nella Console di Configuration Manager

  - Nomi di cartelle e report: dinamici in base alle impostazioni locali della console
  
  - Contenuto del report: dinamico in base alle impostazioni locali della console

Quando si installa un punto di Reporting Services in un sito senza Language Pack, i report vengono installati in inglese. Se un Language Pack viene installato in seguito all'installazione del punto di Reporting Services, è necessario disinstallare e reinstallare il punto di Reporting Services affinché i report siano disponibili nella lingua del Language Pack appropriato.  

Per altre informazioni, vedere [Language Pack](/sccm/core/servers/deploy/install/language-packs).

### <a name="BKMK_FileInstallationAndSecurity"></a> Privilegi di protezione della cartella report e della cartella di installazione file

Configuration Manager esegue le seguenti azioni per installare il punto di Reporting Services e configurare Reporting Services:  

> [!IMPORTANT]  
> Il sito esegue queste azioni nel contesto dell'account configurato per il servizio SMS_Executive. In genere, questo account è l'account di sistema locale del server del sito.  

- Installare il ruolo del sito del punto di Reporting Services.  

- Creare l'origine dati in Reporting Services con le credenziali archiviate specificate nella procedura guidata. Questo account è rappresentato dall'account utente Windows e dalla password usati da Reporting Services per la connessione al database del sito durante l'esecuzione dei report.  

- Creare la cartella radice di Configuration Manager in Reporting Services.  

- Aggiungere i ruoli di sicurezza **Utenti report di Configuration Manager** e **Amministratori report di Configuration Manager** in Reporting Services.  

- Creare sottocartelle e quindi distribuire i report di Configuration Manager da `%ProgramFiles%\SMS_SRSRP` nel server del sito a Reporting Services.  

- Aggiungere il ruolo **Utenti report di Configuration Manager** in Reporting Services alle cartelle radice per tutti gli account utente in Configuration Manager che dispongono dei diritti di **Lettura sito**.  

- Aggiungere il ruolo **Amministratori report di Configuration Manager** in Reporting Services alle cartelle radice per tutti gli account utente in Configuration Manager che dispongono dei diritti di **Modifica sito**.  

- Recuperare il mapping tra le cartelle report e i tipi di oggetto protetti di Configuration Manager. Configuration Manager gestisce questo mapping nel database del sito.  

- Configurare i seguenti diritti per utenti amministratori di Configuration Manager in cartelle report specifiche di Reporting Services:  

  - Aggiungere utenti e assegnare il ruolo **Utenti report di Configuration Manager** alla cartella report associata per gli utenti amministratori che dispongono delle autorizzazioni **Esegui report** per l'oggetto di Configuration Manager.  

  - Aggiungere utenti e assegnare il ruolo **Amministratori report di Configuration Manager** alla cartella report associata per gli utenti amministratori che dispongono delle autorizzazioni **Modifica report** per l'oggetto di Configuration Manager.  

Configuration Manager si connette a Reporting Services e configura le autorizzazioni per gli utenti nelle cartelle radice di Configuration Manager e di Reporting Services e in cartelle report specifiche. Al termine dell'installazione iniziale del punto di Reporting Services, Configuration Manager si connette a Reporting Services ogni 10 minuti per verificare che i diritti utente configurati nelle cartelle report siano i diritti associati configurati per gli utenti di Configuration Manager. Quando vengono aggiunti utenti o vengono modificati i diritti utente nella cartella report usando Gestione report di Reporting Services, Configuration Manager sovrascrive le modifiche mediante le assegnazioni basate sui ruoli archiviate nel database del sito. Configuration Manager rimuove anche gli utenti che non dispongono dei diritti di creazione di report in Configuration Manager.  

### <a name="BKMK_SecurityRoles"></a> Ruoli di sicurezza di Reporting Services

Quando Configuration Manager installa il punto di Reporting Services, in Reporting Services vengono aggiunti i seguenti ruoli di sicurezza:  

- **Utenti report di Configuration Manager**: gli utenti assegnati a questo ruolo di sicurezza possono eseguire soltanto i report di Configuration Manager.  

- **Amministratori report di Configuration Manager**: gli utenti assegnati a questo ruolo di sicurezza possono eseguire tutte le attività relative alla creazione di report in Configuration Manager.  

## <a name="BKMK_VerifyReportingServicesPointInstallation"></a> Verificare l'installazione

Verificare l'installazione del punto di Reporting Services esaminando i messaggi di stato e le voci dei file di log specifici. Utilizzare la seguente procedura per verificare il completamento dell'installazione del punto di Reporting Services.  

> [!Note]  
> È possibile ignorare questa procedura se i report vengono visualizzati nella sottocartella **Report** del nodo **Creazione di report** nell'area di lavoro **Monitoraggio** della console di Configuration Manager.

### <a name="verify-installation-by-status-message"></a>Verificare l'installazione in base al messaggio di stato

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Stato del sistema** e selezionare il nodo **Stato componente**.  

1. Selezionare il componente **SMS_SRS_REPORTING_POINT**.  

1. Nella scheda **Home** della barra multifunzione selezionare **Mostra messaggi** nel gruppo **Componente** e quindi scegliere **Tutti**.  

1. Specificare una data e un'ora per un periodo antecedente all'installazione del punto di Reporting Services e quindi selezionare **OK**.  

1. Verificare l'ID del messaggio di stato **1015**. Questo messaggio di stato indica che l'installazione del punto di Reporting Services è stata completata correttamente.

### <a name="verify-installation-by-log-file"></a>Verificare l'installazione in base al file di log

Aprire il file **Srsrp.log** che si trova nella directory **Logs** del percorso di installazione di Configuration Manager. Cercare la stringa `Installation was successful`.

Scorrere il file di log a partire dalla data in cui è stata completata l'installazione del punto di Reporting Services. Verificare che le cartelle report siano state create, che i report siano stati distribuiti e che i criteri di protezione di ogni cartella siano stati confermati. Dopo l'ultima riga di conferme dei criteri di sicurezza, cercare la stringa `Successfully checked that the SRS web service is healthy on server`.  

## <a name="BKMK_Certificate"></a> Configurare un certificato per la creazione di report

Esistono diverse opzioni per la creazione di report in SQL Server Reporting Services. Quando i report vengono creati o modificati nella console di Configuration Manager, Configuration Manager apre Generatore report che verrà usato come ambiente di creazione. Indipendentemente dalla modalità di creazione dei report di Configuration Manager, è necessario disporre di un certificato autofirmato per eseguire l'autenticazione server nel server di database del sito.

> [!NOTE]  
> Per altre informazioni sulla creazione di report con SQL Server Reporting Services, vedere [Ambiente di creazione di Generatore report](https://docs.microsoft.com/sql/reporting-services/tools/report-builder-authoring-environment-ssrs).  

Configuration Manager installa automaticamente il certificato nel server del sito e tutti i ruoli di Provider SMS. È possibile creare o modificare i report dalla console di Configuration Manager quando viene eseguita da uno di questi server.

Quando si creano o si modificano i report da una console di Configuration Manager in un computer diverso, esportare il certificato dal server del sito. Il nome descrittivo del certificato specifico è il nome di dominio completo del server del sito nell'archivio certificati **Persone attendibili** per il computer locale. Aggiungere questo certificato all'archivio certificati **Persone attendibili** nel computer che esegue la console di Configuration Manager.  

## <a name="BKMK_ModifyReportingServicesPoint"></a> Modificare le impostazioni del punto di Reporting Services

Dopo l'installazione di questo ruolo, è possibile modificare la connessione di database del sito e le impostazioni di autenticazione nelle proprietà del punto di Reporting Services.

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e quindi selezionare il nodo **Server e ruoli del sistema del sito**.  

    > [!TIP]  
    > Per elencare solo i sistemi del sito che ospitano il punto di Reporting Services, fare clic con il pulsante destro del mouse sul nodo **Server e ruoli del sistema del sito** e scegliere **Punto di Reporting Services**.  

1. Selezionare il sistema del sito che ospita il punto di Reporting Services. Selezionare quindi i ruoli del sistema del sito del **Punto di Reporting Services** nel riquadro dei dettagli.

1. Nella scheda **Ruolo del sito** della barra multifunzione selezionare **Proprietà** nel gruppo **Proprietà**.  

1. In **Proprietà punto di Reporting Services** è possibile modificare le seguenti impostazioni:  

    - **Nome server di database del sito**

    - **Nome database**

    - **Account utente**

1. Selezionare **OK** per salvare le modifiche e chiudere le proprietà.  

Per altre informazioni su queste impostazioni, vedere le descrizioni nella sezione [Installare il punto di Reporting Services in un sistema del sito](#bkmk_install).

## <a name="a-namebkmk_upgradesql--upgrade-sql-server"></a><a name="bkmk_upgradesql" /> Aggiornare SQL Server

Per aggiornare SQL Server e SQL Server Reporting Services, rimuovere prima di tutto il punto di Reporting Services dal sito. Dopo aver aggiornato SQL Server, reinstallare il punto di Reporting Services in Configuration Manager.

Se non si segue questo processo, verranno visualizzati errori durante l'esecuzione o la modifica dei report nella console di Configuration Manager. È possibile continuare a eseguire e modificare correttamente i report in un Web browser.  

## <a name="BKMK_ConfigureReportOptions"></a> Configurare le opzioni report

È possibile selezionare il punto di Reporting Services predefinito usato per gestire i report. Il sito può avere più di un punto di Reporting Services, ma usa solo il server predefinito per gestire i report. Utilizzare la seguente procedura per configurare le opzioni report per il sito.  

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Report** e quindi selezionare il nodo **Report**.  

1. Nella scheda **Home** della barra multifunzione selezionare **Opzioni report** nel gruppo **Impostazioni**.  

1. Selezionare il server di report predefinito nell'elenco e quindi selezionare **OK**.

Se non viene visualizzato alcun server, verificare di aver installato e configurato un punto di Reporting Services nel sito. Per altre informazioni, vedere [Verificare l'installazione](#BKMK_VerifyReportingServicesPointInstallation).

Verificare che il computer esegua una versione di Generatore report di SQL Server corrispondente alla versione di SQL Server usata per il server di report. In caso contrario, verrà visualizzato un errore, il server di report predefinito non verrà salvato e non sarà possibile creare o modificare i report.<!-- SCCMDocs#791 -->

## <a name="next-steps"></a>Passaggi successivi

[Operazioni e manutenzione per la creazione di report](/sccm/core/servers/manage/operations-and-maintenance-for-reporting)

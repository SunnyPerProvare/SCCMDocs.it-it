---
title: Configurare la creazione di report | Microsoft Docs
description: Informazioni su come configurare la creazione di report nella gerarchia di Configuration Manager, incluse le informazioni su SQL Server Reporting Services.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 55ae86a7-f0ab-4c09-b4da-89cd0e7fa0e0
caps.latest.revision: 6
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: aed95333b6509b0aa7061f23969381f1ce8aff7f


---
# <a name="configuring-reporting-in-system-center-configuration-manager"></a>Configurazione della creazione di report in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima di poter creare, modificare ed eseguire report nella console di System Center Configuration Manager, è necessario eseguire una serie di attività di configurazione. Usare le sezioni seguenti di questo argomento per configurare la creazione di report nella gerarchia di Configuration Manager:  

 Prima di procedere all'installazione e alla configurazione di Reporting Services nella gerarchia, esaminare i seguenti argomenti sulla creazione di report in Configuration Manager:  

-   [Introduzione alla creazione di report in System Center Configuration Manager](../../../core/servers/manage/introduction-to-reporting.md)  

-   [Pianificazione per la creazione di report in System Center Configuration Manager](../../../core/servers/manage/planning-for-reporting.md)  

##  <a name="a-namebkmksqlreportingservicesa-sql-server-reporting-services"></a><a name="BKMK_SQLReportingServices"></a> SQL Server Reporting Services  
 SQL Server Reporting Services è una piattaforma per la creazione di report basata su server che fornisce funzionalità di creazione di report complete per una vasta gamma di origini dati. Il punto di Reporting Services in Configuration Manager comunica con SQL Server Reporting Services per la copia dei report di Configuration Manager in una cartella report specifica, per la configurazione delle impostazioni di Reporting Services e per la configurazione delle impostazioni di protezione di Reporting Services. Reporting Services si connette al database del sito di Configuration Manager per il recupero dei dati restituiti durante l'esecuzione dei report.  

 Prima dell'installazione del punto di Reporting Services in un sito di Configuration Manager, è necessario installare e configurare SQL Server Reporting Services nel sistema del sito che ospita il ruolo del sistema del sito del punto di Reporting Services. Per informazioni sull'installazione di Reporting Services, vedere la [Libreria TechNet SQL Server](http://go.microsoft.com/fwlink/p/?LinkId=266389).  

 Utilizzare la seguente procedura per verificare che SQL Server Reporting Services sia installato ed eseguito correttamente.  

#### <a name="to-verify-that-sql-server-reporting-services-is-installed-and-running"></a>Per verificare che SQL Server Reporting Services sia installato ed eseguito correttamente  

1.  Sul desktop fare clic su **Start**, **Tutti i programmi**, **Microsoft SQL Server 2008 R2**, **Strumenti di configurazione**e quindi fare clic su **Gestione configurazione Reporting Services**.  

2.  Nella finestra di dialogo **Connessione configurazione Reporting Services** specificare il nome del server che ospita SQL Server Reporting Services e, nel menu, selezionare l'istanza di SQL Server in cui è stato installato SQL Reporting Services, quindi fare clic su **Connetti**. Verrà visualizzato Gestione configurazione Reporting Services.  

3.  Nella pagina **Stato server di report** verificare che **Stato servizio di report** sia impostato su **Avviato**. In caso contrario, fare clic su **Avvia**.  

4.  Nella pagina **URL servizio Web** fare clic sull'URL in **URL servizio Web Servizio report** per testare la connessione alla cartella report. È possibile che venga visualizzata la finestra di dialogo **Protezione di Windows** e che all'utente vengano richieste le credenziali di protezione. Per impostazione predefinita, viene visualizzato l'account utente. Immettere la password e fare clic su **OK**. Verificare che la pagina Web si apra correttamente. Chiudere la finestra del browser.  

5.  Nella pagina **Database** verificare che l'impostazione **Modalità server di report** sia configurata utilizzando **Originale**.  

6.  Nella pagina **URL Gestione report** fare clic sull'URL in **Identificazione sito Gestione report** per testare la connessione alla directory virtuale per Gestione report. È possibile che venga visualizzata la finestra di dialogo **Protezione di Windows** e che all'utente vengano richieste le credenziali di protezione. Per impostazione predefinita, viene visualizzato l'account utente. Immettere la password e fare clic su **OK**. Verificare che la pagina Web si apra correttamente. Chiudere la finestra del browser.  

    > [!NOTE]  
    >  Gestione report di Reporting Services non è necessario per la creazione di report in Configuration Manager, ma è necessario per l'esecuzione di report in un browser Internet o per la gestione di report tramite Gestione report.  

7.  Fare clic su **Esci** per chiudere Configuration Manager Reporting Services.  

##  <a name="a-namebkmkreportbuilder3a-configure-reporting-to-use-report-builder-30"></a><a name="BKMK_ReportBuilder3"></a> Configurare la creazione di report per l'uso di Generatore report 3.0  

#### <a name="to-change-the-report-builder-manifest-name-to-report-builder-30"></a>Per modificare il nome del manifesto di Generatore report in Generatore report 3.0  

1.  Nel computer che esegue la console di Configuration Manager aprire l'editor del Registro di sistema di Windows.  

2.  Selezionare **HKEY_LOCAL_MACHINE/SOFTWARE/Wow6432Node/Microsoft/ConfigMgr10/AdminUI/Reporting**.  

3.  Fare doppio clic sulla chiave **ReportBuilderApplicationManifestName** per modificare i dati del valore.  

4.  Modificare **ReportBuilder_2_0_0_0.application** in **ReportBuilder_3_0_0_0.application**, quindi fare clic su **OK**.  

5.  Chiudere l'editor del Registro di sistema di Windows.  

##  <a name="a-namebkmkinstallreportingservicespointa-install-a-reporting-services-point"></a><a name="BKMK_InstallReportingServicesPoint"></a> Installare un punto di Reporting Services  
 Il punto di Reporting Services deve essere installato in un sito per gestire i report nel sito. Il punto di Reporting Services consente di copiare i report e le cartelle report in SQL Server Reporting Services, di applicare i criteri di protezione per i report e le cartelle, nonché di impostare le impostazioni di configurazione in Reporting Services. Per consentire la visualizzazione dei report nella console di Configuration Manager e la gestione dei report in Configuration Manager, è necessario configurare un punto di Reporting Services. Il punto di Reporting Services è un ruolo del sistema del sito che è necessario configurare su un server in cui Microsoft SQL Server Reporting Services è installato e in esecuzione. Per altre informazioni sui prerequisiti , vedere [Prerequisiti per la creazione di report](prerequisites-for-reporting.md).  

> [!IMPORTANT]  
>  Quando si seleziona un sito per installare il punto di Reporting Services, ricordare che gli utenti che avranno accesso ai report devono essere nello stesso ambito di protezione del sito in cui è installato il punto di Reporting Services.  

> [!IMPORTANT]  
>  Al termine dell'installazione di un punto di Reporting Services in un sistema del sito, non modificare l'URL del server di report. Se ad esempio viene creato il punto di Reporting Services e in Configuration Manager Reporting Services si modifica l'URL del server di report, la console di Configuration Manager continuerà a usare l'URL precedente e non sarà possibile eseguire, modificare o creare report dalla console. Se è necessario modificare l'URL del server di report, rimuovere il punto di Reporting Services, modificare l'URL e quindi reinstallare il punto di Reporting Services.  

 Utilizzare la seguente procedura per installare il punto di Reporting Services.  

#### <a name="to-install-the-reporting-services-point-on-a-site-system"></a>Per installare il punto di Reporting Services in un sistema del sito  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Configurazione del sito**, quindi fare clic su **Server e ruoli del sistema del sito**.  

    > [!TIP]  
    >  Per elencare solo i sistemi del sito che ospitano il ruolo del sito del punto di Reporting Services, fare clic con il pulsante destro del mouse su **Server e ruoli del sistema del sito** per selezionare **Punto di Reporting Services**.  

3.  Aggiungere il ruolo del sistema del sito del punto di Reporting Services a un server del sistema del sito nuovo o esistente utilizzando il passaggio associato:  

    > [!NOTE]  
    >  Per altre informazioni sulla configurazione dei sistemi del sito, vedere [Aggiungere ruoli del sistema del sito per System Center Configuration Manager](../deploy/configure/add-site-system-roles.md).  

    -   **Nuovo sistema del sito**: nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea server di sistema sito**. Viene visualizzata la **Creazione guidata server del sistema sito** .  

    -   **Sistema del sito esistente**: fare clic sul server in cui si vuole installare il ruolo del sistema del sito del punto di Reporting Services. Quando si seleziona un server, nel riquadro dei risultati viene visualizzato un elenco dei ruoli del sistema del sito già installati nel server.  

         Nella scheda **Home** , nel gruppo **Server** , fare clic su **Aggiungi ruoli del sistema del sito**. Verrà visualizzata la finestra di **Aggiunta guidata ruoli del sistema del sito** .  

4.  Nella scheda **Generale** specificare le impostazioni generali per il server del sistema del sito. Quando si aggiunge il punto di Reporting Services a un server del sistema del sito esistente, verificare i valori configurati in precedenza.  

5.  Nella pagina **Selezione ruolo del sistema** selezionare **Punto di Reporting Services** dall'elenco dei ruoli disponibili, quindi fare clic su **Avanti**.  

6.  Nella pagina **Punto di Reporting Services** configurare le seguenti impostazioni:  

    -   **Nome server di database del sito**: specificare il nome del server che ospita il database del sito di Configuration Manager. In genere, la procedura guidata recupera automaticamente il nome di dominio completo (FQDN) del server. Per specificare un'istanza di database, usare il formato &lt;*Nome server*>\&lt;*<Nome istanza*>.  

    -   **Nome del database**: specificare il nome del database del sito di Configuration Manager, quindi fare clic su **Verifica** per verificare che la procedura guidata abbia accesso al database del sito.  

        > [!IMPORTANT]  
        >  L'account utente che crea il punto di Reporting Services deve disporre dell'accesso in **Lettura** al database del sito. Se la prova di connessione non riesce, verrà visualizzata un'icona di avviso rossa. Spostare il cursore sull'icona per leggere i dettagli dell'errore. Correggere l'errore, quindi fare nuovamente clic su **Verifica** .  

    -   **Nome cartella**: specificare il nome della cartella creata e usata per l'hosting dei report di Configuration Manager in Reporting Services.  

    -   **Istanza server di Reporting Services**: selezionare nell'elenco l'istanza di SQL Server per Reporting Services. Se viene rilevata solo un'istanza, questa verrà elencata e selezionata per impostazione predefinita. Se non viene rilevata nessuna istanza, verificare che SQL Server Reporting Services sia installato e configurato e che il servizio SQL Server Reporting Services sia stato avviato nel sistema nel sito.  

        > [!IMPORTANT]  
        >  Configuration Manager esegue una connessione nell'ambito dell'utente corrente a Windows Management Instrumentation (WMI) nel sistema del sito selezionato per recuperare l'istanza di SQL Server per Reporting Services. Se l'utente corrente non dispone dell'accesso in **Lettura** a WMI nel sistema del sito, non è possibile recuperare le istanze di Reporting Services.  

    -   **Account punto di Reporting Services**: fare clic su **Imposta**, selezionare un account da usare quando SQL Server Reporting Services nel punto di Reporting Services si connette al database del sito di Configuration Manager per recuperare i dati visualizzati in un report. Selezionare **Account esistente** per specificare un account utente di Windows precedentemente configurato come account di Configuration Manager oppure selezionare **Nuovo account** per specificare un account utente di Windows non attualmente configurato come account di Configuration Manager. Configuration Manager concede automaticamente all'utente specificato l'accesso al database del sito. L'utente viene visualizzato nella sottocartella **Account** del nodo **Sicurezza** nell'area di lavoro **Amministrazione** con il nome account **Punto di Reporting Services di Configuration Manager** .  

         L'account che esegue Reporting Services deve appartenere al gruppo di sicurezza locale del dominio **Gruppo di accesso Windows Authorization**e disporre dell'autorizzazione **Lettura tokenGroupsGlobalAndUniversal** impostata su **Consenti**.  

         La password e l'account utente Windows specificati vengono crittografati e archiviati nel database di Reporting Services. Reporting Services recupera i dati per i report dal database del sito utilizzando l'account e la password.  

        > [!IMPORTANT]  
        >  L'account specificato deve disporre delle autorizzazioni di **Accesso locale** nel computer che ospita il database di Reporting Services.  

7.  Nella pagina **Punto di Reporting Services** fare clic su **Avanti**.  

8.  Nella pagina **Riepilogo** verificare le impostazioni, quindi fare clic su **Avanti** per installare il punto di Reporting Services.  

     Al termine della procedura guidata vengono create le cartelle report e i report di Configuration Manager vengono copiati nelle cartelle specificate.  

    > [!NOTE]  
    >  Dopo che le cartelle report sono state create e i report sono stati copiati nel server di report, Configuration Manager determina la lingua appropriata per gli oggetti. Se il Language Pack associato è installato nel sito, Configuration Manager crea gli oggetti nella stessa lingua del sistema operativo in esecuzione nel server di report del sito. Se la lingua non è disponibile, i report vengono creati e visualizzati in inglese. Quando si installa un punto di Reporting Services in un sito senza Language Pack, i report vengono installati in inglese. Se un Language Pack viene installato in seguito all'installazione del punto di Reporting Services, è necessario disinstallare e reinstallare il punto di Reporting Services affinché i report siano disponibili nella lingua del Language Pack appropriato. Per altre informazioni sui Language Pack, vedere [Language Pack in System Center Configuration Manager](../deploy/install/language-packs.md).  

###  <a name="a-namebkmkfileinstallationandsecuritya-file-installation-and-report-folder-security-rights"></a><a name="BKMK_FileInstallationAndSecurity"></a> Privilegi di protezione della cartella report e della cartella di installazione file  
 Configuration Manager esegue le seguenti azioni per installare il punto di Reporting Services e configurare Reporting Services:  

> [!IMPORTANT]  
>  Le azioni contenute nel seguente elenco vengono eseguite utilizzando le credenziali dell'account configurato per il servizio SMS_Executive, che solitamente corrisponde all'account di sistema locale del server del sito.  

-   Consente di installare il ruolo del sito del punto di Reporting Services.  

-   Consente di creare l'origine dati in Reporting Services con le credenziali archiviate specificate nella procedura guidata. Si tratta della password e dell'account utente Windows utilizzati da Reporting Services per la connessione al database del sito durante l'esecuzione dei report.  

-   Consente di creare la cartella radice di Configuration Manager in Reporting Services.  

-   Consente di aggiungere i ruoli di sicurezza **Utenti report di Configuration Manager** e **Amministratori report di Configuration Manager** in Reporting Services.  

-   Consente di creare sottocartelle e di distribuire i report di Configuration Manager da %ProgramFiles%\SMS_SRSRP a Reporting Services.  

-   Consente di aggiungere il ruolo **Utenti report di Configuration Manager** in Reporting Services alle cartelle radice per tutti gli account utente in Configuration Manager che dispongono dei diritti di **Lettura**.  

-   Consente di aggiungere il ruolo **Amministratori report di Configuration Manager** in Reporting Services alle cartelle radice per tutti gli account utente in Configuration Manager che dispongono dei diritti di **lettura**.  

-   Consente di recuperare il mapping tra le cartelle report e i tipi di oggetti protetti di Configuration Manager (gestiti nel database del sito di Configuration Manager).  

-   Consente di configurare i seguenti diritti per utenti amministratori di Configuration Manager in cartelle report specifiche di Reporting Services:  

    -   Consente di aggiungere utenti e di assegnare il ruolo **Utenti report di Configuration Manager** alla cartella report associata per gli utenti amministratori che dispongono delle autorizzazioni **Esegui report** per l'oggetto di Configuration Manager.  

    -   Consente di aggiungere utenti e di assegnare il ruolo **Amministratori report di Configuration Manager** alla cartella report associata per gli utenti amministratori che dispongono delle autorizzazioni **Modifica report** per l'oggetto di Configuration Manager.  

     Configuration Manager si connette a Reporting Services e configura le autorizzazioni per gli utenti nelle cartelle radice di Configuration Manager e di Reporting Services e in cartelle report specifiche. Al termine dell'installazione iniziale del punto di Reporting Services, Configuration Manager si connette a Reporting Services ad intervalli di 10 minuti per verificare che i diritti utente configurati nelle cartelle report siano i diritti associati configurati per gli utenti di Configuration Manager. Quando vengono aggiunti utenti o vengono modificati i diritti utente nella cartella report usando Gestione report di Reporting Services, Configuration Manager sovrascrive le modifiche mediante le assegnazioni basate sui ruoli archiviate nel database del sito. Configuration Manager rimuove anche gli utenti che non dispongono dei diritti di creazione di report in Configuration Manager.  

##  <a name="a-namebkmksecurityrolesa-reporting-services-security-roles-for-configuration-manager"></a><a name="BKMK_SecurityRoles"></a> Ruoli di sicurezza di Reporting Services per Configuration Manager  
 Quando Configuration Manager installa il punto di Reporting Services, in Reporting Services vengono aggiunti i seguenti ruoli di sicurezza:  

-   **Utenti report di Configuration Manager**: gli utenti assegnati a questo ruolo di sicurezza possono eseguire soltanto i report di Configuration Manager.  

-   **Amministratori report di Configuration Manager**: gli utenti assegnati a questo ruolo di sicurezza possono eseguire tutte le attività relative alla creazione di report in Configuration Manager.  

##  <a name="a-namebkmkverifyreportingservicespointinstallationa-verify-the-reporting-services-point-installation"></a><a name="BKMK_VerifyReportingServicesPointInstallation"></a> Verificare l'installazione del punto di Reporting Services  
 Al termine dell'aggiunta del ruolo del sito del punto di Reporting Services, è possibile verificare l'installazione esaminando i messaggi di stato specifici e le voci dei file di log. Utilizzare la seguente procedura per verificare il completamento dell'installazione del punto di Reporting Services.  

> [!WARNING]  
>  È possibile ignorare questa procedura se i report vengono visualizzati nella sottocartella **Report** del nodo **Creazione di report** nell'area di lavoro **Monitoraggio** della console di Configuration Manager.  

#### <a name="to-verify-the-reporting-services-point-installation"></a>Per verificare l'installazione del punto di Reporting Services  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** , espandere **Stato del sistema**, quindi fare clic su **Stato componente**.  

3.  Fare clic su **SMS_SRS_REPORTING_POINT** nell'elenco dei componenti.  

4.  Nella scheda **Home** , nel gruppo **Componente** , fare clic su **Mostra messaggi**, quindi selezionare **Tutti**.  

5.  Specificare una data e un'ora per un periodo antecedente all'installazione del punto di Reporting Services, quindi fare clic su **OK**.  

6.  Verificare che sia elencato il messaggio di stato ID 1015, in cui viene indicato che l'installazione del punto di Reporting Services è stata completata. In alternativa, è possibile aprire il file Srsrp.log file in &lt;*Percorso di installazione di Configuration Manager*>\Logs e individuare **Installazione completata**.  

     In Esplora risorse passare a Percorso di installazione di &lt;*Configuration Manager*>\Logs.  

7.  Aprire Srsrp.log e procedere con il file di log a partire dal completamento dell'installazione del punto di Reporting Services. Verificare che le cartelle report siano state create, che i report siano stati distribuiti e che i criteri di protezione di ogni cartella siano stati confermati. Individuare **Verifica dell'integrità del servizio Web SRS nel server completata** dopo l'ultima riga di conferme dei criteri di sicurezza.  

##  <a name="a-namebkmkcertificatea-configure-a-self-signed-certificate-for-configuration-manager-console-computers"></a><a name="BKMK_Certificate"></a> Configurare un certificato autofirmato per i computer della console di Configuration Manager  
 Esistono diverse opzioni per la creazione di report SQL Server Reporting Services. Quando i report vengono creati o modificati nella console di Configuration Manager, Configuration Manager apre Generatore report che verrà usato come ambiente di creazione. A prescindere dalla modalità di creazione dei report di Configuration Manager, è necessario disporre di un certificato autofirmato per eseguire l'autenticazione server nel server di database del sito. Configuration Manager installa automaticamente il certificato nel server del sito e nei computer con installato il provider SMS. È pertanto possibile creare o modificare i report dalla console di Configuration Manager quando viene eseguita da uno di questi computer. Tuttavia, quando i report vengono creati o modificati da una console di Configuration Manager installata in un computer diverso, è necessario esportare il certificato dal server del sito e quindi aggiungerlo all'archivio certificati **Persone attendibili** nel computer che esegue la console di Configuration Manager.  

> [!NOTE]  
>  Per ulteriori informazioni su altri ambienti di creazione report per SQL Server Reporting Services, vedere [Comparing Report Authoring Environments (Confronto tra ambienti di creazione report)](http://go.microsoft.com/fwlink/p/?LinkId=242805) nella documentazione online di SQL Server 2008.  

 Usare la procedura seguente come esempio di trasferimento di una copia del certificato autofirmato dal server del sito a un altro computer che esegue la console di Configuration Manager quando entrambi i computer eseguono Windows Server 2008 R2. Se non è possibile seguire questa procedura poiché si dispone di una versione diversa del sistema operativo, fare riferimento alla documentazione del sistema operativo per individuare la procedura equivalente.  

#### <a name="to-transfer-a-copy-of-self-signed-certificate-from-the-site-server-to-another-computer"></a>Per trasferire una copia del certificato autofirmato dal server del sito a un altro computer  

1.  Nel server del sito eseguire i seguenti passaggi per esportare il certificato autofirmato:  

    1.  Fare clic su **Start**, quindi su **Esegui**e digitare **mmc.exe**. Nella console vuota fare clic su **File**, quindi fare clic su **Aggiungi/Rimuovi snap-in**.  

    2.  Nella finestra di dialogo **Aggiungi o rimuovi snap-in** , selezionare **Certificati** dall'elenco di **Snap-in disponibili**, quindi fare clic su **Aggiungi**.  

    3.  Nella finestra di dialogo **Snap-in certificati** , selezionare **Account computer**, quindi fare clic su **Avanti**.  

    4.  Nella finestra di dialogo **Seleziona computer** verificare che l'opzione **Computer locale: (computer in cui è in esecuzione la console)** sia selezionata, quindi fare clic su **Fine**.  

    5.  Nella finestra di dialogo **Aggiungi o rimuovi snap-in** , fare clic su **OK**.  

    6.  Nella console espandere **Certificati (computer locale)**, quindi **Persone attendibili**e selezionare **Certificati**.  

    7.  Fare clic con il pulsante destro del mouse sul certificato con il nome descrittivo &lt;*FQDN del server sito*>, fare clic su **Tutte le attività**, quindi selezionare **Esporta**.  

    8.  Completare l' **Esportazione guidata certificati** usando le opzioni predefinite e salvare il certificato con l'estensione del nome file **.cer** .  

2.  Eseguire i seguenti passaggi nel computer che esegue la console di Configuration Manager per aggiungere il certificato autofirmato all'archivio certificati Persone attendibili:  

    1.  Ripetere i passaggi precedenti da 1.a a 1.e per configurare la console MMC dello snap-in dei **certificati** nel computer del punto di gestione.  

    2.  Nella console espandere **Certificati (computer locale)**, quindi **Persone attendibili**, fare clic con il pulsante destro del mouse su **Certificati**, selezionare **Tutte le attività**e infine **Importa** per avviare l' **Importazione guidata certificati**.  

    3.  Nella pagina **File da importare** selezionare il certificato salvato nel passaggio 1.h, quindi fare clic su **Avanti**.  

    4.  Nella pagina **Archivio certificati** selezionare **Mettere tutti i certificati nel seguente archivio**con l'opzione **Archivio certificati** impostata su **Persone attendibili**, quindi fare clic su **Avanti**.  

    5.  Fare clic su **fine** per chiudere la procedura guidata e completare la configurazione dei certificati del computer.  

##  <a name="a-namebkmkmodifyreportingservicespointa-modify-reporting-services-point-settings"></a><a name="BKMK_ModifyReportingServicesPoint"></a> Modificare le impostazioni del punto di Reporting Services  
 Al termine dell'installazione del punto di Reporting Services, è possibile modificare la connessione database del sito e le impostazioni di autenticazione nelle proprietà del punto di Reporting Services. Utilizzare la seguente procedura per modificare le impostazioni del punto di Reporting Services.  

#### <a name="to-modify-reporting-services-point-settings"></a>Per modificare le impostazioni del punto di Reporting Services  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Configurazione del sito**, quindi fare clic su **Server e ruoli del sistema del sito** per un elenco dei sistemi del sito.  

    > [!TIP]  
    >  Per elencare solo i sistemi del sito che ospitano il ruolo del sito del punto di Reporting Services, fare clic con il pulsante destro del mouse su **Server e ruoli del sistema del sito** per selezionare **Punto di Reporting Services**.  

3.  Selezionare il sistema del sito che ospita il punto di Reporting Services in cui si desidera modificare le impostazioni, quindi selezionare **Punto di Reporting Services** in **Ruoli sistema del sito**.  

4.  Nella scheda **Ruolo del sito** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

5.  Nella finestra di dialogo **Proprietà punto di Reporting Services** è possibile modificare le seguenti impostazioni:  

    -   **Nome server di database del sito**: specificare il nome del server che ospita il database del sito di Configuration Manager. In genere, la procedura guidata recupera automaticamente il nome di dominio completo (FQDN) del server. Per specificare un'istanza di database, usare il formato &lt;*Nome server*>\&lt;*<Nome istanza*>.  

    -   **Nome del database**: specificare il nome del database del sito di System Center 2012 Configuration Manager, quindi fare clic su **Verifica** per verificare che la procedura guidata abbia accesso al database del sito.  

        > [!IMPORTANT]  
        >  L'account utente che crea il punto di Reporting Services deve disporre dell'accesso in Lettura al database del sito. Se la prova di connessione non riesce, verrà visualizzata un'icona di avviso rossa. Spostare il cursore sull'icona per leggere i dettagli dell'errore. Correggere l'errore, quindi fare nuovamente clic su **Verifica** .  

    -   **Account utente**: fare clic su **Imposta**, selezionare un account usato quando SQL Server Reporting Services nel punto di Reporting Services si connette al database del sito di Configuration Manager per recuperare i dati visualizzati in un report. Selezionare **Account esistente** per specificare un account utente Windows che attualmente dispone dei diritti per Configuration Manager. oppure selezionare **Nuovo account** per specificare un account utente Windows che attualmente non dispone dei diritti per Configuration Manager. Configuration Manager concede automaticamente all'account utente specificato l'accesso al database del sito. L'account viene visualizzato come account **Punto SQL Server Reporting Services di Configuration Manager** nella sottocartella **Account** del nodo **Sicurezza** nell'area di lavoro **Amministrazione** .  

         La password e l'account utente Windows specificati vengono crittografati e archiviati nel database di Reporting Services. Reporting Services recupera i dati per i report dal database del sito utilizzando l'account e la password.  

        > [!IMPORTANT]  
        >  Quando il database del sito si trova in un sistema del sito remoto, l'account specificato deve disporre dell'autorizzazione **Accesso locale** per il computer.  

6.  Fare clic su **OK** per salvare le modifiche e chiudere la finestra di dialogo.  

## <a name="upgrading-sql-server"></a>Aggiornamento di SQL Server  
 Al termine dell'aggiornamento di SQL Server e di SQL Server Reporting Services usato come origine dei dati per un punto di Reporting Services, è possibile che si verifichino errori durante l'esecuzione o la modifica dei report dalla console di Configuration Manager. Per una corretta creazione dei report dalla console di Configuration Manager, è necessario rimuovere il ruolo del sistema del sito del punto di Reporting Services per il sito e reinstallarlo. Al termine dell'aggiornamento è tuttavia possibile continuare a eseguire e modificare correttamente i report da un browser Internet.  

##  <a name="a-namebkmkconfigurereportoptionsa-configure-report-options"></a><a name="BKMK_ConfigureReportOptions"></a> Configurare le opzioni report  
 Usare le opzioni dei report per un sito di Configuration Manager per selezionare il punto di Reporting Services predefinito usato per la gestione dei report. Benché sia possibile disporre di più di un punto di Reporting Services in un sito, per la gestione dei report viene utilizzato solo il server di report predefinito selezionato nelle opzioni report. Utilizzare la seguente procedura per configurare le opzioni report per il sito.  

#### <a name="to-configure-report-options"></a>Per configurare le opzioni report  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** espandere **Creazione di report**, quindi fare clic su **Report**.  

3.  Nella scheda **Home** , nel gruppo **Impostazioni** , fare clic su **Opzioni rapporti**.  

4.  Selezionare il server di report predefinito nell'elenco, quindi fare clic su **OK**. Se nell'elenco non sono presenti punti di Reporting Services, verificare di disporre di un punto di Reporting Services correttamente installato e configurato nel sito.  

## <a name="next-steps"></a>Passaggi successivi
[Operazioni e manutenzione per la creazione di report](operations-and-maintenance-for-reporting.md)



<!--HONumber=Dec16_HO3-->



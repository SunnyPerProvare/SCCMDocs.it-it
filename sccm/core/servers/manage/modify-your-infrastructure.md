---
title: Modificare l'infrastruttura
titleSuffix: Configuration Manager
description: Informazioni su come apportare modifiche o eseguire azioni che interessano l'infrastruttura di Configuration Manager distribuita.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a7975dc8-46ab-4dae-86b6-dc3e3cf3b2f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d39552749081ee211c99a6f16fb57b2a1b9961e6
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56134606"
---
# <a name="modify-your-system-center-configuration-manager-infrastructure"></a>Modificare l'infrastruttura di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Dopo aver installato uno o più siti, può essere necessario modificare le configurazioni o eseguire azioni che incidono sull'infrastruttura distribuita.  


##  <a name="BKMK_ManageSMSprovider"></a> Gestire il provider SMS  
 Il provider SMS (un file di libreria a collegamento dinamico: smsprov.dll) offre il punto di contatto amministrativo per una o più console di Configuration Manager. Quando si installano più provider SMS, è possibile fornire ridondanza per i punti di contatto per l'amministrazione del sito e della gerarchia.  

 In ogni sito di Configuration Manager è possibile eseguire nuovamente il programma di installazione per:  

- Aggiungere un'altra istanza del provider SMS (ogni istanza aggiuntiva del provider SMS deve trovarsi in un computer separato)  

- Rimuovere un'istanza del provider (per rimuovere l'ultimo provider SMS per un sito, è necessario disinstallare il sito)  

  È possibile monitorare l'installazione o la rimozione del provider SMS visualizzando **ConfigMgrSetup.log** nella cartella radice del server del sito su cui si esegue il programma di installazione.  

  Prima di modificare il provider SMS in un sito, leggere le informazioni contenute in [Plan for the SMS Provider for System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) (Pianificare per il provider SMS per System Center Configuration Manager).  

#### <a name="to-manage-the-sms-provider-configuration-for-a-site"></a>Per gestire la configurazione del provider SMS per un sito  

1. Eseguire il **programma di installazione di Configuration Manager** da **&lt;cartella di installazione del sito di Configuration Manager\>\BIN\X64\setup.exe**.  

2. Nella pagina **Riquadro attività iniziale** selezionare **Esegui una manutenzione del sito o reimposta il sito**, quindi fare clic su **Avanti**.  

3. Nella pagina **Manutenzione sito** selezionare **Modifica configurazione provider SMS**, quindi fare clic su **Avanti**.  

4. Nella pagina **Gestisci provider SMS** selezionare una delle seguenti opzioni per completare la procedura guidata:  

   -   Per aggiungere un provider SMS aggiuntivo in questo sito:  

        Selezionare **Aggiungi nuovo provider SMS**, specificare l'FQDN per un computer che ospiterà il provider SMS e che attualmente non ne ospita uno, quindi fare clic su **Avanti**.  

   -   Per rimuovere un provider SMS da un server:  

        Selezionare **Disinstalla il provider SMS specificato**, selezionare il nome del computer da cui si desidera rimuovere il provider SMS, fare clic su **Avanti**, quindi confermare l'azione.  

       > [!TIP]  
       >  Per spostare il provider SMS tra due computer, occorre installarlo sul nuovo computer e rimuoverlo dal percorso originale. Non esiste nessuna opzione dedicata per spostare il provider SMS tra computer in un unico processo.  

   Al termine dell'Installazione guidata, viene completata la configurazione del provider SMS. Nella scheda **Generale** della finestra di dialogo del sito **Proprietà** , è possibile verificare i computer su cui è installato un provider SMS per un sito.  

##  <a name="bkmk_Console"></a> Gestire la console di Configuration Manager  
 Di seguito sono riportate le attività che è possibile eseguire per gestire la console di Configuration Manager:  

-   **Modificare la lingua visualizzata nella console di Configuration Manager**: per modificare le lingue installate, vedere [Gestire la lingua della console di Configuration Manager](#BKMK_ManageConsoleLanguages) in questo argomento.  

-   **Installare console aggiuntive**: per installare altre console, vedere [Install System Center Configuration Manager consoles](/sccm/core/servers/deploy/install/install-consoles) (Installare le console di System Center Configuration Manager).  

-   **Configurare DCOM**: per configurare le autorizzazioni DCOM per abilitare la connessione delle console remote rispetto al server del sito, vedere [Configurare le autorizzazioni DCOM per le console remote di Configuration Manager](#BKMK_ConfigDCOMforRemoteConsole) in questo argomento.  

-   **Modificare le autorizzazioni per limitare le informazioni che gli utenti amministratori possono vedere nella console**: per modificare le autorizzazioni amministrative che limitano ciò che gli utenti possono fare e vedere nella console, vedere [Modificare l'ambito amministrativo di un utente amministratore](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_ModAdminUser).     

###  <a name="BKMK_ManageConsoleLanguages"></a> Gestire la lingua della console di Configuration Manager  
 Durante l'installazione del server del sito, i file di installazione della console di Configuration Manager e i Language Pack supportati per il sito vengono copiati nella sottocartella **&lt;PercorsoInstallazioneConfigMgr\>\Tools\ConsoleSetup** nel server del sito.  

-   Quando si avvia l'installazione della console di Configuration Manager da questa cartella nel server del sito, la console di Configuration Manager e i file dei Language Pack supportati vengono copiati nel computer  

-   Quando un Language Pack è disponibile per l'impostazione della lingua corrente nel computer, la console di Configuration Manager viene aperta in questa lingua  

-   Se il Language Pack associato non è disponibile per la console di Configuration Manager, la console viene aperta in inglese  

Ad esempio, considerare uno scenario in cui si installa la console di Configuration Manager da un server del sito che supporta l'inglese, il tedesco e il francese. Se si apre la console di Configuration Manager su un computer con un'impostazione lingua configurata sul francese, la console si aprirà in francese. Se si apre la console di Configuration Manager su un computer con la lingua configurata sul giapponese, la console si aprirà in inglese perché il Language Pack giapponese non è disponibile.  

 A ogni apertura della console di Configuration Manager, vengono determinate le impostazioni di lingua configurate per il computer, viene verificata la disponibilità di un Language Pack associato per la console di Configuration Manager e infine viene aperta la console usando il Language Pack appropriato. Per aprire la console di Configuration Manager in inglese indipendentemente dalle impostazioni di lingua configurate nel computer, è necessario rimuovere o rinominare manualmente i file dei Language Pack nel computer.  

 Usare le procedure seguenti per avviare la console di Configuration Manager in inglese indipendentemente dalle impostazioni locali configurate nel computer.  

##### <a name="to-install-an-english-only-version-of-the-configuration-manager-console-on-computers"></a>Per installare una versione solo in lingua inglese della console di Configuration Manager sui computer  

1.  In Esplora risorse passare a **&lt;PercorsoInstallazioneConfigMgr\>\Tools\ConsoleSetup\LanguagePack**  

2.  Rinominare i file **.msp** e **.mst** Ad esempio, è possibile modificare **&lt;nome file\>.MSP** in **&lt;nome file\>.MSP.disabled**.  

3.  Installare la console di Configuration Manager nel computer.  

    > [!IMPORTANT]  
    >  Quando vengono configurate nuove lingue per il server del sito, i file .msp e .mst vengono ricopiati nella cartella **LanguagePack** ed è necessario ripetere questa procedura per installare le nuove console di Configuration Manager solo in lingua inglese.  

##### <a name="to-temporarily-disable-a-console-language-on-an-existing-configuration-manager-console-installation"></a>Per disattivare temporaneamente una lingua della console in un'installazione della console di Configuration Manager esistente  

1.  Nel computer che esegue la console di Configuration Manager chiudere la console.  

2.  In Esplora risorse passare a &lt;*PercorsoInstallazioneConsole*>\Bin\ nel computer della console di Configuration Manager.  

3.  Rinominare la cartella della lingua appropriata per la lingua configurata nel computer. Ad esempio, se le impostazioni della lingua per il computer erano configurate per il tedesco, è possibile rinominare la cartella **de** in **de.disabled**.  

4.  Per aprire la console di Configuration Manager nella lingua configurata per il computer, rinominare la cartella con il nome originale. Ad esempio, rinominare **de.disabled** in **de**.  

##  <a name="BKMK_ConfigDCOMforRemoteConsole"></a> Configurare le autorizzazioni DCOM per le console remote di Configuration Manager  
 L'account utente su cui è in esecuzione la console di Configuration Manager richiede l'autorizzazione ad accedere al database del sito usando il provider SMS. Tuttavia, un utente amministratore che usa una console di Configuration Manager remota deve avere anche le autorizzazioni DCOM di **attivazione remota** per:  

- Il computer del server del sito  

- Ogni computer che ospita un'istanza del provider SMS  

  Il gruppo di sicurezza **SMS Admins** concede l'accesso a un computer al provider SMS e può essere usato anche per concedere le autorizzazioni DCOM necessarie. Questo gruppo è locale nel computer quando il provider SMS è in esecuzione in un server membro ed è un gruppo locale di dominio quando il provider SMS è in esecuzione in un controller di dominio.  

> [!IMPORTANT]  
>  La console di Configuration Manager usa la Strumentazione gestione Windows (WMI) per collegarsi al provider SMS, mentre la WMI usa a sua volta DCOM a livello interno. Pertanto, Configuration Manager richiede le autorizzazioni per attivare un server DCOM sul computer del provider SMS se la console di Configuration Manager è in esecuzione su un computer diverso dal computer del provider SMS. Per impostazione predefinita, l'attivazione remota viene concessa solo ai membri del gruppo Administrators incorporato. Se si concede l'autorizzazione di attivazione remota al gruppo SMS Admins, un membro di tale gruppo potrebbe tentare degli attacchi DCOM contro il computer del provider SMS. Questa configurazione aumenta anche la superficie di attacco del computer. Per limitare questo rischio, è necessario monitorare attentamente l'appartenenza al gruppo SMS Admins.  

 Usare la procedura riportata di seguito per configurare ciascun sito di amministrazione centrale, server del sito primario e ciascun computer in cui è installato il provider SMS per garantire alla console remota di Configuration Manager l'accesso per gli utenti amministratori.  

#### <a name="to-configure-dcom-permissions-for-remote-configuration-manager-console-connections"></a>Per configurare le autorizzazioni DCOM per le connessioni remote della console di Configuration Manager  

1. Aprire  **Servizi componenti** eseguendo **Dcomcnfg.exe**.  

2. In **Servizi componenti**fare clic su **Radice console** >  **Servizi componenti** > **Computer**, quindi fare clic su **Risorse del computer**. Nel menu **Azione** fare clic su **Proprietà**.  

3. Nella finestra di dialogo **Proprietà computer** , nella scheda **Protezione COM** , nella sezione **Autorizzazioni di esecuzione e attivazione** , fare clic su **Modifica limiti**.  

4. Nella finestra di dialogo **Autorizzazioni di esecuzione e attivazione** , fare clic su **Aggiungi**.  

5. Nella casella **Immettere i nomi degli oggetti da selezionare (esempi)** della finestra di dialogo **Seleziona utenti, computer, account di servizio o gruppi** digitare **SMS Admins**, quindi fare clic su **OK**.  

   > [!NOTE]  
   >  Potrebbe essere necessario modificare l'impostazione per **Da questo percorso** per individuare il gruppo SMS Admins. Questo gruppo è in locale sul computer quando il provider SMS è in esecuzione su un server membro ed è un gruppo locale di dominio quando il provider SMS è in esecuzione su un controller di dominio.  

6. Nella sezione **Autorizzazioni per SMS Admins** , per consentire l'attivazione remota selezionare la casella di controllo **Attivazione remota** .  

7. Fare clic su **OK** e ancora su **OK** , quindi chiudere **Gestione computer**. Il computer è ora configurato per consentire l'accesso alla console remota di Configuration Manager ai membri del gruppo Amministratori SMS.  

   Ripetere questa procedura in ciascun computer del provider SMS che potrebbe supportare le console remote di Configuration Manager.  

##  <a name="bkmk_dbconfig"></a> Modificare la configurazione del database del sito  
 Dopo aver installato un sito, è possibile modificarne la configurazione del database e del server di database eseguendo il programma di installazione su un server del sito di amministrazione centrale o un server del sito primario. È possibile spostare il database del sito in una nuova istanza di SQL Server sullo stesso computer o su un computer diverso sul quale è in esecuzione una versione supportata di SQL Server. Queste modifiche e quelle correlate non sono supportate per la configurazione del database nei siti secondari.  

 Per altre informazioni sui limiti del supporto, vedere [Criteri di supporto per la modifica manuale del database in un ambiente di Configuration Manager](https://support.microsoft.com/kb/3106512).  

> [!NOTE]  
>  Quando si modifica la configurazione del database di un sito, Configuration Manager riavvia o reinstalla i servizi di Configuration Manager nel server del sito e nei server del sistema del sito remoto che comunicano con il database.  

**Per modificare la configurazione del database**, è necessario eseguire il programma di installazione nel server del sito e selezionare l'opzione **Esegui una manutenzione del sito o reimposta il sito**. Selezionare quindi l'opzione **Modifica la configurazione di SQL Server** . È possibile modificare le seguenti configurazioni del database del sito:  

-   Il server basato su Windows che ospita il database.  

-   L'istanza di SQL Server in uso su un server che ospita il database SQL Server.  

-   Nome del database.  

-   Porta di SQL Server usata da Configuration Manager  

-   Porta di SQL Server Service Broker usata da Configuration Manager  

**Se si sposta il database del sito, è necessario configurare quanto segue:**  

-   **Configura accesso**: Quando si sposta il database del sito su un nuovo computer, aggiungere l'account computer del server del sito al gruppo di **amministratori locali** sul computer che esegue SQL Server. Se si utilizza un cluster SQL Server per il database del sito, è necessario aggiungere l'account computer al gruppo di **amministratori locali** di ciascun computer nodo cluster Windows Server.  

-   **Abilita integrazione con CLR**:  Quando si sposta il database in una nuova istanza di SQL Server o in un nuovo computer SQL Server, è necessario abilitare l'integrazione di Common Language Runtime (CLR). Per abilitare CLR, usare **SQL Server Management Studio** per connettersi all'istanza di SQL Server che ospita il database del sito ed eseguire la stored procedure seguente come query: **sp_configure 'clr enabled',1; reconfigure**.  
-  **Verificare che il nuovo SQL Server sia in possesso dell'accesso al percorso di backup**: quando si usa un percorso UNC per archiviare il backup del database del sito, dopo lo spostamento del database in un nuovo server, incluso lo spostamento in un gruppo di disponibilità AlwaysOn di SQL Server o in un cluster di SQL Server, verificare che l'account del computer del nuovo SQL Server abbia le autorizzazioni di **scrittura** per il percorso UNC.  


> [!IMPORTANT]  
>  Prima di spostare un database contenente una o più repliche di database per i punti di gestione, è necessario rimuovere innanzitutto le repliche di database. Dopo aver completato lo spostamento del database, è possibile riconfigurare le repliche di database. Per altre informazioni, vedere [Repliche di database per i punti di gestione per System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

##  <a name="bkmk_SPN"></a> Gestire il nome dell'entità servizio (SPN) per il server di database del sito  
È possibile scegliere l'account che esegue i servizi di SQL per il database del sito:  

-   Quando i servizi vengono eseguiti con l'account di sistema del computer, il SPN viene registrato automaticamente.  

-   Quando i servizi vengono eseguiti con un account utente locale di dominio, è necessario registrare manualmente il SPN per assicurarsi che i client SQL e altri sistemi del sito possano eseguire l'autenticazione Kerberos. Senza l'autenticazione Kerberos, la comunicazione con il database potrebbe non riuscire.  

La documentazione di SQL Server contiene informazioni su come [registrare manualmente il SPN](https://technet.microsoft.com/library/ms191153\(v=sql.120\).aspx), oltre che maggiori dettagli sulle connessioni SPN e Kerberos.  

> [!IMPORTANT]
> - Quando si crea un SPN per un server SQL in cluster, è necessario specificare il nome virtuale del cluster SQL Server come nome del computer SQL Server.  
>   -   Il comando per registrare un SPN per un'istanza denominata di SQL Server è lo stesso usato per la registrazione di un SPN per un'istanza predefinita, salvo per il numero di porta, che deve corrispondere alla porta usata dall'istanza denominata.  

È possibile registrare un SPN per l'account del servizio SQL Server del server di database del sito usando lo strumento **Setspn** . È necessario eseguire lo strumento Setspn su un computer che risiede nel dominio di SQL Server e che per l'esecuzione utilizza le credenziali dell'amministratore di dominio.  

 Utilizzare le procedure seguenti come un esempio della modalità di gestione dell'SPN per l'account servizio SQL Server che utilizza lo strumento Setspn su Windows Server 2008 R2. Per una guida specifica sullo strumento Setspn, vedere [Setspn Overview (Panoramica su Setspn)](http://go.microsoft.com/fwlink/p/?LinkId=226343)o una documentazione simile specifica del sistema operativo in uso.  

> [!NOTE]  
>  Le procedure seguenti fanno riferimento allo strumento da riga di comando di Setspn. Lo strumento da riga di comando di Setspn è incluso in caso di installazione degli strumenti di supporto di Windows Server 2003 da CD o da [Microsoft Download Center (Area download Microsoft)](http://go.microsoft.com/fwlink/p/?LinkId=100114). Per ulteriori informazioni sulla modalità di installazione degli strumenti di supporto di Windows da CD, vedere [Installare gli Strumenti di supporto di Windows](http://go.microsoft.com/fwlink/p/?LinkId=62270).  

#### <a name="to-manually-create-a-domain-user-service-principal-name-spn-for-the-sql-server-service-account"></a>Per creare manualmente il nome dell'entità di servizio (SPN) di un utente di dominio per l'account servizio SQL Server  

1.  Nel menu **Start** , fare clic su **Esegui**, quindi immettere **cmd** nella finestra di dialogo Esegui.  

2.  Nella riga di comando, passare alla directory di installazione degli strumenti di supporto di Windows Server. Per impostazione predefinita, questi strumenti si trovano nella directory **C:\Programmi\Support Tools** .  

3.  Immettere un comando valido per creare l'SPN. Per creare l'SPN, è possibile utilizzare il nome NetBIOS o il nome di dominio completo (FQDN) del computer che esegue SQL Server. Tuttavia, è necessario creare un SPN per il nome NetBIOS e il nome FQDN.  

    > [!IMPORTANT]  
    >  Quando si crea un SPN per un server SQL del cluster, è necessario specificare il nome virtuale del cluster SQL Server come nome del computer SQL Server.  

    -   Per creare un SPN per il nome NetBIOS del computer SQL Server, digitare il comando seguente: **setspn -A MSSQLSvc/&lt;nome computer SQL Server>:1433 <Dominio\Account\>:1433 &lt;Dominio\Account>**  

    -   Per creare un SPN per il nome FQDN del computer SQL Server, digitare il comando seguente: **setspn -A MSSQLSvc/&lt;FQDN SQL Server\>:1433 &lt;Dominio\Account>**  

    > [!NOTE]  
    >  Il comando per registrare un SPN per un'istanza denominata SQL Server è lo stesso utilizzato per la registrazione di un SPN per un'istanza predefinita, salvo per il numero di porta che deve corrispondere alla porta utilizzata dall'istanza denominata.  

#### <a name="to-verify-the-domain-user-spn-is-registered-correctly-by-using-the-setspn-command"></a>Per verificare che l'SPN dell'utente di dominio sia registrato correttamente tramite il comando Setspn  

1.  Nel menu **Start** , fare clic su **Esegui**, quindi immettere **cmd** nella finestra di dialogo **Esegui** .  

2.  Al prompt dei comandi immettere il comando seguente: **setspn -L &lt;dominio\Account servizio SQL>**.  

3.  Esaminare l'attributo **ServicePrincipalName** registrato per assicurarsi che sia stato creato un SPN valido per SQL Server.  

#### <a name="to-verify-the-domain-user-spn-is-registered-correctly-when-using-the-adsiedit-mmc-console"></a>Per verificare che l'SPN dell'utente di dominio sia stato registrato correttamente quando si utilizza la console MMC ADSIEdit  

1.  Nel menu **Start** , fare clic su **Esegui**, quindi immettere **adsiedit.msc** per avviare la console MMC ADSIEdit.  

2.  Se necessario, connettersi al dominio del server del sito.  

3.  Nel riquadro della console espandere il dominio del server del sito, espandere **DC=&lt;nome distinto server\>**, espandere **CN=Users**, fare clic con il pulsante destro del mouse su **CN=&lt;Utente account servizio\>** e quindi fare clic su **Proprietà**.  

4.  Nella finestra di dialogo **Proprietà CN=&lt;Utente account servizio\>**, esaminare il valore **servicePrincipalName** per verificare che sia stato creato un SPN valido e che sia stato associato al computer SQL Server corretto.  

#### <a name="to-change-the-sql-server-service-account-from-local-system-to-a-domain-user-account"></a>Per modificare l'account servizio SQL Server dal sistema locale in un account utente di dominio  

1.  Creare o selezionare un dominio o un account utente del sistema locale che si desidera utilizzare come account servizio SQL Server.  

2.  Aprire **Gestione configurazione SQL Server**.  

3.  Fare clic su **Servizi di SQL Server**, quindi fare doppio clic su **SQL Server&lt;NOME ISTANZA\>**.  

4.  Nella scheda **Accedi** , selezionare **Questo account**, quindi immettere il nome utente e la password per l'account utente di dominio creati al passaggio 1, oppure fare clic su **Sfoglia** per trovare l'account utente in Servizi di dominio Active Directory, quindi fare clic su **Applica**.  

5.  Fare clic su **Sì** nella finestra di dialogo **Conferma modifica account** per confermare la modifica dell'account servizio e riavviare il servizio SQL Server.  

6.  Fare clic su **OK** dopo aver modificato correttamente l'account servizio.  

##  <a name="bkmk_reset"></a> Eseguire una reimpostazione del sito  
 Quando viene eseguita la reimpostazione di un sito di amministrazione centrale o di un sito primario, il sito:  

-   Riapplica le autorizzazioni di file e registro di sistema predefinite di Configuration Manager  

-   Reinstalla tutti i componenti e tutti i ruoli del sistema del sito  

I siti secondari non supportano la reimpostazione del sito.  

Le reimpostazioni di siti possono essere eseguite manualmente, quando si preferisce, oppure automaticamente, dopo aver modificato la configurazione del sito.  

Ad esempio, se è stata apportata una modifica agli account usati dai componenti di Configuration Manager, è consigliabile eseguire una reimpostazione manuale del sito per assicurarsi che componenti del sito vengano aggiornati in modo da usare i nuovi dati degli account. Se si modificano le lingue del client o del server in un sito, tuttavia, Configuration Manager esegue una reimpostazione automatica del sito, necessaria perché il sito possa usare la modifica.  

> [!NOTE]  
>  Una reimpostazione del sito non consente la reimpostazione delle autorizzazioni di accesso a oggetti non Configuration Manager.  

Quando viene eseguita la reimpostazione di un sito:  

1.  Il programma di installazione interrompe e riavvia il servizio **SMS_SITE_COMPONENT_MANAGER** e i componenti thread del servizio **SMS_EXECUTIVE** .  

2.  Il programma di installazione rimuove, quindi ricrea, la cartella condivisa del sistema del sito e il componente **SMS Executive** nel computer locale e nei computer del sistema del sito remoto.  

3.  Il programma di installazione riavvia il servizio **SMS_SITE_COMPONENT_MANAGER** e quest'ultimo installa a sua volta i servizi **SMS_EXECUTIVE** e **SMS_SQL_MONITOR** .  

Inoltre, una reimpostazione del sito consente di ripristinare gli oggetti seguenti:  

-   Le chiavi del Registro di sistema **SMS** o **NAL** e qualsiasi altra sottochiave di queste chiavi.  

-   L'albero della directory di file di Configuration Manager e qualsiasi sottodirectory o file predefinito presenti nell'albero.  

**Prerequisiti per eseguire una reimpostazione del sito**  

L'account utilizzato per eseguire una reimpostazione del sito deve disporre delle seguenti autorizzazioni:  

-   L'account utilizzato per eseguire una reimpostazione del sito deve disporre delle seguenti autorizzazioni:  

    -   **Sito di amministrazione centrale**: l'account usato per eseguire una reimpostazione del sito deve essere un server del sito di amministrazione centrale o un amministratore locale e deve disporre dei privilegi equivalenti al ruolo di sicurezza di amministrazione basato su ruoli **Amministratore completo**.  

    -   **Sito primario**: l'account usato per eseguire una reimpostazione del sito deve essere un amministratore locale nel server del sito primario e deve disporre dei privilegi equivalenti al ruolo di sicurezza di amministrazione basato su ruoli **Amministratore completo**. Se il sito primario si trova in una gerarchia con un sito di amministrazione centrale, anche questo account deve essere un amministratore locale nel server del sito di amministrazione centrale.  

**Limitazioni per la reimpostazione del sito**
  - A partire dalla versione 1602, non è possibile usare una reimpostazione del sito per modificare i Language Pack server o client installati nei siti quando la gerarchia è configurata per supportare i [test degli aggiornamenti client in una raccolta di pre-produzione](/sccm/core/clients/manage/upgrade/test-client-upgrades).

#### <a name="to-perform-a-site-reset"></a>Per eseguire una reimpostazione del sito  

1.  Eseguire il **programma di installazione di Configuration Manager** da **&lt;cartella di installazione del sito di Configuration Manager\>\BIN\X64\setup.exe**.  

    > [!TIP]  
    >  È possibile eseguire una reimpostazione del sito anche avviando l'installazione di Configuration Manager nel menu **Start** del computer del server del sito o dal supporto di origine di Configuration Manager.  

2.  Nella pagina **Riquadro attività iniziale** selezionare **Esegui una manutenzione del sito o reimposta il sito**, quindi fare clic su **Avanti**.  

3.  Nella pagina **Manutenzione sito** selezionare **Reimposta sito senza modifiche alla configurazione**, quindi fare clic su **Avanti**.  

4.  Fare clic su **Sì** per iniziare la reimpostazione del sito.  

Al termine della reimpostazione del sito, fare clic su **Chiudi** per completare la procedura.  

##  <a name="bkmk_sitelang"></a> Gestire i Language Pack in un sito  
Dopo l'installazione di un sito, è possibile gestire i Language Pack di server e client in uso:  

**Language Pack server:**  

-   **Si applica a:**  

     Installazioni delle console di Configuration Manager  

     Nuove installazioni dei ruoli del sistema del sito applicabili  

-   **Dettagli:**  

     Dopo aver aggiornato i Language Pack server in un sito è possibile aggiungere il supporto per i Language Pack nelle console di Configuration Manager.  

     Per aggiungere il supporto per un Language Pack server in una console di Configuration Manager, è necessario installare la console di Configuration Manager dalla cartella **ConsoleSetup** in un server del sito che include il Language Pack da usare. Se la console di Configuration Manager è già installata, è necessario innanzitutto disinstallarla per consentire alla nuova installazione di identificare l'elenco corrente di Language Pack supportati.  

**Language Pack client:**  

-   **Si applica a:**  

     Le modifiche ai Language Pack dei client aggiornano i file di origine dell'installazione client in modo che le nuove installazioni di client o gli aggiornamenti possano aggiungere il supporto per l'elenco corrente di lingue del client.  

-   **Dettagli:**  

     Dopo aver aggiornato i Language Pack client in un sito è necessario installare ogni client che utilizzerà i Language Pack tramite i file origine che includono i Language Pack client.  

Per informazioni sulle lingue di client e server supportate da Configuration Manager, vedere [Language Pack in System Center Configuration Manager](../../../core/servers/deploy/install/language-packs.md)  

#### <a name="to-modify-the-language-packs-that-are-supported-at-a-site"></a>Per modificare i Language Pack supportati in un sito  

1.  Nel server del sito eseguire l'installazione di Configuration Manager da **&lt;cartella di installazione sito Configuration Manager\>\BIN\X64\setup.exe.**  

2.  Nella pagina **Riquadro attività iniziale** selezionare **Esegui una manutenzione del sito o reimposta il sito**, quindi fare clic su **Avanti**.  

3.  Nella pagina **Manutenzione sito** selezionare **Modifica la configurazione della lingua**, quindi fare clic su **Avanti**.  

4.  Nella pagina **Download prerequisiti** selezionare **Scarica file richiesti** per acquisire gli aggiornamenti nei Language Pack o selezionare **Utilizza file scaricati precedentemente** per utilizzare i file scaricati in precedenza che includono i Language Pack da aggiungere al sito. Fare clic su **Avanti** per convalidare i file e continuare.  

5.  Nella pagina **Selezione della lingua server** selezionare la casella di controllo relativa alle lingue del server supportate dal sito e quindi fare clic su **Avanti**.  

6.  Nella pagina **Selezione della lingua client** selezionare la casella di controllo relativa alle lingue del client supportate dal sito e quindi fare clic su **Avanti**.  

7.  Fare clic su **Avanti**per modificare la lingua di supporto nel sito.  

    > [!NOTE]  
    >  Configuration Manager avvia una reimpostazione del sito che reinstalla anche tutti i ruoli di sistema del sito presenti nel sito.  

8.  Fare clic su **Chiudi** per completare la procedura.  

##  <a name="BKMK_ModDBAlert"></a> Modificare la soglia di avviso del server di database  
 Per impostazione predefinita, Configuration Manager genera avvisi quando lo spazio libero su disco in un server di database del sito è insufficiente. Le impostazioni predefinite sono configurate per generare un'avvertenza quando lo spazio disponibile su disco è pari o inferiore a 10 GB e un avviso critico quando tale spazio è pari o inferiore a 5 GB. È possibile modificare questi valori o disattivare gli avvisi per ogni sito.  

 Per modificare queste impostazioni:  

1.  Nell'area di lavoro **Amministrazione** , espandere **Configurazione sito**, quindi fare clic su **Siti**.  

2.  Selezionare il sito che si vuole configurare e aprire la finestra di dialogo **Proprietà** del sito.  

3.  Nella finestra di dialogo **Proprietà** del sito selezionare la scheda **Avviso** e quindi modificare le impostazioni.  

4.  Fare clic su **OK** per chiudere la finestra di dialogo delle proprietà del sito.  

---
title: Distribuire i client Mac| Microsoft Docs
description: Informazioni su come distribuire i client a computer Mac in System Center Configuration Manager.
ms.custom: na
ms.date: 11/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
caps.latest.revision: 12
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 66071227fd10a43f7cd4e64508494d485392ffcd
ms.openlocfilehash: 6cbddd623767522a0026e0736b1f647fddbecfb6


---
# <a name="how-to-deploy-clients-to-macs-in-system-center-configuration-manager"></a>How to deploy clients to Macs in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In questo argomento viene descritto come installare il client di Configuration Manager sui computer Mac.

## <a name="prerequisites-and-preparatory-steps"></a>Prerequisiti e fasi preparatorie

### <a name="mac-prerequisites"></a>Prerequisiti Mac

Prima di installare il client verificare che i computer Mac soddisfino i prerequisiti, come descritto nella sezione dei [sistemi operativi supportati per i computer Mac](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).  

### <a name="certificate-requirements"></a>Requisiti del certificato
Per installare e gestire i client per computer Mac sono necessari i certificati di infrastruttura a chiave pubblica (PKI). I certificati PKI proteggono la comunicazione tra i computer Mac e il sito di Configuration Manager usando l'autenticazione manuale e i trasferimenti di dati crittografati. Configuration Manager può chiedere e installare un certificato client utente usando i Servizi certificati Microsoft con un'autorità di certificazione dell'organizzazione (CA) e il punto di registrazione di Configuration Manager e i ruoli del sistema del sito del punto proxy di registrazione. In alternativa, è possibile richiedere e installare un certificato del computer indipendentemente da Configuration Manager se il certificato soddisfa i requisiti per Configuration Manager.   
  
I client Mac di Configuration Manager eseguono sempre il controllo della revoca del certificato. Diversamente dai client di Configuration Manager eseguiti in Windows, è impossibile disattivare questa funzione di controllo dell'elenco di revoche di certificati (CRL).  
  
Se i client Mac non riescono a confermare lo stato di revoca del certificato per un certificato del server poiché non riescono a individuare il CRL, non saranno in grado di connettersi ai sistemi del sito di Configuration Manager, ad esempio i punti di gestione e i punti di distribuzione. Per i client Mac che si trovano in una foresta diversa rispetto a quella dell'autorità di certificazione emittente, controllare la struttura del CRL per verificare che i client Mac siano in grado di individuare e connettersi a un punto di distribuzione dell'elenco di revoche di certificati (CDP) per la connessione dei server del sistema del sito.  

Prima di installare il client di Configuration Manager in un computer Mac, stabilire come installare il certificato client:  

-   Usare la registrazione di Configuration Manager tramite lo strumento CMEnroll e seguire la procedura presentata nella sezione successiva di questo argomento. Il processo di registrazione non supporta il rinnovo automatico del certificato, di conseguenza è necessario registrare nuovamente i computer Mac prima della scadenza del certificato installato.  

-   Usare una richiesta di certificato e un metodo di installazione indipendente da Configuration Manager. Per questo metodo di installazione, vedere la sezione [Use a certificate request and installation method that is independent from Configuration Manager](#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager) in questo argomento.  

Per altre informazioni sui requisiti del certificato del client Mac e altri certificati PKI necessari per supportare i computer Mac, vedere [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md) (Requisiti dei certificati PKI per System Center Configuration Manager).  

I client Mac vengono assegnati automaticamente al sito di Configuration Manager che li gestisce. I client Mac vengono installati come client solo Internet, anche se la comunicazione è limitata alla rete Intranet. In base a questa configurazione client, le comunicazioni avverranno con i ruoli del sistema del sito (punti di gestione e punti di distribuzione) nel sito assegnato quando questi ruoli del sistema del sito vengono configurati per consentire le connessioni client dalla rete Internet. I computer Mac non comunicano con i ruoli del sistema del sito al di fuori del sito assegnato.  

> [!IMPORTANT]  
>  Il client Mac di Configuration Manager non può essere usato per connettersi a un punto di gestione configurato per usare una [replica di database](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  


### <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Distribuire un certificato server Web nei server di sistema del sito  
Se i sistemi del sito non hanno un certificato server Web, distribuirlo nei computer con questi ruoli del sistema del sito:  

-   Punto di gestione  

-   Punto di distribuzione  

-   Punto di registrazione  

-   Punto proxy di registrazione  

Il certificato del server Web deve contenere l'FQDN Internet specificato nelle proprietà del sistema del sito. Il server non deve essere accessibile da Internet per supportare i computer Mac. Se non è richiesta la gestione client basata su Internet, è possibile specificare il valore FQDN intranet per FQDN Internet.  

Specificare il valore FQDN Internet del sistema del sito nel certificato server Web per il punto di gestione, il punto di distribuzione e il punto proxy di registrazione. 

Per una distribuzione di esempio che crea e installa questo certificato server Web, vedere [Deploying the Web Server Certificate for Site Systems that Run IIS](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012) (Distribuire il certificato del server Web per sistemi del sito che eseguono IIS).  

 

### <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Distribuire un certificato di autenticazione client nei server di sistema del sito  
 Se i sistemi del sito non hanno un certificato di autenticazione client, distribuirlo nei computer con i seguenti ruoli del sistema del sito:  

-   Punto di gestione  

-   Punto di distribuzione  

 Per una distribuzione di esempio che crea e installa il certificato client per i punti di gestione, vedere [Deploying the Client Certificate for Windows Computers](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012) (Distribuzione del certificato client per computer Windows)  

 Per una distribuzione di esempio che crea e installa il certificato client per i punti di gestione, vedere [Deploying the Client Certificate for Distribution Points](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012) (Distribuzione del certificato client per punti di distribuzione).  

### <a name="prepare-the-client-certificate-template-for-macs"></a>Preparare il modello di certificato client per i computer Mac  

> [!NOTE]  
>  Per eseguire lo strumento di registrazione di Configuration Manager, è necessario essere in possesso di un account utente Active Directory.  

 Il modello di certificato deve disporre delle autorizzazioni di **lettura** e **registrazione** per l'account utente che registrerà il certificato nel computer Mac.  

 Vedere [Deploying the Client Certificate for Mac Computers](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1) (Distribuzione del certificato client per computer Mac).  

### <a name="configure-the-management-point-and-distribution-point"></a>Configurare il punto di gestione e il punto di distribuzione  
 Configurare i punti di gestione per le seguenti opzioni:  

-   HTTPS  

-   Consentire le connessioni client da Internet. Questo valore di configurazione è necessario per gestire computer Mac. Tuttavia, non significa che i server del sistema del sito devono essere accessibile da Internet.  

-   Consenti ai dispositivi mobili e ai computer Mac l'utilizzo del punto di gestione  

 Nonostante i punti di distribuzione non siano necessari per l'installazione del client, è necessario configurarli per consentire le connessioni client da Internet se si vuole distribuire il software in questi computer dopo aver installato il client.  

 
##### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>Per configurare i punti di gestione e i punti di distribuzione per supportare i computer Mac  

Prima di iniziare questa procedura, assicurarsi che il server del sistema del sito su cui sono in esecuzione il punto di gestione e di distribuzione siano configurati con un FQDN Internet. Se questi server non supportano la gestione client basata su Internet, è possibile specificare il valore FQDN Intranet come valore FQDN Internet. 

Questi ruoli del sistema del sito devono trovarsi in un sito primario.  


1.  Nella console di Configuration Manager selezionare **Amministrazione** > **Configurazione del sito** > **Server e ruoli del sistema del sito** e scegliere il server con i ruoli del sistema del sito corretti.  

3.  Nel riquadro dei dettagli fare clic con il pulsante destro del mouse su **Punto di gestione**, scegliere **Proprietà ruolo** e configurare le opzioni seguenti nella finestra di dialogo **Proprietà punto di gestione**:  

    1.  Scegliere **HTTPS**.  

    2.  Selezionare **Consenti solo connessione client Internet** o **Allow intranet and Internet client connections** (Consenti connessioni client Intranet e Internet). Per queste opzioni è necessario un valore FQDN Internet o Intranet.  

    3.  Selezionare **Consenti ai dispositivi mobili e ai computer Mac l'utilizzo del punto di gestione**.  

4.  Nel riquadro dei dettagli fare clic con il pulsante destro del mouse su **Punto di distribuzione**, scegliere **Proprietà ruolo** e configurare le opzioni seguenti nella finestra di dialogo **Proprietà punto di distribuzione**:  

    -   Scegliere **HTTPS**.  

    -   Selezionare **Consenti solo connessione client Internet** o **Allow intranet and Internet client connections** (Consenti connessioni client Intranet e Internet). Per queste opzioni è necessario un valore FQDN Internet o Intranet.  

    -   Fare clic su **Importa certificato**, selezionare il file del certificato del punto di distribuzione client esportato e specificare la password.  

5.  Ripetere i passaggi da 2 a 4 per tutti i punti di gestione e i punti di distribuzione dei siti primari che verranno usati con i computer Mac.  

### <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Configurare il punto proxy di registrazione e il punto di registrazione  
 È necessario installare entrambi questi ruoli del sistema del sito nello stesso sito, ma non occorre installarli nello stesso server del sistema del sito o nella stessa foresta Active Directory.  

 Per altre informazioni sul posizionamento del ruolo del sistema del sito e relative considerazioni, vedere [Site system roles](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles) (Ruoli del sistema del sito) in [Plan for site system servers and site system roles for System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md) (Pianificare i server e i ruoli del sistema del sito per System Center Configuration Manager).  

 Queste procedure consentono di configurare i ruoli del sistema del sito per supportare i computer Mac. Scegliere una di queste procedure a seconda che si installi un nuovo server del sistema del sito per supportare i computer Mac oppure si usi un server del sistema del sito esistente:  

-   [Nuovo server di sistema del sito](#new-site-system-server)  

-   [Server di sistema del sito esistente](#existing-site-system-server)  

####  <a name="new-site-system-server"></a>nuovo server del sistema del sito  

1.  Nella console di Configuration Manager selezionare **Amministrazione** >  **Configurazione del sito** > **Server e ruoli del sistema del sito**  

3.  Nella scheda **Home**, nel gruppo **Crea**, selezionare **Crea server di sistema sito**.  

4.  Nella pagina **Generale** specificare le impostazioni generali per il sistema del sito.  Assicurarsi di aver specificato un valore FQDN Internet. Se il server non è accessibile da Internet, usare il valore FQDN Intranet.  

5.  Nella pagina **Selezione ruolo del sistema** selezionare **Punto proxy di registrazione** e **Punto di registrazione** dall'elenco dei ruoli disponibili.  

6.  Nella pagina **Punto proxy di registrazione** rivedere le impostazioni e apportare eventuali modifiche necessarie.  

7.  Nella pagina **Enrollment Point Settings** (Impostazioni punto di registrazione) rivedere le impostazioni e apportare eventuali modifiche necessarie. Completare la procedura guidata.  

#### <a name="existing-site-system-server"></a>server del sistema del sito esistente  

1.  Nella console di Configuration Manager selezionare **Amministrazione** >  **Configurazione del sito** > **Server e ruoli del sistema del sito** e scegliere il server che si vuole usare per supportare i computer Mac.  

3.  Nella scheda **Home**, nel gruppo **Crea**, selezionare **Aggiungi ruoli del sistema del sito**.  

4.  Nella pagina **Generale** specificare le impostazioni generali per il sistema del sito e quindi fare clic su **Avanti**. Assicurarsi di aver specificato un valore FQDN Internet. Se il server non è accessibile da Internet, usare il valore FQDN Intranet.   

5.  Nella pagina **Selezione ruolo del sistema** scegliere **Punto proxy di registrazione** e **Punto di registrazione** dall'elenco dei ruoli disponibili.  

6.  Nella pagina **Punto proxy di registrazione** rivedere le impostazioni e apportare eventuali modifiche necessarie.  

7.  Nella pagina **Enrollment Point Settings** (Impostazioni punto di registrazione) rivedere le impostazioni e apportare eventuali modifiche necessarie. Completare la procedura guidata.  

### <a name="optional-install-the-reporting-services-point"></a>Facoltativo: installare il punto di Reporting Services  
 Installare il punto di Reporting Services se si vuole eseguire report per i computer Mac.  

 Per altre informazioni su come installare e configurare un punto di Reporting Services, vedere [Configuring Reporting in Configuration Manager](../../../core/servers/manage/configuring-reporting.md) (Configurazione della creazione di report in Configuration Manager).  


##  <a name="install-and-configure-the-client-for-macs"></a>Installare e configurare il client per i computer Mac  


### <a name="configure-client-settings-for-enrollment"></a>Configurare le impostazioni client per la registrazione  
 È necessario usare le impostazioni client predefinite per configurare la registrazione per i computer Mac. È impossibile usare le impostazioni client personalizzate.  

 Per altre informazioni sulle impostazioni client, vedere [About client settings in System Center Configuration Manager](../../../core/clients/deploy/about-client-settings.md).  

 Questa operazione è necessaria affinché Configuration Manager richieda e installi il certificato nel computer Mac.  

#### <a name="to-configure-the-default-client-settings-for-configuration-manager-to-enroll-certificates-for-macs"></a>Per configurare le impostazioni client predefinite per Configuration Manager per registrare i certificati per i computer Mac  

1.  Nella console di Configuration Manager selezionare **Amministrazione** >  **Impostazioni client** > **Impostazioni client predefinite**.  

4.  Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

5.  Selezionare la sezione **Registrazione** e quindi configurare le seguenti impostazioni:  

    1.  **Consentire agli utenti di registrare i dispositivi mobili e i computer Mac: Sì**  

    2.  **Profilo di registrazione**: scegliere **Imposta profilo**.  

6.  Nella finestra di dialogo **Profilo di registrazione del dispositivo mobile** scegliere **Crea**.  

7.  Nella finestra di dialogo **Crea profilo di registrazione** inserire un nome per questo profilo di registrazione e quindi configurare il **Codice del sito di gestione**. Selezionare il sito primario di Configuration Manager che contiene i punti di gestione che gestiranno i computer Mac.  

    > [!NOTE]  
    >  Se è impossibile selezionare il sito, verificare che almeno un punto di gestione nel sito sia configurato per supportare i dispositivi mobili.  

8.  Scegliere **Aggiungi**.  

9. Nella finestra di dialogo **Aggiungi autorità di certificazione per dispositivi mobili** selezionare il server dell'autorità di certificazione (CA) che emetterà i certificati per i computer Mac.  

10. Nella finestra di dialogo **Crea profilo di registrazione** selezionare il modello di certificato del computer Mac creato nel passaggio 3.  

11. Fare clic su **OK** per chiudere la finestra di dialogo **Profilo di registrazione** e quindi la finestra di dialogo **Impostazioni client predefinite**.  

    > [!TIP]  
    >  Se si desidera modificare l'intervallo dei criteri client, usare l'impostazione client **Intervallo di polling dei criteri client** nel gruppo di impostazione client **Criteri client** .  

 Tutti gli utenti verranno configurati con queste impostazioni al successivo download dei criteri client. Per avviare il recupero dei criteri per un singolo client, vedere [Initiate Policy Retrieval for a Configuration Manager Client](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval) (Avviare il recupero criteri per un client di Configuration Manager).  

 Oltre alle impostazioni client di registrazione, verificare di aver configurato le seguenti impostazioni del dispositivo client di Configuration Manager:  

-   **Inventario hardware**: abilitare e configurare questa opzione se si vuole raccogliere l'inventario hardware dai computer client Mac e Windows. Per altre informazioni, vedere [How to extend hardware inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/extend-hardware-inventory.md) (Come estendere l'inventario hardware in System Center Configuration Manager).  

-   **Impostazioni di conformità**: abilitare e configurare questa opzione se si vuole valutare e correggere le impostazioni nei computer client Mac e Windows. Per altre informazioni, vedere [Plan for and configure compliance settings](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) (Pianificare e configurare le impostazioni di conformità).  

> [!NOTE]  
>  Per altre informazioni sulle impostazioni client di Configuration Manager, vedere [How to configure client settings in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md) (Come configurare le impostazioni client in System Center Configuration Manager).  

### <a name="download-the-client-source-files-for-macs"></a>Scaricare i file di origine del client per i computer Mac  
 È necessario scaricare e installare i seguenti programmi prima di poter installare e gestire il client di Configuration Manager nei computer Mac:  

-   **Ccmsetup**: usare questa applicazione per installare il client di Configuration Manager nei computer Mac.  

-   **CMDiagnostics**: usare questo strumento per raccogliere informazioni di diagnostica correlate al client di Configuration Manager nei computer Mac.  

-   **CMUninstall**: usare questo strumento per disinstallare il client di Configuration Manager dai computer Mac.  

-   **CMAppUtil**: usare questo strumento per convertire pacchetti di applicazioni Apple in un formato che possa essere distribuito come applicazione di Configuration Manager.  

-   **CMEnroll**: usare questo strumento per richiedere e installare il certificato client per un computer Mac per poter quindi installare il client di Configuration Manager.  

> [!IMPORTANT]  
>  Quando si installa un nuovo client per i computer Mac, può essere necessario installare anche gli aggiornamenti di Configuration Manager per riflettere le nuove informazioni client nella console di Configuration Manager.  

##### <a name="to-download-and-install-the-mac-os-x-client-files"></a>Per scaricare e installare i file del client Mac OS X  

1.  Scaricare il pacchetto di file del client Mac OS X, **ConfigmgrMacClient.msi**e salvarlo in un computer con sistema operativo Windows.  

     Questo file non è incluso nel supporto di installazione di Configuration Manager. È possibile scaricare questo file dall' [Area download Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

2.  Nel computer Windows, eseguire il file **ConfigmgrMacClient.msi** appena scaricato per estrarre il pacchetto del client Mac Macclient.dmg in una cartella sul disco locale (per impostazione predefinita **C:\Programmi (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client\\**).  

3.  Copiare il file Macclient.dmg in una cartella sul computer Mac.  

4.  Eseguire il file Macclient.dmg nel computer Mac per estrarre i file in una cartella sul disco locale.  

5.  Nella cartella, assicurarsi che i file Ccmsetup e CMClient.pkg vengano estratti e che venga creata una cartella denominata Strumenti che contenga gli strumenti CMDiagnostics, CMUninstall, CMAppUtil e CMEnroll.  

### <a name="install-the-client-and-then-enroll-the-client-certificate-on-the-mac"></a>Installare il client e registrare il certificato client nel computer Mac  
 Questa procedura installa il client e usa lo strumento CMEnroll per richiedere e installare il certificato client per un computer Mac, in modo da poter quindi gestire questo computer usando Configuration Manager.  

 È possibile registrare il client usando la registrazione guidata dei computer Mac senza dover usare lo strumento CMEnroll, come descritto nella sezione relativa alla [registrazione del client usando la procedura guidata per i computer Mac](#enroll-the-client-by-using-the-mac-computer-enrollment-wizard)  

#### <a name="to-install-the-client-and-enroll-the-certificate-by-using-the-cmenroll-tool"></a>Per installare il client e registrare il certificato usando lo strumento CMEnroll  

1.  Nel computer Mac passare alla cartella in cui è stato estratto il contenuto del file Macclient.dmg.  

2.  Immettere la riga di comando seguente: **sudo ./ccmsetup**  

3.  Attendere fino a visualizzare il messaggio **Installazione completata** . Sebbene il programma di installazione visualizzi un messaggio di riavvio necessario immediato, non riavviare e andare al passaggio successivo.  

4.  Dalla cartella Strumenti nel computer Mac, digitare quanto segue: **sudo ./CMEnroll -s &lt;nome_server_proxy_registrazione> -ignorecertchainvalidation -u &lt;nome utente'>**  

    Dopo l'installazione del client, viene avviata la procedura guidata di registrazione del computer Mac per semplificarne la registrazione. Per registrare il client con questo metodo, vedere [To enroll the client by using the Mac Computer Enrollment Wizard](#BKMK_EnrollR2) in questo argomento.  

5. Digitare la password per l'account utente di Active Directory.  Quando si immette questo comando vengono richieste due password: la prima richiesta è per l'esecuzione del comando da parte dell'account utente con privilegi avanzati. La seconda richiesta è relativa all'account utente di Active Directory. L'aspetto delle due richieste è identico, quindi accertarsi di specificarli nella sequenza corretta.  

    Il nome utente può essere nei seguenti formati:  

    -   'dominio\nome'. Ad esempio: 'contoso\mnorth'  

    -   'user@domain'. Ad esempio: 'mnorth@contoso.com'  

     Il nome utente e la relativa password devono corrispondere a un account utente Active Directory a cui sono concesse la autorizzazioni di Lettura e Registrazione nel modello di certificato del client Mac.  

     Esempio: se il server del punto proxy di registrazione è denominato **server02.contoso.com**e a un nome utente di **contoso\mnorth** sono state concesse le autorizzazioni per il modello di certificato client Mac, digitare: **sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'**  

    > [!NOTE]  
    >  Se il nome utente contiene i caratteri **&lt;>"+=,** la registrazione avrà esito negativo. Per risolvere questo problema, ottenere un certificato fuori banda con un nome utente che non contenga tali caratteri.  
    >  
    >  Per un'esperienza utente più fluida, è possibile eseguire lo script dei passaggi e comandi di installazione, in modo che gli utenti debbano fornire solo il nome utente e la password.  

5.  Attendere fino a visualizzare il messaggio **Registrazione completata** .  

6.  Per limitare il certificato registrato in Configuration Manager, sul computer Mac, aprire una finestra terminale e apportare le modifiche seguenti:  

    a.  Immettere il comando **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  Nella finestra di dialogo **Keychain Access** (Accesso portachiavi) scegliere **System** (Sistema) nella sezione **Keychains** (Portachiavi) e quindi **Keys** (Chiavi) nella sezione **Category** (Categoria).  

    c.  Espandere le chiavi per visualizzare i certificati client. Dopo aver identificato il certificato con una chiave privata appena installata, fare doppio clic sulla chiave.  

    d.  Nella scheda **Access Control** (Controllo di accesso) selezionare **Confirm before allowing access** (Conferma prima di consentire l'accesso).  

    e.  Passare a **/Library/Application Support/Microsoft/CCM**, selezionare **CCMClient** (CCMClient) e fare clic su **Add** (Aggiungi).  

    f.  Fare clic su **Save Changes** (Salva modifiche) e chiudere la finestra di dialogo **Keychain Access** (Accesso portachiavi).  

7.  Riavviare il computer Mac.  

 Verificare che l'installazione client sia avvenuta correttamente aprendo l'elemento **Configuration Manager** in **Preferenze di Sistema** nel computer Mac. È possibile inoltre aggiornare e visualizzare la raccolta **Tutti i sistemi** per confermare che il computer Mac venga visualizzato in questa raccolta come client gestito.  

> [!TIP]  
>  Per risolvere qualsiasi tipo di problema con il client Mac, è possibile usare il programma CMDiagnostics incluso nel pacchetto del client Mac OS X, per raccogliere le seguenti informazioni diagnostiche:  
>   
>  -   Un elenco dei processi in esecuzione  
> -   La versione del sistema operativo Mac OS X  
> -   Le segnalazioni di arresto anomalo del Mac OS X relative al client di Configuration Manager incluse **CCM\*.crash** e **System Preference.crash**.  
> -   Il file della distinta base (BOM) e dell'elenco delle proprietà (.plist) creato dall'installazione client di Configuration Manager.  
> -   Il contenuto della cartella /Library/Application Support/Microsoft/CCM/Logs.  
>   
>  Le informazioni raccolte da CmDiagnostics vengono aggiunte a un file zip che viene salvato sul desktop del computer e denominato *<nomehost\>***-***<data e ora\>*.zip.  

####  <a name="enroll-the-client-by-using-the-mac-computer-enrollment-wizard"></a>Registrare il client usando la registrazione guidata computer Mac  

1.  Dopo aver completato l'installazione del client viene avviata la registrazione guidata computer. Se la procedura guidata non si apre oppure se viene chiusa in modo accidentale, fare clic su **Registra** dalla pagina delle preferenze **Configuration Manager** per aprire la procedura guidata.  

2.  Nella seconda pagina della procedura guidata specificare le informazioni seguenti:  

    -   **Nome utente** : è possibile scegliere uno dei seguenti formati:  

        -   'dominio\nome'. Ad esempio: 'contoso\mnorth'  

        -   'user@domain'. Ad esempio: 'mnorth@contoso.com'  

            > [!IMPORTANT]  
            >  Se si usa un indirizzo di posta elettronica per compilare il campo **Nome utente**, il nome di dominio dell'indirizzo di posta elettronica e il nome predefinito del server del punto proxy di registrazione vengono usati da Configuration Manager per compilare automaticamente il campo **Nome server**. Se il nome di dominio e il nome server non corrispondono al nome del server del punto proxy di registrazione, è necessario consigliare il nome corretto da usare, in modo da poterlo inserire durante la registrazione dei computer Mac.  

         Il nome utente e la relativa password devono corrispondere a un account utente Active Directory a cui sono concesse la autorizzazioni di Lettura e Registrazione nel modello di certificato del client Mac.  

    -   **Password**: immettere una password corrispondente per il nome utente specificato.  

    -   **Nome server**: immettere il nome del server del punto proxy di registrazione.  

3.  Fare clic su **Avanti** per continuare, quindi completare la procedura guidata.  

## <a name="maintenance-tasks-for-mac-clients"></a>Attività di manutenzione per i client Mac

###  <a name="uninstalling-the-mac-client"></a>Disinstallazione del client Mac  

1.  In un computer Mac aprire una finestra terminale e spostarsi nella cartella in cui è stato estratto il contenuto del file macclient.dmg scaricato in precedenza.  

2.  Spostarsi nella cartella Strumenti e immettere la seguente riga di comando:  

     **./CMUninstall -c**  

    > [!NOTE]  
    >  La proprietà **-c** indica alla disinstallazione del client di rimuovere anche i log di arresto anomalo e i file di log del client. Questa operazione è facoltativa, ma una procedura consigliata per evitare confusione se si reinstalla successivamente il client.  

3.  Se necessario, rimuovere manualmente il certificato di autenticazione client usato da Configuration Manager o revocarlo. CMUnistall non rimuove né revoca questo certificato.  

###  <a name="renewing-the-mac-client-certificate"></a>Rinnovo del certificato del client Mac  
 Per rinnovare il certificato del client Mac, usare uno dei seguenti metodi:  

-   [Rinnovo guidato del certificato](#renew-certificate-wizard)  

-   [Rinnovo manuale del certificato](#renew-certificate-manually)  

####  <a name="renew-certificate-wizard"></a>Rinnovo guidato del certificato  

1.  Configurare i valori seguenti come *stringhe* nel file ccmclient.plist che specifica quando aprire il Rinnovo guidato del certificato:  

    -   **RenewalPeriod1**: specifica, in secondi, il primo periodo di rinnovo in cui gli utenti possono rinnovare il certificato. Il valore predefinito è 3888000 secondi (45 giorni). Non configurare un valore inferiore a 300, poiché il periodo sarà ripristinato sul valore predefinito. 


    -   **RenewalPeriod2**: specifica, in secondi, il secondo periodo di rinnovo in cui gli utenti possono rinnovare il certificato. Il valore predefinito è 259200 secondi (3 giorni). Se il valore viene configurato, è superiore o uguale a 300 secondi ed è inferiore o uguale a **RenewalPeriod1**, il valore sarà usato. Se **RenewalPeriod1** è maggiore di 3 giorni, verrà usato un valore di 3 giorni per **RenewalPeriod2**.  Se **RenewalPeriod1** è minore di 3 giorni, **RenewalPeriod2** viene impostato sullo stesso valore di **RenewalPeriod1**.  

    -   **RenewalReminderInterval1**: specifica, in secondi, la frequenza con la quale la procedura guidata di rinnovo certificato verrà presentata agli utenti durante il primo periodo di rinnovo. Il valore predefinito è 86.400 secondi (1 giorno). Se **RenewalReminderInterval1** è superiore a 300 secondi e inferiore al valore configurato per **RenewalPeriod1**, verrà usato il valore configurato. In caso contrario, verrà usato il valore predefinito di 1 giorno.  

    -   **RenewalReminderInterval2**: specifica, in secondi, la frequenza con la quale la procedura guidata di rinnovo del certificato verrà presentata agli utenti durante il secondo periodo di rinnovo. Il valore predefinito è 28.800 secondi (8 ore). Se **RenewalReminderInterval2** è superiore a 300 secondi, inferiore o uguale a **RenewalReminderInterval1** e inferiore o uguale a **RenewalPeriod2**, verrà usato il valore configurato. In caso contrario, verrà usato un valore di 8 ore.  

     **Esempio** : se vengono mantenuti i valori predefiniti, 45 giorni prima della scadenza del certificato la procedura guidata verrà avviata ogni 24 ore.  Entro 3 giorni del certificato in scadenza, la procedura guidata si aprirà ogni 8 ore.  

     **Esempio:** usare la riga di comando seguente o uno script per impostare il primo periodo di rinnovo su 20 giorni.  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2.  Quando si apre il Rinnovo guidato del certificato, i campi **Nome utente** e **Nome server** verranno generalmente prealimentati e l'utente necessiterà soltanto di immettere una password per rinnovare il certificato.  

    > [!NOTE]  
    >  Se la procedura guidata non si apre oppure se questa viene chiusa in modo accidentale, fare clic su **Rinnova** dalla pagina delle preferenze **Configuration Manager** per aprire la procedura guidata.  

####  <a name="renewing-the-mac-client-certificate-manually"></a>Rinnovo manuale del certificato del client Mac  
 Il periodo di validità tipico per il certificato client Mac è 1 anno. Configuration Manager non rinnova automaticamente il certificato utente richiesto durante la registrazione, perciò è necessario usare la procedura seguente per rinnovare il certificato manualmente.  

> [!IMPORTANT]  
>  Se il certificato scade, è necessario disinstallare, reinstallare e quindi registrare nuovamente il client Mac.  

 Questa procedura rimuove l'SMSID, necessario per richiedere un nuovo certificato per lo stesso computer Mac. Quando si rimuove e sostituisce l'SMSID del client, tutte le cronologie client archiviate, come l'inventario, vengono eliminate dopo aver eliminato il client dalla console di Configuration Manager.  

1.  Creare e popolare una raccolta di dispositivi per i computer Mac che devono rinnovare i certificati utente.  

    > [!WARNING]  
    >  Configuration Manager non monitora il periodo di validità del certificato che registra per i computer Mac. È necessario monitorarlo indipendentemente da Configuration Manager per identificare i computer Mac da aggiungere a questa raccolta.  

2.  Nell'area di lavoro **Asset e conformità** , avviare la **Creazione guidata dell'elemento di configurazione**.  

3.  Nella pagina **Generale** della procedura guidata specificare le informazioni seguenti:  

    -   **Nome:Rimuovere SMSID per Mac**  

    -   **Tipo:Mac OS X**  

4.  Nella pagina **Piattaforme supportate** della procedura guidata, assicurarsi che siano selezionate tutte le versioni di Mac OS X.  

5.  Nella pagina **Impostazioni** della procedura guidata scegliere **Nuovo**, quindi nella finestra di dialogo **Crea impostazione** specificare le informazioni seguenti:  

    -   **Nome:Rimuovere SMSID per Mac**  

    -   **Tipo di impostazione:Script**  

    -   **Tipo di dati: stringa**  

6.  Nella finestra di dialogo **Crea impostazione**, per **Script di individuazione** scegliere **Aggiungi script** per specificare uno script che individui i computer Mac con un SMSID configurato.  

7.  Nella finestra di dialogo **Modifica script di individuazione** , immettere il seguente script della shell:  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Fare clic su **OK** per chiudere la finestra di dialogo **Modifica script di individuazione** .  

9. Nella finestra di dialogo **Crea impostazione**, per **Script di monitoraggio e aggiornamento (facoltativo)** scegliere **Aggiungi script** per specificare uno script che rimuova l'SMSID quando viene rilevato in computer Mac.  

10. Nella finestra di dialogo **Crea script di monitoraggio e aggiornamento** , immettere il seguente script della shell:  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Fare clic su **OK** per chiudere la finestra di dialogo **Crea script di monitoraggio e aggiornamento**.  

12. Nella pagina **Regole di conformità** della procedura guidata fare clic su **Nuovo**, quindi nella finestra di dialogo **Crea regola** specificare le informazioni seguenti:  

    -   **Nome:Rimuovere SMSID per Mac**  

    -   **Impostazione selezionata:** fare clic su **Sfoglia** e selezionare lo script di individuazione specificato in precedenza.  

    -   Nel campo **i seguenti valori** immettere **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    -   Abilitare l'opzione **Eseguire lo script di monitoraggio e aggiornamento specificato quando l'impostazione non è conforme**.  

13. Completare la Creazione guidata dell'elemento di configurazione.  

14. Creare una linea di base di configurazione che contenga l'elemento di configurazione appena creato e distribuirlo nella raccolta di dispositivi creata nel passaggio 1.  

     Per altre informazioni su come creare e distribuire le linee di base della configurazione, vedere [How to create configuration baselines in System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md) (Come creare linee di base di configurazione in System Center Configuration Manager) e [How to deploy configuration baselines in System Center Configuration Manager](../../../compliance/deploy-use/deploy-configuration-baselines.md) (Come distribuire linee di base di configurazione in System Center Configuration Manager).  

15. Nei computer Mac con l'SMSID rimosso, eseguire il comando seguente per installare un nuovo certificato:  

    ```  
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     Se richiesto, fornire la password per l'account utente con privilegi avanzati per eseguire il comando, quindi la password per l'account utente di Active Directory.  

16. Per limitare il certificato registrato in Configuration Manager, sul computer Mac, aprire una finestra terminale e apportare le modifiche seguenti:  

    a.  Immettere il comando **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  Nella finestra di dialogo **Keychain Access** (Accesso portachiavi) scegliere **System** (Sistema) nella sezione **Keychains** (Portachiavi) e quindi **Keys** (Chiavi) nella sezione **Category** (Categoria).  

    c.  Espandere le chiavi per visualizzare i certificati client. Dopo aver identificato il certificato con una chiave privata appena installata, fare doppio clic sulla chiave.  

    d.  Nella scheda **Access Control** (Controllo di accesso) selezionare **Confirm before allowing access** (Conferma prima di consentire l'accesso).  

    e.  Passare a **/Library/Application Support/Microsoft/CCM**, selezionare **CCMClient** (CCMClient) e fare clic su **Add** (Aggiungi).  

    f.  Fare clic su **Save Changes** (Salva modifiche) e chiudere la finestra di dialogo **Keychain Access** (Accesso portachiavi).  

17. Riavviare il computer Mac.  

##  <a name="use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager"></a>Usare una richiesta di certificato e un metodo di installazione indipendente da Configuration Manager  
 Quando non si usa la registrazione di Configuration Manager ma si richiede e installa il certificato client indipendentemente da Configuration Manager, i passaggi di configurazione sono leggermente diversi

Iniziare eseguendo *solo* questi passaggi:

a. [Distribuire un certificato server Web nei server del sistema del sito](#deploy-a-web-server-certificate-to-site-system-servers)

b. [Distribuire un certificato di autenticazione client nei server del sistema del sito](#deploy-a-client-authentication-certificate-to-site-system-servers)

c. [Configurare il punto di gestione e il punto di distribuzione](#configure-the-management-point-and-distribution-point)

d. [Facoltativo: installare il punto di Reporting Services](#optional:-install-the-reporting-services-point)

e. [Scaricare i file di origine del client per i computer Mac](#download-the-client-source-files-forMacs).  
  

#### <a name="to-install-the-client-certificate-independently-from-configuration-manager-and-install-the-client"></a>Per installare il certificato client indipendentemente da Configuration Manager e installare il client  

1.  Per installare il certificato client indipendentemente da Configuration Manager, usare le istruzioni allegate al metodo di distribuzione del certificato scelto per richiedere e installare il certificato client nel computer Mac.  

2.  Spostarsi nella cartella in cui è stato estratto il contenuto del file macclient.dmg scaricato dall'Area download Microsoft.  

3.  Immettere la riga di comando seguente: **sudo ./ccmsetup –MP <FQDN Internet punto di gestione\> -SubjectName <valore oggetto certificato\>**.  Il valore dell'oggetto certificato distingue tra maiuscole e minuscole, quindi digitarlo esattamente come appare nei dettagli del certificato.  

     Esempio: se l'FQDN Internet nelle proprietà del sistema del sito è **server03.contoso.com** e il certificato del client Mac ha l'FQDN **mac12.contoso.com** come nome comune nel soggetto del certificato, digitare: **sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com**  

4.  Attendere fino a visualizzare il messaggio **Installazione completata** , quindi riavviare il computer Mac.  

5.  Per verificare che questo certificato sia accessibile da Configuration Manager, sul computer Mac aprire una finestra terminale e apportare le modifiche seguenti:  

    a.  Immettere il comando **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  Nella finestra di dialogo **Keychain Access** (Accesso portachiavi) scegliere **System** (Sistema) nella sezione **Keychains** (Portachiavi) e quindi **Keys** (Chiavi) nella sezione **Category** (Categoria).  

    c.  Espandere le chiavi per visualizzare i certificati client. Dopo aver identificato il certificato con una chiave privata appena installata, fare doppio clic sulla chiave.  

    d.  Nella scheda **Access Control** (Controllo di accesso) selezionare **Confirm before allowing access** (Conferma prima di consentire l'accesso).  

    e.  Passare a **/Library/Application Support/Microsoft/CCM**, selezionare **CCMClient** (CCMClient) e fare clic su **Add** (Aggiungi).  

    f.  Fare clic su **Save Changes** (Salva modifiche) e chiudere la finestra di dialogo **Keychain Access** (Accesso portachiavi).  

6.  Se si dispone di più certificati contenenti lo stesso valore soggetto, specificare il numero di serie del certificato per identificare il certificato da usare per il client di Configuration Manager. A tale scopo, usare il comando seguente: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<numero di serie\>"**.  

     Ad esempio: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

 Verificare che l'installazione client sia avvenuta correttamente aprendo l'elemento **Configuration Manager** in **Preferenze di Sistema** nel computer Mac. È anche possibile aggiornare e visualizzare la raccolta **Tutti i sistemi** per verificare se il computer Mac appare in questa raccolta come client gestito.  

### <a name="renewing-the-mac-client-certificate"></a>Rinnovo del certificato del client Mac  
 Attenersi alla seguente procedura prima di rinnovare il certificato del computer nei computer Mac.  

 Questa procedura rimuove l'SMSID, che è necessario affinché il client usi un certificato nuovo o rinnovato nel computer Mac.  

> [!IMPORTANT]  
>  Quando si rimuove e sostituisce l'SMSID del client, tutte le cronologie client archiviate, come l'inventario, vengono eliminate dopo aver eliminato il client dalla console di Configuration Manager.  

#### <a name="to-renew-the-mac-client-certificate"></a>Per rinnovare il certificato del client Mac  

1.  Creare e popolare una raccolta di dispositivi per i computer Mac che devono rinnovare i certificati dei computer.  

2.  Nell'area di lavoro **Asset e conformità** , avviare la **Creazione guidata dell'elemento di configurazione**.  

3.  Nella pagina **Generale** della procedura guidata specificare le informazioni seguenti:  

    -   **Nome:Rimuovere SMSID per Mac**  

    -   **Tipo:Mac OS X**  

4.  Nella pagina **Piattaforme supportate** della procedura guidata, assicurarsi che siano selezionate tutte le versioni di Mac OS X.  

5.  Nella pagina **Impostazioni** della procedura guidata fare clic su **Nuovo** , quindi nella finestra di dialogo **Crea impostazione** specificare le informazioni seguenti:  

    -   **Nome:Rimuovere SMSID per Mac**  

    -   **Tipo di impostazione:Script**  

    -   **Tipo di dati: stringa**  

6.  Nella finestra di dialogo **Crea impostazione** , per **Script di individuazione**, fare clic su **Aggiungi script** per specificare uno script che individui i computer Mac con un SMSID configurato.  

7.  Nella finestra di dialogo **Modifica script di individuazione** , immettere il seguente script della shell:  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Fare clic su **OK** per chiudere la finestra di dialogo **Modifica script di individuazione** .  

9. Nella finestra di dialogo **Crea impostazione**, per **Script di monitoraggio e aggiornamento (facoltativo)** scegliere **Aggiungi script** per specificare uno script che rimuova l'SMSID quando viene rilevato in computer Mac.  

10. Nella finestra di dialogo **Crea script di monitoraggio e aggiornamento** , immettere il seguente script della shell:  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Fare clic su **OK** per chiudere la finestra di dialogo **Crea script di monitoraggio e aggiornamento**.  

12. Nella pagina **Regole di conformità** della procedura guidata fare clic su **Nuovo**, quindi nella finestra di dialogo **Crea regola** specificare le informazioni seguenti:  

    -   **Nome:Rimuovere SMSID per Mac**  

    -   **Impostazione selezionata:** fare clic su **Sfoglia** e selezionare lo script di individuazione specificato in precedenza.  

    -   Nel campo **i seguenti valori** immettere **The domain/default pair of (com.microsoft.ccmclient, SMSID) does not exist**.  

    -   Abilitare l'opzione **Eseguire lo script di monitoraggio e aggiornamento specificato quando l'impostazione non è conforme**.  

13. Completare la Creazione guidata dell'elemento di configurazione.  

14. Creare una linea di base della configurazione che contenga l'elemento di configurazione appena creato e lo distribuisca nella raccolta dispositivi creata nel Passaggio 1.  

     Per altre informazioni su come creare e distribuire le linee di base di configurazione, vedere [How to create configuration baselines in System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md) (Come creare linee di base di configurazione in System Center Configuration Manager).  

15. Dopo aver installato un nuovo certificato nei computer Mac con l'SMSID rimosso, eseguire il comando seguente per configurare il client per l'utilizzo del nuovo certificato:  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <Subject_Name_of_New_Certificate>  
    ```  

16. Se si hanno più certificati contenenti lo stesso valore soggetto, specificare il numero di serie del certificato per identificare il certificato da usare per il client di Configuration Manager. A tale scopo, usare il comando seguente: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<numero di serie\>"**.  

     Ad esempio: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

17. Riavviare il computer Mac.  



<!--HONumber=Dec16_HO3-->



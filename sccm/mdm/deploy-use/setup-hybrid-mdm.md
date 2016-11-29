---
title: Impostazione della gestione dei dispositivi mobili locale ibrida | System Center Configuration Manager e Microsoft Intune
description: Impostazione della registrazione ibrida di dispositivi con Configuration Manager e Intune.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: 34
caps.handback.revision: 0
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 44c0947fcb7abdc4369fe0b4f47409b49d068861

---

# <a name="setup-hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Impostare la gestione dei dispositivi mobili ibrida con System Center Configuration Manager e Microsoft Intune

*Si applica a: System Center Configuration Manager (Current Branch)*


Prima di poter essere gestiti con Configuration Manager, i dispositivi iOS, Windows e Android devono essere registrati con Intune. Usare i passaggi seguenti per impostare la registrazione ibrida dei dispositivi con Configuration Manager tramite Intune. Una volta completati i passaggi seguenti, la registrazione "bring your own device" (BYOD) per gli utenti sarà abilitata. Questi passaggi sono anche i prerequisiti per la [registrazione dei dispositivi di proprietà dell'azienda](enroll-company-owned-devices.md).

 |Passaggi|Dettagli|  
 |-----------|-------------|  
 |**Passaggio 1:** [Creare una raccolta della gestione dei dispositivi mobili](#step-1-create-an-mdm-collection)|Creare una raccolta utente di Configuration Manager con gli utenti i cui dispositivi possono essere registrati|  
 |**Passaggio 2:** [Requisiti dei nomi di dominio](#step-2-domain-name-requirements)|Confermare che il servizio Domain Name Service (DNS) e la gestione utente di Active Directory della propria organizzazione soddisfino i requisiti della gestione dei dispositivi mobili|
 |**Passaggio 3:** [Configurare una sottoscrizione di Intune](#step-3-configure-intune-subscription)|Il servizio Intune consente di gestire i dispositivi su Internet.|  
 |**Passaggio 4:** [Aggiungere termini e condizioni](#step-4-add-terms-and-conditions)| Creare i termini e le condizioni che devono essere accettate dagli utenti per poter usare l'app Portale aziendale|
 |**Passaggio 5:** [Creare il punto di connessione del servizio](#step-5-create-service-connection-point)|Il punto di connessione del servizio invia le impostazioni e le informazioni di distribuzione del software a Configuration Manager e recupera i messaggi di stato e di inventario dai dispositivi mobili. |  
 |**Passaggio 6:** [Abilitare la registrazione della piattaforma](#step-6-enable-platform-enrollment)|La registrazione nella gestione dei dispositivi mobili per i dispositivi [iOS](#ios-and-mac-enrollment-setup) e [Windows](#windows-enrollment-setup) richiede passaggi aggiuntivi per la comunicazione tra il servizio e i dispositivi. Per Android non è richiesta alcuna configurazione aggiuntiva.|  
 |**Passaggio 7:** [Impostare la gestione aggiuntiva](#step-7-set-up-additional-management)|(Facoltativo) Impostare gli elementi di configurazione e l'accesso condizionale per i dispositivi registrati|
 |**Passaggio 8:** [Verificare la configurazione della gestione dei dispositivi mobili](#step-8-verify-mdm-configuration)|Visualizzare i file di log per verificare che il punto di connessione del servizio sia stato creato correttamente e che gli account utente siano sincronizzati.|
 |**Passaggio 9:** [Registrare i dispositivi](#step-9-enroll-devices)|Informare gli utenti sulle modalità di registrazione dei dispositivi oppure avviare la registrazione dei dispositivi di proprietà dell'azienda per soddisfare le esigenze dell'organizzazione|

Per informazioni su Intune senza Configuration Manager
> [!div class="button"]
[Vedi documenti di Intune >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)

## <a name="step-1-create-an-mdm-collection"></a>Passaggio 1: Creare una raccolta della gestione dei dispositivi mobili
La raccolta utenti di Configuration Manager è necessaria per specificare gli utenti che possono registrare i dispositivi nella gestione. Solo le raccolte utenti possono rappresentare una destinazione perché le licenze di Intune vengono assegnate agli utenti. A scopo di test è possibile impostare una **Regola diretta** e aggiungere utenti specifici che possono registrare i dispositivi. Nella console di Configuration Manager scegliere **Asset e conformità** > **Raccolte utenti**, fare clic sulla scheda **Home** > gruppo **Crea** e quindi fare clic su **Crea raccolta utenti**. Per definire gli utenti per una distribuzione più ampia è necessario usare **Regole di query**. Per altre informazioni sulle raccolte, vedere [Come creare le raccolte in System Center Configuration Manager](https://technet.microsoft.com/library/mt629371.aspx).

![Per creare una raccolta utenti per la gestione dei dispositivi mobili](../media/mdm-create-user-collection.png)

## <a name="step-2-domain-name-requirements"></a>Passaggio 2: Requisiti dei nomi di dominio

Se necessario, eseguire i passaggi seguenti per soddisfare tutte le dipendenze esterne a Configuration Manager:

1. Ogni utente deve avere assegnata una licenza Intune per registrare i dispositivi. Per associare le licenze Intune agli utenti, ogni utente deve avere un nome entità utente (UPN) che può essere risolto pubblicamente. Ad esempio, johndoe@contoso.com) o un ID di accesso alternativo configurato in Azure Active Directory. La configurazione di un ID di accesso alternativo consente agli utenti di accedere con un indirizzo di posta elettronica, ad esempio, anche se il loro UPN è in formato NetBIOS (ad esempio, CONTOSO\davidemilano).

  - Se la società usa UPN risolvibili pubblicamente, ad esempio johndoe@contoso.com),, non è richiesta alcun'altra configurazione.
  - Se la società usa un UPN non risolvibile, ad esempio CONTOSO\davidemilano, è necessario [configurare un ID alternativo in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#pages-under-the-section-sync).

2.  Distribuire e configurare Active Directory Federation Services (AD FS). Facoltativo

     Quando viene configurato l'accesso Single Sign-On, gli utenti possono usare le credenziali aziendali per accedere ai servizi di Intune.

     Per altre informazioni, vedere i seguenti argomenti:
    -   [Preparazione dell'accesso Single Sign-On](http://go.microsoft.com/fwlink/?LinkID=271124)
    -   [Pianificare e distribuire AD FS 2.0 per l'uso con l'accesso Single Sign-On](http://go.microsoft.com/fwlink/?LinkID=271125)

3.  Distribuire e configurare la sincronizzazione directory.

     La sincronizzazione della directory consente di popolare Intune con gli account utente sincronizzati. I gruppi di sicurezza e gli account utente sincronizzati vengono aggiunti a Intune. La mancata abilitazione di Sincronizzazione della directory è una causa comune dell'impossibilità di registrare i dispositivi quando si configura la gestione dei dispositivi mobili per Configuration Manager con Microsoft Intune.

     Per altre informazioni, vedere [Integrazione di directory](http://go.microsoft.com/fwlink/?LinkID=271120) nella libreria della documentazione di Active Directory.

4.  Facoltativo, non consigliato: se non si usa Active Directory Federation Services, reimpostare le password di Microsoft Online degli utenti.

     Se non si usa ADFS, è necessario impostare una password di Microsoft Online per ciascun utente.

## <a name="step-3-configure-intune-subscription"></a>Passaggio 3: Configurare una sottoscrizione di Intune
 La sottoscrizione di Intune consente di gestire i dispositivi su Internet. Consente anche di specificare quale raccolta utenti può registrare i dispositivi e di definire le informazioni presentate agli utenti. La sottoscrizione di Intune esegue le operazioni seguenti:

-   Recupera il certificato necessario al punto di connessione del servizio per connettersi al servizio Intune
-   Definisce la raccolta di utenti che consente agli utenti di registrare i dispositivi mobili
-   Definisce e configura le piattaforme mobili da supportare

> [!IMPORTANT]
>  Quando si crea una sottoscrizione per Microsoft Intune in Configuration Manager, il punto di connessione del servizio del sito passerà in "modalità online". Vedere [Informazioni sul punto di connessione del servizio in System Center Configuration Manager](../../core/servers/deploy/configure/about-the-service-connection-point.md).

### <a name="to-create-the-microsoft-intune-subscription"></a>Per creare la sottoscrizione a Microsoft Intune

1.  Se non è già stato fatto, creare un account di Microsoft Intune nel sito [Microsoft Intune](http://go.microsoft.com/fwlink/?LinkID=258216).  Dopo aver creato l'account di Intune, non sarà necessario aggiungere utenti per l'account di Intune o eseguire altre configurazioni.

2.  Nella console di Configuration Manager fare clic su **Amministrazione**.

3.  Nell'area di lavoro **Amministrazione** espandere **Servizi cloud**e fare clic su **Sottoscrizioni a Microsoft Intune**. Nella scheda **Home** fare clic su **Aggiungi sottoscrizione a Microsoft Intune**.

![Creare una sottoscrizione di Intune](../media/mdm-set-intune.png)

4.  Nella pagina **Introduzione** della Creazione guidata di una sottoscrizione a Microsoft Intune verificare il testo e quindi fare clic su **Avanti**.

5.  Nella pagina **Sottoscrizione** fare clic su **Accedi** e accedere usando l'account aziendale o dell'istituto di istruzione. Nella finestra di dialogo **Impostare l'autorità di gestione dei dispositivi mobili** selezionare la casella di controllo per gestire solo i dispositivi mobili usando Configuration Manager mediante la console di Configuration Manager. Per continuare con la sottoscrizione, è necessario selezionare questa opzione.

    > [!IMPORTANT]
    >  Dopo aver selezionato Configuration Manager come autorità di gestione, non sarà possibile modificarla successivamente in Microsoft Intune.

6.  Fare clic sui collegamenti privacy per verificarli e quindi fare clic su **Avanti**.

7.  Nella pagina **Generale** specificare le seguenti opzioni e quindi fare clic su **Avanti**.

  -   **Raccolta**: Specificare una raccolta utenti che contenga gli utenti che registreranno i dispositivi mobili.

      > [!NOTE]
      >  Se un utente viene rimosso dalla raccolta, il dispositivo dell'utente continuerà a essere gestito per un massimo di 24 ore finché il record utente non verrà rimosso dal database utenti.

  -   **Nome società**: specificare il nome della società.

  -   **URL della documentazione sulla privacy**: se si pubblicano le informazioni sulla privacy della società in un collegamento accessibile da Internet, fornire un collegamento a cui gli utenti possano accedere dal portale aziendale, ad esempio http://www.contoso.com/CP_privacy.html. Le informazioni sulla privacy possono chiarire quali informazioni gli utenti condividono con la società.

  -   **Combinazione colori per portale società**: Facoltativamente, modificare il colore predefinito blu per i portali società.

  -   **Codice del sito Configuration Manager**: Specificare un codice del sito per un sito primario per gestire i dispositivi mobili.

    > [!NOTE]
    >  La modifica del codice del sito riguarda solo le nuove registrazioni e non i dispositivi registrati esistenti.

8.  Nella pagina **Informazioni di contatto società** specificare le informazioni di contatto dell'azienda che vengono visualizzate nell'app Portale aziendale in **Contatta l'IT**. Specificare le informazioni di contatto dell'azienda e quindi fare clic su **Avanti**.

9. Nella pagina **Logo società** scegliere se visualizzare un logo nel portale aziendale e quindi fare clic su **Avanti**.

10. Completare la procedura guidata.

## <a name="step-4-add-terms-and-conditions"></a>Passaggio 4: Aggiungere termini e condizioni
 Dopo aver configurato la gestione Intune per dispositivi mobili, è possibile creare i **termini e le condizioni**. Usare i termini e le condizioni per spiegare agli utenti cosa accade quando registrano i dispositivi. Gli utenti devono accettare i termini e le condizioni prima di poter registrare un dispositivo. Nella console di Configuration Manager passare a **Asset e conformità** > **Panoramica** > **Impostazioni di conformità** > **Termini e condizioni** e fare clic su **Crea termini e condizioni**. Vedere [Termini e condizioni in System Center Configuration Manager](terms-and-conditions.md).

##  <a name="step-5-create-service-connection-point"></a>Passaggio 5 Creare il punto di connessione del servizio
Dopo avere creato la sottoscrizione, sarà quindi possibile installare il ruolo del sistema del sito del punto di connessione del servizio che consente di connettersi al servizio Intune. Questo ruolo del sistema del sito effettuerà il push delle impostazioni e delle applicazioni al servizio Intune.

 Il punto di connessione del servizio invia le impostazioni e le informazioni di distribuzione del software a Configuration Manager e recupera i messaggi di stato e di inventario dai dispositivi mobili. Il servizio Configuration Manager funge da gateway che comunica con i dispositivi mobili e archivia le impostazioni.

> [!NOTE]
>  Il ruolo del sistema del sito del punto di connessione del servizio può essere installato solo in un sito di amministrazione centrale o in un sito primario autonomo. Il punto di connessione del servizio deve avere accesso a Internet.


### <a name="configure-the-service-connection-point-role"></a>Configurare il ruolo del punto di connessione del servizio

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.

2.  Nell'area di lavoro **Amministrazione** espandere **Siti**, quindi fare clic su **Server e ruoli del sistema del sito**.

3.  Aggiungere il ruolo del **punto di connessione del servizio** a un server del sistema del sito nuovo o esistente usando il passaggio associato:

    -   Nuovo server del sistema del sito: nel gruppo **Crea** della scheda **Home** fare clic su **Crea server di sistema sito** per avviare la Creazione guidata server del sistema sito.

    -   Server del sistema del sito esistente: fare clic sul server in cui si vuole installare il ruolo del punto di connessione del servizio. Nella scheda **Home** , nel gruppo **Server** , fare clic su **Aggiungi ruoli del sistema del sito** per avviare l'Aggiunta guidata ruoli del sistema del sito.

4.  Nella pagina **Selezione ruolo del sistema** selezionare **Punto di connessione del servizio**, quindi fare clic su **Avanti**.

![Configurare un punto di connessione del servizio](../media/mdm-service-connection-point.png)

5.  Completare la procedura guidata.

### <a name="how-does-the-service-connection-point-authenticate-with-the-microsoft-intune-service"></a>Autenticazione del punto di connessione del servizio con il servizio Microsoft Intune
 Il punto di connessione del servizio estende Configuration Manager mediante una connessione al servizio basato su cloud Intune che gestisce i dispositivi mobili su Internet. Il punto di connessione del servizio esegue l'autenticazione con il servizio Intune come di seguito:

1.  Quando si crea una sottoscrizione di Intune nella console di Configuration Manager, l'amministratore di Configuration Manager viene autenticato mediante la connessione ad Azure Active Directory, che reindirizza al rispettivo server AD FS per la richiesta di nome utente e password. Intune rilascia quindi un certificato al tenant.

2.  Il certificato del passaggio 1 viene installato nel ruolo del sito del punto di connessione del servizio e viene usato per autenticare e autorizzare tutte le ulteriori comunicazioni con il servizio Microsoft Intune.

## <a name="step-6-enable-platform-enrollment"></a>Passaggio 6: Abilitare la registrazione della piattaforma
  Piattaforme per dispositivi diverse richiedono una configurazione aggiuntiva per abilitare la registrazione dei dispositivi:
  - [Impostazione della registrazione per iOS e Mac](#ios-and-mac-enrollment-setup): ottenere un certificato push MDM Apple
  - [Impostazione della registrazione per Windows](#windows-enrollment-setup): configurare il DNS e abilitare la registrazione per i dispositivi PC Windows, Windows Mobile 10 e Windows Phone
  - Android: i dispositivi Android non richiedono alcuna operazione aggiuntiva per abilitare la registrazione


### <a name="ios-and-mac-enrollment-setup"></a>Impostazione della registrazione per iOS e Mac
  La procedura seguente abilita la gestione per i dispositivi Apple, caricando un certificato push MDM Apple al servizio Intune.

  1.  **Scaricare una richiesta di firma certificato** : è necessario un file di richiesta di firma del certificato (CSR) per richiedere un certificato per il servizio APN da Apple.  

      1.  Nell'area di lavoro **Amministrazione** della console di Configuration Manager andare a **Servizi cloud**> **Sottoscrizioni a Microsoft Intune**.  

      2.  Nella scheda **Home** fare clic su **Crea richiesta certificato per servizio APN**. Si apre la finestra di dialogo **Richiesta di firma del certificato per Apple Push Notification Service** .  

      3.  **Andare** al percorso per salvare il nuovo file di richiesta di firma del certificato (csr). Salvare il file della richiesta di firma del certificato (estensione csr) in locale.  

      4.  Fare clic su **Scarica**. Il nuovo file CSR di Microsoft Intune viene scaricato e salvato da Configuration Manager. Questo file viene usato per richiedere un certificato di relazione di trust al portale Apple Push Certificates.  

  2.  **Richiedere un certificato per il servizio APN di Apple** : il certificato per il servizio APN (Apple Push Notification) viene usato per stabilire una relazione di trust tra il servizio di gestione, Intune e i dispositivi iOS mobili registrati.  

      1.  Usando un browser andare al [portale Apple Push Certificates](http://go.microsoft.com/fwlink/?LinkId=269844) e accedere con il proprio ID Apple aziendale. Questo ID Apple deve essere usato in futuro per rinnovare il certificato APN.  

      2.  Completare la procedura guidata usando il file della richiesta di firma del certificato (con estensione CSR). Scaricare il certificato APNs e salvare il file PEM in locale. Questo file del certificato APN con estensione pem viene usato per stabilire una relazione di trust tra il server Apple Push Notification e l'autorità di gestione dei dispositivi mobili di Intune.  

  3.  **Abilitare la registrazione e caricare il certificato APNs** : per abilitare la registrazione iOS, caricare il certificato APNs.  

      1.  Nell'area di lavoro **Amministrazione** della console di Configuration Manager andare a **Servizi cloud** > **Sottoscrizioni a Microsoft Intune**.  

      2.  Nella scheda **Home** nel gruppo **Sottoscrizione** fare clic su **Configura piattaforme** > **iOS**.  

          > [!NOTE]  
          >  Non caricare il certificato per il servizio Apple Push Notification (APNs) finché non viene abilitata la registrazione iOS nella console di Configuration Manager.  

      3.  Nella finestra di dialogo **Proprietà della sottoscrizione a Microsoft Intune** selezionare la scheda **iOS** e fare clic per selezionare la casella di controllo **Abilita registrazione iOS** .  

      4.  Fare clic su **Sfoglia**e andare al file (con estensione CER) del certificato per il servizio APN scaricato da Apple. Configuration Manager visualizza le informazioni sul certificato APNs. Fare clic su **OK** per salvare il certificato APN in Intune.    


Altre informazioni sulla [registrazione iOS e Mac](enroll-hybrid-ios-mac.md).

### <a name="windows-enrollment-setup"></a>Impostazione della registrazione per Windows  
È possibile usare Configuration Manager con Intune per gestire desktop, portatili e altri dispositivi che eseguono Windows come dispositivi mobili. È anche possibile configurare i dispositivi Windows 10 per [registrarsi automaticamente quando accedono ad Azure Active Directory](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/enroll-hybrid-windows#azure-active-directory-enrollment) mediante l'aggiunta di un account aziendale o dell'istituto di istruzione nel dispositivo.

Un Alias DNS (tipo di record CNAME) semplifica la registrazione dei dispositivi perché durante la registrazione del dispositivo il nome del server viene inserito automaticamente. È quindi possibile abilitare la registrazione per dispositivi mobili PC Windows.  

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager passare a **Servizi cloud** > **Sottoscrizioni a Microsoft Intune** ed eseguire quanto riportato:  
  - **PC Windows:** nella scheda **Home** fare clic su **Configura piattaforme** e quindi su **Windows**. Nella scheda **Generale** selezionare **Abilita registrazione Windows**.  
  - **Windows 10 Mobile e Windows Phone:** nella scheda **Home** fare clic su **Configura piattaforme** e quindi su **Windows Phone**.  Nella scheda **Generale** scegliere  **Windows Phone 8.1 e Windows 10 Mobile**.

2.  È anche possibile configurare Configuration Manager per semplificare la registrazione usando l'app Portale aziendale.
(Facoltativo) Creare un alias DNS, con tipo di record CNAME, nei record DNS della società che reindirizzi le richieste inviate a un URL nel dominio della società ai server del servizio cloud di Microsoft.  Ad esempio, se il sito Web della società è contoso.com, si creerà un record CNAME in DNS che reindirizzi EnterpriseEnrollment.contoso.com a EnterpriseEnrollment-s.manage.microsoft.com.  

|Tipo|Nome dell'host|Punta a|  
|----------|---------------|---------------|  
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com|  
|CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|  

Per altre informazioni, vedere [la registrazione dei dispositivi Windows](enroll-hybrid-windows.md).

### <a name="android-enrollment-setup"></a>Impostazione della registrazione per Android
È possibile usare Configuration Manager con Intune per gestire telefoni e tablet che eseguono Android.
1.  Nell'area di lavoro **Amministrazione** della console di Configuration Manager andare a **Servizi cloud** > **Sottoscrizioni a Microsoft Intune**.  

2.  Nel gruppo **Sottoscrizione** della scheda **Home** fare clic su **Configura piattaforme** > **Android**.  

3.  Nella finestra di dialogo **Proprietà sottoscrizione di Microsoft Intune** selezionare la scheda **Android** e fare clic per selezionare la casella di controllo **Abilita registrazione Android** .

Per altre informazioni, vedere [Android](enroll-hybrid-android.md).

## <a name="step-7-set-up-additional-management"></a>Passaggio 7: Impostare la gestione aggiuntiva
(Facoltativo) È possibile impostare la gestione aggiuntive prima che i dispositivi vengano registrati. Queste soluzioni di gestione possono essere create e distribuite una volta registrati i dispositivi, anche se molte organizzazioni preferiscono distribuirle nel momento in cui i dispositivi iniziano a essere gestiti.

**Gli elementi di configurazione** consentono di gestire le impostazioni, ad esempio richiedere un PIN o la crittografia nei dispositivi registrati in base alla piattaforma dei dispositivi:
- [Dispositivi Windows 10 e Windows 8.1](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)
- [Dispositivi Windows Phone](/sccm/compliance/deploy-use/create-configuration-items-for-windows-phone-devices-managed-without-the-client)
- [Dispositivi iOS e Mac](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)
- [Dispositivi Android e Samsung KNOX](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client)

**Le applicazioni** possono essere distribuite ai dispositivi gestiti:
- [Applicazioni iOS](/sccm/apps/get-started/creating-ios-applications)
- [Applicazioni Mac](/sccm/apps/get-started/creating-mac-computer-applications)
- [Applicazioni PC Windows](/sccm/apps/get-started/creating-windows-applications)
- [Applicazioni Windows Phone](/sccm/apps/get-started/creating-windows-phone-applications)
- [Applicazioni Android](/sccm/apps/get-started/creating-android-applications)

**L'accesso condizionale** consente di gestire l'accesso alle risorse aziendali tra cui:  
- [Accesso alla posta elettronica](/sccm/protect/deploy-use/manage-email-access)
- [Accesso a SharePoint](/sccm/protect/deploy-use/manage-sharepoint-online-access)
- [Accesso a Skype for Business](/sccm/protect/deploy-use/manage-skype-for-business-online-access)
- [Dynamics CRM Online](/sccm/protect/deploy-use/manage-dynamics-crm-online-access)

## <a name="step-8-verify-mdm-configuration"></a>Passaggio 8: Verificare la configurazione della gestione dei dispositivi mobili

 È possibile verificare alcuni componenti di gestione dei dispositivi controllando i file di log seguenti:

-   Controllare Cloudusersync.log per verificare che gli account utente siano sincronizzati correttamente.

-   Controllare Sitecomp.log per verificare che il punto di connessione del servizio sia stato creato correttamente.

## <a name="step-9-enroll-devices"></a>Passaggio 9: registrare i dispositivi
La configurazione ibrida è stata completata. È possibile registrare i dispositivi in Configuration Manager in diversi modi:
- Dispositivi di proprietà dell'utente (BYOD): [Informazioni sull'uso di Microsoft Intune per gli utenti finali](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune) - Le linee guida per la registrazione sono le stesse per i dispositivi gestiti con Intune e con la gestione ibrida
- Dispositivi di proprietà dell'azienda (COD): [la registrazione di dispositivi di proprietà dell'azienda](enroll-company-owned-devices.md) offre indicazioni sulle modalità specifiche per piattaforma per registrare i dispositivi di proprietà dell'azienda.

### <a name="managing-intune-subscriptions-associated-with-configuration-manager"></a>Gestione delle sottoscrizioni di Intune associate a Configuration Manager
 Se si aggiunge una sottoscrizione di valutazione o a pagamento di Microsoft Intune in Configuration Manager e successivamente è necessario passare a una sottoscrizione di Intune diversa, eliminare sia la **sottoscrizione a Microsoft Intune** che il **punto di connessione del servizio** dalla console di Configuration Manager prima di aggiungere una nuova sottoscrizione.

#### <a name="how-to-delete-an-intune-subscription-from-configuration-manager"></a>Come eliminare una sottoscrizione di Intune da Configuration Manager

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.

2.  Nell'area di lavoro **Amministrazione** espandere **Panoramica**, passare a **Servizi cloud** e fare clic su **Sottoscrizioni a Microsoft Intune**.

3.  Fare clic con il pulsante destro del mouse su **Sottoscrizione a Microsoft Intune** e quindi fare clic su **Elimina**. **Sottoscrizione a Microsoft Intune**.

    > [!IMPORTANT]
    >  Tutto il contenuto, incluse le registrazioni utente, i criteri e le distribuzioni dell'app configurate per la sottoscrizione di valutazione di Intune, andrà perso.

4.  Nell'area di lavoro **Amministrazione** espandere **Panoramica**, passare a **Configurazione del sito** e selezionare **Server e ruoli del sistema del sito**.

5.  Selezionare il server che ospita il ruolo **Punto di connessione del servizio**.

6.  Nell'elenco **Ruoli sistema del sito** selezionare **Punto di connessione del servizio** e quindi fare clic su **Rimuovi ruolo** nella barra multifunzione. Confermare la rimozione del ruolo. Il punto di connessione del servizio viene eliminato.

7.  È ora possibile creare un nuovo punto di connessione del servizio, aggiungere una nuova sottoscrizione di Intune a Configuration Manager e impostare Configuration Manager come autorità MDM.



<!--HONumber=Nov16_HO1-->



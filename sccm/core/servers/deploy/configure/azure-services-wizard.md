---
title: Procedura guidata per i servizi di Azure
titleSuffix: Configuration Manager
description: Informazioni sulla Procedura guidata per i servizi di Azure per System Center Configuration Manager.
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 833bc6588e079e124209d9c7adb91062e6afe6c3
ms.sourcegitcommit: d025a2cbd1ed82f42f67255c97b913f2163b3baf
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/02/2017
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configurare i servizi di Azure da usare con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

A partire da Current Branch versione 1706, per semplificare il processo di configurazione dei servizi di Azure usati con Configuration Manager viene usata la **Procedura guidata per i servizi di Azure**.

Questa procedura guidata offre un'esperienza di configurazione comune perché usa un'**app Web di Azure** per fornire i dettagli della sottoscrizione e della configurazione ed esegue l'autenticazione delle comunicazioni con Azure AD. L'app Web evita di dover immettere le stesse informazioni ogni volta che si configura un nuovo componente o servizio di Configuration Manager con Azure.

Tramite la Procedura guidata per i servizi di Azure è possibile configurare i servizi di Azure seguenti:
-   **Gestione cloud**   
    [Consente ai client di eseguire l'autenticazione usando Azure Active Directory](/sccm/core/clients/deploy/deploy-clients-cmg-azure) (Azure AD). È anche possibile [configurare l'individuazione utenti di Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc).
-   **OMS Connector**
    [Effettua la connessione a Operations Manager Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) (OMS) e sincronizza i dati, ad esempio le raccolte, in OMS Log Analytics.
-   **Preparazione aggiornamenti**
    [Connette a Preparazione aggiornamenti](/sccm/core/clients/manage/upgrade/upgrade-analytics) e visualizza i dati relativi alla compatibilità con l'aggiornamento per il client.
-   **Windows Store per le aziende** Effettua la connessione a [Windows Store per le aziende](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) e ottiene le app per l'organizzazione che è possibile distribuire con Configuration Manager.

Quando si usa la procedura guidata per configurare un servizio, sono disponibili diverse azioni comuni.
Sono inclusi:
-   *Configurare l'ambiente di Azure* : nella pagina **App** della procedura guidata selezionare l'**ambiente di Azure** in uso. Verificare il contenuto di ogni servizio per sapere se supporta solo il cloud di Azure pubblico o può supportare un cloud privato.
-   *Creare o importare un'app server*: nella pagina **App** della procedura guidata è possibile **creare** e **importare** metadati di registrazione dell'app Web di Azure. Le opzioni disponibili dipendono dal servizio che si sta configurando. Alcuni servizi potrebbero anche richiedere un'app aggiuntiva. Il servizio **Gestione cloud**, ad esempio, richiede un'**app client nativa** da usare per l'autenticazione diretta delle comunicazioni dei client con i servizi di Azure.


Per informazioni sulle app Web di Azure, vedere [Autenticazione e autorizzazione nel servizio app di Azure](/azure/app-service/app-service-authentication-overview) e [Panoramica di App Web](/azure/app-service-web/app-service-web-overview).


## <a name="webapp"></a>Creare o importare la registrazione di un'app Web di Azure Active Directory da usare con Configuration Manager

La registrazione dell'app Web per i servizi di Azure connette il sito di Configuration Manager ad Azure AD ed è un prerequisito per l'uso dei servizi di Azure con l'infrastruttura. Per eseguire questa operazione:

1.  Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e quindi fare clic su **Servizi di Azure**.
2.  Nella scheda **Home**, nel gruppo **Servizi di Azure**, fare clic su **Configura i servizi di Azure**.
3.  Nella pagina **Servizi di Azure** della procedura guidata per i servizi di Azure selezionare il servizio di Azure da connettere a Configuration Manager.
4.  Nella pagina **Generale** della procedura guidata specificare un nome e una descrizione per il servizio di Azure.
5.  Nella pagina **App** della procedura guidata selezionare l'ambiente di Azure nell'elenco, quindi fare clic su **Sfoglia** per selezionare l'*app Web* e l'*app client nativa* (solo se richiesto) che verranno usate per configurare il servizio di Azure.

    **App Web:** l'opzione Sfoglia apre la finestra App server.    
      Nella finestra **Server App** (App server) selezionare l'app server che si vuole usare e quindi fare clic su **OK**. Le app server sono le registrazioni di app Web di Azure AD che contengono le configurazioni per l'account Azure, inclusi ID del tenant, ID client e una chiave privata per i client.
    Se non è disponibile un'app, usare una delle opzioni seguenti:

    - **Crea**: automatizza la creazione della registrazione di un'app Web in Azure AD in base alle informazioni immesse nella console di Configuration Manager. Immettere un nome descrittivo per l'app, l'URL della home page, l'URI dell'ID app e il periodo di validità della chiave privata. Per impostazione predefinita, il periodo di validità della chiave privata è di un anno.
        
        Per continuare e completare la creazione dell'app Web in Azure, un utente deve ora accedere con le proprie credenziali di Azure AD. Non è necessario che l'account usato per accedere ad Azure sia lo stesso account che esegue la Procedura guidata per i servizi di Azure. Dopo l'accesso ad Azure, Configuration Manager crea l'app Web in Azure, inclusi l'ID client e la chiave privata da usare con l'app Web. In un secondo momento, è possibile visualizzare queste informazioni dal portale di Azure.

        Quando si usa *Crea* per configurare un'app Web, Configuration Manager può creare automaticamente l'app Web in Azure AD.
    
    - **Importa**: immettere le informazioni di registrazione di un'app Web di Azure AD già creata nel **portale di Azure** per importare i metadati relativi a tale registrazione in Configuration Manager. Specificare un nome descrittivo per l'app e il tenant, quindi specificare ID tenant, ID client e chiave privata per l'app Web di Azure che si vuole rendere disponibile per l'uso con Configuration Manager. Dopo aver verificato le informazioni, fare clic su **OK** per continuare.
        > [!NOTE]
        > Prima che sia possibile usare **Importa**, è necessario creare una registrazione di app di Azure AD di tipo *App Web/API* nel [portale di Azure](https://portal.azure.com). Per altre informazioni su come creare la registrazione di un'app, vedere [Registrare l'applicazione nel tenant di Azure Active Directory](/azure/active-directory/active-directory-app-registration). Quando si configura Preparazione aggiornamenti o Operations Management Suite, è anche necessario concedere all'app Web appena registrata autorizzazioni di *collaboratore* per il gruppo di risorse che contiene l'area di lavoro OMS pertinente, per consentire a Configuration Manager di accedere all'area di lavoro. A tale scopo, durante l'assegnazione dell'autorizzazione è necessario cercare il nome della registrazione dell'app nel pannello **Aggiungi utenti**. Questo processo è lo stesso che deve essere eseguito quando [si concedono a Configuration Manager autorizzazioni per OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) per le connessioni a [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm). Queste autorizzazioni devono essere assegnate prima che l'app venga importata in Configuration Manager.


    **App client nativa:** l'opzione Sfoglia apre la finestra App client.  
     Nella finestra **App client** selezionare l'app client che si vuole usare e quindi fare clic su **OK**.

     Se non è disponibile un'app client, usare una delle opzioni seguenti:
     - **Crea**: per creare una nuova app client, fare clic su **Crea**. Specificare quindi un nome descrittivo per l'app e l'URI di reindirizzamento.

         Per continuare e completare la creazione dell'app Web in Azure, un utente deve ora accedere con le proprie credenziali di Azure AD. Non è necessario che l'account usato per accedere ad Azure sia lo stesso account che esegue la Procedura guidata per i servizi di Azure. Dopo l'accesso ad Azure, Configuration Manager crea l'app client nativa in Azure AD, inclusi l'ID client e la chiave privata. In seguito sarà possibile visualizzare queste informazioni dal [portale di Azure](https://portal.azure.com). 

     - **Importa**: consente di usare un'app client già esistente nella sottoscrizione di Azure. Specificare un nome descrittivo per l'app e l'ID client. Fare quindi clic su **OK** per continuare.

  <!--  MOVE THIS AND STEP 6 TO configure Azure AD User Discover  content
       [!TIP]  
     When you use Import, the account you use to run the wizard must have the *Read directory data* application permission in the Azure portal. This is required to set the correct permissions for the App. When you use Create, Configuration Manager creates the app with the correct permissions. However, you still must give consent to the application in the Azure portal.   -->


6.  Solo se si sta configurando il servizio **Gestione cloud**, nella pagina **Individuazione** della procedura guidata fare clic su **Abilita l'individuazione utente di Azure Active Directory** e quindi fare clic su **Impostazioni**.
Nella finestra di dialogo **Impostazioni di individuazione utenti di Azure AD** configurare una pianificazione per quando si verifica l'individuazione. È anche possibile abilitare l'individuazione differenziale che verifica solo gli account nuovi o modificati in Azure AD. Altre informazioni sull'[individuazione utenti di Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).

7.  Completare la procedura guidata.

A questo punto la configurazione di un servizio di Azure in Configuration Manager è completata. È possibile ripetere questo processo per configurare altri servizi di Azure.

## <a name="view-the-configuration-of-an-azure-service"></a>Visualizzare la configurazione di un servizio di Azure
È possibile visualizzare le proprietà di un servizio di Azure configurato per l'uso.

Nella console andare ad **Amministrazione** > **Panoramica** > **Servizi cloud** > **Servizi di Azure**. Scegliere quindi il servizio che si vuole visualizzare o modificare e quindi fare clic su **Proprietà**.

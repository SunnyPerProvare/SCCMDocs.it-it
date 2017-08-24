---
title: Procedura guidata per i servizi di Azure | Microsoft Docs
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
ms.openlocfilehash: 22203b358830903cf2e531c0532ae3111b8265fc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configurare i servizi di Azure da usare con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

A partire da Current Branch versione 1706, la **Procedura guidata per i servizi di Azure** viene usata per semplificare il processo di configurazione dei servizi di Azure usati con Configuration Manager.

Questa procedura guidata offre un'esperienza di configurazione comune perché usa un'**app Web di Azure** per fornire i dettagli della sottoscrizione e della configurazione. L'app Web evita di dover immettere le stesse informazioni ogni volta che si configura un nuovo componente o servizio di Configuration Manager con Azure.

Usando la procedura guidata Configura i servizi di Azure, vengono configurati i servizi di Azure seguenti:
-   **Gestione cloud**   
    [Consente ai client di eseguire l'autenticazione usando Azure Active Directory]() (Azure AD). È anche possibile [configurare l'individuazione utenti di Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc).
-   **OMS Connector**
    [Connette a Operations Manager Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) (OMS) e sincronizza i dati, ad esempio le raccolte, con Log Analytics di OMS.
-   **Preparazione aggiornamenti**
    [Connette a Preparazione aggiornamenti](/sccm/core/clients/manage/upgrade/upgrade-analytics) e visualizza i dati relativi alla compatibilità con l'aggiornamento per il client.
-   **Windows Store per le aziende** Connette allo store online di [Windows Store per le aziende](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) e ottiene le app per l'organizzazione che è possibile distribuire con Configuration Manager.

Quando si usa la procedura guidata per configurare un servizio, sono disponibili diverse azioni comuni.
Sono inclusi:
-   Configurare l'ambiente di Azure: nella pagina **App** della procedura guidata si seleziona l'**ambiente di Azure** usato. Verificare il contenuto di ogni servizio per sapere se supporta solo il cloud di Azure pubblico o può supportare un cloud privato.
-   Creare o importare un'app server: nella pagina **App** della procedura guidata è possibile **creare** e **importare** app Web di Azure. Le opzioni disponibili dipendono dal servizio che si sta configurando.  Alcuni servizi potrebbero anche richiedere un'app aggiuntiva. Un servizio, ad esempio, potrebbe richiedere anche un'**app client nativa**.


Per informazioni sulle app Web di Azure, vedere [Autenticazione e autorizzazione nel servizio app di Azure](/azure/app-service/app-service-authentication-overview) e [Panoramica di App Web](/azure/app-service-web/app-service-web-overview)


## <a name="webapp"></a> Creare l'app Web di Azure da usare con Configuration Manager

L'app Web per i servizi di Azure connette il sito di Configuration Manager ad Azure AD ed è un prerequisito per l'uso dei servizi di Azure con l'infrastruttura. Per eseguire questa operazione:

1.  Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e quindi fare clic su **Servizi di Azure**.
2.  Nella scheda **Home**, nel gruppo **Servizi di Azure**, fare clic su **Configura i servizi di Azure**.
3.  Nella pagina **Servizi di Azure** della procedura guidata per i servizi di Azure, selezionare **Gestione cloud** per consentire ai client di autenticarsi nella gerarchia usando Azure AD.
4.  Nella pagina **Generale** della procedura guidata specificare un nome e una descrizione per il servizio di Azure.
5.  Nella pagina **App** della procedura guidata selezionare l'ambiente di Azure dall'elenco, quindi fare clic su **Sfoglia** per selezionare l'*app Web* e l'*app client nativa* che verranno usate per configurare il servizio di Azure.     
    **App Web:** l'opzione Sfoglia apre la finestra App server.    
      Nella finestra **Server App** (App server) selezionare l'app server che si vuole usare e quindi fare clic su **OK**. Le app server sono app Web di Azure che contengono le configurazioni per l'account Azure, inclusi ID del tenant, ID client e una chiave privata per i client.
    Se non è disponibile un'app, usare una delle opzioni seguenti:
        - **Crea**: per creare una nuova app server, fare clic su **Crea**. Immettere quindi un nome descrittivo per l'app, l'URL della home page, l'URI dell'ID app e il periodo di validità della chiave privata. Per impostazione predefinita, il periodo di validità della chiave privata è di un anno.

         Per continuare, un utente deve ora accedere ad Azure per completare la creazione dell'app Web in Azure. Non è necessario che l'account usato per accedere ad Azure sia lo stesso account che esegue la Procedura guidata per i servizi di Azure. Dopo l'accesso ad Azure, Configuration Manager crea l'app Web in Azure, inclusi l'ID client e la chiave privata da usare con l'app Web. In un secondo momento, è possibile visualizzare queste informazioni dal portale di Azure.

         Quando si usa Crea per configurare un'app Web, Configuration Manager può creare automaticamente l'app Web in Azure AD.
        - **Importa**: per usare un'app Web già esistente nella sottoscrizione di Azure, fare clic su **Importa**. Specificare un nome descrittivo per l'app e il tenant, quindi specificare ID tenant, ID client e chiave privata per l'app Web di Azure che si vuole rendere disponibile per l'uso con Configuration Manager. Dopo aver verificato le informazioni, fare clic su **OK** per continuare.

          Questa opzione non è disponibile per tutti i servizi, che è possibile configurare.

   **App client nativa:** l'opzione Sfoglia apre la finestra App client.  
     Nella finestra **App client** selezionare l'app client che si vuole usare e quindi fare clic su **OK**.

     Se non è disponibile un'app client, usare una delle opzioni seguenti:
     - **Crea**: per creare una nuova app client, fare clic su **Crea**. Specificare quindi un nome descrittivo per l'app e l'URL di risposta.

          Per continuare, un utente deve ora accedere ad Azure per completare la creazione dell'app client in Azure. Non è necessario che l'account usato per accedere ad Azure sia lo stesso account che esegue la Procedura guidata per i servizi di Azure. Dopo l'accesso ad Azure, Configuration Manager crea l'app client nativa in Azure, incluso l'ID client da usare con l'app Web. In un secondo momento, è possibile visualizzare queste informazioni dal portale di Azure.
          Quando si usa Crea per configurare l'app, Configuration Manager può creare automaticamente l'app client nativa in Azure AD.
     - **Importa**: per usare un'app client già esistente nella sottoscrizione di Azure, fare clic su **Importa**. Specificare un nome descrittivo per l'app e l'ID client. Fare quindi clic su **OK** per continuare.
           Questa opzione non è disponibile per tutti i servizi, che è possibile configurare.

  <!--  MOVE THIS AND STEP 6 TO configure Azure AD User Discover  content
       [!TIP]  
     When you use Import, the account you use to run the wizard must have the *Read directory data* application permission in the Azure portal. This is required to set the correct permissions for the App. When you use Create, Configuration Manager creates the app with the correct permissions. However, you still must give consent to the application in the Azure portal.   -->


6.  Nella pagina **Individuazione** della procedura guidata fare clic su **Abilita l'individuazione utente di Azure Active Directory** e quindi fare clic su **Impostazioni**.
Nella finestra di dialogo **Impostazioni di individuazione utenti di Azure AD** configurare una pianificazione per quando si verifica l'individuazione. È anche possibile abilitare l'individuazione differenziale che verifica solo gli account nuovi o modificati in Azure AD. Altre informazioni sull'[individuazione utenti di Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).
 
 7. Completare la procedura guidata.

A questo punto il sito di Configuration Manager è connesso ad Azure AD.

## <a name="view-the-configuration-of-an-azure-service"></a>Visualizzare la configurazione di un servizio di Azure
È possibile visualizzare le proprietà di un servizio di Azure configurato per l'uso.

Nella console andare ad **Amministrazione** > **Panoramica** > **Servizi cloud** > **Servizi di Azure**. Scegliere quindi il servizio che si vuole visualizzare o modificare e quindi fare clic su **Proprietà**.

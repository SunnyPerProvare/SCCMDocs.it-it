---
title: Configurare i servizi di Azure
titleSuffix: Configuration Manager
description: Connettere l'ambiente di Configuration Manager con i servizi di Azure per la gestione del cloud, Preparazione aggiornamenti, Microsoft Store per le aziende e Operations Management Suite.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7ff953d658c54c2cebbbfd29a6bba83fe65cc08e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342342"
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configurare i servizi di Azure da usare con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare la **Procedura guidata per i servizi di Azure** per semplificare il processo di configurazione dei servizi di Azure usati con Configuration Manager. Questa procedura guidata offre un'esperienza di configurazione comune usando le registrazioni di app Web di Azure Active Directory (Azure AD). Queste app specificano dettagli di sottoscrizione e configurazione e autenticano le comunicazioni con Azure AD. L'app evita di dover immettere le stesse informazioni ogni volta che si configura un nuovo componente o servizio di Configuration Manager con Azure.



## <a name="available-services"></a>Servizi disponibili

Configurare i seguenti servizi di Azure tramite questa procedura guidata:  

-   **Gestione cloud**: questo servizio consente al sito e ai client di eseguire l'autenticazione usando Azure AD. Questa autenticazione abilita altri scenari, ad esempio:  

    - [Installare e assegnare client di Configuration Manager in dispositivi Windows 10 usando Azure AD per l'autenticazione](/sccm/core/clients/deploy/deploy-clients-cmg-azure)  

    - [Configurare l'individuazione utente di Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

    - Supporto di alcuni [scenari di Cloud Management Gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#scenarios)  

-   **OMS Connector**: [connessione a Operations Management Suite (OMS)](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite). Consente di sincronizzare dati come le raccolte con OMS Log Analytics.  

-   **Connettore Upgrade Readiness**: connessione a [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) di Windows Analytics. Consente di visualizzare i dati di compatibilità degli aggiornamenti del client.  

-   **Microsoft Store per le aziende**: connessione a [Microsoft Store per le aziende](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business). Consente di ottenere da Microsoft Store le app distribuibili con Configuration Manager.  

### <a name="service-details"></a>Dettagli dei servizi

La tabella seguente elenca informazioni dettagliate sui singoli servizi.  

- **Tenant**: numero di istanze del servizio che è possibile configurare. Ogni istanza deve essere un tenant di Azure distinto.  

- **Cloud**: tutti i servizi supportano il cloud globale di Azure, ma non tutti i servizi supportano i cloud privati, ad esempio il cloud Azure Governo degli Stati Uniti.  

- **App Web**: indica se il servizio usa un'app Azure AD di tipo *App Web/API*, detta anche app server in Configuration Manager.  

- **App nativa**: indica se il servizio usa un'app Azure AD di tipo *Nativo*, detta anche app client in Configuration Manager.  

- **Azioni**: indica se è possibile importare o creare queste app nella procedura guidata per i servizi di Azure di Configuration Manager.  


|Service  |Tenant  |Cloud  |App Web  |App nativa  |Azioni  |
|---------|---------|---------|---------|---------|---------|
|Gestione cloud con</br>Individuazione utente Azure AD | Più elementi | Pubblico | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | Importa, Crea |
|Connettore OMS | Uno | Pubblico, Privato | ![Supportato](media/green_check.png) | ![Non supportato](media/Red_X.png) | Importa |
|Preparazione aggiornamenti | Uno | Pubblico | ![Supportato](media/green_check.png) | ![Non supportato](media/Red_X.png) | Importa |
|Microsoft Store per</br>le aziende e la formazione | Uno | Pubblico | ![Supportato](media/green_check.png) | ![Non supportato](media/Red_X.png) | Importa, Crea |


### <a name="about-azure-ad-apps"></a>Informazioni sulle app di Azure AD

I diversi servizi di Azure richiedono configurazioni distinte, implementabili nel portale di Azure. Le app di ogni servizio possono richiedere autorizzazioni di accesso specifiche alle risorse di Azure.  

È possibile usare una singola app per più servizi. In Configuration Manager e Azure AD è presente un solo oggetto da gestire. Quando la chiave di sicurezza dell'app scade, è sufficiente aggiornare una sola chiave.

La configurazione più sicura è l'uso di app separate per ogni servizio. Un'app per un determinato servizio può richiedere autorizzazioni aggiuntive che non sono richieste da un altro servizio. Se si usa un'unica app per più servizi è possibile che l'app disponga di più autorizzazioni di quelle necessarie. 

Quando si creano servizi di Azure aggiuntivi nella procedura guidata, Configuration Manager è progettato per riusare le informazioni comuni tra i servizi. Questo comportamento evita di dover specificare le stesse informazioni più volte. 

Per altre informazioni sulle autorizzazioni delle app necessarie e sulle configurazioni per ogni servizio, vedere l'articolo di Configuration Manager corrispondente in [Servizi disponibili](#available-services). 

Per altre informazioni sulle app di Azure, vedere gli articoli seguenti:
- [Autenticazione e autorizzazione nel servizio app di Azure](/azure/app-service/app-service-authentication-overview)
- [Panoramica di App Web](/azure/app-service-web/app-service-web-overview)
- [Basics of Registering an Application in Azure AD](/azure/active-directory/develop/active-directory-authentication-scenarios#basics-of-registering-an-application-in-azure-ad) (Nozioni di base per la registrazione di un'applicazione in Azure AD)  
- [Registrare l'applicazione nel tenant di Azure Active Directory](/azure/active-directory/active-directory-app-registration)



## <a name="before-you-begin"></a>Prima di iniziare

Dopo aver scelto il servizio al quale connettersi, fare riferimento alla tabella in [Dettagli servizio](#service-details). Questa tabella specifica informazioni necessarie per completare la procedura guidata del servizio di Azure. In primo luogo valutare le alternative con l'amministratore di Azure AD. Decidere se creare manualmente e in anticipo le app nel portale di Azure e quindi importare i dettagli dell'app in Configuration Manager. In alternativa è possibile usare Configuration Manager per creare le app direttamente in Azure AD. Per raccogliere i dati necessari da Azure AD, esaminare le informazioni delle altre sezioni di questo articolo.

Alcuni servizi richiedono che le app di Azure AD dispongano di autorizzazioni specifiche. Esaminare le informazioni per ogni servizio per determinare le autorizzazioni necessarie. Ad esempio, prima di poter importare un'app Web è necessario che un amministratore di Azure crei l'app nel [portale di Azure](https://portal.azure.com). Quando si configura Upgrade Readiness o OMS Connector è necessario concedere alla nuova app Web registrata l'autorizzazione *Collaboratore* per il gruppo di risorse che contiene l'area di lavoro OMS appropriata. Questa autorizzazione consente a Configuration Manager di accedere all'area di lavoro. Cercare il nome della registrazione dell'app nel pannello **Aggiungi utenti** durante l'assegnazione dell'autorizzazione. Questo processo è analogo a quello che [aggiunge a Configuration Manager le autorizzazioni per OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms). Queste autorizzazioni devono essere assegnate da un amministratore prima dell'importazione dell'app in Configuration Manager.



## <a name="start-the-azure-services-wizard"></a>Avviare la procedura guidata per i servizi di Azure

1.  Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**.  

2.  Nella scheda **Home** della barra multifunzione trovare il gruppo **Servizi di Azure** e fare clic su **Configura i servizi di Azure**.  

3.  Nella pagina **Servizi di Azure** della procedura guidata per i servizi di Azure:  

    1. Specificare un **Nome** per l'oggetto in Configuration Manager.  

    2. Specificare un parametro facoltativo **Descrizione** per identificare il servizio.  

    3. Selezionare il servizio di Azure che si vuole connettere con Configuration Manager.  

4. Fare clic su **Avanti** per passare alla pagina [Proprietà dell'app](#azure-app-properties) della procedura guidata per i servizi di Azure.  



## <a name="azure-app-properties"></a>Proprietà dell'app di Azure

Nella pagina **App** della procedura guidata per i servizi di Azure selezionare l'**ambiente Azure** dall'elenco. Per informazioni sull'ambiente attualmente disponibile per il servizio, vedere la tabella [Dettagli servizio](#service-details).

Il resto della pagina App varia in base al servizio specifico. Per informazioni sul tipo di app usata dal servizio e sull'azione che è possibile usare, vedere la tabella in [Dettagli servizio](#service-details). 
- Se l'app supporta sia l'azione di importazione che quella di creazione, fare clic su **Sfoglia**. Viene visualizzata la [finestra di dialogo App server](#server-app-dialog) o la [finestra di dialogo App client](#client-app-dialog).
- Se l'app supporta solo l'azione di importazione, fare clic su **Importa**. Viene visualizzata la [finestra di dialogo Importa le app (server)](#import-apps-dialog-server) o la finestra di dialogo [Importa le app (client)](#import-apps-dialog-client).

Dopo aver specificato le app in questa pagina, fare clic su **Avanti** per aprire la pagina [Configurazione o Individuazione](#configuration-or-discovery) della procedura guidata per i servizi di Azure.

### <a name="web-app"></a>App Web

Questa app Azure AD di tipo *App Web/API* è detta anche app server in Configuration Manager.

#### <a name="server-app-dialog"></a>Finestra di dialogo App server

Quando si fa clic su **Sfoglia** per **App Web** nella pagina App della procedura guidata per i servizi di Azure, viene visualizzata la finestra di dialogo App server. La finestra visualizza un elenco con le proprietà seguenti per le app web esistenti:
- Nome descrittivo del tenant
- Nome descrittivo dell'app
- Tipo di servizio

Nella finestra di dialogo App server è possibile eseguire tre operazioni:
- Per riusare un'app Web esistente, selezionarla nell'elenco. 
- Fare clic su **Importa** per aprire la [finestra di dialogo Importa le app](#import-apps-dialog-server).
- Fare clic su **Crea** per aprire la [finestra di dialogo Crea un'applicazione server](#create-server-application-dialog).

Dopo aver selezionato, importato o creato un'app Web, fare clic su **OK** per chiudere la finestra di dialogo App server. Questa azione torna a visualizzare la [pagina App](#azure-app-properties) della procedura guidata per i servizi di Azure.

#### <a name="import-apps-dialog-server"></a>Finestra di dialogo Importa le app (server)

Quando si fa clic su **Importa** nella finestra di dialogo App server o nella pagina App della procedura guidata per i servizi di Azure, viene visualizzata la finestra di dialogo Importa le app. Questa pagina consente di immettere informazioni su un'app Web di Azure AD che è già stata creata nel portale di Azure. Consente anche di importare i metadati relativi a questa app Web in Configuration Manager. Specificare le informazioni seguenti:
- **Nome del tenant di Azure AD**
- **ID tenant di Azure AD**
- **Nome applicazione**: nome descrittivo per l'app.
- **ID client**
- **Chiave privata**
- **Scadenza della chiave privata**: selezionare una data futura nel calendario. 
- **URI ID app**: questo valore deve essere univoco nel tenant di Azure AD. È incluso nel token di accesso usato dal client Configuration Manager per richiedere l'accesso al servizio. Per impostazione predefinita, questo valore è impostato su https://ConfigMgrService.  

Dopo aver immesso le informazioni, fare clic su **Verifica**. Quindi fare clic su **OK** per chiudere la finestra di dialogo Importa le app. Questa azione torna a visualizzare la [pagina App](#azure-app-properties) della procedura guidata per i servizi di Azure o la [finestra di dialogo App server](#server-app-dialog).

#### <a name="create-server-application-dialog"></a>Finestra di dialogo Crea un'applicazione server

Quando si fa clic su **Crea** nella finestra di dialogo App server viene visualizzata la finestra di dialogo Crea un'applicazione server. Questa pagina automatizza la creazione di un'app Web in Azure AD. Specificare le informazioni seguenti:
- **Nome applicazione**: nome descrittivo per l'app.
- **URL della home page**: questo valore non viene usato da Configuration Manager, ma è richiesto da Azure AD. Per impostazione predefinita, questo valore è impostato su https://ConfigMgrService.  
- **URI ID app**: questo valore deve essere univoco nel tenant di Azure AD. È incluso nel token di accesso usato dal client Configuration Manager per richiedere l'accesso al servizio. Per impostazione predefinita, questo valore è impostato su https://ConfigMgrService.  
- **Periodo di validità della chiave privata**: fare clic sull'elenco a discesa e selezionare **1 anno** o **2 anni**. Il valore predefinito è 1 anno.

Fare clic su **Accedi** per eseguire l'autenticazione in Azure come utente amministratore. Queste credenziali non vengono memorizzate in Configuration Manager. Questo utente tipo non richiede autorizzazioni in Configuration Manager e non deve necessariamente essere lo stesso account che esegue la procedura guidata per i servizi di Azure. Dopo l'autenticazione in Azure, nella pagina viene visualizzato il **Nome del tenant di Azure AD** come riferimento. 

Fare clic su **OK** per creare l'app Web in Azure AD e chiudere la finestra di dialogo Crea un'applicazione server. Questa azione torna a visualizzare la [finestra di dialogo App server](#server-app-dialog).


### <a name="native-client-app"></a>App client nativa
    
Questa app Azure AD di tipo *Nativo* è detta anche app client in Configuration Manager.

#### <a name="client-app-dialog"></a>Finestra di dialogo App client

Quando si fa clic su **Sfoglia** per **App client nativa** nella pagina App della procedura guidata per i servizi di Azure, viene visualizzata la finestra di dialogo App client. La finestra visualizza un elenco con le proprietà seguenti per le app native esistenti:
- Nome descrittivo del tenant
- Nome descrittivo dell'app
- Tipo di servizio

Nella finestra di dialogo App client è possibile eseguire tre operazioni:
- Per riusare un'app nativa esistente, selezionarla nell'elenco. 
- Fare clic su **Importa** per aprire la [finestra di dialogo Importa le app](#import-apps-dialog-client).
- Fare clic su **Crea** per aprire la [finestra di dialogo Crea un'applicazione client](#create-client-application-dialog).

Dopo aver selezionato, importato o creato un'app nativa, fare clic su **OK** per chiudere la finestra di dialogo App client. Questa azione torna a visualizzare la [pagina App](#azure-app-properties) della procedura guidata per i servizi di Azure.

#### <a name="import-apps-dialog-client"></a>Finestra di dialogo Importa le app (client)

Quando si fa clic su **Importa** nella finestra di dialogo App client viene visualizzata la finestra di dialogo Importa le app. Questa pagina consente di immettere informazioni su un'app nativa di Azure AD che è già stata creata nel portale di Azure. Consente anche di importare i metadati relativi all'app nativa in Configuration Manager. Specificare le informazioni seguenti:
- **Nome applicazione**: nome descrittivo per l'app.
- **ID client** 

Dopo aver immesso le informazioni, fare clic su **Verifica**. Quindi fare clic su **OK** per chiudere la finestra di dialogo Importa le app. Questa azione torna a visualizzare la [finestra di dialogo App client](#client-app-dialog).

#### <a name="create-client-application-dialog"></a>Finestra di dialogo Crea un'applicazione client

Quando si fa clic su **Crea** nella finestra di dialogo App client viene visualizzata la finestra di dialogo Crea un'applicazione client. Questa pagina automatizza la creazione di un'app nativa in Azure AD. Specificare le informazioni seguenti:
- **Nome applicazione**: nome descrittivo per l'app.
- **URL di risposta**: questo valore non viene usato da Configuration Manager, ma è richiesto da Azure AD. Per impostazione predefinita, questo valore è impostato su https://ConfigMgrService. 

Fare clic su **Accedi** per eseguire l'autenticazione in Azure come utente amministratore. Queste credenziali non vengono memorizzate in Configuration Manager. Questo utente tipo non richiede autorizzazioni in Configuration Manager e non deve necessariamente essere lo stesso account che esegue la procedura guidata per i servizi di Azure. Dopo l'autenticazione in Azure, nella pagina viene visualizzato il **Nome del tenant di Azure AD** come riferimento. 

Fare clic su **OK** per creare l'app nativa in Azure AD e chiudere la finestra di dialogo Crea un'applicazione client. Questa azione torna a visualizzare la [finestra di dialogo App client](#client-app-dialog).


## <a name="configuration-or-discovery"></a>Configurazione o Individuazione

Dopo aver specificato l'app Web e l'app nativa nella pagina App, la procedura guidata per i servizi di Azure visualizza una pagina **Configurazione** o una pagina **Individuazione**, a seconda del servizio a cui ci si connette. I dettagli di questa pagina variano a seconda del servizio. Per altre informazioni, vedere uno degli articoli seguenti:  

-   Servizio **Gestione cloud**, pagina **Individuazione**: [Configurare l'individuazione utente di Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

-   Servizio **OMS Connector**, pagina **Configurazione**: [Configurare la connessione a OMS](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#use-the-azure-services-wizard-to-configure-the-connection-to-oms)  

-   Servizio **Connettore Upgrade Readiness**, pagina **Configurazione**: [Usare la procedura guidata per Azure per creare la connessione](/sccm/core/clients/manage/upgrade/upgrade-analytics#use-the-azure-wizard-to-create-the-connection)  

-   Servizio **Microsoft Store per le aziende**, pagina **Configurazione**: [Configurare la sincronizzazione di Microsoft Store per le aziende](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#for-configuration-manager-version-1706-and-later)  


Infine completare la procedura guidata per i servizi di Azure con le pagine Riepilogo, Stato e Completamento. La configurazione di un servizio di Azure in Configuration Manager è completata. Ripetere questo processo per configurare altri servizi di Azure.


## <a name="view-the-configuration-of-an-azure-service"></a>Visualizzare la configurazione di un servizio di Azure
È possibile visualizzare le proprietà di un servizio di Azure configurato per l'uso. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare **Servizi di Azure**. Selezionare il servizio che si vuole visualizzare o modificare e fare clic su **Proprietà**.

Se si seleziona un servizio e quindi si fa clic su **Elimina** nella barra multifunzione, viene eliminata la connessione in Configuration Manager. L'app in Azure AD non viene eliminata. Chiedere all'amministratore di Azure di eliminare l'app quando non è più necessaria. In alternativa eseguire la procedura guidata per i servizi di Azure per importare l'app.<!--483440-->


## <a name="cloud-management-data-flow"></a>Flusso di dati per la gestione cloud

Il diagramma seguente è un flusso di dati concettuale per l'interazione tra Configuration Manager, Azure AD e i servizi cloud connessi. Questo esempio specifico usa il servizio **Gestione cloud**, che include un client Windows 10 e app sia server che client. I flussi per altri servizi sono simili.

![Diagramma di flusso di dati per Configuration Manager con Azure AD e gestione cloud](media/aad-auth.png)

1.  L'amministratore di Configuration Manager importa o crea le app client e server in Azure AD.  

2.  Viene eseguito il metodo di individuazione utenti di Azure AD Configuration Manager. Il sito usa il token dell'app server di Azure AD per il rilevamento di oggetti utente in Microsoft Graph.  

3.  Il sito archivia dati sugli oggetti utente. Per altre informazioni, vedere [Individuazione utente Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).  

4.  Il client Configuration Manager richiede il token utente di Azure AD. Il client esegue l'attestazione mediante l'ID applicazione dell'app client di Azure AD, con l'app server come gruppo di destinatari. Per altre informazioni, vedere [Claims in Azure AD Security Tokens](/azure/active-directory/develop/active-directory-authentication-scenarios#claims-in-azure-ad-security-tokens) (Attestazioni nei token di sicurezza di Azure AD).  

5.  Il client esegue l'autenticazione con il sito presentando il token Azure AD a Cloud Management Gateway e/o al punto di gestione locale abilitato per HTTPS.  



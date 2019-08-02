---
title: Risolvere i problemi di analisi del desktop
titleSuffix: Configuration Manager
description: Dettagli tecnici che consentono di risolvere i problemi relativi a desktop Analytics.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1ecb1657903fd3d1dfe43f2ad46258b4643c2f55
ms.sourcegitcommit: ef7800a294e5db5d751921c34f60296c1642fc1f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68712598"
---
# <a name="troubleshoot-desktop-analytics"></a>Risolvere i problemi di analisi del desktop

Usare i dettagli in questo articolo per risolvere i problemi relativi a desktop Analytics integrato con Configuration Manager.



## <a name="confirm-prerequisites"></a>Conferma prerequisiti

Molti problemi comuni sono causati da prerequisiti mancanti. Confermare innanzitutto le configurazioni seguenti:

- [Prerequisiti](/sccm/desktop-analytics/overview#prerequisites)  

- [Aggiornamenti componenti Windows](/sccm/desktop-analytics/enroll-devices#update-devices)  

- [Come abilitare la condivisione dei dati, in cui vengono](/sccm/desktop-analytics/enable-data-sharing)trattati gli argomenti seguenti:  

    - Endpoint Internet a cui i client devono connettersi  

    - Autenticazione del server proxy  

    - Livelli di dati di diagnostica  



## <a name="monitor-connection-health"></a>Monitorare l'integrità della connessione

Usare il dashboard di **integrità della connessione** in Configuration Manager per eseguire il drill-down delle categorie in base all'integrità del dispositivo. Nella console di Configuration Manager passare all'area di lavoro **raccolta software** , espandere il nodo **servizio di analisi desktop** e selezionare il dashboard di integrità della **connessione** .  

Per altre informazioni, vedere [monitorare l'integrità della connessione](/sccm/desktop-analytics/monitor-connection-health).


## <a name="log-files"></a>File di log

Per altre informazioni, vedere [file di log per analisi desktop](/sccm/core/plan-design/hierarchy/log-files#desktop-analytics)

A partire da Configuration Manager versione 1906, usare lo strumento **DesktopAnalyticsLogsCollector. ps1** dalla directory di installazione Configuration Manager per risolvere i problemi di analisi del desktop. Esegue alcuni passaggi di base per la risoluzione dei problemi e raccoglie i log rilevanti in un'unica directory di lavoro. Per altre informazioni, vedere [Log Collector](/sccm/desktop-analytics/log-collector).

### <a name="enable-verbose-logging"></a>Abilita la registrazione dettagliata

1. Nel punto di connessione del servizio passare alla chiave del registro di sistema seguente:`HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. Impostare il valore di **LoggingLevel** su`0`  


## <a name="bkmk_AzureADApps"></a>Applicazioni Azure AD

Desktop Analytics aggiunge le applicazioni seguenti ai Azure AD:

- **Microservizio Configuration Manager**: Stabilisce la connessione Configuration Manager con analisi desktop. Questa app non ha requisiti di accesso.  

- **MALogAnalyticsReader**: Recupera i gruppi e i dispositivi OMS creati in Log Analytics. Per ulteriori informazioni, vedere [ruolo applicazione MALogAnalyticsReader](#bkmk_MALogAnalyticsReader).  

Se è necessario effettuare il provisioning di queste app dopo aver completato l'installazione, passare al riquadro **servizi connessi** . Selezionare **Configure Users and Apps Access**ed effettuare il provisioning delle app.  

- **App Azure ad per Configuration Manager**. Se è necessario eseguire il provisioning o risolvere i problemi di connessione dopo aver completato l'installazione, vedere [creare e importare app per Configuration Manager](#create-and-import-app-for-configuration-manager). Questa app richiede **i dati della raccolta cm di scrittura** e **legge i dati della raccolta cm** nell'API del **servizio Configuration Manager** .  


### <a name="create-and-import-app-for-configuration-manager"></a>Creare e importare app per Configuration Manager

Se non è possibile creare l'app Azure AD per Configuration Manager dalla configurazione guidata dei servizi di Azure o se si vuole riusare un'app esistente, è necessario crearla e importarla manualmente. Dopo aver completato il caricamento [iniziale](/sccm/desktop-analytics/set-up#initial-onboarding) nel portale di analisi desktop, seguire questa procedura:

#### <a name="create-app-in-azure-ad"></a>Crea app in Azure AD

1. Aprire il [portale di Azure](https://portal.azure.com) come utente con autorizzazioni di *amministratore globale* , passare a **Azure Active Directory**e selezionare **registrazioni app**. Quindi selezionare **nuova registrazione**.  

2. Nel pannello **Crea** configurare le impostazioni seguenti:  

    - **Nome**: nome univoco che identifica l'app, ad esempio:`Desktop-Analytics-Connection`  

    - **Tipi di account supportati**: **Solo account in questa directory organizzativa (contoso)**

    - **URI di reindirizzamento (facoltativo)** : **Web**  

    <!--     - **Sign-on URL**: this value isn't used by Configuration Manager, but required by Azure AD. Enter a unique and valid URL, for example: `https://configmgrapp`   -->
  
    Selezionare **Registra**.  

3. Selezionare l'app, annotare l'ID dell' **applicazione (client)** e l' **ID della directory (tenant)** . I valori sono GUID utilizzati per configurare la connessione Configuration Manager.  

4. Scegliere **certificati & segreti**dal menu **Gestisci** . Selezionare **nuovo segreto client**. Immettere una **Descrizione**, specificare una durata di scadenza e quindi selezionare **Aggiungi**. Copiare il **valore** della chiave, che viene usato per configurare la connessione Configuration Manager.

    > [!Important]  
    > Questa è l'unica opportunità per copiare il valore della chiave. Se non lo si copia adesso, è necessario creare un'altra chiave.  
    >
    > Salvare il valore della chiave in una posizione sicura.  

5. Scegliere **autorizzazioni API**dal menu **Gestisci** .  

    1. Nel pannello **autorizzazioni API** selezionare **Aggiungi un'autorizzazione**.  

    2. Nel pannello **autorizzazioni API richiesta** passare alle **API utilizzate dall'organizzazione**.  

    3. Cercare e selezionare l'API del **microservizio Configuration Manager** .  

    4. Selezionare il gruppo **Autorizzazioni applicazione** . Espandere **CmCollectionData**e selezionare entrambe le autorizzazioni seguenti: **Scrivere i dati della raccolta cm** e **leggere i dati della raccolta cm**.  

    5. Selezionare **Aggiungi autorizzazioni**.  

6. Nel pannello **autorizzazioni API** selezionare Concedi il **consenso dell'amministratore.** Selezionare **Sì**.  


#### <a name="import-app-in-configuration-manager"></a>Importa app in Configuration Manager

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**. Selezionare **Configura i servizi di Azure** nella barra multifunzione.  

2. Nella pagina **servizi di Azure** della procedura guidata per i servizi di Azure configurare le impostazioni seguenti:  

    - Specificare un **Nome** per l'oggetto in Configuration Manager.  

    - Specificare un parametro facoltativo **Descrizione** per identificare il servizio.  

    - Selezionare **Desktop Analytics** dall'elenco dei servizi disponibili.  
  
   Selezionare **Avanti**.  

3. Nella pagina **app** selezionare l' **ambiente Azure**appropriato. Quindi selezionare **Importa** per l'app Web. Configurare le impostazioni seguenti nella finestra **Importa app** :  

    - **Nome del Tenant Azure ad**: Questo nome è il nome in Configuration Manager  

    - **ID Tenant Azure ad**: **ID directory** copiato da Azure ad  

    - **Client ID** (ID client): **ID applicazione** copiato dall'app Azure ad  

    - **Chiave privata**: **Valore** della chiave copiato dall'app Azure ad  

    - **Scadenza della chiave privata**: Data di scadenza della chiave  

    - **URI ID app**: Questa impostazione deve essere popolata automaticamente con il valore seguente:`https://cmmicrosvc.manage.microsoft.com/`  
  
   Selezionare **Verifica**, quindi fare clic su **OK** per chiudere la finestra Importa app. Selezionare **Avanti** nella pagina app della procedura guidata per i servizi di Azure.  

Per continuare il resto della procedura guidata nella pagina **dati di diagnostica** , vedere [connettersi al servizio](/sccm/desktop-analytics/connect-configmgr#bkmk_connect).

#### <a name="troubleshoot-app-in-configuration-manager"></a>Risolvere i problemi dell'app in Configuration Manager

In caso di problemi durante la creazione o l'importazione dell'app, controllare innanzitutto **SMSAdminUI. log** per l'errore specifico. Controllare quindi le configurazioni seguenti:

- Il tenant è stato registrato correttamente nel servizio desktop Analytics. Per altre informazioni, vedere [How to set up desktop Analytics](/sccm/desktop-analytics/set-up).

- Tutti gli endpoint necessari sono accessibili. Per ulteriori informazioni, vedere [endpoint](/sccm/desktop-analytics/enable-data-sharing#endpoints).

- Assicurarsi che l'utente che accede disponga delle autorizzazioni corrette. Per altre informazioni, vedere [Prerequisiti](/sccm/desktop-analytics/overview#prerequisites).

- Assicurarsi che l'utente possa accedere ad Azure in generale. Questa azione determina se esistono problemi generali di autenticazione Azure AD.

- Controllare i messaggi di stato per il componente **SMS_SERVICE_CONNECTOR** per il ruolo di *lavoro di desktop Analytics*.


### <a name="bkmk_MALogAnalyticsReader"></a>Ruolo applicazione MALogAnalyticsReader

Quando si configura analisi desktop, l'utente acconsente per conto dell'organizzazione. Questo consenso consiste nell'assegnare all'applicazione MALogAnalyticsReader il ruolo di lettore Log Analytics per l'area di lavoro. Questo ruolo applicazione è richiesto da desktop Analytics.

Se si verifica un problema con questo processo durante l'installazione, usare il processo seguente per aggiungere manualmente questa autorizzazione:

1. Passare alla [portale di Azure](https://portal.azure.com)e selezionare **tutte le risorse**. Selezionare l'area di lavoro di tipo **log Analytics**.  

2. Nel menu dell'area di lavoro selezionare **controllo di accesso (IAM)** , quindi selezionare **Aggiungi**.  

3. Nel pannello **Aggiungi autorizzazioni** configurare le impostazioni seguenti:  

    - **Ruolo**: **Lettore**  

    - **Assegnare l'accesso a**: **Azure AD utente, gruppo o applicazione**  

    - **Selezionare**: **MALogAnalyticsReader**  

4. Selezionare **Salva**.

Nel portale viene visualizzata una notifica che ha aggiunto l'assegnazione di ruolo.


## <a name="data-latency"></a>Latenza dei dati

<!-- 3846531 -->
Quando si configura per la prima volta analisi desktop, si registrano nuovi client o si configurano nuovi piani di distribuzione, i report in Configuration Manager e il portale di analisi desktop potrebbero non visualizzare immediatamente i dati completi. Possono essere necessari 2-3 giorni per l'esecuzione dei passaggi seguenti:

- I dispositivi attivi inviano i dati di diagnostica al servizio desktop Analytics
- Il servizio elabora i dati
- Il servizio viene sincronizzato con il sito di Configuration Manager

Quando si sincronizzano le raccolte di dispositivi dalla gerarchia di Configuration Manager a analisi desktop, potrebbe essere necessaria fino a un'ora prima che le raccolte vengano visualizzate nel portale di analisi del desktop. Analogamente, quando si crea un piano di distribuzione in analisi desktop, può essere necessaria fino a un'ora prima che le nuove raccolte associate al piano di distribuzione vengano visualizzate nella gerarchia di Configuration Manager. I siti primari creano le raccolte e il sito di amministrazione centrale si sincronizza con analisi desktop. Configuration Manager possono richiedere fino a 24 ore per valutare e aggiornare l'appartenenza alla raccolta. Per velocizzare il processo, aggiornare manualmente l'appartenenza alla raccolta.<!-- 4984639 -->

> [!Note]
> Per gli aggiornamenti manuali della raccolta in modo da riflettere le modifiche, è necessario innanzitutto sincronizzare il componente SMS_SERVICE_CONNECTOR_M365ADeploymentPlanWorker. L'esecuzione di questo processo può richiedere fino a un'ora. Per ulteriori informazioni, vedere **M365ADeploymentPlanWorker. log**.

All'interno del portale di analisi desktop sono disponibili due tipi di dati: Dati di **diagnostica**e **dati dell'amministratore** :

- **I dati dell'amministratore** fanno riferimento a tutte le modifiche apportate alla configurazione dell'area di lavoro. Ad esempio, quando si modifica la decisione o l' **importanza** dell' **aggiornamento** di un asset, si stanno cambiando i dati dell'amministratore. Queste modifiche hanno spesso un effetto di composizione, in quanto possono modificare lo stato di conformità di un dispositivo con l'asset in questione installato.

- I **dati di diagnostica** fanno riferimento ai metadati di sistema caricati da dispositivi client a Microsoft. Questi dati hanno l'autorità di analisi del desktop. Sono inclusi attributi come l'inventario dei dispositivi e lo stato di sicurezza e aggiornamento delle funzionalità.

Per impostazione predefinita, tutti i dati nel portale di analisi desktop vengono aggiornati automaticamente ogni giorno. Questo aggiornamento include le modifiche apportate ai dati di diagnostica e le eventuali modifiche apportate alla configurazione (dati dell'amministratore). Dovrebbe essere visibile nel portale di analisi desktop entro 08:00 UTC ogni giorno.

Quando si apportano modifiche ai dati dell'amministratore, è possibile attivare un aggiornamento su richiesta dei dati dell'amministratore nell'area di lavoro. Da qualsiasi pagina nel portale di analisi del desktop, aprire il riquadro a comparsa valuta dati:

![Screenshot della scheda del riquadro a comparsa valuta dati nel portale di analisi del desktop](media/data-currency-flyout.png)

Quindi selezionare **Applica modifiche**:

![Screenshot del riquadro a comparsa di valuta dati espanso nel portale di analisi desktop](media/data-currency-flyout-expand.png)

Questo processo richiede in genere tra 15-60 minuti. La durata dipende dalle dimensioni dell'area di lavoro e dall'ambito delle modifiche che necessitano di processi. Quando si richiede un aggiornamento dati su richiesta, non vengono apportate modifiche ai dati di diagnostica.  Per altre informazioni, vedere le [domande frequenti su desktop Analytics](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

Se non vengono visualizzate modifiche aggiornate entro i frame temporali indicati in precedenza, attendere altre 24 ore per l'aggiornamento giornaliero successivo. Se vengono visualizzati ritardi più lunghi, controllare il dashboard dell'integrità dei servizi. Se il servizio viene segnalato come integro, contattare il supporto tecnico Microsoft.<!-- 3896921 -->

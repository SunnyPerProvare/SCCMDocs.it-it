---
title: Risolvere i problemi di Analitica Desktop
titleSuffix: Configuration Manager
description: Dettagli tecnici per risolvere i problemi con Desktop Analitica.
ms.date: 06/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: acaefcf2c505786dcc65fa7c74063765ca2fe0cf
ms.sourcegitcommit: e3c1eb0b75d79c05a750d49354c851d15d5e26a3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/13/2019
ms.locfileid: "67038614"
---
# <a name="troubleshoot-desktop-analytics"></a>Risolvere i problemi di Analitica Desktop

Usare i dettagli in questo articolo per risolvere i problemi con Desktop Analitica integrato con Configuration Manager.



## <a name="confirm-prerequisites"></a>Verificare i prerequisiti

Molti problemi comuni sono causati da prerequisiti mancanti. Prima di tutto verificare le configurazioni seguenti:

- [Prerequisiti](/sccm/desktop-analytics/overview#prerequisites)  

- [Aggiornamenti dei componenti di Windows](/sccm/desktop-analytics/enroll-devices#update-devices)  

- [Come abilitare la condivisione dei dati](/sccm/desktop-analytics/enable-data-sharing), che include gli argomenti seguenti:  

    - Endpoint Internet a cui i client devono connettersi  

    - Autenticazione del server proxy  

    - Livelli di dati di diagnostica  



## <a name="monitor-connection-health"></a>Monitorare l'integrità della connessione

Usare la **integrità della connessione** dashboard in Configuration Manager per eseguire il drill-in categorie dall'integrità del dispositivo. Nella console di Configuration Manager passare ad il **raccolta Software** dell'area di lavoro, espandere il **Desktop Analitica Servicing** nodo e selezionare il **integrità della connessione** cruscotto.  

Per altre informazioni, vedere [monitorare l'integrità della connessione](/sccm/desktop-analytics/monitor-connection-health).


## <a name="log-files"></a>File di registro

Usare file di log seguenti per risolvere i problemi con Desktop Analitica integrato con Configuration Manager.


### <a name="service-connection-point"></a>punto di connessione del servizio

Sono i seguenti file di log nel punto di connessione del servizio nella directory seguente: `C:\Program Files\Configuration Manager\Logs\M365A`:

| Registro | Descrizione |
|---------|---------|
| **M365ADeploymentPlanWorker.log** | Informazioni sulla sincronizzazione di piano di distribuzione dal Desktop Analitica cloud del servizio per Gestione configurazione locale |
| **M365ADeviceHealthWorker.log** | Informazioni sull'integrità del dispositivo caricare da Configuration Manager in Microsoft cloud |
| **M365AUploadWorker.log** | Informazioni sulla raccolta e dispositivo caricare da Configuration Manager in Microsoft cloud |
| **SmsAdminUI.log** | Informazioni sulle attività della console di Configuration Manager, ad esempio la configurazione dei servizi cloud di Azure  |


### <a name="configuration-manager-client"></a>Client di Configuration Manager

File di log seguenti sono nel client di Configuration Manager nella directory seguente: `C:\Windows\CCM\logs`:

| Registro | Descrizione |
|---------|---------|
| **M365AHandler.log** | Informazioni sui criteri di impostazioni Desktop Analitica |


### <a name="enable-verbose-logging"></a>Abilita la registrazione dettagliata

1. Punto di connessione del servizio, passare alla chiave del Registro di sistema seguente: `HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. Impostare il **LogLevel** valore `0`  
3. (Facoltativo) Eseguire il comando SQL seguente sul database del sito:  

    ```SQL
    DELETE FROM M365AProperties WHERE Name = 'M365ATenantUpdateInfo_LastUpdateTime'
    ```

4. Riavviare il **SMS_EXECUTIVE** servizio nel server del sito



## <a name="bkmk_AzureADApps"></a> Applicazioni di Azure AD

Desktop Analitica aggiunge le seguenti applicazioni in Azure AD:

- **Configuration Manager Microservizio**: Connette Configuration Manager con Analitica Desktop. Questa app non include alcun requisito di accesso.  

- **MALogAnalyticsReader**: Recupera i gruppi di OMS e dispositivi creati in Log Analitica. Per altre informazioni, vedere [ruolo applicazione MALogAnalyticsReader](#bkmk_MALogAnalyticsReader).  

Se è necessario eseguire il provisioning di queste App al termine dell'installazione, andare alla **servizi connessi di** riquadro. Selezionare **configurare l'accesso a utenti e app**ed effettuare il provisioning di App.  

- **App di Azure AD per Configuration Manager**. Se è necessario eseguire il provisioning o risolvere i problemi di connessione al termine dell'installazione, vedere [crea e importa un'app per Configuration Manager](#create-and-import-app-for-configuration-manager). Questa app richiede **scrivere i dati della raccolta CM** e **lettura CM raccolta dati** sul **Configuration Manager Service** API.  


### <a name="create-and-import-app-for-configuration-manager"></a>Creare e importare app for Configuration Manager

Se non è possibile creare questa app di Azure AD dalla procedura guidata Configure Azure Services in Configuration Manager, usare la procedura seguente per creare manualmente e importazione dell'app per Configuration Manager.

#### <a name="create-app-in-azure-ad"></a>Creare app in Azure AD

1. Aprire il [portale di Azure](http://portal.azure.com) come utente con autorizzazioni di amministratore aziendale, passare alla **Azure Active Directory**e selezionare **registrazioni per l'App**. Quindi selezionare **registrazione nuova applicazione**.  

2. Nel **Create** panel, configurare le impostazioni seguenti:  

    - **Nome**: un nome univoco che identifica l'app, ad esempio: `Desktop-Analytics-Connection`  

    - **Tipo di applicazione**: **App Web / API**  

    - **URL Sign-on**: questo valore non è usato da Configuration Manager, ma richiesto da Azure AD. Immettere un URL valido e univoco, ad esempio: `https://configmgrapp`  
  
   Selezionare **Create**.  

3. Selezionare l'app e prendere nota di **ID applicazione**. Questo valore è un GUID che viene usato per configurare la connessione di Configuration Manager.  

4. Selezionare **le impostazioni** relativi all'app e quindi selezionare **chiavi**. Nel **password** , quindi immettere un **descrizione chiave**, specificare una scadenza **durata**e quindi selezionare **Salva**. Copia il **valore** della chiave, che consente di configurare la connessione di Configuration Manager.

    > [!Important]  
    > Questa è l'unica possibilità per copiare il valore della chiave. Se si non copiarlo a questo punto, è necessario creare un'altra chiave.  
    >
    > Salvare il valore della chiave in un luogo sicuro.  

5. Nell'app **le impostazioni** Pannello di selezione **autorizzazioni necessarie**.  

    1. Nel **autorizzazioni necessarie** riquadro, seleziona **Aggiungi**.  

    2. Nel **Aggiungi accesso all'API** pannello **selezionare un'API**.  

    3. Cercare il **Microservizio di Configuration Manager** API. Selezionarlo e quindi scegliere **seleziona**.  

    4. Nel **Abilita accesso** pannello, selezionare entrambe le autorizzazioni applicazione: **Scrivere i dati della raccolta CM** e **leggere i dati della raccolta CM**. Quindi scegliere **seleziona**.  

    5. Nel **Aggiungi accesso all'API** Pannello di selezione **eseguita**.  

6. Nel **autorizzazioni necessarie** pagina, selezionare **concedere le autorizzazioni**. Selezionare **Sì**.  

7. Copiare l'ID tenant di Azure AD. Questo valore è un GUID che viene usato per configurare la connessione di Configuration Manager. Selezionare **Azure Active Directory** nel menu principale e quindi selezionare **proprietà**. Copia il **ID Directory** valore.  

#### <a name="import-app-in-configuration-manager"></a>Importa app in Configuration Manager

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**. Selezionare **configurare i servizi Azure** nella barra multifunzione.  

2. Nel **servizi di Azure** pagina della procedura guidata servizi di Azure, configurare le impostazioni seguenti:  

    - Specificare un **Nome** per l'oggetto in Configuration Manager.  

    - Specificare un parametro facoltativo **Descrizione** per identificare il servizio.  

    - Selezionare **Analitica Desktop** dall'elenco dei servizi disponibili.  
  
   Selezionare **Avanti**.  

3. Nel **App** pagina, selezionare un valore appropriato **ambiente Azure**. Quindi selezionare **importazione** per l'app web. Configurare le impostazioni seguenti nel **Importa le app** finestra:  

    - **Nome del Tenant di Azure AD**: Questo nome è il modo in cui file è denominato in Configuration Manager  

    - **ID Tenant di Azure AD**: Il **ID Directory** copiato da Azure AD  

    - **Client ID** (ID client): Il **ID applicazione** copiato dall'app Azure AD  

    - **Chiave privata**: Il tasto **valore** copiato dall'app Azure AD  

    - **Scadenza della chiave privata**: La stessa data di scadenza della chiave  

    - **URI ID app**: Questa impostazione verranno inseriti automaticamente con il valore seguente: `https://cmmicrosvc.manage.microsoft.com/`  
  
   Selezionare **Verify**, quindi selezionare **OK** per chiudere la finestra di Importa le app. Selezionare **successivo** nella pagina App della procedura guidata servizi di Azure.  

Per continuare il resto della procedura guidata di **dati di diagnostica** pagina, vedere [Connect al servizio](/sccm/desktop-analytics/connect-configmgr#bkmk_connect).

#### <a name="troubleshoot-app-in-configuration-manager"></a>Risolvere i problemi di app in Configuration Manager

Se si verificano problemi creando o importando l'app, verificare innanzitutto **Smsadminui** dell'errore specifico. Quindi verificare le configurazioni seguenti:

- È stato correttamente registrato il tenant per il servizio Desktop Analitica. Per altre informazioni, vedere [come configurare Desktop Analitica](/sccm/desktop-analytics/set-up).

- Gli endpoint sono accessibili tutti necessari. Per altre informazioni, vedere [endpoint](/sccm/desktop-analytics/enable-data-sharing#endpoints).

- Assicurarsi che l'utente che esegue l'accesso disponga delle autorizzazioni corrette. Per altre informazioni, vedere [Prerequisiti](/sccm/desktop-analytics/overview#prerequisites).

- Assicurarsi che l'utente può accedere ad Azure in generale. Questa azione determina se sono presenti AD Azure generale problemi di autenticazione.

- Controllare i messaggi di stato per il **SMS_SERVICE_CONNECTOR** componente per quanto riguarda le *ruolo di lavoro di Analitica Desktop*.


### <a name="bkmk_MALogAnalyticsReader"></a> Ruolo applicazione MALogAnalyticsReader

Quando si configura Desktop Analitica, fornire il consenso per conto dell'organizzazione. Questo consenso consiste nell'assegnare l'applicazione MALogAnalyticsReader il ruolo di lettura Log Analitica per l'area di lavoro. Questo ruolo applicazione è richiesto dal Desktop Analitica.

Se si è verificato un problema con questo processo durante l'installazione, usare la seguente procedura per aggiungere manualmente questa autorizzazione:

1. Andare alla [portale di Azure](http://portal.azure.com)e selezionare **tutte le risorse**. Selezionare l'area di lavoro di tipo **Log Analitica**.  

2. Nel menu dell'area di lavoro, selezionare **controllo di accesso (IAM)** , quindi selezionare **Add**.  

3. Nel **aggiungere autorizzazioni** panel, configurare le impostazioni seguenti:  

    - **Ruolo**: **Agente di lettura log Analitica**  

    - **Assegna accesso a**: **Utente, gruppo o applicazione AD Azure**  

    - **Selezionare**: **MALogAnalyticsReader**  

4. Selezionare **Salva**.

Il portale visualizzerà il messaggio una notifica che aggiunto l'assegnazione di ruolo.


## <a name="data-latency"></a>Latenza dei dati

<!-- 3846531 -->
Quando si configura prima Analitica Desktop, i report in Configuration Manager e il portale di Analitica Desktop non risultino dati completi sin da subito. Potrebbero essere necessari 2-3 giorni per i passaggi seguenti si verifichi:

- Dispositivi attivi inviano dati di diagnostica per il servizio Desktop Analitica
- Il servizio elabora i dati
- Il servizio viene sincronizzato con il sito di Configuration Manager

Durante la sincronizzazione di raccolte di dispositivi dalla gerarchia di Configuration Manager per Desktop Analitica, possono volerci fino a 10 minuti per le raccolte da visualizzare nel portale di Analitica Desktop. Analogamente, quando si crea un piano di distribuzione in Desktop Analitica, possono volerci fino a 10 minuti per le nuove raccolte associati al piano di distribuzione venga visualizzato nella gerarchia di Configuration Manager. I siti primari creano le raccolte e il sito di amministrazione centrale si sincronizza con Desktop Analitica.

All'interno del portale di Analitica Desktop, esistono due tipi di dati: **I dati dell'amministratore** e **i dati di diagnostica**:

- **I dati dell'amministratore** fa riferimento a qualsiasi modifica apportata alla configurazione dell'area di lavoro. Ad esempio, quando si modifica un asset **decisioni di aggiornamento** oppure **importanza** che si desidera modificare i dati dell'amministratore. Queste modifiche hanno spesso un effetto di composizione, come è possibile modificare lo stato di conformità di un dispositivo con l'asset in questione è installato.

- **I dati di diagnostica** fa riferimento a metadati di sistema caricati dai dispositivi client per Microsoft. Questi dati consente di creare Desktop Analitica. Include gli attributi, ad esempio inventario dei dispositivi e sicurezza e funzionalità di aggiornare lo stato.

Per impostazione predefinita, tutti i dati di Analitica Desktop portale viene automaticamente aggiornato ogni giorno. Questo aggiornamento include modifiche di dati di diagnostica e le eventuali modifiche apportate alla configurazione (i dati dell'amministratore). Deve essere visibile nel portale di Analitica Desktop da 08 12:00:00 AM UTC ogni giorno.

Quando si apportano modifiche per i dati dell'amministratore, è possibile attivare un aggiornamento su richiesta dei dati di amministratore nell'area di lavoro. Da qualsiasi pagina nel portale di Analitica Desktop, aprire il menu a comparsa valuta i dati:

![Schermata della scheda di controllo flyout valuta i dati nel portale di Analitica Desktop](media/data-currency-flyout.png)

Quindi selezionare **applicare le modifiche**:

![Screenshot del menu a comparsa valuta espanse dei dati nel portale di Analitica Desktop](media/data-currency-flyout-expand.png)

Questo processo richiede in genere compreso tra 15 e 60 minuti. L'intervallo di tempo dipende la dimensione dell'area di lavoro e l'ambito delle modifiche che richiedono i processi. Quando si richiede un aggiornamento dei dati on demand, non risulta in tutte le modifiche ai dati di diagnostica.  Per altre informazioni, vedere la [domande frequenti su Analitica Desktop](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

Se non è possibile visualizzare le modifiche aggiornate entro gli intervalli di tempo indicati in precedenza, attendere un altro 24 ore il successivo aggiornamento giornaliero. Se viene visualizzato a intervalli più lunghi, controllare il dashboard di integrità del servizio. Se il servizio vengono segnalati come integri, contattare il supporto tecnico Microsoft.<!-- 3896921 -->

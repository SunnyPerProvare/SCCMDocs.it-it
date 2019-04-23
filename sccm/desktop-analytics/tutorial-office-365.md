---
title: 'Esercitazione: distribuire Office 365'
titleSuffix: Configuration Manager
description: Un'esercitazione sull'uso di Desktop Analitica e Configuration Manager per distribuire Office 365 a un gruppo pilota.
ms.date: 04/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: tutorial
ms.assetid: 0b2b633a-91d7-4497-8c2a-1fc7aa310bb1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 006a887a3989d7f05b7cf44b13562e644e6f7d94
ms.sourcegitcommit: d23ccf7b95e6c2a6b156975194ebbc375cb5e6ea
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "60124404"
---
# <a name="tutorial-deploy-office-365-to-pilot"></a>Esercitazione: Distribuire Office 365 per contenuto pilota

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Questa esercitazione Usa Desktop Analitica e Configuration Manager per distribuire Office 365 ProPlus in un gruppo pilota. Verrà evidenziato l'integrazione del servizio cloud per offrire informazioni dettagliate per distribuire l'app con il prodotto locale. Usare Desktop Analitica per determinare i dispositivi migliori da inserire in un gruppo pilota. Quindi è possibile usare Configuration Manager per ottenere corrente con Office.

In questa esercitazione, apprenderà come:  

> [!div class="checklist"]  
> * Configurare Desktop Analitica nel portale di Azure  
> * Connettere Configuration Manager e configurare le impostazioni del dispositivo  
> * Creare un piano di distribuzione Desktop Analitica per Office 365 ProPlus  
> * Distribuire Office 365 ProPlus in Configuration Manager nel gruppo pilota  

Se non hai una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare. Quando è configurato correttamente, uso di Desktop Analitica non comporta l'applicazione di eventuali costi di Azure.

Desktop Analitica Usa un' *dell'area di lavoro di Log Analitica* nella sottoscrizione di Azure. Un'area di lavoro è sostanzialmente un contenitore che include informazioni sull'account e semplici informazioni di configurazione per l'account. Per altre informazioni, vedere [gestire le aree di lavoro](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json).



## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare questa esercitazione, accertarsi di avere i prerequisiti seguenti:  

- Una sottoscrizione di Azure attiva con **amministratore società** autorizzazioni  
    
    Per altre informazioni, vedere [prerequisiti di Analitica Desktop](/sccm/desktop-analytics/overview#prerequisites).

- Configuration Manager, versione 1810 con aggiornamento cumulativo 4488598 o versione successiva, con **amministratore completo** ruolo  

- Almeno un dispositivo Windows 10 con le configurazioni seguenti:  

    - Windows 10, versione 1709 o successiva

    - L'aggiornamento di qualità aggiornamento cumulativo più recente di Windows 10  

    - Configuration Manager client versione 1810 con aggiornamento cumulativo 4486457 o versione successiva  

    - Una versione Windows in base al programma di installazione di Office, ad esempio Office 2013  

- Approvazione aziendale per configurare il livello di dati di diagnostica di Windows per **Enhanced (Limited)** nei dispositivi pilota  

    Per altre informazioni, vedere [privacy Desktop Analitica](/sccm/desktop-analytics/privacy).

- Connettività di rete dal dispositivo agli endpoint internet seguenti:

    - `https://v10c.events.data.microsoft.com`  
    - `https://settings-win.data.microsoft.com`  
    - `http://adl.windows.com`  
    - `https://watson.telemetry.microsoft.com`  
    - `https://umwatsonc.events.data.microsoft.com`  
    - `https://ceuswatcab01.blob.core.windows.net`  
    - `https://ceuswatcab02.blob.core.windows.net`  
    - `https://eaus2watcab01.blob.core.windows.net`  
    - `https://eaus2watcab02.blob.core.windows.net`  
    - `https://weus2watcab01.blob.core.windows.net`  
    - `https://weus2watcab02.blob.core.windows.net`  
    - `https://www.msftncsi.com`  
    - `https://www.msftconnecttest.com`  
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://nexusrules.officeapps.live.com`  
    - `https://nexus.officeapps.live.com`  
    - `https://office.pipe.aria.microsoft.com`  
    - `https://graph.windows.net` (al solo ruolo del Server di Configuration Manager)
    - `https://fef.msua06.manage.microsoft.com` (al solo ruolo del Server di Configuration Manager)

    Per altre informazioni, vedere [come abilitare la condivisione per Desktop Analitica dei dati](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

> [!Important]  
> Questi prerequisiti sono ai fini di questa esercitazione. Per altre informazioni sui prerequisiti generali per Desktop Analitica con Configuration Manager, vedere [prerequisiti](/sccm/desktop-analytics/overview#prerequisites).  



## <a name="set-up-desktop-analytics"></a>Configurare Desktop Analytics

Utilizzare questa procedura per accedere al Desktop Analitica e configurarlo nella sottoscrizione. Questa procedura è un processo unico per configurare Desktop Analitica per l'organizzazione.  

1. Aprire il portale di Analitica Desktop nella gestione di dispositivi di Microsoft 365 come utente con **amministratore società** autorizzazioni. Selezionare **avviare**.  

2. Nel **accettare il contratto di servizio** pagina, esaminare il contratto di servizio e selezionare **Accept**.  

3. Nel **confermare la tua iscrizione** pagina, l'elenco di licenze idonee sono per la funzionalità integrità del dispositivo Windows del Desktop Analitica. Selezionare **Avanti** per continuare.  

4. Nel **consentire agli utenti accesso** pagina:

    - **Chcete Desktop Analitica per gestire i ruoli della Directory per gli utenti**: Desktop Analitica assegna automaticamente le **i proprietari dell'area di lavoro** e **collaboratori dell'area di lavoro** Raggruppa per il **Analitica Desktop Administrator** ruolo. Se tali gruppi ha già un **amministratore globale**, non è stata modificata.  

        Se non si seleziona questa opzione, Analitica Desktop aggiunge comunque agli utenti come membri di due gruppi di sicurezza. Oggetto **amministratore globale** deve assegnare manualmente le **Desktop Administrator Analitica** ruolo per gli utenti.  

        Per altre informazioni sull'assegnazione di autorizzazioni del ruolo amministratore in Azure Active Directory e le autorizzazioni assegnate ai **gli amministratori di Desktop Analitica**, vedere [le autorizzazioni del ruolo amministratore in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Desktop Analitica preconfigura due gruppi di sicurezza in Azure Active Directory:  

        - **I proprietari dell'area di lavoro**: Un gruppo di sicurezza per creare e gestire le aree di lavoro. Questi account devono accesso come proprietario della sottoscrizione di Azure.  

        - **I collaboratori dell'area di lavoro**: Un gruppo di sicurezza per creare e gestire i piani di distribuzione nell'area di lavoro. Non è necessario alcun accesso di Azure aggiuntivo.  

        Per aggiungere un utente a entrambi i gruppi, digitare l'indirizzo di posta elettronica o nome nella **immettere l'indirizzo di posta elettronica o nome** sezione del gruppo appropriato. Al termine, selezionare **successivo**.

Il passaggio seguente può essere completato tramite un **proprietario dell'area di lavoro** oppure **collaboratore**. 

5. Nella pagina per **configurare l'area di lavoro**:  

    - Selezionare la sottoscrizione di Azure. 

    - Per usare un'area di lavoro per Desktop Analitica, selezionarlo e continuare con il passaggio successivo.  

    - Per creare un'area di lavoro per Desktop Analitica, selezionare **Aggiungi area di lavoro**.  

        1. Immettere un **nome area di lavoro**.  

        2. Selezionare l'elenco a discesa per **selezionare il nome di sottoscrizione di Azure per l'area di lavoro**, scegliere la sottoscrizione di Azure per l'area di lavoro.  

        3. **Creare un nuovo** gruppo di risorse oppure **Usa esistente**.  

        4. Selezionare il **regione** dall'elenco, quindi selezionare **Add**.  

6. Selezionare un'area di lavoro nuovo o esistente e quindi selezionare **imposta come area di lavoro di Analitica Desktop**.  Quindi selezionare **continuazione** nel **Confirm e concedere l'accesso** finestra di dialogo.  

7. Nella nuova scheda del browser, scegliere un account da usare per l'accesso. Selezionare l'opzione **fornire il consenso per conto dell'organizzazione** e selezionare **Accept**.  

8. Tornare alla pagina al **configurare l'area di lavoro**, selezionare **successivo**.  

9. Nel **ultimi passaggi** pagina, selezionare **passare al Desktop Analitica**. Il portale di Azure Mostra il Desktop Analitica **Home** pagina.  


### <a name="create-an-app-in-azure-ad-for-configuration-manager"></a>Creare un'app in Azure AD per Configuration Manager  

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



## <a name="connect-configuration-manager"></a>Connettere Configuration Manager

Usare questa procedura per aggiornare Configuration Manager, connettersi a Desktop Analitica e configurare le impostazioni del dispositivo. Questa procedura è un processo unico per collegare la gerarchia per il servizio cloud.  


### <a name="update-configuration-manager"></a>Aggiornamento di Configuration Manager

Installare l'aggiornamento cumulativo Configuration Manager versione 1810 (4486457) per supportare l'integrazione con Desktop Analitica. Per altre informazioni su questo aggiornamento, vedere [aggiornamento cumulativo per Configuration Manager current branch, versione 1810](https://support.microsoft.com/help/4486457).

1. Aggiornare il sito con l'aggiornamento cumulativo per la versione 1810. Per altre informazioni, vedere [Installare gli aggiornamenti nella console](/sccm/core/servers/manage/install-in-console-updates).  

2. Aggiornare i client. Per semplificare questo processo, è consigliabile usare l'aggiornamento automatico. Per altre informazioni, vedere [Aggiornare i client](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  


### <a name="connect-to-the-service"></a>Connettersi al servizio

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**. Selezionare **configurare i servizi Azure** nella barra multifunzione.  

2. Nel **servizi di Azure** pagina della procedura guidata servizi di Azure, configurare le impostazioni seguenti:  

    - Specificare una **nome** per l'oggetto in Configuration Manager  

    - Specificare un parametro facoltativo **descrizione** che consentono di identificare il servizio  

    - Selezionare **Analitica Desktop** dall'elenco dei servizi disponibili  
  
   Selezionare **Avanti**.  

3. Nel **App** pagina, selezionare un valore appropriato **ambiente Azure**. Quindi selezionare **importazione** per l'app web. Configurare le impostazioni seguenti nel **Importa le app** finestra:  

    - **Nome del Tenant di Azure AD**: Questo nome è il modo in cui file è denominato in Configuration Manager  

    - **ID Tenant di Azure AD**: Il **ID Directory** copiato da Azure AD  

    - **Client ID** (ID client): Il **ID applicazione** copiato dall'app Azure AD  

    - **Chiave privata**: Il tasto **valore** copiato dall'app Azure AD  

    - **Scadenza della chiave privata**: La stessa data di scadenza della chiave   

    - **URI ID app**: Questa impostazione verranno inseriti automaticamente con il valore seguente: `https://cmmicrosvc.manage.microsoft.com/`  
  
   Selezionare **Verify**, quindi selezionare **OK** per chiudere la finestra di Importa le app. Selezionare **successivo** nella pagina App della procedura guidata servizi di Azure.  

4. Nel **dati di diagnostica** pagina, configurare le impostazioni seguenti:  

    - **ID commerciale**: questo valore verranno inseriti automaticamente con l'ID dell'organizzazione  

    - **A livello di dati di diagnostica di Windows 10**: selezionare almeno **Enhanced (Limited)**  

    - **Consente il nome di dispositivo nei dati di diagnostica**: selezionare **abilitare**  
  
   Selezionare **Avanti**. Il **funzionalità disponibili** pagina Mostra le funzionalità di Analitica Desktop sono disponibile con le impostazioni di dati di diagnostica dalla pagina precedente. Selezionare **Avanti**.  

5. Nel **raccolte** pagina, configurare le impostazioni seguenti:  

    - **Nome visualizzato**: Il portale di Analitica Desktop Visualizza questa connessione di Configuration Manager usando questo nome. Usato per distinguere tra gerarchie diverse. Ad esempio, *lab di test* oppure *produzione*.  

    - **Raccolta di destinazione**: Questa raccolta include tutti i dispositivi che consente di configurare Configuration Manager con l'ID commerciale e le impostazioni di dati di diagnostica. È il set completo di dispositivi che Configuration Manager si connette al servizio Analitica Desktop.  

    - **I dispositivi nella raccolta di destinazione usano un proxy con autenticazione utente per le comunicazioni in uscita**: Per impostazione predefinita, questo valore è **No**. Se necessario nell'ambiente in uso, impostato su **Sì**.  

    - **Selezionare le raccolte specifiche da sincronizzare con Desktop Analitica**: Selezionare **Add** da includere altre raccolte. Queste raccolte sono disponibili nel portale di Analitica Desktop per il raggruppamento con piani di distribuzione. Assicurarsi di includere raccolte di esclusioni pilota e pilota.  

        Queste raccolte comunque eseguita la sincronizzazione le modifiche all'appartenenza. Ad esempio, il piano di distribuzione Usa una raccolta con una regola di appartenenza a Windows 7. Come aggiornare i dispositivi a Windows 10 e Configuration Manager valuta l'appartenenza alla raccolta, tali dispositivi eliminare esplicitamente la raccolta e un piano di distribuzione.  

6. Completare la procedura guidata.  

Configuration Manager crea un criterio delle impostazioni per configurare i dispositivi nella raccolta di destinazione. Questo criterio include le impostazioni di dati di diagnostica per consentire ai dispositivi di inviare dati a Microsoft. Per impostazione predefinita, i client di aggiornano i criteri ogni ora. Dopo aver ricevuto le nuove impostazioni, può essere più diverse ore prima che i dati sono disponibili in Desktop Analitica.

Monitorare la configurazione dei dispositivi per Desktop Analitica. Nella console di Configuration Manager passare ad il **raccolta Software** dell'area di lavoro, espandere il **Microsoft 365 Servicing** nodo e selezionare il **integrità della connessione** dashboard.  

Configuration Manager si sincronizza i piani di distribuzione Desktop Analitica entro 15 minuti di creazione della connessione. Nella console di Configuration Manager passare ad il **raccolta Software** dell'area di lavoro, espandere il **Microsoft 365 Servicing** nodo e selezionare il **piani di distribuzione** nodo.



## <a name="create-a-desktop-analytics-deployment-plan"></a>Creare un piano di distribuzione Desktop Analitica

Utilizzare questa procedura per creare un piano di distribuzione nel Desktop Analitica.

1. Aprire il [portale di Analitica Desktop](https://aka.ms/m365aprod). Usare le credenziali che dispongono di almeno **collaboratori dell'area di lavoro** autorizzazioni.  

2. Selezionare **piani di distribuzione** nel gruppo di gestione.  

3. Nel **piani di distribuzione** riquadro, selezionare **crea**.  

4. Nel **piano di distribuzione crea** riquadro, configurare le impostazioni seguenti:  

    - **Nome**: Pianificare un nome univoco per la distribuzione, ad esempio `Office 365 pilot`  

    - **Prodotti e le versioni**: Selezionare il **Office** prodotto e la versione più recente disponibile consigliato. Ad esempio, **i client di Office 365, versione 1808 (scelta consigliata)**.  

    - **Gruppi di dispositivi**: Selezionare uno o più gruppi e quindi selezionare **imposta come destinazione gruppi**. Gruppi con **sccm** come origine vengono raccolte sincronizzate da Configuration Manager.  

    - **Le regole di conformità**: Queste regole consentono di determinare i dispositivi che soddisfano le condizioni per l'aggiornamento. Selezionare **le applicazioni di Office** e configurare le impostazioni seguenti:  

        - Aggiornamento di Office 365 ProPlus da 32 a 64 bit. Questa impostazione si applica solo ai dispositivi che eseguono una versione a 64 bit di Windows. L'impostazione predefinita è **Sì**.  

        - Durante l'aggiornamento da una versione precedente di Office, lasciare precedenti deprecate le app di Office. Questo comportamento si applica anche se tali App non presenti nella versione più recente di Office. L'impostazione predefinita è **No**.  

        - Bassa installare soglia conteggio per i componenti aggiuntivi di Office. La soglia predefinita è `2%`. Componenti aggiuntivi sotto questa soglia vengono impostati automaticamente su *bassa conteggio installazioni*. Desktop Analitica non convalida questi componenti aggiuntivi durante la fase pilota. 

            Se un componente aggiuntivo viene installato in una percentuale di computer superiore a questa soglia, contrassegna il piano di distribuzione come il componente aggiuntivo *Noteworthy*. È quindi possibile decidere la sua importanza per eseguire il test durante la fase pilota.  

    - **Data completamento**: Scegliere la data che Office deve essere completamente distribuito a tutti i dispositivi di destinazione.  

5. Selezionare **Create**. Il nuovo piano viene visualizzato nell'elenco dei piani di distribuzione relativi in fase di elaborazione. L'elaborazione può richiedere fino a 48 ore prima di procedere al passaggio successivo.  

6. Aprire il piano di distribuzione selezionando il relativo nome.  

7. Nel menu piano di distribuzione, nelle **Prepara** gruppo, selezionare **identificare importanza**.  

    1. Nel **Office Add-ins** scheda, selezionare questa opzione per mostrare solo **non rivisti** asset.  

    2. Selezionare ogni componente aggiuntivo e quindi selezionare **modifica**. È possibile selezionare più di un'app da modificare nello stesso momento.  

    3. Scegliere un livello di priorità dal **importanza** elenco. Se si vuole che Desktop Analitica per convalidare il componente aggiuntivo durante la fase pilota, selezionare **critici** oppure **importante**. Componenti aggiuntivi contrassegnati come non vengono convalidate **importanti non**. Valutare i rischi di compatibilità e altre importanti informazioni piano quando si assegnano livelli di importanza.  

        Quando si assegnano livelli di importanza, è anche possibile scegliere le decisioni relative all'aggiornamento.  

    4. Selezionare **salvare** al termine.  

8. Nel menu piano di distribuzione, nelle **preparazione** gruppo, selezionare **Identify pilota**.  

    1. Esaminare i dispositivi consigliati per il progetto pilota.  

    2. Selezionare ogni dispositivo e selezionare **aggiungere al progetto pilota**. Se non sono d'accordo con la raccomandazione, selezionare **sostituire**.  

        Per altre informazioni su come Desktop Analitica rende questi consigli, selezionare l'icona informazioni nell'angolo superiore destro del **pilota Identify** riquadro.



## <a name="deploy-office-365-in-configuration-manager"></a>Distribuire Office 365 in Configuration Manager

Utilizzare questa procedura per distribuire Office 365 ProPlus in Configuration Manager nel gruppo pilota.

- Se si ha già uno, prima di tutto [creare un'app per Office 365 ProPlus](#bkmk_create-app)  

- [Distribuire l'app](#bkmk_deploy-app) usando il piano di distribuzione Desktop Analitica  

- [Installare l'app](#bkmk_install-app) da Software Center in un dispositivo di destinazione  

<!-- 
- [Monitor](#bkmk_monitor-app) status in Configuration Manager  
 -->

### <a name="bkmk_create-app"></a> Creare un'app per Office 365 ProPlus

1. Nella console di Configuration Manager passare ad il **raccolta Software**e selezionare il **Office 365 Client Management** nodo. Selezionare il **programma di installazione di Office 365** riquadro nel dashboard.  

2. Nel **le impostazioni dell'applicazione** pagina, fornire un **nome** per questa applicazione. Ad esempio, `Office 365 ProPlus`. Facoltativamente, specificare una **descrizione**. Specificare il **percorso dei contenuti** per il file di installazione e quindi selezionare **successivo**.  

3. Nel **impostazioni Office** pagina, selezionare **passare allo strumento di personalizzazione di Office**. Configurare le impostazioni di distribuzione necessari per l'installazione di Office 365:  

    1. Nel **prodotti e le versioni** gruppo, selezionare **Office 365 ProPlus** dall'elenco, selezionare **Add**.  

    2. Nel **linguaggio** gruppo, selezionare la lingua principale.  

    3. Nel **Update e l'aggiornamento** gruppo, assicurarsi che l'impostazione da **disinstallare qualsiasi versione MSI di Office, tra cui Visio e Project** viene **su**.  

    4. Configurare eventuali impostazioni aggiuntive in base alle esigenze dell'organizzazione.  

    5. Al termine, selezionare **revisione** nell'angolo superiore destro. Esaminare le impostazioni configurate e quindi selezionare **Submit**.  

4. Selezionare **Avanti**. Nel **distribuzione** pagina, selezionare **No** per distribuirlo subito. (La procedura successiva Usa il piano di distribuzione Desktop Analitica per la distribuzione). Selezionare **successivo** e completare la procedura guidata.  


### <a name="bkmk_deploy-app"></a> Distribuire Office 365 usando il piano di distribuzione Desktop Analitica

1. Nella console di Configuration Manager passare ad il **raccolta Software**, espandere **Desktop Analitica Servicing**e selezionare il **piani di distribuzione** nodo.  

2. Selezionare il piano di distribuzione pilota di Office 365 e quindi **dettagli piano di distribuzione** nella barra multifunzione.  

3. Nel **pilota stato** riquadro, scegliere **Application** dall'elenco a discesa e quindi selezionare **Distribuisci**.  

4. Nel **generali** pagina della distribuzione guidata del Software, selezionare **Sfoglia** accanto al **Software** campo. Selezionare l'applicazione di Office 365, ad esempio **Office 365 ProPlus**. Selezionare **Avanti**.  

    > [!Note]  
    > Con l'integrazione Analitica Desktop, Configuration Manager crea automaticamente una raccolta per il piano di distribuzione pilota. Possono volerci fino a 10 minuti per questa raccolta per la sincronizzazione prima di usarlo.<!-- 3887891 -->
    >
    > Questa raccolta è riservata per i dispositivi piano di distribuzione Desktop Analitica. Non sono supportate le modifiche manuali a questa raccolta.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Nel **contenuti** pagina, selezionare **Add**e quindi selezionare **punto di distribuzione**. Selezionare un punto di distribuzione disponibili per ospitare il contenuto di installazione e selezionare **OK**. Selezionare quindi **Avanti**.  

6. Nel **impostazioni di distribuzione** pagina, selezionare **successivo** per accettare le impostazioni predefinite. (Un'installazione disponibile).  

7. Nel **pianificazione** pagina, selezionare **successivo** per accettare le impostazioni predefinite. (Presto disponibile).  

8. Nel **esperienza utente** pagina, selezionare **successivo** per accettare le impostazioni predefinite. (Visualizza in Software Center e Mostra solo le notifiche di riavvii del computer).  

9. Nel **gli avvisi** pagina, selezionare **successivo** per accettare le impostazioni predefinite.  

10. Completare la procedura guidata.  


### <a name="bkmk_install-app"></a> Installare Office 365 da Software Center

1. Accedere a un dispositivo che è un membro del piano di distribuzione pilota.  

2. Aprire **Software Center** e installare l'app disponibile per Office 365.  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->


## <a name="next-steps"></a>Passaggi successivi

Passare all'articolo successivo per altre informazioni sui piani di distribuzione Desktop Analitica.
> [!div class="nextstepaction"]  
> [Piani di distribuzione](/sccm/desktop-analytics/about-deployment-plans)

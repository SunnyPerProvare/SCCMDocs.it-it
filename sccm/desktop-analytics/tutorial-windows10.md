---
title: 'Esercitazione: distribuire Windows 10'
titleSuffix: Configuration Manager
description: Un'esercitazione sull'uso di Desktop Analitica e Configuration Manager per distribuire Windows 10 in un gruppo pilota.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: tutorial
ms.assetid: 3e82cd96-0ce0-474a-a597-d65fceadc95a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0700644f9548ea588821141a34abc6d249909cdf
ms.sourcegitcommit: d8cfd0edf2579e2b08a0ca8a0a7b8f53d1e4196f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67463760"
---
# <a name="tutorial-deploy-windows-10-to-pilot"></a>Esercitazione: Distribuire Windows 10 a un gruppo pilota

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Questa esercitazione Usa Desktop Analitica e Configuration Manager per distribuire Windows 10 a un gruppo pilota. Verrà evidenziato l'integrazione del servizio cloud per offrire approfondimenti per la distribuzione di Windows con il prodotto locale. Usare Desktop Analitica per determinare i dispositivi migliori da inserire in un gruppo pilota. Quindi è possibile usare Configuration Manager per ottenere aggiornate su Windows.

In questa esercitazione, apprenderà come:  

> [!div class="checklist"]  
> * Configurare Desktop Analitica nel portale di Azure  
> * Connettere Configuration Manager e configurare le impostazioni del dispositivo  
> * Creare un piano di distribuzione Desktop Analitica per Windows 10  
> * Usare Configuration Manager per distribuire Windows 10 per il gruppo pilota  

Se non hai una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free) prima di iniziare. Quando è configurato correttamente, uso di Desktop Analitica non comporta l'applicazione di eventuali costi di Azure.

Desktop Analitica Usa un' *dell'area di lavoro di Log Analitica* nella sottoscrizione di Azure. Un'area di lavoro è sostanzialmente un contenitore che include informazioni sull'account e semplici informazioni di configurazione per l'account. Per altre informazioni, vedere [gestire le aree di lavoro](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json).



## <a name="prerequisites"></a>Prerequisiti

Prima di iniziare questa esercitazione, accertarsi di avere i prerequisiti seguenti:  

- Una sottoscrizione di Azure attiva con [ **amministratore globale** ](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator) autorizzazioni  

    Per altre informazioni, vedere [prerequisiti di Analitica Desktop](/sccm/desktop-analytics/overview#prerequisites).

- Configuration Manager, versione 1902 con aggiornamento cumulativo (4500571) o versione successiva, con **amministratore completo** ruolo  

- Supporto di installazione per la versione più recente di Windows 10

- Almeno un dispositivo Windows 10 con le configurazioni seguenti:  

    - Windows 10, versione 1709 o successiva, ma minore di quella dei supporti di installazione si intende usare

    - L'aggiornamento di qualità aggiornamento cumulativo più recente di Windows 10  

    - Configuration Manager client versione 1902 con aggiornamento cumulativo (4500571) o versione successiva  

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
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://graph.windows.net` (in Configuration Manager solo ruolo server)
    - `https://fef.msua06.manage.microsoft.com` (in Configuration Manager solo ruolo server)

    Per altre informazioni, vedere [come abilitare la condivisione per Desktop Analitica dei dati](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

> [!Important]  
> Questi prerequisiti sono ai fini di questa esercitazione. Per altre informazioni sui prerequisiti generali per Desktop Analitica con Configuration Manager, vedere [prerequisiti](/sccm/desktop-analytics/overview#prerequisites).  



## <a name="set-up-desktop-analytics"></a>Configurare Desktop Analytics

Utilizzare questa procedura per accedere al Desktop Analitica e configurarlo nella sottoscrizione. Questa procedura è un processo unico per configurare Desktop Analitica per l'organizzazione.  

1. Aprire il [portale Desktop Analitica](https://aka.ms/desktopanalytics) in Gestione dei dispositivi Microsoft 365 come utente con **amministratore globale** autorizzazioni. Selezionare **avviare**.  

2. Nel **accettare il contratto di servizio** pagina, esaminare il contratto di servizio e selezionare **Accept**.  

3. Nel **confermare la tua iscrizione** pagina, l'elenco di licenze idonee sono per la funzionalità integrità del dispositivo Windows del Desktop Analitica. Selezionare **Avanti** per continuare.  

4. Nel **consentire agli utenti accesso** pagina:

    - **Consenti Desktop Analitica gestire i ruoli della Directory per tuo conto**: Desktop Analitica assegna automaticamente il **i proprietari dell'area di lavoro** le **Desktop Administrator Analitica** ruolo. Se tali gruppi ha già un **amministratore globale**, non è stata modificata.  

        Se non si seleziona questa opzione, Analitica Desktop ancora consente di aggiungere utenti come membri del gruppo di sicurezza. Oggetto **amministratore globale** deve assegnare manualmente le **Desktop Administrator Analitica** ruolo per gli utenti.  

        Per altre informazioni sull'assegnazione di autorizzazioni del ruolo amministratore in Azure Active Directory e le autorizzazioni assegnate ai **gli amministratori di Desktop Analitica**, vedere [le autorizzazioni del ruolo amministratore in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Desktop Analitica preconfigura i **i proprietari dell'area di lavoro** gruppo di sicurezza in Azure Active Directory per creare e gestire le aree di lavoro e i piani di distribuzione. 

        Per aggiungere un utente al gruppo, digitare l'indirizzo di posta elettronica o nome nella **immettere l'indirizzo di posta elettronica o nome** sezione. Al termine, selezionare **successivo**.

5. Nella pagina per **configurare l'area di lavoro**:  

    > [!Note]  
    > Per completare questo passaggio, le esigenze degli utenti **proprietario dell'area di lavoro** accesso aggiuntiva per la sottoscrizione di Azure e il gruppo di risorse e delle autorizzazioni. Per altre informazioni, vedere [prerequisiti](/sccm/desktop-analytics/overview#prerequisites).  

    - Selezionare la sottoscrizione di Azure.  

    - Per usare un'area di lavoro per Desktop Analitica, selezionarlo e continuare con il passaggio successivo.  

    - Per creare un'area di lavoro per Desktop Analitica, selezionare **Aggiungi area di lavoro**.  

        1. Immettere un **nome area di lavoro**.  

        2. Selezionare l'elenco a discesa per **selezionare il nome di sottoscrizione di Azure per l'area di lavoro**, scegliere la sottoscrizione di Azure per l'area di lavoro.  

        3. **Creare un nuovo** gruppo di risorse oppure **Usa esistente**.  

        4. Selezionare il **regione** dall'elenco, quindi selezionare **Add**.  

6. Selezionare un'area di lavoro nuovo o esistente e quindi selezionare **imposta come area di lavoro di Analitica Desktop**.  Quindi selezionare **continuazione** nel **Confirm e concedere l'accesso** finestra di dialogo.  

7. Nella nuova scheda del browser, scegliere un account da usare per l'accesso. Selezionare l'opzione **fornire il consenso per conto dell'organizzazione** e selezionare **Accept**.  


    > [!Note]  
    > Questo consenso consiste nell'assegnare l'applicazione MALogAnalyticsReader il ruolo di lettura Log Analitica per l'area di lavoro. Questo ruolo applicazione è richiesto dal Desktop Analitica. Per altre informazioni, vedere [ruolo applicazione MALogAnalyticsReader](/sccm/desktop-analytics/troubleshooting#bkmk_MALogAnalyticsReader).  

8. Tornare alla pagina al **configurare l'area di lavoro**, selezionare **successivo**.  

9. Nel **ultimi passaggi** pagina, selezionare **passare al Desktop Analitica**. Il portale di Azure Mostra il Desktop Analitica **Home** pagina.  



## <a name="connect-configuration-manager"></a>Connettere Configuration Manager

Usare questa procedura per aggiornare Configuration Manager, connettersi a Desktop Analitica e configurare le impostazioni del dispositivo. Questa procedura è un processo unico per collegare la gerarchia per il servizio cloud.  

### <a name="update-configuration-manager"></a>Aggiornamento di Configuration Manager

Installare l'aggiornamento cumulativo Configuration Manager versione 1902 (4500571) per supportare l'integrazione con Desktop Analitica. Per altre informazioni su questo aggiornamento, vedere [aggiornamento cumulativo per Configuration Manager current branch, versione 1902](https://support.microsoft.com/help/4500571).

1. Aggiornare il sito con l'aggiornamento cumulativo per la versione 1902. Per altre informazioni, vedere [Installare gli aggiornamenti nella console](/sccm/core/servers/manage/install-in-console-updates).  

2. Aggiornare i client. Per semplificare questo processo, è consigliabile usare l'aggiornamento automatico. Per altre informazioni, vedere [Aggiornare i client](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  


### <a name="connect-to-the-service"></a>Connettersi al servizio

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**. Selezionare **configurare i servizi Azure** nella barra multifunzione.  

2. Nel **servizi di Azure** pagina della procedura guidata servizi di Azure, configurare le impostazioni seguenti:  

    - Specificare una **nome** per l'oggetto in Configuration Manager  

    - Specificare un parametro facoltativo **descrizione** che consentono di identificare il servizio  

    - Selezionare **Analitica Desktop** dall'elenco dei servizi disponibili  
  
   Selezionare **Avanti**.  

3. Nel **App** pagina, selezionare un valore appropriato **ambiente Azure**. Quindi selezionare **esplorare** per l'app web.

4. Selezionare **Create** aggiungere con facilità un'app di Azure AD per la connessione di Desktop Analitica.

5. Configurare le impostazioni seguenti nel **crea un'applicazione Server** finestra:  

    - **Nome applicazione**: Un nome descrittivo per l'app di Azure AD.

    - **URL della home page**: questo valore non viene usato da Configuration Manager, ma è richiesto da Azure AD. Per impostazione predefinita, questo valore è impostato su `https://ConfigMgrService`.  

    - **URI ID app**: questo valore deve essere univoco nel tenant di Azure AD. Nel token di accesso utilizzato dal client di Configuration Manager per richiedere l'accesso al servizio. Per impostazione predefinita, questo valore è impostato su `https://ConfigMgrService`.  

    - **Periodo di validità della chiave privata**: scegliere **1 anno** o **2 anni** dall'elenco a discesa. Il valore predefinito è 1 anno.  

    Selezionare **Accedi**. Dopo l'autenticazione in Azure, nella pagina viene visualizzato il **Nome del tenant di Azure AD** come riferimento.

    > [!Note]  
    > Completare questo passaggio come un **amministratore globale**. Queste credenziali non vengono memorizzate in Configuration Manager. Questo utente tipo non richiede autorizzazioni in Configuration Manager e non deve necessariamente essere lo stesso account che esegue la procedura guidata per i servizi di Azure.  

    Selezionare **OK** per creare l'app Web in Azure AD e chiudere la finestra di dialogo Crea un'applicazione server. Nella finestra di dialogo App Server, selezionare **OK**. Quindi selezionare **successivo** nella pagina App della procedura guidata servizi di Azure.  

6. Nel **dati di diagnostica** pagina, configurare le impostazioni seguenti:  

    - **ID commerciale**: questo valore verranno inseriti automaticamente con l'ID dell'organizzazione  

    - **A livello di dati di diagnostica di Windows 10**: selezionare almeno **Enhanced (Limited)**  

    - **Consente il nome di dispositivo nei dati di diagnostica**: selezionare **abilitare**  
  
   Selezionare **Avanti**. Il **funzionalità disponibili** pagina Mostra le funzionalità di Analitica Desktop sono disponibile con le impostazioni di dati di diagnostica dalla pagina precedente. Selezionare **Avanti**.  

7. Nel **raccolte** pagina, configurare le impostazioni seguenti:  

    - **Nome visualizzato**: Il portale di Analitica Desktop Visualizza questa connessione di Configuration Manager usando questo nome. Usato per distinguere tra gerarchie diverse. Ad esempio, *lab di test* oppure *produzione*.  

    - **Raccolta di destinazione**: Questa raccolta include tutti i dispositivi che consente di configurare Configuration Manager con l'ID commerciale e le impostazioni di dati di diagnostica. È il set completo di dispositivi che Configuration Manager si connette al servizio Analitica Desktop.  

    - **I dispositivi nella raccolta di destinazione usano un proxy con autenticazione utente per le comunicazioni in uscita**: Per impostazione predefinita, questo valore è **No**. Se necessario nell'ambiente in uso, impostato su **Sì**.  

    - **Selezionare le raccolte specifiche da sincronizzare con Desktop Analitica**: Selezionare **Add** da includere altre raccolte. Queste raccolte sono disponibili nel portale di Analitica Desktop per il raggruppamento con piani di distribuzione. Assicurarsi di includere raccolte di esclusioni pilota e pilota.  

        Queste raccolte comunque eseguita la sincronizzazione le modifiche all'appartenenza. Ad esempio, il piano di distribuzione Usa una raccolta con una regola di appartenenza a Windows 7. Come aggiornare i dispositivi a Windows 10 e Configuration Manager valuta l'appartenenza alla raccolta, tali dispositivi eliminare esplicitamente la raccolta e un piano di distribuzione.  

8. Completare la procedura guidata.  

Configuration Manager crea un criterio delle impostazioni per configurare i dispositivi nella raccolta di destinazione. Questo criterio include le impostazioni di dati di diagnostica per consentire ai dispositivi di inviare dati a Microsoft. Per impostazione predefinita, i client di aggiornano i criteri ogni ora. Dopo aver ricevuto le nuove impostazioni, può essere più diverse ore prima che i dati sono disponibili in Desktop Analitica.

> [!Note]  
> Per altre informazioni su queste impostazioni, vedere [delle impostazioni di Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Monitorare la configurazione dei dispositivi per Desktop Analitica. Nella console di Configuration Manager passare ad il **raccolta Software** dell'area di lavoro, espandere il **Desktop Analitica Servicing** nodo e selezionare il **integrità della connessione** cruscotto.  

Configuration Manager si sincronizza raccolte entro 60 minuti dalla creazione della connessione. Nel portale di Analitica Desktop, passare a **pilota globale**e visualizzare le raccolte di dispositivi di Configuration Manager.


## <a name="create-a-desktop-analytics-deployment-plan"></a>Creare un piano di distribuzione Desktop Analitica

Utilizzare questa procedura per creare un piano di distribuzione nel Desktop Analitica.

1. Aprire il [portale di Analitica Desktop](https://aka.ms/desktopanalytics). Usare le credenziali che dispongono di almeno **collaboratori dell'area di lavoro** autorizzazioni.  

2. Selezionare **piani di distribuzione** nel gruppo di gestione.  

3. Nel **piani di distribuzione** riquadro, selezionare **crea**.  

4. Nel **piano di distribuzione crea** riquadro, configurare le impostazioni seguenti:  

    - **Nome**: Pianificare un nome univoco per la distribuzione, ad esempio `Windows 10 pilot`  

    - **Prodotti e le versioni**: Selezionare il **Windows** prodotto e la versione più recente disponibile consigliato. Ad esempio, **Windows 10, versione 1809 (scelta consigliata)** .  

    - **Gruppi di dispositivi**: Selezionare uno o più gruppi dalla scheda di Configuration Manager e quindi selezionare **imposta come destinazione gruppi**. Questi gruppi sono raccolte sincronizzate da Configuration Manager.  

    - **Le regole di conformità**: Queste regole consentono di determinare i dispositivi che soddisfano le condizioni per l'aggiornamento. Selezionare **sistemi operativi WIndows** e configurare le impostazioni seguenti:  

        - **Computer gestiti ottengono automaticamente i driver da Windows Update**: L'impostazione predefinita è **disattivata**, utile quando si distribuisce con Configuration Manager.  

        - **Definire una soglia di conteggio installazione bassa per le app**: L'impostazione predefinita è `2%`. Le app sotto questa soglia vengono impostate automaticamente su *bassa conteggio installazioni*. Desktop Analitica non convalida questi componenti aggiuntivi durante la fase pilota.  

            Se un'app è installata in una percentuale di computer superiore a questa soglia, il piano di distribuzione contrassegna l'app come *Noteworthy*. È quindi possibile decidere la sua importanza per eseguire il test durante la fase pilota.  

    - **Data completamento**: Scegliere la data da cui Windows deve essere completamente distribuito a tutti i dispositivi di destinazione.  

5. Selezionare **Create**. Il nuovo piano viene visualizzato nell'elenco dei piani di distribuzione relativi in fase di elaborazione. Per velocizzare l'elaborazione, richiedere un aggiornamento dei dati on demand. Per altre informazioni, vedere [domande frequenti su Analitica Desktop](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

6. Aprire il piano di distribuzione selezionando il relativo nome.  

7. Nel menu piano di distribuzione, nelle **Prepara** gruppo, selezionare **identificare importanza**.  

    1. Nel **Apps** scheda, selezionare questa opzione per mostrare solo **non rivisti** asset.  

    2. Selezionare tutte le app e quindi selezionare **modifica**. È possibile selezionare più di un'app da modificare nello stesso momento.  

    3. Scegliere un livello di priorità dal **importanza** elenco. Se si vuole che Desktop Analitica per convalidare l'app durante la fase pilota, selezionare **critici** oppure **importante**. Le app contrassegnate come non vengono convalidate **importanti non**. Valutare la relativa [compatibilità](/sccm/desktop-analytics/compat-assessment) e altre importanti informazioni piano quando si assegnano livelli di importanza.  

        Quando si assegnano livelli di importanza, è anche possibile scegliere le decisioni relative all'aggiornamento.  

    4. Selezionare **salvare** al termine.  

8. Nel menu piano di distribuzione, nelle **preparazione** gruppo, selezionare **Identify pilota**.  

    1. Esaminare i dispositivi consigliati per il progetto pilota.  

    2. Selezionare ogni dispositivo e selezionare **aggiungere al progetto pilota**. Se non sono d'accordo con la raccomandazione, selezionare **sostituire**.  

        Per altre informazioni su come Desktop Analitica rende questi consigli, selezionare l'icona informazioni nell'angolo superiore destro del **pilota Identify** riquadro.



## <a name="deploy-windows-10-in-configuration-manager"></a>Distribuzione di Windows 10 in Configuration Manager

Utilizzare questa procedura per distribuire Windows 10 in Configuration Manager per il gruppo pilota.

- Se si ha già uno, prima di tutto [creare un pacchetto di aggiornamento del sistema operativo per Windows 10](#bkmk_create-package)  

- Se non ne hai già uno, [creare una sequenza di attività di aggiornamento del sistema operativo per Windows 10](#bkmk_create-ts)  

- [Distribuire la sequenza di attività](#bkmk_deploy-ts) usando il piano di distribuzione Desktop Analitica  

- [Installare la sequenza di attività](#bkmk_install-ts) da Software Center in un dispositivo di destinazione  

<!-- 
- [Monitor](#bkmk_monitor-ts) status in Configuration Manager  
 -->

### <a name="bkmk_create-package"></a> Creare un pacchetto di aggiornamento del sistema operativo per Windows 10

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare il nodo **Pacchetti di aggiornamento del sistema operativo**.  

2. Nella scheda **Home** della barra multifunzione, nel gruppo **Crea** selezionare **Aggiungi pacchetto di aggiornamento del sistema operativo**. Questa azione avvia l'Aggiunta guidata del pacchetto di aggiornamento del sistema operativo.  

3. Nel **Zdroj dat** , specificare la rete **percorso** per l'installazione del pacchetto di aggiornamento file di origine del sistema operativo. Ad esempio, `\\server\share\path`.  

    > [!NOTE]  
    > I file di origine dell'installazione contengono Setup.exe e altri file e cartelle per installare il sistema operativo.  

4. Nel **generali** , specificare un valore univoco **nome** pacchetto di aggiornamento per il sistema operativo.  

5. Completare l'aggiunta guidata pacchetto di aggiornamento del sistema operativo.  

#### <a name="distribute-content"></a>Distribuire il contenuto

Quindi distribuire il pacchetto di aggiornamento del sistema operativo ai punti di distribuzione.  

1. Selezionare il pacchetto di aggiornamento del sistema operativo nell'elenco. Nella scheda **Home** della barra multifunzione selezionare **Distribuisci contenuto** nel gruppo **Distribuzione**. Viene visualizzata la Distribuzione guidata contenuto.  

2. Nel **generali** pagina, verificare che il contenuto elencato sia il contenuto che si desidera distribuire e quindi selezionare **successivo**.  

3. Nel **destinazione contenuto** pagina, selezionare **Add**e scegliere **punto di distribuzione**. Selezionare un punto di distribuzione esistente e quindi selezionare **OK**. Dopo aver aggiunto le destinazioni del contenuto, selezionare **successivo**.  

4. Completare la distribuzione guidata contenuto.  


### <a name="bkmk_create-ts"></a> Creare una sequenza di attività di aggiornamento del sistema operativo per Windows 10

1. Nella console di Configuration Manager passare ad il **raccolta Software** dell'area di lavoro, espandere **sistemi operativi**e quindi selezionare **sequenze di attività**.  

2. Nel **Home** della barra multifunzione, nella **Create** gruppo, selezionare **Crea sequenza di attività**.  

3. Nel **crea una nuova sequenza di attività** pagina della finestra di creazione guidata sequenza attività, selezionare **aggiornare un sistema operativo da un pacchetto di aggiornamento**e quindi selezionare **Avanti**.  

4. Nel **informazioni sequenza di attività** , specificare un **nome sequenza di attività** che identifica la sequenza di attività.  

5. Nel **aggiornare il sistema operativo di Windows** pagina, specificare le impostazioni seguenti e quindi selezionare **successivo**:  

    - **Pacchetto di aggiornamento**: specificare il pacchetto di aggiornamento che contiene i file di origine per l'aggiornamento del sistema operativo.  

    - **Indice dell'edizione**: se nel pacchetto sono disponibili più indici dell'edizione del sistema operativo, selezionare l'indice dell'edizione desiderato. Per impostazione predefinita, la procedura guidata seleziona il primo indice.  

    - **Codice Product Key**: specificare il codice Product Key Windows per il sistema operativo da installare. Specificare i codici Product Key per contratti multilicenza codificati o i codici Product Key standard. Se si usa un codice Product Key standard, separare ogni gruppo di cinque caratteri con un trattino (-). Ad esempio: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Se l'aggiornamento è per un'edizione per contratti multilicenza, il codice Product Key potrebbe non essere obbligatorio.  

        > [!Note]  
        > Questo codice Product Key può essere un codice ad attivazione multipla (MAK) o un codice generico di contratti multilicenza (GVLK). Un codice GVLK è anche definito codice di configurazione client del servizio di gestione delle chiavi (KMS). Per altre informazioni, vedere [Pianificare l'attivazione dei contratti multilicenza](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Per un elenco di codici di configurazione client KMS, vedere l'[Appendice A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) della Guida di attivazione di Windows Server.

6. Nel **Includi aggiornamenti** pagina, selezionare **successivo** di non installare il software degli aggiornamenti.  

7. Nel **installa applicazioni** pagina, selezionare **successivo** non installare tutte le applicazioni.

8. Completare la creazione guidata sequenza di attività.  


### <a name="bkmk_deploy-ts"></a> Distribuire la sequenza di attività usando il piano di distribuzione Desktop Analitica

1. Nella console di Configuration Manager passare ad il **raccolta Software**, espandere **Desktop Analitica Servicing**e selezionare il **piani di distribuzione** nodo.  

2. Selezionare il piano di distribuzione pilota di Windows 10 e quindi selezionare **dettagli piano di distribuzione** nella barra multifunzione.  

3. Nel **distribuzione pilota di stato** riquadro, scegliere **Sequenza_attività** dall'elenco a discesa e quindi selezionare **Distribuisci**.  

4. Nel **generali** pagina della distribuzione guidata del Software, selezionare **Sfoglia** accanto al **Software** campo. Selezionare la sequenza di attività di aggiornamento sul posto di Windows 10 e selezionare **successivo**.  

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


### <a name="bkmk_install-ts"></a> Installare la sequenza di attività da Software Center

1. Accedere a un dispositivo che è un membro del piano di distribuzione pilota.  

2. Aprire **Software Center** e installare il sistema operativo disponibile per Windows 10.  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->


## <a name="next-steps"></a>Passaggi successivi

Passare all'articolo successivo per altre informazioni sui piani di distribuzione Desktop Analitica.
> [!div class="nextstepaction"]  
> [Piani di distribuzione](/sccm/desktop-analytics/about-deployment-plans)

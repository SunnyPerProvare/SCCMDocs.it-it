---
title: Esercitazione-distribuire Windows 10
titleSuffix: Configuration Manager
description: Esercitazione sull'uso di analisi desktop e Configuration Manager per distribuire Windows 10 in un gruppo pilota.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: tutorial
ms.assetid: 3e82cd96-0ce0-474a-a597-d65fceadc95a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c84b5bf720a974bd767db56b9e9da4784caefad1
ms.sourcegitcommit: b64ed4a10a90b93a5bd5454b6efafda90ad45718
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72384681"
---
# <a name="tutorial-deploy-windows-10-to-pilot"></a>Esercitazione: distribuire Windows 10 in progetto pilota

Questa esercitazione usa l'analisi del desktop e Configuration Manager per distribuire Windows 10 in un gruppo pilota. Viene evidenziata l'integrazione del servizio cloud per fornire informazioni dettagliate per la distribuzione di Windows con il prodotto locale. Usare analisi del desktop per determinare i dispositivi più adatti da inserire in un gruppo pilota. Usare quindi Configuration Manager per ottenere la corrente con Windows.

In questa esercitazione si apprenderà come:  

> [!div class="checklist"]  
> * Configurare Desktop Analytics nell'portale di Azure  
> * Connetti Configuration Manager e configura le impostazioni del dispositivo  
> * Creare un piano di distribuzione di desktop Analytics per Windows 10  
> * Usare Configuration Manager per distribuire Windows 10 al gruppo pilota  

Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free) prima di iniziare. Una volta configurata correttamente, l'uso di analisi desktop non comporta costi di Azure.

Desktop Analytics usa un' *area di lavoro log Analytics* nella sottoscrizione di Azure. Un'area di lavoro è essenzialmente un contenitore che include informazioni sull'account e semplici informazioni di configurazione per l'account. Per altre informazioni, vedere [gestire le aree di lavoro](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json).



## <a name="prerequisites"></a>Prerequisites

Prima di iniziare questa esercitazione, verificare che siano soddisfatti i prerequisiti seguenti:  

- Una sottoscrizione di Azure attiva con autorizzazioni di [**amministratore globale**](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions)  

    Per altre informazioni, vedere [prerequisiti di analisi del desktop](/sccm/desktop-analytics/overview#prerequisites).

- Configuration Manager, versione 1902 con aggiornamento cumulativo (4500571) o versione successiva, con ruolo di **amministratore completo**  

- Supporto di installazione per la versione più recente di Windows 10

- Almeno un dispositivo Windows 10 con le configurazioni seguenti:  

    - Windows 10, versione 1709 o successiva, ma inferiore alla versione del supporto di installazione che si prevede di usare

    - Aggiornamento della qualità cumulativa di Windows 10 più recente  

    - Configuration Manager client versione 1902 con aggiornamento cumulativo (4500571) o versione successiva  

- Approvazione aziendale per configurare il livello di dati di diagnostica di Windows su **Enhanced (Limited)** sui dispositivi pilota  

    Per ulteriori informazioni, vedere la pagina relativa alla [privacy di analisi desktop](/sccm/desktop-analytics/privacy).

- Connettività di rete dal dispositivo agli endpoint Internet seguenti:

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
    - `https://graph.windows.net` (solo nel ruolo Server Configuration Manager)
    - `https://*.manage.microsoft.com` (solo nel ruolo Server Configuration Manager)

    Per altre informazioni, vedere [How to Enable Data Sharing for desktop Analytics](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

> [!Important]  
> Questi prerequisiti sono ai fini di questa esercitazione. Per ulteriori informazioni sui prerequisiti generali per desktop Analytics con Configuration Manager, vedere [prerequisiti](/sccm/desktop-analytics/overview#prerequisites).  



## <a name="set-up-desktop-analytics"></a>Configurare Desktop Analytics

Usare questa procedura per accedere a desktop Analytics e configurarlo nella sottoscrizione. Questa procedura è un processo unico per la configurazione di analisi desktop per l'organizzazione.  

1. Aprire il [portale di analisi del desktop](https://aka.ms/desktopanalytics) in Microsoft 365 gestione dei dispositivi come utente con autorizzazioni di **amministratore globale** . Selezionare **Avvia**.  

2. Nella pagina **accetta contratto di servizio** esaminare il contratto di servizio e selezionare **accetta**.  

3. Nella pagina **conferma sottoscrizione** , l'elenco delle licenze idonee necessarie è per le funzionalità di integrità dei dispositivi Windows di desktop Analytics. Selezionare **Avanti** per continuare.  

4. Nella pagina **Give users access** :

    - **Consenti a desktop Analytics di gestire i ruoli della directory per conto dell'utente**: desktop Analytics assegna automaticamente ai proprietari dell'area di **lavoro** il ruolo di **amministratore di desktop Analytics** . Se tali gruppi sono già un **amministratore globale**, non vi sono modifiche.  

        Se non si seleziona questa opzione, desktop Analytics aggiunge ancora gli utenti come membri del gruppo di sicurezza. Un **amministratore globale** deve assegnare manualmente il ruolo di **amministratore di analisi desktop** per gli utenti.  

        Per ulteriori informazioni sull'assegnazione delle autorizzazioni del ruolo amministratore in Azure Active Directory e sulle autorizzazioni assegnate agli **amministratori di desktop Analytics**, vedere autorizzazioni per i [ruoli di amministratore in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Desktop Analytics preconfigura il gruppo di sicurezza **proprietari dell'area di lavoro** in Azure Active Directory per creare e gestire aree di lavoro e piani di distribuzione. 

        Per aggiungere un utente al gruppo, digitarne il nome o l'indirizzo di posta elettronica nella sezione **immettere il nome o l'indirizzo di posta elettronica** . Al termine, selezionare **Avanti**.

5. Nella pagina per **configurare l'area di lavoro**:  

    > [!Note]  
    > Per completare questo passaggio, l'utente deve disporre delle autorizzazioni di **proprietario dell'area di lavoro** e di accesso aggiuntivo alla sottoscrizione e al gruppo di risorse di Azure. Per altre informazioni, vedere i [prerequisiti](/sccm/desktop-analytics/overview#prerequisites).  

    - Selezionare la sottoscrizione di Azure.  

    - Per usare un'area di lavoro esistente per analisi desktop, selezionarla e continuare con il passaggio successivo.  

    - Per creare un'area di lavoro per desktop Analytics, selezionare **Aggiungi area di lavoro**.  

        1. Immettere un **nome**per l'area di lavoro.  

        2. Selezionare l'elenco a discesa per **selezionare il nome della sottoscrizione di Azure per l'area di lavoro**e scegliere la sottoscrizione di Azure per l'area di lavoro.  

        3. **Crea nuovo** Gruppo di risorse o **utilizza esistente**.  

        4. Selezionare l' **area** nell'elenco e quindi selezionare **Aggiungi**.  

6. Selezionare un'area di lavoro nuova o esistente e quindi selezionare **Imposta come area di lavoro di analisi del desktop**.  Quindi selezionare **continua** nella finestra di dialogo **conferma e Concedi accesso** .  

7. Nella scheda nuovo browser selezionare un account da usare per l'accesso. Selezionare l'opzione per il **consenso per conto dell'organizzazione** e selezionare **accetta**.  


    > [!Note]  
    > Questo consenso consiste nell'assegnare all'applicazione MALogAnalyticsReader il ruolo di lettore Log Analytics per l'area di lavoro. Questo ruolo applicazione è richiesto da desktop Analytics. Per ulteriori informazioni, vedere [ruolo applicazione MALogAnalyticsReader](/sccm/desktop-analytics/troubleshooting#bkmk_MALogAnalyticsReader).  

8. Tornare alla pagina per **configurare l'area di lavoro**, quindi fare clic su **Avanti**.  

9. Nella pagina **Last Steps** selezionare **go to desktop Analytics**. Il portale di Azure Mostra la **Home** page di analisi del desktop.  



## <a name="connect-configuration-manager"></a>Connettere Configuration Manager

Usare questa procedura per aggiornare Configuration Manager, connettersi a desktop Analytics e configurare le impostazioni del dispositivo. Questa procedura è un processo monouso per l'associazione della gerarchia al servizio cloud.  

### <a name="update-configuration-manager"></a>Aggiornare Configuration Manager

Installare l'aggiornamento cumulativo di Configuration Manager versione 1902 (4500571) per supportare l'integrazione con desktop Analytics. Per ulteriori informazioni su questo aggiornamento, vedere [aggiornamento cumulativo per Configuration Manager Current Branch, versione 1902](https://support.microsoft.com/help/4500571).

1. Aggiornare il sito con l'aggiornamento cumulativo per la versione 1902. Per altre informazioni, vedere [Installare gli aggiornamenti nella console](/sccm/core/servers/manage/install-in-console-updates).  

2. Aggiornare i client. Per semplificare questo processo, è consigliabile usare l'aggiornamento automatico. Per altre informazioni, vedere [Aggiornare i client](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  


### <a name="connect-to-the-service"></a>Connettersi al servizio

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**. Selezionare **Configura i servizi di Azure** nella barra multifunzione.  

2. Nella pagina **servizi di Azure** della procedura guidata per i servizi di Azure configurare le impostazioni seguenti:  

    - Specificare un **nome** per l'oggetto in Configuration Manager  

    - Specificare una **Descrizione** facoltativa che consenta di identificare il servizio  

    - Selezionare **Desktop Analytics** dall'elenco dei servizi disponibili  
  
   Selezionare **Avanti**.  

3. Nella pagina **app** selezionare l' **ambiente Azure**appropriato. Selezionare quindi **Cerca** nell'app Web.

4. Selezionare **Crea** per aggiungere facilmente un'app Azure ad per la connessione a desktop Analytics.

5. Configurare le impostazioni seguenti nella finestra **Crea applicazione server** :  

    - **Nome applicazione**: nome descrittivo per l'app in Azure ad.

    - **URL della home page**: questo valore non viene usato da Configuration Manager, ma è richiesto da Azure AD. Per impostazione predefinita, questo valore è impostato su `https://ConfigMgrService`.  

    - **URI ID app**: questo valore deve essere univoco nel tenant di Azure AD. Si trova nel token di accesso usato dal client Configuration Manager per richiedere l'accesso al servizio. Per impostazione predefinita, questo valore è impostato su `https://ConfigMgrService`.  

    - **Periodo di validità della chiave privata**: scegliere **1 anno** o **2 anni** dall'elenco a discesa. Il valore predefinito è 1 anno.  

    Selezionare **Sign in (accedi**). Dopo l'autenticazione in Azure, nella pagina viene visualizzato il **Nome del tenant di Azure AD** come riferimento.

    > [!Note]  
    > Completare questo passaggio come **amministratore globale**. Queste credenziali non vengono salvate da Configuration Manager. Questo utente tipo non richiede autorizzazioni in Configuration Manager e non deve necessariamente essere lo stesso account che esegue la procedura guidata per i servizi di Azure.  

    Selezionare **OK** per creare l'app Web in Azure AD e chiudere la finestra di dialogo Crea un'applicazione server. Nella finestra di dialogo app Server selezionare **OK**. Quindi selezionare **Avanti** nella pagina app della procedura guidata per i servizi di Azure.  

6. Nella pagina **dati di diagnostica** configurare le impostazioni seguenti:  

    - **ID commerciale**: questo valore deve essere popolato automaticamente con l'ID dell'organizzazione  

    - **Livello dati di diagnostica di Windows 10**: selezionare almeno **migliorato (limitato)**  

    - **Consenti nome dispositivo nei dati di diagnostica**: selezionare **Abilita**  
  
   Selezionare **Avanti**. La pagina **funzionalità disponibili** Mostra la funzionalità di analisi del desktop disponibile con le impostazioni dei dati di diagnostica della pagina precedente. Selezionare **Avanti**.  

7. Nella pagina **raccolte** configurare le impostazioni seguenti:  

    - **Nome visualizzato**: il portale di analisi del desktop Visualizza questa connessione Configuration Manager usando questo nome. Utilizzarlo per distinguere le diverse gerarchie. Ad esempio, *Lab di test* o *produzione*.  

    - **Raccolta di destinazione**: questa raccolta include tutti i dispositivi che Configuration Manager configura con l'ID commerciale e le impostazioni dei dati di diagnostica. Si tratta del set completo di dispositivi che Configuration Manager si connette al servizio desktop Analytics.  

    - **I dispositivi nella raccolta di destinazione usano un proxy autenticato dall'utente per le comunicazioni in uscita**: per impostazione predefinita, questo valore è **No**. Se necessario nell'ambiente in uso, impostare su **Sì**.  

    - **Selezionare raccolte specifiche da sincronizzare con analisi desktop**: selezionare **Aggiungi** per includere raccolte aggiuntive. Queste raccolte sono disponibili nel portale di analisi del desktop per il raggruppamento con i piani di distribuzione. Assicurarsi di includere le raccolte di esclusioni pilota e pilota.  

        Queste raccolte continuano a essere sincronizzate in seguito alla modifica dell'appartenenza. Il piano di distribuzione, ad esempio, usa una raccolta con una regola di appartenenza di Windows 7. Quando i dispositivi eseguono l'aggiornamento a Windows 10 e Configuration Manager valuta l'appartenenza alla raccolta, tali dispositivi rilasciano il piano di raccolta e di distribuzione.  

8. completare la procedura guidata.  

Configuration Manager crea un criterio di impostazioni per configurare i dispositivi nella raccolta di destinazione. Questo criterio include le impostazioni dei dati di diagnostica per consentire ai dispositivi di inviare dati a Microsoft. Per impostazione predefinita, i client aggiornano i criteri ogni ora. Dopo aver ricevuto le nuove impostazioni, è possibile che si ritrovino diverse ore prima che i dati siano disponibili in desktop Analytics.

> [!Note]  
> Per ulteriori informazioni su queste impostazioni, vedere [impostazioni di Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Monitorare la configurazione dei dispositivi per desktop Analytics. Nella console di Configuration Manager passare all'area di lavoro **raccolta software** , espandere il nodo **servizio di analisi desktop** e selezionare il dashboard di integrità della **connessione** .  

Configuration Manager Sincronizza le raccolte entro 60 minuti dalla creazione della connessione. Nel portale di analisi dei desktop passare a **progetto pilota globale**e visualizzare le raccolte di dispositivi Configuration Manager.


## <a name="create-a-desktop-analytics-deployment-plan"></a>Creare un piano di distribuzione di analisi desktop

Usare questa procedura per creare un piano di distribuzione in desktop Analytics.

1. Aprire il [portale di Analytics per desktop](https://aka.ms/desktopanalytics). Usare le credenziali che dispongono almeno delle autorizzazioni **Collaboratore area di lavoro** .  

2. Selezionare **piani di distribuzione** nel gruppo Gestisci.  

3. Nel riquadro **piani di distribuzione** selezionare **Crea**.  

4. Nel riquadro **crea piano di distribuzione** configurare le impostazioni seguenti:  

    - **Nome**: nome univoco per il piano di distribuzione, ad esempio `Windows 10 pilot`  

    - **Prodotti e versioni**: selezionare il prodotto **Windows** e la versione consigliata disponibile più recente. Ad esempio, **Windows 10, versione 1809 (scelta consigliata)**.  

    - **Gruppi di dispositivi**: selezionare uno o più gruppi dalla scheda Configuration Manager, quindi selezionare **Imposta come gruppi di destinazione**. Questi gruppi sono raccolte sincronizzate da Configuration Manager.  

    - **Regole di conformità**: queste regole consentono di determinare quali dispositivi sono idonei per l'aggiornamento. Selezionare **sistema operativo Windows** e configurare le impostazioni seguenti:  

        - I **computer ricevono automaticamente i driver da Windows Update**: l'impostazione predefinita è **off**, che è consigliabile quando si esegue la distribuzione con Configuration Manager.  

        - **Definire una soglia per il numero di installazioni basso per le app**: l'impostazione predefinita è `2%`. Le app al di sotto di questa soglia vengono impostate automaticamente su *numero minimo di installazioni*. Desktop Analytics non convalida questi componenti aggiuntivi durante il progetto pilota.  

            Se un'app è installata in una percentuale superiore di computer rispetto a questa soglia, il piano di distribuzione contrassegna l'app come *degno*di nota. È quindi possibile decidere la relativa importanza da testare durante la fase pilota.  

    - **Data di completamento**: scegliere la data in cui Windows deve essere distribuito completamente a tutti i dispositivi di destinazione.  

5. Selezionare **Crea**. Il nuovo piano viene visualizzato nell'elenco dei piani di distribuzione durante l'elaborazione. Per velocizzare l'elaborazione, richiedere un aggiornamento dati su richiesta. Per altre informazioni, vedere [domande frequenti su desktop Analytics](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

6. Per aprire il piano di distribuzione, selezionarne il nome.  

7. Nel menu piano di distribuzione, nel gruppo **prepara** , selezionare **identifica importanza**.  

    1. Nella scheda **app** selezionare per visualizzare solo gli asset **non rivisti** .  

    2. Selezionare ogni app e quindi fare clic su **modifica**. È possibile selezionare più app da modificare nello stesso momento.  

    3. Scegliere un livello di importanza dall'elenco di **priorità** . Se si vuole che l'app venga convalidata da desktop Analytics durante il progetto pilota, selezionare **critico** o **importante**. Non convalida le app contrassegnate come **non importanti**. Valutare la [compatibilità](/sccm/desktop-analytics/compat-assessment) e altre informazioni sui piani quando si assegnano livelli di importanza.  

        Quando si assegnano livelli di importanza, è anche possibile scegliere la decisione di aggiornamento.  

    4. Al termine, selezionare **Salva** .  

8. Nel menu piano di distribuzione, nel gruppo **prepara** , selezionare **identifica pilota**.  

    1. Esaminare i dispositivi consigliati per il progetto pilota.  

    2. Selezionare ogni dispositivo e selezionare **Aggiungi a progetto pilota**. Se non si è d'accordo con la raccomandazione, selezionare **Sostituisci**.  

        Per ulteriori informazioni sul modo in cui l'analisi desktop esegue queste raccomandazioni, selezionare l'icona informazioni nell'angolo superiore destro del riquadro **identifica progetto pilota** .



## <a name="deploy-windows-10-in-configuration-manager"></a>Distribuire Windows 10 in Configuration Manager

Usare questa procedura per distribuire Windows 10 in Configuration Manager al gruppo pilota.

- Se non è già presente, creare prima [un pacchetto di aggiornamento del sistema operativo per Windows 10](#bkmk_create-package)  

- Se non ne è già presente uno, [creare una sequenza di attività di aggiornamento del sistema operativo per Windows 10](#bkmk_create-ts)  

- [Distribuire la sequenza di attività](#bkmk_deploy-ts) usando il piano di distribuzione di analisi desktop  

- [Installare la sequenza di attività](#bkmk_install-ts) da software Center in un dispositivo di destinazione  

<!-- 
- [Monitor](#bkmk_monitor-ts) status in Configuration Manager  
 -->

### <a name="bkmk_create-package"></a>Creare un pacchetto di aggiornamento del sistema operativo per Windows 10

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare il nodo **Pacchetti di aggiornamento del sistema operativo**.  

2. Nella scheda **Home** della barra multifunzione, nel gruppo **Crea** selezionare **Aggiungi pacchetto di aggiornamento del sistema operativo**. Questa azione avvia l'Aggiunta guidata del pacchetto di aggiornamento del sistema operativo.  

3. Nella pagina **origine dati** specificare il **percorso** di rete dei file di origine dell'installazione del pacchetto di aggiornamento del sistema operativo. Ad esempio, `\\server\share\path`.  

    > [!NOTE]  
    > I file di origine dell'installazione contengono Setup.exe e altri file e cartelle per installare il sistema operativo.  

4. Nella pagina **generale** specificare un **nome** univoco per il pacchetto di aggiornamento del sistema operativo.  

5. Completare la procedura guidata Aggiungi pacchetto di aggiornamento del sistema operativo.  

#### <a name="distribute-content"></a>Distribuire il contenuto

Quindi distribuire il pacchetto di aggiornamento del sistema operativo ai punti di distribuzione.  

1. Selezionare il pacchetto di aggiornamento del sistema operativo nell'elenco. Nella scheda **Home** della barra multifunzione selezionare **Distribuisci contenuto** nel gruppo **Distribuzione**. Viene visualizzata la Distribuzione guidata contenuto.  

2. Nella pagina **generale** verificare che il contenuto elencato sia il contenuto che si desidera distribuire, quindi selezionare **Avanti**.  

3. Nella pagina **destinazione contenuto** selezionare **Aggiungi**, quindi scegliere punto di **distribuzione**. Selezionare un punto di distribuzione esistente e quindi fare clic su **OK**. Al termine dell'aggiunta di destinazioni contenuto, selezionare **Avanti**.  

4. Completare la distribuzione guidata contenuto.  


### <a name="bkmk_create-ts"></a>Creare una sequenza di attività di aggiornamento del sistema operativo per Windows 10

1. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e quindi selezionare **Sequenze di attività**.  

2. Nella scheda **Home** della barra multifunzione nel gruppo **Crea** selezionare **Crea sequenza di attività**.  

3. Nella pagina **Crea una nuova sequenza di attività** della Creazione guidata della sequenza di attività selezionare **Aggiorna sistema operativo dal pacchetto di aggiornamento** e quindi selezionare **Avanti**.  

4. Nella pagina **informazioni sequenza di attività** specificare un **nome** per la sequenza di attività che identifichi la sequenza di attività.  

5. Nella pagina **Aggiorna sistema operativo Windows** specificare le impostazioni seguenti e quindi selezionare **Avanti**:  

    - **Pacchetto di aggiornamento**: specificare il pacchetto di aggiornamento che contiene i file di origine per l'aggiornamento del sistema operativo.  

    - **Indice edizione**: se sono presenti più indici edizione del sistema operativo nel pacchetto, selezionare l'indice edizione desiderato. Per impostazione predefinita, la procedura guidata seleziona il primo indice.  

    - **Codice Product Key**: specificare il codice Product Key Windows per il sistema operativo da installare. Specificare i codici Product Key per contratti multilicenza codificati o i codici Product Key standard. Se si usa un codice Product Key standard, separare ogni gruppo di cinque caratteri con un trattino (-). Ad esempio: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX* Se l'aggiornamento è per un'edizione per contratti multilicenza, il codice Product Key potrebbe non essere obbligatorio.  

        > [!Note]  
        > Questo codice Product Key può essere un codice ad attivazione multipla (MAK) o un codice generico di contratti multilicenza (GVLK). Un codice GVLK è anche definito codice di configurazione client del servizio di gestione delle chiavi (KMS). Per altre informazioni, vedere [Pianificare l'attivazione dei contratti multilicenza](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Per un elenco di codici di configurazione client KMS, vedere l'[Appendice A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) della Guida di attivazione di Windows Server.

6. Nella pagina **Includi aggiornamenti** selezionare **Avanti** per non installare gli aggiornamenti software.  

7. Nella pagina **installa applicazioni** selezionare **Avanti** per non installare alcuna applicazione.

8. Completare la creazione guidata della sequenza di attività.  


### <a name="bkmk_deploy-ts"></a>Distribuire la sequenza di attività usando il piano di distribuzione di analisi desktop

1. Nella console di Configuration Manager passare alla **raccolta software**, espandere manutenzione di **analisi desktop**e selezionare il nodo piani di **distribuzione** .  

2. Selezionare il piano di distribuzione pilota di Windows 10 e quindi selezionare **Dettagli piano di distribuzione** nella barra multifunzione.  

3. Nel riquadro **stato pilota** scegliere **sequenza attività** dall'elenco a discesa, quindi selezionare **Distribuisci**.  

4. Nella pagina **generale** della distribuzione guidata del software selezionare **Sfoglia** accanto al campo **software** . Selezionare la sequenza di attività di aggiornamento sul posto di Windows 10 e fare clic su **Avanti**.  

    > [!Note]  
    > Con l'integrazione di analisi del desktop, Configuration Manager crea automaticamente raccolte pilota e di produzione per il piano di distribuzione. Prima di poterli usare, la sincronizzazione di queste raccolte può richiedere tempo. Per ulteriori informazioni, vedere [Troubleshoot-latence data](/sccm/desktop-analytics/troubleshooting#data-latency).<!-- 4984639 -->
    >
    > Questa raccolta è riservata ai dispositivi del piano di distribuzione di desktop Analytics. Le modifiche manuali a questa raccolta non sono supportate.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Nella pagina **contenuto** selezionare **Aggiungi**, quindi selezionare **punto di distribuzione**. Selezionare un punto di distribuzione disponibile per ospitare il contenuto di installazione e fare clic su **OK**. Selezionare quindi **Avanti**.  

6. Nella pagina **Impostazioni distribuzione** selezionare **Avanti** per accettare le impostazioni predefinite. (Un'installazione disponibile).  

7. Nella pagina **pianificazione** selezionare **Avanti** per accettare le impostazioni predefinite. (Disponibile appena possibile).  

8. Nella pagina **esperienza utente** selezionare **Avanti** per accettare le impostazioni predefinite. (Visualizza in Software Center e Mostra solo le notifiche per i riavvii del computer).  

9. Nella pagina **avvisi** selezionare **Avanti** per accettare le impostazioni predefinite.  

10. completare la procedura guidata.  


### <a name="bkmk_install-ts"></a>Installare la sequenza di attività da software Center

1. Accedere a un dispositivo che è membro del piano di distribuzione pilota.  

2. Aprire **Software Center** e installare il sistema operativo disponibile per Windows 10.  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->


## <a name="next-steps"></a>Passaggi successivi

Per ulteriori informazioni sui piani di distribuzione di analisi desktop, passare all'articolo successivo.
> [!div class="nextstepaction"]  
> [Piani di distribuzione](/sccm/desktop-analytics/about-deployment-plans)

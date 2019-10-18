---
title: Connettere Configuration Manager
titleSuffix: Configuration Manager
description: Guida alle procedure per la connessione di Configuration Manager con analisi desktop.
ms.date: 07/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 138cf7b8cc6c1279e72d7c620154f703581a9f49
ms.sourcegitcommit: b64ed4a10a90b93a5bd5454b6efafda90ad45718
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72386628"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>Come connettersi Configuration Manager con analisi del desktop

Desktop Analytics è strettamente integrato con Configuration Manager. Prima di tutto, assicurarsi che il sito sia aggiornato per supportare le funzionalità più recenti. Creare quindi la connessione desktop Analytics in Configuration Manager. Infine, monitorare l'integrità della connessione.


## <a name="bkmk_hotfix"></a>Aggiornare il sito

Assicurarsi prima di tutto che il sito Configuration Manager esegua almeno la versione 1902. Per altre informazioni, vedere [Installare gli aggiornamenti nella console](/sccm/core/servers/manage/install-in-console-updates).

È anche necessario installare l'aggiornamento cumulativo versione 1902 (4500571) per supportare l'integrazione con analisi desktop. Per ulteriori informazioni su questo aggiornamento, vedere [aggiornamento cumulativo per Configuration Manager Current Branch, versione 1902](https://support.microsoft.com/help/4500571).

1. Aggiornare il sito con l'aggiornamento cumulativo per la versione 1902. Per altre informazioni, vedere [Installare gli aggiornamenti nella console](/sccm/core/servers/manage/install-in-console-updates).  

2. Aggiornare i client. Per semplificare questo processo, è consigliabile usare l'aggiornamento automatico. Per altre informazioni, vedere [Aggiornare i client](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  



## <a name="bkmk_connect"></a>Connettersi al servizio

Usare questa procedura per connettere Configuration Manager a desktop Analytics e configurare le impostazioni del dispositivo. Questa procedura è un processo monouso per l'associazione della gerarchia al servizio cloud.  

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**. Selezionare **Configura i servizi di Azure** nella barra multifunzione.  

    > [!Tip]  
    > Nella console di Configuration Manager passare all'area di lavoro **raccolta software** e selezionare il nodo **servizio di analisi desktop** . Nella casella *nuovo a desktop Analytics?* selezionare il secondo collegamento per *connettersi Configuration Manager al servizio desktop Analytics*.  

2. Nella pagina **servizi di Azure** della procedura guidata per i servizi di Azure configurare le impostazioni seguenti:  

    - Specificare un **Nome** per l'oggetto in Configuration Manager.  

    - Specificare un parametro facoltativo **Descrizione** per identificare il servizio.  

    - Selezionare **Desktop Analytics** dall'elenco dei servizi disponibili.  
  
   Selezionare **Avanti**.  

3. Nella pagina **app** selezionare l' **ambiente Azure**appropriato. Selezionare quindi **Cerca** nell'app Web.  

4. Se si dispone di un'app esistente che si vuole riutilizzare per questo servizio, selezionarla dall'elenco e selezionare **OK**.  

5. Nella maggior parte dei casi, è possibile creare un'app per la connessione desktop Analytics con questa procedura guidata. Selezionare **Crea**.<!-- 3572123 -->  

    > [!Tip]  
    > Se non è possibile creare l'app da questa procedura guidata, è possibile creare manualmente l'app in Azure AD e quindi importarla nel Configuration Manager. Per altre informazioni, vedere [creare e importare app per Configuration Manager](/sccm/desktop-analytics/troubleshooting#create-and-import-app-for-configuration-manager).  

6. Configurare le impostazioni seguenti nella finestra **Crea applicazione server** :  

    - **Nome applicazione**: nome descrittivo per l'app in Azure ad.

    - **URL della home page**: questo valore non viene usato da Configuration Manager, ma è richiesto da Azure AD. Per impostazione predefinita, questo valore è impostato su `https://ConfigMgrService`.  

    - **URI ID app**: questo valore deve essere univoco nel tenant di Azure AD. Si trova nel token di accesso usato dal client Configuration Manager per richiedere l'accesso al servizio. Per impostazione predefinita, questo valore è impostato su `https://ConfigMgrService`.  

    - **Periodo di validità della chiave privata**: scegliere **1 anno** o **2 anni** dall'elenco a discesa. Il valore predefinito è 1 anno.  

    Selezionare **Sign in (accedi** ). Dopo l'autenticazione in Azure, nella pagina viene visualizzato il **Nome del tenant di Azure AD** come riferimento.
        
    > [!Note]  
    > Completare questo passaggio come **amministratore globale**. Queste credenziali non vengono memorizzate in Configuration Manager. Questo utente tipo non richiede autorizzazioni in Configuration Manager e non deve necessariamente essere lo stesso account che esegue la procedura guidata per i servizi di Azure.  

    Selezionare **OK** per creare l'app Web in Azure AD e chiudere la finestra di dialogo Crea un'applicazione server. Nella finestra di dialogo app Server selezionare **OK**. Quindi selezionare **Avanti** nella pagina app della procedura guidata per i servizi di Azure.  

7. Nella pagina **dati di diagnostica** configurare le impostazioni seguenti:  

    - **ID commerciale**: questo valore deve essere popolato automaticamente con l'ID dell'organizzazione. In caso contrario, assicurarsi che il server proxy sia configurato per consentire tutti gli [endpoint](/sccm/desktop-analytics/enable-data-sharing#endpoints) necessari prima di continuare. In alternativa, recuperare manualmente l'ID commerciale dal [portale di analisi dei desktop](/sccm/desktop-analytics/monitor-connection-health#bkmk_ViewCommercialID).  

    - **Livello dati di diagnostica di Windows 10**: selezionare almeno di **base**. Vedere [livelli di dati di diagnostica](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)
  
    - **Consenti nome dispositivo nei dati di diagnostica**: selezionare **Abilita**  

        > [!Note]  
        > A partire da Windows 10 versione 1803, il nome del dispositivo non viene inviato a Microsoft per impostazione predefinita. Se non si invia il nome del dispositivo, questo viene visualizzato in desktop Analytics come "sconosciuto". Questo comportamento può rendere difficile l'identificazione e la valutazione dei dispositivi.  

   Selezionare **Avanti**. La pagina **funzionalità disponibili** Mostra la funzionalità di analisi del desktop disponibile con le impostazioni dei dati di diagnostica della pagina precedente. Selezionare **Avanti** per continuare o **indietro** per apportare modifiche.  

    ![Pagina della funzionalità di esempio disponibile nella procedura guidata per i servizi di Azure](media/available-functionality.png)

8. Nella pagina **raccolte** configurare le impostazioni seguenti:  

    - **Nome visualizzato**: il portale di analisi del desktop Visualizza questa connessione Configuration Manager usando questo nome. Utilizzarlo per distinguere le diverse gerarchie. Ad esempio, *Lab di test* o *produzione*.  

    - **Raccolta di destinazione**: questa raccolta include tutti i dispositivi che Configuration Manager configura con l'ID commerciale e le impostazioni dei dati di diagnostica. Si tratta del set completo di dispositivi che Configuration Manager si connette al servizio desktop Analytics.  

    - **I dispositivi nella raccolta di destinazione usano un proxy autenticato dall'utente per le comunicazioni in uscita**: per impostazione predefinita, questo valore è **No**. Se necessario nell'ambiente in uso, impostare su **Sì**.  

    - **Selezionare raccolte specifiche da sincronizzare con analisi desktop**: selezionare **Aggiungi** per includere raccolte aggiuntive dalla gerarchia della **raccolta di destinazione** . Queste raccolte sono disponibili nel portale di analisi del desktop per il raggruppamento con i piani di distribuzione. Assicurarsi di includere le raccolte di esclusioni pilota e pilota.  <!-- 4097528 -->  

        > [!Tip]  
        > Nella finestra Seleziona raccolte vengono visualizzate solo le raccolte limitate dalla raccolta di **destinazione**.
        >
        > Nell'esempio seguente si seleziona Collectiona come raccolta di destinazione. Quando si aggiungono altre raccolte, vengono visualizzati Collectiona, CollectionB e CollectionC. Non è possibile aggiungere la raccolta.
        >
        > - Collectiona: limitato dalla raccolta **tutti i sistemi**
        >     - CollectionB: limitato da Collectiona
        >         - CollectionC: limitato da CollectionB
        > - Raccolta: limitata dalla raccolta di **tutti i sistemi**

        > [!Important]  
        > Queste raccolte continuano a essere sincronizzate in seguito alla modifica dell'appartenenza. Il piano di distribuzione, ad esempio, usa una raccolta con una regola di appartenenza di Windows 7. Quando i dispositivi eseguono l'aggiornamento a Windows 10 e Configuration Manager valuta l'appartenenza alla raccolta, tali dispositivi rilasciano il piano di raccolta e di distribuzione.  


9. completare la procedura guidata.  

Configuration Manager crea un criterio di impostazioni per configurare i dispositivi nella raccolta di destinazione. Questo criterio include le impostazioni dei dati di diagnostica per consentire ai dispositivi di inviare dati a Microsoft. Per impostazione predefinita, i client aggiornano i criteri ogni ora. Dopo aver ricevuto le nuove impostazioni, è possibile che si ritrovino diverse ore prima che i dati siano disponibili in desktop Analytics.



## <a name="bkmk_monitor"></a>Monitorare l'integrità della connessione

Monitorare la configurazione dei dispositivi per desktop Analytics. Nella console di Configuration Manager passare all'area di lavoro **raccolta software** , espandere il nodo **servizio di analisi desktop** e selezionare il dashboard di integrità della **connessione** .  

Per altre informazioni, vedere [monitorare l'integrità della connessione](/sccm/desktop-analytics/troubleshooting#monitor-connection-health).

Configuration Manager Sincronizza le raccolte entro 60 minuti dalla creazione della connessione. Nel portale di analisi dei desktop passare a **progetto pilota globale**e visualizzare le raccolte di dispositivi Configuration Manager.



## <a name="next-steps"></a>Passaggi successivi

Passare all'articolo successivo per registrare i dispositivi in desktop Analytics.
> [!div class="nextstepaction"]  
> [Registrare i dispositivi](/sccm/desktop-analytics/enroll-devices)  

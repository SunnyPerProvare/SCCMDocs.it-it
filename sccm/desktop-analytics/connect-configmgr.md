---
title: Connettere Configuration Manager
titleSuffix: Configuration Manager
description: Guida pratica per la connessione di Configuration Manager a Desktop Analytics.
ms.date: 07/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 776c79afea87523fb6da5c92d0b50f128af2a515
ms.sourcegitcommit: edc7a5ad6a2eb72d0448d4689b9534f7e6f4d2b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73623409"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>Come connettere Configuration Manager a Desktop Analytics

Desktop Analytics è strettamente integrato con Configuration Manager. Assicurarsi innanzitutto che il sito sia aggiornato per supportare le funzionalità più recenti. Creare quindi la connessione a Desktop Analytics in Configuration Manager. Infine, monitorare l'integrità della connessione.


## <a name="bkmk_hotfix"></a> Aggiornare il sito

Assicurarsi prima di tutto che il sito di Configuration Manager esegua almeno la versione 1902. Per altre informazioni, vedere [Installare gli aggiornamenti nella console](/sccm/core/servers/manage/install-in-console-updates).

È anche necessario installare l'aggiornamento cumulativo versione 1902 (4500571) per supportare l'integrazione con Desktop Analytics. Per altre informazioni su questo aggiornamento, vedere [Aggiornamento cumulativo per Configuration Manager Current Branch, versione 1902](https://support.microsoft.com/help/4500571).

1. Aggiornare il sito con l'aggiornamento cumulativo per la versione 1902. Per altre informazioni, vedere [Installare gli aggiornamenti nella console](/sccm/core/servers/manage/install-in-console-updates).  

2. Aggiornare i client. Per semplificare questo processo, è consigliabile usare l'aggiornamento automatico. Per altre informazioni, vedere [Aggiornare i client](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  



## <a name="bkmk_connect"></a> Connettersi al servizio

Usare questa procedura per connettere Configuration Manager a Desktop Analytics e configurare le impostazioni del dispositivo. Questa procedura è un processo singolo per l'associazione della gerarchia al servizio cloud.  

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**. Selezionare **Configura i servizi di Azure** nella barra multifunzione.  

    > [!Tip]  
    > Connettersi al servizio direttamente dal nodo **Manutenzione di Desktop Analytics**. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software** e selezionare il nodo **Manutenzione di Desktop Analytics**. Nella casella *Nuovo utente di Desktop Analytics?* selezionare il secondo collegamento *Connettere Configuration Manager al servizio Desktop Analytics*.  

2. Nella pagina **Servizi di Azure** della Procedura guidata per i servizi di Azure configurare le impostazioni seguenti:  

    - Specificare un **Nome** per l'oggetto in Configuration Manager.  

    - Specificare un parametro facoltativo **Descrizione** per identificare il servizio.  

    - Selezionare **Desktop Analytics** dall'elenco dei servizi disponibili.  
  
   Selezionare **Avanti**.  

3. Nella pagina **App** selezionare l'**Ambiente di Azure** appropriato. Quindi selezionare **Sfoglia** per l'app Web.  

4. Se è disponibile un'app che si vuole riutilizzare per questo servizio, selezionarla dall'elenco e selezionare **OK**.  

5. Nella maggior parte dei casi è possibile creare un'app per la connessione a Desktop Analytics con questa procedura guidata. Selezionare **Crea**.<!-- 3572123 -->  

    > [!Tip]  
    > Se non è possibile creare l'app da questa procedura guidata, è possibile creare manualmente l'app in Azure AD e quindi importarla in Configuration Manager. Per altre informazioni, vedere [Creare e importare app per Configuration Manager](/sccm/desktop-analytics/troubleshooting#create-and-import-app-for-configuration-manager).  

6. Configurare le impostazioni seguenti nella finestra **Crea un'applicazione server**:  

    - **Nome applicazione**: nome descrittivo per l'app in Azure AD.

    - **URL della home page**: questo valore non viene usato da Configuration Manager, ma è richiesto da Azure AD. Per impostazione predefinita, questo valore è impostato su `https://ConfigMgrService`.  

    - **URI ID app**: questo valore deve essere univoco nel tenant di Azure AD. È incluso nel token di accesso usato dal client Configuration Manager per richiedere l'accesso al servizio. Per impostazione predefinita, questo valore è impostato su `https://ConfigMgrService`.  

    - **Periodo di validità della chiave privata**: scegliere **1 anno** o **2 anni** dall'elenco a discesa. Il valore predefinito è 1 anno.  

    Selezionare **Accedi**. Dopo l'autenticazione in Azure, nella pagina viene visualizzato il **Nome del tenant di Azure AD** come riferimento.
        
    > [!Note]  
    > Completare questo passaggio come **Amministratore globale**. Queste credenziali non vengono memorizzate in Configuration Manager. Questo utente tipo non richiede autorizzazioni in Configuration Manager e non deve necessariamente essere lo stesso account che esegue la procedura guidata per i servizi di Azure.  

    Selezionare **OK** per creare l'app Web in Azure AD e chiudere la finestra di dialogo Crea un'applicazione server. Nella finestra di dialogo App server selezionare **OK**. Selezionare **Avanti** nella pagina App della Procedura guidata per i servizi di Azure.  

7. Nella pagina **Dati di diagnostica** configurare le impostazioni seguenti:  

    - **ID commerciale**: questo valore deve essere popolato automaticamente con l'ID dell'organizzazione. In caso contrario, assicurarsi che il server proxy sia configurato in modo da consentire tutti gli [endpoint](/sccm/desktop-analytics/enable-data-sharing#endpoints) necessari prima di continuare. In alternativa, recuperare manualmente l'ID commerciale dal [portale di Desktop Analytics](/sccm/desktop-analytics/monitor-connection-health#bkmk_ViewCommercialID).  

    - **Livello dei dati di diagnostica di Windows 10**: selezionare almeno **Base**. Vedere [Livelli dei dati di diagnostica](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)
  
    - **Consenti il nome del dispositivo nei dati di diagnostica**: selezionare **Abilita**  

        > [!Note]  
        > A partire da Windows 10 versione 1803, il nome del dispositivo non viene inviato a Microsoft per impostazione predefinita. Se non si invia il nome del dispositivo, il dispositivo viene visualizzato in Desktop Analytics come "Sconosciuto". Questo comportamento può rendere difficile l'identificazione e la valutazione dei dispositivi.  

   Selezionare **Avanti**. La pagina **Funzionalità disponibile** mostra la funzionalità Desktop Analytics disponibile con le impostazioni dei dati di diagnostica della pagina precedente. Selezionare **Avanti** per continuare o **Precedente** per apportare modifiche.  

    ![Pagina Funzionalità disponibile di esempio nella Procedura guidata per i servizi di Azure](media/available-functionality.png)

8. Nella pagina **Raccolte** configurare le impostazioni seguenti:  

    - **Nome visualizzato**: Il portale di Desktop Analytics visualizza questa connessione a Configuration Manager usando questo nome. Usare il nome per distinguere le diverse gerarchie. Ad esempio, *lab di test* o *produzione*.  

    - **Raccolta di destinazione**: Questa raccolta include tutti i dispositivi che Configuration Manager configura con l'ID commerciale e le impostazioni dei dati di diagnostica. Si tratta del set completo di dispositivi che Configuration Manager connette al servizio Desktop Analytics.  

    - **I dispositivi nella raccolta di destinazione usano un proxy autenticato dall'utente per le comunicazioni in uscita**: Per impostazione predefinita, questo valore è **No**. Se necessario nell'ambiente in uso, impostare su **Sì**.  

    - **Selezionare raccolte specifiche da sincronizzare con Desktop Analytics**: Selezionare **Aggiungi** per inserire ulteriori raccolte della gerarchia **Raccolta di destinazione**. Queste raccolte sono disponibili nel portale di Desktop Analytics per il raggruppamento con i piani di distribuzione. Assicurarsi di includere le raccolte pilota e di esclusioni pilota.  <!-- 4097528 -->  

        > [!Tip]  
        > La finestra Seleziona raccolte visualizza solo le raccolte limitate dalla **Raccolta di destinazione**.
        >
        > Nell'esempio seguente si seleziona CollectionA come raccolta di destinazione. Quando si aggiungono altre raccolte, vengono visualizzate CollectionA, CollectionB e CollectionC. Non è possibile aggiungere CollectionD.
        >
        > - CollectionA: limitata dalla raccolta **Tutti i sistemi**
        >     - CollectionB: limitata da CollectionA
        >         - CollectionC: limitata da CollectionB
        > - CollectionD: limitata dalla raccolta **Tutti i sistemi**

        > [!Important]  
        > Queste raccolte continuano a essere sincronizzate quando viene modifica l'appartenenza. Il piano di distribuzione, ad esempio, usa una raccolta con una regola di appartenenza di Windows 7. Quando i dispositivi eseguono l'aggiornamento a Windows 10 e Configuration Manager valuta l'appartenenza alla raccolta, i dispositivi escono dalla raccolta e dal piano di distribuzione.  


9. Completare la procedura guidata.  

Configuration Manager crea criteri di impostazioni per configurare i dispositivi nella raccolta di destinazione. Questi criteri includono le impostazioni dei dati di diagnostica per abilitare i dispositivi all'invio di dati a Microsoft. Per impostazione predefinita, i client aggiornano i criteri ogni ora. Dopo aver ricevuto le nuove impostazioni, può essere necessario attendere diverse ore prima che i dati siano disponibili in Desktop Analytics.



## <a name="bkmk_monitor"></a> Monitorare l'integrità della connessione

Monitorare la configurazione dei dispositivi per Desktop Analytics. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere il nodo **Manutenzione di Desktop Analytics** e selezionare la dashboard **Integrità connessione**.  

Per altre informazioni, vedere [Monitorare l'integrità della connessione](/sccm/desktop-analytics/troubleshooting#monitor-connection-health).

Configuration Manager sincronizza le raccolte entro 60 minuti dalla creazione della connessione. Nel portale di Desktop Analytics passare a **Pilota globale** e visualizzare le raccolte di dispositivi di Configuration Manager.



## <a name="next-steps"></a>Passaggi successivi

Passare all'articolo successivo per registrare i dispositivi in Desktop Analytics.
> [!div class="nextstepaction"]  
> [Registrare i dispositivi](/sccm/desktop-analytics/enroll-devices)  

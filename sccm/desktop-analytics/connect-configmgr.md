---
title: Connettere Configuration Manager
titleSuffix: Configuration Manager
description: Informazioni di Guida per la connessione di Configuration Manager con Desktop Analitica.
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7925bf44c78b6f8d51797145b5ae463ac3498eea
ms.sourcegitcommit: af207075c4a8bc59242a41d3192a4057452a0e55
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/14/2019
ms.locfileid: "67141060"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>Come connettere Configuration Manager con Desktop Analitica

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Desktop Analitica è strettamente integrato con Configuration Manager. In primo luogo, assicurarsi che il sito viene aggiornato per supportare le funzionalità più recenti. Creare quindi la connessione di Desktop Analitica in Configuration Manager. Infine, monitorare l'integrità della connessione.


## <a name="bkmk_hotfix"></a> Aggiornare il sito

In primo luogo, assicurarsi che il sito di Configuration Manager è in esecuzione almeno versione 1902. Per altre informazioni, vedere [Installare gli aggiornamenti nella console](/sccm/core/servers/manage/install-in-console-updates).

È anche necessario installare l'aggiornamento cumulativo versione 1902 (4500571) per supportare l'integrazione con Desktop Analitica. Per altre informazioni su questo aggiornamento, vedere [aggiornamento cumulativo per Configuration Manager current branch, versione 1902](https://support.microsoft.com/help/4500571).

1. Aggiornare il sito con l'aggiornamento cumulativo per la versione 1902. Per altre informazioni, vedere [Installare gli aggiornamenti nella console](/sccm/core/servers/manage/install-in-console-updates).  

2. Aggiornare i client. Per semplificare questo processo, è consigliabile usare l'aggiornamento automatico. Per altre informazioni, vedere [Aggiornare i client](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  



## <a name="bkmk_connect"></a> Connettersi al servizio

Utilizzare questa procedura per connettere Configuration Manager a Desktop Analitica e configurare le impostazioni del dispositivo. Questa procedura è un processo unico per collegare la gerarchia per il servizio cloud.  

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**. Selezionare **configurare i servizi Azure** nella barra multifunzione.  

    > [!Tip]  
    > Nella console di Configuration Manager passare ad il **raccolta Software** dell'area di lavoro e selezionare il **Desktop Analitica Servicing** nodo. Nel *nuovo per Desktop Analitica?* , selezionare il collegamento al secondo *connettere Configuration Manager per il servizio Desktop Analitica*.  

2. Nel **servizi di Azure** pagina della procedura guidata servizi di Azure, configurare le impostazioni seguenti:  

    - Specificare un **Nome** per l'oggetto in Configuration Manager.  

    - Specificare un parametro facoltativo **Descrizione** per identificare il servizio.  

    - Selezionare **Analitica Desktop** dall'elenco dei servizi disponibili.  
  
   Selezionare **Avanti**.  

3. Nel **App** pagina, selezionare un valore appropriato **ambiente Azure**. Quindi selezionare **esplorare** per l'app web.  

4. Se si dispone di un'app esistente che si desidera riutilizzare per questo servizio, selezionarla dall'elenco e selezionare **OK**.  

5. Nella maggior parte dei casi, è possibile creare un'app per la connessione di Desktop Analitica con questa procedura guidata. Selezionare **Create**.<!-- 3572123 -->  

    > [!Tip]  
    > Se è possibile creare l'app da questa procedura guidata, è possibile creare manualmente l'app di Azure AD e quindi importare in Configuration Manager. Per altre informazioni, vedere [crea e importa un'app per Configuration Manager](/sccm/desktop-analytics/troubleshooting#create-and-import-app-for-configuration-manager).  

6. Configurare le impostazioni seguenti nel **crea un'applicazione Server** finestra:  

    - **Nome applicazione**: Un nome descrittivo per l'app di Azure AD.

    - **URL della home page**: questo valore non viene usato da Configuration Manager, ma è richiesto da Azure AD. Per impostazione predefinita, questo valore è impostato su `https://ConfigMgrService`.  

    - **URI ID app**: questo valore deve essere univoco nel tenant di Azure AD. Nel token di accesso utilizzato dal client di Configuration Manager per richiedere l'accesso al servizio. Per impostazione predefinita, questo valore è impostato su `https://ConfigMgrService`.  

    - **Periodo di validità della chiave privata**: scegliere **1 anno** o **2 anni** dall'elenco a discesa. Il valore predefinito è 1 anno.  

    Selezionare **Accedi** . Dopo l'autenticazione in Azure, nella pagina viene visualizzato il **Nome del tenant di Azure AD** come riferimento.
        
    > [!Note]  
    > Completare questo passaggio come un **amministratore società**. Queste credenziali non vengono memorizzate in Configuration Manager. Questo utente tipo non richiede autorizzazioni in Configuration Manager e non deve necessariamente essere lo stesso account che esegue la procedura guidata per i servizi di Azure.  

    Selezionare **OK** per creare l'app Web in Azure AD e chiudere la finestra di dialogo Crea un'applicazione server. Nella finestra di dialogo App Server, selezionare **OK**. Quindi selezionare **successivo** nella pagina App della procedura guidata servizi di Azure.  

7. Nel **dati di diagnostica** pagina, configurare le impostazioni seguenti:  

    - **ID commerciale**: questo valore verranno inseriti automaticamente con l'ID. dell'organizzazione Se non, assicurarsi che il server proxy sia configurato per consentire tutti obbligatori [endpoint](/sccm/desktop-analytics/enable-data-sharing#endpoints) prima di continuare. In alternativa, recuperare l'ID commerciale manualmente tramite il [portale Analitica Desktop](/sccm/desktop-analytics/monitor-connection-health#bkmk_ViewCommercialID).  

    - **A livello di dati di diagnostica di Windows 10**: selezionare almeno **base**. Vedere [i livelli di dati di diagnostica](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)
  
    - **Consente il nome di dispositivo nei dati di diagnostica**: selezionare **abilitare**  

        > [!Note]  
        > A partire da Windows 10 versione 1803, il nome del dispositivo non viene inviato a Microsoft per impostazione predefinita. Se si non invia il nome del dispositivo, viene visualizzata nel Desktop Analitica come "Sconosciuto". Questo comportamento può rendere difficile identificare e valutare i dispositivi.  

   Selezionare **Avanti**. Il **funzionalità disponibili** pagina Mostra le funzionalità di Analitica Desktop sono disponibile con le impostazioni di dati di diagnostica dalla pagina precedente. Selezionare **successivo** per continuare oppure **Previous** per apportare modifiche.  

    ![Pagina di funzionalità disponibile di esempio della procedura guidata servizi di Azure](media/available-functionality.png)

8. Nel **raccolte** pagina, configurare le impostazioni seguenti:  

    - **Nome visualizzato**: Il portale di Analitica Desktop Visualizza questa connessione di Configuration Manager usando questo nome. Usato per distinguere tra gerarchie diverse. Ad esempio, *lab di test* oppure *produzione*.  

    - **Raccolta di destinazione**: Questa raccolta include tutti i dispositivi che consente di configurare Configuration Manager con l'ID commerciale e le impostazioni di dati di diagnostica. È il set completo di dispositivi che Configuration Manager si connette al servizio Analitica Desktop.  

    - **I dispositivi nella raccolta di destinazione usano un proxy con autenticazione utente per le comunicazioni in uscita**: Per impostazione predefinita, questo valore è **No**. Se necessario nell'ambiente in uso, impostato su **Sì**.  

    - **Selezionare le raccolte specifiche da sincronizzare con Desktop Analitica**: Selezionare **Add** raccolte aggiuntive da includere le **raccolta di destinazione** gerarchia. Queste raccolte sono disponibili nel portale di Analitica Desktop per il raggruppamento con piani di distribuzione. Assicurarsi di includere raccolte di esclusioni pilota e pilota.  <!-- 4097528 -->  

        > [!Important]  
        > Queste raccolte comunque eseguita la sincronizzazione le modifiche all'appartenenza. Ad esempio, il piano di distribuzione Usa una raccolta con una regola di appartenenza a Windows 7. Come aggiornare i dispositivi a Windows 10 e Configuration Manager valuta l'appartenenza alla raccolta, tali dispositivi eliminare esplicitamente la raccolta e un piano di distribuzione.  


9. Completare la procedura guidata.  

Configuration Manager crea un criterio delle impostazioni per configurare i dispositivi nella raccolta di destinazione. Questo criterio include le impostazioni di dati di diagnostica per consentire ai dispositivi di inviare dati a Microsoft. Per impostazione predefinita, i client di aggiornano i criteri ogni ora. Dopo aver ricevuto le nuove impostazioni, può essere più diverse ore prima che i dati sono disponibili in Desktop Analitica.



## <a name="bkmk_monitor"></a> Monitorare l'integrità della connessione

Monitorare la configurazione dei dispositivi per Desktop Analitica. Nella console di Configuration Manager passare ad il **raccolta Software** dell'area di lavoro, espandere il **Desktop Analitica Servicing** nodo e selezionare il **integrità della connessione** cruscotto.  

Per altre informazioni, vedere [monitorare l'integrità della connessione](/sccm/desktop-analytics/troubleshooting#monitor-connection-health).

Configuration Manager si sincronizza raccolte entro 60 minuti dalla creazione della connessione. Nel portale di Analitica Desktop, passare a **pilota globale**e visualizzare le raccolte di dispositivi di Configuration Manager.



## <a name="next-steps"></a>Passaggi successivi

Passare all'articolo successivo per registrare i dispositivi Desktop Analitica.
> [!div class="nextstepaction"]  
> [Registrare i dispositivi](/sccm/desktop-analytics/enroll-devices)  

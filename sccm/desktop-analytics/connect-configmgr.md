---
title: Connettere Configuration Manager
titleSuffix: Configuration Manager
description: Informazioni di Guida per la connessione di Configuration Manager con Desktop Analitica.
ms.date: 04/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 11979d35829660633dd77059562dcf519e0af05b
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62206157"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>Come connettere Configuration Manager con Desktop Analitica

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Desktop Analitica è strettamente integrato con Configuration Manager. In primo luogo, assicurarsi che il sito viene aggiornato per supportare le funzionalità più recenti. Creare quindi la connessione di Desktop Analitica in Configuration Manager. Infine, monitorare l'integrità della connessione.


## <a name="bkmk_hotfix"></a> Aggiornare il sito

In primo luogo, assicurarsi che il sito di Configuration Manager è in esecuzione almeno versione 1810. Per altre informazioni, vedere [Installare gli aggiornamenti nella console](/sccm/core/servers/manage/install-in-console-updates).

È anche necessario installare la versione 1810 aggiornamento cumulativo 2 (4488598) per supportare l'integrazione con Desktop Analitica. Per altre informazioni su questo aggiornamento, vedere [aggiornamento cumulativo 2 per Configuration Manager current branch, versione 1810](https://support.microsoft.com/help/4488598).

1. Aggiornare il sito con l'aggiornamento cumulativo per la versione 1810. Per altre informazioni, vedere [Installare gli aggiornamenti nella console](/sccm/core/servers/manage/install-in-console-updates).  

2. Aggiornare i client. Per semplificare questo processo, è consigliabile usare l'aggiornamento automatico. Per altre informazioni, vedere [Aggiornare i client](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  



## <a name="bkmk_connect"></a> Connettersi al servizio

Utilizzare questa procedura per connettere Configuration Manager a Desktop Analitica e configurare le impostazioni del dispositivo. Questa procedura è un processo unico per collegare la gerarchia per il servizio cloud.  

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

4. Nel **dati di diagnostica** pagina, configurare le impostazioni seguenti:  

    - **ID commerciale**: questo valore verranno inseriti automaticamente con l'ID. dell'organizzazione Se non, assicurarsi che il server proxy sia configurato nell'elenco elementi consentiti tutti i necessari [endpoint](/sccm/desktop-analytics/enable-data-sharing#endpoints) prima di continuare. In alternativa, recuperare l'ID commerciale dal **servizi connessi** riquadro le [portale Analitica Desktop](https://aka.ms/m365aprod).  

    - **A livello di dati di diagnostica di Windows 10**: selezionare almeno **Enhanced (Limited)**  

    - **Consente il nome di dispositivo nei dati di diagnostica**: selezionare **abilitare**  

        > [!Note]  
        > A partire da Windows 10 versione 1803, il nome del dispositivo non viene inviato a Microsoft per impostazione predefinita. Se si non invia il nome del dispositivo, viene visualizzata nel Desktop Analitica come "Sconosciuto". Questo comportamento può rendere difficile identificare e valutare i dispositivi.  

   Selezionare **Avanti**. Il **funzionalità disponibili** pagina Mostra le funzionalità di Analitica Desktop sono disponibile con le impostazioni di dati di diagnostica dalla pagina precedente. Selezionare **successivo** per continuare oppure **Previous** per apportare modifiche.  

    ![Pagina di funzionalità disponibile di esempio della procedura guidata servizi di Azure](media/available-functionality.png)

5. Nel **raccolte** pagina, configurare le impostazioni seguenti:  

    - **Nome visualizzato**: Il portale di Analitica Desktop Visualizza questa connessione di Configuration Manager usando questo nome. Usato per distinguere tra gerarchie diverse. Ad esempio, *lab di test* oppure *produzione*.  

    - **Raccolta di destinazione**: Questa raccolta include tutti i dispositivi che consente di configurare Configuration Manager con l'ID commerciale e le impostazioni di dati di diagnostica. È il set completo di dispositivi che Configuration Manager si connette al servizio Analitica Desktop.  

    - **I dispositivi nella raccolta di destinazione usano un proxy con autenticazione utente per le comunicazioni in uscita**: Per impostazione predefinita, questo valore è **No**. Se necessario nell'ambiente in uso, impostato su **Sì**.  

    - **Selezionare le raccolte specifiche da sincronizzare con Desktop Analitica**: Selezionare **Add** da includere altre raccolte. Queste raccolte sono disponibili nel portale di Analitica Desktop per il raggruppamento con piani di distribuzione. Assicurarsi di includere raccolte di esclusioni pilota e pilota.  

        Queste raccolte comunque eseguita la sincronizzazione le modifiche all'appartenenza. Ad esempio, il piano di distribuzione Usa una raccolta con una regola di appartenenza a Windows 7. Come aggiornare i dispositivi a Windows 10 e Configuration Manager valuta l'appartenenza alla raccolta, tali dispositivi eliminare esplicitamente la raccolta e un piano di distribuzione.  

        > [!Important]  
        > Assicurarsi di limitare queste raccolte aggiuntive per la raccolta di destinazione. Nelle proprietà di queste raccolte aggiuntive, il **raccolta di limitazione** deve essere lo stesso insieme di Desktop Analitica **raccolta di destinazione**.<!-- 4097528 -->  

6. Completare la procedura guidata.  

Configuration Manager crea un criterio delle impostazioni per configurare i dispositivi nella raccolta di destinazione. Questo criterio include le impostazioni di dati di diagnostica per consentire ai dispositivi di inviare dati a Microsoft. Per impostazione predefinita, i client di aggiornano i criteri ogni ora. Dopo aver ricevuto le nuove impostazioni, può essere più diverse ore prima che i dati sono disponibili in Desktop Analitica.



## <a name="bkmk_monitor"></a> Monitorare l'integrità della connessione

Monitorare la configurazione dei dispositivi per Desktop Analitica. Nella console di Configuration Manager passare ad il **raccolta Software** dell'area di lavoro, espandere il **Microsoft 365 Servicing** nodo e selezionare il **integrità della connessione** dashboard.  

Per altre informazioni, vedere [monitorare l'integrità della connessione](/sccm/desktop-analytics/troubleshooting#monitor-connection-health).

Configuration Manager si sincronizza i piani di distribuzione Desktop Analitica entro 15 minuti di creazione della connessione. Nella console di Configuration Manager passare ad il **raccolta Software** dell'area di lavoro, espandere il **Microsoft 365 Servicing** nodo e selezionare il **piani di distribuzione** nodo.



## <a name="next-steps"></a>Passaggi successivi

Passare all'articolo successivo per registrare i dispositivi Desktop Analitica.
> [!div class="nextstepaction"]  
> [Registrare i dispositivi](/sccm/desktop-analytics/enroll-devices)  

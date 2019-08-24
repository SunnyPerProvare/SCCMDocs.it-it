---
title: Domande frequenti su desktop Analytics
titleSuffix: Configuration Manager
description: Domande frequenti su desktop Analytics.
ms.date: 08/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 84cbcd11790ebf83b508a3db167efc7c02152652
ms.sourcegitcommit: e2e07d74779a2f48693ecaa17a5974204949d109
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/23/2019
ms.locfileid: "69999379"
---
# <a name="desktop-analytics-faq"></a>Domande frequenti su desktop Analytics

> [!Note]  
> Queste informazioni si riferiscono a un servizio di anteprima che può essere modificato in modo sostanziale prima del rilascio commerciale. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

## <a name="prerequisites"></a>Prerequisiti 

### <a name="can-i-use-desktop-analytics-with-intune-managed-devices"></a>È possibile usare analisi desktop con i dispositivi gestiti da Intune? 

La maggior parte dei clienti che possono trarre vantaggio dal flusso di lavoro di analisi desktop USA Configuration Manager per la distribuzione di Windows. I clienti di Intune apprezzano le informazioni aggiuntive dai dati di analisi e sono in grado di condividere informazioni approfondite anche con loro.

### <a name="its-been-over-72-hours-and-the-portal-is-still-processing-data-what-next"></a>Sono passate oltre 72 ore e il portale sta ancora elaborando i dati? 

Quando si configura per la prima volta analisi desktop, è possibile che i report Configuration Manager e il portale di analisi desktop non visualizzino immediatamente i dati completi. Per elaborare i dati, il servizio può richiedere 2-3 giorni. Se è passato più di 72 ore e il portale sta ancora elaborando i dati, attenersi alla procedura seguente:

- Per verificare che i dispositivi attivi siano configurati correttamente, usare il [dashboard di integrità della connessione](/sccm/desktop-analytics/monitor-connection-health). Questo dashboard non viene aggiornato in tempo reale.
- Assicurarsi che i dispositivi inviino i dati di diagnostica al servizio desktop Analytics. Per altre informazioni, vedere [abilitare la condivisione dei dati](/sccm/desktop-analytics/enable-data-sharing).
- Effettuare il provisioning di [Azure ad applicazioni](/sccm/desktop-analytics/troubleshooting#bkmk_AzureADApps) nel Azure ad.
- Controllare i dispositivi associati all'organizzazione negli ultimi sette giorni. Nel [portale di analisi dei desktop](https://aka.ms/desktopanalytics)passare al riquadro **servizi connessi** . Selezionare **registra i dispositivi**e **visualizzare i dati recenti**

Se i dispositivi sono configurati correttamente e non vengono ancora visualizzati i dati nell'area di lavoro, [contattare il supporto tecnico Microsoft](https://support.microsoft.com/hub/4343728/support-for-business).


## <a name="windows-upgrade"></a>Aggiornamento di Windows

### <a name="can-i-upgrade-windows-and-change-architecture"></a>È possibile aggiornare Windows e modificare l'architettura?

Desktop Analytics è progettato per supportare al meglio gli aggiornamenti sul posto. Gli aggiornamenti sul posto non supportano le migrazioni dall'architettura a 32 bit a quella a 64 bit. Se è necessario eseguire la migrazione dei computer in questo scenario, usare lo scenario di aggiornamento. Le informazioni dettagliate su desktop Analytics sono ancora utili in questo scenario, ma è possibile ignorare le indicazioni specifiche per l'aggiornamento.

Per altre informazioni, vedere [Aggiornare un computer esistente con una nuova versione di Windows](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows).

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>È possibile passare da BIOS a UEFI durante l'aggiornamento di Windows?

Sì. Per ulteriori informazioni, vedere [conversione da BIOS a UEFI durante un aggiornamento sul posto](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>È possibile usare desktop Analytics con Windows 10 LTSC?

Sebbene sia possibile usare l'analisi del desktop per supportare l'aggiornamento dei dispositivi da Windows 10 Long-Term Servicing Channel (LTSC) a un canale semestrale di Windows 10, desktop Analytics non supporta gli aggiornamenti per Windows 10 LTSC. Questo canale di Windows 10 non è destinato a un uso ampio e non riceve gli aggiornamenti delle funzionalità, quindi non si tratta di una destinazione supportata con analisi desktop. Per altre informazioni, vedere [Panoramica di Windows come servizio](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).

### <a name="can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal"></a>È possibile ridurre la quantità di tempo necessaria per l'aggiornamento dei dati nel portale di analisi desktop?

Nel portale di analisi desktop sono disponibili due tipi di dati: Dati dell'amministratore e dati di diagnostica. Per aggiornare i dati dell'amministratore su richiesta, aprire il riquadro a comparsa valuta dati e selezionare **Applica modifiche**. Questa azione attiva immediatamente un aggiornamento unico di eventuali modifiche amministrative in sospeso nelle aree di lavoro. Le modifiche vengono propagate e sono disponibili a livello generale entro 15-60 minuti. La durata dipende dalle dimensioni dell'area di lavoro e dall'ambito delle modifiche in sospeso. È possibile richiedere un aggiornamento dati su richiesta fino a sei volte nell'arco di 24 ore. 

Tutti i dati vengono aggiornati automaticamente una volta al giorno, anche se non si richiede un aggiornamento dati su richiesta. Non è possibile attivare un aggiornamento su richiesta dei dati di diagnostica. Per altre informazioni sui diversi tipi di dati in analisi desktop, vedere [latenza dei dati](/sccm/desktop-analytics/troubleshooting#data-latency).

## <a name="privacy"></a>Privacy

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>È possibile usare l'analisi del desktop senza una connessione client diretta al servizio Microsoft Gestione dati?

No, l'intero servizio è basato sui dati di diagnostica di Windows, che richiedono che i dispositivi abbiano questa connettività diretta.

### <a name="can-i-choose-the-data-center-location"></a>È possibile scegliere il percorso data center?

Per Log Analytics di Azure: Sì, quando si configura analisi desktop e si crea l'area di lavoro Log Analytics.

Per il servizio Microsoft Gestione dati e il servizio di archiviazione Azure Analytics: No, questi due servizi sono ospitati nel Stati Uniti.

### <a name="where-is-my-organizations-data-stored"></a>Dove vengono archiviati i dati dell'organizzazione?

I dati di diagnostica di Windows dei computer vengono crittografati, inviati ed elaborati nei data center protetti gestiti da Microsoft presenti nel Stati Uniti. L'analisi dei dati correlati a analisi desktop viene quindi fornita tramite la soluzione desktop Analytics nella portale di Azure. Desktop Analytics è supportato in tutte le aree di Azure. La selezione di un'area di Azure internazionale non impedisce l'invio e l'elaborazione dei dati di diagnostica nei data center protetti di Microsoft negli Stati Uniti.

## <a name="other"></a>Altro

### <a name="can-i-use-desktop-analytics-for-my-office-365-proplus-upgrades"></a>È possibile usare l'analisi del desktop per gli aggiornamenti di Office 365 ProPlus?

No, desktop Analytics è incentrato su Windows. Microsoft ha sviluppato desktop Analytics in stretta collaborazione con numerosi clienti. Tramite il programma di anteprima, il feedback dei clienti riguarda il modo in cui analisi desktop ha migliorato la propria capacità di gestire le distribuzioni di Windows in tutta sicurezza. Ci hanno inoltre comunicato che volevano che [office 365 ProPlussse](/sccm/sum/deploy-use/office-365-dashboard#bkmk_o365_readiness) più accuratamente l'integrazione con gli strumenti di gestione di office in Configuration Manager e Intune. Microsoft continuerà a creare investimenti in tali aree, concentrandosi sugli scenari di Windows in desktop Analytics.

### <a name="how-can-i-provide-feedback-about-desktop-analytics"></a>Come è possibile fornire commenti e suggerimenti su desktop Analytics?

Per condividere commenti e suggerimenti su desktop Analytics, selezionare l'icona **Invia smile** nella parte superiore del portale. Includi uno screenshot con la tua presentazione per aiutare Microsoft a comprendere meglio i tuoi commenti. È anche possibile inviare suggerimenti sul prodotto e votare altre idee in [UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas?category_id=366805).

> [!Note]
> Non condividere mai le informazioni private tramite Invia smile o UserVoice. Tali informazioni private includono l'ID tenant o l'ID commerciale. Microsoft non fornisce supporto tramite i canali Invia smile o UserVoice. Per ottenere assistenza con l'area di lavoro di desktop Analytics, selezionare il collegamento **Guida e supporto** nel menu di navigazione per aprire un ticket di supporto.

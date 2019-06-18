---
title: Aggiornamenti in Desktop Analitica
titleSuffix: Configuration Manager
description: Informazioni sugli aggiornamenti di sicurezza e funzionalità in Desktop Analitica.
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7fc673cfa11224394df785f2e13e77ad2e0f5888
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159221"
---
# <a name="updates-in-desktop-analytics"></a>Aggiornamenti in Desktop Analitica

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Nel portale di Analitica Desktop, visualizzare lo stato degli aggiornamenti di sicurezza e funzionalità. Selezionare i nodi nel gruppo di monitoraggio del menu principale di Analitica Desktop. Questi nodi offrono informazioni dettagliate sullo stato di questi aggiornamenti nell'ambiente in uso.



## <a name="security-updates"></a>Aggiornamenti della sicurezza

Per esaminare lo stato corrente degli aggiornamenti della protezione, selezionare **gli aggiornamenti della sicurezza** nel **Monitor** sezione di Analitica Desktop:

![Nodo di Analitica Desktop aggiornamenti della sicurezza](media/security-updates.png)

Questa visualizzazione riepiloga *sicurezza* gli aggiornamenti per i dispositivi che eseguono Windows 10. I dispositivi nel grafico a barre vengono classificati in base le etichette seguenti:

#### <a name="latest"></a>più recente

I dispositivi eseguono l'aggiornamento della sicurezza più recente per tale versione e il canale.

#### <a name="latest-1"></a>Versione più recente-1

I dispositivi sono in esecuzione una sicurezza aggiornamento una versione precedente rispetto all'aggiornamento più recente disponibile su tale canale.

#### <a name="older"></a>Più vecchio

I dispositivi sono in esecuzione un aggiornamento della protezione meno recente versione più recente-1.

#### <a name="not-measured"></a>Non è stato misurato

Analitica desktop non è stato valutato il dispositivo. Questo stato include i dispositivi che eseguono Windows 7, Windows 8.1 o Windows 10 dispositivi registrati per il programma di Insider di Windows.  



## <a name="feature-updates"></a>Aggiornamenti delle funzionalità

Per esaminare lo stato corrente degli aggiornamenti di funzionalità, selezionare **gli aggiornamenti delle funzionalità** nel **Monitor** sezione di Analitica Desktop:

![Nodo gli aggiornamenti di funzionalità del Desktop Analitica](media/feature-updates.png)

Questa visualizzazione riepiloga *funzionalità* gli aggiornamenti per i dispositivi che eseguono Windows 10.

Per altre informazioni sui periodi di servizio, vedere [fogli informativi del ciclo di vita di Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).  

I dispositivi nel grafico a barre vengono classificati in base le etichette seguenti:

#### <a name="in-service"></a>Nel servizio

I dispositivi eseguono l'aggiornamento delle funzionalità più recente per tale versione e il canale.  

#### <a name="near-end-of-service"></a>Prossimo alla assistenza

I dispositivi sono in esecuzione un aggiornamento delle funzionalità che è entro 90 giorni di raggiunta la fine del servizio.

#### <a name="end-of-service"></a>Arresto del servizio

I dispositivi sono in esecuzione un aggiornamento delle funzionalità che ha superato la data di fine del servizio. Per informazioni dettagliate sulla fine del periodo di servizio, vedere [fogli informativi del ciclo di vita di Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

#### <a name="not-measured"></a>Non è stato misurato

Analitica desktop non è stato valutato il dispositivo. Questo stato include i dispositivi che eseguono Windows 7, Windows 8.1 o Windows 10 dispositivi registrati per il programma di Insider di Windows.



## <a name="next-steps"></a>Passaggi successivi

- [Informazioni sugli asset di Analitica Desktop](/sccm/desktop-analytics/about-assets): i dispositivi, driver e le app  

- [Informazioni sui piani di distribuzione](/sccm/desktop-analytics/about-deployment-plans)  

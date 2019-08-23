---
title: Aggiornamenti in desktop Analytics
titleSuffix: Configuration Manager
description: Informazioni sugli aggiornamenti della sicurezza e delle funzionalità in desktop Analytics.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0cceaf6f4475a024b8f3375ef962a6dfc2dddc4d
ms.sourcegitcommit: e0d303d87c737811c2d3c40d01cd3d260a5c7bde
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/22/2019
ms.locfileid: "69974778"
---
# <a name="updates-in-desktop-analytics"></a>Aggiornamenti in desktop Analytics

> [!Note]  
> Queste informazioni si riferiscono a un servizio di anteprima che può essere modificato in modo sostanziale prima del rilascio commerciale. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Nel portale di analisi dei desktop visualizzare lo stato degli aggiornamenti della sicurezza e delle funzionalità. Selezionare questi nodi nel gruppo monitoraggio del menu principale di analisi desktop. Questi nodi forniscono informazioni dettagliate sullo stato di questi aggiornamenti nell'ambiente in uso.


## <a name="security-updates"></a>Aggiornamenti della sicurezza

Per esaminare lo stato corrente degli aggiornamenti della sicurezza, selezionare **aggiornamenti della sicurezza** nella sezione **monitoraggio** di analisi del desktop:

![Nodo aggiornamenti della sicurezza di analisi desktop](media/security-updates.png)

Questa vista riepiloga gli aggiornamenti della *sicurezza* per i dispositivi che eseguono Windows 10. I dispositivi nel grafico a barre sono suddivisi in categorie in base alle etichette seguenti:

#### <a name="latest"></a>Ultima

I dispositivi eseguono l'aggiornamento della sicurezza più recente per la versione e il canale.

#### <a name="latest-1"></a>Più recente-1

I dispositivi eseguono un aggiornamento della sicurezza di una versione precedente all'ultimo aggiornamento disponibile sul canale.

#### <a name="older"></a>Precedente

I dispositivi eseguono un aggiornamento della sicurezza precedente alla più recente-1.

#### <a name="not-measured"></a>Non misurato

Il dispositivo non è stato valutato da desktop Analytics. Questo stato include i dispositivi che eseguono dispositivi Windows 7, Windows 8.1 o Windows 10 registrati per il programma Windows Insider.  

Se un dispositivo Windows 10 *non* è autenticato con una account Microsoft, Windows non segnala questi dati. Questa autenticazione viene in genere completata come parte del Installazione di Windows la configurazione guidata.<!-- 5148153 -->


## <a name="feature-updates"></a>Aggiornamenti delle funzionalità

Per esaminare lo stato corrente degli aggiornamenti delle funzionalità, selezionare **aggiornamenti funzionalità** nella sezione **monitoraggio** di analisi del desktop:

![Nodo aggiornamenti funzionalità di analisi desktop](media/feature-updates.png)

Questa vista riepiloga gli aggiornamenti delle *funzionalità* per i dispositivi che eseguono Windows 10.

Per ulteriori informazioni sui periodi di servizio, vedere la pagina dei [fatti del ciclo](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)di vita di Windows.  

I dispositivi nel grafico a barre sono suddivisi in categorie in base alle etichette seguenti:

#### <a name="in-service"></a>Nel servizio

I dispositivi eseguono l'aggiornamento delle funzionalità più recente per la versione e il canale.  

#### <a name="near-end-of-service"></a>Vicino alla fine del servizio

I dispositivi eseguono un aggiornamento delle funzionalità entro 90 giorni dalla fine del servizio.

#### <a name="end-of-service"></a>Fine del servizio

I dispositivi eseguono un aggiornamento delle funzionalità oltre la data di fine del servizio. Per informazioni dettagliate sulle date di fine del servizio, vedere [foglio dei fatti del ciclo](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)di vita di Windows.

#### <a name="not-measured"></a>Non misurato

Il dispositivo non è stato valutato da desktop Analytics. Questo stato include i dispositivi che eseguono dispositivi Windows 7, Windows 8.1 o Windows 10 registrati per il programma Windows Insider.

Se un dispositivo Windows 10 *non* è autenticato con una account Microsoft, Windows non segnala questi dati. Questa autenticazione viene in genere completata come parte del Installazione di Windows la configurazione guidata.<!-- 5148153 -->


## <a name="next-steps"></a>Passaggi successivi

- Informazioni [sulle risorse di analisi desktop](/sccm/desktop-analytics/about-assets): dispositivi, driver e app  

- [Informazioni sui piani di distribuzione](/sccm/desktop-analytics/about-deployment-plans)  

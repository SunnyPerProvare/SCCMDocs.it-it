---
title: Aggiornamenti in Desktop Analitica
titleSuffix: Configuration Manager
description: Informazioni sugli aggiornamenti di sicurezza e funzionalità in Desktop Analitica.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: b46bf167bc77716fe360940c4fb45cae2dc9dc5a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755386"
---
# <a name="updates-in-desktop-analytics"></a>Aggiornamenti in Desktop Analitica 

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Nel portale di Analitica Desktop, visualizzare lo stato degli aggiornamenti di sicurezza e funzionalità. Selezionare i nodi nel gruppo di monitoraggio del menu principale di Analitica Desktop. Questi nodi offrono informazioni dettagliate sullo stato di questi aggiornamenti nell'ambiente in uso. 



## <a name="security-updates"></a>Aggiornamenti della sicurezza

Per esaminare lo stato corrente degli aggiornamenti della protezione, selezionare **gli aggiornamenti della sicurezza** nel **Monitor** sezione di Analitica Desktop:

![Nodo di Analitica Desktop aggiornamenti della sicurezza](media/security-updates.png)

Questa visualizzazione riepiloga *sicurezza* gli aggiornamenti per i dispositivi che eseguono Windows 10 o Office 365 ProPlus. I dispositivi nel grafico a barre vengono classificati in base le etichette seguenti:

#### <a name="latest"></a>più recente
I dispositivi eseguono l'aggiornamento della sicurezza più recente per tale versione e il canale.

#### <a name="latest-1"></a>Versione più recente-1
I dispositivi sono in esecuzione una sicurezza aggiornamento una versione precedente rispetto all'aggiornamento più recente disponibile su tale canale.

#### <a name="older"></a>Più vecchio
I dispositivi sono in esecuzione un aggiornamento della protezione meno recente versione più recente-1.

#### <a name="not-measured"></a>Non è stato misurato
Analitica desktop non è stato valutato il dispositivo. 

- Per Windows, inclusi i dispositivi che eseguono Windows 7 o Windows 8.1  

- Per Office, inclusi i dispositivi con una delle versioni seguenti:  

    - Canale di Office 365 ProPlus, Insider  

    - Una versione perpetua di Office che usano Windows installer. Ad esempio Office 2016, Office 2013 o Office 2010.  

    - Office 365 ProPlus in un dispositivo che non ha restituito dati sufficienti per valutare lo stato di sicurezza  



## <a name="feature-updates"></a>Aggiornamenti delle funzionalità

Per esaminare lo stato corrente degli aggiornamenti di funzionalità, selezionare **gli aggiornamenti delle funzionalità** nel **Monitor** sezione di Analitica Desktop:

![Nodo gli aggiornamenti di funzionalità del Desktop Analitica](media/feature-updates.png)

Questa visualizzazione riepiloga *funzionalità* gli aggiornamenti per i dispositivi che eseguono Windows 10 o Office 365 ProPlus. 

Per altre informazioni sui periodi di servizio, vedere gli articoli seguenti: 
- [Fogli informativi del ciclo di vita di Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)  
- [Cronologia di aggiornamento per Office 365 ProPlus](https://docs.microsoft.com/officeupdates/update-history-office365-proplus-by-date)  

I dispositivi nel grafico a barre vengono classificati in base le etichette seguenti:

#### <a name="in-service"></a>Nel servizio
I dispositivi eseguono l'aggiornamento delle funzionalità più recente per tale versione e il canale.  

#### <a name="near-end-of-service"></a>Prossimo alla assistenza
I dispositivi sono in esecuzione un aggiornamento delle funzionalità che è entro 90 giorni di raggiunta la fine del servizio.

#### <a name="end-of-service"></a>Arresto del servizio
I dispositivi sono in esecuzione un aggiornamento delle funzionalità che ha superato la data di fine del servizio. Per informazioni dettagliate sulla fine del periodo di servizio, vedere {xlink nella relativa sezione del UDR_monitoring} |

#### <a name="not-measured"></a>Non è stato misurato
Analitica desktop non è stato valutato il dispositivo. 

- Per Windows, inclusi i dispositivi che eseguono Windows 7 o Windows 8.1  

- Per Office, inclusi i dispositivi con una delle versioni seguenti:  

    - Canale di Office 365 ProPlus, Insider  

    - Una versione perpetua di Office che usano Windows installer. Ad esempio Office 2016, Office 2013 o Office 2010.  

    - Office 365 ProPlus in un dispositivo che non ha restituito dati sufficienti per valutare lo stato di sicurezza  



## <a name="next-steps"></a>Passaggi successivi

- [Informazioni sugli asset di Analitica Desktop](/sccm/desktop-analytics/about-assets): i dispositivi, App, le app di Office, componenti aggiuntivi di Office e macro di Office  

- [Informazioni sui piani di distribuzione](/sccm/desktop-analytics/about-deployment-plans)  


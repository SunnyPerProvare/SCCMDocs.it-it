---
title: Dati di utilizzo e di diagnostica | Microsoft Docs
description: Informazioni sui dati di utilizzo e di diagnostica raccolti da System Center Configuration Manager.
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
caps.latest.revision: 9
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 4a4b7c9c0d40b6bd3ea2f318e37d744f1a0cc084
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017


---
# <a name="diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Dati di diagnostica e di utilizzo per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager raccoglie dati di utilizzo e di diagnostica su se stesso che vengono usati da Microsoft per migliorare l'esperienza, la qualità e la sicurezza di installazione delle versioni future.  

 I dati di utilizzo e di diagnostica sono abilitati per ogni gerarchia di System Center Configuration Manager. Essi consistono in query di SQL Server eseguite su base settimanale in ogni sito primario e nel sito di amministrazione centrale. Quando la gerarchia usa un sito di amministrazione centrale, i dati dai siti primari vengono quindi replicati in tale sito. Nel sito di livello superiore della gerarchia, il punto di connessione del servizio invia queste informazioni quando verifica la presenza di aggiornamenti. Se il punto di connessione del servizio è in modalità offline, le informazioni vengono trasferite tramite lo strumento di connessione del servizio.  

> [!NOTE]  
>  Configuration Manager raccoglie i dati solo dal database di SQL Server del sito e non direttamente dai client o dai server del sito.  

 Per altre informazioni, vedere l'[Informativa sulla privacy per System Center Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=626527).  

 Altre informazioni sui dati di utilizzo e di diagnostica per System Center Configuration Manager sono disponibili negli articoli seguenti:  

-   [Come vengono usati i dati di utilizzo e di diagnostica per System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used.md)  

-   Livelli di raccolta dati utilizzo e di diagnostica:
    - [Dati di diagnostica per 1702](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1702)      
    - [Dati di diagnostica per 1610](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)  
    - [Dati di diagnostica per 1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)    

<!--
    - [Diagnostic data for 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
    - [Diagnostic data for  1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
-->

-   [Come vengono raccolti i dati di utilizzo e di diagnostica da System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected.md)  

-   [Come visualizzare dati di utilizzo e di diagnostica per System Center Configuration Manager](../../../core/plan-design/diagnostics/view-diagnostics-and-usage-data.md)  

-   [Analisi utilizzo software per System Center Configuration Manager](../../../core/plan-design/diagnostics/customer-experience-improvement-program-ceip.md)  

-   [Domande frequenti sui dati di utilizzo e di diagnostica per System Center Configuration Manager](../../../core/understand/frequently-asked-questions-about-diagnostics-and-usage-data.md)  

## <a name="see-also"></a>Vedere anche  
 [Informazioni sul punto di connessione del servizio in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md)


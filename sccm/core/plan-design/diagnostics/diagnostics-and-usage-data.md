---
title: Dati di utilizzo e di diagnostica | System Center Configuration Manager
description: Informazioni sui dati di utilizzo e di diagnostica raccolti da System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
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
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 996efaeb89926b04d2f071cf600dcf45bd2edc89


---
# <a name="diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Dati di diagnostica e di utilizzo per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager raccoglie dati di utilizzo e di diagnostica su se stesso che vengono usati da Microsoft per migliorare l'esperienza, la qualità e la sicurezza di installazione delle versioni future.  

 I dati di utilizzo e di diagnostica sono abilitati per ogni gerarchia di System Center Configuration Manager. Essi consistono in query di SQL Server eseguite su base settimanale in ogni sito primario e nel sito di amministrazione centrale. Quando la gerarchia usa un sito di amministrazione centrale, i dati dai siti primari vengono quindi replicati in tale sito. Nel sito di livello superiore della gerarchia, il punto di connessione del servizio invia queste informazioni quando verifica la presenza di aggiornamenti. Se il punto di connessione del servizio è in modalità offline, le informazioni vengono trasferite tramite lo strumento di connessione del servizio.  

> [!NOTE]  
>  Configuration Manager raccoglie solo i dati dal database di SQL Server dei siti e non direttamente dai client o dai server del sito.  

 Per altre informazioni, vedere l' [Informativa sulla privacy per System Center Configuration Manager](http://go.microsoft.com/fwlink/?LinkID=626527).  

 Altre informazioni sui dati di utilizzo e di diagnostica per System Center Configuration Manager sono disponibili negli argomenti seguenti:  

-   [How diagnostics and usage data is used for System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used.md) (Come vengono usati i dati di utilizzo e di diagnostica per System Center Configuration Manager)  

-   Livelli di raccolta dati utilizzo e di diagnostica:
    - [Dati di diagnostica per 1511](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
    - [Dati di diagnostica per la versione 1602](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
    - [Dati di diagnostica per 1606](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)  
    

-   [How diagnostics and usage data is collected by System Center Configuration Manager](../../../core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected.md) (Come vengono raccolti i dati di utilizzo e di diagnostica da System Center Configuration Manager)  

-   [How to view diagnostics and usage data for System Center Configuration Manager](../../../core/plan-design/diagnostics/view-diagnostics-and-usage-data.md) (Come visualizzare dati di utilizzo e di diagnostica per System Center Configuration Manager)  

-   [Customer Experience Improvement Program (CEIP) for System Center Configuration Manager](../../../core/plan-design/diagnostics/customer-experience-improvement-program-ceip.md) (Analisi utilizzo software per System Center Configuration Manager)  

-   [Frequently asked questions about diagnostics and usage data for System Center Configuration Manager](../../../core/understand/frequently-asked-questions-about-diagnostics-and-usage-data.md) (Domande frequenti sui dati di utilizzo e di diagnostica per System Center Configuration Manager)  

## <a name="see-also"></a>Vedere anche  
 [About the service connection point in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md) (Informazioni sul punto di connessione del servizio in System Center Configuration Manager)



<!--HONumber=Nov16_HO1-->


---
title: Diagnostica e dati di utilizzo
titleSuffix: Configuration Manager
description: Informazioni sui dati di utilizzo e di diagnostica raccolti da System Center Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 132604418ce810fb78b397f3d5f322b10abe6bb3
ms.sourcegitcommit: 1439817f1309658b31008d7bafaab32fc5ef8789
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52820017"
---
# <a name="diagnostics-and-usage-data-for-system-center-configuration-manager"></a>Dati di diagnostica e di utilizzo per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Configuration Manager raccoglie dati di utilizzo e di diagnostica su se stesso che vengono usati da Microsoft per migliorare l'esperienza, la qualità e la sicurezza di installazione delle versioni future.  

 I dati di utilizzo e di diagnostica sono abilitati per ogni gerarchia di Configuration Manager. Essi consistono in query di SQL Server eseguite su base settimanale in ogni sito primario e nel sito di amministrazione centrale. Quando la gerarchia usa un sito di amministrazione centrale, i dati dai siti primari vengono quindi replicati in tale sito. Nel sito di livello superiore della gerarchia, il punto di connessione del servizio invia queste informazioni quando verifica la presenza di aggiornamenti. Se il punto di connessione del servizio è in modalità offline, le informazioni vengono trasferite tramite lo strumento di connessione del servizio.  

> [!NOTE]  
>  Configuration Manager raccoglie i dati solo dal database di SQL Server del sito e non direttamente dai client o dai server del sito.  

 Per altre informazioni, vedere l'[Informativa sulla privacy Microsoft](https://go.microsoft.com/fwlink/?LinkID=626527).  

## <a name="articles"></a>Articoli
 Altre informazioni sui dati di utilizzo e di diagnostica per Configuration Manager sono disponibili negli articoli seguenti:  

-   [Come vengono usati i dati di diagnostica e di utilizzo](/sccm/core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used)  

-   Livelli di raccolta dati utilizzo e di diagnostica:
    - [Dati di diagnostica per la versione 1810](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1810)  

    - [Dati di diagnostica per la versione 1806](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1806)  

    - [Dati di diagnostica per la versione 1802](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1802)  
    
    - [Dati di diagnostica per la versione 1710](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1710)  

-   [Come vengono raccolti i dati di diagnostica e di utilizzo](/sccm/core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected)  

-   [Come visualizzare i dati di diagnostica e di utilizzo](/sccm/core/plan-design/diagnostics/view-diagnostics-and-usage-data)  

-   [Analisi utilizzo software](/sccm/core/plan-design/diagnostics/customer-experience-improvement-program-ceip)  

     > [!Note]  
     > A partire da Configuration Manager versione 1802 la funzionalità Analisi utilizzo software è stata rimossa dal prodotto.  


-   [Domande frequenti sui dati di diagnostica e di utilizzo](/sccm/core/understand/frequently-asked-questions-about-diagnostics-and-usage-data)  



## <a name="see-also"></a>Vedere anche  
 [Informazioni sul punto di connessione del servizio](/sccm/core/servers/deploy/configure/about-the-service-connection-point)

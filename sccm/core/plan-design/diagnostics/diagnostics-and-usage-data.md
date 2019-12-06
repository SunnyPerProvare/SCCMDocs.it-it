---
title: Diagnostica e dati di utilizzo
titleSuffix: Configuration Manager
description: Informazioni sui dati di diagnostica e utilizzo raccolti da Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 88ac4e55-d47b-4c94-b9c3-704c6a48b845
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 68a5787b4c4fa2caf05c1a8c9c6e64bbdd437279
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "68536766"
---
# <a name="diagnostics-and-usage-data-for-configuration-manager"></a>Dati di diagnostica e utilizzo per Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Configuration Manager raccoglie dati di utilizzo e di diagnostica su se stesso che vengono usati da Microsoft per migliorare l'esperienza, la qualità e la sicurezza di installazione delle versioni future.  

I dati di utilizzo e di diagnostica sono abilitati per ogni gerarchia di Configuration Manager. Essi consistono in query di SQL Server eseguite su base settimanale in ogni sito primario e nel sito di amministrazione centrale. Quando la gerarchia usa un sito di amministrazione centrale, i dati dai siti primari vengono quindi replicati in tale sito. Nel sito di livello superiore della gerarchia, il punto di connessione del servizio invia queste informazioni quando verifica la presenza di aggiornamenti. Se il punto di connessione del servizio è in modalità offline, le informazioni vengono trasferite tramite lo strumento di connessione del servizio.  

> [!NOTE]  
> Configuration Manager raccoglie i dati solo dal database di SQL Server del sito e non direttamente dai client o dai server del sito.  

Per altre informazioni, vedere l'[Informativa sulla privacy Microsoft](https://go.microsoft.com/fwlink/?LinkID=626527).  

## <a name="articles"></a>Articoli

Altre informazioni sui dati di utilizzo e di diagnostica per Configuration Manager sono disponibili negli articoli seguenti:  

- [Come vengono usati i dati di diagnostica e di utilizzo](/sccm/core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-used)  

- Livelli di raccolta dati utilizzo e di diagnostica:

    - [Dati di diagnostica per la versione 1906](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1906)  

    - [Dati di diagnostica per la versione 1902](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1902)  

    - [Dati di diagnostica per la versione 1810](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1810)  

    - [Dati di diagnostica per la versione 1806](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1806)  

- [Come vengono raccolti i dati di diagnostica e di utilizzo](/sccm/core/plan-design/diagnostics/how-diagnostics-and-usage-data-is-collected)  

- [Come visualizzare i dati di diagnostica e di utilizzo](/sccm/core/plan-design/diagnostics/view-diagnostics-and-usage-data)  

- [Domande frequenti sui dati di diagnostica e di utilizzo](/sccm/core/understand/frequently-asked-questions-about-diagnostics-and-usage-data)  


## <a name="see-also"></a>Vedere anche

[Informazioni sul punto di connessione del servizio](/sccm/core/servers/deploy/configure/about-the-service-connection-point)

---
title: Raccolta di dati di diagnostica
titleSuffix: Configuration Manager
description: Informazioni sulla modalità di raccolta dei dati di utilizzo e di diagnostica di Configuration Manager da parte di questo strumento.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 47d1bf3d7a21f7286f0f46371fcb7a1abc7930a9
ms.sourcegitcommit: bfece120a6f9a79dbcc8bacc83905f16f3f1b144
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "76917381"
---
# <a name="how-configuration-manager-collects-diagnostics-and-usage-data"></a>Come Configuration Manager raccoglie i dati di diagnostica e utilizzo

*Si applica a: Configuration Manager (Current Branch)*

Per raccogliere dati di diagnostica e di utilizzo per Configuration Manager, ogni sito primario esegue query di SQL Server su base settimanale. In una gerarchia a più siti, i dati vengono replicati nel sito di amministrazione centrale.  

Nel sito di livello superiore di una gerarchia, il punto di connessione del servizio invia queste informazioni quando verifica la presenza di aggiornamenti. La modalità del punto di connessione del servizio determina il modo in cui vengono trasferiti i dati:

- **Online**: una volta alla settimana, il punto di connessione del servizio invia automaticamente i dati di diagnostica e utilizzo al servizio cloud.

- **Offline**: i dati di diagnostica e di utilizzo possono essere trasferiti manualmente con lo [strumento di connessione del servizio](/configmgr/core/servers/manage/use-the-service-connection-tool).

Per altre informazioni, vedere [Informazioni sul punto di connessione del servizio](/configmgr/core/servers/deploy/configure/about-the-service-connection-point).

> [!div class="nextstepaction"]
> [Come visualizzare i dati di diagnostica e di utilizzo](/configmgr/core/plan-design/diagnostics/view-diagnostics-and-usage-data)

---
title: Raccolta di dati di diagnostica
titleSuffix: Configuration Manager
description: Informazioni sulla modalità di raccolta dei dati di utilizzo e di diagnostica di Configuration Manager da parte di questo strumento.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 63ac768d4c2779be02c8258a964bb4181e246608
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75801512"
---
# <a name="how-diagnostics-and-usage-data-is-collected-by-configuration-manager"></a>Come vengono raccolti i dati di utilizzo e di diagnostica da Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Per raccogliere dati di diagnostica e di utilizzo per Configuration Manager, ogni sito primario esegue query di SQL Server su base settimanale. In una gerarchia a più siti, i dati vengono replicati nel sito di amministrazione centrale.  

Nel sito di livello superiore della gerarchia, il ruolo del sistema del sito del punto di connessione del servizio invia queste informazioni quando verifica la presenza di aggiornamenti. La modalità del punto di connessione del servizio determina il modo in cui vengono trasferiti i dati:  

-   **In modalità online:** i dati di diagnostica e di utilizzo vengono inviati automaticamente dopo una settimana dal punto di connessione del servizio al servizio cloud.  

-   **In modalità offline:** i dati di diagnostica e di utilizzo vengono trasferiti manualmente usando lo strumento di connessione del servizio. Per altre informazioni, vedere [Usare lo strumento di connessione del servizio per Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

Per altre informazioni, vedere [Informazioni sul punto di connessione del servizio](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

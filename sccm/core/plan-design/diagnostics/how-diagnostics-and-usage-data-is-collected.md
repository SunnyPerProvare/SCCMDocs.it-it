---
title: Raccolta di dati di diagnostica
titleSuffix: Configuration Manager
description: Informazioni sulla modalità di raccolta dei dati di utilizzo e di diagnostica di System Center Configuration Manager da parte di questo strumento.
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7eb4becd24ac143ce17c476cda0535ac6bedd039
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="how-diagnostics-and-usage-data-is-collected-by-system-center-configuration-manager"></a>Come vengono raccolti i dati di diagnostica e di utilizzo da System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Per raccogliere dati di diagnostica e di utilizzo per System Center Configuration Manager, ogni sito primario esegue query di SQL Server su base settimanale. In una gerarchia a più siti, i dati vengono replicati nel sito di amministrazione centrale.  

Nel sito di livello superiore della gerarchia, il ruolo del sistema del sito del punto di connessione del servizio invia queste informazioni quando verifica la presenza di aggiornamenti. La modalità del punto di connessione del servizio determina il modo in cui vengono trasferiti i dati:  

-   **In modalità online:** i dati di diagnostica e di utilizzo vengono inviati automaticamente dopo una settimana dal punto di connessione del servizio al servizio cloud.  

-   **In modalità offline:** i dati di diagnostica e di utilizzo vengono trasferiti manualmente usando lo strumento di connessione del servizio. Per altre informazioni, vedere [Usare lo strumento di connessione del servizio per System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

Per ulteriori informazioni, vedere [Informazioni sul punto di connessione del servizio in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

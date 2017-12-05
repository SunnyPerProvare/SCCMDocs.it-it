---
title: Raccolta di dati di diagnostica
titleSuffix: Configuration Manager
description: "Informazioni sulla modalità di raccolta dei dati di utilizzo e di diagnostica di System Center Configuration Manager da parte di questo strumento."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
caps.latest.revision: "5"
author: aaroncz
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: a879bd0eba04ffef1f3c6c6ce8426c380aefc1d3
ms.sourcegitcommit: 7fe45ff75f05f7cc03ad021db8119791abe18049
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/01/2017
---
# <a name="how-diagnostics-and-usage-data-is-collected-by-system-center-configuration-manager"></a>Come vengono raccolti i dati di diagnostica e di utilizzo da System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Per raccogliere dati di diagnostica e di utilizzo per System Center Configuration Manager, ogni sito primario esegue query di SQL Server su base settimanale. In una gerarchia a più siti, i dati vengono replicati nel sito di amministrazione centrale.  

Nel sito di livello superiore della gerarchia, il ruolo del sistema del sito del punto di connessione del servizio invia queste informazioni quando verifica la presenza di aggiornamenti. La modalità del punto di connessione del servizio determina il modo in cui vengono trasferiti i dati:  

-   **In modalità online:** i dati di diagnostica e di utilizzo vengono inviati automaticamente dopo una settimana dal punto di connessione del servizio al servizio cloud.  

-   **In modalità offline:** i dati di diagnostica e di utilizzo vengono trasferiti manualmente usando lo strumento di connessione del servizio. Per altre informazioni, vedere [Usare lo strumento di connessione del servizio per System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md).  

Per ulteriori informazioni, vedere [Informazioni sul punto di connessione del servizio in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md).  

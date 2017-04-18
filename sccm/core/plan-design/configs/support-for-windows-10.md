---
title: Supporto per Windows 10 | Microsoft Docs
description: Informazioni su quali versioni di Windows 10 sono supportate per eseguire il client di System Center Configuration Manager.
ms.custom: na
ms.date: 3/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: 5
author: brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2cdd25343cf68a79067a317b820572491a3633a2
ms.openlocfilehash: 84d6fdcec2c539f0fd3043f01d18e165da8c52c9
ms.lasthandoff: 04/12/2017

---
# <a name="support-for-windows-10-as-a-client-of-system-center-configuration-manager"></a>Supporto per Windows 10 come client di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


 In questo argomento sono indicate le versioni di Windows 10 che è possibile usare come client con le diverse versioni del Current Branch di System Center Configuration Manager.

- Questo argomento completa l'articolo [Sistemi operativi supportati per client e dispositivi](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
- Se si usa il Long-Term Servicing Branch di Configuration Manager, vedere [Configurazioni supportate per Long-Term Servicing Branch](/sccm/core/understand/supported-configurations-for-ltsb).

Configuration Manager tenta di offrire supporto per ogni nuova versione di Windows 10 appena possibile dopo il rilascio di tale versione di Windows. Poiché i prodotti hanno pianificazioni separate di sviluppo e rilascio, il supporto offerto da Configuration Manager dipende da quando vengono rilasciate le versioni e i rami di ogni prodotto.

Ad esempio, una versione di Configuration Manager viene eliminata dalla matrice dopo che termina il [supporto per tale versione](/sccm/core/servers/manage/current-branch-versions-supported). Analogamente, il supporto per le versioni di Windows 10 come Enterprise 2015 LTSB o 1607 (CBB) viene eliminato dalla matrice quando queste vengono rimosse dall'elenco delle configurazioni supportate di Configuration Manager. Per altre informazioni, vedere [Sistemi operativi deprecati](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems).



|Versioni di Windows 10                    |Configuration Manager 1606          |Configuration Manager 1610          |    Configuration Manager 1702 |
|---------------------|-----|-----|-----|
|Enterprise 2015 LTSB                   |![Supportato](media/green_check.png) |![Supportato](media/green_check.png) |![Supportato](media/green_check.png) |
|1507 <br />(*vedere le edizioni*)            |![Supportato](media/green_check.png) |![Supportato](media/green_check.png) |![Supportato](media/green_check.png) |
|1511 (CB), (CBB)<br />(*vedere le edizioni*) |![Supportato](media/green_check.png) |![Supportato](media/green_check.png) |![Supportato](media/green_check.png) |
|Enterprise 2016 LTSB                   |![Supportato](media/green_check.png) |![Supportato](media/green_check.png) |![Supportato](media/green_check.png) |
|1607 (CB)    <br />Aggiornamento dell'anniversario<br />(*vedere le edizioni*)      |![Compatibile con le versioni precedenti](media/blue_compat.png) |![Supportato](media/green_check.png) |![Supportato](media/green_check.png) |
|1607 (CBB)    <br />Aggiornamento dell'anniversario<br />(*vedere le edizioni*)      |![Non supportato](media/Red_X.png)   |![Supportato](media/green_check.png) |![Supportato](media/green_check.png) |
|1703 (CBB)    <br />Creators Update<br />(*vedere le edizioni*)      |![Non supportato](media/Red_X.png)   |![Non supportato](media/Red_X.png) |![Compatibile con le versioni precedenti](media/blue_compat.png) |



**Edizioni:** Enterprise, Pro, Education, Pro Education   

|Chiave|
|--|
|![Supportato](media/green_check.png) = **Supportato**  |
|![Non supportato](media/blue_compat.png)  = **Compatibile con le versioni precedenti**: significa che le funzionalità di gestione client esistenti (inventario hardware, inventario software, aggiornamenti software, e così via) dovrebbero funzionare con la nuova build Current Branch di Windows 10. Verranno documentati eventuali problemi noti o avvertenze. <br><br>Questo approccio offre la possibilità di distribuire e gestire fin dal primo giorno le nuove build di Windows 10 CB con il supporto di compatibilità delle applicazioni senza richiedere una nuova versione di aggiornamento di Configuration Manager. |
|![Supportato](media/Red_X.png) = **Non supportato**|


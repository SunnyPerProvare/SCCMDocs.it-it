---
title: Supporto per Windows 10 | Microsoft Docs
description: Informazioni sulle versioni di Windows 10 supportate come client o per OSD con System Center Configuration Manager.
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: "5"
author: brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 1d2e6e128531237ed76f94584aa42f76067db164
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="support-for-windows-10-for-system-center-configuration-manager"></a>Supporto per Windows 10 per System Center Configuration Manager  

*Si applica a: System Center Configuration Manager (Current Branch)*


 Questo argomento descrive in dettagli le versioni di Windows 10 che è possibile usare con varie versioni di System Center Configuration Manager Current Branch. Sono inclusi:
 -  Windows 10 come client di Configuration Manager.
 -  Windows 10 Windows Assessment and Deployment Kit (ADK).

## <a name="windows-10-as-a-client"></a>Windows 10 come client
Configuration Manager tenta di garantire il supporto come client per ogni nuova versione di Windows 10 appena possibile dopo il rilascio. Poiché i prodotti hanno pianificazioni di sviluppo e rilascio separate, il supporto offerto da Configuration Manager dipende dalla data di disponibilità di ogni prodotto.

Ad esempio, una versione di Configuration Manager viene eliminata dalla matrice dopo che termina il [supporto per tale versione](/sccm/core/servers/manage/current-branch-versions-supported). Analogamente, il supporto per le versioni di Windows 10 come Enterprise 2015 LTSB o 1511 viene eliminato dalla matrice quando queste vengono rimosse dal supporto. Per altre informazioni, vedere [Sistemi operativi deprecati](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-operating-systems).

-   Le informazioni seguenti sono a complemento dell'articolo [Sistemi operativi supportati per client e dispositivi](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
-   Se si usa il Long-Term Servicing Branch di Configuration Manager, vedere [Configurazioni supportate per Long-Term Servicing Branch](/sccm/core/understand/supported-configurations-for-ltsb).

|Versione di Windows 10                    |Configuration Manager 1610          |    Configuration Manager 1702          |    Configuration Manager 1706 |
|---------------------|-----|-----|-----|
|Enterprise 2015 LTSB                   |![Supportato](media/green_check.png) |![Supportato](media/green_check.png) |![Supportato](media/green_check.png) |
|1511  <br />(*vedere le edizioni*)           |![Supportato](media/green_check.png) |![Supportato](media/green_check.png) |![Supportato](media/green_check.png) |
|Enterprise 2016 LTSB                   |![Supportato](media/green_check.png) |![Supportato](media/green_check.png) |![Supportato](media/green_check.png) |
|1607   <br />Aggiornamento dell'anniversario<br />(*vedere le edizioni*)   |![Supportato](media/green_check.png) |![Supportato](media/green_check.png)            |![Supportato](media/green_check.png) |
|1703   <br />Creators Update<br />(*vedere le edizioni*)      |![Non supportato](media/Red_X.png)   |![Compatibile con le versioni precedenti](media/blue_compat.png) |![Supportato](media/green_check.png) |


**Edizioni:** Enterprise, Pro, Education, Pro Education   

|Chiave|
|--|
|![Supportato](media/green_check.png) = **Supportato**  |
|![Non supportato](media/blue_compat.png)  = **Compatibile con le versioni precedenti**: significa che le funzionalità di gestione client esistenti (inventario hardware, inventario software, aggiornamenti software e così via) dovrebbero funzionare con la nuova versione di Windows 10. Verranno documentati eventuali problemi noti o avvertenze. <br><br>Questo approccio offre la possibilità di distribuire e gestire fin dal primo giorno le nuove build di Windows con il supporto di compatibilità delle applicazioni senza richiedere una nuova versione di aggiornamento di Configuration Manager. |
|![Supportato](media/Red_X.png) = **Non supportato**|


## <a name="windows-10-adk"></a>Windows 10 ADK
Quando si distribuiscono sistemi operativi con Configuration Manager, [Windows ADK è una dipendenza esterna](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment) obbligatoria.

La tabella seguente elenca le versioni di Windows ADK 10 che è possibile usare con versioni diverse di Configuration Manager.

|Versione di Windows 10 ADK  |Configuration Manager 1610 |Configuration Manager 1702   |Configuration Manager 1706 |
|--------------------|-----|-----|-----|
|1511  |![Non supportato](media/Red_X.png)             |![Non supportato](media/Red_X.png)              |![Non supportato](media/Red_X.png)|
|1607  |![Supportato](media/green_check.png)           |![Compatibile con le versioni precedenti](media/blue_compat.png) |![Non supportato](media/Red_X.png)|
|1703  |![Non supportato](media/Red_X.png)             |![Supportato](media/green_check.png)            |![Supportato](media/green_check.png) |  

|Chiave|
|--|
|![Supportato](media/green_check.png) = **Supportato**: è consigliato l'uso della versione di Windows ADK corrispondente alla versione di Windows che si intende distribuire. Ad esempio, usare Windows ADK per Windows 10 versione 1703 per la distribuzione di Windows 10 versione 1703.  |
|![Compatibile con le versioni precedenti](media/blue_compat.png)  = **Compatibile con le versioni precedenti**: questa combinazione non è stata testata ma dovrebbe funzionare. Verranno documentati eventuali problemi noti o avvertenze. |
|![Supportato](media/Red_X.png) = **Non supportato**|

---
title: Supporto per Windows 10
titleSuffix: Configuration Manager
description: Informazioni sulle versioni di Windows 10 supportate come client o per la distribuzione del sistema operativo con System Center Configuration Manager
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
caps.latest.revision: 5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 877732c4095438b19a863335a4a0026b7b088b24
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2018
---
# <a name="support-for-windows-10-in-system-center-configuration-manager"></a>Supporto per Windows 10 in System Center Configuration Manager  

*Si applica a: System Center Configuration Manager (Current Branch)*


Informazioni sulle versioni di Windows 10 supportate da Configuration Manager, incluse:
 -  Windows 10 come client di Configuration Manager
 -  Windows Assessment and Deployment Kit (ADK) per Windows 10

## <a name="windows-10-as-a-client"></a>Windows 10 come client
Configuration Manager tenta di garantire il supporto come client per ogni nuova versione di Windows 10 appena possibile dopo il rilascio. Poiché i prodotti hanno pianificazioni di sviluppo e rilascio separate, il supporto offerto da Configuration Manager dipende dalla data di disponibilità di ogni prodotto.

Ad esempio, una versione di Configuration Manager viene eliminata dalla matrice dopo che termina il [supporto per tale versione](/sccm/core/servers/manage/current-branch-versions-supported). Analogamente, il supporto per le versioni di Windows 10 come Enterprise 2015 LTSB o 1511 viene eliminato dalla matrice quando queste vengono rimosse dal supporto. Per altre informazioni, vedere [Sistemi operativi deprecati](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems).


-   Le informazioni seguenti sono a complemento dell'articolo [Sistemi operativi supportati per client e dispositivi](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).
-   Se si usa il Long-Term Servicing Branch di Configuration Manager, vedere [Configurazioni supportate per Long-Term Servicing Branch](/sccm/core/understand/supported-configurations-for-ltsb).

| Versione di Windows 10 | Configuration Manager 1706 | Configuration Manager 1710 | Configuration Manager 1802 |
|---------------------|-----|-----|-----|
| Enterprise 2015 LTSB            <!--10/14/2025-->   | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |
| Enterprise 2016 LTSB            <!--10/13/2026-->   | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |
| 1607   <br />(*vedere le edizioni*)   <!--04/10/2018-->   | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |
| 1703   <br />(*vedere le edizioni*)   <!--10/09/2018-->   | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |
| 1709   <br />(*vedere le edizioni*)   <!--04/09/2019-->   | ![Compatibile con le versioni precedenti](media/blue_compat.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

**Edizioni:** Enterprise, Pro, Education, Pro Education   

|Chiave|
|--|
|![Supportato](media/green_check.png) = **Supportato**  |
|![Compatibile con le versioni precedenti](media/blue_compat.png)  = **Compatibile con le versioni precedenti**: le funzionalità di gestione client esistenti dovrebbero funzionare con la nuova versione di Windows 10, ad esempio l'inventario hardware e software e gli aggiornamenti software. Verranno documentati eventuali problemi noti o avvertenze. <br><br>Questo approccio offre la possibilità di distribuire e gestire immediatamente le nuove versioni di Windows con il supporto della compatibilità delle applicazioni e senza richiedere una nuova versione di aggiornamento di Configuration Manager. |
|![Non supportato](media/Red_X.png) = **Non supportato**|

 > [!NOTE]
 > A partire dalla versione 1802, Configuration Manager supporta il client nei dispositivi Windows 10 ARM64. Le funzionalità di gestione client esistenti dovrebbero funzionare con questi nuovi dispositivi, ad esempio l'inventario hardware e software, gli aggiornamenti del software e la gestione delle applicazioni. La distribuzione del sistema operativo non è attualmente supportata. <!-- 1353704 --> 



## <a name="windows-10-adk"></a>Windows 10 ADK
Quando si distribuiscono sistemi operativi con Configuration Manager, [Windows ADK è una dipendenza esterna](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment) obbligatoria.

La tabella seguente elenca le versioni di Windows ADK 10 che è possibile usare con versioni diverse di Configuration Manager.

| Versione di Windows 10 ADK  | Configuration Manager 1706 | Configuration Manager 1710 | Configuration Manager 1802   |
|--------------------|-----|-----|-----|
| 1607  | ![Non supportato](media/Red_X.png)   | ![Non supportato](media/Red_X.png) | ![Non supportato](media/Red_X.png) |
| 1703  | ![Supportato](media/green_check.png) | ![Compatibile con le versioni precedenti](media/blue_compat.png) | ![Compatibile con le versioni precedenti](media/blue_compat.png) |
| 1709  | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |

|Chiave|
|--|
|![Supportato](media/green_check.png) = **Supportato**: è consigliato l'uso della versione di Windows ADK corrispondente alla versione di Windows che si intende distribuire. Ad esempio, usare Windows ADK per Windows 10 versione 1703 per la distribuzione di Windows 10 versione 1703. Per altre informazioni sul supporto del componente Windows ADK, vedere [Piattaforme supportate di Gestione e manutenzione immagini distribuzione](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) e [Requisiti USMT](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
|![Compatibile con le versioni precedenti](media/blue_compat.png)  = **Compatibile con le versioni precedenti**: questa combinazione non è stata testata ma dovrebbe funzionare. Verranno documentati eventuali problemi noti o avvertenze. |
|![Non supportato](media/Red_X.png) = **Non supportato**|

 > [!Note]
 > Configuration Manager supporta solo i componenti x86 e amd64 di Windows 10 ADK e attualmente non supporta i componenti arm e arm64. 
---
title: Supporto per Windows 10
titleSuffix: Configuration Manager
description: Informazioni sulle versioni di Windows 10 supportate come client o per la distribuzione del sistema operativo con Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a1626a65-da22-49e0-9564-d2f752ea3f4b
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f3ec5f9b9bbda3b3bec6fdd1d955b8911f8029b5
ms.sourcegitcommit: 4316bff400ffbde8404f8a2092ec17e3601b8d29
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/06/2019
ms.locfileid: "70738505"
---
# <a name="support-for-windows-10-in-configuration-manager"></a>Supporto per Windows 10 in Configuration Manager  

*Si applica a: System Center Configuration Manager (Current Branch)*

Informazioni sulle versioni di Windows 10 supportate da Configuration Manager, incluse:

- [Windows 10 come client](#windows-10-as-a-client)
- [Windows 10 ADK](#windows-10-adk)

> [!Tip]
> Sono supportate le stesse build di Windows Server come client della versione di Windows 10 associata. Ad esempio, Windows Server 2016 è la stessa versione build di Windows 10 LTSB 2016, mentre Windows Server versione 1803 è la stessa versione build di Windows 10 versione 1803.
>
> Per altre informazioni su Windows Server come sistema del sito, vedere [Sistemi operativi supportati per i server dei sistemi del sito di Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers#bkmk_core).


## <a name="windows-10-as-a-client"></a>Windows 10 come client

Configuration Manager tenta di garantire il supporto come client per ogni nuova versione di Windows 10 appena possibile dopo il rilascio. Poiché i prodotti hanno pianificazioni di sviluppo e rilascio separate, il supporto offerto da Configuration Manager dipende dalla data di disponibilità di ogni prodotto.

Una versione di Configuration Manager viene eliminata dalla matrice dopo che termina il [supporto per tale versione](/sccm/core/servers/manage/current-branch-versions-supported). Analogamente, il supporto per le versioni di Windows 10 come Enterprise 2015 LTSB o 1511 viene eliminato dalla matrice quando queste vengono rimosse dal supporto.

- L'ultima versione di Configuration Manager Current Branch riceve aggiornamenti di sicurezza e critici che possono includere la correzione dei problemi con le versioni di Windows 10. Quando Microsoft rilascia una nuova versione di Configuration Manager Current Branch, le versioni precedenti ricevono solo aggiornamenti di sicurezza. Per altre informazioni, vedere [Supporto per le versioni di System Center Configuration Manager Current Branch](/sccm/core/servers/manage/current-branch-versions-supported).  

    > [!Note]  
    > Il metodo migliore per mantenere aggiornato Windows 10 consiste nel mantenere aggiornato Configuration Manager. Per altre informazioni, vedere [Configuration Manager e Windows as a Service](/sccm/core/understand/configuration-manager-and-windows-as-service).  

- Le informazioni seguenti sono a complemento dell'articolo [Sistemi operativi supportati per client e dispositivi](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).  

- Se si usa Long-Term Servicing Branch di Configuration Manager, vedere [Configurazioni supportate per Long-Term Servicing Branch](/sccm/core/understand/supported-configurations-for-ltsb).  

<br/>
La tabella seguente elenca le versioni di Windows 10 che è possibile usare come client con versioni diverse di Configuration Manager.

| Versione di Windows 10 | Configuration Manager 1802 | Configuration Manager 1806 | Configuration Manager 1810 | Configuration Manager 1902 | Configuration Manager 1906 |
|---------------------|-----|-----|-----|-----|-----|
| Enterprise 2015 LTSB <!--10/14/2025-->   | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |
| Enterprise 2016 LTSB <!--10/13/2026-->   | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |
| Enterprise LTSC 2019 <!--01/09/2029-->   | ![Non supportato](media/Red_X.png)   | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |
| 1703   <!--10/08/2019-->   | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |
| 1709   <!--04/14/2020-->   | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |
| 1803   <!--11/10/2020-->   | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |
| 1809   <!--05/11/2021-->   | ![Non supportato](media/Red_X.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |
| 1903   <!--TBD-->   | ![Non supportato](media/Red_X.png) | ![Non supportato](media/Red_X.png) | ![Non supportato](media/Red_X.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |

<!-- lifecycle reference: https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet -->

Per altre informazioni sul ciclo di vita di Windows, vedere [Date importanti nel ciclo di vita di Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet)

> [!Note]  
> Il supporto delle versioni di canale semestrale Windows 10 include le edizioni seguenti: Enterprise, Pro, Education e Pro Education.  
>
> A partire dalla versione 1906 Configuration Manager supporta Windows 10 Pro for Workstations.

| Chiave |
|--|
| ![Supportato](media/green_check.png) = **Supportato**  |
| ![Non supportato](media/Red_X.png) = **Non supportato** |

> [!NOTE]  
> Configuration Manager supporta il client nei dispositivi ARM64 Windows 10. Le funzionalità di gestione client esistenti dovrebbero funzionare con questi nuovi dispositivi, ad esempio l'inventario hardware e software, gli aggiornamenti del software e la gestione delle applicazioni. La distribuzione del sistema operativo non è attualmente supportata. <!-- 1353704 -->


## <a name="windows-10-adk"></a>Windows 10 ADK

Quando si distribuiscono sistemi operativi con Configuration Manager, Windows ADK è una dipendenza esterna obbligatoria. Per altre informazioni, vedere [Requisiti dell'infrastruttura per la distribuzione del sistema operativo](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment#windows-adk-for-windows-10).

> [!Important]  
> A partire da Windows 10 versione 1809, Windows PE è un programma di installazione separato. Non ci sono altre differenze funzionali.

<br/>
La tabella seguente elenca le versioni di Windows ADK 10 che è possibile usare con versioni diverse di Configuration Manager.

| Versione di Windows 10 ADK  | Configuration Manager 1802 | Configuration Manager 1806 | Configuration Manager 1810 | Configuration Manager 1902 | Configuration Manager 1906 |
|--------------------|-----|-----|-----|-----|-----|
| **1703**<br>(10.1.15063) | ![Compatibile con le versioni precedenti](media/blue_compat.png) | ![Non supportato](media/Red_X.png) | ![Non supportato](media/Red_X.png) | ![Non supportato](media/Red_X.png) | ![Non supportato](media/Red_X.png) |
| **1709**<br>(10.1.16299) | ![Supportato](media/green_check.png) | ![Compatibile con le versioni precedenti](media/blue_compat.png) | ![Non supportato](media/Red_X.png)   | ![Non supportato](media/Red_X.png) | ![Non supportato](media/Red_X.png) |
| **1803**<br>(10.1.17134) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Compatibile con le versioni precedenti](media/blue_compat.png) | ![Compatibile con le versioni precedenti](media/blue_compat.png) | ![Non supportato](media/Red_X.png) |
| **1809**<br>(10.1.17763) | ![Non supportato](media/Red_X.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) | ![Compatibile con le versioni precedenti](media/blue_compat.png) |
| **1903**<br>(10.1.18362) | ![Non supportato](media/Red_X.png) | ![Non supportato](media/Red_X.png) | ![Non supportato](media/Red_X.png) | ![Supportato](media/green_check.png) | ![Supportato](media/green_check.png) |

> [!Note]  
> Configuration Manager supporta solo i componenti x86 e amd64 di Windows 10 ADK e attualmente non supporta i componenti ARM e ARM64.

|Chiave|
|--|
| ![Supportato](media/green_check.png) = **Supportato** <br/> Questa tabella mostra solo il supporto di Windows ADK in relazione alla versione di Configuration Manager. Microsoft consiglia l'uso della versione di Windows ADK corrispondente alla versione di Windows che si vuole distribuire. Quando si distribuisce la versione più recente di Windows 10, usare la versione più recente di Windows ADK. La versione più recente di Windows ADK può supportare la distribuzione di versioni del sistema operativo meno recenti, ad esempio Windows 7.<!-- SCCMDocs issue 1229 --> Per altre informazioni sul supporto del componente Windows ADK, vedere [Piattaforme supportate di Gestione e manutenzione immagini distribuzione](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) e [Requisiti USMT](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1). |
| ![Compatibile con le versioni precedenti](media/blue_compat.png)  = **Compatibile con le versioni precedenti** <br/> Questa combinazione non è stata testata ma dovrebbe funzionare. Verranno documentati eventuali problemi noti o avvertenze. |
| ![Non supportato](media/Red_X.png) = **Non supportato** |

> [!Tip]
> Le build di Windows Server hanno gli stessi requisiti Windows ADK della versione di Windows 10 associata. Ad esempio, Windows Server 2016 è la stessa versione build di Windows 10 LTSB 2016.

---
title: Creare e distribuire criteri di Windows Defender Application Guard
titleSuffix: Configuration Manager
description: Creare e distribuire criteri di Windows Defender Application Guard.
ms.custom: na
ms.date: 11/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 
caps.latest.revision: "5"
author: ErikjeMS
ms.author: erikje
manager: angrobe
ms.openlocfilehash: db2508e5bbd1435fce432b6ef98d7968e68ea5ab
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="create-and-deploy-windows-defender-application-guard-policy----1351960---"></a>Creare e distribuire criteri di Windows Defender Application Guard <!-- 1351960 -->

È possibile creare e distribuire criteri di [Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview) usando Endpoint Protection di Configuration Manager. Questi criteri consentono di proteggere gli utenti tramite l'apertura dei siti Web non attendibili in un contenitore isolato protetto e non accessibile da altre parti del sistema operativo.

## <a name="prerequisites"></a>Prerequisiti

Per creare e distribuire criteri di Windows Defender Application Guard, è necessario usare la versione Fall Creators Update di Windows 10. Inoltre, i dispositivi Windows 10 in cui verranno distribuiti i criteri devono essere configurati con criteri di isolamento di rete. Per altre informazioni, vedere [Panoramica di Windows Defender Application Guard](https://docs.microsoft.com/en-us/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview). Questa funzionalità funziona solo con le build correnti di Windows 10 Insider. Per provarla, i client devono eseguire una build recente di Windows 10 Insider.


## <a name="create-a-policy-and-to-browse-the-available-settings"></a>Creare un criterio e passare alle impostazioni disponibili:

1. Nella console di Configuration Manager scegliere **Asset e conformità**.
2. Nell'area di lavoro **Asset e conformità** scegliere **Panoramica** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea i criteri di Windows Defender Application Guard**.
4. Usando il [post di blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97) come riferimento, è possibile selezionare e configurare le impostazioni disponibili.
5. Nella pagina **Definizione di rete** specificare l'identità aziendale e definire il limite di rete aziendale.

    > [!NOTE]
    > I PC Windows 10 archiviano solo un elenco di isolamento rete nel client. È possibile creare due tipi diversi di elenchi di isolamento di rete e quindi distribuirli nel client:
    >
    >  - uno da Windows Information Protection
    >  - un altro da Windows Defender Application Guard
    >
    > Se si distribuiscono entrambi i criteri, questi elenchi di isolamento rete devono corrispondere. Se si distribuiscono elenchi che non corrispondono allo stesso client, la distribuzione avrà esito negativo. Per altre informazioni, vedere la [documentazione di Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).
    > 
    > 

6. Al termine, completare la procedura guidata e distribuire il criterio in uno o più dispositivi Windows 10.

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni su Windows Defender Application Guard, vedere [questo post di blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Per altre informazioni sulla modalità autonoma di Windows Defender Application Guard vedere [questo post di blog](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).

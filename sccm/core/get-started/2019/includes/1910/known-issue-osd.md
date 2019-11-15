---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: include
ms.date: 10/17/2019
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1a92c149de02087d7dec586769ec770f50190329
ms.sourcegitcommit: 90f51008deeabf2a434bd12f81bb25669045029c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/21/2019
ms.locfileid: "72694428"
---
### <a name="ki_osd"></a> Le sequenze di attività non sono disponibili per PXE o supporti

<!--5578298-->
Se si distribuisce una sequenza di attività per PXE o supporti (USB o DVD), il client non riceve i criteri. Il messaggio seguente si trova in **smsts.log**:

`There are no task sequences available to this computer.`

#### <a name="workaround"></a>Soluzione alternativa

Avviare la sequenza di attività da Software Center.
---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 10/17/2019
ms.openlocfilehash: 7010162cdc8ef2652e4cc560940d226813388eb3
ms.sourcegitcommit: ccc3c929b5585c05d562020e68044de7d7e11c6a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2020
ms.locfileid: "80604009"
---
### <a name="task-sequences-arent-available-to-pxe-or-media"></a><a name="ki_osd"></a> Le sequenze di attività non sono disponibili per PXE o supporti

<!--5578298-->
Se si distribuisce una sequenza di attività per PXE o supporti (USB o DVD), il client non riceve i criteri. Il messaggio seguente si trova in **smsts.log**:

`There are no task sequences available to this computer.`

#### <a name="workaround"></a>Soluzione alternativa

Avviare la sequenza di attività da Software Center.

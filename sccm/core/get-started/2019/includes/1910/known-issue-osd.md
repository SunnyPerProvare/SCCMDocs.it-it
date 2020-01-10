---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: include
ms.date: 10/17/2019
ms.openlocfilehash: 01f38845992f79d49e141c5a326c0cea1c721605
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75805974"
---
### <a name="ki_osd"></a> Le sequenze di attività non sono disponibili per PXE o supporti

<!--5578298-->
Se si distribuisce una sequenza di attività per PXE o supporti (USB o DVD), il client non riceve i criteri. Il messaggio seguente si trova in **smsts.log**:

`There are no task sequences available to this computer.`

#### <a name="workaround"></a>Soluzione alternativa

Avviare la sequenza di attività da Software Center.

---
title: Configurare l'inventario software | System Center Configuration Manager
description: Configurare l'inventario software e una cartella di esclusione di inventario in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: cc226259-0e28-410a-94d3-223bdc948818
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5f30eb754832fcc259caf853dc33ccfcb82cf8bc


---
# <a name="how-to-configure-software-inventory-in-system-center-configuration-manager"></a>Come configurare l'inventario software in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile creare un file nascosto denominato **Skpswi.dat** e inserirlo nella radice di un disco rigido del client per escluderlo dall'inventario software di System Center Configuration Manager. È anche possibile inserire questo file nella radice di qualsiasi struttura di cartelle che si vuole escludere dall'inventario software. Questa procedura può essere usata per disabilitare l'inventario software in una singola workstation o un singolo client di server, ad esempio un file server di grandi dimensioni.  

> [!NOTE]  
>  L'inventario software non effettua l'inventario dell'unità del client a meno che questo file non venga eliminato dall'unità nel computer client.  

### <a name="to-exclude-folders-from-software-inventory"></a>Per escludere cartelle dall'inventario software  

1.  Usando Notepad.exe, creare un file vuoto denominato **Skpswi.dat**.  

2.  Fare clic con il pulsante destro del mouse sul file **Skpswi.dat** e quindi scegliere **Proprietà**. Nelle proprietà per il file Skpswi.dat selezionare l'attributo **Hidden** .  

3.  Inserire il file **Skpswi.dat** nella radice di ogni disco rigido o struttura di cartelle del client che si vuole escludere dall'inventario software.  



<!--HONumber=Nov16_HO1-->


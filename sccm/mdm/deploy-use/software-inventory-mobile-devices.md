---
title: Inventario software per dispositivi mobili registrati con Microsoft Intune
titleSuffix: Configuration Manager
description: Inventario software per dispositivi mobili registrati con Microsoft Intune.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0eae17a-60a8-4132-91af-0b10ad338c92
caps.latest.revision: "18"
caps.handback.revision: "0"
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: c0a583de1a0b24bd31c0d55c1acb54f480bb4230
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Inventario software per dispositivi mobili registrati con Microsoft Intune

*Si applica a: System Center Configuration Manager (Current Branch)*

 È possibile raccogliere l'inventario per le app installate in dispositivi mobili. Le app vengono inserite nell'inventario a seconda che il dispositivo sia di proprietà dell'azienda o personale. Per quanto riguarda i dispositivi personali, le uniche app che vengono inserite nell'inventario sono quelle gestite da Microsoft Intune.  

> [!NOTE]  
>  L'inventario per le app installate in dispositivi mobili viene eseguito nell'ambito del processo di [inventario hardware](mobile-device-hardware-inventory-hybrid.md).  

 Queste sono le app incluse nell'inventario per i dispositivi personali o di proprietà dell'azienda.  

|Piattaforma|Per i dispositivi di proprietà personale|Per i dispositivi di proprietà dell'azienda|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10 senza il client di Configuration Manager|Solo le app gestite|Solo le app gestite|
|Windows 8.1 senza il client di Configuration Manager|Solo le app gestite|Solo le app gestite|  
|Windows Phone 8|Solo le app gestite|Solo le app gestite|  
|Windows RT|Solo le app gestite|Solo le app gestite|  
|iOS|Solo le app gestite|Tutte le app installate nel dispositivo|  
|Android|Solo le app gestite|Tutte le app installate nel dispositivo|  

Per informazioni dettagliate sull'uso dell'inventario software per raccogliere informazioni sui file nei dispositivi client, vedere [Introduzione all'inventario software](../../core/clients/manage/inventory/introduction-to-software-inventory.md) e [Come configurare l'inventario software ](../../core/clients/manage/inventory/configure-software-inventory.md).

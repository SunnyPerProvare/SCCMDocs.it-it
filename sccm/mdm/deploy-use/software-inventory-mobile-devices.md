---
title: Inventario software per dispositivi mobili registrati con Microsoft Intune
titleSuffix: Configuration Manager
description: Inventario software per dispositivi mobili registrati con Microsoft Intune.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: a0eae17a-60a8-4132-91af-0b10ad338c92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c4ae28910772a3a615a87f130b4fa5114e2a6117
ms.sourcegitcommit: 7f64c5fb3e9fa3dba006af618b1f1ceaf61a99f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/28/2019
ms.locfileid: "75519743"
---
# <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Inventario software per dispositivi mobili registrati con Microsoft Intune

*Si applica a: Configuration Manager (Current Branch)*

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

Vedere [Introduzione all'inventario software](../../core/clients/manage/inventory/introduction-to-software-inventory.md) e [come configurare l'inventario software](../../core/clients/manage/inventory/configure-software-inventory.md) per informazioni dettagliate sull'uso dell'inventario software per raccogliere informazioni sui file nei dispositivi client.

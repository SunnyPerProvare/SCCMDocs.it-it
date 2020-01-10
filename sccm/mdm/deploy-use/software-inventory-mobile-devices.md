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
ms.openlocfilehash: d7e2cc186cbb3ac6c5ea251ea71061803366f429
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75826561"
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

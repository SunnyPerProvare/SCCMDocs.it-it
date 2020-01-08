---
title: Configurare l'inventario hardware per dispositivi mobili
titleSuffix: Configuration Manager
description: Configurare l'inventario hardware per i dispositivi mobili registrati da Microsoft Intune e Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 78a0aecc-f775-451e-aa05-56377ec91b1f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1dea53c3d98870d225df860a7b1f2ea7a43741f1
ms.sourcegitcommit: 7f64c5fb3e9fa3dba006af618b1f1ceaf61a99f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/28/2019
ms.locfileid: "75520151"
---
# <a name="how-to-configure-hardware-inventory-for-mobile-devices-enrolled-by-microsoft-intune-and-configuration-manager"></a>Come configurare l'inventario hardware per i dispositivi mobili registrati tramite Microsoft Intune e Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

In Configuration Manager è possibile raccogliere l'inventario hardware nei dispositivi iOS, Android e Windows usando il connettore Microsoft Intune. Per informazioni su come configurare l'inventario hardware, vedere [come estendere l'inventario hardware](../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 Per informazioni su come registrare i dispositivi in Microsoft Intune, vedere [Gestire i dispositivi mobili con Microsoft Intune](https://technet.microsoft.com/library/dn646962.aspx).  

## <a name="hardware-inventory-for-mobile-devices"></a>Inventario hardware per dispositivi mobili  
 Nelle tabelle seguenti sono elencate le classi di inventario disponibili per l'inventario hardware nelle piattaforme per dispositivi mobili più comuni.  

 **iOS**  

|Classe di inventario hardware|iOS|  
|------------------------------|---------|  
|Name|Device_ComputerSystem.DeviceName|  
|ID univoco del dispositivo|Device_ComputerSystem.UDID|  
|Numero di serie|Device_ComputerSystem.SerialNumber|  
|Indirizzo E-mail|Device_Email.OwnerEmailAddress|  
|Tipo di sistema operativo|Not applicable|  
|Versione del sistema operativo|Device_OSInformation.OSVersion|  
|Versione build|Not applicable|  
|Versione principale del Service Pack|Not applicable|  
|Versione secondaria del Service Pack|Not applicable|  
|Lingua del sistema operativo|Not applicable|  
|Spazio di archiviazione totale|Device_Memory.DeviceCapacity|  
|Spazio di archiviazione disponibile|Device_Memory.AvailableDeviceCapacity|  
|Identità internazionale apparecchiature mobili (IMEI)|Device_ComputerSystem.IMEI|  
|Identificativo di apparecchiatura mobile (MEID)|Device_ComputerSystem.MEID|  
|Produttore|Not applicable|  
|Modello|ModelName|  
|Numero di telefono<sup>1</sup>|Device_ComputerSystem.PhoneNumber|  
|Gestore sottoscrizione|Device_ComputerSystem.SubscriberCarrierNetwork|  
|Tecnologia cellulare|Device_ComputerSystem.CellularTechnology|  
|MAC Wi-Fi|Device_WLAN.WiFiMAC|  

 **Android**  

> [!NOTE]  
>  **NOTA:** le classi di inventario Android sono disponibili quando si usa l'app del portale aziendale Android.  

|Classe di inventario hardware|Android|  
|------------------------------|-------------|  
|Name|Not applicable|  
|ID univoco del dispositivo|Not applicable|  
|Numero di serie|Device_ComputerSystem.SerialNumber|  
|Indirizzo E-mail|Not applicable|  
|Tipo di sistema operativo|Device_OSInformation.Platform|  
|Versione del sistema operativo|Device_OSInformation.Version|  
|Versione build|Not applicable|  
|Versione principale del Service Pack|Not applicable|  
|Versione secondaria del Service Pack|Not applicable|  
|Lingua del sistema operativo|Not applicable|  
|Spazio di archiviazione totale|Device_Memory.StorageTotal|  
|Spazio di archiviazione disponibile|Device_Memory.StorageFree|  
|Identità internazionale apparecchiature mobili (IMEI)|Device_ComputerSystem.IMEI|  
|Identificativo di apparecchiatura mobile (MEID)|Not applicable|  
|Produttore|Device_Info.Manufacturer|  
|Modello|Device_Info.Model|  
|Numero di telefono<sup>1</sup>|Device_ComputerSystem.PhoneNumber|  
|Gestore sottoscrizione|Device_ComputerSystem.SubscriberCarrierNetwork|  
|Tecnologia cellulare|Device_ComputerSystem.CellularTechnology|  
|MAC Wi-Fi|Device_WLAN.WiFiMAC|  

 **Windows Phone 8/8.1**  

|Classe di inventario hardware|Windows Phone 8 e Windows Phone 8.1|  
|------------------------------|-------------------------------------------|  
|Name|Device_ComputerSystem.DeviceName|  
|ID univoco del dispositivo|Device_ComputerSystem.DeviceClientID|  
|Numero di serie|Not applicable|  
|Indirizzo E-mail|Device_Email.OwnerEmailAddress|  
|Tipo di sistema operativo|Device_OSInformation.Platform|  
|Versione del sistema operativo|Device_ComputerSystem.SoftwareVersion|  
|Versione build|Not applicable|  
|Versione principale del Service Pack|Not applicable|  
|Versione secondaria del Service Pack|Not applicable|  
|Lingua del sistema operativo|Device_OSInformation.Language|  
|Spazio di archiviazione totale|Not applicable|  
|Spazio di archiviazione disponibile|Not applicable|  
|Identità internazionale apparecchiature mobili (IMEI)|Not applicable|  
|Identificativo di apparecchiatura mobile (MEID)|Not applicable|  
|Produttore|Device_ComputerSystem.DeviceManufacturer|  
|Modello|Device_ComputerSystem.DeviceModel|  
|Numero di telefono<sup>1</sup>|Not applicable|  
|Gestore sottoscrizione|Not applicable|  
|Tecnologia cellulare|Not applicable|  
|MAC Wi-Fi|Not applicable|  

 **Windows RT**  

|Classe di inventario hardware|Windows RT|  
|------------------------------|----------------|  
|Name|Device_ComputerSystem.DeviceName|  
|ID univoco del dispositivo|Device_ComputerSystem.DeviceName|  
|Numero di serie|Not applicable|  
|Indirizzo E-mail|Device_Email.OwnerEmailAddress|  
|Tipo di sistema operativo|CCM_OperatingSystem.SystemType|  
|Versione del sistema operativo|Win32_OperatingSystem.Version|  
|Versione build|Win32_OperatingSystem.BuildNumber|  
|Versione principale del Service Pack|Win32_OperatingSystem.ServicePackMajorVersion|  
|Versione secondaria del Service Pack|Win32_OperatingSystem.ServicePackMinorVersion|  
|Lingua del sistema operativo|Not applicable|  
|Spazio di archiviazione totale|Win32_PhysicalMemory.Capacity|  
|Spazio di archiviazione disponibile|Win32_OperatingSystem.FreePhysicalMemory|  
|Identità internazionale apparecchiature mobili (IMEI)|Not applicable|  
|Identificativo di apparecchiatura mobile (MEID)|Not applicable|  
|Produttore|Win32_ComputerSystem.Manufacturer|  
|Modello|Win32_ComputerSystem.Model|  
|Numero di telefono<sup>1</sup>|Not applicable|  
|Gestore sottoscrizione|Not applicable|  
|Tecnologia cellulare|Not applicable|  
|MAC Wi-Fi|Win32_NetworkAdapter.MACAddress|  

 <sup>1</sup> Il numero di telefono viene nascosto con * tranne le ultime 4 cifre.  

 Affinché l'inventario possa ottenere il numero di telefono, il dispositivo deve disporre di una scheda SIM e di un numero di telefono fornito dal gestore telefonico.  

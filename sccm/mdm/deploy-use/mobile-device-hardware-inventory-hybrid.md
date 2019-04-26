---
title: Configurare l'inventario hardware per dispositivi mobili
titleSuffix: Configuration Manager
description: Configurare l'inventario hardware per i dispositivi mobili registrati da Microsoft Intune e System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 78a0aecc-f775-451e-aa05-56377ec91b1f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d1a208b3bac5d0b12a9fd395506f02d283a0b55f
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62228247"
---
# <a name="how-to-configure-hardware-inventory-for-mobile-devices-enrolled-by-microsoft-intune-and-system-center-configuration-manager"></a>Come configurare l'inventario hardware per i dispositivi mobili registrati tramite Microsoft Intune e System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In Configuration Manager è possibile raccogliere l'inventario hardware nei dispositivi iOS, Android e Windows usando il connettore Microsoft Intune. Per informazioni su come configurare l'inventario hardware, vedere [Come estendere l'inventario hardware in System Center Configuration Manager](../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 Per informazioni su come registrare i dispositivi in Microsoft Intune, vedere [Gestire i dispositivi mobili con Microsoft Intune](https://technet.microsoft.com/library/dn646962.aspx).  

## <a name="hardware-inventory-for-mobile-devices"></a>Inventario hardware per dispositivi mobili  
 Nelle tabelle seguenti sono elencate le classi di inventario disponibili per l'inventario hardware nelle piattaforme per dispositivi mobili più comuni.  

 **iOS**  

|Classe di inventario hardware|iOS|  
|------------------------------|---------|  
|Name|Device_ComputerSystem.DeviceName|  
|ID univoco del dispositivo|Device_ComputerSystem.UDID|  
|Numero di serie|Device_ComputerSystem.SerialNumber|  
|Indirizzo di posta elettronica|Device_Email.OwnerEmailAddress|  
|Tipo di sistema operativo|Non applicabile|  
|Versione del sistema operativo|Device_OSInformation.OSVersion|  
|Versione build|Non applicabile|  
|Versione principale del Service Pack|Non applicabile|  
|Versione secondaria del Service Pack|Non applicabile|  
|Lingua del sistema operativo|Non applicabile|  
|Spazio di archiviazione totale|Device_Memory.DeviceCapacity|  
|Spazio di archiviazione disponibile|Device_Memory.AvailableDeviceCapacity|  
|Identità internazionale apparecchiature mobili (IMEI)|Device_ComputerSystem.IMEI|  
|Identificativo di apparecchiatura mobile (MEID)|Device_ComputerSystem.MEID|  
|Produttore|Non applicabile|  
|Modello|ModelName|  
|Numero di telefono<sup>1</sup>|Device_ComputerSystem.PhoneNumber|  
|Gestore sottoscrizione|Device_ComputerSystem.SubscriberCarrierNetwork|  
|Tecnologia cellulare|Device_ComputerSystem.CellularTechnology|  
|MAC Wi-Fi|Device_WLAN.WiFiMAC|  

 **Android**  

> [!NOTE]  
>  **NOTA:** Classi di inventario Android sono disponibili quando si usa l'app portale aziendale per Android.  

|Classe di inventario hardware|Android|  
|------------------------------|-------------|  
|Name|Non applicabile|  
|ID univoco del dispositivo|Non applicabile|  
|Numero di serie|Device_ComputerSystem.SerialNumber|  
|Indirizzo di posta elettronica|Non applicabile|  
|Tipo di sistema operativo|Device_OSInformation.Platform|  
|Versione del sistema operativo|Device_OSInformation.Version|  
|Versione build|Non applicabile|  
|Versione principale del Service Pack|Non applicabile|  
|Versione secondaria del Service Pack|Non applicabile|  
|Lingua del sistema operativo|Non applicabile|  
|Spazio di archiviazione totale|Device_Memory.StorageTotal|  
|Spazio di archiviazione disponibile|Device_Memory.StorageFree|  
|Identità internazionale apparecchiature mobili (IMEI)|Device_ComputerSystem.IMEI|  
|Identificativo di apparecchiatura mobile (MEID)|Non applicabile|  
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
|Numero di serie|Non applicabile|  
|Indirizzo di posta elettronica|Device_Email.OwnerEmailAddress|  
|Tipo di sistema operativo|Device_OSInformation.Platform|  
|Versione del sistema operativo|Device_ComputerSystem.SoftwareVersion|  
|Versione build|Non applicabile|  
|Versione principale del Service Pack|Non applicabile|  
|Versione secondaria del Service Pack|Non applicabile|  
|Lingua del sistema operativo|Device_OSInformation.Language|  
|Spazio di archiviazione totale|Non applicabile|  
|Spazio di archiviazione disponibile|Non applicabile|  
|Identità internazionale apparecchiature mobili (IMEI)|Non applicabile|  
|Identificativo di apparecchiatura mobile (MEID)|Non applicabile|  
|Produttore|Device_ComputerSystem.DeviceManufacturer|  
|Modello|Device_ComputerSystem.DeviceModel|  
|Numero di telefono<sup>1</sup>|Non applicabile|  
|Gestore sottoscrizione|Non applicabile|  
|Tecnologia cellulare|Non applicabile|  
|MAC Wi-Fi|Non applicabile|  

 **Windows RT**  

|Classe di inventario hardware|Windows RT|  
|------------------------------|----------------|  
|Name|Device_ComputerSystem.DeviceName|  
|ID univoco del dispositivo|Device_ComputerSystem.DeviceName|  
|Numero di serie|Non applicabile|  
|Indirizzo di posta elettronica|Device_Email.OwnerEmailAddress|  
|Tipo di sistema operativo|CCM_OperatingSystem.SystemType|  
|Versione del sistema operativo|Win32_OperatingSystem.Version|  
|Versione build|Win32_OperatingSystem.BuildNumber|  
|Versione principale del Service Pack|Win32_OperatingSystem.ServicePackMajorVersion|  
|Versione secondaria del Service Pack|Win32_OperatingSystem.ServicePackMinorVersion|  
|Lingua del sistema operativo|Non applicabile|  
|Spazio di archiviazione totale|Win32_PhysicalMemory.Capacity|  
|Spazio di archiviazione disponibile|Win32_OperatingSystem.FreePhysicalMemory|  
|Identità internazionale apparecchiature mobili (IMEI)|Non applicabile|  
|Identificativo di apparecchiatura mobile (MEID)|Non applicabile|  
|Produttore|Win32_ComputerSystem.Manufacturer|  
|Modello|Win32_ComputerSystem.Model|  
|Numero di telefono<sup>1</sup>|Non applicabile|  
|Gestore sottoscrizione|Non applicabile|  
|Tecnologia cellulare|Non applicabile|  
|MAC Wi-Fi|Win32_NetworkAdapter.MACAddress|  

 <sup>1</sup> Il numero di telefono viene nascosto con * tranne le ultime 4 cifre.  

 Affinché l'inventario possa ottenere il numero di telefono, il dispositivo deve disporre di una scheda SIM e di un numero di telefono fornito dal gestore telefonico.  

---
title: Configurare l&quot;inventario hardware | Microsoft Docs | dispositivi mobili
description: Configurare l&quot;inventario hardware per i dispositivi mobili registrati da Microsoft Intune e System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 78a0aecc-f775-451e-aa05-56377ec91b1f
caps.latest.revision: 7
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 6db22a2ddce1afb471cf8b603c6d98f7f0acbc15


---
# <a name="how-to-configure-hardware-inventory-for-mobile-devices-enrolled-by-microsoft-intune-and-system-center-configuration-manager"></a>Come configurare l'inventario hardware per i dispositivi mobili registrati tramite Microsoft Intune e System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager è possibile raccogliere l'inventario hardware nei dispositivi iOS, Android e Windows usando il connettore Microsoft Intune. Per informazioni su come configurare l'inventario hardware, vedere [Come estendere l'inventario hardware in System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

 Per informazioni su come registrare i dispositivi con Microsoft Intune, vedere [Gestire i dispositivi mobili con Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).  

## <a name="hardware-inventory-for-mobile-devices"></a>Inventario hardware per dispositivi mobili  
 Nelle tabelle seguenti sono elencate le classi di inventario disponibili per l'inventario hardware nelle piattaforme per dispositivi mobili più comuni.  

 **iOS**  

|Classe di inventario hardware|iOS|  
|------------------------------|---------|  
|Nome|Device_ComputerSystem.DeviceName|  
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
>  **NOTA:** le classi di inventario Android sono disponibili quando si usa l'app del portale aziendale Android.  

|Classe di inventario hardware|Android|  
|------------------------------|-------------|  
|Nome|Non applicabile|  
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
|Nome|Device_ComputerSystem.DeviceName|  
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
|Nome|Device_ComputerSystem.DeviceName|  
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



<!--HONumber=Dec16_HO3-->



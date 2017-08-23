---
title: "ハードウェア インベントリの構成 | Microsoft Docs | モバイル デバイス"
description: "Microsoft Intune と System Center Configuration Manager によって登録されたモバイル デバイス用のハードウェア インベントリを構成します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 78a0aecc-f775-451e-aa05-56377ec91b1f
caps.latest.revision: "7"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 7ab9042a525e07b8e3107479cedeec6b99f7bc86
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-hardware-inventory-for-mobile-devices-enrolled-by-microsoft-intune-and-system-center-configuration-manager"></a>System Center Configuration Manager と Microsoft Intune で登録されたモバイル デバイスのハードウェア インベントリを構成する方法

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager では、Microsoft Intune コネクタを使って、iOS、Android、および Windows デバイスのハードウェア インベントリを収集することができます。 カスタム ハードウェア インベントリを構成する方法については、「[System Center Configuration Manager でのハードウェア インベントリの拡張方法](../../core/clients/manage/inventory/extend-hardware-inventory.md)」を参照してください。  

 Microsoft Intune にデバイスを登録する方法については、「[Microsoft Intune を使用してモバイル デバイスを管理する](https://technet.microsoft.com/en-us/library/dn646962.aspx)」を参照してください。  

## <a name="hardware-inventory-for-mobile-devices"></a>モバイル デバイスのハードウェア インベントリ  
 次の表は、一般的に使用されるモバイル プラットフォームのハードウェア インベントリに使用できるインベントリ クラスの一覧です。  

 **iOS**  

|ハードウェア インベントリ クラス|iOS|  
|------------------------------|---------|  
|名前|Device_ComputerSystem.DeviceName|  
|一意のデバイス ID|Device_ComputerSystem.UDID|  
|シリアル番号|Device_ComputerSystem.SerialNumber|  
|電子メール アドレス|Device_Email.OwnerEmailAddress|  
|オペレーティング システムの種類|該当なし|  
|オペレーティング システムのバージョン|Device_OSInformation.OSVersion|  
|ビルド バージョン|該当なし|  
|Service Pack メジャー バージョン|該当なし|  
|Service Pack マイナー バージョン|該当なし|  
|オペレーティング システムの言語|該当なし|  
|記憶域の合計容量|Device_Memory.DeviceCapacity|  
|記憶域の空き容量|Device_Memory.AvailableDeviceCapacity|  
|International Mobile Equipment Identity または IMEI (IMEI)|Device_ComputerSystem.IMEI|  
|Mobile Equipment Identifier (MEID)|Device_ComputerSystem.MEID|  
|製造元|該当なし|  
|モデル|ModelName|  
|電話番号<sup>1</sup>|Device_ComputerSystem.PhoneNumber|  
|通信事業者|Device_ComputerSystem.SubscriberCarrierNetwork|  
|通信方式|Device_ComputerSystem.CellularTechnology|  
|Wi-Fi MAC|Device_WLAN.WiFiMAC|  

 **Outlook Web Access (OWA)**  

> [!NOTE]  
>  **注:** Android インベントリ クラスは、Android 用ポータル サイト アプリ使用時にのみ使用できます。  

|ハードウェア インベントリ クラス|Android|  
|------------------------------|-------------|  
|名前|該当なし|  
|一意のデバイス ID|該当なし|  
|シリアル番号|Device_ComputerSystem.SerialNumber|  
|電子メール アドレス|該当なし|  
|オペレーティング システムの種類|Device_OSInformation.Platform|  
|オペレーティング システムのバージョン|Device_OSInformation.Version|  
|ビルド バージョン|該当なし|  
|Service Pack メジャー バージョン|該当なし|  
|Service Pack マイナー バージョン|該当なし|  
|オペレーティング システムの言語|該当なし|  
|記憶域の合計容量|Device_Memory.StorageTotal|  
|記憶域の空き容量|Device_Memory.StorageFree|  
|International Mobile Equipment Identity または IMEI (IMEI)|Device_ComputerSystem.IMEI|  
|Mobile Equipment Identifier (MEID)|該当なし|  
|製造元|Device_Info.Manufacturer|  
|モデル|Device_Info.Model|  
|電話番号<sup>1</sup>|Device_ComputerSystem.PhoneNumber|  
|通信事業者|Device_ComputerSystem.SubscriberCarrierNetwork|  
|通信方式|Device_ComputerSystem.CellularTechnology|  
|Wi-Fi MAC|Device_WLAN.WiFiMAC|  

 **Windows Phone 8/8.1**  

|ハードウェア インベントリ クラス|Windows Phone 8 および Windows Phone 8.1|  
|------------------------------|-------------------------------------------|  
|名前|Device_ComputerSystem.DeviceName|  
|一意のデバイス ID|Device_ComputerSystem.DeviceClientID|  
|シリアル番号|該当なし|  
|電子メール アドレス|Device_Email.OwnerEmailAddress|  
|オペレーティング システムの種類|Device_OSInformation.Platform|  
|オペレーティング システムのバージョン|Device_ComputerSystem.SoftwareVersion|  
|ビルド バージョン|該当なし|  
|Service Pack メジャー バージョン|該当なし|  
|Service Pack マイナー バージョン|該当なし|  
|オペレーティング システムの言語|Device_OSInformation.Language|  
|記憶域の合計容量|該当なし|  
|記憶域の空き容量|該当なし|  
|International Mobile Equipment Identity または IMEI (IMEI)|該当なし|  
|Mobile Equipment Identifier (MEID)|該当なし|  
|製造元|Device_ComputerSystem.DeviceManufacturer|  
|モデル|Device_ComputerSystem.DeviceModel|  
|電話番号<sup>1</sup>|該当なし|  
|通信事業者|該当なし|  
|通信方式|該当なし|  
|Wi-Fi MAC|該当なし|  

 **Windows RT**  

|ハードウェア インベントリ クラス|Windows RT|  
|------------------------------|----------------|  
|名前|Device_ComputerSystem.DeviceName|  
|一意のデバイス ID|Device_ComputerSystem.DeviceName|  
|シリアル番号|該当なし|  
|電子メール アドレス|Device_Email.OwnerEmailAddress|  
|オペレーティング システムの種類|CCM_OperatingSystem .SystemType|  
|オペレーティング システムのバージョン|Win32_OperatingSystem.Version|  
|ビルド バージョン|Win32_OperatingSystem.BuildNumber|  
|Service Pack メジャー バージョン|Win32_OperatingSystem.ServicePackMajorVersion|  
|Service Pack マイナー バージョン|Win32_OperatingSystem.ServicePackMinorVersion|  
|オペレーティング システムの言語|該当なし|  
|記憶域の合計容量|Win32_PhysicalMemory.Capacity|  
|記憶域の空き容量|Win32_OperatingSystem.FreePhysicalMemory|  
|International Mobile Equipment Identity または IMEI (IMEI)|該当なし|  
|Mobile Equipment Identifier (MEID)|該当なし|  
|製造元|Win32_ComputerSystem.Manufacturer|  
|モデル|Win32_ComputerSystem.Model|  
|電話番号<sup>1</sup>|該当なし|  
|通信事業者|該当なし|  
|通信方式|該当なし|  
|Wi-Fi MAC|Win32_NetworkAdapter.MACAddress|  

 <sup>1</sup> 電話番号は、下 4 桁を除き * で代替表示されます。  

 電話番号を収集するインベントリの場合、デバイスには SIM カードが挿入されており、その SIM にはキャリアから提供された電話番号が格納されている必要があります。  

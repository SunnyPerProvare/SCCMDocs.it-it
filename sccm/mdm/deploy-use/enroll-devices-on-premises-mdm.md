---
title: "デバイスの登録 | Microsoft Docs"
description: "System Center Configuration Manager でのオンプレミス モバイル デバイス管理の対象となるデバイスを登録する方法について説明します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
caps.latest.revision: "6"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 4abaef35969ef1a5340ae8ca8aa5699cd3942642
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="enroll-devices-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>System Center Configuration Manager でのオンプレミス モバイル デバイス管理の対象となるデバイスの登録

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のオンプレミス モバイル デバイス管理を使用してコンピューターとデバイスを管理するには、Configuration Manager がデバイスと通信して管理タスクを実行できるように、デバイスを登録する必要があります。 Configuration Manager には、デバイスを登録する 2 つの方法があります。  

-   **ユーザー登録** - この方法では、ユーザーが自分のデバイスで登録プロセスを開始します。 ユーザー登録を正常に行うには、信頼されたルート証明書がデバイスにインストールされている必要があります。また、ユーザーは登録のために Configuration Manager によってプロビジョニングされている必要があります。  デバイスを登録するために、ユーザーは作業の資格情報を提供するだけで、そのデバイスは管理の対象として登録されます。  

     詳細については、「[System Center Configuration Manager でのオンプレミス モバイル デバイス管理の対象となるデバイスをユーザーが登録する方法](../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)」をご覧ください。  

-   **一括登録** - この方法では、デバイスのユーザーが登録を開始する必要はありません。 代わりに、Configuration Manager で一括登録パッケージが作成され、デバイス上に配置され、開かれます。 パッケージが開かれると、デバイスを登録するために必要な情報が提供されます。  

     詳細については、「[System Center Configuration Manager オンプレミス モバイル デバイス管理を使ったデバイスの一括登録の方法](../../mdm/deploy-use/bulk-enroll-devices-on-premises-mdm.md)」をご覧ください。  

 > [!NOTE]  
>  Configuration Manager の現在のブランチでは、次のオペレーティング システムを実行しているデバイスをオンプレミス モバイル デバイス管理で登録することができます。  
>   
>  -   Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team 
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise   

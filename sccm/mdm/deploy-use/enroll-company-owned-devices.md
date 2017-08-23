---
title: "会社所有のデバイスを登録する - Configuration Manager | Microsoft Docs"
description: "Configuration Manager を使用してハイブリッド展開用に会社所有のデバイスを登録するさまざまな方法について説明します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2754ce6-1460-4ddd-9050-2cc87e7964f4
caps.latest.revision: "13"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: f0b503d8c9eba2dd1b6eb4c41ec40c001b727326
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="enroll-company-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>Configuration Manager を使用してハイブリッド展開用に会社所有のデバイスを登録する

*適用対象: System Center Configuration Manager (Current Branch)*

組織または会社所有のデバイス (COD) は、デバイスおよびその購入方法に応じて、さまざまな方法で管理対象に含めることができます。  

## <a name="enroll-device-enrollment-program-ios-devices"></a>Device Enrollment Program による iOS デバイスの登録  
 Apple の Device Enrollment Program を通じて購入したデバイスに対し、無線による登録プロファイルの展開を行います。 ユーザーがデバイス上でセットアップ アシスタントを実行すると、そのデバイスが Intune に登録されます。  DEP を使用して登録したデバイスの場合は、ユーザーが登録を解除することはできません。 「[Configuration Manager とのハイブリッド展開に対応する iOS Device Enrollment Program (DEP) 登録](../../mdm/deploy-use/ios-device-enrollment-program-for-hybrid.md)」をご覧ください。  

## <a name="enroll-ios-devices-with-apple-configurator"></a>Apple Configurator による iOS デバイスの登録  
 この方法では、管理者は、Apple Configurator を実行している Mac コンピューターに iOS デバイスを USB 経由で接続し、登録を事前構成する必要があります。 その後、デバイスは、セットアップ アシスタント プロセスを実行するユーザーに届けられ、そのユーザーの所属する職場や学校の資格情報を使用して構成されて、登録プロセスを完了します。 「[Apple Configurator と Configuration Manager を使用した iOS ハイブリッド登録](../../mdm/deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)」をご覧ください。  

## <a name="device-enrollment-manager"></a>デバイス登録マネージャー  
 組織は Intune を使用して、デバイス登録マネージャー アカウントと呼ばれる単一のユーザー アカウントで多数のモバイル デバイスを管理することができます。 デバイス登録マネージャー アカウントを作成すると、そのアカウントをマネージャーが使用して、通常のユーザーに既定で許可されている標準の 5 台を超えるデバイスを登録することができます。 デバイス登録マネージャーを使用したデバイスの登録は、特定のユーザーが使用していないデバイスに対してのみ機能します。 これらのデバイスは、たとえば販売時点管理 (POS) アプリやユーティリティ アプリには適していますが、電子メールや会社のリソースにアクセスする必要があるユーザーには適していません。 「[デバイス登録マネージャーと Configuration Manager を使用したデバイスの登録](../../mdm/deploy-use/enroll-devices-with-device-enrollment-manager.md)」をご覧ください。  

## <a name="user-affinity-for-managed-devices"></a>管理対象デバイスのユーザー アフィニティ  
 管理者は会社所有のデバイスのプロファイルを構成するときに、管理対象デバイスが*ユーザー アフィニティ*をサポートするかどうかを指定できます (ユーザー アフィニティはデバイスで特定のユーザーを識別します)。 **ユーザー アフィニティ**が構成されているデバイスは、会社のポータル アプリをインストールして実行することにより、アプリをダウンロードしてデバイスを管理できるようになります。 「[Configuration Manager でのハイブリッド管理のデバイス向けユーザー アフィニティ](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md)」をご覧ください。  

## <a name="manage-devices-with-activation-lock"></a>アクティブ化ロックによるデバイスの管理  
 Microsoft Intune は、iOS 7.1 以降のデバイス向けの iPhone を探すアプリの機能である iOS のアクティベーション ロックを管理するために役立ちます。 iPhone を探すアプリをデバイスで使用すると、アクティブ化ロックが自動的に有効になります。 「[System Center Configuration Manager を使用した iOS のアクティベーション ロックの管理](../../mdm/deploy-use/manage-ios-activation-lock.md)」をご覧ください。

 ## <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>IMEI または iOS シリアル番号によるデバイスの事前宣言

会社所有のデバイスの International station Mobile Equipment Identity (IMEI) 番号または iOS シリアル番号をインポートすることで、それらのデバイスを識別できます。 デバイスの IMEI 番号を含むコンマ区切り値 (.csv) ファイルをアップロードするか、デバイス情報を手動で入力することができます。  「[Predeclare devices with hardware ID numbers](../../mdm/deploy-use/predeclare-devices-with-hardware-id.md)」 (ハードウェア ID 番号によるデバイスの事前宣言) をご覧ください。

---
title: "ハイブリッド MDM のデバイス登録方法 | Microsoft Docs"
description: "ハイブリッド MDM のデバイス登録方法です。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b81d06dc-3844-4117-9937-16732a227994
caps.latest.revision: "9"
caps.handback.revision: "0"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: e09e639e939b846cdc162681f9d7bd4c39cd6fbf
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="overview-of-device-enrollment-methods"></a>デバイス登録方法の概要

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager を Intune を利用して拡張すると、会社所有のデバイスを登録して管理したり、ユーザーに個人デバイスの登録許可を与えたりできます。 Intune を使用する会社所有のデバイスを、Configuration Manager を使用して管理することもできます。

次の表は、登録方法とサポートされている機能をまとめたものです。 含まれる機能:
- **ワイプ** - デバイスを出荷時の設定に戻します。すべてのデータが削除されます。 [デバイスをインベントリから削除する](../deploy-use/wipe-lock-reset-devices.md)
- **アフィニティ** - ユーザーとデバイスを関連付けます。 モバイル アプリケーション管理 (MAM) と会社データへの制限付きアクセスのために必要です。 [ユーザー アフィニティ](../deploy-use/user-affinity-for-hybrid-managed-devices.md)
- **ロック** ユーザーが管理からデバイスを削除できないようにします。 iOS デバイスの場合、ロックには監視モードが必要になります。 [リモート ロック](../deploy-use/wipe-lock-reset-devices.md#remote-lock)

**iOS 登録方法**

| **方法** |  **ワイプ** |  **アフィニティ**    |   **ロック** | **詳細** |
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | いいえ|    [はい] |   × | [詳細](../deploy-use/enable-platform-enrollment.md)|
|**[DEM](#dem)**|   いいえ |いいえ |×  | [詳細](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|
|**[DEP](#dep)**|   ○ |   オプション |  オプション|[詳細](../deploy-use/ios-device-enrollment-program-for-hybrid.md)|
|**[USB-SA](#usb-sa)**| ○ |   オプション |  いいえ| [詳細](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)|

**Windows と Android の登録方法**

| **方法** |  **ワイプ** |  **アフィニティ**    |   **ロック** | **詳細**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | いいえ|    [はい] |   × | [詳細](../deploy-use/enroll-hybrid-windows.md)|
|**[DEM](#dem)**|   いいえ |いいえ |×  |[詳細](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|

適切な方法を見つけるのに役立つ質問集が「[Choose how to enroll devices](/intune/get-started/choose-how-to-enroll-devices1)」 (デバイスの登録方法を選択する) にあります。

## <a name="byod"></a>BYOD
"Bring your own device" (BYOD) ユーザーは会社のポータル アプリをインストールし、自分のデバイスを登録します。 ドメインまたは Azure Active Directory に参加し、会社のネットワークに接続できます。 BYOD 登録を有効にすることは、ほとんどのプラットフォームで、さまざまな COD シナリオの前提条件になります。 「[Setup hybrid MDM](../deploy-use/setup-hybrid-mdm.md)」 (ハイブリッド MDM のセットアップ) を参照してください。 ([テーブルに戻る](#overview-of-device-enrollment-methods))

## <a name="corporate-owned-devices"></a>企業所有のデバイス
企業所有のデバイス (COD) は、Configuration Manager コンソールで管理できます。 iOS デバイスは、Apple から提供されるツールを使用して直接登録できます。 デバイス登録マネージャーを利用することで、監理者とマネージャーはあらゆる種類のデバイスを登録できます。 IMEI 番号の付いたデバイスも識別し、会社所有のタグを付け、COD シナリオを実行できます。

[企業所有のデバイスの登録](../deploy-use/enroll-company-owned-devices.md)

### <a name="dem"></a>DEM
デバイス登録マネージャーは、複数の会社所有デバイスの登録と管理に使用される特別なユーザー アカウントです。 マネージャーは会社ポータルをインストールし、さまざまユーザーなしデバイスを登録できます。 [DEM の詳細はこちらをご覧ください](../deploy-use/enroll-devices-with-device-enrollment-manager.md)。 ([テーブルに戻る](#overview-of-device-enrollment-methods))

### <a name="dep"></a>DEP
Apple デバイス登録プログラム (DEP) 管理では、ポリシーを作成したら、DEP で購入し、管理する iOS デバイスに “無線で” 展開できます。 ユーザーがデバイスを初めてオンにし、iOS セットアップ アシスタントを実行すると、デバイスが登録されます。 この方法では **iOS 監視**モードがサポートされていますが、このモードでは次の操作が可能です。
  - ロック登録
  - 条件付きアクセス
  - 脱獄検出
  - モバイル アプリケーション管理

[DEP の詳細はこちらをご覧ください](../deploy-use/ios-device-enrollment-program-for-hybrid.md)。 ([テーブルに戻る](#overview-of-device-enrollment-methods))

### <a name="usb-sa"></a>USB-SA
USB 接続、セットアップ アシスタント登録。 管理者はポリシーを作成し、それを Apple Configurator にエクスポートします。 ポリシーにより USB 接続の会社所有デバイスが準備されます。 管理者は、手動で各デバイスを登録する必要があります。 ユーザーはデバイスを受け取り、セットアップ アシスタントを実行し、デバイスを登録します。 この方法では **iOS 監視**モードがサポートされていますが、このモードでは次の操作が可能です。
  - 条件付きアクセス
  - 脱獄検出
  - モバイル アプリケーション管理

詳細は、「[Setup Assistant enrollment with Apple Configurator](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)」 (Apple Configurator によるセットアップ アシスタント登録) にあります。 ([テーブルに戻る](#overview-of-device-enrollment-methods))

## <a name="mobile-device-management-with-exchange-activesync-and-configuration-manager"></a>Exchange ActiveSync と Configuration Manager を使用したモバイル デバイス管理
登録されていないが、Exchange ActiveSync (EAS) に接続するモバイル デバイスは EAS MDM ポリシーを利用することで Intune で管理できます。 Intune は Exchange Connector を利用し、オンプレミスまたはクラウド ホストの EAS と通信します。

[Exchange ActiveSync および Intune を使用したモバイル デバイス管理](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)

---
title: "ハイブリッド MDM のセットアップ | Microsoft Docs"
description: "Configuration Manager と Intune を使用してハイブリッド デバイス登録をセットアップします。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: "34"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: c494fcc38955571c06507278a1ae88e5777b5708
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="setup-hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune を使用してハイブリッド モバイル デバイス管理 (MDM) をセットアップする

*適用対象: System Center Configuration Manager (Current Branch)*


Configuration Manager で iOS デバイス、Windows デバイス、および Android デバイスを管理するには、まず Intune に登録する必要があります。 Intune を使用して Configuration Manager へのハイブリッド デバイス登録をセットアップするには、以下の手順を実行します。 以下の手順を完了すると、ユーザーが "Bring Your Own Device" (BYOD) 登録を利用できるようになります。 この手順は、[BYOD デバイスの登録](enroll-hybrid-ios-mac.md)および[会社所有のデバイスの登録](enroll-company-owned-devices.md)のための前提条件でもあります。

 |手順|説明|  
 |-----------|-------------|  
 |**手順 1:** [MDM コレクションを作成する](create-mdm-collection.md)|デバイスの登録を許可するユーザーを使用して Configuration Manager ユーザー コレクションを作成します|  
 |**手順 2:** [ドメイン名の要件](confirm-dns.md)|組織のドメイン ネーム サービス (DNS) と Active Directory ユーザー管理が MDM の要件を満たしていることを確認します|
 |**手順 3:** [Intune サブスクリプションを構成する](configure-intune-subscription.md)|Intune サービスを使用すると、インターネット上でデバイスを管理できます。|  
 |**手順 4:** [使用条件を追加する](terms-and-conditions.md)| 使用条件を作成します。ユーザーは、ポータル サイト アプリを使用する前にこの使用条件に同意する必要があります。|
 |**手順 5:** [サービス接続ポイントを作成する](create-service-connection-point.md)|サービス接続ポイントは、設定とソフトウェアの展開情報を Configuration Manager に送信し、モバイル デバイスからステータス メッセージとインベントリ メッセージを取得します。 |  
 |**手順 6:** [プラットフォームの登録を有効にする](enable-platform-enrollment.md)|iOS デバイスと Windows デバイスの MDM 登録には、サービスとデバイス間の通信のために追加の手順が必要です。 Android の場合、追加の構成は必要ありません。|  
 |**手順 7:** [追加の管理をセットアップする](set-up-additional-management.md)|(省略可能) 登録デバイスの構成アイテムと条件付きアクセスを設定します|
 |**手順 8:** [MDM の構成を確認する](verify-mdm-configuration.md)|ログ ファイルを見て、サービス接続ポイントが正常に作成されたことと、ユーザー アカウントが同期していることを確認します。|

Configuration Manager を使用せずに Intune を使用する場合
> [!div class="button"]
[Intune ドキュメントを見る >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)


## <a name="enroll-devices"></a>デバイスの登録
ハイブリッドのセットアップが完了したら、いくつかの方法でデバイスを Configuration Manager に登録できます。
- **会社所有 (COD) のデバイス:** [会社所有のデバイスを登録します](enroll-company-owned-devices.md)。会社所有のデバイスの登録方法に関するガイダンスはプラットフォームごとに異なります。
- **ユーザー所有 (BYOD) のデバイス:** [ユーザー所有 (BYOD) のデバイスを登録します](enroll-hybrid-ios-mac.md)。ユーザー所有のデバイスを登録する方法について説明します。

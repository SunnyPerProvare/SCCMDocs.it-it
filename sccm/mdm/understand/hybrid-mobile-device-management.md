---
title: "ハイブリッド モバイル デバイス管理 (MDM) - Configuration Manager および Microsoft Intune | Microsoft Docs"
description: "System Center Configuration Manager と Microsoft Intune を使用するハイブリッド モバイル デバイス管理 (MDM) について説明します。"
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
ms.openlocfilehash: e54478a03807c939ffa64ff39a21ef6f9ea4ae2d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune を使用するハイブリッド モバイル デバイス管理 (MDM)

*適用対象: System Center Configuration Manager (Current Branch)*


Configuration Manager と Microsoft Intune を使用して iOS、Windows、Android デバイスを管理できます。 すべての管理タスクは Configuration Manager コンソールから処理されます。このコンソールでは、インターネット経由で Microsoft Intune のオンライン サービスとシームレスに統合された残りの管理タスクを実行します。  Configuration Manager を利用し、ユーザーが自分のデバイスで安全かつ管理された方法で会社のリソースにアクセスできるように設定できます。 つまり、会社のデータを守ると共に、ユーザー個人のデバイスや会社支給のデバイスから会社のデータにアクセスできるようにします。 デバイスの管理機能:

-   デバイスの削除とワイプ
-   パスワード、セキュリティ、ローミング、暗号化、ワイヤレス通信などのコンプライアンス設定の構成
-   デバイスへの基幹業務 (LOB) アプリの展開
-   Windows ストア、Windows Phone ストア、App Store、または Google Play に接続するデバイスへのアプリの展開
-   ハードウェア インベントリの収集
-   組み込みレポートを使用したソフトウェア インベントリの収集

ハイブリッド MDM で使用できる新機能については、「[What's new in hybrid mobile device management](../understand/whats-new-in-hybrid-mobile-device-management.md)」 (ハイブリッド モバイル デバイス管理の新機能) を参照してください。

このドキュメントでは、Configuration Manager を使ってコンピューターを管理しており、モバイル デバイスも管理するために Intune を使って Configuration Manager コンソールを拡張する場合を考えます。 Intune とハイブリッド モバイル デバイス管理の違いを理解するには、「[Microsoft Intune スタンドアロンか System Center Configuration Manager を使用するハイブリッド モバイル デバイス管理を選択する](choose-between-standalone-intune-and-hybrid-mobile-device-management.md)」を参照してください。

Configuration Manager を Intune を利用して拡張すると、会社所有のデバイスを登録して管理したり、ユーザーに個人デバイスの登録許可を与えたりできます。 Intune を使用する会社所有のデバイスを、Configuration Manager を使用して管理することもできます。

## <a name="hybrid-mdm-enrollment"></a>ハイブリッド MDM の登録
デバイスをハイブリッド管理するには、サービスに登録する必要があります。 デバイスの登録方法は、デバイスの種類、所有権、必要な管理のレベルによって異なります。
- "Bring your own device" (BYOD) 登録の場合、ユーザーは個人のスマートフォン、タブレット、PC を登録できます。
- 企業所有デバイス (COD) 登録の場合、リモート ワイプ、共有デバイス、デバイスのユーザー アフィニティなどの管理シナリオを有効にできます。
- オンプレミスの、あるいはクラウドでホストされている [Exchange ActiveSync](../plan-design/device-enrollment-methods.md#mobile-device-management-with-exchange-activesync-and-configuration-manager) を使用する場合、登録なしの簡単な Intune 管理を有効にできます。 Windows PC は [Intune クライアント ソフトウェア](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune)でも管理できます。

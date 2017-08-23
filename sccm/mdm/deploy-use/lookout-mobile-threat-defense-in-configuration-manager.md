---
title: "リスクに基づいたアクセスの制限 | Microsoft Docs"
description: "デバイス、ネットワーク、アプリケーションのリスクに基づいてアクセスを制限します。"
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 21841d97387f07f53993d957641f9ad892d723c2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>デバイス、ネットワーク、アプリケーションのリスクに基づき、会社のリソースへのアクセスを管理する

*適用対象: System Center Configuration Manager (Current Branch)*

Lookout が実施するリスク評価に基づき、モバイル デバイスから企業のリソースへのアクセスを制御できます。Lookout はデバイスを脅威から守るためのソリューションであり、Microsoft Intune と統合されています。 リスクは、Lookout サービスがデバイスから集めた、オペレーティング システム (OS) の脆弱性、インストールされた悪意のあるアプリ、悪意のあるネットワーク プロファイルに関する製品利用統計情報に基づきます。 

System Center Configuration Manager (SCCM) コンプライアンス ポリシー経由で有効になる、Lookout のリスク評価レポートに基づき、条件付きアクセス ポリシーを構成したり、検出された脅威に起因して非準拠として判断されたデバイスをブロックしたりできます。

[ハイブリッド MDM 展開 (SCCM と Intune)](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) では、Lookout のようなデバイスを脅威から守るためのソリューションが提供するリスク評価に基づき、会社のリソースやデータへのアクセスを制御できます。

## <a name="how-do-the-hybrid-mdm-deployment-and-lookout-device-threat-protection-help-protect-company-resources"></a>ハイブリッド MDM 展開と Lookout デバイス脅威防御で会社のリソースを守るしくみとはどのようなものですか。
モバイル デバイスで実行される Lookout のモバイル アプリ (Lookout for work) は、ファイル システム、ネットワーク スタック、デバイス、アプリケーションの製品利用統計情報を記録し (利用できる場合)、Lookout デバイス脅威防御クラウド サービスに送信し、モバイルの脅威に関するデバイスのリスクを計算し、集計します。 Lookout コンソールで、脅威のリスク レベルの分類を要件に合わせて変更することもできます。  

SCCM のコンプライアンス ポリシーには、Lookout デバイス脅威リスク評価に基づく、Lookout モバイル脅威防御のための新しいルールが追加されました。 このルールを有効にすると、デバイスのコンプライアンスが評価されます。

デバイスがコンプライアンス ポリシーに準拠していないと判断されると、Exchange Online や SharePoint Online など、リソースへのアクセスを条件付きアクセス ポリシーでブロックできます。 アクセスがブロックされると、問題を解決し、会社のリソースに再度アクセスするためのチュートリアルがエンドユーザーに与えられます。 このチュートリアルは、Lookout for work アプリ経由で起動します。

## <a name="supported-platforms"></a>サポートされているプラットフォーム:
* **Android 4.1 以降**、Microsoft Intune に登録済み。
* **iOS 8 以降**、Microsoft Intune に登録済み。
Lookout でサポートされているプラットフォームと言語の詳細については、この[記事](https://personal.support.lookout.com/hc/en-us/articles/114094140253)をご覧ください。

## <a name="prerequisites"></a>必要条件:
* [ハイブリッド MDM 展開](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management)
* Microsoft Intune のサブスクリプションと Azure Active Directory。
* Lookout Mobile EndPoint Security のエンタープライズ サブスクリプション。  詳細については、「[Lookout Mobile Endpoint Security」](https://www.lookout.com/products/mobile-endpoint-security)を参照してください。

## <a name="example-scenarios"></a>シナリオ例
一般的なシナリオを次に示します。
### <a name="control-access-based-on-threat-from-malicious-apps"></a>悪意のあるアプリからの脅威に基づくアクセス制御:
マルウェアなど、悪意のあるアプリがデバイスで検出されると、そのデバイスで次の動作が禁止されます。
* 脅威を解決する前に企業の電子メールに接続すること。
* OneDrive for Work アプリを利用して企業のファイルを同期すること。
* ビジネス クリティカルなアプリケーションにアクセスすること。

**悪意のあるアプリが検出されると、アクセスが禁止される:**

![悪意のあるアプリに起因し、デバイスが非準拠として見なされたときにアクセスを禁止する条件付きアクセス ポリシーの図](media/config-mgr-maliciousapps_blocked.png)

**脅威が取り除かれると、デバイスのブロックが解除され、会社のリソースにアクセスできる:**

![修復後、デバイスが準拠として見なされたときにアクセスを与える条件付きアクセス ポリシーの図](media/config-mgr-maliciousapps-unblocked.png)
### <a name="control-access-based-on-threat-to-network"></a>ネットワークの脅威に基づくアクセス制御:
Man-in-the-middle 攻撃のようなネットワークの脅威を検出し、デバイス リスクに基づき、WiFi ネットワークへのアクセスを制限します。

**WiFi 経由のネットワーク アクセスを禁止する:**

![ネットワークの脅威に基づいて WiFi アクセスを禁止する条件付きアクセスの図](media/config-mgr-network-wifi-blocked.png)

**修復後、アクセスが与えられる:**

![脅威が取り除かれたときにアクセスを許可する条件付きアクセスの図](media/config-mgr-network-wifi-unblocked.png)
### <a name="control-access-to-sharepoint-online-based-on-threat-to-network"></a>ネットワークの脅威に基づき、SharePoint Online へのアクセスを制御する:

Man-in-the-middle 攻撃のようなネットワークの脅威を検出し、デバイス リスクに基づき、企業ファイルの同期を制限します。

**デバイスで検出されたネットワークの脅威に基づき、SharePoint Online へのアクセスを禁止する:**

![脅威の検出に基づいて SharePoint Online へのデバイス アクセスを禁止する条件付きアクセスの図](media/config-mgr-network-spo-blocked.png)


**修復後、アクセスが与えられる:**

![ネットワークの脅威が取り除かれたときにアクセスを許可する条件付きアクセスの図](media/config-mgr-network-spo-unblocked.png)

## <a name="next-steps"></a>次のステップ
このソリューションを実装するために必須となる主な手順:
1.  [Lookout モバイル脅威防御のサブスクリプションを設定する](set-up-your-subscription-with-lookout.md)
2.  [Intune で Lookout MTP の接続を有効にする](enable-lookout-connection-in-intune.md)
3.  [Lookout for work アプリケーションを構成し、展開する](configure-and-deploy-lookout-for-work-apps.md)
4.  [コンプライアンス ポリシーを構成する](enable-device-threat-protection-rule-compliance-policy.md)
5.  [Troubleshoot Lookout integration](troubleshoot-lookout-integration.md) (Lookout 統合のトラブルシューティング)

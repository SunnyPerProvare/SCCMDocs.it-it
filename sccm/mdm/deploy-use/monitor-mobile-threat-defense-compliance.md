---
title: "Mobile Threat Defense コンプライアンスの監視| System Center Configuration Manager"
description: "Configuration Manager マネージャー コンソールからの Mobile Threat Defense パートナー コンプライアンス ステータスの監視"
ms.custom: na
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 408190da-bea6-4122-9dd6-f90155040e88
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 8edf83a0f761dfc16274ce49c3aa2b878c7fe6cd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-mobile-threat-defense-compliance"></a>**Mobile Threat Defense コンプライアンスの監視**

*適用対象: System Center Configuration Manager (Current Branch)*

## <a name="to-monitor-the-overall-compliance-status"></a>全体的なコンプライアンス ステータスを監視するには

Mobile Threat Defense のステータスを監視するには、次のようにします。

1.  Configuration Manager コンソールで、**[監視]** ワークスペースをクリックします。

2.  **[監視]** ワークスペースで、**[セキュリティ]** ノードをクリックします。

ビジュアル グラフ形式で表示されるコンプライアンス ステータスの概要を、さまざまなレベルで確認することができます。 グラフの個々のセクションをクリックして、次のような詳細情報を表示することができます。 

- プラットフォームごとの、非準拠として報告されたデバイスの数
- デバイスのコンプライアンス ステータスに関連するエラー

![](http://i.imgur.com/bmPsiWk.png)

## <a name="to-monitor-the-individual-compliance-status"></a>個々のコンプライアンス ステータスを監視するには

次のようにして、個々のデバイス ステータスを確認することもできます。

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** ワークスペースをクリックします。

2.  **[デバイス]** をクリックします。

> [!TIP] 
> **[Device threat compliance]** (デバイス脅威コンプライアンス) 列と **[デバイス脅威レベル]** 列を追加して、状態を確認できます。 既定では、これらの列は表示されません。

## <a name="device-threat-protection-tab"></a>[デバイス脅威保護] タブ

さらに、**[デバイス]** 画面で、特定のデバイスを選択し、**[デバイス脅威保護]** タブをクリックして、デバイス コンプライアンス ステータスの詳細を表示することができます。 以下の列の説明と予期される値は、デバイスのコンプライアンス ステータスを分析するのに役立ちます。

> [!IMPORTANT] 
> 選択したデバイスがモバイル デバイスである場合は、[デバイスの脅威保護] タブのみが表示されます。

|列名|既定で表示|説明| 
|-|-|-|
|**説明**| ○ | Mobile Threat Defense パートナーによって提供される脅威に関する詳細。 |
|**最終更新時刻**| ○ | Mobile Threat Defense パートナーが Intune に脅威に関する更新済みの詳細情報を最後に送信した時刻。 |
|**脅威の重要度**| ○ | 脅威の重要度は、Mobile Threat Defense パートナー コンソールでの管理者の構成に基づく個々の脅威の定義です。 3 つの値 (**低**、**中**、**高**) のいずれかになります。 |
|**脅威の状態**| ○ | デバイスの脅威の現在の状態。 使用可能な値は、**Active** (アクティブ)、**Resolved** (解決済み)、**Ignored** (無視) です。無視の場合、ユーザーはデバイスの脅威を無視したが、脅威はまだ存在していることを意味します。 |
|**脅威の種類**| ○ | Mobile Threat Defense パートナーの脅威の種類。 使用可能な値: **App** (アプリ)、**File** (ファイル)、**OS** |
|**AAD アカウント ID**| × | Azure Active Directory の一意の識別子です。 |
|**分類**| ○ | Mobile Threat Defense パートナーにより提供される脅威の分類。 使用可能な値: **Root Enabler, Riskware, Adware, Chargeware, DataLeak, Trojan, Worm, Virus, Exploit, Backdoor, Bot, AppDropper, ClickFraud, Spam, Spyware, SurveillanceWare, Vulnerability, Unknown, Root Jailbrake, Connectivity, TollFraud, SideloadedApp (ルート イネーブラー、リスクウェア、アドウェア、チャージウェア、データのリーク、トロイの木馬、ワーム、ウイルス、エクスプロイト、バックドア、ボット、アプリ ドロッパー、クリック詐欺、スパム、スパイウェア、監視ウェア、脆弱性、不明、root 化/脱獄、接続、料金詐欺、サイドロードされたアプリ)** |
|**デバイス ID**| × | 脅威にさらされている社内参加済みデバイスに関する情報を示す Azure Active Directory のオブジェクト ID。 |
|**脅威 ID**| × | Mobile Threat Defense パートナーで生成される脅威の一意の識別子。 脅威 ID は解決方法を追跡するために使用されます。 |
|**脅威 URL**| × | 脅威 URL がある場合は、特定の脅威の Mobile Threat Defense パートナーの管理コンソール ビューに戻るリンクが示されます。 |

> [!TIP] 
> **既定で表示**されない列を有効にして、デバイスの Mobile Threat Defense コンプライアンス ステータスの詳細を確認できるようにしてください。

---
title: "System Center Configuration Manager を使用した MDM コレクションの作成 | Microsoft Docs"
description: "System Center Configuration Manager を使用して MDM コレクションを作成します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d1b4337f-85e8-45e6-8bbe-9f18b49041c7
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: fabbcfd2d5656d4fa8cb87feffe87e17998df145
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="create-an-mdm-collection-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune を使用した MDM コレクションの作成

*適用対象: System Center Configuration Manager (Current Branch)*

デバイスを管理対象に登録できるユーザーを指定するには、Configuration Manager ユーザー コレクションが必要です。 Intune のライセンスはユーザーごとに割り当てられるため、使用できるのはユーザー コレクション (デバイス コレクションではなく) のみです。

> [!NOTE]
> Intune にデバイスを登録する場合、Office 365 ポータルまたは Azure Active Directory ポータルでユーザーにライセンスを割り当てる必要はありません。 Intune サブスクリプションに関連付けられたコレクションにユーザーを含める ([後の手順](configure-intune-subscription.md)を参照) だけで済みます。

テスト目的で**ダイレクト規則**をセットアップし、デバイスを登録できる特定のユーザーを追加することができます。 Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[ユーザー コレクション]** を選択し、**[ホーム]** タブ > **[作成]** グループをクリックし、**[ユーザー コレクションの作成]** をクリックします。 配布を広範にするには、**クエリ規則**を使用してユーザーを定義するようにします。 コレクションの詳細については、「[System Center Configuration Manager でコレクションを作成する方法](https://technet.microsoft.com/library/mt629371.aspx)」を参照してください。

![MDM のユーザー コレクションを作成する](../media/mdm-create-user-collection.png)

> [!div class="button"]
[次のステップ >](confirm-dns.md)

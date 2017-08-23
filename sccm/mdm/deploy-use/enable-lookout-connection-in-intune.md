---
title: "Intune で Lookout MTP を有効にする | Microsoft Docs"
description: "Intune 管理コンソールで、Lookout Mobile Threat Protection を有効にします。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7e4ada34-63bf-4b9f-8246-31816aa44196
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: f9ddbcc981fa1274a41ae16a6a939c0cdf739c3e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="enable-lookout-mtp-connection-in-the-intune-admin-console"></a>Intune 管理コンソールで、Lookout MTP 接続を有効にする

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックでは、Intune で Lookout MTP 接続を有効にする方法を説明します。 この手順を実行する前に、Lookout コンソールで Intune コネクタを構成しておきます。  まだ構成していない場合は、「[Set up your subscription with Lookout mobile threat protection](set-up-your-subscription-with-lookout.md)」(Lookout Mobile Threat Protection 用にサブスクリプションを設定する) で説明されている手順を実行します。

Intune で Lookout MTP 接続を有効にするには、[Microsoft Intune 管理者コンソール](https://manage.microsoft.com)の「**管理**」ページで、**[Third Party Service Integration]** (サード パーティ サービスの統合) を選択します。 **[Lookout の状態]** を選択し、**[MTP との同期]** をトグル ボタンを使用して有効にします。

![有効になったトグル ボタンが強調表示された、Lookout の同期ページのスクリーン ショット](media/lookout-intune-synchronization.png)

これで、Intune 管理者コンソールでの Lookout と Intune の統合の設定は完了です。  このソリューションを実装するための次の手順には、[Lookout for Work アプリ](configure-and-deploy-lookout-for-work-apps.md)の展開や、[コンプライアンス](enable-device-threat-protection-rule-compliance-policy.md) ポリシーの設定などが含まれます。

>[!IMPORTANT]
> コンプライアンス ポリシー ルールを作成し、条件付きアクセスを構成するには、事前に Lookout for Work アプリを構成する**必要があります**。 これにより、エンド ユーザーがアプリをインストールして、電子メールやその他の会社のリソースにアクセスする場合に使用できるようになります。

## <a name="next-steps"></a>次のステップ
[Lookout for Work アプリを構成する](configure-and-deploy-lookout-for-work-apps.md)

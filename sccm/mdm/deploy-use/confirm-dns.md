---
title: "System Center Configuration Manager を使用したドメイン名の要件の確認 | Microsoft Docs"
description: "System Center Configuration Manager を使用してドメイン名の要件を確認します。"
ms.custom: na
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 522c2e82-20eb-4f38-859b-d55640b24e32
caps.latest.revision: "18"
caps.handback.revision: "0"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 35b24294073956a6bdb14cae07705f56d31e00a9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="confirm-domain-name-requirements-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune を使用したドメイン名の要件の確認

*適用対象: System Center Configuration Manager (Current Branch)*

必要に応じて、Configuration Manager 外部の依存関係を満たすため、次の手順を実行します。

1. デバイスを登録するには、各ユーザーに Intune ライセンスが割り当てられている必要があります。 Intune ライセンスをユーザーに割り当てるには、パブリックに解決できるユーザー プリンシパル名 (UPN) (たとえば、johndoe@contoso.com) または Azure Active Directory で構成された代替ログイン ID を各ユーザーが持っている必要があります。 代替ログイン ID を構成すると、たとえば UPN が NetBIOS 形式 (CONTOSO\johndoe など) の場合でも、ユーザーが電子メール アドレスでサインインできるようになります。

  - 会社がパブリックに解決できる UPN (つまり johndoe@contoso.com) を使用している場合、それ以上の構成は必要ありません。
  - 会社が解決できない UPN (つまり CONTOSO\johndoe) を使用している場合、[Azure Active Directory で代替 ID を構成する](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#pages-under-the-section-sync)必要があります。

2.  Active Directory Federation Services (AD FS) を展開および構成する (オプション)

     シングル サインオンをセットアップすると、ユーザーは会社の資格情報を使用してサインインし、Intune のサービスにアクセスできます。

     詳細については、以下のトピックを参照してください。
    -   [シングル サインオンを準備する](http://go.microsoft.com/fwlink/?LinkID=271124)
    -   [チェックリスト: AD FS 2.0 を使用してシングル サインオンを実装および管理する](http://go.microsoft.com/fwlink/?LinkID=271125)

3.  ディレクトリ同期の展開と構成

     ディレクトリ同期を使用すると、同期したユーザー アカウントで Intune を設定できます。 同期したユーザー アカウントとセキュリティ グループは、Intune に追加されます。 Configuration Manager MDM と Microsoft Intune をセットアップするときに、デバイスを登録できない一般的な原因は、ディレクトリ同期が有効になっていないことです。

     詳しくは、Active Directory ドキュメント ライブラリの「 [ディレクトリ統合](http://go.microsoft.com/fwlink/?LinkID=271120) 」をご覧ください。

4.  省略可能で推奨されない手順: Active Directory フェデレーション サービスを使用していない場合は、ユーザーの Microsoft Online パスワードをリセットします。

     AD FS を使用していない場合、各ユーザーの Microsoft Online パスワードを設定する必要があります。

> [!div class="button"]
[< 前のステップ](create-mdm-collection.md)  [次のステップ >](configure-intune-subscription.md)

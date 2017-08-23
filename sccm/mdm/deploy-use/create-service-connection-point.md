---
title: "System Center Configuration Manager を使用したサービス接続ポイントの作成 | Microsoft Docs"
description: "System Center Configuration Manager を使用してサービス接続ポイントを作成します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 617abb22-d22f-41fb-a76b-1c4259e419d2
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 9a21d02cb2a50162e5de50481f0f27f2dd7a616c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="create-a-service-connection-point-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune を使用したサービス接続ポイントの作成

*適用対象: System Center Configuration Manager (Current Branch)*

サブスクリプションを作成したら、サービス接続ポイントのサイト システムの役割をインストールして、Intune サービスに接続できるようにします。 このサイト システムの役割は、設定とアプリケーションを Intune サービスにプッシュします。

 サービス接続ポイントは、設定とソフトウェアの展開情報を Configuration Manager に送信し、モバイル デバイスからステータス メッセージとインベントリ メッセージを取得します。 Configuration Manager サービスは、モバイル デバイスと通信し、設定を保存するゲートウェイとして機能します。

> [!NOTE]
>  サービス接続ポイントのサイト システムの役割は、中央管理サイトかスタンドアロン プライマリ サイトだけにインストールできます。 サービス接続ポイントにはインターネット アクセスが必要です。


## <a name="configure-the-service-connection-point-role"></a>サービス接続ポイントの役割を構成する

1.  Configuration Manager コンソールで、[ **管理**] をクリックします。

2.  **[管理]** ワークスペースで **[サイト]** を展開して、**[サーバーとサイト システムの役割]** をクリックします。

3.  対応する手順を使用して、 **サービス接続ポイント** の役割を新規または既存のサイト システム サーバーに追加します。

    -   新しいサイト システム サーバー: **[ホーム]** タブの **[作成]** グループにある **[サイト システム サーバーの作成]** をクリックして、サイト システム サーバーの作成ウィザードを開始します。

    -   既存のサイト システム サーバー: サービス接続ポイントの役割をインストールするサーバーをクリックします。 [ホーム **** ] タブの [サーバー **** ] グループにある [サイト システムの役割の追加 **** ] をクリックして、サイト システムの役割の追加ウィザードを開始します。

4.  **[システムの役割の選択]** ページで、 **[サービス接続ポイント]**を選んで、 **[次へ]**をクリックします。
![サービス接続ポイントを作成する](../media/mdm-service-connection-point.png)

* ウィザードを完了します。

## <a name="how-does-the-service-connection-point-authenticate-with-the-microsoft-intune-service"></a>サービス接続ポイントが Microsoft Intune サービスで認証を行う方法
 サービス接続ポイントは、インターネット経由でモバイル デバイスを管理するクラウド ベースの Intune サービスへの接続を確立することによって、Configuration Manager を拡張します。 サービス接続ポイントは、次のように Intune サービスで認証を行います。

1.  Configuration Manager コンソールで Intune サブスクリプションを作成する場合、Configuration Manager 管理者は、Azure Active Directory に接続して認証されます。Azure Active Directory は、各 ADFS サーバーにリダイレクトして、ユーザーに対してユーザー名とパスワードの入力を求めるダイアログを表示します。 次に、Intune はテナントに証明書を発行します。

2.  手順 1 の証明書は、サービス接続ポイントのサイトの役割にインストールされ、Microsoft Intune サービスとのそれ以降のすべての通信を認証および承認するために使用されます。

> [!div class="button"]
[< 前のステップ](terms-and-conditions.md)  [次のステップ >](enable-platform-enrollment.md)

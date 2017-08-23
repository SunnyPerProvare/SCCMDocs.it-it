---
title: "Lookout 統合のトラブルシューティング | System Center Configuration Manager"
description: "このトピックでは、Lookout 統合でよく発生する問題のトラブルシューティングについて説明します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e36b98c7-d0f4-4dd6-bac3-6a6c4b4bf841
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 4fd2d3b8aae6a2f42e7c6a87723d16368be30984
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="troubleshoot-lookout-integration-with-intune"></a>Intune による Lookout 統合のトラブルシューティング

*適用対象: System Center Configuration Manager (Current Branch)*

## <a name="troubleshoot-login-errors"></a>ログイン エラーのトラブルシューティング
### <a name="403-errors"></a>403 エラー
[Lookout MTP コンソール](https://aad.lookout.com)へのログイン時に**サービスにアクセスする権限がありません**という 403 エラーが発生する場合があります。このエラーは、Lookout MTP にアクセスするように構成されている Azure Active Directory (Azure AD) グループのメンバーではないユーザー名を指定した場合に発生することがあります。

Lookout MTP は、構成済みの Azure AD グループのユーザーのみがアクセスできるように構成されています。 Lookout MTP へのアクセス権が構成されているグループがわからない場合は、Lookout サポートに連絡してください。

Lookout サポートには次の方法で連絡することができます。

* 電子メール: enterprisesupport@lookout.com
* [MTP コンソール](http://aad.lookout.com)にログインし、**[サポート]** モジュールに移動します。
* https://enterprise.support.lookout.com/hc/en-us/requests に移動して、サポートを要求します。

### <a name="unable-to-sign-in"></a>サインインできない
Azure AD グローバル管理者ユーザーが初期の Lookout セットアップを受け入れていない場合、次のエラーが表示される可能性があります。

![サインイン エラーを示す Lookout ログイン画面のスクリーン ショット](media/lookout-consent-not-accepted-error.png)

この問題を解決するには、グローバル管理者ユーザーが https://aad.lookout.com/les?action=consent にログインし、セットアップを開始するためのプロンプトを受け入れる必要があります。 詳細については、[Lookout MTP でのサブスクリプションのセットアップ](set-up-your-subscription-with-lookout.md)に関するトピックを参照してください。

## <a name="troubleshoot-device-status-issues"></a>デバイスの状態に関する問題のトラブルシューティング

### <a name="device-not-showing-up-in-the-lookout-mtp-console-device-list"></a>Lookout MTP コンソールのデバイス リストにデバイスが表示されない

これは、次のシナリオのいずれかで発生する可能性があります。
* このデバイスを所有するユーザーが、**Lookout MTP コンソール**で指定されている**登録グループ**に属していない場合。  **[システム]** モジュールから、**[Intune コネクタ]** タブに移動し、**[登録管理]** 設定を確認します。  1 つ以上の Azure AD グループが登録用に構成されている必要があります。  表示されないデバイスを所有するユーザーが、指定されている Azure AD グループのいずれかのメンバーであることを確認します。  新しいユーザーが登録グループに追加されてから、Lookout MTP コンソールの **[デバイス]** モジュールにデバイスが表示されるようになるまで、最大で構成されているポーリング間隔 (既定値は 5 分) かかります。

* Lookout MTP でデバイスがサポートされていない場合。  サポートされていないデバイスは、Lookout MTP コンソールのコネクタ設定の **[管理対象デバイス]** セクションに表示されます。

### <a name="device-continues-to-be-reported-as-pending"></a>デバイスは**保留中**と表示され続ける

デバイスが**保留中**と表示される場合、エンド ユーザーが Lookout for Work アプリを開いて、**[アクティブ化]** ボタンをタップしていないことを意味します。 Lookout for Work アプリでのデバイスのアクティブ化の詳細については、以下のトピックを参照してください。

[Android デバイスで Lookout for Work のインストールを求められる](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

### <a name="in-the-lookout-mtp-console-a-device-is-showing-as-active-but-does-not-have-a-device-id"></a>Lookout MTP コンソールで、デバイスはアクティブと表示されるが、デバイス ID がない
これは、このデバイスを所有するユーザーが、Lookout MTP コンソールで指定されている登録グループに含まれていないことを意味します。   デバイスを所有するユーザーが登録グループから削除されているか、ユーザーが属している登録グループが削除されている場合、デバイスがこのような状態になることがあります。

Lookout MTP コンソールの **[システム]** モジュールから **[Intune コネクタ]** タブに移動し、**[登録]** 設定を確認します。  1 つ以上の Azure AD グループが登録用に構成されている必要があります。  デバイスを所有するユーザーが指定された Azure AD グループのいずれかに属していることを確認します。

デバイスがこの状態である間は、Lookout は検出された脅威をユーザーに通知し続けますが、Intune には脅威情報は送信されません。

### <a name="device-shows-disconnected-state"></a>デバイスが切断状態を示す

切断とは、Lookout MTP が構成されている期間 (既定値は 30 日、最小は 7 日) 中にデバイスから応答を受信していないことを意味します。 これは、ポータル サイト アプリまたは Lookout for Work アプリがデバイスにインストールされていないか、アンインストールされていることを意味します。 アプリを再インストールすることでこの問題が解決されます。 ユーザーが Lookout for Work を開き、アプリをアクティブ化すると、デバイスは Lookout MTP および Intune と再同期します。

### <a name="forcing-a-resync-on-the-device"></a>デバイスの強制的な再同期
Lookout MTP コンソールの **[デバイス]** モジュールから、管理者はデバイスを選択して削除することができます。   次回、デバイスの所有者が Lookout for Work アプリを開き、**[アクティブ化]** をタップしたときに、デバイスは完全な再同期状態となります。

### <a name="the-owner-of-the-device-is-no-longer-using-this-device"></a>デバイスの所有者がこのデバイスを使用しなくなった
デバイスをワイプし、[このトピック](https://docs.microsoft.com/en-us/sccm/mdm/deploy-use/wipe-lock-reset-devices#full-wipe)の説明に従って新しいユーザーに登録を要求する必要があります。


Lookout MTP コンソールの **[デバイス]** モジュールに移動して、**[削除]** を選択することもできます。

新しいユーザーが Lookout MTP コンソールで指定されている登録グループのいずれかに属している限り、Azure AD がデバイスを新しいユーザーに関連付けるとデバイスは表示されます。

## <a name="compliance-remediation-workflows"></a>コンプライアンス修復のワークフロー
[Android デバイスで Lookout for Work のインストールを求められる]( http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

[Lookout for Work が Android デバイスで検出した脅威を解決する必要がある](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)

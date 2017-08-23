---
title: "iOS のアクティベーション ロックの管理 | Microsoft Docs"
description: "System Center Configuration Manager を使用して iOS のアクティベーション ロックを管理します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2745bac-e1b4-4dac-8ac7-32f1c820bc9c
caps.latest.revision: "9"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 88bef04a52f716ae13afc21c25d33dea06a3fc9c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="manage-ios-activation-lock-with-system-center-configuration-manager"></a>System Center Configuration Manager を使用した iOS のアクティベーション ロックの管理

*適用対象: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager は、iOS 7.1 以降向けの「iPhone を探す」アプリの機能である、iOS のアクティベーション ロックを管理するために役立ちます。 アクティベーション ロックを有効にすると、ユーザーの Apple ID とパスワードを入力しない限り、以下の操作を実行できなくなります。

- iPhone を探すアプリをオフにする
- デバイスを消去する
- ディスクを再アクティブ化する

**監視対象外** のデバイスでは、iPhone を探すアプリを使用すると、アクティベーション ロックが自動的に有効になります。

**管理対象** のデバイスでは、Configuration Manager のコンプライアンス設定を使用して、アクティベーション ロックをアクティブにする必要があります。

> [!TIP]
> iOS デバイスの監視モードでは、Apple Configurator ツールを使用して、デバイスをロックダウンし、特定のビジネス目的に必要な機能のみに制限することができます。 監視モードは、通常、企業所有のデバイス専用の機能です。

アクティベーション ロックにより、iOS デバイスをセキュリティで保護でき、紛失や盗難にあった場合に戻ってくる可能性が高まりますが、この機能は IT 管理者にさまざまな課題をもたらすことがあります。 たとえば、

- あるユーザーがデバイスでアクティブ化ロックを設定します。 その後、そのユーザーが退職し、デバイスを返却します。 ユーザーの Apple ID とパスワードがわからなければ、デバイスをワイプしても、再アクティベートすることはできません。
- アクティベーション ロックが有効になっているすべてのデバイスのレポートが必要です。
- 組織でデバイスを更新する場合に、一部のデバイスを別の部門に再割り当てする必要があります。 その際に再割り当てできるのは、アクティベーション ロックが有効になっていないデバイスに限られます。


こうした問題を解決するために、Apple は iOS 7.1 でアクティブ化ロックのバイパスを導入しました。 この機能により、ユーザーの Apple ID とパスワードがなくても、監視対象のデバイスのアクティブ化ロックを解除することができます。 監視対象のデバイスでは、デバイス固有のアクティブ化ロックのバイパス コードを生成できます。このコードは、Apple のアクティブ化サーバーに格納されます。

アクティベーション ロックについては、 [こちら](https://support.apple.com/HT201365)を参照してください。

## <a name="how-configuration-manager-helps-you-manage-activation-lock"></a>Configuration Manager を使ってアクティベーション ロックを管理する方法

Configuration Manager を使ってアクティベーション ロックを管理するには、次の 2 つの方法があります。

1. 監視対象のデバイスでアクティベーション ロックを有効にする。
2. 監視対象のデバイスでアクティベーション ロックをバイパスする。

> [!IMPORTANT]
> 監視対象外のデバイスでは、アクティベーション ロックをバイパスできません。

企業所有のデバイスでは、この機能には次のようなビジネス上のメリットがあります。



- ユーザーが iPhone を探すアプリのセキュリティ上のメリットを受けることができる。
- デバイスを再利用する必要がある場合に、デバイスをインベントリから削除することや、ロック解除できることを把握したうえで、ユーザーが業務を遂行できるようにすることができる。


## <a name="enable-activation-lock-on-supervised-devices"></a>監視対象のデバイスでアクティベーション ロックを有効にする

Configuration Manager のコンプライアンス設定を使用して、 **iOS および Mac OS X** タイプの構成項目を作成して展開し、監視対象のデバイスでアクティベーション ロックを有効にします。

1. トピック「[System Center Configuration Manager クライアントを使用せずに管理されている iOS デバイスと Mac OS X デバイスの構成項目を作成する方法](/sccm/compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)」の情報を使用して、**iOS および Mac OS X** タイプの構成項目を作成します。
2. 構成項目の作成ウィザードの「 **システム セキュリティ** 」ページで、 **[アクティブ化ロックを許可する (監視モードのみ)]** を **[許可]**に設定します。
3. [構成基準に構成項目を追加します](/sccm/compliance/deploy-use/create-configuration-baselines)。
4. アクティベーション ロックを有効にする iOS デバイスが属するコレクションに、[この構成基準を展開](/sccm/compliance/deploy-use/deploy-configuration-baselines)します。

> [!IMPORTANT]
> デバイスが実際に手元にある状態で、この手順を実行してください。 そうしない場合、アクティベーション ロックがバイパスされたときにデバイスを手元に持っている人が完全なアクセス権を持つことになり、「iPhone を探す」アプリをオフにしたり、デバイスを消去したり、再アクティブ化したりできてしまいます。

アクティベーション ロックのバイパスや、アクティベーション ロックのバイパス コードの取得は、監視対象デバイスでのみ行えます。監視対象外のデバイスでアクティベーション ロックをバイパスしようとしたり、バイパス コードを表示しようとしたりすると、エラーになります。



## <a name="view-the-activation-lock-bypass-code"></a>アクティベーション ロックのバイパス コードを表示する

1. Configuration Manager コンソールで、[ **資産とコンプライアンス**] をクリックします。
2. [ **資産とコンプライアンス** ] ワークスペースで [ **デバイス**] をクリックします。
3. アクティベーション ロックが有効になっている、監視モードの登録済みのデバイスを選びます。
4. **[ホーム]** タブの **[デバイス]** グループで、 **[リモート デバイスの操作]** > **[アクティブ化ロックのバイパス コードの表示]**をクリックします。
5. 選んだデバイスのバイパス コードが **[アクティベーション ロックのバイパス コード (Activation Lock Bypass Code)]** ダイアログ ボックスに表示されます。

## <a name="bypass-activation-lock"></a>アクティベーション ロックをバイパスする

1. Configuration Manager コンソールで、[ **資産とコンプライアンス**] をクリックします。
2. [ **資産とコンプライアンス** ] ワークスペースで [ **デバイス**] をクリックします。
3. アクティベーション ロックが有効になっている、監視モードの登録済みのデバイスを選びます。
3. **[ホーム]** タブの **[デバイス]** グループで、 **[リモート デバイスの操作]** > **[アクティブ化ロックのバイパス]**をクリックします。
5. 警告ダイアログ ボックスのメッセージを読み、続ける準備ができたら **[はい]** をクリックします。
6. 次の場所で、ロック解除要求の状態を確認できます。

    - デバイスのプロパティ ダイアログ ボックスで、デバイスの検出データを確認する。
    - **[デバイス]** ビューの **[アクティブ化ロック バイパスの状態]** 列 (既定でこの列は非表示) で確認する。
    - 詳細ウィンドウの **[概要]** タブにある **[リモート デバイスの操作に関する情報]** セクション (デバイスが選ばれている状態) で確認する。

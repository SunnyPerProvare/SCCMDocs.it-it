---
title: "Lookout でサブスクリプションを設定する | System Center Configuration Manager"
description: "このトピックでは、Lookout デバイス脅威保護を構成する方法の詳細を説明します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6087b279-ba05-4824-b5e3-3af14f3d3cfe
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: b777140c753e709f4048a30e63d8ae730d3e8723
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-your-subscription-for--lookout-device-threat-protection"></a>Lookout デバイス脅威保護のサブスクリプションを設定する

*適用対象: System Center Configuration Manager (Current Branch)*

Lookout デバイス脅威保護サービス用にサブスクリプションを準備するには、Lookout サポート (enterprisesupport@lookout.com) で Azure Active Directory (Azure AD) サブスクリプションに関する次の情報が必要です。 Lookout Mobility Endpoint Security テナントは、Lookout と Intune を統合するために Azure AD サブスクリプションに関連付けられます。 

* **Azure AD テナント ID**
* Lookout コンソールへの**フル** アクセス用の **Azure AD グループ オブジェクト ID**
* Lookout コンソールへの**制限付き**アクセス用の **Azure AD グループ オブジェクト ID** (省略可能)

> [!IMPORTANT]
> Azure AD テナントとまだ関連付けられていない既存の Lookout Mobile Endpoint Security テナントは、Azure AD および Intune との統合に使用できません。 新しい Lookout Mobile Endpoint Security テナントの作成については、Lookout のサポートに問い合わせてください。 新しいテナントを使って Azure AD ユーザーをオンボーディングします。

Lookout サポート チームに提供する必要がある情報を収集するには、次のセクションを使用します。  

## <a name="get-your-azure-ad-information"></a>Azure AD の情報を取得する
### <a name="azure-ad-tenant-id"></a>Azure AD テナント ID
[Azure AD 管理ポータル](https://manage.windowsazure.com)にサインインし、サブスクリプションを選択します。 

![テナントの名前を示す Azure AD のページのスクリーンショット](media/aad_tenant_name.png)サブスクリプションの名前を選択すると、結果の URL にはサブスクリプション ID が含まれます。  サブスクリプション ID の検索に問題がある場合は、[Microsoft サポート記事](https://support.office.com/en-us/article/Find-your-Office-365-tenant-ID-6891b561-a52d-4ade-9f39-b492285e2c9b?ui=en-US&rs=en-US&ad=US)でサブスクリプション ID の検索に関するヒントを参照してください。   
### <a name="azure-ad-group-id"></a>Azure AD グループ ID
Lookout コンソールは 2 つのレベルのアクセスをサポートします。  
* **フル アクセス:** Azure AD 管理者は、フル アクセス権を持つユーザーのグループを作成でき、必要に応じて制限付きアクセス権を持つユーザーのグループを作成できます。  これらのグループのユーザーだけが、**Lookout コンソール**にログインできます。
* **制限付きアクセス:** このグループのユーザーは、Lookout コンソールの構成と登録に関連する複数のモジュールにアクセスできず、Lookout コンソールの**セキュリティ ポリシー** モジュールには読み取りアクセス権だけがあります。  

アクセス許可の詳細については、Lookout の Web サイトの[こちらの記事](https://personal.support.lookout.com/hc/en-us/articles/114094105653)をご覧ください。

**グループ オブジェクト ID** は、**Azure AD 管理コンソール**のグループの **[プロパティ]** ページにあります。

![[グループ ID] フィールドが強調表示されているプロパティ ページのスクリーンショット](media/aad_group_object_id.png)

この情報を収集した後で、Lookout のサポート (メール: enterprisesupport@lookout.com) にお問い合わせください。

Lookout サポートは、主要連絡先を使用してサブスクリプションをオンボーディングし、収集された情報を使用して Lookout Enterprise アカウントを作成します。


## <a name="configure-your-subscription-with-lookout-device-threat-protection"></a>Lookout デバイス脅威保護でサブスクリプションを構成する
### <a name="step-1-set-up-your-device-threat-protection"></a>ステップ 1: デバイス脅威保護をセットアップする
Lookout サポートが Lookout Enterprise アカウントを作成した後、Lookout コンソールにサインインできます。   ログイン URL (https://aad.lookout.com/les?action=consent) へのリンクを含む Lookout からメールが、会社の主要連絡先に送信されます。

Lookout コンソールに初めてログインするときは、グローバル管理者の Azure AD の役割を持つユーザー アカウントを使う必要があります。Lookout は、Azure AD テナントを登録するためにこの情報を必要とします。   それ以降にユーザーがサインインするときは、このレベルの Azure AD 権限は不要です。  この最初のログインでは、同意ページが表示されます。 **[同意する]** を選んで登録を完了します。

![Lookout コンソールの初回ログイン ページのスクリーンショット](media/lookout-initial-login.png)

受け入れて同意すると、Lookout コンソールにリダイレクトされます。 最初の登録が済んだ後のログインは、URL (https://aad.lookout.com) を使って行うことができます。

ログインに問題がある場合は、[トラブルシューティングに関する記事]()をご覧ください。

以下の手順では、[Lookout コンソール](https://aad.lookout.com)で Lookout のセットアップを完了するために行う必要のあるタスクの概要を説明します。

### <a name="step-2-configure-the-intune-connector"></a>ステップ 2: Intune コネクタを構成する

1.  Lookout コンソールの **[System]** (システム) モジュールから、**[Connectors]** (コネクタ) タブを選択し、**[Intune]** を選択します。

  ![[Connectors] (コネクタ) タブが開き [Intune] オプションが強調表示されている Lookout コンソールのスクリーンショット](media/lookout-setup-intune-connector.png)

2.  接続設定のオプションで、ハートビートの頻度を分単位で構成します。  Intune コネクタの準備ができます。  

  ![ハートビートの頻度が構成された接続設定タブのスクリーンショット](media/lookout-connection-settings.png)

### <a name="step-3-configure-enrollment-groups"></a>ステップ 3: 登録グループを構成する
**[Enrollment Management]** (登録管理) オプションで、デバイスを Lookout に登録する必要があるユーザーのセットを定義します。 小さなユーザー グループから始めてテストし、統合のしくみを理解するのがベスト プラクティスです。  テスト結果に問題がなければ、他のユーザー グループに登録を拡張できます。

登録グループを使い始めるときは、最初に Azure AD セキュリティ グループを定義します。これは、Lookout デバイス脅威保護に初めて登録するのに適したユーザー セットです。 Azure AD でグループを作成した後、Lookout コンソールで **[Enrollment Management]** (登録管理) オプションに移動し、登録用に Azure AD セキュリティ グループの **[Display Name(s)]** (表示名) を追加します。

ユーザーが登録グループ内にいると、Azure AD で識別されてサポートされるすべてのデバイスが登録され、Lookout デバイス脅威保護のアクティブ化の対象になります。  サポートされるデバイスで Lookout for Work アプリを初めて開くと、デバイスが Lookout でアクティブ化されます。

![Intune コネクタ登録ページのスクリーンショット](media/lookout-enrollment.png)

新しいデバイスをチェックする時間の増分には既定値 (5 分) を使うのがベスト プラクティスです。

>[!IMPORTANT]
> 表示名は大文字と小文字が区別されます。  Azure Portal でセキュリティ グループの **[プロパティ]** ページに表示される **[表示名]** を使います。 下に示すセキュリティ グループの **[プロパティ]** ページでは、[表示名] が大文字で始まっていることに注意してください。  一方、タイトルはすべて小文字で表示されており、これを Lookout コンソールへの入力には使用しないでください。
>![Azure Portal での Azure Active Directory サービスの [プロパティ] ページのスクリーンショット](media/aad-group-display-name.png)

現在のリリースには次の制限があります。  
* グループの表示名の検証は行われません。  Azure Portal で Azure AD セキュリティ グループに表示される **[表示名]** フィールドの値を使用してください。
* グループ内にグループを作成することは、現在はサポートされていません。  指定されている Azure AD セキュリティ グループはユーザーのみを含むことができ、入れ子になったグループを含むことはできません。


### <a name="step-4-configure-state-sync"></a>ステップ 4: 状態の同期を構成する
**[State Sync]** (状態同期) オプションで、Intune に送信するデータの種類を指定します。  現在は、Lookout と Intune の統合が正常に動作するには、デバイスと脅威の両方の状態を有効にする必要があります。  これらは既定で有効になります。
### <a name="step-5-configure-error-report-email-recipient-information"></a>ステップ 5: エラー レポート メール受信者情報を構成する
**[Error Management]** (エラー管理) オプションで、エラー レポートを受け取る必要のあるメール アドレスを入力します。

![Intune コネクタ エラー管理ページのスクリーンショット](media/lookout-connector-error-notifications.png)

### <a name="step-6-configure-enrollment-settings"></a>ステップ 6:  登録の設定を構成する
**[System]** (システム) モジュールの **[Connectors]** (コネクタ) ページで、デバイスが切断と判断されるようになるまでの日数を指定します。  切断されたデバイスは非準拠と見なされ、SCCM 条件付きアクセス ポリシーに基づいて、社内アプリケーションへのアクセスをブロックされます。 1 ～ 90 日の範囲の値を指定できます。

![](media/lookout-console-enrollment-settings.png)

### <a name="step-7-configure-email-notifications"></a>ステップ 7: メール通知を構成する
脅威のメール通知を受け取る場合は、通知を受け取るユーザー アカウントで [Lookout コンソール](https://aad.lookout.com)にサインインします。 **[System]** (システム) モジュールの **[Preferences]** (設定) タブで、目的の通知を選んで **[ON]** (オン) に設定します。 変更内容を保存します。

![ユーザー アカウントが表示された設定ページのスクリーンショット](media/lookout-email-notifications.png) メール通知を受け取る必要がなくなったら、通知を **[OFF]** (オフ) に設定して変更を保存します。
### <a name="step-8-configure-threat-classification"></a>ステップ 8: が脅威の分類を構成する
Lookout のデバイス脅威保護は、さまざまな種類のモバイル脅威を分類します。 [Lookout の脅威分類](http://personal.support.lookout.com/hc/en-us/articles/114094130693)には、既定のリスク レベルが関連付けられています。 これらは、会社の要件に合わせていつでも変更できます。

![脅威と分類を示すポリシー ページのスクリーンショット](media/lookout-threat-classification.png)

>[!IMPORTANT]
> Intune 統合は実行時にこれらのリスク レベルに従ってデバイスのコンプライアンスを計算するため、ここで指定するリスク レベルはデバイス脅威保護の重要な側面です。 つまり、Intune 管理者は、デバイスが最低レベル (高、中、低) のアクティブな脅威を持っている場合に非準拠としてデバイスを識別するように、ポリシーのルールを設定します。 Lookout デバイス脅威保護の脅威分類ポリシーが、Intune のデバイス コンプライアンス計算に直接反映されます。

## <a name="watching-enrollment"></a>登録の監視
セットアップが完了すると、Lookout デバイス脅威保護は、指定された登録グループに対応するデバイスの Azure AD でのポーリングを開始します。  デバイス モジュールで登録されたデバイスに関する情報を検索できます。  デバイスの初期状態は保留中と表示されます。  デバイスで Lookout for Work アプリがインストールされ、開かれ、アクティブ化されると、デバイスの状態が変化します。  Lookout for Work アプリをデバイスにプッシュする方法の詳細については、「[Configure and deploy Lookout for work apps](configure-and-deploy-lookout-for-work-apps.md)」 (Lookout for work アプリを構成して展開する) トピックをご覧ください。
## <a name="next-steps"></a>次のステップ
[Intune 管理コンソールで Lookout MTP の接続を有効にする](enable-lookout-connection-in-intune.md)

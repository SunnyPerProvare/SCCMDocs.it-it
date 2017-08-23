---
title: "System Center Configuration Manager と Microsoft Intune を使ったハイブリッド Windows デバイス管理のセットアップ | Microsoft Docs"
description: "System Center Configuration Manager と Microsoft Intune を使用して Windows デバイス管理を設定します。"
ms.custom: na
ms.date: 03/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: "9"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 47348baeac26bfa2ad5016622fe4dbcb9f572483
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune を使ったハイブリッド Windows デバイス管理のセットアップ

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックでは、IT 管理者を対象に、ユーザーが Configuration Manager と Microsoft Intune を使用して、Windows PC とモバイル デバイスを管理できるようにする方法について説明します。

## <a name="enable-windows-device-management"></a>Windows デバイスの管理を有効にする
PC やモバイル デバイスの Windows デバイスの管理を有効にするには、次の手順を使用します。

1.  任意のプラットフォームの登録をセットアップする前に、「[ハイブリッド MDM をセットアップする](setup-hybrid-mdm.md)」に記載されている前提条件と手順を完了しておきます。  
2.  Configuration Manager コンソールの **[管理]** ワークスペースで、**[概要]** > **[クラウド サービス]** > **[Microsoft Intune サブスクリプション]** に移動します。  
3.  リボンで、**[プラットフォームの構成]** をクリックし、Windows プラットフォームを選択します。
    - Windows PC やラップトップの場合は、**[Windows]** を選択し、次の手順を実行します。
      1. **[全般]** タブで **[Windows の登録を有効にする]**をクリックします。
      2. 証明書を使用して会社ポータル アプリにコード署名して展開する場合は、「**コード署名証明書**」を参照してください。 デバイスのユーザーが Windows ストアから会社ポータル アプリをインストールすることも、管理者がコード署名せずにビジネス向け Windows ストアからアプリを展開することもできます。
      3. [Windows Hello for Business 設定](windows-hello-for-business-settings.md)を構成することもできます。
    - Windows Phone やタブレットの場合は、**[Windows Phone]** を選択し、次の手順を実行します。
      1. **[全般]** タブで、**[Windows Phone 8.1 と Windows 10 Mobile]** チェック ボックスをオンにします。 Windows Phone 8.0 はサポートされなくなりました。
      2. 組織で会社アプリをサイドロードする必要がある場合は、必要なトークンやファイルをアップロードできます。 アプリのサイドローディングの詳細については、「[Windows アプリの作成](https://docs.microsoft.com/sccm/apps/get-started/creating-windows-applications)」を参照してください。
        - **アプリケーション登録トークン**
        - **.pfx ファイル**
        - **[なし]** Symantec 証明書を使用する場合は、**[Symantec 証明書の有効期限が切れる前にアラートを表示する]** を指定できます。
4. [OK **** ] をクリックしてダイアログ ボックスを閉じます。  会社ポータルを使用して、登録プロセスを簡略化するには、デバイス登録用の DNS エイリアスを作成してください。 自分のデバイスを登録する方法をユーザーに通知することができます。

## <a name="choose-how-to-enroll-windows-devices"></a>Windows デバイスの登録方法を選択する

Intune ライセンスをユーザーに割り当てたら、Windows デバイスを追加の手順なしで登録できますが、ユーザーのために登録を簡単にすることができます。

Windows デバイスの登録を簡単にする方法は次の 2 つの要素で決まります。
- **Azure Active Directory Premium を使用していますか?** <br>[Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) は、Enterprise Mobility + Security およびその他のライセンス プランに付属します。
- **どのバージョンの Windows クライアントが登録されますか?** <br>Windows 10 デバイスは、職場または学校のアカウントを追加すると自動的に登録できます。 以前のバージョンでは、会社ポータル アプリを使用して登録する必要があります。

||**Azure AD Premium**|**その他の AD**|
|----------|---------------|---------------|  
|**Windows 10**|[自動登録](#enable-windows-10-automatic-enrollment) |[ユーザー登録](#enable-windows-enrollment-without-azure-ad-premium)|
|**以前の Windows バージョン**|[ユーザー登録](#enable-windows-enrollment-without-azure-ad-premium)|[ユーザー登録](#enable-windows-enrollment-without-azure-ad-premium)|

## <a name="enable-windows-10-automatic-enrollment"></a>Windows 10 の自動登録を有効にする

自動登録を使用して、職場や学校のアカウントを追加し、管理されることに同意すると、会社所有のデバイスや個人の Windows 10 PC および Windows 10 Mobile デバイスを Intune に登録できます。 このように簡単です。 ユーザーのデバイスはバックグラウンドで登録され、Azure Active Directory に参加します。 登録されると、デバイスは Intune で管理されます。

**必要条件**
- Azure Active Directory Premium サブスクリプション ([試用版サブスクリプション](http://go.microsoft.com/fwlink/?LinkID=816845))
- Microsoft Intune サブスクリプション


### <a name="configure-automatic-mdm-enrollment"></a>自動 MDM 登録の構成

1. [Azure 管理ポータル](https://portal.azure.com) (https://manage.windowsazure.com) にサインインし、**[Azure Active Directory]** を選択します。

  ![Azure ポータルのスクリーンショット](../media/auto-enroll-azure-main.png)

2. **[モビリティ (MDM および MAM)]** を選択します。

  ![Azure ポータルのスクリーンショット](../media/auto-enroll-mdm.png)

3. **[Microsoft Intune]** を選択します。

  ![Azure ポータルのスクリーンショット](../media/auto-enroll-intune.png)

4. **[MDM ユーザー スコープ]** を構成します。 Microsoft Intune で管理するユーザーのデバイスを指定します。 これらのユーザーの Windows 10 デバイスは、Microsoft Intune の管理対象として自動的に登録されます。

    - **なし**
    - **一部**
    - **すべて**

   ![Azure ポータルのスクリーンショット](../media/auto-enroll-scope.png)

5. 次の URL の既定値を使用します。
    - **MDM 使用条件 URL**
    - **MDM 探索 URL**
    - **MDM 準拠 URL**

6. **[保存]** を選択します。


既定では、サービスの 2 要素認証は有効になっていません。 ただし、デバイスを登録するときには 2 要素認証をお勧めします。 このサービスの 2 要素認証を要求する前に、Azure Active Directory で 2 要素認証プロバイダーを構成し、多要素認証用にユーザー アカウントを構成する必要があります。 「[クラウドでの Azure Multi-Factor Authentication Server の概要](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud)」を参照してください。

## <a name="enable-windows-enrollment-without-azure-ad-premium"></a>Azure AD Premium なしで Windows 登録を有効にする
Azure AD Premium 自動登録なしでデバイスを登録することをユーザーに許可できます。 ライセンスを割り当てると、ユーザーは、自分の職場のアカウントを個人所有のデバイスに追加するか、会社所有のデバイスを Azure AD に参加させることで登録できます。 DNS エイリアス (CNAME レコード タイプ) を作成すると、ユーザーは自分のデバイスを簡単に登録できるようになります。 DNS CNAME リソース レコードを作成すると、ユーザーは Intune サーバー名を入力することなく Intune に接続して登録できます。

### <a name="create-cnames-to-simplify-enrollment"></a>CNAME を作成して登録を簡単にする
会社のドメインの CNAME DNS リソース レコードを作成します。 たとえば、会社の Web サイトが contoso.com の場合、EnterpriseEnrollment.contoso.com を enterpriseenrollment-s.manage.microsoft.com にリダイレクトする CNAME を DNS に作成します。

CNAME DNS エントリの作成は省略可能ですが、CNAME レコードにより、ユーザーによる登録が簡単になります。 CNAME レコードの登録が見つからない場合、ユーザーは手動で MDM サーバー名 enrollment.manage.microsoft.com を入力するように求められます。

|型|ホスト名|指定先|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 時間|

複数の UPN サフィックスがある場合は、各ドメイン名について 1 つの CNAME レコードを作成し、それぞれで EnterpriseEnrollment s.manage.microsoft.com をポイントする必要があります。 たとえば、Contoso 社でユーザーが name@contoso.com を使用しており、電子メール/UPN として name@us.contoso.com と name@eu.constoso.com も使用している場合、Contoso の DNS 管理者は次の CNAME を作成する必要があります。

|型|ホスト名|指定先|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 時間|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 時間|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 時間|

`EnterpriseEnrollment-s.manage.microsoft.com` – Intune サービスへのリダイレクトと電子メールのドメイン名によるドメイン認識をサポートします。

DNS レコードの変更が反映されるまでには、最大で 72 時間かかります。 DNS レコードの変更が反映されるまで、Intune で DNS の変更を確認することはできません。

## <a name="tell-users-how-to-enroll-devices"></a>デバイスの登録方法をユーザーに通知する  

 セットアップが完了したら、デバイスを登録する方法をユーザーに知らせる必要があります。 ガイダンスとして[デバイスの登録についてユーザーに通知する項目](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune)に関する記事を参照してください。 ユーザーに「[Enroll your Windows device in Intune](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows)」 (Intune での Windows デバイスの登録) のページを案内します。 この情報は、Microsoft Intune と Configuration Manager の両方によって管理されるモバイル デバイスに適用されます。

> [!div class="button"]
[< 前のステップ](create-service-connection-point.md)  [次のステップ >](set-up-additional-management.md)

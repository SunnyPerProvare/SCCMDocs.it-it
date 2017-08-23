---
title: "Lookout for Work アプリの展開 | Microsoft Docs"
description: "Lookout for Work アプリを構成し、展開します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f62b763-4347-453d-b0a7-1f4a0d1d4105
caps.latest.revision: 
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 59f43c922d1d3bc64625733014b0def1e42c4d2d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="configure-and-deploy-lookout-for-work-apps"></a>Lookout for Work アプリを構成し、展開する

*適用対象: System Center Configuration Manager (Current Branch)*

この記事では、Android デバイス用と iOS デバイス用の Lookout for Work アプリを構成し、展開する方法について説明します。

## <a name="android-google-play-store-app"></a>Android (Google Play ストア アプリ)
1.  Configuration Manager コンソールで、**[ソフトウェア ライブラリ]** > **[アプリケーション管理]** > **[アプリケーション]** の順にクリックします。

2.  ソフトウェアの展開ウィザードの **[全般]** ページで、次の情報を指定します。
  * 種類: **[Android アプリケーション パッケージ (Google Play 内)]** を選択します。
  * 場所: Google Play ストアから Lookout for Work アプリ リンクをコピーし、ここに貼り付けます。
  * 発行元: Lookout Mobile Security
  * 名前: Lookout for Work
  * 説明: Lookout は、モバイルの脅威に対し最高レベルの保護性能があり、デバイスを安全に保ちます。 Lookout アプリをデバイスにインストールすると、デバイスが保護され、脅威が検出された場合、ユーザーと会社の管理者に通知されます。
  * 管理カテゴリ: コンピューター管理

  正常に完了すると、アプリケーションの一覧に Lookout for Work アプリが表示されます。

3.  **[ホーム]** タブの **[展開]** グループで、**[展開]** を選択し、Lookout for Work アプリをユーザーに展開します。
>[!IMPORTANT]
>Lookout MTP コンソールで登録管理オプションに追加した同じユーザーを選択する必要があります。

  **[必須のインストール]** オプションを選択し、Lookout アプリをユーザーのデバイスにインストールすることを要求します。

## <a name="ios-enterprise-signed-version-of-lookout-app"></a>iOS (Lookout アプリの Enterprise 署名版)

* **手順 1:** デバイスで **iOS 管理**がセットアップされていることを確認します。 デバイスの iOS 管理のセットアップ方法については、「[Set up iOS and Mac device management]()」 (iOS と Mac のデバイス管理のセットアップ) を参照してください。

* **手順 2:** Lookout for Work iOS アプリに**再署名**します。 Lookout により、その Lookout for Work iOS アプリが the iOS App Store の外部で配布されます。 **アプリの配布の前に**、iOS Enterprise Developer Certificate でアプリに再署名する必要があります。 Lookout for Work iOS アプリの再署名に関する詳細については、Lookout サイトの「[Lookout for Work iOS app re-signing process](https://personal.support.lookout.com/hc/en-us/articles/114094038714)」 (Lookout for Work iOS アプリの再署名プロセス) を参照してください。


* **手順 3:** 次の操作を行い、iOS ユーザーの Azure Active Directory 認証を有効にします。
  1.  [Azure Active Directory 管理ポータル](https://manage.windowsazure.com)にログインし、アプリケーション ページに移動します。
  2.  **Lookout for Work iOS アプリ**を**ネイティブ クライアント アプリケーション**として追加します。
  ![アプリの追加ダイアログのスクリーンショット。ネイティブ クライアント アプリ オプションが表示されています。](media/aad-add-app.png)

  3. **com.lookout.enterprise.yourcompanyname** を、IPA に署名したときに選択したカスタマー バンドル ID に置換します。
  4.  リダイレクト URI を追加します。**&lt;companyportal://code/>** の後に元のリダイレクト URI を URL エンコードしたものを続けます。
  5.  アプリに**委任されたアクセス許可**を追加します。

  詳細については、「[Configure a native client application](https://azure.microsoft.com/en-us/documentation/articles/app-service-mobile-how-to-configure-active-directory-authentication/#optional-configure-a-native-client-application)」 (ネイティブ クライアント アプリケーションを構成する) を参照してください。


* **手順 4:** 「[Create iOS applications in System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/apps/get-started/creating-ios-applications)」 (System Center Configuration Manager で iOS アプリケーションを作成する) トピックの説明に基づき、再署名された .ipa ファイルをアップロードします。 最小 OS バージョンを iOS 8.0 以降に設定します。


* **手順 5:** 「[Configure iOS apps with mobile app configuration policies in System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies)」 (System Center Configuration Manager で iOS アプリをモバイル アプリ構成ポリシーで構成する) トピックの説明に基づき、管理対象アプリの構成ポリシーを作成します。


* **手順 6:** **アプリをユーザーに展開するには**、**[アプリケーション]** ページで Lookout for Work アプリを選択し、**[ホーム]** タブの **[展開]** グループで **[展開]** を展開します。

  Lookout コンソールで登録管理オプションに追加した同じユーザーを選択する必要があります。  
**[必須のインストール]** オプションを選択し、Lookout アプリをユーザーのデバイスにインストールすることを要求します。

## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>展開したアプリをデバイスで開いたときの動作




デバイスで Lookout for Work を開くと、アプリをアクティベートし、[Azure Active Directory でサインインする] オプションを選択するように求められます。 次のトピックに、エンドユーザー フローの詳細なチュートリアルがあります。

* [Android デバイスで Lookout for Work のインストールを求められる](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

* [Lookout for Work が Android デバイスで検出した脅威を解決する必要がある](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)

## <a name="next-steps"></a>次のステップ
* [コンプライアンス ポリシーのデバイス脅威保護の規則を有効にする](enable-device-threat-protection-rule-compliance-policy.md)

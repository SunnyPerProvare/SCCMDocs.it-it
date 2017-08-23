---
title: "Azure サービス ウィザード | Microsoft Docs"
description: "System Center Configuration Manager の Azure サービス ウィザードについて"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 22203b358830903cf2e531c0532ae3111b8265fc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Configuration Manager と共に使用するように Azure サービスを構成する

*適用対象: System Center Configuration Manager (Current Branch)*

Current Branch バージョン 1706 以降、**Azure サービス ウィザード**を使用して、Configuration Manager で使用する Azure サービスの構成のプロセスを簡単にできます。

このウィザードの構成操作は一般的なものです。**Azure Web アプリ**を利用し、サブスクリプションと構成の詳細を提供します。 Web アプリを利用することで、Azure で新しい Configuration Manager コンポーネントやサービスをセットアップするたびに同じ情報を入力する必要がなくなります。

次の Azure サービスは Azure サービスの構成ウィザードで構成されます。
-   **クラウド管理**   
    [Azure Active Directory (Azure AD) を利用し、クライアントの認証を有効にする]() [Azure AD ユーザー探索を構成](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)することもできます。
-   **OMS コネクタ**
    [Operations Manager Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) (OMS) に接続し、OMS Log Analytics にコレクションなどのデータを同期します。
-   **Upgrade Readiness**
    [Upgrade Readiness に接続](/sccm/core/clients/manage/upgrade/upgrade-analytics)し、クライアント アップグレード互換性データを表示します。
-   **Windows Store for Business** [Windows Store for Business](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) のオンライン ストアに接続し、Configuration Manager でデプロイできるアプリを組織のために入手します。

ウィザードでサービスを構成するとき、いくつかの共通アクションがあります。
次の設定があります。
-   Azure 環境を構成する: ウィザードの **[アプリ]** ページで、使用する **Azure 環境**を選択します。 サービスごとのコンテンツを参照し、公共の Azure クラウドのみに対応しているか、プライベート クラウドにも対応しているか確認してください。
-   サーバー アプリを作成またはインポートする: ウィザードの **[アプリ]** ページで、Azure Web アプリを**作成**し、**インポート**できます。 利用できるオプションは、構成しているサービスによって異なります。  さらに、他のアプリが必要になるサービスもあります。 たとえば、**ネイティブ クライアント アプリ**も必要とするサービスがあります。


Azure Web アプリの詳細については、「[Azure App Service での認証および承認](/azure/app-service/app-service-authentication-overview)」と「[Web Apps の概要](/azure/app-service-web/app-service-web-overview)」を参照してください。


## <a name="webapp"></a> Configuration Manager と共に使用するように Azure Web アプリを作成する

Azure サービス Web アプリは Configuration Manager サイトを Azure AD に接続します。このアプリは、ご利用のインフラストラクチャで Azure サービスを使用するための前提条件です。 手順は次のとおりです。

1.  Configuration Manager コンソールの **[管理]** ワークスペースで、**[クラウド サービス]** を展開して、**[Azure サービス]** をクリックします。
2.  **[ホーム]** タブの **[Azure サービス]** グループで、**[Azure サービスの構成]** をクリックします。
3.  Azure サービス ウィザードの **[Azure サービス]** ページで、**[クラウド管理]** を選択して、クライアントが Azure AD を使用して、階層で認証できるようにします。
4.  ウィザードの **[全般]** ページで、Azure サービスの名前と説明を指定します。
5.  ウィザードの **[アプリ]** ページで、一覧から Azure 環境を選択し、**[参照]** をクリックして Azure サービスの構成に利用する *Web アプリ*と*ネイティブ クライアント アプリ*を選択します。     
    **Web アプリ:** [参照] をクリックすると、[サーバー アプリ] ウィンドウが開きます。    
      **[サーバー アプリ]** ウィンドウで、使用するサーバー アプリを選択し、**[OK]** をクリックします。 サーバー アプリとは、Azure アカウントの構成 (クライアントのテナント ID、クライアント ID、シークレット キーなど) を格納する Azure Web アプリです。
    利用可能なアプリがない場合は、次のいずれかを使用します。
        - **作成**: 新しいセッションを作成するには、**[作成]** をクリックします。 次に、アプリのフレンドリ名、ホームページ URL、アプリ ID URI、シークレット キーの有効期間を指定します。 既定では、シークレット キーの有効期間は 1 年間です。

         続行するには、誰かが Azure にサインインし、Azure で Web アプリ作成を完了する必要があります。 Azure のサインインに使用するアカウントは、Azure サービス ウィザードを実行するアカウントと同じである必要はありません。 Azure にサインインすると、Configuration Manager によって、Azure で Web アプリと、Web アプリで使用するクライアント ID やシークレット キーが作成されます。 その後、Azure Portal からこれらを表示できます。

         [作成] を利用して Web アプリを構成するとき、Configuration Manager は Azure AD で Web アプリを自動的に作成できます。
        - **インポート**: Azure サブスクリプションに既に存在する Web アプリを使用するには、**[インポート]** をクリックします。 アプリとテナントのフレンドリ名を指定し、Configuration Manager で使用する Azure Web アプリのテナント ID、クライアント ID、シークレット キーを指定します。 情報を確認した後、**[OK]** をクリックして続行します。

          このオプションは一部のサービスでは利用できないことがあります。

   **ネイティブ クライアント アプリ:** [参照] をクリックすると、[クライアント アプリ] ウィンドウが開きます。  
     **[クライアント アプリ]** ウィンドウで、使用するクライアント アプリを選択し、**[OK]** をクリックします。

     利用可能なクライアント アプリがない場合は、次のいずれかを使用します。
     - **作成**: 新しいクライアント アプリを作成するには、**[作成]** をクリックします。 次に、アプリのフレンドリ名と応答 URL を指定します。

          続行するには、誰かが Azure にサインインし、Azure でクライアント アプリ作成を完了する必要があります。 Azure のサインインに使用するアカウントは、Azure サービス ウィザードを実行するアカウントと同じである必要はありません。 Azure にサインインすると、Configuration Manager によって、Azure でネイティブ クライアント アプリが自動的に作成されます。これには、Web アプリで使用するためのクライアント ID が含まれます。 その後、Azure Portal からこれらを表示できます。
          [作成] を利用してアプリを構成するとき、Configuration Manager は Azure AD でネイティブ クライアント アプリを自動的に作成できます。
     - **インポート**: Azure サブスクリプションに既に存在するクライアント アプリを使用するには、**[インポート]** をクリックします。 アプリのフレンドリ名とクライアント ID を指定します。 **[OK]** をクリックして続行します。
           このオプションは一部のサービスでは利用できないことがあります。

  <!--  MOVE THIS AND STEP 6 TO configure Azure AD User Discover  content
       [!TIP]  
     When you use Import, the account you use to run the wizard must have the *Read directory data* application permission in the Azure portal. This is required to set the correct permissions for the App. When you use Create, Configuration Manager creates the app with the correct permissions. However, you still must give consent to the application in the Azure portal.   -->


6.  ウィザードの **[検出]** ページで、**[Azure Active Directory ユーザーの探索を有効にする]** をクリックし、**[設定]** をクリックします。
**[Azure AD ユーザー探索設定]** ダイアログ ボックスで、検出を実行するスケジュールを設定します。 Azure AD の新規または変更されたアカウントのみをチェックする差分探索を有効にすることもできます。 Azure AD ユーザー探索の詳細については[こちら](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc)をご覧ください。
 
 7. ウィザードを完了します。

この時点で、Configuration Manager サイトが Azure AD に接続されています。

## <a name="view-the-configuration-of-an-azure-service"></a>Azure サービスの構成を表示する
構成した Azure サービスのプロパティを表示できます。

コンソールで、**[管理]** > **[概要]** > **[Cloud Services]** > **[Azure サービス]** の順に進みます。 次に、表示または編集するサービスを選択し、**[プロパティ]** をクリックします。

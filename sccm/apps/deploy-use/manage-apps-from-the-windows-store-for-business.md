---
title: "ビジネス向け Windows ストアからのアプリの管理 | Microsoft Docs"
description: "System Center Configuration Manager を使用してビジネス向け Windows ストアからアプリを管理および展開します。"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
caps.latest.revision: "11"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 369b6a82a20a90ca534f9484c0be71096dd35a30
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="manage-apps-from-the-windows-store-for-business-with-system-center-configuration-manager"></a>System Center Configuration Manager によるビジネス向け Windows ストアからのアプリの管理
[ビジネス向け Windows ストア](https://www.microsoft.com/business-store)は、組織向けの Windows アプリを検索して、個別に、または一括で購入できる場所です。 Configuration Manager にストアを接続することで、購入したアプリの一覧と Configuration Manager を同期できます。 同期後、Configuration Manager コンソールでアプリを表示し、他のアプリを展開する場合と同様に展開できます。


## <a name="online-and-offline-apps"></a>オンライン アプリとオフライン アプリ

ビジネス向け Windows ストアは、次の 2 種類のアプリをサポートしています。

- **オンライン** - この種類のライセンスでは、ユーザーとデバイスはストアに接続してアプリとそのライセンスを取得する必要があります。 Windows 10 デバイスは、Azure Active Directory ドメインに参加している必要があります。
- **オフライン** - ストアに接続したり、インターネットに接続したりせずに、アプリとライセンスをキャッシュし、オンプレミス ネットワーク内で直接展開できます。

ビジネス向け Windows ストアの詳細については、[こちら](https://technet.microsoft.com/itpro/windows/whats-new/windows-store-for-business-overview?f=255&MSPPError=-2147217396)を参照してください。

Configuration Manager では、Configuration Manager クライアントを実行している Windows 10 デバイスと、Microsoft Intune に登録されている Windows 10 デバイスの両方でビジネス向け Windows ストアのアプリを管理できます (ハイブリッド構成と呼ばれます)。 Configuration Manager は、オンラインおよびオフライン アプリ向けに次の機能を提供します。

> [!IMPORTANT]
> この機能を使用するには、Windows 10 デバイスで 2015 年 11 月 (1511) リリース以降が実行されている必要があります。


|機能|オフライン アプリ|オンライン アプリ|
|------------|------------|------------|
|アプリ データと Configuration Manager の同期<br>(同期は 24 時間ごとに発生)|○|○|
|ストア アプリからの Configuration Manager アプリケーションの作成|○|○|
|ストアからの無料アプリのサポート|○|○|
|ストアからの有料アプリのサポート|×|○|
|ユーザーまたはデバイス コレクションへの必要な展開のサポート|○|○|
|ユーザーまたはデバイス コレクションへの利用可能な展開のサポート|○|○|
|ストアからの基幹業務アプリのサポート|○|○|

Configuration Manager クライアントを含む Windows 10 PC にオンライン ライセンス アプリを展開するには、Windows 10 Creators Update 以降を実行する必要があります。

## <a name="deploying-online-apps-using-the-windows-store-for-business-with-pcs-that-run-the-configuration-manager-client"></a>Configuration Manager クライアントを実行している PC でのビジネス向け Windows ストアを使用したオンライン アプリの展開
完全な Configuration Manager クライアントを実行している PC にビジネス向け Windows ストア アプリを展開する前に、次のことを考慮してください。

- すべての機能を利用するには、PC で Windows 10 Creators Update 以降を実行する必要があります。
- PC は Azure Active Directory に社内参加済みで、管理ツールとしてビジネス向け Windows ストアを登録したのと同じ AAD テナントにある必要があります。
- PC は、組み込み管理者アカウントでログインしているときに、ビジネス向け Windows ストア アプリにアクセスできません。
- PC にはビジネス向け Windows ストアへのライブ インターネット接続が必要です。

### <a name="notes-for-pcs-running-earlier-versions-of-windows-10"></a>以前のバージョンの Windows 10 を実行している PC に関する注記
(Configuration Manager クライアントを含む) Creators Update より前のバージョンの Windows 10 を実行している PC では、次の機能が適用されます。


- アプリケーションをインストールするユーザー、インストール期限に達するアプリケーション、必須の展開のインストール後の再評価によりインストールが実行された場合:
    - アプリケーションはビジネス向け Windows ストア アプリを起動することで "実行" されます。 
    - したがって、アプリがインストールされる前に、エンド ユーザーはストアからインストールを完了する必要があります。
    - Configuration Manager コンソールではアプリケーション ステータスは失敗と報告され、"Windows Store アプリをクライアント PC で開いています。ユーザーがインストールを完了するのを待機しています" というエラーが表示されます。
- 次のアプリケーションの評価サイクル時:
    - アプリケーションがストアからエンド ユーザーによってインストールされた場合、そのアプリケーションで報告されるステータスは **[成功]** となります。 
    - エンド ユーザーがストアからのアプリのインストールを試行しなかった場合:
        - 必須の展開でストアの起動が試行され、アプリケーションのインストールが再度実行されます。
        - 利用可能な展開は再実行されません。

#### <a name="further-notes-for-pcs-running-earlier-versions-of-windows-10"></a>以前のバージョンの Windows 10 を実行している PC についてのその他の注記:

- ビジネス向け Windows ストアから基幹業務アプリを展開することはできません。
- ストアから有料アプリを展開する場合、エンド ユーザーはストアにログインし、アプリ自体を購入する必要があります。
- コンシューマー バージョンの Windows Store へのアクセスを無効にしてグループ ポリシーを展開した場合、ビジネス向け Windows ストアが有効な場合でも、ビジネス向け Windows ストアから展開することはできません。


## <a name="set-up-windows-store-for-business-synchronization"></a>ビジネス向け Windows ストアの同期の設定

### <a name="for-configuration-manager-versions-prior-to-1706"></a>1706 より前の Configuration Manager バージョンの場合

**Azure Active Directory で、"Web アプリケーションや Web API" 管理ツールとして Configuration Manager を登録します。これで、後で必要になるクライアント ID が与えられます。**
1. [https://manage.windowsazure.com](https://manage.windowsazure.com) の Active Directory ノードで、Azure Active Directory を選択し、[**アプリケーション**]  >  [**追加**] をクリックします。
2.  **[組織で開発中のアプリケーションを追加]** をクリックします。
3.  アプリケーションの名前を入力し、**[Web アプリケーション]** または **[Web API]**、あるいはその両方を選択し、**次へ進む**矢印をクリックします。
4.  **[サインオン URL]** と **[アプリケーション ID/URI]** の両方に同じ URL を入力します。 URL はあらゆるものを使用でき、実際のアドレスに解決する必要はありません。 たとえば、*https://yourdomain/sccm*を入力できます。
5.  ウィザードを完了します。

**Azure Active Directory で、登録済み管理ツールのクライアント キーを作成します。**
1.  作成したアプリケーションを強調表示し、**[構成]** をクリックします。
2.  **[キー]** で、リストから期間を選択して、**[保存]** をクリックします。 これで新しいクライアント キーが作成されます。 ビジネス向け Windows ストアを Configuration Manager に正常にオンボードするまで、このページから移動しないでください。

**ビジネス向け Windows ストアで、ストア管理ツールとして Configuration Manager を構成します。**
1.  [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools) を開き、サインインを求められたらサインインします。
2.  要求された場合は、使用条件に同意します。
3.  **[管理ツール]** で、**[Add a management tool]** (管理ツールを追加) をクリックします。
4.  **[Search for the tool by name]** (名前でツールを検索) で、先ほど AAD で作成したアプリケーションの名前を入力して、**[追加]** クリックします。
5.  インポートしたアプリケーションの横にある **[アクティブ化]** をクリックします。
6.  オフラインでライセンスされるアプリケーションを購入する場合、**[管理] > [アカウント情報]** ページで、**[オフラインでライセンスされたアプリの表示]** をクリックします。

**ストアのアカウントを Configuration Manager に追加します。**

1. ビジネス向け Windows ストアから少なくとも 1 つのアプリを購入したことを確認します。 Configuration Manager コンソールの**管理**ワークスペースで、[**Cloud Services**] を展開して、[**ビジネス向け Windows ストア**] をクリックします。
2.  **[ホーム]** タブの**[ビジネス向け Windows ストア]** グループで、**[ビジネス向け Windows ストア アカウントの追加]** をクリックします。 
3.  Azure Active Directory からテナント ID、クライアント ID、クライアント キーを追加し、ウィザードを完了します。
4. 完了した時点で、Configuration Manager コンソールの **[ビジネス向け Windows ストア]** で構成されたアカウントが表示されます。

### <a name="for-configuration-manager-version-1706-and-later"></a>1706 以降の Configuration Manager バージョンの場合

1. コンソールで、**[管理]** > **[概要]** > **[クラウド サービスの管理]** > **[Azure]** > **[Azure サービス]** に移動し、**[Azure サービスの構成]** を選択して、**Azure サービス ウィザード**を開始します。
2. **[Azure サービス]** ページで、構成するサービスを選択し、**[次へ]** をクリックします。
3. **[全般]** ページで、[Azure サービス名] のフレンドリ名とオプションの説明を入力し、**[次へ]** をクリックします。
4. **[アプリ]** ページで、Azure 環境を指定し、**[参照]** をクリックして **[サーバー アプリ]** ウィンドウを開きます。
5. **[サーバー アプリ]** ウィンドウで、使用するサーバー アプリを選択し、**[OK]** をクリックします。 サーバー アプリとは、Azure アカウントの構成 (クライアントのテナント ID、クライアント ID、シークレット キーなど) を格納する Azure Web アプリです。 利用可能なサーバー アプリがない場合は、次のいずれかを使用します。
    - **作成**: 新しいセッションを作成するには、**[作成]** をクリックします。 アプリとテナントのフレンドリ名を指定します。 次に、Azure にサインインすると、Configuration Manager によって、Azure で Web アプリと、Web アプリで使用するクライアント ID やシークレット キーが作成されます。 その後、Azure Portal からこれらを表示できます。
    - **インポート**: Azure サブスクリプションに既に存在する Web アプリを使用するには、**[インポート]** をクリックします。 アプリとテナントのフレンドリ名を指定し、Configuration Manager で使用する Azure Web アプリのテナント ID、クライアント ID、シークレット キーを指定します。 情報を**確認**した後、**[OK]** をクリックして続行します。 
6. **[情報]** ページを確認し、指示に従って、追加の手順と構成を完了します。 これらの構成は、Configuration Manager でサービスを使用するために必要です。 たとえば、ビジネス向け Windows ストアを構成するには
    - Azure で、Configuration Manager を Web アプリケーションまたは Web API 管理ツールとして登録し、クライアント ID を記録します。 また、管理ツール (Configuration Manager) で使用するためのクライアント キーを指定します。
    - ビジネス向け Windows ストア コンソールで、ストアの管理ツールとして Configuration Manager を構成し、オフラインのライセンスされたアプリのサポートを有効にするには、少なくとも 1 つのアプリを購入する必要があります。 
7. 操作を続行する準備ができたら **[次へ]** をクリックします。
8. **[アプリケーションの構成]** ページで、このサービスのアプリケーション カタログと言語の構成を完了し、**[次へ]** をクリックします。
9. ウィザードが完了したのち、Configuration Manager コンソールに**ビジネス向け Windows ストア**を**クラウド サービスの種類**として構成したことが示されます。




## <a name="create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-app"></a>ビジネス向け Windows ストアのアプリから Configuration Manager アプリケーションを作成して展開します。
1.  Configuration Manager コンソールの **[ソフトウェア ライブラリ]** ワークスペースで **[アプリケーション管理]** を展開し、**[ストア アプリのライセンス情報]** をクリックします。
2.  展開するアプリを選び、**[ホーム]** タブの **[作成]** グループで、**[アプリケーションの作成]** をクリックします。
ビジネス向け Windows ストアのアプリを含む Configuration Manager アプリケーションが作成されます。 他の Configuration Manager のアプリケーションと同様に、このアプリケーションを展開して監視できます。

> [!IMPORTANT]
> Intune に登録されたデバイスの場合、展開されたアプリは当初デバイスを登録したユーザーのみが利用できます。 それ以外のユーザーはアプリにアクセスできません。

## <a name="next-steps"></a>次のステップ

**[ソフトウェア ライブラリ]** ワークスペースで **[アプリケーション管理]** を展開し、**[ストア アプリのライセンス情報]** をクリックします。

管理するストア アプリごとに、アプリの情報を表示できます。これには、アプリの名前、プラットフォーム、所有しているアプリのライセンスの数、利用可能なライセンスの数が含まれます。

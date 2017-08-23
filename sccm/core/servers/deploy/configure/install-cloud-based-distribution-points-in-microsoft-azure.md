---
title: "クラウドベースの配布ポイントのインストール | Microsoft Docs"
description: "Microsoft Azure でクラウドベース配布ポイントの使用を開始するために必要なことについて説明します。"
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
caps.latest.revision: "7"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 39b35cccf78bba4e69a7de0ca3a5a8dc516201e3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="install-cloud-based-distribution-points-in-microsoft-azure-for-system-center-configuration-manager"></a>Microsoft Azure for System Center Configuration Manager のクラウド ベース配布ポイントのインストール

*適用対象: System Center Configuration Manager (Current Branch)*

Microsoft Azure では、System Center Configuration Manager のクラウドベース配布ポイントをインストールできます。 クラウドベースの配布ポイントに関する詳細については、「[クラウドベースの配布ポイントの使用](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)」を参照してください。

 インストールを開始する前に、必要な証明書ファイルがあることを確認します。  

-   .cer ファイルと .pfx ファイルにエクスポートされた Microsoft Azure 管理証明書  

-   .pfx ファイルにエクスポートされた、Configuration Manager のクラウドベースの配布ポイントのサーバー証明書  

    > [!TIP]
    >   これらの証明書の詳細については、「[System Center Configuration Manager での PKI 証明書の要件](../../../../core/plan-design/network/pki-certificate-requirements.md)」トピックのクラウドベースの配布ポイントの部分を参照してください。 クラウドベースの配布ポイントのサービス証明書を展開する例については、「[System Center Configuration Manager PKI 証明書の展開手順の例: Windows Server 2008 証明機関](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)」トピックの「クラウドベースの配布ポイント用のサービス証明書の展開」を参照してください。  


 クラウドベースの配布ポイントをインストールすると、Azure によって自動的にサービスの GUID が生成され、**cloudapp.net**の DNS サフィックスに追加されます。 この GUID を使用して、DNS エイリアス (CNAME レコード) で DNS を構成する必要があります。 これにより、Configuration Manager のクラウドベースの配布ポイントのサービス証明書に定義しているサービス名を自動的に生成された GUID にマップすることができます。  

 プロキシ Web サーバーを使用する場合は、配布ポイントをホストするクラウド サービスとの通信を有効にするように、プロキシ設定を構成することが必要になる可能性があります。  

##  <a name="BKMK_ConfigWindowsAzureandInstallDP"></a> Azure の設定とクラウドベースの配布ポイントのインストール  
 配布ポイントをサポートするように Azure を設定してから、Configuration Manager でクラウドベースの配布ポイントをインストールするには、次の手順に従います。  

### <a name="to-set-up-a-cloud-service-in-azure-for-a-distribution-point"></a>配布ポイント用に Azure にクラウド サービスを設定するには  

1.  Web ブラウザーを開いて Azure ポータル (https://manage.windowsazure.com) に移動し、自分のアカウントにアクセスします。  

2.  **[ホステッド サービス、ストレージ アカウント、CDN]** をクリックしてから、**[管理証明書]** を選択します。  

3.  サブスクリプションを右クリックしてから、[ **証明書の追加** ] を選択します。  

4.  [**証明書ファイル**] で、このクラウド サービスに使用する、エクスポートした Azure 管理証明書が含まれている .cer ファイルを指定してから、[**OK**] をクリックします。  

管理証明書が Azure に読み込まれて、クラウドベースの配布ポイントをインストールできるようになります。  

### <a name="to-install-a-cloud-based-distribution-point-for-configuration-manager"></a>Configuration Manager 用にクラウドベースの配布ポイントをインストールするには  

1.  管理証明書を使って Azure にクラウド サービスを設定する、前述の手順を完了します。  

2.  Configuration Manager コンソールの [**管理**] ワークスペースで、[**クラウド サービス**] を展開して、[**クラウド配布ポイント**] を選択します。 [**ホーム**] タブで、[**クラウド配布ポイントの作成**] をクリックします。  

3.  クラウドの配布ポイントの作成ウィザードの [**全般**] タブで、次のように設定します。  

    -   Azure アカウントの [**サブスクリプション ID**] を指定します。  

        > [!TIP]  
        >  自分の Azure サブスクリプション ID は、Azure ポータルで確認できます。  

    -   [ **管理証明書** ] を指定します。 [**参照**] をクリックして、エクスポートされた Azure 管理証明書が含まれている .pfx ファイルを指定してから、証明書のパスワードを入力します。 必要に応じて、Azure SDK 1.7 のバージョン 1 の .publishsettings ファイルを指定できます。  

4.  [ **次へ** ] をクリックします。 Configuration Manager が Azure に接続して管理証明書を検証します。  

5.  [ **設定** ] ページで、以下を完了してから [ **次へ** ] をクリックします。  

    -   [**地域**] で、この配布ポイントをホストするクラウド サービスを作成する、Azure の地域を選択します。  

    -   [**証明書ファイル**] に、Configuration Manager クラウドベースの配布ポイント サービスにエクスポートされた証明書を含む .pfx ファイルを指定します。 パスワードを入力します。  

        > [!NOTE]  
        >  [**サービスの FQDN**] ボックスには、証明書のサブジェクト名から自動的に入力されます。 ほとんどの場合、編集する必要はありません。 テスト環境でワイルドカード証明書を使用している場合は例外です。 たとえば、この場合、ホスト名を指定せずに、同じ DNS サフィックスを持つ複数のコンピューターが証明書を使用できるようすることができます。 このシナリオでは、証明書のサブジェクトには **CN=\*.contoso.com** のような値が含まれており、Configuration Manager によって、正しい FQDN を指定する必要があることを示すメッセージが表示されます。 [ **OK** ] をクリックしてメッセージを閉じてから、DNS サフィックスの前に特定の名前を入力して、完全な FQDN を指定します。 たとえば、 **clouddp1** を追加して、 **clouddp1.contoso.com**のサービスの完全な FQDN を指定します。 サービスの FQDN は、ドメインの中で固有である必要があり、ドメインに参加している他のデバイスと同じ FQDN は使用できません。  
        >   
        >  ワイルドカード証明書は、テスト環境でのみサポートされています。  

6.  [**アラート**] ページで、記憶域クォータ、転送クォータを設定し、Configuration Manage にアラートを生成させるそれぞれのクォータの使用率を指定します。 **[次へ]**をクリックします。  

7.  ウィザードを完了します。  

クラウドベースの配布ポイントの新しいホステッド サービスが作成されます。 ウィザードを閉じたら、Configuration Manager コンソールでクラウドベースの配布ポイントのインストールの進行状況を監視できます。 プライマリ サイト サーバーで **CloudMgr.log** ファイルを監視することもできます。 Azure ポータルでクラウド サービスのプロビジョニングを監視することができます。  

> [!NOTE]  
>  Azure に新しい配布ポイントをプロビジョニングするのに最大 30 分かかる可能性があります。 ストレージ アカウントがプロビジョニングされるまで、**CloudMgr.log** ファイルに次のメッセージが繰り返し出力されます。**コンテナーが存在するかどうかのチェックを待機しています。10 秒後にもう一度確認します**。 その後、サービスが作成されて構成されます。  

 次の方法を使用すると、クラウドベースの配布ポイントのインストールが完了したことを確認できます。  

-   Azure ポータルで、クラウドベースの配布ポイントの [**展開**] にステータス [**準備完了**] と表示されます。  

-   Configuration Manager コンソールの [**管理**] ワークスペースで、[**階層の構成**]、[**クラウド**] ノードに、クラウドベースの配布ポイントのステータスが [**準備完了**] として表示されます。  

-   Configuration Manager に、SMS_CLOUD_SERVICES_MANAGER コンポーネントのステータス メッセージ ID **9409** が表示されます。  

##  <a name="BKMK_ConfigDNSforCloudDPs"></a> クラウドベースの配布ポイントの名前解決の設定  
 クライアントは、クラウドベースの配布ポイントにクライアントがアクセスするためには、クラウドベースの配布ポイントの名前を Azure で管理される IP アドレスに解決できる必要があります。 クライアントでは、これを 2 段階で行います。  

1.  クライアントは、Configuration Manager のクラウドベースの配布ポイントのサービスの証明書に指定されているサービス名を Azure サービスの FQDN にマップします。 この FQDN には、 **cloudapp.net**の GUID と DNS サフィックスが含まれています。 GUID は、クラウドベースの配布ポイントがインストールされると自動的に生成されます。 Azure ポータルで完全な FQDN を確認するには、クラウド サービスのダッシュボードにある [**サイトの URL**] を参照します。 サイトの URL の例として、 **http://d1594d4527614a09b934d470.cloudapp.net**があります。  

2.  クライアントは、Azure サービスの FQDN を Azure によって割り当てられる IP アドレスに解決します。 この IP アドレスも、Azure ポータルのクラウド サービスのダッシュボードで確認できます。名前は、[**公開仮想 IP アドレス (VIP)**] です。  

Configuration Manager のクラウドベースの配布ポイントのサービス証明書に指定されているサービス名 (たとえば **clouddp1.contoso.com**) を Azure サービスの FQDN (たとえば **d1594d4527614a09b934d470.cloudapp.net**) にマップするためには、インターネット上の DNS サーバーに DNS エイリアス (CNAME レコード) が構成されている必要があります。 これにより、クライアントでは、インターネット上の DNS サーバーを使用して、Azure サービスの FQDN を IP アドレスに解決できます。  

##  <a name="BKMK_ConfigProxyforCloud"></a> クラウド サービスを管理するプライマリ サイトのプロキシ設定の設定  
 Configuration Manager でクラウド サービスを使用するときに、クラウドベースの配布ポイントを管理するプライマリ サイトが、Azure ポータルに接続できる必要があります。 サイトは、プライマリ サイト コンピューターの**システム**アカウントを使用して接続します。 この接続は、プライマリ サイト サーバー コンピューターの既定の Web ブラウザーを使用して行われます。  

 クラウドベースの配布ポイントを管理するプライマリ サイト サーバーで、プライマリ サイトがインターネットと Azure にアクセスできるように、プロキシ設定を設定することが必要になる場合があります。  

 Configuration Manager コンソールでプライマリ サイト サーバーのプロキシ設定を設定するには、次の手順に従います。  

> [!TIP]  
>  プライマリ サイト サーバーに新しいサイト システムの役割をインストールするときに、**サイト システムの役割の追加ウィザード**を使用してプロキシ サーバーを設定することもできます。  

#### <a name="to-set-up-proxy-settings-for-the-primary-site-server"></a>プライマリ サイト サーバーのプロキシ設定を設定するには  

1.  Configuration Manager コンソールで、[ **管理**] をクリックします。  

2.  **[管理]** ワークスペースで、 **[サイトの構成]**を展開して **[サーバーとサイト システムの役割]**をクリックします。 次に、クラウドベースの配布ポイントを管理するプライマリ サイト サーバーを選択します。  

3.  詳細ウィンドウで、[ **サイト システム**] を右クリックし、[ **プロパティ**] をクリックします。  

4.  [**サイト システムのプロパティ**] で [**プロキシ**] タブを選択し、そのプライマリ サイト サーバーのプロキシ設定を構成します。  

5.  [**OK**] をクリックして設定を保存します。  

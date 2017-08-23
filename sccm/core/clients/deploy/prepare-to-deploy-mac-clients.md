---
title: "Mac コンピューターにクライアント ソフトウェアを展開するための準備 | Microsoft ドキュメント"
description: "Configuration Manager クライアントを Mac コンピューターに展開する前の構成タスク。"
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: aaroncz
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
caps.latest.revision: "12"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: b3bb72f81812705b4654e268025074402e89a7cb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>Mac コンピューターにクライアント ソフトウェアを展開するための準備

*適用対象: System Center Configuration Manager (Current Branch)*

[Configuration Manager クライアントを Mac コンピューターに展開](/sccm/core/clients/deploy/deploy-clients-to-macs)する準備ができていることを確認するには、以下の手順に従ってください。 

## <a name="mac-prerequisites"></a>Mac の前提条件

Configuration Manager メディアでは、Mac クライアント インストール パッケージは提供されません。 [Microsoft ダウンロード センター](http://go.microsoft.com/fwlink/?LinkID=525184)から、**追加のオペレーティング システム用のクライアント**をダウンロードします。  

**サポートされるバージョン:**  

-   **Mac OS X 10.6** (Snow Leopard) 

-   **Mac OS X 10.7** (Lion) 

-   **Mac OS X 10.8** (Mountain Lion)

-   **Mac OS X 10.9** (Mavericks)

-   **Mac OS X 10.9** (Mavericks)  

-   **Mac OS X 10.10** (Yosemite)  

-   **Mac OS X 10.11** (El Capitan)  

-   **Mac OS X 10.12** (macOS Sierra)  

## <a name="certificate-requirements"></a>証明書の要件
Mac コンピューターにクライアントをインストールして管理するには、公開キー基盤 (PKI) 証明書が必要です。 PKI 証明書は、相互認証と暗号化データ転送を使用して、Mac コンピューターと Configuration Manager サイト間の通信を保護します。 Configuration Manager では、Microsoft 証明書サービスを使用して、エンタープライズ証明機関 (CA) と、Configuration Manager 登録ポイントおよび登録プロキシ ポイント サイト システムの役割に、ユーザー クライアント証明書を要求してインストールできます。 または、証明書が Configuration Manager の要件を満たしている場合、Configuration Manager とは独立して、コンピューター証明書を要求してインストールできます。   
  
Configuration Manager の Mac クライアントは常に証明書失効確認を実行します。 この機能を無効にすることはできません。  
  
Mac クライアントで、CRL の場所を特定できないことが原因でサーバー証明書の証明書失効ステータスを確認できない場合、クライアントは Configuration Manager サイト システムに正常に接続できなくなります。 特に、Mac クライアントが発行側の証明機関とは別のフォレストにある場合、CRL の設計を確認して、サイト システム サーバーに接続するために、Mac クライアントが CRL 配布ポイント (CDP) の場所を特定し、接続できるようにしてください。  

Mac コンピューターに構成マネージャー クライアントをインストールする前に、クライアント証明書をインストールする方法を決定します。  

-   [CMEnroll ツール](/sccm/core/clients/deploy/deploy-clients-to-macs#install-the-client-and-then-enroll-the-client-certificate-on-the-mac) を使用して Configuration Manager 登録を使用する。 登録プロセスでは自動証明書更新がサポートされていないため、インストールされている証明書が期限切れになる前に、Mac コンピューターを再登録する必要があります。  

-   [Configuration Manager とは独立した証明書の要求とインストールの方法を使用する](/sccm/core/clients/deploy/deploy-clients-to-macs#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager)。  

Mac クライアントの証明書の要件と、Mac コンピューターのサポートに必要なその他の PKI 証明書の詳細については、「[System Center Configuration Manager での PKI 証明書の要件](../../../core/plan-design/network/pki-certificate-requirements.md)」をご覧ください。  

Mac クライアントは、クライアントを管理する Configuration Manager サイトに自動的に割り当てられます。 Mac クライアントは、通信がイントラネットに制限されている場合でも、インターネット専用クライアントとしてインストールされます。 割り当てられているサイトのサイト システムの役割 (管理ポイントおよび配布ポイント) がインターネットからのクライアント接続を許可するように構成されている場合に、それらのサイト システムと通信します。 Mac コンピューターは、割り当てられたサイト以外のサイト システムの役割と通信しません。  

> [!IMPORTANT]  
>  Configuration Manager の Mac クライアントを使用して、[データベース レプリカ](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)を使用するように構成されている管理ポイントに接続することはできません。  


## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Web サーバー証明書をサイト システム サーバーに展開する  
これらのサイト システムに証明書がない場合は、次のサイト システムの役割があるコンピューターに Web サーバー証明書を展開します。  

-   管理ポイント  

-   配布ポイント  

-   登録ポイント  

-   登録プロキシ ポイント  

Web サーバー証明書には、サイト システム プロパティで指定されるインターネット FQDN が含まれていなければなりません。 サーバーはインターネットからアクセスできない場合でも Mac コンピューターをサポートできます。 インターネットベースのクライアント管理が不要な場合、インターネット FQDN にイントラネット FQDN 値を指定できます。  

管理ポイント、配布ポイント、および登録プロキシ ポイントの Web サーバー証明書に、サイト システムのインターネット FQDN 値を指定します。 

この Web サーバー証明書を作成してインストールする展開の例については、「[IIS を実行するサイト システム用の Web サーバー証明書の展開](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012)」をご覧ください。  


## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>クライアント認証証明書をサイト システム サーバーに展開する  
 これらのサイト システムに証明書がない場合は、クライアント認証証明書を、次のサイト システムの役割をホストするコンピューターに展開します。  

-   管理ポイント  

-   配布ポイント  

 管理ポイントのクライアント証明書を作成してインストールする展開の例については、「[Windows コンピューター用のクライアント証明書の展開](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012)」をご覧ください。  

 配布ポイントのクライアント証明書を作成してインストールする展開の例については、「[配布ポイント用のクライアント証明書の展開](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012)」をご覧ください。  

>[!IMPORTANT]
>  Mac OS Sierra を実行しているデバイスにクライアントを展開するには、管理ポイント証明書のサブジェクト名を正しく構成する必要があります。たとえば、管理ポイント サーバーの FQDN を指定します。

## <a name="prepare-the-client-certificate-template-for-macs"></a>Mac 用のクライアント証明書テンプレートを準備する  

 証明書テンプレートには、Mac コンピューターに証明書を登録するユーザー アカウントに対する **読み取り** と **登録** の権限が必要です。  

 「[Mac コンピューター用のクライアント証明書の展開](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1)」をご覧ください。  

## <a name="configure-the-management-point-and-distribution-point"></a>管理ポイントおよび配布ポイントを構成する  
 次のオプションを指定して、管理ポイントを構成します。  

-   HTTPS  

-   インターネットからのクライアント接続を許可する。 この構成値は、Mac コンピューターの管理に必要です。 ただし、インターネットからサイト システム サーバーにアクセスする必要があるということではありません。  

-   モバイル デバイスおよび Mac コンピューターでこの管理ポイントを使用できるようにする  

 クライアントのインストールに配布ポイントは必要ありませんが、クライアントをインストールした後で、これらのコンピューターにソフトウェアを展開する場合は、インターネットからのクライアント接続を許可するように配布ポイントを構成する必要があります。  

 
### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>管理ポイントと配布ポイントで Mac のサポートを構成するには  

この手順を開始する前に、管理ポイントおよび配布ポイントを実行するサイト システム サーバーがインターネット FQDN を指定して構成されていることを確認してください。 このようなサーバーがインターネットベースのクライアント管理をサポートしない場合、インターネット FQDN 値としてイントラネット FQDN を指定できます。 

これらのサイト システムの役割はプライマリ サイト内にある必要があります。  


1.  Configuration Manager コンソールで、**[管理]** > **[サイトの構成]** > **[サーバーとサイト システムの役割]** の順に選択し、適切なサイト システムの役割があるサーバーを選択します。  

3.  詳細ウィンドウで、**[管理ポイント]** を右クリックし、**[役割のプロパティ]** を選択して、**[管理ポイントのプロパティ]** ダイアログ ボックスで次のオプションを構成します。  

    1.  **[HTTPS]** を選択します。  

    2.  **[インターネットのみのクライアント接続を許可する]** または **[イントラネットとインターネット両方のクライアント接続を許可する]** を選択します。 これらのオプションには、インターネットまたはイントラネット FQDN が必要です。  

    3.  **[モバイル デバイスおよび Mac コンピューターでこの管理ポイントを使用できるようにする]** を選択します。  

4.  詳細ウィンドウで、**[配布ポイント]** を右クリックし、**[役割のプロパティ]** をクリックして、**[配布ポイントのプロパティ]** ダイアログ ボックスで次のオプションを構成します。  

    -   **[HTTPS]** を選択します。  

    -   **[インターネットのみのクライアント接続を許可する]** または **[イントラネットとインターネット両方のクライアント接続を許可する]** を選択します。 これらのオプションには、インターネットまたはイントラネット FQDN が必要です。  

    -   **[証明書をインポートする]** を選択し、エクスポートされているクライアント配布ポイント証明書ファイルを参照して、パスワードを指定します。  

5.  Mac で使用するプライマリ サイトのすべての管理ポイントと配布ポイントについて、手順 2 ～ 4 を繰り返します。  

## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>登録プロキシ ポイントおよび登録ポイントを構成する  
 これらのサイト システムの役割は同じサイトにインストールする必要がありますが、同じサイト システム サーバーや同じ Active Directory フォレストにインストールする必要はありません。  

 サイト システムの役割の配置と考慮事項について詳しくは、「[System Center Configuration Manager のサイト システム サーバーとサイト システムの役割の計画](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)」の「[サイト システムの役割](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles)」をご覧ください。  

 これらの手順では、サイト システム サーバーで Mac コンピューターのサポートを構成します。   

-   [新しいサイト システム サーバー](#new-site-system-server)  

-   [既存のサイト システム サーバー](#existing-site-system-server)  

###  <a name="new-site-system-server"></a>(新しいサイト システム サーバーの場合)  

1.  Configuration Manager コンソールで、**[管理]** >  **[サイトの構成]** > **[サーバーとサイト システムの役割]** の順に選択します。  

3.  **[ホーム]** タブの **[作成]** グループで、**[サイト システム サーバーの作成]** を選択します。  

4.  **[全般]** ページで、サイト システムの全般設定を指定します。  インターネット FQDN に値が指定されていることを確認します。 サーバーにインターネットからアクセスできない場合は、イントラネット FQDN を使用します。  

5.  **[システムの役割の選択]** ページの利用可能な役割の一覧で、**[登録プロキシ ポイント]** および **[登録ポイント]** を選択します。  

6.  **[登録プロキシ ポイント]** ページで、設定を確認し、必要な変更を加えます。  

7.  **[登録ポイントの設定]** ページで、設定を確認し、必要な変更を加えます。 その後、ウィザードを完了します。  

### <a name="existing-site-system-server"></a>既存のサイト システム サーバー  

1.  Configuration Manager コンソールで、**[管理]** >  **[サイトの構成]** > **[サーバーとサイト システムの役割]** の順に選択し、Mac のサポートに使用するサーバーを選択します。  

3.  **[ホーム]** タブの **[作成]** グループで、**[サイト システムの役割の追加]** を選択します。  

4.  **[全般]** ページで、サイト システムの全般設定を指定し、 **[次へ]**をクリックします。 インターネット FQDN に値が指定されていることを確認します。 サーバーにインターネットからアクセスできない場合は、イントラネット FQDN を使用します。   

5.  **[システムの役割の選択]** ページの利用可能な役割の一覧で、**[登録プロキシ ポイント]** および **[登録ポイント]** を選択します。  

6.  **[登録プロキシ ポイント]** ページで、設定を確認し、必要な変更を加えます。  

7.  **[登録ポイントの設定]** ページで、設定を確認し、必要な変更を加えます。 その後、ウィザードを完了します。  

## <a name="install-the-reporting-services-point"></a>レポート サービス ポイントをインストールする  
 Mac のレポートを実行する場合は、[レポート サービス ポイントをインストール](../../../core/servers/manage/configuring-reporting.md)します。  

### <a name="next-steps"></a>次のステップ

[Configuration Manager クライアントを Mac コンピューターに展開する](/sccm/core/clients/deploy/deploy-clients-to-macs)。  
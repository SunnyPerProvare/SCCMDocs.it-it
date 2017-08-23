---
title: "サイト システムの役割オプション | Microsoft Docs"
description: "この記事では、必ずしも説明の必要がないとは言えない、Configuration Manager サイト システム役割の詳細を示します。"
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b4db5d86cc0ed020ed176feb2e8f1f9dc51a2280
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="configuration-options-for-site-system-roles-for-system-center-configuration-manager"></a>System Center Configuration Manager のサイト システム役割の構成オプション

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のサイト システム役割のほとんどの構成オプションについては、説明の必要がないか、構成時にウィザードかダイアログ ボックスで説明されます。 以下のセクションでは、追加情報を必要とする設定があるサイト システムの役割について説明します。  

##  <a name="BKMK_ApplicationCatalog_Website"></a> アプリケーション カタログ Web サイト ポイント  
 アプリケーション カタログのアプリケーション カタログ Web サイト ポイントの設定方法については、「[System Center Configuration Manager のアプリケーション管理の計画と構成](../../../../apps/plan-design/plan-for-and-configure-application-management.md)」を参照してください。  

 **クライアント接続**  

 セキュリティを高めた接続設定を使用し、クライアントがインターネットから接続してきているかどうかをチェックするには、**[HTTPS]** を選択します。 このオプションでは、クライアントに対してサーバーを認証し、Secure Socket Layer (SSL) を介してデータを暗号化するために、PKI 証明書がサーバー上にあることが必要とされます。 証明書の要件の詳細については、「[System Center Configuration Manager での PKI 証明書の要件](../../../../core/plan-design/network/pki-certificate-requirements.md)」をご覧ください。  

 サーバー証明書の展開例と、それをインターネット インフォメーション サービス (IIS) で構成する方法については、「[System Center Configuration Manager PKI 証明書の展開手順の例: Windows Server 2008 証明機関](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)」の「*IIS を実行するサイト システム用の Web サーバー証明書の展開*」セクションを参照してください。  

 **アプリケーション カタログ Web サイトを信頼済みサイト ゾーンに追加する**  

 メッセージに既定のクライアント設定の値が表示され、**[Add Application Catalog website to Internet Explorer trusted sites zone (アプリケーション カタログ Web サイトを、Internet Explorer の信頼済みサイト ゾーンに追加する)]** クライアント設定が現在 **[True]** と **[False]** のどちらに設定されているかが示されます。 カスタム クライアント設定を使用してこの設定を構成した場合は、この値を自分で確認する必要があります。  

 このサイト システムが完全修飾ドメイン名 (FQDN) 用に設定されていて、Web サイトが Internet Explorer の信頼済みサイト ゾーンに追加されていない場合は、ユーザーがアプリケーション カタログに接続する際に資格情報を入力するようにプロンプトが表示されます。  

 **組織名**  

 アプリケーション カタログのユーザーに表示される名称を入力します。 ユーザーがこの Web サイトを信頼されるソースとして認識する際に、この組織情報が役立ちます。  

##  <a name="BKMK_ApplicationCatalog_WebService"></a> アプリケーション カタログ Web サービス ポイント  
 アプリケーション カタログのアプリケーション カタログ Web サービス ポイントの設定方法については、「[System Center Configuration Manager のアプリケーション管理の計画と構成](../../../../apps/plan-design/plan-for-and-configure-application-management.md)」を参照してください。  

 **HTTPS**  

 アプリケーション カタログ Web サイト ポイントをこのアプリケーション カタログ Web サービス ポイントに対して認証するには、[HTTPS] を選択します。 ****  このオプションでは、サーバーを認証し、SSL を介してデータを暗号化するために、アプリケーション カタログ Web サイト ポイントを実行するサーバー上に PKI 証明書があることが必要とされます。 証明書の要件の詳細については、「[System Center Configuration Manager での PKI 証明書の要件](../../../../core/plan-design/network/pki-certificate-requirements.md)」をご覧ください。  

 サーバー証明書の展開例と、それを IIS で構成する方法については、「[System Center Configuration Manager PKI 証明書の展開手順の例: Windows Server 2008 証明機関](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)」の「*IIS を実行するサイト システム用の Web サーバー証明書の展開*」セクションを参照してください。  

##  <a name="BKMK_CertificateRegistrationPoint"></a> 証明書登録ポイント  
 証明書登録ポイントの設定方法の詳細については、「[証明書プロファイルの概要](/sccm/protect/deploy-use/introduction-to-certificate-profiles)」を参照してください。  

##  <a name="BKMK_Distribution_Point"></a> 配布ポイント  
 コンテンツ展開の配布ポイントの構成方法については、「[Manage content and content infrastructure for System Center Configuration Manager](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理)」を参照してください。  

 PXE 展開の配布ポイントの設定方法については、「[System Center Configuration Manager で PXE を使用してネットワーク経由で Windows を展開する](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md)」を参照してください。  

 マルチキャスト展開の配布ポイントの設定方法については、「[System Center Configuration Manager でマルチキャストを使用してネットワーク経由で Windows を展開する](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md)」を参照してください。  

 **Configuration Manager で必要な場合は IIS をインストールして構成する**  
 IIS がまだインストールされていない場合に、Configuration Manager で自動的に IIS をインストールして設定するには、このオプションを選択します。 IIS はすべての配布ポイントにインストールする必要があり、ウィザードを続行するにはこの設定を選択する必要があります。  

 **サイト システムのインストール アカウント**  
 サイト サーバーにインストールされている配布ポイントでは、サイト システムのインストール アカウントとしての使用がサポートされているのは、サイト サーバーのコンピューター アカウントだけです。  

 **自己署名入り証明書を作成するか、PKI クライアント証明書をインポートする**  
 この証明書には、次の 2 つの目的があります。  

1.  配布ポイントがステータス メッセージを管理ポイントに送信する前に、管理ポイントから認証を受けるようにします。  

2.  **[クライアントの PXE サポートを有効にする]** がオンになっていると、オペレーティング システムの展開中に管理ポイントに接続できるように、PXE ブートを実行するコンピューターに証明書が送信されます。  

サイトのすべての管理ポイントが HTTP 用に設定されている場合は、自己署名証明書を作成します。 管理ポイントが HTTPS 用に設定されている場合は、PKI クライアント証明書をインポートします。  

証明書をインポートするには、次の Configuration Manager の要件を満たす PKI 証明書を含む公開キー暗号化標準 #12 (PKCS #12) ファイルを見つけます。  

-   使用目的にクライアント認証が含まれている。  

-   秘密キーがエクスポートできるように設定されている。  

証明書のサブジェクトやサブジェクトの別名 (SAN) には、特定の要件はありません。複数の配布ポイントで同じ証明書を使用することができます。  

証明書の要件の詳細については、「[System Center Configuration Manager での PKI 証明書の要件](../../../../core/plan-design/network/pki-certificate-requirements.md)」をご覧ください。 この証明書の展開の例については、「[System Center Configuration Manager PKI 証明書の展開手順の例: Windows Server 2008 証明機関](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)」の「*配布ポイント用のクライアント証明書の展開*」セクションを参照してください。  

**事前設定されたコンテンツ用にこの配布ポイントを有効にする**  
事前設定されたコンテンツ用にこの配布ポイントを有効にするには、このチェック ボックスをオンにします。 このチェック ボックスがオンの場合、コンテンツの配布時の動作を設定できます。 配布ポイントで常にコンテンツを事前設定するか、パッケージの初期コンテンツを事前設定するかを選択できますが、コンテンツに更新がある場合には標準のコンテンツ配布プロセスを使用するか、パッケージ内のコンテンツに対して常に標準コンテンツ配布プロセスを使用するようにします。  

**境界グループ**  
 境界グループを配布ポイントに関連付けることができます。 コンテンツを展開するときに、クライアントがコンテンツ ソースの場所として配布ポイントを使用するには、クライアントは、その配布ポイントに関連付けられた境界グループ内になければなりません。
 - **バージョン 1610 より前では**、**[代替のコンテンツ ソースの場所の使用を許可する]** チェック ボックスをオンにすると、他に利用できる代替ポイントがない場合に、この境界グループ外のクライアントのフォールバックが許可され、配布ポイントをコンテンツ ソースの場所として使用できるようになります。
 - **バージョン 1610 以降**、**[代替のコンテンツ ソースの場所の使用を許可する]** は構成できません。  代わりに、境界グループ間の関係を設定してください。有効なコンテンツ ソースの場所を追加の境界グループからクライアントが検索できるようになるタイミングが、その関係によってチェックされるようにします。

##  <a name="BKMK_Enrollment_Point"></a> 登録ポイント  
登録ポイントは、Mac コンピューターをインストールし、オンプレミスのモバイル デバイス管理で管理するデバイスを登録するために使用します。 詳細については、次をご覧ください。  

-   [System Center Configuration Manager で Mac にクライアントを展開する方法](../../../../core/clients/deploy/deploy-clients-to-macs.md)  

-   [System Center Configuration Manager でのオンプレミス モバイル デバイス管理の対象となるデバイスをユーザーが登録する方法](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

**許可される接続**  
 HTTPS 設定が自動的に選択されます。HTTPS 設定では、登録プロキシ ポイントと帯域外サービス ポイントに対してサーバーを認証し、SSL を介してデータを暗号化するために、サーバー上に PKI 証明書があることが必要とされます。 証明書の要件の詳細については、「[System Center Configuration Manager での PKI 証明書の要件](../../../../core/plan-design/network/pki-certificate-requirements.md)」をご覧ください。  

 サーバー証明書の展開例と、それを IIS で構成する方法については、「[System Center Configuration Manager PKI 証明書の展開手順の例: Windows Server 2008 証明機関](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)」の「*IIS を実行するサイト システム用の Web サーバー証明書の展開*」セクションを参照してください。  

##  <a name="BKMK_Enrollment_Proxy_Point"></a> 登録プロキシ ポイント  
モバイル デバイスの登録プロキシ ポイントの構成方法について詳しくは、「[System Center Configuration Manager でのオンプレミス モバイル デバイス管理の対象となるデバイスをユーザーが登録する方法](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)」をご覧ください。  

**クライアント接続**  
 HTTPS 設定が自動的に選択されます。HTTPS 設定では、Configuration Manager で登録されているモバイル デバイスと Mac コンピューターに対してサーバーを認証し、SSL (Secure Sockets Layer) を介してデータを暗号化するために、サーバー上に PKI 証明書がある必要があります。 証明書の要件の詳細については、「[System Center Configuration Manager での PKI 証明書の要件](../../../../core/plan-design/network/pki-certificate-requirements.md)」をご覧ください。  

 サーバー証明書の展開例と、それを IIS で構成する方法については、「[System Center Configuration Manager PKI 証明書の展開手順の例: Windows Server 2008 証明機関](/sccm/core/plan-design/network/example-deployment-of-pki-certificates)」の「*IIS を実行するサイト システム用の Web サーバー証明書の展開*」セクションを参照してください。  

##  <a name="BKMK_Fallback_Status_Point"></a> フォールバック ステータス ポイント  
**状態メッセージの数** と **調整間隔 (秒)**  
これらのオプションの既定の設定 (状態メッセージの数 10,000、調整間隔 3,600 秒) は、ほとんどの状況に十分に対応できますが、次の両方の条件に一致する場合には、設定の変更が必要になることがあります。  

-   フォールバック ステータス ポイントがイントラネットからのみ接続を受け入れる。  

-   多数のコンピューターを対象としたクライアント展開のロールアウト中に、フォールバック ステータス ポイントを使用する。  

この場合は、状態メッセージの連続したストリームのために状態メッセージのバックログが生成され、サイト サーバーの CPU (中央処理装置) 使用率が長時間高くなることがあります。 さらに、Configuration Manager コンソールとクライアント展開レポートに、クライアント展開の最新情報が表示されない場合もあります。  

これらのフォールバック ステータス ポイント設定は、クライアント展開中に生成される状態メッセージ用に設定するように設計されています。 これらの設定は、インターネット上のクライアントがインターネットベースの管理ポイントに接続できないなどの、クライアントの通信問題用に設定するようには設計されていません。 フォールバック ステータス ポイントは、クライアント展開中に生成された状態メッセージだけに設定を適用することができないため、フォールバック ステータス ポイントがインターネットからの接続を受け入れる場合には、これらの設定は構成しないでください。  

System Center 2012 Configuration Manager クライアントを正常にインストールする各コンピューターは、次の 4 つの状態メッセージをフォールバック ステータス ポイントに送信します。  

-   クライアントの展開が開始されました  

-   クライアントの展開に成功しました  

-   クライアントの割り当てが開始されました  

-   クライアントの割り当てに成功しました  

インストールできないコンピューター、または Configuration Manager クライアントを割り当てることができないコンピューターは、追加の状態メッセージを送信します。  

たとえば、Configuration Manager クライアントを 20,000 台のコンピューターに展開する場合、フォールバック ステータス ポイントへの状態メッセージが 80,000 個送信されるとします。 既定のスロットル構成では、3,600 秒 (1 時間) ごとに 10,000 の状態メッセージをフォールバック ステータス ポイントに送信できるため、状態メッセージはフォールバック ステータス ポイント上でバックログされる可能性があります。 また、フォールバック ステータス ポイントとサイト サーバー間の利用可能なネットワーク帯域幅と、サイト サーバーが大量の状態メッセージを扱う処理能力も考慮する必要があります。  

このような問題を防止するため、状態メッセージの数を増やして、調整間隔を短くすることを検討してください。  

次の状態のいずれかが該当する場合は、フォールバック ステータス ポイントの調整値を再設定します。  

-   現在のスロットル値が、フォールバック ステータス ポイントからの状態メッセージの処理に必要な値より大きいことが計算される場合。  

-   現在の調整設定では、サイト サーバーの CPU 負荷が高くなる場合。  

フォールバック ステータス ポイントの調整設定を変更する場合は、変更により生じる結果について理解していることが条件となります。 たとえば、調整設定を高くすると、サイト サーバーの CPU 負荷が高くなり、すべてのサイト操作の速度が遅くなります。  

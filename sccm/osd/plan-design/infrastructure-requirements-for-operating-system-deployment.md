---
title: "オペレーティング システムの展開のインフラストラクチャ要件 | Microsoft Docs"
description: "オペレーティング システム展開に System Center 2012 Configuration Manager を利用する前に、外部依存関係と製品依存関係を理解しておきます。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 1dc74219-7ff5-4e3b-b4f6-5aad663bb75b
caps.latest.revision: "24"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 167e639cdb9995fd743787cc9fbf364ec70f6ed9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="infrastructure-requirements-for-operating-system-deployment-in-system-center-configuration-manager"></a>System Center Configuration Manager のオペレーティング システムの展開のインフラストラクチャ要件

*適用対象: System Center Configuration Manager (Current Branch)*

System Center 2012 Configuration Manager のオペレーティング システム展開には、外部依存関係と製品内部依存関係があります。 オペレーティング システムの展開を準備するには、次のセクションを使用します。  

##  <a name="BKMK_ExternalDependencies"></a> Configuration Manager 外部の依存関係  
 Configuration Manager でオペレーティング システムを展開するのに必要な外部ツール、インストール キット、オペレーティング システムに関する情報を以下に示します。  

### <a name="windows-adk-for-windows-10"></a>Windows 10 用 Windows ADK  
 Windows ADK は、Windows オペレーティング システムの構成と展開をサポートするツールとドキュメントのセットです。 Configuration Manager では、Windows インストールの自動化、Windows イメージのキャプチャ、ユーザー プロファイルとデータの移行などを自動化するために Windows ADK を使用しています。  

 階層の最上位サイトのサイト サーバーと、階層内の各プライマリ サイトのサイト サーバー、サイト システム サーバーの SMS プロバイダーに、Windows ADK の次の機能をインストールする必要があります。  

-   ユーザー状態移行ツール (USMT) <sup>1</sup>  

-   Windows 展開ツール  

-   Windows プレインストール環境 (Windows PE)

さまざまなバージョンの Configuration Manager で使用できる Windows 10 ADK のバージョン一覧については、[クライアントとしての Windows 10 のサポート](https://docs.microsoft.com/en-us/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk)に関するページを参照してください。

 <sup>1</sup> USMT は、SMS プロバイダー サイト システム サーバーでは必要ありません。  

> [!NOTE]  
>  Configuration Manager サイトをインストールする前に、中央管理サイトまたはプライマリ サイト サーバーをホストする各コンピューターに、Windows ADK を手動でインストールする必要があります。  

 詳細については、次をご覧ください。  

-   [IT 担当者向け Windows ADK for Windows 10 シナリオ](https://technet.microsoft.com/library/mt280162\(v=vs.85\).aspx)  

-   [Windows ADK for Windows 10 をダウンロードする](https://msdn.microsoft.com/windows/hardware/dn913721.aspx#adkwin10)  

-   [Windows 10 のサポート](/sccm/core/plan-design/configs/support-for-windows-10)  


### <a name="user-state-migration-tool-usmt"></a>ユーザー状態移行ツール (USMT)  
 Configuration Manager では、USMT 10 ソース ファイルを含む USMT パッケージを使用して、オペレーティング システムの展開の一部として、ユーザーの状態をキャプチャして復元します。 最上位サイトに Configuration Manager をセットアップすると、USMT パッケージが自動的に作成されます。 USMT 10 では、Windows 7、Windows 8、Windows 8.1 および Windows 10 からユーザー状態をキャプチャできます。 USMT 10 は、Windows 10 用 Windows アセスメント & デプロイメント キット (Windows ADK) に含まれています。  

 詳細については、次をご覧ください。  

-   [USMT 10 の一般的な移行シナリオ](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx)  

-   [ユーザー状態の管理](../get-started/manage-user-state.md)  

### <a name="windows-pe"></a>Windows PE  
 Windows PE は、コンピューターを起動するブート イメージに使用されます。 それは、Windows オペレーティング システムのプレインストールや展開の最中に使用される、サービスが制限された Windows オペレーティング システムです。 Configuration Manager のバージョン、サポートされている Windows ADK のバージョン、Configuration Manager コンソールからカスタマイズできるブート イメージのベースとなる Windows PE バージョン、DISM でカスタマイズした後で Configuration Manager の指定バージョンに追加できるブート イメージのベースとなる Windows PE バージョンは、次のとおりです。  

#### <a name="configuration-manager-version-1511"></a>Configuration Manager バージョン 1511  
 サポートされている Windows ADK のバージョン、Configuration Manager コンソールからカスタマイズできるブート イメージのベースとなる Windows PE バージョン、DISM でカスタマイズした後で Configuration Manager に追加できるブート イメージのベースとなる Windows PE バージョンは次のとおりです。  

-   **Windows ADK バージョン**  

     Windows 10 用 Windows ADK  

-   **Configuration Manager コンソールでカスタマイズできる Windows PE ブート イメージのバージョン**  

     Windows PE 10  

-   **Configuration Manager コンソールでカスタマイズできない Windows PE ブート イメージのバージョン**  

     Windows PE 3.1<sup>1</sup> および Windows PE 5  

     <sup>1</sup> Windows PE 3.1 のブートイメージしか Configuration Manager に追加することができません。 Windows AIK for Windows 7 (Windows PE 3 の構築用) を Windows AIK Supplement for Windows 7 SP1 (Windows PE 3.1 の構築用) にアップグレードしてください。 Windows AIK Supplement for Windows 7 SP1 は、 [Microsoft ダウンロード センター](http://www.microsoft.com/download/details.aspx?id=5188)からダウンロードできます。  

     たとえば、Configuration Manager を使っている場合は、Windows 10 用 Windows ADK (Windows PE 10 に基づく) で構築したブート イメージを Configuration Manager コンソールでカスタマイズできます。 一方、Windows PE 5 のブート イメージはサポートされていますが、このブート イメージをカスタマイズするには、別のコンピューターにある Windows 8 用 Windows ADK に付属している DISM を使わなければなりません。 その後、ブート イメージを Configuration Manager コンソールに追加できます。 ブート イメージのカスタマイズ (オプションのコンポーネントとドライバーの追加)、ブート イメージのコマンド サポートの有効化、Configuration Manager コンソールへのブート イメージの追加、ブート イメージによる配布ポイントの更新の手順の詳細については、「[ブート イメージのカスタマイズ](../get-started/customize-boot-images.md)」を参照してください。 ブート イメージの詳細については、「[ブート イメージの管理](../get-started/manage-boot-images.md)」を参照してください。  

### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  
次の WSUS 4.0 修正プログラムをインストールする必要があります。
  - [Hotfix 3095113](https://support.microsoft.com/kb/3095113) を適用した WSUS 4.0 は Windows 10 サービスに必要であり、ソフトウェアの更新インフラストラクチャを使用して、Windows 10 の機能アップグレードを取得します。 WSUS 3.2 がある場合は、Windows 10 をアップグレードするためのタスク シーケンスを使用する必要があります。 詳細については、「[サービスとしての Windows の管理](../deploy-use/manage-windows-as-a-service.md)」を参照してください。  
  - [Hotfix 3159706](https://support.microsoft.com/kb/3159706) は、Windows 10 サービスを利用してコンピューターを Windows 10 Anniversary Update とその後続バージョンにアップグレードするために必要です。 この修正プログラムをインストールするには、サポート記事で紹介されている手順を手動で実行する必要があります。 詳細については、「[サービスとしての Windows の管理](../deploy-use/manage-windows-as-a-service.md)」を参照してください。


### <a name="internet-information-services-iis-on-the-site-system-servers"></a>サイト システム サーバー上のインターネット インフォメーション サービス (IIS)  
 IIS は、配布ポイント、状態移行ポイント、および管理ポイントに必要です。 この要件に関する詳細については、「[サイトとサイト システムの前提条件](../../core/plan-design/configs/site-and-site-system-prerequisites.md)」を参照してください。  

### <a name="windows-deployment-services-wds"></a>Windows 展開サービス (WDS)  
 WDS は、PXE 展開の場合、展開の帯域幅を最適化するのにマルチキャストを使用する場合と画像のオフライン サービスに必要です。 プロバイダーがリモート サーバーにインストールされている場合は、サイト サーバーとリモート プロバイダーに WDS をインストールする必要があります。 詳細については、このトピックの「 [Windows 展開サービス](#BKMK_WDS) 」をご覧ください。  

### <a name="dynamic-host-configuration-protocol-dhcp"></a>動的ホスト構成プロトコル (DHCP)  
 PXE の展開には DHCP が必要です。 PXE を使用してオペレーティング システムを展開するには、アクティブなホストを持つ、機能している DHCP サーバーを用意する必要があります。 PXE 展開に関する詳細については、「[PXE を使用したネットワーク経由での Windows の展開](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md)」を参照してください。  

### <a name="supported-operating-systems-and-hard-disk-configurations"></a>サポートされるオペレーティング システムおよびハード ディスクの構成  
 オペレーティング システムを展開する場合に Configuration Manager がサポートするオペレーティング システムのバージョンとハード ディスクの構成についての詳細は、「[サポートされているオペレーティング システム](#BKMK_SupportedOS)」および「[サポートされているディスク構成](#BKMK_SupportedDiskConfig)」を参照してください。  

### <a name="windows-device-drivers"></a>Windows デバイス ドライバー  
 Windows デバイス ドライバーは、対象コンピューターにオペレーティング システムをインストールする場合と、ブート イメージを使って Windows PE を実行する場合に使用できます。 デバイス ドライバーの詳細については、「[ドライバーの管理](../get-started/manage-drivers.md)」を参照してください。  

##  <a name="BKMK_InternalDependencies"></a> Configuration Manager の依存関係  
 Configuration Manager オペレーティング システムの展開の前提条件について、以下に示します。  

### <a name="operating-system-image"></a>オペレーティング システム イメージ  
 Configuration Manager のオペレーティング システム イメージは、Windows Imaging (WIM) ファイル形式で格納され、コンピューターのオペレーティング システムを正常にインストールおよび構成するのに必要な参照ファイルおよびフォルダーのコレクションを圧縮したものです。 詳細については、「[オペレーティング システム イメージの管理](../get-started/manage-operating-system-images.md)」を参照してください。  

### <a name="driver-catalog"></a>ドライバー カタログ  
 デバイス ドライバーを展開するには、まずデバイス ドライバーをインポートしてこれを有効化し、Configuration Manager クライアントがアクセスできる配布ポイントで利用可能にする必要があります。 ドライバー カタログの詳細については、「[ドライバーの管理](../get-started/manage-drivers.md)」を参照してください。  

### <a name="management-point"></a>管理ポイント  
 管理ポイントは、クライアント コンピューターと Configuration Manager サイト間で情報を転送します。 クライアントは、オペレーティング システムの展開を完了するのに必要なあらゆるタスク シーケンスを実行するのに管理ポイントを使用します。  

 タスク シーケンスの詳細については、「[タスクの自動化計画に関する考慮事項](planning-considerations-for-automating-tasks.md)」を参照してください。  

### <a name="distribution-point"></a>配布ポイント  
 配布ポイントは、オペレーティング システムのイメージや、デバイス ドライバーのパッケージなど、オペレーティング システムを展開するのに使用されるデータを格納するために、ほとんどの展開によって使用されます。 タスク シーケンスは通常、オペレーティング システムを展開するために配布ポイントからデータを取得します。  

 配布ポイントをインストールして、コンテンツを管理する方法の詳細については、「[コンテンツとコンテンツ インフラストラクチャの管理](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

### <a name="pxe-enabled-distribution-point"></a>PXE 対応配布ポイント  
 PXE を使った展開を行うには、クライアントからの PXE 要求を受け入れるように配布ポイントを構成する必要があります。 配布ポイントの構成方法の詳細については、「[配布ポイントの構成](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pxe)」をご覧ください。  

### <a name="multicast-enabled-distribution-point"></a>マルチキャスト対応の配布ポイント  
 マルチキャストを使ってオペレーティング システムの展開を最適化するには、配布ポイントがマルチキャストをサポートするように構成する必要があります。 配布ポイントの構成方法の詳細については、「[配布ポイントの構成](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#multicast)」をご覧ください。   

### <a name="state-migration-point"></a>状態移行ポイント  
 並列展開および更新展開用にユーザー状態のデータをキャプチャして復元する場合、別のコンピューターにユーザー状態データを格納するように状態移行ポイントを構成する必要があります。  

 状態移行ポイントを構成する方法の詳細については、「 [状態移行ポイント](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints)」をご覧ください。  

 ユーザー状態をキャプチャして復元方法については、「[ユーザー状態の管理](../get-started/manage-user-state.md)」を参照してください。  

### <a name="service-connection-point"></a>[サービス接続ポイント]  
 Windows 10 Current Branch を展開するために、Windows をサービスとして (WaaS) 使用する場合は、サービス接続ポイントをインストールする必要があります。 詳細については、「[サービスとしての Windows の管理](../deploy-use/manage-windows-as-a-service.md)」を参照してください。  

### <a name="reporting-services-point"></a>レポート サービス ポイント  
 オペレーティング システムの展開に Configuration Manager レポートを使用するには、レポート サービス ポイントをインストールして構成する必要があります。 詳細については、「[レポート](../../core/servers/manage/reporting.md)」を参照してください。  

### <a name="security-permissions-for-operating-system-deployments"></a>オペレーティング システム展開でのセキュリティ アクセス許可  
 **[オペレーティング システム展開マネージャー]** セキュリティ ロールは、変更のできない組み込みのセキュリティ ロールです。 しかし、このセキュリティ ロールをコピーして、変更を加え、変更を新しいカスタム セキュリティ ロールとして保存することができます。 オペレーティング システムの展開に直接適用できる許可を次に示します。  

-   **ブート イメージ パッケージ**: 作成、削除、変更、フォルダーの変更、オブジェクトの移動、読み取り、セキュリティ スコープの設定  

-   **デバイス ドライバー**: 作成、削除、変更、フォルダーの変更、レポートの変更、オブジェクトの移動、読み取り、レポートの実行  

-   **ドライバー パッケージ**: 作成、削除、変更、フォルダーの変更、オブジェクトの移動、読み取り、セキュリティ スコープの設定  

-   **オペレーティング システム イメージ**: 作成、削除、変更、フォルダーの変更、オブジェクトの移動、読み取り、セキュリティ スコープの設定  

-   **オペレーティング システム インストール パッケージ**: 作成、削除、変更、フォルダーの変更、オブジェクトの移動、読み取り、セキュリティ スコープの設定  

-   **タスク シーケンス パッケージ**: 作成、タスク シーケンス メディアの作成、削除、変更、フォルダーの変更、レポートの変更、オブジェクトの移動、読み取り、レポートの実行、セキュリティ スコープの設定  

 カスタム セキュリティ ロールの詳細については、「 [カスタム セキュリティ ロールの作成](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole)」をご覧ください。  

### <a name="security-scopes-for-operating-system-deployments"></a>オペレーティング システム展開のセキュリティ スコープ  
 セキュリティ スコープを使用すると、管理者は、オペレーティング システムとブート イメージ、ドライバー パッケージ、タスク シーケンス パッケージなど、オペレーティング システムの展開で使用される保護可能なオブジェクトにアクセスすることができます。 詳細については、「 [セキュリティ スコープ](../../core/understand/fundamentals-of-role-based-administration.md#bkmk_PlanScope)」をご覧ください。  

##  <a name="BKMK_WDS"></a> Windows 展開サービス  
 Windows 展開サービス (WDS) は、PXE やマルチキャストをサポートするように構成する配布ポイントと同じサーバー上にインストールする必要があります。 WDS は、サーバーのオペレーティング システムに含まれています。 PXE 展開では、PXE ブートを行うサービスは WDS です。 PXE 用に配布ポイントがインストールされ、有効化された場合、Configuration Manager は、WDS PXE ブート機能を使用する WDS にプロバイダーをインストールします。  

> [!NOTE]  
>  サーバーの再起動が必要な場合、WDS のインストールに失敗する場合があります。 

 考慮すべきその他の WDS の構成には、次のようなものがあります。  

-   WDS のサーバーへのインストールには、管理者がローカルの Administrators グループのメンバーであることが必要です。  

-   WDS サーバーが、Active Directory ドメインのメンバーか、Active Directory ドメインのドメイン コントローラーであること。 すべての Windows ドメインおよびフォレストの構成が WDS をサポートしていること。  

-   プロバイダーがリモート サーバーにインストールされている場合は、サイト サーバーとリモート プロバイダーに WDS をインストールする必要があります。  

###  <a name="BKMK_WDSandDHCP"></a> 同じサーバー上に、WDS と DHCP がある場合の考慮事項  
 DHCP を実行するサーバーで配布ポイントを同時にホストする場合は、次の構成の問題を考慮する必要があります。  

-   アクティブなスコープを持つ、機能している DHCP サーバーが必要です。 Windows 展開サービスは PXE を使用しますが、PXE には DHCP サーバーが必要です。  

-   DHCP および Windows 展開サービスはどちらもポート番号 67 を必要とします。 Windows 展開サービスと DHCP を同時にホストする場合、PXE 用に構成した DHCP または配布ポイントを別のサーバーに移動できます。 または、次の手順を使用して、別のポートをリッスンするように Windows 展開サービス サーバーを構成できます。  

    #### <a name="to-configure-the-windows-deployment-services-server-to-listen-on-a-different-port"></a>別のポートをリッスンするように Windows 展開サービス サーバーを構成するには  

    1.  次のレジストリ キーを変更します。  

         **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WDSServer\Providers\WDSPXE**  

    2.  レジストリ値を次の値に設定します。 **UseDHCPPorts = 0**  

    3.  新しい構成を適用するには、サーバーで次のコマンドを実行します。  

         `WDSUTIL /Set-Server /UseDHCPPorts:No /DHCPOption60:Yes`  

-   Windows 展開サービスを実行するには DNS サーバーが必要です。  

-   Windows 展開サービス サーバーで、次の UDP ポートを開く必要があります。  

    -   ポート 67 (DHCP)  

    -   ポート 69 (TFTP)  

    -   ポート 4011 (PXE)  

    > [!NOTE]  
    >  さらに、サーバーで DHCP の承認が必要な場合、サーバーで DHCP クライアント用のポート 68 を開く必要があります。  

##  <a name="BKMK_SupportedOS"></a> サポート対象のオペレーティング システム  
 「[クライアントとデバイスでサポートされるオペレーティング システム](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)」でサポート対象クライアント オペレーティング システムとして示されているすべての Windows オペレーティング システムは、オペレーティング システム展開に対応しています。  

##  <a name="BKMK_SupportedDiskConfig"></a> 対応するディスク構成  
 次の表は、Configuration Manager オペレーティング システムの展開での使用がサポートされている参照コンピューターおよび展開先コンピューターのハード ディスク構成の組み合わせを示します。  

|参照コンピューターのハード ディスク構成|展開先コンピューターのハード ディスク構成|  
|------------------------------------------------|--------------------------------------------------|  
|ベーシック ディスク|ベーシック ディスク|  
|ダイナミック ディスク上のシンプル ボリューム|ダイナミック ディスク上のシンプル ボリューム|  

 Configuration Manager では、シンプル ボリュームで構成されたコンピューターからのオペレーティング システム イメージのキャプチャのみをサポートしています。 次のハード ディスク構成はサポートされません。  

-   スパン ボリューム  

-   ストライプ ボリューム (RAID 0)  

-   ミラー ボリューム (RAID 1)  

-   パリティ ボリューム (RAID 5)  

 次の表は、Configuration Manager のオペレーティング システム展開でサポートされていない参照および展開先コンピューターの追加のハード ディスク構成を示します。  

|参照コンピューターのハード ディスク構成|展開先コンピューターのハード ディスク構成|  
|------------------------------------------------|--------------------------------------------------|  
|ベーシック ディスク|ダイナミック ディスク|  

## <a name="next-steps"></a>次のステップ
[オペレーティング システムの展開の準備](../get-started/prepare-for-operating-system-deployment.md)

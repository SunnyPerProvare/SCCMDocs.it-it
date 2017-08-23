---
title: "サポートされている SQL Server のバージョン | Microsoft ドキュメント"
description: "System Center Configuration Manager サイト データベースをホストするための SQL Server のバージョンおよび構成要件を取得します。"
ms.custom: na
ms.date: 05/10/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
caps.latest.revision: "21"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b35e45b9514297e2f9ce405a3244462ed735f39f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="supported-sql-server-versions-for-system-center-configuration-manager"></a>System Center Configuration Manager のサポートされている SQL Server バージョン

*適用対象: System Center Configuration Manager (Current Branch)*

それぞれの System Center Configuration Manager サイトには、サイト データベースをホストするためにサポートされている SQL Server バージョンおよび構成が必要です。  

##  <a name="bkmk_Instances"></a> SQL Server インスタンスと場所  
 **中央管理サイトとプライマリ サイト**  
サイト データベースは SQL Server のフル インストールを使用する必要があります。  

 SQL Server は次の場所に配置できます。  

-   サイト サーバー コンピューター。  
-   サイト サーバーから離れたコンピューター。  

次のインスタンスがサポートされています。  

-   SQL Server の既定のインスタンスまたは名前付きインスタンス。  
-   複数インスタンス構成。  
-   SQL Server クラスター。 「[SQL Server クラスターを使用したサイト データベースのホスティング](../../../core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md)」を参照してください。
-   SQL Server AlwaysOn 可用性グループ。 このオプションでは、Configuration Manager 1602 以降のバージョンが必要です。 詳細については、「[System Center Configuration Manager 用の高可用性サイト データベースの SQL Server AlwaysOn](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)」を参照してください。


 **セカンダリ サイト:**  
 サイト データベースは SQL Server または SQL Server Express のフル インストールの既定のインスタンスを使用できます。  

 SQL Server はサイト サーバー コンピューターに配置する必要があります。  

 **サポートの制限事項**   
 次の構成はサポートされていません。
 -   ネットワーク負荷分散 (NLB) クラスター構成の SQL Server クラスター
 -   クラスター共有ボリューム (CSV) 上の SQL Server クラスター
 -   SQL Server のデータベース ミラーリング テクノロジとピア ツー ピア レプリケーション

SQL Server のトランザクション レプリケーションは、[データベース レプリカ](https://technet.microsoft.com/library/mt608546.aspx)を使用するように構成されている管理ポイントにオブジェクトをレプリケートする場合にのみサポートされます。  

##  <a name="bkmk_SQLVersions"></a> サポートされている SQL Server のバージョン  
 複数のサイトを含む階層では、次の条件を満たす場合、それぞれのサイトが異なるバージョンの SQL Server を使用してサイト データベースをホストできます。
 -  Configuration Manager によってサポートされている SQL Server のバージョンを使用していること。
 -  使用する SQL Server のバージョンが、Microsoft によって引き続きサポートされていること。
 -  SQL Server で、SQL Server の 2 つのバージョン間のレプリケーションをサポートしていること。  たとえば、[SQL Server では SQL Server 2008 R2 と SQL Server 2016 間のレプリケーションをサポートしていません](https://docs.microsoft.com/sql/relational-databases/replication/deprecated-features-in-sql-server-replication)。



 特に指定のない限り、次のバージョンの SQL Server はすべてのアクティブ バージョンの System Center Configuration Manager でサポートされます。 新しい SQL Server バージョンまたは Service Pack のサポートが追加されている場合、そのサポートを追加する Configuration Manager バージョンが示されます。 同様に、サポートが推奨されていない場合は、Configuration Manager の影響を受けるバージョンの詳細を確認してください。   

特定の SQL Server Service Pack のサポートには、基本の Service Pack バージョンに戻せない場合を除き、その Service Pack の累積的な更新プログラムが含まれます。 Service Pack のバージョンが示されない場合、サポートは、そのバージョンの Service Pack なしの SQL Server に対するものです。 今後、そのバージョンの Service Pack がリリースされた場合、その新しい Service Pack バージョンがサポートされる前に、別のサポート ステートメントが宣言されます。


> [!IMPORTANT]  
>  中央管理サイトでデータベース用に SQL Server Standard を使用する場合、階層でサポートできるクライアントの合計数が制限されます。 「[サイジングとスケールの数値](../../../core/plan-design/configs/size-and-scale-numbers.md)」をご覧ください。

### <a name="sql-server-2016-sp1-standard-enterprise"></a>SQL Server 2016 SP1: Standard、Enterprise  
次の累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。  

-   中央管理サイト  
-   プライマリ サイト  
-   セカンダリ サイト  

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016: Standard、Enterprise  
次の累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。  

-   中央管理サイト  
-   プライマリ サイト  
-   セカンダリ サイト  


### <a name="sql-server-2014-sp2-standard-enterprise"></a>SQL Server 2014 SP2: Standard、Enterprise  
次の累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。  

-   中央管理サイト  
-   プライマリ サイト  
-   セカンダリ サイト



### <a name="sql-server-2014-sp1-standard-enterprise"></a>SQL Server 2014 SP1: Standard、Enterprise  
 次の累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。  

-   中央管理サイト  
-   プライマリ サイト  
-   セカンダリ サイト


### <a name="sql-server-2012-sp3-standard-enterprise"></a>SQL Server 2012 SP3: Standard、Enterprise  
 次の累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。  

-   中央管理サイト  
-   プライマリ サイト  
-   セカンダリ サイト  

<!-- Support for this service pack version has been dropped by Microsoft    
### SQL Server 2012 SP2: Standard, Enterprise   
 You can use this version of SQL Server with no minimum cumulative update version for the following:  

-   A central administration site  
-   A primary site  
-   A secondary site  
-->

### <a name="sql-server-2008-r2-sp3-standard-enterprise-datacenter"></a>SQL Server 2008 R2 SP3: Standard、Enterprise、Datacenter     
  [バージョン 1702 以降](/sccm/core/plan-design/changes/removed-and-deprecated-features#deprecated-support-for-sql-server-versions-as-a-site-database)では、このバージョンの SQL Server はサポートされていません。  
 1702 より前のバージョンの Configuration Manager を使用している場合、このバージョンの SQL Server は引き続きサポートされます。

使用しているバージョンの Configuration Manager でサポートされている場合は、次の累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。  

-   中央管理サイト  
-   プライマリ サイト
-   セカンダリ サイト



### <a name="sql-server-2016-express-sp1"></a>SQL Server 2016 Express SP1  
次の累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。
-   セカンダリ サイト

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express
次の累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。
-   セカンダリ サイト


### <a name="sql-server-2014-express-sp2"></a>SQL Server 2014 Express SP2   
次の累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。  

-   セカンダリ サイト  


### <a name="sql-server-2014-express-sp1"></a>SQL Server 2014 Express SP1   
 次の累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。  

-   セカンダリ サイト  

### <a name="sql-server-2012-express-sp3"></a>SQL Server 2012 Express SP3  
次の累積的な更新プログラムの最小バージョンなしで、このバージョンの SQL Server を使用できます。  

-   セカンダリ サイト  

<!-- Support for this service pack version has been dropped by Microsoft   
### SQL Server 2012 Express SP2   
 You can use this version of SQL Server with no minimum cumulative update version for the following:  

-   A secondary site  
-->


##  <a name="bkmk_SQLConfig"></a> SQL Server の必須構成  
 サイト データベースに使用する SQL Server (SQL Server Express を含む) のすべてのインストールでの要件は次のとおりです。 Configuration Manager が SQL Server Express をセカンダリ サイト インストールの一部としてインストールするときには、これらの構成は自動的に作成されます。  

 **SQL Server アーキテクチャのバージョン:**  
 Configuration Manager には、サイト データベースをホストするために 64 ビット版の SQL Server が必要です。  

 **データベース照合順序：**  
 各サイトでは、サイトとサイト データベースの両方に使用される SQL Server のインスタンスが、 **SQL_Latin1_General_CP1_CI_AS**の照合順序を使用する必要があります。  

 Configuration Manager は、GB18030 で定義されている中国で使用するための標準を満たすために、この照合順序に対して 2 つの例外をサポートしています。 詳細については、「[System Center Configuration Manager のインターナショナル サポート](../../../core/plan-design/hierarchy/international-support.md)」をご覧ください。  

 **SQL Server の機能：**  
 各サイト サーバーに必要な機能は、 **データベース エンジン サービス** 機能のみです。  

 Configuration Manager データベース レプリケーションは、**SQL Server レプリケーション**機能を必要としません。 ただし、[System Center Configuration Manager の管理ポイントのデータベース レプリカ](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)を使用する場合は、この SQL Server の構成が必要です。  

 **Windows 認証:**  
 Configuration Manager は、データベースへの接続を検証するために、**Windows 認証**を必要とします。  

 **SQL Server インスタンス:**  
 サイトごとに専用の SQL Server のインスタンスを使用する必要があります。 **名前付きインスタンス** か、 **既定のインスタンス**を使用できます。  

 **SQL Server のメモリ：**  
 SQL Server Management Studio を使用して、 **[サーバー メモリ オプション]** で **[最小サーバー メモリ]**設定を指定して、SQL Server のメモリを予約します。 固定量のメモリを設定する方法の詳細については、「 [固定量のメモリを設定する方法 (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759)」を参照してください。  

-   **サイト サーバーと同じコンピューターにインストールされたデータベース サーバーの場合:** SQL Server 用のメモリをアドレス可能なシステム メモリの 50% から 80% に制限します。  

-   **専用データベース サーバー (サイト サーバーからリモート) の場合:** SQL Server 用のメモリをアドレス指定可能なシステム メモリの 80% から 90% に制限します。  

-   **使用中の各 SQL Server インスタンスのバッファー プール用のメモリ予約の場合:**   

    -   中央管理サイト: 最小で 8 ギガバイト (GB) に設定  
    -   プライマリ サイト: 最小で 8 ギガバイト (GB) に設定  
    -   セカンダリ サイト: 最小で 4 ギガバイト (GB) に設定  

**SQL の入れ子になったトリガー**  
 [SQL の入れ子になったトリガー](http://go.microsoft.com/fwlink/?LinkId=528802) は、有効にする必要があります。  

 **SQL Server の CLR 統合**  
  サイト データベースには、SQL Server 共通言語ランタイム (CLR) を有効にする必要があります。 これは、Configuration Manager のインストール時に自動的に有効になります。 CLR の詳細については、「[SQL Server の CLR 統合の概要](https://msdn.microsoft.com/library/ms254498\(v=vs.110\).aspx)」をご覧ください。  

##  <a name="bkmk_optional"></a> SQL Server のオプション構成  
 以下の構成は、SQL Server の完全インストールを使用する各データベースのオプションです。  

 **SQL Server サービス:**  
 SQL Server サービスを、以下のものを使用して実行するように構成できます。  

-   **ドメイン ローカル ユーザー** アカウント:  

    -   これはベスト プラクティスであり、アカウントのサービス プリンシパル名 (SPN) を手動で登録しなければならない場合があります。  

-   SQL Server を実行しているコンピューターの**ローカル システム** アカウント:  

    -   ローカル システム アカウントを使用すると、構成プロセスが簡単になります。  
    -   ローカル システム アカウントを使用すると、Configuration Manager によって自動的に SQL Server サービスの SPN が登録されます。  
    -   SQL Server サービスにローカル システム アカウントを使用することは、SQL Server のベスト プラクティスではないことに注意してください。  

SQL Server を実行するコンピューターが、ローカル システム アカウントを使用して SQL Server サービスを実行していない場合、SQL Server サービスを実行するアカウントの SPN を Active Directory Domain Services で構成する必要があります  (システム アカウントを使用する場合、SPN が自動的に登録されます)。

サイト データベースの SPN については、「[Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md#bkmk_SPN)」 (System Center Configuration Manager インフラストラクチャの変更) トピックの「[Manage the SPN for the site database server](../../../core/servers/manage/modify-your-infrastructure.md)」 (サイト データベース サーバーの SPN の管理) を参照してください。  

SQL Server サービスで使用されるアカウントを変更する方法については、「 [方法: SQL Server のサービス開始アカウントの変更 (SQL Server 構成マネージャー)](http://go.microsoft.com/fwlink/p/?LinkId=237661)」を参照してください。  

**SQL Server Reporting Services:**  
レポートを実行できるようにするレポート サービス ポイントをインストールするには、SQL Server Reporting Services が必要です。  

> [!IMPORTANT]  
> 以前のバージョンから SQL Server をアップグレードした後、「*Report Builder Does Not Exist*」 (レポート ビルダーが存在しません) というエラーが表示されることがあります。    
> このエラーを解決するには、レポート サービス ポイント サイト システムの役割を再インストールする必要があります。

**SQL Server のポート:**  
SQL Server データベース エンジンとの通信、およびサイト間のレプリケーションには、SQL Server の既定ポート構成を使用することも、カスタム ポートを指定することもできます。  

-   **サイト間の通信** には SQL Server Service Broker が使用され、既定ではポート TCP 4022 が使用されます。  
-   SQL Server データベース エンジンとさまざまな Configuration Manager サイト システムの役割の間の**サイト内通信**では、既定でポート TCP 1433 が使用されます。 次のサイト システムの役割は、SQL Server データベースと直接通信します。  

    -   管理ポイント  
    -   SMS プロバイダー コンピューター  
    -   レポート サービス ポイント  
    -   サイト サーバー  

SQL Server を実行しているコンピューターが複数のサイトからデータベースをホストする場合、各データベースは個別の SQL Server インスタンスを使用する必要があります。 さらに、各インスタンスは一意のポート セットを使用するように構成されている必要があります。  

> [!WARNING]  
>  Configuration Manager は、動的ポートをサポートしていません。 SQL Server 名前付きインスタンスの既定動作では、データベース エンジンへの接続に動的ポートが使用されるため、名前付きインスタンスの使用時に、サイト内通信に使用する静的ポートを手動で構成する必要があります。  

SQL Server を実行しているコンピューターのファイアウォールが有効に設定されている場合は、展開で使用されているポートと、SQL Server と通信するコンピューター間のネットワーク上のあらゆる場所にあるポートを許可するように構成してください。  

特定のポートを使用するように SQL Server を構成する方法の例については、SQL Server TechNet ライブラリの「 [特定の TCP ポートで受信待ちするようにサーバーを構成する方法 (SQL Server 構成マネージャー)](http://go.microsoft.com/fwlink/p/?LinkID=226349) 」を参照してください。  

## <a name="upgrade-options-for-sql-server"></a>SQL Server のアップグレード オプション
使用している SQL Server のバージョンをアップグレードする必要がある場合は、次の方法 (簡単な方法から順に示されています) を使用することをお勧めします。
1. [SQL Server をインプレースでアップグレードします](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (推奨)。
2. 新しいコンピューターに新しいバージョンの SQL Server をインストールしてから、Configuration Manager セットアップの[データベースの移動オプションを使用](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration)して、サイト サーバーを新しい SQL Server にポイントします。
3. [バックアップと回復](/sccm/protect/understand/backup-and-recovery)を使用します。

---
title: "レポートの計画 | Microsoft Docs"
description: "インストールの詳細からセキュリティとネットワーク帯域幅まで、Configuration Manager でレポートを計画することが重要です。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ff920c84-d5c8-458c-b67f-bc7219b05690
caps.latest.revision: "6"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 119f501057bf44e483be31db20b88326b3d05ebb
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="planning-for-reporting-in-system-center-configuration-manager"></a>System Center Configuration Manager のレポートの計画

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のレポート機能には、SQL Reporting Services のレポート機能を使用するための一連のツールとリソースが搭載されています。 Configuration Manager のレポートを計画するときは、次のセクションを参考にしてください。  

##  <a name="BKMK_InstallReportingServicesPoint"></a> レポート サービス ポイントのインストール場所を決定する  
 サイトで Configuration Manager レポートを実行するとき、レポートは接続先のサイト データベース内の情報にアクセスできます。 次のセクションを参考に、レポート サービス ポイントのインストール場所と使用するデータ ソースを決定してください。  

> [!NOTE]  
>  サイト システムの計画の詳細については、「[サイト システムの役割を追加する](../deploy/configure/add-site-system-roles.md)」を参照してください。  

###  <a name="BKMK_SupportedSiteServers"></a> サポートされるサイト システム サーバー  
 レポート サービス ポイントは、中央管理サイトとプライマリ サイト、および、階層内の単一サイトとその他のサイトの複数のサイト システムにインストールできます。 レポート サービス ポイントはセカンダリ サイトではサポートされません。 サイトの最初のレポート サービス ポイントが既定のレポート サーバーとして構成されます。 1 つのサイトに複数のレポート サービス ポイントをインストールすることは可能ですが、各サイトの既定のレポート サーバーが、Configuration Manager レポート用に優先して使用されます。 レポート サービス ポイントは、サイト サーバーまたはリモート サイト システムにインストールすることができます。 ただし、パフォーマンス上の最善の方法として、リモート サイト システム サーバーでは Reporting Services を使用してください。  

###  <a name="BKMK_DataReplication"></a> データ レプリケーションに関する注意事項  
 Configuration Manager は、レプリケートするデータをグローバル データまたはサイト データとして分類します。 グローバル データは、管理ユーザーにより作成され、階層内のすべてのサイトに対してレプリケートされるオブジェクトを対象としますが、セカンダリ サイトはグローバル データのサブセットのみを受信します。 グローバル データの例としては、ソフトウェアの展開、ソフトウェア更新プログラム、コレクション、役割に基づいた管理のセキュリティ スコープがあります。 サイト データとは、Configuration Manager のプライマリ サイトと、プライマリ サイトに報告するクライアントが作成する処理情報を指します。 サイト データは、中央管理サイトにレプリケートされますが、他のプライマリ サイトにはレプリケートされません。 サイト データの例としては、ハードウェア インベントリ データ、ステータス メッセージ、アラート、クエリによって生成されるコレクションがあります。 サイト データは、中央管理サイトと、データの作成元のプライマリ サイトだけで見ることができます。  

 レポート サービス ポイントのインストール場所を決定するにあたり、以下の要素を考慮してください。  

-   中央管理サイトのデータベースをレポート データ ソースとするレポート サービス ポイントは、グローバル データと Configuration Manager 階層内のすべてのサイト データにアクセスできます。 階層内の複数サイトのサイト データを含むレポートが必要な場合は、レポート サービス ポイントを中央管理サイトのサイト システムにインストールし、中央管理サイトのデータベースをレポート データ ソースとして使用することを検討してください。  

-   子プライマリ サイトのデータベースをレポート データ ソースとするレポート サービス ポイントは、グローバル データと、ローカルのプライマリ サイトと子セカンダリ サイトのみのサイト データにアクセスできます。 Configuration Manager 階層内のその他のプライマリ サイトのサイト データはこのプライマリ サイトに対してレプリケートされないため、Reporting Services がアクセスすることはできません。 特定のプライマリ サイトのサイト データまたはグローバル データを含むレポートが必要であり、レポート ユーザーにその他のプライマリ サイトのサイト データへのアクセスを許可したくない場合は、特定のプライマリ サイトのサイト システムにレポート サービス ポイントをインストールし、そのプライマリ サイトのデータベースをレポート データ ソースとして使用してください。  

###  <a name="BKMK_NetworkBandwidth"></a> ネットワークの帯域幅に関する考慮事項  
 同じサイト内のサイト システム サーバーは、サイトの構成方法に応じて、サーバー メッセージ ブロック (SMB)、HTTP、HTTPS のいずれかを使用して相互に通信します。 この通信は管理対象外であり、ネットワークの帯域幅の制御なしに随時生じ得るため、レポート サービス ポイントの役割をサイト システムにインストールする前に使用可能なネットワーク帯域幅を確認しておいてください。  

> [!NOTE]  
>  サイト システムの計画の詳細については、「[サイト システムの役割を追加する](../deploy/configure/add-site-system-roles.md)」を参照してください。  

##  <a name="BKMK_RoleBaseAdministration"></a> レポートのロール ベース管理の計画  
 レポートのセキュリティは、セキュリティ ロールとアクセス許可を管理ユーザーに割り当てることができる Configuration Manager のその他のオブジェクトと同様に機能します。 管理ユーザーは、適切なセキュリティ権限が付与されたレポートのみの実行と変更が可能です。 Configuration Manager コンソールでレポートを実行するには、**サイト** の **読み取り** 権限アクセス許可と特定のオブジェクト用に構成されたアクセス許可が必要です。  

 ただし、Configuration Manager のその他のオブジェクトとは異なり、Configuration Manager コンソールで管理ユーザー向けに設定するセキュリティ権限は、Reporting Services でも構成する必要があります。 Configuration Manager コンソールでセキュリティ権限を構成すると、レポート サービス ポイントは Reporting Services に接続して、レポート用に適切なアクセス許可を設定します。 たとえば、 **ソフトウェア更新マネージャー** セキュリティ ロールには、 **レポートの実行** と **レポートの変更** アクセス許可が関連付けられます。 "ソフトウェア更新マネージャー" の役割のみが割り当てられた管理ユーザーは、ソフトウェア更新プログラムのレポートの実行と変更のみを行うことができます。 **** その他のオブジェクトのレポートは Configuration Manager コンソールに表示されません。 例外として、特定の Configuration Manager の保護可能なオブジェクトが関連付けられていないレポートがあります。 これらのレポートについて、管理ユーザーには、レポートを実行する場合は **サイト** の **読み取り** 権限アクセス許可が、レポートを変更する場合は **サイト** の **変更** 権限アクセス許可が必要です。  

 レポートはロール ベース管理に対応しています。 Configuration Manager に含まれているすべてのレポートのデータが、レポートを実行する管理ユーザーのアクセス許可に基づいてフィルター処理されます。 特定の役割を持つ管理ユーザーに対して、個々の役割に定義されている情報のみ表示できます。  

 レポートのセキュリティ権限について詳しくは、「[Configure reporting](configuring-reporting.md)」(レポートを構成する) を参照してください。  

 Configuration Manager の役割に基づいた管理の詳細については、「[Configure role-based administration](../deploy/configure/configure-role-based-administration.md)」(役割に基づいた管理の構成) を参考にしてください。  

## <a name="next-steps"></a>次のステップ  
 Configuration Manager のレポートを計画する際には、次の補足トピックを参考にしてください。  

-   [System Center Configuration Manager のレポートの前提条件](../../../core/servers/manage/prerequisites-for-reporting.md)  
-   [System Center Configuration Manager のレポートのベスト プラクティス](../../../core/servers/manage/best-practices-for-reporting.md)  

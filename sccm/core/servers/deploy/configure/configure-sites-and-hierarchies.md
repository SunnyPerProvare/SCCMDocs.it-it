---
title: "サイトの構成 | Microsoft Docs"
description: "このチェックリストを利用し、サイトと階層の両方に影響を与える最も一般的な構成を考慮してください。"
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
caps.latest.revision: "15"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 862f420c063cb44c419d4904fbb4696efb739758
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="configure-sites-and-hierarchies-for-system-center-configuration-manager"></a>System Center Configuration Manager のサイトと階層の構成

*適用対象: System Center Configuration Manager (Current Branch)*

最初の System Center Configuration Manager サイトのインストールまたは階層へのサイトの追加後に、次のチェック リストを使用して、サイトと階層の両方に影響する最も一般的な構成を検討しているか確認します。  

## <a name="checklist-of-common-configurations-for-new-and-additional-sites"></a>新規および追加のサイト用の一般的な構成のチェック リスト  
以下に示したのは構成に関する注意事項であり、ほとんどの展開に該当します。

-   Active Directory フォレストの探索、境界、境界グループなどのように、互いに依存しているオプションもあります。  

-   一部の構成には、当面は構成の変更を必要とせずに使用できる既定値が設定されています。  

-   境界グループや配布ポイント グループなどのその他の構成は、使用前に構成が必要となります。  

|操作|説明|  
|------------|-------------|  
|ロール ベース管理の構成|Configuration Manager 環境でさまざまなオブジェクトやデータを表示および管理できる管理ユーザーを制御するために、管理の割り当て区分を設定します。<br /><br /> ロール ベース管理の構成は、階層内のすべてのサイトで共有されます。   <br/><br/>詳細については、「[Configure role-based administration for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md)」(System Center Configuration Manager の役割ベースの管理の構成) を参照してください。|  
|サイト データを Active Directory ドメイン サービス (AD DS) に発行する|クライアントから簡単にサービスを検出し、サイトのリソースを効率よく使用できるようにします。<br /><br /> まず、[System Center Configuration Manager 向けに Active Directory スキーマを拡張し](../../../../core/plan-design/network/extend-the-active-directory-schema.md)、次に、各サイトがそれぞれ [System Center Configuration Manager のサイト データを発行する](../../../../core/servers/deploy/configure/publish-site-data.md)ように構成する必要があります。|  
|サービス接続ポイントを構成する|サービス接続ポイントは、階層の最上位層にインストールして構成するようにします。 詳細については、[System Center Configuration Manager のサービス接続ポイントについて](../../../../core/servers/deploy/configure/about-the-service-connection-point.md)をご覧ください。|  
|サイト システムの役割を追加する|個々のサイトに追加のサイト システムの役割を 1 つ以上インストールします。  詳細については、「[System Center Configuration Manager のサイト システム役割の追加](../../../../core/servers/deploy/configure/add-site-system-roles.md)」を参照してください。|  
|サイト境界と境界グループを構成する|イントラネット上で管理対象デバイスを置くことのできるネットワークの場所は、境界を指定することによって定義します。 そのうえで、そうしたネットワークの場所に置かれたクライアントが Configuration Manager のリソースを検出できるように境界グループを構成します。 詳細については、「[System Center Configuration Manager のサイト境界と境界グループの定義](../../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md)」を参照してください。|  
|配布ポイント グループを構成する|展開を管理しやすくするために配布ポイントの論理グループを構成します。 詳しくは、「[System Center Configuration Manager の配布ポイントのインストールと構成](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md)」の「[配布ポイント グループの管理](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage)」をご覧ください。|  
|検出を実行する|検出を実行して、ネットワーク インフラストラクチャ、デバイス、ユーザーなどのネットワーク上のリソースを見つけます。<br /><br /> 詳細については、「 [System Center Configuration Manager 用の探索の実行](../../../../core/servers/deploy/configure/run-discovery.md)」をご覧ください。|  
|インフラストラクチャの管理者向けに冗長性と容量を追加する|追加の SMS プロバイダーと Configuration Manager コンソールをインストールすると、管理者がインフラストラクチャの管理に使用する容量を拡張することができます。<br /><br /> **追加の SMS プロバイダーをインストール**して、サイトや階層を管理するための接続ポイントに冗長性を与えます。 詳細については、「[System Center Configuration Manager インフラストラクチャの変更](../../../../core/servers/manage/modify-your-infrastructure.md)」の「[SMS プロバイダーを管理する](../../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider)」を参照してください。<br /><br /> **追加の Configuration Manager コンソールをインストール**して、追加の管理ユーザーに対してアクセス許可を与えます。 詳しくは、「[System Center Configuration Manager コンソールをインストールする](../../../../core/servers/deploy/install/install-consoles.md)」をご覧ください。|  
|サイト コンポーネントを構成する|サイト システムの役割とサイト ステータス レポートの動作は、各サイトでサイト コンポーネントを構成することによって変更できます。 詳細については、[System Center Configuration Manager のサイト コンポーネント](../../../../core/servers/deploy/configure/site-components.md)をご覧ください。|  
|カスタム コレクションを作成する|デバイスとユーザーについて検出された情報を使用し、将来の管理タスクを単純化するために、オブジェクトのカスタム コレクションを作成します。 詳細については、「[System Center Configuration Manager でコレクションを作成する方法](../../../../core/clients/manage/collections/create-collections.md)」を参照してください。|  
|危険度の高い展開を管理するための設定を構成する|管理ユーザーが危険度の高いタスク シーケンスの展開を作成すると警告が表示されるように、サイトの設定を構成します。  詳細については、「[System Center Configuration Manager の危険度の高い展開を管理するための設定](../../../../protect/understand/settings-to-manage-high-risk-deployments.md)」を参照してください。|  
|管理ポイントのデータベース レプリカを構成する|管理ポイントがクライアントからの要求を供給することでサイト データベース サーバーに加えられた CPU 負荷を軽減するように、データベース レプリカを構成します。 詳細については、「[Database replicas for management points for System Center Configuration Manager (System Center Configuration Manager の管理ポイント用データベース レプリカ)](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md)」を参照してください。|  
|サイト データベースをホストする SQL Server AlwaysOn 可用性グループの構成|バージョン 1602 以降では、プライマリ サイトと中央管理サイトでサイト データベースをホストするための高可用性と障害復旧ソリューションとして可用性グループを構成します。 詳細については、「[System Center Configuration Manager 用の高可用性サイト データベースの SQL Server AlwaysOn](../../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)」を参照してください。|  
|サイト間のレプリケーションを変更する|「[System Center Configuration Manager のサイト間でのデータの転送](../../../../core/servers/manage/data-transfers-between-sites.md)」をご覧になり、次に挙げる事項についてお読みください。<br /><br /> セカンダリ サイト間の[ファイルベースのレプリケーション](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_fileroute)を構成する<br /><br /> [データベース レプリケーション リンク](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_Dblinks)を構成する<br /><br /> [分散ビュー](../../../../core/servers/manage/data-transfers-between-sites.md#bkmk_distviews)を構成する|  

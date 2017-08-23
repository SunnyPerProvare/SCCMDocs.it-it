---
title: "サイト データベースの計画 | Microsoft Docs"
description: "System Center Configuration Manager の階層を計画するとき、サイト データベースとサイト データベース サーバーの役割を考える必要があります。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: d4efe1f013dbb74efca79cd27f7248fc085c7424
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-the-site-database-for-system-center-configuration-manager"></a>System Center Configuration Manager のサイト データベースの計画

*適用対象: System Center Configuration Manager (Current Branch)*

サイト データベース サーバーとは、Microsoft SQL Server のサポートされているバージョンを実行するコンピューターのことです。 SQL Server を使用して、Configuration Manager サイトの情報を格納します。 Configuration Manager 階層内の各サイトには、サイト データベースと、サイト データベース サーバーの役割を持つサーバーがあります。  

-   中央管理サイトとプライマリ サイトでは、SQL Server をサイト サーバーにインストールすることも、サイト サーバー以外のサーバーにインストールすることもできます。  

-   セカンダリ サイトでは、SQL Server の完全版の代わりに、SQL Server Express をインストールできます。 ただし、データベース サーバーは、セカンダリ サイト サーバーで実行する必要があります。  

次の SQL Server 構成を使用して、サイト データベースをホストできます。  

-   SQL Server の既定のインスタンス  

-   SQL Server を実行している 1 台のコンピューターの名前付きインスタンス  

-   SQL Server のクラスター化されたインスタンスの名前付きインスタンス  

-   SQL Server AlwaysOn 可用性グループ (System Center Configuration Manager のバージョン 1602 以降)


サイト データベースをホストするには、SQL Server が「[System Center Configuration Manager の SQL Server バージョンのサポート](../../../core/plan-design/configs/support-for-sql-server-versions.md)」に記載されている要件を満たしている必要があります。  



## <a name="remote-database-server-location-considerations"></a>リモート データベース サーバーの場所に関する考慮事項  

リモート データベース サーバーのコンピューターを使用する場合は、介在するネットワーク接続が可用性の高い広帯域のネットワーク接続であることを確認します。 サイト サーバーとサイト システムの役割のいくつかは、サイト データベースをホストしているリモート サーバーと継続的に通信する必要があります。

-   データベース サーバーとの通信に必要な帯域幅は、サイトとクライアントの構成によって異なります。 そのため、実際に必要な帯域幅を的確に予測することはできません。  

-   SMS プロバイダーを実行し、サイト データベースに接続するコンピューターが多いほど、必要なネットワーク帯域幅が大きくなります。  

-   SQL Server を実行するコンピューターは、サイト サーバー、および SMS プロバイダーを実行しているすべてのコンピューターとの双方向の信頼関係があるドメインになければなりません。  

-   サイト データベースとサイト サーバーを併置する場合は、クラスター化された SQL Server をサイト データベース サーバーにすることはできません。  


通常、サイト システム サーバーは、1 つだけの Configuration Manager サイトのサイト システムの役割をサポートしています。 ただし、SQL Server を実行するクラスター化または非クラスター化サーバーで、SQL Server のさまざまなインスタンスを使用して、さまざまな Configuration Manager サイトのデータベースをホストできます。 この場合は、SQL Server の各インスタンスが、通信用に別々のポートを使用するように構成する必要があります。  

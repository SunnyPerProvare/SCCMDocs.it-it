---
title: "移行の計画 | Microsoft Docs"
description: "System Center Configuration Manager の移行先階層にデータを移行する前に、サイトと階層について学んでください。"
ms.custom: na
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: fffef1e95e1dfa03971f140a6e5a7fff9bfe5e27
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-migration-to-system-center-configuration-manager"></a>System Center Configuration Manager の移行の計画

*適用対象: System Center Configuration Manager (Current Branch)*

データを System Center Configuration Manager 移行先階層に移行する前に、Configuration Manager のサイトと階層を把握しておく必要があります。 サイトと階層の詳細については、「[System Center Configuration Manager の基本](../../core/understand/fundamentals.md)」を参照してください。  

 移行先階層にする System Center Configuration Manager 階層をインストールしてから、サポートされるソース階層からデータを移行する必要があります。  

 移行先階層をインストールしたら、移行先階層で使用する管理機能を設定してから、データの移行を開始します。  

 さらに、状況に応じて、ソース階層と移行先階層で重複が発生した場合についても計画する必要があります。 たとえば、移行先階層と同じネットワークの場所または境界を使用するようにソース階層が設定されている場合に、移行先階層に新しいクライアントをインストールして、自動サイト割り当てを使用するとします。 このシナリオでは、新しくインストールした Configuration Manager クライアントが、いずれかの階層から参加するサイトを選択できるため、クライアントがソース階層に誤って割り当てられる可能性があります。 そのため、移行先階層内の新しい各クライアントは、自動サイト割り当てを使用せずに、その階層内の特定のサイトに割り当てるように計画してください。  

 サイトの割り当ての詳細については、「[異なるバージョンの Configuration Manager 間の相互運用性](../../core/plan-design/hierarchy/interoperability-between-different-versions.md)」の「[クライアントのサイト割り当てに関する考慮事項](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment)」を参照してください。  

## <a name="plan-topics"></a>計画に関するトピック  
 サポートされるソース階層を System Center Configuration Manager 移行先階層に移行する方法を計画する際には、次のトピックを参照してください。

-   [System Center Configuration Manager での移行の前提条件](../../core/migration/prerequisites-for-migration.md)  

-   [System Center Configuration Manager での移行計画の管理者チェックリスト](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [データを System Center Configuration Manager に移行するかどうかの判断](../../core/migration/determine-whether-to-migrate-data.md)  

-   [System Center Configuration Manager でのソース階層戦略の計画](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [System Center Configuration Manager での移行計画の管理者チェックリスト](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [System Center Configuration Manager でのクライアント移行戦略の計画](../../core/migration/planning-a-client-migration-strategy.md)  

-   [System Center Configuration Manager のコンテンツ展開移行戦略の計画](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Configuration Manager オブジェクトの System Center Configuration Manager への移行の計画](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [System Center Configuration Manager での移行アクティビティの監視の計画](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [System Center Configuration Manager での移行完了の計画](../../core/migration/planning-to-complete-migration.md)  

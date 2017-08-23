---
title: "データの移行 | Microsoft Docs"
description: "ソース階層から System Center Configuration Manager の移行先階層にデータを転送する方法について説明します。"
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
caps.latest.revision: "11"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: dface33392c2a2a662522656eabf0936b52b28fc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="migrate-data-between-hierarchies-in-system-center-configuration-manager"></a>System Center Configuration Manager の階層間でのデータの移行

*適用対象: System Center Configuration Manager (Current Branch)*

サポートされるソース階層から System Center Configuration Manager の移行先階層にデータを転送するには、移行を使用します。  ソース階層からデータを移行すると、次のようになります。  

-   ソース インフラストラクチャで識別したサイト データベースからデータにアクセスし、そのデータを現在の環境に転送します。  

-   移行処理ではソース階層内のデータは変更されません。代わりに、そのデータを検出して、移行先階層のデータベースにコピーを保存します。  

移行戦略を計画する場合は、次の点を考慮してください。  

-   既存の Configuration Manager 2007 SP2 インフラストラクチャを、System Center Configuration Manager に移行できます。  

-   サポートされるデータの一部またはすべてをソース サイトから移行することができます。  

-   1 つのソース サイトから移行先階層の複数のサイトにデータを移行することができます。  

-   複数のソース サイトから移行先階層内の 1 つのサイトにデータを移動することができます。  

##  <a name="BKMK_MigrationConcepts"></a> 移行に関する概念  
 移行を使用するとき、次の概念や用語が出てくることがあります。  

|概念または用語|説明|  
|---------------------|----------------------|  
|ソース階層|Configuration Manager のサポートされているバージョンを実行していて、移行するデータを含む階層。 移行を構成する場合、ソース階層の最上位サイトを指定するときにソース階層を識別します。 ソース階層の指定後、移行先階層の最上位サイトは、指定されたソース サイトのデータベースからデータを収集して、移行可能なデータを特定します。<br /><br /> 詳しくは、「[System Center Configuration Manager でのソース階層戦略の計画](../../core/migration/planning-a-source-hierarchy-strategy.md)」の「[ソース階層](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Source_Hierarchies)」を参照してください。|  
|ソース サイト|移行先階層に移行できるデータを含むソース階層のサイト。<br /><br /> 詳しくは、「[System Center Configuration Manager でのソース階層戦略の計画](../../core/migration/planning-a-source-hierarchy-strategy.md)」の「[ソース サイト](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Source_Sites)」を参照してください。|  
|移行先階層|ソース階層からのデータのインポートが実行される System Center Configuration Manager 階層。|  
|データ収集|移行先階層に移行可能なソース階層内の情報を特定する継続的な処理。 Configuration Manager は、スケジュールに従ってソース階層を確認し、移行済みのソース階層内の情報に対する変更や、移行先階層で更新する可能性があるデータを識別します。<br /><br /> 詳しくは、「[System Center Configuration Manager でのソース階層戦略の計画](../../core/migration/planning-a-source-hierarchy-strategy.md)」の「[データ収集](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering)」を参照してください。|  
|移行ジョブ|移行する特定のオブジェクトを構成してから、そのオブジェクトの移行先階層への移行を管理する処理。<br /><br /> 詳しくは、「[System Center Configuration Manager での移行ジョブ戦略の計画](../../core/migration/planning-a-migration-job-strategy.md)」を参照してください。|  
|クライアントの移行|クライアントが使用する情報をソース サイトのデータベースから移行先階層のデータベースに転送する処理。 データの移行後、デバイス上のクライアント ソフトウェアを、移行先階層のクライアント ソフトウェアにアップグレードします。<br /><br /> 詳細については、[System Center Configuration Manager での移行ジョブ戦略の計画](../../core/migration/planning-a-client-migration-strategy.md)をご覧ください。|  
|共有配布ポイント|移行期間中に移行先階層と共有されるソース階層の配布ポイント。<br /><br /> 移行期間中に、移行先階層内のサイトに割り当てられたクライアントは、共有配布ポイントからコンテンツを取得できます。<br /><br /> 詳しくは、「[System Center Configuration Manager のコンテンツ展開移行戦略の計画](../../core/migration/planning-a-content-deployment-migration-strategy.md)」の「[ソース階層と移行先階層で配布ポイントを共有する](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration)」を参照してください。|  
|移行の監視|移行処理を監視する処理。 [**管理**] ワークスペースの [**移行**] ノードから、移行の進行状況と成功状態を監視します。<br /><br /> 詳しくは、「[System Center Configuration Manager での移行アクティビティの監視の計画](../../core/migration/planning-to-monitor-migration-activity.md)」を参照してください。|  
|データ収集の停止|ソース サイトからのデータ収集を停止する処理。 ソース階層から移行するデータがなくなった場合や、移行関連のアクティビティを一時停止する場合、ソース階層からのデータ収集を停止するように移行先階層を構成できます。<br /><br /> 詳しくは、「[System Center Configuration Manager でのソース階層戦略の計画](../../core/migration/planning-a-source-hierarchy-strategy.md)」の「[データ収集](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering)」を参照してください。|  
|移行データのクリーンアップ|移行先階層のデータベースから移行関連情報を削除することで、ソース階層からの移行を終了する処理。<br /><br /> 詳細については、[System Center Configuration Manager での移行完了の計画](../../core/migration/planning-to-complete-migration.md)をご覧ください。|  

## <a name="typical-workflow-for-migration"></a>移行の一般的なワークフロー  
移行のワークフローを設定するには:

1.  サポートされるソース階層を指定します。  

2.  データ収集を設定します。 データ収集によって、Configuration Manager は、ソース階層から移行できるデータに関する情報を収集できます。  

     データ収集プロセスを停止するまで、Configuration Manager は、簡単なスケジュールに基づいてデータを収集するプロセスを自動的に繰り返します。 既定では、データ収集プロセスは 4 時間間隔で繰り返されるため、Configuration Manager は、移行対象であるソース階層内のデータの変更を特定できます。 データ収集は、ソース階層から移行先階層への配布ポイントを共有するためにも必要です。  

3.  ソース階層と移行先階層間でデータを移行する移行ジョブを作成します。  

4.  データ収集プロセスは、[ **データ収集の停止** ] コマンドを使用していつでも停止できます。 データ収集を停止すると、Configuration Manager はソース階層内のデータに対する変更内容を特定する処理も停止されるため、ソース階層と移行先階層間の配布ポイントは共有できなくなります。 通常、この操作は、ソース階層からのデータ移行や配布ポイントの共有を行う予定がなくなった場合に使用します。  

5.  必要に応じて、ソース階層のすべてのサイトでデータ収集を停止した後に、[ **移行データのクリーン アップ** ] コマンドを使用して移行データをクリーン アップすることができます。 このコマンドで、ソース階層の移行に関する階層データが移行先階層のデータベースから削除されます。  

Configuration Manager ソース階層からデータを移行した後に、ソース階層を環境の管理に使用しない場合は、そのソース階層とインフラストラクチャの使用を停止できます。  

##  <a name="BKMK_MigrationScenarios"></a> 移行シナリオ  
 Configuration Manager は次の移行シナリオをサポートします。  

> [!NOTE]  
>  スタンドアロン サイトを含む階層を、中央管理サイトを含む階層に拡張することは、移行に分類されません。 階層の拡張の詳細については、「[Use the Setup Wizard to install sites](../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md)」(セットアップ ウィザードを使用してサイトをインストールする) の「[Expand a stand-alone primary site](../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand)」(スタンドアロン プライマリ サイトを拡張する) を参照してください。  

### <a name="migration-from-configuration-manager-2007-hierarchies"></a>Configuration Manager 2007 階層からの移行  
 Configuration Manager 2007 からデータを移行する場合、既存のサイト インフラストラクチャの投資を保護できるだけでなく、次の利点があります。  

|特長|説明|  
|-------------|----------------------|  
|サイト データベースの向上点|System Center Configuration Manager データベースは、Unicode を完全にサポートします。|  
|サイト間のデータベース レプリケーション|System Center Configuration Manager のレプリケーションは、Microsoft SQL Server に基づいています。 そのため、サイト間のデータ転送のパフォーマンスが改善されます。|  
|ユーザー中心の管理|System Center Configuration Manager での管理タスクの中心はユーザーです。 たとえば、ユーザーのデバイス名が不明な場合にも、ユーザーにソフトウェアを配布することができます。 また、System Center Configuration Manager では、ユーザーのデバイスにインストールできるソフトウェアやインストールのタイミングの管理だけでなく、さまざまな管理機能を利用できます。|  
|階層の簡略化|System Center Configuration Manager では、サイトの種類に中央管理サイトが追加されたほか、プライマリ サイトとセカンダリ サイトの動作が変更され、使用するネットワーク帯域幅とサーバーの数が少なくて済む、より簡素なサイト階層を構築できるようになりました。|  
|役割に基づいた管理|System Center Configuration Manager の中央管理型のセキュリティ モデルにより、それぞれの管理要件と業務要件に合わせた階層全体のセキュリティと管理機能が提供されます。|  

> [!NOTE]  
>  System Center 2012 Configuration Manager で初めて導入された設計の変更のため、Configuration Manager 2007 のインフラストラクチャを System Center Configuration Manager にアップグレードすることはできません。 System Center 2012 Configuration Manager から System Center Configuration Manager へのインプレース アップグレードはサポートされています。  

### <a name="migration-from-configuration-manager-2012-or-another-system-center-configuration-manager-hierarchy"></a>Configuration Manager 2012 または他の System Center Configuration Manager 階層からの移行  
 System Center 2012 Configuration Manager 階層または System Center Configuration Manager 階層からデータを移行するプロセスは同じです。 たとえば、会社が Configuration Manager によって既に管理されている追加のリソースを獲得する場合などに、複数のソース階層のデータを 1 つの移行先階層に移行することができます。 さらに、テスト環境のデータを Configuration Manager 運用環境に移行することもできます。 そのため、Configuration Manager テスト環境への投資を維持できます。  

## <a name="additional-topics-for-migration"></a>移行に関連するトピック:  

-   [System Center Configuration Manager への移行の計画](../../core/migration/planning-for-migration.md)  

-   [System Center Configuration Manager に移行するためのソース階層とソース サイトの構成](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)  

-   [System Center Configuration Manager に移行するための操作](../../core/migration/operations-for-migration.md)  

-   [System Center Configuration Manager への移行のセキュリティとプライバシー](../../core/migration/security-and-privacy-for-migration.md)  

## <a name="see-also"></a>関連項目  
 [System Center Configuration Manager の使用の開始](../../core/servers/deploy/start-using.md)

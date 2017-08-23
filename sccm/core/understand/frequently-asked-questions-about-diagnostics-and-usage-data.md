---
title: "診断データに関してよく寄せられる質問 |Microsoft Docs"
description: "System Center Configuration Manager の診断および使用状況データに関してよく寄せられる質問を説明します。"
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 177a30a30f6b8579fa1956d28581d4f9d3a11838
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>System Center Configuration Manager の診断および使用状況データに関してよく寄せられる質問

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の診断および使用状況データに関してよく寄せられる質問は次のとおりです。  

###  <a name="bkmk_off"></a> テレメトリを無効にするには、どうすればよいですか。  
テレメトリを無効にすることはできません。 ただし、収集されるテレメトリ データのレベルを選択することはできます。 サービス接続ポイントをオフライン モードで使用することによって、テレメトリ データが送信されるタイミングを管理することもできます。

Configuration Manager の現在のブランチは、Windows 10 と Microsoft Intune の新しいバージョンをサポートするために、定期的に更新する必要があります。 製品を最新の状態に保ち、更新プログラムのエクスペリエンスおよび製品の品質とセキュリティを向上させるために、Microsoft は少なくとも基本レベルの診断および使用状況データを必要としています。

###  <a name="bkmk_retention"></a> データの保存期間を教えてください。  
 診断結果と使用状況データは 1 年間は保持されます。  

###  <a name="bkmk_update"></a> 製品をインストールまたは更新するときに、診断と使用状況のデータは送信されますか。  
 いいえ。 診断および使用状況データは、サイトがインストールされて使用できる状態になったら送信されます。  

###  <a name="bkmk_frequency"></a> データはどのくらいの頻度で送信されますか。  
 SQL ストアド プロシージャは (サイトがインストールされた日) から 7 日おきに実行されます。 オンライン モードでは、サービス接続ポイントはクエリの実行後にデータをアップロードするように構成されています。 オフライン モードでは、管理者はサービス接続ツールを使用してデータをアップロードします。 (注: サイトがインストールされてから 7 日間経過したときに初めてデータをオフラインで使用できるようになります。)  

###  <a name="bkmk_network"></a> データを使用してネットワーク マップを作成できますか。  
 「System Center Configuration Manager の診断の使用状況データ収集のレベル」の説明のとおり、サイトの詳細には各サイトからのタイムゾーン情報が含まれます。 この情報により、階層の複数のサイトの広範な位置情報とグローバル分散を理解できます。 ただし、IP アドレスや詳細な地理情報など、ネットワークの詳細情報は収集されません。
 - [1511 の診断データ](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1511)
 - [1602 の診断データ](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1602)
 - [1606 の診断データ](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1606)
 - [1610 の診断データ](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1610)


###  <a name="bkmk_tables"></a> カスタム テーブルのデータを確認できますか。  
 いいえ。 データベース内の既定の製品テーブルに対する診断および使用状況データは、SQL ストアド プロシージャによって収集されます (これらのすべてには接頭辞 **TEL_** が付いています)。 SQL スキーマ検出クエリの一部として、すべてのテーブル名は既知の既定値と比較するためにハッシュされます。 これにより、カスタム テーブルがデータベースに存在する (つまり、データベース スキーマが既定値から拡張された) けれども、それらのテーブル内にはデータが含まれていないことが分かります。  

###  <a name="bkmk_databases"></a> 他のデータベースの名前や、他のデータベース内のデータを確認できますか。  
 いいえ。 データを収集するストアド プロシージャは、サイト データベースに限定されます。  

## <a name="see-also"></a>関連項目  
 [System Center Configuration Manager の診断結果と使用状況データ](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)

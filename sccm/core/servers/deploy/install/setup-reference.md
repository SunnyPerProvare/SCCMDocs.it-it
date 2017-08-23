---
title: "セットアップのリファレンス | Microsoft Docs"
description: "Configuration Manager サイトまたは階層をインストールするための準備をするには、このリファレンスを参照してください。"
ms.custom: na
ms.date: 4/18/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
caps.latest.revision: "22"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 739461a6cca0fd67431093524c1e8158afd80d0f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="reference-for-system-center-configuration-manager-setup"></a>System Center Configuration Manager のセットアップのリファレンス

*適用対象: System Center Configuration Manager (Current Branch)*

「System Center Configuration Manager のセットアップ」には、他のトピックへのリンクが掲載されています。詳細については、以下のセクションを参照してください。 ここに記載されている情報は、Configuration Manager サイトまたは階層のインストールの準備、およびインストール中に決定する必要があるいくつかの事項についての準備に役立ちます。  


##  <a name="bkmk_start"></a> 始める前に  
新しい Configuration Manager サイトをインストールする前に、展開を正常に設計するためのステージの設定に役立つ次の情報を必ずご確認ください。  

-   [System Center Configuration Manager の基本](../../../../core/understand/fundamentals.md)  
-   [System Center Configuration Manager インフラストラクチャの計画](../../../plan-design/network/configure-firewalls-ports-domains.md)  
-   [System Center Configuration Manager サイトのインストールを準備する](prepare-to-install-sites.md)  

##  <a name="bkmk_assess"></a> サーバーの準備状態の評価  
新しいサイトのインストールを開始する前に、サイトに使用しようとしているサイト サーバーとリモート サイト システム サーバー (サイト データベースをホストするサーバーなど) がすべての前提条件の構成を満たしていることを確認します。 ドキュメント ライブラリの以下のトピックが参考になります。  

-   [System Center Configuration Manager のサポートされている構成](../../../../core/plan-design/configs/supported-configurations.md)  
-   [前提条件チェッカー](prerequisite-checker.md)  

##  <a name="bkmk_Addclients"></a> 追加のオペレーティング システム用のクライアント  
Microsoft ダウンロード センターから、次のオペレーティング システム向けの Configuration Manager のクライアント ソフトウェアをダウンロードできます。  

-   Mac (Apple)  
-   UNIX  
-   Linux  

次のリンクを使用して、使用する Configuration Manager のバージョンのクライアントをダウンロードします。  

-   「[Microsoft System Center Configuration Manager - 追加のオペレーティング システム用のクライアント](http://www.microsoft.com/download/details.aspx?id=47719)」を参照してください。  

##  <a name="bkmk_usage"></a> 使用状況データのレベルと設定  
最初の System Center Configuration Manager サイトをインストールすると、Configuration Manager によってサイト サーバーに新しいサイト システムの役割 (**サービス接続ポイント**) が自動的にインストールされて構成されます。 既定では、サービス接続ポイントが次のように設定されています。  

-   **オンライン** モード (オフライン モードも利用可能)  
-   **拡張**のデータ収集レベル (その他 "基本" と "完全" の 2 つのデータ収集レベルが利用可能)  

サービス接続ポイントがサイト システムの役割としてオンラインになると、Microsoft が自動的に診断情報と使用状況情報をインターネット経由で収集できるようになります。 収集された情報は次のことに役立ちます。  

-   問題の識別とトラブルシューティング  
-   Microsoft の製品やサービスの向上  
-   使用する Configuration Manager のバージョンに適用する Configuration Manager の更新プログラムの識別  

### <a name="levels-of-data-collection"></a>データ コレクションのレベル  
データ収集には、次の 3 つのレベルがあります。

-   **基本**には、サイトの数や有効になる Configuration Manager 機能など、セットアップとアップグレードに関するデータが含まれます。 個人を特定できる情報は送信されません。  

-   **拡張**には、基本レベル設定内のデータが含まれるだけでなく、階層に関するデータ、各機能の使用方法 (頻度と期間)、システムまたはアプリのクラッシュが発生した場合のサーバーのメモリ状態などの詳細な診断情報が送信されます。 個人を特定できるデータは送信されません。  

-   **完全**には、基本レベル設定と拡張レベル設定内のデータが含まれるだけでなく、システム ファイルやメモリ スナップショットなどの高度な診断情報も送信されます。 このオプションには個人を特定できる情報が含まれる場合がありますが、その情報を使用して個人を特定して連絡したり、広告のターゲットにしたりすることはありません。  

各レベルで収集した詳細情報の開示を含む詳細については、「[System Center Configuration Manager の診断結果と使用状況データ](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)」を参照してください。  

System Center Configuration Manager のプライバシーに関する声明をオンラインで参照するには、[http://go.microsoft.com/fwlink/?LinkID=626527](http://go.microsoft.com/fwlink/?LinkID=626527) にアクセスしてください。

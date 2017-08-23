---
title: "レポートの概要 | Microsoft Docs"
description: "Configuration Manager でレポートを管理する際に使用できるツールとリソースについて説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 230be984-d2cd-4d53-bd7a-bc24dd93fc22
caps.latest.revision: "7"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 5846ca3c91626491b03b36dd17b454bb9382a8dc
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-reporting-in-system-center-configuration-manager"></a>System Center Configuration Manager のレポートの概要

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のレポートでは、SQL Reporting Services の高度なレポート機能と Reporting Services レポート ビルダーの充実したオーサリング機能を活用するために役立つ一連のツールとリソースを利用できます。 レポートは、組織内のユーザー、ハードウェアおよびソフトウェア インベントリ、ソフトウェアの更新、アプリケーション、サイト ステータス、およびその他の Configuration Manager 操作に関する情報を収集、整理、および提示するのに役立ちます。 レポート機能には、そのまま利用することも、必要に応じて変更することもできる定義済みレポートが多数用意されています。また、カスタム レポートを作成することもできます。 Configuration Manager のレポートを管理す際は、次のセクションを参考にしてください。  

##  <a name="BKMK_SQLServerReportingServices"></a> SQL Server Reporting Services  
 SQL Server Reporting Services は、各組織のレポートの作成、展開、および管理に役立つ既成の各種ツールとサービス、および、レポート機能の拡張とカスタマイズを可能にするプログラミング機能を提供します。 Reporting Services は、多様なデータ ソースを対象とした総合的レポート機能を提供する、サーバーベースのレポート プラットフォームです。  

 Configuration Manager は、SQL Server Reporting Services をレポート ソリューションとして使用します。 この Reporting Services との統合の利点は、次のとおりです。  

-   Configuration Manager データベースのクエリに業界標準のレポート システムを使用できます。  

-   Configuration Manager レポート ビューアー、または Web ベースでレポートに接続するレポート マネージャーを使用してレポートを表示できます。  

-   優れたパフォーマンス、可用性、およびスケーラビリティを実現します。  

-   ユーザーがサブスクライブ可能なレポートのサブスクリプション機能を利用できます。たとえば管理者は、ソフトウェア更新プログラムのロールアウト ステータスの詳細を示すレポートにサブスクライブし、毎日自動的に電子メールでレポートを受信することができます。  

-   ユーザーが選択できる各種の標準形式でレポートをエクスポートできます。  

 Reporting Services の詳細については、SQL Server 2008 オンライン ブックの「 [SQL Server Reporting Services](http://go.microsoft.com/fwlink/p/?LinkID=212032) 」を参照してください。  

##  <a name="BKMK_ReportingServicesPoint"></a> レポート サービス ポイント  
 レポート サービス ポイントはサイト システムの役割の 1 つで、Microsoft SQL Server Reporting Services を実行しているサーバー上にインストールされます。 レポート サービス ポイントは、Configuration Manager レポートの定義を Reporting Services にコピーし、レポート カテゴリを基にレポート フォルダーを作成し、Configuration Manager 管理ユーザーの役割に基づいた権限に従ってレポート フォルダーとレポートのセキュリティ ポリシーを設定します。 レポート マネージャーなどを使用して、10 分間隔でレポート サービス ポイントが Reporting Services に接続し、変更があったセキュリティ ポリシーを再度適用します。 レポート サービス ポイントの計画とインストールの詳細については、次のドキュメントを参照してください。  

-   [System Center Configuration Manager のレポートの計画](planning-for-reporting.md)  

-   [System Center Configuration Manager におけるレポートの構成](configuring-reporting.md)  

##  <a name="BKMK_ConfigurationManagerReports"></a> Configuration Manager レポート  
 Configuration Manager は、50 以上のレポート フォルダー内の 400 以上のレポートを対象とするレポート定義を提供します。レポート サービス ポイントのインストール過程で、このレポート定義は SQL Server Reporting Services のルート レポート フォルダーにコピーされます。 レポートは Configuration Manager コンソールに表示され、レポート カテゴリに基づくサブフォルダーに整理されます。 レポートは、Configuration Manager 階層の上位や下位へ伝達されることはなく、作成されたデータベースに対してのみ実行されます。 ただし、Configuration Manager はグローバル データを階層全体にレプリケートするため、階層全体の情報にアクセスできます。 レポートがサイト データベースからデータを取得する際に、現在のサイトと子サイトのサイト データ、および階層内の全サイトのグローバル データにアクセスできます。 他の Configuration Manager オブジェクトと同様に、管理ユーザーがレポートの実行や変更を行うには適切なアクセス許可が必要となります。 レポートを実行するには、オブジェクトの "レポートの実行" アクセス許可が必要です。 **** レポートを作成するには、オブジェクトの "レポートの変更" アクセス許可が必要です。 ****  

###  <a name="BKMK_CreatingReports"></a> レポートの作成と変更  
 Configuration Manager では、モデルベースのレポートと SQL ベースのレポートの両方を対象に、Microsoft SQL Server レポート ビルダーが専用のオーサリングおよび編集ツールとして使用されます。 Configuration Manager コンソールでレポートの作成または編集を行うと、レポート ビルダーが開きます。 レポートの管理の詳細については、「[System Center Configuration Manager でのレポートの操作とメンテナンス](operations-and-maintenance-for-reporting.md)」を参照してください。  

###  <a name="BKMK_RunningReports"></a> レポートを実行する  
 Configuration Manager コンソールでレポートを実行すると、レポート ビルダーが開きます。 レポートの必須パラメーターの指定後、Reporting Services がデータを取得してビューアーに結果を表示します。 また、SQL Services Reporting Services に接続し、サイトのデータ ソースにアクセスしてレポートを実行することもできます。  

###  <a name="BKMK_ReportPrompts"></a> レポートのプロンプト  
 Configuration Manager のレポート プロンプトまたはレポート パラメーターは、レポートの作成時または変更時に構成可能なレポート プロパティです。 レポート プロンプトは、レポートで取得するデータを制限したり指定したりするために作成します。 レポートには、プロンプト名が固有のものである限りは複数のプロンプトを入れることができ、識別子については SQL Server 規則に準拠する英数字のみが使用できます。  

 レポートを実行すると、必要なパラメーターの値を要求するプロンプトが表示され、その値に基づいてレポート データが取得されます。 たとえば、[特定のコンピューターのコンピューター情報] レポートは、特定のコンピューターに関するコンピューター情報を取得するため、管理ユーザーがコンピューター名を入力することが求められます。 **** Reporting Services は、レポートの SQL ステートメントで定義されている変数に指定値を渡します。  

###  <a name="BKMK_ReportLinks"></a> レポート リンク  
 Configuration Manager のレポート リンクをソース レポートで使用して、ソース レポートの各項目の詳細などの追加データへの簡単なアクセスを管理ユーザーに示すことができます。 ターゲット レポートでプロンプトを実行する必要がある場合は、各プロンプトの適切な値の入った列をソース レポートに含める必要があります。 プロンプトの値が含まれている列の番号を指定する必要があります。 たとえば、最近探索されたコンピューターを一覧表示するレポートを、特定のコンピューターに関して最近受信されたメッセージを一覧表示するレポートにリンクするとします。 リンクを作成するときに、ソース レポートの列 2 に、ターゲット レポートに必要なプロンプトであるコンピューター名を格納するように指定できます。 ソース レポートを実行すると、データの各行の左側にリンク アイコンが表示されます。 任意の行のアイコンをクリックすると、その行の指定された列にある値が、ターゲット レポートを表示するために必要なプロンプト値として渡されます。 レポートの構成に使用できるリンクは 1 つのみで、そのリンクは 1 つの対象リソースのみに接続可能です。  

> [!WARNING]  
>  ターゲット レポートを別のレポート フォルダーに移動すると、ターゲット レポートの場所が変更されます。 ソース レポートのレポート リンクは自動的に新しい場所に更新されず、レポート リンクはソース レポート内では動作しなくなります。  

##  <a name="BKMK_ReportFolders"></a> レポート フォルダー  
 System Center Configuration Manager のレポート フォルダーは、Reporting Services に格納されているレポートを並べ替えてフィルターする手段を提供します。 管理するレポートが多くある場合、レポート フォルダーは特に便利です。 レポート サービス ポイントをインストールすると、レポートが Reporting Services にコピーされ、50 以上のレポート フォルダーに整理されます。 レポート フォルダーは読み取り専用です。 Configuration Manager コンソールで変更することはできません。  

##  <a name="BKMK_ReportSubscriptions"></a> レポートのサブスクリプション  
 Reporting Services のレポートのサブスクリプションは、サブスクリプションで指定するアプリケーション ファイル形式のレポートの定期配信またはイベントへの応答としての配信を求める定期要求です。 サブスクリプションは、オンデマンド レポート実行の代替手段となります。 オンデマンド レポートでは、レポートを表示するたびに手動でレポートを選択しなければなりません。 これと対照的に、サブスクリプションはスケジュールを設定して自動的にレポートを配信できます。  

 レポートのサブスクリプションは、Configuration Manager コンソールで管理できます。 レポート サーバーでその処理が行われます。 サブスクリプションの配信には、サーバーに展開される配信拡張機能が使用されます。 既定では、共有フォルダーまたは電子メール アドレスにレポートを送信するサブスクリプションを作成できます。 レポート サブスクリプションの管理の詳細については、「[System Center Configuration Manager でのレポートの操作とメンテナンス](operations-and-maintenance-for-reporting.md)」を参照してください。  

##  <a name="BKMK_ReportBuilder"></a> レポート ビルダー  
 Configuration Manager では、モデルベースのレポートと SQL ベースのレポートの両方を対象に、Microsoft SQL Server Reporting Services レポート ビルダーが専用のオーサリングおよび編集ツールとして使用されます。 Configuration Manager コンソールでレポートの作成操作または編集操作を開始すると、レポート ビルダーが開きます。 レポートの初回作成時または変更時に、レポート ビルダーが自動的にインストールされます。 レポートを実行または編集すると、インストールされているバージョンの SQL Server と関連付けられたバージョンの Report Builder が開きます。  

 レポート ビルダーのインストールにより、20 言語のサポートが追加されます。 レポート ビルダーを実行すると、ローカル コンピューターで実行中のオペレーティング システムの言語でデータが表示されます。 レポート ビルダーがその言語をサポートしない場合は、データは英語で表示されます。 レポート ビルダーは SQL Server 2008 Reporting Services の全機能をサポートします。以下の機能が含まれます。  

-   Microsoft Office のような外観の直観的なレポート オーサリング環境  

-   SQL Server 2008 レポート定義言語 (RDL) の柔軟なレポート レイアウト  

-   チャートやゲージなど多様なデータ表示形式  

-   リッチ形式のテキスト ボックス  

-   Microsoft Word 形式のエクスポート  

 レポート ビルダーは、SQL Server Reporting Services から開くこともできます。  

##  <a name="BKMK_ReportModels"></a> SQL Server Reporting Services のレポート モデル  
 Configuration Manager の SQL Reporting Services では、レポート モデルを使用することで、管理ユーザーがモデルベースのレポートに含める項目をデータベースから容易に選択することができます。 レポートを構築する管理ユーザーには、レポート モデルで指定したビューと項目のみが選択用に表示されます。 モデルベースのレポートを作成するには、少なくとも 1 つのレポート モデルが必要です。 レポート モデルには、次の特長があります。  

-   データベースのフィールドとビューに論理的な事業名を設定し、レポート生成を効率化することができます。 レポートを生成するには、データベース構造に関する知識は必要ありません。  

-   項目は論理的にグループ化できます。  

-   項目間のリレーションシップ  

-   モデルの要素にセキュリティ保護を適用することで、管理ユーザーが表示のアクセス許可を持っているデータのみが表示されるように管理できます。  

 Configuration Manager にはレポート モデルのサンプルが用意されていますが、それぞれの業務要件に適したレポート モデルを定義することもできます。 レポート モデルの作成方法の詳細については、「[SQL Server Reporting Services での System Center Configuration Manager のカスタム レポート モデルの作成](creating-custom-report-models-in-sql-server-reporting-services.md)」を参照してください。  

## <a name="next-steps"></a>次のステップ
[レポートの計画](planning-for-reporting.md)

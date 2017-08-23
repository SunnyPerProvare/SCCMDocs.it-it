---
title: "クライアント管理の基礎 | Microsoft Docs"
description: "System Center Configuration Manager クライアントを管理するために実行するタスクについて説明します。"
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8d4e5641-354e-4439-8b4f-620a760e233d
caps.latest.revision: "4"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0fee4f4ba462e59859ac93c4218b67cb26bdd6f6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="fundamentals-of-client-management-tasks-for-system-center-configuration-manager"></a>System Center Configuration Manager のクライアント管理タスクの基礎

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager クライアントをインストールした後、クライアントを管理するために実行するタスクがいくつかあります。  一部のタスクは、Configuration Manager コンソールから実行されます。 それ以外のタスクは、Configuration Manager クライアント アプリケーションから実行されます。 Configuration Manager クライアント アプリケーションは、Configuration Manager クライアント ソフトウェアと共にインストールされます。

## <a name="configuration-manager-console-tasks"></a>Configuration Manager コンソールのタスク
 Configuration Manager コンソールでは、次のようなさまざまなクライアント管理タスクを実行できます。  

-   アプリケーション、ソフトウェア更新プログラム、メンテナンス スクリプト、およびオペレーティング システムの展開。 特定の日時にインストールするように構成したり、ユーザーが要求したときにソフトウェアをインストールできるようにしたり、アプリケーションをアンインストールするように構成したりする。  

-   マルウェアおよびセキュリティの脅威からコンピューターを保護し、問題が検出されたときに通知を出力する。  

-   コンプライアンスに準拠しているかどうかを監視して修復するためのクライアントの構成設定を定義する。  

-   ハードウェアおよびソフトウェアのインベントリ情報の収集。これには、Microsoft のライセンス情報の監視および調整が含まれます。  

-   リモート コントロールを使用してコンピューターをトラブルシューティングします。  

-   コンピューターの電力消費を管理および監視するための電源管理設定の実装。  

Configuration Manager コンソールでは、ほぼリアルタイムで前のタスクを監視します。 各タスクの通知と状態情報は、Configuration Manager コンソールで使用できます。 データおよび過去の傾向を取得するには、SQL Server Reporting Services の統合レポート機能を使用します。 クライアントは、クライアントのステータスとしての詳細をサイトに送信します。  クライアント ステータス情報では、クライアントとクライアント アクティビティの正常性に関するデータが提供されます。これらのデータはコンソールで、または Configuration Manager の組み込みレポートを使用して表示できます。 このデータを使用すると、応答していないコンピューターを識別できます。また、問題が自動的に修復されることもあります。  

 クライアントの管理タスクに関する詳細については、「[System Center Configuration Manager でクライアントを管理する方法](../../core/clients/manage/manage-clients.md)」および「[System Center Configuration Manager で Linux および UNIX サーバーのクライアントを管理する方法](../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md)」を参照してください。 レポートの使用の詳細については、   
            「[System Center Configuration Manager のレポートの概要](../../core/servers/manage/introduction-to-reporting.md)」を参照してください。  

## <a name="configuration-manager-client-application"></a>Configuration Manager クライアント アプリケーション  
 Configuration Manager クライアント ソフトウェアをインストールすると、Configuration Manager クライアント アプリケーションもインストールされます。 ソフトウェア センターとは異なり、Configuration Manager クライアント アプリケーションはエンドユーザーではなく、ヘルプ デスク用に設計されています。 一部の構成オプションにはローカルの管理アクセス許可が必要であり、ほとんどのオプションには Configuration Manager クライアント アプリケーションの機能についての技術的な知識が必要です。 このアプリケーションを使用すると、クライアントで次のタスクを実行できます。  

-   クライアントに関するプロパティ (ビルド番号、割り当てられているサイト、通信する管理ポイント、およびクライアントが公開キー基盤 (PKI) 証明書と自己署名入り証明書のどちらを使用するかなど) を表示する。  

-   クライアントの初回インストール後に、クライアントでクライアント ポリシーが正常にダウンロードされたかどうかを確認する。 また、Configuration Manager コンソールで構成されているクライアント設定に従って、予期したとおりにクライアント設定が有効または無効になっているかどうかを確認します。  

-   クライアント アクションを開始する。 たとえば、Configuration Manager コンソールで最近構成の変更が行われ、次のスケジュール時間まで待機しない場合に、クライアント ポリシーをダウンロードします。  

-   手動で Configuration Manager サイトにクライアントを割り当てる、またはサイトの検索を試みる。 その後、DNS (ドメイン ネーム システム) に発行する、管理ポイントの DNS サフィックスを指定します。  

-   ファイルを一時的に格納するクライアント キャッシュを構成する。 ソフトウェアをインストールするためにさらにディスク容量が必要な場合は、キャッシュ内のファイルを削除します。  

-   インターネット ベースのクライアント管理のための設定の構成  

-   クライアントに展開されている構成基準の表示、コンプライアンスの評価の開始、およびコンプライアンス レポートの表示。  

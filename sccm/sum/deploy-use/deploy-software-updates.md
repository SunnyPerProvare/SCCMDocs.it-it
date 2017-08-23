---
title: "ソフトウェア更新プログラムの展開 | Microsoft Docs"
description: "Configuration Manager コンソールでソフトウェア更新プログラムを選択し、展開プロセスを手動で開始するか、更新プログラムを自動的に展開します。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
ms.openlocfilehash: 70a0ad1da03a7ca88df206fec683ab1df2b531e1
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
#  <a name="BKMK_SUMDeploy"></a> ソフトウェアの更新を展開する  

*適用対象: System Center Configuration Manager (Current Branch)*

ソフトウェア更新プログラムの展開フェーズは、ソフトウェア更新プログラムを展開するプロセスです。 ソフトウェア更新プログラムの展開方法にかかわらず、更新プログラムは通常、ソフトウェア更新プログラム グループに追加され、ソフトウェア更新プログラムは配布ポイントにダウンロードされ、更新プログラム グループはクライアントに展開されます。 展開を作成すると、関連するソフトウェア更新プログラム ポリシーがクライアント コンピューターに送信され、ソフトウェア更新プログラムのコンテンツ ファイルが配布ポイントからクライアント コンピューターのローカル キャッシュにダウンロードされて、ソフトウェア更新プログラムがクライアントでインストールに使用できるようになります。 インターネットに接続されているクライアントは、Microsoft Update からコンテンツをダウンロードします。  

> [!NOTE]  
>  イントラネットのクライアントで、配布ポイントを利用できない場合に、Microsoft Update からのソフトウェア更新プログラムのダウンロードを構成できます。  

> [!NOTE]  
>  他の種類の展開とは異なり、すべてのソフトウェア更新プログラムは、クライアントの最大キャッシュ サイズの設定に関係なく、クライアント キャッシュにダウンロードされます。 クライアント キャッシュ設定の詳細については、「 [Configure the Client Cache for Configuration Manager Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache)」を参照してください。  

必要なソフトウェア更新プログラムの展開を構成すると、ソフトウェア更新プログラムは、スケジュールされた期限に自動的にインストールされます。 または、クライアント コンピューターのユーザーが、期限前にソフトウェア更新プログラムのインストールをスケジュール設定または開始できます。 指定したインストール後、ソフトウェア更新プログラムのインストールが正常に完了したかどうかを報告する状態メッセージがクライアント コンピューターからサイト サーバーに送信されます。 ソフトウェア更新プログラムの展開の詳細については、「 [Software update deployment workflows](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows)」を参照してください。  

ソフトウェ更新プログラムを展開するための主なシナリオには、手動展開と自動展開の 2 つがあります。 通常は、最初にソフトウェア更新プログラムを手動で展開してクライアント コンピューター用の基準を作成してから、自動展開を使用してクライアントでソフトウェア更新プログラムを管理します。  

## <a name="BKMK_ManualDeployment"></a> ソフトウェア更新プログラムの手動展開
Configuration Manager コンソールでソフトウェア更新プログラムを選択し、展開プロセスを手動で開始することができます。 継続的な月ごとのソフトウェア更新プログラムの展開を管理する自動展開規則を作成する前に、必要なソフトウェア更新プログラムでクライアントを最新の状態にする場合と、帯域外のソフトウェア更新プログラム要件を展開する場合は、通常、この展開方法を使用します。 次の一覧に、ソフトウェア更新プログラムの手動展開の一般的なワークフローを示します。  

1. 特定の要件を使用するソフトウェア更新プログラムをフィルター処理します。 たとえば、50 を超えるクライアント コンピューターで必要なすべてのセキュリティまたは重要なソフトウェア更新プログラムを取得する条件を指定できます。  
2. ソフトウェア更新プログラムを格納するソフトウェア更新プログラム グループを作成します。  
3. ソフトウェア更新プログラム グループにソフトウェア更新プログラムのコンテンツをダウンロードします。  
4. 手動でソフトウェア更新プログラム グループを展開します。

詳細な手順については、「[ソフトウェア更新プログラムの手動展開](manually-deploy-software-updates.md)」をご覧ください。

## <a name="automatically-deploy-software-updates"></a>ソフトウェア更新プログラムの自動展開
ソフトウェア更新プログラムの自動展開は自動展開規則 (ADR) を使用して構成します。 月ごとのソフトウェア更新プログラム (一般的に "月例パッチ" として知られています) と、定義の更新の管理には、通常、この展開方法が使用されます。 ルールの実行時、ソフトウェア更新プログラムがソフトウェア更新プログラム グループから削除され (既存の更新プログラム グループを使用している場合)、指定した基準 (たとえば、先月リリースされたすべてのセキュリティ ソフトウェア更新プログラム) を満たすソフトウェア更新プログラムがソフトウェア更新プログラム グループに追加され、ソフトウェア更新プログラムのコンテンツ ファイルがダウンロードされ、配布ポイントにコピーされ、ソフトウェア更新プログラムがターゲット コレクションのクライアントに展開されます。 次の一覧に、ソフトウェア更新プログラムの自動展開の一般的なワークフローを示します。  

1.  展開設定を指定する ADR を作成します。
2.  ソフトウェア更新プログラムがソフトウェア更新プログラム グループに追加されます。  
3.  ソフトウェア更新プログラム グループは、ターゲット コレクションが指定されている場合、そのターゲット コレクションのクライアント コンピューターに展開されます。  

環境で使用する展開戦略を決定する必要があります。 たとえば、ADR を作成して、テスト用クライアントのコレクションをターゲットにします。 ソフトウェア更新プログラムがテスト グループにインストールされることを確認した後で、規則に新しい展開を追加したり、この既存の展開規則に指定したコレクションを、さらに多くのクライアントが含まれるターゲット コレクションに変更したりすることができます。 ADR で作成されるソフトウェア更新プログラムのオブジェクトは双方向です。  

-   ADR を使用して展開されたソフトウェア更新プログラムは、ターゲット コレクションに追加された新しいクライアントに自動的に展開されます。  
-   ソフトウェア更新プログラム グループに追加された新しいソフトウェア更新プログラムは、ターゲット コレクションのクライアントに自動的に展開されます。  
-   ADR では、展開をいつでも有効または無効にできます。  

ADR を作成した後、ルールにさらに他の展開を追加できます。 これにより、コレクションごとに異なる更新プログラムを展開する複雑さが軽減されます。 それぞれの新しい展開がさまざまな機能と展開監視エクスペリエンスを備え、追加するそれぞれの新しい展開には次の機能があります。  

-   ADR を初めて実行したときに作成されたものと同じ更新グループとパッケージを使用します。  
-   別のコレクションを指定することができます。  
-   次のような独自の展開プロパティをサポートします。  
   -   アクティベーション時間  
   -   期限  
   -   エンド ユーザー エクスペリエンスの表示/非表示  
   -   この展開の個別のアラート  

詳細な手順については、「[ソフトウェア更新プログラムの自動展開](automatically-deploy-software-updates.md)」をご覧ください。

<!-- ###  <a name="BKMK_ClientCache"></a> Client cache setting  
The Configuration Manager client downloads the content for required software updates to the local client cache soon after it receives the deployment. However, the client waits to download the content until after the **Software available time** setting for the deployment. The client does not download software updates in optional deployments (deployments that do not have a scheduled installation deadline) until the user manually starts the installation. When the configured deadline passes, the software updates client agent performs a scan to verify that the software update is still required, then the software updates client agent checks the local cache on the client computer to verify that the software update source file is still available, and then installs the software update. If the content was deleted from the client cache to make room for another deployment, the client downloads the software updates to the cache. Software updates are always downloaded to the client cache regardless of the configured maximum client cache size. For other deployments, such as applications or packages, the client only downloads content that is within the maximum cache size that you configure for the client. Cached content is not automatically deleted, but it remains in the cache for at least one day after the client used that content.  -->


 <!-- For more information about the deployment process, see [Software update deployment process](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).  -->

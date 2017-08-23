---
title: "ソフトウェア更新プログラムのベスト プラクティス | Microsoft Docs"
description: "System Center Configuration Manager でのソフトウェア更新プログラムのベスト プラクティスを使用します。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 6d20389a-9de2-4a64-bced-9fc4fa519174
ms.openlocfilehash: 5df20f3703442de1be6220ca2770e182e330c036
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="best-practices-for-software-updates-in-system-center-configuration-manager"></a>System Center Configuration Manager でのソフトウェア更新プログラムについて推奨する運用方法

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックには、System Center Configuration Manager でのソフトウェア更新プログラムのベスト プラクティスが含まれています。 また、最初のインストール時のベスト プラクティスと、運用時のベスト プラクティスに分けて説明しています。  

## <a name="installation-best-practices"></a>インストールについて推奨する運用方法  
 Configuration Manager にソフトウェア更新プログラムをインストールするときには、次のベスト プラクティスを使用してください。  

### <a name="use-a-shared-wsus-database-for-software-update-points"></a>ソフトウェアの更新ポイント用に共有 WSUS データベースを使用する  
 プライマリ サイトに複数のソフトウェアの更新ポイントをインストールする場合、同じ Active Directory フォレストの各ソフトウェアの更新ポイントで、同じ WSUS データベースを使用します。 クライアントが新しいソフトウェアの更新ポイントに切り替えるときに、クライアントとネットワークのパフォーマンスが低下する可能性がありますが、同じデータベースを共有することで、その影響を大幅に軽減できます。 クライアントが、古いソフトウェアの更新ポイントとデータベースを共有する新しいソフトウェアの更新ポイントに切り替えた場合でも、差分スキャンは発生しますが、WSUS サーバーに専用のデータベースがある場合よりも、差分スキャンのサイズは大幅に小さくなります。  

> [!IMPORTANT]  
>  また、ソフトウェアの更新ポイントに共有の WSUS データベースを使用する場合は、ローカルの WSUS コンテンツ フォルダーを共有する必要があります。  

 ソフトウェアの更新ポイントを切り替える際の詳細については、「[Plan for software updates in System Center Configuration Manager](../../sum/plan-design/plan-for-software-updates.md)」(System Center Configuration Manager でのソフトウェア更新プログラムの計画) トピックの「[Software update point switching](../../sum/plan-design/plan-for-software-updates.md#BKMK_SUPSwitching)」(ソフトウェアの更新ポイントの切り替え) セクションを参照してください。  

### <a name="when-configuration-manager-and-wsus-use-the-same-sql-server-configure-one-of-these-to-use-a-named-instance-and-the-other-to-use-the-default-instance-of-sql-server"></a>Configuration Manager と WSUS が同じ SQL Server を使用する場合は、一方は名前付きインスタンスを使用し、もう一方は SQL Server の規定のインスタンスを使用するように構成してください。  
 Configuration Manager と WSUS のデータベースが同じ SQL Server を使用し、SQL Server の同じインスタンスを共有する場合は、この 2 つのアプリケーション間のリソースの使用状況を容易に判別できなくなります。 Configuration Manager と WSUS に異なる SQL Server インスタンスを使用すると、それぞれのアプリケーションで発生する可能性のあるリソース使用の問題のトラブルシューティングおよび診断が容易になります。  

### <a name="specify-the-store-updates-locally-setting-for-the-wsus-installation"></a>WSUS インストールで [更新プログラムをローカルに保存する] 設定をオンにする  
 WSUS をインストールするときに、**[更新プログラムをローカルに保存する]** 設定をオンにします。 この設定をオンにすると、同期プロセス時にソフトウェア更新プログラムに関連付けられたライセンス条項がダウンロードされ、WSUS サーバーのローカル ハード ドライブに保存されます。 この設定を選択しないと、クライアント コンピューターがライセンス条項が含まれる更新プログラムでのソフトウェア更新プログラム対応のスキャンに失敗することがあります。 ソフトウェアの更新のポイントをインストールすると、WSUS 同期マネージャーが、規定では 60 分ごとにこの設定が有効になっているかを確認します。  

## <a name="operational-best-practices"></a>操作について推奨する運用方法  
 ソフトウェア更新プログラムを使用するときには、次の推奨する運用方法を使用してください。  

### <a name="limit-software-updates-to-1000-in-a-single-software-update-deployment"></a>単一のソフトウェア更新プログラムの展開を 1000 までに制限する  
 ソフトウェア更新プログラムの展開ごとのソフトウェア更新プログラムの数を 1000 以下にする必要があります。 自動展開規則を作成したときに、指定した条件でソフトウェア更新プログラムが 1000 以内になるかご確認ください。 ソフトウェア更新プログラムを手動で展開する場合は、1000 を超える更新プログラムを展開対象として選択しないでください。  

### <a name="create-a-new-software-update-group-each-time-an-automatic-deployment-rule-runs-for-patch-tuesday-and-for-general-deployment"></a>"Patch Tuesday" (月例パッチ) および一般の展開による自動展開規則の実行ごとのソフトウェア更新プログラム グループの新規作成  
 ソフトウェアの更新展開ではソフトウェア更新プログラムに 1000 の制限があります。 自動展開規則を作成するときに、既存の更新グループを使用するか、規則が実行されるたびに更新グループを新しく作成するかを指定します。 自動展開規則で、複数のソフトウェア更新プログラムが該当する条件を指定し、その規則を定期的に実行する場合、規則を実行するたびに新しいソフトウェア更新プログラム グループを作成するように指定します。 こうすることで、1 回の展開でソフトウェア更新プログラムが 1,000 の制限を超えないようにすることができます。  

### <a name="use-an-existing-software-update-group-for-automatic-deployment-rules-for-endpoint-protection-definition-updates"></a>Endpoint Protection の定義ファイルの更新用自動展開規則での既存のソフトウェア更新プログラム グループの使用  
 頻繁に Endpoint Protection の定義ファイルの更新を展開する自動展開規則を使用する場合は、既存のソフトウェア更新プログラム グループを常に使用してください。 そうしないと、時間の経過とともに、多くのソフトウェア更新プログラム グループが作成される可能性があります。 通常、定義ファイルの更新の発行元は、定義ファイルの更新がより新しい 4 件の更新で置き換えられると期限切れになるように設定します。 そのため、自動展開規則によって作成されたソフトウェア更新プログラム グループには、発行元に対して 4 件 (1 件がアクティブ、3 件が置き換え済み) を超える定義更新が含まれることはありません。  

## <a name="see-also"></a>関連項目  
 [System Center Configuration Manager でのソフトウェア更新プログラムの計画](../../sum/plan-design/plan-for-software-updates.md)

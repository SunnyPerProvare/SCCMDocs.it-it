---
title: "電子メール、Wi-Fi、VPN のプロファイルの監視 | Microsoft Docs"
description: "電子メール、Wi-Fi、VPN のプロファイルのコンプライアンス ステータスを System Center Configuration Manager で監視する方法を説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2315b8b-98bc-40e1-8ef9-bfb5e69ab109
caps.latest.revision: "4"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 73d941633d270cf9628f8be14e1e56f3c78624b6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-email-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager での電子メール、Wi-Fi、VPN のプロファイルの監視

*適用対象: System Center Configuration Manager (Current Branch)*

階層内のユーザーに System Center Configuration Manager の電子メール、Wi-Fi、VPN のプロファイルを展開した後は、以下の手順に従って、プロファイルのコンプライアンス ステータスを監視できます。  

-   [Configuration Manager コンソールでコンプライアンス評価結果を表示する方法](#BKMK_console)  

-   [レポートを使用してコンプライアンス評価結果を表示する方法](#BKMK_Reports)  

##  <a name="BKMK_console"></a> Configuration Manager コンソールでコンプライアンス評価結果を表示する方法  
 System Center Configuration Manager コンソールで、展開したプロファイルのコンプライアンスの詳細を表示するには、この手順に従います。  

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Configuration Manager コンソールでコンプライアンス結果を表示するには  

1.  System Center Configuration Manager コンソールで、**[監視]** をクリックします。  

2.  [監視] **** ワークスペースで、[展開] ****をクリックします。  

3.  **[展開]** の一覧で、コンプライアンス情報を確認するプロファイルの展開を選択します。  

4.  メイン ページで、プロファイルの展開のコンプライアンスに関する概要情報を確認できます。 詳細情報を表示するには、プロファイルの展開を選択してから、**[ホーム]** タブの **[展開]** グループで **[ステータスの表示]** をクリックして、**[展開ステータス]** ページを開きます。  

     [展開のステータス] **** ページには次のタブがあります。  

    -   **対応:** 影響を受けた資産の数に基づいて、プロファイルのコンプライアンスが表示されます。 規則をダブルクリックして、[資産とコンプライアンス **** ] ワークスペースの [ユーザー **** ] ノードに、このプロファイルに対応しているすべてのユーザーが含まれた一時ノードを作成できます。 **[資産の詳細]** ウィンドウに、このプロファイルに対応しているユーザーが表示されます。 詳細情報を表示するには、一覧内のユーザーをダブルクリックします。  

        > [!IMPORTANT]  
        >  プロファイルをクライアント デバイスに適用できない場合は評価されませんが、対応しているという結果が返されます。  

    -   **エラー:** 選択したプロファイルの展開で発生したすべてのエラーの一覧が、影響を受けた資産の数に基づいて表示されます。 規則をダブルクリックして、[資産とコンプライアンス **** ] ワークスペースの [ユーザー **** ] ノードに、このプロファイルでエラーが生成されたすべてのユーザーが含まれた一時ノードを作成できます。 ユーザーを選択すると、[資産の詳細 **** ] ウィンドウに、選択した問題に影響を受けているユーザーが表示されます。 問題の詳細情報を表示するには、一覧内のユーザーをダブルクリックします。  

    -   **非対応:** プロファイルにある非対応の規則とその影響を受けた資産の数の一覧が表示されます。 規則をダブルクリックして、[ **資産とコンプライアンス** ] ワークスペースの [ **ユーザー** ] ノードに一時ノードを作成できます。このノードには、このプロファイルに対応していないすべてのユーザーを含めます。 ユーザーを選択すると、[資産の詳細 **** ] ウィンドウに、選択した問題に影響を受けているユーザーが表示されます。 問題の詳細情報を表示するには、一覧内のユーザーをダブルクリックします。  

    -   **不明:** 選択したプロファイルの展開でコンプライアンスがレポートされなかったすべてのユーザーの一覧が、デバイスの現在のクライアント ステータスと共に表示されます。  

5.  **[展開ステータス]** ページでは、展開したプロファイルのコンプライアンスの詳細情報を確認できます。 [展開] **** ノードの下に一時ノードが作成されるため、後から再度この情報をすばやく確認できます。  

##  <a name="BKMK_Reports"></a> レポートを使用してコンプライアンス評価結果を表示する方法  
 System Center Configuration Manager のプロファイルを含むコンプライアンス設定には、プロファイルの情報を監視するのに便利なレポートが多数組み込まれています。 これらのレポートには、[コンプライアンスおよび設定管理] ****のカテゴリがあります。  

> [!IMPORTANT]  
>  コンプライアンス設定でレポートの [デバイス フィルター **** ] と [ユーザー フィルター **** ] パラメーターを指定するときは、必ず、ワイルドカード (%) 文字を使ってください。  

 System Center Configuration Manager でのレポートの構成方法に関して詳しくは、「[System Center Configuration Manager のレポート](../../core/servers/manage/reporting.md)」を参照してください。  

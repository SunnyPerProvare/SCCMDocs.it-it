---
title: "リモート コントロール使用状況の監査 | Microsoft Docs"
description: "System Center Configuration Manager でリモート コントロール使用状況を監査します。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c975e69-0cc0-4afd-b7fb-b7182162a933
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 4259ecfca48ccdffa83247e9ab5a65b3f006c5d9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-audit-remote-control-usage-in-system-center-configuration-manager"></a>System Center Configuration Manager でリモート コントロール使用状況を監査する方法

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のレポートを使用して、リモート コントロールの監査情報を表示することができます。  

 Configuration Manager でのレポートの構成方法に関して詳しくは、「[System Center Configuration Manager のレポート](../../../../core/servers/manage/reporting.md)」をご覧ください。  

 [ **ステータス メッセージ - 監査** ] のカテゴリでは次の 2 つのレポートが使用できます。  

-   **リモート コントロール - 特定のユーザーによりリモートで制御されるコンピューターすべて** – 特定のユーザーが開始したリモート コントロール操作の概要が表示されます。  

-   **リモート コントロール - リモート コントロール情報すべて** – クライアント コンピューターのリモート コントロールに関するステータス メッセージの概要が表示されます。  

### <a name="to-run-the-report-remote-control---all-computers-remote-controlled-by-a-specific-user"></a>[リモート コントロール - 特定のユーザーによりリモートで制御されるコンピューターすべて] レポートを実行するには  

1.  Configuration Manager コンソールで、[ **監視** ] をクリックします。  

2.  [ **監視** ] ワークスペースで、[ **レポート**] を展開し、[ **レポート**] をクリックします。  

3.  **レポート** ノードをクリックして、 **カテゴリ** レポートを並べ替え、カテゴリのレポートをより簡単に見つけられるように列 **ステータス メッセージ - 監査**です。  

4.  レポートを選択して **リモート_コントロール - 特定のユーザーによって制御されるすべてのリモートのコンピューター**, 、、 **ホーム**  タブで、 **レポート グループ**, 、 をクリックして **実行**です。  

5.  **ユーザー名** の一覧、 **リモート_コントロール - 特定のユーザーによって制御されるすべてのリモートのコンピューター**, 、クリックして、監査情報をレポートするユーザー指定 **レポートの表示**です。  

6.  レポートのデータの確認が終わったら、レポート ウィンドウを閉じます。  

### <a name="to-run-the-report-remote-control---all-remote-control-information"></a>[リモート コントロール - リモート コントロール情報すべて] レポートを実行するには  

1.  Configuration Manager コンソールで、[ **監視** ] をクリックします。  

2.  [ **監視** ] ワークスペースで、[ **レポート**] を展開し、[ **レポート**] をクリックします。  

3.  **[レポート]** ノードで、 **[カテゴリ]** 列をクリックしてレポートを並べ替え、 **[ステータス メッセージ - 監査]**カテゴリのレポートを簡単に見つけられるようにします。  

4.  レポートを選択 **リモート_コントロール - リモート_コントロール情報すべて**, 、、 **ホーム**  タブで、 **レポート グループ**, 、 をクリックして **実行** を開くには、 **リモート_コントロール - リモート_コントロール情報すべて** ウィンドウです。  

5.  レポートのデータの確認が終わったら、レポート ウィンドウを閉じます。  

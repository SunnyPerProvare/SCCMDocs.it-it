---
title: "移行監視 | Microsoft Docs"
description: "Configuration Manager コンソールを使用して、移行ジョブの進行状況と成功を監視する方法について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc731d3f-edd7-4049-b17b-653d6693a564
caps.latest.revision: "4"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 896807ec2c4be2835094a27add59d4cc09e93add
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="planning-to-monitor-migration-activity-in-system-center-configuration-manager"></a>System Center Configuration Manager での移行アクティビティの監視の計画

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager では、移行先階層に接続している Configuration Manager コンソールで移行を監視できます。 Configuration Manager コンソールの **[管理]** ワークスペースの **[移行]** ノードから、移行ジョブの進行状況と成功状態を監視できます。 移行済みオブジェクトが示されている各移行ジョブ、移行前のオブジェクト、および移行ジョブから除外されているオブジェクトの数に関する概要情報を表示できます。 また、移行で問題が生じた場合はその詳細も表示されます。  

## <a name="view-migration-progress"></a>移行の進行状況の表示  
 移行ジョブの進行状況を表示するには、次の操作のいずれかを実行します。  

-   Configuration Manager コンソールの **[管理]** ワークスペースで、**[移行ジョブ]** ノードを展開し、移行ジョブを選択してから、**[ジョブ内のオブジェクト]** タブをクリックします。  

-   移行の進行状況を確認したり問題を特定したりするには、Configuration Manager ログ ファイルを使用します。 移行マネージャーは、移行操作を追跡管理し、サイト サーバー上の **\&lt;InstallationPath\>\\LOGS** フォルダー内の migmctrl.log ファイルにそのデータを記録する Configuration Manage プロセスです。  

    > [!NOTE]  
    >  移行ジョブに失敗した場合は、直ちに migmctrl.log ファイルで詳細を確認してください。 移行ログのエントリは、継続的にファイルに追加され、旧データを上書きします。 エントリが上書きされてしまうと、移行済みのオブジェクトで問題が発生した場合に、それが移行処理の問題に関連するかどうかを特定できなくなることがあります。 移行の構成時に Configuration Manager コンソールが接続するサイトに関係なく、移行アクティビティは階層の最上位サイトで記録されます。\-  

-   Configuration Manager のレポートを使用します。 Configuration Manager では、組み込みの移行用レポートがいくつか提供されています。これらのレポートは、要件に合わせて編集できます。\- Configuration Manager でのレポートの詳細については、「[System Center Configuration Manager のレポート](../../core/servers/manage/reporting.md)」を参照してください。  

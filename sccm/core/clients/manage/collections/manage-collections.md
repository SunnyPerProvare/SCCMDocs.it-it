---
title: "コレクションの管理 | Microsoft Docs"
description: "System Center Configuration Manager で一般的なコレクション管理タスクを実行します。"
ms.custom: na
ms.date: 4/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
caps.latest.revision: "8"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 4d44f98eb0755619cdd2101203a13725186b835b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-manage-collections-in-system-center-configuration-manager"></a>System Center Configuration Manager でコレクションを管理する方法

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager でコレクションの管理タスクを行う際は、このトピックの概要情報を参考にしてください。  

> [!NOTE]  
>  Configuration Manager コレクションを作成する方法については、「[System Center Configuration Manager でコレクションを作成する方法](../../../../core/clients/manage/collections/create-collections.md)」を参照してください。  

## <a name="how-to-manage-device-collections"></a>デバイス コレクションを管理する方法  
 [資産とコンプライアンス] **** ワークスペースで [デバイス コレクション] ****を選択し、管理するコレクションと管理タスクを選択します。  

 次の表で、管理タスクに関する詳細と、各タスクを選択する前に必要となる追加情報について説明します。  

|管理タスク|説明|説明|  
|---------------------|-------------|----------------------|  
|**メンバーの表示**|[デバイス] **** ノードの一時ノードで選択されたコレクションのメンバーであるすべてのリソースを表示します。|詳細情報はありません。|  
|**選択された項目の追加**|次のアクションのいずれかを行うために次のオプションを提供します。<br /><br /> - <br />                    **選択した項目を既存のデバイス コレクションに追加する** - 選択したコレクションのメンバーを追加するコレクションを選択できる **[コレクションの選択]** ダイアログ ボックスを開きます。 [コレクションを含める] **** のメンバーシップ規則を使用すると、選択されたコレクションは、このコレクションに含められます。<br /><br /> - **選択した項目を新しいデバイス コレクションに追加する** - 新しいコレクションを作成できる**デバイス コレクションの作成ウィザード**を開きます。 [コレクションを含める] **** のメンバーシップ規則を使用すると、選択されたコレクションは、このコレクションに含められます。|[System Center Configuration Manager でコレクションを作成する方法](../../../../core/clients/manage/collections/create-collections.md)|  
|**クライアントのインストール**|クライアント プッシュのインストールを使用して、Configuration Manager クライアントを選択したコレクションのすべてのコンピューターにインストールする**クライアントのインストール ウィザード**を開きます。|[Windows コンピューターにクライアントを展開する方法](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)|  
|**アフィニティ要求の管理**|保留中の要求を承認または拒否して選択されたコレクションのデバイスにおけるユーザーとデバイスのアフィニティを確立できる [ユーザーとデバイスのアフィニティ要求の管理] **** ダイアログボックスを開きます。|[System Center Configuration Manager でのユーザーとデバイスのアフィニティへのユーザーとデバイスの関連付け](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)|  
|**必須の PXE 展開の消去**|選択されたコレクションのすべてのメンバーから必要な PXE ブート展開を消去します。|[オペレーティング システムの展開の概要](../../../../osd/understand/introduction-to-operating-system-deployment.md)|  
|**メンバーシップの更新**|選択されたコレクションのメンバーシップを評価します。 多くのメンバーからなるコレクションでは、更新の完了には時間がかかることがあります。 更新が完了したら、[リフレッシュ] **** アクションを使用して、新しいコレクションのメンバーで画面を更新します。|詳細情報はありません。|  
|**リソースの追加**|新しいリソースを検索して選択されたコレクションに追加できる [コレクションへのリソースの追加] **** ダイアログ ボックスを開きます。<br /><br /> 更新中は選択されたコレクションで砂時計のアイコンが表示されます。|詳細情報はありません。|  
|**クライアント通知**|選択したデバイス コレクションのすべてのクライアントがコンピューターまたはユーザー ポリシーをダウンロードするように指定します。|詳細情報はありません。|  
|**Endpoint Protection**|選択されたコレクションで、フルまたはクイックのアンチマルウェア スキャンの実行、または最新のアンチマルウェアの定義をコンピューターにダウンロードをします。|[System Center Configuration Manager での Endpoint Protection](../../../../protect/deploy-use/endpoint-protection.md)|  
|**エクスポート**|別の Configuration Manager サイトでアーカイブまたは使用できる Managed Object Format (MOF) と呼ばれる形式のファイルにコレクションをエクスポートする**コレクションのエクスポート ウィザード** を開きます。<br /><br /> コレクションをエクスポートするとき、コレクションは [含む] **** の規則の使用を通じて選択されたコレクションを参照し、または [除外する] **** の規則についてはエクスポートしません。|詳細情報はありません。|  
|**コピー**|選択したコレクションのコピーを作成します。 新しいコレクションは選択したコレクションを限定コレクションとして使用します。|詳細情報はありません。|  
|**削除**|選択したコレクションを削除します。 コレクションのすべてのリソースをサイト データベースから削除することもできます。<br /><br /> Configuration Manager に構築されたコレクションは削除することができません。|組み込みコレクションの一覧については、「[Configuration Manager でのコレクションの概要](../../../../core/clients/manage/collections/introduction-to-collections.md)」を参照してください。|  
|**展開のシミュレート**|アプリケーションをインストールしたりアンインストールしたりせずにアプリケーションの展開結果をテストできる、アプリケーションのシミュレート ウィザード **** を開きます。|[System Center Configuration Manager でアプリケーションの展開をシミュレーションする方法](../../../../apps/deploy-use/simulate-application-deployments.md)|  
|**デプロイ**|次のオプションを表示します。<br /><br /> - <br />                    **アプリケーション** - 選択したコレクションへのアプリケーションの展開を選択して構成できる、 **ソフトウェアの展開ウィザード** を開きます。<br /><br /> - <br />                    **プログラム** – 選択したコレクションへのパッケージやプログラムの展開を選択して構成できる、 **ソフトウェアの展開ウィザード** を開きます。<br /><br /> - **構成基準** - 選択されたコレクションへの 1 つ以上の構成基準の展開を構成できる **[構成基準の展開]** ダイアログ ボックスを開きます。<br /><br /> - <br />                    **タスク シーケンス** – 選択したコレクションへのタスク シーケンスの展開を選択して構成できる、 **ソフトウェアの展開ウィザード** を開きます。<br /><br /> - <br />                    **ソフトウェア更新プログラム** - 選択したコレクションのリソースへのソフトウェア更新プログラムの展開を構成できる、**ソフトウェア更新の展開ウィザード**を開きます。|[System Center Configuration Manager でアプリケーションを展開する方法](../../../../apps/deploy-use/deploy-applications.md)<br /><br /> [System Center Configuration Manager のパッケージとプログラム](../../../../apps/deploy-use/packages-and-programs.md)<br /><br /> [System Center Configuration Manager で構成基準を展開する方法](../../../../compliance/deploy-use/deploy-configuration-baselines.md)<br /><br /> [System Center Configuration Manager でのタスクを自動化するためのタスク シーケンスの管理](../../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)<br /><br /> [System Center Configuration Manager でのソフトウェア更新プログラムの管理](/sccm/sum/understand/software-updates-introduction)|  

## <a name="how-to-manage-user-collections"></a>ユーザー コレクションを管理する方法  
 [資産とコンプライアンス] **** ワークスペースで [ユーザー コレクション] ****を選択し、管理するコレクションと管理タスクを選択します。  

 次の表で、管理タスクに関する詳細と、各タスクを選択する前に必要となる追加情報について説明します。  

|管理タスク|説明|説明|  
|---------------------|-------------|----------------------|  
|**メンバーの表示**|[ユーザー] **** ノードの一時ノードで選択されたコレクションのメンバーであるすべてのリソースを表示します。|詳細情報はありません。|  
|**選択された項目の追加**|このオプションでは次のアクションのいずれかが実行できます。<br /><br /> - <br />                    **選択した項目を既存のユーザー コレクションに追加する** - 選択したコレクションのメンバーを追加するコレクションを選択できる **[コレクションの選択]** ダイアログ ボックスを開きます。 [コレクションを含める] **** のメンバーシップ規則を使用すると、選択されたコレクションは、このコレクションに含められます。<br /><br /> - **選択した項目を新しいユーザー コレクションに追加する** - 新しいコレクションを作成できる、**ユーザー コレクションの作成ウィザード**を開きます。 [コレクションを含める] **** のメンバーシップ規則を使用すると、選択されたコレクションは、このコレクションに含められます。|[System Center Configuration Manager でコレクションを作成する方法](../../../../core/clients/manage/collections/create-collections.md)|  
|**アフィニティ要求の管理**|保留中の要求を承認または拒否して選択されたコレクションのユーザーにおけるユーザーとデバイスのアフィニティを確立できる [ユーザーとデバイスのアフィニティ要求の管理] **** ダイアログ ボックスを開きます。|[System Center Configuration Manager でのユーザーとデバイスのアフィニティへのユーザーとデバイスの関連付け](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)|  
|**メンバーシップの更新**|選択されたコレクションのメンバーシップを評価します。 多くのメンバーからなるコレクションでは、更新の完了には時間がかかることがあります。 更新が完了したら、[リフレッシュ] **** アクションを使用して、新しいコレクションのメンバーで画面を更新します。<br /><br /> 更新中は選択されたコレクションで砂時計のアイコンが表示されます。|詳細情報はありません。|  
|**リソースの追加**|新しいリソースを検索して選択されたコレクションに追加できる [コレクションへのリソースの追加] **** ダイアログ ボックスを開きます。|詳細情報はありません。|  
|**エクスポート**|別の Configuration Manager サイトでアーカイブまたは使用できる Managed Object Format (MOF) と呼ばれる形式のファイルにコレクションをエクスポートする**コレクションのエクスポート ウィザード** を開きます。<br /><br /> コレクションをエクスポートするとき、コレクションは [含む] **** の規則の使用を通じて選択されたコレクションを参照し、または [除外する] **** の規則についてはエクスポートしません。|詳細情報はありません。|  
|**コピー**|選択したコレクションのコピーを作成します。 新しいコレクションは選択したコレクションを限定コレクションとして使用します。|詳細情報はありません。|  
|**削除**|選択したコレクションを削除します。 コレクションのすべてのリソースをサイト データベースから削除することもできます。<br /><br /> Configuration Manager に構築されたコレクションは削除することができません。|組み込みコレクションの一覧については、「[Configuration Manager でのコレクションの概要](../../../../core/clients/manage/collections/introduction-to-collections.md)」を参照してください。|  
|**展開のシミュレート**|アプリケーションをインストールしたりアンインストールしたりせずにアプリケーションの展開結果をテストできる、アプリケーションのシミュレート ウィザード **** を開きます。|[System Center Configuration Manager でアプリケーションの展開をシミュレーションする方法](../../../../apps/deploy-use/simulate-application-deployments.md)|  
|**デプロイ**|次のオプションを表示します。<br /><br /> - **アプリケーション** - 選択したコレクションへのアプリケーションの展開を選択して構成できる、**ソフトウェアの展開ウィザード**を開きます。<br /><br /> - <br />                    **プログラム** – 選択したコレクションへのパッケージやプログラムの展開を選択して構成できる、 **ソフトウェアの展開ウィザード** を開きます。<br /><br /> - **構成基準** - 選択されたコレクションへの 1 つ以上の構成基準の展開を構成できる **[構成基準の展開]** ダイアログ ボックスを開きます。|[System Center Configuration Manager でアプリケーションを展開する方法](../../../../apps/deploy-use/deploy-applications.md)<br /><br /> [System Center Configuration Manager のパッケージとプログラム](../../../../apps/deploy-use/packages-and-programs.md)<br /><br /> [System Center Configuration Manager で構成基準を展開する方法](../../../../compliance/deploy-use/deploy-configuration-baselines.md)|  

##  <a name="BKMK_CollProp"></a> コレクションのプロパティ  
 コレクションの [プロパティ] **** ダイアログ ボックスを開くと、コレクションの次のプロパティを表示し構成することができます。  

|タブ名|説明|  
|--------------|----------------------|  
|**全般**|コレクション名や限定コレクションを含め選択されたコレクションに関する概要を表示し構成することができます。|  
|**メンバーシップの規則**|このコレクションのメンバーシップを定義するメンバーシップ規則を構成することができます。 詳細については、「[Configuration Manager でのコレクションの作成方法](../../../../core/clients/manage/collections/create-collections.md)」を参照してください。|  
|**電源管理**|選択したコレクションのコンピューターに割り当てられた電源管理の計画を構成することができます。 詳細については、「[電源管理の概要](../../../../core/clients/manage/power/introduction-to-power-management.md)」を参照してください。|  
|**展開**|選択されたコレクションのメンバーに展開されたソフトウェアを表示します。|  
|**メンテナンス期間**|選択されたコレクションのメンバーに適用されたメンテナンス期間を表示し構成することができます。 詳細については、「[System Center Configuration Manager のメンテナンス期間の使用方法](../../../../core/clients/manage/collections/use-maintenance-windows.md)」を参照してください。|  
|**コレクション変数**|コレクションに適用され、タスク シーケンスで使用することができる変数を構成します。 組み込みのタスク シーケンス変数の詳細については、「[タスク シーケンス組み込み変数](../../../../osd/understand/task-sequence-built-in-variables.md)」を参照してください。|  
|**配布ポイント グループ**|1 つ以上の配布ポイント グループを選択されたコレクションのメンバーに関連付けることができます。 詳細については、「[System Center Configuration Manager のコンテンツ インフラストラクチャとコンテンツの管理](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。|  
|**セキュリティ**|関連付けられた役割やセキュリティの範囲で選択されたコレクションへの権限を持つ管理者ユーザーを表示します。|  
|**モニター**|クライアント ステータスや Endpoint Protection に関するアラートが生成されたときの設定ができます。 詳細については、「[How to configure client status in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-status.md)」 (System Center Configuration Manager でクライアント ステータスを構成する方法) および「[System Center Configuration Manager で Endpoint Protection を監視する方法](../../../../protect/deploy-use/monitor-endpoint-protection.md)」を参照してください。|  

---
title: "カスタム タスク シーケンスの作成 | Microsoft Docs"
description: "System Center Configuration Manager でカスタム タスク シーケンスを編集して、タスク シーケンスにステップを追加します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
caps.latest.revision: "6"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 03c844084c72fc52806123d9f4c11a410a3ec775
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="create-a-custom-task-sequence-with-system-center-configuration-manager"></a>System Center Configuration Manager のカスタム タスク シーケンスの作成

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager で作成したばかりのカスタム タスク シーケンスにはタスク シーケンス ステップが含まれていません。 作成後にタスク シーケンスを編集し、必要なタスク シーケンス ステップを追加しなければなりません。  

##  <a name="BKMK_CustomTS"></a> カスタム タスク シーケンスの作成  
 カスタム タスク シーケンスを作成するには、次の手順に従います。  

#### <a name="to-create-a-custom-task-sequence"></a>カスタム タスク シーケンスを作成するには  

1.  Configuration Manager コンソールで、[ソフトウェア ライブラリ] ****をクリックします。  

2.  [ **ソフトウェア ライブラリ** ] ワークスペースで [ **オペレーティング システム**] を展開して、[ **タスク シーケンス** ] をクリックします。  

3.  [ホーム **** ] タブの [作成 **** ] グループで [タスク シーケンスの作成 **** ] をクリックして、タスク シーケンスの作成ウィザードを起動します。  

4.  [新しいタスク シーケンスの作成 **** ] ページで [新しいカスタム タスク シーケンスを作成する ****] を選択します。  

5.  [タスク シーケンス情報 **** ] ページで、タスク シーケンスの名前、タスク シーケンスの説明、および使用するタスク シーケンスのオプションのブート イメージを指定して、ウィザードを完了します。  

 タスク シーケンスの作成ウィザードを完了すると、Configuration Manager によってカスタム タスク シーケンスが [**タスク シーケンス**] ノードに追加されます。 これで、タスク シーケンスを編集してタスク シーケンス ステップを追加できるようになります。  

 使用可能なタスク シーケンス ステップの一覧については、「[タスク シーケンスのステップ](../understand/task-sequence-steps.md)」をご覧ください。  

 タスク シーケンスの編集方法について詳しくは、「[タスク シーケンスの編集](manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence)」をご覧ください。  

 タスク シーケンスを使用することが最も多いのはオペレーティング システムの展開のタスクを自動化する場合ですが、カスタム タスク シーケンスはさまざまなタスクを自動化するために作成できます。 詳細については、「[オペレーティング システム以外の展開用タスク シーケンスの作成](create-a-task-sequence-for-non-operating-system-deployments.md)」をご覧ください。  

 ## <a name="next-steps"></a>次のステップ
 [タスク シーケンスの展開](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)

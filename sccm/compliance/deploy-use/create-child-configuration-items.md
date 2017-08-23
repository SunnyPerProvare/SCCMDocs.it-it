---
title: "子構成項目の作成 | Microsoft Docs"
description: "System Center Configuration Manager で子構成項目を作成します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 113984fa-6150-41a1-89ed-d2a83b979732
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 33d4a2d5a09af74e1d76ac9b34a42b749f5bf7ef
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-child-configuration-items-in-system-center-configuration-manager"></a>System Center Configuration Manager で子構成項目を作成する方法

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の子構成項目は構成項目のコピーであり、元の構成項目への関係を保持しています。したがって、子構成項目は親構成項目から元の構成を継承しています。  

Configuration Manager コンソールで子構成項目のプロパティを表示したときに、独自の検証条件を持つ継承されたオブジェクトと設定は編集できません。 ただし、子構成項目に検証条件を追加してから、その検証条件を編集することはできます。また、新しいオブジェクトや設定を子構成項目に追加することもできます。
通常、子構成項目を作成したり編集したりする場合は、元の構成項目をビジネス要件に合わせることが目的になります。  

> [!NOTE]  
>  子構成項目は、種類が **Windows デスクトップおよびサーバー (カスタム)**の構成項目からのみ作成できます。  

## <a name="to-create-a-child-configuration-item"></a>子構成項目を作成するには  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[コンプライアンス設定]** > **[構成項目]** の順にクリックします。  

3.  **構成項目** 一覧で、子構成項目を作成するため、次の構成項目を選択、 **ホーム** ] タブで、 **構成項目** グループで、[ **子構成項目の作成**です。  

4.  **全般** のページ、 **子の構成項目の作成ウィザード**, 、親の特定のバージョンを使用して、子を作成する構成項目を選択できます。 このウィザードのほかの手順は、標準の構成項目を作成する場合に使用する手順と同じです。 詳細については、｢[System Center Configuration Manager クライアントを使用して管理されている Windows デスクトップおよびサーバー コンピューターのカスタム構成項目を作成する方法](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md)｣を参照してください。  

5.  ウィザードを完了します。 新しい子構成項目は、[構成項目] 一覧に表示されます。 ****  

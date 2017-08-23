---
title: "危険度の高い展開の管理 | Microsoft Docs"
description: "管理者が危険度の高い展開を作成した場合に管理者に警告するように System Center Configuration Manager のサイト設定を構成する方法について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 8d37b983-a964-402c-819d-2512ed2d463b
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 8b5564f39f07a67a3c9278379ed59ca415603d21
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="settings-to-manage-high-risk-deployments-for-system-center-configuration-manager"></a>System Center Configuration Manager の危険度の高い展開を管理するための設定

*適用対象: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager では、管理者が危険度の高いタスク シーケンスの展開を作成すると警告が表示されるように、サイトの設定を構成することができます。 危険度の高い展開とは次のようなものです。  

-   自動的にインストールされる展開  

-   望ましくない結果を引き起こす可能性がある展開  

 たとえば、オペレーティング システムを展開する**必須**の目的を持つタスク シーケンスは、高危険度と見なされます。  

 望ましくない危険度の高い展開のリスクを減らすためには、これらの展開検証設定でサイズ制限を構成できます。  

-   **コレクション サイズの制限**: 展開の作成時に、制限より多くのクライアントが含まれているコレクションを非表示にします。  

    -   **既定サイズ**: この設定は、既定では、展開の作成時に、制限より多くのクライアントが含まれているコレクションを非表示にします。 展開の作成時にもこれらのコレクションを表示できますが、既定で非表示になっています。 既定値は 100 です。 この設定を無視する場合は 0 の値を入力します。  

    -   **最大サイズ**: この設定は、展開の作成時に、制限より多くのクライアントが含まれているコレクションを常に非表示にします。 既定値は 0 であり、この設定は無視されます。 **最大サイズ** の値は、 **既定サイズ** の値より大きい必要があります。  

     たとえば、**既定サイズ**を 100、**最大サイズ**を 1000 に設定します。 危険度の高い展開の作成時に、**[コレクションの選択]** ウィンドウには、含まれるクライアント数が 100 未満のコレクションのみが表示されます。 **[メンバー数がサイトの最小サイズ構成を超えるコレクションを非表示にする]** の設定をオフにすると、含まれるクライアント数が 1000 未満のコレクションがウィンドウに表示されます。  

-   **サイト システム サーバーを含むコレクション**: 対象のコレクションにサイト システムの役割を持つコンピューターが含まれている場合は、展開をブロックするか、展開を作成する前に検証が必要になります。 展開がブロックされている場合は、展開の検証条件を満たす別のコレクションを選択する必要があります。  

> [!NOTE]  
>  危険度の高い展開は、常にカスタム コレクション、作成されたコレクション、および組み込みの **不明なコンピューター** コレクションに制限されています。 危険度の高い展開を作成する際、 **すべてのシステム**などの組み込みのコレクションは選択できません。  

### <a name="to-configure-deployment-verification-for-a-site"></a>サイトの展開の検証を構成するには  

1.  Configuration Manager コンソールで、**[管理]** >**[サイトの構成]** > **[サイト]** の順に選択して、構成するプライマリ サイトを選択します。  

2.  **[ホーム]** タブの **[プロパティ]** グループで、**[プロパティ]** を選択して、**[展開の検証]** タブを選択します。  

3.  使用する構成を設定した後は、**[OK]** を選択して構成を保存します。  

### <a name="see-also"></a>関連項目  
 [System Center Configuration Manager のサイトと階層の構成](../../core/servers/deploy/configure/configure-sites-and-hierarchies.md)

---
title: "System Center Configuration Manager での使用条件 | Microsoft Docs"
description: "System Center Configuration Manager のユーザー グループに使用条件ポリシーを展開します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d3f9e6b-4d71-4fc4-9b91-47f1bfbd8c70
caps.latest.revision: "9"
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 20be68496099a67ad2d475067f073da2cef16c86
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="add-terms-and-conditions-with-system-center-configuration-manager"></a>System Center Configuration Manager での使用条件の追加

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の使用条件をユーザー グループに展開すると、デバイスの登録、会社のリソースへのアクセス、会社のポータルの使用によるデバイスとユーザーへの影響を説明できます。 ユーザーは、会社のポータルを使用して登録したり作業にアクセスしたりする前に、使用条件に同意する必要があります。  

 ## <a name="working-with-terms-and-conditions-policies-in-system-center-configuration-manager"></a>System Center Configuration Manager での使用条件ポリシーの扱い  
 複数の使用条件セットを作成および展開できます。 また、同じ使用条件のさまざまな言語のバージョンを作成し、適切なグループに展開することもできます。  

## <a name="to-create-a-terms-and-conditions"></a>使用条件を作成するには  

1.  Configuration Manager コンソールで、 **[資産とコンプライアンス]** > **[概要]** > **[コンプライアンス設定]** > **[使用条件]**と移動します。  

2.  **[使用条件の作成]** をクリックして、新しい使用条件を作成します。  

3.  **[全般]** ページで、以下の情報を指定します。  

    -   **[名前]** - Configuration Manager コンソールに表示される一意の名前  

    -   **[説明]** - Configuration Manager コンソールで使用条件を識別するための詳細  

     **[次へ]**をクリックします。  

4.  **[条件]** ページで、次の情報を指定します。  

    -   **[タイトル]** - 会社のポータルでユーザーに表示されるタイトル  

    -   **[条件に関するテキスト]** - 会社のポータルでユーザーに表示される使用条件  

    -   **[ユーザーによる同意の意味を説明するテキスト]** - ユーザーに表示される同意に関するラベル **例**: "使用条件に同意します。"  

     **[次へ]**をクリックします。  

5.  新しい使用条件を作成するウィザードを完了します。 [資産とコンプライアンス] ワークスペースの [使用条件] ノードに新しい使用条件が表示されます。  

## <a name="to-deploy-a-terms-and-conditions"></a>使用条件を展開するには  

1.  Configuration Manager コンソールで、 **[資産とコンプライアンス]** > **[概要]** > **[コンプライアンス設定]** > **[使用条件]**と移動します。  

2.  **[使用条件]** 一覧で、展開する項目を選択して、 **[展開]**をクリックします。  

3.  **[参照]** を使用して、使用条件の展開先となる **[コレクション]** を選択し、 **[OK]**をクリックします。  

     対象デバイスが会社のポータルにアクセスすると、展開した使用条件が表示されます。 ユーザーは、これらの使用条件に同意しないと、会社のリソースへのアクセスできません。  

    > [!NOTE]  
    >  特定のユーザーが属する複数のユーザー コレクションに同じ条件セットを展開する場合、そのユーザーが会社のポータルを開くと、複数の同じ条件がユーザーに表示されます。 ユーザーが同意または拒否できるのはすべての条項に関してのみであるため、ユーザーが同意と拒否の両方を行って条件に関してあいまいな状態になるという危険はありません。 使用条件への同意レポートには、ユーザーごとにそれぞれの条件セットに対して 1 行ずつしか含まれません。レポートにエラーは含まれません。  

## <a name="to-monitor-terms-and-conditions"></a>使用条件を監視するには  

1.  Configuration Manager コンソールで使用条件の展開を監視できます。 Configuration Manager コンソールで **[監視]** > **[概要]** > **[展開]**に移動します。  

2.  使用条件の展開を 展開一覧から選択します。  

     概要領域には、以下の統計情報が表示されます。  

    -   **[対応]** - ユーザーが最新バージョンの使用条件に同意しました  

    -   **エラー**  

    -   **[非対応]** - ユーザーが最新のバージョンではない使用条件に同意しました  

    -   **[不明]** - 登録済みデバイスのない使用条件を含めて、ユーザーが使用条件に同意したことはありません  

3.  使用条件の展開を選択してから、 **[構成基準の概要]** を選択すると、各ユーザーの展開ステータスが表示されます。  

     [展開ステータス] 画面でステータスのタブを選択すると、そのステータスであるユーザーが表示されます。 階層全体のデータを更新するには、 **[構成基準の概要]** をクリックします。 コンソールのデータを更新するには、 **[更新]** をクリックします  

## <a name="to-view--a-terms-and-conditions-report"></a>使用条件のレポートを表示するには  

1.  Configuration Manager コンソールで、 **[監視]** > **[概要]** > **[レポート]** > **[レポート]**に移動します。  

2.  **[使用条件の同意]** を選択して、 **[実行]**をクリックします。 使用条件への同意レポートが開きます。 このレポートには、使用条件が展開された各ユーザーが表示されます。 フィールドは次のとおりです。  

    -   使用条件名  

    -   ユーザー名  

    -   同意済みのバージョン  

    -   同意日  

    -   最新の利用条件に同意済み  

## <a name="updates-and-version-control-for-terms-and-conditions"></a>使用条件の更新およびバージョン管理  
 既存の使用条件を編集する際は、その使用条件を展開するときの動作を選択できます。 既存の使用条件を更新するには、次の手順に従います。  

### <a name="how-to-work-with-multiple-versions-of-terms-and-conditions"></a>使用条件の複数のバージョンを使用する方法  

1.  Configuration Manager コンソールで、 **[資産とコンプライアンス]** > **[概要]** > **[コンプライアンス設定]** > **[使用条件]**と移動します。  

2.  編集する使用条件インスタンスを選択してダブルクリックし、開きます。  

3.  **[全般]** ページまたは **[条件]** ページでコンテンツを変更して必要な編集を行えます。  

4.  **[条件]** ページで、新しいバージョンにおいては使用条件をすべてのユーザーが同意する必要があるか、あるいは新規ユーザーにのみ新しいバージョンを表示するかどうかを指定できます。  

     使用条件に対して重要な変更を行うときは常にバージョン番号を大きくし、同意を求めることをお勧めします。 誤植の修正や書式設定の変更などを行った場合は、現在のバージョン番号をそのままにします。

> [!div class="button"]
[< 前のステップ](configure-intune-subscription.md)  [次のステップ >](create-service-connection-point.md)

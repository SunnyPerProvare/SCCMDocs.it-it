---
title: "境界の定義 | Microsoft Docs"
description: "管理するデバイスを含めることができる、イントラネット上のネットワークの場所を定義する方法について説明します。"
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
caps.latest.revision: "10"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: bed70809008fde5e2b0215f4dce049402edf83ba
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="define-network-locations-as-boundaries-for-system-center-configuration-manager"></a>System Center Configuration Manager の境界としてネットワークの場所を定義する

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager の境界は、管理対象のデバイスが含まれる、ネットワーク上の場所です。 デバイスが置かれている境界は、Active Directory サイトか、デバイスにインストールされている Configuration Manager クライアントにより識別されるネットワーク IP アドレスに相当します。
 - 個別の境界を手動で作成できます。 ただし、Configuration Manager では、境界としてスーパーネットを直接入力できません。 代わりに、境界の種類として IP アドレスの範囲を使用してください。
 - [Active Directory フォレスト探索](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest)という手法を構成すると、自動検出を実行し、検出された各 IP サブネットと Active Directory サイトに対して境界を作成できます。 Active Directory フォレストの探索によって、Active Directory サイトに割り当てられているスーパーネットが特定されると、Configuration Manager はスーパーネットを IP アドレスの範囲の境界に変換します。  

Configuration Manager 管理者によって認識されない IP アドレスをデバイスが使用することは珍しくありません。 ネットワークの上でのデバイスの場所に疑問がある場合は、デバイス上で **IPCONFIG** コマンドを使用して、デバイスがレポートする場所を確認します。  

境界を作成すると、境界の種類とスコープに基づいて自動的に名前が付けられます。 この名前は変更できません。 代わりに、Configuration Manager コンソールで境界を識別しやすいように説明を入力できます。  

各境界は階層内のすべてのサイトで利用できます。 境界を作成したら、プロパティを変更して次の操作を行うことができます。  
-   1 つまたは複数の境界グループに境界を追加する。  
-   境界の種類またはスコープを変更する。  
-   境界の **[サイト システム]** タブで、境界に関連付けられたサイト システム サーバー (配布ポイント、状態移行ポイント、および管理ポイント) を確認します。  

## <a name="to-create-a-boundary"></a>境界を作成するには  

1.  Configuration Manager コンソールで、[**管理**] > [**階層の構成**] > [**境界**] をクリックします。  

2.  **[ホーム]** タブの **[作成]** グループで、 **[作成] Boundary.**をクリックします。  

3.  [境界の作成] ダイアログ ボックスの **[全般]** タブで、 **[説明]** を指定して、フレンドリ名または参照によって境界を識別します。  

4.  この境界の [種類] を選択します。 ****  

    -   **[IP サブネット]**を選択した場合、この境界の **サブネット ID** を指定する必要があります。  
        > [!TIP]  
        >  **[ネットワーク]** と **[サブネット マスク]** を指定すると、 **サブネット ID** を自動的に取得できます。 境界を保存すると、サブネット ID 値だけが保存されます。  

    -   **[Active Directory サイト]**を選択した場合、サイト サーバーのローカル フォレスト内の Active Directory サイトを指定するか、その場所を **[参照]** する必要があります。  

        > [!IMPORTANT]  
        >  境界の Active Directory サイトを指定すると、Active Directory サイトのメンバーである各 IP サブネットが境界に含まれます。 Active Directory で Active Directory サイトの構成が変更されると、この境界に含まれているネットワークの場所も変更されます。  

    -   **[IPv6 プレフィックス]**を選択した場合、IPv6 プレフィックス形式で **[プレフィックス]** を指定する必要があります。  

    -   **[IP アドレスの範囲]**を選択した場合、IP サブネットの一部または複数の IP サブネットを含む **[開始 IP アドレス]** と **[終了 IP アドレス]** を指定する必要があります。    

5.  [OK] をクリックして新しい境界を保存します。 ****  

## <a name="to-configure-a-boundary"></a>境界を構成するには  

1.  Configuration Manager コンソールで、[**管理**] > [**階層の構成**] > [**境界**] をクリックします。  

2.  変更する境界を選択します。  

3.  **[ホーム]** タブの **[プロパティ]** グループで、 **[プロパティ]**をクリックします。  

4.  境界の **[プロパティ]** ダイアログ ボックスで、 **[全般]** タブを選択して、境界の **[説明]** または **[種類]** を編集します。 境界のネットワークの場所を編集して、境界のスコープを変更することもできます。 たとえば、Active Directory サイトの境界の場合、新しい Active Directory サイト名を指定できます。  

5.  [サイト システム **** ] タブを選択し、その境界に関連付けられているサイト システムを確認します。 この構成は、境界のプロパティから変更することはできません。  

    > [!TIP]  
    >  サイト システム サーバーが境界のサイト システムの一覧に表示されるようにするには、サイト システム サーバーが、この境界を含む、少なくとも 1 つの境界グループのサイト システム サーバーとして関連付けられている必要があります。 これは、境界グループの **[参照]** タブで構成されます。  

6.  [境界グループ] タブを選択して、この境界の境界グループ メンバーシップを変更します。 ****  

    -   この境界を 1 つまたは複数の境界グループに追加するには、 **[追加]**をクリックして、1 つまたは複数の境界グループのチェック ボックスをオンにし、 **[OK]**をクリックします。  

    -   この境界を境界グループから削除するには、境界グループを選択して [削除] をクリックします。 ****  

7.  [OK] をクリックして境界のプロパティを閉じ、構成を保存します。 ****  

---
title: "デバイスを自動的にコレクションごとに分類する | Microsoft Docs"
description: "System Center Configuration Manager でデバイスをコレクションに自動的に分類します。"
ms.custom: na
ms.date: 04/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
caps.latest.revision: "5"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d1b79fb091a6ae4b967d63843ae7b45a0cbeb555
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="automatically-categorize-devices-into-collections-with-system-center-configuration-manager"></a>System Center Configuration Manager でデバイスをコレクションに自動的に分類する

*適用対象: System Center Configuration Manager (Current Branch)*

Microsoft Intune と Configuration Manager を使用している場合に、デバイス コレクションにデバイスを自動的に配置するために使用できるデバイス カテゴリを作成することができます。 ユーザーは Intune にデバイスを登録するときに、デバイス カテゴリを選択する必要があります。 デバイス カテゴリは、Configuration Manager コンソールから変更できます。

> [!IMPORTANT]  
    >  この機能は、Microsoft Intune の **2016 年 6 月**以降のリリースで動作します。 これらの手順を実行する前に、今回のリリースに更新していることを確認してください。

## <a name="create-device-categories"></a>デバイス カテゴリを作成する

1.  [**資産とコンプライアンス**] > [**概要**] > [**デバイス コレクション**] の順に移動します。
2.  [**ホーム**] タブの [**デバイス コレクション**] グループで、[**デバイス カテゴリの管理**] を選択します。
3.  カテゴリを作成、編集、または削除します。

## <a name="associate-a-collection-with-a-device-category"></a>コレクションをデバイス カテゴリに関連付ける

コレクションをデバイス カテゴリと関連付けると、そのカテゴリのすべてのデバイスがそのコレクションに追加されます。 [**すべてのシステム**] などの組み込みコレクションにデバイス カテゴリの規則を追加することはできません。

1.  デバイス コレクションの [**プロパティ**] ダイアログの [**メンバーシップの規則**] で、[**規則の追加**] > [**デバイス カテゴリの規則**] の順に選びます。
2.  [**デバイス カテゴリの選択**] ダイアログ ボックスで、コレクション内のすべてのデバイスに適用される 1 つ以上のカテゴリを選択します。

## <a name="change-the-category-of-a-device"></a>デバイスのカテゴリを変更する

1.  [**資産とコンプライアンス**] > [**概要**] > [**デバイス**] で、[**デバイス**] 一覧からデバイスを選びます。
2.  [**ホーム**] タブの [**デバイス**] グループで、[**カテゴリの変更**] を選びます。
3.  カテゴリを選択し、[**OK**] を選びます。

## <a name="view-which-category-a-device-belongs-to"></a>デバイスが属するカテゴリを表示する

[**資産とコンプライアンス**] > [**概要**] > [**デバイス**] で、[**デバイス**] 一覧の [**デバイス カテゴリ**] 列にカテゴリが表示されます。

[**デバイス カテゴリ**] 列が表示されない場合、[**デバイス**] 一覧のいずれかの列の見出し ([**名前**] など) を右クリックし、[**デバイス カテゴリ**] を選択します。

デバイスをカテゴリに割り当て、その後、カテゴリを削除した場合、[**Microsoft Intune に各ユーザーが登録したデバイス一覧**] レポートには、[**デバイス カテゴリ**] 列にカテゴリ名ではなく GUID が表示されます。

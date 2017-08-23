---
title: "資産インテリジェンスの検証状態移行の例 | Microsoft Docs"
description: "System Center Configuration Manager での資産インテリジェンスの検証状態移行の例について説明します。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6230a6e5-a1f6-459b-84f1-07fbde0e70f0
caps.latest.revision: "6"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: f280e06f34c0ed355b7c2652c571e36eb6684c59
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="example-validation-state-transitions-for-asset-intelligence-in-system-center-configuration-manager"></a>System Center Configuration Manager での資産インテリジェンスの検証状態移行の例

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の資産インテリジェンスの検証の状態は固定したものではなく、資産インテリジェンス カタログに保持されたデータに影響を与える管理操作によって変化することがあります。 このトピックでは、考えられる検証状態の変化について例を挙げて説明します。

##  <a name="BKMK_UncategorizedIsCategorized"></a> カテゴリ化されていないカタログ項目が管理ユーザーによってカテゴリ化される  

|**状態の変化**|**状態の変化の説明**|  
|--------------------------|--------------------------------------|  
|**カテゴリ化されていない**|System Center Online または管理ユーザーによってカテゴリ化されたことがない、インベントリされたソフトウェア タイトルが、資産インテリジェンス カタログに入力されます。|  
|**カテゴリ化されていない** に **ユーザー定義**|カテゴリ化されていない項目が、管理ユーザーによってカテゴリ化されます。|  

##  <a name="BKMK_CategorizedIsReCategorized"></a> カテゴリ化されたカタログ項目が管理ユーザーによって再カテゴリ化される  

|**状態の変化**|**状態の変化の説明**|  
|--------------------------|--------------------------------------|  
|**検証済み**|カタログ項目は、System Center Online の調査員によって定義され、資産インテリジェンス カタログ内に存在しています。|  
|**カテゴリ化されていない** から **検証済み**|検証されていない項目が、管理ユーザーによってカテゴリ化されます。|  

> [!NOTE]  
>  System Center Online から取得したカテゴリ化情報はデータベースに格納されて削除できないため、管理ユーザーは、後で System Center Online のカテゴリ化を復元することができます。  

##  <a name="BKMK_UserDefinedIsRecategorized"></a> ユーザー定義のカタログ項目が System Center Online によって再カテゴリ化される  

|**状態の変化**|**状態の変化の説明**|  
|--------------------------|--------------------------------------|  
|**カテゴリ化されていない**|インベントリされたソフトウェア タイトルが、System Center Online または管理ユーザーによってカテゴリ化されたことのない資産インテリジェンス カタログに入力されます。|  
|**検証済み**|カテゴリ化されていない項目が、管理ユーザーによってカテゴリ化されます。|  
|**ユーザー定義済み** から **更新可能**|ユーザー定義のカタログ項目は、その後の資産インテリジェンス カタログの手動一括更新中に、System Center Online によって異なったカテゴリ化がされています。<br /><br /> 管理ユーザーは [ソフトウェア詳細の不一致の解決] ダイアログ ボックスを使用して、新しいカテゴリ化情報と以前のユーザー定義済みの値のいずれを使用するのかを決定できます。 ****|  
|**更新可能** から **検証済み**|管理ユーザーは [ソフトウェア詳細の不一致の解決] ダイアログ ボックスを使用して、前回のカタログ更新中に System Center Online から受信した新しいカテゴリ化情報を使用します。 ****|  
|または||  
|**更新可能** から **検証済み**|管理ユーザーは [ソフトウェア詳細の不一致の解決] ダイアログ ボックスを使用して、以前のユーザー定義済みの値を使用します。 ****|  

> [!NOTE]  
>  System Center Online から取得したカテゴリ化情報はデータベースに格納されて削除できないため、管理ユーザーは、後で System Center Online のカテゴリ化を復元することができます。  

##  <a name="BKMK_UncategorizedIsSubmitted"></a> カテゴリ化されていないカタログ項目が、カテゴリ化のために System Center Online に送信される  

|**状態の変化**|**状態の変化の説明**|  
|--------------------------|--------------------------------------|  
|**カテゴリ化されていない**|インベントリされたソフトウェア タイトルが、System Center Online または管理ユーザーによってカテゴリ化されたことのない資産インテリジェンス データベースに入力されます。|  
|**カテゴリ化されていない** から **保留中**|カテゴリ化されていない項目が、管理ユーザーによるカテゴリ化のために System Center Online に送信されます。|  
|**保留中** から **検証済み**|この項目は System Center Online によってカテゴリ化されています。 管理ユーザーは、一括カタログ更新または資産インテリジェンス カタログの同期化を使用して、この項目を資産インテリジェンス カタログにインポートします。 資産インテリジェンス同期ポイント サイト システムの役割を使用すると、両方を使用できます。|  

##  <a name="BKMK_UserDefinedIsSubmitted"></a> ユーザー定義のカタログ項目が、カテゴリ化のために System Center Online に送信される  

|**状態の変化**|**状態の変化の説明**|  
|--------------------------|--------------------------------------|  
|**カテゴリ化されていない**|インベントリされたソフトウェア タイトルが、System Center Online または管理ユーザーによってカテゴリ化されたことのない資産インテリジェンス データベースに入力されます。|  
|**検証済み**|ユーザーがカテゴリ化されていない項目がカテゴリ化しました。|  
|**ユーザー定義済み** から **保留中**|ユーザー定義のカタログ項目を、カテゴリ化のために System Center Online に送信します。|  
|**保留中** から **更新可能**|ユーザー定義のカタログ項目が、その後のカタログ同期時に System Center Online により、異なるようにカテゴリ化されました。 [競合の解決] 操作を使用して、新しいカテゴリ化情報または以前のユーザー定義値を使用するかどうかを決定することができます。 **** 競合の解決の詳細については、「[ソフトウェア詳細の競合の解決](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails)」をご覧ください。|  
|**更新可能** から **検証済み**|[競合の解決] 操作を使用して、前回のカタログ更新中に System Center Online から受信した新しいカテゴリ化情報を選択します。 **** 競合の解決の詳細については、「[ソフトウェア詳細の競合の解決](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails)」をご覧ください。|  
|または||  
|**更新可能** から **検証済み**|[競合の解決] 操作を使用して、以前のユーザー定義値の使用を選択します。 **** 競合の解決の詳細については、「[ソフトウェア詳細の競合の解決](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails)」をご覧ください。|  

> [!NOTE]  
>  System Center Online から取得したカテゴリ化情報はデータベースに格納されて削除できないため、後で System Center Online のカテゴリ化を復元することができます。  

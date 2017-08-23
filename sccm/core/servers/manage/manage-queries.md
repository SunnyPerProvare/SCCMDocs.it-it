---
title: "クエリの管理 | Microsoft Docs"
description: "クエリを管理する方法について説明します。 詳しい参照情報を記載した表が含まれています。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e562e2a0-8df8-4952-952f-e8c38461c612
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 738dcf0b52f18b38b732bf8ca5d7a87369b1c468
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-manage-queries-in-system-center-configuration-manager"></a>System Center Configuration Manager でクエリを管理する方法

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックでは、System Center Configuration Manager でクエリを管理する方法について説明します。  

 クエリの作成方法については、「[System Center Configuration Manager でクエリを管理する方法](../../../core/servers/manage/create-queries.md)」を参照してください。  

## <a name="how-to-manage-queries"></a>クエリを管理する方法  
 [監視] **** ワークスペースで [クエリ] ****を選択し、管理するクエリと管理タスクを選択します。  

 次の表で、管理タスクに関する詳細と、各タスクを選択する前に必要となる追加情報について説明します。  

|管理タスク|説明|説明|  
|---------------------|-------------|----------------------|  
|**実行**|Configuration Manager コンソールで選択されたクエリを実行し、結果を表示します。|詳細情報はありません。|  
|**クライアントのインストール**|**クライアントのインストール ウィザード** を開くと、クエリによって戻されたコンピューターに Configuration Manager クライアントをインストールできます。<br /><br /> このオプションは、モバイル デバイスやユーザー、またはユーザー グループを返すクエリでは使用できません。|クライアント プッシュで Configuration Manager をインストールする方法の詳細については、「[How to deploy clients to Windows computers](/sccm/core/clients/deploy/deploy-clients-to-windows-computers)」 (Windows コンピューターにクライアントを展開する方法) を参照してください。|  
|**エクスポート**|別のサイトへインポートができる Managed Object Format (MOF) と呼ばれる形式のファイルにクエリをエクスポートするオブジェクトのエクスポート ウィザード **** を開きます。|詳細情報はありません。|  
|**移動**|選択したクエリを [クエリ] **** ノードの下に作成されたフォルダーに移動する [選択した項目の移動] **** ダイアログ ボックスを開きます。|詳細情報はありません。|  

## <a name="see-also"></a>関連項目  
 [System Center Configuration Manager でのクエリの操作とメンテナンス](../../../core/servers/manage/operations-and-maintenance-for-queries.md)

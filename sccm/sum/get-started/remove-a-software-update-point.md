---
title: "ソフトウェアの更新ポイントの削除 | Microsoft Docs"
description: "次の手順に従って、ソフトウェアの更新ポイント サイト システムの役割を Configuration Manager コンソールから削除できます。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 2486375c-d4a2-4cf2-9124-9bee02bbf173
ms.openlocfilehash: 22de02c51be3a0cd66b1be0f04b2fbdeb897858c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
#  <a name="BKMK_RemoveSUP"></a> ソフトウェアの更新ポイント サイト システムの役割を削除する  

*適用対象: System Center Configuration Manager (Current Branch)*

ソフトウェアの更新ポイント サイト システムの役割を Configuration Manager コンソールから削除できます。 クライアント ポリシーが更新され、一覧からソフトウェアの更新ポイントが削除されます。 サイトにある最後のソフトウェアの更新ポイントを削除すると、ソフトウェアの更新ポイント一覧にはソフトウェアの更新ポイントが表示されなくなり、サイトのソフトウェア更新プログラムは実質的に無効になります。 プライマリ サイトに複数のソフトウェアの更新ポイントがあり、同期ソースとして構成されるソフトウェアの更新ポイントを削除する場合、サイトにある別のソフトウェアの更新ポイントを選択して、新しい同期ソースにする必要があります。  

> [!NOTE]  
>  ソフトウェアの更新ポイント サイトの役割をサイト システムから削除した場合、15 分以上待ってから、ソフトウェアの更新ポイント サイトの役割を再インストールする必要があります。  

 ソフトウェア更新ポイントを削除するには、次の手順を実行します。  

#### <a name="to-remove-the-software-update-point"></a>ソフトウェアの更新ポイントを削除するには  

1.  Configuration Manager **** コンソールで、[管理 ****] をクリックします。  

2.  [管理] ワークスペースで、[サイトの構成 ****] を展開して [サーバーとサイト システムの役割 ****] をクリックします。  

3.  削除するソフトウェアの更新ポイントがあるサイト システム サーバーを選択し、[サイト システムの役割 ****] で、[ソフトウェアの更新ポイント ****] を選択します。  

4.  [サイトの役割 **** ] タブの [サイトの役割 **** ] グループで、[役割の削除 ****] をクリックします。 ソフトウェアの更新ポイントを削除することを確認するか、またはサイトにある他のソフトウェアの更新ポイント用に新しい同期ソースを選択します。  

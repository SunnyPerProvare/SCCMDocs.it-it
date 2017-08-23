---
title: "診断データの収集 | Microsoft Docs"
description: "System Center Configuration Manager がそれ自体に関する診断と使用状況データを収集する方法について説明します。"
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: becfa825-b19f-448c-ab82-bb929255e4ae
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 9c0165212fe34f460be2ce870d0542b616f3bc4d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="how-diagnostics-and-usage-data-is-collected-by-system-center-configuration-manager"></a>System Center Configuration Manager が診断と使用状況データを収集する方法

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の診断と使用状況データを収集するため、毎週、各プライマリ サイトで SQL Server のクエリを実行します。 複数サイトの階層では、データは中央管理サイトにレプリケートされます。  

階層の最上位のサイトでは、サービス接続ポイントのサイト システムの役割が、更新プログラムをチェックするときに、この情報を送信します。 サービス接続ポイントのモードは、データの転送方法によって決まります。  

-   **オンライン モード:** 診断と使用状況データは、週に 1 回、サービス接続ポイントからクラウド サービスに自動送信されます。  

-   **オフライン モード:** 診断と使用状況データはサービス接続ツールを使用して手動で転送されます。 詳細については、[System Center Configuration Manager のサービス接続ツールの使用](../../../core/servers/manage/use-the-service-connection-tool.md)を参照してください。  

詳細については、[System Center Configuration Manager のサービス接続ポイントについて](../../../core/servers/deploy/configure/about-the-service-connection-point.md)をご覧ください。  

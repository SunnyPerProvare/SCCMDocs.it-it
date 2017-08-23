---
title: "レポートの前提条件 | Microsoft Docs"
description: "System Center Configuration Manager のレポートの使用に影響するさまざまな依存関係について理解します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9cc508a5-5023-4833-b776-ae9a6971138f
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 2e624eb2ea061a4eb7d92365410fada335640224
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-reporting-in-system-center-configuration-manager"></a>System Center Configuration Manager のレポートの前提条件

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のレポートには、外部依存関係と製品内部依存関係があります。  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部の依存関係  
 次の表に、レポートの外部の依存関係を示します。  

|前提条件|説明|  
|------------------|----------------------|  
|SQL Server Reporting Services|Configuration Manager のレポートを使用するには、事前に SQL Server Reporting Services をインストールして構成しておく必要があります。<br /><br /> 各組織の環境内での Reporting Services の計画と展開については、SQL Server 2008 オンライン ブックの「 [SQL Server Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=212032) 」を参照してください。|  
|レポート サービス ポイントを実行するコンピューターのサイト システムの役割の依存関係|[System Center Configuration Manager のサポートされている構成](../../../core/plan-design/configs/supported-configurations.md)|  

## <a name="dependencies-internal-to-configuration-manager"></a>Configuration Manager 内部の依存関係  
 次の表に、Configuration Manager のレポートの依存関係を示します。  

|前提条件|説明|  
|------------------|----------------------|  
|レポート サービス ポイント|Configuration Manager のレポートを使用するには、事前にレポート サービス ポイントのサイト システムの役割を構成しておく必要があります。 レポート サービス ポイントのインストールと構成方法の詳細については、「[System Center Configuration Manager におけるレポートの構成](../../../core/servers/manage/configuring-reporting.md)」を参照してください。|  

## <a name="supported-sql-server-versions-for-the-reporting-services-point"></a>レポート サービス ポイントでサポートされる SQL Server バージョン  
 レポート サービス データベースは、64 ビット SQL Server インストールの既定のインスタンスまたは名前付きインスタンスにインストールできます。 SQL Server インスタンスは、サイト システム サーバーまたはリモート コンピューターと併置できます。  

 次の表に、レポート サービス ポイントがサポートする SQL Server バージョンを示します。  

|SQL Server バージョン|レポート サービス ポイント|  
|------------------------|------------------------------|  
|累積的な更新プログラム 9 以上を適用した SQL Server 2008 SP2<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|○|  
|累積的な更新プログラム 4 以上を適用した SQL Server 2008 SP3<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|○|  
|SP1 と累積的な更新プログラム 6 以上を適用した SQL Server 2008 R2<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|○|  
|SP2 を適用した SQL Server 2008 R2<br /><br /> -   Standard<br />-   Enterprise<br />-   Datacenter|○|  
|SP1 と累積的な更新プログラム 4 以上を適用した SQL Server Express 2008 R2|サポートされません|  
|SP2 を適用した SQL Server Express 2008 R2|サポートされません|  
|累積的な更新プログラム 2 以上を適用した SQL Server 2012<br /><br /> -   Standard<br />-   Enterprise|○|  
|SP1 を適用し、最小の累積的な更新プログラムを適用していない SQL Server 2012<br /><br /> -   Standard<br />-   Enterprise|○|  
|SQL Server 2014<br /><br /> -   Standard<br />-   Enterprise|○|
|SQL Server 2016<br /><br /> -   Standard<br />-   Enterprise|○|
|SQL Server 2016 SP1<br /><br /> -   Standard<br />-   Enterprise|○|
## <a name="next-steps"></a>次のステップ
[レポートの操作とメンテナンス](operations-and-maintenance-for-reporting.md)

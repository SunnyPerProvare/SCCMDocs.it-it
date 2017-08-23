---
title: "Configuration Manager の評価 | Microsoft Docs"
description: "組織で使用するために System Center Configuration Manager を評価するラボ環境を作成します。"
ms.custom: na
ms.date: 2/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
caps.latest.revision: "25"
caps.handback.revision: "0"
author: brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: d7ea785ab1beee09b9adda735a87f89bc9481620
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>独自のラボ環境を構築して System Center Configuration Manager を評価する

*適用対象: System Center Configuration Manager (Current Branch)*

 組織で使用するために System Center Configuration Manager を評価するラボ環境を作成する方法について説明します。  

 System Center Configuration Manager は、ユーザー、デバイス、およびソフトウェアを管理するための、複雑で強力なツールです。 概念の理解を現場での実践に結び付けることができるように、完全な展開の前に System Center Configuration Manager の詳細な評価をすることをお勧めします。  

 このガイドは、主に、企業環境内で Configuration Manager の使用を評価する次のような管理者を対象にしています。  

-   PC、サーバー、およびモバイル デバイスを完全に管理するソリューションを必要とする管理者  

-   オンプレミス デバイス管理のセキュリティと、クラウドベースのデバイス管理の柔軟性を必要とする高セキュリティ業界の管理者  

-   オンプレミス サーバー アーキテクチャのスケールアップの管理を必要とする管理者  

## <a name="what-this-lab-does"></a>このラボの実行内容  
 このラボ環境を作成する主な目的は、Configuration Manager の使用を開始するための一般的な知識を提供すること、および Configuration Manager についての理解を深めることです。 次の 2 台のサーバーを使用して、最新バージョンの Configuration Manager の簡易化した構成を使って説明します。  

-   Active Directory、ドメイン コントローラー、および DNS サーバーをホストするサーバー  

-   Configuration Manager と、関連するすべての SQL Server コンポーネントをホストするサーバー  

クライアント コンピューターは Hyper-V 内にインストールされます。 ラボ自体は、単一のサーバーで完全に仮想化されたシステムとして実行することもできます。  

## <a name="what-this-lab-does-not-do"></a>このラボで実行しないこと  
 このラボでは、Configuration Manager のすべてのシナリオについて説明しません。 すぐにアクティブな環境に移行することは想定されていません。  

 このラボを構築すると、機能し、作業できる環境が整います。 ただし、この環境は、システム パフォーマンス、ハード ディスク領域の管理、SQL Server の記憶域などの要因に対して最適化されません。  

##  <a name="BKMK_EvalRec"></a>ラボを構築する前の推奨資料  
 「[System Center Configuration Manager のドキュメント](http://docs.microsoft.com/sccm/)」には豊富なコンテンツがあります。 ラボを構築する前に、このライブラリから次のトピックを読むことをお勧めします。  

-   「[System Center Configuration Manager の概要](../../core/understand/introduction.md)」。Configuration Manager コンソール、エンドユーザー ポータル、およびシナリオ例の主要な概念について説明しています。  

-   「[System Center Configuration Manager の特徴と機能](../../core/plan-design/changes/features-and-capabilities.md)」。Configuration Manager の主な管理機能について説明しています。  

-   「[System Center Configuration Manager の基本](../../core/understand/fundamentals.md)」。知識を強化します。  

-   「[System Center Configuration Manager のロール ベース管理の基礎](../../core/understand/fundamentals-of-role-based-administration.md)」。セキュリティ ロールの重要性について説明しています。  

-   「[System Center Configuration Manager でのコンテンツ管理の基本的な概念](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md)」。コンテンツ管理について説明しています。  

-   「[クライアントが System Center Configuration Manager のサイト リソースやサービスを検索する方法を理解する](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)」。展開全体での日常のタスクを適切にサポートする方法を説明しています。  

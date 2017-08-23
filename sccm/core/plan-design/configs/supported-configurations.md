---
title: "サポートされている構成 | Microsoft Docs"
description: "機能的な System Center Configuration Manager 展開を計画、展開、および管理するための主要な構成および要件を特定します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45a10878-ff48-4318-9c6d-c014b38a4039
caps.latest.revision: "9"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: aad46e9ab893b9bb3e32d35c17b9678b3a265c99
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="supported-configurations-for-system-center-configuration-manager"></a>System Center Configuration Manager のサポートされている構成

*適用対象: System Center Configuration Manager (Current Branch)*

オンプレミス ソリューションとして、System Center Configuration Manager は、サーバー、クライアント、ネットワーク構成、および Microsoft Intune、SQL Server および Azure などのその他の製品を使用します。

このドキュメントおよび次のトピックの情報では、機能的な Configuration Manager 展開を計画、展開、および管理するための主要な構成および要件、または制限事項を識別するために不可欠です。  この情報は、Configuration Manager サイト、階層、および管理対象デバイスのインフラストラクチャに固有です。

Configuration Manager 機能に、さらに明確な構成が必要な場合、その情報は機能固有のドキュメントに含められ、これらのより一般的な構成の詳細を補足します。  

 次のトピックで説明する製品とテクノロジが、Configuration Manager でサポートされています。 ただし、このコンテンツにそれらが含まれていても、その製品の個別のサポート ライフサイクルを超える製品サポートの延長を表すものではありません。 既にサポート ライフサイクルが終了している製品は、Configuration Manager ではサポートされません。 マイクロソフト サポート ライフサイクルの詳細については、 [「マイクロソフト サポート ライフサイクル」](http://go.microsoft.com/fwlink/p/?LinkId=208270) Web サイトを参照してください。  

> [!NOTE]  
>  マイクロソフトのサポート ライフサイクル ポリシーについては、[マイクロソフト サポートの「ライフサイクル ポリシー FAQ」](http://go.microsoft.com/fwlink/p/?LinkId=31976)Web サイトを参照してください。  

 さらに、次のトピックに示されていない製品および製品バージョンは、[Enterprise Mobility および Security ブログ](https://blogs.technet.microsoft.com/enterprisemobility/)で告知されていない限り、System Center Configuration Manager でサポートされません。  このブログのコンテンツは、このドキュメントの本文よりも先に更新される場合があります。


-  [サイジングとスケールの数値](../../../core/plan-design/configs/size-and-scale-numbers.md)  
サイトの数、サイトごとのサイト システムの役割、Configuration Manager のさまざまな階層設計でサポートされるクライアントまたはデバイスの詳細について説明します。

-  [サイトとサイト システムの前提条件](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
Windows Server でさまざまな種類のサイトの種類とサイト システムの役割をサポートするために必要な構成について説明します。

-  [サイト システム サーバーのサポートされるオペレーティング システム](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
サイト サーバーまたはサイト システム サーバーとして使用できるオペレーティング システムについて説明します。

-  [クライアントとデバイスのサポートされるオペレーティング システム](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)  
Windows、Windows Embedded、Linux および UNIX、Mac、モバイル デバイスを含む Configuration Manager で管理できるオペレーティング システムについて説明します。

-  [コンソールでサポートされているオペレーティング システム](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
展開を管理するためのアクセス ポイントを提供する Configuration Manager コンソールをホストできるオペレーティング システムについて説明します。  

-  [SQL Server バージョンのサポート](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
サイト データベースとレポート データベースをホストできる SQL Server のバージョン、および必要な構成と使用可能なオプションの構成についても説明します。

-  [高可用性オプション](../../../protect/understand/high-availability-options.md)  
Configuration Manager 展開の高可用性サービスを維持するために、環境の設計時に実装できるオプションについて説明します。

-  [推奨ハードウェア](../../../core/plan-design/configs/recommended-hardware.md)  
Configuration Manager サイトと主要なサービスをホストするための適切なハードウェアおよび構成の識別に役立つガイドラインについて説明します。

-  [Active Directory ドメインのサポート](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
Configuration Manager が必要とする Active Directory ドメインのサポートされている構成、およびサポートについて説明します。

-  [Windows の機能とネットワークのサポート](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
サポートされている Windows テクノロジ (BranchCache やデータ重複除去など) および Configuration Manager 使用時の制限について説明します。

-  [仮想環境のサポート](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
サポートされている仮想マシン テクノロジの使用方法について説明します。

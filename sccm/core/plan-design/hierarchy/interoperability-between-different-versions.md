---
title: "Configuration Manager のバージョン間の相互運用性 | Microsoft Docs"
description: "同じネットワーク上に複数の System Center Configuration Manager 階層がある場合に競合を回避する方法について説明します。"
ms.custom: na
ms.date: 1/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 28593d271603ff9775425327996d844d7ed358cd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="interoperability-between-different-versions-of-system-center-configuration-manager"></a>異なるバージョンの Configuration Manager 間の相互運用性

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の複数の独立した階層を同じネットワークにインストールして動作させることができます。 ただし、移行プロセス以外では Configuration Manager の異なる階層は相互運用されないため、各階層に階層間の競合を防ぐ構成が必要です。 また、管理対象のリソースが正しい階層のサイト システムと対話できるように、特定の構成を作成することができます。  

 以下のセクションでは、同じネットワークで複数のバージョンの Configuration Manager を使用するときの相互運用性について説明します。  

-   [System Center Configuration Manager と以前のバージョンの製品間の相互運用性](#BKMK_SupConfigInterop)  

-   [Configuration Manager コンソールの相互運用性](#BKMK_ConsoleInterop)  

-   [バージョンが混在している階層内の Configuration Manager の制限](#bkmk_mixed)  

##  <a name="BKMK_SupConfigInterop"></a> System Center Configuration Manager と以前のバージョンの製品間の相互運用性  
 System Center 2012 Configuration Manager から System Center Configuration Manager へ、または (コンソール内更新プログラムを使用した) ある System Center Configuration Manager バージョンから新しいバージョンへのアップグレード プロセス中を除き、異なるバージョンのサイトが同じ階層に共存することはできません。   

 System Center Configuration Manager のサイトまたは階層は既存の System Center 2012 Configuration Manager のサイトまたは階層と並列展開できるため、一方のバージョンのサイトにもう一方のバージョンのクライアントが参加することがないように計画することをお勧めします。

たとえば、複数の Configuration Manager 階層に、同じネットワークの場所が含まれる、重複する境界がある場合には、(「[重複する境界について](/sccm/core/servers/deploy/configure/boundary-groups#overlapping-boundaries)」を参照)、サイトの自動割り当てを使用する代わりに、新しい各クライアントを特定のサイトに割り当てるのが最善です。 System Center 2012 Configuration Manager のサイトの自動割り当ての詳細については、「[System Center Configuration Manager でクライアントをサイトに割り当てる方法](../../../core/clients/deploy/assign-clients-to-a-site.md)」を参照してください。  

 また、System Center Configuration Manager のサイト システムの役割をホストしているコンピューターに System Center 2012 Configuration Manager のクライアントをインストールすることや、System Center 2012 Configuration Manager のサイト システムの役割をホストしているコンピューターに System Center Configuration Manager クライアントをインストールすることはできません。  

 同様に、次のクライアントと仮想プライベート ネットワーク (VPN) 接続は、サポートされていません。  

-   System Center 2012 Configuration Manager 以前のコンピューター クライアント バージョン  

-   System Center 2012 Configuration Manager 以前のデバイス管理クライアント  

-   Windows CE Platform Builder デバイス管理クライアント (すべてのバージョン)  

-   System Center Mobile Device Manager VPN 接続  

###  <a name="BKMK_SupConfigSiteAssignment"></a> クライアントのサイト割り当てに関する考慮事項  
 System Center Configuration Manager クライアントは、1 つのプライマリ サイトにのみ割り当てることができます。 クライアントのインストール時にサイトの自動割り当てによってサイトにクライアントが割り当てられ、複数の境界グループに同じ境界が含まれており、それらの境界グループに異なるサイトが割り当てられている場合は、クライアントの実際のサイト割り当てを予測することはできません。  

 Configuration Manager の複数のサイトと階層で境界が重複している場合、予期したとおりのサイトにクライアントが割り当てられなかったり、サイトにまったく割り当てられない可能性があります。  

 System Center Configuration Manager クライアントは、サイト割り当てを完了する前に Configuration Manager サイトのバージョンを確認するため、境界が重複している場合は、以前のバージョンのサイトには割り当てられません。 ただし、System Center 2012 Configuration Manager クライアントが System Center Configuration Manager サイトに間違って割り当てられる場合があります。  

 2 つの階層に重複する境界がある場合に、クライアントが正しくないサイトに割り当てられるのを防ぐため、クライアントを特定のサイトに割り当てるように Configuration Manager クライアント インストール パラメーターを構成することをお勧めします。  

##  <a name="bkmk_mixed"></a> バージョンが混在している階層内の Configuration Manager の制限  
 System Center Configuration Manager サイトのアップグレードの過程において、サイトごとにバージョンが異なることがあります。 たとえば、中央管理サイトを新しいバージョンにアップグレードするものの、サイトのメンテナンス期間のために 1 つ以上のプライマリ サイトが後日までアップグレードできないことがあります。  

 特定の階層内にある各種サイトのバージョンが異なる場合、一部の機能は利用できません。 これが、Configuration Manager コンソールで Configuration Manager オブジェクトを管理する方法と、クライアントで使用できる機能に影響する可能性があります。 通常、Configuration Manager の新しいバージョンの機能を、古いサービス バック バージョンを実行しているサイトまたはクライアントで使用することはできません。  

### <a name="limitations-when-upgrading--configuration-manager"></a>Configuration Manager のアップグレード時の制限事項  

|オブジェクト|説明|  
|------------|-------------|  
|ネットワーク アクセス アカウント|**System Center 2012 Configuration Manager から System Center Configuration Manager にアップグレードする場合:** System Center Configuration Manager に更新された中央管理サイトに接続されている Configuration Manager コンソールからネットワーク アクセス アカウントの詳細を表示する場合、コンソールには System Center 2012 Configuration Manager を実行するプライマリ サイトで構成されたアカウントの詳細が表示されません。 プライマリ サイトを中央管理サイトと同じバージョンにアップグレードすると、コンソールにアカウントの詳細が表示されます。<br /><br /> **System Center Configuration Manager バージョン間でアップグレードする場合:** System Center Configuration Manager の新しいバージョンに更新された中央管理サイトに接続されている Configuration Manager コンソールからネットワーク アクセス アカウントの詳細を表示する場合、コンソールには、以前のバージョンを実行するプライマリ サイトで構成されたアカウントの詳細が表示されません。 プライマリ サイトを中央管理サイトと同じバージョンにアップグレードすると、コンソールにアカウントの詳細が表示されます。|  
|オペレーティング システム展開用のブート イメージ|**System Center 2012 Configuration Manager から System Center Configuration Manager にアップグレードする場合:** 階層の最上位サイトが System Center Configuration Manager にアップグレードされると、既定のブート イメージは、Windows アセスメント & デプロイメント キット 10 (Windows ADK) に基づいてブート イメージに自動的に更新されます。 これらのブート イメージは、System Center Configuration Manager サイトのクライアントへの展開にのみ使用してください。 詳細については、「[System Center Configuration Manager のオペレーティング システムの展開の相互運用性に関する計画](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md)」を参照してください。<br /><br /> **System Center Configuration Manager バージョン間のアップグレードの場合:** 新しいバージョンの cm6long が使用中のバージョンの Windows ADK を更新しない限り、ブート イメージには影響ありません。|  
|新しいタスク シーケンス ステップ|以前のバージョンでは利用できないあるバージョンの Configuration Manager で導入された手順を使用してタスク シーケンスを作成すると、次の問題が生じる可能性があります。<br /><br /> -- 以前のバージョンの Configuration Manager を実行しているサイトからタスク シーケンスを編集しようとするとエラーが発生する。<br /><br /> -- 以前のバージョンの Configuration Manager クライアントを実行するコンピューターでタスク シーケンスが実行されない。|  
|ダウン レベルの管理ポイント通信のクライアント|クライアントよりも古いバージョンを実行しているサイトの管理ポイントと通信する Configuration Manager クライアントでは、ダウン レベルのバージョンの Configuration Manager がサポートしている機能のみ使用できます。 たとえば、最近アップグレードされた System Center Configuration Manager サイトのコンテンツをクライアントに展開する場合、そのバージョンにまだアップグレードされていない管理ポイントと通信していると、クライアントは最新バージョンの新しい機能を使用できません。|  

##  <a name="BKMK_ConsoleInterop"></a> Configuration Manager コンソールの相互運用性  
 次の表に、複数のバージョンの Configuration Manager が存在する環境での Configuration Manager の使用についてまとめます。  

|相互運用環境|説明|  
|----------------------------------|----------------------|  
|System Center 2012 Configuration Manager と System Center Configuration Manager の両方がある環境|Configuration Manager サイトを管理するには、コンソール、およびそのコンソールが接続するサイトの両方が、同じバージョンの Configuration Manager でなければなりません。 たとえば、System Center 2012 Configuration Manager コンソールを使って、System Center Configuration Manager サイトを管理することはできません。また、その逆も同様です。<br /><br /> 同じコンピューターに、System Center 2012 Configuration Manager コンソールと System Center Configuration Manager コンソールの両方をインストールすることはできません。|  
|System Center Configuration Manager の複数のバージョンがある環境|System Center Configuration Manager では、1 台のコンピューターに複数の Configuration Manager コンソールをインストールすることはできません。 System Center Configuration Manager の複数のバージョンのコンソールを使用したい場合は、それぞれ別のコンピューターにインストールする必要があります。<br /><br /> 階層内のサイトを更新しているときに、コンソールを、新しいバージョンを実行しているサイトに接続して、その階層にある他のサイトの情報を見ることができます。 ただし、この構成は推奨されていません。コンソールのバージョン間と Configuration Manager サイトのバージョンが異なるとデータに問題が生じる可能性があり、最新の製品バージョンで利用できる一部の機能がコンソールで利用できなくなります。 <br /></br /> サイトのバージョンと一致しないバージョンのコンソールを使用している場合は、サイトの管理がサポートされません。 これによりデータが失われ、サイトが危険にさらされる可能性があります。 たとえば、バージョン 1610 のコンソールを使用して、バージョン 1606 を実行しているサイトを管理することはサポートされません。 |

---
title: "デバイス管理ソリューションの選択 - Configuration Manager | Microsoft Docs"
description: "PC、サーバー、およびデバイスを管理するために System Center Configuration Manager で提供されるソリューションについて説明します。"
ms.custom: na
ms.date: 12/08/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
caps.latest.revision: "14"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 9989ea1bf4cb74a6286ebae9de7614ed622de5b6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="choose-a-device-management-solution-for-system-center-configuration-manager"></a>System Center Configuration Manager のデバイス管理ソリューションの選択

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager (ConfgMgr または SCCM とも呼ばれます) には、PC、サーバー、およびデバイスを管理するためのさまざまなソリューションが備わっています。 管理する必要のあるデバイス プラットフォームや、必要な管理機能に基づいて、適切なソリューションを選択できます。  


##  <a name="overview-of-device-management-solutions"></a>デバイス管理ソリューションの概要  
 この記事では、次の 4 つのデバイス管理ソリューションについて説明します: Configuration Manager クライアント アプリケーション、オンプレミス Configuration Manager インフラストラクチャ、Microsoft Intune、Exchange。 この記事では、各管理ソリューションを[サポートされているモバイル デバイス プラットフォーム別](#compare-device-management-solutions-based-on-supported-mobile-device-platforms)と[管理機能別](#compare-mobile-device-management-solutions-based-on-management-functionality)に比較した 2 つの表を示しています。


###  <a name="manage-devices-with-the-configuration-manager-client"></a>Configuration Manager クライアントを使用してデバイスを管理する  

このオプションでは、デバイスに Configuration Manager クライアント アプリケーションをインストールする必要はありますが、環境内の PC やサーバーなどのデバイスを管理するためのほとんどの機能が提供されます。 詳細については、「[System Center Configuration Manager でのクライアントのインストール方法](/sccm/core/clients/deploy/plan/client-installation-methods)」を参照してください。  

###  <a name="manage-devices-with-on-premises-configuration-manager-infrastructure"></a>オンプレミス Configuration Manager インフラストラクチャを使用してデバイスを管理する  

このオプションでは、一部のデバイス プラットフォームのオペレーティング システムに組み込まれているデバイス管理機能を使用します。 オンプレミス モバイル デバイス管理では、クライアント ベースの管理とは異なりフル機能は提供されませんが、管理するための簡略化された方法が提供されます。この方法では、オンプレミス Configuration Manager リソースを使用して、デバイスのアクセスと管理を行います。 このオプションは、現在 Windows 10 PC と Windows 10 Mobile デバイスのみでサポートされています。  

詳細については、「[Manage mobile devices with on-premises infrastructure in System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)」 (System Center Configuration Manager のオンプレミス インフラストラクチャとともにモバイル デバイスを管理する) を参照してください。  

###  <a name="manage-devices-with-microsoft-intune-hybrid"></a>Microsoft Intune を使用してデバイスを管理する (ハイブリッド)  

このオプションでは、Configuration Manager のオンプレミス リソースを使用する代わりに、Microsoft Intune を使用してデバイスを登録し、管理します。 Intune でデバイスが管理されている場合でも、Configuration Manager コンソールで管理タスクにアクセスできます。 このオプションは、Windows 10 Mobile、Windows Phone、iOS、Mac OS X、Android を含む主要なモバイル デバイス オペレーティング システムをすべてサポートします。 また、組織内の Windows 8.1 と Windows 10 のコンピューターの管理も提供します。  

詳細については、「[System Center Configuration Manager と Microsoft Intune を使用するハイブリッド モバイル デバイス管理 (MDM)](../../mdm/understand/hybrid-mobile-device-management.md)」を参照してください。  

###  <a name="manage-devices-with-microsoft-exchange"></a>Microsoft Exchange を使用してデバイスを管理する  

このオプションでは、Exchange Server コネクタを使用して、Configuration Manager に複数の Exchange サーバーを接続します。 これにより、Exchange ActiveSync に接続できるデバイスが一元的に管理されます。 Configuration Manager コンソールから、複数の Exchange サーバー向けにリモート デバイス ワイプおよび設定コントロールといった、Exchange モバイル デバイス管理機能を構成できます。  

詳細については、「[System Center Configuration Manager と Exchange によるモバイル デバイスの管理](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)」を参照してください。  

これらのデバイス管理ソリューションは、単独で使用することも、相互に組み合わせて使用することもできます。 たとえば、クライアントベースの管理方法を使用して組織内のコンピューターとサーバーの管理を行いつつ、Intune を使用してモバイル デバイスを管理することができます。 このようにアプローチを組み合わせることによって、Configuration Manager コンソールでデバイス管理のすべてのニーズに対応することができます。  

## <a name="compare-device-management-solutions-based-on-supported-mobile-device-platforms"></a>サポートされているモバイル デバイス プラットフォームに基いたデバイス管理ソリューションの比較  

|プラットフォーム|Configuration Manager クライアントを使用|Configuration Manager と Microsoft Intune の併用 (ハイブリッド)|オンプレミス モバイル デバイス管理\-|Configuration Manager と Exchange の併用|  
|--------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Android||○||○|  
|iOS||○||○|  
|Mac OS X|○|||○|  
|UNIX/Linux|○|||○|  
|Windows 10|○|[はい]|[はい]|○|  
|Windows 10 Mobile||○|[はい]|○|  
|Windows (以前のバージョン)|○|[はい]||○|  
|Windows CE|○ (モバイル デバイス レガシ クライアントを使用)|||○|  
|Windows Embedded|○||||  
|Windows Phone||○||○|  
|Windows Server|○|||○|  

 サポート対象プラットフォームの一覧については、「[Supported operating systems for clients and devices for System Center Configuration Manager](configs\supported-operating-systems-for-clients-and-devices.md)」 (System Center Configuration Manager のクライアントとデバイスでサポートされるオペレーティング システム) を参照してください。

##  <a name="bkmk_comp2"></a> 管理機能に基づいたモバイル デバイス管理ソリューションの比較  

|管理機能|Configuration Manager クライアントを使用|Configuration Manager と Microsoft Intune の併用 (ハイブリッド)|オンプレミス モバイル デバイス管理\-|Configuration Manager と Exchange の併用|  
|------------------------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|モバイル デバイスと Configuration Manager 間の公開キー基盤 (PKI) セキュリティ (相互認証と SSL によるデータ転送暗号化を使用)|○|[はい]|○||  
|クライアントのインストール|○||||  
|インターネット経由のサポート|○||||  
|探索|○|||○|  
|ハードウェア インベントリ|○|[はい]|[はい]|○|  
|ソフトウェア インベントリ|○|||○|  
|設定|○|[はい]|[はい]|○|  
|ソフトウェアの展開|○|[はい]|○||  
|フォールバック ステータス ポイントによる監視|○||||  
|管理ポイントへの接続|○||○||  
|配布ポイントへの接続|○||○||  
|Configuration Manager からのブロック|○|[はい]|○||  
|Exchange Server (および Configuration Manager) からの検疫とブロック||||○|  
|リモート ワイプ| |○|[はい]|○|  

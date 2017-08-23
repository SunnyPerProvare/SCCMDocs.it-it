---
title: "デバイスの管理の基礎 | Microsoft ドキュメント"
description: "System Center Configuration Manager を使用してデバイスを管理する方法について説明します。"
ms.custom: na
ms.date: 12/04/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
caps.latest.revision: "6"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 45d84122a86da880268c93ecd994250df6b76c8a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="fundamentals-of-managing-devices-with-system-center-configuration-manager"></a>System Center Configuration Manager を使用したデバイス管理の基礎

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager は、大きく分けて 2 つのカテゴリのデバイスを管理できます。

-   "*クライアント*" は、Configuration Manager クライアント ソフトウェアのインストール先とするデバイスであり、ワークステーション、ノート PC、サーバー、モバイル デバイスなどがあります。 ハードウェア インベントリのような一部の管理機能には、このクライアント ソフトウェアが必要です。  

-   "*管理対象デバイス*" には "*クライアント*" が含まれることもありますが、通常は Configuration Manager クライアント ソフトウェアがインストールされていないモバイル デバイスを指します。 この種のデバイスを管理するには、Intune を使用するか、または Configuration Manager に組み込まれているオンプレミスのモバイル デバイス管理を使用します。

また、クライアントの種類だけでなくユーザーに基づいてデバイスをグループ化および識別することもできます。

## <a name="managing-devices-with-the-configuration-manager-client"></a>Configuration Manager クライアントを使用したデバイスの管理

Configuration Manager クライアント ソフトウェアを使用してデバイスを管理するには、2 つの方法があります。 1 つ目の方法は、ネットワーク上でデバイスを探索し、そのデバイスにクライアント ソフトウェアを展開するというものです。 2 つ目の方法は、新しいコンピューターにクライアント ソフトウェアを手動でインストールし、そのコンピューターをネットワークに参加させるときに、サイトにも参加させるというものです。 クライアント ソフトウェアがまだインストールされていないデバイスを探索するには、組み込まれた探索方法のうちの 1 つまたは複数を実行します。 デバイスが探索されたら、いくつかの方法のいずれかで、クライアント ソフトウェアをインストールします。 探索の使用の詳細については、「[System Center Configuration Manager 用の探索の実行](../../core/servers/deploy/configure/run-discovery.md)」をご覧ください。  

 Configuration Manager クライアント ソフトウェアを実行するようにサポートされているデバイスを検出したら、いくつかの方法のうちの 1 つを使用して、ソフトウェアをインストールできます。 ソフトウェアがインストールされて、クライアントがプライマリ サイトに割り当てられたら、デバイスの管理を開始できます。  一般的なインストール方法には次のものがあります。

 - クライアント プッシュ インストール。

 - ソフトウェアの更新に基づいたインストール。

 - グループ ポリシー。

 - コンピューターへの手動インストール。
 - 展開するオペレーティング システム イメージの一部としてのクライアントの追加。  


 クライアントがインストールされたら、コレクションを使用して、デバイス管理タスクを簡略化できます。 コレクションは、デバイスやユーザーをグループとして管理できるように作成されたデバイスまたはユーザーのグループです。 たとえば、Configuration Manager に登録されているすべてのモバイル デバイスに、モバイル デバイス アプリケーションをインストールすることができます。 この場合は、[すべてのモバイル デバイス] コレクションを使用することができます。  

 詳細については、次のトピックを参照してください。  

-   [System Center Configuration Manager のデバイス管理ソリューションの選択](../../core/plan-design/choose-a-device-management-solution.md)  

-   [System Center Configuration Manager でのクライアントのインストール方法](../../core/clients/deploy/plan/client-installation-methods.md)  

-   [System Center Configuration Manager のコレクションの概要](../../core/clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>クライアント設定  
 Configuration Manager を最初にインストールすると、階層内のすべてのクライアントは既定のクライアント設定で構成されます (これは変更可能です)。 これらのクライアント設定には、次のような構成オプションがあります。

 -  デバイスがサイトと通信する頻度。

 -  クライアントがソフトウェア更新プログラムとその他の管理操作に対してセットアップされているかどうか。

 -  ユーザーがモバイル デバイスを Configuration Manager による管理対象として登録できるかどうか。  

カスタム クライアント設定を作成し、コレクションに割り当てることができます。  カスタム設定が適用されるようにコレクションのメンバーに構成されます。指定する (番号) 順序で適用されるように複数のカスタム クライアントを作成できます。  競合する設定がある場合は、順序番号が最も小さい設定がその他の設定に優先します。  

次の図は、カスタム クライアント設定を作成および適用する方法の例を示します。  

 ![クライアント設定](media/ClientSettings.gif)  

 クライアント設定の詳細については、  
                「[System Center Configuration Manager でクライアント設定を構成する方法](../../core/clients/deploy/configure-client-settings.md)」および「[System Center Configuration Manager のクライアント設定について](../../core/clients/deploy/about-client-settings.md)」をご覧ください。

## <a name="managing-devices-without-the-configuration-manager-client"></a>Configuration Manager クライアントを使用しないデバイス管理  
 Configuration Manager では、クライアント ソフトウェアがインストールされていないデバイスの管理、および Intune によって管理されないデバイスの管理をサポートします。 詳細については、[System Center Configuration Manager でのオンプレミス インフラストラクチャによるモバイル デバイスの管理](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)に関する記事、および「[System Center Configuration Manager と Exchange によるモバイル デバイスの管理](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)」をご覧ください。  

## <a name="user-based-management"></a>ユーザー ベースの管理  
 Configuration Manager では、Active Directory Domain Services ユーザーのコレクションをサポートします。 ユーザー コレクションを使用する場合、コレクションのメンバーによって使用されるすべてのコンピューターにソフトウェアをインストールすることができます。 展開するソフトウェアがユーザーのプライマリ デバイスとして指定されているデバイスのみにインストールされるようにするには、ユーザーとデバイスのアフィニティを設定します。 ユーザーは 1 つまたは複数のプライマリ デバイスを持つことができます。  

 ユーザーがソフトウェア展開のエクスペリエンスを制御できる 1 つの方法は、クライアント インターフェイスである**ソフトウェア センター**を使用することです。 **ソフトウェア センター**は、クライアント コンピューターに自動的にインストールされ、[**スタート**] メニューから実行します。 ユーザーは**ソフトウェア センター**を使用して自分のソフトウェアを管理でき、次のタスクを実行できます。  

-   ソフトウェアのインストール。  

-   勤務時間外にソフトウェアが自動的にインストールされるようにスケジュールする。  

-   Configuration Manager がデバイスにソフトウェアをインストールできるタイミングを構成する。  

-   Configuration Manager でリモート コントロールがセットアップされている場合に、リモート コントロールのアクセス設定を構成する。  

-   管理者が電源管理オプションを設定している場合、そのオプションを構成する。  


 **ソフトウェア センター**内のリンクを使用すると、ユーザーは**アプリケーション カタログ**に接続して、ソフトウェアの参照、インストール、および要求を行えます。 また**アプリケーション カタログ**により、優先設定を構成したり、モバイル デバイスをワイプしたり、設定されている場合はユーザーとデバイスのアフィニティのプライマリ デバイスを指定したりできます。   

 ユーザーはまた、ブラウザーのイントラネットまたはインターネット セッションを通して**アプリケーション カタログ**にアクセスすることができます。  

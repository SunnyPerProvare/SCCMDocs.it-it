---
title: "Configuration Manager 2012 からの変更点 | Microsoft Docs "
description: "System Center 2012 Configuration Manager と比較した System Center Configuration Manger の新機能と変更をご確認いただけます。"
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 3ae68fa6-8b30-45dd-9d12-50bb67cb4a9d
caps.latest.revision: "51"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0a3eb93a99533a1569d8f72ca01d6dfcdc75da20
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="what39s-changed-in-system-center-configuration-manager-from-system-center-2012-configuration-manager"></a>System Center 2012 Configuration Manager からの System Center Configuration Manager の変更点

*適用対象: System Center Configuration Manager (Current Branch)*


 System Center Configuration Manager Current Branch には、System Center 2012 Configuration Manager からの重要な変更点があります。 このトピックでは、System Center Configuration Manager の基準バージョン 1511 における重要な変更点と新機能について紹介します。 System Center Configuration Manager の後続の更新で導入された変更点の詳細については、「[System Center Configuration Manager 増分バージョンの新機能](/sccm/core/plan-design/changes/whats-new-incremental-versions)」を参照してください。



 2015 年 12 月リリースの System Center Configuration Manager (バージョン 1511) は、Microsoft から提供される現在の Configuration Manager 製品の最初のリリースでした。 これは一般に System Center Configuration Manager の Current Branch と呼ばれます。 *Current Branch* は、これが製品の増分更新をサポートするバージョンであることを示します。 さらに、Configuration Manager のこのリリースと以前のリリースを区別する手段も提供します。  

 System Center Configuration Manager:  

-   Configuration Manager 2007 や System Center 2012 Configuration Manager などの過去のバージョンとは異なり、製品名に年や製品識別子を使用していません。

-   製品組み込みの増分更新をサポートしているため、更新プログラム バージョンとも呼ばれます。 最初のリリースはバージョン 1511 でした。 後続のバージョンは、バージョン 1610 のように、コンソール内の更新プログラムとして年に数回リリースされます。
-   基準バージョンを使用してインストールします。 1511 は元の基準バージョンでしたが、新しい基準バージョンも、1702 のように、ときどきリリースされます。 基準バージョンを使用して、新しい System Center Configuration Manager サイトと階層をインストールしたり、サポート対象バージョンの Configuration Manager 2012 からアップグレードしたりすることができます。




##  <a name="bkmk_updates"></a> Configuration Manager のコンソール内更新  
 System Center Configuration Manager では、**更新とサービス**と呼ばれるコンソール内でのサービス提供方式が採られています。この方式により、推奨される更新プログラムを簡単に特定し、インストールすることができます。  

 バージョンによっては、(Configuration Manager コンソール内から) 既存のサイトに対する更新プログラムとしてのみ使用できて、新規 Configuration Manager サイトのインストールに使用できないものがあります。   
たとえば、1610 更新プログラムは、Configuration Manager コンソール内からのみ使用可能です。 任意のバージョンの System Center Configuration Manager を既に実行しているサイトを更新する場合に使用されます。

更新プログラム バージョンも、新しい基準バージョン (更新プログラム 1702 など) として定期的にリリースされます。 このような更新プログラムを使用すれば、古い基準バージョン (1511 など) から開始して最新バージョンまでアップグレードしなくても、新しい階層をインストールできます。


更新プログラムの使用の詳細については、「[System Center Configuration Manager の更新プログラム](../../../core/servers/manage/updates.md)」を参照してください。  
基準の詳細については、「[基準バージョンと更新プログラムのバージョン](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)」を参照してください。

##  <a name="bkmk_servicepoint"></a>新しいサイト システムの役割: サービス接続ポイント  
 **Microsoft Intune コネクタ**は新しいサイト システムの役割に置き換えられ、新たに追加された**サービス接続ポイント**機能が有効になります。 サービス接続ポイント:  

-   Intune を System Center Configuration Manager オンプレミス モバイル デバイス管理と統合するときに、Microsoft Intune コネクタに置き換えられます  

-   管理するデバイスのコンタクト ポイントとして使用します。  

-   展開に関する使用状況データを、Microsoft クラウド サービスにアップロードします  

-   対象の展開に適用する更新プログラムを Configuration Manager 内から利用できるようにします。  

このサイト システムの役割は、オンラインとオフラインの両方の操作モードをサポートしています。 詳細については、「 [About the service connection point in System Center Configuration Manager](../../../core/servers/deploy/configure/about-the-service-connection-point.md)」をご覧ください。  

##  <a name="bkmk_usage"></a> 使用状況データの収集  
 System Center Configuration Manager は、サイトとインフラストラクチャに関する使用状況データを収集します。 この情報がコンパイルされ、サービス接続ポイントによって Microsoft クラウド サービスに送信されます。 使用している Configuration Manager のバージョンに適用される更新プログラムをダウンロードするには、Configuration Manager を有効にする必要があります。 サービス接続ポイントを設定するときには、収集するデータのレベルと、そのデータを自動的に送信するか (オンライン モード)、手動で送信するか (オフライン モード) の両方を設定できます。  

 詳細については、「[使用状況データのレベルと設定](../../../core/servers/deploy/install/setup-reference.md#bkmk_usage)」を参照してください。  

##  <a name="bkmk_AMT"></a> Intel Active Management Technology (AMT) のサポート  
 System Center Configuration Manager では、Configuration Manager コンソール内からの AMT ベースのコンピューターに対するネイティブ サポートは削除されました。 [Microsoft System Center Configuration Manager 用 Intel SCS アドオン](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)を使用すれば、AMT ベースのコンピューターは引き続き完全に管理されます。 アドオンを使用することで、最新の機能にアクセスして AMT を管理できます。Configuration Manager にこれらの変更が組み込まれるまでに適用されていた制限は解除されます。  

System Center Configuration Manager での統合 AMT の削除には、帯域外管理が含まれています。 帯域外管理ポイント サイト システムの役割は、もう使用されず、使用できなくなります。  

System Center 2012 Configuration Manager での帯域外管理は、この変更の影響を受けません。

##  <a name="bkmk_out"></a> 非推奨機能  
 ネイティブな [Intel Active Management Technology (AMT) のサポート](#bkmk_AMT)などのいくつかの機能は、Configuration Manager コンソールから削除されます。 ネットワーク アクセス保護などの他の機能は、完全に削除されます。 さらに、Windows Vista、Windows Server 2008、SQL Server 2008 などの古い Microsoft 製品の一部はサポートされていません。  

 非推奨機能の一覧については、「[System Center Configuration Manager から削除された機能と非推奨の機能](../../../core/plan-design/changes/removed-and-deprecated-features.md)」を参照してください。  

 サポートされる製品、オペレーティング システム、および構成の詳細については、「[System Center Configuration Manager のサポートされている構成](../../../core/plan-design/configs/supported-configurations.md)」を参照してください。  

## <a name="client-deployment"></a>クライアント展開  
 System Center Configuration Manager では、Configuration Manager クライアントの新しいバージョンをテストしてから、この新しいソフトウェアでサイトの他の部分をアップグレードするようにするための新機能を導入しています。 新しいクライアントをパイロット運用するための実稼働前コレクションをセットアップすることができます。 実稼働前環境で新しいクライアント ソフトウェアが正常に動作することを確認した後、その新しいバージョンでサイトの残りの部分を自動的にアップグレードするようにクライアントを昇格できます。  

 クライアントをテストする方法の詳細については、「[System Center Configuration Manager で実稼働前コレクションのクライアント アップグレードをテストする方法](../../../core/clients/manage/upgrade/test-client-upgrades.md)」を参照してください。  

## <a name="operating-system-deployment"></a>オペレーティング システムの展開  

オペレーティング システムの展開に関する次の変更に注意してください。

-   タスク シーケンスの作成ウィザードの **[オペレーティング システムをアップグレード パッケージからアップグレードする]** で、新しいタスク シーケンスの種類を使用できます。 このシーケンスでは、コンピューターを Windows 7、Windows 8、または Windows 8.1 から Windows 10 にアップグレードする手順を作成します。 詳細については、「 [Upgrade Windows to the latest version with System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md)」をご覧ください。  

-   オペレーティング システムを展開するときに、Windows PE ピア キャッシュを利用できるようになりました。 オペレーティング システムを展開するタスク シーケンスを実行しているコンピューターでは、配布ポイントからコンテンツをダウンロードするのではなく、Windows PE ピア キャッシュを使用してローカル ピア (ピア キャッシュ ソース) からコンテンツを取得できます。 これにより、ローカル配布ポイントが存在しないブランチ オフィス シナリオでワイド エリア ネットワーク (WAN) トラフィックが最小限に抑えられます。 詳細については、「 [Prepare Windows PE peer cache to reduce WAN traffic in System Center Configuration Manager](/sccm/osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic)」をご覧ください。  

-   環境内でサービスとして今すぐ Windows の状態を表示できます。 サービス プランを作成して展開リングを形成し、新しいビルドがリリースされたときに Windows 10 Current Branch を最新の状態に維持することもできます。 または、Windows 10 クライアントの Current Branch (CB) または Current Branch for Business (CBB) のビルドのサポート終了に近づいたときにアラートを表示できます。 詳細については、「 [Manage Windows as a service using System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md)」を参照してください。  

## <a name="application-management"></a>アプリケーション管理  

アプリケーション管理に関する次の変更に注意してください。

-   System Center Configuration Manager では、Windows 10 以降を実行しているデバイス用のユニバーサル Windows プラットフォーム (UWP) アプリを展開できます。 「[System Center Configuration Manager での Windows アプリケーションの作成](../../../apps/get-started/creating-windows-applications.md)」を参照してください。  

-   ソフトウェア センターは新しい現代的な外観へと一新されます。 これまではアプリケーション カタログにしか表示されなかったアプリ (ユーザーが利用できるアプリ) がソフトウェア センターの [アプリケーション] タブに表示されるようになりました。 これで、これらの展開を見つけやすくなり、ユーザーがアプリケーション カタログを参照する必要がなくなります。 さらに、Silverlight 対応のブラウザーが必要なくなります。 「[System Center Configuration Manager のアプリケーション管理の計画と構成](../../../apps/plan-design/plan-for-and-configure-application-management.md)」を参照してください。  

-   MDM アプリケーションを介した新しい Windows インストーラーの種類では、Windows インストーラー ベースのアプリを作成して、Windows 10 を実行する登録済み PC に展開できます。 「[System Center Configuration Manager での Windows アプリケーションの作成](../../../apps/get-started/creating-windows-applications.md)」を参照してください。  

-   社内 iOS アプリとしてアプリケーションを作成するときは、アプリのインストーラー (.ipa) ファイルを指定することのみが必要になります。 対応するプロパティ リスト (.plist) ファイルを指定する必要はなくなりました。 「[System Center Configuration Manager での iOS アプリケーションの作成](../../../apps/get-started/creating-ios-applications.md)」を参照してください。  

-   Configuration Manager 2012 では、Windows ストアのアプリへのリンクを指定する場合、リンクを直接指定するか、またはアプリがインストールされているリモート コンピューターを参照します。 System Center Configuration Manager でも、引き続きリンクを直接入力できますが、参照コンピューターを参照するのではなく、Configuration Manager コンソールから直接アプリのストアを参照できるようになりました。  

## <a name="software-updates"></a>ソフトウェア更新プログラム  

ソフトウェア更新プログラムに関する次の変更に注意してください。

-   System Center Configuration Manager では、コンピューターのソフトウェア更新プログラムの管理方法の違いを検出できるようになりました。 具体的には、ソフトウェア更新プログラムの管理のために Windows Update for Business (WUfB) に接続する Windows 10 コンピューターと、ソフトウェア更新プログラムの管理のために Windows Server Update Services (WSUS) に接続するコンピューターとを区別できるようになりました。 **UseWUServer** は新たに導入された属性で、WUfB でコンピューターを管理するかどうかを指定します。 コレクションでこの設定を使用すると、ソフトウェアの更新管理からこれらのコンピューターを除外できます。 詳細については、「 [Integration with Windows Update for Business in Windows 10](../../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md)」をご覧ください。  

-   Configuration Manager コンソールから WSUS クリーンアップ タスクをスケジュールし、実行できるようになりました。 **ソフトウェアの更新ポイント コンポーネント**のプロパティで、WSUS クリーンアップ タスクを実行することを選ぶと、次回、ソフトウェア更新プログラムを最新に保つときにこのタスクが実行されます。 期限切れのソフトウェアの更新プログラムは WSUS サーバー上で拒否状態に設定され、コンピューター上の Windows Update エージェントでこれらのソフトウェア更新プログラムをスキャンできなくなります。 詳細については、「 [Schedule and run the WSUS clean up task](../../../sum/deploy-use/software-updates-maintenance.md)」をご覧ください。  

## <a name="compliance-settings"></a>コンプライアンス設定  

コンプライアンス設定に関する次の変更に注意してください。

-   System Center Configuration Manager では、構成項目を作成するためのワークフローが改良されています。 これで、構成項目を作成し、サポートされているプラットフォームを選択するときに、そのプラットフォームに関連する設定のみが使用できるようになります。 「[System Center Configuration Manager のコンプライアンス設定を使ってみる](../../../compliance/get-started/get-started-with-compliance-settings.md)」を参照してください。  

-   **構成項目の作成**ウィザードでは、作成する構成項目の種類が選択しやすくなりました。 さらに、次のものに対して使用できる構成項目が追加および更新されています。  

    -   Configuration Manager クライアントを使用して管理されている Windows 10 デバイス  

    -   Configuration Manager クライアントを使用して管理されている Mac OS X デバイス  

    -   Configuration Manager クライアントを使用して管理されている Windows デスクトップおよびサーバー コンピューター  

    -   Configuration Manager クライアントを使用せずに管理されている Windows 8.1 および Windows 10 デバイス  

    -   Configuration Manager クライアントを使用せずに管理されている Windows Phone デバイス  

    -   Configuration Manager クライアントを使用せずに管理されている iOS および Mac OS X デバイス  

    -   Configuration Manager クライアントを使用せずに管理されている Android および Samsung KNOX Standard デバイス  

 「[System Center Configuration Manager で構成項目を作成する方法](../../../compliance/deploy-use/create-configuration-items.md)」を参照してください。  

-   Microsoft Intune に登録されているか、Configuration Manager クライアントを使用して管理されている、Mac OS X コンピューター上の設定を管理するためのサポート。 「[System Center Configuration Manager クライアントを使用せずに管理されている iOS デバイスと Mac OS X デバイスの構成項目を作成する方法](../../../compliance/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client.md)」を参照してください。  

## <a name="protect-data-and-site-infrastructure"></a>データとサイト インフラストラクチャの保護  
System Center Configuration Manager を Windows Hello for Business (旧称: Microsoft Passport for Windows) と統合することができます。 Windows Hello for Business は、Active Directory や Azure Active Directory アカウントを使った代替サインイン方法であり、Windows 10 を実行しているデバイス上のパスワード、スマート カード、または仮想スマート カードに取って代わります。 「[System Center Configuration Manager における Windows Hello for Business 設定について](../../../protect/deploy-use/windows-hello-for-business-settings.md)」を参照してください。

## <a name="mobile-device-management-with-microsoft-intune"></a>Microsoft Intune を使用したモバイル デバイスの管理  
 System Center Configuration Manager では、次に挙げるように、モバイル デバイス管理エクスペリエンスが改良されています。  

-   ユーザーが登録できるデバイスの数を制限します。  

-   会社のポータルのユーザーがアプリを登録または使用するために事前に同意する必要がある使用条件を指定します。  

-   大量のデバイスを管理できるようにデバイス登録マネージャーの役割が追加されました。  

Configuration Manager および Intune によるモバイル デバイス管理機能の詳細については、「[System Center Configuration Manager と Microsoft Intune を使用するハイブリッド モバイル デバイス管理 (MDM)](../../../mdm/understand/hybrid-mobile-device-management.md)」を参照してください。  

## <a name="on-premises-mobile-device-management"></a>オンプレミス モバイル デバイス管理  
 オンプレミス Configuration Manager インフラストラクチャを使用してモバイル デバイスを管理できるようになりました。 すべてのデバイス管理と管理データはオンプレミスで処理され、Microsoft Intune またはその他のクラウド サービスの一部ではなくなります。 この種類のデバイスの管理には、クライアント ソフトウェアは必要ありません。 Configuration Manager では、デバイスのオペレーティング システムに組み込まれている機能を使用してデバイスを管理します。  

 詳細については、「[System Center Configuration Manager でオンプレミス インフラストラクチャを使用したモバイル デバイスの管理](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)」を参照してください。

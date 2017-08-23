---
title: "ソフトウェア更新プログラムの前提条件 | Microsoft Docs"
description: "System Center Configuration Manager でのソフトウェア更新プログラムの前提条件について説明します。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: fdf05118-162a-411e-b72e-386b9dc9a5e1
ms.openlocfilehash: 179f076f228daa5adf612275a822cd379b0ce1e3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-software-updates-in-system-center-configuration-manager"></a>System Center Configuration Manager でのソフトウェア更新プログラムの前提条件

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックでは、System Center Configuration Manager でのソフトウェア更新プログラムの前提条件の一覧を示します。 前提条件ごとに、外部の依存関係と内部の依存関係を別の表にまとめています。  

## <a name="software-update-dependencies-external-to-configuration-manager"></a>Configuration Manager 外部のソフトウェア更新プログラムの依存関係  
 次のセクションに、ソフトウェア更新の外部の依存関係の一覧を示します。  

### <a name="internet-information-services-iis"></a>インターネット インフォメーション サービス (IIS)  
 ソフトウェアの更新ポイント、管理ポイント、および配布ポイントを実行するすには、サイト システム サーバーにインターネット インフォメーション サービス (IIS) が置かれている必要があります。 詳細については、「[サイト システムの役割の前提条件](../../core/plan-design/configs/site-and-site-system-prerequisites.md)」を参照してください。  

### <a name="windows-server-update-services-wsus"></a>Windows Server Update Services (WSUS)  
 ソフトウェア更新プログラムの同期と、クライアントでのソフトウェア更新プログラムのコンプライアンス評価スキャンを行うには、WSUS が必要です。 WSUS サーバーは、ソフトウェア更新ポイント サイト システムの役割を作成する前にインストールする必要があります。 ソフトウェアの更新ポイントでは、次のバージョンの WSUS がサポートされています。  

-   WSUS 4 (Windows Server 2012 および Windows Server 2012 R2 における役割)  

-   WSUS 3.2 (Windows Server 2008 R2 における役割)  

 1 つのサイトにソフトウェアの更新ポイントが複数ある場合、すべてのポイントが同じバージョンの WSUS を実行するようにします。  

> [!WARNING]  
>  **アップグレード**のソフトウェア更新プログラムの分類は、WSUS 4.0 以降のみでサポートされています。 この新しい分類を同期し、Windows 10 サービス プランで Windows 10 コンピューターを評価できるようにする前に、ソフトウェアの更新ポイントとサイト サーバーに WSUS の [修正プログラム 3095113](https://support.microsoft.com/kb/3095113) をインストールする必要があります。 この修正プログラムは、Windows 10 の機能アップグレードを同期および配布するために、Windows Server 2012 ベースまたは Windows Server 2012 R2 ベースのサーバーで WSUS を有効にします。 詳細については、「[サービスとしての Windows の管理](../../osd/deploy-use/manage-windows-as-a-service.md)」を参照してください。  
>   
>  [修正プログラム 3095113](https://support.microsoft.com/kb/3095113) をインストールする前に**アップグレード**分類のソフトウェア更新プログラムを同期する場合は、「[KB 3095113 をインストールする前のアップグレード カテゴリの同期からの回復](#BKMK_RecoverUpgrades)」をご覧ください。  

### <a name="wsus-administration-console"></a>WSUS 管理コンソール  
 ソフトウェアの更新ポイントがリモート サイトのシステム サーバー上にあり、WSUS がそのサイト サーバーにインストールされていない場合、Configuration Manager サイト サーバーには WSUS 管理コンソールが必要です。  

> [!IMPORTANT]  
>  サイト サーバーの WSUS バージョンは、ソフトウェアの更新ポイントで実行されている WSUS バージョンと同じにする必要があります。  

> [!IMPORTANT]  
>  WSUS 管理コンソールを使ってWSUS の設定を構成しないでください。 Configuration Manager はソフトウェアの更新ポイントで実行されている WSUS に接続し、適切な設定を構成します。  

### <a name="windows-update-agent-wua"></a>Windows Update エージェント (WUA)  
 クライアントが WSUS サーバーに接続し、コンプライアンス対応スキャンに必要なソフトウェア更新プログラムの一覧を取得するには、WUA クライアントが必要です。  

 Configuration Manager をインストールすると、最新バージョンの WUA がダウンロードされます。 次に、Configuration Manager クライアントをインストールすると、必要に応じて WUA がアップグレードされます。 インストールに失敗した場合は、別の方法で WUA をアップグレードする必要があります。  

## <a name="software-update-dependencies-internal-to-configuration-manager"></a>Configuration Manager 内部のソフトウェア更新プログラムの依存関係  
 次のセクションに、Configuration Manager のソフトウェア更新の内部の依存関係の一覧を示します。  

### <a name="management-points"></a>管理ポイント  
 管理ポイントは、クライアント コンピューターと Configuration Manager サイト間で情報を転送します。 これらはソフトウェア更新プログラムのために必要です。  

### <a name="software-update-point"></a>ソフトウェアの更新ポイント  
 Configuration Manager でソフトウェア更新プログラムを展開できるようにするには、ソフトウェアの更新ポイントを WSUS サーバーにインストールする必要があります。 詳細については、「[ソフトウェアの更新ポイントのインストールと構成](../get-started/install-a-software-update-point.md)」を参照してください。

### <a name="distribution-points"></a>配布ポイント  
 ソフトウェア更新プログラムのコンテンツを保存できる配布ポイントが必要です。 配布ポイントをインストールして、コンテンツを管理する方法の詳細については、「[コンテンツとコンテンツ インフラストラクチャの管理](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md)」を参照してください。  

### <a name="client-settings-for-software-updates"></a>ソフトウェア更新プログラムのクライアントの設定  
 既定で、クライアントのソフトウェア更新プログラムは有効です。 ただし、クライアントがソフトウェア更新プログラムのコンプライアンスを評価する方法とタイミングを制御し、ソフトウェア更新プログラムのインストール方法を制御するために使用できるその他の設定があります。  

 詳細については、次をご覧ください。  

-   [ソフトウェア更新プログラムのクライアントの設定](../get-started/manage-settings-for-software-updates.md#a-namebkmkclientsettingsa-client-settings-for-software-updates)  

-   [ソフトウェア更新プログラムのクライアントの設定](../../core/clients/deploy/about-client-settings.md#software-updates)トピック  

### <a name="reporting-services-point"></a>レポート サービス ポイント  
 レポート サービス ポイントのサイト システムの役割は、ソフトウェア更新プログラムのレポートを表示できます。 この役割は任意ですが、使用することをお勧めします。 レポート サービス ポイント作成の詳細については、「[レポートの構成](../../core/servers/manage/configuring-reporting.md)」を参照してください。  

##  <a name="BKMK_RecoverUpgrades"></a> KB 3095113 をインストールする前のアップグレード カテゴリの同期からの回復  
 **アップグレード**分類を同期する前に、ソフトウェアの更新ポイントとサイト サーバーに WSUS の[修正プログラム 3095113](https://support.microsoft.com/kb/3095113) をインストールする必要があります。 **アップグレード** 分類が有効になっているときに修正プログラムがインストールされていない場合、WSUS は関連付けられているパッケージを適切にダウンロードおよび展開できない場合でも、Windows 10 ビルド 1511 の機能アップグレードを表示します。 [修正プログラム 3095113](https://support.microsoft.com/kb/3095113)を最初にインストールせずにアップグレードを同期する場合、アップグレードを適切に展開するには、WSUS データベース (SUSDB) に、クリアする必要がある使用不可のデータを読み込みます。  この問題から回復するには、次の手順を実行します。  

#### <a name="to-recover-from-synchronizing-the-upgrades-classification-before-you-install-kb-3095113"></a>KB 3095113 をインストールする前に、アップグレード分類の同期から回復するには  

1.  アップグレード分類のソフトウェア更新プログラムを削除します。 次のサンプル スクリプトのような PowerShell スクリプトを使用することができます。  

    ```  
    $Server = Get-WSUSServer  
    $Config = $Server.GetConfiguration()  
    $Update10563 = “df4e45a3-946d-4467-b3fd-8621174bb666”  
    $UpdateGUID = New-Object Guid($Update10563)  
    $Server.DeleteUpdate($UpdateGUID)  
    ```  

    > [!IMPORTANT]  
    >  次の手順に進む前に、Configuration Manager 階層内のすべてのソフトウェアの更新ポイントでスクリプトを実行する必要があります。  

     アップグレード分類のソフトウェア更新プログラムを一括で削除するために、txt ファイルから複数の GUID を読み取るように PowerShell スクリプトを変更できます。  

2.  ソフトウェア更新プログラムの [**アップグレード**] 分類チェック ボックスをオフにし (詳細については、「[分類と製品の構成](../get-started/configure-classifications-and-products.md)」を参照してください)、ソフトウェア更新プログラムの同期を開始します (詳細については、「[ソフトウェア更新プログラムの同期](../get-started/synchronize-software-updates.md)」を参照してください)。  

3.  ソフトウェアの更新ポイントとサイト サーバーに、WSUS の [修正プログラム 3095113](https://support.microsoft.com/kb/3095113) をインストールする必要があります。  

4.  ソフトウェア更新プログラムの [**アップグレード**] 分類チェック ボックスをオンにし (詳細については、「[分類と製品の構成](../get-started/configure-classifications-and-products.md)」を参照してください)、ソフトウェア更新プログラムの同期を開始します (詳細については、「[ソフトウェア更新プログラムの同期](../get-started/synchronize-software-updates.md)」を参照してください)。  

## <a name="next-steps"></a>次のステップ
[ソフトウェア更新管理の準備](../get-started/prepare-for-software-updates-management.md)

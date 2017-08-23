---
title: "System Center Configuration Manager バージョン 1602 の新機能 | Microsoft Docs"
description: "System Center Configuration Manager のバージョン 1602 の変更点および導入された新機能について詳しく説明します。"
ms.custom: na
ms.date: 12/30/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4021eca1-adfb-4e5a-adee-159263c29637
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.openlocfilehash: 9a548f43625a907173e7b967d26356bd80f1c5d9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="what39s-new-in-version-1602-of-system-center-configuration-manager"></a>System Center Configuration Manager のバージョン 1602 の新機能

*適用対象: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager の更新プログラム 1602 は、以前にインストール済みで、バージョン 1511 を実行するサイトを対象とする、コンソール内の更新プログラムとしてのみ使用可能な更新プログラムです。 バージョン 1511 は、新しい Configuration Manager サイトのインストールに使用する初期の基準バージョンです。  


> [!TIP]  
>  詳細については、下記のリンクをクリックしてください。  
>   
>   -   [新しいサイトをインストールする](/sccm/core/servers/deploy/install) (1511 などの基準バージョンを使用)  
>   -   [サイトで更新プログラムをインストールする](/sccm/core/servers/manage/updates) (更新プログラム 1602 など)  

 以降のセクションでは、Configuration Manager のバージョン 1602 の変更点および導入された新機能について詳しく説明します。  

## <a name="site-infrastructure"></a>サイトのインフラストラクチャ  

###  <a name="bkmk_UpgradeOS"></a> Windows Server 2008 R2 を実行するサイト サーバーのオペレーティング システムのインプレース アップグレード  
 1602 またはそれ以降のバージョンを実行する Configuration Manager サイトでは、Windows Server 2008 R2 から Windows Server 2012 R2 へのサイト サーバーのオペレーティング システムのインプレース アップグレードをサポートします。  

> [!WARNING]  
>  Windows Server 2012 R2 にアップグレードする前に、サーバーから WSUS 3.2 をアンインストールする必要があります。  
>   
>  この重要な手順の詳細については、Windows Server ドキュメントの「[Windows Server Update Services の概要](https://technet.microsoft.com/library/hh852345.aspx)」の「新機能と変更された機能」セクションを参照してください。  

 サーバーをアップグレードするには、Windows Server 2012 R2 のアップグレード手順を使用します。 アップグレード後に Configuration Manager サイト サーバーの復元を実行する必要はありません。 アップグレード手順については、Windows Server のドキュメントの「[Windows Server 2012 R2 のアップグレード オプション](https://technet.microsoft.com/library/dn303416.aspx)」をご覧ください。  

###  <a name="bkmk_AOAG"></a> SQL Server AlwaysOn 可用性グループ  
 高可用性と障害復旧ソリューションとして、SQL Server AlwaysOn 可用性グループを使用して、プライマリ サイトと中央管理サイトでサイト データベースをホストします。  

 詳細については、「[System Center Configuration Manager 用の高可用性サイト データベースの SQL Server AlwaysOn](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)」を参照してください。  

## <a name="operating-system-deployment"></a>オペレーティング システムの展開  

### <a name="windows-10-servicing"></a>Windows 10 サービス  
 Configuration Manager バージョン 1602 には、Windows 10 のサービスに対する次の機能強化が追加されました。  

-   サービス プランに新しいフィルター オプションを使用して、**[言語]**、**[必須]**、および **[タイトル]** でフィルターできます。 指定された条件を満たすアップグレードだけが、関連付けられている展開に追加されます。  

-   ソフトウェア更新プログラムの同期で、**アップグレード**分類を選択した場合は、警告が表示されます。 この警告は、ソフトウェアの更新を正常に同期させ、さらに Windows 10 サービスを適切に機能させるには、その前に Windows Server Update Services (WSUS) 4.0 の[修正プログラム 3095113](https://support.microsoft.com/kb/3095113) が必要であることを知らせます。 警告メッセージから、関連するサポート技術情報の記事に移動できます。  

-   利用可能な Windows 10 アップグレードは、Configuration Manager コンソールの **[Windows 10 のサービス]** \ **[すべての Windows 10 更新プログラム]** ノードにのみ表示されるようになりました。 これらの更新プログラムは、コンソールの **[ソフトウェア更新プログラム]** \ **[すべてのソフトウェア更新プログラム]** ノードには表示されなくなりました。  

-   サービス プランは危険度の高い展開であると見なされるようになりました。**[コレクションの選択]** ウィンドウには、サイトのプロパティで構成されている展開の検証の設定に適合するカスタム コレクションのみが表示されます。 詳細については、「 [Settings to manage high-risk deployments for System Center Configuration Manager](../../../protect/understand/settings-to-manage-high-risk-deployments.md)」をご覧ください。  

-   Windows 10 へのアップグレード パッケージを今すぐ開始するユーザーには、オペレーティング システムをアップグレードすることを知らせるメッセージが表示されます。  

## <a name="application-management"></a>アプリケーション管理  

### <a name="ios-app-configuration-policies"></a>iOS アプリ構成ポリシー  
 ユーザーが iOS アプリを実行するときに必要となる可能性がある設定を Configuration Manager アプリ構成ポリシーで指定できます。 たとえば、アプリでは、カスタム ポート番号、言語、セキュリティの設定、または会社のロゴなどのブランド設定をユーザーが指定することが必要になる場合があります。 これらの設定を誤って入力すると、ヘルプ デスクの負荷が増加し、新しいアプリの採用も遅くなる可能性があります。  

 アプリ構成ポリシーを使用すると、ユーザーがアプリを実行する前にこれらの設定をポリシー内のユーザーに展開できるため、上記の問題を排除するのに役立ちます。 設定が自動的に指定されるため、ユーザーの操作は不要です。 詳細については、「[Configure iOS apps with app configuration policies in System Center Configuration Manager](../../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md)」 (System Center Configuration Manager でのアプリ構成ポリシーを使用した iOS アプリの構成) を参照してください。  

### <a name="manage-volume-purchased-ios-apps"></a>Manage volume-purchased iOS apps  
 Configuration Manager は、Apple Volume-Purchase Program (VPP) から一括で購入したアプリの展開と管理に役立ちます。 Configuration Manager では、App Store からライセンス情報をインポートし、使用したライセンスの数を追跡します。  

 詳細については、「[Manage volume-purchased iOS apps with System Center Configuration Manager](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md)」 (System Center Configuration Manager でのボリューム購入 iOS アプリの管理) を参照してください。  

### <a name="automatic-creation-of-office-mobile-apps"></a>Office モバイル アプリの自動作成  
 1511 からバージョン 1602 に更新すると、Configuration Manager は Android および iOS 用の次の Microsoft Office モバイル アプリを自動的に作成します。  

-   Microsoft Word  

-   Microsoft Excel  

-   Microsoft PowerPoint  

-   Microsoft OneDrive  

-   Microsoft OneNote (iOS のみ)  

-   Microsoft Outlook  

これらのアプリは、Configuration Manager コンソールの **[アプリケーション]** ノードに表示されます。  

 アプリケーションの展開の詳細については、「[System Center Configuration Manager でアプリケーションを展開する方法](../../../apps/deploy-use/deploy-applications.md)」をご覧ください。  

## <a name="software-updates"></a>ソフトウェア更新プログラム  

### <a name="manage-office-365-client-updates"></a>Office 365 のクライアント更新プログラムの管理  
 System Center Configuration Manager では、ソフトウェア更新プログラムの管理ワークフローを使用して、Office 365 のクライアント更新プログラムを管理できます。 詳細については、「[System Center Configuration Manager での Office 365 ProPlus の更新プログラムの管理](/sccm/sum/deploy-use/manage-office-365-proplus-updates)」をご覧ください。  

## <a name="compliance-settings"></a>コンプライアンス設定  

### <a name="compliance-settings-for-devices-running-windows-10-team"></a>Windows 10 Team を実行するデバイスのコンプライアンス設定  
 **Windows 8.1 および Windows 10** の構成項目に新しい設定が追加されました。 これらの設定は、Surface Hub デバイスなどの Windows 10 Team を実行するデバイスの制御に役立ちます。  

 詳細については、「[System Center Configuration Manager クライアントを使用せずに管理されている Windows 8.1 デバイスと Windows 10 デバイスの構成項目を作成する方法](../../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)」をご覧ください。  

### <a name="kiosk-mode-settings-for-android-samsung-knox-standard-devices"></a>Android Samsung KNOX Standard デバイスのキオスク モードの設定  
 キオスク モードでは、特定の機能のみ実行できるようにデバイスをロックできます。 たとえば、指定した 1 つの管理対象アプリの実行のみをデバイスに許可することや、デバイスのボリューム ボタンを無効にすることができます。 これらの設定は、デバイスのデモ モデルや、POS デバイスなどの 1 つの機能の実行専用のデバイス向けに使用できます。 Configuration Manager では、Samsung KNOX Standard デバイスのキオスク モードの設定を指定できるようになりました。  

 詳細については、「[System Center Configuration Manager クライアントを使用せずに管理されている Android デバイスと Samsung KNOX Standard デバイスの構成項目を作成する](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md)」を参照してください。  

## <a name="conditional-access"></a>条件付きアクセス  

### <a name="conditional-access-for-pcs-managed-by-system-center-configuration-manager"></a>System Center Configuration Manager が管理する PC の条件付きアクセス  
 このリリースより前に PC の条件付きアクセスを設定するには、PC が Intune に登録されているか、またはドメインに参加している PC である必要がありました。 1602 更新プログラムより、System Center Configuration Manager が管理する PC の条件付きアクセスがサポートされます。 System Center Configuration Manager によって管理される PC では、設定したコンプライアンス ポリシーに準拠しているデバイスのみが Exchange Online と SharePoint Online にアクセスできるように制限できます。  

 詳細については、「[Manage access to O365 services for PCs managed by System Center Configuration Manager](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)」 (System Center Configuration Manager で管理されている PC の O365 サービスへのアクセスを管理する) をご覧ください。  

### <a name="restricting-access-based-on-the-health-of-devices"></a>デバイスの正常性に基づいてアクセスを制限する  
 正常性構成証明サービスで報告されるデバイスの正常性に基づいて、電子メールおよび 0ffice 365 サービスへのアクセスを制限できるようになりました。 さらに、Intune で管理されているデバイスが、デバイスの正常性レポートに含まれます。  

 新しいコンプライアンス ルールが Configuration Manager コンソールに追加されました。このルールを使用すると、デバイスの正常性の状態に基づいてアクセスを許可するかブロックするかを指定できます。 正常性構成証明サービスの詳細、およびデバイスの正常性が Intune でどのように報告されるのかについての詳細は、「[System Center Configuration Manager の正常性構成証明書](../../../core/servers/manage/health-attestation.md)」をご覧ください。  

### <a name="new-compliance-policy-rules"></a>新しいコンプライアンス ポリシーの規則  
 より適切なセキュリティ要件をサポートするために、自動更新、デバイスのロックを解除するために必要なパスワードなど、新しいコンプライアンス ポリシー規則が追加されました。

 詳細については、「[System Center Configuration Manager でのデバイス コンプライアンス ポリシー](../../../protect/deploy-use/device-compliance-policies.md)」をご覧ください。  

### <a name="make-sure-enrolled-and-compliant-devices-always-have-access-to-exchange-on-premises"></a>登録された準拠デバイスがいつも Exchange On-Premises ポリシーにアクセスできるかどうかを確認します。  
 **[既定の規則より優先 - Intune に登録された準拠デバイスに Exchange On-Premises へのアクセスを常に許可する]** オプションをオンにすると、Intune に登録されていてコンプライアンス ポリシーに準拠しているデバイスが Exchange On-Premises にアクセスすることを許可されます。 この規則は、Exchange On-Premises の**条件付きアクセス ポリシーの構成ウィザード**の **[全般]** ページにあります。

 このルールは既定のルールに優先します。つまり、アクセスを検疫またはブロックする既定のルールを設定した場合でも、登録された準拠デバイスは引き続きオンプレミスの Exchange にアクセスできます。 登録された準拠デバイスが Exchange On-Premises 経由で電子メールにいつでもアクセスできるようにするには、この設定を使用します。   

 詳細のウォークスルーについては、「[System Center Configuration Manager でのメール アクセスの管理](../../../protect/deploy-use/manage-email-access.md)」をご覧ください。  

## <a name="client-management"></a>クライアント管理  

### <a name="client-online-status"></a>クライアントのオンライン状態  
 コンピューターがオンラインかどうかを監視するために、クライアントに関する新しい状態を利用できます。 割り当てられている管理ポイントに接続されているコンピューターは、オンラインであると見なされます。 コンピューターがオンラインであることを示すには、クライアントが ping のようなメッセージを管理ポイントに送信します。 5 分経過しても管理ポイントがメッセージを受信しないと、クライアントはオフラインであると見なされます。  

 詳細については、「[System Center Configuration Manager でクライアントを監視する方法](../../../core/clients/manage/monitor-clients.md)」をご覧ください。  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>ソフトウェア センターから PC コンピューターとユーザーのポリシーを更新する  
 新しいオプションである **同期ポリシー** が、ソフトウェア センターの **[オプション]** > **[コンピューターのメンテナンス]** ページに追加されました。これにより、PC では Configuration Manager コンピューターとユーザーのポリシーが更新されます。  

### <a name="software-center-branding-changes"></a>ソフトウェア センターのブランド変更  
 ソフトウェア センターに表示される色、組織名、およびアイコンを変更できます。 これらの設定は、次の規則に従って適用されます。  

- アプリケーション カタログ Web サイトのポイント サイト サーバーの役割がインストールされていない場合は、[**ソフトウェア センターに表示される組織名**] という [**コンピューター エージェント**] クライアント設定で指定された組織名がソフトウェア センターに表示されます。  

- アプリケーション カタログ Web サイトのポイント サイト サーバーの役割がインストールされている場合は、アプリケーション カタログ Web サイトのポイント サイト サーバーの役割プロパティに指定されている組織名と色がソフトウェア センターに表示されます。  

- Microsoft Intune サブスクリプションが構成されていて Configuration Manager 環境に接続されている場合は、Intune サブスクリプションのプロパティに指定されている組織名、色、および会社のロゴがソフトウェア センターに表示されます。  

### <a name="health-attestation"></a>正常性構成証明  
 管理者は、Configuration Manager コンソールで Windows 10 デバイス正常性構成証明の状態を確認できます。 この機能は、Configuration Manager および Configuration Manager と Microsoft Intune の併用で利用できます。 デバイスの正常性構成証明で、管理者はクライアント コンピューターで次の信頼できる BIOS、TPM、およびブート ソフトウェアの構成が有効になっていることを確認できます。  

-   起動時マルウェア対策  

-   BitLocker  

-   セキュア ブート  

-   コードの整合性  

詳細については、「[System Center Configuration Manager の正常性構成証明書](../../../core/servers/manage/health-attestation.md)」をご覧ください。  

### <a name="improvements-to-endpoint-protection-antimalware-settings"></a>Endpoint Protection マルウェア対策の設定の機能強化  
 1602 では、Windows Defender の Endpoint Protection マルウェア対策ポリシーに次の新しい設定が追加されました。  

-   リアルタイム保護: 望ましくない可能性のあるアプリケーションのダウンロード時およびインストール前にブロックします。  

-   スキャンの設定: フル スキャンの実行時にマップされたネットワーク ドライブをスキャンします。  

-   自動サンプル ファイルの送信の設定:  

     マルウェア対策エンジンは、さらに詳しい分析のために Microsoft へのファイルのサンプルの送信を要求することがあります。 既定では、このようなサンプルを送信する前に必ず確認が求められます。 管理者は、この動作を構成する次の設定を管理できるようになりました。  

    -   詳細設定: サンプル ファイルの自動送信を有効にすると、マイクロソフトは検出された特定の項目が危険であるかどうかを判断できます。  

    -   詳細設定: サンプル ファイルの自動送信の設定を変更することをユーザーに許可します。  

    さらに、Endpoint Protection マルウェア対策ポリシーの [除外の設定] セクションの既存の **[ファイルとフォルダーを除外する]** 設定でデバイスを除外できるようになりました。  

詳細については、「[System Center Configuration Manager で Endpoint Protection 用にマルウェア対策ポリシーを作成し展開する方法](../../../protect/deploy-use/endpoint-antimalware-policies.md)」をご覧ください。  

## <a name="mobile-device-management"></a>モバイル デバイス管理  

### <a name="ios-activation-lock"></a>iOS のアクティベーション ロック  
 Configuration Manager は、iOS 7.1 以降のデバイス向けの iPhone を探すアプリの機能である iOS のアクティベーション ロックを管理するために役立ちます。 iPhone を探すアプリをデバイスで使用すると、アクティブ化ロックが自動的に有効になります。 有効になると、ユーザーの Apple ID とパスワードを入力しない限り、以下の操作を実行できなくなります。  

-   iPhone を探すアプリをオフにする。  

-   デバイスを消去する。  

-   ディスクを再アクティブ化する。  

Configuration Manager では、iOS 7.1 以降を実行している監視対象と監視対象外の両方のデバイスのアクティベーション ロックの状態を要求できます。 監視対象デバイスの場合には、Configuration Manager はアクティベーション ロックのバイパス コードを取得して、直接デバイスに発行できます。  

 詳細については、「[System Center Configuration Manager でアクティベーション ロックのバイパスを使用して iOS デバイスを保護する](/sccm/mdm/deploy-use/manage-ios-activation-lock)」をご覧ください。  

### <a name="monitor-terms-and-conditions-deployments"></a>使用条件の展開の監視  
 Configuration Manager コンソールで使用条件の展開を監視できます。  

 使用条件の展開を展開の一覧から選択します。 概要領域には、以下の統計情報が表示されます。  

-   **[対応]**: ユーザーが最新バージョンの使用条件に同意しました  

-   **エラー**  

-   **[非対応]**: ユーザーが最新のバージョンではない使用条件に同意しました  

-   **[不明]**: 登録済みデバイスのない使用条件を含めて、ユーザーが使用条件に同意したことはありません  

---
title: "モバイル デバイスの管理 | Microsoft Docs"
description: "System Center Configuration Manager で Exchange Server コネクタを使用してモバイル デバイスを管理します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: aba688d9-fd5b-4c42-8cb4-f7e1b161ef50
caps.latest.revision: "8"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 44958bc35586f5e57ab3fb59681bfb018d2bd5da
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="manage-mobile-devices-with-system-center-configuration-manager-and-exchange"></a>System Center Configuration Manager と Exchange によるモバイル デバイスの管理

*適用対象: System Center Configuration Manager (Current Branch)*

Microsoft Exchange ActiveSync プロトコルを使って Exchange Server (社内またはオンライン) に接続するモバイル デバイスを管理したいけれども、Configuration Manager でそのデバイスを登録できない場合は、System Center Configuration Manager の Exchange Server コネクタを使います。 Configuration Manager コンソールから、複数の Exchange サーバー向けにリモート デバイス ワイプおよび設定コントロールといった、Exchange モバイル デバイス管理機能を構成できます。  

 ![configmgr&#45;with&#45;exchange](../../mdm/deploy-use/media/configmgr-with-exchange.png "configmgr-with-exchange")  

 Exchange Server コネクタを使ってモバイル デバイスを管理するときは、モバイル デバイスに Configuration Manager クライアントをインストールしません。 そのため、使用できる管理機能が限られています。 たとえば、管理対象のモバイル デバイスにソフトウェアをインストールしたり、構成項目を使用したりすることはできません。 Configuration Manager でモバイル デバイス用に使用できるさまざまな管理機能の詳細については、「[Choose a device management solution for System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)」 (System Center Configuration Manager のデバイス管理ソリューションの選択) を参照してください。  

> [!IMPORTANT]  
>  Exchange Server コネクタをインストールする前に、使用する Microsoft Exchange のバージョンが Configuration Manager でサポートされているかどうかを確認してください。 詳細については、「[System Center Configuration Manager のサイトおよびクライアントのサポートされるオペレーティング システム](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers)」の「Exchange Server コネクタ」を参照してください。  

 Exchange Server コネクタを使用すると、既定の Exchange ActiveSync メール ボックス ポリシーでの代わりに、Configuration Manager で構成した設定でモバイル デバイスを管理することができます。 使用する設定は、 **[全般]**、 **[パスワード]**、 **[電子メール管理]**、 **[セキュリティ]**、 **[アプリケーション]**のグループに分けて定義します。 たとえば、[ **パスワード** ] グループでは、モバイル デバイスでパスワードを必要とするかどうか、パスワードに最低限必要な文字数と複雑さ、パスワードを回復可能にするかどうかを設定します。  

 グループで 1 つでも設定を行うと、Configuration Manager がグループのすべてのモバイル デバイス用設定を管理します。 グループにあるどの設定も構成しないと、モバイル デバイスの該当する設定が Exchange Server によって管理されます。 その場合でも、Exchange Server で設定され、ユーザーに割り当てられた Exchange ActiveSync メールボックス ポリシーは適用されます。  

 また、Exchange Server コネクタで、モバイル デバイスから Exchange へのアクセスを許可、ブロック、検疫するための規則を設定することもできます。 モバイル デバイスをリモートでワイプするには Configuration Manager コンソールを使います。一方、ユーザーが自分のモバイル デバイスをリモートでワイプするには、アプリケーション カタログを使います。  

 Exchange Server が社内にある場合は、ユーザーのモバイル デバイスが Exchange Server コネクタによって管理されているときに、アプリケーション カタログに自動的に表示されます。 一方、Microsoft Exchange Online 用の Exchange Server コネクタでは、ユーザーのモバイル デバイスがアプリケーション カタログに表示されるようにするには、ユーザーとデバイスのアフィニティを手動で構成する必要があります。 ユーザーとデバイスのアフィニティを手動で構成する方法については、「[System Center Configuration Manager でのユーザーとデバイスのアフィニティへのユーザーとデバイスの関連付け](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)」を参照してください。  

> [!TIP]  
>  モバイル デバイスを Exchange Server コネクタで管理しているときに、そのモバイル デバイスの所有者が変わった場合は、新しい所有者がモバイル デバイスで自分の Exchange アカウントを構成する前に、Configuration Manager コンソールからモバイル デバイスを削除してください。  

## <a name="required-security-permissions"></a>必要なセキュリティのアクセス許可  
 Exchange Server コネクタを構成するには、次のセキュリティのアクセス許可を持っている必要があります。  

-   Exchange Server コネクタを追加、変更、削除する: **サイト** オブジェクトの **変更** のアクセス許可。  

-   モバイル デバイス設定を構成する: **サイト** オブジェクトの **ModifyConnectorPolicy** のアクセス許可。  

 **[完全な権限を持つ管理者]** のセキュリティの役割には、Exchange Server コネクタを構成するために必要な許可が含まれています。  

 モバイル デバイスを管理するには、次のセキュリティのアクセス許可が必要です。  

-   モバイル デバイスをワイプする: **コレクション** オブジェクトの **リソースの削除** 。  

-   ワイプ コマンドを取り消す: **コレクション** オブジェクトの **リソースの変更** 。  

-   モバイル デバイスを許可またはブロックする: **コレクション** オブジェクトの **リソースの変更**  

 **[オペレーション管理者]** のセキュリティの役割には、Exchange Server コネクタを使用してモバイル デバイスを管理するために必要な許可が含まれています。  

 セキュリティのアクセス許可を構成する方法の詳細については、「[System Center Configuration Manager のロール ベース管理の構成](../../core/servers/deploy/configure/configure-role-based-administration.md)」を参照してください。  

## <a name="installing-and-configuring-an-exchange-server-connector"></a>Exchange Server コネクタのインストールと構成  
 モバイル デバイスを管理するように Exchange Server コネクタをインストールし構成するには次の手順に従います。 Configuration Manager では、1 つの Exchange 組織に設定できるコネクタは 1 つのみです。 これらの手順を完了すると、モバイル デバイスを表示するコレクションを表示するとき、およびモバイル デバイスのレポートを使用するとき、コネクタによって検索され管理されるモバイル デバイスを監視できます。  

> [!NOTE]  
>  Configuration Manager は、*ユーザー名*_*デバイスの種類*という形式を使用して見つかったモバイル デバイスに名前を付けます。 あるユーザーが同じ種類のモバイル デバイスを複数持っているときは、それらのモバイル デバイスについて、Configuration Manager はコンソールおよびレポートに同じ名前を表示します。  

#### <a name="to-install-and-configure-an-exchange-server-connector"></a>Exchange Server コネクタをインストールし構成するには  

1.  どのアカウントを Exchange クライアント アクセス サーバーに接続しモバイル デバイスを管理するかを判断します。 アカウントは、サイト サーバーのコンピューター アカウントでも、Windows ユーザー アカウントでも構いません。 そのアカウントで、次の Exchange Server コマンドレットを実行するように構成します。  

    -   **Clear-ActiveSyncDevice**  

    -   **Get-ActiveSyncDevice**  

    -   **Get-ActiveSyncDeviceAccessRule**  

    -   **Get-ActiveSyncDeviceStatistics**  

    -   **Get-ActiveSyncMailboxPolicy**  

    -   **Get-ActiveSyncOrganizationSettings**  

    -   **Get-ExchangeServer**  

    -   **Get-Recipient**  

    -   **Set-ADServerSettings**  

    -   **Set-ActiveSyncDeviceAccessRule**  

    -   **Set-ActiveSyncMailboxPolicy**  

    -   **Set-CASMailbox**  

    -   **New-ActiveSyncDeviceAccessRule**  

    -   **New-ActiveSyncMailboxPolicy**  

    -   **Remove-ActiveSyncDevice**  

    > [!NOTE]  
    >  次の Exchange Server の管理の役割には、受信者管理、表示限定の組織管理、サーバー管理のコマンドレットが含まれます。 Microsoft Exchange Server 2010 の管理役割グループの詳細については、「 [管理役割グループについて](http://go.microsoft.com/fwlink/p/?LinkId=212914)」を参照してください。  

    > [!TIP]  
    >  必要なコマンドレットなしで Exchange Server コネクタをインストールしたり、使おうとしたりすると、サイト サーバー コンピューターの EasDisc.log ログ ファイルに、「 `Invoking cmdlet <cmdlet> failed` 」というメッセージが記録されます。  

2.  Configuration Manager コンソールで、[ **管理**] をクリックします。  

3.  **[管理]** ワークスペースで、**[階層の構成]** を展開し、**[探索方法]** をクリックします。  

4.  **[ホーム]** タブの **[作成]** グループで **[Exchange Server の追加]** をクリックします。  

5.  以下の手順で、Exchange Server の追加ウィザードを完了します。  

    -   社内にある Exchange Server インスタンスを使用する場合は、クライアント アクセス サーバーを指定するときに、各 Active Directory サイト用に 1 台のサーバーまたはクライアント アクセス サーバー アレイを指定することができます。 サーバーまたはアレイがオフラインの場合は、Configuration Manager が使用するクライアント アクセス サーバーを検出しようとします。 失敗した場合、Configuration Manager はメール ボックス サーバーの使用にフォールバックして、クライアント アクセス サーバーに接続します。 この動作は、サイト サーバー コンピューターの EasDisc.log ファイルに警告として記録されます。 たとえば、「 `Failed to open runspace for site <site_name>`」というメッセージを探してみてください。  

    -   Exchange Server のコネクタ アカウントでは、手順 1 で構成したアカウントを指定します。  

    -   Configuration Manager を使用してモバイル デバイスを登録している場合、**[外部のモバイル デバイス管理]** オプションを有効にして、これらのモバイル デバイスが、Configuration Manager がデバイスを登録した後も引き続き Exchange から電子メールを受信し続けるようにします。  

    -   ウィザードの **[アカウント]** ページで、Configuration Manager 条件付きアクセスによってブロックされているクライアントにメール通知を送信するために使用するアカウントを構成できます。 指定するアカウントには、Exchange サーバー上の有効なメールボックスが必要です。  

         詳細については、「[System Center Configuration Manager でサービスへのアクセスを管理する](../../protect/deploy-use/manage-access-to-services.md)」を参照してください。  

6.  ステータス メッセージとログ ファイルで、Exchange Server コネクタがインストールされていることを確認できます。  

    -   サイト コンポーネント マネージャーが Exchange Server コネクタに正常にインストールされたことを確認するには、 **SMS_EXCHANGE_CONNECTOR** コンポーネントのステータス ID **1015** を探します。 Configuration Manager がコネクタを正常にインストールできない場合 (たとえば、指定したクライアント アクセス サーバーのコンピューターがオフラインであるため)、インストールが成功するか Exchange Server コネクタを削除するまで、Configuration Manager は 60 分ごとにインストールを再試行します。  

    -   サイト サーバー コンピューターにある SiteComp.log ファイルを見つけ、そのファイル内で「 `Component SMS_EXCHANGE_CONNECTOR flagged for installation`」というメッセージを探します。 インストールが正常に完了していると、「 `STATMSG: ID=1015`」という値が付いているはずです。  

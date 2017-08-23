---
title: "Configuration Manager のサイト コンポーネント | Microsoft Docs"
description: "サイト コンポーネントを構成して、サイト システムの役割とサイト ステータス レポートの動作を変更する方法について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
caps.latest.revision: "9"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 83550fbf0ef1f9adb0bb2c51a4f3c26a7500d352
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="site-components-for-system-center-configuration-manager"></a>System Center Configuration Manager のサイト コンポーネント

*適用対象: System Center Configuration Manager (Current Branch)*

各 System Center Configuration Manager サイトでサイト コンポーネントを設定すると、サイト システムの役割とサイト ステータス レポートの動作を変更できます。 サイト コンポーネントの構成はサイトと、サイトで適用可能なサイト システムの役割の各インスタンスに適用されます。  

## <a name="about-site-components"></a>サイト コンポーネントについて  
 さまざまなサイト コンポーネントのオプションのほとんどは、Configuration Manager コンソールに表示すると、ひとめでわかります。 ただし、次の詳細では、一部のより複雑な構成について説明しています。または、より複雑な構成について説明している追加のコンテンツを参照できます。  

### <a name="software-distribution"></a>ソフトウェアの配布  

-   **コンテンツ配布の設定:**  サイト サーバーから配布ポイントへのコンテンツの転送方法を変更する設定を指定できます。 同時配布設定に使用する値を増やすと、コンテンツの配布でより多くのネットワーク帯域幅を使用できます。  

-   **ネットワーク アクセス アカウント:**  ネットワーク アクセス アカウントの設定と使用の詳細については、「[Network Access Account](../../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA)」(ネットワーク アクセス アカウント) を参照してください。  

### <a name="software-update-point"></a>ソフトウェアの更新ポイント  

-   ソフトウェアの更新ポイント コンポーネントの構成オプションについては、「[Install a software update point](../../../../sum/get-started/install-a-software-update-point.md)」(ソフトウェアの更新ポイントをインストールする) を参照してください。  

### <a name="management-point"></a>管理ポイント  

-   **管理ポイント:** 管理ポイントに関する情報を Active Directory Domain Services に発行するようにサイトを設定することができます。  

     Configuration Manager クライアントは、管理ポイントを使用してサービスを特定し、境界グループのメンバーシップや PKI 証明書の選択オプションなどのサイト情報を検索します。 また、クライアントは、サイト内の他の管理ポイントの検索や、ソフトウェアのダウンロード元の配布ポイントの検索にも管理ポイントを使用します。 クライアントは、管理ポイントを使用して、サイト割り当ての実行、クライアント ポリシーのダウンロード、クライアント情報のアップロードも行うことができます。  

     クライアントが管理ポイントを見つけるには、Active Directory ドメイン サービスに発行するのが最も安全な方法であるため、通常は、機能している管理ポイントをすべて選択して Active Directory ドメイン サービスに発行します。 ただし、このサービスの場所検索方法では、次の条件を満たしている必要があります。

     - Configuration Manager のスキーマが拡張されている。
     - **System Management** コンテナーがあり、サイト サーバーがこのコンテナーに発行するための適切なセキュリティ アクセス許可が設定されている。
     - Configuration Manager サイトが Active Directory Domain Services に発行するように設定されている。
     - クライアントが、サイト サーバーと同じ Active Directory フォレストに属している  

     イントラネット上のクライアントが管理ポイントの検索に Active Directory Domain Services を使用できない場合は、代わりに [DNS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns) 発行を使用します。  

 サービスの場所の概要については、「[Understand how clients find site resources and services for System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)」(クライアントが System Center Configuration Manager のサイト リソースやサービスを検索する方法を理解する) を参照してください。  

-   **選択したイントラネット管理ポイントを DNS に発行する:** イントラネット上のクライアントが Active Directory ドメイン サービスから管理ポイントを検索できない場合は、このオプションを指定します。 代わりに、DNS サービスの場所リソース レコード (SRV RR) を使用して、割り当てられたサイト内の管理ポイントを検索できます。  

    Configuration Manager がイントラネットの管理ポイントを DNS に発行するには、次の条件が満たされていなければなりません。  

    -   DNS サーバーが、バージョン 8.1.2 以降の BIND を使用している。  

    -   DNS サーバーが自動更新用に設定されていて、サービスの場所のリソース レコードをサポートする。  

    -   Configuration Manager 内の管理ポイント用に指定された完全修飾ドメイン名 (FQDN) に DNS のホスト エントリ (A または AAA レコード) がある。  

    > [!WARNING]  
    >  クライアントが DNS で発行された管理ポイントを見つけるには、自動サイト割り当てを使用せずに、クライアントを特定のサイトに割り当てる必要があります。 管理ポイントのドメイン サフィックスを持つサイト コードを使用するには、これらのクライアントを設定します。 詳細については、「[How to assign clients to a site in System Center Configuration Manager](/sccm/core/clients/deploy/assign-clients-to-a-site)」(System Center Configuration Manager のサイトにクライアントを割り当てる方法) の「[Locating Management Points](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points)」(管理ポイントの特定) を参照してください。  

     Configuration Manager クライアントがイントラネット上の管理ポイントの検索に Active Directory Domain Services も DNS も使用できない場合は、[WINS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins) を使用します。 イントラネット上の HTTP クライアント接続を受信するように設定されている場合、サイトで最初にインストールされた管理ポイントが自動的に WINS に発行されます。  

### <a name="status-reporting"></a>ステータス レポート  

-   これらの設定は、サイトとクライアントからの状態レポートに含まれている詳細のレベルを直接設定します。  

### <a name="email-notification"></a>電子メール通知  

-   アカウントと電子メール サーバーの詳細を指定して、Configuration Manager を有効にし、アラートとして電子メール通知を送信します。  

### <a name="collection-membership-evaluation"></a>コレクション メンバーシップの評価  

-   このタスクは、コレクションのメンバーシップの変更箇所を評価する頻度を設定する場合に使用します。 変更箇所の評価は、新しいリソースが追加された場合またはリソースが変更された場合にのみコレクションのメンバーシップを更新します。  

### <a name="edit-the-site-components-at-a-site"></a>サイトでサイト コンポーネントを編集する  

サイト コンポーネントを編集するには、次の手順を使用します。

1.  Configuration Manager コンソールで、**[管理]** > **[サイトの構成]** > **[サイト]** の順にクリックし、構成するサイト コンポーネントのあるサイトを選択します。  

2.  **[ホーム]** タブの **[設定]** グループで、**[サイト コンポーネントの構成]** をクリックします。 構成するサイト コンポーネントを選択します。  

##  <a name="BKMK_ServiceMgr"></a> Configuration Manager サービス マネージャーによるサイト コンポーネントの管理  
Configuration Manager サービス マネージャーを使用して、Configuration Manager サービスを管理し、Configuration Manager サービスや実行中のスレッド (まとめて Configuration Manager コンポーネントと呼びます) のステータスを確認することができます。 Configuration Manager コンポーネントについて次のことを理解してください。  

-   コンポーネントは任意のサイト システムで実行できます。  

-   コンポーネントは、Windows のサービスを管理する場合と同じ方法で管理されます。 Configuration Manager コンポーネントの開始、停止、一時停止、再開、または照会を行うことができます。  

Configuration Manager サービスによる処理が必要になると (通常は構成ファイルがコンポーネントの受信トレイに書き込まれたとき)、サービスが実行されます。 操作に関連するコンポーネントを識別する必要がある場合は、Configuration Manager サービス マネージャーを使用して、各種のサービスとスレッドを操作することができます。 Configuration Manager の動作で発生した変更を表示できます。 たとえば、特定の応答が排除されるまで Configuration Manager サービスを一度に 1 つずつ停止できます。 これにより、特定の動作の原因となっているサービスを判別できます。  

> [!TIP]  
>  次の手順は、Configuration Manager コンポーネントの操作を変更するために使用できます。  

### <a name="use-the-configuration-manager-service-manager"></a>Configuration Manager サービス マネージャーを使用する  

1.  Configuration Manager コンソールで **[監視]** >  **[システムのステータス]** の順にクリックし、**[コンポーネントのステータス]** をクリックします。  

2.  **[ホーム]** タブの **[コンポーネント]** グループで、**[開始]** をクリックします。 次に **[Configuration Manager サービス マネージャー]** を選択します。  

3.  Configuration Manager サービス マネージャーが開いたら、管理したいサイトに接続します。  

     管理したいサイトが表示されない場合は、 **[サイト]**、 **[接続]**の順にクリックして、該当するサイトのサイト サーバーの名前を入力します。  

4.  サイトを展開して、管理したいコンポーネントのある場所に応じて、[ **コンポーネント** ] または [ **サーバー**] に移動します。  

5.  右側のウィンドウで、1 つまたは複数のコンポーネントを選択します。 次に、**[コンポーネント]** メニューの **[クエリ]** をクリックして、選択項目の状態を更新します。  

6.  コンポーネントのステータスを更新したら、**[コンポーネント]** メニューの 4 つのアクション ベースのオプションのいずれかを使用して、コンポーネントの操作を変更します。 アクションを要求したら、コンポーネントを照会して、コンポーネントの新しいステータスを表示する必要があります。  

7.  コンポーネントの操作の状態の変更が完了したら、Configuration Manager サービス マネージャーを閉じます。  

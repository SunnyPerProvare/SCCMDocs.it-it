---
title: "SQL Server クラスター | Microsoft Docs"
description: "SQL Server クラスターを使用して System Center Configuration Manager サイト データベースをホストします。 サポートされているオプションに関する情報が含まれます。"
ms.custom: na
ms.date: 2/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d09a82c6-bbd1-49ca-8ffe-e3ce87b85d33
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 53f119bbb1f8827a9c23c8b747840350bbb92790
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="use-a-sql-server-cluster-for-the-system-center-configuration-manager-site-database"></a>SQL Server クラスターを使用した System Center Configuration Manager サイト データベースのホスト

*適用対象: System Center Configuration Manager (Current Branch)*


 SQL Server クラスターを使用して System Center Configuration Manager サイト データベースをホストします。 サイト データベースは、サーバー クラスターでサポートされているサイト システムの役割として唯一のものです。  

> [!IMPORTANT]  
>  SQL Server クラスターの正常なセットアップは、SQL Server ドキュメント ライブラリで提供されるドキュメントと手順に依存します。  

 クラスターは、フェールオーバーをサポートできるため、サイト データベースの信頼性を高めることができます。 ただし、処理や負荷分散に関するメリットが増えることはありません。 さらに、サイト サーバーが、サイト データベースに接続する前に SQL Server クラスターのアクティブ ノードを検索する必要があるため、パフォーマンスの低下が発生する可能性があります。  

 Configuration Manager をインストールする前に、Configuration Manager をサポートするために SQL Server クラスターを準備する必要があります。 (このセクションで後ほど説明する前提条件をご覧ください)。  

 Configuration Manager のセットアップ中に、Microsoft Windows Server クラスターの各物理コンピューター ノードに Windows ボリューム シャドウ コピー サービス ライターがインストールされます。 これは、**バックアップ サイト サーバー**のメンテナンス タスクをサポートしています。  

 サイトのインストール後に Configuration Manager は、1 時間ごとにクラスター ノードが変更されたかどうかを確認します。 Configuration Manager は、Configuration Manager コンポーネントのインストールに影響する、検出したすべての変更 (ノードのフェールオーバーや SQL Server クラスターへの新しいノードの追加など) を自動的に管理します。  

## <a name="supported-options-for-using-a-sql-server-failover-cluster"></a>SQL Server フェールオーバー クラスターの使用でサポートされるオプション

サイト データベースとして使用される SQL Server フェールオーバー クラスターでは、次のオプションがサポートされます。

-   単一インスタンス クラスター  

-   複数インスタンス構成  

-   複数のアクティブ ノード  

-   名前付きインスタンスと既定のインスタンスの両方  

次の前提条件に注意してください。  

-   サイト データベースは、サイト サーバーからリモートである必要があります (クラスターは、サイト システム サーバーを含めることはできません)。  

-   サイト サーバーのコンピューター アカウントを、クラスター内の各サーバーのローカルの Administrators グループに追加しなければなりません。  

-   Kerberos 認証をサポートするには、**TCP/IP** ネットワーク通信プロトコルを各 SQL Server クラスター ノードのネットワーク接続に対して有効にする必要があります。 **名前付きパイプ** は不要ですが、Kerberos 認証に問題が発生したときのトラブルシューティングに使用できます。 ネットワーク プロトコルの設定は、**[SQL Server ネットワークの構成]** にある **[SQL Server 構成マネージャー]**で構成します。  

-   PKI を使用する場合は、「Configuration Manager での PKI 証明書の要件」を参照し、サイト データベースに SQL Server クラスターを使用する場合に必要となる特定の証明書の要件を確認します。  

次の制限が適用されます。  

-   **インストールおよび構成:**  

    -   セカンダリ サイトには、SQL Server クラスターを使用できません。  

    -   サイト データベースに対して既定以外のファイルの場所を指定するオプションは、SQL Server クラスターを指定する場合は使用できません。  

-   **SMS プロバイダー:**  

    -   SQL Server クラスター、またはクラスター化された SQL Server ノードとして実行されるコンピューターに SMS プロバイダーのインスタンスをインストールすることはサポートされていません。  

-   **データ レプリケーションのオプション:**  

    -   **分散ビュー**を使用する場合は、サイト データベースをホストするために SQL Server クラスターを使用することはできません。  

-   **バックアップと回復:**  

    -   Configuration Manager では、名前付きインスタンスを使用する SQL Server クラスターの Data Protection Manager (DPM) のバックアップはサポートしません。 ただし、SQL Server の既定のインスタンスを使用する SQL Server クラスター上の DPM バックアップはサポートします。  

## <a name="prepare-a-clustered-sql-server-instance-for-the-site-database"></a>サイト データベースに対してクラスター化された SQL Server インスタンスを準備する  

サイト データベースを準備するために完了する主なタスクを次に示します。

-   サイト データベースをホストする仮想 SQL Server クラスターを既存の Windows Server クラスター環境で作成します。 SQL Server クラスターをインストールおよび設定するための特定の手順については、使用している SQL Server のバージョンのドキュメントをご覧ください。 たとえば、SQL Server 2008 R2 を使用している場合は、「 [SQL Server 2008 R2 フェールオーバー クラスターのインストール](http://go.microsoft.com/fwlink/p/?LinkId=240231)」を参照してください。  

-   SQL Server クラスター内の各コンピューターで、ドライブのルート フォルダーにファイルを配置すると、Configuration Manager はサイト コンポーネントをそのドライブにインストールしません。 ファイル名は **NO_SMS_ON_DRIVE.SMS** にする必要があります。 既定では、Configuration Manager は各物理ノードにいくつかのコンポーネントをインストールして、バックアップなどの操作をサポートします。  

-   サイト サーバーのコンピューター アカウントを、各 Windows Server クラスター ノード コンピューターのローカルの [ **Administrators** ] グループに追加します。  

-   仮想 SQL Server インスタンスで、Configuration Manager セットアップを実行するユーザー アカウントに、**sysadmin** という SQL Server の役割を割り当てます。  

### <a name="to-install-a-new-site-using-a-clustered-sql-server"></a>クラスター化された SQL Server を使用して新しいサイトをインストールするには  
 クラスター化されたサイト データベースを使用するサイトをインストールするには、次の部分を変更したうえで通常のサイトのインストール プロセスに従って、Configuration Manager のセットアップを実行します。  

-   **[データベース情報]** ページで、サイト データベースをホストする仮想 SQL Server クラスター インスタンスの名前を指定します。 仮想インスタンスは、SQL Server を実行するコンピューターの名前を置き換えます。  

    > [!IMPORTANT]  
    >  仮想 SQL Server クラスター インスタンスの名前を入力するとき、Windows Server クラスターによって作成される仮想 Windows Server 名を入力しないでください。 仮想 Windows Server 名を使用すると、サイト データベースが、アクティブな Windows Server クラスター ノードのローカル ハード ディスクにインストールされます。 これにより、そのノードに障害が発生しても、正常にフェールオーバーできません。  

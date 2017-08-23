---
title: "コレクションの作成 | Microsoft Docs"
description: "System Center Configuration Manager でユーザーとデバイスのグループをより簡単に管理するコレクションを作成します。"
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
caps.latest.revision: "6"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 44b4707b1a40624c51decf548d23ddd2164c5833
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-collections-in-system-center-configuration-manager"></a>System Center Configuration Manager でコレクションを作成する方法

*適用対象: System Center Configuration Manager (Current Branch)*

コレクションはユーザーまたはデバイスのグループです。 コレクションを使用して、アプリケーションの管理、コンプライアンス設定の展開、ソフトウェア更新プログラムのインストールなどのタスクを行います。 クライアント設定のグループを管理したり、役割ベースの管理を行ってリソースを管理者ユーザーのみアクセス可能に指定したりといったことに、コレクションを使用することもできます。 Configuration Manager には、組み込みコレクションが複数含まれます。 詳細については、「[Introduction to collections in System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md)」(System Center Configuration Manager でのコレクションの概要) をご覧ください。  

> [!NOTE]  
>  コレクションにはユーザーまたはデバイスを含めることができますが、両方を含めることはできません。  

 次の表は、Configuration Manager でのコレクションのメンバーを構成するために使用する規則の一覧を示しています。  

|メンバーシップ規則の種類|説明|  
|--------------------------|----------------------|  
|ダイレクト規則|コレクションに追加するユーザーまたはコンピューターを選択する場合に使用します。 このメンバーシップは、リソースを Configuration Manager から削除しない限り、変わりません。 リソースをダイレクト規則コレクションに追加するには、そのリソースが Configuration Manager で既に検出されているか、ユーザーがそのリソースをインポートしておく必要があります。 ダイレクト規則コレクションは、手動で変更する必要があるため、クエリ規則コレクションよりも管理オーバーヘッドが高くなります。|  
|クエリ規則|Configuration Manager がスケジュールに従って実行するクエリに基づいて、コレクションのメンバーシップを動的に更新します。 たとえば、Active Directory ドメイン サービスの人事ユニットのメンバーであるユーザーのコレクションを作成することができます。 このコレクションは、人事ユニットに対して新しいユーザーが追加または削除されたりすると、自動的に更新されます。<br /><br /> コレクションを構築するのに使用できるクエリの例については、「[System Center Configuration Manager でクエリを作成する方法](../../../../core/servers/manage/create-queries.md)」を参照してください。|  
|[コレクションを含める] 規則|Configuration Manager コレクションに他のコレクションのメンバーを含めます。該当するコレクションに変更があった場合は、現在のコレクションのメンバーシップはスケジュールに従って更新されます。<br /><br /> 複数の [コレクションを含める] 規則をコレクションに追加できます。<br /> |  
|[コレクションを除外する] 規則|[コレクションを除外する] 規則を使用すると、Configuration Manager における他のコレクションのメンバーを除外することができます。 除外されるコレクションに変更があった場合は、現在のコレクションのメンバーシップはスケジュールに従って更新されます。<br /><br /> 複数の [コレクションを除外する] 規則をコレクションに追加できます。 コレクションが、[コレクションを含める] 規則と [コレクションを除外する] 規則の両方を含み、競合が生じた場合は、[コレクションを除外する] 規則が優先されます。<br />              **例:** [コレクションを含める] 規則と [コレクションを除外する] 規則が 1 つずつ含まれるコレクションを作成します。 [コレクションを含める] 規則の対象は Dell デスクトップのコレクションです。 [コレクションを除外する] 規則の対象は、RAM が 4 GB 未満のコンピューターのコレクションです。 新しいコレクションには、RAM が 4 GB 以上の Dell デスクトップが含まれます。|  

 Configuration Manager でコレクションを作成する際は、次の手順を参考にします。 Configuration Manager サイトに作成されたコレクションをインポートすることもできます。 コレクションのエクスポートとインポートの方法については、「[System Center Configuration Manager でコレクションを管理する方法](../../../../core/clients/manage/collections/manage-collections.md)」を参照してください。  

 Linux および UNIX を実行しているコンピューターのコレクションの作成については、「[System Center Configuration Manager で Linux および UNIX サーバーのクライアントを管理する方法](../../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md)」を参照してください。  

##  <a name="BKMK_1"></a> デバイス コレクションを作成するには  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[デバイス コレクション]** の順に選択します。  

3.  **[ホーム]** タブの **[作成]** グループで、**[デバイス コレクションの作成]** を選択します。  

4.  **[全般]** ページで、**[名前]** と **[コメント]** を指定します。 次に、**[限定コレクション]** で、**[参照]** を選んで限定コレクションを選択します。 コレクションが限定コレクションのメンバーのみを含むようになります。  

5.  **デバイス コレクションの作成ウィザード**の **[メンバーシップの規則]** ページにある **[規則の追加]** リストで、このコレクションで使用するメンバーシップ規則の種類を選択します。 1 つのコレクションにつき複数の規則を構成することができます。  

        
##### <a name="to-configure-a-direct-rule"></a>ダイレクト規則を構成するには  

1.  ダイレクト メンバーシップの規則の作成ウィザード **** の [リソースの検索] ****ページで、次の情報を指定します。  

-   **リソース クラス**: 検索してコレクションに追加するリソースの種類を選択します。 [システム リソース] **** から選択してクライアント コンピューターが返すインベントリ データを検索、または[不明なコンピューター] **** を選択して不明なコンピューターが返す値から選択します。  

-   **属性名**: 検索対象として選択したリソース クラスに関連する属性を選択します。 たとえば、NetBIOS 名でコンピューターを選択する場合は、[リソース クラス] **** の一覧で [システム リソース] **** を、 [属性名] **** の一覧で [NetBIOS 名] **** を選択します。  

-   **不使用とマークされているリソースを除外する**: クライアント コンピューターが不使用とマークされている場合は、検索結果にその値を含めません。  

-   **Configuration Manager クライアントがインストールされていないリソースを除外する** - この場合、検索結果には表示されません。  

-   **値** : 選択した属性名を検索するための値を入力します。 ワイルドカードとしてパーセント ( **%** ) を使用できます。 たとえば、"M" で始まる NetBIOS 名のコンピューターを検索する場合は、このフィールドに「**M%**」と入力します。  

2.  **[リソースの選択]** ページで、コレクションに追加するリソースを **[リソース]** リストから選択し、**[次へ]** を選択します。  


##### <a name="to-configure-a-query-rule"></a>クエリ規則を構成するには  

1.  [クエリ規則のプロパティ] **** ダイアログ ボックスで、次の情報を入力します。  

-   **名前**: 固有の名前を指定します。  

-   **クエリ ステートメントのインポート** - コレクションのクエリ規則として使用する [Configuration Manager クエリ](../../../../core/servers/manage/create-queries.md)を選択できる **[クエリの参照]** ダイアログ ボックスを開きます。   

-   **リソース クラス**: 検索してコレクションに追加するリソースの種類を選択します。 [システム リソース] **** から値を選択してクライアント コンピューターが返すインベントリ データを検索、または[不明なコンピューター] **** を選択して不明なコンピューターが返す値から選択します。  

-   **クエリ ステートメントの編集**: コレクションのクエリ規則として使用するクエリを編集できる [**クエリ ステートメントのプロパティ**] ダイアログ ボックスを開きます。 クエリに関する詳細については、「[System Center Configuration Manager のクエリのテクニカル リファレンス](../../../../core/servers/manage/queries-technical-reference.md)」を参照してください。  

    
##### <a name="to-configure-an-include-collection-rule"></a>[コレクションを含める] 規則を構成するには  

**[コレクションの選択]** ダイアログ ボックスで、新しいコレクションに含めるコレクションを選択し、**[OK]** を選択します。  

##### <a name="to-configure-an-exclude-collection-rule"></a>[コレクションを除外する] 規則を構成するには  

**[コレクションの選択]** ダイアログ ボックスで、新しいコレクションから除外コレクションを選択し、**[OK]** を選択します。  

-   **このコレクションで増分更新を使用する** - コレクションのフル評価とは別に、新しいリソースまたは前回のコレクション評価から変更されたリソースのみを定期的にスキャンおよび更新する場合は、このオプションを選択します。 増分更新は 10 分間隔で行われます。  

> [!IMPORTANT]  
>  次のクラスを使用しているクエリ規則で構成されたコレクションは、増分更新をサポートしません。  
>   
> -   SMS_G_System_CollectedFile  
> -   SMS_G_System_LastSoftwareScan  
> -   SMS_G_System_AppClientState  
> -   SMS_G_System_DCMDeploymentState  
> -   SMS_G_System_DCMDeploymentErrorAssetDetails  
> -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
> -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
> -   SMS_G_User_DCMDeploymentCompliantAssetDetails (ユーザーのコレクションのみ)  
> -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (ユーザーのコレクションのみ)  
> -   SMS_G_System_SoftwareUsageData  
> -   SMS_G_System_CI_ComplianceState  
> -   SMS_G_System_EndpointProtectionStatus  
> -   SMS_GH_System_*  
> -   SMS_GEH_System_*  

-   **このコレクションの完全な更新をスケジュールする** - コレクションのメンバーシップのフル評価を定期的にスケジュールします。  

6.  新しいコレクションを作成するウィザードを完了します。 新しいコレクションは、[資産とコンプライアンス] **** ワークスペースの [デバイス コレクション] **** ノードに表示されます。  

> [!NOTE]  
>  コレクション メンバーを表示するには、Configuration Manager コンソールを更新または再読み込みする必要があります。 ただし、メンバーは、スケジュールされた最初の更新が行われるか、コレクションに対して **[メンバーシップの更新]** を手動で選択するまでコレクションに表示されません。 コレクションの更新が完了するまで、しばらく時間がかかる場合があります。  

##  <a name="BKMK_2"></a> ユーザー コレクションを作成するには  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[ユーザー コレクション]** の順に選択します。  

3.  **[ホーム]** タブの **[作成]** グループで、**[ユーザー コレクションの作成]** を選択します。  

4.  ウィザードの **[全般]** ページで、**[名前]** と **[コメント]** を指定します。 次に、**[限定コレクション]** で、**[参照]** を選んで限定コレクションを選択します。 コレクションが限定コレクションのメンバーのみを含むようになります。  

5.  **[メンバーシップの規則]** ページで、次のように指定します。  

    -   [規則の追加] **** 一覧で、このコレクションで使用するメンバーシップ規則の種類を選択します。 1 つのコレクションにつき複数の規則を構成することができます。  

##### <a name="to-configure-a-direct-rule"></a>ダイレクト規則を構成するには  

1.  **ダイレクト メンバーシップの規則の作成ウィザード**の **[リソースの検索]** ページで、次のように指定します。  

-   **リソース クラス**: 検索してコレクションに追加するリソースの種類を選択します。 Configuration Manager によって収集されるユーザー情報を検索する場合は [**ユーザー リソース**] から、Configuration Manager によって収集されたユーザー グループ情報を検索する場合は [**ユーザー グループ リソース**] から選択します。  

-   **属性名**: 検索するリソース クラスに関連する属性を選択します。 たとえば、組織単位 (OU) 名でユーザーを選択する場合は、 **[リソース クラス]** の一覧で **[ユーザー リソース]** を、 **[属性名]** の一覧で **[ユーザー OU 名]** を選択します。  

-   **値:** 検索する値を入力します。 ワイルドカードとしてパーセント ( **%** ) を使用できます。 たとえば、Contoso OU 内のユーザーを検索する場合は、このフィールドに「**Contoso**」と入力します。  

2.  **[リソースの選択]** ページで、コレクションに追加するリソースを **[リソース]** リストから選択します。  

##### <a name="to-configure-a-query-rule"></a>クエリ規則を構成するには  

1.  **[クエリ規則のプロパティ]** ダイアログ ボックスで、次のように指定します。  

-   **名前**: 一意の名前です。  

-   **クエリ ステートメントのインポート** - コレクションのクエリ規則として使用する [Configuration Manager クエリ](../../../../core/servers/manage/queries-technical-reference.md)を選択できる **[クエリの参照]** ダイアログ ボックスを開きます。  

-   **リソース クラス**: 検索してコレクションに追加するリソースの種類を選択します。 Configuration Manager によって収集されるユーザー情報を検索する場合は [**ユーザー リソース**] から、Configuration Manager によって収集されたユーザー グループ情報を検索する場合は [**ユーザー グループ リソース**] から選択します。  

-   **クエリ ステートメントの編集** - コレクションの規則として使用する[クエリを作成](../../../../core/servers/manage/queries-technical-reference.md)できる **[クエリ ステートメントのプロパティ]** ダイアログ ボックスを開きます。  

##### <a name="to-configure-an-include-collection-rule"></a>[コレクションを含める] 規則を構成するには  

**[コレクションの選択]** ダイアログ ボックスで、新しいコレクションに含めるコレクションを選択し、**[OK]** を選択します。  

##### <a name="to-configure-an-exclude-collection-rule"></a>[コレクションを除外する] 規則を構成するには  

**[コレクションの選択]** ダイアログ ボックスで、新しいコレクションから除外コレクションを選択し、**[OK]** を選択します。  


-   **このコレクションで増分更新を使用する** - コレクションのフル評価とは別に、新しいリソースまたは前回のコレクション評価から変更されたリソースのみを定期的にスキャンおよび更新する場合は、このオプションを選択します。 増分更新は 10 分間隔で行われます。  

> [!IMPORTANT]  
>  次のクラスを使用しているクエリ規則で構成されたコレクションは、増分更新をサポートしません。  
>   
> -   SMS_G_System_CollectedFile  
> -   SMS_G_System_LastSoftwareScan  
> -   SMS_G_System_AppClientState  
> -   SMS_G_System_DCMDeploymentState  
> -   SMS_G_System_DCMDeploymentErrorAssetDetails  
> -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
> -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
> -   SMS_G_User_DCMDeploymentCompliantAssetDetails (ユーザーのコレクションのみ)  
> -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (ユーザーのコレクションのみ)  
> -   SMS_G_System_SoftwareUsageData  
> -   SMS_G_System_CI_ComplianceState  
> -   SMS_G_System_EndpointProtectionStatus  
> -   SMS_GH_System_*  
> -   SMS_GEH_System_*  

-   **このコレクションの完全な更新をスケジュールする** - コレクションのメンバーシップのフル評価を定期的にスケジュールします。  

6.  ウィザードを完了します。 新しいコレクションは、[資産とコンプライアンス] **** ワークスペースの [ユーザー コレクション] **** ノードに表示されます。  

> [!NOTE]  
>  コレクション メンバーを表示するには、Configuration Manager コンソールを更新または再読み込みする必要があります。 ただし、メンバーは、スケジュールされた最初の更新が行われるか、コレクションに対して **[メンバーシップの更新]** を手動で選択するまでコレクションに表示されません。 コレクションの更新が完了するまで、しばらく時間がかかる場合があります。  

##  <a name="BKMK_3"></a> コレクションをインポートするには  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[ユーザー コレクション]** または **[デバイス コレクション]** の順に選択します。  

3.  **[ホーム]** タブの **[作成]** グループで、**[コレクションのインポート]** を選択します。  

4.  **コレクションのインポート ウィザード**の **[全般]** ページで **[次へ]** を選択します。  

5.  **[MOF ファイル名]** ページで、**[参照]** を選択し、インポートするコレクション情報を含む MOF ファイルを参照します。  

    > [!NOTE]  
    >  インポートするファイルは、同じバージョンの Configuration Manager が動作するサイトからエクスポートされたものである必要があります。 コレクションのエクスポートの詳細については、「[System Center Configuration Manager でコレクションを管理する方法](../../../../core/clients/manage/collections/manage-collections.md)」を参照してください。  

6.  コレクションをインポートするウィザードを完了します。 新しいコレクションは、 **[資産とコンプライアンス]** ワークスペースの **[ユーザー コレクション]** または **[デバイス コレクション]** ノードに表示されます。 新しくインポートされたコレクションのコレクション メンバーを表示するには、Configuration Manager コンソールを更新または再読み込みします。  

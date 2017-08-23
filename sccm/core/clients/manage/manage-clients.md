---
title: "クライアントの管理 | Microsoft Docs"
description: "System Center Configuration Manager でクライアントを管理する方法について説明します。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
caps.latest.revision: "17"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 3a86924b2e5db3ac16eeda78b95ae6747ffd656f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-manage-clients-in-system-center-configuration-manager"></a>System Center Configuration Manager でクライアントを管理する方法

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager クライアントがインストールされ、Configuration Manager サイトに正しく割り当てられると、**[デバイス]** ノードの **[資産とコンプライアンス]** ワークスペースと、**[デバイス コレクション]** ノードの 1 つまたは複数のコレクションにデバイスが表示されます。 デバイスまたはコレクションを選択するときに、管理操作を実行できます。 ただし、コンソールの他のワークスペースを使用するか、Configuration Manager コンソールを使用しないタスクを実行して、別の方法でクライアントを管理することもできます。  

> [!NOTE]  
>  Configuration Manager クライアントがインストールされていても、Configuration Manager コンソールに表示されない場合があります。 この問題は、クライアントがサイトに正常に割り当てられていない場合や、コンソールの更新やコレクション メンバーシップの更新が必要な場合に生じる可能性があります。  
>   
>  また、Configuration Manager クライアントがインストールされていないのに、デバイスがコンソールに表示されることもあります。 この問題は、デバイスが検出されているが、Configuration Manager クライアントのインストールと割り当てが行われていない場合に生じる可能性があります。 Exchange Server コネクタを使用して管理されるモバイル デバイスと、Microsoft Intune に登録されているデバイスでは、Configuration Manager クライアントがインストールされません。  
>   
>  Configuration Manager コンソールで **[クライアント]** 列を使用して、Configuration Manager クライアントがインストールされていて Configuration Manager コンソールから管理できるかどうかを判断できます。  

##  <a name="BKMK_ManagingClients_DevicesNode"></a> [デバイス] ノードを使用してクライアントを管理する  

デバイスの種類によっては、一部のオプションを使用できません。  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** >  **[デバイス]** を選択します。  

3.  1 つまたは複数のデバイスを選択してから、リボンからクライアント管理タスクのいずれかを選択するか、デバイスを右クリックします。  

    -   **ユーザー デバイスのアフィニティ情報を管理する**  

         ユーザーとデバイスの関連付けを構成して、ユーザーにソフトウェアを効率的に展開することができます。  

         「[System Center Configuration Manager でのユーザーとデバイスのアフィニティへのユーザーとデバイスの関連付け](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)」を参照してください  

    -   **新規または既存のコレクションにデバイスを追加する**  

         ダイレクト規則でデバイスをコレクションに追加します。  
         
    -   **クライアント プッシュ ウィザードを使用してクライアントのインストールと再インストールを実行する**  

         Configuration Manager クライアントの修復、または Windows を実行するコンピューターでの再構成には、インストールまたは再インストールを実行します。 サイトの構成オプションと、クライアントのプッシュ インストール用に設定した client.msi プロパティを含めます。  

        > [!TIP]  
        >  Configuration Manager クライアントのインストール (および再インストール) を実行するには、さまざまな方法があります。 クライアント プッシュ ウィザードはコンソールから実行できるため、クライアントのインストールには便利な方法ですが、この方法には数多くの依存関係があり、すべての環境に適しているわけではありません。 依存関係の詳細については、「[System Center Configuration Manager で Windows コンピューターにクライアントを展開するための前提条件](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md)」を参照してください。 他のクライアント インストール方法の詳細については、「[System Center Configuration Manager でのクライアントのインストール方法](../../../core/clients/deploy/plan/client-installation-methods.md)」を参照してください。  

         「 [クライアント プッシュを使用した Configuration Manager クライアントのインストール方法](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)」を参照してください。  

    -   **サイトの再割り当て**  

         1 つまたは複数のクライアント (管理しているモバイル デバイスを含む) を、階層内の別のプライマリ サイトに再割り当てします。 新しいサイトへのクライアントの再割り当ては、個別に行うことも、複数のクライアントを選択して一括で行うこともできます。  

    -   **クライアントをリモート管理する**  

         リソース エクスプローラーを実行して、ハードウェアとソフトウェアのインベントリ情報を Windows クライアントから確認したり、リモート コントロール、リモート アシスタンス、またはリモート デスクトップを使用してこれらの情報をリモートで管理できます。  

         「[System Center Configuration Manager でリソース エクスプローラーを使用してハードウェア インベントリを表示する方法](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)」および「[System Center Configuration Manager でリソース エクスプローラーを使用してソフトウェア インベントリを表示する方法](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md)」を参照してください。  

         「[System Center Configuration Manager を使用して Windows クライアント コンピューターをリモート管理する方法](../../../core/clients/manage/remote-control/remotely-administer-a-windows-client-computer.md)」を参照してください。  

    -   **クライアントを承認する**  

         クライアントが HTTP および自己署名証明書を使用してサイト システムと通信する場合、信頼されるコンピューターとして識別されるように、これらのクライアントを承認する必要があります。 既定では、各クライアントを手動で承認せずに済むように、サイト構成により、同じ Active Directory フォレストおよび信頼されるフォレストのクライアントは自動的に承認されます。 ただし、信頼できるワークグループ コンピューター、および信頼できるが承認されていないその他のコンピューターは手動で承認する必要があります。  

        > [!WARNING]  
        >  一部の管理機能は承認されていないクライアントでも動作する可能性がありますが、このシナリオは Configuration Manager ではサポートされていません。  

         常に HTTPS を使用してサイト システムと通信するクライアントや、HTTP を使用してサイト システムと通信する際に PKI 証明書を使用するクライアントは、承認する必要はありません。 これらのクライアントは、PKI 証明書を使用して信頼を確立します。  

    -   **クライアントをブロックまたはブロック解除する**  

         信頼できなくなったクライアントをブロックして、このクライアントがクライアント ポリシーを受け取るのを防いだり、Configuration Manager サイト システムがこのクライアントと通信するのを防ぎます。  

        > [!WARNING]  
        >  クライアントをブロックすると、クライアントから Configuration Manager サイト システムへの通信のみ防ぐことができます。クライアントから他のデバイスへの通信を防ぐことはできません。 また、HTTPS の代わりに HTTP を使用してクライアントがサイト システムに通信する場合、セキュリティ上の制限がいくつか生じます。  

         ブロックされていたクライアントのブロックを解除できます。 ただし、ブロックしたときに AMT 用にプロビジョニングされていた Inel AMT 搭載コンピューターのブロックを解除する場合、そのコンピューターを再度、帯域外管理するためには、追加の手順を実行する必要があります。  

         「[System Center Configuration Manager でクライアントをブロックするかどうかの判断](../../../core/clients/deploy/plan/determine-whether-to-block-clients.md)」を参照してください。  

    -   **必要な PXE 展開をクリアする**  

         コンピューターに必要な PXE 展開を再展開します。  

         「[System Center Configuration Manager で PXE を使用してネットワーク経由で Windows を展開する](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md)」を参照してください。  

    -   **クライアントのプロパティを管理する**  

         クライアントを対象とした探索データと展開を表示します。 また、オペレーティング システムをデバイスに展開するためにタスク シーケンスで使用される変数を構成することもできます。  

    -   **クライアントを削除する**  

        > [!WARNING]  
        >  Configuration Manager クライアントをアンインストールする場合やコレクションから削除する際、クライアントを削除しないでください。  

         **[削除]** 操作を実行して、Configuration Manager データベースからクライアント レコードを手動で削除します。通常、この操作は、トラブルシューティング以外では使用しないでください。 クライアント レコードを削除しても、クライアントが引き続きインストールされており、Configuration Manager と通信している場合は、クライアント履歴と以前の関連付けは失われますが、定期探索によってクライアント レコードが再作成されて Configuration Manager コンソールに表示されます。  

        > [!NOTE]  
        >  Configuration Manager によって登録されているモバイル デバイス クライアントを削除すると、この操作により、モバイル デバイス クライアントに発行された PKI 証明書が失効し、IIS によって CRL がチェックされない場合でも、この証明書が管理ポイントで拒否されるようになります。 モバイル デバイス レガシ クライアントを削除しても、これらのクライアントの証明書は失効しません。  

         クライアントをアンインストールするには、「 [Configuration Manager クライアントのアンインストール](#BKMK_UninstalClient)」を参照してください。  

         クライアントを新しいプライマリ サイトに割り当てるには、「[System Center Configuration Manager でクライアントをサイトに割り当てる方法](../../../core/clients/deploy/assign-clients-to-a-site.md)」を参照してください。  

         クライアントをコレクションから削除するには、コレクションのプロパティを再構成します。 「[System Center Configuration Manager でコレクションを管理する方法](../../../core/clients/manage/collections/manage-collections.md)」を参照してください。  

    -   **モバイル デバイスをワイプする**  

         ワイプ コマンドをサポートするモバイル デバイスをワイプできます。  

         この操作により、個人設定や個人データを含め、モバイル デバイスのすべてのデータが削除されます。 通常、この操作で、モバイル デバイスが工場出荷時の設定にリセットされます。 モバイル デバイスは、紛失や盗難にあうなど、信頼できなくなった場合にワイプします。  

        > [!TIP]  
        >  モバイル デバイスでリモート ワイプ コマンドがどのように処理されるかについては、製造元のドキュメントを参照してください。  

         モバイル デバイスがワイプ コマンドを受信するまで、通常、待ち時間が発生します。  

        -   モバイル デバイスが Configuration Manager または Microsoft Intune によって登録されている場合、クライアントは、クライアント ポリシーのダウンロード時にコマンドを受信します。  

        -   モバイル デバイスが Exchange Server コネクタによって管理されている場合、Exchange との同期時にコマンドを受信します。  

         **[ワイプのステータス]** 列を使用して、デバイスがワイプ コマンドをいつ受信するのかを監視できます。 デバイスが Configuration Manager にワイプ確認を送信するまで、ワイプ コマンドをキャンセルできます。  

    -   **モバイル デバイスをインベントリから削除する**  

         **[インベントリから削除]** オプションをサポートしているのは、Intune に登録されたか、\-オンプレミス モバイル デバイス管理で登録されたモバイル デバイスのみです。  

         詳細については、「 [System Center Configuration Manager によるリモート ワイプ、リモート ロック、パスコードのリセットを使用したデータの保護](../../../mdm/deploy-use/wipe-lock-reset-devices.md)」をご覧ください。  

    -   **デバイスの所有権を変更する**  

         デバイスがドメインに参加しておらず、Configuration Manager クライアントがインストールされていない場合は、デバイスの所有権を **[会社]** または **[個人]** に変更できます。  

         アプリケーションの要件にこの値を使用して、展開を制御できます。また、ユーザー デバイスから収集するインベントリの量を制御できます。  

        また、必要に応じて、列見出しを右クリックして選択し、ビューに **[デバイスの所有者]** 列を追加することもできます。

         詳細については、「[System Center Configuration Manager と Microsoft Intune を使用するハイブリッド モバイル デバイス管理 (MDM)](../../../mdm/understand/hybrid-mobile-device-management.md)」を参照してください。  

##  <a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> [デバイス コレクション] ノードを使用してクライアントを管理する  
  **[デバイス]** ノードの 1 つのデバイスまたは複数のデバイスに対して実行できる多くのタスクは、コレクションに対しても実行できます。 コレクションに対して実行すると、コレクション内の対象となるすべてのデバイスに操作が適用されます。 この処理で多数のネットワーク パケットが生成され、サイト サーバーの CPU 使用率が増加する点に注意してください。  

  コレクション レベルのクライアント管理タスクを実行する前に、コレクションにどの程度の数のデバイスが含まれているのか、それらのデバイスが低帯域幅のネットワーク接続で接続されていないかどうか、およびすべてのデバイスでタスクを完了するのにどの程度の時間がかかるのかを検討します。 タスクの開始後にコンソールからタスクを停止することはできません。  

#### <a name="to-manage-clients-from-the-device-collections-node"></a>[デバイス コレクション] ノードを使用してクライアントを管理するには  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[デバイス コレクション]** の順に選択します。  

3.  コレクションを選んだ後、リボンから (またはコレクションを右クリックして) 次のいずれかのクライアント管理タスクを選びます。 これらのクライアント管理タスクは、*コレクション レベルでのみ*使用できます。  

    -   **マルウェアがないかどうかコンピューターをスキャンし、マルウェア対策の定義ファイルをダウンロードする**  

         「[System Center Configuration Manager での Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)」を参照してください。  

    -   **ソフトウェア、構成基準、タスク シーケンスを展開する**  

         関連項目  

        -   [System Center Configuration Manager でのソフトウェア更新プログラムの展開](../../../sum/deploy-use/deploy-software-updates.md)  

        -   [System Center Configuration Manager におけるコンプライアンス設定の計画と構成](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)  

    -   **電源管理設定を構成する**  

         「[System Center Configuration Manager で電源プランを作成して適用する方法](../../../core/clients/manage/power/create-and-apply-power-plans.md)」を参照してください。 電源プランは Windows を実行するコンピューターにのみ使用できます。  

    -   **直ちにポリシーをダウンロードするようにコンピューターに通知する**  

         クライアント通知を使用して、クライアント ポリシーのポーリング間隔に関係なく、直ちにコンピューター ポリシーをダウンロードするように、選択した Windows クライアントに通知します。  

         クライアント通知タスクは、[ **監視** ] ワークスペースの [ **クライアントの操作** ] ノードに表示されます。  

##  <a name="BKMK_ClientCache"></a> Configuration Manager クライアントにクライアントキャッシュを構成する  
クライアントでアプリケーションとプログラムをインストールすると、一時ファイルがクライアント キャッシュに格納されます。 ソフトウェアの更新ではクライアント キャッシュも使用されますが、ソフトウェアの更新は構成されているキャッシュ サイズには制限されず、常にキャッシュへのダウンロードが試みられます。 Configuration Manager クライアントを手動でインストールする際、クライアント プッシュ インストールを使用する際、またはクライアントのインストール後に、クライアント キャッシュ設定 (サイズや場所など) を構成できます。

Configuration Manager バージョン 1606 以降では、Configuration Manager コンソールでクライアント設定を使用してキャッシュ フォルダー サイズを指定できます。   

 Configuration Manager クライアント キャッシュの既定の場所は %*windir*%\ccmcache で、既定のディスク容量は 5120 MB です。  

> [!IMPORTANT]  
>  クライアント キャッシュに使用するフォルダーは暗号化しないでください。 Configuration Manager は暗号化されたフォルダーにコンテンツをダウンロードすることはできません。  

### <a name="about-client-cache"></a>クライアント キャッシュについて  

Configuration Manager クライアントは、展開を受けた後まもなく要求されたソフトウェアのコンテンツをダウンロードしますが、スケジュールされた展開時刻まで、それを実行しません。 スケジュールされた時刻になると、Configuration Manager クライアントはコンテンツがキャッシュで利用可能かどうかを確認します。 キャッシュにコンテンツがあり、それが正しいバージョンの場合は、クライアントはこのキャッシュされたコンテンツを使用します。 要求されたコンテンツのバージョンが変更されたり、別のパッケージのためにコンテンツが削除されたりした場合は、コンテンツはキャッシュに再びダウンロードされます。  

クライアントがキャッシュのサイズより大きいプログラム コンテンツまたはアプリケーション コンテンツをダウンロードしようとすると、Configuration Manager はステータス メッセージ ID 10050 を生成します。 後でキャッシュ サイズが増えると、結果は次のようになります。  

-   要求されるプログラムの場合:クライアントは、コンテンツのダウンロードを自動的に再試行しません。 パッケージとプログラムを再度展開する必要があります。  
-   要求されるアプリケーションの場合: クライアントは、クライアント ポリシーをダウンロードするときに、自動的にコンテンツのダウンロードを再試行します。  

クライアントがダウンロードしようとするパッケージのサイズがキャッシュ サイズより小さくても、キャッシュに空きがない場合、キャッシュ領域が利用可能になるまで、またはダウンロードがタイムアウトするまで、あるいはキャッシュ領域による失敗の再試行回数の上限まで、要求された展開は再試行を繰り返します。 キャッシュ サイズが後で拡大されると、Configuration Manager クライアントは、次回の再試行時に再びパッケージのダウンロードを試みます。 クライアントは 4 時間ごとに 18 回になるまでコンテンツのダウンロードを試みます。  

キャッシュされたコンテンツは自動的には削除されず、クライアントがコンテンツを使用した後、少なくとも 1 日の間キャッシュに保持されます。 パッケージのプロパティを、クライアント キャッシュの内容を保持するオプションで構成すると、クライアントはキャッシュからコンテンツを自動的に削除しません。 クライアント キャッシュ領域が、24 時間以内にダウンロードされたパッケージによって使用されているときに、新しいパッケージをダウンロードする必要がある場合は、キャッシュ サイズを拡張するか、削除オプションを使って、保持しているキャッシュ コンテンツを削除できます。  

 手動によるクライアントのインストール中またはクライアントのインストール後に、クライアント キャッシュを構成するには、次の手順を使用します。  

### <a name="to-configure-the-client-cache-when-you-install-clients-by-using-manual-client-installation"></a>手動によってクライアントをインストールするときにクライアント キャッシュを構成するには  

必要に応じて次のプロパティを指定して、インストール ソースの場所から CCMSetup.exe コマンドを実行します。プロパティはスペースで区切ります。  

   -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > バージョン 1606 では、SMSCACHESIZE ではなく Configuration Manager コンソールの **[クライアント設定]** で使用可能なキャッシュ サイズ設定を使用します。 詳細については、「[クライアントのキャッシュ設定](../../../core/clients/deploy/about-client-settings.md#client-cache-settings)」を参照してください。

CCMSetup.exe 用のこれらのコマンド ライン プロパティを使用する方法の詳細については、「[System Center Configuration Manager のクライアント インストール プロパティについて](../../../core/clients/deploy/about-client-installation-properties.md)」を参照してください。  

### <a name="to-configure-the-client-cache-folder-when-you-install-clients-by-using-client-push-installation"></a>クライアント プッシュ インストールによってクライアントをインストールするときにクライアント キャッシュを構成するには  

1.  Configuration Manager コンソールで、[**管理**] > [**サイトの構成**] > [**サイト**] の順に選択します。  

3.  適切なサイトを選択し、**[ホーム]** タブの **[設定]** グループで **[クライアント インストール設定]** > **[インストールのプロパティ]** タブを選択します。  

5.  スペース区切りで次のプロパティを指定します。  

    -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > バージョン 1606 では、SMSCACHESIZE ではなく Configuration Manager コンソールの **[クライアント設定]** で使用可能なキャッシュ サイズ設定を使用します。 詳細については、「[クライアントのキャッシュ設定](../../../core/clients/deploy/about-client-settings.md#client-cache-settings)」を参照してください。

       CCMSetup.exe 用のこれらのコマンド ライン プロパティを使用する方法の詳細については、「[System Center Configuration Manager のクライアント インストール プロパティについて](../../../core/clients/deploy/about-client-installation-properties.md)」を参照してください。  

### <a name="to-configure-the-client-cache-folder-on-the-client-computer"></a>クライアント コンピューターでクライアント キャッシュ フォルダーを構成するには  

1.  クライアント コンピューターで、コントロール パネルの **[Configuration Manager]** に移動し、ダブルクリックしてプロパティを開きます。  

2.  **[キャッシュ]** タブで領域と場所のプロパティを設定します。 既定の場所は *%windir%*\ccmcache です。  

5.  キャッシュ フォルダーのファイルを削除するには、**[ファイルの削除]** を選択します。  

    > [!NOTE]
    > 
    > キャッシュ フォルダーは通常の Windows フォルダーです。そのため、スクリプト、ユーティリティ、または PowerShell コマンドレット `Remove-Item` を使用してフォルダーの内容を自動的に削除することができます。 


### <a name="to-configure-client-cache-size-in-client-settings"></a>[クライアント設定] でクライアント キャッシュ サイズを構成するには

バージョン 1606 以降、クライアントを再インストールしなくても、クライアント キャッシュ フォルダーのサイズを調整できるようになりました。 これを行うには、Configuration Manager コンソールで [クライアント設定] を使用してクライアント キャッシュ サイズを構成します。  

1. Configuration Manager コンソールで、 **[管理]** > **[クライアント設定]**に移動します。

2. **[既定のクライアント設定]**をダブルクリックします。
  また、キャッシュ サイズをより選択的に適用するためにカスタム クライアント設定を作成することもできます。 既定およびカスタムのクライアント設定の詳細については、「[System Center Configuration Manager でクライアント設定を構成する方法](../../../core/clients/deploy/configure-client-settings.md)」を参照してください。

 3. **[クライアント キャッシュの設定]** を選択し、**[クライアント キャッシュ サイズの構成]** で **[はい]** を選択して、ディスク設定の **[MB]** または **[割合]** のいずれかを使用します。 いずれか小さい方のサイズにキャッシュが調整されます。

     Configuration Manager クライアントは、次のクライアント ポリシーがダウンロードされるときにこれらの設定値を使ってキャッシュ サイズを構成します。

##  <a name="BKMK_UninstalClient"></a> Configuration Manager クライアントをアンインストールする  
 **/Uninstall** プロパティを付けて **CCMSetup.exe** を使用すると、Windows Configuration Manager クライアント ソフトウェアをコンピューターからアンインストールできます。 個々のコンピューター上でコマンド プロンプトから CCMSetup.exe を実行するか、パッケージとプログラムを展開して、コンピューターのコレクションからクライアントをアンインストールします。  

> [!WARNING]  
>  Configuration Manager クライアントをモバイル デバイスからアンインストールすることはできません。 Configuration Manager クライアントをモバイル デバイスから除去する必要がある場合は、デバイスをワイプする必要があります。ワイプはモバイル デバイス上のすべてのデータを削除します。  

#### <a name="to-uninstall-the-configuration-manager-client-from-the-command-prompt"></a>コマンド プロンプトから Configuration Manager クライアントをアンインストールするには  

1.  Windows コマンド プロンプトを開き、CCMSetup.exe のある場所へフォルダーを移動します。  

2.  「 **Ccmsetup.exe /uninstall**」と入力し、 **Enter**キーを押します。  

> [!NOTE]  
>  アンインストールを実行しても、画面に結果は表示されません。 クライアントのアンインストールが成功したことを確認するには、クライアント コンピューター上の **%windir%\ ccmsetup** 内にあるログ ファイル *CCMSetup.log* を確認します。  

##  <a name="BKMK_ConflictingRecords"></a> Configuration Manager クライアントの競合しているレコードを管理する  
 Configuration Manager は、ハードウェア ID を使用して重複している可能性のあるクライアントを特定し、競合するレコードについて警告を発します。 たとえば、コンピューターを再インストールする場合、ハードウェア ID が同じであっても Configuration Manager の使用する GUID が異なる可能性があります。  

 コンピューター アカウントの Windows 認証または信頼されたソースからの PKI 証明書を使用して Configuration Manager が競合を解決できる場合、競合は自動的に解決されます。 ただし、Configuration Manager が競合を解決できない場合は階層設定が使用され、重複するハードウェア ID を検出したときにレコードを自動的にマージするか (既定の設定)、新しいクライアント レコードをマージ、ブロック、または作成するタイミングを管理者が決定できます。 重複レコードを手動で管理すると決定した場合、Configuration Manager コンソールを使用して競合するレコードを手動で解決する必要があります。  


#### <a name="to-change-the-hierarchy-setting-for-managing-conflicting-records"></a>競合しているレコードの管理に関する階層の設定を変更するには  

1.  Configuration Manager コンソールで、**[管理]** > **[サイトの構成]** > **[サイト]** > **[階層設定]** の順に選択します。
2.  **[クライアントの承認と競合レコードの処理]** タブで **[競合しているレコードを自動的に解決する]** または **[競合しているレコードを手動で解決する]** を選択します。  

#### <a name="to-manually-resolve-conflicting-records"></a>競合しているレコードを手動で解決するには  

1.  Configuration Manager コンソールで **[監視]** > **[システムのステータス]** > **[競合しているレコード]** を選択します。  

3.  1 つまたは複数の競合しているレコードを選択し、**[競合しているレコード]** をクリックします。  

4.  次のいずれかを選択します。  

    -   **[結合]**: 新しく検出されたレコードを既存のクライアント レコードと結合します。  

    -   [**新規** ]: 競合しているクライアント レコードに対して新しいレコードを作成します。  

    -   [**ブロック** ]: 競合しているクライアント レコードに対して新しいレコードを作成しますが、ブロックに設定します。  

## <a name="manage-duplicate-hardware-identifiers"></a>重複するハードウェア識別子を管理する
Configuration Manager バージョン 1610 より、PXE ブートとクライアント登録で Configuration Manager が無視するハードウェア ID の一覧を指定できます。 それにより 2 つの一般的な問題に対処できます。

1. Surface Pro 3 など、新しいデバイスの多くにオンボード イーサネット ポートが含まれません。 オペレーティング システムの展開で有線接続を確立するとき、一般的に USB/イーサネット アダプターが使用されます。 しかしながら、コストや汎用性に起因し、多くの場合、共有アダプターになります。 そのアダプターの MAC アドレスを利用してデバイスを識別するため、展開ごとに管理者による追加措置がないと、アダプターの再利用が問題になります。 バージョン 1610 以降、このアダプターの MAC アドレスを除外できるようになったので、このシナリオで再利用できます。
2. SMBIOS ID は一意のハードウェア識別子ですが、専門的なハードウェア デバイスには ID が重複するものもあります。 上記の USB/イーサネット アダプターのシナリオほど一般的ではありませんが、ハードウェア ID の一覧を利用してこの問題に対処することもできます。

#### <a name="to-add-hardware-identifiers-for-configuration-manager-to-ignore"></a>Configuration Manager で無視するハードウェア識別子を追加するには  
1. Configuration Manager コンソールで、[**管理**] > [**概要**] > [**サイトの構成**] > [**サイト**] の順に移動します。
2. **[ホーム]** タブの **[サイト]** グループで、**[階層設定]** を選択します。
3. **[クライアントの承認と競合レコードの処理]** タブの **[重複するハードウェア ID]** セクションの **[追加]** を選択して、新しいハードウェア識別子を追加します。

##  <a name="BKMK_PolicyRetrieval"></a> Configuration Manager クライアントのポリシーの取得開始  
 Windows Configuration Manager クライアントは、クライアント設定として構成されているスケジュールに従ってクライアント ポリシーをダウンロードします。 ただし、トラブルシューティングやテストなどで、クライアントから特別なポリシー取得を開始する場合があります。  

次の方法でポリシーの取得を開始できます。


- [クライアント通知](#initiate-client-policy-retrieval-using-client-notification) 
- [クライアントの **[操作]** タブ](#manually-initiate-client-policy-retrieval-on-the-actions-tab-of-the-configuration-manager-client)
- [スクリプト](#manually-initiate-client-policy-retrieval-by-script)

> [!NOTE]  
>   
>  Linux および UNIX を実行するクライアントのポリシー取得については、「 [Computer policy for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_PolicyforLnU)」をご覧ください。  

#### <a name="initiate-client-policy-retrieval-using-client-notification"></a>クライアント通知を使用してクライアント ポリシーの取得を開始する  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[デバイス コレクション]** の順に選択します。  

3.  ポリシーをダウンロードするコンピューターを含むデバイス コレクションを選択します。 **[ホーム]** タブの **[コレクション]** グループで **[クライアント通知]** > **[コンピューター ポリシーのダウンロード]** を選択します。  

    > [!NOTE]  
    >  また、[ **デバイス** ] ノードの一時コレクション ノードに表示されるデバイスから 1 つまたは複数のデバイスを選択して、クライアント通知を使用してポリシーの取得を開始することもできます。  

#### <a name="manually-initiate-client-policy-retrieval-on-the-actions-tab-of-the-configuration-manager-client"></a>Configuration Manager クライアントの [操作] タブでクライアント ポリシーの取得を手動で開始する  

1.  コンピューターのコントロール パネルで、[ **Configuration Manager** ] を選択します。  

2.  **[操作]** タブの **[コンピューター ポリシーの取得および評価サイクル]** を選択してコンピューター ポリシーを開始し、**[直ちに実行]** をクリックします。  

4.  **[OK]** を選択してプロンプトを確定します。  

5.  ユーザー クライアント設定で必要な他の操作 (**[ユーザー ポリシーの取得および評価サイクル]** など) に関して、手順 3 と 4 を繰り返します。  

#### <a name="manually-initiate-client-policy-retrieval-by-script"></a>スクリプトを使用してクライアント ポリシーの取得を手動で開始する  

1.  メモ帳などのテキスト エディターを開きます。  

2.  次をコピーし、ファイルに挿入します。  

    ```  
    on error resume next  

    dim oCPAppletMgr 'Control Applet manager object.  
    dim oClientAction 'Individual client action.  
    dim oClientActions 'A collection of client actions.  

    'Get the Control Panel manager object.  
    set  oCPAppletMgr=CreateObject("CPApplet.CPAppletMgr")  
    if err.number <> 0 then  
        Wscript.echo "Couldn't create control panel application manager"  
        WScript.Quit  
    end if  

    'Get a collection of actions.  
    set oClientActions=oCPAppletMgr.GetClientActions  
    if err.number<>0 then  
        wscript.echo "Couldn't get the client actions"  
        set oCPAppletMgr=nothing  
        WScript.Quit  
    end if  

    'Display each client action name and perform it.  
    For Each oClientAction In oClientActions  

        if oClientAction.Name = "Request & Evaluate Machine Policy" then  
            wscript.echo "Performing action " + oClientAction.Name   
            oClientAction.PerformAction  
        end if  
    next  

    set oClientActions=nothing  
    set oCPAppletMgr=nothing  
    ```  

3.  ファイルを .vbs 拡張子で保存します。  

4.  クライアント コンピューターにおいて、次のいずれかの方法でこのファイルを実行します。  

    -   エクスプローラーを使用してファイルに移動し、スクリプト ファイルをダブルクリックします。  

    -   コマンド プロンプトを開き、「**cscript &lt;パス\ファイル名.vbs>**」と入力します。  

5.  **[Windows スクリプト ホスト]** ダイアログ ボックスで **[OK]** をクリックします。  

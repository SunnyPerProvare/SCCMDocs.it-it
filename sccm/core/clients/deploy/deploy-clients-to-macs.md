---
title: "Mac クライアントの展開 | Microsoft Docs"
description: "System Center Configuration Manager でクライアントを Mac コンピューターに展開する方法を説明します。"
ms.custom: na
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.reviewer: aaroncz
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
caps.latest.revision: "12"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 6ce212c6745b70a47553891e5dbc124b4c4e50fa
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-deploy-clients-to-macs"></a>How to deploy clients to Macs

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックでは、Mac コンピューターに Configuration Manager クライアントを展開して管理する方法について説明します。 Mac コンピューターにクライアントを展開する前に構成する必要がある内容の詳細については、「[Mac コンピューターにクライアント ソフトウェアを展開するための準備](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients)」を参照してください。

Mac コンピューター用の新しいクライアントをインストールする場合は、Configuration Manager の更新プログラムをインストールして、Configuration Manager コンソールで新しいクライアント情報を反映する必要もあります。

これらの手順には、クライアント証明書をインストールするための 2 つのオプションがあります。 Mac コンピューターのクライアント証明書の詳細については、「[Mac コンピューターにクライアント ソフトウェアを展開するための準備](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#certificate-requirements)」を参照してください。  

-   [CMEnroll ツール](#install-the-client-and-then-enroll-the-client-certificate-on-the-mac) を使用して Configuration Manager 登録を使用する。 登録プロセスでは自動証明書更新がサポートされていないため、インストールされている証明書が期限切れになる前に、Mac コンピューターを再登録する必要があります。    

-   [Configuration Manager とは独立した証明書の要求とインストールの方法を使用する](#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager)。 

>[!IMPORTANT]
>  Mac OS Sierra を実行しているデバイスにクライアントを展開するには、管理ポイント証明書のサブジェクト名を正しく構成する必要があります。たとえば、管理ポイント サーバーの FQDN を指定します。


## <a name="configure-client-settings-for-enrollment"></a>登録のためのクライアント設定を構成する  
 Mac コンピューターの登録を構成するには、[既定のクライアント設定](../../../core/clients/deploy/about-client-settings.md)を使用する必要があります。カスタムのクライアント設定は使用できません。  

 この手順は、Configuration Manager が Mac で証明書を要求してインストールするために必要です。  

### <a name="to-configure-the-default-client-settings-for-configuration-manager-to-enroll-certificates-for-macs"></a>Mac に証明書を登録する Configuration Manager の既定のクライアント設定を構成するには  

1.  Configuration Manager コンソールで、**[管理]** >  **[クライアント設定]** > **[既定のクライアント設定]** の順に選択します。  

4.  **[ホーム]** タブの **[プロパティ]** グループで、**[プロパティ]** を選択します。  

5.  **[登録]** セクションを選択し、次の設定を構成します。  

    1.  **ユーザーがモバイル デバイスと Mac コンピューターを登録できるようにする: はい**  

    2.  **[登録プロファイル]:** **[プロファイルの設定]** を選択します。  

6.  **[モバイル デバイス登録プロファイル]** ダイアログ ボックスで、**[作成]** をクリックします。  

7.  [ **登録プロファイルの作成** ] ダイアログ ボックスで、この登録プロファイルの名前を入力し、[ **管理サイト コード**] を構成します。 Mac コンピューターを管理する管理ポイントを含む Configuration Manager プライマリ サイトを選択します。  

    > [!NOTE]  
    >  サイトを選択できない場合は、そのサイト内で少なくとも 1 つの管理ポイントがモバイル デバイスをサポートするように構成されていることを確認してください。  

8.  **[追加]** を選びます。  

9. **[モバイル デバイスの証明機関の追加]** ダイアログ ボックスで、Mac コンピューターに証明書を発行する認証機関 (CA) サーバーを選択します。  

10. **[登録プロファイルの作成]** ダイアログ ボックスで、手順 3 で作成した Mac コンピューター証明書テンプレートを選択します。  

11. **[OK]** をクリックして **[登録プロファイル]** ダイアログ ボックスを閉じ、**[既定のクライアント設定]** ダイアログ ボックスを閉じます。  

    > [!TIP]  
    >  クライアント ポリシーの間隔を変更する場合、**[クライアント ポリシー]** クライアント設定グループの **[クライアント ポリシーのポーリング間隔]** を使用します。  

 すべてのユーザーは、次にクライアント ポリシーをダウンロードするときに、これらの設定で構成されます。 1 つのクライアントのポリシーの取得を開始するには、「[構成マネージャー クライアントのポリシーの取得開始](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval)」をご覧ください。  

 登録クライアント設定の他に、次のクライアント デバイス設定が構成されていることを確認します。  

-   **[ハードウェア インベントリ]**: Mac および Windows クライアント コンピューターからハードウェア インベントリを収集する場合、この設定を有効にして構成します。 詳細については、「[System Center Configuration Manager でのハードウェア インベントリの拡張方法](../../../core/clients/manage/inventory/extend-hardware-inventory.md)」をご覧ください。  

-   **[コンプライアンス設定]**: Mac および Windows クライアント コンピューターの設定を評価して修復する場合、この設定を有効にして構成します。 詳細については、「[コンプライアンス設定の計画と構成](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)」をご覧ください。  

> [!NOTE]  
>  構成マネージャー クライアント設定の詳細については、「[System Center Configuration Manager でクライアント設定を構成する方法](../../../core/clients/deploy/configure-client-settings.md)」をご覧ください。  

## <a name="download-the-client-source-files-for-macs"></a>Mac 用のクライアント ソース ファイルをダウンロードする  

1.  Mac OS X クライアント ファイル パッケージ ( **ConfigmgrMacClient.msi**) をダウンロードして、Windows を実行しているコンピューターに保存します。  

     このファイルは Configuration Manager インストール メディアに含まれていません。 このファイルは、 [Microsoft ダウンロード センター](http://go.microsoft.com/fwlink/?LinkID=525184)からダウンロードできます。  

2.  Windows コンピューターで、**ConfigmgrMacClient.msi** を実行し、Mac クライアント パッケージ (Macclient.dmg) をローカル ディスクのフォルダー (既定では、**C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client\\**) に抽出します。  

3.  Macclient.dmg ファイルを Mac コンピューターのフォルダーにコピーします。  

4.  Mac コンピューターで、Macclient.dmg ファイルを実行して、ローカル ディスクのフォルダーにファイルを抽出します。  

5.  フォルダーに Ccmsetup と CMClient.pkg ファイルが抽出されていることと、Tools という名前のフォルダーが作成され、CMDiagnostics、CMUninstall、CMAppUtil and CMEnroll ツールが含まれていることを確認します。

    -  **Ccmsetup**: Mac コンピューターに Configuration Manager クライアントをインストールします。  

    -   **CMDiagnostics**: Mac コンピューターの Configuration Manager クライアントに関連する診断情報を収集します。  

    -   **CMUninstall**: Mac コンピューターからクライアントをアンインストールします。  

    -   **CMAppUtil**: Apple アプリケーション パッケージを Configuration Manager アプリケーションとして展開できる形式に変換します。  

    -   **CMEnroll**: Mac コンピューター用のクライアント証明書を要求してインストールし、Configuration Manager クライアントをインストールできるようにします。   

## <a name="install-the-client-and-then-enroll-the-client-certificate-on-the-mac"></a>Mac にクライアントをインストールし、クライアント証明書を登録する  

[Mac コンピューターの登録ウィザード](#enroll-the-client-with-the-mac-computer-enrollment-wizard)で個々のクライアントを登録することができます。

多数のクライアントを登録できる自動化の場合、[CMEnroll ツール](#client-and-certificate-automation-with-cmenroll)を使用します。   


###  <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>Mac コンピューターの登録ウィザードでクライアントを登録する  

1.  クライアントのインストールを完了したら、コンピューターの登録ウィザードが開きます。 ウィザードが開かない場合や、間違ってウィザードを閉じてしまった場合は、**Configuration Manager** の環境設定ページで **[登録]** をクリックして、ウィザードを開いてください。  

2.  ウィザードの 2 番目のページで、次のように指定します。  

    -   **ユーザー名** : 次の形式で入力できます。  

        -   'ドメイン\名前' (たとえば、'contoso\mnorth')  

        -   'user@domain'. 例: 'mnorth@contoso.com'  

            > [!IMPORTANT]  
            >  電子メール アドレスを使用して **[ユーザー名]** フィールドを指定すると、Configuration Manager により、電子メール アドレスのドメイン名と登録プロキシ ポイント サーバーの既定の名前を使用して **[サーバー名]** フィールドが自動的に指定されます。 このドメイン名とサーバー名が登録プロキシ ポイント サーバーの名前と一致しない場合は、Mac コンピューターを登録するときに使用する正しい名前をユーザーに知らせます。  

         ユーザー名と、対応するパスワードは、Mac クライアント証明書テンプレートに対する読み取り権限と登録権限が付与された Active Directory ユーザー アカウントと一致している必要があります。  

    -   **パスワード**: 指定したユーザー名に対応するパスワードを入力します。  

    -   **サーバー名**: 登録プロキシ ポイント サーバーの名前を入力します。  


### <a name="client-and-certificate-automation-with-cmenroll"></a>CMEnroll によるクライアントと証明書の自動化  

CMEnroll ツールでクライアントのインストール、クライアント証明書の要求と登録を自動化する場合に、この手順を使用します。 ツールを実行するには、Active Directory ユーザー アカウントが必要です。

1.  Mac コンピューターで、Macclient.dmg ファイルのコンテンツを抽出したフォルダーに移動します。  

2.  次のコマンドラインを入力します。 **sudo ./ccmsetup**  

3.  「 **Completed installation (インストール完了)** 」メッセージが表示されるまで待ちます。 インストーラーでは、再起動が必要というメッセージが表示されますが、ここでは再起動せず、次の手順に進みます。  

4.  Mac コンピューターの Tools フォルダーで、次のコマンドを入力します: **sudo ./CMEnroll -s &lt;enrollment_proxy_server_name> -ignorecertchainvalidation -u &lt;user name'>**  

    クライアントのインストール後に、Mac コンピューターの登録ウィザードを使用して Mac コンピューターを登録できます。 この方法でクライアントを登録する場合は、このトピックの「 [To enroll the client by using the Mac Computer Enrollment Wizard](#BKMK_EnrollR2) 」を参照してください。  

5. Active Directory ユーザー アカウントのパスワードを入力します。  このコマンドを入力すると、2 つのパスワードの入力が求められます。最初のプロンプトは、コマンドを実行するスーパー ユーザー アカウント用です。 2 つ目のプロンプトは、Active Directory ユーザー アカウント用です。 プロンプトは似ているため、正しい順番で指定するように気を付けてください。  

    ユーザー名は、次の形式で入力できます。  

    -   'ドメイン\名前' (たとえば、'contoso\mnorth')  

    -   'user@domain'. 例: 'mnorth@contoso.com'  

     ユーザー名と、対応するパスワードは、Mac クライアント証明書テンプレートに対する読み取り権限と登録権限が付与された Active Directory ユーザー アカウントと一致している必要があります。  

     例: 登録プロキシ ポイント サーバーの名前が **server02.contoso.com** で、ユーザー名が **contoso\mnorth**のユーザーに Mac クライアント証明書テンプレートに対するアクセス許可が付与されている場合、次のように入力します: **sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'**  

    > [!NOTE]  
    >  ユーザー名に **&lt;>"+=** のいずれかの文字が含まれている場合、登録は失敗します。 これらの文字が含まれていないユーザー名で帯域外証明書を取得します。  
    >  
    >  ユーザー エクスペリエンスを単純化するには、インストール手順とコマンドをスクリプト化し、ユーザーがユーザー名とパスワードを指定するだけで済むようにします。  

5.  「 **Successfully enrolled (正常に登録されました)** 」メッセージが表示されるまで待ちます。  

6.  Mac コンピューターで、登録する証明書を Configuration Manager に制限するには、ターミナル ウィンドウを開き、次のように変更します。  

    a.  コマンド **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**を入力します。  

    b.  **[キーチェーン アクセス]** ダイアログ ボックスの **[キーチェーン]** セクションで、**[システム]** を選択し、**[カテゴリ]** セクションの **[キー]** を選択します。  

    c.  キーを展開してクライアント証明書を表示します。 インストールした秘密キーの証明書を特定したら、そのキーをダブルクリックします。  

    d.  **[アクセス制御]** タブで、**[アクセスを許可する前に確認する]** を選択します。  

    e.  **/Library/Application Support/Microsoft/CCM** を参照し、**[CCMClient]** を選択して **[追加]** を選択します。  

    f.  **[変更を保存]** をクリックし、**[キーチェーン アクセス]** ダイアログ ボックスを閉じます。  

7.  Mac コンピューターを再起動します。  

 Mac コンピューターの [ **システム環境設定** ] で [ **Configuration Manager** ] 項目を開いて、クライアントのインストールが正常に完了したことを確認します。 また、[ **すべてのシステム** ] コレクションを更新して表示し、Mac コンピューターが管理されたクライアントとして、このコレクションに表示されていることを確認できます。  

> [!TIP]  
>  Mac クライアントに関するトラブルシューティングを行うために、Mac OS X クライアント パッケージに含まれている CMDiagnostics プログラムを使用して、次の診断情報を収集できます。  
>   
>  -   実行中のプロセスの一覧  
> -   Mac OS X オペレーティング システムのバージョン  
> -   構成マネージャー クライアントに関連する Mac OS X のクラッシュ レポート (**CCM\*.crash** と **System Preference.crash** を含む)  
> -   構成マネージャー クライアントのインストールで作成される Bill of Materials (BOM) ファイルとプロパティ一覧 (.plist) ファイル  
> -   /Library/Application Support/Microsoft/CCM/Logs フォルダーの内容  
>   
>  CmDiagnostics で収集された情報は、コンピューターのデスクトップに保存される zip ファイルに追加され、cmdiag-*<ホスト名\>***-***&gt;日付と時刻\>*.zip という名前が付けられます。***


##  <a name="use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager"></a>Configuration Manager とは独立した証明書要求およびインストール方法を使用する  

まず、「[Mac コンピューターにクライアント ソフトウェアを展開するための準備](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients)」の以下の特定のタスクを実行します。

1. [Web サーバー証明書をサイト システム サーバーに展開する](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#deploy-a-web-server-certificate-to-site-system-servers)

2. [クライアント認証証明書をサイト システム サーバーに展開する](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#deploy-a-client-authentication-certificate-to-site-system-servers)

3. [管理ポイントおよび配布ポイントを構成する](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#configure-the-management-point-and-distribution-point)

4. [オプション: レポート サービス ポイントをインストールする](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#install-the-reporting-services-point)

次に、以下のタスクを実行します。

5. [Mac 用のクライアント ソース ファイルをダウンロードする](#download-the-client-source-files-for-macs) .  
6. 選択した証明書の展開方法で指定されている指示に従い、クライアント証明書を要求して、Mac コンピューターにインストールします。  
7.  Microsoft ダウンロード センターからダウンロードした macclient.dmg ファイルのコンテンツを抽出したフォルダーに移動します。  

3.  次のコマンドラインを入力します: **sudo ./ccmsetup -MP <管理ポイントのインターネット FQDN\> -SubjectName <証明書のサブジェクト値\>**。  証明書のサブジェクト値は大文字と小文字が区別されるので、証明書の詳細に表示されるとおりに入力してください。  

     例: サイト システムのプロパティのインターネット FQDN が **server03.contoso.com** であり、Mac クライアント証明書が証明書のサブジェクトで共通名として **mac12.contoso.com** という FQDN を持っている場合、次のように入力します: **sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com**  

4.  **"Completed installation** " というメッセージが表示されるまで待ってから、Mac コンピューターを再起動します。  

5.  Mac コンピューターで、この証明書から Configuration Manager にアクセスできるようにするには、ターミナル ウィンドウを開き、次のように変更します。  

    a.  コマンド **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**を入力します。  

    b.  **[キーチェーン アクセス]** ダイアログ ボックスの **[キーチェーン]** セクションで、**[システム]** を選択し、**[カテゴリ]** セクションの **[キー]** を選択します。  

    c.  キーを展開してクライアント証明書を表示します。 インストールした秘密キーの証明書を特定したら、そのキーをダブルクリックします。  

    d.  **[アクセス制御]** タブで、**[アクセスを許可する前に確認する]** を選択します。  

    e.  **/Library/Application Support/Microsoft/CCM** を参照し、**[CCMClient]** を選択して **[追加]** を選択します。  

    f.  **[変更を保存]** をクリックし、**[キーチェーン アクセス]** ダイアログ ボックスを閉じます。  

6.  同じサブジェクト値を含む証明書が複数ある場合、構成マネージャー クライアントに使用する証明書を特定するには、証明書のシリアル番号を指定する必要があります。 このためには、次のコマンドを使用します: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<シリアル番号\>"**  

     たとえば、次のように入力します。 **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

 Mac の **[システム環境設定]** で **[Configuration Manager]** 項目を開いて、クライアントのインストールが正常に完了したことを確認します。 また、**[すべてのシステム]** コレクションを更新して表示し、Mac が管理されたクライアントとして、このコレクションに表示されていることを確認できます。  

## <a name="renewing-the-mac-client-certificate"></a>Mac クライアント証明書の更新  
 Mac コンピューターのコンピューター証明書を更新する前に、次の手順を実行します。  

 この手順で SMSID を削除します。SMSID は、クライアントが Mac コンピューターで新規または更新された証明書を使用するときに必要です。  

> [!IMPORTANT]  
>  クライアント SMSID を削除して置き換えると、Configuration Manager コンソールからクライアントが削除された後に、インベントリなどの保存されているクライアント履歴も削除されます。  

### <a name="to-renew-the-mac-client-certificate"></a>Mac クライアント証明書を更新するには  

1.  ユーザー証明書を更新する必要がある Mac コンピューターのデバイス コレクションを作成します。  

2.  [ **資産とコンプライアンス** ] ワークスペースで、 **構成項目の作成ウィザード** を開始します。  

3.  ウィザードの [ **全般** ] ページで、次の情報を指定します。  

    -   **[名前]:Mac の SMSID の削除**  

    -   **[種類]:Mac OS X**  

4.  ウィザードの [ **サポートされているプラットフォーム** ] ページで、すべての Mac OS X バージョンが選択されていることを確認します。  

5.  ウィザードの [ **設定** ] ページで [ **新規作成** ] をクリックし、[ **設定の作成** ] ダイアログ ボックスで次の情報を指定します。  

    -   **[名前]:Mac の SMSID の削除**  

    -   **[設定の種類]:スクリプト**  

    -   **[データ型]:文字列**  

6.  **[設定の作成]** ダイアログ ボックスの **[検索スクリプト]**で **[スクリプトの追加]** をクリックし、SMSID が構成されている Mac コンピューターを検出するスクリプトを指定します。  

7.  [ **探索スクリプトの編集** ] ダイアログ ボックスで、次のシェル スクリプトを入力します。  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  **[OK]** を選択して、**[探索スクリプトの編集]** ダイアログ ボックスを閉じます。  

9. **[設定の作成]** ダイアログ ボックスの **[修復スクリプト (オプション)]** で、**[スクリプトの追加]** を選択して、Mac コンピューターで見つかった SMSID を削除するスクリプトを指定します。  

10. [ **修復スクリプトの作成** ] ダイアログ ボックスで、次のシェル スクリプトを入力します。  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. **[OK]** を選択して **[修復スクリプトの作成]** ダイアログ ボックスを閉じます。  

12. ウィザードの **[コンプライアンス規則]** ページで **[新規作成]** を選択し、**[規則の作成]** ダイアログ ボックスで次の情報を指定します。  

    -   **[名前]:Mac の SMSID の削除**  

    -   **[選択した設定]:** **[参照]** を選択し、前に指定した探索スクリプトを選びます。  

    -   **[次の値]** フィールドに「**存在しないドメインと既定のペア (com.microsoft.ccmclient, SMSID)**」と入力します。  

    -   オプション [ **この設定が対応していない場合に指定した修復スクリプトを実行する** ] を有効にします。  

13. 構成項目の作成ウィザードを完了します。  

14. 作成した構成項目を含む構成基準を作成し、それを手順 1 で作成したデバイス コレクションに展開します。  

     構成基準の作成方法と展開方法の詳細については、「[System Center Configuration Manager で構成基準を作成する方法](../../../compliance/deploy-use/create-configuration-baselines.md)」をご覧ください。  

15. SMSID を削除した Mac コンピューターに新しい証明書をインストールしたら、次のコマンドを実行して、新しい証明書を使用するクライアントを構成します。  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <Subject_Name_of_New_Certificate>  
    ```  

16. 同じサブジェクト値を含む証明書が複数ある場合、構成マネージャー クライアントに使用する証明書を特定するには、証明書のシリアル番号を指定する必要があります。 このためには、次のコマンドを使用します: **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<シリアル番号\>"**  

     たとえば、次のように入力します。 **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

17. 再起動します。  


## <a name="see-also"></a>関連項目

[Mac クライアントを維持する](/sccm/core/clients/manage/maintain-mac-clients)

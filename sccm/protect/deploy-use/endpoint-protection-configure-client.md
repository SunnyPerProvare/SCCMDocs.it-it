---
title: "Endpoint Protection クライアントの構成 | Microsoft Docs"
description: "階層内のコンピューターのコレクションに展開できる Endpoint Protection のカスタム クライアント設定を構成する方法について説明します。"
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 1488aaa465fb9810bc1b641d41dad95189d37418
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="configure-custom-client-settings-for-endpoint-protection"></a>Endpoint Protection のカスタム クライアント設定を構成する

*適用対象: System Center Configuration Manager (Current Branch)*

この手順では、階層内のコンピューターのコレクションに展開できる Endpoint Protection のカスタム クライアント設定を構成します。

> [!IMPORTANT]
>  階層内のすべてのコンピューターに適用する場合にのみ、既定の Endpoint Protection クライアント設定を構成します。

## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>Endpoint Protection を有効にしてカスタム クライアント設定を構成するには

1.  Configuration Manager コンソールで、[ **管理**] をクリックします。

2.  [ **管理** ] ワークスペースで [ **クライアント設定**] をクリックします。

3.  [ホーム **** ] タブの [作成 **** ] グループで、[カスタム クライアント デバイス設定の作成 ****] をクリックします。

4.  [カスタム クライアント デバイス設定の作成 **** ] ダイアログ ボックスで、設定のグループの名前と説明を指定し、[Endpoint Protection ****] を選択します。

5.  必要な Endpoint Protection クライアント設定を構成します。 構成できる Endpoint Protection クライアント設定の完全な一覧については、「[System Center Configuration Manager のクライアント設定について](../../core/clients/deploy/about-client-settings.md)」の「Endpoint Protection」セクションをご覧ください。

   > [!IMPORTANT]
   >  Endpoint Protection のクライアント設定を構成するには、事前に Endpoint Protection サイト システムの役割をインストールしておく必要があります。

6.  [OK **** ] をクリックして [カスタム クライアント デバイス設定の作成 **** ] ダイアログ ボックスを閉じます。 新しいクライアント設定は、[管理 **** ] ワークスペースの [クライアント設定 **** ] ノードに表示されます。

7.  カスタム クライアント設定を使用する前に、この設定をコレクションに展開する必要があります。 展開するカスタム クライアント設定を選択し、[ホーム **** ] タブの [クライアント設定 **** ] グループで [展開 ****] をクリックします。

8.  [コレクションの選択 **** ] ダイアログ ボックスで、クライアント設定を展開するコレクションを選択し、[OK ****] をクリックします。 新しい展開は、詳細ウィンドウの [展開 **** ] タブに表示されます。

クライアント コンピューターは、次にクライアント ポリシーをダウンロードするときに、これらの設定で構成されます。 単一クライアントのポリシーの取得を開始する場合は、「[How to manage clients in System Center Configuration Manager](../../core/clients/manage/manage-clients.md)」 (System Center Configuration Manager でのクライアントの管理方法) の「Initiate Policy Retrieval for a Configuration Manager Client」 (構成マネージャー クライアントのポリシーの取得開始) セクションをご覧ください。

## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image-in-configuration-manager"></a>Configuration Manager で Endpoint Protection クライアントをディスク イメージにプロビジョニングする方法
Configuration Manager のオペレーティング システムの展開でディスク イメージ ソースとして使用するコンピューターに、Endpoint Protection クライアントをインストールできます。 このコンピューターは通常、参照コンピューターと呼ばれます。 オペレーティング システムのイメージを作成したら、次に、Configuration Manager のオペレーティング システムの展開を使用して、Endpoint Protection などのソフトウェア パッケージを含めることができるイメージをクライアント コンピューターに展開できます。

参照コンピューターに Endpoint Protection クライアントをインストールして構成するには、このトピックの手順に従います。

### <a name="prerequisites-for-installing-the-endpoint-protection-client-on-the-reference-computer"></a>参照コンピューターに Endpoint Protection クライアントをインストールするための前提条件
以下に、参照コンピューターに Endpoint Protection クライアント ソフトウェアをインストールするために必要な前提条件を示します。

-   Endpoint Protection クライアント インストール パッケージ **scepinstall.exe** にアクセスできる必要があります。 このパッケージは、サイト サーバー上の Microsoft System Center Configuration Manager インストール フォルダーの **Client** フォルダーにあります。

-   Endpoint Protection クライアントを組織で必要な構成で展開できるように、マルウェア対策ポリシーを作成してから、そのポリシーをエクスポートします。 その後、Endpoint Protection クライアントを手動でインストールするときに、使用するマルウェア対策ポリシーを指定できます。 詳細については、「[System Center Configuration Manager で Endpoint Protection 用にマルウェア対策ポリシーを作成し展開する方法](endpoint-antimalware-policies.md)」をご覧ください。

   > [!NOTE]
   >  [既定のクライアント マルウェア対策ポリシー **** ] をエクスポートすることはできません。

-   Endpoint Protection クライアントを最新の定義とともにインストールする場合、[Microsoft マルウェア プロテクション センター](http://go.microsoft.com/fwlink/?LinkID=200965)からダウンロードする必要があります。

### <a name="how-to-install-the-endpoint-protection-client-software-on-the-reference-computer"></a>参照コンピューターに Endpoint Protection クライアント ソフトウェアをインストールする方法
コマンド プロンプトから、Endpoint Protection クライアントを参照コンピューターのローカルにインストールできます。 このためには、まず、インストール ファイル **scepinstall.exe**を取得する必要があります。 事前に構成したマルウェア対策ポリシーまたは先にエクスポートしたマルウェア対策ポリシーとともに、クライアントをインストールすることもできます。

## <a name="to-install-the-endpoint-protection-client-from-a-command-prompt"></a>コマンド プロンプトで Endpoint Protection クライアントをインストールするには

1.  System Center Configuration Manager インストール メディアの **Client** フォルダーから、Endpoint Protection クライアント ソフトウェアをインストールするコンピューターに **scepinstall.exe** をコピーします。

2.  管理者特権でコマンド プロンプトを開き、 **scepinstall.exe** が配置されているフォルダーに移動してから、必要なコマンド ライン プロパティを追加して次のコマンドを実行します。

   ```
   scepinstall.exe
   ```

    次のいずれかのコマンド ライン プロパティを指定できます。

   |プロパティ|説明|
   |--------------|-----------------|
   |/s|サイレント インストールを実行することを指定します。|
   |/q|セットアップ ファイルの自動抽出を実行することを指定します。|
   |/i|標準インストールを実行することを指定します。|
   |/noreplace|セットアップ時にサードパーティのマルウェア対策ソフトウェアをアンインストールしないことを指定します。|
   |/policy|インストール時にマルウェア対策ポリシー ファイルを使用してクライアントを構成することを指定します。|
   |/sqmoptin|このクライアント ソフトウェアのインストールで、マイクロソフトのカスタマー エクスペリエンス向上プログラムに参加することを指定します。|

3.  画面の手順に従ってクライアントのインストールを完了します。

4.  最新の更新定義パッケージをダウンロードしている場合、パッケージをクライアント コンピューターにコピーしてから、定義パッケージをダブルクリックしてインストールします。

   > [!NOTE]
   >  Endpoint Protection クライアントのインストールが完了すると、クライアントで定義の更新チェックが自動的に実行されます。 この更新チェックが成功した場合は、最新の定義更新パッケージを手動でインストールする必要はありません。

## <a name="to-install-the-client-software-with-an-antimalware-policy-from-the-command-prompt"></a>コマンド プロンプトでクライアント ソフトウェアをマルウェア対策ポリシーとともにインストールするには

1.  **scepinstall.exe** およびエクスポートしたマルウェア対策ポリシーまたは事前に構成したマルウェア対策ポリシーを、Endpoint Protection クライアント ソフトウェアをインストールするコンピューターにコピーします。

2.  管理者特権でコマンド プロンプトを開き、 **scepinstall.exe** とマルウェア対策ポリシーが配置されているフォルダーに移動してから、次のコマンドを実行します。

   ```
   scepinstall.exe /policy <full path>\<policy file>
   ```

3.  画面の手順に従ってクライアントのインストールを完了します。

4.  最新の定義パッケージをダウンロードしている場合、パッケージをクライアント コンピューターにコピーしてから、定義パッケージをダブルクリックしてインストールします。

   > [!NOTE]
   >  Endpoint Protection クライアントのインストールが完了すると、クライアントで定義の更新チェックが自動的に実行されます。 この更新チェックが成功した場合は、最新の定義更新パッケージを手動でインストールする必要はありません。

## <a name="verify-that-the-endpoint-protection-client-is-installed-correctly"></a>Endpoint Protection クライアントが正しくインストールされているかどうかの確認
参照コンピューターに Endpoint Protection クライアントをインストールしたら、クライアントが正しく機能していることを確認します。

### <a name="to-verify-that-the-endpoint-protection-client-is-installed-correctly"></a>Endpoint Protection クライアントが正しくインストールされていることを確認するには

1.  参照コンピューターで、Windows 通知領域から **[System Center Endpoint Protection]** を開きます。

2.  **[System Center Endpoint Protection]** ダイアログ ボックスの **[ホーム]** タブで、**[リアルタイム保護]** が **[オン]** に設定されていることを確認します。

3.  **[ウイルス定義およびスパイウェアの定義]** で **[最新]**が表示されていることを確認します。

4.  参照コンピューターのイメージングの準備ができていることを確認するには、[スキャン オプション ****] で [フル ****] を選択してから、[今すぐスキャン ****] をクリックします。

### <a name="how-to-prepare-the-endpoint-protection-client-for-imaging"></a>Endpoint Protection クライアントのイメージングを準備する方法
参照コンピューターに Endpoint Protection クライアントが正しくインストールされていることを確認したら、コンピューターのイメージングを準備できます。 Endpoint Protection クライアントのイメージングを準備するには、次の手順を実行します。


Configuration Manager でのオペレーティング システムの展開の詳細については、「[System Center Configuration Manager でのオペレーティング システム イメージの管理](/sccm/osd/get-started/manage-operating-system-images)」をご覧ください。

### <a name="to-prepare-the-endpoint-protection-client-for-imaging"></a>Endpoint Protection クライアントのイメージングを準備するには

1.  参照コンピューターで、管理者特権を持つユーザーとしてログオンします。

2.  TechNet の **Windows SysInternals サイト** から、 [PsTools](http://go.microsoft.com/fwlink/?LinkId=215263) をダウンロードしてインストールします。

3.  管理者特権でコマンド プロンプトを開き、PsTools をインストールしたフォルダーに移動してから、次のコマンドを入力します。

   ```
   Psexec.exe -s -i regedit.exe
   ```

   > [!IMPORTANT]
   >  レジストリ エディターをこのように実行するときは、慎重に行ってください。PsExec.exe の -s オプションでは、LocalSystem 特権でレジストリ エディターが実行されます。

4.  レジストリ エディターで、次の各レジストリ キーに移動して、これらのキーを削除します。

   > [!IMPORTANT]
   >  レジストリ キーの削除は、参照コンピューターをイメージングする前の最後の手順として行う必要があります。 レジストリ キーは、Endpoint Protection クライアントが開始されると再作成されます。 参照コンピューターを再起動する場合は、レジストリ キーを再度削除する必要があります。

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID**

上記の手順を完了したら、参照コンピューターのイメージングを準備できます。 Configuration Manager でのオペレーティング システムの展開の詳細については、「[System Center Configuration Manager でのオペレーティング システム イメージの管理](/sccm/osd/get-started/manage-operating-system-images)」をご覧ください。

Endpoint Protection クライアント ソフトウェアが含まれたイメージが展開されると、コンピューターが割り当てられている Configuration Manager サイトに Endpoint Protection クライアントから情報が自動的にレポートされて、このクライアント コンピューターに適用可能なポリシーがダウンロードされて適用されます。

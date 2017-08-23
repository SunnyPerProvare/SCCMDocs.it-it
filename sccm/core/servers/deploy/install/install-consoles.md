---
title: "コンソールのインストール | Microsoft Docs"
description: "Configuration Manager コンソールをインストールし、中央管理サイトまたはプライマリ サイトに接続する方法についてご確認ください。"
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d39c201f-d364-4e7b-bde4-faa76d747f33
caps.latest.revision: "3"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 88ecbc48fd03ce988f04408d0378844cbed1de2b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="install-the-system-center-configuration-manager-console"></a>System Center Configuration Manager コンソールをインストールする

*適用対象: System Center Configuration Manager (Current Branch)*

管理者は System Center Configuration Manager コンソールを利用し、Configuration Manager 環境を管理します。 各 Configuration Manager コンソールで中央管理サイトまたはプライマリ サイトに接続できます。 Configuration Manager をセカンダリ サイトに接続することはできません。

> [!NOTE]  
>  コンソールを実行している管理者に対して表示されるオブジェクトは、そのユーザー アカウントに割り当てられているアクセス許可によって変わります。 ロール ベース管理について詳しくは、「[System Center Configuration Manager のロール ベース管理の基礎](../../../../core/understand/fundamentals-of-role-based-administration.md)」を参照してください。  

 セットアップ ウィザードを利用し、サイト サーバーのインストール中に Configuration Manager コンソールをインストールできます。あるいは、セットアップ ウィザードを利用するスタンドアロン インストール アプリケーションを実行できます。  

 スタンドアロンのアプリケーションを使用して Configuration Manager コンソールをインストールするには、次の手順に従います。  

## <a name="to-install-the-configuration-manager-console-by-using-the-setup-wizard"></a>セットアップ ウィザードを使用して Configuration Manager コンソールをインストールするには  

1.  次の要件を満たすことを確認してください。  

    -  コンソールを実行するコンピューターの**ローカル管理者** 権限が与えられていること。  

    -   コンソールのインストール ファイルのある場所の **読み取り** 権限が与えられていること。  

2.  次のいずれかの場所に移動します。  

    -   サイト サーバーで、**<*Configuration Manager サイト サーバーのインストール パス*>\Tools\ConsoleSetup** に移動します。  

    -   Configuration Manager のソース メディアから、**<*Configuration Manager ソース ファイル*>\Smssetup\Bin\I386** に移動します。  

    > [!TIP]  
    >  ベスト プラクティスとして、Configuration Manager コンソールのインストールは、System Center Configuration Manager のインストール メディアではなく、サイト サーバーから開始することをお勧めします。 サイト サーバーからインストールする方法では、Configuration Manager コンソールのインストール ファイル、およびサイト用にサポートされている言語パックが **Tools\ConsoleSetup** サブフォルダーにコピーされます。 インストール メディアから Configuration Manager コンソールをインストールする場合、サイト サーバーでサポートされている言語やコンピューターのオペレーティング システムの言語設定には関係なく、常に英語版がインストールされます。 **ConsoleSetup** フォルダーを別の場所にコピーして、その場所からインストールを開始することもできます。

3.  Configuration Manager コンソールのセットアップ ウィザードを開くには、**consolesetup.exe** をダブルクリックします。  

    > [!IMPORTANT]  
    >  Configuration Manager コンソールのインストールには、常に、consolesetup.exe を使用します。 AdminConsole.msi を実行しても Configuration Manager コンソールをインストールできますが、前提条件や依存関係のチェックは行われず、正しくインストールされない可能性があります。  

4.  ウィザードで、**[次へ]** を選択します。  

5.  **[サイト サーバー]** ページで、Configuration Manager コンソールが接続するサイト サーバーの完全修飾ドメイン名 (FQDN) を入力します。  

6.  **[インストール先フォルダー]** ページで、Configuration Manager コンソールのインストール先フォルダーを入力します。 フォルダーのパスに Unicode 文字を含めたり、末尾にスペースを付けたりすることはできません。  

7.  **[カスタマー エクスペリエンス向上プログラム]** ページで、カスタマー エクスペリエンス向上プログラム (CEIP) に参加するかどうかを選択します。  

8.  **[インストールの準備完了]** ページで、**[インストール]** を選択して Configuration Manager コンソールをインストールします。  

## <a name="to-install-the-configuration-manager-console-from-a-command-prompt"></a>コマンド プロンプトから Configuration Manager コンソールをインストールするには  

1.  Configuration Manager コンソールのインストールを開始するサーバーでコマンド プロンプト ウィンドウを開き、次のいずれかの場所に移動します。  

    -   **<*Configuration Manager サイト サーバーのインストール パス*>\Tools\ConsoleSetup**  

    -   **<*Configuration Manager インストール メディア*>\SMSSETUP\BIN\I386**  

    > [!TIP]  
    >  コマンド プロンプトから Configuration Manager コンソールをインストールすると、コンピューターのオペレーティング システムの言語設定に関係なく、常に英語版がインストールされます。 英語以外の言語で Configuration Manager コンソールをインストールするには、[セットアップ ウィザードを利用して Configuration Manager コンソールをインストールする](#to-install-the-configuration-manager-console-by-using-the-setup-wizard)必要があります。  

2.  コマンド プロンプトで「**consolesetup.exe**」と入力します。 次のコマンド ライン オプションから選択します。  

|  コマンド ライン オプションを使用します     | [説明]     |
  | :------------- | :------------- |
  |/q|Configuration Manager コンソールを無人インストールします。 **EnableSQM**、 **TargetDir**、 **DefaultSiteServerName** の各オプションは、このオプションを使用する場合に指定する必要があります。|  
  |/uninstall|Configuration Manager コンソールをアンインストールします。 **/q** オプションと共に使用する場合は、このオプションを先に指定する必要があります。|  
  |LangPackDir|言語ファイルが含まれているフォルダーのパスを指定します。 **セットアップ ダウンローダー** を使用して言語ファイルをダウンロードできます。 このオプションを指定しないと、現在のフォルダー内で言語フォルダーが検索されます。 言語フォルダーが見つからなかった場合は、英語版だけがインストールされます。 詳細については、「[セットアップ ダウンローダー](setup-downloader.md)」を参照してください。|  
  |TargetDir|Configuration Manager コンソールをインストールするインストール先フォルダーを指定します。 このオプションは、 **/q** オプションを使用する場合に指定する必要があります。|  
  |EnableSQM|カスタマー エクスペリエンス向上プログラム (CEIP) に参加するかどうかを指定します。 値として **1** を指定すると、CEIP に参加します。**0** を指定すると、参加しません。 このオプションは、 **/q** オプションを使用する場合に指定する必要があります。|  
  |DefaultSiteServerName|コンソールを開いたときに接続されるサイト サーバーの FQDN を指定します。 このオプションは、 **/q** オプションを使用する場合に指定する必要があります。|  


  **例:**

  -  **consolesetup.exe /q TargetDir="D:\Program Files\ConfigMgr" EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /q LangPackDir=C:\Downloads\ConfigMgr TargetDir="D:\Program Files\ConfigMgr" Console EnableSQM=1 DefaultSiteServerName=MyServer.Contoso.com**  

  -  **consolesetup.exe /uninstall /q**  

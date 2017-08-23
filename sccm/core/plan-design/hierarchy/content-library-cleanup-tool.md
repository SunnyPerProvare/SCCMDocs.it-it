---
title: "コンテンツ ライブラリ クリーンアップ ツール | Microsoft Docs"
description: "System Center Configuration Manager の展開と関連付けられなくなった孤立コンテンツを削除するには、コンテンツ ライブラリ クリーンアップ ツールを使います。"
ms.custom: na
ms.date: 4/7/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 226cbbb2-9afa-4e2e-a472-be989c0f0e11
caps.latest.revision: "4"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 76e6772bdd5cbd32d525e728f6ebc988b045da78
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="the-content-library-cleanup-tool-for-system-center-configuration-manager"></a>System Center Configuration Manager のコンテンツ ライブラリ クリーンアップ ツール

*適用対象: System Center Configuration Manager (Current Branch)*

 バージョン 1702 以降では、コマンド ライン ツール (**ContentLibraryCleanup.exe**) を使って、どのパッケージまたはアプリケーションにも関連付けられなくなったコンテンツ (孤立コンテンツ) を配布ポイントから削除できます。 このツールはコンテンツ ライブラリ クリーンアップ ツールと呼ばれ、過去の Configuration Manager 製品用にリリースされた同様のツールの古いバージョンに代わるものです。  

このツールでは、ツールを実行するときに指定する配布ポイントのコンテンツのみが処理されます。 このツールで、サイト サーバー上のコンテンツ ライブラリからコンテンツを削除することはできません。

**ContentLibraryCleanup.exe** は、中央管理サイトまたはプライマリ サイトのサイト サーバーの *%CM_Installation_Path%\cd.latest\SMSSETUP\TOOLS\ContentLibraryCleanup\* フォルダーにあります。

## <a name="requirements"></a>［要件］  
 このツールは、一度に 1 つの配布ポイントに対してのみ実行できます。  
 - このツールは、クリーンアップする配布ポイントをホストするコンピューター上で直接実行することも、別のサーバーからリモートで実行することもできます。
 - ツールを実行するユーザー アカウントは、Configuration Manager 階層の完全な権限を持つ管理者と同じロールベース管理アクセス許可を直接持っている必要があります。 完全なアクセス許可を持つ管理者のアクセス許可がある Windows セキュリティ グループのメンバーとしてこれらのアクセス許可を付与される場合、このツールは機能しません。

## <a name="modes-of-operation"></a>操作モード
このツールは、次の 2 つのモードで実行できます。 *What If モード*でツールを実行して結果を確認した後、*削除モード*でツールを実行することをお勧めします。
  1.    **What If モード**:   
      **/delete** スイッチを指定しないと、ツールは What If モードで実行され、配布ポイントから削除されるコンテンツを識別します。
   - このモードでツールを実行した場合、データは削除されません。
   - 削除されるコンテンツに関する情報はツールのログ ファイルに書き込まれ、可能性のある削除ごとにユーザーが確認を求められることはありません。  
      </br>   

  2. **削除モード**:   
    **/delete** スイッチを使ってツールを実行すると、ツールは削除モードで実行されます。

     - このモードでツールを実行すると、指定した配布ポイントで検出された孤立コンテンツを、配布ポイントのコンテンツ ライブラリから削除することができます。
     -  各ファイルを削除する前に、ユーザーはファイルを削除することを確認する必要があります。  削除する場合は [**Y**] を選択し、削除しない場合は [**N**] を選択します。あるいは、[**すべて削除**] を選択すると、以降のメッセージは省略され、孤立したすべてのコンテンツが削除されます。  
     </br>

ツールをどちらのモードで実行しても、自動的にログが作成されます。このログには、ツールの実行モード、配布ポイントの名前、日付、および操作時刻を含んだ名前が付けられます。 ツールが終了すると、ログ ファイルが自動的に開きます。

既定では、ログ ファイルは、ツールが実行されているコンピューターの、ツールを実行しているユーザー アカウントの一時フォルダーに書き込まれます。 **/log** スイッチを使って、ネットワーク共有などの別の場所にログ ファイルをリダイレクトできます。


## <a name="run-the-tool"></a>ツールを実行します。
ツールを実行するには:
1. 管理コマンド プロンプトで、**ContentLibraryCleanup.exe** を含むフォルダーを開きます。  
2. 次に、必須のコマンド ライン スイッチと、使用する省略可能なスイッチを含めたコマンドラインを入力します。

**既知の問題** パッケージまたは展開が失敗した場合、または進行中の場合、ツールを実行すると、次のようなエラーが返される可能性があります。
-  *System.InvalidOperationException: This content library cannot be cleaned up right now because package <packageID> is not fully installed.* (System.InvalidOperationException: パッケージ <パッケージ ID> が完全にインストールされていないため、このコンテンツ ライブラリを今すぐクリーンアップすることはできません。)

**対応策 :** なし。 コンテンツの展開が進行中または失敗した場合、このツールは孤立ファイルを確実に識別することはできません。 したがって、その問題が解決されるまで、ツールではコンテンツのクリーンアップが許可されません。

### <a name="command-line-switches"></a>コマンド ライン スイッチ  
コマンドライン スイッチは、任意の順に使用できます。   

|スイッチ|説明|
|---------|-------|
|**/delete**  |**省略可能** </br> 配布ポイントからコンテンツを削除する場合は、このスイッチを使用します。 コンテンツが削除される前に確認を求めるメッセージが表示されます。 </br></br> このスイッチが使われていない場合、ツールはどのコンテンツが削除対象かについて結果をログに記録しますが、配布ポイントからコンテンツを削除しません。 </br></br> 例: ***ContentLibraryCleanup.exe /dp server1.contoso.com /delete*** |
| **/q**       |**省略可能** </br> このスイッチを指定すると、ツールはすべてのプロンプト (コンテンツを削除する場合のプロンプトなど) を非表示にする Quiet モードで実行し、ログ ファイルは自動的に開かれません。 </br></br> 例: ***ContentLibraryCleanup.exe /q /dp server1.contoso.com*** |
| **/dp &lt;配布ポイント FQDN>**  | **必須** </br> クリーニングする配布ポイントの完全修飾ドメイン名 (FQDN) を指定します。 </br></br> 例: ***ContentLibraryCleanup.exe /dp server1.contoso.com***|
| **/ps &lt;プライマリ サイト FQDN>**       | プライマリ サイトで配布ポイントからコンテンツをクリーニングする場合は**省略可能**。</br>セカンダリ サイトで配布ポイントからコンテンツをクリーニングする場合は**必須**。 </br></br>このツールは、親プライマリ サイトに接続して、SMS_Provider に対するクエリを実行します。 このクエリによって、どのコンテンツを配布ポイントに置くかをツールが決定して、孤立しているコンテンツや削除できるコンテンツを特定できるようになります。 必要な情報がセカンダリ サイトからは直接入手できないため、親プライマリ サイトへのこの接続はセカンダリ サイトの配布ポイントに対して行う必要があります。</br></br> 配布ポイントが属するプライマリ サイトの FQDN を指定します。または、配布ポイントがセカンダリ サイトにある場合は、親であるプライマリ サイトの FQDN を指定します。 </br></br> 例: ***ContentLibraryCleanup.exe /dp server1.contoso.com /ps siteserver1.contoso.com*** |
| **/sc &lt;プライマリ サイト コード>**  | プライマリ サイトで配布ポイントからコンテンツをクリーニングする場合は**省略可能**。</br>セカンダリ サイトで配布ポイントからコンテンツをクリーニングする場合は**必須**。 </br></br> 配布ポイントが属するプライマリ サイトのサイト コードを指定します。あるいは、配布ポイントがセカンダリ サイトにある場合は親であるプライマリ サイトのサイト コードを指定します。</br></br> 例: ***ContentLibraryCleanup.exe /dp server1.contoso.com /sc ABC*** |
| **/log <log file directory>**       |**省略可能** </br> ツールがログ ファイルを書き込む場所を指定します。 ローカル ドライブやネットワーク共有上の場所を指定できます。</br></br> このスイッチを指定しないと、ログ ファイルは、ツールが実行されているコンピューター上のユーザーの一時フォルダーに格納されます。</br></br> ローカル ドライブの例: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log C:\Users\Administrator\Desktop*** </br></br>ネットワーク共有の例: ***ContentLibraryCleanup.exe /dp server1.contoso.com /log \\&lt;share>\&lt;folder>***|

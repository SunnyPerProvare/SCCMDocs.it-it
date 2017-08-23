---
title: "インターネットに接続されていない場合の更新プログラムの同期 - Configuration Manager | Microsoft Docs"
description: "インターネットから切断されている最上位のソフトウェアの更新ポイントでソフトウェア更新プログラムの同期を実行します。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 01/23/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 1a997c30-8e71-4be5-89ee-41efb2c8d199
ms.openlocfilehash: fd9c1e9418ff1956c6ef98753e23a293440179be
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="synchronize-software-updates-from-a-disconnected-software-update-point"></a>切断されているソフトウェアの更新ポイントからのソフトウェア更新プログラムの同期  

*適用対象: System Center Configuration Manager (Current Branch)*

 最上位サイトのソフトウェアの更新ポイントがインターネットから切断されている場合、WSUSUtil ツールのエクスポート機能とインポート機能を使ってソフトウェア更新プログラムのメタデータを同期させる必要があります。 Configuration Manager 階層に含まれていない既存の WSUS サーバーを同期ソースとして選択することができます。 このトピックでは、WSUSUtil ツールのエクスポート機能とインポート機能を使用する方法について説明します。  

 ソフトウェア更新プログラムのメタデータをエクスポートおよびインポートするためには、指定のエクスポート サーバーの WSUS データベースからソフトウェア更新プログラムのメタデータをエクスポートしてから、切断されているソフトウェアの更新ポイントに対して、ローカルに保存したライセンス条項ファイルをコピーし、その後で、切断されているソフトウェアの更新ポイントの WSUS データベースにソフトウェア更新プログラムのメタデータをインポートします。  

 ソフトウェア更新プログラムのメタデータをエクスポートするエクスポート サーバーを判断するときに、次の表を参考にしてください。  

|ソフトウェアの更新ポイント|接続されているソフトウェア更新ポイントのアップストリームの更新ソース|切断されているソフトウェアの更新ポイントのエクスポート サーバー|  
|---------------------------|-----------------------------------------------------------------|------------------------------------------------------------|  
|中央管理サイト|Microsoft Update (インターネット)<br /><br /> 既存の WSUS サーバー|Configuration Manager 環境で必要なソフトウェア更新プログラムの分類、製品、および言語を使用して Microsoft Update と同期される WSUS サーバーを選択します。|  
|スタンドアロン プライマリ サイト|Microsoft Update (インターネット)<br /><br /> 既存の WSUS サーバー|Configuration Manager 環境で必要なソフトウェア更新プログラムの分類、製品、および言語を使用して Microsoft Update と同期される WSUS サーバーを選択します。|  

 最新のソフトウェア更新プログラムのメタデータが同期されるように、エクスポート プロセスを開始する前に、選択したエクスポート サーバーでソフトウェア更新プログラムの同期が完了していることを確認してください。 ソフトウェア更新プログラムの同期が正常に完了したことを確認するには、次の手順を実行します。  

#### <a name="to-verify-that-software-updates-synchronization-has-completed-successfully-on-the-export-server"></a>エクスポート サーバーでソフトウェア更新プログラムの同期が正常に完了したことを確認するには  

1.  WSUS 管理コンソールを開き、エクスポート サーバーの WSUS データベースに接続します。  

2.  WSUS 管理コンソールで、[同期 ****] をクリックします。 試行されたソフトウェア更新プログラムの同期の一覧が結果ウィンドウに表示されます。  

3.  結果ウィンドウで、最新のソフトウェア更新プログラムの同期を見つけ、それが正常に完了していることを確認します。  

> [!IMPORTANT]  
>  ソフトウェア更新プログラムのメタデータをエクスポートするためには、WSUSUtil ツールをエクスポート サーバーでローカルに実行する必要があります。また、ソフトウェア更新プログラムのメタデータをインポートするためには、WSUSUtil ツールを切断されているソフトウェアの更新ポイント サーバーで実行する必要があります。 また、WSUSUtil ツールを実行するユーザーは、各サーバーのローカル Administrators グループのメンバーである必要があります。  

## <a name="export-process-for-software-updates"></a>ソフトウェア更新プログラムのエクスポート プロセス  
 ソフトウェア更新プログラムのエクスポート プロセスは、主に 2 つの手順で構成されます。1 つは、ローカルに保存されているライセンス条項ファイルを、切断されているソフトウェアの更新ポイントにコピーする手順で、もう 1 つは、ソフトウェア更新プログラムのメタデータをエクスポート サーバーの WSUS データベースからエクスポートする手順です。  

 ローカルに保存されているライセンス条項メタデータを、切断されているソフトウェアの更新ポイントにコピーするには、次の手順に従います。  

#### <a name="to-copy-local-files-from-the-export-server-to-the-disconnected-software-update-point-server"></a>切断されているソフトウェアの更新ポイント サーバーにエクスポート サーバーからローカル ファイルをコピーするには  

1.  エクスポート サーバーで、ソフトウェアの更新、およびソフトウェアの更新のライセンス条項が保存されているフォルダーに移動します。 既定では、WSUS サーバーによって、このファイルは<*WSUSInstallationDrive*>\WSUS\WSUSContent\\ に保存されています。ここで、*WSUSInstallationDrive* は、WSUS がインストールされているドライブです。  

2.  この場所のすべてのファイルおよびフォルダーをソフトウェアの更新ポイント サーバーの WSUSContent フォルダーにコピーします。  

 ソフトウェア更新プログラムのメタデータをエクスポート サーバーの WSUS データベースからエクスポートするには、次の手順に従います。  

#### <a name="to-export-software-updates-metadata-from-the-wsus-database-on-the-export-server"></a>ソフトウェア更新プログラムのメタデータをエクスポート サーバーの WSUS データベースからエクスポートするには  

1.  エクスポート サーバーのコマンド プロンプトで、WSUSutil.exe を含むフォルダーに移動します。 既定では、このツールは %*ProgramFiles*%\Update Services\Tools にあります。 たとえば、ツールが既定の場所にある場合は、 **cd %ProgramFiles%\Update Services\Tools**のように入力します。  

2.  次のように指定して、ソフトウェア更新プログラムのメタデータをパッケージ ファイルにエクスポートします。  

     **wsusutil.exe export**  *packagename*  *logfile*  

     たとえば、  

     **wsusutil.exe export export.cab export.log**  

     この書式をまとめると、WSUSutil.exe、export オプション、エクスポート操作中に作成されるエクスポート .cab ファイルの名前、ログ ファイルの名前の順になります。 WSUSutil.exe により、エクスポート サーバーからメタデータがエクスポートされ、操作のログ ファイルが作成されます。  

    > [!NOTE]  
    >  パッケージ (.cab ファイル) 名およびログ ファイル名は、現在のフォルダー内で一意である必要があります。  

3.  インポート WSUS サーバーで WSUSutil.exe を含むフォルダーにエクスポート パッケージを移動します。  

    > [!NOTE]  
    >  このフォルダーにパッケージを移動すると、インポート操作が簡単になります。 インポート サーバーにアクセスできる任意の場所にパッケージを移動し、WSUSutil.exe の実行時にその場所を指定できます。  

## <a name="import-software-updates-metadata"></a>ソフトウェア更新プログラムのメタデータのインポート  
 切断されているソフトウェアの更新ポイントにソフトウェア更新プログラムのメタデータをエクスポート サーバーからインポートするには、次の手順に従います。  

> [!IMPORTANT]  
>  信頼していないソースからエクスポートされたデータをインポートしないでください。 信頼していないソースのコンテンツをインポートすると、WSUS サーバーのセキュリティが低下する可能性があります。  

#### <a name="to-import-metadata-to-the-database-of-the-import-server"></a>インポート サーバーのデータベースにメタデータをインポートするには  

1.  インポート WSUS サーバーのコマンド プロンプトで、WSUSutil.exe を含むフォルダーに移動します。 既定では、このツールは %*ProgramFiles*%\Update Services\Tools にあります。  

2.  次のように入力します。  

     **wsusutil.exe import**  *packagename*  *logfile*  

     たとえば、  

     **wsusutil.exe import export.cab import.log**  

     この書式をまとめると、WSUSutil.exe、import コマンド、エクスポート操作中に作成されたパッケージ ファイル (.cab) の名前 (他のフォルダーに存在する場合はパッケージ ファイルのパス)、ログ ファイルの名前の順になります。 WSUSutil.exe により、エクスポート サーバーからメタデータがインポートされ、操作のログ ファイルが作成されます。  

## <a name="next-steps"></a>次のステップ
最初にソフトウェア更新プログラムを同期した後、または使用可能な新しい分類または製品があったら、[新しい分類と製品を構成](configure-classifications-and-products.md)して、新しい条件のソフトウェア更新プログラムを同期します。

必要な条件でソフトウェア更新プログラムを同期した後、[ソフトウェア更新プログラムの設定を管理します](manage-settings-for-software-updates.md)。  

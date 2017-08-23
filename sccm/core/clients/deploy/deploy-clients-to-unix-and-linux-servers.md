---
title: "UNIX または Linux クライアントの展開 | Microsoft Docs"
description: "System Center Configuration Manager で UNIX または Linux サーバーにクライアントを展開する方法を説明します。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 15a4e323-9f42-4fea-bb14-f2b905d1f77c
caps.latest.revision: "9"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d61d53daa5ef3d9c986cba8791d4471fea94d29d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-deploy-clients-to-unix-and-linux-servers-in-system-center-configuration-manager"></a>System Center Configuration Manager で UNIX および Linux サーバーにクライアントを展開する方法

*適用対象: System Center Configuration Manager (Current Branch)*

Linux または UNIX サーバーを System Center Configuration Manager で管理するには、その前に各 Linux または UNIX サーバー上に Linux および UNIX 用の構成マネージャー クライアントをインストールする必要があります。 各コンピューターでクライアントのインストールを手動で実行することも、シェル スクリプトを使用してクライアントをリモートでインストールすることもできます。 Configuration Manager では、Linux または UNIX サーバーのクライアント プッシュ インストールを使用することはできません。 必要に応じて、Linux または UNIX サーバーへのクライアントのインストールを自動化するように System Center Orchestrator の Runbook を構成することができます。  

 使用するインストール方法に関わりなく、インストール プロセスでは、インストール プロセスを管理するために **install** という名前のスクリプトを使用する必要があります。 このスクリプトは、Linux および UNIX 用クライアントをダウンロードするときに含まれます。  

 Linux および UNIX 用の構成マネージャー クライアントのインストール スクリプトは、コマンド ライン プロパティをサポートしています。 いくつかのコマンド ライン プロパティは、他のユーザーは省略可能な必要です。 たとえば、クライアントをインストールするときに、サイトとその初期の連絡先の Linux または UNIX サーバーで使用するサイトの管理ポイントを指定する必要があります。 コマンド ライン プロパティの完全な一覧については、「 [Linux サーバーおよび UNIX サーバーにクライアントをインストールするためのコマンド ライン プロパティ](#BKMK_CmdLineInstallLnUClient)」を参照してください。  

 クライアントをインストールした後、Configuration Manager コンソールでクライアント設定を指定して、Windows ベースのクライアントと同じ方法でクライアント エージェントを構成します。 詳細については、「  [Client settings for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ClientSettingsforLnU)」をご覧ください。  

##  <a name="BKMK_AboutInstallPackages"></a> クライアント インストール パッケージと Universal Agent について  
 特定のプラットフォーム上に Linux および UNIX 用クライアントをインストールするには、クライアントをインストールするコンピューターに適したクライアント インストール パッケージを使用する必要があります。 適切なクライアント インストール パッケージは、 [Microsoft ダウンロード センター](http://go.microsoft.com/fwlink/?LinkID=525184)から各クライアントにダウンロードされるデータの一部として含まれています。 クライアント インストール パッケージに加え、クライアント ダウンロードには、各コンピューター上でクライアントのインストールを管理する **install** スクリプトも含まれています。  

 クライアントをインストールする場合は、使用するクライアント インストール パッケージに関係なく同じプロセスとコマンド ライン プロパティを使用できます。  

 Linux および UNIX 用の構成マネージャー クライアントの各リリースでサポートされるオペレーティング システム、プラットフォーム、およびクライアント インストール パッケージの詳細については、「[Linux and UNIX servers](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#linux-and-unix-servers)」 (Linux および UNIX サーバー) をご覧ください。  

##  <a name="BKMK_InstallLnUClient"></a> Linux および UNIX サーバーにクライアントをインストールします。  
 Linux および UNIX 用クライアントをインストールするには、各 Linux または UNIX コンピューターでスクリプトを実行します。 スクリプトの名前は **インストール** コマンド ライン プロパティをインストールの動作を変更して、クライアント インストール パッケージの参照をサポートしています。 クライアントには、インストール スクリプトとクライアントのインストール パッケージを配置する必要があります。 クライアント インストール パッケージには、特定の Linux または UNIX オペレーティング システムおよびプラットフォーム用の構成マネージャー クライアント ファイルが含まれています。
各クライアント インストール パッケージでは、クライアントのインストールを完了に必要なすべてのファイルが含まれていて、Windows ベースのコンピューターとは異なりがダウンロードしない追加のファイル、管理ポイントまたはその他のソースの場所からします。  

 Linux および UNIX 用の構成マネージャー クライアントをインストールした後、コンピューターを再起動する必要はありません。 ソフトウェアのインストールが完了するとすぐには、クライアントが動作します。 コンピューターを再起動すると、構成マネージャー クライアントは自動的に再起動します。  

 インストール済みのクライアントは、ルート資格情報を実行します。 ルート資格情報は、ハードウェア インベントリを収集し、ソフトウェアの展開を行うために必要です。  

 次にコマンドの形式を示します。  

 **./install -mp &lt;computer\> -sitecode &lt;sitecode\> &lt;property #1> &lt;property #2> &lt;client installation package\>**  

-   **インストール** Linux および UNIX 用クライアントをインストールするスクリプト ファイルの名前を指定します。 このファイルには、クライアント ソフトウェアが付属しています。  

-   **-mp &lt;computer** には、クライアントによって使用される最初の管理ポイントを指定します。  

     例: smsmp.contoso.com  

-   **-sitecode &lt;site code\>** には、クライアントが割り当てられているサイト コードを指定します。  

     例: S01  

-   &lt;property #1> &lt;property #2> には、インストール スクリプトに使用するコマンド ライン プロパティを指定します。  

    > [!NOTE]  
    >  詳細については、「 [Linux サーバーおよび UNIX サーバーにクライアントをインストールするためのコマンド ライン プロパティ](#BKMK_CmdLineInstallLnUClient)  

-   **client installation package** は、このコンピューターのオペレーティング システム、バージョン、CPU アーキテクチャのクライアント インストール .tar パッケージの名前を指定します。 最後に、クライアント インストールの .tar ファイルを指定する必要があります。  

     例: ccm-Universal-x64.&lt;build\>.tar  

###  <a name="BKMK_ToInstallLnUClinent"></a> Linux および UNIX サーバーに Configuration Manager クライアントをインストールするには  

1.  Windows コンピューターで、管理する [Linux または UNIX サーバーの適切なクライアント ファイルをダウンロードします](http://go.microsoft.com/fwlink/?LinkID=525184) 。  

2.  Windows コンピューターで自己解凍型の .exe ファイルを実行して、インストール スクリプトとクライアントのインストール .tar ファイルを抽出します。  

3.  **インストール** スクリプトおよび .tar ファイルを管理するサーバー上のフォルダーにコピーします。  

4.  UNIX または Linux サーバーで次のコマンドを実行し、スクリプトをプログラムとして実行できるようにします。 **chmod +x install**  

    > [!IMPORTANT]  
    >  ルート資格情報を使用すると、クライアントをインストールするのに必要があります。  

5.  次のコマンドを実行して、構成マネージャー クライアントをインストールします: **./install -mp &lt;hostname\> -sitecode &lt;code\> ccm-Universal-x64.&lt;build\>.tar**  

     このコマンドを入力する場合は、必要なその他のコマンド ライン プロパティを使用します。  コマンド ライン プロパティの一覧については、「 [Linux サーバーおよび UNIX サーバーにクライアントをインストールするためのコマンド ライン プロパティ](#BKMK_CmdLineInstallLnUClient)」を参照してください。  

6.  スクリプトを実行した後は、 **/var/opt/microsoft/scxcm.log** ファイルを確認することで、インストールを検証します。 さらに、Configuration Manager コンソールの **[資産とコンプライアンス]** ワークスペースの **[デバイス]** ノードでクライアントの詳細を表示することによって、クライアントがインストールされ、サイトと通信していることを確認できます。  

###  <a name="BKMK_CmdLineInstallLnUClient"></a> Linux サーバーおよび UNIX サーバーにクライアントをインストールするためのコマンド ライン プロパティ  
 次のプロパティを使って、インストール スクリプトの動作を変更することができます。  

> [!NOTE]  
>  プロパティを使用して **-h** のサポートされているプロパティには、この一覧を表示します。  

-   **-mp &lt;server FQDN\>**  

     必須。 クライアントは、最初の接続ポイントとして使用する管理ポイント サーバーの FQDN を指定します。  

    > [!IMPORTANT]  
    >  このプロパティは、インストール後にクライアントが割り当てられる管理ポイントは指定しません。  

    > [!NOTE]  
    >  **-mp** プロパティを使用して HTTPS クライアント接続のみを受け入れるように構成された管理ポイントを指定する場合、 **-UsePKICert** プロパティも使用する必要があります。  

-   **-sitecode &lt;sitecode\>**  

     必須。 構成マネージャー クライアントを割り当てる Configuration Manager プライマリ サイトを指定します。  

     例: - sitecode S01  

-   **-fsp &lt;server_FQDN>**  

     任意。 状態メッセージを送信するクライアントが使用するフォールバック ステータス ポイント サーバーの FQDN を指定します。  

     フォールバック ステータス ポイントの詳細については、「 [Determine Whether You Require a Fallback Status Point](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients#determine-if-you-need-a-fallback-status-point) 」を参照してください。  


-   **-dir &lt;directory\>**  

     任意。 構成マネージャー クライアント ファイルをインストールする別の場所を指定します。  

     既定では、クライアントは、次の場所にインストールされます。: **/opt/microsoft**です。  

-   **-nostart**  

     任意。 クライアントのインストールが完了した後、構成マネージャー クライアント サービス (**ccmexec.bin**) が自動的に起動しないようにします。  

     クライアントのインストール後に、クライアント サービスを手動で開始する必要があります。  

     既定では、クライアント サービスは、クライアントのインストールが完了すると、し、毎回、コンピューターの再起動した後を開始します。  

-   **-クリーン**  

     任意。 新規インストールを開始する前に、Linux および UNIX では、すべてのクライアントのファイルと、以前にインストールしたクライアントからのデータの削除を指定します。 これにより、クライアントのデータベースと証明書ストアが削除されます。  

-   **-keepdb**  

     任意。 クライアントのローカル データベースが保持され、クライアントを再インストールするときに再利用されることを指定します。 既定では、クライアントを再インストールすると、このデータベースが削除されます。  

-   **-UsePKICert &lt;parameter\>**  

     任意。 公開キーの証明書標準 (PKCS #12) 形式では、X.509 の PKI 証明書に完全なパスとファイル名を指定します。 この証明書は、クライアント認証に使用されます。 証明書がインストール時に指定されていない場合、また証明書を追加または変更する必要がある場合、 **certutil** ユーティリティを使用します。 certutil については、「 [How to manage certificates on the client for Linux and UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts) 」を参照してください。  

     **-UsePKICert**を使用する場合は、 **-certpw** コマンド ライン パラメーターを使って、PKCS#12 ファイルに関連付けられているパスワードも指定する必要があります。  

     PKI 証明書を指定するのにはこのプロパティを使用しない場合、クライアントは自己署名証明書を使用し、サイト システムへのすべての通信は、HTTP 経由ではします。  

     無効な証明書を指定する場合は、コマンドラインのインストール、クライアント、エラーは返されません。 これは、クライアントのインストール後に証明書の検証が行われるためです。 クライアントを起動し、証明書の管理ポイントと検証されに証明書の検証に失敗した場合、次のメッセージが表示されます **scxcm.log**, 、Unix および Linux の Configuration Manager クライアントのログ ファイル。 **管理ポイントの証明書の検証に失敗した**です。 既定のログ ファイルの場所は、  **/var/opt/microsoft/scxcm.log**です。  

    > [!NOTE]  
    >  クライアントをインストールし、 **-mp** プロパティを使用して HTTPS クライアント接続のみを許可するように構成された管理ポイントを指定する場合は、このプロパティを指定する必要があります。  

     例: -UsePKICert &lt;Full path and filename\> -certpw &lt;password\>  

-   **-certpw &lt;parameter\>**  

     任意。 使用して、指定した PKCS #12 ファイルに関連付けられたパスワードを示す、 **- UsePKICert** プロパティです。  

     例: -UsePKICert &lt;Full path and filename\> -certpw &lt;password\>  

-   **-NoCRLCheck**  

     任意。 エントリの PKI 証明書を使用して HTTPS 経由で通信するとき、クライアントが証明書失効リスト (CRL) が確認されませんを指定します。 このオプションが指定されていない場合、クライアントは PKI 証明書を使用して、HTTPS 接続を確立する前に、CRL を確認します。 詳細については、クライアントの CRL チェック、PKI 証明書失効の計画を参照してください。  

     例: -UsePKICert &lt;Full path and filename\> -certpw &lt;password\> -NoCRLCheck  

-   **-rootkeypath &lt;file location\>**  

     任意。 Configuration Manager の信頼されたルート キーへの完全パスとファイル名を指定します。 Configuration Manager の信頼されたルート キーは、適切な階層に属しているサイト システムに接続されていることを確認するために Linux および UNIX クライアントが使用するメカニズムを提供します。  

     コマンド ラインで信頼されたルート キーを指定しない場合、クライアントは、通信する最初の管理ポイントを信頼し、その管理ポイントから信頼されたルート キーを自動的に取得します。  

     詳細については、「  [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK)」を参照してください。  

     例: -rootkeypath &lt;Full path and filename\>  

-   **-httpport &lt;port\>**  

     任意。 クライアントが HTTP 経由で、管理ポイントと通信する際に使用する管理ポイントに構成されているポートを指定します。 ポートが指定されていない場合は、80 の既定の値が使用されます。  

     例: -httpport 80  

-   **-httpsport &lt;port\>**  

     任意。 クライアントが HTTPS 経由で、管理ポイントと通信する際に使用する管理ポイントに構成されているポートを指定します。 ポートが指定されていない場合は、443 の既定の値が使用されます。  

     例: -UsePKICert &lt;Full path and certificate name\> -httpsport 443  

-   **-ignoreSHA256validation**  

     任意。 クライアントのインストールで sha-256 検証をスキップすることを指定します。 SHA-256 をサポートする OpenSSL のバージョンがリリースされていないオペレーティング システムにクライアントをインストールする場合に、このオプションを使用します。 詳細については、「 [About Linux and UNIX Operating Systems That do not Support SHA-256](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256)」をご覧ください。  

-   **-signcertpath &lt;file location\>**  

     任意。 完全パスを指定し、 **.cer** サイト サーバーにエクスポートされた自己署名証明書のファイル名。 PKI 証明書を使用できない場合、Configuration Manager サイト サーバーは自己署名証明書を自動的に生成します。  

     これらの証明書を使用して、目的のサイトから管理ポイントからダウンロードするクライアント ポリシーが送信されたことを検証します。 自己署名証明書がインストール時に指定されていない場合、また証明書を変更する必要がある場合、 **certutil** ユーティリティを使用します。 certutil については、「 [How to manage certificates on the client for Linux and UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts) 」を参照してください。  

     この証明書は、 **SMS** 証明書ストアから取得することができます。サブジェクト名は **Site Server** 、フレンドリ名は **Site Server Signing Certificate**です。  

     インストール時に、このオプションが指定されていない、Linux および UNIX クライアントは最初の管理ポイントと通信し、その管理ポイントから、署名証明書を自動的に取得するを信頼します。  

     例: -signcertpath &lt;Full path and file name\>  

-   **-rootcerts**  

     任意。 追加される PKI 証明書をインポートする管理ポイントの証明機関 (CA) 階層の一部ではないを指定します。 コマンドラインで複数の証明書を指定する場合は、コンマ区切りがあります。  

     サイト管理ポイントによって信頼されているルート CA 証明書にチェーンされない PKI クライアントの証明書を使用する場合は、このオプションを使用します。 クライアント証明書がサイトの証明書発行者リストの信頼されたルート証明書にチェーンされていない場合、管理ポイントはそのクライアントを拒否します。  

     Linux および UNIX クライアントが信頼関係の階層内の証明書のみを使用してのことを確認はこのオプションを使用しない場合、 **- UsePKICert** オプション。  

     例: -rootcerts &lt;Full path and file name\>,&lt;Full path and file name\>  

###  <a name="BKMK_UninstallLnUClient"></a> Linux および UNIX サーバーからクライアントをアンインストールする  
 Linux および UNIX 用の構成マネージャー クライアントをアンインストールするには、アンインストール ユーティリティ **uninstall** を使用します。 既定では、このファイルにある、 **/選択/microsoft/configmgr/bin/** 、クライアント コンピューター上のフォルダーです。 これはアンインストール コマンドは、コマンド ライン パラメーターのサポートし、サーバーからクライアント ソフトウェアに関連するすべてのファイルが削除されます。  

 クライアントをアンインストールするには、次のコマンドラインを使用します **/opt/microsoft/configmgr/bin/uninstall**。  

 Linux および UNIX 用の構成マネージャー クライアントをアンインストールした後、コンピューターを再起動する必要はありません。  

##  <a name="BKMK_ConfigLnUClientCommuincations"></a> Linux および UNIX 用のクライアントの要求ポートを構成します。  
 Windows ベースのクライアントと同様に、Linux および UNIX 用の構成マネージャー クライアントは、HTTP および HTTPS を使用して Configuration Manager サイト システムと通信します。 構成マネージャー クライアントが通信に使用するポートは、要求ポートと呼ばれます。  

 Linux および UNIX 用の構成マネージャー クライアントをインストールするときに、**-httpport** および **-httpsport** インストール プロパティを指定することによって、クライアントの既定の要求ポートを変更することができます。 インストールのプロパティとカスタムの値を指定しなかった場合、クライアントは、既定値を使用します。 既定値は **80** HTTP トラフィック用と **443** HTTPS トラフィック用です。  

 クライアントをインストールした後の要求ポートの構成を変更することはできません。 代わりに、ポートの構成を変更するには、クライアントを再インストールし、新しいポートの構成を指定する必要があります。 要求のポート番号を変更するクライアントを再インストールするときに、実行、 **インストール** 、新しいクライアント インストールの場合のようなコマンドしますが、の追加のコマンド ライン プロパティを使用して **- keepdb**です。 このスイッチは、クライアント データベースおよびクライアントの GUID と証明書ストアを含むファイルを保持するインストールを指示します。  

 クライアント通信のポート番号の詳細については、「[System Center Configuration Manager でのクライアント通信ポートの構成方法](../../../core/clients/deploy/configure-client-communication-ports.md)」を参照してください。  

##  <a name="BKMK_ConfigClientMP"></a> 管理ポイントを探すには、Linux および UNIX 用クライアントを構成します。  
 Linux および UNIX 用の構成マネージャー クライアントをインストールする場合、最初の接続ポイントとして使用する管理ポイントを指定する必要があります。  

 Linux および UNIX 用の構成マネージャー クライアントは、クライアントのインストール時にこの管理ポイントに接続します。 クライアントによる管理ポイントへの接続が失敗した場合、クライアント ソフトウェアは成功するまで試行し続けます。  

 クライアントが管理ポイントを検出する方法の詳細については、「 [Locating Management Points](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points)」を参照してください。

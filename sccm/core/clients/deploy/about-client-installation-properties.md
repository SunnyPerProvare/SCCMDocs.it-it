---
title: "クライアントのインストール プロパティ | Microsoft Docs"
description: "System Center Configuration Manager のクライアント インストール プロパティについて説明します。"
ms.custom: na
ms.date: 01/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
caps.latest.revision: "15"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 36bcbbca4fdee3e95d293c436a105a41a6e3953e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="about-client-installation-properties-in-system-center-configuration-manager"></a>System Center Configuration Manager のクライアント インストール プロパティについて

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager CCMSetup.exe コマンドを使用して、Configuration Manager クライアントを手動でインストールします。  

##  <a name="aboutCCMSetup"></a> CCMSetup.exe について  
 CCMSetup.exe コマンドは、クライアントのインストールに必要なファイルを管理ポイントまたはソースの場所からダウンロードします。 次のようなファイルが含まれます。  

-   クライアント ソフトウェアをインストールする Windows インストーラー パッケージ Client.msi。  

-   Microsoft バックグラウンド インテリジェント転送サービス (BITS) インストール ファイル。  

-   Windows インストーラー インストール ファイル。  

-   Configuration Manager クライアントの更新プログラムまたは修正プログラム。  

> [!NOTE]  
>  Configuration Manager では、Client.msi ファイルを直接実行することはできません。  

 CCMSetup.exe には、インストールをカスタマイズするための[コマンド ライン プロパティ](#ccmsetup-exe-command-line-properties)が用意されています。 CCMSetup.exe コマンド ラインで Client.msi の動作を変更するプロパティを指定することもできます。  

> [!IMPORTANT]  
>  Client.msi のプロパティを指定する前に、CCMSetup のプロパティを指定します。  

 CCMSetup.exe およびそのサポート ファイルは、Configuration Manager サイト サーバーの Configuration Manager インストール フォルダーの **[クライアント]** フォルダーにあります。 このフォルダーは **&lt;サイト サーバー名\>\SMS_&lt;サイト コード\>\Client** としてネットワークで共有されます。  

 コマンド プロンプトで、CCMSetup.exe コマンドは次の形式を使用します。  

 `CCMSetup.exe [<Ccmsetup properties>] [<client.msi setup properties>]`  

 例:  

 'CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

 この例では次が実行されます。  

-   配布ポイントの一覧を要求し、クライアント インストール ファイルをダウンロードするために SMSMP01 という名前の管理ポイントを指定します。  

-   クライアントのバージョンが既にコンピューターに存在している場合にインストールを停止するように指定します。  

-   クライアントをサイト コード S01 に割り当てるように client.msi で指定します。  

-   SMSFP01 というフォールバック ステータス ポイントを使用するように client.msi で指定します。  

> [!NOTE]  
>  プロパティにスペースを含める場合は、引用符で囲みます。  


> [!IMPORTANT]  
>  Configuration Manager 用に Active Directory スキーマを拡張した場合は、多くのクライアント インストール プロパティが Active Directory Domain Services に発行され、Configuration Manager クライアントによって自動的に読み取られます。 Active Directory ドメイン サービスに発行されるクライアント インストールのプロパティの一覧は、「 [System Center Configuration Manager で Active Directory ドメイン サービスに発行されたクライアント インストールのプロパティについて](about-client-installation-properties-published-to-active-directory-domain-services.md)」を参照してください。  

##  <a name="ccmsetupexe-command-line-properties"></a>CCMSetup.exe のコマンド ライン プロパティ  

### <a name=""></a>/?  

CCMSetup.exe のコマンド ライン プロパティを表示する **[CCMSetup]** のダイアログ ボックスを開きます。  

例: **ccmsetup.exe /?**  

### <a name="sourceltpath"></a>/source:&lt;パス\>  

 ファイルのダウンロード場所を指定します。 ローカルまたは UNC パスを使用します。 ファイルはサーバー メッセージ ブロック (SMB) プロトコルを使用してダウンロードされます。  **/source** を使用するには、クライアント インストール用の Windows ユーザー アカウントに、その場所に対する読み取りアクセス許可が必要です。

> [!NOTE]  
>  コマンド ラインで **/source** プロパティを複数回使用して、ダウンロードの代替場所を指定することができます。  

 例: **ccmsetup.exe /source:"\\\computer\folder"**  

### <a name="mpltcomputer"></a>/mp:&lt;コンピューター\>

 インストール ファイルの最も近い配布ポイントを探せるように、コンピューターが接続するソース管理ポイントを指定します。 配布ポイントがない、またはコンピューターが 4 時間経っても配布ポイントからファイルをダウンロードできない場合は、クライアントは指定された管理ポイントからファイルをダウンロードします。  

> [!IMPORTANT]  
>  このプロパティは、ダウンロード ソースを見つけるためのコンピューターの最初の管理ポイントを指定するために使用され、任意のサイト内の任意の管理ポイントを指定できます。 クライアントを管理ポイントに*割り当てる*ことはありません。   

 クライアント接続におけるサイト システムの役割の構成によって、コンピューターは HTTP または HTTPS 接続でファイルをダウンロードします。 BITS スロットルが構成されている場合は、ダウンロードで使用されます。 すべての配布ポイントおよび管理ポイントが HTTPS クライアント接続のみに構成されている場合は、クライアント コンピューターに有効なクライアント証明書があることを確認します。  

**/mp** コマンドライン プロパティを使用すると、複数の管理ポイントを指定し、コンピューターが接続に失敗しても、次の管理ポイントを試すように構成できます。 複数の管理ポイントは、値をセミコロンで区切って指定します。

クライアントが HTTPS を使用して管理ポイントに接続する場合、通常はコンピューター名ではなく FQDN を指定する必要があります。 値は、管理ポイントの PKI 証明書のサブジェクトまたはサブジェクトの別名と一致している必要があります。 Configuration Manager は、証明書のコンピューター名を使用してイントラネットでの接続をサポートしますが、セキュリティのベスト プラクティスとして、FQDN が推奨されます。

コンピューター名を使用する場合の例: `ccmsetup.exe /mp:SMSMP01`  

FQDN を使用する場合の例: `ccmsetup.exe /mp:smsmp01.contoso.com`  

### <a name="retryltminutes"></a>/retry:&lt;分\>

CCMSetup.exe がインストール ファイルのダウンロードに失敗した場合の再試行間隔です。  CCMSetup は、**downloadtimeout** プロパティで指定された制限に達するまで再試行し続けます。  

例: `ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

CCMSetup がサービスとして実行 (既定) されるのを防ぎます。 CCMSetup がサービスとして実行されると、コンピューターのローカル システム アカウントとの関連で実行されます。ローカル システム アカウントには、インストールに必要なネットワーク リソースにアクセスする十分な権利がない場合があります。 **/noservice** を使用すると、CCMSetup.exe は、インストールを開始するために使用するユーザー アカウントの関連で実行されます。 また、スクリプトを使用して、**/service** プロパティで CCMSetup.exe を実行すると、CCMSetup.exe はサービスが開始されると終了し、インストールの詳細を正しくレポートしないことがあります。   

例: `ccmsetup.exe /noservice`  

### <a name="service"></a>/service

CCMSetup がローカル システム アカウントを使用してサービスとして実行されることを指定します。  

例: `ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

クライアント ソフトウェアをアンインストールすることを指定します。 詳細については、「 [How to manage clients in System Center Configuration Manager](../manage/manage-clients.md)」をご覧ください。  

例: `ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

クライアントの任意のバージョンが既にインストールされている場合にクライアント インストールを停止するように指定します。  

例: `ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

 インストールを完了するためにクライアント コンピューターの再起動が必要な場合に、CCMSetup でクライアント コンピューターを強制的に再起動することを指定します。 これが指定されていないと、CCMSetup は再起動が必要なときに終了し、次回手動で再起動した後に続行します。  

 例: `CCMSetup.exe /forcereboot`  

### <a name="bitspriorityltpriority"></a>/BITSPriority:&lt;優先順位\>

 クライアント インストール ファイルが HTTP 接続を介してダウンロードされるときのダウンロードの優先順位を指定します。 使用できる値は次のとおりです。  

-   FOREGROUND  

-   HIGH  

-   NORMAL  

-   LOW  

 既定値は NORMAL です。  

 例: `ccmsetup.exe /BITSPriority:HIGH`  

### <a name="downloadtimeoutltminutes"></a>/downloadtimeout:&lt;分\>

CCMSetup がインストール ファイルのダウンロードの試行を開始してから停止するまでの時間 (分単位) です。 既定値は **1440** 分 (1 日) です。  

例: `ccmsetup.exe /downloadtimeout:100`  

### <a name="usepkicert"></a>/UsePKICert

 指定されるとクライアントは、利用可能であれば、クライアントの認証を含んだ PKI 証明書を使用します。 有効な証明書が見つからない場合、クライアントは、HTTP 接続と自己署名証明書を使用します。これはこのプロパティを使用しない場合の動作でもあります。

> [!NOTE]  
>  クライアントをインストールし、クライアントの証明書を引き続き使用する場合には、このプロパティを指定する必要はありません。 これらのシナリオには、クライアント プッシュおよびソフトウェアの更新ポイント ベースを使用したクライアントのインストールが含まれます。 しかし、手動でクライアントをインストールするときは、このプロパティを指定し、 **/mp** プロパティを使用して HTTPS クライアント接続のみを許可するように構成された管理ポイントを指定する必要があります。 また、インターネット通信のみのクライアントをインストールする場合も、(インターネットベースの管理ポイントおよびサイト コードと共に) CCMALWAYSINF=1 プロパティを使って、このプロパティを指定する必要があります。 インターネット ベースのクライアント管理の詳細については、「[System Center Configuration Manager でのエンドポイント間の通信](../../plan-design/hierarchy/communications-between-endpoints.md)」の「[インターネットや信頼されていないフォレストからのクライアント通信に関する考慮事項](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)」を参照してください。  

 例: `CCMSetup.exe /UsePKICert`  

### <a name="nocrlcheck"></a>/NoCRLCheck

 PKI 証明書を使用して HTTPS で通信するときは、クライアントが証明書失効リスト (CRL) を確認しないように指定します。  

 指定しない場合、クライアントは HTTPS 接続を確立する前に CRL を確認します。  

 クライアントの CRL チェックの詳細については、「 [Plan for Security 」 の「 System Center Configuration Manager](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs) 」 の「[Plan for security 」 の「 System Center Configuration Manager](../../plan-design/security/plan-for-security.md)」を参照してください。  

 例: `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="configltconfiguration-file"></a>/config:&lt;構成ファイル\>

クライアント インストールのプロパティを含むテキスト ファイルの名前を指定します。

- **/noservice** CCMSetup プロパティを指定しない場合、このファイルは CCMSetup フォルダーに置く必要があります。このフォルダーは、32 ビット版と 64 ビット版のいずれのオペレーティング システムでも %Windir%\\Ccmsetup にあります。
- **/noservice** プロパティを指定する場合、このファイルは CCMSetup.exe を実行するフォルダーと同じフォルダーに存在する必要があります。  

例: `CCMSetup.exe /config:&lt;Configuration File Name.txt\>`  

サイト サーバー コンピューターの &lt;Configuration Manager ディレクトリ\>\\bin\\&lt;プラットフォーム\> フォルダーにある mobileclienttemplate.tcf ファイルを使用して、正しいファイル形式を提供します。 このファイルには、セクションに関するコメントと、その使用方法に関する情報も含まれています。 **Install=INSTALL=ALL**というテキストに続く [Client Install] セクションに、クライアント インストールのプロパティを指定します。  

[Client Install] セクション エントリの例: `Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereqltfilename"></a>/skipprereq:&lt;ファイル名\>

 Configuration Manager クライアントがインストールされた場合は、指定した前提条件のプログラムを CCMSetup.exe がインストールしないように指定します。 このプロパティは複数値の入力をサポートします。 個々の値を区切るには、セミコロン文字 (;) を使用します。  


 例: `CCMSetup.exe /skipprereq:silverlight.exe` または `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;Silverlight.exe`  

### <a name="forceinstall"></a>/forceinstall

 既存のクライアントがアンインストールされてから、新しいクライアントがインストールされることを指定します。  

### <a name="excludefeaturesltfeature"></a>/ExcludeFeatures:&lt;機能\>

クライアントをインストールするときに、指定した機能を CCMSetup.exe がインストールしないように指定します。  

例: `CCMSetup.exe /ExcludeFeatures:ClientUI` は、クライアントにソフトウェア センターをインストールしません。  

> [!NOTE]  
>  このリリースでは、 **ClientUI** が、 **/ExcludeFeatures** プロパティでサポートされる唯一の値です。  

##  <a name="ccmsetupReturnCodes"></a> CCMSetup.exe のリターン コード  
 CCMSetup.exe コマンドは、完了すると次のリターン コードを提供します。 問題を解決するには、クライアント コンピューターで ccmsetup.log ファイルを確認して、リターン コードのコンテキストと詳細を確認します。  

|リターン コード|意味|  
|-----------------|-------------|  
|0|成功|  
|6|エラー|  
|7|再起動が必要です|  
|8|セットアップは既に実行されています|  
|9|前提条件の評価エラー|  
|10|セットアップのマニフェスト ハッシュ検証エラー|  

##  <a name="clientMsiProps"></a> Client.msi のプロパティ  
 次のプロパティを使って、client.msi のインストールの動作を変更することができます。 クライアント プッシュ インストール方式を使用する場合は、[ **クライアント プッシュ インストールのプロパティ** ] ダイアログ ボックスの [ **クライアント** ] タブでプロパティを指定することもできます。  

### <a name="ccmadmins"></a>CCMADMINS  

クライアント設定およびポリシーへのアクセスを許可する 1 つまたは複数の Windows ユーザー アカウントまたはグループを指定します。 これは、Configuration Manager 管理者に、クライアント コンピューターに対するローカル管理者資格情報がない場合に役立ちます。 セミコロンで区切って、アカウントの一覧を指定します。  

例: `CCMSetup.exe CCMADMINS="Domain\Account1;Domain\Group1"`  

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

クライアント インストール後に、必要に応じてコンピューターを再起動できるように指定します。  

> [!IMPORTANT]  
>  ユーザーがログオンしている場合でもコンピューターは警告なしに再起動します。  

例: **CCMSetup.exe  CCMALLOWSILENTREBOOT**  

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

 クライアントが常にインターネットベースであり、イントラネットには接続しないことを指定するには、「1」に設定します。 クライアントの接続の種類に **[常にインターネット]**と表示されます。  

 このプロパティは、インターネットベースの管理ポイントの FQDN を指定する CCMHOSTNAME と共に使用する必要があります。 このプロパティはまた、CCMSetup プロパティ /UsePKICert およびサイト コードと共に使用する必要があります。  

 インターネット ベースのクライアント管理の詳細については、「[System Center Configuration Manager でのエンドポイント間の通信](../../plan-design/hierarchy/communications-between-endpoints.md)」の「[インターネットや信頼されていないフォレストからのクライアント通信に関する考慮事項](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan)」を参照してください。  

 例: `CCMSetup.exe /UsePKICert  CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`  

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

 Configuration Manager サイトが信頼する、信頼されたルート証明機関の一覧である証明書発行元一覧を指定します。  

 証明書発行者リストと、これをクライアントが証明書選択プロセスで使用する方法の詳細については、「 [Plan for Security 」 の「 System Center Configuration Manager](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection) 」 の「 [Plan for security 」 の「 System Center Configuration Manager](../../plan-design/security/plan-for-security.md)」を参照してください。  

 ルート CA 証明書のオブジェクトの属性では、大文字と小文字が区別されます。 属性はコンマ (,) またはセミコロン (;) で区切ることができます。 区切り文字を使用すると、複数のルート CA 証明書を指定することができます。 例:  

 `CCMCERTISSUERS=”CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US &#124; CN=Litware Corporate Root CA; O=Litware, Inc.”`  

> [!TIP]  
>  サイト サーバー コンピューターの &lt;Configuration Manager ディレクトリ\>\bin\\&lt;プラットフォーム\> フォルダーで mobileclient.tcf ファイルを参照して、サイト用に構成された **CertificateIssuers=&lt;文字列\>** をコピーします。  

### <a name="ccmcertsel"></a>CCMCERTSEL

 クライアントに HTTPS 通信用の複数の証明書 (クライアント認証機能を含む有効な証明書) がある場合の証明書の選択条件を指定します。  

 サブジェクト名またはサブジェクトの別名の完全一致を検索 (**Subject:** を使用) することも、部分一致を検索 (**SubjectStr:** を使用) することもできます。 例:  

 `CCMCERTSEL="Subject:computer1.contoso.com"` と指定すると、サブジェクト名またはサブジェクトの別名でコンピューター名 "computer1.contoso.com" と完全に一致する証明書を検索します。  

 `CCMCERTSEL="SubjectStr:contoso.com"` と指定すると、サブジェクト名またはサブジェクトの別名で "contoso.com" を含む証明書を検索します。  

 サブジェクト名またはサブジェクトの別名の属性でオブジェクト ID (OID) または識別名の属性を使用することもできます。たとえば、次のようになります。  

 `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"` と指定すると、オブジェクト ID として表される組織単位属性および指定したコンピューターを検索します。  

 `CCMCERTSEL="SubjectAttr:OU = Computers"` と指定すると、識別名として表される組織単位属性および指定したコンピューターを検索します。  

> [!IMPORTANT]  
>  [サブジェクト名] ボックスを使用する場合、**Subject:** では大文字と小文字が区別され、**SubjectStr:** では区別されません。  
>   
>  [サブジェクトの別名] ボックスを使用する場合、**Subject:** と **SubjectStr:** では大文字と小文字は区別されません。  

 証明書の選択に使用できる属性の完全な一覧は、「 [PKI 証明書の選択条件としてサポートされている属性値](#BKMK_attributevalues)」に記載されています。  

 1 つ以上の証明書が検索で一致し、プロパティ CCMFIRSTCERT が「1」に設定されている場合は、有効期限の最も長い証明書が選択されます。  

### <a name="ccmcertstore"></a>CCMCERTSTORE

 HTTPS 用のクライアント証明書が、コンピューター ストアの既定の **個人**用証明書ストアにない場合の代替の証明書ストアの名前を指定します。  

 例: `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

  デバッグ ログを有効にします。 設定できる値は 0 (オフ、既定) または 1 (オン) です。 この場合、クライアントでは、トラブルシューティングのための低レベルの情報がログ出力されます。 実稼働サイトではこのプロパティを使用しないことをお勧めします。これは、このプロパティを使用すると、過度のログ記録が実行され、ログ ファイル内で適切な情報を見つけることが困難になる可能性があるためです。 デバッグ ログを有効にするには、CCMENABLELOGGING も TRUE に設定する必要があります。  

  例: `CCMSetup.exe CCMDEBUGLOGGING=1`  

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

  既定では、ログ記録を有効にするように TRUE に設定されています。 ログ ファイルは、Configuration Manager クライアントのインストール フォルダー内の **Logs** フォルダーに保存されます。 既定では、このフォルダーは %Windir%\CCM\Logs にあります。  

  例: `CCMSetup.exe CCMENABLELOGGING=TRUE`  

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL  

 クライアントの正常性評価ツール (ccmeval.exe) を実行する頻度です。 **1** ～ **1440** 分で設定できます。 既定では 1 日に 1 回実行されます。  

### <a name="ccmevalhour"></a>CCMEVALHOUR

 クライアントの正常性評価ツール (ccmeval.exe) を実行する時刻です。**0** (午前) ～ **23** (午後 11 時) で指定します。 既定では午前 0 時に実行されます。  

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

 「1」に設定されている場合は、このプロパティはクライアントが最も有効期限の長い PKI  証明書を選択するように指定します。 この設定は、IPsec 実施でネットワーク アクセス保護を使用している場合に必要になることがあります。  

 例: `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`  

### <a name="ccmhostname"></a>CCMHOSTNAME

 クライアントがインターネット経由で管理される場合の、インターネットベースの管理ポイントの FQDN を指定します。  

 SMSSITECODE=AUTO のインストール プロパティでこのオプションを指定しないでください。 インターネットベースのクライアントはインターネットベースのサイトに直接割り当てる必要があります。  

 例: `CCMSetup.exe  /UsePKICert/ CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

### <a name="ccmhttpport"></a>CCMHTTPPORT

 HTTP を介してサイト システム サーバーと通信するときにクライアントが使用するポートを指定します。 既定でポート 80 に設定されています。  

 例: `CCMSetup.exe CCMHTTPPORT=80`  

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

HTTPS を介してサイト システム サーバーと通信するときにクライアントが使用するポートを指定します。 既定でポート 443 に設定されています。  

例: `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`  

### <a name="ccminstalldir"></a>CCMINSTALLDIR

 Configuration Manager クライアント ファイルがインストールされるフォルダーを指定します。既定では *%Windir%*\CCM です。 ファイルのインストール場所に関係なく、Ccmcore.dll ファイルは常に *%Windir%\System32* フォルダーにインストールされます。 また、64 ビット オペレーティング システムでは、Configuration Manager ソフトウェア開発キット (SDK) からの Configuration Manager クライアント API の 32 ビット版を使用する 32 ビット アプリケーションをサポートするために、必ず、Ccmcore.dll ファイルのコピーが *%Windir%*\SysWOW64 フォルダーにインストールされます。  

 例: `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`  

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Configuration Manager ログ ファイルに記録する詳細レベルを指定します。 0 ～ 3 の整数を指定します。0 が最も詳細なログ出力で、3 はエラーのみがログに出力されます。 既定値は 1 です。  

例: `CCMSetup.exe CCMLOGLEVEL=3`  

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Configuration Manager ログ ファイルのサイズが 250000 バイト (または CCMLOGMAXSIZE プロパティで指定された値) になると、バックアップとして名前が変更され、新しいログ ファイルが作成されます。  

このプロパティでは、保持する以前のバージョンのログ ファイルの数を指定します。 既定値は 1 です。 このプロパティを 0 に設定すると、ログ ファイルは保持されません。  

例: `CCMSetup.exe CCMLOGMAXHISTORY=0`  

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

ログ ファイルの最大サイズ (バイト単位) です。 ログ ファイルが指定されたサイズに達すると、履歴ファイルとして名前が変更され、新しいファイルが作成されます。 このプロパティは、10000 バイト以上に設定する必要があります。 既定値は 250000 バイトです。  

例: `CCMSetup.exe CCMLOGMAXSIZE=300000`  

### <a name="disablesiteopt"></a>DISABLESITEOPT

 TRUE に設定すると、クライアント コンピューターの管理者資格情報を持つエンド ユーザーが、クライアントのコントロール パネルの **Configuration Manager** で、Configuration Manager の割り当て済みサイトを変更することができなくなります。  

 例: **CCMSetup.exe DISABLESITEOPT=TRUE**  

### <a name="disablecacheopt"></a>DISABLECACHEOPT

「TRUE」 に設定すると、クライアント コンピューターの管理者資格情報を持つエンドユーザーが、クライアント コンピューターのコントロール パネルで Configuration Manager を使用して、Configuration Manager クライアントのプログラム クライアントのキャッシュ フォルダーの設定を変更することができなくなります。  

例: `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

 クライアント用に、DNS で発行されている管理ポイントを検索する DNS ドメインを指定します。 管理ポイントが特定されると、その管理ポイントは、階層内のその他の管理ポイントについて、クライアントに通知します。 つまり、DNS 発行によって特定される管理ポイントは、クライアントのサイトに存在する必要はなく、階層内のすべての管理ポイントが対象となります。  

> [!NOTE]  
>  このプロパティは、発行された管理ポイントとクライアントが同じドメインにある場合、指定する必要はありません。 この場合、DNS での管理ポイントの検索で、クライアントのドメインが自動的に使用されます。  

 Configuration Manager クライアントに対するサービスの場所の検索方法として DNS 発行を使用することの詳細については、「[クライアントが System Center Configuration Manager のサイト リソースやサービスを検索する方法を理解する](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)」の「[サービスの場所とクライアントが割り当て済み管理ポイントを特定する方法](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location)」を参照してください。  

> [!NOTE]  
>  既定では、DNS 発行は Configuration Manager で無効になっています。  

 例: `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`  

### <a name="fsp"></a>FSP

Configuration Manager クライアント コンピューターによって送信される状態メッセージを受信して処理するフォールバック ステータス ポイントを指定します。  

フォールバック ステータス ポイントの詳細については、「[Determine if you need a fallback status point](/sccm/core/clients/deploy/plan#determine-if-you-need-a-fallback-status-point)」 (フォールバック ステータス ポイントが必要かどうかを確認する) をご覧ください。  

例: `CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

 クライアントがインストールされる前に、Microsoft Application Virtualization (App-V) の必要最小バージョンが存在するかどうかを確認しないことを指定します。  

> [!IMPORTANT]  
>  App-V をインストールせずに Configuration Manager クライアントをインストールすると、仮想アプリケーションを展開することはできません。  

 例: `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`  

### <a name="notifyonly"></a>NOTIFYONLY

クライアントで見つかった問題について、クライアントのステータスで報告しますが、修復はしないことを指定します。  

例: `CCMSetup.exe NOTIFYONLY=TRUE`  

詳細については、「 [How to configure client status in System Center Configuration Manager](configure-client-status.md)」をご覧ください。  

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

 Configuration Manager クライアントに間違った Configuration Manager の信頼されたルート キーがあり、信頼された管理ポイントに接続して新しい信頼されたルート キーを取得できない場合は、このプロパティを使用して古い信頼されたルート キーを手動で削除する必要があります。 この状況は、クライアントを 1 つのサイト階層から別のサイト階層に移動したときに発生する場合があります。 このプロパティは、HTTP および HTTPS クライアント接続を使用するクライアントに適用されます。  

 例: `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

[SMSSITECODE](#smssitecode)=AUTO と共に使用して、クライアント アップグレードの自動サイト再割り当てを有効にします。

例: `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

一時ファイルを保存するクライアント コンピューターのクライアントキャッシュ フォルダーの場所を指定します。 既定では、 *%Windir \ccmcache*にあります。  

例: `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

このプロパティを SMSCACHEFLAGS プロパティと共に使用すると、クライアント キャッシュ フォルダーの場所を制御できます。  

例: `CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE` は、最も空き容量の大きいクライアント ディスク ドライブにクライアント キャッシュ フォルダーをインストールします。  

### <a name="smscacheflags"></a>SMSCACHEFLAGS

クライアント キャッシュ フォルダーのインストールの詳細を指定します。 SMSCACHEFLAGS プロパティは、単独で、またはセミコロンで区切った組み合わせで使用できます。 このプロパティを指定しない場合、クライアント キャッシュ フォルダーは SMSCACHEDIR プロパティに従ってインストールされ、フォルダーは圧縮されず、SMSCACHESIZE の値は MB 単位のフォルダー サイズとして使用されます。  

既存のクライアントをアップグレードすると、この設定は無視されます。  

［プロパティ］:  

-   PERCENTDISKSPACE: フォルダー サイズを合計ディスク領域に対する割合として指定します。 このプロパティを指定する場合は、SMSCACHESIZE プロパティを使用する割合値として指定する必要もあります。  

-   PERCENTFREEDISKSPACE: フォルダー サイズをディスク空き領域に対する割合として指定します。 このプロパティを指定する場合は、SMSCACHESIZE プロパティを使用する割合値として指定する必要もあります。 たとえば、ディスクに 10 MB の空き領域があり、SMSCACHESIZE を 50 に指定した場合、フォルダー サイズは 5 MB に設定されます。 このプロパティを PERCENTDISKSPACE プロパティと共に使用することはできません。  

-   MAXDRIVE: 利用できる最も大きいディスクにフォルダーをインストールすることを指定します。 この値は、パスが SMSCACHEDIR プロパティと共に指定されている場合は無視されます。  

-   MAXDRIVESPACE: 空き領域が最も大きいディスク ドライブにフォルダーをインストールするように指定します。 この値は、パスが SMSCACHEDIR プロパティと共に指定されている場合は無視されます。  

-   NTFSONLY: NTFS ディスク ドライブにのみフォルダーをインストールするように指定します。 この値は、パスが SMSCACHEDIR プロパティと共に指定されている場合は無視されます。  

-   COMPRESS: フォルダーを圧縮形式で保持するように指定します。  

-   FAILIFNOSPACE: フォルダーをインストールするための領域が十分にない場合にクライアント ソフトウェアを削除するように指定します。  

例: `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`  


### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> Configuration Manager バージョン 1606 以降では、新しいクライアント設定でクライアント キャッシュ フォルダーのサイズを指定できます。 これらのクライアント設定を追加すると、SMSCACHESIZE を使用して、クライアント キャッシュのサイズを指定する client.msi プロパティとして効果的に置き換えられます。 詳細については、「[キャッシュ サイズに関するクライアント設定](about-client-settings.md#client-cache-settings)」を参照してください。  

1602 より前では、PERCENTDISKSPACE プロパティまたは PERCENTFREEDISKSPACE プロパティと共に使用する場合は、SMSCACHESIZE はクライアント キャッシュ フォルダーのサイズをメガバイト (MB) 単位またはパーセント単位で指定します。 このプロパティを設定しない場合は、フォルダーは既定の最大サイズの 5120 MB に設定されます。 指定できる最小値は 1 MB です。  

> [!NOTE]  
>  ダウンロードが必要な新しいパッケージが原因でフォルダーが最大サイズを超えた場合で、フォルダーを消去して十分な領域を空けることができない場合は、パッケージのダウンロードは失敗し、プログラムまたはアプリケーションは実行されません。  

既存のクライアントをアップグレードしたり、クライアントがソフトウェア更新プログラムをダウンロードしたりしたときは、この設定は無視されます。  

例: `CCMSetup.exe SMSCACHESIZE=100`  

> [!NOTE]  
>  クライアントをインストールする場合、SMSCACHESIZE プロパティまたは SMSCACHEFLAGS プロパティを使用して以前よりも小さいキャッシュ サイズを設定することはできません。 小さいサイズを設定しようとすると、値は無視され、キャッシュ サイズには以前の設定値が自動的に設定されます。  

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

Configuration Manager インストーラーで構成設定を確認する場所と順序を指定します。 このプロパティは、各文字が特定の構成ソースを定義する 1 つまたは複数の文字で構成される文字列です。 R、P、M、および U の文字の値を単独で、または組み合わせて使用します。  

-   R: レジストリで構成設定を確認します。  

   詳しくは、[レジストリ内のクライアント インストール プロパティの保存に関する情報](https://technet.microsoft.com/library/gg712298.aspx#BKMK_Provision)をご覧ください。  

-   P: コマンド プロンプトで指定したインストール プロパティで構成設定を確認します。  

-   M: 古いクライアントを Configuration Manager クライアント ソフトウェアでアップグレードするときに既存の設定を確認します。  

-   U: インストールしたクライアントを新しいバージョンにアップグレードします (さらに、割り当てられたサイト コードを使用します)。  

 既定では、クライアント インストールでは `PU` が使用され、最初にインストール プロパティ、次に既存の設定がチェックされます。  

 例: `CCMSetup.exe SMSCONFIGSOURCE=RP`  

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

 クライアントが Windows Internet Name Service (WINS) を使用して HTTP 接続を許可する管理ポイントを検索できるようにするかどうかを指定します。 Active Directory ドメイン サービスまたは DNS に管理ポイントが見つからないとき、クライアントはこの方法を使用します。  

 このプロパティは、クライアントが名前解決に WINS を使用するかどうかに影響しません。  

 このプロパティでは 2 つの異なるモードを構成できます。  

-   NOWINS: これはこのプロパティでは最も安全な設定であり、クライアントが WINS で管理ポイントを探すのを防ぎます。  この設定を使用する場合は、クライアントには、Active Directory ドメイン サービスといったイントラネット上、または DNS 公開の使用などで管理ポイントを探す代替の方法が用意されている必要があります。  

-   WINSSECURE (既定): このモードでは、HTTP 通信を使用するクライアントは、WIN を使用して管理ポイントを探すことができます。 しかし、クライアントは管理ポイントへ接続する前に信頼されたルート キーを持っている必要があります。 詳細については、「 [Plan for Security 」の「 System Center Configuration Manager](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) 」の「 [Plan for security 」の「 System Center Configuration Manager](../../plan-design/security/plan-for-security.md)」を参照してください。  


 例: `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  

### <a name="smsmp"></a>SMSMP

Configuration Manager クライアントが使用する最初の管理ポイントを指定します。  

> [!IMPORTANT]  
>  管理ポイントが HTTPS でのクライアント接続のみを受け入れる場合、管理ポイント名の先頭に https:// を付加する必要があります。  

例: `CCMSetup.exe SMSMP=smsmp01.contoso.com`

例: `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  

### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

 Configuration Manager の信頼されたルート キーを Active Directory Domain Services から取得できない場合は、Configuration Manager の信頼されたルート キーを指定します。 このプロパティは、HTTP および HTTPS クライアント接続を使用するクライアントに適用されます。 詳細については、「 [Plan for Security 」の「 System Center Configuration Manager](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) 」の「 [Plan for security 」の「 System Center Configuration Manager](../../plan-design/security/plan-for-security.md)」を参照してください。  

 例: `CCMSetup.exe SMSPUBLICROOTKEY=&lt;key\>`  

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

 Configuration Manager の信頼されたルート キーを再インストールするために使用します。 信頼されたルート キーを含むファイルの完全なパスとファイル名を指定します。 このプロパティは、HTTP および HTTPS クライアント接続を使用するクライアントに適用されます。 詳細については、「 [Plan for Security 」の「 System Center Configuration Manager](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) 」の「 [Plan for security 」の「 System Center Configuration Manager](../../plan-design/security/plan-for-security.md)」を参照してください。  

 例: CCMSetup.exe SMSROOTKEYPATH=&lt;完全なパスとファイル名\>`  

### <a name="smssigncert"></a>SMSSIGNCERT

 サイト サーバーのエクスポートされる自己署名した証明書の完全なパスと .cer ファイル名を指定します。  

 この証明書は、 **SMS** 証明書ストアに保存されています。サブジェクト名は **Site Server** 、フレンドリ名は **Site Server Signing Certificate**です。  

 例: **CCMSetup.exe /UsePKICert SMSSIGNCERT=&lt;完全なパスとファイル名\>**  

### <a name="smssitecode"></a>SMSSITECODE

 Configuration Manager クライアントを割り当てる Configuration Manager サイトを指定します。 3 文字のサイト コードか、または AUTO を指定できます。 AUTO が指定された場合、またはこのプロパティが指定されなかった場合は、クライアントは、Active Directory Domain Services または指定した管理ポイントからの Configuration Manager サイト割り当てを判断しようと試みます。 クライアントのアップグレードに対して AUTO を有効にするには、[SITEREASSIGN](#sitereassign) を TRUE に設定する必要もあります。    

> [!NOTE]  
>  インターネットベースの管理ポイント (CCMHOSTNAME) も指定する場合、AUTO を使用しないでください。 この場合、クライアントをそのサイトに直接割り当てる必要があります。  

 例: `CCMSetup.exe SMSSITECODE=XZY`  

##  <a name="BKMK_attributevalues"></a> PKI 証明書の選択条件としてサポートされている属性値  
 Configuration Manager は、PKI 証明書の選択条件として次の属性値をサポートしています。  

|OID 属性|識別名属性|属性の定義|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|ドメイン要素|  
|1.2.840.113549.1.9.1|E または E-mail|電子メール アドレス|  
|2.5.4.3|CN|共通名|  
|2.5.4.4|SN|サブジェクト名|  
|2.5.4.5|SERIALNUMBER|シリアル番号|  
|2.5.4.6|C|国番号|  
|2.5.4.7|L|地域|  
|2.5.4.8|S または ST|州または都道府県|  
|2.5.4.9|STREET|住所|  
|2.5.4.10|O|組織名|  
|2.5.4.11|OU|組織単位|  
|2.5.4.12|T または Title|タイトル|  
|2.5.4.42|G または GN または GivenName|名前|  
|2.5.4.43|I または Initials|イニシャル|  
|2.5.29.17|(値なし)|サブジェクト代替名|  

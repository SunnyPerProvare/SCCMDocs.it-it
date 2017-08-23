---
title: "タスク シーケンス アクション変数 | Microsoft Docs"
description: "ネットワーク設定変数などのシーケンス アクション変数を使用して、Configuration Manager のタスク シーケンスでシングル ステップの構成設定を指定します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2269031-0977-4f01-a274-420e00630575
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 6049ec2369e0a97b21ce6523ba8448335385ab9a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="task-sequence-action-variables-in-system-center-configuration-manager"></a>System Center Configuration Manager でのタスク シーケンス アクション変数

*適用対象: System Center Configuration Manager (Current Branch)*

タスク シーケンス アクション変数では、System Center Configuration Manager タスク シーケンスの単一ステップで使用される構成設定を指定します。 既定では、タスク シーケンスのステップで使用される設定は、ステップの実行前に初期化され、関連付けられているタスク シーケンスのステップの実行時にのみ利用できます。 つまり、タスク シーケンス変数の設定は、タスク シーケンスのステップの実行前にタスク シーケンス環境に追加され、タスク シーケンスのステップの実行後にタスク シーケンス環境から値が削除されます。  

## <a name="action-variable-example"></a>アクション変数の例  
 たとえば、[コマンド ラインの実行 **** ] タスク シーケンスのステップを使用して、コマンド ライン操作の開始ディレクトリを指定できます。 このステップには、既定値がタスク シーケンス環境に **WorkingDirectory** 変数として格納される [開始 **** ] プロパティが含まれます。 **WorkingDirectory** 環境変数は、[コマンド ラインの実行] タスク シーケンス アクションの実行前に初期化されます。 **** [コマンド ラインの実行 **** ] ステップの実行中に、[開始 **** ] プロパティを使用して **WorkingDirectory** の値にアクセスできます。 タスク シーケンスのステップが完了すると、 **WorkingDirectory** 変数の値はタスク シーケンス環境から削除されます。 シーケンスに別の [コマンド ラインの実行 **** ] タスク シーケンスのステップが含まれている場合、新しい **WorkingDirectory** 変数は初期化され、そのタスク シーケンスのステップの初期値に設定されます。  

 タスク シーケンス アクション設定の既定値はタスク シーケンスのステップの実行中に存在しますが、設定した任意の新しい値は、シーケンス内の複数のステップにより使用できます。 タスク シーケンス変数の作成方法のいずれかを使用して、組み込み変数値を上書きすると、新しい値が環境に残り、タスク シーケンスの他のステップの既定値が上書きされます。 前の例で言えば、[**タスク シーケンス変数の設定**] ステップをタスク シーケンスの最初のステップとして追加し、[**WorkingDirectory**] 環境変数の値を **C:\ \\**に設定した場合は、タスク シーケンス内の両方の [**コマンド ラインの実行**] ステップで、新しい開始ディレクトリ値が使用されます。  

## <a name="action-variables-for-task-sequence-actions"></a>タスク シーケンス アクションのアクション変数  
 Configuration Manager タスク シーケンス変数は、関連付けられたタスク シーケンス アクションごとに分類されます。 特定のアクションに関連付けられているアクション変数の詳細については、次のリンク先を参照してください。 タスク シーケンス変数は、タスク シーケンスで何が行われるかを制御します。 タスク シーケンスの入力変数に指定した変数が、読み取られて使用されます。 または、[タスク シーケンス変数の設定] か TSEnvironment COM オブジェクトを使用して、実行時に変数を設定することもできます。 タスク シーケンス内の現在位置より後で読み取られる変数だけが出力変数と見なされます。  

> [!NOTE]  
>  すべてのタスク シーケンス アクションが、一連のタスク シーケンス変数に関連付けられているわけではありません。 たとえば、BitLocker の有効化アクションに関連付けれている変数はありますが、BitLocker の無効化アクションに関連付けられている変数はありません。  

###  <a name="BKMK_ApplyDataImage"></a> データ イメージの適用タスク シーケンス アクション変数  
 このアクションの変数では、WIM ファイルのどのイメージを対象のコンピューターに適用するのか、および対象のパーティションのファイルを削除するかどうかを指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Apply Data Image Task Sequence Step](task-sequence-steps.md#BKMK_ApplyDataImage)」 (データ イメージの適用タスク シーケンス ステップ) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDDataImageIndex<br /><br /> (入力)|対象のコンピューターに適用されるイメージのインデックス値を指定します。|  
|OSDWipeDestinationPartition<br /><br /> (入力)|対象のパーティションにあるファイルを削除するかどうかを指定します。<br /><br /> 有効な値:<br /><br /> **"TRUE"** (既定)<br /><br /> **"FALSE"**|  

###  <a name="BKMK_ApplyDriverPackage"></a> ドライバー パッケージの適用タスク シーケンス アクション変数  
 このアクションの変数では、大容量記憶装置ドライバーのインストールに関する情報、および署名されていないドライバーをインストールするかどうかを指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Apply Driver Package](task-sequence-steps.md#BKMK_ApplyDriverPackage)」 (ドライバー パッケージの適用) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDApplyDriverBootCriticalContentUniqueID<br /><br /> (入力)|ドライバー パッケージからインストールする大容量記憶装置デバイス ドライバーのコンテンツ ID を指定します。 この値を指定しない場合、大容量記憶装置ドライバーはインストールされません。|  
|OSDApplyDriverBootCriticalINFFile<br /><br /> (入力)|インストールする大容量記憶装置ドライバーの INF ファイルを指定します。<br /><br /> <br /><br /> このタスク シーケンス変数は、OSDApplyDriverBootCriticalContentUniqueID が設定されている場合に必要です。|  
|OSDApplyDriverBootCriticalHardwareComponent<br /><br /> (入力)|大容量記憶装置デバイス ドライバーをインストールするかどうかを指定します。値は **scsi** にする必要があります。<br /><br /> <br /><br /> このタスク シーケンス変数は、OSDApplyDriverBootCriticalContentUniqueID が設定されている場合に必要です。|  
|OSDApplyDriverBootCriticalID<br /><br /> (入力)|インストールする大容量記憶装置デバイス ドライバーの起動に必要な ID を指定します。 この ID は、デバイス ドライバーの txtsetup.oem ファイルの "**scsi**" セクションに一覧表示されます。<br /><br /> <br /><br /> このタスク シーケンス変数は、OSDApplyDriverBootCriticalContentUniqueID が設定されている場合に必要です。|  
|OSDAllowUnsignedDriver<br /><br /> (入力)|署名されていないデバイス ドライバーのインストールを許可するように Windows を構成するかどうかを指定します。 このタスク シーケンス変数は、Windows Vista 以降のオペレーティング システムの展開時には使用されません。<br /><br /> 有効な値:<br /><br /> **"TRUE"**<br /><br /> **"FALSE"** (既定)|  

###  <a name="BKMK_ApplyNetworkSettings"></a> ネットワーク設定の適用タスク シーケンス アクション変数  
 このアクションの変数では、コンピューターのネットワーク アダプターの設定、ドメイン設定、ワークグループ設定などの、対象コンピューターのネットワーク設定を指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Apply Network Settings Step](task-sequence-steps.md#BKMK_ApplyNetworkSettings)」 (ネットワーク設定の適用ステップ) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDAdapter<br /><br /> (入力)|このタスク シーケンス変数は、配列変数です。 配列内の各要素は、コンピューター上の単一ネットワーク アダプターの設定を表します。 各アダプターに定義された設定にアクセスするには、配列変数名にゼロから始まるネットワーク アダプター インデックスとプロパティ名を組み合わせます。<br /><br /> <br /><br /> このタスク シーケンス アクションを使用して複数のネットワーク アダプターを構成する場合、2 つ目のネットワーク アダプターのプロパティを定義するときに、OSDAdapter1EnableDHCP、OSDAdapter1IPAddressList、OSDAdapter1DNSDomain、OSDAdapter1WINSServerList、OSDAdapter1EnableWINS など、変数名のインデックスを使用できます。<br /><br /> <br /><br /> たとえば、次の変数名を使用して、このタスク シーケンス アクションで構成する 1 つ目のネットワーク アダプターにプロパティを定義できます。<br /><br /> <ul><li>**OSDAdapter0EnableDHCP** – true になっていると、アダプターの動的ホスト構成プロトコル (DHCP) が有効になります。<br />    この設定は必須です。 使用できる値は True または False です。</li><li>**OSDAdapter0IPAddressList** – アダプターの IP アドレスを記載したコンマ区切りの一覧です。 このプロパティは **EnableDHCP** が **FALSE**に設定されている場合を除き、無視されます。<br />    この設定は必須です。</li><li>**OSDAdapter0SubnetMask** – サブネット マスクを記載したコンマ区切りの一覧です。 このプロパティは **EnableDHCP** が **FALSE**に設定されている場合を除き、無視されます。<br />    この設定は必須です。</li><li>**OSDAdapter0Gateways** – IP ゲートウェイ アドレスを記載したコンマ区切りの一覧です。 このプロパティは **EnableDHCP** が **FALSE**に設定されている場合を除き、無視されます。<br />    この設定は必須です。</li><li>**OSDAdapter0DNSDomain** - アダプターの ドメイン ネーム システム (DNS) です。</li><li>**OSDAdapter0DNSServerList** – アダプターの DNS サーバーを記載したコンマ区切りの一覧です。<br />    この設定は必須です。</li><li>**OSDAdapter0EnableDNSRegistration** - **true** になっているとアダプターの IP アドレスが DNS に登録されます。</li><li>**OSDAdapter0EnableFullDNSRegistration** - **true** になっているとアダプターの IP アドレスが コンピューターのフル DNS 名で DNS に登録されます。</li><li>**OSDAdapter0EnableIPProtocolFiltering** - **true** になっているとアダプターで IP プロトコル フィルターが有効になります。</li><li>**OSDAdapter0IPProtocolFilterList** – IP での実行を許可されたプロトコルを記載したコンマ区切りの一覧です。 このプロパティは **EnableIPProtocolFiltering** が **FALSE**に設定されている場合、無視されます。</li><li>**OSDAdapter0EnableTCPFiltering** - **true** になっているとアダプターで TCP ポート フィルターが有効になります。</li><li>**OSDAdapter0TCPFilterPortList** – TCP へのアクセス許可を付与するポートを記載したコンマ区切りの一覧です。 このプロパティは **EnableTCPFiltering** が **FALSE**に設定されている場合、無視されます。</li><li>**OSDAdapter0TcpipNetbiosOptions** – NetBIOS over TCP/IP 用のオプションです。 使用できる値は次のとおりです。<br /><br /> <ul><li>0: DHCP サーバーから NetBIOS 設定を使用する。</li><li>1: NetBIOS over TCP/IP を有効にする。</li><li>2: NetBIOS over TCP/IP を無効にする。</li></ul></li><li>**OSDAdapter0EnableWINS** - **true** になっていると名前解決に WINS が使用されます。</li><li>**OSDAdapter0WINSServerList** – WINS サーバー IP アドレスを記載したコンマ区切りの一覧です。 このプロパティは **EnableWINS** が **TRUE**に設定されている場合を除き、無視されます。</li><li>**OSDAdapter0MacAddress** – 設定を物理ネットワーク アダプターに合わせるために使用するメディア アクセス コントローラー (MAC) アドレスです。</li><li>**OSDAdapter0Name** – ネットワーク接続のコントロール パネル プログラムに表示されるネットワーク接続名です。 名前は 0 ～ 255 文字の長さにしてください。</li><li>**OSDAdapter0Index** – 設定の配列内にあるネットワーク アダプター設定のインデックスです。<br /><br />     OSDAdapterCount=1<br />    OSDAdapter0EnableDHCP=FALSE<br />    OSDAdapter0IPAddressList=192.168.0.40<br />    OSDAdapter0SubnetMask=255.255.255.0<br />    OSDAdapter0Gateways=192.168.0.1<br />    OSDAdapter0DNSSuffix=contoso.com</li></ul>|  
|OSDAdapterCount<br /><br /> (入力)|対象のコンピューターにインストールされているネットワーク アダプターの数を指定します。 **OSDAdapterCount** 値が設定されている場合、各アダプターのすべての構成オプションを設定する必要があります。 たとえば、特定のアダプターの **OSDAdapterTCPIPNetbiosOptions** 値を設定したら、そのアダプターのすべての値を構成する必要があります。<br /><br /> <br /><br /> この値が指定されていない場合、すべての **OSDAdapter** 値が無視されます。|  
|OSDDNSDomain<br /><br /> (入力)|対象のコンピューターによって使用されるプライマリ DNS サーバーを指定します。|  
|OSDDomainName<br /><br /> (入力)|対象のコンピューターを参加させる Windows ドメインの名前を指定します。 指定する値は Active Directory ドメイン サービスの有効なドメイン名でなければなりません。|  
|OSDDomainOUName<br /><br /> (入力)|対象コンピューターを参加させる組織単位 (OU) の RFC 1779 形式の名前を指定します。 指定する場合の値は、完全なパスを含む必要があります。<br /><br /> 例:<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDEnableTCPIPFiltering<br /><br /> (入力)|TCP/IP フィルタリングを有効にするかどうかを指定します。<br /><br /> 有効な値:<br /><br /> **"TRUE"**<br /><br /> **"FALSE"** (既定)|  
|OSDJoinAccount<br /><br /> (入力)|対象のコンピューターを Windows ドメインに追加するために使用するネットワーク アカウントを指定します。|  
|OSDJoinPassword<br /><br /> (入力)|対象のコンピューターを Windows ドメインに追加するために使用するネットワーク パスワードを指定します。|  
|OSDNetworkJoinType<br /><br /> (入力)|対象コンピューターを Windows ドメインに参加させるか、ワークグループに参加させるかを指定します。<br /><br /> "**0** " を指定すると、対象のコンピューターは Windows ドメインに参加します。 "**1** " を指定すると、コンピューターはワークグループに参加します。<br /><br /> 有効な値:<br /><br /> **0**<br /><br /> **1**|  
|OSDDNSSuffixSearchOrder<br /><br /> (入力)|対象のコンピューターの DNS 検索順序を指定します。|  
|OSDWorkgroupName<br /><br /> (入力)|対象のコンピューターを参加させるワークグループの名前を指定します。<br /><br /> この変数と **OSDDomainName** のどちらかの値を指定する必要があります。 ワークグループの名前は 32 文字までの長さにできます。<br /><br /> 例:<br /><br /> **"会計"**|  

###  <a name="BKMK_ApplyOperatingSystem"></a> オペレーティング システム イメージの適用タスク シーケンス アクション変数  
 このアクションの変数では、対象のコンピューターにインストールするオペレーティング システムの設定を指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Apply Operating System Image](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage)」 (オペレーティング システム イメージの適用) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDConfigFileName<br /><br /> (入力)|オペレーティング システムの展開パッケージに関連付けられているオペレーティング システムの展開の応答ファイルの名前を指定します。|  
|OSDImageIndex<br /><br /> (入力)|対象のコンピューターに適用される WIM イメージのイメージ インデックス値を指定します。|  
|OSDInstallEditionIndex<br /><br /> (入力)|インストールする Windows Vista 以降のオペレーティング システムのバージョンを指定します。 バージョンを指定しない場合、Windows セットアップでは参照されたプロダクト キーを使用してインストールするバージョンが判断されます。<br /><br /> 次の条件を満たす場合は、0 (ゼロ) のみを使用してください。<br /><br /> -   Windows Vista より前のオペレーティング システムをインストールしている<br />-   Windows Vista 以降のボリューム ライセンス版をインストールしており、プロダクト キーを指定していない<br /><br /> 有効な値:<br /><br /> **"0"** (既定)|  
|OSDTargetSystemDrive (出力)|オペレーティング システム ファイルが含まれているパーティションのドライブ文字を設定します。|  

###  <a name="BKMK_ApplyWindowsSettings"></a> Windows 設定の適用タスク シーケンス アクション変数  
 このアクションの変数では、コンピューター名、Windows プロダクト キー、登録ユーザーと組織、ローカルの管理者パスワードなどの、対象のコンピューターの Windows 設定を指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「 [Apply Windows Settings](task-sequence-steps.md#BKMK_ApplyWindowsSettings)」 (Windows 設定の適用) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDComputerName<br /><br /> (入力)|対象のコンピューターの名前を指定します。<br /><br /> 例:<br /><br /> **"%_SMSTSMachineName%"** (既定)|  
|OSDProductKey<br /><br /> (入力)|Windows のプロダクト キーを指定します。 値は 1 ～ 255 文字の範囲で指定する必要があります。|  
|OSDRegisteredUserName<br /><br /> (入力)|新しいオペレーティング システムに既定で登録するユーザー名を指定します。 値は 1 ～ 255 文字の範囲で指定する必要があります。|  
|OSDRegisteredOrgName<br /><br /> (入力)|新しいオペレーティング システムに既定で登録する組織名を指定します。 値は 1 ～ 255 文字の範囲で指定する必要があります。|  
|OSDTimeZone<br /><br /> (入力)|新しいオペレーティング システムで使用する既定のタイム ゾーン設定を指定します。|  
|OSDServerLicenseMode<br /><br /> (入力)|使用する Windows Server ライセンス モードを指定します。<br /><br /> 有効な値:<br /><br /> **"PerSeat"**<br /><br /> **"PerServer"**|  
|OSDServerLicenseConnectionLimit<br /><br /> (入力)|最大接続許可数を指定します。 接続数は 5 ～ 9999 の範囲で指定する必要があります。|  
|OSDRandomAdminPassword<br /><br /> (入力)|新しいオペレーティング システムの管理者アカウントにランダム生成パスワードを使用するかどうかを指定します。 **true** に設定した場合、対象のコンピューターのローカル管理者アカウントは無効になります。 **false** に設定した場合、対象のコンピューターのローカル管理者アカウントが有効になり、ローカル管理者アカウントのパスワードには、変数 **OSDLocalAdminPassword** の値が割り当てられます。<br /><br /> 有効な値:<br /><br /> **"TRUE"** (既定)<br /><br /> **"FALSE"**|  
|OSDLocalAdminPassword<br /><br /> (入力)|ローカルの管理者パスワードを指定します。 この値は、[ローカルの管理者パスワードをランダムに生成し、サポートされているすべてのプラットフォームのアカウントを無効にする] オプションをオンにした場合は無視されます。 **** 値は 1 ～ 255 文字の範囲で指定する必要があります。|  

###  <a name="BKMK_AutoApplyDrivers"></a> ドライバーの自動適用タスク シーケンス アクション変数  
 このアクションの変数では、対象のコンピューターにどの Windows ドライバーをインストールするのか、および署名されていないドライバーをインストールするかどうかを指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Auto Apply Drivers](task-sequence-steps.md#BKMK_AutoApplyDrivers)」 (ドライバーの自動適用) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDAutoApplyDriverCategoryList<br /><br /> (入力)|ドライバー カタログ カテゴリの一意の ID を記載するカンマ区切りの一覧です。 指定した場合、[ドライバーの自動適用] タスク シーケンス アクションでは、ドライバーのインストール時に、これらのカテゴリに含まれているドライバーのみが考慮されます。 **** この値は省略可能であり、既定では設定されていません。 利用可能なカテゴリ ID は、サイトの **SMS_CategoryInstance** オブジェクトの一覧を列挙することで取得できます。|  
|OSDAllowUnsignedDriver<br /><br /> (入力)|署名されていないデバイス ドライバーのインストールを許可するように Windows を構成するかどうかを指定します。 このタスク シーケンス変数は、Windows Vista 以降のオペレーティング システムの展開時には使用されません。<br /><br /> 有効な値:<br /><br /> **"TRUE"**<br /><br /> **"FALSE"** (既定)|  
|OSDAutoApplyDriverBestMatch<br /><br /> (入力)|ハードウェア デバイスと互換性のある複数のデバイス ドライバーがドライバー カタログに含まれている場合にタスク シーケンス アクションで実行する処理を指定します。 **"true"** に設定すると最適なデバイス ドライバーのみがインストールされます。  **false** を指定すると、互換性のあるすべてのデバイス ドライバーがインストールされ、使用する最適なドライバーは、オペレーティング システムによって選択されます。<br /><br /> 有効な値:<br /><br /> **"TRUE"** (既定)<br /><br /> **"FALSE"**|  

###  <a name="BKMK_CaptureNetworkSettings"></a> ネットワーク設定のキャプチャ タスク シーケンス アクション変数  
 このアクションの変数では、ネットワーク アダプター設定 (TCP/IP、DNS、WINS) の構成情報をキャプチャするかどうか、およびワークグループまたはドメインのメンバーシップ情報をオペレーティング システム展開の一部として移行するかどうかを指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Capture Network Settings](task-sequence-steps.md#BKMK_CaptureNetworkSettings)」 (ネットワーク設定のキャプチャ) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDMigrateAdapterSettings<br /><br /> (入力)|ネットワーク アダプター設定 (TCP/IP、DNS、WINS) の構成情報をキャプチャするかどうかを指定します。<br /><br /> 例:<br /><br /> **"TRUE"** (既定)<br /><br /> **"FALSE"**|  
|OSDMigrateNetworkMembership<br /><br /> (入力)|ワークグループまたはドメインのメンバーシップ情報をオペレーティング システムの展開の一部として移行するかどうかを指定します。<br /><br /> 例:<br /><br /> **"TRUE"** (既定)<br /><br /> **"FALSE"**|  

###  <a name="BKMK_CaptureOperatingSystemImage"></a> オペレーティング システム イメージのキャプチャ タスク シーケンス アクション変数  
 このアクションの変数では、イメージの格納場所、イメージの作成者、イメージの説明などの、キャプチャするオペレーティング システム イメージに関する情報を指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Capture Operating System Image](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage)」 (オペレーティング システム イメージのキャプチャ) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDCaptureAccount<br /><br /> (入力)|キャプチャしたイメージをネットワーク共有に格納するためのアクセス許可を持つ Windows アカウント名を指定します。|  
|OSDCaptureAccountPassword<br /><br /> (入力)|キャプチャしたイメージをネットワーク共有に格納するのに使用される Windows アカウントのパスワードを指定します。|  
|OSDCaptureDestination<br /><br /> (入力)|キャプチャしたオペレーティング システム イメージを保存する場所を指定します。 ディレクトリ名の最大長は 255 文字です。|  
|OSDImageCreator<br /><br /> (入力)|イメージを作成したユーザーのオプションの名前。 この名前は WIM ファイルに保存されます。 ユーザー名の最大長は 255 文字です。|  
|OSDImageDescription<br /><br /> (入力)|キャプチャするオペレーティング システム イメージに関する、オプションのユーザー定義の説明。 この説明は WIM ファイルに保存されます。 この説明の最大長は 255 文字です。|  
|OSDImageVersion<br /><br /> (入力)|キャプチャしたオペレーティング システム イメージに割り当てる、ユーザーが任意に定義したバージョン番号。 このバージョン番号は WIM ファイルに保存されます。 この値は、文字の任意の組み合わせにすることができ、最大長は 32 文字です。|  
|OSDTargetSystemRoot<br /><br /> (入力)|参照コンピューター上にインストールされたオペレーティング システムの Windows ディレクトリへのパスを指定します。 このオペレーティング システムは Configuration Manager によるキャプチャをサポートするオペレーティング システムとして検証済みです。|  

###  <a name="BKMK_CaptureUserState"></a> ユーザー状態のキャプチャ タスク シーケンス アクション変数  
 このアクションの変数では、ユーザー状態を保存するフォルダー、USMT のコマンド ライン オプション、ユーザー プロファイルの制御とキャプチャに使用する構成ファイルなどの、ユーザー状態移行ツール (USMT) で使用される情報を指定します。  これらの変数に関連するタスク シーケンス ステップの詳細については、「[Capture User State](task-sequence-steps.md#BKMK_CaptureUserState)」 (ユーザー状態のキャプチャ) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (入力)|ユーザー状態を保存するフォルダーの UNC またはローカル パス名。 既定の設定はありません。|  
|OSDMigrateAdditionalCaptureOptions<br /><br /> (入力)|ユーザー状態のキャプチャ時に使用する、Configuration Manager ユーザー インターフェイスに表示されない、ユーザー状態移行ツール (USMT) のコマンド ライン オプションを指定します。 追加のオプションは、自動生成された USMT コマンド ラインに付加される文字列の形式で指定されます。<br /><br /> <br /><br /> タスク シーケンスを実行するまで、このタスク シーケンス変数で指定される USMT オプションの正確性は検証されません。|  
|OSDMigrateMode<br /><br /> (入力)|USMT によってキャプチャされたファイルをカスタマイズできます。 この変数を "Simple" に設定した場合、標準の USMT 構成ファイルのみ使用されます。 この変数を "Advanced" に設定した場合、タスク シーケンス変数 OSDMigrateConfigFiles により、USMT が使用する構成ファイルが指定されます。<br /><br /> 有効な値:<br /><br /> **"Simple"**<br /><br /> **"Advanced"**|  
|OSDMigrateConfigFiles<br /><br /> (入力)|ユーザー プロファイルのキャプチャの制御に使用される構成ファイルを指定します。 この変数は、OSDMigrateMode が "Advanced" に設定されている場合のみ使用されます。 カスタマイズされたユーザー プロファイル移行を実行するためには、このカンマ区切りの一覧の値を設定します。<br /><br /> 例: miguser.xml,migsys.xml,migapps.xml|  
|OSDMigrateContinueOnLockedFiles<br /><br /> (入力)|一部のファイルをキャプチャできない場合も、ユーザー状態のキャプチャを続行できます。<br /><br /> 有効な値:<br /><br /> **"TRUE"** (既定)<br /><br /> **"FALSE"**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (入力)|USMT の詳細ログ記録を有効にします。<br /><br /> 有効な値:<br /><br /> **"TRUE"**<br /><br /> **"FALSE"** (既定)|  
|OSDMigrateSkipEncryptedFiles<br /><br /> (入力)|暗号化ファイルをキャプチャするかどうかを指定します。<br /><br /> 有効な値:<br /><br /> **"TRUE"**<br /><br /> **"FALSE"** (既定)|  
|_OSDMigrateUsmtPackageID<br /><br /> (入力)|USMT ファイルを含む Configuration Manager パッケージのパッケージ ID を指定します。 この変数は必須です。|  

###  <a name="BKMK_CaptureWindowsSettings"></a> Windows 設定のキャプチャ タスク シーケンス アクション変数  
 このアクションの変数では、コンピューター名、登録組織名、タイム ゾーン情報などの特定の Windows 設定を対象のコンピューターに移行するかどうかを指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Capture Windows Settings](task-sequence-steps.md#BKMK_CaptureWindowsSettings)」 (Windows 設定のキャプチャ) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDMigrateComputerName<br /><br /> (入力)|コンピューター名を移行するかどうかを指定します。<br /><br /> 有効な値:<br /><br /> **"TRUE"** (既定)<br /><br /> **"FALSE"**<br /><br /> この値が "true" の場合、変数 OSDComputerName がコンピューターの NetBIOS 名に設定されます。|  
|OSDComputerName<br /><br /> (出力)|コンピューターの NetBIOS 名に設定します。 この値は、変数 OSDMigrateComputerName が "true" の場合のみ設定されます。|  
|OSDMigrateRegistrationInfo<br /><br /> (入力)|コンピューターのユーザー情報と組織情報を移行するかどうかを指定します。<br /><br /> 有効な値:<br /><br /> **"TRUE"** (既定)<br /><br /> **"FALSE"**<br /><br /> この値が "true," の場合、変数 OSDRegisteredOrgName がコンピューターの登録組織名に設定されます。|  
|OSDRegisteredOrgName<br /><br /> (出力)|コンピューターの登録組織名に設定します。 この値は、変数 OSDMigrateRegistrationInfo が "true" の場合のみ設定されます。|  
|OSDMigrateTimeZone<br /><br /> (入力)|コンピューターのタイム ゾーンを移行するかどうかを指定します。<br /><br /> 有効な値:<br /><br /> **"TRUE"** (既定)<br /><br /> **"FALSE"**<br /><br /> この値が "true" の場合、変数 OSDTimeZone がコンピューターのタイム ゾーンに設定されます。|  
|OSDTimeZone<br /><br /> (出力)|コンピューターのタイム ゾーンに設定します。 この値は、変数 OSDMigrateTimeZone が "true" の場合のみ設定されます。|  

###  <a name="BKMK_ConnecttoNetworkFolder"></a> ネットワーク フォルダーへの接続タスク シーケンス アクション変数  
 このアクションの変数では、ネットワーク フォルダーへの接続に使用するアカウントとパスワード、フォルダーのドライブ文字、フォルダーへのパスなどの、ネットワーク上のフォルダーに関する情報を指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Connect To Network Folder](task-sequence-steps.md#BKMK_ConnectToNetworkFolder)」 (ネットワーク フォルダーに接続) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|SMSConnectNetworkFolderAccount<br /><br /> (入力)|ネットワーク共有に接続するために使用する管理者アカウントを指定します。|  
|SMSConnectNetworkFolderDriveLetter<br /><br /> (入力)|接続先のネットワーク ドライブ文字を指定します。 この値は省略可能です。指定しない場合、ネットワーク接続はドライブ文字にマップされません。 値を指定する場合は、D: から Z: の範囲で指定する必要があります。  また、X: は使用しないでください。X: は、Windows PE 段階で Windows PE によって使用されるドライブ文字です。<br /><br /> 例:<br /><br /> **"D:"**<br /><br /> **"E:"**|  
|SMSConnectNetworkFolderPassword<br /><br /> (入力)|ネットワーク共有に接続するために使用するネットワーク パスワードを指定します。|  
|SMSConnectNetworkFolderPath<br /><br /> (入力)|接続に使用するネットワーク パスを指定します。<br /><br /> 例:<br /><br /> **"\\\サーバー名\共有名"**|  

###  <a name="BKMK_ConvertDisk"></a> ディスクをダイナミックに変換タスク シーケンス アクション変数  
 このアクションの変数では、ベーシック ディスクからダイナミック ディスクに変換する物理ディスクの番号を指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Convert Disk to Dynamic](task-sequence-steps.md#BKMK_ConvertDisktoDynamic)」 (ダイナミック ディスクに変換) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDConvertDiskIndex<br /><br /> (入力)|変換する物理ディスクの番号を指定します。|  

###  <a name="BKMK_EnableBitLocker"></a> BitLocker の有効化タスク シーケンス アクション変数  
 このアクションの変数では、対象のコンピューターで BitLocker を有効にするために使用する、回復パスワード オプションとスタートアップ キー オプションを指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Enable BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker)」 (BitLocker の有効化) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDBitLockerRecoveryPassword<br /><br /> (入力)|[BitLocker の有効化 **** ] タスク シーケンス アクションは、ランダムな回復パスワードを生成する代わりに、指定された値を回復パスワードとして使用します。 有効な数値の BitLocker 回復パスワードを指定する必要があります。|  
|OSDBitLockerStartupKey<br /><br /> (入力)|[**BitLocker の有効化**] タスク シーケンス アクションは、キー管理オプション [**USB 上のスタートアップ キーのみ** ] のランダムなスタートアップ キーを生成する代わりに、信頼されたプラットフォーム モジュール (TPM) をスタートアップ キーとして使用します。 有効な 256 ビット の Base64 エンコードされた BitLocker スタートアップ キーを指定する必要があります。|  

###  <a name="BKMK_FormatPartitionDisk"></a> ディスクのフォーマットとパーティション作成タスク シーケンス アクション変数  
 このアクションの変数では、ディスク番号やパーティション設定の配列などの、物理ディスクをフォーマットおよびパーティション作成するための情報を指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Format and Partition Disk](task-sequence-steps.md#BKMK_FormatandPartitionDisk)」 (ディスクのフォーマットとパーティション作成) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDDiskIndex<br /><br /> (入力)|パーティションを作成する物理ディスク番号を指定します。|  
|OSDDiskpartBiosCompatibilityMode<br /><br /> (入力)|特定の種類の BIOS との互換性を保つため、ハード ディスクのパーティションを作成するときに、キャッシュ整合の最適化を無効にするかどうかを指定します。 これは、Windows XP または Windows Server 2003 オペレーティング システムの展開時に必要になることがあります。 詳細については、Microsoft サポート技術情報の [記事 931760](http://go.microsoft.com/fwlink/?LinkId=134081) および [記事 931761](http://go.microsoft.com/fwlink/?LinkId=134082) を参照してください。<br /><br /> 有効な値:<br /><br /> **"TRUE"**<br /><br /> **"FALSE"** (既定)|  
|OSDGPTBootDisk<br /><br /> (入力)|EFI ベース コンピューターで EFI パーティションをスタートアップ ディスクとして使用できるように、GPT ハード ディスクに EFI パーティションを作成するかどうかを指定します。<br /><br /> 有効な値:<br /><br /> **"TRUE"**<br /><br /> **"FALSE"** (既定)|  
|OSDPartitions<br /><br /> (入力)|パーティション設定の配列を指定します。タスク シーケンス環境で配列変数にアクセスする方法については、SDK のトピックを参照してください。<br /><br /> このタスク シーケンス変数は、配列変数です。 配列内の各要素は、ハード ディスクの単一パーティションの設定を表します。 各パーティションに定義された設定にアクセスするには、配列変数名にゼロから始まるディスク パーティション番号とプロパティ名を結合します。<br /><br /> たとえば次の変数名は、このタスク シーケンス アクションによってハード ディスクに作成される最初のパーティションに対して、プロパティを定義するときに使用できます。<br /><br /> - **OSDPartitions0Type** - パーティションの種類を指定します。 このプロパティは必須です。 有効な値は、"**Primary**"、"**Extended**"、"**Logical**"、および "**Hidden**" です。<br />-   **OSDPartitions0FileSystem** - パーティションをフォーマットするときに使用するファイル システムの種類を指定します。 このプロパティは省略可能です。ファイル システムを指定しない場合、パーティションはフォーマットされません。 有効な値は、"**FAT32**" および "**NTFS**" です。<br />-   **OSDPartitions0Bootable** - パーティションが起動可能かどうかを指定します。 このプロパティは必須です。 MBR ディスクでこの値が "**TRUE**" に設定されると、アクティブなパーティションが作成されます。<br />-   **OSDPartitions0QuickFormat** - 使用されるフォーマットの種類を指定します。 このプロパティは必須です。 この値が "**TRUE**" に設定されると、クイック フォーマットが実行され、それ以外の場合は完全フォーマットが実行されます。<br />-   **OSDPartitions0VolumeName** - フォーマット時にボリュームに割り当てられる名前を指定します。 このプロパティは省略可能です。<br />-   **OSDPartitions0Size** - パーティションのサイズを指定します。 単位は **OSDPartitions0SizeUnits** 変数で指定します。 このプロパティは省略可能です。 このプロパティを指定しない場合、残りの空き領域すべてを使用してパーティションが作成されます。<br />-   **OSDPartitions0SizeUnits** - **OSDPartitions0Size** タスク シーケンス 変数の解釈時に使用される単位を指定します。 このプロパティは省略可能です。 有効な値は、"**MB**" (既定)、"**GB**"、および "**Percent**" です。<br />-   **OSDPartitions0VolumeLetterVariable** - パーティションのドライブ文字は、パーティションの作成時に Windows PE で次に利用可能なドライブ文字が常に使用されます。 この省略可能なプロパティを使用すると、別のタスク シーケンス変数の名前を指定し、そのシーケンス変数を新しいドライブ文字の将来使う場合に備え保存するときに使うことができます。<br /><br /> <br /><br /> このタスク シーケンス アクションで複数のパーティションが定義される場合、2 番目のパーティションのプロパティを定義するには、そのインデックスを変数名で使用します。たとえば、 **OSDPartitions1Type**、 **OSDPartitions1FileSystem**、 **OSDPartitions1Bootable**、 **OSDPartitions1QuickFormat**、 **OSDPartitions1VolumeName** などのようになります。|  
|OSDPartitionStyle<br /><br /> (入力)|ディスクをパーティション分割するときに使用するパーティション スタイルを指定します。 "**MBR**" はマスター ブート レコードのパーティションの形式を、"**GPT**" は GUID パーティション テーブル形式を示します。<br /><br /> 有効な値:<br /><br /> **"GPT"**<br /><br /> **"MBR"**|  

###  <a name="BKMK_InstallSoftwareUpdates"></a> ソフトウェアの更新のインストール タスク シーケンス アクション変数  
 このアクションの変数では、すべての更新プログラムをインストールするのか、必須の更新プログラムのみインストールするのかを指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Install Software Updates](task-sequence-steps.md#BKMK_InstallSoftwareUpdates)」 (ソフトウェアの更新プログラムのインストール) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名<br /><br /> (入力)|説明|  
|----------------------------------------|-----------------|  
|SMSInstallUpdateTarget<br /><br /> (入力)|すべての更新プログラムをインストールするのか、必須の更新プログラムのみインストールするのかを指定します。<br /><br /> 有効な値:<br /><br /> **"All"**<br /><br /> **"Mandatory"**|  

###  <a name="BKMK_JoinDomainWorkgroup"></a> ドメインまたはワークグループへの参加タスク シーケンス アクション変数  
 このアクションの変数では、対象のコンピューターを Windows ドメインまたはワークグループに参加させるために必要な情報を指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Join Domain or Workgroup](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup)」 (ドメインまたはワークグループに参加) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDJoinAccount<br /><br /> (入力)|対象コンピューターを Windows ドメインに参加させるために使用するアカウントを指定します。 この変数はドメインに参加するときに必要になります。|  
|OSDJoinDomainName<br /><br /> (入力)|対象コンピューターを参加させる Windows ドメインの名前を指定します。 Windows ドメイン名の長さは 1 ～ 255 文字の範囲であることが必要です。|  
|OSDJoinDomainOUName<br /><br /> (入力)|対象コンピューターを参加させる組織単位 (OU) の RFC 1779 形式の名前を指定します。 指定する場合の値は、完全なパスを含む必要があります。 Windows ドメインの OU 名の長さは 0 ～ 32,767 文字の範囲であることが必要です。 OSDJoinType 変数が "1" (ワークグループに参加) に設定されている場合は、この値を設定しないでください。 ****<br /><br /> 例:<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDJoinPassword<br /><br /> (入力)|対象コンピューターを Windows ドメインに参加させるために使用するネットワーク パスワードを指定します。 変数が指定されていない場合は、空白のパスワードが試行されます。 **OSDJoinType** 変数が "**0**" (ドメインに参加) に設定されている場合は、この値が必要になります。|  
|OSDJoinSkipReboot<br /><br /> (入力)|対象コンピューターがドメインまたはワークグループに参加した後、再起動をするかどうかを指定します。<br /><br /> 有効な値:<br /><br /> **"TRUE"**<br /><br /> **"FALSE"**|  
|OSDJoinType<br /><br /> (入力)|対象コンピューターを Windows ドメインに参加させるか、ワークグループに参加させるかを指定します。 対象コンピューターを Windows ドメインに参加させる場合は、"0" を指定します。**** 対象コンピューターをワークグループに参加させる場合は、"1" を指定します。****<br /><br /> 有効な値:<br /><br /> **0**<br /><br /> **1**|  
|OSDJoinWorkgroupName<br /><br /> (入力)|対象コンピューターを参加させるワークグループの名前を指定します。 ワークグループ名の長さは 1 ～ 32 文字の範囲であることが必要です。<br /><br /> 例:<br /><br /> **"会計"**|  

###  <a name="BKMK_PrepareWindowsCapture"></a> Windows のキャプチャの準備タスク シーケンス アクション変数  
 このアクションの変数は、対象コンピューターから Windows オペレーティング システムをキャプチャするのに使用する情報を指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Prepare ConfigMgr Client for Capture](task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture)」 (ConfigMgr クライアントのキャプチャの準備) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDBuildStorageDriverList<br /><br /> (入力)|sysprep が大容量記憶装置のドライバー一覧を構築するかどうかを指定します。 この設定は、Windows XP および Windows Server 2003 にのみ適用されます。 これにより、sysprep.inf の [SysprepMassStorage] セクションに、キャプチャするイメージがサポートすべき大容量記憶装置のドライバーすべてに関する情報が入力されます。<br /><br /> 有効な値:<br /><br /> **"TRUE"**<br /><br /> **"FALSE"** (既定)|  
|OSDKeepActivation<br /><br /> (入力)|sysprep がプロダクト アクティベーション フラグをリセットするかどうかを指定します。<br /><br /> 有効な値:<br /><br /> **"TRUE"**<br /><br /> **"FALSE"** (既定)|  
|OSDTargetSystemRoot<br /><br /> (出力)|参照コンピューター上にインストールされたオペレーティング システムの Windows ディレクトリへのパスを指定します。 このオペレーティング システムは Configuration Manager によるキャプチャをサポートするオペレーティング システムとして検証済みです。|  

###  <a name="BKMK_ReleaseStateStore"></a> 状態ストアのリリース シーケンス アクション変数  
 このアクションの変数は、格納されたユーザー状態をリリースするのに使用する情報を指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Release State Store](task-sequence-steps.md#BKMK_ReleaseStateStore)」 (状態ストアのリリース) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (入力)|ユーザー状態の復元元となる場所への UNC またはローカル パス名。 この値は、**ユーザー状態のキャプチャ** タスク シーケンス アクションと**ユーザー状態の復元**タスク シーケンス アクションの両方で使用されます。|  

###  <a name="BKMK_RequestState"></a> 状態ストアの要求タスク シーケンス アクション変数  
 このアクションの変数は、ユーザー データが格納されている状態移行ポイント上のフォルダーのように、格納されたユーザー状態を要求するのに使用する情報を指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Release State Store](../../osd/understand/task-sequence-steps.md#BKMK_ReleaseStateStore)」 (状態ストアのリリース) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDStateFallbackToNAA<br /><br /> (入力)|コンピューター アカウントが状態移行ポイントへの接続に失敗したときに、その代替としてネットワーク アクセス アカウントを使用するかどうかを指定します。<br /><br /> 有効な値:<br /><br /> **"TRUE"**<br /><br /> **"FALSE"** (既定)|  
|OSDStateSMPRetryCount<br /><br /> (入力)|タスク シーケンス ステップが状態移行ポイントの検索を試行する回数を指定します。この回数を超えるとこの手順は失敗します。 回数は 0 ～ 600 の範囲で指定する必要があります。|  
|OSDStateSMPRetryTime<br /><br /> (入力)|タスク シーケンス ステップが再試行間に待機する秒数を指定します。 最大秒数は 30 文字です。|  
|OSDStateStorePath<br /><br /> (出力)|ユーザー状態が格納される状態移行ポイント上にあるフォルダーへの UNC パス。|  

###  <a name="BKMK_RestartComputer"></a> コンピューターの再起動タスク シーケンス アクション変数  
 このアクションの変数は、対象コンピューターを再起動するのに使用する情報を指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Restart Computer](task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer)」 (コンピューターの再起動) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|SMSRebootMessage<br /><br /> (入力)|対象コンピューターの再起動前にユーザーに表示されるメッセージを指定します。 この変数を設定しなかった場合、既定のメッセージ テキストが表示されます。 メッセージは、512 文字以内で指定する必要があります。<br /><br /> 例:<br /><br /> "このコンピューターは再起動されます。作業中のファイルを保存してください。"|  
|SMSRebootTimeout<br /><br /> (入力)|コンピューターが再起動される前にユーザーに警告を表示する秒数を指定します。 0 秒を指定すると、再起動されるというメッセージは表示されません。<br /><br /> 例:<br /><br /> **"0"** (既定)<br /><br /> **"5"**<br /><br /> **"10"**|  

###  <a name="BKMK_RestoreUserState"></a> ユーザー状態の復元 タスク シーケンス アクション変数  
 このアクションの変数は、ユーザー状態が復元されるフォルダーのパス名など、対象コンピューターのユーザー状態を復元するのに使用される情報を指定します。また、ローカル コンピューター アカウントを復元するかどうかも指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Restore User State](task-sequence-steps.md#BKMK_RestoreUserState)」 (ユーザー状態の復元) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (入力)|ユーザー状態の復元元となるフォルダーの UNC またはローカル パス名。|  
|OSDMigrateContinueOnRestore<br /><br /> (入力)|一部のファイルを復元できなくても、ユーザー状態の復元を続行するかどうかを指定します。<br /><br /> 有効な値:<br /><br /> **"TRUE"** (既定)<br /><br /> **"FALSE"**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (入力)|USMT ツールの詳細ログ記録を有効にします。 この値は、アクションに必要で、"TRUE" または "FALSE" に設定されている必要があります。<br /><br /> 有効な値:<br /><br /> **"TRUE"**<br /><br /> **"FALSE"** (既定)|  
|OSDMigrateLocalAccounts<br /><br /> (入力)|ローカル コンピューター アカウントを復元するかどうかを指定します。<br /><br /> 有効な値:<br /><br /> **"TRUE"**<br /><br /> **"FALSE"** (既定)|  
|OSDMigrateLocalAccountPassword<br /><br /> (入力)|**OSDMigrateLocalAccounts** 変数が TRUE の場合、この変数には移行されたすべてのローカル アカウントに割り当てるパスワードが含まれる必要があります。 移行されたすべてのローカル アカウントに同じパスワードが割り当てられるため、このパスワードは一時的なパスワードと考え、後で Configuration Manager オペレーティング システムの展開以外の方法で変更することをお勧めします。|  
|OSDMigrateAdditionalRestoreOptions<br /><br /> (入力)|ユーザー状態の復元時に使用する、追加のユーザー状態移行ツール (USMT) コマンド ライン オプションを指定します。 追加のオプションは、自動生成された USMT コマンド ラインに付加される文字列の形式で指定されます。 タスク シーケンスを実行するまで、このタスク シーケンス変数で指定される USMT オプションの正確性は検証されません。|  
|_OSDMigrateUsmtRestorePackageID<br /><br /> (入力)|USMT ファイルを含む Configuration Manager パッケージのパッケージ ID を指定します。 この変数は必須です。|  

###  <a name="BKMK_RunCommand"></a> コマンド ラインの実行タスク シーケンス アクション変数  
 このアクションの変数は、コマンドが実行される作業ディレクトリなど、コマンド ラインからコマンドを実行するのに使用する情報を指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Run Command Line](task-sequence-steps.md#BKMK_RunCommandLine)」 (コマンド ラインの実行) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名|説明|  
|--------------------------|-----------------|  
|SMSTSDisableWow64Redirection<br /><br /> (入力)|既定では、64 ビット オペレーティング システム上で実行するときは、コマンド ラインのプログラムは検索され、WOW64 ファイル システム リダイレクターを使用して実行されます。これは32 ビット バージョンのオペレーティング システムのプログラムや DLL が検出できるようにするためです。 この変数を "true" に設定すると、WOW64 ファイル システム リダイレクターの使用が無効になり、64 ビット バージョンのオペレーティング システムのプログラムや DLL が検出できます。 32 ビット オペレーティング システム上で実行している場合は、この変数は影響を及ぼしません。|  
|WorkingDirectory<br /><br /> (入力)|コマンド ラインのアクションの開始ディレクトリを指定します。 ディレクトリ名は、255 文字以内で指定する必要があります。<br /><br /> 次に例を示します。<br /><br /> -   **"C:\\"**<br />-   **"%SystemRoot%"**|  
|SMSTSRunCommandLineUserName<br /><br /> (入力)|コマンド ラインを実行するアカウントを指定します。 この値は、ユーザー名 または ドメイン\ユーザー名 という形式の文字列になります。|  
|SMSTSRunCommandLinePassword<br /><br /> (入力)|SMSTSRunCommandLineUserName 変数で指定されたアカウントのパスワードを指定します。|  

### <a name="set-dynamic-variables"></a>動的変数の設定  
 [動的変数の設定] タスク シーケンス ステップを追加すると、このアクションの変数が自動的に設定されます。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Set Dynamic Variables](task-sequence-steps.md#BKMK_SetDynamicVariables)」 (動的変数の設定) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名<br /><br /> (入力)|説明|  
|----------------------------------------|-----------------|  
|_SMSTSMake|コンピューターのメーカーを指定します。|  
|_SMSTSModel|コンピューターのモデルを指定します。|  
|_SMSTSMacAddresses|コンピューターで使用される MAC アドレスを指定します。|  
|_SMSTSIPAddresses|コンピューターで使用される IP アドレスを指定します。|  
|_SMSTSSerialNumber|コンピューターのシリアル番号を指定します。|  
|_SMSTSAssetTag|コンピューターの資産タグを指定します。|  
|_SMSTSUUID|コンピューターの UUID を指定します。|  
|_SMSTSDefaultGateways|コンピューターで使用される既定のゲートウェイを指定します。|  

###  <a name="BKMK_SetupWindows"></a> Windows と ConfigMgr のセットアップ タスク シーケンス アクション変数  
 このアクションの変数は、Configuration Manager クライアントをインストールするときに使用されるクライアント インストール プロパティを指定します。 これらの変数に関連するタスク シーケンス ステップの詳細については、「[Setup Windows and ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)」 (Windows と ConfigMgr のセットアップ) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名<br /><br /> (入力)|説明|  
|----------------------------------------|-----------------|  
|SMSClientInstallProperties<br /><br /> (入力)|Configuration Manager クライアントをインストールするときに使用するクライアント インストール プロパティを指定します。|  

### <a name="upgrade-operating-system"></a>オペレーティング システムのアップグレード  
 このアクションの変数では、Windows 10 へのアップグレードの際にセットアップに追加されるコマンド ライン オプションを指定します。これらのオプションは Configuration Manager コンソールでは使用できません。 この変数に関連するタスク シーケンス ステップの詳細については、「[Upgrade Operating System](task-sequence-steps.md#BKMK_UpgradeOS)」 (オペレーティング システムのアップグレード) を参照してください。  

#### <a name="details"></a>説明  

|アクション変数名<br /><br /> (入力)|説明|  
|----------------------------------------|-----------------|  
|OSDSetupAdditionalUpgradeOptions<br /><br /> (入力)|Windows 10 へのアップグレードの際にセットアップに追加されるコマンド ライン オプションを指定します。 これらのコマンド ライン オプションは検証されません。 したがって、入力したオプションが正しいことを確認してください。<br /><br /> 詳細については、「 [Windows セットアップ コマンド ライン オプション](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx)」を参照してください。|  

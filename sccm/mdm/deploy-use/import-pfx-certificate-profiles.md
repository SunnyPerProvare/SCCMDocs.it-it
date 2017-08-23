---
title: "証明書の詳細をインポートして PFX 証明書プロファイルを作成する | Microsoft Docs"
description: "System Center Configuration Manager で PFX ファイルを使用して暗号化されたデータ交換をサポートするユーザーに固有の証明書を生成する方法について説明します。"
ms.custom: na
ms.date: 04/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
caps.latest.revision: "5"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: c8346d04c7cd9761291824f5d30f09fab9acbcf9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-pfx-certificate-profiles-by-importing-certificate-details"></a>証明書の詳細をインポートして PFX 証明書プロファイルを作成する方法

*適用対象: System Center Configuration Manager (Current Branch)*


ここでは、外部証明書から資格情報をインポートして証明書プロファイルを作成する方法を説明します。  

[証明書プロファイル](../../protect/deploy-use/introduction-to-certificate-profiles.md)に関する記事には、証明書プロファイルの作成と構成に関する一般的な情報が記載されています。 このトピックでは、PFX 証明書に関連した証明書プロファイルの具体的な情報をいくつか取り上げます。

-  Configuration Manager は、さまざまなデバイスやオペレーティング システムに適した各種証明書ストアです。  次の設定があります。

 -   iOS と Mac OS/OS X
 -   Android と Android for Work
 -   Windows 10 (Windows 10 mobile を含む)

詳細については、「[System Center Configuration Manager での証明書プロファイルの前提条件](../../protect/plan-design/prerequisites-for-certificate-profiles.md)」を参照してください。

## <a name="pfx-certificate-profiles"></a>PFX 証明書プロファイル
System Center Configuration Manager では、証明書資格情報をインポートしてから、ユーザーのデバイスに Personal Information Exchange (.pfx) ファイルをプロビジョニングできます。 PFX ファイルを使用してユーザー固有の証明書を生成すると、データ交換の暗号化に対応できます。

> [!TIP]  
>  このプロセスの手順について説明したチュートリアルは、「 [Configuration Manager で PFX 証明書プロファイルを作成および展開する方法](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx)」に記載されています。  

## <a name="create-import-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Personal Information Exchange (PFX) 証明書プロファイルの作成、インポート、および展開  

### <a name="get-started"></a>作業開始

1.  System Center Configuration Manager コンソールで、[**資産とコンプライアンス**] をクリックします。  
2.  [ **資産とコンプライアンス** ] ワークスペースで、[ **コンプライアンス設定** ]、[ **会社のリソースへのアクセス** ] の順に展開してから、[ **証明書プロファイル** ] をクリックします。  

3.  [ **ホーム** ] タブの [ **作成** ] グループで、[ **証明書プロファイルの作成**] をクリックします。

4.  **[証明書プロファイルの作成]** ウィザードの **[全般]** ページで、次の情報を指定します。  

    -   **名前**: 証明書プロファイルの固有な名前を入力します。 最大 256 文字を使用できます。  

    -   **説明**: System Center Configuration Manager コンソールで証明書プロファイルを区別しやすくなるように、簡単な説明と他の関連情報を入力します。 最大 256 文字を使用できます。  

    -   **[作成する証明書プロファイルの種類を指定します]**: PFX 証明書の場合、次のいずれかのオプションを選びます。  

        -   **Personal Information Exchange - PKCS #12 (PFX) 設定 -- インポート**: プログラムによって既存の証明書から情報をインポートして、証明書プロファイルを作成します。  

        -   **Personal Information Exchange - PKCS #12 (PFX) 設定 - 作成**: 証明機関によって提供された資格情報を使用して、PFX 証明書プロファイルを作成します。  詳細については、「[System Center Configuration Manager で PFX 証明書プロファイルを作成する方法](../../mdm/deploy-use/create-pfx-certificate-profiles.md)」を参照してください。


### <a name="create-a-pfx-certificate-profile-for-the-imported-credentials"></a>インポートされた資格情報に PFX 証明書プロファイルを作成する

PFX 証明書をインポートするには、Configuration Manager SDK を使用して PFX 作成スクリプトを展開します。 

インポートした証明書は、後で登録済みデバイスに展開されます。

1. **証明書プロファイルの作成ウィザード**の **[PFX 証明書]** ページで、デバイス キーの記憶域プロバイダーの場所を指定します。
    -   **トラステッド プラットフォーム モジュール (TPM) にインストールする (存在する場合)**  
    -   **トラステッド プラットフォーム モジュール (TPM) にインストールする (それ以外は失敗)** 
    -   **Windows Hello for Business にインストールする (それ以外は失敗)** 
    -   **ソフトウェア キー記憶域プロバイダーにインストールする** 
2. **[次へ]**をクリックします。 
3. ウィザードの **[サポートされているプラットフォーム]** ページで、サポートされているデバイス プラットフォームを選択してから、**[次へ]** をクリックします。

### <a name="finish-the-profile"></a>プロファイルを完了する

1.  **[次へ]**をクリックし、 **[概要]** ページを確認してウィザードを終了します。  
2.  現在、PFX ファイルを含む証明書プロファイルは **[証明書プロファイル]** ワークスペースから取得できます。 
3.  プロファイルを展開するには、**[資産とコンプライアンス]** ワークスペースで、**[コンプライアンス設定]** > **[会社のリソースへのアクセス]** > **[証明書プロファイル]** の順に開き、証明書を右クリックして、**[展開]** をクリックします。 

### <a name="deploy-a-create-pfx-script"></a>PFX 作成スクリプトを展開する

[Configuration Manager SDK](http://go.microsoft.com/fwlink/?LinkId=613525) を使用して PFX 作成スクリプトを展開します。 

Configuration Manager 2012 SP2 に追加された PFX 作成スクリプトは、SDK に SMS_ClientPfxCertificate クラスを追加します。 このクラスには、次のメソッドが含まれています。  

    -   `ImportForUser`  

    -   `DeleteForUser`  

次の例では、資格情報を PFX 証明書プロファイルにインポートします。

``` powershell
    $EncryptedPfxBlob = "<blob>"  
    $Password = "abc"  
    $ProfileName = "PFX_Profile_Name"  
    $UserName = "ComputerName\Administrator"  

    #New pfx  
    $WMIConnection = ([WMIClass]"\\nksccm\root\SMS\Site_MDM:SMS_ClientPfxCertificate")  
        $NewEntry = $WMIConnection.psbase.GetMethodParameters("ImportForUser")  
        $NewEntry.EncryptedPfxBlob = $EncryptedPfxBlob  
        $NewEntry.Password = $Password  
        $NewEntry.ProfileName = $ProfileName  
        $NewEntry.UserName = $UserName  
    $Resource = $WMIConnection.psbase.InvokeMethod("ImportForUser",$NewEntry,$null)  
```  

この例を使用するには、次のスクリプト変数を更新します。  

   -   **blob**\ - PFX の base64 で暗号化された blob  
   -   **$Password** - PFX ファイルのパスワード  
   -   **$ProfileName** - PFX プロファイル名  
   -   **ComputerName** - ホスト コンピューター名   

## <a name="see-also"></a>関連項目
「[新しい証明書プロファイルを作成する](../../protect/deploy-use/create-certificate-profiles.md)」では、証明書プロファイルの作成ウィザードについて説明します。

[証明書の詳細をインポートして PFX 証明書プロファイルを作成する方法](../../mdm/deploy-use/create-pfx-certificate-profiles.md)

「[System Center Configuration Manager でのプロファイルの展開](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)」では、証明書プロファイルの展開について説明しています。
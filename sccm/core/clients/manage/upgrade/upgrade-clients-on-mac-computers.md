---
title: "macOS クライアントのアップグレード - Configuration Manager | Microsoft Docs"
description: "System Center Configuration Manager で Mac コンピューター上のクライアントをアップグレードします。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 74c60941-5eae-4905-9e58-252bdb39df96
caps.latest.revision: "10"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 502116b66fc14914ca0606ae416e82202824de7a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-upgrade-clients-on-mac-computers-in-system-center-configuration-manager"></a>System Center Configuration Manager で Mac コンピューター上のクライアントをアップグレードする方法

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager アプリケーションを使用して Mac コンピューター用のクライアントをアップグレードするには、次に説明する基本的な手順に従います。 または、Mac クライアントのインストール ファイルをダウンロードし、共有のネットワーク フォルダーまたは Mac コンピューターのローカル フォルダーにコピーして、手動でインストールするようにユーザーに指示することもできます。  

> [!NOTE]  
>  これらの手順を実行する前に、Mac コンピューターが前提条件を満たしていることをご確認ください。 「[Mac コンピューターでサポートされるオペレーティング システム](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers)」を参照してください。  

## <a name="step-1-download-the-latest-mac-client-installation-file-from-the-microsoft-download-center"></a>手順 1: Microsoft ダウンロード センターから最新の Mac クライアント インストール ファイルをダウンロードする  
 Configuration Manager 用の Mac クライアントは、Configuration Manager インストール メディアに含まれていません。Microsoft ダウンロード センターからダウンロードする必要があります。 Mac クライアントのインストール ファイルは、ConfigmgrMacClient.msi という Windows インストーラー ファイルに含まれています。  

 このファイルは、 [Microsoft ダウンロード センター](http://go.microsoft.com/fwlink/p/?LinkId=525184)からダウンロードできます。  

## <a name="step-2-run-the-downloaded-installation-file-to-create-the-mac-client-installation-file"></a>手順 2: ダウンロードしたインストール ファイルを実行して Mac クライアント インストール ファイルを作成する  
 Windows を実行するコンピューターで、ダウンロードした **ConfigmgrMacClient.msi** を実行して、 **Macclient.dmg**という Mac クライアント インストール ファイルをアンパックします。 このファイルは、Windows コンピューターの既定で **C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client** フォルダーにアンパックされます。  

## <a name="step-3-extract-the-client-installation-files"></a>手順 3: クライアント インストール ファイルを抽出する  
 Macclient.dmg ファイルをネットワーク共有または Mac コンピューターのローカル フォルダーにコピーします。 次に、Mac コンピューターから、Macclient.dmg ファイルをマウントして開き、Mac コンピューターのフォルダーにコピーします。  

## <a name="step-4-create-a-cmmac-file-that-can-be-used-to-create-an-application"></a>手順 4: アプリケーションの作成に使用できる .cmmac ファイルを作成する  

1.  **CMAppUtil** ツール (Mac クライアント インストール ファイルの **Tools** フォルダーにあります) を使用して、クライアント インストール パッケージから .cmmac ファイルを作成します。 このファイルは Configuration Manager アプリケーションの作成に使用されます。  

2.  新しいファイル **CMClient.pkg.cmmac** を、Configuration Manager コンソールを実行しているコンピューターから使用できる場所にコピーします。  

 詳細については、「[Mac コンピューターのアプリケーションを作成および展開するための補足手順](/sccm/apps/get-started/creating-mac-computer-applications#supplemental-procedures-to-create-and-deploy-applications-for-mac-computers)」を参照してください。  

## <a name="step-5-create-and-deploy-an-application-containing-the-mac-client-files"></a>**手順 5:** Mac クライアント ファイルを含むアプリケーションを作成および展開する  

1.  Configuration Manager コンソールで、クライアント インストール ファイルを含む **CMClient.pkg.cmmac** ファイルからアプリケーションを作成します。  

2.  このアプリケーションを階層内の Mac コンピューターに展開します。  

 詳細については、「[System Center Configuration Manager での Mac コンピューター アプリケーションの作成](../../../../apps/get-started/creating-mac-computer-applications.md)」を参照してください。  

## <a name="step-6-users-install-the-latest-client"></a>手順 6: ユーザーが最新のクライアントをインストールする  
 Mac クライアントのユーザーに、Configuration Manager クライアントの更新プログラムを使用可能であり、インストールする必要がある、というメッセージが表示されます。 ユーザーは、クライアントをインストールした後に Mac コンピューターを再起動する必要があります。  

 コンピューターを再起動すると、コンピューターの登録ウィザードが自動的に実行され、新しいユーザー証明書が要求されます。  

 Configuration Manager の登録を使用せず、Configuration Manager とは独立したクライアント証明書をインストールする場合は、「[アップグレードしたクライアントが既存の証明書を使用するように構成する](#BKMK_UpgradingClient_MachineEnrollment)」を参照してください。  

##  <a name="BKMK_UpgradingClient_MachineEnrollment"></a> Configure the upgraded client to use an existing certificate  
 次の手順に従って、コンピューターの登録ウィザードの実行を回避し、アップグレードしたクライアントが既存のクライアント証明書を使用するように構成します。  

-   Configuration Manager コンソールで、種類が **[Mac OS X]** の構成項目を作成します。  

-   [ **スクリプト** ] という設定の種類を使用して、この構成項目に設定を追加します。  

-   次のスクリプトを設定に追加します。  

    ```  
    #!/bin/sh  
    echo "Starting script\n"  
    echo "Changing directory to MAC Client\n"  
    cd /Users/Administrator/Desktop/'MAC Client'/  
    echo "Import root cert\n"  
    /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/Root.pfx -A -k /Library/Keychains/System.Keychain -P ROOT  
    echo "Using openssl to convert pfx to a crt\n"  
    /usr/bin/sudo openssl pkcs12 -in /Users/Administrator/Desktop/'MAC Client'/Root.pfx -out Root1.crt -nokeys -clcerts -passin pass:ROOT  
    echo "Adding trust to root cert\n"  
    /usr/bin/sudo /usr/bin/security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.Keychain Root1.crt  
    echo "Import client cert\n"  
    /usr/bin/sudo /usr/bin/security import /Users/Administrator/Desktop/'MAC Client'/MacClient.pfx -A -k /Library/Keychains/System.Keychain -P MAC  
    echo "Executing ccmclient with MP\n"  
    sudo ./ccmsetup -MP https://SCCM34387.SCCM34387DOM.NET/omadm/cimhandler.ashx  
    echo "Editing Plist file\n"  
    sudo /usr/libexec/Plistbuddy -c 'Add:SubjectName string CMMAC003L' /Library/'Application Support'/Microsoft/CCM/ccmclient.plist  
    echo "Changing directory to CCM\n"  
    cd /Library/'Application Support'/Microsoft/CCM/  
    echo "Making connection to the server\n"  
    sudo open ./CCMClient  
    echo "Ending Script\n"  
    exit  

    ```  

-   構成項目を構成基準に追加し、Configuration Manager とは独立して証明書をインストールする構成基準をすべての Mac コンピューターに展開します。  

 Mac コンピューター用の構成項目を作成し、展開する方法の詳細については、「[System Center Configuration Manager クライアントを使用して管理されている Mac OS X デバイスの構成項目を作成する方法](../../../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md)」と「[System Center Configuration Manager で構成基準を展開する方法](../../../../compliance/deploy-use/deploy-configuration-baselines.md)」を参照してください。  

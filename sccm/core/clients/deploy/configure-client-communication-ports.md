---
title: "クライアント通信ポートを構成する | Microsoft Docs"
description: "System Center Configuration Manager でクライアント通信ポートを設定します。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 406bbdbf-ab4a-4121-a68b-154f96ea14ec
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstack
ms.author: robstackmsft
manager: angrobe
ms.openlocfilehash: 63e033fdb436930ac5f37e7408ca9292bc444560
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-client-communication-ports-in-system-center-configuration-manager"></a>System Center Configuration Manager でのクライアント通信ポートの構成方法

*適用対象: System Center Configuration Manager (Current Branch)*

通信に HTTP および HTTPS を使用するサイト システムとの通信で System Center Configuration Manager クライアントが使用する要求ポート番号は変更できます。 HTTP または HTTPS は、既にファイアウォール用に構成されている可能性が高いのですが、HTTP または HTTPS を使用するクライアント通知は、カスタムのポート番号を使用する場合よりも、管理ポイント コンピューターに必要な CPU 使用量とメモリが増えます。 従来のウェイクアップ パケットを使用してクライアントを起動するときに使用する、サイトのポート番号を指定することもできます。  

 HTTP および HTTPS の要求ポートを指定する場合は、既定のポート番号と代替のポート番号の両方を指定できます。 既定のポートで通信が失敗すると、クライアントは自動的に代替のポートを試します。 HTTP および HTTPS によるデータ通信の設定を指定できます。  

 クライアントの要求ポートの既定値は、HTTP トラフィック用が **80** 、HTTPS トラフィック用が **443** です。 変更するのは、これらの既定の値を使用しない場合に限定してください。 通常、IIS で既定の Web サイトではないカスタム Web サイトを使用する場合に、カスタム ポートを使います。 IIS の既定の Web サイトの既定のポート番号を変更し、他のアプリケーションも既定の Web サイトを使用している場合、それらのアプリケーションはエラーになる可能性があります。  

> [!IMPORTANT]  
>  Configuration Manager でポート番号を変更する場合は、その結果を検討してからにしてください。 次に例を示します。  
>   
>  -   サイトの構成としてクライアント要求サービスのポート番号を変更し、既存のクライアントが新しいポート番号を使用するように再構成されていない場合、これらのクライアントは管理されていない状態になります。  
> -   既定以外のポート番号を構成する前に、ファイアウォールおよび介在するすべてのネットワーク デバイスがこの構成をサポートできることを確認し、必要に応じて再構成します。 インターネット上でクライアントを管理し、既定の HTTPS ポート番号 443 を変更する場合、インターネット上のルーターおよびファイアウォールがこの通信をブロックする可能性があります。  

 要求ポート番号を変更した後にクライアントが管理されていない状態にならないようにするには、新しい要求ポート番号を使用するようにクライアントを構成する必要があります。 プライマリ サイトで要求ポートを変更すると、接続されたセカンダリ サイトは自動的に同じポート構成を継承します。 このトピックの手順に従って、プライマリ サイトで要求ポートを構成します。  

> [!NOTE]  
>  Linux と UNIX を実行しているコンピューター上のクライアントに要求ポートを構成する方法については、「[Linux および UNIX 用のクライアントの要求ポートを構成します。](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigLnUClientCommuincations)」をご覧ください。  

 Configuration Manager サイトが Active Directory Domain Services に発行されている場合、この情報にアクセスできる新しいクライアントおよび既存のクライアントは自動的にサイト ポート設定で構成されます。それ以上ユーザーが対処する必要はありません。 Active Directory Domain Services に発行されたこの情報にアクセスできないクライアントには、ワークグループ クライアント、別の Active Directory フォレストのクライアント、インターネット専用に構成されたクライアント、および現在インターネット上にあるクライアントが含まれます。 これらのクライアントをインストールした後で既定のポート番号を変更する場合は、次のいずれかの方法を使用してクライアントを再インストールし、新しいクライアントも同様にインストールします。  

-   クライアント プッシュ インストール ウィザードを使用して、クライアントを再インストールします。 クライアント プッシュ インストールでは、自動的に現在のサイト ポート構成でクライアントを構成します。 クライアント プッシュ インストール ウィザードの使用法の詳細については、「[クライアント プッシュを使用した Configuration Manager クライアントのインストール方法](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush)」をご覧ください。  

-   CCMHTTPPORT および CCMHTTPSPORT の CCMSetup.exe と client.msi のインストールのプロパティを使用して、クライアントを再インストールします。 これらのプロパティの詳細については、「[System Center Configuration Manager のクライアント インストール プロパティについて](../../../core/clients/deploy/about-client-installation-properties.md)」を参照してください。  

-   Active Directory Domain Services で Configuration Manager クライアント インストールのプロパティを検索する方法を使用して、クライアントを再インストールします。 詳細については、「[System Center Configuration Manager で Active Directory ドメイン サービスに発行されたクライアント インストールのプロパティについて](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md)」を参照してください。  

 既存のクライアントのポート番号を再構成する場合は、SMSSETUP\Tools\PortConfiguration フォルダーにあるインストール メディアと共に提供されるスクリプト PORTSWITCH.VBS も使用できます。  

> [!IMPORTANT]  
>  現在インターネット上にある既存のクライアントおよび新しいクライアントについては、CCMHTTPPORT および CCMHTTPSPORT の CCMSetup.exe client.msi プロパティを使用して、既定以外のポート番号を構成する必要があります。  

 サイトの要求ポートを変更した後に、サイト全体のクライアント プッシュ インストール方法を使用してインストールした新しいクライアントは、サイトの現在のポート番号で自動的に構成されます。  

#### <a name="to-configure-the-client-communication-port-numbers-for-a-site"></a>サイトのクライアント通信のポート番号を構成するには  

1.  Configuration Manager コンソールで、[ **管理**] をクリックします。  

2.  **管理**  ワークスペースで、展開 **サイトの構成**, 、 をクリックして **サイト**, 、し構成するプライマリ サイトを選択します。  

3.  [ **ホーム** ] タブで、[ **プロパティ**] をクリックしてから、[ **ポート** ] タブをクリックします。  

4.  いずれかの項目を選択し、[ **プロパティ** ] アイコンをクリックして、[ポートの詳細] ダイアログ ボックスを表示します。  

5.  [ **ポートの詳細** ] ダイアログ ボックスで、ポート番号と項目の説明を指定してから、[ **OK**] をクリックします。  

6.  IIS を実行するサイト システムの **SMSWeb** のカスタム Web サイト名を使用する場合は、[ **カスタム Web サイトを使用する** ] を選択します。  

7.  [ **OK** ] をクリックして、サイトの [プロパティ] ダイアログ ボックスを閉じます。  

 階層内のすべてのプライマリ サイトで、この手順を繰り返します。

---
title: "System Center Configuration Manager で VPN プロファイルを作成する方法 | Microsoft Docs"
description: "System Center Configuration Manager で VPN プロファイルを作成する方法を説明します。"
ms.custom: 
ms.date: 4/19/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
caps.latest.revision: "15"
author: lleonard-msft
caps.handback.revision: "0"
ms.author: alleonar
ms.manager: angrobe
ms.openlocfilehash: 359fcfd9754fb5c81763bc44cac45376ea3ab0b8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-vpn-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager で VPN プロファイルを作成する方法

*適用対象: System Center Configuration Manager (Current Branch)*

さまざまなデバイス プラットフォームで使用可能な接続の種類については、「[System Center Configuration Manager の VPN プロファイル](../../protect/deploy-use/vpn-profiles.md)」を参照してください。  

サード パーティの VPN 接続の場合は、VPN プロファイルを展開する前に VPN アプリを配布します。 アプリを展開しないと、ユーザーが VPN に接続しようとしたときに、アプリを展開するように求められます。 アプリの展開方法については、「[System Center Configuration Manager でアプリケーションを展開する方法](../../apps/deploy-use/deploy-applications.md)」を参照してください。

### <a name="create-a-vpn-profile"></a>VPN プロファイルの作成   

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[コンプライアンス設定]** > **[会社のリソースへのアクセス]** > **[VPN プロファイル]** の順に選択します。  

3.  **[ホーム]** タブの **[作成]** グループで、**[VPN プロファイルの作成]** を選択します。  


1.  **[全般]** ページに入力します。 」を参照し、次のことに注意してください。  

    - VPN プロファイル名には、\\/:*?&lt;>&#124; などの文字や空白文字は使用しないでください。 Windows Server VPN プロファイルでは、これらの文字はサポートされていません。  

     -   **[ファイルから既存の VPN プロファイルの項目をインポートする]** を選択し、XML ファイルにエクスポートされた VPN プロファイルの情報をインポートします (Windows 8.1 および Windows RT のみ)。  

1.  **[接続]** ページで、次のように指定します。  

    -   **接続の種類**: VPN 接続の種類を選択します。 次の表にある接続の種類から選択できます。  

    -   **サーバーの一覧**: VPN 接続に使用する新しいサーバーを追加します。 接続の種類によっては、1 つ以上の VPN サーバーを追加して、既定のサーバーを指定することもできます。  

        > [!NOTE]  
        >  iOS を実行するデバイスは、複数の VPN サーバーの使用をサポートしていません。 複数の VPN サーバーを構成して VPN プロファイルを iOS デバイスに展開すると、既定のサーバーだけが使用されます。  

     次の表に、接続の種類のオプションを示します。 詳細については、VPN サーバーのマニュアルを参照してください。

| &nbsp;&nbsp;オプション&nbsp;&nbsp; | 説明 | &nbsp;&nbsp;接続の&nbsp;種類&nbsp;&nbsp; |  
|----------------|----------------------|---------------------|  
|**領域**     |使用する認証領域です。 認証領域とは、"Pulse Secure" 接続の種類で使用される認証リソースのグループを表します。|Pulse Secure|    
|**ロール**        |この接続に対するアクセス権を持つユーザー ロールです。 |Pulse Secure|  
|**ログイン グループまたはドメイン** |接続するログイン グループまたはドメインの名前です。|Dell SonicWALL Mobile Connect|  
|**指紋**  |VPN サーバーが信頼できることを確認するために使用される文字列 ("Contoso 指紋コード" など) です。<br /><br /> 指紋:<br /><br /> - 指紋をクライアントに送信することにより、クライアントは、接続するときに同じ指紋を示すすべてのサーバーを信頼できます。<br /><br /> - デバイスにまだ指紋がない場合、指紋を表示すると共に、接続先の VPN サーバーを信頼するようにユーザーを促します (ユーザーは、手動で指紋を検証し、**[信頼する]** を選択して接続する必要があります)。|チェック ポイント モバイル VPN|  
|**VPN 接続を介してすべてのネットワーク トラフィックを送信する** |このオプションが選択されていない場合、( **Microsoft SSL (SSTP)**、 **Microsoft Automatic**、 **IKEv2**、 **PPTP** 、および **L2TP** の各接続の種類に対して) 接続の追加のルートを指定することができます。これを分割または VPN のトンネリングといいます。<br /><br /> 企業ネットワークへの接続だけが VPN トンネル経由で送信されます。 インターネット上のリソースに接続するときは、VPN トンネリングは使用されません。 |すべて|  
|**接続専用 DNS サフィックス** |接続専用のドメイン ネーム システム (DNS) サフィックスです。|- Microsoft SSL (SSTP)<br /><br /> - Microsoft 自動<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
|**企業の Wi-Fi ネットワークに接続しているときは VPN をバイパスする**  |デバイスが企業の Wi-Fi ネットワークに接続されている場合、VPN 接続は使用されません。|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - チェック ポイント モバイル VPN<br /><br /> - Microsoft SSL (SSTP)<br /><br /> - Microsoft 自動<br /><br /> - IKEv2<br /><br /> - L2TP|  
|**家庭の Wi-Fi ネットワークに接続しているときは VPN をバイパスする**  |デバイスが家庭の Wi-Fi ネットワークに接続されている場合、VPN 接続は使用されません。|すべて|  
|**アプリ VPN ごと (iOS 7 以降、Mac OS X 10.9 以降)** |VPN 接続を iOS アプリに関連付けて、アプリを実行すると接続が開かれるようにします。 アプリを展開するときに VPN プロファイルをアプリに関連付けることができます。|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - チェック ポイント モバイル VPN|  
|**カスタム XML (省略可能)** |VPN 接続を構成するカスタムの XML コマンドを指定します。<br /><br /> 例:<br /><br /> **Pulse Secure**の場合:<br /><br /> **&lt;pulse-schema><br /> &nbsp; &lt;isSingleSignOnCredential>true&lt;/isSingleSignOnCredential\><br />&lt;/pulse-schema>**<br /><br /> **チェックポイント モバイル VPN**の場合:<br /><br /> **&lt;CheckPointVPN <br /> &nbsp; port="443" name="CheckPointSelfhost" <br /> &nbsp; sso="true" <br /> &nbsp; debug="3"<br />/>**<br /><br /> **Dell SonicWALL Mobile Connect**の場合:<br /><br /> **&lt;MobileConnect\><br />&nbsp; &nbsp; &lt;Compression\>false&lt;/Compression\><br />&nbsp; &nbsp; &lt;debugLogging\>True&lt;/debugLogging\><br />&nbsp; &nbsp; &lt;packetCapture\>False&lt;/packetCapture\><br />&lt;/MobileConnect\>**<br /><br /> **F5 Edge Client**の場合:<br /><br /> **&lt;f5-vpn-conf>&lt;single-sign-on-credential>&lt;/f5-vpn-conf>**<br /><br /> カスタムの XML コマンドの記述方法については、各製造元の VPN に関するマニュアルを参照してください。|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - チェック ポイント モバイル VPN|  

> [!NOTE]  
>  モバイル デバイスの VPN プロファイルの作成に特化した情報については、[VPN プロファイルの作成](../../mdm/deploy-use/create-vpn-profiles.md)に関する記事を参照してください。  

ウィザードを完了します。 新しい VPN プロファイルは、[資産とコンプライアンス **** ] ワークスペースの [VPN プロファイル **** ] ノードに表示されます。

### <a name="next-steps"></a>次のステップ

- サード パーティの VPN 接続の場合は、VPN プロファイルを展開する前に VPN アプリを配布します。 アプリを展開しないと、ユーザーが VPN に接続しようとしたときに、アプリを展開するように求められます。 アプリの展開方法については、「[System Center Configuration Manager でアプリケーションを展開する方法](../../apps/deploy-use/deploy-applications.md)」を参照してください。

- 「[System Center Configuration Manager でのプロファイルの展開](deploy-wifi-vpn-email-cert-profiles.md)」に記載されているとおりに、VPN プロファイルを展開します。  

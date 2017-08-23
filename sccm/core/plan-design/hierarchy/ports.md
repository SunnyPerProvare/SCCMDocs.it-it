---
title: "Configuration Manager で使用されるポート | Microsoft Docs"
description: "System Center Configuration Manager が接続に使用する必要なポートとカスタマイズ可能なポートについて説明します。"
ms.custom: na
ms.date: 3/20/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6777fb0-0754-4abf-8a1b-7639d23e9391
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 78caa69e10f5d386daab1e61e484d4d134469708
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="ports-used-in-system-center-configuration-manager"></a>System Center Configuration Manager で使用されるポート

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager は、分散クライアント/サーバー システムです。 Configuration Manager が分散であるということは、サイト サーバー、サイト システム、およびクライアントの間で接続を確立できることを意味します。 接続によっては、構成不可能なポートを使用する場合も、ユーザーが指定するカスタム ポートをサポートする場合もあります。 ファイアウォール、ルーター、プロキシ サーバー、IPsec など、何らかのポート フィルタリング テクノロジを使用する場合は、必要なポートが利用可能であることを確認する必要があります。  

> [!NOTE]  
>  SSL ブリッジを使用してインターネットベースのクライアントをサポートする場合は、特定の HTTP 動詞とヘッダーでファイアウォールの通過を許可することが必要になることもあります。   

 次に示すポートの一覧は、Configuration Manager で使用されるもので、Active Directory Domain Services のグループ ポリシー設定や Kerberos 認証など、標準の Windows サービスの情報は含まれていません。 Windows サーバーのサービスとポートの詳細については、「 [Windows サーバー システムのサービス概要およびネットワーク ポート要件](http://go.microsoft.com/fwlink/p/?LinkID=123652)」を参照してください。  

##  <a name="BKMK_ConfigurablePorts"></a> 構成できるポート  
 Configuration Manager では、次の種類の通信でポートを構成できます。  

-   アプリケーション カタログ Web サイト ポイントからアプリケーション カタログ Web サービス ポイントへの通信  

-   登録プロキシ ポイントから登録ポイントへの通信  

-   クライアントから IIS を実行するサイト システムへの通信  

-   クライアントからインターネットへの通信 (プロキシ サーバー設定として)  

-   ソフトウェアの更新ポイントからインターネットへの通信 (プロキシ サーバー設定として)  

-   ソフトウェアの更新ポイントから WSUS サーバーへの通信  

-   サイト サーバーからサイト データベース サーバーへの通信  

-   レポート サービス ポイント  

    > [!NOTE]  
    >  レポート サービス ポイントのサイト システムの役割に使用されるポートは、SQL Server Reporting Services で構成されます。 レポート サービス ポイントとの通信中に、Configuration Manager によりこれらのポートが使用されます。 IPsec ポリシーまたはファイアウォールの構成用に IP フィルターの情報を定義する各ポートを確認しておいてください。  

既定では、クライアントからサイト システムへの通信に使用する HTTP ポートは 80、既定の HTTPS ポートは 443 です。 クライアントとサイト システム間の HTTP または HTTPS 通信に使用するポートは、セットアップ中に変更することも、Configuration Manager サイトのサイト プロパティで変更することもできます。  

レポート サービス ポイントのサイト システムの役割に使用されるポートは、SQL Server Reporting Services で構成されます。 レポート サービス ポイントとの通信中に、Configuration Manager によりこれらのポートが使用されます。 IPsec ポリシーまたはファイアウォールの構成用に IP フィルターの情報を定義する場合に、各ポートを確認しておいてください。  

##  <a name="BKMK_NonConfigurablePorts"></a> 構成不可能なポート  
Configuration Manager では、次の種類の通信用にポートを構成することはできません。  

-   サイト間の通信  

-   サイト サーバーからサイト システムへの通信  

-   Configuration Manager コンソールから SMS プロバイダーへの通信  

-   Configuration Manager コンソールからインターネットへの通信  

-   クラウド サービスへの接続 (Microsoft Intune やクラウドベースの配布ポイントなど)  

##  <a name="BKMK_CommunicationPorts"></a> Configuration Manager クライアントとサイト システムで使用されるポート  
次のセクションでは、Configuration Manager で通信に使用されるポートについて詳しく説明します。 セクションのタイトルの矢印は、通信の方向を表します。  

-   -- > は、一方のコンピューターが通信を開始し、他方のコンピューターが常に応答する状態を示します  

-   &lt; -- > は、どちらのコンピューターからも通信を開始できる状態を示します  

###  <a name="BKMK_PortsAI"></a> 資産インテリジェンス同期ポイント -- > Microsoft  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS)|--|443|  

###  <a name="BKMK_PortsAI-to-SQL"></a> 資産インテリジェンス同期ポイント -- > SQL Server  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (注 2「**代替ポートを利用可能**」を参照)|  

###  <a name="BKMK_PortsAppCatalogService-SQL"></a> アプリケーション カタログ Web サービス ポイント -- > SQL Server  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (注 2「**代替ポートを利用可能**」を参照)|  

###  <a name="BKMK_PortsAppCatalogWebSitePoint_AppCatalogWebServicePoint"></a> アプリケーション カタログ Web サイト ポイント -- > アプリケーション カタログ Web サービス ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|ハイパーテキスト転送プロトコル (HTTP)|--|80 (注 2「**代替ポートを利用可能**」を参照)|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS)|--|443 (注 2「**代替ポートを利用可能**」を参照)|  

###  <a name="BKMK_PortsClient-AppCatalogWebsitePoint"></a> クライアント -- > アプリケーション カタログ Web サイト ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|ハイパーテキスト転送プロトコル (HTTP)|--|80 (注 2「**代替ポートを利用可能**」を参照)|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS)|--|443 (注 2「**代替ポートを利用可能**」を参照)|  

###  <a name="BKMK_PortsClient-ClientWakeUp"></a> クライアント -- &gt; クライアント  
 ウェイクアップ プロキシ用にクライアントを構成するときに、ウェイクアップ プロキシは、次の表に示すポートに加え、1 つのクライアントから別のクライアントに対して Internet Control Message Protocol (ICMP) のエコー要求メッセージも使用します。

この通信は、他のクライアント コンピューターがネットワークで起動しているかどうかを確認するために使用します。 ICMP は TCP/IP Ping コマンドとも呼ばれます。 ICMP には UDP または TCP プロトコル番号がないため、次の表には記載されていません。 ただし、サブネット内のこのようなクライアント コンピューターまたは介在するネットワーク デバイスに、ホストベースのファイアウォールがある場合、ウェイクアップ プロキシ通信が正常に実行されるように、そのファイアウォールで ICMP トラフィックを許可する必要があります。  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|Wake On LAN|9 (注 2「**代替ポートを利用可能**」を参照)|--|  
|ウェイクアップ プロキシ|25536 (注 2「**代替ポートを利用可能**」を参照)|--|  

###  <a name="BKMK_PortsClient-PolicyModule"></a> クライアント -- &gt; Configuration Manager ポリシー モジュール (ネットワーク デバイス登録サービス)  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|ハイパーテキスト転送プロトコル (HTTP)||80|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS)|--|443|  

###  <a name="BKMK_PortsClient-CloudDP"></a>クライアント -- > クラウドベースの配布ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS)|--|443|  

###  <a name="BKMK_PortsClient-DP"></a>クライアント -- > 配布ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|ハイパーテキスト転送プロトコル (HTTP)|--|80 (注 2「**代替ポートを利用可能**」を参照)|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS)|--|443 (注 2「**代替ポートを利用可能**」を参照)|  

###  <a name="BKMK_PortsClient-DP2"></a>クライアント -- > マルチキャスト向けに構成された配布ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|マルチキャスト プロトコル|63000-64000|--|  

###  <a name="BKMK_PortsClient-DP3"></a> クライアント -- > PXE 向けに構成された配布ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|動的ホスト構成プロトコル (DHCP)|67 および 68|--|  
|簡易ファイル転送プロトコル (TFTP)|69 (注 4「**簡易 FTP (TFTP) デーモン**」を参照)|--|  
|Boot Information Negotiation Layer (BINL)|4011|--|  

###  <a name="BKMK_PortsClient-FSP"></a> クライアント -- > フォールバック ステータス ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|ハイパーテキスト転送プロトコル (HTTP)|--|80 (注 2「**代替ポートを利用可能**」を参照)|  

###  <a name="BKMK_PortsClient-GCDC"></a> クライアント -- > グローバル カタログ ドメイン コントローラー  
 Configuration Manager クライアントは、ワークグループ コンピューターである場合やインターネットのみの通信用に構成されている場合、グローバル カタログ サーバーに接続しません。  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|グローバル カタログ LDAP|--|3268|  
|グローバル カタログ LDAP SSL|--|3269|  

###  <a name="BKMK_PortsClient-MP"></a> クライアント -- > 管理ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|クライアント通知 (代替で HTTP または HTTPS が使用される前の既定の通信)|--|10123 (注 2「**代替ポートを利用可能**」を参照)|  
|ハイパーテキスト転送プロトコル (HTTP)|--|80 (注 2「**代替ポートを利用可能**」を参照)|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS)|--|443 (注 2「**代替ポートを利用可能**」を参照)|  

###  <a name="BKMK_PortsClient-SUP"></a> クライアント -- > ソフトウェアの更新ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|ハイパーテキスト転送プロトコル (HTTP)|--|80 または 8530 (注 3「 **Windows Server Update Services**」を参照)|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS)|--|443 または 8531 (注 3「 **Windows Server Update Services**」を参照)|  

###  <a name="BKMK_PortsClient-SMP"></a> クライアント -- > 状態移行ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|ハイパーテキスト転送プロトコル (HTTP)|--|80 (注 2「**代替ポートを利用可能**」を参照)|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS)|--|443 (注 2「**代替ポートを利用可能**」を参照)|  
|サーバー メッセージ ブロック (SMB)|--|445|  

###  <a name="BKMK_PortsConsole-Client"></a> Configuration Manager コンソール -- > クライアント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|リモート コントロール (コントロール)|--|2701|  
|リモート アシスタンス (RDP および RTC)|--|3389|  

###  <a name="BKMK_PortsConsole-Internet"></a> Configuration Manager コンソール -- > インターネット  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|ハイパーテキスト転送プロトコル (HTTP)|--|80|  

###  <a name="BKMK_PortsConsole-RSP"></a> Configuration Manager コンソール -- > レポート サービス ポイント  


|説明|UDP|TCP|
|-----------------|---------|---------|   
|ハイパーテキスト転送プロトコル (HTTP)|--|80 (注 2「**代替ポートを利用可能**」を参照)|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS)|--|443 (注 2「**代替ポートを利用可能**」を参照)|  

###  <a name="BKMK_PortsConsole-Site"></a> Configuration Manager コンソール -- > サイト サーバー  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|RPC (プロバイダー システムを特定するための WMI への初期接続)|--|135|  

###  <a name="BKMK_PortsConsole-Provider"></a> Configuration Manager コンソール -- > SMS プロバイダー  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC (注 6「 **動的ポート**」を参照)|  

###  <a name="BKMK_PortsCertificateRegistationPoint_PolicyModule"></a> Configuration Manager ポリシー モジュール (ネットワーク デバイス登録サービス) -- > 証明書登録ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS)|--|443 (注 2「**代替ポートを利用可能**」を参照)|  

###  <a name="BKMK_PortsDist_MP"></a> 配布ポイント --> 管理ポイント  
 配布ポイントは次のシナリオで管理ポイントと通信します。  

-   事前設定されたコンテンツのステータスをレポートする  

-   使用状況の概要データをレポートする  

-   コンテンツの検証をレポートする  

-   パッケージのダウンロード (プル配布ポイント) のステータスをレポートする

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|ハイパーテキスト転送プロトコル (HTTP)|--|80 (注 2「**代替ポートを利用可能**」を参照)|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS)|--|443 (注 2「**代替ポートを利用可能**」を参照)|  

###  <a name="BKMK_PortsEndpointProtection_Internet"></a> Endpoint Protection ポイント -- > インターネット  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|ハイパーテキスト転送プロトコル (HTTP)|--|80|  

###  <a name="BKMK_PortsEP-to-SQL"></a> Endpoint Protection ポイント -- > SQL Server  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (注 2「**代替ポートを利用可能**」を参照)|  

###  <a name="BKMK_PortsEnrollmentProxyEnrollmentPoint"></a> 登録プロキシ ポイント -- > 登録ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS)|--|443 (注 2「**代替ポートを利用可能**」を参照)|  

###  <a name="BKMK_PortsEnrollmentEnrollmentSQL"></a> 登録ポイント -- > SQL Server  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (注 2「**代替ポートを利用可能**」を参照)|  

###  <a name="BKMK_PortsExchangeConnectorHosted"></a> Exchange Server コネクタ -- &gt; Exchange Online  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTPS 経由の Windows リモート管理|--|5986|  

###  <a name="BKMK_PortsExchangeConnectorOnPrem"></a> Exchange Server コネクタ -- > 社内の Exchange Server  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP 経由の Windows リモート管理|--|5985|  

###  <a name="BKMK_PortsMacEnrollmentProxyPoint"></a> Mac コンピューター -- > 登録プロキシ ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS)|--|443|  

###  <a name="BKMK_PortsMP-DC"></a> 管理ポイント -- > ドメイン コントローラー  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|ライトウェイト ディレクトリ アクセス プロトコル (LDAP)|--|389|  
|LDAP (Secure Sockets Layer [SSL] 接続)|636|636|  
|グローバル カタログ LDAP|--|3268|  
|グローバル カタログ LDAP SSL|--|3269|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC (注 6「 **動的ポート**」を参照)|  

###  <a name="BKMK_PortsMP-Site"></a> 管理ポイント &lt; -- > サイト サーバー  
 (注 5「 **サイト サーバーとサイト システムの間の通信**」を参照)  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|RPC エンドポイント マッパー|--|135|  
|RPC|--|DYNAMIC (注 6「 **動的ポート**」を参照)|  
|サーバー メッセージ ブロック (SMB)|--|445|  

###  <a name="BKMK_PortsMP-SQL"></a> 管理ポイント -- > SQL Server  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (注 2「**代替ポートを利用可能**」を参照)|  

###  <a name="BKMK_PortsMobileDeviceClient-EnrollmentProxyPoint"></a> モバイル デバイス -- > 登録プロキシ ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS)|--|443|  

###  <a name="BKMK_PortsMobileDeviceClient-WindowsIntune"></a> モバイル デバイス -- > Microsoft Intune  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS)|--|443|  

###  <a name="BKMK_PortsRSP-SQL"></a> レポート サービス ポイント -- > SQL Server  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (注 2「**代替ポートを利用可能**」を参照)|  

###  <a name="BKMK_PortsIntuneConnector-WindowsIntune"></a> サービス接続ポイント -- > Microsoft Intune  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS)|--|443|
詳細については、サービス接続ポイントの[インターネット アクセス要件](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls)を参照してください。

###  <a name="BKMK_PortsAppCatalogWebServicePoint_SiteServer"></a> サイト サーバー &lt; -- > アプリケーション カタログ Web サービス ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC (注 6「 **動的ポート**」を参照)|  

###  <a name="BKMK_PortsAppCatalogWebSitePoint_SiteServer"></a> サイト サーバー &lt; -- > アプリケーション カタログ Web サイト ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC (注 6「 **動的ポート**」を参照)|  

###  <a name="BKMK_PortsSite-AISP"></a> サイト サーバー &lt; -- > 資産インテリジェンス同期ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC (注 6「 **動的ポート**」を参照)|  

###  <a name="BKMK_PortsSite-Client"></a> サイト サーバー -- > クライアント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|Wake On LAN|9 (注 2「**代替ポートを利用可能**」を参照)|--|  

###  <a name="BKMK_PortsSiteServer-CloudDP"></a> サイト サーバー -- > クラウドベースの配布ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS)|--|443|  

###  <a name="BKMK_PortsSite-DP"></a> サイト サーバー -- > 配布ポイント  
 (注 5「 **サイト サーバーとサイト システムの間の通信**」を参照)  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC (注 6「 **動的ポート**」を参照)|  

###  <a name="BKMK_PortsSite-DC"></a> サイト サーバー -- > ドメイン コントローラー  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|ライトウェイト ディレクトリ アクセス プロトコル (LDAP)|--|389|  
|LDAP (Secure Sockets Layer [SSL] 接続)|636|636|  
|グローバル カタログ LDAP|--|3268|  
|グローバル カタログ LDAP SSL|--|3269|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC (注 6「 **動的ポート**」を参照)|  

###  <a name="BKMK_PortsCertificateRegistrationPoint_SiteServer"></a> サイト サーバー &lt; -- > 証明書登録ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC (注 6「 **動的ポート**」を参照)|  

###  <a name="BKMK_PortsEndpointProtection_SiteServer"></a> サイト サーバー &lt; -- > Endpoint Protection ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC (注 6「 **動的ポート**」を参照)|  

###  <a name="BKMK_EnrollmentPoint_SiteServer"></a> サイト サーバー &lt; -- > 登録ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC (注 6「 **動的ポート**」を参照)|  

###  <a name="BKMK_EnrollmentProxyPoint_SiteServer"></a> サイト サーバー &lt; -- > 登録プロキシ ポイント  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC (注 6「 **動的ポート**」を参照)|  

###  <a name="BKMK_PortsSite-FSP"></a> サイト サーバー &lt; -- > フォールバック ステータス ポイント  
 (注 5「 **サイト サーバーとサイト システムの間の通信**」を参照)  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC (注 6「 **動的ポート**」を参照)|  

###  <a name="BKMK_PortSite-Internet"></a> サイト サーバー -- > インターネット  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|ハイパーテキスト転送プロトコル (HTTP)|--|80 (注 1「**プロキシ サーバーのポート**」を参照)|  

###  <a name="BKMK_PortsIssuingCA_SiteServer"></a> サイト サーバー &lt; -- > 発行元の証明機関 (CA)  
 この通信は、証明書登録ポイントを使用して、証明書プロファイルを展開するときに使用します。 通信は階層内のすべてのサイト サーバーで使用されるわけではありません。 代わりに、階層の最上位のサイト サーバーでのみ使用されます。  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|RPC エンドポイント マッパー|135|135|  
|RPC (DCOM)|--|DYNAMIC (注 6「 **動的ポート**」を参照)|  

###  <a name="BKMK_PortsSite-RSP"></a> サイト サーバー &lt; -- > レポート サービス ポイント  
 (注 5「 **サイト サーバーとサイト システムの間の通信**」を参照)  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC (注 6「 **動的ポート**」を参照)|  

###  <a name="BKMK_PortsSite-Site"></a> サイト サーバー &lt; -- > サイト サーバー  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  

###  <a name="BKMK_PortsSite-SQL"></a> サイト サーバー -- > SQL Server  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (注 2「**代替ポートを利用可能**」を参照)|  

 サイト データベースをリモート SQL Server でホストするサイトをインストールするときに、サイト サーバーと SQL Server 間の次のポートを開く必要があります。  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC (注 6「 **動的ポート**」を参照)|  

###  <a name="BKMK_PortsSite-Provider"></a> サイト サーバー -- > SMS プロバイダー  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  
|RPC|--|DYNAMIC (注 6「 **動的ポート**」を参照)|  

###  <a name="BKMK_PortsSite-SUP"></a> サイト サーバー &lt; -- > ソフトウェアの更新ポイント  
 (注 5「 **サイト サーバーとサイト システムの間の通信**」を参照)  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|ハイパーテキスト転送プロトコル (HTTP)|--|80 または 8530 (注 3「 **Windows Server Update Services**」を参照)|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS)|--|443 または 8531 (注 3「 **Windows Server Update Services**」を参照)|  

###  <a name="BKMK_PortsSite-SMP"></a> サイト サーバー &lt; -- > 状態移行ポイント  
 (注 5「 **サイト サーバーとサイト システムの間の通信**」を参照)  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  
|RPC エンドポイント マッパー|135|135|  

###  <a name="BKMK_PortsProvider-SQL"></a> SMS プロバイダー -- &gt; SQL Server  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (注 2「**代替ポートを利用可能**」を参照)|  

###  <a name="BKMK_PortsSUP-Internet"></a> ソフトウェアの更新ポイント -- > インターネット  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|ハイパーテキスト転送プロトコル (HTTP)|--|80 (注 1「**プロキシ サーバーのポート**」を参照)|  

###  <a name="BKMK_PortsSUP-WSUS"></a> ソフトウェアの更新ポイント -- > 上流の WSUS サーバー  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|ハイパーテキスト転送プロトコル (HTTP)|--|80 または 8530 (注 3「 **Windows Server Update Services**」を参照)|  
|セキュア ハイパーテキスト転送プロトコル (HTTPS)|--|443 または 8531 (注 3「 **Windows Server Update Services**」を参照)|  

###  <a name="BKMK_PortsSQL-SQL"></a> SQL Server --&gt; SQL Server  
 サイト間のデータベース レプリケーションでは、1 つのサイトの SQL Server がその親または子のサイトの SQL Server と直接通信する必要があります。  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL Server サービス|--|1433 (注 2「**代替ポートを利用可能**」を参照)|  
|SQL Server Service Broker|--|4022 (注 2「**代替ポートを利用可能**」を参照)|  

> [!TIP]  
>  Configuration Manager では、SQL Server Browser は必要ありません。SQL Server Browser は、UDP ポート 1434 を使用します。  

###  <a name="BKMK_PortsStateMigrationPoint-to-SQL"></a> 状態移行ポイント --> SQL Server  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|SQL over TCP|--|1433 (注 2「**代替ポートを利用可能**」を参照)|  



###  <a name="BKMY_PortNotes"></a> Configuration Manager クライアントとサイト システムで使用されるポートのメモ  

1.  **プロキシ サーバーのポート**: このポートは構成できませんが、構成されたプロキシ サーバーを経由してルーティングすることができます。  

2.  **代替ポートを利用可能**: この値に対して代替ポートを Configuration Manager 内で定義できます。 カスタム ポートを定義済みの場合、IPsec ポリシーまたはファイアウォールの構成用の IP フィルター情報を定義するときは、そのカスタム ポートを代わりに使用してください。  

3.  **Windows Server Update Services (WSUS)**: WSUS をインストールする際、クライアント接続用にポート 80/443 を使用するかポート 8530/8531 を使用するかを選択できます。 Windows Server 2012 または Windows Server 2016 で WSUS を実行する場合、WSUS は既定で HTTP にはポート 8530 を、HTTPS にはポート 8531 を使うように構成されています。  

     インストール後にポートを変更できます。 サイト階層全体で同じポート番号を使用する必要はありません。  

    -   HTTP ポートが 80 の場合、HTTPS ポートは 443 の必要があります。  

    -   HTTP ポートがその他の場合、HTTPS ポートは 1 大きくする必要があります (8530 と 8531 など)。   

    > [!NOTE]  
    >  HTTPS を使用するようソフトウェアの更新ポイントを構成するときには、HTTP ポートも開いている必要があります。 特定の更新プログラムの使用許諾契約書などの暗号化されていないデータは、HTTP ポートを使用します。  

4.  **簡易 FTP (TFTP) デーモン**: 簡易 FTP (TFTP) デーモン システム サービスは、Windows 展開サービス (WDS) で不可欠な要素で、ユーザー名やパスワードを必要としません。 簡易 FTP デーモン サービスでは、次の RFC で定義されている TFTP プロトコルのサポートを実装しています。  

    -   RFC 350: TFTP  

    -   RFC 2347: オプションの拡張  

    -   RFC 2348: ブロック サイズのオプション  

    -   RFC 2349: タイムアウト間隔、および転送サイズのオプション  

     TFTP は、ディスクレス ブート環境をサポートするように設計されています。 TFTP デーモンは、UDP ポート 69 でリッスンしますが、動的に割り当てられた高次のポートから応答します。 そのため、このポートを有効にすると、TFTP サービスは着信 TFTP 要求を受信できるようになりますが、選択したサーバーがそれらの要求に応答することはできません。 TFTP サーバーがポート 69 から応答するように構成しなければ、選択したサーバーが着信 TFTP 要求に応答するようにできません。  

5.  **サイト サーバーとサイト システムの間の通信**: 既定では、サイト サーバーとサイト システムの間の通信は双方向です。 サイト サーバーが通信を開始してサイト システムを構成し、次にほとんどのサイト システムはサイト サーバーに接続してステータス情報を送り返します。 レポート サービス ポイントおよび配布ポイントは、ステータス情報を送信しません。 サイト システムのプロパティで [**サイト サーバーがこのサイト システムへの接続を開始する必要がある**] を選択した場合、サイト システムのインストール後、サイト システムがサイト サーバーとの通信を開始しません。 代わりに、サイト サーバーが通信を開始し、サイト システム サーバーに対する認証用にサイト システムのインストール アカウントを使用します。  

6.  **動的ポート**: 動的ポート (または一時ポート) は、ポート番号の範囲を使用します。この範囲は、オペレーティング システムのバージョンによって定義されています。 既定のポート範囲の詳細については、「 [Windows のサービス概要およびネットワーク ポート要件](http://go.microsoft.com/fwlink/p/?LinkId=317965)」を参照してください。  

##  <a name="BKMK_AdditionalPorts"></a> その他のポートの一覧  
 次のセクションには、Configuration Manager により使用されるポートに関する追加情報が記載されています。  

###  <a name="BKMK_ClientShares"></a> クライアントからサーバーへの共有  
 クライアントは、UNC 共有に接続するたびにサーバー メッセージ ブロック (SMB) を使用します。 たとえば、  

-   CCMSetup.exe **/source:** コマンド ライン プロパティを指定する手動クライアント インストール  

-   UNC パスから定義ファイルをダウンロードする Endpoint Protection クライアント

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|サーバー メッセージ ブロック (SMB)|--|445|  

###  <a name="BKMK_SQLPorts"></a> Microsoft SQL Server への接続  
 SQL Server データベース エンジンとの通信、およびサイト間のレプリケーションには、SQL Server の既定ポートを使用することも、カスタム ポートを指定することもできます。  

-   サイト間通信では、次のポートが使用されます。  

    -   SQL Server Service Broker では、既定のポート TCP 4022 が使用されます。  

    -   SQL Server サービスでは、既定のポート TCP 1433 が使用されます。  

-   SQL Server データベース エンジンとさまざまな Configuration Manager サイト システムの役割の間のサイト内通信では、既定でポート TCP 1433 が使用されます。  

- Configuration Manager は、サイト データベースをホストする各 SQL 可用性グループ レプリカがスタンドアロン SQL Server インスタンスであるかのように、同じポートとプロトコルを利用して各レプリカと通信します。

Azure を利用するとき、サイト データベースが内部または外部の負荷分散装置の後ろにある場合は、各レプリカで次のファイアウォール例外を設定し、次のポートに負荷分散ルールを追加します。
 - SQL over TCP: TCP 1433
 - SQL Server Service Broker: TCP 4022
 - サーバー メッセージ ブロック (SMB): TCP 445
 - RPC エンドポイント マッパー: TCP 135

> [!WARNING]  
>  Configuration Manager は、動的ポートをサポートしていません。 SQL Server 名前付きインスタンスの既定動作では、データベース エンジンへの接続に動的ポートが使用されるため、名前付きインスタンスの使用時に、サイト内通信に使用する静的ポートを手動で構成する必要があります。  

 次のサイト システムの役割は、SQL Server データベースと直接通信します。  

-   アプリケーション カタログ Web サービス ポイント  

-   証明書登録ポイントの役割  

-   登録ポイントの役割  

-   管理ポイント  

-   サイト サーバー  

-   レポート サービス ポイント  

-   SMS プロバイダー  

-   SQL Server --> SQL Server  

SQL Server が複数のサイトからデータベースをホストする場合、各データベースは個別の SQL Server インスタンスを使用する必要があり、各インスタンスは一意のポート セットで構成されなければなりません。  

SQL Server コンピューターでファイアウォールを有効にしている場合は、展開で使用するポートを許可するように構成されていることを確認します。 また、SQL Server と通信するコンピューター間のネットワーク上の他の場所にあるファイアウォールもこれらの同じポートを許可するように構成します。  

特定のポートを使用するように SQL Server を構成する方法の例については、SQL Server TechNet ライブラリの「 [特定の TCP ポートで受信待ちするようにサーバーを構成する方法 (SQL Server 構成マネージャー)](http://go.microsoft.com/fwlink/p/?LinkID=226349) 」を参照してください。  


### <a name="bkmk_discovery"> </a> 検出と公開
次のポートは、サイト情報の検出と公開に使用されます。
 - ライトウェイト ディレクトリ アクセス プロトコル (LDAP) : 389
 - LDAP (Secure Sockets Layer [SSL] 接続) : 636


 - グローバル カタログ LDAP : 3268
 - グローバル カタログ LDAP SSL : 3269


 - RPC エンドポイント マッパー: 135
 - RPC : 動的に割り当てられた高 TCP ポート


 - TCP: 1024: 5000
 - TCP: 49152: 65535


###  <a name="BKMK_External"></a> Configuration Manager により確立される外部接続  
 Configuration Manager クライアントまたはサイト システムは、次の外部接続を実行できます。  

-   [資産インテリジェンス同期ポイント -- &gt; Microsoft](#BKMK_PortsAI)  

-   [Endpoint Protection ポイント -- &gt; インターネット](#BKMK_PortsEndpointProtection_Internet)  

-   [クライアント -- &gt; グローバル カタログ ドメイン コントローラー](#BKMK_PortsClient-GCDC)  

-   [Configuration Manager コンソール -- &gt; インターネット](#BKMK_PortsConsole-Internet)  

-   [管理ポイント -- &gt; ドメイン コントローラー](#BKMK_PortsMP-DC)  

-   [サイト サーバー -- &gt; ドメイン コントローラー](#BKMK_PortsSite-DC)  

-   [サイト サーバー &lt; -- &gt; 発行元の証明機関 (CA)](#BKMK_PortsIssuingCA_SiteServer)  

-   [ソフトウェアの更新ポイント -- &gt; インターネット](#BKMK_PortsSUP-Internet)  

-   [ソフトウェアの更新ポイント -- &gt; 上流の WSUS サーバー](#BKMK_PortsSUP-WSUS)  

-   [サービス接続ポイント -- &gt; Microsoft Intune](#BKMK_PortsIntuneConnector-WindowsIntune)  

###  <a name="BKMK_IBCMports"></a> インターネット ベースのクライアントをサポートするサイト システムのインストール要件  
 インターネットベースのクライアントをサポートする管理ポイントと配布ポイント、ソフトウェアの更新ポイント、およびフォールバック ステータス ポイントは、インストールと修復に次のポートを使用します。  

-   サイト サーバー --> サイト システム: UDP および TCP ポート 135 を使用する RPC エンドポイント マッパー。  

-   サイト サーバー --> サイト システム: RPC 動的 TCP ポート  

-   サイト サーバー &lt; --> サイト システム: TCP ポート 445 を使用するサーバー メッセージ ブロック (SMB)

配布ポイントでのアプリケーションとパッケージのインストールには、次の RPC ポートが必要です。  

-   サイト サーバー --> 配布ポイント: UDP および TCP ポート 135 を使用する RPC エンドポイント マッパー

-   サイト サーバー --> 配布ポイント: RPC 動的 TCP ポート  

サイト サーバーとサイト システム間のトラフィックをセキュリティで保護するために IPsec を使用します。 RPC で使用される動的ポートを制限する必要がある場合、Microsoft RPC 構成ツール (rpccfg.exe) を使用し、これらの RPC パケットに対しポートの限定範囲を構成することができます。 RPC 構成ツールの詳細については、「 [RPC で特定のポートが使用されるように構成する方法、および IPSec を使用してそれらのポートをセキュリティで保護する方法](http://go.microsoft.com/fwlink/p/?LinkId=124096)」を参照してください。  

> [!IMPORTANT]  
>  これらのサイト システムをインストールする前に、リモート レジストリ サービスがサイト システム サーバーで実行されていること、サイト システムが信頼関係のない別の Active Directory フォレストにある場合は、サイト システムのインストール アカウントを指定していることを確認します。  

###  <a name="BKMK_PortsClientInstall"></a> Configuration Manager クライアント インストールで使用されるポート  
クライアントのインストール中に使用されるポートは、クライアントの展開方法に応じて異なります。 クライアントの展開方法別のポートの一覧については、「[System Center Configuration Manager におけるクライアントの Windows ファイアウォールとポートの設定](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md)」の「**Configuration Manager クライアントの展開で使用されるポート**」を参照してください。 クライアントのインストールとインストール後の通信用にクライアントの Windows ファイアウォールを構成する方法については、「[System Center Configuration Manager におけるクライアントの Windows ファイアウォールとポートの設定](../../../core/clients/deploy/windows-firewall-and-port-settings-for-clients.md)」を参照してください。  

###  <a name="BKMK_MigrationPorts"></a> 移行で使用されるポート  
移行を実行しているサイト サーバーは、ソース階層内の該当するサイトに接続するいくつかのポートを使用して、ソース サイトの SQL Server データベースからデータを収集し、配布ポイントを共有します。  

 これらのポートの詳細については、「[System Center Configuration Manager での移行の前提条件](../../../core/migration/prerequisites-for-migration.md)」の「[移行に必要な構成](../../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations)」セクションを参照してください。  

###  <a name="BKMK_ServerPorts"></a> Windows サーバーで使用されるポート  
 次の表に、Windows サーバーで使用される主なポートとそれらの機能について示します。 Windows サーバーのサービスとネットワーク ポートの要件の詳細の一覧については、「 [Windows サーバー システムのサービス概要およびネットワーク ポート要件](http://go.microsoft.com/fwlink/p/?LinkID=123652)」を参照してください。  

|説明|UDP|TCP|  
|-----------------|---------|---------|  
|ドメイン ネーム システム (DNS)|53|53|  
|動的ホスト構成プロトコル (DHCP)|67 および 68|--|  
|NetBIOS 名前解決|137|--|  
|NeTBIOS データグラム サービス|138|--|  
|NeTBIOS セッション サービス|--|139|  

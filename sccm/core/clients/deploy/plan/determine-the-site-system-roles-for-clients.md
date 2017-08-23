---
title: "クライアントのサイト システムの役割 | Microsoft Docs"
description: "System Center Configuration Manager でクライアントのサイト システムの役割を決定します。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
caps.latest.revision: "9"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 9f2dda834f23b2ee85c4c301c7e1b6a3a54ebc97
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="determine-the-site-system-roles-for-system-center-configuration-manager-clients"></a>System Center Configuration Manager クライアントのサイト システムの役割の決定

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックは、Configuration Manager クライアントを展開するうえで必要なサイト システムの役割を特定するのに役立ちます。  

 階層内で必要なサイト システムの役割をインストールする場所の詳細については、「[System Center Configuration Manager のサイト階層の設計](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md)」をご覧ください。  

 必要なサイト システムの役割をインストールして構成する方法の詳細については、「[サイト システムの役割のインストール](../../../../core/servers/deploy/configure/install-site-system-roles.md)」をご覧ください。  

##  <a name="determine-if-you-need-a-management-point"></a>管理ポイントが必要かどうかを判断する  
 既定では、すべての Windows クライアント コンピューターは配布ポイントを使用して Configuration Manager クライアントをインストールし、配布ポイントが使用できない場合は、その代替として管理ポイントを使用できます。 ただし、CCMSetup コマンド ライン プロパティ **/source:<パス\>** を使用して、代替ソースからコンピューターに Windows クライアントをインストールできます。 たとえば、インターネット上にクライアントをインストールする場合に有効です。 また、必要なポートをファイアウォールがブロックしているため、あるいは低帯域幅接続をしているために、クライアントのインストール時にコンピューターと管理ポイントの間でのネットワーク パケットの送信を避けたい場合が考えられます。 しかし、すべてのクライアントは、サイトに割り当てて Configuration Manager で管理するために管理ポイントと通信する必要があります。  

 CCMSetup のコマンドライン プロパティ **/source:<パス\>** の詳細については、「[System Center Configuration Manager のクライアント インストール プロパティについて](../../../../core/clients/deploy/about-client-installation-properties.md)」をご覧ください。  

 階層内に複数の管理ポイントをインストールすると、クライアントは、フォレストのメンバーシップとネットワーク上の位置に基づいて、1 つの管理ポイントに自動的に接続します。 セカンダリ サイトには複数の管理ポイントをインストールすることはできません。  

 Mac コンピューター クライアント、および Configuration Manager に登録するモバイル デバイス クライアントには、クライアント インストールのために常に管理ポイントが必要です。 この管理ポイントは、プライマリ サイトにあり、モバイル デバイスをサポートするよう構成され、インターネットからのクライアント接続を受け入れることが必要です。 モバイル デバイス クライアントはセカンダリ サイトの管理ポイントを使用できず、ほかのプライマリ サイトの管理ポイントに接続することもできません。  

##  <a name="determine-if-you-need-a-fallback-status-point"></a>フォールバック ステータス ポイントをインストールするかどうかを判断する  
 フォールバック ステータス ポイントを使用すると、Windows コンピューターのクライアントの展開を監視できます。 管理ポイントとの通信ができないために管理されていない Windows コンピューターのクライアントを識別することもできます。 Mac コンピューター、Configuration Manager によって登録されるモバイル デバイス、Exchange Server コネクタを使用して管理されるモバイル デバイスは、フォールバック ステータス ポイントを使用しません。  

 フォールバック ステータス ポイントは、クライアントのアクティビティやクライアントのヘルスを監視するのに必要ではありません。  

 フォールバック ステータス ポイントは常に HTTP を介してクライアントと通信しますが、HTTP は接続時の認証がなく、データをクリア テキストで送信します。 したがって、特にインターネット ベースでクライアントを管理している場合には、フォールバック ステータス ポイントが攻撃対象になる可能性があります。 このような危険を避けるには、実稼働環境にフォールバック ステータス ポイントだけを実行する専用サーバーを設置し、このサーバーには別のサイト システムの役割をインストールしないようにします。  

 次の条件すべてに該当する場合は、フォールバック ステータス ポイントをインストールしてください。  

-   クライアント コンピューターが管理ポイントと通信できなくても、Windows コンピューターからのクライアント通信エラーをサイトに送る。  

-   フォールバック ステータス ポイントから送信されるデータを表示する、構成マネージャー クライアントの展開レポートを使用する。  

-   このサイト システムの役割専用のサーバーがあり、サーバーを攻撃から保護することができるセキュリティ手段が他にもある。  

-   接続時の認証がなく HTTP トラフィックでは平文のままデータが転送されるためセキュリティ上のリスクはありますが、それよりもフォールバック ステータス ポイントを使用する利点の方が高くなります。  

 接続時の認証がなく、データをクリア テキストで送信するために発生する、Web サイト実行上のセキュリティ リスクが、クライアントで発生する通信上の問題を特定することによる利点よりも高い場合は、フォールバック ステータス ポイントをインストールしないでください。  

##  <a name="determine-whether-you-need-a-reporting-services-point"></a>レポート サービス ポイントが必要かどうかを判断する  
 Configuration Manager には、Configuration Manager コンソールでのクライアントのインストール、割り当て、および管理を監視するのに役立つ多数のレポートがあります。 一部のクライアント展開レポートは、クライアントがフォールバック ステータス ポイントに割り当てられていることが必要です。  

 クライアントの展開にレポートは必要ではなく、一部の展開情報は Configuration Manager コンソールで確認でき、クライアント ログ ファイルを利用して詳細情報を確認することもできますが、クライアント レポートは、クライアントの展開の監視やトラブルシューティングに役立つ貴重な情報を提供します。  

##  <a name="determine-if-you-need-an-enrollment-point-and-an-enrollment-proxy-point"></a>登録ポイントと登録プロキシ ポイントが必要かどうかを判断する  
 モバイル デバイスを登録し、Mac コンピューター用の証明書を登録するために、Configuration Manager には登録ポイントと登録プロキシ ポイントが必要です。 Exchange Server コネクタを使用してモバイル デバイスを管理する場合や、モバイル デバイスのレガシ クライアント (たとえば Windows CE) をインストールする場合、または Configuration Manager を使用せずにクライアント証明書を要求して Mac コンピューターにインストールする場合、これらのサイト システムの役割は必要ありません。  

##  <a name="determine-if-you-need-a-distribution-point"></a>配布ポイントが必要かどかを判断する  
 Windows コンピューターに Configuration Manager クライアントをインストールする場合、配布ポイントは必要ありません。 ただし、既定では、Configuration Manager はクライアントのソース ファイルを Windows コンピューターにインストールするときに配布ポイントを使用します。配布ポイントを使用できない場合は、代替として管理ポイントからこれらのファイルをダウンロードできます。 配布ポイントは、Configuration Manager に登録していないモバイル デバイス クライアントをインストールする場合には使用されませんが、モバイル デバイスのレガシ クライアントをインストールする場合には使用されます。 構成マネージャー クライアントをオペレーティング システムの展開の一部としてインストールする場合は、オペレーティング システムのイメージは配布ポイントに格納され、そこから取得されます。  

 ほとんどの Configuration Manager クライアントをインストールするのに配布ポイントは必要ありませんが、アプリケーションやソフトウェア更新プログラムなどのソフトウェアをクライアントにインストールする場合には、配布ポイントが必要です。  

##  <a name="determine-if-you-need-an-application-catalog-website-point-and-an-application-catalog-web-services-point"></a>アプリケーション カタログ Web サイト ポイントとアプリケーション カタログ Web サービス ポイントが必要かどうかを判断する  
 アプリケーション カタログ Web サイト ポイントとアプリケーション カタログ Web サービス ポイントは、クライアントの展開に必要ではありません。 ただし、これらをクライアント展開プロセスの一部としてインストールしておくと、構成マネージャー クライアントを Windows コンピューターにインストールしてすぐに、ユーザーが次の操作を実行できるようになります。  

-   モバイル デバイスをワイプする。  

-   アプリケーション カタログでアプリケーションを見つけてインストールする。  

-   展開の目的が [ **利用可能** ] のアプリケーションをユーザーまたはデバイスに展開します。  

##  <a name="determine-whether-you-require-a-cloud-management-gateway-connector-point"></a>クラウド管理ゲートウェイ コネクタ ポイントが必要かどうかを判断する 

[クラウド管理ゲートウェイ](/sccm/core/clients/manage/setup-cloud-management-gateway) を設定して[クライアントをインターネット上でする](/sccm/core/clients/manage/manage-clients-internet)場合は、クラウド管理ゲートウェイ コネクタ ポイントが必要です。


 
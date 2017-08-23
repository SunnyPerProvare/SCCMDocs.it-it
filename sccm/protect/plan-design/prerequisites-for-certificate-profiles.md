---
title: "証明書プロファイルの前提条件 | Microsoft Docs"
description: "System Center Configuration Manager の証明書プロファイル、およびそれらの外部依存関係と製品内依存関係について説明します。"
ms.custom: na
ms.date: 03/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0317fd02-3721-4634-b18b-7c976a4e92bf
caps.latest.revision: "9"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: fba52ee305fe67418f2fe544bfe94d10467236d0
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-certificate-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager での証明書プロファイルの前提条件

*適用対象: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager の証明書プロファイルには、外部依存関係と製品内依存関係があります。  

## <a name="dependencies-external-to-configuration-manager"></a>Configuration Manager 外部の依存関係  

|依存関係|説明|  
|----------------|----------------------|  
|Active Directory 証明書サービス (AD CS) を実行するエンタープライズ証明機関 (CA)<br /><br /> 証明書を失効させるには、階層の最上位のサイト サーバーのコンピューター アカウントに *証明書の発行と管理* の権限が、証明書管理者の証明書プロファイルが使用する各証明書テンプレートに対して必要となります。 または、証明書管理者に、その証明書管理者が使用するすべての証明書テンプレートに対するアクセス許可を付与します。<br /><br /> 証明書要求のCA マネージャーによる承認が必要になるように設定することもできます。 ただし、証明書の発行に使用する証明書テンプレートで、証明書のサブジェクトを **[要求に含まれる]** に設定して、System Center Configuration Manager によってサブジェクトの値が自動的に含まれるようにする必要があります。|Active Directory 証明書サービスの詳細については、Windows Server のドキュメントを参照してください。<br /><br /> Windows Server 2012: [Active Directory 証明書サービスの概要](http://go.microsoft.com/fwlink/p/?LinkId=286744)<br /><br /> Windows Server 2008: [Windows Server 2008 の Active Directory 証明書サービス](http://go.microsoft.com/fwlink/p/?LinkId=115018)|  
|Windows Server 2012 R2 で実行される、Active Directory 証明書サービス用のネットワーク デバイス登録サービスの役割サービス<br /><br /> さらに:<br /><br /> クライアントとネットワーク デバイス登録サービス間の通信で、TCP 443 (HTTPS 用) と TCP 80 (HTTP 用) 以外のポート番号を使用することはできません。<br /><br /> ネットワーク デバイス登録サービスを実行するサーバーは、発行元 CA とは別のサーバーに配置する必要があります。|System Center Configuration Manager は、Windows Server 2012 R2 のネットワーク デバイス登録サービスと通信して、Simple Certificate Enrollment Protocol (SCEP) 要求を生成および検証します。<br /><br /> インターネットから接続するユーザーやデバイス (Microsoft Intune で管理されているモバイル デバイスなど) に証明書を発行する場合は、これらのデバイスが、ネットワーク デバイス登録サービスを実行しているサーバーにインターネットからアクセスできる必要があります。 たとえば、このサーバーを境界ネットワーク (DMZ、非武装地帯、スクリーン サブネットともいいます) に設置します。<br /><br /> ネットワーク デバイス登録サービスを実行するサーバーと発行元 CA の間にファイアウォールがある場合は、この 2 つのサービス間の通信トラフィック (DCOM) を許可するようにファイアウォールを構成する必要があります。 System Center Configuration Manager サイト サーバーを実行するサーバーと発行元 CA 間の通信も同様に設定して、System Center Configuration Manager が証明書を失効できるようにします。<br /><br /> SSL を必要とするようにネットワーク デバイス登録サービスが構成されている場合は、セキュリティのベスト プラクティスに従って、接続するデバイスがサーバー証明書を検証するために証明書失効リスト (CRL) にアクセスできるようにしてください。<br /><br /> Windows Server 2012 R2 のネットワーク デバイス登録サービスの詳細については、「 [ポリシー モジュールとネットワーク デバイス登録サービスの使用](http://go.microsoft.com/fwlink/p/?LinkId=328657)」を参照してください。|  
|発行元 CA で Windows Server 2008 R2 を実行している場合は、SCEP 証明書更新要求に必要な修正プログラムをこのサーバーにインストールする必要があります。|修正プログラムをまだインストールしていない場合は、必ず、インストールしてください。 詳細については、Microsoft サポート技術情報の記事「 [2483564: NDES を使用して、証明書が管理されている場合に Windows Server 2008 R2 の SCEP 証明書更新の要求が失敗しました](http://go.microsoft.com/fwlink/?LinkId=311945) 」を参照してください。|  
|PKI クライアント認証証明書およびエクスポートされたルート CA 証明書|この証明書は、ネットワーク デバイス登録サービスを実行しているサーバーが System Center Configuration Manager から認証を受けるための証明書です。<br /><br /> 詳細については、「[System Center Configuration Manager での PKI 証明書の要件](../../core/plan-design/network/pki-certificate-requirements.md)」を参照してください。|  
|サポートされるデバイス オペレーティング システム|iOS、Windows 8.1、Windows RT 8.1、Windows 10、および Android オペレーティング システムのデバイスに証明書プロファイルを展開できます。|  

## <a name="configuration-manager-dependencies"></a>Configuration Manager の依存関係  

|依存関係|説明|  
|----------------|----------------------|  
|証明書登録ポイントのサイト システムの役割|証明書プロファイルを使用する前に、証明書登録ポイントのサイト システムの役割をインストールする必要があります。 この役割は、System Center Configuration Manager データベース、System Center Configuration Manager サイト サーバー、および System Center Configuration Manager ポリシー モジュールと通信します。<br /><br /> このサイト システムの役割のシステム要件とこの役割をインストールする階層内の場所の詳細については、「[System Center Configuration Manager のサポートされている構成](../../core/plan-design/configs/supported-configurations.md)」トピックの「**サイト システムの要件**」セクションを参照してください。<br /><br /> 証明書登録ポイントは、ネットワーク デバイス登録サービスを実行するサーバーと同じサーバーにインストールしないでください。|  
|System Center Configuration Manager ポリシー モジュールが、Active Directory 証明書サービス用のネットワーク デバイス登録サービスの役割サービスを実行するサーバーにインストールされていること|証明書プロファイルを展開するには、System Center Configuration Manager ポリシー モジュールをインストールする必要があります。 このポリシー モジュールは、System Center Configuration Manager インストール メディアに収録されています。|  
|探索データ|証明書のサブジェクトとサブジェクトの別名の値は System Center Configuration Manager によって供給され、検出によって収集された情報から取得されます。<br /><br /> ユーザー証明書: Active Directory ユーザー探索<br /><br /> コンピューター証明書: Active Directory システム探索とネットワーク探索|  
|証明書プロファイルを管理するためのセキュリティのアクセス許可|証明書プロファイル、Wi-Fi プロファイル、VPN プロファイルなど、会社のリソースへのアクセスの設定を管理するには、以下のセキュリティ アクセス許可を持っている必要があります。<br /><br /> 証明書のアラートとレポートを表示して管理する場合: **アラート**オブジェクトに対する **作成**、 **削除**、 **変更**、 **レポートの変更**、 **読み取り** 、 **レポートの実行** 。<br /><br /> 証明書プロファイルを作成して管理する場合: **証明書プロファイル**オブジェクトに対する **作成者ポリシー**、 **レポートの変更** 、 **読み取り** 、 **レポートの実行** 。<br /><br /> Wi-Fi プロファイル、証明書プロファイル、および VPN プロファイルの展開を管理する場合: **コレクション**オブジェクトに対する **構成ポリシーの展開**、 **クライアント ステータス アラートの変更**、 **読み取り** 、 **リソースの読み取り** 。<br /><br /> すべての構成ポリシーを管理する場合: **構成のポリシー**オブジェクトに対する **作成**、 **削除**、 **変更** 、 **読み取り** 、 **セキュリティ スコープの設定** 。<br /><br /> 証明書プロファイルに関連するクエリを実行する場合: **クエリ** オブジェクトの **読み取り** 。<br /><br /> System Center Configuration Manager コンソールで証明書プロファイル情報を表示する場合: **サイト** オブジェクトの **読み取り** アクセス許可。<br /><br /> 証明書プロファイルのステータス メッセージを表示する場合: **ステータス メッセージ** オブジェクトの **読み取り** アクセス許可。<br /><br /> 信頼された証明機関証明書プロファイルを作成および変更する場合: **信頼された証明機関証明書プロファイル**オブジェクトに対する **作成者ポリシー**、 **レポートの変更** 、 **読み取り** 、 **レポートの実行** 。<br /><br /> VPN プロファイルを作成して管理する場合: **VPN プロファイル**オブジェクトに対する **作成者ポリシー**、 **レポートの変更** 、 **読み取り** 、 **レポートの実行** 。<br /><br /> Wi-Fi プロファイルを作成して管理する場合: **Wi-Fi プロファイル**オブジェクトに対する **作成者ポリシー**、 **レポートの変更** 、 **読み取り** 、 **レポートの実行** 。<br /><br /> **[会社リソース アクセス マネージャー]** セキュリティ ロールには、System Center Configuration Manager で証明書プロファイルを管理するのに必要な上記のアクセス許可が付与されています。 詳細については、「 **Configure role-based administration** 」トピックの「 [Configure security in System Center Configuration Manager](../../core/plan-design/security/configure-security.md) 」セクションを参照してください。|  

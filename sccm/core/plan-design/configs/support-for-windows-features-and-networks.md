---
title: "Windows の機能のサポート | Microsoft Docs"
description: "System Center Configuration Manager でサポートされる Windows とネットワークの機能について説明します。"
ms.custom: na
ms.date: 3/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0cf4bacb-6b6d-4d4f-8640-b13fe15873de
caps.latest.revision: "8"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: e040552dab21ba9a71e06a78f6acc2ffe1b0eb61
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="support-for-windows-features-and-networks-in-system-center-configuration-manager"></a>System Center Configuration Manager での Windows 機能とネットワークのサポート

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックでは、System Center Configuration Manager による一般的な Windows とネットワークの機能のサポートを示します。  


##  <a name="bkmk_branchcache"></a> BranchCache  
配布ポイントで BranchCache を有効にして、分散キャッシュ モードで BranchCache を使用するようにクライアントを構成している場合、Windows BranchCache を Configuration Manager と共に使用することができます。

アプリケーションの展開の種類、パッケージの展開、およびタスク シーケンスに関する BranchCache の設定を構成できます。  

BranchCache の要件を満たしている場合、リモートの場所にあるクライアントは、この機能を使用して、コンテンツの最新のキャッシュを持っているローカルのクライアントからコンテンツを取得できます。  

たとえば、BranchCache が有効な最初のクライアント コンピューターが、BranchCache サーバーとして構成されている配布ポイントからコンテンツを要求するとき、クライアント コンピューターは、コンテンツをダウンロードしてキャッシュします。 これと同じコンテンツを要求する同じサブネット上のクライアントは、このコンテンツを利用できるようになります。

これらのクライアントもそのコンテンツをキャッシュします。 このように、同じサブネット上の後続のクライアントは配布ポイントからコンテンツをダウンロードする必要がありません。コンテンツは、以後の転送で複数のクライアントから配布されます。  

**Configuration Manager で BranchCache をサポートするための要件:**  
-   **配布ポイントの構成:**  
    配布ポイントとして構成されたサイト システム サーバーに **Windows BranchCache** 機能を追加します。    

    -   BranchCache をサポートするように構成されたサーバー上の配布ポイントには、追加の構成は必要ありません。   
    -   Windows BranchCache をクラウド ベースの配布ポイントに追加することはできませんが、クラウド ベースの配布ポイントは、Windows BranchCache が構成されているクライアントによるコンテンツのダウンロードをサポートしています。  

-   **クライアントの構成:**    
    -   BranchCache に対応したクライアントが、BranchCache 分散キャッシュ モード用に構成されている必要があります。  
    -   BITS クライアントの設定に関するオペレーティング システムの設定で、BranchCache のサポートを有効にする必要があります。   <br /> <br />
        
    BranchCache をサポートするようにクライアントを構成する方法については、「[Windows 10 更新プログラム向けの BranchCache の構成](https://technet.microsoft.com/itpro/windows/manage/waas-branchcache)」の「[BranchCache クライアントの構成](https://technet.microsoft.com/itpro/windows/manage/waas-branchcache#configure-clients-for-branchcache)」セクションを参照してください。


**Configuration Manager は、Windows BranchCache に対応している以下のクライアント オペレーティング システムをサポートします。**  

|オペレーティング システム|サポートの詳細|  
|----------------------|---------------------|  
|Windows 7 SP1|既定でサポート|  
|Windows 8|既定でサポート|  
|Windows 8.1|既定でサポート|  
|Windows 10|既定でサポート|  
|Windows Server 2008 SP2|**BITS 4.0 が必要**: BITS 4.0 リリースを Configuration Manager クライアントにインストールするには、ソフトウェアの更新プログラムまたはソフトウェアの配布を使用します。 BITS 4.0 リリースの詳細については、「 [Windows Management Framework](http://go.microsoft.com/fwlink/p/?LinkId=181979)」を参照してください。<br /><br /> このオペレーティング システムでは、BranchCache クライアント機能はネットワークから実行されるソフトウェアの配布または SMB ファイル転送ではサポートされません。 加えてこのオペレーティング システムでは、BranchCache の機能をクラウド ベースの配布ポイントで使用することができません。|  
|Windows Server 2008 R2|既定でサポート|  
|Windows Server 2012|既定でサポート|  
|Windows Server 2012 R2|既定でサポート|  

 BranchCache の詳細については、Windows Server のドキュメントの「 [BranchCache for Windows (Windows の BranchCache)](http://go.microsoft.com/fwlink/p/?LinkId=177945) 」を参照してください。  

##  <a name="bkmk_Workgroups"></a> ワークグループ内のコンピューター  
Configuration Manager では、ワークグループ内のクライアントがサポートされます。  

-   Configuration Manager では、ワークグループとドメインとの間でのクライアントの移動がサポートされます。 詳細については、「[System Center Configuration Manager でクライアントを Windows コンピューターに展開する方法](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)」のトピックの「[ワークグループ コンピューターへの Configuration Manager クライアントのインストール方法](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientWorkgroup)」のセクションを参照してください。  

> [!NOTE]  
>  ワークグループのクライアントはサポートされますが、すべてのサイト システムは、サポートされた Active Directory ドメインのメンバーである必要があります。  


##  <a name="bkmmk_datadedup"></a> データ重複除去  
Configuration Manager は、次に示すオペレーティング システム上の配布ポイントで、データ重複除去の使用をサポートしています。  

-   Windows Server 2012  

-   Windows Server 2012 R2  

> [!IMPORTANT]  
>  パッケージ ソース ファイルをホストするボリュームは、データ重複除去の対象としてマークできません。 これは、データ重複除去には再解析ポイントを使いますが、Configuration Manager では、再解析ポイントで保存したファイルが含まれるコンテンツ ソースの場所の使用はサポートされないためです。  

詳細については、Configuration Manager チームのブログ「[ Configuration Manager Distribution Points and Windows Server 2012 Data Deduplication](http://blogs.technet.com/b/configmgrteam/archive/2014/02/18/configuration-manager-distribution-points-and-windows-server-2012-data-deduplication.aspx)」(Configuration Manager の配布ポイントと Windows Server 2012 のデータ重複除去) および Windows Server TechNet ライブラリの「[データ重複除去の概要](http://technet.microsoft.com/library/hh831602.aspx)」を参照してください。  

##  <a name="bkmk_DA"></a> DirectAccess  
Configuration Manager では、クライアントとサイト サーバー システム間の通信用に、Windows Server 2008 R2 以降の DirectAccess 機能をサポートしています。  

-   DirectAccess の要件がすべて満たされているときに、DirectAccess を使用することで、インターネット上の Configuration Manager クライアントは、イントラネット上にいるかのように割り当て先のサイトと通信できます。  

-   サーバーにより開始される操作 (リモート コントロールやクライアント プッシュ インストールなど) の場合、操作を開始するコンピューター (サイト サーバーなど) は、IPv6 を実行している必要があります。また、このプロトコルは、介在するすべてのネットワーク デバイスでサポートされている必要もあります。  

Configuration Manager では、次に示す DirectAccess を利用した操作はサポートされていません。  

-   オペレーティング システムの展開  

-   Configuration Manager サイト間の通信  

-   サイト内の Configuration Manager サイト システム サーバー間の通信  

##  <a name="bkmk_dualboot"></a> デュアル ブート コンピューター  
 Configuration Manager では、1 台のコンピューター上の複数のオペレーティング システムを管理できません。 1 台の管理対象コンピューターに複数のオペレーティング システムがある場合は、管理対象のオペレーティング システムのみに Configuration Manager クライアントがインストールされるようにするために使用される探索およびインストール方法を調整します。  

##  <a name="bkmk_IPv6"></a> インターネット プロトコル バージョン 6  
 Configuration Manager では、インターネット プロトコル バージョン 4 (IPv4) に加えて、インターネット プロトコル バージョン 6 (IPv6) をサポートしています。ただし次の例外があります。  

|機能| IPv6 のサポートの例外|  
|--------------|-------------------------------|  
|クラウドベースの配布ポイント|Microsoft Azure とクラウド ベースの配布ポイントをサポートするには、IPv4 が必要です。|  
|Microsoft Intune および Microsoft サービス コネクタで登録されるモバイル デバイス|Microsoft Intune および Microsoft サービス コネクタで登録されるモバイル デバイスをサポートするには、IPv4 が必要です。|  
|ネットワーク探索|ネットワーク探索で検索するように DHCP サーバーを構成した場合は、IPv4 が必要です。|  
|オペレーティング システムの展開|オペレーティング システムの展開をサポートするには、IPv4 が必要です。|  
|ウェイクアップ プロキシ通信|クライアントのウェイクアップ プロキシ パケットをサポートするには、IPv4 が必要です。|  
|Windows CE|Windows CE デバイスで Configuration Manager クライアントをサポートするには、IPv4 が必要です。|  

##  <a name="bkmk_NAT"></a> ネットワーク アドレス変換  
 Configuration Manager では、ネットワーク アドレス変換 (NAT) はサポートされていません。ただし、サイトがインターネット上のクライアントをサポートしていて、クライアントがインターネットに接続されていることを検出する場合を除きます。 インターネット ベースのクライアント管理の詳細については、「[Plan for managing Internet-based clients in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-for-managing-internet-based-clients.md)」(System Center Configuration Manager でインターネット ベースのクライアントを管理する計画) を参照してください。  

##  <a name="bkmk_storage"></a> 特殊なストレージ技術  
 Configuration Manager は、Configuration Manager コンポーネントがインストールされているオペレーティング システムのバージョン用の Windows ハードウェア互換性リストで認定されているハードウェアで動作するように設計されています。

サイト サーバーの役割では、ディレクトリとファイルのアクセス許可を設定できるようにするために、NTFS ファイル システムが必要です。 Configuration Manager は論理ドライブの完全な所有権を保持していることを前提としていて、個別のコンピューターで実行するサイト システムはストレージ技術を問わず論理パーティションを共有できないためです。 ただし、各コンピューターは、共有ストレージ デバイスの同じ物理パーティションにある個別の論理パーティションを使用できます。  

 **サポートに関する考慮事項:**  

-   **記憶域ネットワーク**: 記憶域ネットワーク (SAN) は、サポート対象の Windows ベースのサーバーが、SAN でホストされているボリュームに直接接続されている場合にサポートされます。  

-   **単一インスタンス記憶域**: Configuration Manager では、単一インスタンス記憶域 (SIS) が有効なボリューム上の配布ポイント パッケージと署名フォルダーの構成はサポートされていません。  

     さらに、Configuration Manager のクライアントのキャッシュは、SIS が有効なボリュームではサポートされていません。  

-   **リムーバブル ディスク ドライブ**: Configuration Manager では、リムーバブル ディスク ドライブへの Configuration Manager サイト システムまたはクライアントのインストールはサポートされていません。  

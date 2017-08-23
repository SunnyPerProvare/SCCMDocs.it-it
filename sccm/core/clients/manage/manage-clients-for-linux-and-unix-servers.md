---
title: "Linux および UNIX クライアントを管理する | Microsoft Docs"
description: "System Center Configuration Manager で Linux および UNIX サーバーのクライアントを管理します。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 948664f2-239d-47a8-92fc-f8efeebd5796
caps.latest.revision: "7"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 506df4f7c7baa5f0586a1ddf0cb02b3de9f4d076
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-manage-clients-for-linux-and-unix-servers-in-system-center-configuration-manager"></a>System Center Configuration Manager で Linux および UNIX サーバーのクライアントを管理する方法

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager で Linux および UNIX サーバーを管理する場合、サーバーを管理しやすいように、コレクション、メンテナンス期間、およびクライアント設定を構成できます。 また、Linux および UNIX 用の Configuration Manager クライアントにはユーザー インターフェイスがありませんが、クライアントにクライアント ポリシーの手動ポーリングを強制することもできます。

##  <a name="BKMK_CollectionsforLnU"></a> Collections of Linux and UNIX servers  
 コレクションを使用して Linux および UNIX サーバーのグループを管理する方法は、コレクションで他のクライアントの種類を管理する方法と同じです。 コレクションとして使用できるのは、ダイレクト メンバーシップ コレクションまたはクエリ ベースのコレクションです。 クエリ ベースのコレクションでは、クライアント オペレーティング システム、ハードウェア構成、またはサイト データベースに格納されているクライアントに関するその他の詳細情報を識別します。 たとえば、Linux および UNIX サーバーを含むコレクションを使用すると、次の設定を管理できます。  

-   クライアント設定  

-   ソフトウェアの展開  

-   メンテナンス期間の適用  

 Linux または UNIX クライアントをそのオペレーティング システムまたはディストリビューションによって特定するには、そのクライアントから[ハードウェア インベントリ](../../../core/clients/manage/inventory/hardware-inventory-for-linux-and-unix.md)を収集しておく必要があります。  

 ハードウェア インベントリの既定のクライアント設定には、クライアント コンピューターのオペレーティング システムに関する情報が含まれます。 **オペレーティング システム** クラスの **キャプション** プロパティを使用すると、Linux または UNIX サーバーのオペレーティング システムを特定できます。  

 Linux および UNIX 用の Configuration Manager クライアントを実行しているコンピューターに関する詳細は、Configuration Manager コンソールの **[資産とコンプライアンス]** ワークスペースの **[デバイス]** ノードで確認できます。 Configuration Manager コンソールの **[資産とコンプライアンス]** ワークスペースでは、**[オペレーティング システム]** 列に、各コンピューターのオペレーティング システムの名前が表示されます。  

 既定では、Linux および UNIX サーバーは、 **[すべてのシステム]** コレクションのメンバーです。 Linux および UNIX サーバーのみが含まれるカスタム コレクション、またはそのコレクションのサブセットを作成することをお勧めします。 カスタム コレクションでは、展開の成功を正確に判断できるように、ソフトウェアを展開する、同じようなコンピューターのグループにクライアント設定を割り当てるなどの操作を管理できます。   

 Linux および UNIX サーバーのカスタム コレクションを作成する場合は、オペレーティング システム属性のキャプション属性が含まれるメンバーシップの規則クエリを追加します。 コレクションを作成する方法については、「[System Center Configuration Manager でコレクションを作成する方法](../../../core/clients/manage/collections/create-collections.md)」を参照してください。  

##  <a name="BKMK_MaintenanceWindowsforLnU"></a> Maintenance windows for Linux and UNIX servers  
 Linux および UNIX サーバー用の Configuration Manager クライアントでは、[メンテナンス期間](../../../core/clients/manage/collections/use-maintenance-windows.md)を使用できます。 このサポートは、Windows ベースのクライアントから変更されていません。  

##  <a name="BKMK_ClientSettingsforLnU"></a> Client settings for Linux and UNIX servers  
 Linux および UNIX サーバーに適用される[クライアント設定](../../../core/clients/deploy/configure-client-settings.md)は、他のクライアントの設定と同じ方法で構成できます。  

 既定では、 **[既定のクライアント エージェント設定]** が Linux および UNIX サーバーに適用されます。 また、カスタムのクライアント設定を作成し、特定のクライアントのコレクションに展開できます。  

 Linux および UNIX クライアントにのみ適用される追加のクライアント設定はありません。 ただし、Linux および UNIX クライアントに適用されない既定のクライアント設定は存在します。 Linux と UNIX のクライアントは、それがサポートする機能の設定のみを適用します。  

 たとえば、リモート コントロール設定を有効にし、構成するカスタムのクライアント デバイス設定は、Linux サーバーと UNIX サーバーでは無視されます。Linux と UNIX のクライアントはリモート コントロールをサポートしないためです。  

##  <a name="BKMK_PolicyforLnU"></a> Computer policy for Linux and UNIX servers  
 Linux および UNIX サーバーのクライアントは、そのサイトを定期的にポーリングしてコンピューター ポリシーを確認し、要求された構成に関する詳細情報を取得して、展開をチェックします。  

 Linux または UNIX サーバーのクライアントにコンピューター ポリシーのポーリングを直ちに実行するように強制することもできます。 それを実行するには、サーバーで **ルート** 資格情報を使用して、 **/opt/microsoft/configmgr/bin/ccmexec -rs policy**コマンドを実行します。  

 コンピューター ポリシーのポーリングの詳細が、共有クライアントのログ ファイル **scxcm.log**に入力されます。  

> [!NOTE]  
>  Linux および UNIX 用の Configuration Manager クライアントによって、ユーザー ポリシーの要求や処理が実行されることはありません。  

##  <a name="BKMK_ManageLinuxCerts"></a> How to manage certificates on the client for Linux and UNIX  
 Linux および UNIX 用のクライアントをインストールした後、 **certutil** ツールを使用して、新しい PKI 証明書でクライアントを更新し、新しい証明書失効リスト (CRL) をインポートできます。 Linux および UNIX 用のクライアントをインストールするとき、このツールは **/opt/microsoft/configmgr/bin/certutil** に配置されます。 

 証明書を管理するには、各クライアントで、次のいずれかのオプションを指定して certutil を実行します。  

|オプション|説明|  
|------------|----------------------|  
|importPFX|このオプションを使用すると、証明書を指定して、クライアントが現在使用している証明書と置き換えることができます。<br /><br /> **-importPFX** を使用する場合は、**-password** コマンド ライン パラメーターを使って、PKCS#12 ファイルに関連付けられているパスワードを指定する必要もあります。<br /><br /> 追加のルート証明書の要件を指定するには、 **-rootcerts** を使用します。<br /><br /> 例: **certutil -importPFX &lt;Path to the PKCS#12 certificate> -password &lt;Certificate password\> [-rootcerts &lt;証明書のコンマ区切りの一覧>]**|  
|-importsitecert|このオプションを使用すると、管理サーバー上にあるサイト サーバー署名証明書を更新できます。<br /><br /> 例: **certutil -importsitecert &lt;DER 証明書のパス\>**|  
|-importcrl|このオプションを使用すると、1 つ以上の CRL ファイル パスを指定してクライアント上の CRL を更新できます。<br /><br /> 例: **certutil -importcrl &lt;CRL ファイル パスのコンマ区切りの一覧\>**|  

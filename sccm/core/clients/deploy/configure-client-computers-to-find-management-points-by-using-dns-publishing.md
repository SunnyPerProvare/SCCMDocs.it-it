---
title: "DNS 発行を使用して管理ポイントを検出するようにクライアント コンピューターを構成する | Microsoft Docs"
description: "System Center Configuration Manager で DNS 発行を使用して、管理ポイントを検出するようにクライアント コンピューターを設定します。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 03cec407-0f9f-454f-a360-b005af738d29
caps.latest.revision: "6"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d016ec3fe106b2d90b3c14b4f9296aed4d198644
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-client-computers-to-find-management-points-by-using-dns-publishing-in-system-center-configuration-manager"></a>System Center Configuration Manager で DNS 発行を使用して、管理ポイントを検出するようにクライアント コンピューターを構成する方法

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のクライアントは、サイトの割り当てを完了しても、実行中のプロセスとして管理対象にとどまるために、管理ポイントを特定する必要があります。 Active Directory ドメイン サービスは、イントラネット上のクライアントが管理ポイントを見つけるのに最も安全な方法を提供します。 しかし、クライアントがこのサービスの場所検索方法を利用できない場合は (たとえば Active Directory スキーマを拡張していない、クライアントがワークグループに所属するなど)、DNS 発行を代替方法として使用します。  

> [!NOTE]  
>  Linux および UNIX 用のクライアントをインストールする場合、最初の接続ポイントとして使用する管理ポイントを使用する必要があります。 Linux と UNIX でクライアントをインストールする方法については、「[System Center Configuration Manager で UNIX および Linux サーバーにクライアントを展開する方法](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md)」を参照してください。  

 管理ポイント用に DNS 発行を使用する前に、イントラネット上の DNS サーバーがそのサイトの管理ポイントについて、サービスの場所のリソース レコード (SRV RR) とそれに対応するホスト (A または AAA) のリソース レコードを持っていることを確認してください。 このサービスの場所リソース レコードは、Configuration Manager で自動的に作成することもできますが、DNS でレコードを作成する DNS 管理者によって手動で作成することもできます。  

 Configuration Manager クライアントに対するサービスの場所の検索方法として DNS 発行を使用する方法については、「[クライアントが System Center Configuration Manager のサイト リソースやサービスを検索する方法を理解する](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md)」を参照してください。  

 既定では、クライアントは、クライアントの DNS ドメインで、管理ポイント用の DNS を検索します。 ただし、クライアントのドメインに発行されている管理ポイントが存在しない場合、手動でクライアントに管理ポイントの DNS サフィックスを構成する必要があります。 このクライアントの DNS サフィックスは、クライアントのインストール中、またはインストール後に構成できます。  

-   クライアントのインストール中に、クライアントに管理ポイントのサフィックスを構成するには、CCMSetup Client.msi プロパティを構成します。  

-   クライアントのインストール後に、クライアントに管理ポイントのサフィックスを構成するには、コントロールパネルで、[ **Configuration Manager のプロパティ** ] を構成します。  

#### <a name="to-configure-clients-for-a-management-point-suffix-during-client-installation"></a>クライアントのインストール中に、クライアントに管理ポイントのサフィックスを構成するには  

-   次の CCMSetup client.msi プロパティを使用してクライアントをインストールします。  

    -   **DNSSUFFIX=** *&lt;管理ポイント ドメイン\>*  

         サイトに複数の管理ポイントがあり、その管理ポイントが複数のドメインに存在する場合は、一つのドメインだけを指定します。 このドメインの管理ポイントにクライアントが接続すると、クライアントは、使用可能な管理ポイントの一覧をダウンロードします。この一覧には、ほかのドメインにある管理ポイントも含まれます。  

     CCMSetup のコマンドライン プロパティの詳細については、「[System Center Configuration Manager のクライアント インストール プロパティについて](../../../core/clients/deploy/about-client-installation-properties.md)」をご覧ください。  

#### <a name="to-configure-clients-for-a-management-point-suffix-after-client-installation"></a>クライアントのインストール後に、クライアントに管理ポイントのサフィックスを構成するには  

1.  クライアント コンピューターのコントロール パネルで、 **Configuration Manager**に移動し、[ **プロパティ**] をダブルクリックします。  

2.  [ **サイト** ] タブで管理ポイントの DNS サフィックスを指定してから、[ **OK** ] をクリックします。  

     サイトに複数の管理ポイントがあり、その管理ポイントが複数のドメインに存在する場合は、一つのドメインだけを指定します。 このドメインの管理ポイントにクライアントが接続すると、クライアントは、使用可能な管理ポイントの一覧をダウンロードします。この一覧には、ほかのドメインにある管理ポイントも含まれます。

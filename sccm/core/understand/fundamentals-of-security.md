---
title: "セキュリティの基礎 | Microsoft Docs"
description: "System Center Configuration Manager のセキュリティ層について説明します。"
ms.custom: na
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: df3198885259b1db4a1aadee0db6512a1a2d4911
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="fundamentals-of-security-for-system-center-configuration-manager"></a>System Center Configuration Manager のセキュリティの基礎

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のセキュリティは、複数の階層で構成されています。 オペレーティング システムとネットワークの両方に、Windows セキュリティ機能によって最初の層が提供されます。この層には、以下のものが含まれます。  

-   Configuration Manager コンポーネント間でファイルを転送するためのファイル共有。  

-   ファイルとレジストリ キーの保護に役立つアクセス制御リスト (ACL)。  

-   通信の保護に役立つインターネット プロトコル セキュリティ (IPsec)。  

-   セキュリティ ポリシーを設定するためのグループ ポリシー。  

-   Configuration Manager コンソールなど、配布されたアプリケーションの分散コンポーネント オブジェクト モデル (DCOM) アクセス許可。  

-   セキュリティ プリンシパルを保存するための Active Directory Domain Services。  

-   Configuration Manager セットアップ中に作成された一部のグループを含む、Windows アカウント セキュリティ。  

さらにファイアウォールや侵入検出などのセキュリティ コンポーネントを使用することで、環境全体を防御することができます。 業界標準の公開キー基盤 (PKI) 実装で発行される証明書により、認証、署名および暗号化が可能になります。  

Windows Server とネットワーク インフラストラクチャによって提供されるセキュリティだけでなく、いくつかの方法で、Configuration Manager によって Configuration Manager コンソールとそのリソースへのアクセスが制御されます。 既定では、Configuration Manager コンソールがインストールされているコンピューター上でコンソールを実行するために必要なファイルおよびレジストリ キーへのアクセス権は、ローカル管理者のみにあります。  

次のセキュリティ階層は、Windows Management Instrumentation (WMI) によるアクセスに基づいています。これは SMS プロバイダーに特有のものです。 SMS プロバイダーは、サイト データベースの情報を照会するためのユーザー アクセスを付与する Configuration Manager コンポーネントです。 既定では、プロバイダーへのアクセスは、ローカルの SMS 管理グループのメンバーに限定されています。 このグループには最初のうち、Configuration Manager をインストールしたユーザーのみが含まれています。 他のアカウントに Common Information Model (CIM) リポジトリおよび SMS プロバイダーへのアクセス許可を与えるには、SMS 管理グループに他のアカウントを追加します。  

最後のセキュリティ階層は、サイト データベース内のオブジェクトに対するアクセス許可に基づいています。 既定では、Configuration Manager をインストールする際に使用したローカル システム アカウントおよびユーザー アカウントは、サイト データベース内のすべてのオブジェクトを管理できます。 Configuration Manager コンソールで、ロール ベース管理を使用すると、追加の管理ユーザーに対してアクセス許可を付与したり、制限したりすることができます。  



## <a name="role-based-administration"></a>役割に基づいた管理  
 Configuration Manager では、ロール ベース管理を使用して、オブジェクト (コレクション、展開、サイトなど) を保護できます。 この管理モデルは、階層内のすべてのサイトのセキュリティのアクセス権の設定およびサイトの設定を一元的に定義および管理します。 セキュリティ ロールは、管理ユーザーとグループのアクセス許可に割り当てられます。 アクセス許可は、クライアント設定の作成または変更に使用されるアクセス許可など、さまざまな Configuration Manager オブジェクトの種類に関連しています。 セキュリティ スコープは、管理ユーザーが管理を担当する特定のオブジェクトのインスタンス (Microsoft Office をインストールするアプリケーションなど) をグループ化します。 セキュリティ ロール、セキュリティ スコープ、およびコレクションの組み合わせによって、管理ユーザーが表示および管理できるオブジェクトが定義されます。 Configuration Manager は、一般的な管理タスクのためにいくつかの既定のセキュリティ ロールをインストールします。 ただし、独自のセキュリティ ロールを作成して、特定のビジネスの要件をサポートすることができます。  

 詳細については、「[Configure role-based administration for System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)」(System Center Configuration Manager の役割ベースの管理の構成) を参照してください。  

## <a name="securing-client-endpoints"></a>クライアント エンドポイントの保護  
 サイト システムの役割へのクライアント通信は、自己署名入り証明書、または PKI 証明書を使用して保護されます。 PKI 証明書は、Configuration Manager がインターネット上にあると見なしたコンピューター クライアントと、モバイル デバイス クライアントに対して使用する必要があります。 PKI 証明書では HTTPS を使用して、クライアント エンドポイントを保護します。 クライアントが接続するサイト システムの役割は、HTTPS または HTTP を使用してクライアント通信を行うように構成できます。 クライアント コンピューターは、使用可能な最も安全な方法を使用して常に通信を行います。 クライアント コンピューターは、HTTP 通信を許可するサイト システムの役割がある場合にのみ、安全性が劣るイントラネットでの HTTP による通信方法を代替で使用します。  

 詳細については、「[System Center Configuration Manager の暗号化コントロールのテクニカル リファレンス](../../protect/deploy-use/cryptographic-controls-technical-reference.md)」を参照してください。  

## <a name="configuration-manager-accounts-and-groups"></a>Configuration Manager のアカウントとグループ  
 Configuration Manager では、ほとんどのサイト操作にローカル システム アカウントを使用します。 いくつかの管理タスクでは、追加のアカウントを作成して管理する必要がある場合があります。 いくつかの既定のグループと SQL Server の役割がセットアップ時に作成されます。 既定のグループと SQL Server の役割には、コンピューターまたはユーザー アカウントを手動で追加する必要がある場合があります。  

 詳細については、「[System Center Configuration Manager で使用されるアカウント](../../core/plan-design/hierarchy/accounts.md)」を参照してください。  

## <a name="privacy"></a>プライバシー  
 多くのクライアントを効果的に管理できるため、エンタープライズ管理製品には多くの利点がありますが、このソフトウェアが組織のユーザーのプライバシーに影響を与える可能性について注意する必要があります。 System Center Configuration Manager にはデータを収集してデバイスを監視するための多くのツールが備わっています。 一部のツールではプライバシーの問題が生じる可能性があります。  

 たとえば、構成マネージャー クライアントをインストールすると、既定で多数の管理設定が有効になります。 これにより、クライアント ソフトウェアから情報が Configuration Manager サイトに送信されます。 クライアント情報は Configuration Manager データベースに格納され、Microsoft に送信されることはありません。 System Center Configuration Manager を実装する前に、プライバシー要件について検討してください。  

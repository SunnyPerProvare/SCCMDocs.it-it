---
title: "オンプレミス MDM の計画 | Microsoft Docs"
description: "System Center Configuration Manager でモバイル デバイスを管理するために、オンプレミス モバイル デバイス管理を計画します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
caps.latest.revision: "9"
caps.handback.revision: "0"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 544c3bea0c7df96887ee1717f061c39c64b82d01
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>System Center Configuration Manager でのオンプレミス モバイル デバイス管理の計画

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager のインフラストラクチャでオンプレミス モバイル デバイス管理を処理する場合、次の要件を考慮します。

##  <a name="bkmk_devices"></a> サポートされるデバイス  
 オンプレミス モバイル デバイス管理を使用すると、デバイスのオペレーティング システムに組み込まれている管理機能を使用してモバイル デバイスを管理できます。  管理機能は、Open Mobile Alliance (OMA) Device Management (DM) 標準に基づいており、多くのデバイス プラットフォームでは、この標準を使用して、デバイスを管理できます。  これらを (ドキュメントおよび Configuration Manager コンソールのユーザー インターフェイスの) **最新のデバイス**と呼び、管理するために Configuration Manager クライアントを必要とするその他のデバイスと区別します。  

 > [!NOTE]  
>  Configuration Manager の現在のブランチでは、次のオペレーティング システムを実行しているデバイスをオンプレミス モバイル デバイス管理で登録することができます。  
>   
> -  Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team\( Configuration Manager バージョン 1602 以降\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise
> -   Windows 10 IoT Enterprise   

##  <a name="bkmk_intune"></a> Microsoft Intune サブスクリプションの使用  
 オンプレミス モバイル デバイス管理の使用を開始するには、Microsoft Intune のサブスクリプションが必要です。 このサブスクリプションは、デバイスのライセンスの追跡にのみ必要のみがあり、デバイスの管理情報の管理や格納には使用されません。 すべての管理は、オンプレミスの Configuration Manager インフラストラクチャを使用して組織のエンタープライズで処理されます。  

 > [!NOTE]  
 > バージョン 1610 以降の Configuration Manager では、Microsoft Intune とオンプレミスの Configuration Manager インフラストラクチャの両方を同時に使用してモバイル デバイスを管理できます。   

 サイトにインターネット接続があるデバイスがある場合、Intune サービスを使用して、ポリシーの更新のデバイス管理ポイントを確認するようデバイスに通知することができます。 Intune のこの使用は、インターネットに接続されたデバイスの通知のみに限定されます。 インターネット接続のないデバイス (Intune が接続できない) は、管理機能のサイト システムの役割を使用してチェックインする場合に、構成されたポーリング間隔に依存します。  

> [!TIP]  
>  サイト システムの役割をセットアップする前に、Intune をセットアップすることをお勧めします。これにより、サイト システムの役割が機能するまでにかかる時間を最小化できます。  

 Intune サブスクリプションのセットアップ方法については、「[System Center Configuration Manager でのオンプレミスのモバイル デバイス管理のために Microsoft Intune サブスクリプションをセットアップする](../../mdm/get-started/set-up-intune-subscription-on-premises-mdm.md)」を参照してください。  

##  <a name="bkmk_roles"></a> 必要なサイト システムの役割  
 オンプレミス モバイル デバイス管理には、次のサイト システムの役割がそれぞれ 1 つ以上必要です。  

-   **登録プロキシ ポイント** 。登録要求をサポートします。  

-   **登録ポイント** 。デバイスの登録をサポートします。  

-   **デバイス管理ポイント** 。ポリシー配信用です。 このサイト システムの役割は、モバイル デバイス管理を許可するように構成されている管理ポイントの役割のバリエーションの 1 つです。  

-   **配布ポイント** 。コンテンツ配信用です。  

-   **サービス接続ポイント**。Intune に接続して、ファイアウォールの外側のデバイスに通知します。  

 これらのサイト システムの役割は、1 つのサイト システム サーバーにインストールできます。または、組織のニーズに応じて、異なるサーバー上で別々に実行することができます。 オンプレミス モバイル デバイス管理で使用される各サイト システム サーバーは信頼されているデバイスと通信するための HTTPS エンドポイントとして構成する必要があります。 詳細については、「 [必要な信頼された通信](#bkmk_trustedComs)」をご覧ください。  

 サイト システムの役割の計画の詳細については、「[System Center Configuration Manager のサイト システム サーバーとサイト システムの役割の計画](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md)」を参照してください。  

 必要なサイト システムの役割の追加方法の詳細については、「[System Center Configuration Manager でのオンプレミス モバイル デバイス管理のサイト システムの役割のインストール](../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)」を参照してください。  

##  <a name="bkmk_trustedComs"></a> 必要な信頼された通信  
 オンプレミス モバイル デバイス管理では、HTTPS 接続用にサイト システムの役割を有効にする必要があります。 必要に応じて、エンタープライズ証明機関 (CA) を使用して、サーバーとデバイスの間で信頼された接続を確立するか、または信頼された機関として一般的に利用できる CA を使用することができます。  いずれの場合も、必要なサイト システムの役割をホストしているサイト システム サーバー上で、IIS を使用して Web サーバー証明書を構成する必要があります。また、それらのサーバーに接続する必要があるデバイスにインストールされる、その CA のルート証明書が必要です。  

 信頼された通信を確立するためにエンタープライズ CA を使用する場合は、次のタスクを実行する必要があります。  

-   CA で Web サーバー証明書テンプレートを作成および発行します。  

-   必要なサイト システムの役割をホストする各サイト システム サーバー用の Web サーバー証明書を要求します。  

-   要求された Web サーバー証明書を使用するサイト システム サーバーで IIS を構成します。  

 企業の Active Directory ドメインに参加しているデバイスの場合、信頼された接続用のデバイスでは、エンタープライズ CA のルート証明書が既に使用可能です。 これは、ドメインに参加しているデバイス (デスクトップ コンピューターなど) がサイト システム サーバーとの HTTPS 接続で自動的に信頼されることを示します。 ただし、ドメインに参加していないデバイス (通常、モバイル) には、必要なルート証明書がインストールされていません。 これらのデバイスには、オンプレミス モバイル デバイス管理をサポートするサイト システム サーバーと正常に通信するためにルート証明書を手動でインストールする必要があります。  

 個々 のデバイスで使用する発行元 CA のルート証明書をエクスポートする必要があります。 ルート証明書ファイルを取得するには、CA を使用してエクスポートするか、または簡単な方法として、CA によって発行された Web サーバー証明書を使用して、ルートを抽出し、ルート証明書ファイルを作成します。   その後、ルート証明書をデバイスに配信する必要があります。  次に配信方法の例をいくつか示します。  

-   ファイル システム  

-   電子メールの添付ファイル  

-   メモリ カード  

-   テザリングされたデバイス  

-   クラウドの記憶域 (OneDrive など)  

-   近距離無線通信 (NFC) 接続  

-   バーコード スキャナ  

-   Out of Box Experience (OOBE) プロビジョニング パッケージ  

 詳細については、「 [Set up certificates for trusted communications for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)」をご覧ください。  

##  <a name="bkmk_enrollment"></a> 登録の注意事項  
 オンプレミス モバイル デバイス管理のデバイスの登録を有効にするには、登録する権限がユーザーに付与され、かつ、ユーザーのデバイスが、必要なサイト システムの役割をホストするサイト システム サーバーとの信頼された通信を行うことができる必要があります。  

 ユーザーへの登録権限の付与は、Configuration Manager クライアントの設定で登録プロファイルを設定することによって行います。 既定のクライアント設定を使用して、検出されたすべてのユーザーに、登録プロファイルをプッシュするか、またはカスタム クライアント設定で、登録プロファイルを設定して、設定を 1 つまたは複数のユーザー コレクションにプッシュできます。  

 ユーザー登録権限が付与されたユーザーは、自分のデバイスを登録できます。 登録するには、ユーザーのデバイスに、Web サーバー証明書 (必要なサイト システムの役割をホストするサイト システム サーバーで使用されるもの) を発行した証明機関 (CA) のルート証明書がある必要があります。  

 ユーザーによる登録の代わりに、ユーザーの介入なしにデバイスを登録できる一括登録パッケージを設定することができます。 このパッケージは、デバイスが使用するために最初にプロビジョニングされる前、またはデバイスで OOBE プロセスを実行した後に、デバイスに配布することができます。  

 デバイスを設定および登録する方法の詳細については、次を参照してください。  

-   [System Center Configuration Manager でのオンプレミスのモバイル デバイス管理のデバイス登録の設定](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)  

-   [System Center Configuration Manager でのオンプレミス モバイル デバイス管理の対象となるデバイスの登録](../../mdm/deploy-use/enroll-devices-on-premises-mdm.md)  

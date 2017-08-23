---
title: "サポートされる Active Directory ドメイン |Microsoft ドキュメント"
description: "Active Directory ドメインで System Center Configuration Manager サイト システムのメンバーシップの要件を取得します。"
ms.custom: na
ms.date: 3/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8c5a13f8-42d5-4898-b7b6-e594dae8b335
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 2654ab4eaaaf6a4bf3bd7dca9908e7033647dc2c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="supported-active-directory-domains-for-system-center-configuration-manager"></a>System Center Configuration Manager のサポートされる Active Directory ドメイン

*適用対象: System Center Configuration Manager (Current Branch)*

すべての System Center Configuration Manager サイト システムは、サポートされている Windows Server Active Directory ドメインのメンバーであることが必要です。 Configuration Manager クライアント コンピューターは、ドメインのメンバー、またはワークグループのメンバーになれます。  

 **要件と制限事項**  

-   ドメイン メンバーシップは、境界ネットワーク (DMZ、非武装地帯、スクリーン サブネットとも呼ばれます) でインターネット ベースのクライアント管理をサポートするサイト システムに適用されます。  

-   サイト システムの役割をホストするコンピューターでは、次の変更はサポートされていません。  

    -   ドメインのメンバーシップ  

    -   ドメイン名  

    -   コンピューター名  

これらの変更を加える前に、サイト システムの役割 (サイト サーバーの場合はサイトを含む) をアンインストールする必要があります。  

**次に示すドメインの機能レベルを持つドメインがサポートされています。**  
- Windows Server 2016

- Windows Server 2012 R2  

- Windows Server 2012

- Windows Server 2008 R2

- Windows Server 2008  







##  <a name="bkmk_Disjoint"></a> 不整合のある名前空間  
Configuration Manager は、名前空間に不整合があるドメイン内でのサイト システムおよびクライアントのインストールをサポートしています。  

不整合のある名前空間のシナリオとは、あるコンピューターのプライマリ ドメイン ネーム システム (DNS) のサフィックスが、そのコンピューターの属する Active Directory DNS ドメイン名と一致しないという状況のことです。 矛盾するプライマリ DNS のサフィックスを使用するコンピューターは、不整合であると考えられます。 それとは別の不正後のある名前空間のシナリオは、ドメイン コントローラーの NetBIOS ドメイン名が Active Directory DNS ドメイン名と一致しない場合に発生します。  

次の表に、不整合のある名前空間についてサポートされるシナリオを記載します。  

|通信の種類|説明|  
|--------------|----------------------|  
|**シナリオ 1 :**<br /><br /> ドメイン コントローラーのプライマリ DNS サフィックスが、Active Directory DNS ドメイン名と異なっています。 ドメインのメンバーであるコンピューターは、不整合になることも、不整合にならないこともあります。|このシナリオでは、ドメイン コントローラーのプライマリ DNS サフィックスが、Active Directory DNS ドメイン名と異なっています。 このシナリオのドメイン コントローラーは不整合になります。 ドメインのメンバーであるコンピューター (サイト サーバーやコンピューターなど) のプライマリ DNS サフィックスは、ドメイン コントローラーのプライマリ DNS サフィックスと一致するか、Active Directory DNS ドメイン名に一致するかのどちらかになります。|  
|**シナリオ 2 :**<br /><br /> Active Directory ドメイン内のメンバー コンピューターには不整合があるにもかかわらず、ドメイン コントローラーには不整合がありません。|このシナリオでは、サイト システムがインストールされたメンバー コンピューターのプライマリ DNS サフィックスが Active Directory DNS ドメイン名と異なっているにもかかわらず、ドメイン コントローラーのプライマリ DNS サフィックスは Active Directory DNS ドメイン名と同じになっています。 このシナリオでは、不整合のないドメイン コントローラーと、不整合のあるメンバー コンピューターが存在します。 Configuration Manager クライアントを実行しているメンバー コンピューターは、不整合のあるサイト システム サーバーのプライマリ DNS サフィックス、または Active Directory DNS ドメイン名のどちらかに一致するプライマリ DNS サフィックスを持ちます。|  

 不整合のあるドメイン コントローラーにコンピューターがアクセスできるようにするには、ドメイン オブジェクト コンテナーの **msDS-AllowedDNSSuffixes** Active Directory 属性を変更する必要があります。 この属性に両方の DNS サフィックスを追加する必要があります。  

 さらに、組織内に展開されたすべての DNS 名前空間が DNS サフィックス検索一覧に含まれていることを確認して、不整合があるドメイン内のコンピューターごとに検索一覧を構成する必要があります。 名前空間の一覧に、ドメイン コントローラーのプライマリ DNS サフィックス、DNS ドメイン名、および Configuration Manager と相互運用する可能性のあるその他のサーバーに対応する追加の名前空間を含まれていることを確認します。 グループ ポリシー管理コンソールを使用すると、 **ドメイン ネーム システム (DNS) サフィックス検索** 一覧を構成できます。  

> [!IMPORTANT]  
>  Configuration Manager でコンピューターを参照する場合は、プライマリ DNS サフィックスを使用してコンピューターを入力します。 このサフィックスは、 **dnsHostName** 属性として Active Directory ドメインに登録した完全修飾ドメイン名と一致し、およびシステムに関連付けられたサービス プリンシパル名と一致する必要があります。  

##  <a name="bkmk_SLD"></a> 単一ラベルのドメイン  
 Configuration Manager は、次に示す条件が満たされたときには、単一ラベルのドメイン内のサイト システムとクライアントをサポートします。  

-   Active Directory Domain Services の単一ラベルのドメインは、有効な最上位ドメインを持つ不整合がある DNS 名前空間で構成する必要があります。  

     **例:** 単一ラベルのドメインである Contoso は、DNS の不整合のある名前空間 contoso.com を持つように構成されています。 そのため、Configuration Manager で Contoso ドメイン内のコンピューターに DNS サフィックスを指定するときには、"Contoso" ではなく "Contoso.com" を指定します。  

-   システム コンテキストでのサイト サーバー間の分散コンポーネント オブジェクト モデル (DCOM) 接続は、Kerberos 認証を使用して正常に実行できる必要があります。  

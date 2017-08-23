---
title: "データとサイト インフラストラクチャの保護 | Microsoft Docs"
description: "System Center Configuration Manager で組織のリソースを漏洩や悪意のある攻撃から保護する方法について説明します。"
ms.custom: na
ms.date: 11/27/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2117f786-d521-4790-9e8d-ec096c63c9d7
caps.latest.revision: "8"
author: Robstack
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d527cb4bfb55ca50c8d2a0fed7c427af5747fe99
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="protect-data-and-site-infrastructure-with-system-center-configuration-manager"></a>System Center Configuration Manager でのデータとサイト インフラストラクチャの保護

*適用対象: System Center Configuration Manager (Current Branch)*


インフラストラクチャとデータの両方が公開や悪意のある攻撃から保護されるように、ユーザーが組織のリソースに安全にアクセスできるようにします。 これらのトピックでは、System Center Configuration Manager (ConfigMgr、SCCM とも呼ばれます) を使用して、安全にアクセスできるようにする方法と、組織のリソースを保護する方法について説明します。  

-   VPN プロファイルを使用して VPN 接続を有効にすると、企業リソースに接続するためのユーザーの作業を最小化できます。 詳細については、「[System Center Configuration Manager の VPN プロファイル](../deploy-use/vpn-profiles.md)」を参照してください。  

-   Wi-Fi プロファイルには、組織内のデバイス用にワイヤレス ネットワーク設定を作成して展開し、監視するためのツールとリソースが用意されています。 この設定を展開することにより、エンド ユーザーが会社のワイヤレス ネットワークに接続するときの手間をできるだけ省きます。 詳細については、「[System Center Configuration Manager の Wi-Fi プロファイル](/sccm/protect/deploy-use/create-wifi-profiles)」を参照してください。  

-   「[System Center Configuration Manager の証明書プロファイル](../deploy-use/introduction-to-certificate-profiles.md)」では、会社のリソースへの接続に必要な証明書を持つユーザーのデバイスをプロビジョニングする方法について説明します。  

-   [System Center Endpoint Protection](../deploy-use/endpoint-protection.md) を使用して、クライアント コンピューターのマルウェア対策ポリシーと Windows ファイアウォールのセキュリティを管理できます。  

-   「[System Center Configuration Manager でサービスへのアクセスを管理する](../deploy-use/manage-access-to-services.md)」の説明に従って、条件付きアクセスを使用することにより、Microsoft Intune に登録されているデバイスで、電子メールやその他のサービスをセキュリティで保護できます。  

-   電子メール プロファイルは、デバイスでの電子メール設定の作成、展開、監視を支援する一連のツールとリソースを提供する拡張機能です。 これにより、ユーザーは最小限の設定で個人のデバイスから会社の電子メールにアクセスできるようになります。 詳細については、「[System Center Configuration Manager の電子メール プロファイル](../deploy-use/introduction-to-email-profiles.md)」を参照してください。  

-   Configuration Manager で、Windows Hello for Business (旧称 Microsoft Passport for Work) を統合できます。これは Active Directory や Azure Active Directory アカウントを使った代替サインイン方法であり、パスワード、スマート カード、または仮想スマート カードに取って代わります。 詳細については、「[System Center Configuration Manager における Windows Hello for Business 設定について](../deploy-use/windows-hello-for-business-settings.md)」を参照してください。  

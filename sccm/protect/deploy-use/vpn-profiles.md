---
title: "System Center Configuration Manager の VPN プロファイル | Microsoft Docs"
description: "System Center Configuration Manager の VPN プロファイルを使用して、VPN 設定を組織内のユーザーに展開する方法について説明します。"
ms.custom: na
ms.date: 11/27/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
caps.latest.revision: "6"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: e07a80c1a59043b74cda7219f78c5fef66989ba8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager の VPN プロファイル

*適用対象: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager (ConfigMgr または SCCM とも呼ばれます) の VPN プロファイルを使用して、VPN 設定を組織内のユーザーに展開します。 これらの設定を展開して、企業ネットワーク上のリソースに接続するために必要なエンド ユーザーの作業を最小化します。  

 たとえば、Windows RT オペレーティング システムを実行するすべてのデバイスに対して、企業ネットワーク上のファイル共有に接続するために必要な設定をプロビジョニングするとします。 企業ネットワークに接続するために必要な設定が含まれている VPN プロファイルを作成した後、階層内で Windows RT を実行するデバイスを持つすべてのユーザーにこのプロファイルを展開することができます。 Windows RT デバイスのユーザーには利用可能なネットワークの一覧で VPN 接続が表示されるため、最小限の作業でこのネットワークに接続できます。  

 VPN プロファイルを作成するときに、System Center Configuration Manager 証明書プロファイルを使用してプロビジョニングされた、サーバー検証用の証明書、クライアント認証用の証明書などの幅広いセキュリティ設定を含めることができます。 証明書プロファイルの詳細については、「[System Center Configuration Manager の証明書プロファイル](introduction-to-certificate-profiles.md)」を参照してください。  

 以下のセクションでは、Configuration Manager を使用している場合に、VPN プロファイルを使用して構成できるデバイスについて説明します。

 [モバイル デバイスの VPN プロファイル](/sccm/mdm/deploy-use/create-vpn-profiles)に関する記事を参照して、Microsoft Intune で Configuration Manager を使用する場合に構成できるデバイスを確認してください。  

## <a name="vpn-profiles-when-using-configuration-manager"></a>Configuration Manager を使用する場合の VPN プロファイル  
 次の表では、さまざまなデバイス プラットフォームに対して構成できる VPN プロファイルについて説明します。  

|接続の種類|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|  
|---------------------|-----------------|----------------|--------------------|----------------|  
|**Cisco AnyConnect**|いいえ|いいえ|いいえ|×|  
|**Pulse Secure**|○|×|[はい]|○|  
|**F5 Edge Client**|○|×|[はい]|○|  
|**Dell SonicWALL Mobile Connect**|○|×|[はい]|○|  
|**チェック ポイント モバイル VPN**|○|×|[はい]|○|  
|**Microsoft SSL (SSTP)**|○|[はい]|○|×|  
|**Microsoft 自動**|○|[はい]|○|×|  
|**IKEv2**|○|[はい]|○|いいえ|  
|**PPTP**|○|[はい]|○|いいえ|  
|**L2TP**|○|[はい]|○|いいえ|  

### <a name="next-steps"></a>次のステップ  
 Configuration Managerで VPN プロファイルの計画、構成、操作、およびメンテナンスを行うときに、次のトピックを参考にしてください。  

-   [System Center Configuration Manager の VPN プロファイルの前提条件](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [System Center Configuration Manager の VPN プロファイルのセキュリティとプライバシー](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)

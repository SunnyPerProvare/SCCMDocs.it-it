---
title: "Wi-Fi および VPN プロファイルのセキュリティとプライバシー | Microsoft Docs"
description: "System Center Configuration Manager でデバイスの Wi-Fi および VPN プロファイルを管理する場合のセキュリティのベスト プラクティスについて説明します。"
ms.custom: na
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
caps.latest.revision: "4"
caps.handback.revision: "0"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 6d1d0a393a2ce614ae5f819475bd47b05e699b45
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager の Wi-Fi および VPN プロファイルのセキュリティとプライバシー

*適用対象: System Center Configuration Manager (Current Branch)*

##  <a name="security-best-practices-for-wi-fi--and-vpn-profiles"></a>Wi-Fi および VPN プロファイルのセキュリティのベスト プラクティス  
 デバイスの Wi-Fi および VPN プロファイルを管理するときは、次のようなセキュリティのベスト プラクティスに従ってください。  

|セキュリティのベスト プラクティス|説明|  
|----------------------------|----------------------|  
|可能な場合、使用する Wi-Fi および VPN インフラストラクチャとクライアントのオペレーティング システムでサポートできる最も安全なオプションを選択します。|Wi-Fi および VPN プロファイルは、デバイスで既にサポートしている Wi-Fi および VPN 設定を中央から配付して管理するのに便利です。 Configuration Manager では、Wi-Fi および VPN 機能は追加されません。<br /><br /> デバイスとインフラストラクチャに推奨されるセキュリティ ベスト プラクティスを特定し、実装し、従います。|  

## <a name="privacy-information-for-wi-fi-profiles"></a>Wi-Fi プロファイルのプライバシー情報  
 Wi-Fi および VPN プロファイルを使って、クライアント デバイスと Wi-Fi および VPN サーバーとの接続を構成し、プロファイルの適用後に、それらのデバイスがコンプライアンスに対応しているかどうかを評価できます。 コンプライアンス対応情報は、管理ポイントからサイト サーバーに送信され、サイト データベースに保存されます。 情報はデバイスが管理ポイントに送信するときは暗号化されますが、サイト データベースに保存するときは暗号化されません。 データベースに保存された情報は、"期限切れの構成管理データの削除" というメンテナンス タスクで削除されるまで維持されます。 **** 情報が削除される既定の期限は 90 日ですが、変更することができます。 対応情報がマイクロソフトに送信されることはありません。  

 既定では、デバイスでは Wi-Fi および VPN プロファイルを評価しません。 また、プロファイルを構成してから、プロファイルをユーザーに展開する必要があります。  

 Wi-Fi または VPN プロファイルを構成する前に、プライバシー要件について検討してください。  

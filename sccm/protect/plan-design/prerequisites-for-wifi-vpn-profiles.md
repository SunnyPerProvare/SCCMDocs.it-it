---
title: "Wi-Fi および VPN プロファイルの前提条件 | Microsoft Docs"
description: "System Center Configuration Manager で証明書プロファイル、Wi-Fiプロファイル、および VPN プロファイルを管理するために必要なセキュリティ アクセス許可について説明します。"
ms.custom: na
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 309b0363f9b3ec4a31b8323b9e64c9f73060c281
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager の Wi-Fi プロファイルおよび VPN プロファイルの前提条件

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の Wi-Fi プロファイルおよび VPN プロファイルには、製品内の依存関係のみがあります。  

 証明書プロファイルや Wi-Fi プロファイル、VPN プロファイルなどの会社のリソースのアクセス設定を管理するには、次のセキュリティのアクセス許可が必要です。  

-   Wi-Fi プロファイルのアラートとレポートを表示して管理する場合: **アラート**オブジェクトの**作成**、**削除**、**変更**、**レポートの変更**、**読み取り**、**レポートの実行**。  

-   証明書プロファイルを作成して管理する場合: **証明書プロファイル**オブジェクトの **作成者ポリシー**、 **レポートの変更**、 **読み取り** 、 **レポートの実行** 。  

-   Wi-Fi プロファイル、証明書プロファイル、および VPN プロファイルの展開を管理する場合: **コレクション**オブジェクトの **構成ポリシーの展開**、 **クライアント ステータス アラートの変更**、 **読み取り** 、 **リソースの読み取り** 。  

-   すべての構成ポリシーを管理する場合: **構成のポリシー**オブジェクトの **作成**、 **削除**、 **変更**、 **読み取り** 、 **セキュリティ スコープの設定** 。  

-   Wi-Fi プロファイルおよび VPN プロファイルに関連するクエリを実行する場合: **クエリ** オブジェクトの**読み取り**アクセス許可。  

-   System Center Configuration Manager コンソールで Wi-Fiプロファイルおよび VPN プロファイル情報を表示する場合: **サイト** オブジェクトの**読み取り**アクセス許可。  

-   Wi-Fi プロファイルおよび VPN プロファイルのステータス メッセージを表示する場合: **ステータス メッセージ** オブジェクトの **読み取り** アクセス許可。  

-   信頼された証明機関証明書プロファイルを作成および変更する場合: **信頼された証明機関証明書プロファイル**オブジェクトの **作成者ポリシー**、 **レポートの変更**、 **読み取り** 、 **レポートの実行** 。  

-   VPN プロファイルを作成して管理する場合: **VPN プロファイル**オブジェクトの **作成者ポリシー**、 **レポートの変更**、 **読み取り** 、 **レポートの実行** 。  

-   Wi-Fi プロファイルを作成して管理する場合: **Wi-Fi プロファイル**オブジェクトの **作成者ポリシー**、 **レポートの変更**、 **読み取り** 、 **レポートの実行** 。  

 **[会社リソース アクセス マネージャー]** セキュリティ ロールには、System Center Configuration Manager で Wi-Fi プロファイルを管理するのに必要な上記のアクセス許可が付与されています。 詳細については、「[System Center Configuration Manager でのセキュリティの構成](../../core/plan-design/security/configure-security.md)」を参照してください。

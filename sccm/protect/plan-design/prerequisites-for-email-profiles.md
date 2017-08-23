---
title: "電子メール プロファイルの前提条件 | Microsoft Docs"
description: "System Center Configuration Manager の電子メール プロファイル、およびそれらの外部依存関係と製品内依存関係の両方について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dccf0b73-43bd-4545-8914-114168ebad36
caps.latest.revision: "5"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 451317db1d7aab888c03d1a099b9ce25311e06d0
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="email-profile-prerequisites"></a>電子メール プロファイルの前提条件

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の電子メール プロファイルには、外部依存関係と製品内依存関係の両方があります。  

## <a name="configuration-manager-dependencies"></a>Configuration Manager の依存関係  

|依存関係|説明|  
|----------------|----------------------|  
|電子メール プロファイルを管理するために、特定のセキュリティのアクセス許可が必要です。|電子メール プロファイルなどの会社リソース アクセス設定を管理するには、次のセキュリティ アクセス許可が必要です。<br /><br /> - 電子メール プロファイルのアラートとレポートを表示して管理する場合: **アラート** オブジェクトに対する**作成**、**削除**、**変更**、**レポートの変更**、**読み取り**、**レポートの実行**のアクセス許可。<br /><br /> - 証明書プロファイルを作成して管理する場合: **証明書プロファイル** オブジェクトに対する**作成者ポリシー**、**レポートの変更**、**読み取り**、**レポートの実行** のアクセス許可。<br /><br /> - 電子メール プロファイルの展開を管理する場合: **コレクション** オブジェクトに対する**構成ポリシーの展開**、**クライアント ステータス アラートの変更**、**読み取り**、**リソースの読み取り**のアクセス許可。<br /><br /> - すべての構成ポリシーを管理する場合: **構成ポリシー** オブジェクトに対する**作成**、**削除**、**変更**、**読み取り**、**セキュリティ スコープの設定**のアクセス許可。<br /><br /> - 電子メール プロファイルに関連するクエリを実行する場合: **クエリ** オブジェクトの**読み取り**アクセス許可。<br /><br /> - System Center Configuration Manager コンソールで証明書プロファイル情報を表示する場合: **サイト** オブジェクトの**読み取り**アクセス許可。<br /><br /> - 電子メール プロファイルのステータス メッセージを表示する場合: **ステータス メッセージ** オブジェクトの**読み取り**アクセス許可。<br /><br /> - 電子メール プロファイルを作成して管理する場合: **通信プロビジョニング プロファイル** オブジェクトに対する**作成者ポリシー**、**レポートの変更**、**読み取り**、**レポートの実行**のアクセス許可。<br /><br /> - **[会社リソース アクセス マネージャー]** セキュリティ ロールには、System Center Configuration Manager で電子メール プロファイルを管理するのに必要な上記のアクセス許可が付与されています。 詳細については、「[System Center Configuration Manager でのセキュリティの構成](../../core/plan-design/security/configure-security.md)」を参照してください。|  
|Active Directory のメール属性|電子メール プロファイルで、ユーザーのプライマリ SMTP アドレスを使用してユーザーの電子メール アドレスを生成する場合は、Active Directory から **メール** 属性を検索するためにSystem Center Configuration Manager ユーザー探索を構成する必要があります (既定で構成済みです)。|  

## <a name="external-dependencies"></a>外部依存関係  

|依存関係|説明|  
|----------------|----------------------|  
|Active Directory のメール属性|ユーザーのプライマリ SMTP アドレスを使用して電子メールでユーザーの電子メール アドレスを生成する場合、このアドレスが Active Directory の **メール** 属性に存在する必要があります。<br /><br /> 詳細については、Windows Server のマニュアルを参照してください。|

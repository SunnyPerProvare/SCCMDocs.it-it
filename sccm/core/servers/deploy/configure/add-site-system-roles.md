---
title: "サイト システムの役割の追加 | Microsoft Docs"
description: "Configuration Manager サイト システムの役割について説明すると共に、それらの役割を追加してサイトの機能と処理能力を拡張する方法について説明します。"
ms.custom: na
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b90de2d9-494e-43ad-b269-c8ed589f37d3
caps.latest.revision: "12"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 1ad4abf1f06ed24bd1d505648280b5e5d80220c7
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="add-site-system-roles-for-system-center-configuration-manager"></a>System Center Configuration Manager のサイト システム役割の追加

*適用対象: System Center Configuration Manager (Current Branch)*

サイト システムの役割は、1 つの System Center Configuration Manager サイトにつき複数利用することができます。 サイトにサービスを提供したりデバイスとユーザーを管理したりするうえで必要となるサイトの機能や処理能力は、それぞれの役割によって拡張することになります。 1 つのサイト システム サーバーのそれぞれのサイト システムの役割は、同じサイトにある必要があります。   

Configuration Manager では、単一のサイト システム サーバー上で、複数サイトのサイト システムの役割を使用することはサポートされません。  

> [!TIP]  
>  サイト システムの役割の基本や、サイト サーバー、サイト システム サーバー、サイト システムの役割の相違点についてあまり詳しくない場合は、「[System Center Configuration Manager の基本](../../../../core/understand/fundamentals.md)」をご覧ください。  

 次のトピックには、サイト システムの役割をインストールするための手順と関連する詳細情報が詳述されています。  

-   [System Center Configuration Manager のサイト システム役割のインストール](../../../../core/servers/deploy/configure/install-site-system-roles.md)  

     このトピックでは、新しいサイト システムの役割をインストールするのに利用できる 2 つのコンソール内ウィザードの使用方法についての基本的なガイダンスを提供します。  

-   [Microsoft Azure for System Center Configuration Manager のクラウド ベース配布ポイントのインストール](../../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md)  

    クライアントに展開するコンテンツをホストするのに Microsoft Azure を使用する場合には、Configuration Manager が Microsoft Azure と通信して Microsoft Azure サブスクリプションを使用できるようにするために、このトピックの情報に基づいて必要な証明書ファイルを設定できます。 クライアントがクラウドベースの配布ポイントを検索できるように名前解決を設定する必要もあります。  

-   [System Center Configuration Manager でのオンプレミス モバイル デバイス管理のサイト システムの役割のインストール](../../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md)  

     Configuration Manager オンプレミス MDM を使用した新しいデバイスの管理をサポートするために、サイト システムの役割を正しく設定するには、このトピックが役立ちます。  

-   [System Center Configuration Manager のサイト システム役割の構成オプション](../../../../core/servers/deploy/configure/configuration-options-for-site-system-roles.md)  

     サイト システムの一部の役割は、ユーザー インターフェイス内で説明可能な詳細情報を必要とする構成をサポートします。 このトピックでは、それらの詳細情報を提供します。  

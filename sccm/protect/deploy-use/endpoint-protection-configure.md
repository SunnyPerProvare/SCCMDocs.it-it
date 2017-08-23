---
title: "Endpoint Protection の構成 | Microsoft Docs"
description: "Configuration Manager を設定して Windows Defender のマルウェア定義を更新および配布する方法について説明します。"
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 6917644d6719a1ca636713aa5aebf277927123c8
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="configure-endpoint-protection"></a>Endpoint Protection の構成

*適用対象: System Center Configuration Manager (Current Branch)*

Endpoint Protection を使用して構成マネージャー クライアント コンピューターのセキュリティとマルウェアを管理するには、事前にこのトピックの構成手順を実行する必要があります。  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Configuration Manager の Endpoint Protection の構成方法  
 Configuration Manager の Endpoint Protection には、外部依存関係と製品内部の依存関係があります。  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>Configuration Manager で Endpoint Protection を構成する手順  
 次の表に、Endpoint Protection の構成に関する手順、説明、および参照情報を示します。  

> [!IMPORTANT]  
>  Windows 10 コンピューターの Endpoint Protection を管理する場合、Windows Defender のマルウェア定義ファイルを更新し、配布するように Configuration Manager を構成する必要があります。 Windows Defender は Windows 10 に含まれていますが、SCEPInstall をインストールする必要があります。また、Endpoint Protection のカスタム クライアント設定が必要です (以下の**手順 5**)。  

|手順|説明|  
|-----------|-------------|  
|**手順 1:** [Endpoint Protection ポイント サイト システムの役割を作成する](endpoint-protection-site-role.md)|Endpoint Protection を使用するには、事前に Endpoint Protection ポイント サイト システムの役割をインストールしておく必要があります。 これは、1 つのサイト システム サーバーのみにインストールします。また、中央管理サイトまたはスタンドアロンのプライマリ サイトの階層の最上位にインストールしなければなりません。 |  
|**手順 2:** [Endpoint Protection のアラートを構成する](endpoint-configure-alerts.md)|マルウェア感染などの特定のイベントが発生すると、管理者にアラートが通知されます。 アラートは、 **[監視]** ワークスペースの **[アラート]** ノードに表示されます。必要に応じて、指定のユーザーに電子メールで送信することもできます。 |  
|**手順 3:** [Endpoint Protection クライアントの定義ファイルの更新ソースを構成する](endpoint-definition-updates.md)|Endpoint Protection は、さまざまなソースを使用して定義ファイルの更新をダウンロードするように構成できます。 |  
|**手順 4:** [既定のマルウェア対策ポリシーを構成してカスタムのマルウェア対策ポリシーを作成する](endpoint-antimalware-policies.md)|既定のマルウェア対策ポリシーは、Endpoint Protection クライアントがインストールされると適用されます。 展開されているカスタムのポリシーは、クライアント展開の 60 分以内に既定で適用されます。 Endpoint Protection クライアントを展開する前に、マルウェア対策ポリシーを構成していることを確認します。 |  
|**手順 5:** [Endpoint Protection のカスタム クライアント設定を構成する](endpoint-protection-configure-client.md)|カスタム クライアント設定を使用して、階層内のコンピューターのコレクションに Endpoint Protection 設定を構成します。<br /><br /> メモ: 階層内のすべてのコンピューターに適用する場合を除き、既定の Endpoint Protection クライアント設定は構成しないでください。 |  

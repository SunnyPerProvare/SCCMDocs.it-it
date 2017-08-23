---
title: "クライアントのインストール方法 | Microsoft Docs"
description: "System Center Configuration Manager でのクライアントのインストール方法について説明します。"
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 51b5964b-374d-4abc-8619-414a9fffad2d
caps.latest.revision: "9"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: edca31249cc2bb3e0c67265962815c82e3f4711e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="client-installation-methods-in-system-center-configuration-manager"></a>System Center Configuration Manager でのクライアントのインストール方法

*適用対象: System Center Configuration Manager (Current Branch)*

Configuration Manager クライアント ソフトウェアはさまざまな方法でインストールできます。 1 つの方法を利用することも、複数の方法を組み合わせることもできます。 このトピックでは、それぞれの方法について説明します。組織にとって最適な方法を理解できます。  

## <a name="client-push-installation"></a>クライアント プッシュ インストール  

 **サポートされるクライアント プラットフォーム:** Windows  

 **長所**  

-   単一コンピューター、コンピューターのコレクション、またはクエリの結果に対してクライアントをインストールするのに使用できます。  

-   検出されたすべてのコンピューターにクライアントを自動インストールするときに使用できます。  

-   **[クライアント プッシュ インストールのプロパティ]** ダイアログ ボックスの **[クライアント]** タブで定義したクライアント インストールのプロパティが自動的に使用されます。  

 **短所**  

-   大きなコレクションにプッシュするとき、ネットワーク トラフィックの量が増加する可能性があります。  

-   Configuration Manager で検出されたコンピューターでしか使用できません。  

-   ワークグループにクライアントをインストールするときに使用することはできません。  

-   クライアント プッシュ インストールのアカウントでは、どのアカウントに目的のクライアント コンピューターに対する管理者権限を付与するかを指定する必要があります。  

-   クライアント プッシュ インストールを完了するには、クライアント コンピューターで Windows ファイアウォールに例外を構成する必要があります。  

-   クライアント プッシュ インストールはキャンセルできません。 このクライアントのインストール方法をサイトで使用すると、Configuration Manager はクライアントを検出されたすべてのリソースにインストールしようとし、失敗した場合は最大 7 日間にわたって再試行します。  

 このインストール方法の詳細については、「[System Center Configuration Manager でクライアントを Windows コンピューターに展開する方法](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)」を参照してください。  

## <a name="software-update-point-based-installation"></a>ソフトウェアの更新ポイント経由のインストール  
 **サポートされるクライアント プラットフォーム:** Windows  

 **利点:**  

-   既存のソフトウェアの更新のインフラストラクチャを使用して、クライアント ソフトウェアを管理できます。  

-   Windows Server Update Services (WSUS) および Active Directory ドメイン サービスのグループ ポリシー設定が正しく構成されている場合は、新しいコンピューターにクライアント ソフトウェアを自動的にインストールできます。  

-   クライアントをインストールする前に、コンピューターが検出されている必要はありません。  

-   コンピューターは、Active Directory ドメイン サービスに公表されたクライアント インストール プロパティを読み取ることができます。  

-   クライアント ソフトウェアが削除された場合、再インストールします。  

-   目的のクライアント コンピューターのインストール アカウントを構成してメンテナンスを行う必要はありません。  

 **欠点:**  

-   ソフトウェアの更新のインフラストラクチャが機能していることが前提条件です。  

-   クライアントのインストールとソフトウェアの更新に同じサーバーを使用する必要があります。また、このサーバーはプライマリ サイトに存在している必要があります。  

-   新しいクライアントをインストールするには、クライアントのアクティブなソフトウェアの更新ポイントおよびポートを使用して、Active Directory Domain Services 内のグループ ポリシー オブジェクト (GPO) を構成する必要があります。  

-   Active Directory スキーマが Configuration Manager 向けに拡張されていない場合、グループ ポリシー設定を使用してクライアント インストールのプロパティをコンピューターにプロビジョニングする必要があります。  

 このインストール方法の詳細については、「[System Center Configuration Manager でクライアントを Windows コンピューターに展開する方法](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)」を参照してください。  

## <a name="group-policy-installation"></a>グループ ポリシーによるインストール  
 **サポートされるクライアント プラットフォーム:** Windows  

 **利点:**  

-   クライアントをインストールする前に、コンピューターが検出されている必要はありません。  

-   新しいクライアントのインストールまたは更新で使用できます。  

-   コンピューターは、Active Directory ドメイン サービスに公表されたクライアント インストール プロパティを読み取ることができます。  

-   目的のクライアント コンピューターのインストール アカウントを構成してメンテナンスを行う必要はありません。  

 **欠点:**  

-   多数のクライアントがインストールされた場合、ネットワーク トラフィックの量が増加する可能性があります。  

-   Active Directory スキーマが Configuration Manager 向けに拡張されていない場合、グループ ポリシー設定を使用してサイト内のコンピューターにクライアント インストール プロパティを追加する必要があります。  

 このインストール方法の詳細については、「[System Center Configuration Manager でクライアントを Windows コンピューターに展開する方法](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)」を参照してください。  

## <a name="logon-script-installation"></a>ログオン スクリプトによるインストール  
 **サポートされるクライアント プラットフォーム:** Windows  

 **利点:**  

-   クライアントをインストールする前に、コンピューターが検出されている必要はありません。  

-   CCMSetup のコマンド ライン プロパティを使用してサポートします。  

 **欠点:**  

-   多数のクライアントが短時間にインストールされた場合、ネットワーク トラフィックの量が増加する可能性があります。  

-   ユーザーがネットワークに頻繁にログオンしない場合は、すべてのクライアント コンピューターにインストールするのに長時間かかる場合があります。  

 このインストール方法の詳細については、「[System Center Configuration Manager でクライアントを Windows コンピューターに展開する方法](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)」を参照してください。  

## <a name="manual-installation"></a>手動インストール  
 **サポートされるクライアント プラットフォーム:** Windows、UNIX/Linux、Mac OS X  

 **利点:**  

-   クライアントをインストールする前に、コンピューターが検出されている必要はありません。  

-   テストの目的で役立ちます。  

-   CCMSetup のコマンド ライン プロパティを使用してサポートします。  

 **欠点:**  

-   自動化されていないため、時間を削減できます。  

 各プラットフォームのクライアントを手動でインストールする方法の詳細については、次をご覧ください。  

-   [System Center Configuration Manager でクライアントを Windows コンピューターに展開する方法](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

-   [System Center Configuration Manager で UNIX および Linux サーバーにクライアントを展開する方法](../../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md)  

-   [System Center Configuration Manager で Mac にクライアントを展開する方法](../../../../core/clients/deploy/deploy-clients-to-macs.md)  

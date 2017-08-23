---
title: "アップグレード、更新、およびインストールについて | Microsoft Docs"
description: "Configuration Manager のインフラストラクチャを管理するときのインストール、更新、およびアップグレードという用語の相違点について説明します。"
ms.custom: na
ms.date: 1/11/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17fab17f-304d-4f6a-87c7-30ab4f5521ed
caps.latest.revision: "0"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 6bd6cd7ea3c41fa1d70e17a1290c9f1f74cc9e37
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="about-upgrade-update-and-install-for-site-and-hierarchy-infrastructure"></a>サイトと階層のインフラストラクチャでのアップグレード、更新、およびインストールについて

*適用対象: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager のサイトと階層のインフラストラクチャの管理において、*アップグレード*、*更新*、および*インストール* という用語は 3 つの異なる概念を説明するものです。

## <a name="upgrade"></a>Upgrade
*アップグレード*または*インプレース アップグレード*は、Configuration Manager 2012 のサイトまたは階層を System Center Configuration Manager を実行するサイトまたは階層に変換する際に使用されます。
System Center 2012 Configuration Manager を System Center Configuration Manager にアップグレードする場合は、サイトおよびサイト サーバーをホストするために同じサーバーを引き続き使用し、Configuration Manager の既存のデータおよび構成を維持します。  これは、新しいハードウェアにインストールされている新しい System Center Configuration Manager サイトを使用しているときに、管理対象のデバイスに関する構成およびデータを保持する方法である[移行](/sccm/core/migration/migrate-data-between-hierarchies)とは異なります。

詳細については、「[System Center Configuration Manager へのアップグレード](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)」を参照してください。



## <a name="update"></a>更新
*更新*は、System Center Configuration Manager のコンソール内の更新プログラム、および Configuration Manager コンソール内から配信できない更新プログラムであるアウトオブバンドの更新プログラムのインストールに使用されます。 以降のバージョンが実行されるように、コンソール内の更新プログラムでは、Current Branch サイト (またはテクニカル プレビュー サイト) のバージョンを変更できます。 たとえば、サイトでバージョン 1606 を実行している場合は、バージョン 1610 用の更新プログラムをインストールできます。 更新プログラムではサイトのバージョンを変更しなくても、既知の問題に対する修正プログラムをインストールすることもできます。      

通常、更新プログラムではセキュリティ修正プログラム、品質の向上、および新機能が既存の展開に追加されます。 Technical Preview ブランチを使用する場合、更新プログラムでは Technical Preview の最新バージョンをインストールできます。
-   コンソール内の更新プログラムをインストールするタイミングの選択を、階層の最上位サイトからします。
- コンソール内から利用できる更新プログラムはすべてインストールできます。 たとえば、サイトでバージョン 1602 を実行していて、1606 と 1610 の両方が利用可能な場合は、バージョン 1610 をインストールすることをお勧めします。これは、以前にリリースされたバージョンで利用可能になった機能がそれ以降のバージョンに含まれているためです。
- 新しい更新プログラムが最上位サイトでインストールを完了すると、子プライマリ サイトは自動的にプロセスを開始して更新します。 ただし、[サービス ウィンドウ](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkservicewindowa-service-windows-for-site-servers)を設定し、更新のタイミングを制御することができます。
- セカンダリ サイトは更新プログラムを自動的にインストールしません。 代わりに、Configuration Manager コンソール内から手動で更新プログラムを開始します。

詳細については、「[System Center Configuration Manager の更新プログラム](/sccm/core/servers/manage/updates)」、および「[System Center Configuration Manager の Technical Preview](/sccm/core/get-started/technical-preview)」を参照してください。



## <a name="install"></a>[インストール]
*インストール*は、最初から新しい Configuration Manager の階層を作成する際、または追加のサイトを既存の階層に追加する際に使用されます。  

新しいプライマリ サイトまたは中央管理サイトをインストールする場合、使用する setup.exe の場所と関連するソース ファイルは、インストール シナリオによって異なります。

詳細については、[サイトのインストールの準備](/sccm/core/servers/deploy/install/prepare-to-install-sites)に関するページを参照してください。

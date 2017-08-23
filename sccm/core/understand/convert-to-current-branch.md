---
title: "Long-Term Servicing Branch の Current Branch へのアップグレード | Microsoft Docs"
description: "Long-Term Servicing Branch サイトを Current Branch サイトに変換する方法について説明します。"
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec5b54cf-62b7-4ed1-9bb3-e8c63b9641c8
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 6e7edc85630d22c5bbba1ff66bd1199903db76db
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="upgrade-the-long-term-servicing-branch-to-the-current-branch"></a>Long-Term Servicing Branch の Current Branch へのアップグレード

*適用対象: System Center Configuration Manager (Long-Term Servicing Branch)*

このトピックでは、Configuration Manager の Long-Term Servicing Branch (LTSB) を実行するサイトと階層を Current Branch にアップグレード (変換) する方法について説明します。

Current Branch の使用権を付与する現在のソフトウェア アシュアランス契約 (または同様のライセンス権) がある場合は、インストールしている LTSB を Current Branch に変換することができます。  これは片方向変換です。Current Branch サイトから LTSB への変換はサポートされていません。

複数のサイトがある場合、変換する必要があるのは最上階層のサイトのみです。 最上階層のサイトを変換すると、次のようになります。
- 子プライマリ サイトが自動的に変換されます。
-   セカンダリ サイトを Configuration Manager コンソール内から手動で更新する必要があります。

## <a name="run-setup-to-convert-the-long-term-servicing-branch"></a>Long-Term Servicing Branch を変換するためのセットアップの実行
最上階層のサイトで、適切な構成基準メディアから Configuration Manager セットアップを実行して、**[サイトのメンテナンス]** を選択できます。  次に、ライセンス ページが表示されたら、Current Branch のオプションを選択し、ウィザードを完了します。

サイトが Current Branch に変換されると、以前は使用できなかった機能が使用できるようになります。

> [!NOTE]  
> 適切な基準メディアとは、インストールされている LTSB バージョン以上のバージョンを含むメディアのことです。

たとえば、LTSB がバージョン 1606 に基づいている場合、1511 基準メディアを使用して Current Branch に変換することはできません。 このような場合は、LTSB サイトのインストールに使用したものと同じバージョンの 1606 構成基準メディアからセットアップを実行し、Current Branch のライセンス オプションを選択します。  また、Current Branch の新しい構成基準がリリースされている場合には、その構成基準メディアからセットアップを実行することもできます。

基準バージョンの一覧については、「[System Center Configuration Manager の更新プログラム](/sccm/core/servers/manage/updates)」の「**基準バージョンと更新プログラムのバージョン**」を参照してください。

## <a name="use-the-configuration-manager-console-to-convert-the-long-term-servicing-branch"></a>Long-Term Servicing Branch を変換するには、Configuration Manager コンソールを使用します。
サイトで LTSB を実行する場合は、Configuration Manager コンソールで以下のオプションを使用して、Current Branch に変換することができます。

 1. コンソールで、**[管理]** > **[サイトの構成]** > **[サイト]** の順に移動し、**[階層設定]** を開きます。  

 2. Current Branch に変換するためのオプションを選択し、**[適用]** を選択します。  

サイトが Current Branch に変換されると、以前は使用できなかった機能が使用できるようになります。

---
title: "LTSB の管理 | Microsoft Docs"
description: "System Center Configuration Manager LTSB の管理の変更点"
ms.custom: na
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8da2887a-fd8e-438c-b926-849c121f7fdf
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 9c6f349ead906532a7a58df74609de976769e251
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="manage-the-long-term-servicing-branch-of-configuration-manager"></a>Configuration Manager の Long-Term Servicing Branch の管理

*適用対象: System Center Configuration Manager (Long-Term Servicing Branch)*

System Center Configuration Manager の Long-Term Servicing Branch (LTSB) を使用する場合は、インフラストラクチャの管理方法に影響する重要な変更点を理解するために、以下の情報が役に立ちます。

LTSB は Current Branch バージョン 1606 と同等であるため (Intune の統合やクラウド関連の機能などいくつかの例外はあります)、計画、展開、構成、日常の管理のために使用するほとんどのタスクが同じです。

たとえば、LTSB は、Current Branch と同じ数のサイト、サイトの種類、クライアント、全般的なインフラストラクチャをサポートしています。 そのため、Current Branch のサイトおよび階層の計画、設計に関するトピックのガイドを参照できます。 同様に、両方のブランチでサポートされる LTSB の機能 (ソフトウェア更新プログラム、オペレーティング システムの展開など) については、Current Branch ドキュメントの該当するセクションをご覧ください。ただし、Current Branch バージョン 1606 の後に導入された変更や機能は使用できないことに注意してください。

同じではない管理タスクの詳細については、次のセクションをご覧ください。

## <a name="updates-and-servicing"></a>更新プログラムとサービス
LTSB のコンソール内更新プログラムでは、重要なセキュリティ更新プログラムのみを使用できます。  

コンソールには、以降の Current Branch リリース用の通常の更新プログラムに関する情報が表示されますが、LTSB からは使用できません。 更新プログラムはダウンロードされず、インストールすることはできません。

重要なセキュリティ修正プログラムについてコンソール内更新プログラムをサポートするには、LTSB で[サービス接続ポイント](/sccm/core/servers/deploy/configure/about-the-service-connection-point)を使用する必要があります。 Current Branch と同様に、このサイト システムの役割はオフライン モードまたはオンライン モードで構成できます。 LTSB は、Current Branch と同じテレメトリと使用状況データを収集および送信します。

LTSB は、Current Branch のドキュメントで説明されているように、Hotfix Installer and Update Registration ツールの使用をサポートしています。

更新プログラムとサービスの全般的な情報については、「 [Updates for Configuration Manager](/sccm/core/servers/manage/updates)」(Configuration Manager の更新プログラム) を参照してください。


## <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>サイトの拡張と CD.Latest フォルダーの変更
新しい中央管理サイトをインストールして LTSB を実行し、スタンドアロンのプライマリ サイトを実行する場合、1606 基準メディアのセットアップおよびソース ファイルを使用する必要があります Current Branch の場合、CD.Latest フォルダーのセットアップを実行し、ソース ファイルを使用します。

サイトの拡張には CD.Latest フォルダーのセットアップを実行しませんが、サイトの回復には CD.Latest フォルダーを使用します。また、最初の LTSB サイトが中央管理サイトだったときに、新しい子プライマリ サイトをインストールする場合にも、CD.Latest フォルダーを使用します。

サイトの拡張の詳細については、[スタンドアロン プライマリ サイトの拡張](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#expand-a-stand-alone-primary-site)に関するページをご覧ください。 CD.Latest フォルダーの詳細については、「[The CD.Latest folder](/sccm/core/servers/manage/the-cd.latest-folder)」(CD.Latest フォルダー) を参照してください。


## <a name="recovery"></a>復元
サイトを復元する場合は、サイトまたはサイト データベースを元のブランチに復元する必要があります。 Current Branch サイト データベースを LTSB インストールに復元することはできません。また、その逆も同様です。

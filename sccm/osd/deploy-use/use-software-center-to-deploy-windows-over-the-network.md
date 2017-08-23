---
title: "ソフトウェア センターを使用してネットワーク経由での Windows を展開する | Microsoft Docs"
description: "オペレーティング システムをソフトウェア センターに展開して、既存のコンピューターを新しいバージョンの Windows に更新したり、Windows を最新バージョンにアップグレードしたりできます。"
ms.custom: na
ms.date: 6/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
caps.latest.revision: "5"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: 8988409c68b7f69439ed03872c316b2139d25616
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>System Center Configuration Manager でソフトウェア センターを使用してネットワーク経由で Windows を展開する

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager でオペレーティング システムをインストールするためのタスク シーケンスは、ソフトウェア センターで使用可能にすることができます。 次のオペレーティング システムの展開シナリオでは、オペレーティング システムをソフトウェア センターに展開することができます。

-   [新しいバージョンの Windows で既存のコンピューターを更新する](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Windows を最新バージョンにアップグレードする](upgrade-windows-to-the-latest-version.md)

いずれかのオペレーティング システムの展開シナリオの手順を実行します。 その後で、次のセクションを使用して、ソフトウェア センターで使用可能な展開を準備します。

## <a name="configure-deployment-settings"></a>展開の設定の構成  
オペレーティング システムの展開をソフトウェア センターで使用できるようにするには、展開を構成します。 展開は、ソフトウェアの展開ウィザードの **[展開の設定]** ページか展開のプロパティの **[配置の設定]** タブで構成することができます。 **[利用できるようにする項目]** 設定で、 **[Configuration Manager クライアントのみ]** または **[Configuration Manager クライアント、メディア、PXE]**のいずれかを構成します。 システムでオペレーティング システムが展開された後、オペレーティング システムは、ソフトウェア センターにターゲット コレクションのメンバーとして表示されます。

##  <a name="BKMK_Deploy"></a> コンピューターへのタスク シーケンスの展開  
オペレーティング システムをターゲット コレクションに展開します。 詳細については、「 [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)」をご覧ください。 ソフトウェア センターでオペレーティング システムを展開するとき、展開が必須か使用可能かを設定することができます。

-   **必須の展開**: 必須の展開では、ソフトウェア センターでオペレーティング システムが利用可能になりますが、構成された割り当てスケジュールで自動的に開始されます。

-   **使用可能な展開**: オペレーティング システムはソフトウェア センターで使用可能になり、ユーザーはオンデマンドでインストールすることができます。

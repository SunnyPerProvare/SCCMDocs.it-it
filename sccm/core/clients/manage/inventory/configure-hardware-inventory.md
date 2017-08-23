---
title: "ハードウェア インベントリの構成 | Microsoft Docs"
description: "System Center Configuration Manager ですべてのクライアントまたは 1 つのコレクションに対してハードウェア インベントリを設定します。"
ms.custom: na
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
caps.latest.revision: "5"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 0baadb95ec8dbb945f1a611ebb95a03cec3199bd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-hardware-inventory-in-system-center-configuration-manager"></a>How to configure hardware inventory in System Center Configuration Manager

*適用対象: System Center Configuration Manager (Current Branch)*

この手順により、ハードウェア インベントリの既定のクライアント設定を構成し、階層内のすべてのクライアントに適用します。 いくつかのクライアントにのみこの設定を適用するには、カスタムのデバイス クライアント設定を作成し、ハードウェア インベントリを使用するデバイスが含まれるコレクションにそれを割り当てます。 「[System Center Configuration Manager でクライアント設定を構成する方法](../../../../core/clients/deploy/configure-client-settings.md)」を参照してください。  

> [!NOTE]  
>  クライアント デバイスが複数のクライアント設定をハードウェア インベントリを受信した場合は、各設定のハードウェア インベントリのクラスは、クライアントがハードウェア インベントリをレポートするときに結合されます。  

### <a name="to-configure-hardware-inventory"></a>ハードウェア インベントリを構成するには  

1.  Configuration Manager コンソールで、**[管理]** > **[クライアント設定]** > **[既定のクライアント設定]** の順に選択します。  

4.  **[ホーム]** タブの **[プロパティ]** グループで、**[プロパティ]** を選択します。  

5.  [**既定の設定**] ダイアログ ボックスで、[**ハードウェア インベントリ**] を選択します。  

6.  [デバイスの設定] **** 一覧で、次を構成します。  

    -   **クライアントのハードウェア インベントリを有効にする** - [**True**] を選択します。  

    -   **ハードウェア インベントリのスケジュール** - [**スケジュール**] をクリックしてクライアントがハードウェア インベントリを収集する間隔を指定します。  

7.  必要なその他の[ハードウェア インベントリのクライアント設定](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory)を構成します。  

クライアント デバイスは、次の機会にクライアント ポリシーをダウンロードしたときに、これらの設定で構成されます。 1 つのクライアントのポリシーの取得を開始する場合は、「 [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md)」を参照してください。  

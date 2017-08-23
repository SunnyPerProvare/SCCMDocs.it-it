---
title: "Intune に登録されたデバイスのポリシーをリモートで同期する | Microsoft Docs"
description: "Intune に登録されたデバイスのポリシーを Configuration Manager コンソールから同期する方法について説明します"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b3731ad0-2a24-4042-994e-5e4c1230e3fe
caps.latest.revision: "18"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 337814fd5ba49ed17fc97aba49f79f02df817f4e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="remotely-synchronize-policy-on-intune-enrolled-devices-from-the-configuration-manager-console"></a>Intune に登録されたデバイスのポリシーを Configuration Manager コンソールからリモートで同期する

*適用対象: System Center Configuration Manager (Current Branch)*


デバイス自体のポータル サイト アプリから同期を要求するのではなく、Configuration Manager コンソールから Intune に登録されたデバイスのポリシー同期を要求できます。 

手順は次のとおりです。

1.  **[資産とコンプライアンス]** > **[概要]** > **[デバイス]** で、デバイスを選択します。
2.  **[リモート デバイスの操作]** メニューの **[同期要求の送信]** をクリックします。


5 ～ 10 分で、ポリシーのすべての変更がデバイスに同期されます。 同期要求の状態の情報を、デバイス ビューの新しい列 **[Remote Sync State]** (リモート同期の状態)、および各デバイスの **[プロパティ]** ダイアログ ボックスの [探索データ] セクションで、見ることができます。

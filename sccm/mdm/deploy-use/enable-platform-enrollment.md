---
title: "System Center Configuration Manager を使用してプラットフォームの登録を有効にする | Microsoft Docs"
description: "System Center Configuration Manager と Microsoft Intune を使用してプラットフォームの登録を有効にします。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a9163b77-a67d-4139-8272-bb1dfdb8707c
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 4b047aa752b638aeeb7dd363a66564800d00a8df
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="enable-platform-enrollment-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager と Microsoft Intune を使用してプラットフォームの登録を有効にする

*適用対象: System Center Configuration Manager (Current Branch)*

デバイスの登録を有効にするには、デバイス プラットフォームごとに必要な追加の構成があります。
  - [iOS と Mac の登録セットアップ](enroll-hybrid-ios-mac.md): Apple MDM プッシュ証明書を取得します

  - [Windows の登録セットアップ](enroll-hybrid-windows.md): DNS を構成し、Windows PC、Windows 10 Mobile デバイス、Windows Phone デバイスのすべてで登録を有効にします

  - [Android](enroll-hybrid-android.md): Android デバイスの場合、登録を有効にするために必要な追加の手順はありません

MDM 管理を有効にした後は、各ユーザーが登録できるデバイスの数を指定できます (ユーザーごとに最大 15 デバイス)。

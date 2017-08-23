---
title: "電子メール プロファイルのセキュリティとプライバシー | Microsoft Docs"
description: "System Center Configuration Manager でデバイスの電子メール プロファイルを管理する場合のセキュリティのベスト プラクティスについて説明します。"
ms.custom: na
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 601e3a8d-e9e7-456f-a844-f19c3dae12a9
caps.latest.revision: "3"
caps.handback.revision: "0"
author: Nbigman
ms.author: nbigman
manager: angrobe
ms.openlocfilehash: 17707f931a4fa58b225ce14f04c2a19648585bc4
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="security-and-privacy-for-email-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager の電子メール プロファイルのセキュリティとプライバシー

*適用対象: System Center Configuration Manager (Current Branch)*

## <a name="security-best-practices-for-email-profiles"></a>電子メール プロファイルのセキュリティ上のベスト プラクティス  
 デバイスの電子メール プロファイルを管理するときには、次のセキュリティのベスト プラクティスに従ってください。  

|セキュリティのベスト プラクティス|説明|  
|----------------------------|----------------------|  
|可能な限り、使用する電子メール インフラストラクチャとクライアント オペレーティング システムでサポートできる、最も安全なオプションを選択します。|電子メール プロファイルは、デバイスで既にサポートしている電子メール設定を中央から配付して管理するのに便利です。 Configuration Manager では、電子メール機能は追加されません。<br /><br /> 使用するデバイスと電子メール インフラストラクチャに推奨されているセキュリティ上のベスト プラクティスを特定および実装し、それに従います。|  

## <a name="privacy-information-for-email-profiles"></a>電子メール プロファイルのプライバシー情報  
 既定では、デバイスは電子メール プロファイルを評価しません。 また、電子メール プロファイルを構成してから、電子メール プロファイルをユーザーに展開する必要があります。  

 電子メール プロファイルを構成する前に、プライバシー要件について検討してください。  

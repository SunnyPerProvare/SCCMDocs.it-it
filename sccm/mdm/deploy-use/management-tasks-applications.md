---
title: "System Center Configuration Manager でのアプリケーションの管理 | Microsoft Docs"
description: "System Center Configuration Manager でアプリケーションを管理します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: bc7bb99bc526ed0bbaaad15fc9af39fa8b7c3893
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="manage-applications-in-system-center-configuration-manager"></a>System Center Configuration Manager でのアプリケーションの管理

*適用対象: System Center Configuration Manager (Current Branch)*

Microsoft Intune または Configuration Manager のオンプレミス デバイス管理でデバイスを管理すると、さらに次のアプリケーションの種類も管理できます。
- Windows Phone アプリケーション パッケージ (*.xap ファイル)
- iOS アプリ パッケージ (*.ipa ファイル)
- Android アプリ パッケージ (*.apk ファイル)
- Android 用アプリ パッケージ (Google Play 内)
- Windows Phone アプリケーション パッケージ (Windows Phone ストア内)
- MDM を介した Windows インストーラー
- Web アプリケーション

このセクションでは、ハイブリッド MDM またはオンプレミス MDM を使用したアプリケーションの作成と管理について詳しく説明します。

「[System Center Configuration Manager アプリケーションの管理タスク](../../apps/deploy-use/management-tasks-applications.md)」では、System Center Configuration Manager のアプリケーションと展開の種類の管理に関するより一般情報を提供しています。

## <a name="deploying-and-monitoring-apps"></a>アプリの展開と監視

System Center Configuration Manager でアプリケーションを展開し監視するモバイル デバイスのプロセスは、ラップトップやデスクトップ コンピューターなどのオンサイト デバイスのプロセスと同じです。 アプリケーションの展開と監視に関する一般情報は、次のトピックを参照してください。

- [System Center Configuration Manager でアプリケーションを展開する](../../apps/deploy-use/deploy-applications.md)
- [System Center Configuration Manager でアプリケーションを監視する](../../apps/deploy-use/monitor-applications-from-the-console.md)

アプリケーションの展開と監視において留意すべき、モバイル デバイスの管理に固有の考慮事項は次のとおりです。

- MDM 登録デバイスは、シミュレートされた展開、ユーザー エクスペリエンス、またはスケジュール設定をサポートしていません。

- 既に構成している場合は、iOS アプリの構成ポリシーを使用して展開を関連付けることができます。 [アプリ構成ポリシーを使用した iOS アプリの構成](configure-ios-apps-with-app-configuration-policies.md)に関する記事を参照してください。

### <a name="next-steps"></a>次のステップ

いずれはアプリケーションに変更を加えたり、アンインストールしたり、既に展開されているアプリケーションを新しいアプリケーションに置き換えたりすることが必要になる可能性があります。 「[System Center Configuration Manager でのアプリケーションの更新とインベントリからの削除](../../apps/deploy-use/update-and-retire-applications.md)」を参照して、これらの機能を理解してください。

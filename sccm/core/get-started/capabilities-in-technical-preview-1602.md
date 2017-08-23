---
title: "Configuration Manager の Technical Preview 1602 の機能"
description: "System Center Configuration Manager の Technical Preview バージョン 1602 で使用できる機能について説明します。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b9265d1-b461-47f8-b7ef-885da0fdd969
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex,nofollow
ms.openlocfilehash: 2354f885aaf69683004ad78f0e1978e78fee9145
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="capabilities-in-technical-preview-1602-for-system-center-configuration-manager"></a>System Center Configuration Manager の Technical Preview 1602 の機能

*適用対象: System Center Configuration Manager (Technical Preview)*

この記事では、System Center Configuration Manager の Technical Preview バージョン 1602 で使用できる機能について説明します。 このバージョンをインストールして更新し、新機能を Configuration Manager の Technical Preview サイトに追加できます。 このバージョンの Technical Preview をインストールする前に、説明のトピック「[System Center Configuration Manager の Technical Preview](../../core/get-started/technical-preview.md)」を確認して、Technical Preview の使用に関する一般的な要件と制限、バージョン間の更新方法、および Technical Preview の機能に関するフィードバックを提供する方法について理解してください。  

 このバージョンでお試しいただける新機能を次に示します。  

##  <a name="BKMK_MDM"></a> モバイル デバイス管理の機能強化  

### <a name="ios-activation-lock"></a>iOS のアクティベーション ロック  
 System Center Configuration Manager は、iOS 7.1 以降向けの「iPhone を探す」アプリの機能である、iOS のアクティベーション ロックを管理するために役立ちます。 iPhone を探すアプリをデバイスで使用すると、アクティブ化ロックが自動的に有効になります。 有効になると、ユーザーの Apple ID とパスワードを入力しない限り、以下の操作を実行できなくなります。  

-   iPhone を探すアプリをオフにする  

-   デバイスを消去する  

-   ディスクを再アクティブ化する  

 Configuration Manager では、iOS 7.1 以降を実行している監視対象と監視対象外の両方のデバイスのアクティベーション ロックの状態を要求できます。 監視対象のデバイスの場合、Intune では、アクティベーション ロックのバイパス コードを取得し、直接デバイスに発行できます。  

 詳しくは「[Configuration Manager でアクティベーション ロックのバイパスを使用して iOS デバイスを保護する](/sccm/mdm/deploy-use/manage-ios-activation-lock)」をご覧ください。  

##  <a name="BKMK_SC1601"></a> バージョン 1602 でのソフトウェア センターの機能強化  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>ソフトウェア センターから PC コンピューターとユーザーのポリシーを更新する  
 新しいオプションである **同期ポリシー** が、ソフトウェア センターの **[オプション]** > **[コンピューターのメンテナンス]** ページに追加されました。これにより、PC では Configuration Manager コンピューターとユーザーのポリシーが更新されます。  

##  <a name="BKMK_Win10Servicing"></a> Windows 10 サービスの機能強化  
 1602 Technical Preview では、次の Windows 10 サービスの機能が追加されました。  

-   サービス プランの新しいフィルター オプション。  **言語**、**必須**、**タイトル**ごとにフィルター処理できるようになりました。 指定された条件を満たすアップグレードだけが、関連付けられている展開に追加されます。  

-   ソフトウェア更新プログラムの同期の**アップグレード**の分類を選ぶと、ソフトウェア更新プログラムが正常に同期され、Windows 10 サービスが適切に動作するためには、WSUS [修正プログラム 3095113](https://support.microsoft.com/kb/3095113) が必要なことを通知する警告ダイアログが表示されます。  このダイアログから、修正プログラムのサポート技術情報の記事に移動できます。  

-   利用可能な Windows 10 アップグレードは、Configuration Manager コンソールの **[Windows 10 のサービス]** \ **[すべての Windows 10 更新プログラム]** ノードにのみ表示されるようになりました。 これらの更新プログラムは、[**ソフトウェア更新プログラム** \ **すべてのソフトウェアの更新**] ノードには表示されなくなりました。  

-   Windows 10 Upgrade パッケージを開始するエンド ユーザーには、オペレーティング システムがアップグレードされることを通知するダイアログが表示されます。  

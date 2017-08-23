---
title: "Mac コンピューターへのクライアント展開の計画 | Microsoft Docs"
description: "System Center Configuration Manager での Mac コンピューターへのクライアント展開の計画"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 8d15ae3f-de42-461f-a907-c43873da22d2
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 75bddb41d4d1cf209fa7595c52b5a6aa831ba3dd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="planning-for-client-deployment-to-mac-computers-in-system-center-configuration-manager"></a>System Center Configuration Manager での Mac コンピューターへのクライアント展開の計画

*適用対象: System Center Configuration Manager (Current Branch)*

Mac OS X オペレーティング システムを実行する Mac コンピューターに Configuration Manager クライアントをインストールして、次の管理機能を使用できます。  

-   **ハードウェア インベントリ**  

     Configuration Manager ハードウェア インベントリを使用して、Mac コンピューターのハードウェアと、インストールされているアプリケーションに関する情報を収集できます。 この情報を Configuration Manager コンソールのリソース エクスプローラーで確認し、コレクション、クエリ、レポートの作成に使用できます。 詳細については、「[System Center Configuration Manager でリソース エクスプローラーを使用してハードウェア インベントリを表示する方法](../../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md)」を参照してください。  

     Configuration Manager は、Mac コンピューターから次のハードウェア情報を収集します。  

    -   プロセッサ  

    -   コンピューター システム  

    -   ディスク ドライブ  

    -   ディスク パーティション  

    -   ネットワーク アダプター  

    -   オペレーティング システム  

    -   [サービス]  

    -   プロセス  

    -   インストール済みソフトウェア  

    -   コンピューター システム製品  

    -   USB コントローラー  

    -   USB デバイス  

    -   CD-ROM ドライブ  

    -   ビデオ コントローラー  

    -   デスクトップ モニター  

    -   ポータブル バッテリー  

    -   物理メモリ  

    -   プリンター  

    > [!IMPORTANT]  
    >  ハードウェア インベントリ時に Mac コンピューターから収集されるハードウェア情報を拡張することはできません。  

-   **コンプライアンス設定**  

     Configuration Manager コンプライアンス設定を使用して、コンプライアンスを確認し、Mac OS X 環境設定 (.plist) の設定を修復できます。 たとえば、Safari Web ブラウザーのホーム ページの設定を強制したり、Apple ファイアウォールを有効にしたりできます。 また、シェル スクリプトを使用して、Mac OS X の設定を監視、修復することもできます。  

-   **アプリケーション管理**  

     Configuration Manager は、Mac コンピューターにソフトウェアを展開できます。 Mac コンピューターには、次のソフトウェア形式を展開できます。  

    -   Apple Disk Image (.DMG)  

    -   Meta Package File (.MPKG)  

    -   Mac OS X Installer Package (.PKG)  

    -   Mac OS X Application (.APP)  

 Mac コンピューターに Configuration Manager クライアントをインストールする場合、Windows ベースのコンピューターにインストールされた Configuration Manager クライアントでサポートされる次の管理機能を使用できません。  

-   クライアント プッシュ インストール  

-   オペレーティング システムの展開  

-   ソフトウェア更新プログラム  

    > [!NOTE]  
    >  必要な Mac OS X ソフトウェア更新プログラムを Mac コンピューターに展開するには、Configuration Manager アプリケーション管理を使用します。 また、コンプライアンス設定を使用して、必要なソフトウェア更新プログラムを常にコンピューターに適用することもできます。  

-   メンテナンス期間  

-   リモート コントロール  

-   電源管理  

-   クライアント ステータスのクライアント チェックと修復  

 Configuration Manager Mac クライアントのインストールおよび構成方法については、「[System Center Configuration Manager で Mac にクライアントを展開する方法](../../../../core/clients/deploy/deploy-clients-to-macs.md)」を参照してください。

---
title: "工場出荷時の OEM 用、または現地保管場所用のイメージの作成 | Microsoft Docs"
description: "事前設定されたメディアによる展開を使用して、完全にはプロビジョニングされていないコンピューターにオペレーティング システムを展開する際のネットワーク トラフィックを軽減します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
caps.latest.revision: "8"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 07aba04fb1b845e389a5f75b115d536136c1569c
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-system-center-configuration-manager"></a>System Center Configuration Manager による工場出荷時の OEM 用、または現地保管場所用のイメージの作成

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager における事前設定されたメディアによる展開では、完全にはプロビジョニングされていないコンピューターにオペレーティング システムを展開できます。 事前設定されたファイルは、Windows Imaging Format (WIM) と呼ばれる形式のファイルであり、製造元によるベア メタル コンピューター (OEM)、または Configuration Manager 環境に接続していない企業の準備センターにインストールすることができます。 その後、Configuration Manager 環境でコンピューターはメディアが提供するブート イメージを使用して起動し、事前設定されたメディア上でハッシュ チェックを実行し、正しいかどうかを確認します。さらに、コンピューターはサイト管理ポイントに接続して利用可能なタスク シーケンスを取得し、ダウンロード プロセスを完了します。


ブート イメージとオペレーティング システム イメージが展開先のコンピューターに存在するので、この展開の方法はネットワーク トラフィックを軽減します。 事前設定メディアに含めるアプリケーション、パッケージ、ドライバー パッケージを指定できます。 コンピューターにオペレーティング システムがインストールされた後、まずローカルのタスク シーケンス キャッシュにアプリケーション、パッケージ、またはドライバー パッケージがないか検査されます。コンテンツが見つからない場合、または変更されている場合は、事前設定メディアで構成されている配布ポイントからコンテンツがダウンロードされて、インストールされます。  

 事前設定されたメディアは、次のオペレーティング システムの展開シナリオに使用できます。  

-   [新しいコンピューター (ベア メタル) に新しいバージョンの Windows をインストールする](install-new-windows-version-new-computer-bare-metal.md)  

-   [既存のコンピューターの置き換えと設定の転送](replace-an-existing-computer-and-transfer-settings.md)  

 オペレーティング システムのいずれかの展開シナリオの手順を実行してから、次のセクションに従って事前設定メディアを準備し、作成します。  

## <a name="configure-deployment-settings"></a>展開の設定の構成  
 事前設定されたメディアを使用してオペレーティング システムの展開プロセスを開始する場合、オペレーティング システムをメディアから使用できるように展開を構成する必要があります。 これはソフトウェアの展開ウィザードの **[展開の設定]** ページか展開のプロパティの **[配置の設定]** タブで構成することができます。  **[利用できるようにする項目]** の設定では、次のいずれかを設定します。  

-   **Configuration Manager クライアント、メディア、PXE**  

-   **メディアと PXE のみ**  

-   **メディアと PXE のみ (非表示)**  

## <a name="create-the-prestaged-media"></a>事前設定メディアの作成  
 OEM または現地保管場所に送信する事前設定メディア ファイルを作成します。 詳細については、「 [Create prestaged media with System Center Configuration Manager](create-prestaged-media.md)」をご覧ください。  

## <a name="send-the-prestaged-media-file-to-the-oem-or-local-depot"></a>OEM または現地保管場所への事前設定されたメディア ファイルの送信  
 OEM または現地保管場所へメディアを送信し、コンピューターを事前設定します。 事前設定されたメディア ファイルは、コンピューターのフォーマット済みのハード ディスクに適用されます。  

## <a name="start-the-computer-to-install-the-operating-system"></a>オペレーティング システムをインストールするコンピューターの起動  
 事前設定されたメディア ファイルは、コンピューターに適用されます。 コンピューターを初めて起動すると、オペレーティング システムのインストール プロセスが開始します。  

---
title: "特徴と機能 | Microsoft Docs"
description: "System Center Configuration Manager の主な管理機能について説明します。"
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
caps.latest.revision: "18"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 4691f43dccdf73936107f4635321897b9779bead
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="features-and-capabilities-of-system-center-configuration-manager"></a>System Center Configuration Manager の特徴と機能

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の主な管理機能について次に説明します。 機能ごとに個別の前提条件があり、使用する機能が Configuration Manager 階層の設計と実装に影響する可能性があります。 たとえば、階層内のデバイスにソフトウェアを展開する場合、配布ポイント サイト システムの役割をインストールする必要があります。  

 ご使用の環境でこれらの管理機能がサポートされるように Configuration Manager の計画とインストールを行う方法の詳細については、「[System Center Configuration Manager の準備](../../../core/plan-design/get-ready.md)」をご覧ください。  

 **アプリケーション管理**  

 アプリケーションの作成、管理、展開、および監視に役立つ一連のツールとリソースを管理対象のさまざまなデバイスに提供します。 さらに、Configuration Manager にはユーザーのアプリ内で会社のデータを保護するのに役立つツールも用意されています。 「[アプリケーション管理の概要](/sccm/apps/understand/introduction-to-application-management)」をご覧ください。

 **会社のリソースへのアクセス**  

 組織内のユーザーがリモートの場所からデータとアプリケーションにアクセスできるようにするための、ツールのセットとリソースを提供します。 これらのツールには、Wi-Fi プロファイル、VPN プロファイル、証明書プロファイル、Exchange および SharePoint へのオンラインでの条件付きアクセスが含まれます。 「[System Center Configuration Manager でのデータとサイト インフラストラクチャの保護](../../../protect/understand/protect-data-and-site-infrastructure.md)」と「[System Center Configuration Manager でサービスへのアクセスを管理する](../../../protect/deploy-use/manage-access-to-services.md)」をご覧ください。  

 **コンプライアンス設定**  

 企業内のクライアント デバイスの構成対応状態を評価、追跡、および修復するのに役立つ一連のツールとリソースを提供します。 さらに、コンプライアンス設定を使用すると、管理対象デバイスでさまざまな機能とセキュリティ設定を構成できます。 「[System Center Configuration Manager でのデバイス コンプライアンスの確認](../../../compliance/understand/ensure-device-compliance.md)」をご覧ください。  

 **Endpoint Protection**  

 企業内のコンピューターにセキュリティ、マルウェア対策、および Windows ファイアウォール管理を提供します。 「[System Center Configuration Manager での Endpoint Protection](../../../protect/deploy-use/endpoint-protection.md)」をご覧ください。  

 **インベントリ**  

 資産の特定と監視に役立つ一連のツールを提供します。  

-   **ハードウェア インベントリ**: 社内のデバイスのハードウェアに関する詳細情報を収集します。 「[System Center Configuration Manager のハードウェア インベントリの概要](../../../core/clients/manage/inventory/introduction-to-hardware-inventory.md)」をご覧ください。  

-   **ソフトウェア インベントリ**: 組織内のクライアント コンピューターに保存されているファイルに関する情報を収集して報告します。 「[System Center Configuration Manager のソフトウェア インベントリの概要](../../../core/clients/manage/inventory/introduction-to-software-inventory.md)」をご覧ください。  

-   **資産インテリジェンス**: インベントリ データを収集し、社内のソフトウェア ライセンスの使用状況を監視するためのツールを提供します。 「[System Center Configuration Manager の資産インテリジェンスの概要](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md)」をご覧ください。  

**Microsoft Intune を使用したモバイル デバイスの管理**  

 Configuration Manager を使用すると、インターネット経由で Microsoft Intune サービスを利用して、iOS、Android (Samsung KNOX Standard など)、Windows Phone、および Windows デバイスを管理することができます。

 Intune サービスを使用しますが、管理作業は Configuration Manager コンソール経由で使用可能なサービス接続ポイントのサイト システムの役割を使って実施します。 「[System Center Configuration Manager と Microsoft Intune を使用するハイブリッド モバイル デバイス管理 (MDM)](../../../mdm/understand/hybrid-mobile-device-management.md)」をご覧ください。  

 **オンプレミス モバイル デバイス管理**  

 (個別にインストールされている Configuration Manager クライアントではなく) デバイス プラットフォームに組み込まれたオンプレミスの Configuration Manager インフラストラクチャと管理機能を使用して、PC とモバイル デバイスを登録および管理します。 現時点で、Windows 10 Enterprise および Windows 10 Mobile デバイスの管理をサポートしています。 「[System Center Configuration Manager でオンプレミス インフラストラクチャを使用したモバイル デバイスの管理](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)」をご覧ください。  

 **オペレーティング システムの展開**  

 オペレーティング システム イメージを作成するためのツールを提供します。 これらのイメージを使用し、PXE ブートまたは CD セット、DVD、USB フラッシュ デバイスなどの起動可能メディアを用いて、コンピューターにオペレーティング システムを展開できます。 これは、Configuration Manager で管理されているコンピューターと、管理されていないコンピューターに適用されることに注意してください。 「[System Center Configuration Manager のオペレーティング システムの展開の概要](../../../osd/understand/introduction-to-operating-system-deployment.md)」をご覧ください。  

 **電源管理**  

 企業内のクライアント コンピューターの電力消費を管理および監視するために使用する一連のツールとリソースを提供します。 「[System Center Configuration Manager の電源管理の概要](../../../core/clients/manage/power/introduction-to-power-management.md)」をご覧ください。  

 **クエリ**  

 階層内のリソースに関する情報、およびインベントリ データとステータス メッセージに関する情報を取得するためのツールを提供します。 この情報は、レポートに使用したり、ソフトウェア展開や構成設定でデバイスやユーザーのコレクションを定義したりするために使用できます。 「[System Center Configuration Manager のクエリの概要](../../../core/servers/manage/introduction-to-queries.md)」をご覧ください。  

 **リモート接続プロファイル**  

 組織のデバイスのリモート接続設定を作成、展開、監視する際に役立つ、一連のツールとリソースを提供します。 これらの設定を展開することにより、ユーザーが会社のネットワークにある自分のコンピューターに接続するときの手間をできるだけ省きます。 「[System Center Configuration Manager でのリモート接続プロファイルの操作](/sccm/compliance/deploy-use/create-remote-connection-profiles)」をご覧ください。  

 **ユーザー データとプロファイル構成項目**  

 Configuration Manager のユーザー データとプロファイル構成項目には、階層内のユーザーの Windows 8 以降を実行するコンピューターのフォルダー リダイレクト、オフライン ファイル、およびローミング プロファイルを管理できる設定が含まれています。 「[System Center Configuration Manager でのユーザー データとプロファイル構成アイテムの操作](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items)」をご覧ください。  

 **リモート コントロール**  

 Configuration Manager コンソールからクライアント コンピューターをリモート管理するためのツールを提供します。 「[System Center Configuration Manager のリモート コントロールの概要](../../../core/clients/manage/remote-control/introduction-to-remote-control.md)」をご覧ください。  

 **レポート**  

 Configuration Manager コンソールから SQL Server Reporting Services の高度なレポート機能を使用するための一連のツールとリソースを提供します。 「[System Center Configuration Manager のレポートの概要](../../../core/servers/manage/introduction-to-reporting.md)」をご覧ください。  

 **ソフトウェア使用状況測定**  

 構成マネージャー クライアントからソフトウェア使用状況データを監視および収集するためのツールを提供します。 「[System Center Configuration Manager のソフトウェア使用状況測定でアプリの使用状況を監視する](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md)」を参照してください。  

 **ソフトウェア更新プログラム**  

 企業内のソフトウェアの更新を管理、展開、および監視するための一連のツールとリソースを提供します。 「[System Center Configuration Manager のソフトウェア更新プログラムの概要](/sccm/sum/understand/software-updates-introduction)」をご覧ください。  

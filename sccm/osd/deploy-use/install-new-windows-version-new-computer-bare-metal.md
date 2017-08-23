---
title: "新しいコンピューターへの Windows のインストール - Configuration Manager | Microsoft Docs"
description: "Configuration Manager で PXE、OEM、またはスタンドアロン メディアを使用して、新しいコンピューター (ベア メタル) にオペレーティング システムをインストールします。"
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5ad22d5-7df1-49c6-8a0f-db1c3f0cda19
caps.latest.revision: "8"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 584dad7d8b05a2da9f7a66b73028ae99ff1a594f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal-with-system-center-configuration-manager"></a>System Center Configuration Manager を使用して、新しいコンピューター (ベア メタル) に新しいバージョンの Windows をインストールする

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックでは、System Center Configuration Manager で新しいコンピューターにオペレーティング システムをインストールする一般的な手順を示します。 このシナリオでは、PXE、OEM、スタンドアロン メディアなど、展開のさまざまな方法の中から選択することができます。 適切なオペレーティング システムの展開シナリオがわからない場合は、「[エンタープライズ オペレーティング システムを展開するシナリオ](scenarios-to-deploy-enterprise-operating-systems.md)」を参照してください。  

Windows の新しいバージョンで既存のコンピューターを更新する場合は、次のセクションを参考にします。  

##  <a name="BKMK_Plan"></a> プラン  

-   **インフラストラクチャの要件の計画と実装**  

     オペレーティング システムを展開する前に解決しなければならないインフラストラクチャの要件として、Windows ADK、Windows 展開サービス (WDS)、Windows 展開サービス (WDS)、サポートされているハード ディスクの構成などがあります。詳細については、「[オペレーティング システムの展開のインフラストラクチャ要件](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)」を参照してください。

##  <a name="BKMK_Configure"></a> 構成  

1.  **ブート イメージの準備**  

     ブート イメージは、Windows PE 環境 (コンポーネントやサービスが制限された最小オペレーティング システム) でコンピューターを起動して、完全な Windows オペレーティング システムをコンピューターにインストールできるようにします。   オペレーティング システムを展開する場合は、使用するブート イメージを選択し、配布ポイントにそのイメージを配布する必要があります。 ブート イメージを準備するには、次のものを使用します。  

    -   イメージの詳細については、「[ブート イメージの管理](../get-started/manage-boot-images.md)」を参照してください。  

    -   ブート イメージをカスタマイズする方法の詳細については、「[ブート イメージのカスタマイズ](../get-started/customize-boot-images.md)」を参照してください。  

    -   配布ポイントへブート イメージを配布します。 詳細については、「[コンテンツの配布](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content)」を参照してください。  

2.  **オペレーティング システム イメージの準備**  

     オペレーティング システム イメージには、セットアップ先のコンピューターにオペレーティング システムをインストールするために必要なファイルが含まれています。 オペレーティング システム イメージを準備するには、次のものを使用します。  

    -   オペレーティング システム イメージを作成する方法の詳細については、「[オペレーティング システム イメージを管理する](../get-started/manage-operating-system-images.md)」を参照してください。

    -   オペレーティング システム イメージを配布ポイントに配布します。 詳細については、「[コンテンツの配布](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content)」を参照してください。

3.  **オペレーティング システムをネットワーク経由で展開するためのタスク シーケンスの作成**  

     ネットワーク経由でのオペレーティング システムのインストールを自動化するタスク シーケンスを使用します。 「[オペレーティング システムをインストールするタスク シーケンスの作成](create-a-task-sequence-to-install-an-operating-system.md)」の手順でオペレーティング システムを展開するためのタスク シーケンスを作成します。 選択した展開方法に応じて、タスク シーケンスに追加の考慮事項があります。  

##  <a name="BKMK_Deploy"></a> デプロイ  

-   オペレーティング システムを展開するには、次の展開方法のいずれかを使用します。  

    -   [PXE を使用したネットワーク経由での Windows の展開](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [マルチキャストを使用した、ネットワーク経由での Windows の展開](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [工場出荷時の OEM 用、または現地保管場所用のイメージの作成](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [ネットワークではなくスタンドアロン メディアを使用した Windows の展開](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [起動可能なメディアを使用したネットワーク経由での Windows の展開](use-bootable-media-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>モニター  

-   **タスク シーケンスの展開の監視**  

     オペレーティング システムをインストールするために、タスク シーケンスの展開を監視するには、「[オペレーティング システムの展開の監視](monitor-operating-system-deployments.md)」を参照してください。  

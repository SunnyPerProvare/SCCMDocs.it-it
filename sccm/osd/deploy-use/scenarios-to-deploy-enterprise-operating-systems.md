---
title: "エンタープライズ オペレーティング システムを展開するシナリオ | Microsoft Docs"
description: "System Center Configuration Manager を使用してエンタープライズ オペレーティング システムを展開するいくつかのシナリオについて説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
caps.latest.revision: "11"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: b1bea8b1b890f7c96a432835d28ad840a9b6873d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-system-center-configuration-manager"></a>System Center Configuration Manager を使用してエンタープライズ オペレーティング システムを展開するシナリオ

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager では、次のオペレーティング システムの展開シナリオを使用できます。  

-   [Windows を最新バージョンにアップグレードする](upgrade-windows-to-the-latest-version.md): このシナリオでは、現在 Windows 7、Windows 8、Windows 8.1、または Windows 10 を実行しているコンピューター上のオペレーティング システムをアップグレードします。 アップグレード プロセスでは、コンピューター上のアプリケーション、設定、およびユーザー データが保持されます。 Windows ADK などの外部の依存関係はなく、このプロセスは、従来のオペレーティング システムの展開よりも高速で、回復性に優れています。  

-   [既存のコンピューターを Windows の新しいバージョンに更新する](refresh-an-existing-computer-with-a-new-version-of-windows.md): このシナリオでは、既存のコンピューターにパーティションを作成してフォーマットし (ワイプ)、コンピューターに新しいオペレーティング システムをインストールします。 オペレーティング システムをインストールした後、設定とユーザー データを移行できます。  

-   [新しいバージョンの Windows を新しいコンピューターにインストールする (ベア メタル) ](install-new-windows-version-new-computer-bare-metal.md): このシナリオでは、新しいコンピューターにオペレーティング システムをインストールします。 これは、オペレーティング システムの新規インストールであり、設定やユーザー データの移行は含まれません。  

-   [既存のコンピューターの置き換えと設定の転送](replace-an-existing-computer-and-transfer-settings.md): このシナリオでは、新しいコンピューターにオペレーティング システムをインストールします。 必要に応じて、古いコンピューターから新しいコンピューターに設定およびユーザー データを移行できます。  

## <a name="things-to-consider-before-you-deploy-operating-system-images"></a>オペレーティング システム イメージを配置する前に考慮すべきこと  
 オペレーティング システムを展開する前に考慮すべきいくつかの点があります。  

### <a name="operating-system-image-size"></a>オペレーティング システム イメージ のサイズ  
 オペレーティング システム イメージのサイズは非常に大きくなることがあります。 たとえば、Windows 7 のイメージ サイズは 3 ギガバイト (GB) 以上です。 イメージのサイズや、オペレーティング システムを同時に展開するコンピューターの数は、ネットワーク パフォーマンスや利用可能な帯域幅に影響をおよぼします。 イメージの展開がおよぼす可能性がある影響や展開が完了するまでにかかる時間をより正確に捉えるためにも、ネットワーク パフォーマンスをテストします。 ネットワーク パフォーマンスに影響を与える Configuration Manager の操作には、配布ポイントへのイメージの配布、サイトからサイトへのイメージの配布、Configuration Manager クライアントへのイメージのダウンロードなどが含まれます。  

 また、オペレーティング システム イメージをホストする配布ポイントに十分なディスク容量を必ず設けます。  

### <a name="client-cache-size"></a>クライアントのキャッシュ サイズ  
 Configuration Manager クライアントがコンテンツをダウンロードする際は、バックグラウンド インテリジェント転送サービス (BITS) が使用可能であれば、このサービスを自動的に使用します。 オペレーティング システムをインストールするタスク シーケンスを展開する際は、Configuration Manager クライアントがタスク シーケンスが実行される前に、ローカル キャッシュのフル イメージをダウンロードできるように、展開に関するオプションを設定することができます。  

 通常、Configuration Manager クライアントがオペレーティング システム イメージ (あるいはその他のいずれかのパッケージ) をダウンロードする必要があるけれども、キャッシュに十分な容量がない場合、クライアントはキャッシュの他のパッケージを確認して、古いパッケージのいくつか、またはすべてを削除することで、イメージを使用できるかを判断します。 パッケージを削除しても十分なディスク容量を確保できない場合は、クライアントはイメージをダウンロードせず、展開は失敗します。 これは、キャッシュに大きなパッケージが保存されており、それを保持するように設定した場合に起こる可能性があります。 パッケージを削除するとキャッシュに十分なディスク容量を確保できる場合は、クライアントはそれらを削除し、イメージをダウンロードしてキャッシュに保存します。  

 Configuration Manager クライアントの既定のキャッシュ サイズでは、ほとんどの場合、オペレーティング システム イメージの展開に十分な容量を確保できません。 クライアントのキャッシュにイメージをすべてダウンロードしてからそのイメージを実行する場合は、展開するイメージのサイズに合わせて、ダウンロード先のコンピューターにおける Configuration Manager クライアントのキャッシュ サイズを調整する必要があります。  

 詳細については、「 [Configure the Client Cache for Configuration Manager Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache)」を参照してください。  

## <a name="task-sequence-deployments"></a>タスク シーケンスの展開  
 作成したタスク シーケンスは、次のいずれかの方法で、Configuration Manager クライアント コンピューターにオペレーティング システム イメージを展開できます。  

-   まず配布ポイントからイメージとコンテンツを Configuration Manager クライアント キャッシュにダウンロードして、インストールする。  

-   配布ポイントのイメージとコンテンツを即座にインストールする。  

-   配布ポイントが定めたようにイメージとコンテンツをインストールする。  

 タスク シーケンスの展開を作成すると、既定では、イメージは Configuration Manager クライアントのキャッシュにダウンロードされてからインストールされます。 イメージを Configuration Manager クライアントのキャッシュにダウンロードしてから実行する場合、タスク シーケンスにハード ドライブのパーティション再作成ステップが設定されていると、パーティション再作成ステップでエラーが発生します。これは、ハード ドライブのパーティションが作成されるときに Configuration Manager クライアントのキャッシュの内容が消去されるためです。 タスク シーケンスでハード ドライブのパーティションを再作成する必要がある場合は、タスク シーケンスをデプロイするときに **[配布ポイントからプログラムを実行する]**  オプションを使用して、配布ポイントからイメージのインストールを実行する必要があります。  

 詳細については、「 [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)」をご覧ください。  

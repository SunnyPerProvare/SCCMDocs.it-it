---
title: "オペレーティング システムの展開の相互運用性に関する計画 | Microsoft Docs"
description: "単一の階層内の異なる System Center Configuration Manager サイトで異なるバージョンを使用する場合の相互運用性の問題について理解します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
caps.latest.revision: "10"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 50a4b75b8c8c1cb6f7a8e696abad285f99080fcd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="planning-for-operating-system-deployment-interoperability-in-system-center-configuration-manager"></a>System Center Configuration Manager のオペレーティング システムの展開の相互運用性の計画

*適用対象: System Center Configuration Manager (Current Branch)*

単一の階層内の異なる System Center Configuration Manager サイトで異なるバージョンを使用する場合、一部の Configuration Managerの機能が使用できなくなります。 通常、Configuration Manager の新しいバージョンの機能は、古いバージョンを実行しているサイトでアクセスしたり、古いバージョンを実行しているクライアントで使用したりすることはできません。 詳細については、「 [Interoperability between different versions of System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md)」をご覧ください。  

 階層内の最上位サイトをアップグレードし、階層内の他のサイトは古いバージョンの Configuration Manager を実行する場合、次の点を考慮してください。  

-   クライアント インストール パッケージ  

    -   既定のクライアント インストール パッケージのソースは自動的にアップグレードされ、階層内のすべての配布ポイントは、古いバージョンの階層内のサイトにある配布ポイントの場合でも、新しいクライアント インストール パッケージで更新されます。  

    -   新しいバージョンを実行するクライアントを、まだ新しいバージョンにアップグレードされていないサイトに割り当てることはできません。 割り当ては管理ポイントでブロックされます。  

-   ブート イメージ  

    -   最上位サイトを Configuration Manager の最新バージョンにアップグレードすると、既定のブート イメージ (x86 および x64) は、Windows PE 10 を使用する Windows ADK for Windows 10 ベースのブート イメージに自動更新されます。 既定のブート イメージと関連付けられているファイルは、Configuration Manager の最新バージョンのファイルで更新されます。 カスタム ブート イメージは自動的に更新されません。 カスタム ブート イメージは、古いバージョンの Windows PE を含め、手動で更新する必要があります。  

    -   サイト階層内に複数バージョンの Configuration Manager が含まれる場合、動的メディアは使用しないでください。 この場合、すべてのサイトが同じバージョンの Configuration Manager のサイトが含まれる場合、動的メディアは使用しないでください。  

    -   Configuration Manager の最新のブート イメージに必要なカスタマイズが含まれることを確認してから、Configuration Manager の最新バージョンを使用して、サイトのすべての配布ポイントを新しいブート イメージに更新します。  

-   ユーザー状態移行ツール (USMT)  

    -   最上位サイトを Configuration Manager の最新バージョンにアップグレードすると、既定の USMT パッケージが最新のバージョンに自動的に更新されます。 カスタム USMT パッケージは自動的に更新されません。 これらのパッケージは手動で更新する必要があります。  

-   新しいタスク シーケンス ステップ  

    -   定期的に、新しいバージョンの Configuration Manager のサイトが含まれる場合、動的メディアは使用しないでください。 新しいステップのあるタスク シーケンスを古いクライアントに展開すると、タスク シーケンスのステップは失敗します。 新しいステップのあるタスク シーケンスを展開する前に、ターゲット コレクション内のクライアントが新しいバージョンに更新されていることをご確認ください。  

-   オペレーティング システムの展開メディア  

    -   サイトが新しいバージョンに更新されたとき、すべてのメディア (起動可能、キャプチャ、事前設定、スタンドアロン) を新しい Configuration Manager クライアント パッケージで更新する必要があります。  

-   オペレーティング システムの展開に対するサード パーティ製の拡張機能  

    -   オペレーティング システムの展開に対するサード パーティ製の拡張機能があり、Configuration Manager サイトまたは Configuration Manager クライアントにさまざまなバージョンがある、混在階層となっている場合、拡張に関する問題がある可能性があります。  

 階層内のサイトを積極的にアップグレードする場合、次のセクションを参照してオペレーティング システムを展開してください。  

## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>混在階層における最新バージョンの Configuration Manager  サイト  
 1 つのサイトを最新バージョンの Configuration Manager にアップグレードすると、既定のクライアント インスタンス パッケージを参照するタスク シーケンスによって、最新バージョンの Configuration Manager クライアントの展開が自動的に開始されます。 次に、カスタム クライアント インストール パッケージを参照するタスク シーケンスによって、そのカスタム パッケージに含まれるバージョンのクライアント (多くの場合、前のバージョンの Configuration Manager クライアント) が展開されます。このクライアントは、タスク シーケンスの展開エラーを防ぐために更新する必要があります。 カスタム クライアント インストール パッケージを使用するように構成されたタスク シーケンスがある場合、最新バージョンの Configuration Manager クライアント インストール パッケージを使用するようにタスク シーケンス ステップを更新するか、最新の Configuration Manager クライアント インストール ソースを使用するようにカスタム パッケージを更新する必要があります。  

> [!IMPORTANT]  
>  最新の Configuration Manager クライアント インストール パッケージを参照するタスク シーケンスは、前の Configuration Manager サイトのクライアントに展開しないでください。 古い Configuration Manager サイトに割り当てられているクライアントが最新の Configuration Manager クライアント バージョンにアップグレードされた場合、Configuration Manager は、古い Configuration Manager サイトへの割り当てをブロックします。 そのため、手動でクライアントを最新の Configuration Manager サイトに割り当てるか、前のバージョンの Configuration Manager クライアントをコンピューターに再インストールするまで、そのクライアントにサイトは割り当てられず、管理対象ではなくなります。  

## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>混在階層における古いバージョンの Configuration Manager  サイト  
 中央管理サイトを最新バージョンの Configuration Manager にアップグレードする際、前の (最新バージョンの Configuration Manager にアップグレードされていない) Configuration Manager サイトに割り当てられたクライアントに対して、オペレーティング システム展開タスク シーケンスを実行する場合、管理されていない状態のクライアントが残らないことを次の手順で確認します。  

-   Configuration Manager サイト内のクライアントにのみ展開するタスク シーケンスを作成します。 同様に、最新バージョンの Configuration Manager サイトのクライアントに展開するために使用するタスク シーケンスのコピーを作成し、前の Configuration Manager サイトのクライアントに展開しないでください。 次に、前の Configuration Manager クライアント インストール ソースを使用するようにカスタム パッケージを更新する必要があります。 前の Configuration Manager クライアント インストール ソースを参照するカスタム クライアント インストール パッケージがまだない場合、手動で作成する必要があります。  

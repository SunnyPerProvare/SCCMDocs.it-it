---
title: "Wake On LAN の構成 | Microsoft Docs"
description: "System Center Configuration Manager で Wake On LAN 設定を選択します。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
caps.latest.revision: "7"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 9c920651ba1dc6e0a28df458d28956126ddbaff0
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-configure-wake-on-lan-in-system-center-configuration-manager"></a>System Center Configuration Manager で Wake on LAN を構成する方法

*適用対象: System Center Configuration Manager (Current Branch)*

コンピューターをスリープ状態から復帰させて、必要なソフトウェア (ソフトウェア更新プログラム、アプリケーション、タスク シーケンス、プログラムなど) をインストールする場合は、System Center Configuration Manager の Wake On LAN 設定を指定します。

ウェイクアップ プロキシ クライアント設定を使用して、Wake on LAN を補うことができます。 ただし、ウェイクアップ プロキシを使用する場合は、まずそのサイト用に Wake on LAN を有効にし、Wake on LAN 送信方法で [ **ウェイクアップ パケットのみを使用する** ] および [ **ユニキャスト** ] オプションを指定する必要があります。 このウェイクアップ ソリューションは、リモート デスクトップ接続などのアドホック接続もサポートします。

最初の手順を Wake on LAN 用にプライマリ サイトを構成します。 次に、2 番目の手順を使用してウェイクアップ プロキシ クライアント設定を構成します。 この 2 番目の手順では、ウェイクアップ プロキシ設定用に既定のクライアント設定を構成し、階層内のすべてのコンピューターに適用します。 一部のコンピューターにのみこれらの設定を適用するには、カスタムのデバイス設定を作成し、ウェイクアップ プロキシ用に構成するコンピューターが含まれるコレクションに割り当てます。 カスタム クライアント設定の作成方法については、[System Center Configuration Manager でクライアント設定を構成する方法](../../../core/clients/deploy/configure-client-settings.md)を参照してください。

ウェイクアップ プロキシ クライアント設定を受け取ったコンピューターでは、多くの場合、そのネットワーク接続が 1 ～ 3 秒間一時停止されます。 これは、クライアントのウェイクアップ プロキシ ドライバーを有効にするために、クライアントでネットワーク インターフェイスをリセットする必要があるために発生します。

> [!WARNING]
> ネットワーク サービスの予期しない中断を防ぐために、まず分離した代表的なネットワーク インフラストラクチャを使用してウェイクアップ プロキシを評価します。 次に、カスタム クライアント設定を使用して、いくつかのサブネット上にある一部のコンピューター グループにテスト範囲を広げます。 ウェイクアップ プロキシの詳細については、「[System Center Configuration Manager でクライアントをウェイク アップする方法を計画する](../../../core/clients/deploy/plan/plan-wake-up-clients.md)」を参照してください。

## <a name="to-configure-wake-on-lan-for-a-site"></a>サイトに Wake On LAN を構成するには

1. Configuration Manager コンソールで、**[管理]、[サイトの構成]、[サイト]** の順に移動します。
2. 構成するプライマリ サイトをクリックし、**[プロパティ]** をクリックします。
3. **[Wake on LAN]** タブをクリックし、このサイトに必要なオプションを構成します。 ウェイクアップ プロキシをサポートするには、**[ウェイクアップ パケットのみを使用する]** と **[ユニキャスト]** を選択する必要があります。 詳細については、「[System Center Configuration Manager でクライアントをウェイク アップする方法を計画します](../../../core/clients/deploy/plan/plan-wake-up-clients.md)」をご覧ください。
4. **[OK]** をクリックし、階層内のすべてのプライマリ サイトでこの手順を繰り返します。

## <a name="to-configure-wake-up-proxy-client-settings"></a>ウェイク アップ プロキシ クライアント設定を構成するには

1. Configuration Manager コンソールで、**[管理]、[クライアント設定]** に移動します。
2. **[既定のクライアント設定]** をクリックし、**[プロパティ]** をクリックします。
3. **[電力管理]** を選択し、**[ウェイクアップ プロキシを有効にする]** に対して **[はい]** を選択します。
4. 設定を確認し、必要に応じてウェイクアップ プロキシ設定を変更します。 これらの設定の詳細については、「[電力管理設定](../../../core/clients/deploy/about-client-settings.md#power-management)」を参照してください。
5. **[OK]** をクリックしてダイアログ ボックスを閉じ、**[OK]** をクリックして [既定のクライアント設定] ダイアログ ボックスを閉じます。

次の Wake on LAN レポートを使用して、ウェイクアップ プロキシのインストールと構成を監視します。

- ウェイクアップ プロキシの展開状態の概要
- ウェイクアップ プロキシの展開状態の詳細

> [!TIP]
> ウェイクアップ プロキシが機能しているかどうかをテストするには、休止中のコンピューターに対する接続をテストします。 たとえば、休止中のコンピューターにある共有フォルダーに接続したり、リモート デスクトップを使用して休止中のコンピューターへの接続を試行したりします。 Direct Access を使用している場合、現在インターネット上にある休止中のコンピューターに対して同じテストを実行して、IPv6 プレフィックスが機能することを確認します。

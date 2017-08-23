---
title: "Endpoint Protection の構成 | Microsoft Docs"
description: "System Center Configuration Manager で Endpoint Protection を使用する方法を選択および構成し、クライアント コンピューターでマルウェア対策定義を最新の状態に保つ方法について説明します。"
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 537dd2a7-4e44-4877-b8dd-5e1499407f8d
caps.latest.revision: "21"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: b5da7900a4f8e2f330c4dcb2cac00b45099bd909
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
#  <a name="configure-definition-updates-for-endpoint-protection"></a>Endpoint Protection の定義ファイルの更新を構成する  

*適用対象: System Center Configuration Manager (Current Branch)*

 System Center Configuration Manager で Endpoint Protection を使用すると、利用できるいくつかの方法のいずれかを使用して、階層内のクライアント コンピューターでマルウェア対策定義を最新の状態に保つことができます。 このトピックの情報は、これらの方法を選んで構成するのに役立ちます。

 マルウェア対策定義を更新するには、次の方法から 1 つ以上を使用できます。

-   [[Configuration Manager から配布される更新プログラム]](endpoint-definitions-configmgr.md) - この方法では、Configuration Manager ソフトウェア更新プログラムを使用して、階層内のコンピューターに定義とエンジンの更新プログラムを配布します。

-   [[Windows Server Update Services (WSUS) から配信される更新プログラム]](endpoint-definitions-wsus.md) - この方法では、WSUS インフラストラクチャを使用して定義とエンジンの更新プログラムをコンピューターに配布します。

-   [[Microsoft Update から配信される更新プログラム]](endpoint-definitions-microsoft-updates.md) - この方法では、コンピューターを Microsoft Update に直接接続し、定義とエンジンの更新プログラムをダウンロードできます。 この方法は、ビジネス ネットワークにあまり接続していないコンピューターに役立ちます。

-   [[Microsoft Malware Protection Center から配信された更新プログラム]](endpoint-definitions-protection-center.md) - この方法では、Microsoft Malware Protection Center から定義ファイルの更新をダウンロードします。

-   [[UNC ファイル共有から更新する]](endpoint-definitions-network.md) - この方法では、最新の定義とエンジンの更新プログラムをネットワーク上の共有に保存できます。 各クライアントは、ネットワークにアクセスして更新プログラムをインストールできます。

 定義ファイルの更新ソースを複数構成し、それを評価および適用する順序を制御できます。 これは、マルウェア対策ポリシーを作成するときに、 **[定義ファイルの更新ソースの構成]** ダイアログ ボックスで行います。

> [!IMPORTANT]
>  Windows 10 が動作する PC の場合は、Endpoint Protection を構成して Windows Defender のマルウェア定義を更新する必要があります。

## <a name="how-to-configure-definition-update-sources"></a>定義ファイルの更新ソースを構成する方法
 次の手順を使用すると、各マルウェア対策ポリシーに使用する定義ファイルの更新ソースを構成できます。

1.  Configuration Manager コンソールで、[ **資産とコンプライアンス**] をクリックします。

2.  **[資産とコンプライアンス]** ワークスペースで **[Endpoint Protection]**を展開してから、 **[マルウェア対策ポリシー]**をクリックします。

3.  **[既定のマルウェア対策ポリシー]** プロパティ ページを開くか、新しいマルウェア対策ポリシーを作成します。 マルウェア対策ポリシーを作成する方法の詳細については、「[System Center Configuration Manager で Endpoint Protection 用にマルウェア対策ポリシーを作成し展開する方法](endpoint-antimalware-policies.md)」をご覧ください。

4.  マルウェア対策プロパティ ダイアログ ボックスの **[定義ファイルの更新]** セクションで **[ソースの設定]**をクリックします。

5.  **[定義ファイルの更新ソースの構成]** ダイアログ ボックスで、定義ファイルの更新に使用するソースを選びます。 **[上]** または **[下]** をクリックしてそれらのソースを使用する順序を変更します。

6.  **[OK]** をクリックして **[定義ファイルの更新ソースの構成]** ダイアログ ボックスを閉じます。

## <a name="configure-endpoint-protection-definitions"></a>Endpoint Protection 定義の構成

-   [[Configuration Manager から配布される更新プログラム]](endpoint-definitions-configmgr.md) - この方法では、Configuration Manager ソフトウェア更新プログラムを使用して、階層内のコンピューターに定義とエンジンの更新プログラムを配布します。

-   [[Windows Server Update Services (WSUS) から配信される更新プログラム]](endpoint-definitions-wsus.md) - この方法では、WSUS インフラストラクチャを使用して定義とエンジンの更新プログラムをコンピューターに配布します。

-   [[Microsoft Update から配信される更新プログラム]](endpoint-definitions-microsoft-updates.md) - この方法では、コンピューターを Microsoft Update に直接接続し、定義とエンジンの更新プログラムをダウンロードできます。 この方法は、ビジネス ネットワークにあまり接続していないコンピューターに役立ちます。

-   [Microsoft Malware Protection Center から配信された更新プログラム] - この方法では、Microsoft Malware Protection Center から定義ファイルの更新をダウンロードします。

-   [[UNC ファイル共有から更新する]](endpoint-definitions-network.md) - この方法では、最新の定義とエンジンの更新プログラムをネットワーク上の共有に保存できます。 各クライアントは、ネットワークにアクセスして更新プログラムをインストールできます。

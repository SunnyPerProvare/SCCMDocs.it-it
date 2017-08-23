---
title: "Windows Server の準備 | Microsoft Docs"
description: "コンピューターが System Center Configuration Manager のサイト サーバーまたはサイト システム サーバーとして使用するための前提条件を満たしていることを確認します。"
ms.custom: na
ms.date: 2/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2aca914f-641e-4bc8-98d4-bbf0a2a5276f
caps.latest.revision: "10"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 9b97dedb5d2be0bd2e47260033e6e4361467dc4e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="prepare-windows-servers-to-support-system-center-configuration-manager"></a>System Center Configuration Manager をサポートするための Windows Server の準備

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager のサイト システム サーバーとして Windows コンピューターを使用するためには、サイト サーバーまたはサイト システム サーバーとして意図された用途の前提条件を満たす必要があります。  

-   一般に前提条件には Windows の機能や役割が該当し、コンピューターのサーバー マネージャーを使用してそれらを有効にすることができます。  

-   Windows の機能や役割を有効にする方法はオペレーティング システムによって異なります。それらを構成する方法については、実際に使用するオペレーティング システムのドキュメントを参照してください。  

この記事の情報では、Configuration Manager サイト システムのサポートに必要な Windows の構成の種類の概要を説明します。 特定のサイト システムの役割の構成の詳細については、「[サイトとサイト システムの前提条件](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)」をご覧ください。

##  <a name="BKMK_WinFeatures"></a> Windows の機能と役割  
 コンピューターに対して Windows の機能や役割を設定するときは、コンピューターを再起動してその構成を完了させることが必要な場合があります。 そのため、Configuration Manager のサイトまたはサイト システム サーバーをインストールする前に、どのコンピューターでどのサイト システムの役割をホストするかを決めておくことをお勧めします。
### <a name="features"></a>機能  
 特定のサイト システム サーバーでは次の Windows 機能が必要となります。これらは、コンピューターにサイト システムの役割をインストールする前に設定しておく必要があります。  

-   **.NET Framework**: 次を含みます。  

    -   ASP.NET  
    -   HTTP アクティブ化  
    -   非 HTTP アクティブ化  
    -   Windows Communication Foundation (WCF) サービス  

    サイト システムの役割によって異なるバージョンの .NET Framework が必要となります。  

    .NET Framework 4.0 以降には、3.5 以前のバージョンとの下位互換性がありません。複数のバージョンが必須としてリストされているときは、それぞれのバージョンを同じコンピューターで使用できるようにしてください。  

-   **バックグラウンド インテリジェント転送サービス (BITS)**: 管理対象デバイスとの通信をサポートするため、管理ポイントには BITS (および自動選択されるオプション) が必要です。  

-   **BranchCache**: BranchCache を使用するクライアントに対応するため、配布ポイントに BranchCache を設定できます。  

-   **データ重複除去**: 配布ポイントにはデータ重複除去を設定し、その利点を活かすことができます。  

-   **Remote Differential Compression (RDC)**: サイト サーバーまたは配布ポイントをホストするすべてのコンピューターには RDC が必要です。   
    RDC は、パッケージの署名を生成したり、署名の比較を実行したりする際に使用されます。  

### <a name="roles"></a>役割  
 ソフトウェアの更新やオペレーティング システムの展開など、特定の機能をサポートするために、以下に示した Windows の役割が必要となります。また、一般的なサイト システムの役割には、そのほとんどで IIS が必要となります。  

 -   **ネットワーク デバイス登録サービス** (Active Directory 証明書サービスの下): この Windows の役割は Configuration Manager で証明書プロファイルを使用する前提条件です。  

 -   **Web サーバー (IIS)**: 次を含みます。  
    -   共通の HTTP 機能 >  
        -   HTTP リダイレクト  
    -   アプリケーションの開発 >  
        -   .NET 拡張機能  
        -   ASP.NET  
        -   ISAPI 拡張機能  
        -   ISAPI フィルター  
    -   管理ツール >  
        -   IIS 6 管理互換性  
        -   IIS 6 メタベース互換  
        -   IIS 6 Windows Management Instrumentation (WMI) 互換性  
    -   セキュリティ >  
        -   要求のフィルタリング  
        -   Windows 認証  

 以下に示すサイト システムの役割では、ここに記載した IIS の構成が使用されます。  
    -   アプリケーション カタログ Web サービス ポイント  
    -   アプリケーション カタログ Web サイト ポイント  
    -   配布ポイント  
    -   登録ポイント  
    -   登録プロキシ ポイント  
    -   フォールバック ステータス ポイント  
    -   管理ポイント  
    -   ソフトウェアの更新ポイント  
    -   状態移行ポイント     

    サイト サーバーのオペレーティング システムに備わっている IIS のバージョンが、必要な IIS の最小バージョンとなります。  

    これらの IIS 構成に加えて、[IIS の要求フィルター (配布ポイント用)](#BKMK_IISFiltering) の設定が必要になる場合があります。  

-   **Windows 展開サービス**: この役割は、オペレーティング システムの展開で使用されます。  
-   **Windows Server Update Services**: この役割は、ソフトウェア更新プログラムを展開するときに必要になります。  

##  <a name="BKMK_IISFiltering"></a> IIS の要求フィルター (配布ポイント用)  
 特定のファイル名拡張子とフォルダーの場所は、IIS の要求フィルターによって、HTTP または HTTPS 通信によるアクセスがブロックされるように既定で設定されています。 そのままでは、ブロックされた拡張子やフォルダーの場所を含んだパッケージをクライアントが配布ポイントからダウンロードできません。  

 IIS の要求フィルター構成によってブロックされる拡張子がパッケージのソース ファイルに含まれている場合、それらを許可するように要求フィルターを設定する必要があります。 そのためには、配布ポイント コンピューターの IIS マネージャーで [要求フィルター機能を編集](https://technet.microsoft.com/library/hh831621.aspx) します。  

 また、Configuration Manager では、パッケージとアプリケーションに次のファイル名拡張子が使用されます。 これらのファイル拡張子が要求フィルターの構成でブロックされないよう注意してください。  

-   .PCK  
-   .PKG  
-   .STA  
-   .TAR  

たとえば、ソフトウェア展開のソース ファイルに **bin** という名前のフォルダーや **.mdb** というファイル名拡張子の付いたファイルが含まれている場合があります。  

-   既定では、これらの要素へのアクセスは、IIS の要求フィルターによってブロックされます (**bin** は非表示セグメントとしてブロックされ、 **.mdb** はファイル名拡張子としてブロックされます)。  

-   配布ポイントで IIS の既定の構成を使用する場合、BITS を使用するクライアントは配布ポイントからこのソフトウェア展開をダウンロードできず、コンテンツの待機状態となります。  

-   このコンテンツをクライアントがダウンロードできるようにするためには、展開するパッケージとアプリケーションに含まれているファイル拡張子およびフォルダーへのアクセスを許可するように、該当するすべての配布ポイントで、IIS マネージャーの**要求フィルター**を編集する必要があります。  

> [!IMPORTANT]  
>  要求フィルターを編集すると、コンピューターの攻撃対象領域が拡大する可能性があります。  
>   
>  -   サーバー レベルで行った編集は、そのサーバー上のすべての Web サイトに適用されます。  
> -   個々の Web サイトに対して行った編集は、その Web サイトにのみ適用されます。  
>   
>  専用の Web サーバーで Configuration Manager を実行するのが、セキュリティ上は最適な方法です。 Web サーバー上で他のアプリケーションを実行する必要がある場合は、Configuration Manager のカスタム Web サイトを使用します。 詳細については、「[System Center Configuration Manager のサイト システム サーバーの Web サイト](../../../core/plan-design/network/websites-for-site-system-servers.md)」を参照してください。  

## <a name="http-verbs"></a>HTTP 動詞
**管理ポイント:** クライアントが管理ポイントと正常に通信できるように、管理ポイント サーバーで次の HTTP 動詞が許可されていることを確認します。  
 - GET
 - POST
 - CCM_POST
 - HEAD
 - PROPFIND

**配布ポイント:** 配布ポイントでは、次の HTTP 動詞が許可されている必要があります。
 - GET
 - HEAD
 - PROPFIND

要求のフィルタリングを構成する方法の詳細については、TechNet の「[Configure Request Filtering in IIS](https://technet.microsoft.com/library/hh831621.aspx#Verbs)」 (IIS で要求フィルターを構成する) または管理ポイントをホストする Windows Server のバージョンに適用される同様のドキュメントを参照してください。

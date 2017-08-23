---
title: "インストール シナリオ | Microsoft Docs"
description: "サイトを更新またはアップグレードするときに新しい Configuration Manager 階層をインストールする手法について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35586a85-4af9-4c8b-925a-0e32dc8b7346
caps.latest.revision: "6"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 938b2970e4d8534fdd5f3daf0c9a5ddb1f576e60
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="scenarios-to-streamline-your-installation-of-system-center-configuration-manager"></a>System Center Configuration Manager のインストールを合理化するシナリオ

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の Current Branch の更新プログラムのバージョンのリリースには、更新プログラムのバージョン (更新プログラム 1610 など) への新しい階層のインストールを効率化したり、Microsoft System Center 2012 Configuration Manager からアップグレードしたりするための新しいシナリオがあります。

次のシナリオがサポートされます。  

**更新プログラムのバージョンを実行する新しい System Center Configuration Manager の Current Branch の階層** をインストールする:  

-   最上階層のサイトのみをインストールした直後に、使用する更新プログラムのバージョンでサイトを更新する更新プログラムをインストールします。 次に、追加サイトをその更新プログラムのバージョンに直接インストールできます。  
-   このシナリオでは、基本レベルへの追加サイトのインストールのプロセスをスキップし、使用する更新プログラムのバージョンへそれらを更新します。  
-   このシナリオでは、構成基準バージョンへのクライアントのインストールのプロセスをスキップし、新しいバージョンに更新するときにそれらを再インストールします。  

 **Microsoft System Center 2012 Configuration Manager** インフラストラクチャを System Center Configuration Manager の更新プログラムのバージョンにアップグレードします。  

-   中央管理サイトと各プライマリ サイトを構成基準のバージョン (バージョン 1606 など) に手動でアップグレードしてから、更新プログラムのバージョン (バージョン 1610 など) をインストールします。  
-   使用する更新プログラムのバージョンがプライマリ サイトで実行されるようになるまで、セカンダリ サイトを System Center 2012 Configuration Manager からアップグレードしないでください。  
-   使用する更新プログラムのバージョンがプライマリ サイトで実行されるようになるまで、クライアントを System Center 2012 Configuration Manager からアップグレードしないでください。  

## <a name="scenario-install-a-new-hierarchy-to-an-update-version"></a>シナリオ - 更新プログラムのバージョンへの新しい階層のインストール  
このシナリオ例では、System Center Configuration Manager の構成基準のバージョン (バージョン 1610 など) を使用して、階層の最初のサイトをインストールします。 次に、1610 更新プログラムをインストールしてから、追加サイトまたはクライアントを展開します。  

-   更新プログラムのバージョン (バージョン 1610 など) を使用して、構成基準のバージョン (バージョン 1606 など) に留まらないことを計画しているので、追加サイトをインストールしてからアップグレードする必要はありません。 これはクライアントにも当てはまります。  
-   バージョン 1606 のセカンダリ サイトをインストールしてからバージョン 1610 にアップグレードしないでください。 代わりに、プライマリ サイトで 1610 のバージョンを実行した後に、セカンダリ サイトをインストールします。  

この順序に従います。  

1.  構成基準メディアを使用して、**新しい階層の最上階層サイトをインストールします**。  

    -   構成基準メディアは、新しい階層の最初のサイトのインストールにのみ使用できます。  
    -   たとえば、構成基準のバージョン 1606 を使用して、最上階層サイトをインストールします。 詳細については、「[セットアップ ウィザードを使用してサイトをインストールする](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)」を参照してください。  

    この手順の後には、最上階層サイトはバージョン 1606 を実行します。  

2.  **コンソール内の更新プログラムを使用して、最上階層サイトを新しいバージョンに更新します。**  

    -   使用を計画している更新プログラムのバージョンに最上階層サイトを更新してから、すべての子サイトまたはクライアントをインストールします。  
    -   たとえば、バージョン 1606 を実行している最上階層サイトをバージョン 1610 に更新できます。 詳細については、「[System Center Configuration Manager の更新プログラム](../../../../core/servers/manage/updates.md)」を参照してください。  

    この手順の後には、最上階層サイトはバージョン 1610 を実行します。  

3.  **中央管理サイトの下に、新しい子プライマリ サイトをインストールします。**  

    -   中央管理サイト サーバーで CD.Latest フォルダーからのインストール メディアを使用して、子プライマリ サイトをインストールします 詳細については、[「System Center Configuration Manager の CD.Latest フォルダー」](../../../../core/servers/manage/the-cd.latest-folder.md)」をご覧ください。  

      このソース メディアは、新しい子プライマリ サイトと中央管理サイトのバージョンを一致させるために必要です。  

    この手順の後に、新しい子プライマリ サイトは、バージョン 1610 を実行します。  

4.  **各プライマリ サイトには、コンソール内のオプションを使用して、新しいセカンダリ サイトをインストールします。**  

    -   プライマリ サイトがバージョン 1606 であった期間はセカンダリ サイトをインストールしなかったので、セカンダリ サイトをアップグレードする必要はありません。  
    -   代わりに、バージョン 1610 を実行する新しいセカンダリ サイトをインストールします。 詳細については、「[セットアップ ウィザードを使用してサイトをインストールする](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites)」トピックの「[セカンダリ サイトのインストール](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_secondary)」をご覧ください。  

    この手順の後には、新しいセカンダリ サイトがインストールされて、バージョン 1610 が実行されます。  

5.  **プライマリ サイトに新しいクライアントをインストールします。**  

    -   プライマリ サイトがバージョン 1606 であった期間はクライアントをインストールしなかったので、クライアントをバージョン 1606 からバージョン 1610 にアップグレードする必要はありません。  
    -   代わりに、バージョン 1610 を実行する新しいクライアントをインストールします。 詳細については、「[Deploy clients in System Center Configuration Manager](../../../clients/deploy/deploy-clients-to-windows-computers.md)」 (System Center Configuration Manager でクライアントを展開する) を参照してください。  

    この手順の後には、バージョン 1610 を実行する新しいクライアントがインストールされます。  

## <a name="scenario-upgrade-system-center-2012-configuration-manager-to-an-update-version-of-system-center-configuration-manager-current-branch"></a>シナリオ: System Center 2012 Configuration Manager を System Center Configuration Manager の Current Branch の更新プログラムのバージョンにアップグレードする  
このシナリオの例では、Microsoft System Center 2012 Configuration Manager インフラストラクチャを System Center Configuration Manager の更新プログラムのバージョン (バージョン 1610 など) にアップグレードします。  

-   中央管理サイトおよび各プライマリ サイトを構成基準のバージョン 1606 にアップグレードしてから、バージョン 1610 の更新プログラムをインストールする必要があります。  
-   セカンダリ サイトとクライアントをアップグレードしたり、バージョン 1606 をインストールしたりすることはありません。 代わりに、Microsoft System Center 2012 Configuration Manager から System Center Configuration Manager バージョンに 1610 に直接移行します。  

この順序に従います。  

1.  System Center Configuration Manager (バージョン 1606 など) のソース メディアを使用して、**最上階層 Microsoft System Center 2012 Configuration Manager サイトを** Current Branch の構成基準バージョンにアップグレードします。 詳細については、「[System Center Configuration Manager へのアップグレード](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md)」を参照してください。  

    -   従来のアップグレード シナリオのように、階層の最上階層サイトを最初にアップグレードしてから、子サイトをアップグレードします。  

    この手順の後には、最上階層サイトはバージョン 1606 を実行します。  

2.  同じ構成基準のバージョンに**階層内の各子プライマリ サイトをアップグレード** します。  

    -   Microsoft System Center 2012 Configuration Manager からアップグレードするときには、各プライマリ サイトを Current Branch の構成基準のバージョンに手動でアップグレードする必要があります。  
    -   この時点でセカンダリ サイトをアップグレードすることはありません。  

    この手順の後には、各プライマリ サイトはバージョン 1606 を実行します。  

3.  **子プライマリ サイトのメンテナンス期間を設定します。** すべてのプライマリ サイトを構成基準のバージョンにアップグレードしたら、それらのサイトがインフラストラクチャの更新プログラムをインストール時期を制御するメンテナンス期間の構成を計画します。 詳細については、「[System Center Configuration Manager でメンテナンス期間を使用する方法](../../../../core/clients/manage/collections/use-maintenance-windows.md)」をご覧ください。  (バージョン 1606 では、メンテナンス期間は*サービス時間帯*と呼ばれます。)  

    -   子プライマリ サイトは、中央管理サイトにインストールされる同じ更新プログラムを自動的にインストールします。  
    -   セカンダリ サイトは新しいバージョンを自動的にインストールしません。 コンソール内から手動でそれらをアップグレードする必要があります。  

  この手順の後に、更新プログラムが中央管理サイトにインストールされると、子プライマリ サイトはその更新プログラムだけをメンテナンス期間中にインストールします。  

4.  **最上階層サイトに更新プログラムのバージョンをインストールします。** これにより、最上階層サイトが更新されます。 中央管理サイトが更新プログラムのバージョンをインストールしたら、メンテナンス期間によってインストールがブロックされていない限り、各子プライマリ サイトは更新プログラムを自動的にインストールします。  

    -   たとえば、最上階層サイトをバージョン 1606 からバージョン 1610 に更新できます。 詳細については、「[System Center Configuration Manager の更新プログラム](../../../../core/servers/manage/updates.md)」を参照してください。  

    この手順の後に、中央管理サイトと各プライマリ サイトはバージョン 1610 を実行します。  

5.  **セカンダリ サイトをアップグレードします。** プライマリ サイトが更新プログラムをインストールしてバージョン 1610 を実行するようになったら、コンソール内のオプションを使用して、セカンダリ サイトをアップグレードします。  

    -   これにより、セカンダリ サイトは Microsoft System Center 2012 Configuration Manager から、プライマリ サイトにインストールした更新プログラムのバージョンに直接アップグレードされます。  
    -   セカンダリ サイトのアップグレードの詳細については、「[System Center Configuration Manager へのアップグレード](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md)」の「[サイトをアップグレードする](../../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_upgrade)」を参照してください。  

6.  **クライアントをアップグレードする** クライアントをアップグレードするには、「[System Center Configuration Manager で Windows コンピューター用クライアントをアップグレードする方法](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)」を参照してください。  

    -   これにより、クライアントは Microsoft System Center 2012 Configuration Manager から、プライマリ サイトにインストールした更新プログラムのバージョンに直接アップグレードされます。  

    この手順の後に、クライアントは最初にバージョン 1606 にアップグレードすることなく、バージョン 1610 にアップグレードされます。

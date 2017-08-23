---
title: "仮想デスクトップ インフラストラクチャ (VDI) クライアント管理 | Microsoft Docs "
description: "仮想デスクトップ インフラストラクチャ (VDI) で System Center Configuration Manager クライアントを管理します。"
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: abd45393-d84e-4583-bc80-74bbb3709577
caps.latest.revision: "7"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d73daf6427b8c58d21d579f3b41df513cc3e3b0b
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="considerations-for-managing-system-center-configuration-manager-clients--in-a-virtual-desktop-infrastructure-vdi"></a>仮想デスクトップ インフラストラクチャ (VDI) で System Center Configuration Manager クライアントを管理するための考慮事項

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager では、次の仮想デスクトップ インフラストラクチャ (VDI) シナリオでの Configuration Manager クライアントのインストールがサポートされています。  

-   **パーソナル バーチャル マシン** - パーソナル バーチャル マシンは、一般的に、セッション間でユーザーのデータと設定をバーチャル マシンに保持する場合に使用します。  

-   **リモート デスクトップ サービス セッション** - リモート デスクトップ サービスを使用して、1 つのサーバーで複数の同時クライアント セッションをホストできます。 ユーザーはセッションに接続し、そのサーバーでアプリケーションを実行できます。  

-   **プール バーチャル マシン** - プール バーチャル マシンはセッション間で保持されません。 セッションを閉じると、すべてのデータと設定が破棄されます。 プール バーチャル マシンは、クライアント セッションをホストする Windows Server で必要なビジネス アプリケーションを実行できないことが原因で、リモート デスクトップ サービスを使用できない場合に有用です。  

 仮想デスクトップ インフラストラクチャで Configuration Manager クライアントを管理する場合の考慮事項の一覧を次の表に示します。  

|バーチャル マシンの種類|注意事項|  
|--------------------------|--------------------|  
|パーソナル バーチャル マシン|Configuration Manager ではパーソナル バーチャル マシンを物理コンピューターと同じものとして扱います。 Configuration Manager クライアントは、バーチャル マシン イメージに事前インストールするか、バーチャル マシンの事前準備の後に展開できます。|  
|リモート デスクトップ サービス|Configuration Manager クライアントは、個別のリモート デスクトップ セッション用にインストールされません。 クライアントは、リモート デスクトップ サービス サーバーに一度だけインストールされます。 リモート デスクトップ サービス サーバーではすべての Configuration Manager 機能を使用できます。|  
|プール バーチャル マシン|プール バーチャル マシンを使用停止すると、Configuration Manager を使用して行った変更はすべて失われます。<br /><br /> バーチャル マシンは短時間のみ運用されることがあるため、ハードウェア インベントリ、ソフトウェア インベントリ、ソフトウェア メータリングなどの Configuration Manager 機能から返されるデータはニーズと関係がない可能性があります。 インベントリ タスクからプール バーチャル マシンを除外することを考慮してください。|  

 仮想化では、同一の物理コンピューターでの複数の Configuration Manager クライアントの実行がサポートされるため、多くのクライアント操作には、ハードウェアおよびソフトウェア インベントリ、マルウェア対策スキャン、ソフトウェアのインストール、ソフトウェア更新プログラムのスキャンなどのスケジュールされた操作で、組み込みのランダム待機時間があります。 この待機時間に、Configuration Manager クライアントを実行する複数のバーチャル マシンを持つコンピューターの CPU 処理とデータ転送を分散することができます。  

> [!NOTE]  
>  保守モードの Windows Embedded クライアントを除き、仮想化環境で実行されていない Configuration Manager クライアントも、このランダム待機時間を使用します。 多くのクライアントが展開されている場合、この動作によって、ネットワーク帯域幅のピークを回避し、管理ポイントやサイト サーバーなどの Configuration Manager サイト システムの CPU 処理要件を減らすことができます。 待機時間の間隔は、Configuration Manager の機能によって変わります。  
>   
>  次のクライアント設定を使用して、必要なソフトウェア更新プログラムと必要なアプリケーション展開のランダム待機時間を既定で無効にできます。 **コンピューター エージェント**: **期限のランダム化を無効にする**。

---
title: "Long-Term Servicing Branch の概要 | Microsoft Docs"
description: "System Center Configuration Manager の Long-Term Servicing Branch について説明します。"
ms.custom: na
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
caps.latest.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 91c1ca860069c6ebe0d20230c4620bf3f68735a2
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>System Center Configuration Manager の Long-Term Servicing Branch の概要

*適用対象: System Center Configuration Manager (Long-Term Servicing Branch)*

System Center Configuration Manager の Long-Term Servicing Branch (LTSB) は、Configuration Manager のブランチの 1 つで、すべてのユーザーが使用できるインストール オプションとして設計されています。 ただし、Configuration Manager のソフトウェア アシュアランス (SA) または同等のサブスクリプションが期限切れになったユーザーにとっては、この LTSB が唯一の選択肢になります。


Configuration Manager バージョン 1606 では、Configuration Manager の Current Branch と比較すると、LTSB の機能は制限されています。

 > [!TIP]   
 > **Windows Server** のブランチの詳細については、ブログ記事 [Windows Server 2016 の新しい Current Branch for Business サービス オプション]( https://blogs.technet.microsoft.com/windowsserver/2016/07/12/windows-server-2016-new-current-branch-for-business-servicing-option/) (Windows Server 2016 new Current Branch for Business servicing option) をご覧ください。

## <a name="features-that-are-not-available-in-the-ltsb-of-configuration-manager"></a>Configuration Manager の LTSB で使用できない機能
Configuration Manager の Current Branch では、LTSB の場合には使用できない次の機能がサポートされています。

-   新しい機能を追加したり機能を改善したりする、コンソール内の更新プログラム。
-   サイト サーバーとクライアントとして使用する新しくリリースされたオペレーティング システムのサポート。
-   以下のことをサポートする Microsoft Intune サブスクリプションの使用:
    -   ハイブリッド モバイル デバイス管理 (MDM) 構成の Intune
    -   オンプレミス MDM
-   Windows 10 サービス ダッシュボード、サービス プランのサポート (最近の Windows 10 の Current Branch (CB) と Current Branch for Business (CBB) バージョンのサポートも含む)  
-   Windows Server と Windows 10 LTSB の今後のリリースのサポート
-   資産インテリジェンス
-   クラウドベースの配布ポイント
-   Exchange Online と Exchange Connector    

これらの機能やサポートは LTSB では使用できません。一部の機能は Configuration Manager コンソールに表示されますが、選択したり使用したりすることはできません。


## <a name="find-documentation-for-the-ltsb"></a>LTSB のドキュメントを検索する
LTSB は、Current Branch バージョン 1606 に基づいています。 製品ドキュメントについては、[Current Branch の ドキュメント](https://docs.microsoft.com/sccm/)に関するページをご覧ください。LTSB 固有の注意事項と制限事項があります。 次のオンライン トピックで、注意事項と制限事項を確認できます。

-     [Long-Term Servicing Branch の概要](introduction-to-the-ltsb.md): (このトピック)
-     [Long-Term Servicing Branch のインストール](install-the-ltsb.md)
-     [Long-Term Servicing Branch の Current Branch へのアップグレード](convert-to-current-branch.md)
-     [Long-Term Servicing Branch でサポートされている構成](supported-configurations-for-ltsb.md)
-   [Configuration Manager の Long-Term Servicing Branch の管理](manage-the-ltsb.md)

LTSB について Current Branch ドキュメントを参照する場合、バージョン 1606 についての説明は LTSB にも当てはまります。 バージョン 1610 以降で導入された機能や説明は LTSB ではサポートされません。


## <a name="licensing-overview-for-the-ltsb"></a>LTSB のライセンスの概要   
2016 年 10 月 1 日の時点で System Center Configuration Manager ライセンスに対してソフトウェア アシュアランス (SA) が有効になっているお客様または同等のサブスクリプション権限を持っているお客様には、2016 年 10 月リリースのバージョン 1606 の System Center Configuration Manager を使用する権限があります。 2016 年 10 月 1 日以降、System Center Configuration Manager に対する権限を持つお客様には、インストール時に Current Branch および Long-Term Servicing Branch (LTSB) の 2 つのライセンス オプションが表示されます。

System Center Configuration Manager に対して永続的な権利を持つお客様または、10 月 1 日の後に SA またはサブスクリプションが期限切れになったお客様は、該当する時点で最新のバージョンである System Center Configuration Manager LTSB をインストールできます。

[Microsoft ボリューム ライセンス プログラムを通して購入する製品の使用条件についてはこちらを参照してください](http://go.microsoft.com/fwlink/?LinkId=800052)。

Configuration Manager のブランチの詳細については、[System Center Configuration Manager のライセンスとブランチ](learn-more-editions.md)に関するページをご覧ください。

## <a name="next-steps"></a>次のステップ

お使いの環境に適したブランチは Configuration Manager LTSB だと思われた場合は、新しい階層の一部として[新しい LTSB サイトをインストールする](/sccm/core/understand/install-the-ltsb#install-a-new-site)か、[System Center 2012 Configuration Manager サイトと階層をアップグレード](/sccm/core/understand/install-the-ltsb#upgrade-from-system-center-2012-configuration-manager)してください。

インストール メディアがない場合は、[System Center 2016 ドキュメント](https://technet.microsoft.com/system-center-docs/system-center)に関するページをご覧ください。System Center 2016 の取得方法と System Center Configuration Manager LTSB のインストールに使用できるメディアの情報が確認できます。  

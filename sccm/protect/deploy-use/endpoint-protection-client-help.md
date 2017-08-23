---
title: "Endpoint Protection クライアント ヘルプ | Microsoft Docs"
description: "コンピューターを脅威から保護するのに役立つ Endpoint Protection の機能と拡張機能について説明します。"
ms.custom: na
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fdcee455-22e3-451d-bcf3-e7b62792f04a
caps.latest.revision: "6"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 212c73fcb947c3b56da6055bf47fe078301ad90d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="endpoint-protection-client-help"></a>Endpoint Protection クライアント ヘルプ

*適用対象: System Center Configuration Manager (Current Branch)*


このバージョンの Windows Defender または Endpoint Protection には、コンピューターを脅威から保護するのに役立つ、次のような機能があります。  

-   **Windows ファイアウォールとの統合。** Endpoint Protection セットアップで Windows ファイアウォールを有効または無効にできます。  
-   **ネットワーク検査システム:** ネットワーク トラフィックを検査して、既知のネットワークベースの脆弱性の悪用を未然に防ぐことで、リアルタイム保護機能を強化します。  
-   **保護エンジン。** リアルタイム保護では、PC にインストールされているか実行されているマルウェアを見つけて阻止します。 更新されたエンジンでは、保護機能と除去機能が拡張され、パフォーマンスが改善されています。  

Windows Defender は、Windows 10 オペレーティング システムの一部として提供されます。  以前のバージョンの Windows では、管理者は、管理ソフトウェアを使用して Windows Defender または Endpoint Protection を提供することができます。

「[Windows Defender と Endpoint Protection についてよく寄せられる質問](endpoint-protection-client-faq.md)」の一覧もあります。 トラブルシューティングについては、「[Windows Defender または Endpoint Protection クライアントのトラブルシューティング](troubleshoot-endpoint-client.md)」を参照してください。 新機能のリストについては、「[Windows Defender の新機能](https://support.microsoft.com/help/29276/windows-10-whats-new-in-windows-defender)」を参照してください。

## <a name="windows-firewall-integration"></a>Windows ファイアウォールとの統合  
 Windows ファイアウォールは、攻撃者や悪意のあるソフトウェアがインターネットやネットワークを介してコンピューターにアクセスすることを防ぐうえで役立ちます。 Endpoint Protection のインストール時に、インストール ウィザードによって Windows ファイアウォールが有効であるかどうかが確認されるようになりました。 Windows ファイアウォールを意図的に無効にしていた場合は、チェック ボックスをオフにすることで有効にならないようにすることができます。 Windows ファイアウォールの設定は、コントロール パネルのシステムとセキュリティの設定からいつでも変更できます。  

## <a name="network-inspection-system"></a>ネットワーク検査システム  
 ソフトウェア ベンダーがセキュリティ更新プログラムを開発し配布する前に、未対応の脆弱性をねらったネットワーク ベースの攻撃が実行されるケースが増えています。 脆弱性についての研究によると、最初の攻撃が報告されてから適切なセキュリティ更新プログラムが開発、テスト、およびリリースされるまで、1 か月かかることがあります。 この保護の時間差によって、相当の期間、多数のコンピューターが攻撃や脆弱性の悪用に対して無防備になります。 ネットワーク検査システムはリアルタイム保護と連携して、脆弱性の発覚から修正プログラムの開発までの期間を数週間から数時間に短縮することで、ネットワーク ベースの攻撃に対する保護を強化しています。  

## <a name="award-winning-protection-engine"></a>受賞歴のある保護エンジン  
 Windows Defender や Endpoint Protection の中身は、定期的に更新される、受賞歴のある保護エンジンです。 このエンジンは、マイクロソフト マルウェア プロテクション センターのマルウェア対策研究者のチームによって支えられ、最新のマルウェアの脅威に 24 時間体制で対応しています。  

## <a name="windows-defender-settings"></a>Windows Defender の設定
Windows Defender の設定で、悪意のあるソフトウェアから PC を保護できるようにします。 管理者は、ユーザーに代わって、いくつかの Windows Defender の設定を管理する場合があります。 Windows Defender の設定を使用すれば、他のユーザーを管理することができます。 PC とデータを保護するのに役立つ Windows Defender の設定を有効にすることをお勧めします。

Windows Defender の設定を表示するには、PC で `Windows Defender` を検索します。 **Windows Defender** を開き、**[設定]** を選択します。 Windows Defender の設定には以下のものが含まれます。
- **リアルタイム保護** - PC にインストールされているか実行されているマルウェアを見つけて阻止します。
- **クラウドベースの保護** - Windows Defender は、潜在的なセキュリティ脅威について Microsoft に情報を送信します。
- **自動サンプル送信** - Windows Defender で不審なファイルのサンプルを Microsoft に送信し、マルウェア検出を強化できるようにします。
- **除外** - Windows Defender でのスキャン対象から、特定のファイル、フォルダー、ファイル拡張子、プロセスを除外することができます。
- **拡張通知** - PC の正常性に関する通知を有効にします。 **[オフ]** にしても、重要な通知は受け取れます。
- **Windows Defender オフライン** - Windows Defender オフラインを実行することで、悪意のあるソフトウェアを見つけて削除することができます。 このスキャンでは PC が再起動され、完了まで約 15 分かかります。

### <a name="see-also"></a>関連項目  
 [Endpoint Protection クライアントのよく寄せられる質問](endpoint-protection-client-faq.md)   
 [Windows Defender または Endpoint Protection クライアントのトラブルシューティング](troubleshoot-endpoint-client.md)

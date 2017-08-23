---
title: "リスクに基づいたアクセスの制限 | Microsoft Docs"
description: "デバイス、ネットワーク、アプリケーションのリスクに基づいてアクセスを制限します。"
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 250671660c1c6da0ca9b593b06b8f344dfe17ad6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>デバイス、ネットワーク、アプリケーションのリスクに基づき、会社のリソースへのアクセスを管理する

*適用対象: System Center Configuration Manager (Current Branch)*

Mobile Threat Defense コネクターを使用すると、選択した Mobile Threat Defense ベンダーをコンプライアンス ポリシーと条件付きアクセス規則の情報ソースとして活用できます。 これにより、IT 管理者が、特に危険にさらされたモバイル デバイスから、Exchange、Sharepoint などの企業リソースに保護レイヤーを追加することができます。

## <a name="what-problem-does-this-solve"></a>これはどのような問題を解決しますか。

会社は物理的な脅威、アプリ ベースの脅威、ネットワーク ベースの脅威など、新種の脅威やオペレーティング システムの脆弱性から機密データを保護する必要があります。
これまで、企業は PC の防御を積極的に行ってきましたが、モバイル デバイスは監視や保護のない状態が続いていました。 モバイル プラットフォームには、アプリの分離や検証済みコンシューマー アプリ ストアなどの防御手法が組み込まれていますが、依然として高度な攻撃を受けやすい状態にあります。 今日では、仕事でモバイル デバイスを利用して、機密情報にアクセスする社員が増えています。 より高度さを増す攻撃からモバイル デバイスを守る必要があります。

[ハイブリッド MDM 展開 (SCCM と Intune)](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) では、パートナーが提供する Mobile Threat Defense のようなデバイスを脅威から守るためのソリューションが提供するリスク評価に基づき、会社のリソースやデータへのアクセスを制御できます。

## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>Intune Mobile Threat Defense コネクターのしくみ

このコネクターは、Intune と選択した Mobile Threat Defense ベンダーの間に通信チャネルを作成することで、会社のリソースを保護します。 Intune Mobile Threat Defense パートナーは、直感的で簡単に展開できるモバイル デバイス向けアプリケーションを提供します。これらのアプリケーションは、脅威情報を積極的にスキャンして分析し、レポートや強制を目的として Intune と共有します。 たとえば、Mobile Threat Defense アプリが、ネットワーク上の電話が Man in the Middle 攻撃に対して脆弱なネットワークに接続されていることを Mobile Threat Defense ベンダーに報告した場合、この情報は共有されて適切なリスク レベル (低/中/高) に分類されます。その後、Intune で構成済みのリスク レベル許容度と比較されて、デバイスが侵害されたときに選択した特定のリソースへのアクセスを無効にする必要があるかどうかが判断されます。

## <a name="sample-scenarios"></a>サンプル事例

Mobile Threat Defense ソリューションによってデバイスが感染したと見なされた場合

![Mobile Threat Defense の感染デバイス](../media/mtp/MTD-image-1.png)

デバイスが修復されたときにアクセスが許可されます。

![Mobile Threat Defense のアクセス許可](../media/mtp/MTD-image-2.png)

## <a name="next-steps"></a>次のステップ

デバイス、ネットワーク、アプリケーションのリスクに基づいて、会社のリソースへのアクセスを保護する方法について説明します。次のものを使用します。

- [Lookout](https://docs.microsoft.com/intune/deploy-use/lookout-mobile-threat-defense-connector)
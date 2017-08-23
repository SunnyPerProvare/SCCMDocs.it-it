---
title: "電源管理のベスト プラクティス | Microsoft Docs"
description: "System Center Configuration Manager の電源管理のベスト プラクティスを示します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9f7142e1-c972-4384-853b-2da1568cb3e3
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: d3cc24c7923141f039dcda26ac27489cb0143e89
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="best-practices-for-power-management-in-system-center-configuration-manager"></a>System Center Configuration Manager の電源管理のベスト プラクティス

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の電源管理に関する以下のベスト プラクティスを使用してください。  

## <a name="perform-the-monitoring-phase-at-a-representative-time"></a>監視段階は代表的な時間帯に実施する  
 電源管理の監視段階により、組織内のコンピューターの電力消費、電源動作、電源管理機能、および環境影響量に関する情報を得ることができます。 監視段階は、代表的な時間に実施してください。 たとえば、監視段階を休日に実施した場合、コンピューターの電力使用状況についての現実的なレポートを入手することはできません。  

## <a name="create-a-control-collection-of-computers-with-no-power-plans-applied"></a>電源プランが適用されていないコンピューターのリストを作成する  
 2 つのコンピューター コレクションを作成して、電源プランをコンピューターに適用した場合の影響を監視します。 一方のコレクションには、サブ コレクションに電源設定を適用する大半のコンピューターを含め、もう一方のコレクション (コントロール コレクション) には残りのコンピューターを含めます。 大半のコンピューターが含まれる方のコレクションに、必要な電源管理プランを適用します。 その後、レポートを実行すると、電源設定が適用されているコンピューターの電力コスト、電力使用状況、および環境への影響を、電源設定が適用されていないコントロール コレクションの情報と比較できます。  

## <a name="run-the-power-settings-report-before-you-apply-a-power-management-plan"></a>電源管理プランを適用する前に、[電源設定] レポートを実行する。  
 コンピューターのコレクションに電源管理プランを適用する前に、[電源設定] レポートを実行すると、そのコレクション内のコンピューターで既に構成されている電源管理設定についての理解を深めることができます。 **** 既存の設定について調査を行わずに新しい電源管理設定を適用すると、電力消費量が増える結果になる可能性があります。  

## <a name="exclude-servers-from-power-management"></a>電源管理からサーバーを除外する  
 Windows Server を実行しているコンピューターの電源管理はサポートされていません (ただし、電力使用状況データは収集されます)。 サーバーをコレクションに追加し、そのコレクションを電源管理から除外します。  

## <a name="exclude-computers-that-you-do-not-want-to-manage"></a>管理に適さないコンピューターを除外する  
 電源管理で管理したくないコンピューターがある場合、これらのコンピューターを特定のコレクションに追加して、そのコレクションを電源管理の対象から除外します。  

 次のようなコンピューターは、電源管理に適していません。  

-   電源を常にオンにしておく必要のあるコンピューター  

-   ユーザーがリモート デスクトップ接続を使って接続する必要のあるコンピューター  

-   電源管理機能を使用できないコンピューター  

-   配布ポイント サイト システムの役割を持つコンピューター  

-   キオスク コンピューター、情報表示用コンピューター、監視用コンソールなど、コンピューターおよびモニターを常にオンにしておく必要のある、公共のコンピューター  

 詳細については、「[System Center Configuration Manager での電源管理の構成](../../../../core/clients/manage/power/configuring-power-management.md)」を参照してください。  

## <a name="first-apply-power-plans-to-a-test-collection-of-computers"></a>電源プランは、まずテスト用のコンピューター コレクションに適用する  
 電源管理プランを多数のコンピューターが含まれるコレクションに適用する前に、テスト用のコレクションに適用して、電源プランの効果をテストします。  

 Windows XP または Windows Server 2003 を実行するコンピューターに適用された電源設定は、そのコンピューターを電源管理から除外した場合でも、元の値に戻りません。 Windows のこれより新しいバージョンでは、電源管理からコンピューターを除外すると、すべての電源設定が元の値に戻ります。 個々の電源設定をその元の値に戻すことはできません。  

## <a name="apply-power-plan-settings-individually"></a>電源プラン設定はそれぞれ個別に適用する  
 それぞれの設定により目的の効果が得られることを確認するため、電源設定は一度に 1 つずつ適用してその効果を監視します。 電源プランの設定の詳細については、「[System Center Configuration Manager で電源プランを作成して適用する方法](../../../../core/clients/manage/power/create-and-apply-power-plans.md)」トピックの「[使用できる電源管理プランの設定](../../../../core/clients/manage/power/create-and-apply-power-plans.md#BKMK_Plans)」を参照してください。  

## <a name="regularly-monitor-computers-to-see-if-they-have-multiple-power-plans-applied"></a>コンピューターを定期的に監視して、複数の電源プランが適用されていないか確認する  
 電源管理では、複数の電源プランが適用されているコンピューターを表示するレポートを作成できます。  

 コンピューターが、それぞれ異なる電源プランが適用されている複数のコレクションのメンバーである場合、次の処理が行われます。  

-   電源プラン: 1 台のコンピューターに複数の電源設定値が適用されている場合、最も制限の緩い値が使用されます。  

-   ウェイクアップ時間: 1 台のデスクトップ コンピューターに複数のウェイクアップ時間が適用されている場合、深夜に最も近い時間が使用されます。  

     詳細については、「[System Center Configuration Manager で電源管理を監視して計画する方法](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md)」トピックの「[電源プランが複数あるコンピューター](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Multiple)」を参照してください。 電源管理が競合を解決する方法の詳細については、「[System Center Configuration Manager で電源プランを作成して適用する方法](../../../../core/clients/manage/power/create-and-apply-power-plans.md)」を参照してください。  

## <a name="save-or-export-power-management-information-during-the-monitoring-and-planning-phase-of-power-management"></a>電源管理の監視段階と計画段階で、電源管理情報を保存またはエクスポートする  
 日次レポートで使用される電源管理情報は、Configuration Manager サイト データベースに 31 日間保持されます。  

 月次レポートで使用される電源管理情報は、Configuration Manager サイト データベースに 13 か月間保持されます。  

 電源管理の監視、計画、コンプライアンス対応評価の段階でレポートを実行する場合、後日 Configuration Manager によってこれらのレポートが削除された場合にもデータを比較できるよう、すべてのレポートの結果を保存またはエクスポートしておくことをお勧めします。  

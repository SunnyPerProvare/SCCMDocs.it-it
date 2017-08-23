---
title: "クライアントの監視 - Configuration Manager で Windows Analytics を使用する | Microsoft Docs"
description: "Windows Analytics は、Operations Management Suite 上で実行するソリューションのセットで、環境内のデバイスによってレポートされる Windows 利用統計情報を利用して、環境の現在の状態に有益な洞察を導くことができます。"
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
caps.latest.revision: "23"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: adabe8f475eb12dd44005ec07344e8565be20582
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="use-windows-analytics-with-configuration-manager"></a>Configuration Manager で Windows Analytics を使用する

*適用対象: System Center Configuration Manager (Current Branch)*

[Windows Analytics](https://www.microsoft.com/en-us/WindowsForBusiness/windows-analytics) は、[Operations Management Suite](/azure/operations-management-suite/operations-management-suite-overview) 上で実行するソリューションのセットです。 このソリューションでは、環境の現在の状態に洞察を形成することができます。 環境内のデバイスでは、Windows の利用統計情報がレポートされます。 このデータは、[Operations Management Suite の Web ポータル](https://mms.microsoft.com)のソリューションによって、アクセスおよび分析することができます。 [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) の場合、データは Upgrade Readiness と Configuration Manager を接続することによって、Configuration Manager の監視ノードで直接利用することもできます。

Windows Analytics によって使用される Windows 利用統計情報は、Configuration Manager サイト サーバーに直接転送されることはありません。 クライアント コンピューターは、Windows 利用統計情報を利用統計情報のサービスに送信します。 その後、関連するデータは、組織の OMS ワークスペースのいずれかでホストされている Windows Analytics ソリューションに転送されます。 Configuration Manager では、コンテキスト内リンクを持つ Web ポータルの関連するデータにユーザーを誘導したり、Configuration Manager に接続しているソリューションの一部であるデータを直接表示したりすることができます。 また、Operation Management Suite の Web ポータルからデータを直接クエリすることもできます。

>[!Important]
>Configuration Manager サイト サーバーから Microsoft にレポートされる、[Configuration Manager の診断と利用状況データ](../../plan-design/diagnostics/diagnostics-and-usage-data.md)は、Windows Analytics と Windows 利用統計情報とは完全に区別されています。

## <a name="configure-clients-to-report-data-to-windows-analytics"></a>Windows Analytics にデータをレポートするようにクライアントを構成する

クライアント デバイスで Windows Analytics にデータをレポートするために、デバイスは組織の Windows Analytics データをホストする、Operations Management Suite ワークスペースに関連付けられている業務用 ID で構成される必要があります。 また、デバイスは、使用する特定のソリューションに適切な利用統計情報のレベルで、利用統計情報をレポートするように構成される必要もあります。 

### <a name="configure-windows-analytics-client-settings"></a>Windows Analytics クライアント設定の構成
Windows Analytics を構成するには、Configuration Manager コンソールで、**[管理]** > **[クライアント設定]** を選択し、**[Create Custom Device Client Settings]\(カスタム デバイス クライアント設定の作成\)** をダブルクリックして、**[Windows Analytics]** を選択します。  

**[Windows Analytics]** 設定タブに移動した後に、以下を構成します。
  -  **商用 ID**  
商用 ID キーは、管理するデバイスから組織の Windows Analytics データをホストする OMS ワークスペースに情報をマップします。 使用する商用 ID キーを Upgrade Readiness で既に構成している場合は、その ID を使用します。 まだ商用 ID キーがない場合は、「[Generate your commercial ID key (商用 ID キーを生成する)]( https://technet.microsoft.com/itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key)」をご覧ください。

  -  **Windows 10 デバイスの利用統計情報のレベル**   
Windows 10 の利用統計情報の各レベルで収集される情報については、「[Configure Windows telemetry in your organization (組織の利用統計情報の構成)](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels)」をご覧ください。

  -  **Windows 7、8、8.1 デバイスでの商用データ収集のオプトイン**   
オプトインしたときにこれらのオペレーティング システムから収集されるデータについては、Microsoft のサイトから [Windows 7、Windows 8、Windows 8.1 の利用統計情報のイベントとフィールドに関する pdf ファイル](https://go.microsoft.com/fwlink/?LinkID=822965)をダウンロードして参照してください。

  -  **インターネット エクスプ ローラーのデータ収集を構成する**  
Windows 8.1 以前のバージョンが動作しているデバイスでは、Internet Explorer で収集されるデータによって、Upgrade Readiness が Web アプリケーションの非互換性を検出できるため、Windows 10 へのスムーズなアップグレードが妨げられる可能性が排除されます。 Internet Explorer のデータ収集は、インターネット ゾーンごとに有効にできます。 インターネット ゾーンの詳細については、「[About URL Security Zones (セキュリティ ゾーンについて)](https://msdn.microsoft.com/library/ms537183(v=vs.85).aspx)」をご覧ください。

## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>Upgrade Readiness を使用して Windows 10 の互換性の問題を特定する

Upgrade Readiness (旧称 Upgrade Analytics) を使用すると、デバイスの準備と Windows 10 との互換性を分析できます。 この評価ではスムーズなアップグレードが可能です。 Configuration Manager と Upgrade Readiness を接続した後、Configuration Manager コンソールからこのクライアントのアップグレードの互換性データに直接アクセスできます。 その後、デバイス リストからアップグレードまたは修復対象のデバイスを指定できます。

Upgrade Readiness を構成および接続する方法の詳細については、[Upgrade Readiness](../../clients/manage/upgrade/upgrade-analytics.md)に関するページを参照してください。

## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>Windows Analytics を使用して Windows 情報保護ポリシー内のギャップを識別する

[Windows 情報保護](https://docs.microsoft.com/en-us/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP) ポリシーで構成される Windows 10 バージョン 1703 以降のデバイスは、WIP ポリシー アプリケーション規則で構成されない環境内の会社のデータにアクセスするアプリケーションの利用統計情報をレポートします。 これらは、環境内のユーザーは生産性を保持するために必要ですが、アクセスがブロックされている可能性があるアプリケーションです。そのため、会社のデータにアクセスしている知識は、Configuration Manager の Windows 情報保護ポリシーのメンテナンスに役立つ場合があります。 

この Windows 情報保護データには、この [Operations Management Suite クエリ](https://go.microsoft.com/fwlink/?linkid=849952)を使用してアクセスできます。
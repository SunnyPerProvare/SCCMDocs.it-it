---
title: "正常性構成証明書 | Microsoft Docs"
description: "Configuration Manager コンソールに表示できるデバイス正常性構成証明書の機能について説明します。"
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91f9de33-b277-4500-acd6-e7d90a2947c9
caps.latest.revision: "17"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 54b3433a002b8ef29059bab04458138348f95d66
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="health-attestation-for-system-center-configuration-manager"></a>System Center Configuration Manager の正常性構成証明書

*適用対象: System Center Configuration Manager (Current Branch)*

管理者は Configuration Manager コンソールで [Windows 10 デバイス正常性構成証明](https://technet.microsoft.com/library/mt592023.aspx)の状態を確認できます。  デバイスの正常性構成証明で、管理者はクライアント コンピューターで次の信頼できる BIOS、TPM、およびブート ソフトウェアの構成が有効になっていることを確認できます。  

-   起動時マルウェア対策 - 起動時マルウェア対策 (ELAM) により、サードパーティのドライバーが初期化される前の起動時にコンピューターが保護されます。 [ELAM を有効にする方法](https://gallery.technet.microsoft.com/How-to-turn-on-Early-84552ec5)  
-   BitLocker - Windows BitLocker ドライブ暗号化は、Windows オペレーティング システムのボリュームに格納されているすべてのデータを暗号化できるソフトウェアです。  [BitLocker を有効にする方法](https://gallery.technet.microsoft.com/How-to-turn-on-BitLocker-34294d3d)  
-   セキュア ブート - セキュア ブートは、PC 業界のメンバーによって開発されたセキュリティ標準で、PC の製造元によって信頼されているソフトウェアのみを使用して PC が起動されるようにするのに役立ちます。 [セキュア ブートの詳細](https://technet.microsoft.com/library/hh824987.aspx)  
-   コードの整合性 - コードの整合性は、メモリに読み込まれるたびに、ドライバーまたはシステム ファイルの整合性を検証することによって、オペレーティング システムのセキュリティを強化する機能です。 [コードの整合性の詳細](https://technet.microsoft.com/library/dd348642.aspx)  

この機能は、Configuration Manager によって管理されている PC と内部設置型リソース、および Microsoft Intune で管理されているモバイル デバイスで利用できます。 管理者は、報告がクラウドを使用して行われるか、内部設置型インフラストラクチャを使用して行われるかを指定できます。 オンプレミスのデバイス正常性構成証明書の監視により、インターネット アクセスがなくても管理者がクライアント PC を監視することができます。

## <a name="enable-health-attestation"></a>正常性構成証明書を有効にする

 **要件:**  

-   [デバイス正常性構成証明書が有効になっている](https://technet.microsoft.com/windows-server-docs/security/device-health-attestation)、Windows 10 バージョン 1607 または Windows Server 2016 バージョン 1607 を実行しているクライアント デバイス
-    TPM 1.2 または TPM 2 が有効になっているデバイス
-   Configuration Manager クライアント エージェントと has.spserv.microsoft.com (ポート 443) 正常性構成証明書サービス (クラウド管理)、またはデバイスの正常性構成証明書が有効な管理ポイント (オンプレミス) との間の通信

### <a name="how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Configuration Manager クライアント コンピューターの正常性構成証明書サービスの通信を有効にする方法

次の手順を使用して、インターネットに接続するデバイスのデバイス正常性構成証明書の監視を有効にします。

1.  Configuration Manager コンソールで、**[管理]**  >  **[概要]**  >  **[クライアント設定]** を選択します。  **[コンピューター エージェント]** 設定のタブを選択します。  
2.  **[既定の設定]** ダイアログ ボックスで、 **[コンピューター エージェント]** を選択して、 **[正常性構成証明書サービスとの通信を有効にする]**まで下にスクロールします。  
3.  **[正常性構成証明書サービスとの通信を有効にする]** を **[はい]**に設定し、 **[OK]**をクリックします。  
4. デバイスの正常性を報告するデバイスのコレクションのターゲットを設定します。

### <a name="how-to-enable-on-premises-health-attestation-service-communication-on-configuration-manager-client-computers"></a>Configuration Manager クライアント コンピューターの内部設置型正常性構成証明書サービスの通信を有効にする方法
次の手順を使用して、インターネットに接続しない、オンプレミスのデバイスのデバイス正常性構成証明書の監視を有効にします。

Configuration Manager 1702 から、インターネット アクセスのないクライアント デバイスをサポートするために、管理ポイントにオンプレミスのデバイス正常性構成証明書のサービス URL を構成できるようになりました。

1. Configuration Manager コンソールで、**[管理]** > **[概要]** > **[サイト構成]** > **[サイト]** の順に移動します。
2. オンプレミスのデバイス正常性構成証明書クライアントをサポートしている管理ポイントを含むプライマリまたはセカンダリ サイトを右クリックして、**[サイト コンポーネントの構成]** > **[管理ポイント]** を選択します。 **[管理ポイント コンポーネントのプロパティ]** ページが開きます。
3. **[詳細オプション]** タブで **[追加]** を選択し、有効なオンプレミスのデバイス正常性構成証明書のサービス URL を指定します。 複数の URL を追加できます。 オンプレミスの URL が複数指定されると、クライアントはそのすべてを受け取り、どれを使用するかをランダムに選択します。
4.  Configuration Manager コンソールで、**[管理]**  >  **[概要]**  >  **[クライアント設定]** を選択します。  **[コンピューター エージェント]** 設定のタブを選択します。  
5.  **[既定の設定]** ダイアログ ボックスで、 **[コンピューター エージェント]** を選択して、 **[オンプレミスの正常性構成証明サービスを使用する]** まで下にスクロールして、**[はい]** を設定します。
6. クライアント エージェントの設定でデバイス正常性構成証明書のレポートが有効に設定されている、デバイスの正常性をレポートするデバイスのコレクションのターゲットを設定します。

デバイス正常性構成証明書サービスの URL を**編集**または**削除**することもできます。

> [!NOTE]
> Configuration Manager 1702 にアップグレードする前にデバイス正常性構成証明書を使用した場合は、クライアント エージェント設定で指定されたオンプレミスの URL がアップグレード中に管理ポイントのプロパティに事前に設定されます。 オンプレミスのクライアントはアップグレードされるまで、クライアント エージェント設定で指定された URL を引き続き使用します。 その後、管理ポイントで指定された URL のいずれかに切り替えます。

## <a name="monitor-device-health-attestation"></a>Windows のデバイス正常性構成証明書

1.  デバイス正常性構成証明書ビューを表示するには、Configuration Manager コンソールで **[監視]** ワークスペースに移動し、 **[セキュリティ]** ノードをクリックしてから **[正常性構成証明書]**をクリックします。  
2.  デバイス正常性構成証明書が表示されます。  

Configuration Manager デバイス正常性構成証明書には、次の情報が表示されます。  

-   **正常性構成証明書のステータス** - 対応、非対応、エラー、および不明な状態のデバイスの共有を表示します。  
-   **正常性構成証明書を報告するデバイス** - 正常性構成証明書のステータスを報告するデバイスの割合を示します。  
-   **クライアントの種類別の非対応のデバイス** - 非対応のモバイル デバイスとコンピューターの共有を表示します。  
-   **最も不足している正常性構成証明書の設定** - 正常性構成証明書の設定のないデバイスの数を設定ごとに表示します。

クライアント デバイス正常性構成証明書のステータスは、Microsoft Intune を備えた Configuration Manager によって管理されるデバイスのコンプライアンス ポリシーに条件付きアクセスの規則を定義するために使用できます。 詳細については、「[System Center Configuration Manager でのデバイス コンプライアンス ポリシーの管理](/sccm/protect/deploy-use/device-compliance-policies)」をご覧ください。  

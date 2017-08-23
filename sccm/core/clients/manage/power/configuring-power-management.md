---
title: "電源管理の構成 | Microsoft Docs"
description: "System Center Configuration Manager で電源管理をセットアップします。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 435c923c-ea30-4dce-8afd-48962ed85502
caps.latest.revision: "5"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: e111ac2545dd9e0b96a50c10246bb75d286a737a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="configuring-power-management-in-system-center-configuration-manager"></a>System Center Configuration Manager での電源管理の構成

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager で電源管理を使用するには、次の構成手順を実行する必要があります。  

## <a name="enable-and-configure-power-management-client-settings"></a>電源管理のクライアント設定の有効化と構成  
 この手順に従って、電源管理に既定のクライアント設定を構成し、階層内のすべてのコンピューターに適用します。 これらの設定を一部のコンピューターのみに適用する場合は、カスタム クライアント デバイス設定を作成して、電源管理を使用するコンピューターを含むコレクションに割り当てます。 カスタムのデバイス設定の作成方法の詳細については、「[System Center Configuration Manager でクライアント設定を構成する方法](../../../../core/clients/deploy/configure-client-settings.md)」を参照してください。  

#### <a name="to-enable-power-management-and-configure-client-settings"></a>電源管理を有効にしてクライアント設定を構成するには  

1.  Configuration Manager コンソールで、[ **管理**] をクリックします。  

2.  [ **管理** ] ワークスペースで [ **クライアント設定**] をクリックします。  

3.  [既定のクライアント設定 ****] をクリックします。  

4.  **[ホーム]** タブの **[プロパティ]** グループで、 **[プロパティ]**をクリックします。  

5.  **既定のクライアント設定** ダイアログ ボックスで、クリックして **電源管理**です。  

6.  次のような電源管理のクライアント設定の値を構成します。  

    -   **[デバイスの電源管理を許可する]** – ドロップダウン リストから [TRUE] を選択して、電源管理を有効にします。 ****  

7.  必要なクライアント設定を構成します。 構成できる電源管理のクライアント設定の一覧については、「[About client settings in System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md)」 (System Center Configuration Manager のクライアント設定について) トピックの「[Power Management](../../../../core/clients/deploy/about-client-settings.md#power-management)」 (電源管理) セクションを参照してください。  

8.  [ **OK** ] をクリックして [ **既定のクライアント設定** ] ダイアログ ボックスを閉じます。  

 クライアント コンピューターは、次にクライアント ポリシーをダウンロードするときに、これらの設定で構成されます。 1 つのクライアントのポリシーの取得を開始する場合は、「 [How to manage clients in System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md)」を参照してください。  

## <a name="exclude-computers-from-power-management"></a>電源管理からのコンピューターの除外  
 コンピューターに電源管理設定が適用されるのを防ぐことができます。 コンピューターが電源管理設定から除外されるコレクションのメンバーである場合、そのコンピューターが電源管理設定を適用する別のコレクションに属していても、電源管理設定は適用されません。  

 次のいずれかの場合は、コンピューターを電源管理から除外できます。  

-   事業の必要性からコンピューターを常時オンにしておく必要がある場合  

-   電源管理設定を適用しないコンピューターで構成される、制御コレクションを作成した場合  

-   一部のコンピューターに、電源管理設定を適用する機能が備わっていない場合  

-   Windows Server を実行しているコンピューターを電源管理から除外する場合  

> [!NOTE]  
>  クライアント設定で [ユーザーがデバイスを電源管理対象から外せるようにする] オプションが構成されていると、ユーザーはソフトウェア センターを使用して、自分のコンピューターを電源管理から除外することができます。 ****  

 電源管理から除外されたコンピューターを見つけるには、[除外されているコンピューター] レポートを実行してください。 **** このレポートの詳細については、「[How to monitor and plan for power management in System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md)」 (System Center Configuration Manager で電源管理を監視して計画する方法) の「[Computers Excluded](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md#BKMK_Excluded)」 (除外されたコンピューター) を参照してください。  

> [!IMPORTANT]  
>  Windows XP または Windows Server 2003 を実行するコンピューターに適用された電源設定は、そのコンピューターを電源管理から除外した場合でも、元の値に戻りません。 Windows のこれより新しいバージョンでは、電源管理からコンピューターを除外すると、すべての電源設定が元の値に戻ります。 個々の電源設定をその元の値に戻すことはできません。  

#### <a name="to-exclude-a-collection-of-computers-from-power-management"></a>コンピューターのコレクションを電源管理から除外するには  

1.  Configuration Manager コンソールで、[ **資産とコンプライアンス**] をクリックします。  

2.  [ **資産とコンプライアンス** ] ワークスペースで [ **デバイス コレクション**] をクリックします。  

3.  **デバイス コレクション** ボックスの一覧で、電源管理から除外するコレクションを選択し、、 **ホーム**  タブで、 **プロパティ** グループで、 **プロパティ**です。  

4.  *[<コレクション名\>* **のプロパティ]** ダイアログ ボックスの **[電源管理]** タブで、**[このコレクションのコンピューターに電源管理設定を適用しない]** を選択します。  

5.  **[OK]** をクリックし、*[<コレクション名\>* **のプロパティ]** ダイアログ ボックスを閉じて設定を保存します。  

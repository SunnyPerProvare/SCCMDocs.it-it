---
title: "クライアントで管理されているデバイスのコンプライアンスを管理するための一般的なタスク - Configuration Manager | Microsoft Docs"
description: "いくつかの一般的なシナリオを使用して、System Center Configuration Manager のコンプライアンス設定について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 2012ab5e55da8d707fd668e0163b42fe7d56c72f
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-system-center-configuration-manager-client"></a>System Center Configuration Manager クライアントでデバイスのコンプライアンスを管理するための一般的なタスク

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックのシナリオでは、一般的なシナリオに従って作業することで、System Center Configuration Manager コンプライアンス設定を使用する方法の概要を説明します。  

 「[System Center Configuration Manager クライアントを使用して管理されているデバイスの構成項目](../../compliance/deploy-use/configuration-items-for-devices-managed-with-the-client.md)」には、コンプライアンス設定に関する知識を既にお持ちの方を対象とした、使用するすべての機能に関する詳細なドキュメントが記載されています。  

 作業を開始する前に、「[コンプライアンス設定を使ってみる](../../compliance/get-started/get-started-with-compliance-settings.md)」をお読みになり、いくつかの基本的なコンプライアンス設定を確認してください。また、[コンプライアンス設定の計画と構成](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)に関するページをお読みになり、必要な前提条件の実装方法をご確認してください。  

## <a name="general-information-for-each-scenario"></a>各シナリオ共通の情報  
 各シナリオでは、特定のタスクを実行する構成項目を作成します。 構成項目の作成ウィザードを開き、次の手順に従います。  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[コンプライアンス設定]** > **[構成項目]** の順にクリックします。  

3.  [ホーム **** ] タブの [作成 **** ] グループで、[構成項目の作成 ****] をクリックします。  

4.  次のように構成項目の作成ウィザードの **[全般]** タブで、構成項目の名前と説明を指定し、このトピックの各シナリオに適した構成項目の種類を選択します。  

     ![構成項目の作成ウィザードの全般ページが表示されます。](/sccm/compliance/plan-design/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenarios-for-windows-10-devices-managed-with-the-configuration-manager-client"></a>Configuration Manager クライアントを使用して管理されている Windows 10 デバイスのシナリオ  

### <a name="scenario-disable-the-use-of-bluetooth-on-windows-10-devices"></a>シナリオ: Windows 10 デバイスで Bluetooth の使用を無効にする  
 このシナリオでは、セキュリティ部門は会社の機密情報を社外に送信する手段としてデバイスの Bluetooth 機能が使用される可能性があると考えています。 最近になってすべての PC を Windows 10 にアップグレードしており、この機会にこれらのデバイスで Bluetooth 機能を無効にすることにしました。  

1.  構成項目の作成ウィザードの **[全般]** ページで、構成項目の種類として **[Windows 10]** を選択し、 **[次へ]**をクリックします。  

2.  ウィザードの **[サポートされているプラットフォーム]** ページで、すべての Windows 10 プラットフォームを選択します。  

3.  **[デバイス設定]** ページで、 **[デバイス]**を選択し、 **[次へ]**をクリックします。  

4.  **[デバイス]** ページで、 **[Bluetooth]** の値として **[禁止]**を選択します。  

5.  **[対応していない設定を修復する]** を選択して、変更がすべての Windows 10 デバイスに確実に適用されるようにします。  

6.  ウィザードを完了して構成項目を作成します。  

 これで、「[System Center Configuration Manager での構成基準の作成と展開に関する一般的なタスク](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)」トピックの情報を使用して、作成した構成をデバイスに簡単に展開できるようになります。  

## <a name="scenarios-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>Configuration Manager クライアントを使用して管理されている Windows デスクトップおよびサーバー コンピューターを対象としたシナリオ  
 Configuration Manager クライアントを実行している Mac コンピューターでは、コンプライアンスを評価するためのオプションが 2 つあります。  

-   Mac OS X の設定 (plist) ファイルを評価します。  

-   カスタム スクリプトを使用し、そのスクリプトから返される結果を評価します。  

 詳細については、「[System Center Configuration Manager クライアントを使用して管理されている Mac OS X デバイスの構成項目を作成する方法](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md)」を参照してください。  

### <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>シナリオ: Windows デスクトップ コンピューターで正しくないレジストリ値を修復する  
 このシナリオでは、Windows 8.1 を実行している管理対象の一部のコンピューターで、重要な基幹業務アプリが正しく実行されていません。 調査の結果、その原因は一部のコンピューターで **HKEY_LOCAL_MACHINE\SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1** というレジストリ キーの値が **0** に設定されているためと判明します。 基幹業務アプリを正常に実行するには、この値を **1**に設定する必要があります。  

 この手順では、レジストリ キーの値を監視し、正しくない値が見つかった場合には自動的に修復する構成項目を作成します。  

1.  構成項目の作成ウィザードの **[全般]** ページで、構成項目の種類として **[Windows デスクトップおよびサーバー (カスタム)]** を選択し、 **[次へ]**をクリックします。  

2.  ウィザードの **[サポートされているプラットフォーム]** ページで、 **[Windows 8.1]** を選択します (これで、構成項目は対象となるコンピューターにのみ適用されます)。  

3.  **[設定]** ページで、 **[新規]** をクリックして新しい設定を作成します。  

4.  **[設定の作成]** ダイアログ ボックスの **[全般]** タブで、次のように構成します。  

    -   **[名前]** > **[設定例]**  

    -   **[設定の種類]** > **[レジストリ値]**  

    -   **[データ型]** > **[整数]** (値に数値のみが含まれているため)  

    -   **[ハイブ]** > **HKEY_LOCAL_MACHINE**  

    -   **[キー]** > **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

    -   **[値]** > **1** (必須の値)  

5.  **[設定の作成]** ダイアログ ボックスの **[コンプライアンス規則]** タブで、 **[新規]**をクリックし、 **[規則の作成]** ダイアログ ボックスで次のように構成します。  

    -   **[名前]** > **[規則の例]**  

    -   **[選択した設定]** - 選択した設定が **[設定例]**であることを確認します。  

    -   **[規則の種類]** > **[値]**  

    -   **[この設定は次の規則に対応する必要があります]** - 設定名が正しいことを確認して、設定値が **[1]**に等しくなければならないことを指定するオプションを構成します。  

    -   **[サポートされている場合は対応していない規則を修復する]** – レジストリ キー値が正しくない場合に Configuration Manager が正しい値にリセットするようにするには、このボックスをオンにします。  

6.  ウィザードを完了して構成項目を作成します。  

 これで、「[構成基準の作成と展開に関する一般的なタスク](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md)」トピックの情報を使用して、作成した構成をデバイスに簡単に展開できるようになります。  

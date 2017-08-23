---
title: "Configuration Manager を利用し、Windows デバイスを別のバージョンにアップグレードする | Microsoft Docs"
description: "Configuration Manager を利用し、Windows 10 Desktop、Windows 10 Mobile、Windows 10 Holographic を実行するデバイスを自動的に別のエディションにアップグレードします。"
ms.custom: na
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b0c9db74-841e-46eb-8924-957cde968bf7
caps.latest.revision: "8"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: cd8c644d07dab0010dc211df8ce4f2dc6e1fa7ae
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="upgrade-windows-devices-with-the-edition-upgrade-policy-in-system-center-configuration-manager"></a>System Center Configuration Manager でエディションのアップグレード ポリシーを使用して、Windows デバイスをアップグレードする

*適用対象: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager **エディションのアップグレード ポリシー**を使用して、次に挙げる Windows 10 のバージョンのいずれかを実行するデバイスを自動的に別のエディションにアップグレードできます。

- Windows 10 Desktop
- Windows 10 Mobile
<!-- - Windows 10 Holographic -->

次のアップグレード パスがサポートされます。

- Windows 10 Pro から Windows 10 Enterprise
- Windows 10 Home から Windows 10 Education
- Windows 10 Mobile から Windows 10 Mobile Enterprise
<!-- - From Windows 10 Holographic Pro to Windows 10 Holographic Enterprise -->

デバイスは Microsoft Intune に登録するか、Configuration Manager クライアント ソフトウェアを実行する必要があります。 現在、このポリシーは、オンプレミス MDM で管理されている PC と互換性はありません。

## <a name="before-you-start"></a>アップグレードを開始する前に  
 デバイスを最新バージョンにアップグレードし始める前に、次のいずれかを用意する必要があります。  

-   ポリシーで対象とするすべてのデバイスに新しいバージョンの Windows をインストールするための有効なプロダクト キー (デスクトップ オペレーティング システムの場合)  

-   ポリシーで対象とするすべてのデバイスに新しいバージョンの Windows をインストールするためのライセンス情報を含む、Microsoft からのライセンス ファイル (Windows 10 Mobile<!-- and Windows 10 Holographic-->の場合)。

- この種類のポリシーを作成して展開するには、Configuration Manager の**完全な権限を持つ管理者**のセキュリティ ロールが割り当てられている必要があります。

## <a name="configure-the-edition-upgrade-policy"></a>エディションのアップグレード ポリシーを構成する  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[コンプライアンス設定]** > **[Windows 10 エディションのアップグレード]** の順にクリックします。  

3.  **[ホーム]** タブの **[作成]** グループで、 **[エディション アップグレード ポリシーの作成]**をクリックします。  

4.  **[ポリシーを作成する]**をクリックします。  

5.  **エディション アップグレード ポリシーの作成ウィザード** の **[全般]**ページで、次の情報を指定します。  

    -   **名前** - エディションのアップグレード ポリシーの名前を入力します。  

    -   **説明** (省略可能) - 必要に応じて、Intune コンソールでの識別に役立つポリシーの説明を入力します。  

    -   **デバイスのアップグレード先の SKU** - 対象のデバイスのアップグレード先となる Windows 10 Desktop、<!-- Windows 10 Holographic,-->、または Windows 10 Mobile のバージョンをドロップダウン リストから選びます。  

    -   **ライセンス情報** - 次のいずれかを選びます。  

        -   **プロダクト キー** - Windows 10 Desktop オペレーティング システムを実行する対象デバイスをアップグレードするために使用する、Windows 10 の有効なプロダクト キーを入力します。  

            > [!NOTE]  
            >  プロダクト キーを含むポリシーを作成した後でプロダクト キーを編集することはできません。 これは、セキュリティ上の理由からキーが隠されるためです。 プロダクト キーを変更するには、キー全体を再入力する必要があります。  

        -   **ライセンス ファイル** - **[参照]** をクリックし、<!--Windows 10 Holographic and -->Windows 10 Mobile のオペレーティング システムを実行する対象デバイスをアップグレードするために使用する XML 形式の正しいライセンス ファイルを選びます。  

6.  ウィザードを完了します。  

新しいポリシーは、 **[資産とコンプライアンス]** ワークスペースの **[Windows 10 エディション アップグレード]** ノードに表示されます。  

## <a name="deploy-the-edition-upgrade-policy"></a>エディションのアップグレード ポリシーを展開する  

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** > **[コンプライアンス設定]** > **[Windows 10 エディションのアップグレード]** の順にクリックします。  

3.  展開する Windows 10 のエディションのアップグレード ポリシーを選び、 **[ホーム]** タブの **[展開]** グループで **[展開]**をクリックします。  

4.  **[Windows 10 エディション アップグレードの展開]** ダイアログ ボックスで、ポリシーを展開するコレクションと、ポリシーを評価するスケジュールを選択し、**[OK]**をクリックします。 Configuration Manager クライアントで管理されている PC の場合は、デバイス コレクションにポリシーを展開する必要があります。 Intune で登録されている PC の場合は、ユーザーまたはデバイス コレクションにポリシーを展開できます。 



## <a name="next-steps"></a>次のステップ

**[監視]** ワークスペースの **[展開]** ノードから、作成したばかりの展開を監視すると、展開が次のように失敗したことを示すエラーが表示されることがあります。
- **このデバイスには該当しません**
- **データ型を変換できませんでした**

これらのエラーは、展開が失敗したことを意味しているわけではありません。 対象の PC で、アップグレードが正常に実行されたことを確認してください。

ポリシーが対象の Windows PC に到達し、評価されると、アップグレードを適用するために PC が 2 時間以内に再起動します。 ポリシーを展開するすべてのユーザーに通知するか、ポリシーの実行をユーザーの業務時間外にスケジュール設定します。

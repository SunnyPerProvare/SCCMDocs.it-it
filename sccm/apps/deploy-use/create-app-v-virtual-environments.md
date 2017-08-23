---
title: "App-V 仮想環境を作成する | Microsoft Docs"
description: "Microsoft Application Virtualization を使用して仮想環境を作成し、アプリが互いにデータを共有できるようにします。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b6b86078-fcc4-46cf-87d6-4b52b914b712
caps.latest.revision: "6"
caps.handback.revision: "0"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 377ed9732fb16b062f53e78504aea394acdb7462
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="create-app-v-virtual-environments-in-system-center-configuration-manager"></a>System Center Configuration Manager で App-V 仮想環境を作成する

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager (Configuration Manager) の Microsoft Application Virtualization (App-V) 仮想環境で、展開した仮想アプリケーションはクライアント Windows PC と同じファイル システムとレジストリを共有できます。 標準の仮想アプリケーションとは異なり、これらのアプリケーションは相互にデータを共有できます。 アプリケーションがインストールされた場合、または、インストールされたアプリケーションをクライアントが次回評価するときに、クライアント PC に仮想環境が作成または変更されます。 複数のアプリケーションがファイル システムまたはレジストリ値を変更しようとしたときに、順序が先のアプリケーションが優先されるように、アプリケーションを並べることができます。  

> [!IMPORTANT]  
>  マルウェアなどからのセキュリティ保護を行うために、App-V 仮想環境に依存しないようにしてください。  

 App-V 仮想環境を Configuration Manager に作成するには、次の手順を使用します。  

## <a name="create-an-app-v-virtual-environment"></a>App-V 仮想環境を作成する  

1.  Configuration Manager コンソールで、**[ソフトウェア ライブラリ]** > **[アプリケーション管理]** > **[App-V 仮想環境]** の順に選択します。  

3.  **[ホーム]** タブの **[作成]** グループで、**[仮想環境の作成]** を選択します。  

4.  **[仮想環境の作成]** ダイアログ ボックスで、次の情報を入力します。  

    -   **名前**。  仮想環境の一意の名前 (128 文字以内) を入力します。  

    -   **説明**。 (省略可能) 仮想環境の説明を入力します。  

5.  新しい展開の種類を仮想環境に追加する場合は、**[追加]** を選択します。 展開の種類を少なくとも 1 つ追加する必要があります。  

6.  **[アプリケーションの追加]** ダイアログ ボックスで、**[グループ名]** (128 文字以内) を指定します。 仮想環境に追加するアプリケーションのグループを示す際にこの名前を使用します。  

7.  **[追加]** を選択し、グループに追加する App-V 5 アプリケーションと展開の種類を選択して、**[OK]** を選択します。  

8.  **[アプリケーションの追加]** ダイアログ ボックスで、**[順位を上げる]** または **[順位を下げる]** を選択して、同じ仮想環境内で複数のアプリケーションがファイル システムまたはレジストリ設定を変更しようとしたときに、優先するアプリケーションを設定します。  

9. **[仮想環境の作成]** ダイアログ ボックスに戻る場合は、**[OK]** を選択します。  

10. グループの追加を完了したら、**[OK]** を選択して仮想環境を作成します。 新しい仮想環境が Configuration Manager コンソールの [**APP-V 仮想環境**] ノードに表示されます。 [App-V 仮想環境のステータス] レポートを使用して、仮想環境の状態を監視できます。  

    > [!NOTE]  
    >  アプリケーションがインストールされたとき、またはインストールされたアプリケーションをクライアントが次回評価するときに、クライアント PC で仮想環境が追加または変更されます。  

---
title: "Skype for Business Online のアクセスの管理 | Microsoft Docs"
description: "条件付きアクセス ポリシーを使用して、Skype for Business Online へのアクセスを管理する方法について説明します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 71c44250-626e-482c-8794-434c6aeb2fb1
caps.latest.revision: "6"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: cacb22a85e74a7d9cae75ad907d0206487cd4dc7
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="manage-skype-for-business-online-access"></a>Skype for Business Online のアクセスの管理

*適用対象: System Center Configuration Manager (Current Branch)*


**Skype for Business Online** の条件付きアクセス ポリシーを使用して、Skype for Business Online へのアクセスを指定条件に基づいて管理します。  


 対象ユーザーが各自のデバイスで Skype for Business Online を使用しようとすると、次の評価が行われます。![ConditionalAccess&#95;SFBFlow](media/ConditionalAccess_SFBFlow.png)  

## <a name="prerequisites"></a>必要条件  

-   Skype for Business Online の先進認証を有効にします。 この [接続フォーム](https://connect.microsoft.com/office/Survey/NominationSurvey.aspx?SurveyID=17299&ProgramID=8715) に必要事項を記入して、最新の認証プログラムに登録します。  

-   すべてのエンドユーザーが Skype for Business Online を使用している必要があります。 Skype for Business Online と Skype for Business オンプレミスの両方が含まれている展開の場合は、条件付きアクセス ポリシーはエンドユーザーに適用されません。  

-   Skype for Business Online へのアクセスを必要とするデバイスは次の条件を満たしている必要があります。  

    -   Android または iOS デバイスである。  

    -   Intune に登録されている。  

    -   展開されているすべての Intune コンプライアンス ポリシーに準拠している。  

 デバイスの状態は、Azure Active Directory に格納され、指定した条件に基づいてアクセスが許可されたりブロックされたりします。  
条件が満たされない場合、ユーザーにはログイン時に以下のうちのいずれかのメッセージが表示されます。  

-   デバイスが Intune または Azure Active Directory に登録されていない場合は、会社ポータルのアプリをインストールおよび登録する手順を含むメッセージが表示されます。  

-   デバイスが準拠していない場合は、Intune の会社ポータル Web サイトまたは会社ポータルのアプリにユーザーを誘導するメッセージが表示されます。このポータルで、ユーザーは問題とその解決方法に関する情報を確認できます。  

## <a name="configure-conditional-access-for-skype-for-business-online"></a>Skype for Business Online の条件付きアクセスの構成  

### <a name="step-1-configure-active-directory-security-groups"></a>手順 1. Active Directory セキュリティ グループを構成する  
 開始する前に、条件付きアクセス ポリシーの Azure Active Directory セキュリティ グループを構成します。 Office 365 管理センターでこれらのグループを構成できます。 これらのグループには、ポリシーの対象となるユーザーや、ポリシーから除外されるユーザーが含まれます。 ユーザーがポリシーの対象となる場合、ユーザーに使用される各デバイスがリソースにアクセスするには、ポリシーを遵守している必要があります。  

 Skype for Business ポリシーに適用する 2 つのグループの種類を指定できます。  

-   対象グループ – ポリシーを適用するユーザーのグループが含まれます。  

-   例外グループ – ポリシーから除外されるユーザーのグループが含まれます (省略可能)。  
    ユーザーが両方のグループに含まれている場合は、ポリシーから除外されます。  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>手順 2:コンプライアンス ポリシーを構成し展開する  
 コンプライアンス ポリシーを作成して、Skype for Business Online ポリシーの対象となるすべてのデバイスに展開します。  

 コンプライアンス ポリシーを構成する方法の詳細については、「[System Center Configuration Manager でのデバイス コンプライアンス ポリシーの管理](../../protect/deploy-use/device-compliance-policies.md)」を参照してください。  

> [!NOTE]  
>  コンプライアンス ポリシーを展開していない場合に Skype for Business Online ポリシーを有効にすると、Intune に登録されているすべての対象デバイスにアクセスが許可されます。  

 準備ができたら、手順 3 に進みます。  

### <a name="step-3-configure-the-skype-for-business-online-policy"></a>手順 3: Skype for Business Online ポリシーを構成する  
 次に、管理対象の準拠デバイスのみが Skype for Business Online にアクセスできるようにポリシーを構成します。 このポリシーは、Azure Active Directory に格納されます。  

1.  [Microsoft Intune 管理コンソール](https://manage.microsoft.com)で、 **[ポリシー]** > **[条件付きアクセス]** > **Skype for Business Online [ポリシー]**」を参照してください。  

     ![ConditionalAccess&#95;SFBPolicy](media/ConditionalAccess_SFBPolicy.png)  

2.  **[条件付きアクセス ポリシーを有効にする]** を選択します。  

3.  **[アプリケーション アクセス]**で、条件付きアクセス ポリシーの適用対象を次の中から選択できます。  

    -   iOS  

    -   Android  

4.  **[対象グループ]**で、 **[変更]** をクリックして、ポリシーを適用する Azure Active Directory セキュリティ グループを選択します。 すべてのユーザーを対象にすることも、選んだユーザー グループのみを対象にすることもできます。  

5.  **[例外グループ]**で、必要に応じて **[変更]** をクリックして、このポリシーから除外する Azure Active Directory セキュリティ グループを選択します。  

6.  終了したら、 **[保存]**をクリックします。  

 これで Skype for Business Online の条件付きアクセスの構成が完了します。 条件付きアクセス ポリシーを展開する必要はありません。直ちに有効になります。  

## <a name="monitor-the-compliance-and-conditional-access-policies"></a>コンプライアンスと条件付きアクセス ポリシーを監視する  
 [グループ] ワークスペースで、デバイスの条件付きアクセスの状態を表示できます。  

 モバイル デバイス グループを選択し、 **[デバイス]** タブで、次の **[フィルター]**のいずれかを選択します。  

-   **AAD に登録されていないデバイス** – これらのデバイスは Skype for Business Online からブロックされます。  

-   **準拠していないデバイス** – これらのデバイスは Skype for Business Online からブロックされます。  

-   **AAD に登録され、準拠しているデバイス** – これらのデバイスは、Skype for Business Online にアクセスできます。  

### <a name="see-also"></a>関連項目  

 [System Center Configuration Manager でのデバイス コンプライアンス ポリシーの管理](../../protect/deploy-use/device-compliance-policies.md)

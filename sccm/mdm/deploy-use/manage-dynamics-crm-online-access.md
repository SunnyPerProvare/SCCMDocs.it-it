---
title: "Dynamics CRM Online アクセスの管理 | Microsoft Docs"
description: "Microsoft Intune 条件付きアクセスを使用して iOS および Android デバイスから Microsoft Dynamics CRM Online へのアクセスを制御する方法について説明します。"
ms.custom: na
ms.date: 03/05/2017
ms.reviewer: na
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bfc4c51-b25c-4c70-b81e-8a3b6ddf02c8
caps.latest.revision: "5"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: bd00f12ae3bc14a34d24c22c3d5277d275d51e85
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="manage-dynamics-crm-online-access-in-system-center-configuration-manager"></a>System Center Configuration Manager での Dynamics CRM Online アクセスの管理

*適用対象: System Center Configuration Manager (Current Branch)*

Microsoft Intune の条件付きアクセスを使用して、iOS および Android デバイスから Microsoft Dynamics CRM Online へのアクセスを制御できます。  Intune の条件付きアクセスには、2 つのコンポーネントがあります。
* [デバイス コンプライアンス ポリシー](../../protect/deploy-use/device-compliance-policies.md): 準拠と見なされるためにデバイスが準拠する必要があるポリシーです。
* [条件付きアクセス ポリシー](../../protect/deploy-use/manage-access-to-services.md): サービスにアクセスするためにデバイスが満たす必要のある条件を指定するポリシーです。

条件付きアクセスのしくみの詳細については、「[Manage access to services](../../protect/deploy-use/manage-access-to-services.md)」 (サービスへのアクセスの管理) を参照してください。


対象ユーザーが各自のデバイスで Dynamics CRM を使用しようとすると、次の評価が行われます。

![デバイスからサービスへのアクセスが許可されるか、またはブロックされるかを判断するために使用する意思決定ポイントを示す図](media/mdm-ca-dynamics-crm-flow-diagram.png)

Dynamics CRM Online へのアクセスを必要とするデバイスは、次の条件を満たしている必要があります。
* **Android** または **iOS** デバイスである。
* Microsoft Intune に**登録**されている。
* 展開されているすべての Intune コンプライアンス ポリシーに**準拠**している。

デバイスの状態は、Azure Active Directory に格納され、指定した条件に基づいてアクセスが許可されたりブロックされたりします。

条件が満たされない場合、ユーザーにはログイン時に以下のうちのいずれかのメッセージが表示されます。
* デバイスが Microsoft Intune または Azure Active Directory に登録されていない場合は、会社ポータルのアプリをインストールおよび登録する手順を含むメッセージが表示されます。
* デバイスが準拠していない場合は、Microsoft Intune の会社ポータル Web サイトまたは会社ポータルのアプリにユーザーを誘導するメッセージが表示されます。このポータルで、ユーザーは問題とその解決方法に関する情報を確認できます。

## <a name="configure-conditional-access-for-dynamics-crm-online"></a>Dynamics CRM Online 用の条件付きアクセスの構成  
### <a name="step-1-configure-active-directory-security-groups"></a>手順 1. Active Directory セキュリティ グループを構成する

開始する前に、条件付きアクセス ポリシーの Azure Active Directory セキュリティ グループを構成します。 **Office 365 管理センター**でこれらのグループを構成できます。 これらのグループは、ユーザーをポリシーの対象にするか、または対象外にするために使用します。 ユーザーがポリシーの対象となる場合、ユーザーに使用される各デバイスがリソースにアクセスするには、ポリシーを遵守している必要があります。

Dynamics CRM ポリシーに適用する 2 つのグループの種類を指定できます。
* **対象グループ** – ポリシーを適用するユーザーのグループを含みます。
* **例外グループ** – ポリシーから除外されるユーザーのグループを含みます。

ユーザーが両方のグループに含まれている場合は、ポリシーから除外されます。

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>手順 2:コンプライアンス ポリシーを構成し展開する
影響を受けるすべてのデバイスに対してコンプライアンス ポリシーを[作成および展開](../../protect/deploy-use/device-compliance-policies.md)します。 これらは、対象グループ内のユーザーが使用するすべてのデバイスです。

> [!NOTE]
> コンプライアンス ポリシーは Microsoft Intune グループに展開されますが、条件付きアクセス ポリシーは、Azure Active Directory セキュリティ グループを対象とします。

> [!IMPORTANT]
> コンプライアンス ポリシーを展開していない場合、デバイスは準拠として扱われます。

準備ができたら、手順 3 に進みます。
### <a name="step-3-configure-the-dynamics-crm-policy"></a>手順 3: Dynamics CRM ポリシーを構成する
次に、管理デバイスおよび準拠デバイスのみが Dynamics CRM にアクセスできるように要求するポリシーを構成します。 このポリシーは、Azure Active Directory に格納されます。

1.  Microsoft Intune 管理コンソールで、**[ポリシー] > [条件付きアクセス] > [Dynamics CRM Online ポリシー]** をクリックします。

     ![Dynamics CRM Online の条件付きアクセス ポリシー ページのスクリーン ショット](media/mdm-ca-dynamics-crm-policy-configuration.png)

2.  **[条件付きアクセス ポリシーを有効にする]**を選択します。
3.  **[アプリケーション アクセス]**で、条件付きアクセス ポリシーの適用対象を次の中から選択できます。
  * **iOS**
  * **Outlook Web Access (OWA)**
4.  **[対象グループ]**で、 **[変更]** をクリックして、ポリシーを適用する Azure Active Directory セキュリティ グループを選択します。 すべてのユーザーを対象にすることも、選んだユーザー グループのみを対象にすることもできます。
5.  **[例外グループ]**で、必要に応じて **[変更]** をクリックして、このポリシーから除外する Azure Active Directory セキュリティ グループを選択します。
6.  終了したら、 **[保存]**をクリックします。

これで Dynamics CRM の条件付きアクセスの構成が完了します。 条件付きアクセス ポリシーを展開する必要はありません。直ちに有効になります。
##  <a name="monitor-the-compliance-and-conditional-access-policies"></a>コンプライアンスと条件付きアクセス ポリシーを監視する

**[グループ]** ワークスペースで、デバイスの条件付きアクセスの状態を表示できます。

モバイル デバイス グループを選択し、 **[デバイス]** タブで、次の **[フィルター]**のいずれかを選択します。
* **AAD に登録されていないデバイス** – これらのデバイスは Dynamics CRM からブロックされます。
* **準拠していないデバイス** – これらのデバイスは Dynamics CRM からブロックされます。
* **AAD に登録され、準拠しているデバイス** – これらのデバイスは、Dynamics CRM にアクセスできます。

###  <a name="see-also"></a>関連項目
[電子メールへのアクセスの管理](../../protect/deploy-use/manage-email-access.md)

[SharePoint Online へのアクセスの管理](../../protect/deploy-use/manage-sharepoint-online-access.md)

[Skype for Business Online へのアクセスの管理](../../protect/deploy-use/manage-skype-for-business-online-access.md)

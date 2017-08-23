---
title: "Windows Hello for Business の設定 | Microsoft Docs"
description: "System Center Configuration Manager に Windows Hello for Business を統合する方法について説明します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0593c07-5dd7-4d23-a0d8-d30165f49ef7
caps.latest.revision: "17"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: a97b3d97eb302e4133b0a79a8c7e27004872c8b1
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager-hybrid"></a>System Center Configuration Manager における Windows Hello for Business の設定 (ハイブリッド)

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager を、Windows 10 デバイスの代替サインイン方法である Windows Hello for Business (旧称: Microsoft Passport for Windows) と統合することができます。 Hello for Business では、パスワード、スマート カード、または仮想スマート カードの代わりに Active Directory または Azure Active Directory アカウントを使用します。  

Hello for Business を使用すると、パスワードの代わりに **ユーザー ジェスチャ** を使用してログインできます。 ユーザー ジェスチャには、単純な暗証番号 (PIN)、生体認証、または指紋リーダーなどの外部のデバイスがあります。  

 Configuration Manager と Windows Hello for Business を統合するには、次の 2 つの方法があります。  

-   Configuration Manager を使用して、ユーザーがサインインに使用できるジェスチャと使用できないジェスチャを制御できます。  

-   Windows Hello for Business のキー格納プロバイダー (KSP) に認証証明書を格納できます。 詳細については、「[Certificate profiles](create-pfx-certificate-profiles.md)」 (証明書プロファイル) をご覧ください。  

- ドメインに参加しており構成マネージャー クライアントを実行している Windows 10 デバイスに Windows Hello for Business ポリシーを展開できます。 この構成については、「[ドメインに参加している Windows 10 デバイスで Windows Hello for Business を構成する](../../protect/deploy-use/windows-hello-for-business-settings.md#configure-windows-hello-for-business-on-domain-joined-windows-10-devices)」で説明されています。 Configuration Manager と Intune (ハイブリッド) を使用している場合、これらの設定は、Windows 10 デバイスと Windows 10 Mobile デバイスで構成できますが、ドメインに参加しており構成マネージャー クライアントを実行しているデバイスでは構成できません。   

Windows Hello for Business 設定の構成に関する一般情報は、「[System Center Configuration Manager における Windows Hello for Business の設定](../../protect/deploy-use/windows-hello-for-business-settings.md)」をご覧ください。

## <a name="configure-windows-hello-for-business-settings-hybrid"></a>Windows Hello for Business 設定を構成する (ハイブリッド)  

1.  Configuration Manager コンソールで、**[管理]** > **[Cloud Services]** > **[Microsoft Intune サブスクリプション]** の順にクリックします。  

3.  リストから、Microsoft Intune サブスクリプションを選び、 **[ホーム]** タブの **[サブスクリプション]** グループで、 **[プラットフォームの構成]** > **[Windows (MDM)]**をクリックします。  

4.  **[Microsoft Intune サブスクリプションのプロパティ]** ダイアログ ボックスの **[Windows Hello for Business]** タブで、登録されているすべての Windows 10 および Windows 10 Mobile デバイスに影響する次の値から選びます。  

    -   **[登録デバイスで Windows Hello for Business を無効にする]** または **[登録デバイスで Windows Hello for Business を有効にする]** - 登録されているすべての Windows 10 および Windows 10 Mobile デバイスで Windows Hello for Business の使用を有効または無効にします。  

    -   **トラステッド プラットフォーム モジュール (TPM) の使用** - トラステッド プラットフォーム モジュール (TPM) チップでは、追加のデータのセキュリティ層を提供します。 次のいずれかの値を選択します。  

        -   **必須** (既定) - アクセス可能な TPM を装備したデバイスのみが Windows Hello for Business をプロビジョニングできます。  

        -   **優先** -デバイスは最初に TPM を使用しようとします。 これが使用できない場合、ソフトウェアの暗号化を使用できます。  

    -   **PIN の最小長** - Windows Hello for Business の PIN に必要な文字の最小数を指定します。 少なくとも 4 文字を使用する必要があります (既定値は 6 文字)。  

    -   **PIN の最大長** - Windows Hello for Business の PIN に使用できる文字の最大数を指定します。 127 文字まで使用できます。  

    -   **PIN に小文字が必要** - Windows Hello for Business の PIN に小文字を使用する必要があるかどうかを指定します。 次の中から選択します。  

        -   **許可** -ユーザーは PIN に小文字を使用することができます。  

        -   **必須** -ユーザーは PIN に小文字を 1 文字以上含める必要があります。  

        -   **使用不可** (既定) -ユーザーは PIN に小文字を使用することができません。  

    -   **PIN に大文字が必要** - Windows Hello for Business の PIN に大文字を使用する必要があるかどうかを指定します。 次の中から選択します。  

        -   **許可** -ユーザーは PIN に大文字を使用することができます。  

        -   **必須** -ユーザーは PIN に大文字を 1 文字以上含める必要があります。  

        -   **使用不可** (既定) -ユーザーは PIN に大文字を使用することができません。  

    -   **特殊文字が必要** - PIN の特殊文字の使用を指定します。 次の中から選択します。  

        -   **許可** -ユーザーは PIN に特殊文字を使用することができます。  

        -   **必須** -ユーザーは PIN に特殊文字を 1 文字以上含める必要があります。  

        -   **使用不可** (既定) -ユーザーは PIN に特殊文字を使用することができません (これは、設定を構成していない場合の動作でもあります)。  

         特殊文字には次のものが含まれます。**! " # $ % & ' ( ) \* + , - . / : ; < = > ? @ [ \ ] ^ _ ` { &#124; } ~**  

    -   **PIN の有効期限が必要 (日)** - PIN の変更が必要になるまでの日数を指定します。 既定は 41 日です。  

    -   **前の PIN の再利用を防止** - この設定を使用すると、以前に使用した PIN の再利用を制限できます。 既定では過去 5 回の PIN を再利用することはできません。  

    -   **生体認証のジェスチャを有効にする** - Windows Hello for Business の PIN の代わりとして、顔認識や指紋などの生体認証を有効にします。 ユーザーは、生体認証に失敗した場合のために、Work の PIN も設定する必要があります。  

         **[有効]**に設定されている場合は、Windows Hello for Business で生体認証が利用できます。  **[無効]**に設定されている場合は、Windows Hello for Business で生体認証が利用できません (すべてのアカウントの種類が対象)。  

    -   **拡張スプーフィング対策が使用可能な場合は使用する** - デバイスでサポートされている場合に拡張スプーフィング対策を使用するかどうかを構成します。  

         **[有効]**に設定されている場合、Windows のすべてのユーザーは、サポートされている場合に顔の特徴のスプーフィング対策を使用する必要があります。  

    -   **リモートの Passport を使用する** - このオプションが **[有効]**に設定されている場合、ユーザーはデスクトップ コンピューターの認証にポータブル コンパニオン デバイスとして機能するリモートの Hello for Business を使用することができます。 デスクトップ コンピューターは Azure Active Directory に参加している必要があり、コンパニオン デバイスは、Windows Hello for Business の PIN を使用して設定されている必要があります。  

5.  操作が完了したら、 **[OK]**をクリックします。  

### <a name="see-also"></a>関連項目  
 [System Center Configuration Manager でのデータとサイト インフラストラクチャの保護](../../protect/understand/protect-data-and-site-infrastructure.md)

 [Windows Hello for Business を使用した本人確認の管理](https://technet.microsoft.com/itpro/windows/keep-secure/manage-identity-verification-using-microsoft-passport)  

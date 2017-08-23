---
title: "条件付きアクセス | Microsoft Docs"
description: "System Center Configuration Manager で条件付きアクセスを使用して、電子メールおよびその他のサービスをセキュリティで保護する方法について説明します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b04727b-d563-422f-8d59-4dd66215d0b3
caps.latest.revision: "26"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: d6933a331bb229f7e378e8f0bfa511f6b0553ae9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="manage-access-to-services-in-system-center-configuration-manager"></a>System Center Configuration Manager でサービスへのアクセスを管理する

*適用対象: System Center Configuration Manager (Current Branch)*


## <a name="conditional-access-in-system-center-configuration-manager"></a>System Center Configuration Manager での条件付きアクセス
**条件付きアクセス**を使用すると、Microsoft Intune に登録されているデバイスで、指定する条件に基づいて電子メールやその他のサービスをセキュリティで保護できます。  

 **System Center Configuration Manager で管理され**、コンプライアンスが評価される PC の条件付きアクセスに関する詳細は、「[System Center Configuration Manager で管理されている PC の O365 サービスへのアクセスを管理する](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)」を参照してください。  


 条件付きアクセスの一般的なフローは、次のようになります。  

 ![ConditionalAccess4](media/ConditionalAccess4.png)  

 条件付きアクセスを使用すると、次のサービスへのアクセスを管理できます。  

-   Microsoft Exchange On-premises  

-   Microsoft Exchange Online  

-   Exchange Online Dedicated  

-   SharePoint Online  

-   Skype for Business Online

-   Dynamics CRM Online

 条件付きアクセスを実装するには、Configuration Manager で次の 2 種類のポリシーを構成します。  

-   **コンプライアンス ポリシー** 。ユーザー コレクションに展開できるオプションのポリシーで、次のような設定を評価します。  

    -   パスコード  

    -   暗号化  

    -   デバイスが脱獄またはルート化されているかどうか  

    -   Configuration Manager または Intune ポリシーでデバイス上の電子メールを管理するかどうか  

     **コンプライアンス ポリシーがデバイスに展開されていない場合、適用可能なすべての条件付きアクセス ポリシーでデバイスが準拠デバイスとして扱われます**。  

-   **条件付きアクセス ポリシー**。このポリシーは特定のサービス用に構成され、どの Azure Active Directory セキュリティ ユーザー グループまたは Configuration Manager ユーザー コレクションを対象とするか、などを定義します。  

     Configuration Manager コンソールから、オンプレミスの Exchange 条件付きアクセス ポリシーを構成します。 ただし、Exchange Online または SharePoint Online のポリシーを構成する場合は、そのポリシーを構成するための Intune 管理コンソールが開きます。  

     その他の Intune または Configuration Manager ポリシーとは異なり、条件付きアクセス ポリシーは展開しません。 その代わり、このポリシーを 1 回構成すると、すべての対象ユーザーに適用されます。  

 構成した条件をデバイスが満たしていない場合、デバイスの登録と、デバイスが準拠デバイスとなることを妨げている問題の修正を行うプロセスがユーザーに案内されます。  

条件付きアクセスの使用を開始する**前に**、次の該当する**要件**を満たしていることを確認してください。  

## <a name="requirements-for-exchange-online-using-the-shared-multi-tenant-environment"></a>Exchange Online (共有マルチテナント環境を使用) の要件
Exchange Online への条件付きのアクセスでは、次を実行するデバイスがサポートされます。
-   Windows 8.1 以降 (Intune に登録されている場合)
-   Windows 7.0 または Windows 8.1 (ドメインに参加している場合)
-   Windows Phone 8.1 以降
-   iOS 7.1 以降
-   Android 4.0 以降、Samsung KNOX Standard 4.0 以降

 **補足**:
-   デバイスをワークプレース参加させる必要があります。ワークプレース参加させると、デバイスは Azure Active Directory Device Registration Service (AAD DRS) に登録されます。<br />     
- ドメインに参加した PC は、グループ ポリシーまたは MSI によって自動的に Azure Active Directory に登録されるはずです。

  このトピックの「 **PC の条件付きアクセス** 」セクションに、PC の条件付きアクセスを有効にするためのすべての要件が説明されています。<br />     
  AAD DRS は、Intune や Office 365 のお客様に対して自動的にアクティブ化されます。 ADFS Device Registration Service をデプロイ済みのお客様には、オンプレミスの Active Directory で登録されたデバイスは表示されません。
-   Exchange Online を含む Office 365 サブスクリプション (E3 など) を使用する必要があります。ユーザーには Exchange Online のライセンスが必要です。
-   オプションの **Exchange Server コネクタ**により、Configuration Manager が Microsoft Exchange Online に接続されて、Configuration Manager コンソールでデバイス情報を監視できるようになります (「[System Center Configuration Manager と Exchange によるモバイル デバイスの管理](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)」を参照してください)。
コンプライアンス ポリシーまたは条件付きアクセス ポリシーを使用するうえでコネクタを使用する必要はありませんが、条件付きアクセスの影響を評価するためのレポートの実行に必要です。

## <a name="requirements-for-exchange-online-dedicated"></a>Exchange Online Dedicated の要件
Exchange Online Dedicated への条件付きのアクセスでは、次を実行するデバイスがサポートされます。
-   Windows 8 以降 (Intune に登録されている場合)
-   Windows 7.0 または Windows 8.1 (ドメインに参加している場合)

  新しい Exchange Online 専用環境にあるテナント専用のドメイン参加 PC への条件付きアクセス
-   Windows Phone 8 以降
-   Exchange ActiveSync (EAS) 電子メール クライアントを使用する iOS デバイス
-   Android 4 以降
-   **従来の Exchange Online Dedicated 環境**のテナントの場合:    

  Configuration Manager を Microsoft Exchange On-premises に接続する **Exchange Server コネクタ**を使用する必要があります。 これにより、モバイル デバイスを管理して、条件付きアクセスを使用できるようになります (「[System Center Configuration Manager と Exchange によるモバイル デバイスの管理](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)」を参照してください)。
-   **新しい Exchange Online Dedicated 環境**のテナントの場合:     
  オプションの **Exchange Server コネクタ**により、Configuration Manager が Microsoft Exchange Online に接続されて、デバイス情報を管理できるようになります (「[System Center Configuration Manager と Exchange によるモバイル デバイスの管理](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)」を参照してください)。 コンプライアンス ポリシーまたは条件付きアクセス ポリシーを使用するうえでコネクタを使用する必要はありませんが、条件付きアクセスの影響を評価するためのレポートの実行に必要です。  

## <a name="requirements-for-exchange-on-premises"></a>Exchange On-premises の要件
Exchange On-premises に対する条件付きアクセスでは、次のデバイスをサポートします。
-   Windows 8 以降 (Intune に登録されている場合)
-   Windows Phone 8 以降
-   iOS のネイティブ電子メール アプリ
-   Android 4 以降のネイティブ電子メール アプリ
-   Microsoft Outlook アプリはサポートされていません (Android および iOS)。

**補足**:

-  Exchange のバージョンは、Exchange 2010 以降である必要があります。 Exchange Server クライアント アクセス サーバー (CAS) アレイがサポートされています。

> [!TIP]
> Exchange 環境が CAS サーバー構成にある場合は、CAS サーバーのいずれかを指すようにオンプレミスの Exchange コネクタを構成する必要があります。
- Configuration Manager を Microsoft Exchange On-premises に接続する **Exchange Server コネクタ**を使用する必要があります。 これにより、モバイル デバイスを管理して、条件付きアクセスを使用できるようになります (「[System Center Configuration Manager と Exchange によるモバイル デバイスの管理](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)」を参照してください)。
  - 最新バージョンの **On-Premises Exchange Connector**を使用していることを確認してください。 オンプレミスの Exchange コネクタは、Configuration Manager コンソールから構成する必要があります。 詳細な手順の説明については、「[System Center Configuration Manager と Exchange によるモバイル デバイスの管理](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)」を参照してください。
  - コネクタは、System Center Configuration Manager のプライマリ サイトにのみ構成する必要があります。</li><li>このコネクタは、Exchange CAS 環境をサポートします。 <br />        コネクタを構成する際には、Exchange CAS サーバーのいずれかと通信するように設定する必要があります。

- Exchange ActiveSync は、証明書ベースの認証またはユーザーの資格情報のエントリで構成できます。


## <a name="requirements-for-skype-for-business-online"></a>Skype for Business Online の要件
SharePoint Online への条件付きアクセスでは、次を実行するデバイスがサポートされます。
 -   iOS 7.1 以降
 -   Android 4.0 以降
 -   Samsung KNOX Standard 4.0 以降

**さらに**、Skype for Business Online の先進認証を有効にする必要があります。 この [接続フォーム](https://connect.microsoft.com/office/Survey/NominationSurvey.aspx?SurveyID=17299&ProgramID=8715) に必要事項を記入して、最新の認証プログラムに登録します。

すべてのエンドユーザーが Skype for Business Online を使用している必要があります。 Skype for Business Online と Skype for Business オンプレミスの両方が含まれている展開の場合は、条件付きアクセス ポリシーはオンプレミスの展開を使用するエンドユーザーに適用されません。

## <a name="requirements-for-sharepoint-online"></a>SharePoint Online の要件
SharePoint Online への条件付きアクセスでは、次を実行するデバイスがサポートされます。
 -   Windows 8.1 以降 (Intune に登録されている場合)
 -   Windows 7.0 または Windows 8.1 (ドメインに参加している場合)
 -   Windows Phone 8.1 以降
 -   iOS 7.1 以降
 -   Android 4.0 以降、Samsung KNOX Standard 4.0 以降

 **補足**:
 -   デバイスをワークプレース参加させる必要があります。ワークプレース参加させると、デバイスは Azure Active Directory Device Registration Service (AAD DRS) に登録されます。

 ドメインに参加した PC は、グループ ポリシーまたは MSI によって自動的に Azure Active Directory に登録されるはずです。 このトピックの「 **PC の条件付きアクセス** 」セクションに、PC の条件付きアクセスを有効にするためのすべての要件が説明されています。

 AAD DRS は、Intune や Office 365 のお客様に対して自動的にアクティブ化されます。 ADFS Device Registration Service をデプロイ済みのお客様には、オンプレミスの Active Directory で登録されたデバイスは表示されません。
 -   SharePoint Online サブスクリプションが必要です。ユーザーには、SharePoint Online のライセンスが必要です。

 ### <a name="conditional-access-for-pcs"></a>PC の条件付きアクセス

 PC が Office デスクトップ アプリケーションを実行して **Exchange Online** と **SharePoint Online** にアクセスする場合、次の要件を満たす PC に対して条件付きアクセスをセットアップできます。
 -   Windows 7.0 または Windows 8.1 を実行している PC であること。
 -   ドメインに参加しているか、ドメイン対応の PC であること。

 準拠するためには、PC は Intune に登録済みで、ポリシーに準拠している必要があります。

 ドメインに参加する PC の場合、Azure Active Directory に [デバイスを自動的に登録](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) するように設定する必要があります。
 -   [Office 365 の最新の認証が有効化](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)されていて、最新の Office 更新プログラムがすべて適用されている必要があります。<br />     最新の認証により、Active Directory Authentication Library (ADAL) ベースのサインインが Office 2013 Windows クライアントに導入され、 **多要素認証**および **証明書ベースの認証**などのより強力なセキュリティが有効になります。
 -   最新ではない認証プロトコルをブロックするように ADFS 要求規則を設定します。  

## <a name="next-steps"></a>次のステップ  
 必要なシナリオのコンプライアンス ポリシーと条件付きアクセス ポリシーを構成する方法については、次のトピックを参照してください。  

-   [System Center Configuration Manager でのデバイス コンプライアンス ポリシーの管理](../../protect/deploy-use/device-compliance-policies.md)  

-   [System Center Configuration Manager でのメール アクセスの管理](../../protect/deploy-use/manage-email-access.md)  

-   [System Center Configuration Manager での SharePoint Online アクセスの管理](../../protect/deploy-use/manage-sharepoint-online-access.md)  

-   [Skype for Business Online のアクセスの管理](../../protect/deploy-use/manage-skype-for-business-online-access.md)  

### <a name="see-also"></a>関連項目  

 [System Center Configuration Manager のコンプライアンス設定を使ってみる](../../compliance/get-started/get-started-with-compliance-settings.md)

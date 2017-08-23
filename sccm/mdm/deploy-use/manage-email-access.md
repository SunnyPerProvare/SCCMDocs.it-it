---
title: "電子メール アクセスの管理 | Microsoft Docs"
description: "System Center Configuration Manager の条件付きアクセスを使用して Exchange メールへのアクセスを管理する方法について説明します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fa648e73-5fb8-4818-ab57-7466ffaf888e
caps.latest.revision: "24"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: a5c2a8912cd2ef95a778b81d0b7f1f98315b8413
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="manage-email-access-in-system-center-configuration-manager"></a>System Center Configuration Manager でのメール アクセスの管理

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の条件付きアクセスを使用して、指定した条件に基づいて Exchange メールへのアクセスを管理します。  

以下のものへのアクセスを管理できます。  

-   Microsoft Exchange On-premises  

-   Microsoft Exchange Online  

-   Exchange Online Dedicated

次のプラットフォームでは、組み込みの電子メール クライアントから Exchange Online と Exchange On-premises へのアクセスを制御できます。  

-   Android 4.0 以降、Samsung KNOX Standard 4.0 以降  

-   iOS 7.1 以降  

-   Windows Phone 8.1 以降  

-   Windows 8.1 以降でのメール アプリケーション

以下を実行している PC で、Office デスクトップ アプリケーションから Exchange Online にアクセスできます。  

-   [最新の認証](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) が有効にされた Office デスクトップ 2013 以降。  

-   Windows 7.0 または Windows 8.1  

> [!NOTE]  
>  PC はドメインに参加しているか、Intune で設定されたポリシーに準拠している必要があります。  


## <a name="device-requirements"></a>デバイスの要件
 条件付きアクセスを構成すると、ユーザーが電子メールに接続するには、使用するデバイスが以下の条件を満たさなくてはならなくなります。  

-   Intune に登録されているか、ドメインに参加する PC である。  

-   デバイスが Azure Active Directory に登録されている (デバイスが Intune に登録されている場合は、自動的に登録されます) (Exchange Online のみ)。 また、クライアントの Exchange ActiveSync ID が Azure Active Directory に登録されている必要があります (Exchange On-premises に接続している Windows および Windows Phone デバイスには該当しません)。  

     ドメインに参加している PC の場合、Azure Active Directory に自動的に登録するように設定する必要があります。  「[System Center Configuration Manager でサービスへのアクセスを管理する](../../protect/deploy-use/manage-access-to-services.md)」トピックの「**PC の条件付きアクセス**」セクションでは、PC の条件付きアクセスを有効にするためのすべての要件を示します。  

-   そのデバイスに展開されているすべての Configuration Manager コンプライアンス ポリシーを遵守している。  

 条件付きアクセス条件が満たされない場合、ユーザーにはログイン時に以下のうちのいずれかのメッセージが表示されます。  

-   デバイスが Intune に登録されていないか、Azure Active Directory に登録されていない場合は、ポータル サイト アプリのインストールとデバイスの登録の手順が示されているメッセージが表示されます。Android および iOS デバイスの場合は、メールをアクティブ化する手順も示されます。アクティブ化によって、デバイスの Exchange ActiveSync ID と Azure Active Directory 内のデバイス レコードが関連付けられます。  

-   デバイスがポリシーに準拠していない場合は、ユーザーを Intune Web ポータルに導くメッセージが表示されます。このポータルで、問題とその修復方法に関する情報を確認することができます。  

**モバイル デバイスの場合:**

**iOS** および **Android** デバイスのブラウザーからアクセスされるときの Exchange Online 上の **Outlook Web Access (OWA)** へのアクセスを制限することができます。  準拠デバイスでの、サポートされる以下のブラウザーからのアクセスのみ許可されます。

* Safari (iOS)
* Chrome (Android)
* 管理対象ブラウザー (iOS と Android)

サポートされていないブラウザーはブロックされます。IOS および Android 用の OWA アプリはサポートされていません。  ADFS 要求規則を介してこれらをブロックする必要があります。
* 最新ではない認証プロトコルをブロックするように ADFS 要求規則を設定します。 詳しい手順は、シナリオ 3 - [ブラウザー ベースのアプリケーション以外の O365 への外部アクセスをすべてブロックする](https://technet.microsoft.com/library/dn592182.aspx)に関するページを参照してください。

 **PC の場合:**  

-   条件付きアクセス ポリシーの要件が **[ドメインに参加する]** または **[準拠]**を許可することである場合、デバイスを登録する方法についての手順が示されているメッセージが表示されます。 PC がどちらの要件も満たさない場合、ユーザーはデバイスを Intune に登録するように求められます。  

-   条件付きアクセス ポリシーの要件がドメインに参加している Windows デバイスのみを許可するように設定されている場合は、デバイスはブロックされ、IT 管理者に問い合わせるようにメッセージが表示されます。  

 Exchange ActiveSync 電子メール クライアントを組み込まれた、以下のプラットフォームのデバイスから Exchange 電子メールへのアクセスをブロックできます。  

-   Android 4.0 以降、Samsung KNOX Standard 4.0 以降  

-   iOS 7.1 以降  

-   Windows Phone 8.1 以降  

-   Windows 8.1 以降での **メール** アプリケーション  

 iOS と Android 用の Outlook アプリ、および Outlook デスクトップ 2013 以上がサポートされるのは、Exchange Online に限られます。  

 条件付きアクセスが機能するには、Configuration Manager と Exchange 間に **On-Premises Exchange Connector** が必要です。  

 Configuration Manager コンソールから、Exchange On-premises の条件付きアクセス ポリシーを構成できます。 Exchange Online 用の条件付きアクセス ポリシーを構成する場合、Configuration Manager コンソールでプロセスを開始できます。これにより、Intune コンソールが起動し、そこでプロセスを完了することができます。  

## <a name="configure-conditional-access"></a>条件付きアクセスの構成
### <a name="step-1-evaluate-the-effect-of-the-conditional-access-policy"></a>手順 1. 条件付きアクセス ポリシーの効果を評価する  
 **オンプレミスの Exchange Connector** を構成した後、Configuration Manager の**条件付きアクセスの状態ごとのデバイスの一覧**レポートを使用して、条件付きアクセス ポリシーを構成した後に Exchange へのアクセスがブロックされるデバイスを識別できます。 このレポートには以下も必要です。  

-   Intune のサブスクリプション  

-   サービス接続ポイントを構成して配置する必要があります。  

 レポート パラメーターで、評価する Intune グループを選び、必要に応じて、ポリシーを適用するデバイス プラットフォームを選びます。  

 レポートの実行方法の詳細については、「[System Center Configuration Manager のレポート](../../core/servers/manage/reporting.md)」を参照してください。  

 レポートを実行した後、ユーザーをブロックするかどうかを判断するために、次の 4 つの列を調べます。  

-   **[管理チャネル]** - デバイスが Intune、Exchange ActiveSync、またはその両方によって管理されているかどうかを示します。  

-   **[AAD に登録済み]** - デバイスが Azure Active Directory に登録されている (社内参加と呼ばれます) かどうかを示します。  

-   **[準拠]** - デバイスが、展開したすべてのコンプライアンス ポリシーに準拠しているかどうかを示します。  

-   **[EAS アクティブ化]** - iOS および Android デバイスで、Exchange ActiveSync ID が Azure Active Directory のデバイス登録レコードに関連付けられている必要があります。 これは、ユーザーが検疫電子メールで [ **電子メールのアクティブ化** ] のリンクをクリックしたときに発生します。  

    > [!NOTE]  
    >  Windows Phone デバイスは、常にこの列の値を表示します。  

 対象グループまたはコレクションの一部であるデバイスは、列の値が以下の表に示されている値と一致しない限り、Exchange にアクセスできないようにブロックされます。  

|[管理チャネル]|AAD に登録済み|[準拠]|[EAS アクティブ化]|結果の動作|  
|------------------------|--------------------|---------------|-------------------|----------------------|  
|**Microsoft Intune および Exchange ActiveSync による管理の対象**|○|○|[**はい** ] または [ **いいえ** ] が表示されます|電子メール アクセスが許可される|  
|その他の値|いいえ|いいえ|値が表示されない|電子メール アクセスがブロックされる|  

 レポートの内容をエクスポートし、 **[電子メール アドレス]** 列を使って、ブロックされることをユーザーに通知できます。  

### <a name="step-2-configure-user-groups-or-collections-for-the-conditional-access-policy"></a>手順 2. 条件付きアクセス ポリシーの対象としてユーザー グループまたはコレクションを構成する  
 条件付きアクセス ポリシーは、ポリシーの種類に応じて、さまざまなユーザーのグループまたはコレクションを対象とします。 これらのグループには、ポリシーの対象となるユーザーや、ポリシーから除外されるユーザーが含まれます。 ユーザーがポリシーの対象となる場合、ユーザーに使用される各デバイスが電子メールにアクセスするには、ポリシーを遵守している必要があります。  

-   **Exchange Online ポリシーの場合** - Azure Active Directory セキュリティ ユーザー グループを対象。 これらのグループは、 **Office 365 管理センター**または **Intune アカウント ポータル**で構成できます。  

-   **Exchange On-premises ポリシーの場合** - Configuration Manager ユーザー コレクションを対象。 [ **資産とコンプライアンス** ] ワークスペースでこれらを構成できます。  

 各ポリシーには、次の 2 つのグループの種類を指定できます。  

-   **対象グループ** - ポリシーが適用されるユーザー グループまたはコレクション  

-   **例外グループ** - ポリシーから除外されるユーザー グループまたはコレクション (省略可能)  

 ユーザーが両方に含まれている場合は、ポリシーから除外されます。  

 条件付きアクセス ポリシーの対象となるグループまたはコレクションだけが、Exchange アクセスのために評価されます。  

### <a name="step-3-configure-and-deploy-a-compliance-policy"></a>手順 3. コンプライアンス ポリシーを構成し、展開する  
 コンプライアンス ポリシーを作成し、Exchange 条件付きアクセス ポリシーの対象となるすべてのデバイスに展開したことを確認します。  

 コンプライアンス ポリシーを構成する方法の詳細については、「[System Center Configuration Manager でのデバイス コンプライアンス ポリシーの管理](device-compliance-policies.md)」を参照してください。  

> [!IMPORTANT]  
>  コンプライアンス ポリシーを展開していない状態で、Exchange 条件付きアクセス ポリシーを有効にすると、すべての対象デバイスによるアクセスが許可されます。  

 準備ができたら、 **手順 4.**に進みます。  

### <a name="step-4-configure-the-conditional-access-policy"></a>手順 4. 条件付きアクセス ポリシーを構成する  

#### <a name="for-exchange-online-and-tenants-in-the-new-exchange-online-dedicated-environment"></a>Exchange Online (および新しい Exchange Online Dedicated 環境のテナント) の場合

>[!NOTE]
>Azure AD 管理コンソールで条件付きアクセス ポリシーを作成することもできます。 Azure AD の管理コンソールでは、Intune デバイス条件付きアクセス ポリシー (Azure AD のデバイスベースの条件付きアクセス ポリシーと呼ぶ) に加えて、多要素認証のような他の条件付きアクセス ポリシーを作成することができます。 また、Salesforce や Box など、Azure AD がサポートするサード パーティ製エンタープライズ アプリ用の条件付きアクセス ポリシーを設定することもできます。 詳細については、「[Azure Active Directory に接続されたアプリケーションのアクセスを制御する Azure Active Directory デバイス ベースの条件付きアクセス ポリシーを設定する方法](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-policy-connected-applications/)」を参照してください。

 Exchange Online の条件付きアクセス ポリシーは、次のフローを使用して、デバイスを許可するかブロックするかを評価します。  

 ![ConditionalAccess8&#45;1](media/ConditionalAccess8-1.png)  

 電子メールにアクセスするには、デバイスは以下の条件を満たす必要があります。  

-   Intune に登録する。  

-   PC はドメインに参加しているか、登録されており、Intune で設定されたポリシーに準拠している必要があります。  

-   デバイスが Azure Active Directory に登録されている (デバイスが Intune に登録されている場合は、自動的に登録されます)。  

     ドメインに参加する PC の場合、Azure Active Directory に [デバイスを自動的に登録](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) するように設定する必要があります。  

-   アクティブ化された電子メールがある。これによって、デバイスの Exchange ActiveSync ID が Azure Active Directory のデバイス レコードに関連付けられます (iOS および Android デバイスのみに適用)。  

-   展開されているすべてのコンプライアンス ポリシーを遵守している。  

 デバイスの状態は Azure Active Directory に格納され、条件の評価に基づいて、電子メールへのアクセスが許可されたりブロックされたりします。  

 条件が満たされない場合、ユーザーにはログイン時に以下のうちのいずれかのメッセージが表示されます。  

-   デバイスが登録されていないか、Azure Active Directory に登録されている場合は、メッセージが表示され、ポータル サイト アプリのインストールと登録の手順が示されます。  

-   デバイスが準拠していない場合は、Intune の会社ポータル Web サイトまたは会社ポータルのアプリにユーザーを誘導するメッセージが表示されます。このポータルで、ユーザーは問題とその解決方法に関する情報を確認できます。  

-   PC の場合:  

    -   ドメインへの参加を要求するようにポリシーを設定して、PC がドメインに参加していない場合、IT 管理者に連絡するようにメッセージが表示されます。  

    -   ドメインへの参加または遵守を要求するようにポリシーを設定して、PC がいずれかの要件を満たしていない場合、ポータル サイト アプリをインストールして登録する方法についての手順が示されたメッセージが表示されます。  

 メッセージは、新しい Exchange Online Dedicated 環境の Exchange Online ユーザーおよびテナントのデバイスに表示され、Exchange On-premises および従来の Exchange Online Dedicated デバイスのユーザー受信トレイに配信されます。  

> [!NOTE]  
>  Configuration Manager 条件付きアクセス規則は、Exchange Online 管理コンソールで定義された規則を上書き、許可、ブロック、および検疫します。  

> [!NOTE]  
>  条件付きアクセス ポリシーは、Intune コンソールで構成する必要があります。 Intune コンソールに Configuration Manager を介してアクセスし、次の手順を開始します。 要求された場合は、Configuration Manager と Intune 間のサービス接続ポイントを設定するために使用した資格情報を使用してログインします。  

##### <a name="to-enable-the-exchange-online-policy"></a>Exchange Online ポリシーを有効にするには  

1.  Configuration Manager コンソールで、[ **資産とコンプライアンス**] をクリックします。  

2.  [ **コンプライアンス設定**]、[ **条件付きアクセス**] の順に展開し、[ **Exchange Online**] をクリックします。  

3.  [ **ホーム** ] タブの [ **リンク** ] グループで、[ **Intune コンソールでの条件付きアクセス ポリシーの構成**] をクリックします。 Configuration Manager を Intune サービスの全体管理者と結び付けるために使用したアカウントのユーザー名とパスワードの入力が必要になる場合があります。  

     Intune 管理コンソールが開きます。  

4.  [Microsoft Intune 管理コンソール](https://manage.microsoft.com)で、**[ポリシー]**  >  **[条件付きアクセス]**  >  **[Exchange Online ポリシー]** をクリックします。  

     ![HybridOnlineSetupIntune](media/HybridOnlineSetupIntune.png)  

5.  **[Exchange Online ポリシー]** ページで、 **[Exchange Online の条件付きアクセス ポリシーを有効にする]**を選択します。 これをチェックする場合、デバイスは準拠している必要があります。 これをチェックしないと、条件付きアクセスは適用されません。  

    > [!NOTE]  
    >  コンプライアンス ポリシーを展開していない状態で、Exchange Online ポリシーを有効にすると、すべての対象となるデバイスが準拠デバイスとして報告されます。  
    >   
    >  コンプライアンスの状態に関係なく、ポリシーの対象となっているすべてのユーザーがデバイスを Intune に登録する必要があります。  

6.  Outlook、および先進認証を使用するその他のアプリの **[アプリケーション アクセス]**で、各プラットフォームの準拠デバイスのみにアクセスを制限することを選択できます。  Windows デバイスはドメインに参加しているか、Intune に登録または準拠している必要があります。  

    > [!TIP]  
    >  **先進認証** では、Active Directory Authentication Library (ADAL) ベースのサインインが Office クライアントに提供されます。  
    >   
    >  -   ADAL ベースの認証を使用すると、Office クライアントでブラウザー ベースの認証 (パッシブ認証とも呼ばれます) を利用できます。  認証する際に、ユーザーはサインイン Web ページに転送されます。  
    > -   この新しいサインイン方法では、 **デバイスのコンプライアンス** と、 **多要素認証** が実行されたかどうかに基づいて、条件付きのアクセスなどの新しいシナリオを実現できます。  
    >   
    >  先進認証の動作の詳細については、この [記事](https://support.office.com/en-US/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517) を参照してください。  

     Configuration Manager と Intune と共に Exchange Online を使用すると、条件付きアクセスでモバイル デバイスだけではなく、デスクトップ コンピューターも管理できます。 PC はドメインに参加しているか、または Intune に登録または準拠している必要があります。 以下の要件を設定できます。  

    -   **デバイスはドメインに参加しているか準拠デバイスである必要があります。** PC はドメインに参加しているか、ポリシーに準拠している必要があります。 PC がどちらの要件も満たさない場合、ユーザーはデバイスを Intune に登録するように求められます。  

    -   **デバイスはドメインに参加している必要があります** 。PC は Exchange Online にアクセスするために、ドメインに参加する必要があります。 PC がドメインに参加していない場合、メールへのアクセスはブロックされ、ユーザーは IT 管理者に連絡するように求められます。  

    -   **デバイスは準拠デバイスである必要があります** PC は Intune に登録および準拠している必要があります。 PC を登録していない場合は、登録する方法についての手順を示したメッセージが表示されます。  

7.  **Outlook web access (OWA)**で、サポートされるブラウザーである Safari (iOS) および Chrome (Android) による Exchange Online へのアクセスのみ許可することができます。 その他のブラウザーからのアクセスはブロックされます。 Outlook のアプリケーション アクセス用に選択した、同じプラットフォーム制限もここで適用されます。

    **Android** デバイスで、ユーザーはブラウザー アクセスを有効にする必要があります。  これを行うには、エンドユーザーは以下のように、登録されたデバイス上で [ブラウザー アクセスを有効にする] オプションを有効にする必要があります。
     1. **ポータル サイト アプリ**を起動します。
     2. トリプル ドット (...) またはハードウェアのメニュー ボタンから、 **[設定]** ページに移動します。
      3.    **[ブラウザー アクセスを有効にする]** ボタンを押します。
      4.    Chrome ブラウザーでは、Office 365 からサインアウトし、Chrome を再起動します。

     **IOS および Android** プラットフォームでは、サービスへのアクセスに使用するデバイスを特定するために、Azure Active Directory によってトランスポート層セキュリティ (TLS) 証明書がデバイスに対して発行されます。  デバイスは、次のスクリーンショットに示すように、証明書を選択するようエンドユーザーに促すプロンプトとともに証明書を表示します。 エンドユーザーは、ブラウザーを使用し続けるには、まずこの証明書を選択する必要があります。

     **Android**

     ![iPad での証明書プロンプトのスクリーンショット](media/mdm-browser-ca-ios-cert-prompt_v2.png)

    **Outlook Web Access (OWA)**

    ![Android デバイスでの証明書プロンプトのスクリーンショット](media/mdm-browser-ca-android-cert-prompt.png)

7.  **[Exchange ActiveSync メール アプリ]**では、デバイスがポリシーに準拠していない場合にメールによる Exchange Online へのアクセスをブロックすることを選択できます。Intune がデバイスを管理できない場合にメールへのアクセスを許可またはブロックすることも選択できます。  

8.  **[対象グループ]**で、ポリシーを適用するユーザーの Active Directory セキュリティ グループを選択します。  

    > [!NOTE]  
    >  対象グループに含まれているユーザーについては、Exchange のルールとポリシーが Intune のポリシーに置き換えられます。  
    >   
    >  次の場合にのみ、Exchange の許可、ブロック、検疫のルールと、Exchange のポリシーが適用されます。  
    >   
    >  -   ユーザーが Intune のライセンスを取得していない。  
    > -   ユーザーが Intune のライセンスを取得しているが、条件付きアクセス ポリシーの対象となるどのセキュリティ グループにも属していない。  

9. **[例外グループ]**で、このポリシーから除外するユーザーの Active Directory セキュリティ グループを選択します。 ユーザーが対象グループと例外グループの両方に属している場合、ユーザーはポリシーから除外され、自分のメールにアクセスできます。  

10. 操作が完了したら、 **[保存]**をクリックします。  

-   条件付きアクセス ポリシーを展開する必要はありません。直ちに有効になります。  

-   ユーザーが電子メール アカウントを作成すると、デバイスはすぐにブロックされます。  

-   ブロックされたユーザーがデバイスを Intune に登録すると (または非準拠を修復すると)、メールのアクセスは 2 分以内にブロック解除されます。  

-   ユーザーがデバイスの登録を解除した場合、メールは約 6 時間後にブロックされます。  

### <a name="for-exchange-on-premises-and-tenants-in-the-legacy-exchange-online-dedicated-environment"></a>Exchange On-premises (および従来の Exchange Online Dedicated 環境のテナント) の場合  
 従来の Exchange Online Dedicated 環境の Exchange On-premises およびテナントの条件付きアクセス ポリシーは、次のフローを使用して、デバイスを許可するかブロックするかを評価します。  

 ![ConditionalAccess8&#45;2](media/ConditionalAccess8-2.png)  

##### <a name="to-enable-the-exchange-on-premises-policy"></a>Exchange On-premises ポリシーを有効にするには  

1.  Configuration Manager コンソールで、[ **資産とコンプライアンス**] をクリックします。  

2.  [ **コンプライアンス設定**]、[ **条件付きアクセス**] の順に展開し、[ **On-Premises Exchange**] をクリックします。  

3.  [ **ホーム** ] タブの [ **On-Premises Exchange** ] グループで、[ **条件付きアクセス ポリシーの構成**] をクリックします。  

4.  **Configuration Manager のバージョン 1602 以降**では、 **条件付きアクセス ポリシーの構成ウィザード** の **[全般]**ページで、Exchange Active Sync の既定ルールを上書きするかどうかを指定します。 既定のルールが検疫またはアクセス禁止に設定されていたとしても、登録された準拠デバイスが電子メールにいつでもアクセスできるようにするには、このオプションの登録をクリックします。  

    > [!NOTE]  
    >  Android デバイスの既定の上書きに関する問題があります。 Exchange サーバーの既定のアクセス ルールが **[ブロック]** に設定されていて、既定のルールの上書きオプションと Exchange 条件付きアクセス ポリシーが有効である場合は、対象ユーザーの Android デバイスが Intune に登録されて準拠したとしても、デバイスのブロックが解除されない可能性があります。  この問題を回避するには、既定の Exchange アクセス ルールを **[検疫]**に設定します。 このデバイスから Exchange へのアクセスは既定で許可されることはありません。管理者は Exchange サーバーから検疫対象デバイスの一覧にレポートを取得できます。  

     Exchange Connector をセットアップするときに、通知の電子メール アカウントをセットアップしなかった場合は、このページに警告が表示されて、 **[次へ]** ボタンが無効になります。  続行するには、最初に Exchange Connector で通知の電子メール設定を構成してから、 **条件付きアクセス ポリシーの構成ウィザード** に戻って、プロセスを完了する必要があります。  

     ![HybridCondAccessWiz1](media/HybridCondAccessWiz1.PNG)  

     [次へ] をクリックします。 ****  

5.  [ **対象コレクション** ] ページで、1 つまたは複数のユーザー コレクションを追加します。 Exchange にアクセスするには、これらのコレクション内のユーザーは、Intune にデバイスを登録し、展開されたすべてのコンプライアンス ポリシーに準拠する必要があります。  

     ![HybridCondAccessWiz2](media/HybridCondAccessWiz2.PNG)  

     [次へ] をクリックします。 ****  

6.  [ **除外コレクション** ] ページで、条件付きアクセス ポリシーから除外するすべてのユーザー コレクションを追加します。 これらのグループ内のユーザーは、Intune にデバイスを登録する必要はなく、Exchange にアクセスするために、展開されたコンプライアンス ポリシーに準拠する必要もありません。  

     ![HybridCondAccessWiz3](media/HybridCondAccessWiz3.png)  

     ユーザーが対象リストと例外リストの両方に属している場合、ユーザーは条件付きアクセス ポリシーから除外されます。  

     [次へ] をクリックします。 ****  

7.  **[ユーザー通知の編集]** ページで、Intune がデバイスのブロックを解除する方法についての指示と共にユーザーに送信するメールを構成します (Exchange が送信するメールに加えて)。  

     既定のメッセージを編集したり、テキストの表示方法を HTML タグで書式設定したりすることができます。 変更の予定を通知し、デバイスを登録する手順を説明するメールを事前に従業員に送信することもできます。  

     ![HybridCondAccessWiz4](media/HybridCondAccessWiz4.PNG)  

    > [!NOTE]  
    >  修復手順が記載されている Intune 通知電子メールはユーザーの Exchange 受信トレイに送信されるため、電子メール メッセージを受信する前にユーザーのデバイスがブロックされた場合は、ブロックされていないデバイスや、Exchange にアクセスするその他の方法を使用して、メッセージを表示できます。  

    > [!NOTE]  
    >  Exchange が通知電子メールを送信できるようにするには、通知電子メールの送信に使用されるアカウントを構成する必要があります。 Exchange Server コネクタのプロパティを構成する場合に、これを実行します。  
    >   
    >  詳細については、「[System Center Configuration Manager と Exchange によるモバイル デバイスの管理](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)」を参照してください。  

     [次へ] をクリックします。 ****  

8.  [  **概要** ] ページで設定を確認し、ウィザードを完了します。  

-   条件付きアクセス ポリシーを展開する必要はありません。直ちに有効になります。  

-   ユーザーが Exchange ActiveSync のプロファイルを設定してからデバイスがブロックされるまでに、1 ～ 3 時間かかる場合があります (Intune で管理されていない場合)。  

-   ブロックされたユーザーがデバイスを Intune に登録すると (または非準拠を修復すると)、メールのアクセスは 2 分以内でブロック解除されます。  

-   ユーザーが Intune から登録解除した場合、デバイスがブロックされるまでに 1 ～ 3 時間かかる場合があります。  

### <a name="see-also"></a>関連項目  
 [System Center Configuration Manager でサービスへのアクセスを管理する](../../protect/deploy-use/manage-access-to-services.md)

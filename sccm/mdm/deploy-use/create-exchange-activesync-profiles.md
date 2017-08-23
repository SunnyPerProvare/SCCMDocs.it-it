---
title: "Exchange ActiveSync 電子メール プロファイルを作成する | Microsoft Docs"
description: "Microsoft Intune と連携して機能する System Center Configuration Manager で電子メール プロファイルを作成および構成する方法について説明します。"
ms.custom: na
ms.date: 07/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 120442be-179e-450c-a0c4-284046895da3
caps.latest.revision: "4"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 7434c98f2217cf63fdcd250b91e772de72daaea9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="exchange-activesync-email-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager で Exchange ActiveSync 電子メール プロファイルを作成する

*適用対象: System Center Configuration Manager (Current Branch)*

Microsoft Intune と Exchange ActiveSync を利用すると、デバイスに電子メール プロファイルと制約を設定できます。 ユーザーは最小限の設定で自分のデバイスから会社の電子メールにアクセスできるようになります。  

 次の種類のデバイスに電子メール プロファイルを構成できます。  

- Windows 10
- Windows Phone 8.1
- Windows Phone 8.0
- iPhone (iOS 5、iOS 6、iOS 7、iOS 8)  
- iPad (iOS 5、iOS 6、iOS 7、iOS 8)  
- Samsung KNOX Standard (4 以降)
- Android for Work

電子メール プロファイルをデバイスに展開するには、デバイスを Intune に登録する必要があります。 デバイスの登録方法については、「 [Microsoft Intune を使用したモバイル デバイスの管理](https://technet.microsoft.com/en-us/library/dn646962.aspx)」を参照してください。

> [!NOTE]
> Intune には Android for Work 電子メール プロファイルが 2 つあります。それぞれ、Gmail 電子メール アプリ用と Nine Work 電子メール アプリ用です。 これらのアプリは Google Play ストアで入手できます。また、Exchange への接続をサポートしています。 電子メール接続を有効にするには、いずれかの電子メール アプリをユーザーのデバイスに展開し、適切なプロファイルを作成して展開します。 Nine Work などの電子メール アプリは有料になる場合があります。 アプリケーションのライセンスの詳細を確認するか、アプリの会社に問い合わせてください。

 デバイスに電子メール アカウントを構成するだけでなく、アドレス帳、予定表、作業の同期を設定できます。  

 電子メール プロファイルを作成するとき、さまざまなセキュリティ設定を含めることができます。 たとえば、ID の証明書、暗号化、System Center Configuration Manager プロファイルにより設定された署名などです。 証明書プロファイルの詳細については、「[System Center Configuration Manager の証明書プロファイル](/sccm/protect/deploy-use/introduction-to-certificate-profiles.md)」を参照してください。    

## <a name="create-an-exchange-activesync-email-profile"></a>Exchange ActiveSync 電子メール プロファイルを作成する  

プロファイルを作成するには、Exchange ActiveSync 電子メール プロファイルの作成ウィザードを利用します。 

1.  Configuration Manager コンソールで、**[資産とコンプライアンス]** を選択します。  

2.  **[資産とコンプライアンス]** ワークスペースで、**[コンプライアンス設定]**、**[会社リソースのアクセス]** の順に展開し、**[電子メール プロファイル]** を選択します。  

3.  **[ホーム]** タブの **[作成]** グループで、**[Exchange ActiveSync 電子メール プロファイルの作成]** を選択し、ウィザードを起動します。

4.  ウィザードの **[全般]** ページで、次のように構成します。

    - **名前**。 電子メール プロファイルにわかりやすい名前を指定します。

    - **説明**。 必要に応じて、Configuration Manager コンソールで識別するのに役立つ電子メール プロファイルの説明を指定します。

    - **この電子メール プロファイルは Android for Work 用です**。 Android for Work デバイスにのみこの電子メール プロファイルを展開する場合、このオプションを選択します。 このチェック ボックスをオンにした場合、**サポートされているプラットフォーム** ウィザード ページは表示されません。 Android for Work の電子メール プロファイルのみが構成されます。

4.  ウィザードの **[Exchange ActiveSync]** ページで、次の情報を指定します。  

    -   **Exchange ActiveSync ホスト**。 Exchange ActiveSync サービスをホストする社内 Exchange サーバーのホスト名を指定します。  

    -   **アカウント名**。 ユーザーのデバイスに表示される電子メール アカウントの表示名を指定します。  

    -   **アカウントのユーザー名**。 クライアント デバイスで電子メール アカウントのユーザー名を構成する方法を選択します。 ドロップダウン リストから次のオプションのいずれかを選択できます。  

        -   **ユーザー プリンシパル名**。 完全なユーザー プリンシパル名を使用して Exchange にサインインします。  

        -   **AccountName**。 Active Directory の完全なユーザー アカウント名を使用します。

        -   **プライマリ SMTP アドレス**。 ユーザーのプライマリ SMTP アドレスを使用して Exchange にサインインします。  

    -   **電子メール アドレス**。 各クライアント デバイスでユーザーの電子メール アドレスを生成する方法を選択します。 ドロップダウン リストから次のオプションのいずれかを選択できます。  

        -   **プライマリ SMTP アドレス**。 ユーザーのプライマリ SMTP アドレスを使用して Exchange にサインインします。  

        -   **ユーザー プリンシパル名**。 電子メール アドレスとして完全ユーザー プリンシパル名を使用します。  

    -   **アカウント ドメイン**。 次のいずれかのオプションを選択します。  

        -   **Active Directory から取得する**  

        -   **カスタム**  

         このフィールドは、**[sAMAccountName]** が **[アカウントのユーザー名]** ドロップボックス リストで選択されている場合にのみ該当します。  

    -   **認証方法**。 Exchange ActiveSync への接続の認証に使用する認証方法を次から 1 つ選択します。  

        -   **証明書**。 ID 証明書を Exchange ActiveSync 接続の認証に使用します。  

        -   **ユーザー名とパスワード**。 デバイスのユーザーが Exchange ActiveSync に接続するには、パスワードを入力する必要があります。 (ユーザー名は電子メール プロファイルの一部として構成されます。)  

    -   **ID 証明書**。 **[選択]** を選択し、ID として使用する証明書を選択します。  

         ID 証明書には SCEP 証明書を使用する必要があります。PFX 証明書は使用できません。  詳細については、「[Certificate profiles in System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles)」(System Center Configuration Manager の証明書プロファイル) を参照してください。  

         このオプションは、**[認証方法]** の下で **[証明書]** を選択した場合にのみ利用できます。  

    -   **S/MIME を使用する**。 S/MIME 暗号化を使用して送信メールを送信します。 このオプションは iOS デバイスにのみ適用されます。 次のオプションを選択します。

        -   **[署名証明書]**。  **[選択]** を選択し、暗号化に使用する証明書プロファイルを選択します。  

            SCEP 証明書または PFX 証明書のプロファイルを使用できます。  ただし、署名と暗号化の両方を使用する場合は、署名と暗号化の*両方*のために PFX 証明書プロファイルを選択する必要があります。

        -   **暗号化証明書**。 **[選択]** を選択し、暗号化に使用する証明書を選択します。 暗号化証明書として使うことができるのは、PFX 証明書だけです。

        -   iOS デバイス上のすべての電子メール メッセージを暗号化するには、**[暗号化を必須にする]** をオンにします。    

         この項目を選択するには、証明書プロファイルを作成しておく必要があります。  詳細については、「[Certificate profiles in System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles)」(System Center Configuration Manager の証明書プロファイル) を参照してください。  

## <a name="configure-synchronization-settings-for-the-exchange-activesync-email-profile"></a>Exchange ActiveSync 電子メール プロファイルの同期設定を構成します。  

Exchange ActiveSync 電子メール プロファイルの作成ウィザードの [ **同期設定の構成** ] ページで、次の情報を指定します。  

-   **スケジュール**。 デバイスが Exchange サーバーからデータを同期するスケジュールを選択します。 このオプションは Windows Phone デバイスにのみ適用できます。 次の中から選択します。  

    -   **未構成**。 同期スケジュールは強制されません。 それにより、独自の同期スケジュールを構成できます。  

    -   **メッセージの着信時**。 電子メールや予定表アイテムなどのデータが到着したとき、自動的に同期します。  

    -   **15 分**。 電子メールや予定表アイテムなどのデータが 15 分おきに同期されます。  

    -   **30 分**。 電子メールや予定表アイテムなどのデータが 30 分おきに同期されます。  

    -   **60 分**。 電子メールや予定表アイテムなどのデータが 60 分おきに同期されます。  

    -   **手動**。 手動で同期を開始する必要があります。  

-   **同期する電子メールの日数**。 ドロップダウン リストから、同期する電子メールの日数を選択します。 次のいずれかの値を選択します。  

    -   **未構成**。 設定は強制されません。 そのため、デバイスにダウンロードする電子メールの量を構成できます。  

    -   **無制限**。 利用可能なすべての電子メールを同期します。  

    -   **1 日**  

    -   **3 日間**  

    -   **1 週間**  

    -   **2 週間**  

    -   **1 か月**  

-   **他の電子メール アカウントへのメッセージの移動を許可する**。 このオプションを選択すると、デバイス上に構成されている複数のアカウント間で電子メール メッセージを移動できます。 このオプションは iOS デバイスにのみ適用されます。  

-   **サード パーティ製アプリケーションからの電子メールの送信を許可する**。 このオプションを選択すると、既定ではない、サードパーティ製アプリケーションから電子メールを送信できます。 このオプションは iOS デバイスにのみ適用されます。  

-   **最近使用した電子メール アドレスを同期する**。 このオプションを選択すると、デバイスで最近使用された電子メール アドレスのリストが同期されます。 このオプションは iOS デバイスにのみ適用されます。  

-   **SSL の使用**。 電子メールの送受信と Exchange Server との通信に Secure Sockets Layer (SSL) 通信を使用するには、このオプションを選択します。  

-   **同期するコンテンツの種類**。 デバイスに同期するコンテンツの種類を選択します。 このオプションは Windows Phone デバイスにのみ適用できます。 次の中から選択します。  

    -   **電子メール**  

    -   **連絡先**  

    -   **カレンダー**  

    -   **タスク**  

## <a name="specify-supported-platforms-for-the-exchange-activesync-email-profile"></a>Exchange ActiveSync 電子メール プロファイルにサポートされているプラットフォームを指定します。  

1.  Exchange ActiveSync 電子メール プロファイルの作成ウィザードの **[サポートされているプラットフォーム]** ページで、電子メール プロファイルをインストールするオペレーティング システムを選択します。 あるいは、**[すべて選択]** を選択し、利用可能なすべてのオペレーティング システムに電子メール プロファイルをインストールします。  

2.  ウィザードを終了します。

Exchange ActiveSync 電子メール プロファイルを展開する方法については、「[How to Deploy Email Profiles in Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)」(System Center Configuration Manager でプロファイルを展開する方法) を参照してください。  

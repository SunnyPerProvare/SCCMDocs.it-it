---
title: "Managed Browser ポリシーを使用したインターネット アクセスの管理 | Microsoft Docs"
description: "Intune Managed Browser を展開してインターネット アクセスを管理および制限します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e25e00c-c9a8-473f-bcb7-ea989f6ca3c5
caps.latest.revision: "6"
caps.handback.revision: "0"
author: mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: d2dd2c25a2714851ba1e71414cabcef38d3ce014
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="manage-internet-access-using-managed-browser-policies-with-system-center-configuration-manager"></a>System Center Configuration Manager での Managed Browser ポリシーを使用したインターネット アクセスの管理

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager では、Intune Managed Browser という Web 閲覧アプリケーションを展開し、アプリケーションを Managed Browser ポリシーに関連付けることができます。 Managed Browser ポリシーは、Managed Browser のユーザーがアクセスできる Web サイトを制限する許可リストまたはブロック リストをセットアップするものです。  

 このアプリは管理対象アプリであり、モバイル アプリケーション管理ポリシーを適用できます。切り取り、コピー、貼り付けの利用の管理などです。 画面のキャプチャを禁止し、コンテンツのリンクが他の管理対象アプリでのみ開くようにできます。 詳細については、「[Protect apps using mobile application management policies](protect-apps-using-mam-policies.md)」 (モバイル アプリケーション管理ポリシーを使ったアプリの保護) を参照してください。  

> [!IMPORTANT]  
>  ユーザーが Managed Browser を自分でインストールした場合、指定されたポリシーで管理されなくなります。 ブラウザーを確実に Configuration Manager で管理するには、ユーザーにアプリをアンインストールしてもらってから、管理対象アプリとして展開する必要があります。  

 次の種類のデバイス用に Managed Browser のポリシーを作成することができます。  

-   Android 4 以降が実行されているデバイス  

-   iOS 7 以降を実行するデバイス  

> [!NOTE]  
>  Intune Managed Browser アプリの詳細とダウンロード方法については、[iTunes](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) (iOS の場合)、および [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en) (Android の場合) を参照してください。  

## <a name="create-a-managed-browser-policy"></a>Managed Browser のポリシーを作成する  

1.  Configuration Manager コンソールで、**[ソフトウェア ライブラリ]** > **[アプリケーション管理]** > **[アプリケーション管理ポリシー]** の順に選択します。  

3.  **[ホーム]** タブの **[作成]** グループで、**[アプリケーション管理ポリシーの作成]** を選択します。  

4.  **[全般]** ページで、ポリシーの名前と説明を入力してから、**[次へ]** を選択します。  

5.  **[ポリシーの種類]** ページで、プラットフォームを選択し、ポリシーの種類で **[管理対象ブラウザー]** を選択してから、 **[次へ]**を選択します。  

     **[管理対象ブラウザー]** ページで、次のオプションのいずれかを選択します。  

    -   **Managed Browser が以下に示す URL のみを開けるようにする** : Managed Browser で開くことができる URL の一覧を指定します。  

    -   **Managed Browser が以下に示す URL を開けないようにする** : Managed Browser で開けないようにブロックする URL の一覧を指定します。  

    > [!NOTE]  
    >  同じ Managed Browser ポリシーに、許可される URL とブロックされる URL の両方を含めることはできません。  

     指定できる URL の形式の詳細については、この記事の「許可される URL とブロックされる URL の形式」を参照してください。  

    > [!NOTE]  
    >  [全般] ポリシーの種類を使用すると、会社のコンプライアンス ポリシーとセキュリティ ポリシーに合わせて、展開するアプリの機能を変更することができます。 たとえば、切り取り、コピー、貼り付けの各操作を制限付きのアプリ内で制限することができます。 全般的なポリシーの種類の詳細については、「[Protect apps using mobile application management policies](protect-apps-using-mam-policies.md)」 (モバイル アプリケーション管理ポリシーを使ったアプリの保護) を参照してください。  

6.  ウィザードを終了します。  

新しいポリシーが **[ソフトウェア ライブラリ]** ワークスペースの **[アプリケーション管理ポリシー]** ノードに表示されます。  

## <a name="create-a-software-deployment-for-the-managed-browser-app"></a>Managed Browser アプリ向けにソフトウェアの展開を作成する  
 管理対象ブラウザー ポリシーを作成した後、管理対象ブラウザー アプリ向けにソフトウェア展開の種類を作成できます。 管理対象ブラウザー アプリには、全般ポリシーと管理対象ブラウザー ポリシーの両方を関連付ける必要があります。  

 詳細については、「[Create applications](create-applications.md)」 (アプリケーションを作成する) を参照してください。  

## <a name="security-and-privacy-for-the-managed-browser"></a>Managed Browser のセキュリティとプライバシー  

-   iOS デバイスでは、証明書の有効期限が切れている Web サイトや証明書が信頼されていない Web サイトにユーザーがアクセスしても、開くことができません。  

-   ユーザーが自分のデバイスの組み込みブラウザーに対して構成した設定は、Managed Browser では使用されません。 Managed Browser はこれらの設定にアクセスできません。  

-   Managed Browser に関連付けられているモバイル アプリケーション管理ポリシーで **[アクセスの際にシンプルな PIN を要求する]** オプションか **[アクセスの際に会社の資格情報を要求する]** オプションが設定されている場合は、ユーザーが認証ページのヘルプ リンクをクリックすると、Managed Browser ポリシーのブロック リストに追加されている場合でも、ユーザーはすべてのサイトにアクセスできます。  

-   Managed Browser では、直接アクセスされたときのみ、サイトへのアクセスをブロックできます。 サイトへのアクセスに中間サービス (翻訳サービスなど) が使用されている場合は、アクセスをブロックすることができません。  

## <a name="reference-information"></a>参照情報  

###  <a name="url-format-for-allowed-and-blocked-urls"></a>許可される URL とブロックされる URL の形式  

許可リストとブロック リストで URL を指定するときに使用できる形式とワイルドカードについて説明します。  

-   ワイルドカード記号 "**\***" は、以下の許可されているパターン リストの規則に従って使用できます。  

-   リストに入力するときは、すべての URL の先頭に必ず **http** または **https** を付けてください。  

-   アドレスにはポート番号を指定できます。 ポート番号を指定しない場合は、次の値が使用されます。  

    -   http の場合はポート 80  

    -   https の場合はポート 443  

     **http://www.contoso.com:\*** や **http://www.contoso.com: /\*** のように、ポート番号にワイルドカードを使用することはできません。  

-   URL を指定するときに使用できるパターンの詳細については、次の表を参照してください。  

    |[URL]|［一致する］|［次の値に一致しない］|  
    |---------|-------------|--------------------|  
    |http://www.contoso.com<br /><br /> 単一のページと一致する|www.contoso.com|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> contoso.com/|  
    |http://contoso.com<br /><br /> 単一のページと一致する|contoso.com/|host.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com|  
    |http://www.contoso.com/*<br /><br /> www.contoso.com で始まるすべての URL と一致する|www.contoso.com<br /><br /> www.contoso.com/images<br /><br /> www.contoso.com/videos/tvshows|host.contoso.com<br /><br /> host.contoso.com/images|  
    |http://*.contoso.com/\*<br /><br /> contoso.com の下のすべてのサブドメインに一致する|developer.contoso.com/resources<br /><br /> news.contoso.com/images<br /><br /> news.contoso.com/videos|contoso.host.com|  
    |http://www.contoso.com/images<br /><br /> 単一のフォルダーと一致する|www.contoso.com/images|www.contoso.com/images/dogs|  
    |http://www.contoso.com:80<br /><br /> ポート番号を使用し、単一のページと一致する|http://www.contoso.com:80||  
    |https://www.contoso.com<br /><br /> セキュリティで保護された単一のページと一致する|https://www.contoso.com|http://www.contoso.com|  
    |http://www.contoso.com/images/*<br /><br /> 1 つのフォルダーおよびすべてのサブフォルダーと一致する|www.contoso.com/images/dogs<br /><br /> www.contoso.com/images/cats|www.contoso.com/videos|  

-   指定することができない入力例を次に示します。  

    -   *.com  

    -   *.contoso/\*  

    -   www.contoso.com/*images  

    -   www.contoso.com/*images\*pigs  

    -   www.contoso.com/page*  

    -   IP アドレス  

    -   https://*  

    -   http://*  

    -   http://www.contoso.com:*  

    -   http://www.contoso.com:/*  

> [!NOTE]  
>  *.microsoft.com は常に許可されます。  

### <a name="how-conflicts-between-the-allow-and-block-list-are-resolved"></a>許可リストとブロック リストの競合を解決する方法  
 複数の Managed Browser ポリシーがデバイスに展開され、設定が競合する場合、モード (許可またはブロック) と URL の一覧の両方が競合していると判断されます。 競合が発生した場合は、次の動作が適用されます。  

-   各ポリシーのモードは同じで、URL の一覧が異なる場合、URL はデバイスに適用されません。  

-   各ポリシーのモードが異なり、URL の一覧は同じである場合、URL はデバイスに適用されません。  

-   デバイスが初めて Managed Browser ポリシーを受信するときに、2 つのポリシーが競合する場合、URL はデバイスに適用されません。 **[ポリシー]** ワークスペースの **[ポリシーの競合]** ノードを使用して、競合を表示します。  

-   デバイスが Managed Browser ポリシーを既に受信していて、2 番目のポリシーが競合する設定で展開される場合、元の設定がデバイスに残ります。 **[ポリシー]** ワークスペースの **[ポリシーの競合]** ノードを使用して、競合を表示します。  

---
title: "デバイス登録のセットアップ | Microsoft Docs"
description: "System Center Configuration Manager でのオンプレミス モバイル デバイス管理の対象となるデバイスを登録できるアクセス許可をユーザーに付与します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ffaea91-1379-4b86-9953-b25e152f56a9
caps.latest.revision: "10"
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.openlocfilehash: 16d4106d486d821b7ce92a1de65ebb04469d18de
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="set-up-device-enrollment-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>System Center Configuration Manager でのオンプレミスのモバイル デバイス管理のデバイス登録の設定

*適用対象: System Center Configuration Manager (Current Branch)*

ユーザーが System Center Configuration Manager のオンプレミス モバイル デバイス管理に自分のデバイスを登録できるようにするには、そのためのアクセス許可をユーザーに付与する必要があります。 ユーザーにアクセス許可を付与してデバイスを登録するには、以下のタスクを実行します。

-   [ユーザーが最新のデバイスを登録できるようにするための登録プロファイルを作成する](#bkmk_createProf)  

-   [登録されているデバイスの追加のクライアント設定のセットアップ](#bkmk_addClient)  

-   [ユーザーが最新のデバイス登録プロファイルを受信できるようにする](#bkmk_enableUsers)  

-   [登録するデバイスにルート証明書を格納する](#bkmk_storeCert)  

##  <a name="bkmk_createProf"></a> ユーザーが最新のデバイスを登録できるようにするための登録プロファイルを作成する  
 最新のデバイスをユーザーが登録するのに必要な設定をプッシュするため、新しい登録プロファイルを既定のクライアント設定に追加できます。これは、Configuration Manager サイトで検出されるすべてのユーザーに適用されます。  

1.  Configuration Manager コンソールで、**[管理]** > **[概要]** > **[クライアント設定]**の順にクリックして **[既定のクライアント設定]** を開き、**[登録]** を選択します。  

2.  [デバイスの設定] で、最新のデバイスのポーリング間隔を指定します。  

3.  [ユーザー設定] の **[ユーザーが最新のデバイスを登録できるようにする]** で **[はい]**を選びます。  

4.  **[最新のデバイス登録プロファイル]** の横にある **[プロファイルの設定...]** をクリックし、**[作成...]** をクリックします。  

5.  [登録プロファイルの作成] で登録プロファイルの名前を入力し、登録プロファイルを持つユーザーが使用する管理サイト コードを選びます。 **[OK]** を何回かクリックして、[既定の設定] ページを終了します。  

> [!NOTE]  
>  検出されたユーザーのサブセットに登録プロファイルを展開する場合は、ユーザーのコレクションを使用し、そのコレクションに展開するためのカスタム クライアント設定を作成できます。 カスタム クライアント設定を作成する方法については、「 [How to configure client settings in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md)」をご覧ください。  

##  <a name="bkmk_addClient"></a> 登録されているデバイスの追加のクライアント設定のセットアップ  
 最新のデバイスの登録プロファイルをセットアップするだけでなく、登録時に、デバイスを構成する他のクライアント設定をセットアップすることができます。  クライアント設定をセットアップする方法については、「[System Center Configuration Manager でクライアント設定を構成する方法](../../core/clients/deploy/configure-client-settings.md)」を参照してください。  

 オンプレミス モバイル デバイス管理では使用できないクライアント設定があります。 Configuration Manager の現在のブランチでは、オンプレミス モバイル デバイス管理について、次のクライアント設定がサポートされています。  

-   登録 - これらの設定は、管理対象デバイスの登録プロファイルを指定します。 登録プロファイルをセットアップする方法の詳細については、「 [ユーザーが最新のデバイスを登録できるようにするための登録プロファイルを作成する](#bkmk_createProf)」を参照してください。  

-   クライアント ポリシー - これらの設定は、デバイスにクライアント ポリシーをダウンロードする頻度を指定します。 また、ポリシーのポーリングを使用した対象ユーザーの設定を有効にすることができます。 クライアント ポリシー設定の詳細については、「[System Center Configuration Manager のクライアント設定について](../../core/clients/deploy/about-client-settings.md)」の「クライアント ポリシー」セクションを参照してください。  

-   ソフトウェアの展開 - この設定は、ソフトウェアの展開用にクライアント デバイスを評価する間隔を設定します。 ソフトウェア展開の設定の詳細については、「[System Center Configuration Manager のクライアント設定について](../../core/clients/deploy/about-client-settings.md)」の「ソフトウェアの展開」セクションを参照してください。  

    > [!NOTE]  
    >  オンプレミス モバイル デバイス管理の場合は、ソフトウェア展開の設定は、既定のクライアント設定としてのみ使用できます。 ソフトウェア展開の設定は、Configuration Manager の現在のブランチのカスタム クライアント設定では使用できません。  

##  <a name="bkmk_enableUsers"></a> ユーザーが最新のデバイス登録プロファイルを受信できるようにする  
 ユーザーは、変更されたクライアント設定をオンプレミス モバイル デバイス管理の登録プロファイルによって受信するために、Active Directory の探索方法で検出される必要があります。 必要とする全員が登録プロファイルを取得できるように、Active Directory ユーザーの探索を実行します。 ユーザーの検出方法の手順については、「 [Run discovery for System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md)」をご覧ください。  

##  <a name="bkmk_storeCert"></a> 登録するデバイスにルート証明書を格納する  
 ドメインに参加しているデバイスを持つユーザーは、サイト システムの役割をホストするサーバーとの信頼された通信のための必要なルート証明書を既に持っていると考えられます。これは、Active Directory を使用したドメイン参加プロセスの一部としてルートが発行されているためです。 ドメインに参加していないコンピューターとモバイル デバイスは、デバイスにルート証明書を手動でインストールして、登録を実行できるようにする必要があります。 これらのデバイスが必要なルート証明書を自動的に持つことはありません。  

 エクスポートされた証明書ファイルを用意して、デバイスに手動でインストールできるようにする必要があります。 これは、メール、OneDrive、SD カード、USB メモリ、またはニーズに最適な方法を使用して実行できます。  

 デバイスで使用するルート証明書は、「[Web サーバー証明書と同じルートの証明書をエクスポートする](../../mdm/get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert)」でエクスポートした証明書です。  

1.  登録するデバイスで、ルート証明書ファイルを検索し、ダブルクリックします。  

2.  [証明書] ウィンドウで **[証明書のインストール...]** をクリックします。  

3.  証明書のインポート ウィザードで **[ローカル コンピューター]**を選び、 **[次へ]**をクリックします。  

4.  [ユーザー アカウント コントロール] ウィンドウで **[はい]**をクリックします。  

5.  **[証明書をすべて次のストアに配置する]**を選び、 **[参照]**をクリックします。  

6.  **[信頼されたルート証明機関]**をクリックして、 **[OK]**をクリックし、 **[次へ]**をクリックします。  

7.  **[完了]**をクリックします。  

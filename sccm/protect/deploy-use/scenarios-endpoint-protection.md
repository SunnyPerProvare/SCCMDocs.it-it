---
title: "Endpoint Protection でマルウェアからコンピューターを保護するシナリオ | Microsoft Docs"
description: "Configuration Manager で Endpoint Protection を実装してマルウェアからコンピューターを保護する方法について説明します。"
ms.custom: na
ms.date: 03/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 539c7a89-3c03-4571-9cb4-02d455064eeb
caps.latest.revision: "8"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: b98684d44874ff246e4d675039c6e443aee82a62
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="example-scenario-using-system-center-endpoint-protection-to-protect-computers-from-malware-in-system-center-configuration-manager"></a>シナリオ例: System Center Configuration Manager でSystem Center Endpoint Protection を使用してマルウェアからコンピューターを保護する

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックには、Configuration Manager で Endpoint Protection を実装して、組織のコンピューターをマルウェアによる攻撃から保護する方法に関するサンプル シナリオを示します。  

 John は、Woodgrove Bank の Configuration Manager 管理者です。 現在この銀行は System Center Endpoint Protection を使用して、マルウェアによる攻撃からコンピューターを保護しています。 また、Windows グループ ポリシーによって、社内のすべてのコンピューターで Windows ファイアウォールが有効になっていること、Windows ファイアウォールが新しいプログラムをブロックする場合にはユーザーに通知することが確認されています。  

 John は、ウッドグローブ銀行のマルウェア対策ソフトウェアを System Center Endpoint Protection にアップグレードするよう依頼されています。アップグレードによって、最新のマルウェア対策機能を利用し、Configuration Manager コンソールからマルウェア対策ソリューションを一元管理できるようになります。 この実装を行うには、以下の要件があります。  

-   Configuration Manager を使用して、現在グループ ポリシーによって管理されている Windows ファイアウォール設定を管理します。  

-   Configuration Manager ソフトウェア更新プログラムを使用して、マルウェア定義をコンピューターにダウンロードします。 ソフトウェア更新プログラムが利用できない場合 (たとえば、コンピューターが企業ネットワークに接続されていない場合など)、コンピューターは、Microsoft Update から定義ファイルの更新プログラムをダウンロードする必要があります。  

-   ユーザーのコンピューターでは、毎日マルウェアのクイック スキャンを実行する必要があります。 ただしサーバーは、業務時間外の毎週土曜日午前 1 時に、フル スキャンを実行する必要があります。  

-   次のいずれかのイベントが発生するたびに電子メール アラートを送信します。  

    -   いずれかのコンピューターでマルウェアが検出される。  

    -   5% を超えるコンピューターで同じマルウェアの脅威が検出される  

    -   任意の 24 時間以内に同じマルウェアの脅威が 6 回以上検出される  

    -   任意の 24 時間以内に 4 つ以上の異なる種類のマルウェアが検出される  

-   既存のマルウェア対策ソリューションをアンインストールします。  

 John は、Endpoint Protection を実装するために次の手順を実行します。  

##  <a name="steps-to-implement-endpoint-protection"></a>Endpoint Protection を実装する手順を実行します。  

|プロセス|参照先|  
|-------------|---------------|  
|John は、Configuration Manager での Endpoint Protection の基本概念に関して、提供されている情報を確認します。|Endpoint Protection の詳細については、「[System Center Configuration Manager での Endpoint Protection](endpoint-protection.md)」を参照してください。|  
|Endpoint Protection を使用するために必要な前提条件を確認して実装します。|Endpoint Protection の前提条件の詳細については、「[Endpoint Protection の導入計画](../plan-design/planning-for-endpoint-protection.md)」を参照してください。|  
|ウッドグローブ銀行の最上位階層にある 1 つのサイト システム サーバーにのみ Endpoint Protection サイト システムの役割をインストールします。|Endpoint Protection サイト システムの役割をインストールする方法について詳しくは、「[Configure Endpoint Protection](configure-endpoint-protection.md)」(Endpoint Protection の構成) の「前提条件」を参照してください。|  
|SMTP サーバーを使用して電子メール アラートを送信するように Configuration Manager を構成します。<br /><br /> **注:** SMTP サーバーを構成する必要があるのは、Endpoint Protection アラートが生成されるときに電子メールで通知する場合のみです。|詳細については、「[Endpoint Protection のアラートを構成する](endpoint-configure-alerts.md)」を参照してください。|  
|Endpoint Protection クライアントをインストールするすべてのコンピューターとサーバーが含まれるデバイス コレクションを作成します。 このコレクションに**「Endpoint Protection によって保護されるすべてのコンピューター」**という名前を付けます。<br /><br /> **ヒント:** ユーザーのコレクションに対してアラートを構成することはできません。|コレクションを作成する方法については、「[System Center Configuration Manager でコレクションを作成する方法](../../core/clients/manage/collections/create-collections.md)」を参照してください。|  
|彼には、コレクションの次のアラートを構成します。 <br /><br />1) **マルウェアが検出された場合**: アラートの重要度 **[重大]** を構成します。 <br /><br />2) **多数のコンピューターで同じ種類のマルウェアが検出された場合**: アラートの重要度 **[重大]** を構成し、5% を超えるコンピューターでマルウェアが検出された場合にこのアラートが生成されることを指定します。 <br /><br />3) **同種類のマルウェアが指定時間内に特定のコンピューター上で繰り返し検出される場合**: アラートの重要度 **[重大]** を構成し、マルウェアが 24 時間以内に 6 回以上検出された場合にこのアラートが生成されることを指定します。 <br /><br />4) **複数の種類のマルウェアが指定時間内に特定のコンピューター上で検出される場合**: アラートの重要度 **[重大]** を構成し、4 種類以上のマルウェアが 24 時間以内に検出された場合にこのアラートが生成されることを指定します。<br /><br /> **[アラートの重要度]** の値は、Configuration Manager コンソールに、および電子メール メッセージで受信するアラートに表示されるアラート レベルを示します。<br /><br /> さらに、Configuration Manager コンソールでアラートを監視できるように、オプション **[このコレクションを Endpoint Protection ダッシュボードに表示する]** を選択します。|「[System Center Configuration Manager での Endpoint Protection の構成](endpoint-configure-alerts.md)」の「Endpoint Protection のアラートを構成する」を参照してください。|  
|Configuration Manager ソフトウェア更新プログラムを、自動展開ルールを使用して 1 日に 3 回、定義の更新プログラムをダウンロードして展開するように構成します。|詳細については、「[Use Configuration Manager software updates to deliver definition updates](endpoint-definitions-configmgr.md)」(Configuration Manager ソフトウェア更新プログラムを使用して定義の更新プログラムを配信する) の「Configuration Manager ソフトウェア更新プログラムにより定義の更新プログラムを配信する」を参照してください。|  
|既定のマルウェア対策ポリシーの設定を調べます。この設定には、Microsoft によって推奨されているセキュリティ ポリシーが含まれています。 毎日のクイック スキャンを実行するコンピューターに関しては、次の設定を変更します。<br /><br /> 1) **クライアント コンピューターでクイック スキャンを毎日実行する**: **はい**<br /><br /> 2) **日次クイック スキャンの実行予定時刻**: **午前 9:00**<br /><br /> 定義の更新プログラムのソースとして **[Microsoft Update から配信される更新プログラム]** が既定で選択されています。 この選択項目は、Configuration Manager ソフトウェアの更新プログラムを受信できない場合には、コンピューターは Microsoft Update から定義をダウンロードするというビジネス要件と合致します。|「[System Center Configuration Manager で Endpoint Protection 用にマルウェア対策ポリシーを作成し展開する方法](endpoint-antimalware-policies.md)」を参照してください。|  
|**「ウッドグローブ銀行のサーバー」**という名前のウッドグローブ銀行のサーバーのみが含まれるコレクションを作成します。|[「System Center Configuration Manager でコレクションを作成する方法](../../core/clients/manage/collections/create-collections.md)」を参照してください|  
|**「ウッドグローブ銀行のサーバー ポリシー」**という名前のカスタム マルウェア対策ポリシーを作成します。 **[スケジュールされたスキャン]** の設定にのみ、次の変更を加えます。<br /><br /> **スキャンの種類**:  **完全**<br /><br /> **スキャンの実行**:  **土曜日**<br /><br /> **スキャン時刻**: **午前 1:00**<br /><br /> **クライアント コンピューターでクイック スキャンを毎日実行する**:  **いいえ**|「[System Center Configuration Manager で Endpoint Protection 用にマルウェア対策ポリシーを作成し展開する方法](endpoint-antimalware-policies.md)」を参照してください。|  
|**「ウッドグローブ銀行のサーバー ポリシー」** カスタム マルウェア対策ポリシーを **「ウッドグローブ銀行のサーバー」** コレクションに展開します。|「[Endpoint Protection 用にマルウェア対策ポリシーを作成し展開する方法](endpoint-antimalware-policies.md)」の「マルウェア対策ポリシーをクライアント コンピューターに展開するには」を参照してください。|  
|Endpoint Protection の新しいカスタム クライアント デバイス設定セットを作成し、「**ウッドグローブ銀行の Endpoint Protection 設定**」という名前を付けます。<br /><br /> **注:** 階層内のすべてのクライアントにおいて Endpoint Protection をインストールして使用可能にする必要がない場合には、**[クライアント コンピューターの Endpoint Protection クライアントを管理する]** と **[Endpoint Protection クライアントをクライアント コンピューターにインストールする]** のどちらも既定のクライアント設定として **[いいえ]** に構成されていることを確認してください。|詳しくは、の「[Endpoint Protection のカスタム クライアント設定を構成する](endpoint-protection-configure-client.md)」を参照してください。|  
|Endpoint Protection に関して以下の設定を構成します。<br /><br /> **[クライアント コンピューターの Endpoint Protection クライアントを管理する]**を実装するために次の手順を実行します。  **はい**<br /><br /> この設定と値を使用すると、インストールされている既存のすべての Endpoint Protection クライアントが Configuration Manager によって管理されます。<br /><br /> **Endpoint Protection クライアントをクライアント コンピューターにインストールする**:  **はい**<br /><br /> **Endpoint Protection をインストールする前に、インストールされているマルウェア対策ソフトウェアを自動的に削除する**:  **はい**<br /><br /> この設定と値を使用すると、Endpoint Protection がインストールされて利用可能になる前に、既存のマルウェア対策ソフトウェアが削除されるというビジネス要件が満たされます。|詳しくは、の「[Endpoint Protection のカスタム クライアント設定を構成する](endpoint-protection-configure-client.md)」を参照してください。|  
|「**ウッドグローブ銀行の Endpoint Protection 設定**」クライアント設定を**「Endpoint Protection によって保護されたすべてのコンピューター」**コレクションに展開します。|「[Configuration Manager の Endpoint Protection の構成](endpoint-antimalware-policies.md)」の「Endpoint Protection のカスタム クライアント設定を構成する」を参照してください。|  
|Windows ファイアウォール ポリシーの作成ウィザードを使用して、ドメイン プロファイル用の次の設定を構成してポリシーを作成します。<br /><br /> 1) **Windows ファイアウォールを有効にする**: **はい**<br /><br /> 2)<br />                    **Windows ファイアウォールが新しいプログラムをブロックしたときにユーザーに通知する**: **はい**|「[System Center Configuration Manager の Endpoint Protection 用 Windows ファイアウォール ポリシーを作成および展開する方法](../../protect/deploy-use/create-windows-firewall-policies.md)」を参照してください。|  
|新しいファイアウォール ポリシーを、先に作成した**「Endpoint Protection によって保護されたすべてのコンピューター」**コレクションに展開します。|「[System Center Configuration Manager の Endpoint Protection 用 Windows ファイアウォール ポリシーを作成および展開する方法](create-windows-firewall-policies.md)」を参照してください。|  
|Endpoint Protection に関して利用可能な管理タスクを使用して、マルウェア対策および Windows ファイアウォールのポリシーの管理、必要に応じたオンデマンドのコンピューター スキャンの実行、コンピューターにおける最新の定義の自動ダウンロード、マルウェアが検出されるときに追加実行する操作の指定を行います。|「[System Center Configuration Manager での Endpoint Protection のためのマルウェア対策ポリシーとファイアウォール設定の管理方法](endpoint-antimalware-firewall.md)」を参照してください。|  
|次の方法によって、Endpoint Protection の状態、および Endpoint Protection が実行する処置を監視します。<br /><br /> 1) **[監視]** ワークスペースの **[セキュリティ]** で **[Endpoint Protection のステータス]** ノードを使用する。<br /><br /> 2) **[資産とコンプライアンス]** ワークスペースの **[Endpoint Protection]** ノードを使用する。<br /><br /> 3) Configuration Manager の組み込みレポートを使用する。|「[System Center Configuration Manager で Endpoint Protection を監視する方法](monitor-endpoint-protection.md)」を参照してください。|  

 John は、Endpoint Protection が正常に実装されたことを上司に報告し、ウッドグローブ銀行のコンピューターが、上司によって指示されたビジネス要件に従ってマルウェアから保護されていることを伝えます。

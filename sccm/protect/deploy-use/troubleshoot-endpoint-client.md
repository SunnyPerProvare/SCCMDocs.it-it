---
title: "Windows Defender または Endpoint Protection クライアントのトラブルシューティング | Microsoft Docs"
description: "Windows Defender および Endpoint Protection の問題をトラブルシューティングする方法について説明します。"
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d837253e-fcc2-422a-9e2c-c78b938dfd8c
caps.latest.revision: "7"
caps.handback.revision: "0"
author: NathBarn
ms.author: nathbarn
manager: angrobe
ms.openlocfilehash: 1b096e71f5131214fb4e235e84d0b7f63e566831
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="troubleshooting-windows-defender-or-endpoint-protection-client"></a>Windows Defender または Endpoint Protection クライアントのトラブルシューティング

*適用対象: System Center Configuration Manager (Current Branch)*


Windows Defender または Endpoint Protection で問題が発生した場合は、サポートについて組織のセキュリティ管理者に問い合わせてください。 また、次の問題のトラブルシューティングを試すこともできます。  

-   [Windows Defender または Endpoint Protection の更新](#update-windows-defender-or-endpoint-protection)  
-   [Windows Defender または Endpoint Protection サービスの開始](#starting-windows-defender-or-endpoint-protection-service)  
-   [インターネット接続の問題](#internet-connection-issues)  
-   [検出された脅威を修復できない](#detected-threat-cant-be-remediated)  
-   [Endpoint Protection クライアントのインストール](#install-the-endpoint-protection-client)  

##  <a name="update-windows-defender-or-endpoint-protection"></a>Windows Defender または Endpoint Protection の更新  
 Windows Defender または Endpoint Protection は、ウイルスおよびスパイウェアの定義を最新の状態に維持するために、自動的に Microsoft Update と連携して動作します。  

 **現象**  

 この資料では、次のケースも含め、自動更新に関するよくある問題を扱います。  

-   更新が失敗したというエラー メッセージが表示される。  

-   更新プログラムを確認するときに、ウイルスおよびスパイウェア定義の更新を確認、ダウンロード、またはインストールできないというエラー メッセージが表示される。  

-   インターネットに接続しているのに、更新に失敗する。  

-   更新プログラムがスケジュールどおりに自動的にインストールされない。  

 **原因**  

 更新に関する問題の最も一般的な原因は、インターネット接続の問題です。 ただし、他の Web サイトを閲覧できるのでインターネットには接続されているという場合は、Windows Internet Explorer で設定が競合して問題を起こしている可能性があります。  

> [!IMPORTANT]  
>  以下の手順を実行するには、Internet Explorer を終了する必要があります。 そのため、手順を印刷するか、書き留めるか、または別のファイルにコピーしてください。また、後でアクセスできるようにこのトピックをお気に入りに登録してください。  

### <a name="step-1-reset-your-internet-explorer-settings"></a>手順 1: Internet Explorer の設定をリセットする  

1.  Internet Explorer を含め、開いているすべてのプログラムを終了します。  

    > [!NOTE]  
    >  Internet Explorer でこれらの設定をリセットすると、一時ファイル、Cookie、閲覧履歴、オンライン パスワードが削除されます。 お気に入りは削除されません。  

2.  **[スタート]** をクリックし、 **inetcpl.cpl**を検索して、 **Enter**キーを押します。  

3.  **[インターネット オプション]** ダイアログ ボックスで、 **[詳細設定]** タブをクリックします。  

4.  **[Internet Explorer の設定をリセット]**の下の **[リセット]**をクリックし、もう一度 **[リセット]** をクリックします。  

5.  Internet Explorer の設定のリセットが完了するまで待ってから、 **[OK]**をクリックします。  

6.  Internet Explorer を開きます。  

7.  Microsoft Security Essentials を開き、 **[更新]** タブをクリックし、 **[更新]**をクリックします。  

8.  問題が解決しない場合は、次の手順に進みます。  

### <a name="step-2-set-internet-explorer-as-the-default-browser"></a>手順 2: Internet Explorer を既定のブラウザーとして設定する  

1.  Internet Explorer を含め、開いているすべてのプログラムを終了します。  

2.  **[スタート]** をクリックし、 **inetcpl.cpl**を検索して、 **Enter**キーを押します。  

3.  **[インターネット オプション]** ダイアログ ボックスで、 **[プログラム]** タブをクリックします。  

4.  **[既定の Web ブラウザー]**の下の **[既定に設定する]**をクリックします。  

5.  **[OK]**をクリックします。  

6.  Windows Defender または Endpoint Protection を開きます。 **[更新]** タブをクリックして、 **[更新]**をクリックします。  

7.  問題が解決しない場合は、次の手順に進みます。  

### <a name="step-3-ensure-that-the-date-and-time-are-set-correctly-on-your-computer"></a>手順 3: コンピューターの日付と時刻が正しく設定されていることを確認する  

1.  Windows Defender または Endpoint Protection を開きます。  

2.  受け取ったエラー メッセージにコード 0x80072f8f が含まれている場合、問題の原因はおそらく、コンピューターに設定されている日付と時刻が不正確なことです。  

3.  コンピューターの日付と時刻の設定を再設定するには、「 [診断ツール Fix it : デスクトップ アイコンが動かないなど一般的なシステムの問題](http://go.microsoft.com/fwlink/?LinkId=155579) (http://go.microsoft.com/fwlink/?LinkId=155579)」にある手順を実行してください。  

### <a name="step-4-rename-the-software-distribution-folder-on-your-computer"></a>手順 4: コンピューターにあるソフトウェア配布フォルダーの名前を変更する  

1. 自動更新サービスを停止します。  

    1.  **[スタート]** をクリックし、 **services.msc**を検索して、 **[OK]**をクリックします。  

    2.  **[自動更新サービス]**を右クリックし、 **[停止**] をクリックします。  

    3.  [サービス] スナップインを最小化します。  

2.  **SoftwareDistribution** ディレクトリの名前を、次のようにして変更します。  

    1.  **[スタート]** をクリックし、  **cmd**を検索して、 **[OK]**をクリックします。  

    2.  「 **cd %windir%**」と入力し、 **Enter**キーを押します。  

    3.  「 **ren SoftwareDistribution SDTemp**」と入力し、 **Enter**キーを押します。  

    4.  「 **exit**」と入力し、 **Enter**キーを押します。  

3.  次のようにして、自動更新サービスを開始します。  

    1.  [サービス] スナップインを最大化します。  

    2.  **[自動更新サービス]**を右クリックし、 **[開始]**をクリックします。  

    3.  [サービス] スナップイン ウィンドウを閉じます。  

### <a name="step-5-reset-the-microsoft-antivirus-update-engine-on-your-computer"></a>手順 5: コンピューターの Microsoft ウイルス対策更新エンジンをリセットする  

1.  **[スタート]** をクリックし、  **cmd**を検索して **[OK]**をクリックした後、 **[コマンド プロンプト]**を右クリックし、 **[管理者として実行]**を選びます。  

2.  **[コマンド プロンプト]** ウィンドウに次のコマンドを入力し、各コマンドを入力した後に **Enter** キーを押します。  

     **Cd\\**  

     **Cd program files\windows defender**  

     **Mpcmdrun -RemoveDefinitions -all**  

     **終了**  

3.  コンピューターを再起動する  

4.  Windows Defender または   
          Endpoint Protection で、**[更新]** タブをクリックし、**[更新]** をクリックします。  

5.  問題が解決しない場合は、次の手順に進みます。  

### <a name="step-6-manually-install-the-virus-and-spyware-definition-updates"></a>手順 6: ウイルスおよびスパイウェア定義の更新を手動でインストールする  

-   32 ビット Windows オペレーティング システムを実行している場合は、次の URL から手動で最新の更新プログラムをダウンロードします: [http://go.microsoft.com/fwlink/?LinkID=87342](http://go.microsoft.com/fwlink/?LinkID=87342) (http://go.microsoft.com/fwlink/?LinkID=87342)。  

-   64 ビット Windows オペレーティング システムを実行している場合は、次の URL から手動で最新の更新プログラムをダウンロードします: [http://go.microsoft.com/fwlink/?LinkID=87341](http://go.microsoft.com/fwlink/?LinkID=87341) (http://go.microsoft.com/fwlink/?LinkID=87341)。  

-   [ **実行**] をクリックします。 最新の更新プログラムが、お使いのコンピューターに手動でインストールされます。  


### <a name="step-7-contact-support"></a>手順 7: サポートに問い合わせる  

-   これらの手順を実行しても問題が解決しない場合は、サポートにお問い合わせください。 詳細については「 [カスタマー サポート](http://go.microsoft.com/fwlink/?LinkID=196174) (http://go.microsoft.com/fwlink/?LinkID=196174)」をご覧ください。  

##  <a name="starting-windows-defender-or-endpoint-protection-service"></a>Windows Defender または Endpoint Protection サービスの開始  
 **現象**  

 "**Windows Defender または Endpoint Protection は、プログラムのサービスが停止しているためコンピューターを監視していません。今すぐサービスを再起動してください**" というメッセージが表示されます。 

 **解決方法**  

### <a name="step-1-restart-your-computer"></a>手順 1: コンピューターを再起動する  

-   すべてのアプリケーションを閉じて、コンピューターを再起動します。  

### <a name="step-2-make-sure-the-windows-defender-or-endpoint-protection-service-is-set-to-automatic-and-is-started"></a>手順 2: "Windows Defender" または "Endpoint Protection サービス" が自動に設定され、開始していることを確認する  

1.  **[スタート]** をクリックし、 **services.msc**を検索して、 **Enter**キーを押します。  

2.  [ **Microsoft Antimalware Service**] を探します。 それを右クリックして [ **プロパティ** ] を選択するか、それをダブルクリックしてサービスを開きます。  

3.  [**スタートアップの種類**] が [**自動**] に設定されていることを確認します。  

4.  [ **開始** ] ボタンをクリックして、サービスを開始します。 [ **開始** ] ボタンが使用できない場合は、[ **停止** ] ボタンをクリックしてから [ **開始** ] ボタンをクリックして、サービスを再開させます。  

5.  このプロセスの間に表示されるエラーは必ずメモしておき、オンラインで問い合わせるときに、そのエラー情報を含めるようにします。  

### <a name="step-3-remove-any-existing-internet-security-programs"></a>手順 3: 既存のすべてのインターネット セキュリティ プログラムを削除する  

1.  **[スタート]** をクリックし、 **appwiz.cpl**を検索して、 **Enter**キーを押します。  

2.  インストールされているプログラムの一覧で、サードパーティのすべてのインターネット セキュリティ プログラムをアンインストールします。*  

3.  コンピューターを再起動して、Windows Defender または   
          Endpoint Protection をもう一度インストールしてみてください。  

> [!NOTE]  
>  一部のインターネット セキュリティ アプリケーションは、完全にはアンインストールされません。 完全に削除するには、それらのセキュリティ アプリケーション用のクリーンアップ ユーティリティをダウンロードして実行しなければならない場合があります。  

> [!CAUTION]  
>  インターネット セキュリティ プログラムを削除すると、コンピューターは保護されなくなります。 既存のインターネット セキュリティ プログラムを削除した後、   
>       Endpoint Protection のインストールに問題がある場合は、Windows Defender または   
>       Endpoint Protection サポートにお問い合わせください。このためには、ケース オンラインを送信します (詳細については、「[How to Submit a Case Online](http://www.microsoft.com/en-ph/security_essentials/Support/8c9074b6-1558-4d14-bc39-d294ced11096.aspx)」 (ケース オンラインの送信方法) を参照してください)。  

### <a name="step-4-uninstallreinstall-endpoint-protection"></a>手順 4: Endpoint Protection のアンインストール/再インストール  

1.  **[スタート]** をクリックし、 **appwiz.cpl**を検索して、 **Enter**キーを押します。  

2.  インストールされているプログラムの一覧で、 **[Endpoint Protection]**をクリックし、アンインストールします。  

3.  必要ならメッセージに従ってコンピューターを再起動し、Endpoint Protection をもう一度インストールしてみてください。  

##  <a name="internet-connection-issues"></a>インターネット接続の問題  
 お使いのコンピューターが Windows Update から最新の更新プログラムを受け取っていることを確認するには、インターネットに接続する必要があります。  

### <a name="step-1-verify-that-your-computer-is-connected-to-the-internet"></a>手順 1: お使いのコンピューターがインターネットに接続されていることを確認する  

1.  **[スタート]**をクリックし、 **ncpa.cpl**を検索して、 **Enter**キーを押します。  

2.  接続名を右クリックし、 **[状態]**をクリックします。  

3.  お使いのコンピューターが接続されている場合、Windows XP では、接続の状態として **[接続]**、 **[有効]**、または **[認証に成功]** と表示されます。 Windows Vista および Windows 7 では、 **[IPv4]** の状態が **[インターネット]**と表示されます。  

4.  コンピューターが接続されていない場合は、接続名を右クリックし、 **[接続]**、 **[有効にする]**、 **[認証]**、または **[修復]**をクリックします。  

### <a name="step-3-restart-your-computer"></a>手順 3: コンピューターを再起動する  

-   開いているプログラムをすべて閉じて、コンピューターを再起動します。  

### <a name="step-4-if-you-still-cant-connect-to-the-internet-check-your-connections"></a>手順 4: まだインターネットに接続できない場合は、接続を確認する  

1.  ダイヤルアップ接続を使用している場合は、電話ケーブルが壁のジャックとモデムにしっかり接続されていることを確認します。  

2.  ケーブル モデムを使用している場合は、モデムへのケーブル接続と、モデムからお使いのコンピューターへの接続がしっかりとできていることを確認します。  

3.  ケーブル モデムまたは DSL ルーターを使用している場合は、ルーターへの接続と、コンピューターへの接続がしっかりとできていることを確認します。 プラグを抜き、ルーターとモデムをオフにしてみます。 数分待ってから、まずモデムにプラグを接続します。1 分待ってから、ルーターにプラグを接続します。コンピューターを再起動します。  

##  <a name="detected-threat-cant-be-remediated"></a>検出された脅威を修復できない  
 Windows Defender または   
      Endpoint Protection が、ファイル名の拡張子が .zip である圧縮ファイル内やネットワーク共有内に隠れている潜在的な脅威を検出すると、その脅威を検疫または削除して対処しようとします。  

### <a name="remove-or-scan-the-file"></a>ファイルを削除またはスキャンする  

-   検出された脅威が .zip ファイル内にあった場合は、.zip ファイルの場所に移動し、そのファイルを削除するか、ファイルを右クリックして **[Windows Defender でスキャン]** または **[Endpoint Protection でスキャン]**を選択してスキャンを実行します。 Windows Defender または Endpoint Protection によってファイル内でさらに脅威が検出された場合は、それらの脅威について通知され、適切な操作を選択できます。  

-   検出された脅威がネットワーク共有内にあった場合は、ネットワーク共有の場所に移動し、ファイルを右クリックして **[Windows Defender でスキャン]** または **[Endpoint Protection でスキャン]**を選択してスキャンを実行します。 Windows Defender または Endpoint Protection によってネットワーク共有内でさらに脅威が検出された場合は、それらの脅威について通知され、適切な操作を選択できます。  

-   ファイルの出所が明確でない場合、最も良い対処方法はコンピューターをフル スキャンすることです フル スキャンは完了までに時間がかかる場合がありますが、Windows Defender または Endpoint Protection で感染源を探し、除去できます。  

##  <a name="install-the-endpoint-protection-client"></a>Endpoint Protection クライアントのインストール  

> [!NOTE]  
>  Windows Defender は、Windows 10 PC のオペレーティング システムと共にインストールされます。  

 **現象**  

 インストールが不明な理由で失敗するか、0x80070643、0X8007064A、0x8004FF2E、0x8004FF01、0x8004FF07、0x80070002、0x8007064C、0x8004FF00、0x80070001、0x80070656、0x8004FF40、0xC0000156、0x8004FF41、0x8004FF0B、0x8004FF11、0x80240022、0x8004FF04、0x80070660、0x800106B5、0x80070715、0x80070005、0x8004EE00、0x8007003、0x800B0100、0x8007064E、0x8007007E などのエラー コードのエラー メッセージが表示されます。  

 コンピューターが Windows XP Service Pack 2 (SP2) を実行している場合は、以下のようなエラー メッセージが表示される場合があります。  

-   インストールを完了するために必要なフィルター マネージャー ロールアップ パッケージがインストール ウィザードで見つかりません。  

-   KB914882 セットアップ エラー、お使いのコンピューターにインストールされている言語が更新プログラムの言語と異なるため、Windows XP のファイルをセットアップで更新できません。  

 **原因**  

 Endpoint Protection は、他のセキュリティ プログラムが実行されているコンピューターにはインストールできません。 他のセキュリティ プログラムを削除しても、それらが完全にはアンインストールされない場合があります。 Endpoint Protection をインストールするには、正規品の Windows オペレーティング システムを実行している必要があります。  

 **解決方法**  

> [!IMPORTANT]  
>  この問題の解決の途中で、コンピューターを再起動する必要があります。 このページにブックマークを設定して ([お気に入り] に追加して)、このトピックを簡単に再表示できるようにするか、印刷して簡単に参照できるようにしてください。  

### <a name="step-1-remove-any-existing-security-programs"></a>手順 1: 既存のすべてのセキュリティ プログラムを削除する  
**エンドポイント保護のみ**

1.  既存のすべてのインターネット セキュリティ プログラムを完全にアンインストールします。  

2.  コンピューターを再起動する  

3.  もう一度 Endpoint Protection をインストールします。 これで問題が解決しない場合は、次の手順に進みます。  

### <a name="step-2-ensure-that-the-windows-installer-service-is-running"></a>手順 2: Windows インストーラー サービスが実行されていることを確認する  

1.  **[スタート]** をクリックし、 **services.msc**を検索して、 **Enter**キーを押します。  

2.  [ **Windows Installer**] を右クリックし、[ **開始**] をクリックします。 [ **開始** ] ボタンが使用できず、[ **停止** ] および [ **再開** ] ボタンが使用可能である場合は、このサービスが既に開始されていることを意味しています。  

3.  [ **サービス** ] ページで [ **ファイル** ] メニューの [ **終了**] をクリックします。  

4.  [**スタート**] ボタンをクリックして [**コマンド プロンプト**] を検索します。 [ **Command Prompt**] を右クリックし、[ **管理者として実行**] をクリックします。  

5.  「 **MSIEXEC /REGSERVER**」と入力し、 **Enter**キーを押します。  

    > [!NOTE]  
    >  このコマンドが成功したか失敗したかは、表示されません。  

6.  もう一度 Endpoint Protection をインストールします。 これで問題が解決しない場合は、次の手順に進みます。  

### <a name="step-3-start-windows-in-selective-startup-mode"></a>手順 3: スタートアップのオプションを選択するモードで Windows を起動する  

1.  **[スタート]** をクリックし、 **msconfig**を検索して、 **Enter**キーを押します。  

2.  [ **全般** ] タブで [ **スタートアップのオプションを選択**] をクリックし、[ **スタートアップの項目を読み込む** ] チェック ボックスをオフにします。  

3.  [ **サービス** ] タブで [ **Microsoft のサービスをすべて隠す** ] チェック ボックスをオンにし、一覧に残っているサービスのすべてのチェック ボックスをオフにします。  

4.  [ **OK**] をクリックし、[ **再起動** ] をクリックして、コンピューターを再起動します。  

5.  もう一度 Endpoint Protection をインストールしてみます。  



### <a name="see-also"></a>関連項目  
 [Endpoint Protection クライアントのよく寄せられる質問](../../protect/deploy-use/endpoint-protection-client-faq.md)   

 [Endpoint Protection クライアント ヘルプ](../../protect/deploy-use/endpoint-protection-client-help.md)

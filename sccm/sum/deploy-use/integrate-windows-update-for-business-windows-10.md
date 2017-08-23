---
title: "Windows 10 における Windows Update for Business との統合 | Microsoft Docs"
description: "Windows Update サービスに接続しているデバイスに関して、Windows Update for Business を利用し、組織の Windows 10 デバイスを最新の状態に維持します。"
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
ms.openlocfilehash: 26e73a69d5e6ca69e766fcf3cedd992353c92cd6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="integration-with-windows-update-for-business-in-windows-10"></a>Windows 10 における Windows Update for Business との統合

*適用対象: System Center Configuration Manager (Current Branch)*

Windows Update for Business (WUfB) を使用すると、組織内の Windows 10 ベースのデバイスが Windows Update (WU) サービスに直接接続しているときに、最新のセキュリティ防御と Windows の機能によってこれらのデバイスが常に最新に保たれるようにすることができます。 Configuration Manager には、WUfB を使用してソフトウェア更新プログラムを取得する Windows 10 コンピューターと、WSUS を使用して取得する Windows 10 コンピューターを区別する機能があります。  

 WUfB または Windows Insider などの WU から更新プログラムを受信するように Configuration Manager クライアントが設定されている場合に、以下に示す Configuration Manager の一部の機能が使用できなくなりました。  

-   Windows Update の適用状況レポート:  

    -   Configuration Manager では WU に発行された更新プログラムは認識されません。 WU から更新プログラムを受信するように構成された Configuration Manager クライアントでは、これらの更新プログラムは Configuration Manager コンソールで **[不明]** と表示されます。  

    -   全体的な適用ステータスのトラブルシューティングが困難になっています。これは、以前は **[不明]** ステータスが WSUS からのスキャン状態を報告していないクライアントに対してのみ使用されていたためです。  今後はこれに、WU から更新プログラムを受信する Configuration Manager クライアントも含まれることになります。  

    -   更新プログラムの適用ステータスに基づいた (会社のリソースに対する) 条件付きアクセスは、WU から更新プログラムを受信するクライアントに対して適切に機能しません。これは、これらのクライアントが Configuration Manager からの適用状況要件を満たすことがないためです。  

    -   定義の更新の適用状況は全体的な更新プログラムの適用状況レポートの一部であるため、これも期待される役目を果たしません。  定義の更新の適用状況は条件付きアクセス評価の一部でもあります。  

-   更新プログラムの適応ステータスに基づく Defender の全体的な Endpoint Protection のレポートでは、スキャン データの不足により正確な結果が返されません。  

-   Configuration Manager は、Office、IE、および Visual Studio などの Microsoft の更新プログラムを、WUfB に接続して更新プログラムを受信するクライアントに展開できません。  

-   Configuration Manager は、WSUS に発行され、かつ Configuration Manager を介して管理されるサード パーティの更新プログラムを、WUfB に接続して更新プログラムを受信するクライアントに展開できません。  

-   ソフトウェア更新プログラムのインフラストラクチャを使用する Configuration Manager の完全なクライアント展開は、WUfB に接続して更新プログラムを受信するクライアントに対しては機能しません。  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>WUfB を使用して Windows 10 の更新プログラムを取得するクライアントを識別する  
 次の手順を使用して、Windows 10 の更新プログラムとアップグレードの取得に WUfB を使用するクライアントを識別し、WSUS を使用して更新プログラムを取得することをやめるようそれらのクライアントを構成して、これらのクライアントのソフトウェア更新ワークフローを無効にするためのクライアント エージェント設定を展開します。  

 **必要条件**  

-   Windows 10 Desktop Pro または Windows 10 Enterprise Edition バージョン 1511 以降を実行するクライアント  

-   [Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx) が展開され、クライアントが WUfB を使用して Windows 10 の更新プログラムとアップグレードを取得している。  

#### <a name="to-identify-clients-that-use-wufb"></a>WUfB を使用するクライアントを識別するには  

1.  Windows Update エージェントが以前有効になっていた場合は、WSUS がスキャンされないように、無効にします。   
    レジストリ キー **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer** を設定し、コンピューターによって WSUS または Windows Update がスキャンされるかどうかを指定できます。  この値が 2 の場合、WSUS についてはスキャンされません。  

2.  Configuration Manager リソース エクスプローラーで、**Windows Update** ノードの下に新しい属性 **UseWUServer** を確認できます。  

3.  更新プログラムとアップグレードのために WUfB を介して接続されているすべてのコンピューターを対象とした **UseWUServer** 属性に基づいて、コレクションを作成します。  

4.  ソフトウェア更新プログラム ワークフローを無効にするクライアント エージェント設定を作成し、WUfB に直接接続されているコンピューターのコレクションに、この設定を展開します。  

5.  WUfB を介して管理されているコンピューターの対応ステータスには **[不明]** と表示され、全体のコンプライアンス対応率をカウントする際に、これらのコンピューターは除外されます。  

## <a name="configure-windows-update-for-business-deferral-policies"></a>Windows Update for Business 遅延ポリシーの構成
<!-- 1290890 -->
Configuration Manager バージョン 1706 以降、Windows Update for Business によって直接管理されている Windows 10 デバイスの Windows 10 機能更新プログラムまたは品質更新プログラムに対し、遅延ポリシーを構成できるようになりました。 遅延ポリシーの管理は、**[ソフトウェア ライブラリ]** > **[Windows 10 のサービス]** の下の新しい **[Windows Update for Business ポリシー]** ノードでできます。

### <a name="prerequisites"></a>必要条件
Windows Update for Business で管理されている Windows 10 デバイスには、インターネット接続が必要です。

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Windows Update for Business 遅延ポリシーを作成するには
1. **[ソフトウェア ライブラリ]** > **[Windows 10 のサービス]** > **[Windows Update for Business ポリシー]** に移動します。
2. **[ホーム]** タブの **[作成]** グループで、**[Windows Update for Business ポリシーを作成する]** を選択し、Windows Update for Business ポリシーの作成ウィザードを開きます。
3. **[全般]** ページで、ポリシーの名前と説明を入力します。
4. **[遅延ポリシー]** ページで、機能更新プログラムを遅延または一時停止するかどうかを設定します。    
    機能更新プログラムは通常、Windows の新機能です。 **[ブランチ準備レベル]** を設定すると、機能更新プログラムが Microsoft からリリースされた場合に、受け取りを遅延させるかどうか、およびその期間を定義できます。
    - **[ブランチ準備レベル]**: Windows Update を受け取るデバイスのブランチを設定します (Current Branch または Current Branch for Business)。
    - **[遅延期間 (日数)]**: 機能更新プログラムを遅延させる日数を指定します。 これらの機能更新プログラムの受け取りは、リリースから 180 日間遅延させることができます。
    - **[Pause Features Updates starting]\(機能更新プログラムの一時停止の開始\)**: デバイスでの機能更新プログラムの受け取りを一時停止するかどうかを選択します。一時停止の期間は最大 60 日間です。 最大日数が経過すると、一時停止機能は自動的に期限切れとなり、デバイスは適用可能な更新を確認するために Windows Update をスキャンします。 このスキャンが終ったら、もう一度更新を一時停止することができます。 機能更新プログラムの一時停止を解除するには、チェック ボックスをオフにします。   
5. 品質更新プログラムを遅延または一時停止するかどうかを選択します。     
    品質更新プログラムは通常、既存の Windows 機能の修正と機能強化で、通常は毎月第 1 火曜日に公開されますが、Microsoft が任意のタイミングでリリースすることもあります。 品質更新プログラムが利用可能になった場合に受け取りを遅延させるかどうか、およびその期間を定義できます。
    - **[遅延期間 (日数)]**: 機能更新プログラムを遅延させる日数を指定します。 これらの機能更新プログラムの受け取りは、リリースから 180 日間遅延させることができます。
    - **[品質更新プログラムの一時停止の開始]**: デバイスでの品質更新プログラムの受け取りを一時停止するかどうかを選択します。一時停止の期間は最大 35 日間です。 最大日数が経過すると、一時停止機能は自動的に期限切れとなり、デバイスは適用可能な更新を確認するために Windows Update をスキャンします。 このスキャンが終ったら、もう一度更新を一時停止することができます。 品質更新プログラムの一時停止を解除するには、チェック ボックスをオフにします。
6. **[他の Microsoft 製品の更新プログラムのインストール]** を選択して、遅延の設定を Microsoft Update と Windows Update に適用可能にするグループ ポリシー設定を有効にします。
7. **[Include drivers with Windows Update]\(ドライバーと Windows Update を含める\)** を選択して、Windows Update から自動的にドライバーを更新します。 この設定をオフにすると、Windows Update からドライバーの更新プログラムがダウンロードされません。
8. ウィザードを完了して新しいコレクションを作成します。

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Windows Update for Business 遅延ポリシーを展開するには
1. **[ソフトウェア ライブラリ]** > **[Windows 10 のサービス]** > **[Windows Update for Business ポリシー]** に移動します。
2. **[ホーム]** タブの **[展開]** グループで、**[Windows Update for Business ポリシーを展開する]** を選択します。
3. 次の設定を構成します。
    - **[展開する構成ポリシー]**: 展開する Windows Update for Business ポリシーを選択します。
    - **[コレクション]**: **[参照]** をクリックして、ポリシーを展開するコレクションを選択します。
    - **[サポートされている場合は対応していない規則を修復する]**: 選択すると、Windows Management Instrumentation (WMI)、レジストリ、スクリプト、および、Configuration Manager が登録したモバイル デバイスのすべての設定が対応しない規則があれば、自動的に修復します。
    - **[メンテナンス期間以外の修復を許可する]**: ポリシーの展開先のコレクションにメンテナンス期間が設定されている場合、このオプションを有効にすると、コンプライアンス設定によって、メンテナンス期間外に値を修復できます。 メンテナンス期間について詳しくは、「[メンテナンス期間を使用する方法](/sccm/core/clients/manage/collections/use-maintenance-windows)」を参照してください。
    - **[アラートを生成する]**: 構成基準のコンプライアンスが、指定した日付と時刻までに指定した割合に達しなかった場合に生成されるアラートを構成します。 アラートを System Center Operations Manager に送信するかどうかも指定できます。
    - **[ランダム遅延 (時間)]**: ネットワーク デバイス登録サービスで処理量が過度にならないように、遅延期間を指定します。 既定値は 64 時間です。
    - **[スケジュール]**: 展開されたプロファイルをクライアント コンピューターで評価するコンプライアンス評価スケジュールを指定します。 単純なスケジュールとカスタム スケジュールの 2種類あります。 プロファイルは、ユーザーがログオンしたときにクライアント コンピューターによって評価されます。
4.  ウィザードを完了してプロファイルを展開します。

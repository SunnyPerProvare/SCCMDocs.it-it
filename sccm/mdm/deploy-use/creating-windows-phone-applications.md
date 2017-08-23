---
title: "Windows Phone アプリケーションの作成 | Microsoft Docs"
description: "Windows Phone デバイス用アプリケーションを作成して展開するときに検討する必要がある考慮事項について説明します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68fe11fa-5fb2-4b81-b0f5-b6f2392fb4ad
caps.latest.revision: "10"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 6cbf2389a72c0c384ef8e84a1755ac77b64bfc6d
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="create-windows-phone-applications-with-system-center-configuration-manager"></a>System Center Configuration Manager で Windows Phone アプリケーションを作成する

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager アプリケーションには、デバイスにソフトウェアを展開するために必要なインストール ファイルと情報からなる、1 つまたは複数の展開の種類があります。 また、展開の種類には、ソフトウェアを展開するタイミングと方法を指定する規則があります。  

 アプリケーションを作成するには、次の 2 通りの方法があります。  

-   アプリケーション インストール ファイルを読み取って、アプリケーションおよび展開の種類を自動的に作成する。  

-   アプリケーションを手動で作成してから、後で展開の種類を追加する。  

-   アプリケーションをファイルからインポートする。  

Configuration Manager アプリケーションと展開の種類の作成に必要な手順については、「[アプリケーションの作成ウィザードを開始する](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard)」を参照してください。 また、Windows Phone デバイス用アプリケーションを作成して展開するときは、以下の考慮事項について留意してください。  

## <a name="general-considerations"></a>一般的な考慮事項  
 Configuration Manager では、次のアプリ ファイルの種類の展開がサポートされています。  

|デバイスの種類|サポートされているファイルの種類|  
|-----------------|---------------------|  
|Windows Phone 8|.xap|  
|Windows Phone 8.1|.xap、.appx、.appxbundle|
|Windows 10 Mobile|.xap、.appx、.appxbundle|

 次の展開操作がサポートされています。  

|デバイスの種類|サポートされている操作|  
|-----------------|-----------------------|  
|Windows Phone 8、Windows Phone 8.1、および Windows 10 Mobile|利用可能、必須、アンインストール|  

## <a name="steps-to-deploy-the-latest-windows-phone-company-portal-app-with-supersedence"></a>最新の Windows Phone 会社ポータル アプリケーションに置き換え関係を展開する手順  
 次の表に、Windows Phone 8 用の最新の会社ポータル アプリケーションを作成する手順とその簡単な説明、および関連情報のある場所へのリンクをまとめます。  

|手順|説明|  
|----------|----------------------|  
|**ステップ 1:** 最新の会社ポータル アプリケーションを取得する。|[Windows Phone 8 ポータル サイト アプリ](http://go.microsoft.com/fwlink/?LinkId=268440)をダウンロードします。|  
|**ステップ 2:** 会社ポータル アプリケーションに、Symantec 証明書を使って署名する。|ポータル サイト アプリに署名する方法については、「[System Center Configuration Manager と Microsoft Intune による Windows Phone および Windows 10 Mobile のハイブリッドのデバイス管理のセットアップ](../../mdm/deploy-use/enroll-hybrid-windows.md)」を参照してください。|  
|**ステップ 3:** 最新バージョンの会社ポータルアプリケーションを含む新しいアプリケーションを作成して置き換え関係を指定する。|詳細については、「[アプリケーションの作成](../../apps/deploy-use/create-applications.md)」と「[アプリケーションを修正して置き換える方法](../../apps/deploy-use/revise-and-supersede-applications.md)」を参照してください。|  
|**ステップ 4:** Microsoft Intune サブスクリプションの作成ウィザードでアプリケーションを追加する。|詳細については、「[System Center Configuration Manager と Microsoft Intune による Windows Phone および Windows 10 Mobile のハイブリッドのデバイス管理のセットアップ](../../mdm/deploy-use/enroll-hybrid-windows.md)」を参照してください。|  
|**ステップ 5:** Microsoft Intune サブスクリプションの作成ウィザードで会社ポータル アプリケーションを追加したときに自動的に作成された展開を削除する。|Microsoft Intune のサブスクリプションによって、このアプリケーションの展開が自動的に作成されますが、この展開には置き換えを設定できないので削除します。|  
|**手順 6:**アプリケーションの新しい展開を作成する。 **ソフトウェアの展開ウィザード**の [**展開設定**] ページで [**このアプリケーションの置き換えられるバージョンを自動的にアップグレードする**] チェック ボックスをオンにします。|置き換え関係を設定して作成したアプリケーションの新しい展開を作成します。|  
|**ステップ 7 (オプション):** 既定では、置き換えるアプリケーションがデバイスに 7 日後にインストールされる。 登録済みデバイスに、これより早く会社ポータル アプリケーションを展開したい場合は、[**展開の再評価スケジュールを指定する**] を小さな値に設定します。<br /><br /> この値を既定値より小さくすると、ネットワークとクライアント コンピューターのパフォーマンスが低下する可能性があります。|詳細情報はありません。|  

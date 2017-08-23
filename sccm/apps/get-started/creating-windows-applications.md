---
title: "Windows アプリケーションの作成 | Microsoft Docs"
description: "Windows デバイス用アプリケーションを作成して展開するときに検討する必要がある考慮事項について説明します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9181c84e-d74f-44ea-9bb9-f7805eb465fc
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 9c80cc42f9ce6775067a89a9f5a63c1bf4a0c7ca
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="create-windows-applications-with-system-center-configuration-manager"></a>System Center Configuration Manager で Windows アプリケーションを作成する

*適用対象: System Center Configuration Manager (Current Branch)*

アプリケーションを作成するための System Center Configuration Manager の他の要件と手順に加えて、Windows デバイス用アプリケーションを作成および展開するときには次の考慮事項について検討する必要があります。  

## <a name="general-considerations"></a>一般的な考慮事項  
 Configuration Manager では、次のアプリ ファイルの種類の展開がサポートされています。  

|デバイスの種類|サポートされているファイルの種類|  
|-----------------|---------------------|  
|Windows RT および Windows RT 8.1|*.appx、\*.appxbundle|  
|モバイル デバイスとして登録された Windows 8.1 以降|*.appx、\*.appxbundle|  

 次の展開操作がサポートされています。  

|デバイスの種類|サポートされている操作|  
|-----------------|-----------------------|  
|Windows 8.1 以降|利用可能、必須、アンインストール|  
|Windows RT|利用可能、必須、アンインストール|  

## <a name="support-for-universal-windows-platform-uwp-apps"></a>ユニバーサル Windows プラットフォーム (UWP) アプリのサポート  
 Windows 10 デバイスで基幹業務アプリをインストールする場合、サイドローディング キーは不要です。 ただし、サイドローディングを有効にするため、レジストリ キー **HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Appx\AllowAllTrustedApps** の値は 1 である必要があります。  

 このレジストリ キーが構成されていない場合は、アプリをデバイスに初めて展開する際に、Configuration Manager によってこの値が自動的に **1** に設定されます。 この値を **0**に設定した場合、Configuration Manager は値を自動的には変更することができず、基幹業務アプリの展開は失敗します。  

 ユニバーサル Windows プラットフォームの基幹業務アプリは、アプリが展開される各デバイス上で信頼されているコード署名証明書で署名される必要があります。 社内の PKI 基盤からの証明書を使用することも、デバイスにインストールされたサード パーティのパブリック ルート証明書からの証明書を使用することもできます。  

 Windows 10 Mobile デバイス上では、Symantec 以外のコード署名証明書を使用して、ユニバーサル **.appx** アプリに署名することができます。 **.xap** アプリの場合、また Windows 10 Mobile デバイスにインストールする Windows Phone 8.1 用にビルドされた **.appx** パッケージの場合は、Symantec コード署名証明書を使用する必要があります。  

## <a name="deploy-windows-installer-apps-to-enrolled-windows-10-pcs"></a>登録済みの Windows 10 PC に Windows インストーラー アプリを展開する  
 **MDM を介した Windows インストーラー (\*.msi)** のインストーラーの種類では、Windows インストーラー ベースのアプリを作成して、Windows 10 を実行する登録済み PC に展開できます。  

 このインストーラーの種類を使用する場合は、次の点を考慮してください。  

-   拡張子が .msi のファイルを 1 つだけアップロードできます。  

-   アプリの検出では、ファイルの製品コードと製品バージョンが使用されます。  

-   アプリの既定の再起動動作が使用されます。 Configuration Manager はこれを制御しません。  

-   ユーザー単位の MSI パッケージは単一のユーザーにインストールされます。  

-   コンピューター単位の MSI パッケージはデバイス上のすべてのユーザーにインストールされます。  

-   アプリの更新プログラムは、各バージョンの MSI 製品コードが同じである場合にサポートされます。  

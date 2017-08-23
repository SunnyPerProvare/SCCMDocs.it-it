---
title: "iOS アプリケーションの作成 | Microsoft Docs"
description: "iOS デバイス用アプリケーションを作成して展開するときに検討する必要がある考慮事項について説明します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff633013-5313-4cd3-949c-56d45e777280
caps.latest.revision: "10"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 349fcf335e7faddbcbd2ffe0ece7e711465f28df
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="create-ios-applications-with-system-center-configuration-manager"></a>System Center Configuration Manager で iOS アプリケーションを作成する

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager アプリケーションには、デバイスにソフトウェアを展開するために必要なインストール ファイルと情報からなる、1 つまたは複数の展開の種類があります。 また、展開の種類には、ソフトウェアを展開するタイミングと方法を指定する規則があります。  

 アプリケーションを作成するには、次の 2 通りの方法があります。  

-   アプリケーション インストール ファイルを読み取って、アプリケーションおよび展開の種類を自動的に作成する。  

-   アプリケーションを手動で作成してから、後で展開の種類を追加する。  

-   アプリケーションをファイルからインポートする。  

Configuration Manager アプリケーションと展開の種類の作成に必要な手順については、「[アプリケーションの作成ウィザードを開始する](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard)」を参照してください。 また、iOS デバイス用アプリケーションを作成して展開するときは、以下の考慮事項について留意してください。  

## <a name="general-considerations"></a>一般的な考慮事項  
 Configuration Manager では、次のアプリの種類の展開がサポートされています。  

|デバイスの種類|サポートされているファイル|  
|-----------------|---------------------|  
|iOS|*.ipa<br /><br /> System Center Configuration Manager では、iOS アプリをインポートするときに、プロパティ一覧 (.plist) ファイルを指定する必要はありません。|  

 次の展開操作がサポートされています。  

|デバイスの種類|サポートされている操作|  
|-----------------|-----------------------|  
|iOS|**利用可能**、**必須**。 インストールとアンインストールの両方に、ユーザーが同意する必要があります。

> [!IMPORTANT]  
>  現在、エンド ユーザーは iOS 向け Microsoft Intune 会社ポータル アプリから会社のアプリをインストールできません。 これは、iOS App Store に公開されたアプリに設けられた制限によるものです (「App Store レビューに関するガイドライン」の第 2 節をご覧ください)。 ユーザーが会社アプリ (管理されている App Store アプリ、基幹業務アプリ パッケージなど) をインストールするには、自身のデバイスで Intune Web ポータルを参照する必要があります (portal.manage.microsoft.com)。 Intune ポータル サイト アプリで有効化されるモバイル管理機能について詳しくは、「[Microsoft Intune の登録済みデバイス管理機能](https://technet.microsoft.com/library/dn600287.aspx)」をご覧ください。  

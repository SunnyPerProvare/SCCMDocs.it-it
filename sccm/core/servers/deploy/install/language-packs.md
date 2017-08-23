---
title: "言語パック | Microsoft Docs"
description: "System Center Configuration Manager で使用できる言語サポートについて説明します。"
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
caps.latest.revision: "10"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 47da3c531289ddf13d357bde8bbda85d79ed2803
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="language-packs-in-system-center-configuration-manager"></a>System Center Configuration Manager の言語パック

*適用対象: System Center Configuration Manager (Current Branch)*

このトピックでは、System Center Configuration Manager の言語サポートの技術的な詳細情報について説明します。  

## <a name="BKMK_SupLanguagePacks"></a> サポートされるオペレーティング システム言語  
 中央管理サイトおよびプライマリ サイトに **サーバー言語パック** または **クライアント言語パック** をインストールすることで、次の表の表示言語のサポートをインストールできます。 サイトのインストール中、そのサイトでサポートするサーバーとクライアントの言語を利用可能な言語パック ファイルから選びます。

 前提条件かつ再配布可能なファイル ダウンロードの一部としてセットアップを実行するときに、言語パック ファイルがダウンロードされます。 [セットアップ ダウンローダー](setup-downloader.md)を使用して、セットアップを実行する前にこれらのファイルをダウンロードできます。   

 次の表を参照して、サーバーまたはクライアント クライアントでサポートする言語にロケール ID をマッピングしてください。 ロケール ID の詳細については、「[Locale IDs Assigned by Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=252609)」 (Microsoft による割り当て済みロケール ID) を参照してください。  

### <a name="server-languages"></a>サーバーの言語  

|サーバーの言語|ロケール ID (LCID)|3 文字コード|  
|---------------------|------------------------|-----------------------|  
|英語 (既定)|0409|ENU|  
|中国語 (繁体字、香港特別行政区)|0c04|ZHH|  
|中国語 (簡体字)|0804|CHS|  
|中国語 (繁体字、台湾)|0404|CHT|  
|チェコ語|0405|CSY|  
|オランダ語 - オランダ|0413|NLD|  
|フランス語|040c|FRA|  
|ドイツ語|0407|DEU|  
|ハンガリー語|040e|HUN|  
|イタリア語 - イタリア|0410|ITA|  
|日本語|0411|JPN|  
|韓国語|0412|KOR|  
|ポーランド語|0415|PLK|  
|ポルトガル語 - ブラジル|0416|PTB|  
|ポルトガル語 - ポルトガル|0816|PTG|  
|ロシア語|0419|RUS|  
|スペイン語 - スペイン|0c0a|ESN|  
|スウェーデン語|041d|SVE|  
|トルコ語|041f|TRK|  

### <a name="client-languages"></a>クライアントの言語  

|クライアントの言語|ロケール ID (LCID)|3 文字コード|  
|---------------------|------------------------|-----------------------|  
|英語 (既定)|0409|ENG|  
|中国語 (繁体字、香港特別行政区)|0c04|ZHH|  
|中国語 - 簡体字|0804|CHS|  
|中国語 (繁体字、台湾)|0404|CHT|  
|チェコ語|0405|CSY|  
|デンマーク語|0406|DAN|  
|オランダ語 - オランダ|0413|NLD|  
|フィンランド語|040b|FIN|  
|フランス語|040c|FRA|  
|ドイツ語|0407|DEU|  
|ギリシャ語|0408|ELL|  
|ハンガリー語|040e|HUN|  
|イタリア語 - イタリア|0410|ITA|  
|日本語|0411|JPN|  
|韓国語|0412|KOR|  
|ノルウェー語|0414|NOR|  
|ポーランド語|0415|PLK|  
|ポルトガル語 (ブラジル)|0416|PTB|  
|ポルトガル語 (ポルトガル)|0816|PTG|  
|ロシア語|0419|RUS|  
|スペイン語 - スペイン|0c0a|ESN|  
|スウェーデン語|041d|SVE|  
|トルコ語|041f|TRK|  

### <a name="mobile-device-client-languages"></a>モバイル デバイス クライアントの言語  
 モバイル デバイスの言語のサポートを追加する場合、サポートされるすべてのモバイル デバイス クライアントの言語が含まれます。 モバイル デバイスをサポートするために個々の言語パックを選択することはできません。  

### <a name="identify-installed-language-packs"></a>インストール済みの言語パックを特定する  
Configuration Manager クライアントを実行するコンピューターにインストールされている言語パックを特定するには、コンピューターのレジストリで、インストール済み言語パックのロケール ID (LCID) を確認します。 この情報は次の場所にあります。

 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs**  

ハードウェア インベントリを使用してこの情報を収集し、カスタム レポートを作成して言語の詳細情報を確認することができます。 カスタム ハードウェア インベントリを収集する方法については、「[How to configure hardware inventory in System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md)」(System Center Configuration Manager でハードウェア インベントリを構成する方法) を参照してください。 レポートの作成の詳細については、「[Operations and maintenance for reporting in System Center Configuration Manager](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md)」(System Center Configuration Manager のレポートの操作とメンテナンス) トピックの「[Manage Configuration Manager reports](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md#BKMK_ManageReports)」(Configuration Manager レポートの管理) セクションを参照してください。  

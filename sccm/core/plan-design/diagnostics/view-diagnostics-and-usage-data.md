---
title: "診断データの表示 | Microsoft Docs"
description: "診断および使用状況データを表示して、System Center Configuration Manager 階層に機密情報が含まれていないことを確認します。"
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 594eb284-0d93-4c5d-9ae6-f0f71203682a
caps.latest.revision: "8"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 0932e2b2a4f3e13c35d6b7b0446083f1c233ce03
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-view-diagnostics-and-usage-data-for-system-center-configuration-manager"></a>System Center Configuration Manager の診断および使用状況データを表示する方法

*適用対象: System Center Configuration Manager (Current Branch)*

診断および使用状況データを System Center Configuration Manager 階層から表示して、機密情報や個人情報が含まれていないことを確認できます。 利用統計情報のデータは要約され、サイト データベースの **TEL_TelemetryResults** テーブルに保存されます。このデータは、プログラムで使用できる効率的な形式に設定されます。 次のオプションでは Microsoft に送信されたデータが正確に表示されますが、このデータは、データ分析など、別の目的で使用することを意図したものではありません。  

このテーブルの内容を表示し、送信される正確なデータを表示するには、次の SQL コマンドを使用します  (このデータをテキスト ファイルにエクスポートすることもできます)。  

-   **SELECT \* FROM TEL_TelemetryResults**  

> [!NOTE]  
>  バージョン 1602 のインストール前に製品利用統計情報データを格納するテーブルは **TelemetryResults**です。  

サービス接続ポイントがオフライン モードの場合は、サービス接続ツールを使用して、現在の診断および使用状況データをコンマ区切り値 (CSV) ファイルにエクスポートできます。 サービス接続ポイントで **-Export** パラメーターを使用してサービス接続ツールを実行します。  

##  <a name="bkmk_hashes"></a> 一方向のハッシュ  
一部のデータは、任意の英数字の文字列で構成されています。 Configuration Manager は、一方向のハッシュを使用する SHA-256 アルゴリズムを使用して、機密データを収集していないことを確認します。 このアルゴリズムでは、収集と比較を目的として引き続きデータを使用できる状態にデータが維持されます。 たとえば、サイト データベースのテーブルの名前を収集するのではなく、テーブル名ごとに一方向のハッシュがキャプチャされます。 これにより、ユーザーが作成したカスタム テーブル名や、他社の製品のアドオンが非表示になります。 その後、製品に既定で付属している SQL テーブルの名前に対して同じ一方向のハッシュを行い、2 つのクエリの結果を比較して、ユーザーのデータベース スキーマと製品の既定値の差異を確認します。 これは、SQL スキーマへの変更が必要な更新プログラムの向上に役立てられます。  

生データを表示するときには、共通のハッシュ値がデータの各行に表示されます。 これは階層 ID です。 このハッシュ値は、顧客またはソースを特定せずに、同じ階層内のデータを関連付けるのに使用されます。  

#### <a name="to-see-how-the-one-way-hash-works"></a>一方向のハッシュの動作を確認するには  

1.  SQL Management Studio で、Configuration Manager データベースに対して、SQL ステートメント **select [dbo].[fnGetHierarchyID]\(\)** を実行して、階層 ID を取得します。  

2.  以下の Windows PowerShell スクリプトを使用して、データベースから取得した GUID の一方向のハッシュを実行します。 これをデータ階層 ID と比較して、このデータを分かり難くする方法を確認できます。  

    ```  
    Param( [Parameter(Mandatory=$True)] [string]$value )  
      $guid = [System.Guid]::NewGuid()  
      if( [System.Guid]::TryParse($value,[ref] $guid) -eq $true ) {  
      #many of the values we hash are Guids  
      $bytesToHash = $guid.ToByteArray()  
    } else {  
      #otherwise hash as string (unicode)  
      $ue = New-Object System.Text.UnicodeEncoding  
      $bytesToHash = $ue.GetBytes($value)   
    }  
      # Load Hash Provider (https://en.wikipedia.org/wiki/SHA-2)   
    $hashAlgorithm = [System.Security.Cryptography.SHA256Cng]::Create()    
    # Hash the input   
    $hashedBytes = $hashAlgorithm.ComputeHash($bytesToHash)              
    # Base64 encode the result for transport   
    $result = [Convert]::ToBase64String($hashedBytes)    
    return $result   
    ```  

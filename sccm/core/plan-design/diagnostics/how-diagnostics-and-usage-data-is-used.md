---
title: "診断データの使用 | Microsoft Docs"
description: "System Center Configuration Manager により収集された診断と使用状況データを Microsoft が使用する方法について説明します。"
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 9864f6ba7b9a2211c99b1a5d9ebd582e01ccfeb6
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="how-diagnostics-and-usage-data-is-used-for-system-center-configuration-manager"></a>System Center Configuration Manager での診断結果と使用状況データの使用方法

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager で収集される診断結果と使用状況データは、製品がどのように動作しているかに関するフィードバックを Microsoft に直ちに示し、今後の更新プログラムの調整に使用されます。 また、運用環境における構成を設計およびテストする際に役立つ構成データを確認することもできます。 たとえば、  

-   サイト サーバーが使用している Windows サーバーのバージョン  

-   インストール済みの言語パック  

-   製品の既定値に対する SQL スキーマのデルタ  

このデータによってエンジニアリング チームは、最も一般的な構成の下で最適なエクスペリエンスを確保できるように今後のテストを計画できます。 Configuration Manager の更新プログラムは、(Windows 10、Microsoft Intune など、変化の速いテクノロジを適切にサポートするために) 頻繁にリリースされます。これに合わせて迅速に調整するには、このデータが欠かせません。  

同じくらい重要なのが診断結果と使用状況データが使用されないケースです。 Microsoft は、次に対してこのデータを使用しません。  

-   使用許諾契約に対する顧客の使用状況の比較などのライセンスの監査  

-   サポート外の製品の監査  

-   機能の使用状況や地理的位置情報 (タイム ゾーン) などの利用可能なデータに基づいた広告  

##  <a name="bkmk_improve"></a> 診断結果と使用状況データが製品を向上させる方法の例  
Microsoft では、製品を向上させるために、使用可能なデータを使用します。 例を次にいくつか示します。  

-   **古いサーバーのオペレーティング システムの変更されるサポート:**  

     System Center Configuration Manager の現在のブランチで提供される初期のサポートでは、Windows Server 2008 R2 のサポート タイムラインが制限されていました。 Configuration Manager の現在のブランチにアップグレードした顧客からの使用状況データを調べた後、サイト サーバーとサイト システムの役割をホストするためにこのサーバーのオペレーティング システムを引き続き使用する顧客をサポートするために、このタイムラインを変更して拡張する必要があることがわかりました。  

-   **改良された前提条件の確認:**  

     使用状況データに基づいて、古いルール、追加のケースのアカウント、および場合によっては、自動修復のいくつかの問題を削除する更新プログラムをインストールするための前提条件の確認を改良しました。  

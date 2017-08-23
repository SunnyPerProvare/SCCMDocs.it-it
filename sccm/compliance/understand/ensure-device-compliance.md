---
title: "デバイス コンプライアンスの確認 | Microsoft Docs"
description: "System Center Configuration Manager を使用して、組織内のデバイスの構成とコンプライアンスを管理します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7568c9aa-b99e-4466-bfc8-0301aa376930
caps.latest.revision: "8"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: f7ecfe550d2e28579ea873442b2a68dc1c7c5483
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="ensure-device-compliance-with-system-center-configuration-manager"></a>System Center Configuration Manager でのデバイス コンプライアンスの確認

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager でのコンプライアンス設定は、組織内のデバイスの構成とコンプライアンスを管理するために必要なツールおよびリソースとなります。 これを利用することで、次の業務要件をサポートできます。  

-   管理対象の Windows PC、Mac コンピューター、サーバー、およびモバイル デバイスを、独自に作成したベスト プラクティス構成または他のベンダーから取得したベスト プラクティス構成と比較対照する  

-   承認されていないデバイス構成を特定する  

-   規制に基づくポリシーおよび社内のセキュリティ ポリシーの対応状態を報告する  

-   セキュリティの脆弱性を識別する  

-   非準拠の構成を識別することで、報告されたインシデントや問題の考えられる原因を検出するための情報をヘルプ デスクに提供する  

-   モバイル デバイスの非準拠の設定を自動的に修復する  

-   非準拠であることが報告されたデバイスが自動的に加えられるコレクションに対して、アプリケーション、パッケージとプログラム、またはスクリプトを展開して、非準拠を修復する  


## <a name="get-started"></a>作業開始  
 コンプライアンス設定の基本事項およびそれらで実行できるタスクについて説明します。  

 [コンプライアンス設定を使ってみる](../../compliance/get-started/get-started-with-compliance-settings.md)  

## <a name="plan-and-design"></a>計画と設計  
 コンプライアンス設定での作業を開始する前に、このトピックで必要な前提条件を実施しておきます。  

 [コンプライアンス設定の計画と構成](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)  

## <a name="common-tasks"></a>一般的なタスク  
 このセクションでは、Configuration Manager でのコンプライアンス設定の使用方法に関するいくつかの一般的なシナリオを紹介します。  

 [コンプライアンスを管理するための一般的なタスク](../../compliance/plan-design/common-tasks-for-managing-compliance.md)  

## <a name="remote-connection-profiles"></a>リモート接続プロファイル  
 この構成項目の種類を使用すると、ユーザーがドメインに接続されていない場合やユーザーの PC がインターネット経由で接続されている場合に、会社用のコンピューターにリモート接続するようにユーザーの PC を構成できます。  

 [リモート接続プロファイルの作成](/sccm/compliance/deploy-use/create-remote-connection-profiles)  

## <a name="user-data-and-profiles"></a>ユーザー データとプロファイル  
 この構成項目の種類には、階層内のユーザーの Windows 8 以降のコンピューターのフォルダー リダイレクト、オフライン ファイル、およびローミング プロファイルを管理できる設定が含まれています。  

 [ユーザー データとプロファイルの構成項目の作成](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items)  

## <a name="windows-edition-upgrade-policy"></a>Windows エディションのアップグレード ポリシー  
 エディションのアップグレード ポリシーでは、新しいバージョンに Windows 10 デバイスを自動的にアップグレードできます。 Windows 10 デスクトップ バージョンをアップグレードするためのプロダクト キーを指定したり、Windows 10 Mobile と Windows 10 Holographic を実行しているデバイスをアップグレードするために使用できるライセンス ファイルを指定したりできます。  

 [エディションのアップグレード ポリシーで Windows デバイスをアップグレードする](/sccm/compliance/deploy-use/upgrade-windows-version)  

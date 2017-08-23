---
title: "展開先のコンピューターにユーザーを関連付ける | Microsoft Docs"
description: "オペレーティング システムを展開するときに、ユーザーをセットアップ先のコンピューターと関連付けるように、System Center Configuration Manager を構成します。"
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 07c3c6d9-f056-4c4d-bc70-ede5ca933807
caps.latest.revision: "9"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: c0331567b94a99b29cc73c16de17a9f3bc6b9e43
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="associate-users-with-a-destination-computer-in-system-center-configuration-manager"></a>System Center Configuration Manager でユーザーをセットアップ先のコンピューターに関連付ける

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager を使ってオペレーティング システムを展開するときに、ユーザーを、オペレーティング システムの展開先のコンピューターに関連付けることができます。 この構成には、次の事柄が含まれます。  

-   単一ユーザーが展開先コンピューターのプライマリ ユーザーであること  

-   複数ユーザーが展開先コンピューターのプライマリ ユーザーであること  

 ユーザーとデバイスのアフィニティは、アプリケーションを展開するときにユーザー中心の管理をサポートします。 オペレーティング システムをインストールするセットアップ先のコンピューターにユーザーを関連付けると、後でそのユーザーにアプリケーションを展開することにより、セットアップ先のコンピューターにアプリケーションが自動的にインストールされるようになります。 ただし、オペレーティング システムを展開するときにユーザーとデバイスのアフィニティのサポートを構成することはできますが、ユーザーとデバイスのアフィニティを使ってオペレーティング システムを展開することはできません。  

 ユーザーとデバイスのアフィニティの詳細については、「[ユーザーとデバイスのアフィニティへのユーザーとデバイスの関連付け](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)」をご覧ください。  

## <a name="how-to-specify-a-user-when-you-deploy-operating-systems"></a>オペレーティング システムを展開するときにユーザーを指定する方法  
 次の表に、ユーザーとデバイスのアフィニティをオペレーティング システムの展開に統合するときに実行できる操作を示します。 ユーザーとデバイスのアフィニティは、PXE 展開、起動可能なメディアの展開、事前設定されたメディアの展開に統合することができます。  

|操作|説明|  
|------------|----------------------|  
|**SMSTSAssignUsersMode** 変数を含むタスク シーケンスを作成する|**Set Task Sequence Variable** のタスク シーケンスの手順に沿って、タスク シーケンスの最初に  [SMSTSAssignUsersMode](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) 変数を追加します。 この変数は、タスク シーケンスでのユーザー情報の処理方法を指定します。<br /><br /> 変数に次のいずれかの値を設定します。<br /><br /> <br /><br /> **自動**:タスク シーケンスが自動的にユーザーと展開先コンピューターの関係を作成し、オペレーティング システムを展開します。<br /><br /> **保留中**:タスク シーケンスは、ユーザーと展開先コンピューターの関係を作成しますが、オペレーティング システムを展開する前に管理ユーザーの承認を待ちます。<br /><br /> **無効**:タスク シーケンスは、ユーザーを展開先コンピューターに関連付けずに、オペレーティング システムの展開を続行します。<br /><br /> <br /><br /> この変数は、コンピューターまたはコレクションにも設定することができます。 組み込み変数の詳細については、「[タスク シーケンス組み込み変数](../../osd/understand/task-sequence-built-in-variables.md)」をご覧ください。|  
|ユーザー情報を収集する起動前コマンドを作成する|起動前コマンドは、入力ボックスのある Visual Basic (VB) スクリプト、または、入力されたユーザー データを検証する HTML アプリケーション (HTA) です。<br /><br /> 起動前コマンドには、タスク シーケンスの実行時に使用される **SMSTSUdaUsers** 変数を設定する必要があります。 この変数は、コンピューター、コレクション、あるいはタスク シーケンスの変数にも設定することができます。 複数のユーザー ( *domain\user1、domain\user2、domain\user3*) を追加するときには、次の形式を使用します。|  
|配布ポイントとメディアによるユーザーと展開先コンピューターの関連付けを構成する|[配布ポイントが PXE ブート要求を受け入れるように構成し](https://technet.microsoft.com/library/mt627944\(TechNet.10\).aspx#BKMK_PXEDistributionPoint) 、 [起動可能なメディア](http://technet.microsoft.com/library/mt627921\(TechNet.10\).aspx) や [事前設定されたメディア](https://technet.microsoft.com/library/mt627922\(TechNet.10\).aspx) をタスク シーケンス メディアの作成ウィザードを使って作成する場合、配布ポイントやメディアが、ユーザーとオペレーティング システムのセットアップ先のコンピューターとの関連付けをどのようにサポートするかを指定できます。<br /><br /> ユーザーとデバイスのアフィニティのサポートの構成には、ユーザー ID を検証する方法は組み込まれていません。 このことは、技術者がコンピューターをプロビジョニングするときに、ユーザーに代わって情報を入力するときに重要になります。 タスク シーケンスによるユーザー情報の処理方法の設定に加えて、配布ポイントとメディアにこれらのオプションを構成することで、PXE ブートや特定の種類のメディアからの展開開始を制限することができます。|  

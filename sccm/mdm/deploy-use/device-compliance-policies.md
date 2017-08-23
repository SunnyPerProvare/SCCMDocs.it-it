---
title: "デバイス コンプライアンス ポリシー | Microsoft Docs"
description: "デバイスが条件付きアクセス ポリシーに準拠するように System Center Configuration Manager でコンプライアンス ポリシーを管理する方法について説明します。"
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ad8fa94d-45bb-4c94-8d86-31234c5cf21c
caps.latest.revision: "18"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: bcaa2a9b5474e06bf344dc4fd47dbb160ea36297
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2017
---
# <a name="device-compliance-policies-in-system-center-configuration-manager"></a>System Center Configuration Manager でのデバイス コンプライアンス ポリシー

*適用対象: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager の**コンプライアンス ポリシー**では、デバイスが条件付きアクセス ポリシーに準拠していると見なされるために遵守する必要があるルールと設定を定義します。 コンプライアンス ポリシーを使用して、条件付きアクセスとは別に、デバイスのコンプライアンスに関する問題を監視および修復することもできます。  


> [!IMPORTANT]  
>  この記事では、Microsoft Intune によって管理されるデバイスのコンプライアンス ポリシーについて説明します。    System Center Configuration Manager の管理対象 PC のコンプライアンス ポリシーについては、「[Manage access to O365 services for PCs managed by System Center Configuration Manager (System Center Configuration Manager の管理対象 PC の O365 サービスへのアクセス管理)](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)」に説明されています。  

 これらのルールには、次のような要件が含まれます。  

-   デバイスにアクセスするための PIN とパスワード

-   デバイスに格納されたデータの暗号化

-   デバイスが脱獄またはルート化されているかどうか  

-   デバイス上の電子メールが Intune のポリシーで管理されるかどうか、または Windows デバイスの正常性構成証明サービスでデバイスが異常であると報告されたかどうか
-   デバイスにインストールできないアプリ。


 コンプライアンス ポリシーをユーザー コレクションに展開します。 コンプライアンス ポリシーがユーザーに展開されると、すべてのユーザー デバイスがコンプライアンスをチェックされます。  

 次の表は、コンプライアンス ポリシーによってサポートされているデバイスの種類と、ポリシーが条件付きアクセス ポリシーと共に使用される場合に非準拠設定がどのように管理されるかを示した一覧です。  

|規則|Windows 8.1 以降|Windows Phone 8.1 以降|iOS 6.0 以降|Android 4.0 以降、Samsung KNOX Standard 4.0 以降、Android for Work|  
|----------|---------------------------|---------------------------------|-----------------------|---------------------------|-----------------------------------------|  
|**PIN またはパスワードの構成**|修復|修復|修復|検疫済み|  
|**デバイスの暗号化**|該当なし|修復|修復 (PIN の設定による)|検疫済み<br>(Android for Work は常に暗号化)|  
|**脱獄またはルート化されたデバイス**|該当なし|該当なし|検疫済み (設定ではありません)|検疫済み (設定ではありません)|  
|**電子メールのプロファイル**|該当なし|該当なし|検疫済み|該当なし|  
|**最小 OS バージョン**|検疫済み|検疫済み|検疫済み|検疫済み|  
|**最大 OS バージョン**|検疫済み|検疫済み|検疫済み|検疫済み|  
|**デバイス正常性構成証明 (1602 更新プログラム)**|設定を Windows 8.1 に適用できません<br /><br /> Windows 10 および Windows 10 Mobile は検疫されます。|該当なし|該当なし|該当なし|  
|**アプリをインストールすることはできません。**|該当なし|該当なし|検疫済み|検疫済み|

 **修復** = デバイスのオペレーティング システムによってコンプライアンスが適用されます (たとえば、PIN の設定を求められます)。  設定が非準拠となる場合はありません。  

 **検疫済み** = デバイスのオペレーティング システムはコンプライアンスを適用しません (たとえば、Android デバイスはユーザーにデバイスの暗号化を求めません)。  この場合、次のようになります。  

-   ユーザーが条件付きアクセス ポリシーの対象となる場合は、デバイスがブロックされます。  

-   ポータル サイトまたは Web ポータルは、コンプライアンスの問題をユーザーに通知します。  


### <a name="next-steps"></a>次のステップ  
[デバイス コンプライアンス ポリシーを作成して展開する](create-compliance-policy.md)
### <a name="see-also"></a>関連項目  
 [System Center Configuration Manager でサービスへのアクセスを管理する](../../protect/deploy-use/manage-access-to-services.md)

---
title: Profili VPN in System Center Configuration Manager | Microsoft Docs
description: Di seguito viene illustrato come usare i profili VPN in System Center Configuration Manager per distribuire impostazioni VPN agli utenti dell&quot;organizzazione.
ms.custom: na
ms.date: 11/27/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
caps.latest.revision: 6
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: f9097014c7e988ec8e139e518355c4efb19172b3
ms.openlocfilehash: c11440556abc11d2c19ee0ff3c2bc9e518951e49
ms.contentlocale: it-it
ms.lasthandoff: 03/04/2017


---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>Profili VPN in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


Usare i profili VPN in System Center Configuration Manager (noto anche come ConfigMgr o SCCM) per distribuire impostazioni VPN agli utenti dell'organizzazione. La distribuzione di queste impostazioni consente di ridurre al minimo le operazioni che l'utente finale deve eseguire per connettersi alle risorse nella rete aziendale.  

 Si supponga, ad esempio, di voler effettuare il provisioning, per tutti i dispositivi che eseguono il sistema operativo Windows RT, delle impostazioni necessarie per connettersi a una condivisione file nella rete aziendale. È possibile creare un profilo VPN contenente le impostazioni necessarie per connettersi alla rete aziendale e quindi distribuire questo profilo a tutti gli utenti della gerarchia che hanno dispositivi Windows RT. Gli utenti dei dispositivi Windows RT visualizzano la connessione VPN nell'elenco delle reti disponibili e possono connettersi facilmente alla rete.  

 Quando si crea un profilo VPN, è possibile includere un'ampia gamma di impostazioni di protezione, inclusi i certificati per la convalida server e l'autenticazione client per i quali è stato eseguito il provisioning usando profili certificato in Configuration Manager. Per altre informazioni sui profili certificato, vedere [Profili certificato in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

 Le sezioni seguenti spiegano quali dispositivi è possibile configurare con profili VPN se si usa Configuration Manager.

 Per controllare quali dispositivi è possibile configurare quando si usa Configuration Manager con Microsoft Intune, vedere [Profili VPN nei dispositivi mobili](/sccm/mdm/deploy-use/create-vpn-profiles).  

## <a name="vpn-profiles-when-using-configuration-manager"></a>Profili VPN usando Configuration Manager  
 Nella tabella seguente vengono descritti i profili VPN che possono essere configurati per diverse piattaforme per dispositivi.  

|Tipo di connessione|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|  
|---------------------|-----------------|----------------|--------------------|----------------|  
|**Cisco AnyConnect**|No|No|No|No|  
|**Pulse Secure**|Sì|No|Yes|Sì|  
|**F5 Edge Client**|Sì|No|Yes|Sì|  
|**Dell SonicWALL Mobile Connect**|Sì|No|Yes|Sì|  
|**Check Point Mobile VPN**|Sì|No|Yes|Sì|  
|**Microsoft SSL (SSTP)**|Sì|Sì|Sì|No|  
|**Microsoft Automatico**|Sì|Sì|Sì|No|  
|**IKEv2**|Sì|Sì|Sì|No|  
|**PPTP**|Sì|Sì|Sì|No|  
|**L2TP**|Sì|Sì|Sì|No|  

### <a name="next-steps"></a>Passaggi successivi  
 Usare gli argomenti seguenti per pianificare, configurare, far funzionare e gestire i profili VPN in Configuration Manager.  

-   [Prerequisiti per i profili VPN in System Center Configuration Manager](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Sicurezza e privacy per i profili VPN in System Center Configuration Manager](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)


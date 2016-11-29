---
title: Profili VPN in System Center Configuration Manager | System Center Configuration Manager
description: Di seguito viene illustrato come usare i profili VPN in System Center Configuration Manager per distribuire impostazioni VPN agli utenti dell'organizzazione.
ms.custom: na
ms.date: 10/10/2016
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
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0fbce476b8a9b91a88354fb4abfadfd2526ca5e8
ms.openlocfilehash: dda572392884c54b63af09a9fae79c1e73eb3d95


---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>Profili VPN in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


Usare i profili VPN in System Center Configuration Manager per distribuire impostazioni VPN agli utenti dell'organizzazione. La distribuzione di queste impostazioni consente di ridurre al minimo le operazioni che l'utente finale deve eseguire per connettersi alle risorse nella rete aziendale.  

 Ad esempio, si supponga di voler effettuare il provisioning di tutti i dispositivi che eseguono il sistema operativo iOS con le impostazioni necessarie per connettersi a una condivisione file nella rete aziendale. È possibile creare un profilo VPN contenente le impostazioni necessarie per connettersi alla rete aziendale e quindi distribuire questo profilo a tutti gli utenti della gerarchia che dispongono di dispositivi iOS. Gli utenti dei dispositivi iOS visualizzeranno la connessione VPN nell'elenco delle reti disponibili e potranno connettersi molto facilmente alla rete.  

 Quando si crea un profilo VPN, è possibile includere un'ampia gamma di impostazioni di protezione, inclusi i certificati per la convalida server e l'autenticazione client per i quali è stato eseguito il provisioning usando profili certificato in Configuration Manager. Per altre informazioni sui profili certificato, vedere [Profili certificato in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

 Le sezioni seguenti spiegano quali dispositivi è possibile configurare con profili VPN se si usa Configuration Manager o Configuration Manager con Microsoft Intune.  

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

## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>Profili VPN usando Configuration Manager insieme a Intune  
 Per distribuire i profili nei dispositivi Android, iOS, Windows Phone e Windows 8.1, tali dispositivi devono essere registrati in Microsoft Intune. Anche i dispositivi su altre piattaforme possono essere registrati in Intune. Per informazioni su come eseguire la registrazione, vedere [Gestire i dispositivi mobili con Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx). Questa tabella indica il tipo di connessione supportato per ogni piattaforma del dispositivo:  

|Tipo di connessione|iOS e Mac OS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop e Mobile|  
|---------------------|----------------------|-------------|-----------------|----------------|--------------------|-----------------------|-----------------------------------|  
|Cisco AnyConnect|Sì|Sì|No|No|No|No|Sì (URI OMA)|  
|Pulse Secure|Sì|Sì|Sì|No|Yes|Sì|Sì|  
|F5 Edge Client|Yes|Sì|Sì|No|Yes|Sì|Yes|  
|Dell SonicWALL Mobile Connect|Sì|Sì|Sì|No|Yes|Sì|Sì|  
|VPN mobile Check Point|Sì|Sì|Sì|No|Yes|Sì|Sì|  
|Microsoft SSL (SSTP)|No|No|Yes|Sì|Sì|No|No|  
|Microsoft Automatico|No|No|Yes|Sì|Sì|No|Sì (URI OMA)|  
|IKEv2|Sì (Criteri personalizzati)|No|Yes|Sì|Sì|Sì|Sì (URI OMA)|  
|PPTP|Sì|No|Yes|Sì|Sì|No|Sì (URI OMA)|  
|L2TP|Sì|No|Yes|Sì|Sì|No|Sì (URI OMA)|  

### <a name="next-steps"></a>Passaggi successivi  
 Usare gli argomenti seguenti per pianificare, configurare, far funzionare e gestire i profili VPN in Configuration Manager.  

-   [Prerequisiti per i profili VPN in System Center Configuration Manager](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Sicurezza e privacy per i profili VPN in System Center Configuration Manager](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)



<!--HONumber=Nov16_HO1-->



---
title: Profili VPN
titleSuffix: Configuration Manager
description: Di seguito viene illustrato come usare i profili VPN in System Center Configuration Manager per distribuire impostazioni VPN agli utenti dell'organizzazione.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: c0f094f1-852e-4606-91db-97846d8f0772
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 505a4f3c00bc69e115b4130d422e11d8dec3fe30
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500390"
---
# <a name="vpn-profiles-in-system-center-configuration-manager"></a>Profili VPN in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

<!--1283610-->
Per distribuire impostazioni VPN agli utenti dell'organizzazione, usare i profili VPN in Configuration Manager. La distribuzione di queste impostazioni consente di ridurre al minimo le operazioni che l'utente finale deve eseguire per connettersi alle risorse nella rete aziendale.  

 Si supponga, ad esempio, di voler configurare tutti i dispositivi Windows 10 con le impostazioni necessarie per connettersi a una condivisione file nella rete aziendale. È possibile creare un profilo VPN con le impostazioni necessarie per connettersi alla rete aziendale e quindi distribuire questo profilo a tutti gli utenti che dispongono di dispositivi che eseguono Windows 10. Tali utenti visualizzano la connessione VPN nell'elenco delle reti disponibili e possono connettersi con la massima facilità.  

 Quando si crea un profilo VPN, è possibile includere una vasta gamma di impostazioni di protezione. Queste impostazioni includono certificati per la convalida del server e l'autenticazione del client di cui viene eseguito il provisioning con i profili certificato di Configuration Manager. Per altre informazioni, vedere i [profili certificato](introduction-to-certificate-profiles.md).  

> [!Note]  
> Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) (Abilitare le funzioni facoltative dagli aggiornamenti).<!--505213-->  


 Per controllare quali dispositivi è possibile configurare quando si usa Configuration Manager con Microsoft Intune, vedere [Profili VPN nei dispositivi mobili](/sccm/mdm/deploy-use/create-vpn-profiles).  

## <a name="vpn-profiles-when-using-configuration-manager"></a>Profili VPN usando Configuration Manager  
 Nella tabella seguente vengono descritti i profili VPN che possono essere configurati per diverse piattaforme per dispositivi.  

|Tipo di connessione|Windows 8.1|Windows RT|Windows RT 8.1|Windows 10|  
|---------------------|-----------------|----------------|--------------------|----------------|  
|**Cisco AnyConnect**|No|No|No|No|  
|**Pulse Secure**|Sì|No|Sì|Sì|  
|**F5 Edge Client**|Sì|No|Sì|Sì|  
|**Dell SonicWALL Mobile Connect**|Sì|No|Sì|Sì|  
|**Check Point Mobile VPN**|Sì|No|Sì|Sì|  
|**Microsoft SSL (SSTP)**|Sì|Sì|Sì|No|  
|**Microsoft Automatico**|Sì|Sì|Sì|No|  
|**IKEv2**|Sì|Sì|Sì|No|  
|**PPTP**|Sì|Sì|Sì|No|  
|**L2TP**|Sì|Sì|Sì|No|  

### <a name="next-steps"></a>Passaggi successivi  
 Usare gli argomenti seguenti per pianificare, configurare, far funzionare e gestire i profili VPN in Configuration Manager.  

-   [Prerequisiti per i profili VPN in System Center Configuration Manager](../plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Sicurezza e privacy per i profili VPN in System Center Configuration Manager](../plan-design/security-and-privacy-for-wifi-vpn-profiles.md)

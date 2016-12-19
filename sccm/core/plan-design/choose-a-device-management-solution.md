---
title: Scegliere una soluzione di gestione dei dispositivi per System Center Configuration Manager | Documentazione Microsoft
description: Informazioni sulle soluzioni di System Center Configuration Manager disponibili per la gestione di PC, server e dispositivi.
ms.custom: na
ms.date: 12/08/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
caps.latest.revision: 14
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 099e0001c01713224988e5b49d02cb358e3015d6
ms.openlocfilehash: f4f0a8e8b1b5aae2586cc885734f405f7e7f9ff5


---
# <a name="choose-a-device-management-solution-for-system-center-configuration-manager"></a>Scegliere una soluzione di gestione dei dispositivi per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager, noto anche come ConfgMgr o SCCM, offre diverse soluzioni per la gestione di PC, server e dispositivi. È possibile scegliere la soluzione più adatta in base alle piattaforme del dispositivo da gestire e alle funzionalità di gestione necessarie.  


##  <a name="overview-of-device-management-solutions"></a>Panoramica delle soluzioni di gestione dei dispositivi  
 Questa sezione panoramica è seguita da due tabelle che consentono di confrontare le soluzioni di gestione, una [in base alle piattaforme per dispositivi mobili supportati](#compare-device-management-solutions-based-on-supported-mobile-device-platforms) e [una in base alle funzionalità di gestione](#compare-mobile-device-management-solutions-based-on-management-functionality).
  

-   **Gestione di dispositivi con il client di Configuration Manager**  

     Questa opzione, che richiede l'installazione dell'applicazione client di Configuration Manager sui dispositivi, offre più funzionalità per la gestione di PC, server e altri dispositivi nell'ambiente in uso.   

     Per altre informazioni, vedere [Metodi di installazione client in System Center Configuration Manager](/sccm/core/client/deploy/plan/client-installation-methods).  

-   **Gestione dei dispositivi mobili con l'infrastruttura locale di Configuration Manager**  

     Questa opzione usa le funzionalità di gestione dei dispositivi predefinite nei sistemi operativi di alcune piattaforme del dispositivo. Anche se non è completa come la gestione basata su client, la Gestione di dispositivi mobili locale offre un approccio più semplice che usa risorse locali di Configuration Manager per accedere e gestire i dispositivi. Al momento, Gestione di dispositivi mobili (MDM) locale è supportata solo per i PC Windows 10 e i dispositivi Windows 10 Mobile.  

     Per altre informazioni su questa soluzione, vedere [Manage mobile devices with on-premises infrastructure in System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) (Gestire i dispositivi mobili con infrastruttura locale in System Center Configuration Manager).  

-   **Gestione dei dispositivi mobili con Microsoft Intune (ibridi)**  

     Anziché usare risorse locali di Configuration Manager, questa opzione usa Microsoft Intune per registrare e gestire i dispositivi. Anche se Intune gestisce i dispositivi, è possibile accedere alle attività di gestione nella console di Configuration Manager. Questa opzione supporta tutti i principali sistemi operativi di dispositivi mobili, tra cui Windows 10 Mobile, Windows Phone, iOS, Mac OS X e Android. Fornisce anche la gestione dei computer Windows 8.1 e Windows 10 nell'organizzazione.  

     Per altre informazioni su questa soluzione, vedere [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../mdm/understand/hybrid-mobile-device-management.md)(Gestione di dispositivi mobili ibridi con System Center Configuration Manager e Microsoft Intune).  

-   **Gestione dei dispositivi mobili con Exchange**  

     Questa opzione usa il connettore Exchange Server per connettere più server Exchange a Configuration Manager e centralizza la gestione dei dispositivi che riescono a connettersi a Exchange ActiveSync. È possibile configurare le funzionalità di gestione dei dispositivi mobili di Exchange, come la cancellazione remota dati nel dispositivo e il controllo delle impostazioni per più server Exchange, dalla console di Configuration Manager.  

     Per altre informazioni su questa soluzione, vedere [Manage mobile devices with System Center Configuration Manager and Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md) (Gestire i dispositivi mobili con System Center Configuration Manager ed Exchange).  

 È possibile usare queste soluzioni di gestione dei dispositivi da sole o in combinazione. Ad esempio, è possibile usare l'approccio di gestione basato su client per gestire i computer e i server dell'organizzazione e usare Intune per gestire i dispositivi mobili. Combinando gli approcci in questo modo, è possibile coprire tutte le esigenze di gestione dei dispositivi dalla console di Configuration Manager.  

## <a name="compare-device-management-solutions-based-on-supported-mobile-device-platforms"></a>Confrontare le soluzioni di gestione dei dispositivi in base alle piattaforme per dispositivi mobili supportate  

|Piattaforma|Con il client di Configuration Manager|Configuration Manager con Microsoft Intune (ibrido)|Gestione dei dispositivi mobili (MDM) locale|Configuration Manager con Exchange|  
|--------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Android||Sì||Sì|  
|iOS||Sì||Sì|  
|Mac OS X|Sì|||Sì|  
|UNIX/Linux|Sì|||Sì|  
|Windows 10|Sì|Sì|Sì|Sì|  
|Windows 10 Mobile||Sì|Sì|Sì|  
|Windows (versioni precedenti)|Sì|Sì||Sì|  
|Windows CE|Sì (con client precedente del dispositivo mobile)|||Sì|  
|Windows Embedded|Sì||||  
|Windows Phone||Sì||Sì|  
|Windows Server|Sì|||Sì|  

 Per un elenco completo delle piattaforme supportate, vedere [Supported operating systems for clients and devices for System Center Configuration Manager](configs\supported-operating-systems-for-clients-and-devices.md) (Sistemi operativi supportati per client e dispositivi per System Center Configuration Manager).

##  <a name="a-namebkmkcomp2a-compare-mobile-device-management-solutions-based-on-management-functionality"></a><a name="bkmk_comp2"></a> Confrontare le soluzioni di gestione dei dispositivi mobili in base alle funzionalità di gestione  

|Funzionalità di gestione|Con il client di Configuration Manager|Configuration Manager con Microsoft Intune (ibrido)|Gestione dei dispositivi mobili (MDM) locale|Configuration Manager con Exchange|  
|------------------------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Sicurezza dell'infrastruttura a chiave pubblica (PKI) tra il dispositivo mobile e Configuration Manager usando l'autenticazione reciproca e SSL per crittografare i trasferimenti di dati|Sì|Sì|Sì||  
|Installazione client|Sì||||  
|Supporto via Internet|Sì||||  
|Individuazione|Sì|||Sì|  
|Inventario hardware|Sì|Sì|Sì|Sì|  
|Inventario software|Sì|||Sì|  
|Impostazioni|Sì|Sì|Sì|Sì|  
|Distribuzione software|Sì|Sì|Sì||  
|Monitorare con il punto di stato di fallback|Sì||||  
|Connessioni ai punti di gestione|Sì||Sì||  
|Connessioni ai punti di distribuzione|Sì|Sì|Sì||  
|Blocco da Configuration Manager|Sì|Sì|Sì||  
|Inserimento in quarantena e blocco da Exchange Server (e Configuration Manager)||||Sì|  
|Cancellazione remota|Sì|Sì|Sì|Sì|  



<!--HONumber=Dec16_HO3-->



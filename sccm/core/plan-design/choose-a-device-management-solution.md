---
title: Scegliere una soluzione di gestione dei dispositivi per System Center Configuration Manager
description: Informazioni sulle soluzioni di System Center Configuration Manager disponibili per la gestione di PC, server e dispositivi.
ms.custom: na
ms.date: 10/06/2016
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
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b64135826dd49c594167999aebd322fa3ed61345


---
# <a name="choose-a-device-management-solution-for-system-center-configuration-manager"></a>Scegliere una soluzione di gestione dei dispositivi per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager offre diverse soluzioni per la gestione di PC, server e dispositivi. È possibile scegliere la soluzione più adatta in base alle piattaforme del dispositivo da gestire e alle funzionalità di gestione necessarie.  


##  <a name="a-namebkmkoverviewa-overview-of-device-management-solutions"></a><a name="bkmk_overview"></a> Panoramica delle soluzioni di gestione dei dispositivi  
 Per gestire computer e dispositivi con Configuration Manager, è possibile usare le opzioni seguenti:  

-   **Gestione di dispositivi con il client di Configuration Manager**  

     Questa opzione, che richiede l'installazione dell'applicazione client di Configuration Manager in ogni dispositivo da gestire, offre più funzionalità per la gestione di PC, server e altri dispositivi nell'ambiente in uso. Questa opzione rappresenta la modalità tradizionale con cui Configuration Manager ha sempre fornito la gestione dei dispositivi.  

     Per altre informazioni su questa soluzione, vedere [Metodi di installazione client in System Center Configuration Manager](/sccm/core/client/deploy/plan/client-installation-methods).  

-   **Gestione dei dispositivi mobili con l'infrastruttura locale di Configuration Manager**  

     Questa opzione usa le funzionalità di gestione dei dispositivi predefinite nei sistemi operativi di determinate piattaforme del dispositivo. Anche se non è completa come la gestione basata su client, la Gestione di dispositivi mobili locale offre un approccio più semplice che usa risorse locali di Configuration Manager per accedere e gestire i dispositivi. Al momento, la Gestione di dispositivi mobili locale è supportata solo per i PC di Windows 10 e i dispositivi di Windows 10 Mobile.  

     Per altre informazioni su questa soluzione, vedere [Manage mobile devices with on-premises infrastructure in System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) (Gestire i dispositivi mobili con infrastruttura locale in System Center Configuration Manager).  

-   **Gestione dei dispositivi mobili con Microsoft Intune (ibridi)**  

     Questa opzione è definita come gestione ibrida dei dispositivi mobili.  L'opzione usa Microsoft Intune per registrare e gestire dispositivi invece di usare risorse locali di Configuration Manager. Anche se Intune gestisce i dispositivi, è possibile controllare le attività di gestione nella console di Configuration Manager. Questa opzione supporta tutti i principali sistemi operativi di dispositivi mobili, tra cui Windows 10 Mobile, Windows Phone, iOS e Android. Fornisce anche la gestione dei computer Windows 8.1 e Windows 10 nell'organizzazione.  

     Per altre informazioni su questa soluzione, vedere [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../mdm/plan-design/hybrid-mobile-device-management.md)(Gestione di dispositivi mobili ibridi con System Center Configuration Manager e Microsoft Intune).  

-   **Gestione dei dispositivi mobili con Exchange**  

     Questa opzione, che usa il connettore Exchange Server per connettere più server Exchange a Configuration Manager, centralizza la gestione dei dispositivi che riescono a connettersi a Exchange ActiveSync. È possibile configurare le funzionalità di gestione dei dispositivi mobili di Exchange, come la cancellazione remota dati nel dispositivo e il controllo delle impostazioni per più server Exchange, dalla console di Configuration Manager.  

     Per altre informazioni su questa soluzione, vedere [Manage mobile devices with System Center Configuration Manager and Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md) (Gestire i dispositivi mobili con System Center Configuration Manager ed Exchange).  

 È possibile usare queste soluzioni di gestione dei dispositivi autonomamente o in combinazione. Ad esempio, è possibile usare l'approccio di gestione basata su client per eseguire la gestione di computer e server dell'organizzazione e anche la gestione basata su Intune per i dispositivi mobili. Combinando gli approcci in questo modo, è possibile coprire tutte le esigenze di gestione dei dispositivi e controllare la gestione con la console di Configuration Manager.  

##  <a name="a-namebkmkcomp1a-compare-device-management-solutions-based-on-supported-mobile-device-platforms"></a><a name="bkmk_comp1"></a> Confrontare le soluzioni di gestione dei dispositivi in base alle piattaforme per dispositivi mobili supportate  

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



<!--HONumber=Nov16_HO1-->



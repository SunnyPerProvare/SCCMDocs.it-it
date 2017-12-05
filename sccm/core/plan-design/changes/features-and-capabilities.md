---
title: "Caratteristiche e funzionalità"
titleSuffix: Configuration Manager
description: "Informazioni sulle funzionalità di gestione principali di System Center Configuration Manager."
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
caps.latest.revision: "18"
caps.handback.revision: "0"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 71e1edc178e770d7c05007c258e8085a2e3fe984
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/04/2017
---
# <a name="features-and-capabilities-of-system-center-configuration-manager"></a>Caratteristiche e funzionalità di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Di seguito sono descritte le funzionalità di gestione principali di System Center Configuration Manager. Poiché ogni funzionalità ha requisiti diversi, le funzionalità che si intende usare potrebbero influire sulla struttura e l'implementazione della gerarchia di Configuration Manager. Se, ad esempio, si desidera distribuire il software nei dispositivi della gerarchia, è necessario installare il ruolo del sistema del sito del punto di distribuzione.  

 Per altre informazioni sulla pianificazione e l'installazione di Configuration Manager per supportare queste funzionalità di gestione nell'ambiente, vedere [Get ready for System Center Configuration Manager](../../../core/plan-design/get-ready.md) (Preparativi per System Center Configuration Manager).  

 **Gestione delle applicazioni**  

 Fornisce un set di strumenti e risorse che consentono di creare, gestire, distribuire e monitorare le applicazioni in una gamma di diversi dispositivi gestiti. Configuration Manager offre anche strumenti che consentono di proteggere i dati aziendali contenuti nelle app dell'utente. Vedere [Introduction to application management](/sccm/apps/understand/introduction-to-application-management) (Introduzione alla gestione delle applicazioni).

 **Accesso alle risorse aziendali**  

 Offre un insieme di strumenti e risorse che consentono di dare agli utenti dell'organizzazione accesso in remoto ai dati e alle applicazioni. Questi strumenti includono profili Wi-Fi, profili VPN, profili del certificato e l'accesso condizionale a Exchange e SharePoint Online. Vedere [Protect data and site infrastructure with System Center Configuration Manager](../../../protect/understand/protect-data-and-site-infrastructure.md) (Proteggere i dati e l'infrastruttura del sito con System Center Configuration Manager) e [Manage access to services in System Center Configuration Manager](../../../protect/deploy-use/manage-access-to-services.md) (Gestire l'accesso ai servizi in System Center Configuration Manager).  

 **Impostazioni di conformità**  

 Offre un set di strumenti e risorse che consentono di valutare, tenere traccia e correggere la conformità della configurazione dei dispositivi client nell'azienda. Inoltre, è possibile usare le impostazioni di conformità per configurare una gamma di funzionalità e impostazioni di sicurezza nei dispositivi gestiti. Vedere [Ensure device compliance with System Center Configuration Manager](../../../compliance/understand/ensure-device-compliance.md) (Garantire la conformità dei dispositivi con System Center Configuration Manager).  

 **Endpoint Protection**  

 Offre sicurezza, antimalware e gestione di Windows Firewall per i computer dell'azienda. Vedere [Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

 **Inventario**  

 Offre un set di strumenti per identificare e monitorare gli asset:  

-   **Inventario hardware**: raccoglie informazioni dettagliate sull'hardware dei dispositivi nell'azienda. Vedere [Introduction to hardware inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/introduction-to-hardware-inventory.md) (Introduzione all'inventario hardware in System Center Configuration Manager).  

-   **Inventario software**: raccoglie e segnala le informazioni sui file archiviati sui computer client dell'organizzazione. Vedere [Introduction to software inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/introduction-to-software-inventory.md) (Introduzione all'inventario software in System Center Configuration Manager).  

-   **Asset Intelligence**: offre strumenti per raccogliere i dati di inventario e per monitorare l'utilizzo delle licenze software nell'azienda. Vedere [Introduction to Asset Intelligence in System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md) (Introduzione ad Asset Intelligence in System Center Configuration Manager).  

**Gestione dei dispositivi mobili con Microsoft Intune**  

 È possibile usare Configuration Manager per gestire dispositivi iOS, Android (incluso Samsung KNOX Standard), Windows Phone e Windows con il servizio Microsoft Intune in Internet.

 Anche se si usa il servizio Intune, le attività di gestione vengono completate usando il ruolo del sistema del sito del punto di connessione del servizio disponibile tramite la console Configuration Manager. Vedere [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md) (Gestione dei dispositivi mobili (MDM) ibrida con System Center Configuration Manager e Microsoft Intune).  

 **Gestione dei dispositivi mobili locale**  

 Registra e gestisce i PC e i dispositivi mobili usando l'infrastruttura di Configuration Manager locale e la funzionalità di gestione integrata nelle piattaforme per dispositivi (anziché fare affidamento su un client di Configuration Manager installato separatamente). Attualmente supporta la gestione dei dispositivi Windows 10 Enterprise e Windows 10 Mobile. Vedere [Manage mobile devices with on-premises infrastructure in System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) (Gestire i dispositivi mobili con l'infrastruttura locale in System Center Configuration Manager).  

 **Distribuzione del sistema operativo:**  

 Offre uno strumento per creare immagini del sistema operativo. È quindi possibile usare queste immagini per distribuire i sistemi operativi nei computer, usando l'avvio PXE o supporti di avvio, ad esempio un set di CD, DVD o unità flash USB. Si noti che questo vale per i computer gestiti da Configuration Manager, nonché per i computer non gestiti. Vedere [Introduction to operating system deployment in System Center Configuration Manager](../../../osd/understand/introduction-to-operating-system-deployment.md) (Introduzione alla distribuzione del sistema operativo in System Center Configuration Manager).  

 **Risparmio energia**  

 Offre un set di strumenti e risorse utilizzabili per gestire e monitorare il consumo di energia dei computer client nell'azienda. Vedere [Introduction to power management in System Center Configuration Manager](../../../core/clients/manage/power/introduction-to-power-management.md) (Introduzione al risparmio energia in System Center Configuration Manager).  

 **Query**  

 Offre uno strumento per recuperare informazioni sulle risorse nella gerarchia e informazioni sui dati di inventario e sui messaggi di stato. È quindi possibile usare queste informazioni per creare report o definire le raccolte di dispositivi o utenti per le impostazioni di distribuzione e configurazione del software. Vedere [Introduction to queries in System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md) (Introduzione alle query in System Center Configuration Manager).  

 **Profili di connessione remota**  

 Offre un set di strumenti e risorse che consentono di creare, distribuire e monitorare le impostazioni di connessione remota nei dispositivi dell'organizzazione. Distribuendo queste impostazioni, viene ridotto al minimo l'impegno richiesto agli utenti per connettersi ai computer nella rete aziendale. Vedere [Working with remote connection profiles in System Center Configuration Manager](/sccm/compliance/deploy-use/create-remote-connection-profiles) (Uso di profili di connessione remota in System Center Configuration Manager).  

 **Elementi di configurazione di profili e dati utente**  

 Gli elementi di configurazione di profili e dati utente in Configuration Manager contengono le impostazioni che consentono di gestire il reindirizzamento delle cartelle, i file offline e i profili mobili nei computer che eseguono Windows 8 e versioni successive per gli utenti della gerarchia. Vedere [Working with user data and profiles configuration items in System Center Configuration Manager](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items) (Uso degli elementi di configurazione di profili e dati utente in System Center Configuration Manager).  

 **Controllo remoto**  

 Offre strumenti per amministrare in remoto i computer client dalla console di Configuration Manager. Vedere [Introduction to remote control in System Center Configuration Manager](../../../core/clients/manage/remote-control/introduction-to-remote-control.md) (Introduzione al controllo remoto in System Center Configuration Manager).  

 **Creazione di report**  

 Offre un set di strumenti e risorse che consentono di usare le funzionalità di creazione di report avanzate di SQL Server Reporting Services dalla console di Configuration Manager. Vedere [Introduction to reporting in System Center Configuration Manager](../../../core/servers/manage/introduction-to-reporting.md) (Introduzione alla creazione di report in System Center Configuration Manager).  

 **Controllo del software**  

 Offre strumenti per monitorare e raccogliere i dati di utilizzo del software dai client di Configuration Manager. Vedere [Monitorare l'utilizzo delle app con la misurazione del software in System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

 **Aggiornamenti software**  

 Offre un set di strumenti e risorse che consentono di gestire, distribuire e monitorare gli aggiornamenti software nell'azienda. Vedere [Introduction to software updates in System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction) (Introduzione agli aggiornamenti software in System Center Configuration Manager).  

---
title: Firewall e domini | Microsoft Docs
description: Configurare firewall, porte e domini per la preparazione alle comunicazioni di System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: df0622164ae7784ccfedc0f4c3328c42c1d050c3


---
# <a name="configure-firewalls-ports-and-domains-for-system-center-configuration-manager"></a>Configurare firewall, porte e domini per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Per preparare la rete a supportare System Center Configuration Manager, pianificare la configurazione di infrastrutture come i firewall a passare le comunicazioni usate da Configuration Manager.  

|Considerazione|Dettagli|  
|-------------------|-------------|  
|**Porte e protocolli** usati da diverse funzionalità di Configuration Manager. Alcune porte sono obbligatorie, mentre altri **domini e servizi** possono essere personalizzati.|La maggior parte delle comunicazioni di Configuration Manager usa porte comuni, ad esempio la porta 80 per HTTP o 443 per le comunicazioni HTTPS. Tuttavia, [alcuni ruoli del sistema del sito supportano l'uso di siti Web personalizzati](/sccm/core/plan-design/network/websites-for-site-system-servers) e porte personalizzate.<br /><br /> **Prima di distribuire Configuration Manager**, identificare le porte da usare e configurare i firewall in modo appropriato.<br /><br /> **In seguito, se è necessario modificare una porta** dopo l'installazione di Configuration Manager, non trascurare l'aggiornamento dei firewall sui dispositivi e la rete e modificare anche la configurazione della porta dall'interno di Configuration Manager.<br /><br /> Per altre informazioni, vedere: </br>- [Come configurare le porte di comunicazione client](../../../core/clients/deploy/configure-client-communication-ports.md) </br>- [Porte usate in Configuration Manager](../../../core/plan-design/hierarchy/ports.md) </br>- [Requisiti di accesso Internet per il punto di connessione del servizio](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls)|  
|**Domini e i servizi** a cui client e server del sito potrebbero dover accedere.|Le funzionalità di Configuration Manager possono richiedere che i clienti e i server del sito abbiano accesso a servizi e domini specifici su Internet, ad esempio Windowsudpate.microsoft.com o il servizio Microsoft Intune.<br /><br /> Se si usa Microsoft Intune per gestire i dispositivi mobili, è necessario anche configurare l'accesso a [porte e domini che sono richiesti da Intune.](https://docs.microsoft.com/en-us/intune/get-started/network-infrastructure-requirements-for-microsoft-intune)|  
|**Server proxy** per i server del sistema del sito e per le comunicazioni client. È possibile specificare i server proxy per diversi client e server di sistema del sito.|Dal momento che queste configurazioni vengono eseguite in fase di installazione di un ruolo del sistema del sito o un client, è sufficiente essere a conoscenza delle configurazioni del server proxy per riferimento futuro quando si configurano i ruoli del sistema del sito e i client.<br /><br /> Se non si è certi se per la distribuzione sarà necessario usare i server proxy, esaminare [Supporto dei server proxy in System Center Configuration Manager](../../../core/plan-design/network/proxy-server-support.md) per conoscere i ruoli del sistema del sito e le operazioni del client che possono usare un server proxy.|  



<!--HONumber=Dec16_HO3-->



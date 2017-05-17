---
title: Gestione dei dispositivi mobili (MDM) locale | Microsoft Docs
description: Informazioni sulla gestione dispositivi mobili locale, una soluzione di gestione dei dispositivi in System Center Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
caps.latest.revision: 8
author: Mtillman
ms.author: mtillman
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 0d6479bcc134103e6005159a8ea295a5f359a436
ms.openlocfilehash: cbd33bf3cf7d623d9ba7a657d4ca7d746d7e79da
ms.contentlocale: it-it
ms.lasthandoff: 12/16/2016


---
# <a name="on-premises-mobile-device-management-mdm-in-system-center-configuration-manager"></a>Gestione di dispositivi mobili (MDM) locale in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La gestione di dispositivi mobili locale di System Center Configuration Manager è una soluzione di gestione dei dispositivi che si basa sulle funzionalità di gestione integrate dei sistemi operativi dei dispositivi (in base allo standard Open Mobile Alliance Device Management o OMA DM) e usa l'infrastruttura di Configuration Manager aziendale per la gestione e la manutenzione dei dispositivi. La gestione di dispositivi mobili locale richiede Microsoft Intune per la configurazione della funzionalità di gestione. Microsoft Intune, tuttavia, è necessario soltanto per la sottoscrizione e a volte per inviare una notifica ai dispositivi che richiede di verificare eventuali modifiche ai criteri ma non viene usato per la gestione dei dispositivi o l'archiviazione di dati sui dispositivi.  

 ![Gestione locale](media/On-premises-conceptual.png)  

 La gestione di dispositivi mobili locale differisce da Microsoft Intune che si basa anche sulle funzionalità OMA DM integrate, mentre tutte le funzioni di gestione vengono offerte tramite i servizi cloud.  La gestione di dispositivi mobili locale differisce anche dalla soluzione di gestione basata su client tradizionalmente offerta da Configuration Manager perché si basa su un'infrastruttura aziendale simile, ma non usa software client installato separatamente nei computer e nei dispositivi gestiti.  

 La tabella seguente elenca i vantaggi e svantaggi della gestione di dispositivi mobili locale rispetto alla gestione basata su client tradizionale:  

|Vantaggi|Svantaggi|  
|----------------|-------------------|  
|**Infrastruttura semplificata** : sono necessari meno ruoli del sistema del sito.<br /><br /> **Maggiore facilità di gestione**: poiché la funzionalità di gestione è integrata nel sistema operativo del dispositivo, non sono necessarie nuove versioni del software client quando vengono introdotte nuove funzionalità di gestione nel sistema di Configuration Manager.<br /><br /> **Locale** : tutte le attività di gestione e i dati vengono mantenuti in locale.|**Meno funzionalità di gestione client** : nessun supporto di orchestrazione, misurazione del software, integrazione di terze parti, sequenza di attività o Software Center.<br /><br /> **Supporto dei dispositivi limitato**: attualmente la gestione di dispositivi mobili locale supporta solo i dispositivi che eseguono Windows 10 e Windows 10 Mobile.|  

 Gli argomenti seguenti offrono informazioni che è possibile usare per pianificare, preparare e registrare i dispositivi per la gestione di dispositivi mobili locale:  

-   [Pianificare la gestione di dispositivi mobili locale in System Center Configuration Manager](../plan-design/plan-on-premises-mdm.md)  

     Informazioni sugli aspetti da considerare per la configurazione dell'infrastruttura di Configuration Manager e la pianificazione della registrazione dei dispositivi nella gestione di dispositivi mobili locale.  

-   [Preparativi per la gestione dei dispositivi mobili (MDM) locale in System Center Configuration Manager](../get-started/preparation-steps-for-on-premises-mdm.md)  

     Informazioni su come preparare il sistema di Configuration Manager per la gestione di dispositivi mobili locale tramite la configurazione della sottoscrizione di Microsoft Intune, l'impostazione dei certificati, l'installazione dei ruoli di sistema del sito e l'impostazione della registrazione dei dispositivi.  

-   [Registrare i dispositivi per la gestione di dispositivi mobili locale in System Center Configuration Manager](../deploy-use/enroll-devices-on-premises-mdm.md)  

     Informazioni sulla modalità di registrazione, su come gli utenti possono registrare i propri dispositivi e sulla registrazione in blocco dei dispositivi con un pacchetto di registrazione.  


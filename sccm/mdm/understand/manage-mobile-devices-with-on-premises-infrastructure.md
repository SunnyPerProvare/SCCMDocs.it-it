---
title: Software MDM locale
titleSuffix: Configuration Manager
description: Informazioni sulla gestione dei dispositivi mobili in locale, una soluzione di gestione di dispositivi in Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 49e07a7ebe6ec53d61ea9e2ee3bc941dd8561094
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62286986"
---
# <a name="on-premises-mdm-in-configuration-manager"></a>On-premises MDM in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Configuration Manager in locale la gestione dei dispositivi mobili (MDM) è una soluzione di gestione di dispositivi che si basa sulla funzionalità di gestione integrate del sistema operativo del dispositivo. Questa funzionalità si basa sullo standard Open Mobile Alliance (OMA) Device Management (DM). Infrastruttura di Configuration Manager della tua organizzazione Usa per gestire e mantenere i dispositivi. On-premise MDM richiede Microsoft Intune per configurare la funzionalità di gestione, ma è necessario solo per la sottoscrizione. Intune viene usato in alcuni casi per notificare ai dispositivi di archiviare le modifiche ai criteri, ma non viene usato per gestire i dispositivi o archiviare i relativi dati.  

![Gestione locale](media/On-premises-conceptual.png)  

MDM locale è diverso da Microsoft Intune, che si basa anche sulle funzionalità OMA DM integrate. Tutte le funzioni di gestione in Intune vengono fornite tramite i servizi cloud. MDM locale è diversa anche dalla soluzione di gestione basata su client tradizionalmente offerta da Configuration Manager. Perché si basa su un'infrastruttura simile ma non usa software client installato separatamente nei dispositivi gestiti.  

> [!Note]  
> A partire dalla versione 1810, una connessione di Intune non è più necessaria per le nuove distribuzioni MDM locale.<!--3607730, fka 1359124--> Per usare questa funzionalità è comunque necessario che l'organizzazione abbia le licenze di Intune. Attualmente non è possibile rimuovere la connessione a Intune dalle distribuzioni MDM locali esistenti. Per altre informazioni, vedere il [post di blog del supporto tecnico di Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

La tabella seguente elenca i vantaggi e svantaggi della MDM locale rispetto alla gestione basata su client tradizionale:  

|Vantaggi|Svantaggi|  
|----------------|-------------------|  
|**Infrastruttura semplificata** : sono necessari meno ruoli del sistema del sito.<br /><br /> **Maggiore facilità di gestione** - perché la funzionalità di gestione integrata in sistema operativo del dispositivo, le nuove versioni del software client non sono necessarie quando vengono introdotte nuove funzionalità di gestione per il sistema di Configuration Manager.<br /><br /> **Locale** : tutte le attività di gestione e i dati vengono mantenuti in locale.|**Meno funzionalità di gestione client** : nessun supporto di orchestrazione, misurazione del software, integrazione di terze parti, sequenza di attività o Software Center.<br /><br /> **Supporto dei dispositivi limitato** - attualmente MDM solo supporta i dispositivi locali che eseguono Windows 10 e Windows 10 Mobile.|  

Gli articoli seguenti forniscono informazioni che è possibile usare per pianificare, preparare e registrare i dispositivi per MDM locale:  

- [Pianificare la gestione dei dispositivi mobili locale](/sccm/mdm/plan-design/plan-on-premises-mdm)  

    Informazioni sugli aspetti da considerare quando configurazione dell'infrastruttura di Configuration Manager e la pianificazione per la registrazione dei dispositivi in MDM locale  

- [Preparativi per la MDM locale](/sccm/mdm/get-started/preparation-steps-for-on-premises-mdm)  

    Preparare Configuration Manager per MDM locale. Configurare la sottoscrizione di Microsoft Intune, configurare i certificati, installare i ruoli del sistema del sito e impostare la registrazione dei dispositivi.  

- [Registrare i dispositivi per la gestione dei dispositivi mobili locale](/sccm/mdm/deploy-use/enroll-devices-on-premises-mdm)  

    Informazioni sulla modalità di registrazione, su come gli utenti possono registrare i propri dispositivi e sulla registrazione in blocco dei dispositivi con un pacchetto di registrazione.  


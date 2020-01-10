---
title: Software MDM locale
titleSuffix: Configuration Manager
description: Informazioni sulla gestione dei dispositivi mobili locale, una soluzione di gestione dei dispositivi in Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ef153708b490fb4111a2070ccdefb933407fa6fc
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75821546"
---
# <a name="on-premises-mdm-in-configuration-manager"></a>MDM locale in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager gestione di dispositivi mobili (MDM) locale è una soluzione di gestione dei dispositivi che si basa sulle funzionalità di gestione predefinite del sistema operativo del dispositivo. Questa funzionalità è basata sullo standard Open Mobile Alliance (OMA) Device Management (DM). Usa l'infrastruttura di Configuration Manager dell'organizzazione per gestire e gestire i dispositivi. MDM locale richiede Microsoft Intune per configurare la funzionalità di gestione, ma è necessaria solo per la sottoscrizione. Intune viene usato a volte per aiutare a notificare ai dispositivi di archiviare le modifiche dei criteri, ma non viene usato per gestire i dispositivi o archiviare i dati su di essi.  

![Gestione locale](media/On-premises-conceptual.png)  

MDM locale è diverso da Microsoft Intune, che si basa anche sulle funzionalità di DM OMA predefinite. Tutte le funzioni di gestione in Intune vengono fornite tramite i servizi cloud. MDM locale differisce anche dalla soluzione di gestione basata su client tradizionalmente offerta da Configuration Manager. Si basa su un'infrastruttura simile, ma non usa software client installato separatamente nei dispositivi gestiti.  

> [!Note]  
> A partire dalla versione 1810, una connessione a Intune non è più necessaria per le nuove distribuzioni MDM locali.<!--3607730, fka 1359124--> Per usare questa funzionalità è comunque necessario che l'organizzazione abbia le licenze di Intune. Attualmente non è possibile rimuovere la connessione a Intune dalle distribuzioni MDM locali esistenti. Per altre informazioni, vedere il [post di blog del supporto tecnico di Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

La tabella seguente elenca i vantaggi e gli svantaggi di MDM locale rispetto alla gestione basata su client tradizionale:  

|Vantaggi|Svantaggi|  
|----------------|-------------------|  
|**Infrastruttura semplificata** : sono necessari meno ruoli del sistema del sito.<br /><br /> **Più facile da gestire** : poiché la funzionalità di gestione è integrata nel sistema operativo del dispositivo, non sono necessarie nuove versioni del software client quando le nuove funzionalità di gestione vengono introdotte nel sistema di Configuration Manager.<br /><br /> **Locale** : tutte le attività di gestione e i dati vengono mantenuti in locale.|**Meno funzionalità di gestione client** : nessun supporto di orchestrazione, misurazione del software, integrazione di terze parti, sequenza di attività o Software Center.<br /><br /> **Supporto** dei dispositivi limitato: MDM attualmente locale supporta solo i dispositivi che eseguono Windows 10 e Windows 10 Mobile.|  

Gli articoli seguenti forniscono informazioni che è possibile usare per pianificare, preparare e registrare i dispositivi per MDM locale:  

- [Pianificare la gestione dei dispositivi mobili locale](/sccm/mdm/plan-design/plan-on-premises-mdm)  

    Informazioni sugli elementi da considerare quando si configura l'infrastruttura Configuration Manager e si pianifica la registrazione dei dispositivi in MDM locale.  

- [Passaggi di preparazione per MDM locale](/sccm/mdm/get-started/preparation-steps-for-on-premises-mdm)  

    Ottenere Configuration Manager pronto per MDM locale. Configurare la sottoscrizione di Microsoft Intune, configurare i certificati, installare i ruoli del sistema del sito e configurare la registrazione dei dispositivi.  

- [Registrare i dispositivi per la gestione dei dispositivi mobili locale](/sccm/mdm/deploy-use/enroll-devices-on-premises-mdm)  

    Informazioni sulla modalità di registrazione, su come gli utenti possono registrare i propri dispositivi e sulla registrazione in blocco dei dispositivi con un pacchetto di registrazione.  


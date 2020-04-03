---
title: Software MDM locale
titleSuffix: Configuration Manager
description: Informazioni sulla gestione di dispositivi mobili (MDM) locale in Configuration Manager
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 497c05c7-fe9f-4b88-983b-1c5b3d59308e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ef3c956697c5ab1dc33705a8c48a939bdd5040cb
ms.sourcegitcommit: ccc3c929b5585c05d562020e68044de7d7e11c6a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2020
ms.locfileid: "80605298"
---
# <a name="on-premises-mdm-in-configuration-manager"></a>MDM locale in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Configuration Manager gestione di dispositivi mobili (MDM) locale è una soluzione di gestione dei dispositivi che si basa sulle funzionalità di gestione predefinite di Windows. Questa funzionalità è basata sullo standard Open Mobile Alliance (OMA) Device Management (DM). Usa l'infrastruttura di Configuration Manager dell'organizzazione per gestire e gestire i dispositivi. L'organizzazione richiede Microsoft Intune licenze per usare questa funzionalità, ma non richiede alcuna connessione cloud. Configuration Manager archivia tutti i dati sui dispositivi nel database del sito locale.

MDM locale è diverso da Microsoft Intune, che si basa anche sulle funzionalità di DM OMA predefinite. Tutte le funzioni di gestione in Intune vengono fornite tramite i servizi cloud. MDM locale differisce anche dalla soluzione di gestione basata su client tradizionalmente offerta da Configuration Manager. Si basa su un'infrastruttura simile, ma non usa software client installato separatamente nei dispositivi gestiti.  

## <a name="comparison"></a>Confronto

Le sezioni seguenti elencano i vantaggi e gli svantaggi di MDM locale rispetto alla gestione basata su client tradizionale:  

### <a name="advantages"></a>Vantaggi

- **Infrastruttura semplificata**: sono necessari meno ruoli del sistema del sito.

- **Più facile da gestire**: poiché la funzionalità di gestione è integrata nel sistema operativo del dispositivo, non sono necessarie nuove versioni del client Configuration Manager quando vengono introdotte nuove funzionalità di gestione per il sito.

- **Locale**:-tutti i dati e la gestione vengono conservati in locale.

### <a name="disadvantages"></a>Svantaggi

**Meno funzionalità di gestione client**: nessuna orchestrazione, misurazione del software, integrazione di terze parti, sequenza di attività o supporto di Software Center.

- **Supporto limitato**per i dispositivi: MDM locale non supporta il numero di versioni del sistema operativo del client Configuration Manager. Per altre informazioni, vedere [Versioni dei sistemi operativi supportate per client e dispositivi](/configmgr/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#bkmk_OnpremOS).

## <a name="next-step"></a>Passaggio successivo

Informazioni sugli elementi da considerare quando si configura l'infrastruttura Configuration Manager e si pianifica la registrazione dei dispositivi in MDM locale.

> [!div class="nextstepaction"]
> [Pianificare la gestione dei dispositivi mobili locale](/configmgr/mdm/plan-design/plan-on-premises-mdm)  

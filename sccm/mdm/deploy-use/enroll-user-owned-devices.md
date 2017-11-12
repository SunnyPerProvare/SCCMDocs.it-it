---
title: "Registrare i dispositivi di proprietà dell'utente per le distribuzioni ibride"
titleSuffix: Configuration Manager
description: "Informazioni sui vari metodi per registrare i dispositivi di proprietà dell'utente per le distribuzioni ibride con Configuration Manager."
ms.custom: na
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bdaa8a7-6a64-4b0e-b617-309dcd912c45
caps.latest.revision: "13"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 9bc0e23680ff2c7a5099938e546e50e03f998f5e
ms.sourcegitcommit: 1132886e07d0c0a87dcc7eeef4577dd8d8840023
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/01/2017
---
# <a name="enroll-user-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>Registrare i dispositivi di proprietà dell'utente per le distribuzioni ibride con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I dispositivi di proprietà degli utenti possono essere inseriti nella gestione tramite la registrazione, un processo spesso chiamato "bring your own device" o semplicemente "BYOD". A tale scopo, gli utenti installano l'app del Portale aziendale ed eseguono l'accesso al dispositivo (iOS, macOS e Android) oppure aggiungono un account aziendale o dell'istituto di istruzione al dispositivo e un dominio (Windows). Con questo processo si registra il dispositivo in Intune, assegnando all'utente l'accesso alle risorse gestite da Intune e consentendo a Intune di gestire alcune impostazioni del dispositivo, ad esempio la richiesta di un PIN.

Per visualizzare i dispositivi nella gestione, come amministratore, è innanzitutto necessario [impostare la gestione dei dispositivi mobili](setup-hybrid-mdm.md) e [abilitare la registrazione](enable-platform-enrollment.md). Dopo aver abilitato la registrazione, gli utenti possono registrare i propri dispositivi. Vedere [Come informare gli utenti finali su Microsoft Intune](https://docs.microsoft.com/intune/end-user-educate) per indicazioni e procedure da condividere con gli utenti.

Le aziende o gli istituti di istruzione che acquistano dispositivi possono approfittare dei programmi che consentono la [gestione dei dispositivi di proprietà aziendale](enroll-company-owned-devices.md).

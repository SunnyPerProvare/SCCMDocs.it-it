---
title: Registrare i dispositivi di proprietà dell'utente per le distribuzioni ibride
titleSuffix: Configuration Manager
description: Informazioni sui vari metodi per registrare i dispositivi di proprietà dell'utente per le distribuzioni ibride con Configuration Manager.
ms.date: 09/08/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 2bdaa8a7-6a64-4b0e-b617-309dcd912c45
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 957461561386c85512c69d77bf92ea7669064c8c
ms.sourcegitcommit: 7f64c5fb3e9fa3dba006af618b1f1ceaf61a99f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/28/2019
ms.locfileid: "75520763"
---
# <a name="enroll-user-owned-devices-for-hybrid-deployments-with-configuration-manager"></a>Registrare i dispositivi di proprietà dell'utente per le distribuzioni ibride con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

I dispositivi di proprietà degli utenti possono essere inseriti nella gestione tramite la registrazione, un processo spesso chiamato "bring your own device" o semplicemente "BYOD". A tale scopo, gli utenti installano l'app del Portale aziendale ed eseguono l'accesso al dispositivo (iOS, macOS e Android) oppure aggiungono un account aziendale o dell'istituto di istruzione al dispositivo e un dominio (Windows). Con questo processo si registra il dispositivo in Intune, assegnando all'utente l'accesso alle risorse gestite da Intune e consentendo a Intune di gestire alcune impostazioni del dispositivo, ad esempio la richiesta di un PIN.

Per visualizzare i dispositivi nella gestione, come amministratore, è innanzitutto necessario [impostare la gestione dei dispositivi mobili](setup-hybrid-mdm.md) e [abilitare la registrazione](enable-platform-enrollment.md). Dopo aver abilitato la registrazione, gli utenti possono registrare i propri dispositivi. Vedere [Come informare gli utenti finali su Microsoft Intune](https://docs.microsoft.com/intune/end-user-educate) per indicazioni e procedure da condividere con gli utenti.

Le aziende o gli istituti di istruzione che acquistano dispositivi possono approfittare dei programmi che consentono la [gestione dei dispositivi di proprietà aziendale](enroll-company-owned-devices.md).

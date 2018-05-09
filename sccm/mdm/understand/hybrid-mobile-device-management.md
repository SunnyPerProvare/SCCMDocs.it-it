---
title: Gestione di dispositivi mobili (MDM) ibrida con Microsoft Intune
titleSuffix: Configuration Manager
description: Informazioni sulla gestione di dispositivi mobili ibrida con System Center Configuration Manager e Microsoft Intune.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c8651b5a82c4e3cb4e39fac53cc5bc3357df6e47
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Gestione di dispositivi mobili ibridi con System Center Configuration Manager e Microsoft Intune

*Si applica a: System Center Configuration Manager (Current Branch)*


Configuration Manager Microsoft Intune consentono di gestire dispositivi iOS, Windows e Android. Tutte le attività di gestione vengono gestite dalla console di Configuration Manager in cui si esegue il resto delle attività di gestione, integrate perfettamente con il servizio online di Microsoft Intune via Internet.  È possibile configurare Configuration Manager per consentire agli utenti di accedere alle risorse aziendali dai propri dispositivi in modo protetto e gestito. Usando la gestione di dispositivi si proteggono i dati aziendali e si dà la possibilità agli utenti di registrare i propri dispositivi mobili personali o di proprietà dell'azienda per l'accesso ai dati aziendali. Funzionalità di gestione nei dispositivi:

-   Ritirare e cancellare dispositivi
-   Configurare le impostazioni di conformità come le password, la protezione, il roaming, la crittografia e le comunicazioni wireless
-   Distribuire app line-of-business (LOB) ai dispositivi
-   Distribuire le app ai dispositivi che si connettono a Windows Store, Windows Phone Store, App Store o Google Play
-   Raccogliere l'inventario hardware
-   Raccogliere l'inventario software usando i report incorporati

Per informazioni sulle nuove funzionalità disponibili per il software MDM ibrido, vedere [What's new in hybrid mobile device management](../understand/whats-new-in-hybrid-mobile-device-management.md) (Novità della gestione di dispositivi mobili ibrida).

Questo documento presuppone che si stia usando Configuration Manager per gestire i computer e che si abbia intenzione di estendere la console di Configuration Manager con Intune per gestire i dispositivi mobili. Per comprendere le differenze tra Intune e la gestione di dispositivi mobili ibrida, vedere [Scegliere tra Microsoft Intune autonomo e la gestione di dispositivi mobili ibrida con System Center Configuration Manager](choose-between-standalone-intune-and-hybrid-mobile-device-management.md).

Dopo aver esteso Configuration Manager con Intune è possibile concedere agli utenti le autorizzazioni per registrare i propri dispositivi personali o per registrare e gestire i dispositivi di proprietà dell'azienda. È anche possibile gestire i dispositivi aziendali con Intune usando Configuration Manager.

## <a name="hybrid-mdm-enrollment"></a>Registrazione di software MDM ibrida
Per introdurre i dispositivi nella gestione ibrida, i dispositivi devono essere registrati nel servizio. La modalità di registrazione dei dispositivi varia a seconda del tipo di dispositivo in uso, della proprietà e del livello di gestione necessario.
- La registrazione BYOD (Bring Your Own Device) consente agli utenti di registrare i telefoni, i tablet o i PC personali.
- La registrazione dei dispositivi di proprietà dell'azienda (COD) rende possibili scenari di gestione come la cancellazione remota, i dispositivi condivisi o l'affinità utente per un dispositivo.
- Se si usa [Exchange ActiveSync](../plan-design/device-enrollment-methods.md#mobile-device-management-with-exchange-activesync-and-configuration-manager), sia in locale che ospitato nel cloud, è possibile abilitare la gestione semplice con Intune, senza registrazione. I PC Windows possono essere anche gestiti tramite il [software client di Intune](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).

---
title: Gestire le applicazioni
titleSuffix: Configuration Manager
description: Gestire le applicazioni in Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 563e7fe79658e310fdaf3da1b14f8ff0163691b5
ms.sourcegitcommit: 7f64c5fb3e9fa3dba006af618b1f1ceaf61a99f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/28/2019
ms.locfileid: "75520491"
---
# <a name="manage-applications-in-configuration-manager"></a>Gestire le applicazioni in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Quando si gestiscono dispositivi tramite la gestione dei dispositivi locale di Microsoft Intune o Configuration Manager, è possibile gestire questi tipi di applicazione aggiuntivi:
- Pacchetto app Windows Phone (file *.xap)
- Pacchetto app per iOS (file *.ipa)
- Pacchetto app per Android (file *.apk)
- Pacchetto app Android in Google Play
- Pacchetto app Windows Phone (in Windows Phone Store)
- Windows Installer tramite MDM
- Applicazione Web

Questa sezione contiene informazioni dettagliate sulla creazione e la gestione di applicazioni tramite una MDM ibrida o una MDM locale.

Le [attività di gestione per applicazioni Configuration Manager](../../apps/deploy-use/management-tasks-applications.md) forniscono informazioni più generali sulla gestione di Configuration Manager applicazioni e tipi di distribuzione.

## <a name="deploying-and-monitoring-apps"></a>Distribuzione e monitoraggio di app

La distribuzione e il monitoraggio delle applicazioni in Configuration Manager sono gli stessi processi per i dispositivi mobili, come per i dispositivi in loco, ad esempio computer portatili e desktop. Per informazioni generali sulla distribuzione e il monitoraggio delle applicazioni, vedere gli argomenti seguenti:

- [Distribuire applicazioni](../../apps/deploy-use/deploy-applications.md)
- [Monitorare le applicazioni](../../apps/deploy-use/monitor-applications-from-the-console.md)

Di seguito sono riportate alcune considerazioni specifiche per la gestione dei dispositivi mobili da tenere presenti durante la distribuzione e il monitoraggio delle applicazioni.

- I dispositivi registrati con MDM non supportano le distribuzioni simulate, l'esperienza utente o le impostazioni di pianificazione.

- Non aggiungere più di 100 impostazioni locali a una singola app. L'aggiunta di più di 100 impostazioni locali impedisce la sincronizzazione dell'app con Intune. Questa azione impedisce anche l'installazione o la disponibilità dell'app per l'installazione nel dispositivo.

- È possibile associare la distribuzione a criteri di configurazione dell'app iOS, se già configurati. Vedere [Configurare le app iOS con i criteri di configurazione delle app](configure-ios-apps-with-app-configuration-policies.md).

### <a name="next-steps"></a>Passaggi successivi

Dopo un certo periodo di tempo, può essere opportuno apportare modifiche a un'applicazione, disinstallarla o sostituire un'applicazione già distribuita con una nuova. Leggere [le applicazioni Update e Tire con Configuration Manager](../../apps/deploy-use/update-and-retire-applications.md) per comprendere queste funzionalità.

---
title: Gestire le applicazioni
titleSuffix: Configuration Manager
description: Gestire applicazioni in System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 26aff6a374da4c6822943083b24c1a7ac04ee91d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="manage-applications-in-system-center-configuration-manager"></a>Gestire applicazioni in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Quando si gestiscono dispositivi tramite la gestione dei dispositivi locale di Microsoft Intune o Configuration Manager, è possibile gestire questi tipi di applicazione aggiuntivi:
- Pacchetto app Windows Phone (file *.xap)
- Pacchetto app per iOS (file *.ipa)
- Pacchetto app per Android (file *.apk)
- Pacchetto app Android in Google Play
- Pacchetto app Windows Phone (in Windows Phone Store)
- Windows Installer tramite MDM
- Applicazione Web

Questa sezione contiene informazioni dettagliate sulla creazione e la gestione di applicazioni tramite una MDM ibrida o una MDM locale.

L'articolo [Attività di gestione per applicazioni di System Center Configuration Manager](../../apps/deploy-use/management-tasks-applications.md) contiene informazioni generali sulla gestione delle applicazioni e dei tipi di distribuzione di System Center Configuration Manager.

## <a name="deploying-and-monitoring-apps"></a>Distribuzione e monitoraggio di app

I processi di distribuzione e monitoraggio delle applicazioni in System Center Configuration Manager sono identici per i dispositivi mobili e per quelli locali, come computer portatili e desktop. Per informazioni generali sulla distribuzione e il monitoraggio delle applicazioni, vedere gli argomenti seguenti:

- [Distribuire applicazioni in System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md)
- [Monitorare applicazioni in System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md)

Di seguito sono riportate alcune considerazioni specifiche per la gestione dei dispositivi mobili da tenere presenti durante la distribuzione e il monitoraggio delle applicazioni.

- I dispositivi registrati con MDM non supportano le distribuzioni simulate, l'esperienza utente o le impostazioni di pianificazione.

- È possibile associare la distribuzione a criteri di configurazione dell'app iOS, se già configurati. Vedere [Configurare le app iOS con i criteri di configurazione delle app](configure-ios-apps-with-app-configuration-policies.md).

### <a name="next-steps"></a>Passaggi successivi

Dopo un certo periodo di tempo, può essere opportuno apportare modifiche a un'applicazione, disinstallarla o sostituire un'applicazione già distribuita con una nuova. Per comprendere queste funzionalità, vedere [Aggiornare e ritirare le applicazioni con System Center Configuration Manager](../../apps/deploy-use/update-and-retire-applications.md).

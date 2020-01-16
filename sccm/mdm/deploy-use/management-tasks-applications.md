---
title: Gestire le app per MDM locale
titleSuffix: Configuration Manager
description: Gestire le applicazioni per la gestione di dispositivi mobili (MDM) locale in Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 8adbe2e2-de26-4a80-8bbd-a5f34b8bac79
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 660975049ef91ad19e08eb18fa6c557106fbe783
ms.sourcegitcommit: 4ca147f2bb3de35bd5089743c832e00bc3babd19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/15/2020
ms.locfileid: "76032698"
---
# <a name="manage-apps-for-on-premises-mdm-in-configuration-manager"></a>Gestire le app per MDM locale in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Quando si gestiscono i dispositivi con Configuration Manager gestione di dispositivi mobili (MDM) locale, è possibile gestire i tipi di applicazioni seguenti:

- Pacchetto app Windows Phone (file *.xap)
- Pacchetto app Windows Phone (in Windows Phone Store)
- Windows Installer tramite MDM
- Applicazione Web

Per informazioni più generali sulla gestione di applicazioni Configuration Manager e sui tipi di distribuzione, vedere [attività di gestione per le applicazioni Configuration Manager](/configmgr/apps/deploy-use/management-tasks-applications).

## <a name="bkmk_winphone"></a>Crea applicazione Windows Phone

Le applicazioni di Configuration Manager hanno uno o più tipi di distribuzione, Il tipo di distribuzione include i file di installazione e le informazioni necessarie per distribuire il software in un dispositivo. Un tipo di distribuzione contiene anche le regole che specificano quando e come deve essere distribuito il software.

Per la procedura generale per creare un'app e i tipi di distribuzione, vedere [creare un'applicazione](/configmgr/apps/deploy-use/create-applications#bkmk_create).

Configuration Manager supporta i tipi di file di app seguenti per i dispositivi Windows Mobile:

|Tipo di dispositivo|Tipi di file supportati|
|-----------------|---------------------|
|Windows Phone 8|xap|
|Windows Phone 8.1|xap, appx, appxbundle|
|Windows 10 Mobile|xap, appx, appxbundle|

Distribuire le app di Windows Phone come **disponibili** oppure **obbligatorie**. Usare le distribuzioni anche per disinstallare le app.

## <a name="deploy-and-monitor-apps"></a>Distribuire e monitorare le app

Distribuire e monitorare le applicazioni per i dispositivi mobili in Configuration Manager come per altri dispositivi, ad esempio desktop e server. Per altre informazioni, vedere gli articoli seguenti:

- [Distribuire applicazioni](/configmgr/apps/deploy-use/deploy-applications)
- [Monitorare le applicazioni](/configmgr/apps/deploy-use/monitor-applications-from-the-console)

Esaminare le limitazioni seguenti specifiche per i dispositivi mobili:

- I dispositivi registrati con MDM non supportano le distribuzioni simulate, l'esperienza utente o le impostazioni di pianificazione.

- Non aggiungere più di 100 impostazioni locali a una singola app. Questa azione impedisce l'installazione dell'app nel dispositivo.

## <a name="next-step"></a>Passaggio successivo

Per apportare modifiche, disinstallare o sostituire un'applicazione distribuita con una nuova applicazione, gestirla come qualsiasi app in Configuration Manager. Per altre informazioni, vedere [Aggiornare e ritirare le applicazioni](/configmgr/apps/deploy-use/update-and-retire-applications).

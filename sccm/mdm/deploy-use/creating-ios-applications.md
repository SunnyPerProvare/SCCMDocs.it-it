---
title: Creare applicazioni iOS
titleSuffix: Configuration Manager
description: Informazioni su come creare e distribuire applicazioni per dispositivi iOS in Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ff633013-5313-4cd3-949c-56d45e777280
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 246ca26b8fab3a1006e8d72b803c298fe48df9df
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385236"
---
# <a name="create-ios-applications-in-configuration-manager"></a>Creare applicazioni iOS in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Un'applicazione di Configuration Manager contiene uno o più tipi di distribuzione che comprendono le informazioni e i file di installazione necessari per distribuire software in un dispositivo. Un tipo di distribuzione contiene anche le regole che specificano quando e come deve essere distribuito il software.  

Per la procedura necessaria per creare le applicazioni e i tipi di distribuzione di Configuration Manager, vedere l'articolo su come [creare un'applicazione](/sccm/apps/deploy-use/create-applications#bkmk_create). 

Tenere presenti le seguenti considerazioni quando si creano e si distribuiscono applicazioni per i dispositivi iOS:  

- Configuration Manager supporta la distribuzione dei pacchetti iOS con estensione ipa. Quando si importa un'app iOS, non è necessario specificare un file di elenco di proprietà con estensione plist. 

- Distribuire le applicazioni iOS come **disponibili** oppure **obbligatorie**. L'utente deve accettare l'installazione e la disinstallazione.

> [!IMPORTANT]  
>  Al momento gli utenti finali non possono installare app aziendali dall'app Portale aziendale di Microsoft Intune per iOS. Questa limitazione è dovuta alle restrizioni relative alle app pubblicate nell'App Store iOS. Vedere la sezione 2 delle linee guida di revisione dell'App Store. Gli utenti possono installare app aziendali passando al portale di Intune nel proprio dispositivo. Tali app includono quelle gestite dell'App Store e i pacchetti di app line-of-business. Per altre informazioni sulle funzionalità di gestione dei dispositivi mobili offerte dall'app Portale aziendale di Intune, vedere l'articolo sulle [funzionalità di gestione dei dispositivi registrati in Microsoft Intune](https://docs.microsoft.com/intune/device-enrollment).  

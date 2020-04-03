---
title: Registrare i dispositivi per la gestione dei dispositivi mobili locale
titleSuffix: Configuration Manager
description: Informazioni sui metodi per registrare i dispositivi per la gestione di dispositivi mobili (MDM) locale in Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c295d0ad7b264e744c121ec5b7941d46a0391be8
ms.sourcegitcommit: ccc3c929b5585c05d562020e68044de7d7e11c6a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2020
ms.locfileid: "80605488"
---
# <a name="enroll-devices-for-on-premises-mdm-in-configuration-manager"></a>Registrare i dispositivi per MDM locale in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Per gestire i dispositivi con Configuration Manager gestione di dispositivi mobili (MDM) locale, è prima necessario registrarli. Quindi Configuration Manager possibile comunicare con i dispositivi per le attività di gestione. Configuration Manager fornisce due metodi per registrare i dispositivi:

- **Registrazione utente**: gli utenti avviano il processo di registrazione sul dispositivo. Affinché la registrazione utente abbia esito positivo, installare il certificato radice attendibile nel dispositivo ed effettuare il provisioning dell'utente per la registrazione nelle impostazioni client. Per registrare un dispositivo, l'utente deve solo immettere le proprie credenziali.

    Per altre informazioni, vedere [come gli utenti registrano i dispositivi](/configmgr/mdm/deploy-use/user-enroll-devices-on-premises-mdm).

- **Registrazione in blocco**: l'utente del dispositivo non avvia la registrazione. È possibile creare un pacchetto di registrazione in blocco in Configuration Manager. Quando viene aperto nel dispositivo, il pacchetto fornisce le informazioni necessarie per registrare il dispositivo.

    Per ulteriori informazioni, vedere [come registrare in blocco i dispositivi](/configmgr/mdm/deploy-use/bulk-enroll-devices-on-premises-mdm).

Per altre informazioni sulle versioni del sistema operativo che Configuration Manager supporta per la registrazione dei dispositivi in MDM locale, vedere [configurazioni supportate](/configmgr/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#bkmk_OnpremOS).

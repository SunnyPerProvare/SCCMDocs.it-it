---
title: Pianificare MDM locale
titleSuffix: Configuration Manager
description: Pianificare la gestione dei dispositivi mobili locale per gestire i dispositivi mobili in Configuration Manager
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 74f08edddca93cf7f9005630973e06cba6fef920
ms.sourcegitcommit: ccc3c929b5585c05d562020e68044de7d7e11c6a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2020
ms.locfileid: "80605313"
---
# <a name="plan-for-on-premises-mdm-in-configuration-manager"></a>Pianificare la gestione dei dispositivi mobili locale in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Quando si prevede di implementare la gestione di dispositivi mobili (MDM) locale in Configuration Manager, è necessario esaminare diverse aree principali:

- Dispositivi supportati e versioni del sistema operativo
- Ruoli del sistema del sito richiesti
- Comunicazione protetta
- Registrazione del dispositivo

> [!IMPORTANT]
> Mentre il sito o qualsiasi dispositivo mobile non si connette a Microsoft Intune, l'organizzazione richiede ancora le licenze di Intune per usare questa funzionalità. Per ulteriori informazioni, vedere [Microsoft Intune Licensing](https://docs.microsoft.com/intune/fundamentals/licenses).

Considerare i requisiti seguenti prima di preparare l'infrastruttura di Configuration Manager per la gestione di MDM locale.

## <a name="supported-devices"></a><a name="bkmk_devices"></a> Dispositivi supportati  

Current Branch of Configuration Manager supporta la registrazione nella gestione dei dispositivi mobili locale per i dispositivi che eseguono Windows 10. Questi tipi di dispositivi includono principalmente computer portatili, Internet e Surface Hub. Per altre informazioni e per l'elenco di edizioni specifiche, vedere [versioni del sistema operativo supportate per client e dispositivi](/configmgr/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#bkmk_OnpremOS).

## <a name="site-system-roles"></a><a name="bkmk_roles"></a>Ruoli di sistema del sito

MDM locale richiede almeno uno dei seguenti ruoli del sistema del sito:

- **Punto proxy di registrazione** per supportare le richieste di registrazione.

- **Punto di registrazione** per supportare la registrazione dei dispositivi.

- **Punto gestione periferiche** per la distribuzione dei criteri. Questo ruolo è una variante del punto di gestione, ma consente la gestione dei dispositivi mobili.

- **Punto di distribuzione** per la distribuzione di contenuti.

A seconda delle esigenze dell'organizzazione, è possibile installare questi ruoli nel singolo server o separatamente in server diversi.

> [!NOTE]
> È necessario configurare ogni ruolo usato per MDM locale come endpoint HTTPS per comunicare con dispositivi attendibili. Per altre informazioni, vedere [Comunicazioni attendibili richieste](#bkmk_trustedComs).

Per informazioni più generali, vedere [pianificare i server e i ruoli del sistema del sito](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles).

## <a name="trusted-communications"></a><a name="bkmk_trustedComs"></a>Comunicazioni attendibili

MDM locale richiede l'abilitazione dei ruoli del sistema del sito per le comunicazioni HTTPS. A seconda delle esigenze, è possibile usare l'autorità di certificazione (CA) dell'organizzazione per stabilire le connessioni attendibili tra i server e i dispositivi. È anche possibile usare una CA disponibile pubblicamente come autorità attendibile. In entrambi i casi, è necessario configurare i certificati seguenti:

- Un **certificato del server Web** in IIS nei server che ospitano i ruoli del sistema del sito richiesti. Se un server ospita più ruoli del sistema del sito, è necessario solo un certificato per tale server. Se ogni ruolo si trova in un server separato, per ogni server è necessario un certificato separato.

- Il **certificato radice attendibile** della CA che rilascia i certificati del server Web. Installare questo certificato radice in tutti i dispositivi che devono connettersi ai ruoli del sistema del sito.

Per altre informazioni, vedere [configurare i certificati per le comunicazioni attendibili in MDM locale](/sccm/mdm/get-started/set-up-certificates-on-premises-mdm).

## <a name="device-enrollment"></a><a name="bkmk_enrollment"></a>Registrazione del dispositivo

Per abilitare la registrazione del dispositivo per MDM locale:

- Concedere agli utenti le autorizzazioni per la registrazione tramite le impostazioni client

- Configurare i dispositivi per le comunicazioni attendibili con i server del sistema del sito che ospitano i ruoli necessari

In alternativa alla registrazione avviata dall'utente, è possibile configurare un pacchetto di registrazione in blocco. Questo pacchetto consente la registrazione del dispositivo senza l'intervento dell'utente. Distribuire il pacchetto al dispositivo prima di eseguirne il provisioning per l'uso o dopo aver eseguito il processo OOBE.

Per altre informazioni, vedere [configurare la registrazione dei dispositivi per MDM locale](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm).

## <a name="next-step"></a>Passaggio successivo

> [!div class="nextstepaction"]
> [Installare i ruoli del sistema del sito](/configmgr/mdm/get-started/install-site-system-roles-for-on-premises-mdm)

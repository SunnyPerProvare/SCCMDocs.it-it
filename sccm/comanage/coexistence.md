---
title: Coesistenza di gestioni dei dati master di terze parti
titleSuffix: Configuration Manager
description: Informazioni sull'uso di un servizio MDM di terze parti con Configuration Manager
ms.date: 05/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: ed4dc65e-e5d5-4f75-88ac-f4849ec8fc10
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3dce1e4a2719dc6f36ebd1ba4449e477640f6ba8
ms.sourcegitcommit: ccc3c929b5585c05d562020e68044de7d7e11c6a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2020
ms.locfileid: "80596445"
---
# <a name="third-party-mdm-coexistence-with-configuration-manager"></a>Coesistenza di servizi MDM di terze parti con Configuration Manager

Quando si gestiscono i dispositivi Windows 10 contemporaneamente tramite Configuration Manager e Microsoft Intune, questa funzionalità è detta [co-gestione](/sccm/comanage/overview). Quando si gestiscono i dispositivi con Configuration Manager e ci si iscrive a un servizio MDM di terze parti, questa funzionalità è detta *coesistenza*. La disponibilità di due autorità di gestione per un singolo dispositivo può essere problematica se non si implementa la corretta orchestrazione tra le due. Con la co-gestione, Configuration Manager e Intune bilanciano i [carichi di lavoro](/sccm/comanage/workloads) per assicurare che non si verifichino conflitti. Questa interazione non esiste con i servizi di terze parti, quindi le funzionalità di gestione della coesistenza presentano limitazioni.

Il client Configuration Manager può coesistere con un servizio MDM di terze parti in un dispositivo con Windows 10 versione 1709 o successiva, aggiunto ad Azure Active Directory. Il dispositivo può essere di uno dei due tipi seguenti:

- [Aggiunto solo ad Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan). Questo tipo è anche noto come "aggiunto a un dominio cloud".  

- [Aggiunto a dominio ibrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan), per cui il dispositivo è aggiunto ad Active Directory locale e registrato in Azure Active Directory.  

> [!Note]  
> I [dispositivi di proprietà personale](https://docs.microsoft.com/windows/client-management/mdm/mdm-enrollment-of-windows-devices#connecting-personally-owned-devices-bring-your-own-device) non sono supportati.  

Quando il client Configuration Manager rileva che il dispositivo viene gestito anche da un servizio MDM di terze parti, disattiva automaticamente determinati carichi di lavoro di Configuration Manager. Questo comportamento consente al servizio MDM di acquisire queste funzioni. Evita inoltre l'uso di impostazioni in conflitto nel client che potrebbero influire negativamente sul dispositivo e sull'esperienza utente. In questo caso vengono disattivati i carichi di lavoro seguenti in Configuration Manager:

- Criteri di accesso alle risorse per le impostazioni relative a VPN, Wi-Fi, posta elettronica e certificati
- Gestione delle applicazioni, inclusi i pacchetti legacy
- Ricerca e installazione di aggiornamenti software
- Protezione degli endpoint, la famiglia di funzionalità di protezione antimalware di Windows Defender
- Criteri di conformità per l'accesso condizionale
- Configurazione del dispositivo
- Gestione di Office A portata di clic

Il client Configuration Manager evita il conflitto con l'autorità di gestione di terze parti continuando a eseguire le operazioni di sola lettura seguenti:

- Inventario hardware e software
- Asset Intelligence
- Controllo del software
- Report sul risparmio energia

Per altre informazioni sui vantaggi della co-gestione con Configuration Manager e Intune, vedere [Vantaggi della co-gestione](/sccm/comanage/overview#benefits).

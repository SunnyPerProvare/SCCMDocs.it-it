---
title: Metodi di registrazione dei dispositivi per MDM ibrida | Microsoft Docs
description: Metodi di registrazione dei dispositivi per una MDM ibrida.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: b81d06dc-3844-4117-9937-16732a227994
caps.latest.revision: 9
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: c38b3bae681821a886bfdab66d71cd6067adc425
ms.lasthandoff: 03/06/2017


---
# <a name="overview-of-device-enrollment-methods"></a>Panoramica dei metodi di registrazione dei dispositivi

*Si applica a: System Center Configuration Manager (Current Branch)*

Dopo aver esteso Configuration Manager con Intune, è possibile registrare e gestire i dispositivi aziendali o concedere agli utenti l'autorizzazione di registrare i dispositivi personali. È anche possibile gestire i dispositivi aziendali con Intune usando Configuration Manager.

La tabella seguente illustra i metodi di registrazione con le relative funzionalità supportate. Queste funzionalità includono:
- **Cancellazione**: ripristino delle impostazioni predefinite del dispositivo, con rimozione di tutti i dati. [Ritiro di dispositivi](../deploy-use/wipe-lock-reset-devices.md)
- **Affinità**: associazione dei dispositivi agli utenti. Obbligatoria per la gestione di applicazioni per dispositivi mobili (MAM) e l'accesso condizionale ai dati aziendali. [Affinità utente](../deploy-use/user-affinity-for-hybrid-managed-devices.md)
- **Blocco**: impedisce agli utenti di rimuovere il dispositivo dal sistema di gestione. Per il blocco dei dispositivi iOS è richiesta la modalità con supervisione. [Blocco remoto](../deploy-use/wipe-lock-reset-devices.md#remote-lock)

**Metodi di registrazione iOS**

| **Metodo** |    **Cancellazione** |    **Affinità**    |    **Blocco** | **Informazioni dettagliate** |
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | No|    Yes |    No | [altro](../deploy-use/enable-platform-enrollment.md)|
|**[DEM](#dem)**|    No |No |No    | [altro](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|
|**[DEP](#dep)**|    Sì |    Facoltativo |    Facoltativo|[altro](../deploy-use/ios-device-enrollment-program-for-hybrid.md)|
|**[USB-SA](#usb-sa)**|    Sì |    Facoltativo |    No| [altro](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)|

**Metodi di registrazione per Android e Windows**

| **Metodo** |    **Cancellazione** |    **Affinità**    |    **Blocco** | **Informazioni dettagliate**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | No|    Yes |    No | [altro](../deploy-use/enroll-hybrid-windows.md)|
|**[DEM](#dem)**|    No |No |No    |[altro](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|

Per una serie di domande e risposte utili per individuare il metodo corretto, vedere [Scegliere come registrare i dispositivi mobili](/intune/get-started/choose-how-to-enroll-devices1).

## <a name="byod"></a>BYOD
Gli utenti BYOD (Bring Your Own Device) installano l'app del portale aziendale e registrano il dispositivo di loro proprietà. Ciò consente agli utenti di connettersi alla rete aziendale, entrando a far parte del dominio o di Azure Active Directory. L'attivazione della registrazione BYOD costituisce un prerequisito per molti scenari di dispositivi di proprietà dell'azienda per la maggior parte delle piattaforme. Vedere [Setup hybrid MDM](../deploy-use/setup-hybrid-mdm.md) (Configurare la gestione di dispositivi mobili ibrida). ([Torna alla tabella](#overview-of-device-enrollment-methods))

## <a name="corporate-owned-devices"></a>Dispositivi di proprietà dell'azienda
I dispositivi di proprietà dell'azienda possono essere gestiti con la console di Configuration Manager. I dispositivi iOS possono essere registrati direttamente tramite strumenti forniti da Apple. Tutti i tipi di dispositivo possono essere registrati da un amministratore o da un responsabile usando il manager di registrazione dispositivi. È anche possibile identificare e contrassegnare come dispositivi di proprietà dell'azienda i dispositivi con numero IMEI e abilitare questo tipo di registrazione.

[Enroll corporate-owned devices](../deploy-use/enroll-company-owned-devices.md) (Registrare dispositivi di proprietà dell'azienda)

### <a name="dem"></a>DEM
Il manager di registrazione dispositivi è un account utente speciale usato per registrare e gestire più dispositivi di proprietà dell'azienda. I responsabili possono installare il portale aziendale e registrare molti dispositivi senza utente associato. Altre informazioni su [DEM](../deploy-use/enroll-devices-with-device-enrollment-manager.md). ([Torna alla tabella](#overview-of-device-enrollment-methods))

### <a name="dep"></a>DEP
La gestione tramite il programma DEP (Device Enrollment Program) di Apple consente di creare e distribuire criteri in modalità wireless ai dispositivi iOS acquistati e gestiti tramite questo programma. Un dispositivo viene registrato quando l'utente lo accende per la prima volta ed esegue Assistente configurazione di iOS. Questo metodo supporta la modalità **iOS Supervised** (Con supervisione iOS), che a sua volta abilita:
  -    Registrazione bloccata
  -    Accesso condizionale
  -    Rilevamento jailbreak
  -    Gestione per applicazioni mobili

Altre informazioni su [DEP](../deploy-use/ios-device-enrollment-program-for-hybrid.md). ([Torna alla tabella](#overview-of-device-enrollment-methods))

### <a name="usb-sa"></a>USB-SA
Registrazione con Assistente configurazione con connessione USB. L'amministratore crea i criteri e li esporta in Apple Configurator. I dispositivi di proprietà dell'azienda connessi tramite USB vengono preparati con i criteri. L'amministratore deve registrare ogni dispositivo manualmente. Gli utenti ricevono i propri dispositivi ed eseguono Assistente configurazione per registrarli. Questo metodo supporta la modalità **iOS Supervised** (Con supervisione iOS), che a sua volta abilita:
  -    Accesso condizionale
  -    Rilevamento jailbreak
  -    Gestione per applicazioni mobili

Altre informazioni sulla [registrazione tramite Assistente configurazione con Apple Configurator](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md). ([Torna alla tabella](#overview-of-device-enrollment-methods))

## <a name="mobile-device-management-with-exchange-activesync-and-configuration-manager"></a>Gestione dei dispositivi mobili con Exchange ActiveSync e Configuration Manager
I dispositivi mobili non registrati ma connessi a Exchange ActiveSync possono essere gestiti da Intune mediante i criteri di gestione di dispositivi mobili di EAS. Intune usa Exchange Connector per comunicare con EAS, in locale e ospitato nel cloud.

[Manage mobile devices with System Center Configuration Manager and Exchange](../deploy-use/manage-mobile-devices-with-exchange-activesync.md) (Gestione di dispositivi mobili con System Center Configuration Manager ed Exchange)

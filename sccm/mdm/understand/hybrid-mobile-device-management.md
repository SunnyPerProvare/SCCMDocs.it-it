---
title: Gestione di dispositivi mobili ibrida con System Center Configuration Manager e Microsoft Intune | Microsoft Docs
description: Informazioni sulla gestione di dispositivi mobili ibrida con System Center Configuration Manager e Microsoft Intune.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
caps.latest.revision: 34
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 238ef5814c0c1b832c28d63c9f3879e21a6c439b
ms.openlocfilehash: caedfa2f89daf9ebad72602161dd618f0d18b4ab

---
# <a name="hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune

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
Per introdurre i dispositivi nella gestione ibrida, i dispositivi devono essere registrati nel servizio. La modalità di registrazione dei dispositivi varia a seconda del tipo di dispositivo in uso, della proprietà e del livello di gestione necessario. La registrazione BYOD (Bring Your Own Device) consente agli utenti di registrare i telefoni, i tablet o i PC personali. La registrazione dei dispositivi di proprietà dell'azienda (COD) rende possibili scenari di gestione come la cancellazione remota, i dispositivi condivisi o l'affinità utente per un dispositivo.

 Se si usa [Exchange ActiveSync](#mobile-device-management-with-exchange-activesync-and-configuration-manager), sia in locale che ospitato nel cloud, è possibile abilitare la gestione semplice con Intune, senza registrazione. I PC Windows possono essere anche gestiti tramite il [software client di Intune](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).

## <a name="overview-of-device-enrollment-methods"></a>Panoramica dei metodi di registrazione dei dispositivi

 La tabella seguente illustra i metodi di registrazione con le relative funzionalità supportate. Queste funzionalità includono:
 - **Cancellazione**: ripristino delle impostazioni predefinite del dispositivo, con rimozione di tutti i dati. [Ritiro di dispositivi](../deploy-use/wipe-lock-reset-devices.md)
 - **Affinità**: associazione dei dispositivi agli utenti. Obbligatoria per la gestione di applicazioni per dispositivi mobili (MAM) e l'accesso condizionale ai dati aziendali. [Affinità utente](../deploy-use/user-affinity-for-hybrid-managed-devices.md)
 - **Blocco**: impedisce agli utenti di rimuovere il dispositivo dal sistema di gestione. Per il blocco dei dispositivi iOS è richiesta la modalità con supervisione. [Blocco remoto](../deploy-use/wipe-lock-reset-devices.md#remote-lock)

 **Metodi di registrazione iOS**

| **Metodo** |  **Cancellazione** |  **Affinità**    |   **Blocco** | **Informazioni dettagliate** |
|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | No|    Yes |   No | [altro](../deploy-use/setup-hybrid-mdm.md#step-6-enable-platform-enrollment)|
|**[DEM](#dem)**|   No |No |No  | [altro](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|
|**[DEP](#dep)**|   Sì |   Facoltativo |  Facoltativo|[altro](../deploy-use/ios-device-enrollment-program-for-hybrid.md)|
|**[USB-SA](#usb-sa)**| Sì |   Facoltativo |  No| [altro](../deploy-use/ios-hybrid-enrollment-using-apple-configurator.md)|

**Metodi di registrazione per Android e Windows**

| **Metodo** |  **Cancellazione** |  **Affinità**    |   **Blocco** | **Informazioni dettagliate**|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**[BYOD](#byod)** | No|    Yes |   No | [altro](../deploy-use/setup-hybrid-mdm.md#windows-enrollment-setup)|
|**[DEM](#dem)**|   No |No |No  |[altro](../deploy-use/enroll-devices-with-device-enrollment-manager.md)|

Per una serie di domande e risposte utili per individuare il metodo corretto, vedere [Scegliere come registrare i dispositivi mobili](/intune/get-started/choose-how-to-enroll-devices1).

## <a name="byod"></a>BYOD
Gli utenti BYOD (Bring Your Own Device) installano l'app Portale aziendale e registrano il dispositivo di loro proprietà. Ciò consente agli utenti di connettersi alla rete aziendale, entrando a far parte del dominio o di Azure Active Directory. L'attivazione della registrazione BYOD costituisce un prerequisito per molti scenari di dispositivi di proprietà dell'azienda per la maggior parte delle piattaforme. Vedere [Setup hybrid MDM](../deploy-use/setup-hybrid-mdm.md) (Configurare la gestione di dispositivi mobili ibrida). ([Torna alla tabella](#overview-of-device-enrollment-methods))

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


##  <a name="supported-device-platforms"></a>Piattaforme per dispositivi supportate

La gestione di dispositivi mobili ibrida di Configuration Manager consente di gestire le seguenti piattaforme per dispositivi:

[!INCLUDE[../includes/mdm-supported-devices](../includes/mdm-supported-devices.md)]

## <a name="next-steps"></a>Passaggi successivi
 - [Prerequisiti per la registrazione dei dispositivi](../deploy-use/setup-hybrid-mdm.md)
 - [Gestire i dispositivi di proprietà dell'azienda](../deploy-use/enroll-company-owned-devices.md)



<!--HONumber=Dec16_HO3-->



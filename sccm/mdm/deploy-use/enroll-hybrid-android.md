---
title: Configurare la gestione di dispositivi Android ibrida con System Center Configuration Manager e Microsoft Intune | Microsoft Docs
description: Preparare la gestione dei dispositivi mobili Android con Configuration Manager e Intune.
ms.custom: na
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c517fe34-0130-465b-a020-bdb555878778
caps.latest.revision: 9
caps.handback.revision: 0
author: nathbarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 27a92dc1c3710ff55f0b145386319dda371533d9
ms.openlocfilehash: 0e93cd55ce49afb6395dcbe758c933bf509dd367
ms.lasthandoff: 04/07/2017


---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurare la gestione di dispositivi mobili ibridi Android con System Center Configuration Manager e Microsoft Intune

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo argomento offre informazioni utili agli amministratori IT per abilitare la registrazione ibrida di dispositivi Android e Android for Work. L'amministratore IT può quindi usare System Center Configuration Manger per gestire i dispositivi tramite una sottoscrizione a Microsoft Intune configurata. Gli utenti possono scaricare da Google Play l'app Portale aziendale Android che consente di registrare dispositivi Android, inclusi i dispositivi Samsung KNOX Standard, e Android for Work. 

Gli amministratori di Configuration Manager possono gestire le impostazioni di conformità, cancellare o eliminare dispositivi Android, distribuire app e raccogliere l'inventario software e hardware. Se l'app del portale aziendale Android non è installata nei dispositivi Android, non saranno disponibili tutte le funzionalità di gestione, come le impostazioni di inventario e di conformità, ma sarà comunque possibile distribuire app nei dispositivi Android.  

## <a name="enable-android-enrollment"></a>Abilitare la registrazione di Android  
La procedura seguente consente a Configuration Manager di gestire dispositivi Android senza un profilo di lavoro, ad esempio per la registrazione "Android classica".

1. Prima di poter configurare la registrazione per una qualsiasi piattaforma, completare i prerequisiti e le procedure indicate in [Setup hybrid MDM](setup-hybrid-mdm.md) (Impostare una MDM ibrida).  
2. Nell'area di lavoro **Amministrazione** della console di Configuration Manager scegliere **Panoramica** > **Servizi cloud** > **Sottoscrizioni a Microsoft Intune** e scegliere la sottoscrizione di Intune personale.  
3. Nel gruppo **Sottoscrizione** della scheda **Home** scegliere **Configura piattaforme** > **Android**.  
4. Nella finestra di dialogo **Proprietà sottoscrizione di Microsoft Intune** scegliere la scheda **Android** e selezionare la casella di controllo **Abilita registrazione Android**.  

 Dopo aver completato la configurazione occorre informare gli utenti su come registrare i loro dispositivi. Vedere [Informazioni sull'uso di Microsoft Intune per gli utenti finali](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Queste informazioni si applicano ai dispositivi mobili gestiti sia con Microsoft Intune che con Configuration Manager.

## <a name="enable-android-for-work-enrollment"></a>Abilitare la registrazione di Android for Work
La procedura seguente consente a Configuration Manager di gestire dispositivi Android senza un profilo di lavoro, ad esempio per la registrazione "Android classica".

1. Creare un account di Google all'indirizzo https://accounts.google.com/SignUp da usare come account amministratore di Android for Work. Oppure accedere con l'account che verrà associato a tutte le attività di gestione di Android for Work per il tenant di Intune. Potrebbe trattarsi di un account di Google condiviso tra gli amministratori che gestiscono i dispositivi Android. Si tratta dell'account Google usato dall'organizzazione per gestire e pubblicare applicazioni nella console di Play for Work. Questo account verrà usato per approvare le applicazioni nello store di Play for Work, quindi è consigliabile appuntarsi nome dell'account e password.
2. Abilitare la registrazione di Android associando l'account Google al tenant di Intune gestito in Configuration Manager:
   1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager scegliere **Panoramica** > **Servizi cloud** > **Sottoscrizioni a Microsoft Intune** e scegliere la sottoscrizione di Intune personale.
   2. Nel gruppo **Sottoscrizione** della scheda **Home** scegliere **Configura piattaforme** > **Android for Work**.
   3. Nella finestra di dialogo scegliere **Configura Android for Work nella console di Intune**. La console di Intune viene aperta nel Web browser.
   4. Usare le credenziali di amministratore di Intune per accedere al portale di Intune.
   5. Scegliere **Configura** per aprire il sito Web Android for Work di Google Play.
   6. Nella pagina di accesso di Google immettere le credenziali Google dal passaggio 1 e quindi specificare le informazioni aziendali.
3. Quando si torna al portale di Intune, Android for Work è attivato e sono disponibili tre opzioni di registrazione per i dispositivi Android for Work:
   - **Gestisci tutti i dispositivi come Android** (disabilitata). Tutti i dispositivi Android, inclusi i dispositivi che supportano Android for Work, vengono registrati come dispositivi Android convenzionali.
   - **Gestisci i dispositivi supportati come Android for Work** (abilitata). Tutti i dispositivi che supportano Android for Work vengono registrati come dispositivi Android for Work. I dispositivi Android che non supportano Android for Work vengono registrati come dispositivi Android convenzionali.
   - **Gestisci i dispositivi supportati per gli utenti solo in questi gruppi come Android for Work** (abilitata solo per alcuni gruppi). Consente di destinare la gestione Android for Work a un insieme limitato di utenti. I dispositivi che supportano Android for Work vengono registrati come dispositivi Android for Work solo quando vengono registrati dai membri dei gruppi selezionati. Tutti gli altri dispositivi vengono registrati come dispositivi Android.

> [!NOTE]
> Un problema noto impedisce all'opzione **Gestisci i dispositivi supportati per gli utenti solo in questi gruppi come Android for Work** di funzionare come previsto. I dispositivi degli utenti nei gruppi Azure AD specificati saranno registrati come Android anziché Android for Work. Per abilitare Android for Work, è necessario usare l'opzione **Gestisci i dispositivi supportati come Android for Work**.


Dopo aver completato la configurazione occorre informare gli utenti su come registrare i loro dispositivi. Vedere [Informazioni sull'uso di Microsoft Intune per gli utenti finali](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Queste informazioni si applicano ai dispositivi mobili gestiti sia con Microsoft Intune che con Configuration Manager.

Il nome dell'account e il nome dell'organizzazione verranno visualizzati nel portale di Intune dopo il completamento dell'associazione. A quel punto sarà possibile chiudere entrambi i browser.

### <a name="enroll-an-android-for-work-device"></a>Registrare un dispositivo Android for Work
La procedura di registrazione dei dispositivi Android for Work è simile alla registrazione per Android. È possibile scaricare e installare l'app Portale aziendale per Android nei propri dispositivi mobili. Nell'ambito del processo di registrazione verrà chiesto di creare un profilo di lavoro. Dopo aver creato il profilo, è necessario passare alla versione gestita dell'app Portale aziendale. La versione gestita dell'app Portale aziendale è contrassegnata da una piccola valigetta arancione nell'angolo in basso a destra.

### <a name="manage-android-for-work-devices"></a>Gestire dispositivi Android for Work
Dopo aver abilitato la registrazione di dispositivi Android for Work è possibile eseguire le attività di gestione seguenti per i dispositivi Android for Work:
- [Approvare app](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [Creare elementi di configurazione](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Gestire le impostazioni di conformità](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client)
- [Gestire profili di posta elettronica](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [Cancellare in modo selettivo il profilo di lavoro](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)

> [!div class="button"]
[< Passaggio precedente](create-service-connection-point.md)  [Passaggio successivo >](set-up-additional-management.md)


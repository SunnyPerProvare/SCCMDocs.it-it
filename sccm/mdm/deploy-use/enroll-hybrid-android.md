---
title: Configurare la gestione di dispositivi Android ibrida con System Center Configuration Manager e Microsoft Intune | Microsoft Docs
description: Preparare la gestione dei dispositivi mobili Android con Configuration Manager e Intune.
ms.custom: na
ms.date: 03/05/2017
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
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 1eca422bc62f669412732ec70395d7bbf3ad9c7a
ms.lasthandoff: 03/06/2017


---
# <a name="set-up-android-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurare la gestione di dispositivi mobili ibridi Android con System Center Configuration Manager e Microsoft Intune

*Si applica a: System Center Configuration Manager (Current Branch)*

Per System Center Configuration Manager, è possibile scaricare l'app Portale aziendale Android da Google Play che consente di registrare i dispositivi Android, inclusi i dispositivi Samsung KNOX Standard. Tramite l'app del portale aziendale Android è possibile gestire le impostazioni di conformità, cancellare o eliminare dispositivi Android, distribuire app e raccogliere l'inventario software e hardware. Se l'app del portale aziendale Android non è installata nei dispositivi Android, non saranno disponibili tutte le funzionalità di gestione, come le impostazioni di inventario e di conformità, ma sarà comunque possibile distribuire app nei dispositivi Android.  

## <a name="prepare-to-manage-android-mobile-devices-with-configuration-manager-and-intune"></a>Preparare la gestione dei dispositivi Android con Configuration Manager e Intune  
 Questa procedura consente di gestire i dispositivi Android con Configuration Manager.  

#### <a name="to-enable-android-enrollment"></a>Per abilitare la registrazione di Android  

1.  **Prerequisiti**: prima di impostare la registrazione per una qualsiasi piattaforma, completare i prerequisiti e le procedure in [Setup hybrid MDM](setup-hybrid-mdm.md) (Impostare una MDM ibrida).  

2.  Nell'area di lavoro **Amministrazione** della console di Configuration Manager andare a **Servizi cloud** > **Sottoscrizioni a Microsoft Intune**.  

3.  Nel gruppo **Sottoscrizione** della scheda **Home** fare clic su **Configura piattaforme** > **Android**.  

4.  Nella finestra di dialogo **Proprietà sottoscrizione di Microsoft Intune** selezionare la scheda **Android** e fare clic per selezionare la casella di controllo **Abilita registrazione Android** .  

 Dopo aver completato la configurazione occorre informare gli utenti su come registrare i loro dispositivi. Vedere [Informazioni sull'uso di Microsoft Intune per gli utenti finali](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Queste informazioni si applicano ai dispositivi mobili gestiti sia con Microsoft Intune che con Configuration Manager.

 > [!div class="button"]
 [< Passaggio precedente](create-service-connection-point.md)  [Passaggio successivo >](set-up-additional-management.md)


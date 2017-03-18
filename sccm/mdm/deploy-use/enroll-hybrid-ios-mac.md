---
title: Configurare la gestione dei dispositivi iOS e Mac ibrida con System Center Configuration Manager e Microsoft Intune | Microsoft Docs
description: Impostare la gestione dei dispositivi iOS con System Center Configuration Manager e Microsoft Intune.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5eae4400-58ca-4c71-804c-6a585cd3df5d
caps.latest.revision: 10
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 2288be606d7d586de5dc18d640f295e823daf266
ms.lasthandoff: 03/06/2017


---
# <a name="set-up-ios-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurare la gestione dei dispositivi iOS ibrido con Microsoft Intune e System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Con Configuration Manager e Intune è possibile abilitare la registrazione dei dispositivi iOS e Mac OS X BYOD (Bring Your Own Device) perché gli utenti di iPhone, iPad e Mac possano accedere alla posta elettronica e alle risorse aziendali. Dopo aver installato l'app Portale aziendale di Intune, è possibile assegnare criteri ai relativi dispositivi. Prima di poter gestire i dispositivi iOS e Mac, è necessario importare un certificato del servizio APN (Apple Push Notification Service). Questo certificato consente a Intune di gestire i dispositivi iOS e Mac e di stabilire una connessione IP accreditata e crittografata con i servizi dell'autorità di gestione dei dispositivi mobili.  

 È anche possibile registrare i dispositivi iOS di proprietà dell'azienda.  Vedere [Registrare i dispositivi aziendali](enroll-company-owned-devices.md).  

## <a name="enable-ios-device-enrollment"></a>Abilitare la registrazione dei dispositivi iOS  
 Per supportare la registrazione di dispositivi iOS, è necessario attenersi alla procedura seguente:  

#### <a name="set-up-ios-device-enrollment-in-configuration-manager"></a>Impostare la registrazione dei dispositivi iOS in Configuration Manager  

1.  **Prerequisiti**: prima di impostare la registrazione per una qualsiasi piattaforma, completare i prerequisiti e le procedure in [Setup hybrid MDM](setup-hybrid-mdm.md) (Impostare una MDM ibrida).    

2.  **Scaricare una richiesta di firma certificato** : è necessario un file di richiesta di firma del certificato (CSR) per richiedere un certificato per il servizio APN da Apple.  

    1.  Nell'area di lavoro **Amministrazione** della console di Configuration Manager andare a **Servizi cloud**> **Sottoscrizioni a Microsoft Intune**.  

    2.  Nella scheda **Home** fare clic su **Crea richiesta certificato per servizio APN**. Si apre la finestra di dialogo **Richiesta di firma del certificato per Apple Push Notification Service** .  

    3.  **Andare** al percorso per salvare il nuovo file di richiesta di firma del certificato (csr). Salvare il file della richiesta di firma del certificato (estensione csr) in locale.  

    4.  Fare clic su **Scarica**. Il nuovo file CSR di Microsoft Intune viene scaricato e salvato da Configuration Manager. Questo file viene usato per richiedere un certificato di relazione di trust al portale Apple Push Certificates.  

3.  **Richiedere un certificato per il servizio APN di Apple** : il certificato per il servizio APN (Apple Push Notification) viene usato per stabilire una relazione di trust tra il servizio di gestione, Intune e i dispositivi iOS mobili registrati.  

    1.  Usando un browser andare al [portale Apple Push Certificates](http://go.microsoft.com/fwlink/?LinkId=269844) e accedere con il proprio ID Apple aziendale. Questo ID Apple deve essere usato in futuro per rinnovare il certificato APN.  

    2.  Completare la procedura guidata usando il file della richiesta di firma del certificato (con estensione CSR). Scaricare il certificato APNs e salvare il file PEM in locale. Questo file del certificato APN con estensione pem viene usato per stabilire una relazione di trust tra il server Apple Push Notification e l'autorità di gestione dei dispositivi mobili di Intune.  

4.  **Abilitare la registrazione e caricare il certificato APNs** : per abilitare la registrazione iOS, caricare il certificato APNs.  

    1.  Nell'area di lavoro **Amministrazione** della console di Configuration Manager andare a **Servizi cloud** > **Sottoscrizioni a Microsoft Intune**.  

    2.  Nella scheda **Home** nel gruppo **Sottoscrizione** fare clic su **Configura piattaforme** > **iOS**.  

        > [!NOTE]  
        >  Non caricare il certificato per il servizio Apple Push Notification (APNs) finché non viene abilitata la registrazione iOS nella console di Configuration Manager.  

    3.  Nella finestra di dialogo **Proprietà della sottoscrizione a Microsoft Intune** selezionare la scheda **iOS** e fare clic per selezionare la casella di controllo **Abilita registrazione iOS** .  

    4.  Fare clic su **Sfoglia**e andare al file (con estensione CER) del certificato per il servizio APN scaricato da Apple. Configuration Manager visualizza le informazioni sul certificato APNs. Fare clic su **OK** per salvare il certificato APN in Intune.  

 Dopo aver completato la configurazione occorre informare gli utenti su come registrare i loro dispositivi. Vedere [Informazioni sull'uso di Microsoft Intune per gli utenti finali](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Queste informazioni si applicano ai dispositivi mobili gestiti sia con Microsoft Intune che con Configuration Manager.

 > [!div class="button"]
 [< Passaggio precedente](create-service-connection-point.md)  [Passaggio successivo >](set-up-additional-management.md)


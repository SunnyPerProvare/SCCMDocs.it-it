---
title: Configurare la gestione di dispositivi iOS e Mac ibrida con Microsoft Intune
titleSuffix: Configuration Manager
description: Configurare la gestione dei dispositivi iOS con Configuration Manager e Microsoft Intune.
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 5eae4400-58ca-4c71-804c-6a585cd3df5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8c8d88b5f539338c790c18e5973bde1ba3e5b28f
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75821869"
---
# <a name="set-up-ios-hybrid-device-management-with-configuration-manager-and-microsoft-intune"></a>Configurare la gestione di dispositivi ibridi iOS con Configuration Manager e Microsoft Intune

*Si applica a: Configuration Manager (Current Branch)*

Con Configuration Manager e Intune si abilita la registrazione dei dispositivi iOS e Mac OS affinché gli utenti di iPhone, iPad e Mac possano accedere alla posta elettronica e alle risorse aziendali. Dopo aver installato l'app Portale aziendale di Intune, è possibile assegnare criteri ai relativi dispositivi. Prima di poter gestire i dispositivi iOS e Mac, è necessario importare un certificato del servizio APN (Apple Push Notification Service). Questo certificato consente a Intune di gestire i dispositivi iOS e Mac stabilendo una connessione con il servizio di gestione dei dispositivi di Apple.  

 È anche possibile registrare i dispositivi iOS di proprietà dell'azienda.  Vedere [Registrare i dispositivi aziendali](enroll-company-owned-devices.md).  

**Prerequisiti**<br>
Prima che sia possibile impostare la registrazione per una qualsiasi piattaforma, completare i prerequisiti e le procedure indicate in [Impostare la gestione dei dispositivi mobili ibrida](setup-hybrid-mdm.md).

Per supportare la registrazione di dispositivi iOS, è necessario attenersi alla procedura seguente:  

## <a name="download-a-certificate-signing-request"></a>Scaricare una richiesta di firma del certificato
Per richiedere ad Apple un certificato APN, è necessario un file di richiesta di firma del certificato.  

1.  Nell'area di lavoro **Amministrazione** della console di Configuration Manager andare a **Servizi cloud**> **Sottoscrizioni a Microsoft Intune**.  

2.  Nella scheda **Home** fare clic su **Crea richiesta certificato per servizio APN**. Si apre la finestra di dialogo **Richiesta di firma del certificato per Apple Push Notification Service** .  

3.  **Andare** al percorso per salvare il nuovo file di richiesta di firma del certificato. Salvare il file della richiesta di firma del certificato in locale.  

4.  Fare clic su **Scarica**. Il nuovo file di richiesta di firma del certificato di Microsoft Intune viene scaricato e salvato da Configuration Manager. Questo file viene usato per richiedere un certificato di relazione di trust al portale Apple Push Certificates.  

## <a name="request-an-mdm-push-certificate-from-apple"></a>Richiedere un certificato push MDM ad Apple
Il certificato push MDM viene usato per stabilire una relazione di trust tra il servizio di gestione, Intune e i dispositivi mobili iOS registrati.  

1.  Usando un browser andare al [portale Apple Push Certificates](https://identity.apple.com/pushcert) e accedere con il proprio ID Apple aziendale. Questo ID Apple deve essere usato in futuro per rinnovare il certificato APN.  

2.  Completare la procedura guidata usando il file della richiesta di firma del certificato (con estensione CSR). Scaricare il certificato push MDM e salvare il file con estensione pem in locale. Questo file del certificato con estensione pem viene usato per stabilire una relazione di trust tra il server Apple Push Notification e l'autorità di gestione dei dispositivi mobili di Intune.  

> [!NOTE]  
>  Non caricare il certificato per il servizio Apple Push Notification (APN) in Intune finché non viene abilitata la registrazione iOS nella console di Configuration Manager.  

## <a name="enable-enrollment-and-upload-the-mdm-push-certificate"></a>Abilitare la registrazione e il caricamento del certificato push MDM
Per abilitare la registrazione iOS, caricare il certificato APN.  

1.  Nell'area di lavoro **Amministrazione** della console di Configuration Manager andare a **Servizi cloud** > **Sottoscrizioni a Microsoft Intune**.  

2.  Nella scheda **Home** nel gruppo **Sottoscrizione** fare clic su **Configura piattaforme** > **iOS**.  

3.  Nella finestra di dialogo **Proprietà della sottoscrizione a Microsoft Intune** selezionare la scheda **iOS** e fare clic per selezionare la casella di controllo **Abilita registrazione iOS** .  
4.  Fare clic su **Sfoglia**e andare al file (con estensione CER) del certificato per il servizio APN scaricato da Apple. Configuration Manager visualizza le informazioni sul certificato APNs. Fare clic su **OK** per salvare il certificato APN in Intune.  

Dopo aver completato la configurazione occorre informare gli utenti su come registrare i loro dispositivi. Vedere [Informazioni sull'uso di Microsoft Intune per gli utenti finali](https://docs.microsoft.com/intune/end-user-educate). Queste informazioni si applicano ai dispositivi mobili gestiti sia con Microsoft Intune che con Configuration Manager.

## <a name="configure-enrollment-restrictions"></a>Configurare le restrizioni di registrazione

È possibile limitare i dispositivi che possono effettuare la registrazione bloccando i dispositivi di proprietà personale. In questo modo, si impedisce agli utenti di registrare dispositivi personali tramite il Portale aziendale. Se si bloccano i dispositivi di proprietà personale, sarà possibile registrare solo i dispositivi seguenti:
- [Dispositivi predichiarati](predeclare-devices-with-hardware-id.md)
- [Dispositivi gestiti da Apple Configurator](ios-hybrid-enrollment-using-apple-configurator.md)
- [Dispositivi gestiti da Device Enrollment Program (DEP)](ios-device-enrollment-program-for-hybrid.md)
- Dispositivi registrati con un [account del manager di registrazione dispositivi](enroll-devices-with-device-enrollment-manager.md)

### <a name="to-enable-enrollment-restrictions"></a>Per abilitare le restrizioni di registrazione
1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager andare a **Servizi cloud** > **Sottoscrizioni a Microsoft Intune**.
2. Nella scheda **Home** nel gruppo **Sottoscrizione** fare clic su **Configura piattaforme** > **iOS**.
3. Scegliere **Blocca dispositivi di proprietà personale** per limitare la registrazione ai dispositivi di proprietà dell'azienda.

> [!div class="button"]
> [Passaggio successivo](set-up-additional-management.md) [< passaggio precedente](create-service-connection-point.md)>

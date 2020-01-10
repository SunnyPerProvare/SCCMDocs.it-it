---
title: Impostare la gestione dei dispositivi mobili ibrida
titleSuffix: Configuration Manager
description: Impostazione della registrazione ibrida di dispositivi con Configuration Manager e Intune.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ffcb92d4a3df31d0771719d13c65f77b259e4dd4
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75826578"
---
# <a name="set-up-hybrid-mdm-with-configuration-manager-and-microsoft-intune"></a>Impostare la gestione dei dispositivi mobili ibrida con Configuration Manager e Intune

*Si applica a: Configuration Manager (Current Branch)*


Prima di poter essere gestiti con Configuration Manager, i dispositivi iOS, Windows e Android devono essere registrati con Intune. Usare i passaggi seguenti per impostare la registrazione ibrida dei dispositivi con Configuration Manager tramite Intune. Una volta completati i passaggi seguenti, la registrazione "bring your own device" (BYOD) per gli utenti sarà abilitata. Questi passaggi sono anche i prerequisiti per la [registrazione di dispositivi di proprietà dell'utente (BYOD)](enroll-hybrid-ios-mac.md) e la [registrazione di dispositivi di proprietà dell'azienda](enroll-company-owned-devices.md).

> [!Important]  
> A partire dal 14 agosto 2018, la gestione ibrida dei dispositivi mobili è una [funzionalità deprecata](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Per altre informazioni, vedere [Informazioni sulla gestione di dispositivi mobili ibrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## <a name="set-up-steps"></a>Passaggi di configurazione

 |Passaggi|Details|  
 |-----------|-------------|  
 |**Passaggio 1:** [creare una raccolta MDM](create-mdm-collection.md)|Creare una raccolta utente di Configuration Manager con gli utenti i cui dispositivi possono essere registrati|  
 |**Passaggio 2:** [requisiti dei nomi di dominio](confirm-dns.md)|Confermare che il servizio Domain Name Service (DNS) e la gestione utente di Active Directory della propria organizzazione soddisfino i requisiti della gestione dei dispositivi mobili|
 |**Passaggio 3:** [configurare la sottoscrizione di Intune](configure-intune-subscription.md)|Il servizio Intune consente di gestire i dispositivi su Internet.|  
 |**Passaggio 4:** [aggiungere termini e condizioni](terms-and-conditions.md)| Creare i termini e le condizioni che devono essere accettate dagli utenti per poter usare l'app Portale aziendale|
 |**Passaggio 5:** [creare il punto di connessione del servizio](create-service-connection-point.md)|Il punto di connessione del servizio invia le impostazioni e le informazioni di distribuzione del software a Configuration Manager e recupera i messaggi di stato e di inventario dai dispositivi mobili. |  
 |**Passaggio 6:** [abilitare la registrazione della piattaforma](enable-platform-enrollment.md)|La registrazione di software MDM per dispositivi iOS e Windows richiede passaggi aggiuntivi per la comunicazione tra il servizio e i dispositivi. Per Android non è richiesta alcuna configurazione aggiuntiva.|  
 |**Passaggio 7:** [configurare la gestione aggiuntiva](set-up-additional-management.md)|(Facoltativo) Impostare gli elementi di configurazione e l'accesso condizionale per i dispositivi registrati|
 |**Passaggio 8:** [verificare la configurazione MDM](verify-mdm-configuration.md)|Visualizzare i file di log per verificare che il punto di connessione del servizio sia stato creato correttamente e che gli account utente siano sincronizzati.|



## <a name="enroll-devices"></a>Registrare i dispositivi

Al termine dell'installazione ibrida è possibile registrare i dispositivi in Configuration Manager in diversi modi:

- **Dispositivi di proprietà dell'azienda (COD):** [registrare i dispositivi di proprietà](enroll-company-owned-devices.md) dell'azienda fornisce indicazioni su diversi modi specifici della piattaforma per registrare i dispositivi di proprietà dell'azienda  

- **Dispositivi di proprietà dell'utente (BYOD):** la registrazione dei dispositivi di [proprietà dell'utente (BYOD)](enroll-hybrid-ios-mac.md) fornisce indicazioni sui modi per registrare i dispositivi di proprietà dell'utente  



## <a name="see-also"></a>Vedere anche

Per informazioni su Intune senza Configuration Manager
> [!div class="button"]
> [Vedi documenti di Intune >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)



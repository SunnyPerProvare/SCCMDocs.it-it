---
title: Impostare la gestione di dispositivi mobili ibrida
titleSuffix: Configuration Manager
description: Impostazione della registrazione ibrida di dispositivi con Configuration Manager e Intune.
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fbc5b9abf63d95185795716cfcb9ebfaf3e2ec3d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32347077"
---
# <a name="setup-hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>Impostare la gestione dei dispositivi mobili ibrida con System Center Configuration Manager e Microsoft Intune

*Si applica a: System Center Configuration Manager (Current Branch)*


Prima di poter essere gestiti con Configuration Manager, i dispositivi iOS, Windows e Android devono essere registrati con Intune. Usare i passaggi seguenti per impostare la registrazione ibrida dei dispositivi con Configuration Manager tramite Intune. Una volta completati i passaggi seguenti, la registrazione "bring your own device" (BYOD) per gli utenti sarà abilitata. Questi passaggi sono anche i prerequisiti per la [registrazione di dispositivi di proprietà dell'utente (BYOD)](enroll-hybrid-ios-mac.md) e la [registrazione di dispositivi di proprietà dell'azienda](enroll-company-owned-devices.md).

 |Passaggi|Dettagli|  
 |-----------|-------------|  
 |**Passaggio 1:** [Creare una raccolta della gestione dei dispositivi mobili](create-mdm-collection.md)|Creare una raccolta utente di Configuration Manager con gli utenti i cui dispositivi possono essere registrati|  
 |**Passaggio 2:** [Requisiti dei nomi di dominio](confirm-dns.md)|Confermare che il servizio Domain Name Service (DNS) e la gestione utente di Active Directory della propria organizzazione soddisfino i requisiti della gestione dei dispositivi mobili|
 |**Passaggio 3:** [Configurare una sottoscrizione di Intune](configure-intune-subscription.md)|Il servizio Intune consente di gestire i dispositivi su Internet.|  
 |**Passaggio 4:** [Aggiungere termini e condizioni](terms-and-conditions.md)| Creare i termini e le condizioni che devono essere accettate dagli utenti per poter usare l'app Portale aziendale|
 |**Passaggio 5:** [Creare il punto di connessione del servizio](create-service-connection-point.md)|Il punto di connessione del servizio invia le impostazioni e le informazioni di distribuzione del software a Configuration Manager e recupera i messaggi di stato e di inventario dai dispositivi mobili. |  
 |**Passaggio 6:** [Abilitare la registrazione della piattaforma](enable-platform-enrollment.md)|La registrazione di software MDM per dispositivi iOS e Windows richiede passaggi aggiuntivi per la comunicazione tra il servizio e i dispositivi. Per Android non è richiesta alcuna configurazione aggiuntiva.|  
 |**Passaggio 7:** [Impostare la gestione aggiuntiva](set-up-additional-management.md)|(Facoltativo) Impostare gli elementi di configurazione e l'accesso condizionale per i dispositivi registrati|
 |**Passaggio 8:** [Verificare la configurazione della gestione dei dispositivi mobili](verify-mdm-configuration.md)|Visualizzare i file di log per verificare che il punto di connessione del servizio sia stato creato correttamente e che gli account utente siano sincronizzati.|

Per informazioni su Intune senza Configuration Manager
> [!div class="button"]
[Vedi documenti di Intune >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)


## <a name="enroll-devices"></a>Registrare i dispositivi
Al termine dell'installazione ibrida è possibile registrare i dispositivi in Configuration Manager in diversi modi:
- **Dispositivi di proprietà dell'azienda (COD):** nell'articolo [Registrare i dispositivi aziendali](enroll-company-owned-devices.md) sono riportate indicazioni su diverse modalità specifiche della piattaforma per la registrazione dei dispositivi di proprietà dell'azienda.
- **Dispositivi di proprietà dell'utente (BYOD):** nell'articolo [Registrare i dispositivi di proprietà dell'utente (BYOD)](enroll-hybrid-ios-mac.md) sono riportate indicazioni sulle modalità di registrazione dei dispositivi di proprietà degli utenti.

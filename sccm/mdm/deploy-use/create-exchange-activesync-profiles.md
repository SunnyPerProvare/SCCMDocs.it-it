---
title: Creare profili di posta elettronica di Exchange ActiveSync | Microsoft Docs
description: Di seguito viene illustrato come creare e configurare i profili di posta elettronica in System Center Configuration Manager che funzionano con Microsoft Intune.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 120442be-179e-450c-a0c4-284046895da3
caps.latest.revision: 4
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 1cbe1d8f34b0a7482232488e907190a7a9cadf30
ms.lasthandoff: 03/06/2017


---

# <a name="exchange-activesync-email-profiles-in-system-center-configuration-manager"></a>Profili di posta elettronica di Exchange ActiveSync in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I profili di posta elettronica supportano Microsoft Intune per consentire il provisioning di dispositivi con restrizioni e profili di posta elettronica usando Exchange ActiveSync. In questo modo gli utenti possono accedere alla posta elettronica aziendale dai propri dispositivi dopo aver eseguito pochissime operazioni di configurazione.  

 È possibile configurare i seguenti tipi di dispositivi con profili di posta elettronica:  

-   Dispositivi che eseguono Windows Phone 8  

-   Dispositivi che eseguono Windows Phone 8.1  

-   Dispositivi che eseguono Windows 10 Mobile  

-   Dispositivi iPhone che eseguono iOS 5, iOS 6, iOS 7 e iOS 8  

-   Dispositivi iPad che eseguono iOS 5, iOS 6, iOS 7 e iOS 8  

> [!IMPORTANT]  
>  Per distribuire profili in dispositivi iOS, Android Samsung KNOX Standard, Windows Phone e Windows 8.1 o Windows 10, tali dispositivi devono essere registrati in Intune. Per informazioni su come registrare i dispositivi, vedere [Gestire i dispositivi mobili con Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).  

 Oltre a configurare un account di posta elettronica sul dispositivo, è anche possibile configurare le impostazioni di sincronizzazione per i contatti, i calendari e le attività.  

 Quando si crea un profilo di posta elettronica, è possibile includere un'ampia gamma di impostazioni di protezione, tra cui i certificati per l'identità, la crittografia e la firma, per i quali è stato effettuato il provisioning usando profili certificato in System Center Configuration Manager. Per altre informazioni sui profili certificato, vedere [Profili certificato in System Center Configuration Manager](introduction-to-certificate-profiles.md).    


## <a name="create-a-new-exchange-activesync-email-profile"></a>Creare un nuovo profilo di posta elettronica di Exchange ActiveSync  

Avviare la Creazione guidata profilo di posta elettronica di Exchange ActiveSync  

1.  Nella console di System Center Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità**, **Accesso risorse aziendali**e quindi fare clic su **Profili di posta elettronica**.  

3.  Nella scheda **Home** del gruppo **Crea** fare clic su **Crea profilo Exchange ActiveSync**.

4.  Seguire le istruzioni della procedura guidata   

### <a name="to-configure-exchange-activesync-settings-for-the-exchange-activesync-email-profile"></a>Configurare le impostazioni di Exchange ActiveSync per il profilo di posta elettronica di Exchange ActiveSync  

1.  Nella pagina **Exchange ActiveSync** della Creazione guidata profilo di posta elettronica di Exchange ActiveSync specificare le informazioni seguenti:  

    -   **Host di Exchange ActiveSync:** specificare il nome host del server Exchange aziendale che ospita i servizi di Exchange ActiveSync.  

    -   **Nome account:** specificare il nome visualizzato dell'account di posta elettronica che verrà visualizzato nei dispositivi degli utenti.  

    -   **Nome utente account:** selezionare il modo in cui è configurato il nome utente dell'account di posta elettronica nei dispositivi client. Nell'elenco a discesa è possibile selezionare una delle opzioni seguenti:  

        -   **Nome entità utente** : usare il nome completo dell'entità utente per accedere a Exchange.  

        -   **Nome account SAM** : usare  

        -   **Indirizzo SMTP primario** : usare l'indirizzo SMTP primario usato dagli utenti per accedere a Exchange.  

    -   **Indirizzo di posta elettronica:** selezionare la modalità di generazione dell'indirizzo di posta elettronica per l'utente in ogni dispositivo client. Nell'elenco a discesa è possibile selezionare una delle opzioni seguenti:  

        -   **Indirizzo SMTP primario** : usare l'indirizzo SMTP primario usato dagli utenti per accedere a Exchange.  

        -   **Nome entità utente** : usare come indirizzo di posta elettronica il nome completo dell'entità utente.  

    -   **Dominio account:** scegliere una delle seguenti opzioni:  

        -   **Ottieni da Active Directory**  

        -   **Personalizzato**  

         Questo campo è applicabile solo se nell'elenco a discesa **Nome utente account** è selezionato **Nome account SAM** .  

    -   **Metodo di autenticazione:** scegliere uno dei seguenti metodi di autenticazione che verranno usati per autenticare la connessione a Exchange ActiveSync:  

        -   **Certificati** : verrà usato un certificato di identità per autenticare la connessione a Exchange ActiveSync.  

        -   **Nome utente e password** : l'utente del dispositivo deve specificare una password per connettersi a Exchange ActiveSync (il nome utente è configurato come parte del profilo di posta elettronica).  

    -   **Certificato di identità:** fare clic su **Seleziona** e quindi selezionare un certificato da usare per l'identità.  

        > [!NOTE]  
        >  Prima di poter selezionare il certificato di identità, è necessario configurarlo come profilo certificato Simple Certificate Enrollment Protocol (SCEP). Per altre informazioni sui profili certificato, vedere [Profili certificato in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

         Questa opzione è disponibile solo se in **Metodo di autenticazione** è stata selezionata l'opzione **Certificati**.  

    -   **Usa S/MIME** : consente di usare la crittografia S/MIME per inviare posta elettronica in uscita. Questa opzione è applicabile solo ai dispositivi iOS.  

    -   **Certificati di crittografia:** fare clic su **Seleziona** e quindi selezionare un certificato da usare per la crittografia. Questa opzione è applicabile solo ai dispositivi iOS.  

        > [!NOTE]  
        >  Prima di poter selezionare il certificato di crittografia, è necessario configurarlo come profilo certificato Simple Certificate Enrollment Protocol (SCEP). Per altre informazioni sui profili certificato, vedere [Profili certificato in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

         Questa opzione è disponibile solo se è stata selezionata l'opzione **Usa S/MIME**.  

    -   **Certificati di firma:** fare clic su **Seleziona** e quindi selezionare un certificato da usare per la firma. Questa opzione è applicabile solo ai dispositivi iOS.  

        > [!NOTE]  
        >  Prima di poter selezionare il certificato di firma, è necessario configurarlo come profilo certificato Simple Certificate Enrollment Protocol (SCEP). Per altre informazioni sui profili certificato, vedere [Profili certificato in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

         Questa opzione è disponibile solo se è stata selezionata l'opzione **Usa S/MIME**.  

###   <a name="configure-synchronization-settings-for-the-exchange-activesync-email-profile"></a>Configurare le impostazioni di sincronizzazione per il profilo di posta elettronica di Exchange ActiveSync.  

1.  Nella pagina **Configura impostazioni di sincronizzazione** della Creazione guidata profilo di posta elettronica di Exchange ActiveSync specificare le informazioni seguenti:  

    -   **Pianifica:** selezionare la pianificazione in base a cui i dispositivi sincronizzeranno i dati dal server di Exchange. Questa opzione è applicabile solo ai dispositivi Windows Phone. È possibile scegliere tra:  

        -   **Non configurato** : non viene applicata una pianificazione della sincronizzazione. In questo modo gli utenti possono configurare una pianificazione personalizzata per la sincronizzazione.  

        -   **All'arrivo di messaggi** : i dati quali i messaggi di posta elettronica e gli elementi del calendario verranno sincronizzati automaticamente all'arrivo.  

        -   **15 minuti** : i dati quali i messaggi di posta elettronica e gli elementi del calendario verranno sincronizzati automaticamente ogni 15 minuti.  

        -   **30 minuti** : i dati quali i messaggi di posta elettronica e gli elementi del calendario verranno sincronizzati automaticamente ogni 30 minuti.  

        -   **60 minuti** : i dati quali i messaggi di posta elettronica e gli elementi del calendario verranno sincronizzati automaticamente ogni 60 minuti.  

        -   **Manuale** : la sincronizzazione verrà avviata manualmente dall'utente del dispositivo.  

    -   **Numero di giorni di messaggi di posta elettronica da sincronizzare:** selezionare il numero di giorni di posta elettronica da sincronizzare. Scegliere uno dei valori seguenti:  

        -   **Non configurato** : l'impostazione non viene applicata. In questo modo gli utenti possono configurare la quantità di posta elettronica da scaricare sul dispositivo.  

        -   **Illimitata** : viene sincronizzata tutta la posta elettronica disponibile.  

        -   **1 giorno**  

        -   **3 giorni**  

        -   **1 settimana**  

        -   **2 settimane**  

        -   **1 mese**  

    -   **Consentire lo spostamento dei messaggi ad altri account di posta elettronica** : selezionare questa opzione per consentire agli utenti di spostare i messaggi di posta elettronica tra diversi account configurati nel dispositivo. Questa opzione è applicabile solo ai dispositivi iOS.  

    -   **Consentire l'invio di messaggi di posta elettronica da applicazioni di terze parti** : selezionare questa opzione per consentire agli utenti di inviare messaggi di posta elettronica da alcune applicazioni di posta elettronica di terze parti non predefinite. Questa opzione è applicabile solo ai dispositivi iOS.  

    -   **Sincronizzare gli indirizzi di posta elettronica usati di recente** : selezionare questa opzione per sincronizzare l'elenco di indirizzi di posta elettronica usati di recente sul dispositivo. Questa opzione è applicabile solo ai dispositivi iOS.  

    -   **Usare SSL** : selezionare questa opzione per usare la comunicazione Secure Sockets Layer (SSL) durante l'invio di messaggi di posta elettronica, la ricezione di messaggi di posta elettronica e la comunicazione con Exchange Server.  

    -   **Tipo di contenuto da sincronizzare:** selezionare i tipi di contenuto da sincronizzare nei dispositivi. Questa opzione è applicabile solo ai dispositivi Windows Phone. È possibile scegliere tra:  

        -   **Posta elettronica**  

        -   **Contatti**  

        -   **Calendarioio**  

        -   **Attività**  

###  <a name="specify-supported-platforms-for-the-exchange-activesync-email-profile"></a>Specificare le piattaforme supportate per il profilo di posta elettronica di Exchange ActiveSync.  

1.  Nella pagina **Piattaforme supportate** della Creazione guidata profilo di posta elettronica di Exchange ActiveSync selezionare i sistemi operativi in cui verrà installato il profilo oppure fare clic su **Seleziona tutto** per installare il profilo di posta elettronica in tutti i sistemi operativi disponibili.  

2.  Completare la procedura guidata.

Per informazioni su come distribuire i profili di posta elettronica di Exchange ActiveSync, vedere l'argomento sulla [distribuzione dei profili in System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).  


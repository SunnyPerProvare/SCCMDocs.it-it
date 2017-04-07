---
title: Creare profili di posta elettronica di Exchange ActiveSync | Microsoft Docs
description: Di seguito viene illustrato come creare e configurare i profili di posta elettronica in System Center Configuration Manager che funzionano con Microsoft Intune.
ms.custom: na
ms.date: 03/28/2017
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
ms.sourcegitcommit: aa8924a013ebdbee888cab33001fddbe7ad2d67e
ms.openlocfilehash: a0353c49360cd99bc92b4546e12a52c3d13d1d14
ms.lasthandoff: 03/30/2017


---

# <a name="exchange-activesync-email-profiles-in-system-center-configuration-manager"></a>Profili di posta elettronica di Exchange ActiveSync in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I profili di posta elettronica supportano Microsoft Intune per consentire il provisioning di dispositivi con restrizioni e profili di posta elettronica usando Exchange ActiveSync. In questo modo gli utenti possono accedere alla posta elettronica aziendale dai propri dispositivi dopo aver eseguito pochissime operazioni di configurazione.  

 È possibile configurare i seguenti tipi di dispositivi con profili di posta elettronica:  

- Windows 10
- Windows Phone 8.1
- Windows Phone 8.0
- iPhone che eseguono iOS 5, iOS 6, iOS 7 e iOS 8  
- iPad che eseguono iOS 5, iOS 6, iOS 7 e iOS 8  
- Samsung KNOX Standard (4 e versioni successive)
- Android for Work

Per distribuire profili di posta elettronica ai dispositivi, è necessario che questi siano registrati in Intune. Per informazioni su come registrare i dispositivi, vedere [Gestire i dispositivi mobili con Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).

>[!NOTE]
>Intune offre due profili di posta elettronica Android for Work, uno per Gmail e uno per Nine Work. Queste app sono disponibili in Google Play Store e possono connettersi a Exchange. Per abilitare la connettività della posta elettronica, distribuire una di queste app nei dispositivi dell'utente. In seguito creare e distribuire il profilo appropriato. Particolari app di posta elettronica, ad esempio Nine Work, potrebbero non essere gratuite. Rivedere i dettagli della licenza dell'app o contattare la società produttrice per chiedere chiarimenti.

 Oltre a configurare un account di posta elettronica sul dispositivo, è anche possibile configurare le impostazioni di sincronizzazione per i contatti, i calendari e le attività.  

 Quando si crea un profilo di posta elettronica, è possibile includere un'ampia gamma di impostazioni di protezione, tra cui i certificati per l'identità, la crittografia e la firma, per i quali è stato effettuato il provisioning usando profili certificato in System Center Configuration Manager. Per altre informazioni sui profili certificato, vedere [Profili certificato in System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles).    

## <a name="create-a-new-exchange-activesync-email-profile"></a>Creare un nuovo profilo di posta elettronica di Exchange ActiveSync  

Avviare la Creazione guidata profilo di posta elettronica di Exchange ActiveSync  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità**, **Accesso risorse aziendali**e quindi fare clic su **Profili di posta elettronica**.  

3.  Nella scheda **Home** del gruppo **Crea** fare clic su **Crea il profilo di posta elettronica di Exchange ActiveSync**.
4.  Nella pagina Generale della procedura guidata configurare le opzioni seguenti:
    - **Nome**: specificare un nome descrittivo per il profilo di posta elettronica.
    - **Descrizione**: facoltativamente, immettere una descrizione del profilo di posta elettronica che consenta di identificarlo nella console di Configuration Manager.
    - **Questo profilo di posta elettronica è per Android for Work**: selezionare questa opzione se il profilo di posta elettronica verrà distribuito soltanto a dispositivi Android for Work. Se si seleziona questa casella di controllo, la pagina **Piattaforme supportate** della procedura guidata non viene visualizzata. Vengono configurati soltanto i profili di posta elettronica Android for Work.
4.  Nella pagina **Exchange ActiveSync** della Creazione guidata profilo di posta elettronica di Exchange ActiveSync specificare le informazioni seguenti:  

    -   **Host di Exchange ActiveSync:** specificare il nome host del server Exchange aziendale che ospita i servizi di Exchange ActiveSync.  

    -   **Nome account:** specificare il nome visualizzato dell'account di posta elettronica che verrà visualizzato nei dispositivi degli utenti.  

    -   **Nome utente account:** selezionare il modo in cui è configurato il nome utente dell'account di posta elettronica nei dispositivi client. Nell'elenco a discesa è possibile selezionare una delle opzioni seguenti:  

        -   **Nome entità utente** : usare il nome completo dell'entità utente per accedere a Exchange.  

        -   **Nome account**: usare il nome completo dell'account da Active Directory.

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
        >  Prima di poter selezionare il certificato di identità, è necessario configurarlo come profilo certificato Simple Certificate Enrollment Protocol (SCEP). Per altre informazioni sui profili certificato, vedere [Profili certificato in System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

         Questa opzione è disponibile solo se in **Metodo di autenticazione** è stata selezionata l'opzione **Certificati**.  

    -   **Usa S/MIME** (solo per dispositivi iOS): consente di usare la crittografia S/MIME per inviare posta elettronica in uscita. È possibile scegliere una delle opzioni seguenti:


        -   **Certificati di crittografia:** fare clic su **Seleziona** e quindi selezionare un certificato da usare per la crittografia. Questa opzione è applicabile solo ai dispositivi iOS. È possibile selezionare solo un certificato PFX da usare come certificato di crittografia.

        Se si seleziona sia un certificato di crittografia che un certificato di firma, è necessario che i certificati siano entrambi in formato PFX.

        > [!NOTE]  
        >  Per poter selezionare i certificati, è prima necessario configurarli come profilo certificato SCEP (Simple Certificate Enrollment Protocol) o PFX. Per altre informazioni sui profili certificato, vedere [Profili certificato in System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  




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


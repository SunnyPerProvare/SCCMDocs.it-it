---
title: Creare profili di posta elettronica di Exchange ActiveSync | Microsoft Docs
description: Di seguito viene illustrato come creare e configurare i profili di posta elettronica in System Center Configuration Manager che funzionano con Microsoft Intune.
ms.custom: na
ms.date: 07/28/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 120442be-179e-450c-a0c4-284046895da3
caps.latest.revision: "4"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 0af556b5b63b465a99650c8889eae3adbf7307f6
ms.sourcegitcommit: 13599667ea77c16db1aebe64f8a6748c268f0b45
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/11/2017
---
# <a name="exchange-activesync-email-profiles-in-system-center-configuration-manager"></a>Profili di posta elettronica di Exchange ActiveSync in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usando Microsoft Intune ed Exchange ActiveSync è possibile configurare i dispositivi con profili di posta elettronica e restrizioni. In questo modo gli utenti possono accedere alla posta elettronica aziendale dai propri dispositivi dopo aver eseguito pochissime operazioni di configurazione.  

 È possibile configurare i seguenti tipi di dispositivi con profili di posta elettronica:  

- Windows 10
- Windows Phone 8.1
- iPhone che eseguono iOS 8  
- iPad che eseguono iOS 8  
- Samsung KNOX Standard (4 e versioni successive)
- Android for Work

Per distribuire profili di posta elettronica ai dispositivi, è necessario registrare questi ultimi in Intune. Per informazioni su come registrare i dispositivi, vedere [Gestire i dispositivi mobili con Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).

> [!NOTE]
> Intune offre due profili di posta elettronica Android for Work, uno per Gmail e l'altro per l'app di posta elettronica Nine Work. Queste app sono disponibili in Google Play Store e possono connettersi a Exchange. Per abilitare la connettività della posta elettronica, distribuire una di queste app nei dispositivi dell'utente. In seguito creare e distribuire il profilo appropriato. App di posta elettronica come Nine Work potrebbero non essere gratuite. Rivedere i dettagli della licenza dell'app o contattare la società produttrice per chiedere chiarimenti.

 Oltre a configurare un account di posta elettronica sul dispositivo, è possibile configurare le impostazioni di sincronizzazione per i contatti, i calendari e le attività.  

 Quando si crea un profilo di posta elettronica, è possibile includere una vasta gamma di impostazioni di protezione. Queste impostazioni includono certificati per l'identità, la crittografia e la firma, che sono stati configurati usando profili certificato in System Center Configuration Manager. Per altre informazioni sui profili certificato, vedere [Profili certificato in System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles.md).    

## <a name="create-an-exchange-activesync-email-profile"></a>Creare un profilo di posta elettronica di Exchange ActiveSync  

Per creare un profilo, usare la Creazione guidata profilo di posta elettronica di Exchange ActiveSync. 

1.  Nella console di Configuration Manager scegliere **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità**, **Accesso risorse aziendali** e quindi scegliere **Profili di posta elettronica**.  

3.  Nella scheda **Home** del gruppo **Crea** scegliere **Crea il profilo di posta elettronica di Exchange ActiveSync** per avviare la procedura guidata.

4.  Nella pagina **Generale** della procedura guidata configurare le opzioni seguenti:

    - **Nome**. Specificare un nome descrittivo per il profilo di posta elettronica.

    - **Descrizione**. Facoltativamente, immettere una descrizione del profilo di posta elettronica che consenta di identificarlo nella console di Configuration Manager.

    - **Questo profilo di posta elettronica è per Android for Work**. Scegliere questa opzione se si intende distribuire questo profilo di posta elettronica solo ai dispositivi Android for Work. Se si seleziona questa casella, la pagina **Piattaforme supportate** della procedura guidata non viene mostrata. Vengono configurati soltanto i profili di posta elettronica Android for Work.

4.  Nella pagina **Exchange ActiveSync** della procedura guidata specificare le informazioni seguenti:  

    -   **Nome host di Exchange ActiveSync**. Specificare il nome host del server Exchange aziendale che ospita i servizi di Exchange ActiveSync.  

    -   **Nome account**. Specificare il nome visualizzato dell'account di posta elettronica così come verrà mostrato nei dispositivi degli utenti.  

    -   **Nome utente account**. Scegliere la configurazione del nome utente dell'account di posta elettronica sui dispositivi client. Nell'elenco a discesa è possibile scegliere una delle opzioni seguenti:  

        -   **Nome entità utente**. Usare il nome completo dell'entità utente per accedere a Exchange.  

        -   **Nome account**. Usare il nome completo dell'account da Active Directory.

        -   **Indirizzo SMTP primario**. Usare l'indirizzo SMTP primario usato dagli utenti per accedere a Exchange.  

    -   **Indirizzo di posta elettronica**. Scegliere la modalità di generazione dell'indirizzo di posta elettronica per l'utente in ogni dispositivo client. Nell'elenco a discesa è possibile scegliere una delle opzioni seguenti:  

        -   **Indirizzo SMTP primario**. Usare l'indirizzo SMTP primario usato dagli utenti per accedere a Exchange.  

        -   **Nome entità utente**. Usare come indirizzo di posta elettronica il nome completo dell'entità utente.  

    -   **Dominio account**. Scegliere una delle seguenti opzioni:  

        -   **Ottieni da Active Directory**  

        -   **Personalizzato**  

         Questo campo è applicabile solo se nell'elenco a discesa **Nome utente account** è selezionato **Nome account SAM**.  

    -   **Metodo di autenticazione**. scegliere uno dei seguenti metodi di autenticazione che verranno usati per autenticare la connessione a Exchange ActiveSync:  

        -   **Certificati**. Verrà usato un certificato di identità per autenticare la connessione a Exchange ActiveSync.  

        -   **Nome utente e password**. L'utente del dispositivo deve specificare una password per connettersi a Exchange ActiveSync (il nome utente è configurato come parte del profilo di posta elettronica).  

    -   **Certificato di identità**. Scegliere **Seleziona** e quindi scegliere un certificato da usare per l'identità.  

         I certificati di identità devono essere certificati SCEP. Non è possibile usare un certificato PFX.  Per altre informazioni, vedere [Profili certificato in System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

         Questa opzione è disponibile solo se in **Metodo di autenticazione** è stata scelta l'opzione **Certificati**.  

    -   **Usa S/MIME**. Consente di usare la crittografia S/MIME per inviare posta elettronica in uscita. Questa opzione è applicabile solo ai dispositivi iOS. È possibile scegliere una delle opzioni seguenti:

        -   **Certificati di firma**.  Scegliere **Seleziona** e quindi scegliere un profilo certificato da usare per la crittografia.  

            Il profilo può essere un certificato SCEP o PFX.  Tuttavia, se si usano sia la firma che la crittografia, è necessario selezionare profili certificato PFX per *entrambe*, sia per la firma che per la crittografia.

        -   **Certificati di crittografia**. Scegliere **Seleziona** e quindi scegliere un certificato da usare per la crittografia. È possibile scegliere solo un certificato PFX da usare come certificato di crittografia.

        -   Per crittografare tutti i messaggi di posta elettronica all'interno di dispositivi iOS, abilitare la casella di controllo **Richiedi crittografia**.    

         Perché sia possibile scegliere profili certificato qui, è necessario crearli.  Per altre informazioni, vedere [Profili certificato in System Center Configuration Manager](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

## <a name="configure-synchronization-settings-for-the-exchange-activesync-email-profile"></a>Configurare le impostazioni di sincronizzazione per il profilo di posta elettronica di Exchange ActiveSync  

Nella pagina **Configura impostazioni di sincronizzazione** della Creazione guidata profilo di posta elettronica di Exchange ActiveSync specificare le informazioni seguenti:  

-   **Pianificazione**. Scegliere la pianificazione in base a cui i dispositivi sincronizzeranno i dati dal server di Exchange. Questa opzione è applicabile solo ai dispositivi Windows Phone. È possibile scegliere tra:  

    -   **Non configurato**. Non viene applicata una pianificazione della sincronizzazione. In questo modo gli utenti possono configurare una pianificazione personalizzata per la sincronizzazione.  

    -   **All'arrivo di messaggi**. I dati quali i messaggi di posta elettronica e gli elementi del calendario verranno sincronizzati automaticamente all'arrivo.  

    -   **15 minuti**. I dati quali i messaggi di posta elettronica e gli elementi del calendario verranno sincronizzati automaticamente ogni 15 minuti.  

    -   **30 minuti**. I dati quali i messaggi di posta elettronica e gli elementi del calendario verranno sincronizzati automaticamente ogni 30 minuti.  

    -   **60 minuti**. I dati quali i messaggi di posta elettronica e gli elementi del calendario verranno sincronizzati automaticamente ogni 60 minuti.  

    -   **Manuale**. L'utente del dispositivo deve avviare manualmente la sincronizzazione.  

-   **Numero di giorni di messaggi di posta elettronica da sincronizzare**. Scegliere il numero di giorni di posta elettronica da sincronizzare. Scegliere uno dei valori seguenti:  

    -   **Non configurato**. L'impostazione non viene applicata. In questo modo gli utenti possono configurare la quantità di posta elettronica da scaricare sul dispositivo.  

    -   **Illimitato**. Sincronizza tutti i messaggi di posta elettronica disponibili.  

    -   **1 giorno**  

    -   **3 giorni**  

    -   **1 settimana**  

    -   **2 settimane**  

    -   **1 mese**  

-   **Consenti di spostare i messaggi negli altri account di posta elettronica**. Scegliere questa opzione per consentire agli utenti di spostare i messaggi di posta elettronica tra i diversi account configurati nel dispositivo. Questa opzione è applicabile solo ai dispositivi iOS.  

-   **Consentire l'invio di messaggi di posta elettronica da applicazioni di terze parti**. Selezionare questa opzione per consentire agli utenti di inviare messaggi di posta elettronica da alcune applicazioni di posta elettronica di terze parti non predefinite. Questa opzione è applicabile solo ai dispositivi iOS.  

-   **Sincronizza gli indirizzi di posta elettronica utilizzati di recente**. Scegliere questa opzione per sincronizzare l'elenco di indirizzi di posta elettronica usati di recente nel dispositivo. Questa opzione è applicabile solo ai dispositivi iOS.  

-   **Usa SSL**. Scegliere questa opzione per usare la comunicazione Secure Sockets Layer (SSL) per l'invio di messaggi di posta elettronica, la ricezione di messaggi di posta elettronica e la comunicazione con Exchange Server.  

-   **Tipo di contenuti da sincronizzare**. Scegliere i tipi di contenuto da sincronizzare nei dispositivi. Questa opzione è applicabile solo ai dispositivi Windows Phone. È possibile scegliere tra:  

    -   **Posta elettronica**  

    -   **Contatti**  

    -   **Calendario**  

    -   **Attività**  

## <a name="specify-supported-platforms-for-the-exchange-activesync-email-profile"></a>Specificare le piattaforme supportate per il profilo di posta elettronica di Exchange ActiveSync  

1.  Nella pagina **Piattaforme supportate** della Creazione guidata profilo di posta elettronica di Exchange ActiveSync scegliere i sistemi operativi in cui verrà installato il profilo. In alternativa, scegliere **Seleziona tutto** per installare il profilo di posta elettronica su tutti i sistemi operativi disponibili.  

2.  Completa la procedura guidata.

Per informazioni su come distribuire i profili di posta elettronica di Exchange ActiveSync, vedere l'argomento sulla [distribuzione dei profili in System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).  

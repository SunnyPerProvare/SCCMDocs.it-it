---
title: Pianificare una MDM locale | System Center Configuration Manager
description: Pianificare la gestione dei dispositivi mobili locale per gestire dispositivi mobili in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
caps.latest.revision: 9
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 6bc3bf68d098fec7b6ac976d8e7ee7a7d71fab6a


---
# <a name="plan-for-on-premises-mobile-device-management-in-system-center-configuration-manager"></a>Pianificare la gestione di dispositivi mobili locale in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Prendere in considerazione i requisiti seguenti prima di preparare l'infrastruttura di Configuration Manager per eseguire la gestione dei dispositivi mobili locale.

##  <a name="a-namebkmkdevicesa-supported-devices"></a><a name="bkmk_devices"></a> Dispositivi supportati  
 La gestione di dispositivi mobili locale consente di gestire i dispositivi mobili usando le funzionalità di gestione predefinite nei sistemi operativi dei dispositivi.  La funzionalità di gestione si basa sullo standard Open Mobile Alliance (OMA) Device Management (DM), usato da molte piattaforme per dispositivi per consentire la gestione dei dispositivi.  Nella documentazione e nell'interfaccia utente della console di Configuration Manager questi dispositivi vengono indicati con il termine **dispositivi moderni** per distinguerli da altri dispositivi la cui gestione richiede il client di Configuration Manager.  

 > [!NOTE]  
>  Configuration Manager (Current Branch) supporta la registrazione nella gestione dei dispositivi mobili locale per i dispositivi che eseguono i sistemi operativi seguenti:  
>   
>  -   Windows 10 Enterprise  
> -   Windows 10 Pro  
> -   Windows 10 Team \( a partire da Configuration Manager versione 1602\)  
> -   Windows 10 Mobile  
> -   Windows 10 Mobile Enterprise   

##  <a name="a-namebkmkintunea-use-of-the-microsoft-intune-subscription"></a><a name="bkmk_intune"></a> Usare la sottoscrizione a Microsoft Intune  
 Per iniziare a usare la gestione dei dispositivi mobili, è necessaria una sottoscrizione a Microsoft Intune. La sottoscrizione è richiesta solo per tenere traccia delle licenze dei dispositivi e non viene usata per gestire o archiviare le informazioni di gestione per i dispositivi. Tutte le attività di gestione vengono eseguite all'interno dell'azienda usando l'infrastruttura di Configuration Manager locale.  

> [!IMPORTANT]  
>  Configuration Manager non supporta l'uso di Microsoft Intune e l'infrastruttura di Configuration Manager locale come autorità di gestione allo stesso tempo. Pertanto, se si imposta la sottoscrizione di Intune per la gestione locale, si disabilita in effetti la gestione di Intune.  

 Se nel sito sono presenti dispositivi con connessione Internet, è possibile usare il servizio di Intune per notificare ai dispositivi di controllare il punto gestione dei dispositivi per gli aggiornamenti dei criteri. Questo uso di  Intune è rigorosamente riservato alle notifiche per i dispositivi con connessione Internet. I dispositivi senza connessioni Internet (e che non possono essere contattati da Intune) si basano sull'intervallo di polling configurato per controllare le funzioni di gestione con i ruoli di sistema del sito.  

> [!TIP]  
>  È consigliabile configurare Intune prima di configurare i ruoli di sistema del sito obbligatori per ridurre al minimo il tempo necessario per l'attivazione dei ruoli di sistema del sito.  

 Per informazioni su come configurare la sottoscrizione di Intune, vedere [Impostare una sottoscrizione di Microsoft Intune per la gestione dei dispositivi mobili locale in System Center Configuration Manager](../../mdm/get-started/set-up-intune-subscription-on-premises-mdm.md).  

##  <a name="a-namebkmkrolesa-required-site-system-roles"></a><a name="bkmk_roles"></a> Ruoli di sistema del sito necessari  
 La gestione dei dispositivi mobili locale richiede minimo uno dei ruoli di sistema del sito seguenti:  

-   **Punto proxy di registrazione** per supportare le richieste di registrazione.  

-   **Punto di registrazione** per supportare la registrazione dei dispositivi.  

-   **Punto gestione periferiche** per la distribuzione dei criteri. Questo ruolo del sistema del sito è una variante del ruolo del punto di gestione che è stato configurato per consentire la gestione dei dispositivi mobili.  

-   **Punto di distribuzione** per la distribuzione di contenuti.  

-   **Punto di connessione del servizio** per la connessione a Intune per le notifiche a dispositivi esterni al firewall.  

 Questi ruoli del sistema del sito possono essere installati in un unico server del sistema del sito oppure possono essere eseguiti separatamente in server diversi a seconda delle esigenze dell'organizzazione. Ogni server di sistema del sito usato per la gestione dei dispositivi mobili locale deve essere configurato come endpoint HTTPS per comunicare con dispositivi attendibili. Per altre informazioni, vedere [Comunicazioni attendibili richieste](#bkmk_trustedComs).  

 Per altre informazioni sulla pianificazione dei ruoli del sistema del sito, vedere [Plan for site system servers and site system roles for System Center Configuration Manager](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).  

 Per altre informazioni su come aggiungere i ruoli del sistema del sito, vedere [Install site system roles for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md).  

##  <a name="a-namebkmktrustedcomsa-required-trusted-communications"></a><a name="bkmk_trustedComs"></a> Comunicazioni attendibili necessarie  
 La gestione dei dispositivi mobili richiede che i ruoli di sistema del sito siano abilitati per le comunicazioni HTTPS. A seconda delle esigenze, è possibile usare l'autorità di certificazione (CA) dell'azienda per stabilire connessioni attendibili tra server e dispositivi oppure è possibile usare un'autorità di certificazione disponibile pubblicamente come CA attendibile.  In entrambi i casi, è necessario che un certificato server Web sia configurato con IIS nei server del sistema del sito che ospitano i ruoli del sistema del sito richiesti e sarà necessario il certificato radice della CA installato nei dispositivi che devono connettersi a tali server.  

 Se si usa la CA dell'azienda per stabilire una comunicazione attendibile, è necessario eseguire le attività seguenti:  

-   Creare ed emettere il modello di certificato del server Web nella CA.  

-   Richiedere un certificato del server web per ogni server del sistema del sito che ospita un ruolo del sistema del sito richiesto.  

-   Configurare IIS nel server del sistema del sito per usare il certificato del server Web richiesto.  

 Per i dispositivi aggiunti al dominio Active Directory aziendale, il certificato radice della CA aziendale è già disponibile nel dispositivo per le connessioni attendibili. Ciò significa che i dispositivi appartenenti a un dominio (come i computer desktop) saranno automaticamente attendibili per le connessioni HTTPS con i server del sistema del sito. Nei dispositivi (in genere mobili) non appartenenti a un dominio, invece, il certificato radice obbligatorio non sarà installato. Tali dispositivi richiederanno l'installazione manuale del certificato radice per comunicare correttamente con i server di sistema del sito che supportano la gestione dei dispositivi mobili locale.  

 È necessario esportare il certificato radice della CA emittente per l'uso da parte di singoli dispositivi. Per ottenere il file del certificato radice, è possibile esportarlo usando la CA oppure, per un metodo più semplice, usando il certificato del server Web rilasciato dalla CA per estrarre la radice e creare un file del certificato radice.   Il certificato radice deve essere quindi recapitato al dispositivo.  Alcuni metodi di recapito semplici includono  

-   File system  

-   Allegato e-mail  

-   Scheda di memoria  

-   Dispositivo con tethering  

-   Archiviazione cloud (ad esempio OneDrive)  

-   Connessione NFC (Near Field Communication)  

-   Lettore di codice a barre  

-   Pacchetto di provisioning della Configurazione guidata  

 Per altre informazioni, vedere [Set up certificates for trusted communications for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md)  

##  <a name="a-namebkmkenrollmenta-enrollment-considerations"></a><a name="bkmk_enrollment"></a> Considerazioni sulla registrazione  
 Per abilitare la registrazione di dispositivi per la gestione dei dispositivi mobili locale, gli utenti devono avere l'autorizzazione alla registrazione e i dispositivi devono poter stabilire comunicazioni attendibili con i server di sistema del sito che ospitano i ruoli di sistema del sito necessari.  

 La concessione dell'autorizzazione di registrazione degli utenti può essere eseguita con la configurazione di un profilo di registrazione nelle impostazioni client di Configuration Manager. È possibile usare le impostazioni client predefinite per inviare il profilo di registrazione a tutti gli utenti individuati o è possibile impostare il profilo di registrazione nelle impostazioni client personalizzate e inviare le impostazioni a una o più raccolte di utenti.  

 Con l'autorizzazione di registrazione, gli utenti possono registrare i propri dispositivi. Per essere registrato, il dispositivo dell'utente deve avere il certificato radice dell'autorità di certificazione (CA) che ha emesso il certificato del server Web usato nei server di sistema del sito che ospitano i ruoli del sistema del sito richiesto.  

 Come alternativa alla registrazione avviata dall'utente, è possibile configurare un pacchetto di registrazione in blocco che consente la registrazione del dispositivo senza intervento dell'utente. Questo pacchetto può essere recapitato al dispositivo prima che venga inizialmente sottoposto a provisioning per l'uso o dopo che il dispositivo viene sottoposto al processo di Configurazione guidata.  

 Per altre informazioni su come configurare e registrare i dispositivi, vedere  

-   [Impostare la registrazione dei dispositivi per la gestione dei dispositivi mobili locale in System Center Configuration Manager](../../mdm/get-started/set-up-device-enrollment-on-premises-mdm.md)  

-   [Registrare i dispositivi per la gestione dei dispositivi mobili locale in System Center Configuration Manager](../../mdm/deploy-use/enroll-devices-on-premises-mdm.md)  



<!--HONumber=Nov16_HO1-->



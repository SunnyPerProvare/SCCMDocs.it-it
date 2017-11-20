---
title: "Novità nella gestione di dispositivi mobili ibrida"
titleSuffix: Configuration Manager
description: "Informazioni sulle nuove funzionalità di gestione dei dispositivi mobili disponibili per le distribuzioni ibride con Configuration Manager e Intune."
ms.custom: na
ms.date: 11/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 29dd4bff6d35712c23d66751db16a00aa761b8b4
ms.sourcegitcommit: 922d6d9c91ba2158b938df381277be1b5f1d434a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2017
---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Novità della gestione ibrida di dispositivi mobili con System Center Configuration Manager e Microsoft Intune

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo illustra le nuove funzionalità di gestione dei dispositivi mobili (MDM) disponibili per le distribuzioni ibride con System Center Configuration Manager e Intune.     

> [!Note]    
> Intune in Azure è la soluzione MDM consigliata da Microsoft.     
> - Per informazioni dettagliate sulle nuove caratteristiche e gli aggiornamenti in Intune autonomo, vedere [Novità di Microsoft Intune](https://docs.microsoft.com/intune/whats-new).    
> - Per informazioni dettagliate su come eseguire la migrazione a Intune autonomo, vedere [Migrate hybrid MDM users and devices to Intune standalone](https://docs.microsoft.com/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa) (Eseguire la migrazione di utenti e dispositivi di MDM ibrido a Intune autonomo).
> - Per informazioni dettagliate sugli aggiornamenti dell'interfaccia utente per Intune e MDM ibrido, vedere [Aggiornamenti dell'interfaccia utente per le applicazioni degli utenti finali in Intune](https://docs.microsoft.com/intune/whats-new-app-ui). 

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilità con le versioni di Configuration Manager  
Ogni sezione di questo articolo elenca le funzionalità ibride in tre categorie diverse. Usare le indicazioni che seguono per determinare la compatibilità delle funzionalità di ogni categoria con versioni diverse di Configuration Manager:  

|Categorie di funzionalità|Descrizione|
|-|-|
|**Novità di Microsoft Intune** | In generale, tutte le funzionalità elencate in questa categoria dovrebbero funzionare con tutte le versioni di Configuration Manager, incluse le versioni di System Center 2012 R2 Configuration Manager, poiché richiedono solo il servizio Intune e non richiedono altre funzionalità di Configuration Manager.|
|**Novità di Configuration Manager Technical Preview**| Tutte le funzionalità elencate in questa categoria funzionano solo con la versione di Technical Preview specificata. Per provare queste funzionalità, è necessario installare la versione di Technical Preview specificata nella descrizione della funzionalità. Per altre informazioni, vedere [Technical Preview per System Center Configuration Manager](../../core/get-started/technical-preview.md).|
|**Novità di Configuration Manager (Current Branch)**| Tutte le funzionalità elencate in questa categoria funzionano solo con la versione di Configuration Manager (Current Branch) specificata, ad esempio la versione 1511 o 1602. Se si usa una versione precedente di Configuration Manager per la distribuzione ibrida, è necessario eseguire l'aggiornamento alla versione di Configuration Manager (Current Branch) specificata nella descrizione della funzionalità. Per altre informazioni, vedere l'articolo relativo agli [aggiornamenti a System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|


## <a name="november-2017"></a>Novembre 2017

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

- **Accesso a log di app gestite per iOS** <!-- 1469920 --> Gli utenti finali con Managed Browser installato possono ora visualizzare lo stato della gestione di tutte le app Microsoft pubblicate e inviare i log per la risoluzione dei problemi delle app iOS gestite.
  
  Per informazioni su come abilitare la modalità di risoluzione dei problemi in Managed Browser in un dispositivo iOS, vedere [How to access to managed app logs using the Managed Browser on iOS](https://docs.microsoft.com/intune/app-configuration-managed-browser#how-to-access-to-managed-app-logs-using-the-managed-browser-on-ios) (Come accedere ai log di app gestite tramite Managed Browser in iOS).


## <a name="october-2017"></a>Ottobre 2017

### <a name="new-in-configuration-manager-technical-preview-1709"></a>Novità di Configuration Manager Technical Preview 1709

- **Esperienza del profilo VPN migliorata nella console di Configuration Manager** <!-- 1313282 -->     
  Le impostazioni del profilo VPN vengono ora filtrate in base alla piattaforma. Quando si creano nuovi profili VPN, ogni piattaforma supportata contiene solo le impostazioni appropriate per la piattaforma stessa. La nuova funzionalità non influisce sui profili VPN esistenti. Altre informazioni su questa modifica sono disponibili [qui](/sccm/core/get-started/capabilities-in-technical-preview-1709#improved-vpn-profile-experience-in-configuration-manager-console).


### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune  

- **Supporto dell'autenticazione basata su certificati nel portale aziendale per iOS** <!--1029830--> È stato aggiunto il supporto per l'autenticazione basata su certificati nell'app Portale aziendale per iOS. Gli utenti con autenticazione basata su certificati immettono il nome utente e quindi toccano il collegamento "Sign in with a certificate" (Accedi con un certificato). L'autenticazione basata su certificati è già supportata nelle app Portale aziendale per Android e Windows. Per altre informazioni, vedere la pagina sull'[accesso all'app Portale aziendale](https://docs.microsoft.com/intune-user-help/sign-in-to-the-company-portal) pagina.

- **Miglioramenti al flusso di lavoro di configurazione dei dispositivi in Portale aziendale**<!--1490692-->    
  È stato migliorato il flusso di lavoro di configurazione dei dispositivi nell'app Portale aziendale per Android. Il linguaggio è più semplice e specifico della società e sono state inserite schermate dove possibile. È possibile visualizzare questi miglioramenti nella pagina delle [novità dell'interfaccia utente dell'app](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-october-2-2017).

- **Materiale sussidiario migliorato sulla richiesta di accesso ai contatti per i dispositivi Android** <!--1484985-->    
  L'app Portale aziendale per Android chiede spesso all'utente l'autorizzazione all'accesso ai contatti. Se l'utente finale rifiuta l'accesso, viene ora visualizzata una notifica in-app che richiede tale autorizzazione per l'accesso condizionale. 

- **Correzione dell'avvio protetto per Android**<!--1490712-->    
  Gli utenti finali con dispositivi Android potranno toccare il motivo della mancata conformità nell'app Portale aziendale. Se possibile, con questa operazione passeranno direttamente al percorso corretto nell'app di configurazione per risolvere il problema. 

- **Notifiche push aggiuntive per gli utenti finali dell'app Portale aziendale per Android Oreo** <!--1475932 -->    
  Verranno visualizzate ulteriori notifiche per gli utenti finali per indicare quando l'app Portale aziendale per Android Oreo sta eseguendo attività in background, ad esempio quando sta recuperando criteri dal servizio Intune. Le notifiche aumentano la trasparenza per gli utenti finali, che sapranno quando sono in corso attività amministrative nell'app Portale aziendale nei loro dispositivi, e rientra nell'ambito della complessiva [ottimizzazione dell'interfaccia utente del portale aziendale](https://blogs.technet.microsoft.com/intunesupport/2017/08/21/android-8-0-o-behaviour-changes-and-microsoft-intune) per l'app Portale aziendale per Android Oreo. 

- **Nuovi comportamenti dell'app Portale aziendale per Android con i profili di lavoro**<!--1485783-->    
  Quando si registra un dispositivo Android for Work con un profilo di lavoro, è l'app Portale aziendale nel profilo di lavoro che esegue le attività di gestione per il dispositivo. 

  A meno che nel profilo personale non venga usata un'app abilitata per la gestione di applicazioni mobili, l'app Portale aziendale per Android non ha più alcuna funzione. Per migliorare l'esperienza dei profili di lavoro, Intune nasconde automaticamente l'app Portale aziendale personale dopo la registrazione di un profilo di lavoro.

  L'app Portale aziendale per Android può essere abilitata in qualsiasi momento nel profilo personale. A tale scopo, cercare [Portale aziendale in Play Store](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) e toccare **Abilita**.

- **Passaggio dell'app Portale aziendale per Windows 8.1 e Windows Phone 8.1 alla modalità di solo supporto** <!--1428681-->    
 È stato aggiunto un avviso per annunciare che le app Portale aziendale per Windows 8.1 e Windows Phone 8.1 sono in fase di passaggio alla modalità di solo supporto. Per informazioni, vedere [Notifiche](#notices).  

- **Blocco della registrazione di dispositivi Samsung Knox non supportati**<!-- 1490695 -->    
  L'app Portale aziendale tenta di registrare solo i dispositivi Samsung Knox supportati. Per evitare errori di attivazione KNOX che impediscono la registrazione MDM, la registrazione del dispositivo viene tentata solo se il dispositivo è presente nell'[elenco dei dispositivi pubblicato da Samsung](https://www.samsungknox.com/knox-supported-devices/knox-workspace). Alcuni numeri di modello di dispositivi Samsung supportano KNOX, mentre altri non lo supportano. Verificare la compatibilità Knox presso il rivenditore del dispositivo prima dell'acquisto e della distribuzione. È possibile trovare l'elenco completo dei dispositivi verificati nelle [impostazioni dei criteri Android e Samsung KNOX Standard](https://docs.microsoft.com/intune-classic/deploy-use/android-policy-settings-in-microsoft-intune#supported-samsung-knox-standard-devices).

- **Fine del supporto per Android 4.3 e versioni precedenti**<!--1171126, 1326920 -->    
  È stata aggiunta la comunicazione della fine del supporto per Android 4.3 e versioni precedenti. Per informazioni, vedere [Notifiche](#notices).

- **Informazioni per gli utenti finali sul tipo di informazioni sui dispositivi visualizzabili nei dispositivi registrati** <!--1165314-->    
  L'informazione **Tipo di proprietà** è in corso di aggiunta nella schermata Dettagli dispositivo in tutte le app Portale aziendale. In questo modo gli utenti potranno ottenere altre informazioni sulla privacy direttamente dall'articolo [Quali sono le informazioni visibili per l'azienda quando si registra il dispositivo?](https://docs.microsoft.com/intune-user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune). Questa modifica verrà applicata in tutte le app Portale aziendale in un prossimo futuro. È stata annunciata per iOS in [settembre](https://docs.microsoft.com/intune/whats-new#week-of-september-11-2017). 


## <a name="september-2017"></a>Settembre 2017

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune     

- **Azione di aggiornamento aggiunta all'app Portale aziendale per Windows 10** <!-- 1132468 -->    
    L'app Portale aziendale per Windows 10 consente agli utenti di aggiornare i dati nell'app trascinando verso il basso per aggiornare o, nei desktop, premendo F5.

- **Informazioni per gli utenti finali sul tipo di informazioni sui dispositivi che possono essere visualizzate per iOS** <!--739894-->    
    L'informazione **Tipo di proprietà** è stata aggiunta alla schermata Dettagli dispositivo nell'app Portale aziendale per iOS. In questo modo gli utenti potranno ottenere maggiori informazioni sulla privacy direttamente da questa pagina dai documenti per gli utenti finali di Intune. Sarà inoltre possibile accedere a queste informazioni nella schermata Informazioni. 

- **Testo più comprensibile per l'app Portale aziendale per Android** <!---1396349-->       
    Il processo di registrazione per l'app Portale aziendale per Android è ora più semplice per gli utenti finali, grazie all'uso di un nuovo testo più comprensibile. Se si usa una documentazione personalizzata per la registrazione, è consigliabile aggiornarla sulla base delle nuove schermate. Alcune immagini di esempio sono disponibili nella pagina [Aggiornamenti dell'interfaccia utente per le applicazioni degli utenti finali in Intune](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-september-11-2017).

- **Aggiunta dell'app Portale aziendale di Windows 10 ai criteri Consenti di Windows Information Protection** <!-- 677129 -->    
    L'app Portale aziendale di Windows 10 è stata aggiornata per supportare Windows Information Protection (WIP). L'app può essere aggiunta ai criteri Consenti di WIP. Con questa modifica, non è più necessario aggiungere l'app all'**elenco esenzioni**. 

     Solo un singolo elemento di configurazione WIP può essere recapitato a un dispositivo.  Se due elementi di configurazione WIP sono destinati allo stesso dispositivo, non si applica nessun criterio WIP.

- **Aggiunta della comunicazione di fine supporto per iOS 8.0**    
    È stata aggiunta la comunicazione della fine del supporto per iOS 8.0. Per informazioni, vedere [Notifiche](#notices).

## <a name="august-2017"></a>Agosto 2017

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune     

- **Nuova esperienza di accesso per gli utenti del portale aziendale Android e gli utenti di criteri di protezione delle app** <!-- 621669 -->    
Gli utenti finali possono ora visualizzare le app, gestire i dispositivi e accedere a informazioni sui contatti IT tramite l'app Portale aziendale Android senza registrare i dispositivi Android personali. Inoltre, se un utente finale usa già un'app protetta dai criteri di protezione delle app di Intune e avvia l'app Portale aziendale Android, non visualizza più la richiesta di registrare il dispositivo.


## <a name="july-2017"></a>Luglio 2017

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

- **Aggiunta di comunicazioni di fine supporto per Android e Windows Phone**

    Sono state aggiunte nuove comunicazioni relative alla fine del supporto per alcune versioni di Android e di Windows Phone. Per informazioni, vedere [Notifiche](#notices).


### <a name="new-in-configuration-manager-current-branch"></a>Novità di Configuration Manager (Current Branch)

Le funzionalità seguenti, che prima erano disponibili nelle versioni di Configuration Manager Technical Preview, sono ora disponibili nelle distribuzioni ibride con Intune e Configuration Manager (Current Branch) versione 1706.

- [Supporto di Entrust per le autorità di certificazione Entrust](/sccm/core/get-started/capabilities-in-technical-preview-1706#support-for-entrust-certification-authorities)
- [Nuove impostazioni dei criteri di gestione delle applicazioni mobili](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-mobile-application-management-policy-settings)
- [Aggiornamenti della configurazione della condivisione di Android for Work](/sccm/core/plan-design/changes/whats-new-in-version-1706#updates-to-android-for-work-sharing-configuration)
- [Nuove regole per i criteri di conformità dei dispositivi](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-device-compliance-policy-rules)
- [Nuove impostazioni di configurazione per dispositivi Windows 10 non gestiti con il client di Configuration Manager](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client)
- [Supporto Cisco (IPsec) per i profili VPN di MacOS](/sccm/core/get-started/capabilities-in-technical-preview-1706#cisco-ipsec-support-for-macos-vpn-profiles)
- [Restrizioni di registrazione per Android e iOS](/sccm/core/plan-design/changes/whats-new-in-version-1706#android-and-ios-enrollment-restrictions) 

## <a name="june-2017"></a>Giugno 2017

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

- **Modificare l'autorità MDM**

  A partire dalla versione 1610 di Configuration Manager, è possibile cambiare l'autorità MDM senza bisogno di contattare il supporto tecnico Microsoft e senza dover annullare e ripetere la registrazione dei dispositivi gestiti esistenti. Per altre informazioni, vedere [Cambiare l'autorità MDM](/sccm/mdm/deploy-use/change-mdm-authority).

- **Integrazione di Managed Browser e del proxy di applicazione**

  Intune Managed Browser può ora integrarsi con il servizio proxy di applicazione di Azure AD per consentire agli utenti di accedere ai siti Web interni, anche quando lavorano in remoto. Gli utenti del browser immettono l'URL del sito nel modo usuale e Managed Browser indirizza la richiesta tramite il gateway Web del proxy di applicazione. Per altre informazioni, vedere [Gestire un accesso Internet tramite i criteri di Managed Browser](https://docs.microsoft.com/intune/app-configuration-managed-browser).

- **L'app Portale aziendale per Android offre ora all'utente finale una nuova esperienza dei criteri di protezione delle app**

  In base ai suggerimenti dei clienti, l'app Portale aziendale per Android è stata modificata in modo da includere un pulsante **Accesso al contenuto aziendale**. Lo scopo è impedire che gli utenti finali eseguano inutilmente il processo di registrazione quando hanno solo necessità di accedere alle app che supportano i criteri di protezione delle app, una funzionalità di gestione delle applicazioni mobili di Intune. È possibile visualizzare queste modifiche nella pagina delle [novità dell'interfaccia utente dell'app](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Nuova azione di menu per rimuovere facilmente Portale aziendale**

  In base ai suggerimenti degli utenti, nell'app Portale aziendale per Android è stata aggiunta a una nuova azione di menu per avviare la rimozione di Portale aziendale dal dispositivo. Questa azione rimuove il dispositivo dalla gestione di Intune in modo che l'utente possa rimuovere l'app dal dispositivo. È possibile visualizzare queste modifiche nella pagina [Novità dell'interfaccia utente dell'app](https://docs.microsoft.com/intune/whats-new-app-ui) e nella [documentazione di Android per l'utente finale](https://docs.microsoft.com/intune-user-help/unenroll-your-device-from-intune-android).

- **Miglioramenti alla sincronizzazione delle app con Windows 10 Creators Update**

  L'app Portale aziendale per Windows 10 a questo punto avvia automaticamente una sincronizzazione per le richieste di installazione di app per i dispositivi con Windows 10 Creators Update (versione 1703). Ciò riduce il problema del blocco dell'installazione di app durante lo stato "In attesa di sincronizzazione". Gli utenti sono anche in grado di avviare manualmente la sincronizzazione all'interno dell'app. È possibile visualizzare queste modifiche nella pagina delle [novità dell'interfaccia utente dell'app](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Nuova esperienza interattiva per Portale aziendale di Windows 10**

  L'app Portale aziendale per Windows 10 include un'esperienza guidata per Intune per i dispositivi che non sono stati identificati o registrati. La nuova esperienza fornisce istruzioni dettagliate che guidano l'utente nella fase di registrazione in Azure Active Directory (obbligatoria per le funzionalità di accesso condizionale) e la registrazione in MDM (obbligatoria per le funzionalità di gestione dei dispositivi). L'esperienza interattiva sarà accessibile dalla home page di Portale aziendale. Gli utenti possono continuare a usare l'app se non completano la registrazione, ma le funzionalità saranno limitate.

  Questo aggiornamento è disponibile solo nei dispositivi che eseguono l'Aggiornamento dell'anniversario di Windows 10 (build 1607) o versione successiva. È possibile visualizzare queste modifiche nella pagina delle [novità dell'interfaccia utente dell'app](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Miglioramenti ai riquadri dell'app nell'app Portale aziendale per iOS**

  La progettazione dei riquadri dell'app nella home page è stata aggiornata in modo da riflettere il colore della personalizzazione impostato per il Portale aziendale. Per altre informazioni, vedere la pagina delle [novità dell'interfaccia utente dell'app](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Selezione account ora disponibile per l'app Portale aziendale per iOS**

  Gli utenti di dispositivi iOS possono visualizzare la nuova selezione account quando effettuano l'accesso a Portale aziendale se usano il proprio account aziendale o dell'istituto di istruzione per accedere alle altre app Microsoft. Per altre informazioni, vedere la pagina delle [novità dell'interfaccia utente dell'app](https://docs.microsoft.com/intune/whats-new-app-ui).

### <a name="new-in-configuration-manager-technical-preview-1706"></a>Novità di Configuration Manager Technical Preview 1706

- **Nuove impostazioni degli elementi di configurazione di Windows**<!-- 1354715 -->    

  Nuovi elementi di configurazione di Windows sono disponibili per le categorie di impostazioni relative a password, dispositivi, archivi e Microsoft Edge. Per altre informazioni, vedere [Nuove attività degli elementi di configurazione di Windows](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-windows-configuration-item-settings).

- **Nuove regole per i criteri di conformità dei dispositivi**    

  È ora possibile configurare nuove opzioni per i criteri di conformità che in precedenza erano disponibili solo nella versione autonoma di Intune. Per i dettagli, vedere [Miglioramenti dei criteri di conformità dei dispositivi](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-device-compliance-policy-rules).

- **Restrizioni di registrazione di Android e iOS** <!-- 1290826 -->      

  Gli amministratori possono ora specificare che gli utenti non possono registrare dispositivi Android o iOS personali nel proprio ambiente ibrido. Ciò consente di limitare i dispositivi registrati ai dispositivi pre-dichiarati, ai dispositivi di proprietà dell'azienda o ai dispositivi iOS registrati solo tramite Device Enrollment Program. Per i dettagli vedere [Restrizioni di registrazione di Android e iOS](/sccm/core/get-started/capabilities-in-technical-preview-1706#android-and-ios-enrollment-restrictions).

- **Supporto per le autorità di certificazione Entrust** <!-- 1350740 -->     

  Configuration Manager supporta ora l'autorità di certificazione Entrust; ciò consente la consegna del certifica PFX nei dispositivi registrati in Microsoft Intune.    

  Quando si aggiunge un ruolo di punto di registrazione certificato in Configuration Manager, è possibile configurare Entrust come autorità di certificazione. Quando si aggiunge un nuovo profilo di certificato che emette i certificati PFX, è possibile selezionare l'autorità di certificazione Microsoft o Entrust.

  **Problema noto**: nella Technical Preview 1706, i certificati PFX non vengono emessi per le autorità di certificazione di Microsoft. Ciò non influenza i certificati PFX importati o i profili SCEP.

- **Supporto Cisco (IPsec) per i profili VPN di MacOS** <!-- 1321367 -->    

  È possibile creare un profilo VPN di MacOS con Cisco (IPsec) come tipo di connessione. Per altre informazioni, vedere [Creare i profili VPN](/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles).


## <a name="april-2017"></a>Aprile 2017

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

- **MyApps disponibile per Managed Browser**

  Microsoft MyApps offre ora un supporto migliore all'interno di Managed Browser. Gli utenti di Managed Browser che non sono assegnati alla gestione passeranno direttamente al servizio MyApps, in cui potranno accedere alle app SaaS con provisioning dell'amministratore. Gli utenti destinati alla gestione di Intune continueranno a poter accedere a MyApps dal segnalibro di Managed Browser incorporato.

- **Nuove icone per Managed Browser e il portale aziendale**

  Managed Browser riceve icone aggiornate per le versioni sia Android che iOS dell'app. La nuova icona conterrà il badge Intune aggiornato per renderla più coerente con altre app in Enterprise Mobility + Security (EM + S). È possibile visualizzare la nuova icona per Managed Browser nella [pagina delle novità dell'interfaccia utente dell'app Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

  Anche il portale aziendale riceve icone aggiornate per le versioni di Android, iOS e Windows dell'app per migliorare la coerenza con altre applicazioni in EM+S. Queste icone verranno rilasciate gradualmente tra piattaforme da aprile alla fine di maggio.

- **Indicatore dello stato di accesso nel portale aziendale Android**

  Un aggiornamento per l'app Portale aziendale Android visualizza un indicatore dello stato di accesso quando l'utente avvia o riprende l'uso dell'app. L'indicatore attraversa nuovi stati, a partire da "Connessione in corso...", quindi "Accesso in corso..." e infine "Verifica dei requisiti di protezione..." prima di consentire all'utente di accedere all'app. È possibile visualizzare le nuove schermate per l'app Portale aziendale di Intune per Android nella [pagina delle novità dell'interfaccia utente dell'app Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Bloccare l'accesso delle app a SharePoint Online**

  È ora possibile creare un criterio di accesso condizionale basato su app per bloccare l'accesso delle applicazioni, a cui non sono stati applicati criteri di protezione di app, a [SharePoint Online](https://docs.microsoft.com/intune-classic/deploy-use/mam-ca-for-sharepoint-online). Nello scenario di accesso condizionale basato su app, è possibile specificare le app che dovranno accedere a SharePoint Online usando il portale di Azure.

### <a name="new-in-configuration-manager-technical-preview-1704"></a>Novità di Configuration Manager Technical Preview 1704

- **Configurare le app Android con i criteri di configurazione delle app**

  È possibile usare i criteri di configurazione delle app in System Center Configuration Manager (Configuration Manager) per distribuire impostazioni preconfigurate quando un utente esegue un'app in un dispositivo Android for Work. I criteri di configurazione delle app per Android sono disponibili solo nei dispositivi che eseguono Android for Work e riguardano le applicazioni approvate per lo store Play for Work. Per altre informazioni su come provare questa funzionalità, vedere [Configurare le app Android con i criteri di configurazione delle app](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies).

## <a name="march-2017"></a>Marzo 2017

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

- **Nuova esperienza utente per l'app Portale aziendale per Android**

  L'app Portale aziendale per Android offre un'interfaccia utente dall'aspetto più moderno. Gli aggiornamenti più importanti riguardano gli aspetti seguenti:

  - Colori: le intestazioni delle schede dell'app Portale aziendale possono avere un colore personalizzato definito dal personale IT.
  - App: nella scheda **App** i pulsanti **App in evidenza** e **Tutte le app** sono stati aggiornati.
  - Ricerca: nella scheda **App** il pulsante **Cerca** è un pulsante di azione mobile.
  - Navigazione tra le app: in **Tutte le app** è disponibile una visualizzazione a schede di **In evidenza**, **Tutte** e **Categorie** per una navigazione più semplice.
  - Supporto: le schede **Dispositivi personali** e **Contatta l'IT** sono state aggiornate per migliorare la leggibilità.

  Per altre informazioni su queste modifiche, vedere [Aggiornamenti dell'interfaccia utente per le applicazioni degli utenti finali in Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Script di firma per l'app Portale aziendale di Windows 10**

  Se è necessario scaricare e trasferire localmente l'app Portale aziendale di Windows 10, è ora disponibile uno script per semplificare e ottimizzare il processo di firma dell'app per l'organizzazione.  Per scaricare lo script e le relative istruzioni d'uso, vedere [Microsoft Intune Signing Script for Windows 10 Company Portal](https://aka.ms/win10cpscript) (Script di firma di Microsoft Intune per l'app Portale aziendale di Windows 10) nella raccolta TechNet. Per altre informazioni su questo annuncio, vedere [Updating your Windows 10 Company Portal app](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) (Aggiornamento dell'app Portale aziendale per Windows 10) nel blog del team di supporto di Intune.

- **Supporto migliorato per gli utenti Android in Cina**

  A causa dell'assenza di Google Play Store in Cina, i dispositivi Android devono ottenere le app da marketplace cinesi. L'app Portale aziendale supporta questo flusso di lavoro reindirizzando gli utenti Android in Cina per scaricare le app Portale aziendale e Outlook da App Store locali. Ciò consente di migliorare l'esperienza utente quando sono abilitati i criteri di accesso condizionale, per la gestione sia dei dispositivi mobili che delle relative applicazioni. Le app Portale aziendale e Outlook per Android sono disponibili negli app store cinesi seguenti:

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

- **Verificare che le app Portale aziendale siano aggiornate**

  Nel mese di dicembre 2016 è stato rilasciato un aggiornamento che imponeva l'uso di Multi-Factor Authentication (MFA) a un gruppo di utenti che registrano un dispositivo iOS, Android, Windows 8.1+ o Windows Phone 8.1+. Questa funzionalità non può essere usata senza determinate versioni di base dell'app Portale aziendale per Android (5.0.3419.0+) e iOS (2.1.17+).

  Le funzionalità di gestione di Intune sono in continua evoluzione e molti miglioramenti sono accompagnati da aggiornamenti alle app Portale aziendale su tutte le piattaforme supportate. Di conseguenza, è consigliabile tenere installate nei dispositivi le versioni più recenti delle app Portale aziendale per poter sfruttare i vantaggi offerti dai miglioramenti in Intune e per garantire un'esperienza utente ottimale.

  >[!Tip]
  > Chiedere agli utenti di impostare i dispositivi in modo da aggiornare automaticamente le app dall'app store appropriato. Se si è resa disponibile l'app Portale aziendale per Android su una condivisione di rete, è possibile scaricare la versione più recente dall'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=49140).

- **Microsoft Teams è ora abilitato per MAM su iOS e Android**

  Nelle app Microsoft Teams per iOS e Android sono ora abilitate le funzionalità di gestione delle app mobili (MAM, Mobile App Management) di Intune. È così possibile consentire ai team di passare liberamente da un dispositivo all'altro, garantendo la protezione delle conversazioni e dei dati aziendali a ogni cambio di dispositivo. Per altre informazioni, vedere [l'annuncio relativo a Microsoft Teams](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/) nel blog di Enterprise Mobility + Security.

### <a name="new-in-configuration-manager-technical-preview-1703"></a>Novità di Configuration Manager Technical Preview 1703

- **Supporto aggiuntivo per scenari VPP (Volume Purchase Program) di Apple**

   A partire da Technical Preview 1703 è disponibile il supporto per gli scenari VPP (Volume Purchase Program) seguenti:

   - Licenze per dispositivi: le app che supportano le licenze per dispositivi e vengono distribuite in raccolte di dispositivi richiedono ora una sola licenza per ogni dispositivo.  In precedenza, era necessario usare una licenza per ogni utente in un dispositivo. Per altre informazioni, vedere [Distribuire app iOS acquistate con Volume Purchase Program a raccolte di dispositivi](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections).
   - Uso di più token VPP per un tenant singolo ibrido con entrambi i token usati per gestire le app VPP.
   - Uso di token per istituti di istruzione VPP con la possibilità di distinguere tra i token aziendali e di istituti di istruzione.

### <a name="new-in-configuration-manager-current-branch"></a>Novità di Configuration Manager (Current Branch)

Le funzionalità seguenti, che in precedenza erano disponibili nelle versioni di Configuration Manager Technical Preview, sono ora disponibili nelle distribuzioni ibride con Intune e Configuration Manager (Current Branch) versione 1702.

- [Supporto di Android for Work](/sccm/core/plan-design/changes/whats-new-in-version-1702##android-for-work-support)
- [Impostazioni di conformità di app non conformi](/sccm/core/plan-design/changes/whats-new-in-version-1702#conditional-access-device-compliance-policy-improvements)
- [Creazione e distribuzione del certificato PFX e supporto per S/MIME](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-to-certificate-profiles)
- [Non è più necessario specificare le versioni di Android e iOS nella creazione guidata della gestione ibrida dei dispositivi mobili](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)

Nella versione 1702 di Configuration Manager (Current Branch) sono disponibili anche le funzionalità ibride aggiuntive seguenti:

- **Supporto migliorato per Volume Purchase Program (VPP) di Apple**

  - È ora possibile distribuire app con licenza sia ai dispositivi che agli utenti. In base alla capacità dell'app di supportare la gestione delle licenze dei dispositivi, al momento della distribuzione viene richiesta una licenza appropriata, come indicato di seguito:

    | Versione di Configuration Manager | Gestione delle licenze dei dispositivi supportata | Tipo di raccolta della distribuzione | Licenza richiesta |
    |-|-|-|-|
    |Precedente la 1702|Sì|utente|Licenza utente|
    |Precedente la 1702|No|utente|Licenza utente|
    |Precedente la 1702|Sì|Dispositivo|Licenza utente|
    |Precedente la 1702|No|Dispositivo|Licenza utente|
    |1702 e versioni successive|Sì|utente|Licenza utente|
    |1702 e versioni successive|No|utente|Licenza utente|
    |1702 e versioni successive|Sì|Dispositivo|Licenza dispositivo|
    |1702 e versioni successive|No|Dispositivo|Licenza utente|

  - È ora possibile anche distribuire e tenere traccia delle app acquistate tramite iOS Volume Purchase Program for Education.

  - È ora possibile associare a Configuration Manager più token di Volume Purchase Program di Apple.

  Per altre informazioni sulle app iOS acquistate tramite Volume Purchase Program, vedere [Gestire le app iOS acquistate tramite Volume Purchase Program](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

- **Supporto per app line-of-business in Windows Store per le aziende**

  È ora possibile sincronizzare app line-of-business personalizzate da Windows Store per le aziende.

- **Nuovi strumenti di monitoraggio Mobile Threat Defense**

    Sono ora disponibili nuovi strumenti per il monitoraggio dello stato di conformità con il provider di servizi Mobile Threat Defense.

    Per altre informazioni, vedere [Monitorare la conformità a Mobile Threat Defense](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance).

## <a name="february-2017"></a>Febbraio 2017

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

- **Modernizzazione del sito Web del portale aziendale**

  Il sito Web del portale aziendale supporta app rivolte agli utenti che non hanno dispositivi gestiti. Il sito Web si allinea ad altri prodotti e servizi Microsoft usando una nuova combinazione di colori a contrasto, illustrazioni dinamiche e un "menu hamburger" che contiene i dettagli di contatto del supporto tecnico e le informazioni sui dispositivi gestiti esistenti. La pagina di destinazione è stata riorganizzata per evidenziare le app a disposizione degli utenti, con sequenze per le app in evidenza e aggiornate di recente. Nella pagina [UI updates](https://docs.microsoft.com/intune/whats-new-app-ui) (Aggiornamenti dell'interfaccia utente) sono disponibili immagini precedenti e successive all'aggiornamento.

- **Nuovo indirizzo del server MDM per dispositivi Windows**

  L'indirizzo del server MDM per la registrazione dei dispositivi Windows e Windows Phone è cambiato da manage.microsoft.com a enrollment.manage.microsoft.com. Comunicare agli utenti di usare enrollment.manage.microsoft.com come indirizzo del server MDM, se richiesto, durante la registrazione di un dispositivo Windows o Windows Phone. Questo aggiornamento richiede anche la sostituzione di qualsiasi CNAME in DNS che reindirizza EnterpriseEnrollment.contoso.com a manage.microsoft.com con un CNAME in DNS che reindirizzi EnterpriseEnrollment.contoso.com a EnterpriseEnrollment-s.manage.microsoft.com. Per altre informazioni su questa modifica, visitare http://aka.ms/intuneenrollsvrchange.

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Novità di Configuration Manager Technical Preview 1702

- **Supporto di Android for Work**

  È ora possibile gestire i dispositivi Android con Android for Work in ambienti ibridi MDM tramite Configuration Manager Technical Preview 1702. I dispositivi Android supportati possono ora essere registrati come dispositivi Android for Work, che crea un profilo di lavoro nel dispositivo a cui possono essere distribuite le app approvate in Play for Work. È possibile configurare e distribuire anche gli elementi di configurazione, i criteri di conformità e i profili di accesso alle risorse per questi dispositivi. Per altre informazioni, vedere [Supporto per Android for Work](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support).

- **Impostazioni di conformità di app non conformi**

  È ora possibile creare regole di app non conformi per app Android e iOS nei criteri di conformità. Se nei dispositivi sono installate le applicazioni specificate, queste vengono contrassegnate come "non conformi" e non hanno accesso alle risorse aziendali in base ai criteri di accesso condizionale in uso. Per altre informazioni, vedere [Miglioramento dei criteri di conformità dei dispositivi per l'accesso condizionale](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements).

- **Creazione e distribuzione del certificato PFX e supporto per S/MIME**

  È ora possibile creare e distribuire i certificati PFX agli utenti in un ambiente ibrido. Questi certificati possono essere quindi usati per la crittografia S/MIME della posta elettronica e la decrittografia da parte di dispositivi che l'utente ha registrato. Per altre informazioni, vedere [Creare certificati PFX con il supporto di S/MIME](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support).

- **Supporto per impostazioni di configurazione iOS aggiuntive**
   
    Sono ora disponibili 42 impostazioni iOS aggiuntive che è possibile configurare come parte di un elemento di configurazione. La maggior parte delle impostazioni, 35 in tutto, è stata aggiunta per dispositivi iOS con supervisione. Per altre informazioni, vedere [Nuove impostazioni di conformità per dispositivi iOS](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices).

## <a name="january-2017"></a>Gennaio 2017

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

- **Supporto di Android 7.1.1**

  Intune ora supporta e gestisce in modo completo Android 7.1.1.

- **Risolvere i problemi di inattività dei dispositivi iOS o di comunicazione tra la console di amministrazione e questi dispositivi**

  Quando i dispositivi degli utenti perdono il contatto con Intune, è possibile assegnare loro nuove istruzioni per la risoluzione dei problemi, in modo che possano riottenere l'accesso alle risorse aziendali. Vedere [Devices are inactive, or the admin console cannot communicate with them](https://docs.microsoft.com/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them) (I dispositivi sono inattivi o la console di amministrazione non può comunicare con loro).

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Novità di Configuration Manager Technical Preview 1701

- **Non è più necessario specificare le versioni di Android e iOS nella creazione guidata della gestione ibrida dei dispositivi mobili**

  A partire dalla Technical Preview 1701 per la gestione ibrida dei dispositivi mobili, non è più necessario indicare versioni specifiche di Android e iOS quando si creano nuovi criteri e profili per i dispositivi gestiti in Intune. Con questa modifica, le distribuzioni ibride possono offrire il supporto più rapidamente per le nuove versioni di Android e iOS, senza attendere una nuova versione o un'estensione di Configuration Manager. Per altre informazioni, vedere [Non è più necessario specificare le versioni di Android e iOS nella creazione guidata](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).


## <a name="notices"></a>Notifiche

### <a name="company-portal-for-windows-81-and-windows-phone-81-moving-to-sustaining-mode"></a>Passaggio dell'app Portale aziendale per Windows 8.1 e Windows Phone 8.1 alla modalità di solo supporto 
<!--1428681-->
*6 ottobre 2017*   
 
A partire da ottobre 2017, le app Portale aziendale per Windows 8.1 e Windows Phone 8.1 passeranno alla modalità di solo supporto. Ciò significa che le app e gli scenari esistenti, ad esempio la registrazione e la conformità, continueranno a essere supportati per queste piattaforme. Queste app continueranno a essere disponibili per il download tramite i canali di rilascio esistenti, ad esempio Microsoft Store. 

Quando saranno passate alla modalità di solo supporto, queste applicazioni riceveranno solo gli aggiornamenti di sicurezza critici. Non verranno rilasciati altri aggiornamenti né nuove funzionalità per queste app. Per le nuove funzionalità è consigliabile aggiornare i dispositivi a Windows 10 o a Windows 10 Mobile. 

### <a name="end-of-support-for-ios-80"></a>Fine del supporto per iOS 8.0 
<!---1164477--->
Per accedere alle risorse aziendali, le app gestite e l'app Portale aziendale per iOS richiederanno iOS 9.0 o versione successiva. I dispositivi non aggiornati prima di settembre non saranno in grado di accedere al Portale aziendale o alle app gestite. 

### <a name="platform-support-reminder-windows-phone-81-mainstream-support-ended-july-11-2017"></a>Promemoria di supporto di piattaforma: il supporto Mainstream di Windows Phone 8.1 è terminato l'11 luglio 2017
<!-- 1327781 -->
*11 luglio 2017*

La piattaforma Windows Phone 8.1 ha raggiunto la fine del supporto Mainstream. Ciò non influisce sul supporto di Windows 8.1 per PC.

Non ci sono conseguenze immediate a sui dispositivi Windows Phone 8.1 gestiti dal servizio Intune, inclusi quelli registrati in MDM ibrida. I dispositivi registrati continueranno a funzionare e tutti i criteri, le configurazioni e le app continueranno a funzionare come previsto. Si noti che all'interno del servizio Intune non ci sono miglioramenti destinati alla piattaforma Windows Phone 8.1 e all'app del Portale aziendale di Windows Phone 8.1.

È consigliabile eseguire l'aggiornamento dei dispositivi Windows Phone 8.1 idonei a Windows 10 Mobile non appena possibile.  

### <a name="end-of-support-for-android-43-and-lower"></a>Fine del supporto per Android 4.3 e versioni precedenti
<!---1171127--->
*6 luglio 2017*

Per accedere alle risorse aziendali, le app gestite e l'app Portale aziendale per Android richiederanno Android 4.4 o versione successiva. I dispositivi non aggiornati prima dell'inizio di ottobre non saranno in grado di accedere al Portale aziendale o alle app gestite. Nel mese di dicembre verrà imposto il ritiro di tutti i dispositivi registrati, con conseguente perdita dell'accesso alle risorse aziendali. Se si usano criteri di protezione delle app senza MDM, le app non riceveranno gli aggiornamenti e la qualità dell'esperienza diminuirà nel tempo.


### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 e System Center 2012 R2 Configuration Manager (RTM): il supporto per la gestione ibrida di dispositivi mobili termina il 10 aprile 2017
*11 gennaio 2017*

Il supporto per System Center 2012 Configuration Manager SP1 e System Center 2012 R2 Configuration Manager RTM è terminato il 12 luglio 2016. Per quanto riguarda la connessione di queste versioni al servizio Microsoft Intune per la gestione ibrida di dispositivi mobili, il supporto termina il 10 aprile 2017. Dopo tale data, la gestione ibrida di dispositivi mobili non sarà più disponibile con queste versioni. In pratica, i dispositivi gestiti non saranno più gestiti poiché il connettore Intune non si connetterà più al servizio Intune. I dati di Configuration Manager, ad esempio criteri e applicazioni, non verranno propagati a Intune e i dati dei dispositivi gestiti non verranno propagati a Configuration Manager finché non verrà eseguito un aggiornamento.

Se si esegue una distribuzione ibrida con Configuration Manager 2012 SP1 o R2 RTM, è consigliabile eseguire l'aggiornamento a Configuration Manager (Current Branch) o al Service Pack supportato più recente per Configuration Manager 2012 (R2 SP1 o SP2) prima del 10 aprile 2017 per evitare l'interruzione del servizio.

Risorse aggiuntive:
-   [Eseguire l'aggiornamento a System Center Configuration Manager (Current Branch)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-   [Pianificazione dell'aggiornamento a System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-   [Pianificazione dell'aggiornamento a System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Il caricamento del portale aziendale per Windows Phone 8 è deprecato
*25 ottobre 2016*

L'opzione che consente di caricare un'app Portale aziendale firmata è stata rimossa dalla console di Configuration Manager, poiché il supporto di Intune viene deprecato per Windows 8, Windows Phone 8 e Windows RT e il supporto per il portale aziendale per Windows Phone 8 termina in novembre.  I dispositivi Windows 8, Windows Phone 8 e Windows RT che sono già registrati continueranno a essere supportati, ma la registrazione di dispositivi aggiuntivi con queste piattaforme non sarà più supportata.


### <a name="see-also"></a>Vedere anche

- [Funzionalità MDM ibride precedenti](whats-new-hybrid-archive.md)
- [Novità di MDM in System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)

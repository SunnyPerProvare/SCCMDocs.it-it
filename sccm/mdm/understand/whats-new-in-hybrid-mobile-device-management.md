---
title: Novità nella gestione di dispositivi mobili ibrida
titleSuffix: Configuration Manager
description: Informazioni sulle nuove funzionalità di gestione dei dispositivi mobili disponibili per le distribuzioni ibride con Configuration Manager e Intune.
ms.date: 02/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c6e883b6ea5cea6d6b27863afc84eef774b4d552
ms.sourcegitcommit: f38ef9afb0c608c0153230ff819e5f5e0fb1520c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/19/2019
ms.locfileid: "58197147"
---
# <a name="whats-new-in-hybrid-mobile-device-management-with-configuration-manager-and-microsoft-intune"></a>Novità della gestione ibrida di dispositivi mobili con Configuration Manager e Microsoft Intune

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo illustra le nuove funzionalità di gestione dei dispositivi mobili (MDM) disponibili per le distribuzioni ibride con System Center Configuration Manager e Intune.     

> [!Important]  
> A partire dal 14 agosto 2018, la gestione ibrida dei dispositivi mobili è una [funzionalità deprecata](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Per altre informazioni, vedere [Informazioni sulla gestione di dispositivi mobili ibrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  


> [!Note]    
> Intune in Azure è la soluzione MDM consigliata da Microsoft.     
> - Per informazioni dettagliate sulle nuove caratteristiche e gli aggiornamenti in Intune autonomo, vedere [Novità di Microsoft Intune](https://docs.microsoft.com/intune/whats-new).    
> - Per informazioni dettagliate su come eseguire la migrazione a Intune autonomo, vedere [Migrate hybrid MDM users and devices to Intune standalone](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa) (Eseguire la migrazione di utenti e dispositivi di MDM ibrido a Intune autonomo).
> - Per informazioni dettagliate sugli aggiornamenti dell'interfaccia utente per Intune e MDM ibrido, vedere [Aggiornamenti dell'interfaccia utente per le applicazioni degli utenti finali in Intune](https://docs.microsoft.com/intune/whats-new-app-ui). 



##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilità con le versioni di Configuration Manager  

Ogni sezione di questo articolo elenca le funzionalità ibride in tre categorie diverse. Usare le indicazioni che seguono per determinare la compatibilità delle funzionalità di ogni categoria con versioni diverse di Configuration Manager:  

|Categorie di funzionalità|Descrizione|
|-|-|
|**Novità di Microsoft Intune** | In generale, tutte le funzionalità elencate in questa categoria dovrebbero funzionare con tutte le versioni di Configuration Manager, incluse le versioni di System Center 2012 R2 Configuration Manager, perché richiedono solo il servizio Intune e non richiedono altre funzionalità di Configuration Manager.|
|**Novità di Configuration Manager Technical Preview**| Tutte le funzionalità elencate in questa categoria funzionano solo con il ramo di Technical Preview specificato. Per provare queste funzionalità, è necessario installare la versione di Technical Preview specificata nella descrizione della funzionalità. Per altre informazioni, vedere [Technical Preview per Configuration Manager](/sccm/core/get-started/technical-preview).|
|**Novità di Configuration Manager (Current Branch)**| Tutte le funzionalità elencate in questa categoria funzionano solo con la versione di Configuration Manager (Current Branch) specificata. Se si usa una versione precedente di Configuration Manager per la distribuzione ibrida, eseguire l'aggiornamento alla versione di Configuration Manager (Current Branch) specificata nella descrizione della funzionalità. Per altre informazioni, vedere [Eseguire l'aggiornamento a Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).|



## <a name="february-2019"></a>Febbraio 2019

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

#### <a name="create-new-intune-tenants-in-azure-portal"></a>Creare nuovi tenant di Intune nel portale di Azure
<!--3754067-->  
La possibilità di creare un nuovo tenant MDM ibrida è stata rimossa del 1902 Intune aggiornata. Creare tutti i nuovi tenant di Intune nel portale di Azure. Si ricordi [hybrid MDM è deprecata](/sccm/mdm/understand/hybrid-mobile-device-management). Devono eseguire la migrazione di attuali clienti MDM ibrido a Intune autonomo appena possibile.

Per altre informazioni, vedere il [post di blog del supporto tecnico di Intune](https://aka.ms/hybrid_notification).


#### <a name="intune-uses-google-play-protect-apis-on-android-devices"></a>Intune Usa Google Play proteggere le API nei dispositivi Android 
<!--2577355-->  
Alcuni amministratori hanno un panorama applicativo BYOD in cui potrebbero radice gli utenti o jailbreak proprio telefono cellulare. Questo comportamento, mentre in alcuni casi non dannose, comporta un bypass molti dei criteri di Intune impostati per proteggere i dati dell'organizzazione nei dispositivi degli utenti finali. In questo modo, Intune fornisce il rilevamento root e jailbreak per dispositivi non registrati sia registrati. 

Con questa versione, Intune Usa ora Google Play proteggere le API per aggiungere i controlli di rilevamento radice esistenti per i dispositivi non registrati. Mentre Google non condivide i controlli di rilevamento radice che si verificano nella sua totalità, prevediamo di queste API per rilevare gli utenti che hanno una radice i propri dispositivi per qualsiasi motivo dalla personalizzazione del dispositivo allo stato in grado di ottenere gli aggiornamenti del sistema operativo più recente nei dispositivi meno recenti. Questi utenti possono quindi essere impediti l'accesso a dati aziendali o i propri account aziendali possono essere cancellati dalle proprie App criteri abilitata. 


#### <a name="new-app-categories-screen-in-the-company-portal-app-for-windows-10"></a>Nuove **categorie di App** schermata nell'app portale aziendale per Windows 10
<!--3834780-->  
Per migliorare l'esperienza di esplorazione e selezione di app nel portale aziendale per Windows 10, ora include una nuova schermata chiamata **categorie di App**. Gli utenti ora visualizzare le proprie App ordinate in categorie, ad esempio **in primo piano**, **Education**, e **produttività**. Questa modifica viene visualizzata nelle versioni di portale aziendale 10.3.3451.0 e versioni successive. Per visualizzare la nuova schermata, vedere [novità dell'interfaccia utente dell'app](https://docs.microsoft.com/intune/whats-new). Per altre informazioni sulle app nel portale aziendale, vedere [installare e condividere le app nel dispositivo](https://docs.microsoft.com/intune-user-help/install-apps-cpapp-windows).  


#### <a name="macos-users-are-prompted-to-update-their-password"></a>gli utenti di macOS vengono richiesto di aggiornare la propria password 
<!--1873216-->  
Nei dispositivi macOS, gli utenti finali viene richiesto di aggiornare la propria password. Questa richiesta si verifica ogni volta che un utente esegue un'attività che richiede l'autenticazione, ad esempio l'accesso al dispositivo. Utenti inoltre richiesto di aggiornare la password quando eseguire alcuna operazione che richiede privilegi amministrativi, ad esempio richiedendo l'accesso keychain.  


#### <a name="intune-macos-company-portal-dark-mode"></a>Intune macOS modalità scura portale aziendale
<!--3300524-->  
Il portale aziendale macOS di Intune ora supporta la modalità scura per macOS. Quando si abilita la modalità scura in un dispositivo macOS 10.14 +, l'App portale aziendale consente di regolare l'aspetto a colori che riflettere tale modalità.



## <a name="january-2019"></a>Gennaio 2019

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

#### <a name="intune-app-protection-policies-ui-update"></a>Aggiornamento dell'interfaccia utente di Intune app protection criteri 
<!--3251427-->  
È stato modificato le etichette per le impostazioni e i pulsanti per la protezione delle app di Intune rendere ogni più facile da comprendere. Alcune delle modifiche includono:  

- Controlli vengono modificati da **yes** / **alcun** principalmente i controlli ai **blocco** / **Consenti** e **disabilitare** / **abilitare** controlli. Le etichette vengono aggiornate anche.  

- Le impostazioni vengono riformattate, in modo che l'impostazione e la relativa etichetta siano side-by-side nel controllo, per fornire una migliore navigazione.   

Le impostazioni predefinite e il numero di impostazioni rimangono invariati, ma questa modifica consente all'utente di comprendere, esplorare e utilizzare le impostazioni più facilmente per applicare i criteri di protezione delle app selezionata. Per altre informazioni, vedere [delle impostazioni iOS](https://docs.microsoft.com/intune/app-protection-policy-settings-ios#access-requirements) e [impostazioni Android](https://docs.microsoft.com/intune/app-protection-policy-settings-android#access-requirements).

#### <a name="tenant-status-dashboard"></a>Dashboard dello stato del tenant
<!--1124854-->  
Il nuovo [pagina dello stato del Tenant](https://docs.microsoft.com/intune/tenant-status) fornisce un'unica posizione in cui è possibile visualizzare lo stato e i relativi dettagli per il tenant. Il dashboard è suddiviso in quattro aree:

- **Dettagli del tenant**: Visualizza le informazioni che includono il nome del Tenant e il percorso, l'autorità MDM, il totale registrato i dispositivi nel tenant e del numero di licenze. In questa sezione elenca anche la versione corrente del servizio per il tenant.  

- **Lo stato del connettore**: Visualizza informazioni sui connettori disponibili è configurato ed è anche possibile elencare quelli che non è ancora abilitata.  

    Basato sullo stato corrente di ogni connettore, vengono contrassegnati come non integro, avviso o integro. Selezionare un connettore per il drill-through e visualizzare i dettagli o configurare informazioni aggiuntive per tale istanza.  

- **Integrità dei servizi Intune**: Consente di visualizzare i dettagli relativi a eventi imprevisti attivi o interruzioni per il tenant. Le informazioni contenute in questa sezione viene recuperate direttamente dal centro messaggi di Office.  

- **Novità di Intune**: Consente di visualizzare i messaggi attivi per il tenant. I messaggi includono elementi quali le notifiche quando il tenant riceve le funzionalità di Intune più recente.  Le informazioni contenute in questa sezione viene recuperate direttamente dal centro messaggi di Office.  

#### <a name="new-help-and-support-experience-in-company-portal-for-windows-10"></a>Nuova Guida e supporto tecnico esperienza nel portale aziendale per Windows 10 
<!--1488939-->  
La nuova pagina nella Guida del portale aziendale e supporto consente agli utenti di risolvere i problemi e richiedere assistenza per problemi di app e l'accesso. Dalla nuova pagina, possono inviare tramite posta elettronica di errori e i dettagli del log di diagnostica e trovare i dettagli di supporto tecnico dell'organizzazione. È disponibile anche una sezione Domande frequenti con i collegamenti per la relativa documentazione di Intune. Per altre informazioni e screenshot, vedere [assistenza e supporto nel portale aziendale per Windows 10](https://docs.microsoft.com/intune-user-help/help-and-support-windows-cpapp).

#### <a name="some-bitlocker-settings-support-windows-10-pro-edition"></a>Alcune impostazioni BitLocker supportano Windows 10 Pro edition
<!--2727036-->  
È possibile creare un elemento di configurazione che imposta le impostazioni di endpoint protection nei dispositivi Windows 10, tra cui BitLocker. Questo aggiornamento aggiunge il supporto per Windows 10 Professional edition per alcune impostazioni di BitLocker.

Per altre informazioni, vedere [impostazioni di crittografia per Windows 10](/sccm/mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client#encryption).



## <a name="december-2018"></a>Dicembre 2018

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

#### <a name="microsoft-auto-update-version-450-required-for-macos-devices"></a>Versione di aggiornamento automatico Microsoft 4.5.0 necessaria per i dispositivi macOS
<!--3503442-->  
Per continuare a ricevere gli aggiornamenti per l'App portale aziendale e altre applicazioni di Office, è necessario aggiornare i dispositivi macOS gestiti da Intune per l'aggiornamento automatico Microsoft 4.5.0. Gli utenti potrebbero disporre già questa versione per le app di Office.

#### <a name="the-intune-app-sdk-will-support-256-bit-encryption-keys"></a>Intune App SDK supporta le chiavi di crittografia a 256 bit 
<!--1832174-->  
Intune App SDK per Android ora Usa le chiavi di crittografia a 256 bit durante la crittografia è abilitata per i criteri di protezione delle App. il SDK continuerà a fornire supporto di chiavi a 128 bit per garantire la compatibilità con le app che usano versioni precedenti di SDK e contenuti.

#### <a name="intune-requires-macos-1012-or-later"></a>Intune richiede macOS 10.12 o versione successiva 
<!--2827778-->  
Intune è ora necessario macOS 10.12 o versione successiva. I dispositivi con versioni precedenti di macOS non è possibile usare l'App portale aziendale per registrarsi in Intune. Per ricevere supporto tecnico e le nuove funzionalità, gli utenti devono aggiornare il dispositivo MacOS 10.12 o versione successiva e aggiornare l'App portale aziendale alla versione più recente.

Per altre informazioni, vedere [modifiche pianificate: Intune supporta macOS 10.12 e versioni successive nel mese di dicembre](#plan-for-change-intune-supports-macos-1012-and-higher-in-december).



## <a name="november-2018"></a>Novembre 2018

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

#### <a name="new-intune-device-subscription-sku"></a>Nuova sottoscrizione di dispositivo Intune SKU
<!--3312071-->  
Per consentire più basso il costo di gestione dei dispositivi nelle aziende, una sottoscrizione basata su dispositivo nuovo SKU è ora disponibile. Questo dispositivo di Intune SKU è concesso in licenza per ogni dispositivo su base mensile. Prezzo varia in base al programma di licenza. È disponibile nel canale Direct, Enterprise Agreement (EA), Microsoft Products e Services programma (MPSA) e Open e Cloud Solution Provider (CSP).

#### <a name="new-apps-support-with-app-protection-policies"></a>Supporto di nuove app con criteri di protezione delle app 
<!--3330037-->  
È ora possibile gestire le app seguenti con [criteri di protezione app di Intune](https://docs.microsoft.com/intune/app-protection-policies):

- Stream (iOS)  
- Azioni (Android, iOS)  
- PowerApps (Android, iOS)  
- Flusso (Android, iOS)  

Usare criteri di protezione delle app per la protezione azienda trasferimento dati e controllo dei dati per queste App, come altre App gestite da criteri di Intune. 

> [!Note]  
> Se il flusso non è ancora visibile nella console, aggiungere il flusso quando si crea o modifica eventuali criteri di protezione delle app. Selezionare **altre app**, quindi specificare il *App ID* per Flow nel campo di input. Per l'uso di Android `com.microsoft.flow`, e per iOS usare `com.microsoft.procsimo`.  



## <a name="october-2018"></a>Ottobre 2018

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

#### <a name="updates-for-application-transport-security"></a>Aggiornamenti per Application Transport Security 
<!--748318-->  
Microsoft Intune supporta la sicurezza TLS (Transport Layer) 1.2 + per la crittografia migliori, per verificare che Intune è più sicuro per impostazione predefinita e l'allineamento con altri servizi Microsoft, ad esempio Microsoft Office 365. Per poter soddisfare questo requisito, i portali aziendali iOS e macOS applicheranno i requisiti di Application Transport Security (ATS) aggiornati di Apple che richiedono anche TLS 1.2+. ATS viene usato per applicare una sicurezza più rigorosa a tutte le comunicazioni delle app su HTTPS. Questa modifica interessa i clienti di Intune che usano le app del portale aziendale iOS e macOS. Per altre informazioni, vedere [Intune moving to TLS 1.2 for encryption](https://blogs.technet.microsoft.com/intunesupport/2018/06/05/intune-moving-to-tls-1-2-for-encryption/) (Transizione di Intune a TLS 1.2 per la crittografia).

#### <a name="remove-an-email-profile-from-a-device-even-when-theres-only-one-email-profile"></a>Rimuovere un profilo di posta elettronica da un dispositivo, anche quando è presente un solo profilo di posta elettronica 
<!--1818139-->  
In precedenza, non è stato possibile rimuovere un profilo di posta elettronica da un dispositivo se è l'unico profilo di posta elettronica. Con questo aggiornamento, questo comportamento viene modificato. Ora è possibile rimuovere un profilo di posta elettronica, anche se è l'unico profilo di posta elettronica presente nel dispositivo. 

#### <a name="remove-pkcs-and-scep-certificates-from-your-devices"></a>Rimuovere i certificati PKCS e SCEP dai dispositivi 
<!--3218390-->  
In alcuni scenari, i certificati SCEP e PKCS rimangono nei dispositivi, anche quando si rimuove un criterio da un gruppo, l'eliminazione di una configurazione o distribuzione di conformità o da un amministratore l'aggiornamento di un profilo SCEP o PKCS esistente. 

Questo aggiornamento modifica il comportamento. In alcuni scenari i certificati PKCS e SCEP vengono rimossi dai dispositivi, mentre in altri scenari questi certificati rimangono nel dispositivo. 

#### <a name="access-to-key-profile-properties-using-the-company-portal-app"></a>Accedere alle proprietà principali del profilo tramite l'app Portale aziendale
<!--772203-->  
Gli utenti finali possono ora accedere alle proprietà e alle azioni principali per gli account, ad esempio la reimpostazione della password, dall'app Portale aziendale. 

#### <a name="pin-prompt-when-you-change-fingerprints-or-face-id-on-an-ios-device"></a>Richiesta del PIN quando si modificano le impronte digitali o l'ID del viso in un dispositivo iOS  
<!--2637704-->  
Agli utenti viene ora richiesto un PIN dopo la modifica dei dati biometrici nel proprio dispositivo iOS. Sono incluse le modifiche alle impronte digitali o all'ID del viso registrati. La durata del messaggio di richiesta dipende dalla configurazione del timeout *Controlla di nuovo i requisiti di accesso dopo (minuti)*.  Se non è impostato alcun PIN, all'utente viene richiesto di impostarne uno.  

Questa funzionalità è disponibile solo per iOS e richiede la partecipazione delle applicazioni che integrano Intune APP SDK per iOS, versione 8.1.1 o versioni successive. L'integrazione dell'SDK è necessaria in modo il comportamento possa essere imposto nelle applicazioni di destinazione. Questa integrazione avviene sistematicamente e dipende dai team delle applicazioni specifiche. Alcune app partecipanti sono WXP, Outlook, Managed Browser e Yammer.

#### <a name="end-user-device-and-app-content-menu"></a>Dispositivo dell'utente finale e menu di scelta rapida delle app 
<!--2771453-->  
Gli utenti finali possono ora usare il menu di scelta rapida nel dispositivo e nelle app per attivare azioni comuni come la ridenominazione di un dispositivo o il controllo della conformità. 

#### <a name="windows-company-portal-keyboard-shortcuts"></a>Tasti di scelta rapida per il portale aziendale di Windows
<!--2771518-->  
Gli utenti finali possono ora attivare le azioni per app e dispositivi nel portale aziendale di Windows tramite tasti di scelta rapida.



## <a name="august-2018"></a>Agosto 2018

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

#### <a name="new-user-experience-update-for-the-company-portal-website"></a>Nuovo aggiornamento dell'esperienza utente per il sito Web Portale aziendale
<!--2000968-->  
Basata su commenti e suggerimenti, sono state aggiunte nuove funzionalità al sito Web del portale aziendale. Le funzionalità esistenti e la semplicità d'uso risulteranno molto migliorate dai dispositivi Android, iOS e Windows. In alcune aree del sito è stato applicato un nuovo design reattivo moderno. Tali aree includono quelle relative a dettagli dei dispositivi, commenti e suggerimenti e supporto tecnico e panoramica dei dispositivi. Sono stati inoltre apportati i miglioramenti seguenti:

- Semplificazione dei flussi di lavoro in tutte le piattaforme per dispositivi
- Miglioramento dei flussi di identificazione e registrazione dei dispositivi
- Messaggi di errore più utili
- Linguaggio più semplice con meno gergo tecnico
- Possibilità di condividere collegamenti diretti alle app
- Miglioramento delle prestazioni per i cataloghi di app di grandi dimensioni
- Maggiore accessibilità per tutti gli utenti



## <a name="july-2018"></a>Luglio 2018

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

#### <a name="updated-intune-app-sdk-for-android-is-now-available"></a>Versione aggiornata di Intune App SDK per Android ora disponibile
<!--2744271-->  
Una versione aggiornata di Intune App SDK per Android è disponibile per il supporto della versione di Android a torta 9. Gli sviluppatori di app che usano Intune SDK per Android possono installare la versione aggiornata di Intune App SDK. Questo aggiornamento garantisce che la funzionalità di Intune nelle app Android continui a funzionare come previsto nei dispositivi Android Pie 9. Questa versione di Intune App SDK offre un plug-in integrato che esegue gli aggiornamenti SDK. Non è necessario riscrivere il codice esistente integrato. Per altre informazioni, vedere [Intune SDK per Android](https://github.com/msintuneappsdk/ms-intune-app-sdk-android). 

Se si usa lo stile di personalizzazione precedente per Intune, iniziare a usare l'icona a forma di valigetta. Per altre informazioni sulla personalizzazione, vedere [Intune App Badging System](https://github.com/msintuneappsdk/intune-app-partner-badge) (Sistema di personalizzazione di app di Intune).


#### <a name="support-for-security-enhancement-in-intune-service"></a>Supporto per miglioramenti della sicurezza nel servizio Intune
<!--2520152-->  
È ora possibile specificare che i dispositivi senza criteri di conformità assegnato non conformi nell'ambiente ibrido. Configurare questa impostazione in Intune nel portale di Azure. È consigliabile abilitare questa funzionalità per proteggere le risorse interne.

Nei tenant ibridi questa funzionalità è disabilitata per impostazione predefinita. Quando si abilita questa funzionalità, i dispositivi che non hanno criteri di conformità assegnati vengono considerati non conformi. Se si abilita anche l'accesso condizionale, questi dispositivi non potranno accedere alle risorse interne, ad esempio Outlook o SharePoint, in base ai criteri di accesso condizionale nell'ambiente. Se si lascia questa impostazione disabilitata, questi dispositivi continueranno ad avere lo stesso livello di accesso di sempre.

Per capire meglio quale impatto può avere questa funzionalità se attivata, è disponibile uno [script nella raccolta di TechNet](https://gallery.technet.microsoft.com/SQL-Query-for-Hybrid-MDM-5bcb8695). Eseguendo lo script nel database di Configuration Manager, vengono elencati i dispositivi che non sono interessati dai criteri di conformità.

Per altre informazioni, vedere gli articoli seguenti:
- Post di blog [Security Enhancements in the Intune Service](https://aka.ms/compliance_policies) (Miglioramenti apportati alla sicurezza nel servizio Intune) 
- [Criteri di conformità del dispositivo in Configuration Manager](/sccm/mdm/deploy-use/device-compliance-policies)

#### <a name="updates-to-out-of-compliance-messages-in-company-portal-app"></a>Aggiornamenti per i messaggi di mancata conformità nell'app Portale aziendale 
<!--1832222-->  
Si sta rivedere i messaggi che gli utenti dei dispositivi visualizzano quando un dispositivo è insufficiente conformi. I messaggi conservano il significato originale, ma vengono aggiornati con un linguaggio più descrittivo e un minor uso di terminologia tecnica. Verranno anche aggiornati i collegamenti alla documentazione e alle procedure di correzione per mantenerli aggiornati.  

Il testo seguente è un esempio dei miglioramenti dei messaggi che verranno introdotti:  

- Prima: *Questo dispositivo non ha contattato il servizio Intune nel periodo di tempo specificato richiesto dall'amministratore IT. Per risolvere questo problema, aprire l'app Portale aziendale nel dispositivo e fare clic sul pulsante Controlla conformità.*  

- Dopo: *Il dispositivo non è archiviato con l'organizzazione in un periodo di tempo. Per ristabilire una connessione, aprire l'app Portale aziendale nel dispositivo e toccare Verifica le impostazioni per il dispositivo.*  

#### <a name="select-device-categories-by-using-the-access-work-or-school-settings"></a>Selezionare le categorie di dispositivi usando le impostazioni per l'accesso all'azienda o all'istituto di istruzione 
<!--1058963-->  
Se è stato abilitato [mapping del gruppo di dispositivi](https://docs.microsoft.com/intune/device-group-mapping), gli utenti in Windows 10 a questo punto vengono richiesto di selezionare una categoria di dispositivi dopo la registrazione tramite il **Connect** sul pulsante **impostazioni**  >  **Conti** > **accesso azienda o dell'istituto di istruzione**.  

#### <a name="new-browsing-experiences-in-the-company-portal-app-for-windows"></a>Nuove esperienze di esplorazione nell'app Portale aziendale per Windows 
<!--2317227-->  
A questo punto durante l'esplorazione o la ricerca per le app nell'app portale aziendale per Windows, viceversa esistente **riquadri** appena aggiunta e visualizzazione **dettagli** visualizzazione. La nuova vista elenca i dettagli dell'applicazione, ad esempio nome, editore, data di pubblicazione e stato dell'installazione. 

La vista **Installata** della pagina **App** consente di visualizzare i dettagli delle installazioni delle app completate e in corso. Per visualizzare l'aspetto della nuova vista, vedere [Novità dell'interfaccia utente](https://docs.microsoft.com/intune/whats-new-app-ui).

#### <a name="more-opportunities-to-sync-in-the-company-portal-app-for-windows"></a>Altre opportunità per eseguire la sincronizzazione nell'app Portale aziendale per Windows  
<!--2683177-->  
A questo punto l'app portale aziendale per Windows consente di avviare la sincronizzazione direttamente dalla barra delle applicazioni Windows e menu Start. Questa funzionalità è particolarmente utile se le uniche attività sono la sincronizzazione dei dispositivi e l'accesso alle risorse aziendali. Per accedere alla nuova funzionalità, fare clic con il pulsante destro del mouse sull'icona Portale aziendale aggiunta alla barra delle applicazioni o al menu Start. Tra le opzioni del menu scegliere **Sincronizza il dispositivo**. Questo menu è detto anche jump list. Dal portale aziendale si accede alla pagina **Impostazioni** e la sincronizzazione viene avviata. Per la procedura aggiornata, vedere l'articolo relativo alla [sincronizzazione manuale del dispositivo Windows](https://docs.microsoft.com/intune/intune-user-help/sync-your-device-manually-windows#sync-from-device-taskbar-or-start-menu).



## <a name="june-2018"></a>Giugno 2018

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

#### <a name="access-to-macos-company-portal-pre-release-build"></a>Accesso alla build in versione non definitiva di Portale aziendale macOS 
<!--1734766-->  
Usa Microsoft AutoUpdate, Iscriviti per ricevere le compilazioni tempestivamente unendo in join il programma di Insider. L'iscrizione consente di usare il portale aziendale aggiornato prima che sia disponibile per gli utenti finali.

#### <a name="intune-app-protection-policies-and-microsoft-edge"></a>Criteri di protezione delle app di Intune e Microsoft Edge 
<!--1818968,1818969-->  
Il browser Microsoft Edge per dispositivi mobili (iOS e Android) ora supporta criteri di protezione delle app di Microsoft Intune. Gli utenti di dispositivi iOS e Android che accedono all'applicazione Edge tramite account di Azure Active Directory aziendali sono protetti da Intune. Nei dispositivi iOS, i criteri **Richiedi un browser gestito per l'apertura del collegamento** consentono agli utenti di aprire collegamenti in Edge, se quest'ultimo è gestito.



## <a name="may-2018"></a>Maggio 2018

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

#### <a name="requesting-help-in-the-company-portal-for-windows-10"></a>Richiesta di assistenza in Portale aziendale per Windows 10 
<!--1874137-->  
Portale aziendale per Windows 10 ora invia i log dell'app direttamente a Microsoft quando l'utente avvia il flusso di lavoro di richiesta di assistenza per risolvere un problema. Questo comportamento rende più semplice la risoluzione dei problemi segnalati a Microsoft.  


### <a name="new-in-configuration-manager-current-branch"></a>Novità di Configuration Manager (Current Branch)

#### <a name="android-for-work-and-lookout-onboarding-moved-to-intune-on-azure"></a>Android for Work e onboarding Lookout spostati in Intune in Azure
<!--2355022,2357366-->  
Con l'aggiornamento di Intune più recente è possibile abilitare e gestire l'integrazione di Android for Work e della protezione dalle minacce per dispositivi mobili di Lookout nei tenant di gestione di dispositivi mobili ibrida in Intune nel portale di Azure. Prima dell'aggiornamento, queste impostazioni erano configurabili solo nel portale di Intune classico (Silverlight).
 
Nota: Lookout è il provider di solo mobile threat defense (MTD) supportato in ambiente ibrido. Se in precedenza è stata eseguita l'integrazione con un altro provider MTD, quest'ultimo compare comunque in Intune nel portale di Azure. Se si elimina il connettore di questo, non è possibile aggiungerlo di nuovo.
 
Queste modifiche non influiscono sulle funzionalità esistenti. Continuare a usare la console di Configuration Manager per la gestione delle app correlate, per la creazione di report e per i criteri.
 
Per altre informazioni, vedere gli articoli seguenti:
- [Configurare la gestione di dispositivi Android ibrida](/sccm/mdm/deploy-use/enroll-hybrid-android)
- [Gestire l'accesso alle risorse aziendali in base ai rischi per dispositivi, rete e applicazioni](/sccm/mdm/deploy-use/lookout-mobile-threat-defense-in-configuration-manager)


#### <a name="support-for-new-versions-of-cisco-anyconnect-client-for-ios"></a>Supporto per nuove versioni del client Cisco AnyConnect per iOS
<!--1357393-->  
È possibile abilitare il supporto per Cisco AnyConnect per iOS 4.0.7 o versione successiva. In questo modo, i profili VPN Cisco AnyConnect esistenti vengono etichettati **Cisco Legacy AnyConnect** e continuano a funzionare come prima. L'opzione **Cisco AnyConnect** è per i profili VPN nuovi che possono essere usati con Cisco AnyConnect su iOS 4.0.7 o versione successiva.

  > [!Tip]  
  > Cisco AnyConnect 4.0.07x e versioni successive per iOS è una funzionalità introdotta per la prima volta nella versione 1802 come [versione non definitiva](/sccm/core/servers/manage/pre-release-features). A partire dall'[aggiornamento 4163547](https://support.microsoft.com/help/4163547) per la versione 1802, questa funzionalità non è più in versione non definitiva.  

> [!Note]  
> Continuare a usare l'opzione **Cisco AnyConnect Legacy** per i profili VPN macOS. 



## <a name="april-2018"></a>Aprile 2018

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

#### <a name="intune-adapts-to-fluent-design-system-in-the-company-portal-app-for-windows-10"></a>Intune si adatta a Fluent Design System nell'app Portale aziendale per Windows 10 
<!--1195010-->  
L'app Portale aziendale Intune per Windows 10 è stata aggiornata con la [visualizzazione della navigazione di Fluent Design System](/windows/uwp/design/basics/navigation-basics). A lato dell'app si noti un elenco verticale statico di tutte le pagine di primo livello. Fare clic su un collegamento per visualizzare rapidamente tutte le pagine e passare da una all'altra. Questo è il primo di molti aggiornamenti che saranno resi disponibili come parte del continuo impegno per creare un'esperienza più adattiva, empatica e familiare in Intune. Per visualizzare l'aspetto aggiornato, vedere [Novità dell'interfaccia utente dell'app](/intune/whats-new-app-ui).

#### <a name="improved-device-tiles-in-the-windows-10-company-portal"></a>Riquadri di dispositivo migliorati nel Portale aziendale di Windows 10
<!--2213364-->  
I riquadri sono stati aggiornati per risultare più accessibili agli utenti con ipovisione e offrire prestazioni migliori per gli strumenti per la lettura su schermo.


#### <a name="test-the-company-portal-for-macos-on-virtual-machines"></a>Testare il Portale aziendale per macOS nelle macchine virtuali
<!--2216679-->  
Abbiamo pubblicata indicazioni che consentono agli amministratori IT di testare l'app Portale aziendale per macOS nelle macchine virtuali in Parallels Desktop e VMware Fusion. Per altre informazioni, vedere [Registrare le macchine virtuali macOS per i test](/intune/macos-enroll#enroll-virtual-macos-machines-for-testing).


#### <a name="send-diagnostic-reports-in-company-portal-app-for-macos"></a>Inviare i report di diagnostica nell'app Portale aziendale per macOS
<!--2216677-->  
L'app Portale aziendale per i dispositivi macOS è stata aggiornata per migliorare il modo in cui gli utenti segnalano gli errori relativi a Intune. Dall'app Portale aziendale gli utenti possono:

- Caricare i report di diagnostica direttamente al team di sviluppo Microsoft.
- Inviare tramite posta elettronica l'ID dell'evento imprevisto al team di supporto IT dell'azienda.


#### <a name="updated-help-experience-on-company-portal-app-for-android"></a>Esperienza Guida aggiornata per l'app Portale aziendale per Android 
<!--1631531-->  
È stata aggiornata l'esperienza Guida nell'app Portale aziendale per Android per la compatibilità con le procedure consigliate per la piattaforma Android. Quando gli utenti riscontrano un problema nell'app, ora possono toccare **Menu** > **Guida** e:
- Caricare i log di diagnostica in Microsoft.
- Inviare un messaggio di posta elettronica con la descrizione del problema e l'ID evento imprevisto a un addetto del supporto aziendale.


#### <a name="update-where-to-configure-your-app-protection-policies"></a>Aggiornare la posizione in cui configurare i criteri di protezione dell'app 
<!--2144597-->  
Nel portale di Azure all'interno del servizio di Microsoft Intune, verrà temporaneamente reindirizzati dal **Intune App Protection** area per il **app per dispositivi mobili** sezione. Tutti i criteri di protezione delle app sono già nella sezione **App per dispositivi mobili** in Intune sotto la configurazione delle app. Invece di andare a Protezione app di Intune, si passerà a Intune. Ad aprile 2018 il reindirizzamento verrà interrotto e **Protezione app di Intune** verrà completamente rimossa. Dopo tale data, sarà presente una sola posizione per i criteri di protezione delle app in Intune. 

**Quali sono le conseguenze di questa modifica?** Questa modifica avrà effetto sia sui clienti di Intune autonomi che sui clienti ibridi (Intune con Configuration Manager). Questa integrazione consentirà di semplificare l'amministrazione della gestione del cloud.

**Operazioni di preparazione alla modifica** Contrassegnare **Intune** come preferito invece di **Protezione app di Intune**. Acquisire familiarità con il flusso di lavoro dei criteri di protezione dell'app nell'area **App per dispositivi mobili** in Intune. Per un breve periodo di tempo verrà effettuato il reindirizzamento e quindi **Protezione app** verrà rimossa. Tenere presente che tutti i criteri di protezione delle app sono già in Intune ed è possibile modificare qualsiasi criterio di accesso condizionale. Per altre informazioni sulla modifica dei criteri di accesso condizionale, vedere [Accesso condizionale in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). Per altre informazioni, vedere [Che cosa sono i criteri di protezione delle app?](https://docs.microsoft.com/intune/app-protection-policy) 




#### <a name="user-experience-update-for-the-company-portal-app-for-ios"></a>Aggiornamento dell'esperienza utente per l'app Portale aziendale per iOS 
<!--1412866-->  
È stato rilasciato un aggiornamento dell'esperienza utente principale per l'app Portale aziendale per iOS. L'aggiornamento include una riprogettazione visuale completa con un aspetto modernizzato. La funzionalità dell'app è stata mantenuta, ma migliorandone il livello di usabilità e accessibilità.  

L'aggiornamento include anche:
- Supporto per iPhone X.
- Tempi di risposta più rapidi per l'avvio e il caricamento dell'app, per consentire agli utenti di risparmiare tempo.
- Indicatori di stato aggiuntivi per offrire agli utenti informazioni sullo stato più aggiornate.
- Miglioramenti della modalità di caricamento dei log, in modo che sia possibile segnalare eventuali problemi.  

Per visualizzare l'aspetto aggiornato, vedere [Novità dell'interfaccia utente dell'app](https://docs.microsoft.com/intune/whats-new-app-ui).



## <a name="march-2018"></a>Marzo 2018

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

#### <a name="windows-company-portal-send-feedback-option-may-no-longer-work"></a>L'opzione Invia commenti e suggerimenti del Portale aziendale di Windows potrebbe non funzionare più
<!--2070166-->  
L'app Portale aziendale di Windows include l'opzione "Invia commenti e suggerimenti" che consente agli utenti di inviare a Microsoft commenti e suggerimenti sull'app. Dal 30 aprile 2018, questa opzione continua a essere supportata solo nell'app Portale aziendale di Windows 10 in esecuzione in Windows 10 versione 1607 e successive.   

**Quali sono le conseguenze di questa modifica?**

Se l'app Portale aziendale di Windows non è installata per gli utenti finali, ignorare questo messaggio.

Se gli utenti finali usano l'app Portale aziendale, a partire dal 30 aprile il pulsante "Invia commenti e suggerimenti" non funzionerà più per l'app negli scenari seguenti:  

 - App Portale aziendale di Windows 10 in Windows 10 versioni 1507 e 1511  

 - App Portale aziendale di Windows Phone 8.1  

Per i dispositivi interessati, l'opzione "Invia commenti e suggerimenti" non funziona al primo tentativo né a quelli successivi. Per inviare commenti e suggerimenti a Microsoft relativi alle esperienze in queste piattaforme, sono disponibili i canali alternativi elencati di seguito.

**Operazioni di preparazione alla modifica**

Informare di questa modifica gli utenti finali e aggiornare eventuali materiali sussidiari, se necessario. 

Informare gli utenti finali che usano il Portale aziendale in Windows Phone 8.1, Windows 10 versione 1507 e Windows 10 versione 1511 della disponibilità di due canali alternativi. Gli utenti possono:  

- Usare l'app Hub di Feedback in Windows 10  
- Inviare un messaggio di posta elettronica a WinCPfeedback@microsoft.com  

Chiedere agli utenti finali che usano Windows 10 versione 1607 o successiva di eseguire l'aggiornamento alla versione più recente del Portale aziendale di Windows disponibile in Microsoft Store.



#### <a name="azure-active-directory-web-sites-can-require-the-intune-managed-browser-app-and-support-single-sign-on-for-the-managed-browser-public-preview"></a>I siti Web di Azure Active Directory possono richiedere l'app Intune Managed Browser e supportano il Single Sign-On per Managed Browser (anteprima pubblica)
<!-- 710595 -->  
Tramite Azure Active Directory (Azure AD) è ora possibile limitare l'accesso ai siti Web nei dispositivi mobili all'app Intune Managed Browser. Nel browser gestito i dati del sito Web rimarranno protetti e separati dai dati personali dell'utente finale. Managed Browser supporta inoltre le funzionalità Single Sign-On per i siti protetti da Azure AD. L'accesso a Managed Browser o l'uso di Managed Browser in un dispositivo con un'altra app gestita da Intune consente a Managed Browser di accedere ai siti aziendali protetti da Azure AD senza che l'utente debba immettere le proprie credenziali. Questa funzionalità si applica a siti quali Outlook Web Access (OWA) e SharePoint Online, nonché ad altri siti aziendali, ad esempio le risorse Intranet a cui si accede tramite il proxy app di Azure.



## <a name="february-2018"></a>Febbraio 2018

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

- **Supporto del portale aziendale macOS per le registrazioni che usano il manager di registrazione dispositivi**  
    Gli utenti ora possono usare il manager di registrazione dispositivi durante la registrazione con il portale aziendale macOS.
    <!-- 1352411 -->  


## <a name="january-2018"></a>Gennaio 2018

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

- **Approvare l'app Portale aziendale per Android for Work**  
  Se nell'organizzazione viene usato Android for Work, approvare manualmente l'app Portale aziendale per Android. L'app continuerà a ricevere gli aggiornamenti automatici dalla versione gestita di Google Play Store.
  <!--1797090 -->  

- **I criteri di accesso condizionale per Intune sono disponibili solo dal portale di Azure**   
  A partire da questa versione, è necessario configurare e gestire i criteri di accesso condizionale nel [portale di Azure](https://portal.azure.com) da **Azure Active Directory** > **Accesso condizionale** . Per praticità, è anche possibile accedere a queste impostazioni da Intune nel portale di Azure in **Intune** > **Accesso condizionale**.
  <!-- 1737088 1634311 -->  

- **Aggiornamenti per i messaggi di posta elettronica sulla conformità**    
  Quando viene inviato un messaggio di posta elettronica per segnalare un dispositivo non conforme, vengono inclusi i dettagli sul dispositivo non conforme. 
  <!--1637547 -->  

- **Nuove funzionalità per l'azione "Risolvi" per i dispositivi Android**    
  L'app Portale aziendale per Android sta estendendo l'azione "Risolvi" di **Aggiorna impostazioni del dispositivo** in modo da risolvere i [problemi di crittografia del dispositivo](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android).
  <!--1583480-->  

- **Blocco remoto disponibile nell'app Portale aziendale per Windows 10**    
  Gli utenti possono ora bloccare i dispositivi in modalità remota dall'app Portale aziendale per Windows 10. Questa azione non viene visualizzata per il dispositivo locale in uso.
  <!--676506-->  

- **Risoluzione più semplice dei problemi di conformità per l'app Portale aziendale per Windows 10**   
  Gli utenti con dispositivi Windows possono toccare il motivo della mancata conformità nell'app Portale aziendale. Se possibile, con questa operazione passano direttamente al percorso corretto nell'app di configurazione per risolvere il problema.
  <!--676546-->    



## <a name="december-2017"></a>Dicembre 2017

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

- **Distribuzioni di applicazioni disponibili ora supportate per Android Enterprise**    
  È ora possibile distribuire le app Android Enterprise, in precedenza Android for Work, con stato **Disponibile**, oltre che **Richiesto**. Per informazioni dettagliate, vedere [Creare applicazioni Android con System Center Configuration Manager](/sccm/mdm/deploy-use/creating-android-applications).



## <a name="november-2017"></a>Novembre 2017

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

- **Protocollo di testo consentito dalle app gestite**  
  Le app gestite da Intune App SDK possono inviare messaggi SMS.
  <!-- 1414050  -->   

- **Disponibile l'app Portale aziendale per macOS**   
  Per l'app Portale aziendale Intune in macOS è disponibile un'esperienza aggiornata. L'app è ottimizzata per visualizzare al meglio tutte le informazioni e le notifiche di conformità che servono agli utenti per tutti i dispositivi registrati. Dopo la distribuzione di Portale aziendale Intune in un dispositivo, inoltre, gli aggiornamenti vengono forniti da Microsoft AutoUpdate per macOS. Per scaricare la nuova app Portale aziendale Intune per macOS, accedere al sito Web Portale aziendale Intune da un dispositivo macOS.
  <!--1541700-->   

- **Microsoft Planner fa ora parte dell'elenco di app approvate per la gestione delle app mobili (MAM)**    
  L'app Microsoft Planner per iOS e Android fa ora parte delle app approvate per la gestione delle app mobili (MAM). Configurare l'app da Protezione app di Intune nel portale di Azure in tutti i tenant. Per informazioni dettagliate, vedere [elenco MAM di app approvate](https://www.microsoft.com/cloud-platform/microsoft-intune-apps).
  <!-- 1248473 -->    

- **Accesso ai log delle app gestite per iOS**    
  Gli utenti finali con Managed Browser installato possono ora visualizzare lo stato della gestione di tutte le app Microsoft pubblicate e inviare i log per la risoluzione dei problemi delle app iOS gestite.
  <!-- 1469920 -->    

  Per informazioni su come abilitare la modalità di risoluzione dei problemi in Managed Browser in un dispositivo iOS, vedere [How to access to managed app logs using the Managed Browser on iOS](https://docs.microsoft.com/intune/app-configuration-managed-browser#how-to-access-to-managed-app-logs-using-the-managed-browser-on-ios) (Come accedere ai log di app gestite tramite Managed Browser in iOS).

- **Miglioramenti al flusso di lavoro di configurazione dei dispositivi in Portale aziendale per iOS nella versione 2.9.0**    
  È stato migliorato il flusso di lavoro di configurazione dei dispositivi nell'app Portale aziendale per iOS. Il linguaggio è più semplice e sono state inserite schermate dove possibile. Il linguaggio è stato inoltre reso più specifico per ogni azienda, usandone il nome in tutto il testo del programma di installazione. È possibile visualizzare il flusso di lavoro aggiornato nella pagina delle [novità dell'interfaccia utente dell'app](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-november-13-2017).

- **Richiesta di commenti e suggerimenti per l'app Portale aziendale per Android**    
  L'app Portale aziendale per Android ora richiede commenti e suggerimenti degli utenti finali. I commenti vengono inviati direttamente a Microsoft e offrono agli utenti finali la possibilità di valutare l'app nel Google Play Store pubblico. Non è obbligatorio inviare commenti e suggerimenti e la richiesta può essere facilmente ignorata in modo che gli utenti possano continuare a usare l'app. 
  <!--1165249-->    

- **Informazioni per gli utenti finali sul tipo di informazioni sui dispositivi che possono essere visualizzate per Windows 10**    
  L'informazione **Tipo di proprietà** è stata aggiunta alla schermata Dettagli dispositivo nell'app Portale aziendale per Windows 10. In questo modo, gli utenti possono ottenere maggiori informazioni sulla privacy direttamente dai documenti per gli utenti finali di Intune. È inoltre possibile accedere a queste informazioni nella schermata **Informazioni su**.
  <!--1337920-->    

- **Nuova azione "Risolvi" disponibile per i dispositivi Android**    
  L'app Portale aziendale per Android introduce un'azione "Risolvi" nella pagina _Aggiorna impostazioni del dispositivo_. Selezionando questa opzione, l'utente finale viene indirizzato direttamente all'impostazione che causa la non conformità del dispositivo. L'app Portale aziendale per Android supporta attualmente questa azione per le impostazioni [passcode del dispositivo](https://docs.microsoft.com/intune-user-help/set-your-pin-or-password-android), [crittografia del dispositivo](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android), [debug USB](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-usb-debugging-android) e [Origini sconosciute](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-unknown-sources-android). 
  <!--1583480-->    


### <a name="new-in-configuration-manager-current-branch"></a>Novità di Configuration Manager (Current Branch)

- **Azioni per la mancata conformità**    
  Ora è possibile configurare una sequenza in ordine temporale delle azioni applicate ai dispositivi che non soddisfano la conformità. Ad esempio, è possibile segnalare agli utenti i dispositivi non conformi inviando notifiche via posta elettronica o contrassegnando tali dispositivi come non conformi. Per informazioni dettagliate, vedere [Configurare azioni per la mancata conformità](/sccm/mdm/deploy-use/actions-for-noncompliance).
  <!--1321366 -->  

- **Nuove impostazioni dei criteri di gestione delle applicazioni mobili**     
  Sono state aggiunte le impostazioni seguenti relative ai criteri di gestione delle applicazioni per dispositivi mobili:
  - **Disabilita la sincronizzazione dei contatti**: impedisce all'app di salvare i dati nell'app dei contatti nativa del dispositivo.
  - **Disabilita stampa**: impedisce all'app di stampare dati aziendali o dell'istituto di istruzione.
  <!-- 1324760 -->    

  Vedere [Proteggere le app usando i criteri di gestione delle applicazioni mobili in System Center Configuration Manager](/sccm/mdm/deploy-use/protect-apps-using-mam-policies) per provare le nuove impostazioni dei criteri di protezione dell'app.

- **Supporto per dispositivi ARM64 Windows 10**     
  Nei dispositivi ARM64 che eseguono Windows 10 è supportata la gestione ibrida dei dispositivi mobili quando questi dispositivi sono disponibili. Per informazioni dettagliate, vedere [Supporto per dispositivi ARM64 Windows 10](/sccm/core/plan-design/changes/whats-new-in-version-1710#windows-10-arm64-device-support).
  <!-- 1355000 -->    

- **Esperienza del profilo VPN migliorata nella console di Configuration Manager**     
  In questa versione sono state aggiornate la procedura guidata di creazione del profilo VPN e le pagine delle proprietà per visualizzare le impostazioni appropriate per la piattaforma selezionata. Questa funzionalità era in precedenza disponibile in Configuration Manager Technical Preview 1709. Ora è disponibile nelle distribuzioni ibride con Intune e Configuration Manager (Current Branch) versione 1710. Per altre informazioni, vedere [Esperienza del profilo VPN migliorata nella console di Configuration Manager](/sccm/core/plan-design/changes/whats-new-in-version-1710#improved-vpn-profile-experience-in-configuration-manager-console).
  <!-- 1318232 -->  


### <a name="new-in-configuration-manger-technical-preview-1711"></a>Novità di Configuration Manager Technical Preview 1711

- **Nuove opzioni per i criteri di conformità per Windows 10**   
  È ora possibile configurare nuove opzioni per i criteri di conformità per i dispositivi Windows 10. Le nuove impostazioni includono criteri per firewall, controllo dell'account utente, Windows Defender Antivirus e controllo delle versioni delle build del sistema operativo. Per altri dettagli, vedere [Nuovi criteri di conformità per Windows 10](/sccm/core/get-started/capabilities-in-technical-preview-1711#new-compliance-policy-options-for-windows-10).



## <a name="october-2017"></a>Ottobre 2017

### <a name="new-in-configuration-manager-technical-preview-1709"></a>Novità di Configuration Manager Technical Preview 1709

- **Esperienza del profilo VPN migliorata nella console di Configuration Manager**      
  Le impostazioni del profilo VPN vengono ora filtrate in base alla piattaforma. Quando si creano nuovi profili VPN, ogni piattaforma supportata contiene solo le impostazioni appropriate per la piattaforma stessa. La nuova funzionalità non influisce sui profili VPN esistenti. Altre informazioni su questa modifica sono disponibili [qui](/sccm/core/get-started/capabilities-in-technical-preview-1709#improved-vpn-profile-experience-in-configuration-manager-console).
  <!-- 1313282 -->  


### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune  

- **Istruzioni per gli utenti nell'app Portale aziendale per Android**     
  L'app Portale aziendale per Android include ora istruzioni indirizzate agli utenti per agevolare la comprensione e, se possibile, la risoluzione dei problemi nei nuovi casi d'uso.
    - Nel caso abbiano raggiunto il numero massimo di dispositivi che sono autorizzati ad aggiungere, gli utenti vengono indirizzati al [portale di Azure Active Directory](https://account.activedirectory.windowsazure.com/r/#/profile) per rimuovere un dispositivo.
    - Agli utenti finali verranno indicati i passaggi da eseguire per [correggere gli errori di attivazione sui dispositivi Samsung Knox](https://go.microsoft.com/fwlink/?linkid=859718) o per [disattivare la modalità di risparmio energia](https://docs.microsoft.com/intune-user-help/power-saving-mode-android). Se nessuna di queste soluzioni risolve il problema, viene indicato come [inviare log a Microsoft](https://docs.microsoft.com/intune-user-help/send-logs-to-microsoft-android).
  <!-- 1573324, 1573150, 1558616, 1564878 -->      

- **Indicatore dello stato di avanzamento della configurazione del dispositivo nel portale aziendale Android**    
  L'app Portale aziendale per Android visualizza un indicatore dello stato di avanzamento della configurazione del dispositivo quando un utente registra il proprio dispositivo. L'indicatore segnala i nuovi stati, a partire da "Configurazione del dispositivo...", quindi "Registrazione del dispositivo...", "Completamento della registrazione del dispositivo..." e infine "Completamento della configurazione del dispositivo...".  
  <!--1565657-->    

- **Supporto dell'autenticazione basata su certificati nel portale aziendale per iOS**    
  È stato aggiunto il supporto per l'autenticazione basata su certificati (CBA) nell'app Portale aziendale per iOS. Gli utenti con autenticazione basata su certificati immettono il nome utente e quindi toccano il collegamento "Sign in with a certificate" (Accedi con un certificato). L'autenticazione basata su certificati è già supportata nelle app Portale aziendale per Android e Windows. Per altre informazioni, vedere la pagina [Accedere all'app Portale aziendale](https://docs.microsoft.com/intune-user-help/sign-in-to-the-company-portal).
  <!--1029830-->   

- **Miglioramenti al flusso di lavoro di configurazione dei dispositivi in Portale aziendale**     
  È stato migliorato il flusso di lavoro di configurazione dei dispositivi nell'app Portale aziendale per Android. Il linguaggio è più semplice e specifico della società e sono state inserite schermate dove possibile. È possibile visualizzare questi miglioramenti nella pagina delle [novità dell'interfaccia utente dell'app](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-october-2-2017).
  <!--1490692-->     

- **Materiale sussidiario migliorato sulla richiesta di accesso ai contatti per i dispositivi Android**     
  L'app Portale aziendale per Android chiede spesso all'utente l'autorizzazione all'accesso ai contatti. Se un utente finale rifiuta l'accesso, viene visualizzata una notifica in-app che richiede tale autorizzazione per l'accesso condizionale. 
  <!--1484985-->     

- **Correzione dell'avvio protetto per Android**     
  Gli utenti con dispositivi Android possono toccare il motivo della mancata conformità nell'app Portale aziendale. Quando possibile, questa operazione passano direttamente al percorso corretto nell'app impostazioni per risolvere il problema. 
  <!--1490712-->    

- **Notifiche push aggiuntive per gli utenti finali dell'app Portale aziendale per Android Oreo**    
  Vengono visualizzate ulteriori notifiche per gli utenti finali per indicare quando l'app Portale aziendale per Android Oreo sta eseguendo attività in background, ad esempio quando sta recuperando criteri dal servizio Intune. Le notifiche aumentano la trasparenza per gli utenti finali, che sapranno quando sono in corso attività amministrative nell'app Portale aziendale nei loro dispositivi, Questo miglioramento rientra nell'ambito della complessiva [ottimizzazione dell'interfaccia utente portale società](https://blogs.technet.microsoft.com/intunesupport/2017/08/21/android-8-0-o-behaviour-changes-and-microsoft-intune) per l'app portale aziendale per Android Oreo. 
  <!--1475932 -->     

- **Nuovi comportamenti dell'app Portale aziendale per Android con i profili di lavoro**     
  Quando si registra un dispositivo Android for Work con un profilo di lavoro, è l'app Portale aziendale nel profilo di lavoro che esegue le attività di gestione per il dispositivo. 

  A meno che nel profilo personale non venga usata un'app abilitata per la gestione di applicazioni mobili, l'app Portale aziendale per Android non ha più alcuna funzione. Per migliorare l'esperienza dei profili di lavoro, Intune nasconde automaticamente l'app Portale aziendale personale dopo la registrazione di un profilo di lavoro.

  L'app Portale aziendale per Android può essere abilitata in qualsiasi momento nel profilo personale. A tale scopo, cercare [Portale aziendale in Play Store](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) e toccare **Abilita**.
  <!--1485783-->    

- **Passaggio dell'app Portale aziendale per Windows 8.1 e Windows Phone 8.1 alla modalità di solo supporto**    
  È stato aggiunto un avviso per annunciare che le app Portale aziendale per Windows 8.1 e Windows Phone 8.1 sono in fase di passaggio alla modalità di solo supporto. Per informazioni, vedere [Notifiche](#notices).  
  <!--1428681-->    

- **Blocco della registrazione di dispositivi Samsung Knox non supportati**   
  L'app Portale aziendale tenta di registrare solo i dispositivi Samsung Knox supportati. Per evitare errori di attivazione KNOX che impediscono la registrazione MDM, la registrazione del dispositivo viene tentata solo se il dispositivo è presente nell'[elenco dei dispositivi pubblicato da Samsung](https://www.samsungknox.com/knox-supported-devices/knox-workspace). Alcuni numeri di modello di dispositivi Samsung supportano KNOX, mentre altri non lo supportano. Verificare la compatibilità Knox presso il rivenditore del dispositivo prima dell'acquisto e della distribuzione. È possibile trovare l'elenco completo dei dispositivi verificati nelle [impostazioni dei criteri Android e Samsung KNOX Standard](https://docs.microsoft.com/intune-classic/deploy-use/android-policy-settings-in-microsoft-intune#supported-samsung-knox-standard-devices).
  <!-- 1490695 -->     

- **Fine del supporto per Android 4.3 e versioni precedenti**     
  È stata aggiunta la comunicazione della fine del supporto per Android 4.3 e versioni precedenti. Per informazioni, vedere [Notifiche](#notices).
  <!--1171126, 1326920 -->     

- **Informazioni per gli utenti finali sul tipo di informazioni sui dispositivi visualizzabili nei dispositivi registrati**     
  L'informazione **Tipo di proprietà** è in corso di aggiunta nella schermata Dettagli dispositivo in tutte le app Portale aziendale. In questo modo, gli utenti possono ottenere altre informazioni sulla privacy direttamente dall'articolo [Quali sono le informazioni visibili per l'azienda quando si registra il dispositivo?](https://docs.microsoft.com/intune-user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune). Questo miglioramento verrà presto implementato in tutte le app Portale aziendale. Per iOS, questa funzionalità è stata annunciata a [settembre](https://docs.microsoft.com/intune/whats-new#week-of-september-11-2017). 
  <!--1165314-->     



## <a name="september-2017"></a>Settembre 2017

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune     

- **Azione di aggiornamento aggiunta all'app Portale aziendale per Windows 10**    
    L'app Portale aziendale per Windows 10 consente agli utenti di aggiornare i dati nell'app trascinando verso il basso per aggiornare o, nei desktop, premendo F5.
    <!-- 1132468 -->     

- **Informazioni per gli utenti finali sul tipo di informazioni sui dispositivi che possono essere visualizzate per iOS**   
    È stato aggiunto **tipo di proprietà** alla schermata Dettagli dispositivo nell'app portale aziendale per iOS. In questo modo, gli utenti possono ottenere maggiori informazioni sulla privacy direttamente dai documenti per gli utenti finali di Intune. È inoltre possibile accedere a queste informazioni nella schermata Informazioni su. 
    <!--739894-->    

- **Testo più comprensibile per l'app Portale aziendale per Android**   
    Il processo di registrazione per l'app Portale aziendale per Android è ora più semplice per gli utenti finali, grazie all'uso di un nuovo testo più comprensibile. Se si usa una documentazione personalizzata per la registrazione, aggiornarla sulla base delle nuove schermate. Alcune immagini di esempio sono disponibili nella pagina [Aggiornamenti dell'interfaccia utente per le applicazioni degli utenti finali in Intune](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-september-11-2017).
    <!---1396349-->    

- **Aggiunta dell'app Portale aziendale di Windows 10 ai criteri Consenti di Windows Information Protection**    
    L'app Portale aziendale di Windows 10 è stata aggiornata per supportare Windows Information Protection (WIP). L'app può essere aggiunta ai criteri Consenti di WIP. Con questa modifica, non è più necessario aggiungere l'app all'**elenco esenzioni**. 

    Solo un singolo elemento di configurazione WIP può essere recapitato a un dispositivo. Se due elementi di configurazione WIP sono destinati allo stesso dispositivo, non si applica nessun criterio WIP.
    <!-- 677129 -->    

- **Aggiunta della comunicazione di fine supporto per iOS 8.0**    
    È stata aggiunta la comunicazione della fine del supporto per iOS 8.0. Per informazioni, vedere [Notifiche](#notices).



## <a name="august-2017"></a>Agosto 2017

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune     

- **Nuova esperienza di accesso per gli utenti del portale aziendale Android e gli utenti di criteri di protezione delle app**    
  Gli utenti finali possono ora visualizzare le app, gestire i dispositivi e accedere a informazioni sui contatti IT tramite l'app Portale aziendale Android senza registrare i dispositivi Android personali. Inoltre, se un utente finale usa già un'app protetta dai criteri di protezione delle app di Intune e avvia l'app Portale aziendale Android, non visualizza più la richiesta di registrare il dispositivo.
  <!-- 621669 -->  



## <a name="notices"></a>Notifiche

### <a name="plan-for-change-intune-supports-macos-1012-and-higher-in-december"></a>Modifiche pianificate: Intune supporta macOS 10.12 e versioni successive nel mese di dicembre 
<!--2970975-->  

Apple ha rilasciato macOS 10.14, quindi, a partire da dicembre 2018, Intune supporterà macOS 10.12 e versioni successive. 

#### <a name="how-does-this-affect-me"></a>Quali sono le conseguenze di questa modifica?

A partire da dicembre, gli utenti con dispositivi con macOS 10.11 e versioni precedenti non potranno usare il portale aziendale per registrarsi in Intune. Per continuare a ricevere supporto e le nuove funzionalità, dovranno aggiornare il dispositivo a MacOS 10.12 o versione successiva e aggiornare l'app Portale aziendale alla versione più recente. 

MacOS 10.12 e versioni successive sono attualmente supportati in: 
- MacBook (fine 2009 o più recente)  
- iMac (fine 2009 o più recente)
- MacBook Air (fine 2010 o più recente)  
- MacBook Pro (fine 2010 o più recente)  
- Mac Mini (fine 2010 o più recente)  
- Mac Pro (fine 2010 o più recente)  

Dopo dicembre gli utenti finali che usano dispositivi diversi da quelli elencati sopra non potranno accedere alla versione più recente dell'app Portale aziendale per macOS. È possibile continuare a gestire i dispositivi registrati esistenti che eseguono versioni non supportate precedenti a macOS 10.12.

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Operazioni di preparazione alla modifica

- Richiedere agli utenti di aggiornare i dispositivi a una versione supportata del sistema operativo prima di dicembre 2018.  
- Controllare il reporting di Intune nel portale di Azure per vedere quali dispositivi o utenti possono essere interessati. Passare a **Dispositivi** > **Tutti i dispositivi** e filtrare per **sistema operativo**. È possibile aggiungere altre colonne per consentire l'identificazione degli utenti dell'organizzazione che usano dispositivi con macOS 10.11.  
- Se si usa la gestione ibrida dei dispositivi mobili, nella console di Configuration Manager passare all'area di lavoro **Asset e conformità** e selezionare il nodo **Dispositivi**. Fare clic con il pulsante destro del mouse sulle colonne per aggiungere le colonne **Sistema operativo** e **Versione client**. Quindi ordinare per versione del sistema operativo. Si noti che la gestione ibrida ora è deprecata ed è necessario passare a Intune in Azure non appena possibile. 
 
#### <a name="additional-information"></a>Informazioni aggiuntive
Per altre informazioni, vedere [Registrare il dispositivo macOS in Intune con l'app Portale aziendale](https://docs.microsoft.com/intune-user-help/enroll-your-device-in-intune-macos-cp).


### <a name="plan-for-change-use-intune-on-azure-now-for-your-mdm-management"></a>Modifiche pianificate: Usare Intune in Azure per la gestione MDM 
<!--1227338-->  
Un anno fa, Microsoft ha annunciato [versione di anteprima pubblica di Intune in Azure](https://cloudblogs.microsoft.com/enterprisemobility/2016/12/07/public-preview-of-intune-on-azure/) e seguita, sei mesi fa [disponibilità generale della nuova esperienza di amministrazione](https://cloudblogs.microsoft.com/enterprisemobility/2017/06/08/the-new-intune-and-conditional-access-admin-consoles-are-ga/) per Intune. A partire dal 31 agosto 2018, verrà disattivata la gestione dei dispositivi mobili (MDM) nella console Silverlight classica per i clienti che usano la versione autonoma di Intune. Usare invece [Intune in Azure](https://aka.ms/Intune_on_Azure) per la gestione dei dispositivi mobili. Se si usa ancora la console classica per la gestione dei dispositivi mobili, smettere di usarla e acquisire familiarità con Intune in Azure. Microsoft non prevede alcun impatto di questa modifica sull'utente finale. La gestione dei PC classica con Intune rimane in Silverlight. Per altre informazioni, vedere il [blog del team di supporto di Intune](https://aka.ms/Intune_on_Azure_mdm).


### <a name="plan-for-change-upcoming-macos-and-intune-password-enforcement-change"></a>Modifiche pianificate: MacOS imminenti e modifica di imposizione della password di Intune
<!--1873216-->  
Nella versione del servizio di settembre, i piani di Intune per l'integrazione di Apple appena rilasciato impostazione "Modifica Password al successivo Auth" per i dispositivi che eseguono macOS 10.13 versioni e versioni successive. Prima dell'introduzione di questa impostazione, i provider MDM non avevano modo di verificare che il passcode in un dispositivo fosse stato modificato per garantire la conformità. I criteri di configurazione e conformità di Intune verificavano solo che alla successiva modifica di una password nel dispositivo, questa venisse contrassegnata come conforme. Gli utenti di macOS riceveranno una richiesta di aggiornamento della password quando questa nuova funzionalità di Apple verrà integrata, anche se la password è già conforme.

#### <a name="how-does-this-change-affect-me"></a>Quali sono le conseguenze di questa modifica?
Questa modifica riguarda solo i clienti MDM autonomo o ibrido di Intune con un criterio del dispositivo macOS. Apple ha introdotto l'impostazione Change Password at New Auth (Cambia password alla nuova autenticazione). Intune ora può imporre agli utenti di aggiornare la password con una conforme quando si esegue il push dei criteri password. Se si bloccano le risorse aziendali fino a quando il dispositivo non viene contrassegnato come conforme, tenere presente che agli utenti finali potrebbe essere impedito l'accesso alle risorse aziendali, ad esempio alla posta elettronica o ai siti di SharePoint, fino a quando non reimpostano la password. In futuro, tutti gli aggiornamenti ai criteri password di configurazione e conformità imporranno agli utenti di destinazione di aggiornare le password.

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Operazioni di preparazione alla modifica
È possibile informare il supporto tecnico. Se non si vuole applicare questo criterio del dispositivo macOS, annullare l'assegnazione o eliminare i criteri esistenti di macOS. La ricerca di mercato condotta prima dell'implementazione di questa modifica ha rivelato che la maggior parte dei clienti non ne sarà interessata. Gli utenti finali in genere aggiornano la password dopo aver ricevuto una richiesta di registrazione con una password o reimpostano la password per garantire la conformità.  


### <a name="plan-for-change-intune-moving-to-support-ios-10-and-later-in-september-2018"></a>Modifiche pianificate: Intune lo spostamento per il supporto di iOS 10 e versioni successive nel mese di settembre 2018 
<!--2454656-->  

Nel mese di settembre 2018 è previsto il rilascio di iOS 12 da Apple. Poco dopo il rilascio, verrà effettuata la transizione del servizio di registrazione di Intune, dell'app Portale aziendale e di Managed Browser per il supporto di iOS 10 e versioni successive.

#### <a name="how-does-this-change-affect-me"></a>Quali sono le conseguenze di questa modifica?

Le app per dispositivi mobili di Office 365 sono supportate in iOS 10 e versioni successive, quindi è probabile che il sistema operativo o i dispositivi siano già stati aggiornati. In questo caso, questa transizione non avrà alcun impatto.

Se tuttavia si usa uno dei dispositivi inclusi nell'elenco seguente o si vuole registrare un dispositivo tra quelli elencati, questi supportano solo iOS 9 e versioni precedenti. Per continuare ad accedere al portale aziendale di Intune, è necessario aggiornare questi dispositivi entro settembre a dispositivi che supportano iOS 10 o versioni successive: 

- iPhone 4s
- iPod Touch 
- iPad 2
- iPad (terza generazione)
- iPad Mini (prima generazione)

A partire da luglio, nei dispositivi registrati in MDM con iOS 9 e il portale aziendale verrà visualizzato un messaggio di avviso per l'aggiornamento del sistema operativo o del dispositivo. Se si usano criteri di protezione delle app, è anche possibile impostare l'impostazione di accesso "Richiedi sistema operativo iOS minimo (solo avviso)".  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Operazioni di preparazione alla modifica

Verificare se nell'organizzazione sono presenti dispositivi o utenti interessati. In Intune nel portale di Azure passare a **Dispositivi** > **Tutti i dispositivi** e filtrare in base a **Sistema operativo**.  Fare clic su **Colonne** per visualizzare i dettagli, come la versione del sistema operativo. Richiedere agli utenti di aggiornare i dispositivi a una versione supportata del sistema operativo prima di settembre.


### <a name="company-portal-for-windows-81-and-windows-phone-81-moving-to-sustaining-mode"></a>Passaggio dell'app Portale aziendale per Windows 8.1 e Windows Phone 8.1 alla modalità di solo supporto 
<!--1428681-->  
*6 ottobre 2017*   
 
A partire da ottobre 2017, le app Portale aziendale per Windows 8.1 e Windows Phone 8.1 sono passate alla modalità di solo supporto. Ciò significa che le app e gli scenari esistenti, ad esempio la registrazione e la conformità, continuano a essere supportati per queste piattaforme. Queste app continuano a essere disponibili per il download tramite i canali di rilascio esistenti, ad esempio Microsoft Store. 

Nella modalità di solo supporto, queste app ricevono solo gli aggiornamenti della sicurezza critici. Non verranno rilasciati altri aggiornamenti né nuove funzionalità per queste app. Per le nuove funzionalità è consigliabile aggiornare i dispositivi a Windows 10 o a Windows 10 Mobile. 

### <a name="end-of-support-for-ios-80"></a>Fine del supporto per iOS 8.0 
<!---1164477--->  
Per accedere alle risorse aziendali, le app gestite e l'app Portale aziendale per iOS richiedono iOS 9.0 o versione successiva. I dispositivi non aggiornati prima di settembre non sono in grado di accedere al Portale aziendale o alle app gestite. 

### <a name="platform-support-reminder-windows-phone-81-mainstream-support-ended-july-11-2017"></a>Promemoria di supporto della piattaforma: Il supporto "Mainstream" di Windows Phone 8.1 è terminato 11 luglio 2017
<!-- 1327781 -->  
*11 luglio 2017*

La piattaforma Windows Phone 8.1 ha raggiunto la fine del supporto Mainstream. Ciò non influisce sul supporto di Windows 8.1 per PC.

Non ci sono conseguenze immediate sui dispositivi Windows Phone 8.1 gestiti dal servizio Intune, inclusi quelli registrati nella gestione dei dispositivi mobili ibrida. I dispositivi registrati continuano a funzionare. Tutti i criteri, le configurazioni e le app continuano a funzionare come previsto. Si noti che all'interno del servizio Intune non ci sono miglioramenti destinati alla piattaforma Windows Phone 8.1 e all'app del Portale aziendale di Windows Phone 8.1.

È consigliabile eseguire l'aggiornamento dei dispositivi Windows Phone 8.1 idonei a Windows 10 Mobile non appena possibile.  

### <a name="end-of-support-for-android-43-and-lower"></a>Fine del supporto per Android 4.3 e versioni precedenti
<!---1171127--->  
*6 luglio 2017*

Per accedere alle risorse aziendali, le app gestite e l'app Portale aziendale per Android richiedono Android 4.4 o versione successiva. I dispositivi non aggiornati prima dell'inizio di ottobre non sono in grado di accedere al Portale aziendale o alle app gestite. Entro dicembre è stato imposto il ritiro di tutti i dispositivi registrati, con conseguente perdita dell'accesso alle risorse aziendali. Se si usano criteri di protezione delle app senza MDM, le app non ricevono gli aggiornamenti e la qualità dell'esperienza diminuisce nel tempo.



## <a name="see-also"></a>Vedere anche

- [Funzionalità MDM ibride precedenti e notifiche](whats-new-hybrid-archive.md)
- [Novità di MDM in System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)

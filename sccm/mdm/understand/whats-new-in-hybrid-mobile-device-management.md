---
title: Novità nella gestione di dispositivi mobili ibrida
titleSuffix: Configuration Manager
description: Informazioni sulle nuove funzionalità di gestione dei dispositivi mobili disponibili per le distribuzioni ibride con Configuration Manager e Intune.
ms.date: 07/05/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d527d2fc4fdc52e132b6f603d9b83851e1693f3
ms.sourcegitcommit: c9d0a4c24ce90825cb2d05e4fe37c5b41fa48a50
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2018
ms.locfileid: "37923539"
---
# <a name="whats-new-in-hybrid-mobile-device-management-with-configuration-manager-and-microsoft-intune"></a>Novità della gestione ibrida di dispositivi mobili con Configuration Manager e Microsoft Intune

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



## <a name="july-2018"></a>Luglio 2018

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

#### <a name="updates-to-out-of-compliance-messages-in-company-portal-app"></a>Aggiornamenti per i messaggi di mancata conformità nell'app Portale aziendale 
<!--1832222--> È in corso la revisione dei messaggi visualizzati dagli utenti dei dispositivi quando un dispositivo risulta non conforme. I messaggi conservano il significato originale, ma vengono aggiornati con un linguaggio più descrittivo e un minor uso di terminologia tecnica. Verranno anche aggiornati i collegamenti alla documentazione e alle procedure di correzione per mantenerli aggiornati.  

L'esempio seguente di testo prima e dopo è un esempio dei miglioramenti dei messaggi che verranno introdotti:  

- Prima: *questo dispositivo non ha contattato il servizio Intune nel periodo di tempo specificato richiesto dall'amministratore IT. Per risolvere questo problema, aprire l'app Portale aziendale nel dispositivo e fare clic sul pulsante Controlla conformità.*  

- Dopo: *Il dispositivo non ha contattato ultimamente l'organizzazione. Per ristabilire una connessione, aprire l'app Portale aziendale nel dispositivo e toccare Verifica le impostazioni per il dispositivo.*  

#### <a name="select-device-categories-by-using-the-access-work-or-school-settings"></a>Selezionare le categorie di dispositivi usando le impostazioni per l'accesso all'azienda o all'istituto di istruzione 
<!--1058963--> Se è stato abilitato il [mapping del gruppo di dispositivi](https://docs.microsoft.com/intune/device-group-mapping), agli utenti in Windows 10 viene ora richiesto di selezionare una categoria di dispositivi dopo la registrazione tramite il pulsante **Connetti** in **Impostazioni**  >  **Account** > **Access work or school** (Accesso ad azienda o istituto di istruzione).  



## <a name="june-2018"></a>Giugno 2018

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

#### <a name="access-to-macos-company-portal-pre-release-build"></a>Accesso alla build in versione non definitiva di Portale aziendale macOS 
<!--1734766--> Usare Microsoft AutoUpdate per iscriversi per ricevere le build anticipatamente partecipando al programma Insider. L'iscrizione consente di usare il portale aziendale aggiornato prima che sia disponibile per gli utenti finali.

#### <a name="intune-app-protection-policies-and-microsoft-edge"></a>Criteri di protezione delle app di Intune e Microsoft Edge 
<!--1818968,1818969--> Il browser Microsoft Edge per dispositivi mobili (iOS e Android) ora supporta criteri di protezione delle app di Microsoft Intune. Gli utenti di dispositivi iOS e Android che accedono all'applicazione Edge tramite account di Azure Active Directory aziendali sono protetti da Intune. Nei dispositivi iOS, i criteri **Richiedi un browser gestito per l'apertura del collegamento** consentono agli utenti di aprire collegamenti in Edge, se quest'ultimo è gestito.



## <a name="may-2018"></a>Maggio 2018

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

#### <a name="requesting-help-in-the-company-portal-for-windows-10"></a>Richiesta di assistenza in Portale aziendale per Windows 10 
<!--1874137--> Portale aziendale per Windows 10 ora invia i log dell'app direttamente a Microsoft quando l'utente avvia il flusso di lavoro di richiesta di assistenza per risolvere un problema. Questo comportamento rende più semplice la risoluzione dei problemi segnalati a Microsoft.  


### <a name="new-in-configuration-manager-current-branch"></a>Novità di Configuration Manager (Current Branch)

#### <a name="android-for-work-and-lookout-onboarding-moved-to-intune-on-azure"></a>Android for Work e onboarding Lookout spostati in Intune in Azure
<!--2355022,2357366--> Con l'aggiornamento di Intune più recente è possibile abilitare e gestire l'integrazione di Android for Work e della protezione dalle minacce per dispositivi mobili di Lookout nei tenant di gestione di dispositivi mobili ibrida in Intune nel portale di Azure. Prima dell'aggiornamento, queste funzionalità erano configurabili solo nel portale di Intune classico (Silverlight).
 
Nota: Lookout è l'unico provider di protezione dalle minacce per dispositivi mobili (MTD, Mobile Threat Defense) supportato dalla gestione ibrida. Se in precedenza è stata eseguita l'integrazione con un altro provider MTD, quest'ultimo compare comunque in Intune nel portale di Azure. Se si elimina il connettore di questo, non è possibile aggiungerlo di nuovo.
 
Queste modifiche non influiscono sulle funzionalità esistenti. Continuare a usare la console di Configuration Manager per la gestione delle app correlate, per la creazione di report e per i criteri.
 
Per altre informazioni, vedere gli articoli seguenti:
- [Configurare la gestione di dispositivi Android ibrida](/sccm/mdm/deploy-use/enroll-hybrid-android)
- [Gestire l'accesso alle risorse aziendali in base ai rischi per dispositivi, rete e applicazioni](/sccm/mdm/deploy-use/lookout-mobile-threat-defense-in-configuration-manager)


#### <a name="support-for-new-versions-of-cisco-anyconnect-client-for-ios"></a>Supporto per nuove versioni del client Cisco AnyConnect per iOS
<!--1357393--> È possibile abilitare il supporto per Cisco AnyConnect per iOS 4.0.7 o versione successiva. In questo modo, i profili VPN Cisco AnyConnect esistenti vengono etichettati **Cisco Legacy AnyConnect** e continuano a funzionare come prima. L'opzione **Cisco AnyConnect** è per i profili VPN nuovi che possono essere usati con Cisco AnyConnect su iOS 4.0.7 o versione successiva.

  > [!Tip]  
  > Cisco AnyConnect 4.0.07x e versioni successive per iOS è una funzionalità introdotta per la prima volta nella versione 1802 come [versione non definitiva](/sccm/core/servers/manage/pre-release-features). A partire dall'[aggiornamento 4163547](https://support.microsoft.com/help/4163547) per la versione 1802, questa funzionalità non è più in versione non definitiva.  

> [!Note]  
> Continuare a usare l'opzione **Cisco AnyConnect Legacy** per i profili VPN macOS. 



## <a name="april-2018"></a>Aprile 2018

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

#### <a name="intune-adapts-to-fluent-design-system-in-the-company-portal-app-for-windows-10"></a>Intune si adatta a Fluent Design System nell'app Portale aziendale per Windows 10 
<!--1195010--> L'app Portale aziendale Intune per Windows 10 è stata aggiornata con la [visualizzazione della navigazione di Fluent Design System](/windows/uwp/design/basics/navigation-basics). A lato dell'app si noti un elenco verticale statico di tutte le pagine di primo livello. Fare clic su un collegamento per visualizzare rapidamente tutte le pagine e passare da una all'altra. Questo è il primo di molti aggiornamenti che saranno resi disponibili come parte del continuo impegno per creare un'esperienza più adattiva, empatica e familiare in Intune. Per visualizzare l'aspetto aggiornato, vedere [Novità dell'interfaccia utente dell'app](/intune/whats-new-app-ui).

#### <a name="improved-device-tiles-in-the-windows-10-company-portal"></a>Riquadri di dispositivo migliorati nel Portale aziendale di Windows 10
<!--2213364--> I riquadri sono stati aggiornati per risultare più accessibili agli utenti con ipovisione e offrire prestazioni migliori per gli strumenti per la lettura su schermo.


#### <a name="test-the-company-portal-for-macos-on-virtual-machines"></a>Testare il Portale aziendale per macOS nelle macchine virtuali
<!--2216679--> Microsoft ha pubblicato indicazioni che consentono agli amministratori IT di testare l'app Portale aziendale per macOS nelle macchine virtuali in Parallels Desktop e VMware Fusion. Per altre informazioni, vedere [Registrare le macchine virtuali macOS per i test](/intune/macos-enroll#enroll-virtual-macos-machines-for-testing).


#### <a name="send-diagnostic-reports-in-company-portal-app-for-macos"></a>Inviare i report di diagnostica nell'app Portale aziendale per macOS
<!--2216677--> L'app Portale aziendale per i dispositivi macOS è stata aggiornata per migliorare il modo in cui gli utenti segnalano gli errori relativi a Intune. Dall'app Portale aziendale gli utenti possono:

- Caricare i report di diagnostica direttamente al team di sviluppo Microsoft.
- Inviare tramite posta elettronica l'ID dell'evento imprevisto al team di supporto IT dell'azienda.


#### <a name="updated-help-experience-on-company-portal-app-for-android"></a>Esperienza Guida aggiornata per l'app Portale aziendale per Android 
<!--1631531--> È stata aggiornata l'esperienza Guida nell'app Portale aziendale per Android per la compatibilità con le procedure consigliate per la piattaforma Android. Quando gli utenti riscontrano un problema nell'app, ora possono toccare **Menu** > **Guida** e:
- Caricare i log di diagnostica in Microsoft.
- Inviare un messaggio di posta elettronica con la descrizione del problema e l'ID evento imprevisto a un addetto del supporto aziendale.


#### <a name="update-where-to-configure-your-app-protection-policies"></a>Aggiornare la posizione in cui configurare i criteri di protezione dell'app 
<!--2144597--> Nel portale di Azure, nell'ambito del servizio Microsoft Intune, si verrà temporaneamente reindirizzati dal pannello del servizio **Protezione app di Intune** al pannello **App per dispositivi mobili**. Si noti che tutti i criteri di protezione delle app sono già nel pannello **App per dispositivi mobili** in Intune sotto la configurazione delle app. Invece di andare a Protezione app di Intune, si passerà a Intune. Ad aprile 2018 il reindirizzamento verrà arrestato e il pannello del servizio **Protezione app di Intune** verrà completamente rimosso. All'interno di Intune sarà quindi disponibile una sola posizione per i criteri di protezione delle app. 

**Quali sono le conseguenze di questa modifica?** Questa modifica avrà effetto sia sui clienti di Intune autonomi che sui clienti ibridi (Intune con Configuration Manager). Questa integrazione consentirà di semplificare l'amministrazione della gestione del cloud.

**Operazioni di preparazione alla modifica** Contrassegnare **Intune** come preferito invece del pannello del servizio **Protezione app di Intune** e assicurarsi di avere familiarità con il flusso di lavoro dei criteri di protezione delle app nel pannello del servizio **Dispositivi mobili** in Intune. Per un breve periodo di tempo verrà effettuato il reindirizzamento e quindi il pannello **Protezione app** verrà rimosso. Tenere presente che tutti i criteri di protezione delle app sono già in Intune ed è possibile modificare qualsiasi criterio di accesso condizionale. Per altre informazioni sulla modifica dei criteri di accesso condizionale, vedere [Accesso condizionale in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). Per altre informazioni, vedere [Che cosa sono i criteri di protezione delle app?](/intune/app-protection-policy) 




#### <a name="user-experience-update-for-the-company-portal-app-for-ios"></a>Aggiornamento dell'esperienza utente per l'app Portale aziendale per iOS 
<!--1412866--> È stato rilasciato un aggiornamento dell'esperienza utente principale per l'app Portale aziendale per iOS. L'aggiornamento include una riprogettazione visuale completa con un aspetto modernizzato. La funzionalità dell'app è stata mantenuta, ma migliorandone il livello di usabilità e accessibilità.  

L'aggiornamento include anche:
- Supporto per iPhone X.
- Tempi di risposta più rapidi per l'avvio e il caricamento dell'app, per consentire agli utenti di risparmiare tempo.
- Indicatori di stato aggiuntivi per offrire agli utenti informazioni sullo stato più aggiornate.
- Miglioramenti della modalità di caricamento dei log, in modo che sia possibile segnalare eventuali problemi.  

Per visualizzare l'aspetto aggiornato, vedere le [novità dell'interfaccia utente dell'app](/intune/whats-new-app-ui).



## <a name="march-2018"></a>Marzo 2018

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

#### <a name="windows-company-portal-send-feedback-option-may-no-longer-work"></a>L'opzione Invia commenti e suggerimenti del Portale aziendale di Windows potrebbe non funzionare più
<!--2070166--> L'app Portale aziendale di Windows include l'opzione "Invia commenti e suggerimenti" che consente agli utenti di inviare a Microsoft commenti e suggerimenti sull'app. Dal 30 aprile 2018, questa opzione continua a essere supportata solo nell'app Portale aziendale di Windows 10 in esecuzione in Windows 10 versione 1607 e successive.   

**Quali sono le conseguenze di questa modifica?**

Se l'app Portale aziendale di Windows non è installata per gli utenti finali, ignorare questo messaggio.

Se gli utenti finali usano l'app Portale aziendale, si noti che a partire dal 30 aprile il pulsante "Invia commenti e suggerimenti" non funzionerà più per l'app negli scenari seguenti:  

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
<!-- 710595 --> Tramite Azure Active Directory (Azure AD) è ora possibile limitare l'accesso ai siti Web nei dispositivi mobili all'app Intune Managed Browser. Nel browser gestito i dati del sito Web rimarranno protetti e separati dai dati personali dell'utente finale. Managed Browser supporta inoltre le funzionalità Single Sign-On per i siti protetti da Azure AD. L'accesso a Managed Browser o l'uso di Managed Browser in un dispositivo con un'altra app gestita da Intune consente a Managed Browser di accedere ai siti aziendali protetti da Azure AD senza che l'utente debba immettere le proprie credenziali. Questa funzionalità si applica a siti quali Outlook Web Access (OWA) e SharePoint Online, nonché ad altri siti aziendali, ad esempio le risorse Intranet a cui si accede tramite il proxy app di Azure.



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
  A partire da questa versione, è necessario configurare e gestire i criteri di accesso condizionale nel [portale di Azure](https://portal.azure.com) da **Azure Active Directory** > **Accesso condizionale** . Per praticità, è anche possibile accedere a questo pannello da Intune nel portale di Azure in **Intune** > **Accesso condizionale**.
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
  Le app gestite da Intune App SDK sono in grado di inviare messaggi SMS.
  <!-- 1414050  -->   

- **Disponibile l'app Portale aziendale per macOS**   
  Per l'app Portale aziendale Intune in macOS è disponibile un'esperienza aggiornata. L'app è ottimizzata per visualizzare al meglio tutte le informazioni e le notifiche di conformità che servono agli utenti per tutti i dispositivi registrati. Dopo la distribuzione di Portale aziendale Intune in un dispositivo, inoltre, gli aggiornamenti vengono forniti da Microsoft AutoUpdate per macOS. Per scaricare la nuova app Portale aziendale Intune per macOS, accedere al sito Web Portale aziendale Intune da un dispositivo macOS.
  <!--1541700-->   

- **Microsoft Planner fa ora parte dell'elenco di app approvate per la gestione delle app mobili (MAM)**    
  L'app Microsoft Planner per iOS e Android fa ora parte delle app approvate per la gestione delle app mobili (MAM). Configurare l'app tramite il pannello Protezione app di Intune nel portale di Azure in tutti i tenant. Per informazioni dettagliate, vedere [elenco MAM di app approvate](https://www.microsoft.com/cloud-platform/microsoft-intune-apps).
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
  È stato aggiunto il supporto per l'autenticazione basata su certificati (CBA) nell'app Portale aziendale per iOS. Gli utenti con autenticazione basata su certificati immettono il nome utente e quindi toccano il collegamento "Sign in with a certificate" (Accedi con un certificato). L'autenticazione basata su certificati è già supportata nelle app Portale aziendale per Android e Windows. Per altre informazioni, vedere la pagina sull'[accesso all'app Portale aziendale](https://docs.microsoft.com/intune-user-help/sign-in-to-the-company-portal) pagina.
  <!--1029830-->   

- **Miglioramenti al flusso di lavoro di configurazione dei dispositivi in Portale aziendale**     
  È stato migliorato il flusso di lavoro di configurazione dei dispositivi nell'app Portale aziendale per Android. Il linguaggio è più semplice e specifico della società e sono state inserite schermate dove possibile. È possibile visualizzare questi miglioramenti nella pagina delle [novità dell'interfaccia utente dell'app](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-october-2-2017).
  <!--1490692-->     

- **Materiale sussidiario migliorato sulla richiesta di accesso ai contatti per i dispositivi Android**     
  L'app Portale aziendale per Android chiede spesso all'utente l'autorizzazione all'accesso ai contatti. Se l'utente finale rifiuta l'accesso, viene visualizzata una notifica in-app che richiede tale autorizzazione per l'accesso condizionale. 
  <!--1484985-->     

- **Correzione dell'avvio protetto per Android**     
  Gli utenti con dispositivi Android possono toccare il motivo della mancata conformità nell'app Portale aziendale. Se possibile, con questa operazione passano direttamente al percorso corretto nell'app di configurazione per risolvere il problema. 
  <!--1490712-->    

- **Notifiche push aggiuntive per gli utenti finali dell'app Portale aziendale per Android Oreo**    
  Vengono visualizzate ulteriori notifiche per gli utenti finali per indicare quando l'app Portale aziendale per Android Oreo sta eseguendo attività in background, ad esempio quando sta recuperando criteri dal servizio Intune. Le notifiche aumentano la trasparenza per gli utenti finali, che sapranno quando sono in corso attività amministrative nell'app Portale aziendale nei loro dispositivi, Questo miglioramento rientra nell'ambito della complessiva [ottimizzazione dell'interfaccia utente del portale aziendale](https://blogs.technet.microsoft.com/intunesupport/2017/08/21/android-8-0-o-behaviour-changes-and-microsoft-intune) per l'app Portale aziendale per Android Oreo. 
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
  L'app Portale aziendale tenta di registrare solo i dispositivi Samsung Knox supportati. Per evitare errori di attivazione KNOX che impediscono la registrazione MDM, la registrazione del dispositivo viene tentata solo se il dispositivo è presente nell'[elenco dei dispositivi pubblicato da Samsung](https://www.samsungknox.com/knox-supported-devices/knox-workspace). Alcuni numeri di modello di dispositivi Samsung supportano KNOX, mentre altri non lo supportano. Verificare la compatibilità Knox presso il rivenditore del dispositivo prima dell'acquisto e della distribuzione. È possibile trovare l'elenco completo dei dispositivi verificati nelle [impostazioni dei criteri Android e Samsung KNOX Standard](https://docs.microsoft.com/intune-classic/deploy-use/android-policy-settings-in-microsoft-intune#supported-samsung-knox-standard-devices).
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
    L'informazione **Tipo di proprietà** è stata aggiunta alla schermata Dettagli dispositivo nell'app Portale aziendale per iOS. In questo modo, gli utenti possono ottenere maggiori informazioni sulla privacy direttamente dai documenti per gli utenti finali di Intune. È inoltre possibile accedere a queste informazioni nella schermata Informazioni su. 
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



## <a name="july-2017"></a>Luglio 2017

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

- **Aggiunta di comunicazioni di fine supporto per Android e Windows Phone**    
    Sono state aggiunte nuove comunicazioni relative alla fine del supporto per alcune versioni di Android e di Windows Phone. Per informazioni, vedere [Notifiche](#notices).


### <a name="new-in-configuration-manager-current-branch"></a>Novità di Configuration Manager (Current Branch)

Le funzionalità seguenti erano precedentemente disponibili nelle versioni di Configuration Manager Technical Preview. Ora sono disponibili nelle distribuzioni ibride con Intune e Configuration Manager (Current Branch) versione 1706.

- [Supporto di Entrust per le autorità di certificazione Entrust](/sccm/core/get-started/capabilities-in-technical-preview-1706#support-for-entrust-certification-authorities)
- [Nuove impostazioni dei criteri di gestione delle applicazioni mobili](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-mobile-application-management-policy-settings)
- [Aggiornamenti della configurazione della condivisione di Android for Work](/sccm/core/plan-design/changes/whats-new-in-version-1706#updates-to-android-for-work-sharing-configuration)
- [Nuove regole per i criteri di conformità dei dispositivi](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-device-compliance-policy-rules)
- [Nuove impostazioni di configurazione per dispositivi Windows 10 non gestiti con il client di Configuration Manager](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client)
- [Supporto Cisco (IPsec) per i profili VPN di MacOS](/sccm/core/get-started/capabilities-in-technical-preview-1706#cisco-ipsec-support-for-macos-vpn-profiles)
- [Restrizioni di registrazione per Android e iOS](/sccm/core/plan-design/changes/whats-new-in-version-1706#android-and-ios-enrollment-restrictions) 



## <a name="june-2017"></a>Giugno 2017

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

- **Cambiare l'autorità MDM**    
  A partire dalla versione 1610 di Configuration Manager, è possibile cambiare l'autorità MDM senza bisogno di contattare il supporto tecnico Microsoft. Inoltre, non è necessario annullare e ripetere la registrazione dei dispositivi gestiti esistenti. Per altre informazioni, vedere [Cambiare l'autorità MDM](/sccm/mdm/deploy-use/change-mdm-authority).

- **Integrazione di Managed Browser e del proxy di applicazione**    
  Intune Managed Browser può ora integrarsi con il servizio proxy di applicazione di Azure AD per consentire agli utenti di accedere ai siti Web interni, anche quando lavorano in remoto. Gli utenti del browser immettono l'URL del sito nel modo usuale e Managed Browser indirizza la richiesta tramite il gateway Web del proxy di applicazione. Per altre informazioni, vedere [Gestire un accesso Internet tramite i criteri di Managed Browser](https://docs.microsoft.com/intune/app-configuration-managed-browser).

- **L'app Portale aziendale per Android offre ora all'utente finale una nuova esperienza dei criteri di protezione delle app**  
  In base ai suggerimenti dei clienti, l'app Portale aziendale per Android è stata modificata in modo da includere un pulsante **Accesso al contenuto aziendale**. Lo scopo è impedire che gli utenti finali eseguano inutilmente il processo di registrazione quando hanno solo necessità di accedere alle app che supportano i criteri di protezione delle app, una funzionalità di gestione delle applicazioni mobili di Intune. È possibile visualizzare queste modifiche nella pagina delle [novità dell'interfaccia utente dell'app](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Nuova azione di menu per rimuovere facilmente Portale aziendale**  
  In base ai suggerimenti degli utenti, nell'app Portale aziendale per Android è stata aggiunta a una nuova azione di menu per avviare la rimozione di Portale aziendale dal dispositivo. Questa azione rimuove il dispositivo dalla gestione di Intune in modo che l'utente possa rimuovere l'app dal dispositivo. È possibile visualizzare queste modifiche nella pagina [Novità dell'interfaccia utente dell'app](https://docs.microsoft.com/intune/whats-new-app-ui) e nella [documentazione di Android per l'utente finale](https://docs.microsoft.com/intune-user-help/unenroll-your-device-from-intune-android).

- **Miglioramenti alla sincronizzazione delle app con Windows 10 Creators Update**  
  L'app Portale aziendale per Windows 10 a questo punto avvia automaticamente una sincronizzazione per le richieste di installazione di app per i dispositivi con Windows 10 Creators Update (versione 1703). Questo comportamento riduce il problema del blocco dell'installazione di app durante lo stato "In attesa di sincronizzazione". Gli utenti sono anche in grado di avviare manualmente la sincronizzazione all'interno dell'app. È possibile visualizzare queste modifiche nella pagina delle [novità dell'interfaccia utente dell'app](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Nuova esperienza interattiva per Portale aziendale di Windows 10**  
  L'app Portale aziendale per Windows 10 include un'esperienza guidata per Intune per i dispositivi che non sono stati identificati o registrati. La nuova esperienza fornisce istruzioni dettagliate che guidano l'utente nella fase di registrazione in Azure Active Directory (obbligatoria per le funzionalità di accesso condizionale) e la registrazione in MDM (obbligatoria per le funzionalità di gestione dei dispositivi). L'esperienza interattiva è accessibile dalla home page di Portale aziendale. Se gli utenti non completano la registrazione, possono continuare a usare l'app, ma le funzionalità saranno limitate.

  Questo aggiornamento è disponibile solo nei dispositivi che eseguono l'Aggiornamento dell'anniversario di Windows 10 (build 1607) o versione successiva. È possibile visualizzare queste modifiche nella pagina delle [novità dell'interfaccia utente dell'app](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Miglioramenti ai riquadri dell'app nell'app Portale aziendale per iOS**  
  La progettazione dei riquadri dell'app nella home page è stata aggiornata in modo da riflettere il colore della personalizzazione impostato per il Portale aziendale. Per altre informazioni, vedere la pagina delle [novità dell'interfaccia utente dell'app](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Selezione account ora disponibile per l'app Portale aziendale per iOS**  
  Se gli utenti di dispositivi iOS usano il proprio account aziendale o dell'istituto di istruzione per accedere alle altre app Microsoft, possono visualizzare la nuova selezione account quando effettuano l'accesso a Portale aziendale. Per altre informazioni, vedere la pagina delle [novità dell'interfaccia utente dell'app](https://docs.microsoft.com/intune/whats-new-app-ui).

### <a name="new-in-configuration-manager-technical-preview-1706"></a>Novità di Configuration Manager Technical Preview 1706

- **Nuove impostazioni degli elementi di configurazione di Windows**      
  Nuovi elementi di configurazione di Windows sono disponibili per le categorie di impostazioni relative a password, dispositivi, archivi e Microsoft Edge. Per altre informazioni, vedere [Nuove attività degli elementi di configurazione di Windows](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-windows-configuration-item-settings).
  <!-- 1354715 -->

- **Nuove regole per i criteri di conformità dei dispositivi**   
  È ora possibile configurare nuove opzioni per i criteri di conformità che in precedenza erano disponibili solo nella versione autonoma di Intune. Per i dettagli, vedere [Miglioramenti dei criteri di conformità dei dispositivi](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-device-compliance-policy-rules).

- **Restrizioni di registrazione per Android e iOS**       
  Gli amministratori possono ora specificare che gli utenti non possono registrare dispositivi Android o iOS personali nel proprio ambiente ibrido. Questa azione consente di limitare i dispositivi registrati ai dispositivi pre-dichiarati, ai dispositivi di proprietà dell'azienda o ai dispositivi iOS registrati solo tramite Device Enrollment Program. Per i dettagli vedere [Restrizioni di registrazione di Android e iOS](/sccm/core/get-started/capabilities-in-technical-preview-1706#android-and-ios-enrollment-restrictions).
  <!-- 1290826 -->

- **Supporto per le autorità di certificazione Entrust**      
  Configuration Manager ora supporta l'autorità di certificazione Entrust. Questo supporto consente il recapito dei certificati PFX ai dispositivi registrati in Microsoft Intune.    
  <!-- 1350740 -->

  Quando si aggiunge un ruolo di punto di registrazione certificato in Configuration Manager, è possibile configurare Entrust come autorità di certificazione. Quando si aggiunge un nuovo profilo di certificato che emette i certificati PFX, è possibile selezionare l'autorità di certificazione Microsoft o Entrust.

  **Problema noto**: nella Technical Preview 1706, i certificati PFX non vengono emessi per le autorità di certificazione di Microsoft. Questo problema non influenza i certificati PFX importati o i profili SCEP.

- **Supporto Cisco (IPsec) per i profili VPN di MacOS**      
  È possibile creare un profilo VPN di MacOS con Cisco (IPsec) come tipo di connessione. Per altre informazioni, vedere [Creare profili VPN](/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles).
  <!-- 1321367 -->


## <a name="notices"></a>Notifiche

### <a name="plan-for-change-intune-moving-to-support-ios-10-and-later-in-september-2018"></a>Modifiche pianificate: Intune supporterà iOS 10 e versioni successive a settembre 2018 
<!--2454656-->

Nel mese di settembre 2018 è previsto il rilascio di iOS 12 da Apple. Poco dopo il rilascio, verrà effettuata la transizione del servizio di registrazione di Intune, dell'app Portale aziendale e di Managed Browser per il supporto di iOS 10 e versioni successive.

#### <a name="how-does-this-affect-me"></a>Quali sono le conseguenze di questa modifica?

Le app per dispositivi mobili di Office 365 sono supportate in iOS 10 e versioni successive, quindi è probabile che il sistema operativo o i dispositivi siano già stati aggiornati. In questo caso, questa transizione non avrà alcun impatto.

Tuttavia, con i dispositivi inclusi nell'elenco seguente o se si vuole registrare un dispositivo tra quelli elencati, tenere presente che questi supportano solo iOS 9 e versioni precedenti. Per continuare ad accedere al portale aziendale di Intune, è necessario aggiornare questi dispositivi entro settembre a dispositivi che supportano iOS 10 o versioni successive: 

- iPhone 4s
- iPod Touch 
- iPad 2
- iPad (terza generazione)
- iPad Mini (prima generazione)

A partire da luglio, nei dispositivi registrati in MDM con iOS 9 e il portale aziendale verrà visualizzato un messaggio di avviso per l'aggiornamento del sistema operativo o del dispositivo. Se si usano criteri di protezione delle app, è anche possibile impostare l'impostazione di accesso "Richiedi sistema operativo iOS minimo (solo avviso)".  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Operazioni di preparazione alla modifica

Verificare se nell'organizzazione sono presenti dispositivi o utenti interessati. In Intune nel portale di Azure passare a **Dispositivi** > **Tutti i dispositivi** e filtrare in base a **Sistema operativo**.  Fare clic su **Colonne** per visualizzare i dettagli, come la versione del sistema operativo. Richiedere agli utenti di aggiornare i dispositivi a una versione supportata del sistema operativo prima di settembre.


### <a name="plan-for-change-intune-moving-to-tls-12"></a>Modifiche pianificate: Transizione di Intune a TLS 1.2

A partire dal 31 ottobre 2018, Intune supporterà il protocollo Transport Layer Security (TLS) versione 1.2 per fornire la crittografia migliore, per assicurarsi che il servizio sia più sicuro per impostazione predefinita e per allinearsi ad altri servizi Microsoft, come Microsoft Office 365. Office ha comunicato questa modifica in MC128929.

#### <a name="how-does-this-affect-me"></a>Quali sono le conseguenze di questa modifica?

A partire dal 31 ottobre 2018, Intune non supporterà più le versioni del protocollo TLS 1.0 o 1.1. Tutte le combinazioni di client-server e browser-server devono usare TLS versione 1.2 per garantire una connessione senza problemi a Intune. Si noti che questa modifica influirà sui dispositivi degli utenti finali che non sono più supportati da Intune, ma che ricevono ancora criteri tramite Intune, e che non possono usare TLS versione 1.2. Sono inclusi i dispositivi come quelli che eseguono Android 4.3 e versioni precedenti. Per un elenco di dispositivi e browser interessati, vedere le informazioni aggiuntive più avanti.

Dopo il 31 ottobre 2018, se si riscontra un problema relativo all'uso di una versione di TLS precedente, sarà necessario eseguire l'aggiornamento a TLS 1.2 o a un dispositivo che supporti TLS 1.2 come parte della risoluzione.

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Operazioni di preparazione alla modifica

È consigliabile rimuovere in modo proattivo le dipendenze da TLS 1.0 e 1.1 negli ambienti e disabilitare TLS 1.0 e 1.1 a livello del sistema operativo, laddove possibile. Iniziare quanto prima a pianificare la migrazione a TLS 1.2. Controllare il post del blog del supporto tecnico di seguito per l'elenco dei dispositivi che non sono attualmente supportati da Intune, ma che possono comunque ancora ricevere criteri e che non saranno in grado di comunicare tramite TLS versione 1.2. Potrebbe essere necessario informare gli utenti finali che perderanno l'accesso alle risorse aziendali.

Per altre informazioni, vedere [Intune moving to TLS 1.2 for encryption](https://blogs.technet.microsoft.com/intunesupport/2018/06/05/intune-moving-to-tls-1-2-for-encryption/) (Transizione di Intune a TLS 1.2 per la crittografia).


### <a name="company-portal-for-windows-81-and-windows-phone-81-moving-to-sustaining-mode"></a>Passaggio dell'app Portale aziendale per Windows 8.1 e Windows Phone 8.1 alla modalità di solo supporto 
<!--1428681-->
*6 ottobre 2017*   
 
A partire da ottobre 2017, le app Portale aziendale per Windows 8.1 e Windows Phone 8.1 sono passate alla modalità di solo supporto. Ciò significa che le app e gli scenari esistenti, ad esempio la registrazione e la conformità, continuano a essere supportati per queste piattaforme. Queste app continuano a essere disponibili per il download tramite i canali di rilascio esistenti, ad esempio Microsoft Store. 

Nella modalità di solo supporto, queste app ricevono solo gli aggiornamenti della sicurezza critici. Non verranno rilasciati altri aggiornamenti né nuove funzionalità per queste app. Per le nuove funzionalità è consigliabile aggiornare i dispositivi a Windows 10 o a Windows 10 Mobile. 

### <a name="end-of-support-for-ios-80"></a>Fine del supporto per iOS 8.0 
<!---1164477---> Per accedere alle risorse aziendali, le app gestite e l'app Portale aziendale per iOS richiedono iOS 9.0 o versione successiva. I dispositivi non aggiornati prima di settembre non sono in grado di accedere al Portale aziendale o alle app gestite. 

### <a name="platform-support-reminder-windows-phone-81-mainstream-support-ended-july-11-2017"></a>Promemoria di supporto di piattaforma: il supporto Mainstream di Windows Phone 8.1 è terminato l'11 luglio 2017
<!-- 1327781 -->
*11 luglio 2017*

La piattaforma Windows Phone 8.1 ha raggiunto la fine del supporto Mainstream. Ciò non influisce sul supporto di Windows 8.1 per PC.

Non ci sono conseguenze immediate a sui dispositivi Windows Phone 8.1 gestiti dal servizio Intune, inclusi quelli registrati nella gestione dei dispositivi mobili ibrida. I dispositivi registrati continuano a funzionare. Tutti i criteri, le configurazioni e le app continuano a funzionare come previsto. Si noti che all'interno del servizio Intune non ci sono miglioramenti destinati alla piattaforma Windows Phone 8.1 e all'app del Portale aziendale di Windows Phone 8.1.

È consigliabile eseguire l'aggiornamento dei dispositivi Windows Phone 8.1 idonei a Windows 10 Mobile non appena possibile.  

### <a name="end-of-support-for-android-43-and-lower"></a>Fine del supporto per Android 4.3 e versioni precedenti
<!---1171127--->
*6 luglio 2017*

Per accedere alle risorse aziendali, le app gestite e l'app Portale aziendale per Android richiedono Android 4.4 o versione successiva. I dispositivi non aggiornati prima dell'inizio di ottobre non sono in grado di accedere al Portale aziendale o alle app gestite. Entro dicembre è stato imposto il ritiro di tutti i dispositivi registrati, con conseguente perdita dell'accesso alle risorse aziendali. Se si usano criteri di protezione delle app senza MDM, le app non ricevono gli aggiornamenti e la qualità dell'esperienza diminuisce nel tempo.



## <a name="see-also"></a>Vedere anche

- [Funzionalità MDM ibride precedenti e notifiche](whats-new-hybrid-archive.md)
- [Novità di MDM in System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)

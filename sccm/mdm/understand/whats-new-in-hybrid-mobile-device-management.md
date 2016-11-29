---
title: "Novità di MDM per dispositivi ibridi | Microsoft Intune | System Center Configuration Manager"
description: "Informazioni sulle nuove funzionalità di gestione dei dispositivi mobili disponibili per le distribuzioni ibride con System Center Configuration Manager e Intune."
ms.custom: na
ms.date: 10/25/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
caps.latest.revision: 40
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f13b38fcc4e7c55f05dbf6a7d8f516643939ba92
ms.openlocfilehash: 3525fba1b75196bddebc89e49f40cbfd3c75d9d0

---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Novità della gestione ibrida di dispositivi mobili con System Center Configuration Manager e Microsoft Intune

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo illustra le nuove funzionalità di gestione dei dispositivi mobili (MDM) disponibili per le distribuzioni ibride con System Center Configuration Manager e Intune.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilità con le versioni di Configuration Manager  

 In ogni sezione di questo articolo vengono elencate le funzionalità ibride in 3 categorie diverse. Usare le indicazioni che seguono per determinare la compatibilità delle funzionalità di ogni categoria con versioni diverse di Configuration Manager:  

|Categorie di funzionalità|
|-|  
|**Novità di Microsoft Intune**: in generale, tutte le funzionalità elencate in questa categoria devono funzionare con tutte le versioni di Configuration Manager, incluse le versioni di System Center 2012 R2 Configuration Manager, poiché richiedono solo il servizio Intune e non richiedono altre funzionalità di Configuration Manager.<br /><br /> **Novità di Configuration Manager Technical Preview**: tutte le funzionalità elencate in questa categoria funzionano solo con la versione di Technical Preview specificata. Per provare queste funzionalità, è necessario installare la versione di Technical Preview specificata nella descrizione della funzionalità. Per altre informazioni, vedere [Technical Preview per System Center Configuration Manager](../../core/get-started/technical-preview.md).<br /><br /> **Novità di Configuration Manager (Current Branch)**: tutte le funzionalità elencate in questa categoria funzionano solo con la versione di Configuration Manager (Current Branch) specificata, ad esempio la versione 1511 o 1602. Se si usa una versione precedente di Configuration Manager per la distribuzione ibrida, è necessario eseguire l'aggiornamento alla versione di Configuration Manager (Current Branch) specificata nella descrizione della funzionalità. Per altre informazioni, vedere l'articolo relativo agli [aggiornamenti a System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|  

## <a name="new-hybrid-features-in-october-2016"></a>Nuove funzionalità ibride (ottobre 2016)

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

Le seguenti funzionalità di Intune introdotte in ottobre 2016 funzionano nelle distribuzioni ibride.

- **Accesso condizionale per la gestione di applicazioni per dispositivi mobili**

  È possibile limitare l'accesso a Exchange Online in modo che possa essere eseguito solo dalle app che supportano i criteri di gestione delle applicazioni mobili di Intune, ad esempio Outlook. [Questa nuova funzionalità](/intune/deploy-use/allow-policy-managed-apps-access-to-o365) si combina perfettamente con i criteri di gestione MAM di Intune poiché è possibile bloccare l'accesso ai client di posta predefiniti o ad altre applicazioni che non sono state configurate con i criteri MAM di Intune. In questo modo gli utenti accedono ai dati dell'organizzazione con applicazioni che possono essere protette usando MAM di Intune. È possibile iniziare a usare la gestione delle app per dispositivi mobili di Intune dal portale di Azure. Cercare la nuova sezione relativa all'accesso condizionale nel pannello "Impostazioni".

-   **Strumento per la disposizione testo per app di Intune per Android**

  È possibile abilitare le app per l'uso dei criteri di gestione delle applicazioni per dispositivi mobili (MAM) di Intune usando lo strumento per la disposizione testo per app di Intune.

- **Compatibilità di Android Samsung KNOX con Intune**

  Alcuni modelli di telefoni Samsung Galaxy Ace non possono essere gestiti da Intune come dispositivi Samsung KNOX. Quando vengono registrati con Intune, questi dispositivi verranno invece gestiti come dispositivi Android standard.

  I numeri di modello interessati sono:

  - SM-G313HU
  - SM-G313HY
  - SM-G313M
  - SM-G313MY
  - SM-G313U

  L'utente e gli utenti finali non devono effettuare alcuna operazione. Per altre informazioni, visitare il sito Web di Samsung KNOX.

### <a name="new-in-configuration-manager-technical-preview-1610"></a>Novità di Configuration Manager Technical Preview 1610

Le seguenti nuove funzionalità ibride sono state introdotte nella versione di ottobre 2016 di Configuration Manager Technical Preview 1610.

- **Richiesta di una sincronizzazione dei criteri dalla console di amministrazione**

  È possibile richiedere una sincronizzazione dei criteri per un dispositivo mobile registrato dalla console di Configuration Manager anziché richiedere la sincronizzazione nell'app Portale aziendale sul dispositivo stesso. Si tratta di una nuova azione del menu Azioni remote dispositivo, **Send Sync Request** (Invia richiesta di sincronizzazione), che appare nella barra multifunzione quando si seleziona un dispositivo mobile nel nodo Dispositivi.

- **Impostazioni di configurazione di Windows Defender**

  È ora possibile configurare le impostazioni del client di Windows Defender nei computer Windows 10 registrati in Intune usando gli elementi di configurazione nella console di Configuration Manager. Esiste un nuovo gruppo di impostazioni denominato **Windows Defender** nella creazione guidata dell'elemento di configurazione. Si noti che questo è supportato solo in Windows 10 versione 1511 e successive.


### <a name="new-in-configuration-manager-current-branch"></a>Novità di Configuration Manager (Current Branch)

Non sono state introdotte nuove funzionalità ibride nella versione di agosto 2016 di Configuration Manager (Current Branch).

## <a name="new-hybrid-features-in-september-2016"></a>Nuove funzionalità ibride (settembre 2016)

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

Le seguenti funzionalità di Intune introdotte in settembre 2016 funzionano nelle distribuzioni ibride.

- **Aggiunta di "Notifiche" al portale aziendale per Android**

  Una nuova icona di notifica è stata aggiunta al portale aziendale per Android nella home page. Toccando l'icona si accede alla pagina delle notifiche, che visualizza per gli utenti finali tutti gli elementi che richiedono attenzione nell'app Portale aziendale, ad esempio la non conformità dei dispositivi, l'aggiornamento della registrazione e l'attivazione della registrazione. Nell'app Portale aziendale per iOS questo tipo di notifica è già in uso. Grazie alla disponibilità della nuova pagina Notifiche, l'utente non visualizzerà la pagina Configurazione dell'accesso aziendale ogni volta che avvia o riprende il portale aziendale, purché il dispositivo sia già registrato. Se si creano le proprie linee guida per l'utente finale, è consigliabile aggiornare la documentazione in modo che rifletta questa modifica. Le schermate aggiornate sono disponibili [qui](https://aka.ms/androidcpupdate).

- **Modifiche al supporto per l'app Portale aziendale per iOS**

  Tutti gli utenti dell'app Portale aziendale di Microsoft Intune per iOS ora devono usare la versione più recente. I nuovi utenti possono scaricare solo la versione più recente e gli utenti correnti devono eseguire l'aggiornamento a tale versione. La versione più recente richiede iOS 8.0 o versione successiva, quindi i dispositivi che eseguono versioni precedenti di iOS non possono usare il portale aziendale o essere registrati finché non vengono aggiornati a iOS 8.0 o versione successiva e l'app portale aziendale non viene aggiornata alla versione più recente. I dispositivi registrati che eseguono versioni precedenti a iOS 8.0 continueranno a essere gestiti ed elencati nella console di amministrazione di Intune.

- **Pulsante di invio feedback aggiunto all'app Portale aziendale per Windows Phone 8.1**

  L'app Portale aziendale per Windows Phone 8.1 consente agli utenti finali di inviare commenti e suggerimenti relativi all'app usando un nuovo pulsante di invio feedback. Per trovare il pulsante, gli utenti devono toccare il menu "tre punti" nella parte inferiore destra della schermata dell'app Portale aziendale e quindi toccare **Commenti e suggerimenti**. I commenti, raccolti in forma anonima, consentiranno a Microsoft di migliorare l'esperienza con l'app Portale aziendale degli utenti.

### <a name="new-in-configuration-manager-technical-preview-1609"></a>Novità di Configuration Manager Technical Preview 1609

Le seguenti nuove funzionalità ibride sono state introdotte nella versione di settembre 2016 di Configuration Manager Technical Preview 1609.

- **Impostazioni aggiuntive e prestazioni migliorate per le impostazioni degli elementi di configurazione**

  Sono state aggiunte nuove impostazioni per Android, iOS e Windows e solo le impostazioni relative alle piattaforme selezionate nella pagina delle piattaforme supportate vengono visualizzate nella procedura guidata. Per altre informazioni, vedere la sezione relativa alle [nuove impostazioni di conformità per gli elementi di configurazione in TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#new-compliance-settings-for-configuration-items).

- **Impostazioni aggiuntive per i profili DEP**

  Le opzioni TouchID, ApplePay e Zoom sono state aggiunte come impostazioni configurabili nei profili DEP per i dispositivi iOS.

- **App a pagamento in Windows Store per le aziende**

  È ora possibile aggiungere applicazioni sia a pagamento che gratuite a Windows Store per le aziende e distribuirle agli utenti dell'organizzazione. Per altre informazioni, vedere la sezione relativa ai [miglioramenti apportati a Windows Store per le aziende in TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#enhancements-to-windows-store-for-business-integration-with-configuration-manager).

- **Tipi di connessione nativa per i profili VPN di Windows 10**

  Ora è possibile creare profili VPN di Windows 10 per MDM con tipi di connessione Microsoft Automatico, IKEv2 e PPTP nella console di Configuration Manager senza usare URI OMA.

- **Grafici di conformità di Intune**

  È possibile visualizzare rapidamente informazioni generali sulla conformità dei dispositivi e i motivi principali di non conformità usando i nuovi grafici disponibili nell'area di lavoro Monitoraggio. Per altre informazioni, vedere i [grafici di conformità di Intune in TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#intune-compliance-charts).

### <a name="new-in-configuration-manager-current-branch"></a>Novità di Configuration Manager (Current Branch)

Le seguenti nuove funzionalità introdotte in settembre 2016 sono disponibili per le distribuzioni ibride con Microsoft Intune e Configuration Manager versione 1606 (Current Branch).

- **Supporto di iOS 10**

  Se si usano profili o elementi di configurazione destinati a tutte le piattaforme iOS, verranno inseriti in iOS 10. È stato anche rilasciato un aggiornamento di Configuration Manager versione 1606 che consente di destinare i profili e gli elementi di configurazione a singole piattaforme iOS tra cui iOS 10. È possibile installare l'aggiornamento con la console di amministrazione di Configuration Manager da **Amministrazione > Panoramica > Servizi cloud > Aggiornamenti e manutenzione**. Altre informazioni sull'aggiornamento sono disponibili all'indirizzo [http://support.microsoft.com/kb/3192616](http://support.microsoft.com/kb/3192616).

## <a name="new-hybrid-features-in-august-2016"></a>Nuove funzionalità ibride (agosto 2016)

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

Le seguenti funzionalità di Intune introdotte in agosto 2016 funzionano nelle distribuzioni ibride.

- **Supporto per Android 7 nell'app Portale aziendale**

  L'app Portale aziendale di Intune per Android offre il supporto "giorno 0" per il sistema operativo Android 7.0 per dispositivi mobili`che verrà introdotto prossimamente.

- **Rimozione da parte di Google della funzionalità di reimpostazione remota del passcode nei dispositivi Android 7.0**

  Google sta eliminando la possibilità per amministratori IT e utenti finali di reimpostare in modalità remota il passcode dei dispositivi Android 7.0. In precedenza gli amministratori IT potevano reimpostare il passcode di un utente in modalità remota e gli utenti finali potevano reimpostare i propri passcode dal sito Web del portale aziendale.

- **Criterio per app consentite e bloccate per i dispositivi Samsung KNOX**

  È ora possibile configurare per i dispositivi Samsung KNOX un criterio personalizzato che consente di creare uno dei seguenti elementi:

  - Un elenco di app la cui esecuzione è bloccata sul dispositivo. Anche se installata, un'app definita nell'elenco delle app bloccate non può essere attivata sul dispositivo.
  - Un elenco di app che gli utenti del dispositivo sono autorizzati a installare da Google Play Store. Non sarà possibile installare altre app dallo Store.

  Queste impostazioni possono essere usate solo dai dispositivi con Samsung KNOX. Per informazioni dettagliate, vedere [Usare criteri personalizzati per consentire e bloccare app per dispositivi Samsung KNOX](/intune/deploy-use/custom-policy-to-allow-and-block-samsung-knox-apps).

- **Collegamento per invio del feedback dal Portale aziendale a Microsoft**

   Il sito Web del portale aziendale consente agli utenti di toccare il nuovo collegamento "Commenti e suggerimenti" nella parte inferiore della pagina, per inviare un feedback a Microsoft sulla propria esperienza con il sito. I commenti, raccolti in forma anonima, consentiranno a Microsoft di migliorare l'esperienza degli utenti con il sito Web del portale aziendale.

- **Versione minima di Managed Browser per iOS aggiornata a 8.0**

  L'app Microsoft Intune Managed Browser per iOS è stata aggiornata in modo da supportare i dispositivi che eseguono iOS 8.0 o versioni successive. Anche se i dispositivi iOS 7.1 possono continuare a usare l'app Managed Browser esistente, suggerire agli utenti di aggiornare iOS alla versione 8.0 o successiva per accedere e usufruire di tutte le nuove funzionalità di Managed Browser.

### <a name="new-in-configuration-manager-technical-preview"></a>Novità di Configuration Manager Technical Preview

Non sono state introdotte nuove funzionalità ibride nella versione di agosto 2016 di Configuration Manager Technical Preview.

### <a name="new-in-configuration-manager-current-branch"></a>Novità di Configuration Manager (Current Branch)

Non sono state introdotte nuove funzionalità ibride nella versione di agosto 2016 di Configuration Manager (Current Branch).

## <a name="new-hybrid-features-in-july-2016"></a>Nuove funzionalità ibride (luglio 2016)

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

Le seguenti funzionalità di Intune introdotte in luglio 2016 funzionano nelle distribuzioni ibride.

- **È disponibile Xamarin SDK per le app di Intune**

  Il componente Xamarin SDK per app di Intune consente di abilitare le funzionalità di gestione delle app per dispositivi mobili di Intune nelle app per dispositivi mobili iOS e Android compilate con Xamarin. Il componente è disponibile nell'[archivio Xamarin](https://components.xamarin.com/view/Microsoft.Intune.MAM) o nella [pagina GitHub di Microsoft Intune](https://github.com/msintuneappsdk).

- **Esperienza utente finale migliorata durante la registrazione dei dispositivi Windows**

  Quando si utilizza l'accesso condizionale, la procedura di registrazione per Windows 8.1, Windows 10 Desktop e 10 Windows Mobile è illustrata nel sito Web del portale aziendale. Gli utenti ora vedono passaggi separati per la **registrazione del dispositivo** e l'**aggiunta all'area di lavoro** quindi è più semplice verificare lo stato del dispositivo e completare il processo nel caso in cui l'aggiunta all'area di lavoro abbia esito negativo. Si prevede che la separazione dei passaggi semplifichi anche il processo di risoluzione dei problemi per gli amministratori IT. In precedenza, quando gli utenti finali tentavano di eseguire la registrazione e tutti i passaggi, tranne l'aggiunta all'area di lavoro, venivano completati correttamente, il dispositivo non appariva nell'elenco dei dispositivi per l'identificazione e questo causava confusione per gli utenti.

 - **Cancellazione completa ora disponibile per i dispositivi Windows 10**

    I computer desktop e portatili Windows 10 registrati come dispositivi mobili possono essere cancellati per ripristinare le impostazioni di fabbrica del dispositivo. Per altre informazioni, vedere le istruzioni per [proteggere i dispositivi con la cancellazione remota](/sccm/mdm/deploy-use/wipe-lock-reset).

- **Modifiche agli account di Manager di registrazione dispositivi nell'app Portale aziendale per iOS**

  Per migliorare le prestazioni e la scalabilità, in Intune non vengono più visualizzati tutti i dispositivi di Manager di registrazione dispositivi (DEM) nel riquadro dei dispositivi personali dell'app Portale aziendale per iOS. Viene visualizzato solo il dispositivo locale che esegue l'app e solo se è stato registrato usando l'app Portale aziendale.

  L'utente di DEM può eseguire azioni sul dispositivo locale, ma la gestione remota di altri dispositivi registrati può essere effettuata solo dalla console di amministrazione di Intune. In Intune verrà anche deprecato l'uso degli account DEM con il programma di registrazione dispositivi di Apple o lo strumento Apple Configurator. Entrambi i metodi di registrazione supportano già la registrazione senza utente per i dispositivi iOS condivisi.

  Usare gli account DEM solo se non è disponibile la registrazione senza utente per i dispositivi condivisi. Per altre informazioni, vedere l'articolo relativo alla [registrazione dei dispositivi di proprietà dell'azienda con Manager di registrazione dispositivi in Microsoft Intune](../deploy-use/enroll-devices-with-device-enrollment-manager.md).

- **Modifiche dell'app Portale aziendale per Android**

  Se gli utenti finali di Android visualizzano un messaggio di errore che indica che manca un certificato obbligatorio per il dispositivo, possono toccare il pulsante "Risoluzione del problema" per avere informazioni sulla procedura di installazione del certificato mancante. Se gli utenti completano la procedura ma visualizzano un altro messaggio di errore che indica che manca un certificato, dovranno contattare l'amministratore IT e indicare questo collegamento, dove gli amministratori IT troveranno i passaggi da seguire per risolvere il problema.

- **Limitazione delle installazioni di app sottoposte a sideload nei dispositivi Android registrati**

  I dispositivi Android non sono più in grado di installare applicazioni dal sito Web del portale aziendale, a meno che non siano stati registrati in Intune usando l'app Portale aziendale per Android.


### <a name="new-in-configuration-manager-technical-preview"></a>Novità di Configuration Manager Technical Preview

Non sono state introdotte nuove funzionalità ibride nella versione di luglio 2016 di Configuration Manager Technical Preview.

### <a name="new-in-configuration-manager-current-branch"></a>Novità di Configuration Manager (Current Branch)

Le seguenti funzionalità, che in precedenza erano disponibili nelle versioni di Configuration Manager Technical Preview, sono ora disponibili nelle distribuzioni ibride con Intune e Configuration Manager (Current Branch) versione 1606.

* Trovare, gestire e distribuire app di Windows Store per le aziende per i dispositivi Windows 10 dalla console di Configuration Manager ([1604](whats-new-hybrid-archive.md#new-in-1604-technical-preview))
*   Impostazione di Smart Lock per dispositivi Android ([1604](whats-new-hybrid-archive.md#new-in-1604-technical-preview))
*   VPN attivata dall'app per dispositivi Windows 10 ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Nuova esperienza per le azioni dei dispositivi remoti ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   App di Windows Store per le aziende ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Miglioramenti generali per le app acquistate con Volume Purchase Program ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Windows Information Protection (WIP) ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Predichiarazione dei dispositivi di proprietà dell'azienda con numero di serie IMEI o iOS ([1605](whats-new-hybrid-archive.md#new-in-1605-technical-preview))
*   Categorizzazione automatica dei dispositivi in raccolte ([1606](whats-new-hybrid-archive.md#new-in-1606-technical-preview))

Per informazioni sulle nuove funzionalità, vedere la documentazione relativa alla versione di Technical Preview specificata.

## <a name="notices"></a>Notifiche

- **25 ottobre 2016: deprecato il caricamento del portale aziendale per Windows Phone 8**

  L'opzione che consente di caricare un'app Portale aziendale firmata è stata rimossa dalla console di Configuration Manager, poiché il supporto di Intune viene deprecato per Windows 8, Windows Phone 8 e Windows RT e il supporto per il portale aziendale per Windows Phone 8 termina in novembre.  I dispositivi Windows 8, Windows Phone 8 e Windows RT che sono già registrati continueranno a essere supportati, ma la registrazione di dispositivi aggiuntivi con queste piattaforme non sarà più supportata.


### <a name="see-also"></a>Vedere anche

- [Funzionalità MDM ibride precedenti](whats-new-hybrid-archive.md)
- [Novità di MDM in System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)



<!--HONumber=Nov16_HO1-->



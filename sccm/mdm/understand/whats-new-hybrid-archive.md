---
title: "Archivio delle novità della gestione ibrida di dispositivi mobili | Microsoft Docs"
description: "Archivio di funzionalità di gestione dei dispositivi mobili precedenti disponibili per le distribuzioni ibride con System Center Configuration Manager e Intune."
ms.custom: na
ms.date: 10/25/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c27b161-9eb7-4cdd-b469-d8eb27e71aea
author: Mtillman
ms.author: mtillman
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: 238ef5814c0c1b832c28d63c9f3879e21a6c439b
ms.openlocfilehash: 086b350005e9665e8b91c11e664563f9687aca27

---
# <a name="past-hybrid-features-with-system-center-configuration-manager-and-microsoft-intune"></a>Funzionalità ibride precedenti con System Center Configuration Manager e Microsoft Intune

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo illustra le funzionalità di gestione dei dispositivi mobili (MDM) precedenti disponibili per le distribuzioni ibride con System Center Configuration Manager e Intune.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilità con le versioni di Configuration Manager  

 In ogni sezione di questo articolo vengono elencate le funzionalità ibride in 3 categorie diverse. Usare le indicazioni che seguono per determinare la compatibilità delle funzionalità di ogni categoria con versioni diverse di Configuration Manager:  

|Categorie di funzionalità|
|-|  
|**Novità di Microsoft Intune**: in generale, tutte le funzionalità elencate in questa categoria devono funzionare con tutte le versioni di Configuration Manager, incluse le versioni di System Center 2012 R2 Configuration Manager, poiché richiedono solo il servizio Intune e non richiedono altre funzionalità di Configuration Manager.<br /><br /> **Novità di Configuration Manager Technical Preview**: tutte le funzionalità elencate in questa categoria funzionano solo con la versione di Technical Preview specificata. Per provare queste funzionalità, è necessario installare la versione di Technical Preview specificata nella descrizione della funzionalità. Per altre informazioni, vedere [Technical Preview per System Center Configuration Manager](../../core/get-started/technical-preview.md).<br /><br /> **Novità di Configuration Manager (Current Branch)**: tutte le funzionalità elencate in questa categoria funzionano solo con la versione di Configuration Manager (Current Branch) specificata, ad esempio la versione 1511 o 1602. Se si usa una versione precedente di Configuration Manager per la distribuzione ibrida, è necessario eseguire l'aggiornamento alla versione di Configuration Manager (Current Branch) specificata nella descrizione della funzionalità. Per altre informazioni, vedere l'articolo relativo agli [aggiornamenti a System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|  

## <a name="new-hybrid-features-in-june-2016"></a>Nuove funzionalità ibride (giugno 2016)

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune
Le seguenti funzionalità di Intune introdotte in giugno 2016 funzionano nelle distribuzioni ibride.

- **Stato del servizio Intune**: le informazioni sullo stato del servizio per Intune sono state spostate in una posizione centrale con altri servizi Microsoft. Queste informazioni ora sono disponibili nel portale di gestione di Office 365 in Integrità del servizio. Per altre informazioni, vedere questo [post di blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/04/28/intune-service-health-is-now-available-in-the-office-365-portal/).

- **Gestione ottimizzata della configurazione dei criteri per i dati aziendali in Windows 10**

  Intune è ora in grado di offrire una migliore esperienza di configurazione dei criteri di protezione dei dati di Windows 10. I miglioramenti includono procedure ottimizzate per la creazione di regole delle app, la definizione dei limiti di rete e altre impostazioni di protezione delle informazioni di Windows. Per altre informazioni, vedere [Creare un criterio di Windows Information Protection (WIP) con Microsoft Intune](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-intune).

- **Criteri di controllo dell'accesso alla rete Cisco ISE per Intune**

  I clienti che usano Cisco Identity Service Engine (ISE) 2.1 oltre a Microsoft Intune possono impostare in ISE un criterio di controllo dell'accesso alla rete in base al quale i dispositivi che si connettono alla rete usando una connessione Wi-Fi o VPN devono soddisfare le condizioni seguenti per essere autorizzati ad accedere:

  - Devono essere gestiti da Intune
  - Devono essere conformi a eventuali criteri di conformità di Intune distribuiti

  Agli utenti finali dei dispositivi non conformi verrà richiesto di effettuare la registrazione e di risolvere eventuali problemi di conformità per ottenere l'accesso.

- **Accesso condizionale per il browser**

  È possibile impostare un criterio di accesso condizionale per Exchange Online e SharePoint Online in modo che siano accessibili solo dai Web browser supportati in dispositivi iOS e Android gestiti e conformi. Agli utenti finali che tentano di accedere a siti di Outlook Web Access (OWA) e SharePoint con dispositivi iOS e Android verrà richiesta la registrazione del dispositivo con Intune nonché la correzione di eventuali problemi di conformità per poter eseguire l'accesso. Per ulteriori informazioni, vedere

  * [Limitare l'accesso alla posta elettronica per Exchange Online e il nuovo ambiente Exchange Online dedicato](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-exchange-online-with-microsoft-intune)
  * [Limitare l'accesso a SharePoint Online con Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune)

- **Dynamics CRM Online supporta l'accesso condizionale**

  È possibile impostare un criterio di accesso condizionale per Dynamics CRM Online in modo che sia possibile accedervi solo da dispositivi iOS e Android gestiti e conformi. Gli utenti finali che tentano di accedere all'App mobile Dynamics CRM in iOS e Android dovranno eseguire la registrazione con Intune, nonché risolvere eventuali problemi di conformità prima di accedere. Per altre informazioni, vedere [Limitare l'accesso a Dynamics CRM Online con Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-dynamics-crm-online-with-microsoft-intune).

- **Aggiornamenti dell'app Portale aziendale per Android**

  Intune ora offre i seguenti nuovi criteri agli utenti del portale aziendale per Android:   

  Criteri  |Effetti sugli utenti  
  ---------|---------
  Richiedi che i dispositivi impediscano l'installazione di app da origini sconosciute (Android 4.0+)     |  Gli utenti finali con dispositivi Android 4.0 o versioni successive vedranno il messaggio "L'installazione da origini sconosciute deve essere disabilitata". Gli utenti dovranno passare a **Impostazioni > Sicurezza** sui propri dispositivi e disattivare **Origini sconosciute**. Un collegamento nel messaggio sulla conformità consente agli utenti di visualizzare altre informazioni sul messaggio e sul motivo per cui viene richiesta la disattivazione dell'impostazione.
  Richiedi che i dispositivi impediscano l'installazione di app da origini sconosciute (Android 4.0+)  |    Gli utenti finali con dispositivi Android 4.0 o versioni successive vedranno il messaggio "Cerca minacce per la sicurezza nel dispositivo". Gli utenti dovranno passare a **Impostazioni > Google > Sicurezza** sui propri dispositivi e attivare **Cerca minacce per la sicurezza nel dispositivo**. Un collegamento nel messaggio sulla conformità consente agli utenti di visualizzare altre informazioni sul messaggio e sul motivo per cui viene richiesta l'attivazione dell'impostazione.     
  Richiedi la disabilitazione del debug USB (Android 4.2+)  | Gli utenti finali con dispositivi Android 4.2 o versioni successive vedranno il messaggio "Il debug USB deve essere disabilitato". Gli utenti dovranno passare a **Impostazioni > Opzioni per gli sviluppatori** sui propri dispositivi e disattivare **Debug USB**. Un collegamento nel messaggio sulla conformità consente agli utenti di visualizzare altre informazioni sul messaggio e sul motivo per cui viene richiesta la disattivazione dell'impostazione.
  Livello minimo di patch di protezione per Android (Android 6.0+)  | Gli utenti finali con dispositivi Android 6.0 o versioni successive vedranno il messaggio "Questo dispositivo non rispetta il livello minimo di patch di protezione per Android". Gli utenti dovranno installare la patch di protezione richiesta. Un collegamento nel messaggio sulla conformità consente agli utenti di visualizzare informazioni sulla procedura di installazione della patch di protezione richiesta e sulla patch di protezione attualmente installata.

- **Aggiornamenti dell'app Portale aziendale per iOS**

  * Quando gli utenti finali installano le applicazioni line-of-business, ora usufruiscono di un'esperienza di installazione ottimizzata. Se l'installazione delle app richiede molto tempo, gli utenti possono sincronizzare manualmente il dispositivo per forzare la ripresa del processo di sincronizzazione. Per leggere le istruzioni per l'utente finale, vedere la sezione sulla sincronizzazione manuale dei dispositivi iOS.
  * L'app Portale aziendale di Microsoft Intune per iOS è stata aggiornata per supportare iOS versione 8.0 e versioni successive. Questo aggiornamento significa che gli utenti finali possono installare l'app Portale aziendale e registrare i nuovi dispositivi per Intune solo se i dispositivi eseguono iOS versione 8.0 o successiva. Gli utenti che hanno già iscritto dispositivi che eseguono una versione non supportata di iOS possono continuare a utilizzare l'app portale aziendale sul dispositivo.


### <a name="new-in-1606-technical-preview"></a>Novità in Technical Preview 1606
Le seguenti nuove funzionalità introdotte in giugno 2016 sono disponibili nelle distribuzioni ibride con Intune e Configuration Manager Technical Preview 1606.

- **Categorizzazione automatica dei dispositivi in raccolte**

  È possibile creare categorie di dispositivi da usare per inserire automaticamente i dispositivi in raccolte quando si usa Configuration Manager con Intune. Agli utenti verrà quindi richiesto di scegliere una categoria di dispositivi quando eseguono la registrazione di un dispositivo in Intune. È possibile modificare la categoria di un dispositivo dalla console di Configuration Manager. Per altre informazioni, vedere [Categorizzazione automatica dei dispositivi in raccolte](/sccm/core/get-started/capabilities-in-technical-preview-1606.md#dmp_category) in [Funzionalità di Technical Preview 1606 per System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1606.md).

  > [!IMPORTANT]
  > Questa funzionalità può essere usata con la versione di Microsoft Intune di giugno 2016. Verificare che l'installazione sia aggiornata a questa versione prima di tentare tali procedure.

### <a name="new-in-configuration-manager-current-branch"></a>Novità di Configuration Manager (Current Branch)
Non sono state introdotte nuove funzionalità ibride nella versione di giugno 2016 di Configuration Manager (Current Branch).

##  <a name="new-hybrid-features-in-may-2016"></a>Nuove funzionalità ibride (maggio 2016)  

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune  
 Le seguenti funzionalità di Intune introdotte in maggio 2016 funzionano nelle distribuzioni ibride.

- **SDK MAM: supporto per la configurazione della lunghezza del PIN**

  È ora possibile specificare la lunghezza del PIN per le app MAM in modo simile al PIN di un dispositivo. Per eseguire questa operazione gli utenti finali devono rispettare i nuovi limiti impostati. La schermata del PIN è stata leggermente modificata per consentire un input più lungo. Per informazioni dettagliate, vedere le [ impostazioni dei criteri MAM per Android](https://docs.microsoft.com/intune/deploy-use/android-mam-policy-settings) e le [impostazioni dei criteri MAM per iOS](https://docs.microsoft.com/intune/deploy-use/ios-mam-policy-settings).  

- **Skype for Business per iOS e Android**

  È ora possibile applicare a Skype for Business i [criteri MAM senza registrazione](https://docs.microsoft.com/intune/deploy-use/get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune). Quando gli utenti eseguono l'accesso, i criteri MAM vengono applicati.  

- **Nuove app disponibili per la gestione con i criteri MAM**

  Le app Microsoft Word, Excel e PowerPoint per Android ora possono essere associate a criteri MAM sui dispositivi non registrati per Intune. Per un elenco completo delle app supportate, vedere la raccolta di applicazioni per dispositivi mobili di Microsoft Intune nella pagina dei [partner di applicazioni di Microsoft Intune](https://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/partners.aspx).  

- **App Portale aziendale Android: notifiche di tipo avviso popup degli utenti finali**

  Le notifiche di tipo avviso popup provenienti dall'app Portale aziendale per Android vengono visualizzate quando gli utenti finali registrano o rimuovono i propri dispositivi dal portale aziendale.  

- **Sito Web del portale aziendale: il banner di identificazione del dispositivo contiene più informazioni per gli utenti finali**

  Gli utenti finali ora possono identificare più facilmente il dispositivo selezionato quando usano il sito Web del portale aziendale. Se è selezionato il dispositivo errato, è possibile selezionare il dispositivo corretto toccando il collegamento **Tocca qui** nel banner della pagina iniziale.  


### <a name="new-in-1605-technical-preview"></a>Novità in Technical Preview 1605  
 Le seguenti nuove funzionalità introdotte in maggio 2016 sono disponibili nelle distribuzioni ibride con Intune e Configuration Manager Technical Preview 1605. Queste funzionalità richiedono l'uso della console di Configuration Manager per la configurazione e la gestione.  

- **VPN attivata dall'app per dispositivi Windows 10**

  Per i dispositivi Windows 10 gestiti usando Configuration Manager con Intune è possibile aggiungere un elenco di app che aprono automaticamente una connessione VPN configurata dalla console di amministrazione di Configuration Manager. Per altre informazioni, vedere la sezione relativa alle [connessioni VPN attivate da app per Windows 10](/sccm/core/get-started/capabilities-in-technical-preview-1605) in [Funzionalità di Technical Preview 1605 per System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605)  

- **Nuova esperienza per le azioni dei dispositivi remoti**

  È stata migliorata l'esperienza di esecuzione di azioni dei dispositivi remoti dalla console di Configuration Manager.

  Azioni comuni come **ritiro/cancellazione**, **reimpostazione passcode**, **blocco remoto** e **blocco attivazione bypass** sono adesso disponibili nel menu **Azioni dispositivo remoto** accessibile dall'area di lavoro **Asset e conformità**

  Per altre informazioni, vedere [Nuova esperienza per le azioni dei dispositivi remoti](/sccm/core/get-started/capabilities-in-technical-preview-1605#new-experience-for-remote-device-actions) in [Funzionalità di Technical Preview 1605 per System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **App di Windows Store per le aziende**

  In [Windows Store per le aziende](https://www.microsoft.com/en-us/business-store) è possibile trovare e acquistare app per l'organizzazione, singolarmente o con Volume Purchase Program. Connettendo lo Store a Configuration Manager, è possibile gestire le app acquistate con Volume Purchase Program dalla console di Configuration Manager. Per altre informazioni, vedere la sezione sulle [app disponibili in Windows Store per le aziende](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#windows-store-for-business-apps) in [Funzionalità di Technical Preview 1605 per System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Miglioramenti generali per le app acquistate con Volume Purchase Program**

  Le app acquistate con Volume Purchase Program da Windows Store per le aziende e dall'App Store di iOS sono state consolidate nella vista delle **informazioni sulle licenze per le app dello Store**. È stato anche migliorato il modo in cui vengono create le app acquistate con Volume Purchase Program per iOS. Per altre informazioni, vedere [Miglioramenti generali per le app acquistate con Volume Purchase Program](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#general-improvements-for-volume-purchased-apps) in [Funzionalità di Technical Preview 1605 per System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Predichiarare i dispositivi di proprietà dell'azienda con numero di serie IMEI o iOS**

  È ora possibile identificare i dispositivi di proprietà dell'azienda importando i relativi codici IMEI (International station Mobile Equipment Identity). È possibile caricare un file con valori separati da virgola (CSV) contenente i codici IMEI o immettere manualmente le informazioni relative ai dispositivi.  È possibile importare i numeri di serie anche per i dispositivi iOS.  Per altre informazioni, vedere [Predichiarare i dispositivi di proprietà dell'azienda con numero di serie IMEI o iOS](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_IMEI) in [Funzionalità di Technical Preview 1605 per System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Windows Information Protection (WIP)**

  È possibile creare elementi di configurazione che consentono di distribuire i criteri di Windows Information Protection (WIP), ad esempio consentono di scegliere le app protette, il livello di protezione WIP e come trovare i dati aziendali in rete. Per altre informazioni su WIP, vedere gli argomenti seguenti:  

  -   [Proteggere i dati aziendali con Windows Information Protection (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [Creare e distribuire un criterio di Windows Information Protection (WIP) con System Center Configuration Manager](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### <a name="new-in-configuration-manager-current-branch"></a>Novità di Configuration Manager (Current Branch)  
 Non sono state introdotte nuove funzionalità ibride nella versione di maggio 2016 di Configuration Manager (Current Branch).  

##  <a name="new-hybrid-features-in-april-2016"></a>Nuove funzionalità ibride (aprile 2016)  

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune  
 Le seguenti funzionalità di Intune introdotte in aprile 2016 funzionano nelle distribuzioni ibride.  

- **Conformità utente MAM**

  È ora possibile visualizzare lo stato dei criteri di gestione delle applicazioni per qualsiasi utente nel tenant di Azure Active Directory (AAD).  Per altre informazioni, vedere [Monitorare i criteri di gestione delle app per dispositivi mobili con Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) nella libreria di Intune.  

- **Controlli MAM per impedire la sincronizzazione dei contatti di Outlook (Android)**

  È disponibile una nuova impostazione che consente di impedire a un'applicazione di sincronizzare i contatti con la rubrica nativa sui dispositivi Android. Questa nuova impostazione è supportata inizialmente dall'applicazione Outlook sui dispositivi Android. Per altre informazioni, vedere [Creare e distribuire i criteri di gestione delle app per dispositivi mobili con Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) nella libreria di Intune.  

- **Miglioramenti del sito Web del portale aziendale**

  Quando gli utenti di Windows Phone 8.1 e Windows 10 Mobile installano le app line-of-business, visualizzeranno i nuovi stati descritti di seguito, che offrono maggiori dettagli sullo stato dell'installazione:  

  -   **In attesa della sincronizzazione del dispositivo**: l'utente ha toccato "Installa" e il dispositivo tenta di sincronizzarsi con l'infrastruttura di Intune. La sincronizzazione è necessaria per poter completare l'installazione. Il messaggio "In attesa della sincronizzazione del dispositivo" è anche un collegamento che gli utenti possono toccare per visualizzare le istruzioni su come sincronizzare manualmente il dispositivo con Intune se il processo di sincronizzazione impiega troppo tempo o si blocca.  

  -   **Download in corso**: viene elaborata la richiesta di download dell'utente e il dispositivo sta scaricando e installando l'app.  

- **Miglioramenti dell'app Portale aziendale per Android**

  Gli utenti che non hanno registrato il proprio dispositivo in Intune e non hanno installato il certificato corretto non saranno in grado di accedere all'app Portale aziendale per Android e visualizzeranno il messaggio "Non è possibile accedere perché un certificato necessario non è presente nel dispositivo". Il messaggio include un collegamento "Risoluzione del problema" che gli utenti possono toccare per vedere le istruzioni per l'installazione del certificato. Per i passaggi che gli utenti finali devono seguire per risolvere il problema, vedere [Manca un certificato necessario per il dispositivo](/intune/enduser/using-your-android-device-with-intune) nella libreria di Intune.  

- **Miglioramenti dell'app Portale aziendale per iOS**

  È stato aggiunto il supporto per l'azione Pull per aggiornare, che consente di aggiornare il contenuto della schermata iniziale, che include le applicazioni elencate, i dispositivi elencati e le informazioni di contatto del reparto IT. L'azione Pull per aggiornare non controlla le informazioni relative alla conformità o ai criteri, ma l'operazione può essere eseguita selezionando il riquadro per il dispositivo corrente e toccando il pulsante **Sincronizza**.  

- **Miglioramenti dell'app Portale aziendale per Windows 10 Mobile e Windows Phone 8.1**

  Quando gli utenti finali installano le applicazioni line-of-business, ora usufruiscono di un'esperienza di installazione ottimizzata. Se l'installazione delle app richiede molto tempo, gli utenti possono sincronizzare manualmente il dispositivo per forzare la ripresa del processo di sincronizzazione. Per esaminare le istruzioni per l'utente finale, vedere l'argomento della libreria di Intune sulla [sincronizzazione manuale del dispositivo per velocizzare l'installazione delle app](/intune/enduser/using-your-windows-device-with-intune).  

###  <a name="new-in-1604-technical-preview"></a>Novità in Technical Preview 1604
 Le seguenti nuove funzionalità introdotte in aprile 2016 sono disponibili nelle distribuzioni ibride con Intune e Configuration Manager Technical Preview 1604. Queste funzionalità richiedono l'uso della console di Configuration Manager per la configurazione e la gestione.  

- **Trovare, gestire e distribuire app di Windows Store per le aziende per i dispositivi Windows 10 dalla console di Configuration Manager**


  In Configuration Manager Technical Preview 1604 è disponibile il supporto per Windows Store per le aziende, che consente di trovare, gestire e distribuire le app ai dispositivi Windows 10 gestiti dall'utente. Per informazioni dettagliate, vedere la sezione [Gestire le app acquistate con Volume Purchase Program da Windows Store per le aziende](/sccm/core/get-started/capabilities-in-technical-preview-1604#manage-volume-purchased-apps-from-the-windows-store-for-business) in [Funzionalità di Technical Preview 1604 per System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604).  

- **Impostazione di Smart Lock per dispositivi Android**

  È stata aggiunta all'elemento di configurazione Android e Samsung KNOX Standard una nuova impostazione che consente di controllare la funzionalità Smart Lock sui dispositivi Android compatibili.  È possibile usare questa impostazione per impedire agli utenti finali di configurare Smart Lock. Vedere [Impostazione di SmartLock per dispositivi Android](/sccm/get-started/capabilities-in-technical-preview-1604#smartlock-setting-for-android-devices) in [Funzionalità di Technical Preview 1604 per System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604.md).  

### <a name="new-in-configuration-manager-current-branch"></a>Novità di Configuration Manager (Current Branch)  
 Non sono state introdotte nuove funzionalità ibride nella versione di aprile 2016 di Configuration Manager (Current Branch).  

##  <a name="new-hybrid-features-in-march-2016"></a>Nuove funzionalità ibride (marzo 2016)  

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune  
 Le seguenti funzionalità di Intune introdotte in marzo 2016 funzionano nelle distribuzioni ibride.  

- **Controlli MAM per impedire la sincronizzazione dei contatti di Outlook (iOS)**

  È disponibile una nuova impostazione che consente di impedire a un'applicazione di sincronizzare i contatti con la rubrica nativa sui dispositivi iOS. Questa nuova impostazione è supportata dall'applicazione Outlook sui dispositivi iOS. Per altre informazioni su questa e altre impostazioni, vedere [Creare e distribuire i criteri di gestione delle app per dispositivi mobili con Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) nella libreria di Intune.  

- **Skype for Business Online supporta l'accesso condizionale**

  È possibile impostare un criterio di accesso condizionale per Skype for Business Online in modo che sia possibile accedervi solo da dispositivi iOS e Android gestiti e conformi.  Per informazioni dettagliate, vedere l'articolo sulla [gestione dell'accesso a Skype per Business Online](/intune/deploy-use/restrict-access-to-skype-for-business-online-with-microsoft-intune) nella libreria di Intune.  

- **Supporto per iOS 9.3**

  Lunedì 21 marzo Apple ha annunciato la disponibilità di iOS 9.3. Tutte le funzionalità Intune esistenti attualmente disponibili per la gestione dei dispositivi iOS continueranno a funzionare senza interruzioni quando gli utenti aggiornano i propri dispositivi a iOS 9.3.  

- **Pacchetti di app Windows disponibili direttamente dal sito Web del portale aziendale**

  Gli utenti dei computer con Windows 8, Windows 8.1 e Windows RT ora possono installare i pacchetti di app Windows (con estensione APPX) direttamente dal sito Web del portale aziendale. In precedenza era necessario distribuire i pacchetti o gli utenti dovevano installare l'app Portale aziendale nei dispositivi per installare le app.  

- **Gli utenti possono bloccare in remoto il proprio dispositivo dal sito Web del portale aziendale**

  La nuova opzione Blocco remoto è stata aggiunta al sito Web del portale aziendale per consentire agli utenti di bloccare in remoto il proprio dispositivo dal portale se il dispositivo viene smarrito o rubato.  

- **Sfruttare i vantaggi della gestione "Open In" di iOS per i dispositivi registrati in una soluzione MDM di terze parti**

  È possibile usare il fornitore MDM di terze parti per sfruttare i vantaggi della gestione "Open In" di iOS. Le restrizioni possono essere impostate nel profilo di configurazione e l'app può essere distribuita usando il software MDM. Quando l'utente installa l'app gestita, vengono applicate le restrizioni. Per maggiori dettagli, vedere [Criteri di gestione delle app per dispositivi mobili e funzionalità Open In di iOS](/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune) nella libreria di Intune.  

- **App Microsoft che supportano MAM**

  L'elenco di app Microsoft che possono essere usate con i criteri di gestione delle applicazioni per dispositivi mobili di Intune è stato aggiornato in modo da includere le app più recenti (solo per i dispositivi registrati per Intune).  

- **Distribuire Adobe Reader per Microsoft Intune ai dispositivi iOS gestiti da Intune nell'azienda**

  L'app Adobe Reader per iOS ora può essere gestita sui dispositivi registrati con il criterio di gestione delle applicazioni per dispositivi mobili di Intune.  

- L'app di condivisione Rights Management è supportata per Android

  Gli amministratori IT possono distribuire i criteri di gestione delle applicazioni per dispositivi mobili in modo tale che gli utenti finali siano in grado di visualizzare immagini, contenuto audio e video e file PDF in modo più sicuro, indipendentemente dal fatto che il reparto IT usi Intune per gestire i dispositivi.  

- **Miglioramenti dell'app Portale aziendale per Android e iOS**

  -   Quando gli utenti avviano un'app gestita dalla funzionalità di gestione delle applicazioni per dispositivi mobili (MAM) visualizzano un messaggio che li informa che l'applicazione è gestita dall'azienda. Gli utenti ora possono toccare il collegamento "Ulteriori informazioni" per visualizzare maggiori dettagli sul significato di "app gestita". Se gli utenti toccano "Non visualizzare più questo messaggio", non vedranno più il messaggio quando avviano l'app.  

  -   Sono state aggiunte nuove schermate per guidare gli utenti nel processo di registrazione e offrire altre informazioni sui motivi per cui gli utenti devono registrare i dispositivi e sugli elementi che gli amministratori IT possono e non possono vedere sui dispositivi registrati.  

  -   I messaggi di errore relativi alla registrazione ora vengono visualizzati nell'app Portale aziendale.  

### <a name="new-in-configuration-manager-technical-preview"></a>Novità di Configuration Manager Technical Preview  
 Non sono state introdotte nuove funzionalità ibride nella versione di marzo 2016 di Configuration Manager Technical Preview.  

### <a name="new-in-configuration-manager-current-branch"></a>Novità di Configuration Manager (Current Branch)  
 Le seguenti nuove funzionalità introdotte in marzo 2016 sono disponibili nelle distribuzioni ibride con Intune e Configuration Manager (Current Branch) versione 1602. Queste funzionalità richiedono l'uso della console di Configuration Manager per la configurazione e la gestione.  

- **Criteri di configurazione delle app iOS**

  Nella versione 1602 di Configuration Manager (Current Branch) è possibile usare i criteri di configurazione delle app per specificare le impostazioni che potrebbero essere necessarie quando l'utente esegue un'app iOS. Per i dettagli, vedere [Configurare le app iOS con i criteri di configurazione in System Center Configuration Manager](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).  

- **Gestire le app iOS acquistate con Volume Purchase Program**

  Nella versione 1602 di Configuration Manager (Current Branch) è possibile distribuire e gestire le app acquistate con Volume Purchase Program (VPP) di Apple importando le informazioni di licenza dall'App Store e verificando il numero di licenze usate. Per informazioni dettagliate, vedere [Gestire le app iOS acquistate tramite Volume Purchase Program con System Center Configuration Manager](/sccm/apps/deploy-use/manage-volume-purchased-ios-apps).  

- **Creazione automatica di app di Office per dispositivi mobili**

  A partire dalla versione 1602 di Configuration Manager (Current Branch) le seguenti app per dispositivi mobili di Microsoft Office per Android e iOS vengono create quando si esegue l'aggiornamento dalla versione 1511:  

  -   Microsoft Word  
  -   Microsoft Excel  
  -   Microsoft PowerPoint  
  -   Microsoft OneDrive  
  -   Microsoft OneNote (solo iOS)  
  -   Microsoft Outlook  

  Queste app si trovano nel nodo Applicazioni della console di Configuration Manager. Per altre informazioni sulla distribuzione di applicazioni, vedere [Come distribuire le applicazioni con System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).  

- **Impostazioni della modalità tutto schermo per i dispositivi Android Samsung KNOX Standard**

  La modalità tutto schermo consente di bloccare un dispositivo per consentire solo l'uso di alcune funzionalità.  A partire dalla versione 1602 di Configuration Manager (Current Branch) è possibile specificare le impostazioni della modalità tutto schermo per i dispositivi Samsung KNOX Standard. Per informazioni dettagliate, vedere [Creare elementi di configurazione per dispositivi Android e Samsung KNOX Standard gestiti senza il client System Center Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client).  

- **Blocco attivazione di iOS**

  A partire dalla versione 1602 di Configuration Manager (Current Branch) è possibile gestire il blocco attivazione iOS, una funzionalità dell'app Trova il mio iPhone per dispositivi iOS 7.1 e versioni successive. Blocco attivazione viene abilitato automaticamente quando si usa l'app Trova il mio iPhone in un dispositivo.  Per informazioni dettagliate, vedere [Gestire il blocco attivazione iOS con System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock#bypass-activation-lock).  



<!--HONumber=Dec16_HO3-->



---
title: Archivio delle novità della gestione di dispositivi mobili ibrida
titleSuffix: Configuration Manager
description: Archivio di funzionalità di gestione dei dispositivi mobili precedenti disponibili per le distribuzioni ibride con System Center Configuration Manager e Intune.
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 4c27b161-9eb7-4cdd-b469-d8eb27e71aea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 006580a7ae4965ab4662ae02bee13ed9796697f8
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "71826253"
---
# <a name="past-hybrid-features-with-system-center-configuration-manager-and-microsoft-intune"></a>Funzionalità ibride precedenti con System Center Configuration Manager e Microsoft Intune

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo illustra le funzionalità di gestione dei dispositivi mobili (MDM) precedenti disponibili per le distribuzioni ibride con System Center Configuration Manager e Intune.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilità con le versioni di Configuration Manager  

 In ogni sezione di questo articolo vengono elencate le funzionalità ibride in 3 categorie diverse. Usare le indicazioni che seguono per determinare la compatibilità delle funzionalità di ogni categoria con versioni diverse di Configuration Manager:  

|Categorie di funzionalità|
|-|  
|**Novità di Microsoft Intune**: in generale, tutte le funzionalità elencate in questa categoria devono funzionare con tutte le versioni di Configuration Manager, incluse le versioni di System Center 2012 R2 Configuration Manager, poiché richiedono solo il servizio Intune e non richiedono altre funzionalità di Configuration Manager.<br /><br /> **Novità di Configuration Manager Technical Preview**: tutte le funzionalità elencate in questa categoria funzionano solo con la versione di Technical Preview specificata. Per provare queste funzionalità, è necessario installare la versione di Technical Preview specificata nella descrizione della funzionalità. Per altre informazioni, vedere [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) (Technical Preview per System Center Configuration Manager).<br /><br /> **Novità di Configuration Manager (Current Branch)** : tutte le funzionalità elencate in questa categoria funzionano solo con la versione di Configuration Manager (Current Branch) specificata, ad esempio la versione 1511 o 1602. Se si usa una versione precedente di Configuration Manager per la distribuzione ibrida, è necessario eseguire l'aggiornamento alla versione di Configuration Manager (Current Branch) specificata nella descrizione della funzionalità. Per altre informazioni, vedere [Upgrade to System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md) (Eseguire l'aggiornamento a System Center Configuration Manager).|  



## <a name="april-2017"></a>Aprile 2017

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

- **MyApps disponibile per Managed Browser**  
  Microsoft MyApps offre ora un supporto migliore all'interno di Managed Browser. Gli utenti di Managed Browser che non sono assegnati alla gestione passano direttamente al servizio MyApps, in cui possono accedere alle app SaaS con provisioning dell'amministratore. Gli utenti destinati alla gestione di Intune continuano ad accedere a MyApps dal segnalibro di Managed Browser incorporato.

- **Nuove icone per Managed Browser e il portale aziendale**  
  Managed Browser riceve icone aggiornate per le versioni sia Android che iOS dell'app. La nuova icona contiene il badge Intune aggiornato per renderla più coerente con altre app in Enterprise Mobility + Security (EM + S). È possibile visualizzare la nuova icona per Managed Browser nella [pagina delle novità dell'interfaccia utente dell'app Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

  Anche il portale aziendale riceve icone aggiornate per le versioni di Android, iOS e Windows dell'app per migliorare la coerenza con altre applicazioni in EM+S. Queste icone verranno rilasciate gradualmente per tutte le piattaforme da aprile alla fine di maggio.

- **Indicatore dello stato di accesso nel portale aziendale Android**  
  Un aggiornamento per l'app del portale aziendale Android mostra un indicatore dello stato di accesso quando l'utente avvia o riprende l'uso dell'app. L'indicatore attraversa nuovi stati, a partire da "Connessione in corso...", quindi "Accesso in corso..." e infine "Verifica dei requisiti di protezione..." prima di consentire all'utente di accedere all'app. È possibile visualizzare le nuove schermate per l'app Portale aziendale di Intune per Android nella [pagina delle novità dell'interfaccia utente dell'app Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Bloccare l'accesso delle app a SharePoint Online**  
  È ora possibile creare un criterio di accesso condizionale basato su app per bloccare l'accesso delle applicazioni, a cui non sono stati applicati criteri di protezione di app, a [SharePoint Online](https://docs.microsoft.com/intune-classic/deploy-use/mam-ca-for-sharepoint-online). Nello scenario di accesso condizionale basato su app, è possibile specificare le app che dovranno accedere a SharePoint Online usando il portale di Azure.

### <a name="new-in-configuration-manager-technical-preview-1704"></a>Novità di Configuration Manager Technical Preview 1704

- **Configurare le app Android con i criteri di configurazione delle app**  
  Quando un utente esegue un'app in un dispositivo Android for Work, è possibile usare i criteri di configurazione delle app in Configuration Manager per distribuire impostazioni preconfigurate. I criteri di configurazione delle app per Android sono disponibili solo nei dispositivi che eseguono Android for Work e riguardano le app approvate per lo store Play for Work. Per altre informazioni, vedere [Configurare le app Android con i criteri di configurazione delle app](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies).



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
  Se è necessario scaricare e trasferire localmente l'app Portale aziendale di Windows 10, è ora disponibile uno script per semplificare e ottimizzare il processo di firma dell'app per l'organizzazione. Per scaricare lo script e le relative istruzioni d'uso, vedere [Microsoft Intune Signing Script for Windows 10 Company Portal](https://aka.ms/win10cpscript) (Script di firma di Microsoft Intune per l'app Portale aziendale di Windows 10) nella raccolta TechNet. Per altre informazioni su questo annuncio, vedere [Updating your Windows 10 Company Portal app](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) (Aggiornamento dell'app Portale aziendale per Windows 10) nel blog del team di supporto di Intune.

- **Supporto migliorato per gli utenti Android in Cina**  
  A causa dell'assenza di Google Play Store in Cina, i dispositivi Android devono ottenere le app da marketplace cinesi. L'app Portale aziendale supporta questo flusso di lavoro, reindirizzando gli utenti Android in Cina per scaricare le app Portale aziendale e Outlook da App Store locali. Questo comportamento consente di migliorare l'esperienza utente quando sono abilitati i criteri di accesso condizionale, per la gestione sia dei dispositivi mobili che delle relative applicazioni. Le app Portale aziendale e Outlook per Android sono disponibili negli app store cinesi seguenti:

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

- **Verificare che le app Portale aziendale siano aggiornate**  
  Nel mese di dicembre 2016 è stato rilasciato un aggiornamento che imponeva l'uso di Multi-Factor Authentication (MFA) a un gruppo di utenti che registrano un dispositivo iOS, Android, Windows 8.1+ o Windows Phone 8.1+. Questa funzionalità non può essere usata senza determinate versioni di base dell'app Portale aziendale per Android (5.0.3419.0+) e iOS (2.1.17+).

  Le funzionalità di gestione di Intune sono in continua evoluzione. Molti miglioramenti sono accompagnati da aggiornamenti alle app Portale aziendale su tutte le piattaforme supportate. È consigliabile mantenere installate nei dispositivi le versioni più recenti delle app Portale aziendale. In tal modo, è possibile sfruttare i vantaggi offerti dai miglioramenti di Intune e garantire un'esperienza utente ottimale.

  >[!Tip]
  > Chiedere agli utenti di impostare i dispositivi in modo da aggiornare automaticamente le app dall'app store appropriato. Se si è resa disponibile l'app Portale aziendale per Android su una condivisione di rete, è possibile scaricare la versione più recente dall'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=49140).

- **Microsoft Teams è ora abilitato per MAM su iOS e Android**  
  Nelle app Microsoft Teams per iOS e Android sono ora abilitate le funzionalità di gestione delle app mobili (MAM, Mobile App Management) di Intune. È possibile consentire ai team di passare liberamente da un dispositivo all'altro, garantendo la protezione delle conversazioni e dei dati aziendali. Per altre informazioni, vedere [l'annuncio relativo a Microsoft Teams](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/) nel blog di Enterprise Mobility + Security.

### <a name="new-in-configuration-manager-technical-preview-1703"></a>Novità di Configuration Manager Technical Preview 1703

- **Supporto aggiuntivo per scenari VPP (Volume Purchase Program) di Apple**  
   A partire da Technical Preview 1703 è disponibile il supporto per gli scenari VPP (Volume Purchase Program) seguenti:

   - Licenze per dispositivi: le app che supportano le licenze per dispositivi e vengono distribuite in raccolte di dispositivi richiedono ora una sola licenza per ogni dispositivo. In precedenza, era necessario usare una licenza per ogni utente in un dispositivo. Per altre informazioni, vedere [Distribuire app iOS acquistate con Volume Purchase Program a raccolte di dispositivi](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections).
   - Uso di più token VPP per un tenant singolo ibrido con entrambi i token usati per gestire le app VPP.
   - Uso di token per istituti di istruzione VPP con la possibilità di distinguere tra i token aziendali e di istituti di istruzione.

### <a name="new-in-configuration-manager-current-branch"></a>Novità di Configuration Manager (Current Branch)

Le funzionalità seguenti erano precedentemente disponibili nelle versioni di Configuration Manager Technical Preview. Ora sono disponibili nelle distribuzioni ibride con Intune e Configuration Manager (Current Branch) versione 1702.

- [Supporto di Android for Work](/sccm/core/plan-design/changes/whats-new-in-version-1702##android-for-work-support)
- [Impostazioni di conformità di app non conformi](/sccm/core/plan-design/changes/whats-new-in-version-1702#conditional-access-device-compliance-policy-improvements)
- [Creazione e distribuzione del certificato PFX e supporto per S/MIME](/sccm/core/plan-design/changes/whats-new-in-version-1702#mobile-device-management)
- [Non è più necessario specificare le versioni di Android e iOS nella creazione guidata della gestione ibrida dei dispositivi mobili](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)

Nella versione 1702 di Configuration Manager (Current Branch) sono disponibili anche le funzionalità ibride aggiuntive seguenti:

- **Supporto migliorato per Volume Purchase Program (VPP) di Apple**  
  - È ora possibile distribuire app con licenza sia ai dispositivi che agli utenti. In base alla capacità dell'app di supportare la gestione delle licenze dei dispositivi, al momento della distribuzione viene richiesta una licenza appropriata, come indicato di seguito:

    | Versione di Configuration Manager | Gestione delle licenze dei dispositivi supportata | Tipo di raccolta della distribuzione | Licenza richiesta |
    |-|-|-|-|
    |Precedente la 1702|Yes|utente|Licenza utente|
    |Precedente la 1702|No|utente|Licenza utente|
    |Precedente la 1702|Yes|Dispositivo|Licenza utente|
    |Precedente la 1702|No|Dispositivo|Licenza utente|
    |1702 e versioni successive|Yes|utente|Licenza utente|
    |1702 e versioni successive|No|utente|Licenza utente|
    |1702 e versioni successive|Yes|Dispositivo|Licenza dispositivo|
    |1702 e versioni successive|No|Dispositivo|Licenza utente|

  - È ora possibile anche distribuire e tenere traccia delle app acquistate tramite iOS Volume Purchase Program for Education.

  - È ora possibile associare a Configuration Manager più token di Volume Purchase Program di Apple.

  Per altre informazioni sulle app iOS acquistate tramite Volume Purchase Program, vedere [Gestire le app iOS acquistate tramite Volume Purchase Program](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

- **Supporto per app line-of-business in Microsoft Store per le aziende**  
  È ora possibile sincronizzare app line-of-business personalizzate da Microsoft Store per le aziende.

- **Nuovi strumenti di monitoraggio Mobile Threat Defense**  
    Sono ora disponibili nuovi strumenti per il monitoraggio dello stato di conformità con il provider di servizi Mobile Threat Defense.

    Per altre informazioni, vedere [Monitorare la conformità a Mobile Threat Defense](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance).





## <a name="february-2017"></a>Febbraio 2017

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

- **Modernizzazione del sito Web del portale aziendale**

  Il sito Web del portale aziendale supporta app rivolte agli utenti che non hanno dispositivi gestiti. Il sito Web si allinea ad altri prodotti e servizi Microsoft usando una nuova combinazione di colori a contrasto, illustrazioni dinamiche e un "menu hamburger" che contiene i dettagli di contatto del supporto tecnico e le informazioni sui dispositivi gestiti esistenti. La pagina di destinazione è stata riorganizzata per evidenziare le app a disposizione degli utenti, con sequenze per le app in evidenza e aggiornate di recente. Nella pagina [UI updates](https://docs.microsoft.com/intune/whats-new-app-ui) (Aggiornamenti dell'interfaccia utente) sono disponibili immagini precedenti e successive all'aggiornamento.

- **Nuovo indirizzo del server MDM per dispositivi Windows**

  L'indirizzo del server MDM per la registrazione dei dispositivi Windows e Windows Phone è cambiato da manage.microsoft.com a enrollment.manage.microsoft.com. Comunicare agli utenti di usare enrollment.manage.microsoft.com come indirizzo del server MDM, se richiesto, durante la registrazione di un dispositivo Windows o Windows Phone. Questo aggiornamento richiede anche la sostituzione di qualsiasi CNAME in DNS che reindirizza EnterpriseEnrollment.contoso.com a manage.microsoft.com con un CNAME in DNS che reindirizzi EnterpriseEnrollment.contoso.com a EnterpriseEnrollment-s.manage.microsoft.com. Per altre informazioni su questa modifica, vedere https://aka.ms/intuneenrollsvrchange.

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

  Quando i dispositivi degli utenti perdono il contatto con Intune, è possibile assegnare loro nuove istruzioni per la risoluzione dei problemi, in modo che possano riottenere l'accesso alle risorse aziendali. Vedere [Devices are inactive, or the admin console cannot communicate with them](https://docs.microsoft.com/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cant-communicate-with-them) (I dispositivi sono inattivi o la console di amministrazione non può comunicare con loro).

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Novità di Configuration Manager Technical Preview 1701

- **Non è più necessario specificare le versioni di Android e iOS nella creazione guidata della gestione ibrida dei dispositivi mobili**

  A partire dalla Technical Preview 1701 per la gestione ibrida dei dispositivi mobili, non è più necessario indicare versioni specifiche di Android e iOS quando si creano nuovi criteri e profili per i dispositivi gestiti in Intune. Con questa modifica, le distribuzioni ibride possono offrire il supporto più rapidamente per le nuove versioni di Android e iOS, senza attendere una nuova versione o un'estensione di Configuration Manager. Per altre informazioni, vedere [Non è più necessario specificare le versioni di Android e iOS nella creazione guidata](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).



## <a name="december-2016"></a>Dicembre 2016

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

- **Multi-Factor Authentication al momento dell'iscrizione è stato trasferito nel portale di Azure**

  In precedenza, per impostare Multi-Factor Authentication per le registrazioni di Intune si accedeva alla console di Intune o alla console di Configuration Manager. Con questa funzionalità aggiornata, è ora possibile accedere al [portale di Microsoft Azure](https://manage.windowsazure.com) usando le credenziali di Intune e configurare le impostazioni dell'autenticazione a più fattori tramite Azure ad. Per altre informazioni, vedere [Multi-Factor Authentication per Microsoft Intune](https://aka.ms/mfa_ad).

- **App Portale aziendale per Android ora disponibile in Cina**

  L'app Portale aziendale per Android è ora disponibile in Cina. A causa dell'assenza di Google Play Store in Cina, i dispositivi Android devono ottenere le app da marketplace di app cinesi. L'app Portale aziendale per Android è disponibile per il download negli store seguenti:

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)

  L'app Portale aziendale per Android usa Google Play Services per comunicare con il servizio Microsoft Intune. Poiché Google Play Services non è ancora disponibile in Cina, per eseguire una delle attività seguenti possono essere necessarie fino a 8 ore.

  | Console di amministrazione di Configuration Manager | App Portale aziendale di Intune per Android | Sito Web dell'app Portale aziendale di Intune |
  |----|----|----|
  | Disattiva/Cancella (rimuovere tutti i dati)| Rimuovere un dispositivo remoto | Rimuovi dispositivo (locale e remoto) |
  | Disattiva/Cancella (rimuovere i dati aziendali)| Reimposta dispositivo | Reimposta dispositivo|
  | Distribuzioni di app nuove o aggiornate | Installare le app line-of-business disponibili | Reimpostazione del passcode del dispositivo|
  | Blocco remoto| | |
  | Reimpostazione del passcode | | |


## <a name="november-2016"></a>Novembre 2016

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

- **Nuova app Portale aziendale di Microsoft Intune disponibile per dispositivi Windows 10**

  Microsoft ha rilasciato una nuova [app Portale aziendale per dispositivi Windows 10](https://www.microsoft.com/store/apps/9wzdncrfj3pz). Questa app, basata sul nuovo formato universale di Windows 10, offre un'innovativa esperienza utente comune a tutti i dispositivi Windows 10, siano essi PC o dispositivi mobili, pur mantenendo le stesse funzionalità disponibili nella versione precedente dell'app Portale aziendale.

  La nuova app integra funzionalità specifiche della piattaforma, come l'accesso Single Sign-On (SSO) e l'autenticazione basata su certificati nei dispositivi Windows 10. L'app è disponibile come aggiornamento dell'app Portale aziendale per Windows 8.1 e dell'app Portale aziendale di Windows Phone 8.1 e può essere installata da Windows Store. Per altre informazioni, vedere [Intune Support Team Blog](https://aka.ms/intunecp_universalapp) (Blog del team di supporto Intune).

  La nuova app Portale aziendale consente anche di visualizzare qualsiasi applicazione di Windows Store per le aziende contrassegnata come **Disponibile** nella console di Configuration Manager.


### <a name="new-in-configuration-manager-current-branch"></a>Novità di Configuration Manager (Current Branch)

Le funzionalità seguenti, che in precedenza erano disponibili nelle versioni di Configuration Manager Technical Preview, sono ora disponibili nelle distribuzioni ibride con Intune e Configuration Manager (Current Branch) versione 1610.

* [Impostazioni aggiuntive e prestazioni migliorate per elementi di Configuration Manager](/sccm/core/plan-design/changes/whats-new-in-version-1610#new-compliance-settings-for-configuration-items)
* [Impostazioni aggiuntive per i profili DEP](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [App a pagamento in Windows Store per le aziende](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)
* [Tipi di connessione nativa per i profili VPN di Windows 10](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Grafici di conformità di Intune](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)
* [Richiesta di sincronizzazione dei criteri dalla console](/sccm/mdm/deploy-use/sync-intune-device)
* [Impostazioni di configurazione di Windows Defender](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client#windows-defender)

Nella versione 1610 di Configuration Manager (Current Branch) sono disponibili anche le funzionalità ibride aggiuntive seguenti:

- **Aumento del numero di dispositivi registrati**

  È ora possibile consentire agli utenti di registrare fino a 15 dispositivi. In precedenza, il limite era di 5 dispositivi per utente.


- **Supporto di sicurezza aggiuntivo**

  Oltre al ruolo Amministratore completo, anche i ruoli di sicurezza incorporati seguenti hanno ora l'accesso completo agli elementi nel nodo Tutti i dispositivi di proprietà dell'azienda, inclusi i dispositivi predichiarati, i profili di registrazione iOS e i profili di registrazione Windows:

    - Gestione asset
    - Gestione accesso risorse aziendali

  A queste aree della console di Configuration Manager continua a essere concesso l'accesso in sola lettura al ruolo Analista di sola lettura.

- **Attivazione automatica dell'accesso VPN dalle app Windows Information Protection di Windows**

  È possibile aggiungere un dominio principale di Windows Information Protection a profili VPN di Windows 10 in modo che tutte le app associate attivino automaticamente una connessione VPN nel momento in cui vengono eseguite sul dispositivo. Questa opzione è disponibile solo se si sceglie un tipo di connessione nativa.

- **Accesso condizionale per profili VPN di Windows 10**

    È ora possibile richiedere la conformità dei dispositivi Windows 10 registrati in Azure Active Directory per poter ottenere l'accesso alla rete VPN tramite i profili VPM di Windows 10 creati nella console di Configuration Manager. Per disporre di questa funzionalità, selezionare la casella di controllo **Abilita l'accesso condizionale per questa connessione VPN** nella pagina Metodo di autenticazione della procedura di creazione guidata del profilo VPN e nelle proprietà dei profili VPN di Windows 10. Questa opzione è disponibile solo se si sceglie un tipo di connessione nativa.

    Se si abilita l'accesso condizionale per il profilo, è anche possibile specificare un certificato separato per l'autenticazione Single Sign-On.

## <a name="october-2016"></a>Ottobre 2016

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

Le seguenti funzionalità di Intune introdotte in ottobre 2016 funzionano nelle distribuzioni ibride.

- **Accesso condizionale per la gestione di applicazioni per dispositivi mobili**

  È possibile limitare l'accesso a Exchange Online in modo che possa essere eseguito solo dalle app che supportano i criteri di gestione delle applicazioni mobili di Intune, ad esempio Outlook. [Questa nuova funzionalità](/intune/deploy-use/allow-policy-managed-apps-access-to-o365) si combina perfettamente con i criteri di gestione MAM di Intune poiché è possibile bloccare l'accesso ai client di posta predefiniti o ad altre applicazioni che non sono state configurate con i criteri MAM di Intune. In questo modo gli utenti accedono ai dati dell'organizzazione con applicazioni che possono essere protette usando MAM di Intune. È possibile iniziare a usare la gestione delle app per dispositivi mobili di Intune dal portale di Azure. Cercare la nuova sezione relativa all'accesso condizionale nel pannello "Impostazioni".

- **Strumento per la disposizione testo per app di Intune per Android**

  È possibile abilitare le app per l'uso dei criteri di gestione delle applicazioni per dispositivi mobili (MAM) di Intune usando lo strumento per la disposizione testo per app di Intune.

- **Compatibilità di Android Samsung KNOX Standard con Intune**

  Alcuni modelli di telefoni Samsung Galaxy Ace non possono essere gestiti da Intune come dispositivi Samsung KNOX Standard. Quando vengono registrati con Intune, questi dispositivi verranno invece gestiti come dispositivi Android standard.

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

## <a name="september-2016"></a>Settembre 2016

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

  Se si usano profili o elementi di configurazione destinati a tutte le piattaforme iOS, verranno inseriti in iOS 10. È stato anche rilasciato un aggiornamento di Configuration Manager versione 1606 che consente di destinare i profili e gli elementi di configurazione a singole piattaforme iOS tra cui iOS 10. È possibile installare l'aggiornamento con la console di amministrazione di Configuration Manager da **Amministrazione > Panoramica > Servizi cloud > Aggiornamenti e manutenzione**. Altre informazioni sull'aggiornamento sono disponibili all'indirizzo [https://support.microsoft.com/kb/3192616](https://support.microsoft.com/kb/3192616).

## <a name="august-2016"></a>Agosto 2016

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

Le seguenti funzionalità di Intune introdotte in agosto 2016 funzionano nelle distribuzioni ibride.

- **Supporto per Android 7 nell'app Portale aziendale**

  L'app Portale aziendale di Intune per Android offre il supporto "giorno 0" per il sistema operativo Android 7.0 per dispositivi mobili`che verrà introdotto prossimamente.

- **Rimozione da parte di Google della funzionalità di reimpostazione remota del passcode nei dispositivi Android 7.0**

  Google sta eliminando la possibilità per amministratori IT e utenti finali di reimpostare in modalità remota il passcode dei dispositivi Android 7.0. In precedenza gli amministratori IT potevano reimpostare il passcode di un utente in modalità remota e gli utenti finali potevano reimpostare i propri passcode dal sito Web del portale aziendale.

- **Criteri per app consentite e bloccate per i dispositivi Samsung KNOX Standard**

  È ora possibile configurare per i dispositivi Samsung KNOX Standard criteri personalizzati che consentono di creare uno degli elementi seguenti:

  - Un elenco di app la cui esecuzione è bloccata sul dispositivo. Anche se installata, un'app definita nell'elenco delle app bloccate non può essere attivata sul dispositivo.
  - Un elenco di app che gli utenti del dispositivo sono autorizzati a installare da Google Play Store. Non sarà possibile installare altre app dallo Store.

  Queste impostazioni possono essere usate solo dai dispositivi con Samsung KNOX Standard. Per informazioni dettagliate, vedere [Usare criteri personalizzati per consentire e bloccare app per dispositivi Samsung KNOX Standard](/intune/deploy-use/custom-policy-to-allow-and-block-samsung-knox-apps).

- **Collegamento per invio del feedback dal Portale aziendale a Microsoft**

   Il sito Web del portale aziendale consente agli utenti di toccare il nuovo collegamento "Commenti e suggerimenti" nella parte inferiore della pagina, per inviare un feedback a Microsoft sulla propria esperienza con il sito. I commenti, raccolti in forma anonima, consentiranno a Microsoft di migliorare l'esperienza degli utenti con il sito Web del portale aziendale.

- **Versione minima di Managed Browser per iOS aggiornata a 8.0**

  L'app Microsoft Intune Managed Browser per iOS è stata aggiornata in modo da supportare i dispositivi che eseguono iOS 8.0 o versioni successive. Anche se i dispositivi iOS 7.1 possono continuare a usare l'app Managed Browser esistente, suggerire agli utenti di aggiornare iOS alla versione 8.0 o successiva per accedere e usufruire di tutte le nuove funzionalità di Managed Browser.

### <a name="new-in-configuration-manager-technical-preview"></a>Novità di Configuration Manager Technical Preview

Non sono state introdotte nuove funzionalità ibride nella versione di agosto 2016 di Configuration Manager Technical Preview.

### <a name="new-in-configuration-manager-current-branch"></a>Novità di Configuration Manager (Current Branch)

Non sono state introdotte nuove funzionalità ibride nella versione di agosto 2016 di Configuration Manager (Current Branch).

## <a name="july-2016"></a>Luglio 2016

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

Le seguenti funzionalità di Intune introdotte in luglio 2016 funzionano nelle distribuzioni ibride.

- **È disponibile Xamarin SDK per le app di Intune**

  Il componente Xamarin SDK per app di Intune consente di abilitare le funzionalità di gestione delle app per dispositivi mobili di Intune nelle app per dispositivi mobili iOS e Android compilate con Xamarin. Il componente è disponibile nell'[archivio Xamarin](https://components.xamarin.com/view/Microsoft.Intune.MAM) o nella [pagina GitHub di Microsoft Intune](https://github.com/msintuneappsdk).

- **Esperienza utente finale migliorata durante la registrazione dei dispositivi Windows**

  Quando si utilizza l'accesso condizionale, la procedura di registrazione per Windows 8.1, Windows 10 Desktop e 10 Windows Mobile è illustrata nel sito Web del portale aziendale. Gli utenti ora vedono passaggi separati per la **registrazione del dispositivo** e l'**aggiunta all'area di lavoro** quindi è più semplice verificare lo stato del dispositivo e completare il processo nel caso in cui l'aggiunta all'area di lavoro abbia esito negativo. Si prevede che la separazione dei passaggi semplifichi anche il processo di risoluzione dei problemi per gli amministratori IT. In precedenza, quando gli utenti finali tentavano di eseguire la registrazione e tutti i passaggi, tranne l'aggiunta all'area di lavoro, venivano completati correttamente, il dispositivo non appariva nell'elenco dei dispositivi per l'identificazione e questo causava confusione per gli utenti.

  - **Cancellazione completa ora disponibile per i dispositivi Windows 10**

    I computer desktop e portatili Windows 10 registrati come dispositivi mobili possono essere cancellati per ripristinare le impostazioni di fabbrica del dispositivo. Per altre informazioni, vedere le istruzioni per [proteggere i dispositivi con la cancellazione remota](/sccm/mdm/deploy-use/wipe-lock-reset-devices).

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

* Trovare, gestire e distribuire app di Windows Store per le aziende per i dispositivi Windows 10 dalla console di Configuration Manager ([1604](#new-in-1604-technical-preview))
* Impostazione di Smart Lock per dispositivi Android ([1604](#new-in-1604-technical-preview))
* VPN attivata dall'app per dispositivi Windows 10 ([1605](#new-in-1605-technical-preview))
* Nuova esperienza per le azioni dei dispositivi remoti ([1605](#new-in-1605-technical-preview))
* App di Windows Store per le aziende ([1605](#new-in-1605-technical-preview))
* Miglioramenti generali per le app acquistate con Volume Purchase Program ([1605](#new-in-1605-technical-preview))
* Windows Information Protection (WIP) ([1605](#new-in-1605-technical-preview))
* Predichiarazione dei dispositivi di proprietà dell'azienda con numero di serie IMEI o iOS ([1605](#new-in-1605-technical-preview))
* Categorizzazione automatica dei dispositivi in raccolte ([1606](#new-in-1606-technical-preview))

Per informazioni sulle nuove funzionalità, vedere la documentazione relativa alla versione di Technical Preview specificata.

## <a name="june-2016"></a>Giugno 2016

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune
Le seguenti funzionalità di Intune introdotte in giugno 2016 funzionano nelle distribuzioni ibride.

- **Stato del servizio Intune**: le informazioni sullo stato del servizio per Intune sono state spostate in una posizione centrale con altri servizi Microsoft. Queste informazioni sono ora disponibili nell'interfaccia di amministrazione di Microsoft 365 in integrità del servizio. Per altre informazioni, vedere questo [post di blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/04/28/intune-service-health-is-now-available-in-the-office-365-portal/).

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

  È possibile creare categorie di dispositivi da usare per inserire automaticamente i dispositivi in raccolte quando si usa Configuration Manager con Intune. Agli utenti verrà quindi richiesto di scegliere una categoria di dispositivo quando eseguono la registrazione di un dispositivo in Intune. È anche possibile modificare la categoria di un dispositivo dalla console di Configuration Manager. Per altre informazioni, vedere [Categorizzazione automatica dei dispositivi in raccolte](/sccm/core/get-started/capabilities-in-technical-preview-1606#dmp_category) in [Funzionalità di Technical Preview 1606 per System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1606).

  > [!IMPORTANT]
  > Questa funzionalità può essere usata con la versione di Microsoft Intune di giugno 2016. Verificare che l'installazione sia aggiornata a questa versione prima di tentare queste procedure.

### <a name="new-in-configuration-manager-current-branch"></a>Novità di Configuration Manager (Current Branch)
Non sono state introdotte nuove funzionalità ibride nella versione di giugno 2016 di Configuration Manager (Current Branch).

##  <a name="may-2016"></a>Maggio 2016  

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

  Per altre informazioni, vedere [Nuova esperienza per le azioni dei dispositivi remoti](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_Remote) in [Funzionalità di Technical Preview 1605 per System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **App di Windows Store per le aziende**

  In [Windows Store per le aziende](https://www.microsoft.com/business-store) è possibile trovare e acquistare app per l'organizzazione, singolarmente o con Volume Purchase Program. Connettendo lo Store a Configuration Manager, è possibile gestire le app acquistate con Volume Purchase Program dalla console di Configuration Manager. Per altre informazioni, vedere la sezione sulle [app disponibili in Windows Store per le aziende](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_WSFB) in [Funzionalità di Technical Preview 1605 per System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Miglioramenti generali per le app acquistate con Volume Purchase Program**

  Le app acquistate con Volume Purchase Program da Windows Store per le aziende e dall'App Store di iOS sono state consolidate nella vista delle **informazioni sulle licenze per le app dello Store**. È stato anche migliorato il modo in cui vengono create le app acquistate con Volume Purchase Program per iOS. Per altre informazioni, vedere [Miglioramenti generali per le app acquistate con Volume Purchase Program](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_VPP2) in [Funzionalità di Technical Preview 1605 per System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Predichiarare i dispositivi di proprietà dell'azienda con numero di serie IMEI o iOS**

  È ora possibile identificare i dispositivi di proprietà dell'azienda importando i relativi codici IMEI (International station Mobile Equipment Identity). È possibile caricare un file con valori separati da virgola (CSV) contenente i codici IMEI o immettere manualmente le informazioni relative ai dispositivi.  Possono essere importati i numeri di serie anche per i dispositivi iOS.  Per altre informazioni, vedere [Predichiarare i dispositivi di proprietà dell'azienda con numero di serie IMEI o iOS](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_IMEI) in [Funzionalità di Technical Preview 1605 per System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Windows Information Protection (WIP)**

  È possibile creare elementi di configurazione che consentono di distribuire i criteri di Windows Information Protection (WIP), ad esempio consentono di scegliere le app protette, il livello di protezione WIP e come trovare i dati aziendali in rete. Per altre informazioni su WIP, vedere gli argomenti seguenti:  

  -   [Proteggere i dati aziendali con Windows Information Protection (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [Creare e distribuire un criterio di Windows Information Protection (WIP) con System Center Configuration Manager](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### <a name="new-in-configuration-manager-current-branch"></a>Novità di Configuration Manager (Current Branch)  
 Non sono state introdotte nuove funzionalità ibride nella versione di maggio 2016 di Configuration Manager (Current Branch).  

##  <a name="april-2016"></a>Aprile 2016  

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


  In Configuration Manager Technical Preview 1604 è disponibile il supporto per Windows Store per le aziende, che consente di trovare, gestire e distribuire le app ai dispositivi Windows 10 gestiti dall'utente. Per informazioni dettagliate, vedere la sezione [Gestire le app acquistate con Volume Purchase Program da Windows Store per le aziende](/sccm/core/get-started/capabilities-in-technical-preview-1604#BKMK_WindowsVPP) in [Funzionalità di Technical Preview 1604 per System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604).  

- **Impostazione di Smart Lock per dispositivi Android**

  È stata aggiunta all'elemento di configurazione Android e Samsung KNOX Standard una nuova impostazione che consente di controllare la funzionalità Smart Lock sui dispositivi Android compatibili.  È possibile usare questa impostazione per impedire agli utenti finali di configurare Smart Lock. Vedere [Impostazione di SmartLock per dispositivi Android](/sccm/core/get-started/capabilities-in-technical-preview-1604#BKMK_Smart) in [Funzionalità di Technical Preview 1604 per System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604).  

### <a name="new-in-configuration-manager-current-branch"></a>Novità di Configuration Manager (Current Branch)  
 Non sono state introdotte nuove funzionalità ibride nella versione di aprile 2016 di Configuration Manager (Current Branch).  

##  <a name="march-2016"></a>Marzo 2016  

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

  Nella versione 1602 di Configuration Manager (Current Branch) è possibile usare i criteri di configurazione delle app per specificare le impostazioni che potrebbero essere necessarie quando l'utente esegue un'app iOS. Per informazioni dettagliate, vedere [Configure iOS apps with app configuration policies in System Center Configuration Manager](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies) (Configurare le app iOS con i criteri di configurazione in System Center Configuration Manager).  

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



## <a name="notices"></a>Notifiche

### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 e System Center 2012 R2 Configuration Manager (RTM): il supporto per la gestione ibrida di dispositivi mobili termina il 10 aprile 2017
*11 gennaio 2017*

Il supporto per System Center 2012 Configuration Manager SP1 e System Center 2012 R2 Configuration Manager RTM è terminato il 12 luglio 2016. Per quanto riguarda la connessione di queste versioni al servizio Microsoft Intune per la gestione ibrida di dispositivi mobili, il supporto termina il 10 aprile 2017. Dopo tale data, la gestione ibrida di dispositivi mobili non sarà più disponibile con queste versioni. In pratica, i dispositivi gestiti non saranno più gestiti poiché il connettore Intune non si connetterà più al servizio Intune. I dati di Configuration Manager, ad esempio criteri e applicazioni, non verranno propagati a Intune e i dati dei dispositivi gestiti non verranno propagati a Configuration Manager finché non verrà eseguito un aggiornamento.

Se si esegue una distribuzione ibrida con Configuration Manager 2012 SP1 o R2 RTM, è consigliabile eseguire l'aggiornamento a Configuration Manager (Current Branch) o al Service Pack supportato più recente per Configuration Manager 2012 (R2 SP1 o SP2) prima del 10 aprile 2017 per evitare l'interruzione del servizio.

Risorse aggiuntive:
- [Eseguire l'aggiornamento a System Center Configuration Manager (Current Branch)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
- [Pianificazione dell'aggiornamento a System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
- [Pianificazione dell'aggiornamento a System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Il caricamento del portale aziendale per Windows Phone 8 è deprecato
*25 ottobre 2016*

L'opzione che consente di caricare un'app Portale aziendale firmata è stata rimossa dalla console di Configuration Manager, poiché il supporto di Intune viene deprecato per Windows 8, Windows Phone 8 e Windows RT e il supporto per il portale aziendale per Windows Phone 8 termina in novembre.  I dispositivi Windows 8, Windows Phone 8 e Windows RT che sono già registrati continueranno a essere supportati, ma la registrazione di dispositivi aggiuntivi con queste piattaforme non sarà più supportata.

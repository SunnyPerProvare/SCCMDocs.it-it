---
title: "Novità della gestione ibrida di dispositivi mobili con Configuration Manager | Microsoft Docs"
description: "Informazioni sulle nuove funzionalità di gestione dei dispositivi mobili disponibili per le distribuzioni ibride con Configuration Manager e Intune."
ms.custom: na
ms.date: 04/21/2017
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
ms.translationtype: Human Translation
ms.sourcegitcommit: ae008c91a7387ba76f2bfac13f8feb489a0cc558
ms.openlocfilehash: 0af5ae68353fcf1db846e2e27f3391fe87dcfc42
ms.contentlocale: it-it
ms.lasthandoff: 04/21/2017

---
# <a name="whats-new-in-hybrid-mobile-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Novità della gestione ibrida di dispositivi mobili con System Center Configuration Manager e Microsoft Intune

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo illustra le nuove funzionalità di gestione dei dispositivi mobili (MDM) disponibili per le distribuzioni ibride con System Center Configuration Manager e Intune.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilità con le versioni di Configuration Manager  

 In ogni sezione di questo articolo vengono elencate le funzionalità ibride in 3 categorie diverse. Usare le indicazioni che seguono per determinare la compatibilità delle funzionalità di ogni categoria con versioni diverse di Configuration Manager:  

|Categorie di funzionalità|Descrizione|
|-|-|
|**Novità di Microsoft Intune** | In generale, tutte le funzionalità elencate in questa categoria devono funzionare con tutte le versioni di Configuration Manager, incluse le versioni di System Center 2012 R2 Configuration Manager, poiché richiedono solo il servizio Intune e non richiedono altre funzionalità di Configuration Manager.|
|**Novità di Configuration Manager Technical Preview**| Tutte le funzionalità elencate in questa categoria funzionano solo con la versione di Technical Preview specificata. Per provare queste funzionalità, è necessario installare la versione di Technical Preview specificata nella descrizione della funzionalità. Per altre informazioni, vedere [Technical Preview per System Center Configuration Manager](../../core/get-started/technical-preview.md).|
|**Novità di Configuration Manager (Current Branch)**| Tutte le funzionalità elencate in questa categoria funzionano solo con la versione di Configuration Manager (Current Branch) specificata, ad esempio la versione 1511 o 1602. Se si usa una versione precedente di Configuration Manager per la distribuzione ibrida, è necessario eseguire l'aggiornamento alla versione di Configuration Manager (Current Branch) specificata nella descrizione della funzionalità. Per altre informazioni, vedere l'articolo relativo agli [aggiornamenti a System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|

## <a name="april-2017"></a>Aprile 2017

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

- **MyApps disponibile per Managed Browser**

  Microsoft MyApps offre ora un supporto migliore all'interno di Managed Browser. Gli utenti di Managed Browser che non sono assegnati alla gestione passeranno direttamente al servizio MyApps, in cui potranno accedere alle app SaaS con provisioning dell'amministratore. Gli utenti assegnati alla gestione di Intune continueranno a poter accedere a MyApps dal segnalibro di Managed Browser incorporato.

- **Nuove icone per Managed Browser e il portale aziendale**

  Managed Browser riceve icone aggiornate per le versioni sia Android che iOS dell'app. La nuova icona conterrà il badge Intune aggiornato per renderla più coerente con altre app in Enterprise Mobility + Security (EM + S). È possibile visualizzare la nuova icona per Managed Browser nella [pagina delle novità dell'interfaccia utente dell'app Intune](/intune/whats-new/whats-new-in-intune-app-ui.md).

  Anche il portale aziendale riceve icone aggiornate per le versioni di Android, iOS e Windows dell'app per migliorare la coerenza con altre applicazioni in EM+S. Queste icone verranno rilasciate gradualmente tra piattaforme da aprile alla fine di maggio.

- **Indicatore dello stato di accesso nel portale aziendale Android**

  Un aggiornamento per l'app del portale aziendale Android mostra un indicatore dello stato di accesso quando l'utente avvia o riprende l'uso dell'app. L'indicatore attraversa nuovi stati, a partire da "Connessione in corso...", quindi "Accesso in corso..." e infine "Verifica dei requisiti di protezione..." prima di consentire all'utente di accedere all'app. È possibile visualizzare le nuove schermate per l'app Portale aziendale di Intune per Android nella [pagina delle novità dell'interfaccia utente dell'app Intune](/intune/whats-new/whats-new-in-intune-app-ui.md).

- **Bloccare l'accesso delle app a SharePoint Online**

  È ora possibile creare un criterio di accesso condizionale basato su app per bloccare l'accesso delle applicazioni, a cui non sono stati applicati criteri di protezione di app, a [SharePoint Online](/InTune/deploy-use/mam-ca-for-sharepoint-online). Nello scenario di accesso condizionale basato su app, è possibile specificare le app che dovranno accedere a SharePoint Online usando il portale di Azure.

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

  Per altre informazioni su queste modifiche, vedere [Aggiornamenti dell'interfaccia utente per le applicazioni degli utenti finali in Intune](/intune/whats-new/whats-new-in-intune-app-ui).

- **Script di firma per l'app Portale aziendale di Windows 10**

  Se è necessario scaricare e trasferire localmente l'app Portale aziendale di Windows 10, è ora disponibile uno script per semplificare e ottimizzare il processo di firma dell'app per l'organizzazione.  Per scaricare lo script e le relative istruzioni d'uso, vedere [Microsoft Intune Signing Script for Windows 10 Company Portal](https://aka.ms/win10cpscript) (Script di firma di Microsoft Intune per l'app Portale aziendale di Windows 10) nella raccolta TechNet. Per altre informazioni su questo annuncio, vedere [Updating your Windows 10 Company Portal app](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) (Aggiornamento dell'app Portale aziendale di Windows 10) nel blog del team di supporto di Intune.

- **Supporto migliorato per gli utenti Android in Cina**

  A causa dell'assenza di Google Play Store in Cina, i dispositivi Android devono ottenere le app da marketplace cinesi. L'app Portale aziendale supporterà questo flusso di lavoro reindirizzando gli utenti Android in Cina per scaricare le app Portale aziendale e Outlook da app store locali. Ciò consentirà di migliorare l'esperienza utente quando sono abilitati i criteri di accesso condizionale, per la gestione dei dispositivi e delle applicazioni mobili. Le app Portale aziendale e Outlook per Android sono disponibili negli app store cinesi seguenti:

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

   - Licenze per dispositivi - Le app che supportano le licenze per dispositivi e vengono distribuite in raccolte di dispositivi richiederanno una sola licenza per ogni dispositivo.  In precedenza, era necessario usare una licenza per ogni utente in un dispositivo. Per altre informazioni, vedere [Distribuire app iOS acquistate con Volume Purchase Program a raccolte di dispositivi](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections).
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

  - È ora possibile distribuire app con licenza sia ai dispositivi che agli utenti. In base alla possibilità dell'app di supportare la gestione delle licenze dei dispositivi, al momento della distribuzione verrà richiesta una licenza appropriata, come indicato di seguito:

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

  Il sito Web del portale aziendale supporta app rivolte agli utenti che non hanno dispositivi gestiti. Il sito Web si allinea ad altri prodotti e servizi Microsoft usando una nuova combinazione di colori a contrasto, illustrazioni dinamiche e un "menu hamburger" che contiene i dettagli di contatto del supporto tecnico e le informazioni sui dispositivi gestiti esistenti. La pagina di destinazione è stata riorganizzata per evidenziare le app a disposizione degli utenti, con sequenze per le app in evidenza e aggiornate di recente. Nella pagina [UI updates](/intune/whats-new/whats-new-in-intune-app-ui) (Aggiornamenti dell'interfaccia utente) sono disponibili immagini precedenti e successive all'aggiornamento.

- **Nuovo indirizzo del server MDM per dispositivi Windows**

  L'indirizzo del server MDM per la registrazione dei dispositivi Windows e Windows Phone è cambiato da manage.microsoft.com a enrollment.manage.microsoft.com. Comunicare agli utenti di usare enrollment.manage.microsoft.com come indirizzo del server MDM, se richiesto, durante la registrazione di un dispositivo Windows o Windows Phone. Questo aggiornamento richiede anche la sostituzione di qualsiasi CNAME in DNS che reindirizza EnterpriseEnrollment.contoso.com a manage.microsoft.com con un CNAME in DNS che reindirizzi EnterpriseEnrollment.contoso.com a EnterpriseEnrollment-s.manage.microsoft.com. Per altre informazioni su questa modifica, visitare http://aka.ms/intuneenrollsvrchange.

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Novità di Configuration Manager Technical Preview 1702

- **Supporto di Android for Work**

  È ora possibile gestire i dispositivi Android con Android for Work in ambienti ibridi MDM tramite Configuration Manager Technical Preview 1702. I dispositivi Android supportati possono ora essere registrati come dispositivi Android for Work, che crea un profilo di lavoro nel dispositivo a cui possono essere distribuite le app approvate in Play for Work. È possibile configurare e distribuire anche gli elementi di configurazione, i criteri di conformità e i profili di accesso alle risorse per questi dispositivi. Per altre informazioni, vedere [Supporto per Android for Work](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support).

- **Impostazioni di conformità di app non conformi**

  È ora possibile creare regole di app non conformi per app Android e iOS nei criteri di conformità. Se i dispositivi hanno le applicazioni specificate installate, queste verranno contrassegnate come "non conformi" e non avranno accesso alle risorse aziendali in base ai criteri di accesso condizionale in uso. Per altre informazioni, vedere [Miglioramento dei criteri di conformità dei dispositivi per l'accesso condizionale](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements).

- **Creazione e distribuzione del certificato PFX e supporto per S/MIME**

  È ora possibile creare e distribuire i certificati PFX agli utenti in un ambiente ibrido. Questi certificati possono essere quindi usati per la crittografia S/MIME della posta elettronica e la decrittografia da parte di dispositivi che l'utente ha registrato. Per altre informazioni, vedere [Creare certificati PFX con il supporto di S/MIME](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support).

- **Supporto per impostazioni di configurazione iOS aggiuntive**
   
    Sono ora disponibili 42 impostazioni iOS aggiuntive che è possibile configurare come parte di un elemento di configurazione. La maggior parte delle impostazioni, 35 in tutto, è stata aggiunta per dispositivi iOS con supervisione. Per altre informazioni, vedere [Nuove impostazioni di conformità per dispositivi iOS](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices).

## <a name="january-2017"></a>Gennaio 2017

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

- **Supporto di Android 7.1.1**

  Intune ora supporta e gestisce in modo completo Android 7.1.1.

- **Risolvere i problemi di inattività dei dispositivi iOS o di comunicazione tra la console di amministrazione e questi dispositivi**

  Quando i dispositivi degli utenti perdono il contatto con Intune, è possibile assegnare loro nuove istruzioni per la risoluzione dei problemi, in modo che possano riottenere l'accesso alle risorse aziendali. Vedere [Devices are inactive, or the admin console cannot communicate with them](/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them) (I dispositivi sono inattivi o la console di amministrazione non può comunicare con loro).

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Novità di Configuration Manager Technical Preview 1701

- **Non è più necessario specificare le versioni di Android e iOS nella creazione guidata della gestione ibrida dei dispositivi mobili**

  A partire dalla Technical Preview 1701 per la gestione ibrida dei dispositivi mobili, non è più necessario indicare versioni specifiche di Android e iOS quando si creano nuovi criteri e profili per i dispositivi gestiti in Intune. Con questa modifica, le distribuzioni ibride possono offrire il supporto più rapidamente per le nuove versioni di Android e iOS, senza attendere una nuova versione o un'estensione di Configuration Manager. Per altre informazioni, vedere [Non è più necessario specificare le versioni di Android e iOS nella creazione guidata](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).


## <a name="december-2016"></a>Dicembre 2016

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

- **Multi-Factor Authentication al momento dell'iscrizione è stato trasferito nel portale di Azure**

  In precedenza, per impostare Multi-Factor Authentication per le registrazioni di Intune si accedeva alla console di Intune o alla console di Configuration Manager. Con l'aggiornamento di questa funzionalità è ora possibile accedere al [portale di Microsoft Azure] (https://manage.windowsazure.com) usando le credenziali di Intune e configurare le impostazioni di Multi-Factor Authentication tramite Azure AD. Per altre informazioni, vedere [Multi-Factor Authentication for Microsoft Intune] (https://aka.ms/mfa_ad) (Multi-Factor Authentication per Microsoft Intune).

- **App Portale aziendale per Android ora disponibile in Cina**

  L'app Portale aziendale per Android è ora disponibile in Cina. A causa dell'assenza di Google Play Store in Cina, i dispositivi Android devono ottenere le app da marketplace di app cinesi. L'app Portale aziendale per Android è disponibile per il download negli store seguenti:

  -    [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  -    [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  -    [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  -    [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)
  -    [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)

  L'app Portale aziendale per Android usa Google Play Services per comunicare con il servizio Microsoft Intune. Poiché Google Play Services non è ancora disponibile in Cina, per eseguire una delle attività seguenti possono essere necessarie fino a 8 ore.

  | Console di amministrazione di Configuration Manager | App Portale aziendale di Intune per Android | Sito Web dell'app Portale aziendale di Intune |
  |----|----|----|        
  | Disattiva/Cancella (rimuovere tutti i dati)    | Rimuovere un dispositivo remoto | Rimuovi dispositivo (locale e remoto) |
  | Disattiva/Cancella (rimuovere i dati aziendali)    | Reimposta dispositivo | Reimposta dispositivo|
  | Distribuzioni di app nuove o aggiornate | Installare le app line-of-business disponibili | Reimpostazione del passcode del dispositivo|
  | Blocco remoto    | | |
  | Reimpostazione del passcode | | |        


## <a name="november-2016"></a>Novembre 2016

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

- **Nuova app Portale aziendale di Microsoft Intune disponibile per dispositivi Windows 10**

  Microsoft ha rilasciato una nuova [app Portale aziendale per dispositivi Windows 10](https://www.microsoft.com/store/apps/9wzdncrfj3pz). Questa app, basata sul nuovo formato universale di Windows 10, offre un'innovativa esperienza utente comune a tutti i dispositivi Windows 10, siano essi PC o dispositivi mobili, pur mantenendo le stesse funzionalità disponibili nella versione precedente dell'app Portale aziendale.

  La nuova app integra funzionalità specifiche della piattaforma, come l'accesso Single Sign-On (SSO) e l'autenticazione basata su certificati nei dispositivi Windows 10. L'app è disponibile come aggiornamento dell'app Portale aziendale per Windows 8.1 e dell'app Portale aziendale di Windows Phone 8.1 e può essere installata da Windows Store. Per altre informazioni, vedere [Intune Support Team Blog](http://aka.ms/intunecp_universalapp) (Blog del team di supporto Intune).

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


## <a name="notices"></a>Notifiche

### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 e System Center 2012 R2 Configuration Manager (RTM): il supporto per la gestione ibrida di dispositivi mobili termina il 10 aprile 2017

*11 gennaio 2017*

Il supporto per System Center 2012 Configuration Manager SP1 e System Center 2012 R2 Configuration Manager RTM è terminato il 12 luglio 2016. Per quanto riguarda la connessione di queste versioni al servizio Microsoft Intune per la gestione ibrida di dispositivi mobili, il supporto termina il 10 aprile 2017. Dopo tale data, la gestione ibrida di dispositivi mobili non sarà più disponibile con queste versioni. In pratica, i dispositivi gestiti non saranno più gestiti poiché il connettore Intune non si connetterà più al servizio Intune. I dati di Configuration Manager, ad esempio criteri e applicazioni, non verranno propagati a Intune e i dati dei dispositivi gestiti non verranno propagati a Configuration Manager finché non verrà eseguito un aggiornamento.

Se si esegue una distribuzione ibrida con Configuration Manager 2012 SP1 o R2 RTM, è consigliabile eseguire l'aggiornamento a Configuration Manager (Current Branch) o al Service Pack supportato più recente per Configuration Manager 2012 (R2 SP1 o SP2) prima del 10 aprile 2017 per evitare l'interruzione del servizio.

Risorse aggiuntive:
-    [Eseguire l'aggiornamento a System Center Configuration Manager (Current Branch)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-    [Pianificazione dell'aggiornamento a System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-    [Pianificazione dell'aggiornamento a System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Il caricamento del portale aziendale per Windows Phone 8 è deprecato
*25 ottobre 2016*

L'opzione che consente di caricare un'app Portale aziendale firmata è stata rimossa dalla console di Configuration Manager, poiché il supporto di Intune viene deprecato per Windows 8, Windows Phone 8 e Windows RT e il supporto per il portale aziendale per Windows Phone 8 termina in novembre.  I dispositivi Windows 8, Windows Phone 8 e Windows RT che sono già registrati continueranno a essere supportati, ma la registrazione di dispositivi aggiuntivi con queste piattaforme non sarà più supportata.


### <a name="see-also"></a>Vedere anche

- [Funzionalità MDM ibride precedenti](whats-new-hybrid-archive.md)
- [Novità di MDM in System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)


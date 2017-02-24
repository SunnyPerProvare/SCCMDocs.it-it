---
title: "Novità della gestione ibrida di dispositivi mobili | Documentazione Microsoft"
description: "Informazioni sulle nuove funzionalità di gestione dei dispositivi mobili disponibili per le distribuzioni ibride con System Center Configuration Manager e Intune."
ms.custom: na
ms.date: 02/14/2017
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
ms.sourcegitcommit: 7972aa2c39f5b86e69087b1ed5a1c3b50ba69940
ms.openlocfilehash: f74bd019b5403f3f5702795279759270261ce4db

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

## <a name="new-hybrid-features-in-february-2017"></a>Nuove funzionalità ibride (febbraio 2017)

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

Le funzionalità seguenti di Intune introdotte a febbraio 2017 funzionano nelle distribuzioni ibride:

- **Modernizzazione del sito Web del portale aziendale**

  Il sito Web del portale aziendale supporta app rivolte agli utenti che non hanno dispositivi gestiti. Il sito Web si allinea ad altri prodotti e servizi Microsoft usando una nuova combinazione di colori a contrasto, illustrazioni dinamiche e un "menu hamburger" che contiene i dettagli di contatto del supporto tecnico e le informazioni sui dispositivi gestiti esistenti. La pagina di destinazione è stata riorganizzata per evidenziare le app a disposizione degli utenti, con sequenze per le app in evidenza e aggiornate di recente. Nella pagina [UI updates](/intune/whats-new/whats-new-in-intune-app-ui) (Aggiornamenti dell'interfaccia utente) sono disponibili immagini precedenti e successive all'aggiornamento.

- **Nuovo indirizzo del server MDM per dispositivi Windows**

  L'indirizzo del server MDM per la registrazione dei dispositivi Windows e Windows Phone è cambiato da manage.microsoft.com a enrollment.manage.microsoft.com. Comunicare agli utenti di usare enrollment.manage.microsoft.com come indirizzo del server MDM, se richiesto, durante la registrazione di un dispositivo Windows o Windows Phone. Questo aggiornamento richiede anche la sostituzione di qualsiasi CNAME in DNS che reindirizza EnterpriseEnrollment.contoso.com a manage.microsoft.com con un CNAME in DNS che reindirizzi EnterpriseEnrollment.contoso.com a EnterpriseEnrollment-s.manage.microsoft.com. Per altre informazioni su questa modifica, visitare http://aka.ms/intuneenrollsvrchange. 

## <a name="new-hybrid-features-in-january-2017"></a>Nuove funzionalità ibride (gennaio 2017)

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

Le funzionalità seguenti di Intune introdotte in gennaio 2017 funzionano nelle distribuzioni ibride:

- **Supporto di Android 7.1.1**

  Intune ora supporta e gestisce in modo completo Android 7.1.1.

- **Risolvere i problemi di inattività dei dispositivi iOS o di comunicazione tra la console di amministrazione e questi dispositivi**

  Quando i dispositivi degli utenti perdono il contatto con Intune, è possibile assegnare loro nuove istruzioni per la risoluzione dei problemi, in modo che possano riottenere l'accesso alle risorse aziendali. Vedere [Devices are inactive, or the admin console cannot communicate with them](/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them) (I dispositivi sono inattivi o la console di amministrazione non può comunicare con loro).

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Novità di Configuration Manager Technical Preview 1701

- **Non è più necessario specificare le versioni di Android e iOS nella creazione guidata della gestione ibrida dei dispositivi mobili**

  A partire dalla Technical Preview 1701 per la gestione ibrida dei dispositivi mobili, non è più necessario indicare versioni specifiche di Android e iOS quando si creano nuovi criteri e profili per i dispositivi gestiti in Intune. Con questa modifica, le distribuzioni ibride possono offrire il supporto più rapidamente per le nuove versioni di Android e iOS, senza attendere una nuova versione o un'estensione di Configuration Manager. Per altre informazioni, vedere [Non è più necessario specificare le versioni di Android e iOS nella creazione guidata](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).


## <a name="new-hybrid-features-in-december-2016"></a>Nuove funzionalità ibride (dicembre 2016)

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

Le funzionalità seguenti di Intune introdotte in dicembre 2016 funzionano nelle distribuzioni ibride.

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


## <a name="new-hybrid-features-in-november-2016"></a>Nuove funzionalità ibride (novembre 2016)

### <a name="new-in-microsoft-intune"></a>Novità di Microsoft Intune

Le funzionalità seguenti di Intune introdotte in novembre 2016 funzionano nelle distribuzioni ibride.

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


## <a name="see-also"></a>Vedere anche

- [Funzionalità MDM ibride precedenti](whats-new-hybrid-archive.md)
- [Novità di MDM in System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)



<!--HONumber=Feb17_HO2-->



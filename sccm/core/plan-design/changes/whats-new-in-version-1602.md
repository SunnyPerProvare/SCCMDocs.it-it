---
title: "Novità della versione 1602 | System Center Configuration Manager"
description: "Le sezioni seguenti illustrano in dettaglio le modifiche e le nuove funzionalità introdotte nella versione 1602 di System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4021eca1-adfb-4e5a-adee-159263c29637
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: 0803a13bb58f0d02803c34e6a3cb20f5e6ba60b7

---
# <a name="what39s-new-in-version-1602-of-system-center-configuration-manager"></a>Novità della versione 1602 di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


L'aggiornamento 1602 per System Center Configuration Manager è un aggiornamento nella console per siti installati in precedenza che eseguono la versione 1511. La versione 1511 è la versione di base iniziale usata per installare nuovi siti di Configuration Manager.  


> [!TIP]  
>  Sono disponibili altre informazioni su:  
>   
>   -   [Installing new sites](/sccm/core/servers/deploy/install) (Installazione di nuovi siti) (con una versione di base, ad esempio 1511)  
>   -   [Installing updates at sites](/sccm/core/servers/manage/updates) (Installazione di aggiornamenti nei siti) (ad esempio versione 1602)  

 Le sezioni seguenti illustrano in dettaglio le modifiche e le nuove funzionalità introdotte nella versione 1602 di Configuration Manager.  

## <a name="site-infrastructure"></a>Infrastruttura del sito  

###  <a name="a-namebkmkupgradeosa-in-place-upgrade-the-operating-system-of-site-servers-that-run-windows-server-2008-r2"></a><a name="bkmk_UpgradeOS"></a>Aggiornamento sul posto del sistema operativo dei server del sito che eseguono Windows Server 2008 R2  
 I siti di Configuration Manager che eseguono la versione 1602 o versioni successive supportano l'aggiornamento sul posto del sistema operativo dei server del sito da Windows Server 2008 R2 a Windows Server 2012 R2.  

> [!WARNING]  
>  Prima di eseguire l'aggiornamento a Windows Server 2012 R2, **è necessario disinstallare WSUS 3.2** dal server.  
>   
>  Per informazioni su questo passaggio critico, vedere la sezione Funzionalità nuove e modificate in [Panoramica di Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx) nella documentazione di Windows Server.  

 Per aggiornare un server si usano le procedure di aggiornamento di Windows Server 2012 R2 e non è necessario eseguire un ripristino del server del sito di Configuration Manager dopo l'aggiornamento.  Per le procedure di aggiornamento, vedere [Opzioni di aggiornamento per Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) nella documentazione di Windows Server.  

###  <a name="a-namebkmkaoaga-sql-server-alwayson-availability-groups"></a><a name="bkmk_AOAG"></a> Gruppi di disponibilità SQL Server AlwaysOn  
 È possibile usare i gruppi di disponibilità SQL Server AlwaysOn per ospitare il database del sito nei siti primari e nel sito di amministrazione centrale come soluzione a disponibilità elevata e di ripristino di emergenza.  

 Per informazioni dettagliate, vedere [SQL Server AlwaysOn per database del sito a disponibilità elevata per System Center Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)  

## <a name="operating-system-deployment"></a>Distribuzione del sistema operativo  

### <a name="windows-10-servicing"></a>Manutenzione di Windows 10  
 In Configuration Manager versione 1602 sono stati aggiunti i miglioramenti seguenti per la manutenzione di Windows 10:  

-   Sono disponibili nuove opzioni di filtro per i piani di manutenzione che consentono di filtrare per **Lingua**, **Richiesto** e **Titolo**. Verranno aggiunti alla distribuzione associata solo gli aggiornamenti che soddisfano i criteri specificati.  

-   Quando si seleziona la classificazione **Aggiornamenti** per la sincronizzazione degli aggiornamenti software, viene visualizzata una finestra di dialogo di avviso per informare gli utenti che è necessario l'[hotfix 3095113 di WSUS 4.0](https://support.microsoft.com/kb/3095113) per la corretta sincronizzazione degli aggiornamenti software e per il corretto funzionamento della manutenzione di Windows 10. Dalla finestra di dialogo è possibile passare all'articolo della Knowledge Base associato.  

-   Gli aggiornamenti disponibili di Windows 10 vengono visualizzati ora solo nel nodo **Manutenzione di Windows 10** \ **Tutti gli aggiornamenti di Windows 10** della console di Configuration Manager. Questi aggiornamenti non vengono più visualizzati nel nodo **Aggiornamenti software** \ **Tutti gli aggiornamenti software** della console.  

-   Un piano di manutenzione è considerato una distribuzione ad alto rischio e nella finestra **Seleziona raccolta** vengono visualizzate soltanto le raccolte personalizzate che soddisfano le impostazioni di verifica della distribuzione configurate nelle proprietà del sito. Per altre informazioni, vedere [Settings to manage high-risk deployments for System Center Configuration Manager](../../../protect/understand/settings-to-manage-high-risk-deployments.md).  

-   Quando gli utenti finali avviano un pacchetto di aggiornamento di Windows 10, verrà visualizzata una finestra di dialogo che li informa che stanno per aggiornare il proprio sistema operativo.  

## <a name="application-management"></a>Gestione delle applicazioni  

### <a name="ios-app-configuration-policies"></a>Criteri di configurazione delle app iOS  
 Usare i criteri di configurazione delle app di Configuration Manager per specificare le impostazioni che potrebbero essere necessarie quando l'utente esegue un'app iOS. Un'applicazione potrebbe richiedere all'utente di specificare un numero di porta personalizzato, una lingua, o impostazioni di sicurezza o personalizzazione, ad esempio un logo aziendale.   
Se queste impostazioni vengono immesse in modo non corretto dall'utente, si può avere un aumento del carico dell'help desk rallentando inoltre l'adozione di nuove app.  

 I criteri di configurazione delle app permettono di evitare questi problemi consentendo di distribuire tali impostazioni agli utenti in un criterio prima dell'esecuzione dell'app. Le impostazioni vengono quindi specificate automaticamente e l'utente non deve intraprendere alcuna azione.  

 Per informazioni dettagliate, vedere [Configure iOS apps with app configuration policies in System Center Configuration Manager](../../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md) (Configurare le app iOS con i criteri di configurazione in System Center Configuration Manager).  

### <a name="manage-volume-purchased-ios-apps"></a>Manage volume-purchased iOS apps  
 Configuration Manager semplifica la distribuzione e la gestione delle app acquistate con Volume Purchase Program (VPP) di Apple con l'importazione delle informazioni di licenza dall'App Store e la verifica del numero di licenze usate.  

 Per informazioni dettagliate, vedere [Gestire le app iOS acquistate tramite Volume Purchase Program con System Center Configuration Manager](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md).  

### <a name="automatic-creation-of-office-mobile-apps"></a>Creazione automatica di app di Office per dispositivi mobili  
 Quando si esegue l'aggiornamento alla versione 1602 dalla versione 1511, Configuration Manager crea automaticamente le seguenti app di Microsoft Office per dispositivi mobili Android e iOS:  

-   Microsoft Word  

-   Microsoft Excel  

-   Microsoft PowerPoint  

-   Microsoft OneDrive  

-   Microsoft OneNote (solo iOS)  

-   Microsoft Outlook  

Queste app si trovano nel nodo **Applicazioni** della console di Configuration Manager.  

 Per altre informazioni sulla distribuzione di applicazioni, vedere [Come distribuire le applicazioni con System Center Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

## <a name="software-updates"></a>Aggiornamenti software  

### <a name="manage-office-365-client-updates"></a>Gestire gli aggiornamenti del client di Office 365  
 System Center Configuration Manager consente di gestire gli aggiornamenti del client di Office 365 usando il flusso di lavoro Gestione aggiornamenti software. Per altre informazioni, vedere [Gestire gli aggiornamenti di Office 365 ProPlus con System Center Configuration Manager](/sccm/sum/deploy-use/manage-office-365-proplus-updates).  

## <a name="compliance-settings"></a>Impostazioni di conformità  

### <a name="compliance-settings-for-devices-running-windows-10-team"></a>Impostazioni di conformità per i dispositivi che eseguono Windows 10 Team  
 Sono state aggiunte nuove impostazioni all'elemento di configurazione **Windows 8.1 e Windows 10** che consentono di controllare i dispositivi che eseguono Windows 10 Team, ad esempio un dispositivo Surface Hub.  

 Per informazioni dettagliate, vedere [Come creare elementi di configurazione per dispositivi Windows 8.1 e Windows 10 gestiti senza il client di System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="kiosk-mode-settings-for-android-samsung-knox-devices"></a>Impostazioni della modalità tutto schermo per i dispositivi Android Samsung KNOX  
 La modalità tutto schermo consente di bloccare un dispositivo per consentire solo l'uso di alcune funzionalità. Ad esempio, è possibile consentire a un dispositivo di eseguire solo un'app gestita specificata o disabilitare i pulsanti del volume in un dispositivo. Queste impostazioni potrebbero essere usate per un modello demo di un dispositivo o per un dispositivo dedicato all'esecuzione di una sola funzione, ad esempio un dispositivo POS. In Configuration Manager è ora possibile specificare le impostazioni della modalità tutto schermo per i dispositivi Samsung KNOX.  

 Per informazioni dettagliate, vedere [Come creare elementi di configurazione per dispositivi Android e Samsung KNOX gestiti senza il client di System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md).  

## <a name="conditional-access"></a>Accesso condizionale  

### <a name="conditional-access-for-pcs-managed-by-system-center-configuration-manager"></a>Accesso condizionale per i PC gestiti da System Center Configuration Manager  
 Prima di questa versione, per configurare l'accesso condizionale per un PC era necessario che il PC fosse registrato in Intune o aggiunto a un dominio. A partire dall'aggiornamento 1602 è supportato l'accesso condizionale per i PC gestiti da System Center Configuration Manager. Per i PC gestiti da System Center Configuration Manager, è possibile limitare l'accesso a Exchange Online e SharePoint Online solo ai dispositivi che soddisfano i criteri di conformità impostati.  

 Per informazioni dettagliate, vedere [Gestire l'accesso ai servizi di O365 per i PC gestiti da System Center Configuration Manager](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  

### <a name="restricting-access-based-on-device-health-attestation-status"></a>Limitazione dell'accesso in base allo stato di attestazione dell'integrità del dispositivo  
 È ora possibile limitare l'accesso alla posta elettronica e ai servizi di Office 365 in base all'integrità dei dispositivi, come segnalato dal servizio di attestazione dell'integrità. Inoltre, i dispositivi gestiti da Intune sono inclusi nei report sull'integrità del dispositivo.  

 È stata aggiunta una nuova regola di conformità alla console di Configuration Manager che consente di specificare se l'accesso deve essere consentito o negato ai dispositivi in base al loro stato di integrità.   Per informazioni dettagliate sul servizio di attestazione dell'integrità e su come viene segnalata l'integrità dei dispositivi in Intune, vedere [Attestazione dell'integrità per System Center Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### <a name="new-compliance-policy-rules"></a>Nuove regole dei criteri di conformità  
 Sono state aggiunte nuove regole dei criteri di conformità, come gli aggiornamenti automatici e la password per sbloccare i dispositivi, per supportare requisiti di sicurezza migliori.  


 Per maggiori dettagli, vedere [Criteri di conformità del dispositivo in System Center Configuration Manager](../../../protect/deploy-use/device-compliance-policies.md).  

### <a name="make-sure-enrolled-and-compliant-devices-always-have-access-to-exchange-on-premises"></a>Assicurarsi che i dispositivi registrati e conformi abbiano sempre accesso a Exchange locale  
 **Sostituzione della regola predefinita: consenti sempre l'accesso a Exchange ai dispositivi conformi e registrati in Intune:** quando si seleziona questa opzione, i dispositivi registrati in Intune e conformi ai criteri di conformità possono accedere a Exchange locale. Questa regola sostituisce la regola predefinita, ossia anche se si definisce per la regola predefinita l'impostazione per la quarantena o il blocco dell'accesso, i dispositivi registrati e conformi potranno accedere a Exchange locale. Usare questa impostazione quando si vuole che i dispositivi registrati e conformi abbiano sempre accesso alla posta elettronica tramite Exchange locale.  

 Questa regola è disponibile nella pagina **Generale** della **Configurazione guidata dei criteri di accesso condizionale** per Exchange locale.  

 Per la procedura dettagliata, vedere [Gestire l'accesso alla posta elettronica in System Center Configuration Manager](../../../protect/deploy-use/manage-email-access.md).  

## <a name="client-management"></a>Gestione dei client  

### <a name="client-online-status"></a>Stato online del client  
 È disponibile un nuovo stato per i client per monitorare se un computer è online o meno. Un computer viene considerato online se è connesso al relativo punto di gestione assegnato. Per indicare che il computer è online, il client invia messaggi di tipo ping al punto di gestione. Se il punto di gestione non riceve alcun messaggio per 5 minuti, lo stato del client viene considerato offline.  

 Per informazioni dettagliate, vedere [Come monitorare i client in System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md).  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Aggiornare i criteri di computer e utenti da Software Center  
 È stata aggiunta una nuova opzione, **Criteri sincronizzazione**, alla pagina **Opzioni** > **Manutenzione computer** di Software Center che consente al computer di aggiornare i criteri di computer e utenti di Configuration Manager.  

### <a name="software-center-branding-changes"></a>Modifiche di personalizzazione di Software Center  
 È possibile modificare il colore, il nome dell'organizzazione e l'icona visualizzati in Software Center. Queste impostazioni verranno applicate in base alle regole seguenti:  

1.  Se il ruolo del server del sito punto per siti Web del Catalogo applicazioni non è installato, Software Center visualizzerà il nome dell'organizzazione specificato nell'impostazione **Nome organizzazione visualizzato in Software Center** del client **Agente computer**.  

2.  Se il ruolo del server del sito punto per siti Web del Catalogo applicazioni è installato, Software Center visualizzerà il nome dell'organizzazione e il colore specificati nelle proprietà del ruolo del server del sito punto per siti Web del Catalogo applicazioni.  

3.  Se una sottoscrizione di Microsoft Intune è configurata e connessa all'ambiente Configuration Manager, Software Center visualizzerà il nome dell'organizzazione, il colore e il logo aziendale specificati nelle proprietà della sottoscrizione di Intune.  

### <a name="health-attestation"></a>Attestazione dell'integrità  
 Gli amministratori possono visualizzare l'attestazione dell'integrità del dispositivo di Windows 10 nella console di Configuration Manager.  Questa funzionalità è disponibile per Configuration Manager e Configuration Manager con Microsoft Intune. L'attestazione dell'integrità dei dispositivi consente all'amministratore di assicurare che nei computer client siano abilitate le seguenti configurazioni attendibili di BIOS, TPM e software di avvio:  

-   Antimalware ad esecuzione anticipata  

-   BitLocker  

-   Avvio protetto  

-   Integrità del codice  

Per informazioni dettagliate, vedere [Attestazione dell'integrità per System Center Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### <a name="improvements-to-endpoint-protection-antimalware-settings"></a>Miglioramenti delle impostazioni antimalware di Endpoint Protection  
 Nella versione 1602 sono state aggiunte le nuove impostazioni seguenti nei criteri antimalware di Endpoint Protection per Windows Defender:  

-   Protezione in tempo reale: abilita la protezione per le applicazioni potenzialmente indesiderate al download o prima dell'installazione  

-   Impostazioni di analisi: analizza le unità di rete mappate quando si esegue un'analisi completa  

-   Impostazioni per l'invio automatico dei file di esempio:  

     Il motore antimalware può richiedere l'invio a Microsoft di file di esempio per un'ulteriore analisi. Per impostazione predefinita, viene sempre visualizzata una richiesta prima dell'invio di tali campioni. Gli amministratori ora possono gestire le impostazioni seguenti per configurare questo comportamento:  

    -   Avanzate: abilita l'invio automatico di file di esempio per consentire a Microsoft di determinare se alcuni elementi rilevati siano dannosi  

    -   Avanzate: consente agli utenti di modificare le impostazioni di invio automatico di file di esempio  

    Inoltre, l'impostazione esistente **Cartelle e file esclusi** nella sezione "Impostazioni di esclusione" del criterio antimalware di Endpoint Protection è stata migliorata per consentire le esclusioni dei dispositivi.  

Per informazioni dettagliate, vedere [Come creare e distribuire criteri antimalware per Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-antimalware-policies.md).  

## <a name="mobile-device-management"></a>Gestione dispositivi mobili  

### <a name="ios-activation-lock"></a>Blocco attivazione di iOS  
 Configuration Manager consente di gestire il blocco attivazione iOS, una funzionalità dell'app Trova il mio iPhone per dispositivi iOS 7.1 e versioni successive. Blocco attivazione viene abilitato automaticamente quando si usa l'app Trova il mio iPhone in un dispositivo. Una volta abilitato, richiede l'immissione di un ID Apple e una password dell'utente prima di poter:  

-   Disattivare Trova il mio iPhone  

-   Cancellare il dispositivo  

-   Riattivare il dispositivo  

Configuration Manager può richiedere lo stato del blocco attivazione per i dispositivi con e senza supervisione che eseguono iOS 7.1 e versioni successive. Per i dispositivi con supervisione, Configuration Manager può recuperare il codice del bypass di Blocco attivazione e inviarlo direttamente al dispositivo.  

 Per informazioni dettagliate, vedere [Proteggere i dispositivi iOS con il bypass del blocco attivazione in System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock).  

### <a name="monitor-terms-and-conditions-deployments"></a>Monitorare le distribuzioni di termini e condizioni  
 È possibile monitorare le distribuzioni di termini e condizioni nella console di Configuration Manager.  

 Selezionare la distribuzione di termini e condizioni dall'elenco delle distribuzioni. L'area di riepilogo visualizza le statistiche seguenti:  

-   **Conforme** : gli utenti hanno accettato la versione più recente di termini e condizioni  

-   **Erroree**  

-   **Non conforme** : gli utenti hanno accettato una versione precedente di termini e condizioni  

-   **Sconosciuto** : gli utenti non hanno accettato termini e condizioni, inclusi quelli senza un dispositivo registrato  



<!--HONumber=Nov16_HO1-->


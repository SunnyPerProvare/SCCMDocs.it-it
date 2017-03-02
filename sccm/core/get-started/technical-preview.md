---
title: Technical Preview per System Center Configuration Manager | Microsoft Docs
description: "Informazioni sulla versione Technical Preview che consente di testare nuove funzionalità in System Center Configuration Manager."
ms.custom: na
ms.date: 2/1/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 157
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 4b1daa727477b1273cdbee1bc7e3ac8af5911ff0
ms.openlocfilehash: 4703178c5ce3e23cb9d2e4557466fcec571c2983
ms.lasthandoff: 02/22/2017


---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Technical Preview)*

**Pagina iniziale di System Center Configuration Manager Technical Preview**. Questo argomento include informazioni dettagliate sulla versione di anteprima in evoluzione che comprende nuove funzionalità e caratteristiche in fase di sviluppo. Ogni versione Technical Preview include nuove funzionalità che, nel momento in cui la Technical Preview viene resa disponibile, non sono ancora contenute nella versione Current Branch di System Center Configuration Manager. Tali funzionalità potranno essere inserite in seguito nella versione Current Branch. Tuttavia, prima di essere finalizzate e inserite, viene offerta all'utente la possibilità di provarle e di inviare commenti.  

 Poiché si tratta di una Technical Preview, dettagli e funzionalità sono soggetti a modifiche.  

 Questo argomento include informazioni che si applicano a tutte le versioni Technical Preview. Le informazioni sulle nuove funzionalità sono elencate in base alla versione Technical Preview in cui viene resa disponibile per la prima volta la funzionalità, ad esempio 1701 per gennaio 2017. I dettagli di queste funzionalità sono descritti in argomenti separati dedicati a ogni versione di anteprima.  

 Per informazioni sulle novità della versione Current Branch di Configuration Manager, vedere [What's new in System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012)(Novità di System Center Configuration Manager).



##  <a name="a-namebkmkreqsa-requirements-and-limitations-for-the-technical-preview"></a><a name="bkmk_reqs"></a> Requisiti e limitazioni per la versione Technical Preview  

> [!IMPORTANT]     
>  La Technical Preview viene concessa in licenza per essere usata esclusivamente in un ambiente lab.  Microsoft potrebbe non fornire supporto tecnico e alcune funzionalità potrebbero non essere disponibili nel software di anteprima. Inoltre, il software di anteprima potrebbe essere caratterizzato da standard di sicurezza, privacy, accessibilità, disponibilità e affidabilità ridotti o diversi rispetto al software commercializzato.  

 Per la maggior parte dei prerequisiti di prodotto, usare le informazioni disponibili in [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md) (Configurazioni supportate per System Center Configuration Manager). Per le versioni Technical Preview si applicano le seguenti eccezioni:  

-   Ogni installazione rimane attiva per 90 giorni prima di diventare inattiva.  

-   L'inglese è l'unica lingua supportata.  

-   È supportato solo un sito primario autonomo. Non esiste alcun supporto per un sito di amministrazione centrale, più siti primari o i siti secondari.  

-   Sono supportate solo le seguenti versioni di SQL Server:  

    -   SQL Server 2016 (senza Service Pack e versioni successive)
    -   SQL Server 2014 (senza Service Pack e versioni successive)
    -   SQL Server 2012 (con Service Pack 2 o versioni successive)


-   Il sito supporta fino a 10 client, che devono eseguire uno dei seguenti sistemi operativi:  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 8  
      -   Windows 7  


-   Sono supportati solo i flag di installazione (opzioni) seguenti:  

    -   **/silent**  
    -   **/testdbupgrade**  

-   Quando applicabile, sono inclusi ulteriori limitazioni o requisiti con i dettagli per ogni versione specifica della Technical Preview  

-   Non esiste alcun supporto per la migrazione a o da questa build di anteprima.  

-   Non esiste alcun supporto per l'aggiornamento a questa build di anteprima.  

-   Non esiste alcun supporto per l'aggiornamento a una build di produzione (Current Branch) da questa build di anteprima. Se sono disponibili aggiornamenti per una versione di anteprima, è tuttavia possibile trovarli e installarli dal nodo **Aggiornamenti e manutenzione** della console di Configuration Manager console. Per un video relativo al processo di aggiornamento nella console, vedere [Installazione dei pacchetti di aggiornamento di ConfigMgr](https://www.youtube.com/embed/KBd_EGFbUT8) su youtube.com.  

##  <a name="a-namebkmkinstalla-install-and-update-the-technical-preview"></a><a name="bkmk_install"></a> Installare e aggiornare la versione Technical Preview  
 System Center Configuration Manager Technical Preview è diversa dalla versione corrente di System Center Configuration Manager.  

 Per usare la Technical Preview è innanzitutto necessario installare una **versione di base** della build Technical Preview. Dopo l'installazione di una versione di base, sarà quindi possibile usare gli **aggiornamenti nella console** per aggiornare l'installazione con la versione di anteprima più recente.     In genere, le nuove versioni Technical Preview sono disponibili ogni mese.

Ogni versione di anteprima è supportata finché non sono disponibili fino a tre versioni successive. Pertanto, quando viene rilasciata la versione 1702 la versione 1610 non è più supportata, mentre rimangono supportate le versioni 1611, 1612 e 1701. Se tuttavia l'ultima linea di base non rientra nel supporto (come nel caso della versione 1610), è ancora disponibile il supporto per l'installazione di un nuovo sito Technical Preview, purché tale istallazione venga aggiornata a una versione supportata.

> [!TIP]  
>  Quando si installa un aggiornamento per la Technical Preview, si aggiorna l'installazione di anteprima alla nuova versione Technical Preview.    Un'installazione Technical Preview non prevede mai la possibilità di eseguire l'aggiornamento a un'installazione del ramo corrente, né di ricevere gli aggiornamenti dalla versione ramo corrente.  

 **Versioni di base della Technical Preview attive:**  
 È possibile installare una versione di base per un massimo di 1 anno dopo il rilascio.

-   **Technical Preview 1610**: Configuration Manager Technical Preview 1610 è disponibile sia come aggiornamento nella console per Configuration Manager Technical Preview, sia come nuova versione di base sul sito Web [TechNet Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).




##  <a name="a-namebkmktpfeedbacka-providing-feedback"></a><a name="BKMK_TPFeedback"></a> Invio di commenti e suggerimenti  
 Saremmo lieti di ricevere i vostri commenti sulla technical preview. Per inviare commenti e suggerimenti sulle funzionalità di ogni anteprima, seguire il collegamento al nostro modulo per i commenti e i suggerimenti nella pagina del [programma dei commenti e suggerimenti di Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) del sito Microsoft Connect.  

 Siamo anche interessati a conoscere le vostre idee su eventuali nuove funzionalità. Per inviare nuove idee e votare le idee presentate da altri, [visitare la nostra pagina dedicata alla voce degli utenti](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="a-namebkmktpcapsa-capabilities-delivered-in-technical-previews"></a><a name="bkmk_tpCaps"></a> Funzionalità disponibili nelle Technical Preview  
 Di seguito sono elencate le funzionalità disponibili in ogni versione Technical Preview di Configuration Manager.  Le funzionalità disponibili a partire da una versione Technical Preview rimangono disponibili nelle versioni successive. Analogamente, le funzionalità che sono state aggiunte alla versione System Center Configuration Manager (Current Branch) rimangono disponibili nelle versioni Technical Preview successive.  Fare clic sul contenuto di ogni versione di anteprima per visualizzare altre informazioni su una funzionalità specifica.  

 |Funzionalità|Versione Technical Preview|Versione Current Branch|  
 |----------------|---------------------|--------------------|
 |Miglioramenti dei gruppi di limiti per i punti di aggiornamento software | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#boundary-groups-improvements-for-software-update-points)    |![Non aggiunta](media/Red_X.gif)  |
 |L'inventario hardware raccoglie le informazioni UEFI | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#hardware-inventory-collects-uefi-information)|![Non aggiunta](media/Red_X.gif)  |
 |Miglioramenti alla distribuzione del sistema operativo| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#improvements-to-operating-system-deployment)|![Non aggiunta](media/Red_X.gif)  |
 |Ospitare gli aggiornamenti software in punti di distribuzione basati sul cloud| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#host-software-updates-on-cloud-based-distribution-points)|![Non aggiunta](media/Red_X.gif) |
 |Convalidare i dati di attestazione dell'integrità del dispositivo tramite punti di gestione| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#validate-device-health-attestation-data-via-management-points)|![Non aggiunta](media/Red_X.gif) |
 |Connettore OMS per il cloud di Microsoft Azure per enti pubblici |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#use-the-oms-connector-for-microsoft-azure-government-cloud) |![Non aggiunta](media/Red_X.gif) |
 |Non è più necessario specificare le versioni di Android e iOS nella creazione guidata |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |![Non aggiunta](media/Red_X.gif) |
 |Accesso ai dati di endpoint OData |[Technical Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|![Non aggiunta](media/Red_X.gif)|
 |Punto di servizio Data Warehouse |[Technical Preview 1612](capabilities-in-technical-preview-1612.md#the-data-warehouse-service-point)|![Non aggiunta](media/Red_X.gif)|
 |Strumento di pulizia della raccolta contenuto |[Technical Preview 1612](capabilities-in-technical-preview-1612.md#content-library-cleanup-tool)|![Non aggiunta](media/Red_X.gif)|
 |Miglioramenti per la ricerca nella console |[Technical Preview 1612](capabilities-in-technical-preview-1612.md#improvements-for-in-console-search)|![Non aggiunta](media/Red_X.gif)|
 |Evitare l'installazione di un'applicazione se è in esecuzione un programma specifico|[Technical Preview 1612](capabilities-in-technical-preview-1612.md#prevent-installation-of-an-application-if-a-specified-program-is-running)|![Non aggiunta](media/Red_X.gif)|
 |Nuova notifica di Windows Hello for Business per gli utenti finali|[Technical Preview 1612](capabilities-in-technical-preview-1612.md#new-windows-hello-for-business-notification-for-end-users)|![Non aggiunta](media/Red_X.gif)|
 |Supporto di Windows Store for Business in Configuration Manager|[Technical Preview 1612](capabilities-in-technical-preview-1612.md#windows-store-for-business-support-in-configuration-manager)|![Non aggiunta](media/Red_X.gif)|
 |Tornare alla pagina precedente quando si verifica un errore di una sequenza di attività|[Technical Preview 1612](capabilities-in-technical-preview-1612.md#return-to-previous-page-when-a-task-sequence-fails)|![Non aggiunta](media/Red_X.gif)|
 |Supporto per i file di installazione rapida per gli aggiornamenti di Windows 10|[Technical Preview 1612](capabilities-in-technical-preview-1612.md#express-installation-files-support-for-windows-10-updates)|![Non aggiunta](media/Red_X.gif)|
 |Onboarding di Azure Active Directory|[Technical Preview 1612](capabilities-in-technical-preview-1612.md#azure-active-directory-onboarding)|![Non aggiunta](media/Red_X.gif)|
|Modifica alla configurazione dell'autenticazione a più fattori per la registrazione dei dispositivi|[Technical Preview 1612](capabilities-in-technical-preview-1612.md#change-to-configuring-multi-factor-authentication-for-device-enrollment)|![Non aggiunta](media/Red_X.gif)|
|Pre-cache del contenuto per le distribuzioni e le sequenze di attività |[Technical Preview 1611](capabilities-in-technical-preview-1611.md#pre-cache-content-for-available-deployments-and-task-sequences)|![Non aggiunta](media/Red_X.gif)|
 |Impostazioni di configurazione di Windows Defender|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#windows-defender-configuration-settings)|[Versione 1610](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |Richiedere la sincronizzazione dei criteri dalla console di amministrazione|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#request-policy-sync-from-administrator-console)|[Versione 1610](/sccm/mdm/deploy-use/sync-intune-device)|
 |Supporto di ruoli di sicurezza aggiuntivi per il nodo Dispositivi di proprietà dell'azienda|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#additional-security-role-support)|[Versione 1610](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management#new-hybrid-features-in-november-2016)|
 |Accesso condizionale per profili VPN di Windows 10|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#conditional-access-for-windows-10-vpn-profiles)|[Versione 1610](/sccm/protect/deploy-use/create-vpn-profiles#configure-the-authentication-method-for-the-vpn-profile)|
 |Filtrare per dimensioni del contenuto nelle regole di distribuzione automatica|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|[Versione 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#filter-by-content-size-in-automatic-deployment-rules) |
 |Funzionalità migliorate per le finestre di dialogo del software richieste|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|[Versione 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Negare richieste di applicazioni approvate in precedenza|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|[Versione 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Impedire l'aggiornamento automatico dei client|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|[Versione 1610](/sccm/core/clients/manage/upgrade/exclude-clients-windows)|
 |Miglioramenti a Endpoint Protection|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|![Non aggiunta](media/Red_X.gif)|
 |Aumento del numero di dispositivi registrati|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#increased-number-of-enrolled-devices)|![Non aggiunta](media/Red_X.gif)|
 |Impostazioni aggiuntive per il DEP di Apple|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|[Versione 1610](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)|
 |Miglioramenti all'integrazione di Windows Store per le aziende con Configuration Manager|[Tech Preview 1609](capabilities-in-technical-preview-1609.md)|[Versione 1610](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |Nuove impostazioni di conformità per gli elementi di configurazione|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|[Versione 1610](/sccm/compliance/deploy-use/create-configuration-items)|
 |Integrazione con Upgrade Analytics|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|[Versione 1610](/sccm/core/clients/manage/upgrade/upgrade-analytics)|
 |Tipi di connessione nativa per i profili ibridi VPN di Windows 10|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![Non aggiunta](media/Red_X.gif)|
 |Miglioramenti ai gruppi limite|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|[Versione 1610](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#BKMK_BoundaryGroups)|
 |Dashboard di Gestione client di Office 365|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|[Versione 1610](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard)|
 |Distribuire le app di Office 365 ai client|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#deploy-office-365-apps-to-clients)|![Non aggiunta](media/Red_X.gif)|
 |Miglioramenti alla conversione da BIOS a UEFI|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#BKMK_UEFIConversion)|[Versione 1610](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion)|
 |Grafici di conformità di Intune|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|[Versione 1610](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)|
 |Miglioramenti del passaggio della sequenza di attività Prepara client ConfigMgr per l'acquisizione|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|[Versione 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)|
 |Miglioramenti a Software Center|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|[1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#general-improvements-to-software-center)|
 |Miglioramenti ad Asset Intelligence|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|![Non aggiunta](media/Red_X.gif)|
 |Traduzione della tastiera di controllo remoto|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#remote-control-keyboard-translation)|![Non aggiunta](media/Red_X.gif)|
 |Miglioramenti al criterio di aggiornamento edizione di Windows 10|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#dmp_edition)|[Versione 1610](/sccm/compliance/deploy-use/upgrade-windows-version)|
 |Personalizzazione delle finestre di dialogo di Software Center|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#customizable-branding-for-software-center-dialogs)|![Non aggiunta](media/Red_X.gif)|  
 |Punti di gestione dei dispositivi multipli per la gestione di dispositivi mobili|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_onprem)|[Versione 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#on-premises-mobile-device-management)|
 |Categorizzazione automatica dei dispositivi in raccolte|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_category)|[Version 1606](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections) |
 |Periodo di tolleranza per l'imposizione delle distribuzioni di applicazioni e aggiornamenti software obbligatorie|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_grace)|[Versione 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Uso di Configuration Manager come programma di installazione gestito con Device Guard|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_devg)|![Non aggiunta](media/Red_X.gif)|
 |Gateway di gestione cloud (già Servizio proxy cloud)|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#cloud_proxy) | [Versione 1610](/sccm/core/clients/manage/plan-cloud-management-gateway)|  
 |Gestione dell'agente del client Office 365 in Configuration Manager|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#manage_o365) |[Versione 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#software-updates)|  
 |La variabile della sequenza di attività OSDPreserveDriveLetter è stata deprecata|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#osdpreservedriveletter) |[Versione 1606](/sccm/osd/understand/task-sequence-built-in-variables) |
 |Modifiche per il nodo Aggiornamenti e manutenzione|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#updatesandservicing)|[Versione 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#updates-and-servicing) |
 |VPN per app per dispositivi Windows 10|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PerAppVPN)|[Versione 1606](/sccm/protect/deploy-use/create-vpn-profiles)|  
 |Miglioramenti della sequenza di attività Installa aggiornamenti software|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_InstallSU)|[Versione 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |Miglioramenti del passaggio della sequenza di attività Prepara client ConfigMgr per l'acquisizione |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PrepareConfigMgrClient)|[Versione 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) |
 |Periodo di prova per le distribuzioni di applicazioni obbligatorie |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Grace)|![Non aggiunta](media/Red_X.gif)|  
 |Nuova esperienza per le azioni dei dispositivi remoti |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_Remote)|[Versione 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Windows Store per le app aziendali |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_WSFB)|[Versione 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Miglioramenti generali per le app acquistate con Volume Purchase Program|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP2)|[Versione 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Protezione dei dati aziendali|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_VPP)|[Versione 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606)|  
 |Gli utenti finali possono installare le app dal portale aziendale |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|![Non aggiunta](media/Red_X.gif)|  
 |Nuove schede per gli aggiornamenti e i sistemi operativi in Software Center|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_SW1)|[Versione 1606 ](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Assistenza a un gruppo di server |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|[Versione 1606](/sccm/sum/deploy-use/service-a-server-group)|   
 |Supporto del servizio Windows Defender Advanced Threat Protection |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_ATP)|[Versione 1606](/sccm/protect/deploy-use/windows-defender-advanced-threat-protection)|  
 |Nuove opzioni di riavvio per i client Windows 10 dopo l'installazione degli aggiornamenti software|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_RestartOptions)|[Versione 1606](/sccm/sum/plan-design/plan-for-software-updates#restart-options-for-Windows-10-clients-after-software-update-installation)|  
 |Attestazione dell'integrità del dispositivo locale |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_DHA)|[Versione 1606](/sccm/core/servers/manage/health-attestation)|  
 |Predichiarazione dei dispositivi di proprietà dell'azienda con numero di serie IMEI o iOS|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_IMEI)|[Versione 1606](/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id)|  
 |Gestire le app acquistate con Volume Purchase Program da Windows Store per le aziende| [Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_WindowsVPP)|[Versione 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Miglioramenti alla gestione di Microsoft Passport for Work|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_PFW)|[Versione 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Opzione per il passaggio dei client a un nuovo punto di aggiornamento software|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_switchsup)|[Versione 1606](/sccm/sum/plan-design/plan-for-software-updates#BKMK_ManuallySwitchSUPs)|  
 |Impostazioni client per gestire le impostazioni della cache del client e la peer cache del client |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_peercache)|Impostazioni client: [versione 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#administration)<br/>Peer cache: [versione 1610](/sccm/core/plan-design/hierarchy/client-peer-cache)|  
 |Supporto per Passport for Work come provider di archiviazione chiavi |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_passport)|[Versione 1606](/sccm/protect/deploy-use/create-certificate-profiles)|  
 |Attestazione dell'integrità del dispositivo locale|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_onpremdha)|[Versione 1606](/sccm/core/servers/manage/health-attestation)|  
 |Impostazione di Smart Lock per dispositivi Android|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_Smart)|[Versione 1606](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference)|  
 |Miglioramenti a Software Center|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_SC1603)|[Versione 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Miglioramenti del controllo remoto|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RC1603)|[Versione 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#remote-control)|  
 |Personalizzare le dimensioni della finestra e del blocco TFTP RamDisk nei punti di distribuzione abilitati per PXE|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RamDiskTFTP)|[Versione 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  


 Quando tutte le funzionalità di una versione di Technical Preview sono disponibili nella versione minima supportata del Current Branch, i dettagli per tale versione di anteprima vengono rimossi da questa tabella.


## <a name="see-also"></a>Vedere anche  
[What's new in System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions) (Novità di System Center Configuration Manager)  
 [Introduction to System Center Configuration Manager](../../core/understand/introduction.md) (Introduzione a System Center Configuration Manager)


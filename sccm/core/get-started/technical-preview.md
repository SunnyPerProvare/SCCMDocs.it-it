---
title: Technical Preview per System Center Configuration Manager
description: "Informazioni sulla versione Technical Preview che consente di testare nuove funzionalità in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
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
ms.sourcegitcommit: 39a9cde3bd955c84f301d25258b413fecaa4393b
ms.openlocfilehash: 2aa78c20c919d04401f663063860df06c5262048


---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Technical Preview)*

**Pagina iniziale di System Center Configuration Manager Technical Preview**. Questo argomento include informazioni dettagliate sulla versione di anteprima in evoluzione che comprende nuove funzionalità e caratteristiche in fase di sviluppo. Ogni versione Technical Preview include nuove funzionalità che, nel momento in cui la Technical Preview viene resa disponibile, non sono ancora contenute nella versione Current Branch di System Center Configuration Manager. Tali funzionalità potranno essere inserite in seguito nella versione Current Branch. Tuttavia, prima di essere finalizzate e inserite, viene offerta all'utente la possibilità di provarle e di inviare commenti.  

 Poiché si tratta di una Technical Preview, dettagli e funzionalità sono soggetti a modifiche.  

 Questo argomento include informazioni che si applicano a tutte le versioni Technical Preview. Le informazioni sulle nuove funzionalità sono elencate in base alla versione Technical Preview in cui viene resa disponibile per la prima volta la funzionalità, ad esempio 1512 per dicembre 2015. I dettagli di queste funzionalità sono descritti in argomenti separati dedicati a ogni versione di anteprima.  

 Per informazioni sulle novità della versione Current Branch di Configuration Manager, vedere [What's new in System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012)(Novità di System Center Configuration Manager).



##  <a name="a-namebkmkreqsa-requirements-and-limitations-for-the-technical-preview"></a><a name="bkmk_reqs"></a> Requisiti e limitazioni per la versione Technical Preview  

> [!IMPORTANT]  
>  La Technical Preview viene concessa in licenza per essere usata esclusivamente in un ambiente lab.  Microsoft potrebbe non fornire supporto tecnico e alcune funzionalità potrebbero non essere disponibili nel software di anteprima. Inoltre, il software di anteprima potrebbe essere caratterizzato da standard di sicurezza, privacy, accessibilità, disponibilità e affidabilità ridotti o diversi rispetto al software commercializzato.  

 Per la maggior parte dei prerequisiti di prodotto, usare le informazioni disponibili in [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md) (Configurazioni supportate per System Center Configuration Manager). Per le versioni Technical Preview si applicano le seguenti eccezioni:  

-   Ogni installazione rimane attiva per 90 giorni prima di diventare inattiva.  

-   L'inglese è l'unica lingua supportata.  

-   È supportato solo un sito primario autonomo. Non esiste alcun supporto per un sito di amministrazione centrale, più siti primari o i siti secondari.  

-   Sono supportate solo le seguenti versioni di SQL Server:  

    -   SQL Server 2012 con aggiornamento cumulativo 2 o versione successiva  

    -   SQL Server 2014  

-   Il sito supporta fino a 10 client, che devono eseguire uno dei seguenti sistemi operativi:  

    -   Windows 7  

    -   Windows 8  

    -   Windows 8.1  

    -   Windows 10  

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

> [!TIP]  
>  Quando si installa un aggiornamento per la Technical Preview, si aggiorna l'installazione di anteprima alla nuova versione Technical Preview.    Un'installazione Technical Preview non prevede mai la possibilità di eseguire l'aggiornamento a un'installazione del ramo corrente, né di ricevere gli aggiornamenti dalla versione ramo corrente.  

 **Versioni di base della Technical Preview attive:**  
 È possibile installare una versione di base per un massimo di 1 anno dopo il rilascio.

-   **Technical Preview 1610**: Configuration Manager Technical Preview 1610 è disponibile sia come aggiornamento nella console per Configuration Manager Technical Preview, sia come nuova versione di base sul sito Web [TechNet Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

-   **Technical Preview 1603** come parte di **System Center Technical Preview 5**: Configuration Manager Technical Preview 1603 è disponibile sia come aggiornamento nella console per Configuration Manager Technical Preview, sia come nuova versione di base inclusa in System Center Technical Preview 5.    Solo la versione inclusa in System Center Technical Preview 5 può essere usata per un'installazione di base.  

     Informazioni sulla versione di base di [Configuration Manager Technical Preview inclusa in System Center Technical Preview 5](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview):  

    -   Sia il programma di installazione che la console di Configuration Manager specificano la versione System Center Configuration Manager Technical Preview 1603.  

    -   Questa versione di base funziona analogamente a Configuration Manager Technical Preview 1603, anche per quanto riguarda il supporto per gli aggiornamenti nella console.  


##  <a name="a-namebkmktpfeedbacka-providing-feedback"></a><a name="BKMK_TPFeedback"></a> Invio di commenti e suggerimenti  
 Saremmo lieti di ricevere i vostri commenti sulla technical preview. Per inviare commenti e suggerimenti sulle funzionalità di ogni anteprima, seguire il collegamento al nostro modulo per i commenti e i suggerimenti nella pagina del [programma dei commenti e suggerimenti di Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) del sito Microsoft Connect.  

 Siamo anche interessati a conoscere le vostre idee su eventuali nuove funzionalità. Per inviare nuove idee e votare le idee presentate da altri, [visitare la nostra pagina dedicata alla voce degli utenti](http://configurationmanager.uservoice.com).  

##  <a name="a-namebdmktpknownissuesa-general-changes-introduced-in-technical-previews"></a><a name="bdmk_tpknownissues"></a> Modifiche generali introdotte nelle versioni Technical Preview  

-   **Technical Preview 1603:**  

    -   A partire dalla Technical Preview 1603, è possibile configurare le distribuzioni degli aggiornamenti software in modo che i client eseguano un'analisi della conformità degli aggiornamenti software immediatamente dopo l'installazione degli aggiornamenti software e il riavvio. In questo modo, il client controlla la presenza di aggiornamenti software aggiuntivi che diventano applicabili dopo il riavvio e che possono quindi essere installati (e resi conformi) durante la stessa finestra di manutenzione.  

         Per configurare questo comportamento per una distribuzione, nella pagina **Esperienza utente** della Distribuzione guidata degli aggiornamenti software selezionare l'opzione **Se un aggiornamento di questa distribuzione richiede un riavvio del sistema, eseguire un ciclo di valutazione della distribuzione degli aggiornamenti dopo il riavvio**.  

    -   A partire dalla Technical Preview 1603, il comportamento per la variabile della sequenza di attività SMSTSRebootDelay è stato modificato. La variabile SMSTSRebootDelay specifica il tempo di attesa in secondi prima del riavvio del computer. Se questa variabile non è impostata su 0, il motore di esecuzione della sequenza di attività visualizzerà una finestra di dialogo di notifica prima del riavvio.  
        Quando si configura un valore per questa variabile, tale valore verrà mantenuto finché non si configura un nuovo valore. Il ritardo per tutti i riavvii successivi del computer avrà lo stesso valore. In Configuration Manager versione 1602 e versioni precedenti, la variabile viene reimpostata sul valore predefinito di 30 secondi dopo il riavvio del computer.   Per altre informazioni, vedere [Task sequence built-in variables in System Center Configuration Manager](../../osd/understand/task-sequence-built-in-variables.md).

-   **Technical Preview 1602:** a partire dalla Technical Preview 1602, è possibile eseguire l'aggiornamento sul posto del sistema operativo di un server del sistema del sito che esegue Windows Server 2008 R2 a Windows Server 2012 R2.  Se si usano le procedure di aggiornamento di Windows Server 2012 R2, non è necessario ripristinare il server del sito di Configuration Manager dopo l'aggiornamento.  Per le procedure di aggiornamento, vedere [Opzioni di aggiornamento per Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx).  

    > [!WARNING]  
    >  Prima di eseguire l'aggiornamento a Windows Server 2012 R2, **è necessario disinstallare WSUS 3.2** dal server.  
    >   
    >  Per informazioni su questo passaggio critico, vedere la sezione Funzionalità nuove e modificate in [Panoramica di Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx) nella documentazione di Windows Server.  

-   **Technical Preview 1601:** per impostazione predefinita, il punto di connessione del servizio viene impostato sulla modalità online quando viene installato e non supporta la modifica alla modalità offline.  





##  <a name="a-namebkmktpcapsa-capabilities-delivered-in-technical-previews"></a><a name="bkmk_tpCaps"></a> Funzionalità disponibili nelle Technical Preview  
 Di seguito sono elencate le funzionalità disponibili in ogni versione Technical Preview di Configuration Manager.  Le funzionalità disponibili a partire da una versione Technical Preview rimangono disponibili nelle versioni successive. Analogamente, le funzionalità che sono state aggiunte alla versione System Center Configuration Manager (Current Branch) rimangono disponibili nelle versioni Technical Preview successive.  Fare clic sul contenuto di ogni versione di anteprima per visualizzare altre informazioni su una funzionalità specifica.  

 |Funzionalità|Versione Technical Preview|Versione Current Branch|  
 |----------------|---------------------|--------------------|
 |Filtrare per dimensioni del contenuto nelle regole di distribuzione automatica|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|![Non aggiunta](media/Red_X.gif)|
 |Funzionalità migliorate per le finestre di dialogo del software richieste|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|![Non aggiunta](media/Red_X.gif)|
 |Negare richieste di applicazioni approvate in precedenza|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|![Non aggiunta](media/Red_X.gif)|
 |Impedire l'aggiornamento automatico dei client|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|![Non aggiunta](media/Red_X.gif)|
 |Miglioramenti a Endpoint Protection|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|![Non aggiunta](media/Red_X.gif)|
 |Aumento del numero di dispositivi registrati|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#increased-number-of-enrolled-devices)|![Non aggiunta](media/Red_X.gif)|
 |Impostazioni aggiuntive per il DEP di Apple|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|![Non aggiunta](media/Red_X.gif)|
 |Miglioramenti all'integrazione di Windows Store per le aziende con Configuration Manager|[Tech Preview 1609](capabilities-in-technical-preview-1609.md)|![Non aggiunta](media/Red_X.gif)|
 |Nuove impostazioni di conformità per gli elementi di configurazione|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|![Non aggiunta](media/Red_X.gif)|
 |Integrazione con Upgrade Analytics|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|![Non aggiunta](media/Red_X.gif)|
 |Tipi di connessione nativa per i profili ibridi VPN di Windows 10|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![Non aggiunta](media/Red_X.gif)|
 |Miglioramenti ai gruppi limite|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|![Non aggiunta](media/Red_X.gif)|
 |Dashboard di Gestione client di Office 365|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|![Non aggiunta](media/Red_X.gif)|
 |Distribuire le app di Office 365 ai client|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#ceploy-office-365-apps-to-clients)|![Non aggiunta](media/Red_X.gif)|
 |Miglioramenti alla conversione da BIOS a UEFI|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-bios-to-uefi-conversion)|![Non aggiunta](media/Red_X.gif)|
 |Grafici di conformità di Intune|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|![Non aggiunta](media/Red_X.gif)|
 |Miglioramenti del passaggio della sequenza di attività Prepara client ConfigMgr per l'acquisizione|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|![Non aggiunta](media/Red_X.gif)|
 |Miglioramenti a Software Center|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|![Non aggiunta](media/Red_X.gif)|
 |Miglioramenti ad Asset Intelligence|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|![Non aggiunta](media/Red_X.gif)|
 |Traduzione della tastiera di controllo remoto|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#remote-control-keyboard-translation)|![Non aggiunta](media/Red_X.gif)|
 |Miglioramenti al criterio di aggiornamento edizione di Windows 10|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#dmp_edition)|![Non aggiunta](media/Red_X.gif)|
 |Personalizzazione delle finestre di dialogo di Software Center|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#customizable-branding-for-software-denter-dialogs)|![Non aggiunta](media/Red_X.gif)|  
 |Punti di gestione dei dispositivi multipli per la gestione di dispositivi mobili|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_onprem)|[Versione 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#on-premises-mobile-device-management)|
 |Categorizzazione automatica dei dispositivi in raccolte|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_category)|[Version 1606](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections) |
 |Periodo di tolleranza per l'imposizione delle distribuzioni di applicazioni e aggiornamenti software obbligatorie|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_grace)|![Non aggiunta](media/Red_X.gif)|
 |Uso di Configuration Manager come programma di installazione gestito con Device Guard|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_devg)|![Non aggiunta](media/Red_X.gif)|
 |Servizio proxy cloud|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#cloud_proxy) | ![Non aggiunta](media/Red_X.gif)|  
 |Gestione dell'agente del client Office 365 in Configuration Manager|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#manage_o365) |[Versione 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#software-updates)|  
 |La variabile della sequenza di attività OSDPreserveDriveLetter è stata deprecata|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#osdpreservedriveletter) |[Versione 1606](/sccm/osd/understand/task-sequence-built-in-variables) |
 |Modifiche per il nodo Aggiornamenti e manutenzione|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#updatesandservicing)|[Versione 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#updates-and-servicing) |
 |VPN per app per dispositivi Windows 10|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PerAppVPN)|[Versione 1606](/sccm/protect/deploy-use/create-vpn-profiles)|  
 |Miglioramenti della sequenza di attività Installa aggiornamenti software|[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_InstallSU)|[Versione 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |Miglioramenti del passaggio della sequenza di attività Prepara client ConfigMgr per l'acquisizione |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_PrepareConfigMgrClient)|![Non aggiunta](media/Red_X.gif) |
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
 |Impostazioni client per gestire le impostazioni della cache del client e la peer cache del client |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_peercache)|[Versione 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#administration)|  
 |Supporto per Passport for Work come provider di archiviazione chiavi |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_passport)|[Versione 1606](/sccm/protect/deploy-use/create-certificate-profiles)|  
 |Attestazione dell'integrità del dispositivo locale|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_onpremdha)|[Versione 1606](/sccm/core/servers/manage/health-attestation)|  
 |Impostazione di Smart Lock per dispositivi Android|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_Smart)|[Versione 1606](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference)|  
 |Miglioramenti a Software Center|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_SC1603)|[Versione 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Miglioramenti del controllo remoto|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RC1603)|[Versione 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#remote-control)|  
 |Personalizzare le dimensioni della finestra e del blocco TFTP RamDisk nei punti di distribuzione abilitati per PXE|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RamDiskTFTP)|[Versione 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
 |Miglioramenti alla gestione dei dispositivi mobili|[Tech Preview 1602](capabilities-in-technical-preview-1602.md#BKMK_MDM)|[Versione 1602](/sccm/mdm/deploy-use/manage-ios-activation-lock) |  
 |Miglioramenti di Software Center nella versione 1602|[Tech Preview 1602](capabilities-in-technical-preview-1602.md#BKMK_SC1601)| [Versione 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#client-management)|  
 |Miglioramenti alla manutenzione di Windows 10|[Tech Preview 1602](capabilities-in-technical-preview-1602.md#BKMK_Win10Servicing)|[Versione 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#operating-system-deployment) |  
 |Miglioramenti all'integrazione di Microsoft Intune|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_hybrid1)|[Versione 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#conditional-access)|  
 |Stato online del client|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_clientStatus)|[Versione 1602](/sccm/core/clients/manage/monitor-clients)|
 |Miglioramenti per la gestione delle applicazioni|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_appmgmt1601)|[Versione 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#application-management)|  
 |Miglioramenti per le impostazioni di conformità|[Tech Preview 1601](capabilities-in-technical-preview-1601.md#bkmk_compliance1601)|[Versione 1602](/sccm/core/plan-design/changes/whats-new-in-version-1602#compliance-settings)|  
 |Attestazione dell'integrità dei dispositivi|[Tech Preview 1512](capabilities-in-technical-preview-1512.md#bkmk_devicehealth)|[Versione 1602](/sccm/core/servers/manage/health-attestation))|
 |Monitoraggio nella console di termini e condizioni|[Tech Preview 1512](capabilities-in-technical-preview-1512.md#bkmk_viewterms)|[Versione 1602](/sccm/mdm/deploy-use/terms-and-conditions)|  
 |Miglioramenti delle impostazioni dei criteri di Endpoint Protection|[Tech Preview 1512](capabilities-in-technical-preview-1512.md#bkmk_EPpolicy)|[Versione 1602](/sccm/protect/deploy-use/endpoint-antimalware-policies)|  
 |Integrazione con Windows Update for Business in Windows 10|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_WUfB)|[Versione 1602](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10)|  
 |Gestione dell'aggiornamento del client Office 365 ProPlus tramite System Center Configuration Manager|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_Office365ProPlus)|[Versione 1602](/sccm/sum/deploy-use/manage-office-365-proplus-updates)|  
 |Supporto per SQL Server AlwaysOn per database a disponibilità elevata|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_AlwasyOn)|[Versione 1602](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database)|  
 |Assistenza a un cluster di server|[Tech Preview 1511](capabilities-in-technical-preview-1511.md#BKMK_ClusterServerUpdates)|[Versione 1606](/sccm/sum/deploy-use/service-a-server-group)|  
## <a name="see-also"></a>Vedere anche  
[What's new in System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions) (Novità di System Center Configuration Manager)  
 [Introduction to System Center Configuration Manager](../../core/understand/introduction.md) (Introduzione a System Center Configuration Manager)



<!--HONumber=Nov16_HO1-->


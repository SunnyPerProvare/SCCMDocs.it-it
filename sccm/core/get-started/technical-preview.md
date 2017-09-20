---
title: Technical Preview per Configuration Manager | Microsoft Docs
description: "Informazioni sulla versione Technical Preview che consente di testare nuove funzionalità in System Center Configuration Manager."
ms.custom: na
ms.date: 08/25/2017
ms.prod: configuration-manager
ms.reviewer: nab
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: "157"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: e471e11b3c61172b4e9fcae74944d39aa0ab702f
ms.sourcegitcommit: 31c670a4bce74fd64a7d46ebf7702f65b80d4147
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/13/2017
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Technical Preview)*

**Pagina iniziale di System Center Configuration Manager Technical Preview**. Questo argomento include informazioni dettagliate sulla versione di anteprima in evoluzione che comprende nuove funzionalità e caratteristiche in fase di sviluppo. Ogni versione Technical Preview include nuove funzionalità che, nel momento in cui la Technical Preview viene resa disponibile, non sono ancora contenute nella versione Current Branch di System Center Configuration Manager. Tali funzionalità potranno essere inserite in seguito nella versione Current Branch. Tuttavia, prima di essere finalizzate e inserite, viene offerta all'utente la possibilità di provarle e di inviare commenti.  

 Poiché si tratta di una Technical Preview, dettagli e funzionalità sono soggetti a modifiche.  

 Questo argomento include informazioni che si applicano a tutte le versioni Technical Preview. Le informazioni sulle nuove funzionalità sono elencate in base alla versione Technical Preview in cui viene resa disponibile per la prima volta la funzionalità, ad esempio 1701 per gennaio 2017. I dettagli di queste funzionalità sono descritti in argomenti separati dedicati a ogni versione di anteprima.  

 Per informazioni sulle novità della versione Current Branch di Configuration Manager, vedere [What's new in System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012)(Novità di System Center Configuration Manager).



##  <a name="bkmk_reqs"></a> Requisiti e limitazioni per la versione Technical Preview  

> [!IMPORTANT]     
>  La Technical Preview viene concessa in licenza per essere usata esclusivamente in un ambiente lab.  Microsoft potrebbe non fornire supporto tecnico e alcune funzionalità potrebbero non essere disponibili nel software di anteprima. Inoltre, il software di anteprima potrebbe essere caratterizzato da standard di sicurezza, privacy, accessibilità, disponibilità e affidabilità ridotti o diversi rispetto al software commercializzato.  

 Per la maggior parte dei prerequisiti di prodotto, usare le informazioni disponibili in [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md) (Configurazioni supportate per System Center Configuration Manager). Per le versioni Technical Preview si applicano le seguenti eccezioni:  

-   Ogni installazione rimane attiva per 90 giorni prima di diventare inattiva.  

-   L'inglese è l'unica lingua supportata.


-   Sono supportati solo i flag di installazione (opzioni) seguenti:  

    -   **/silent**  
    -   **/testdbupgrade**    


-   Per impostazione predefinita, se si usa Technical Preview, il punto di connessione del servizio viene impostato sulla modalità online quando viene installato e non supporta il passaggio alla modalità offline.

-   Quando applicabile, sono inclusi ulteriori limitazioni o requisiti con i dettagli per ogni versione specifica della Technical Preview  

-   Non esiste alcun supporto per la migrazione a o da questa build di anteprima.  

-   Non esiste alcun supporto per l'aggiornamento a questa build di anteprima.  

-   Non esiste alcun supporto per l'aggiornamento a una build di produzione (Current Branch) da questa build di anteprima. Se sono disponibili aggiornamenti per una versione di anteprima, è tuttavia possibile trovarli e installarli dal nodo **Aggiornamenti e manutenzione** della console di Configuration Manager console. Per un video relativo al processo di aggiornamento nella console, vedere [Installazione dei pacchetti di aggiornamento di ConfigMgr](https://www.youtube.com/embed/KBd_EGFbUT8) su youtube.com.  
-   È supportato solo un sito primario autonomo. Non esiste alcun supporto per un sito di amministrazione centrale, più siti primari o i siti secondari.  

I prodotti e tecnologie seguenti sono supportati da questo ramo di Configuration Manager. Il loro inserimento in questo contesto, tuttavia, non implica un'estensione del normale ciclo di vita del supporto per un singolo prodotto o versione. I prodotti che non rientrano nel ciclo di vita del supporto non sono supportati per l'uso con Configuration Manager. Per altre informazioni sui cicli di vita del supporto Microsoft, visitare il sito Web [Ciclo di vita del supporto Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270) .  

-   Sono supportate solo le seguenti versioni di SQL Server:  

    -   SQL Server 2016 (senza Service Pack e versioni successive)
    -   SQL Server 2014 (con Service Pack 1 o versioni successive)
    -   SQL Server 2012 (con Service Pack 3 o versioni successive)


-   Il sito supporta fino a 10 client, che devono eseguire uno dei seguenti sistemi operativi:  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 8  
      -   Windows 7  

##  <a name="bkmk_install"></a> Installare e aggiornare la versione Technical Preview  
 System Center Configuration Manager Technical Preview è diversa dalla versione corrente di System Center Configuration Manager.  

 Per usare la Technical Preview è innanzitutto necessario installare una **versione di base** della build Technical Preview. Dopo l'installazione di una versione di base, sarà quindi possibile usare gli **aggiornamenti nella console** per aggiornare l'installazione con la versione di anteprima più recente.     In genere, le nuove versioni Technical Preview sono disponibili ogni mese.

Ogni versione di anteprima è supportata finché non sono disponibili fino a tre versioni successive. Pertanto, quando viene rilasciata la versione 1708, la versione 1704 non è più supportata, mentre rimangono supportate le versioni 1705, 1706 e 1707. Quando una linea di base non rientra più nel supporto (come nel caso della versione 1703), è ancora disponibile il supporto per l'installazione di un nuovo sito Technical Preview (fino a quando non è disponibile una nuova versione di base), a condizione che tale istallazione venga aggiornata a una versione supportata. Durante l'aggiornamento, se non viene visualizzata la versione più recente disponibile nella console, eseguire l'aggiornamento alla versione più recente offerta e quindi ripetere il processo fino a quando non è possibile installare la versione più recente della Technical Preview.

> [!TIP]  
>  Quando si installa un aggiornamento per la Technical Preview, si aggiorna l'installazione di anteprima alla nuova versione Technical Preview.    Un'installazione Technical Preview non prevede mai la possibilità di eseguire l'aggiornamento a un'installazione del ramo corrente, né di ricevere gli aggiornamenti dalla versione ramo corrente.  

**Versioni di base della Technical Preview attive:**  
È possibile installare una versione di base per un massimo di 1 anno dopo il rilascio. Tuttavia, quando si installa un nuovo sito Technical Preview, è consigliabile usare l'ultima versione di base disponibile.
-  **Technical Preview 1703**: Configuration Manager Technical Preview 1703 è disponibile sia come aggiornamento nella console per Configuration Manager Technical Preview, sia come nuova versione di base sul [sito Web TechNet Evaluation Center](http://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

<!-- out of support. Use baseline 1703
-  **Technical Preview 1610** - The Configuration Manager Technical Preview 1610 was available as both an in-console update for the Configuration Manager Technical Preview, and as a baseline version. If you have media for installing 1610, we recommend you download version 1703 and install that version instead.
-->



##  <a name="BKMK_TPFeedback"></a> Invio di commenti e suggerimenti  
 Saremmo lieti di ricevere i vostri commenti sulla technical preview. Per inviare commenti e suggerimenti sulle funzionalità di ogni anteprima, seguire il collegamento al nostro modulo per i commenti e i suggerimenti nella pagina del [programma dei commenti e suggerimenti di Configuration Manager](https://connect.microsoft.com/ConfigurationManagervnext/Feedback) del sito Microsoft Connect.  

 Siamo anche interessati a conoscere le vostre idee su eventuali nuove funzionalità. Per inviare nuove idee e votare le idee presentate da altri, [visitare la nostra pagina dedicata alla voce degli utenti](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Funzionalità disponibili nelle Technical Preview più recente  
 Di seguito sono elencate le funzionalità disponibili in ogni versione Technical Preview di Configuration Manager.  Le funzionalità disponibili a partire da una versione Technical Preview rimangono disponibili nelle versioni successive. Analogamente, le funzionalità che sono state aggiunte alla versione System Center Configuration Manager (Current Branch) rimangono disponibili nelle versioni Technical Preview successive.  Fare clic sul contenuto di ogni versione di anteprima per visualizzare altre informazioni su una funzionalità specifica.  

 |Funzionalità |Versione Technical Preview |Versione Current Branch|  
 |----------------|---------------------|--------------------|
 |Miglioramenti per specificare i parametri degli script quando si distribuiscono gli script di PowerShell da Configuration Manager <!-- 1236459 -->|[Tech Preview 1708](capabilities-in-technical-preview-1708.md#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager)|![Non aggiunta](media/Red_X.gif)|
 |Informazioni dettagliate sulla gestione <!-- 1353967 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#management-insights)|![Non aggiunta](media/Red_X.gif)|
 |Riavviare i computer dalla console di Configuration Manager <!-- 1356283 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#restart-computers-from-the-configuration-manager-console)|![Non aggiunta](media/Red_X.gif)|
 |Personalizzazione di Software Center <!-- 1351224 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#software-center-customization)|![Non aggiunta](media/Red_X.gif)|


## <a name="capabilities-delivered-in-previous-technical-previews"></a>Funzionalità disponibili nelle Technical Preview precedenti
 Quando tutte le funzionalità di una versione di Technical Preview sono disponibili nella versione minima supportata del Current Branch, i dettagli per tale versione di anteprima vengono rimossi dalla tabella seguente.  

 |Funzionalità |Versione Technical Preview |Versione Current Branch|  
 |----------------|---------------------|--------------------|
 |Supporto della peer cache del client per i file di installazione rapida per Windows 10 e Office 365|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365)|![Non aggiunta](media/Red_X.gif)|
 |Dashboard del dispositivo Surface|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#surface-device-dashboard)|![Non aggiunta](media/Red_X.gif)|
 |Configurare e distribuire i criteri di Windows Defender Application Guard|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#configure-and-deploy-windows-defender-application-guard-policies)|![Non aggiunta](media/Red_X.gif)|
 |Aggiungere i parametri quando si distribuiscono gli script di PowerShell da Configuration Manager|[Tech Preview 1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager)|![Non aggiunta](media/Red_X.gif)|
 |Nuove impostazioni dei criteri di gestione delle applicazioni mobili|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#new-mobile-application-management-policy-settings)|![Non aggiunta](media/Red_X.gif)|
 |Gruppi di limiti migliorati per i punti di aggiornamento software|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#improved-boundary-groups-for-software-update-points)|[Versione 1706](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)|
 |Disponibilità elevata per il ruolo del server del sito|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |![Non aggiunta](media/Red_X.gif)|
 |Includere attendibilità per file e cartelle specifici in un criterio di Device Guard|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#include-trust-for-specific-files-and-folders-in-a-device-guard-policy)|[Versione 1706](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|
 |Nascondere l’avanzamento della sequenza di attività|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#hide-task-sequence-progress)|![Non aggiunta](media/Red_X.gif)|
 |Specificare un percorso del contenuto diverso per il contenuto di installazione e il contenuto di disinstallazione|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#specify-a-different-content-location-for-install-content-and-uninstall-content)|[Versione 1706](/sccm/core/get-started/capabilities-in-technical-preview-1706#hide-task-sequence-progress)|
 |Miglioramenti all'accessibilità |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#accessibility-improvements)|[Versione 1706](/sccm/core/understand/accessibility-features)|
 |Supporto per la procedura guidata per i servizi di Azure per Preparazione aggiornamenti |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#changes-to-the-azure-services-wizard-to-support-upgrade-readiness)|[Versione 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |Nuove impostazioni client per i servizi cloud|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#new-client-settings-for-cloud-services)|[Versione 1706](/sccm/core/clients/deploy/deploy-clients-cmg-azure)|
 |Creare ed eseguire script di PowerShell dalla console di Configuration Manager|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console)|[Versione 1706](/sccm/apps/deploy-use/create-deploy-scripts)|
 |Supporto dell'avvio della rete PXE per IPv6 |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|![Non aggiunta](media/Red_X.gif)|
 |Gestire gli aggiornamenti dei driver di Microsoft Surface |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#manage-microsoft-surface-driver-updates)|[Versione 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#manage-microsoft-surface-driver-updates)|
 |Configurare i criteri di rinvio di Windows Update for Business |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#configure-windows-update-for-business-deferral-policies)|[Versione 1706](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies)|
 |Restrizioni di registrazione per iOS|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#android-and-ios-enrollment-restrictions)|[Versione 1706](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac#configure-enrollment-restrictions)|
 |Restrizioni di registrazione per Android|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#android-and-ios-enrollment-restrictions)|[Versione 1706](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-enrollment)|
 |Criteri per la gestione dell'applicazione Android for Work per il copia e incolla|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#android-for-work-application-management-policy-for-copy-paste)|[Versione 1706](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client#android-for-work-configuration-item-settings-reference)|
 |Nuove impostazioni dell’elemento di configurazione di Windows|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#new-windows-configuration-item-settings)|[Versione 1706](/sccm/mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |Nuove regole per i criteri di conformità dei dispositivi|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#new-device-compliance-policy-rules)|[Versione 1706](/sccm/mdm/deploy-use/create-compliance-policy)|
 |Valutazione dell'attestazione dell'integrità dei dispositivi per i criteri di conformità per l'accesso condizionale|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#device-health-attestation-assessment-for-compliance-policies-for-conditional-access)|![Non aggiunta](media/Red_X.gif)|
 |Supporto per le autorità di certificazione Entrust|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#support-for-entrust-certification-authorities)|[Versione 1706](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)|
 |Supporto Cisco (IPsec) per i profili VPN di MacOS|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#cisco-ipsec-support-for-macos-vpn-profiles)|[Versione 1706](/sccm/protect/deploy-use/vpn-profiles)|
 |Nuove funzionalità per la gestione di Azure AD e del cloud|[Tech Preview 1705](capabilities-in-technical-preview-1705.md#new-capabilities-for-azure-ad-and-cloud-management)|[Versione 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#azure-ad-integration-with-configuration-manager)|
 |Configurare e distribuire i criteri di Windows Defender Application Guard|[Tech Preview 1705](capabilities-in-technical-preview-1705.md#configure-and-deploy-windows-defender-application-guard-policies)|![Non aggiunta](media/Red_X.gif)|
 |Strumento di reimpostazione dell'aggiornamento  |[Tech Preview 1705](capabilities-in-technical-preview-1705.md#update-reset-tool)|[Versione 1706](/sccm/core/servers/manage/update-reset-tool)|
 |Supporto per console con DPI elevato  |[Tech Preview 1705](capabilities-in-technical-preview-1705.md#high-dpi-console-support)|[Versione 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#high-dpi-console-support)|
 |Miglioramenti della peer cache  |[Tech Preview 1705](capabilities-in-technical-preview-1705.md#peer-cache-improvements) |[Versione 1706](/sccm/core/plan-design/hierarchy/client-peer-cache#requirements-and-considerations-for-peer-cache)|
 |Miglioramenti per i gruppi di disponibilità Always On di SQL Server |[Tech Preview 1705](capabilities-in-technical-preview-1705.md#improvements-for-sql-server-always-on-availability-groups) |[Versione 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#improvements-for-sql-server-always-on-availability-groups)|
 |Notifiche utente migliorate per gli aggiornamenti di Office 365|[Tech Preview 1705](capabilities-in-technical-preview-1705.md#improved-user-notifications-for-office-365-updates) |[Versione 1706](/sccm/sum/deploy-use/manage-office-365-proplus-updates#restart-behavior-and-client-notifications-for-office-365-updates)|
 |Usare la Procedura guidata Servizi di Azure per configurare una connessione a OMS|[Tech Preview 1705](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) |[Versione 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |Configurare le app Android con i criteri di configurazione delle app  |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#configure-android-apps-with-app-configuration-policies)|![Non aggiunta](media/Red_X.gif)|
 |L'inventario hardware raccoglie le informazioni di Avvio protetto |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#hardware-inventory-collects-secure-boot-information)|[Versione 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#hardware-inventory-collects-secure-boot-information)|
 |Aggiungere sequenze di attività figlio a una sequenza di attività|[Tech Preview 1704](capabilities-in-technical-preview-1704.md#add-child-task-sequences-to-a-task-sequence)|![Non aggiunta](media/Red_X.gif)|
 |Ricaricare immagini di avvio con la versione corrente di Windows PE |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#reload-boot-images-with-current-windows-pe-version)|[Versione 1706](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image)|
 |Miglioramenti alla distribuzione del sistema operativo <!-- This item does not track to be added to the Current Branch. It is covered by various other incremental work. --> |[Tech Preview 1704](capabilities-in-technical-preview-1704.md#improvements-to-operating-system-deployment)|![Non aggiunta](media/Red_X.gif)|
 |Distribuire app iOS acquistate con Volume Purchase Program a raccolte di dispositivi|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#deploy-volume-purchased-ios-apps-to-device-collections)|[Versione 1702](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)|
 |Collegamenti diretti alle applicazioni in Software Center|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#direct-links-to-applications-in-software-center)|[Versione 1706](/sccm/apps/deploy-use/share-applications)
 |Certificati PFX per i computer client Windows di Configuration Manager|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#pfx-certificates-for-configuration-manager-windows-client-computers)|[Versione 1706](/sccm/protect/deploy-use/create-certificate-profiles)|
 |Configurazione guidata servizi di Azure|[Tech Preview 1703](capabilities-in-technical-preview-1703.md#configure-azure-services-wizard)|[Versione 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |Conversione da BIOS a UEFI in una sequenza di attività di aggiornamento del sistema operativo| [Tech Preview 1703](capabilities-in-technical-preview-1703.md#convert-from-bios-to-uefi-during-an-in-place-upgrade) |[Versione 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade)|
 |Gruppi di sequenze di attività comprimibili| [Tech Preview 1703](capabilities-in-technical-preview-1703.md#collapsible-task-sequence-groups) |[Versione 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706#collapsible-task-sequence-groups)|
 |Impostazioni client per configurare Windows Analytics per Upgrade Readiness | [Tech Preview 1703](capabilities-in-technical-preview-1703.md#client-settings-to-configure-windows-analytics-for-upgrade-readiness) |[Versione 1706](/sccm/core/clients/manage/monitor-windows-analytics#configure-clients-to-report-data-to-windows-analytics)|
 |Nuove impostazioni di conformità per i dispositivi iOS|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#new-compliance-settings-for-ios-devices)|[Versione 1702](/sccm/mdm/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client)|
 |Creare certificati PFX con il supporto di S/MIME|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#create-pfx-certificates-with-s-mime-support)|[Versione 1706](/sccm/mdm/deploy-use/create-pfx-certificate-profiles)|
 |Controllare l'esecuzione di file eseguibili prima di installare un'applicazione|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#check-for-running-executable-files-before-installing-an-application)|[Versione 1702](/sccm/apps/deploy-use/deploy-applications)|
 |Inviare commenti e suggerimenti dalla console di Configuration Manager | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#send-feedback-from-the-configuration-manager-console)    |[Versione 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#send-feedback-from-the-configuration-managercconsole)  |
 |Modifiche per Aggiornamenti e manutenzione  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#changes-for-updates-and-servicing)  |[Versione 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#changes-for-updates-and-servicing) |
 |Miglioramenti della peer cache  | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#peer-cache-improvements) |[Versione 1702](/sccm/core/plan-design/hierarchy/client-peer-cache)|
 |Uso di Azure Active Directory <!-- This item does not track to be added to the Current Branch. It is covered by various other incremental work. --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |![Non aggiunta](media/Red_X.gif)|
 |Miglioramenti dei criteri di conformità dei dispositivi per accesso condizionale | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#conditional-access-device-compliance-policy-improvements) |[Versione 1702](/sccm/mdm/deploy-use/create-compliance-policy)|
 |Avviso della versione del client antimalware | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert) |[Versione 1702](/sccm/protect/deploy-use/endpoint-configure-alerts?branch=live#alert-for-outdated-malware-client)|
 |Valutazione della conformità degli aggiornamenti di Windows Update for Business | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |![Non aggiunta](media/Red_X.gif)|
 |Miglioramenti alle impostazioni e ai messaggi di notifica di Software Center per le sequenze di attività a impatto elevato|[Tech Preview 1702](capabilities-in-technical-preview-1702.md#antimalware-client-version-alert)|[Versione 1702](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#set-a-task-sequence-as-a-high-impact-task-sequence)|
 |Supporto per Android for Work| [Tech Preview 1702](capabilities-in-technical-preview-1702.md#android-for-work-support) |[Versione 1702](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-for-work-enrollment)|
 |Miglioramenti dei gruppi di limiti per i punti di aggiornamento software | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#boundary-groups-improvements-for-software-update-points)    |[Versione 1702](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points)  |
 |L'inventario hardware raccoglie le informazioni UEFI | [Tech Preview 1701](capabilities-in-technical-preview-1701.md#hardware-inventory-collects-uefi-information)|[Versione 1702](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#hardware-inventory-collects-uefi-information) |
 |Miglioramenti alla distribuzione del sistema operativo| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#improvements-to-operating-system-deployment)|[Versione 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment) |
 |Ospitare gli aggiornamenti software in punti di distribuzione basati sul cloud| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#host-software-updates-on-cloud-based-distribution-points)|[Versione 1702](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#plan-to-use-a-cloud-based-distribution-point) |
 |Convalidare i dati di attestazione dell'integrità del dispositivo tramite punti di gestione| [Tech Preview 1701](capabilities-in-technical-preview-1701.md#validate-device-health-attestation-data-via-management-points)| [Versione 1702](/sccm/core/servers/manage/health-attestation) |
 |Connettore OMS per il cloud di Microsoft Azure per enti pubblici |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#use-the-oms-connector-for-microsoft-azure-government-cloud) |[Versione 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig) |
 |Non è più necessario specificare le versioni di Android e iOS nella creazione guidata |[Tech Preview 1701](capabilities-in-technical-preview-1701.md#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |[Versione 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm) |
 |Accesso ai dati di endpoint OData |[Technical Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|![Non aggiunta](media/Red_X.gif)|
 |Punto di servizio Data Warehouse |[Technical Preview 1612](capabilities-in-technical-preview-1612.md#the-data-warehouse-service-point)|[Versione 1702](/sccm/core/servers/manage/data-warehouse)|
 |Strumento di pulizia della raccolta contenuto |[Technical Preview 1612](capabilities-in-technical-preview-1612.md#content-library-cleanup-tool)|[Versione 1702](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) |
 |Miglioramenti per la ricerca nella console |[Technical Preview 1612](capabilities-in-technical-preview-1612.md#improvements-for-in-console-search)|[Versione 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-for-in-console-search)|
 |Evitare l'installazione di un'applicazione se è in esecuzione un programma specifico|[Technical Preview 1612](capabilities-in-technical-preview-1612.md#prevent-installation-of-an-application-if-a-specified-program-is-running)|[Versione 1702](/sccm/apps/deploy-use/deploy-applications)|
 |Nuova notifica di Windows Hello for Business per gli utenti finali|[Technical Preview 1612](capabilities-in-technical-preview-1612.md#new-windows-hello-for-business-notification-for-end-users)|[Versione 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#new-windows-hello-for-business-notification-for-end-users)|
 |Supporto di Windows Store for Business in Configuration Manager|[Technical Preview 1612](capabilities-in-technical-preview-1612.md#windows-store-for-business-support-in-configuration-manager)|[Versione 1702](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |Tornare alla pagina precedente quando si verifica un errore di una sequenza di attività|[Technical Preview 1612](capabilities-in-technical-preview-1612.md#return-to-previous-page-when-a-task-sequence-fails)|[Versione 1702](/sccm/core/plan-design/changes/whats-new-in-version-1702#operating-system-deployment)|
 |Supporto per i file di installazione rapida per gli aggiornamenti di Windows 10|[Technical Preview 1612](capabilities-in-technical-preview-1612.md#express-installation-files-support-for-windows-10-updates)|[Versione 1702](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates)|
 |Onboarding di Azure Active Directory|[Technical Preview 1612](capabilities-in-technical-preview-1612.md#azure-active-directory-onboarding)|[Versione 1706](/sccm/core/servers/deploy/configure/azure-services-wizard)|
 |Modifica alla configurazione dell'autenticazione a più fattori per la registrazione dei dispositivi|[Technical Preview 1612](capabilities-in-technical-preview-1612.md#change-to-configuring-multi-factor-authentication-for-device-enrollment)|![Non aggiunta](media/Red_X.gif)|
 |Pre-cache del contenuto per le distribuzioni e le sequenze di attività |[Technical Preview 1611](capabilities-in-technical-preview-1611.md#pre-cache-content-for-available-deployments-and-task-sequences)|[Versione 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
 |Impostazioni di configurazione di Windows Defender|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#windows-defender-configuration-settings)|[Versione 1610](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client)|
 |Richiedere la sincronizzazione dei criteri dalla console di amministrazione|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#request-policy-sync-from-administrator-console)|[Versione 1610](/sccm/mdm/deploy-use/sync-intune-device)|
 |Supporto di ruoli di sicurezza aggiuntivi per il nodo Dispositivi di proprietà dell'azienda|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#additional-security-role-support)|[Versione 1610](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management#new-hybrid-features-in-november-2016)|
 |Accesso condizionale per profili VPN di Windows 10|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#conditional-access-for-windows-10-vpn-profiles)|[Versione 1610](/sccm/protect/deploy-use/create-vpn-profiles#configure-the-authentication-method-for-the-vpn-profile)|
 |Filtrare per dimensioni del contenuto nelle regole di distribuzione automatica|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#filter-by-content-size-in-automatic-deployment-rules)|[Versione 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#filter-by-content-size-in-automatic-deployment-rules) |
 |Funzionalità migliorate per le finestre di dialogo del software richieste|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#improved-functionality-for-required-software-dialogs)|[Versione 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Negare richieste di applicazioni approvate in precedenza|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#deny-previously-approved-application-requests)|[Versione 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Impedire l'aggiornamento automatico dei client|[Tech Preview 1610](capabilities-in-technical-preview-1610.md#exclude-clients-from-automatic-upgrade)|[Versione 1610](/sccm/core/clients/manage/upgrade/exclude-clients-windows)|
 |Miglioramenti a Endpoint Protection|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-to-endpoint-protection)|[Versione 1610](/sccm/protect/deploy-use/endpoint-antimalware-policies#cloud-protection-service)|
 |Aumento del numero di dispositivi registrati|[Tech Preview 1609](/sccm/mdm/deploy-use/enable-platform-enrollment)|[Versione 1610](/sccm/mdm/deploy-use/enable-platform-enrollment)|
 |Impostazioni aggiuntive per il DEP di Apple|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#additional-apple-dep-settings)|[Versione 1610](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)|
 |Miglioramenti all'integrazione di Windows Store per le aziende con Configuration Manager|[Tech Preview 1609](capabilities-in-technical-preview-1609.md)|[Versione 1610](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|
 |Nuove impostazioni di conformità per gli elementi di configurazione|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#new-compliance-settings-for-configuration-items)|[Versione 1610](/sccm/compliance/deploy-use/create-configuration-items)|
 |Integrazione con Upgrade Analytics|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#integration-with-upgrade-analytics)|[Versione 1610](/sccm/core/clients/manage/upgrade/upgrade-analytics)|
 |Tipi di connessione nativa per i profili ibridi VPN di Windows 10|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#native-connection-types-for-windows-10-vpn-hybrid-profiles)|![Non aggiunta](media/Red_X.gif)|
 |Miglioramenti ai gruppi limite|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#improvements-for-boundary-groups)|[Versione 1610](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#BKMK_BoundaryGroups)|
 |Dashboard di Gestione client di Office 365|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#office-365-client-management-dashboard)|[Versione 1610](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard)|
 |Distribuire le app di Office 365 ai client|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#deploy-office-365-apps-to-clients)|[Versione 1702](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps)|
 |Miglioramenti alla conversione da BIOS a UEFI|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#BKMK_UEFIConversion)|[Versione 1610](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion)|
 |Grafici di conformità di Intune|[Tech Preview 1609](capabilities-in-technical-preview-1609.md#intune-compliance-charts)|[Versione 1610](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)|
 |Miglioramenti del passaggio della sequenza di attività Prepara client ConfigMgr per l'acquisizione|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-the-prepare-configmgr-client-for-capture-task-sequence-step)|[Versione 1610](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture)|
 |Miglioramenti a Software Center|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-software-center)|[Versione 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#general-improvements-to-software-center)|
 |Miglioramenti di Asset Intelligence <!-- Listed as TBD. No planned addition to Current Branch -->|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|![Non aggiunta](media/Red_X.gif)|
 |Traduzione della tastiera di controllo remoto|[Tech Preview 1608](capabilities-in-technical-preview-1608.md#remote-control-keyboard-translation)| [Versione 1610](/sccm/core/clients/manage/remote-control/configuring-remote-control#enable-keyboard-translation)|
 |Miglioramenti al criterio di aggiornamento edizione di Windows 10|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#dmp_edition)|[Versione 1610](/sccm/compliance/deploy-use/upgrade-windows-version)|
 |Personalizzazione delle finestre di dialogo di Software Center|[Tech Preview 1607](capabilities-in-technical-preview-1607.md#customizable-branding-for-software-center-dialogs)|[Versione 1610](/sccm/core/plan-design/changes/whats-new-in-version-1610#customizable-branding-for-software-center-dialogs)|  
 |Punti di gestione dei dispositivi multipli per la gestione di dispositivi mobili|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_onprem)|[Versione 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#on-premises-mobile-device-management)|
 |Categorizzazione automatica dei dispositivi in raccolte|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_category)|[Version 1606](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections) |
 |Periodo di tolleranza per l'imposizione delle distribuzioni di applicazioni e aggiornamenti software obbligatorie|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_grace)|[Versione 1610](/sccm/apps/deploy-use/deploy-applications)|
 |Uso di Configuration Manager come programma di installazione gestito con Device Guard|[Tech Preview 1606](capabilities-in-technical-preview-1606.md#dmp_devg)|[Versione 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager )|
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

 <!--  TP 1604 and earlier has aged out of support and all features are in Current Branch builds:
 |Manage volume-purchased apps from the Windows Store for Business| [Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_WindowsVPP)|[Version 1606](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)|  
 |Improvements to Microsoft Passport for Work management|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_PFW)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#device-configuration-and-protection)|  
 |Option for clients to switch to a new software update point|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_switchsup)|[Version 1606](/sccm/sum/plan-design/plan-for-software-updates#BKMK_ManuallySwitchSUPs)|  
 |Client settings to manage Client Cache Settings and client Peer Cache |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_peercache)|Client Settings: [Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#administration)<br/>Peer Cache: [Version 1610](/sccm/core/plan-design/hierarchy/client-peer-cache)|  
 |Support for Passport for Work as a KSP |[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_passport)|[Version 1606](/sccm/protect/deploy-use/create-certificate-profiles)|  
 |On-premises Device Health Attestation|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#bkmk_onpremdha)|[Version 1606](/sccm/core/servers/manage/health-attestation)|  
 |SmartLock setting for Android devices|[Tech Preview 1604](capabilities-in-technical-preview-1604.md#BKMK_Smart)|[Version 1606](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-and-samsung-knox-configuration-item-settings-reference)|  
 |Improvements to Software Center|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_SC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#application-management)|  
 |Improvements to remote control|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RC1603)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#remote-control)|  
 |Customize the RamDisk TFTP block size and window size on PXE-enabled distribution points|[Tech Preview 1603](capabilities-in-technical-preview-1603.md#BKMK_RamDiskTFTP)|[Version 1606](/sccm/core/plan-design/changes/whats-new-in-version-1606#operating-system-deployment)|  
-->



## <a name="see-also"></a>Vedere anche  
[What's new in System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions) (Novità di System Center Configuration Manager)  
 [Introduction to System Center Configuration Manager](../../core/understand/introduction.md) (Introduzione a System Center Configuration Manager)

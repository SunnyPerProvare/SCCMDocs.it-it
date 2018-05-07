---
title: Versioni di Technical Preview
titleSuffix: Configuration Manager
description: Informazioni sulla versione Technical Preview che consente di testare nuove funzionalità in Configuration Manager.
ms.date: 04/25/2018
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 157
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 79a535bd9ee7f597e551c2d4f84c39c84ecf262f
ms.sourcegitcommit: d67c6246bb6027cd5501e772b0521f9272407c28
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2018
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Technical Preview)*

**Pagina iniziale di System Center Configuration Manager Technical Preview**. Questo articolo include informazioni dettagliate sulla versione di anteprima in evoluzione che comprende nuove funzionalità e caratteristiche in fase di sviluppo. Ogni versione Technical Preview presenta nuove funzionalità non incluse nella versione Current Branch di Configuration Manager nel momento in cui diventa disponibile la versione Technical Preview. Tali funzionalità potranno essere inserite in seguito nella versione Current Branch. Tuttavia, prima di essere finalizzate e inserite, viene offerta all'utente la possibilità di provarle e di inviare commenti.  

 Poiché questa versione è una Technical Preview, dettagli e funzionalità sono soggetti a modifiche.  

 Questo articolo contiene informazioni valide per tutte le versioni della Technical Preview. Le informazioni sulle nuove funzionalità sono elencate in base alla versione della Technical Preview in cui viene resa disponibile per la prima volta la funzionalità, ad esempio la versione 1804 per aprile 2018. I dettagli di queste funzionalità sono presentati in argomenti separati dedicati a ogni versione di anteprima.  

 Per informazioni sulle novità della versione Current Branch di Configuration Manager, vedere [What's new in System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012)(Novità di System Center Configuration Manager).



##  <a name="bkmk_reqs"></a> Requisiti e limitazioni per la versione Technical Preview  

> [!IMPORTANT]     
>  La Technical Preview viene concessa in licenza per essere usata esclusivamente in un ambiente lab.  Microsoft potrebbe non offrire supporto tecnico e alcune funzionalità potrebbero non essere disponibili nel software di anteprima. Inoltre, il software di anteprima può essere caratterizzato da standard di sicurezza, privacy, accessibilità, disponibilità e affidabilità ridotti o diversi rispetto al software commercializzato.  

 Per la maggior parte dei prerequisiti di prodotto, usare le informazioni disponibili in [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md) (Configurazioni supportate per System Center Configuration Manager). Per le versioni Technical Preview si applicano le seguenti eccezioni:  

-   Ogni installazione rimane attiva per 90 giorni prima di diventare inattiva.  

-   L'inglese è l'unica lingua supportata.


-   Sono supportati solo i flag di installazione (opzioni) seguenti:  

    -   **/silent**  
    -   **/testdbupgrade**    


-   Per impostazione predefinita, quando si usa la versione Technical Preview, il punto di connessione del servizio viene installato in modalità online. Non supporta il passaggio alla modalità offline.

-   Gli articoli separati per ogni versione specifica della Technical Preview includono ulteriori limitazioni o requisiti, secondo il caso.

-   Non esiste alcun supporto per la migrazione a o da questa build di anteprima.  

-   Non esiste alcun supporto per l'aggiornamento a questa build di anteprima. 

-   Non esiste alcun supporto per il ripristino sito dalla cartella cd.latest.  <!--507106-->

-   Non esiste alcun supporto per l'aggiornamento a una build di produzione (Current Branch) da questa build di anteprima. Se sono disponibili aggiornamenti per una versione di anteprima, è tuttavia possibile trovarli e installarli dal nodo **Aggiornamenti e manutenzione** della console di Configuration Manager console. Per un video relativo al processo di aggiornamento nella console, vedere [Installazione dei pacchetti di aggiornamento di ConfigMgr](https://www.youtube.com/embed/KBd_EGFbUT8) su youtube.com.  
-   È supportato solo un sito primario autonomo. Non esiste alcun supporto per un sito di amministrazione centrale, più siti primari o i siti secondari.  

I prodotti e tecnologie seguenti sono supportati da questo ramo di Configuration Manager. Il loro inserimento in questo contesto, tuttavia, non implica un'estensione del normale ciclo di vita del supporto per un singolo prodotto o versione. I prodotti che non rientrano nel ciclo di vita del supporto non sono supportati per l'uso con Configuration Manager. Per altre informazioni sui cicli di vita del supporto Microsoft, visitare il sito Web [Ciclo di vita del supporto Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270) .  

-   Sono supportate solo le seguenti versioni di SQL Server:  

    -   SQL Server 2017 (con aggiornamento cumulativo 2 e versioni successive) a partire da Configuration Manager versione 1710
    -   SQL Server 2016 (senza Service Pack e versioni successive)
    -   SQL Server 2014 (con Service Pack 1 o versioni successive)
    -   SQL Server 2012 (con Service Pack 3 o versioni successive)


-   Il sito supporta fino a 10 client, che devono eseguire una delle seguenti versioni di Windows:  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 7  

##  <a name="bkmk_install"></a> Installare e aggiornare la versione Technical Preview  
 System Center Configuration Manager Technical Preview è diversa dalla versione corrente di System Center Configuration Manager.  

 Per usare la Technical Preview è innanzitutto necessario installare una **versione di base** della build Technical Preview. Dopo l'installazione di una versione di base, è possibile usare gli **aggiornamenti nella console** per aggiornare l'installazione con la versione di anteprima più recente. In genere, le nuove versioni Technical Preview sono disponibili ogni mese.

Ogni versione di anteprima è supportata finché non sono disponibili fino a tre versioni successive. Pertanto, quando viene rilasciata la versione 1708, la versione 1704 non è più supportata, mentre rimangono supportate le versioni 1705, 1706 e 1707. Quando una versione di base non rientra più nel supporto, è ancora disponibile il supporto per l'installazione di un nuovo sito Technical Preview finché non è disponibile una nuova versione di base, a condizione che tale installazione in seguito venga aggiornata a una versione supportata. Eseguire l'aggiornamento alla versione più recente disponibile, quindi ripetere la procedura fino a quando non è possibile installare la versione più recente della Technical Preview.

> [!TIP]  
>  Quando si installa un aggiornamento della Technical Preview, si aggiorna l'installazione di anteprima alla nuova versione Technical Preview. Un'installazione Technical Preview non prevede mai la possibilità di eseguire l'aggiornamento a un'installazione Current Branch, né di ricevere gli aggiornamenti dalla versione Current Branch corrente.  

**Versioni di base della Technical Preview attive:**
   
È possibile installare una versione di base al massimo per un anno dopo il rilascio. Tuttavia, quando si installa un nuovo sito Technical Preview, è consigliabile usare l'ultima versione di base disponibile.
-  **Technical Preview 1711**: Configuration Manager Technical Preview 1711 è disponibile sia come aggiornamento nella console, sia come nuova versione di base. Scaricare le versioni di base [dal TechNet Evaluation Center](http://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).


##  <a name="BKMK_TPFeedback"></a> Invio di commenti e suggerimenti  
 Saremmo lieti di ricevere i vostri commenti sulle funzionalità della Technical Preview. Per altre informazioni, vedere la sezione su [commenti e suggerimenti per i prodotti](../understand/find-help.md#product-feedback).

Siamo anche interessati a conoscere le vostre idee su eventuali nuove funzionalità. Per inviare nuove idee e votare le idee presentate da altri, [visitare la nostra pagina dedicata alla voce degli utenti](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Funzionalità disponibili nelle Technical Preview più recente  
Di seguito sono elencate le funzionalità disponibili nella versione più recente della Technical Preview di Configuration Manager.  Le funzionalità disponibili in una versione precedente della Technical Preview rimangono disponibili nelle versioni successive. Analogamente, le funzionalità aggiunte alla versione Current Branch di Configuration Manager rimangono disponibili nelle versioni Technical Preview.  Fare clic sul contenuto di ogni versione di anteprima per visualizzare altre informazioni su una funzionalità specifica.  

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1804"></a>Technical Preview versione 1804
- [Configurare una raccolta contenuto remota per il server del sito](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server) <!--1357525--> 
- [Inviare commenti e suggerimenti dalla console di Configuration Manager](capabilities-in-technical-preview-1804.md#bkmk_feedback) <!--1357542--> 
- [Support Center](capabilities-in-technical-preview-1804.md#support-center) <!--1357489--> 
- [Configuration Manager Toolkit](capabilities-in-technical-preview-1804.md#configuration-manager-toolkit) <!--1357145--> 
- [Disinstallare l'applicazione in caso di revoca dell'approvazione](capabilities-in-technical-preview-1804.md#uninstall-application-on-approval-revocation) <!--1357891--> 
- [Escludere i contenitori di Active Directory dall'individuazione](capabilities-in-technical-preview-1804.md#exclude-active-directory-containers-from-discovery) <!--1358143--> 
- [Specificare la visibilità del collegamento del sito Web del Catalogo applicazioni in Software Center](capabilities-in-technical-preview-1804.md#specify-the-visibility-of-the-application-catalog-website-link-in-software-center) <!--1358214--> 
- [Filtrare le regole di distribuzione automatica in base all'architettura di aggiornamento software](capabilities-in-technical-preview-1804.md#filter-automatic-deployment-rules-by-software-update-architecture) <!--1322266--> 
- [Miglioramenti della distribuzione del sistema operativo](capabilities-in-technical-preview-1804.md#improvements-to-os-deployment) <!--1358330,1358493--> 
- [Miglioramenti della console di Configuration Manager](capabilities-in-technical-preview-1804.md#improvements-to-the-configuration-manager-console) <!--510252--> 



## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>Funzionalità disponibili nelle Technical Preview supportate recenti
Di seguito sono elencate le funzionalità disponibili nelle versioni della Technical Preview di Configuration Manager ancora supportate. 

<!-- This is the full list of new features in the past three TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |Funzionalità |Versione Technical Preview |Versione Current Branch|  
 |----------------|---------------------|--------------------|
 | I punti di distribuzione pull supportano punti di distribuzione cloud come origine <!--1321554--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#pull-distribution-points-support-cloud-distribution-points-as-source)  | ![Non aggiunta](media/Red_X.gif) | 
 | Riduzione dell'uso della rete WAN tramite supporto parziale del download nella peer cache del client <!--1357346--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#partial-download-support-in-client-peer-cache-to-reduce-wan-utilization)  | ![Non aggiunta](media/Red_X.gif) | 
 | Finestre di manutenzione in Software Center <!--1358131--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#maintenance-windows-in-software-center)  | ![Non aggiunta](media/Red_X.gif) | 
 | Scheda personalizzata per pagine Web in Software Center <!--1358132--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#custom-tab-for-webpage-in-software-center)  | ![Non aggiunta](media/Red_X.gif) | 
 | Abilitare il supporto dell'aggiornamento software di terze parti nei client <!--1357605--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients)  | ![Non aggiunta](media/Red_X.gif) | 
 | Abilitare le operazioni di copia e incolla dei dettagli degli asset da visualizzazioni di monitoraggio <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-copypaste-of-asset-details-from-monitoring-views)  | ![Non aggiunta](media/Red_X.gif) | 
 | Estensioni SCAP <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#scap-extensions)  | ![Non aggiunta](media/Red_X.gif) | 
 | Transizione del carico di lavoro di Endpoint Protection a Intune usando la co-gestione <!-- 1357365 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#transition-endpoint-protection-workload-to-intune-using-co-management) | [Versione 1802](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune) |  
 | Configurare Ottimizzazione recapito di Windows per l'uso di gruppi di limiti di Configuration Manager <!-- 1324696 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups) | [Versione 1802](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization) |  
 | Sequenza di attività di aggiornamento sul posto di Windows 10 usando il gateway di gestione cloud <!-- 1357149 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway) | [Versione 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#deploy-windows-10-in-place-upgrade-via-cmg) |  
 | Miglioramenti della sequenza di attività di aggiornamento sul posto di Windows 10 <!-- 1357425 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-windows-10-in-place-upgrade-task-sequence) | [Versione 1802](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system) |  
 | Miglioramenti dei punti di distribuzione abilitati per PXE <!-- 1357580 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) | ![Non aggiunta](media/Red_X.gif) | 
 | Modelli di distribuzione per le sequenze di attività <!-- 1357391 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#deployment-templates-for-task-sequences) | [Versione 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS) |  
 | Dashboard del ciclo di vita del prodotto <!--1319632 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#product-lifecycle-dashboard) | ![Non aggiunta](media/Red_X.gif) | 
 | Miglioramenti del reporting <!--1357653 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-reporting) | [Versione 1802](/sccm/core/servers/manage/list-of-reports#operating-system) |  
 | Miglioramenti di Software Center <!--1357592 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-software-center) | [Versione 1802](/sccm/core/clients/deploy/about-client-settings#BKMK_HideInstalled) |  
 | Fallback del gruppo di limiti per i punti di gestione <!-- 1324594 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#boundary-group-fallback-for-management-points) | [Versione 1802](/sccm/core/servers/deploy/configure/boundary-groups#management-points) |  
 | Supporto migliorato per i certificati CNG <!-- 1357314 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improved-support-for-cng-certificates) | [Versione 1802](/sccm/core/plan-design/network/cng-certificates-overview) |  
 | Supporto del gateway di gestione cloud per Azure Resource Manager <!-- 1324735 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#cloud-management-gateway-support-for-azure-resource-manager) | [Versione 1802](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager) |  
 | Approvazione delle richieste di applicazioni degli utenti per dispositivo <!-- 1357015 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#approve-application-requests-for-users-per-device) | [Versione 1802](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings) |  
 | Usare Software Center per esplorare e installare le applicazioni disponibili per gli utenti in dispositivi aggiunti ad Azure AD <!-- 1322613 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices) | [Versione 1802](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices) |  
 | Report sulle informazioni sui dispositivi Windows AutoPilot <!-- 1351442 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#report-on-windows-autopilot-device-information) | [Versione 1802](/sccm/core/clients/manage/co-management-prepare#new-windows-10-devices) |  
 | Miglioramenti dei criteri di Configuration Manager per Windows Defender Exploit Guard <!-- 1356220 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard) | [Versione 1802](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |  
 | Criteri del browser Microsoft Edge <!-- 1357310 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#microsoft-edge-browser-policies) | [Versione 1802](/sccm/compliance/deploy-use/browser-profiles) | 
 | Report sul numero di browser predefiniti <!-- 1357830 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#report-for-default-browser-counts) | [Versione 1802](/sccm/core/servers/manage/list-of-reports#software---companies-and-products) | 
 | Supporto per dispositivi ARM64 Windows 10 <!-- 1353704 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#support-for-windows-10-arm64-devices) | [Versione 1802](/sccm/core/plan-design/configs/support-for-windows-10) |  
 | Creare distribuzioni in più fasi <!-- 1356837 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#create-phased-deployments) | [Versione 1802](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) |
 | Creazione di report di co-gestione <!-- 1356648 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#co-management-reporting) | [Versione 1802](\sccm\core\clients\manage\client-management-dashboard) |
 | Miglioramenti alla pianificazione di valutazione delle regole di distribuzione automatica <!-- 1357133 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-automatic-deployment-rule-evaluation-schedule) | [Versione 1802](/sccm/sum/deploy-use/automatically-deploy-software-updates#BKMK_CreateAutomaticDeploymentRule) |
 | Riassegnare un punto di distribuzione <!-- 1306937 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#reassign-distribution-point) | [Versione 1802](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_reassign) |
 | Miglioramenti all'inventario hardware <!-- 1357389 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-hardware-inventory) | [Versione 1802](/sccm/core/clients/manage/inventory/extend-hardware-inventory#BKMK_GreaterThan255) |
 | Miglioramenti alle impostazioni client per Software Center <!-- 1355146 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-client-settings-for-software-center) | [Versione 1802](/sccm/core/clients/deploy/about-client-settings#BKMK_HideUnapproved) |
 | Nuove impostazioni per Windows Defender Application Guard <!-- 1356256 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#new-settings-for-windows-defender-application-guard) | [Versione 1802](/sccm/protect/deploy-use/create-deploy-application-guard-policy#BKMK_HIS) |
 | Miglioramenti alla funzionalità Esegui script <!-- 1236459 --> | [Tech Preview 1801](capabilities-in-technical-preview-1801.md#improvements-to-run-scripts) | [Versione 1802](/sccm/apps/deploy-use/create-deploy-scripts) |
 
  

## <a name="capabilities-delivered-in-previous-technical-previews"></a>Funzionalità disponibili nelle Technical Preview precedenti
Di seguito sono elencate funzionalità specifiche disponibili nelle versioni precedenti della Technical Preview di Configuration Manager. Queste funzionalità rimangono disponibili nelle versioni successive, ma non sono ancora disponibili in una versione Current Branch corrente. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |Funzionalità |Versione Technical Preview |  
 |----------------|---------------------|
 | Servizio risponditore PXE basato su client <!-- 1357148 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
 |Disponibilità elevata per il ruolo del server del sito <!-- 1128774 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |
 |Supporto dell'avvio della rete PXE per IPv6 <!-- 1269793 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
 |Uso di Azure Active Directory <!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
 |Valutazione della conformità degli aggiornamenti di Windows Update for Business <!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
 |Accesso ai dati di endpoint OData <!-- 1321523 --> |[Technical Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
 |Miglioramenti di Asset Intelligence <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
 |Gli utenti finali possono installare le app dal portale aziendale <!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|



## <a name="see-also"></a>Vedere anche  
[What's new in System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions) (Novità di System Center Configuration Manager)  
 [Introduzione a System Center Configuration Manager](../../core/understand/introduction.md)

> [!Tip]  
> Per altre informazioni sulle funzionalità Current Branch che richiedono il consenso per l'abilitazione, vedere [Funzionalità di versioni non definitive](/sccm/core/servers/manage/pre-release-features).  
> Per altre informazioni sulle funzionalità Current Branch che è necessario abilitare in prima istanza, vedere [Abilitare le funzionalità facoltative degli aggiornamenti](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  


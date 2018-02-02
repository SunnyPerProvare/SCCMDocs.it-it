---
title: Versioni di Technical Preview
titleSuffix: Configuration Manager
description: "Informazioni sulla versione Technical Preview che consente di testare nuove funzionalità in System Center Configuration Manager."
ms.custom: na
ms.date: 01/19/2018
ms.prod: configuration-manager
ms.reviewer: nab
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
caps.latest.revision: 
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 975bd66bb86efb133ccd7017295e8108558f633d
ms.sourcegitcommit: db9978135d7a6455d83dbe4a5175af2bdeaeafd8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/22/2018
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Technical Preview)*

**Pagina iniziale di System Center Configuration Manager Technical Preview**. Questo articolo include informazioni dettagliate sulla versione di anteprima in evoluzione che comprende nuove funzionalità e caratteristiche in fase di sviluppo. Ogni versione Technical Preview presenta nuove funzionalità non incluse nella versione Current Branch di Configuration Manager nel momento in cui diventa disponibile la versione Technical Preview. Tali funzionalità potranno essere inserite in seguito nella versione Current Branch. Tuttavia, prima di essere finalizzate e inserite, viene offerta all'utente la possibilità di provarle e di inviare commenti.  

 Poiché questa versione è una Technical Preview, dettagli e funzionalità sono soggetti a modifiche.  

 Questo articolo contiene informazioni valide per tutte le versioni della Technical Preview. Le informazioni sulle nuove funzionalità sono elencate in base alla versione della Technical Preview in cui viene resa disponibile per la prima volta la funzionalità, ad esempio 1801 per gennaio 2018. I dettagli di queste funzionalità sono presentati in argomenti separati dedicati a ogni versione di anteprima.  

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
>  Quando si installa un aggiornamento per la Technical Preview, si aggiorna l'installazione di anteprima alla nuova versione Technical Preview.    Un'installazione Technical Preview non prevede mai la possibilità di eseguire l'aggiornamento a un'installazione del ramo corrente, né di ricevere gli aggiornamenti dalla versione ramo corrente.  

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

### <a name="technical-preview-version-1801"></a>Technical Preview versione 1801
- [Create phased deployments](capabilities-in-technical-preview-1801.md#create-phased-deployments) <!-- 1357405 --> (Creare distribuzioni in fasi) 
- [Co-management reporting](capabilities-in-technical-preview-1801.md#co-management-reporting) <!-- 1356648 --> (Creazione di report di co-gestione) 
- [Improvements to automatic deployment rule evaluation schedule](capabilities-in-technical-preview-1801.md#improvements-to-automatic-deployment-rule-evaluation-schedule) <!-- 1357133 --> (Miglioramenti alla pianificazione di valutazione delle regole di distribuzione automatica) 
- [Reassign distribution point](capabilities-in-technical-preview-1801.md#reassign-distribution-point) <!-- 1306937 --> (Riassegnare un punto di distribuzione) 
- [Improvements to hardware inventory](capabilities-in-technical-preview-1801.md#improvements-to-hardware-inventory) <!-- 1357389 --> (Miglioramenti all'inventario hardware) 
- [Improvements to client settings for Software Center](capabilities-in-technical-preview-1801.md#improvements-to-client-settings-for-software-center) <!-- 1355146 --> (Miglioramenti alle impostazioni client per Software Center) 
- [New settings for Windows Defender Application Guard](capabilities-in-technical-preview-1801.md#new-settings-for-windows-defender-application-guard) <!-- 1356256 --> (Nuove impostazioni per Windows Defender Application Guard) 
- [Improvements to Run Scripts](capabilities-in-technical-preview-1801.md#improvements-to-run-scripts) <!-- 1236459 --> (Miglioramenti alla funzionalità Esegui script) 




## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>Funzionalità disponibili nelle Technical Preview supportate recenti
Di seguito sono elencate le funzionalità disponibili nelle versioni della Technical Preview di Configuration Manager ancora supportate. 

<!-- This is the full list of new features in the past three TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |Funzionalità |Versione Technical Preview |Versione Current Branch|  
 |----------------|---------------------|--------------------|
 |Non vengono aggiornate automaticamente le applicazioni sostituite<!-- 1351266 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#do-not-automatically-upgrade-superseded-applications)  |![Non aggiunta](media/Red_X.gif)    | 
 |Vengono installate più applicazioni in Software Center <!-- 1357126 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#install-multiple-applications-in-software-center)  |![Non aggiunta](media/Red_X.gif)    |
 |Vengono apportate modifiche all'installazione del client di Configuration Manager <!-- 1356195 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#change-in-the-configuration-manager-client-install)  |![Non aggiunta](media/Red_X.gif)    | 
 |Vengono apportate modifiche al dashboard del dispositivo Surface <!-- 1355788 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#change-to-the-surface-device-dashboard)  |![Non aggiunta](media/Red_X.gif)    | 
 |Vengono apportati miglioramenti al dashboard di gestione client di Office 365 <!-- 1357281 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-office-365-client-management-dashboard)  |![Non aggiunta](media/Red_X.gif)    | 
 |Vengono apportati miglioramenti alla console di Configuration Manager <!-- 1357280,1357282 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-the-configuration-manager-console)  |![Non aggiunta](media/Red_X.gif)    | 
 |Vengono apportati miglioramenti al distribuzione del sistema operativo <!-- SMS 500897 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#improvements-to-operating-system-deployment)  |![Non aggiunta](media/Red_X.gif)    | 
 |Eseguire il passaggio della sequenza di attività <!-- 1261338 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) |[Versione 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence)    |
 |Consentire l'interazione utente durante l'installazione di un'applicazione <!-- 1356976 --> | [Tech Preview 1711](capabilities-in-technical-preview-1711.md) |![Non aggiunta](media/Red_X.gif)    |
 |Telemetria di Windows 10 per l'integrità del dispositivo di Windows Analytics<!--1356148 --> | [Technical Preview 1710](capabilities-in-technical-preview-1710.md#limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health) |[Versione 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710#reporting)    |
 |Miglioramenti alle icone di Software Center <!-- 1356194 --> | [Technical Preview 1710](capabilities-in-technical-preview-1710.md#software-center-no-longer-distorts-icons-larger-than-250x250) |[Versione 1710](/sccm/apps/plan-design/plan-for-and-configure-application-management#supplemental-procedures-to-install-and-configure-the-application-catalog-and-software-center)    |
 |Controllare la conformità da Software Center per i dispositivi cogestiti<!-- 1356374 -->|[Technical Preview 1710](capabilities-in-technical-preview-1710.md#check-compliance-from-software-center-for-co-managed-devices)|[Versione 1710](/sccm/core/clients/manage/co-management-overview)    |
 |Supporto limitato per i certificati CNG<!-- 1356191 -->| [Technical Preview 1710](capabilities-in-technical-preview-1710.md#limited-support-for-cng-certificates)|[Versione 1710](/sccm/core/plan-design/network/cng-certificates-overview)    |
 |Supporto per Exploit Guard <!--1355468 --> | [Technical Preview 1710](capabilities-in-technical-preview-1710.md#support-for-exploit-guard) |[Versione 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)    |
 |Vengono migliorate le descrizioni per il riavvio in sospeso del computer   <!-- 1356283  -->| [Technical Preview 1710](capabilities-in-technical-preview-1710.md)|[Versione 1710](/sccm/core/clients/manage/manage-clients)    |
 |Modifiche ai criteri di Device Guard <!-- 1355092  -->| [Technical Preview 1710](capabilities-in-technical-preview-1710.md)|[Versione 1710](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)    |
 |Configurare e distribuire criteri di Windows Defender Application Guard <!-- 1351960  -->| [Technical Preview 1710](capabilities-in-technical-preview-1710.md)|[Versione 1710](/sccm/protect/deploy-use/create-deploy-application-guard-policy)    |
 |Miglioramenti per la distribuzione di script di PowerShell da Configuration Manager <!-- 1236459 -->| [Technical Preview 1710](capabilities-in-technical-preview-1710.md#improvements-for-deploying-powershell-scripts-from-configuration-manager) | [Versione 1710](/sccm/apps/deploy-use/create-deploy-scripts)
 

## <a name="capabilities-delivered-in-previous-technical-previews"></a>Funzionalità disponibili nelle Technical Preview precedenti
Di seguito sono elencate funzionalità specifiche disponibili nelle versioni precedenti della Technical Preview di Configuration Manager. Queste funzionalità rimangono disponibili nelle versioni successive, ma non sono ancora disponibili in una versione Current Branch corrente. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |Funzionalità |Versione Technical Preview |  
 |----------------|---------------------|
 |Esperienza del profilo VPN migliorata nella console di Configuration Manager <!-- 1313282 --> | [Tech Preview 1709](capabilities-in-technical-preview-1709.md) |
 |Informazioni dettagliate sulla gestione <!-- 1353967 --> |[Tech Preview 1708](capabilities-in-technical-preview-1708.md#management-insights)|
 |Dashboard del dispositivo Surface <!-- 1355788 --> |[Tech Preview 1707](capabilities-in-technical-preview-1707.md#surface-device-dashboard)|
 |Disponibilità elevata per il ruolo del server del sito <!-- 1128774 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |
 |Supporto dell'avvio della rete PXE per IPv6 <!-- 1269793 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
 |Valutazione dell'attestazione dell'integrità dei dispositivi per i criteri di conformità per l'accesso condizionale <!-- 1235616 -->|[Tech Preview 1706](capabilities-in-technical-preview-1706.md#device-health-attestation-assessment-for-compliance-policies-for-conditional-access)|
 |Uso di Azure Active Directory <!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
 |Valutazione della conformità degli aggiornamenti di Windows Update for Business <!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
 |Accesso ai dati di endpoint OData <!-- 1321523 --> |[Technical Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
 |Miglioramenti di Asset Intelligence <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
 |Gli utenti finali possono installare le app dal portale aziendale <!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|



## <a name="see-also"></a>Vedere anche  
[What's new in System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions) (Novità di System Center Configuration Manager)  
 [Introduction to System Center Configuration Manager](../../core/understand/introduction.md) (Introduzione a System Center Configuration Manager)

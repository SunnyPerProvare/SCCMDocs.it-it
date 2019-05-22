---
title: Versioni di Technical Preview
titleSuffix: Configuration Manager
description: Informazioni sulla versione Technical Preview che consente di testare nuove funzionalità e capacità in Configuration Manager.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c6797b25138bdd09dd4a879ef461d5420c38ab47
ms.sourcegitcommit: 8eccf5429aabcef17d5762e4b03912ccad1215e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/30/2019
ms.locfileid: "64928861"
---
# <a name="technical-preview-for-configuration-manager"></a>Technical Preview per Configuration Manager

*Si applica a: System Center Configuration Manager (Technical Preview)*

Questo articolo include informazioni dettagliate sul ramo Technical Preview mensile di Configuration Manager. La versione Technical Preview introduce nuove funzionalità su cui Microsoft sta lavorando. Vengono introdotte nuove funzionalità non ancora incluse in Current Branch di Configuration Manager. Queste funzionalità potrebbero essere alla fine incluse in un aggiornamento a Current Branch. Prima di finalizzare le funzionalità, Microsoft invita gli utenti a provarle e a inviare commenti e suggerimenti.  

Poiché questa versione è una Technical Preview, dettagli e funzionalità sono soggetti a modifiche.  

Queste informazioni si applicano a tutte le versioni del ramo Technical Preview di Configuration Manager. Questo articolo elenca ogni nuova funzionalità insieme alla versione Technical Preview in cui compare per la prima volta. Ad esempio, la versione **1901** per gennaio (01) del 2019 (19). Le singole funzionalità sono descritte in dettaglio in articoli separati dedicati a ogni versione di anteprima.  

Per informazioni sulle novità della versione *Current Branch* di Configuration Manager, vedere [Novità delle versioni incrementali di Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions).

> [!Tip]  
> Per ricevere una notifica quando questa pagina viene aggiornata, copiare e incollare l'URL seguente nel lettore di feed RSS: `https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`

## <a name="bkmk_reqs"></a> Requisiti e limitazioni  

> [!IMPORTANT]  
> La Technical Preview viene concessa in licenza per essere usata esclusivamente in un ambiente lab. Microsoft potrebbe non offrire supporto tecnico e alcune funzionalità potrebbero non essere disponibili nel software di anteprima. Inoltre, il software di anteprima può essere caratterizzato da standard di sicurezza, privacy, accessibilità, disponibilità e affidabilità ridotti o diversi rispetto al software commercializzato.  

Per la maggior parte dei prerequisiti del prodotto, usare le informazioni in [Configurazioni supportate](/sccm/core/plan-design/configs/supported-configurations). Per il ramo Technical Preview si applicano le eccezioni seguenti:  

- Ogni installazione rimane attiva per 90 giorni prima di diventare inattiva.  

- L'inglese è l'unica lingua supportata.  

- Supporta solo i parametri della riga di comando di installazione seguenti:  

    - `/silent`  
    - `/testdbupgrade`  

- Il punto di connessione del servizio viene installato in modalità online. e non supporta la modalità offline.  

- Gli articoli separati per ogni versione specifica della Technical Preview includono ulteriori limitazioni o requisiti, secondo il caso.

- Le funzionalità seguenti non sono supportate con il ramo Technical Preview:  

    - [Migrazione](/sccm/core/migration/migrate-data-between-hierarchies) da o verso questo ramo di anteprima.  

    - [Aggiornamento](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) a questo ramo di anteprima.  

    - [Ripristino di siti](/sccm/core/servers/manage/recover-sites) dalla cartella cd.latest.  <!--507106-->

- Non è previsto alcun supporto per l'aggiornamento a Current Branch da questo ramo di anteprima.  

    > [!Note]  
    > Se sono disponibili aggiornamenti per una versione di anteprima, è ancora possibile trovarli e installarli dal nodo **Aggiornamenti e manutenzione** della console di Configuration Manager. Per un video relativo al processo di aggiornamento nella console, vedere [Installing Configuration Manager update packages](https://www.youtube.com/embed/KBd_EGFbUT8) (Installazione dei pacchetti di aggiornamento di Configuration Manager) su youtube.com.  

- Supporta solo un sito primario autonomo. Non è disponibile alcun supporto per un sito di amministrazione centrale, più siti primari o i siti secondari.  

I prodotti e tecnologie seguenti sono supportati dal ramo Technical Preview di Configuration Manager:

- Sono supportate solo le versioni seguenti di **SQL Server**:  

    - SQL Server 2017 (con aggiornamento cumulativo 2 o versione successiva)
    - SQL Server 2016 (senza Service Pack o versioni successive)
    - SQL Server 2014 (con Service Pack 1 o versioni successive)
    - SQL Server 2012 (con Service Pack 3 o versioni successive)  

- Il sito supporta fino a 10 client, che devono eseguire una delle seguenti versioni di Windows:  

    - Windows 10  
    - Windows 8.1  
    - Windows 7  

> [!Note]  
> L'inclusione di questi prodotti in questo contenuto non implica un'estensione del supporto per una versione oltre il ciclo di vita del supporto. Configuration Manager non supporta prodotti che non rientrano nel ciclo di vita del supporto. Per altre informazioni, vedere [Criteri relativi al ciclo di vita Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=208270).  

## <a name="bkmk_install"></a> Installare e aggiornare  

Il ramo Technical Preview di Configuration Manager per l'uso in ambienti lab è diverso da Current Branch di Configuration Manager per l'uso in ambienti di produzione.  

Prima di tutto installare una versione di base del ramo Technical Preview. Dopo l'installazione di una versione di base, è possibile usare gli aggiornamenti nella console per aggiornare l'installazione con la versione di anteprima più recente. In genere, le nuove versioni Technical Preview sono disponibili ogni mese.

Microsoft supporta ogni versione Technical Preview fino a quando diventano disponibili tre versioni successive. Ad esempio, quando è stata rilasciata la versione 1708, la versione 1704 non era più inclusa nel supporto. Le versioni 1705, 1706 e 1707 sono rimaste incluse nel supporto. Quando una versione di base non è più inclusa nel supporto, è ancora supportata per l'installazione di un nuovo sito Technical Preview, presupponendo che venga eseguito l'aggiornamento immediato a una versione supportata. La versione di base precedente è supportata fino a quando non diventa disponibile una nuova versione di base. Eseguire l'aggiornamento alla versione più recente disponibile dalla versione di base e quindi ripetere il processo di aggiornamento fino a installare l'ultima versione Technical Preview.

> [!TIP]  
> Quando si installa un aggiornamento della Technical Preview, si aggiorna l'installazione di anteprima alla nuova versione Technical Preview. Un'installazione Technical Preview non prevede mai la possibilità di eseguire l'aggiornamento a un'installazione Current Branch, né di ricevere gli aggiornamenti dalla versione Current Branch corrente.
>
> Più volte nel corso dell'anno diventano disponibili versioni del ramo Technical Preview e Current Branch con lo stesso numero di versione. Ad esempio, è presente una versione Technical Preview 1802 e una versione Current Branch 1802.

### <a name="active-baseline-versions"></a>Versioni di base attive

È possibile installare una versione di base al massimo per un anno dopo il rilascio. Quando si installa un nuovo sito Technical Preview, se sono disponibili più versioni di base, usare la versione di base più recente.

- **Technical preview versione 1902.2**: Configuration Manager Technical Preview versione 1902.2 è disponibile sia come aggiornamento nella console che come nuova versione di base. Scaricare le versioni di base dal [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

## <a name="BKMK_TPFeedback"></a> Invio di commenti e suggerimenti  

Microsoft sarebbe lieta di ricevere commenti e suggerimenti sulle nuove funzionalità della Technical Preview. Per altre informazioni, vedere la sezione su [commenti e suggerimenti per i prodotti](/sccm/core/understand/find-help#product-feedback).

Siamo anche interessati a conoscere le vostre idee su eventuali nuove funzionalità. Per inviare nuove idee e votare le idee presentate da altri, [visitare la pagina UserVoice](https://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->

## <a name="bkmk_tpCaps"></a> Funzionalità nella versione più recente  

Le funzionalità seguenti sono disponibili con la versione Technical Preview di Configuration Manager più recente:

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1904"></a>Technical Preview versione 1904

<!-- - [title](/sccm/core/get-started/2019/technical-preview-1901#bkmk_anchor) <!--ID-->

- [Dashboard Preparazione aggiornamenti per Office 365 ProPlus](/sccm/core/get-started/2019/technical-preview-1904#bkmk_o365) <!--4021125-->  

- [Configurare l'aggiornamento dinamico durante gli aggiornamenti delle funzionalità](/sccm/core/get-started/2019/technical-preview-1904#configure-dynamic-update-during-feature-updates) <!--4062619-->  

- [Hub della community e GitHub](/sccm/core/get-started/2019/technical-preview-1904#community-hub-and-github) <!--3555935,3555936-->  

- [Modalità autonoma per CMPivot](/sccm/core/get-started/2019/technical-preview-1904#bkmk_cmpivot) <!--3555890-->  

- [Miglioramenti all'infrastruttura di Software Center](/sccm/core/get-started/2019/technical-preview-1904#bkmk_swctr) <!--3555950-->  

- [Controllo migliorato sulla manutenzione di WSUS](/sccm/core/get-started/2019/technical-preview-1904#improved-control-over-wsus-maintenance) <!--4110109-->  

- [Pre-cache per pacchetti di driver e immagini del sistema operativo](/sccm/core/get-started/2019/technical-preview-1904#bkmk_precache) <!--4224642-->  

- [Miglioramenti alla distribuzione del sistema operativo](/sccm/core/get-started/2019/technical-preview-1904#bkmk_osd) <!--2839943,4447680-->  

> [!Note]  
> Le funzionalità disponibili in una versione precedente della Technical Preview rimangono disponibili nelle versioni successive. Analogamente, le funzionalità aggiunte alla versione Current Branch di Configuration Manager rimangono disponibili nel ramo Technical Preview.  

## <a name="features-in-recent-supported-technical-previews"></a>Funzionalità nelle versioni Technical Preview supportate recenti

Le funzionalità disponibili sono state rilasciate con le versioni precedenti della Technical Preview di Configuration Manager ma sono ancora supportate:

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 | Funzionalità | Versione Technical Preview | Versione Current Branch |  
 |---------|---------------------------|------------------------|
 | Stima dei costi dei servizi cloud <!--3555774--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_cmg) | ![Non aggiunta](media/Red_X.gif) |
 | Usare il punto di distribuzione come server di cache locale per Ottimizzazione recapito <!--3555764--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_doinc) | ![Non aggiunta](media/Red_X.gif) |
 | Richiamare il blocco per la modifica delle sequenze di attività <!--3699337--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_sedo) | ![Non aggiunta](media/Red_X.gif) |
 | Drill-through degli aggiornamenti obbligatori <!--4224414--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_req-updates) | ![Non aggiunta](media/Red_X.gif) |
 | Miglioramento alla creazione del supporto per la sequenza di attività <!--4090666--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_tsmedia) | ![Non aggiunta](media/Red_X.gif) |
 | Lingue aggiuntive per gli aggiornamenti di Office 365 <!--3555955--> | [Tech Preview 1902.2](/sccm/core/get-started/2019/technical-preview-1902-2#bkmk_o365lang) | Versione 1902 |
 | Integrazione con l'analisi per l'idoneità per Office 365 ProPlus <!--3735402--> | [Tech Preview 1902.2](/sccm/core/get-started/2019/technical-preview-1902-2#bkmk_o365) | Versione 1902 |
 | Miglioramento dei criteri di superamento della distribuzione in più fasi <!--3555946--> | [Tech Preview 1902.2](/sccm/core/get-started/2019/technical-preview-1902-2#bkmk_pod) | Versione 1902 |
 | Miglioramento del protocollo HTTP avanzato <!--3798957--> | [Tech Preview 1902.2](/sccm/core/get-started/2019/technical-preview-1902-2#bkmk_ehttp) | Versione 1902 |
 | Sostituire le notifiche di tipo avviso popup con una finestra di dialogo <!--3555947--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_impact) | Versione 1902 |
 | Stato di avanzamento durante la sequenza di attività di aggiornamento sul posto <!--3747129--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_ipu) | Versione 1902 |
 | Reindirizzare le cartelle note di Windows in OneDrive <!--3556021--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_odfb) | Versione 1902 |
 | Visualizzare solo il primo schermo durante il controllo remoto <!--3231732--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_rcmulti) | Versione 1902 |
 | Modificare o copiare gli script di PowerShell <!--3705507--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_psedit) | Versione 1902 |
 | Aggiungere Cloud Management Gateway ai gruppi di limiti <!--3640932--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_cmgbg) | Versione 1902 |
 | Configurare le visualizzazioni predefinite in Software Center <!--3612112--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_swctr) | Versione 1902 |
 | Miglioramenti del dashboard sull'integrità del client <!--3599209--> | [Tech Preview 1902](/sccm/core/get-started/2019/technical-preview-1902#bkmk_health) | Versione 1902 |
 | Dashboard sull'integrità del client <!--3599209--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_health) | Versione 1902 |
 | Specificare la priorità per gli aggiornamenti delle funzionalità nella manutenzione di Windows 10 <!--3734525--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_neo) | Versione 1902 |
 | Monitoraggio dedicato per le distribuzioni in più fasi <!--3555949--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_pod) | Versione 1902 |
 | Eseguire CMPivot dal sito di amministrazione centrale <!--3610960--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_cmpivot) | Versione 1902 |
 | Miglioramenti del passaggio della sequenza di attività Esegui script PowerShell <!--3556028--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_posh) | Versione 1902 |
 | Prodotti Office nel dashboard del ciclo di vita <!--3556026--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_lifecycle) | Versione 1902 |
 | Regole di informazioni dettagliate sulla gestione per le raccolte <!--3555752--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_micoll) | Versione 1902 |
 | Eseguire la ricerca nelle visualizzazioni dispositivi tramite indirizzi MAC <!--3600878--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_mac) | Versione 1902 |
 | Modalità manutenzione per il punto di distribuzione <!--3555754--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_dpmaint) | Versione 1902 |
 | Servizio immagini ottimizzato <!--3555951--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_resetbase) | Versione 1902 |
 | Importare un singolo indice di un'immagine del sistema operativo <!--3719699--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_index) | Versione 1902 |
 | Usare Azure Resource Manager per i servizi cloud <!--3605704--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_arm) | Versione 1902 |
 | Conferma del feedback della console <!--3556010--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_feedback) | Versione 1902 |
 | Creare un lab di Configuration Manager Technical Preview in Azure <!--3556017--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_azurevm) | Non applicabile |
 | Specificare una porta personalizzata per la riattivazione peer <!--3605925--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_sleep) | Versione 1902 |
 | Visualizzare le console connesse di recente <!--3699367--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_console) | Versione 1902 |
 | Arrestare il servizio cloud al superamento di una soglia <!--3735092--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_cmg) | Versione 1902 |
 | Timeout della modalità di provisioning dei client <!--3197824--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_osdprov) | Versione 1902 |
 | Miglioramenti della distribuzione del sistema operativo <!--3633146,3641475,3654172,3734270--> | [Tech Preview 1901](/sccm/core/get-started/2019/technical-preview-1901#bkmk_osd) | Versione 1902 |


## <a name="features-in-previous-technical-previews"></a>Funzionalità nelle versioni Technical Preview precedenti

Le funzionalità seguenti sono state rilasciate con le versioni precedenti del ramo Technical Preview di Configuration Manager. Queste funzionalità rimangono disponibili nelle versioni successive, ma non sono ancora disponibili in Current Branch.

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

| Funzionalità        | Versione Technical Preview |  
|----------------|---------------------------|
| Scaricare report dall'hub della community<!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) |
| Hub della community <!--3556020, fka 1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) |
| Servizio risponditore PXE basato su client <!--3556018, fka 1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| Supporto dell'avvio della rete PXE per IPv6 <!--3601254, fka 1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Uso di Azure Active Directory <!--3607315, fka 1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Miglioramenti ad Asset Intelligence <!--3601024, fka 1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |
| Gli utenti finali possono installare le app dal portale aziendale <!--3601249, fka 1037233--> | [Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End) |

## <a name="see-also"></a>Vedere anche  

Per altre informazioni, vedere gli articoli seguenti:  

- [Valutare Configuration Manager in un lab](/sccm/core/get-started/evaluate-with-lab-environment)
- [Novità delle versioni incrementali di System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Introduzione a Configuration Manager](/sccm/core/understand/introduction)

> [!Tip]  
> Per altre informazioni sulle funzionalità Current Branch che richiedono il consenso per l'abilitazione, vedere [Funzionalità di versioni non definitive](/sccm/core/servers/manage/pre-release-features).  
>
> Per altre informazioni sulle funzionalità Current Branch che è necessario abilitare in prima istanza, vedere [Abilitare le funzionalità facoltative degli aggiornamenti](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  

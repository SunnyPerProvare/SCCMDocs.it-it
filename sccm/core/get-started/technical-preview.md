---
title: Versioni di Technical Preview
titleSuffix: Configuration Manager
description: Informazioni sulla versione Technical Preview che consente di testare nuove funzionalità e capacità in Configuration Manager.
ms.date: 01/17/2020
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7b1ae37ea51b49dd74c625976bc08f9dce2f43a2
ms.sourcegitcommit: d1c6f3f2fa6821f15041e73d411cc4e1de0850ba
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519937"
---
# <a name="technical-preview-for-configuration-manager"></a>Technical Preview per Configuration Manager

*Si applica a: Configuration Manager (Technical Preview Branch)*

Questo articolo include informazioni dettagliate sul ramo Technical Preview mensile di Configuration Manager. La versione Technical Preview introduce nuove funzionalità su cui Microsoft sta lavorando. Vengono introdotte nuove funzionalità non ancora incluse in Current Branch di Configuration Manager. Queste funzionalità potrebbero essere alla fine incluse in un aggiornamento a Current Branch. Prima di finalizzare le funzionalità, Microsoft invita gli utenti a provarle e a inviare commenti e suggerimenti.

Poiché questa versione è una Technical Preview, dettagli e funzionalità sono soggetti a modifiche.

Queste informazioni si applicano a tutte le versioni del ramo Technical Preview di Configuration Manager. Questo articolo elenca ogni nuova funzionalità insieme alla versione Technical Preview in cui compare per la prima volta. Ad esempio, la versione **2001** per gennaio (`01`) del 2020 (`20`). Le singole funzionalità sono descritte in dettaglio in articoli separati dedicati a ogni versione di anteprima.

Per informazioni sulle novità della versione *Current Branch* di Configuration Manager, vedere [Novità delle versioni incrementali di Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions).

> [!Tip]
> Per ricevere una notifica quando questa pagina viene aggiornata, copiare e incollare l'URL seguente nel lettore di feed RSS: `https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`

## <a name="bkmk_reqs"></a> Requisiti e limitazioni

> [!IMPORTANT]
> La Technical Preview viene concessa in licenza per essere usata esclusivamente in un ambiente lab. Microsoft potrebbe non offrire supporto tecnico e alcune funzionalità potrebbero non essere disponibili nelle anteprime tecniche. Inoltre, il software in anteprima tecnica può essere caratterizzato da standard di sicurezza, privacy, accessibilità, disponibilità e affidabilità ridotti o diversi rispetto al software commercializzato.

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

  - [Ripristino di siti](/sccm/core/servers/manage/recover-sites) dalla cartella cd.latest.<!--507106-->

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

- Il sito supporta fino a 10 client, che possono eseguire qualsiasi [versione supportata del sistema operativo client](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices).<!-- SCCMDocs#1656 -->

> [!Note]
> L'inclusione di questi prodotti in questo contenuto non implica un'estensione del supporto per una versione oltre il ciclo di vita del supporto. Configuration Manager non supporta prodotti che non rientrano nel ciclo di vita del supporto. Per altre informazioni, vedere [Criteri relativi al ciclo di vita Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=208270).

## <a name="bkmk_install"></a> Installare e aggiornare

Il ramo Technical Preview di Configuration Manager per l'uso in ambienti lab è diverso da Current Branch di Configuration Manager per l'uso in ambienti di produzione.

Prima di tutto installare una versione di base del ramo Technical Preview. Dopo l'installazione di una versione di base, eseguire gli aggiornamenti nella console per aggiornare l'installazione con la versione di anteprima più recente. In genere, le nuove versioni Technical Preview sono disponibili ogni mese.

Microsoft supporta ogni versione Technical Preview fino a quando diventano disponibili tre versioni successive. Ad esempio, quando è stata rilasciata la versione 1908, la versione 1904 è stata esclusa dal supporto. Le versioni 1905, 1906 e 1907 sono invece rimaste. Quando una versione di base non è più inclusa nel supporto, è ancora supportata per l'installazione di un nuovo sito Technical Preview, presupponendo che venga eseguito l'aggiornamento immediato a una versione supportata. La versione di base precedente è supportata fino a quando non diventa disponibile una nuova versione di base. Eseguire l'aggiornamento alla versione più recente disponibile dalla versione di base e quindi ripetere il processo di aggiornamento fino a installare l'ultima versione Technical Preview.

> [!TIP]
> Quando si installa un aggiornamento della Technical Preview, si aggiorna l'installazione di anteprima alla nuova versione Technical Preview. Un'installazione Technical Preview non prevede mai la possibilità di eseguire l'aggiornamento a un'installazione Current Branch, né di ricevere gli aggiornamenti dalla versione Current Branch corrente.
>
> Più volte nel corso dell'anno diventano disponibili versioni del ramo Technical Preview e Current Branch con lo stesso numero di versione. Ad esempio, una versione Technical Preview 1910 e una versione Current Branch 1910.

### <a name="active-baseline-versions"></a>Versioni di base attive

È possibile installare una versione di base al massimo per un anno dopo il rilascio. Quando si installa un nuovo sito Technical Preview usare la versione di base più recente.

- **Technical Preview versione 1911**: Configuration Manager Technical Preview Branch versione 1911 è disponibile sia come aggiornamento nella console che come nuova versione di base.

Scaricare una versione di base da [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

## <a name="BKMK_TPFeedback"></a> Invio di commenti e suggerimenti

Microsoft sarebbe lieta di ricevere commenti e suggerimenti sulle nuove funzionalità della Technical Preview. Per altre informazioni, vedere la sezione su [commenti e suggerimenti per i prodotti](/sccm/core/understand/find-help#product-feedback).

Microsoft è interessata a conoscere le idee degli utenti su nuove funzionalità che potrebbero essere implementate. È possibile inviare nuove idee e votare le idee di altri utenti: [UserVoice per Configuration Manager](https://configurationmanager.uservoice.com).

<!--
## <a name="bdmk_tpknownissues"></a> General changes introduced in technical preview branch

<!-- (explanatory comment)
Enable this section if needed to include any broad change to the tech preview branch
-->

## <a name="bkmk_tpCaps"></a> Funzionalità nella versione più recente

<!-- (explanatory comment)
This is the full list of new features in the latest TP release
-->

Le funzionalità seguenti sono disponibili con la versione Technical Preview di Configuration Manager più recente:

### <a name="technical-preview-version-2001"></a>Technical Preview versione 2001

<!-- - [title](/sccm/core/get-started/2020/technical-preview-2001#bkmk_anchor) <!--ID-->

- [Dashboard Gestione di Microsoft Edge](/sccm/core/get-started/2020/technical-preview-2001#bkmk_edge-dash) <!--3871913-->
- [Miglioramenti ai gruppi di orchestrazione](/sccm/core/get-started/2020/technical-preview-2001#bkmk_orch) <!--3098816-->
- [Miglioramenti al passaggio della sequenza di attività Verifica conformità](/sccm/core/get-started/2020/technical-preview-2001#bkmk_tsready) <!--6005561-->
- [Integrare il server di report di Power BI](/sccm/core/get-started/2020/technical-preview-2001#bkmk_powerbi) <!--3721603-->
- [Gruppi di log di OneTrace](/sccm/core/get-started/2020/technical-preview-2001#bkmk_onetrace) <!--5559993-->
- [Miglioramenti al servizio di amministrazione](/sccm/core/get-started/2020/technical-preview-2001#bkmk_rest) <!--5728365-->
- [Attivare un dispositivo dal sito di amministrazione centrale](/sccm/core/get-started/2020/technical-preview-2001#bkmk_wake) <!--6030715-->
- [Miglioramenti per lo stato delle sequenze di attività](/sccm/core/get-started/2020/technical-preview-2001#bkmk_tsprogress) <!--2356386-->

> [!NOTE]  
> Le funzionalità disponibili in una versione precedente della Technical Preview rimangono disponibili nelle versioni successive. Analogamente, le funzionalità aggiunte alla versione Current Branch di Configuration Manager rimangono disponibili nel ramo Technical Preview.  

## <a name="features-in-recent-technical-previews"></a>Funzionalità nelle anteprime tecniche recenti

<!-- (explanatory comment)
This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->

Le funzionalità seguenti sono state rilasciate in versioni precedenti del ramo Configuration Manager Technical Preview dopo la versione Current Branch 1910:

### <a name="technical-preview-version-1912"></a>Technical Preview versione 1912

- [Avviare una sequenza di attività immediatamente dopo la registrazione del client](/sccm/core/get-started/2019/technical-preview-1912#bkmk_provisionts) <!--5526972-->
- [Espansione dell'onboarding di Microsoft Defender Advanced Threat Protection (ATP)](/sccm/core/get-started/2019/technical-preview-1912#bkmk_atp) <!--5229962-->
- [Nuove regole delle informazioni dettagliate sulla gestione dai servizi Microsoft](/sccm/core/get-started/2019/technical-preview-1912#bkmk_rules) <!--3607758-->
- [Raccolta dei log del client](/sccm/core/get-started/2019/technical-preview-1912#client-log-collection) <!--4226618-->
- [Miglioramenti di CMPivot](/sccm/core/get-started/2019/technical-preview-1912#improvements-to-cmpivot) <!--5870934-->
- [Miglioramenti alla distribuzione del sistema operativo](/sccm/core/get-started/2019/technical-preview-1912#bkmk_osd) <!--5842295,5573175,5690481-->

> [!TIP]
> Quando è disponibile una nuova versione Current Branch, le funzionalità presenti in tale versione sono elencate nella versione più recente dell'articolo *Novità*. Per altre informazioni, vedere [Novità delle versioni incrementali](/sccm/core/plan-design/changes/whats-new-incremental-versions#supported-versions).

## <a name="features-in-previous-technical-previews"></a>Funzionalità nelle versioni Technical Preview precedenti

<!-- (explanatory comment)
This is the list of individual features that are still in TP (not in CB). 
Copy from the lists above any individual features that are still in TP and add to the top of this list
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

Le funzionalità seguenti sono state rilasciate con le versioni precedenti del ramo Technical Preview di Configuration Manager. Queste funzionalità rimangono disponibili nelle versioni successive, ma non sono ancora disponibili in Current Branch.

| Funzionalità        | Versione Technical Preview |
|----------------|---------------------------|
| Allegare file al feedback <!--3556011--> | [Tech Preview 1910](/sccm/core/get-started/2019/technical-preview-1910#attach-files-to-feedback) |
| Gruppi di orchestrazione <!--3098816--> | [Tech Preview 1909](/sccm/core/get-started/2019/technical-preview-1909#bkmk_OGs) |
| Miglioramenti ai punti di distribuzione abilitati per il multicast <!--3785535--> | [Tech Preview 1908.2](/sccm/core/get-started/2019/technical-preview-1908-2#bkmk_multicast) |
| Modelli di distribuzione in più fasi <!--4961086--> | [Tech Preview 1908](/sccm/core/get-started/2019/technical-preview-1908#phased-deployment-templates) |
| Controllo remoto tramite il gateway di gestione cloud <!--4575930--> | [Tech Preview 1906](/sccm/core/get-started/2019/technical-preview-1906#remote-control-anywhere-using-cloud-management-gateway) |
| Miglioramento dell'hub della community <!--3555935--> | [Tech Preview 1906](/sccm/core/get-started/2019/technical-preview-1906#bkmk_hub) |
| Sequenza di attività come tipo di distribuzione del modello di app <!--3555953--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_tsdt) |
| Miglioramento dell'hub della community <!--4224401--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_hub) |
| Hub della community e GitHub <!--3555935--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#community-hub-and-github) |
| Stima dei costi dei servizi cloud <!--3555774--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_cmg) |
| Scaricare report dall'hub della community <!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) |
| Hub della community <!--3556020, fka 1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) |
| Servizio risponditore PXE basato su client <!--3556018, fka 1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| Supporto dell'avvio della rete PXE per IPv6 <!--3601254, fka 1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Uso di Azure Active Directory <!--3607315, fka 1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Miglioramenti ad Asset Intelligence <!--3601024, fka 1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |

## <a name="see-also"></a>Vedere anche

Per altre informazioni, vedere gli articoli seguenti:

- [Valutare Configuration Manager in un lab](/sccm/core/get-started/evaluate-with-lab-environment)
- [Novità delle versioni incrementali di System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)
- [Introduzione a Configuration Manager](/sccm/core/understand/introduction)

> [!Tip]
> Per altre informazioni sulle funzionalità Current Branch che richiedono il consenso per l'abilitazione, vedere [Funzionalità di versioni non definitive](/sccm/core/servers/manage/pre-release-features).
>
> Per altre informazioni sulle funzionalità Current Branch che è necessario abilitare in prima istanza, vedere [Abilitare le funzionalità facoltative degli aggiornamenti](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).

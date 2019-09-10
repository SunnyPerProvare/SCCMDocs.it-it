---
title: Versioni di Technical Preview
titleSuffix: Configuration Manager
description: Informazioni sulla versione Technical Preview che consente di testare nuove funzionalità e capacità in Configuration Manager.
ms.date: 08/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d5c80836ced76bdf1109c9279bf2068efbbd97f5
ms.sourcegitcommit: f679fc1e46c191a1780ae961d155c927fc353dce
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176762"
---
# <a name="technical-preview-for-configuration-manager"></a>Technical Preview per Configuration Manager

*Si applica a: System Center Configuration Manager (Technical Preview)*

Questo articolo include informazioni dettagliate sul ramo Technical Preview mensile di Configuration Manager. La versione Technical Preview introduce nuove funzionalità su cui Microsoft sta lavorando. Vengono introdotte nuove funzionalità non ancora incluse in Current Branch di Configuration Manager. Queste funzionalità potrebbero essere alla fine incluse in un aggiornamento a Current Branch. Prima di finalizzare le funzionalità, Microsoft invita gli utenti a provarle e a inviare commenti e suggerimenti.  

Poiché questa versione è una Technical Preview, dettagli e funzionalità sono soggetti a modifiche.  

Queste informazioni si applicano a tutte le versioni del ramo Technical Preview di Configuration Manager. Questo articolo elenca ogni nuova funzionalità insieme alla versione Technical Preview in cui compare per la prima volta. Ad esempio, la versione **1908** per agosto (08) del 2019 (19). Le singole funzionalità sono descritte in dettaglio in articoli separati dedicati a ogni versione di anteprima.  

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

- **Technical Preview versione 1907**: Configuration Manager Technical Preview versione 1907 è disponibile sia come aggiornamento nella console che come nuova versione di base. Scaricare le versioni di base dal [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).


## <a name="BKMK_TPFeedback"></a> Invio di commenti e suggerimenti  

Microsoft sarebbe lieta di ricevere commenti e suggerimenti sulle nuove funzionalità della Technical Preview. Per altre informazioni, vedere la sezione su [commenti e suggerimenti per i prodotti](/sccm/core/understand/find-help#product-feedback).

Siamo anche interessati a conoscere le vostre idee su eventuali nuove funzionalità. Per inviare nuove idee e votare le idee presentate da altri, [visitare la pagina UserVoice](https://configurationmanager.uservoice.com).  


<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->


## <a name="bkmk_tpCaps"></a> Funzionalità nella versione più recente  

Le funzionalità seguenti sono disponibili con la versione Technical Preview di Configuration Manager più recente:

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-19082"></a>Technical Preview versione 1908.2

<!-- - [title](/sccm/core/get-started/2019/technical-preview-1901#bkmk_anchor) <!--ID-->

- [Miglioramenti per Connessioni di console](/sccm/core/get-started/2019/technical-preview-1908-2#improvements-to-console-connections) <!--4923997-->
- [Miglioramenti per i punti di distribuzione abilitati per il multicast](/sccm/core/get-started/2019/technical-preview-1908-2#bkmk_multicast) <!--3785535-->
- [Ottimizzazioni per il motore CMPivot](/sccm/core/get-started/2019/technical-preview-1908-2#optimizations-to-the-cmpivot-engine) <!--3197353-->
- [Impostare il layout della tastiera durante la distribuzione del sistema operativo](/sccm/core/get-started/2019/technical-preview-1908-2#bkmk_osd) <!--5138936-->

> [!Note]  
> Le funzionalità disponibili in una versione precedente della Technical Preview rimangono disponibili nelle versioni successive. Analogamente, le funzionalità aggiunte alla versione Current Branch di Configuration Manager rimangono disponibili nel ramo Technical Preview.  


## <a name="features-in-recent-technical-previews"></a>Funzionalità nelle anteprime tecniche recenti

Le funzionalità seguenti sono state rilasciate in versioni precedenti di Configuration Manager Technical Preview Branch dopo la versione Current Branch 1906:

### <a name="technical-preview-version-1908"></a>Technical Preview versione 1908

- [Miglioramenti delle prestazioni della sequenza di attività per le combinazioni per il risparmio di energia](/sccm/core/get-started/2019/technical-preview-1908#bkmk_tsperf) <!--3555926-->
- [Valutazione delle query sul dispositivo locale con CMPivot autonomo](/sccm/core/get-started/2019/technical-preview-1908#local-device-query-evaluation-using-cmpivot-standalone) <!--3197353-->
- [Filtro di aggiornamento software aggiuntivo per le regole di distribuzione automatica](/sccm/core/get-started/2019/technical-preview-1908#additional-software-update-filter-for-adrs) <!--4852033-->
- [Usare Ottimizzazione recapito per tutti gli aggiornamenti di Windows](/sccm/core/get-started/2019/technical-preview-1908#use-delivery-optimization-for-all-windows-updates) <!--4699118 (4685210)-->
- [Modelli di distribuzione in più fasi](/sccm/core/get-started/2019/technical-preview-1908#phased-deployment-templates) <!--4961086-->
- [Miglioramenti al nodo Connessioni di console](/sccm/core/get-started/2019/technical-preview-1908#improvements-to-console-connections-node) <!--4923997 (4951240)-->
- [Copiare e incollare le condizioni della sequenza di attività](/sccm/core/get-started/2019/technical-preview-1908#bkmk_tscondition) <!--4621098-->
- [Miglioramenti per la ricerca nell'editor della sequenza di attività](/sccm/core/get-started/2019/technical-preview-1908#bkmk_tssearch) <!--4621085-->
- [Miglioramenti alla distribuzione del sistema operativo](/sccm/core/get-started/2019/technical-preview-1908#bkmk_osd) <!--4910348, 4931110, 4977616-->

### <a name="technical-preview-version-1907"></a>Technical Preview versione 1907

- [Ricerca nell'editor delle sequenze di attività](/sccm/core/get-started/2019/technical-preview-1907#bkmk_tsedit) <!--4621085-->
- [Miglioramenti al dashboard Preparazione aggiornamenti per Office 365 ProPlus](/sccm/core/get-started/2019/technical-preview-1907#improvements-to-office-365-proplus-upgrade-readiness-dashboard) <!--4021125-->


> [!Tip]  
> Quando è disponibile una nuova versione Current Branch, le funzionalità presenti in tale versione sono elencate nella versione più recente dell'articolo *Novità*. Per altre informazioni, vedere [Novità delle versioni incrementali](/sccm/core/plan-design/changes/whats-new-incremental-versions#supported-versions).

<!-- This is the full list of new features in the past TP releases since the last CB release.
Each month, add features from the list above to a new H3 section at the top of this section.
When there's a new CB, add any features not in that CB to the table in H2 "Features in previous technical previews"
-->


## <a name="features-in-previous-technical-previews"></a>Funzionalità nelle versioni Technical Preview precedenti

Le funzionalità seguenti sono state rilasciate con le versioni precedenti del ramo Technical Preview di Configuration Manager. Queste funzionalità rimangono disponibili nelle versioni successive, ma non sono ancora disponibili in Current Branch.

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

| Funzionalità        | Versione Technical Preview |  
|----------------|---------------------------|
| Controllo remoto tramite il gateway di gestione cloud <!--4575930--> | [Tech Preview 1906](/sccm/core/get-started/2019/technical-preview-1906#remote-control-anywhere-using-cloud-management-gateway) |
| Miglioramento dell'hub della community <!--3555935--> | [Tech Preview 1906](/sccm/core/get-started/2019/technical-preview-1906#bkmk_hub) |
| Opzioni aggiuntive per i cataloghi di aggiornamenti di terze parti <!--4469002--> | [Tech Preview 1906](/sccm/core/get-started/2019/technical-preview-1906#additional-options-for-third-party-update-catalogs) |
| Sequenza di attività come tipo di distribuzione del modello di app <!--3555953--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_tsdt) |
| Gestione di BitLocker <!--3601034--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_bitlocker) |
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

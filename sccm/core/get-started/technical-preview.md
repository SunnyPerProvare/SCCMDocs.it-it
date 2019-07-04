---
title: Versioni di Technical Preview
titleSuffix: Configuration Manager
description: Informazioni sulla versione Technical Preview che consente di testare nuove funzionalità e capacità in Configuration Manager.
ms.date: 06/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2041f51714cbed7a9c9a1a3ad14bbb2d8c697ae4
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/20/2019
ms.locfileid: "67285978"
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

- **Technical preview versione 1902.2**: Configuration Manager Technical Preview versione 1902.2 è disponibile sia come aggiornamento nella console che come nuova versione di base. Scaricare le versioni di base dal [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

## <a name="BKMK_TPFeedback"></a> Invio di commenti e suggerimenti  

Microsoft sarebbe lieta di ricevere commenti e suggerimenti sulle nuove funzionalità della Technical Preview. Per altre informazioni, vedere la sezione su [commenti e suggerimenti per i prodotti](/sccm/core/understand/find-help#product-feedback).

Siamo anche interessati a conoscere le vostre idee su eventuali nuove funzionalità. Per inviare nuove idee e votare le idee presentate da altri, [visitare la pagina UserVoice](https://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->

## <a name="bkmk_tpCaps"></a> Funzionalità nella versione più recente  

Le funzionalità seguenti sono disponibili con la versione Technical Preview di Configuration Manager più recente:

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1906"></a>Anteprima tecnica versione 1906

<!-- - [title](/sccm/core/get-started/2019/technical-preview-1901#bkmk_anchor) <!--ID-->

- [Miglioramenti alle attività di manutenzione](/sccm/core/get-started/2019/technical-preview-1906#improvements-to-maintenance-tasks) <!--3555894-->
- [Monitoraggio dell'aggiornamento del database di Configuration Manager](/sccm/core/get-started/2019/technical-preview-1906#configuration-manager-update-database-upgrade-monitoring) <!--4200581-->
- [Più gruppi pilota per i carici di lavoro con co-gestione](/sccm/core/get-started/2019/technical-preview-1906#bkmk_comgmt_pilot) <!--3555750-->
- [Logica di notifica riprogettata per il nuovo software disponibile](/sccm/core/get-started/2019/technical-preview-1906#redesigned-notification-logic-for-newly-available-software) <!--3555904-->
- [Controllo degli accessi in base al ruolo nelle cartelle](/sccm/core/get-started/2019/technical-preview-1906#rbac-on-folders) <!--3600867-->
- [Individuazione dei gruppi utenti in Azure Active Directory](/sccm/core/get-started/2019/technical-preview-1906#bkmk_aad-disco) <!--3611956-->
- [Controllo remoto tramite Cloud Management Gateway](/sccm/core/get-started/2019/technical-preview-1906#remote-control-anywhere-using-cloud-management-gateway) <!--4575930-->
- [Miglioramento dell'hub della community](/sccm/core/get-started/2019/technical-preview-1906#bkmk_hub) <!--3555935-->
- [Aggiungere join, operatori aggiuntivi e aggregatori in CMPivot](/sccm/core/get-started/2019/technical-preview-1906#bkmk_cmpivot) <!--4054074-->
- [Miglioramenti di CMPivot](/sccm/core/get-started/2019/technical-preview-1906#improvements-to-cmpivot) <!--4619340,4683130-->
- [Miglioramenti della console di Configuration Manager](/sccm/core/get-started/2019/technical-preview-1906#bkmk_console) <!--4223683-->
- [Supporto per Desktop virtuale Windows](/sccm/core/get-started/2019/technical-preview-1906#bkmk_winsku) <!--3556025-->
- [Notifiche del conto alla rovescia più frequenti per i riavvii](/sccm/core/get-started/2019/technical-preview-1906#more-frequent-countdown-notifications-for-restarts) <!--3976435-->
- [Registrazione automatica della co-gestione tramite il token di dispositivo](/sccm/core/get-started/2019/technical-preview-1906#bkmk_comgmt) <!--4454491-->
- [Opzioni aggiuntive per i cataloghi di aggiornamenti di terze parti](/sccm/core/get-started/2019/technical-preview-1906#additional-options-for-third-party-update-catalogs) <!--4469002-->
- [Cancellare il contenuto dell'app dalla cache del client durante la sequenza di attività](/sccm/core/get-started/2019/technical-preview-1906#bkmk_tscache) <!--4485675-->
- [Nuova categoria di prodotti per Windows 10 versione 1903 e successive](/sccm/core/get-started/2019/technical-preview-1906#new-windows-10-version-1903-and-later-product-category) <!--4682946-->
- [Regola delle informazioni dettagliate sulla gestione per il fallback di NTLM](/sccm/core/get-started/2019/technical-preview-1906#bkmk_ntlm) <!--4572953-->
- [Filtrare le applicazioni distribuite nei dispositivi](/sccm/core/get-started/2019/technical-preview-1906#bkmk_appcategory) <!--4451056-->
- [Miglioramenti alla distribuzione del sistema operativo](/sccm/core/get-started/2019/technical-preview-1906#bkmk_osd) <!--4668846, 2840337, 4512937-->
- [Collegamento diretto a schede personalizzate in Software Center](/sccm/core/get-started/2019/technical-preview-1906#bkmk_swctr) <!--4655176-->

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
 | Controllo migliorato sulla manutenzione di WSUS <!--4110109--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#improved-control-over-wsus-maintenance) | ![Non aggiunta](media/Red_X.gif) |
 | Miglioramenti della console di Configuration Manager <!--4616810--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_console) | ![Non aggiunta](media/Red_X.gif) |
 | Configurare il tempo di esecuzione massimo predefinito per gli aggiornamenti software <!--3734426--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_timeout) | ![Non aggiunta](media/Red_X.gif) |
 | Criteri di attendibilità file di Windows Defender Application Guard <!--3555858--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_wdag) | ![Non aggiunta](media/Red_X.gif) |
 | Gruppi di applicazioni <!--3555907--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_app-group) | ![Non aggiunta](media/Red_X.gif) |
 | Sequenza di attività come tipo di distribuzione del modello di app <!--3555953--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_tsdt) | ![Non aggiunta](media/Red_X.gif) |
 | Gestione di BitLocker <!--3601034--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_bitlocker) | ![Non aggiunta](media/Red_X.gif) |
 | Debugger di sequenze di attività <!--3612274--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_tsdebug) | ![Non aggiunta](media/Red_X.gif) |
 | Ottimizzazione del recapito nel dashboard Origini dati del client <!--3555759--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_do) | ![Non aggiunta](media/Red_X.gif) |
 | Miglioramento dell'hub della community <!--4224401--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_hub) | ![Non aggiunta](media/Red_X.gif) |
 | Visualizzare il GUID SMBIOS nell'elenco dei dispositivi <!--4526580--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_smbios) | ![Non aggiunta](media/Red_X.gif) |
 | Visualizzatore log OneTrace <!--3555962--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_onetrace) | ![Non aggiunta](media/Red_X.gif) |
 | Miglioramenti all'infrastruttura di Software Center <!--3555950--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_swctr) | ![Non aggiunta](media/Red_X.gif) |
 | Miglioramenti delle personalizzazioni delle schede di Software Center <!--4063773--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#improvements-to-software-center-tab-customizations) | ![Non aggiunta](media/Red_X.gif) |
 | Miglioramenti delle approvazioni di app <!--4224910--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_approve) | ![Non aggiunta](media/Red_X.gif) |
 | Ripetere l'installazione delle applicazioni pre-approvate <!--4336307--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_retry) | ![Non aggiunta](media/Red_X.gif) |
 | Installare le applicazioni per un dispositivo <!--4402180--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_device-app) | ![Non aggiunta](media/Red_X.gif) |
 | Notifiche del conto alla rovescia più frequenti per i riavvii <!--3976435--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_restart) | ![Non aggiunta](media/Red_X.gif) |
 | Sincronizzare i risultati di appartenenza alla raccolta con i gruppi di Azure Active Directory <!--3607475--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_aadcollsync) | ![Non aggiunta](media/Red_X.gif) |
 | Configurare il periodo di conservazione minimo della cache del client <!--4485509--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_cache) | ![Non aggiunta](media/Red_X.gif) |
 | Miglioramenti della distribuzione del sistema operativo <!--4512937,4224642--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_osd) | ![Non aggiunta](media/Red_X.gif) |
 | Aggiungere un nodo SQL AlwaysOn <!--3127336--> | [Anteprima tecnica 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_sqlao) | ![Non aggiunta](media/Red_X.gif) |
 | Dashboard Preparazione aggiornamenti per Office 365 ProPlus <!--4021125--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#bkmk_o365) | ![Non aggiunta](media/Red_X.gif) |
 | Configurare l'aggiornamento dinamico durante gli aggiornamenti delle funzionalità <!--4062619--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#configure-dynamic-update-during-feature-updates) | ![Non aggiunta](media/Red_X.gif) |
 | Hub della community e GitHub <!--3555935,3555936--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#community-hub-and-github) | ![Non aggiunta](media/Red_X.gif) |
 | Modalità autonoma per CMPivot <!--3555890--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#bkmk_cmpivot) | ![Non aggiunta](media/Red_X.gif) |
 | Miglioramenti all'infrastruttura di Software Center <!--3555950--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#bkmk_swctr) | ![Non aggiunta](media/Red_X.gif) |
 | Controllo migliorato sulla manutenzione di WSUS <!--4110109--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#improved-control-over-wsus-maintenance) | ![Non aggiunta](media/Red_X.gif) |
 | Pre-cache per pacchetti di driver e immagini del sistema operativo <!--4224642--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#bkmk_precache) | ![Non aggiunta](media/Red_X.gif) |
 | Miglioramenti della distribuzione del sistema operativo <!--2839943,4447680--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#bkmk_osd) | ![Non aggiunta](media/Red_X.gif) |
 | Stima dei costi dei servizi cloud <!--3555774--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_cmg) | ![Non aggiunta](media/Red_X.gif) |
 | Usare il punto di distribuzione come server di cache locale per Ottimizzazione recapito <!--3555764--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_doinc) | ![Non aggiunta](media/Red_X.gif) |
 | Richiamare il blocco per la modifica delle sequenze di attività <!--3699337--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_sedo) | ![Non aggiunta](media/Red_X.gif) |
 | Drill-through degli aggiornamenti obbligatori <!--4224414--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_req-updates) | ![Non aggiunta](media/Red_X.gif) |
 | Miglioramento alla creazione del supporto per la sequenza di attività <!--4090666--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_tsmedia) | ![Non aggiunta](media/Red_X.gif) |


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

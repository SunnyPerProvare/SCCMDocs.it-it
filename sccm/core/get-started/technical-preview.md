---
title: Versioni di Technical Preview
titleSuffix: Configuration Manager
description: Informazioni sulla versione Technical Preview che consente di testare nuove funzionalità e capacità in Configuration Manager.
ms.date: 01/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cf432ea32e5946a98b59e158752b3e82cf63b3b3
ms.sourcegitcommit: b8167a60fd6f2d8387b2db723976c0e2c4198d33
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/24/2019
ms.locfileid: "54832772"
---
# <a name="technical-preview-for-configuration-manager"></a>Technical Preview per Configuration Manager

*Si applica a: System Center Configuration Manager (Technical Preview)*

Questo articolo include informazioni dettagliate sul ramo Technical Preview mensile di Configuration Manager. La versione Technical Preview introduce nuove funzionalità su cui Microsoft sta lavorando. Vengono introdotte nuove funzionalità non ancora incluse in Current Branch di Configuration Manager. Queste funzionalità potrebbero essere alla fine incluse in un aggiornamento a Current Branch. Prima di finalizzare le funzionalità, Microsoft invita gli utenti a provarle e a inviare commenti e suggerimenti.  

Poiché questa versione è una Technical Preview, dettagli e funzionalità sono soggetti a modifiche.  

Queste informazioni si applicano a tutte le versioni del ramo Technical Preview di Configuration Manager. Questo articolo elenca ogni nuova funzionalità insieme alla versione Technical Preview in cui compare per la prima volta. Ad esempio, la versione **1901** per gennaio (01) del 2019 (19). Le singole funzionalità sono descritte in dettaglio in articoli separati dedicati a ogni versione di anteprima.  

Per informazioni sulle novità della versione *Current Branch* di Configuration Manager, vedere [Novità delle versioni incrementali di Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions).



##  <a name="bkmk_reqs"></a> Requisiti e limitazioni  

> [!IMPORTANT]     
>  La Technical Preview viene concessa in licenza per essere usata esclusivamente in un ambiente lab. Microsoft potrebbe non offrire supporto tecnico e alcune funzionalità potrebbero non essere disponibili nel software di anteprima. Inoltre, il software di anteprima può essere caratterizzato da standard di sicurezza, privacy, accessibilità, disponibilità e affidabilità ridotti o diversi rispetto al software commercializzato.  

Per la maggior parte dei prerequisiti del prodotto, usare le informazioni in [Configurazioni supportate](/sccm/core/plan-design/configs/supported-configurations). Per il ramo Technical Preview si applicano le eccezioni seguenti:  

-   Ogni installazione rimane attiva per 90 giorni prima di diventare inattiva.  

-   L'inglese è l'unica lingua supportata.  

-   Supporta solo i parametri della riga di comando di installazione seguenti:  
    -   `/silent`  
    -   `/testdbupgrade`    

-   Il punto di connessione del servizio viene installato in modalità online. e non supporta la modalità offline.  

-   Gli articoli separati per ogni versione specifica della Technical Preview includono ulteriori limitazioni o requisiti, secondo il caso.

-   Le funzionalità seguenti non sono supportate con il ramo Technical Preview:  

    - [Migrazione](/sccm/core/migration/migrate-data-between-hierarchies) da o verso questo ramo di anteprima.  

    - [Aggiornamento](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) a questo ramo di anteprima.  

    - [Ripristino di siti](/sccm/core/servers/manage/recover-sites) dalla cartella cd.latest.  <!--507106-->

-   Non è previsto alcun supporto per l'aggiornamento a Current Branch da questo ramo di anteprima.  

    > [!Note]  
    > Se sono disponibili aggiornamenti per una versione di anteprima, è ancora possibile trovarli e installarli dal nodo **Aggiornamenti e manutenzione** della console di Configuration Manager. Per un video relativo al processo di aggiornamento nella console, vedere [Installing Configuration Manager update packages](https://www.youtube.com/embed/KBd_EGFbUT8) (Installazione dei pacchetti di aggiornamento di Configuration Manager) su youtube.com.  

-   Supporta solo un sito primario autonomo. Non è disponibile alcun supporto per un sito di amministrazione centrale, più siti primari o i siti secondari.  

I prodotti e tecnologie seguenti sono supportati dal ramo Technical Preview di Configuration Manager: 

-   Sono supportate solo le versioni seguenti di **SQL Server**:  

    -   SQL Server 2017 (con aggiornamento cumulativo 2 e versioni successive) a partire da Configuration Manager versione 1710
    -   SQL Server 2016 (senza Service Pack e versioni successive)
    -   SQL Server 2014 (con Service Pack 1 o versioni successive)
    -   SQL Server 2012 (con Service Pack 3 o versioni successive)  


-   Il sito supporta fino a 10 client, che devono eseguire una delle seguenti versioni di Windows:  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 7  

> [!Note]  
> L'inclusione di questi prodotti in questo contenuto non implica un'estensione del supporto per una versione oltre il ciclo di vita del supporto. Configuration Manager non supporta prodotti che non rientrano nel ciclo di vita del supporto. Per altre informazioni, vedere [Criteri relativi al ciclo di vita Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=208270).  



##  <a name="bkmk_install"></a> Installare e aggiornare  

Il ramo Technical Preview di Configuration Manager per l'uso in ambienti lab è diverso da Current Branch di Configuration Manager per l'uso in ambienti di produzione.  

Prima di tutto installare una versione di base del ramo Technical Preview. Dopo l'installazione di una versione di base, è possibile usare gli aggiornamenti nella console per aggiornare l'installazione con la versione di anteprima più recente. In genere, le nuove versioni Technical Preview sono disponibili ogni mese.

Microsoft supporta ogni versione Technical Preview fino a quando diventano disponibili tre versioni successive. Ad esempio, quando è stata rilasciata la versione 1708, la versione 1704 non era più inclusa nel supporto. Le versioni 1705, 1706 e 1707 sono rimaste incluse nel supporto. Quando una versione di base non è più inclusa nel supporto, è ancora supportata per l'installazione di un nuovo sito Technical Preview, presupponendo che venga eseguito l'aggiornamento immediato a una versione supportata. La versione di base precedente è supportata fino a quando non diventa disponibile una nuova versione di base. Eseguire l'aggiornamento alla versione più recente disponibile dalla versione di base e quindi ripetere il processo di aggiornamento fino a installare l'ultima versione Technical Preview.

> [!TIP]  
>  Quando si installa un aggiornamento della Technical Preview, si aggiorna l'installazione di anteprima alla nuova versione Technical Preview. Un'installazione Technical Preview non prevede mai la possibilità di eseguire l'aggiornamento a un'installazione Current Branch, né di ricevere gli aggiornamenti dalla versione Current Branch corrente. 
> 
> Più volte nel corso dell'anno diventano disponibili versioni del ramo Technical Preview e Current Branch con lo stesso numero di versione. Ad esempio, è presente una versione Technical Preview 1802 e una versione Current Branch 1802. 


### <a name="active-baseline-versions"></a>Versioni di base attive
   
È possibile installare una versione di base al massimo per un anno dopo il rilascio. Quando si installa un nuovo sito Technical Preview, se sono disponibili più versioni di base, usare la versione di base più recente.

-  **Technical Preview versione 1810.2**: Configuration Manager Technical Preview versione 1810.2 è disponibile sia come aggiornamento nella console che come nuova versione di base. Scaricare le versioni di base dal [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).



##  <a name="BKMK_TPFeedback"></a> Invio di commenti e suggerimenti  

Microsoft sarebbe lieta di ricevere commenti e suggerimenti sulle nuove funzionalità della Technical Preview. Per altre informazioni, vedere la sezione su [commenti e suggerimenti per i prodotti](/sccm/core/understand/find-help#product-feedback).

Siamo anche interessati a conoscere le vostre idee su eventuali nuove funzionalità. Per inviare nuove idee e votare le idee presentate da altri, [visitare la pagina UserVoice](https://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->



##  <a name="bkmk_tpCaps"></a> Funzionalità nella versione più recente  

Le funzionalità seguenti sono disponibili con la versione Technical Preview di Configuration Manager più recente: 

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1901"></a>Technical Preview versione 1901

<!-- - [title](/sccm/core/get-started/2019/technical-preview-1901#bkmk_anchor)<!--ID-->


- [Dashboard sull'integrità del client](/sccm/core/get-started/2019/technical-preview-1901#bkmk_health)<!--3599209-->  
- [Specifica la priorità per gli aggiornamenti delle funzionalità nella manutenzione di Windows 10](/sccm/core/get-started/2019/technical-preview-1901#bkmk_neo)<!--3734525-->  
- [Monitoraggio dedicato per le distribuzioni in più fasi](/sccm/core/get-started/2019/technical-preview-1901#bkmk_pod)<!--3555949--> 
- [Esegui CMPivot dal sito di amministrazione centrale](/sccm/core/get-started/2019/technical-preview-1901#bkmk_cmpivot)<!--3610960-->  
- [Miglioramenti al passaggio della sequenza di attività Esegui script PowerShell](/sccm/core/get-started/2019/technical-preview-1901#bkmk_posh)<!--3556028-->  
- [Prodotti Office nel dashboard del ciclo di vita](/sccm/core/get-started/2019/technical-preview-1901#bkmk_lifecycle)<!--3556026-->  
- [Regole di informazioni dettagliate di gestione per le raccolte](/sccm/core/get-started/2019/technical-preview-1901#bkmk_micoll)<!--3555752-->  
- [Eseguire la ricerca nelle visualizzazioni dispositivi mediante gli indirizzi MAC](/sccm/core/get-started/2019/technical-preview-1901#bkmk_mac)<!--3600878-->  
- [Modalità manutenzione per il punto di distribuzione](/sccm/core/get-started/2019/technical-preview-1901#bkmk_dpmaint)<!--3555754-->  
- [Servizio immagini ottimizzato](/sccm/core/get-started/2019/technical-preview-1901#bkmk_resetbase)<!--3555951-->  
- [Importare un indice singolo di un'immagine del sistema operativo](/sccm/core/get-started/2019/technical-preview-1901#bkmk_index)<!--3719699--> 
- [Usare Azure Resource Manager per i servizi cloud](/sccm/core/get-started/2019/technical-preview-1901#bkmk_arm)<!--3605704-->  
- [Conferma di commenti e suggerimenti della console](/sccm/core/get-started/2019/technical-preview-1901#bkmk_feedback)<!--3556010--> 
- [Creare un lab Configuration Manager Technical Preview in Azure](/sccm/core/get-started/2019/technical-preview-1901#bkmk_azurevm)<!--3556017-->  
- [Specificare una porta personalizzata per la riattivazione peer](/sccm/core/get-started/2019/technical-preview-1901#bkmk_sleep)<!--3605925-->  
- [Visualizzare le console connesse di recente](/sccm/core/get-started/2019/technical-preview-1901#bkmk_console)<!--3699367-->  
- [Arrestare il servizio cloud quando supera una soglia](/sccm/core/get-started/2019/technical-preview-1901#bkmk_cmg)<!--3735092--> 
- [Timeout della modalità di provisioning client](/sccm/core/get-started/2019/technical-preview-1901#bkmk_osdprov)<!--3197824-->
- [Miglioramenti della distribuzione del sistema operativo](/sccm/core/get-started/2019/technical-preview-1901#bkmk_osd)<!--3633146,3641475,3654172,3734270-->


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
 | Miglioramenti al passaggio della sequenza di attività Esegui script PowerShell <!--3556028 fka 1359389--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_posh) | ![Non aggiunta](media/Red_X.gif) | 
 | Miglioramenti alle approvazioni dell'applicazione tramite posta elettronica <!--3594063--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_email) | ![Non aggiunta](media/Red_X.gif) | 
 | Configurare l'affinità utente-dispositivo nel Software Center <!--3485366--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_uda) | ![Non aggiunta](media/Red_X.gif) | 
 | Miglioramenti alla console di Configuration Manager <!--3594151--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_console) | ![Non aggiunta](media/Red_X.gif) | 
 | Scaricare report dall'hub della community<!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) | ![Non aggiunta](media/Red_X.gif) | 
 | Non è necessario caricare i profili di Windows PowerShell <!--1359239--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_noprofile) | ![Non aggiunta](media/Red_X.gif) | 
 | Non è più necessaria una connessione a Intune per MDM locale <!--1359124--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_opmdm) | ![Non aggiunta](media/Red_X.gif) | 
 | Notifiche della console di Configuration Manager <!--1318035--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_notify) | ![Non aggiunta](media/Red_X.gif) | 
 | Miglioramenti nella creazione del supporto per la sequenza attività <!--1359388--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_tsmedia) | ![Non aggiunta](media/Red_X.gif) | 
 | Miglioramento al passaggio della sequenza di attività Esegui script PowerShell <!--1359389--> | [Tech Preview 1811](capabilities-in-technical-preview-1811.md#bkmk_posh) | ![Non aggiunta](media/Red_X.gif) | 
 | Miglioramenti alla valutazione delle raccolte <!--1358981--> | [Tech Preview 1810.2](capabilities-in-technical-preview-1810-2.md#bkmk_colleval) | Versione 1810 | 
 | Autenticazione dell'amministratore di Configuration Manager <!--1357013--> | [Tech Preview 1810.2](capabilities-in-technical-preview-1810-2.md#bkmk_auth) | Versione 1810 | 
 | Regola delle informazioni dettagliate sulla gestione per la versione del client di origine di peer cache <!--1358008--> | [Tech Preview 1810.2](capabilities-in-technical-preview-1810-2.md#bkmk_insights) | Versione 1810 | 
 | Miglioramenti al programma di installazione del client basato su Internet <!--1359181--> | [Tech Preview 1810.2](capabilities-in-technical-preview-1810-2.md#bkmk_cmg) | Versione 1810 | 
 | Convertire applicazioni in MSIX <!--1359029--> | [Tech Preview 1810.2](capabilities-in-technical-preview-1810-2.md#bkmk_msix) | Versione 1810 | 



## <a name="features-in-previous-technical-previews"></a>Funzionalità nelle versioni Technical Preview precedenti

Le funzionalità seguenti sono state rilasciate con le versioni precedenti del ramo Technical Preview di Configuration Manager. Queste funzionalità rimangono disponibili nelle versioni successive, ma non sono ancora disponibili in Current Branch. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

| Funzionalità        | Versione Technical Preview |  
|----------------|---------------------------|
| Dashboard della documentazione nella console <!--1357546--> | [Tech Preview 1810](capabilities-in-technical-preview-1810.md#bkmk_doc-dashboard) | 
| Hub della community <!--1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) | 
| Attività di sincronizzazione dei dispositivi in co-gestione con Intune <!--1358565--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_comgmt) | 
| Servizio risponditore PXE basato su client <!--1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| Supporto dell'avvio della rete PXE per IPv6 <!--1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Uso di Azure Active Directory <!--1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Valutazione della conformità degli aggiornamenti di Windows Update for Business <!--1235390--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
| Miglioramenti di Asset Intelligence <!--1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |
| Gli utenti finali possono installare le app dal portale aziendale <!--1037233?--> | [Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End) |



## <a name="see-also"></a>Vedere anche  

Per altre informazioni, vedere gli articoli seguenti:  

- [Valutare Configuration Manager in un lab](/sccm/core/get-started/evaluate-with-lab-environment)
- [Novità delle versioni incrementali di System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Introduzione a Configuration Manager](/sccm/core/understand/introduction)

> [!Tip]  
> Per altre informazioni sulle funzionalità Current Branch che richiedono il consenso per l'abilitazione, vedere [Funzionalità di versioni non definitive](/sccm/core/servers/manage/pre-release-features).  
> 
> Per altre informazioni sulle funzionalità Current Branch che è necessario abilitare in prima istanza, vedere [Abilitare le funzionalità facoltative degli aggiornamenti](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  

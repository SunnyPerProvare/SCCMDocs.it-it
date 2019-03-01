---
title: Strumenti di Configuration Manager
titleSuffix: Configuration Manager
description: Informazioni sugli strumenti che consentono di gestire e risolvere i problemi di infrastruttura di Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1479524f08f17aa59f6e7dc771253a4fb6720189
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131133"
---
# <a name="configuration-manager-tools"></a>Strumenti di Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Gli strumenti di Configuration Manager comprendono [strumenti basati su client](#client-tools) e [strumenti basati su server](#server-tools). Questi strumenti consentono di supportare e risolvere i problemi di infrastruttura di Configuration Manager. 

A partire dalla versione 1806 di Configuration Manager, questi strumenti sono inclusi nella cartella `CD.Latest\SMSSETUP\Tools` nel server del sito. Non è necessaria un'ulteriore installazione.<!--1357145--> Usare queste versioni degli strumenti con Configuration Manager versione 1806 e versioni successive.

Tutti i sistemi operativi Windows indicati come client supportati in [Sistemi operativi supportati per client e dispositivi](https://docs.microsoft.com/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) sono supportati per l'uso con questi strumenti.

> [!Note]  
> Il [System Center 2012 R2 Configuration Manager Toolkit](https://www.microsoft.com/en-us/download/details.aspx?id=50012) è ancora disponibile nell'Area download Microsoft. Per Configuration Manager versione 1806 e versioni successive, usare le versioni degli strumenti nella cartella CD.Latest nel server del sito. Alcuni strumenti erano precedentemente presenti nel toolkit ma non sono stati inclusi nella versione 1806. Questi strumenti legacy non sono più supportati.


## <a name="client-tools"></a>Strumenti client

- [CMTrace](/sccm/core/support/cmtrace): consente di visualizzare, monitorare e analizzare i file di log di Configuration Manager  

- [Client Spy](/sccm/core/support/clispy): consente di risolvere i problemi relativi alla distribuzione del software, all'inventario e alla misurazione

- [Deployment Monitoring Tool](/sccm/core/support/deployment-monitoring-tool): consente di risolvere i problemi di applicazioni, aggiornamenti e distribuzioni delle linee di base  

- [Policy Spy](/sccm/core/support/policy-spy): consente di visualizzare le assegnazioni dei criteri  

- [Power Viewer Tool](/sccm/core/support/power-viewer-tool): consente di visualizzare lo stato della funzionalità di risparmio energia  

- [Send Schedule Tool](/sccm/core/support/send-schedule-tool): consente di attivare pianificazioni e valutazioni delle linee di base di configurazione  

> [!Note]  
> La cartella ClientTools include anche il file Microsoft.Diagnostics.Tracing.EventSource.dll. Diversi strumenti client richiedono questa libreria. Non è possibile utilizzarla direttamente.  


## <a name="server-tools"></a>Strumenti server

- [DP Job Queue Manager](/sccm/core/support/dp-job-manager): consente di risolvere i problemi dei processi di distribuzione del contenuto ai punti di distribuzione  

- [Collection Evaluation Viewer](/sccm/core/support/ceviewer): consente di visualizzare informazioni dettagliate sulla valutazione della raccolta  

- [Content Library Explorer](/sccm/core/support/content-library-explorer): consente di visualizzare il contenuto dell'archivio a istanza singola della raccolta contenuto  

- [Content Library Transfer](/sccm/core/support/content-library-transfer): trasferisce la raccolta contenuto tra diverse unità  

- [Content Ownership Tool](/sccm/core/support/content-ownership-tool): modifica la proprietà dei pacchetti orfani. Questi pacchetti sono presenti nel sito senza un server del sito proprietario.  

- [Role-based Administration and Auditing Tool](/sccm/core/support/rbaviewer): consente agli amministratori di controllare la configurazione dei ruoli  

- [Run Meter Summarization Tool](/sccm/core/support/run-meter-summ): consente di eseguire l'attività di riepilogo misurazione e di analizzare i dati di misurazione

> [!Note]  
> La cartella ServerTools include anche i file seguenti 
> - AdminUI.WqlQueryEngine.dll
> - Microsoft.ConfigurationManagement.ManagementProvider.dll
> - Microsoft.Diagnostics.Tracing.EventSource.dll. 
>
> Diversi strumenti server richiedono queste librerie. Non è possibile utilizzarli direttamente.  



## <a name="other-tools"></a>Altri strumenti

- [Strumento di pulizia della raccolta contenuto](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool): usare **ContentLibraryCleanup.exe** in `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` per rimuovere contenuto orfano da un punto di distribuzione.  

- [Strumento Gestione gerarchia](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe): usare **Preinst.exe** nella cartella condivisa `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` nel server del sito per passare i comandi al componente di gestione della gerarchia.  

- [Strumento di reimpostazione dell'aggiornamento](/sccm/core/servers/manage/update-reset-tool): usare **CMUpdateReset.exe** in `CD.Latest\SMSSETUP\TOOLS\CMUpdateReset` per risolvere i problemi quando gli aggiornamenti nella console registrano problemi di download o replica.  

- [Strumento Connessione al servizio](/sccm/core/servers/manage/use-the-service-connection-tool): usare **ServiceConnectionTool.exe** in `CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool` per mantenere aggiornato il sito quando il punto di connessione del servizio è offline.  

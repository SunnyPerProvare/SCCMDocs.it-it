---
title: Monitorare i client con Windows Analytics
titleSuffix: Configuration Manager
description: Windows Analytics è un set di soluzioni che consentono di ottenere indicazioni preziose sullo stato corrente dell'ambiente.
ms.date: 10/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c2530b20d065b3b2bd15c0dc38232687d286b6b0
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "72384744"
---
# <a name="use-windows-analytics-with-configuration-manager"></a>Usare Windows Analytics con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

> [!Important]  
> A partire da ottobre 2019, l'integrazione di Windows Analytics in Configuration Manager è una [funzionalità deprecata](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Il servizio Windows Analytics verrà ritirato il 31 gennaio 2020.
>
> [Desktop Analytics ](/sccm/desktop-analytics/overview) è l'evoluzione di Windows Analytics. I clienti esistenti di Windows Analytics possono [eseguire la migrazione a Desktop Analytics](/sccm/desktop-analytics/faq#existing-windows-analytics-customers).
>
> Per altre informazioni, vedere [KB 4521815: Ritiro di Windows Analytics il 31 gennaio 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

[Windows Analytics](https://docs.microsoft.com/windows/deployment/update/windows-analytics-overview) è un set di soluzioni che consentono di ottenere indicazioni sullo stato corrente dell'ambiente. I dispositivi Windows dell'ambiente segnalano a Microsoft dati a cui poter accedere e da poter analizzare tramite queste soluzioni. Ad esempio, connettere [Preparazione aggiornamenti](/sccm/core/clients/manage/upgrade-readiness) a Configuration Manager per accedere direttamente ai dati nell'area di lavoro **Monitoraggio** della console di Configuration Manager.

I dati usati da Windows Analytics non vengono trasferiti direttamente al server del sito di Configuration Manager. I computer client inviano i dati al servizio cloud di Windows. Tale servizio trasferisce quindi i dati pertinenti alle soluzioni di Windows Analytics ospitate in una delle aree di lavoro dell'organizzazione. Configuration Manager indirizza quindi ai dati pertinenti del portale Web con collegamenti contestualizzati. Può anche visualizzare direttamente i dati che fanno parte delle soluzioni connesse a Configuration Manager.

> [!Important]  
> Configuration Manager segnala i dati di diagnostica e di utilizzo a Microsoft. Questi dati sono separati dai dati di Windows Analytics. Per altre informazioni, vedere [Diagnostica e dati di utilizzo](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).  



## <a name="configure-clients-to-report-data-to-windows-analytics"></a>Configurare i client per segnalare i dati a Windows Analytics

Per fare in modo che i dispositivi client segnalino i dati a Windows Analytics, configurarli con una *chiave ID commerciale*. Questa chiave è l'area di lavoro di Log Analytics che ospita i dati di Windows Analytics. Configurare anche i dispositivi per segnalare i dati a un livello appropriato per le soluzioni specifiche che si vogliono usare. 

### <a name="configure-windows-analytics-client-settings"></a>Configurare le impostazioni client di Windows Analytics
Per configurare Windows Analytics: 
1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione** e selezionare il nodo **Impostazioni client**.  
2. Nella barra multifunzione selezionare **Crea impostazioni dispositivo client personalizzate**.  
3. Aggiungere il gruppo **Windows Analytics** a questo criterio delle impostazioni del dispositivo client personalizzate.  

Per altre informazioni sulla creazione delle impostazioni personalizzate del dispositivo client, vedere [Come configurare le impostazioni client](/sccm/core/clients/deploy/configure-client-settings).

Selezionare la scheda delle impostazioni di **Windows Analytics** e configurare le impostazioni seguenti:  

#### <a name="manage-windows-telemetry-settings-with-configuration-manager"></a>Gestire le impostazioni della Telemetria di Windows con Configuration Manager
Impostare questa opzione su **Sì** per configurare le impostazioni dei dati di diagnostica di Windows nei client Windows.   

#### <a name="commercial-id-key"></a>Chiave ID commerciale
La chiave ID commerciale esegue il mapping delle informazioni dai dispositivi gestiti all'area di lavoro di Log Analytics che ospita i dati di Windows Analytics dell'organizzazione. Se è già stata configurata una chiave ID commerciale per l'uso con Preparazione aggiornamenti, usare tale ID. Se non è ancora disponibile una chiave ID commerciale, vedere [Copiare la chiave ID commerciale](https://docs.microsoft.com/windows/deployment/update/windows-analytics-get-started#copy-your-commercial-id-key).

#### <a name="windows-10-telemetry"></a>Telemetria di Windows 10
Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels) (Configurare i dati di diagnostica di Windows nell'organizzazione).

> [!Note]  
> È anche possibile impostare il livello di raccolta dei dati di Windows 10 su **Avanzata (con limitazioni)** . Questa impostazione consente di ottenere informazioni utili sui dispositivi presenti nell'ambiente in uso senza che i dispositivi segnalino tutti i dati nel livello **avanzato** con Windows 10 1709 o versione successiva. Il livello Avanzata (con limitazioni) include metriche del livello di base e un subset di dati raccolti dal livello avanzato pertinenti per Windows Analytics.

#### <a name="windows-81-and-earlier-telemetry"></a>Telemetria di Windows 8.1 e versioni precedenti   
Per altre informazioni, vedere [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields](https://go.microsoft.com/fwlink/?LinkID=822965) (Eventi e campi di valutazione telemetrica per Windows 7, Windows 8 e Windows 8.1).

#### <a name="enable-windows-81-and-earlier-internet-explorer-data-collection"></a>Abilita la raccolta di dati di Internet Explorer in Windows 8.1 e versioni precedenti
Nei dispositivi che eseguono Windows 8.1 o versioni precedenti Internet Explorer può raccogliere dati sulle app Web. Questi dati possono consentire a Preparazione aggiornamenti di rilevare incompatibilità di applicazioni Web che potrebbero impedire un aggiornamento semplice e rapido a Windows 10. Abilitare la raccolta dati di Internet Explorer in base all'area Internet. Per altre informazioni sulle aree Internet, vedere [About URL Security Zones](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/ms537183\(v=vs.85\)) (Informazioni sulle aree di sicurezza degli URL).



## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>Usare Preparazione aggiornamenti per identificare i problemi di compatibilità con Windows 10

Preparazione aggiornamenti consente di analizzare la conformità e la compatibilità dei dispositivi con Windows 10. Questa valutazione facilita l'esecuzione degli aggiornamenti. Dopo avere connesso Configuration Manager a Preparazione aggiornamenti, accedere ai dati di compatibilità dell'aggiornamento dei client direttamente nella console di Configuration Manager. Quindi specificare i dispositivi da aggiornare o correggere dall'elenco relativo.

Per altre informazioni e dettagli su come configurare e connettersi a Preparazione aggiornamenti, vedere [Preparazione aggiornamenti](/sccm/core/clients/manage/upgrade-readiness).



## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>Usare Windows Analytics per identificare le lacune nei criteri di Windows Information Protection

È possibile configurare i dispositivi Windows 10 versione 1703 e successive con un criterio [Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP). Tali dispositivi segnalano i dati di diagnostica nelle applicazioni che accedono ai dati aziendali dell'ambiente, ma non sono inclusi nelle regole di applicazione dei criteri. Tali applicazioni possono essere necessarie agli utenti al fine di mantenere una produttività elevata ma Windows Information Protection ne blocca l'accesso. Queste informazioni sono utili per gestire i criteri di Windows Information Protection in Configuration Manager. 


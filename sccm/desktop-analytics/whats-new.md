---
title: Novità di Desktop Analytics
titleSuffix: Configuration Manager
description: Riepilogo delle nuove funzionalità della versione mensile più recente del servizio cloud Desktop Analytics.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: fa300181-86cb-4afe-8fbf-895a7572378d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c1b17fdc85f0128e7a59a01c5e07a1afe7431c35
ms.sourcegitcommit: ccc3c929b5585c05d562020e68044de7d7e11c6a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2020
ms.locfileid: "80597027"
---
# <a name="whats-new-in-desktop-analytics"></a>Novità di Desktop Analytics

Informazioni sulle novità mensili di Desktop Analytics.

> [!TIP]
> L'implementazione degli aggiornamenti mensili può richiedere fino a tre giorni. Alcune funzionalità possono essere implementate in diverse settimane e durante la prima è possibile che non siano disponibili per tutti i clienti.

Per ricevere una notifica quando questa pagina viene aggiornata, copiare e incollare l'URL seguente nel lettore di feed RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+desktop+analytics+-+Configuration+Manager%22&locale=en-us`
<!-- a locale is required for the RSS search string -->

## <a name="march-2020"></a>Marzo 2020

### <a name="support-for-multiple-hierarchies"></a>Supporto di più gerarchie

<!-- 4814075, 6079184 -->

È ora possibile connettere più gerarchie di Configuration Manager a un singolo tenant di Azure Active Directory con un unico ID commerciale per Desktop Analytics. Il portale categorizza i dispositivi da diverse gerarchie e migliora le esperienze per i progetti pilota globali e i piani di distribuzione.

- Quando si configura il progetto pilota globale, se si includono raccolte che contengono più del 20% dei dispositivi registrati totali, nel portale viene visualizzato un avviso.
- Quando si crea un piano di distribuzione, se si selezionano raccolte per più gerarchie, nel portale viene visualizzato un avviso.

> [!NOTE]
> Il supporto di più gerarchie richiede Configuration Manager versione 1910 o successiva.

Per altre informazioni, vedere gli articoli seguenti:

- [Progetto pilota globale](/configmgr/desktop-analytics/deploy-pilot#bkmk_GlobalPilot)
- [Come creare i piani di distribuzione](/configmgr/desktop-analytics/create-deployment-plans)

### <a name="identify-compatibility-safeguards"></a>Identificare le misure di sicurezza per la compatibilità

<!-- 5746559 -->

I dati di compatibilità di Windows classificano alcune app e driver con una *misura di sicurezza*, che può causare l'esito negativo o il rollback dell'aggiornamento a Windows 10. Desktop Analytics consente ora di identificare queste misure di sicurezza in anticipo, in modo da poter correggere la risorsa prima di distribuire l'aggiornamento. Per altre informazioni, vedere [Valutazione della compatibilità - Misure di sicurezza](/configmgr/desktop-analytics/compat-assessment#safeguards).

## <a name="january-2020"></a>Gennaio 2020

### <a name="additional-app-usage-detail"></a>Ulteriori dettagli sull'utilizzo delle app

<!-- 5533890 -->

Quando si seleziona un'app per visualizzare altre informazioni, nel riquadro dei dettagli sono ora incluse informazioni aggiuntive sull'utilizzo. È possibile usare questi dati per esaminare la gamma di installazioni per un'app, nonché i dispositivi in cui gli utenti usano regolarmente l'app. Per altre informazioni, vedere [Asset - App - Utilizzo](/configmgr/desktop-analytics/about-assets#usage).

### <a name="provide-feedback-on-desktop-analytics"></a>Inviare commenti e suggerimenti su Desktop Analytics

<!-- 5451636 -->

Per condividere i propri commenti e suggerimenti per Desktop Analytics, selezionare l'icona **Invia smile** nella parte superiore del portale sulla destra. Per altre informazioni, vedere [Condividere commenti e suggerimenti sul prodotto](/configmgr/desktop-analytics/get-support#bkmk_feedback).

## <a name="october-2019"></a>Ottobre 2019

### <a name="improvements-to-compatibility-recommendations"></a>Miglioramenti ai consigli per la compatibilità

<!-- 3594545 -->

Desktop Analytics offre ora maggiori dettagli quando rileva che l'aggiornamento di Windows causerà la rimozione completa o parziale di un'applicazione o un driver. Per altre informazioni, vedere [Valutazione della compatibilità](/sccm/desktop-analytics/compat-assessment#asset-is-removed-during-upgrade).

### <a name="migrate-from-windows-analytics-to-existing-tenant"></a>Eseguire la migrazione da Windows Analytics al tenant esistente

<!-- 5202803 -->

È ora possibile migrare gli input da un'area di lavoro di Windows Analytics esistente dopo l'onboarding in Desktop Analytics.

## <a name="september-2019"></a>Settembre 2019

### <a name="migrate-inputs-from-windows-analytics"></a>Eseguire la migrazione degli input da Windows Analytics

<!-- 4252663 -->

Durante l'onboarding è ora possibile eseguire la migrazione degli input da un'area di lavoro di Windows Analytics esistente.

### <a name="offboard-from-desktop-analytics"></a>Eseguire l'offboarding da Desktop Analytics

<!-- 4972396 -->

Se si configura Desktop Analytics nell'ambiente ma si vuole smettere di usare il servizio, è ora possibile chiudere l'account. Se si cambia idea entro 90 giorni, è possibile riattivarlo. Per altre informazioni, vedere [Come chiudere l'account](/sccm/desktop-analytics/account-close).

## <a name="august-2019"></a>Agosto 2019

### <a name="reset-your-account"></a>Reimpostare l'account

<!-- 3733897 -->

Se si configura Desktop Analytics nell'ambiente ma si vuole ricominciare con l'onboarding e la registrazione, è ora possibile reimpostare l'account. Per altre informazioni sul processo, vedere [Reimpostare l'account](/sccm/desktop-analytics/account-reset).

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a>Decisione di aggiornamento automatico delle app di sistema e dello Store

<!-- 3587232 -->

Per facilitare l'annotazione di app importanti, alcuni tipi di app vengono contrassegnati automaticamente come *Non importante*. La decisione di aggiornamento del piano di distribuzione per queste app è contrassegnata anche con *Pronto*. Le app seguenti sono compatibili e continueranno a funzionare dopo l'aggiornamento di Windows:

- App di sistema e componenti pubblicati da Microsoft

- App gestite e aggiornate da Microsoft Store

Per altre informazioni, vedere [Decisione di aggiornamento automatico delle app di sistema e dello Store](/sccm/desktop-analytics/about-assets#bkmk_plan-autoapp).

## <a name="whats-new-in-configuration-manager"></a>Novità di Configuration Manager

La documentazione di Desktop Analytics fa sempre riferimento alla funzionalità della versione più recente di Configuration Manager Current Branch. Per altre informazioni sulle modifiche più recenti di Configuration Manager, vedere gli articoli seguenti:

<!-- - [What's new in version 1910](/sccm/core/plan-design/changes/whats-new-in-version-1910#bkmk_da) -->

- [Novità della versione 1906](/sccm/core/plan-design/changes/whats-new-in-version-1906#bkmk_da)

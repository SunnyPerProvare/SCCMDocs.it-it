---
title: Pronto per Windows
titleSuffix: Configuration Manager
description: Informazioni sul ritiro del sito web pronto per Windows
ms.date: 10/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 3f09226c-4ca7-4e43-9ae8-5ee6e78e6bc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 338ef88d4fa32767d9e4eb605a4ad800c11dbfce
ms.sourcegitcommit: c25a91db838805eca5dbb421a3de401928968bf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/30/2019
ms.locfileid: "73142947"
---
# <a name="ready-for-modern-desktop-retirement-faq"></a>Domande frequenti sul ritiro dei desktop moderni

<!-- placeholder -->

## <a name="general"></a>Generale

### <a name="what-happened-to-the-ready-for-windows-website"></a>Che cosa è successo al sito Web di pronto per Windows?

Molti clienti hanno problemi a ricevere e rimanere aggiornati con Windows 10 e Office 365 ProPlus. Il problema principale è quello di testare le applicazioni, perché questo processo è in genere manuale. Per gli amministratori IT e i proprietari delle applicazioni è necessario molto tempo per analizzare continuamente le applicazioni esistenti e quindi correggere eventuali problemi.

Il *pronto per la directory desktop moderna* elenca le soluzioni software supportate e in uso sui dispositivi commerciali che eseguono Windows 10 e Office 365 ProPlus. La directory consente ai responsabili IT di prendere in considerazione le versioni più recenti di Windows 10 e Office 365 per le distribuzioni.

Il feedback dei responsabili IT è che desiderano integrare queste informazioni dettagliate con gli strumenti che già utilizzano per pianificare i piani di distribuzione. Usare le funzionalità di conformità di ProPlus di [Desktop Analytics](https://aka.ms/dadocs) e [office 365](https://docs.microsoft.com/deployoffice/readiness-tools#office-365-proplus-readiness-features-in-configuration-manager-current-branch) in Configuration Manager per pianificare e gestire i progetti di aggiornamento di Windows 10 e Office 365 ProPlus. 

### <a name="what-is-desktop-analytics"></a>Che cos'è Desktop Analytics?

[Desktop Analytics](https://aka.ms/dadocs) è un servizio basato sul cloud che si integra con Configuration Manager. Il servizio fornisce informazioni e informazioni per prendere decisioni più informate sulla preparazione degli aggiornamenti degli endpoint di Windows. Combina i dati specifici dell'organizzazione con informazioni dettagliate aggregate dai milioni di dispositivi Windows connessi ai servizi cloud Microsoft.

-   Ottenere una visualizzazione completa degli endpoint, delle applicazioni e dei driver gestiti nella propria organizzazione.

-   Valutazione della compatibilità di applicazioni e driver con gli aggiornamenti delle funzionalità di Windows più recenti. Ricevere consigli di mitigazione per i problemi noti, nonché informazioni dettagliate avanzate per le app line-of-business.

-   Usa l'intelligenza artificiale da Microsoft Cloud per ottimizzare il set di dispositivi pilota che rappresentano in modo adeguato l'ambiente globale.

### <a name="why-should-i-use-desktop-analytics-for-my-windows-deployment-plans"></a>Perché usare analisi del desktop per i piani di distribuzione Windows?

Desktop Analytics offre i vantaggi seguenti:

-   **Inventario di dispositivi e software**: inventario di fattori chiave come app e versioni di Windows.

-   **Identificazione pilota**: identificazione del set più piccolo di dispositivi che forniscono la più ampia copertura di fattori. Questo argomento è incentrato sui fattori che sono più importanti per un progetto pilota di aggiornamenti e aggiornamenti di Windows. Assicurarsi che il progetto pilota abbia un maggiore successo consente di continuare in modo più rapido e sicuro per le distribuzioni più ampie nell'ambiente di produzione.

-   **Identificazione del problema**: usando dati di mercato aggregati insieme ai dati dell'ambiente, il servizio prevede potenziali problemi per ottenere e rimanere aggiornati con Windows. Suggerisce quindi potenziali mitigazioni.

-   **Integrazione di Configuration Manager**: il cloud it consente l'infrastruttura locale esistente. Usare questi dati e analisi per distribuire e gestire Windows sui dispositivi.

### <a name="what-does-the-ready-for-windows-status-mean-in-desktop-analytics"></a>Cosa significa lo stato di *pronto per Windows* in analisi desktop?

Lo **stato di adozione** si basa sulle informazioni provenienti da dispositivi commerciali che condividono dati con Microsoft. Lo stato è integrato con le istruzioni di supporto dei fornitori di software.

Desktop Analytics fornisce lo stato di adozione per ogni versione di un asset presente nei dispositivi commerciali. Questo stato non include i dati di dispositivi consumer o dispositivi che non condividono i dati. Lo stato potrebbe non essere rappresentativo della velocità di adozione in tutti i dispositivi Windows 10.

Per ulteriori informazioni, vedere [Compatibility assessment](/sccm/desktop-analytics/compat-assessment#ready-for-windows).

### <a name="what-assets-get-the-ready-for-windows-status-in-desktop-analytics"></a>Quali asset ottengono lo stato *pronto per Windows* in analisi desktop? 

Gli asset hanno lo stato *Ready for Windows* in desktop Analytics se:

-   Il provider software dichiara il supporto per la soluzione.
-   I clienti lo hanno distribuito su un numero significativo di dispositivi Windows 10 commerciali che condividono informazioni con Microsoft.
-   L'asset è pertinente per gli utenti commerciali.

### <a name="what-additional-insights-do-i-get-in-desktop-analytics"></a>Quali informazioni aggiuntive sono reperibili in analisi desktop?

Desktop Analytics fornisce un inventario dei [dispositivi e delle app installate](/sccm/desktop-analytics/about-assets), nonché [informazioni avanzate](/sccm/desktop-analytics/compat-assessment#advanced-insights) per le app line-of-business. 

## <a name="software-providers"></a>Provider di software

### <a name="can-i-still-list-my-software-solution-in-desktop-analytics"></a>È ancora possibile elencare la soluzione software in analisi desktop?

Pubblicare un'istruzione di supporto che il prodotto funziona con Windows 10 o ProPlus a 32 bit o a 64 bit oppure Office 365. Per presentare le soluzioni in analisi desktop, rivolgersi al contatto Microsoft.

### <a name="how-can-listing-my-solutions-benefit-me"></a>Come è possibile elencare le soluzioni?

Migliaia di amministratori IT gestiscono milioni di dispositivi con Configuration Manager e desktop Analytics. Questi strumenti vengono usati per pianificare e aggiornare in modo sicuro le proprie organizzazioni alla versione più recente di Windows 10 e Office 365 ProPlus. Vengono inoltre utilizzate per prendere decisioni di acquisto per le soluzioni software.

Microsoft integra le istruzioni di supporto dei fornitori di software con le informazioni di adozione ricevute dai dispositivi commerciali. Le organizzazioni in tutto il mondo usano questi dati in analisi desktop e strumenti di preparazione per Office. 

Se le istruzioni di supporto non sono associate correttamente agli asset, rivolgersi al proprio contatto Microsoft.

### <a name="can-i-see-detailed-performance-metrics-on-my-assets"></a>È possibile visualizzare le metriche dettagliate delle prestazioni sulle risorse personali?

Valutare le prestazioni delle soluzioni con i report sull'integrità e sulle metriche tramite il centro per sviluppatori: 

- [Windows Store](https://docs.microsoft.com/windows/uwp/publish/health-report)
- [Desktop](https://docs.microsoft.com/windows/desktop/appxpkg/windows-desktop-application-program)
- [Componenti aggiuntivi di Office](https://docs.microsoft.com/office/dev/store/update-unpublish-and-view-metrics) 

### <a name="how-can-i-develop-compatible-assets-for-windows-10-and-office-365-proplus"></a>Come è possibile sviluppare asset compatibili per Windows 10 e Office 365 ProPlus?

Assicurarsi che le applicazioni desktop siano compatibili adesso e rimanere compatibili con Windows 10 in futuro. Per ulteriori informazioni, vedere [compatibilità delle applicazioni per gli sviluppatori](https://developer.microsoft.com/windows/desktop/app-compatibility).

Se si sviluppano soluzioni per Office 365 ProPlus, vedere [procedure consigliate per lo sviluppo di componenti aggiuntivi com, VSTO e VBA in Office](https://docs.microsoft.com/visualstudio/vsto/development-best-practices-for-com-vsto-and-vba-add-ins-in-office).

---
title: Monitoraggio dello stato di integrità
titleSuffix: Configuration Manager
description: Informazioni sull'uso di monitoraggio dello stato di integrità in Desktop Analitica.
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5dc3123763430dc35d566b68e3c1c04762d26de5
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159043"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>Stato di integrità monitoraggio in Desktop Analitica

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Come si [distribuire un aggiornamento nell'ambiente di produzione](/sccm/desktop-analytics/deploy-prod), utilizzare Desktop Analitica per monitorare lo stato di integrità dei dispositivi. Questo articolo illustra in dettaglio come funziona il monitoraggio dell'integrità.

Per altre informazioni su come usare questa funzionalità, vedere [monitorare l'integrità dei dispositivi aggiornati](/sccm/desktop-analytics/deploy-prod#bkmk_monitor).

![Screenshot della pagina di monitoraggio dell'integrità di Analitica Desktop](media/monitor-health.png)

> [!NOTE]  
> Desktop Analitica raccoglie solo i dati di integrità da dispositivi che forniscono i dati di utilizzo che può essere usato come denominatore. Ciò significa che non include i dispositivi che eseguono Windows 7 e Windows 10 che non sono impostati per condividere i dati di diagnostica a livello di Enhanced (Limited). Se più del 10% di dispositivi che eseguono Windows 10 sono impostate per condividere i dati di diagnostica a livelli diversi dal Enhanced (Limited), il **monitorare l'integrità** pagina viene visualizzato un avviso nell'area dell'intestazione.  

Per visualizzare ulteriori informazioni su un'app specifica, selezionarla nell'elenco.



## <a name="apps"></a>App

![Fattori di stato di integrità per un'app in Desktop Analitica](media/monitor-health-status-factors.png)

Analitica desktop consente di monitorare i seguenti fattori lo stato di integrità per le app:

- **Percentuale di dispositivi con arresti anomali del sistema**: Per le ultime due settimane, il numero di dispositivi in cui questa app specifica è arrestato in modo anomalo diviso per il numero di dispositivi in cui è stato usato l'app. In questa vista consente di verificare se la stabilità dell'app è aumentato o diminuito sulla nuova versione del sistema operativo. Analitica desktop consente di calcolare tale percentuale per i set seguenti:  

    - **Dopo l'aggiornamento**: Dispositivi che hanno aggiornato alla versione del sistema operativo di destinazione specificata del piano di distribuzione. Per ridurre il numero degli asset con dati sufficienti, Analitica Desktop raccoglie i dati per tutti i dispositivi aggiornati. Questo set include i dispositivi non nel piano di distribuzione.  

    - **Prima dell'aggiornamento**: Dispositivi che usano una versione del sistema operativo precedente a quello specificato nel piano di distribuzione. Questo elenco non include i dispositivi che eseguono Windows 7.  

    - **Media commerciale**: La media (avg) degli arresti anomali di frequenza tra tutti i dispositivi commerciali. Tale Media viene calcolata nel *tutti* versioni dell'app. Se la versione indica una frequenza di arresto anomalo del sistema di sopra della media commerciale, potrebbe esserci una versione più stabile disponibile.  

- **% Sessioni con gli arresti anomali**: Simile al precedente, ma i conteggi la percentuale di sessioni con gli arresti anomali nelle ultime due settimane.  

Per determinare lo stato di integrità di un'app, Analitica Desktop richiede i dati dai dispositivi almeno 20. In caso contrario segnala **dati insufficienti** per l'app. Il servizio calcola lo stato di integrità in base il *percentuale di arresti anomali sessione* da questi dispositivi. La frequenza di arresto anomalo del sistema del dispositivo viene fornita solo a scopo informativo. Può non viene utilizzato nel calcolo dello stato di integrità.

Nella parte inferiore della pagina di dettagli dell'app, le tre schede seguenti consentono di risolvere i problemi:

- **Altre versioni**: Elenco di versioni alternative di questa app. Per ogni versione, Mostra le modifiche relative alle tariffe di arresto anomalo del sistema all'interno dell'organizzazione e la media commerciale. Se si trova una versione successiva dell'app con una frequenza inferiore di arresto anomalo del sistema, l'aggiornamento dell'app possono essere utili.  

    Indica inoltre se la versione ha una **pronto per Windows** segnale. Per altre informazioni, vedere [valutazione della compatibilità](/sccm/desktop-analytics/compat-assessment#risk-assessment-engine).  

- **Problemi principali**: Elenco di ID errore più frequente dal numero di istanze. L'analisi dello stack associato con l'arresto anomalo è identificata da un ID di errore. Quando si chiama il fornitore dell'app per il supporto, è possibile usare questo ID.  

- **Arresti anomali del sistema recenti**:  Un elenco di dispositivi in cui l'app recente arrestato in modo anomalo. È possibile filtrare per ID di errore e ad altri criteri. Usare queste informazioni per risolvere il problema per la raccolta dei log o sta tentando di correzioni in dispositivi specifici prima di provare una distribuzione più ampia.  

Se si trova una regressione tramite integrità grave che non si riesce a risolvere, modificare l'app **decisione di aggiornamento** al **Impossibile**. Questa azione impedisce la distribuzione futura dell'aggiornamento per i dispositivi con questo asset.


## <a name="see-also"></a>Vedere anche

- [Valutazione della compatibilità nel Desktop Analitica](/sccm/desktop-analytics/compat-assessment)  

- [Come distribuire nell'ambiente di produzione con Desktop Analitica](/sccm/desktop-analytics/deploy-prod)  

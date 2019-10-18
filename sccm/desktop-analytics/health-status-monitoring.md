---
title: Monitoraggio dello stato di integrità
titleSuffix: Configuration Manager
description: Informazioni sul funzionamento del monitoraggio dello stato di integrità in desktop Analytics.
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b27238ea4a77879c353a882c860959d028b81adb
ms.sourcegitcommit: b64ed4a10a90b93a5bd5454b6efafda90ad45718
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72384949"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>Monitoraggio dello stato di integrità in analisi desktop

Quando si [distribuisce un aggiornamento nell'](/sccm/desktop-analytics/deploy-prod)ambiente di produzione, usare analisi del desktop per monitorare lo stato di integrità dei dispositivi. Questo articolo illustra in dettaglio il funzionamento del monitoraggio dello stato.

Per altre informazioni su come usare questa funzionalità, vedere [monitorare l'integrità dei dispositivi aggiornati](/sccm/desktop-analytics/deploy-prod#bkmk_monitor).

![Screenshot della pagina Monitoraggio dell'integrità di analisi del desktop](media/monitor-health.png)

> [!NOTE]  
> Desktop Analytics raccoglie solo i dati di integrità dai dispositivi che forniscono i dati di utilizzo che possono usare come denominatore. Ciò significa che non sono inclusi i dispositivi che eseguono Windows 7 e Windows 10 che non sono impostati per condividere i dati di diagnostica a livello avanzato (limitato). Se più del 10% dei dispositivi che eseguono Windows 10 sono impostati in modo da condividere i dati di diagnostica a livelli diversi da Enhanced (Limited), nella pagina **Monitoraggio integrità** viene visualizzato un avviso nell'area banner.  

Per visualizzare altre informazioni su un'app specifica, selezionarla nell'elenco.



## <a name="apps"></a>Applicazioni

![Fattori di stato di integrità per un'app in desktop Analytics](media/monitor-health-status-factors.png)

Desktop Analytics monitora i seguenti fattori di stato di integrità per le app:

- **% Di dispositivi con arresti anomali**: per le ultime due settimane, il numero di dispositivi in cui questa particolare app si è arrestata in modo anomalo diviso per il numero di dispositivi in cui è stata usata l'app. Questa visualizzazione consente di verificare se la stabilità dell'app è aumentata o diminuita nella nuova versione del sistema operativo. Desktop Analytics calcola questa percentuale per i set seguenti:  

    - **Dopo l'aggiornamento**: dispositivi aggiornati alla versione del sistema operativo di destinazione specificata nel piano di distribuzione. Per ridurre il numero di asset con dati insufficienti, desktop Analytics raccoglie i dati per tutti i dispositivi aggiornati. Questo set include i dispositivi non inclusi nel piano di distribuzione.  

    - **Prima dell'aggiornamento**: i dispositivi che si trovano in una versione del sistema operativo precedente a quanto specificato nel piano di distribuzione. Questo elenco non include i dispositivi che eseguono Windows 7.  

    - Media **commerciale**: percentuale di arresti anomali media (media) in tutti i dispositivi commerciali. Questa media viene calcolata in *tutte* le versioni dell'app. Se la versione Mostra una percentuale di arresti anomali superiore alla media commerciale, potrebbe essere disponibile una versione più stabile.  

- **% Sessioni con arresti anomali**: simile alla precedente, ma conta la percentuale di sessioni con arresti anomali nelle ultime due settimane.  

Per determinare lo stato di integrità di un'app, desktop Analytics richiede dati da almeno 20 dispositivi. In caso contrario, segnala **dati insufficienti** per l'app. Il servizio calcola lo stato di integrità in base alla *frequenza di arresto anomalo della sessione* da questi dispositivi. La frequenza di arresto anomalo del dispositivo viene fornita solo a livello di informazioni. Non viene usato nel calcolo dello stato di integrità.

Nella parte inferiore della pagina dei dettagli dell'app, le tre schede seguenti possono essere utili per la risoluzione dei problemi:

- **Altre versioni**: un elenco di versioni alternative di questa app. Per ogni versione, Mostra le modifiche relative alle frequenze di arresto anomalo all'interno dell'organizzazione e alla media commerciale. Se si trova una versione più recente dell'app con una frequenza di arresto anomalo inferiore, potrebbe essere utile aggiornare l'app.  

    Indica inoltre se la versione dispone di un segnale **pronto per Windows** . Per ulteriori informazioni, vedere [Compatibility assessment](compat-assessment.md#driver-risk-assessment).  

- **Problemi principali**: un elenco degli ID di errore più frequenti in base al numero di istanze. Un ID di errore identifica la traccia dello stack associata all'arresto anomalo. È possibile usare questo ID quando si chiama il fornitore dell'app per il supporto.  

- **Arresti anomali recenti**: un elenco di dispositivi in cui l'app si è arrestata di recente. È possibile filtrare in base all'ID errore e ad altri criteri. Usare queste informazioni per risolvere il problema raccogliendo i log o provando correzioni su dispositivi specifici prima di provare una distribuzione più ampia.  

Se si rileva una grave regressione di integrità che non è possibile correggere, modificare la decisione di **aggiornamento** dell'app in **non è possibile**. Questa azione impedisce la distribuzione futura dell'aggiornamento ai dispositivi con questo asset.


## <a name="see-also"></a>Vedere anche

- [Valutazione della compatibilità in desktop Analytics](/sccm/desktop-analytics/compat-assessment)  

- [Come eseguire la distribuzione nell'ambiente di produzione con analisi desktop](/sccm/desktop-analytics/deploy-prod)  

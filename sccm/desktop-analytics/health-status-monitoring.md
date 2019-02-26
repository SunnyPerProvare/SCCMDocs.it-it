---
title: Monitoraggio dello stato di integrità
titleSuffix: Configuration Manager
description: Informazioni sull'uso di monitoraggio dello stato di integrità in Desktop Analitica.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 343dbe2a-597c-4719-b7ac-45b1f39b49ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 834b7d30aa5331ae73125e1cdfc3c9c7095d58b7
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755465"
---
# <a name="health-status-monitoring-in-desktop-analytics"></a>Stato di integrità monitoraggio in Desktop Analitica

Come si [distribuire un aggiornamento nell'ambiente di produzione](/sccm/desktop-analytics/deploy-prod), utilizzare Desktop Analitica per monitorare lo stato di integrità dei dispositivi. Questo articolo illustra in dettaglio come funziona il monitoraggio dell'integrità.

Per altre informazioni su come usare questa funzionalità, vedere [monitorare l'integrità dei dispositivi aggiornati](/sccm/desktop-analytics/deploy-prod#bkmk_monitor).

![Screenshot della pagina di monitoraggio dell'integrità di Analitica Desktop](media/monitor-health.png)

> [!NOTE]  
> Desktop Analitica raccoglie solo i dati di integrità da dispositivi che forniscono i dati di utilizzo che può essere usato come denominatore. Ciò significa che non include i dispositivi che eseguono Windows 7 e Windows 10 che non sono impostati per condividere i dati di diagnostica a livello di Enhanced (Limited). Se più del 10% di dispositivi che eseguono Windows 10 sono impostate per condividere i dati di diagnostica a livelli diversi dal Enhanced (Limited), il **monitorare l'integrità** pagina viene visualizzato un avviso nell'area dell'intestazione.  

Per visualizzare ulteriori informazioni su un'app specifica, il componente aggiuntivo o advisory (macro), selezionarla nell'elenco. 



## <a name="apps-and-office-apps"></a>Le App e le app di Office

![Fattori di stato di integrità per un'app in Desktop Analitica](media/monitor-health-status-factors.png)

Analitica desktop consente di monitorare i seguenti fattori lo stato di integrità per le App e le app di Office:

- **Percentuale di dispositivi con arresti anomali del sistema**: Per le ultime due settimane, il numero di dispositivi in cui questa app specifica è arrestato in modo anomalo diviso per il numero di dispositivi in cui è stato usato l'app. In questa vista consente di verificare se la stabilità dell'app è aumentato o diminuito sulla nuova versione del sistema operativo. Analitica desktop consente di calcolare tale percentuale per i set seguenti:  

    - **Dopo l'aggiornamento**: Dispositivi che hanno aggiornato alla versione del sistema operativo di destinazione specificata del piano di distribuzione. Per ridurre il numero degli asset con dati sufficienti, Analitica Desktop raccoglie i dati per tutti i dispositivi aggiornati. Questo set include i dispositivi non nel piano di distribuzione.  

    - **Prima dell'aggiornamento**: Dispositivi che usano una versione del sistema operativo precedente a quello specificato nel piano di distribuzione. Questo elenco non include i dispositivi che eseguono Windows 7.   

    - **Media commerciale**: La media (avg) degli arresti anomali di frequenza tra tutti i dispositivi commerciali. Tale Media viene calcolata nel *tutti* versioni dell'app. Se la versione indica una frequenza di arresto anomalo del sistema di sopra della media commerciale, potrebbe esserci una versione più stabile disponibile.  

- **% Sessioni con gli arresti anomali**: Simile al precedente, ma i conteggi la percentuale di sessioni con gli arresti anomali nelle ultime due settimane.  

Per determinare lo stato di integrità di un'app, Analitica Desktop richiede i dati dai dispositivi almeno 20. In caso contrario segnala **dati insufficienti** per l'app. Il servizio calcola lo stato di integrità in base il *percentuale di arresti anomali sessione* da questi dispositivi. La frequenza di arresto anomalo del sistema del dispositivo viene fornita solo a scopo informativo. Può non viene utilizzato nel calcolo dello stato di integrità.

Nella parte inferiore della pagina di dettagli dell'app, le tre schede seguenti consentono di risolvere i problemi:

- **Altre versioni**: Elenco di versioni alternative di questa app. Per ogni versione, Mostra le modifiche relative alle tariffe di arresto anomalo del sistema all'interno dell'organizzazione e la media commerciale. Se si trova una versione successiva dell'app con una frequenza inferiore di arresto anomalo del sistema, l'aggiornamento dell'app possono essere utili.  

    Indica inoltre se la versione ha una **pronto per Windows** segnale. Per altre informazioni, vedere [rischi di compatibilità per le app di Windows](/sccm/desktop-analytics/compat-risk#risk-assessment-engine).  

- **Problemi principali**: Elenco di ID errore più frequente dal numero di istanze. L'analisi dello stack associato con l'arresto anomalo è identificata da un ID di errore. Quando si chiama il fornitore dell'app per il supporto, è possibile usare questo ID.  

- **Arresti anomali del sistema recenti**:  Un elenco di dispositivi in cui l'app recente arrestato in modo anomalo. È possibile filtrare per ID di errore e ad altri criteri. Usare queste informazioni per risolvere il problema per la raccolta dei log o sta tentando di correzioni in dispositivi specifici prima di provare una distribuzione più ampia.  

Se si trova una regressione tramite integrità grave che non si riesce a risolvere, modificare l'app **decisione di aggiornamento** al **Impossibile**. Questa azione impedisce la distribuzione futura dell'aggiornamento per i dispositivi con questo asset.



## <a name="office-add-ins"></a>Componenti aggiuntivi di Office

![Screenshot dei fattori di stato di integrità per un componente aggiuntivo di Office](media/office-add-in-health-status-factors.png)

Analitica desktop consente di monitorare i seguenti fattori lo stato di integrità per i componenti aggiuntivi di Office:

- **Percentuale di dispositivi con eventi imprevisti**: Un evento imprevisto è qualcosa che impedisce che un componente aggiuntivo funziona correttamente. Ad esempio, non riesce a caricare o smette di rispondere. In questa sezione viene illustrato nelle ultime due settimane il numero di dispositivi in cui il componente aggiuntivo selezionato ha un evento imprevisto diviso per il numero di dispositivi in cui è installato il componente aggiuntivo. Analitica desktop consente di calcolare tale percentuale per i set seguenti:  

    - **Dopo l'aggiornamento**: Dispositivi che hanno aggiornato alla versione di Office di destinazione specificata del piano di distribuzione. Per ridurre il numero degli asset con dati sufficienti, Analitica Desktop raccoglie i dati per tutti i dispositivi aggiornati. Questo set include i dispositivi non nel piano di distribuzione.  

    - **Prima dell'aggiornamento**: Dispositivi che eseguono qualsiasi versione di Office meno recenti rispetto alla versione che la distribuzione del pianificazione di destinazioni. <!-- This does not include {include min version of Office}  --> Per valutare l'integrità del componente aggiuntivo, confrontare questa metrica per il **dopo l'aggiornamento** percentuale.  

    - **Media commerciale**: La frequenza degli eventi imprevisti Media (avg) in tutti i dispositivi commerciali che usano la stessa versione del componente aggiuntivo con la stessa versione di Office. Usare questa velocità da confrontare con i dispositivi nell'organizzazione. Questa versione del componente aggiuntivo in caso di una maggiore velocità rispetto alla media commerciale di eventi imprevisti, è possibile alcuni fattori ambientali aggiunta come contributo per gli eventi imprevisti.  

- **% Sessioni con gli eventi imprevisti**: Simile al precedente, ma i conteggi la percentuale di sessioni con gli arresti anomali nelle ultime due settimane.  

Per determinare lo stato di integrità dei componenti aggiuntivi, Analitica Desktop richiede almeno tre dispositivi per la frequenza degli eventi imprevisti di dispositivo e almeno 10 sessioni per la frequenza degli eventi imprevisti di sessione. Per entrambe le frequenze, confronta i valori per determinare se è presente una regressione precedenti e successivi. Nessuna regressione è considerato verso gli obiettivi. 

Desktop Analitica calcola lo stato di integrità complessivo del componente aggiuntivo di Office basato su una combinazione di dispositivi e sessione frequenze degli eventi imprevisti utilizzando la matrice seguente:

|  | Dati insufficienti per arresti anomali del dispositivo  | Metriche di arresto anomalo del sistema di dispositivo integro | Regressione in metriche arresto anomalo del sistema del dispositivo |
|----------------|---------------------|-----------------------|------------------------|
| **Dati insufficienti per le sessioni con gli eventi imprevisti**| Dati insufficienti| Obiettivi di riunione | Dati insufficienti |
| **Integro metriche per le sessioni con gli eventi imprevisti** | Obiettivi di riunione | Obiettivi di riunione | Obiettivi di riunione |
| **Regressione in metriche per le sessioni con gli eventi imprevisti** | Dati insufficienti | Obiettivi di riunione | Attenzione necessita |


La pagina di dettagli di componente aggiuntivo di Office include anche i dettagli seguenti per risolvere i problemi: 

- **Interventi recenti**: Un elenco dei dispositivi in cui un componente aggiuntivo di recente evento imprevisto. Usare questo elenco per risolvere il problema per la raccolta dei log o sta tentando di correzioni in tali dispositivi specifici prima di provare una più ampia implementazione.  



## <a name="office-macros"></a>Macro di Office

![Screenshot dei fattori di stato di integrità per una macro di Office advisory](media/office-macros-health-status-factors.png)

Desktop Analitica segnala lo stato di integrità *gli avvisi di macro*. Gli avvisi di macro rappresentano potenziali problemi rilevati nei file di Office che contiene le macro. Questi problemi sono specifici di un'applicazione di Office. Ad esempio, Word, Excel, PowerPoint o Visio. 

Analitica desktop consente di monitorare i seguenti fattori lo stato di integrità per le macro di Office:

- **Percentuale di dispositivi con errore di compilazione**: Per le ultime due settimane, il numero dei dispositivi nei quali gli errori correlati alla consulenza si è verificato durante l'abilitazione della macro diviso per il numero di dispositivi in cui è stato rilevato l'avviso. Analitica desktop consente di calcolare tale percentuale per i set seguenti: 

    - **Dopo l'aggiornamento**: I dispositivi in cui la versione di Office è lo stesso come destinazione del piano di distribuzione  

    - **Prima dell'aggiornamento**: I dispositivi che eseguono qualsiasi versione di Office meno recenti rispetto a destinazione del piano di distribuzione  

    - **Media commerciale**: La media (avg) di tutti i dispositivi commerciali che eseguono la stessa versione di Office come destinazione del piano di distribuzione  

- **Percentuale di dispositivi con errore di runtime** simile al precedente, ma per le ultime due settimane, i dispositivi in cui gli errori riguardanti la consulenza si è verificato durante l'esecuzione di macro diviso per il numero di dispositivi in cui è stato rilevato l'avviso.  

La pagina dei dettagli le macro di Office include anche i dettagli seguenti per risolvere i problemi: 

- **Interventi recenti**: Un elenco di dispositivi su quale macro si è recentemente verificato gli errori di compilazione e runtime. Usare questo elenco per risolvere il problema per la raccolta dei log o sta tentando di correzioni in tali dispositivi specifici prima di provare una più ampia implementazione.



## <a name="see-also"></a>Vedere anche

- [Rischi di compatibilità per le app di Windows nel Desktop Analitica](/sccm/desktop-analytics/compat-risk)  

- [Come distribuire nell'ambiente di produzione con Desktop Analitica](/sccm/desktop-analytics/deploy-prod)  

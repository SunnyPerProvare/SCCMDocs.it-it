---
title: Come distribuire nell'ambiente di produzione
titleSuffix: Configuration Manager
description: Informazioni di Guida per la distribuzione in un gruppo di produzione Analitica Desktop.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d1a71558c6b87c79c6d4667746e081c6db85ce18
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159150"
---
# <a name="how-to-deploy-to-production-with-desktop-analytics"></a>Come distribuire nell'ambiente di produzione con Desktop Analitica

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Dopo aver [distribuito per contenuto pilota](/sccm/desktop-analytics/deploy-pilot) ed esaminare lo stato degli asset, si è pronti per aggiornare il resto dell'ambiente di produzione.

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

Esistono tre parti principali per eseguire la distribuzione degli aggiornamenti ai dispositivi di produzione:

1. [Esaminare gli asset che richiedono una decisione di aggiornamento](#bkmk_review): Per rendere i dispositivi pronti per la distribuzione di produzione, gli asset devono avere le decisioni relative all'aggiornamento impostata su **pronti** oppure **pronto, le correzioni necessarie**.  

2. [Distribuire ai dispositivi che sono pronti](#bkmk_deploy): Usare Configuration Manager per aggiornare i dispositivi che sono pronti. Analitica desktop fornisce l'elenco dei dispositivi pronti per la distribuzione di produzione e i report per monitorare la riuscita della distribuzione.  

3. [Monitorare l'integrità dei dispositivi aggiornati](#bkmk_monitor): Durante l'avanzamento della distribuzione di aggiornamento, monitorare l'integrità delle risorse più importanti. Se alcune richiedono attenzione, identificare e risolvere tali problemi. Se si decide di non possono essere risolto i problemi, arrestare la distribuzione sui dispositivi interessati impostando le decisioni relative all'aggiornamento **non è possibile**.  

> [!NOTE]  
> Quando si certi che il successo della distribuzione pilota, avviare la distribuzione di produzione in qualsiasi momento. Non è necessario che tutti i dispositivi pilota raggiungano prima di tutto lo stato "completato".  



## <a name="bkmk_review"></a> Esaminare gli asset che richiedono una decisione di aggiornamento

Analitica desktop consente di eseguire in modo semplificato il processo di analisi delle risorse per la distribuzione di produzione. Nel portale di Azure, passare a **piani di distribuzione**, selezionare un piano di distribuzione e quindi selezionare **preparare l'ambiente di produzione** nel menu a sinistra.

![Visualizzazione di screenshot di produzione di preparare in Desktop Analitica](media/prepare-production.png)

Esaminare lo stato delle tue app. Usare queste informazioni per impostare la decisione di aggiornamento per ognuno di tali asset.

Usare le schede per esaminare lo stato delle app. In ogni visualizzazione a schede, è possibile filtrare i risultati per visualizzare i dispositivi che sono in modo corretto per l'aggiornamento, necessitano di attenzione, i dispositivi con risultati misti e tali dispositivi in uno stato indeterminato.

Selezionare **riunione obiettivi** per filtrare la visualizzazione agli asset che sono probabilmente pronti per la distribuzione di produzione in base ai criteri seguenti:

- Dei rischi: valutazione una pre-aggiornamento di rischi noti per l'aggiornamento dei dispositivi che hanno questo asset installato  

- Lo stato di integrità: una valutazione dopo l'aggiornamento dei dispositivi in altre distribuzioni e se si sono verificati problemi dopo l'aggiornamento è stato installato. Per altre informazioni sull'integrità, vedere [monitorare l'integrità dei dispositivi aggiornati](#bkmk_monitor).  

Per approvare un asset per l'aggiornamento, selezionare il nome nell'elenco e quindi selezionare una delle opzioni seguenti dal **decisione di aggiornamento** elenco:

- Revisione in corso
- Pronto
- Pronto (con monitoraggio e aggiornamento)
- Non è possibile
- Verifica non effettuata

Per impostare questo valore per più App in una sola volta, usare la prima colonna da **selezionare questo elemento**, quindi scegliere **decisioni di aggiornamento impostato**.

![Impostare l'opzione di decisioni di aggiornamento in più App](media/prep-prod-set-upgrade-decision.png)

Selezionare **alcun dato** agli asset di visualizzazione che non è stato classificato. Questi asset vengono in genere gli asset che non sono sufficiente la copertura di Analitica Desktop eseguire un'analisi dello stato di integrità o rischio. Per migliorare il code coverage, aggiungere altri dispositivi con questi asset per il contenuto pilota o chiedere agli utenti pilota per provare queste risorse.

Potrebbero essere presenti anche gli asset nel **attenzione necessita** o **risultati misto** dello stato. Questi asset potrebbero richiedere un'ulteriore analisi prima di apportare una decisione di aggiornamento per loro.

Esaminare tutte le app. Una volta che un determinato dispositivo ha una decisione di aggiornamento positiva per tutti gli asset, quindi il relativo stato viene modificato in "pronto per la produzione". Visualizzare il numero corrente nella pagina principale per il piano di distribuzione selezionando il terzo passaggio di distribuzione, **Distribuisci**.


## <a name="bkmk_deploy"></a> Distribuire ai dispositivi che sono pronti

Configuration Manager usa i dati di Analitica Desktop per creare una raccolta per la distribuzione di produzione. Non distribuire la sequenza di attività usando una distribuzione tradizionale. Usare la procedura seguente per creare una distribuzione integrata Analitica Desktop:

Se è stato eseguito il processo consigliato per [distribuire ai dispositivi pilota](/sccm/desktop-analytics/deploy-pilot#deploy-to-pilot-devices), la distribuzione di Configuration Manager in più fasi è pronta. Come contrassegnare gli asset come *pronti*, Analitica Desktop Sincronizza automaticamente i dispositivi in Configuration Manager. Questi dispositivi vengono quindi aggiunti alla raccolta di produzione. Quando si sposta la distribuzione in più fasi per la seconda fase, questi dispositivi di produzione ricevono la distribuzione dell'aggiornamento.

Se è configurata la distribuzione in più fasi **inizia manualmente la seconda fase della distribuzione**, è necessario spostare manualmente alla fase successiva. Per altre informazioni, vedere questo articolo: [Gestire e monitorare le distribuzioni in più fasi](/sccm/osd/deploy-use/manage-monitor-phased-deployments#bkmk_move).

Se è stata creata una distribuzione singola Analitica Desktop integrate nella raccolta pilota, quindi è necessario ripetere la procedura per distribuire nella raccolta di produzione.


### <a name="address-deployment-alerts"></a>Risolvere gli avvisi di distribuzione

Come con la distribuzione pilota, Analitica Desktop suggerisce di eventuali problemi che richiedono attenzione durante la distribuzione di produzione. Nel Desktop Analitica, passare al piano di distribuzione e selezionare **lo stato di distribuzione** nel menu a sinistra. La visualizzazione dello stato di distribuzione sono elencati i dispositivi nelle categorie seguenti:  

- Non avviato
- In corso
- Operazione completata
- Richiede attenzione - dispositivi (ordinati in base al nome di dispositivo)
- Richiede attenzione - i problemi (ordinati in base al tipo di problema)

![Ambiente di produzione di schermata del Desktop Analitica lo stato di distribuzione](media/prod-deployment-status.png)


## <a name="bkmk_monitor"></a> Monitorare l'integrità dei dispositivi aggiornati

Il **preparare l'ambiente di produzione** pagina è incentrata per aiutarti a occorre aggiornare decisioni per gli asset. Tale pagina per impostazione predefinita vengono visualizzati solo gli asset che non sono ancora nel **pronti** dello stato. Il **monitorare l'integrità** pagina vengono visualizzati i problemi di integrità su qualsiasi asset degno di nota, anche tali asset contrassegnati **pronto**. Se rileva i problemi, è possibile risolvere i problemi e correggere il problema o modificare le decisioni relative all'aggiornamento a **non è possibile**. Quando si modificano le decisioni relative all'aggiornamento, questa azione impedisce gli aggiornamenti futuri nei dispositivi con quell'asset.

Filtrare questa pagina per gli asset con gli stati di integrità seguenti:

| Filtro dello stato di integrità | Descrizione |
|----------------------|-------------|
| **Attenzione necessita** | (Filtro predefinito) Desktop Analitica rileva una regressione statisticamente significativa per una metrica di integrità per quell'asset
| **Obiettivi di riunione** | Desktop Analitica non rileva Nessuna regressione nel comportamento |
| **Dati insufficienti** | Desktop Analitica non avere dati sufficienti su questo asset per fornire raccomandazioni |
| **Nessun dato** | Dati sull'utilizzo non è ancora disponibile per questo asset |

Per mostrare una visualizzazione non filtrata di tutti gli asset, selezionare il filtro corrente. Questa azione rimuove il filtro.

> [!NOTE]  
> Per ridurre il numero degli asset con dati sufficienti, Analitica Desktop consente di monitorare gli asset in tutti i dispositivi che hanno eseguito l'aggiornamento alla versione di Windows di destinazione specificata nel piano di distribuzione. Questi dispositivi includono quelli non inclusi nel piano di distribuzione specifico.  

L'ordinamento predefinito è per il numero di dispositivi che hanno avuto un evento imprevisto con tali entità, pertanto è possibile visualizzare rapidamente quelle che causano la maggior parte dei problemi. Ad esempio, quando si visualizzano **Apps**, vengono ordinati in base **due settimane di arresto anomalo di dispositivi con app**.

Se si desidera dello stato per tutti gli asset, anche gli asset con dati sufficienti per Analitica Desktop creare inferenze statistiche, procedere come segue:

1. Selezionare l'elenco a discesa nella **i dispositivi con eventi imprevisti nelle ultime due settimane** colonna. Aggiungere un filtro per solo tali asset a cui si sono verificati gli eventi imprevisti in un numero minimo di interessanti dei dispositivi. Ad esempio, mostrare elementi con valori **maggiore** 100.  

2. Selezionare l'elenco a discesa nella **% dispositivi con eventi imprevisti nelle ultime due settimane** colonna e selezionare questa opzione per ordinare **Descending**.  

    La visualizzazione risultante mostra gli asset con la tariffa più alta di evento imprevisto con un numero minimo di eventi imprevisti.  

3. Selezionare un asset per ottenere altri dettagli o modificare le decisioni relative all'aggiornamento.  

Per altre informazioni, vedere [il monitoraggio dello stato di integrità](/sccm/desktop-analytics/health-status-monitoring).

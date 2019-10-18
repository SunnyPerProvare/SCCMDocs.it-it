---
title: Come eseguire la distribuzione nell'ambiente di produzione
titleSuffix: Configuration Manager
description: Guida alle procedure per la distribuzione in un gruppo di produzione di analisi desktop.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b9030ad805853d1dd607607d80dca2b606e8160c
ms.sourcegitcommit: b64ed4a10a90b93a5bd5454b6efafda90ad45718
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72386056"
---
# <a name="how-to-deploy-to-production-with-desktop-analytics"></a>Come eseguire la distribuzione nell'ambiente di produzione con analisi desktop

Dopo aver [distribuito al programma pilota](/sccm/desktop-analytics/deploy-pilot) e aver esaminato lo stato degli asset, si è pronti per aggiornare il resto dell'ambiente di produzione.

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]

Sono disponibili tre componenti principali per eseguire la distribuzione degli aggiornamenti nei dispositivi di produzione:

1. [Esaminare gli asset che necessitano di una decisione di aggiornamento](#bkmk_review): per rendere i dispositivi pronti per la distribuzione di produzione, è necessario che le relative risorse di aggiornamento siano impostate su **pronto** o pronto, per le **correzioni necessarie**.  

2. [Distribuisci nei dispositivi pronti](#bkmk_deploy): USA Configuration Manager per aggiornare i dispositivi pronti. Desktop Analytics fornisce l'elenco dei dispositivi pronti per la distribuzione di produzione e i report per il monitoraggio del successo della distribuzione.  

3. [Monitorare l'integrità dei dispositivi aggiornati](#bkmk_monitor): con l'avanzamento della distribuzione degli aggiornamenti, monitorare l'integrità delle risorse importanti. Se è necessario prestare attenzione, risolvere i problemi e risolverli. Se si decide che non è possibile risolvere i problemi, arrestare la distribuzione nei dispositivi interessati impostando la relativa decisione di aggiornamento su **non riuscito**.  

> [!NOTE]  
> Quando si è sicuri del successo della distribuzione pilota, avviare la distribuzione di produzione in qualsiasi momento. Non è necessario che tutti i dispositivi pilota raggiungano prima lo stato "completato".  



## <a name="bkmk_review"></a>Esaminare gli asset che necessitano di una decisione di aggiornamento

Desktop Analytics Guida il processo di revisione degli asset per la distribuzione di produzione. Nella portale di Azure passare a piani di **distribuzione**, selezionare un piano di distribuzione e quindi selezionare **prepara produzione** nel menu a sinistra.

![Screenshot di preparare la visualizzazione di produzione in analisi desktop](media/prepare-production.png)

Esaminare lo stato delle app. Usare queste informazioni per impostare la decisione di aggiornamento per ognuno di tali asset.

Usare ognuna delle schede per esaminare lo stato delle app. In ogni visualizzazione a schede è possibile filtrare i risultati per visualizzare i dispositivi che si trovano in una traccia per l'aggiornamento, richiedono attenzione, dispositivi con risultati misti e tali dispositivi in uno stato non determinato.

Selezionare **obiettivi della riunione** per filtrare la visualizzazione in base alle risorse che sono probabilmente pronte per la distribuzione di produzione in base ai criteri seguenti:

- Rischio: valutazione pre-aggiornamento dei rischi noti per l'aggiornamento di dispositivi in cui è installato questo asset  

- Stato di integrità: una valutazione dopo l'aggiornamento dei dispositivi in altre distribuzioni e se hanno riscontrato problemi dopo l'installazione dell'aggiornamento. Per ulteriori informazioni sull'integrità, vedere [monitorare l'integrità dei dispositivi aggiornati](#bkmk_monitor).  

Per approvare un asset per l'aggiornamento, selezionare il nome nell'elenco e quindi selezionare una delle opzioni seguenti dall'elenco di **decisioni di aggiornamento** :

- Revisione in corso
- Pronto
- Pronto (con monitoraggio e aggiornamento)
- Impossibile
- Non verificato

Per impostare questo valore per più app contemporaneamente, usare la prima colonna per **selezionare questo elemento**, quindi scegliere **imposta decisione di aggiornamento**.

![Impostare l'opzione di decisione di aggiornamento in più app](media/prep-prod-set-upgrade-decision.png)

Selezionare **Nessun dato** per visualizzare gli asset che non possono essere classificati. Si tratta in genere di asset che non dispongono di una copertura sufficiente per l'analisi del desktop per eseguire un'analisi dello stato di rischio o integrità. Per migliorare la copertura, aggiungere altri dispositivi con queste risorse al progetto pilota o richiedere agli utenti pilota di provare questi asset.

Potrebbero essere presenti anche risorse nello stato di **attenzione necessario** o **dei risultati misti** . Queste risorse possono richiedere una revisione aggiuntiva prima di prendere una decisione relativa all'aggiornamento.

Esaminare tutte le app. Quando un determinato dispositivo ha una decisione positiva sull'aggiornamento per tutti gli asset, lo stato diventa "pronto per la produzione". Vedere il conteggio corrente nella pagina principale per il piano di distribuzione selezionando il terzo passaggio di distribuzione, **deploy**.


## <a name="bkmk_deploy"></a>Distribuisci nei dispositivi pronti

Configuration Manager usa i dati di analisi del desktop per creare una raccolta per la distribuzione di produzione. Non distribuire la sequenza di attività usando una distribuzione tradizionale. Usare la procedura seguente per creare una distribuzione integrata di analisi del desktop:

Se è stata seguita la procedura consigliata per la [distribuzione nei dispositivi pilota](/sccm/desktop-analytics/deploy-pilot#deploy-to-pilot-devices), la Configuration Manager distribuzione in più fasi è pronta. Quando si contrassegnano gli asset come *pronti*, desktop Analytics sincronizza automaticamente tali dispositivi con Configuration Manager. Questi dispositivi vengono quindi aggiunti alla raccolta di produzione. Quando la distribuzione in più fasi passa alla seconda fase, questi dispositivi di produzione ricevono la distribuzione dell'aggiornamento.

Se la distribuzione in più fasi è stata configurata per **iniziare manualmente la seconda fase della distribuzione**, è necessario spostarla manualmente nella fase successiva. Per altre informazioni, vedere questo articolo: [Gestire e monitorare le distribuzioni in più fasi](/sccm/osd/deploy-use/manage-monitor-phased-deployments#bkmk_move).

Se è stata creata una distribuzione singola integrata di analisi del desktop per la raccolta pilota, è necessario ripetere il processo per la distribuzione nella raccolta di produzione.


### <a name="address-deployment-alerts"></a>Avvisi di distribuzione indirizzi

Come per la distribuzione pilota, desktop Analytics consiglia di individuare eventuali problemi che richiedono attenzione durante la distribuzione di produzione. In desktop Analytics andare al piano di distribuzione e selezionare stato della **distribuzione** nel menu a sinistra. La visualizzazione stato distribuzione Elenca i dispositivi nelle categorie seguenti:  

- Non avviato
- In corso
- Completato
- Richiesta attenzione-dispositivi (ordinati per nome dispositivo)
- Richiesta attenzione-problemi (ordinati per tipo di problema)

![Screenshot dello stato della distribuzione di produzione di analisi desktop](media/prod-deployment-status.png)


## <a name="bkmk_monitor"></a>Monitorare l'integrità dei dispositivi aggiornati

La pagina **prepara produzione** è incentrata sull'assistenza per prendere decisioni di aggiornamento per gli asset. Per impostazione predefinita, questa pagina Mostra solo gli asset che non sono ancora nello stato **pronto** . La pagina **Monitoraggio integrità** Mostra i problemi di integrità di qualsiasi asset degno di nota, anche quelli contrassegnati come **pronti**. Se vengono individuati problemi, è possibile risolvere il problema oppure modificare la decisione di aggiornamento in **non**è possibile. Quando si modifica la decisione di aggiornamento, questa azione impedisce gli aggiornamenti futuri nei dispositivi con tale asset.

Filtrare questa pagina in base alle risorse con gli Stati di integrità seguenti:

| Filtro stato di integrità | Descrizione |
|----------------------|-------------|
| **Attenzione necessaria** | (Filtro predefinito) Desktop Analytics rileva una regressione statisticamente significativa a una metrica di integrità per l'asset
| **Obiettivi della riunione** | Desktop Analytics non rileva alcuna regressione nel comportamento |
| **Dati insufficienti** | Desktop Analytics non dispone di dati sufficienti su questo asset per apportare raccomandazioni |
| **Nessun dato** | Nessun dato di utilizzo ancora disponibile per questo asset |

Per visualizzare una visualizzazione non filtrata di tutti gli asset, selezionare il filtro corrente. Questa azione rimuove il filtro.

> [!NOTE]  
> Per ridurre il numero di asset con dati insufficienti, desktop Analytics monitora gli asset in tutti i dispositivi che hanno eseguito l'aggiornamento alla versione di Windows di destinazione specificata nel piano di distribuzione. Questi dispositivi includono quelli non inclusi nel piano di distribuzione specifico.  

L'ordinamento predefinito è determinato dal numero di dispositivi in cui si è verificato un evento imprevisto con quel particolare asset, quindi è possibile individuare rapidamente quali sono i problemi che causano la maggior parte dei problemi. Ad esempio, quando si visualizzano le **app**, Ordina per **dispositivi con arresti anomali delle app ultime due settimane**.

Se si vuole esaminare lo stato di integrità di tutti gli asset, anche quelli con dati insufficienti per l'analisi del desktop per eseguire inferenze statistiche, usare il processo seguente:

1. Selezionare l'elenco a discesa dei **dispositivi con eventi imprevisti nella colonna ultime due settimane** . Aggiungere un filtro solo ai cespiti in cui si sono verificati eventi imprevisti in un numero minimo di dispositivi. Ad esempio, Mostra gli elementi con valori **maggiori di** 100.  

2. Selezionare l'elenco a discesa nella colonna **% dispositivi con eventi imprevisti nelle ultime due settimane** e selezionare per eseguire l'ordinamento in **ordine decrescente**.  

    La visualizzazione risultante Mostra gli asset con la massima frequenza di evento imprevisto a un numero minimo di eventi imprevisti.  

3. Selezionare un asset per ottenere altri dettagli o modificare la decisione di aggiornamento.  

Per ulteriori informazioni, vedere [monitoraggio dello stato di integrità](/sccm/desktop-analytics/health-status-monitoring).

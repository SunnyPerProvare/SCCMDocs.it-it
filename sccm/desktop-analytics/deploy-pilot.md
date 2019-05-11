---
title: Come distribuire per contenuto pilota
titleSuffix: Configuration Manager
description: Informazioni di Guida per la distribuzione in un gruppo pilota Analitica Desktop.
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: d11e5eeb5e7a183c6b409fdbe58034ebe181898f
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65083161"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>Modalità di distribuzione per eseguire progetti pilota con Desktop Analitica

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Uno dei vantaggi di Analitica Desktop è di identificare il set più piccolo di dispositivi che forniscono la copertura più ampia di fattori. Ma illustra i fattori più importanti per un progetto pilota di Windows gli aggiornamenti. Assicurandosi che il progetto pilota è più riuscito consente di spostare in modo più rapido e sicuro per ampie distribuzioni nell'ambiente di produzione.  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]



## <a name="address-issues"></a>Risolvere i problemi

Usare il portale di Analitica Desktop per esaminare eventuali problemi segnalati con le risorse che potrebbero bloccare la distribuzione. Quindi approvare, rifiutare o modificare la correzione suggerita. Tutti gli elementi devono essere contrassegnati **pronti** oppure **pronto (con monitoraggio e aggiornamento)** prima dell'avvio della distribuzione pilota.

1. Passare al portale di Analitica di Desktop e selezionare **piani di distribuzione** nel gruppo di gestione.  

2. Aprire un piano di distribuzione selezionando il relativo nome.  

3. Selezionare **pilota Prepare** nel gruppo di preparazione del menu di piano di distribuzione.  

4. Nel **app** scheda, esaminare le app che richiedono l'input dell'utente.  

5. Per ogni app, selezionare il nome dell'app. Nel riquadro delle informazioni, esaminare le indicazioni e selezionare la decisione di aggiornamento. Se si sceglie **non rivisti** oppure **Impossibile**, Analitica Desktop non può includere i dispositivi con l'app nella distribuzione pilota. Se si sceglie **pronto (con monitoraggio e aggiornamento)**, utilizzare il **note correzione** per acquisire le azioni da intraprendere per risolvere un problema, ad esempio *reinstallare* o *trovare il versione consigliata del produttore*.

6. Ripetere questa revisione per gli altri asset.  



## <a name="create-software"></a>Creazione del software

Prima di poter distribuire Windows, prima di tutto creare gli oggetti di software in Configuration Manager. Per altre informazioni, vedere [sequenza di attività di aggiornamento sul posto di Windows 10](https://docs.microsoft.com/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).



## <a name="deploy-to-pilot-devices"></a>Distribuzione pilota nei dispositivi

Configuration Manager usa i dati di Analitica Desktop per creare una raccolta per la distribuzione pilota. Non distribuire la sequenza di attività usando una distribuzione tradizionale. Usare la procedura seguente per creare una distribuzione integrata Analitica Desktop:

1. Nella console di Configuration Manager passare ad il **raccolta Software**, espandere **Desktop Analitica Servicing**e selezionare il **piani di distribuzione** nodo.  

2. Selezionare il piano di distribuzione e quindi selezionare **dettagli piano di distribuzione** nella barra multifunzione.  

3. Nel **lo stato di avviare un programma pilota** riquadro, seleziona **sequenza di attività** nell'elenco a discesa.  

    > [!Note]  
    > Non usare la **applicazione** opzione. È riservato per le funzionalità future.

    Selezionare **distribuire**. Questa azione avvia la distribuzione guidata del Software per il tipo di oggetto selezionato.

    > [!Note]  
    > Con l'integrazione Analitica Desktop, Configuration Manager crea automaticamente una raccolta per il piano di distribuzione pilota. Possono volerci fino a 10 minuti per questa raccolta per la sincronizzazione prima di usarlo.<!-- 3887891 -->
    >
    > Questa raccolta è riservata per i dispositivi piano di distribuzione Desktop Analitica. Non sono supportate le modifiche manuali a questa raccolta.<!-- 3866460, SCCMDocs-pr 3544 -->  

Per altre informazioni, vedere [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence).



## <a name="monitor"></a>Monitoraggio

### <a name="configuration-manager-console"></a>Console di Configuration Manager

Distribuzione di utilizzare Gestione configurazione monitoraggio lo stesso come qualsiasi altra distribuzione della sequenza di attività. Per altre informazioni, vedere [distribuzioni del sistema operativo monitoraggio](/sccm/osd/deploy-use/monitor-operating-system-deployments).


### <a name="desktop-analytics-portal"></a>Portale Analitica desktop

Usare il portale di Analitica Desktop per visualizzare lo stato di qualsiasi piano di distribuzione. Selezionare il piano di distribuzione e quindi selezionare **Panoramica del piano**.

![Schermata della panoramica del piano di distribuzione in Desktop Analitica](media/deployment-plan-overview.png)

Selezionare il **pilota** riquadro. Riepilogato lo stato corrente della distribuzione pilota. Questo riquadro Visualizza anche i dati per il numero di dispositivi non è stati avviati, in corso, completato, o la restituzione di problemi.

Eventuali dispositivi che segnalano errori o altri problemi sono inoltre elencati nell'area dettaglio programma pilota a destra. Per ottenere i dettagli del problema segnalato, selezionare **revisione**. Questa azione viene modificata la visualizzazione per il **lo stato di distribuzione** pagina

Il **lo stato di distribuzione** pagina vengono elencati i dispositivi nelle categorie seguenti:

- Non avviato
- In corso
- Operazione completata
- Richiede attenzione - i dispositivi
- Richiede attenzione - problemi

Il **necessita di attenzione** categorie visualizzano le stesse informazioni, ma ordinati in modo diverso.

Selezionare un elenco specifico in una visualizzazione per ottenere altri dettagli sul problema rilevato.

Come risolvere questi problemi di distribuzione, il dashboard continua a mostrare lo stato di avanzamento dei dispositivi. Aggiorna dispositivi lo spostamento dalla **necessita di attenzione** al **Completed**.



## <a name="next-steps"></a>Passaggi successivi

Eseguire il progetto pilota per un periodo di tempo per raccogliere dati operativi. Incoraggiare gli utenti dei dispositivi pilota per testare le app.

Quando la distribuzione pilota soddisfa i criteri di successo, passare all'articolo successivo per la distribuzione nell'ambiente di produzione.
> [!div class="nextstepaction"]  
> [Distribuire nell'ambiente di produzione](/sccm/desktop-analytics/deploy-prod)  

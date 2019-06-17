---
title: Come distribuire per contenuto pilota
titleSuffix: Configuration Manager
description: Informazioni di Guida per la distribuzione in un gruppo pilota Analitica Desktop.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: e18e2e43e9bb768f81233fb2d2deda0ae05c1961
ms.sourcegitcommit: d47d2f03482e48d343e2139a341e61022331e6c2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/14/2019
ms.locfileid: "67145830"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>Modalità di distribuzione per eseguire progetti pilota con Desktop Analitica

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Uno dei vantaggi di Analitica Desktop è di identificare il set più piccolo di dispositivi che forniscono la copertura più ampia di fattori. Ma illustra i fattori più importanti per un progetto pilota di Windows gli aggiornamenti. Assicurandosi che il progetto pilota è più riuscito consente di spostare in modo più rapido e sicuro per ampie distribuzioni nell'ambiente di produzione.  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]


## <a name="identify-devices"></a>Identificare i dispositivi

Il primo passaggio consiste nell'identificare i dispositivi da includere nel progetto pilota. Desktop Analitica suggerisce i dispositivi in base i dati segnalati in ed è possibile includere o sostituire i dispositivi in questo elenco.

1. Andare alla [portal Desktop Analitica](https://aka.ms/desktopanalytics)e selezionare Gestisci gruppo **piani di distribuzione**.

1. Selezionare un piano di distribuzione.

1. Nel gruppo di preparazione del menu di piano di distribuzione, selezionare **pilota Identify**.

Si noterà che i dati di Analitica Desktop che mostra il numero di dispositivi che è consigliabile anche per il code coverage migliore. Questo algoritmo è basato principalmente sull'uso delle App critiche e importanti e la varietà di configurazioni hardware.

Eseguire le azioni seguenti per l'elenco di dispositivi aggiuntivi consigliati:

- **Aggiungi tutto al progetto pilota**: Aggiunge tutti i dispositivi consigliati per il gruppo pilota
- **Aggiungere al progetto pilota**: Aggiungere solo singoli dispositivi
- **Sostituire** eventuali dispositivi specifici durante la fase pilota
- **Ricalcolare** al termine delle modifiche

È anche possibile prendere decisioni a livello di sistema sulle quali raccolte di Configuration Manager per includere o escludere da progetti pilota. Nel menu principale di Analitica Desktop, nel gruppo di impostazioni globali, selezionare **pilota globale**.

### <a name="example"></a>Esempio

- Si configura la connessione di Desktop Analitica in Configuration Manager alla destinazione di **tutti i sistemi** raccolta. Questa azione registra tutti i client del servizio.
- È anche possibile configurare raccolte aggiuntive per la sincronizzazione con Analitica Desktop:
    - Tutti i client Windows 10
    - Tutti i dispositivi IT
    - Office CEO
- Nel **pilota globale** impostazioni, si include il **dispositivi IT tutte** raccolte. Si esclude il **CEO office** raccolta.
- Creare un piano di distribuzione e selezionare il **client tutti i dispositivi Windows 10** raccolta.
- I **pilota dispositivi inclusi** sono elencati i set di dispositivi seguenti:
    - Tutti i dispositivi nell'elenco di inclusione pilota globale: **Tutti i dispositivi IT**
    - Raccolte che fanno parte del gruppo di destinazione del piano di distribuzione: **Tutti i client Windows 10**
- Desktop Analitica esclude dal **aggiuntivi consigliati i dispositivi** elencare tutti i dispositivi nel progetto pilota globale *esclusione* elenco: **CEO office**
- Solo le prime due raccolte sono considerate come parte della fase pilota. Dopo gli aggiornamenti ha esito positivo a tali gruppi e gli asset vengono *pronti*, Analitica Desktop consente di sincronizzare i dispositivi nel **office CEO** insieme alla raccolta di produzione di Configuration Manager.


## <a name="address-issues"></a>Risolvere i problemi

Usare il portale di Analitica Desktop per esaminare eventuali problemi segnalati con le risorse che potrebbero bloccare la distribuzione. Quindi approvare, rifiutare o modificare la correzione suggerita. Tutti gli elementi devono essere contrassegnati **pronti** oppure **pronto (con monitoraggio e aggiornamento)** prima dell'avvio della distribuzione pilota.

1. Andare alla [portal Desktop Analitica](https://aka.ms/desktopanalytics)e selezionare Gestisci gruppo **piani di distribuzione**.  

2. Selezionare un piano di distribuzione.  

3. Nel gruppo di preparazione del menu di piano di distribuzione, selezionare **pilota Prepare**.  

4. Nel **app** scheda, esaminare le app che richiedono l'input dell'utente.  

5. Per ogni app, selezionare il nome dell'app. Nel riquadro delle informazioni, esaminare le indicazioni e selezionare la decisione di aggiornamento. Se si sceglie **non rivisti** oppure **Impossibile**, Analitica Desktop non può includere i dispositivi con l'app nella distribuzione pilota. Se si sceglie **pronto (con monitoraggio e aggiornamento)** , utilizzare il **note correzione** per acquisire le azioni da intraprendere per risolvere un problema, ad esempio *reinstallare* o *trovare il versione consigliata del produttore*.

6. Ripetere questa revisione per gli altri asset.  


## <a name="create-software"></a>Creazione del software

Prima di poter distribuire Windows, prima di tutto creare gli oggetti di software in Configuration Manager. Per altre informazioni, vedere [sequenza di attività di aggiornamento sul posto di Windows 10](https://docs.microsoft.com/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).


## <a name="deploy-to-pilot-devices"></a>Distribuzione pilota nei dispositivi

Configuration Manager usa i dati di Analitica Desktop per creare raccolte per le distribuzioni pilota e di produzione. Per assicurarsi che i dispositivi siano integri dopo ogni fase di distribuzione, usare la procedura seguente per creare una distribuzione graduale Analitica Desktop integrata:

1. Nella console di Configuration Manager passare ad il **raccolta Software**, espandere **Desktop Analitica Servicing**e selezionare il **piani di distribuzione** nodo.  

2. Selezionare il piano di distribuzione e quindi selezionare **dettagli piano di distribuzione** nella barra multifunzione.  

3. Selezionare **creare la distribuzione in più fasi** nella barra multifunzione. Questa azione avvia la procedura guidata di creare la distribuzione in più fasi.

    > [!Tip]  
    > Se si desidera creare una distribuzione sequenza di attività classico per solo la raccolta pilota, selezionare **Deploy** nel **pilota stato** riquadro. Questa azione avvia la distribuzione guidata del Software. Per altre informazioni, vedere [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence).  

4. Immettere un nome per la distribuzione e selezionare la sequenza di attività da utilizzare. Usare l'opzione **crea automaticamente una distribuzione predefinita in due fasi**e quindi configurare le raccolte seguenti:  

    - **Prima raccolta**: Individuare e selezionare il **pilota** raccolta per questo piano di distribuzione. La convenzione di denominazione standard per questa raccolta è `<deployment plan name> (Pilot)`.

    - **Seconda raccolta**: Individuare e selezionare il **produzione** raccolta per questo piano di distribuzione. La convenzione di denominazione standard per questa raccolta è `<deployment plan name> (Production)`.

    > [!Note]  
    > Con l'integrazione Analitica Desktop, Configuration Manager crea automaticamente raccolte pilota e di produzione per il piano di distribuzione. Possono volerci fino a 10 minuti per queste raccolte per la sincronizzazione prima di usarli.<!-- 3887891 -->
    >
    > Questi insiemi sono riservati per i dispositivi piano di distribuzione Desktop Analitica. Le modifiche manuali a queste raccolte non sono supportate.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Completare la procedura guidata per configurare la distribuzione in più fasi. Per altre informazioni, vedere [Creare distribuzioni in più fasi](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).

    > [!Note]  
    > Usare l'impostazione predefinita per **inizia automaticamente questa fase dopo un periodo di differimento (in giorni)** . Per la seconda fase avviare devono essere soddisfatti i criteri seguenti:
    >
    > 1. Dispositivi pilota devono eseguire l'aggiornamento e invio back rivisto i dati di diagnostica.
    > 1. La prima fase raggiunge il **percentuale di completamento distribuzione** criteri per l'esito positivo. Si configura questa impostazione nella distribuzione in più fasi.
    > 1. È necessario rivedere e prendere decisioni di aggiornamento nel Desktop Analitica per contrassegnare gli asset critici e importanti come *pronti*. Per altre informazioni, vedere [esaminare gli asset che richiedono una decisione di aggiornamento](/sccm/desktop-analytics/deploy-prod#bkmk_review).
    > 1. Desktop Analitica Sincronizza per le raccolte di Configuration Manager eventuali dispositivi produzione soddisfano il *pronti* criteri.
    >
    > Quando in più fasi di Gestione configurazione di distribuzione verrà spostato automaticamente alla fase successiva, si applica solo ai dispositivi Desktop Analitica Sincronizza nella raccolta di produzione.

> [!Important]  
> Queste raccolte comunque eseguita la sincronizzazione le modifiche all'appartenenza. Se, ad esempio, identificare un problema con un asset e contrassegnarlo come **Impossibile**, i dispositivi con tale asset non soddisfano più il *pronto* criteri. Questi dispositivi vengono eliminati dalla raccolta di distribuzione di produzione.


## <a name="monitor"></a>Monitoraggio

### <a name="configuration-manager-console"></a>Console di Configuration Manager

Aprire il piano di distribuzione. Il **Preparazione aggiornamento decisioni - stato generale** riquadro offre un riepilogo dello stato per il piano di distribuzione. Questo stato è per raccolte il progetto pilota e di produzione. I dispositivi possono rientrano in una delle categorie seguenti:

- **Aggiornati**: I dispositivi sono aggiornati alla versione di Windows di destinazione per questo piano di distribuzione

- **Eseguire l'aggiornamento delle decisioni completata**: Uno dei seguenti stati:
    - I dispositivi con risorse degno di nota **pronti** o **pronto con monitoraggio e aggiornamento**
    - Lo stato del dispositivo viene **bloccato**, **dispositivo Replace** o **Reinstall dispositivo**

- **Non è stato esaminato**: I dispositivi con risorse degno di nota **non rivisti** o **revisione in corso**

Aggiorna lo stato del dispositivo nel **pilota stato** e **lo stato della produzione** riquadri con le azioni seguenti:

- Si apportano modifiche nella valutazione della compatibilità
- Dispositivi aggiornati alla versione di destinazione di Windows
- L'avanzamento della distribuzione

È anche possibile usare lo stesso come qualsiasi altra distribuzione di sequenza di attività di monitoraggio di distribuzione di Configuration Manager. Per altre informazioni, vedere [distribuzioni del sistema operativo monitoraggio](/sccm/osd/deploy-use/monitor-operating-system-deployments).


### <a name="desktop-analytics-portal"></a>Portale Analitica desktop

Usare la [portale di Analitica Desktop](https://aka.ms/desktopanalytics) per visualizzare lo stato di qualsiasi piano di distribuzione. Selezionare il piano di distribuzione e quindi selezionare **Panoramica del piano**.

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

Eseguire il progetto pilota per un periodo di tempo raccogliere dati operativi. Incoraggiare gli utenti dei dispositivi pilota per testare le app.

Quando la distribuzione pilota soddisfa i criteri di successo, passare all'articolo successivo per la distribuzione nell'ambiente di produzione.
> [!div class="nextstepaction"]  
> [Distribuire nell'ambiente di produzione](/sccm/desktop-analytics/deploy-prod)  

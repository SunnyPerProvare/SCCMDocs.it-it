---
title: Come eseguire la distribuzione in un progetto pilota
titleSuffix: Configuration Manager
description: Guida alle procedure per la distribuzione in un gruppo pilota di analisi desktop.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 637fbd8e-b8ea-4c7e-95ee-a60a323c496e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 75cce53f54221c63c0e6b6af3f1276cf51560f3d
ms.sourcegitcommit: b64ed4a10a90b93a5bd5454b6efafda90ad45718
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72386488"
---
# <a name="how-to-deploy-to-pilot-with-desktop-analytics"></a>Come eseguire la distribuzione in un progetto pilota con desktop Analytics

Uno dei vantaggi di analisi desktop è quello di identificare il set più piccolo di dispositivi che forniscono la più ampia copertura di fattori. Questo argomento è incentrato sui fattori che sono più importanti per un progetto pilota di aggiornamenti e aggiornamenti di Windows. Assicurarsi che il progetto pilota abbia un maggiore successo consente di spostarsi in modo più rapido e sicuro per le distribuzioni più ampie nell'ambiente di produzione.  

[!INCLUDE [Definition of pilot and production](includes/define-pilot-prod.md)]


## <a name="identify-devices"></a>Identificare i dispositivi

Il primo passaggio consiste nell'identificare i dispositivi da includere nel progetto pilota. Desktop Analytics consiglia i dispositivi basati sui dati segnalati ed è possibile includere o sostituire i dispositivi in questo elenco.

1. Passare al [portale di analisi del desktop](https://aka.ms/desktopanalytics)e nel gruppo Gestisci selezionare i piani di **distribuzione**.

1. Selezionare un piano di distribuzione.

1. Nel menu prepara gruppo del piano di distribuzione selezionare **identifica pilota**.

Verranno visualizzati i dati da desktop Analytics che mostrano il numero di dispositivi consigliati, incluso per la migliore copertura. Questo algoritmo si basa principalmente sull'uso di app importanti e critiche e sull'ampia gamma di configurazioni hardware.

Per l'elenco dei dispositivi consigliati aggiuntivi, eseguire le azioni seguenti:

- **Aggiungi tutto a progetto pilota**: aggiunge tutti i dispositivi consigliati al gruppo pilota
- **Aggiungi a progetto pilota**: Aggiungi solo i singoli dispositivi
- **Sostituire** eventuali dispositivi specifici dal progetto pilota
- **Ricalcola** al termine delle modifiche

È inoltre possibile prendere decisioni a livello di sistema relative alle raccolte di Configuration Manager da includere o escludere dai progetti pilota. Nel menu principale di analisi del desktop, nel gruppo impostazioni globali, selezionare **progetto pilota globale**.

### <a name="example"></a>Esempio

- Configurare la connessione desktop Analytics in Configuration Manager per la raccolta **tutti i sistemi** . Questa azione consente di registrare tutti i client nel servizio.
- È anche possibile configurare raccolte aggiuntive per la sincronizzazione con il desktop Analytics:
    - Tutti i client Windows 10
    - Tutti i dispositivi IT
    - Ufficio del CEO
- Nelle impostazioni **globali pilota** si includono tutte le raccolte di **dispositivi it** . Si esclude la raccolta di **uffici del CEO** .
- Si crea un piano di distribuzione e si seleziona **tutte le raccolte di client Windows 10** come **gruppo di destinazione**.
- L'elenco di **dispositivi pilota incluso** contiene il subset di dispositivi nel **gruppo di destinazione**: **tutti i client Windows 10** presenti anche nell'elenco di *inclusione* pilota globale: **tutti i dispositivi it**  
- Gli elenchi **aggiuntivi di dispositivi consigliati** contengono un set di dispositivi del **gruppo di destinazione** che forniscono la massima copertura e ridondanza per le risorse importanti.  Desktop Analytics esclude da questo elenco tutti i dispositivi nell'elenco di *esclusioni* pilota globale: **CEO Office**


## <a name="address-issues"></a>Risolvere i problemi

Usare il portale di analisi del desktop per esaminare eventuali problemi segnalati con asset che potrebbero bloccare la distribuzione. Quindi approvare, rifiutare o modificare la correzione consigliata. Prima che la distribuzione pilota venga avviata, è necessario che tutti gli elementi siano contrassegnati come **pronto** o **pronto (con monitoraggio e aggiornamento)** .

1. Passare al [portale di analisi del desktop](https://aka.ms/desktopanalytics)e nel gruppo Gestisci selezionare i piani di **distribuzione**.  

2. Selezionare un piano di distribuzione.  

3. Nel menu prepara gruppo del piano di distribuzione selezionare **Prepare Pilot**.  

4. Nella scheda **app** esaminare le app che richiedono l'input.  

5. Per ogni app, selezionare il nome dell'app. Nel riquadro informazioni esaminare la raccomandazione e selezionare la decisione di aggiornamento. Se si sceglie di **non rivedere o non** è **possibile**, desktop Analytics non include i dispositivi con questa app nella distribuzione pilota. Se si sceglie **pronto (con monitoraggio e aggiornamento)**, utilizzare le **note correttive** per acquisire le azioni da intraprendere per risolvere un problema, ad esempio *reinstallare* o *trovare la versione consigliata del produttore*.

6. Ripetere questa verifica per altri asset.  


## <a name="create-software"></a>Creazione di software

Prima di poter distribuire Windows, è necessario innanzitutto creare gli oggetti software in Configuration Manager. Per altre informazioni, vedere [sequenza di attività di aggiornamento sul posto di Windows 10](https://docs.microsoft.com/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).


## <a name="deploy-to-pilot-devices"></a>Distribuisci nei dispositivi pilota

Configuration Manager usa i dati di analisi del desktop per creare raccolte per le distribuzioni pilota e di produzione. Per assicurarsi che i dispositivi siano integri dopo ogni fase di distribuzione, usare la procedura seguente per creare una distribuzione in più fasi integrata di analisi del desktop:

1. Nella console di Configuration Manager passare alla **raccolta software**, espandere manutenzione di **analisi desktop**e selezionare il nodo piani di **distribuzione** .  

2. Selezionare il piano di distribuzione e quindi selezionare **Dettagli piano di distribuzione** nella barra multifunzione.  

3. Selezionare **Crea distribuzione** in più fasi nella barra multifunzione. Questa azione avvia la creazione guidata di una distribuzione in più fasi.

    > [!Tip]  
    > Se si vuole creare una distribuzione della sequenza di attività classica solo per la raccolta pilota, selezionare **Distribuisci** nel riquadro **stato pilota** . Questa azione avvia la distribuzione guidata del software. Per altre informazioni, vedere [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence).  

4. Immettere un nome per la distribuzione e selezionare la sequenza di attività da usare. Usare l'opzione per **creare automaticamente una distribuzione in due fasi predefinita**e quindi configurare le raccolte seguenti:  

    - **Prima raccolta**: trovare e selezionare la raccolta **pilota** per questo piano di distribuzione. La convenzione di denominazione standard per questa raccolta è `<deployment plan name> (Pilot)`.

    - **Seconda raccolta**: trovare e selezionare la raccolta di **produzione** per questo piano di distribuzione. La convenzione di denominazione standard per questa raccolta è `<deployment plan name> (Production)`.

    > [!Note]  
    > Con l'integrazione di analisi del desktop, Configuration Manager crea automaticamente raccolte pilota e di produzione per il piano di distribuzione. Prima di poterli usare, la sincronizzazione di queste raccolte può richiedere tempo. Per ulteriori informazioni, vedere [Troubleshoot-latence data](/sccm/desktop-analytics/troubleshooting#data-latency).<!-- 4984639 -->
    >
    > Queste raccolte sono riservate ai dispositivi dei piani di distribuzione di desktop Analytics. Le modifiche manuali a queste raccolte non sono supportate.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Completare la procedura guidata per configurare la distribuzione in più fasi. Per altre informazioni, vedere [Creare distribuzioni in più fasi](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).

    > [!Note]  
    > Usare l'impostazione predefinita per **iniziare automaticamente questa fase dopo un periodo di differimento (in giorni)**. Per avviare la seconda fase, è necessario soddisfare i criteri seguenti:
    >
    > 1. La prima fase raggiunge i criteri **percentuali di successo della distribuzione** per l'esito positivo. Questa impostazione viene configurata nella distribuzione in più fasi.
    > 1. È necessario rivedere e prendere decisioni relative all'aggiornamento in desktop Analytics per contrassegnare le risorse importanti e critiche come *pronte*. Per altre informazioni, vedere [esaminare gli asset che necessitano di una decisione di aggiornamento](/sccm/desktop-analytics/deploy-prod#bkmk_review).
    > 1. Desktop Analytics sincronizza le raccolte di Configuration Manager tutti i dispositivi di produzione che soddisfano i criteri di *pronto* .

> [!Important]  
> Queste raccolte continuano a essere sincronizzate in seguito alla modifica dell'appartenenza. Ad esempio, se si identifica un problema con un asset e lo si contrassegna come **non riuscito**, i dispositivi con tale asset non soddisfano più i criteri di *pronto* . Questi dispositivi vengono eliminati dalla raccolta di distribuzione di produzione.


## <a name="monitor"></a>Monitoraggio

### <a name="configuration-manager-console"></a>Console di Configuration Manager

Aprire il piano di distribuzione. Il riquadro **preparazione dell'aggiornamento-generale stato** fornisce un riepilogo dello stato del piano di distribuzione. Questo stato è per le raccolte pilota e di produzione. I dispositivi possono rientrare in una delle categorie seguenti:

- **Aggiornato: i**dispositivi sono stati aggiornati alla versione di Windows di destinazione per questo piano di distribuzione

- **Decisione di aggiornamento completata**: uno dei seguenti stati:
    - Dispositivi con asset rilevanti **pronti** o **pronti per la correzione**
    - Lo stato del dispositivo è **bloccato**, [**sostituire il dispositivo**](/sccm/desktop-analytics/about-deployment-plans#plan-assets) o reinstallare il **dispositivo**

- **Non verificato**: i dispositivi con asset degni di nota non sono stati **rivisti** o **esaminati in corso**

Lo stato del dispositivo viene aggiornato nei riquadri stato **pilota** e **stato di produzione** con le azioni seguenti:

- Si apportano modifiche alla valutazione della compatibilità
- I dispositivi vengono aggiornati alla versione di destinazione di Windows
- Avanzamento della distribuzione

È anche possibile usare Configuration Manager monitoraggio della distribuzione allo stesso modo di qualsiasi altra distribuzione della sequenza di attività. Per altre informazioni, vedere [Monitorare le distribuzioni del sistema operativo](/sccm/osd/deploy-use/monitor-operating-system-deployments).


### <a name="desktop-analytics-portal"></a>Portale di analisi desktop

Usare il [portale di analisi del desktop](https://aka.ms/desktopanalytics) per visualizzare lo stato di un piano di distribuzione. Selezionare il piano di distribuzione e quindi fare clic su **panoramica piano**.

![Screenshot della panoramica del piano di distribuzione in analisi desktop](media/deployment-plan-overview.png)

Selezionare il riquadro **pilota** . Viene riepilogato lo stato corrente della distribuzione pilota. Questo riquadro Visualizza anche i dati per il numero di dispositivi non avviati, in corso, completati o che restituiscono problemi.

Tutti i dispositivi che segnalano errori o altri problemi sono elencati anche nell'area dei dettagli pilota a destra. Per ottenere i dettagli del problema segnalato, selezionare **Revisione**. Questa azione consente di modificare la visualizzazione nella pagina **stato distribuzione**

Nella pagina **stato distribuzione** sono elencati i dispositivi nelle categorie seguenti:

- Non avviato
- In corso
- Completato
- Richiede attenzione-dispositivi
- Richiesta attenzione-problemi

Le categorie **richieste attenzione** mostrano le stesse informazioni, ma sono ordinate in modo diverso.

Selezionare un elenco specifico in una delle due visualizzazioni per ottenere maggiori dettagli sul problema rilevato.

Quando si affrontano questi problemi di distribuzione, il dashboard continua a mostrare lo stato dei dispositivi. Si aggiorna quando i dispositivi passano da **richiesta attenzione** a **completata**.


## <a name="next-steps"></a>Passaggi successivi

Consentire l'esecuzione del progetto pilota per un periodo di tempo per la raccolta dei dati operativi. Incoraggiare gli utenti di dispositivi pilota a testare le app.

Quando la distribuzione pilota soddisfa i criteri di riuscita, passare all'articolo successivo per eseguire la distribuzione in produzione.
> [!div class="nextstepaction"]  
> [Distribuisci in produzione](/sccm/desktop-analytics/deploy-prod)  

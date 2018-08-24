---
title: Creare una distribuzione in più fasi
titleSuffix: Configuration Manager
description: Usare distribuzioni in più fasi per automatizzare l'implementazione del software in diverse raccolte.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0ab238b2cf98da3d7ea1e86ef6462a721d7347e8
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383617"
---
# <a name="create-phased-deployments-with-configuration-manager"></a>Creare distribuzioni in più fasi con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le distribuzioni in più fasi automatizzano un'implementazione del software coordinata e in sequenza in più raccolte. È possibile, ad esempio, distribuire il software in una raccolta pilota e quindi continuare automaticamente l'implementazione in base ai criteri di superamento. È possibile creare distribuzioni in più fasi con l'impostazione predefinita di due fasi oppure configurare manualmente più fasi. La distribuzione in più fasi delle sequenze di attività non supporta l'installazione di PXE o di supporti. A partire dalla versione 1806, è possibile creare una distribuzione in più fasi per un'applicazione.<!--1358147-->  

> [!Tip]
> La funzionalità della distribuzione in più fasi è stata introdotta per la prima volta nella versione 1802 come [funzionalità di una versione non definitiva](/sccm/core/servers/manage/pre-release-features). A partire dalla versione 1806, questa funzionalità non è più in versione non definitiva.<!--1356837-->



## <a name="prerequisites"></a>Prerequisiti

#### <a name="security-scope"></a>Ambito di protezione
Le distribuzioni create da distribuzioni in più fasi non sono visualizzabili per l'utente amministratore che non ha l'ambito di protezione **Tutto**. Per altre informazioni, vedere [Ambiti di protezione](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_PlanScope).

#### <a name="distribute-application-content"></a>Distribuire il contenuto dell'applicazione
Prima di creare una distribuzione in più fasi per un'applicazione, distribuire il contenuto in un punto di distribuzione.<!--518293-->



## <a name="bkmk_settings"></a> Impostazioni delle fasi

Queste impostazioni sono univoche per le distribuzioni in più fasi. Configurare queste impostazioni durante la creazione o la modifica delle fasi per controllare la pianificazione e il comportamento del processo di distribuzione in più fasi. 


#### <a name="criteria-for-success-of-the-first-phase"></a>Criteri per l'esito positivo della prima fase  

- **Percentuale di esiti positivi della distribuzione**: specificare la percentuale di dispositivi che devono completare la distribuzione per la riuscita della prima fase. Per impostazione predefinita, questo valore è impostato su 95%. In altre parole, il sito considera la prima fase riuscita quando lo stato di conformità del 95% dei dispositivi è **Riuscito** per questa distribuzione. Il sito procede quindi alla seconda fase e crea una distribuzione del software nella raccolta successiva.  


#### <a name="conditions-for-beginning-second-phase-of-deployment-after-success-of-the-first-phase"></a>Condizioni per l'inizio della seconda fase della distribuzione dopo la riuscita della prima fase  

- **Inizia automaticamente questa fase dopo un periodo di differimento (in giorni)**: scegliere il numero di giorni di attesa prima di iniziare la seconda fase dopo la riuscita della prima. Per impostazione predefinita, questo valore è un giorno.  

- **Inizia manualmente la seconda fase della distribuzione**: il sito non inizia automaticamente la seconda fase dopo la riuscita della prima fase. Questa opzione richiede l'avvio manuale della seconda fase. Per altre informazioni, vedere [Passare alla fase successiva](/sccm/osd/deploy-use/manage-monitor-phased-deployments#bkmk_move).  

    > [!Note]  
    > Questa opzione non è disponibile per le distribuzioni in più fasi delle applicazioni.  


#### <a name="gradually-make-this-software-available-over-this-period-of-time-in-days"></a>Rendere gradualmente disponibile il software in questo periodo di tempo (in giorni)
<!--1358578--> A partire dalla versione 1806, configurare questa impostazione affinché l'implementazione in ogni fase avvenga gradualmente. Questo comportamento consente di ridurre il rischio di problemi di distribuzione e diminuisce il carico sulla rete causato dalla distribuzione di contenuto nei client. Il sito rende gradualmente disponibile il software a seconda della configurazione per ogni fase. Tutti i client in una fase hanno una scadenza definita in base al momento in cui il software viene reso disponibile. L'intervallo di tempo tra l'ora di disponibilità e la scadenza è uguale per tutti i client in una fase. Il valore predefinito di questa impostazione è zero, ovvero la distribuzione non è limitata per impostazione predefinita. Non impostare un valore maggiore di 30.<!--SCCMDocs-pr issue 2767--> 


#### <a name="configure-the-deadline-behavior-relative-to-when-the-software-is-made-available"></a>Configurare il comportamento della scadenza rispetto al momento in cui viene reso disponibile il software  

- **L'installazione è obbligatoria non appena possibile**: impostare come scadenza per l'installazione nel dispositivo il momento in cui il dispositivo viene incluso.  

- **L'installazione è obbligatoria dopo questo periodo di tempo**: impostare come scadenza per l'installazione un numero di giorni specifico dopo che il dispositivo è stato incluso. Per impostazione predefinita, questo valore è 7 giorni.   


<!--### Examples
Include a timeline diagram
-->



## <a name="bkmk_auto"></a> Creare automaticamente una distribuzione predefinita in due fasi

1. Avviare la procedura guidata Crea una distribuzione in più fasi nella console di Configuration Manager. Questa azione varia in base al tipo di software da distribuire:  

    - **Applicazione** (solo nella versione 1806 o successiva): passare a **Raccolta software**, espandere **Gestione applicazioni** e selezionare **Applicazioni**. Selezionare un'applicazione esistente e quindi fare clic su **Crea una distribuzione in più fasi** nella barra multifunzione.  

    - **Sequenza di attività**: passare all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare **Sequenze di attività**. Selezionare una sequenza di attività esistente e quindi fare clic su **Crea una distribuzione in più fasi** nella barra multifunzione.  

2. Nella pagina **Generale** assegnare alla distribuzione in più fasi un **Nome** e una **Descrizione** (facoltativa), quindi selezionare **Crea automaticamente una distribuzione predefinita in due fasi**.  

3. Fare clic su **Sfoglia** e selezionare una raccolta di destinazione per i campi **Prima raccolta** e **Seconda raccolta**. Per una sequenza di attività selezionare le raccolte di dispositivi. Per un'applicazione selezionare le raccolte di utenti o dispositivi. Fare clic su **Avanti**.  

    > [!Important]  
    > La procedura guidata Crea una distribuzione in più fasi non segnala all'utente se una distribuzione è potenzialmente ad alto rischio. Per altre informazioni, vedere [Impostazioni per gestire le distribuzioni ad alto rischio](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments) e la nota della sezione [Distribuire una sequenza di attività](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).  

4. Nella pagina **Impostazioni** scegliere un'opzione per ogni impostazione di pianificazione. Per altre informazioni, vedere [Impostazioni delle fasi](#bkmk_settings). Al termine, fare clic su **Avanti**.  

5. Nella pagina **Fasi** vedere le due fasi create dalla procedura guidata per le raccolte specificate. Fare clic su **Avanti**.   

    > [!Note]  
    > Questa sezione descrive la procedura per creare automaticamente una distribuzione predefinita in due fasi. La procedura guidata consente di aggiungere, rimuovere, riordinare, modificare o visualizzare le fasi per una distribuzione in più fasi. Per altre informazioni su queste azioni aggiuntive, vedere [Creare una distribuzione in più fasi con fasi configurate manualmente](#bkmk_manual).  

6. Verificare le selezioni nella scheda **Riepilogo** e quindi fare clic su **Avanti** per completare la procedura guidata.  



## <a name="bkmk_manual"></a> Creare una distribuzione in più fasi con fasi configurate manualmente
<!--1358148--> 

A partire dalla versione 1806, creare una distribuzione in più fasi con fasi configurate manualmente per una sequenza di attività. Aggiungere fino a 10 fasi aggiuntive dalla scheda **Fasi** della procedura guidata Crea una distribuzione in più fasi. 

> [!Note]  
> Al momento non è possibile creare manualmente le fasi per un'applicazione. La procedura guidata crea automaticamente due fasi per le distribuzioni di applicazioni.


1. Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi** e selezionare **Sequenze di attività**.  

2. Fare clic con il pulsante destro del mouse su una sequenza di attività esistente e selezionare **Create Phased Deployment** (Crea distribuzione in fasi).  

3. Nella pagina **Generale** della procedura guidata Crea una distribuzione in più fasi assegnare alla distribuzione in più fasi un **Nome** e una **Descrizione** (facoltativa) e quindi selezionare **Configura manualmente tutte le fasi**.  

4. Nella pagina **Fasi** della procedura guidata Crea una distribuzione in più fasi sono disponibili le azioni seguenti:  

    - **Filtrare** l'elenco di fasi di distribuzione. Immettere una stringa di caratteri per trovare una corrispondenza senza distinzione tra maiuscole e minuscole delle colonne Ordine, Nome o Raccolta. 

    - **Aggiungere** una nuova fase:  

        1. Nella pagina **Generale** dell'Aggiunta guidata fasi specificare un **Nome** per la fase e quindi selezionare la **Raccolta di fasi** di destinazione. Le impostazioni aggiuntive in questa pagina sono uguali a quelle usate quando si distribuisce normalmente una sequenza di attività.  

        2. Nella pagina **Impostazioni delle fasi** dell'Aggiunta guidata fasi configurare le impostazione di pianificazione e al termine selezionare **Avanti**. Per altre informazioni, vedere [Impostazioni](#bkmk_settings).   

            > [!Note]  
            > Non è possibile modificare l'impostazione della fase, **Percentuale di esiti positivi della distribuzione**, nella prima fase. Questa impostazione si applica solo alle fasi che hanno una fase precedente.  

        3. Le impostazioni nelle pagine **Esperienza utente** e **Punti di distribuzione** dell'Aggiunta guidata fasi sono uguali a quelle usate quando si distribuisce normalmente una sequenza di attività.  

        4. Controllare le impostazioni nella pagina **Riepilogo** e quindi completare l'Aggiunta guidata fasi.  

    - **Modifica**: dopo aver aggiunto una fase, selezionarla e fare clic su questo pulsante per modificare la fase. Questa azione apre la finestra Proprietà della fase in cui le schede sono uguali alle pagine dell'Aggiunta guidata fasi.  

    - **Rimuovi**: selezionare una fase esistente e fare clic su questo pulsante per eliminare la fase.  

       > [!Warning]  
       > Non viene visualizzata alcuna conferma e non è possibile in alcun modo annullare questa azione.  

    - **Sposta su** o **Sposta giù**: la procedura guidata ordina le fasi in base a come vengono aggiunte. La fase aggiunta più di recente è l'ultima nell'elenco. Per modificare l'ordine, selezionare una fase e quindi fare clic su uno di questi pulsanti per spostare la posizione della fase nell'elenco.  

       > [!Important]  
       > Dopo aver modificato l'ordine, controllare le impostazioni delle fasi. Verificare che le impostazioni seguenti siano ancora coerenti con i requisiti per la distribuzione in più fasi:  
       > 
       > - Criteri per la riuscita della fase precedente  
       > - Condizioni per l'inizio di questa fase della distribuzione dopo l'esito positivo della fase precedente   

5. Fare clic su **Avanti**. Controllare le impostazioni nella pagina **Riepilogo** e quindi completare la procedura guidata Crea una distribuzione in più fasi.  


Dopo aver creato una distribuzione in più fasi, aprirne le proprietà per apportare le modifiche:  

- **Aggiungere** fasi aggiuntive a una distribuzione in più fasi esistente.  

- Se una fase non è attiva, è possibile **modificarla**, **rimuoverla** o **spostarla** verso l'alto o verso il basso. Non è possibile spostarla prima di una fase attiva.  

- Quando una fase è attiva, è di sola lettura. Non è possibile modificarla, rimuoverla o spostarne la posizione nell'elenco. L'unica opzione consiste nel **visualizzare** le proprietà della fase.  

- Una distribuzione in più fasi di un'applicazione è sempre di sola lettura.  



## <a name="next-steps"></a>Passaggi successivi
[Gestire e monitorare le distribuzioni in più fasi](/sccm/osd/deploy-use/manage-monitor-phased-deployments)

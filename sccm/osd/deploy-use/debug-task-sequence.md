---
title: Eseguire il debug di una sequenza di attività
titleSuffix: Configuration Manager
description: Usare lo strumento Debug sequenza di attività per risolvere i problemi relativi a una sequenza di attività.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 4b60b0e1-ffa4-4fd5-864e-70a0546c8b3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fadcd362f44e5261ae5226ed22b7cff4c4eb261f
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/26/2019
ms.locfileid: "68537739"
---
# <a name="debug-a-task-sequence"></a>Eseguire il debug di una sequenza di attività

<!--3612274-->

A partire dalla versione 1906, il debugger della sequenza di attività è un nuovo strumento per la risoluzione dei problemi. Una sequenza di attività viene distribuita in modalità di debug a una raccolta ridotta. Consente di esaminare la sequenza di attività in modo controllato per facilitare la risoluzione dei problemi e l'analisi. Il debugger viene attualmente eseguito sullo stesso dispositivo del motore della sequenza di attività, ma non è un debugger remoto.

> [!Note]  
> In questa versione di Configuration Manager, il debugger della sequenza di attività è una funzionalità di versione non definitiva. Per abilitarla, vedere [Funzionalità di versioni non definitive in System Center Configuration Manager](/sccm/core/servers/manage/pre-release-features).  


## <a name="prerequisites"></a>Prerequisiti

- Aggiornare il client di Configuration Manager nel dispositivo di destinazione

- Accedere al dispositivo di destinazione come utente nel gruppo **Administrators** locale. Il debugger viene eseguito solo per gli amministratori.

- Aggiornare l'immagine di avvio associata alla sequenza di attività per assicurarsi che la versione del client sia la più recente


## <a name="start-the-tool"></a>Avviare lo strumento

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e selezionare **Sequenze di attività**.

1. Selezionare una sequenza di attività. Nel gruppo di distribuzione della barra multifunzione selezionare **Debug**.

    > [!Tip]  
    > In alternativa, impostare la variabile **TSDebugMode** su `TRUE` per una raccolta a cui viene distribuita la sequenza di attività. Questa variabile modifica il comportamento di qualsiasi sequenza di attività su qualsiasi dispositivo in tale raccolta.  

1. Creare una distribuzione di debug. Le impostazioni di distribuzione sono le stesse di una normale distribuzione della sequenza di attività. Per altre informazioni, vedere [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence#process).

    > [!Note]  
    > È possibile selezionare solo una piccola raccolta per una distribuzione di debug. Vengono visualizzate solo le raccolte di dispositivi con almeno 10 membri.


## <a name="use-the-tool"></a>Usare lo strumento

Quando la sequenza di attività viene eseguita nel dispositivo, viene visualizzata la finestra Debugger delle sequenze di attività come mostra lo screenshot seguente:

![Screenshot del debugger di sequenze di attività](media/3612274-tsdebug.png)

Il debugger include i controlli seguenti:

- **Passaggio**: dalla posizione *corrente* eseguire solo il passaggio successivo della sequenza di attività.  

    > [!Note]  
    > Quando la sequenza di attività è in modalità di debug, se un passaggio restituisce un errore irreversibile, la sequenza di attività non ha esito negativo come di consueto. Questo comportamento consente di ripetere un passaggio dopo avere apportato una modifica esterna.

- **Esegui**: dalla posizione *corrente* eseguire normalmente la sequenza di attività fino alla fine o al punto di *interruzione* successivo oppure se un passaggio non viene eseguito. Prima di usare questa azione, assicurarsi di impostare eventuali punti di rottura con l'azione **imposta interruzioni** .

- **Imposta corrente**: selezionare un passaggio nel debugger e quindi selezionare **Imposta corrente**. Questa azione sposta il puntatore *corrente* su quel passaggio. Questa azione consente di saltare passaggi o spostarsi all'indietro.  

    > [!Warning]  
    > Il debugger non considera il tipo di passaggio quando si modifica la posizione corrente nella sequenza. Alcuni passaggi possono impostare le variabili della sequenza di attività necessarie per la valutazione della condizione nei passaggi successivi. Se l'ordine di esecuzione non è corretto, alcuni passaggi possono non riuscire o causare danni significativi a un dispositivo. Usare questa opzione a proprio rischio.  

- **Imposta interruzione**: selezionare un passaggio nel debugger e quindi selezionare **Imposta interruzione**. Questa azione aggiunge un punto di *interruzione* nel debugger. Durante l'**esecuzione** la sequenza di attività si ferma in corrispondenza di un'*interruzione*.  

    - Prima di usare l'azione **Esegui** , impostare i punti di rottura.

    - I punti di interruzioni non vengono salvati dopo il riavvio del computer, ad esempio con il passaggio [Riavvia computer](/sccm/osd/understand/task-sequence-steps#BKMK_RestartComputer) . Se ad esempio si avvia il debugger da software Center per una sequenza di attività per la creazione di immagini, non impostare interruzioni nella fase Windows PE. Quando il computer viene riavviato in Windows PE, il debugger sospende la sequenza di attività in modo da poter impostare le interruzioni.

- **Cancella tutte le interruzioni**: rimuovere tutti i punti di interruzione.

- **File di log**: apre il file di log della sequenza di attività corrente, **file Smsts. log**, con [CMTrace](/sccm/core/support/cmtrace). È possibile visualizzare le voci di log quando il motore della sequenza di attività è "in attesa del debugger".

- **Prompt**dei comandi: in Windows PE apre un prompt dei comandi.

- **Annulla**: chiude il debugger e non esegue la sequenza di attività.

- **Quit**: scollega e chiude il debugger, ma la sequenza di attività continua a essere eseguita normalmente.

Nella finestra delle **variabili della sequenza di attività** vengono visualizzati i valori correnti per tutte le variabili nell'ambiente della sequenza di attività. Per altre informazioni, vedere [Variabili della sequenza di attività](/sccm/osd/understand/task-sequence-variables). Se si usa il passaggio [Imposta variabile della sequenza di attività](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) con l'opzione non **visualizzare questo valore**, il debugger non visualizzerà il valore della variabile. Non è possibile modificare i valori delle variabili nel debugger.

> [!Note]
> Alcune variabili della sequenza di attività sono solo per uso interno e non sono elencate nella documentazione di riferimento.

Il debugger della sequenza di attività continua a essere eseguito dopo un passaggio [Riavvia computer](/sccm/osd/understand/task-sequence-steps#BKMK_RestartComputer) , ma è necessario ricreare eventuali punti di interruzione. Anche se la sequenza di attività potrebbe non richiederla, poiché il debugger richiede l'interazione dell'utente, è necessario accedere a Windows per continuare. Se non si esegue l'accesso dopo un'ora per continuare il debug, la sequenza di attività ha esito negativo.

Esegue anche la procedura in una sequenza di attività figlio con il passaggio [Esegui sequenza di attività](/sccm/osd/understand/task-sequence-steps#child-task-sequence) . La finestra del debugger Mostra i passaggi della sequenza di attività figlio insieme alla sequenza di attività principale.


## <a name="known-issues"></a>Problemi noti

Se si ha come destinazione una distribuzione normale e una distribuzione di debug allo stesso dispositivo tramite più distribuzioni, è possibile che il debugger della sequenza di attività non venga avviato.


## <a name="see-also"></a>Vedere anche

- [Informazioni sui passaggi della sequenza di attività](/sccm/osd/understand/task-sequence-steps)
- [Variabili della sequenza di attività](/sccm/osd/understand/task-sequence-variables)
- [Come usare le variabili della sequenza di attività](/sccm/osd/understand/using-task-sequence-variables)
- [Distribuire una sequenza di attività](/sccm/osd/deploy-use/deploy-a-task-sequence)
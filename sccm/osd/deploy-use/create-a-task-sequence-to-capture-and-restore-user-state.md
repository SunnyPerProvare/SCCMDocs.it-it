---
title: "Creare una sequenza di attività per acquisire e ripristinare lo stato utente"
titleSuffix: Configuration Manager
description: "Usare le sequenze di attività di System Center Configuration Manager per acquisire e ripristinare i dati dello stato utente in scenari di distribuzione del sistema operativo."
ms.custom: na
ms.date: 06/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
caps.latest.revision: "7"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 5bb55816481db8b93baada07d36c72dd39b62478
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-system-center-configuration-manager"></a>Creare una sequenza di attività per acquisire e ripristinare lo stato utente in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile usare le sequenze attività di System Center Configuration Manager per acquisire e ripristinare i dati sullo stato utente in scenari di distribuzione del sistema operativo in cui si desidera mantenere lo stato utente del sistema operativo corrente. A seconda del tipo di sequenza di attività che si crea, è possibile aggiungervi automaticamente i passaggi di acquisizione e ripristino. In altri scenari potrebbe essere necessario aggiungere manualmente i passaggi di acquisizione e ripristino alla sequenza di attività. Questo argomento fornisce i passaggi che è necessario aggiungere a una sequenza di attività esistente per acquisire e ripristinare i dati dello stato utente.  

##  <a name="BKMK_CaptureRestoreUserState"></a> Come acquisire e ripristinare i dati dello stato utente  
 Per acquisire e ripristinare lo stato utente, è necessario aggiungere i passaggi seguenti alla sequenza di attività:  

-   **Richiedi archiviazione stati**: questo passaggio è necessario solo se si archivia lo stato utente nel punto di migrazione stato.  

-   **Acquisisci stato utente**: questo passaggio consente di acquisire i dati dello stato utente e di archiviarli nel punto di migrazione stato o localmente tramite collegamenti.  

-   **Ripristina stato utente**: questo passaggio consente di ripristinare i dati dello stato utente nel computer di destinazione. Consente di recuperare i dati da un punto di migrazione stato utente o dal computer di destinazione.  

-   **Rilascia archiviazione stati**: questo passaggio è necessario solo se si archivia lo stato utente nel punto di migrazione stato. Questo passaggio consente di rimuovere i dati dal punto di migrazione stato.  

 Utilizzare le procedure seguenti per aggiungere i passaggi della sequenza attività necessari per acquisire lo stato utente e ripristinare lo stato utente. Per altre informazioni sulla creazione di sequenze di attività, vedere [Gestire le sequenze di attività per automatizzare le attività](manage-task-sequences-to-automate-tasks.md).  

#### <a name="to-add-task-sequence-steps-to-capture-the-user-state"></a>Per aggiungere i passaggi della sequenza attività per acquisire lo stato utente  

1.  Nell'elenco **Sequenza attività** selezionare una sequenza attività, quindi fare clic su **Modifica**.  

2.  Se si utilizza un punto di migrazione stato per archiviare lo stato utente, aggiungere il passaggio **Richiedi archiviazione stati** alla sequenza attività. Nella finestra di dialogo **Editor della sequenza attività** fare clic su **Aggiungi**, scegliere **Stato utente**e quindi fare clic su **Richiedi archiviazione stati**. Specificare le proprietà e le opzioni seguenti per il passaggio **Richiedi archiviazione stati** e quindi fare clic su **Applica**.  

     Nella scheda **Proprietà** specificare le opzioni seguenti:  

    -   Immettere un nome e una descrizione per il passaggio.  

    -   Fare clic su **Acquisisci stato dal computer**.  

    -   Nella casella **Numero di tentativi** specificare per quante volte la sequenza attività tenterà di acquisire i dati dello stato utente qualora si verifichi un errore.  

    -   Nella casella **Intervallo tra tentativi (in secondi)** specificare quanti secondi la sequenza attività attenderà prima di riprovare ad acquisire i dati.  

    -   Selezionare la casella di controllo **Se l'account del computer non riesce a connettersi a un archivio stato, usare l'account di accesso alla rete** per specificare se usare l'[account di accesso alla rete](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA) di Configuration Manager per connettersi allo stato utente.  

     Nella scheda **Opzioni** specificare le seguenti opzioni:  

    -   Selezionare la casella di controllo **Continua in caso di errore** se si desidera che la sequenza attività passi al passaggio successivo in caso di errore di questo passaggio.  

    -   Specificare le condizioni che devono essere soddisfatte prima di proseguire la sequenza attività in caso di errore.  

3.  Aggiungere il passaggio **Acquisisci stato utente** alla sequenza attività. Nella finestra di dialogo **Editor della sequenza attività** fare clic su **Aggiungi**, scegliere **Stato utente**e quindi fare clic su **Acquisisci stato utente**. Specificare le proprietà e le opzioni seguenti per il passaggio **Acquisisci stato utente** e quindi fare clic su **OK**.  

    > [!IMPORTANT]  
    >  Quando si aggiunge questo passaggio alla sequenza attività, impostare anche la variabile della sequenza attività **OSDStateStorePath** per specificare dove vengono archiviati i dati dello stato utente. Se si archivia lo stato utente localmente, non specificare una cartella radice perché potrebbe verificarsi un errore nella sequenza attività. Quando si archiviano i dati utente localmente, utilizzare sempre una cartella o una sottocartella. Per informazioni su questa variabile, vedere [Variabili di azione della sequenza di attività Acquisisci stato utente](../understand/task-sequence-action-variables.md#BKMK_CaptureUserState).  

     Nella scheda **Proprietà** specificare le opzioni seguenti:  

    -   Immettere un nome e una descrizione per il passaggio.  

    -   Specificare il pacchetto contenente il file di origine USMT utilizzato per acquisire i dati dello stato utente.  

    -   Specificare i profili utente da acquisire:  

        -   Fare clic su **Acquisisci tutti i profili utente utilizzando le opzioni standard** per acquisire tutti i profili utente.  

        -   Fare clic su **Personalizza modalità di acquisizione dei profili utente** per specificare i singoli profili utente da acquisire. Selezionare il file di configurazione (miguser.xml, migsys.xml o migapp.xml) che contiene le informazioni sul profilo utente. Non è possibile usare il file di configurazione config.xml qui, ma è possibile aggiungerlo manualmente alla riga di comando USMT usando le variabili OSDMigrageAdditionalCaptureOptions e OSDMigrateAdditionalRestoreOptions.

    -   Selezionare **Abilita la registrazione dettagliata** per specificare la quantità di informazioni da scrivere nei file di log in caso di errore.  

    -   Selezionare **Ignora file che utilizzano Encrypting File System (EFS)**.  

    -   Selezionare **Copia utilizzando l'accesso al file system** per specificare le impostazioni seguenti:  

        -   **Continua se non è possibile acquisire alcuni file**: questa impostazione consente al passaggio della sequenza di attività di continuare il processo di migrazione, anche se non è possibile acquisire alcuni file. Se si disattiva questa opzione e non è possibile acquisire un file, il passaggio della sequenza attività avrà esito negativo. Questa opzione è attivata per impostazione predefinita.  

        -   **Esegui acquisizione localmente utilizzando i collegamenti invece di copiare i file**: questa impostazione consente di usare la funzionalità di migrazione con collegamenti reali disponibile in USMT 4.0. Questa impostazione viene ignorata se si utilizzano versioni di USMT precedenti a USMT 4.0.  

        -   **Acquisisci in modalità non in linea (solo Windows PE)**: questa impostazione consente di acquisire lo stato di utilizzo da Windows PE senza eseguire l'avvio del sistema operativo esistente. Questa impostazione viene ignorata se si utilizzano versioni di USMT precedenti a USMT 4.0.  

    -   Selezionare **Acquisisci utilizzando Servizio Copia Shadow del volume (VSS)**. Questa impostazione viene ignorata se si utilizzano versioni di USMT precedenti a USMT 4.0.  

     Nella scheda **Opzioni** specificare le seguenti opzioni:  

    -   Selezionare la casella di controllo **Continua in caso di errore** se si desidera che la sequenza attività passi al passaggio successivo in caso di errore di questo passaggio.  

    -   Specificare le condizioni che devono essere soddisfatte prima di proseguire la sequenza attività in caso di errore.  

4.  Se si usa un punto di migrazione stato per archiviare lo stato utente, aggiungere il passaggio [Rilascia archiviazione stati](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) alla sequenza di attività. Nella finestra di dialogo **Editor della sequenza attività** fare clic su **Aggiungere**, scegliere **Stato utente**, quindi fare clic su **Rilascia archiviazione stati**. Specificare le proprietà e le opzioni seguenti per il passaggio **Rilascia archiviazione stati** , quindi fare clic su **OK**.  

    > [!IMPORTANT]  
    >  È necessario che l'azione della sequenza attività eseguita prima del passaggio **Rilascia archiviazione stati** abbia esito positivo prima dell'avvio del passaggio **Rilascia archiviazione stati** .  

     Nella scheda **Proprietà** immettere un nome e una descrizione per il passaggio.  

     Nella scheda **Opzioni** specificare le seguenti opzioni.  

    -   Selezionare la casella di controllo **Continua in caso di errore** se si desidera che la sequenza attività passi al passaggio successivo in caso di errore di questo passaggio.  

    -   Specificare le condizioni che devono essere soddisfatte prima di proseguire la sequenza attività in caso di errore.  

 Distribuire questa sequenza attività per acquisire lo stato utente in un computer di destinazione. Per altre informazioni su come distribuire sequenze di attività, vedere [Distribuire una sequenza di attività](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

#### <a name="to-add-task-sequence-steps-to-restore-the-user-state"></a>Per aggiungere i passaggi della sequenza attività per ripristinare lo stato utente  

1.  Nell'elenco **Sequenza attività** selezionare una sequenza attività, quindi fare clic su **Modifica**.  

2.  Aggiungere il passaggio [Ripristina stato utente](../understand/task-sequence-steps.md#BKMK_RestoreUserState) alla sequenza attività. Nella finestra di dialogo **Editor della sequenza attività** fare clic su **Aggiungere**, scegliere **Stato utente**, quindi fare clic su **Ripristina stato utente**. Questo passaggio stabilisce una connessione al punto di migrazione dello stato. Specificare le proprietà e le opzioni seguenti per il passaggio **Ripristina stato utente** , quindi fare clic su **OK**.  

     Nella scheda **Proprietà** specificare le seguenti proprietà:  

    -   Immettere un nome e una descrizione per il passaggio.  

    -   Specificare il pacchetto che contiene l'USMT per ripristinare i dati sullo stato dell'utente.  

    -   Specificare i profili utente da ripristinare:  

        -   Fare clic su **Ripristina tutti i profili utente acquisiti con le opzioni standard** per ripristinare tutti i profili utente.  

        -   Fare clic su **Personalizza la modalità di ripristino dei profili utente** per ripristinare singoli profili utente. Selezionare il file di configurazione (miguser.xml, migsys.xml o migapp.xml) che contiene le informazioni sul profilo utente. Non è possibile usare il file di configurazione config.xml qui, ma è possibile aggiungerlo manualmente alla riga di comando USMT usando le variabili OSDMigrageAdditionalCaptureOptions e OSDMigrateAdditionalRestoreOptions.

    -   Selezionare **Ripristina profili utente del computer locale** per fornire una nuova password per i profili ripristinati. Non è possibile eseguire la migrazione delle password per i profili locali.  

        > [!NOTE]  
        >  Se sono disponibili account utente locale e si usa il passaggio [Acquisisci stato utente](../understand/task-sequence-steps.md#BKMK_CaptureUserState) con l'opzione **Acquisisci tutti i profili utente utilizzando le opzioni standard**selezionata, sarà necessario selezionare l'impostazione **Ripristina profili utente del computer locale** nel passaggio [Ripristina stato utente](../understand/task-sequence-steps.md#BKMK_RestoreUserState). In caso contrario, la sequenza attività avrà esito negativo.  

    -   Selezionare **Continua se non è possibile ripristinare dei file** se si desidera che il passaggio **Ripristina stato utente** proceda anche in caso di impossibilità di ripristinare un file.  

         Se lo stato utente viene archiviato tramite collegamenti locali e il ripristino ha esito negativo, l'utente amministratore potrà eliminare manualmente i collegamenti reali creati per l'archiviazione dei dati. In alternativa, la sequenza attività può eseguire lo strumento USMTUtils. Se si utilizza USMTUtils per eliminare il collegamento reale, aggiungere un passaggio [Riavvia computer](../understand/task-sequence-steps.md#BKMK_RestartComputer) dopo l'esecuzione di USMTUtils.  

    -   Selezionare **Abilita la registrazione dettagliata** per specificare la quantità di informazioni da scrivere nei file di log in caso di errore.  

     Nella scheda **Opzioni** specificare le seguenti opzioni:  

    -   Selezionare la casella di controllo **Continua in caso di errore** se si desidera che la sequenza attività passi al passaggio successivo in caso di errore di questo passaggio.  

    -   Specificare le condizioni che devono essere soddisfatte prima di proseguire la sequenza attività in caso di errore.  

3.  Se si usa un punto di migrazione stato per archiviare lo stato utente, aggiungere il passaggio [Rilascia archiviazione stati](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) alla sequenza di attività. Nella finestra di dialogo **Editor della sequenza attività** fare clic su **Aggiungere**, scegliere **Stato utente**, quindi fare clic su **Rilascia archiviazione stati**. Specificare le proprietà e le opzioni seguenti per il passaggio **Rilascia archiviazione stati** , quindi fare clic su **OK**.  

    > [!IMPORTANT]  
    >  È necessario che l'azione della sequenza attività eseguita prima del passaggio **Rilascia archiviazione stati** abbia esito positivo prima dell'avvio del passaggio **Rilascia archiviazione stati** .  

     Nella scheda **Proprietà** immettere un nome e una descrizione per il passaggio.  

     Nella scheda **Opzioni** specificare le seguenti opzioni.  

    -   Selezionare la casella di controllo **Continua in caso di errore** se si desidera che la sequenza attività passi al passaggio successivo in caso di errore di questo passaggio.  

    -   Specificare le condizioni che devono essere soddisfatte prima di proseguire la sequenza attività in caso di errore.  

 Distribuire questa sequenza attività per ripristinare lo stato utente in un computer di destinazione. Per informazioni sulla distribuzione di sequenze di attività, vedere [Distribuire una sequenza di attività](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

## <a name="next-steps"></a>Passaggi successivi
[Monitorare la distribuzione della sequenza di attività](monitor-operating-system-deployments.md#BKMK_TSDeployStatus)

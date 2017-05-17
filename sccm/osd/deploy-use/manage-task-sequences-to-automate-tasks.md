---
title: "Gestire le sequenze di attività per automatizzare le attività | Microsoft Docs"
description: "È possibile creare, modificare, distribuire, importare ed esportare sequenze di attività per gestirle nell&quot;ambiente System Center Configuration Manager."
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
caps.latest.revision: 10
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: 113fa73bf0bd1b3b8a4754eb1e96549c520d7995
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017


---
# <a name="manage-task-sequences-to-automate-tasks-in-system-center-configuration-manager"></a>Gestire le sequenze di attività per automatizzare le attività in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare le sequenze di attività per automatizzare i passaggi nell'ambiente System Center Configuration Manager. Questi passaggi consentono di distribuire un'immagine del sistema operativo in un computer di destinazione, di creare e acquisire un'immagine del sistema operativo da un set di file di installazione del sistema operativo e di acquisire e ripristinare le informazioni sullo stato utente. Le sequenze di attività si trovano nella console di Configuration Manager in **Raccolta software** > **Sistemi operativi** > **Sequenza di attività**. Il nodo **Sequenza di attività** che include le sottocartelle create viene replicato in tutta la gerarchia di Configuration Manager. Per informazioni sulla pianificazione, vedere [Considerazioni sulla pianificazione per l'automazione delle attività](../plan-design/planning-considerations-for-automating-tasks.md).  

 Usare le sezioni seguenti per gestire le sequenze di attività.

##  <a name="BKMK_CreateTaskSequence"></a> Creare sequenze di attività  
 Creare sequenze attività usando la Creazione guidata della sequenza di attività. Questa procedura guidata consente di creare i seguenti tipi di sequenze attività:  

|Tipo di sequenza di attività|Altre informazioni|  
|------------------------|----------------------|  
|[Sequenza di attività per installare un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md)|Questo tipo di sequenza di attività crea i passaggi per installare un sistema operativo, nonché consente di migrare i dati utente, includere gli aggiornamenti software e installare le applicazioni.|  
|[Sequenza di attività per aggiornare un sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md)|Questo tipo di sequenza di attività crea i passaggi per aggiornare un sistema operativo, nonché consente di includere gli aggiornamenti software e installare le applicazioni.|  
|[Sequenza di attività per acquisire un sistema operativo](create-a-task-sequence-to-capture-an-operating-system.md)|Questo tipo di sequenza di attività crea i passaggi per creare e acquisire un sistema operativo da un computer di riferimento. È possibile includere gli aggiornamenti software e installare le applicazioni nel computer di riferimento prima dell'acquisizione dell'immagine.|  
|[Sequenza di attività per acquisire e ripristinare lo stato utente](create-a-task-sequence-to-capture-and-restore-user-state.md)|Questa sequenza di attività fornisce i passaggi da aggiungere a una sequenza di attività esistente per acquisire e ripristinare i dati dello stato utente.|  
|[Sequenza di attività per gestire dischi rigidi virtuali](use-a-task-sequence-to-manage-virtual-hard-disks.md)|Questo tipo di sequenza di attività contiene i passaggi per creare un disco rigido virtuale, includendo l'installazione di un sistema operativo e di applicazioni, che è possibile pubblicare in System Center Virtual Machine Manager (VMM) dalla console di Configuration Manager.|  
|[Sequenza di attività personalizzata](create-a-custom-task-sequence.md)|Questo tipo di sequenza di attività non aggiunge alcun passaggio alla sequenza di attività. È necessario modificare la sequenza di attività e aggiungervi i passaggi dopo la creazione.|  

## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Tornare alla pagina precedente quando si verifica un errore di una sequenza di attività
A partire da Configuration Manager versione 1702, è possibile tornare alla pagina precedente quando si esegue una sequenza di attività e si verifica un errore. Prima di questa versione, se si verificava un errore era necessario riavviare la sequenza di attività. È ad esempio possibile usare il pulsante **Precedente** negli scenari seguenti:

- Quando un computer viene avviato in Windows PE, potrebbe essere visualizzata la finestra di dialogo di avvio della sequenza di attività prima che la sequenza stessa sia disponibile. Se in questo scenario si fa clic su Avanti, viene visualizzata la pagina finale della sequenza di attività che informa l'utente che non sono disponibili sequenze di attività. È ora possibile fare clic su **Precedente** per ripetere la ricerca di sequenze di attività. È possibile ripetere questo processo finché la sequenza di attività non è disponibile.
- Quando si esegue una sequenza di attività ma i pacchetti di contenuto dipendenti non sono ancora disponibili nei punti di distribuzione, la sequenza di attività ha esito negativo. È ora possibile distribuire il contenuto mancante, se non è stato ancora distribuito, o attendere che il contenuto sia disponibile nei punti di distribuzione e quindi fare clic su **Precedente** per ripetere la ricerca di contenuto con la sequenza di attività.

##  <a name="BKMK_ModifyTaskSequence"></a> Modificare una sequenza di attività  
 È possibile modificare una sequenza di attività aggiungendo o rimuovendo passaggi della sequenza di attività, aggiungendo o rimuovendo gruppi di sequenze attività oppure modificando l'ordine dei passaggi. Usare la seguente procedura per modificare una sequenza di attività esistente.  

> [!IMPORTANT]  
>  Quando si modifica una sequenza di attività creata usando la Creazione guidata della sequenza di attività, il nome del passaggio può indicare l'azione del passaggio o il tipo di passaggio. Ad esempio, è possibile che venga visualizzato un passaggio denominato "Disco di partizione 0" che è l'azione per un passaggio di tipo [Formato e disco partizione](../understand/task-sequence-steps.md#BKMK_FormatandPartitionDisk). Tutti i passaggi della sequenza di attività sono documentati in base al tipo, non necessariamente in base al nome del passaggio visualizzato nell'editor.  

#### <a name="to-edit-a-task-sequence"></a>Per modificare una sequenza di attività  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

3.  Nell'elenco **Sequenza di attività** selezionare la sequenza di attività da modificare.  

4.  Nella scheda **Home** , nel gruppo **Sequenza di attività** , fare clic su **Modifica**e quindi eseguire una delle seguenti operazioni:  

    -   Per aggiungere un passaggio della sequenza di attività, fare clic su **Aggiungi**, selezionare il tipo di passaggio e quindi fare clic sul passaggio della sequenza di attività da aggiungere. Ad esempio, per aggiungere il passaggio Esegui riga di comando, fare clic su **Aggiungi**, selezionare **Generale**e quindi fare clic su **Esegui riga di comando**.  

         Per un elenco di tutti i passaggi della sequenza di attività e dei relativi tipi, vedere la tabella di seguito a questa procedura.  

    -   Per aggiungere un gruppo alla sequenza di attività, fare clic su **Aggiungi**e quindi su **Nuovo gruppo**. Dopo aver aggiunto un gruppo è quindi possibile aggiungere passaggi al gruppo.  

    -   Per modificare l'ordine dei passaggi e dei gruppi nella sequenza di attività, selezionare il passaggio o gruppo da riordinare e quindi usare le icone **Sposta elemento in alto** o **Sposta elemento in basso** . È possibile spostare solo un passaggio o un gruppo alla volta.  

    -   Per rimuovere un passaggio o un gruppo, selezionare il passaggio o il gruppo e fare clic su **Rimuovi**.  

5.  Fare clic su **OK** per salvare le modifiche.  

 Per un elenco dei passaggi della sequenza di attività disponibili, vedere [Passaggi della sequenza di attività](../understand/task-sequence-steps.md).  

## <a name="configure-high-impact-task-sequence-settings"></a>Configurare impostazioni della sequenza di attività ad alto impatto
A partire da Configuration Manager versione 1702, è possibile impostare una sequenza di attività come "ad alto impatto" e personalizzare i messaggi ricevuti dagli utenti quando eseguono la sequenza.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Impostare una sequenza di attività come una sequenza di attività a impatto elevato
Attenersi alla procedura seguente per impostare una sequenza di attività a impatto elevato.
> [!NOTE]
> Qualsiasi sequenza di attività che soddisfi determinate condizioni viene definita automaticamente come a impatto elevato. Per altri dettagli, vedere [Gestire le distribuzioni ad alto rischio](http://docs.microsoft.com/sccm/protect/understand/settings-to-manage-high-risk-deployments).

1. Nella console di Configuration Manager accedere a **Raccolta software** > **Sistemi operativi** > **Sequenze di attività**.
2. Selezionare l'attività da modificare e fare clic su **Proprietà**.
3. Nella scheda **Notifica utente** selezionare **Questa è una sequenza di attività a impatto elevato**.

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Creare una notifica personalizzata per le distribuzioni ad alto rischio
Usare la procedura seguente per creare una notifica personalizzata per le distribuzioni ad alto impatto.
1. Nella console di Configuration Manager accedere a **Raccolta software** > **Sistemi operativi** > **Sequenze di attività**.
2. Selezionare l'attività da modificare e fare clic su **Proprietà**.
3. Nella scheda **Notifica utente** selezionare **Usa il testo personalizzato**.
>  [!NOTE]
>  È possibile impostare il testo della notifica utente solo quando l'opzione **Questa è una sequenza di attività a impatto elevato** è selezionata.

4. Configurare le impostazioni seguenti (massimo 255 caratteri per casella di testo):

  **Testo dell'intestazione della notifica all'utente**: specifica il testo blu che viene visualizzato nella notifica utente di Software Center. Ad esempio, nella notifica utente predefinita questa sezione contiene un testo simile a "Confermare l'aggiornamento del sistema operativo in questo computer".

  **Testo del messaggio di notifica all'utente**: sono presenti tre caselle di testo che specificano il corpo della notifica personalizzata. Tutte le caselle di testo richiedono l'aggiunta di testo.
  - Prima casella di testo: specifica il corpo principale del testo, in genere contenente le istruzioni per l'utente. Ad esempio, nella notifica utente predefinita questa sezione contiene un testo simile a "L'aggiornamento del sistema operativo potrebbe durare a lungo e richiedere più riavvii del computer".
  - Seconda casella di testo: specifica il testo in grassetto nel corpo principale del testo. Ad esempio, nella notifica utente predefinita questa sezione contiene un testo simile a "Questo aggiornamento sul posto installa il nuovo sistema operativo ed esegue automaticamente la migrazione di app, dati e impostazioni".
  - Terza casella di testo: specifica l'ultima riga di testo in grassetto. Ad esempio, nella notifica all'utente predefinita questa sezione contiene un testo simile a "Fare clic su Installa per iniziare, altrimenti fare clic su Annulla".   

  Si supponga di configurare la notifica personalizzata seguente nelle proprietà.

    ![Notifica personalizzata per una sequenza di attività](..\media\user-notification.png)

    Verrà visualizzato il messaggio di notifica seguente quando l'utente finale apre il programma di installazione da Software Center.

    ![Notifica personalizzata per una sequenza di attività](..\media\user-notification-enduser.png)

### <a name="configure-software-center-properties"></a>Configurare le proprietà di Software Center
Attenersi alla procedura seguente per configurare i dettagli per la sequenza di attività visualizzata in Software Center. Tali dettagli sono solo a scopo informativo.  
1. Nella console di Configuration Manager accedere a **Raccolta software** > **Sistemi operativi** > **Sequenze di attività**.
2. Selezionare l'attività da modificare e fare clic su **Proprietà**.
3. Nella scheda **Generale** sono disponibili le impostazioni seguenti per Software Center:
  - **Riavvio necessario**: consente all'utente di sapere se è necessario un riavvio durante l'installazione.
  - **Dimensioni del download (MB)**: specifica quanti megabyte vengono visualizzati in Software Center per la sequenza di attività.  
  - **Tempo di esecuzione stimato (minuti)**: specifica il tempo di esecuzione stimato in minuti che viene visualizzato in Software Center per la sequenza di attività.

##  <a name="BKMK_DistributeTS"></a> Distribuire il contenuto a cui fa riferimento una sequenza attività  
 Prima che i client eseguano una sequenza di attività che fa riferimento al contenuto, è necessario distribuire tale contenuto ai punti di distribuzione. In qualsiasi momento, è possibile selezionare la sequenza di attività e distribuire il relativo contenuto per creare un nuovo elenco di pacchetti di riferimento per la distribuzione. Se si apportano modifiche alla sequenza di attività con contenuto aggiornato, è necessario ridistribuire il contenuto prima che diventi disponibile ai client. Usare la seguente procedura per distribuire il contenuto a cui fa riferimento una sequenza di attività.  

#### <a name="to-distribute-referenced-content-to-distribution-points"></a>Per distribuire il contenuto con riferimenti ai punti di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

3.  Nell'elenco **Sequenza di attività** selezionare la sequenza di attività da distribuire.  

4.  Nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Distribuisci contenuto** per avviare la Distribuzione guidata contenuto.  

5.  Nella pagina **Generale** verificare che la sequenza di attività corrente sia selezionata per la distribuzione e quindi fare clic su **Avanti**.  

6.  Nella pagina **Contenuto** controllare il contenuto da distribuire, come ad esempio l'immagine di avvio a cui fa riferimento la sequenza di attività, e quindi fare clic su **Avanti**.  

7.  Nella pagina **Destinazione contenuto** specificare le raccolte, il punto di distribuzione o il gruppo di punti di distribuzione in cui distribuire i contenuti della sequenza di attività e quindi fare clic su **Avanti**.  

    > [!IMPORTANT]  
    >  Se la sequenza di attività selezionata fa riferimento a contenuto già distribuito in un punto di distribuzione specifico, tale punto di distribuzione non viene elencato dalla procedura guidata.  

8.  Completare la procedura guidata.  

 È possibile pre-installare il contenuto a cui viene fatto riferimento nella sequenza di attività. Configuration Manager crea un file di contenuto pre-installato e compresso, contenente i file, le relative dipendenze e i metadati associati per il contenuto selezionato. Quindi, è possibile importare manualmente il contenuto in un server del sito, in un sito secondario o in un punto di distribuzione. Per altre informazioni su come pre-installare i file di contenuto, vedere [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkprestagea-use-prestaged-content) (Pre-installare il contenuto).  

##  <a name="BKMK_DeployTS"></a> Distribuire una sequenza di attività  
 Usare la seguente procedura per distribuire una sequenza di attività ai computer in una raccolta.  

> [!WARNING]  
>  È possibile gestire il comportamento relativo alle distribuzioni di sequenze di attività ad alto rischio. Una distribuzione ad alto rischio viene installata automaticamente e può causare risultati imprevisti. Ad esempio, una sequenza di attività con scopo impostato su **Obbligatorio** e che distribuisce un sistema operativo viene considerata come distribuzione ad alto rischio. Per altre informazioni, vedere [Impostazioni per gestire distribuzioni ad alto rischio](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

> [!NOTE]  
>  I messaggi di stato per la distribuzione della sequenza di attività vengono visualizzati nella finestra Messaggio in un sito primario, ma non vengono visualizzati in un sito di amministrazione centrale.  

#### <a name="to-deploy-a-task-sequence"></a>Per distribuire una sequenza di attività  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

3.  Nell'elenco **Sequenza di attività** selezionare la sequenza di attività da distribuire.  

4.  Nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Distribuisci**.  

    > [!NOTE]  
    >  Se l'opzione **Distribuisci** non disponibile, la sequenza di attività presenta un riferimento non valido.  Correggere il riferimento e quindi tentare nuovamente la distribuzione della sequenza di attività.  

5.  Nella pagina **Generale** specificare le seguenti informazioni e quindi fare clic su **Avanti**.  

    -   **Sequenza di attività**: specificare la sequenza di attività da distribuire. Per impostazione predefinita, in questa casella viene visualizzata la sequenza di attività selezionata.  

    -   **Raccolta**: specificare la raccolta contenente i computer che eseguiranno la sequenza di attività.  

         Non distribuire sequenze attività che installano i sistemi operativi nelle raccolte inappropriate, come la raccolta **Tutti i sistemi** . Assicurarsi che la raccolta selezionata contenga solo i computer che si desidera che eseguano la sequenza di attività.  

        > [!NOTE]  
        >  Quando si esegue una distribuzione ad alto rischio, ad esempio quella del sistema operativo, nella finestra **Seleziona raccolta** vengono visualizzate soltanto le raccolte personalizzate che soddisfano le impostazioni di verifica della distribuzione configurate nelle proprietà del sito. Le distribuzioni ad alto rischio sono sempre limitate alle raccolte personalizzate (quelle create dall'utente) e alla racconta predefinita **Computer sconosciuti** . Quando si crea una distribuzione ad alto rischio, non è possibile selezionare una raccolta predefinita quale **Tutti i sistemi**. Deselezionare **Nascondi le raccolte con un numero di membri maggiore della configurazione delle dimensioni minime del sito** per visualizzare tutte le raccolte personalizzate che contengono un numero di client inferiore rispetto alla dimensione massima configurata. Per altre informazioni, vedere [Impostazioni per gestire distribuzioni ad alto rischio](../../protect/understand/settings-to-manage-high-risk-deployments.md).  
        >   
        >  Le impostazioni di verifica della distribuzione sono basate sull'appartenenza attuale della raccolta. Dopo aver distribuito la sequenza di attività, l'appartenenza alla raccolta non viene rivalutata per le impostazioni di distribuzione ad alto rischio.  
        >   
        >  Ad esempio, si supponga di impostare **Dimensione predefinita** su 100 e **Dimensione massima** su 1000. Quando si crea una distribuzione ad alto rischio, nella finestra **Seleziona raccolta** verranno visualizzate solo le raccolte che contengono meno di 100 client. Se si deseleziona l'impostazione **Nascondi le raccolte con un numero di membri maggiore della configurazione delle dimensioni minime del sito**, nella finestra vengono visualizzate le raccolte che includono meno di 1000 client.  
        >   
        >  Quando si seleziona una raccolta che include un ruolo del sito, sono valide le condizioni seguenti:  
        >   
        >  -   Se la raccolta contiene un server di sistema del sito e le impostazioni di verifica della distribuzione sono state configurate in modo da bloccare le raccolte con server di sistema del sito, si verifica un errore e la procedura si arresta.  
        > -   Se la raccolta include un server di sistema del sito e nelle impostazioni di verifica della distribuzione configurate dall'utente viene riportata la presenza di tali server di sistema del sito, se la raccolta supera la dimensione predefinita oppure se la raccolta include un server, nella distribuzione guidata del software verrà visualizzato un messaggio sul rischio elevato dell'operazione. È necessario accettare di creare una distribuzione ad alto rischio, quindi viene creato un messaggio di stato relativo al controllo.  

    -   **Commenti (facoltativo):**: specificare informazioni aggiuntive che descrivono la distribuzione della sequenza di attività.  

6.  Nella pagina **Impostazioni distribuzione** specificare le seguenti informazioni e quindi fare clic su **Avanti**.  

    -   **Scopo**: dall'elenco a discesa scegliere una delle opzioni seguenti:  

        -   **Disponibile**: se si distribuisce la sequenza di attività a un utente, l'utente la vede pubblicata nel Catalogo applicazioni e può richiederla all'occorrenza. Se la sequenza di attività viene distribuita a un dispositivo, l'utente la visualizzerà in Software Center e potrà installarla su richiesta.  

        -   **Richiesto**: la sequenza di attività viene distribuita automaticamente, in base alla pianificazione configurata. Un utente può tuttavia tenere traccia dello stato della distribuzione, a meno che non sia nascosto, e può installare la sequenza di attività prima della scadenza usando Software Center.  

    -   **Distribuisci automaticamente in base alla pianificazione con o senza accesso utente**: questa opzione non è disponibile quando si distribuisce una sequenza di attività.  

    -   **Invia pacchetti di riattivazione**: se lo scopo della distribuzione è impostato su **Richiesto** e questa opzione è selezionata, ai computer verrà inviato un pacchetto di riattivazione prima dell'installazione della distribuzione in modo da riattivare il computer dalla sospensione alla scadenza dell'installazione. Prima di usare questa opzione, i computer e le reti devono essere configurati per riattivazione LAN.  

    -   **Consente a tutti i client che usano una connessione di rete a consumo di scaricare il contenuto una volta raggiunta la scadenza dell'installazione. Se si abilita questa opzione, potrebbe essere addebitato un costo aggiuntivo**: quando una sequenza di attività installa un'applicazione ma non distribuisce un sistema operativo, è possibile specificare se consentire ai client di scaricare il contenuto dopo la scadenza dell'installazione se usano una connessione Internet a consumo. I provider Internet talvolta applicano un addebito per il traffico dati in entrata e in uscita quando si usa una connessione Internet a consumo.  

        > [!NOTE]  
        >  Se l'utilizzo di una connessione Internet a consumo potrebbe funzionare per le sequenze attività che non distribuiscono un sistema operativo, non è supportato.  

    -   **Richiedi l'approvazione dell'amministratore se gli utenti richiedono questa applicazione**: questa opzione non è disponibile quando si distribuisce una sequenza di attività.  

    -   **Rendi disponibile per**: specificare se la sequenza di attività è disponibile per i client di Configuration Manager, i supporti o PXE.  

        > [!IMPORTANT]  
        >  Usare l'impostazione **Solo supporti e PXE (nascosto)** per le distribuzioni sequenza di attività automatiche. Selezionare **Consenti distribuzione automatica del sistema operativo** e impostare la variabile SMSTSPreferredAdvertID come parte del supporto affinché il computer venga avviato automaticamente con la distribuzione senza alcuna interazione da parte dell'utente. Per altre informazioni sulle variabili della sequenza di attività, vedere [Variabili predefinite della sequenza di attività](../understand/task-sequence-built-in-variables.md)  

7.  Nella pagina **Pianificazione** specificare le seguenti informazioni e quindi fare clic su **Avanti**.  

    > [!IMPORTANT]  
    >  Quando un client di Windows PE viene avviato da PXE o da supporti di avvio, il client non valuta le pianificazioni della distribuzione (avvio, scadenza o date di scadenza). Configurare le pianificazioni solo nelle distribuzioni ai client che vengono avviati dal sistema operativo Windows completo. Considerare la possibilità di usare altri metodi, ad esempio le finestre di manutenzione, per controllare le sequenze di attività attive distribuite ai client che vengono avviati da Windows PE.  

    -   **Pianifica quando questa distribuzione diventerà disponibile**: specificare la data e l'ora in cui la sequenza di attività può essere eseguita nel computer di destinazione. Quando si seleziona la casella di controllo **UTC** , questa impostazione assicura che la sequenza di attività sia disponibile per più computer di destinazione contemporaneamente anziché in momenti diversi, in base all'ora locale dei computer di destinazione.  

         Se l'ora di avvio è precedente rispetto al tempo necessario, il client scarica la sequenza di attività all'ora di avvio specificata.  

    -   **Pianifica alla scadenza di questa assegnazione**: specificare la data e l'ora di scadenza della sequenza di attività nel computer di destinazione. Quando si seleziona la casella di controllo **UTC** , questa impostazione assicura che la sequenza di attività scada in più computer di destinazione contemporaneamente anziché in momenti diversi, in base all'ora locale dei computer di destinazione.  

    -   **Pianificazione assegnazione**: specificare quando la sequenza di attività richiesta viene eseguita nel computer di destinazione. È possibile aggiungere più pianificazioni.  

         È possibile specificare la data e l'ora in cui inizia la pianificazione, se la sequenza di attività viene eseguita settimanalmente, mensilmente o a un intervallo personalizzato e se viene eseguita dopo un evento come l'accesso o la disconnessione dal computer.  

        > [!NOTE]  
        >  Se si pianifica un'ora di avvio per una sequenza di attività richiesta precedente alla data e all'ora in cui è disponibile la sequenza di attività, il client di Configuration Manager scarica la sequenza di attività all'ora di avvio pianificata anche se la sequenza di attività è disponibile a un'ora precedente.  

    -   **Riesegui comportamento**: specificare quando viene eseguita nuovamente la sequenza di attività. È possibile specificare una delle opzioni seguenti.  

        -   **Non rieseguire mai un programma distribuito**: la sequenza di attività non viene rieseguita nel client se è già stata eseguita in precedenza nel client. Anche se si sono originariamente verificati errori o se sono stati modificati i file della sequenza di attività, la sequenza di attività non viene rieseguita.  

        -   **Riesegui sempre un programma**: la sequenza di attività viene rieseguita sempre nel client quando si pianifica la distribuzione, anche se è stata eseguita correttamente in precedenza. Questa impostazione è particolarmente utile quando si usano distribuzioni ricorrenti in cui la sequenza di attività viene regolarmente aggiornata.  

            > [!IMPORTANT]  
            >  Anche se questa opzione è impostata per impostazione predefinita, non produce alcun effetto fino a quando non si assegna una distribuzione necessaria. Le distribuzioni disponibili possono sempre essere rieseguite da un utente.  

        -   **Riesegui se il tentativo precedente non è riuscito**: la sequenza di attività viene rieseguita quando la distribuzione è pianificata solo se la sequenza di attività non è stata eseguita correttamente in precedenza. Questa impostazione è particolarmente utile per le distribuzioni richieste in modo che se ne ritenterà automaticamente l'esecuzione in base alla pianificazione assegnazione se l'ultimo tentativo non è andato a buon fine.  

        -   Riesegui se il tentativo precedente è riuscito: la sequenza di attività viene rieseguita solo se è stata eseguita correttamente in precedenza nel client. Questa impostazione è utile quando di usano distribuzioni ricorrenti in cui la sequenza di attività viene regolarmente aggiornata e ogni aggiornamento richiede che quello precedente sia installato correttamente.  

        > [!NOTE]  
        >  Poiché un utente può rieseguire la distribuzione di una sequenza di attività disponibile, prima di distribuire una sequenza di attività disponibile nell'ambiente di un prodotto, assicurarsi di valutare e testare attentamente cosa accade se un utente riesegue la sequenza di attività più volte.  

8.  Nella pagina **Esperienza utente** specificare le seguenti informazioni, quindi fare clic su **Avanti**.  

    -   **Consenti all'utente di eseguire il programma indipendentemente dalle assegnazioni:**: specificare se l'utente è autorizzato a eseguire una sequenza di attività necessaria in modo indipendente dalle assegnazioni distribuzione.  

    -   **Mostra stato sequenza di attività**: specificare se il client di Configuration Manager visualizza lo stato di avanzamento della sequenza di attività.  

    -   **Installazione software**: specificare se l'utente è autorizzato a installare il software al di fuori di una finestra di manutenzione configurata dopo l'orario pianificato.  

    -   **Riavvio del sistema (se necessario per completare l'installazione)**: specificare se l'utente è autorizzato a riavviare il computer dopo l'installazione software al di fuori di una finestra di manutenzione configurata dopo il periodo di assegnazione.  

    -   **Consenti l'esecuzione della sequenza di attività per il client in Internet:** specificare se la sequenza di attività può essere eseguita in un client basato su Internet rilevato come presente su Internet da Configuration Manager. Le operazioni di installazione di software, quale un sistema operativo, non sono supportate con questa impostazione. Usare questa opzione solo per le sequenze attività generiche basate su script che eseguono operazioni nel sistema operativo standard.  

9. Nella pagina **Avvisi** specificare le impostazioni di avviso desiderate per la distribuzione di questa sequenza di attività e quindi fare clic su **Avanti**.  

10. Nella pagina **Punti di distribuzione** specificare le informazioni seguenti e quindi fare clic su **Avanti**.  

    -   **Opzioni di distribuzione:**specificare una delle opzioni seguenti:  

        > [!NOTE]  
        >  Quando si usa il multicast per distribuire un sistema operativo, il contenuto deve essere scaricato nei computer di destinazione quando necessario oppure prima dell'esecuzione della sequenza di attività.  

        -   Specificare che i client scaricano contenuto dal punto di distribuzione nel computer di destinazione come richiesto dalla sequenza di attività.  

        -   Specificare che i client scaricano tutto il contenuto dal punto di distribuzione nel computer di destinazione prima dell'esecuzione della sequenza di attività. Questa opzione non viene visualizzata se si è specificato che la sequenza di attività è disponibile nelle distribuzioni PXE e dei supporti di avvio (vedere la pagina **Impostazioni distribuzione** ).  

        -   Specificare che i client eseguono il contenuto dal punto di distribuzione. Questa opzione è disponibile solo quando tutti i pacchetti associati con la sequenza di attività vengono abilitati all'utilizzo di una condivisione pacchetto nel punto di distribuzione. Per abilitare il contenuto all'utilizzo di una condivisione pacchetto, vedere la scheda **Accesso dati** nelle **Proprietà** di ciascun pacchetto.  

    -   **Utilizzare un punto di distribuzione remoto quando non sono disponibili punti di distribuzione locali**: specificare se i client possono scaricare il contenuto necessario per la sequenza di attività da punti di distribuzione disponibili in reti lente e inaffidabili.  

11. Completare la procedura guidata.  

##  <a name="BKMK_ExportImport"></a> Esportare e importare sequenze di attività  
 È possibile esportare e importare sequenze attività con o senza i relativi oggetti, come un'immagine del sistema operativo, un'immagine di avvio, un pacchetto dell'agente client, un pacchetto driver e applicazioni con dipendenze.  

 Considerare quanto segue quando si esportano e importano sequenze attività.  

-   Le password memorizzate nella sequenza di attività non vengono esportate. Se si esporta e importa una sequenza di attività che contiene password, è necessario modificare la sequenza di attività importata e specificare nuovamente le password. Assicurarsi di specificare le password per le azioni [Aggiunta a dominio o gruppo di lavoro](../understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup), [Connetti alla cartella di rete](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) ed [Esegui riga di comando](../understand/task-sequence-steps.md#BKMK_RunCommandLine) .  

- Quando si esporta una sequenza di attività con il passaggio **Imposta variabili dinamiche**, per le variabili che sono configurate con l'impostazione **Valore segreto** non vengono esportati valori. È necessario immettere nuovamente i valori per tali variabili dopo aver importato la sequenza di attività.

-   Quando si dispone di più siti primari, è consigliabile importare sequenze attività nel sito di amministrazione centrale.  

 Usare le procedure seguenti per esportare e importare una sequenza di attività.  

#### <a name="to-export-task-sequences"></a>Per esportare sequenze attività  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

3.  Nell'elenco **Sequenza di attività** , selezionare le sequenze attività che si desidera esportare. Se si seleziona più di una sequenza di attività, queste vengono memorizzate in un file di esportazione.  

4.  Nella scheda **Home** del gruppo **Sequenza di attività** , fare clic su **Esporta** per avviare l'Esportazione guidata della sequenza di attività.  

5.  Nella pagina **Generale** specificare le seguenti impostazioni, quindi fare clic su **Avanti**.  

    -   Nella casella **File** specificare il percorso e il nome del file di esportazione. Se si immette direttamente il nome del file, assicurarsi di includere l'estensione .zip nel nome del file. Se si seleziona il file di esportazione, la procedura guidata aggiunge automaticamente questa estensione del nome del file.  

    -   Deselezionare la casella di controllo **Esporta tutte le dipendenze della sequenza di attività** se non si desiderano esportare le dipendenze della sequenza di attività. Per impostazione predefinita, la procedura guidata esegue la scansione di tutti gli oggetti correlati e li esporta con la sequenza di attività. Include tutte le dipendenze per le applicazioni.  

    -   Deselezionare la casella di controllo **Esporta tutti i contenuti per le sequenze attività selezionate e le dipendenze** se non si desidera copiare il contenuto dall'origine del pacchetto al percorso di esportazione. Se questa casella di controllo è selezionata, l'Importazione guidata della sequenza di attività usa il percorso di importazione come nuovo percorso di origine del pacchetto.  

    -   Nella casella **Commenti amministratore** aggiungere una descrizione delle sequenze attività da esportare.  

6.  Completare la procedura guidata.  

 La procedura guidata crea i seguenti file di output:  

-   Se non si esporta contenuto: un file compresso.  

-   Se si esporta contenuto: un file compresso e una cartella denominata *export*_files, in cui *export* è il nome del file compresso che contiene il contenuto esportato.  

 Se si include del contenuto quando si esporta una sequenza di attività, assicurarsi di copiare il file .zip e la cartella *export*_files, altrimenti l'importazione non avrà esito positivo.  

#### <a name="to-import-task-sequences"></a>Per importare sequenze attività  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

3.  Nella scheda **Home** del gruppo **Crea** fare clic su **Importa sequenza di attività** per avviare l'Importazione guidata della sequenza di attività.  

4.  Nella pagina **Generale** specificare il file .zip esportato, quindi fare clic su **Avanti**.  

5.  Nella pagina **Contenuto file** , selezionare l'azione richiesta per ogni oggetto da importare. In questa pagina sono visualizzati tutti gli oggetti che verranno importati da Configuration Manager.  

    -   Se l'oggetto non è mai stata importato, selezionare **Crea nuovo**.  

    -   Se l'oggetto è stato importato in precedenza, selezionare una delle seguenti azioni:  

        -   **Ignorare duplicato** (predefinito): questa azione non importa l'oggetto. Al contrario, la procedura guidata collega l'oggetto esistente alla sequenza di attività.  

        -   **Sovrascrivi**: questa azione sovrascrive l'oggetto esistente con l'oggetto importato. Per le applicazioni, è possibile aggiungere una revisione per aggiornare l'applicazione esistente o creare una nuova applicazione.  

6.  Completare la procedura guidata.  

 Dopo aver importato la sequenza di attività, modificarla per specificare le password che erano presenti nella sequenza di attività originale. Per motivi di sicurezza, le password non vengono esportate.  

##  <a name="BKMK_CreateTSVariables"></a> Creare le variabili della sequenza di attività per computer e raccolte  
 È possibile definire variabili della sequenza di attività personalizzate per computer e insiemi. Le variabili definite per un computer vengono definite variabili della sequenza di attività con ambito computer. Le variabili definite per una raccolta vengono definite variabili della sequenza di attività con ambito raccolta. Se si verifica un conflitto, le variabili con ambito computer hanno la precedenza sulle variabili con ambito raccolta. Questo significa che le variabili della sequenza di attività assegnate a un computer specifico assumono automaticamente una priorità maggiore di quelle assegnate alla raccolta che contiene il computer.  

 Se ad esempio alla raccolta ABC è assegnata una variabile e al computer XYZ, membro della raccolta ABC, è assegnata una variabile con lo stesso nome, la variabile assegnata al computer XYZ avrà priorità maggiore rispetto a quella assegnata alla raccolta ABC.  

 Se si vuole che le variabili con ambito computer e raccolta non siano visibili nella console di Configuration Manager, è possibile nasconderle. Se si desidera che tali variabili non siano più nascoste, sarà necessario eliminarle e ridefinirle senza selezionare l'opzione per nasconderle. Quando si usa l'opzione **Non visualizzare questo valore nella console di Configuration Manager**, il valore della variabile non viene visualizzato, ma può essere usato dalla sequenza di attività quando viene eseguita.  

 È possibile gestire le variabili per computer in un sito primario oppure in un sito di amministrazione centrale. Configuration Manager non supporta più di 1.000 variabili assegnate per computer.  

> [!WARNING]  
>  Quando si usano variabili con ambito raccolta per le sequenze attività, considerare quanto segue:  
>   
>  -   Poiché le modifiche alle raccolte vengono sempre replicate in tutta la gerarchia, qualsiasi modifica apportata alle variabili raccolta verrà applicata non solo ai membri del sito corrente ma a tutti i membri della raccolta in tutta la gerarchia.  
> -   Quando si elimina una raccolta, questa azione elimina anche le variabili della sequenza di attività configurate per la raccolta.  

 Usare le procedure seguenti per creare variabili della sequenza di attività per un computer o per una raccolta.  

#### <a name="to-create-task-sequence-variables-for-a-computer"></a>Per creare variabili della sequenza di attività per un computer  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** espandere la raccolta che contiene il computer al quale si desidera aggiungere la variabile.  

3.  Selezionare il computer e fare clic su **Proprietà**.  

4.  Nella finestra di dialogo **Proprietà** scegliere la scheda **Variabili** .  

5.  Per ogni variabile da creare, fare clic sull'icona **Nuova** nella finestra di dialogo **<Nuova\> variabile** e specificare il nome e il valore della variabile della sequenza di attività. Deselezionare la casella di controllo **Non visualizzare questo valore nella console di Configuration Manager** se si vuole nascondere le variabili in modo che non vengano riportate nella console di Configuration Manager.  

6.  Dopo aver aggiunto tutte le variabili per il computer, fare clic su **OK**.  

#### <a name="to-create-task-sequence-variables-for-a-collection"></a>Per creare variabili della sequenza di attività per una raccolta  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** selezionare la raccolta alla quale si desidera aggiungere la variabile e fare clic su **Proprietà**.  

3.  Nella finestra di dialogo **Proprietà** fare clic sulla scheda **Variabili raccolta** .  

4.  Per ogni variabile da creare, fare clic sull'icona **Nuova** nella finestra di dialogo **<Nuova\> variabile** e specificare il nome e il valore della variabile della sequenza di attività. Deselezionare la casella di controllo **Non visualizzare questo valore nella console di Configuration Manager** se si vuole nascondere le variabili in modo che non vengano riportate nella console di Configuration Manager.  

5.  È inoltre possibile specificare la priorità in base alla quale Configuration Manager valuterà le variabili della sequenza di attività.  

6.  Dopo aver aggiunto tutte le variabili alla raccolta, fare clic su **OK**.  

##  <a name="BKMK_AdditionalActionsTS"></a> Azioni aggiuntive per la gestione delle sequenze di attività  
 È possibile gestire le sequenze attività usando le azioni aggiuntive disponibili quando si seleziona la sequenza di attività usando la procedura seguente.  

#### <a name="to-select-a-task-sequence-to-manage"></a>Per selezionare una sequenza di attività da gestire  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi** , quindi fare clic su **Sequenze attività**.  

3.  Nell'elenco **Sequenza di attività** selezionare la sequenza di attività che si desidera gestire e quindi selezionare una delle opzioni disponibili.  

 Usare la tabella riportata di seguito per ulteriori informazioni su alcune delle azioni aggiuntive per la gestione delle sequenze attività.  

|Azione|Descrizione|  
|------------|-----------------|  
|**Copia**|Crea una copia della sequenza di attività selezionata. Questa azione può risultare utile quando si desidera creare una nuova sequenza di attività basata su una sequenza di attività esistente.<br /><br /> Quando si copia una sequenza di attività in una cartella, la copia viene elencata in tale cartella fino all'aggiornamento del nodo sequenza di attività.  Dopo l'aggiornamento, la copia viene visualizzata nella cartella principale.|  
|**Disabilitato**|Disattiva la sequenza di attività in modo che non possa essere eseguita nei computer. Le sequenze attività disattivate possono essere distribuite ai computer, ma questi non le eseguono finché non vengono attivate.|  
|**Attiva**|Attiva la sequenza di attività in modo che possa essere eseguita. Dopo l'attivazione non è necessario ridistribuire una sequenza di attività già distribuita.|  
|**Crea file di contenuto pre-installazione**|Avvia la Creazione guidata file di contenuto pre-installazione per pre-installare il contenuto della sequenza di attività. Per informazioni su come creare un file di contenuto pre-installato, vedere [Prestage content](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkprestagea-use-prestaged-content) (Pre-installare il contenuto).|  
|**Sposta**|Sposta la sequenza di attività selezionata in un'altra cartella.|  
|**Proprietà**|Apre la finestra di dialogo **Proprietà** per la sequenza di attività selezionata. Usare questa finestra di dialogo per modificare il comportamento dell'oggetto sequenza di attività. Non è possibile usare questa finestra di dialogo per modificare i passaggi della sequenza di attività.|  

## <a name="next-steps"></a>Passaggi successivi
[Scenari di distribuzione di sistemi operativi aziendali](scenarios-to-deploy-enterprise-operating-systems.md)


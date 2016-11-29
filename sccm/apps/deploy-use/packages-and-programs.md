---
title: Pacchetti e programmi | System Center Configuration Manager
description: Supportare le distribuzioni che usano pacchetti e programmi o applicazioni con System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: caad0507-9913-415a-b13d-d36f8f0a1b80
caps.latest.revision: 8
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 5303edf0fe8a3e322b52cabd116b1877a14f8821


---
# <a name="packages-and-programs-in-system-center-configuration-manager"></a>Pacchetti e programmi in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager continua a supportare pacchetti e programmi usati in Configuration Manager 2007. Una distribuzione che usa pacchetti e programmi può essere più adatta rispetto a una che usa un'applicazione quando si distribuisce uno degli elementi seguenti:  

- Si vuole distribuire applicazioni ai server Linux e UNIX.  
- Script che non installano un'applicazione su un computer, ad esempio uno script per deframmentare l'unità disco del computer.  
- Script "One-off" che non è necessario monitorare costantemente.  
- Script eseguiti in base a una pianificazione ricorrente e che non possono usare la valutazione globale.  
  
Quando si esegue la migrazione di pacchetti da una versione precedente di Configuration Manager, è possibile distribuirli nella gerarchia di Configuration Manager. Al termine della migrazione, i pacchetti vengono visualizzati nel nodo **Pacchetti** dell'area di lavoro **Raccolta software** . È possibile modificare e distribuire questi pacchetti allo stesso modo dei casi in cui è stata usata la distribuzione del software. L'**Importazione guidata da definizione** rimane in Configuration Manager per importare pacchetti legacy. Gli annunci vengono convertiti in distribuzioni quando vengono migrati da Configuration Manager 2007 a una gerarchia di Configuration Manager.  
  
> [!NOTE]  
>  È possibile usare Microsoft System Center Configuration Manager Package Conversion Manager per convertire i pacchetti e i programmi in applicazioni di Configuration Manager.  
>   
>  Per altre informazioni, vedere [Configuration Manager Package Conversion Manager](https://technet.microsoft.com/library/hh531519.aspx).  

I pacchetti possono usare alcune nuove funzionalità di Configuration Manager, inclusi i gruppi di punti di distribuzione e il monitoraggio. Le applicazioni Microsoft Application Virtualization (App-V) non possono essere distribuite usando pacchetti e programmi in Configuration Manager. Per distribuire applicazioni virtuali, è necessario crearle come applicazioni di Configuration Manager.  

##  <a name="create-a-package-and-program"></a>Creare un pacchetto e un programma  
 Usare una di queste procedure per creare o importare pacchetti e programmi.  

### <a name="create-a-package-and-program-using-the-create-package-and-program-wizard"></a>Creare un pacchetto e un programma tramite la Creazione guidata pacchetto e programma  

1.  Nella console di Configuration Manager fare clic su **Raccolta software ** > **Gestione applicazioni** > **Pacchetti**.  

3.  Nel gruppo **Crea** della scheda **Home** fare clic su **Crea pacchetto**.  

4.  Nella pagina **Pacchetto** della Creazione guidata pacchetto e programma specificare le informazioni seguenti:  

    -   **Nome** - Specificare un nome per il pacchetto con un massimo di 50 caratteri.  

    -   **Descrizione** - Specificare una descrizione per il pacchetto con un massimo di 128 caratteri (facoltativo).  

    -   **Produttore**: specificare facoltativamente il nome di un produttore per identificare il pacchetto nella console di Configuration Manager. Il nome non può contenere più di 32 caratteri.  

    -   **Lingua** - Specificare la lingua del pacchetto con un massimo di 32 caratteri (facoltativo).  

    -   **Versione** - Specificare un numero di versione del pacchetto con un massimo di 32 caratteri (facoltativo).  

    -   **Questo pacchetto contiene file di origine** - Questa impostazione indica se il pacchetto richiede che nei dispositivi client siano presenti file di origine. Per impostazione predefinita, questa casella di controllo non è selezionata e Configuration Manager non usa i punti di distribuzione per il pacchetto. Se questa casella di controllo è selezionata, vengono usati punti di distribuzione.  

    -   **Cartella di origine** - Se il pacchetto contiene file di origine, fare clic su **Sfoglia** per aprire la finestra di dialogo **Imposta cartella di origine** e specificare il percorso dei file di origine per il pacchetto.  

        > [!NOTE]  
        >  L'account computer del server del sito deve avere autorizzazioni di accesso in lettura alla cartella specificata.  

5.  Nella pagina **Tipo di programma** della Creazione guidata pacchetto e programma selezionare il tipo di programma da creare e quindi fare clic su **Avanti**. È possibile creare un programma per un computer o un dispositivo oppure ignorare questo passaggio e creare un programma in un secondo momento.  

    > [!TIP]  
    >  Per creare un nuovo programma per un pacchetto esistente, selezionare il pacchetto e quindi nel gruppo **Pacchetto** della scheda **Home** fare clic su **Crea programma** per aprire la Creazione guidata programma.  

6.  Per creare un programma standard o un programma di dispositivo, usare una delle procedure seguenti.  
  
    #### <a name="create-a-standard-program"></a>Creare un programma standard  
  
  1.  Sul **tipo di programma** pagina del **Creazione guidata pacchetto e programma**, selezionare **programma Standard**, quindi fare clic su **successivo**.     2.  Nella pagina **Programma standard**, specificare quanto segue:  

        -   **Nome:** Specificare un nome per il programma con un massimo di 50 caratteri.  

            > [!NOTE]  
            >  Il nome del programma deve essere univoco all'interno di un pacchetto. Dopo aver creato un programma, è possibile modificare il relativo nome.  

        -   **Riga di comando** - Immettere la riga di comando da usare per avviare il programma oppure fare clic su **Sfoglia** per accedere al percorso del file.  

             Se per un nome di file non è specificata l'estensione, Configuration Manager prova a usare com, exe e bat come possibili estensioni.  

             Se il programma viene eseguito in un client, Configuration Manager cerca prima il nome del file della riga di comando all'interno del pacchetto, successivamente cerca nella cartella Windows locale e infine nel *%percorso%* locale. Se il file non può essere trovato, l'esecuzione del programma non riesce.  

        -   **Cartella Esecuzione automatica** - Usare questo campo per specificare la cartella da cui viene eseguito il programma, con un massimo di 127 caratteri (facoltativo). Questa cartella può essere un percorso assoluto nel client o un percorso relativo della cartella del punto di distribuzione contenente il pacchetto.  

        -   **Esegui** - Specifica la modalità di esecuzione del programma nei computer client. Selezionare una delle operazioni seguenti:  

            -   **Normale** -il programma viene eseguito in modalità normale in base alle impostazioni predefinite del sistema e del programma. Questa è la modalità predefinita.  

            -   **Ridotta a icona** – viene eseguito il programma ridotto a icona su dispositivi client. Gli utenti potrebbero visualizzare attività di installazione nell'area di notifica o sulla barra delle applicazioni.  

            -   **Ingrandita** – viene eseguito il programma ingrandito sui dispositivi client. Gli utenti vedranno tutta l'attività di installazione.  

            -   **Hidden** : l'esecuzione del programma nascosta sui dispositivi client. Gli utenti non visualizzeranno alcuna attività di installazione.  

        -   **Requisiti per esecuzione programma** - Specificare se il programma può essere eseguito solo quando un utente è connesso, quando nessun utente è connesso o indipendentemente dal fatto che un utente sia o meno connesso al computer client.  

        -   **Modalità esecuzione** - Specificare se il programma verrà eseguito con autorizzazioni amministrative o con le autorizzazioni dell'utente attualmente connesso.  

        -   **Consenti agli utenti di visualizzare e interagire con l'installazione del programma** - Usare questa impostazione, se disponibile, per specificare se permettere agli utenti di interagire con l'installazione del programma. Questa casella di controllo è disponibile solo se sono selezionate le opzioni **Solo se nessun utente è connesso** o **Indipendentemente dalla connessione degli utenti** per **Requisiti per esecuzione programma** e **Esegui con diritti amministrativi** per **Modalità esecuzione**.  

        -   **Modalità unità** - Specificare le informazioni sul modo in cui il programma verrà eseguito in rete. Scegliere uno dei valori seguenti:  

            -   **Viene eseguito con il nome UNC** -indica che il programma viene eseguito con un nome (Universal Naming Convention). Questa è l'impostazione predefinita.  

            -   **Richiede lettera di unità** -indica che il programma richiede una lettera di unità per qualificare completamente il relativo percorso. Per questa impostazione, Configuration Manager può usare qualsiasi lettera di unità disponibile nel client.  

            -   **Richiede una lettera di unità specifica (esempio: Z:)** -indica che il programma richiede una lettera di unità specifico per qualificare completamente il relativo percorso specificato. Se la lettera di unità specificata è già utilizzata in un client, il programma non viene eseguito.  

        -   **Riconnettersi al punto di distribuzione log** -utilizzare questa casella di controllo per indicare se il computer client si riconnette al punto di distribuzione quando l'utente accede. Per impostazione predefinita, questa casella di controllo è deselezionata.  

  3.  Nel **requisiti** pagina della creazione guidata pacchetto e programma, specificare le seguenti informazioni:  

        -   **Esegui prima un altro programma** : È possibile utilizzare questa impostazione per identificare un pacchetto e programma che verrà eseguito prima di questo pacchetto e programma verrà eseguito.  

        -   **Requisiti di piattaforma** - Selezionare **Questo programma può essere eseguito in qualsiasi piattaforma** o **Questo programma può essere eseguito solo in piattaforme specifiche** e quindi scegliere i sistemi operativi che i client devono eseguire per poter installare il pacchetto e il programma.  

        -   **Spazio su disco stimato** - Specificare la quantità di spazio su disco necessaria per l'esecuzione del programma software nel computer. È possibile specificare **Sconosciuto** (impostazione predefinita) o un numero intero maggiore o uguale a zero. Se si specifica un valore, è necessario specificare anche l'unità di misura per il valore.  

        -   **Tempo di esecuzione massimo consentito (minuti)** - Specificare la durata massima di esecuzione prevista per il programma sul computer client. È possibile specificare **Sconosciuto** (impostazione predefinita) o un numero intero maggiore di zero.  

             Per impostazione predefinita, il valore è impostato su 120 minuti.  

            > [!IMPORTANT]  
            >  Se si utilizza finestre di manutenzione per la raccolta in cui viene eseguito questo programma, potrebbe verificarsi un conflitto se il **tempo esecuzione massimo consentito** è più lungo rispetto alla finestra di manutenzione pianificata. Tuttavia, se il numero massimo di esecuzione viene impostato su **sconosciuto**, il programma verrà avviato da eseguire durante la finestra di manutenzione e continuerà a essere eseguito in base alle esigenze dopo aver chiuso la finestra di manutenzione. Se l'utente imposta il limite massimo di esecuzione per un periodo specifico che supera la lunghezza di qualsiasi finestra di manutenzione disponibile, il programma non essere eseguito.  

             Se il valore impostato è **Sconosciuto**, Configuration Manager imposta un limite massimo di 12 ore (720 minuti).  

            > [!NOTE]  
            >  Se il tempo di esecuzione massimo (indipendentemente dal fatto che sia stato impostato dall'utente o che si tratti del valore predefinito) viene superato, Configuration Manager arresta il programma se l'opzione **Esegui con diritti amministrativi** è selezionata e l'opzione **Consenti agli utenti di visualizzare e interagire con l'installazione del programma** non è selezionata.  

  4.  Fare clic su **Avanti**.  
  
    #### <a name="create-a-device-program"></a>Creare un programma di dispositivo  
  
  1.  Sul **tipo di programma** pagina del **Creazione guidata pacchetto e programma**, selezionare **programma per dispositivo**, quindi fare clic su **successivo**.  

  2.  Nella pagina **Programma standard** specificare quanto segue:  

        -   **Nome**: specificare un nome per il programma usando massimo 50 caratteri.  

            > [!NOTE]  
            >  Il nome del programma deve essere univoco all'interno di un pacchetto. Dopo aver creato un programma, non è possibile modificarne il nome.  

        -   **Commento** - Specificare un commento per il programma per dispositivo con un massimo di 127 caratteri (facoltativo).  

        -   **Cartella download** - Specificare il nome della cartella nel dispositivo Windows CE in cui verranno archiviati i file di origine del pacchetto. Il valore predefinito è **\Temp\\**.  

        -   **Riga di comando** - Immettere la riga di comando da usare per avviare il programma oppure fare clic su **Sfoglia** per accedere al percorso del file.  

        -   **Esegui la riga di comando nella cartella download** - Selezionare questa opzione per eseguire il programma dalla cartella di download specificata in precedenza.  

        -   **Esegui la riga di comando da questa cartella** - Selezionare questa opzione per specificare una cartella diversa da cui eseguire il programma.  

    3.  Nella pagina **Requisiti**, specificare quanto segue:  

        -   **Spazio su disco stimato** - Specificare la quantità di spazio su disco necessaria per il software. Questo valore verrà visualizzato agli utenti dei dispositivi mobili prima di installare il programma.  

        -   **Programma download** - Specificare le informazioni relative al momento in cui il programma può essere scaricato nei dispositivi mobili. È possibile specificare **Appena possibile**, **Solo su una rete veloce**o **Solo quando un dispositivo è bloccato**.  

        -   **Altri requisiti** - Specificare eventuali requisiti aggiuntivi per il programma. I requisiti verranno visualizzati agli utenti prima di installare il software. Ad esempio, è possibile inviare una notifica agli utenti che devono essere chiuse tutte le altre applicazioni prima di eseguire il programma.  

  4.  Fare clic su **Avanti**.  

  7.  Nella pagina **Riepilogo**, esaminare le azioni da eseguire e completare la procedura guidata.  

 Verificare che i nuovi pacchetto e programma vengano visualizzati nel nodo **Pacchetti** dell'area di lavoro **Raccolta software** .  

## <a name="create-a-package-and-program-from-a-package-definition-file"></a>Per creare un pacchetto e un programma da un file di definizione del pacchetto  

1.  Nella console di Configuration Manager fare clic su **Raccolta software ** > **Gestione applicazioni** > **Pacchetti**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea pacchetto da definizione**.  

4.  Nella pagina **Definizione pacchetto** della Creazione guidata pacchetto da definizione scegliere un file di definizione del pacchetto esistente oppure fare clic su **Sfoglia** per aprirne uno nuovo. Dopo aver specificato un nuovo file di definizione del pacchetto, selezionarlo nell'elenco **Definizione pacchetto** e quindi fare clic su **Avanti**.  

5.  Nella pagina **File di origine** specificare le informazioni su tutti i file di origine necessari per il pacchetto e per il programma e fare clic su **Avanti**.  

6.  Se il pacchetto richiede file di origine, nella pagina **Cartella di origine** specificare il percorso da cui devono essere ottenuti i file di origine e fare clic su **Avanti**.  

7.  Nella pagina **Riepilogo** esaminare le azioni da eseguire e completare la procedura guidata. I nuovi pacchetto e programma vengono visualizzati nel nodo **Pacchetti** dell'area di lavoro **Raccolta software** .  

 Per altre informazioni sui file definizioni del pacchetto, vedere [Informazioni sul formato di file definizioni del pacchetto](/sccm/apps/deploy-use/packages-and-programs#about-the-package-definition-file-format) in questo argomento.  

##  <a name="deploy-packages-and-programs"></a>Distribuire pacchetti e programmi  

1.  Nella console di Configuration Manager fare clic su **Raccolta software ** > **Gestione applicazioni** > **Pacchetti**.  

3.  Selezionare il pacchetto che si desidera distribuire, quindi nel **Home** nella scheda il **distribuzione** di gruppo, fare clic su **Distribuisci**.  

4.  Nel **Generale** pagina della distribuzione guidata del Software, specificare il nome del pacchetto e programma che si desidera distribuire, la raccolta a cui si desidera distribuire il pacchetto e programma e i commenti facoltativi per la distribuzione.  

     Selezionare **utilizzare gruppi di punti di distribuzione predefiniti associati a questa raccolta** se si desidera archiviare il contenuto del pacchetto nel gruppo di punto di distribuzione predefinito di raccolte. Se la raccolta selezionata non è stata associata ad alcun gruppo di punti di distribuzione, questa opzione non sarà disponibile.  

5.  Nella pagina **Contenuto** fare clic su **Aggiungi** e selezionare i punti di distribuzione o i gruppi di punti di distribuzione a cui si vuole distribuire il contenuto associato a questo programma e pacchetto.  

6.  Nella pagina **Impostazioni distribuzione** scegliere uno scopo per la distribuzione e specificare le opzioni per i pacchetti di riattivazione e le connessioni a consumo:  

    -   **Scopo** - È possibile scegliere tra:  

        -   **Disponibile** -se l'applicazione viene distribuita a un utente, l'utente vede il pacchetto pubblicato e il programma nel catalogo applicazioni e può richiederla all'occorrenza. Se il pacchetto e il programma viene distribuito in un dispositivo, l'utente visualizzerà in Software Center e potrà installarla su richiesta.  

        -   **Necessari** -pacchetto e programma viene distribuita automaticamente, in base alla pianificazione configurata. Tuttavia, un utente può tenere traccia dello stato di distribuzione del pacchetto e programma e installarlo prima della scadenza utilizzando Software Center.  

    -   **Inviare pacchetti di riattivazione** : se lo scopo della distribuzione è impostato su **necessari** e questa opzione è selezionata, verrà inviato un pacchetto di riattivazione ai computer prima dell'installazione della distribuzione per riattivare il computer da sospensione alla scadenza dell'installazione. Prima di poter utilizzare questa opzione, i computer devono essere configurati per la riattivazione LAN.  

    -   Se richiesto, selezionare **Consente a tutti i client che usano una connessione di rete a consumo di scaricare il contenuto una volta raggiunta la scadenza dell'installazione. Se si abilita questa opzione, può essere addebitato un costo aggiuntivo**.  

    > [!NOTE]  
    >  L'opzione **Pre-distribuisci il software nel dispositivo primario dell'utente** non è disponibile durante la distribuzione di un pacchetto e di un programma.  

7.  Nella pagina **Pianificazione** configurare la data e l'ora in cui pacchetto e programma verranno distribuiti o resi disponibili per i dispositivi client.  

     Le opzioni presenti in questa pagina varieranno a seconda che l'azione di distribuzione sia impostata su **Disponibile** o **Richiesto**.  

8.  Se lo scopo della distribuzione è impostato su **necessari**, configurare il comportamento del programma da eseguire di nuovo il **Riesegui comportamento** elenco a discesa. Scegliere le opzioni seguenti:  

    |Riesegui comportamento|Altre informazioni|  
    |--------------------|----------------------|  
    |Non rieseguire mai un programma distribuito|Il programma di non essere rieseguito sul client, anche se il programma di origine non riuscita o vengono modificati i file di programma.|  
    |Riesegui sempre un programma|Il programma verrà sempre eseguiti nuovamente sul client quando si pianifica la distribuzione, anche se il programma è già stato eseguito correttamente. Può essere utile quando si utilizzano distribuzioni ricorrenti in cui viene aggiornato il programma, ad esempio software antivirus.|  
    |Eseguire di nuovo se il tentativo precedente non riuscito|Verrà eseguiti nuovamente il programma quando si pianifica la distribuzione solo se ha esito negativo del tentativo di esecuzione precedente.|  
    |Eseguire di nuovo se ha esito positivo nel tentativo precedente|Il programma eseguito solo se già stato eseguito correttamente sul client. Questa impostazione è utile quando si usano avvisi ricorrenti in cui il programma viene aggiornato regolarmente e ogni aggiornamento richiede l'installazione corretta dell'aggiornamento precedente.|  

9. Nella pagina **Esperienza utente** specificare le informazioni seguenti:  

    -   **Consenti agli utenti di eseguire il programma indipendentemente dalle assegnazioni** - Se questa opzione è abilitata, gli utenti possono installare il software da Software Center indipendentemente da qualsiasi intervallo di installazione pianificato.  

    -   **Installazione software** - Permette l'installazione del software al di fuori di qualsiasi finestra di manutenzione configurata.  

    -   **Riavvio del sistema (se richiesto per completare l'installazione)** - Se l'installazione del software richiede un riavvio del dispositivo per il completamento, questa opzione consente di eseguire tale riavvio al di fuori di qualsiasi finestra di manutenzione configurata.  

    -   **Dispositivi integrati** - Quando si distribuiscono pacchetti e programmi in dispositivi con Windows Embedded abilitati per i filtri di scrittura, è possibile specificare di installare i pacchetti e i programmi nella sovrapposizione temporanea e confermare le modifiche in seguito oppure confermare le modifiche alla scadenza dell'installazione o all'interno di una finestra di manutenzione. Quando si confermano le modifiche alla scadenza dell'installazione o all'interno di una finestra di manutenzione, è necessario il riavvio per mantenere le modifiche nel dispositivo.  

        > [!NOTE]  
        >  Quando si distribuisce un pacchetto o un programma in un dispositivo Windows Embedded, assicurarsi che il dispositivo è un membro di una raccolta che dispone di una finestra di manutenzione configurata. Per altre informazioni sull'uso delle finestre di manutenzione quando si distribuiscono pacchetti e programmi a dispositivi con Windows Embedded, vedere [Creazione di applicazioni Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md).  
  
10. Nella pagina **Punti di distribuzione** specificare le informazioni seguenti:  

    -   **Opzioni di distribuzione** - Specificare le azioni che un client deve intraprendere per eseguire il contenuto del programma. È possibile specificare il comportamento quando il client è un limite di rete veloce o un limite di rete lente o inaffidabili.  

    -   **Consentire ai client di condividere il contenuto con altri client nella stessa subnet** : selezionare questa opzione per ridurre il carico sulla rete consentendo ai client di scaricare contenuto da altri client nella rete che già scaricato e memorizzato nella cache il contenuto. Questa opzione si avvale di Windows BranchCache e può essere usata in computer che eseguono Windows Vista SP2 e versioni successive.  

    -   **Consenti ai client di utilizzare un percorso origine di fallback per il contenuto** - Se questa opzione è abilitata, i client possono cercare il contenuto richiesto in altri punti di distribuzione nella gerarchia se non è disponibile nel punto di distribuzione o nel gruppo di punti di distribuzione specificato.  

11. Nella pagina **Riepilogo** esaminare le azioni da eseguire e completare la procedura guidata.  

     È possibile visualizzare la distribuzione nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio** e nel riquadro dei dettagli della scheda di distribuzione del pacchetto quando si seleziona la distribuzione. Per altre informazioni, vedere [Monitorare pacchetti e programmi](/sccm/apps/deploy-use/packages-and-programs#monitor-packages-and-programs) in questo argomento.  

> [!IMPORTANT]  
>  Se è stata configurata l'opzione **Esegui programma dal punto di distribuzione** nella pagina **Punti di distribuzione** della Distribuzione guidata del software, non deselezionare l'opzione **Copia il contenuto del pacchetto in una condivisione pacchetto nei punti di distribuzione**, perché così facendo il pacchetto non sarà più disponibile per l'esecuzione dai punti di distribuzione.  

##  <a name="monitor-packages-and-programs"></a>Monitorare pacchetti e programmi  
 Per monitorare le distribuzioni di pacchetti e programmi, è necessario seguire le stesse procedure usate per monitorare le applicazioni, descritte in [Monitorare applicazioni](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

 I pacchetti e i programmi includono anche alcuni report predefiniti, che permettono di monitorare le informazioni sullo stato di distribuzione dei pacchetti e dei programmi. Tali report dispongono della categoria report di **distribuzione Software-pacchetti e programmi** e **distribuzione Software-pacchetto e programma lo stato di distribuzione**.  

 Per altre informazioni sulle modalità di configurazione della creazione di report in Configuration Manager, vedere [Creazione di report in System Center Configuration Manager](../../core/servers/manage/reporting.md).  

##  <a name="manage-packages-and-programs"></a>Gestire pacchetti e programmi  
 Nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni**, fare clic su **Pacchetti**, selezionare il pacchetto che si vuole gestire e quindi selezionare un'attività di gestione tra quelle contenute nella tabella seguente.  

|Attività|Altre informazioni|  
|----------|----------------------|  
|**Crea file di contenuto di pre-installazione**|Apre la creazione di pre-installazione guidata File di contenuto che consente di creare un file che contiene il contenuto del pacchetto che può essere importato manualmente a un altro sito. Ciò risulta utile in situazioni in cui si dispone di larghezza di banda bassa tra il server del sito e il punto di distribuzione.|  
|**Crea programma**|Verrà aperto il programma di creazione che consente di creare un nuovo programma per il pacchetto.|  
|**Export**|Apre l'Esportazione guidata del pacchetto, che permette di esportare il pacchetto selezionato e il suo contenuto in un file.<br /><br /> Per informazioni su come importare pacchetti e programmi, vedere Creare pacchetti e programmi in questo argomento.|  
|**Distribuisci**|Apre la Distribuzione guidata del software, che permette di distribuire un pacchetto e un programma selezionati in una raccolta. Per altre informazioni, vedere [Distribuire pacchetti e programmi](/sccm/apps/deploy-use/packages-and-programs#deploy-packages-and-programs) in questo argomento.|  
|**Distribuisci contenuto**|Verrà visualizzata la distribuzione guidata contenuto che consente di inviare il contenuto associato con il pacchetto e programma per punti di distribuzione selezionato o gruppi di punti di distribuzione.|  
|**Aggiorna punti di distribuzione**|Aggiorna i punti di distribuzione con il contenuto più recente per il pacchetto e il programma selezionati.|  

##  <a name="about-the-package-definition-file-format"></a>Informazioni sul formato di file definizioni del pacchetto  
 I file definizioni del pacchetto sono script che è possibile usare per automatizzare la creazione di pacchetti e programmi con Configuration Manager. Specificano tutte le informazioni di cui Configuration Manager ha bisogno per creare un pacchetto e un programma, ad eccezione del percorso dei file di origine del pacchetto. Ogni file di definizione del pacchetto è un file di testo ASCII o UTF-8 seguendo il formato del file ini e contenente descritti nelle sezioni seguenti:  

###  <a name="pdf"></a>[PDF]  
 In questa sezione identifica il file come file di definizione del pacchetto. Contiene le informazioni seguenti:  

-   **Versione**: Specifica la versione del formato di file di definizione pacchetto che viene utilizzata dal file. Corrisponde alla versione di System Management Server (SMS) o Configuration Manager per cui è stato scritto. Questa voce è necessaria.  

###  <a name="package-definition"></a>[Package Definition]  
 In questa sezione del file di definizione del pacchetto specifica le proprietà del pacchetto e programma. Fornisce le informazioni seguenti:  

-   **Nome**: Il nome del pacchetto, fino a 50 caratteri. Questa voce è necessaria.  

-   **Versione**: La versione del pacchetto, un massimo di 32 caratteri. Questa voce è facoltativa.  

-   **Icona**: Facoltativamente, il file contenente l'icona da utilizzare per il pacchetto. Se specificata, questa icona sostituirà l'icona del pacchetto predefinito nella console di Configuration Manager.  

-   **Publisher**: Il server di pubblicazione del pacchetto, un massimo di 32 caratteri. Questa voce è necessaria.  

-   **Lingua**: La versione della lingua del pacchetto, un massimo di 32 caratteri. Questa voce è necessaria.  

-   **Commento**: Commento facoltativo sul pacchetto, fino a 127 caratteri.  

-   **ContainsNoFiles**: Questa voce indica se un'origine è associata al pacchetto.  

-   **Programmi**: I programmi definiti per il pacchetto. Ogni nome del programma corrisponde a un **[programma]** sezione in questo file di definizione del pacchetto. Questa voce è necessaria.  

     Esempio:  

     `Programs=Typical, Custom, Uninstall`  

-   **MIFFileName**: Il nome del file di formato MIF (Management Information) che contiene lo stato del pacchetto, fino a 50 caratteri.  

-   **MIFName**: Il nome del pacchetto (per la corrispondenza MIF), fino a 50 caratteri.  

-   **MIFVersion**: Il numero di versione del pacchetto (per la corrispondenza MIF), un massimo di 32 caratteri.  

-   **MIFPublisher**: Autore del software del pacchetto (per la corrispondenza MIF), un massimo di 32 caratteri.  

###  <a name="program"></a>[programma]  
 Per ogni programma specificato nel **programmi** voce il **[Package Definition]** sezione file di definizione del pacchetto deve includere una sezione [programma] che definisce tale programma. Ogni sezione programma fornisce le seguenti informazioni:  

-   **Nome**: Il nome del programma, fino a 50 caratteri. Questa voce deve essere univoca all'interno di un pacchetto. Questo nome viene utilizzato quando si definiscono gli annunci. Nei computer client, viene visualizzato il nome del programma **Esegui programmi annunciati** nel Pannello di controllo. Questa voce è necessaria.  

-   **Icona**: Facoltativamente, specifica il file che contiene l'icona da utilizzare per questo programma. Se specificata, questa icona sostituirà l'icona di programma predefinita nella console di Configuration Manager e verrà visualizzata nei computer client quando il programma verrà annunciato.  

-   **Commento**: Commento facoltativo sul programma, fino a 127 caratteri.  

-   **CommandLine**: Specifica la riga di comando per il programma, fino a 127 caratteri. Il comando è relativo alla cartella di origine del pacchetto. Questa voce è necessaria.  

-   **StartIn**: Specifica la cartella di lavoro per il programma, fino a 127 caratteri. Questa voce può essere un percorso assoluto sul computer client o un percorso relativo alla cartella di origine del pacchetto. Questa voce è necessaria.  

-   **Esegui**: Specifica la modalità di programma in cui verrà eseguito il programma. È possibile specificare **ridotta a icona**, **ingrandita**, o **Hidden**. Se questa voce non è inclusa, il programma verrà eseguito in modalità normale.  

-   **AfterRunning**: Specifica qualsiasi azione speciale che si verifica dopo che il programma è stato completato correttamente. Le opzioni disponibili sono **SMSRestart**, **ProgramRestart**, o **SMSLogoff**. Se questa voce non è inclusa, il programma non verrà eseguito un'azione speciale.  

-   **EstimatedDiskSpace**: Specifica la quantità di spazio su disco del software richiesto per poter eseguire sul computer. Questo valore può essere specificato come **sconosciuto** (impostazione predefinita) o come un numero intero maggiore o uguale a zero. Se viene specificato un valore, anche le unità per il valore devono essere specificate.  

     Esempio:  

     `EstimatedDiskSpace=38MB`  

-   **EstimatedRunTime**: Specifica la durata stimata (in minuti) che il programma è previsto per l'esecuzione nel computer client. Questo valore può essere specificato come **sconosciuto** (impostazione predefinita) o come numero intero maggiore di zero.  

     Esempio:  

     `EstimatedRunTime=25`  

-   **SupportedClients**: Specifica i processori e sistemi operativi in cui verrà eseguito il programma. Le piattaforme specificate devono essere separate da virgole. Se questa voce non è inclusa, il controllo piattaforma supportata verrà disabilitato per questo programma.  

-   **SupportedClientMinVersionX**, **SupportedClientMaxVersionX**: Specifica l'intervallo di inizio alla fine dei numeri di versione per i sistemi operativi specificati nel **SupportedClients** voce.  

     Esempio:  

    ```  
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999   
    ```  

-   **AdditionalProgramRequirements**: Facoltativamente, fornire eventuali altre informazioni o i requisiti per i computer client, fino a 127 caratteri.  

-   **CanRunWhen**: Specifica lo stato dell'utente che il programma richiede di essere in grado di eseguire nel computer client. I valori disponibili sono **UserLoggedOn**, **NoUserLoggedOn**, o **AnyUserStatus**. Il valore predefinito è **UserLoggedOn**.  

-   **UserInputRequired**: Specifica se il programma richiede l'interazione con l'utente. I valori disponibili sono **True** o **False**. Il valore predefinito è **True**. Questa voce è impostata su **False** se **CanRunWhen** non è impostata su **UserLoggedOn**.  

-   **AdminRightsRequired**: Specifica se il programma richiede credenziali amministrative nel computer sia in grado di eseguire. I valori disponibili sono **True** o **False**. Il valore predefinito è **False**. Questa voce è impostata su **True** se **CanRunWhen** non è impostata su **UserLoggedOn**.  

-   **UseInstallAccount**: Specifica se il programma utilizza l'Account di installazione del Software Client quando viene eseguita nel computer client. Per impostazione predefinita, questo valore è **False**. Questo valore corrisponde anche **False** se **CanRunWhen** è impostato su **UserLoggedOn**.  

-   **DriveLetterConnection**: Specifica se il programma richiede una connessione di lettera di unità per i file del pacchetto che si trovano nel punto di distribuzione. È possibile specificare **True** o **False**. Il valore predefinito è **False**, che consente al programma di utilizzare una connessione (Universal Naming Convention). Quando questo valore è impostato su **True**, verrà utilizzata la lettera di unità disponibile successiva (a partire da z e procedere a ritroso).  

-   **SpecifyDrive**: Facoltativamente, specifica una lettera di unità nel programma sono necessari per connettersi al file del pacchetto nel punto di distribuzione. Questa specifica impone l'utilizzo della lettera di unità specificata per le connessioni client ai punti di distribuzione.  

-   **ReconnectDriveAtLogon**: Specifica se il computer si riconnette al punto di distribuzione quando l'utente accede. I valori disponibili sono **True** o **False**. Il valore predefinito è **False**.  

-   **DependentProgram**: Specifica un programma in questo pacchetto che deve essere eseguito prima il programma corrente. Questa voce usa il formato **DependentProgram**=<**NomeProgramma>**, dove **<NomeProgramma\>** corrisponde alla voce **Name** per il programma nel file di definizione del pacchetto. Se non sono presenti programmi dipendenti, lasciare vuota questa voce.  

     Esempio:  

     DependentProgram = Admin  
    DependentProgram =  

-   **Assegnazione**: Specifica come il programma viene assegnato agli utenti. Questo valore può essere: **FirstUser,** solo il primo utente che esegue l'accesso viene eseguito il programma, o **EveryUser,** ogni utente che accede al client viene eseguito il programma. Quando **CanRunWhen** non è impostata su **UserLoggedOn**, questa voce è impostata su **FirstUser**.  

-   **Disattivata**: Specifica se il programma può essere annunciato ai client. I valori disponibili sono **True** o **False**. Il valore predefinito è **False**.  



<!--HONumber=Nov16_HO1-->



---
title: 'Gestire i driver '
titleSuffix: Configuration Manager
description: Usare il catalogo dei driver di Configuration Manager per importare i driver dei dispositivi, raggruppare i driver in pacchetti e distribuire i pacchetti ai punti di distribuzione.
ms.date: 01/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 84802d55-112e-4f7f-9a48-74a80d91a0f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4eb97430bd5d7ae5cc50044f8049f41cb9b4cf08
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="manage-drivers-in-system-center-configuration-manager"></a>Gestire i driver in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager include un catalogo di driver che è possibile usare per gestire i driver di dispositivo Windows presenti nell'ambiente di Configuration Manager. È possibile usare il catalogo dei driver per importare i driver di dispositivo in Configuration Manager e raggrupparli in pacchetti da distribuire a punti di distribuzione che consentono di accedere ai pacchetti durante la distribuzione di un sistema operativo. È possibile utilizzare i driver di dispositivo durante l'installazione completa del sistema operativo nel computer di destinazione e durante l'installazione di Windows PE tramite un'immagine di avvio. I driver di dispositivo Windows sono costituiti da un file di informazioni per l'installazione (INF) ed eventuali file aggiuntivi necessari per il supporto del dispositivo. Quando si distribuisce un sistema operativo, Configuration Manager recupera le informazioni su piattaforma e hardware per il dispositivo dal file INF. Usare gli argomenti seguenti per gestire i driver nell'ambiente di Configuration Manager.

##  <a name="BKMK_DriverCategories"></a> Categorie di driver di dispositivo  
 Quando si importano i driver di dispositivo, è possibile assegnarli a una categoria. Le categorie di driver di dispositivo consentono di raggruppare nel catalogo i driver utilizzati in modo analogo. Ad esempio, è possibile assegnare tutti i driver di dispositivo della scheda di rete a una categoria specifica. Quindi, quando si crea una sequenza di attività che include il passaggio [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) , è possibile specificare una categoria specifica di driver di dispositivo. Configuration Manager analizza l'hardware e seleziona i driver applicabili dalla categoria per eseguire un'installazione di appoggio sul sistema per l'uso da parte dell'installazione di Windows.  

##  <a name="BKMK_ManagingDriverPackages"></a> Pacchetti driver  
 È possibile raggruppare driver di dispositivo simili in pacchetti per semplificare le distribuzioni del sistema operativo. Si potrebbe, ad esempio, decidere di creare un pacchetto driver per ogni produttore di computer nella rete. È possibile creare un pacchetto driver durante l'importazione dei driver nel catalogo direttamente nel nodo **Pacchetti driver** . Al termine della creazione del pacchetto driver, è necessario distribuirlo ai punti di distribuzione da cui i computer client di Configuration Manager possono installare i driver necessari. Considerare quanto segue:  

-   Quando si crea un pacchetto driver, il percorso di origine del pacchetto deve puntare a una condivisione di rete vuota che non sia utilizzata da un altro pacchetto driver e il provider SMS deve disporre di autorizzazioni di lettura e scrittura per tale percorso.  

-   Quando si aggiungono driver di dispositivo a un pacchetto driver, Configuration Manager copia il driver di dispositivo nel percorso di origine del pacchetto. È possibile aggiungere solo i driver di dispositivo importati e abilitati nel catalogo per un pacchetto driver.  

-   Per copiare un sottoinsieme di driver di dispositivo da un pacchetto driver esistente, creare un nuovo pacchetto, aggiungere il sottoinsieme di driver di dispositivo, quindi distribuire il nuovo pacchetto in un punto di distribuzione.  

 Usare le sezioni seguenti per creare e gestire i pacchetti driver.  

###  <a name="CreatingDriverPackages"></a> Creare un pacchetto driver  
 Utilizzare la seguente procedura per creare un nuovo pacchetto driver.  

> [!IMPORTANT]  
>  Per creare un pacchetto driver, è necessario disporre di una cartella di rete vuota non utilizzata da un altro pacchetto driver. Nella maggior parte dei casi, è necessario creare una nuova cartella prima di avviare questa procedura.  

> [!NOTE]  
>  Quando si usano sequenze di attività per installare i driver, creare pacchetti driver contenenti meno di 500 driver di dispositivo.  

 Utilizzare la seguente procedura per creare un pacchetto driver.  

#### <a name="to-create-a-driver-package"></a>Per creare un pacchetto driver  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Pacchetti driver**.  

3.  Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea pacchetto driver**.  

4.  Nella casella **Nome** specificare un nome descrittivo per il pacchetto driver.  

5.  Nella casella **Commento** immettere una descrizione facoltativa per il pacchetto driver. Assicurarsi che la descrizione fornisca informazioni sul contenuto o sullo scopo del pacchetto driver.  

6.  Nella casella **Percorso** specificare una cartella di origine vuota per il pacchetto driver. Immettere il percorso della cartella di origine in formato UNC (Universal Naming Convention). Ogni pacchetto driver deve utilizzare una cartella univoca.  

    > [!IMPORTANT]  
    >  L'account del server del sito deve avere le autorizzazioni di **lettura** e **scrittura** per la cartella di origine specificata.  

 Il nuovo pacchetto driver non contiene nessun driver. Il passaggio successivo consiste nell'aggiunta dei driver al pacchetto.  

 Se il nodo **Pacchetti driver** contiene diversi pacchetti, è possibile aggiungere cartelle al nodo per separare i pacchetti in gruppi logici.  

###  <a name="BKMK_PackageActions"></a> Azioni aggiuntive per i pacchetti driver  
 Durante la selezione di uno o più pacchetti driver dal nodo **Pacchetti driver** è possibile eseguire azioni aggiuntive per gestire i pacchetti driver. Le azioni includono le seguenti:  

|Action|Descrizione|  
|------------|-----------------|  
|**Crea file di contenuto di pre-installazione**|Crea file che possono essere utilizzati per importare manualmente il contenuto e i metadati associati. Utilizzare il contenuto pre-installazione quando si dispone di larghezza di banda di rete bassa tra il server del sito e i punti di distribuzione in cui è archiviato il pacchetto driver.|  
|**Eliminazione**|Rimuove il pacchetto driver dal nodo **Pacchetti driver** .|  
|**Distribuisci contenuto**|Distribuisce il pacchetto driver nei punti di distribuzione, nei gruppi di punti di distribuzione e nei gruppi di punti di distribuzione associati alle raccolte.|  
|**Gestione account di accesso**|Aggiunge, modifica o rimuove gli account di accesso per il pacchetto driver.<br /><br /> Per altre informazioni sugli account di accesso al pacchetto, vedere [Account usati in Configuration Manager](../../core/plan-design/hierarchy/accounts.md).|  
|**Sposta**|Sposta il pacchetto driver in un'altra cartella del nodo **Pacchetti driver** .|  
|**Aggiorna punti di distribuzione**|Aggiorna il pacchetto driver del dispositivo in tutti i punti di distribuzione in cui è archiviato il pacchetto. Questa azione copia solo il contenuto modificato dopo l'ultima distribuzione.|  
|**Proprietà**|Apre la finestra di dialogo **Proprietà** che consente di esaminare e modificare il contenuto e le proprietà del driver di dispositivo. È ad esempio possibile modificare il nome e la descrizione del driver di dispositivo, abilitare il driver di dispositivo e specificare in quale piattaforma possa essere eseguito il driver di dispositivo.|  

##  <a name="BKMK_DeviceDrivers"></a> Driver di dispositivo  
 È possibile installare i driver del dispositivo nei computer di destinazione senza includerli nell'immagine del sistema operativo in fase di distribuzione. Configuration Manager offre un catalogo dei driver che contiene i riferimenti a tutti i driver di dispositivo importati in Configuration Manager. Il catalogo dei driver si trova nell'area di lavoro **Raccolta software** ed è costituito da due nodi: **Driver** e **Pacchetti driver**. Nel nodo **Driver** vengono elencati tutti i driver sono stati importati nel catalogo dei driver. Usare il nodo per trovare i dettagli di tutti i driver importati, modificare i driver in un pacchetto driver o in un'immagine di avvio, abilitare o disabilitare un driver e altro ancora.  

###  <a name="BKMK_ImportDrivers"></a> Importare i driver di dispositivo nel catalogo dei driver  
 È necessario importare i driver di dispositivo nel catalogo dei driver prima di utilizzarli durante la distribuzione di un sistema operativo. Per gestire meglio i driver di dispositivo, importare solo i driver da installare all'interno della distribuzione del sistema operativo. Tuttavia, è anche possibile archiviare più versioni di driver di dispositivo nel catalogo dei driver per aggiornare in modo semplice i driver dispositivo esistenti quando cambiano i requisiti dei dispositivi hardware nella rete.  

 Durante il processo di importazione del driver di dispositivo, Configuration Manager esegue la lettura delle informazioni relative a provider, classe, versione, firma, hardware supportato e piattaforma supportata associate al dispositivo. Per impostazione predefinita, il driver viene denominato come il primo dispositivo hardware supportato. Tuttavia, è possibile rinominare il driver di dispositivo in un secondo momento. L'elenco di piattaforme supportate si basa sulle informazioni contenute nel file INF del driver. Dal momento che l'accuratezza di queste informazioni può variare, è necessario verificare manualmente che il driver di dispositivo sia supportato dopo l'importazione nel catalogo dei driver.  

 Dopo aver importato i driver di dispositivo nel catalogo, è inoltre possibile aggiungere i driver di dispositivo ai pacchetti driver o ai pacchetti di immagini di avvio.  

> [!IMPORTANT]  
>  Non è possibile importare i driver di dispositivo direttamente in una sottocartella del nodo **Driver** . Per importare un driver di dispositivo in una sottocartella, è innanzitutto necessario importare il driver di dispositivo nel nodo **Driver** , quindi spostare il driver nella sottocartella.  

 Utilizzare la seguente procedura per importare i driver di dispositivo Windows.  

#### <a name="to-import-windows-device-drivers-into-the-driver-catalog"></a>Per importare i driver di dispositivo Windows nel catalogo dei driver  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Driver**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Importa driver** per avviare **Importazione guidata nuovo driver**.  

4.  Nella pagina **Trova driver** specificare le opzioni seguenti e quindi fare clic su **Avanti**:  

    -   **Importa tutti i driver presenti nel percorso di rete seguente (UNC)**: Per importare tutti i driver di dispositivo contenuti in una cartella specifica, specificare il percorso di rete per la cartella del driver di dispositivo. Ad esempio:  **\\\nomeserver\cartella**.  

        > [!NOTE]  
        >  Il processo di importazione di tutti i driver può richiedere alcuni minuti se sono presenti numerose cartelle e numerosi file di driver (.inf).  

    -   **Importa un driver specifico**: per importare un driver specifico da una cartella, specificare il percorso di rete (UNC) del file INF del driver di dispositivo Windows o del file Txtsetup.oem di archiviazione di massa del driver.  

    -   **Specifica l'opzione per i driver duplicati**: selezionare la modalità di gestione delle categorie driver da parte di Configuration Manager quando viene importato un driver di dispositivo duplicato.  

    > [!IMPORTANT]  
    >  Quando si importano i driver, se il server del sito non dispone dell'autorizzazione **Lettura** per la cartella, l'importazione non riesce.  

5.  Nella pagina **Dettagli driver** specificare le opzioni seguenti e quindi fare clic su **Avanti**:  

    -   **Nascondi driver non inclusi in una classe di archiviazione o di rete (per immagini d'avvio)**: usare questa impostazione per visualizzare solo i driver di archiviazione e di rete e per nascondere gli altri driver in genere non necessari per le immagini di avvio, ad esempio, i driver video o quelli del modem.  

    -   **Nascondi driver senza firma digitale**: usare questa impostazione per nascondere i driver privi di firma digitale.  

    -   Nell'elenco dei driver, selezionare i driver che si desidera importare nel catalogo dei driver.  

    -   **Abilita questi driver e consenti ai computer di installarli**: selezionare questa impostazione per consentire ai computer di installare i driver di dispositivo. Per impostazione predefinita, questa casella di controllo è selezionata.  

        > [!IMPORTANT]  
        >  In caso di problemi causati da un dispositivo o se si desidera sospendere l'installazione di un driver di dispositivo, è possibile disabilitare il driver di dispositivo deselezionando la casella di controllo **Abilita questi driver e consenti ai computer di installarli** . È inoltre possibile disattivare i driver in seguito all'importazione.  

    -   Per assegnare i driver di dispositivo a una categoria amministrativa per l'applicazione di filtri, ad esempio le categorie "Desktop" o "Notebook", fare clic su **Categorie** e selezionare una categoria esistente oppure crearne una nuova. È inoltre possibile utilizzare l'assegnazione categoria per la configurazione dei driver di dispositivo applicati alla distribuzione mediante il passaggio della sequenza attività [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers) .  

6.  Nella pagina **Aggiungi driver ai pacchetti** scegliere se aggiungere i driver a un pacchetto e quindi fare clic su **Avanti**. Per aggiungere i driver a un pacchetto tenere presente quanto segue:  

    -   Selezionare i pacchetti driver utilizzati per distribuire i driver di dispositivo.  

         In alternativa, fare clic su **Nuovo pacchetto** per creare un nuovo pacchetto driver. Quando viene creato un nuovo pacchetto driver, è necessario specificare una condivisione di rete non utilizzata da altri pacchetti driver.  

    -   Se il pacchetto è stato già distribuito nei punti di distribuzione, fare clic su **Sì** nella finestra di dialogo per aggiornare le immagini di avvio nei punti di distribuzione. Fino a quando i driver di dispositivo non vengono distribuiti ai punti di distribuzione non è possibile utilizzarli. Se si fa clic su **No**, è necessario eseguire l'azione **Aggiorna punto di distribuzione** prima che l'immagine di avvio contenga i driver aggiornati. Se il pacchetto driver non è mai stato distribuito, è necessario fare clic su **Distribuisci contenuto** nel nodo **Pacchetti driver** .  

7.  Nella pagina **Aggiungi driver alle immagini d'avvio** scegliere se aggiungere i driver di dispositivo alle immagini di avvio esistenti, quindi fare clic su **Avanti**. Se si seleziona un'immagine di avvio, tenere presente quanto segue:  

    > [!NOTE]  
    >  Come procedura consigliata, aggiungere solo driver di dispositivo di rete e di archiviazione di massa alle immagini di avvio per gli scenari di distribuzione del sistema operativo.  

    -   Fare clic su **Sì** nella finestra di dialogo per aggiornare le immagini di avvio nei punti di distribuzione. Fino a quando i driver di dispositivo non vengono distribuiti ai punti di distribuzione non è possibile utilizzarli. Se si fa clic su **No**, è necessario eseguire l'azione **Aggiorna punto di distribuzione** prima che l'immagine di avvio contenga i driver aggiornati. Se il pacchetto driver non è mai stato distribuito, è necessario fare clic su **Distribuisci contenuto** nel nodo **Pacchetti driver** .  

    -   Configuration Manager segnala se l'architettura per uno o più driver non corrisponde all'architettura delle immagini d'avvio selezionate. Se non corrispondono, fare clic su **OK** e tornare alla pagina **Dettagli driver** per cancellare i driver che non corrispondono all'architettura dell'immagine di avvio selezionata. Ad esempio, se si seleziona un'immagine di avvio x64 e x86, tutti i driver devono supportare entrambe le architetture. Se si seleziona un'immagine di avvio x64, tutti i driver devono supportare l'architettura x64.  

        > [!NOTE]  
        >  -   L'architettura è basata su quella riportata nel file con estensione inf fornito dal produttore.  
        > -   Se un driver segnala che supporta entrambe le architetture, è possibile importarlo in un'immagine di avvio.  

    -   Configuration Manager avvisa l'utente se vengono aggiunti driver di dispositivo che non sono driver di rete o di archiviazione a un'immagine d'avvio perché nella maggior parte dei casi non sono necessari per l'immagine d'avvio. Fare clic su **Sì** per aggiungere i driver all'immagine di avvio oppure su **No** per tornare indietro e modificare la selezione dei driver.  

    -   Configuration Manager segnala se uno o più driver selezionati non includono una firma digitale corretta. Fare clic su **Sì** per continuare e fare clic su **No** per tornare indietro e apportare modifiche alla selezione dei driver.  

8.  Completare la procedura guidata.  

###  <a name="BKMK_ModifyDriverPackage"></a> Gestire i driver di dispositivo in un pacchetto driver  
 Utilizzare le seguenti procedure per modificare i pacchetti driver e le immagini di avvio. Per aggiungere o rimuovere i driver di dispositivo, individuare i driver nel nodo **Driver** , quindi modificare i pacchetti o le immagini di avvio a cui sono associati i driver selezionati.  

#### <a name="to-modify-the-device-drivers-in-a-driver-package"></a>Per modificare i driver di dispositivo in un pacchetto driver  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Driver**.  

3.  Nel nodo **Driver** selezionare i driver di dispositivo che si desidera aggiungere al pacchetto driver.  

4.  Nella scheda **Home** , nel gruppo **Driver** , fare clic su **Modifica**, quindi su **Pacchetti driver**.  

5.  Per aggiungere un driver di dispositivo, selezionare la casella di controllo dei pacchetti driver a cui si desidera aggiungere i driver di dispositivo. Per rimuovere un driver di dispositivo, deselezionare la casella di controllo dei pacchetti driver da cui si desidera rimuovere il driver di dispositivo.  

     Se vengono aggiunti driver di dispositivo associati a pacchetti driver, è possibile creare un nuovo pacchetto facendo clic su **Nuovo pacchetto**. In questo modo verrà visualizzata la finestra di dialogo **Nuovo pacchetto driver** .  

6.  Se il pacchetto è stato già distribuito nei punti di distribuzione, fare clic su **Sì** nella finestra di dialogo per aggiornare le immagini di avvio nei punti di distribuzione. Fino a quando i driver di dispositivo non vengono distribuiti ai punti di distribuzione non è possibile utilizzarli. Se si fa clic su **No**, è necessario eseguire l'azione **Aggiorna punto di distribuzione** prima che l'immagine di avvio contenga i driver aggiornati. Se il pacchetto driver non è mai stato distribuito, è necessario fare clic su **Distribuisci contenuto** nel nodo **Pacchetti driver** . Prima che i driver siano disponibili, è necessario aggiornare il pacchetto driver nei punti di distribuzione.  

     Fare clic su **OK**.  

###  <a name="BKMK_ManageDriversBootImage"></a> Gestire i driver di dispositivo in un'immagine di avvio  
 È possibile aggiungere i driver di dispositivo Windows importati nel catalogo dei driver alle immagini di avvio. Quando si aggiungono driver di dispositivo a un'immagine di avvio, utilizzare le seguenti linee guida:  

-   Poiché in genere non sono necessari altri tipi di driver, aggiungere solo driver di dispositivi di archiviazione di massa e di schede di rete alle immagini di avvio. I driver non necessari aumentano inutilmente le dimensioni dell'immagine di avvio.  

-   Considerato che la versione di Windows PE richiesta si basa su Windows 10, aggiungere solo driver di dispositivo per Windows 10 a un'immagine di avvio.  

-   Assicurarsi di utilizzare il driver di dispositivo corretto per l'architettura dell'immagine di avvio.  Non aggiungere un driver di dispositivo x86 a un'immagine di avvio x64.  

 Usare la procedura seguente per aggiungere o rimuovere driver di dispositivo in un'immagine di avvio.  

#### <a name="to-modify-the--device-drivers-associated-with-a-boot-image"></a>Per modificare i driver di dispositivo associati a un'immagine di avvio  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Driver**.  

3.  Nel nodo **Driver** selezionare i driver di dispositivo che si desidera aggiungere al pacchetto driver.  

4.  Nella scheda **Home** , nel gruppo **Driver** , fare clic su **Modifica**, quindi su **Immagini d'avvio**.  

5.  Per aggiungere un driver di dispositivo, selezionare la casella di controllo dell'immagine di avvio a cui si desidera aggiungere i driver di dispositivo. Per rimuovere un driver di dispositivo, deselezionare la casella di controllo dell'immagine di avvio da cui si desidera rimuovere il driver di dispositivo.  

6.  Se non si desidera aggiornare i punti di distribuzione in cui è archiviata l'immagine di avvio, deselezionare la casella di controllo **Al termine aggiorna punti di distribuzioni** . Per impostazione predefinita, i punti di distribuzione vengono aggiornati quando viene aggiornata l'immagine di avvio.  

     Fare clic su **OK** e tenere presente quanto segue:  

    -   Fare clic su **Sì** nella finestra di dialogo per aggiornare le immagini di avvio nei punti di distribuzione. Fino a quando i driver di dispositivo non vengono distribuiti ai punti di distribuzione non è possibile utilizzarli. Se si fa clic su **No**, è necessario eseguire l'azione **Aggiorna punto di distribuzione** prima che l'immagine di avvio contenga i driver aggiornati. Se il pacchetto driver non è mai stato distribuito, è necessario fare clic su **Distribuisci contenuto** nel nodo **Pacchetti driver** .  

    -   Configuration Manager segnala se l'architettura per uno o più driver non corrisponde all'architettura delle immagini d'avvio selezionate. Se non corrispondono, fare clic su **OK** e tornare alla pagina **Dettagli driver** per cancellare i driver che non corrispondono all'architettura dell'immagine di avvio selezionata. Ad esempio, se si seleziona un'immagine di avvio x64 e x86, tutti i driver devono supportare entrambe le architetture. Se si seleziona un'immagine di avvio x64, tutti i driver devono supportare l'architettura x64.  

        > [!NOTE]  
        >  -   L'architettura è basata su quella riportata nel file con estensione inf fornito dal produttore.  
        > -   Se un driver segnala che supporta entrambe le architetture, è possibile importarlo in un'immagine di avvio.  

    -   Configuration Manager avvisa l'utente se vengono aggiunti driver di dispositivo che non sono driver di rete o di archiviazione a un'immagine d'avvio perché nella maggior parte dei casi non sono necessari per l'immagine d'avvio. Fare clic su **Sì** per aggiungere i driver all'immagine di avvio oppure su **No** per tornare indietro e modificare la selezione dei driver.  

    -   Configuration Manager segnala se uno o più driver selezionati non includono una firma digitale corretta. Fare clic su **Sì** per continuare e fare clic su **No** per tornare indietro e apportare modifiche alla selezione dei driver.  

7.  Fare clic su **OK**.  

###  <a name="BKMK_DriverActions"></a> Azioni aggiuntive per i driver di dispositivo  
 Durante la selezione di uno o più driver di dispositivo dal nodo **Driver** è possibile eseguire azioni aggiuntive per gestire i driver di dispositivo. Le azioni includono le seguenti:  

|Action|Descrizione|  
|------------|-----------------|  
|**Categorizza**|Consente di cancellare, gestire o impostare una categoria amministrativa per i driver di dispositivo selezionati.|  
|**Eliminazione**|Rimuove il driver di dispositivo dal nodo **Driver** e dai punti di distribuzione associati.|  
|**Disabilitato**|Impedisce l'installazione del driver di dispositivo. È possibile disattivare temporaneamente i driver di dispositivo in modo che le sequenze di attività e i computer client di Configuration Manager non siano in grado di installarli durante la distribuzione dei sistemi operativi. **Nota:**  l'azione Disabilita impedisce solo l'installazione dei driver con il passaggio della sequenza di attività Applica automaticamente i driver.|  
|**Attiva**|Consente alle sequenze di attività e ai computer client di Configuration Manager di installare il driver di dispositivo durante la distribuzione del sistema operativo.|  
|**Sposta**|Sposta il driver di dispositivo in un'altra cartella del nodo **Driver** .|  
|**Proprietà**|Apre la finestra di dialogo **Proprietà** , che consente di esaminare e modificare le proprietà del driver di dispositivo. È ad esempio possibile modificare il nome e la descrizione del driver di dispositivo, attivare il driver di dispositivo e specificare in quali piattaforme è possibile eseguire il driver di dispositivo.|  

##  <a name="BKMK_TSDrivers"></a> Usare le sequenze di attività per installare i driver di dispositivo  
 Utilizzare le sequenze attività per automatizzare la modalità di distribuzione del sistema operativo. Ogni passaggio della sequenza attività può eseguire un'azione specifica, ad esempio l'installazione di un driver di dispositivo. È possibile utilizzare i due passaggi della sequenza attività che seguono per installare driver di dispositivo durante la distribuzione dei sistemi operativi:  

-   [Auto Apply Drivers](../understand/task-sequence-steps.md#BKMK_AutoApplyDrivers): questo passaggio consente di associare e installare automaticamente i driver di dispositivo all'interno di una distribuzione del sistema operativo. È possibile configurare il passaggio della sequenza attività in modo che venga installato solo il driver più compatibile per ogni dispositivo hardware rilevato oppure specificare che il passaggio della sequenza attività installi tutti i driver compatibili per ogni dispositivo hardware rilevato e quindi consentire all'installazione di Windows di scegliere il driver migliore. Inoltre, è possibile specificare una categoria di driver di dispositivo per limitare i driver disponibili per questo passaggio.  

-   [Apply Driver Package](../understand/task-sequence-steps.md#BKMK_ApplyDriverPackage): questo passaggio consente di rendere disponibili tutti i driver di dispositivo in un pacchetto driver specifico per l'installazione di Windows. Nei pacchetti driver specificati l'installazione di Windows cerca i driver di dispositivo necessari. Quando si creano supporti autonomi, è necessario usare questo passaggio per installare i driver di dispositivo.  

 Quando si utilizzano questi passaggi della sequenza attività, è anche possibile specificare la modalità di installazione dei driver di dispositivo nel computer in cui viene distribuito il sistema operativo. Per altre informazioni, vedere [Gestire le sequenze di attività per automatizzare le attività](../deploy-use/manage-task-sequences-to-automate-tasks.md).  

##  <a name="BKMK_InstallingDeviceDiriversTS"></a> Usare le sequenze di attività per installare driver di dispositivo nei computer  
 Utilizzare la procedura seguente per installare i driver di dispositivo durante la distribuzione del sistema operativo.  

#### <a name="use-a-task-sequence-to-install-device-drivers"></a>Usare una sequenza di attività per installare driver di dispositivo  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

3.  Nel nodo **Sequenze attività** selezionare la sequenza attività che si desidera modificare per installare il driver di dispositivo e quindi fare clic su **Modifica**.  

4.  Passare al punto in cui si desidera aggiungere la procedura **Driver** , fare clic su **Aggiungi**e quindi selezionare **Driver**.  

5.  Aggiungere il passaggio **Applica automaticamente i driver** se si desidera che la sequenza attività installi tutti i driver di dispositivo o solo le categorie specificate. Specificare le opzioni del passaggio nella scheda **Proprietà** e ogni eventuale condizione nella scheda **Opzioni** .  

     Aggiungere il passaggio **Applica pacchetto di driver** se si desidera che la sequenza attività installi solo i driver di dispositivo presenti nel pacchetto specificato. Specificare le opzioni del passaggio nella scheda **Proprietà** e ogni eventuale condizione nella scheda **Opzioni** .  

    > [!IMPORTANT]  
    >  È possibile selezionare **Disattiva questo passaggio** nella scheda **Opzioni** per disattivare il passaggio allo scopo di risolvere i problemi della sequenza di attività.  

6.  Fare clic su **OK** per salvare la sequenza attività.  

 Per altre informazioni sulla creazione di una sequenza di attività per installare un sistema operativo, vedere [Create a task sequence to install an operating system](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md) (Creare una sequenza di attività per installare un sistema operativo).  

##  <a name="BKMK_DriverReports"></a> Report di Gestione driver  
 È possibile utilizzare diversi report nella categoria di report **Gestione driver** per determinare informazioni generali sui driver di dispositivo nel catalogo. Per altre informazioni sui report, vedere [Creazione di report](../../core/servers/manage/reporting.md).

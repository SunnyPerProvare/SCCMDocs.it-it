---
title: "Creare una sequenza di attività per acquisire un sistema operativo"
titleSuffix: Configuration Manager
description: "Una sequenza di attività di creazione e acquisizione crea un computer di riferimento che, insieme al sistema operativo, può includere driver specifici e aggiornamenti software."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 25e4ac68-0e78-4bbe-b8fc-3898b372c4e8
caps.latest.revision: "19"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 98f9f44373b854b61714c21105a28b3240b4a7f7
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="create-a-task-sequence-to-capture-an-operating-system-in-system-center-configuration-manager"></a>Creare una sequenza di attività per acquisire un sistema operativo in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Quando si usa una sequenza di attività per distribuire un sistema operativo in un computer in System Center Configuration Manager, il computer installa l'immagine del sistema operativo specificata nella sequenza di attività. Per personalizzare l'immagine del sistema operativo in modo da includere driver, applicazioni, aggiornamenti software e altri elementi specifici, è possibile usare una sequenza di attività di creazione e acquisizione per creare un computer di riferimento e quindi acquisire l'immagine del sistema operativo dal computer di riferimento. Se un computer di riferimento è già disponibile per l'acquisizione, è possibile creare una sequenza di attività personalizzata per acquisire il sistema operativo. Usare le sezioni seguenti per acquisire un sistema operativo personalizzato.  

##  <a name="BKMK_BuildCaptureTS"></a> Usare una sequenza di attività per creare e acquisire un computer di riferimento  
 La sequenza di attività di creazione e acquisizione partiziona e formatta il computer di riferimento, installa il sistema operativo, oltre al client di Configuration Manager , le applicazioni e gli aggiornamenti software, quindi acquisisce il sistema operativo dal computer di riferimento. I pacchetti associati alla sequenza di attività, ad esempio le applicazioni, devono essere disponibili nei punti di distribuzione prima di creare la sequenza di attività di creazione e acquisizione.  

###  <a name="BKMK_CreatePackages"></a> Preparativi per le distribuzioni del sistema operativo  
 Esistono molti scenari per la distribuzione di un sistema operativo nei computer dell'ambiente. Nella maggior parte dei casi, è necessario creare una sequenza di attività e selezionare **Installa un pacchetto immagine esistente** nella Creazione guidata della sequenza di attività per installare il sistema operativo, eseguire la migrazione delle impostazioni utente, applicare gli aggiornamenti software e installare le applicazioni. Prima di creare una sequenza di attività per installare un sistema operativo, devono essere disponibili gli elementi seguenti:  

-   **Richiesto**  

    -   Nella console di Configuration Manager deve essere disponibile un'[immagine di avvio](../get-started/manage-boot-images.md).  

    -   Nella console di Configuration Manager deve essere disponibile un'[immagine del sistema operativo](../get-started/manage-operating-system-images.md).  

-   **Obbligatorio (se usato)**  

    -   Nella console di Configuration Manager devono essere disponibili i [pacchetti driver](../get-started/manage-drivers.md) che contengono i driver di Windows necessari per il supporto dell'hardware nel computer di riferimento. Per altre informazioni sui passaggi della sequenza di attività per gestire i driver, vedere [Usare le sequenze di attività per installare i driver di dispositivo](../get-started/manage-drivers.md#BKMK_TSDrivers).  

    -   Gli [aggiornamenti software](../../sum/get-started/synchronize-software-updates.md) devono essere sincronizzati nella console di Configuration Manager.  

    -   Le [applicazioni](../../apps/deploy-use/create-applications.md) devono essere aggiunte alla console di Configuration Manager.  

###  <a name="BKMK_CreateBuildCaptureTS"></a> Creare una sequenza di attività di creazione e acquisizione  
 Usare la procedura seguente per usare una sequenza di attività per creare un computer di riferimento e acquisire il sistema operativo.  

#### <a name="to-create-a-task-sequence-that-builds-and-captures-an-operating-system-image"></a>Per creare una sequenza di attività che crea e acquisisce un'immagine del sistema operativo  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea sequenza di attività** per avviare la Creazione guidata della sequenza di attività.  

4.  Nella pagina **Crea una nuova sequenza di attività** selezionare **Crea e acquisisci un'immagine del sistema operativo di riferimento**.  

5.  Nella pagina **Informazioni sequenza di attività** specificare le impostazioni seguenti e quindi fare clic su **Avanti**.  

    -   **Nome sequenza di attività**: specificare un nome che identifichi la sequenza di attività.  

    -   **Descrizione**: specificare una descrizione dell'attività eseguita dalla sequenza di attività, ad esempio una descrizione del sistema operativo creato dalla sequenza di attività.  

    -   **Immagine di avvio**: specificare l'immagine di avvio che installa l'immagine del sistema operativo.  

        > [!IMPORTANT]  
        >  L'architettura dell'immagine di avvio deve essere compatibile con l'architettura hardware del computer di destinazione.  

6.  Nella pagina **Installa Windows** specificare le impostazioni seguenti e quindi fare clic su **Avanti**.  

    -   **Pacchetto immagine**: specificare il pacchetto immagine del sistema operativo, che contiene i file necessari per installare il sistema operativo.  

    -   **Indice immagine**: specificare il sistema operativo da installare. Se l'immagine del sistema operativo contiene più versioni, selezionare la versione da installare.  

    -   **Codice Product Key**: specificare il codice Product Key per il sistema operativo Windows da installare. È possibile specificare i codici Product Key per contratti multilicenza codificati e i codici Product Key standard. Se si usa un codice Product Key non codificato, ogni gruppo di 5 caratteri deve essere separato da un trattino (-). Ad esempio: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   **Modalità di gestione licenze del server**: specificare che la licenza del server è **Per postazione**, **Per server**o che non è specificata alcuna licenza. Se la licenza del server è **Per server**, specificare anche il numero massimo di connessioni al server.  

    -   Specificare come gestire l'account amministratore usato quando viene distribuito il sistema operativo.  

        -   **Genera in modo casuale la password dell'amministratore locale e disattiva l'account su tutte le piattaforme supportate**: specificare se Configuration Manager deve creare una password casuale per l'account amministratore locale e disabilitare l'account quando viene distribuito il sistema operativo.  

        -   **Attiva l'account e specifica la password dell'amministratore locale**: specificare se la stessa password viene usata per l'account di amministratore locale su tutti i computer in cui viene distribuito il sistema operativo.  

7.  Nella pagina **Configura rete** specificare le impostazioni seguenti e quindi fare clic su **Avanti**.  

    -   **Aggiunta a un gruppo di lavoro**: specificare se aggiungere il computer di destinazione a un gruppo di lavoro quando viene distribuito il sistema operativo.  

    -   **Aggiunta a un dominio**: specificare se aggiungere il computer di destinazione a un dominio quando viene distribuito il sistema operativo. In **Dominio**specificare il nome del dominio.  

        > [!IMPORTANT]  
        >  È possibile cercare i domini nella foresta locale, ma è necessario specificare il nome di dominio per una foresta remota.  

         È inoltre possibile specificare un'unità organizzativa. Si tratta di un'impostazione facoltativa che specifica il nome distinto LDAP X.500 dell'unità organizzativa in cui creare l'account computer se non esiste già.  

    -   **Account**: specificare il nome utente e la password per l'account con le autorizzazioni per l'aggiunta al dominio specificato. Ad esempio: *dominio\utente* o *%variabile%*.  

        > [!IMPORTANT]  
        >  Se si prevede di migrare le impostazioni del dominio o le impostazioni del gruppo di lavoro, è necessario immettere le credenziali di dominio appropriate.  

8.  Nella pagina **Installa Configuration Manager** specificare il pacchetto client di Configuration Manager contenente i file di origine per installare il client di Configuration Manager, aggiungere eventuali altre proprietà necessarie per installare il client e quindi fare clic su **Avanti**.  

     Per altre informazioni sulle proprietà utilizzabili per installare un client, vedere [Informazioni sulle proprietà di installazione del client ](../../core/clients/deploy/about-client-installation-properties.md).  

9. Nella pagina **Includi aggiornamenti** specificare se installare gli aggiornamenti software necessari, tutti gli aggiornamenti software o nessun aggiornamento software e quindi fare clic su **Avanti**. Se si sceglie di installare gli aggiornamenti software, Configuration Manager installa solo quelli assegnati alle raccolte di cui il computer di destinazione è membro.  

10. Nella pagina **Installa applicazioni** specificare le applicazioni da installare nel computer di destinazione e quindi fare clic su **Avanti**. Se si specificano più applicazioni, è possibile specificare che la sequenza di attività continui anche se l'installazione di un'applicazione specifica non riesce.  

11. Nella pagina **Preparazione sistema** specificare le seguenti impostazioni e quindi fare clic su **Avanti**.  

    -   **Pacchetto**: specificare il pacchetto di Configuration Manager contenente la versione appropriata di Sysprep da usare per acquisire le impostazioni del computer di riferimento.  

         Se la versione del sistema operativo in esecuzione è Windows Vista o versione successiva, Sysprep viene installato automaticamente nel computer e non è necessario specificare un pacchetto.  

12. Nella pagina **Proprietà immagini** specificare le seguenti impostazioni per l'immagine del sistema operativo e quindi fare clic su **Avanti**.  

    -   **Creato da**: specificare il nome dell'utente che ha creato l'immagine del sistema operativo.  

    -   **Versione**: specificare un numero di versione definito dall'utente da associare all'immagine del sistema operativo.  

    -   **Descrizione**: specificare una descrizione definita dall'utente dell'immagine del computer del sistema operativo.  

13. Nella pagina **Acquisisci immagine** specificare le seguenti impostazioni, quindi fare clic su **Avanti**.  

    -   **Percorso**: specificare una cartella di rete condivisa in cui è archiviato il file di output con estensione WIM. Questo file contiene l'immagine del sistema operativo basata sulle impostazioni specificate usando questa procedura guidata. Se si specifica una cartella che contiene un file con estensione wim esistente, il file esistente viene sovrascritto.  

    -   **Account**: specificare l'account di Windows con le autorizzazioni per la condivisione di rete in cui viene archiviata l'immagine.  

14. Completare la procedura guidata.  

15. Per aggiungere ulteriori passaggi alla sequenza attività, selezionare la sequenza attività creata e fare clic su **Modifica**. Per informazioni su come modificare una sequenza di attività, vedere [Modificare una sequenza di attività](manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

 Distribuire la sequenza di attività in un computer di riferimento in uno dei modi seguenti:  

-   Se il computer di riferimento è un client di Configuration Manager, è possibile distribuire la sequenza di attività di creazione e acquisizione nella raccolta che contiene il computer di riferimento. Per informazioni su come distribuire l'immagine del sistema operativo, vedere [Creare una sequenza di attività per installare un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md).  

    > [!NOTE]  
    >  Se la sequenza attività prevede un passaggio relativo al partizionamento del disco, non selezionare l'opzione **Programma download** durante la distribuzione della sequenza attività.  

-   Se il computer di riferimento non è un client di Configuration Manager o si vuole eseguire manualmente la sequenza di attività nel computer di riferimento, eseguire la **Creazione guidata del supporto per la sequenza di attività per creare il supporto di avvio**. Per informazioni su come creare il supporto di avvio, vedere [Creare supporti di avvio](create-bootable-media.md).  

##  <a name="BKMK_CaptureExistingRefComputer"></a> Acquisire un'immagine del sistema operativo da un computer di riferimento esistente  
 Se si dispone già di un computer di riferimento pronto per l'acquisizione, è possibile creare una sequenza di attività che acquisisce il sistema operativo dal computer di riferimento. A questo scopo, verrà usato il passaggio **Acquisisci immagine del sistema operativo** della sequenza di attività per acquisire una o più immagini da un computer di riferimento e archiviarle in un file di immagine (con estensione wim) nella condivisione di rete specificata. Il computer di riferimento viene avviato in Windows PE tramite un'immagine di avvio e ogni unità disco rigido nel computer di riferimento viene acquisita come immagine separata all'interno del file WIM. Se il computer usato come riferimento include più unità, il file WIM risultante conterrà un'immagine distinta per ogni volume. Vengono acquisiti solo i volumi con formattazione NTFS o FAT32. I volumi con formati diversi e i volumi USB verranno ignorati.  

 Usare la procedura seguente per acquisire un'immagine del sistema operativo da un computer di riferimento esistente.  

#### <a name="to-capture-an-operating-system-from-an-existing-reference-computer"></a>Per acquisire un sistema operativo da un computer di riferimento esistente  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea sequenza di attività** per avviare la Creazione guidata della sequenza di attività.  

4.  Nella pagina **Crea una nuova sequenza di attività** selezionare **Crea una nuova sequenza di attività personalizzata**.  

5.  Nella pagina **Informazioni sequenza di attività** specificare un nome e una descrizione per la sequenza di attività.  

6.  Specificare un'immagine di avvio per la sequenza di attività. Questa immagine di avvio viene usata per avviare il computer di riferimento con Windows PE.  Per altre informazioni, vedere [Gestire le immagini di avvio](../get-started/manage-boot-images.md).  

7.  Completare la procedura guidata.  

8.  In **Sequenze di attività**selezionare la sequenza di attività personalizzata e quindi nella scheda **Home** , nel gruppo **Sequenza di attività** , fare clic su **Modifica** per aprire l'editor della sequenza di attività.  

9. Usare questo passaggio solo se il client di Configuration Manager è installato nel computer di riferimento.  

     Fare clic su **Aggiungi**, fare clic su **Immagini**e quindi su [Prepara client ConfigMgr per l'acquisizione](../understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture). Questo passaggio della sequenza di attività prepara il client di Configuration Manager nel computer di riferimento per l'acquisizione come parte del processo di creazione dell'immagine.  

10. Fare clic su **Aggiungi**, fare clic su **Immagini**e quindi su [Prepara Windows per l'acquisizione](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture). Questa azione della sequenza di attività esegue Sysprep e quindi riavvia il computer nell'immagine di avvio di Windows PE specificata per la sequenza di attività. Per il corretto completamento di questa azione non è necessario che il computer di riferimento sia aggiunto a un dominio.  

11. Fare clic su **Aggiungi**, fare clic su **Immagini**e quindi su [Acquisisci immagine del sistema operativo](../understand/task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).  Questo passaggio della sequenza di attività viene eseguito solo da Windows PE per acquisire le unità disco rigido nel computer di riferimento. Configurare le impostazioni seguenti per il passaggio della sequenza di attività.  

    -   **Nome** e **Descrizione**: facoltativamente, è possibile modificare il nome del passaggio della sequenza di attività e fornire una descrizione.  

    -   **Destinazione**: specificare una cartella di rete condivisa in cui è archiviato il file WIM di output. Questo file contiene l'immagine del sistema operativo basata sulle impostazioni specificate usando questa procedura guidata. Se si specifica una cartella che contiene un file con estensione wim esistente, il file esistente viene sovrascritto.  

    -   **Descrizione**, **Versione**e **Creato da**: facoltativamente, fornire i dettagli relativi all'immagine che verrà acquisita.  

    -   **Account**: specificare l'account di Windows con le autorizzazioni per la condivisione di rete specificata. Fare clic su **Imposta** per specificare il nome dell'account di Windows.  

     Fare clic su **OK** per chiudere l'editor della sequenza di attività.  

 Distribuire la sequenza di attività in un computer di riferimento in uno dei modi seguenti:  

-   Se il computer di riferimento è un client di Configuration Manager, è possibile distribuire la sequenza di attività nella raccolta che contiene il computer di riferimento. Per informazioni su come distribuire l'immagine del sistema operativo, vedere [Creare una sequenza di attività per installare un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md).  

-   Se il computer di riferimento non è un client di Configuration Manager o si vuole eseguire manualmente la sequenza di attività nel computer di riferimento, eseguire la **Creazione guidata del supporto per la sequenza di attività per creare il supporto di avvio**. Per informazioni su come creare il supporto di avvio, vedere [Creare supporti di avvio](create-bootable-media.md).  

##  <a name="BKMK_BuildandCaptureTSExample"></a> Esempio di sequenza di attività per creare e acquisire un'immagine del sistema operativo  
 Usare la tabella seguente come guida durante la creazione di una sequenza di attività che crea e acquisisce un'immagine del sistema operativo. La tabella sarà utile per decidere la sequenza generale per i passaggi della sequenza di attività e come organizzare e strutturare tali passaggi della sequenza di attività in gruppi logici. La sequenza di attività creata può variare rispetto a questo esempio e contenere più o meno passaggi e gruppi.  

> [!IMPORTANT]  
>  Usare sempre la Creazione guidata della sequenza attività per creare questo tipo di sequenza di attività.  

 Quando si usa **Crea nuova sequenza di attività** per creare questa nuova sequenza di attività, alcuni dei nomi dei passaggi sono diversi rispetto ai nomi che verrebbero usati aggiungendo manualmente questi passaggi a una sequenza di attività esistente. La tabella seguente mostra le differenze di denominazione:  

|Nome del passaggio della sequenza di attività di Creazione guidata della sequenza di attività|Nome del passaggio equivalente dell'editor delle sequenze di attività|  
|------------------------------------------------------|-----------------------------------------------|  
|Riavvia in Windows PE|Riavvia in Windows PE o usando il disco rigido|  
|Disco di partizione 0|Formato e disco partizione|  
|Applica driver dispositivo|Applica automaticamente i driver|  
|Installa aggiornamenti|Installa aggiornamenti software|  
|Aggiunta a gruppo di lavoro|Aggiunta a dominio o gruppo di lavoro|  
|Prepara Client ConfigMgr|Prepare ConfigMgr Client for Capture|  
|Prepara sistema operativo|Prepare Windows for Capture|  
|Acquisisci computer di riferimento|Acquisisci immagine del sistema operativo|  

|Gruppo di sequenze di attività/Passaggio|Riferimento|  
|-------------------------------|---------------|  
|Crea computer di riferimento - **(nuovo gruppo di sequenze di attività)**|Creare un gruppo di sequenze di attività. Un gruppo di sequenze di attività consente di mantenere assieme i passaggi delle sequenze di attività per una migliore organizzazione e un maggiore controllo degli errori.<br /><br /> Questo gruppo contiene le azioni necessarie per creare un computer di riferimento.|  
|Riavvia in Windows PE|Usare questo passaggio della sequenza di attività per specificare le opzioni di riavvio per il computer di destinazione. Questo passaggio visualizzerà un messaggio all'utente per informarlo che il computer verrà riavviato in modo da poter continuare l'installazione.<br /><br /> Questo passaggio usa la variabile della sequenza di attività **_SMSTSInWinPE** di sola lettura. Se il valore associato è uguale a **false** , il passaggio della sequenza di attività continuerà.|  
|Disco di partizione 0|Usare questo passaggio della sequenza di attività per specificare le azioni necessarie per formattare l'unità disco rigido nel computer di destinazione. Il numero di disco predefinito è **0**.<br /><br /> Questo passaggio usa la variabile della sequenza di attività **_SMSTSClientCache** di sola lettura. Questo passaggio verrà eseguito se la cache del client di Configuration Manager non esiste.|  
|Applica sistema operativo|Usare questo passaggio della sequenza di attività per installare un'immagine del sistema operativo specificata nel computer di destinazione. Questo passaggio applica tutte le immagini di volume contenute nel file WIM al volume del disco sequenziale corrispondente nel computer di destinazione, dopo aver prima eliminato tutti i file in tale volume (ad eccezione dei file di controllo specifici di Configuration Manager).|  
|Applica impostazioni Windows|Usare questo passaggio della sequenza di attività per configurare le informazioni di configurazione delle impostazioni di Windows per il computer di destinazione.|  
|Applica impostazioni di rete|Usare questo passaggio della sequenza di attività per specificare le informazioni di configurazione per la rete o il gruppo di lavoro per il computer di destinazione.|  
|Applica driver dispositivo|Usare questo passaggio della sequenza di attività per associare e installare i driver come parte della distribuzione di un sistema operativo. È possibile consentire a Installazione di Windows di cercare tutte le categorie di driver esistenti selezionando **Considera i driver di tutte le categorie** oppure limitare le categorie in cui Installazione di Windows esegue la ricerca selezionando **Limita la corrispondenza dei driver in modo da considerare solo i driver delle categorie selezionate**.<br /><br /> Questo passaggio usa la variabile della sequenza di attività **_SMSTSMediaType** di sola lettura. Se il valore associato non è uguale a **FullMedia** verrà eseguito questo passaggio della sequenza di attività.|  
|Imposta Windows e ConfigMgr|Usare questo passaggio della sequenza di attività per installare il software client di Configuration Manager. Configuration Manager installa e registra il GUID del client di Configuration Manager. È possibile assegnare i parametri di installazione necessari nella finestra **Proprietà di installazione** .|  
|Installa aggiornamenti|Usare questo passaggio della sequenza di attività per specificare in che modo gli aggiornamenti software vengono installati nel computer di destinazione. Il computer di destinazione viene valutato alla ricerca di aggiornamenti software applicabili solo in corrispondenza con l'esecuzione di questo passaggio della sequenza di attività, quando il computer di destinazione viene valutato alla ricerca di aggiornamenti software applicabili in modo simile agli altri client gestiti da Configuration Manager.<br /><br /> Questo passaggio usa la variabile della sequenza di attività **_SMSTSMediaType** di sola lettura. Se il valore associato non è uguale a **FullMedia** verrà eseguito questo passaggio della sequenza di attività.|  
|Acquisisci computer di riferimento - **(nuovo gruppo di sequenze di attività)**|Creare un altro gruppo di sequenze di attività. Questo gruppo contiene i passaggi necessari per preparare e acquisire un computer di riferimento.|  
|Aggiunta a gruppo di lavoro|Usare questo passaggio della sequenza di attività per specificare le informazioni necessarie per aggiungere il computer di destinazione a un gruppo di lavoro.|  
|Prepare ConfigMgr Client for Capture|Usare questo passaggio per preparare il client di Configuration Manager nel computer di riferimento per l'acquisizione come parte del processo di creazione dell'immagine.|  
|Prepara sistema operativo|Usare questo passaggio della sequenza di attività per specificare le opzioni di Sysprep da usare durante l'acquisizione delle impostazioni di Windows dal computer di riferimento. Questo passaggio della sequenza di attività esegue Sysprep e quindi riavvia il computer nell'immagine di avvio di Windows PE specificata per la sequenza di attività.|  
|Acquisisci immagine del sistema operativo|Usare questo passaggio della sequenza di attività per immettere una condivisione di rete esistente specifica e un file WIM da usare per il salvataggio dell'immagine. Questo percorso viene usato come percorso di origine del pacchetto durante l'aggiunta di un pacchetto di immagine del sistema operativo tramite l' **Aggiunta guidata immagine del sistema operativo**.|  

 Dopo l'acquisizione di un'immagine da un computer di riferimento, non acquisire un'altra immagine del sistema operativo dal computer di riferimento, perché le voci del Registro di sistema vengono create durante la configurazione iniziale. Creare un nuovo computer di riferimento ogni volta che si acquisisce l'immagine del sistema operativo. Se si intende utilizzare lo stesso computer di riferimento per creare immagini del sistema operativo in futuro, disinstallare innanzitutto il client di Configuration Manager, quindi reinstallare il client di Configuration Manager.  

## <a name="next-steps"></a>Passaggi successivi  
[Metodi per distribuire i sistemi operativi aziendali](methods-to-deploy-enterprise-operating-systems.md)

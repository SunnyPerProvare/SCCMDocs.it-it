---
title: Creare una sequenza di attività per acquisire un sistema operativo
titleSuffix: Configuration Manager
description: Una sequenza di attività di creazione e acquisizione crea un computer di riferimento che può includere driver specifici e aggiornamenti software insieme al sistema operativo.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 25e4ac68-0e78-4bbe-b8fc-3898b372c4e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ee008f256dbdb728d2f31b6a6dfa2828798bd38a
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "74659374"
---
# <a name="create-a-task-sequence-to-capture-an-os"></a>Creare una sequenza di attività per acquisire un sistema operativo

*Si applica a: Configuration Manager (Current Branch)*

Quando si usa una sequenza di attività per distribuire un sistema operativo in un computer in Configuration Manager, il computer installa l'immagine del sistema operativo specificata nella sequenza di attività. È possibile personalizzare l'immagine del sistema operativo in modo da includere driver, applicazioni e aggiornamenti software specifici. Usare prima di tutto una sequenza di attività di creazione e acquisizione per creare un computer di riferimento. Quindi acquisire l'immagine del sistema operativo dal computer di riferimento. Se un computer di riferimento è già disponibile per l'acquisizione, creare una sequenza di attività personalizzata per acquisire il sistema operativo.

## <a name="BKMK_BuildCaptureTS"></a> Informazioni sulla sequenza di attività di creazione e acquisizione

La sequenza di attività di creazione e acquisizione:

- Partiziona e formatta il computer di riferimento
- Installa il sistema operativo
- Installa il client di Configuration Manager
- Installa applicazioni
- Applica gli aggiornamenti software
- Acquisisce il sistema operativo dal computer di riferimento

I pacchetti associati alla sequenza di attività, ad esempio le applicazioni, devono essere disponibili nei punti di distribuzione prima di distribuire la sequenza di attività di creazione e acquisizione.

## <a name="BKMK_CreatePackages"></a> Requisiti

Prima di creare una sequenza di attività per installare un sistema operativo, verificare che siano presenti i componenti seguenti:  

### <a name="required"></a>Richiesto

- [Immagine d'avvio](/sccm/osd/get-started/manage-boot-images)

- [Immagine del sistema operativo](/sccm/osd/get-started/manage-operating-system-images)

### <a name="required-if-used"></a>Obbligatorio (se usato)

- I [pacchetti driver](/sccm/osd/get-started/manage-drivers) che contengono i driver di Windows necessari per il supporto dell'hardware nel computer di riferimento. Per altre informazioni sui passaggi della sequenza di attività per gestire i driver, vedere [Usare le sequenze di attività per installare i driver di dispositivo](/sccm/osd/get-started/manage-drivers#BKMK_TSDrivers).

- [Aggiornamenti software](/sccm/sum/get-started/synchronize-software-updates)

- [Applicazioni](/sccm/apps/deploy-use/create-applications)

## <a name="BKMK_CreateBuildCaptureTS"></a> Creare una sequenza di attività di creazione e acquisizione

Usare la procedura seguente per usare una sequenza di attività per creare un computer di riferimento e acquisire il sistema operativo.

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e quindi selezionare il nodo **Sequenze di attività**.  

1. Nella scheda **Home**, nel gruppo **Crea**, selezionare su **Crea sequenza di attività** per avviare la Creazione guidata della sequenza di attività.  

1. Nella pagina **Crea una nuova sequenza di attività** selezionare **Crea e acquisisci un'immagine del sistema operativo di riferimento**.  

1. Nella pagina **Informazioni sequenza di attività** specificare le impostazioni seguenti:  

    - **Nome sequenza di attività**: specificare un nome che identifica la sequenza di attività.  

    - **Descrizione**: specificare una descrizione facoltativa per la sequenza di attività. Ad esempio, descrivere il sistema operativo creato dalla sequenza di attività.

    - **Immagine d'avvio**: specificare l'immagine d'avvio da usare con questa sequenza di attività.  

        > [!IMPORTANT]  
        > L'architettura dell'immagine di avvio deve essere compatibile con l'architettura hardware del computer di destinazione.  

1. Nella pagina **installa Windows** specificare le impostazioni seguenti:  

    - **Pacchetto immagine**: specificare il pacchetto immagine del sistema operativo, che contiene i file necessari per installare il sistema operativo.  

    - **Image index**: specifica l'indice del sistema operativo da installare nell'immagine. Se l'immagine del sistema operativo contiene più versioni, selezionare la versione da installare.  

    - **Codice Product Key**: se necessario, specificare il codice Product Key per il sistema operativo Windows da installare. È possibile specificare i codici Product Key per contratti multilicenza codificati e i codici Product Key standard. Se si usa un codice Product Key non codificato, separare ogni gruppo di cinque caratteri con un trattino (`-`). Ad esempio: `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX`  

    - **Modalità di gestione licenze del server**: se necessario, specificare che la licenza del server è **Per postazione**, **Per server**o che non è specificata alcuna licenza. Se la licenza del server è **Per server**, specificare anche il numero massimo di connessioni al server.  

    - Specificare come configurare l'account amministratore per il sistema operativo distribuito:  

        - **Genera in modo casuale la password dell'amministratore locale e disattiva l'account su tutte le piattaforme supportate**: creare una password casuale per l'account amministratore locale. Disabilitare l'account quando la finestra è configurata.

        - **Abilitare l'account e specificare la password dell'amministratore locale**: usare la stessa password per l'account amministratore locale in tutti i computer in cui viene distribuito il sistema operativo.

1. Nella pagina **Configura rete** specificare le impostazioni seguenti:

    - **Aggiunta a un gruppo di lavoro**: specificare se aggiungere il computer di destinazione a un gruppo di lavoro quando viene distribuito il sistema operativo.  

    - **Aggiunta a un dominio**: specificare se aggiungere il computer di destinazione a un dominio quando viene distribuito il sistema operativo. In **Dominio**specificare il nome del dominio.  

        > [!IMPORTANT]  
        > È possibile sfogliare la foresta locale per individuare i domini locali. Specificare il nome di dominio per una foresta remota.

        È inoltre possibile specificare un'unità organizzativa. Questa impostazione è facoltativa e specifica il nome distinto LDAP X.500 dell'unità organizzativa in cui creare l'account computer se non esiste già.  

    - **Account**: specificare il nome utente e la password per l'account con le autorizzazioni per l'aggiunta al dominio specificato. Ad esempio: `domain\user` o `%variable%`.  

        > [!IMPORTANT]  
        > Se si prevede di eseguire la migrazione delle impostazioni del dominio o del gruppo di lavoro durante la distribuzione, assicurarsi di immettere le credenziali di dominio appropriate qui.  

1. Nella pagina **installa Configuration Manager** specificare il pacchetto client Configuration Manager. Questo pacchetto contiene i file di origine per installare il client di Configuration Manager. Specificare anche eventuali proprietà aggiuntive necessarie per installare il client.  

    Per altre informazioni, vedere [Proprietà di installazione client](/sccm/core/clients/deploy/about-client-installation-properties).

1. Nella pagina **Includi aggiornamenti** specificare se installare gli aggiornamenti software necessari, tutti gli aggiornamenti software o nessun aggiornamento software. Se si sceglie di installare gli aggiornamenti software, Configuration Manager installa solo quelli assegnati alle raccolte di cui il computer di destinazione è membro.  

1. Nella pagina **Installa applicazioni** specificare le applicazioni da installare nel computer di destinazione. Se si specificano più applicazioni, è possibile specificare che la sequenza di attività continui anche se l'installazione di un'applicazione specifica non riesce.  

    > [!NOTE]
    > La pagina **preparazione sistema** viene visualizzata successivamente nella procedura guidata, ma non viene più utilizzata. Selezionare **Avanti** per continuare.

1. Nella pagina **Proprietà immagini** specificare le seguenti impostazioni per l'immagine del sistema operativo:

    - **Creato da**: specificare il nome dell'utente da considerare come autore dell'immagine del sistema operativo.  

    - **Versione**: specificare il numero di versione associato all'immagine del sistema operativo. Questo attributo non deve essere la versione del sistema operativo, poiché il sito archivia tale valore separatamente.

    - **Descrizione**: specificare la descrizione dell'immagine del sistema operativo.  

1. Nella pagina **Acquisisci immagine** specificare le impostazioni seguenti:

    - **Percorso**: specificare una cartella di rete condivisa in cui Configuration Manager deve archiviare il file di immagine di output (con estensione wim). Questo file contiene l'immagine del sistema operativo basata sulle impostazioni specificate in questa procedura guidata. Se si specifica una cartella che contiene un oggetto esistente. Il file WIM viene sovrascritto.  

    - **Account**: specificare l'account di Windows con le autorizzazioni per la condivisione di rete in cui viene archiviata l'immagine.  

1. Completare la procedura guidata.  

Per aggiungere ulteriori passaggi alla sequenza di attività, selezionarla e scegliere **modifica**. Per altre informazioni su come modificare una sequenza di attività, vedere [Usare l'editor delle sequenze di attività](/sccm/osd/understand/task-sequence-editor).  

Distribuire la sequenza di attività in un computer di riferimento in uno dei modi seguenti:  

- Se il computer di riferimento è già un client di Configuration Manager, distribuire la sequenza di attività di creazione e acquisizione nella raccolta che contiene il computer di riferimento. Per altre informazioni, vedere [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence).

- Se il computer di riferimento non è un client di Configuration Manager o si vuole eseguire manualmente la sequenza di attività nel computer di riferimento, usare la **Creazione guidata del supporto per la sequenza di attività** per creare il supporto di avvio. Per altre informazioni, vedere [Creare supporti di avvio](/sccm/osd/deploy-use/create-bootable-media).  

Una volta acquisita l'immagine, è possibile distribuirla in altri computer. Per altre informazioni su come distribuire l'immagine del sistema operativo acquisita, vedere [creare una sequenza di attività per installare un sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-install-an-operating-system).  

## <a name="BKMK_CaptureExistingRefComputer"></a>Acquisisci da un computer di riferimento esistente

Se è già disponibile un computer di riferimento pronto per l'acquisizione, creare una sequenza di attività che acquisisce solo il sistema operativo dal computer di riferimento. Usare il passaggio **Acquisisci immagine del sistema operativo** della sequenza di attività per acquisire una o più immagini da un computer di riferimento e archiviarle in un file di immagine (con estensione wim) nella condivisione di rete specificata. Avviare il computer di riferimento in Windows PE con un'immagine di avvio. La sequenza di attività acquisisce ogni disco rigido nel computer di riferimento come immagine separata all'interno del file con estensione wim. Se il computer a cui si fa riferimento include più unità, il file con estensione wim risultante contiene un'immagine distinta per ogni volume. Acquisisce solo i volumi con formattazione NTFS o FAT32. I volumi con formati diversi o i volumi USB vengono ignorati.  

Usare la procedura seguente per acquisire un'immagine del sistema operativo da un computer di riferimento esistente:

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e quindi selezionare il nodo **Sequenze di attività**.  

1. Nella scheda **Home** della barra multifunzione nel gruppo **Crea** selezionare **Crea sequenza di attività**. Questa azione avvia la Creazione guidata della sequenza di attività.  

1. Nella pagina **Crea una nuova sequenza di attività** selezionare **Crea una nuova sequenza di attività personalizzata**.  

1. Nella pagina **informazioni sequenza di attività** specificare un nome per la sequenza di attività. Facoltativamente, aggiungere una descrizione per la sequenza di attività.  

1. Specificare un'immagine di avvio per la sequenza di attività. Configuration Manager usa questa immagine di avvio per avviare il computer di riferimento con Windows PE. Per altre informazioni, vedere [Manage boot images](/sccm/osd/get-started/manage-boot-images) (Gestire le immagini d'avvio).  

1. Completare la procedura guidata.  

1. Nel nodo **sequenze attività** selezionare la nuova sequenza di attività. Nella scheda **Home** della barra multifunzione selezionare quindi **Modifica** nel gruppo **Sequenza di attività**. Questa azione consente di aprire l'editor della sequenza di attività.  

1. Se il client di Configuration Manager è installato nel computer di riferimento:

    Scegliere **Immagini**dal menu **Aggiungi** , quindi [preparare il client ConfigMgr per l'acquisizione](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture). Questo passaggio generalizza il client di Configuration Manager nel computer di riferimento.

    > [!Note]  
    > La sequenza di attività non supporta la disinstallazione del client di Configuration Manager.

1. Passare al menu **Aggiungi** , selezionare **Immagini**e scegliere [prepara Windows per l'acquisizione](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareWindowsforCapture). Questo passaggio esegue Sysprep e quindi riavvia il computer nell'immagine di avvio di Windows PE specificata per la sequenza di attività. Per completare correttamente questa azione, non aggiungere il computer di riferimento a un dominio.

1. Passare al menu **Aggiungi** , selezionare **Immagini**e scegliere [Acquisisci immagine del sistema operativo](/sccm/osd/understand/task-sequence-steps#BKMK_CaptureOperatingSystemImage). Questo passaggio viene eseguito solo da Windows PE per acquisire le unità disco rigido nel computer di riferimento. Configurare le seguenti impostazioni:

    - **Nome** e **Descrizione**: facoltativamente, è possibile modificare il nome del passaggio della sequenza di attività e fornire una descrizione.  

    - **Destinazione**: specificare una cartella di rete condivisa in cui è archiviato il file WIM di output. Questo file contiene l'immagine del sistema operativo basata sulle impostazioni specificate tramite questa procedura guidata. Se si specifica una cartella che contiene un oggetto esistente. Il file WIM viene sovrascritto.  

    - **Descrizione**, **Versione**e **Creato da**: facoltativamente, fornire i dettagli relativi all'immagine da acquisire.  

    - **Account**: specificare l'account di Windows con le autorizzazioni per la condivisione di rete specificata. Selezionare **Imposta** per specificare il nome dell'account di Windows.  

Selezionare **OK** per salvare le modifiche e chiudere l'editor della sequenza di attività.  

Distribuire la sequenza di attività in un computer di riferimento in uno dei modi seguenti:  

- Se il computer di riferimento è già un client di Configuration Manager, distribuire la sequenza di attività di acquisizione nella raccolta che contiene il computer di riferimento. Per altre informazioni, vedere [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence).

- Se il computer di riferimento non è un client di Configuration Manager o si vuole eseguire manualmente la sequenza di attività nel computer di riferimento, usare la **Creazione guidata del supporto per la sequenza di attività** per creare il supporto di acquisizione. Per altre informazioni, vedere [Creare supporti di acquisizione](/sccm/osd/deploy-use/create-capture-media).  

Una volta acquisita l'immagine, è possibile distribuirla in altri computer. Per altre informazioni su come distribuire l'immagine del sistema operativo acquisita, vedere [creare una sequenza di attività per installare un sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-install-an-operating-system).

## <a name="BKMK_BuildandCaptureTSExample"></a>Sequenza di attività di esempio

Usare la tabella seguente come guida durante la creazione di una sequenza di attività che crea e acquisisce un'immagine del sistema operativo. La tabella è utile per decidere la sequenza generale per i passaggi della sequenza di attività e come organizzare e strutturare i passaggi in gruppi logici. La sequenza di attività creata può variare rispetto a questo esempio. Può contenere più o meno passaggi e gruppi.

> [!NOTE]  
> Usare sempre la Creazione guidata della sequenza attività per creare questo tipo di sequenza di attività.
>
> La procedura guidata aggiunge i passaggi alla sequenza di attività con nomi leggermente diversi che verrebbero visualizzati se si aggiungono manualmente gli stessi passaggi.

### <a name="group-build-the-reference-machine"></a>Gruppo: Crea computer di riferimento

Questo gruppo contiene le azioni necessarie per creare un computer di riferimento.

|Passaggio della sequenza di attività|Descrizione|  
|-------------------------------|---------------|  
|**Riavvia in Windows PE**|Riavviare il computer di destinazione per l'immagine di avvio assegnata alla sequenza di attività. Questo passaggio visualizza un messaggio all'utente per informarlo che il computer verrà riavviato in modo da poter continuare l'installazione.<br /><br />Questo passaggio usa la variabile della sequenza di attività `_SMSTSInWinPE` di sola lettura. Se il valore associato è uguale a `false`, il passaggio della sequenza di attività continua.|
|**Disco di partizione 0 - BIOS**|Partizionare e formattare il disco rigido nel computer di destinazione in modalità BIOS. Il numero di disco predefinito è `0`.<br /><br />Questo passaggio usa diverse variabili della sequenza di attività di sola lettura. Ad esempio, viene eseguito solo se la cache del client Configuration Manager non esiste e non viene eseguita se il computer è configurato per UEFI.|
|**Disco di partizione 0 - UEFI**|Partizionare e formattare il disco rigido nel computer di destinazione in modalità UEFI. Il numero di disco predefinito è `0`.<br /><br />Questo passaggio usa diverse variabili della sequenza di attività di sola lettura. Ad esempio, viene eseguito solo se la cache del client Configuration Manager non esiste e viene eseguita solo se il computer è configurato per UEFI.|
|**Applica sistema operativo**|Installare l'immagine del sistema operativo specificata nel computer di destinazione. Questo passaggio elimina prima di tutto tutti i file nel volume, ad eccezione dei file di controllo specifici di Configuration Manager. Applica quindi tutte le immagini del volume contenute nel file WIM al volume del disco sequenziale corrispondente nel computer di destinazione.|
|**Applica impostazioni Windows**|Configurare le impostazioni di Windows per il computer di destinazione.|
|**Applica impostazioni di rete**|Specificare le informazioni di configurazione di rete o del gruppo di lavoro per il computer di destinazione.|
|**Applica driver dispositivo**|Abbinare e installare i driver come parte della distribuzione del sistema operativo. Per altre informazioni, vedere [Applica automaticamente i driver](/sccm/osd/understand/task-sequence-steps#BKMK_AutoApplyDrivers).<br /><br />Questo passaggio usa la variabile della sequenza di attività `_SMSTSMediaType` di sola lettura. Se il valore associato non è uguale `FullMedia`, questo passaggio non viene eseguito.|
|**Installa Windows e Configuration Manager**|Installare il software client di Configuration Manager. Configuration Manager installa e registra il GUID del client di Configuration Manager. Includere tutte le **proprietà di installazione**necessarie.|
|**Installa aggiornamenti**|Specificare il modo in cui gli aggiornamenti software vengono installati nel computer di destinazione. Il computer di destinazione viene valutato alla ricerca di aggiornamenti software applicabili solo in corrispondenza con l'esecuzione di questo passaggio. A questo punto, la valutazione è simile a qualsiasi altro client gestito da Configuration Manager. Per altre informazioni, vedere [Installa aggiornamenti software](/sccm/osd/understand/install-software-updates).<br /><br />Questo passaggio usa la variabile della sequenza di attività `_SMSTSMediaType` di sola lettura. Se il valore associato non è uguale `FullMedia`, questo passaggio non viene eseguito.|
|**Installa applicazioni**|Specifica le applicazioni da installare nel computer di riferimento.|

### <a name="group-capture-the-reference-machine"></a>Gruppo: Acquisisci computer di riferimento

Questo gruppo contiene i passaggi necessari per preparare e acquisire un computer di riferimento.

|Passaggio della sequenza di attività|Descrizione|  
|-------------------------------|---------------|  
|**Prepara client di Configuration Manager**|Generalizzare il client di Configuration Manager nel computer di riferimento.|
|**Prepara sistema operativo**|Esegue Sysprep per generalizzare le finestre. Riavvia quindi il computer nell'immagine di avvio di Windows PE specificata per la sequenza di attività.|
|**Acquisisci computer di riferimento**|Acquisisce l'immagine nella condivisione di rete specificata e. File WIM.|

> [!IMPORTANT]
> Una volta acquisita un'immagine da un computer di riferimento, non acquisire un'altra immagine del sistema operativo dal computer di riferimento. Le voci del registro di sistema vengono create durante la configurazione iniziale. Creare un nuovo computer di riferimento ogni volta che si acquisisce l'immagine del sistema operativo. Se si prevede di usare lo stesso computer di riferimento per creare immagini del sistema operativo future, disinstallare e reinstallare il client di Configuration Manager.

## <a name="next-steps"></a>Passaggi successivi

[Metodi per distribuire i sistemi operativi aziendali](/sccm/osd/deploy-use/methods-to-deploy-enterprise-operating-systems)

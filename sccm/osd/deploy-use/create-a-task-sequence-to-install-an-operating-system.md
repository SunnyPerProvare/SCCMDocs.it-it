---
title: "Creare una sequenza di attività per installare un sistema operativo | Microsoft Docs"
description: "Usare le sequenze di attività in System Center Configuration Manager per installare automaticamente l&quot;immagine di un sistema operativo o altro contenuto su un computer di destinazione."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 217c8a0e-5112-420e-a325-2a6d75326290
caps.latest.revision: 13
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: 41aa6cf69a746f0ab67d804f1ee0c70db05d65ee


---
# <a name="create-a-task-sequence-to-install-an-operating-system-in-system-center-configuration-manager"></a>Creare una sequenza di attività per installare un sistema operativo in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare le sequenze di attività in System Center Configuration Manager per installare automaticamente l'immagine di un sistema operativo su un computer di destinazione. Creare una sequenza di attività che faccia riferimento a un'immagine di avvio usata per avviare il computer di destinazione, all'immagine del sistema operativo da installare nel computer di destinazione e qualsiasi altro contenuto aggiuntivo, ad esempio altre applicazioni o aggiornamenti software, che si vuole installare. Distribuire quindi la sequenza di attività in una raccolta che contiene il computer di destinazione.  

##  <a name="a-namebkmkinstallosa-create-a-task-sequence-to-install-an-operating-system"></a><a name="BKMK_InstallOS"></a> Creare una sequenza di attività per installare un sistema operativo  
 Esistono molti scenari per la distribuzione di un sistema operativo nei computer dell'ambiente. Nella maggior parte dei casi, è necessario creare una sequenza di attività e selezionare **Installa un pacchetto immagine esistente** nella Creazione guidata della sequenza di attività per installare il sistema operativo, eseguire la migrazione delle impostazioni utente, applicare gli aggiornamenti software e installare le applicazioni. Prima di creare una sequenza di attività per installare un sistema operativo, devono essere disponibili gli elementi seguenti:   

-   **Richiesto**  

    -   Nella console di Configuration Manager deve essere disponibile un'[immagine di avvio](../get-started/manage-boot-images.md).  

    -   Nella console di Configuration Manager deve essere disponibile un'[immagine del sistema operativo](../get-started/manage-operating-system-images.md).  

-   **Obbligatorio (se usato)**  

    -   Gli [aggiornamenti software](../../sum/get-started/synchronize-software-updates.md) devono essere sincronizzati nella console di Configuration Manager.  

    -   Le [applicazioni](../../apps/deploy-use/create-applications.md) devono essere aggiunte alla console di Configuration Manager.  

#### <a name="to-create-a-task-sequence-that-installs-an-operating-system"></a>Per creare una sequenza di attività che installi un sistema operativo  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea sequenza di attività** per avviare la Creazione guidata della sequenza di attività.  

4.  Nella pagina **Crea una nuova sequenza di attività** fare clic su **Installa un pacchetto immagine esistente**, quindi fare clic su **Avanti**.  

5.  Nella pagina **Informazioni sequenza di attività** specificare le impostazioni seguenti e quindi fare clic su **Avanti**.  

    -   **Nome sequenza di attività**: specificare un nome che identifica la sequenza di attività.  

    -   **Descrizione**: specificare una descrizione dell'attività eseguita dalla sequenza di attività.  

    -   **Immagine di avvio**: specificare l'immagine di avvio che installa il sistema operativo nel computer di destinazione. L'immagine di avvio contiene una versione di Windows PE usata per installare il sistema operativo e i driver di dispositivo aggiuntivi richiesti. Per altre informazioni, vedere [Gestire le immagini di avvio](../get-started/manage-boot-images.md).  

        > [!IMPORTANT]  
        >  L'architettura dell'immagine di avvio deve essere compatibile con l'architettura hardware del computer di destinazione.  

6.  Nella pagina **Installa Windows** specificare le impostazioni seguenti e quindi fare clic su **Avanti**.  

    -   **Pacchetto immagine**: specificare il pacchetto che contiene l'immagine del sistema operativo da installare. Per altre informazioni, vedere [Gestire le immagini del sistema operativo](../get-started/manage-operating-system-images.md).  

    -   **Immagine**: se il pacchetto immagine del sistema operativo contiene più immagini, specificare l'indice dell'immagine del sistema operativo da installare.  

    -   **Creare partizioni e formattare il computer di destinazione prima di installare il sistema operativo**: specificare se si desidera che la sequenza di attività partizioni e formatti il computer di destinazione prima dell'installazione del sistema operativo.  

    -   **Codice Product key**: specificare il codice Product Key per il sistema operativo Windows da installare. È possibile specificare i codici Product Key per contratti multilicenza codificati e i codici Product Key standard. Se si usa un codice Product Key non codificato, ogni gruppo di 5 caratteri deve essere separato da un trattino (-). Ad esempio: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   **Modalità di gestione licenze del server**: specificare che la licenza del server è **Per postazione**, **Per server**o che non è specificata alcuna licenza. Se la licenza del server è **Per server**, specificare anche il numero massimo di connessioni al server.  

    -   Specificare come gestire l'account amministratore usato quando viene distribuita l'immagine del sistema operativo.  

        -   **Disabilita account amministratore locale**: specificare se l'account di amministratore locale viene disabilitato quando viene distribuita l'immagine del sistema operativo.  

        -   **Attiva l'account e specifica la password dell'amministratore locale**: specificare se la stessa password viene usata per l'account di amministratore locale su tutti i computer in cui viene distribuita l'immagine del sistema operativo.  

7.  Nella pagina **Configura rete** specificare le impostazioni seguenti e quindi fare clic su **Avanti**.  

    -   **Aggiunta a un gruppo di lavoro**: specificare se aggiungere il computer di destinazione a un gruppo di lavoro.  

    -   **Aggiunta a un dominio**: specificare se aggiungere il computer di destinazione a un dominio. In **Dominio**specificare il nome del dominio.  

        > [!IMPORTANT]  
        >  È possibile cercare i domini nella foresta locale, ma è necessario specificare il nome di dominio per una foresta remota.  

         È inoltre possibile specificare un'unità organizzativa. Si tratta di un'impostazione facoltativa che specifica il nome distinto LDAP X.500 dell'unità organizzativa in cui creare l'account computer se non esiste già.  

    -   **Account**: specificare il nome utente e la password per l'account con le autorizzazioni per l'aggiunta al dominio specificato. Ad esempio: *dominio\utente* o *%variabile%*.  

        > [!IMPORTANT]  
        >  Se si prevede di migrare le impostazioni del dominio o le impostazioni del gruppo di lavoro, è necessario immettere le credenziali di dominio appropriate.  

8.  Nella pagina **Installa Configuration Manager** specificare il pacchetto client di Configuration Manager da installare nel computer di destinazione e quindi fare clic su **Avanti**.  

9. Nella pagina **Migrazione stato** specificare le informazioni seguenti e quindi fare clic su **Avanti**.  

    -   **Acquisisci impostazioni utente**: specificare se la sequenza di attività acquisisce lo stato utente. Per altre informazioni su come acquisire e ripristinare lo stato utente, vedere [Gestire lo stato utente](../get-started/manage-user-state.md).  

    -   **Acquisisci impostazioni di rete**: specificare se la sequenza di attività acquisisce le impostazioni di rete dal computer di destinazione. È possibile acquisire l'appartenenza del dominio o del gruppo di lavoro oltre alle impostazioni della scheda di rete.  

    -   **Acquisisci impostazioni di Microsoft Windows**:  specificare se la sequenza di attività acquisisce le impostazioni di Windows dal computer di destinazione prima dell'installazione dell'immagine del sistema operativo. È possibile acquisire il nome del computer, il nome dell'utente registrato e dell'organizzazione e le impostazioni di fuso orario.  

10. Nella pagina **Includi aggiornamenti** specificare se installare gli aggiornamenti software necessari, tutti gli aggiornamenti software o nessun aggiornamento software e quindi fare clic su **Avanti**. Se si sceglie di installare gli aggiornamenti software, Configuration Manager installa solo quelli assegnati alle raccolte di cui il computer di destinazione è membro.  

11. Nella pagina **Installa applicazioni** specificare le applicazioni da installare nel computer di destinazione e quindi fare clic su **Avanti**. Se si specificano più applicazioni, è possibile specificare che la sequenza di attività continui anche se l'installazione di un'applicazione specifica non riesce.  

12. Completare la procedura guidata.  

 Ora è possibile distribuire la sequenza di attività in una raccolta di computer.  Per altre informazioni, vedere [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

##  <a name="a-namebkmkinstallexistingosimagetsexamplea-example-task-sequence-to-install-an-existing-operating-system-image"></a><a name="BKMK_InstallExistingOSImageTSExample"></a> Esempio di sequenza di attività per l'installazione di un'immagine del sistema operativo esistente  
 Usare la tabella seguente come guida durante la creazione di una sequenza di attività per la distribuzione di un sistema operativo con un'immagine del sistema operativo esistente. La tabella sarà utile per decidere la sequenza generale per i passaggi della sequenza di attività e per determinare come organizzare e strutturare tali passaggi in gruppi logici. La sequenza di attività creata può variare rispetto a questo esempio e può contenere un numero minore o maggiore di passaggi e gruppi.  

> [!IMPORTANT]  
>  Usare sempre la Creazione guidata della sequenza attività per creare questa sequenza di attività.  

 Quando si usa la Creazione guidata della sequenza attività per creare questa nuova sequenza di attività, alcuni nomi dei passaggi potrebbero essere diversi rispetto a quelli che verrebbero usati aggiungendo manualmente i passaggi a una sequenza di attività esistente. La tabella seguente mostra le differenze di denominazione:  

|Nome del passaggio della sequenza di attività di Creazione guidata della sequenza di attività|Nome del passaggio equivalente dell'editor delle sequenze di attività|  
|---------------------------------------------------------|-----------------------------------------------|  
|Archiviazione dello stato utente richiesta|Richiedi archiviazione stati|  
|Acquisizione file e impostazioni utente|Acquisisci stato utente|  
|Archiviazione dello stato utente di rilascio|Rilascia archiviazione stati|  
|Riavvia in Windows PE|Riavvia in Windows PE o usando il disco rigido|  
|Disco di partizione 0|Formato e disco partizione|  
|Ripristinare file e impostazioni utente|Ripristina stato utente|  

|Passaggio o gruppo di sequenze di attività|Descrizione|  
|---------------------------------|-----------------|  
|Acquisire i File e impostazioni - **(nuovo gruppo di sequenze attività)**|Creare un gruppo di sequenze di attività. Un gruppo di sequenze di attività consente di mantenere simile passaggi della sequenza attività per una migliore organizzazione e il controllo degli errori.<br /><br /> Questo gruppo contiene i passaggi necessari per l'acquisizione di file e impostazioni dal sistema operativo del computer di riferimento.|  
|Acquisisci impostazioni Windows|Usare questo passaggio della sequenza di attività per identificare le impostazioni di Microsoft Windows per l'acquisizione dal computer di riferimento. È possibile acquisire il nome computer, informazioni sull'utente e sull'organizzazione e le impostazioni di fuso orario.|  
|Acquisisci impostazioni di rete|Usare questo passaggio della sequenza di attività per acquisire le impostazioni di rete dal computer di riferimento. È possibile acquisire l'appartenenza al gruppo di lavoro o dominio del computer di riferimento e impostazione delle informazioni relative alla scheda di rete.|  
|Acquisire i file utente e impostazioni - **(nuovo gruppo sequenza attività secondarie)**|Creare un gruppo di sequenze di attività all'interno di un gruppo di sequenze di attività. Questo sottogruppo contiene i passaggi necessari per acquisire dati dello stato utente. Analogamente al gruppo iniziale aggiunto, questo sottogruppo tiene uniti i passaggi delle sequenze di attività per una migliore organizzazione e un maggiore controllo degli errori.|  
|Archiviazione dello stato utente richiesta|Usare questo passaggio della sequenza di attività per richiedere l'accesso a un punto di migrazione stato in cui sono archiviati i dati dello stato utente. È possibile configurare questo passaggio della sequenza di attività per acquisire o ripristinare le informazioni sullo stato utente.|  
|Acquisisci file utente e impostazioni|Usare questo passaggio della sequenza di attività per usare l'Utilità di migrazione stato utente per acquisire lo stato utente e le impostazioni dal computer di riferimento che riceve la sequenza di attività associata a questo passaggio. È possibile acquisire le opzioni standard o configurare le opzioni specifiche da acquisire.|  
|Rilascia archiviazione stato utente|Utilizzare questo passaggio della sequenza attività per notificare lo stato punto di migrazione che l'azione di ripristino o acquisizione è stata completata.|  
|Installare il sistema operativo - **(nuovo gruppo di sequenze attività)**|Creare un altro gruppo secondario di sequenze attività. Questo gruppo secondario contiene i passaggi necessari per installare e configurare l'ambiente Windows PE.|  
|Riavvia in Windows PE|Utilizzare questo passaggio della sequenza attività per specificare le opzioni di riavvio del computer di destinazione che riceve questa sequenza di attività. Questo passaggio viene visualizzato un messaggio all'utente che indica che il computer verrà riavviato affinché possa continuare l'installazione.<br /><br /> Questo passaggio usa la variabile della sequenza di attività **_SMSTSInWinPE** di sola lettura. Se il valore associato è uguale a **false** il passaggio della sequenza attività continua.|  
|Partizione disco 0|Questo passaggio della sequenza attività specifica le azioni necessarie per formattare il disco rigido nel computer di destinazione. Il numero di disco predefinito è **0**.<br /><br /> Questo passaggio usa la variabile della sequenza di attività **_SMSTSClientCache** di sola lettura. Questo passaggio verrà eseguito se la cache del client di Configuration Manager non esiste.|  
|Applica sistema operativo|Utilizzare questo passaggio della sequenza attività per installare l'immagine del sistema operativo nel computer di destinazione. Questo passaggio applica tutte le immagini di volume contenute nel file WIM al volume del disco sequenziale corrispondente nel computer di destinazione, dopo aver prima eliminato tutti i file in tale volume (ad eccezione dei file di controllo specifici di Configuration Manager). È possibile specificare un **sysprep** file di risposte e inoltre configurare la partizione del disco viene utilizzata per l'installazione.|  
|Applica impostazioni Windows|Usare questo passaggio della sequenza di attività per configurare le informazioni di configurazione delle impostazioni di Windows per il computer di destinazione. Le impostazioni di Windows applicabili sono le informazioni sull'utente e sull'organizzazione, le informazioni sul prodotto o sul codice di licenza, il fuso orario e la password dell'amministratore locale.|  
|Applica impostazioni di rete|Usare questo passaggio della sequenza di attività per specificare le informazioni di configurazione per la rete o il gruppo di lavoro per il computer di destinazione. È inoltre possibile specificare se il computer utilizza un server DHCP oppure è possibile assegnare staticamente le informazioni sull'indirizzo IP.|  
|Applica driver dispositivo|Utilizzare questo passaggio della sequenza attività per installare i driver come parte della distribuzione del sistema operativo. È possibile consentire a Installazione di Windows di cercare tutte le categorie di driver esistenti selezionando **Considera i driver di tutte le categorie** oppure limitare le categorie in cui Installazione di Windows esegue la ricerca selezionando **Limita la corrispondenza dei driver in modo da considerare solo i driver delle categorie selezionate**.<br /><br /> Questo passaggio viene utilizzata la proprietà di sola lettura **_SMSTSMediaType** variabile della sequenza attività. Questo passaggio della sequenza attività viene eseguita solo se il valore della variabile non è uguale **FullMedia**.|  
|Applica pacchetto di driver|Utilizzare questo passaggio della sequenza attività per rendere disponibili per l'utilizzo tutti i driver di dispositivo in un pacchetto driver dal programma di installazione di Windows.|  
|Installazione del sistema operativo - **(nuovo gruppo di sequenze attività)**|Creare un altro gruppo secondario di sequenze attività. Questo sottogruppo contiene i passaggi necessari per configurare il sistema operativo installato.|  
|Imposta Windows e ConfigMgr|Usare questo passaggio della sequenza di attività per installare il software client di Configuration Manager. Configuration Manager installa e registra il GUID del client di Configuration Manager. È possibile assegnare i parametri di installazione necessari nella finestra **Proprietà di installazione** .|  
|Installa aggiornamenti|Usare questo passaggio della sequenza di attività per specificare in che modo gli aggiornamenti software vengono installati nel computer di destinazione. Il computer di destinazione viene valutato alla ricerca di aggiornamenti software applicabili solo in corrispondenza con l'esecuzione di questo passaggio della sequenza di attività, quando il computer di destinazione viene valutato alla ricerca di aggiornamenti software applicabili in modo simile agli altri client gestiti da Configuration Manager.<br /><br /> Questo passaggio usa la variabile della sequenza di attività **_SMSTSMediaType** di sola lettura. Questo passaggio della sequenza di attività viene eseguito solo se il valore della variabile è diverso da **FullMedia**.|  
|Ripristina file utente e impostazioni - **(Nuovo sottogruppo di sequenze di attività)**|Creare un altro gruppo secondario di sequenze attività. Questo sottogruppo contiene i passaggi necessari per ripristinare i file utente e le impostazioni.|  
|Richiedi archiviazione stato utente|Utilizzare questo passaggio della sequenza attività per richiedere l'accesso a un punto di migrazione stato archiviazione i dati dello stato utente.|  
|Ripristina file utente e impostazioni|Usare questo passaggio della sequenza di attività per avviare l'Utilità di migrazione stato utente e ripristinare lo stato utente e le impostazioni in un computer di destinazione.|  
|Archiviazione dello stato utente di rilascio|Usare questo passaggio della sequenza di attività per segnalare al punto di migrazione stato che i dati dello stato utente non sono più necessari.|  



<!--HONumber=Dec16_HO3-->



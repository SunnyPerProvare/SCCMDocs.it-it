---
title: Gestire i punti di distribuzione | Microsoft Docs
description: Ospitare il contenuto (file e software) distribuito a utenti e dispositivi tramite punti di distribuzione. Ecco come installarli e configurarli.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1a4a9da88caba55d9e340c7fb1f31f4e3b957f3e
ms.openlocfilehash: 8684bf1231ff9d663717b4c9874dac98d50e3647

---
# <a name="install-and-configure-distribution-points-for-system-center-configuration-manager"></a>Installare e configurare punti di distribuzione per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile installare punti di distribuzione di System Center Configuration Manager per ospitare il contenuto (file e software) distribuito a utenti e dispositivi. È anche possibile creare gruppi di punti di distribuzione per semplificare la gestione dei punti di distribuzione e la distribuzione di contenuto ai punti di distribuzione stessi.  

 Quando si **installa un nuovo punto di distribuzione** tramite l'installazione guidata o si **gestiscono le proprietà di un punto di distribuzione esistente** modificando tali proprietà, è possibile configurare la maggior parte delle impostazioni dei punti di distribuzione. Alcune impostazioni, tuttavia, sono disponibili solo durante l'installazione o la modifica, ma non in entrambi i casi:  

-   **Impostazioni disponibili solo quando si installa un punto di distribuzione:**  

    -   Consentire a Configuration Manager di installare IIS nel computer del punto di distribuzione  

    -   Configurare le impostazioni dello spazio dell'unità per il punto di distribuzione  

-   **Passaggi di impostazione disponibili solo quando si modificano le proprietà di un punto di distribuzione:**  

    -   Gestire le relazioni del gruppo di punti di distribuzione  

    -   Visualizzare il contenuto distribuito nel punto di distribuzione  

    -   Configurare i limiti di velocità per i trasferimenti di dati ai punti di distribuzione  

    -   Configurare le pianificazioni per i trasferimenti di dati ai punti di distribuzione  

##  <a name="a-namebkmkinstalla-install-a-distribution-point"></a><a name="bkmk_install"></a> Installare un punto di distribuzione  
 Prima che il contenuto possa essere reso disponibile nei computer client, è necessario designare un server del sistema del sito come punto di distribuzione. È possibile aggiungere il ruolo del sito del punto di distribuzione a un nuovo server del sistema del sito oppure aggiungere il ruolo del sito a un server del sistema del sito esistente.  

 Quando si installa un nuovo punto di distribuzione, si usa un'installazione guidata che illustra le impostazioni disponibili. Prima di iniziare, si tenga presente quanto segue:  

-   È necessario disporre delle seguenti autorizzazioni di sicurezza per creare e configurare un punto di distribuzione:  

    -   **Lettura** per l'oggetto **Punto di distribuzione**  

    -   **Copia nel punto di distribuzione** per l'oggetto **Punto di distribuzione**  

    -   **Modifica** per l'oggetto **Sito**  

    -   **Gestisci certificati per distribuzione sistema operativo** per l'oggetto **Sito**  

-   IIS deve essere installato nel server che ospiterà il punto di distribuzione. Quando si installa il ruolo del sistema del sito, Configuration Manager può eseguire l'installazione e la configurazione di IIS.  

Usare le procedure di base seguenti per installare o modificare un punto di distribuzione. Fare riferimento alla sezione [Configurazioni dei punti di distribuzione](#bkmk_configs) di questo argomento per informazioni dettagliate sulle opzioni di configurazione disponibili.  

#### <a name="to-install-a-distribution-point"></a>Per installare un punto di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** >  **Configurazione del sito** > **Server e ruoli di sistema del sito**.  

2.  Aggiungere il ruolo del sistema del sito del punto di distribuzione a un server del sistema del sito nuovo o esistente:  

    -   **Nuovo server del sistema sito**: nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea server di sistema sito**. Viene visualizzata la Creazione guidata server del sistema sito.  

    -   **Server del sistema del sito esistente**: Selezionare il server in cui si desidera installare il ruolo del sistema sito del punto di distribuzione. Quando si seleziona un server, nel riquadro dei risultati viene visualizzato un elenco dei ruoli del sistema del sito già installati nel server.  

         Nella scheda **Home** , nel gruppo **Server** , fare clic su **Aggiungi ruoli del sistema del sito**. Verrà visualizzata la finestra di Aggiunta guidata ruoli del sistema del sito.  

3.  Nella scheda **Generale** specificare le impostazioni generali per il server del sistema del sito. Quando si aggiunge il punto di distribuzione a un server del sistema del sito esistente, verificare i valori configurati in precedenza.  

4.  Nella pagina **Selezione ruolo del sistema** selezionare **Punto di distribuzione** dall'elenco dei ruoli disponibili, quindi fare clic su **Avanti**.  

5.  Per completare le pagine successive della procedura guidata quando richiesto, fare riferimento alle informazioni nella sezione [Configurazioni dei punti di distribuzione](#bkmk_configs).  

     Ad esempio, per installare il punto di distribuzione come punto di distribuzione pull, selezionare **Abilita il pull di contenuti di questo punto di distribuzione da altri punti di distribuzione** e quindi definire le configurazioni aggiuntive richieste dai punti di distribuzione pull.  

6.  Al termine della procedura guidata, viene aggiunto il ruolo del sito del punto di distribuzione al server di sistema del sito.  

#### <a name="to-modify-a-distribution-point"></a>Per modificare un punto di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** >  **Punti di distribuzione** e quindi selezionare il punto di distribuzione da configurare.  

2.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

3.  Durante la modifica delle proprietà del punto di distribuzione usare le informazioni nella sezione [Configurazioni dei punti di distribuzione](#bkmk_configs).  

4.  Dopo aver apportato le modifiche desiderate, salvare le impostazioni e chiudere le proprietà del punto di distribuzione.  

##  <a name="a-namebkmkmanagea-manage-distribution-point-groups"></a><a name="bkmk_manage"></a> Gestire i gruppi di punti di distribuzione  
 I gruppi di punti di distribuzione offrono un raggruppamento logico dei punti di distribuzione per la distribuzione del contenuto. È possibile usare tali gruppi per gestire e monitorare il contenuto da una posizione centrale per i punti di distribuzione che si estendono su più siti  

-   È possibile aggiungere uno o più punti di distribuzione da qualsiasi sito nella gerarchia al gruppo di punti di distribuzione  

-   È possibile aggiungere un punto di distribuzione a più di un gruppo di punti di distribuzione  

-   Quando distribuisce il contenuto a un gruppo di punti di distribuzione, Configuration Manager lo distribuisce in tutti i punti di distribuzione membri del gruppo di punti di distribuzione  

-   Se si aggiunge un punto di distribuzione al gruppo di punti di distribuzione dopo una distribuzione iniziale del contenuto, Configuration Manager esegue la distribuzione automatica del contenuto nel nuovo membro del punto di distribuzione  

-   È possibile associare una raccolta a un gruppo di punti di distribuzione. Quindi, quando si distribuisce contenuto a tale raccolta, Configuration Manager determina i gruppi di punti di distribuzione associati alla raccolta e il contenuto viene distribuito in tutti i punti di distribuzione membri dei gruppi di punti di distribuzione  

    > [!NOTE]  
    >  Dopo la distribuzione di contenuto a una raccolta, se si associa la raccolta a un nuovo gruppo di punti di distribuzione, sarà necessario ridistribuire il contenuto alla raccolta prima che il contenuto sia distribuito al nuovo gruppo di punti di distribuzione.  

#### <a name="to-create-and-configure-a-new-distribution-point-group"></a>Per creare e configurare un nuovo gruppo di punti di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Punti di distribuzione**.  

2.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea gruppo**.  

3.  Immettere il nome e la descrizione per il gruppo di punti di distribuzione.  

4.  Nella scheda **Raccolte** fare clic su **Aggiungi**, selezionare le raccolte da associare al gruppo di punti di distribuzione e quindi fare clic su **OK**.  

5.  Nella scheda **Membri** fare clic su **Aggiungi**, selezionare i punti di distribuzione da aggiungere come membri del gruppo di punti di distribuzione e quindi fare clic su **OK**.  

6.  Fare clic su **OK** per creare il gruppo di punti di distribuzione.  

#### <a name="to-add-distribution-points-and-associate-collections-to-an-existing-distribution-point-group"></a>Per aggiungere i punti di distribuzione e associare le raccolte a un gruppo di punti di distribuzione esistente  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Punti di distribuzione**.  

2.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

3.  Nella scheda **Raccolte** fare clic su **Aggiungi** per selezionare le raccolte da associare al gruppo di punti di distribuzione e quindi fare clic su **OK**.  

4.  Nella scheda **Membri** fare clic su **Aggiungi** per selezionare i punti di distribuzione da aggiungere come membri del gruppo di punti di distribuzione e quindi fare clic su **OK**.  

5.  Fare clic su **OK** per salvare le modifiche apportate al gruppo di punti di distribuzione.  

#### <a name="to-add-selected-distribution-points-to-a-new-distribution-point-group"></a>Per aggiungere i punti di distribuzione selezionati a un nuovo gruppo di punti di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Punti di distribuzione** e quindi selezionare i punti di distribuzione da aggiungere al nuovo gruppo di punti di distribuzione.  

2.  Nella scheda **Home** , nel gruppo **Punto di distribuzione** , espandere **Aggiungi elementi selezionati**e quindi fare clic su **Aggiungi elementi selezionati a nuovo gruppo di punti di distribuzione**.  

3.  Immettere il nome e la descrizione per il gruppo di punti di distribuzione.  

4.  Nella scheda **Raccolte** fare clic su **Aggiungi** per selezionare le raccolte da associare al gruppo di punti di distribuzione e quindi fare clic su **OK**.  

5.  Nella scheda **Membri** confermare che Configuration Manager debba aggiungere i punti di distribuzione elencati come membri del gruppo di punti di distribuzione. Fare clic su **Aggiungi** per modificare i punti di distribuzione da aggiungere come membri del gruppo di punti di distribuzione e quindi fare clic su **OK**.  

6.  Fare clic su **OK** per creare il gruppo di punti di distribuzione.  

#### <a name="to-add-selected-distribution-points-to-existing-distribution-point-groups"></a>Per aggiungere i punti di distribuzione selezionati ai gruppi di punti di distribuzione esistenti  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Punti di distribuzione** e quindi selezionare i punti di distribuzione da aggiungere al nuovo gruppo di punti di distribuzione.  

2.  Nella scheda **Home** , nel gruppo **Punto di distribuzione** , espandere **Aggiungi elementi selezionati**e quindi fare clic su **Aggiungi elementi selezionati a gruppi di punti di distribuzione esistenti**.  

3.  In **Gruppi di punti di distribuzione disponibili**selezionare i gruppi di punti di distribuzione a cui aggiungere i punti di distribuzione selezionati come membri e quindi fare clic su **OK**.  

##  <a name="a-namebkmkconfigsa-distribution-point-configurations"></a><a name="bkmk_configs"></a> Configurazioni dei punti di distribuzione  
 I singoli punti di distribuzione supportano un'ampia gamma di configurazioni diverse. Tuttavia, non tutti i tipi di punto di distribuzione supportano tutte le configurazioni. Ad esempio, i punti di distribuzione basati su cloud non supportano distribuzioni del contenuto abilitate per PXE o multicast. È possibile trovare informazioni sui limiti specifici negli argomenti seguenti:  

-   [Use a cloud-based distribution point with System Center Configuration Manager](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) (Usare un punto di distribuzione basato sul cloud con System Center Configuration Manager)  

-   [Use a pull-distribution point with System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point) (Usare un punto di distribuzione pull con System Center Configuration Manager)  

Le sezioni seguenti descrivono le configurazioni che è possibile selezionare quando si installa un nuovo punto di distribuzione o si modificano le proprietà di un punto di distribuzione esistente:  

### <a name="general"></a>Generale  
 Configurare le impostazioni generali del punto di distribuzione:  

-   **Installa e configura IIS se richiesto da Configuration Manager**: selezionare questa impostazione per consentire a Configuration Manager di installare e configurare Internet Information Services (IIS) nel server, se non ancora installato. IIS deve essere installato su tutti i punti di distribuzione. Se IIS non è installato sul server e non viene selezionata questa impostazione, è necessario installare IIS prima di poter installare correttamente il punto di distribuzione.  

    > [!NOTE]  
    >  Questa opzione è disponibile solo quando si installa un nuovo punto di distribuzione  

-   **Specificare in che modo i computer client o i dispositivi mobili comunicano con questo punto di distribuzione:** esistono vantaggi e svantaggi associati all'uso di HTTP e HTTPS. Per altre informazioni, vedere *Security best practices for content management* (Procedure di sicurezza consigliate per la gestione del contenuto) in [Fundamental concepts for content management in System Center Configuration Manager](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md) (Concetti di base per la gestione dei contenuti in System Center Configuration Manager).  

-   **Consenti connessione anonima dei client:** questa impostazione permette di specificare se il punto di distribuzione consentirà connessioni anonime dai client di Configuration Manager alla raccolta contenuto.  

    > [!IMPORTANT]  
    >  Se non si usa questa impostazione, il ripristino di un'applicazione di Windows Installer in un client può non riuscire.  
    >   
    >  -   Quando viene distribuita un'applicazione di Windows Installer in un client di Configuration Manager, Configuration Manager scarica il file nella cache locale del client e i file vengono rimossi al termine dell'installazione.  
    > -   Il client di Configuration Manager aggiorna l'elenco di origine di Windows Installer per le applicazioni di Windows Installer installate con il percorso contenuto per la raccolta contenuto sui punti di distribuzione associati.  
    > -   Se successivamente si avvia l'azione di ripristino da Installazione applicazioni in un client di Configuration Manager, MSIExec prova ad accedere al percorso del contenuto usando un utente anonimo.  
    >   
    >  È comunque possibile installare l'aggiornamento descritto nell'articolo [2619572](http://go.microsoft.com/fwlink/?LinkId=279699) della Microsoft Knowledge Base e quindi modificare una chiave del Registro di sistema per cambiare questo comportamento.  
    >   
    >  -   Dopo che l'aggiornamento è stato installato nei client, MSIExec accederà al percorso del contenuto usando l'account utente connesso, a meno che non sia selezionata l'impostazione **Consenti connessione anonima dei client**  

-   **Creare un certificato autofirmato o importare un certificato client PKI:** il certificato ha gli scopi seguenti:  

    -   Consente l'autenticazione tra il punto di distribuzione e un punto di gestione prima che il punto di distribuzione invii messaggi di stato.  

    -   Quando la casella di controllo **Abilita supporto PXE per i client** è selezionata nella pagina **Impostazioni PXE** , il certificato viene inviato ai computer che eseguono un avvio PXE in modo che possano connettersi a un punto di gestione durante la distribuzione del sistema operativo.  

    Quando tutti i punti di gestione nel sito sono configurati per il protocollo HTTP, è necessario creare un certificato autofirmato. Quando i punti di gestione sono configurati per HTTPS, importare un certificato client PKI.  

    Per importare il certificato, cercare un file Public-Key Cryptography Standards (PKCS #12) che contenga un certificato PKI con i seguenti requisiti per Configuration Manager:  

    -   Lo scopo designato deve includere l'autenticazione client.  

    -   La chiave privata deve essere abilitata per l'esportazione.  

    > [!TIP]  
    >  Non sono previsti requisiti specifici per l'oggetto certificato o il nome alternativo oggetto (SAN) ed è possibile usare lo stesso certificato per più punti di distribuzione.  

     Per altre informazioni sui requisiti dei certificati, vedere [Requisiti dei certificati PKI per System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

     Per un esempio di distribuzione di questo certificato, vedere la sezione *Distribuzione del certificato di servizio per i punti di distribuzione* nell'argomento [Esempio dettagliato di distribuzione dei certificati PKI per System Center Configuration Manager: Autorità di certificazione di Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

-   **Abilita questo punto di distribuzione per il contenuto pre-installato**: selezionare questa impostazione per abilitare il punto di distribuzione per il contenuto pre-installato. Quando questa impostazione è selezionata, è possibile configurare il comportamento per la distribuzione del contenuto. È possibile scegliere se preinstallare sempre il contenuto nel punto di distribuzione, se preinstallare il contenuto iniziale per il pacchetto, ma usare il processo di distribuzione del contenuto normale in presenza di aggiornamenti del contenuto oppure usare sempre il processo di distribuzione del contenuto normale per il contenuto nel pacchetto.  

### <a name="drive-settings"></a>Impostazioni unità  

> [!NOTE]  
>  Queste opzioni sono disponibili solo quando si installa un nuovo punto di distribuzione  

Specificare le impostazioni unità per il punto di distribuzione. È possibile configurare fino a due unità disco per la raccolta contenuto e due unità disco per la condivisione pacchetto, sebbene Configuration Manager possa usare unità aggiuntive nel caso in cui le prime due raggiungano il limite di spazio riservato nell'unità configurata. Nella pagina **Impostazioni unità** è possibile configurare la priorità per le unità disco e la quantità di spazio disponibile su disco da conservare su ciascuna unità disco.  

-   **Spazio riservato nell'unità (MB)**: il valore configurato per questa impostazione determina la quantità di spazio disponibile su un'unità prima che Configuration Manager scelga un'altra unità e continui il processo di copia su tale unità. I file di contenuto possono estendersi su più unità.  

-   **Posizioni contenuto:** specificare le posizioni del contenuto per la condivisione di pacchetti e raccolte contenuto. Configuration Manager copia i contenuti nel percorso del contenuto principale finché la quantità di spazio libero raggiunge il valore specificato per **Riserva spazio su disco (MB)**. Per impostazione predefinita, i percorsi contenuto sono impostati su **Automatico**. Il percorso del contenuto primario è impostato sull'unità disco con maggiore spazio disponibile al momento dell'installazione. Il percorso secondario sarà assegnato all'unità disco con la seconda maggiore quantità di spazio disponibile. Quando le unità primaria e secondaria raggiungono il limite di spazio riservato, Configuration Manager seleziona un'altra unità disponibile con la maggiore quantità di spazio libero e continua il processo di copia.  

> [!NOTE]  
>  Per evitare l'installazione di Configuration Manager in un'unità specifica, creare un file vuoto denominato **no_sms_on_drive.sms** e copiarlo nella cartella radice dell'unità prima dell'installazione del punto di distribuzione.  

### <a name="pull-distribution-point"></a>Punto di distribuzione pull  
È possibile selezionare **Abilita il pull di contenuti di questo punto di distribuzione da altri punti di distribuzione** per modificare il comportamento in base al quale il computer ottiene il contenuto distribuito nel punto di distribuzione. Viene trasformato in un punto di distribuzione pull.  

Per ogni punto di distribuzione pull configurato, è necessario specificare uno o più punti di distribuzione di origine da cui il punto di distribuzione pull ottiene il contenuto.  

-   Fare clic su **Aggiungi**e quindi selezionare uno o più punti di distribuzione disponibili come punti di distribuzione di origine.  

-   Fare clic su **Rimuovi** per rimuovere il punto di distribuzione selezionato come punto di distribuzione di origine.  

-   Usare i pulsanti freccia per modificare l'ordine in cui i punti di distribuzione di origine vengono contattati dal punto di distribuzione pull quando il punto di distribuzione pull tenta di trasferire il contenuto. I punti di distribuzione con il valore più basso vengono contattati per primi.  

### <a name="pxe"></a>PXE  
Specificare se abilitare PXE nel punto di distribuzione. Quando si abilita PXE, Configuration Manager installa i Servizi di distribuzione Windows nel server, se necessario. Servizi di distribuzione Windows è il servizio che esegue l'avvio PXE per installare i sistemi operativi. Dopo aver completato la procedura guidata per creare il punto di distribuzione, Configuration Manager installa un provider in Servizi di distribuzione Windows che usa le funzioni di avvio PXE.  

Quando si seleziona **Abilita supporto PXE per i client**, configurare le seguenti impostazioni:  

-   **Consenti a questo punto di distribuzione di rispondere alle richieste PXE in ingresso**: specifica se abilitare Servizi di distribuzione Windows per rispondere alle richieste di servizio PXE. Usare questa casella di controllo per attivare e disattivare il servizio senza rimuovere la funzionalità PXE dal punto di distribuzione.  

-   **Abilita supporto per computer sconosciuti**: specificare se si vuole abilitare il supporto per i computer che non sono gestiti da Configuration Manager.  

-   **Richiedi password quando i computer usano PXE**: per fornire maggiore sicurezza per le distribuzioni PXE, specificare una password complessa.  

-   **Affinità utente dispositivo**: specificare come si desidera che il punto di distribuzione associ gli utenti al computer di destinazione per le distribuzioni PXE. Selezionare una delle opzioni seguenti:  

    -   **Consenti affinità utente dispositivo con approvazione automatica**: selezionare questa impostazione per associare automaticamente gli utenti al computer di destinazione senza attendere l'approvazione.  

    -   **Consenti approvazione amministratore in sospeso per affinità utente dispositivo**: selezionare questa impostazione per attendere l'approvazione di un utente amministratore prima che gli utenti siano associati al computer di destinazione.  

    -   **Non consentire affinità utente dispositivo**: selezionare questa impostazione per specificare che gli utenti non sono associati al computer di destinazione.  

     Per altre informazioni sull'affinità utente dispositivo, vedere [Collegare utenti e dispositivi mediante l'affinità utente dispositivo in System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

-   **Interfacce di rete**: specificare se il punto di distribuzione risponde alle richieste PXE da tutte le interfacce di rete o da interfacce di rete specifiche. Se il punto di distribuzione risponde a un interfaccia di rete specifica, è necessario fornire l'indirizzo MAC per ogni interfaccia di rete.  

-   **Specificare il ritardo risposta del server PXE (secondi)**: specifica, in secondi, il tempo di attesa del punto di distribuzione prima che risponda alle richieste dei computer quando vengono usati più punti di distribuzione che supportano PXE. Per impostazione predefinita, il punto di servizio PXE di Configuration Manager risponde prima alle richieste PXE di rete.  

> [!NOTE]  
>  È possibile usare il protocollo PXE per avviare le distribuzioni del sistema operativo nei computer client di Configuration Manager. Configuration Manager usa il ruolo del sito del punto di distribuzione PXE per iniziare il processo di distribuzione del sistema operativo. Il punto distribuzione che supporta PXE deve essere configurato in modo da rispondere alle richieste di avvio PXE effettuate dai client di Configuration Manager in rete e quindi interagire con l'infrastruttura di Configuration Manager per determinare le azioni di distribuzione appropriate da eseguire.  

### <a name="multicast"></a>Multicast  
Specificare se abilitare multicast nel punto di distribuzione. Quando si abilita il multicast, Configuration Manager installa i Servizi di distribuzione Windows nel server, se necessario.  

Quando si seleziona la casella di controllo **Abilita multicast per inviare contemporaneamente dati a più client** , configurare le seguenti impostazioni:  

-   **Account di connessione multicast**: specificare l'account da usare quando si configurano le connessioni del database di Configuration Manager per il multicast.  

-   **Impostazioni indirizzo multicast**: specificare gli indirizzi IP usati per l'invio dei dati ai computer di destinazione. Per impostazione predefinita, l'indirizzo IP viene ottenuto da un server DHCP abilitato per la distribuzione di indirizzi multicast. A seconda dell'ambiente di rete, è possibile specificare un intervallo di indirizzi IP compreso tra 239.0.0.0 e 239.255.255.255.  

    > [!IMPORTANT]  
    >  Gli indirizzi IP configurati devono essere accessibili ai computer di destinazione che richiedono l'immagine del sistema operativo. Verificare che i router e firewall consentano il traffico multicast tra il computer di destinazione e il server del sito.  

-   **Intervallo di porte UDP per multicast**: specificare l'intervallo di porte UDP (User Datagram Protocol) usate per inviare dati ai computer di destinazione.  

    > [!IMPORTANT]  
    >  Queste porte UDP devono essere accessibili ai computer di destinazione che richiedono l'immagine del sistema operativo. Verificare che i router e firewall consentano il traffico multicast tra il computer di destinazione e il server del sito.  

-   **Velocità di trasferimento client**: selezionare la velocità di trasferimento per il download dei dati nei computer di destinazione.  

-   **Numero massimo di client**: specificare il numero massimo di computer di destinazione per cui è possibile scaricare il sistema operativo da questo punto di distribuzione.  

-   **Abilita multicast pianificato**: specificare come Configuration Manager esegue i controlli per avviare la distribuzione dei sistemi operativi ai computer di destinazione. Quando è selezionata, è necessario configurare le seguenti opzioni:  

    -   **Ritardo avvio sessione (minuti)**: specificare il numero di minuti che Configuration Manager deve attendere prima di rispondere alla prima richiesta di distribuzione.  

    -   **Dimensione minima sessione (client)**: specificare il numero di richieste che Configuration Manager deve ricevere prima di avviare la distribuzione del sistema operativo.  

> [!NOTE]  
>  Le distribuzioni multicast risparmiano larghezza di banda inviando contemporaneamente i dati a più client di Configuration Manager anziché inviare una copia dei dati a ogni client in una connessione separata. Per altre informazioni sull'uso del multicast per la distribuzione di sistemi operativi, vedere [Use multicast to deploy Windows over the network with System Center Configuration Manager](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md) (Usare il multicast per distribuire Windows in rete con System Center Configuration Manager).  

### <a name="group-relationships"></a>Relazioni gruppi  

> [!NOTE]  
>  Queste opzioni sono disponibili solo quando si modificano le proprietà di un punto di distribuzione installato precedentemente  

Gestire i gruppi di punti di distribuzione di cui il punto di distribuzione è un membro.  

Per aggiungere questo punto di distribuzione come membro di un gruppo esistente, fare clic su **Aggiungi**. Selezionare un gruppo di punti di distribuzione esistente nell'elenco della finestra di dialogo **Aggiungi ai gruppi di punti di distribuzione** e quindi fare clic su **OK**.  

Per rimuovere il punto di distribuzione da un gruppo di punti di distribuzione, selezionare il gruppo di punti di distribuzione dall'elenco e quindi fare clic su **Rimuovi**.  

### <a name="content"></a>Content  

> [!NOTE]  
>  Queste opzioni sono disponibili solo quando si modificano le proprietà di un punto di distribuzione installato precedentemente  

Gestire il contenuto distribuito al punto di distribuzione. Nella sezione Pacchetti di distribuzione è disponibile un elenco dei pacchetti distribuiti a questo punto di distribuzione. È possibile selezionare un pacchetto dall'elenco ed eseguire le azioni seguenti:  

-   **Convalida**: avvia il processo per convalidare l'integrità dei file di contenuto nel pacchetto. Per visualizzare i risultati del processo di convalida del contenuto, nell'area di lavoro **Monitoraggio** espandere **Stato distribuzione**e quindi fare clic sul nodo **Stato contenuto** .  

-   **Ridistribuisci**: copia nel punto di distribuzione tutti i file di contenuto del pacchetto e sovrascrive i file esistenti. Questa operazione viene in genere usata per ripristinare i file di contenuto nel pacchetto.  

-   **Rimuovi**: rimuove i file di contenuto dal punto di distribuzione per il pacchetto.  

### <a name="content-validation"></a>Convalida contenuto  
Specificare se impostare una pianificazione per convalidare l'integrità dei file di contenuto nel punto di distribuzione. Quando si abilita la convalida del contenuto su una pianificazione, Configuration Manager avvia il processo all'orario pianificato e tutto il contenuto sul punto di distribuzione viene verificato. È inoltre possibile configurare la priorità di convalida del contenuto. Per impostazione predefinita, la priorità è impostata su **Minima**.  

Per visualizzare i risultati del processo di convalida del contenuto, nell'area di lavoro **Monitoraggio** espandere **Stato distribuzione**e quindi fare clic sul nodo **Stato contenuto** . Viene visualizzato il contenuto per ogni tipo di pacchetto (ad esempio, applicazione, pacchetto di aggiornamento software e immagine di avvio).  

> [!WARNING]  
>  Se si specifica la pianificazione della convalida del contenuto usando l'ora locale per il computer, la pianificazione viene visualizzata nella console di Configuration Manager in formato UTC.  

### <a name="boundary-group"></a>Gruppo di limiti  
Gestire i gruppi di limiti per i quali viene assegnato il punto di distribuzione. È possibile associare i gruppi di limiti a un punto di distribuzione. Durante la distribuzione del contenuto, i client devono trovarsi in un gruppo di limiti associato al punto di distribuzione per usarlo come percorso di origine per il contenuto.
Inoltre:
- Per le versioni precedenti alla 1610, è possibile selezionare la casella di controllo **Allow clients to use this site system as a fallback source location for content** (Consenti ai client di usare il sistema del sito come percorso origine di fallback per il contenuto) per consentire ai client esterni a questi gruppi di limiti di eseguire il fallback e usare il punto di distribuzione come un percorso di origine per il contenuto in assenza di altri punti di distribuzione disponibili. Per altre informazioni sui gruppi di limiti, vedere [Boundary groups for versions 1511, 1602, and 1606](/sccm/core/servers/deploy/configur/boundary-groups-for-1511-1602-and-1606) (Gruppi di limiti per le versioni 1511, 1602 e 1606) e per informazioni sui punti di distribuzione preferiti, vedere [Concetti di base per la gestione dei contenuti in System Center Configuration Manager](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).
- Con la versione 1610 o versioni successive, è possibile configurare il gruppo di limiti *Relazioni* che definisce quando e in quali gruppi di limiti un client può eseguire il fallback per individuare contenuti. Per altre informazioni vedere [Gruppi di limiti](/sccm/core/servers/deploy/configur/define-site-boundaries-and-boundary-groups#boundary-groups).


### <a name="schedule"></a>Pianificazione  

> [!NOTE]  
>  Queste opzioni sono disponibili solo quando si modificano le proprietà di un punto di distribuzione installato precedentemente  

> [!TIP]  
>  Questa scheda è disponibile solo quando si modificano le proprietà di un punto di distribuzione remoto dal computer del server di sito.  

 Specificare se configurare una pianificazione che stabilisca quando Configuration Manager può trasferire i dati al punto di distribuzione.  

> [!IMPORTANT]  
>  La pianificazione è basata sul fuso orario del sito di invio, non del punto di distribuzione.  

Per limitare i dati, selezionare il periodo di tempo e quindi selezionare una delle impostazioni seguenti per **Disponibilità**:  

-   **Apri per tutte le proprietà**: specifica che Configuration Manager deve inviare i dati al punto di distribuzione senza restrizioni.  

-   **Consenti priorità media e alta**: specifica che Configuration Manager deve inviare solo i dati con priorità media e alta al punto di distribuzione.  

-   **Consenti solo priorità alta**: specifica che Configuration Manager deve inviare solo i dati con priorità alta al punto di distribuzione.  

-   **Chiusa**: specifica che Configuration Manager non deve inviare dati al punto di distribuzione.  

È possibile limitare i dati per priorità o chiudere la connessione per periodi di tempo selezionati.  

### <a name="rate-limits"></a>Limiti di velocità  

> [!NOTE]  
>  Queste opzioni sono disponibili solo quando si modificano le proprietà di un punto di distribuzione installato precedentemente  

> [!TIP]  
>  Questa scheda è disponibile solo quando si modificano le proprietà di un punto di distribuzione remoto dal computer del server di sito.  

Specificare se configurare i limiti di velocità per controllare la larghezza di banda di rete in uso durante il trasferimento di contenuto al punto di distribuzione. È possibile scegliere una delle opzioni seguenti:  

-   **Illimitato per l'invio a questa destinazione**: specifica che Configuration Manager deve inviare il contenuto al punto di distribuzione senza restrizioni.  

-   **Modalità a impulsi**: specifica la dimensione dei blocchi di dati inviati al punto di distribuzione. È inoltre possibile specificare un ritardo tra l'invio di ogni blocco di dati. Usare questa opzione quando è necessario inviare i dati attraverso una connessione di rete con larghezza di banda molto bassa al punto di distribuzione. È possibile, ad esempio, che si sia vincolati a inviare 1 KB di dati ogni cinque secondi, indipendentemente dalla velocità del collegamento o dall'utilizzo in un determinato momento.  

-   **Limitato alle velocità di trasferimento massime specificate per ora**: specificare questa impostazione in modo che un sito invii i dati a un punto di distribuzione usando solo la percentuale di tempo configurata. Quando si usa questa opzione, Configuration Manager non identifica la larghezza di banda disponibile per la rete, ma divide in intervalli il periodo di tempo in cui può inviare i dati. I dati vengono quindi inviati per un breve intervallo di tempo, seguito da periodi di tempo quando i dati non vengono inviati. Se ad esempio la velocità massima è impostata su **50%**, Configuration Manager trasmette i dati per un periodo di tempo seguito da un uguale periodo di tempo in cui non viene inviato alcun dato. La quantità effettiva di dati, o dimensione del blocco di dati, non è gestita. Viene invece gestita solo la quantità di tempo durante il quale i dati vengono inviati.  



<!--HONumber=Dec16_HO3-->



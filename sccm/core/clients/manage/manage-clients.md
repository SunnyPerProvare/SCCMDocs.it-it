---
title: Gestire i client | System Center Configuration Manager
description: Informazioni su come gestire i client in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
caps.latest.revision: 17
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: 67a814330123a1615a0663872bf4af64e5b81a84


---
# <a name="how-to-manage-clients-in-system-center-configuration-manager"></a>Come gestire i client in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Quando un client di System Center Configuration Manager viene installato e assegnato correttamente a un sito di Configuration Manager, il dispositivo viene visualizzato nell'area di lavoro **Asset e conformità** del nodo **Dispositivi** e in una o più raccolte del nodo **Raccolte dispositivi**. Quando si seleziona il dispositivo o la raccolta che contiene il dispositivo, è possibile selezionare varie operazioni di gestione. Esistono tuttavia anche altre modalità di gestione del client che potrebbero interessare altre aree di lavoro della console o attività che non usano la console di Configuration Manager.  

 Usare questo argomento per informazioni generali relative alle attività per la gestione di un client di Configuration Manager dall'area di lavoro **Asset e conformità**, nonché informazioni dettagliate relative ad attività aggiuntive per la gestione del client di Configuration Manager. Per altre informazioni su come configurare il client, vedere [Come configurare le impostazioni client in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md)  

> [!NOTE]  
>  È possibile che un client di Configuration Manager sia installato e non sia visualizzato nella console di Configuration Manager. Questo scenario può verificarsi se il client non è ancora stato assegnato a un sito oppure se è necessario aggiornare la console o l'appartenenza a una raccolta.  
>   
>  È anche possibile che un dispositivo venga visualizzato nella console quando il client di Configuration Manager non è installato. Questo scenario può verificarsi se il dispositivo viene individuato ma il client di Configuration Manager non è installato e assegnato. I dispositivi mobili gestiti usando il connettore Exchange Server non installano il client di Configuration Manager. Anche i dispositivi registrati da Microsoft Intune non installano il client di Configuration Manager.  
>   
>  Usare la colonna **Client** della console di Configuration Manager per determinare se il client di Configuration Manager è installato e può essere gestito dalla console di Configuration Manager.  

##  <a name="a-namebkmkmanagingclientsdevicesnodea-manage-clients-from-the-devices-node"></a><a name="BKMK_ManagingClients_DevicesNode"></a> Gestire i client dal nodo Dispositivi  
 Usare la seguente procedura e la seguente tabella per gestire uno o più dispositivi dal nodo **Dispositivi** dell'area di lavoro **Asset e conformità** .  

> [!IMPORTANT]  
>  A seconda del tipo di dispositivo, alcune di queste opzioni potrebbero non essere disponibili.  

#### <a name="to-manage-clients-from-the-devices-node"></a>Per gestire i client dal nodo Dispositivi  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Dispositivi**.  

3.  Selezionare uno o più dispositivi, quindi selezionare una delle seguenti attività di gestione client dalla barra multifunzione o facendo clic con il pulsante destro del mouse sul dispositivo:  

    -   **Gestire le informazioni di affinità utente dispositivo**  

         Consente di configurare le associazioni tra utenti e dispositivi, per una distribuzione efficiente del software agli utenti.  

         Vedere [Collegare utenti e dispositivi mediante l'affinità utente dispositivo in System Center Configuration Manager](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)  

    -   **Aggiungere il dispositivo a una raccolta nuova o esistente**  

         Usare queste azioni relative alla raccolta per aggiungere rapidamente il dispositivo selezionato a una raccolta mediante una regola diretta.  

         [Operazioni e manutenzione per le raccolte in System Center Configuration Manager](../../../core/clients/manage/collections/operations-and-maintenance-for-collections.md)  

    -   **Installare e reinstallare il client usando l'Installazione push client guidata**  

         L'Installazione push client guidata consente di installare e reinstallare in modo efficiente il client di Configuration Manager per il ripristino o la riconfigurazione nei computer che eseguono Windows con opzioni di configurazione del sito e con proprietà client.msi aggiuntive specificate per l'installazione push client.  

        > [!TIP]  
        >  Esistono diversi modi per installare e reinstallare il client di Configuration Manager. Sebbene l'Installazione push client guidata consenta di installare il client in modo pratico grazie all'esecuzione dalla console, questo metodo di installazione client presenta numerose dipendenze e non è adatto a tutti gli ambienti. Se non è possibile installare correttamente il client tramite installazione push client, è possibile usare molti altri metodi di installazione client. Per altre informazioni sulle dipendenze, vedere [Prerequisiti per la distribuzione dei client nei computer Windows in System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md). Per altre informazioni sugli altri metodi di installazione dei client, vedere [Metodi di installazione client in System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md).  

         Vedere [Come installare i client di Configuration Manager utilizzando push client](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

    -   **Riassegnare il sito**  

         È ora possibile riassegnare uno o più client, inclusi i dispositivi mobili gestiti, a un altro sito principale nella gerarchia. I client possono essere riassegnati singolarmente o possono essere selezionati più volte e riassegnati in massa a un nuovo sito.  

    -   **Amministrare in remoto il client**  

         È possibile eseguire Esplora inventario risorse per visualizzare le informazioni di inventario software e hardware di un client Windows, nonché amministrarlo in remoto usando Controllo remoto, Assistenza remota o Desktop remoto.  

         Vedere [Come usare Esplora inventario risorse per visualizzare l'inventario hardware in System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) e [Come usare Esplora inventario risorse per visualizzare l'inventario software in System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

         Vedere [Come amministrare un computer client Windows in remoto mediante System Center Configuration Manager](../../../core/clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).  

    -   **Approvare un client**  

         Quando il client comunica con i sistemi del sito mediante HTTP e un certificato autofirmato, è necessario approvare i client per identificarli come computer attendibili. Per impostazione predefinita, la configurazione del sito approva automaticamente i client della stessa foresta Active Directory e delle foreste trusted e non è quindi necessario approvare manualmente ciascun client. È tuttavia necessario approvare manualmente i computer del gruppo di lavoro ritenuti attendibili e gli altri computer ritenuti attendibili ma non approvati.  

        > [!WARNING]  
        >  Sebbene alcune funzioni di gestione potrebbero funzionare per i client non approvati, si tratta di uno scenario non supportato per Configuration Manager.  

         Non è necessario approvare i client che comunicano sempre con i sistemi del sito usando HTTPS anziché HTTP o i client che usano un certificato PKI durante la comunicazione con i sistemi del sito mediante HTTP. Questi client stabiliscono relazioni di trust con Configuration Manager mediante certificati PKI.  

    -   **Bloccare o sbloccare un client**  

         Bloccare un client che non si ritiene più attendibile per fare in modo che non riceva i criteri client e che non comunichi con i sistemi del sito di Configuration Manager.  

        > [!WARNING]  
        >  Il blocco di un client impedisce solo la comunicazione del client con i sistemi del sito di Configuration Manager, non la comunicazione con gli altri dispositivi. Inoltre, quando il client comunica con i sistemi del sito mediante HTTP anziché HTTPS, vengono applicate alcune limitazioni di protezione.  

         Se successivamente si cambia idea, è possibile sbloccare un client che è stato bloccato. Se tuttavia si sblocca un computer basato su Intel AMT di cui è stato eseguito il provisioning per AMT al momento del blocco, è necessario eseguire passaggi aggiuntivi prima di poter gestire nuovamente il computer fuori banda.  

         Vedere [Determinare se bloccare o meno i client in System Center Configuration Manager](../../../core/clients/deploy/plan/determine-whether-to-block-clients.md).  

    -   **Cancellare una distribuzione PXE richiesta**  

         Usare questa opzione per ridistribuire distribuzioni PXE richieste per il computer selezionato.  

         Vedere [Usare PXE per distribuire Windows in rete con System Center Configuration Manager](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

    -   **Gestire le proprietà client**  

         È possibile visualizzare i dati di individuazione e le distribuzioni usate come destinazione per il client. È inoltre possibile configurare tutte le variabili usate dalle sequenze attività per distribuire un sistema operativo nel dispositivo.  

    -   **Eliminare il client**  

        > [!WARNING]  
        >  Non eliminare un client se si vuole disinstallare il client di Configuration Manager o rimuoverlo da una raccolta.  

         L'azione **Elimina** consente di eliminare manualmente il record client dal database di Configuration Manager e, in genere, non va usata al di fuori degli scenari di risoluzione dei problemi. Se si elimina il record client e il client di Configuration Manager è ancora installato e comunicante con Configuration Manager, l'individuazione heartbeat ricreerà il record client che verrà visualizzato nuovamente nella console di Configuration Manager, sebbene la cronologia client ed eventuali associazioni precedenti andranno perse.  

        > [!NOTE]  
        >  Quando viene eliminato un client di dispositivi mobili registrato da Configuration Manager, l'azione revoca inoltre il certificato PKI rilasciato al dispositivo mobile. Il certificato viene quindi rifiutato dal punto di gestione, anche se IIS non esegue il controllo CRL. I certificati dei client precedenti del dispositivo mobile non vengono revocati quando i client vengono eliminati.  

         Per disinstallare il client, vedere [Disinstallare il client di Configuration Manager](#BKMK_UninstalClient).  

         Per assegnare il client a un nuovo sito primario, vedere [Come assegnare i client a un sito in System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

         Per rimuovere il client da una raccolta, riconfigurare le proprietà della raccolta. Vedere [Come gestire le raccolte in System Center Configuration Manager](../../../core/clients/manage/collections/manage-collections.md).  

    -   **Cancellare i dati di un dispositivo mobile**  

         È possibile cancellare i dati dei dispositivi mobili che supportano il comando di cancellazione.  

         Questa azione consente di rimuovere definitivamente tutti i dati del dispositivo mobile, comprese le impostazioni e i dati personali. In genere, questa azione consente di ripristinare le impostazioni di fabbrica nel dispositivo. Cancellare i dati di un dispositivo mobile quando il dispositivo mobile non è più considerato attendibile, ad esempio in caso di furto o smarrimento.  

        > [!TIP]  
        >  Vedere la documentazione del produttore per altre informazioni sull'elaborazione di un comando di cancellazione remota da parte del dispositivo mobile.  

         Quando si invia una richiesta di cancellazione, si verifica spesso un ritardo nella ricezione del comando di cancellazione da parte del dispositivo mobile:  

        -   Se il dispositivo mobile viene registrato da Configuration Manager o da Microsoft Intune, il client riceve il comando di cancellazione successivamente al momento del download dei criteri client.  

        -   Se il dispositivo mobile è gestito dal connettore Exchange Server, esso riceve il comando di cancellazione successivamente, al momento della sincronizzazione con Exchange.  

         È possibile usare la colonna **Stato cancellazione** per il monitoraggio della ricezione del comando di cancellazione da parte del dispositivo mobile. Finché il dispositivo mobile non invia un acknowledgment di cancellazione a Configuration Manager, è possibile annullare il comando di cancellazione.  

    -   **Ritirare un dispositivo mobile**  

         L'opzione **Ritira** è supportata solo dai dispositivi mobili registrati da Intune o da Gestione dispositivi mobili locali.  

         Per altre informazioni, vedere [Proteggere i dati con Cancellazione remota, Blocco remoto o Reimpostazione passcode usando System Center Configuration Manager](../../../mdm/deploy-use/wipe-lock-reset-devices.md).  

    -   **Modificare la proprietà di un dispositivo**  

         È possibile modificare la proprietà dei dispositivi in **Società** o **Personale** se un dispositivo non appartiene al dominio e non dispone del client di Configuration Manager installato.  

         È possibile usare questo valore nei requisiti applicazione per controllare le distribuzioni ed è inoltre possibile usare questa configurazione per controllare il volume dell'inventario raccolto dai dispositivi degli utenti.  

        Per visualizzare il valore della proprietà nell'elenco dei dispositivi, è necessario aggiungere la colonna alla visualizzazione facendo clic su un'intestazione di colonna e scegliendo **Proprietario dispositivo**.

         Per altre informazioni, vedere [Gestione di dispositivi mobili ibridi con System Center Configuration Manager e Microsoft Intune](../../../mdm/plan-design/hybrid-mobile-device-management.md).  

##  <a name="a-namebkmkmanagingclientsdevicecollectionsnodea-manage-clients-from-the-device-collections-node"></a><a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> Gestire i client dal nodo Raccolte dispositivi  
 Usare la seguente procedura e la seguente tabella per gestire i dispositivi di una raccolta dal nodo **Raccolte dispositivi** dell'area di lavoro **Asset e conformità** .  

 Molte attività di gestione client eseguibili quando si selezionano uno o più dispositivi dal nodo **Dispositivi** possono essere eseguite anche a livello di raccolta. In tal modo l'attività di gestione viene applicata automaticamente a tutti i dispositivi idonei della raccolta. Sebbene questo metodo sia efficace per la gestione simultanea di più client, può generare un'ampia quantità di pacchetti di rete e richiedere un maggiore utilizzo della CPU nel server del sito.  

 Esistono inoltre alcune attività di gestione client che possono essere eseguite solo a livello di raccolta e sono elencate nella seguente tabella.  

 Prima di eseguire le attività di gestione client a livello di raccolta, tenere in considerazione la quantità di dispositivi presenti nella raccolta, l'eventuale connessione mediante connessioni di rete con larghezza di banda ridotta e il tempo necessario per il completamento dell'attività in tutti i dispositivi. Quando si esegue un'attività di gestione client, non è possibile interromperla dalla console.  

#### <a name="to-manage-clients-from-the-device-collections-node"></a>Per gestire i client dal nodo Raccolte dispositivi  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Raccolte dispositivi**.  

3.  Selezionare una raccolta, quindi selezionare una delle seguenti attività di gestione client dalla barra multifunzione o facendo clic con il pulsante destro del mouse sulla raccolta:  

    -   **Eseguire la scansione dei computer per rilevare la presenza di malware e scaricare i file di definizione antimalware.**  

         Vedere [Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

    -   **Distribuire software, linee di base della configurazione e sequenze attività.**  

         Per altre informazioni sulla distribuzione di software e delle linee di base della configurazione, vedere quanto segue:  

        -   [Distribuire gli aggiornamenti software in System Center Configuration Manager](../../../sum/deploy-use/deploy-software-updates.md)  

        -   [Pianificare e configurare le impostazioni di conformità in System Center Configuration Manager](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)  

    -   **Configurare le impostazioni di risparmio energia.**  

         Vedere [Come creare e applicare combinazioni per il risparmio di energia in System Center Configuration Manager](../../../core/clients/manage/power/create-and-apply-power-plans.md). Le combinazioni per il risparmio di energia sono utilizzabili solo con computer che eseguono Windows.  

    -   **Inviare una notifica ai computer per il download dei criteri appena possibile.**  

         Usare la notifica client per inviare una notifica ai client Windows selezionati per il download dei criteri computer appena possibile all'esterno dell'intervallo di polling dei criteri client configurato.  

         Le attività di notifica client vengono visualizzate nel nodo **Operazioni client** dell'area di lavoro **Monitoraggio** .  

##  <a name="a-namebkmkclientcachea-configure-the-client-cache-for-configuration-manager-clients"></a><a name="BKMK_ClientCache"></a> Configurare la cache del client per i client di Configuration Manager  
 È possibile configurare il percorso e la quantità di spazio su disco che i client di Windows Configuration Manager usano per archiviare i file temporanei quando installano applicazioni e programmi. Gli aggiornamenti software usano anche la cache client, ma non sono limitati dalla dimensione della cache configurata e tenteranno sempre di eseguire il download nella cache. È possibile configurare le impostazioni della cache del client quando si installa manualmente il client di Configuration Manager, quando si usa l'installazione push client oppure dopo aver installato il client.

Nella versione 1606 di Configuration Manager è possibile specificare le dimensioni della cartella cache usando le impostazioni client nella console di Configuration Manager.   

 Il percorso predefinito per la cache del client di Configuration Manager è %*windir*%\ccmcache e lo spazio su disco predefinito è 5120 MB.  

> [!IMPORTANT]  
>  Non crittografare la cartella usata per la cache client. Configuration Manager non può scaricare il contenuto in una cartella crittografata.  

### <a name="about-client-cache"></a>Dimensione della cache del client  

Il client di Configuration Manager scarica il contenuto per il software richiesto non appena riceve la distribuzione ma non effettua l'esecuzione fino all'ora di distribuzione pianificata. All'ora pianificata, il client di Configuration Manager controlla se il contenuto è disponibile nella cache. Se il contenuto si trova nella cache ed è la versione corretta, il client usa sempre questo contenuto nella cache. Tuttavia, quando la versione richiesta del contenuto viene modificata o se il contenuto viene eliminato per liberare spazio per un altro pacchetto, il contenuto viene scaricato di nuovo nella cache.  

Se il client tenta di scaricare il contenuto per un programma o un'applicazione di dimensioni superiori rispetto a quelle della cache, la distribuzione avrà esito negativo perché la dimensione della cache non è sufficiente e Configuration Manager genera l'ID messaggio di stato 10050. Se in seguito la dimensione della cache viene aumentata, il comportamento del nuovo tentativo di download sarà diverso per un programma richiesto e per un'applicazione richiesta:  

-   Per un programma richiesto: il client non tenterà automaticamente di scaricare il contenuto. È necessario ridistribuire il programma e il pacchetto al client.  
-   Per un'applicazione richiesta: poiché una distribuzione applicazione è basata sullo stato, il client tenterà automaticamente di scaricare il contenuto al successivo download dei criteri client.  

Se il client tenta di scaricare un pacchetto di dimensioni inferiori rispetto a quelle della cache ma la cache al momento è piena, tutte le distribuzioni richieste eseguiranno altri tentativi finché non sarà disponibile spazio nella cache, non si verificherà un timeout del download oppure non verrà raggiunto il limite di tentativi per gli errori di spazio nella cache. Se in seguito la dimensione della cache viene aumentata, il client di Configuration Manager tenterà di scaricare nuovamente il pacchetto al successivo intervallo tra tentativi. Il client tenterà di scaricare il contenuto ogni quattro ore finché non avrà eseguito 18 tentativi.  

Il contenuto nella cache non viene eliminato automaticamente ma rimane nella cache per almeno un giorno dopo essere stato usato dal client. Se si configurano le proprietà del pacchetto con l'opzione per mantenere il contenuto nella cache client, il client non elimina automaticamente il contenuto del pacchetto dalla cache. Se lo spazio nella cache client viene usato dai pacchetti scaricati nelle ultime 24 ore e il client deve scaricare nuovi pacchetti, è possibile aumentare la dimensione della cache client oppure scegliere l'opzione per eliminare il contenuto della cache persistente.  

 Usare le seguenti procedure per configurare la cache client durante l'installazione client manuale oppure dopo l'installazione client.  

### <a name="to-configure-the-client-cache-when-you-install-clients-by-using-manual-client-installation"></a>Per configurare la cache client durante l'installazione client usando l'installazione client manuale  

Eseguire il comando CCMSetup.exe dal percorso di origine di installazione e specificare le seguenti proprietà richieste e separate da spazi:  

   -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > Per la versione 1606, usare le impostazioni della dimensione della cache disponibili in **Impostazioni client** nella console di Configuration Manager anziché SMSCACHESIZE. Per altre informazioni vedere [Impostazioni della cache del client](../../../core/clients/deploy/about-client-settings.md#Client-Cache-Settings).

Per altre informazioni sull'uso di queste proprietà della riga di comando di CCMSetup.exe, vedere [Informazioni sulle proprietà di installazione client in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="to-configure-the-client-cache-folder-when-you-install-clients-by-using-client-push-installation"></a>Per configurare la cartella cache client durante l'installazione client usando l'installazione push client  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** , espandere **Configurazione sito**, quindi fare clic su **Siti**.  

3.  Nell'elenco **Siti** selezionare il sito per cui si desidera configurare l'installazione push client automatica a livello di sito.  

4.  Nella scheda **Home** , nel gruppo **Impostazioni** , fare clic su **Impostazioni di installazione client**e quindi sulla scheda **Proprietà di installazione**.  

5.  Nella scheda **Proprietà di installazione** specificare le seguenti proprietà richieste separate da spazi:  

    -   DISABLECACHEOPT  

    -   SMSCACHEDIR  

    -   SMSCACHEFLAGS  

    -   SMSCACHESIZE  

        > [!NOTE]
        > Per la versione 1606, usare le impostazioni della dimensione della cache disponibili in **Impostazioni client** nella console di Configuration Manager anziché SMSCACHESIZE. Per altre informazioni vedere [Impostazioni della cache del client](../../../core/clients/deploy/about-client-settings.md#Client-Cache-Settings).

       Per altre informazioni sull'uso di queste proprietà della riga di comando di CCMSetup.exe, vedere [Informazioni sulle proprietà di installazione client in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

6.  Fare clic su **OK** per salvare le proprietà specificate.  

### <a name="to-configure-the-client-cache-folder-on-the-client-computer"></a>Per configurare la cartella cache del client sul computer client  

1.  Nel Pannello di controllo del computer client passare a **Configuration Manager** e quindi fare doppio clic per aprire le proprietà.  

2.  Fare clic sulla scheda **Cache** .  

3.  Specificare lo spazio su disco da riservare per la cache client.  

4.  Per modificare il percorso della cartella cache client, fare clic su **Cambia percorso**e quindi specificare il nuovo percorso. Il percorso predefinito è *%windir%*\ccmcache.  

5.  Per eliminare i file attualmente archiviati nella cartella cache client, fare clic su **Elimina file**.  

6.  Fare clic su **OK** per chiudere **Proprietà di Configuration Manager**.  

### <a name="to-configure-client-cache-size-in-client-settings"></a>Per configurare la dimensione della cache del client in Impostazioni client

A partire dalla versione 1606, è possibile modificare la dimensione della cartella cache del client senza dover reinstallare il client. A tale scopo, è possibile configurare la dimensione della cache del client nella console di Configuration Manager usando le impostazioni del client.  

1. Nella console di Configuration Manager scegliere **Amministrazione** > **Impostazioni client**.

2. Fare doppio clic su **Impostazioni client predefinite**.
  È anche possibile creare impostazioni client personalizzate per applicare la dimensione della cache in modo più selettivo. Per altre informazioni sulle impostazioni client predefinite e personalizzate, vedere [Come configurare le impostazioni client in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

 3. Fare clic su **Impostazioni della cache del client** e scegliere **Sì** per **configurare la dimensione della cache del client**.

 4. Regolare la dimensione massima della cache usando l'impostazione in **MB** o la **percentuale del disco**. La cache viene adeguata alla dimensione che risulta inferiore.

 5. Fare clic su **OK**.

    Il client di Configuration Manager configurerà la dimensione della cache con queste impostazioni al successivo download dei criteri client.

##  <a name="a-namebkmkuninstalclienta-uninstall-the-configuration-manager-client"></a><a name="BKMK_UninstalClient"></a> Disinstallare il client di Configuration Manager  
 È possibile disinstallare il software client di Windows Configuration Manager da un computer usando **CCMSetup.exe** con la proprietà **/Uninstall**. Eseguire CCMSetup.exe in un singolo computer dal prompt dei comandi oppure distribuire un pacchetto e programma per disinstallare il client da una raccolta di computer.  

> [!WARNING]  
>  È impossibile disinstallare il client di Configuration Manager da un dispositivo mobile. Se è necessario rimuovere il client di Configuration Manager da un dispositivo mobile, è necessario cancellare il dispositivo eliminando tutti i dati nel dispositivo mobile.  

 Usare la seguente procedura per disinstallare il client di Configuration Manager dai computer.  

#### <a name="to-uninstall-the-configuration-manager-client-from-the-command-prompt"></a>Per disinstallare il client di Configuration Manager dal prompt dei comandi  

1.  Aprire un prompt dei comandi di Windows e modificare la cartella del percorso in cui si trova CCMSetup.exe.  

2.  Digitare **Ccmsetup.exe /uninstall**e quindi premere **Invio**.  

> [!NOTE]  
>  Il processo di disinstallazione è invisibile all'utente e non vengono visualizzati risultati sullo schermo. Per verificare il completamento della disinstallazione client, esaminare il file di log **CCMSetup.log** nella cartella *%windir%\ ccmsetup* nel computer client.  

##  <a name="a-namebkmkconflictingrecordsa-manage-conflicting-records-for-configuration-manager-clients"></a><a name="BKMK_ConflictingRecords"></a> Gestire i record in conflitto per i client di Configuration Manager  
 Configuration Manager usa l'ID hardware per tentare di identificare i client che potrebbero essere dei duplicati e avvertire l'utente dei record in conflitto. Ad esempio, se si reinstalla un computer, l'ID hardware rimane lo stesso mentre il GUID usato da Configuration Manager potrebbe cambiare.  

 Quando Configuration Manager è in grado di risolvere un conflitto usando l'autenticazione di Windows dell'account computer o un certificato PKI proveniente da un'origine attendibile, il conflitto viene automaticamente risolto. Quando tuttavia Configuration Manager non è in grado di risolvere il conflitto, viene usata un'impostazione gerarchia che unisce automaticamente i record in caso di rilevamento di ID hardware duplicati (impostazione predefinita) oppure consente di decidere quando unire, bloccare o creare nuovi record client. Se si decide di gestire manualmente i record duplicati, è necessario risolvere manualmente i record in conflitto usando la console di Configuration Manager.  

#### <a name="to-change-the-hierarchy-setting-for-managing-conflicting-records"></a>Per modificare l'impostazione della gerarchia per la gestione dei record in conflitto  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** , espandere **Configurazione sito**, quindi fare clic su **Siti**.  

3.  Nel gruppo **Siti** fare clic su **Impostazioni gerarchia**e quindi sulla scheda **Approvazione client e record in conflitto** .  

4.  Fare clic su **Risolvi automaticamente record in conflitto** per unire automaticamente i record in conflitto oppure fare clic su **Risolvi manualmente record in conflitto**e quindi su **OK**.  

    > [!NOTE]  
    >  Quando Configuration Manager può risolvere il conflitto usando l'account computer o un certificato PKI, questa impostazione viene ignorata e il conflitto viene risolto automaticamente.  

#### <a name="to-manually-resolve-conflicting-records"></a>Per risolvere manualmente i record in conflitto  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** espandere **Stato del sistema**e quindi fare clic su **Record in conflitto**.  

3.  Nel riquadro dei risultati selezionare uno o più record in conflitto e quindi fare clic su **Record in conflitto**.  

4.  Nella finestra di dialogo **Record in conflitto** selezionare una delle seguenti opzioni e quindi fare clic su **OK**:  

    -   **Unisci** per combinare il record appena rilevato con il record client esistente, creando un record unificato.  

    -   **Nuovo** per creare un nuovo record per il record client in conflitto.  

    -   **Blocca** per creare un nuovo record per il record client in conflitto, ma contrassegnandolo come bloccato.  

##  <a name="a-namebkmkpolicyretrievala-initiate-policy-retrieval-for-a-configuration-manager-client"></a><a name="BKMK_PolicyRetrieval"></a> Avviare il recupero criteri per un client di Configuration Manager  
 Un client di Windows Configuration Manager scarica i relativi criteri client in base a una pianificazione configurata come impostazione client. Tuttavia, è possibile che si desideri avviare un recupero criteri ad hoc dal client, ad esempio in uno scenario di risoluzione dei problemi oppure durante una verifica.  

 Usare le seguenti procedure per avviare un recupero criteri ad hoc dal client al di fuori dell'intervallo di polling pianificato, usando la scheda **Azioni** nel client di Configuration Manager oppure eseguendo uno script nel computer. È necessario essere connessi al computer client con diritti amministrativi locali per eseguire queste procedure.  

> [!NOTE]  
>  È possibile usare la notifica client per avviare il recupero criteri client al di fuori dell'intervallo di polling dei criteri client pianificato.  
>   
>  È possibile gestire i client che eseguono Linux e UNIX. Per informazioni sul recupero dei criteri per i client che eseguono Linux e UNIX, vedere [Computer policy for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_PolicyforLnU).  

#### <a name="to-initiate-client-policy-retrieval-by-using-client-notification"></a>Per avviare il recupero dei criteri client usando la notifica client  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Raccolte dispositivi**.  

3.  Selezionare la raccolta dispositivi contenente i computer che devono scaricare i criteri e quindi nella scheda **Home** , nel gruppo **Raccolte** , fare clic su **Notifica client** e quindi su **Scarica criteri computer**.  

    > [!NOTE]  
    >  È inoltre possibile usare la notifica client per avviare il recupero criteri per uno o più dispositivi selezionati visualizzati in un nodo raccolta temporaneo nel nodo **Dispositivi** .  

#### <a name="to-manually-initiate-client-policy-retrieval-by-using-the-actions-tab-on-the-configuration-manager-client"></a>Per avviare manualmente il recupero criteri client usando la scheda Azioni nel client di Configuration Manager  

1.  Selezionare **Configuration Manager** nel Pannello di controllo del computer.  

2.  Fare clic sulla scheda **Azioni** .  

3.  Fare clic su **Ciclo di recupero e valutazione criteri computer** per avviare i criteri computer e quindi fare clic su **Esegui**.  

4.  Fare clic su **OK** per confermare la richiesta.  

5.  Ripetere i passaggi 3 e 4 per ogni altra azione richiesta, ad esempio **Ciclo di recupero e valutazione criteri utente** per le impostazioni client utente.  

6.  Fare clic su **OK** per chiudere **Proprietà di Configuration Manager**.  

#### <a name="to-manually-initiate-client-policy-retrieval-by-using-a-script"></a>Per avviare manualmente il recupero criteri client usando uno script  

1.  Aprire un editor di testo, come Blocco note.  

2.  Copiare e inserire quanto di seguito riportato nel file:  

    ```  
    on error resume next  

    dim oCPAppletMgr 'Control Applet manager object.  
    dim oClientAction 'Individual client action.  
    dim oClientActions 'A collection of client actions.  

    'Get the Control Panel manager object.  
    set  oCPAppletMgr=CreateObject("CPApplet.CPAppletMgr")  
    if err.number <> 0 then  
        Wscript.echo "Couldn't create control panel application manager"  
        WScript.Quit  
    end if  

    'Get a collection of actions.  
    set oClientActions=oCPAppletMgr.GetClientActions  
    if err.number<>0 then  
        wscript.echo "Couldn't get the client actions"  
        set oCPAppletMgr=nothing  
        WScript.Quit  
    end if  

    'Display each client action name and perform it.  
    For Each oClientAction In oClientActions  

        if oClientAction.Name = "Request & Evaluate Machine Policy" then  
            wscript.echo "Performing action " + oClientAction.Name   
            oClientAction.PerformAction  
        end if  
    next  

    set oClientActions=nothing  
    set oCPAppletMgr=nothing  
    ```  

3.  Salvare il file con un'estensione .vbs.  

4.  Nel computer client, eseguire il file usando uno dei seguenti metodi:  

    -   Individuare il file usando Esplora risorse e fare doppio clic sul file script.  

    -   Aprire un prompt dei comandi e digitare: **cscript &lt;percorso\nomefile.vbs>**.  

5.  Fare clic su **OK** nella finestra di dialogo **Windows Script Host** .  



<!--HONumber=Nov16_HO1-->



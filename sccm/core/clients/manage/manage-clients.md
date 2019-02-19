---
title: Gestire i client
titleSuffix: Configuration Manager
description: Informazioni su come gestire i client in System Center Configuration Manager.
ms.date: 12/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8b62ca813b11a6c49366c80623e7c4462e2e4897
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133902"
---
# <a name="how-to-manage-clients-in-system-center-configuration-manager"></a>Come gestire i client in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Quando un client di Configuration Manager viene installato e assegnato correttamente a un sito, il dispositivo viene visualizzato nell'area di lavoro **Asset e conformità** del nodo **Dispositivi** e in una o più raccolte del nodo **Raccolte di dispositivi**. Quando si seleziona il dispositivo o una raccolta, è possibile eseguire le operazioni di gestione. Esistono tuttavia altri modi per gestire i client, che potrebbero interessare altre aree di lavoro della console o attività che non usano la console.  

> [!NOTE]  
>  Se il client di Configuration Manager è installato, ma non è ancora stato assegnato a un sito,è possibile che non venga visualizzato nella console. Dopo aver assegnato il client a un sito, aggiornare l'appartenenza alla raccolta e aggiornare la visualizzazione della console.  
>   
>  È anche possibile che un dispositivo venga visualizzato nella console quando il client di Configuration Manager non è installato. Questo succede se il dispositivo viene individuato, ma il client non è né installato né assegnato. 
>
> I dispositivi mobili gestiti tramite il connettore Exchange Server e i dispositivi registrati in Microsoft Intune non installano il client di Configuration Manager.  
>   
>  Usare la colonna **Client** della console di Configuration Manager per determinare se il client è installato, affinché sia possibile gestirlo dalla console.  

##  <a name="BKMK_ManagingClients_DevicesNode"></a> Gestire i client dal nodo Dispositivi  

A seconda del tipo di dispositivo, alcune di queste opzioni potrebbero non essere disponibili.  

1. Nella console di Configuration Manager scegliere **Asset e conformità** >  **Dispositivi**.  

2. Selezionare uno o più dispositivi, quindi selezionare una di queste attività di gestione client dalla barra multifunzione o facendo clic con il pulsante destro del mouse sul dispositivo:  

   - **Gestire le informazioni di affinità utente dispositivo**  

      Configurare le associazioni tra utenti e dispositivi, per una distribuzione efficiente del software agli utenti.  

      Vedere [Collegare utenti e dispositivi mediante l'affinità utente dispositivo in System Center Configuration Manager](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)  

   - **Aggiungere il dispositivo a una raccolta nuova o esistente**  

      Aggiungere il dispositivo a una raccolta con una regola diretta.  

   - **Installare e reinstallare il client usando l'Installazione push client guidata**  

      Installare e reinstallare il client di Configuration Manager per ripristinarlo o riconfigurarlo. Questa opzione include le impostazioni di configurazione del sito e le proprietà di client.msi impostate per l'installazione push client.  

     > [!TIP]  
     >  Esistono diversi modi per installare e reinstallare il client di Configuration Manager. Sebbene l'Installazione push client guidata consenta di installare il client in modo pratico grazie all'esecuzione dalla console, questo metodo presenta numerose dipendenze e non è adatto a tutti gli ambienti. Per altre informazioni sulle dipendenze, vedere [Prerequisiti per la distribuzione dei client nei computer Windows in System Center Configuration Manager](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md). Per altre informazioni sugli altri metodi di installazione dei client, vedere [Metodi di installazione client in System Center Configuration Manager](../../../core/clients/deploy/plan/client-installation-methods.md).  

      Vedere [Come installare i client di Configuration Manager utilizzando push client](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

   - **Riassegnare il sito**  

      È ora possibile riassegnare uno o più client, inclusi i dispositivi mobili gestiti, a un altro sito principale nella gerarchia. I client possono essere riassegnati singolarmente o possono essere selezionati più volte e riassegnati in massa a un nuovo sito.  

   - **Amministrare in remoto il client**  

      Eseguire Esplora inventario risorse per visualizzare le informazioni sull'inventario hardware e software da un client Windows. Amministrare in remoto il dispositivo tramite Controllo remoto, Assistenza remota o Desktop remoto.  

      Vedere [Come usare Esplora inventario risorse per visualizzare l'inventario hardware](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) e [Come usare Esplora inventario software per visualizzare l'inventario software](../../../core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory.md).  

      Vedere [Come amministrare un computer client Windows in remoto](../../../core/clients/manage/remote-control/remotely-administer-a-windows-client-computer.md).  

   - **Approvare un client**  

      Quando il client comunica con i sistemi del sito mediante HTTP e un certificato autofirmato, è necessario approvare i client per identificarli come computer attendibili. Per impostazione predefinita, la configurazione del sito approva automaticamente i client della stessa foresta Active Directory e delle foreste trusted e non è quindi necessario approvare manualmente ciascun client. È tuttavia necessario approvare manualmente i computer del gruppo di lavoro ritenuti attendibili e altri eventuali computer ritenuti attendibili, ma non approvati.  

     > [!WARNING]  
     >  Sebbene alcune funzioni di gestione potrebbero funzionare per i client non approvati, si tratta di uno scenario non supportato per Configuration Manager.  

      Non è necessario approvare i client che comunicano sempre con i sistemi del sito usando HTTPS o i client che usano un certificato PKI durante la comunicazione con i sistemi del sito mediante HTTP. Questi client stabiliscono relazioni di trust mediante certificati PKI.  

   - **Bloccare o sbloccare un client**  

      È possibile bloccare un client che non è più attendibile. Con il blocco si impedisce al client di ricevere i criteri e ai sistemi del sito di comunicare con il client.  

     > [!WARNING]  
     >  Il blocco di un client impedisce solo la comunicazione del client con i sistemi del sito di Configuration Manager, non la comunicazione con gli altri dispositivi. Inoltre, quando il client comunica con i sistemi del sito mediante HTTP anziché HTTPS, vengono applicate alcune limitazioni di protezione.  

      È anche possibile sbloccare un client bloccato. 

      Vedere [Determinare se bloccare o meno i client in System Center Configuration Manager](../../../core/clients/deploy/plan/determine-whether-to-block-clients.md).  

   - **Cancellare una distribuzione PXE richiesta**  

      Ridistribuire le distribuzioni PXE richieste per il computer.  

      Vedere [Usare PXE per distribuire Windows in rete con System Center Configuration Manager](../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

   - **Gestire le proprietà client**  

      Visualizzare i dati di individuazione e le distribuzioni usate come destinazione per il client. È inoltre possibile configurare le variabili usate dalle sequenze attività per distribuire un sistema operativo nel dispositivo.  

   - **Eliminare il client**  

     > [!WARNING]  
     >  Non eliminare un client se si vuole disinstallare il client di Configuration Manager o rimuoverlo da una raccolta.  

      L'azione **Elimina** consente di eliminare manualmente il record client dal database di Configuration Manager e, in genere, non va usata al di fuori degli scenari di risoluzione dei problemi. Se si elimina il record client, ma il client è ancora installato e comunica con il sito, l'individuazione heartbeat ricrea il record client. Il record client viene nuovamente visualizzato nella console di Configuration Manager, anche se la cronologia client ed eventuali associazioni precedenti andranno perse.  

     > [!NOTE]  
     >  Quando viene eliminato un client di dispositivi mobili registrato da Configuration Manager, l'azione revoca inoltre il certificato PKI rilasciato al dispositivo mobile. Il certificato viene quindi rifiutato dal punto di gestione, anche se IIS non esegue il controllo CRL. I certificati dei client precedenti del dispositivo mobile non vengono revocati quando i client vengono eliminati.  

      Per disinstallare il client, vedere [Disinstallare il client di Configuration Manager](#BKMK_UninstalClient).  

      Per assegnare il client a un nuovo sito primario, vedere [Come assegnare i client a un sito in System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md).  

      Per rimuovere il client da una raccolta, riconfigurare le proprietà della raccolta. Vedere [Come gestire le raccolte in System Center Configuration Manager](../../../core/clients/manage/collections/manage-collections.md).  

   - **Cancellare i dati di un dispositivo mobile**  

      È possibile cancellare i dati dei dispositivi mobili che supportano il comando di cancellazione.  

      Questa azione consente di rimuovere definitivamente tutti i dati del dispositivo mobile, comprese le impostazioni e i dati personali. In genere, questa azione consente di ripristinare le impostazioni di fabbrica nel dispositivo. Cancellare i dati di un dispositivo mobile quando il dispositivo mobile non è più considerato attendibile, ad esempio in caso di furto o smarrimento.  

     > [!TIP]  
     >  Vedere la documentazione del produttore per altre informazioni sull'elaborazione di un comando di cancellazione remota da parte del dispositivo mobile.  

      Si verifica spesso un ritardo nella ricezione del comando di cancellazione da parte del dispositivo mobile:  

     - Se il dispositivo mobile è registrato da Configuration Manager o da Microsoft Intune, il client riceve il comando al momento del download dei criteri client.  

     - Se il dispositivo mobile è gestito dal connettore Exchange Server, riceve il comando al momento della sincronizzazione con Exchange.  

       È possibile usare la colonna **Stato cancellazione** per il monitoraggio della ricezione del comando di cancellazione da parte del dispositivo. Finché il dispositivo non invia un acknowledgment di cancellazione a Configuration Manager, è possibile annullare il comando di cancellazione.  

   - **Ritirare un dispositivo mobile**  

      L'opzione **Ritira** è supportata solo dai dispositivi mobili registrati da Microsoft Intune o da Gestione dispositivi mobili locali.  

      Per altre informazioni, vedere [Proteggere i dati con Cancellazione remota, Blocco remoto o Reimpostazione passcode usando System Center Configuration Manager](../../../mdm/deploy-use/wipe-lock-reset-devices.md).  

   - **Modificare la proprietà di un dispositivo**  

      Se un dispositivo non viene aggiunto a un dominio e non dispone del client di Configuration Manager installato, usare questa opzione per modificare la proprietà in **Società** o **Personale**.  

      È possibile usare questo valore nei requisiti applicazione per controllare le distribuzioni e per controllare il volume dell'inventario raccolto dai dispositivi degli utenti.  

     Può essere necessario aggiungere la colonna **Proprietario dispositivo** alla visualizzazione facendo clic con il pulsante destro del mouse su un'intestazione di colonna e scegliendo l'elemento corrispondente.

      Per altre informazioni, vedere [Gestione di dispositivi mobili ibridi con System Center Configuration Manager e Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

##  <a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> Gestire i client dal nodo Raccolte di dispositivi  
  Molte delle attività disponibili per i dispositivi nel nodo **Dispositivi** sono presenti anche nelle raccolte. La console applica automaticamente l'operazione a tutti i dispositivi idonei della raccolta. Questa azione eseguita in un'intera raccolta genera pacchetti di rete aggiuntivi e aumenta l'utilizzo della CPU nel server del sito.  

  Prima di eseguire attività a livello di raccolta, tenere presente quanto segue. Una volta avviata, non è possibile arrestare l'attività dalla console. 
 - Il numero di dispositivi presenti nella raccolta
 - Se i dispositivi usano una connessione di rete con larghezza di banda ridotta
 - Il tempo necessario all'attività per essere completata in tutti i dispositivi

#### <a name="to-manage-clients-from-the-device-collections-node"></a>Per gestire i client dal nodo Raccolte dispositivi  

1.  Nella console di Configuration Manager scegliere **Asset e conformità** > **Raccolte dispositivi**.  

3.  Selezionare una raccolta, quindi selezionare una delle seguenti attività di gestione client dalla barra multifunzione o facendo clic con il pulsante destro del mouse sulla raccolta. Queste attività di gestione client possono essere eseguite *solo* a livello di raccolta.  

    -   **Eseguire la scansione dei computer per rilevare la presenza di malware e scaricare i file di definizione antimalware.**  

         Vedere [Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

    -   **Distribuire software, linee di base della configurazione e sequenze attività.**  

         Vedere:  

        -   [Distribuire gli aggiornamenti software in System Center Configuration Manager](../../../sum/deploy-use/deploy-software-updates.md)  

        -   [Pianificare e configurare le impostazioni di conformità in System Center Configuration Manager](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)  

    -   **Configurare le impostazioni di risparmio energia.**  

         Vedere [Come creare e applicare combinazioni per il risparmio di energia in System Center Configuration Manager](../../../core/clients/manage/power/create-and-apply-power-plans.md). Le combinazioni per il risparmio di energia sono utilizzabili solo con computer che eseguono Windows.  

    -   **Inviare una notifica ai computer per il download dei criteri appena possibile.**  

         Usare la notifica client per inviare una notifica ai client Windows selezionati per il download dei criteri computer appena possibile all'esterno dell'intervallo di polling dei criteri client.  

         Le attività di notifica client vengono visualizzate nel nodo **Operazioni client** dell'area di lavoro **Monitoraggio** .  


## <a name="restart-clients"></a>Riavviare i client
A partire dalla versione 1710, è possibile usare la console di Configuration Manager per identificare i client che devono essere riavviati. Usare quindi un'azione di notifica client per riavviarli.

> [!Tip]
> Per usare questa funzionalità, è anche necessario aggiornare i client alla versione 1710. È consigliabile abilitare l'aggiornamento client automatico per mantenere i client aggiornati e ridurre al minimo il carico amministrativo. Per altre informazioni, vedere [Usare l'aggiornamento client automatico](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade).

Per identificare i dispositivi che sono in attesa di riavvio, passare all'area di lavoro **Asset e conformità** nella console di Configuration Manager e selezionare il nodo **Dispositivi**. È ora possibile visualizzare lo stato di ogni dispositivo nel riquadro dei dettagli, in una nuova colonna denominata **Riavvio in sospeso**. Ogni dispositivo può avere uno o più dei valori seguenti: 
 - **No**: non sono presenti riavvi in sospeso
 - **Configuration Manager**: questo valore proviene dal componente che coordina il riavvio del client (RebootCoordinator.log)
 - **Ridenominazione di file**: questo valore proviene da Windows e segnala un'operazione di ridenominazione file in sospeso (HKLM\SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations)
 - **Windows Update**: questo valore proviene dall'agente di Windows Update e segnala la necessità di un riavvio in sospeso per uno o più aggiornamenti (HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired)
 - **Aggiungi o rimuovi la funzionalità**: questo valore proviene dal modulo di manutenzione pacchetti basato su componenti di Windows e segnala che l'aggiunta o la rimozione di una funzionalità di Windows richiede un riavvio (HKLM\Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\Reboot Pending)

**Per creare la notifica client per riavviare un dispositivo:**
1.  Individuare il dispositivo da riavviare all'interno della raccolta nel nodo **Raccolte di dispositivi** della console.
2.  Fare clic con il pulsante destro del mouse sul dispositivo, scegliere **Notifica client** e quindi selezionare **Riavvia**. Si aprirà una finestra contenente le informazioni sul riavvio. Fare clic su **OK** per riavviare la richiesta.

Quando la notifica viene ricevuta da un client, viene visualizzata una finestra di notifica di **Software Center** per informare l'utente del riavvio. Per impostazione predefinita, il riavvio viene eseguito dopo 90 minuti. È possibile modificare il tempo di riavvio configurando le [impostazioni client](/sccm/core/clients/deploy/configure-client-settings). Le impostazioni per il comportamento del riavvio sono disponibili nella scheda [Riavvio del computer](/sccm/core/clients/deploy/about-client-settings#computer-restart) delle impostazioni predefinite.


##  <a name="BKMK_ClientCache"></a> Configurare la cache del client per i client di Configuration Manager  
La cache client archivia i file temporanei per l'installazione di applicazioni e programmi nei client. Anche gli aggiornamenti software usano la cache del client, tentando di eseguire sempre il download nella cache indipendentemente dall'impostazione delle dimensioni. Configurare le impostazioni della cache client, ad esempio dimensioni e percorso, quando si installa manualmente il client, quando si usa l'installazione push client oppure dopo l'installazione.

A partire dalla versione 1606 di Configuration Manager, è possibile specificare le dimensioni della cartella della cache usando le impostazioni client nella console di Configuration Manager.   

 Il percorso predefinito per la cache del client di Configuration Manager è %*windir*%\ccmcache e lo spazio su disco predefinito è 5120 MB.  

> [!IMPORTANT]  
>  Non crittografare la cartella usata per la cache client. Configuration Manager non può scaricare il contenuto in una cartella crittografata.  

### <a name="about-client-cache"></a>Dimensione della cache del client  

Il client di Configuration Manager scarica il contenuto per il software richiesto non appena riceve la distribuzione ma non effettua l'esecuzione fino all'ora di distribuzione pianificata. All'ora pianificata, il client di Configuration Manager controlla se il contenuto è disponibile nella cache. Se il contenuto è disponibile nella cache e la versione è corretta, il client usa il contenuto nella cache. Quando la versione richiesta del contenuto viene modificata o se il contenuto viene eliminato dal client per liberare spazio per un altro pacchetto, il client scarica nuovamente il contenuto nella cache.  

Se il client tenta di scaricare il contenuto per un programma o un'applicazione di dimensioni superiori rispetto a quelle della cache, la distribuzione ha esito negativo perché le dimensioni della cache non sono sufficienti. Il client genera il messaggio di stato 10050 per dimensioni della cache non sufficienti. Se le dimensioni della cache vengono aumentate in un secondo momento, il risultato è il seguente:  

-   Per un programma richiesto: il client non tenterà automaticamente di scaricare il contenuto. Ridistribuire il programma e il pacchetto al client.  
-   Per un'applicazione richiesta: il client proverà automaticamente a scaricare il contenuto al momento del download dei criteri client.  

Se il client tenta di scaricare un pacchetto di dimensioni inferiori rispetto a quelle della cache, ma la cache è piena, tutte le distribuzioni richieste eseguiranno altri tentativi finché non sarà disponibile spazio nella cache, non si verificherà un timeout del download oppure non verrà raggiunto il numero massimo di tentativi. Se in seguito la dimensione della cache viene aumentata, il client di Configuration Manager tenterà di scaricare nuovamente il pacchetto al successivo intervallo tra tentativi. Il client tenterà di scaricare il contenuto ogni quattro ore finché non avrà eseguito 18 tentativi.  

Il contenuto nella cache non viene eliminato automaticamente ma rimane nella cache per almeno un giorno dopo essere stato usato dal client. Se si configurano le proprietà del pacchetto con l'opzione per mantenere il contenuto nella cache client, il client non elimina automaticamente il contenuto del pacchetto dalla cache. Se lo spazio nella cache viene usato dai pacchetti scaricati nelle ultime 24 ore e il client deve scaricare nuovi pacchetti, è possibile aumentare le dimensioni della cache oppure scegliere l'opzione per eliminare il contenuto della cache persistente.  

 Usare le seguenti procedure per configurare la cache client durante l'installazione client manuale oppure dopo l'installazione client.  

### <a name="to-configure-the-client-cache-when-you-install-clients-by-using-manual-client-installation"></a>Per configurare la cache client durante l'installazione client usando l'installazione client manuale  

Eseguire il comando CCMSetup.exe dal percorso di origine di installazione e specificare le seguenti proprietà richieste e separate da spazi:  

- DISABLECACHEOPT  

  - SMSCACHEDIR  

  - SMSCACHEFLAGS  

  - SMSCACHESIZE  

    > [!NOTE]
    > Per la versione 1606, usare le impostazioni della dimensione della cache disponibili in **Impostazioni client** nella console di Configuration Manager anziché SMSCACHESIZE. Per altre informazioni vedere [Impostazioni della cache dei client](../../../core/clients/deploy/about-client-settings.md#client-cache-settings).

Per altre informazioni sull'uso delle proprietà della riga di comando di CCMSetup.exe, vedere [Informazioni sulle proprietà di installazione del client](../../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="to-configure-the-client-cache-folder-when-you-install-clients-by-using-client-push-installation"></a>Per configurare la cartella cache client durante l'installazione client usando l'installazione push client  

1. Nella console di Configuration Manager scegliere **Amministrazione** > **Configurazione del sito** > **Siti**.  

2. Selezionare il sito appropriato e nella scheda **Home**, nel gruppo **Impostazioni**, scegliere **Impostazioni di installazione client** > **scheda Proprietà di installazione**.  

3. Specificare le seguenti proprietà, separate da spazi:  

   - DISABLECACHEOPT  

   - SMSCACHEDIR  

   - SMSCACHEFLAGS  

   - SMSCACHESIZE  

     > [!NOTE]
     > Per la versione 1606, usare le impostazioni della dimensione della cache disponibili in **Impostazioni client** nella console di Configuration Manager anziché SMSCACHESIZE. Per altre informazioni vedere [Impostazioni della cache dei client](../../../core/clients/deploy/about-client-settings.md#client-cache-settings).

     Per altre informazioni sull'uso delle proprietà della riga di comando di CCMSetup.exe, vedere [Informazioni sulle proprietà di installazione del client](../../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="to-configure-the-client-cache-folder-on-the-client-computer"></a>Per configurare la cartella cache del client sul computer client  

1.  Nel Pannello di controllo del computer client passare a **Configuration Manager** e fare doppio clic per aprire le proprietà.  

2.  Nella scheda **Cache** impostare le proprietà per lo spazio e il percorso. Il percorso predefinito è *%windir%* \ccmcache.  

3.  Per eliminare i file nella cartella della cache, scegliere **Elimina file**.  

### <a name="to-configure-client-cache-size-in-client-settings"></a>Per configurare la dimensione della cache del client in Impostazioni client

Regolare le dimensioni della cache del client senza reinstallare il client. Configurare le dimensioni della cache nella console di Configuration Manager tramite Impostazioni client.  

1. Nella console di Configuration Manager scegliere **Amministrazione** > **Impostazioni client**.

2. Fare doppio clic su **Impostazioni client predefinite**.
   È anche possibile creare impostazioni client personalizzate per applicare la dimensione della cache in modo più selettivo. Per altre informazioni sulle impostazioni client predefinite e personalizzate, vedere [Come configurare le impostazioni client in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

   3. Scegliere **Impostazioni della cache del client**, scegliere **Sì** per **Configurare le dimensioni della cache del client**, quindi usare l'impostazione in **MB** o la **percentuale del disco**. La cache viene adeguata alla dimensione che risulta inferiore.

      Il client di Configuration Manager configurerà la dimensione della cache con queste impostazioni al successivo download dei criteri client.



##  <a name="BKMK_UninstalClient"></a> Disinstallare il client di Configuration Manager  
 È possibile disinstallare il software client di Windows Configuration Manager da un computer usando **CCMSetup.exe** con la proprietà **/Uninstall**. Eseguire CCMSetup.exe in un singolo computer dal prompt dei comandi oppure distribuire un pacchetto e programma per disinstallare il client da una raccolta di computer.  

> [!WARNING]  
>  È impossibile disinstallare il client di Configuration Manager da un dispositivo mobile. Se è necessario rimuovere il client di Configuration Manager da un dispositivo mobile, è necessario cancellare il dispositivo eliminando tutti i dati nel dispositivo mobile.  

#### <a name="to-uninstall-the-configuration-manager-client-from-the-command-prompt"></a>Per disinstallare il client di Configuration Manager dal prompt dei comandi  

1.  Aprire un prompt dei comandi di Windows e modificare la cartella del percorso in cui si trova CCMSetup.exe.  

2.  Digitare **Ccmsetup.exe /uninstall**e quindi premere **Invio**.  

> [!NOTE]  
>  I risultati del processo di disinstallazione non vengono visualizzati sullo schermo. Per verificare il completamento della disinstallazione client, esaminare il file di log **CCMSetup.log** nella cartella *%windir%\ ccmsetup* nel computer client.  

##  <a name="BKMK_ConflictingRecords"></a> Gestire i record in conflitto per i client di Configuration Manager  
 Configuration Manager usa l'identificatore hardware per tentare di identificare i client che potrebbero essere dei duplicati e avvertire l'utente dei record in conflitto. Ad esempio, se si reinstalla un computer, l'identificatore hardware rimane lo stesso mentre il GUID usato da Configuration Manager potrebbe cambiare.  

 Configuration Manager risolve automaticamente i conflitti usando l'autenticazione di Windows dell'account computer o un certificato PKI proveniente da un'origine attendibile. Quando per Configuration Manager non è tuttavia possibile risolvere il conflitto di identificatori hardware duplicati, un'impostazione gerarchia determina se unire automaticamente i record oppure se consentire all'utente di definire il comportamento. Se si decide di gestire manualmente i record duplicati, è necessario risolvere manualmente i record in conflitto nella console di Configuration Manager.  


#### <a name="to-change-the-hierarchy-setting-for-managing-conflicting-records"></a>Per modificare l'impostazione della gerarchia per la gestione dei record in conflitto  

1.  Nella console di Configuration Manager scegliere **Amministrazione** > **Configurazione del sito** > **Siti** > **Impostazioni gerarchia**
2.  Nella scheda **Approvazione client e record in conflitto** scegliere **Risolvi automaticamente record in conflitto** o **Risolvi manualmente record in conflitto**.  

#### <a name="to-manually-resolve-conflicting-records"></a>Per risolvere manualmente i record in conflitto  

1.  Nella console di Configuration Manager scegliere **Monitoraggio** > **Stato del sistema** > **Record in conflitto**.  

3.  Selezionare uno o più record in conflitto e quindi scegliere **Record in conflitto**.  

4.  Selezionare una delle opzioni seguenti:  

    -   **Unisci** per combinare il record appena rilevato con il record client esistente.  

    -   **Nuovo** per creare un nuovo record per il record client in conflitto.  

    -   **Blocca** per creare un nuovo record per il record client in conflitto, ma contrassegnandolo come bloccato.  

## <a name="manage-duplicate-hardware-identifiers"></a>Gestire gli identificatori di hardware duplicati
Specificando un elenco di identificatori hardware che Configuration Manager deve ignorare nel caso di riavvio PXE e registrazione client, è possibile risolvere due problemi comuni.

1. Molti nuovi dispositivi, ad esempio Surface Pro 3, non includono una porta Ethernet incorporata. I tecnici usano un adattatore da USB a Ethernet per stabilire una connessione cablata per la distribuzione del sistema operativo. Si tratta tuttavia spesso di adattatori condivisi, per motivi di costi e usabilità generale. Poiché per identificare il dispositivo viene usato l'indirizzo MAC dell'adattatore, risulta problematico riusare l'adattatore senza interventi aggiuntivi dell'amministratore tra le diverse distribuzioni. Per riusare l'adattatore in questo scenario, escluderne l'indirizzo MAC.
2. Mentre l'attributo SMBIOS è univoco, per alcuni dispositivi hardware specifici gli identificatori sono duplicati. Escludere l'identificatore duplicato e usare l'indirizzo MAC univoco di ogni dispositivo.

#### <a name="to-add-hardware-identifiers-for-configuration-manager-to-ignore"></a>Per aggiungere identificatori hardware che Configuration Manager deve ignorare  
1. Nella console di Configuration Manager andare su **Amministrazione** > **Panoramica** > **Configurazione del sito** > **Siti**.
2. Nella scheda **Home** del gruppo **Siti** scegliere **Impostazioni gerarchia**.
3. Nella scheda **Approvazione client e record in conflitto** scegliere **Aggiungi** nella sezione **Identificatori hardware duplicati** per aggiungere nuovi identificatori hardware.

##  <a name="BKMK_PolicyRetrieval"></a> Avviare il recupero criteri per un client di Configuration Manager  
 Un client di Windows Configuration Manager scarica i relativi criteri client in base a una pianificazione configurata come impostazione client. In alcuni casi, tuttavia, può essere necessario avviare un recupero criteri su richiesta dal client, ad esempio per la risoluzione dei problemi oppure durante una verifica.  

È possibile avviare il recupero dei criteri tramite:


- [Notifica client](#initiate-client-policy-retrieval-using-client-notification)
- [La scheda **Azioni** nel client](#manually-initiate-client-policy-retrieval-on-the-actions-tab-of-the-configuration-manager-client)
- [Uno script](#manually-initiate-client-policy-retrieval-by-script)

> [!NOTE]  
>   
>  Per informazioni sul recupero dei criteri per i client che eseguono Linux e UNIX, vedere [Computer policy for Linux and UNIX servers](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_PolicyforLnU).  

#### <a name="initiate-client-policy-retrieval-using-client-notification"></a>Avviare il recupero dei criteri client usando la notifica client  

1.  Nella console di Configuration Manager scegliere **Asset e conformità** > **Raccolte dispositivi**.  

3.  Selezionare la raccolta di dispositivi che contiene i computer per cui scaricare i criteri. Nella scheda **Home**, nel gruppo **Raccolte**, scegliere **Notifica client** > **Scarica criteri computer**.  

    > [!NOTE]  
    >  È inoltre possibile usare la notifica client per avviare il recupero criteri per uno o più dispositivi selezionati visualizzati in un nodo raccolta temporaneo nel nodo **Dispositivi** .  

#### <a name="manually-initiate-client-policy-retrieval-on-the-actions-tab-of-the-configuration-manager-client"></a>Avviare manualmente il recupero dei criteri client nella scheda Azioni del client di Configuration Manager  

1.  Selezionare **Configuration Manager** nel Pannello di controllo del computer.  

2.  Nella scheda **Azioni** scegliere **Ciclo di recupero e valutazione criteri computer** per avviare i criteri computer e scegliere **Esegui**.  

4.  Scegliere **OK** per confermare la richiesta.  

5.  Ripetere i passaggi 3 e 4 per ogni altra azione richiesta, ad esempio **Ciclo di recupero e valutazione criteri utente** per le impostazioni client utente.  

#### <a name="manually-initiate-client-policy-retrieval-by-script"></a>Avviare manualmente il recupero criteri client tramite uno script  

1.  Aprire un editor di testo, come Blocco note.  

2.  Copiare e inserire il codice di esempio di Visual Basic Scripting Edition seguente nel file:  

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

5.  Scegliere **OK** nella finestra di dialogo **Windows Script Host**.  

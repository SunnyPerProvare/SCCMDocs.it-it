---
title: Gestire i client
titleSuffix: Configuration Manager
description: Informazioni su come gestire i client in Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 3986a992-c175-4b6f-922e-fc561e3d7cb7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 53ee871a712290c4e74398fd467064aee5f56a9b
ms.sourcegitcommit: f31916c633277cc09b2125f9b7deee131453479b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/15/2020
ms.locfileid: "79405944"
---
# <a name="how-to-manage-clients-in-configuration-manager"></a>Come gestire i client in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Quando un client di Configuration Manager viene installato e assegnato correttamente a un sito, il dispositivo viene visualizzato nell'area di lavoro **Asset e conformità** del nodo **Dispositivi** e in una o più raccolte del nodo **Raccolte di dispositivi**. Selezionare il dispositivo o una raccolta e quindi eseguire le operazioni di gestione. Esistono tuttavia altri modi per gestire i client, che potrebbero interessare altre aree di lavoro della console o attività che non usano la console.  

> [!NOTE]  
> Se si installa il client di Configuration Manager, ma non è ancora stato assegnato a un sito,è possibile che non venga visualizzato nella console. Dopo aver assegnato il client a un sito, aggiornare l'appartenenza alla raccolta e quindi aggiornare la visualizzazione della console.  
>
> È anche possibile che un dispositivo venga visualizzato nella console quando il client di Configuration Manager non è installato. Questo comportamento si verifica se il sito individua un dispositivo ma il client non è installato e assegnato.
>
> I dispositivi mobili gestiti con il [connettore Exchange Server](/configmgr/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync) o una soluzione [MDM locale](/configmgr/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure) non installano il client di Configuration Manager.  
>
> Per gestire un dispositivo dalla console, usare la colonna **Client** nel nodo **Dispositivi** per determinare se il client è installato.  

## <a name="manage-clients-from-the-devices-node"></a><a name="BKMK_ManagingClients_DevicesNode"></a> Gestire i client dal nodo **Dispositivi**  

A seconda del tipo di dispositivo, alcune di queste opzioni potrebbero non essere disponibili.  

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità** e selezionare il nodo **Dispositivi**.  

2. Selezionare uno o più dispositivi, quindi selezionare una di queste attività di gestione client dalla barra multifunzione. È anche possibile fare clic con il pulsante destro del mouse sul dispositivo.  

### <a name="import-user-device-affinity"></a>Importa affinità utente dispositivo

Configurare le associazioni tra utenti e dispositivi, per una distribuzione efficiente del software agli utenti.  

Per altre informazioni, vedere [Collegare utenti e dispositivi mediante l'affinità utente dispositivo](/configmgr/apps/deploy-use/link-users-and-devices-with-user-device-affinity).

### <a name="import-computer-information"></a>Importa informazioni computer

Avviare l'**Importazione guidata informazioni computer** per importare nuove informazioni sui computer nel database di Configuration Manager. È possibile importare più computer usando un file o specificare le informazioni per un singolo computer.

### <a name="add-selected-items"></a>Aggiungi elementi selezionati

Fornisce le opzioni seguenti:

- **Aggiungi elementi selezionati alla raccolta dispositivi esistente**: Apre la finestra di dialogo **Seleziona raccolta** . Selezionare la raccolta a cui si vuole aggiungere il dispositivo. Il dispositivo viene incluso in questa raccolta tramite una regola di appartenenza **diretta**.  

- **Aggiungi elementi selezionati alla nuova raccolta dispositivi**: apre la **Creazione guidata raccolta dispositivi** in cui è possibile creare una nuova raccolta. La raccolta selezionata viene inclusa in questa raccolta tramite una regola di appartenenza **diretta**.  

Per altre informazioni, vedere [Come creare le raccolte](/configmgr/core/clients/manage/collections/create-collections).

### <a name="install-client"></a>Installa client

Apre la **procedura guidata Installa client**. Questa procedura guidata usa l'installazione push client per installare o reinstallare il client di Configuration Manager nel dispositivo selezionato.

> [!TIP]  
> Esistono molti modi diversi per installare il client di Configuration Manager. Sebbene l'Installazione push client guidata consenta di installare il client in modo pratico dalla console, questo metodo presenta numerose dipendenze e non è adatto a tutti gli ambienti. Per altre informazioni sulle dipendenze, vedere [Prerequisiti per la distribuzione dei client nei computer Windows](/configmgr/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#client-push-installation). Per altre informazioni sugli altri metodi di installazione client, vedere [Metodi di installazione client](/configmgr/core/clients/deploy/plan/client-installation-methods).

Per altre informazioni, vedere [Come installare i client di Configuration Manager usando push client](/configmgr/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).

### <a name="run-script"></a>Esegui script

Apre la procedura guidata **Esegui script** per eseguire uno script di PowerShell nel dispositivo selezionato.

Per altre informazioni, vedere [Creare ed eseguire script di PowerShell](/configmgr/apps/deploy-use/create-deploy-scripts).

### <a name="install-application"></a>Installa applicazione

Consente di installare un'applicazione in un dispositivo in tempo reale. Questa funzionalità consente di ridurre la necessità di raccolte separate per ogni applicazione.

Per altre informazioni, vedere [Installare applicazioni per un dispositivo](/configmgr/apps/deploy-use/install-app-for-device).

### <a name="reassign-site"></a>Riassegna sito

È ora possibile riassegnare uno o più client, inclusi i dispositivi mobili gestiti, a un altro sito principale nella gerarchia. È possibile riassegnare singolarmente i client o selezionarne più di uno per riassegnarli in blocco.  

### <a name="client-settings---resultant-client-settings"></a>Impostazioni client - Impostazioni client risultanti

Quando vengono distribuite più impostazioni client allo stesso dispositivo, la definizione delle priorità e la combinazione delle impostazioni risultano complesse. Usare questa opzione per visualizzare il set di impostazioni client risultante distribuito in questo dispositivo.

Per altre informazioni, vedere [Come configurare le impostazioni client](/configmgr/core/clients/deploy/configure-client-settings).

### <a name="start"></a>Avvia

- Eseguire **Esplora inventario risorse** per visualizzare le informazioni sull'inventario hardware e software da un client Windows. Per altre informazioni, vedere gli articoli seguenti:

  - [Come usare Esplora inventario risorse per visualizzare l'inventario hardware](/configmgr/core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory)

  - [Come usare Esplora inventario software per visualizzare l'inventario software](/configmgr/core/clients/manage/inventory/use-resource-explorer-to-view-software-inventory)

- Amministrare in remoto il dispositivo tramite **Controllo remoto**, **Assistenza remota** o **Client Desktop remoto**. Per altre informazioni, vedere [Come amministrare un computer client Windows in remoto](/configmgr/core/clients/manage/remote-control/remotely-administer-a-windows-client-computer).

### <a name="approve"></a>Approva

Quando il client comunica con i sistemi del sito mediante HTTP e un certificato autofirmato, è necessario approvare i client per identificarli come computer attendibili. Per impostazione predefinita, la configurazione del sito approva automaticamente i client della stessa foresta di Active Directory e delle foreste trusted. Questo comportamento predefinito significa che non è necessario approvare manualmente ogni client. Approvare manualmente i computer del gruppo di lavoro ritenuti attendibili e altri eventuali computer ritenuti attendibili, ma non approvati.

> [!IMPORTANT]  
> Sebbene alcune funzioni di gestione potrebbero funzionare per i client non approvati, si tratta di uno scenario non supportato per Configuration Manager.  

Non è necessario approvare i client che comunicano sempre con i sistemi del sito usando HTTPS o i client che usano un certificato PKI per le comunicazioni con i sistemi del sito mediante HTTP. Questi client stabiliscono relazioni di trust mediante certificati PKI.

### <a name="block-or-unblock"></a>Blocca o Sblocca

È possibile bloccare un client che non è più attendibile. Con il blocco si impedisce al client di ricevere i criteri e ai sistemi del sito di comunicare con il client.  

> [!IMPORTANT]  
> Il blocco di un client impedisce solo la comunicazione dal client ai sistemi del sito di Configuration Manager, non la comunicazione con gli altri dispositivi. Quando il client comunica con i sistemi del sito mediante HTTP anziché HTTPS, vengono applicate alcune limitazioni di sicurezza.  

È anche possibile sbloccare un client bloccato.

Per altre informazioni, vedere [Determinare se bloccare i client](/configmgr/core/clients/deploy/plan/determine-whether-to-block-clients).

<!-- Change Category is a hybrid action -->

### <a name="clear-required-pxe-deployments"></a>Cancella distribuzioni PXE richieste

È possibile ridistribuire una distribuzione PXE richiesta cancellando lo stato dell'ultima distribuzione PXE assegnato a una raccolta di Configuration Manager o a un computer. Questa azione consente di reimpostare lo stato di quella distribuzione e reinstalla le distribuzioni richieste più recenti.

Per altre informazioni, vedere [Usare PXE per distribuire Windows in rete](/configmgr/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).

### <a name="client-notification"></a>Notifica client

Per altre informazioni, vedere [Client notifications](/configmgr/core/clients/manage/client-notification#client-notification) (Notifiche client).

### <a name="endpoint-protection"></a>Endpoint Protection

Per altre informazioni, vedere [Client notifications](/configmgr/core/clients/manage/client-notification#endpoint-protection) (Notifiche client).

### <a name="edit-primary-users"></a>Modifica utenti primari

Consente di visualizzare gli utenti del dispositivo negli ultimi 90 giorni oppure di specificare gli utenti primari del dispositivo.

Per altre informazioni, vedere [Collegare utenti e dispositivi mediante l'affinità utente dispositivo](/configmgr/apps/deploy-use/link-users-and-devices-with-user-device-affinity).

### <a name="wipe-a-mobile-device"></a>Cancellare i dati di un dispositivo mobile

È possibile cancellare i dati dei dispositivi mobili che supportano il comando di cancellazione. Questa azione consente di rimuovere definitivamente tutti i dati del dispositivo mobile, comprese le impostazioni e i dati personali. In genere, questa azione consente di ripristinare le impostazioni di fabbrica nel dispositivo. Cancellare i dati di un dispositivo mobile quando non è più attendibile, ad esempio in caso di furto o smarrimento.  

> [!TIP]  
> Vedere la documentazione del produttore per altre informazioni sull'elaborazione di un comando di cancellazione remota da parte del dispositivo mobile.  

Si verifica spesso un ritardo nella ricezione del comando di cancellazione da parte del dispositivo mobile:  

- Se il dispositivo mobile è registrato da Configuration Manager, il client riceve il comando al momento del download dei criteri client.

- Se il dispositivo mobile è gestito dal connettore Exchange Server, riceve il comando al momento della sincronizzazione con Exchange.  

Per monitorare la ricezione del comando di cancellazione da parte del dispositivo, usare la colonna **Stato cancellazione**. Finché il dispositivo non invia un acknowledgment di cancellazione a Configuration Manager, è possibile annullare il comando di cancellazione.  

### <a name="retire-a-mobile-device"></a>Ritirare un dispositivo mobile

L'opzione **Ritira** è supportata solo dai dispositivi mobili registrati da una soluzione MDM locale.  

Per altre informazioni, vedere [Proteggere i dati con cancellazione remota, blocco remoto o reimpostazione passcode](/configmgr/mdm/deploy-use/wipe-lock-reset-devices).

### <a name="change-ownership"></a>Modifica proprietà

Se un dispositivo non è aggiunto a un dominio e non dispone del client di Configuration Manager installato, usare questa opzione per modificare la proprietà in **Società** o **Personale**.  

È possibile usare questo valore nei requisiti applicazione per controllare le distribuzioni e per controllare il volume dell'inventario raccolto dai dispositivi degli utenti.  

Può essere necessario aggiungere la colonna **Proprietario dispositivo** alla visualizzazione facendo clic con il pulsante destro del mouse su un'intestazione di colonna e scegliendo l'elemento corrispondente.

### <a name="delete"></a>Elimina

> [!WARNING]  
> Non eliminare un client se si vuole disinstallare il client di Configuration Manager o rimuoverlo da una raccolta.  

L'azione **Elimina** rimuove manualmente il record client dal database di Configuration Manager. Usare questa azione solo per risolvere un problema. Se si elimina l'oggetto, ma il client è ancora installato e comunica con il sito, Individuazione heartbeat ricrea il record client. Il record client viene nuovamente visualizzato nella console di Configuration Manager, anche se la cronologia client ed eventuali associazioni precedenti vanno perdute.  
> [!NOTE]  
> Quando si elimina un client di dispositivi mobili registrato da Configuration Manager, questa azione revoca anche il certificato PKI emesso. Il certificato viene quindi rifiutato dal punto di gestione, anche se IIS non controlla l'elenco di revoche di certificati.
>
> I certificati dei client precedenti del dispositivo mobile non vengono revocati quando i client vengono eliminati.

Per disinstallare il client, vedere [Disinstallare il client di Configuration Manager](#BKMK_UninstalClient).  

Per assegnare il client a un nuovo sito primario, vedere [Come assegnare i client a un sito](/configmgr/core/clients/deploy/assign-clients-to-a-site).

Per rimuovere il client da una raccolta, riconfigurare le proprietà della raccolta. Per altre informazioni, vedere [Come gestire le raccolte](/configmgr/core/clients/manage/collections/manage-collections).

### <a name="refresh"></a>Aggiorna

Aggiornare la visualizzazione della console con i dati più recenti nel database. Ad esempio, se un dispositivo compare nell'elenco dall'individuazione, ma non viene visualizzato come installato. Dopo aver installato il client e avere verificato che sia assegnato al sito, selezionare **Aggiorna**.

### <a name="properties"></a>Proprietà

Visualizzare i dati di individuazione e le distribuzioni usate come destinazione per il client.

È anche possibile configurare le variabili usate dalle sequenze di attività per distribuire un sistema operativo nel dispositivo. Per altre informazioni, vedere [Creare le variabili della sequenza di attività per dispositivi e raccolte](/configmgr/osd/understand/using-task-sequence-variables#bkmk_set-coll-var).


## <a name="manage-clients-from-the-device-collections-node"></a><a name="BKMK_ManagingClients_DeviceCollectionsNode"></a> Gestire i client dal nodo **Raccolte di dispositivi**

Molte delle attività disponibili per i dispositivi nel nodo **Dispositivi** sono presenti anche nelle raccolte. La console applica automaticamente l'operazione a tutti i dispositivi idonei della raccolta. Questa azione eseguita in un'intera raccolta genera pacchetti di rete aggiuntivi e aumenta l'utilizzo della CPU nel server del sito.  

Prima di eseguire attività a livello di raccolta, prendere in considerazione le domande seguenti. Una volta avviata, non è possibile arrestare l'attività dalla console.

- Il numero di dispositivi presenti nella raccolta
- Se i dispositivi usano una connessione di rete con larghezza di banda ridotta
- Il tempo necessario all'attività per essere completata in tutti i dispositivi

Per altre informazioni, vedere [Come gestire le raccolte](/configmgr/core/clients/manage/collections/manage-collections).


## <a name="restart-clients"></a>Riavviare i client

Usare la console di Configuration Manager per identificare i client che devono essere riavviati. Usare quindi un'azione di notifica client per riavviarli.

> [!Tip]
> Abilitare l'aggiornamento automatico dei client per mantenere i client aggiornati con il minimo sforzo. Per altre informazioni, vedere [Informazioni sull'aggiornamento client automatico](/configmgr/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#bkmk_autoupdate).

Per identificare i dispositivi che sono in attesa di riavvio, passare all'area di lavoro **Asset e conformità** nella console di Configuration Manager e selezionare il nodo **Dispositivi**. È ora possibile visualizzare lo stato di ogni dispositivo nel riquadro dei dettagli, in una nuova colonna denominata **Riavvio in sospeso**. Ogni dispositivo può avere uno o più dei valori seguenti:

- **No**: non sono presenti riavvi in sospeso
- **Configuration Manager**: questo valore proviene dal componente che coordina il riavvio del client (RebootCoordinator.log)
- **Ridenominazione di file**: questo valore proviene da Windows e segnala un'operazione di ridenominazione file in sospeso (HKLM\SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations)
- **Windows Update**: questo valore proviene dall'agente di Windows Update e segnala la necessità di un riavvio in sospeso per uno o più aggiornamenti (HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired)
- **Aggiungi o rimuovi la funzionalità**: questo valore proviene dal modulo di manutenzione pacchetti basato su componenti di Windows e segnala che l'aggiunta o la rimozione di una funzionalità di Windows richiede un riavvio (HKLM\Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\Reboot Pending)

### <a name="create-the-client-notification-to-restart-a-device"></a>Creare la notifica client per riavviare un dispositivo

1. Selezionare il dispositivo da riavviare all'interno della raccolta nel nodo **Raccolte di dispositivi** della console.
2. Nella barra multifunzione selezionare **Notifica client** e quindi **Riavvia**. Si aprirà una finestra contenente le informazioni sul riavvio. Selezionare **OK** per confermare la richiesta di riavvio.

Quando la notifica viene ricevuta da un client, viene visualizzata una finestra di notifica di **Software Center** per informare l'utente del riavvio. Per impostazione predefinita, il riavvio viene eseguito dopo 90 minuti. È possibile modificare il tempo di riavvio configurando le [impostazioni client](/configmgr/core/clients/deploy/configure-client-settings). Le impostazioni per il comportamento del riavvio sono disponibili nella scheda [Riavvio del computer](/configmgr/core/clients/deploy/about-client-settings#computer-restart) delle impostazioni predefinite.


## <a name="configure-the-client-cache"></a><a name="BKMK_ClientCache"></a> Configurare la cache del client

La cache client archivia i file temporanei per l'installazione di applicazioni e programmi nei client. Anche gli aggiornamenti software usano la cache del client, tentando di eseguire sempre il download nella cache indipendentemente dall'impostazione delle dimensioni. Configurare le impostazioni della cache client, ad esempio dimensioni e percorso, quando si installa manualmente il client, quando si usa l'installazione push client oppure dopo l'installazione.

È possibile specificare le dimensioni della cartella della cache usando le impostazioni client nella console di Configuration Manager. Per altre informazioni vedere [Impostazioni della cache dei client](/configmgr/core/clients/deploy/about-client-settings#client-cache-settings).

Il percorso predefinito per la cache del client di Configuration Manager è `%windir%\ccmcache` e lo spazio su disco predefinito è 5120 MB.  

> [!IMPORTANT]  
> Non crittografare la cartella usata per la cache del client. Configuration Manager non può scaricare il contenuto in una cartella crittografata.  

### <a name="about-the-client-cache"></a>Informazioni sulla cache del client  

Il client di Configuration Manager scarica il contenuto per il software richiesto non appena riceve la distribuzione ma non effettua l'esecuzione fino all'ora di distribuzione pianificata. All'ora pianificata, il client di Configuration Manager controlla se il contenuto è disponibile nella cache. Se il contenuto è disponibile nella cache e la versione è corretta, il client usa il contenuto nella cache. Quando la versione richiesta del contenuto viene modificata o se il contenuto viene eliminato dal client per liberare spazio per un altro pacchetto, il client scarica nuovamente il contenuto nella cache.  

Se il client tenta di scaricare il contenuto per un programma o un'applicazione di dimensioni superiori rispetto a quelle della cache, la distribuzione ha esito negativo perché le dimensioni della cache non sono sufficienti. Il client genera il messaggio di stato 10050 per dimensioni della cache non sufficienti. Se le dimensioni della cache vengono aumentate in un secondo momento, il risultato è il seguente:  

- Per un programma richiesto: il client non tenterà automaticamente di nuovo di scaricare il contenuto. Ridistribuire il programma e il pacchetto al client.  
- Per un'applicazione richiesta: il client proverà automaticamente a scaricare il contenuto al momento del download dei criteri client.  

Se il client tenta di scaricare un pacchetto di dimensioni inferiori rispetto a quelle della cache, ma la cache è piena, tutte le distribuzioni *richieste* eseguiranno altri tentativi fino a quando:

- Non sarà disponibile spazio nella cache
- Non si verificherà un timeout del download
- Non verrà raggiunto il numero massimo di tentativi

Se in seguito la dimensione della cache viene aumentata, il client tenterà di scaricare nuovamente il pacchetto al successivo intervallo tra tentativi. Il client tenterà di scaricare il contenuto ogni quattro ore per un massimo di 18 tentativi.  

Il contenuto memorizzato nella cache non viene eliminato automaticamente. Rimane nella cache per almeno un giorno dopo l'uso da parte del client. Se si configurano le proprietà del pacchetto con l'opzione per mantenere il contenuto nella cache del client, il client non lo elimina automaticamente. Se lo spazio nella cache viene usato da pacchetti scaricati nelle ultime 24 ore e il client deve scaricare nuovi pacchetti, aumentare le dimensioni della cache oppure scegliere l'opzione per eliminare il contenuto della cache persistente.  

Usare le seguenti procedure per configurare la cache client durante l'installazione client manuale oppure dopo l'installazione client.  

### <a name="configure-the-cache-during-manual-client-installation"></a>Configurare la cache durante l'installazione client manuale  

Eseguire il comando CCMSetup.exe dal percorso di origine di installazione e specificare le seguenti proprietà richieste e separate da spazi:  

- DISABLECACHEOPT  

  - SMSCACHEDIR  

  - SMSCACHEFLAGS  

  - SMSCACHESIZE  

    > [!NOTE]
    > Usare le impostazioni delle dimensioni della cache disponibili in **Impostazioni client** nella console di Configuration Manager anziché SMSCACHESIZE. Per altre informazioni vedere [Impostazioni della cache dei client](/configmgr/core/clients/deploy/about-client-settings#client-cache-settings).

Per altre informazioni sull'uso delle proprietà della riga di comando di CCMSetup.exe, vedere [Informazioni sulle proprietà di installazione del client](/configmgr/core/clients/deploy/about-client-installation-properties).

### <a name="configure-the-cache-during-client-push-installation"></a>Configurare la cache durante l'installazione push client  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**.  

2. Selezionare il sito appropriato. Nella scheda **Home** della barra multifunzione, nel gruppo **Impostazioni** selezionare **Impostazioni di installazione client** e scegliere **Installazione push client**. Passare alla scheda **Proprietà di installazione**.  

3. Specificare le seguenti proprietà, separate da spazi:  

   - DISABLECACHEOPT  

   - SMSCACHEDIR  

   - SMSCACHEFLAGS  

   - SMSCACHESIZE  

     > [!NOTE]
     > Usare le impostazioni delle dimensioni della cache disponibili in **Impostazioni client** nella console di Configuration Manager anziché SMSCACHESIZE. Per altre informazioni vedere [Impostazioni della cache dei client](/configmgr/core/clients/deploy/about-client-settings#client-cache-settings).

     Per altre informazioni sull'uso delle proprietà della riga di comando di CCMSetup.exe, vedere [Informazioni sulle proprietà di installazione del client](/configmgr/core/clients/deploy/about-client-installation-properties).  

### <a name="configure-the-cache-on-the-client-computer"></a>Configurare la cache nel computer client  

1. Nel computer client aprire il pannello di controllo di **Configuration Manager**.  

2. Passare alla scheda **Cache**. Impostare le proprietà per lo spazio e il percorso. Il percorso predefinito è `%windir%\ccmcache`.  

3. Per eliminare i file nella cartella della cache, scegliere **Elimina file**.  

### <a name="configure-client-cache-size-in-client-settings"></a>Configurare le dimensioni della cache del client in Impostazioni client

È possibile modificare le dimensioni della cache del client senza dover reinstallare il client. Usare le impostazioni delle dimensioni della cache disponibili in **Impostazioni client** nella console di Configuration Manager. Per altre informazioni vedere [Impostazioni della cache dei client](/configmgr/core/clients/deploy/about-client-settings#client-cache-settings).


## <a name="uninstall-the-client"></a><a name="BKMK_UninstalClient"></a> Disinstallare il client

È possibile disinstallare il software client di Configuration Manager da un computer usando **CCMSetup.exe** con la proprietà **/Uninstall**. Eseguire CCMSetup.exe in un singolo computer dal prompt dei comandi oppure distribuire un pacchetto per disinstallare il client da una raccolta di computer.  

> [!NOTE]  
> Non è possibile disinstallare il client di Configuration Manager da un dispositivo mobile. Se è necessario rimuovere il client di Configuration Manager da un dispositivo mobile, è necessario cancellare il dispositivo eliminando tutti i dati nel dispositivo mobile.  

1. Aprire un prompt dei comandi di Windows come amministratore. Passare alla cartella in cui si trova CCMSetup.exe, ad esempio: `cd %windir%\ccmsetup`

2. Eseguire il comando seguente: `CCMSetup.exe /uninstall`

> [!TIP]  
> I risultati del processo di disinstallazione non vengono visualizzati sullo schermo. Per verificare che il client venga disinstallato correttamente, vedere il file di log seguente: `%windir%\ccmsetup\logs\CCMSetup.log`  
>
> Se è necessario attendere il completamento del processo di disinstallazione prima di eseguire un'altra operazione, eseguire `Wait-Process CCMSetup` in PowerShell. Questo comando consente di sospendere uno script fino al completamento del processo CCMSetup.


## <a name="manage-conflicting-records"></a><a name="BKMK_ConflictingRecords"></a> Gestire i record in conflitto

Configuration Manager usa l'identificatore hardware per tentare di identificare i client che potrebbero essere dei duplicati e avvertire l'utente dei record in conflitto. Ad esempio, se si reinstalla un computer, l'identificatore hardware rimane lo stesso mentre il GUID usato da Configuration Manager potrebbe cambiare.  

Configuration Manager risolve automaticamente i conflitti usando l'autenticazione di Windows dell'account computer o un certificato PKI proveniente da un'origine attendibile. Quando Configuration Manager non riesce a risolvere il conflitto di identificatori hardware duplicati, il comportamento dipende da un'impostazione della gerarchia.

### <a name="change-the-hierarchy-setting-for-managing-conflicting-records"></a>Modificare l'impostazione della gerarchia per la gestione dei record in conflitto  

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**.

1. Sulla barra multifunzione selezionare **Impostazioni gerarchia**.

1. Passare alla scheda **Approvazione client e record in conflitto** e selezionare una delle opzioni seguenti:

    - **Risolvi automaticamente record in conflitto**
    - **Risolvi manualmente record in conflitto**

### <a name="manually-resolve-conflicting-records"></a>Risolvere manualmente i record in conflitto  

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere **Stato del sistema** e selezionare il nodo **Record in conflitto**.  

1. Selezionare uno o più record in conflitto e quindi scegliere **Record in conflitto**.  

1. Selezionare una delle opzioni seguenti:  

    - **Unisci**: per combinare il record appena rilevato con il record client esistente.  

    - **Nuovo**: per creare un nuovo record per il record client in conflitto.  

    - **Blocca**: per creare un nuovo record per il record client in conflitto, ma contrassegnandolo come bloccato.  


## <a name="manage-duplicate-hardware-identifiers"></a>Gestire gli identificatori di hardware duplicati

È possibile fornire un elenco di identificatori hardware che Configuration Manager ignora per l'avvio PXE e la registrazione client. Questo elenco consente di risolvere due problemi comuni:

1. Molti nuovi dispositivi non includono una porta Ethernet. I tecnici usano un adattatore da USB a Ethernet per stabilire una connessione cablata per la distribuzione del sistema operativo. Si tratta spesso di adattatori condivisi, per motivi di costi e usabilità generale. Il sito usa l'indirizzo MAC di questo adattatore per identificare il dispositivo. Il riutilizzo dell'adattatore diventa quindi problematico senza ulteriori interventi da parte dell'amministratore tra una distribuzione e l'altra. Per riusare l'adattatore in questo scenario, escluderne l'indirizzo MAC.

2. Mentre l'attributo SMBIOS è univoco, per alcuni dispositivi hardware specifici gli identificatori sono duplicati. Escludere l'identificatore duplicato e usare l'indirizzo MAC univoco di ogni dispositivo.

Usare questa procedura per aggiungere identificatori hardware che Configuration Manager deve ignorare:

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**.

2. Nella scheda **Home** della barra multifunzione scegliere **Impostazioni gerarchia** nel gruppo **Siti**.

3. Passare alla scheda **Approvazione client e record in conflitto**. Per aggiungere nuovi identificatori hardware, scegliere **Aggiungi** nella sezione **Identificatori hardware duplicati**.

> [!TIP]
> A partire dalla versione 1910, usare i cmdlet di PowerShell seguenti per automatizzare la gestione degli identificatori hardware duplicati:<!-- 4852819 -->
>
> - New-CMDuplicateHardwareIdGuid
> - Remove-CMDuplicateHardwareIdGuid
> - New-CMDuplicateHardwareIdMacAddress
> - Remove-CMDuplicateHardwareIdMacAddress


## <a name="start-policy-retrieval"></a><a name="BKMK_PolicyRetrieval"></a> Avviare il recupero dei criteri

Un client di Configuration Manager scarica i relativi criteri client in base a una pianificazione configurata come impostazione client. È anche possibile avviare il recupero dei criteri su richiesta dal client. Ad esempio, per la risoluzione dei problemi o esigenze di test.  

- [Notifica client](#bkmk_policy-notify)
- [Pannello di controllo del client](#bkmk_policy-manual)
- [Support Center](#bkmk_policy-support)
- [Uno script](#bkmk_policy-script)

### <a name="start-client-policy-retrieval-with-client-notification"></a><a name="bkmk_policy-notify"></a> Avviare il recupero dei criteri client con la notifica client  

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità** e selezionare **Dispositivi**.  

1. Selezionare il dispositivo per cui si vogliono scaricare i criteri. Nella scheda **Home** della barra multifunzione, nel gruppo **Dispositivo**, selezionare **Notifica client** e quindi scegliere **Scarica criteri computer**.  

    > [!NOTE]  
    > È anche possibile usare la notifica client per avviare il recupero dei criteri per tutti i dispositivi in una raccolta.  

### <a name="start-client-policy-retrieval-from-the-configuration-manager-client-control-panel"></a><a name="bkmk_policy-manual"></a> Avviare il recupero dei criteri client dal pannello di controllo del client di Configuration Manager

1. Aprire il pannello di controllo di **Configuration Manager** nel computer.  

2. Passare alla scheda **Azioni**. Selezionare **Ciclo di recupero e valutazione criteri computer** per avviare i criteri computer e quindi selezionare **Esegui**.  

3. Selezionare **OK** per confermare la richiesta.  

4. Ripetere i passaggi precedenti per tutte le altre azioni. Ad esempio, **Ciclo di recupero e valutazione criteri utente** per le impostazioni client degli utenti.  

### <a name="start-client-policy-retrieval-with-support-center"></a><a name="bkmk_policy-support"></a> Avviare il recupero dei criteri client con Supporto tecnico

Usare Supporto tecnico per richiedere e visualizzare i criteri client. Per altre informazioni, vedere [Informazioni di riferimento sull'interfaccia utente del Supporto tecnico](/configmgr/core/support/support-center-ui-reference#bkmk_support-policy).

### <a name="start-client-policy-retrieval-by-script"></a><a name="bkmk_policy-script"></a> Avviare il recupero dei criteri client tramite uno script  

1. Aprire un editor di script, ad esempio il Blocco note o Windows PowerShell ISE.  

2. Copiare e inserire il codice PowerShell di esempio seguente<!-- SCCMDocs#1591 --> nel file:  

    ```PowerShell
    $trigger = "{00000000-0000-0000-0000-000000000021}"
    Invoke-WmiMethod -Namespace root\ccm -Class sms_client -Name TriggerSchedule $trigger
    ```  

    > [!TIP]
    > Per altre informazioni sugli ID di pianificazione, vedere [ID messaggi](/configmgr/core/support/send-schedule-tool#bkmk_sendschedule-guids).

3. Salvare il file con un'estensione ps1.  

4. Eseguire lo script nel client.

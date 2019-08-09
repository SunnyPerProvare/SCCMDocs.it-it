---
title: Trasferimenti di dati
titleSuffix: Configuration Manager
description: Informazioni su come Configuration Manager sposta i dati tra i siti e come gestire il trasferimento dei dati in rete.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: cf2890f44bcb6e8e7813581de300e4544202f6ce
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/26/2019
ms.locfileid: "68536243"
---
# <a name="data-transfers-between-sites-in-configuration-manager"></a>Trasferimenti di dati tra siti in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Configuration Manager usa la *replica basata su file* e la *replica di database* per il trasferimento di tipi di informazioni diversi tra i siti. Informazioni su come Configuration Manager sposta i dati tra i siti e come gestire il trasferimento dei dati in rete.  


## <a name="bkmk_fileroute"></a> File-based replication

Configuration Manager usa la replica basata su file per trasferire i dati basati su file tra i siti all'interno della gerarchia. Questi dati includono le applicazioni e i pacchetti che si vuole distribuire ai punti di distribuzione nei siti figlio. Includono anche record dei dati di individuazione non elaborati che vengono trasferiti ai siti padre e quindi elaborati.  

La comunicazione tra siti basata su file usa il protocollo *Server Message Block** (SMB) sulla porta TCP/IP 445. Per controllare la quantità di dati trasferiti attraverso la rete, specificare la limitazione della larghezza di banda e la modalità a impulsi. È anche possibile usare le pianificazioni per controllare quando inviare i dati attraverso la rete.  

### <a name="bkmk_routes"></a> Route di replica file

Le informazioni seguenti possono essere utili per configurare e usare le route di replica file.  

#### <a name="file-replication-route"></a>Route di replica file

Ogni route di replica file identifica un sito di destinazione a cui è possibile trasferire dati basati su file. Ogni sito supporta una route di replica file a un sito di destinazione specifico.  

Per gestire una route di replica file, nell'area di lavoro **Amministrazione** espandere **Configurazione della gerarchia** e quindi selezionare **Replica file**.  

È possibile modificare le impostazioni seguenti per le route di replica file:  

##### <a name="file-replication-account"></a>Account replica file

Questo account si connette al sito di destinazione e scrive i dati nella condivisione **SMS_Site** di tale sito. Il sito ricevente elabora i dati scritti in questa condivisione. Per impostazione predefinita, quando si aggiunge un sito alla gerarchia Configuration Manager assegna l'account computer del server del sito per il nuovo sito come account di replica file per tale sito. Quindi aggiunge il nuovo account al gruppo **SMS_SiteToSiteConnection_&lt;Sitecode\>** del sito di destinazione. Questo gruppo è locale nel computer che concede l'accesso alla condivisione SMS_Site. È possibile modificare questo account in un account utente di Windows. Se si modifica l'account, verificare di aggiungerlo al gruppo **SMS_SiteToSiteConnection_&lt;Sitecode\>** del sito di destinazione.  

> [!NOTE]  
> I siti secondari usano sempre l'account computer del server del sito secondario come **Account replica file**.  

##### <a name="schedule"></a>Pianificazione

Per limitare il tipo di dati e il momento in cui i dati possono essere trasferiti al sito di destinazione, è possibile impostare la pianificazione per ogni route di replica file.

##### <a name="rate-limits"></a>Limiti di velocità

Per controllare la larghezza di banda di rete usata quando il sito trasferisce i dati al sito di destinazione è possibile specificare limiti di velocità per ogni route di replica file:

- **Modalità a impulsi**: Consente di specificare la dimensione dei blocchi di dati che il sito invia al sito di destinazione. È anche possibile specificare un ritardo tra l'invio di ogni blocco di dati. Usare questa opzione quando è necessario inviare i dati al sito di destinazione tramite una connessione di rete a larghezza di banda ridotta.

    Ad esempio è possibile che si sia vincolati a inviare 1 kB di dati ogni cinque secondi, ma non 1 kB ogni tre secondi, indipendentemente dalla velocità del collegamento o dall'uso del collegamento in un momento dato.

- **Limitato alle velocità di trasferimento massime specificate per ora**: Il sito invia i dati a un sito di destinazione usando solo la percentuale di tempo specificata. Quando si usa questa opzione, Configuration Manager non identifica la larghezza di banda disponibile della rete, ma divide in intervalli il periodo di tempo in cui può inviare i dati. I dati vengono quindi inviati in un intervallo di tempo breve, seguito da intervalli di tempo in cui non vengono inviati dati.

    Ad esempio è possibile impostare la velocità massima su **50%** . Configuration Manager trasmette i dati per un periodo di tempo, seguito da un periodo di tempo uguale in cui non viene inviato alcun dato. Non vengono gestite la quantità effettiva di dati o le dimensioni del blocco di dati, ma solo la quantità di tempo durante il quale avviene l'invio dei dati.  

    > [!CAUTION]  
    > Per impostazione predefinita, un sito può usare fino a tre **invii simultanei** per trasferire i dati a un sito di destinazione. Quando si abilitano i limiti di velocità per una route di replica file, gli **invii simultanei** per l'invio dei dati a tale sito sono limitati a uno. Questo comportamento si applica anche quando l'opzione **Limita larghezza di banda disponibile (%)** è impostata su **100%** . Se ad esempio si usano le impostazioni predefinite per il mittente, la velocità di trasferimento al sito di destinazione viene ridotta a un terzo della capacità predefinita.  

##### <a name="secondary-sites"></a>Siti secondari

È possibile configurare una route di replica file tra due siti secondari per distribuire contenuto basato su file fra tali siti.  


#### <a name="sender"></a>Mittente

Ogni sito dispone di un mittente. Il mittente gestisce la connessione di rete da un sito a un sito di destinazione e può stabilire connessioni simultanee con più siti. Per connettersi a un sito, il mittente usa la route di replica file al sito per identificare l'account da usare al fine di stabilire la connessione di rete. Il mittente usa questo account anche per scrivere i dati nella condivisione SMS_Site del sito di destinazione.  

Per impostazione predefinita, il mittente scrive i dati in un sito di destinazione usando più **invii simultanei**, in genere indicati come thread. Ogni invio simultaneo, o thread, è in grado di trasferire un oggetto basato su file differente al sito di destinazione. Per impostazione predefinita, una volta avviato l'invio di un oggetto, il mittente continua a scrivere blocchi di dati relativi a tale oggetto fino al suo completo invio. Dopo l'invio di tutti i dati relativi all'oggetto, sarà possibile iniziare l'invio di un nuovo oggetto su tale thread.  

Per gestire il mittente per un sito, passare all'area di lavoro **Amministrazione** ed espandere il nodo **Configurazione del sito**. Selezionare il nodo **Siti**, quindi selezionare **Proprietà** per il sito che si vuole gestire. Passare alla scheda **Mittente** per modificare le impostazioni del mittente.  

È possibile modificare le impostazioni seguenti per un mittente:  

##### <a name="maximum-concurrent-sendings"></a>Numero massimo di invii simultanei

Per impostazione predefinita ogni sito usa cinque invii simultanei. Quando invia dati a un sito di destinazione, il sito dispone di tre thread. Aumentando tale numero è possibile incrementare la velocità effettiva dei dati tra siti, consentendo a Configuration Manager di trasferire più file simultaneamente. L'incremento di questo numero determina anche un aumento della richiesta di larghezza di banda della rete tra siti.  

##### <a name="retry-settings"></a>Impostazioni tentativi

Per impostazione predefinita, ogni sito ritenta la connessione due volte, con un intervallo di un minuto tra un tentativo e l'altro, in caso di connessione non riuscita. È possibile modificare il numero di tentativi di connessione e il relativo intervallo di attesa.  


## <a name="bkmk_dbrep"></a> Database replication

La replica di database di Configuration Manager usa SQL Server per trasferire i dati e unire le modifiche apportate in un database del sito alle informazioni archiviate nel database in altri siti della gerarchia.

In una gerarchia:

- Tutti i siti condividono le stesse informazioni.  
- Quando si installa un sito in una gerarchia, Configuration Manager definisce automaticamente la replica di database tra il nuovo sito e il sito padre.  
- Al termine dell'installazione del sito, la replica di database viene avviata automaticamente.  

Quando si aggiunge un nuovo sito a una gerarchia, Configuration Manager crea un database generico nel nuovo sito. Successivamente, il sito padre crea uno snapshot dei dati rilevanti nel relativo database e lo trasferisce nel nuovo sito tramite replica basata su file. Il nuovo sito usa poi un programma per la copia bulk di SQL Server (BCP) per caricare le informazioni nella copia locale del database di Configuration Manager. Dopo il caricamento dello snapshot, ogni sito esegue la replica di database con l'altro sito.  

Per replicare i dati tra siti, Configuration Manager usa il proprio servizio di replica database. Il servizio di replica di database usa il rilevamento modifiche di SQL Server per monitorare le modifiche al database del sito locale. Quindi replica le modifiche agli altri siti usando SQL Server Service Broker (SSB). Per impostazione predefinita, questo processo usa la porta TCP/IP 4022.  

### <a name="replication-groups"></a>Gruppi di replica

Configuration Manager riunisce i dati replicati con replica di database in gruppi di replica diversi. Ogni gruppo di replica dispone di una pianificazione di replica fissa separata. Il sito usa questa pianificazione per determinare la frequenza con cui replica le modifiche agli altri siti.  

Ad esempio una modifica alla configurazione dell'amministrazione basata su ruoli viene rapidamente replicata ad altri siti. Questo comportamento assicura che altri siti possano applicare rapidamente queste modifiche. Una modifica della configurazione con priorità più bassa, ad esempio una richiesta di installazione di un nuovo sito secondario, viene invece replicata con minore urgenza. La richiesta di un nuovo sito può infatti impiegare alcuni minuti prima che raggiunga il sito primario di destinazione.  

### <a name="settings-for-database-replication"></a>Impostazioni per la replica di database

Per la replica di database, è possibile modificare le impostazioni seguenti:  

- **Collegamenti di replica di database**: Consentono di controllare quando la rete viene attraversata da traffico specifico.  

- **Viste distribuite**: Quando un sito di amministrazione centrale (CAS, Central Administration Site) richiede dati del sito selezionati, può accedere ai dati stessi direttamente dal database in un sito primario figlio.  

- **Pianificazioni**: Consentono di specificare quando viene usato un collegamento di replica e quando vengono replicati diversi tipi di dati del sito.  

- **Riepilogo**: Impostazioni per il riepilogo di dati sul traffico di rete che attraversa i collegamenti di replica. Per impostazione predefinita, il riepilogo avviene ogni 15 minuti. Viene usato nei report per la replica del database.  

- **Soglie di replica del database**: Consentono di definire quando Configuration Manager segnala i collegamenti come danneggiati o non riusciti. È anche possibile configurare quando Configuration Manager genera avvisi sui collegamenti di replica con stato danneggiato o non riuscito.  

### <a name="types-of-data"></a>Tipi di dati

Configuration Manager classifica i dati che replica come *dati globali* o come *dati del sito*. Quando si verifica la replica di database, il sito trasferisce le modifiche ai dati globali e ai dati del sito attraverso il collegamento di replica di database. I dati globali vengono replicati a un sito padre o a un sito figlio. I dati del sito vengono replicati solo a un sito padre. Esiste un terzo tipo di dati, i *dati locali*, che non viene replicato ad altri siti. I dati locali sono informazioni non richieste da altri siti.

#### <a name="global-data"></a>Dati globali

I dati globali sono oggetti creati dall'amministratore e replicati in tutti i siti in tutta la gerarchia. I siti secondari ricevono solo un subset di dati globali, come dati proxy globali. I dati globali vengono creati nel sito CAS e nei siti primari. Includono i dati seguenti:

- Distribuzioni software
- Aggiornamenti software
- Definizioni di raccolta
- Ambiti di protezione dell'amministrazione basata su ruoli

#### <a name="site-data"></a>Dati del sito

I dati del sito sono informazioni operative create dai siti primari di Configuration Manager e dai rispettivi client assegnati. I dati del sito vengono replicati nel sito di amministrazione centrale, ma non in altri siti primari. I dati del sito possono essere visualizzati solo nel sito di amministrazione centrale e nel sito primario da cui hanno origine. È possibile modificare i dati del sito solo nel sito primario in cui sono stati creati. Includono i dati seguenti:

- Inventario hardware
- Messaggi di stato
- Avvisi
- Risultati di raccolte basate su query

Tutti i dati del sito vengono replicati nel sito di amministrazione centrale. Il sito CAS esegue l'amministrazione e la creazione di report per l'intera gerarchia.  

### <a name="bkmk_Dblinks"></a> Collegamenti di replica di database

Quando si installa un nuovo sito in una gerarchia, Configuration Manager crea automaticamente un collegamento di replica di database tra il sito padre e il nuovo sito. Crea un unico collegamento per collegare i due siti.  

Per controllare il trasferimento dei dati tramite il collegamento della replica di database, modificare le impostazioni di ogni collegamento. Ogni collegamento di replica supporta configurazioni separate. Ogni collegamento della replica di database include i controlli seguenti:  

- Arresto della replica di dati del sito selezionati da un sito primario al sito CAS. Il sito CAS può quindi accedere a questi dati direttamente dal database del sito primario.  
- Pianificazione dei dati del sito selezionati per il trasferimento da un sito primario figlio al sito CAS.
- Definizione delle impostazioni che determinano quando un collegamento di replica di database è danneggiato o non è riuscito.
- La possibilità di specificare in quali casi generare avvisi per un collegamento di replica non riuscito.
- Specificare la frequenza con cui Configuration Manager riepiloga i dati sul traffico di replica che usa il collegamento di replica. Questi dati vengono usati nei report.

Per configurare un collegamento di replica di database, nel nodo **Replica di database** della console di Configuration Manager aprire **Proprietà** per il collegamento. Questo nodo viene visualizzato sia nell'area di lavoro **Monitoraggio** sia nel nodo **Configurazione della gerarchia** nell'area di lavoro **Amministrazione**. È possibile modificare un collegamento di replica dal relativo sito padre o dal sito figlio.

> [!TIP]  
> È possibile modificare i collegamenti di replica di database dal nodo **Replica di database** in qualsiasi area di lavoro. Tuttavia quando si usa il nodo **Replica di database** nell'area di lavoro **Monitoraggio** è possibile visualizzare anche lo stato della replica di database. Il nodo consente anche di accedere allo strumento [Replication Link Analyzer](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA). Usare questo strumento per analizzare i problemi relativi alla replica di database.  

Per altre informazioni su come configurare i collegamenti di replica, vedere [Controlli di replica di database del sito](#BKMK_DBRepControls). Per altre informazioni sul monitoraggio della replica, vedere [Come monitorare lo stato e i collegamenti di replica del database](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_MonitorRepLinksAndStatuss).

### <a name="bkmk_distviews"></a> Viste distribuite

Tramite le viste distribuite, quando si esegue una richiesta di dati del sito selezionati al sito CAS si accede direttamente al database nel sito primario figlio. L'accesso diretto elimina la necessità di replicare questi dati dal sito primario al sito CAS. Poiché ogni collegamento di replica è indipendente dagli altri, è possibile usare le viste distribuite solo nei collegamenti di replica selezionati. Non è possibile usare viste distribuite tra un sito primario e un sito secondario.  

Le viste distribuite offrono i seguenti vantaggi:  

- Ridurre il carico CPU per l'elaborazione le modifiche del database nel sito di amministrazione centrale (CAS) e nei siti primari
- Ridurre la quantità di dati trasferiti attraverso la rete al sito CAS
- Migliorare le prestazioni dell'istanza di SQL Server che ospita il database CAS
- Ridurre lo spazio su disco usato dal database CAS

È consigliabile usare le viste distribuite quando un sito primario si trova vicino al sito CAS sulla rete e i due siti sono sempre attivi e sempre connessi. Le viste distribuite sostituiscono la replica dei dati selezionati tra i siti con connessioni dirette tra i server SQL in ogni sito. Il CAS esegue una connessione diretta ogni volta che vengono richiesti questi dati.

Il sito richiede i dati della vista distribuiti negli scenari di esempio seguenti:

- Quando si eseguono report o query
- Quando si visualizzano informazioni in Esplora inventario risorse
- Valutazione della raccolta per le raccolte che includono regole basate sui dati del sito

Per impostazione predefinita, le viste distribuite sono disabilitate per ogni collegamento di replica. Quando si attivano le viste distribuite si selezionano i dati del sito che non verranno replicati nel CAS su tale collegamento. Il sito CAS accede a questi dati direttamente dal database del sito primario figlio che condivide il collegamento. È possibile configurare i seguenti tipi di dati del sito per le viste distribuite:  

- **Dati di inventario hardware** dei client
- **Dati di controllo e inventario software** dei client
- **Messaggi di stato** dei client, del sito primario e di tutti i siti secondari

Quando si visualizzano i dati nella console di Configuration Manager o nei report, le viste distribuite non sono visibili a livello operativo. Quando si richiedono dati abilitati per le viste distribuite, il server di database del sito CAS accede direttamente al database del sito primario figlio per recuperare le informazioni.

Ad esempio si usa una console di Configuration Manager nel sito CAS per richiedere informazioni di inventario hardware dal sito primario ABC e dal sito primario XYZ. Si abilita l'inventario hardware per una vista distribuita nel sito ABC. Il sito recupera le informazioni di inventario client XYZ dal database CAS. Il sito recupera le informazioni di inventario client ABC dal database del sito ABC. Queste informazioni vengono visualizzate nella console di Configuration Manager o in un report senza identificazione dell'origine.  

Finché il tipo di dati di un collegamento di replica è abilitato per le viste distribuite, il sito primario figlio non replica i dati al sito CAS. Quando si disattivano le viste distribuite per un tipo di dati, il sito primario figlio riprende la replica dei dati al sito CAS come parte della normale replica di dati. Prima che questi dati diventino disponibili nel sito CAS, i gruppi di replica che li contengono devono essere reinizializzati tra il sito primario e il sito CAS. In modo analogo, dopo la disinstallazione di un sito primario in cui sono attivate le viste distribuite, prima di poter accedere a tali dati nel sito CAS è necessario che il sito completi la reinizializzazione dei propri dati.  

> [!IMPORTANT]  
> Quando si usano le viste distribuite in un qualsiasi collegamento di replica nella gerarchia del sito, disabilitare le viste distribuite per tutti i collegamenti di replica prima di disinstallare un sito primario. Per ulteriori informazioni, vedere [Disinstallare un sito primario configurato con viste distribuite](/sccm/core/servers/deploy/install/uninstall-sites-and-hierarchies#BKMK_UninstallPrimaryDistViews).  

#### <a name="prerequisites-and-limitations-for-distributed-views"></a>Prerequisiti e limitazioni per le viste distribuite  

- È possibile usare le viste distribuite solo nei collegamenti di replica tra un sito CAS e un sito primario.

- Il sito CAS deve usare un'edizione *Enterprise* di SQL Server. Il sito primario non presenta questo requisito.

- Nel sito CAS può essere installata una sola istanza del provider SMS. Installare tale istanza nel server di database del sito. Questo requisito supporta l'autenticazione Kerberos. Il server SQL nel sito CAS richiede che Kerberos acceda al server SQL nel sito primario figlio. Non esistono limitazioni nel provider SMS nel sito primario figlio.

- Il sito CAS può avere una sola istanza di SQL Server Reporting Services. Installare il punto di Reporting Services nel server di database del sito. Questo requisito supporta l'autenticazione Kerberos. Il server SQL nel sito CAS richiede che Kerberos acceda al server SQL nel sito primario figlio.

- Non è possibile ospitare il database del sito in un [cluster di SQL Server](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database).

- Nella versione 1902 e versioni precedenti non è possibile ospitare il database del sito in un [gruppo di disponibilità SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database). Per supportare questa configurazione, eseguire l'aggiornamento alla versione 1906 o a versioni successive.<!-- SCCMDocs-pr#3792 -->

- L'account computer del server di database CAS richiede autorizzazioni di **lettura** per il database del sito primario.

> [!IMPORTANT]  
> Le viste distribuite e le [pianificazioni](#BKMK_schedules) del momento in cui poter replicare i dati sono configurazioni per un collegamento di replica del database che si escludono a vicenda.  

### <a name="BKMK_schedules"></a> Pianificare trasferimenti dei dati del sito in collegamenti di replica di database

Per facilitare il controllo della larghezza di banda di rete usata per replicare i dati del sito da un sito primario figlio al sito CAS corrispondente, pianificare quando viene usato un collegamento di replica. È anche possibile specificare quando vengono replicati i diversi tipi di dati del sito. È possibile controllare quando il sito primario replica i messaggi di stato, l'inventario e i dati di controllo. I collegamenti di replica del database dei siti secondari non supportano le pianificazioni per i dati del sito. Non è possibile pianificare il trasferimento di dati globali.  

Quando si configura una pianificazione del collegamento di replica del database, è possibile limitare il trasferimento dei dati del sito selezionati dal sito primario al sito CAS. È anche possibile configurare orari diversi per replicare tipi diversi di dati del sito.  

> [!IMPORTANT]  
> Le [viste distribuite](#bkmk_distviews) e le pianificazioni per quando possono essere replicati i dati sono configurazioni che si escludono a vicenda per un collegamento di replica del database.  

### <a name="BKMK_SummarizeDBReplication"></a> Riepilogo del traffico di replica di database

Ogni sito riepiloga periodicamente i dati sul traffico di rete che attraversa i collegamenti di replica di database del sito. Il sito usa i dati riepilogati nei report per la replica di database. Entrambi i siti su un collegamento di replica riepilogano il traffico di rete che attraversa il collegamento di replica. Il server di database del sito riepiloga i dati. Dopo il riepilogo dei dati, queste informazioni vengono replicate in altri siti come dati globali.  

Per impostazione predefinita, il riepilogo avviene ogni 15 minuti. Per modificare la frequenza di riepilogo per il traffico di rete, modificare **Intervallo riepilogo** nelle proprietà del collegamento di replica del database. La frequenza di riepilogo riguarda le informazioni visualizzate nei report sulla replica di database. È possibile scegliere un intervallo compreso tra 5 e 60 minuti. Più alta è la frequenza di riepilogo, maggiore sarà il carico di elaborazione sul server SQL in ogni sito sul collegamento di replica.  

### <a name="BKMK_DBRepThresholds"></a> Soglie di replica del database

Le soglie di replica del database definiscono quando il sito restituisce uno stato di un collegamento di replica del database ridotto o non riuscito. Per impostazione predefinita, un collegamento assume lo stato *ridotto* quando un gruppo di replica non completa la replica dopo 12 tentativi consecutivi. Il collegamento assume lo stato *non riuscito* quando un gruppo di replica non esegue la replica dopo 24 tentativi consecutivi.  

È possibile specificare valori personalizzati per lo stato ridotto o non riuscito. Se si modificano questi valori, è possibile monitorare con maggior precisione l'integrità della replica di database tra i collegamenti.  

È possibile che uno o più gruppi di replica non siano in grado di eseguire la replica, mentre altri gruppi di replica continuano a replicare correttamente. Pianificare la verifica dello stato della replica di un collegamento quando questo segnala per la prima volta uno stato ridotto. Se sono presenti ritardi ricorrenti per specifici gruppi di replica ma il ritardo non rappresenta un problema oppure il collegamento di replica tra siti ha una larghezza di banda disponibile ridotta, è possibile modificare i valori dei tentativi per lo stato ridotto o non riuscito del collegamento. Aumentando il numero di tentativi prima che il collegamento sia impostato su danneggiato o non riuscito, è possibile eliminare gli avvisi non necessari per problemi noti e tenere traccia con più precisione dello stato del collegamento.  

È necessario considerare anche l'intervallo di sincronizzazione per ogni gruppo di replica, per determinare la frequenza con cui viene eseguita la replica di tale gruppo. Per visualizzare **Intervallo di sincronizzazione** per i gruppi di replica, nel nodo **Replica di database** dell'area di lavoro **Monitoraggio** selezionare la scheda **Dettaglio di replica**.  

Per altre informazioni sul monitoraggio della replica del database e su come visualizzare lo stato della replica, vedere [Come monitorare lo stato e i collegamenti di replica del database](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_MonitorRepLinksAndStatuss).  

Per altre informazioni sulla configurazione delle soglie di replica di database, vedere [Controlli di replica di database del sito](#BKMK_DBRepControls).  


## <a name="BKMK_DBRepControls"></a> Controlli di replica di database del sito

Per controllare la larghezza di banda di rete usata per la replica di database, modificare le impostazioni per ogni database del sito. Le impostazioni si applicano solo al database del sito in cui vengono configurate. Il sito usa sempre queste impostazioni per replicare i dati a un altro sito tramite replica di database.  

È possibile modificare i controlli di replica seguenti per ogni database del sito:  

- Porta SSB
- Tempo di attesa prima che venga reinizializzata la copia del database del sito a seguito di tentativi di replica non riusciti
- Comprimere i dati di replica dalla replica del database. I dati sono compressi solo per il trasferimento tra siti e non per l'archiviazione nel database del sito su ogni sito.  

Per modificare le impostazioni dei controlli di replica per un database del sito, modificare le proprietà del database del sito nella console di Configuration Manager dal nodo **Replica di database**. È possibile visualizzare questo nodo sotto il nodo **Configurazione della gerarchia** nell'area di lavoro **Amministrazione** e anche in **Area di lavoro di monitoraggio**. Per modificare le proprietà del database del sito, selezionare il collegamento di replica tra i siti e aprire **Proprietà database principale** oppure **Proprietà database secondario**.  

> [!TIP]  
> È possibile configurare i controlli di replica del database dal nodo **Replica di database** in qualsiasi area di lavoro. Tuttavia quando si usa il nodo **Replica di database** nell'area di lavoro **Monitoraggio** è possibile visualizzare anche lo stato della replica di database. Il nodo consente anche di accedere allo strumento [Replication Link Analyzer](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA). Usare questo strumento per analizzare i problemi relativi alla replica di database.  

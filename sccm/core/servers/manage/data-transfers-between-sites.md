---
title: Trasferimenti di dati
titleSuffix: Configuration Manager
description: Informazioni su come Configuration Manager sposta i dati tra i siti e come gestire il trasferimento dei dati in rete.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 39ae7c931b2d69199dc2c24cbb1bf9ae804a04b4
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123189"
---
# <a name="data-transfers-between-sites-in-system-center-configuration-manager"></a>Trasferimenti di dati tra siti in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager usa la **replica basata su file** e la **replica di database** per il trasferimento di diversi tipi di informazioni tra siti. Informazioni su come Configuration Manager sposta i dati tra i siti e come gestire il trasferimento dei dati in rete.  


## <a name="bkmk_fileroute"></a> File-based replication  
Configuration Manager usa la replica basata su file per trasferire i dati basati su file tra i siti all'interno della gerarchia. Tali dati includono le applicazioni e i pacchetti che si vogliono distribuire su punti di distribuzione nei siti figlio, oltre ai record dei dati di individuazione non elaborati che vengono trasferiti ai siti padre per poi essere elaborati.  

La comunicazione tra siti basata su file usa il protocollo **Server Message Block** (SMB) sulla porta TCP/IP 445. È possibile specificare la limitazione della larghezza di banda e la modalità a impulsi per controllare la quantità di dati trasferiti in rete. È anche possibile usare pianificazioni per controllare quando inviare i dati in rete.  

### <a name="bkmk_routes"></a> Route di replica file  
Le informazioni seguenti possono essere utili per configurare e usare le route di replica file.  

#### <a name="file-replication-route"></a>Route di replica file

Ogni route di replica file identifica un sito di destinazione a cui è possibile trasferire dati basati su file. Ogni sito supporta una route di replica file a un sito di destinazione specifico.  

È possibile modificare le impostazioni seguenti per le route di replica file:  

-  **Account replica file**. Questo account si connette al sito di destinazione e scrive i dati nella condivisione **SMS_Site** di tale sito. I dati scritti in questa condivisione vengono elaborati dal sito ricevente. Per impostazione predefinita, quando un sito viene aggiunto alla gerarchia, Configuration Manager assegna l'account computer del server del sito dei nuovi siti come Account replica file di tali siti. Questo account viene poi aggiunto al gruppo **SMS_SiteToSiteConnection_&lt;CodiceSito\>** del sito di destinazione, ovvero un gruppo locale nel computer che consente l'accesso alla condivisione SMS_Site. È possibile modificare questo account in un account utente di Windows. Se si modifica l'account, verificare che il nuovo account venga aggiunto al gruppo **SMS_SiteToSiteConnection_&lt;CodiceSito\>** del sito di destinazione.  

    > [!NOTE]  
    >  I siti secondari usano sempre l'account computer del server del sito secondario come **Account replica file**.  

-  **Pianificazione**. È possibile impostare la pianificazione per ogni route di replica file in modo da limitare il tipo di dati e il momento in cui i dati possono essere trasferiti al sito di destinazione.  
-  **Limiti di velocità**. È possibile specificare limiti di velocità per ogni route di replica file in modo da controllare la larghezza di banda di rete usata quando il sito trasferisce i dati al sito di destinazione:  

    -  Usare **Modalità a impulsi** per specificare la dimensione dei blocchi di dati inviati al sito di destinazione. È anche possibile specificare un ritardo tra l'invio di ogni blocco di dati. Usare questa opzione quando è necessario inviare i dati al sito di destinazione tramite una connessione di rete a larghezza di banda ridotta. È possibile, ad esempio, che si sia vincolati a inviare 1 KB di dati ogni cinque secondi, ma non 1 KB ogni tre secondi, indipendentemente dalla velocità del collegamento o dall'utilizzo in un determinato momento.
    -  Usare **Limitato alle velocità di trasferimento massime specificate per ora** per fare in modo che un sito invii i dati a un sito di destinazione usando solo la percentuale di tempo specificata. Quando si usa questa opzione, Configuration Manager non identifica la larghezza di banda disponibile per la rete, ma divide in intervalli il periodo di tempo in cui può inviare i dati. I dati vengono quindi inviati in un breve intervallo di tempo, seguito da periodi di tempo in cui i dati non vengono inviati. Se ad esempio la velocità massima è impostata su **50%**, Configuration Manager trasmette i dati per un periodo di tempo seguito da un uguale periodo di tempo in cui non viene inviato alcun dato. La quantità effettiva di dati, o le dimensioni del blocco di dati, non è gestita. Viene invece gestita solo la quantità di tempo durante il quale i dati vengono inviati.  

        > [!CAUTION]  
        > Per impostazione predefinita, un sito può usare fino a tre **invii simultanei** per trasferire i dati a un sito di destinazione. Quando si abilitano i limiti di velocità per una route di replica file, gli **invii simultanei** per l'invio dei dati a tale sito sono limitati a uno. Questa impostazione si applica anche quando l'opzione **Limita larghezza di banda disponibile (%)** è impostata su **100%**. Se ad esempio si usano le impostazioni predefinite per il mittente, la velocità di trasferimento al sito di destinazione viene ridotta a un terzo della capacità predefinita.  

-  È possibile configurare una route di replica file tra due siti secondari per distribuire contenuto basato su file fra tali siti.  

Per gestire una route di replica file, espandere il nodo **Configurazione della gerarchia** nell'area di lavoro **Amministrazione** e selezionare **Replica file**.  

#### <a name="sender"></a>Mittente

Ogni sito dispone di un mittente. Il mittente gestisce la connessione di rete da un sito a un sito di destinazione e può stabilire connessioni simultanee con più siti. Per connettersi a un sito, il mittente usa la route di replica file al sito per identificare l'account da usare al fine di stabilire la connessione di rete. Il mittente usa questo account anche per scrivere i dati nella condivisione SMS_Site del sito di destinazione.  

Per impostazione predefinita, il mittente scrive i dati in un sito di destinazione usando più **invii simultanei**, in genere indicati come thread. Ogni invio simultaneo, o thread, è in grado di trasferire un oggetto basato su file differente al sito di destinazione. Per impostazione predefinita, una volta avviato l'invio di un oggetto, il mittente continua a scrivere blocchi di dati relativi a tale oggetto fino al suo completo invio. Dopo l'invio di tutti i dati relativi all'oggetto, sarà possibile iniziare l'invio di un nuovo oggetto su tale thread.  

È possibile modificare le impostazioni seguenti per un mittente:  

-  **Numero massimo di invii simultanei**. Per impostazione predefinita, ogni sito usa cinque invii simultanei, tre dei quali sono disponibili in caso di invio dei dati a un sito di destinazione. Aumentando tale numero è possibile incrementare la velocità effettiva dei dati tra siti, consentendo a Configuration Manager di trasferire più file simultaneamente. L'incremento di questo numero determina anche un aumento della richiesta di larghezza di banda della rete tra siti.  

-  **Impostazioni tentativi**. Per impostazione predefinita, ogni sito ritenta la connessione due volte, con un intervallo di un minuto tra un tentativo e l'altro, in caso di connessione non riuscita. È possibile modificare il numero di tentativi di connessione e il relativo intervallo di attesa.  

Per gestire il mittente per un sito, espandere il nodo **Configurazione del sito** nell'area di lavoro **Amministrazione**, selezionare il nodo **Siti**e fare clic su **Proprietà** per il sito che si vuole gestire. Selezionare la scheda **Mittente** per modificare le impostazioni del mittente.  

## <a name="bkmk_dbrep"></a> Database replication  
La replica di database di Configuration Manager usa SQL Server per trasferire i dati e unire le modifiche apportate in un database del sito alle informazioni archiviate nel database in altri siti della gerarchia. Considerare le informazioni seguenti sulla replica di database:

-  Tutti i siti condividono le stesse informazioni.  
-  Quando si installa un sito in una gerarchia, la replica di database viene configurata automaticamente tra il nuovo sito e il sito padre designato.  
-  Al termine dell'installazione del sito, la replica di database viene avviata automaticamente.  

Quando si aggiunge un nuovo sito a una gerarchia, Configuration Manager crea un database generico nel nuovo sito. Successivamente, il sito padre crea uno snapshot dei dati rilevanti nel relativo database e lo trasferisce nel nuovo sito tramite replica basata su file. Il nuovo sito usa poi un programma per la copia bulk di SQL Server (BCP) per caricare le informazioni nella copia locale del database di Configuration Manager. Dopo il caricamento dello snapshot, ogni sito esegue la replica di database con l'altro sito.  

Per replicare i dati tra siti, Configuration Manager usa il proprio servizio di replica database. Il servizio di replica di database usa il rilevamento modifiche di SQL Server per monitorare eventuali modifiche nel database del sito locale e replica le modifiche in altri siti usando SQL Server Service Broker (SSB). Per impostazione predefinita, questo processo usa la porta TCP/IP 4022.  

Configuration Manager riunisce i dati replicati con replica di database in gruppi di replica diversi. Considerare le informazioni seguenti sui gruppi di replica:

-  Ciascun gruppo di replica dispone di una pianificazione di replica fissa, separata, che determina la frequenza di replica delle modifiche apportate ai dati del gruppo su altri siti.  

     Ad esempio, una modifica alla configurazione dell'amministrazione basata su ruoli viene rapidamente replicata ad altri siti per garantire che tali modifiche vengano applicate il prima possibile. Una modifica della configurazione con priorità più bassa, ad esempio una richiesta di installazione di uno nuovo sito secondario, viene invece replicata con minore urgenza. La richiesta di un nuovo sito può infatti impiegare alcuni minuti prima che raggiunga il sito primario di destinazione.  

-   Per la replica di database, è possibile modificare le impostazioni seguenti:  

    -  **Collegamenti di replica di database**. Consentono di controllare quando la rete viene attraversata da traffico specifico.  
    -  **Viste distribuite**. Consentono di modificare le impostazioni per i collegamenti di replica, con i quali le richieste effettuate in un sito di amministrazione centrale per i dati del sito selezionati possono accedere a tali dati direttamente dal database in un sito primario figlio.  
    -  **Pianificazioni**. Consentono di specificare quando viene usato un collegamento di replica e quando vengono replicati diversi tipi di dati del sito.  
    -  **Riepilogo**. Consente di modificare le impostazioni per il riepilogo di dati sul traffico di rete che attraversa i collegamenti di replica. Il riepilogo viene eseguito per impostazione predefinita ogni 15 minuti e viene usato nei report per la replica di database.  
    -  **Soglie di replica del database**. Consentono di definire quando segnalare un collegamento danneggiato o non riuscito. È anche possibile configurare quando Configuration Manager genera avvisi sui collegamenti di replica con stato danneggiato o non riuscito.  

Configuration Manager classifica i dati replicati con la replica di database come **dati globali** o **dati del sito**. Quando si verifica la replica di database, le modifiche ai dati globali e ai dati del sito vengono trasferite attraverso il collegamento di replica di database. I dati globali possono essere replicati a un sito padre o a un sito figlio. I dati del sito vengono replicati solo a un sito padre. Esiste un terzo tipo di dati, vale a dire i dati locali, che non viene replicato ad altri siti. I dati locali sono informazioni non richieste da altri siti. Considerare le informazioni seguenti sui tipi di dati:  

-  **Dati globali**. i dati globali fanno riferimento a oggetti creati dall'amministratore che vengono replicati su tutti i siti in tutta la gerarchia, sebbene i siti secondari ricevano solo un sottoinsieme di dati globali, come dati proxy globali. I dati globali includono distribuzioni e aggiornamenti software, definizioni di raccolte e ambiti di protezione di amministrazione basata sui ruoli. Gli amministratori possono creare dati globali in siti di amministrazione centrale e siti primari.  
-  **Dati del sito**. I dati del sito fanno riferimento a informazioni operative create dai siti primari di Configuration Manager e dai client connessi ai siti primari. I dati del sito vengono replicati nel sito di amministrazione centrale, ma non in altri siti primari. I dati del sito includono dati di inventario hardware, messaggi di stato, avvisi e i risultati delle raccolte basate su query. I dati del sito possono essere visualizzati solo nel sito di amministrazione centrale e nel sito primario da cui hanno origine. Possono essere modificati solo nel sito primario in cui sono stati creati.  

     Tutti i dati del sito vengono replicati al sito di amministrazione centrale. Il sito di amministrazione centrale si occupa dell'amministrazione e della creazione di report per l'intera gerarchia del sito.  

Le sezioni seguenti descrivono nel dettaglio le impostazioni che è possibile modificare per gestire la replica di database.  

### <a name="bkmk_Dblinks"></a> Collegamenti di replica di database  
Quando si installa un nuovo sito in una gerarchia, Configuration Manager crea automaticamente un collegamento di replica di database tra il sito padre e il nuovo sito. Per collegare i due siti, viene creato un solo collegamento.  

È possibile modificare le impostazioni di ogni collegamento di replica di database per controllare il trasferimento dei dati tramite tale collegamento. Ogni collegamento di replica supporta configurazioni separate. I controlli per i collegamenti di replica di database includono:  

-  La possibilità di arrestare la replica dei dati del sito selezionati da un sito primario al sito di amministrazione centrale. Il sito di amministrazione centrale può così accedere direttamente a questi dati dal database del sito primario.  
-  La possibilità di pianificare il trasferimento dei dati del sito selezionati da un sito primario figlio al sito di amministrazione centrale.
-  La possibilità di definire le impostazioni che determinano quando un collegamento di replica di database è danneggiato o non è riuscito.
-  La possibilità di specificare in quali casi generare avvisi per un collegamento di replica non riuscito.
-  Specificare la frequenza con cui Configuration Manager riepiloga i dati sul traffico di replica che usa il collegamento di replica. Questi dati vengono usati nei report.

Per configurare un collegamento di replica di database, modificare le proprietà per il collegamento nella console di Configuration Manager dal nodo **Replica di database**. Questo nodo viene visualizzato nell'area di lavoro **Monitoraggio** e nel nodo **Configurazione della gerarchia** nell'area di lavoro **Amministrazione** . È possibile modificare un collegamento di replica dal relativo sito padre o sito figlio.  

> [!TIP]  
> È possibile modificare i collegamenti di replica di database dal nodo **Replica di database** in qualsiasi area di lavoro. Tuttavia, quando si usa il nodo **Replica di database** nell'area di lavoro **Monitoraggio**, è possibile anche visualizzare lo stato della replica di database per i collegamenti di replica e accedere allo strumento Replication Link Analyzer che consente di rilevare eventuali problemi di replica.  

Per informazioni su come configurare i collegamenti di replica, vedere [Controlli di replica di database del sito](#BKMK_DBRepControls). Per altre informazioni su come monitorare la replica, vedere la sezione [Come monitorare lo stato e i collegamenti di replica del database](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) nell'argomento [Monitorare l'infrastruttura della gerarchia e di replica in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

Usare le informazioni contenute nelle sezioni seguenti per pianificare i collegamenti di replica di database.  

### <a name="bkmk_distviews"></a> Viste distribuite  
Le viste distribuite consentono alle richieste effettuate in un sito di amministrazione centrale per i dati del sito selezionati di accedere ai dati stessi direttamente dal database in un sito primario figlio. L'accesso diretto elimina la necessità di replicare questi dati dal sito primario al sito di amministrazione centrale. Poiché ogni collegamento di replica è indipendente dagli altri, è possibile usare le viste distribuite solo nei collegamenti di replica selezionati. Non è possibile usare viste distribuite tra un sito primario e un sito secondario.  

Le viste distribuite possono offrire i seguenti vantaggi:  

-  Ridurre il carico CPU per elaborare le modifiche del database nel sito di amministrazione centrale e nei siti primari
-  Ridurre la quantità di dati trasferiti attraverso la rete al sito di amministrazione centrale
-  Migliorare le prestazioni del server SQL che ospita il database del sito di amministrazione centrale
-  Ridurre lo spazio su disco usato dal database nel sito di amministrazione centrale

È consigliabile usare le viste distribuite nel caso in cui un sito primario si trovi molto vicino al sito di amministrazione centrale sulla rete e i due siti siano sempre attivi e sempre connessi. Le viste distribuite sostituiscono infatti la replica dei dati selezionati tra i siti con le connessioni dirette tra server SQL in ogni sito. Viene eseguita una connessione diretta ogni volta che viene effettuata una richiesta per questi dati nel sito di amministrazione centrale. In genere, le richieste di dati per le quali è possibile abilitare le viste distribuite vengono effettuate quando si eseguono report o query, quando si visualizzano le informazioni in Esplora inventario risorse e tramite valutazione delle raccolte che includono regole basate su dati del sito.  

Per impostazione predefinita, le viste distribuite sono disabilitate per ogni collegamento di replica. Quando si abilitano le viste distribuite per un collegamento di replica, vengono selezionati i dati del sito che non verranno replicati al sito di amministrazione centrale tramite tale collegamento. Il sito di amministrazione centrale accede a questi dati direttamente dal database del sito primario che condivide il collegamento. È possibile configurare i seguenti tipi di dati del sito per le viste distribuite:  

-  Dati di inventario hardware dai client
-  Dati di controllo e inventario software dai client
-  Messaggi di stato dai client, dal sito primario e da tutti i siti secondari

Da un punto di vista operativo, le viste distribuite non sono visibili a un utente amministratore che visualizza i dati nella console di Configuration Manager o nei report. Quando viene effettuata una richiesta di dati abilitata per le viste distribuite, il server SQL che ospita il database per il sito di amministrazione centrale accede direttamente al server SQL del sito primario figlio per recuperare le informazioni. Supponiamo, ad esempio, che si usi una console di Configuration Manager nel sito di amministrazione centrale per richiedere dati di inventario hardware da due siti, ma che solo un sito abbia un inventario hardware abilitato per una vista distribuita. Le informazioni di inventario per i client del sito non configurato per le viste distribuite vengono recuperate dal database nel sito di amministrazione centrale. È possibile accedere alle informazioni di inventario relative ai client del sito che è configurato per le viste distribuite dal database del sito primario figlio. Queste informazioni vengono visualizzate nella console di Configuration Manager o in un report senza identificazione dell'origine.  

Finché il tipo di dati di un collegamento di replica è abilitato per le viste distribuite, il sito primario figlio non replica i dati al sito di amministrazione centrale. Non appena vengono disattivate le viste distribuite per un tipo di dati, il sito primario figlio riprende la replica dei dati al sito di amministrazione centrale come parte della normale replica di dati. Prima che questi dati diventino disponibili nel sito di amministrazione centrale, i gruppi di replica che li contengono devono comunque essere reinizializzati tra il sito primario e il sito di amministrazione centrale. Allo stesso modo, dopo aver disinstallato un sito primario abilitato per le viste distribuite, il sito di amministrazione centrale deve completare la reinizializzazione dei suoi dati affinché i dati che erano abilitati alle viste distribuite siano accessibili al suo interno.  

> [!IMPORTANT]  
> Quando si usano le viste distribuite in un collegamento di replica nella gerarchia del sito, è necessario disabilitare le viste distribuite per tutti i collegamenti di replica prima di disinstallare un sito primario. Per ulteriori informazioni, vedere [Disinstallare un sito primario configurato con viste distribuite](../../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#BKMK_UninstallPrimaryDistViews).  

#### <a name="prerequisites-and-limitations-for-distributed-views"></a>Prerequisiti e limitazioni per le viste distribuite  

-  È possibile usare le viste distribuite solo nei collegamenti di replica tra un sito di amministrazione centrale e un sito primario.
- Il sito di amministrazione centrale deve usare un'edizione Enterprise di SQL Server. Il sito primario non presenta questo requisito.
-  Il sito di amministrazione centrale prevede l'installazione di una singola istanza del provider SMS, che deve essere eseguita nel server di database del sito. Ciò è richiesto per supportare l'autenticazione Kerberos necessaria per consentire al server SQL nel sito di amministrazione centrale di accedere al server SQL nel sito primario figlio. Non esistono limitazioni nel provider SMS nel sito primario figlio.
-  Il sito di amministrazione centrale prevede l'installazione di un solo punto di Reporting Services SQL Server, che deve essere ubicato nel server di database del sito. Ciò è richiesto per supportare l'autenticazione Kerberos necessaria per consentire al server SQL nel sito di amministrazione centrale di accedere al server SQL nel sito primario figlio.
-  Il database del sito non può essere ospitato su un cluster SQL Server.
-  Il database del sito non può essere ospitato in un gruppo di disponibilità Always On di SQL Server.
-  L'account computer del server del database del sito di amministrazione centrale deve avere le autorizzazioni di lettura per il database del sito primario.

> [!IMPORTANT]  
>  Le viste distribuite e le pianificazioni del momento in cui poter replicare i dati sono configurazioni per un collegamento di replica del database che si escludono a vicenda.  

### <a name="BKMK_schedules"></a> Pianificare trasferimenti dei dati del sito in collegamenti di replica di database  
Per consentire all'utente di controllare la larghezza di banda di rete usata per replicare i dati del sito da un sito primario figlio al relativo sito di amministrazione centrale, è possibile pianificare quando un collegamento di replica viene usato e specificare quando diversi tipi di dati del sito vengono replicati. È possibile controllare quando il sito primario replica i messaggi di stato, l'inventario e i dati di controllo. I collegamenti di replica del database dei siti secondari non supportano le pianificazioni per i dati del sito. Non è possibile pianificare il trasferimento di dati globali.  

Quando si configura un collegamento di replica del database, è possibile limitare il trasferimento di dati del sito selezionati dal sito primario al sito di amministrazione centrale e configurare diversi cicli per replicare diversi tipi di dati del sito.  

> [!IMPORTANT]  
> Le viste e pianificazioni distribuite per quando possono essere replicati i dati sono configurazioni reciprocamente esclusive per un collegamento di replica del database.  

### <a name="BKMK_SummarizeDBReplication"></a> Riepilogo del traffico di replica di database  
Ogni sito riepiloga periodicamente i dati sul traffico di rete che attraversa i collegamenti di replica di database del sito. I dati riepilogati vengono usati nei report per la replica del database. Entrambi i siti su un collegamento di replica riepilogano il traffico di rete che attraversa il collegamento di replica. Il riepilogo dei dati viene eseguito da SQL Server che ospita il database del sito. Dopo il riepilogo dei dati, queste informazioni vengono replicate ad altri siti come dati globali.  

Per impostazione predefinita, il riepilogo avviene ogni 15 minuti. Per modificare la frequenza di riepilogo per il traffico di rete, modificare il valore in **Intervallo riepilogo** nelle proprietà del collegamento di replica del database. La frequenza di riepilogo riguarda le informazioni visualizzate nei report sulla replica di database. È possibile scegliere un intervallo compreso tra 5 e 60 minuti. Più alta è la frequenza di riepilogo, maggiore sarà il carico di elaborazione sul server SQL in ogni sito sul collegamento di replica.  

### <a name="BKMK_DBRepThresholds"></a> Soglie di replica del database  
Le soglie di replica del database definiscono quando lo stato di un collegamento di replica del database risulta ridotto o non riuscito. Per impostazione predefinita, un collegamento assume lo stato danneggiato quando un gruppo di replica non completa la replica dopo 12 tentativi consecutivi. Al collegamento è assegnato lo stato non riuscito quando un gruppo di replica non esegue la replica dopo 24 tentativi consecutivi.  

È possibile specificare valori personalizzati per definire quando Configuration Manager segnala un collegamento di replica come danneggiato o non riuscito. Regolare il momento in cui Configuration Manager riporta ogni stato per i collegamenti di replica del database può consentire all'utente di monitorare con precisione l'integrità della replica del database attraverso i collegamenti di replica di database.  

Poiché è possibile che uno o alcuni gruppi di replica non eseguano la replica mentre altri continuino a replicare correttamente, è consigliabile pianificare la revisione dello stato di replica di un collegamento di replica quando questo assume lo stato di danneggiato. Se sono presenti dei ritardi ricorrenti per specifici gruppi di replica ma il ritardo non rappresenta un problema oppure il collegamento di replica tra siti ha una bassa larghezza di banda disponibile, è possibile modificare i valori dei tentativi per lo stato ridotto o non riuscito del collegamento. Aumentando il numero di tentativi prima che il collegamento sia impostato su danneggiato o non riuscito, è possibile eliminare gli avvisi non necessari per problemi noti e tenere traccia con più precisione dello stato del collegamento.  

È necessario considerare anche l'intervallo di sincronizzazione della replica per ogni gruppo di replica per conoscere la frequenza con cui viene eseguita la replica di tale gruppo. Per visualizzare **Intervallo di sincronizzazione** per i gruppi di replica, nel nodo **Replica di database** dell'area di lavoro **Monitoraggio** selezionare la scheda **Dettaglio di replica**.  

Per altre informazioni su come monitorare la replica di database e su come visualizzarne lo stato, vedere [Come monitorare lo stato e i collegamenti di replica del database](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) nell'argomento [Monitorare l'infrastruttura della gerarchia e di replica in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

Per informazioni sulla configurazione delle soglie di replica di database, vedere [Controlli di replica di database del sito](#BKMK_DBRepControls).  

## <a name="BKMK_DBRepControls"></a> Controlli di replica di database del sito  
È possibile modificare le impostazioni per ogni database del sito per controllare la larghezza di banda di rete usata per la replica di database. Le impostazioni si applicano solo al database del sito in cui vengono configurate. Il sito usa sempre queste impostazioni per replicare i dati a un altro sito tramite replica di database.  

Di seguito sono elencati i controlli di replica che è possibile modificare per ogni database del sito:  

-  Modificare la porta SSB.  
-  Configurare il tempo di attesa prima che venga reinizializzata la copia del database del sito a seguito di tentativi di replica non riusciti.  
-  Configurare un database del sito per comprimere i dati di replica dalla replica del database. I dati sono compressi solo per il trasferimento tra siti e non per l'archiviazione nel database del sito su ogni sito.  

Per modificare le impostazioni dei controlli di replica per un database del sito, modificare le proprietà del database del sito nella console di Configuration Manager dal nodo **Replica di database**. È possibile visualizzare questo nodo sotto il nodo **Configurazione della gerarchia** nell'area di lavoro **Amministrazione** e anche in **Area di lavoro di monitoraggio**. Per modificare le proprietà del database del sito, selezionare il collegamento di replica tra i siti e aprire **Proprietà database principale** oppure **Proprietà database secondario**.  

> [!TIP]  
> È possibile configurare i controlli di replica del database dal nodo **Replica di database** in qualsiasi area di lavoro. Tuttavia, quando si usa il nodo **Replica di database** nell'area di lavoro **Monitoraggio**, è possibile anche visualizzare lo stato di replica del database per un collegamento di replica e accedere allo strumento Replication Link Analyzer, che consente all'utente di esaminare eventuali problemi di replica.  

---
title: Trasferimenti di dati | System Center Configuration Manager
description: "Questo argomento spiega in che modo Configuration Manager sposta i dati tra i siti e come si può gestire il trasferimento dei dati in rete."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
caps.latest.revision: 12
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1abd28aa4ce4f946f6328f8f7924b5f5a81e640c


---
# <a name="data-transfers-between-sites-in-system-center-configuration-manager"></a>Trasferimenti di dati tra siti in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager usa la **replica basata su file** e la **replica di database** per il trasferimento di diversi tipi di informazioni tra siti.  Le sezioni di questo argomento illustrano il modo in cui Configuration Manager sposta i dati tra i siti e come gestire il trasferimento dei dati nella propria rete.  


##  <a name="a-namebkmkfileroutea-file-based-replication"></a><a name="bkmk_fileroute"></a> File-based replication  
 Configuration Manager usa la replica basata su file per trasferire i dati basati su file tra i siti all'interno della gerarchia. Tali dati includono contenuti quali applicazioni e pacchetti che si desidera distribuire in punti di distribuzione nei siti figlio, oltre ai record dei dati di individuazione non elaborati che vengono trasferiti ai siti padre in fase di elaborazione.  

 La comunicazione tra siti basata su file usa il protocollo **Server Message Block** (SMB) con la **porta TCP/IP 445**. È possibile specificare configurazioni che includano la limitazione della larghezza di banda e la modalità a impulsi per controllare la quantità di dati trasferiti attraverso la rete, oltre a pianificazioni per controllare quando inviare i dati attraverso la rete.  

###  <a name="a-namebkmkroutesa-file-replication-routes"></a><a name="bkmk_routes"></a> Route di replica file  
 Le informazioni seguenti possono essere utili per configurare e usare le route di replica file:  

 **Route di replica file** : ogni route di replica file identifica un sito di destinazione a cui è possibile trasferire dati basati su file. Ogni sito supporta una sola route di replica file a uno specifico sito di destinazione.  

 Configuration Manager supporta le seguenti configurazioni per le route di replica file:  

-   **Account replica file**: account usato per la connessione al sito di destinazione e la scrittura di dati nella condivisione **SMS_SITE** di tale sito. I dati scritti in questa condivisione vengono elaborati dal sito ricevente. Per impostazione predefinita, quando un sito viene aggiunto alla gerarchia, Configuration Manager assegna l'account computer del server del sito dei nuovi siti come **Account replica file** di tali siti. Questo account viene quindi aggiunto al gruppo **SMS_SiteToSiteConnection_&lt;CodiceSito\>** del sito di destinazione, ovvero un gruppo locale nel computer che consente l'accesso alla condivisione **SMS_SITE**. È possibile modificare questo account in un account utente di Windows. Se si modifica l'account, verificare che il nuovo account venga aggiunto al gruppo **SMS_SiteToSiteConnection_&lt;CodiceSito\>** del sito di destinazione.  

    > [!NOTE]  
    >  I siti secondari usano sempre l'account computer del server del sito secondario come **Account replica file**.  

-   **Pianificazione**: è possibile configurare la pianificazione per ciascuna route di replica file in modo da limitare il tipo di dati e l'ora in cui i dati possono essere trasferiti al sito di destinazione.  

-   **Limiti di velocità**: È possibile configurare limiti di velocità per ciascuna route di replica file in modo da controllare la larghezza di banda di rete usata quando il sito trasferisce i dati al sito di destinazione:  

    -   Usare **Modalità a impulsi** per specificare la dimensione dei blocchi di dati inviati al sito di destinazione. È inoltre possibile specificare un ritardo tra l'invio di ogni blocco di dati. Usare questa opzione quando è necessario inviare i dati attraverso una connessione di rete con larghezza di banda molto bassa al sito di destinazione. È possibile, ad esempio, che si sia vincolati a inviare 1 KB di dati ogni cinque secondi, ma non 1 KB ogni tre secondi, indipendentemente dalla velocità del collegamento o dall'utilizzo in un determinato momento.  

    -   Usare **Limitato alle velocità di trasferimento massime specificate per ora** per fare in modo che un sito invii i dati a un sito di destinazione usando solo la percentuale di tempo specificata. Quando si usa questa opzione, Configuration Manager non identifica la larghezza di banda disponibile per la rete, ma divide in intervalli il periodo di tempo in cui può inviare i dati. I dati vengono quindi inviati in un breve intervallo di tempo, seguito da periodi di tempo in cui i dati non vengono inviati. Se ad esempio la velocità massima è impostata su **50%**, Configuration Manager trasmette i dati per un periodo di tempo seguito da un uguale periodo di tempo in cui non viene inviato alcun dato. La quantità effettiva di dati, o dimensione del blocco di dati, non è gestita. Viene invece gestita solo la quantità di tempo durante il quale i dati vengono inviati.  

        > [!CAUTION]  
        >  Per impostazione predefinita, un sito può usare fino a tre **invii simultanei** per trasferire i dati a un sito di destinazione. Quando si abilitano i limiti di velocità per una route di replica file, gli **invii simultanei** per l'invio dei dati a tale sito sono limitati a uno. Questa impostazione si applica anche quando l'opzione **Limita larghezza di banda disponibile (%)** è impostata su **100%**. Se ad esempio si usano le impostazioni predefinite per il mittente, la velocità di trasferimento al sito di destinazione viene ridotta a un terzo della capacità predefinita.  

-   È possibile configurare una route di replica file tra due siti secondari per distribuire contenuto basato su file fra tali siti.  

Per gestire una route di replica file, nell'area di lavoro **Amministrazione** espandere il nodo **Configurazione della gerarchia** e selezionare **Replica file**.  

**Mittente** : ogni sito ha un mittente. Il mittente gestisce la connessione di rete da un sito a un sito di destinazione e può stabilire connessioni simultanee con più siti. Per connettersi a un sito, il mittente usa la route di replica file al sito per identificare l'account da usare al fine di stabilire la connessione di rete. Il mittente usa questo account anche per scrivere i dati nella condivisione **SMS_SITE** del sito di destinazione.  

 Per impostazione predefinita, il mittente scrive i dati in un sito di destinazione usando più **invii simultanei**, in genere indicati come thread. Ogni invio simultaneo, o thread, è in grado di trasferire un oggetto basato su file differente al sito di destinazione. Per impostazione predefinita, una volta avviato l'invio di un oggetto, il mittente continua a scrivere blocchi di dati relativi a tale oggetto fino al suo completo invio. Dopo l'invio di tutti i dati relativi all'oggetto, sarà possibile iniziare l'invio di un nuovo oggetto su tale thread.  

 È possibile configurare le seguenti impostazioni per un mittente:  

-   **Numero massimo di invii simultanei**: per impostazione predefinita, ciascun sito è configurato per l'utilizzo di cinque **invii simultanei**, tre dei quali sono disponibili in caso di invio dei dati a un sito di destinazione. Aumentando tale numero è possibile incrementare la velocità effettiva dei dati tra siti, consentendo a Configuration Manager di trasferire più file simultaneamente. L'incremento di questo numero determina anche un aumento della richiesta di larghezza di banda della rete tra siti.  

-   **Impostazioni tentativi**: per impostazione predefinita, ogni sito è configurato per eseguire due tentativi, a distanza di un minuto, in caso di connessione non riuscita. È possibile modificare il numero di tentativi di connessione e il relativo intervallo di attesa.  

Per gestire il mittente per un sito, espandere il nodo **Configurazione del sito** nell'area di lavoro **Amministrazione** , selezionare il nodo **Siti** , quindi fare clic su **Proprietà** per il sito che si desidera gestire. Fare clic sulla scheda **Mittente** per modificare la configurazione del mittente.  

##  <a name="a-namebkmkdbrepa-database-replication"></a><a name="bkmk_dbrep"></a> Database replication  
La replica di database di Configuration Manager usa SQL Server per trasferire i dati e unire le modifiche apportate in un database del sito con le informazioni archiviate nel database in altri siti della gerarchia.  

-   In questo modo, tutti i siti condividono le stesse informazioni  

-   Quando si installa un sito in una gerarchia, viene configurata automaticamente la replica di database tra il nuovo sito e il sito padre designato.  

-   Al termine dell'installazione del sito, la replica di database viene avviata automaticamente.  

Quando si aggiunge un nuovo sito in una gerarchia, Configuration Manager crea un database generico nel nuovo sito. Successivamente, il sito padre crea uno snapshot dei dati rilevanti nel relativo database e trasferisce tale snapshot nel nuovo sito tramite replica basata su file. Il nuovo sito usa quindi un programma di copia bulk SQL Server (BCP) per caricare le informazioni nella copia locale del database di Configuration Manager. Dopo il caricamento dello snapshot, ogni sito esegue la replica di database con l'altro sito.  

Per replicare i dati tra siti, Configuration Manager usa il proprio servizio di replica database. Il servizio di replica di database usa il rilevamento delle modifiche SQL Server per monitorare eventuali modifiche nel database del sito locale e quindi replica tali modifiche in altri siti usando **SQL Server Service Broker**. Per impostazione predefinita, questo processo usa la **porta TCP/IP 4022**.  

Configuration Manager riunisce i dati replicati con replica di database in gruppi di replica diversi.  

-   Ciascun gruppo di replica dispone di una pianificazione di replica fissa, separata, che determina la frequenza di replica delle modifiche apportate ai dati del gruppo su altri siti.  

     Ad esempio, una modifica alla configurazione dell'amministrazione basata su ruoli viene rapidamente replicata su altri siti per garantire che tali cambiamenti vengano applicati il prima possibile. Al contempo, una modifica alla configurazione con priorità più bassa, come una richiesta di installazione di un nuovo sito secondario, viene replicata con meno urgenza e sono necessari diversi minuti perché la richiesta del nuovo sito raggiunga il sito primario di destinazione.  

-   Per la replica di database, è possibile modificare gli aspetti seguenti:  

    -   **Collegamenti di replica di database** , che consentono di controllare quando traffico specifico attraversa la rete.  

    -   **Viste distribuite** , che rappresentano una configurazione per i collegamenti di replica e consentono alle richieste effettuate in un sito di amministrazione centrale per i dati del sito selezionati di accedere a tali dati direttamente dal database in un sito primario figlio.  

    -   **Pianificazioni** , che consentono di definire quando viene usato un collegamento di replica e di specificare quando diversi tipi di dati del sito vengono replicati.  

    -   **Riepilogo** dei dati sul traffico di rete che attraversa i collegamenti di replica, eseguito per impostazione predefinita ogni 15 minuti e usato nei report per la replica di database.  

    -   **Soglie di replica del database** , che definiscono quando i collegamenti vengono segnalati come danneggiati o non riusciti. È anche possibile definire quando Configuration Manager genera avvisi sui collegamenti di replica con stato danneggiato o non riuscito.  

Configuration Manager classifica i dati replicati con la replica di database come dati globali o dati del sito. Quando si verifica la replica di database, le modifiche ai dati globali e ai dati del sito vengono trasferite attraverso il collegamento di replica di database. I dati globali possono essere replicati sul sito padre o sito figlio e il sito viene replicato solo su un sito padre. Un terzo tipo di dati, denominato dati locali, non viene replicato su altri siti. I dati locali includono informazioni non richieste da altri siti:  

-   **Dati globali**: i dati globali fanno riferimento a oggetti creati dall'amministratore che vengono replicati su tutti i siti in tutta la gerarchia, sebbene i siti secondari ricevano solo un sottoinsieme di dati globali, come dati proxy globali. Esempi di dati globali includono distribuzioni e aggiornamenti software, definizioni di raccolte e ambiti di protezione amministrazione basata sui ruoli. Gli amministratori possono creare dati globali in siti di amministrazione centrale e siti primari.  

-   **Dati del sito**: i dati del sito fanno riferimento a informazioni operative create dai siti primari di Configuration Manager e dai client connessi ai siti primari. I dati del sito vengono replicati nel sito di amministrazione centrale, ma non in altri siti primari. Esempi di dati del sito includono dati dell'inventario hardware, messaggi di stato, avvisi e i risultati delle raccolte basate su query. I dati del sito possono essere visualizzati solo nel sito di amministrazione centrale e nel sito primario da originano. Possono essere modificati solo nel sito primario in cui sono stati creati.  

     Tutti i dati del sito vengono replicati sul sito di amministrazione centrale; pertanto, quest'ultimo si occupa dell'amministrazione e del reporting dell'intera gerarchia.  

Le seguenti sezioni descrivono in dettaglio le configurazioni che è possibile usare per gestire la replica di database  

###  <a name="a-namebkmkdblinksa-database-replication-links"></a><a name="bkmk_Dblinks"></a> Collegamenti di replica di database  
Quando si installa un nuovo sito in una gerarchia, Configuration Manager crea automaticamente un collegamento di replica di database tra i due siti. Viene creato un singolo collegamento per collegare il nuovo sito al sito padre.  

Ogni collegamento di replica di database supporta configurazioni che aiutano a controllare il trasferimento dei dati nel collegamento. Ogni collegamento di replica supporta configurazioni separate. I controlli per i collegamenti di replica di database includono:  

-   Usare le viste distribuite per arrestare la replica dei dati del sito selezionati da un sito primario al sito di amministrazione centrale, quindi abilitare il sito di amministrazione centrale per accedere direttamente a questi dati dal database del sito primario.  

-   Pianificare le tempistiche di trasferimento dei dati del sito selezionati da un sito primario figlio al sito di amministrazione centrale.  

-   Definire le impostazioni che determinano quando un collegamento di replica di database è in uno stato danneggiato o non è riuscito.  

-   Configurare le tempistiche di generazione degli avvisi per un collegamento di replica non riuscito.  

-   Specificare la frequenza con cui Configuration Manager riepiloga i dati sul traffico di replica che usa il collegamento di replica. Questi dati vengono usati nei report.  

Per configurare un collegamento di replica di database, è necessario modificare le proprietà per il collegamento nella console di Configuration Manager dal nodo **Replica di database**. Questo nodo viene visualizzato nell'area di lavoro **Monitoraggio** e nel nodo **Configurazione della gerarchia** nell'area di lavoro **Amministrazione** . È possibile modificare un collegamento di replica dal relativo sito padre o sito figlio.  

> [!TIP]  
>  È possibile modificare i collegamenti di replica di database dal nodo **Replica di database** in qualsiasi area di lavoro. Tuttavia, quando si usa il nodo **Replica di database** nell'area di lavoro **Monitoraggio** , è possibile anche visualizzare lo stato della replica di database per i collegamenti di replica e accedere allo strumento Replication Link Analyzer che consente all'utente di esaminare eventuali problemi di replica.  

Per informazioni su come configurare i collegamenti di replica, vedere [Controlli di replica di database del sito](#BKMK_DBRepControls). Per altre informazioni su come monitorare la replica, vedere la sezione [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) nell'argomento [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) .  

Usare le informazioni nelle sezioni seguenti per pianificare i collegamenti di replica di database.  

###  <a name="a-namebkmkdistviewsa-distributed-views"></a><a name="bkmk_distviews"></a> Viste distribuite  
Le viste distribuite consentono le richieste effettuate su un sito di amministrazione centrale per i dati del sito selezionati, per l'accesso ai dati stessi direttamente dal database presente nel sito primario figlio. L'accesso diretto elimina la necessità di replicare questi dati dal sito primario al sito di amministrazione centrale. Poiché ogni collegamento di replica è indipendente dagli altri, è possibile abilitare le viste distribuite solo sui collegamenti di replica desiderati. Le viste distribuite non sono supportate tra un sito primario e un sito secondario.  

Le viste distribuite possono offrire i seguenti vantaggi:  

-   Ridurre il carico della CPU per elaborare le modifiche del database sul sito di amministrazione centrale e sui siti primari.  

-   Ridurre la quantità di dati trasferiti attraverso la rete al sito di amministrazione centrale.  

-   Migliorare le prestazioni di SQL Server che ospita il database dei siti di amministrazione centrale.  

-   Ridurre lo spazio su disco usato dal database sul sito di amministrazione centrale.  

Considerare l'utilizzo di viste distribuite quando un sito primario si trova molto vicino al sito di amministrazione centrale sulla rete e i due siti sono sempre attivi, sempre connessi. Le viste distribuite sostituiscono la replica dei dati selezionati tra i siti con le connessioni dirette tra server SQL in ciascun sito. Questa connessione diretta viene eseguita ogni volta che viene effettuata una richiesta per questi dati nel sito di amministrazione centrale. In genere, le richieste di dati per le quali è possibile abilitare le viste distribuite vengono effettuate quando si eseguono report o query, si visualizzano le informazioni in Esplora inventario risorse e tramite valutazione delle raccolte che includono regole basate sui dati del sito.  

Per impostazione predefinita, le viste distribuite sono disabilitate per ciascun collegamento di replica. Quando vengono abilitate le viste distribuite per un collegamento di replica, è necessario selezionare i dati del sito che non saranno replicati nel sito di amministrazione centrale nel collegamento. È inoltre necessario abilitare il sito di amministrazione centrale per l'accesso diretto a questi dati dal database del sito primario figlio che condivide il collegamento. È possibile configurare i seguenti tipi di dati del sito per le viste distribuite:  

-   Dati di inventario hardware dai client  

-   Dati di controllo e inventario software dai client  

-   Messaggi di stato dai client, dal sito primario e da tutti i siti secondari  

Da un punto di vista operativo, le viste distribuite non sono visibili a un utente amministratore che visualizza i dati nella console di Configuration Manager o nei report. Quando viene effettuata una richiesta di dati abilitata per le viste distribuite, il server SQL che ospita il database per il sito di amministrazione centrale accede direttamente al server SQL del sito primario figlio per recuperare le informazioni. Supponiamo, ad esempio, che si usi una console di Configuration Manager nel sito di amministrazione centrale per richiedere dati di inventario hardware da due siti, ma che solo un sito abbia un inventario hardware abilitato per una vista distribuita. Le informazioni di inventario per i client del sito non configurato per le viste distribuite vengono recuperate dal database nel sito di amministrazione centrale. È possibile accedere alle informazioni di inventario relative ai client del sito che è configurato per le viste distribuite dal database del sito primario figlio. Queste informazioni vengono visualizzate nella console di Configuration Manager o nel report senza distinzione dell'origine.  

Finché un collegamento di replica dispone di un tipo di dati abilitato per le viste distribuite, il sito primario figlio non replica tali dati nel sito di amministrazione centrale. Non appena vengono disattivate le viste distribuite per un tipo di dati, il sito primario figlio riprende la replica di tali dati sul sito di amministrazione centrale come parte della normale replica di dati. Tuttavia, prima che questi dati siano resi disponibili sul sito di amministrazione centrale, i gruppi di replica che li contengono devono essere reinizializzati tra il sito primario e il sito di amministrazione centrale. Allo stesso modo, dopo aver disinstallato un sito primario abilitato per le viste distribuite, il sito di amministrazione centrale deve completare la reinizializzazione dei suoi dati affinché i dati che erano abilitati alle viste distribuite siano accessibili al suo interno.  

> [!IMPORTANT]  
>  Quando si usano le viste distribuite su un collegamento di replica nella gerarchia, è necessario disabilitare le viste distribuite per tutti i collegamenti di replica prima di disinstallare qualsiasi sito primario. Per ulteriori informazioni, vedere [Uninstall a primary site that is configured with distributed views](../../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#BKMK_UninstallPrimaryDistViews).  

**Prerequisiti e limitazioni per le viste distribuite:**  

-   Le viste distribuite sono supportate solo sui collegamenti di replica tra un sito di amministrazione centrale e un sito primario.  

-  Il sito di amministrazione centrale deve usare un'edizione Enterprise di SQL Server. Il sito primario non presenta questo requisito.

-   Il sito di amministrazione centrale prevede l'installazione di una singola istanza del provider SMS, che deve essere eseguita nel server di database del sito. Ciò è richiesto per supportare l'autenticazione Kerberos necessaria per consentire al server SQL sul sito di amministrazione centrale di accedere al server SQL sul sito primario figlio. Non esistono limitazioni nel provider SMS nel sito primario figlio.  

-   Il sito di amministrazione centrale prevede l'installazione di un solo punto di Reporting Services SQL Server, che deve essere ubicato nel server di database del sito. Ciò è richiesto per supportare l'autenticazione Kerberos necessaria per consentire al server SQL sul sito di amministrazione centrale di accedere al server SQL sul sito primario figlio.  

-   Il database del sito non può essere ospitato su un cluster SQL Server.  

-   Il database del sito non può essere ospitato in un gruppo di disponibilità SQL Server AlwaysOn.  

-   L'account computer del server del database dal sito di amministrazione centrale richiede le autorizzazioni di **Read** per il database del sito primario.  

> [!IMPORTANT]  
>  Le viste e pianificazioni distribuite per quando possono essere replicati i dati sono configurazioni reciprocamente esclusive per un collegamento di replica del database.  

###  <a name="a-namebkmkschedulesa-schedule-transfers-of-site-data-on-database-replication-links"></a><a name="BKMK_schedules"></a> Pianificare trasferimenti dei dati del sito in collegamenti di replica di database  
Per consentire all'utente di controllare la larghezza di banda di rete usata per replicare i dati del sito da un sito primario figlio al relativo sito di amministrazione centrale, è possibile pianificare quando un collegamento di replica viene usato e specificare quando diversi tipi di dati del sito vengono replicati. È possibile controllare quando il sito primario replica i messaggi di stato, l'inventario e i dati di controllo. I collegamenti di replica del database dei siti secondari non supportano le pianificazioni per i dati del sito. Non è possibile pianificare il trasferimento di dati globali.  

Quando si configura un collegamento di replica del database, è possibile limitare il trasferimento di dati del sito selezionati dal sito primario al sito di amministrazione centrale e configurare diversi cicli per replicare diversi tipi di dati del sito.  

> [!IMPORTANT]  
>  Le viste e pianificazioni distribuite per quando possono essere replicati i dati sono configurazioni reciprocamente esclusive per un collegamento di replica del database.  

###  <a name="a-namebkmksummarizedbreplicationa-summarization-of-database-replication-traffic"></a><a name="BKMK_SummarizeDBReplication"></a> Riepilogo del traffico di replica di database  
Periodicamente, ogni sito riepiloga i dati sul traffico di rete che attraversa i collegamenti di replica di database che includono il sito. Tali dati riepilogati vengono usati nei report per la replica del database. Entrambi i siti su un collegamento di replica riepilogano il traffico di rete che attraversa il collegamento di replica. Il riepilogo dei dati viene eseguito da SQL Server che ospita il database del sito. Dopo il riepilogo dei dati, queste informazioni replicano su altri siti come dati globali.  

Per impostazione predefinita, il riepilogo avviene ogni 15 minuti. È possibile modificare la frequenza del riepilogo per il traffico di rete modificando l' **Intervallo riepilogo** nelle proprietà del collegamento di replica del database. La frequenza di riepilogo riguarda le informazioni visualizzate nei report sulla replica del database. È possibile modificare questo intervallo da 5 a 60 minuti. Quando si aumenta la frequenza di riepilogo, è possibile aumentare il carico di elaborazione su SQL Server in ogni sito sul collegamento di replica.  

###  <a name="a-namebkmkdbrepthresholdsa-database-replication-thresholds"></a><a name="BKMK_DBRepThresholds"></a> Soglie di replica del database  
Le soglie di replica del database definiscono quando lo stato di un collegamento di replica del database risulta ridotto o non riuscito. Per impostazione predefinita, un collegamento viene impostato su ridotto quando un gruppo di replica non riesce a completare la replica con 12 tentativi consecutivi e su non riuscito quando non riesce a effettuare la replica con 24 tentativi consecutivi.  

È possibile specificare valori personalizzati per definire quando Configuration Manager segnala un collegamento di replica come danneggiato o non riuscito. Regolare il momento in cui Configuration Manager riporta ogni stato per i collegamenti di replica del database può consentire all'utente di monitorare con precisione l'integrità della replica del database attraverso i collegamenti di replica di database.  

Poiché è possibile che uno o alcuni gruppi di replica non riescano a replicare mentre altri gruppi di replica continuano a replicare correttamente, pianificare la revisione dello stato di replica di un collegamento di replica quando questo riporta per primo lo stato di ridotto. Se sono presenti dei ritardi ricorrenti per specifici gruppi di replica ma il ritardo non rappresenta un problema oppure il collegamento di replica tra siti ha una bassa larghezza di banda disponibile, è possibile modificare i valori dei tentativi per lo stato ridotto o non riuscito del collegamento. Quando si aumenta il numero di tentativi prima che il collegamento sia impostato su ridotto o non riuscito, è possibile eliminare i falsi avvisi per i problemi noti, cosa che consente all'utente di tenere traccia con più precisione dello stato del collegamento.  

È necessario prendere in considerazione anche l'intervallo di sincronizzazione di replica per ogni gruppo di replica per comprendere la frequenza con cui viene eseguita la replica di tale gruppo. L' **Intervallo di sincronizzazione** per i gruppi di replica è disponibile nella scheda **Dettaglio di replica** di un collegamento di replica nel nodo **Replica di database** nell'area di lavoro **Monitoraggio** .  

Per altre informazioni sul monitoraggio della replica di database, inclusa la visualizzazione dello stato della replica, vedere la sezione [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) nell'argomento [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) .  

Per informazioni sulla configurazione delle soglie di replica di database, vedere [Controlli di replica di database del sito](#BKMK_DBRepControls).  

##  <a name="a-namebkmkdbrepcontrolsa-site-database-replication-controls"></a><a name="BKMK_DBRepControls"></a> Controlli di replica di database del sito  
Ogni database del sito supporta le configurazioni che consentono di controllare la larghezza di banda di rete usata per la replica del database. Queste configurazioni si applicano solo al database del sito laddove si configurano le impostazioni e vengono sempre usate quando il sito replica qualsiasi dato per replica del database su qualsiasi altro sito.  

I controlli di replica per ogni database del sito includono i seguenti elementi:  

-   Cambiare la porta usata da Configuration Manager per SQL Server Service Broker.  

-   Configurare il tempo di attesa prima che venga reinizializzata la copia del database del sito a seguito di tentativi di replica non riusciti.  

-   Configurare un database del sito per comprimere i dati di replica dalla replica del database. I dati sono compressi solo per il trasferimento tra siti e non per l'archiviazione nel database del sito su ogni sito.  

Per configurare i controlli di replica per un database del sito, si modificano le proprietà del database del sito nella console di Configuration Manager dal nodo **Replica di database**. È possibile visualizzare questo nodo sotto il nodo **Configurazione della gerarchia** nell'area di lavoro **Amministrazione** e anche in **Area di lavoro di monitoraggio**. Per modificare le proprietà del database del sito, selezionare il collegamento di replica tra i siti e aprire **Proprietà database principale** oppure **Proprietà database secondario**.  

> [!TIP]  
>  È possibile configurare i controlli di replica del database dal nodo **Replica di database** in qualsiasi area di lavoro. Tuttavia, quando si usa il nodo **Replica di database** nell'area di lavoro **Monitoraggio** , è possibile anche visualizzare lo stato della replica del database per un collegamento di replica e accedere allo strumento Replication Link Analyzer che consente all'utente di esaminare eventuali problemi di replica.  



<!--HONumber=Nov16_HO1-->



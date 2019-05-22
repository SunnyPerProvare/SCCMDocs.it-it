---
title: Monitorare la replica
titleSuffix: Configuration Manager
description: Informazioni su come monitorare l'infrastruttura e le operazioni in Configuration Manager usando l'area di lavoro Monitoraggio della console.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3fab4d67-8d2a-45ce-8b06-471280102cf6
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: dcc3a43f1cc2393a66fe50ef74e864afeb27704c
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65501058"
---
# <a name="monitor-hierarchy-and-replication-infrastructure-in-system-center-configuration-manager"></a>Monitorare l'infrastruttura della gerarchia e di replica in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Per monitorare l'infrastruttura e le operazioni in System Center Configuration Manager, usare l'area di lavoro **Monitoraggio** della console di Configuration Manager.  

> [!NOTE]  
>  L'eccezione in questo percorso è la Migrazione, che viene monitorata direttamente nel nodo **Migrazione** nell'area di lavoro **Amministrazione** . Per altre informazioni, vedere [Operazioni per la migrazione a System Center Configuration Manager](../../../core/migration/operations-for-migration.md).  

 Oltre a usare la console di Configuration Manager per il monitoraggio, è possibile usare i report di Configuration Manager o visualizzare i file di log di Configuration Manager per i componenti di Configuration Manager. Per informazioni sui report, vedere [Creazione di report in System Center Configuration Manager](../../../core/servers/manage/reporting.md). Per informazioni sui file di log, vedere [File di log in System Center Configuration Manager](../../../core/plan-design/hierarchy/log-files.md).  

 Quando si effettua il monitoraggio di siti, cercare dei segnali che indichino problemi che richiedono un intervento. Ad esempio:  

-   Un backlog di file sui server del sito e sui sistemi del sito.  

-   Messaggi di stato che indicano un errore o un problema.  

-   Errori di comunicazione all'interno del sito.  

-   Messaggi di errore e di avviso nel registro eventi di sistema sui server.  

-   Messaggi di errore e di avviso nel registro degli errori di Microsoft SQL Server.  

-   Siti o client che non inviano report da molto tempo.  

-   Risposta lenta da parte del database di SQL Server.  

-   Segnali di errore hardware.  

Per ridurre al minimo il rischio di errore del sito, se le attività di monitoraggio manifestano qualsiasi tipo di problema, analizzare l'origine del problema e risolverlo appena possibile.  



##  <a name="BKMK_MonintorMgmtTasks"></a> Monitorare le attività di gestione comuni per Configuration Manager  
 Configuration Manager include una funzionalità di monitoraggio predefinita all'interno della console. È possibile monitorare numerose attività, tra cui quelle relative a: aggiornamenti software, risparmio energia e distribuzione del contenuto all'interno della gerarchia.  

 Usare le informazioni seguenti per monitorare le attività di Configuration Manager comuni:  

 **Avvisi**  
   Vedere [Avvisi di monitoraggio](../../../core/servers/manage/use-alerts-and-the-status-system.md#BKMK_MonitorAlerts) in [Usare gli avvisi e il sistema di stato per System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

 **Impostazioni di conformità**  
   Vedere [Come monitorare le impostazioni di conformità in System Center Configuration Manager](../../../compliance/deploy-use/monitor-compliance-settings.md).  

 **Distribuzione del contenuto**  
   Per informazioni generali sul monitoraggio del contenuto, vedere [Gestire il contenuto e l'infrastruttura del contenuto per System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

Per informazioni sul monitoraggio di tipi specifici di distribuzione del contenuto:
-   Per monitorare le applicazioni, vedere [Monitorare le applicazioni con System Center Configuration Manager](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

-   Per monitorare pacchetti e programmi, vedere Come gestire pacchetti e programmi in [Pacchetti e programmi in System Center Configuration Manager](../../../apps/deploy-use/packages-and-programs.md).  

**Endpoint Protection**  
   Vedere [Come monitorare Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/monitor-endpoint-protection.md).  

**Monitorare il risparmio energia**  
 Vedere [Come monitorare e pianificare il risparmio energia in System Center Configuration Manager](../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

**Monitorare il controllo del software**  
Vedere [Monitorare l'utilizzo delle app con la misurazione del software in System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

**Monitorare gli aggiornamenti software**  
 Vedere [Monitorare gli aggiornamenti software in System Center Configuration Manager](../../../sum/deploy-use/monitor-software-updates.md).  


##  <a name="BKMK_MonitorInfrastructure"></a> Monitorare l'infrastruttura della gerarchia per Configuration Manager  
Configuration Manager offre diversi metodi per monitorare lo stato e le operazioni della gerarchia. È possibile controllare lo stato del sistema di siti attraverso la gerarchia, monitorare la replica tra siti dalla gerarchia e dalla vista geografica del sito, monitorare i collegamenti di replica tra siti per la replica di database e utilizzare lo strumento Replication Link Analyzer per correggere problemi di replica.  

###  <a name="BKMK_SH_Node"></a> Informazioni sul nodo Gerarchia siti  
Il nodo **Gerarchia siti** dell'area di lavoro **Monitoraggio** offre una panoramica della gerarchia e dei collegamenti tra siti di Configuration Manager. È possibile utilizzare due viste:  

-   **Diagramma gerarchia**: visualizza la gerarchia come mappa topologica semplificata per mostrare solo le informazioni più importanti.  

-   **Vista geografica**: visualizza i siti in una mappa geografica con i percorsi del sito configurati.  

Utilizzare il nodo **Gerarchia siti** per monitorare l'integrità di ciascun sito, i collegamenti di replica tra siti e la loro relazione con fattori esterni, come la posizione geografica.  

Poiché lo stato del sito e lo stato dei collegamenti tra siti vengono replicati come dati del sito e non come dati globali, quando si collega la console di Configuration Manager a un sito primario figlio, non è possibile visualizzare lo stato del sito o del collegamento per gli altri siti primari o i relativi siti secondari figlio. Ad esempio, in una gerarchia a più siti primari, quando la console di Configuration Manager si collega a un sito primario, è possibile visualizzare lo stato dei siti secondari figlio, del sito primario e del sito di amministrazione centrale, ma non quello di altri nodi della gerarchia al di sotto del sito di amministrazione centrale.  

 Utilizzare il comando **Configura impostazioni** per controllare la modalità di visualizzazione dei rendering da parte della gerarchia del sito. Le configurazioni del nodo **Gerarchia siti** effettuate quando la console di Configuration Manager è collegata a un altro sito vengono replicate su tutti gli altri siti.  

#### <a name="hierarchy-diagram"></a>Diagramma gerarchia  
 Il diagramma gerarchia visualizza i siti in una mappa topologica. In questa vista, è possibile selezionare un sito e visualizzare un riepilogo dei messaggi di stato di tale sito, analizzare i messaggi di stato e accedere alla finestra di dialogo **Proprietà** dei siti.  

 Inoltre, è possibile lasciare il puntatore del mouse su un sito o un collegamento di replica tra siti per visualizzare lo stato di alto livello per l'oggetto. Poiché lo stato del collegamento di replica non viene replicato a livello globale, in una gerarchia con più siti primati, è necessario collegare la console di Configuration Manager al sito di amministrazione centrale per visualizzare i dettagli del collegamento di replica tra tutti i siti.  

 Le seguenti opzioni di modificano il diagramma gerarchia:  

-   **Gruppi**: è possibile configurare il numero di siti primari e secondari che attivano una modifica nella vista diagramma gerarchia che combini i siti in un singolo oggetto. Quando i siti vengono combinati in un singolo oggetto, si visualizza il numero totale di siti e un rollup di alto livello si messaggi di stato e stato dei siti. Le configurazioni dei gruppi non influenzano la vista geografica.  

-   **Siti preferiti**: è possibile specificare i singoli siti come sito preferito. Un'icona a stella identifica un sito preferito nel diagramma gerarchia. I siti preferiti non si combinano con altri siti quando sono stati utilizzati i gruppi e vengono sempre visualizzati singolarmente.  

#### <a name="geographical-view"></a>Vista geografica  
 la vista geografica visualizza la posizione di ogni sito su una mappa geografica. Vengono visualizzati solo i siti che è possibile configurare con una posizione. Quando si seleziona un sito in questa vista, vengono visualizzati i collegamenti di replica a siti padre o figlio. A differenza della vista Diagramma gerarchia, in questa vista non è possibile visualizzare i dettagli del messaggio di stato del sito o del collegamento di replica.  

> [!NOTE]  
>  Per utilizzare la vista geografica, sul computer a cui si collega la console di Configuration Manager deve essere installato Internet Explorer e deve essere possibile l'accesso a Bing Maps tramite il protocollo HTTP.  

L'opzione seguente modifica la vista geografica.  

-   **Percorso sito**: è possibile specificare una posizione geografica per ogni sito. È possibile specificare la posizione sotto forma di indirizzo, nome di località come un città oppure di coordinate latitudinali e longitudinali. Ad esempio, per utilizzare la latitudine e la longitudine di Redmond Washington, si dovrebbe specificare **N 47 40 26.3572 W 122 7 17.4432** come posizione del sito. Non è necessario specificare i simboli per i gradi, minuti o secondi della longitudine o latitudine. Configuration Manager usa Bing Maps per visualizzare la posizione nella vista geografica. Ciò fornisce l'opzione di visualizzare la gerarchia in relazione a una posizione geografica, che può fornire informazioni su questioni locali che possono influenzare la replica specifica di siti o tra siti.  

     Quando si specifica una posizione, è possibile utilizzare la casella **Percorso** per effettuare la ricerca di un sito specifico nella gerarchia. Una volta selezionato il sito, immettere la posizione come il nome di una città o un indirizzo nella colonna **Percorso** . Configuration Manager usa Bing Maps per risolvere il percorso.  

###  <a name="BKMK_MonitorRepLinksAndStatuss"></a> Come monitorare lo stato e i collegamenti di replica del database  
 Oltre ai dettagli di alto livello accessibili dal nodo **Gerarchia siti** nell'area di lavoro **Monitoraggio** , è possibile monitorare i dettagli della replica dei database anche usando il nodo **Replica di database** nell'area di lavoro **Monitoraggio** . Da **Replica di database** è possibile monitorare lo stato dei collegamenti di replica tra siti e i dettagli dell'inizializzazione e della replica per i gruppi di replica nel sito a cui è collegato Configuration Manager.  

> [!TIP]  
>  Nonostante un nodo **Replica di database** venga visualizzato anche sotto il nodo **Configurazione della gerarchia** nell'area di lavoro **Amministrazione** , da quella posizione non è possibile visualizzare lo stato di replica per i collegamenti di replica del database.  

####  <a name="BKMK_MonitorReplicationLinks"></a> Stato del collegamento di replica  
La replica di database tra siti implica la replica di diversi insiemi di informazioni, denominati gruppi di replica. Ogni gruppo di replica viene replicato con priorità di replica diverse. Per impostazione predefinita, i dati contenuti in un gruppo di replica e la frequenza di replica non possono essere modificati.  

 Quando un collegamento di replica è attivo e non presenta lo stato di non riuscito o ridotto, tutti i gruppi di replica vengono replicati nel tempo previsto. Quando uno o più gruppi di replica non riescono a completare la replica nel periodo di tempo previsto, il collegamento viene visualizzato come ridotto. I collegamenti ridotti possono comunque funzionare, ma occorre monitorarli per assicurarsi che ritornino allo stato attivo o esaminarli per assicurarsi che non si verifichino ulteriori errori di riduzione o replica.  

 Per ciascun collegamento di replica è possibile specificare il numero di volte che un gruppo di replica replicato con esito negativo può ritentare la replica prima che lo stato del collegamento venga impostato su ridotto o non riuscito. Anche se tutti i gruppi di replica tranne uno vengono replicati correttamente, lo stato del collegamento viene impostato su ridotto o non riuscito, perché un gruppo di replica non riesce a completare la replica nel numero specificato di tentativi. Per informazioni sulle soglie di replica, vedere la sezione [Soglie di replica del database](../../../core/servers/manage/data-transfers-between-sites.md#BKMK_DBRepThresholds) nell'argomento [Trasferimenti di dati tra siti in System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md).  

 Utilizzare le informazioni nella tabella riportata di seguito per conoscere lo stato dei collegamenti di replica che potrebbero richiedere ulteriori indagini.  

|Descrizione del collegamento|Altre informazioni|  
|----------------------|----------------------|  
|**Il collegamento è attivo**|Non è stato rilevato alcun problema e la comunicazione nel collegamento è corrente.|  
|**Il collegamento è ridotto**|La replica ha funzionato, ma almeno una oggetto o gruppo di replica è in ritardo. Monitorare i collegamenti in questo stato e rivedere le informazioni da entrambi i siti sul collegamento per indicazioni sul possibile non funzionamento del collegamento.<br /><br /> Un collegamento può anche visualizzare lo stato di ridotto quando il sito che riceve i dati replicati non è in grado di confermare rapidamente i dati al database. Questa situazione può verificarsi quando si replicano grandi volumi di dati. Ad esempio, se si distribuisce un aggiornamento software in un numero elevato di computer, il sito padre sul collegamento potrebbe impiegare un po' di tempo per elaborare il volume di dati che vengono replicati. Un ritardo di elaborazione nel sito padre può portare all'impostazione dello stato del collegamento su ridotto fino a quando il sito padre non può elaborare correttamente il backlog di dati.|  
|**Il collegamento non è riuscito**|La replica non funziona. È possibile che un collegamento di replica possa essere ripristinato senza ulteriori azioni. È possibile utilizzare Replication Link Analyzer per analizzare e correggere la replica su questo collegamento.<br /><br /> Questo stato può anche indicare un problema con la rete fisica tra il sito padre e il sito figlio sul collegamento di replica.|  

 Mentre un sito padre sta per effettuare l'aggiornamento a un nuovo Service Pack e si visualizza lo stato del collegamento dal sito figlio, lo stato del collegamento viene visualizzato come attivo. Dopo l'aggiornamento, finché anche il sito figlio è nello stesso Service Pack del sito padre, lo stato del collegamento viene visualizzato come attivo se visualizzato dal sito padre e come in corso di configurazione se visualizzato dal sito figlio.  

####  <a name="BKMK_MonitorReplicationStatus"></a> Stato della replica  
 È possibile utilizzare il nodo **Replica di database** nell'area di lavoro **Monitoraggio** per visualizzare lo stato della replica per un collegamento di replica e i dettagli relativi al database del sito su ciascun sito nel collegamento di replica. È anche possibile visualizzare i dettagli relativi ai gruppi di replica. Per visualizzare i dettagli, selezionare un collegamento di replica e selezionare la scheda appropriata per lo stato di replica che si desidera visualizzare. Di seguito vengono fornite informazioni dettagliate sulle diverse schede per lo stato della replica.  

 **Riepilogo**  
 Visualizza informazioni di alto livello sulla replica dei dati del sito e i dati globali tra i due siti su un collegamento.  

 È inoltre possibile fare clic su **Visualizza report per la cronologia dei dati di traffico** per visualizzare un report con i dettagli relativi alla larghezza di banda di rete utilizzata dalla replica nel collegamento di replica.  

 **Sito padre**  
 Per il sito padre su un collegamento di replica, visualizzare i dettagli sul database, che includono:  

-   Porte del firewall per SQL Server  

-   Spazio libero su disco  

-   Percorsi dei file del database  

-   Certificati  

**Sito figlio**  
 Per il sito figlio su un collegamento di replica, visualizzare i dettagli sul database, che includono:  

-   Porte del firewall per SQL Server  

-   Spazio libero su disco  

-   Percorsi dei file del database  

-   Certificati  

**Dettaglio di inizializzazione**    
 Visualizzare lo stato di inizializzazione per i gruppi di replica che vengono replicati nel collegamento di replica. Queste informazioni consentono di identificare quando l'inizializzazione dei dati di replica è in corso o ha avuto esito negativo.  

 Inoltre, è possibile utilizzare queste informazioni per identificare quando un sito potrebbe essere in modalità di interoperabilità. La modalità di interoperabilità si verifica quando il sito figlio non esegue la stessa versione di Configuration Manager del sito padre.  

**Dettaglio di replica**    
 Visualizzare lo stato della replica per ciascun gruppo di replica che replica tramite il collegamento. Utilizzare queste informazioni per individuare i problemi o i ritardi nella replica di dati specifici, nonché per determinare le soglie di replica di database appropriate per il collegamento. Per informazioni sulle soglie di replica del database, vedere la sezione [Soglie di replica del database](../../../core/servers/manage/data-transfers-between-sites.md#BKMK_DBRepThresholds) nell'argomento [Trasferimenti di dati tra siti in System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md).  

> [!TIP]  
>  I gruppi di replica per i dati del sito vengono inviati solo dal sito figlio al sito padre. I gruppi di replica per i dati globali vengono replicati in entrambe le direzioni.  

###  <a name="BKMK_RLA"></a> Informazioni su Replication Link Analyzer  
 Configuration Manager include **Replication Link Analyzer** che consente di analizzare e risolvere i problemi di replica. Se la replica non riesce oppure si interrompe ma non viene segnalato l'errore è possibile utilizzare Replication Link Analyzer per monitorare e aggiornare errori nei collegamenti di replica. Replication Link Analyzer può essere usato per risolvere i problemi di replica tra i seguenti computer nella gerarchia di Configuration Manager (la direzione dell'errore di replica non è rilevante):  

-   Tra un server del sito e il server di database del sito.  

-   Tra un server di database del sito per i siti e un altro computer del database del sito per i siti (replica tra siti).  

È possibile eseguire Replication Link Analyzer sia nella console di Configuration Manager che al prompt dei comandi:  

-   Per l'esecuzione nella console di Configuration Manager: Nell'area di lavoro **Monitoraggio** fare clic sul nodo **Replica di database**, selezionare il collegamento di replica da analizzare e quindi nel gruppo **Replica di database** della scheda **Home** selezionare **Replication Link Analyzer**.  

-   Per l'esecuzione al prompt dei comandi, digitare il seguente comando: **%path%\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManager.ReplicationLinkAnalyzer.Wizard.exe &lt;FQDN server sito di origine\> &lt;FQDN server sito di destinazione\>**  

Quando si esegue Replication Link Analyzer, vengono rilevati eventuali problemi mediante una serie di controlli e regole diagnostiche. Quando questo strumento viene eseguito, è possibile visualizzare i problemi identificati. Se le istruzioni per risolvere il problema sono disponibili, vengono visualizzate. Se Replication Link Analyzer è in grado di monitorare e aggiornare automaticamente un problema, l'utente visualizza tale opzione. Al completamento dell'esecuzione di Replication Link Analyzer, i risultati vengono salvati nel seguente report basato su XML e in un file di log sul desktop dell'utente che esegue lo strumento:  

-   ReplicationAnalysis.xml  

-   ReplicationLinkAnalysis.log  

Durante il monitoraggio e l'aggiornamento dei problemi, Replication Link Analyzer interrompe i seguenti servizi e, al termine del monitoraggio e dell'aggiornamento, li riavvia:  

-   SMS_SITE_COMPONENT_MANAGER  

-   SMS_EXECUTIVE  

In caso di errori nel monitoraggio e nell'aggiornamento dei problemi, esaminare il server del sito e riavviare i servizi eventualmente interrotti.  

Le azioni di monitoraggio, aggiornamento e rilevamento con e senza errori vengono registrate per fornire dettagli aggiuntivi non presenti nell'interfaccia dello strumento.  

**Prerequisiti per l'uso di Replication Link Analyzer**  

-   L'account utilizzato per eseguire Replication Link Analyzer deve disporre dei diritti di amministratore locale in ciascun computer interessato dal collegamento di replica. L'account non richiede un ruolo di sicurezza di amministrazione basato su ruoli specifico. Un utente amministratore che dispone delle autorizzazioni di accesso al nodo **Replica di database** è pertanto in grado di eseguire lo strumento nella console di Configuration Manager. In alternativa, un amministratore di sistema che dispone di diritti sufficienti per ciascun computer è in grado di eseguire lo strumento al prompt dei comandi.  

-   L'account utilizzato per eseguire Replication Link Analyzer deve disporre dei diritti di amministratore di sistema in ciascun database SQL Server interessato dal collegamento di replica.  

**Problemi noti di Replication Link Analyzer**  

-   Con la versione 1511 di System Center Configuration Manager, Replication Link Analyzer genera errori relativi al certificato SQL Server Service Broker per i siti primari aggiornati da System Center 2012 Configuration Manager. Ciò è dovuto a modifiche apportate ai nomi dei certificati introdotte con la versione 1511 per i quali Replication Link Analyzer non è ancora stato aggiornato. È possibile ignorare questi errori.  

###  <a name="BKMK_ProcsforMonitoringReplication"></a> Procedure per il monitoraggio della replica dei database  

##### <a name="to-monitor-high-level-site-to-site-database-replication-status"></a>Per monitorare a livello generale lo stato della replica del database da sito a sito    
1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** fare clic su **Gerarchia siti** per aprire la visualizzazione **Diagramma gerarchia** .  

3.  Lasciare brevemente il puntatore del mouse sulla riga tra i due siti al fine di visualizzare lo stato della replica dei dati del sito e globali per i siti.  

##### <a name="to-monitor-the-replication-status-for-a-replication-link"></a>Per monitorare lo stato della replica per un collegamento di replica    
1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** fare clic su **Replica di database**, quindi selezionare il collegamento di replica per il collegamento da monitorare. Quindi, nell'area di lavoro, selezionare la scheda appropriata per visualizzare diversi dettagli relativi allo stato della replica per il collegamento.  

---
title: Versioni di SQL Server supportate
titleSuffix: Configuration Manager
description: Requisiti di configurazione e della versione di SQL Server per l'hosting di un database del sito di System Center Configuration Manager.
ms.custom: na
ms.date: 12/18/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
caps.latest.revision: 
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 82df06873449d538b7efbe414a451d746d48e11f
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2018
---
# <a name="supported-sql-server-versions-for-system-center-configuration-manager"></a>Versioni di SQL Server supportate per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Ogni sito di System Center Configuration Manager richiede una versione e una configurazione di SQL Server supportate per ospitare il database del sito.  

##  <a name="bkmk_Instances"></a> Istanze e percorsi di SQL Server  
 **Sito di amministrazione centrale e siti primari:**  
Il database del sito deve usare un'installazione completa di SQL Server.  

 SQL Server può trovarsi:  

-   Nel computer del server del sito.  
-   In un computer remoto rispetto al server del sito.  

Sono supportate le istanze seguenti:  

-   Istanza predefinita o denominata di SQL Server.  
-   Configurazioni a più istanze.  
-   Cluster SQL Server. Vedere [Usare un cluster SQL Server per ospitare il database del sito](../../../core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md).
-   Gruppo di disponibilità SQL Server AlwaysOn. Questa opzione richiede Configuration Manager 1602 o versione successiva. Per informazioni dettagliate, vedere [SQL Server AlwaysOn per database del sito a disponibilità elevata per System Center Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).


 **Siti secondari:**  
 Il database del sito può usare l'istanza predefinita di un'installazione completa di SQL Server o SQL Server Express.  

 È necessario che SQL Server si trovi nel computer del server del sito.  

 **Limitazioni al supporto**   
 Le configurazioni seguenti non sono supportate:
 -   Un cluster SQL Server in una configurazione cluster Bilanciamento carico di rete (NLB)
 -   Un cluster SQL Server cluster in un Volume condiviso cluster
 -   La tecnologia di mirroring e la replica peer-to-peer del database di SQL Server

La replica transazionale di SQL Server è supportata solo per la replica di oggetti ai punti di gestione configurati per l'uso delle [repliche di database](https://technet.microsoft.com/library/mt608546.aspx).  

##  <a name="bkmk_SQLVersions"></a> Versioni supportate di SQL Server  
 In una gerarchia con più siti, diversi siti possono usare versioni diverse di SQL Server per ospitare il database del sito se si verificano le condizioni seguenti:
 -  Configuration Manager supporta le versioni di SQL Server usate.
 -  Le versioni di SQL Server usate sono supportate da Microsoft.
 -  SQL Server supporta la replica tra le due versioni di SQL Server.  Ad esempio, [SQL Server non supporta la replica tra SQL Server 2008 R2 e SQL Server 2016](https://docs.microsoft.com/sql/relational-databases/replication/deprecated-features-in-sql-server-replication).



 Se non specificato diversamente, le versioni seguenti di SQL Server sono supportate con tutte le versioni attive di System Center Configuration Manager. Se viene aggiunto il supporto per una nuova versione di SQL Server o del Service Pack, verrà indicata la versione di Configuration Manager che aggiunge tale supporto. Analogamente, se il supporto è deprecato, cercare i dettagli relativi alle versioni di Configuration Manager interessate.   

Il supporto per un Service Pack di SQL Server specifico include gli aggiornamenti cumulativi, a meno che non interrompano la compatibilità con la versione di base del Service Pack. Quando non è indicata alcuna versione del Service Pack, il supporto si intende per la versione di SQL Server senza Service Pack. Se in futuro viene rilasciato un Service Pack per la versione di SQL Server, verrà dichiarata un'istruzione di supporto separata prima che sia supportata la nuova versione del Service Pack.


> [!IMPORTANT]  
>  Se si usa SQL Server Standard per il database nel sito di amministrazione centrale, si limita il numero totale di client che una gerarchia può supportare. Vedere [Numeri di ridimensionamento e scalabilità](../../../core/plan-design/configs/size-and-scale-numbers.md).

### <a name="sql-server-2017-standard-enterprise"></a>SQL Server 2017: Standard, Enterprise  
È possibile usare questa versione di SQL Server con almeno la [versione dell'aggiornamento cumulativo 2](https://support.microsoft.com/help/4052574), a partire da [Configuration Manager versione 1710](https://docs.microsoft.com/en-us/sccm/core/plan-design/changes/whats-new-in-version-1710) per i siti seguenti: 

-   sito di amministrazione centrale  
-   sito primario  
-   sito secondario  
<!--SMS.498506-->

### <a name="sql-server-2016-sp1-standard-enterprise"></a>SQL Server 2016 SP1 - Standard, Enterprise  
È possibile usare questa versione di SQL Server senza una versione dell'aggiornamento cumulativo minima per i siti seguenti:  

-   sito di amministrazione centrale  
-   sito primario  
-   sito secondario  

### <a name="sql-server-2016-standard-enterprise"></a>SQL Server 2016 - Standard, Enterprise  
È possibile usare questa versione di SQL Server senza una versione dell'aggiornamento cumulativo minima per i siti seguenti:  

-   sito di amministrazione centrale  
-   sito primario  
-   sito secondario  


### <a name="sql-server-2014-sp2-standard-enterprise"></a>SQL Server 2014 SP2 - Standard, Enterprise  
È possibile usare questa versione di SQL Server senza una versione dell'aggiornamento cumulativo minima per i siti seguenti:  

-   sito di amministrazione centrale  
-   sito primario  
-   sito secondario

### <a name="sql-server-2014-sp1-standard-enterprise"></a>SQL Server 2014 SP1 - Standard, Enterprise  
 È possibile usare questa versione di SQL Server senza una versione dell'aggiornamento cumulativo minima per i siti seguenti:  

-   sito di amministrazione centrale  
-   sito primario  
-   sito secondario

### <a name="sql-server-2012-sp4-standard-enterprise"></a>SQL Server 2012 SP4: Standard, Enterprise  
 È possibile usare questa versione di SQL Server senza una versione dell'aggiornamento cumulativo minima per i siti seguenti:  

-   sito di amministrazione centrale  
-   sito primario  
-   sito secondario  

### <a name="sql-server-2012-sp3-standard-enterprise"></a>SQL Server 2012 SP3 - Standard, Enterprise  
 È possibile usare questa versione di SQL Server senza una versione dell'aggiornamento cumulativo minima per i siti seguenti:  

-   sito di amministrazione centrale  
-   sito primario  
-   sito secondario  

<!-- Support for this service pack version has been dropped by Microsoft    
### SQL Server 2012 SP2: Standard, Enterprise   
 You can use this version of SQL Server with no minimum cumulative update version for the following sites:  

-   A central administration site  
-   A primary site  
-   A secondary site  
-->

### <a name="sql-server-2008-r2-sp3-standard-enterprise-datacenter"></a>SQL Server 2008 R2 SP3 - Standard, Enterprise, Datacenter     
  Questa versione di SQL Server non è supportata [a partire dalla versione 1702](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-support-for-sql-server-versions-as-a-site-database).  
 Rimane supportata quando si usa una versione di Configuration Manager precedente la 1702.

Quando è supportata dalla versione di Configuration Manager, questa versione di SQL Server può essere usata senza una versione dell'aggiornamento cumulativo minima per i siti seguenti:  

-   sito di amministrazione centrale  
-   sito primario
-   sito secondario

### <a name="sql-server-2017-express"></a>SQL Server 2017 Express   
È possibile usare questa versione di SQL Server con almeno la [versione dell'aggiornamento cumulativo 2](https://support.microsoft.com/help/4052574), a partire da [Configuration Manager versione 1710](https://docs.microsoft.com/en-us/sccm/core/plan-design/changes/whats-new-in-version-1710) per i siti seguenti:
-   sito secondario
<!--SMS.498506-->

### <a name="sql-server-2016-express-sp1"></a>SQL Server 2016 Express SP1  
È possibile usare questa versione di SQL Server senza una versione dell'aggiornamento cumulativo minima per i siti seguenti:
-   sito secondario

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express
È possibile usare questa versione di SQL Server senza una versione dell'aggiornamento cumulativo minima per i siti seguenti:
-   sito secondario


### <a name="sql-server-2014-express-sp2"></a>SQL Server 2014 Express SP2   
È possibile usare questa versione di SQL Server senza una versione dell'aggiornamento cumulativo minima per i siti seguenti:  

-   sito secondario  


### <a name="sql-server-2014-express-sp1"></a>SQL Server 2014 Express SP1   
 È possibile usare questa versione di SQL Server senza una versione dell'aggiornamento cumulativo minima per i siti seguenti:  

-   sito secondario  

### <a name="sql-server-2012-express-sp3"></a>SQL Server 2012 Express SP3  
È possibile usare questa versione di SQL Server senza una versione dell'aggiornamento cumulativo minima per i siti seguenti:  

-   sito secondario  

<!-- Support for this service pack version has been dropped by Microsoft   
### SQL Server 2012 Express SP2   
 You can use this version of SQL Server with no minimum cumulative update version for the following sites:  

-   A secondary site  
-->


##  <a name="bkmk_SQLConfig"></a> Configurazioni necessarie per SQL Server  
 Le configurazioni seguenti sono necessarie per tutte le installazioni di SQL Server usate per un database del sito, incluso SQL Server Express. Quando Configuration Manager installa SQL Server Express come parte dell'installazione di un sito secondario, queste configurazioni vengono create automaticamente.  

 **Versione dell'architettura di SQL Server:**  
 Configuration Manager richiede una versione a 64 bit di SQL Server per ospitare il database del sito.  

 **Regole di confronto del database:**  
 In ogni sito sia l'istanza di SQL Server usata per il sito che il database del sito devono usare le regole di confronto seguenti: **SQL_Latin1_General_CP1_CI_AS**.  

 Configuration Manager supporta due eccezioni a queste regole di confronto per rispettare gli standard definiti in GB18030 per l'uso in Cina. Per altre informazioni, vedere [Supporto internazionale in System Center Configuration Manager](../../../core/plan-design/hierarchy/international-support.md).  

 **Livello di compatibilità database:** </br>
 Configuration Manager richiede un livello di compatibilità per il database del sito non inferiore alla versione minima di SQL Server supportata per la versione di Configuration Manager. Ad esempio, a partire dalla versione 1702, è necessario avere un [livello di compatibilità del database](https://docs.microsoft.com/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database) maggiore o uguale a 110. <!-- SMS.506266--> 

 **Funzionalità di SQL Server:**  
 Solo la funzionalità **Servizi Motore di database** è necessaria per ogni server del sito.  

 La replica di database di Configuration Manager non richiede la funzionalità di **replica di SQL Server**. Questa configurazione di SQL Server, tuttavia, è necessaria se si usano [repliche di database per i punti di gestione per System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Autenticazione di Windows:**  
 Configuration Manager richiede l' **autenticazione di Windows** per convalidare le connessioni al database.  

 **Istanza di SQL Server:**  
 È necessario usare un'istanza dedicata di SQL Server per ogni sito. L'istanza può essere un'**istanza denominata** o un'**istanza predefinita**.  

 **Memoria di SQL Server:**  
 Riservare la memoria per SQL Server usando SQL Server Management Studio e l'impostazione **Memoria minima per il server** in **Opzioni per la memoria del server**. Per altre informazioni su come impostare una quantità fissa di memoria, vedere [Procedura: Impostazione di una quantità di memoria fissa (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759).  

-   **Per un server di database che viene installato nello stesso computer del server del sito**: limitare la memoria per SQL Server al 50-80% della memoria di sistema indirizzabile disponibile.  

-   **Per un server di database dedicato (remoto dal server del sito)**: limitare la memoria per SQL Server all'80-90% della memoria di sistema indirizzabile disponibile.  

-   **Per una riserva di memoria per il pool di buffer di ogni istanza di SQL Server in uso:**  

    -   Per un sito di amministrazione centrale, impostare almeno 8 gigabyte (GB).  
    -   Per un sito primario, impostare almeno 8 gigabyte (GB).  
    -   Per un sito secondario, impostare almeno 4 gigabyte (GB).  

**Trigger nidificati SQL:**  
 I[trigger nidificati SQL](http://go.microsoft.com/fwlink/?LinkId=528802) devono essere abilitati.  

 **Integrazione CLR di SQL Server**  
  Il database del sito richiede l'abilitazione di Common Language Runtime (CLR) di SQL Server. Questa funzione viene abilitata automaticamente quando si installa Configuration Manager. Per altre informazioni su CLR, vedere [Introduzione all'integrazione CLR di SQL Server](https://msdn.microsoft.com/library/ms254498\(v=vs.110\).aspx).  

##  <a name="bkmk_optional"></a> Configurazioni facoltative per SQL Server  
 Le configurazioni seguenti sono facoltative per ogni database che usa un'installazione completa di SQL Server.  

 **Servizio SQL Server:**  
 È possibile configurare il servizio SQL Server per l'esecuzione con:  

-   Un account *utente di dominio con diritti limitati*:  

    -   È una procedura ottimale che potrebbe rendere necessario configurare manualmente il nome dell'entità servizio (SPN) per l'account.  

-   L'account **sistema locale** del computer in cui viene eseguito SQL Server:  

    -   Usare l'account sistema locale per semplificare il processo di configurazione.  
    -   Quando si usa l'account sistema locale, Configuration Manager registra automaticamente il nome SPN per il servizio SQL Server.  
    -   Tenere presente che l’uso dell'account di sistema locale per il servizio SQL Server non è una procedura consigliata di SQL Server.  

Se il computer che esegue SQL Server non usa il proprio account di sistema locale per eseguire il servizio di SQL Server, è necessario configurare il nome dell'entità servizio (SPN) dell'account che esegue il servizio di SQL Server in Servizi di dominio Active Directory. Se viene usato l'account di sistema, il nome dell'entità servizio viene registrato automaticamente.

Per informazioni sui nomi dell'entità servizio per il database del sito, vedere [Gestire il nome dell'entità servizio (SPN) per il server di database del sito](../../../core/servers/manage/modify-your-infrastructure.md#bkmk_SPN) nell'articolo [Modificare l'infrastruttura di System Center Configuration Manager](../../../core/servers/manage/modify-your-infrastructure.md).  

Per informazioni su come modificare l'account usato dal servizio di SQL Server, vedere [Procedura: Modifica dell'account di avvio del servizio di SQL Server (Gestione configurazione SQL Server)](http://go.microsoft.com/fwlink/p/?LinkId=237661).  

**SQL Server Reporting Services:**  
SQL Server Reporting Services è necessario per l'installazione di un punto di Reporting Services che consente di eseguire report.  

> [!IMPORTANT]  
> Dopo aver aggiornato SQL Server da una versione precedente, potrebbe essere visualizzato l'errore seguente: *Report Builder Does Not Exist* (Generatore report inesistente).    
> Per risolvere questo errore è necessario reinstallare il ruolo del sistema del sito del punto di Reporting Services.

**Porte di SQL Server:**  
Per la comunicazione con il motore di database di SQL Server e per la replica tra siti, è possibile usare le configurazioni di porte SQL Server predefinite o specificare porte personalizzate:  

-   Le **comunicazioni tra siti** usano SQL Server Service Broker, che per impostazione predefinita usa la porta TCP 4022.  
-   Le **comunicazioni all'interno del sito** tra il motore di database SQL Server e i diversi ruoli del sistema del sito di Configuration Manager usano per impostazione predefinita la porta TCP 1433. I ruoli del sistema del sito seguenti comunicano direttamente con il database di SQL Server:  

    -   Punto di gestione  
    -   Computer del provider SMS  
    -   Punto di Reporting Services  
    -   Server del sito  

Se un computer che esegue SQL Server ospita un database da più di un sito, ogni database deve usare un'istanza separata di SQL Server e ogni istanza deve essere configurata con un set univoco di porte.  

> [!WARNING]  
>  Configuration Manager non supporta porte dinamiche. Poiché per impostazione predefinita le istanze denominate di SQL Server usano le porte dinamiche per le connessioni al motore di database, quando si usa un'istanza denominata è necessario configurare manualmente la porta statica da usare per la comunicazione tra siti.  

Se si dispone di un firewall abilitato nel computer che esegue SQL Server, assicurarsi che sia configurato per consentire le porte usate dalla distribuzione e in tutti i percorsi della rete tra i computer che comunicano con SQL Server.  

Per un esempio di come configurare SQL Server per l'uso di una porta specifica, vedere [Procedura: Configurazione di un server per l'attesa su una porta TCP specifica (Gestione configurazione SQL Server)](http://go.microsoft.com/fwlink/p/?LinkID=226349) nella Libreria TechNet di SQL Server.  

## <a name="upgrade-options-for-sql-server"></a>Opzioni di aggiornamento per SQL Server
Se è necessario aggiornare la versione di SQL Server, è consigliabile seguire i metodi seguenti, dal più semplice al più complesso.
1. [Aggiornare SQL Server sul posto](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (scelta consigliata).
2. Installare una nuova versione di SQL Server in un nuovo computer e quindi [usare l'opzione di spostamento del database](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) dell'installazione di Configuration Manager in modo che il server del sito punti alla nuova versione di SQL Server.
3. Usare le funzionalità di [backup e ripristino](/sccm/protect/understand/backup-and-recovery).

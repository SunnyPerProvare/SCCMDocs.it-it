---
title: Supporto per SQL Server | System Center Configuration Manager
description: Requisiti di configurazione e della versione di SQL Server per l'hosting di un database del sito di System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35e237b6-9f7b-4189-90e7-8eca92ae7d3d
caps.latest.revision: 21
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b17720021f797d404a89933939427696dfafd7dc


---
# <a name="support-for-sql-server-versions-for-system-center-configuration-manager"></a>Supporto per le versioni di SQL Server per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Ogni sito di System Center Configuration Manager richiede una versione e una configurazione di SQL Server supportate per ospitare il database del sito.  

##  <a name="a-namebkmkinstancesa-sql-server-instances-and-locations"></a><a name="bkmk_Instances"></a> Istanze e percorsi di SQL Server  
 **Sito di amministrazione centrale e siti primari:**  

Il database del sito deve usare un'installazione completa di SQL Server.  

 Il percorso di SQL Server può trovarsi in:  

-   Il computer del server del sito  
-   Un computer remoto dal server del sito  

Sono supportate le istanze seguenti:  

-   Istanza predefinita o denominata di SQL Server  
-   Configurazioni di più istanze  
-   Cluster di SQL Server: vedere [Usare un cluster SQL Server per ospitare il database del sito](../../../core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database.md)
-   Gruppo di disponibilità SQL Server AlwaysOn: questa opzione richiede Configuration Manager 1602 o versione successiva. Per informazioni dettagliate, vedere [SQL Server AlwaysOn per database del sito a disponibilità elevata per System Center Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md)  

> [!NOTE]  
>  Un cluster SQL Server in una configurazione cluster Bilanciamento carico di rete (NLB) non è supportato. Inoltre, non sono supportate la tecnologia di mirroring e la replica peer-to-peer del database di SQL Server. La replica transazionale standard di SQL Server è supportata solo per la replica di oggetti ai punti di gestione che sono configurati per usare le [repliche di database](https://technet.microsoft.com/library/mt608546.aspx).  


 **Siti secondari:**  

 Il database del sito può usare l'istanza predefinita di un'installazione completa di SQL Server o SQL Server Express  

 Il percorso di SQL Server deve trovarsi nel computer server del sito  

##  <a name="a-namebkmksqlversionsa-supported-versions-of-sql-server"></a><a name="bkmk_SQLVersions"></a> Versioni supportate di SQL Server  
 In una gerarchia con più siti, diversi siti possono usare versioni diverse di SQL Server per ospitare il database del sito, purché le versioni di SQL Server in uso siano supportate da Configuration Manager.  

 Le versioni seguenti di SQL Server sono supportate con System Center Configuration Manager versione 1511 e successive.  

> [!IMPORTANT]  
>  L'uso di SQL Server Standard per il database nel sito di amministrazione centrale limita il numero totale di client che una gerarchia può supportare. Vedere [Numeri di ridimensionamento e scalabilità](../../../core/plan-design/configs/size-and-scale-numbers.md).

### <a name="sql-server-2016---standard-enterprise"></a>SQL Server 2016 - Standard, Enterprise  

Supportato per la versione 1606.   
È possibile usare questa versione di SQL Server senza una versione di aggiornamento cumulativo minima per i seguenti elementi:  

-   Sito di amministrazione centrale  
-   Sito primario  
-   Sito secondario  


### <a name="sql-server-2014-sp2---standard-enterprise"></a>SQL Server 2014 SP2 - Standard, Enterprise  

Supportato per la versione 1511 e versioni successive.  
È possibile usare questa versione di SQL Server senza una versione di aggiornamento cumulativo minima per i seguenti elementi:  

-   Sito di amministrazione centrale  
-   Sito primario  
-   Sito secondario  



### <a name="sql-server-2014-sp1---standard-enterprise"></a>SQL Server 2014 SP1 - Standard, Enterprise  

Supportato per la versione 1511 e versioni successive.  
 È possibile usare questa versione di SQL Server senza una versione di aggiornamento cumulativo minima per i seguenti elementi:  

-   Sito di amministrazione centrale  
-   Sito primario  
-   Sito secondario  


### <a name="sql-server-2012-sp3---standard-enterprise"></a>SQL Server 2012 SP3 - Standard, Enterprise  

Supportato per la versione 1511 e versioni successive.  
 È possibile usare questa versione di SQL Server senza una versione di aggiornamento cumulativo minima per i seguenti elementi:  

-   Sito di amministrazione centrale  
-   Sito primario  
-   Sito secondario  


### <a name="sql-server-2012-sp2---standard-enterprise"></a>SQL Server 2012 SP2 - Standard, Enterprise  

Supportato per la versione 1511 e versioni successive.  
 È possibile usare questa versione di SQL Server senza una versione di aggiornamento cumulativo minima per i seguenti elementi:  

-   Sito di amministrazione centrale  
-   Sito primario  
-   Sito secondario  


### <a name="sql-server-2008-r2-sp3---standard-enterprise-datacenter"></a>SQL Server 2008 R2 SP3 - Standard, Enterprise, Datacenter  

Supportato per la versione 1511 e versioni successive.    
È possibile usare questa versione di SQL Server senza una versione di aggiornamento cumulativo minima per i seguenti elementi:  

-   Sito di amministrazione centrale  
-   Sito primario  
-   Sito secondario  

### <a name="sql-server-2016-express"></a>SQL Server 2016 Express
Supportato per la versione 1606.  
È possibile usare questa versione di SQL Server senza una versione di aggiornamento cumulativo minima per i seguenti elementi:
-   Sito secondario

### <a name="sql-server-2014-express-sp2"></a>SQL Server 2014 Express SP2  
Supportato per la versione 1511 e versioni successive.  
È possibile usare questa versione di SQL Server senza una versione di aggiornamento cumulativo minima per i seguenti elementi:  

-   Sito secondario  


### <a name="sql-server-2014-express-sp1"></a>SQL Server 2014 Express SP1  
 Supportato per la versione 1511 e versioni successive.   
 È possibile usare questa versione di SQL Server senza una versione di aggiornamento cumulativo minima per i seguenti elementi:  

-   Sito secondario  

### <a name="sql-server-2012-express-sp3"></a>SQL Server 2012 Express SP3  
Supportato per la versione 1511 e versioni successive.   
È possibile usare questa versione di SQL Server senza una versione di aggiornamento cumulativo minima per i seguenti elementi:  

-   Sito secondario  

### <a name="sql-server-2012-express-sp2"></a>SQL Server 2012 Express SP2  
 Supportato per la versione 1511 e versioni successive.  
 È possibile usare questa versione di SQL Server senza una versione di aggiornamento cumulativo minima per i seguenti elementi:  

-   Sito secondario  

##  <a name="a-namebkmksqlconfiga-required-configurations-for-sql-server"></a><a name="bkmk_SQLConfig"></a> Configurazioni necessarie per SQL Server  
 Quanto segue è richiesto per tutte le installazioni di SQL Server usate per un database del sito, incluso SQL Server Express. Quando Configuration Manager installa SQL Server Express come parte dell'installazione del sito secondario, queste configurazioni vengono eseguite automaticamente.  

 **Versione dell'architettura di SQL Server:**  
 Configuration Manager richiede una versione a 64 bit di SQL Server per ospitare il database del sito.  

 **Regole di confronto del database:**  
 In ogni sito sia l'istanza di SQL Server usata per il sito che il database del sito devono usare le regole di confronto seguenti: **SQL_Latin1_General_CP1_CI_AS**.  

 Configuration Manager supporta due eccezioni a queste regole di confronto per rispettare gli standard definiti in GB18030 per l'uso in Cina. Per altre informazioni, vedere [Supporto internazionale in System Center Configuration Manager](../../../core/plan-design/hierarchy/international-support.md).  

 **Funzionalità di SQL Server:**  
 Solo la funzionalità **Servizi Motore di database** è necessaria per ogni server del sito.  

 La replica di database di Configuration Manager non richiede la funzionalità di **replica di SQL Server**. Tuttavia, questa configurazione di SQL Server è necessaria se si utilizzano le [Repliche di database per i punti di gestione per System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

 **Autenticazione di Windows:**  
 Configuration Manager richiede l' **autenticazione di Windows** per convalidare le connessioni al database.  

 **Istanza di SQL Server:**  
 È necessario usare un'istanza dedicata di SQL Server per ogni sito. Può trattarsi di un **istanza denominata** o **istanza predefinita**.  

 **Memoria di SQL Server:**  
 Riservare la memoria per SQL Server usando SQL Server Management Studio e l'impostazione **Memoria minima per il server** in **Opzioni per la memoria del server**. Per altre informazioni su come impostare una quantità fissa di memoria, vedere [Procedura: Impostazione di una quantità di memoria fissa (SQL Server Management Studio)](http://go.microsoft.com/fwlink/p/?LinkId=233759).  

-   **Server di database che viene installato nello stesso computer del server del sito** : limitare la memoria per SQL Server al 50-80% della memoria di sistema indirizzabile disponibile.  

-   **Server di database dedicato (remoto dal server del sito)** : limitare la memoria per SQL Server all'80-90% della memoria di sistema indirizzabile disponibile.  

-   **La riserva di memoria per il pool di buffer di ogni istanza di SQL Server in uso:**  

    -   Sito di amministrazione centrale: minimo 8 gigabyte (GB)  
    -   Sito primario: minimo 8 gigabyte (GB)  
    -   Sito secondario: minimo 4 gigabyte (GB)  

 **Trigger nidificati SQL:**  

 I[trigger nidificati SQL](http://go.microsoft.com/fwlink/?LinkId=528802) devono essere abilitati.  

 **Integrazione CLR di SQL Server**  

  Il database del sito richiede l'abilitazione di Common Language Runtime (CLR) di SQL Server. Questa funzione viene abilitata automaticamente quando si installa Configuration Manager. Per altre informazioni su CLR, vedere [Introduzione all'integrazione CLR di SQL Server](https://msdn.microsoft.com/library/ms254498\(v=vs.110\).aspx)  

##  <a name="a-namebkmkoptionala-optional-configurations-for-sql-server"></a><a name="bkmk_optional"></a> Configurazioni facoltative per SQL Server  
 Le configurazioni seguenti sono facoltative per ogni database che usa un'installazione completa di SQL Server.  

 **Servizio SQL Server:**  
 È possibile configurare il servizio SQL Server per l'esecuzione con:  

-   Account**utente locale di dominio** :  

    -   È una procedura ottimale che potrebbe rendere necessario configurare manualmente il nome dell'entità servizio (SPN) per l'account.  

-   Account**sistema locale** del computer in cui viene eseguito SQL Server:  

    -   Usare l'account sistema locale per semplificare il processo di configurazione.  
    -   Quando si usa l'account sistema locale, Configuration Manager registra automaticamente il nome SPN per il servizio SQL Server.  
    -   Tenere presente che l’uso dell'account di sistema locale per il servizio SQL Server non è una procedura consigliata di SQL Server.  

Quando SQL Server non usa tale account di sistema locale del computer per eseguire i servizi di SQL Server, è necessario configurare il nome dell'entità servizio (SPN) dell'account che esegue servizi di SQL Server in Servizi di dominio Active Directory. Quando viene usato l'account di sistema, il nome dell'entità servizio viene automaticamente registrato per l'utente.

Per informazioni sui nomi dell'entità servizio per il database del sito, vedere  [Manage the SPN for the site database server](../../../core/servers/manage/modify-your-infrastructure.md#bkmk_SPN) nell'argomento [Modify your System Center Configuration Manager infrastructure](../../../core/servers/manage/modify-your-infrastructure.md) .  

Per informazioni su come modificare l'account usato dal servizio SQL, vedere [Procedura: Modifica dell'account di avvio del servizio di SQL Server (Gestione configurazione SQL Server)](http://go.microsoft.com/fwlink/p/?LinkId=237661).  

**SQL Server Reporting Services:**  
Necessario per installare un punto di Reporting Services che consente di eseguire i report.  

**Porte di SQL Server:**  
Per la comunicazione con il motore di database di SQL Server e per la replica tra siti, è possibile usare le configurazioni di porte SQL Server predefinite o specificare porte personalizzate:  

-   Le**comunicazioni tra siti** usano SQL Server Service Broker, che per impostazione predefinita usa la porta TCP 4022.  
-   La**comunicazione nei siti** tra il motore di database di SQL Server e i diversi ruoli del sistema del sito di Configuration Manager usa la porta TCP 1433 per impostazione predefinita. I ruoli del sistema del sito seguenti comunicano direttamente con il database di SQL Server:  

    -   Punto di gestione  
    -   Computer del provider SMS  
    -   Punto di Reporting Services  
    -   Server del sito  

Se SQL Server ospita un database da più di un sito, ogni database deve usare un'istanza separata di SQL Server e ogni istanza deve essere configurata con un set univoco di porte.  

> [!WARNING]  
>  Configuration Manager non supporta le porte dinamiche. Poiché per impostazione predefinita le istanze denominate di SQL Server usano le porte dinamiche per le connessioni al motore di database, quando si usa un'istanza denominata è necessario configurare manualmente la porta statica da usare per la comunicazione tra siti.  

Se si dispone di un firewall abilitato nel computer che esegue SQL Server, assicurarsi che sia configurato per consentire le porte usate dalla distribuzione e in tutti i percorsi della rete tra i computer che comunicano con SQL Server.  

Per un esempio di come configurare SQL Server per l'uso di una porta specifica, vedere [Procedura: Configurazione di un server per l'attesa su una porta TCP specifica (Gestione configurazione SQL Server)](http://go.microsoft.com/fwlink/p/?LinkID=226349) nella Libreria TechNet di SQL Server.  



<!--HONumber=Nov16_HO1-->


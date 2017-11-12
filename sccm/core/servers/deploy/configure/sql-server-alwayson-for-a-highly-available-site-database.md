---
title: SQL Server Always On
titleSuffix: Configuration Manager
description: "Pianificare l'uso di un gruppo di disponibilità Always On di SQL Server con SCCM."
ms.custom: na
ms.date: 09/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
caps.latest.revision: "16"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 24eaa33f1f9b333894817f089149e2cbed35df75
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="prepare-to-use-sql-server-always-on-availability-groups-with-configuration-manager"></a>Preparare l'uso di gruppi di disponibilità Always On di SQL Server con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Preparare System Center Configuration Manager all'uso di gruppi di disponibilità Always On di SQL Server come soluzione di disponibilità elevata e ripristino di emergenza per il database del sito.  
Configuration Manager supporta l'uso di gruppi di disponibilità:
-     nei siti primari e nel sito di amministrazione centrale;
-     in locale o in Microsoft Azure.

Quando si usano i gruppi di disponibilità in Microsoft Azure, è possibile aumentare ulteriormente la disponibilità del database del sito con i *set di disponibilità di Azure*. Per altre informazioni sui set di disponibilità di Azure, vedere [Gestione della disponibilità delle macchine virtuali](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).

>  [!Important]   
>  Prima di continuare, acquisire familiarità con la configurazione di SQL Server e dei gruppi di disponibilità di SQL Server. Le informazioni seguenti fanno riferimento alla libreria della documentazione e alle procedure relative a SQL Server.

## <a name="supported-scenarios"></a>Scenari supportati
Di seguito sono riportati gli scenari supportati per l'uso di gruppi di disponibilità con Configuration Manager. Informazioni dettagliate e procedure per ogni scenario sono reperibili in [Configurare i gruppi di disponibilità per Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag).


-      [Creare un gruppo di disponibilità per l'uso con Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag#create-and-configure-an-availability-group).
-     [Configurare un sito per l'uso di un gruppo di disponibilità](/sccm/core/servers/deploy/configure/configure-aoag#configure-a-site-to-use-the-database-in-the-availability-group).
-     [Aggiungere e rimuovere i membri di una replica sincrona da un gruppo di disponibilità che ospita un database del sito](/sccm/core/servers/deploy/configure/configure-aoag#add-and-remove-synchronous-replica-members).
-     [Configurare le repliche con commit asincrono](/sccm/core/servers/deploy/configure/configure-aoag#configure-an-asynchronous-commit-repilca) (richiede Configuration Manager 1706 o versione successiva)
-     [Recuperare un sito da una replica con commit asincrono](/sccm/core/servers/deploy/configure/configure-aoag#use-the-asynchronous-replica-to-recover-your-site) (richiede Configuration Manager 1706 o versione successiva)
-     [Spostare un database del sito da un gruppo di disponibilità a un'istanza predefinita o denominata di SQL Server autonomo](/sccm/core/servers/deploy/configure/configure-aoag#stop-using-an-availability-group).


## <a name="prerequisites"></a>Prerequisiti
I prerequisiti seguenti si applicano a tutti gli scenari. Se a uno scenario si applicano prerequisiti aggiuntivi, i dettagli verranno forniti con lo scenario specifico.   

### <a name="configuration-manager-accounts-and-permissions"></a>Account e autorizzazioni di Configuration Manager
**Server del sito per l'accesso ai membri di replica:**   
L'account computer del server del sito deve essere un membro del gruppo **Administrators locale** in tutti i computer membri del gruppo di disponibilità.

### <a name="sql-server"></a>SQL Server
**Versione:**  
Ogni replica nel gruppo di disponibilità deve eseguire una versione di SQL Server supportata dalla versione in uso di Configuration Manager. Se supportati da SQL Server, nodi diversi di un gruppo di disponibilità possono eseguire versioni diverse di SQL Server.

**Edizione:**  
È necessario usare un'edizione *Enterprise* di SQL Server.

**Account:**  
Ogni istanza di SQL Server può essere eseguita con un account utente di dominio (**account del servizio**) o con un account non di dominio. Ogni replica in un gruppo può avere una configurazione diversa. Per le [procedure consigliate di SQL Server](/sql/sql-server/install/security-considerations-for-a-sql-server-installation#before-installing-includessnoversionincludesssnoversion-mdmd), usare un account con le autorizzazioni più restrittive possibili.

-   Per configurare gli account del servizio e le autorizzazioni per SQL Server 2016, vedere [Configurare account di servizio e autorizzazioni di Windows](/sql/database-engine/configure-windows/configure-windows-service-accounts-and-permissions) in MSDN.
-   Per usare un account non di dominio, sono necessari certificati. Per altre informazioni, vedere [Utilizzare certificati per un endpoint del mirroring del database (Transact-SQL)](https://docs.microsoft.com/sql/database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql).


Per altre informazioni vedere [Creare un endpoint del mirroring del database per i gruppi di disponibilità Always On](/sql/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell).

### <a name="availability-group-configurations"></a>Configurazioni dei gruppi di disponibilità
**Membri di replica:**  
-   Il gruppo di disponibilità deve avere una sola replica primaria.
-   Prima della versione 1706 erano consentite fino a due repliche secondarie sincrone.
-   A partire dalla versione 1706, in un gruppo di disponibilità è possibile usare lo stesso numero e tipo di repliche supportate dalla versione di SQL Server in uso.

-   A partire dalla versione 1706, per ripristinare la replica sincrona è possibile usare la replica con commit asincrono. Vedere le [opzioni di ripristino del database del sito]( /sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption) nell'argomento Backup e ripristino per informazioni su come eseguire questa operazione.
    > [!CAUTION]  
    > Configuration Manager non supporta il failover per l'uso della replica con commit asincrono come database del sito.
Poiché Configuration Manager non convalida lo stato della replica con commit asincrono per verificare che sia corrente, e [per comportamento normale del prodotto, una replica di questo tipo può non essere sincronizzata]( https://msdn.microsoft.com/library/ff877884(SQL.120).aspx(d=robot)#Availability%20Modes), l'uso di una replica con commit asincrono come database del sito può mettere a rischio l'integrità dei dati del sito.

Ogni membro di replica deve:
-   Usare l' **istanza predefinita**  
    *A partire dalla versione 1702 è possibile usare un'* ***istanza denominata***.

-     Avere il valore di **Connessioni nel ruolo primario** impostato su **Sì**
-     Avere il valore di **Secondario leggibile** impostato su **Sì**  
-     Essere impostate per il **failover manuale**      

    >  [!TIP]
    >  Configuration Manager supporta l'uso di repliche sincrone del gruppo di disponibilità se è stata scelta l'impostazione **Failover automatico**. Tuttavia **Failover manuale** deve essere impostato quando:
    >  -  Si esegue il programma di installazione per specificare l'uso del database del sito nel gruppo di disponibilità.
    >  -  Quando si installa un aggiornamento a Configuration Manager, non solo gli aggiornamenti applicabili al database del sito.  

**Percorso dei membri della replica:**  
Tutte le repliche in un gruppo di disponibilità devono essere ospitate in locale o in Microsoft Azure. Non sono supportati gruppi che includono un membro locale e un membro in Azure.     

Quando si imposta un gruppo di disponibilità in Azure e il gruppo si trova dietro un bilanciamento del carico interno o esterno, è necessario che le seguenti porte predefinite siano aperte per abilitare l'accesso del programma di installazione a ogni replica:   

-     Agente mapping endpoint RCP: **TCP 135**   
-     Server Message Block (SMB): **TCP 445**  
    *Dopo il trasferimento del database è possibile rimuovere questa porta. A partire dalla versione 1702, questa porta non è più necessaria.*
-     SQL Server Service Broker: **TCP 4022**
-     SQL su TCP: **TCP 1433**   

Al termine dell'installazione le porte seguenti devono restare accessibili:
-     SQL Server Service Broker: **TCP 4022**
-     SQL su TCP: **TCP 1433**

A partire dalla versione 1702 è possibile usare porte personalizzate per queste configurazioni. Le stesse porte devono essere usate dall'endpoint e in tutte le repliche nel gruppo di disponibilità.


**Listener:**   
Il gruppo di disponibilità deve avere almeno un **listener del gruppo di disponibilità**. Il nome virtuale di questo listener viene usato quando si configura Configuration Manager per usare il database del sito nel gruppo di disponibilità. Anche se un gruppo di disponibilità può contenere più listener, Configuration Manager può usarne solo uno. Per altre informazioni vedere [Creare o configurare un listener del gruppo di disponibilità (SQL Server)](/sql/database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server).

**Percorsi di file:**   
Quando si esegue installazione di Configuration Manager per configurare un sito per l'uso del database in un gruppo di disponibilità, ogni server di replica secondaria deve avere un percorso di file di SQL Server identico a quello dei file di database del sito nella replica primaria corrente.
-   Se non esiste un percorso identico, non sarà possibile aggiungere l'istanza per il gruppo di disponibilità come nuovo percorso del database del sito.
-   Inoltre l'account del servizio di SQL Server locale deve avere l'autorizzazione **Controllo completo** per questa cartella.

I server di replica secondaria richiedono questo percorso file solo durante l'installazione per specificare l'istanza di database nel gruppo di disponibilità. Dopo che l'installazione ha completato la configurazione del database del sito nel gruppo di disponibilità, è possibile eliminare il percorso non usato dai server di replica secondari.

Prendere ad esempio in considerazione i seguenti scenari:
-   Si crea un gruppo di disponibilità che usa tre server SQL.

-   Il server di replica primaria è una nuova installazione di SQL Server 2014. Per impostazione predefinita, i file MDF e LDF del database vengono archiviati in C:\Programmi\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\DATA.

-   Entrambi i server di replica secondaria sono stati aggiornati a SQL Server 2014 da versioni precedenti e continuano a usare il percorso di file originale per archiviare i file di database: C:\Programmi\Microsoft SQL Server\MSSQL10. MSSQLSERVER\MSSQL\DATA.

-   Prima di tentare di spostare il database del sito in questo gruppo di disponibilità, in ogni server di replica secondaria è necessario creare il seguente percorso di file, anche se le repliche secondarie non useranno questo percorso: C:\Programmi\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\DATA. Questo percorso è un duplicato del percorso usato nella replica primaria.

-   È quindi possibile concedere all'account del servizio SQL Server in ogni replica secondaria l'accesso con controllo completo al percorso di file appena creato nel server.

-   È ora possibile eseguire correttamente l'installazione di Configuration Manager per configurare il sito in modo che usi il database del sito nel gruppo di disponibilità.

**Configurare il database su una nuova replica:**   
 Il database di ogni replica deve essere impostato con i valori seguenti:
-   L'**integrazione con CLR** deve essere *abilitata*
-     **Max text repl size** deve essere *2147483647*
-     Il proprietario del database deve essere l'*account di amministratore di sistema*
-     **TRUSTWORTY** deve essere **ON**
-     **Service Broker** deve essere *abilitato*

È possibile creare queste configurazioni solo su una replica primaria. Per configurare una replica secondaria, è necessario prima eseguire il failover della replica primaria nella replica secondaria per far sì che la replica secondaria diventi la nuova replica primaria.   

Se necessario, consultare la documentazione di SQL Server per configurare le impostazioni. Ad esempio, vedere [TRUSTWORTHY](/sql/relational-databases/security/trustworthy-database-property) o [Integrazione con CLR](/sql/relational-databases/clr-integration/clr-integration-enabling) nella documentazione di SQL Server.

### <a name="verification-script"></a>Script di verifica
È possibile eseguire lo script seguente per verificare le configurazioni di database per le repliche primarie e secondarie. Prima di risolvere un problema su una replica secondaria, è necessario modificare tale replica secondaria in modo che diventi la replica primaria.

    SET NOCOUNT ON

    DECLARE @dbname NVARCHAR(128)

    SELECT @dbname = sd.name FROM sys.sysdatabases sd WHERE sd.dbid = DB_ID()

    IF (@dbname = N'master' OR @dbname = N'model' OR @dbname = N'msdb' OR @dbname = N'tempdb' OR @dbname = N'distribution' ) BEGIN
    RAISERROR(N'ERROR: Script is targetting a system database.  It should be targeting the DB you created instead.', 0, 1)
    GOTO Branch_Exit;
    END ELSE
    PRINT N'INFO: Targetted database is ' + @dbname + N'.'

    PRINT N'INFO: Running verifications....'

    IF NOT EXISTS (SELECT * FROM sys.configurations c WHERE c.name = 'clr enabled' AND c.value_in_use = 1)
    PRINT N'ERROR: CLR is not enabled!'
    ELSE
    PRINT N'PASS: CLR is enabled.'

    DECLARE @repltable TABLE (
    name nvarchar(max),
    minimum int,
    maximum int,
    config_value int,
    run_value int )

    INSERT INTO @repltable
    EXEC sp_configure 'max text repl size (B)'

    IF NOT EXISTS(SELECT * from @repltable where config_value = 2147483647 and run_value = 2147483647 )
    PRINT N'ERROR: Max text repl size is not correct!'
    ELSE
    PRINT N'PASS: Max text repl size is correct.'

    IF NOT EXISTS (SELECT db.owner_sid FROM sys.databases db WHERE db.database_id = DB_ID() AND db.owner_sid = 0x01)
    PRINT N'ERROR: Database owner is not sa account!'
    ELSE
    PRINT N'PASS: Database owner is sa account.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_trustworthy_on = 1 )
    PRINT N'ERROR: Trustworthy bit is not on!'
    ELSE
    PRINT N'PASS: Trustworthy bit is on.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_broker_enabled = 1 )
    PRINT N'ERROR: Service broker is not enabled!'
    ELSE
    PRINT N'PASS: Service broker is enabled.'

    IF NOT EXISTS( SELECT * FROM sys.databases db WHERE db.database_id = DB_ID() AND db.is_honor_broker_priority_on = 1 )
    PRINT N'ERROR: Service broker priority is not set!'
    ELSE
    PRINT N'PASS: Service broker priority is set.'

    PRINT N'Done!'

    Branch_Exit:

## <a name="limitations-and-known-issues"></a>Limitazioni e problemi noti
Le limitazioni seguenti si applicano a tutti gli scenari.   

**Opzioni e configurazioni di SQL Server non supportate:**
- **Gruppi di disponibilità di base**  
  Introdotti con SQL Server 2016 Standard Edition, [i gruppi di disponibilità di base](https://msdn.microsoft.com/library/mt614935.aspx) non supportano l'accesso in lettura alle repliche secondarie, requisito essenziale per l'uso con Configuration Manager.
- **Istanza del cluster di failover**  
  Le [istanze del cluster di failover](/sql/sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server) non sono supportate per una replica usata con Configuration Manager.

**SQL Server che ospitano gruppi di disponibilità aggiuntivi:**   
Prima della versione 1610 di Configuration Manager, quando un gruppo di disponibilità su un'istanza di SQL Server ospita una o più gruppi di disponibilità in aggiunta al gruppo usato per Configuration Manager, ogni replica in ogni gruppo di disponibilità aggiuntivo deve avere le configurazioni seguenti impostate al momento dell'installazione di Configuration Manager o di un suo aggiornamento:
-   **failover manuale**
-   **consentire le connessioni di sola lettura**

**Uso di database non supportati:**
-   **Configuration Manager supporta solo il database del sito in un gruppo di disponibilità:** non sono supportati i database seguenti:
    -   Database di report
    -   Database WSUS
-   **Database preesistente:** non è possibile usare il nuovo database creato nella replica. In alternativa, è necessario ripristinare una copia di un database di Configuration Manager esistente nella replica primaria quando si configura un gruppo di disponibilità.

**Errori di installazione in ConfigMgrSetup.log:**  
Quando si esegue l'installazione per spostare un database del sito in un gruppo di disponibilità, l'installazione tenta di elaborare i ruoli del database nelle repliche secondarie del gruppo di disponibilità e registra errori simili al seguente:
-   ERRORE: Errore SQL Server: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Impossibile aggiornare il database "CM_AAA" perché è di sola lettura. Installazione di Configuration Manager 1/21/2016 4:54:59 PM 7344 (0x1CB0)  

Ignorare questi errori.

## <a name="changes-for-site-backup"></a>Modifiche per il backup del sito
**Eseguire il backup dei file di database:**  
Quando un database del sito viene eseguito in un gruppo di disponibilità, è necessario eseguire l'attività di manutenzione predefinita **Backup server sito** per eseguire il backup di impostazioni e file comuni di Configuration Manager. Non usare tuttavia i file MDF o LDF creati dal backup. Eseguire invece backup diretti di questi file del sito usando SQL Server.

**Log delle transazioni:**  
Il modello di recupero del database del sito deve essere impostato su **Completo** per l'uso in un gruppo di disponibilità. Con questa configurazione pianificare il monitoraggio e la gestione delle dimensioni del log delle transazioni del database del sito. Nel modello di recupero Completo le transazioni non vengono finalizzate fino a quando non viene eseguito un backup completo del database o del log delle transazioni. Per altre informazioni vedere [Backup e ripristino di database SQL Server](/sql/relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases) nella documentazione di SQL Server.

## <a name="changes-for-site-recovery"></a>Modifiche per il ripristino del sito
È possibile usare l'opzione di ripristino del sito **Ignora ripristino database (usare questa opzione se non si sono verificati errori nel database del sito)** a condizione che almeno uno dei nodi del gruppo di disponibilità continui a funzionare.

 Se invece tutti i nodi di un gruppo di disponibilità sono andati perduti, prima di poter ripristinare il sito è necessario ricreare il gruppo di disponibilità. Configuration Manager non è in grado di ricompilare o ripristinare il nodo di disponibilità. Dopo aver ricreato il gruppo e ripristinato e riconfigurato un backup, è possibile usare l'opzione di ripristino del sito **Ignora ripristino database (usare questa opzione se non si sono verificati errori nel database del sito)**.

Per altre informazioni, vedere [Backup e ripristino per System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

## <a name="changes-for-reporting"></a>Modifiche per la creazione di report
**Installare il punto di Reporting Services:**  
Il punto di Reporting Services non supporta l'uso del nome virtuale del listener del gruppo di disponibilità o l'hosting del database di Reporting Services in un gruppo di disponibilità Always On di SQL Server:
-   Per impostazione predefinita, il punto di Reporting Services imposta il **nome del server del database del sito** sul nome virtuale specificato come listener. Modificare questa opzione per specificare un nome di computer e l'istanza di una replica nel gruppo di disponibilità.
-   Per eseguire l'offload del carico di creazione di report e aumentare la disponibilità quando un nodo di replica è offline, prendere in considerazione l'installazione di altri punti di Reporting Services in ogni nodo di replica e la configurazione di ogni punto di Reporting Services in modo che punti al proprio nome di computer.

Quando si installa un punto di Reporting Services in ogni replica del gruppo di disponibilità, il reporting può sempre connettersi a un server del punto di reporting attivo.

**Cambiare il punto di Reporting Services usato dalla console:**  
Per eseguire i report, nella console passare a **Monitoraggio** > **Panoramica** > **Reporting** > **Report**, quindi scegliere **Opzioni report**. Nella finestra di dialogo Opzioni report selezionare il punto di Reporting Services desiderato.

## <a name="next-steps"></a>Passaggi successivi
Dopo avere compreso i prerequisiti, le limitazioni e le modifiche alle attività comuni necessarie quando si usano i gruppi di disponibilità, vedere [Configurare i gruppi di disponibilità per Configuration Manager](/sccm/core/servers/deploy/configure/configure-aoag), per le procedure che consentono di installare e configurare il sito per l'uso di gruppi di disponibilità.

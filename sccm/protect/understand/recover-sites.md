---
title: Ripristino del sito | Microsoft Docs
description: Informazioni su come ripristinare i siti in System Center Configuration Manager.
ms.custom: na
ms.date: 6/5/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
caps.latest.revision: 
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: f5aff56e9948536944140fbadb0539c7a4e20f26
ms.sourcegitcommit: 5ca89204716750eaaceb01bba40b35b85c7122ba
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/18/2017
---
#  <a name="recover-a-configuration-manager-site"></a>Ripristinare un sito di Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Eseguire un ripristino del sito di Configuration Manager dopo che si verifica un errore nel sito di Configuration Manager o una perdita di dati nel database del sito. La riparazione e la risincronizzazione dei dati sono le attività principali del ripristino di un sito e sono necessarie per evitare l'interruzione delle operazioni.

Le sezioni in questo argomento sono utili per il ripristino di un sito di Configuration Manager. Per creare un backup, vedere [Backup di Configuration Manager](/sccm/protect/understand/backup-and-recovery).

## <a name="considerations-before-recovering-a-site"></a>Considerazioni prima del recupero di un sito
**È necessario usare la stessa versione ed edizione di SQL Server,** ad esempio non è supportato il ripristino di un database eseguito in SQL Server 2014 in SQL Server 2016. Analogamente non è supportato il ripristino di un database del sito eseguito nella Standard Edition di SQL Server 2016 alla Enterprise Edition di SQL Server 2016.
-   SQL Server non deve essere impostato sulla **modalità utente singolo**.
-   Assicurarsi che i file MDF e LDF siano validi. Quando si ripristina un sito, non viene eseguita alcuna verifica dello stato dei file da ripristinare.

**Se si usa un gruppo di disponibilità Always On di SQL Server per ospitare il database del sito:** Modificare i piani di ripristino come descritto in [Preparare l'uso di gruppi di disponibilità Always On di SQL Server](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-recovery).

**Quando si usano le repliche di database:** dopo avere ripristinato il database di un sito che era stato configurato per le repliche di database, prima di poter usare le repliche è necessario riconfigurare ciascuna replica del database, ricreando sia le pubblicazioni sia le sottoscrizioni.

## <a name="determine-your-recovery-options"></a>Determinare le opzioni di ripristino
Ci sono due aree principali da tenere in considerazione per il ripristino del sito di amministrazione centrale e del server del sito primario di Configuration Manager: il **server del sito** e il **database del sito**.
Le sezioni seguenti consentono di selezionare le opzioni migliori per lo scenario di ripristino.

> [!NOTE]   
> Quando il programma di installazione rileva la presenza di un sito di Configuration Manager sul server, è possibile avviare un ripristino del sito, sebbene le opzioni di ripristino per il server del sito siano limitate. Ad esempio, se si esegue il programma di installazione su un server del sito esistente, scegliendo l'operazione di ripristino è possibile recuperare il server di database del sito, ma l'opzione di ripristino del server del sito è disabilitata.

### <a name="site-server-recovery-options"></a>Opzioni di ripristino del server del sito
Avviare l'installazione da una copia della cartella **CD.Latest** creata esternamente alla cartella di installazione di Configuration Manager.
-   Se si esegue il programma di installazione di Configuration Manager dal menu **Start** sul server del sito, l'opzione **Ripristina un sito** non sarà disponibile.
-   Se sono stati installati aggiornamenti dalla console di Configuration Manager prima di eseguire il backup, non è possibile reinstallare il sito usando l'installazione dai supporti di installazione o dal percorso di installazione di Configuration Manager.

Selezionare quindi l'opzione **Ripristina un sito**. Sono disponibili le seguenti opzioni di ripristino per il server del sito in cui si è verificato un errore:

-   **Ripristina il server di sito utilizzando un backup esistente**: usare questa opzione quando è disponibile un backup del server del sito di Configuration Manager creato nel server del sito come parte dell'attività di manutenzione **Backup server sito** prima dell'errore nel sito. Il sito viene reinstallato e vengono configurate le relative impostazioni in base al sito di cui era stato eseguito il backup.
-   **Reinstalla il server del sito**: usare questa opzione quando non è disponibile un backup del server del sito. Il server del sito viene reinstallato ed è necessario specificare le impostazioni del sito come nella procedura di installazione iniziale.
  -   È necessario usare lo stesso codice sito e nome del database del sito usati durante l'installazione iniziale del sito su cui si è verificato l'errore.
  -   È possibile reinstallare il sito in un nuovo computer che esegue un nuovo sistema operativo.
  -   Il computer deve usare lo stesso nome, nome di dominio completo, del server del sito originale.   

### <a name="site-database-recovery-options"></a>Opzioni di ripristino del database del sito
Quando si esegue il programma di installazione, sono disponibili le seguenti opzioni di ripristino per il database del sito:
-   **Ripristina il database del sito usando il set di backup**: usare questa opzione quando è disponibile un backup del database del sito di Configuration Manager creato come parte dell'attività di manutenzione **Backup server sito** in esecuzione nel sito prima dell'errore nel database del sito. Quando si dispone di una gerarchia, le modifiche apportate al database del sito dopo l'ultimo backup del database del sito vengono recuperate dal sito di amministrazione centrale per un sito primario o da un sito primario di riferimento per un sito di amministrazione centrale. Quando si ripristina il database del sito per un sito primario autonomo, si perdono le modifiche apportate al sito dopo l'ultimo backup.

   Quando si ripristina il database del sito per un sito in una gerarchia, il comportamento di ripristino è differente per un sito di amministrazione centrale o un sito primario e a seconda del fatto che l'ultimo backup rientri o meno nel periodo di memorizzazione del rilevamento delle modifiche SQL Server. Per altre informazioni, vedere la sezione [Scenari di ripristino del database del sito](##site-database-recovery-scenarios) in questo argomento.
  > [!NOTE]   
  > Il ripristino non riesce se si sceglie di ripristinare il database del sito usando un set di backup ma il database del sito è già esistente.  

-   **Crea un nuovo database per il sito**: usare questa opzione quando non è disponibile un backup del database del sito di Configuration Manager. Quando si dispone di una gerarchia, viene creato un nuovo database del sito e i dati vengono ripristinati usando i dati replicati del sito di amministrazione centrale per un sito primario, oppure di un sito primario di riferimento per un sito di amministrazione centrale. Questa opzione non è disponibile quando si ripristina un sito primario autonomo o un sito di amministrazione centrale che non dispone di siti primari.

-   **Utilizza un database del sito ripristinato manualmente**: usare questa opzione quando è già stato eseguito il ripristino del database del sito di Configuration Manager, ma è necessario completare il processo di ripristino.
    -   Configuration Manager è in grado di ripristinare il database del sito dall'attività di manutenzione di backup di Configuration Manager oppure da un backup del database del sito eseguito mediante DPM o un altro processo. Dopo il ripristino del database del sito mediante un metodo esterno a Configuration Manager, è necessario eseguire il programma di installazione e selezionare questa opzione per completare il ripristino del database del sito.

    > [!NOTE]   
    > Quando si usa DPM per il backup del database del sito, usare le procedure DPM per ripristinare il database del sito in una posizione specifica prima di continuare il processo di ripristino in Configuration Manager. Per altre informazioni su DPM, vedere [Data Protection Manager Documentation Library (Libreria di documentazione di Data Protection Manager)]() in TechNet.    

    -   Quando si dispone di una gerarchia, le modifiche apportate al database del sito dopo l'ultimo backup del database del sito vengono recuperate dal sito di amministrazione centrale per un sito primario o da un sito primario di riferimento per un sito di amministrazione centrale. Quando si ripristina il database del sito per un sito primario autonomo, si perdono le modifiche apportate al sito dopo l'ultimo backup.     


-   **Ignora ripristino database**: usare questa opzione quando non si è verificata alcuna perdita di dati nel server di database del sito di Configuration Manager. Questa opzione è valida solo quando il database del sito si trova in un computer diverso rispetto al server del sito che si desidera ripristinare.

### <a name="sql-server-change-tracking-retention-period"></a>Periodo di memorizzazione del rilevamento modifiche di SQL Server
Il rilevamento delle modifiche è abilitato per il database del sito in SQL Server. Il rilevamento delle modifiche consente a Configuration Manager di eseguire query per informazioni sulle modifiche apportate alle tabelle di database in seguito a un momento precedente. Il periodo di memorizzazione specifica per quanto tempo verranno conservate le informazioni di rilevamento delle modifiche. Per impostazione predefinita, il database del sito è configurato per un periodo di memorizzazione di 5 giorni. Quando si ripristina un database del sito, il processo di ripristino viene eseguito in modo diverso a seconda che il backup rientri o meno nel periodo di memorizzazione. Se, ad esempio, nel server di database del sito si verifica un errore e l'ultimo backup risale a 7 giorni fa, il backup è esterno al periodo di memorizzazione.

Per altre informazioni sui meccanismi interni di rilevamento delle modifiche di SQL Server, vedere i post di blog seguenti del team di SQL Server: [Change Tracking Cleanup - part 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1/) (Pulizia del rilevamento modifiche - parte 1) e [Change Tracking Cleanup - part 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2) (Pulizia del rilevamento modifiche - parte 2).

### <a name="reinitialization-of-site-or-global-data"></a>Reinizializzazione dei dati globali o del sito
Il processo per reinizializzare i dati globali o i dati del sito sostituisce i dati esistenti nel database del sito con i dati di un altro database del sito. Quando ad esempio il sito ABC reinizializza i dati dal sito XYZ, vengono eseguiti i seguenti passaggi:
-   I dati vengono copiati dal sito XYZ al sito ABC.
-   I dati esistenti per il sito XYZ vengono rimossi dal database del sito nel sito ABC.
-   I dati copiati dal sito XYZ vengono inseriti nel database del sito per il sito ABC.

#### <a name="example-scenario-1"></a>Scenario di esempio 1
**Il sito primario reinizializza i dati globali dal sito di amministrazione centrale**: il processo di ripristino rimuove i dati globali esistenti per il sito primario nel database del sito primario e li sostituisce con i dati globali copiati dal sito di amministrazione centrale.

#### <a name="example-scenario-2"></a>Scenario di esempio 2
**Il sito di amministrazione centrale reinizializza i dati del sito da un sito primario**: il processo di ripristino rimuove i dati del sito esistenti per il sito primario nel database del sito di amministrazione centrale e li sostituisce con i dati del sito copiati dal sito primario. I dati del sito per altri siti primari non sono interessati.

### <a name="site-database-recovery-scenarios"></a>Scenari di ripristino del database del sito
Dopo il ripristino di un database del sito da un backup, Configuration Manager tenta di ripristinare le modifiche apportate nei dati globali e nei dati del sito dopo l'ultimo backup del database. Di seguito vengono descritte le azioni avviate da Configuration Manager in seguito al ripristino del database del sito dal backup.

**Il sito ripristinato è un sito di amministrazione centrale:**
-   **Backup del database all'interno del periodo di memorizzazione del rilevamento delle modifiche**
    -   **Dati globali:** le modifiche presenti nei dati globali dopo il backup vengono replicate da tutti i siti primari.
    -   **Dati del sito:** le modifiche presenti nei dati del sito dopo il backup vengono replicate da tutti i siti primari.


-   **Backup del database antecedente al periodo di memorizzazione del rilevamento delle modifiche**
    -   **Dati globali:** il sito di amministrazione centrale reinizializza i dati globali dal sito primario di riferimento, se specificato. Tutti gli altri siti primari reinizializzano quindi i dati globali dal sito di amministrazione centrale. Se non viene specificato alcun sito di riferimento, tutti i siti primari reinizializzano i dati globali dal sito di amministrazione centrale (i dati ripristinati dal backup).
    -   **Dati del sito:** il sito di amministrazione centrale reinizializza i dati del sito da ogni sito primario.


**Il sito ripristinato è un sito primario:**
-   **Backup del database all'interno del periodo di memorizzazione del rilevamento delle modifiche**
    -   **Dati globali:** le modifiche presenti nei dati globali dopo il backup vengono replicate dal sito di amministrazione centrale.
    -   **Dati del sito:** il sito di amministrazione centrale reinizializza i dati del sito dal sito primario. Le modifiche apportate dopo il backup vanno perse, ma la maggior parte dei dati viene rigenerata dai client che inviano le informazioni al sito primario.


-   **Backup del database antecedente al periodo di memorizzazione del rilevamento delle modifiche**
    -   **Dati globali:** il sito primario reinizializza i dati globali dal sito di amministrazione centrale.
    -   **Dati del sito:** il sito di amministrazione centrale reinizializza i dati del sito dal sito primario. Le modifiche apportate dopo il backup vanno perse, ma la maggior parte dei dati viene rigenerata dai client che inviano le informazioni al sito primario.

## <a name="site-recovery-procedures"></a>Procedure di ripristino del sito
Usare una delle seguenti procedure per ripristinare il server del sito e il database del sito.

### <a name="to-start-a-site-recovery-in-the-setup-wizard"></a>Per avviare un ripristino del sito nell'Installazione guidata
1.  Copiare la cartella [CD.Latest](/sccm/core/servers/manage/the-cd.latest-folde) in un percorso esterno alla cartella di installazione di Configuration Manager.
Dalla copia della cartella CD.Latest eseguire l'Installazione guidata di Configuration Manager.

2.  Nella pagina **Riquadro attività iniziale** selezionare **Ripristina un sito**, quindi fare clic su **Avanti**.

3.  Completare la procedura guidata usando le opzioni appropriate per il ripristino del sito.

  -   Durante il ripristino, il programma di installazione identifica la porta di SQL Server Service Broker (SSB) usata da SQL Server. Se questa impostazione porta viene modificata durante il ripristino, la replica dei dati non verrà eseguita correttamente al termine del ripristino.

  -   È possibile specificare il percorso originale o uno nuovo da usare per l'installazione di Configuration Manager nell'Installazione guidata.

### <a name="to-start-an-unattended-site-recovery"></a>Per avviare un ripristino del sito automatico
  1.    Preparare lo script di installazione automatica per le opzioni richieste per il ripristino del sito.  Vedere [Chiavi del file di script di ripristino del sito automatico](/sccm/protect/understand/unattended-site-recovery-script-file-keys).

  2.    Eseguire il programma di installazione di Configuration Manager con l'opzione di comando **/script**. Se, ad esempio, il file di inizializzazione dell'installazione è stato denominato ConfigMgrUnattend.ini e salvato nella directory C:\Temp del computer in cui viene eseguito il programma di installazione, il comando sarà: **Setup /script C:\temp\ConfigMgrUnattend.ini**.

  > [!NOTE]   
  >  Dopo aver ripristinato un sito di amministrazione centrale, potrebbe non essere possibile stabilire la replica di alcuni dati del sito da siti figlio. Sono inclusi, tra gli altri, l'inventario hardware, l'inventario software e i messaggi di stato.
  >
  >  In tal caso è necessario reinizializzare **ConfigMgrDRSSiteQueue** per la replica di database.  A tale scopo, usare **SQL Server Manager** per eseguire la query riportata di seguito nel database del sito di Configuration Manager nel sito di amministrazione centrale:
  >
  >  **IF EXISTS (SELECT \* FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)**
  >
  >  **ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON**


## <a name="post-recovery-tasks"></a>Attività post-ripristino
Dopo aver eseguito il ripristino del sito, è necessario considerare diverse attività post-ripristino prima di completare il ripristino del sito. Usare le seguenti sezioni per completare il processo di ripristino del sito.

### <a name="re-enter-user-account-passwords"></a>Immettere di nuovo le password account utente
Dopo il ripristino di un server del sito, è necessario immettere nuovamente le password per gli account utente specificati per il sito perché vengono reimpostate durante il ripristino. Gli account vengono elencati nella pagina **Operazione completata** dell'Installazione guidata dopo aver completato il ripristino del sito e vengono salvati in C:\ConfigMgrPostRecoveryActions.html nel server del sito ripristinato.

#### <a name="to-re-enter-user-account-passwords-after-site-recovery"></a>Per immettere nuovamente le password account utente dopo il ripristino del sito

1.  Aprire la console di Configuration Manager e connettersi al sito ripristinato.

2.  Nella console di Configuration Manager fare clic su **Amministrazione**.

3.  Nell'area di lavoro **Amministrazione** espandere **Sicurezza**e quindi fare clic su **Account**.

4.  Per ogni account in cui si immette nuovamente la password, eseguire le seguenti operazioni:

    1.  Selezionare l'account dall'elenco degli account individuati dopo il ripristino del sito. È possibile trovare questo elenco di C:\ConfigMgrPostRecoveryActions.html nel server del sito ripristinato.

    2.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà** per aprire le proprietà dell'account.

    3.  Nella scheda **Generale** fare clic su **Imposta**e quindi immettere nuovamente le password per l'account.

    4.  Fare clic su **Verifica**, selezionare l'origine dati appropriata per l'account utente selezionato e quindi fare clic su **Verifica connessione** per verificare che l'account utente possa connettersi all'origine dati.

    5.  Fare clic su **OK** per salvare le modifiche alle password e quindi fare clic su **OK**.

### <a name="re-enter-sideloading-keys"></a>Immettere nuovamente le chiavi di trasferimento locale
Dopo un ripristino del server di sito, è necessario immettere nuovamente le chiavi di trasferimento locale di Windows specificate per il sito perché queste vengono reimpostate durante il ripristino del sito. Dopo aver immesso nuovamente le chiavi di trasferimento locale, il conteggio nella colonna **Attivazioni usate** per le chiavi di trasferimento locale è reimpostato nella console di Configuration Manager. Supponiamo ad esempio che prima dell'errore del sito il conteggio **Attivazioni totali** sia impostato su **100** e **Attivazioni usate** su **90** per il numero di chiavi usate dai dispositivi. Dopo il ripristino del sito, la colonna **Attivazioni totali** visualizza ancora **100**, ma la colonna **Attivazioni usate** visualizza erroneamente **0**. Tuttavia successivamente all'uso da parte di 10 nuovi dispositivi di una chiave di trasferimento locale, non esisteranno chiavi di trasferimento locale residue e per il dispositivo successivo sarà impossibile applicare una chiave di trasferimento locale.

### <a name="recreate-the-microsoft-intune-subscription"></a>Ricreare la sottoscrizione di Microsoft Intune
 Se si ripristina un server del sito di Configuration Manager dopo aver ricreato l'immagine del computer server del sito, la sottoscrizione di Microsoft Intune non viene ripristinata. Dopo aver ripristinato il sito, è necessario riconnettersi alla sottoscrizione.  Non creare una nuova richiesta di APN, ma caricare invece il file PEM valido corrente caricato in occasione dell'ultima configurazione o dell'ultimo rinnovo della gestione iOS. Per ulteriori informazioni, vedere [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription).

### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Configurare SSL per i ruoli del sistema del sito che usano IIS
Quando si ripristinano sistemi del sito che eseguono IIS e che erano configurati per HTTPS prima dell'errore, è necessario riconfigurare IIS per usare il certificato server Web.

### <a name="reinstall-hotfixes-in-the-recovered-site-server"></a>Reinstallare gli aggiornamenti rapidi nel server del sito ripristinato
Dopo il ripristino di un sito, è necessario reinstallare gli aggiornamenti rapidi applicati al server del sito. Visualizzare l'elenco degli aggiornamenti rapidi installati in precedenza nella pagina **Completato** dell'installazione guidata dopo il ripristino del sito. Questo elenco viene salvato anche in **C:\ConfigMgrPostRecoveryActions.html** nel server del sito ripristinato.

### <a name="recover-custom-reports-on-the-computer-running-reporting-services"></a>Ripristinare i report personalizzati nel computer che esegue Reporting Services
Quando si creano dei report personalizzati di Reporting Services e si verifica un errore di Reporting Services, è possibile ripristinare i report quando si esegue il backup del server di report. Per altre informazioni sul ripristino dei report personalizzati in Reporting Services, vedere [Operazioni di backup e ripristino per un'installazione di Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=228724) nella documentazione online di SQL Server 2008.

### <a name="recover-content-files"></a>Ripristinare i file di contenuto
 Il database del sito contiene informazioni sul percorso di archiviazione dei file di contenuto nel server del sito, ma non viene eseguito il backup né il ripristino di tali file di contenuto come parte del processo di backup e ripristino. Per eseguire il ripristino completo dei file di contenuto, è necessario ripristinare i file di origine del pacchetto e la raccolta contenuto nel percorso originale. Sono disponibili diversi metodi per il ripristino dei file di contenuto, ma il metodo più semplice è ripristinare i file da un backup del file system del server del sito.

 Se non si dispone di un backup del file system per i file di origine del pacchetto, è necessario copiare o scaricare manualmente tali file come per il primo pacchetto creato in origine. È possibile eseguire la seguente query in SQL Server per trovare il percorso di origine del pacchetto per tutti i pacchetti e le applicazioni: `SELECT * FROM v_Package`. È possibile identificare il sito di origine del pacchetto esaminando i primi tre caratteri dell'ID di pacchetto. Ad esempio, se l'ID del pacchetto è CEN00001, il codice del sito per il sito di origine è CEN. I file di origine del pacchetto devono essere ripristinati nella stessa posizione in cui si trovavano prima dell'errore.

 Se non si dispone di un backup del file system che contenga la raccolta contenuto, eseguire una delle seguenti opzioni di ripristino:

-   **Importare un file di contenuti in versione di preproduzione**: quando è disponibile una gerarchia di Configuration Manager, è possibile creare un file di contenuti in versione di preproduzione con tutti i pacchetti e le applicazioni da un altro percorso e quindi importare questo file per ripristinare la raccolta contenuto nel server del sito.

-   **Aggiornare il contenuto**: quando si avvia l'azione di aggiornamento del contenuto per un tipo di distribuzione dell'applicazione o del pacchetto, il contenuto viene copiato dall'origine del pacchetto alla raccolta contenuto. Per completare correttamente questa azione, è necessario che i file di origine del pacchetto siano disponibili nel percorso originale. È necessario eseguire questa azione in ogni pacchetto e applicazione.

### <a name="recover-custom-software-updates-on-the-computer-running-updates-publisher"></a>Recuperare gli aggiornamenti software personalizzati nel computer che esegue Updates Publisher
Quando sono stati inclusi i file di database di Updates Publisher nel piano di backup, è possibile ripristinare i database in caso di errore nel computer in cui viene eseguito Updates Publisher. Per altre informazioni su Updates Publisher, vedere [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) nella Libreria TechCenter di System Center.

Usare la procedura seguente per ripristinare il backup del database Updates Publisher.

#### <a name="to-restore-the-updates-publisher-2011-database"></a>Per ripristinare il database Updates Publisher 2011
1.  Reinstallare Updates Publisher nel computer ripristinato.

2.  Copiare il file di database (Scupdb.sdf) dalla destinazione di backup in %*PROFILOUTENTE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\ nel computer che esegue Updates Publisher.

3.  Quando più utenti eseguono Updates Publisher nel computer, è necessario copiare ogni file di database nel percorso del profilo utente appropriato.

### <a name="user-state-migration-data"></a>Dati di migrazione sullo stato utente
Come parte delle proprietà del sistema del sito del punto di migrazione, è possibile specificare le cartelle in cui vengono archiviati i dati di migrazione stato utente. Dopo aver ripristinato un server con una cartella che archivia dati di migrazione stato utente, è necessario ripristinare manualmente i dati di migrazione stato utente nel server nelle stesse cartelle in cui sono stati archiviati i dati prima dell'errore.

### <a name="regenerate-the-certificates-for-distribution-points"></a>Rigenerare i certificati per i punti di distribuzione
Dopo aver ripristinato un sito, il file distmgr.log potrebbe contenere una voce per uno o più punti di distribuzione, che indica che non è stato possibile decrittografare i dati PFX ****del certificato. Questa voce indica che i dati del certificato del punto di distribuzione non possono essere decrittografati dal sito. Per risolvere questo problema, è necessario rigenerare o reimportare il certificato per i punti di distribuzione interessati. A questo scopo, è possibile usare il cmdlet[Set-CMDistributionPoint](https://technet.microsoft.com/library/jj821872\(v=sc.20\).aspx) di PowerShell.

### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Aggiornare i certificati usati per i punti di distribuzione basati su cloud
 Configuration Manager richiede un certificato di gestione che utilizza per la comunicazione dal server del sito al punto di distribuzione basato su cloud. Dopo un ripristino del sito è necessario aggiornare i certificati per i punti di distribuzione basati su cloud.

## <a name="recover-a-secondary-site"></a>Ripristinare un sito secondario
 Configuration Manager non supporta il backup del database in un sito secondario, ma supporta il ripristino mediante reinstallazione del sito secondario. Il ripristino del sito secondario è necessario quando si verifica un errore del sito secondario di Configuration Manager.

### <a name="requirements-for-reinstalling-a-secondary-site"></a>Requisiti per la reinstallazione di un sito secondario
-   Il computer deve soddisfare tutti i prerequisiti del sito secondario e deve disporre dei privilegi di protezione appropriati configurati.
-   Usare lo stesso percorso di installazione usato per il sito per cui si è verificato un errore.
-   È necessario usare un computer con la stessa configurazione del computer in cui si è verificato l'errore, ad esempio con il FQDN, per ripristinare correttamente il sito secondario.
-   Il computer deve avere la stessa configurazione di SQL Server del sito in cui si è verificato l'errore.
  -   Durante il ripristino di un sito secondario Configuration Manager non installa SQL Server Express, se questo non è già installato nel computer.
  -   È necessario usare la stessa versione di SQL Server e la stessa istanza di SQL Server usate per il database del sito secondario prima dell'errore.

### <a name="to-recover-a-secondary-site"></a>Per ripristinare un sito secondario:
Per ripristinare un sito secondario, usare l'azione **Ripristina sito secondario** dal nodo **Siti** nella console di Configuration Manager. Diversamente dal ripristino di un sito di amministrazione centrale o un sito primario, il ripristino di un sito secondario non usa un file di backup, ma reinstalla i file del sito secondario in cui si è verificato l'errore. Dopo la reinstallazione del sito, i dati del sito secondario vengono quindi reinizializzati con i dati del sito primario padre.

Durante il processo di ripristino Configuration Manager verifica se la raccolta contenuto esiste nel computer del sito secondario e che il contenuto appropriato sia disponibile. Il sito secondario userà la raccolta contenuto esistente, se questa include il contenuto appropriato. In caso contrario, per ripristinare la raccolta contenuto di un sito secondario ripristinato, è necessario ridistribuire o pre-installare il contenuto in tale sito ripristinato.

Quando si dispone di un punto di distribuzione che non si trova nel sito secondario, non è necessario reinstallare il punto di distribuzione durante un ripristino del sito secondario. Dopo il ripristino del sito secondario il sito si sincronizza automaticamente con il punto di distribuzione.

È possibile verificare lo stato del sito secondario mediante l'azione **Mostra stato installazione** dal nodo **Siti** nella console di Configuration Manager.

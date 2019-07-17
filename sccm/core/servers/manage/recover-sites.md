---
title: Ripristino del sito
titleSuffix: Configuration Manager
description: Informazioni su come ripristinare i siti in Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 19539f4d-1667-4b4c-99a1-9995f12cf5f7
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 48e0f2c1d04f0592cd794aa4315641fe6f9cd15b
ms.sourcegitcommit: 9670e11316c9ec6e5f78cd70c766bbfdf04ea3f9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67818113"
---
#  <a name="recover-a-configuration-manager-site"></a>Ripristinare un sito di Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Eseguire un ripristino del sito di Configuration Manager dopo che si verifica un errore nel sito o una perdita di dati nel database del sito. La riparazione e la risincronizzazione dei dati sono le attività principali del ripristino di un sito e sono necessarie per evitare l'interruzione delle operazioni.

Le sezioni in questo articolo sono utili per il ripristino di un sito di Configuration Manager. Per creare un backup, vedere [Backup di Configuration Manager](/sccm/core/servers/manage/backup-and-recovery).



## <a name="considerations-before-recovering-a-site"></a>Considerazioni prima del recupero di un sito

> [!Important]  
> Queste informazioni si applicano solo agli scenari di ripristino sito. Se si sta aggiornando l'infrastruttura locale e non ripristinando attivamente un sito in cui si è verificato un errore, esaminare le informazioni negli articoli seguenti:
> - [Aggiornare l'infrastruttura locale](/sccm/core/servers/manage/upgrade-on-premises-infrastructure)
> - [Modificare l'infrastruttura](/sccm/core/servers/manage/modify-your-infrastructure)


#### <a name="use-the-same-version-and-edition-of-sql-server"></a>Usare la stessa versione ed edizione di SQL Server   
Ad esempio, il ripristino di un database da SQL Server 2014 a SQL Server 2016 non è supportato. Analogamente, non è supportato il ripristino di un database del sito di SQL Server 2016 dall'edizione Standard all'edizione Enterprise.
- SQL Server non può essere impostato sulla **modalità utente singolo**.
- Verificare che i file MDF e LDF siano validi. Quando si ripristina un sito, non viene eseguita alcuna verifica dello stato dei file.  

#### <a name="sql-server-always-on-availability-groups"></a>Gruppi di disponibilità Always On di SQL Server   
Se si usano i gruppi di disponibilità Always On di SQL Server per ospitare il database del sito, modificare i piani di ripristino come descritto in [Prepararsi all'uso di SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#changes-for-site-recovery).

#### <a name="database-replicas"></a>Repliche di database  
Dopo aver ripristinato un database del sito configurato per le repliche di database, riconfigurare ogni replica. Prima di poter usare le repliche di database, ricreare sia le pubblicazioni che le sottoscrizioni.



## <a name="determine-your-recovery-options"></a>Determinare le opzioni di ripristino

Ci sono due aree principali da tenere in considerazione per il ripristino del sito di amministrazione centrale e del server del sito primario di Configuration Manager: il **server del sito** e il **database del sito**.
Le sezioni seguenti consentono di selezionare le opzioni migliori per lo scenario di ripristino.

> [!NOTE]   
> Quando il programma di installazione di Configuration Manager rileva la presenza di un sito sul server, è possibile avviare un ripristino del sito, nonostante le opzioni di ripristino per il server del sito siano limitate. Ad esempio, se si esegue il programma di installazione su un server del sito esistente, scegliendo l'operazione di ripristino è possibile recuperare il server di database del sito, ma l'opzione di ripristino del server del sito è disabilitata.


### <a name="site-server-recovery-options"></a>Opzioni di ripristino del server del sito

Avviare l'installazione di Configuration Manager da una copia della cartella **CD.Latest** creata esternamente alla cartella di installazione di Configuration Manager.  

-   Se si esegue il programma di installazione dal menu **Start** sul server del sito, l'opzione **Ripristina un sito** non sarà disponibile.  

-   Se sono stati installati aggiornamenti dalla console di Configuration Manager prima di aver eseguito il backup, non è possibile reinstallare il sito usando il programma di installazione dalle posizioni seguenti: 
    - Supporti di installazione
    - Percorso di installazione di Configuration Manager 

Selezionare quindi l'opzione **Ripristina un sito**. Sono disponibili le seguenti opzioni di ripristino per il server del sito in cui si è verificato un errore:  

#### <a name="recover-the-site-server-using-an-existing-backup"></a>Ripristina il server di sito utilizzando un backup esistente
Usare questa opzione quando si ha un backup di Configuration Manager del server del sito da prima che si verificasse l'errore del sito. Il sito crea questo backup durante l'attività di manutenzione **Backup server sito**. Il sito viene reinstallato e vengono configurate le relative impostazioni in base al sito di cui era stato eseguito il backup.  

#### <a name="reinstall-the-site-server"></a>Reinstallare il server del sito
Usare questa opzione se non si ha un backup del server del sito. Il server del sito viene reinstallato ed è necessario specificare le impostazioni del sito come nella procedura di installazione iniziale.  

-   Usare lo stesso codice del sito e nome del database del sito usati durante l'installazione iniziale del sito in cui si è verificato l'errore.  

-   È possibile reinstallare il sito in un nuovo computer che esegue una nuova versione del sistema operativo.  

-   Il server deve usare lo stesso nome host e lo stesso nome di dominio completo (FQDN) del server del sito originale.   


### <a name="site-database-recovery-options"></a>Opzioni di ripristino del database del sito

Quando si esegue il programma di installazione di Configuration Manager, sono disponibili le opzioni di ripristino seguenti per il database del sito:  

#### <a name="recover-the-site-database-using-a-backup-set"></a>Recover the site database using a backup set (Ripristina il database del sito usando un set di backup)
Usare questa opzione quando si ha un backup di Configuration Manager del database del sito da prima che si verificasse l'errore del database. Il sito crea questo backup durante l'attività di manutenzione **Backup server sito**. In una gerarchia, quando si ripristina un sito primario, il processo di ripristino recupera dal sito di amministrazione centrale tutte le modifiche apportate al database del sito dopo l'ultimo backup. Quando si ripristina il sito di amministrazione centrale, il processo di ripristino recupera queste modifiche da un sito primario di riferimento. Quando si ripristina il database del sito per un sito primario autonomo, si perdono le modifiche apportate al sito dopo l'ultimo backup.  

Quando si ripristina il database del sito per un sito in una gerarchia, il comportamento di ripristino è differente per un sito di amministrazione centrale o un sito primario. Il comportamento è diverso anche quando l'ultimo backup è compreso o non compreso nel periodo di conservazione del rilevamento delle modifiche di SQL Server. Per altre informazioni, vedere la sezione [Scenari di ripristino del database del sito](#site-database-recovery-scenarios) in questo articolo.  

> [!NOTE]   
> Se si sceglie di ripristinare il database del sito usando un set di backup, ma il database del sito è già esistente, il ripristino non riesce.   

#### <a name="create-a-new-database-for-this-site"></a>Crea un nuovo database per il sito
Usare questa opzione se non si ha un backup del database del sito. In una gerarchia il processo di ripristino crea un nuovo database del sito. Quando ripristina un sito primario figlio, recupera i dati eseguendo la replica dal sito di amministrazione centrale. Quando ripristina il sito di amministrazione centrale, replica i dati da un sito primario di riferimento. Questa opzione non è disponibile quando si ripristina un sito primario autonomo o un sito di amministrazione centrale che non ha siti primari.  

#### <a name="use-a-site-database-that-has-been-manually-recovered"></a>Usa un database del sito ripristinato manualmente
Usare questa opzione quando è già stato eseguito il ripristino del database del sito di Configuration Manager, ma è necessario completare il processo di ripristino.  

- Configuration Manager può ripristinare il database del sito da uno qualsiasi dei processi seguenti:  

  - L'attività di manutenzione di backup di Configuration Manager  
  - Un backup del database del sito tramite Data Protection Manager (DPM)  
  - Un altro processo di backup   

    Dopo il ripristino del database del sito mediante un metodo esterno a Configuration Manager, eseguire il programma di installazione e selezionare questa opzione per completare il ripristino del database del sito.  

    > [!NOTE]   
    > Quando si usa DPM per il backup del database del sito, usare le procedure DPM per ripristinare il database del sito in una posizione specifica prima di continuare il processo di ripristino in Configuration Manager. Per altre informazioni su DPM, vedere la raccolta della documentazione di [Data Protection Manager](https://docs.microsoft.com/system-center/dpm).    

- In una gerarchia, quando si recupera il database di un sito primario, il processo di ripristino recupera dal sito di amministrazione centrale tutte le modifiche apportate al database del sito dopo l'ultimo backup. Quando si ripristina il sito di amministrazione centrale, il processo di ripristino recupera queste modifiche da un sito primario di riferimento. Quando si ripristina il database del sito per un sito primario autonomo, si perdono le modifiche apportate al sito dopo l'ultimo backup.   

#### <a name="skip-database-recovery"></a>Ignorare il ripristino del database
Usare questa opzione quando non si è verificata alcuna perdita di dati nel server di database del sito di Configuration Manager. Questa opzione è valida solo quando il database del sito si trova in un computer diverso rispetto al server del sito che si vuole ripristinare.  


### <a name="sql-server-change-tracking-retention-period"></a>Periodo di memorizzazione del rilevamento modifiche di SQL Server

Configuration Manager consente il rilevamento delle modifiche per il database del sito in SQL Server. Il rilevamento delle modifiche consente a Configuration Manager di cercare le informazioni sulle modifiche apportate alle tabelle di database dopo un punto di ripristino precedente. Il periodo di conservazione specifica per quanto tempo verranno conservate le informazioni di rilevamento delle modifiche. Per impostazione predefinita, il database del sito è configurato per un periodo di conservazione di cinque giorni. Quando si ripristina un database del sito, il processo di ripristino viene eseguito in modo diverso a seconda che il backup rientri o meno nel periodo di memorizzazione. Se, ad esempio, nel server SQL si verifica un errore e l'ultimo backup risale a sette giorni fa, il backup non è compreso nel periodo di conservazione.

Per altre informazioni sui meccanismi interni di rilevamento delle modifiche di SQL Server, vedere i post di blog seguenti del team di SQL Server: [Change Tracking Cleanup - part 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1/) (Pulizia del rilevamento modifiche - parte 1) e [Change Tracking Cleanup - part 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2) (Pulizia del rilevamento modifiche - parte 2).


### <a name="reinitialization-of-site-or-global-data"></a>Reinizializzazione dei dati globali o del sito

Il processo per reinizializzare i dati globali o i dati del sito sostituisce i dati esistenti nel database del sito con i dati di un altro database del sito. Quando ad esempio il sito ABC reinizializza i dati dal sito XYZ, vengono eseguiti i seguenti passaggi:
- I dati vengono copiati dal sito XYZ al sito ABC.
- I dati esistenti per il sito XYZ vengono rimossi dal database del sito nel sito ABC.
- I dati copiati dal sito XYZ vengono inseriti nel database del sito per il sito ABC.

#### <a name="example-scenario-1-the-primary-site-reinitializes-the-global-data-from-the-central-administration-site"></a>Scenario di esempio 1: il sito primario reinizializza i dati globali dal sito di amministrazione centrale  
Il processo di ripristino rimuove i dati globali esistenti per il sito primario nel database del sito primario e li sostituisce con i dati globali copiati dal sito di amministrazione centrale.

#### <a name="example-scenario-2-the-central-administration-site-reinitializes-the-site-data-from-a-primary-site"></a>Scenario di esempio 2: il sito di amministrazione centrale reinizializza i dati del sito da un sito primario 
Il processo di ripristino rimuove i dati del sito esistenti per il sito primario nel database del sito di amministrazione centrale. Sostituisce i dati con i dati del sito copiati dal sito primario. I dati del sito per altri siti primari non sono interessati.


### <a name="site-database-recovery-scenarios"></a>Scenari di ripristino del database del sito

Dopo il ripristino di un database del sito da un backup, Configuration Manager prova a ripristinare le modifiche apportate nei dati globali e nei dati del sito dopo l'ultimo backup del database. Configuration Manager avvia le azioni seguenti dopo il ripristino del database del sito dal backup:  

#### <a name="recovered-site-is-a-central-administration-site"></a>Il sito ripristinato è un sito di amministrazione centrale
- Backup del database all'interno del periodo di memorizzazione del rilevamento delle modifiche  

     - **Dati globali**: le modifiche apportate ai dati globali in seguito al backup vengono replicate da tutti i siti primari.  

     - **Dati del sito**: le modifiche apportate ai dati del sito in seguito al backup vengono replicate da tutti i siti primari.  

- Backup del database antecedente al periodo di memorizzazione del rilevamento delle modifiche  

     - **Dati globali**: il sito di amministrazione centrale reinizializza i dati globali dal sito primario di riferimento, se specificato. Tutti gli altri siti primari reinizializzano quindi i dati globali dal sito di amministrazione centrale. Se non si specifica un sito di riferimento, tutti i siti primari reinizializzano quindi i dati globali dal sito di amministrazione centrale. Questi dati sono quelli ripristinati dal backup.  

     - **Dati del sito**: il sito di amministrazione centrale reinizializza i dati del sito da ogni sito primario.  

#### <a name="recovered-site-is-a-primary-site"></a>Il sito ripristinato è un sito primario
- Backup del database all'interno del periodo di memorizzazione del rilevamento delle modifiche  

     - **Dati globali**: le modifiche apportate ai dati globali in seguito al backup vengono replicate dal sito di amministrazione centrale.  

     - **Dati del sito**: il sito di amministrazione centrale reinizializza i dati del sito dal sito primario. Le modifiche apportate dopo il backup vanno perse. I client riscrivono la maggior parte dei dati quando inviano le informazioni al sito primario.  

- Backup del database antecedente al periodo di memorizzazione del rilevamento delle modifiche  
     - **Dati globali**: il sito primario reinizializza i dati globali dal sito di amministrazione centrale.  

     - **Dati del sito**: il sito di amministrazione centrale reinizializza i dati del sito dal sito primario. Le modifiche apportate dopo il backup vanno perse. I client riscrivono la maggior parte dei dati quando inviano le informazioni al sito primario.  



## <a name="site-recovery-procedures"></a>Procedure di ripristino del sito

Usare una delle procedure seguenti per ripristinare il server del sito e il database del sito:


### <a name="start-a-site-recovery-in-the-setup-wizard"></a>Avviare un ripristino sito nell'Installazione guidata

1. Copiare la cartella [CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder) in un percorso esterno alla cartella di installazione di Configuration Manager. Dalla copia della cartella CD.Latest eseguire l'Installazione guidata di Configuration Manager.  

2. Nella pagina **Riquadro attività iniziale** selezionare **Ripristina un sito**, quindi fare clic su **Avanti**.  

3. Completare la procedura guidata usando le opzioni appropriate per il ripristino del sito.  

     - Durante il ripristino, il programma di installazione identifica la porta di SQL Server Service Broker (SSB) usata da SQL Server. Se questa impostazione della porta viene modificata durante il ripristino, la replica dei dati non verrà eseguita correttamente al termine del ripristino.  

     - È possibile specificare il percorso originale o uno nuovo da usare per l'installazione di Configuration Manager nell'Installazione guidata.  


### <a name="start-an-unattended-site-recovery"></a>Avviare un ripristino sito automatico

1. Preparare lo script di installazione automatica per le opzioni richieste per il ripristino del sito. Per altre informazioni, vedere [Ripristino automatico dei siti](/sccm/core/servers/manage/unattended-recovery).  

2. Eseguire il programma di installazione di Configuration Manager con l'opzione della riga di comando `/script`. Si crea, ad esempio, un file di inizializzazione dell'installazione **ConfigMgrUnattend.ini**. Lo si salva nella directory `C:\Temp` del computer in cui si esegue l'installazione. Usare il comando seguente:  

    `setup.exe /script C:\temp\ConfigMgrUnattend.ini`  


> [!NOTE]   
>  Dopo aver ripristinato un sito di amministrazione centrale, potrebbe non essere possibile stabilire la replica di alcuni dati del sito da siti figlio. Questi dati includono, tra gli altri, l'inventario hardware, l'inventario software e i messaggi di stato.
>
>  Se si verifica questo problema, reinizializzare **ConfigMgrDRSSiteQueue** per la replica di database. Usare **SQL Server Manager** per eseguire la query riportata di seguito nel database del sito per il sito di amministrazione centrale:
>
> ``` SQL
> IF EXISTS (SELECT * FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)  
>  
> ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON
> ```



## <a name="post-recovery-tasks"></a>Attività post-ripristino

Dopo aver eseguito il ripristino del sito, considerare alcune attività post-ripristino prima di completare il ripristino del sito. Usare le seguenti sezioni per completare il processo di ripristino del sito.


### <a name="reenter-user-account-passwords"></a>Immettere di nuovo le password account utente

Dopo un ripristino del server del sito, immettere nuovamente le password per tutti gli account utente nel sito. Queste password vengono reimpostate durante il ripristino del sito. Gli account vengono elencati nella pagina **Completato** dell'Installazione guidata dopo il completamento del ripristino sito. L'elenco viene salvato anche in `C:\ConfigMgrPostRecoveryActions.html` nel server del sito ripristinato.

#### <a name="reenter-user-account-passwords-after-site-recovery"></a>Immettere nuovamente le password account utente dopo il ripristino del sito
1. Aprire la console di Configuration Manager e connettersi al sito ripristinato.  

2. Andare all'area di lavoro **Amministrazione**, espandere **Sicurezza** e quindi fare clic su **Account**.  

3. Per ogni account, seguire questa procedura per immette nuovamente la password:  

     1. Selezionare l'account dall'elenco identificato dopo il ripristino sito.  

     2. Fare clic su **Proprietà** nella barra multifunzione.  

     3. Nella scheda **Generale** fare clic su **Imposta**e quindi immettere nuovamente la password per l'account.  

     4. Fare clic su **Verifica**, selezionare l'origine dati appropriata per l'account utente selezionato e quindi fare clic su **Verifica connessione**. Questo passaggio consente di controllare che l'account utente possa connettersi all'origine dati e verifica le credenziali.  

     5. Fare clic su **OK** per salvare le modifiche alla password e quindi fare clic su **OK** per chiudere la pagina delle proprietà dell'account.  


### <a name="reenter-sideloading-keys"></a>Immettere nuovamente le chiavi di sideload

Dopo un ripristino del server del sito, immettere nuovamente le chiavi di sideload di Windows specificate per il sito. Queste chiavi vengono reimpostate durante il ripristino sito. Dopo aver immesso nuovamente le chiavi di sideload, il sito reimposta il conteggio nella colonna **Attivazioni usate** per le chiavi di sideload di Windows. 

Ad esempio, prima dell'errore del sito il conteggio **Attivazioni totali** è pari a **100**. Il numero di chiavi usate dal dispositivo, indicato in **Attivazioni utilizzate**, è pari a **90**. Dopo il ripristino del sito, **Attivazioni totali** visualizza ancora **100**, ma la colonna **Attivazioni usate** visualizza erroneamente **0**. Successivamente all'uso da parte di 10 nuovi dispositivi di una chiave di sideload, non esistono più chiavi di sideload e per l'undicesimo dispositivo non sarà possibile applicare una chiave di sideload.


### <a name="recreate-the-microsoft-intune-subscription"></a>Ricreare la sottoscrizione di Microsoft Intune

Se si ripristina un server del sito di Configuration Manager dopo aver ricreato l'immagine del server del sito, la sottoscrizione di Microsoft Intune non viene ripristinata. Dopo aver ripristinato il sito, riconnettersi alla sottoscrizione. Non creare una nuova richiesta APN. Caricare invece il file PEM valido corrente. Usare lo stesso file caricato l'ultima volta che è stata configurata o rinnovata la gestione iOS. Per ulteriori informazioni, vedere [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription).


### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Configurare SSL per i ruoli del sistema del sito che usano IIS

Quando si ripristinano sistemi del sito che eseguono IIS e che erano configurati per HTTPS, riconfigurare IIS per usare il certificato del server Web.


### <a name="reinstall-hotfixes"></a>Reinstallare gli aggiornamenti rapidi 

Dopo il ripristino di un sito, è necessario reinstallare gli [aggiornamenti rapidi fuori banda](/sccm/core/servers/manage/updates#bkmk_outofband) applicati al server del sito. Dopo il ripristino sito, visualizzare l'elenco degli aggiornamenti rapidi installati in precedenza nella pagina **Completato** dell'Installazione guidata. Questo elenco viene salvato anche in `C:\ConfigMgrPostRecoveryActions.html` nel server del sito ripristinato.


### <a name="recover-custom-reports"></a>Recuperare i report personalizzati 

Alcuni clienti creano report personalizzati in SQL Server Reporting Services. Quando si verifica un errore in questo componente, recuperare i report da un backup del server di report. Per altre informazioni sul ripristino dei report personalizzati in Reporting Services, vedere [Operazioni di backup e ripristino per Reporting Services](https://docs.microsoft.com/sql/reporting-services/install-windows/backup-and-restore-operations-for-reporting-services).


### <a name="recover-content-files"></a>Ripristinare i file di contenuto

Il database del sito tiene traccia di dove il server del sito archivia i file di contenuto. I file di contenuto in sé non sono sottoposti a backup o ripristino durante il processo di backup e ripristino. Per eseguire il ripristino completo dei file di contenuto, ripristinare i file di origine del pacchetto e la raccolta contenuto nel percorso originale. Esistono diversi metodi per ripristinare i file di contenuto. Il metodo più semplice consiste nel ripristinare i file da un backup del file system del server del sito.

Se non si ha un backup del file system per i file di origine pacchetto, copiarli o scaricarli manualmente. Questo processo è simile a quando si è creato il pacchetto in origine. Eseguire la query seguente in SQL Server per trovare il percorso di origine del pacchetto per tutti i pacchetti e le applicazioni: `SELECT * FROM v_Package`. Identificare il sito di origine del pacchetto esaminando i primi tre caratteri dell'ID di pacchetto. Ad esempio, se l'ID del pacchetto è CEN00001, il codice del sito per il sito di origine è CEN. I file di origine del pacchetto devono essere ripristinati nella stessa posizione in cui si trovavano prima dell'errore.

Se non si ha un backup del file system che includa la raccolta contenuto, eseguire una delle seguenti opzioni di ripristino:  

- **Importare un file di contenuti in versione di preproduzione**: in una gerarchia di Configuration Manager è possibile creare un file di contenuti in versione di preproduzione con tutti i pacchetti e le applicazioni da un altro percorso. Importare quindi il file di contenuti in versione di preproduzione per ripristinare la raccolta contenuto nel server del sito.  

- **Aggiornare il contenuto**: Configuration Manager copia il contenuto dall'origine del pacchetto alla raccolta contenuto. Per completare correttamente questa azione, è necessario che i file origine pacchetto siano disponibili nel percorso originale. Eseguire questa azione in ogni pacchetto e applicazione.


### <a name="recover-custom-software-updates"></a>Ripristinare gli aggiornamenti software personalizzati

Quando sono stati inclusi i file di database di System Center Updates Publisher nel piano di backup, è possibile ripristinare i database in caso di errore del computer Updates Publisher. Per altre informazioni su System Center Updates Publisher, vedere [System Center Updates Publisher](/sccm/sum/tools/updates-publisher).

#### <a name="restore-the-updates-publisher-database"></a>Ripristinare il database Updates Publisher
1. Reinstallare Updates Publisher nel computer ripristinato.  

2. Copiare il file di database **Scupdb.sdf** dalla destinazione di backup a `%USERPROFILE%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\` nel computer che esegue Updates Publisher.  

3. Quando più utenti eseguono Updates Publisher nel computer, copiare ogni file di database nel percorso del profilo utente appropriato.  


### <a name="user-state-migration-data"></a>Dati di migrazione sullo stato utente

Come parte delle proprietà del punto di migrazione stato, è possibile specificare le cartelle in cui vengono archiviati i dati dello stato utente. Dopo aver ripristinato un punto di migrazione stato, ripristinare manualmente i dati dello stato utente nel server. Ripristinarli nelle stesse cartelle in cui erano archiviati i dati prima dell'errore.


### <a name="regenerate-the-certificates-for-distribution-points"></a>Rigenerare i certificati per i punti di distribuzione

Dopo aver ripristinato un sito, **distmgr.log** potrebbe elencare la voce seguente per uno o più punti di distribuzione: `Failed to decrypt cert PFX data`. Questa voce indica che i dati del certificato del punto di distribuzione non possono essere decrittografati dal sito. Per risolvere questo problema, rigenerare o reimportare il certificato per i punti di distribuzione interessati. Usare il cmdlet[Set-CMDistributionPoint](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmdistributionpoint) di PowerShell.


### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Aggiornare i certificati usati per i punti di distribuzione basati sul cloud

Configuration Manager richiede un certificato di gestione di Azure per la comunicazione dal server del sito con i punti di distribuzione basati sul cloud. Dopo un ripristino del sito, aggiornare i certificati per i punti di distribuzione basati sul cloud.



## <a name="recover-a-secondary-site"></a>Ripristinare un sito secondario

Configuration Manager non supporta il backup del database in un sito secondario, ma supporta il ripristino mediante reinstallazione del sito secondario. Il ripristino del sito secondario è necessario quando si verifica un errore del sito secondario di Configuration Manager.


### <a name="requirements"></a>requisiti

- Il server deve soddisfare tutti i prerequisiti del sito secondario e deve avere i diritti di sicurezza appropriati configurati.  

- Usare lo stesso percorso di installazione usato per il sito in cui si è verificato l'errore.  

- Usare un server con la stessa configurazione del server in cui si è verificato l'errore. Questa configurazione include il nome di dominio completo (FQDN).  

- Il server deve avere la stessa configurazione di SQL Server del sito in cui si è verificato l'errore.  

     - Durante il ripristino di un sito secondario, Configuration Manager non installa SQL Server Express, se questo non è già installato nel computer.  

     - Usare la stessa versione di SQL Server e la stessa istanza di SQL Server usate per il database del sito secondario prima dell'errore.  


### <a name="procedure"></a>Procedura

Usare l'azione **Ripristina sito secondario** dal nodo **Siti** nella console di Configuration Manager. A differenza di altri tipi di siti, il ripristino di un sito secondario non usa un file di backup. Questo processo reinstalla i file del sito secondario nel server in cui si è verificato l'errore. Dopo la reinstallazione del sito, i dati del sito secondario vengono reinizializzati dal sito primario padre.

Durante il processo di ripristino, Configuration Manager verifica se la raccolta contenuto esiste nel server del sito secondario. Controlla anche che il contenuto appropriato sia disponibile. Il sito secondario usa la raccolta contenuto esistente, se questa include il contenuto appropriato. In caso contrario, per ripristinare la raccolta contenuto di un sito secondario, ridistribuire o pre-installare il contenuto nel server.

Quando si ha un punto di distribuzione che non si trova nel server del sito secondario, non è necessario reinstallare il punto di distribuzione durante un ripristino del sito secondario. Dopo il ripristino del sito secondario il sito si sincronizza automaticamente con il punto di distribuzione.

È possibile verificare lo stato del sito secondario usando l'azione **Mostra stato installazione** dal nodo **Siti** nella console di Configuration Manager.

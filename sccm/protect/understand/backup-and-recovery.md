---
title: Backup e ripristino | Microsoft Docs
description: Informazioni su come eseguire il backup e ripristinare i siti in caso di errore o perdita di dati in System Center Configuration Manager.
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7832d83-9ae2-4530-8a77-790e0845e12f
caps.latest.revision: 22
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: ea6668ee7ee6b209b659426a0dc2c0be605ceaf1
ms.lasthandoff: 03/27/2017

---

# <a name="backup-and-recovery"></a>Backup e ripristino

*Si applica a: System Center Configuration Manager (Current Branch)*

Preparare gli approcci di backup e ripristino per evitare la perdita di dati. Per i siti di Configuration Manager un approccio di backup e ripristino consente di ripristinare siti e gerarchie più rapidamente e con la minore perdita di dati. Le sezioni di questo argomento possono essere utili per eseguire il backup dei siti e ripristinare un sito in caso di errore del sito o perdita di dati.  



- [Eseguire il backup di un sito di Configuration Manager](#BKMK_SiteBackup)   

  - [Attività di manutenzione di backup](#BKMK_BackupMaintenanceTask)   

  - [Utilizzo di Data Protection Manager per eseguire il backup del database del sito](#BKMK_DPMBackup)   

  -  [Archiviazione dello snapshot di backup](#BKMK_ArchivingBackupSnapshot)   

  -  [Uso del file AfterBackup.bat](#BKMK_UsingAfterBackup)   

  -  [Attività di backup supplementari](#BKMK_SupplementalBackup)   

-  [Ripristinare un sito di Configuration Manager](#BKMK_RecoverSite)   

  -   [Determinare le opzioni di ripristino](#BKMK_DetermineRecoveryOptions)   

         -   [Opzioni di ripristino del server del sito](#BKMK_SiteServerRecoveryOptions)   

         -   [Opzioni di ripristino del database del sito](#BKMK_SiteDatabaseRecoveryOption)   

         -   [Periodo di memorizzazione del rilevamento modifiche di SQL Server](#bkmk_SQLretention)   

         -   [Processo per reinizializzare dati globali o del sito.](#bkmk_reinit)   

         -   [Scenari di ripristino del database del sito](#BKMK_SiteDBRecoveryScenarios)  

  -   [Chiavi del file di script di ripristino del sito automatico](#BKMK_UnattendedSiteRecoveryKeys)  

  -   [Attività post-ripristino](#BKMK_PostRecovery)  

  -   [Ripristinare un sito secondario](#BKMK_RecoverSecondarySite)  

-   [Servizio SMS Writer](#BKMK_SMSWriterService)  

> [!NOTE]  
>  Se si usa un gruppo di disponibilità SQL Server AlwaysOn per ospitare il database del sito, modificare i piani di backup e ripristino come descritto nella sezione [Modifiche a Backup e ripristino quando si usa un gruppo di disponibilità SQL Server AlwaysOn](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md#bkmk_BnR) dell'argomento [SQL Server AlwaysOn per database del sito a disponibilità elevata per System Center Configuration Manager](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

##  <a name="BKMK_SiteBackup"></a> Eseguire il backup di un sito di Configuration Manager  
 Configuration Manager prevede un'attività di manutenzione di backup che:  

-   Viene eseguita in base a una pianificazione  

-   Esegue il backup del database del sito  

-   Esegue il backup di chiavi del Registro di sistema specifiche  

-   Esegue il backup di cartelle e file specifici  

-   Esegue il backup della cartella **CD.Latest**. Vedere [Cartella CD.Latest per System Center Configuration Manager](../../core/servers/manage/the-cd.latest-folder.md).  

 Pianificare l'esecuzione dell'attività di backup del sito predefinita almeno ogni cinque giorni. Il motivo è che Configuration Manager usa un [periodo di conservazione del rilevamento delle modifiche di SQL Server](#bkmk_SQLretention) di cinque giorni.  

 Per semplificare il processo di backup, è possibile creare un file **AfterBackup.bat** per eseguire automaticamente azioni post-backup dopo la corretta esecuzione dell'attività di manutenzione di backup. Il file AfterBackup.bat viene usato di solito per archiviare lo snapshot di backup in una posizione sicura. È inoltre possibile usare il file AfterBackup.bat per copiare i file nella cartella di backup e avviare attività di backup supplementari.

Usare le seguenti sezioni per creare la strategia di backup di Configuration Manager.  

> [!NOTE]  
>  Configuration Manager è in grado di ripristinare il database del sito dall'attività di manutenzione di backup di Configuration Manager oppure da un backup del database del sito creato mediante un altro processo. Ad esempio, è possibile ripristinare il database del sito da un backup creato all'interno di un piano di manutenzione di Microsoft SQL Server. È possibile ripristinare il database del sito da un backup creato usando System Center 2012 Data Protection Manager (DPM). Per altre informazioni, vedere [Utilizzo di Data Protection Manager per eseguire il backup del database del sito](#BKMK_DPMBackup).  

###  <a name="BKMK_BackupMaintenanceTask"></a> Attività di manutenzione di backup  
 È possibile automatizzare il backup per i siti di Configuration Manager mediante la programmazione dell'attività di manutenzione Backup server sito predefinita. È possibile eseguire il backup di un sito di amministrazione centrale e di un sito primario, ma per i siti secondari o i server di sistema del sito il backup non è supportato. Durante l'esecuzione del servizio di backup di Configuration Manager vengono seguite le istruzioni definite nel file di controllo del backup (**&lt;CartellaInstallazioneConfigMgr\>\Inboxes\Smsbkup.box\Smsbkup.ctl**). È possibile modificare il file di controllo del backup per modificare il comportamento del servizio di backup. Le informazioni sullo stato di backup del sito vengono scritte nel file **Smsbkup.log** . Questo file viene creato nella cartella di destinazione specificata nelle proprietà dell'attività di manutenzione di Backup server sito.  


##### <a name="to-enable-the-site-backup-maintenance-task"></a>Per attivare l'attività di manutenzione di backup del sito  

1.  Nella console di Configuration Manager aprire **Amministrazione** > **Configurazione del sito**  

     \> **Siti**.  

2.  Selezionare il sito in cui si desidera attivare l'attività di manutenzione di backup del sito.  

3.  Nella scheda **Home**, nel gruppo **Impostazioni**, selezionare **Attività di manutenzione sito**.  

4.  Scegliere **Backup server sito**  >  **Modifica**.  

5.  Selezionare **Abilita questa attività** > **Imposta percorsi** per specificare la destinazione di backup. Sono disponibili le seguenti opzioni:  

    > [!IMPORTANT]  
    >  Per impedire la manomissione dei file di backup, archiviare i file in una posizione sicura. Il percorso di backup più sicuro è un'unità locale, che consente di impostare le autorizzazioni del file system NTFS nella cartella. Configuration Manager non esegue la crittografia dei dati di backup archiviati nel percorso di backup.  

    -   **Unità locale nel server del sito per il database e i dati del sito**: specifica che i file di backup per il sito e il database del sito vengono archiviati nel percorso indicato nel disco rigido locale del server del sito. È necessario creare la cartella locale prima dell'esecuzione dell'attività di backup. L'account di sistema locale nel server del sito deve disporre delle autorizzazioni del file system NTFS di **Scrittura** nella cartella locale per il backup del server del sito. L'account di sistema locale nel computer che esegue SQL Server deve disporre delle autorizzazioni NTFS di **Scrittura** nella cartella per il backup database del sito.  

    -   **Percorso di rete (nome UNC) per il database e i dati del sito**: specifica che i file di backup per il sito e il database del sito vengono archiviati nel percorso UNC indicato. È necessario creare la condivisione prima dell'esecuzione dell'attività di backup. L'account computer del server del sito e l'account computer di SQL Server, se SQL Server è installato in un altro computer, devono disporre delle autorizzazioni di condivisione e NTFS di **Scrittura** nella cartella di rete condivisa.  

    -   **Unità locali nel server del sito e in SQL Server**: specifica che i file di backup per il sito vengono archiviati nel percorso indicato nell'unità locale del server del sito, mentre i file di backup per il database del sito vengono archiviati nel percorso indicato nell'unità locale del server di database del sito. È necessario creare le cartelle locali prima dell'esecuzione dell'attività di backup. L'account computer del server del sito deve disporre delle autorizzazioni NTFS di **Scrittura** nella cartella creata nel server del sito. L'account computer di SQL Server deve disporre delle autorizzazioni NTFS di **Scrittura** nella cartella creata nel server di database del sito. Questa opzione è disponibile solo quando il database del sito non è installato nel server del sito.  

    > [!NOTE]  
    >    - L'opzione per selezionare la destinazione di backup è disponibile solo quando si specifica il percorso UNC della destinazione di backup.

    > - Il nome della cartella o il nome condivisione usato per la destinazione di backup non supporta l'utilizzo di caratteri Unicode.  


6.  Configurare una pianificazione per l'attività di backup del sito. Come procedura ottimale, è consigliabile valutare una pianificazione di backup in orari non lavorativi. Se si dispone di una gerarchia, valutare una pianificazione da eseguire almeno due volte a settimana per garantire la massima conservazione dei dati in caso di errore del sito.  

    Quando la console di Configuration Manager viene eseguita nello stesso server del sito configurato per il backup, l'attività di manutenzione Backup server sito usa l'ora locale per la pianificazione. Quando la console di Configuration Manager viene eseguita da un computer in remoto rispetto al sito configurato per il backup, l'attività di manutenzione Backup server sito usa l'ora UTC per la pianificazione.  

7.  Scegliere se creare un avviso in caso di errore dell'attività di backup del sito, fare clic su **OK**, quindi su **OK**. Se l'opzione è selezionata, Configuration Manager crea un avviso critico per l'errore di backup che è possibile esaminare nel nodo **Avvisi** dell'area di lavoro **Monitoraggio**.  

 Successivamente verificare che l'attività di manutenzione Backup server sito sia in esecuzione, per garantire che i backup vengano creati.  

##### <a name="to-verify-that-the-backup-site-server-maintenance-task-is-running"></a>Per verificare che l'attività di manutenzione Backup server sito sia stata completata correttamente  

-   Accertarsi che l'attività di manutenzione Backup sito sia in esecuzione effettuando una delle verifiche seguenti:  

    -   Esaminare il timestamp nei file della cartella di destinazione del backup creata dall'attività di manutenzione Backup server sito. Verificare che il timestamp sia stato aggiornato con un orario corrispondente all'orario in cui è stata pianificata l'ultima esecuzione dell'attività.  

    -   Nel nodo **Stato componente** dell'area di lavoro **Monitoraggio** esaminare i messaggi di stato per SMS_SITE_BACKUP. Al termine del backup del sito verrà visualizzato il messaggio ID 5035, in cui viene indicato che il backup del sito è stato completato senza errori.  

    -   Se l'attività di manutenzione Backup server sito è configurata per la creazione di un avviso in caso di errore del backup, è possibile controllare il nodo **Avvisi** nell'area di lavoro **Monitoraggio** per verificare la presenza di errori.  

    -   In &lt;*CartellaInstallazioneConfigMgr*>\Logs esaminare Smsbkup.log per verificare la presenza di avvisi ed errori. Quando il backup del sito viene completato correttamente, viene visualizzato `Backup completed` con un timestamp e un ID messaggio `STATMSG: ID=5035`.  

    > [!TIP]  
    >  In caso di errore dell'attività di manutenzione di backup, è possibile riavviare l'attività di backup interrompendo e riavviando il servizio SMS_SITE_BACKUP.  

###  <a name="BKMK_DPMBackup"></a> Utilizzo di Data Protection Manager per eseguire il backup del database del sito  
 È possibile usare System Center 2012 Data Protection Manager (DPM) per eseguire il backup del database del sito. È necessario creare un nuovo gruppo di protezione in DPM per il computer del database del sito. Nella pagina **Seleziona membri del gruppo** della procedura guidata Crea nuovo gruppo protezione dati, selezionare il servizio SMS Writer dall'elenco di origine dei dati, quindi selezionare il database del sito come membro appropriato. Per altre informazioni sull'utilizzo di Data Protection Manager per il backup del database del sito, vedere [Data Protection Manager Documentation Library (Libreria di documentazione di Data Protection Manager)](http://go.microsoft.com/fwlink/?LinkId=272772) in TechNet.  

> [!IMPORTANT]  
>  Configuration Manager non supporta il backup DPM per un cluster SQL Server che usa un'istanza denominata ma supporta il backup DPM in un cluster SQL Server che usa l'istanza predefinita di SQL Server.  

 Dopo il ripristino del database del sito, seguire i passaggi della procedura di installazione per ripristinare il sito. Selezionare l'opzione di ripristino **Usa un database del sito ripristinato manualmente** per usare il database del sito ripristinato mediante Data Protection Manager.  

###  <a name="BKMK_ArchivingBackupSnapshot"></a> Archiviazione dello snapshot di backup  
 Durante la prima esecuzione dell'attività di manutenzione Backup server sito, viene creato lo snapshot di backup, che è possibile usare per il ripristino del server del sito in caso di errore. Quando l'attività di backup viene eseguita nuovamente durante i cicli successivi, viene creato un nuovo snapshot di backup che sovrascrive lo snapshot precedente. Di conseguenza, il sito dispone di un singolo snapshot di backup e non è possibile recuperare uno snapshot di backup precedente.  

 Come procedura consigliata, mantenere più archivi dello snapshot di backup per i seguenti motivi:  

-   I supporti di backup possono presentare problemi, venire smarriti o contenere solo un backup parziale. Il ripristino di un sito primario autonomo danneggiato da un vecchio backup è una soluzione migliore rispetto a un ripristino senza backup. Per un server sito in una gerarchia, il backup deve essere eseguito nel periodo di memorizzazione del rilevamento delle modifiche SQL Server, altrimenti il backup non è richiesto.  

-   È possibile che un danneggiamento del sito non venga rilevato per diversi cicli di backup. Potrebbe essere necessario usare lo snapshot di un backup precedente il danneggiamento del sito. Quanto detto si applica a un sito primario autonomo e ai siti in una gerarchia in cui il backup rientri nel periodo di memorizzazione del rilevamento delle modifiche SQL Server.  

-   Il sito potrebbe non avere alcuno snapshot di backup se, ad esempio, l'attività di manutenzione Backup server sito non fosse completata correttamente. Dal momento che l'attività di backup determina la rimozione dello snapshot di backup precedente prima di avviare il backup dei dati correnti, non ci sarà alcuno snapshot di backup valido.  

###  <a name="BKMK_UsingAfterBackup"></a> Uso del file AfterBackup.bat  
 Dopo aver eseguito correttamente il backup up del sito, l'attività Backup server sito prova a eseguire automaticamente un file denominato AfterBackup.bat. È necessario creare manualmente il file AfterBackup.bat in &lt;*CartellaInstallazioneConfigMgr*>\Inboxes\Smsbkup. Se un file AfterBackup.bat è già presente ed è memorizzato nella cartella corretta, il file viene eseguito automaticamente al termine dell'attività di backup. Il file AfterBackup.bat consente di archiviare lo snapshot di backup al termine di ogni operazione di backup e di eseguire automaticamente altre attività post-backup che non rientrano nell'attività di manutenzione Backup server sito. Il file AfterBackup.bat integra l'archivio e le operazioni di backup, assicurando che ogni nuovo snapshot di backup sia archiviato. Quando il file AfterBackup.bat non è presente, questo passaggio viene ignorato dall'attività di backup senza effetto sull'operazione di backup. Per verificare che l'attività di backup del sito abbia eseguito correttamente il file AfterBackup.bat, vedere il nodo **Stato componente** nell'area di lavoro **Monitoraggio** e rivedere i messaggi di stato per SMS_SITE_BACKUP. Quando l'attività avvia correttamente il file di comando AfterBackup.bat, viene visualizzato il messaggio ID 5040.  

> [!TIP]  
>  Per creare il file AfterBackup.bat per archiviare i file di backup del server del sito, è necessario usare uno strumento di comando copia nel file batch come Robocopy. Ad esempio, è possibile creare il file AfterBackup.bat e aggiungere nella prima riga un stringa simile a quella indicata di seguito: `Robocopy E:\ConfigMgr_Backup \\ServerName\ShareName\ConfigMgr_Backup /MIR`. Per altre informazioni su Robocopy, vedere la pagina Web di riferimento della riga di comando [Robocopy](http://go.microsoft.com/fwlink/p/?LinkId=228408) .  

 Sebbene il file AfterBackup.bat sia pensato principalmente per l'archiviazione di snapshot di backup, è possibile creare un file AfterBackup.bat che consenta di eseguire attività aggiuntive al termine di ogni operazione di backup.  

###  <a name="BKMK_SupplementalBackup"></a> Attività di backup supplementari  
 L'attività di manutenzione Backup server sito fornisce uno snapshot di backup per i file del server del sito e il database del sito. Tuttavia, quando si definisce una strategia di backup, occorre considerare anche altri elementi di cui non viene eseguito il backup. Per completare la strategia di backup di Configuration Manager usare le seguenti sezioni.  

#### <a name="back-up-custom-reporting-services-reports"></a>Eseguire il backup dei report di Reporting Services personalizzati  
 Dopo aver modificato dei report di Reporting Services predefiniti o aver creato dei report di Reporting Services personalizzati, la creazione di un backup per i file del database del server di report rappresenta una priorità nella strategia di backup. Il backup del server di report deve includere un backup dei file di origine per report e modelli, chiavi di crittografia, estensioni o assembly personalizzati, file di configurazione, visualizzazioni SQL Server personalizzate usate nei report personalizzati, stored procedure personalizzate e così via.  

> [!IMPORTANT]  
>  Quando Configuration Manager viene aggiornato a una versione più recente, i report predefiniti potrebbero essere sovrascritti da nuovi report. Se si modifica un report predefinito, eseguirne il backup e quindi ripristinare il report in Reporting Services.  

 Per altre informazioni sul backup dei report personalizzati in Reporting Services, vedere [Operazioni di backup e ripristino per Reporting Services](https://technet.microsoft.com/library/ms155814\(v=sql.120\).aspx) nella documentazione online di SQL Server 2014.  

#### <a name="backup-content-files"></a>Backup di file di contenuto  
 La raccolta contenuto in Configuration Manager è il luogo in cui vengono archiviati tutti i file di contenuto per aggiornamenti software, applicazioni, distribuzione di sistemi operativi e così via. La raccolta contenuto si trova sul server del sito e in corrispondenza di ogni punto di distribuzione. L'attività di manutenzione Backup server sito non include una copia di backup per la raccolta contenuto o i file di origine del pacchetto. Quando si verifica un errore sul server del sito, le informazioni sui file della raccolta contenuto vengono ripristinate nel database del sito, ma è necessario ripristinare la raccolta contenuto e i file di origine del pacchetto sul server del sito.  

-   **Raccolta contenuto**: la raccolta contenuto deve essere ripristinata prima di ridistribuire il contenuto nei punti di distribuzione. Quando si avvia la ridistribuzione del contenuto, Configuration Manager copia i file dalla raccolta contenuto sul server del sito nei punti di distribuzione. La raccolta contenuto per il server del sito si trova nella cartella SCCMContentLib, generalmente posizionata nell'unità con maggiore spazio su disco disponibile al momento dell'installazione del sito.  

-   **File di origine del pacchetto**: i file di origine del pacchetto devono essere ripristinati prima di aggiornare il contenuto nei punti di distribuzione. Quando si avvia un aggiornamento del contenuto, Configuration Manager copia i file nuovi o modificati dall'origine del pacchetto alla raccolta contenuto, che a sua volta li copia nei punti di distribuzione associati. È possibile eseguire la seguente query in SQL Server per trovare il percorso di origine del pacchetto per tutti i pacchetti e le applicazioni: `SELECT * FROM v_Package`. È possibile identificare il sito di origine del pacchetto esaminando i primi tre caratteri dell'ID di pacchetto. Ad esempio, se l'ID del pacchetto è CEN00001, il codice del sito per il sito di origine è CEN. I file di origine del pacchetto devono essere ripristinati nella stessa posizione in cui si trovavano prima dell'errore.  

 Verificare di aver incluso sia la raccolta contenuto sia i percorsi di origine del pacchetto nel backup del file system per il server del sito.  

#### <a name="back-up-custom-software-updates"></a>Eseguire il backup di aggiornamenti software personalizzati  
 System Center Updates Publisher 2011 è uno strumento autonomo che consente di pubblicare aggiornamenti software personalizzati in Windows Server Update Services (WSUS), sincronizzare gli aggiornamenti software di Configuration Manager, valutare la conformità degli aggiornamenti software e distribuire gli aggiornamenti software personalizzati ai client. Updates Publisher usa un database locale per il relativo repository degli aggiornamenti software. Quando si usa Updates Publisher per gestire gli aggiornamenti software personalizzati, stabilire se è necessario includere il database di Updates Publisher nel piano di backup. Per altre informazioni su Updates Publisher, vedere [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) nella Libreria TechCenter di System Center.  

 Per eseguire il backup del database Updates Publisher usare la procedura seguente.  

###### <a name="to-back-up-the-updates-publisher-2011-database"></a>Per eseguire il backup del database di Updates Publisher 2011  

1.  Sul computer su cui è in esecuzione Updates Publisher individuare il file del database Updates Publisher (Scupdb.sdf) in %*PROFILOUTENTE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\\. Esiste un file di database diverso per ogni utente che esegue Updates Publisher.  

2.  Copiare il file di database nella destinazione di backup. Ad esempio, se la destinazione di backup è E:\ConfigMgr_Backup, è possibile copiare il file di database di Updates Publisher in E:\ConfigMgr_Backup\SCUP2011.  

    > [!TIP]  
    >  In presenza di più file di database su un computer, archiviare eventualmente il file in una sottocartella che indichi il profilo associato con il file di database. Ad esempio, si potrebbe avere un file di database in E:\ConfigMgr_Backup\SCUP2011\User1 e un altro file di database in E:\ConfigMgr_Backup\SCUP2011\User2.  

### <a name="user-state-migration-data"></a>Dati di migrazione sullo stato utente  
 È possibile usare le sequenze attività di Configuration Manager per acquisire e ripristinare i dati sullo stato utente in scenari di distribuzione del sistema operativo in cui si desidera mantenere lo stato utente del sistema operativo corrente. Le cartelle che contengono i dati sullo stato dell'utente sono elencate nelle proprietà del punto di migrazione dello stato. Non è previsto il backup di questi dati di migrazione sullo stato utente nell'ambito dell'attività di manutenzione Backup server sito. Come parte del piano di backup, è necessario eseguire manualmente il backup delle cartelle in cui si è specificato di archiviare i dati di migrazione sullo stato dell'utente.   

#### <a name="to-determine-the-folders-used-to-store-user-state-migration-data"></a>Per determinare le cartelle usate per l'archiviazione dei dati di migrazione sullo stato dell'utente  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Configurazione del sito** e scegliere **Server e ruoli del sistema del sito**.  

3.  Selezionare il sistema del sito che ospita il ruolo migrazione stato, quindi selezionare **Punto di migrazione stato** in **Ruoli sistema del sito**.  


4.  Nella scheda **Ruolo del sito** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  
5.  Nella sezione **Dettagli cartella** della scheda **Generale** vengono elencate le cartelle in cui sono archiviati i dati di migrazione sullo stato dell'utente.  

## <a name="recover-a-configuration-manager-site"></a>Ripristinare un sito di Configuration Manager
 È necessario ripristinare un sito di Configuration Manager ogni volta che si verifica un errore nel sito di Configuration Manager o una perdita di dati nel database del sito. La riparazione e la risincronizzazione dei dati sono le attività principali del ripristino di un sito e sono necessarie per evitare l'interruzione delle operazioni.  

> [!IMPORTANT]  
>  Quando si ripristina il database per un sito:  

>  -   È necessario usare la stessa versione ed edizione di SQL Server. Ad esempio, il ripristino di un database eseguito in SQL Server dalla versione 2012 alla 2014 non è supportato. Analogamente, non è supportato il ripristino di un database del sito eseguito in SQL Server dall'edizione Standard 2014 all'edizione Enterprise 2014.  
> -   SQL Server non deve essere impostato sulla **modalità utente singolo**.  
> -   Assicurarsi che i file MDF e LDF siano validi. Quando si ripristina un sito, non viene eseguita alcuna verifica dello stato dei file da ripristinare.  


 Il ripristino del sito viene avviato eseguendo l'Installazione guidata di Configuration Manager dalla cartella CD.Latest.  È anche possibile configurare lo script di installazione automatica e quindi usare l'opzione **/script** del comando di installazione per eseguire l'installazione da questa stessa cartella CD.Latest. Le opzioni di ripristino variano a seconda che si disponga o meno di un backup del database del sito di Configuration Manager. Per altre informazioni, vedere [Cartella CD.Latest per System Center Configuration Manager](../../core/servers/manage/the-cd.latest-folder.md).  

> [!IMPORTANT]  
>  Se si esegue il programma di installazione di Configuration Manager dal menu **Start** sul server del sito, l'opzione **Ripristina un sito** non sarà disponibile.  

>  Se sono stati installati aggiornamenti dalla console di Configuration Manager prima di eseguire il backup, non è possibile reinstallare il sito usando il programma di installazione dai supporti di installazione o dal percorso di installazione di Configuration Manager.  

> [!NOTE]  
>  Dopo aver ripristinato il database di un sito che era stato configurato per le repliche di database, prima di poter usare le repliche è necessario riconfigurare ciascuna replica del database, ricreando sia le pubblicazioni sia le sottoscrizioni.  

###  <a name="BKMK_DetermineRecoveryOptions"></a> Determinare le opzioni di ripristino  
 Ci sono due aree principali da tenere in considerazione per il ripristino del sito di amministrazione centrale e del server del sito primario di Configuration Manager: il server del sito e il database del sito. Usare le sezioni seguenti per determinare le opzioni da selezionare per lo scenario di ripristino.  

> [!NOTE]  

####  <a name="BKMK_SiteServerRecoveryOptions"></a> Opzioni di ripristino del server del sito  
 È necessario avviare il programma di installazione da una copia della cartella CD.Latest creata esternamente alla cartella di installazione di Configuration Manager. Selezionare quindi l'opzione **Ripristina un sito** . Quando si esegue il programma di installazione, sono disponibili le seguenti opzioni di ripristino per il server del sito in cui si è verificato un errore:  

-   **Ripristina il server di sito utilizzando un backup esistente**: usare questa opzione quando è disponibile un backup del server del sito di Configuration Manager creato nel server del sito come parte dell'attività di manutenzione **Backup server sito** prima dell'errore del sito. Il sito viene reinstallato e vengono configurate le relative impostazioni in base al sito di cui era stato eseguito il backup.  

-   **Reinstalla il server del sito**: usare questa opzione quando non è disponibile un backup del server del sito. Il server del sito viene reinstallato ed è necessario specificare le impostazioni del sito come nella procedura di installazione iniziale. Per ripristinare correttamente il sito, è necessario usare lo stesso codice sito e nome del database del sito usati durante l'installazione iniziale del sito su cui si è verificato l'errore.  

> [!NOTE]  
>  Quando il programma di installazione rileva la presenza di un sito di Configuration Manager sul server, è possibile avviare un ripristino del sito, sebbene le opzioni di ripristino per il server del sito siano limitate. Ad esempio, se si esegue il programma di installazione su un server del sito esistente, scegliendo l'operazione di ripristino è possibile recuperare il server di database del sito, ma l'opzione di ripristino del server del sito è disabilitata.  

####  <a name="BKMK_SiteDatabaseRecoveryOption"></a> Opzioni di ripristino del database del sito  
 Quando si esegue il programma di installazione, sono disponibili le seguenti opzioni di ripristino per il database del sito:  

-   **Ripristina il database del sito usando il set di backup**: usare questa opzione quando è disponibile un backup del database del sito di Configuration Manager creato come parte dell'attività di manutenzione **Backup server sito** in esecuzione nel sito prima dell'errore del database del sito. Quando si dispone di una gerarchia, le modifiche apportate al database del sito dopo l'ultimo backup del database del sito vengono recuperate dal sito di amministrazione centrale per un sito primario o da un sito primario di riferimento per un sito di amministrazione centrale. Quando si ripristina il database del sito per un sito primario autonomo, si perdono le modifiche apportate al sito dopo l'ultimo backup.  

     Quando si ripristina il database del sito per un sito in una gerarchia, il comportamento di ripristino è differente per un sito di amministrazione centrale o un sito primario e a seconda del fatto che l'ultimo backup rientri o meno nel periodo di memorizzazione del rilevamento delle modifiche SQL Server. Per altre informazioni, vedere la sezione [Scenari di ripristino del database del sito](#BKMK_SiteDBRecoveryScenarios) in questo argomento.  

    > [!NOTE]  
    >  Il ripristino non riesce se si sceglie di ripristinare il database del sito usando un set di backup ma il database del sito è già esistente.  

-   **Crea un nuovo database per il sito**: usare questa opzione quando non è disponibile un backup del database del sito di Configuration Manager. Quando si dispone di una gerarchia, viene creato un nuovo database del sito e i dati vengono ripristinati usando i dati replicati del sito di amministrazione centrale per un sito primario, oppure di un sito primario di riferimento per un sito di amministrazione centrale. Questa opzione non è disponibile quando si ripristina un sito primario autonomo o un sito di amministrazione centrale che non dispone di siti primari.  

-   **Utilizza un database del sito ripristinato manualmente**: usare questa opzione quando è già stato eseguito il ripristino del database del sito di Configuration Manager, ma è necessario completare il processo di ripristino. Configuration Manager è in grado di ripristinare il database del sito dall'attività di manutenzione di backup di Configuration Manager oppure da un backup del database del sito eseguito mediante DPM o un altro processo. Dopo il ripristino del database del sito mediante un metodo esterno a Configuration Manager, è necessario eseguire il programma di installazione e selezionare questa opzione per completare il ripristino del database del sito. Quando si dispone di una gerarchia, le modifiche apportate al database del sito dopo l'ultimo backup del database del sito vengono recuperate dal sito di amministrazione centrale per un sito primario o da un sito primario di riferimento per un sito di amministrazione centrale. Quando si ripristina il database del sito per un sito primario autonomo, si perdono le modifiche apportate al sito dopo l'ultimo backup.  

    > [!NOTE]  
    >  Quando si usa DPM per il backup del database del sito, usare le procedure DPM per ripristinare il database del sito in una posizione specifica prima di continuare il processo di ripristino in Configuration Manager. Per altre informazioni su DPM, vedere [Data Protection Manager Documentation Library (Libreria di documentazione di Data Protection Manager)](http://go.microsoft.com/fwlink/?LinkId=272772) in TechNet.  

-   **Ignora ripristino database**: usare questa opzione quando non si è verificata alcuna perdita di dati nel server di database del sito di Configuration Manager. Questa opzione è valida solo quando il database del sito si trova in un computer diverso rispetto al server del sito che si desidera ripristinare.  

####  <a name="bkmk_SQLretention"></a> Periodo di memorizzazione del rilevamento modifiche di SQL Server  
 Il rilevamento delle modifiche è abilitato per il database del sito in SQL Server. Il rilevamento delle modifiche consente a Configuration Manager di eseguire query per informazioni sulle modifiche apportate alle tabelle di database in seguito a un momento precedente. Il periodo di memorizzazione specifica per quanto tempo verranno conservate le informazioni di rilevamento delle modifiche. Per impostazione predefinita, il database del sito è configurato per un periodo di memorizzazione di 5 giorni. Quando si ripristina un database del sito, il processo di ripristino viene eseguito in modo diverso a seconda che il backup rientri o meno nel periodo di memorizzazione. Se, ad esempio, nel server di database del sito si verifica un errore e l'ultimo backup risale a 7 giorni fa, il backup è esterno al periodo di memorizzazione.

 Per altre informazioni sui meccanismi interni di rilevamento delle modifiche di SQL Server, vedere i post di blog seguenti del team di SQL Server: [Change Tracking Cleanup - part 1](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-1) (Pulizia del rilevamento modifiche - parte 1) e [Change Tracking Cleanup - part 2](https://blogs.msdn.microsoft.com/sql_server_team/change-tracking-cleanup-part-2) (Pulizia del rilevamento modifiche - parte 2).



####  <a name="bkmk_reinit"></a> Processo per reinizializzare dati globali o del sito.  
 Il processo per reinizializzare i dati globali o i dati del sito sostituisce i dati esistenti nel database del sito con i dati di un altro database del sito. Quando ad esempio il sito ABC reinizializza i dati dal sito XYZ, vengono eseguiti i seguenti passaggi:  

-   I dati vengono copiati dal sito XYZ al sito ABC.  

-   I dati esistenti per il sito XYZ vengono rimossi dal database del sito nel sito ABC.  

-   I dati copiati dal sito XYZ vengono inseriti nel database del sito per il sito ABC.  

##### <a name="example-scenario-1"></a>Scenario di esempio 1  
 **Il sito primario reinizializza i dati globali dal sito di amministrazione centrale**: il processo di ripristino rimuove i dati globali esistenti per il sito primario nel database del sito primario e li sostituisce con i dati globali copiati dal sito di amministrazione centrale.  

##### <a name="example-scenario-2"></a>Scenario di esempio 2  
 **Il sito di amministrazione centrale reinizializza i dati del sito da un sito primario**: il processo di ripristino rimuove i dati del sito esistenti per il sito primario nel database del sito di amministrazione centrale e li sostituisce con i dati del sito copiati dal sito primario. I dati del sito per altri siti primari non sono interessati.  

####  <a name="BKMK_SiteDBRecoveryScenarios"></a> Scenari di ripristino del database del sito  
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

### <a name="site-recovery-procedures"></a>Procedure di ripristino del sito  
 Usare una delle seguenti procedure per ripristinare il server del sito e il database del sito.  

##### <a name="to-start-a-site-recovery-in-the-setup-wizard"></a>Per avviare un ripristino del sito nell'Installazione guidata  

1.  Copiare la cartella CD.Latest in un percorso esterno alla cartella di installazione di Configuration Manager. Vedere [Cartella CD.Latest per System Center Configuration Manager](../../core/servers/manage/the-cd.latest-folder.md).  

     Dalla copia della cartella CD.Latest eseguire l'Installazione guidata di Configuration Manager.  

2.  Nella pagina **Riquadro attività iniziale** selezionare **Ripristina un sito**, quindi fare clic su **Avanti**.  

3.  Completare la procedura guidata usando le opzioni appropriate per il ripristino del sito.  

    > [!IMPORTANT]  
    >  Durante il ripristino, il programma di installazione identifica la porta di SQL Server Service Broker (SSB) usata da SQL Server. Se questa impostazione porta viene modificata durante il ripristino, la replica dei dati non verrà eseguita correttamente al termine del ripristino.  

    > [!NOTE]  
    >  È possibile specificare il percorso originale o uno nuovo da usare per l'installazione di Configuration Manager nell'Installazione guidata.  

##### <a name="to-start-an-unattended-site-recovery"></a>Per avviare un ripristino del sito automatico  

1.  Preparare lo script di installazione automatica per le opzioni richieste per il ripristino del sito.  

2.  Eseguire il programma di installazione di Configuration Manager con l'opzione di comando **/script**. Se, ad esempio, il file di inizializzazione dell'installazione è stato denominato ConfigMgrUnattend.ini e salvato nella directory C:\Temp del computer in cui viene eseguito il programma di installazione, il comando sarà: **Setup /script C:\temp\ConfigMgrUnattend.ini**.  

> [!NOTE]  
>  Dopo aver ripristinato un sito di amministrazione centrale, potrebbe non essere possibile stabilire la replica di alcuni dati del sito da siti figlio. Sono inclusi, tra gli altri, l'inventario hardware, l'inventario software e i messaggi di stato.  
>   
>  In tal caso è necessario reinizializzare **ConfigMgrDRSSiteQueue** per la replica di database.  A tale scopo, usare **SQL Server Manager** per eseguire la query riportata di seguito nel database del sito di Configuration Manager nel sito di amministrazione centrale:  
>   
>  **IF EXISTS (SELECT \* FROM sys.service_queues WHERE name = 'ConfigMgrDRSSiteQueue' AND is_receive_enabled = 0)**  
>   
>  **ALTER QUEUE [dbo].[ConfigMgrDRSSiteQueue] WITH STATUS = ON**  

###  <a name="BKMK_UnattendedSiteRecoveryKeys"></a> Chiavi del file di script di ripristino del sito automatico  
 Per eseguire un ripristino automatico di un sito di amministrazione centrale o di un sito primario di Configuration Manager, è possibile creare uno script di installazione automatica e usare il programma di installazione con l'opzione di comando /script. Lo script fornisce lo stesso tipo di informazioni richieste dall'Installazione guidata, ma non prevede impostazioni predefinite. Per le chiavi di installazione applicabili al tipo di ripristino che si usa, è necessario specificare tutti i valori.  

 È possibile eseguire il programma di installazione automatica di Configuration Manager usando un file di inizializzazione con l'opzione di installazione da riga di comando /script. L'installazione automatica è supportata per il ripristino di un sito di amministrazione centrale e di un sito primario di Configuration Manager. Per usare l'opzione di installazione da riga di comando /script, è necessario creare un file di inizializzazione e specificarne il nome dopo l'opzione di installazione da riga di comando /script. Il nome del file non è rilevante, purché l'estensione del nome file sia INI. Quando si fa riferimento a file di inizializzazione dell'installazione dalla riga di comando, è necessario specificare il percorso completo del file. Se ad esempio il file di inizializzazione dell'installazione è denominato setup.ini e viene archiviato nella cartella C:\setup, la riga di comando sarà:  

 **setup /script c:\setup\setup.ini**.  

> [!IMPORTANT]  
>  È necessario disporre dei diritti di amministratore per eseguire il programma di installazione. Quando il programma di installazione viene eseguito con lo script automatico, è necessario avviare il prompt dei comandi in un contesto di amministrazione usando **Esegui come amministratore**.  

 Lo script contiene nomi di sezione, nomi delle chiavi e valori. I nomi delle chiavi di sezione richiesti variano a seconda del tipo di ripristino per cui si crea lo script. L'ordine delle chiavi all'interno delle sezioni e l'ordine delle sezioni all'interno del file non è rilevante. Alle chiavi non viene applicata la distinzione tra maiuscole e minuscole. Quando si specificano i valori per le chiavi, il nome della chiave deve essere seguito dal segno uguale (=) e dal valore della chiave.  

 Usare le seguenti sezioni per creare lo script per il ripristino automatico del sito. Nelle tabelle sono elencate le chiavi dello script di installazione, i relativi valori, se richiesti, il tipo di installazione per cui vengono usate e una breve descrizione relativa alla chiave.  

#### <a name="recover-a-central-administration-site-unattended"></a>Ripristinare un sito di amministrazione centrale in modo automatico  
 Usare le informazioni seguenti per configurare un file di script di installazione automatica per ripristinare un sito di amministrazione centrale.  

 **Identification**  

-   **Nome chiave:** Action  

    -   **Richiesto:** sì  

    -   **Valori:** RecoverCCAR  

    -   **Dettagli:** ripristina un sito di amministrazione centrale  

-   **Nome chiave:** CDLatest  

    -   **Richiesto:** sì, solo quando si usano supporti dalla cartella CD.Latest.    

    -   **Valori:** 1. Qualsiasi valore diverso da 1 presuppone che non venga usata la cartella CD.Latest.

    -   **Dettagli:** lo script deve includere la chiave e il valore quando si esegue il programma di installazione dal supporto di una cartella CD.Latest allo scopo di installare o ripristinare un sito di amministrazione centrale o primario. Questo valore indica al programma di installazione che viene usato il formato di supporto CD.Latest.  

**RecoveryOptions**  

-   **Nome chiave:** ServerRecoveryOptions  

    -   **Richiesto:** sì  

    -   **Valori:** 1, 2 o 4  

         1 = Ripristina il server del sito e SQL Server.  

         2 = Ripristina solo il server del sito.  

         4 = Ripristina solo SQL Server.  

    -   **Dettagli:** specifica se il programma di installazione ripristinerà il server del sito, SQL Server o entrambi. Le chiavi associate sono necessarie quando si imposta il valore seguente per l'impostazione ServerRecoveryOptions:  

        -   **Valore = 1** È possibile specificare un valore per la chiave **SiteServerBackupLocation** per il ripristino del sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

             La chiave **BackupLocation** è richiesta in caso di configurazione del valore **10** per la chiave **DatabaseRecoveryOptions** necessaria per il ripristino del database del sito dal backup.  

        -   **Valore = 2** È possibile specificare un valore per la chiave **SiteServerBackupLocation** per il ripristino del sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

        -   **Valore = 4** La chiave **BackupLocation** è richiesta in caso di configurazione del valore **10** per la chiave **DatabaseRecoveryOptions** necessaria per il ripristino del database del sito dal backup.  

-   **Nome chiave:** DatabaseRecoveryOptions  

    -   **Richiesto:** forse  

    -   **Valori:** 10, 20, 40, 80  

         10 = Ripristina il database del sito dal backup.  

         20 = Usa un database del sito che è stato ripristinato manualmente usando un altro metodo.  

         40 = Crea un nuovo database per il sito. Usare questa opzione quando non è disponibile alcun backup di database del sito. I dati globali e i dati del sito vengono ripristinati tramite la replica da altri siti.  

         80 = Ignora il ripristino del database.  

    -   **Dettagli:** specifica le modalità secondo cui il programma di installazione ripristinerà il database del sito in SQL Server. Questa chiave è richiesta quando l'impostazione **ServerRecoveryOptions** ha il valore **1** o **4**.  

-   **Nome chiave:** ReferenceSite  

    -   **Richiesto:** forse  

    -   **Valori:** &lt;FQDNSitoRiferimento\>  

    -   **Dettagli:** specifica il sito primario di riferimento usato dal sito di amministrazione centrale per il ripristino dei dati globali se il backup del database è antecedente al periodo di conservazione del rilevamento delle modifiche o se il sito viene ripristinato senza backup.  

         Se non viene specificato un sito di riferimento e il backup è antecedente al periodo di memorizzazione del rilevamento delle modifiche, tutti i siti primari vengono reinizializzati con i dati ripristinati dal sito di amministrazione centrale.  

         Se non viene specificato un sito di riferimento e il backup rientra nel periodo di memorizzazione del rilevamento delle modifiche, solo le modifiche apportate dal momento del backup verranno replicate dai siti primari. In caso di modifiche in conflitto provenienti da diversi siti primari, il sito di amministrazione centrale usa la prima modifica ricevuta.  

         Questa chiave è richiesta quando l'impostazione **DatabaseRecoveryOptions** ha il valore **40**.  

-   **Nome chiave:** SiteServerBackupLocation  

    -   **Richiesto:** no  

    -   **Valori:** &lt;PercorsoSetBackupServerSito\>  

    -   **Dettagli:** specifica il percorso del set di backup del server del sito. Questa chiave è facoltativa quando l'impostazione **ServerRecoveryOptions** ha il valore **1** o **2**. Specificare un valore affinché la chiave **SiteServerBackupLocation** ripristini il sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

-   **Nome chiave:** BackupLocation  

    -   **Richiesto:** forse  

    -   **Valori:** &lt;PercorsoSetBackupDatabaseSito\>  

    -   **Dettagli:** specifica il percorso del set di backup del database del sito. La chiave **BackupLocation** è richiesta quando viene configurato il valore **1** o **4** per la chiave **ServerRecoveryOptions** e viene configurato il valore **10** per la chiave **DatabaseRecoveryOptions** .  

**Opzioni**  

-   **Nome chiave:** ProductID  

    -   **Richiesto:** sì  

    -   **Valori:**  

         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  

         valutazione  

    -   **Dettagli:** codice Product Key per l'installazione di Configuration Manager, trattini inclusi. Immettere **Eval** per installare la versione di valutazione di Configuration Manager.  

-   **Nome chiave:** SiteCode  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;Codice del sito\>  

    -   **Dettagli:** tre caratteri alfanumerici che identificano in modo univoco il sito nella gerarchia. È necessario specificare il codice del sito usato dal sito prima dell'errore.  

-   **Nome chiave:** SiteName  

    -   **Richiesto:** sì  

    -   **Valori:** SiteName  

    -   **Dettagli:** descrizione del sito.  

-   **Nome chiave:** SMSInstallDir  

    -   **Richiesto:** sì  

    -   **Values:** &lt;*PercorsoInstallazioneConfigMg*>  

    -   **Dettagli:** specifica la cartella di installazione per i file di programma di Configuration Manager.  

        > [!NOTE]  
        >  È possibile specificare il percorso originale o uno nuovo da usare per l'installazione di Configuration Manager.  

-   **Nome chiave:** SDKServer  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;*FQDN del provider SMS*>  

    -   **Dettagli:** specifica l'FQDN del server che ospiterà il provider SMS. È necessario specificare il server che ospitava il provider SMS prima dell'errore.  

         Dopo l'installazione iniziale, è possibile configurare altri provider SMS per il sito.  

-   **Nome chiave:** PrerequisiteComp  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = scarica  

         1 = già scaricato  

    -   **Dettagli:** specifica se i file dei prerequisiti di installazione sono già stati scaricati. Se ad esempio si usa un valore pari a 0, il programma di installazione eseguirà il download dei file.  

-   **Nome chiave:** PrerequisitePath  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Dettagli:** specifica il percorso dei file dei prerequisiti di installazione. A seconda del valore di **PrerequisiteComp** , il programma di installazione usa questo percorso per archiviare i file scaricati oppure per individuare i file scaricati in precedenza.  

-   **Nome chiave:** AdminConsole  

    -   **Richiesto:** forse  

    -   **Valori:** 0 o 1  

         0 = non installare  

         1 = installa  

    -   **Dettagli:** specifica se installare la console di Configuration Manager. Questa chiave è necessaria tranne quando l'impostazione **ServerRecoveryOptions** ha valore **4**.  

-   **Nome chiave:** JoinCEIP  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = non partecipare  

         1 = partecipa  

    -   **Dettagli:** specifica se partecipare al programma Analisi utilizzo software.  

**SQLConfigOptions**  

-   **Nome chiave:** SQLServerName  

    -   **Richiesto:** sì  

    -   **Valori:** *&lt;NomeSQLServer\>*  

    -   **Dettagli:** nome del server, o nome dell'istanza in cluster, che esegue il sistema SQL Server in cui verrà ospitato il database del sito. È necessario specificare lo stesso server in cui era ospitato il database del sito prima dell'errore.  

-   **Nome chiave:** DatabaseName  

    -   **Richiesto:** sì  

    -   **Valori:**  

         *&lt;NomeDatabaseSito\>*  

         o  

         *&lt;NomeIstanza\>*\\*&lt;NomeDatabaseSito\>*  

    -   **Dettagli:** specifica il nome del database di SQL Server da creare o usare per installare il database del sito di amministrazione centrale. È necessario specificare lo stesso nome database usato prima dell'errore.  

        > [!IMPORTANT]  
        >  Se non si usa l'istanza predefinita, è necessario specificare il nome dell'istanza e il nome database del sito.  

-   **Nome chiave:** SQLSSBPort  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*NumeroPortaSSB*>  

    -   **Dettagli:** specifica la porta di SQL Server Service Broker (SSB) usata da SQL Server. In genere, SSB è configurato per usare la porta TCP 4022, ma sono supportate anche altre porte. È necessario specificare la stessa porta SSB usata prima dell'errore.  

#### <a name="recover-a-primary-site-unattended"></a>Ripristinare un sito primario automatico  
 Usare le informazioni seguenti per configurare un file di script di installazione automatica per ripristinare un sito di amministrazione centrale.  

 **Identification**  

-   **Nome chiave:** Action  

    -   **Richiesto:** sì  

    -   **Valori:** RecoverPrimarySite  

    -   **Dettagli:** ripristina un sito primario  

-   **Nome chiave:** CDLatest  

    -   **Richiesto:** sì, solo quando si usano supporti dalla cartella CD.Latest.    

    -   **Valori:** 1. Qualsiasi valore diverso da 1 presuppone che non venga usata la cartella CD.Latest.

    -   **Dettagli:** lo script deve includere la chiave e il valore quando si esegue il programma di installazione dal supporto di una cartella CD.Latest allo scopo di installare o ripristinare un sito di amministrazione centrale o primario. Questo valore indica al programma di installazione che viene usato il formato di supporto CD.Latest.

**RecoveryOptions**  

-   **Nome chiave:** ServerRecoveryOptions  

    -   **Richiesto:** sì  

    -   **Valori:** 1, 2 o 4  

         1 = Ripristina il server del sito e SQL Server.  

         2 = Ripristina solo il server del sito.  

         4 = Ripristina solo SQL Server.  

    -   **Dettagli:** specifica se il programma di installazione ripristinerà il server del sito, SQL Server o entrambi. Le chiavi associate sono necessarie quando si imposta il valore seguente per l'impostazione ServerRecoveryOptions:  

        -   **Valore = 1** È possibile specificare un valore per la chiave **SiteServerBackupLocation** per il ripristino del sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

             La chiave **BackupLocation** è richiesta in caso di configurazione del valore **10** per la chiave **DatabaseRecoveryOptions** necessaria per il ripristino del database del sito dal backup.  

        -   **Valore = 2** È possibile specificare un valore per la chiave **SiteServerBackupLocation** per il ripristino del sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

        -   **Valore = 4** La chiave **BackupLocation** è richiesta in caso di configurazione del valore **10** per la chiave **DatabaseRecoveryOptions** necessaria per il ripristino del database del sito dal backup.  

-   **Nome chiave:** DatabaseRecoveryOptions  

    -   **Richiesto:** forse  

    -   **Valori:** 10, 20, 40, 80  

         10 = Ripristina il database del sito dal backup.  

         20 = Usa un database del sito che è stato ripristinato manualmente usando un altro metodo.  

         40 = Crea un nuovo database per il sito. Usare questa opzione quando non è disponibile alcun backup di database del sito. I dati globali e i dati del sito vengono ripristinati tramite la replica da altri siti.  

         80 = Ignora il ripristino del database.  

    -   **Dettagli:** specifica le modalità secondo cui il programma di installazione ripristinerà il database del sito in SQL Server. Questa chiave è richiesta quando l'impostazione **ServerRecoveryOptions** ha il valore **1** o **4**.  

-   **Nome chiave:** SiteServerBackupLocation  

    -   **Richiesto:** no  

    -   **Valori:** &lt;PercorsoSetBackupServerSito\>  

    -   **Dettagli:** specifica il percorso del set di backup del server del sito. Questa chiave è facoltativa quando l'impostazione **ServerRecoveryOptions** ha il valore **1** o **2**. Specificare un valore affinché la chiave **SiteServerBackupLocation** ripristini il sito usando un backup del sito. Se non si specifica un valore, il sito viene reinstallato senza eseguire il ripristino da un set di backup.  

-   **Nome chiave:** BackupLocation  

    -   **Richiesto:** forse  

    -   **Valori:** &lt;PercorsoSetBackupDatabaseSito\>  

    -   **Dettagli:** specifica il percorso del set di backup del database del sito. La chiave **BackupLocation** è richiesta quando viene configurato il valore **1** o **4** per la chiave **ServerRecoveryOptions** e viene configurato il valore **10** per la chiave **DatabaseRecoveryOptions** .  

**Opzioni**  

-   **Nome chiave:** ProductID  

    -   **Richiesto:** sì  

    -   **Valori:**  

         xxxxx-xxxxx-xxxxx-xxxxx-xxxxx  

         valutazione  

    -   **Dettagli:** codice Product Key per l'installazione di Configuration Manager, trattini inclusi. Immettere **Eval** per installare la versione di valutazione di Configuration Manager.  

-   **Nome chiave:** SiteCode  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;Codice del sito\>  

    -   **Dettagli:** tre caratteri alfanumerici che identificano in modo univoco il sito nella gerarchia. È necessario specificare il codice del sito usato dal sito prima dell'errore.  

-   **Nome chiave:** SiteName  

    -   **Richiesto:** sì  

    -   **Valori:** SiteName  

    -   **Dettagli:** descrizione del sito.  

-   **Nome chiave:** SMSInstallDir  

    -   **Richiesto:** sì  

    -   **Values:** &lt;*PercorsoInstallazioneConfigMg*>  

    -   **Dettagli:** specifica la cartella di installazione per i file di programma di Configuration Manager.  

        > [!NOTE]  
        >  È possibile specificare il percorso originale o uno nuovo da usare per l'installazione di Configuration Manager.  

-   **Nome chiave:** SDKServer  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;*FQDN del provider SMS*>  

    -   **Dettagli:** specifica l'FQDN del server che ospiterà il provider SMS. È necessario specificare il server che ospitava il provider SMS prima dell'errore.  

         Dopo l'installazione iniziale, è possibile configurare altri provider SMS per il sito.  

-   **Nome chiave:** PrerequisiteComp  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = scarica  

         1 = già scaricato  

    -   **Dettagli:** specifica se i file dei prerequisiti di installazione sono già stati scaricati. Se ad esempio si usa un valore pari a 0, il programma di installazione eseguirà il download dei file.  

-   **Nome chiave:** PrerequisitePath  

    -   **Richiesto:** sì  

    -   **Valori:** &lt;*PathToSetupPrerequisiteFiles*>  

    -   **Dettagli:** specifica il percorso dei file dei prerequisiti di installazione. A seconda del valore di **PrerequisiteComp** , il programma di installazione usa questo percorso per archiviare i file scaricati oppure per individuare i file scaricati in precedenza.  

-   **Nome chiave:** AdminConsole  

    -   **Richiesto:** forse  

    -   **Valori:** 0 o 1  

         0 = non installare  

         1 = installa  

    -   **Dettagli:** specifica se installare la console di Configuration Manager. Questa chiave è necessaria tranne quando l'impostazione **ServerRecoveryOptions** ha valore **4**.  

-   **Nome chiave:** JoinCEIP  

    -   **Richiesto:** sì  

    -   **Valori:** 0 o 1  

         0 = non partecipare  

         1 = partecipa  

    -   **Dettagli:** specifica se partecipare al programma Analisi utilizzo software.  

**SQLConfigOptions**  

-   **Nome chiave:** SQLServerName  

    -   **Richiesto:** sì  

    -   **Valori:** *&lt;NomeSQLServer\>*  

    -   **Dettagli:** nome del server, o nome dell'istanza in cluster, che esegue il sistema SQL Server in cui verrà ospitato il database del sito. È necessario specificare lo stesso server in cui era ospitato il database del sito prima dell'errore.  

-   **Nome chiave:** DatabaseName  

    -   **Richiesto:** sì  

    -   **Valori:**  

         *&lt;NomeDatabaseSito\>*  

         o  

         *&lt;NomeIstanza\>*\\*&lt;NomeDatabaseSito\>*  

    -   **Dettagli:** specifica il nome del database di SQL Server da creare o usare per installare il database del sito di amministrazione centrale. È necessario specificare lo stesso nome database usato prima dell'errore.  

        > [!IMPORTANT]  
        >  Se non si usa l'istanza predefinita, è necessario specificare il nome dell'istanza e il nome database del sito.  

-   **Nome chiave:** SQLSSBPort  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*NumeroPortaSSB*>  

    -   **Dettagli:** specifica la porta di SQL Server Service Broker (SSB) usata da SQL Server. In genere, SSB è configurato per usare la porta TCP 4022, ma sono supportate anche altre porte. È necessario specificare la stessa porta SSB usata prima dell'errore.  

**Hierarchy ExpansionOption**  

-   **Nome chiave:** CCARSiteServer  

    -   **Richiesto:** forse  

    -   **Valori:** &lt;*CodiceSitoPerSitoAmministrazioneCentrale*>  

    -   **Dettagli:** specifica il sito di amministrazione centrale a cui si collegherà il sito primario quando verrà aggiunto alla gerarchia di Configuration Manager. Questa impostazione è necessaria se il sito primario era collegato a un sito di amministrazione centrale prima dell'errore. È necessario specificare il codice del sito usato dal sito di amministrazione centrale prima dell'errore.  

-   **Nome chiave:** CASRetryInterval  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*Intervallo*>  

    -   **Dettagli:** specifica l'intervallo (in minuti) tra i tentativi di connessione al sito di amministrazione centrale dopo l'errore di connessione. Se ad esempio si verifica un errore di connessione al sito di amministrazione centrale, il sito primario attende il numero di minuti specificato per CASRetryInterval e quindi tenta nuovamente di eseguire la connessione.  

-   **Nome chiave:** WaitForCASTimeout  

    -   **Richiesto:** no  

    -   **Valori:** &lt;*Timeout*>  

    -   **Dettagli:** specifica il valore di timeout massimo (in minuti) per la connessione di un sito primario al sito di amministrazione centrale. Se ad esempio un sito primario non riesce a connettersi al sito di amministrazione centrale, tale sito primario proverà nuovamente a connettersi al sito di amministrazione centrale in base a CASRetryInterval finché non viene raggiunto il periodo di WaitForCASTimeout. È possibile specificare un valore compreso tra 0 e 100.  

###  <a name="BKMK_PostRecovery"></a> Attività post-ripristino  
 Dopo aver eseguito il ripristino del sito, è necessario considerare diverse attività post-ripristino prima di completare il ripristino del sito. Usare le seguenti sezioni per completare il processo di ripristino del sito.  

#### <a name="re-enter-user-account-passwords"></a>Immettere di nuovo le password account utente  
 Dopo il ripristino di un server del sito, è necessario immettere nuovamente le password per gli account utente specificati per il sito perché vengono reimpostate durante il ripristino. Gli account vengono elencati nella pagina **Operazione completata** dell'Installazione guidata dopo aver completato il ripristino del sito e vengono salvati in C:\ConfigMgrPostRecoveryActions.html nel server del sito ripristinato.  

###### <a name="to-re-enter-user-account-passwords-after-site-recovery"></a>Per immettere nuovamente le password account utente dopo il ripristino del sito  

1.  Aprire la console di Configuration Manager e connettersi al sito ripristinato.  

2.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

3.  Nell'area di lavoro **Amministrazione** espandere **Sicurezza**e quindi fare clic su **Account**.  

4.  Per ogni account in cui è necessario immettere nuovamente la password, eseguire le seguenti operazioni:  

    1.  Selezionare l'account dall'elenco degli account individuati dopo il ripristino del sito. È possibile trovare questo elenco di C:\ConfigMgrPostRecoveryActions.html nel server del sito ripristinato.  

    2.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà** per aprire le proprietà dell'account.  

    3.  Nella scheda **Generale** fare clic su **Imposta**e quindi immettere nuovamente le password per l'account.  

    4.  Fare clic su **Verifica**, selezionare l'origine dati appropriata per l'account utente selezionato e quindi fare clic su **Verifica connessione** per verificare che l'account utente possa connettersi all'origine dati.  

    5.  Fare clic su **OK** per salvare le modifiche alle password e quindi fare clic su **OK**.  

#### <a name="re-enter-sideloading-keys"></a>Immettere nuovamente le chiavi di trasferimento locale  
 Dopo un ripristino del server di sito, è necessario immettere nuovamente le chiavi di trasferimento locale di Windows specificate per il sito perché queste vengono reimpostate durante il ripristino del sito. Dopo aver immesso nuovamente le chiavi di trasferimento locale, il conteggio nella colonna **Attivazioni usate** per le chiavi di trasferimento locale è reimpostato nella console di Configuration Manager. Supponiamo ad esempio che prima dell'errore del sito il conteggio **Attivazioni totali** sia impostato su **100** e **Attivazioni usate** su **90** per il numero di chiavi usate dai dispositivi. Dopo il ripristino del sito, la colonna **Attivazioni totali** visualizza ancora **100**, ma la colonna **Attivazioni usate** visualizza erroneamente **0**. Tuttavia successivamente all'uso da parte di 10 nuovi dispositivi di una chiave di trasferimento locale, non esisteranno chiavi di trasferimento locale residue e per il dispositivo successivo sarà impossibile applicare una chiave di trasferimento locale.  

#### <a name="recreate-the-microsoft-intune-subscription"></a>Ricreare la sottoscrizione di Microsoft Intune  
 Se si ripristina un server del sito di Configuration Manager dopo aver ricreato l'immagine del computer server del sito, la sottoscrizione di Microsoft Intune non viene ripristinata. Dopo aver ripristinato il sito, è necessario riconnettersi alla sottoscrizione.  Non creare una nuova richiesta di APN, ma caricare invece il file PEM valido corrente caricato in occasione dell'ultima configurazione o dell'ultimo rinnovo della gestione iOS. Per ulteriori informazioni, vedere [Configuring the Microsoft Intune subscription](/sccm/mdm/deploy-use/configure-intune-subscription).  

#### <a name="configure-ssl-for-site-system-roles-that-use-iis"></a>Configurare SSL per i ruoli del sistema del sito che usano IIS  
 Quando si ripristinano sistemi del sito che eseguono IIS e che erano configurati per HTTPS prima dell'errore, è necessario riconfigurare IIS per usare il certificato server Web.  

#### <a name="reinstall-hotfixes-in-the-recovered-site-server"></a>Reinstallare gli aggiornamenti rapidi nel server del sito ripristinato  
 Dopo il ripristino di un sito, è necessario reinstallare gli aggiornamenti rapidi applicati al server del sito. Un elenco degli aggiornamenti rapidi installati in precedenza è disponibile nella pagina **Operazione completata** dell'Installazione guidata dopo il ripristino del sito e viene salvato in **C:\ConfigMgrPostRecoveryActions.html** nel server del sito ripristinato.  

#### <a name="recover-custom-reports-on-the-computer-running-reporting-services"></a>Ripristinare i report personalizzati nel computer che esegue Reporting Services  
 Quando si creano dei report personalizzati di Reporting Services e si verifica un errore di Reporting Services, è possibile ripristinare i report quando si esegue il backup del server di report. Per altre informazioni sul ripristino dei report personalizzati in Reporting Services, vedere [Operazioni di backup e ripristino per un'installazione di Reporting Services](http://go.microsoft.com/fwlink/p/?LinkId=228724) nella documentazione online di SQL Server 2008.  

#### <a name="recover-content-files"></a>Ripristinare i file di contenuto  
 Il database del sito contiene informazioni sul percorso di archiviazione dei file di contenuto nel server del sito, ma non viene eseguito il backup né il ripristino di tali file di contenuto come parte del processo di backup e ripristino. Per eseguire il ripristino completo dei file di contenuto, è necessario ripristinare i file di origine del pacchetto e la raccolta contenuto nel percorso originale. Sono disponibili diversi metodi per il ripristino dei file di contenuto, ma il metodo più semplice è ripristinare i file da un backup del file system del server del sito.  

 Se non si dispone di un backup del file system per i file di origine del pacchetto, è necessario copiare o scaricare manualmente tali file come per il primo pacchetto creato in origine. È possibile eseguire la seguente query in SQL Server per trovare il percorso di origine del pacchetto per tutti i pacchetti e le applicazioni: `SELECT * FROM v_Package`. È possibile identificare il sito di origine del pacchetto esaminando i primi tre caratteri dell'ID di pacchetto. Ad esempio, se l'ID del pacchetto è CEN00001, il codice del sito per il sito di origine è CEN. I file di origine del pacchetto devono essere ripristinati nella stessa posizione in cui si trovavano prima dell'errore.  

 Se non si dispone di un backup del file system che contenga la raccolta contenuto, eseguire una delle seguenti opzioni di ripristino:  

-   **Importare un file di contenuti in versione di preproduzione**: quando è disponibile una gerarchia di Configuration Manager, è possibile creare un file di contenuti in versione di preproduzione con tutti i pacchetti e le applicazioni da un altro percorso e quindi importare questo file per ripristinare la raccolta contenuto nel server del sito.  

-   **Aggiornare il contenuto**: quando si avvia l'azione di aggiornamento del contenuto per un tipo di distribuzione dell'applicazione o del pacchetto, il contenuto viene copiato dall'origine del pacchetto alla raccolta contenuto. Per completare correttamente questa azione, è necessario che i file di origine del pacchetto siano disponibili nel percorso originale. È necessario eseguire questa azione in ogni pacchetto e applicazione.  

#### <a name="recover-custom-software-updates-on-the-computer-running-updates-publisher"></a>Recuperare gli aggiornamenti software personalizzati nel computer che esegue Updates Publisher  
 Quando sono stati inclusi i file di database di Updates Publisher nel piano di backup, è possibile ripristinare i database in caso di errore nel computer in cui viene eseguito Updates Publisher. Per altre informazioni su Updates Publisher, vedere [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=228726) nella Libreria TechCenter di System Center.  

 Usare la procedura seguente per ripristinare il backup del database Updates Publisher.  

###### <a name="to-restore-the-updates-publisher-2011-database"></a>Per ripristinare il database Updates Publisher 2011  

1.  Reinstallare Updates Publisher nel computer ripristinato.  

2.  Copiare il file di database (Scupdb.sdf) dalla destinazione di backup in %*PROFILOUTENTE*%\AppData\Local\Microsoft\System Center Updates Publisher 2011\5.00.1727.0000\ nel computer che esegue Updates Publisher.  

3.  Quando più utenti eseguono Updates Publisher nel computer, è necessario copiare ogni file di database nel percorso del profilo utente appropriato.  

#### <a name="user-state-migration-data"></a>Dati di migrazione sullo stato utente  
 Come parte delle proprietà del sistema del sito del punto di migrazione, è possibile specificare le cartelle in cui vengono archiviati i dati di migrazione stato utente. Dopo aver ripristinato un server con una cartella che archivia dati di migrazione stato utente, è necessario ripristinare manualmente i dati di migrazione stato utente nel server nelle stesse cartelle in cui sono stati archiviati i dati prima dell'errore.  

#### <a name="regenerate-the-certificates-for-distribution-points"></a>Rigenerare i certificati per i punti di distribuzione  
 Dopo aver ripristinato un sito, il file distmgr.log potrebbe contenere una voce per uno o più punti di distribuzione, che indica che non è stato possibile decrittografare i dati PFX ****del certificato. Questa voce indica che i dati del certificato del punto di distribuzione non possono essere decrittografati dal sito. Per risolvere questo problema, è necessario rigenerare o reimportare il certificato per i punti di distribuzione interessati. A questo scopo, è possibile usare il cmdlet[Set-CMDistributionPoint](https://technet.microsoft.com/library/jj821872\(v=sc.20\).aspx) di PowerShell.  

#### <a name="update-certificates-used-for-cloud-based-distribution-points"></a>Aggiornare i certificati usati per i punti di distribuzione basati su cloud  
 Configuration Manager richiede un certificato di gestione che utilizza per la comunicazione dal server del sito al punto di distribuzione basato su cloud. Dopo un ripristino del sito è necessario aggiornare i certificati per i punti di distribuzione basati su cloud.  

####  <a name="BKMK_RecoverSecondarySite"></a> Ripristinare un sito secondario  
 Configuration Manager non supporta il backup del database in un sito secondario, ma supporta il ripristino mediante reinstallazione del sito secondario. Il ripristino del sito secondario è necessario quando si verifica un errore del sito secondario di Configuration Manager. È possibile ripristinare un sito secondario mediante l'azione **Ripristina sito secondario** dal nodo **Siti** nella console di Configuration Manager. Diversamente dal ripristino di un sito di amministrazione centrale o un sito primario, il ripristino di un sito secondario non usa un file di backup, ma reinstalla i file del sito secondario in cui si è verificato l'errore. I dati del sito secondario vengono quindi reinizializzati con i dati del sito primario padre. Durante il processo di ripristino Configuration Manager verifica se la raccolta contenuto esiste nel computer del sito secondario e che il contenuto appropriato sia disponibile. Il sito secondario userà la raccolta contenuto esistente, se questa include il contenuto appropriato. In caso contrario, per ripristinare la raccolta contenuto di un sito secondario ripristinato, è necessario ridistribuire o pre-installare il contenuto in tale sito ripristinato. Quando si dispone di un punto di distribuzione che non si trova nel sito secondario, non è necessario reinstallare il punto di distribuzione durante un ripristino del sito secondario. Dopo il ripristino del sito secondario il sito si sincronizza automaticamente con il punto di distribuzione.  

 È possibile verificare lo stato del sito secondario mediante l'azione **Mostra stato installazione** dal nodo **Siti** nella console di Configuration Manager.  

> [!IMPORTANT]  
>  È necessario usare un computer con la stessa configurazione del computer in cui si è verificato l'errore, ad esempio con il FQDN, per ripristinare correttamente il sito secondario. Il computer deve inoltre soddisfare tutti i prerequisiti del sito secondario e deve disporre dei privilegi di protezione appropriati configurati. Inoltre, usare lo stesso percorso di installazione usato per il sito per cui si è verificato un errore.  

> [!IMPORTANT]  
>  Durante il ripristino di un sito secondario Configuration Manager non installa SQL Server Express se questo non è installato nel computer. Pertanto, prima di ripristinare un sito secondario è necessario installare manualmente SQL Server Express o SQL Server. È necessario usare la stessa versione di SQL Server e la stessa istanza di SQL Server usate per il database del sito secondario prima dell'errore.  

##  <a name="BKMK_SMSWriterService"></a> Servizio SMS Writer  
 SMS Writer è un servizio che interagisce con Servizio Copia Shadow del volume (VSS) durante il processo di backup. Per la corretta esecuzione del backup del sito di Configuration Manager è necessario che SMS Writer sia in esecuzione.  

### <a name="purpose"></a>Scopo  
 SMS Writer esegue la registrazione al servizio VSS e associa le interfacce e gli eventi. Quando VSS trasmette gli eventi o invia determinate notifiche a SMS Writer, questo risponde alla notifica ed esegue l'azione appropriata. SMS Writer legge il file di controllo del backup (smsbkup.ctl), disponibile in &lt;*Percorso installazione ConfigMgr*>\inboxes\smsbkup.box, e determina i file e i dati di cui eseguire il backup. SMS Writer crea i metadati, composti da vari componenti, in base a tali informazioni e a dati specifici provenienti dalla chiave e dalle sottochiavi di registro SMS. Quando richiesto invia i metadati a VSS. VSS invia quindi i metadati all'applicazione richiedente: Gestione backup di Configuration Manager. Gestione backup seleziona i dati di cui eseguire il backup e li invia a SMS Writer tramite VSS. SMS Writer esegue i passaggi appropriati per la preparazione del backup. Quando VSS è pronto per lo snapshot, invia un evento. A quel punto SMS Writer interrompe tutti i servizi di Configuration Manager e garantisce che le attività di Configuration Manager vengano bloccate durante la creazione dello snapshot. In seguito al completamento dello snapshot, SMS Writer riavvia i servizi e le attività.  

 Il servizio SMS Writer viene installato automaticamente. Deve essere eseguito quando l'applicazione VSS richiede un backup o un ripristino.  

### <a name="writer-id"></a>ID writer  
 L'ID writer per SMS Writer è: 03ba67dd-dc6d-4729-a038-251f7018463b.  

### <a name="permissions"></a>Autorizzazioni  
 Il servizio SMS Writer deve essere eseguito all'interno dell'account di sistema locale.  

### <a name="volume-shadow-copy-service"></a>Servizio Copia Shadow del volume  
 VSS è un set di API COM che consente di implementare un framework per l'esecuzione dei backup del volume durante la scrittura delle applicazioni di un sistema nei volumi. VSS offre un'interfaccia coerente che consente il coordinamento tra le applicazioni utente per l'aggiornamento dei dati sul disco (il servizio SMS Writer) e quelle che eseguono il backup delle applicazioni (il servizio Gestione backup). Per altre informazioni su VSS, vedere l'argomento [Volume Shadow Copy Service (Servizio Copia Shadow del volume)](http://go.microsoft.com/fwlink/p/?LinkId=241968) in TechCenter di Windows Server.  


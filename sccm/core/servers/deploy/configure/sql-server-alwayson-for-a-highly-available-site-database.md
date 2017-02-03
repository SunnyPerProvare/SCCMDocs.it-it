---
title: SQL Server AlwaysOn | Microsoft Docs
ms.custom: na
ms.date: 1/4/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 58d52fdc-bd18-494d-9f3b-ccfc13ea3d35
caps.latest.revision: 16
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 4d34a272a93100426cccd2308c5b3b0b0ae94a60
ms.openlocfilehash: 5fb6bc0bca5ee590000fd30bd46c765871cf5220


---
# <a name="sql-server-alwayson-for-a-highly-available-site-database-for-system-center-configuration-manager"></a>SQL Server AlwaysOn per database del sito a disponibilità elevata per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*



 A partire dalla versione 1602 di System Center Configuration Manager, è possibile usare [Gruppi di disponibilità AlwaysOn](https://msdn.microsoft.com/library/hh510230\(v=sql.120\).aspx) di SQL Server per ospitare il database del sito nei siti primari e nel sito di amministrazione centrale come soluzione a disponibilità elevata e di ripristino di emergenza. Il gruppo di disponibilità può essere ospitato localmente o in Microsoft Azure.  

 Quando si usa Microsoft Azure per ospitare il gruppo di disponibilità, è possibile aumentare ulteriormente la disponibilità del database del sito usando i gruppi di disponibilità SQL Server AlwaysOn con i set di disponibilità di Azure. Per altre informazioni sui set di disponibilità di Azure, vedere [Gestione della disponibilità delle macchine virtuali](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-manage-availability/).  

 Di seguito sono riportati gli scenari supportati con gruppi di disponibilità:  

-   È possibile spostare il database del sito nell'istanza predefinita di un gruppo di disponibilità  

-   È possibile aggiungere o rimuovere membri di replica da un gruppo di disponibilità che ospita un database del sito  

-   È possibile spostare il database del sito da un gruppo di disponibilità a un'istanza predefinita o denominata di SQL Server autonomo  


> [!NOTE]  
>  Per la configurazione e l'uso corretti dei gruppi di disponibilità, è necessario che l'utente abbia una certa familiarità con la configurazione di SQL Server e dei gruppi di disponibilità di SQL Server. Le procedure per System Center Configuration Manager in questo argomento si basano su documentazione aggiuntiva e sulle procedure presenti nella libreria della documentazione di SQL Server.  

 **Problemi noti durante l'utilizzo di gruppi di disponibilità AlwaysOn con Configuration Manager:**  

-   **Tutti i server di replica richiedono un identico percorso di file al momento dell'impostazione di Configuration Manager per l'uso dei gruppi di disponibilità:**  

    -   Quando si esegue il programma di installazione di Configuration Manager per reindirizzare il sito per l'uso del database in un gruppo di disponibilità, ogni server di replica secondaria del gruppo deve avere un percorso di file identico a quello usato per ospitare i file di database del sito nella replica primaria corrente. Se non esiste un percorso identico nelle repliche secondarie, il programma di installazione non sarà in grado di aggiungere l'istanza dei gruppi di disponibilità come nuovo percorso del database del sito.  

         In ogni server di replica secondaria, l'account del servizio SQL Server locale deve avere l'autorizzazione **Controllo completo** per questa cartella.  

         I server di replica secondaria richiedono questo percorso file solo durante l'installazione per specificare l'istanza di database nel gruppo di disponibilità.  Dopo aver completato la modifica per usare il database del sito nel gruppo di disponibilità, è possibile eliminare il percorso non usato dai server di replica secondari.  

         Prendere ad esempio in considerazione i seguenti scenari:  

        -   Si crea un gruppo di disponibilità che usa tre server SQL  

        -   Il server di replica primaria è una nuova installazione di SQL Server 2014.  Per impostazione predefinita, i file MDF e LDF del database vengono archiviati in C:\Programmi\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\DATA  

        -   Entrambi i server di replica secondaria sono stati aggiornati a SQL Server 2014 da versioni precedenti e continuano a usare il percorso di file originale per archiviare i file di database: C:\Programmi\Microsoft SQL Server\MSSQL10. MSSQLSERVER\MSSQL\DATA  

        -   Prima di tentare di spostare il database del sito in questo gruppo di disponibilità, in ogni server di replica secondaria è necessario creare il seguente percorso di file anche se le repliche secondarie non useranno questo percorso: C:\Programmi\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\DATA (questo è un duplicato del percorso usato nella replica primaria)  

        -   È quindi possibile concedere all'account del servizio SQL Server in ogni replica secondaria l'accesso con controllo completo al percorso di file appena creato nel server  

        -   È ora possibile eseguire correttamente l'installazione di Configuration Manager per indirizzare il sito in modo che usi il database del sito nel gruppo di disponibilità  

-   **Quando si esegue il programma di installazione per indirizzare il database del sito in modo che usi il gruppo di disponibilità, nel file ConfigMgrSetup.log possono essere registrati errori simili ai seguenti:**  

    -   ERRORE: Errore SQL Server: [25000][3906][Microsoft][SQL Server Native Client 11.0][SQL Server]Impossibile aggiornare il database "CM_AAA" perché è di sola lettura.   Installazione di Configuration Manager 1/21/2016 4:54:59 PM  7344 (0x1CB0)  

     Questi errori vengono registrati quando il programma di installazione prova a elaborare i ruoli del database nelle repliche secondarie del gruppo di disponibilità. È possibile ignorare questi errori.
- **SQL Server che ospitano i gruppi di disponibilità aggiuntivi:**

  Prima di installare la versione 1610, quando si usa un gruppo di disponibilità e quindi si esegue l'installazione di Configuration Manager o di un suo aggiornamento, ogni replica in ogni gruppo di disponibilità aggiuntivo negli SQL Server che ospitano il gruppo di disponibilità di Configuration Manager deve avere le configurazioni seguenti:
    - **failover manuale**
    - **consentire le connessioni di sola lettura**


##  <a name="a-namebkmkbnra-changes-for-backup-and-recovery-when-you-use-a-sql-server-alwayson-availability-group"></a><a name="bkmk_BnR"></a> Modifiche a Backup e ripristino quando si usa un gruppo di disponibilità SQL Server AlwaysOn  
 **Backup:**  

 Quando un database del sito viene eseguito in un gruppo di disponibilità, è necessario continuare a eseguire l'attività di manutenzione predefinita **Backup server sito** per eseguire il backup di impostazioni e file comuni di Configuration Manager, senza usare però i file MDF o LDF creati da tale backup. Pianificare invece backup diretti del database del sito usando SQL Server.  

 È anche necessario pianificare il monitoraggio e la gestione delle dimensioni del log delle transazioni del database del sito perché il modello di recupero del database è impostato su Completo.  Nel modello di recupero Completo le transazioni non vengono finalizzate fino a quando non viene eseguito un backup completo del database o del log delle transazioni. Un modello di recupero con registrazione completa è un requisito per poter usare il database del sito in un gruppo di disponibilità e deve essere impostato quando si configura il gruppo per l'uso con Configuration Manager. Per altre informazioni sul backup e il ripristino di SQL Server, vedere [Backup e ripristino di database SQL Server](https://msdn.microsoft.com/library/ms187048\(v=sql.120\).aspx) nella documentazione di SQL Server.  

 **Recupero:**  

 Durante un ripristino del sito, è possibile usare l'opzione di ripristino del sito **Ignora ripristino database (utilizzare questa opzione se non si sono verificati errori nel database del sito)**a condizione che uno dei nodi del gruppo di disponibilità continui a funzionare.  

 Se invece tutti i nodi di un gruppo di disponibilità sono andati perduti, prima di poter ripristinare il sito è necessario ricreare il gruppo di disponibilità poiché System Center Configuration Manager non può ricompilare o ripristinare il nodo di disponibilità.  Dopo aver ricreato il gruppo con un backup ripristinato e riconfigurato, è possibile usare l'opzione di ripristino del sito **Ignora ripristino database (utilizzare questa opzione se non si sono verificati errori nel database del sito)**.  

 Per altre informazioni sulle attività di backup e ripristino, vedere [Backup e ripristino per System Center Configuration Manager](../../../../protect/understand/backup-and-recovery.md).  

##  <a name="a-namebkmkcreatea-configure-an-availability-group-for-use-with-configuration-manager"></a><a name="bkmk_create"></a> Configurare un gruppo di disponibilità da usare con Configuration Manager  
 Prima di iniziare la procedura seguente, acquisire familiarità con le procedure di SQL Server necessarie per completare la configurazione e con le informazioni seguenti che si applicano ai gruppi di disponibilità configurati per l'uso con Configuration Manager.  

 **Requisiti per i gruppi di disponibilità AlwaysOn usati con System Center Configuration Manager:**  

-  *Versione*: ogni nodo, o replica, nel gruppo di disponibilità deve eseguire una versione di SQL Server supportata da System Center Configuration Manager. Se supportati da SQL Server, diversi nodi del gruppo di disponibilità possono eseguire diverse versioni di SQL Server.   

- *Edizione*: è necessario usare un'edizione Enterprise di SQL Server.  In SQL Server 2016 Standard Edition sono stati introdotti i gruppi di disponibilità di base, non supportati da Configuration Manager.


-   I gruppi di disponibilità devono disporre di una replica primaria e possono avere fino a due repliche secondarie sincrone.  

-  Dopo aver aggiunto un database a un gruppo di disponibilità, eseguire il failover della replica primaria a una replica secondaria (trasformandola nella nuova replica primaria) e quindi configurare il database come segue:
    - Enable Trustworthy: equal to True
    - Enable the Service Broker: equal to True
    - Set the dbowner: equal to SA

    È possibile eseguire lo script seguente per configurare queste impostazioni, dove cm_ABC è il nome del database del sito:  

    >     USE master  
    >     ALTER DATABASE cm_ABC SET NEW_BROKER   
    >     ALTER DATABASE cm_ABC SET ENABLE_BROKER  
    >     ALTER DATABASE cm_ABC SET TRUSTWORTHY ON;  
    >     USE cm_ABC  
    >     EXEC sp_changedbowner 'sa'  
    >     Exec sp_configure 'max text repl size (B)', 2147483647
    >     reconfigure



-   Il gruppo di disponibilità deve avere almeno un **listener del gruppo di disponibilità**.  Il nome virtuale di questo listener viene usato quando si configura Configuration Manager per usare il database del sito nel gruppo di disponibilità. Anche se un gruppo di disponibilità può contenere più listener, Configuration Manager può usarne solo uno  

-   Tutte le repliche primarie e secondarie devono:  
    - Essere impostate per **consentire le connessioni di sola lettura**
    - Usare l' **istanza predefinita**
    - Essere impostate per il **failover manuale**  

        > [!TIP]  
        >  System Center Configuration Manager supporta l'uso di repliche del gruppo di disponibilità quando sono impostate su Failover automatico. Tuttavia, è necessario impostare Failover manuale quando si esegue l'installazione per specificare l'uso del database del sito nel gruppo di disponibilità e quando si installano gli aggiornamenti in Configuration Manager, inclusi quelli che non si applicano al database del sito.  

  **Limitazioni per i gruppi di disponibilità**
   - Non sono supportati i gruppi di disponibilità di base (introdotti con SQL Server 2016 Standard Edition). Questi gruppi, infatti, non supportano l'accesso in lettura alle repliche secondarie, requisito essenziale per l'uso con Configuration Manager. Per altre informazioni, vedere [Gruppi di disponibilità di base (gruppi di disponibilità AlwaysOn)](https://msdn.microsoft.com/en-us/library/mt614935.aspx).

   - I gruppi di disponibilità sono supportati solo per il database del sito e non per il database di aggiornamento software o il database di report.   
   - Quando si usa un gruppo di disponibilità è necessario configurare manualmente il punto di reporting per usare la replica primaria corrente e non il listener del gruppo di disponibilità. Se la replica primaria esegue il failover a un'altra replica, è necessario riconfigurare il punto di reporting per usare la nuova replica primaria.  
   - Prima di installare gli aggiornamenti, ad esempio la versione 1606, verificare che il gruppo di disponibilità sia impostato sul failover manuale. Dopo l'aggiornamento del sito, è possibile ripristinare la modalità di failover automatico.



 **Autorizzazioni necessarie per configurare e usare i gruppi di disponibilità:**  

-   L'account computer del server del sito deve essere un membro del gruppo **Administrators locale** in tutti i computer membri del gruppo di disponibilità.  

#### <a name="to-configure-an-availability-group-to-host-a-site-database"></a>Per configurare un gruppo di disponibilità per ospitare un database del sito  

1.  Usare il comando seguente per arrestare il sito di Configuration Manager:  
     **Preinst.exe /stopsite**  

     Per altre informazioni sull'uso di preinst.exe, vedere [Strumento di manutenzione gerarchia (Preinst.exe) per System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

2.  Modificare il modello di backup per il database del sito da **SIMPLE** a **FULL**.  

     Vedere [Visualizzazione o modifica del modello di recupero di un database](https://msdn.microsoft.com/library/ms189272\(v=sql.120\).aspx) nella documentazione di SQL Server. I gruppi di disponibilità supportano solo FULL.  

3.  Nel server che ospiterà la replica primaria del gruppo usare la **Creazione guidata Gruppo di disponibilità** per creare il gruppo di disponibilità. Nella procedura guidata:  

    -   Nella pagina **Seleziona database** selezionare il database per il sito di Configuration Manager  

    -   Nella pagina **Specifica repliche** configurare:  

        -   **Repliche**: specificare i server che ospiteranno le repliche secondarie  

        -   **Listener**: specificare il **Nome DNS del listener** come un nome DNS completo, ad esempio **&lt;Listener_Server> fabrikam.com**. Il nome viene usato quando si configura Configuration Manager per usare il database nel gruppo di disponibilità.

    -   Nella pagina **Seleziona sincronizzazione dati iniziale** selezionare **Completa**. Dopo aver creato il gruppo di disponibilità, la procedura guidata esegue il backup del database primario e del log delle transazioni e li ripristina in ogni server che ospita una replica secondaria. Se non si esegue questo passaggio, è necessario ripristinare una copia del database del sito in ogni server che ospita una replica secondaria e aggiungere manualmente il database al gruppo.  

    Per altre informazioni, vedere [Usare la Creazione guidata Gruppo di disponibilità](https://msdn.microsoft.com/library/hh403415\(v=sql.120\).aspx) nella documentazione di SQL Server.  

4.  Dopo aver configurato il gruppo di disponibilità, configurare il database del sito nella replica primaria con la proprietà **TRUSTWORTHY** , quindi **abilitare l'integrazione CLR**. Per informazioni sulla configurazione, vedere [Proprietà di database TRUSTWORTHY](https://msdn.microsoft.com/library/ms187861\(v=sql.120\).aspx) e  [Abilitazione dell'integrazione con CLR](https://msdn.microsoft.com/library/ms131048\(v=sql.120\).aspx) nella documentazione di SQL Server.  

5.  Completare le azioni seguenti per configurare ogni replica secondaria nel gruppo di disponibilità:  

    1.  Eseguire il failover manuale della replica primaria corrente in una replica secondaria. Vedere [Eseguire un failover manuale pianificato di un gruppo di disponibilità](https://msdn.microsoft.com/library/hh231018\(v=sql.120\).aspx) nella documentazione di SQL Server.  

    2.  Configurare il database nella nuova replica primaria con la proprietà **TRUSTWORTHY** , quindi **abilitare l'integrazione CLR**.  

6.  Dopo che tutte le repliche sono state alzate di livello fino a diventare repliche primarie e dopo aver configurato i database, il gruppo di disponibilità può essere usato con Configuration Manager.  





##  <a name="a-namebkmkdirecta-move-a-site-database-to-an-availability-group"></a><a name="bkmk_direct"></a> Spostare un database del sito in un gruppo di disponibilità  
 È possibile spostare un database di un sito installato in precedenza in un gruppo di disponibilità. Per prima cosa è necessario creare il gruppo di disponibilità e quindi configurare il database per l'operazione nel gruppo di disponibilità.  

 Per completare questa procedura, l'account utente che esegue l'installazione di Configuration Manager deve essere un membro del gruppo **Administrators locale** in tutti i computer membri del gruppo di disponibilità.  

#### <a name="to-move-a-site-database-to-an-availability-group"></a>Per spostare un database del sito in un gruppo di disponibilità  

1.  Eseguire l'**installazione di Configuration Manager** da **&lt;cartella di installazione del sito di Configuration Manager\>\BIN\X64\setup.exe**.  

2.  Nella pagina **Riquadro attività iniziale** selezionare **Esegui una manutenzione del sito o reimposta il sito**, quindi fare clic su **Avanti**.  

3.  Selezionare l'opzione **Modifica la configurazione di SQL Server** , quindi fare clic su **Avanti**.  

4.  Riconfigurare quanto segue per il database del sito:  

    -   **Nome server SQL** : immettere il nome virtuale per il listener del gruppo di disponibilità configurato al momento della creazione del gruppo di disponibilità. Il nome virtuale deve essere un nome DNS completo, ad esempio **&lt;endpointServer\>.fabrikam.com**  

    -   **Istanza** : questo valore deve essere vuoto per specificare l'istanza predefinita per il listener del gruppo di disponibilità.  Se è installato il database del sito corrente in un'istanza denominata, questa istanza viene elencata e deve essere cancellata  

    -   **Database** : non modificare il nome visualizzato. È il nome del database del sito corrente.  

5.  Dopo aver specificato le informazioni per il nuovo percorso del database, completare l'installazione con il processo e le configurazioni normali.  

##  <a name="a-namebkmkchangea-add-or-remove-members-of-an-active-availability-group"></a><a name="bkmk_change"></a> Aggiungere o rimuovere membri di un gruppo di disponibilità attivo  
 Quando Configuration Manager usa un database del sito ospitato in un gruppo di disponibilità, è possibile rimuovere un membro di replica o aggiungerne un altro, senza superare un nodo primario e due secondari.  

#### <a name="to-add-a-new-replica-member"></a>Per aggiungere un nuovo membro di replica  

1.  Aggiungere il nuovo server come replica secondaria al gruppo di disponibilità. Vedere  [Aggiungere una replica secondaria a un gruppo di disponibilità (SQL Server)](https://msdn.microsoft.com/library/hh213247\(v=sql.120\).aspx)nella libreria della documentazione di SQL Server.  

2.  Arrestare il sito di Configuration Manager eseguendo **Preinst.exe /stopsite** Vedere [Hierarchy Maintenance Tool (Preinst.exe) for System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md) (Strumento di manutenzione gerarchia (Preinst.exe) per System Center Configuration Manager).  

3.  Configurare tutte le repliche secondarie. Completare le azioni seguenti per ogni replica secondaria nel gruppo di disponibilità:  

    1.  Eseguire il failover manuale della replica primaria nella nuova replica secondaria. Vedere [Eseguire un failover manuale pianificato di un gruppo di disponibilità](https://msdn.microsoft.com/library/hh231018\(v=sql.120\).aspx) nella documentazione di SQL Server.  

    2.  Configurare il database nel nuovo server con la proprietà Trustworthy e abilitare l'integrazione CLR. Vedere [Proprietà di database TRUSTWORTHY](https://msdn.microsoft.com/library/ms187861\(v=sql.120\).aspx) e  [Abilitazione dell'integrazione con CLR](https://msdn.microsoft.com/library/ms131048\(v=sql.120\).aspx)nella documentazione di SQL Server.  

4.  Riavviare il sito avviando i servizi di Gestione componenti del sito (**sitecomp**) e **SMS_Executive** .  

#### <a name="to-remove-a-replica-member-from-the-availability-group"></a>Per rimuovere un membro di replica dal gruppo di disponibilità  

-   Usare le informazioni contenute in [Rimuovere una replica secondaria da un gruppo di disponibilità](https://msdn.microsoft.com/library/hh213149\(v=sql.120\).aspx) nella documentazione di SQL Server.  

##  <a name="a-namebkmkremovea-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a><a name="bkmk_remove"></a> Spostare il database del sito da un gruppo di disponibilità a un'istanza singola di SQL Server  
 Usare la procedura seguente se non si vuole più ospitare il database del sito in un gruppo di disponibilità.  

#### <a name="to-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a>Per spostare il database del sito da un gruppo di disponibilità a un'istanza singola di SQL Server  

1.  Usare il comando seguente per arrestare il sito di Configuration Manager:  
     **Preinst.exe /stopsite**.  Per altre informazioni, vedere [Strumento di manutenzione gerarchia (Preinst.exe) per System Center Configuration Manager](../../../../core/servers/manage/hierarchy-maintenance-tool-preinst.exe.md).  

2.  Usare SQL Server per creare un backup completo del database del sito dalla replica primaria. Per informazioni su come completare questo passaggio, vedere [Creare un backup completo del database (SQL Server)](https://msdn.microsoft.com/library/ms187510\(v=sql.120\).aspx) nella documentazione di SQL Server.  

3.  Se il server che ospita la replica primaria del gruppo di disponibilità ora ospita l'istanza singola del database del sito, è possibile ignorare questo passaggio:  

    -   Usare SQL Server per ripristinare il backup del database del sito nel server che ospiterà il database del sito.  Vedere [Ripristinare un backup del database (SQL Server Management Studio)](https://msdn.microsoft.com/library/ms177429\(v=sql.120\).aspx) nella libreria della documentazione di SQL Server.  

4.  Nel database del sito ripristinato modificare il modello di backup per il database del sito da **FULL** a **SIMPLE**.  Vedere [Visualizzazione o modifica del modello di recupero di un database](https://msdn.microsoft.com/library/ms189272\(v=sql.120\).aspx) nella documentazione di SQL Server.  

5.  Eseguire l'**installazione di Configuration Manager** da **&lt;cartella di installazione del sito di Configuration Manager\>\BIN\X64\setup.exe**.  

6.  Nella pagina **Riquadro attività iniziale** selezionare **Esegui una manutenzione del sito o reimposta il sito**, quindi fare clic su **Avanti**.  

7.  Selezionare l'opzione **Modifica la configurazione di SQL Server** , quindi fare clic su **Avanti**.  

8.  Riconfigurare quanto segue per il database del sito:  

    -   **Nome server SQL** : immettere il nome del server che ora ospita il database del sito.  

    -   **Istanza** : specificare l'istanza denominata che ospita il database del sito o lasciare vuoto il campo se il database si trova nell'istanza predefinita.  

    -   **Database** : non modificare il nome visualizzato. È il nome del database del sito corrente.  

9. Dopo aver specificato le informazioni per il nuovo percorso del database, completare l'installazione con il processo e le configurazioni normali. Al termine dell'installazione, il sito viene riavviato e inizia a usare il nuovo percorso del database.  

10. Per pulire i server che erano membri del gruppo di disponibilità, seguire le indicazioni riportate in [Rimuovere un gruppo di disponibilità](https://msdn.microsoft.com/library/ff878113\(v=sql.120\).aspx) nella documentazione di SQL Server.



<!--HONumber=Jan17_HO1-->



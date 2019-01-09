---
title: Configurare gruppi di disponibilità
titleSuffix: Configuration Manager
description: Configurare e gestire gruppi di disponibilità Always On di SQL Server con SCCM.
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7e4ec207-bb49-401f-af1b-dd705ecb465d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 10b15f8463bb54df859f09379f41a809a45fc5b9
ms.sourcegitcommit: 81e3666c41eb976cc7651854042dafe219e2e467
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2018
ms.locfileid: "53747127"
---
# <a name="configure-sql-server-always-on-availability-groups-for-configuration-manager"></a>Configurare gruppi di disponibilità Always On di SQL Server con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le informazioni contenute in questo argomento consentono di configurare e gestire i gruppi di disponibilità usati con Configuration Manager.

Prima di iniziare:  
-   Acquisire familiarità con le informazioni contenute in [Prepararsi a usare i gruppi di disponibilità Always On di SQL Server con Configuration Manager](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).
-   Acquisire familiarità con la documentazione di SQL Server relativa all'uso dei gruppi di disponibilità e alle procedure correlate. Tali informazioni sono necessarie per completare gli scenari seguenti.

> [!TIP]  
>  I collegamenti in questo argomento relativi a SQL Server rimandano al contenuto relativo a SQL Server 2016. Se non si usa questa versione di SQL Server, consultare la documentazione relativa alla versione in uso.

## <a name="create-and-configure-an-availability-group"></a>Creare e configurare un gruppo di disponibilità
Adottare la procedura seguente per creare un gruppo di disponibilità e quindi spostare una copia del database del sito nel gruppo di disponibilità creato.

Per completare la procedura, l'account usato deve:
-   Essere membro del gruppo **Administrators locale** su ogni computer incluso nel gruppo di disponibilità.
-   Essere **amministratore di sistema** in ogni istanza di SQL Server che ospita il database del sito.

### <a name="to-create-and-configure-an-availability-group-for-configuration-manager"></a>Per creare e configurare un gruppo di disponibilità per Configuration Manager  
1. Usare il comando seguente per arrestare il sito di Configuration Manager: **Preinst.exe /stopsite**. Per altre informazioni sull'uso di Preinst.exe, vedere [Strumento di manutenzione gerarchia](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe).

2. Modificare il modello di backup per il database del sito da **SIMPLE** a **FULL**.
   Vedere [Visualizzazione o modifica del modello di recupero di un database](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server) nella documentazione di SQL Server. I gruppi di disponibilità supportano solo FULL.

3. Usare SQL Server per creare un backup completo del database del sito. Eseguire quindi una delle operazioni seguenti, a seconda del fatto che il server che ospita il database del sito sarà o meno un membro di replica del nuovo gruppo di disponibilità:
   - **Sarà membro del gruppo di disponibilità:**  
     Se si usa questo server come membro di replica primaria iniziale del gruppo di disponibilità, non è necessario ripristinare una copia del database del sito su questo o su un altro server nel gruppo. Il database risulterà già incluso nella replica primaria e SQL Server eseguirà la replica del database nelle repliche secondarie in un passaggio successivo.  

     -    **Non sarà membro del gruppo di disponibilità:**   
     Ripristinare una copia del database del sito nel server che ospiterà la replica primaria del gruppo.

   Per informazioni su come completare questo passaggio, vedere [Creazione di un backup completo del database (SQL Server)](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) e [Ripristinare un backup del database tramite SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms) nella documentazione di SQL Server.

4. Nel server che ospiterà la replica primaria iniziale del gruppo usare la [Creazione guidata Gruppo di disponibilità](/sql/database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio) per creare il gruppo di disponibilità. Nella procedura guidata:
   - Nella pagina **Seleziona database** selezionare il database per il sito di Configuration Manager.  

   - Nella pagina **Specifica repliche** configurare:
     -    **Repliche**: specificare i server che ospiteranno le repliche secondarie.

     -    **Listener**: specificare il **Nome DNS del listener** come un nome DNS completo, ad esempio **&lt;Listener_Server> fabrikam.com**. Il nome viene usato quando si configura Configuration Manager per usare il database nel gruppo di disponibilità.

   - Nella pagina **Seleziona sincronizzazione dati iniziale** selezionare **Completa**. Dopo avere creato il gruppo di disponibilità, la procedura guidata esegue il backup del database primario e del log delle transazioni, quindi li ripristina in ogni server che ospita una replica secondaria. Se non si esegue questo passaggio, è necessario ripristinare una copia del database del sito in ogni server che ospita una replica secondaria e aggiungere manualmente il database al gruppo.   

5. Controllare la configurazione in ogni replica:   
   1.    Verificare che l'account computer del server del sito sia un membro del gruppo **Administrators locale** in tutti i computer membri del gruppo di disponibilità.  

   2.  Eseguire lo [script di verifica](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites) dai prerequisiti per verificare che il database del sito in ogni replica sia configurato correttamente.

   3.    Prima di impostare le configurazioni nelle repliche secondarie, è necessario eseguire il failover manuale della replica primaria nella replica secondaria. È possibile configurare solo il database di una replica primaria. Per altre informazioni, vedere [Eseguire un failover manuale pianificato di un gruppo di disponibilità](/sql/database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server) nella documentazione di SQL Server.

6. Quando tutte le repliche soddisfano i requisiti, il gruppo di disponibilità è pronto per essere usato con Configuration Manager.

## <a name="configure-a-site-to-use-the-database-in-the-availability-group"></a>Configurare un sito per usare il database nel gruppo di disponibilità
Dopo aver [creato e configurato il gruppo di disponibilità](#create-and-configure-an-availability-group), usare la funzione di manutenzione del sito di Configuration Manager per configurare il sito affinché usi il database ospitato dal gruppo di disponibilità.

Non è supportata l'installazione di un nuovo sito con il proprio database in un gruppo di disponibilità. Se, ad esempio, si usa la versione di base 1702, è necessario installare il sito usando una singola istanza di SQL Server. Dopo aver completato l'installazione, è possibile spostare il database del sito nel gruppo di disponibilità.

Per completare la procedura, l'account usato per eseguire il programma di installazione di Configuration Manager deve:
-   Essere membro del gruppo **Administrators locale** su ogni computer membro del gruppo di disponibilità.
-   Essere **amministratore di sistema** in ogni istanza di SQL Server che ospita il database del sito.

> [!IMPORTANT]
> Quando si usa Microsoft Intune con Configuration Manager in una configurazione ibrida, lo spostamento del database del sito da o verso un gruppo di disponibilità attiva la risincronizzazione dei dati con il cloud. Non è possibile evitare questa risincronizzazione.

### <a name="to-configure-a-site-to-use-the-availability-group"></a>Per configurare un sito per usare un gruppo di disponibilità
1.  Eseguire **Installazione di Configuration Manager** da **&lt;*cartella di installazione del sito di Configuration Manager*>\BIN\X64\setup.exe**.

2.  Nella pagina **Riquadro attività iniziale** selezionare **Esegui una manutenzione del sito o reimposta il sito**, quindi fare clic su **Avanti**.

3.  Selezionare l'opzione **Modifica la configurazione di SQL Server** , quindi fare clic su **Avanti**.

4.  Riconfigurare quanto segue per il database del sito:
    -   **Nome server SQL:** immettere il nome virtuale del **listener** del gruppo di disponibilità configurato al momento della creazione del gruppo di disponibilità. Il nome virtuale deve essere un nome DNS completo, ad esempio ***&lt;Serverendpoint*>.fabrikam.com**.  

    -   **Istanza**: questo valore deve essere vuoto per specificare l'istanza predefinita per il *listener* del gruppo di disponibilità. Se il database del sito corrente viene eseguito in un'istanza denominata, questa istanza viene elencata e deve essere cancellata.

    -   **Database**: non modificare il nome visualizzato. È il nome del database del sito corrente.

5.  Dopo aver specificato le informazioni per il nuovo percorso del database, completare l'installazione con il processo e le configurazioni normali.



## <a name="add-or-remove-synchronous-replica-members"></a>Aggiungere o rimuovere membri di replica sincrona  
Se il database del sito è ospitato in un gruppo di disponibilità, usare le procedure seguenti per aggiungere o rimuovere membri di replica sincrona. Per informazioni sul tipo e sul numero di repliche supportate, vedere **Configurazioni dei gruppi di disponibilità** nella sezione [Prerequisiti](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database#prerequisites) dell'argomento Preparare l'uso di gruppi di disponibilità.

Per completare le procedure seguenti, l'account usato deve:
-   Essere membro del gruppo **Administrators locale** su ogni computer membro del gruppo di disponibilità.
-   Essere **amministratore di sistema** in ogni istanza di SQL Server che ospita o ospiterà il database del sito.


### <a name="to-add-a-new-synchronous-replica-member"></a>Per aggiungere un nuovo membro di replica sincrona  
Il processo per aggiungere una replica secondaria a un gruppo di disponibilità usato con Configuration Manager può risultare complesso, dinamico e richiedere passaggi e procedure che variano in base ai singoli ambienti. Sono previsti alcuni miglioramenti di Configuration Manager per semplificare il processo. Nel frattempo, se è necessario aggiungere repliche secondarie, vedere il bloc seguente disponibile nella libreria TechNet per indicazioni utili
-   [ConfigMgr 1702: Adding a new node (Secondary Replica) to an existing SQL AO AG](https://blogs.technet.microsoft.com/umairkhan/2017/07/17/configmgr-1702-adding-a-new-node-secondary-replica-to-an-existing-sql-ao-ag/) (Aggiungere un nuovo nodo (replica secondaria) a un gruppo di disponibilità SQL AlwaysOn esistente)

### <a name="to-remove-a-replica-member"></a>Per rimuovere un membro di replica
Per questa procedura usare le informazioni contenute in [Rimuovere una replica secondaria da un gruppo di disponibilità](/sql/database-engine/availability-groups/windows/remove-a-secondary-replica-from-an-availability-group-sql-server) nella documentazione di SQL Server.  


## <a name="configure-an-asynchronous-commit-replica"></a>Configurare una replica con commit asincrono
A partire da Configuration Manager versione 1706, è possibile aggiungere una replica asincrona a un gruppo di disponibilità usato con Configuration Manager. A questo scopo, non è necessario eseguire gli script di configurazione richiesti per configurare una replica sincrona perché non viene offerto supporto per l'uso di tale replica asincrona come database del sito. Per altre informazioni sull'aggiunta di repliche secondarie ai gruppi di disponibilità, vedere la [documentazione di SQL Server](https://msdn.microsoft.com/library/hh213247(v=sql.120).aspx(d=robot)).

## <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Usare la replica asincrona per il ripristino del sito
Con Configuration Manager versione 1706 e successive, è possibile usare una replica asincrona per recuperare il database del sito. A questo scopo, è necessario arrestare il sito primario attivo per impedire operazioni di scrittura aggiuntive nel database del sito. Dopo aver arrestato il sito, è possibile usare una replica asincrona al posto di un [database ripristinato manualmente](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption).

Per arrestare il sito, è possibile usare lo[Strumento di manutenzione gerarchia](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe) per interrompere i servizi principali nel server del sito. Usare la riga di comando: **Preinst.exe /stopsite**   

Arrestare il sito equivale ad arrestare il servizio Gestione componenti del sito (sitecomp) e poi il servizio SMS_Executive service, nel server del sito.

<!-- For inclusion with passive primary site support:
> [!TIP]  
> If you use a primary passive replica (introduced in version [TBD],  you do not need to stop the passive replica. Only the active primary site must be stopped.
-->  

## <a name="stop-using-an-availability-group"></a>Interrompere l'uso di un gruppo di disponibilità
Usare la procedura seguente se non si vuole più ospitare il database del sito in un gruppo di disponibilità. Implica il dover riportare il database del sito a una singola istanza di SQL Server.

Per completare la procedura, l'account usato deve:
-   Essere membro del gruppo **Administrators locale** su ogni computer membro del gruppo di disponibilità.
-   Essere **amministratore di sistema** in ogni istanza di SQL Server che ospita il database del sito.

> [!IMPORTANT]  
> Quando si usa Microsoft Intune con Configuration Manager in una configurazione ibrida, lo spostamento del database del sito da o verso un gruppo di disponibilità attiva la risincronizzazione dei dati con il cloud. Non è possibile evitare questo problema.

### <a name="to-move-the-site-database-from-an-availability-group-back-to-a-single-instance-sql-server"></a>Per spostare il database del sito da un gruppo di disponibilità a un'istanza singola di SQL Server
1.  Usare il comando seguente per arrestare il sito di Configuration Manager: **Preinst.exe /stopsite**. Per altre informazioni, vedere [Strumento di manutenzione gerarchia](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe).

2.  Usare SQL Server per creare un backup completo del database del sito dalla replica primaria. Per informazioni su come completare questo passaggio, vedere [Creare un backup completo del database (SQL Server)](/sql/relational-databases/backup-restore/create-a-full-database-backup-sql-server) nella documentazione di SQL Server.

3.  Se il server che funge da replica primaria del gruppo di disponibilità ospita l'istanza singola del database del sito, è possibile ignorare questo passaggio:  

    -   Usare SQL Server per ripristinare il backup del database del sito nel server che ospiterà il database del sito. Vedere [Ripristinare un backup del database tramite SSMS](/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms) nella documentazione di SQL Server.   <br />  <br />

4.  Nel server che ospiterà il database del sito, che sia la replica primaria o il server in cui è stato ripristinato il database del sito, modificare il modello di backup del database del sito da **Completo** a **Semplice**. Vedere [Visualizzazione o modifica del modello di recupero di un database](/sql/relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server) nella documentazione di SQL Server.  

5.  Eseguire **Installazione di Configuration Manager** da **&lt;*cartella di installazione del sito di Configuration Manager>* \BIN\X64\setup.exe**.

6.  Nella pagina **Riquadro attività iniziale** selezionare **Esegui una manutenzione del sito o reimposta il sito**, quindi fare clic su **Avanti**.  

7.  Selezionare l'opzione **Modifica la configurazione di SQL Server** , quindi fare clic su **Avanti**.  

8.  Riconfigurare quanto segue per il database del sito:
    -   **Nome server SQL:** immettere il nome del server che ora ospita il database del sito.

    -   **Istanza**: specificare l'istanza denominata che ospita il database del sito o lasciare vuoto il campo se il database si trova nell'istanza predefinita.

    -   **Database**: non modificare il nome visualizzato. È il nome del database del sito corrente.    

9.  Dopo aver specificato le informazioni per il nuovo percorso del database, completare l'installazione con il processo e le configurazioni normali. Al termine dell'installazione, il sito viene riavviato e inizia a usare il nuovo percorso del database.    

10. Per pulire i server che erano membri del gruppo di disponibilità, seguire le indicazioni riportate in [Rimuovere un gruppo di disponibilità](/sql/database-engine/availability-groups/windows/remove-an-availability-group-sql-server) nella documentazione di SQL Server.

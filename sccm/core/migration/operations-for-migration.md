---
title: Operazioni di migrazione | Microsoft Docs
description: Creare ed eseguire processi per la migrazione di dati e client a System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c28e3492-851a-40fc-ba13-67ebc2d8b41a
caps.latest.revision: 6
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5e3d3f4194b06442e34c10988a20fe9ca40ac5d7
ms.openlocfilehash: 3b5fc05542125454e224df73344cb29cb5f502ef


---
# <a name="operations-for-migrating-to-system-center-configuration-manager"></a>Operazioni per la migrazione a System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile iniziare la migrazione di dati e client in System Center Configuration Manager dopo aver raccolto correttamente i dati da un sito di origine in una gerarchia di origine supportata. Utilizzare le informazioni nelle sezioni riportate di seguito per creare ed eseguire i processi di migrazione per la migrazione di dati, client e quindi completare il processo di migrazione.  

-   [Creare e modificare i processi di migrazione](#Create_Edit_migration_Jobs)  

-   [Eseguire i processi di migrazione](#Run_Migration_Jobs)  

-   [Aggiornare o riassegnare un punto di distribuzione condiviso](#BKMK_ProcUpgrdSS)  

-   [Monitorare l'attività di migrazione nell'area di lavoro Migrazione](#Monitor_MIgration)  

-   [Eseguire la migrazione dei client](#BKMK_MigrateClients)  

-   [Completare la migrazione](#Complete_Migration)  

##  <a name="a-namecreateeditmigrationjobsa-create-and-edit-migration-jobs"></a><a name="Create_Edit_migration_Jobs"></a> Creare e modificare i processi di migrazione  
 Utilizzare le seguenti procedure per creare processi di migrazione dei dati, modificare l'elenco di esclusione per i processi di migrazione basati su raccolte, configurare i punti di distribuzione condivisi e modificare le pianificazioni dei processi di migrazione.  

> [!NOTE]  
>  La procedura seguente per la creazione di un processo di migrazione, che esegue la migrazione per raccolte, viene applicata solo alle gerarchie di origine che eseguono una versione supportata di Configuration Manager 2007. Il tipo di processo di migrazione basato su raccolte non è disponibile quando si esegue la migrazione da una gerarchia di origine di System Center 2012 Configuration Manager o System Center Configuration Manager.  

#### <a name="to-create-a-migration-job-to-migrate-by-collections"></a>Per creare un processo di migrazione per eseguire la migrazione per raccolte  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Migrazione**e quindi fare clic su **Processi di migrazione**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea processo di migrazione**.  

4.  Nella pagina **Generale** della Creazione guidata del processo di migrazione configurare gli elementi seguenti e quindi fare clic su **OK**:  

    -   Specificare un nome per il processo di migrazione.  

    -   Nell'elenco a discesa **Tipo di processo** selezionare **Migrazione raccolta**.  

5.  Nella pagina **Seleziona raccolte** configurare gli elementi seguenti e quindi fare clic su **Avanti**:  

    -   Selezionare le raccolte da migrare.  

    -   Se si desidera migrare solo le raccolte e non gli oggetti associati a tali raccolte, deselezionare l'opzione **Esegui la migrazione degli oggetti associati alle raccolte specificate** . Se si deseleziona questa opzione, in questo processo non verrà migrato nessun oggetto associato ed è possibile ignorare i passaggi 6 e 7.  

6.  Nella pagina **Seleziona oggetti** deselezionare tutti i tipi di oggetto oppure specifici oggetti disponibili che non si desidera migrare. Per impostazione predefinita, vengono selezionati tutti gli oggetti disponibili e tutti i tipi di oggetto associati. Fare quindi clic su **Avanti**.  

7.  Nella pagina **Proprietà contenuto** assegnare la proprietà del contenuto da ciascun sito di origine elencato a un sito nella gerarchia di destinazione e quindi fare clic su **Avanti**.  

8.  Nella pagina **Ambito di protezione** selezionare uno o più ambiti di protezione dell'amministrazione basata su ruoli da assegnare agli oggetti da migrare in questo processo di migrazione e quindi fare clic su **Avanti**.  

9. Nella pagina **Limitazione della raccolta** configurare una raccolta dalla gerarchia di destinazione per limitare l'ambito di ogni raccolta elencata e quindi fare clic su **Avanti**. In alternativa, se non è elencata alcuna raccolta, fare clic su **Avanti**.  

10. Nella pagina **Sostituzione dei codici del sito**, assegnare un codice del sito dalla gerarchia di destinazione per sostituire il codice del sito di Configuration Manager 2007 per ogni raccolta elencata e fare clic su **Avanti**. In alternativa, se non è elencata alcuna raccolta, fare clic su **Avanti**.  

11. Nella pagina **Riesamina informazioni** fare clic su **Salva nel file** per salvare le informazioni per una visualizzazione successiva. Per continuare, fare clic su **Avanti**.  

12. Nella pagina **Impostazioni** configurare il momento in cui eseguire il processo di migrazione ed eventuali impostazioni aggiuntive necessarie per questo processo di migrazione, quindi fare clic su **Avanti**.  

13. Confermare le impostazioni e completare la procedura guidata.  

#### <a name="to-create-a-migration-job-to-migrate-by-objects"></a>Per creare un processo di migrazione per eseguire la migrazione per oggetti  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Migrazione**e quindi fare clic su **Processi di migrazione**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea processo di migrazione**.  

4.  Nella pagina **Generale** della Creazione guidata del processo di migrazione configurare gli elementi seguenti e quindi fare clic su **Avanti**:  

    -   Specificare un nome per il processo di migrazione.  

    -   Nell'elenco a discesa **Tipo di processo** selezionare **Migrazione oggetti**.  

5.  Nella pagina **Seleziona oggetti** selezionare i tipi di oggetto da migrare. Per impostazione predefinita, vengono selezionati tutti gli oggetti disponibili per ogni tipo di oggetto selezionato.  

6.  Nella pagina **Proprietà contenuto** assegnare la proprietà del contenuto da ciascun sito di origine elencato a un sito nella gerarchia di destinazione e quindi fare clic su **Avanti**. In alternativa, se non è elencato alcuna sito di origine, fare clic su **Avanti**.  

7.  Nella pagina **Ambito di protezione** selezionare uno o più ambiti di protezione dell'amministrazione basata su ruoli da assegnare agli oggetti in questo processo di migrazione e quindi fare clic su **Avanti**.  

8.  Nella pagina **Riesamina informazioni** fare clic su **Salva nel file** per salvare le informazioni per una visualizzazione successiva. Per continuare, fare clic su **Avanti**.  

9. Nella pagina **Impostazioni** configurare il momento in cui eseguire la migrazione ed eventuali impostazioni aggiuntive necessarie per questo processo di migrazione. Fare quindi clic su **Avanti**.  

10. Confermare le impostazioni e completare la procedura guidata.  

#### <a name="to-create-a-migration-job-to-migrate-changed-objects"></a>Per creare un processo di migrazione per eseguire la migrazione di oggetti modificati  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Migrazione**e quindi fare clic su **Processi di migrazione**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea processo di migrazione**.  

4.  Nella pagina **Generale** della Creazione guidata del processo di migrazione configurare gli elementi seguenti e quindi fare clic su **Avanti**:  

    -   Specificare un nome per il processo di migrazione.  

    -   Nell'elenco a discesa **Tipo di processo** selezionare **Oggetti modificati dopo la migrazione**.  

5.  Nella pagina **Seleziona oggetti** selezionare i tipi di oggetto da migrare. Per impostazione predefinita, vengono selezionati tutti gli oggetti disponibili per ogni tipo di oggetto selezionato.  

6.  Nella pagina **Proprietà contenuto** assegnare la proprietà del contenuto da ciascun sito di origine elencato a un sito nella gerarchia di destinazione e quindi fare clic su **Avanti**. In alternativa, se non è elencato alcuna sito di origine, fare clic su **Avanti**.  

7.  Nella pagina **Ambito di protezione** selezionare uno o più ambiti di protezione dell'amministrazione basata su ruoli da assegnare agli oggetti in questo processo di migrazione e quindi fare clic su **Avanti**.  

8.  Nella pagina **Riesamina informazioni** fare clic su **Salva nel file** per salvare le informazioni per una visualizzazione successiva. Per continuare, fare clic su **Avanti**.  

9. Nella pagina **Impostazioni** configurare il momento in cui eseguire la migrazione ed eventuali impostazioni aggiuntive necessarie per questo processo di migrazione. Diversamente dagli altri tipi di processi di migrazione, questo processo deve sovrascrivere gli oggetti migrati in precedenza nel database di System Center Configuration Manager. Fare clic su **Avanti**.  

10. Confermare le impostazioni e quindi completare la procedura guidata.  

###  <a name="a-namebkmkmodifyexclusionlista-to-modify-the-exclusion-list-for-migration"></a><a name="BKMK_Modify_Exclusion_List"></a> Per modificare l'elenco di esclusione per la migrazione  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** fare clic su **Migrazione** per ottenere l'accesso all'elenco di esclusione. È possibile accedere all'elenco di esclusione anche dal nodo **Gerarchia di origine** o **Processi di migrazione** .  

3.  Nella scheda **Home** , nel gruppo **Migrazione** , fare clic su **Modifica elenco di esclusione**.  

4.  Nella finestra di dialogo **Modifica elenco di esclusione** selezionare l'oggetto escluso che si desidera rimuovere dall'elenco di esclusione e quindi fare clic su **Rimuovi**.  

5.  Fare clic su **OK** per salvare le modifiche e completare la modifica. Per annullare le modifiche correnti e ripristinare tutti gli oggetti rimossi, fare clic su **Annulla**e quindi su **No**. In questo modo verrà annullata la rimozione degli oggetti e la finestra di dialogo **Modifica elenco di esclusione** verrà chiusa.  

#### <a name="to-share-distribution-points-from-the-source-hierarchy"></a>Per condividere i punti di distribuzione dalla gerarchia di origine  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Migrazione**, fare clic su **Gerarchia di origine**e quindi selezionare il sito di origine da configurare.  

3.  Nella scheda **Home** , nel gruppo **Sito di origine** , fare clic su **Configura**.  

4.  Nella finestra di dialogo **Credenziali del sito di origine** selezionare **Abilita la condivisione dei punti di distribuzione per il server del sito di origine**e quindi fare clic su **OK**.  

5.  Al termine della raccolta dati, fare clic su **Chiudi**.  

#### <a name="to-change-the-schedule-of-a-migration-job"></a>Per modificare la pianificazione di un processo di migrazione  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Migrazione**e quindi fare clic su **Processi di migrazione**.  

3.  Fare clic sul processo di migrazione da modificare. Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

4.  Nelle proprietà del processo di migrazione selezionare la scheda **Impostazioni** , modificare il tempo di esecuzione per il processo di migrazione e quindi fare clic su **OK**.  

##  <a name="a-namerunmigrationjobsa-run-migration-jobs"></a><a name="Run_Migration_Jobs"></a> Eseguire i processi di migrazione  
 Utilizzare la seguente procedura per eseguire un processo di migrazione non ancora avviato.  

#### <a name="to-run-migration-jobs"></a>Per eseguire i processi di migrazione  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Migrazione**e quindi fare clic su **Processi di migrazione**.  

3.  Fare clic sul processo di migrazione da eseguire. Nella scheda **Home** , nel gruppo **Processo di migrazione** , fare clic su **Avvia**.  

4.  Fare clic su **Sì** per avviare subito il processo di migrazione.  

##  <a name="a-namebkmkprocupgrdssa-upgrade-or-reassign-a-shared-distribution-point"></a><a name="BKMK_ProcUpgrdSS"></a> Aggiornare o riassegnare un punto di distribuzione condiviso  
 È possibile aggiornare un punto di distribuzione supportato condiviso da un sito di origine di Configuration Manager 2007 oppure riassegnare un punto di distribuzione supportato condiviso da un sito di origine di System Center Configuration Manager in modo che diventi un punto di distribuzione nella gerarchia di destinazione.  

> [!IMPORTANT]  
>  Prima di aggiornare un punto di distribuzione secondario di Configuration Manager 2007, è necessario disinstallare il software client di Configuration Manager 2007 dal computer del punto di distribuzione secondario. Se il software client di Configuration Manager 2007 viene installato durante il tentativo di aggiornamento del punto di distribuzione, l'aggiornamento ha esito negativo e il contenuto precedentemente distribuito a un punto di distribuzione secondario viene rimosso dal computer.  

> [!CAUTION]  
>  Quando si aggiorna o si riassegna un punto di distribuzione condiviso, il computer di sistema del sito e il ruolo di sistema del sito del punto di distribuzione vengono rimossi dal sito di origine e aggiunti come punto di distribuzione al sito nella gerarchia di destinazione selezionata.  

#### <a name="to-upgrade-or-reassign-a-shared-distribution-point"></a>Per aggiornare o riassegnare un punto di distribuzione condiviso  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Migrazione**, quindi fare clic su **Gerarchia di origine**.  

3.  Selezionare il sito che possiede il punto di distribuzione da aggiornare, fare clic sulla scheda **Punti di distribuzione condivisi** e selezionare il punto di distribuzione appropriato da aggiornare o riassegnare.  

4.  Nella scheda **Punto di distribuzione** , nel gruppo **Punto di distribuzione** , fare clic su **Riassegna**.  

5.  Specificare le impostazioni in Riassegnazione guidata punti di distribuzione condivisi come per l'installazione di un nuovo punto di distribuzione per la gerarchia di destinazione, con le seguenti aggiunte:  

    -   Nella pagina **Conversione del contenuto** controllare le indicazioni relative allo spazio richiesto per convertire il contenuto esistente. Nella pagina **Impostazioni unità** della procedura guidata verificare quindi che nell'unità del computer del punto di distribuzione selezionata sia disponibile la quantità di spazio libero su disco necessaria.  

6.  Confermare le impostazioni e quindi completare la procedura guidata.  

##  <a name="a-namemonitormigrationa-monitor-migration-activity-in-the-migration-workspace"></a><a name="Monitor_MIgration"></a> Monitorare l'attività di migrazione nell'area di lavoro Migrazione  
 Usare la procedura seguente per monitorare la migrazione tramite la console di Configuration Manager.  

#### <a name="to-monitor-migration-activity-in-the-migration-workspace"></a>Per monitorare l'attività di migrazione nell'area di lavoro di migrazione  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Migrazione**e quindi fare clic su **Processi di migrazione**.  

3.  Fare clic sul processo di migrazione da monitorare.  

4.  Visualizzare i dettagli e lo stato relativi al processo di migrazione selezionato nelle schede **Riepilogo** e **Oggetti nel processo**.  

##  <a name="a-namebkmkmigrateclientsa-migrate-clients"></a><a name="BKMK_MigrateClients"></a> Eseguire la migrazione dei client  
 Dopo aver eseguito la migrazione dei dati per i client da una gerarchia all'altra, ma prima di completare tale operazione, pianificare la migrazione dei client nella gerarchia di destinazione. La migrazione di client da una gerarchia all'altra comporta la disinstallazione del software client di Configuration Manager dai computer assegnati alla gerarchia di origine e l'installazione del software client di Configuration Manager dalla gerarchia di destinazione. Quando si installa il client dalla gerarchia di destinazione si assegna anche il client a un sito primario in tale gerarchia. Per altre informazioni sulla migrazione dei client, vedere [Pianificazione di una strategia di migrazione client in System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).  

##  <a name="a-namecompletemigrationa-complete-migration"></a><a name="Complete_Migration"></a> Completare la migrazione  
 Utilizzare questa procedura per completare la migrazione dalla gerarchia di origine.  

#### <a name="to-complete-migration"></a>Per completare la migrazione  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Migrazione**, quindi fare clic su **Gerarchia di origine**.  

3.  Per una gerarchia di origine di Configuration Manager 2007, selezionare un sito di origine nel livello inferiore della gerarchia di origine. Per una gerarchia di origine di System Center 2012 Configuration Manager o System Center Configuration Manager, selezionare il sito di origine disponibile.  

4.  Nella scheda **Home** , nel gruppo **Pulisci** , fare clic su **Interrompi raccolta dati**.  

5.  Fare clic su **Sì** per confermare l'azione.  

6.  Per una gerarchia di origine di Configuration Manager 2007, ripetere i passaggi 3, 4 e 5 prima di passare al passaggio successivo. Eseguire questi passaggi in ciascun sito della gerarchia, dal livello inferiore a quello superiore. Per una gerarchia di origine di System Center 2012 Configuration Manager o System Center Configuration Manager, continuare con il passaggio successivo.  

7.  Nella scheda **Home** , nel gruppo **Pulisci** , fare clic su **Pulisci dati migrazione**.  

8.  Nella finestra di dialogo **Pulisci dati migrazione** selezionare dall'elenco a discesa **Gerarchia di origine** il codice e il server del sito del sito di livello superiore della gerarchia di origine e quindi fare clic su **OK**.  

9. Fare clic su **Sì** per completare il processo di migrazione per la gerarchia di origine.  



<!--HONumber=Dec16_HO3-->



---
title: Eseguire la migrazione del contenuto | System Center Configuration Manager
description: Usare i punti di distribuzione per gestire il contenuto durante la migrazione dei dati a una gerarchia di destinazione di System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 66f7759c-6272-4116-aad7-0d05db1d46cd
caps.latest.revision: 8
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: aa88f18247b49995bff4a4a6f5fd1e1ed70ca214


---
# <a name="planning-a-content-deployment-migration-strategy-in-system-center-configuration-manager"></a>Pianificazione di una strategia di migrazione per la distribuzione del contenuto in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Mentre si esegue la migrazione attiva dei dati in una gerarchia di destinazione di System Center Configuration Manager, i client di Configuration Manager in entrambe le gerarchie di origine e destinazione possono mantenere l'accesso al contenuto distribuito nella gerarchia di origine. Inoltre, è possibile utilizzare la migrazione per aggiornare o riassegnare i punti di distribuzione dalla gerarchia di origine come punti di distribuzione nella gerarchia di destinazione. Quando si condividono e aggiornano o riassegnano i punti di distribuzione, questa strategia consente di evitare la redistribuzione del contenuto nella gerarchia di destinazione per i client di cui si effettua la migrazione.  

Sebbene sia possibile ricreare e distribuire il contenuto nella gerarchia di destinazione, è possibile utilizzare anche le seguenti opzioni per la gestione del contenuto:  

-   Condividere i punti di distribuzione nella gerarchia di origine con i client nella gerarchia di destinazione.  

-   Aggiornare i punti di distribuzione autonomi di Configuration Manager 2007 oppure i siti secondari di Configuration Manager 2007 nella gerarchia di origine in modo che diventino punti di distribuzione nella gerarchia di destinazione.  

-   Riassegnare i punti di distribuzione da una gerarchia di origine di System Center Configuration Manager a un sito nella gerarchia di destinazione.  

Utilizzare le sezioni seguenti per pianificare la distribuzione del contenuto durante la migrazione:  

-   [Condividere punti di distribuzione tra gerarchie di origine e destinazione](#About_Shared_DPs_in_Migration)  

-   [Pianificazione dell'aggiornamento dei punti di distribuzione condivisi di Configuration Manager 2007](#Planning_to_Upgrade_DPs)  

    -   [Processo di aggiornamento del punto di distribuzione](#BKIMK_UpgradeProcess)  

    -   [Planning to upgrade Configuration Manager 2007 secondary sites](#BKMK_UpgradeSS)  

-   [Pianificazione della riassegnazione dei punti di distribuzione di System Center Configuration Manager](#BKMK_ReassignDistPoint)  

    -   [Processo di riassegnazione dei punti di distribuzione](#BKMK_ReassignProcess)  

-   [Proprietà del contenuto durante la migrazione del contenuto](#About_Migrating_Content)  

##  <a name="a-nameaboutshareddpsinmigrationa-share-distribution-points-between-source-and-destination-hierarchies"></a><a name="About_Shared_DPs_in_Migration"></a> Condividere punti di distribuzione tra gerarchie di origine e destinazione  
Durante la migrazione, è possibile condividere i punti di distribuzione di una gerarchia di origine con la gerarchia di destinazione. È possibile utilizzare punti di distribuzione condivisi per rendere il contenuto di cui si è effettuata la migrazione da una gerarchia di origine immediatamente disponibile ai client della gerarchia di destinazione senza dover ricreare quel contenuto, quindi distribuirlo nei nuovi punti di distribuzione nella gerarchia di destinazione. Quando i client della gerarchia di destinazione richiedono il contenuto che viene distribuito nei punti di distribuzione condivisi, i punti di distribuzione condivisi possono essere forniti ai client come percorsi di contenuto validi.  

 Oltre a essere un percorso di contenuto valido per i client nella gerarchia di destinazione finché la migrazione dalla gerarchia di origine è attiva, è possibile aggiornare o riassegnare un punto di distribuzione alla gerarchia di destinazione. È possibile aggiornare i punti di distribuzione condivisi di Configuration Manager 2007 e riassegnare i punti di distribuzione condivisi di System Center 2012 Configuration Manager. Quando si aggiorna o si riassegna un punto di distribuzione condiviso, il punto di distribuzione viene rimosso dalla gerarchia di origine e diventa un punto di distribuzione nella gerarchia di destinazione. Dopo aver aggiornato o riassegnato un punto di distribuzione condiviso, è possibile continuare a utilizzare il punto di distribuzione nella gerarchia di destinazione dopo che la migrazione dalla gerarchia di origine sia terminata. Per ulteriori informazioni su come aggiornare un punto di distribuzione condiviso, vedere [Planning to upgrade Configuration Manager 2007 shared distribution points](#Planning_to_Upgrade_DPs). Per informazioni su come riassegnare un punto di distribuzione condiviso, vedere [Pianificazione della riassegnazione dei punti di distribuzione di System Center Configuration Manager](#BKMK_ReassignDistPoint).  

 È possibile scegliere punti di distribuzione da qualsiasi sito di origine nella gerarchia di origine. Quando si condividono punti di distribuzione per un sito di origine, vengono condivisi tutti i punti di distribuzione validi in quel sito primario e in ciascuno dei siti secondari figlio di tale sito primario. Per poter diventare un punto di distribuzione condiviso, il server del sistema del sito che ospita il punto di distribuzione deve essere configurato con un nome di dominio completo (FQDN). Tutti i punti di distribuzione configurati con un nome NetBIOS vengono ignorati.  

> [!TIP]  
>  Configuration Manager 2007 non richiede la configurazione di un FQDN per i server di sistema del sito.  

Per la pianificazione dei punti di distribuzione condivisi, utilizzare le seguenti informazioni:  

-   I punti di distribuzione condivisi devono soddisfare i prerequisiti per i punti di distribuzione condivisi. Per informazioni su questi prerequisiti, vedere la sezione [Configurazioni necessarie per la migrazione](../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations) nell'argomento [Prerequisiti per la migrazione in System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md).  

-   L'azione di condivisione del punto di distribuzione è un'impostazione a livello di sito che condivide tutti i punti di distribuzione validi in un sito di origine e in tutti i siti secondari figlio diretti. Non è possibile selezionare singoli punti di distribuzione da condividere quando si abilita la condivisione dei punti di distribuzione.  

-   I client nella gerarchia di destinazione possono ricevere informazioni sul percorso dei contenuti per i pacchetti distribuiti nei punti di distribuzione che vengono condivisi nella gerarchia di origine. Per i punti di distribuzione di una gerarchia di origine di Configuration Manager 2007, sono inclusi i punti di distribuzione secondari, i punti di distribuzione nelle condivisioni server e i punti di distribuzione standard.  

    > [!WARNING]  
    >  Se si modifica la gerarchia di origine, i punti di distribuzione condivisi dalla gerarchia di origine originale non sono più disponibili e non possono essere forniti come percorsi di contenuti ai client nella gerarchia di destinazione. Se si riconfigura la migrazione per utilizzare la gerarchia di origine originale, vengono ripristinati i punti di distribuzione condivisi in precedenza come server con percorso dei contenuti validi.  

-   Quando si effettua la migrazione di un pacchetto ospitato su un punto di distribuzione condiviso, la versione del pacchetto deve rimanere la stessa nelle gerarchie di origine e di destinazione. Quando la versione del pacchetto non è la stessa nella gerarchia di origine e di destinazione, i client nella gerarchia di destinazione non possono recuperare il contenuto dal punto di distribuzione condiviso. Pertanto, se si aggiorna il pacchetto nella gerarchia di origine, è necessario rieseguire la migrazione dei dati del pacchetto prima che i client nella gerarchia di destinazione possano recuperare tale contenuto da un punto di distribuzione condiviso.  

    > [!NOTE]  
    >  Quando si visualizzano i dettagli per un pacchetto ospitato su un punto di distribuzione condiviso, il numero di pacchetti visualizzati come **Pacchetti migrati ospitati** sulla scheda **Punti di distribuzione condivisi** dei siti di origine non viene aggiornato finché non termina il ciclo di raccolta dati successivo.  

-   È possibile visualizzare i punti di distribuzione condivisi e le loro proprietà nel nodo **Gerarchia di origine** dell'area di lavoro **Amministrazione** nella console di Configuration Manager che si connette alla gerarchia di destinazione.  

-   Non è possibile usare un punto di distribuzione condiviso da una gerarchia di origine di Configuration Manager 2007 per ospitare pacchetti per Microsoft Application Virtualization (App-V). È necessario migrare i pacchetti App-V e convertirli per essere utilizzati dai client nella gerarchia di destinazione. È possibile tuttavia usare un punto di distribuzione condiviso da una gerarchia di System Center 2012 Configuration Manager o System Center Configuration Manager per ospitare i pacchetti App-V per client in una gerarchia di destinazione.  

-   Quando si condivide un punto di distribuzione protetto da una gerarchia di origine di Configuration Manager 2007, la gerarchia di destinazione crea un gruppo di limiti che include i percorsi di rete protetti di tale punto di distribuzione. Non è possibile modificare questo gruppo di limiti nella gerarchia di destinazione. Se si modificano tuttavia le informazioni sui limiti protetti per il punto di distribuzione nella gerarchia di origine di Configuration Manager 2007, tale modifica si riflette nella gerarchia di destinazione dopo il termine del ciclo di raccolta dati successivo.  

    > [!NOTE]  
    >  Poiché i siti di System Center 2012 Configuration Manager e System Center Configuration Manager seguono il concetto di punti di distribuzione preferiti invece di punti di distribuzione protetti, tale condizione si applica solo ai punti di distribuzione che vengono condivisi dai siti di origine di Configuration Manager 2007.  

Prima di condividere punti di distribuzione da un sito di origine, i punti di distribuzione idonei non sono visibili nella console di Configuration Manager. Dopo aver condiviso i punti di distribuzione, vengono elencati solo i punti di distribuzione condivisi correttamente.  

Dopo aver condiviso i punti di distribuzione, è possibile modificare la configurazione di tutti i punti di distribuzione condivisi nella gerarchia di origine. Le modifiche apportate alla configurazione di un punto di distribuzione vengono riflesse nella gerarchia di destinazione dopo il ciclo di raccolta dati successivo. I punti di distribuzione aggiornati per la condivisione vengono condivisi automaticamente, mentre quelli che non soddisfano più le condizioni interrompono la condivisione dei punti di distribuzione. Ad esempio, si potrebbe avere un punto di distribuzione che non è configurato con un FQDN intranet e che non veniva inizialmente condiviso con la gerarchia di destinazione. Dopo aver configurato l'FQDN per tale punto di distribuzione, il ciclo di raccolta dati successivo identifica questa configurazione e il punto di distribuzione viene quindi condiviso con la gerarchia di destinazione.  

##  <a name="a-nameplanningtoupgradedpsa-planning-to-upgrade-configuration-manager-2007-shared-distribution-points"></a><a name="Planning_to_Upgrade_DPs"></a> Pianificazione dell'aggiornamento dei punti di distribuzione condivisi di Configuration Manager 2007  
Quando si esegue la migrazione da una gerarchia di origine di Configuration Manager 2007, è possibile aggiornare un punto di distribuzione condiviso per renderlo un punto di distribuzione di System Center Configuration Manager. È possibile aggiornare i punti di distribuzione sia su siti primari che su siti secondari. Il processo di aggiornamento rimuove il punto di distribuzione dalla gerarchia di Configuration Manager 2007 e lo rende come server di sistema del sito nella gerarchia di destinazione. Questo processo copia anche il contenuto esistente che si trova sul punto di distribuzione in un nuovo percorso sul computer del punto di distribuzione. Il processo di aggiornamento quindi modifica la copia del contenuto per creare l'archivio a istanza singola di  da utilizzare con la distribuzione contenuti di nella gerarchia di destinazione. Quando si aggiorna un punto di distribuzione, non è necessario ridistribuire il contenuto di cui è stata eseguita la migrazione ospitato nel punto di distribuzione di Configuration Manager 2007.  

Dopo che Configuration Manager converte il contenuto nell'archivio in un'istanza singola, elimina il contenuto di origine nel computer del punto di distribuzione per liberare spazio su disco e non usa il percorso del contenuto di origine.  

Non tutti i punti di distribuzione di Configuration Manager 2007, che è possibile condividere, sono idonei all'aggiornamento a System Center Configuration Manager. Per essere idoneo all'aggiornamento, un punto di distribuzione di Configuration Manager 2007 deve soddisfare le condizioni per l'aggiornamento che includono il server di sistema del sito in cui è installato il punto di distribuzione e il tipo di punto di distribuzione di Configuration Manager 2007 installato. Ad esempio, non è possibile aggiornare nessun tipo di punto di distribuzione installato sul computer del server del sito su un sito primario, ma è possibile aggiornare un punto di distribuzione standard installato sul computer del server del sito su un sito secondario.  

> [!NOTE]  
>  È possibile aggiornare solo quei punti di distribuzione condivisi di Configuration Manager 2007 che sono in un computer con una versione di sistema operativo supportata per i punti di distribuzione nella gerarchia di destinazione. Ad esempio, anche se è possibile condividere un punto di distribuzione di Configuration Manager 2007 che si trova in un computer con Windows Vista, non è possibile aggiornare tale punto di distribuzione condiviso perché il sistema operativo non è supportato da System Center Configuration Manager per l'uso come punto di distribuzione.  

La tabella seguente elenca i percorsi supportati per ogni tipo di punto di distribuzione di Configuration Manager 2007 per i quali è possibile eseguire l'aggiornamento.  

|Tipo di punto di distribuzione|Punto di distribuzione in un computer del sistema del sito diverso dal server del sito|Punto di distribuzione in un computer del sistema del sito diverso dal server del sito e che ospita altri ruoli del sistema del sito|Punto di distribuzione in un server del sito secondario|  
|--------------------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------------------------------------------|  
|Punto di distribuzione standard|Sì|No|Sì|  
|Punto di distribuzione in condivisioni server<sup>1</sup>|Sì|No|No|  
|Punto di distribuzione secondario|Sì|No|No|  

 <sup>1</sup> System Center Configuration Manager non supporta le condivisioni server per i sistemi del sito, ma supporta l'aggiornamento di un punto di distribuzione di Configuration Manager 2007 che si trova su una condivisione server. Quando si esegue l'aggiornamento di un punto di distribuzione di Configuration Manager 2007 che si trova in una condivisione server, il tipo di punto di distribuzione viene automaticamente convertito in un server ed è necessario selezionare l'unità nel computer del punto di distribuzione che memorizzerà l'archivio del contenuto a istanza singola.  

> [!WARNING]  
>  Prima di aggiornare un punto di distribuzione secondario, disinstallare il software client di Configuration Manager 2007. Quando si esegue l'aggiornamento di un punto di distribuzione secondario che ha il software client di Configuration Manager 2007 installato, il contenuto precedentemente distribuito nel computer viene rimosso dal computer e l'aggiornamento del punto di distribuzione ha esito negativo.  

Per identificare i punti di distribuzione idonei all'aggiornamento nella console di Configuration Manager, nel nodo **Gerarchia di origine** selezionare un sito di origine e la scheda **Punti di distribuzione condivisi**. I punti di distribuzione idonei visualizzano **Sì** nella colonna **Idoneo per l'aggiornamento** .  

Quando si aggiorna un punto di distribuzione installato in un server del sito secondario di Configuration Manager 2007, il sito secondario viene disinstallato dalla gerarchia di origine. Benché questo scenario venga chiamato aggiornamento del sito secondario, si applica solo al ruolo del sistema del sito del punto di distribuzione. Il risultato è che il sito secondario non è aggiornato e verrà disinstallato. In questo modo, nel computer che era il server del sito secondario rimane solo un punto di distribuzione della gerarchia di destinazione. Dal momento che il sito secondario viene rimosso dalla gerarchia di origine, se si pianifica di aggiornare il punto di distribuzione in un sito secondario, vedere la sezione [Planning to upgrade Configuration Manager 2007 secondary sites](#BKMK_UpgradeSS) in questo argomento.  

###  <a name="a-namebkimkupgradeprocessa-distribution-point-upgrade-process"></a><a name="BKIMK_UpgradeProcess"></a> Processo di aggiornamento dei punti di distribuzione  
È possibile usare la console di Configuration Manager per aggiornare i punti di distribuzione di Configuration Manager 2007 condivisi con la gerarchia di destinazione. Se si aggiorna un punto di distribuzione condiviso, questo viene disinstallato dal sito di Configuration Manager 2007 e installato come punto di distribuzione collegato a un sito primario o secondario specificato nella gerarchia di destinazione. Il processo di aggiornamento crea una copia del contenuto migrato che viene archiviato nel punto di distribuzione, quindi converte tale copia in un archivio contenuti a istanza singola. Quando Configuration Manager converte un pacchetto in un archivio del contenuto a istanza singola, elimina tale pacchetto dalla condivisione SMSPKG nel computer del punto di distribuzione a meno che il pacchetto non abbia uno o più annunci configurati con **Esegui programma dal punto di distribuzione**.  

Per aggiornare il punto di distribuzione, Configuration Manager usa l'**account di accesso al sito di origine** configurato per raccogliere dati dal provider SMS del sito di origine. Nonostante questo account richieda solo l'autorizzazione **Lettura** affinché gli oggetti del sito possano raccogliere dati dal sito di origine, deve anche avere l'autorizzazione **Eliminazione** e **Modifica** per la classe **Sito** per poter rimuovere correttamente il punto di distribuzione dal sito di Configuration Manager 2007 durante l'aggiornamento.  

> [!NOTE]  
>  Configuration Manager può convertire il contenuto nell'archivio a istanza singola solo in un punto di distribuzione alla volta. Quando si configurano gli aggiornamenti di più punti di distribuzione, questi ultimi vengono accodati per l'aggiornamento ed elaborati uno alla volta.  

Prima di aggiornare un punto di distribuzione condiviso, assicurarsi che sia eseguita la migrazione di tutto il contenuto distribuito nel punto di distribuzione. Il contenuto che non viene migrato prima dell'aggiornamento del punto di distribuzione non sarà disponibile dopo l'aggiornamento nella gerarchia di destinazione. Quando si aggiorna un punto di distribuzione, il contenuto nei pacchetti migrati viene convertito in un formato compatibile con l'archivio a istanza singola della gerarchia di destinazione.  

Per aggiornare un punto di distribuzione dall'interno della console di Configuration Manager, il server di sistema del sito di Configuration Manager 2007 deve soddisfare le condizioni seguenti:  

-   La configurazione e il percorso dei punti di distribuzione devono essere idonei per l'aggiornamento.  

-   Il computer del punto di distribuzione deve avere uno spazio su disco sufficiente a garantire la conversione del contenuto dal formato di archiviazione contenuto di Configuration Manager 2007 nel formato di archiviazione a istanza singola. Questa conversione richiede uno spazio su disco disponibile pari alla dimensione del pacchetto più grande archiviato nel punto di distribuzione.  

-   Il computer del punto di distribuzione deve eseguire una versione del sistema operativo supportata come un punto di distribuzione nella gerarchia di destinazione.  

    > [!NOTE]  
    >  Quando Configuration Manager verifica l'idoneità di un punto di distribuzione per l'aggiornamento, non convalida la versione del sistema operativo del computer del punto di distribuzione.  

Per aggiornare un punto di distribuzione, nell'area di lavoro **Amministrazione** espandere **Migrazione**, quindi espandere il nodo **Gerarchia di origine** e infine selezionare il sito contenente il punto di distribuzione che si desidera aggiornare. Successivamente, nel riquadro dei dettagli, nella scheda **Punti di distribuzione condivisi** , selezionare il punto di distribuzione che si desidera aggiornare.  

È possibile verificare che il punto di distribuzione sia pronto per l'aggiornamento visualizzando lo stato nella colonna **Idoneo per la riassegnazione** .  Successivamente, nella barra multifunzione della console di Configuration Manager all'interno della scheda **Punti di distribuzione** del gruppo **Punto di distribuzione** selezionare **Riassegna**. Verrà visualizzata una procedura guidata che consente di completare l'aggiornamento del punto di distribuzione.  

Quando si aggiorna un punto di distribuzione condiviso, questo viene assegnato a un sito primario o secondario di scelta nella gerarchia di destinazione. Al termine dell'aggiornamento, il punto di distribuzione viene gestito come qualsiasi altro punto di distribuzione nella gerarchia di destinazione.  

È possibile monitorare l'avanzamento dell'aggiornamento del punto di distribuzione nella console di Configuration Manager selezionando il nodo **Migrazione dei punti di distribuzione** nel nodo **Migrazione** dell'area di lavoro **Amministrazione**. È inoltre possibile visualizzare le informazioni nel file **Migmctrl.log** nel server del sito di amministrazione centrale della gerarchia di destinazione oppure nel file **distmgr.log** nel server del sito nella gerarchia di destinazione che gestisce il punto di distribuzione aggiornato.  

> [!NOTE]  
>  Quando si aggiorna un punto di distribuzione alla gerarchia di destinazione, il ruolo di sistema del sito del punto di distribuzione viene rimosso dal sito di origine di Configuration Manager 2007. I pacchetti inviati al punto di distribuzione non vengono tuttavia aggiornati nella gerarchia di Configuration Manager 2007. Nella console di Configuration Manager 2007, i pacchetti inviati al punto di distribuzione continuano a elencare il computer del sistema del sito come punto di distribuzione con **Tipo** **Sconosciuto**. I successivi aggiornamenti del pacchetto in Configuration Manager 2007 danno come risultato la segnalazione di errori da parte di Distribution Manager nel file distmgr.log per tale sito quando prova ad aggiornare il pacchetto nel sistema del sito sconosciuto.  

Se si decide di non aggiornare un punto di distribuzione condiviso, è ancora possibile installare un punto di distribuzione da una gerarchia di destinazione in un punto di distribuzione di Configuration Manager 2007 precedente. Prima di installare il nuovo punto di distribuzione, è necessario disinstallare tutti i ruoli di sistema del sito di Configuration Manager 2007 dal computer del punto di distribuzione. Tale operazione include il sito di Configuration Manager 2007 qualora fosse il computer del server del sito. Se si disinstalla un punto di distribuzione di Configuration Manager 2007, il contenuto che era stato distribuito al punto di distribuzione non viene eliminato dal computer.  

###  <a name="a-namebkmkupgradessa-planning-to-upgrade-configuration-manager-2007-secondary-sites"></a><a name="BKMK_UpgradeSS"></a> Pianificazione per aggiornare i siti secondari di Configuration Manager 2007  
 Quando si usa la migrazione per aggiornare un punto di distribuzione condiviso ospitato in un server di un sito secondario di Configuration Manager 2007, Configuration Manager non solo aggiorna il ruolo di sistema del sito del punto di distribuzione per essere un punto di distribuzione nella gerarchia di destinazione, ma disinstalla anche il sito secondario dalla gerarchia di origine. Il risultato è un punto di distribuzione di System Center Configuration Manager, ma non un sito secondario.  

 Affinché un punto di distribuzione nel computer del server del sito sia idoneo all'aggiornamento, Configuration Manager deve essere in grado di disinstallare il sito secondario, inclusi tutti i ruoli di sistema del sito in tale computer. In genere, un punto di distribuzione condiviso in una condivisione server di Configuration Manager 2007 è idoneo all'aggiornamento. Tuttavia, in presenza di una condivisione server sul server del sito secondario, il sito secondario e qualsiasi punto di distribuzione condiviso su tale computer non sono idonei per l'aggiornamento. Ciò dipende dal fatto che quando il processo tenta di disinstallare il sito secondario, la condivisione del server viene considerata come un oggetto del sistema del sito aggiuntivo, e il processo non è in grado di disinstallare l'oggetto. In questo scenario, è possibile abilitare un punto di distribuzione standard sul server del sito secondario e quindi ridistribuire il contenuto in tal punto. In questo caso non viene utilizzata la larghezza di banda della rete e, al termine di tale operazione, è possibile disinstallare il punto di distribuzione nella condivisione del server, rimuovere quest'ultima e quindi aggiornare il punto di distribuzione e il sito secondario.  

 Prima di aggiornare un punto di distribuzione condiviso, verificare la configurazione di tale punto in Configuration Manager 2007 per evitare di aggiornare un punto di distribuzione in un sito secondario che si vuole ancora usare con Configuration Manager 2007. Questa operazione è necessaria perché dopo aver aggiornato un punto di distribuzione condiviso in un server del sito secondario, il server di sistema del sito viene rimosso dalla gerarchia di Configuration Manager 2007 e non è più disponibile in tale gerarchia. Quando viene rimosso il sito secondario, i punti di distribuzione che rimangono nel sito secondario diventano orfani. Ciò significa che non vengono gestiti da Configuration Manager 2007 e non sono più condivisi o idonei all'aggiornamento.  

> [! Avviso]  
>  Quando si visualizza un punto di distribuzione condiviso nella console di Configuration Manager, non è presente alcuna indicazione visibile che specifichi se un punto di distribuzione condiviso si trova in un server di sistema del sito remoto o nel server del sito secondario.  

 Si consiglia di aggiornare i siti secondari che dispongono di un punto di distribuzione condiviso in presenza di un sito secondario in un percorso di rete remoto utilizzato principalmente per controllare la distribuzione del contenuto in tale percorso. Dal momento che è possibile configurare il controllo della larghezza di banda per lo scenario in cui si distribuisce il contenuto in un punto di distribuzione di System Center Configuration Manager, è spesso possibile aggiornare un sito secondario a un punto di distribuzione, configurare il punto di distribuzione per i controlli della larghezza di banda ed evitare l'installazione di un sito secondario in tale percorso di rete nella gerarchia di destinazione.  

 Il processo di aggiornamento di un punto di distribuzione condiviso in un server del sito secondario opera allo stesso modo di qualsiasi altro aggiornamento di punto di distribuzione condiviso. Il contenuto viene copiato e convertito nell'archivio a istanza singola in uso dalla gerarchia di destinazione. Tuttavia, quando si esegue l'aggiornamento di un punto di distribuzione condivisa che si trova in un server del sito secondario, il processo di aggiornamento disinstalla anche il punto di gestione, se presente, e quindi disinstalla il sito secondario dal server. Il risultato è che il sito secondario viene rimosso dalla gerarchia di Configuration Manager 2007. Per disinstallare il sito secondario, Configuration Manager usa l'account configurato per raccogliere i dati dal sito di origine.  

 Durante l'aggiornamento, si verifica un ritardo tra il momento in cui il sito secondario di Configuration Manager 2007 viene disinstallato e il momento in cui l'installazione del punto di distribuzione nella gerarchia di destinazione inizia. Il ciclo di raccolta dei dati determina questo ritardo di un massimo di quattro ore. Il ritardo è volto a garantire il tempo necessario per la disinstallazione del sito secondario prima che l'installazione del nuovo punto di distribuzione abbia inizio.  

 Per ulteriori informazioni su come aggiornare un punto di distribuzione condiviso, vedere [Planning to upgrade Configuration Manager 2007 shared distribution points](#Planning_to_Upgrade_DPs).  

##  <a name="a-namebkmkreassigndistpointa-planning-to-reassign-system-center-configuration-manager-distribution-points"></a><a name="BKMK_ReassignDistPoint"></a> Pianificazione della riassegnazione dei punti di distribuzione di System Center Configuration Manager  
 Quando si esegue la migrazione da una versione supportata di System Center 2012 Configuration Manager a una gerarchia della stessa versione, è possibile riassegnare un punto di distribuzione condiviso dalla gerarchia di origine a un sito nella gerarchia di destinazione. Questa attività segue lo stesso concetto di aggiornamento di un punto di distribuzione di Configuration Manager 2007 per diventare un punto di distribuzione nella gerarchia di destinazione. È possibile riassegnare i punti di distribuzione sia da siti primari che da siti secondari. Tale azione determina la rimozione del punto di distribuzione dalla gerarchia di origine e rende il computer, con il relativo punto di distribuzione, un server del sistema del sito per un sito selezionato nella gerarchia di destinazione.  

 Quando si riassegna un punto di distribuzione, non è necessario ridistribuire il contenuto migrato che era stato ospitato sul punto di distribuzione del sito di origine. A differenza dell'aggiornamento di un punto di distribuzione di Configuration Manager 2007, la riassegnazione di un punto di distribuzione non richiede spazio su disco aggiuntivo nel computer del punto di distribuzione. Questo avviene perché a partire da System Center 2012 Configuration Manager, i punti di distribuzione usano il formato di archivio a istanza singola per il contenuto e il contenuto nel computer del punto di distribuzione non deve essere convertito quando il punto di distribuzione viene riassegnato tra le gerarchie.  

 Per essere idoneo alla riassegnazione, un punto di distribuzione di System Center 2012 Configuration Manager deve soddisfare i criteri seguenti:  

-   Un punto di distribuzione condiviso deve essere installato in un computer diverso dal server del sito.  

-   Un punto di distribuzione condiviso non può essere condiviso con eventuali ruoli del sistema del sito aggiuntivi.  

Per identificare i punti di distribuzione idonei alla riassegnazione nella console di Configuration Manager, nel nodo **Gerarchia di origine** selezionare un sito di origine e la scheda **Punti di distribuzione condivisi**. I punti di distribuzione idonei visualizzano l'opzione **Sì** nella colonna **Idoneo alla riassegnazione** (prima di System Center 2012 R2 Configuration Manager, la colonna era denominata **Idoneo per l'aggiornamento**).  

###  <a name="a-namebkmkreassignprocessa-distribution-point-reassignment-process"></a><a name="BKMK_ReassignProcess"></a> Processo di riassegnazione dei punti di distribuzione  
 È possibile usare la console di Configuration Manager per riassegnare i punti di distribuzione condivisi da una gerarchia di origine attiva. Quando si riassegna un punto di distribuzione condiviso, questo viene disinstallato dal sito di origine, quindi installato come un punto di distribuzione collegato a un sito primario o secondario specificato nella gerarchia di destinazione.  

 Per riassegnare il punto di distribuzione, la gerarchia di destinazione utilizza l'account di accesso al sito di origine configurato per raccogliere dati dal provider SMS del sito di origine. Per altre informazioni sulle autorizzazioni e sui prerequisiti aggiuntivi necessari, vedere [Prerequisiti per la migrazione in System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md).  

##  <a name="a-nameaboutmigratingcontenta-content-ownership-when-migrating-content"></a><a name="About_Migrating_Content"></a> Proprietà del contenuto durante la migrazione del contenuto  
 Quando si esegue la migrazione dei contenuti per le distribuzioni, è necessario assegnare l'oggetto contenuto a un sito nella gerarchia di destinazione. Il sito diventa quindi il proprietario di tale contenuto nella gerarchia di destinazione. Benché il sito di livello superiore della gerarchia di destinazione sia il sito che esegue la migrazione dei metadati per il contenuto, è il sito assegnato che accede ai file di origine per il contenuto nella rete.  

 Per ridurre al minimo la larghezza di banda di rete utilizzata durante la migrazione del contenuto, si consiglia di trasferire la proprietà del contenuto a un sito nella gerarchia di destinazione vicina nella rete del percorso del contenuto nella gerarchia di origine. Poiché le informazioni sul contenuto vengono condivise globalmente nella gerarchia di destinazione, saranno disponibili in tutti i siti.  

 Benché le informazioni sul contenuto vengano condivise in tutti i siti utilizzando la replica di database, i contenuti assegnati a un sito primario e quindi distribuiti nei punti di distribuzione in altri siti primari, vengono trasferiti utilizzando la replica basata su file. Il trasferimento viene instradato attraverso il sito di amministrazione centrale e quindi al sito primario aggiuntivo. Centralizzando i pacchetti che si prevede di distribuire in più siti primari prima o durante la migrazione quando si assegna un sito come proprietario del contenuto, è possibile ridurre i trasferimenti di dati in reti a larghezza di banda ridotta.  



<!--HONumber=Nov16_HO1-->



---
title: Pianificazione del processo di migrazione | System Center Configuration Manager
description: Usare i processi di migrazione per configurare i dati di cui si vuole eseguire la migrazione nell'ambiente di System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a70bfbd4-757a-4468-9312-1c3b373ef9fc
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 21e00064a8ecad3dd1c24b7f02bd0a8a8c36924f


---
# <a name="planning-a-migration-job-strategy-in-system-center-configuration-manager"></a>Pianificazione di una strategia di processo di migrazione in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare i processi di migrazione per configurare i dati specifici di cui si vuole eseguire la migrazione nell'ambiente di System Center Configuration Manager. I processi di migrazione identificano gli oggetti che si prevede di migrare e vengono eseguiti nel sito di livello superiore nella gerarchia di destinazione. È possibile configurare uno o più processi di migrazione per ogni sito di origine. In questo modo è possibile eseguire la migrazione di tutti gli oggetti in una sola volta o di limitati sottogruppi di dati in ogni processo.  

 È possibile creare i processi di migrazione dopo che Configuration Manager ha raccolto i dati da uno o più siti nella gerarchia di origine. È possibile migrare i dati in qualsiasi sequenza dai siti di origine da cui sono stati raccolti i dati. Con un sito di origine di Configuration Manager 2007 è possibile eseguire la migrazione dei dati solo dal sito in cui è stato creato l'oggetto. Con i siti di origine che eseguono System Center 2012 Configuration Manager o versioni successive, tutti i dati di cui è possibile eseguire la migrazione sono disponibili nel sito principale della gerarchia di origine.  

 Prima di eseguire la migrazione dei client da una gerarchia all'altra, verificare che gli oggetti utilizzati dai client siano stati migrati e che questi oggetti siano disponibili nella gerarchia di destinazione. Ad esempio, quando si esegue la migrazione da una gerarchia di origine di Configuration Manager 2007 SP2, si potrebbe ricevere un annuncio per contenuti che sono distribuiti in una raccolta personalizzata che contiene un client. In questo scenario è necessario eseguire la migrazione della raccolta, dell'annuncio e del contenuto associato prima di eseguire la migrazione del client. Questo avviene perché, se il contenuto, la raccolta e l'annuncio non vengono migrati prima della migrazione del client, i dati non potranno essere associati con il client nella gerarchia di destinazione. Se un client non è associato ai dati relativi a un annuncio e contenuto precedentemente eseguiti, il client potrebbe ricevere il contenuto per l'installazione nella gerarchia di destinazione che potrebbe non essere necessario. Se viene eseguita la migrazione del client dopo che sono stati migrati i dati, il client viene associato al contenuto e all'annuncio e, a meno che l'annuncio non sia ricorrente, non riceve di nuovo il contenuto per l'annuncio migrato.  

 Alcuni oggetti richiedono altro oltre alla migrazione dei dati dalla gerarchia di origine nella gerarchia di destinazione. Ad esempio, per eseguire la migrazione degli aggiornamenti software dai client alla gerarchia di destinazione, nella gerarchia di destinazione è necessario distribuire un punto di aggiornamento software attivo, configurare il catalogo dei prodotto e sincronizzare il punto di aggiornamento software con Windows Server Update Services (WSUS).  

 Utilizzare le sezioni seguenti per pianificare i processi di migrazione.  

-   [Tipi di processi di migrazione](#Types_of_Migration)  

-   [Pianificazione generale di tutti i processi di migrazione](#About_Migration_Jobs)  

-   [Pianificazione di processi di migrazione raccolta](#About_Collection_Migration)  

-   [Pianificazione di processi di migrazione oggetto](#About_Object_Migration)  

-   [Pianificazione di processi di migrazione di oggetti migrati precedentemente](#About_Object_Migrations)  

##  <a name="a-nametypesofmigrationa-types-of-migration-jobs"></a><a name="Types_of_Migration"></a> Tipi di processi di migrazione  
 Configuration Manager supporta i tipi seguenti di processi di migrazione. Ogni tipo di processo è progettato per definire gli oggetti che è possibile includere nel processo:  

 **Migrazione raccolta** (supportata solo durante la migrazione da Configuration Manager 2007 SP2): esegue la migrazione di oggetti relativi alle raccolte selezionate. Per impostazione predefinita, la migrazione raccolta include tutti gli oggetti che sono associati ai membri della raccolta. Quando si utilizza un processo di migrazione raccolta, è possibile escludere le istanze specifiche di oggetti.  

 **Migrazione oggetto**: esegue la migrazione di singoli oggetti selezionati. Selezionare solo i dati da migrare.  

 **Migrazione di oggetti di cui è già stata eseguita la migrazione**: esegue la migrazione di oggetti precedentemente migrati, quando tali oggetti sono stati aggiornati nella gerarchia di origine dopo l'ultima migrazione.  

###  <a name="a-nameobjectsthatcanmigratea-objects-that-you-can-migrate"></a><a name="Objects_that_can_migrate"></a> Oggetti di cui è possibile eseguire la migrazione  
 Non tutti gli oggetti possono essere migrati da un tipo specifico di processo di migrazione. L'elenco seguente identifica il tipo di oggetti di cui è possibile eseguire la migrazione con ciascun tipo di processo di migrazione.  

> [!NOTE]  
>  I processi di migrazione raccolta sono disponibili solo quando si esegue la migrazione di oggetti da una gerarchia di origine di Configuration Manager 2007 SP2.  

 **Tipi di processo che è possibile usare per la migrazione di ogni oggetto:**  

-   **Annunci** (disponibili per la migrazione dai siti di origine di Configuration Manager 2007 supportati)  

    -   Migrazione raccolta  

-   **Catalogo di Asset Intelligence**  

    -   Migrazione oggetto  

    -   Migrazione di oggetti di cui è già stata eseguita la migrazione  

-   **Requisiti hardware di Asset Intelligence**  

    -   Migrazione oggetto  

    -   Migrazione di oggetti di cui è già stata eseguita la migrazione  

-   **Elenco di software di Asset Intelligence**  

    -   Migrazione oggetto  

    -   Migrazione di oggetti di cui è già stata eseguita la migrazione  

-   **Limiti**  

    -   Migrazione oggetto  

    -   Migrazione di oggetti di cui è già stata eseguita la migrazione  

-   **Configurazione di base**  

    -   Migrazione raccolta  

    -   Migrazione oggetto  

    -   Migrazione di oggetti di cui è già stata eseguita la migrazione  

-   **Elementi di configurazione**  

    -   Migrazione raccolta  

    -   Migrazione oggetto  

    -   Migrazione di oggetti di cui è già stata eseguita la migrazione  

-   **Finestre di manutenzione**  

    -   Migrazione raccolta  

-   **Immagini di avvio della distribuzione del sistema operativo**  

    -   Migrazione raccolta  

    -   Migrazione oggetto  

    -   Migrazione di oggetti di cui è già stata eseguita la migrazione  

-   **Pacchetti driver della distribuzione del sistema operativo**  

    -   Migrazione raccolta  

    -   Migrazione oggetto  

    -   Migrazione di oggetti di cui è già stata eseguita la migrazione  

-   **Driver di distribuzione del sistema operativo**  

    -   Migrazione raccolta  

    -   Migrazione oggetto  

    -   Migrazione di oggetti di cui è già stata eseguita la migrazione  

-   **Immagini di distribuzione del sistema operativo**  

    -   Migrazione raccolta  

    -   Migrazione oggetto  

    -   Migrazione di oggetti di cui è già stata eseguita la migrazione  

-   **Pacchetti di distribuzione del sistema operativo**  

    -   Migrazione raccolta  

    -   Migrazione oggetto  

    -   Migrazione di oggetti di cui è già stata eseguita la migrazione  

-   **Pacchetti di distribuzione software**  

    -   Migrazione raccolta  

    -   Migrazione oggetto  

    -   Migrazione di oggetti di cui è già stata eseguita la migrazione  

-   **Regole di controllo software**  

    -   Migrazione oggetto  

    -   Migrazione di oggetti di cui è già stata eseguita la migrazione  

-   **Pacchetti di distribuzione degli aggiornamenti software**  

    -   Migrazione raccolta  

    -   Migrazione oggetto  

    -   Migrazione di oggetti di cui è già stata eseguita la migrazione  

-   **Modelli di distribuzione degli aggiornamenti software**  

    -   Migrazione raccolta  

    -   Migrazione oggetto  

    -   Migrazione di oggetti di cui è già stata eseguita la migrazione  

-   **Distribuzioni di aggiornamenti software**  

    -   Migrazione raccolta  

-   **Elenchi di aggiornamenti software**  

    -   Migrazione oggetto  

    -   Migrazione di oggetti di cui è già stata eseguita la migrazione  

-   **Sequenze di attività**  

    -   Migrazione raccolta  

    -   Migrazione oggetto  

    -   Migrazione di oggetti di cui è già stata eseguita la migrazione  

-   **Pacchetti di applicazioni virtuali**  

    -   Migrazione raccolta  

    -   Migrazione oggetto  

    > [!IMPORTANT]  
    >  Sebbene sia possibile eseguire la migrazione di un pacchetto di applicazioni virtuali utilizzando la migrazione oggetto, non è possibile seguire la migrazione dei pacchetti utilizzando il tipo di processo di migrazione di **Migrazione di oggetti di cui è già stata eseguita la migrazione**. Al contrario, è necessario eliminare il pacchetto di applicazioni virtuali di cui è stata eseguita la migrazione dal sito di destinazione e quindi creare un nuovo processo di migrazione per eseguire la migrazione dell'applicazione virtuale.  

##  <a name="a-nameaboutmigrationjobsa-general-planning-for-all-migration-jobs"></a><a name="About_Migration_Jobs"></a>Pianificazione generale di tutti i processi di migrazione  
 Utilizzare la Creazione guidata del processo di migrazione per creare un processo di migrazione per la migrazione degli oggetti nella gerarchia di destinazione. Il tipo di processo di migrazione creato determina quali oggetti sono disponibili per la migrazione. È possibile creare e utilizzare più processi di migrazione per trasferire i dati dallo stesso sito di origine o da più siti di origine. L'utilizzo di un tipo di processo di migrazione non blocca l'utilizzo di un altro tipo di processo di migrazione.  

 Dopo che è stato eseguito il processo di migrazione, lo stato viene elencato come **Completato** e non può essere eseguito di nuovo. Tuttavia, è possibile creare un nuovo processo di migrazione per eseguire la migrazione degli oggetti che sono stati trasferiti dal processo originario. Il nuovo processo di migrazione può includere anche oggetti aggiuntivi. Quando si creano ulteriori processi di migrazione, gli oggetti che sono stati trasferiti precedentemente, visualizzeranno lo stato di **Migrato**. È possibile selezionare gli oggetti per eseguire di nuovo la migrazione. Tuttavia, a meno che l'oggetto sia stato aggiornato nella gerarchia di origine, non sarà necessario eseguire nuovamente la migrazione di questi oggetti. Se l'oggetto è stato aggiornato nella gerarchia di origine dopo la migrazione originaria, è possibile identificare l'oggetto quando si utilizza il tipo di processo di migrazione di **Oggetti modificati dopo la migrazione**.  

 È possibile eliminare un processo di migrazione prima dell'esecuzione. Dopo che un processo di migrazione è stato completato, rimane tuttavia visibile nella console di Configuration Manager e non può essere eliminato. Ogni processo di migrazione completato o non ancora eseguito rimane visibile nella console di Configuration Manager finché il processo di migrazione non viene completato e non viene eseguita la pulizia dei dati della migrazione.  

> [!NOTE]  
>  Dopo aver completato la migrazione utilizzando l'azione **Pulisci dati migrazione** , è possibile configurare di nuovo una gerarchia analoga alla gerarchia di origine corrente per ripristinare la visibilità agli oggetti di cui è stata precedentemente eseguita la migrazione.  

 È possibile visualizzare gli oggetti contenuti in ogni processo di migrazione nella console di Configuration Manager selezionando il processo di migrazione e facendo clic sulla scheda **Oggetti nel processo**.  

 Utilizzare le informazioni nelle sezioni riportate di seguito per pianificare tutti i processi di migrazione.  

### <a name="data-selection"></a>Selezione dei dati  
 Quando si crea un processo di migrazione raccolta, è necessario selezionare una o più raccolte. Dopo aver selezionato le raccolte, la Creazione guidata del processo di migrazione consente di visualizzare gli oggetti sono associati alle raccolte. Per impostazione predefinita, viene eseguita la migrazione degli oggetti associati alle raccolte selezionate, ma è possibile cancellare gli oggetti che non si desidera trasferire con quel processo. Quando si cancella un oggetto contenente oggetti dipendenti, anche gli oggetti dipendenti verranno cancellati. Tutti gli oggetti cancellati vengono aggiunti a un elenco di esclusione. Gli oggetti in un elenco di esclusione vengono rimossi dalla selezione automatica per i processi di migrazione futura. È necessario modificare manualmente l'elenco di esclusione per rimuovere gli oggetti che si desidera selezionare automaticamente per la migrazione nei processi di migrazione futura.  

### <a name="site-ownership-for-migrated-content"></a>Proprietà del sito per i contenuti migrati  
 Quando si esegue la migrazione dei contenuti per le distribuzioni, è necessario assegnare l'oggetto contenuto a un sito nella gerarchia di destinazione. Il sito diventa quindi il proprietario di tale contenuto nella gerarchia di destinazione. Benché il sito di livello superiore della gerarchia di destinazione sia il sito che esegue la migrazione dei metadati per il contenuto, è il sito assegnato che accede ai file di origine per il contenuto nella rete.  

 Per ridurre al minimo la larghezza di banda di rete utilizzata durante la migrazione, si consiglia di trasferire la proprietà del contenuto al sito disponibile più vicino. Poiché le informazioni sul contenuto vengono condivise globalmente in System Center Configuration Manager, saranno disponibili in ogni sito.  

 Benché le informazioni sul contenuto vengano condivise in tutti i siti nella gerarchia di destinazione utilizzando la replica di database, i contenuti assegnati a un sito primario e quindi distribuiti nei punti di distribuzione in altri siti primari, vengono trasferiti utilizzando la replica basata su file. Il trasferimento viene instradato attraverso il sito di amministrazione centrale e quindi a ciascun sito primario aggiuntivo. Centralizzando i pacchetti che si prevede di distribuire in più siti primari prima o durante la migrazione quando si assegna un sito come proprietario del contenuto, è possibile ridurre i trasferimenti di dati in reti a larghezza di banda ridotta.  

### <a name="configure-role-based-administration-security-scopes-for-migrated-data"></a>Configurare gli ambiti di protezione dell'amministrazione basata su ruoli per i dati di cui è stata eseguita la migrazione  
 Quando si esegue la migrazione dei dati in una gerarchia di destinazione, è necessario assegnare uno o più ambiti di protezione dell'amministrazione basata su ruoli agli oggetti di cui si esegue la migrazione dei dati. In questo modo solo gli utenti amministrativi appropriati hanno accesso ai dati dopo che viene eseguita la migrazione. Gli ambiti di protezione specificati vengono definiti dal processo di migrazione e vengono applicati a tutti gli oggetti migrati da quel processo. Se è necessario applicare ambiti di protezione diversi a set di oggetti diversi e si desidera assegnare gli ambiti durante la migrazione, è necessario eseguire la migrazione dei diversi set di oggetti utilizzando diversi processi di migrazione.  

 Prima di configurare un processo di migrazione, verificare il funzionamento dell'amministrazione basata su ruoli in System Center Configuration Manager e, se necessario, configurare uno o più ambiti di sicurezza per i dati di cui si esegue la migrazione per controllare gli utenti che avranno accesso agli oggetti migrati nella gerarchia di destinazione.  

 Per altre informazioni sugli ambiti di sicurezza e sull'amministrazione basata su ruoli, vedere  [Nozioni fondamentali sull'amministrazione basata sui ruoli per System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

### <a name="review-migration-actions"></a>Verificare le azioni di migrazione  
 Quando si configura un processo di migrazione, la Creazione guidata del processo di migrazione visualizza un elenco di azioni da eseguire per completare una migrazione in maniera corretta e un elenco di azioni che Configuration Manager esegue durante la migrazione dei dati selezionati. Leggere attentamente queste informazioni per verificare il risultato previsto.  

### <a name="scheduling-migration-jobs"></a>Pianificazione dei processi di migrazione  
 Per impostazione predefinita, un processo di migrazione viene eseguito subito dopo la sua creazione. Tuttavia, è possibile specificare quando il processo di migrazione viene eseguito quando si crea il processo o in un secondo momento modificando le proprietà del processo. È possibile pianificare l'esecuzione del processo di migrazione come riportato di seguito.  

-   Eseguire il processo ora  

-   Eseguire il processo a un'ora specifica  

-   Non eseguire il processo  

### <a name="specify-conflict-resolution-for-migrated-data"></a>Specificare la risoluzione conflitti per i dati di cui è stata eseguita la migrazione  
 Per impostazione predefinita, i processi di migrazione non sovrascrivono i dati nel database di destinazione, a meno che il processo di migrazione non sia configurato per ignorare o sovrascrivere i dati precedentemente migrati nel database di destinazione.  

##  <a name="a-nameaboutcollectionmigration-a-planning-for-collection-migration-jobs"></a><a name="About_Collection_Migration "></a> Pianificazione dei processi di migrazione raccolta  
 I processi di migrazione raccolta sono disponibili solo quando si esegue la migrazione di dati da una gerarchia di origine che esegue una versione supportata di Configuration Manager 2007. Quando si esegue la migrazione per raccolta, è necessario specificare una o più raccolte di cui eseguire la migrazione. Per ogni raccolta specificata, il processo di migrazione seleziona automaticamente tutti gli oggetti correlati per la migrazione. Ad esempio, se si seleziona una raccolta specifica di utenti, vengono identificati i membri della raccolta e sarà possibile eseguire la migrazione delle distribuzioni associate a tale raccolta. Facoltativamente, è possibile selezionare altri oggetti di distribuzione associati a tali membri per eseguirne la migrazione. Tutti questi elementi selezionati vengono aggiunti all'elenco di oggetti di cui può essere eseguita la migrazione.  

 Quando viene eseguita la migrazione di una raccolta, System Center Configuration Manager esegue anche la migrazione delle impostazioni della raccolta che includono finestre di manutenzione e variabili di raccolta, ma non può eseguire la migrazione delle impostazioni della raccolta per il provisioning del client AMT.  

 Utilizzare le informazioni nelle sezioni riportate di seguito per comprendere altre configurazioni che possono essere applicabili ai processi di migrazione basati sulle raccolte.  

### <a name="excluding-objects-from-collection-migration-jobs"></a>Esclusione di oggetti dai processi di migrazione raccolta  
 È possibile escludere oggetti specifici da un processo di migrazione raccolte. Quando si esclude un oggetto specifico da un processo di migrazione raccolte, tale oggetto viene aggiunto a un elenco di esclusione globale contenente tutti gli oggetti esclusi dai processi di migrazione creati per ogni sito di origine nella gerarchia di origine corrente. Gli oggetti inclusi nell'elenco di esclusione risultano ancora disponibili per la migrazione in processi futuri, ma non vengono inclusi automaticamente quando si crea un nuovo processo di migrazione basato su raccolte.  

 È possibile modificare l'elenco di esclusione per rimuovere gli oggetti esclusi in precedenza. Dopo la rimozione dall'elenco di esclusione, l'oggetto verrà selezionato automaticamente quando si specifica una raccolta associata durante la creazione di un nuovo processo di migrazione.  

### <a name="unsupported-collections"></a>Raccolte non supportate  
 Configuration Manager può eseguire la migrazione di qualsiasi raccolta utente predefinita, di qualsiasi raccolta dispositivi e della maggior parte delle raccolte personalizzate da una gerarchia di origine di Configuration Manager 2007. Configuration Manager non può eseguire la migrazione di raccolte che contengono utenti e dispositivi nella stessa raccolta.  

 Non è possibile eseguire la migrazione delle raccolte seguenti:  

-   Raccolta contenente utenti e dispositivi.  

-   Raccolta contenente un riferimento a una raccolta con tipo di risorse diverso. Ad esempio, una raccolta basata su dispositivi che include una sottoraccolta o un collegamento a una raccolta basata su utenti. In questo esempio viene eseguita la migrazione solo della raccolta di livello superiore.  

-   Raccolta contenente una regola per l'inclusione di computer sconosciuti. Viene eseguita la migrazione della raccolta, ma non della regola per l'inclusione di computer sconosciuti.  

### <a name="empty-collections"></a>Raccolte vuote  
 Una raccolta vuota è una raccolta a cui non è associata alcuna risorsa. Quando Configuration Manager esegue la migrazione di una raccolta vuota, converte la raccolta in una cartella organizzativa che non contiene utenti o dispositivi. Tale cartella viene creata usando il nome della raccolta vuota nel nodo **Raccolte utenti** o **Raccolte dispositivi** dell'area di lavoro **Asset e conformità** della console di Configuration Manager.  

### <a name="linked-collections-and-subcollections"></a>Raccolte e sottoraccolte collegate  
 Quando si esegue la migrazione di raccolte collegate ad altre raccolte o che includono sottoraccolte, Configuration Manager crea una cartella nel nodo **Raccolte utenti** o **Raccolte dispositivi** in aggiunta alle raccolte e sottoraccolte collegate.  

### <a name="collection-dependencies-and-include-objects"></a>Dipendenze della raccolta e inclusione di oggetti  
 Quando si specifica una raccolta di cui eseguire la migrazione nella Creazione guidata del processo di migrazione, eventuali raccolte dipendenti verranno selezionate automaticamente per l'inclusione nel processo. Questo comportamento assicura che tutte le risorse necessarie siano disponibili dopo la migrazione.  

 Ad esempio: si seleziona una raccolta per dispositivi che eseguono Windows 7 e denominata **Win_7**. Questa raccolta è limitata a una raccolta contenente tutti i sistemi operativi client e denominata **All_Clients**. La raccolta **All_Clients** verrà selezionata automaticamente per la migrazione.  

### <a name="collection-limiting"></a>Limitazione della raccolta  
 Con System Center Configuration Manager, le raccolte sono dati globali e vengono valutate in ogni sito nella gerarchia. Pianificare quindi come limitare l'ambito di una raccolta dopo la migrazione. Durante la migrazione è possibile identificare una raccolta della gerarchia di destinazione da utilizzare per limitare l'ambito della raccolta di cui si esegue la migrazione, in modo che la raccolta di cui è stata eseguita la migrazione non includa membri imprevisti.  

 Ad esempio, in Configuration Manager 2007 le raccolte vengono valutate nel sito in cui vengono create e nei siti figlio. È possibile distribuire un annuncio solo nel sito figlio, in modo da limitare l'ambito di tale annuncio a tale sito figlio. Con System Center Configuration Manager, invece, le raccolte e gli annunci associati vengono valutati in ogni sito. La limitazione della raccolta consente di specificare i membri della raccolta in base a un'altra raccolta, in modo da evitare l'aggiunta di membri di raccolta imprevisti.  

### <a name="site-code-replacement"></a>Sostituzione del codice del sito  
 Quando si esegue la migrazione di una raccolta contenente criteri che identificano un sito di Configuration Manager 2007, è necessario definire un sito specifico nella gerarchia di destinazione. Ciò assicura il funzionamento corretto della raccolta di cui è stata eseguita la migrazione nella gerarchia di destinazione, senza incrementi dell'ambito.  

### <a name="specify-behavior-for-migrated-advertisements"></a>Specificare il comportamento di annunci di cui è stata eseguita la migrazione  
 Per impostazione predefinita, i processi di migrazione basati su raccolte disabilitano gli annunci di cui viene eseguita la migrazione nella gerarchia di destinazione. Sono inclusi tutti i programmi associati all'annuncio. Quando si crea un processo di migrazione basato su raccolte contenente annunci, viene visualizzata l'opzione **Abilitare i programmi per la distribuzione nella gerarchia di destinazione dopo la migrazione di un annuncio da una gerarchia di origine** nella pagina **Impostazioni** della Creazione guidata del processo di migrazione. Se si seleziona questa opzione, i programmi associati agli annunci verranno abilitati dopo la migrazione. È consigliabile non selezionare questa opzione e abilitare invece i programmi dopo la migrazione, quando sarà possibile verificare i client che li riceveranno.  

> [!NOTE]  
>  L'opzione **Abilitare i programmi per la distribuzione nella gerarchia di destinazione dopo la migrazione di un annuncio da una gerarchia di origine** viene visualizzata solo quando si crea un processo di migrazione basato su raccolte e se il processo di migrazione contiene annunci.  

 Per abilitare un programma dopo la migrazione, deselezionare l'opzione **Disattiva il programma nei computer in cui è distribuito** nella scheda **Avanzate** delle proprietà del programma.  

##  <a name="a-nameaboutobjectmigrationa-planning-for-object-migration-jobs"></a><a name="About_Object_Migration"></a> Pianificazione dei processi di migrazione di oggetti  
 A differenza di migrazione di raccolte, è necessario selezionare ogni oggetto e l'istanza dell'oggetto di cui si desidera eseguire la migrazione. È possibile selezionare i singoli oggetti, ad esempio annunci da una gerarchia di Configuration Manager 2007 o una pubblicazione da una gerarchia di System Center 2012 Configuration Manager o System Center Configuration Manager, da aggiungere all'elenco di oggetti di cui eseguire la migrazione per un determinato processo di migrazione. Il processo di migrazione oggetti non eseguirà la migrazione nel sito di destinazione di eventuali oggetti non aggiungi all'elenco di migrazione.  

 I processi di migrazione basati su oggetti non richiedono configurazione aggiuntiva rispetto alle configurazione applicabili a tutti i processi di migrazione.  

##  <a name="a-nameaboutobjectmigrationsa-planning-for-previously-migrated-object-migration-jobs"></a><a name="About_Object_Migrations"></a> Pianificazione di processi di migrazione di oggetti migrati precedentemente  
 Quando un oggetto di cui è già stata eseguita la migrazione nella gerarchia di destinazione viene aggiornato nella gerarchia di origine, sarà possibile eseguire di nuovo la migrazione di tale oggetto utilizzando il tipo di processo **Oggetti modificati dopo la migrazione** . Ad esempio, quando si rinominano o si aggiornano i file di origine per un pacchetto nella gerarchia di origine, la versione del pacchetto viene incrementata nella gerarchia di origine. Dopo gli incrementi di versione del pacchetto, il pacchetto può essere identificato per la migrazione da questo tipo di processo.  

 Questo tipo di processo è analogo al tipo di migrazione oggetti, ma quando si selezionano gli oggetti di cui eseguire la migrazione è possibile selezionare solo gli oggetti aggiornati dopo la migrazione da parte di un processo di migrazione precedente.  

 Quando si seleziona questo tipo di processo, il comportamento di risoluzione dei conflitti nella pagina **Impostazioni** della Creazione guidata del processo di migrazione viene configurato in modo da sovrascrivere oggetti di cui è stata eseguita in precedenza la migrazione e non sarà possibile modificare questa impostazione.  

> [!NOTE]  
>  Questo processo di migrazione consente di identificare gli oggetti che vengono aggiornati automaticamente dalla gerarchia di origine e gli oggetti aggiornati da un utente amministrativo.  



<!--HONumber=Nov16_HO1-->


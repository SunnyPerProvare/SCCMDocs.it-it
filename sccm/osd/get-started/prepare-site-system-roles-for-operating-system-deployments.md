---
title: Preparare i ruoli del sistema del sito per le distribuzioni del sistema operativo | Microsoft Docs
description: Prima di distribuire sistemi operativi in System Center Configuration Manager, configurare i ruoli di sistema del sito.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
caps.latest.revision: 11
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 761c3f58f7c57d8f87ee802da37821895062546d
ms.openlocfilehash: 11c0f169afebdb071fefb5ce300fd1ae3481a94f
ms.lasthandoff: 04/19/2017


---
# <a name="prepare-site-system-roles-for-operating-system-deployments-with-system-center-configuration-manager"></a>Preparare i ruoli del sistema del sito per le distribuzioni del sistema operativo con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Per distribuire i sistemi operativi in System Center Configuration Manager, è necessario preparare i ruoli di sistema del sito seguenti che richiedono considerazioni e configurazioni specifiche.

##  <a name="BKMK_DistributionPoints"></a> Punti di distribuzione  
 Il ruolo del sistema del sito del punto di distribuzione contiene i file di origine che devono essere scaricati dai client, ad esempio il contenuto dell'applicazione, gli aggiornamenti software, le immagini del sistema operativo e le immagini di avvio. È possibile controllare la distribuzione del contenuto usando le opzioni della larghezza di banda, della limitazione e della pianificazione.  

 È importante avere sufficienti punti di distribuzione per supportare la distribuzione dei sistemi operativi nei computer. È anche importante pianificare la posizione di questi punti di distribuzione nella gerarchia. La maggior parte delle informazioni sulla pianificazione si trova in [Gestire il contenuto e l'infrastruttura del contenuto](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md). Tuttavia, esistono altre considerazioni sulla pianificazione dei punti di distribuzione specifiche per la distribuzione del sistema operativo.  

###  <a name="BKMK_AdditionalPlanning"></a> Considerazioni aggiuntive sulla pianificazione per i punti di distribuzione  
 Di seguito sono descritti altri aspetti della pianificazione da considerare per i punti di distribuzione:  

-   **Come si possono evitare distribuzioni indesiderate del sistema operativo?**  

     Configuration Manager non distingue i server del sito dagli altri computer di destinazione in una raccolta. Se si distribuisce una sequenza di attività richiesta in una raccolta che contiene un server del sito, questo esegue la sequenza di attività esattamente come qualsiasi altro computer presente nella raccolta. Verificare che la distribuzione del sistema operativo usi una raccolta contenente i client di cui eseguire la distribuzione.  

     È possibile gestire il comportamento relativo alle distribuzioni di sequenze di attività ad alto rischio. Una distribuzione ad alto rischio viene installata automaticamente in un client e può causare risultati imprevisti. È il caso, ad esempio, di una sequenza di attività con scopo impostato su Obbligatorio che distribuisce un sistema operativo. Per ridurre il rischio di una distribuzione ad alto rischio indesiderata, è possibile configurare le impostazioni di verifica della distribuzione. Per altre informazioni, vedere [Impostazioni per gestire distribuzioni ad alto rischio](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

-   **Quanti computer possono ricevere simultaneamente un'immagine del sistema operativo da un singolo punto di distribuzione?**  

     Per stimare il numero di punti di distribuzione necessario, prendere in considerazione la velocità di elaborazione e le operazioni di input/output su disco del punto di distribuzione, la larghezza di banda disponibile nella rete e l'effetto delle dimensioni del pacchetto di immagini su queste risorse. Ad esempio, in una rete Ethernet da 100 megabyte (MB) il numero massimo di computer che possono elaborare un pacchetto di immagini da 4 gigabyte (GB) in un'ora è 11, se non si considerano altri fattori relativi alle risorse server.  

     `100 Megabits/sec = 12.5 Megabytes/sec = 750 Megabytes/min = 45 Gigabytes/hour = 11 images @ 4GB per image.`  

     Se è necessario eseguire la distribuzione di un sistema operativo in un numero specifico di computer in un determinato intervallo di tempo, distribuire l'immagine in un numero appropriato di punti di distribuzione.  

-   **È possibile distribuire un sistema operativo in un punto di distribuzione?**  

     È possibile distribuire un sistema operativo in un punto di distribuzione, ma l'immagine del sistema operativo deve essere ricevuta da un punto di distribuzione diverso.  

###  <a name="BKMK_PXEDistributionPoint"></a> Configurazione dei punti di distribuzione per accettare le richieste PXE  
 Per distribuire i sistemi operativi ai client di Configuration Manager che eseguono richieste di avvio PXE, è necessario configurare uno o più punti di distribuzioni per accettare le richieste PXE. Una volta configurato, il punto di distribuzione risponderà alla richiesta di avvio PXE e stabilirà l'azione appropriata da eseguire per la distribuzione.

> [!IMPORTANT]  
>  [Windows Deployment Services](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDS) deve essere installato in tutti i punti di distribuzione abilitati per PXE.  

 Utilizzare la seguente procedura per modificare un punto di distribuzione esistente in modo che possa accettare le richieste PXE. Per informazioni su come installare un nuovo punto di distribuzione, vedere [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).  

#### <a name="to-modify-an-existing-distribution-point-to-accept-pxe-requests"></a>Per modificare un punto di distribuzione esistente per accettare le richieste PXE  

1.  Nella console di Configuration Manager, fare clic su **Amministrazione**, espandere **Panoramica** e fare clic su **Punti di distribuzione**.  

2.  Selezionare il punto di distribuzione da configurare, quindi nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

3.  Nella pagina delle proprietà per il punto di distribuzione fare clic sulla scheda **PXE** . e selezionare **Abilita supporto PXE per i client** per abilitare PXE nel punto di distribuzione.  

4.  Fare clic su **Sì** nella finestra di dialogo **Controllare le porte richieste per PXE** per confermare che si vuole abilitare PXE. Configuration Manager configura automaticamente le porte predefinite in un firewall di Windows. Se si usa un altro firewall, è necessario configurare manualmente le porte.  

    > [!NOTE]  
    >  Se WDS e DHCP sono installati nello stesso server, è necessario configurare WDS per l'ascolto su una porta diversa, perché DHCP è in ascolto sulla stessa porta. Per altre informazioni, vedere [Considerazioni in presenza di Servizi di distribuzione Windows e DHCP nello stesso server](../plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDSandDHCP).  

5.  Selezionare **Consenti a questo punto di distribuzione di rispondere alle richieste PXE in ingresso** per abilitare WDS in modo che risponda alle richieste di servizio PXE in ingresso. È possibile usare questa impostazione per attivare e disattivare il servizio senza rimuovere la funzionalità PXE dal punto di distribuzione.  

6.  Per distribuire sistemi operativi a computer non gestiti da Configuration Manager, selezionare **Abilita supporto per computer sconosciuti**.  

7.  Selezionare **Richiedi password quando i computer usano PXE**e specificare una password complessa per offrire maggiore sicurezza per le distribuzioni PXE.  

8.  In the **Affinità utente dispositivo** scegliere la modalità di associazione del punto di distribuzione tra utenti e computer di destinazione per le distribuzioni PXE.  

    -   Selezionare **Non utilizzare l'affinità dispositivo utente** per non associare gli utenti al computer di destinazione.  

    -   Selezionare **Consenti affinità dispositivo utente con approvazione manuale** per attendere l'approvazione da un utente amministratore prima di associare gli utenti al computer di destinazione.  

    -   Selezionare **Consenti affinità dispositivo utente con approvazione automatica** per associare automaticamente gli utenti al computer di destinazione senza attendere l'approvazione.  

     Per altre informazioni, vedere [Associare gli utenti a un computer di destinazione](../get-started/associate-users-with-a-destination-computer.md).  

9. specificare se il punto di distribuzione risponde alle richieste PXE da tutte le interfacce di rete o da interfacce di rete specifiche. Se si sceglie di fare in modo che il punto di distribuzione risponda a un'interfaccia di rete specifica, specificare l'indirizzo MAC per ogni interfaccia di rete.  

10. Specificare, in secondi, il tempo di attesa del punto di distribuzione prima che risponda alle richieste dei computer quando vengono utilizzati più punti di distribuzione che supportano PXE.  

11. Fare clic su **OK** per aggiornare le proprietà del punto di distribuzione.  

###  <a name="BKMK_RamDiskTFTP"></a> Personalizzare le dimensioni della finestra e del blocco TFTP RamDisk nei punti di distribuzione abilitati per PXE  
È possibile personalizzare le dimensioni del blocco TFTP RamDisk e, a partire da Configuration Manager versione 1606, le dimensioni della finestra per i punti di distribuzione abilitati per PXE. Se la rete è stata personalizzata, il download dell'immagine di avvio potrebbe non riuscire a causa di un errore di timeout perché le dimensioni del blocco o della finestra sono troppo grandi. La personalizzazione delle dimensioni della finestra e del blocco TFTP RamDisk consentono di ottimizzare il traffico TFTP quando si usa PXE per soddisfare requisiti di rete specifici.   
È necessario testare le impostazioni personalizzate nel proprio ambiente per stabilire quale sia la scelta più efficiente.  

-   **Dimensioni blocco TFTP**: le dimensioni del blocco corrispondono alle dimensioni dei pacchetti di dati che vengono inviati dal server al client che sta scaricando il file (come descritto in RFC 2347). Dimensioni maggiori del blocco consentono al server di inviare meno pacchetti e di conseguenza si verificano meno ritardi per il round trip tra il server e client. Dimensioni del blocco grandi, tuttavia, comportano la creazione di pacchetti frammentati, che non sono supportati dalla maggior parte delle implementazioni di client PXE.  

-   **Dimensioni finestra TFTP**: TFTP richiede un pacchetto di acknowledgment (ACK) per ogni blocco di dati inviato. Il server non invia il blocco successivo nella sequenza finché non riceve il pacchetto ACK per il blocco precedente. L'uso di finestre TFTP è una funzionalità di Servizi di distribuzione Windows che consente di definire quanti blocchi di dati sono necessari per riempire una finestra. Il server invia i blocchi di dati back-to-back fino a riempire la finestra e quindi il client invia un pacchetto ACK. Aumentando le dimensioni di questa finestra si riduce il numero di ritardi di round trip tra il client e il server, nonché il tempo complessivo necessario per scaricare un'immagine di avvio.  


#### <a name="to-modify-the-ramdisk-tftp-window-size"></a>Per modificare le dimensioni della finestra TFTP RamDisk  

-   Aggiungere la chiave del Registro di sistema seguente nei punti di distribuzione abilitati per PXE per personalizzare le dimensioni della finestra TFTP RamDisk:  

     **Percorso**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Nome: RamDiskTFTPWindowSize  

     **Tipo**: REG_DWORD  

     **Valore**: &lt;dimensioni finestra personalizzate>  

 Il valore predefinito è 1 (1 blocco di dati riempie la finestra)  

#### <a name="to-modify-the-ramdisk-tftp-block-size"></a>Per modificare le dimensioni del blocco TFTP RamDisk  

-   Aggiungere la chiave del Registro di sistema seguente nei punti di distribuzione abilitati per PXE per personalizzare le dimensioni della finestra TFTP RamDisk:  

     **Percorso**: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP  
    Nome: RamDiskTFTPBlockSize  

     **Tipo**: REG_DWORD  

     **Valore**: &lt;dimensioni blocco personalizzate>  

 Il valore predefinito è 4096 (4k).  


###  <a name="BKMK_DPMulticast"></a> Configurare i punti di distribuzione per il supporto del multicast  
 Il multicast è un metodo di ottimizzazione della rete che è possibile usare nei punti di distribuzione in cui è probabile che più client scarichino contemporaneamente la stessa immagine del sistema. Quando si usa il multicast, l'immagine del sistema operativo viene scaricata contemporaneamente da più computer mentre il punto di distribuzione ne esegue il multicast, invece di far inviare una copia dei dati dal punto di distribuzione a ogni client in una connessione separata. Per supportare il multicast, è necessario configurare almeno un punto di distribuzione. Per altre informazioni, vedere [Usare multicast per distribuire Windows in rete](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

 Prima di distribuire il sistema operativo, è necessario configurare un punto di distribuzione per il supporto di multicast. Utilizzare la seguente procedura per modificare un punto di distribuzione esistente per il supporto di multicast. Per informazioni su come installare un nuovo punto di distribuzione, vedere [Installare e modificare un punto di distribuzione](../../core/servers/deploy/configure/install-and-configure-distribution-points.md).

#### <a name="to-enable-multicast-for-a-distribution-point"></a>Per attivare multicast per un punto di distribuzione  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Panoramica**, quindi selezionare il nodo **Punti di distribuzione** .  

3.  Selezionare il punto di distribuzione che si desidera utilizzare per il multicast dell'immagine del sistema operativo.  

4.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

5.  Selezionare la scheda **Multicast** , quindi configurare le seguenti opzioni:  

    -   **Abilita multicast**: è necessario selezionare questa opzione per abilitare il supporto del multicast nel punto di distribuzione.  

    -   **Account di connessione multicast**: specificare un account per connettersi al database del sito.  

    -   **Impostazioni indirizzo multicast**: specificare gli indirizzi IP usati per l'invio dei dati ai computer di destinazione. Per impostazione predefinita, l'indirizzo IP viene ottenuto da un server DHCP abilitato per la distribuzione di indirizzi multicast. A seconda dell'ambiente di rete, è possibile specificare un intervallo di indirizzi IP compreso tra 239.0.0.0 e 239.255.255.255.  

        > [!IMPORTANT]  
        >  Questi indirizzi IP devono essere accessibili ai computer di destinazione che richiedono l'immagine del sistema operativo. Di conseguenza è necessario configurare i router e i firewall tra il computer di destinazione e il server del sito per consentire il traffico multicast.  

    -   **Intervallo porte UDP**: Specificare l'intervallo di porte UDP per l'invio dei dati ai computer di destinazione.  

        > [!IMPORTANT]  
        >  Queste porte devono essere accessibili ai computer di destinazione che richiedono l'immagine del sistema operativo. Di conseguenza è necessario configurare i router e i firewall tra il computer di destinazione e il server del sito per consentire il traffico multicast.  

    -   **Abilita multicast pianificato**: specificare come Configuration Manager esegue i controlli per avviare la distribuzione dei sistemi operativi ai computer di destinazione. Fare clic su **Abilita multicast pianificato**, quindi selezionare le seguenti opzioni.  

         Nella casella **Ritardo avvio sessione** specificare i minuti di attesa prima che Configuration Manager risponda alla prima richiesta di distribuzione.  

         Nella casella **Dimensione minima sessione** specificare la quantità di richieste che Configuration Manager deve ricevere prima di avviare la distribuzione del sistema operativo.  

    -   **Velocità di trasferimento**: Selezionare la velocità di trasferimento per il download dei dati nei computer di destinazione.  

    -   **Numero massimo di client**: specificare il numero massimo di computer di destinazione per cui è possibile scaricare il sistema operativo da questo punto di distribuzione.  

6.  Fare clic su **OK**.  

##  <a name="BKMK_StateMigrationPoints"></a> Punto di migrazione stato  
 Il punto di migrazione stato archivia i dati sullo stato dell'utente acquisiti in un computer e quindi ripristinati in un altro computer. Tuttavia, quando si acquisiscono le impostazioni utente per una distribuzione del sistema operativo nello stesso computer, ad esempio una distribuzione in cui il sistema operativo viene aggiornato nel computer di destinazione, è possibile scegliere se archiviare i dati nello stesso computer con collegamenti reali oppure usare un punto di migrazione stato. Per alcune distribuzioni ai computer, quando viene creata l'archiviazione stati, Configuration Manager crea automaticamente un'associazione tra l'archiviazione stati e il computer di destinazione. Durante la pianificazione del punto di migrazione stato tenere presenti i seguenti fattori.  

### <a name="user-state-size"></a>Dimensioni stato utente  
 Le dimensioni dello stato utente influiscono direttamente sull'archiviazione su disco nel punto di migrazione stato e sulle prestazioni di rete durante la migrazione. Tenere presenti le dimensioni dello stato utente e il numero di computer di cui verrà eseguita la migrazione. Tenere presenti anche le impostazioni di cui eseguire la migrazione dal computer. Ad esempio, se nel server è già presente il backup di **Documenti** , potrebbe non essere necessario eseguirne la migrazione nell'ambito della distribuzione dell'immagine. Evitando migrazioni superflue è possibile ridurre le dimensioni generali dello stato utente e diminuire gli effetti sulle prestazioni di rete e sull'archiviazione su disco nel punto di migrazione stato.  

### <a name="user-state-migration-tool"></a>Utilità di migrazione stato utente  
 Per acquisire e ripristinare lo stato utente durante la distribuzione dei sistemi operativi, è necessario utilizzare un pacchetto per Utilità di migrazione stato utente (USMT) che punti ai file di origine USMT. Configuration Manager crea automaticamente questo pacchetto nella console di Configuration Manager in **Raccolta software** > **Gestione applicazioni** > **Pacchetti**. Configuration Manager usa USMT 10.0, che viene distribuito in Windows Assessment and Deployment Kit (Windows ADK), per acquisire lo stato utente da un sistema operativo e ripristinarlo in un altro sistema operativo.  

 Per una descrizione dei diversi scenari di migrazione per USMT 10.0, vedere [Scenari di migrazione comuni](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx).  

### <a name="retention-policy"></a>Criteri di conservazione  
 Quando si configura il punto di migrazione stato è possibile specificare l'intervallo di tempo per cui conservare i dati sullo stato utente archiviati al suo interno. L'intervallo di tempo per cui conservare i dati nel punto di migrazione stato dipende da due considerazioni:  

-   L'effetto dei dati archiviati sull'archiviazione su disco.  

-   La possibilità di conservare i dati per un determinato periodo nel caso in cui sia necessario eseguire un'ulteriore migrazione dei dati.  

 La migrazione dello stato avviene in due fasi: acquisizione e ripristino dei dati. Quando si acquisiscono dati, i dati sullo stato utente vengono raccolti e salvati nel punto di migrazione stato. Quando si ripristinano i dati, i dati sullo stato utente vengono recuperati dal punto di migrazione stato e scritti nel computer di destinazione. Quindi, il passaggio della sequenza attività **Rilascia archiviazione stati** rilascia i dati archiviati. Quando i dati vengono rilasciati, viene avviato il timer di conservazione. Se si seleziona l'opzione per eliminare immediatamente i dati migrati, i dati sullo stato utente vengono eliminati non appena vengono rilasciati. Se si seleziona l'opzione per conservare i dati per un determinato periodo di tempo, i dati vengono eliminati dopo il rilascio dei dati sullo stato, al termine dell'intervallo di tempo stabilito. Più è lungo il periodo di conservazione impostato, più spazio su disco potrebbe essere necessario.  

### <a name="select-drive-to-store-user-state-migration-data"></a>Selezionare l'unità in cui archiviare i dati di migrazione sullo stato utente  
 Quando si configura il punto di migrazione stato, è necessario specificare l'unità sul server in cui archiviare i dati sulla migrazione dello stato utente. È possibile selezionare un'unità da un elenco non modificabile di unità. Tuttavia, alcune unità potrebbero rappresentare unità non accessibili in scrittura, ad esempio l'unità CD o un'unità di condivisione non di rete. Inoltre, alcune lettere di unità potrebbero non essere mappate su un'unità del computer. Quando si configura il punto di migrazione stato, è necessario specificare un'unità condivisa e scrivibile.  

### <a name="configure-a-state-migration-point"></a>Configurare un punto di migrazione stato  
 Per configurare un punto di migrazione stato per archiviare i dati dello stato utente, è possibile utilizzare i metodi seguenti:  

-   Utilizzare la **Creazione guidata server del sistema sito** per creare un nuovo server di sistema del sito per il punto di migrazione stato.  

-   Utilizzare l' **Aggiunta guidata ruoli del sistema del sito** per aggiungere un punto di migrazione stato a un server esistente.  

 Quando si utilizzano queste procedure guidate, viene richiesto di fornire le informazioni seguenti per il punto di migrazione stato:  

-   Cartelle in cui archiviare i dati dello stato utente.  

-   Numero massimo di client che possono archiviare i dati nel punto di migrazione stato.  

-   Spazio minimo disponibile per il punto di migrazione stato in cui archiviare i dati sullo stato utente.  

-   Criteri di eliminazione per il ruolo. È possibile specificare che i dati dello stato utente vengano eliminati immediatamente dopo il ripristino in un computer o dopo un numero specifico di giorni dopo il ripristino dei dati utente in un computer.  

-   Se il punto di migrazione stato deve rispondere solo alle richieste di ripristino dei dati dello stato utente. Quando si abilita questa opzione, non è possibile utilizzare il punto di migrazione stato per archiviare dati dello stato utente.  

 Per i passaggi relativi all'installazione di un ruolo di sistema del sito, vedere [Aggiungere ruoli di sistema del sito](../../core/servers/deploy/configure/add-site-system-roles.md).  


---
title: Sicurezza e privacy per la distribuzione del sistema operativo
titleSuffix: Configuration Manager
description: Informazioni sulle procedure consigliate per sicurezza e privacy per la distribuzione del sistema operativo in System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4ec1457fafabe2e40106ec76310d9ff64b2aa267
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="security-and-privacy-for-operating-system-deployment-in-system-center-configuration-manager"></a>Sicurezza e privacy per la distribuzione del sistema operativo in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In questo argomento vengono illustrate le informazioni sulla sicurezza e la privacy per la distribuzione del sistema operativo in System Center Configuration Manager.  

##  <a name="BKMK_Security_HardwareInventory"></a> Procedure di sicurezza consigliate per la distribuzione del sistema operativo  
 Usare le seguenti procedure di sicurezza consigliate quando si distribuiscono sistemi operativi con Configuration Manager:  

-   **Implementare i controlli di accesso per proteggere il supporto di avvio**  

     Quando si crea un supporto di avvio, assegnare sempre una password per proteggere il supporto. Tuttavia, anche con una password, vengono crittografati solo i file che contengono informazioni sensibili e tutti i file possono essere sovrascritti.  

     Controllare l'accesso fisico ai supporti per evitare che un utente malintenzionato utilizzi gli attacchi crittografici per ottenere il certificato di autenticazione client.  

     Per evitare che un client installi criteri contenuto o clienti manomessi, viene eseguito l'hashing del contenuto e il contenuto deve essere usato con i criteri originali.  Se l'hash contenuto o il controllo che il contenuto soddisfi i criteri hanno esito negativo, il client non utilizzerà il supporto di avvio. Viene effettuato solo l'hashing del contenuto, ma non dei criteri, che vengono crittografati e protetti quando si specifica una password, cosa che rende più difficile la possibilità di un attacco per la modifica dei criteri.  

-   **Usare una posizione protetta quando si crea il supporto per le immagini del sistema operativo**  

     Se degli utenti non autorizzati hanno accesso alla posizione, possono manomettere i file creati o anche utilizzare tutto lo spazio disponibile su disco in modo che la creazione del supporto non riesca.  

-   **Proteggere i file del certificato (PFX) con una password complessa e se si memorizzano in rete, proteggere il canale della rete quando vengono importati in Configuration Manager**  

     Quando si richiede una password per importare il certificato di autenticazione client che si utilizza per il supporto di avvio, il certificato viene protetto da potenziali attacchi.  

     Utilizzare la firma SMB o IPsec tra il percorso di rete e il server del sito per impedire all'autore di un attacco di manomettere il file di certificato.  

-   **Se il certificato client viene compromesso, bloccare il certificato da Configuration Manager e revocarlo se si tratta di un certificato PKI**  

     Per distribuire un sistema operativo utilizzando il supporto di avvio e l'avvio PXE, è necessario disporre di un certificato di autenticazione client con una chiave privata. Se tale certificato è compromesso, bloccarlo nel nodo **Certificati** dell'area di lavoro **Amministrazione** , nodo **Sicurezza** .  

-   **Quando il provider SMS è in un computer o più computer diversi dal server del sito, proteggere il canale di comunicazione per proteggere le immagini di avvio**  

     Quando le immagini di avvio vengono modificate e il provider SMS è in esecuzione su un server che non è il server del sito, le immagini di avvio sono vulnerabili agli attacchi. Proteggere il canale di rete tra questi computer utilizzando la firma SMB o IPsec.  

-   **Abilitare i punti di distribuzione per la comunicazione client PXE solo su segmenti di rete protetta**  

     Quando un client invia una richiesta di avvio PXE, è necessario assicurarsi che la richiesta sia presa in carico da un punto di distribuzione valido che supporta PXE. Questo scenario include i rischi di protezione seguenti:  

    -   Un punto di distribuzione non autorizzato che risponde alle richieste PXE potrebbe fornire ai client un'immagine manomessa.  

    -   Un utente malintenzionato potrebbe lanciare un attacco man-in-the-middle contro il protocollo TFTP utilizzato da PXE e inviare codice dannoso con i file del sistema operativo oppure potrebbe creare un client non autorizzato per effettuare richieste TFTP direttamente al punto di distribuzione.  

    -   Un utente malintenzionato potrebbe utilizzare un client dannoso per avviare un attacco Denial of Service contro il punto di distribuzione.  

     Utilizzare una difesa in profondità per proteggere i segmenti di rete in cui i client avranno accesso ai punti di distribuzione per le richieste PXE.  

    > [!WARNING]  
    >  In ragioni di tali rischi di sicurezza, non abilitare un punto di distribuzione per la comunicazione PXE quando si trova in una rete non affidabile, come una rete perimetrale.  

-   **Configurare i punti di distribuzione che supportano PXE per rispondere alle richieste PXE solo su interfacce di rete specificate**  

     Se si consente al punto di distribuzione di rispondere a richieste PXE su tutte le interfacce di rete, questa configurazione potrebbe esporre il servizio PXE a reti non affidabili.  

-   **Richiedere una password per l'avvio PXE**  

     Quando si richiede una password per l'avvio PXE, questa configurazione aggiunge un livello aggiuntivo di protezione al processo di avvio PXE, per evitare che client dannosi raggiungano la gerarchia di Configuration Manager.  

-   **Non includere applicazioni line-of-business o software che contiene dati sensibili in un'immagine che verrà usata per l'avvio PXE o il multicast**  

     Per i rischi di protezione inerenti coinvolti con l'avvio PXE e il multicast, ridurre i rischi se il computer non autorizzato scarica l'immagine del sistema operativo.  

-   **Non includere applicazioni line-of-business o software che contiene dati sensibili nei pacchetti software installati usando variabili di sequenze attività**  

     Quando si distribuiscono pacchetti software utilizzando variabili di sequenze attività, il software potrebbe essere installato su computer e in utenti che non sono autorizzati a ricevere tale software.  

-   **Quando si esegue la migrazione dello stato utente, proteggere il canale di rete tra il client e il punto di migrazione dello stato usando la firma SMB o IPsec**  

     Dopo la connessione iniziale in HTTP, i dati della migrazione dello stato utente vengono trasferiti tramite SMB.  Se non si protegge il canale di rete, un utente malintenzionato può leggere e modificare questi dati.  

-   **Usare la versione più recente dell'utilità di migrazione stato utente (USMT) supportata da Configuration Manager**  

     La versione più recente dell'USMT fornisce miglioramenti della protezione e un controllo maggiore durante la migrazione dei dati dello stato utente.  

-   **Eliminare manualmente le cartelle nel punto di migrazione dello stato quando vengono rimosse**  

     Quando si rimuove una cartella del punto di migrazione dello stato dalle proprietà del punto di migrazione dello stato nella console di Configuration Manager, la cartella fisica non viene eliminata. Per proteggere i dati della migrazione dello stato utente dalla divulgazione di informazioni, è necessario rimuovere la condivisione di rete manualmente ed eliminare la cartella.  

-   **Non configurare il criterio di eliminazione per eliminare immediatamente lo stato utente**  

     Se si configura il criterio di eliminazione nel punto di migrazione dello stato per rimuovere i dati contrassegnati per l'eliminazione immediatamente e un utente malintenzionato riesce a recuperare i dati dello stato utente prima che lo faccia il computer valido, i dati dello stato utente verrebbero eliminati immediatamente. Impostare un intervallo **Elimina dopo** abbastanza ampio per verificare il ripristino corretto dei dati dello stato utente.  

-   **Eliminare manualmente le associazioni computer quando il ripristino dei dati della migrazione dello stato utente è stato completato e verificato**  

     Configuration Manager non rimuove automaticamente le associazioni computer. Proteggere l'identificazione dei dati dello stato utente eliminando manualmente le associazioni computer che non sono più necessarie.  

-   **Eseguire manualmente il backup dei dati della migrazione dello stato utente nel punto di migrazione dello stato**  

     Il backup di Configuration Manager non include i dati della migrazione dello stato utente.  

-   **Ricordare di abilitare BitLocker dopo l'installazione del sistema operativo**  

     Se un computer supporta BitLocker, è necessario disabilitarlo usando un passaggio della sequenza di attività se si desidera installare il sistema operativo automaticamente. Configuration Manager non abilita BitLocker dopo l'installazione del sistema operativo, quindi è necessario abilitarlo manualmente.  

-   **Implementare i controlli di accesso per proteggere i supporti pre-installati**  

     Controllare l'accesso fisico ai supporti per evitare che un utente malintenzionato utilizzi gli attacchi crittografici per ottenere il certificato di autenticazione client e i dati sensibili.  

-   **Implementare i controlli di accesso per proteggere il processo di creazione dell'immagine del computer di riferimento**  

     Assicurarsi che il computer di riferimento che si utilizza per acquisire le immagini del sistema operativo si trovi in un ambiente protetto con controlli di accesso appropriati, in modo che non possa essere installato e inavvertitamente incluso nell'immagine acquisita del software imprevisto o dannoso. Quando si acquisisce l'immagine, assicurarsi che il percorso di condivisione del file della rete di destinazione sia protetto in modo che l'immagine non possa essere manomessa dopo l'acquisizione.  

-   **Installare sempre gli aggiornamenti di protezione più recenti sul computer di riferimento**  

     Quando il computer di riferimento dispone degli aggiornamenti di sicurezza correnti, ciò riduce la vulnerabilità dei nuovi computer quando vengono avviati per la prima volta.  

-   **Se è necessario distribuire i sistemi operativi in un computer sconosciuto, implementare i controlli di accesso per impedire la connessione alla rete di computer non autorizzati**  

     Nonostante il provisioning di computer sconosciuti fornisca un metodo utile per distribuire nuovi computer su richiesta, questa operazione può anche consentire a un utente malintenzionato di diventare un client affidabile nella rete. Limitare l'accesso fisico alla rete e monitorare i client per rilevare i computer non autorizzati. Inoltre, i computer che rispondono alla distribuzione di sistemi operativi avviata da PXE potrebbero assistere alla distruzione di tutti i dati durante la distribuzione del sistema operativo, che potrebbe portare a una perdita di disponibilità di sistemi che vengono inavvertitamente riformattati.  

-   **Abilitare la crittografia per i pacchetti multicast**  

     Per ogni pacchetto di distribuzione del sistema operativo, è possibile abilitare la crittografia quando Configuration Manager trasferisce il pacchetto usando multicast. Questa configurazione consente di impedire ai computer non autorizzati di partecipare alla sessione multicast e a utenti malintenzionati di manomettere la trasmissione.  

-   **Monitorare i punti di distribuzione non autorizzati abilitati per multicast**  

     Se degli utenti malintenzionati riescono ad accedere alla rete, possono configurare server multicast non autorizzati per lo spoofing della distribuzione del sistema operativo.  

-   **Quando si esportano sequenze di attività in un percorso di rete, proteggere il percorso e il canale di rete**  

     Limitare l'accesso alla cartella di rete.  

     Utilizzare la firma SMB o IPsec tra il percorso di rete e il server del sito per impedire all'autore di un attacco di manomettere la sequenza attività esportata.  

-   **Proteggere il canale di comunicazione quando si carica un disco rigido virtuale in Virtual Machine Manager**  

     Per impedire l'eventuale manomissione di dati durante il trasferimento in rete, usare IPsec (Internet Protocol security) o SMB (Server Message Block) tra il computer che esegue la console di Configuration Manager e il computer che esegue Virtual Machine Manager.  

-   **Se è necessario usare l'esecuzione della sequenza attività come account, adottare misure di sicurezza aggiuntive**  

     Se si utilizza l'esecuzione della sequenza attività come account, attenersi ai seguenti passaggi precauzionali:  

    -   Utilizzare un account con autorizzazioni minime.  

    -   Non usare l'account di accesso alla rete per questo account.  

    -   Non modificare mai l'account in amministratore di dominio.  

     Inoltre:  

    -   Non configurare mai profili mobili per questo account. Quando viene eseguita la sequenza di attività, verrà scaricato il profilo mobile per l'account, che rende il profilo vulnerabile all'accesso sul computer locale.  

    -   Limitare l'ambito dell'account. Ad esempio, creare diverse esecuzioni della sequenza attività come account per ciascuna sequenza attività, in modo che nel caso in cui venga compromesso un account, vengano compromessi solo i computer client a cui tale account ha accesso. Se la riga di comando richiede accesso amministrativo al computer, creare un account amministratore locale unicamente per l'esecuzione della sequenza attività come account su tutti i computer che eseguiranno la sequenza attività ed eliminare l'account non appena non è più necessario.  

-   **Limitare e monitorare gli utenti amministrativi a cui è garantito il ruolo di protezione Gestione distribuzione del sistema operativo**  

     Gli utenti amministratori a cui è garantito il ruolo di protezione Gestione distribuzione del sistema operativo possono creare certificati autofirmati che in seguito possono essere usati per impersonare un client e ottenere criteri client da Configuration Manager.  

### <a name="security-issues-for-operating-system-deployment"></a>Problemi di sicurezza per la distribuzione del sistema operativo  
 Nonostante la distribuzione del sistema operativo possa essere un modo utile per distribuire i sistemi operativi e le configurazioni più sicure per i computer sulla rete, presenta i seguenti rischi di sicurezza:  

-   Divulgazione di informazioni e Denial of Service  

     Se un utente malintenzionato riesce a ottenere il controllo dell'infrastruttura di Configuration Manager, potrebbe eseguire qualsiasi sequenza attività, tra cui la formattazione dei dischi rigidi di tutti i computer client. Le sequenze attività possono essere configurate per contenere informazioni sensibili, come gli account che dispongono delle autorizzazioni per raggiungere il dominio e le chiavi di Volume Licensing.  

-   Rappresentazione e aumento di privilegi  

     Le sequenze di attività possono aggiungere un computer a un dominio, operazione che può fornire a un computer non autorizzato l'accesso autenticato alla rete. Un'altra importante considerazioni di sicurezza per la distribuzione del sistema operativo è la protezione del certificato di autenticazione client che viene utilizzato per i supporti della sequenza attività di avvio e per la distribuzione dell'avvio PXE. Quando si acquisisce un certificato di autenticazione client, si da a un utente malintenzionato l'opportunità di ottenere la chiave privata nel certificato e di rappresentare quindi un client valido sulla rete.  

     Se un utente malintenzionato ottiene il certificato client utilizzato per il supporto della sequenza attività di avvio e per la distribuzione dell'avvio PXE, questo certificato può essere usato per rappresentare un client valido in Configuration Manager. In questo scenario, il computer non autorizzato può scaricare criteri, che possono contenere dati sensibili.  

     Se i client utilizzano l'Account di accesso alla rete per accedere a dati archiviati sul punto di migrazione dello stato, tali client condivideranno effettivamente la stessa identità e potranno accedere ai dati di migrazione dello stato da un altro client che utilizza l'Account di accesso alla rete. I dati vengono crittografati in modo che solo il client originale sia in grado di leggerli, ma i dati potrebbero essere alterati o eliminati.  

-   L'autenticazione client al punto di migrazione stato viene ottenuta con un token di Configuration Manager emesso dal punto di gestione.  

     Configuration Manager inoltre non limita e non gestisce la quantità di dati archiviati nel punto di migrazione dello stato, quindi è possibile che lo spazio su disco disponibile venga riempito da un utente malintenzionato, provocando un attacco di tipo Denial of Service.  

-   Se si utilizzano le variabili di raccolta, gli amministratori locali saranno in grado di leggere informazioni potenzialmente riservate  

     Anche se le variabili di raccolta offrono un metodo flessibile per distribuire i sistemi operativi, è possibile che si verifichi una divulgazione di informazioni.  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Informazioni sulla privacy per la distribuzione del sistema operativo  
 Oltre a distribuire sistemi operativi in computer privi di sistema operativo, Configuration Manager consente anche di eseguire la migrazione di file e impostazioni utente da un computer all'altro. L'amministratore configura le informazioni da trasferire, inclusi file di dati personali, impostazioni di configurazione e cookie del browser.  

 Le informazioni vengono archiviate in un punto di migrazione dello stato e vengono crittografate durante la trasmissione e l'archiviazione. Le informazioni potranno essere recuperate tramite il nuovo computer associato alle informazioni sullo stato. Se il nuovo computer perde la chiave per il recupero delle informazioni, un amministratore di Configuration Manager con diritto Visualizza informazioni di ripristino negli oggetti di istanza di associazione computer potrà accedere alle informazioni e associarle a un nuovo computer. Dopo il ripristino delle informazioni sullo stato, per impostazione predefinita il nuovo computer elimina i dati dopo un giorno. È possibile configurare il momento in cui il punto di migrazione dello stato rimuoverà i dati contrassegnati per l'eliminazione. Le informazioni sulla migrazione dello stato non vengono archiviati database del sito e non vengono inviate a Microsoft.  

 Se si utilizzano supporti di avvio per distribuire immagini del sistema operativo, utilizzare sempre l'opzione predefinita per proteggere con una password il supporto di avvio. La password crittografa eventuali variabili archiviate nella sequenza attività, ma eventuali informazioni non archiviate in una variabile potrebbero essere esposte alla divulgazione.  

 Distribuzione sistema operativo può utilizzare sequenze attività per eseguire varie attività durante il processo di distribuzione, che include l'installazione di applicazioni e aggiornamenti software. Quando si configurano le sequenze attività, è necessario inoltre tenere presenti le implicazioni sulla privacy relative all'installazione del software.  

 Se si carica un disco rigido virtuale in Virtual Machine Manager senza utilizzare prima Sysprep per pulire l'immagine, il disco rigido virtuale caricato potrebbe contenere dati personali dall'immagine originale.  

 Configuration Manager non implementa la distribuzione del sistema operativo per impostazione predefinita. Per raccogliere informazioni sullo stato utente o creare sequenze attività o immagini di avvio, saranno necessari alcuni passaggi di configurazione.  

 Prima di configurare la distribuzione del sistema operativo, prendere in considerazione la tutela della privacy.  

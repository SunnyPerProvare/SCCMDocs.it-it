---
title: Ripristino automatico
titleSuffix: Configuration Manager
description: Usare uno script per ripristinare i siti in System Center Configuration Manager.
ms.custom: na
ms.date: 6/5/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 828c31d1-3d70-4412-b1a8-c92e7e504d39
caps.latest.revision: 
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: 45db0a824f325d2391f784cbf9bb8e3a35166579
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="unattended-site-recovery-for-configuration-manager"></a>Ripristino automatico del sito per Configuration Manager   

*Si applica a: System Center Configuration Manager (Current Branch)* Per eseguire un [ripristino automatico](/sccm/protect/understand/recover-sites#site-recovery-procedures) di un sito di amministrazione centrale o di un sito primario di Configuration Manager, è possibile creare uno script di installazione automatica e usare il programma di installazione con l'opzione di comando **/script**. Lo script fornisce lo stesso tipo di informazioni richieste dall'Installazione guidata, ma non prevede impostazioni predefinite. Per le chiavi di installazione applicabili al tipo di ripristino che si usa, è necessario specificare tutti i valori.

 Per usare l'opzione di installazione da riga di comando /script, è necessario creare un file di inizializzazione e specificarne il nome dopo l'opzione di installazione da riga di comando /script. Il nome del file non è rilevante, purché l'estensione del nome file sia **INI**. Quando si fa riferimento a file di inizializzazione dell'installazione dalla riga di comando, è necessario specificare il percorso completo del file. Se ad esempio il file di inizializzazione dell'installazione è denominato *setup.ini* e viene archiviato nella cartella *C:\setup*, la riga di comando sarà:

 **setup /script c:\setup\setup.ini**.

> [!IMPORTANT]  
>  È necessario disporre dei diritti di amministratore per eseguire il programma di installazione. Quando il programma di installazione viene eseguito con lo script automatico, è necessario avviare il prompt dei comandi in un contesto di amministrazione usando **Esegui come amministratore**.

 Lo script contiene nomi di sezione, nomi delle chiavi e valori. I nomi delle chiavi di sezione richiesti variano a seconda del tipo di ripristino per cui si crea lo script. L'ordine delle chiavi all'interno delle sezioni e l'ordine delle sezioni all'interno del file non è rilevante. Alle chiavi non viene applicata la distinzione tra maiuscole e minuscole. Quando si specificano i valori per le chiavi, il nome della chiave deve essere seguito dal segno uguale (=) e dal valore della chiave.

 Usare le seguenti sezioni per creare lo script per il ripristino automatico del sito. Nelle tabelle sono elencate le chiavi dello script di installazione, i relativi valori, se richiesti, il tipo di installazione per cui vengono usate e una breve descrizione relativa alla chiave.

## <a name="recover-a-central-administration-site-unattended"></a>Ripristinare un sito di amministrazione centrale in modo automatico
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
    -   **Valori:** 0 o 1 0 = non installare   
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
    -   **Valori:** *&lt;NomeDatabaseSito\>* o *&lt;NomeIstanza\>*\\*&lt;NomeDatabaseSito\>*
    -   **Dettagli:** specifica il nome del database di SQL Server da creare o usare per installare il database del sito di amministrazione centrale. È necessario specificare lo stesso nome database usato prima dell'errore.

        > [!IMPORTANT]  
        >  Se non si usa l'istanza predefinita, è necessario specificare il nome dell'istanza e il nome database del sito.

-   **Nome chiave:** SQLSSBPort

    -   **Richiesto:** no
    -   **Valori:** &lt;*NumeroPortaSSB*>
    -   **Dettagli:** specifica la porta di SQL Server Service Broker (SSB) usata da SQL Server. In genere, SSB è configurato per usare la porta TCP 4022, ma sono supportate anche altre porte. È necessario specificare la stessa porta SSB usata prima dell'errore.

## <a name="recover-a-primary-site-unattended"></a>Ripristinare un sito primario automatico
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
    -   **Valori:** *&lt;NomeDatabaseSito\>* o *&lt;NomeIstanza\>*\\*&lt;NomeDatabaseSito\>*
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

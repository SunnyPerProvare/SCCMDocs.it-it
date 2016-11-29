---
title: Installazione guidata | System Center Configuration Manager
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1f703376-5f2c-4fd2-8209-7028c931ddc7
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: ffcdf4285d5f182e8d625200989f65c748bc2067
ms.openlocfilehash: 9552ac1b77acfce6a398ec6e74f1be3686ee15a4

---
# <a name="use-the-setup-wizard-to-install-system-center-configuration-manager-sites"></a>Usare l'installazione guidata per installare i siti di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


Per installare un nuovo sito di System Center Configuration Manager usando un'interfaccia utente interattiva, è possibile usare l'installazione guidata di Configuration Manager (setup.exe). La procedura guidata supporta l'installazione di un sito primario o un sito di amministrazione centrale. È anche possibile usare la procedura guidata per [aggiornare un'installazione di valutazione](../../../../core/servers/deploy/install/upgrade-an-evaluation-install-to-a-full-install.md) di Configuration Manager per un'installazione con licenza completa.  È possibile usare in alternativa alla procedura guidata uno [script di installazione](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md) ed eseguire un'installazione automatica dalla riga di comando.

Per installare un sito secondario, è necessario installare il sito dall'interno della console di Configuration Manager.  I siti secondari non supportano l'installazione con script dalla riga di comando.

## <a name="a-namebkmkprimarya-install-a-central-administration-site-or-primary-site"></a><a name="bkmk_primary"></a> Installare un sito di amministrazione centrale o primario
Usare la procedura seguente per installare un sito di amministrazione centrale, un sito primario o per aggiornare un sito di valutazione a un sito di Configuration Manager con licenza completa.   

Prima di iniziare l'installazione del sito, è consigliabile acquisire una certa familiarità con gli argomenti seguenti:
 -  [Preparare l'installazione di siti](../../../../core/servers/deploy/install/prepare-to-install-sites.md)
 -  [Prerequisiti per l'installazione di un sito](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md)

Se si installa un sito di amministrazione centrale come parte di uno scenario di espansione del sito, consultare la sezione relativa all'[espansione di un sito primario autonomo](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand) in questo argomento prima di usare la procedura seguente.

### <a name="a-namebkmkinstallpria-to-install-a-primary-or-central-administration-site"></a><a name="bkmk_installpri"></a> Per installare un sito di amministrazione centrale o primario

1.  Nel computer in cui si vuole installare il sito eseguire **&lt;InstallationMedia\>\SMSSETUP\BIN\X64\Setup.exe** per avviare la procedura di **Installazione guidata di System Center Configuration Manager**.  

    > [!NOTE]  
    >  Quando si installa un sito di amministrazione centrale per espandere un sito primario autonomo o si installa un nuovo sito primario figlio in una gerarchia esistente, è necessario usare il supporto di installazione (file di origine) corrispondente alla versione del sito o dei siti esistenti.  Se sono stati installati nella console aggiornamenti che hanno modificato la versione dei siti installati in precedenza, non usare il supporto di installazione originale ma i file di origine della [cartella CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) di un sito aggiornato.  Configuration Manager richiede l'uso di file di origine corrispondenti alla versione del sito esistente a cui si connetterà il nuovo sito.  

2.  Nella pagina **Prima di iniziare** fare clic su **Avanti**.  

3.  Nella pagina **Riquadro attività iniziale** selezionare il tipo di sito che si vuole installare:  

     **Sito di amministrazione centrale**: come il primo sito di una nuova gerarchia o quando si espande un sito primario autonomo:  

    -   Selezionare: **Installa un sito di amministrazione centrale di Configuration Manager**  

         In un passaggio successivo di questa procedura, è possibile scegliere di installare un sito di amministrazione centrale come primo sito di una nuova gerarchia oppure installare un sito di amministrazione centrale per l'espansione in un sito primario autonomo.  

     **Sito primario**: come sito primario autonomo che è il primo sito di una nuova gerarchia o come sito primario figlio:  

    -   Selezionare: **Installa un server di sito primario di Configuration Manager**  

        > [!TIP]  
        >  In genere, si seleziona l'opzione **Utilizza le opzioni di installazione tipiche per un sito primario autonomo** solo quando si vuole installare un sito primario autonomo in un ambiente di test. Se si seleziona questa opzione:  
        >   
        > -   Il programma di installazione configura automaticamente il sito come sito primario autonomo  
        > -   Usa un percorso di installazione predefinito  
        > -   Usa un'installazione locale dell'istanza predefinita di SQL Server per il database del sito  
        > -   Installa un punto di gestione e un punto di distribuzione nel computer server del sito  
        > -   Configura il sito in lingua inglese e nella lingua di visualizzazione del sistema operativo nel server del sito primario, se corrisponde a una delle lingue supportate da Configuration Manager  

4.  Nella pagina **Codice Product Key**:
    - Scegliere se installare Configuration Manager come versione di valutazione o versione con licenza.  

      -   Se si seleziona una versione con licenza, immettere il codice Product Key e fare clic su **Avanti**.  

      -   Se si seleziona una versione di valutazione, fare clic su **Avanti**. È possibile aggiornare un'installazione di valutazione a un'installazione completa in un secondo momento.  
    - A partire dalla versione di ottobre 2016 del supporto di base per System Center Configuration Manager versione 1606, è possibile specificare la data di scadenza del contratto Software Assurance. In questa pagina è possibile specificare la **data di scadenza di Software Assurance** del contratto di licenza come utile promemoria per l'utente. Se non si immette questa data durante l'installazione, è possibile specificarla in un secondo momento dalla console di Configuration Manager.

      >  [!NOTE]   
      >  Microsoft non convalida la data di scadenza immessa e non userà tale data per la convalida della licenza.  È possibile invece usarla come promemoria della data di scadenza. Configuration Manager infatti verifica periodicamente la presenza di nuovi aggiornamenti software disponibili online. È necessario che lo stato di licenza di Software Assurance sia regolare per poter usufruire di questi aggiornamenti aggiuntivi.    

      Per altre informazioni, vedere [Licensing and branches for System Center Configuration Manager](/sccm/core/understand/learn-more-editions) (Licenze e branch per System Center Configuration Manager).

5.  Nella pagina **Condizioni di licenza software Microsoft** leggere e accettare le condizioni di licenza.  

6.  Nella pagina **Licenze prerequisite** leggere e accettare le condizioni di licenza per i prerequisiti software.  Il programma di installazione scarica e installa automaticamente il software sui client o sui sistemi del sito secondo necessità. Prima di procedere alla pagina successiva, è necessario selezionare tutte le caselle di controllo.  

7.  Nella pagina **Download prerequisiti** specificare se il programma di installazione deve scaricare da Internet i file ridistribuibili richiesti più recenti o se usare i file scaricati in precedenza:  

    -   Se si vuole che il programma di installazione scarichi i file al momento dell'installazione, selezionare **Scarica file richiesti** e specificare un percorso in cui memorizzare i file.  

    -   Se i file sono stati scaricati in precedenza con il [downloader di installazione](../../../../core/servers/deploy/install/setup-downloader.md), selezionare **Utilizza file scaricati precedentemente** e specificare la cartella di download.  

        > [!TIP]  
        >  Se si usano i file scaricati in precedenza, verificare che il percorso alla cartella di download contenga la versione più recente dei file.  

8.  Nella pagina **Selezione della lingua server** selezionare le lingue disponibili per la console di  Configuration Manager e per i report. La lingua inglese è selezionata per impostazione predefinita e non può essere rimossa.  

9. Nella pagina **Selezione della lingua client** selezionare le lingue disponibili per i computer client e specificare se abilitare tutte le lingue client per i client dei dispositivi mobili. La lingua inglese è selezionata per impostazione predefinita e non può essere rimossa.  

    > [!IMPORTANT]  
    > Quando si usa un sito di amministrazione centrale verificare che le lingue client configurate nel sito di amministrazione centrale includano tutte le lingue client configurate in ogni sito primario figlio. In questo modo i client installati da un punto di distribuzione hanno accesso alle lingue client dal sito di livello superiore, mentre client installati da un punto di gestione hanno accesso alle lingue client dal relativo sito primario assegnato.  

10. Nella pagina **Impostazioni di installazione e del sito** specificare quanto segue per il nuovo sito che si sta installando:  

    -   **Codice del sito**: [ogni codice del sito in una gerarchia deve essere univoco](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_sitecodes) ed essere costituito da tre caratteri alfanumerici (dalla A alla Z e da 0 a 9). Dal momento che il codice del sito viene usato nei nomi di cartella, non usare i nomi seguenti per il sito, tra cui i nomi riservati di Windows:    
        -   AUX  
        -   CON    
        -   NUL    
        -   PRN    
        -   SMS  

        > [!NOTE]  
        >  Il programma di installazione non verifica se il codice del sito specificato è già in uso o se è un nome riservato.  

    -   **Nome sito:** ogni sito deve essere identificato da un nome descrittivo.  

    -   **Cartella di installazione**: questo è il percorso della cartella per l'installazione di Configuration Manager. Non è possibile modificare il percorso dopo l'installazione del sito e il percorso non può contenere caratteri Unicode o spazi finali.  

11. Nella pagina **Installazione sito** usare l'opzione seguente che corrisponde allo scenario:  

    -   **Installazione di un sito di amministrazione centrale:**  

         Nella pagina **Installazione del sito di amministrazione centrale** selezionare **Installa come primo sito in una nuova gerarchia**e quindi fare clic su **Avanti** per continuare.  

    -   **Espansione di un sito primario autonomo in una gerarchia con un sito di amministrazione centrale:**  

         Nella pagina **Installazione del sito di amministrazione centrale** selezionare **Espandi un sito primario autonomo esistente in una gerarchia**, specificare il nome FQDN del server del sito primario autonomo e quindi fare clic su **Avanti** per continuare.  

         Il supporto usato per l'installazione del nuovo sito di amministrazione centrale deve corrispondere alla versione del sito primario.  

    -   **Installazione di un sito primario autonomo:**  

         Nella pagina **Installazione del sito primario** selezionare**Installa il sito primario come sito autonomo**e quindi fare clic su **Avanti**.  

    -   **Installazione di un sito primario figlio:**  

         Nella pagina **Installazione del sito primario** selezionare **Associa il sito primario a una gerarchia esistente**, specificare l'FQDN per il sito di amministrazione centrale e fare clic su **Avanti**.  

12. Nella pagina Informazioni database specificare le informazioni seguenti:  

    -   **Nome SQL Server (FQDN):** per impostazione predefinita, il valore è impostato come computer server del sito.  

    -   **Nome istanza:** per impostazione predefinita, questo valore è vuoto e userà l'istanza predefinita di SQL del computer server del sito.  

    -   **Nome database:** per impostazione predefinita, questo valore è impostato su CM_&lt;CodiceSito\>. È possibile specificare un nome differente.  

    -   **Porta di Service Broker:** per impostazione predefinita, questo valore è impostato per usare la porta SQL Server di Service Broker (SSB) predefinita 4022 e viene usato da SQL per comunicare direttamente con il database del sito in altri siti.  

13. Nella seconda pagina **Informazioni database** è possibile specificare percorsi non predefiniti per il file di dati e il file di log SQL Server per il database del sito:  

    -   Sono impostati i percorsi di file predefiniti per SQL Server  

    -   L'opzione per specificare percorsi di file non predefiniti non è disponibile quando si usa un cluster di SQL Server  

    -   Il Controllo prerequisiti non verifica lo spazio libero su disco per i percorsi di file non predefiniti  

14. Nella pagina **Impostazioni del provider SMS** specificare il nome FQDN per il server in cui si vuole installare il provider SMS.  

    -   Per impostazione predefinita, è specificato il server del sito.  

    -   Dopo l'installazione del sito, è possibile configurare altri provider SMS  

15. Nella pagina **Impostazioni di comunicazione client** scegliere se configurare tutti i sistemi del sito per l'accettazione esclusiva delle comunicazioni HTTPS dai client o per il metodo di comunicazione da configurare in ciascun ruolo del sistema del sito.  

    -   Quando si seleziona **Tutti i ruoli del sistema del sito accettano solo le comunicazioni HTTPS dai client**, il computer client deve avere un certificato PKI valido per l'autenticazione client. Per altre informazioni sui requisiti dei certificati, vedere l'argomento relativo ai requisiti dei certificati PKI per Configuration Manager  

    > [!NOTE]  
    >  Questo passaggio si applica solo quando si installa un sito primario. Se si installa un sito di amministrazione centrale, ignorare questo passaggio.  

16. Nella pagina **Ruoli sistema del sito** scegliere se installare un punto di gestione o un punto di distribuzione. Per ogni ruolo che si è deciso di installare con il programma di installazione:  

    -   È necessario immettere il nome **FQDN** per il computer che ospiterà il ruolo e scegliere il metodo di connessione client supportato dal server (HTTP o HTTPS).  

    -   Se nella pagina precedente si è selezionato **Tutti i ruoli del sistema del sito accettano solo le comunicazioni HTTPS dai client** , le impostazioni di connessione client vengono automaticamente configurate per HTTPS e non sarà possibile modificarle a meno che non si torni indietro e si cambi l'impostazione.  

    > [!NOTE]  
    >  Questo passaggio si applica solo quando si installa un sito primario. Se si installa un sito di amministrazione centrale, ignorare questo passaggio.  

    > [!NOTE]  
    >  Per installare i ruoli del sistema del sito, il programma di installazione usa l' **account di installazione del sistema del sito**. Per impostazione predefinita, quest'ultimo usa l'account computer del sito primario.  Per installare il ruolo del sistema del sito, tale account deve corrispondere a un amministratore locale in un computer remoto. Se l'account non ha le autorizzazioni necessarie, deselezionare i ruoli del sistema del sito e installarli in un secondo momento dalla console di Configuration Manager, dopo aver configurato gli account aggiuntivi da usare come account di installazione del sistema del sito.  

17. Nella pagina **Dati di utilizzo** esaminare le informazioni sui dati raccolti da Microsoft e quindi fare clic su **Avanti**.  

18. L' **installazione del punto di connessione del servizio** è disponibile solo durante una delle installazioni seguenti:  

    -   Installazione di un sito primario autonomo  

    -   Installazione di un sito di amministrazione centrale  

    > [!NOTE]  
    >  Se si installa un sito primario figlio, ignorare questo passaggio (questa pagina non è disponibile).  

     Se si installa un sito di amministrazione centrale come parte di uno scenario di espansione del sito e questo ruolo è già installato nel sito primario autonomo, è necessario disinstallare il ruolo dal sito primario autonomo. In una gerarchia è consentita solo un'istanza di questo ruolo ed è consentita solo nel sito di livello superiore della gerarchia.  

     Dopo aver selezionato una configurazione per il **punto di connessione del servizio** fare clic su **Avanti**. Al termine dell'installazione, è possibile modificare questa configurazione nella console di Configuration Manager.  

19. Nella pagina **Riepilogo impostazioni** esaminare l'impostazione selezionata e fare clic su **Avanti** per avviare il Controllo prerequisiti.  

20. Nella pagina di **verifica dell'installazione dei prerequisiti** vengono elencati i problemi che possono essere identificati.  

    -   Quando il Controllo prerequisiti rileva un problema, fare clic su un elemento nell'elenco per informazioni dettagliate sulla relativa modalità di risoluzione.  

    -   Prima di continuare a installare il sito è necessario risolvere gli elementi con stato **Non riuscito** . Gli elementi con stato **Avviso** devono essere risolti, ma non bloccano l'installazione del sito.  

    -   Dopo la risoluzione dei problemi fare clic su **Esegui controllo** per eseguire nuovamente il Controllo prerequisiti.  

     Se si esegue il Controllo prerequisiti e a nessun controllo viene assegnato lo stato **Non riuscito** , è possibile fare clic su **Inizia installazione** per avviare l'installazione del sito.  

    > [!TIP]  
    >  Oltre ai suggerimenti forniti nella procedura guidata, è possibile trovare altre informazioni sui problemi dei prerequisiti quando si visualizza il file **ConfigMgrPrereq.log** nella radice dell'unità di sistema del computer che si sta installando.  Per un elenco delle regole e delle descrizioni dei prerequisiti di installazione, vedere l'[elenco dei controlli dei prerequisiti per System Center Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md).  

21. Nella pagina **Installazione** viene visualizzato lo stato dell'installazione. Dopo aver completato l'installazione del server del sito principale sarà possibile **chiudere** l'installazione guidata. Dopo aver chiuso la procedura guidata, l'installazione e la configurazione iniziale del sito continuano in background.  

    -   Prima del completamento dell'installazione è possibile connettere una console di Configuration Manager al sito. Questa console si connette in sola lettura e consente di visualizzare gli oggetti e le impostazioni, ma non introduce modifiche.  

    -   Al termine dell'installazione, sarà possibile connettersi a una console che consente di modificare gli oggetti e le impostazioni.  


## <a name="a-namebkmkexpanda-expand-a-stand-alone-primary-site"></a><a name="bkmk_expand"></a> Espandere un sito primario autonomo
Dopo aver installato un sito primario autonomo come primo sito, è possibile espanderlo, in un secondo momento, in una gerarchia più ampia installando un sito di amministrazione centrale.   

Quando si espande un sito primario autonomo, si installa un nuovo sito di amministrazione centrale che usa il database del sito primario autonomo esistente come riferimento. Dopo l'installazione del nuovo sito di amministrazione centrale, il sito primario autonomo agisce da sito primario figlio.


-   Soltanto un sito primario autonomo può essere espanso in una nuova gerarchia.  

-   È possibile espandere un solo sito primario autonomo in una gerarchia specifica. È possibile usare questa opzione per aggiungere altri siti primari autonomi nella stessa gerarchia. In alternativa, usare la migrazione per migrare i dati da una gerarchia a un'altra.  

-   In seguito all'espansione di un sito primario autonomo in una gerarchia con un sito di amministrazione centrale, è possibile aggiungere altri siti primari figlio.  

-   Per rimuovere un sito primario da una gerarchia con un sito di amministrazione centrale, è necessario disinstallare il sito primario.  

Per espandere il sito, usare l'installazione guidata di System Center Configuration Manager per installare un nuovo sito di amministrazione centrale in base alle indicazioni seguenti:  

-   È necessario installare il sito di amministrazione centrale usando la stessa versione di Configuration Manager come sito primario autonomo.  

-   Nella pagina introduttiva dell'installazione guidata, selezionare l'opzione per installare un sito di amministrazione centrale. In una fase successiva dell'installazione, scegliere un'opzione per espandere un sito primario autonomo esistente.  

-   Quando si configura la pagina Selezione della lingua client per il nuovo sito di amministrazione centrale, è necessario selezionare le stesse lingue client configurate per il sito primario autonomo che si vuole espandere.  

-   Nella pagina Installazione sito selezionare l'opzione per espandere il sito primario autonomo.  

Per espandere un sito primario autonomo, usare la procedura *[Per installare un sito di amministrazione centrale o primario](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_installpri)*, riportata in precedenza in questo articolo.


## <a name="a-namebkmksecondarya-install-a-secondary-site"></a><a name="bkmk_secondary"></a> Installare un sito secondario
 Per installare un sito secondario, usare la console di Configuration Manager.  

-   Se la console in uso non è connessa al sito primario che sarà il sito padre per il nuovo sito secondario, il comando per installare il sito verrà replicato nel sito primario corretto.  

-   Prima di iniziare l'installazione del sito, verificare che l'account utente abbia le autorizzazioni richieste e che il computer che ospiterà il nuovo sito secondario soddisfi tutti i prerequisiti per l'uso come server del sito secondario.  

-   Quando si installa il sito secondario, Configuration Manager configura il nuovo sito per l'uso delle porte di comunicazione del client configurate nel sito primario padre.  

### <a name="a-namebkmkinstallsecondarya-to-install-a-secondary-site"></a><a name="bkmk_installsecondary"></a> Per installare un sito secondario  


1.  Nella console di Configuration Manager passare a **Amministrazione** > **Configurazione del sito** > **Siti**e selezionare il sito che diventerà il sito primario padre del nuovo sito secondario.  

2.  Fare clic su **Crea sito secondario** per avviare la **Creazione guidata sito secondario**.  

3.  Nella pagina **Prima di iniziare** confermare che il sito primario elencato sia quello che si vuole definire come padre del nuovo sito secondario e quindi fare clic su **Avanti**.  

4.  Nella pagina **Generale** specificare le impostazioni seguenti:  

    -   **Codice del sito**: ogni codice del sito in una gerarchia deve essere univoco ed essere costituito da tre caratteri alfanumerici (dalla A alla Z e da 0 a 9). Dal momento che il codice del sito viene usato nei nomi di cartella, non usare i nomi riservati di Windows, ad esempio:  

        -   AUX    
        -   CON    
        -   NUL    
        -   PRN  
        -   SMS  

       > [!NOTE]  
       >  Il programma di installazione non verifica se il codice del sito specificato è già in uso o se è un nome riservato.  

    -   **Nome server sito**: questo è il nome FQDN del server in cui verrà installato il nuovo sito secondario.  

    -   **Nome sito**: ogni sito deve essere identificato da un nome descrittivo.  

    -   **Cartella di installazione**: questo è il percorso della cartella per l'installazione di Configuration Manager. Non è possibile modificare il percorso dopo l'installazione del sito e il percorso non può contenere caratteri Unicode o spazi finali.  

    > [!IMPORTANT]  
    >  Dopo aver specificato i dettagli in questa pagina, è possibile fare clic su **Riepilogo** per usare le impostazioni predefinite per le rimanenti opzioni del sito secondario e per passare direttamente alla pagina **Riepilogo** della procedura guidata.  
    >   
    >  -   Usare questa opzione solo quando si ha familiarità con le impostazioni predefinite della procedura guidata e si vogliono usare tali impostazioni.  
    >  -   I gruppi di limiti non sono associati al punto di distribuzione quando si usano le impostazioni predefinite. Di conseguenza, finché non si configurano i gruppi di limiti che includono il server del sito secondario, i client non useranno il punto di distribuzione installato in questo sito secondario come percorso di origine del contenuto.  

5.  Nella pagina **File di origine dell'installazione** scegliere la modalità usata dal computer del sito secondario per ottenere i file di origine per l'installazione del sito.  

     Quando si usano i file di origine archiviati nella rete o nel computer del sito secondario:  

    -   Il percorso del file di origine deve includere una cartella denominata **Redist** che include tutti i file scaricati in precedenza con il Downloader di installazione.  

    -   Se i file della cartella **Redist** non sono disponibili, l'installazione del sito secondario avrà esito negativo.  

    -   L'account del computer del sito secondario deve avere le autorizzazioni di **lettura** sulla cartella del file di origine e di autorizzazioni di condivisione.  

6.  Nella pagina **Impostazioni di SQL Server** specificare la versione di SQL Server da usare e quindi configurare le impostazioni correlate.  

    > [!NOTE]  
    >  Il programma di installazione non convalida le informazioni immesse in questa pagina fino all'avvio dell'installazione. Prima di continuare, verificare queste impostazioni.  

     **Installa e configura una copia locale di SQL Express nel computer del sito secondario**  

    -   **Porta del servizio di SQL Server**: specificare la porta del servizio di SQL Server per l'uso da parte di SQL Server Express. La porta del servizio è in genere configurata per l'utilizzo della porta TCP 1433, ma è possibile configurare un'altra porta.  

    -   **Porta di SQL Server Service Broker**: specificare la porta di SQL Server Broker (SSB) per l'uso da parte di SQL Server Express. La porta di Service Broker è in genere configurata per l'utilizzo della porta TCP 4022, ma è possibile configurare un'altra porta. È necessario specificare una porta valida che non sia usata da nessun altro sito o servizio e che non sia soggetta ad alcuna restrizione del firewall.  

    > [!IMPORTANT]  
    >  Quando Configuration Manager installa SQL Server Express, viene installata la versione 2012 senza Service Pack:  
    >   
    >  -   Per il supporto del sito secondario, dopo l'installazione è necessario aggiornare SQL Server Express 2012 installando il Service Pack 2 (o versione successiva).
    >  -   Inoltre, se l'installazione del nuovo sito secondario non riesce, ma viene prima completata l'installazione di SQL Server Express 2012, è necessario aggiornare tale istanza di SQL Server Express prima che Configuration Manager possa ripetere l'installazione del sito secondario.  

     **Usa un'istanza di SQL Server esistente**  

    -   **FQDN di SQL Server**: esaminare il nome FQDN del computer SQL Server. È necessario usare un server SQL locale per ospitare il database del sito secondario e non è possibile modificare questa impostazione.  

    -   **Istanza SQL Server**: specificare l'istanza di SQL Server da usare come database del sito secondario. Lasciare vuota questa opzione per usare l'istanza predefinita.  

    -   **Nome database del sito di Configuration Manager**: specificare il nome da usare per il database del sito secondario.  

    -   **Porta di SQL Server Service Broker**: specificare la porta di SQL Server Service Broker (SSB) per l'uso da parte di SQL Server. È necessario specificare una porta valida che non sia usata da nessun altro sito o servizio e che non sia soggetta ad alcuna restrizione del firewall.  

    > [!TIP]  
    >  Vedere l'argomento relativo al [supporto per le versioni di SQL Server](../../../../core/plan-design/configs/support-for-sql-server-versions.md) per l'elenco delle versioni di SQL Server supportate con System Center Configuration Manager.  

7.  Nella pagina **Punto di distribuzione** configurare le impostazioni per il punto di distribuzione che verranno installate sul server del sito secondario.  

     **Impostazioni obbligatorie:**  

    -   **Specificare la modalità di comunicazione dei dispositivi client con il punto di distribuzione** : scegliere tra HTTP e HTTPS.  

    -   **Creare un certificato autofirmato o importare un certificato client PKI** : scegliere tra l'uso di un certificato autofirmato (che consente anche di usare connessioni anonime dai client di Configuration Manager alla raccolta contenuto) o l'importazione di un certificato da PKI.  

         Il certificato viene usato per l'autenticazione tra il punto di distribuzione e un punto di gestione prima che il punto di distribuzione invii messaggi di stato.  

         Per informazioni sui requisiti del certificato, vedere Requisiti dei certificati PKI per Configuration Manager.  

    **Impostazioni facoltative:**  

    -   **Installa e configura IIS se richiesto da Configuration Manager** : selezionare questa impostazione per consentire a Configuration Manager di installare e configurare Internet Information Services (IIS) sul server, se non già installato. IIS deve essere installato su tutti i punti di distribuzione.  

        > [!NOTE]  
        >  Anche se questa impostazione è facoltativa, è necessario installare IIS nel server prima di poter installare un punto di distribuzione.  

    -   **Abilitare e configurare BranchCache per il punto di distribuzione** •  

    -   **Descrizione** : descrizione del punto di distribuzione per semplificarne il riconoscimento.  

    -   **Abilita questo punto di distribuzione per il contenuto pre-installato**  

8.  Nella pagina **Impostazioni unità** specificare le impostazioni unità per il punto di distribuzione del sito secondario.  

     È possibile configurare fino a due unità disco per la raccolta contenuto e due unità disco per la condivisione pacchetto, sebbene Configuration Manager possa usare unità aggiuntive nel caso in cui le prime due raggiungano il limite di spazio riservato nell'unità configurata. Nella pagina **Impostazioni unità** è possibile configurare la priorità per le unità disco e la quantità di spazio disponibile su disco da conservare su ciascuna unità disco.  

    -   **Spazio riservato nell'unità (MB)**: il valore configurato per questa impostazione determina la quantità di spazio disponibile su un'unità prima che Configuration Manager scelga un'altra unità e continui il processo di copia su tale unità. I file di contenuto possono estendersi su più unità.  

    -   **Percorsi contenuto**: Specificare i percorsi del contenuto per la condivisione di pacchetti e raccolte di contenuti. Configuration Manager copia i contenuti nel percorso del contenuto principale finché la quantità di spazio libero raggiunge in valore specificato per **Riserva spazio su disco (MB)**. Per impostazione predefinita, i percorsi del contenuto sono impostati su **Automatico**e il percorso del contenuto primario sarà impostato sull'unità disco con maggiore spazio disponibile al momento dell'installazione. Il percorso secondario sarà assegnato all'unità disco con la seconda maggiore quantità di spazio disponibile. Quando le unità primaria e secondaria raggiungono il limite di spazio riservato, Configuration Manager seleziona un'altra unità disponibile con la maggiore quantità di spazio libero e continua il processo di copia.  

9. Nella pagina **Convalida contenuto** specificare se convalidare l'integrità dei file di contenuto nel punto di distribuzione.  

    -   Quando si abilita la convalida del contenuto su una pianificazione, Configuration Manager avvia il processo all'orario pianificato e tutto il contenuto sul punto di distribuzione viene verificato.  

    -   È anche possibile configurare la **priorità di convalida del contenuto**.  

    -   Per visualizzare i risultati del processo di convalida del contenuto, nella console di Configuration Manager passare a **Monitoraggio** >  **Stato distribuzione** >  **Stato contenuto**. Viene visualizzato il contenuto per ogni tipo di pacchetto (ad esempio, applicazione, pacchetto di aggiornamento software e immagine di avvio).  

10. Nella pagina **Gruppi limite** gestire i gruppi di limiti per i quali viene assegnato questo punto di distribuzione:  

    -   Durante la distribuzione del contenuto, i client devono trovarsi in un gruppo di limiti associato al punto di distribuzione per usarlo come percorso di origine per il contenuto.  

    -   È possibile selezionare l'opzione **Consenti percorso origine di fallback per il contenuto** per consentire ai client al di fuori di questi gruppi di limiti di eseguire il fallback e usare il punto di distribuzione come un percorso di origine quando i punti di distribuzione preferiti non sono disponibili.  

     Per informazioni sui punti di distribuzione preferiti, vedere l'argomento [Concetti di base sulla gestione dei contenuti](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

11. Nella pagina **Riepilogo** verificare le impostazioni, quindi fare clic su **Avanti** per installare il sito secondario. Quando la procedura guidata visualizza la pagina **Completamento** , è possibile chiudere la procedura guidata. L'installazione del sito secondario continua in background.  


### <a name="a-namebkmkverifya-to-verify-the-secondary-site-installation-status"></a><a name="bkmk_verify"></a> Per verificare lo stato di installazione del sito secondario  

1.  Nella console di Configuration Manager passare a **Amministrazione** > **Configurazione del sito** > **Siti**.  

2.  Selezionare il server del sito secondario che si sta installando e quindi fare clic su **Mostra stato installazione**.  

    > [!TIP]  
    >  Quando si installa più di un sito secondario simultaneamente, il controllo prerequisiti viene eseguito su un sito alla volta e deve essere terminato su un sito per poter poi avviarsi sul sito successivo.  



<!--HONumber=Nov16_HO1-->


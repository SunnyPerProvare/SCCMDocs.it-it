---
title: Pacchetti e programmi
titleSuffix: Configuration Manager
description: Supportare le distribuzioni che usano pacchetti e programmi o applicazioni con System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: caad0507-9913-415a-b13d-d36f8f0a1b80
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7c840c0a42ccf36e9c69044a6591b29d70c19093
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126456"
---
# <a name="packages-and-programs-in-system-center-configuration-manager"></a>Pacchetti e programmi in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager continua a supportare pacchetti e programmi usati in Configuration Manager 2007. Una distribuzione che usa pacchetti e programmi può essere più adatta rispetto a una che usa un'applicazione quando si distribuisce uno degli elementi seguenti:  

- Applicazioni per server Linux e UNIX
- Script che non installano un'applicazione in un computer, ad esempio uno script per deframmentare l'unità disco del computer
- Script occasionali che non devono essere monitorati continuamente  
- Script eseguiti in base a una pianificazione ricorrente e che non possono usare la valutazione globale

Quando si esegue la migrazione di pacchetti da una versione precedente di Configuration Manager, è possibile distribuirli nella gerarchia di Configuration Manager. Al termine della migrazione, i pacchetti vengono visualizzati nel nodo **Pacchetti** dell'area di lavoro **Raccolta software** .

È possibile modificare e distribuire questi pacchetti nello stesso modo dei casi in cui è stata usata la distribuzione del software. L'**Importazione guidata da definizione** rimane in Configuration Manager per importare pacchetti legacy. Gli annunci vengono convertiti in distribuzioni quando vengono migrati da Configuration Manager 2007 a una gerarchia di Configuration Manager.  

> [!NOTE]  
>  È possibile usare Microsoft System Center Configuration Manager Package Conversion Manager per convertire i pacchetti e i programmi in applicazioni di Configuration Manager.  
>   
>  Per altre informazioni, vedere [Configuration Manager Package Conversion Manager](https://technet.microsoft.com/library/hh531519.aspx).  

I pacchetti possono usare alcune nuove funzionalità di Configuration Manager, inclusi i gruppi di punti di distribuzione e il monitoraggio. Le applicazioni Microsoft Application Virtualization (App-V) non possono essere distribuite usando pacchetti e programmi in Configuration Manager. Per distribuire applicazioni virtuali, è necessario crearle come applicazioni di Configuration Manager.  

##  <a name="create-a-package-and-program"></a>Creare un pacchetto e un programma  
 Usare una di queste procedure per creare o importare pacchetti e programmi.  

### <a name="create-a-package-and-program-using-the-create-package-and-program-wizard"></a>Creare un pacchetto e un programma tramite la Creazione guidata pacchetto e programma  

1. Nella console di Configuration Manager scegliere **Raccolta software**  > **Gestione applicazioni** > **Pacchetti**.  

2. Nel gruppo **Crea** della scheda **Home** scegliere **Crea pacchetto**.  

3. Nel **pacchetto** di pagina il **Creazione guidata pacchetto e programma**, specificare le seguenti informazioni:  

   -   **Nome**: specificare un nome per il pacchetto con un massimo di 50 caratteri.  

   -   **Descrizione**: specificare una descrizione per il pacchetto con un massimo di 128 caratteri.  

   -   **Produttore** (facoltativo): specificare un nome produttore per identificare il pacchetto nella console di Configuration Manager. Il nome non può contenere più di 32 caratteri.

   -   **Lingua** (facoltativo): specificare la lingua del pacchetto con un massimo di 32 caratteri.  

   -   **Versione** (facoltativo):  specificare un numero di versione per il pacchetto con un massimo di 32 caratteri.

   -   **Questo pacchetto contiene file di origine**: questa impostazione indica se il pacchetto richiede che nei dispositivi client siano presenti file di origine. Per impostazione predefinita, questa casella di controllo non è selezionata e Configuration Manager non usa i punti di distribuzione per il pacchetto. Se questa casella di controllo è selezionata, vengono usati punti di distribuzione.  

   -   **Cartella di origine**: se il pacchetto contiene file di origine, scegliere **Sfoglia** per aprire la finestra di dialogo **Imposta cartella di origine** e specificare il percorso dei file di origine per il pacchetto.  

       > [!NOTE]  
       >  L'account computer del server del sito deve avere autorizzazioni di accesso in lettura alla cartella specificata.  

4. Nella pagina **Tipo di programma** della **Creazione guidata pacchetto e programma** selezionare il tipo di programma da creare e fare clic su **Avanti**. È possibile creare un programma per un computer o un dispositivo oppure ignorare questo passaggio e creare un programma in un secondo momento.  

   > [!TIP]  
   >  Per creare un nuovo programma per un pacchetto esistente, selezionare prima il pacchetto. Nel gruppo **Pacchetto** della scheda **Home** scegliere **Crea programma** per aprire la **Creazione guidata programma**.  

5. Per creare un programma standard o un programma di dispositivo, usare una delle procedure seguenti.  

   #### <a name="create-a-standard-program"></a>Creare un programma standard  

   1.  Nella pagina **Tipo di programma** della **Creazione guidata pacchetto e programma** selezionare **Programma standard** e fare clic su **Avanti**.     

   2.  Nella pagina **Programma standard**, specificare quanto segue:  

       -   **Nome**: specificare un nome per il programma con un massimo di 50 caratteri.  

           > [!NOTE]  
           >  Il nome del programma deve essere univoco all'interno di un pacchetto. Dopo aver creato un programma, non è possibile modificarne il nome.  

       -   **Riga di comando**: immettere la riga di comando da usare per avviare il programma oppure scegliere **Sfoglia** per selezionare il percorso del file.  

           Se per un nome di file non è specificata l'estensione, Configuration Manager prova a usare com, exe e bat come possibili estensioni.  

            Se il programma viene eseguito in un client, Configuration Manager cerca prima il nome del file della riga di comando all'interno del pacchetto, successivamente cerca nella cartella Windows locale e infine nel *%percorso%* locale. Se il file non può essere trovato, l'esecuzione del programma non riesce.  

       -   **Cartella Esecuzione automatica** (facoltativo): specificare la cartella da cui viene eseguito il programma, con un massimo di 127 caratteri. Questa cartella può essere un percorso assoluto nel client o un percorso relativo alla cartella del punto di distribuzione contenente il pacchetto.

       -   **Esegui**: specificare la modalità di esecuzione del programma nei computer client. Selezionare una delle opzioni seguenti:  

           -   **Normale**: il programma viene eseguito in modalità normale in base alle impostazioni predefinite del sistema e del programma. Questa è la modalità predefinita.  

           -   **Ridotta a icona**: il programma viene eseguito in modalità ridotta a icona nei dispositivi client. Gli utenti potranno seguire l'attività di installazione nell'area di notifica o sulla barra delle applicazioni.  

           -   **Ingrandita**: il programma viene eseguito in modalità ingrandita nei dispositivi client. Gli utenti potranno seguire l'intera l'attività di installazione.  

           -   **Nascosta**: il programma viene eseguito in modalità nascosta nei dispositivi client. Gli utenti non potranno seguire l'attività di installazione.  

       -   **Requisiti per esecuzione programma**: specificare se il programma viene eseguito solo quando un utente ha eseguito l'accesso, quando nessun utente ha eseguito l'accesso o indipendentemente dal fatto che un utente abbia o meno eseguito l'accesso al computer client.  

       -   **Modalità esecuzione**: specificare se il programma viene eseguito con autorizzazioni amministrative o con le autorizzazioni dell'utente che ha eseguito l'accesso.  

       -   **Consenti agli utenti di visualizzare e interagire con l'installazione del programma**: usare questa impostazione, se disponibile, per specificare se consentire agli utenti di interagire con l'installazione del programma. Questa casella di controllo è disponibile solo se sono selezionate le opzioni **Solo se nessun utente è connesso** o **Indipendentemente dalla connessione degli utenti** per **Requisiti per esecuzione programma** e **Esegui con diritti amministrativi** per **Modalità esecuzione**.  

       -   **Modalità unità**: specificare le informazioni sull'esecuzione del programma in rete. Scegliere uno dei valori seguenti:  

           -   **Viene eseguito con nome UNC**: il programma viene eseguito con un nome UNC (Universal Naming Convention). Questa è l'impostazione predefinita.  

           -   **Richiede lettera di unità**: il programma richiede una lettera di unità per specificare un percorso completo. Per questa impostazione, Configuration Manager può usare qualsiasi lettera di unità disponibile nel client.  

           -   **Richiede lettera di unità specifica**: il programma richiede una lettera di unità specifica per indicarne il percorso completo, ad esempio **Z:**. Se la lettera di unità specificata è già usata in un client, il programma non viene eseguito.  

       -   **Riconnettiti al punto di distribuzione all'accesso**: usare questa casella di controllo per indicare se il computer client si riconnette al punto di distribuzione quando l'utente esegue l'accesso. Per impostazione predefinita, questa casella di controllo è deselezionata.  

   3.  Nella pagina **Requisiti** della **Creazione guidata pacchetto e programma** specificare le informazioni seguenti:  

       -   **Esegui prima un altro programma**: usare questa impostazione per identificare un pacchetto e un programma che devono essere eseguiti prima dell'esecuzione del pacchetto e del programma corrente.  

       -   **Requisiti di piattaforma**: selezionare **Questo programma può essere eseguito in qualsiasi piattaforma** o **Questo programma può essere eseguito solo in piattaforme specifiche** e scegliere i sistemi operativi che i client devono eseguire per poter installare il pacchetto e il programma.  

       -   **Spazio su disco stimato**: specificare la quantità di spazio su disco necessaria per l'esecuzione del programma software nel computer. Questo valore può essere specificato come **sconosciuto** (impostazione predefinita) o come un numero intero maggiore o uguale a zero. Se si specifica un valore, è necessario specificare anche l'unità di misura per il valore.  

       -   **Tempo di esecuzione massimo consentito (minuti)**: specifica il tempo massimo previsto dal programma per l'esecuzione nel computer client. Questo valore può essere specificato come **sconosciuto** (impostazione predefinita) o come numero intero maggiore di zero.  

            Per impostazione predefinita, il valore è impostato su 120 minuti.  

           > [!IMPORTANT]  
           >  Se si usano finestre di manutenzione per la raccolta in cui viene eseguito il programma, può verificarsi un conflitto se il valore di **Tempo di esecuzione massimo consentito**  è maggiore della finestra di manutenzione pianificata. Se il tempo di esecuzione massimo è invece impostato su **Sconosciuto**, il programma viene avviato durante la finestra di manutenzione e l'esecuzione prosegue nel modo necessario dopo il termine della finestra di manutenzione. Se l'utente imposta il tempo di esecuzione massimo su una durata specifica maggiore della durata di qualsiasi finestra di manutenzione disponibile, il programma non viene eseguito.  

            Se il valore impostato è **Sconosciuto**, Configuration Manager imposta un limite massimo di esecuzione di 12 ore (720 minuti).  

           > [!NOTE]  
           >  Se il tempo di esecuzione massimo, indipendentemente dal fatto che sia stato impostato dall'utente o che si tratti del valore predefinito, viene superato, Configuration Manager arresta il programma se l'opzione **Esegui con diritti amministrativi** è selezionata e l'opzione **Consenti agli utenti di visualizzare e interagire con l'installazione del programma** non è selezionata.  

   4.  Scegliere **Avanti**.  

   #### <a name="create-a-device-program"></a>Creare un programma di dispositivo  

   1.  Nella pagina **Tipo di programma** della **Creazione guidata pacchetto e programma** selezionare **Programma per dispositivo** e scegliere **Avanti**.  

   2.  Nella pagina **Programma standard** specificare quanto segue:  

       -   **Nome**: specificare un nome per il programma con un massimo di 50 caratteri.  

           > [!NOTE]  
           >  Il nome del programma deve essere univoco all'interno di un pacchetto. Dopo aver creato un programma, non è possibile modificarne il nome.  

       -   **Commento** (facoltativo): specificare un commento per il programma del dispositivo, con un massimo di 127 caratteri.  

       -   **Cartella download**: specificare il nome della cartella nel dispositivo Windows CE in cui verranno archiviati i file di origine del pacchetto. Il valore predefinito è **\Temp\\**.  

       -   **Riga di comando**: immettere la riga di comando da usare per avviare il programma oppure scegliere **Sfoglia** per selezionare il percorso del file.  

       -   **Esegui la riga di comando nella cartella download**: selezionare questa opzione per eseguire il programma dalla cartella di download specificata in precedenza.  

       -   **Esegui la riga di comando da questa cartella**: selezionare questa opzione per specificare una cartella diversa da cui eseguire il programma.  

   3.  Nella pagina **Requisiti**, specificare quanto segue:  

       -   **Spazio su disco stimato**: specificare la quantità di spazio su disco necessaria per il software. Questo valore viene visualizzato agli utenti dei dispositivi mobili prima di installare il programma.  

       -   **Programma download**: specificare le informazioni relative al momento in cui il programma può essere scaricato nei dispositivi mobili. È possibile specificare **Appena possibile**, **Solo su una rete veloce**o **Solo quando un dispositivo è bloccato**.  

       -   **Altri requisiti**: specificare eventuali requisiti aggiuntivi per il programma. I requisiti vengono visualizzati agli utenti prima di installare il software. Ad esempio, è possibile informare gli utenti che è necessario chiudere tutte le altre applicazioni prima di eseguire il programma.  

   4.  Scegliere **Avanti**.  

   7.  Nella pagina **Riepilogo** esaminare le azioni da eseguire e quindi completare la procedura guidata.  

   Verificare che i nuovi pacchetto e programma vengano visualizzati nel nodo **Pacchetti** dell'area di lavoro **Raccolta software**.  

## <a name="create-a-package-and-program-from-a-package-definition-file"></a>Per creare un pacchetto e un programma da un file di definizione del pacchetto  

1. Nella console di Configuration Manager scegliere **Raccolta software**  > **Gestione applicazioni** > **Pacchetti**.  

2. Nel gruppo **Crea** della scheda **Home** scegliere **Crea pacchetto da definizione**.  

3. Nella pagina **Definizione pacchetto** della **Creazione guidata pacchetto da definizione** scegliere un file di definizione del pacchetto esistente oppure selezionare**Sfoglia** per aprirne uno nuovo. Dopo aver specificato un nuovo file di definizione del pacchetto, selezionarlo nell'elenco **Definizione pacchetto** e scegliere **Avanti**.  

4. Nella pagina **File di origine** specificare le informazioni su tutti i file di origine necessari per il pacchetto e per il programma e scegliere **Avanti**.  

5. Se per il pacchetto sono necessari file di origine, nella pagina **Cartella di origine** specificare il percorso da cui devono essere ottenuti i file di origine e scegliere **Avanti**.  

6. Nella pagina **Riepilogo** esaminare le azioni da eseguire e quindi completare la procedura guidata. Il nuovo pacchetto e il nuovo programma vengono visualizzati nel nodo **Pacchetti** dell'area di lavoro **Raccolta software**.  

   Per altre informazioni sui file definizioni del pacchetto, vedere [Informazioni sul formato di file definizioni del pacchetto](/sccm/apps/deploy-use/packages-and-programs#about-the-package-definition-file-format) in questo argomento.  

##  <a name="deploy-packages-and-programs"></a>Distribuire pacchetti e programmi  

1. Nella console di Configuration Manager scegliere **Raccolta software**  > **Gestione applicazioni** > **Pacchetti**.  

2. Selezionare il pacchetto che si vuole distribuire. Nel gruppo **Distribuzione** della scheda **Home** scegliere **Distribuisci**.  

3. Nella pagina **Generale** della **Distribuzione guidata del software** specificare il nome del pacchetto e del programma che si vuole distribuire, la raccolta in cui si vuole distribuire il pacchetto e il programma ed eventuali commenti per la distribuzione.  

    Selezionare **utilizzare gruppi di punti di distribuzione predefiniti associati a questa raccolta** se si desidera archiviare il contenuto del pacchetto nel gruppo di punto di distribuzione predefinito di raccolte. Se la raccolta selezionata non è stata associata a un gruppo di punti di distribuzione, questa opzione non è disponibile.  

4. Nella pagina **Contenuto** scegliere **Aggiungi** e selezionare i punti di distribuzione o i gruppi di punti di distribuzione in cui si vuole distribuire il contenuto associato a questo programma e pacchetto.  

5. Nella pagina **Impostazioni distribuzione** scegliere uno scopo per la distribuzione e specificare le opzioni per i pacchetti di riattivazione e le connessioni a consumo:  

   - **Scopo**: È possibile scegliere tra:  

     -   **Disponibile**: se l'applicazione viene distribuita a un utente, l'utente visualizza il pacchetto e il programma pubblicati nel Catalogo applicazioni e può richiederli appositamente. Se il pacchetto e il programma vengono distribuiti in un dispositivo, vengono visualizzati in Software Center e l'utente può installarli su richiesta.  

     -   **Richiesto**: il pacchetto e il programma vengono distribuiti automaticamente in base alla pianificazione configurata. Tuttavia, un utente può tenere traccia dello stato di distribuzione del pacchetto e del programma e installarli prima della scadenza usando Software Center.  

     > [!NOTE]
     >  Se più utenti hanno eseguito l'accesso al dispositivo, le distribuzioni di sequenze di attività e di pacchetti potrebbero non comparire in Software Center.

   - **Invia pacchetti di riattivazione**: se lo scopo della distribuzione è impostato su **Richiesto** e questa opzione è selezionata, ai computer viene inviato un pacchetto di riattivazione prima dell'installazione della distribuzione, per riattivare il computer dalla sospensione alla scadenza dell'installazione. Prima di poter utilizzare questa opzione, i computer devono essere configurati per la riattivazione LAN.  

   - **Consente a tutti i client che utilizzano una connessione di rete a consumo di scaricare il contenuto una volta raggiunta la scadenza dell'installazione. Se si abilita questa opzione, potrebbe essere addebitato un costo aggiuntivo**: selezionare questa opzione se richiesto.  

   > [!NOTE]  
   >  L'opzione **Pre-distribuisci il software nel dispositivo primario dell'utente** non è disponibile durante la distribuzione di un pacchetto e di un programma.  

6. Nella pagina **Pianificazione** configurare la data e l'ora in cui pacchetto e programma verranno distribuiti o resi disponibili per i dispositivi client.  

    Le opzioni presenti in questa pagina varieranno a seconda che l'azione di distribuzione sia impostata su **Disponibile** o **Richiesto**.  

7. Se lo scopo della distribuzione è impostato su **Richiesto**, configurare il comportamento di riesecuzione per il programma nell'elenco a discesa **Riesegui comportamento**. È possibile scegliere una delle opzioni seguenti:  


   |             Riesegui comportamento             |                                                                                                                        Altre informazioni                                                                                                                        |
   |----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |      Non rieseguire mai un programma distribuito      |                                                                      Il programma non verrà rieseguito nel client, anche se l'esecuzione originale non è riuscita o i file di programma sono stati modificati.                                                                      |
   |          Riesegui sempre un programma          |   Il programma viene sempre rieseguito nel client quando è pianificata la distribuzione, anche se è già stato eseguito correttamente. Questa impostazione può essere utile quando si usano distribuzioni ricorrenti in cui il programma viene aggiornato, ad esempio con un software antivirus.    |
   |    Riesegui se il tentativo precedente non è riuscito    |                                                                              Il programma viene rieseguito quando è pianificata la distribuzione ,solo se l'esecuzione non è riuscita durante il tentativo precedente.                                                                              |
   | Riesegui se il tentativo precedente è riuscito | Il programma viene rieseguito solo se è già stato eseguito correttamente nel client. Questa impostazione è utile quando si usano avvisi ricorrenti in cui il programma viene aggiornato regolarmente e ogni aggiornamento richiede l'installazione corretta dell'aggiornamento precedente. |


8. Nella pagina **Esperienza utente** specificare le informazioni seguenti:  

    -   **Consenti agli utenti di eseguire il programma indipendentemente dalle assegnazioni**: se questa opzione è abilitata, gli utenti possono installare il software da Software Center indipendentemente da qualsiasi intervallo di installazione pianificato.  

    -   **Installazione software**: consente al software di essere installato al di fuori di tutte le finestre di manutenzione configurate.  

    -   **Riavvio del sistema (se necessario per completare l'installazione)**: se l'installazione del software richiede un riavvio del dispositivo per il completamento, questa opzione consente di eseguire il riavvio al di fuori di qualsiasi finestra di manutenzione configurata.  

    -   **Embedded devices** (Dispositivi con Embedded): quando si distribuiscono pacchetti e programmi in dispositivi con Windows Embedded con filtro di scrittura abilitato, è possibile specificare di installare i pacchetti e i programmi nella sovrapposizione temporanea ed eseguire il commit delle modifiche successivamente. In alternativa, il commit delle modifiche viene eseguito alla scadenza dell'installazione o all'interno una finestra di manutenzione. Quando si esegue il commit delle modifiche alla scadenza dell'installazione o all'interno di una finestra di manutenzione, è necessario il riavvio per salvare le modifiche nel dispositivo in modo permanente.  

        > [!NOTE]  
        >  Quando si distribuisce un pacchetto o un programma in un dispositivo con Windows Embedded, assicurarsi che il dispositivo sia membro di una raccolta a cui è associata una finestra di manutenzione configurata. Per altre informazioni sull'uso delle finestre di manutenzione quando si distribuiscono pacchetti e programmi a dispositivi con Windows Embedded, vedere [Creazione di applicazioni Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md).  

9. Nella pagina **Punti di distribuzione** specificare le informazioni seguenti:  

    -   **Opzioni di distribuzione**: specificare le azioni che un client deve intraprendere per eseguire il contenuto del programma. È possibile specificare il comportamento da adottare quando il client si trova in un limite di rete veloce, lento o non affidabile.  

    -   **Consenti ai client di condividere il contenuto con altri client nella stessa subnet**: selezionare questa opzione per ridurre il carico sulla rete consentendo ai client di scaricare contenuto da altri client della rete che lo abbiano già scaricato e memorizzato nella cache. Questa opzione si avvale di Windows BranchCache e può essere usata in computer che eseguono Windows Vista SP2 e versioni successive.  

    -   **Consenti ai client di utilizzare un percorso origine di fallback per il contenuto**:  

        -  **Versioni precedenti alla 1610**: è possibile selezionare la casella di controllo **Consenti percorso origine di fallback** per il contenuto per consentire ai client esterni a questi gruppi di limiti di eseguire il fallback e usare il punto di distribuzione come percorso di origine per il contenuto in assenza di altri punti di distribuzione disponibili.

        - **Versione 1610 e successive**: non è più possibile configurare l'opzione **Consenti percorso origine di fallback per il contenuto**.  È invece possibile configurare relazioni tra gruppi di limiti per determinare quando un client può iniziare la ricerca di gruppi di limiti aggiuntivi per un percorso di origine del contenuto valido.

10. Nella pagina **Riepilogo** esaminare le azioni da eseguire e quindi completare la procedura guidata.  

     È possibile visualizzare la distribuzione nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio** e nel riquadro dei dettagli della scheda di distribuzione del pacchetto quando si seleziona la distribuzione. Per altre informazioni, vedere [Monitorare pacchetti e programmi](/sccm/apps/deploy-use/packages-and-programs#monitor-packages-and-programs) in questo argomento.  

> [!IMPORTANT]  
>  Se è stata configurata l'opzione **Esegui programma dal punto di distribuzione** nella pagina **Punti di distribuzione** della **Distribuzione guidata del software**, non deselezionare l'opzione **Copia il contenuto del pacchetto in una condivisione pacchetto nei punti di distribuzione** perché così facendo il pacchetto non sarà più disponibile per l'esecuzione dai punti di distribuzione.  

##  <a name="monitor-packages-and-programs"></a>Monitorare pacchetti e programmi  
 Per monitorare le distribuzioni di pacchetti e programmi, seguire le stesse procedure usate per monitorare le applicazioni, come descritto in [Monitorare le applicazioni](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

 I pacchetti e i programmi includono anche alcuni report predefiniti, che consentono di monitorare le informazioni sullo stato di distribuzione di pacchetti e programmi. Tali report dispongono della categoria report di **distribuzione Software-pacchetti e programmi** e **distribuzione Software-pacchetto e programma lo stato di distribuzione**.  

 Per altre informazioni sulle modalità di configurazione della creazione di report in Configuration Manager, vedere [Creazione di report in System Center Configuration Manager](../../core/servers/manage/reporting.md).  

##  <a name="manage-packages-and-programs"></a>Gestire pacchetti e programmi  
 Nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni**, scegliere **Pacchetti**, selezionare il pacchetto che si vuole gestire e scegliere un'attività di gestione tra quelle contenute nella tabella seguente:  

|Attività|Altre informazioni|  
|----------|----------------------|  
|**Crea file di contenuto di pre-installazione**|Apre la **Creazione guidata file di contenuto pre-installazione**, che consente di creare un file che include il contenuto del pacchetto che può essere importato manualmente in un altro sito. Questa impostazione è utile nei casi in cui è disponibile larghezza di banda ridotta tra il server del sito e il punto di distribuzione.|  
|**Crea programma**|Apre la **Creazione guidata programma**, che consente di creare un nuovo programma per il pacchetto.|  
|**Export**|Apre l'**Esportazione guidata del pacchetto**, che consente di esportare il pacchetto selezionato e il suo contenuto in un file.<br /><br /> Per informazioni su come importare pacchetti e programmi, vedere [Creare pacchetti e programmi ](/sccm/apps/deploy-use/packages-and-programs#create-packages-and-programs) in questo argomento.|  
|**Distribuzione**|Apre la **Distribuzione guidata del software**, che consente di distribuire il pacchetto e il programma selezionati in una raccolta. Per altre informazioni, vedere [Distribuire pacchetti e programmi](/sccm/apps/deploy-use/packages-and-programs#deploy-packages-and-programs) in questo argomento.|  
|**Distribuisci contenuto**|Apre la **Distribuzione guidata contenuto**, che consente di inviare il contenuto associato al pacchetto e al programma a punti di distribuzione o gruppi di punti di distribuzione selezionati.|  
|**Aggiorna punti di distribuzione**|Aggiorna i punti di distribuzione con il contenuto più recente per il pacchetto e il programma selezionati.|  

##  <a name="about-the-package-definition-file-format"></a>Informazioni sul formato di file definizioni del pacchetto  
 I file definizioni del pacchetto sono script che è possibile usare per automatizzare la creazione di pacchetti e programmi con Configuration Manager. Specificano tutte le informazioni necessarie a Configuration Manager per creare un pacchetto e un programma, ad eccezione del percorso dei file origine del pacchetto. Ogni file di definizione del pacchetto è un file di testo ASCII o UTF-8 con estensione ini, che contiene le sezioni descritte di seguito:  

###  <a name="pdf"></a>[PDF]  
 Questa sezione identifica il file come file di definizione del pacchetto. Contiene le informazioni seguenti:  

-   **Versione**: specificare la versione del formato del file di definizione del pacchetto usato dal file. Corrisponde alla versione di System Management Server (SMS) o Configuration Manager per cui è stato scritto. Questa voce è necessaria.  

###  <a name="package-definition"></a>[Package Definition]  
 Specificare le proprietà del pacchetto e del programma. Contiene le informazioni seguenti:  

-   **Nome**: nome del pacchetto, con un massimo di 50 caratteri.  

-   **Versione** (facoltativo): versione del pacchetto, con un massimo di 32 caratteri.  

-   **Icona** (facoltativo): file contenente l'icona da usare per il pacchetto. Se specificata, questa icona sostituisce quella del pacchetto predefinita nella console di Configuration Manager.

-   **Server di pubblicazione**: server di pubblicazione del pacchetto, con un massimo di 32 caratteri.

-   **Lingua**: versione della lingua del pacchetto, con un massimo di 32 caratteri.

-   **Commento** (facoltativo): commento sul pacchetto, con un massimo di 127 caratteri.

-   **ContainsNoFiles**: questa voce indica se al pacchetto è associata un'origine.  

-   **Programmi**: programmi definiti per il pacchetto. Ogni nome del programma corrisponde a un **[programma]** sezione in questo file di definizione del pacchetto.  

     Esempio:  

     `Programs=Typical, Custom, Uninstall`  

-   **MIFFileName**: nome del file MIF (Management Information) che contiene lo stato del pacchetto, con un massimo di 50 caratteri.  

-   **MIFName**: nome del pacchetto (per la corrispondenza MIF), con un massimo di 50 caratteri.  

-   **MIFVersion**: numero di versione del pacchetto (per la corrispondenza MIF), con un massimo di 32 caratteri.  

-   **MIFPublisher**: autore del software del pacchetto (per la corrispondenza MIF), con un massimo di 32 caratteri.  

###  <a name="program"></a>[Program]  
 Per ogni programma specificato alla voce **Programmi** nella sezione **[Package Definition]**, il file di definizione del pacchetto deve includere una sezione [Program] che definisce tale programma. Ogni sezione Program fornisce le informazioni seguenti:  

-   **Nome**: nome del programma, con un massimo di 50 caratteri. Questa voce deve essere univoca all'interno di un pacchetto. Questo nome viene utilizzato quando si definiscono gli annunci. Nei computer client, viene visualizzato il nome del programma **Esegui programmi annunciati** nel Pannello di controllo.  

-   **Icona** (facoltativo): specificare il file contenente l'icona da usare per il programma. Se specificata, questa icona sostituisce l'icona di programma predefinita nella console di Configuration Manager e viene visualizzata nei computer client quando il programma è annunciato.

-   **Commento** (facoltativo): commento sul programma, con un massimo di 127 caratteri.

-   **CommandLine**: specificare la riga di comando per il programma, con un massimo di 127 caratteri. Il comando è relativo alla cartella di origine del pacchetto.

-   **StartIn**: specificare la cartella di lavoro per il programma, con un massimo di 127 caratteri. Questa voce può essere un percorso assoluto nel computer client o un percorso relativo della cartella di origine del pacchetto.

-   **Esegui**: specificare la modalità in cui viene eseguito il programma. È possibile specificare **ridotta a icona**, **ingrandita**, o **Hidden**. Se questa voce non è inclusa, il programma viene eseguito in modalità normale.  

-   **AfterRunning**: specificare qualsiasi azione speciale da eseguire dopo che il programma è stato completato correttamente. Le opzioni disponibili sono **SMSRestart**, **ProgramRestart**, o **SMSLogoff**. Se questa voce non è inclusa, il programma non esegue azioni speciali.  

-   **EstimatedDiskSpace**: specificare la quantità di spazio su disco necessaria per l'esecuzione del programma software nel computer. Questo valore può essere specificato come **sconosciuto** (impostazione predefinita) o come un numero intero maggiore o uguale a zero. Se viene specificato un valore, anche le unità per il valore devono essere specificate.  

     Esempio:  

     `EstimatedDiskSpace=38MB`  

-   **EstimatedRunTime**: specificare la durata stimata (in minuti) dell'esecuzione del programma nel computer client. Questo valore può essere specificato come **sconosciuto** (impostazione predefinita) o come numero intero maggiore di zero.  

     Esempio:  

     `EstimatedRunTime=25`  

-   **SupportedClients**: specificare i processori e i sistemi operativi in cui viene eseguito il programma. Le piattaforme specificate devono essere separate da virgole. Se questa voce non è inclusa, il controllo piattaforma supportata viene disabilitato per questo programma.  

-   **SupportedClientMinVersionX**, **SupportedClientMaxVersionX**: specificare l'intervallo tra numero di versione iniziale e finale per i sistemi operativi specificati alla voce **SupportedClients**.  

     Esempio:  

    ```  
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999   
    ```  

-   **AdditionalProgramRequirements** (facoltativo): specificare qualsiasi altro requisito o informazione per i computer client, con un massimo di 127 caratteri.

-   **CanRunWhen**: specificare lo stato dell'utente necessario per l'esecuzione del programma nel computer client. I valori disponibili sono **UserLoggedOn**, **NoUserLoggedOn**, o **AnyUserStatus**. Il valore predefinito è **UserLoggedOn**.  

-   **UserInputRequired**: specificare se il programma richiede interazione con l'utente. I valori disponibili sono **True** o **False**. Il valore predefinito è **True**. Questa voce è impostata su **False** se **CanRunWhen** non è impostata su **UserLoggedOn**.  

-   **AdminRightsRequired**: specificare se per l'esecuzione del programma è necessario immettere credenziali amministrative nel computer. I valori disponibili sono **True** o **False**. Il valore predefinito è **False**. Questa voce è impostata su **True** se **CanRunWhen** non è impostata su **UserLoggedOn**.  

-   **UseInstallAccount**: specificare se il programma usa l'account di installazione software client per l'esecuzione nei computer client. Per impostazione predefinita, questo valore è **False**. Questo valore corrisponde anche **False** se **CanRunWhen** è impostato su **UserLoggedOn**.  

-   **DriveLetterConnection**: specificare se il programma richiede una connessione con lettera di unità per i file del pacchetto che si trovano nel punto di distribuzione. È possibile specificare **True** o **False**. Il valore predefinito è **False**, che consente al programma di usare una connessione UNC (Universal Naming Convention). Quando questo valore è impostato su **True**, viene usata la lettera di unità successiva disponibile, a partire da Z e andando a ritroso.  

-   **SpecifyDrive** (facoltativo): specificare una lettera di unità necessaria al programma per connettersi ai file del pacchetto nel punto di distribuzione. Questa impostazione forza l'uso della lettera di unità specificata per le connessioni client ai punti di distribuzione.

-   **ReconnectDriveAtLogon**: specificare se il computer si riconnette al punto di distribuzione quando l'utente esegue l'accesso. I valori disponibili sono **True** o **False**. Il valore predefinito è **False**.  

-   **DependentProgram**: specificare un programma in questo pacchetto che deve essere eseguito prima del programma corrente. Questa voce usa il formato **DependentProgram**=<**NomeProgramma>**, dove **<NomeProgramma\>** corrisponde alla voce **Name** per il programma nel file di definizione del pacchetto. Se non sono presenti programmi dipendenti, lasciare vuota questa voce.  

     Esempio:  

     DependentProgram = Admin  
    DependentProgram =  

-   **Assignment**: specificare come il programma viene assegnato agli utenti. Questo valore può essere: **FirstUser** (solo il primo utente che accede al client esegue il programma) oppure **EveryUser** (chiunque acceda al client può eseguire il programma). Quando **CanRunWhen** non è impostata su **UserLoggedOn**, questa voce è impostata su **FirstUser**.  

-   **Disabled**: specificare se il programma può essere annunciato ai client. I valori disponibili sono **True** o **False**. Il valore predefinito è **False**.  

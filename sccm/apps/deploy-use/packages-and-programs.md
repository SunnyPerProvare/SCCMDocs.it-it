---
title: Pacchetti e programmi
titleSuffix: Configuration Manager
description: Supportare le distribuzioni che usano pacchetti e programmi legacy con Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: caad0507-9913-415a-b13d-d36f8f0a1b80
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 11af81b3da1c26fb83e96e5deda108880461333c
ms.sourcegitcommit: 72faa1266b31849ce1a23d661a1620b01e94f517
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/26/2019
ms.locfileid: "68534772"
---
# <a name="packages-and-programs-in-configuration-manager"></a>Pacchetti e programmi in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Configuration Manager continua a supportare pacchetti e programmi usati in Configuration Manager 2007. Una distribuzione che usa pacchetti e programmi può essere più adatta rispetto a un'applicazione quando si distribuisce uno degli strumenti o degli script seguenti:  

- Strumenti di amministrazione che non installano un'applicazione in un computer
- Script occasionali che non devono essere monitorati continuamente  
- Script eseguiti in base a una pianificazione ricorrente e che non possono usare la valutazione globale

> [!TIP]  
> È consigliabile usare la funzionalità [Script](/sccm/apps/deploy-use/create-deploy-scripts) nella console di Configuration Manager. Per gli scenari precedenti, l'uso di script potrebbe essere una soluzione migliore rispetto all'uso di pacchetti e programmi.

Quando si esegue la migrazione di pacchetti da una versione precedente di Configuration Manager, è possibile distribuirli nella gerarchia di Configuration Manager. Al termine della migrazione, i pacchetti vengono visualizzati nel nodo **Pacchetti** dell'area di lavoro **Raccolta software** .

È possibile modificare e distribuire questi pacchetti nello stesso modo dei casi in cui è stata usata la distribuzione del software. L'**Importazione guidata da definizione** rimane in Configuration Manager per importare pacchetti legacy. Gli annunci vengono convertiti in distribuzioni quando si esegue la migrazione da Configuration Manager 2007 a una gerarchia di Configuration Manager.  

> [!NOTE]  
> Usare Package Conversion Manager per convertire i pacchetti e i programmi in applicazioni Configuration Manager.  
>
> A partire dalla versione 1806, Package Conversion Manager è integrato con Configuration Manager. Per altre informazioni, vedere [Package Conversion Manager](/sccm/apps/pcm/package-conversion-manager).  

I pacchetti possono usare alcune nuove funzionalità di Configuration Manager, inclusi i gruppi di punti di distribuzione e il monitoraggio. Non è possibile distribuire applicazioni Microsoft Application Virtualization (App-V) con pacchetti e programmi in Configuration Manager. Per distribuire applicazioni virtuali, crearle come applicazioni di Configuration Manager. Per ulteriori informazioni, vedere [Deploy App-V Virtual Applications](/sccm/apps/get-started/deploying-app-v-virtual-applications).  


## <a name="create-a-package-and-program"></a>Creare un pacchetto e un programma

### <a name="use-the-create-package-and-program-wizard"></a>Usare la Creazione guidata pacchetto e programma

1. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere **Gestione applicazioni** e selezionare il nodo **Pacchetti**.  

2. Nel gruppo **Crea** della scheda **Home** della barra multifunzione scegliere **Crea pacchetto**.  

3. Nel **pacchetto** di pagina il **Creazione guidata pacchetto e programma**, specificare le seguenti informazioni:  

    - **Nome**: specificare un nome per il pacchetto con un massimo di 50 caratteri.  

    - **Descrizione**: specificare una descrizione per il pacchetto con un massimo di 128 caratteri.  

    - **Produttore** (facoltativo): specificare un nome produttore per identificare il pacchetto nella console di Configuration Manager. Il nome non può contenere più di 32 caratteri.

    - **Lingua** (facoltativo): specificare la lingua del pacchetto con un massimo di 32 caratteri.  

    - **Versione** (facoltativo): specificare un numero di versione per il pacchetto con un massimo di 32 caratteri.

    - **Questo pacchetto contiene file di origine**: questa impostazione indica se il pacchetto richiede che nei dispositivi client siano presenti file di origine. Per impostazione predefinita, la procedura guidata non abilita questa opzione e Configuration Manager non usa i punti di distribuzione per il pacchetto. Quando si seleziona questa opzione, specificare il contenuto del pacchetto da distribuire ai punti di distribuzione.  

    - **Cartella di origine**: se il pacchetto contiene file di origine, scegliere **Sfoglia** per aprire la finestra di dialogo **Imposta cartella di origine** e specificare il percorso dei file di origine per il pacchetto.  

        > [!NOTE]  
        > L'account computer del server del sito deve avere autorizzazioni di accesso in lettura alla cartella specificata.  

    - A partire dalla versione 1906, se si vuole memorizzare anticipatamente il contenuto nella cache in un client, specificare **Architettura** e **Lingua** del pacchetto. Per altre informazioni, vedere [Configurare la pre-cache del contenuto](/sccm/osd/deploy-use/configure-precache-content).<!--4224642-->  

4. Nella pagina **Tipo di programma** della **Creazione guidata pacchetto e programma** selezionare il tipo di programma da creare e fare clic su **Avanti**. È possibile creare un programma per un [computer](#create-a-standard-program) o un [dispositivo](#create-a-device-program) oppure ignorare questo passaggio e creare un programma in un secondo momento.  

    > [!TIP]  
    > Per creare un nuovo programma per un pacchetto esistente, selezionare prima il pacchetto. Nel gruppo **Pacchetto** della scheda **Home** scegliere **Crea programma** per aprire la **Creazione guidata programma**.  

#### <a name="create-a-standard-program"></a>Creare un programma standard

1. Nella pagina **Tipo di programma** della **Creazione guidata pacchetto e programma** selezionare **Programma standard** e fare clic su **Avanti**.  

2. Nella pagina **Programma standard**, specificare quanto segue:  

    - **Nome:** Specificare un nome per il programma con un massimo di 50 caratteri.  

        > [!NOTE]  
        > Il nome del programma deve essere univoco all'interno di un pacchetto. Dopo aver creato un programma, non è possibile modificarne il nome.  

    - **Riga di comando**: immettere la riga di comando da usare per avviare il programma oppure scegliere **Sfoglia** per selezionare il percorso del file.  

        Se non si specifica un'estensione per un nome di file, Configuration Manager tenta di usare. com,. exe e. bat come possibili estensioni.  

        Quando il client esegue il programma, Configuration Manager cerca il file nei percorsi seguenti:

        - All'interno del pacchetto
        - Cartella locale di Windows
        - % *Path* % locale

        Se il file non viene trovato, il programma ha esito negativo.  

    - **Cartella Esecuzione automatica** (facoltativo): specificare la cartella da cui viene eseguito il programma, con un massimo di 127 caratteri. Questa cartella può corrispondere a un percorso assoluto nel client. Può anche essere un percorso relativo alla cartella del punto di distribuzione contenente il pacchetto.

    - **Esegui**: specificare la modalità di esecuzione del programma nei computer client. Selezionare una delle opzioni seguenti:  

        - **Normale**: il programma viene eseguito in modalità normale in base alle impostazioni predefinite del sistema e del programma. Questa è la modalità predefinita.  

        - **Ridotta a icona**: il programma viene eseguito in modalità ridotta a icona nei dispositivi client. Gli utenti potranno seguire l'attività di installazione nell'area di notifica o sulla barra delle applicazioni.  

        - **Ingrandita**: il programma viene eseguito in modalità ingrandita nei dispositivi client. Gli utenti potranno seguire l'intera l'attività di installazione.  

        - **Nascosta**: il programma viene eseguito in modalità nascosta nei dispositivi client. Gli utenti non potranno seguire l'attività di installazione.  

    - **Requisiti per esecuzione programma**: specificare se il programma viene eseguito solo quando un utente ha eseguito l'accesso, quando nessun utente ha eseguito l'accesso o indipendentemente dal fatto che un utente abbia o meno eseguito l'accesso al computer client.  

    - **Modalità esecuzione**: specificare se il programma viene eseguito con autorizzazioni amministrative o con le autorizzazioni dell'utente che ha eseguito l'accesso.  

    - **Consenti agli utenti di visualizzare e interagire con l'installazione del programma**: usare questa impostazione, se disponibile, per specificare se consentire agli utenti di interagire con l'installazione del programma. Questa opzione è disponibile solo se vengono soddisfatte le condizioni seguenti:

        - L'impostazione del **programma può essere eseguita** **solo quando nessun utente è connesso** o **se un utente è connesso**
        - L'impostazione della **modalità di esecuzione** deve essere **eseguita con diritti amministrativi**  

    - **Modalità unità**: specificare le informazioni sull'esecuzione del programma in rete. Scegliere una delle seguenti opzioni:  

        - **Viene eseguito con nome UNC**: il programma viene eseguito con un nome UNC (Universal Naming Convention). È l'impostazione predefinita.  

        - **Richiede lettera di unità**: il programma richiede una lettera di unità per specificare un percorso completo. Per questa impostazione, Configuration Manager può usare qualsiasi lettera di unità disponibile nel client.  

        - **Richiede lettera di unità specifica**: il programma richiede una lettera di unità specifica, che è necessario specificare per indicarne il percorso completo. Ad esempio, **Z:** . Se il client sta già usando la lettera di unità specificata, il programma non viene eseguito.  

    - **Riconnettiti al punto di distribuzione all'accesso**: consente di indicare se il client deve riconnettersi al punto di distribuzione quando l'utente esegue l'accesso. Per impostazione predefinita, la procedura guidata non abilita questa opzione.

3. Nella pagina **Requisiti** della **Creazione guidata pacchetto e programma** specificare le informazioni seguenti:  

    - **Esegui prima un altro programma**: consente di identificare un pacchetto e un programma da eseguire prima dell'esecuzione del pacchetto e del programma correnti.  

    - **Requisiti della piattaforma**: selezionare **questo programma può essere eseguito in qualsiasi piattaforma** o **questo programma può essere eseguito solo su piattaforme specifiche**. Quindi scegliere le versioni del sistema operativo che i client devono avere per installare il pacchetto e il programma.  

    - **Spazio su disco stimato**: specifica la quantità di spazio su disco necessaria per l'esecuzione del programma nel computer. L'impostazione predefinita è **Sconosciuto**. Se necessario, specificare un numero intero maggiore o uguale a zero. Se si imposta un valore, selezionare anche unità per il valore.  

    - **Tempo di esecuzione massimo consentito (minuti)** : specificare la durata massima di esecuzione prevista per il programma nel computer client. Il valore predefinito è **120** minuti. Usare solo numeri interi maggiori di zero.  

        > [!IMPORTANT]  
        > Se si utilizzano finestre di manutenzione nella stessa raccolta in cui si distribuisce il programma, è possibile che si verifichi un conflitto se il **tempo di esecuzione massimo consentito** è superiore alla finestra di manutenzione pianificata. Se il tempo di esecuzione massimo è impostato su **sconosciuto**, l'esecuzione del programma viene avviata durante la finestra di manutenzione. Quindi continua a funzionare in base alle esigenze dopo la chiusura della finestra di manutenzione. Se si imposta il tempo di esecuzione massimo su un periodo specifico maggiore della lunghezza di qualsiasi finestra di manutenzione disponibile, il client non esegue il programma.  

        Se si imposta questo valore su **Sconosciuto**, Configuration Manager imposta il limite massimo di esecuzione su 12 ore (720 minuti).  

        > [!NOTE]  
        > Se il programma supera il tempo di esecuzione massimo, Configuration Manager lo arresta se vengono soddisfatte le condizioni seguenti:
        >
        > - Abilitare l'opzione per l' **esecuzione con diritti amministrativi**
        > - Non è possibile abilitare l'opzione per **consentire agli utenti di visualizzare e interagire con l'installazione del programma**  

#### <a name="create-a-device-program"></a>Creare un programma di dispositivo  

1. Nella pagina **Tipo di programma** della **Creazione guidata pacchetto e programma** selezionare **Programma per dispositivo** e scegliere **Avanti**.  

2. Nella pagina **Programma per dispositivo** specificare le impostazioni seguenti:  

    - **Nome**: specificare un nome per il programma con un massimo di 50 caratteri.  

        > [!NOTE]  
        > Il nome del programma deve essere univoco all'interno di un pacchetto. Dopo aver creato un programma, non è possibile modificarne il nome.  

    - **Commento** (facoltativo): specificare un commento per il programma del dispositivo con un massimo di 127 caratteri.  

    - **Cartella di download**: specificare il nome della cartella nel dispositivo in cui vengono archiviati i file di origine del pacchetto. Il valore predefinito è `\Temp\`.  

    - **Riga di comando**: immettere la riga di comando da usare per avviare il programma. Per passare al percorso del file, scegliere **Sfoglia**.  

    - **Esegui la riga di comando nella cartella download**: selezionare questa opzione per eseguire il programma dalla cartella di download.  

    - **Esegui la riga di comando da questa cartella**: selezionare questa opzione per specificare una cartella diversa da cui eseguire il programma.  

3. Nella pagina **Requisiti** specificare le impostazioni seguenti:  

    - **Spazio su disco stimato**: specificare la quantità di spazio su disco necessaria per il software. Il client Visualizza questo valore sugli utenti dei dispositivi mobili prima di installare il programma.  

    - **Scarica programma**: specificare le informazioni relative al momento in cui il dispositivo mobile può scaricare il programma. È possibile specificare **Appena possibile**, **Solo su una rete veloce**o **Solo quando un dispositivo è bloccato**.  

    - **Altri requisiti**: specificare eventuali requisiti aggiuntivi per il programma. Gli utenti visualizzano questi requisiti prima di installare il software. Ad esempio, è possibile informare gli utenti che è necessario chiudere tutte le altre applicazioni prima di eseguire il programma.  

## <a name="deploy-packages-and-programs"></a>Distribuire pacchetti e programmi  

1. Nella console di Configuration Manager passare all'area di lavoro **Raccolta software**, espandere **Gestione applicazioni** e selezionare il nodo **Pacchetti**.  

2. Selezionare il pacchetto che si vuole distribuire. Nella scheda **Home** della barra multifunzione scegliere **Distribuisci** nel gruppo **Distribuzione**.  

3. Nella pagina **generale** della **distribuzione guidata del software**specificare il nome del pacchetto e del programma che si desidera distribuire. Selezionare la raccolta in cui si desidera distribuire il pacchetto e il programma ed eventuali commenti facoltativi.  

    Per archiviare il contenuto del pacchetto nel gruppo di punti di distribuzione predefinito della raccolta, selezionare **Utilizza gruppi di punti di distribuzione predefiniti associati a questa raccolta**. Se la raccolta non è stata associata a un gruppo di punti di distribuzione, questa opzione non è disponibile.  

4. Nella pagina **contenuto** scegliere **Aggiungi**. Selezionare i punti di distribuzione o i gruppi di punti di distribuzione a cui si desidera distribuire il contenuto per il pacchetto e il programma.  

5. Nella pagina **Impostazioni distribuzione** configurare le impostazioni seguenti:  

    - **Scopo**: scegliere una della seguenti opzioni:

        - **Disponibile**: l'utente Visualizza il pacchetto e il programma pubblicati in Software Center e può installarlo su richiesta.  

        - **Richiesto**: il pacchetto e il programma vengono distribuiti automaticamente in base alla pianificazione configurata. In Software Center è possibile tenere traccia dello stato di distribuzione e installarlo prima della scadenza.  

        > [!NOTE]
        > Se più utenti hanno eseguito l'accesso al dispositivo, le distribuzioni di sequenze di attività e di pacchetti potrebbero non comparire in Software Center.

    - **Invia pacchetti**di riattivazione: se lo scopo della distribuzione è impostato su **richiesto** e si seleziona questa opzione, il sito invia prima di tutto un pacchetto di riattivazione ai computer al momento della scadenza dell'installazione. Prima di poter usare questa opzione, configurare i computer per riattivazione LAN. Per altre informazioni, vedere [Come configurare la riattivazione LAN](/sccm/core/clients/deploy/configure-wake-on-lan).  

    - **Consente a tutti i client che usano una connessione di rete a consumo di scaricare il contenuto una volta raggiunta la scadenza dell'installazione. Se si abilita questa opzione, potrebbe essere addebitato un costo aggiuntivo**  

    > [!NOTE]  
    > Durante la distribuzione di un pacchetto e di un programma, l'opzione **Pre-distribuisci il software nel dispositivo primario dell'utente** non è disponibile.  

6. Nella pagina **pianificazione** configurare quando distribuire il pacchetto e il programma nei dispositivi client.  

    Le opzioni presenti in questa pagina variano a seconda che l'azione di distribuzione sia impostata su **Disponibile** o **Richiesto**.  

    Per le distribuzioni **richieste** , configurare il comportamento di riesecuzione per il programma dal menu a discesa **Riesegui comportamento** . È possibile scegliere una delle opzioni seguenti:  

    | Riesegui comportamento | Descrizione |
    |----------------|-------------|
    | **Non rieseguire mai un programma distribuito** | Il client non eseguirà di nuovo il programma. Questo comportamento si verifica anche se il programma non è stato originariamente superato o se i file di programma sono stati modificati. |
    | **Riesegui sempre un programma** | Il client riesegue sempre il programma quando la distribuzione è pianificata. Questo comportamento si verifica anche se il programma è già stato eseguito correttamente. È utile con distribuzioni ricorrenti quando si aggiorna il programma. |
    | **Riesegui se il tentativo precedente non è riuscito** | Il client riesegue il programma quando è pianificata la distribuzione solo se il tentativo di esecuzione precedente ha avuto esito negativo. |
    | **Riesegui se il tentativo precedente è riuscito** | Il client riesegue il programma solo se l'ha già eseguito correttamente nel client. Questo comportamento è utile con le distribuzioni ricorrenti quando si aggiorna periodicamente il programma e ogni aggiornamento richiede l'installazione corretta dell'aggiornamento precedente. |

7. Nella pagina **Esperienza utente** specificare le informazioni seguenti:  

    - **Consenti agli utenti di eseguire il programma indipendentemente dalle assegnazioni**: gli utenti possono installare il software da Software Center indipendentemente da qualsiasi orario di installazione pianificato.  

    - **Installazione software**: permette l'installazione del software al di fuori di qualsiasi finestra di manutenzione configurata.  

    - **Riavvio del sistema (se richiesto per completare l'installazione)** : se per completare l'installazione del software è necessario il riavvio del dispositivo, questa opzione consente di eseguire il riavvio al di fuori di qualsiasi finestra di manutenzione configurata.  

    - **Embedded devices** (Dispositivi con Embedded): quando si distribuiscono pacchetti e programmi in dispositivi con Windows Embedded con filtro di scrittura abilitato, è possibile specificare di installare i pacchetti e i programmi nella sovrapposizione temporanea ed eseguire il commit delle modifiche successivamente. In alternativa, eseguire il commit delle modifiche alla scadenza dell'installazione o all'interno una finestra di manutenzione. Quando si esegue il commit delle modifiche alla scadenza dell'installazione o all'interno di una finestra di manutenzione, è necessario il riavvio per salvare le modifiche nel dispositivo in modo permanente.  

        > [!NOTE]  
        > Quando si distribuisce un pacchetto o un programma in un dispositivo con Windows Embedded, assicurarsi che il dispositivo sia membro di una raccolta a cui è associata una finestra di manutenzione configurata. Per altre informazioni sull'uso delle finestre di manutenzione quando si distribuiscono pacchetti e programmi a dispositivi con Windows Embedded, vedere [Creazione di applicazioni Windows Embedded](/sccm/apps/get-started/creating-windows-embedded-applications).  

8. Nella pagina **Punti di distribuzione** specificare le informazioni seguenti:  

    - **Opzioni di distribuzione**: specificare l'azione che un client utilizza un punto di distribuzione nel gruppo di limiti corrente. Selezionare anche l'azione per il client quando usa un punto di distribuzione da un gruppo di limiti adiacente o dal gruppo di limiti del sito predefinito.

        > [!IMPORTANT]  
        > Se si configura l'opzione di distribuzione per **eseguire il programma dal punto di distribuzione**, assicurarsi di abilitare l'opzione **copia il contenuto del pacchetto in una condivisione pacchetto nei punti di distribuzione** nella scheda **accesso dati** delle proprietà del pacchetto. In caso contrario, il pacchetto non è disponibile per l'esecuzione dai punti di distribuzione.  

    - **Consenti ai client di usare punti di distribuzione dal gruppo di limiti del sito predefinito**: quando il contenuto non è disponibile in alcun punto di distribuzione nel gruppo di limiti corrente o in uno vicino, abilitare questa opzione per consentire di provare i punti di distribuzione nel gruppo di limiti predefinito del sito.

9. Completare la procedura guidata.  

Visualizzare la distribuzione nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio** e nel riquadro dei dettagli della scheda di distribuzione del pacchetto quando si seleziona la distribuzione. Per altre informazioni, vedere [Monitorare pacchetti e programmi](#monitor-packages-and-programs).  


## <a name="monitor-packages-and-programs"></a>Monitorare pacchetti e programmi

Per monitorare le distribuzioni di pacchetti e programmi, seguire le stesse procedure usate per monitorare le applicazioni, come descritto in [Monitorare le applicazioni](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

I pacchetti e i programmi includono anche alcuni report predefiniti, che consentono di monitorare le informazioni sullo stato di distribuzione dei pacchetti e dei programmi stessi. Tali report dispongono della categoria report di **distribuzione Software-pacchetti e programmi** e **distribuzione Software-pacchetto e programma lo stato di distribuzione**.  

Per altre informazioni sulle modalità di configurazione della creazione di report in Configuration Manager, vedere [Creazione di report in Configuration Manager](/sccm/core/servers/manage/reporting).  


## <a name="manage-packages-and-programs"></a>Gestire pacchetti e programmi

Nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni** e selezionare il nodo **Pacchetti**. Selezionare il pacchetto che si desidera gestire, quindi scegliere un'attività di gestione.  

### <a name="create-prestage-content-file"></a>Crea file di contenuto di pre-installazione

Apre la creazione **guidata file di contenuto pre-installazione**per creare un file che contiene il contenuto del pacchetto. Utilizzare questo file per importare manualmente il pacchetto in un punto di distribuzione remoto. Questa azione è utile quando è disponibile una larghezza di banda ridotta tra il server del sito e il punto di distribuzione.

### <a name="create-program"></a>Creazione di programma

Apre la **Creazione guidata programma**, che consente di creare un nuovo programma per il pacchetto.

### <a name="export"></a>Esporta

Apre l'**Esportazione guidata del pacchetto**, che consente di esportare il pacchetto selezionato e il suo contenuto in un file. Utilizzare questo file per importare il file in un'altra gerarchia.

Per informazioni su come importare pacchetti e programmi, vedere [Creare un pacchetto e un programma ](#create-a-package-and-program).

### <a name="deploy"></a>Distribuire

Apre la **Distribuzione guidata del software**, che consente di distribuire il pacchetto e il programma selezionati in una raccolta. Per altre informazioni, vedere [Distribuire pacchetti e programmi](#deploy-packages-and-programs).

### <a name="distribute-content"></a>Distribuire il contenuto

Apre la **distribuzione guidata contenuto**per inviare il contenuto di un pacchetto e un programma ai punti di distribuzione o ai gruppi di punti di distribuzione selezionati.

### <a name="update-distribution-points"></a>Aggiorna punti di distribuzione

Aggiorna i punti di distribuzione con il contenuto più recente per il pacchetto e il programma selezionati.


## <a name="see-also"></a>Vedere anche

- [Script](/sccm/apps/deploy-use/create-deploy-scripts)

- [Package Conversion Manager](/sccm/apps/pcm/package-conversion-manager)

- [File di definizione del pacchetto](/sccm/apps/deploy-use/package-definition-files)

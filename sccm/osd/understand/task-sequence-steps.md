---
title: "Passaggi della sequenza di attività | Configuration Manager"
description: "Informazioni sui passaggi della sequenza di attività che è possibile aggiungere a una sequenza di attività di Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
caps.latest.revision: 26
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2a45cfb3e00d8078fbf45bdc8a2668b7dd0a62c6
ms.openlocfilehash: 538cb9795586115ad8b52b44fb82b50a0abdbaa2


---
# <a name="task-sequence-steps-in-system-center-configuration-manager"></a>Passaggi della sequenza di attività in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

A una sequenza di attività di Configuration Manager è possibile aggiungere i passaggi seguenti. Per informazioni sulla modifica di una sequenza di attività, vedere [Edit a task sequence](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  


##  <a name="a-namebkmkapplydataimagea-apply-data-image-task-sequence-step"></a><a name="BKMK_ApplyDataImage"></a> Passaggio Applica immagine dei dati della sequenza di attività  
 Usare il passaggio **Applica immagine dei dati** della sequenza di attività per copiare l'immagine dei dati nella partizione di destinazione specificata.  

 Questo passaggio può essere eseguito solo in Windows PE. Non può essere eseguito in un sistema operativo standard. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Variabili di azione della sequenza di attività](task-sequence-action-variables.md).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Pacchetto immagine**  
 Specificare il **Pacchetto immagine** che verrà usato da questo passaggio della sequenza di attività facendo clic su **Sfoglia**. Selezionare il pacchetto da installare nella finestra di dialogo **Seleziona un pacchetto** . Le informazioni sulle proprietà associate per ogni pacchetto immagine esistente sono visualizzate nella parte inferiore della finestra di dialogo **Seleziona un pacchetto** . Usare l'elenco a discesa per selezionare l' **Immagine** da installare dal pacchetto **Pacchetto immagine**selezionato.  

> [!NOTE]  
>  Questa azione della sequenza di attività considera l'immagine come un file di dati e non esegue alcuna operazione di configurazione necessaria per l'avvio dell'immagine come sistema operativo.  

 **Destinazione**  
 Specifica una partizione formattata e un disco rigido esistenti, una lettera di unità logica specifica o il nome di una variabile della sequenza di attività che include la lettera dell'unità logica.  

-   **Partizione disponibile successiva**: usare la partizione sequenziale successiva non sottoposta in precedenza a un'azione Applica sistema operativo o Applica immagine dei dati in questa sequenza di attività.  

-   **Disco e partizione specifici**: selezionare il numero del **Disco**, partendo da 0, e il numero della **Partizione**, partendo da 1.  

-   **Lettera unità logica specifica**: specificare la **Lettera unità** assegnata alla partizione da Windows PE. Si noti che questa lettera di unità può risultare diversa dalla lettera di unità assegnata dal sistema operativo appena distribuito.  

-   **Lettera unità logica archiviata in una variabile**: specificare la variabile della sequenza di attività contenente la lettera di unità assegnata alla partizione da Windows PE. Questa variabile viene in genere impostata nella sezione Avanzate della finestra di dialogo **Proprietà della partizione** per l'azione **Formato e disco partizione** della sequenza di attività.  

 **Elimina tutti i contenuti nella partizione prima di applicare l'immagine**  
 Specifica che tutti i file nella partizione di destinazione verranno eliminati prima dell'installazione dell'immagine. Non eliminando il contenuto della partizione, questo passaggio può essere usato per applicare contenuti aggiuntivi a una partizione interessata in precedenza da questa attività.  

##  <a name="a-namebkmkapplydriverpackagea-apply-driver-package"></a><a name="BKMK_ApplyDriverPackage"></a> Applica pacchetto di driver  
 Usare il passaggio **Applica pacchetto di driver** della sequenza di attività per scaricare tutti i driver del pacchetto di driver e installarli nel sistema operativo Windows.

 Il passaggio **Applica pacchetto di driver** della sequenza di attività rende disponibili tutti i driver di dispositivo inclusi in un pacchetto di driver per l'uso da parte di Windows. Questo passaggio può essere aggiunto a una sequenza di attività tra i passaggi **Applica sistema operativo**  e **Imposta Windows e ConfigMgr** per rendere disponibili a Windows i driver di dispositivo inclusi nel pacchetto di driver. In genere, il passaggio **Applica pacchetto di driver** viene posizionato dopo il passaggio **Applica automaticamente i driver** della sequenza di attività. Il passaggio **Applica pacchetto di driver** della sequenza di attività è utile anche negli scenari di distribuzione di supporti autonomi.  

 Assicurarsi che i driver di dispositivi simili siano inseriti in un pacchetto di driver e quindi distribuirli nei punti di distribuzione appropriati. Dopo aver distribuito i driver, i computer client di Configuration Manager possono installarli. È ad esempio possibile inserire tutti i driver di dispositivo di un produttore specifico in un pacchetto di driver e quindi distribuire il pacchetto nei punti di distribuzione, in modo che i computer associati possano accedervi.

 Questo passaggio è utile per i supporti autonomi e per gli amministratori che vogliono installare un set specifico di driver, inclusi i driver per dispositivi che non verrebbero rilevati in una scansione Plug-n-Play, ad esempio per le stampanti di rete.  

 Questo passaggio della sequenza di attività può essere eseguito solo in Windows PE. Non può essere eseguito in un sistema operativo standard. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Apply Driver Package Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyDriverPackage).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Pacchetto driver**  
 Specificare il pacchetto di driver contenente i driver di dispositivo necessari, facendo clic su **Sfoglia** e aprendo la finestra di dialogo **Seleziona un pacchetto** . Specificare un pacchetto esistente da rendere disponibile. Le proprietà associate del pacchetto vengono visualizzate nella parte inferiore della finestra di dialogo.  

 **Selezionare il driver di archiviazione di massa nel pacchetto da installare prima che Configuration Manager installi i sistemi operativi Windows precedenti a Windows Vista**  
 Specificare eventuali driver di dispositivi di archiviazione di massa necessari per le installazioni di sistemi operativi precedenti a Windows Vista.  

 **Driver**  
 Selezionare il file del driver di dispositivi di archiviazione di massa da installare prima della configurazione in distribuzioni di sistemi operativi precedenti a Windows Vista. L'elenco a discesa viene popolato dal pacchetto specificato.  

 **Model**  
 Specificare il dispositivo critico per l'avvio necessario per le distribuzioni di sistemi operativi precedenti a Windows Vista.  

 **Esegui l'installazione automatica dei driver senza firma sulle versioni di Windows in cui è consentito**  
 Selezionare questa opzione per permettere a Windows di installare driver senza firma nel computer di riferimento.  

##  <a name="a-namebkmkapplynetworksettingsa-apply-network-settings-step"></a><a name="BKMK_ApplyNetworkSettings"></a> Passaggio Applica impostazioni di rete  
 Usare il passaggio **Applica impostazioni di rete** della sequenza di attività per specificare le informazioni di configurazione per la rete o il gruppo di lavoro per il computer di destinazione. I valori specificati vengono archiviati nel formato di file di risposte appropriato per l'uso da parte del programma di installazione di Windows durante l'esecuzione del passaggio **Imposta Windows e ConfigMgr** della sequenza di attività.  

 Questo passaggio della sequenza di attività viene eseguito in un sistema operativo standard o in Windows PE. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Apply Network Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyNetworkSettings).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Aggiunta a un gruppo di lavoro**  
 Selezionare questa opzione per aggiungere il computer di destinazione al gruppo di lavoro specificato. Immettere il nome del gruppo di lavoro nella riga **Gruppo di lavoro** . Questo valore può essere sostituito dal valore acquisito dal passaggio **Acquisisci impostazioni di rete** della sequenza di attività.  

 **Aggiunta a un dominio**  
 Selezionare questa opzione per aggiungere il computer di destinazione al dominio specificato. Specificare o selezionare il dominio, ad esempio *fabricam.com*. Specificare o selezionare un percorso LDAP (Lightweight Directory Access Protocol) per un'unità organizzativa, ad esempio LDAP//OU=computers, DC=Fabricam.com, C=com.  

 **Account**  
 Fare clic su **Imposta** per specificare un account con le autorizzazioni necessarie per l'aggiunta del computer al dominio. Nella finestra di dialogo **Account utente di Windows** è possibile immettere il nome utente usando il formato seguente: **Dominio\Utente** .  

 **Impostazioni della scheda**  
 Specificare le configurazioni di rete per ogni scheda di rete nel computer. Fare clic su **Nuovo** per aprire la finestra di dialogo **Impostazioni di rete** , quindi specificare le impostazioni di rete. Se le impostazioni di rete sono state acquisite in un passaggio **Acquisisci impostazioni di rete** precedente della sequenza di attività, le impostazioni precedenti verranno applicate alla scheda di rete e le impostazioni specificate in questo passaggio non verranno applicate. Se le impostazioni di rete non sono state acquisite in precedenza, le impostazioni specificate nel passaggio **Applica impostazioni di rete** verranno applicate alle schede di rete in base all'ordine di enumerazione dei dispositivi Windows.  

##  <a name="a-namebkmkapplyoperatingsystemimagea-apply-operating-system-image"></a><a name="BKMK_ApplyOperatingSystemImage"></a> Applica immagine del sistema operativo  
 Usare il passaggio **Applica immagine del sistema operativo** della sequenza di attività per installare un sistema operativo nel computer di destinazione. Questo passaggio della sequenza di attività esegue un insieme di azione, in base all'uso di un'immagine del sistema operativo o di un pacchetto di installazione del sistema operativo per installare il sistema operativo.  

 Quando si usa un'immagine del sistema operativo, il passaggio **Applica immagine del sistema operativo** esegue le azioni seguenti.  

1.  Eliminazione di tutti i contenuti nel volume interessato, ad eccezione dei file presenti nella cartella specificata dalla variabile _SMSTSUserStatePath della sequenza di attività.  

2.  Estrazione dei contenuti del file con estensione wim specificato nella partizione di destinazione specificata.  

3.  Preparazione del file di risposte:  

    1.  Creazione di un nuovo file di risposte predefinito del programma di installazione di Windows (sysprep.inf o unattend.xml) per il sistema operativo da distribuire.  

    2.  Unione di eventuali valori disponibili nel file di risposte fornito dall'utente.  

4.  Copia dei caricatori di avvio di Windows nella partizione attiva.  

5.  Configurazione del file boot.ini o dei dati di configurazione di avvio in modo che facciano riferimento al sistema operativo appena installato.  

 Quando si usa un pacchetto di installazione del sistema operativo, il passaggio **Applica immagine del sistema operativo** esegue le azioni seguenti.  

1.  Eliminazione di tutti i contenuti nel volume interessato, ad eccezione dei file presenti nella cartella specificata dalla variabile _SMSTSUserStatePath della sequenza di attività.  

2.  Preparazione del file di risposte:  

    1.  Creazione di un nuovo file di risposte con valori standard generati da Configuration Manager.  

    2.  Unione di eventuali valori disponibili nel file di risposte fornito dall'utente.  

> [!NOTE]  
>  L'installazione effettiva di Windows viene avviata dal passaggio **Imposta Windows e ConfigMgr** della sequenza di attività. Dopo l'esecuzione del passaggio **Applica sistema operativo** della sequenza di attività, la variabile OSDTargetSystemDrive della sequenza di attività verrà impostata sulla lettera di unità della partizione che include i file del sistema operativo.  

 Questo passaggio della sequenza di attività può essere eseguito solo in Windows PE. Non può essere eseguito in un sistema operativo standard. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Apply Operating System Image Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyOperatingSystem).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   **Accedi al contenuto direttamente dal punto di distribuzione**:  

     Usare questa opzione per specificare se si vuole che la sequenza di attività acceda all'immagine del sistema operativo direttamente dal punto di distribuzione. È ad esempio possibile usare questa opzione quando si distribuiscono sistemi operativi in dispositivi incorporati con capacità di archiviazione limitata. Quando questa opzione è selezionata, è necessario configurare anche le impostazioni di condivisione pacchetto nella scheda **Accesso dati** delle proprietà del pacchetto.  

    > [!NOTE]  
    >  Questa impostazione sostituisce l'opzione di distribuzione configurata nella pagina **Punti di distribuzione** nella **Distribuzione guidata del software** solo per l'immagine del sistema operativo specificata in questo passaggio della sequenza di attività. Non sostituisce tutto il contenuto per l'intera sequenza di attività.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Applica sistema operativo da un'immagine acquisita**  
 Installa un'immagine del sistema operativo acquisita in precedenza. Fare clic su **Sfoglia** per aprire la finestra di dialogo **Seleziona un pacchetto** , quindi selezionare il pacchetto immagine esistente da installare. Se al **Pacchetto immagine**specificato sono associate più immagini, usare l'elenco a discesa per specificare l'immagine associata che verrà usata per questa distribuzione. Per visualizzare le informazioni di base su ogni immagine esistente, fare clic sull'immagine.  

 **Applica sistema operativo da un'origine di installazione originale**  
 Installa un sistema operativo usando un'origine di installazione originale. Fare clic su **Sfoglia** per aprire la finestra di dialogo **Seleziona un pacchetto di installazione del sistema operativo** , quindi selezionare il pacchetto di installazione del sistema operativo esistente da usare. Per visualizzare le informazioni di base su ogni immagine esistente, fare clic sull'origine dell'immagine. Le proprietà associate dell'origine dell'immagine vengono visualizzate nel riquadro dei risultati nella parte inferiore della finestra di dialogo. Se al pacchetto specificato sono associate più edizioni, usare l'elenco a discesa per specificare l' **Edizione** associata usata.  

 **Utilizza un file di risposta automatica o Sysprep per un'installazione personalizzata**  
 Usare questa opzione per fornire un file di risposte del programma di installazione di Windows (**unattend.xml**, **unattend.txt**o **sysprep.inf**), in base alla versione e al metodo di installazione del sistema operativo. Il file specificato può includere qualsiasi opzione di configurazione standard supportata dai file di risposte di Windows. È ad esempio possibile usarla per specificare la home page predefinita di Internet Explorer. È necessario specificare il pacchetto che contiene il file di risposte e il percorso associato al file nel pacchetto.  

> [!NOTE]  
>  Il file di risposte del programma di installazione di Windows fornito può includere variabili incorporate della sequenza di attività con formato %*varname*%, dove varname indica il nome della variabile. La stringa %*varname*% verrà sostituita dai valori effettivi delle variabili nel passaggio **Imposta Windows e ConfigMgr** della sequenza di attività. Si noti tuttavia che queste variabili incorporate della sequenza di attività non possono essere usate in campi di tipo solo numerico in un file di risposte unattend.xml.  

 Se non si fornisce alcun file di risposte del programma di installazione di Windows, questo passaggio della sequenza di attività genererà automaticamente un file di risposte.  

 **Destinazione**  
 Specifica una partizione formattata e un disco rigido esistenti, una lettera di unità logica specifica o il nome di una variabile della sequenza di attività che include la lettera dell'unità logica.  

-   **Partizione disponibile successiva**: usare la partizione sequenziale successiva non sottoposta in precedenza a un'azione Applica sistema operativo o Applica immagine dei dati in questa sequenza di attività.  

-   **Disco e partizione specifici**: selezionare il numero del **Disco**, partendo da 0, e il numero della **Partizione**, partendo da 1.  

-   **Lettera unità logica specifica**: specificare la **Lettera unità** assegnata alla partizione da Windows PE. Si noti che questa lettera di unità può risultare diversa dalla lettera di unità assegnata dal sistema operativo appena distribuito.  

-   **Lettera unità logica archiviata in una variabile**: specificare la variabile della sequenza di attività contenente la lettera di unità assegnata alla partizione da Windows PE. Questa variabile viene in genere impostata nella sezione Avanzate della finestra di dialogo **Proprietà della partizione** per l'azione **Formato e disco partizione** della sequenza di attività.  

##  <a name="a-namebkmkapplywindowssettingsa-apply-windows-settings"></a><a name="BKMK_ApplyWindowsSettings"></a> Applica impostazioni Windows  
 Usare il passaggio **Applica impostazioni Windows** della sequenza di attività per configurare le impostazioni di Windows per il computer di destinazione. I valori specificati vengono archiviati nel formato di file di risposte appropriato per l'uso da parte del programma di installazione di Windows durante l'esecuzione del passaggio **Imposta Windows e ConfigMgr** della sequenza di attività.  

 Questo passaggio della sequenza di attività può essere eseguito solo in Windows PE. Non può essere eseguito in un sistema operativo standard. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Apply Windows Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyWindowsSettings).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Nome utente**  
 Specificare il nome dell'utente registrato associato al computer di destinazione. Questo valore può essere sostituito dal valore acquisito dal passaggio **Acquisisci impostazioni Windows** della sequenza di attività.  

 **Nome organizzazione**  
 Specificare il nome dell'organizzazione registrata associata al computer di destinazione. Questo valore può essere sostituito dal valore acquisito dal passaggio **Acquisisci impostazioni Windows** della sequenza di attività.  

 **Codice Product Key**  
 Specificare il codice Product Key usato per l'installazione di Windows nel computer di destinazione.  

 **Licenze server**  
 Specificare la modalità di gestione delle licenza del server, ovvero **Per server** o **Per Utente** . Se si sceglie la modalità di gestione delle licenze Per server, sarà necessario specificare anche il numero massimo di connessioni consentite in base al contratto di licenza. Selezionare **Non specificare** se il computer di destinazione non è un server o se non si vuole specificare la modalità di gestione delle licenze.  

 **Numero massimo di connessioni**  
 Specificare il numero massimo di connessioni disponibili per questo computer, in base a quanto indicato nel contratto di licenza.  

 **Genera in modo casuale la password dell'amministratore locale e disattiva l'account su tutte le piattaforme supportate (consigliato)**  
 Selezionare questa opzione per generare in modo casuale una password per l'amministratore locale. Verrà creata una password per l'amministratore locale e l'account verrà disabilitato nelle piattaforme supportate.  

 **Attiva l'account e specifica la password dell'amministratore locale**  
 Selezionare questa opzione per abilitare l'account dell'amministratore locale e creare la password dell'amministratore locale. Immettere la password nella riga **Password** e confermare la password nella riga **Conferma password** .  

 **Fuso orario**  
 Specificare il fuso orario da configurare nel computer di destinazione. Questo valore può essere sostituito dal valore acquisito dal passaggio **Acquisisci impostazioni Windows** della sequenza di attività.  

##  <a name="a-namebkmkautoapplydriversa-auto-apply-drivers"></a><a name="BKMK_AutoApplyDrivers"></a> Applica automaticamente i driver  
 Usare il passaggio **Applica automaticamente i driver** della sequenza di attività per associare e installare i driver come parte della distribuzione del sistema operativo.  

 Il passaggio **Applica automaticamente i driver** della sequenza di attività esegue le azioni seguenti:  

1.  Analisi dell'hardware e individuazione degli ID Plug-n-Play per tutti i dispositivi presenti nel sistema.  

2.  Invio dell'elenco di dispositivi e dei rispettivi ID Plug-n-Play al punto di gestione. Il punto di gestione restituisce un elenco di driver compatibili dal catalogo di driver per ogni dispositivo. Il punto di gestione considera tutti i driver, a prescindere dal pacchetto di driver in cui sono presenti. Vengono considerati soltanto i driver contrassegnati da una determinata categoria e quelli che non sono contrassegnati come disattivati.  

3.  Per ogni dispositivo, il client sceglie il driver migliore idoneo al sistema operativo in cui viene distribuito e disponibile in un punto di distribuzione accessibile.  

4.  I driver selezionati vengono scaricati da un punto di distribuzione e gestiti in modo temporaneo nel sistema operativo di destinazione.  

    1.  Per le installazioni basate su immagine, i driver vengono inseriti nell'archivio driver del sistema operativo.  

    2.  Per le installazioni basate sul programma di installazione, il Programma di installazione di Windows Setup viene configurato in modo da individuare i driver.  

5.  Quando viene eseguito il passaggio **Imposta Windows e ConfigMgr** della sequenza di attività e nelle fasi iniziali dell'avvio di Windows verranno individuati i driver gestiti in modo temporanea da questa azione.  

> [!IMPORTANT]
>  Il passaggio **Applica automaticamente i driver** della sequenza di attività non può essere usato con supporti autonomi, poiché il programma di installazione di Windows non sarà connesso al sito di Configuration Manager.

Questo passaggio della sequenza di attività può essere eseguito solo in Windows PE. Non può essere eseguito in un sistema operativo standard. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Auto Apply Drivers Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_AutoApplyDrivers).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Installa solo i driver compatibili con la corrispondenza migliore**  
 Indica che il passaggio della sequenza di attività installa solo i driver con la corrispondenza migliore per ogni dispositivo hardware rilevato.  

 **Installa tutti i driver compatibili**  
 Indica che il passaggio della sequenza di attività installa tutti i driver compatibili per ogni dispositivo hardware e permette al programma di installazione di Windows di scegliere il driver migliore. Questa opzione richiede una maggiore larghezza di banda e più spazio su disco, poiché scarica più driver, ma può permettere la selezione di un driver migliore.  

 **Considera i driver di tutte le categorie**  
 Indica che l'azione della sequenza di attività cerca i driver di dispositivo appropriati in tutte le categorie di driver disponibili.  

 **Limita la corrispondenza dei driver in modo da considerare solo i driver delle categorie selezionate**  
 Indica che l'azione della sequenza di attività cerca i driver di dispositivo in categorie di driver specificate per i driver di dispositivo appropriati.  

 **Esegui l'installazione automatica dei driver senza firma sulle versioni di Windows in cui è consentito**  
 Permette a questa azione della sequenza di attività di installare driver di dispositivo Windows senza firma.  

> [!IMPORTANT]  
>  Questa opzione non è applicabile ai sistemi operativi in cui non è possibile configurare i criteri di firma dei driver.  

##  <a name="a-namebkmkcapturenetworksettingsa-capture-network-settings"></a><a name="BKMK_CaptureNetworkSettings"></a> Acquisisci impostazioni di rete  
 Usare il passaggio **Acquisisci impostazioni di rete** della sequenza di attività per acquisire le impostazioni di rete Microsoft dal computer che esegue la sequenza di attività. Le impostazioni vengono salvate nelle variabili della sequenza di attività che sostituiranno le impostazioni predefinite configurate nel passaggio **Applica impostazioni di rete** della sequenza di attività.  

 Questo passaggio della sequenza di attività può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Capture Network Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureNetworkSettings).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Specifica un nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Fornisce informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Esegui la migrazione del dominio e dell'appartenenza a gruppi di lavoro**  
 Acquisisce le informazioni sull'appartenenza a domini e gruppi di lavoro del computer di destinazione.  

 **Esegui la migrazione della configurazione della scheda di rete**  
 Acquisisce la configurazione della scheda di rete del computer di destinazione. Le informazioni acquisite includono le impostazioni di rete globali, il numero di schede e le impostazioni di rete associate a ogni scheda. Queste impostazioni includono le impostazioni associate a DNS, WINS, IP e ai filtri delle porte.  

##  <a name="a-namebkmkcaptureoperatingsystemimagea-capture-operating-system-image"></a><a name="BKMK_CaptureOperatingSystemImage"></a> Acquisisci immagine del sistema operativo  
 Usare il passaggio **Acquisisci immagine del sistema operativo** della sequenza di attività per acquisire una o più immagini da un computer di riferimento e archiviarle in un file con estensione wim nella condivisione di rete specificata. La procedura guidata del pacchetto potrà essere usata per aggiungere l'immagine del sistema operativo e importare il file con estensione wim in Configuration Manager. In questo modo sarà possibile usarlo per le distribuzioni del sistema operativo basate su immagine.  

 Ogni volume (unità) nel computer di riferimento viene acquisito come immagine distinta nel file con estensione wim. Se il computer a cui si fa riferimento include più volumi, il file con estensione WIM risultate conterrà un'immagine distinta per ogni volume. Vengono acquisiti solo i volumi con formattazione NTFS o FAT32. I volumi con formati diversi e i volumi USB verranno ignorati.  

 Il sistema operativo installato nel computer di riferimento deve essere una versione di Windows supportata da Configuration Manager e deve essere stato preparato usando lo strumento SysPrep. Il volume del sistema operativo installato deve essere uguale al volume di avvio.  

 È anche necessario immettere un account di Windows con autorizzazioni di scrittura per la condivisione di rete selezionata.  

 Questo passaggio della sequenza di attività può essere eseguito solo in Windows PE. Non può essere eseguito in un sistema operativo standard. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Capture Operating System Image Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureOperatingSystemImage).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Destinazione**  
 Percorso del file system usato da Configuration Manager per l'archiviazione dell'immagine acquisita del sistema operativo.  

 **Descrizione**  
 Descrizione facoltativa definita dall'utente dell'immagine acquisita del sistema operativo archiviata nel file con estensione WIM.  

 **Versione**  
 Numero di versione facoltativo definito dall'utente da assegnare all'immagine acquisita del sistema operativo. Questo valore può essere costituito da qualsiasi combinazione di lettere e numeri e viene archiviato nel file con estensione WIM.  

 **Creato da**  
 Nome facoltativo dell'utente che ha creato l'immagine del sistema operativo. Viene archiviato nel file con estensione WIM.  

 **Account di acquisizione dell'immagine del sistema operativo**  
 È necessario immettere l'account di Windows con autorizzazioni per la condivisione di rete specificata. Fare clic su **Imposta** per specificare il nome dell'account di Windows.  

##  <a name="a-namebkmkcaptureuserstatea-capture-user-state"></a><a name="BKMK_CaptureUserState"></a> Acquisisci stato utente  
 Usare il passaggio **Acquisisci stato utente** della sequenza di attività per usare l'Utilità di migrazione stato utente (USMT, User State Migration Tool) per acquisire lo stato utente e le impostazioni dal computer che esegue la sequenza di attività. Questo passaggio della sequenza di attività viene usato insieme al passaggio **Ripristina stato utente** . In USMT 3.0.1 e versioni successive questa opzione crittografa sempre l'archiviazione stati USMT usando una chiave di crittografia generata e gestita da Configuration Manager.  

 Per altre informazioni sulla gestione dello stato utente durante la distribuzione di sistemi operativi, vedere [Manage user state](../get-started/manage-user-state.md) (Gestire lo stato utente).  

 È anche possibile usare il passaggio **Acquisisci stato utente** della sequenza di attività insieme ai passaggi **Richiedi archiviazione stati** e **Rilascia archiviazione stati** se si vogliono salvare le impostazioni dello stato o ripristinare tali impostazioni da un punto di migrazione stato nel sito di Configuration Manager.  

 Il passaggio **Acquisisci stato utente** della sequenza di attività fornisce il controllo su un sottoinsieme limitato delle opzioni USMT più usate. È possibile specificare opzioni aggiuntive da riga di comando usando la variabile OSDMigrateAdditionalCaptureOptions della sequenza di attività.  

 Questo passaggio della sequenza di attività può essere eseguito solo in Windows PE. Non può essere eseguito in un sistema operativo standard. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Capture User State Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureUserState).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Pacchetto degli strumenti di migrazione dello stato utente**  
 Immettere il pacchetto di Configuration Manager che contiene la versione di USMT che deve essere usata da questo passaggio della sequenza di attività durante l'acquisizione dello stato e delle impostazioni utente. Questo pacchetto non richiede alcun programma. Quando viene eseguito il passaggio della sequenza di attività, verrà usata la versione di USMT disponibile nel pacchetto specificato. Specificare un pacchetto contenente la versione a 32 bit o x64 di USMT, in base all'architettura del sistema operativo da cui si acquisisce lo stato.  

 **Acquisisci tutti i profili utente utilizzando le opzioni standard**  
 Selezionare questa opzione per eseguire la migrazione di tutte le informazioni sul profilo utente. Questa opzione è selezionata per impostazione predefinita.  

 Se si seleziona questa opzione, ma non si seleziona l'opzione Ripristina profili utente del computer locale nel passaggio Ripristina stato utente, la sequenza di attività avrà esito negativo poiché Configuration Manager non può eseguire la migrazione dei nuovi account senza aver prima assegnato loro una password. Se inoltre si usa la procedura guidata **Crea nuova sequenza di attività** e si crea una sequenza di attività che **Installa un pacchetto immagine esistente**, per la sequenza di attività risultante verrà usato il valore predefinito Acquisisci tutti i profili utente usando le opzioni standard, ma non verrà selezionata l'opzione Ripristina profili utente del computer locale, ovvero gli account non di dominio.  

 Selezionare **Ripristina profili utente del computer locale** e fornire una password per l'account di cui deve essere eseguita la migrazione. In una sequenza di attività creata manualmente questa impostazione è disponibile nel passaggio Ripristina stato utente. In una sequenza di attività creata dalla procedura guidata **Crea nuova sequenza di attività** questa impostazione è disponibile nella pagina della procedura guidata **Ripristina file utente e impostazioni** .  

 Se non sono presenti account utente locali, questa opzione non è applicabile.  

 **Personalizza modalità di acquisizione dei profili utente**  
 Selezionare questa opzione per specificare una migrazione del file di profilo personalizzato. Fare clic su **File** per selezionare i file di configurazione che USMT dovrà usare con questo passaggio. È necessario specificare un file con estensione xml personalizzato contenente le regole che definiscono i file di stato utente di cui eseguire la migrazione.  

 **Fare clic qui per selezionare i file di configurazione:**  
 Selezionare questa opzione per selezionare i file di configurazione nel pacchetto USMT da usare per l'acquisizione dei profili utente. Fare clic su **File** per aprire la finestra di dialogo **File di configurazione** . Per specificare un file di configurazione, immettere il nome del file nella riga **Nome file** e quindi fare clic su **Aggiungi** .  

 **Abilita la registrazione dettagliata**  
 Abilitare questa opzione per generare informazioni di file di log più dettagliate. Durante l'acquisizione dello stato, il file Scanstate.log viene generato e archiviato per impostazione predefinita nella cartella Log della sequenza di attività nella cartella \windows\system32\ccm\logs.  

 **Ignora file che utilizzano Encrypting File System (EFS)**  
 Abilitare questa opzione per ignorare i file di acquisizione crittografati con Encrypted File System (EFS), inclusi i file di profilo. In base al sistema operativo e alla versione di USMT, è possibile che i file crittografati non siano leggibili dopo il ripristino. Per altre informazioni, vedere la documentazione relativa a USMT.  

 **Copia utilizzando l'accesso al file system**  
 Abilitare questa opzione per specificare una delle impostazioni seguenti:  

-   **Continua se non è possibile acquisire alcuni file**: questa impostazione consente al passaggio della sequenza di attività di continuare il processo di migrazione, anche se non è possibile acquisire alcuni file. Se si disabilita questa opzione, il passaggio della sequenza di attività avrà esito negativo nel caso in cui non sia possibile acquisire un file. Questa opzione è attivata per impostazione predefinita.  

-   **Esegui acquisizione localmente utilizzando i collegamenti invece di copiare i file**: abilitare questa impostazione per usare i collegamenti reali NTFS per acquisire i file.  

     Per altre informazioni sulla migrazione di dati tramite i collegamenti reali, vedere [Archivio delle migrazioni con collegamento reale](http://go.microsoft.com/fwlink/p/?LinkId=240222)  

-   **Acquisisci in modalità non in linea (solo Windows PE)**: abilitare questa impostazione per acquisire lo stato utente in Windows PE invece che nel sistema operativo completo.  

 **Acquisisci utilizzando Servizio Copia Shadow del volume (VSS)**  
 Questa opzione consente di acquisire file anche se sono bloccati per la modifica da un'altra applicazione.  

##  <a name="a-namebkmkcapturewindowssettingsa-capture-windows-settings"></a><a name="BKMK_CaptureWindowsSettings"></a> Acquisisci impostazioni Windows  
 Usare il passaggio **Acquisisci impostazioni Windows** della sequenza di attività per acquisire le impostazioni di Windows dal computer che esegue la sequenza di attività. Le impostazioni vengono salvate nelle variabili della sequenza di attività che sostituiranno le impostazioni predefinite configurate nel passaggio **Applica impostazioni Windows** della sequenza di attività.  

 Questo passaggio della sequenza di attività può essere eseguito in Windows PE o in un sistema operativo standard. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Capture Windows Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureWindowsSettings).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Esegui la migrazione del nome computer**  
 Selezionare questa opzione per acquisire il nome NetBIOS del computer.  

 **Esegui la migrazione dell'utente registrato e dei nomi organizzazione**  
 Selezionare questa opzione per acquisire l'utente registrato e i nomi dell'organizzazione dal computer.  

 **Esegui la migrazione del fuso orario**  
 Selezionare questa opzione per acquisire l'impostazione relativa al fuso orario nel computer.  

##  <a name="a-namebkmkcheckreadinessa-check-readiness"></a><a name="BKMK_CheckReadiness"></a> Verifica conformità  
 Usare il passaggio **Verifica conformità** della sequenza di attività per verificare che il computer di destinazione soddisfi le condizioni dei prerequisiti di distribuzione specificate.  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio. Non selezionare questa impostazione per questo passaggio, altrimenti il passaggio registrerà solo le verifiche della conformità e non interromperà la sequenza di attività in caso di errore della verifica.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Verifica la quantità di memoria minima (MB)**  
 Selezionare questa impostazione per verificare se la quantità di memoria, in megabyte, installata nel computer di destinazione soddisfa o supera la quantità specificata. Questa opzione è selezionata per impostazione predefinita.  

 **Verifica la velocità minima del processore (MHz)**  
 Selezionare questa opzione per verificare se la velocità del processore, in megahertz (MHz), installato nel computer di destinazione soddisfa o supera la quantità specificata. Questa opzione è selezionata per impostazione predefinita.  

 **Verifica lo spazio minimo disponibile su disco (MB)**  
 Selezionare questa impostazione per verificare se la quantità di spazio disponibile su disco, in megabyte, nel computer di destinazione soddisfa o supera la quantità specificata.  

 **Verifica che il sistema operativo corrente da aggiornare sia**  
 Selezionare questa impostazione per verificare se il sistema operativo installato nel computer client soddisfa i requisiti specificati. Per impostazione predefinita, questa impostazione è selezionata con un valore **CLIENT**.  

##  <a name="a-namebkmkconnecttonetworkfoldera-connect-to-network-folder"></a><a name="BKMK_ConnectToNetworkFolder"></a> Connetti alla cartella di rete  
 Usare l'azione **Connetti alla cartella di rete** della sequenza di attività per creare una connessione a una cartella di rete condivisa.  

 Questo passaggio della sequenza di attività viene eseguito in un sistema operativo standard o in Windows PE. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Connect to Network Folder Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ConnecttoNetworkFolder).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

##  <a name="a-namebkmkconvertdisktodynamica-convert-disk-to-dynamic"></a><a name="BKMK_ConvertDisktoDynamic"></a> Converti il disco selezionato in disco dinamico  
 Usare il passaggio **Converti il disco selezionato in disco dinamico** della sequenza di attività per convertire un disco fisico da un tipo di disco di base a un tipo di disco dinamico.  

 Questo passaggio viene eseguito in un sistema operativo standard o in Windows PE. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Convert Disk to Dynamic Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ConvertDisk).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Numero disco**  
 Numero del disco fisico che verrà convertito.  

##  <a name="a-namebkmkdisablebitlockera-disable-bitlocker"></a><a name="BKMK_DisableBitLocker"></a> Disattiva BitLocker  
 Usare il passaggio **Disattiva BitLocker** della sequenza di attività per disabilitare la crittografia BitLocker nell'unità attuale del sistema operativo o in un'unità specificata. Questa azione lascia che le protezioni con chiave siano visibili in testo non crittografato nel disco rigido, ma non decrittografa i contenuti dell'unità. Questa azione viene quindi completata quasi istantaneamente.  

> [!NOTE]  
>  La crittografia unità BitLocker offre una crittografia di basso livello dei contenuti di un volume del disco.  

 Se sono disponibili più unità crittografate, sarà necessario disabilitare BitLocker in qualsiasi unità di dati prima di disabilitare BitLocker nell'unità del sistema operativo.  

 Questo passaggio può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE.  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Specifica un nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Fornisce informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Unità del sistema operativo corrente**  
 Disabilita BitLocker nell'unità attuale del sistema operativo.  

 **Unità specifica**  
 Disabilita BitLocker in un'unità specifica. Usare l'elenco a discesa per specificare l'unità in cui BitLocker è disabilitato.  

##  <a name="a-namebkmkdownloadpackagecontenta-download-package-content"></a><a name="BKMK_DownloadPackageContent"></a> Scarica contenuto pacchetto  
 Usare il passaggio della sequenza di attività **Scarica contenuto pacchetto** per scaricare uno dei tipi di pacchetto seguenti:  

-   Immagini del sistema operativo  

-   Pacchetti di aggiornamento del sistema operativo  

-   Pacchetti driver  

-   Pacchetti  

 Questo passaggio funziona bene in una sequenza di attività per eseguire l'aggiornamento di un sistema operativo negli scenari seguenti:  

-   Usare una singola sequenza di attività di aggiornamento che può funzionare con piattaforme x86 e x64. Per portare a termine la procedura, è necessario includere due passaggi **Scarica contenuto pacchetto** nel gruppo **Preparazione dell'aggiornamento** con le condizioni per rilevare l'architettura client e scaricare solo il pacchetto di aggiornamento del sistema operativo appropriato. Configurare ogni passaggio **Scarica contenuto pacchetto** in modo da usare la stessa variabile e usare la variabile per il percorso del supporto durante il passaggio **Aggiorna sistema operativo** .  

-   Per scaricare in modo dinamico un pacchetto di driver applicabile, usare due passaggi **Scarica contenuto pacchetto** con le condizioni per rilevare il tipo di hardware appropriato per ogni pacchetto driver. Configurare ogni passaggio **Scarica contenuto pacchetto** in modo da usare la stessa variabile e usare la variabile per il valore **Contenuto preconfigurato** durante il passaggio **Aggiorna sistema operativo** .  

 Questo passaggio può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE.  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Specifica un nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Fornisce informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 Icona**Selezione pacchetto**  
 Fare clic sull'icona per selezionare il pacchetto da scaricare. Dopo aver selezionato un pacchetto, è possibile fare clic sull'icona di nuovo per scegliere un altro pacchetto.  

 **Inserire nel seguente percorso**  
 Scegliere di salvare il pacchetto in uno dei seguenti percorsi:  

-   **Directory di lavoro della sequenza di attività**  

-   **Cache del client di Configuration Manager**: usare questa opzione per archiviare il contenuto nella cache del client. Ciò consente al client di fungere da origine della cache peer per gli altri client della cache peer. Per altre informazioni, vedere [Prepare Windows PE peer cache to reduce WAN traffic](../get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md) (Preparare la peer cache di Windows PE per ridurre il traffico della rete WAN)  

-   **Percorso personalizzato**  

 **Salvare il percorso come variabile**  
 È possibile salvare il percorso come variabile utilizzabile in un altro passaggio della sequenza di attività. Quando sono presenti più pacchetti, Configuration Manager aggiunge un suffisso numerico al nome della variabile. Ad esempio, se si specifica una variabile %*mycontent*% come variabile personalizzata, questa è la radice in cui è archiviato tutto il contenuto di riferimento (che possono essere più pacchetti). Quando si fa riferimento alla variabile in un passaggio secondario della sequenza, ad esempio Aggiorna sistema operativo, viene usata con un suffisso numerico. In questo esempio, %*mycontent01*% o %*mycontent02*% , dove il numero corrisponde all'ordine di elencazione del pacchetto in questo passaggio.  

 **Se il download di un pacchetto non riesce, continuare a scaricare gli altri pacchetti nell'elenco**  
 Specifica che se il download del pacchetto ha esito negativo, verrà avviato il download del pacchetto successivo nell'elenco.  

##  <a name="a-namebkmkenablebitlockera-enable-bitlocker"></a><a name="BKMK_EnableBitLocker"></a> Attiva BitLocker  
 Usare il passaggio **Attiva BitLocker** della sequenza di attività per abilitare la crittografia BitLocker in almeno due partizioni sul disco rigido. La prima partizione attiva include il codice bootstrap di Windows. Un'altra partizione contiene il sistema operativo. La partizione bootstrap deve rimanere non crittografata.  

 Usare il passaggio **BitLocker pre-provisioning** della sequenza di attività per abilitare BitLocker in un'unità in Windows PE. Per altre informazioni, vedere la sezione [BitLocker pre-provisioning](#BKMK_PreProvisionBitLocker) in questo argomento.  

> [!NOTE]  
>  La crittografia unità BitLocker offre una crittografia di basso livello dei contenuti di un volume del disco.  

 Il passaggio **Attiva BitLocker** può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Enable BitLocker Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

 Lo stato di TPM (Trusted Platform Module) deve essere il seguente quando si specifica **Solo TPM**, **TPM e chiave di avvio su USB** o **TPM e PIN**, prima di potere eseguire il passaggio **Attiva BitLocker** :  

-   Abilitato  

-   Attivato  

-   Proprietà consentita  

 Il passaggio della sequenza di attività può completare eventuali operazioni di inizializzazione TPM rimanente, poiché i passaggi rimanenti non necessitano della presenza fisica o di riavvii. I passaggi rimanenti dell'inizializzazione TPM che possono essere completati in modo trasparente da **Attiva BitLocker** (se necessario) includono i seguenti:  

-   Creazione della coppia di chiavi di verifica autenticità.  

-   Creazione di un valore di autorizzazione del proprietario e del deposito in Active Directory, che deve essere stato esteso per supportare questo valore.  

-   Acquisizione della proprietà.  

-   Creazione della chiave radice di archiviazione o reimpostazione nel caso in cui la chiave sia già presente ma non sia compatibile.  

 Se si vuole che il passaggio **Attiva BitLocker** attenda il completamento del processo di crittografia dell'unità prima di procedere al passaggio successivo nella sequenza di attività, selezionare la casella di controllo **Attendere** . Se non si seleziona la casella di controllo **Attendere** , il processo di crittografia dell'unità verrà eseguito in background e la sequenza di attività procederà immediatamente al passaggio successivo.  

 È possibile usare BitLocker per crittografare più unità in un sistema di computer, sia nelle unità del sistema operativo che nelle unità dati. Per crittografare un'unità dati, il sistema operativo deve essere già crittografato e il processo di crittografia deve essere stato completato, poiché le protezioni con chiave per le unità dati vengono archiviate nell'unità del sistema operativo. Se quindi si crittografa l'unità del sistema operativo e l'unità dati nello stesso processo, sarà necessario selezionare l'opzione di attesa per il passaggio che abilita BitLocker per l'unità del sistema operativo.  

 Se il disco rigido è già crittografato ma BitLocker è disabilitato, il passaggio Attiva BitLocker abilita di nuovo le protezioni con chiavi e verrà completato quasi immediatamente. In questo caso non è necessario ripetere la crittografia del disco rigido.  

 Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Enable BitLocker Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Specifica un nome descrittivo per questo passaggio della sequenza di attività.  

 **Descrizione**  
 Permette di immettere facoltativamente una descrizione per questo passaggio della sequenza di attività.  

 **Scegli l'unità da crittografare**  
 Specifica l'unità da crittografare Per crittografare l'unità attuale del sistema operativo, selezionare **Unità del sistema operativo corrente** , quindi configurare una delle opzioni seguenti per la gestione delle chiavi:  

-   **Solo TPM**: selezionare questa opzione per usare solo TPM (Trusted Platform Module).  

-   **Chiave di avvio solo su USB**: selezionare questa opzione per usare una chiave di avvio archiviata in un'unità flash USB. Quando si seleziona questa opzione, BitLocker blocca il normale processo di avvio fino al collegamento di un dispositivo USB contenente una chiave di avvio BitLocker al computer.  

-   **TPM e chiave di avvio su USB**: selezionare questa opzione per usare TPM e una chiave di avvio archiviata in un'unità flash USB. Quando si seleziona questa opzione, BitLocker blocca il normale processo di avvio fino al collegamento di un dispositivo USB contenente una chiave di avvio BitLocker al computer.  

-   **TPM e PIN**: selezionare questa opzione per usare TPM e un codice PIN. Quando si seleziona questa opzione, BitLocker blocca il normale processo di avvio fino a quando l'utente fornisce il codice PIN.  

 Per crittografare un'unità dati specifica, non del sistema operativo, selezionare **Unità specifica**, quindi selezionare l'unità dall'elenco.  

 **Scegli dove creare la chiave di ripristino**  
 Per specificare dove viene creata la password di ripristino, selezionare **In Active Directory** per depositare la password in Active Directory. Se si seleziona questa opzione, sarà necessario estendere Active Directory per il sito, in modo che vengano salvate le informazioni di ripristino BitLocker associate. È possibile decidere di non creare la password selezionando **Non creare una chiave di ripristino**. È tuttavia consigliabile creare una password.  

 **Attendi il completamento del processo di crittografia di tutte le unità di BitLocker prima di continuare l'esecuzione della sequenza di attività con Configuration Manager**  
 Selezionare questa opzione per permettere il completamento della crittografia unità BitLocker prima dell'esecuzione del passaggio successivo nella sequenza di attività. Se questa opzione è selezionata, l'intero volume del disco verrà crittografato prima che l'utente possa accedere al computer.  

 Il completamento del processo di crittografia può richiedere alcune ore se si deve crittografare un disco rigido di grandi dimensioni. Se non si seleziona questa opzione, la sequenza di attività potrà proseguire immediatamente.  

##  <a name="a-namebkmkformatandpartitiondiska-format-and-partition-disk"></a><a name="BKMK_FormatandPartitionDisk"></a> Formato e disco partizione  
 Usare il passaggio **Formato e disco partizione** della sequenza di attività per formattare e partizionare un dico specificato nel computer di destinazione.  

> [!IMPORTANT]  
>  Ogni impostazione specificata per questo passaggio della sequenza di attività è applicabile a un singolo disco specificato. Se si vuole formattare e partizionare un altro disco nel computer di destinazione, sarà necessario aggiungere un altro passaggio **Formato e disco partizione** alla sequenza di attività.  

 Questo passaggio della sequenza di attività può essere eseguito solo in Windows PE. Non può essere eseguito in un sistema operativo standard. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Format and Partition Disk Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_FormatPartitionDisk).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Numero disco**  
 Numero del disco fisico che verrà formattato. Il numero è basato sull'ordinamento di enumerazione dei dischi Windows.  

 **Tipo di disco**  
 Tipo del disco formattato. Nell'elenco a discesa è possibile selezionare le due opzioni seguenti:  

-   Standard (MBR) - MBR (Record di avvio principale, Master Boot Record).  

-   GPT - Tabella di partizione GUID  

> [!NOTE]  
>  Se si cambia il tipo di disco da **Standard (MBR)** a **GPT**e il layout della partizione include una partizione estesa, tutte le partizioni estese e logiche verranno rimosse dal layout. Prima della modifica del tipo di disco, verrà richiesta la conferma dell'azione.  

 **Volume**  
 Informazioni specifiche sulla partizione o sul volume da creare, incluse le informazioni seguenti:  

-   Nome  

-   Spazio su disco rimanente  

 Per creare una nuova partizione, fare clic su **Nuovo** per aprire la finestra di dialogo **Proprietà della partizione** . È possibile specificare il tipo e le dimensioni della partizione e quindi specificare se sarà una partizione di avvio. Per modificare una partizione esistente, fare clic sulla partizione da modificare, quindi su Proprietà. Per altre informazioni su come configurare le partizioni del disco rigido, vedere uno degli argomenti seguenti:  

-   [Configurare partizioni in un disco rigido basato su UEFI/GPT](http://go.microsoft.com/fwlink/?LinkID=272104)  

-   [Configurare partizioni in un disco rigido basato su BIOS/MBR](http://go.microsoft.com/fwlink/?LinkId=272105)  

 Per eliminare una partizione, selezionare la partizione da eliminare, quindi fare clic su **Elimina**.  

##  <a name="a-namebkmkinstallapplicationa-install-application"></a><a name="BKMK_InstallApplication"></a> Installa applicazione  
 Usare il passaggio **Installa applicazione** della sequenza di attività per installare le applicazioni come parte della sequenza di attività. Questo passaggio permette di installare un insieme di applicazioni specificate dal passaggio della sequenza di attività o un insieme di applicazioni specificate da un elenco dinamico di variabili della sequenza di attività. Quando si esegue questo passaggio, l'installazione dell'applicazione inizia immediatamente, senza attendere il termine dell'intervallo di polling dei criteri.  

 Le applicazioni installate devono soddisfare i criteri seguenti:  

-   L'applicazione deve essere un tipo di distribuzione Windows Installer o Programma di installazione dello script. Non sono supportati i tipi di distribuzione Pacchetto app Windows (file .appx).  

-   Deve essere in esecuzione con l'account di sistema locale e non con l'account utente.  

-   Non deve interagire con il desktop. Il programma deve essere eseguito automaticamente o in modalità automatica.  

-   Non deve dare inizio autonomamente a un riavvio. L'applicazione deve richiedere un riavvio usando il codice di riavvio standard, ovvero un codice di uscita 3010. Ciò garantisce che il passaggio della sequenza di attività gestirà correttamente il riavvio. Se l'applicazione restituisce un codice di uscita 3010, il motore della sequenza di attività sottostante eseguirà il riavvio. Dopo il riavvio, la sequenza di attività continua automaticamente.  

 Quando si esegue il passaggio **Installa applicazione** , l'applicazione verifica l'applicabilità delle regole dei requisiti e del metodo di rilevamento nei tipi di distribuzione dell'applicazione. In base ai risultati di questa verifica, l'applicazione installa il tipo di distribuzione applicabile. Se il tipo di distribuzione contiene dipendenze, il tipo di distribuzione dipendente verrà valutato e installato come parte del passaggio Installa applicazione. Le dipendenze delle applicazioni non vengono supportati per i supporti autonomi.  

> [!NOTE]  
>  Per installare un'applicazione che sostituisce un'altra applicazione, è necessario che i file di contenuto per l'applicazione sostituita siano disponibili. In caso contrario, il passaggio della sequenza di attività avrà esito negativo. Ad esempio, Microsoft Visio 2010 viene installato in un client o in un'immagine acquisita. Quando si esegue il passaggio Installa applicazione della sequenza di attività per installare Microsoft Visio 2013, i file di contenuto per Microsoft Visio 2010 (l'applicazione sostituita) devono essere disponibili nel punto di distribuzione. In caso contrario, la sequenza di attività avrà esito negativo. Un client o un'immagine acquisita senza installazione di Microsoft Visio completerà l'installazione di Microsoft Visio 2013 senza verificare i file di contenuto di Microsoft Visio 2010.  

> [!NOTE]
> È possibile usare le variabili SMSTSMPListRequestTimeoutEnabled e SMSTSMPListRequestTimeout predefinite per abilitare e specificare quanti millisecondi una sequenza di attività deve attendere prima di riprovare a installare un'applicazione o un aggiornamento software se non è riuscita a recuperare l'elenco dei punti di gestione dai servizi di posizione. Per altre informazioni, vedere [Variabili predefinite della sequenza di attività](task-sequence-built-in-variables.md).

 Questo passaggio della sequenza di attività può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE.  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare di ripetere questo passaggio se il computer si riavvia in modo imprevisto. È anche possibile specificare la frequenza di tentativi da eseguire in seguito a un riavvio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Installa le seguenti applicazioni**  
 Questa impostazione specifica le applicazioni che vengono installate nell'ordine in cui sono state specificate.  

 Configuration Manager escluderà tramite filtro le applicazioni disabilitate o le applicazioni con le impostazioni seguenti. Queste applicazioni non saranno visualizzate nella finestra di dialogo **Seleziona l'applicazione da installare** .  

-   Solo se un utente è connesso  

-   Esegui con diritti dell'utente  

 **Installa le applicazioni in base all'elenco di variabili dinamiche**  
 Questa impostazione specifica il nome di base per un set di variabili della sequenza di attività definite per una raccolta o per un computer. Queste variabili specificano le applicazioni che verranno installate per tale raccolta o computer. Ogni nome di variabile comprende il nome base comune e un suffisso numerico che inizia con 01. Il valore di ogni variabili deve contenere soltanto il nome dell'applicazione.  

 Per le applicazioni da installare tramite un elenco di variabili dinamiche, è necessario abilitare l'impostazione seguente nella scheda **Generale** della finestra di dialogo **Proprietà** dell'applicazione: **Consenti l'installazione dell'applicazione dall'operazione sequenza di attività Installazione applicazione senza distribuzione**  

> [!NOTE]  
>  Non è possibile installare le applicazioni usando un elenco dinamico di variabili per distribuzioni con supporti autonomi.  

 Ad esempio, per installare una singola applicazione tramite una variabile della sequenza di attività denominata AA01, è necessario specificare la variabile seguente:  

|Nome variabile|Valore variabile|  
|-------------------|--------------------|  
|AA01|Microsoft Office|  

 Per installare due applicazioni, è necessario specificare le variabili seguenti:  

|Nome variabile|Valore variabile|  
|-------------------|--------------------|  
|AA01|Microsoft Lync|  
|AA02|Microsoft Office|  

 Le condizioni seguenti determineranno le applicazioni installate:  

-   Se il valore di una variabile include informazioni diverse dal nome dell'applicazione, l'applicazione non verrà installata e la sequenza di attività continuerà.  

-   Se non viene individuata alcuna variabile con il nome di base specificato e il suffisso "01", non verrà installata alcuna applicazione. Quando si seleziona **Continua in caso di errore** nella scheda Opzioni del passaggio della sequenza di attività, la sequenza di attività continuerà in caso di errore di installazione di un'applicazione. Se l'impostazione non è selezionata, la sequenza di attività avrà esito negativo e non installerà le applicazioni rimanenti.  

 **Se l'installazione di un'applicazione non riesce, continuare installando le altre applicazioni dell'elenco**  
 Questa impostazione specifica che il passaggio procederà in caso di errore di installazione di una singola applicazione. Se si specifica questa impostazione, la sequenza di attività continuerà indipendentemente da eventuali errori di installazione restituiti. Se non si specifica questa impostazione e si verifica un errore di installazione, il passaggio della sequenza di attività si interromperà immediatamente.  

##  <a name="a-namebkmkinstalldeploymenttoolsa-install-deployment-tools"></a><a name="BKMK_InstallDeploymentTools"></a> Installa strumenti di distribuzione  
 Usare il passaggio **Installa strumenti di distribuzione** della sequenza di attività per installare il pacchetto di Configuration Manager contenente gli strumenti di distribuzione Sysprep.  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Pacchetto Sysprep**  
 Questa impostazione specifica il pacchetto di Configuration Manager contenente gli strumenti di distribuzione Sysprep per i sistemi operativi seguenti:  

-   Windows XP SP3  

-   Windows XP X64 SP2  

-   Windows Server 2003 SP2  

##  <a name="a-namebkmkinstallpackagea-install-package"></a><a name="BKMK_InstallPackage"></a> Installa pacchetto

 Usare il passaggio **Installa pacchetto** della sequenza di attività per installare il software come parte della sequenza di attività. Quando si esegue questo passaggio, l'installazione inizia immediatamente, senza attendere il termine dell'intervallo di polling dei criteri.  

 Il software installato deve soddisfare i criteri seguenti:  

-   Deve essere in esecuzione con l'account di sistema locale e non con l'account utente.  

-   Non deve interagire con il desktop. Il programma deve essere eseguito automaticamente o in modalità automatica.  

-   Non deve dare inizio autonomamente a un riavvio. Il software deve richiedere un riavvio usando il codice di riavvio standard, ovvero un codice di uscita 3010. Ciò garantisce che il passaggio della sequenza di attività gestirà correttamente il riavvio. Se il software restituisce un codice di uscita 3010, il motore della sequenza di attività sottostante eseguirà il riavvio. Dopo il riavvio, la sequenza di attività continuerà automaticamente.  

 I programmi che usano l'opzione **Esegui prima un altro programma** per installare un programma dipendente non sono supportati durante la distribuzione di un sistema operativo. Se l'opzione **Esegui prima un altro programma** è abilitata per il software e il programma dipendente è già stato eseguito nel computer di destinazione, il programma dipendente verrà eseguito e la sequenza di attività continuerà. Se tuttavia il programma dipendente non è già stato eseguito nel computer di destinazione, il passaggio della sequenza di attività avrà esito negativo.  

> [!NOTE]  
>  Il sito di amministrazione centrale non dispone dei criteri di configurazione del client necessari per abilitare l'agente di distribuzione software durante l'esecuzione della sequenza di attività. Quando si creano supporti autonomi per una sequenza di attività in un sito di amministrazione centrale e la sequenza di attività include il passaggio **Installa pacchetto** , è possibile che nel file CreateTsMedia.log venga visualizzato il seguente errore:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>   
>  Per un supporto autonomo che include il passaggio Installa pacchetto, è necessario creare il supporto autonomo in un sito primario in cui l'agente di distribuzione software abilitato oppure aggiungere un passaggio **Esegui riga di comando** dopo **Imposta Windows e ConfigMgr** e prima del primo passaggio **Installa pacchetto** . Il passaggio **Esegui riga di comando** esegue un comando WMIC per abilitare l'agente di distribuzione software prima dell'esecuzione del primo passaggio Installa pacchetto. È possibile usare quanto segue nel passaggio della sequenza di attività **Esegui riga di comando** :  
>   
>  **Riga di comando**: **WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE**  
>   
>  Per altre informazioni sulla creazione di supporti autonomi, vedere [Create stand-alone media](../deploy-use/create-stand-alone-media.md) (Creare supporti autonomi).  

 Questo passaggio della sequenza di attività può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE.  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Installa un solo pacchetto software**  
 Questa impostazione specifica un pacchetto software di Configuration Manager. Il passaggio attenderà fino al completamento dell'installazione.  

 **Installa i pacchetti software in base all'elenco di variabili dinamiche**  
 Questa impostazione specifica il nome di base per un set di variabili della sequenza di attività definite per una raccolta o per un computer. Queste variabili specificano i pacchetti che verranno installati per tale raccolta o computer. Ogni nome di variabile comprende il nome base comune e un suffisso numerico che inizia con 001. Il valore di ogni variabile deve includere un ID pacchetto e il nome del software separati da due punti.  

 Per installare un software tramite un elenco di variabili dinamiche, è necessario abilitare l'impostazione seguente nella scheda **Avanzate** della finestra di dialogo **Proprietà** del pacchetto: **Consenti l'installazione di questo programma dalla sequenza di attività Installa pacchetto senza che venga distribuito**  

> [!NOTE]  
>  Non è possibile installare pacchetti software usando un elenco dinamico di variabili per distribuzioni con supporti autonomi.  

 Ad esempio, per installare un singolo pacchetto software tramite una variabile della sequenza di attività denominata AA001, è necessario specificare la variabile seguente:  

|Nome variabile|Valore variabile|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  

 Per installare tre pacchetti software, è necessario specificare le variabili seguenti:  

|Nome variabile|Valore variabile|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  
|AA002|CEN00107:Install Silent|  
|AA003|CEN00031:Install|  

 Le condizioni seguenti determineranno le applicazioni installate:  

-   Se il valore di una variabile non viene creato con il formato corretto o se non specifica un ID e un nome applicazione validi, l'installazione del software avrà esito negativo.  

-   Se l'ID del pacchetto include caratteri minuscoli, l'installazione del software avrà esito negativo.  

-   Se non vengono individuate variabili con il nome di base specificato e con il suffisso "001", non verrà installato alcun pacchetto e la sequenza di attività continuerà.  

 **Se l'installazione di un pacchetto software non riesce, continuare con l'installazione degli altri pacchetti dell'elenco**  
 Questa impostazione specifica che il passaggio procederà in caso di errore di installazione di un singolo pacchetto software. Se si specifica questa impostazione, la sequenza di attività continuerà indipendentemente da eventuali errori di installazione restituiti. Se non si specifica questa impostazione e si verifica un errore di installazione, il passaggio della sequenza di attività si interromperà immediatamente.  

##  <a name="a-namebkmkinstallsoftwareupdatesa-install-software-updates"></a><a name="BKMK_InstallSoftwareUpdates"></a> Installa aggiornamenti software  
 Usare il passaggio **Installa aggiornamenti software** della sequenza di attività per installare aggiornamenti software nel computer di destinazione. Il computer di destinazione viene valutato alla ricerca di aggiornamenti software applicabili solo in corrispondenza con l'esecuzione di questo passaggio della sequenza di attività, A questo punto il computer di destinazione viene valutato per aggiornamenti software come un qualsiasi altro client gestito da Configuration Manager. In particolare, questo passaggio installa solo gli aggiornamenti software destinati a raccolte di cui il computer è attualmente membro.  
>  [!IMPORTANT]
>Per migliori prestazioni con il passaggio della sequenza di attività Installa aggiornamenti software è consigliabile installare l'ultima versione dell'agente Windows Update.
>* Per Windows 7, vedere l'[articolo della Knowledge Base 3161647](https://support.microsoft.com/kb/3161647).
>* Per Windows 8, vedere l'[articolo della Knowledge Base 3163023](https://support.microsoft.com/kb/3163023).

 Questo passaggio della sequenza di attività può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE. Per informazioni sulle variabili della sequenza di attività per questa azione della sequenza di attività, vedere [Install Software Updates Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_InstallSoftwareUpdates).

 > [!NOTE]
 > È possibile usare le variabili SMSTSMPListRequestTimeoutEnabled e SMSTSMPListRequestTimeout predefinite per abilitare e specificare quanti millisecondi una sequenza di attività deve attendere prima di riprovare a installare un'applicazione o un aggiornamento software se non è riuscita a recuperare l'elenco dei punti di gestione dai servizi di posizione. Per altre informazioni, vedere [Variabili predefinite della sequenza di attività](task-sequence-built-in-variables.md).

> [!NOTE]
>Nella scheda Opzioni è possibile configurare questa sequenza di attività per eseguire altri tentativi se il computer si riavvia in modo imprevisto. Ad esempio, l'installazione di un aggiornamento software che riavvia automaticamente il computer. A partire da Configuration Manager 1602, è possibile configurare la variabile SMSTSWaitForSecondReboot per specificare quanti secondi una sequenza di attività deve restare in pausa dopo il riavvio del computer durante l'installazione degli aggiornamenti software. Per altre informazioni, vedere [Variabili predefinite della sequenza di attività](task-sequence-built-in-variables.md).

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare di ripetere questo passaggio se il computer si riavvia in modo imprevisto. È anche possibile specificare la frequenza di tentativi da eseguire in seguito a un riavvio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Necessario per l'installazione - Solo aggiornamenti software obbligatori**  
 Selezionare questa opzione per installare tutti gli aggiornamenti software contrassegnati in Configuration Manager come obbligatori per i computer di destinazione che ricevono la sequenza di attività. Per l'installazione degli aggiornamenti software obbligatori sono previste scadenze definite dagli amministratori.  

 **Disponibile per l'installazione - Tutti gli aggiornamenti software**  
 Selezionare questa opzione per installare tutti gli aggiornamenti software disponibili che fanno riferimento alla raccolta di Configuration Manager che riceverà la sequenza di attività. Tutti gli aggiornamenti software disponibili verranno installati nei computer di destinazione.  

 **Valuta gli aggiornamenti software dai risultati di analisi memorizzati nella cache**  
A partire da Configuration Manager versione 1606, è possibile eseguire un'analisi completa degli aggiornamenti software anziché usare i risultati di analisi memorizzati nella cache. Per impostazione predefinita, la sequenza di attività usa i risultati memorizzati nella cache. È possibile deselezionare la casella di controllo per fare in modo che il client si connetta al punto di aggiornamento software per elaborare e scaricare il catalogo degli aggiornamenti software più recente. È possibile scegliere questa opzione quando si usa una sequenza di attività per [acquisire e creare l'immagine di un sistema operativo](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md) in cui si prevedono numerosi aggiornamenti software, in particolare aggiornamenti con dipendenze, ovvero che richiedono l'installazione di X per poter usare Y. Se si deseleziona questa impostazione e si distribuisce la sequenza di attività in un numero elevato di client, i client si connetteranno tutti contemporaneamente al punto di aggiornamento software. Ciò potrebbe comportare problemi di prestazioni durante il processo e il download del catalogo. Nella maggior parte dei casi, è consigliabile usare l'impostazione predefinita.

In Configuration Manager versione 1606 è stata inserita la nuova variabile di sequenza di attività SMSTSSoftwareUpdateScanTimeout che consente di controllare il timeout dell'analisi degli aggiornamenti software durante il passaggio della sequenza di attività Installa aggiornamenti software. Il valore predefinito è 30 minuti. Per altre informazioni, vedere [Variabili predefinite della sequenza di attività](task-sequence-built-in-variables.md).


##  <a name="a-namebkmkjoindomainorworkgroupa-join-domain-or-workgroup"></a><a name="BKMK_JoinDomainorWorkgroup"></a> Aggiunta a dominio o gruppo di lavoro  
 Usare il passaggio **Aggiunta a dominio o gruppo di lavoro** della sequenza di attività per aggiungere il computer di destinazione a un gruppo di lavoro o a un dominio.  

 Questo passaggio della sequenza di attività può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE. Per informazioni sulle variabili della sequenza di attività per questa azione della sequenza di attività, vedere [Join Domain or Workgroup Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_JoinDomainWorkgroup).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Aggiunta a un gruppo di lavoro**  
 Selezionare questa opzione per aggiungere il computer di destinazione al gruppo di lavoro specificato. Se il computer è attualmente un membro di un dominio, la selezione di questa opzione provocherà il riavvio del computer.  

 **Aggiunta a un dominio**  
 Selezionare questa opzione per aggiungere il computer di destinazione al dominio specificato.  

 Facoltativamente, immettere o selezionare un'unità organizzativa nel dominio specificato a cui aggiungere il computer. Se il computer è attualmente un membro di un altro dominio o un altro gruppo di lavoro, il computer verrà riavviato. Se il computer è già membro di un'altra unità organizzativa, Servizi di dominio Active Directory non permette di cambiare l'unità organizzativa e questa impostazione verrà ignorata.  

 **Immettere l'account con le autorizzazioni per l'aggiunta al dominio**  
 Fare clic su **Imposta** per immettere un account e una password con autorizzazioni per l'aggiunta al dominio. L'account deve essere immesso nel formato seguente:  

 *Dominio\account*  

##  <a name="a-namebkmkprepareconfigmgrclientforcapturea-prepare-configmgr-client-for-capture"></a><a name="BKMK_PrepareConfigMgrClientforCapture"></a> Prepara client ConfigMgr per l'acquisizione  
 Usare il passaggio **Prepara client ConfigMgr per l'acquisizione** per portare il client di Configuration Manager nel computer di riferimento e prepararlo per l'acquisizione come parte del processo di creazione dell'immagine eseguendo le attività seguenti:  

-   Rimozione della sezione relativa alle proprietà di configurazione del client dal file smscfg.ini nella directory Windows. Queste proprietà includono informazioni specifiche dei client, quali il GUID di Configuration Manager e altri identificatori del client.  

-   Eliminazione di tutti i certificati della macchina di SMS e di Configuration Manager.  

-   Eliminazione della cache del client di Configuration Manager.  

-   Cancellazione della variabile di sito assegnato per il client di Configuration Manager.  

-   Installazione di tutti i criteri di Configuration Manager locali.  

-   Rimozione della chiave radice attendibile per il client di Configuration Manager.  

 Questo passaggio della sequenza di attività può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE.  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

##  <a name="a-namebkmkpreparewindowsforcapturea-prepare-windows-for-capture"></a><a name="BKMK_PrepareWindowsforCapture"></a> Prepara Windows per l'acquisizione  
 Usare il passaggio **Prepara Windows per l'acquisizione** della sequenza di attività per specificare le opzioni di Sysprep da usare durante l'acquisizione di un'immagine del sistema operativo nel computer di riferimento. Questa azione della sequenza di attività esegue Sysprep e quindi riavvia il computer nell'immagine di avvio di Windows PE specificata per la sequenza di attività. Per il corretto completamento di questa azione non è necessario che il computer di riferimento sia aggiunto a un dominio.  

 Questo passaggio della sequenza di attività può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE. Per informazioni sulle variabili della sequenza di attività per questa azione della sequenza di attività, vedere [Prepare Windows for Capture Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_PrepareWindowsCapture).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Crea automaticamente l'elenco di driver di archiviazione di massa**  
 Selezionare questa opzione per fare in modo che Sysprep crei automaticamente un elenco di driver di archiviazione di massa dal computer di riferimento. Questa opzione abilita l'opzione per la creazione di driver di archiviazione di massa del file sysprep.inf nel computer di riferimento. Per altre informazioni su questa impostazione, vedere la documentazione relativa a Sysprep.  

 **Non reimpostare il flag di attivazione**  
 Selezionare questa opzione per impedire a Sysprep di reimpostare il flag di attivazione del prodotto.  

##  <a name="a-namebkmkpreprovisionbitlockera-pre-provision-bitlocker"></a><a name="BKMK_PreProvisionBitLocker"></a> BitLocker pre-provisioning  
 Usare il passaggio **BitLocker pre-provisioning** della sequenza di attività per abilitare BitLocker in un'unità in Windows PE. Solo lo spazio su disco usato viene crittografato e pertanto i tempi di crittografia sono molto più veloci. È possibile applicare le opzioni di gestione delle chiavi usando il passaggio [Attiva BitLocker](#BKMK_EnableBitLocker) della sequenza di attività dopo l'installazione del sistema operativo. Questo passaggio può essere eseguito solo in Windows PE. Non può essere eseguito in un sistema operativo standard.  

> [!IMPORTANT]  
>  Per eseguire il pre-provisioning di BitLocker, è necessario distribuire almeno il sistema operativo Windows 7 e TPM deve essere supportato e abilitato nel computer.  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Specificare un nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Specificare informazioni dettagliate sull'azione eseguita in questo passaggio.  

 **Applica BitLocker all'unità specificata**  
 Specificare l'unità per cui si vuole abilitare BitLocker. Viene crittografato solo lo spazio usato sull'unità.  

 **Ignora questo passaggio per computer senza TPM o con TPM non abilitato**  
 Selezionare questa opzione per ignorare la crittografia unità quando l'hardware del computer non supporta TPM o se TPM non è abilitato. È ad esempio possibile usare questa opzione quando si distribuisce un sistema operativo in una macchina virtuale.  

##  <a name="a-namebkmkreleasestatestorea-release-state-store"></a><a name="BKMK_ReleaseStateStore"></a> Rilascia archiviazione stati  
 Usare il passaggio **Rilascia archiviazione stati** della sequenza di attività per segnalare al punto di migrazione stato il completamento dell'azione di acquisizione o ripristino. Questo passaggio viene usato insieme ai passaggi **Richiedi archiviazione stati**, **Acquisisci stato utente**e **Ripristina stato utente** della sequenza di attività per eseguire la migrazione dei dati relativi agli stati utente usando un punto di migrazione stato e l'Utilità di migrazione stato utente (USMT, User State Migration Tool).  

 Per altre informazioni sulla gestione dello stato utente durante la distribuzione di sistemi operativi, vedere [Manage user state](../get-started/manage-user-state.md) (Gestire lo stato utente).  

 Se è stato richiesto l'accesso al punto di migrazione stato per acquisire lo stato utente nel passaggio **Richiedi archiviazione stati**  della sequenza di attività, questo passaggio segnala al punto di migrazione stato che il processo di acquisizione è stato completato che i dati relativi allo stato utente sono disponibili per il ripristino. Il punto di migrazione stato imposta le autorizzazioni di Controllo di accesso per lo stato acquisito, in modo che sia possibile accedervi (sola lettura) solo dal computer di ripristino.  

 Se è stato richiesto l'accesso a un punto di migrazione stato per ripristinare lo stato utente nel passaggio **Richiedi archiviazione stati** della sequenza di attività, questo passaggio della sequenza di attività segnalerà al punto di migrazione stato che il processo di ripristino è stato completato. A questo punto vengono attivate eventuali impostazioni di memorizzazione configurate per il punto di migrazione stato.  

> [!IMPORTANT]  
>  È consigliabile impostare **Continua in caso di errori** in ogni passaggio della sequenza di attività tra il passaggio **Richiedi archiviazione stati** e il passaggio **Rilascia archiviazione stati** , in modo che ogni azione **Richiedi archiviazione stati** della sequenza di attività abbia un'azione **Rilascia archiviazione stati** corrispondente.  

 Questo passaggio della sequenza di attività può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE. Per informazioni sulle variabili della sequenza di attività per questa azione della sequenza di attività, vedere [Release State Store Sequence Action Variables](task-sequence-action-variables.md#BKMK_ReleaseStateStore).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

##  <a name="a-namebkmkrequeststatestorea-request-state-store"></a><a name="BKMK_RequestStateStore"></a> Richiedi archiviazione stati  
 Usare il passaggio **Richiedi archiviazione stati** della sequenza di attività per richiedere l'accesso a un punto di migrazione stato durante l'acquisizione dello stato da un computer o il ripristino dello stato in un computer.  

 Per altre informazioni sulla gestione dello stato utente durante la distribuzione di sistemi operativi, vedere [Manage user state](../get-started/manage-user-state.md) (Gestire lo stato utente).  

 È possibile usare il passaggio **Richiedi archiviazione stati** della sequenza di attività insieme ai passaggi **Rilascia archiviazione stati**, **Acquisisci stato utente**e **Ripristina stato utente** per eseguire la migrazione dello stato del computer usando un punto di migrazione stato e l'Utilità di migrazione stato utente.  

> [!NOTE]  
>  Se è stato appena stabilito un nuovo ruolo del sito del punto di migrazione stato, potrebbe essere necessario attendere fino a un'ora perché sia reso disponibile per l'archiviazione dello stato utente. Per rendere disponibile più rapidamente il punto di migrazione stato, è possibile modificare le impostazioni delle proprietà del punto di migrazione stato, in modo da attivare un aggiornamento del file di controllo del sito.  

 Questo passaggio della sequenza di attività può essere eseguito in un sistema operativo standard e in Windows PE per USMT offline. Per informazioni sulle variabili della sequenza di attività per questa azione della sequenza di attività, vedere [Request State Store Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RequestState).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Acquisisci stato dal computer**  
 Individua un punto di migrazione stato che soddisfa i requisiti minimi definiti nelle impostazioni corrispondenti, ovvero numero massimo di client e quantità minima di spazio disponibile su disco, ma non assicura che sia disponibile spazio sufficiente al momento della migrazione dello stato. Se si seleziona questa opzione, verrà richiesto l'accesso al punto di migrazione stato per permettere l'acquisizione dello stato utente e delle impostazioni da un computer.  

 Se nel sito di Configuration Manager sono abilitati più punti di migrazione stato, questo passaggio della sequenza di attività individua un punto di migrazione stato con spazio su disco disponibile eseguendo una query nel punto di gestione del sito per individuare un elenco di punti di migrazione stato, e valutando poi ogni punto fino a individuare quello che soddisfa i requisiti minimi.  

 **Ripristina stato da un altro computer**  
 Selezionare questa opzione per richiedere l'accesso a un punto di migrazione stato per permettere il ripristino delle impostazioni e dello stato utente acquisiti in precedenza in un computer di destinazione.  

 Se nel sito di Configuration Manager sono presenti più punti di migrazione stato, questo passaggio della sequenza di attività individua il punto di migrazione stato con lo stato computer archiviato per il computer di destinazione.  

 **Numero di tentativi**  
 Numero di tentativi effettuati da questo passaggio della sequenza di attività per trovare un punto di migrazione stato appropriato prima di restituire un esito negativo.  

 **Intervallo tra tentativi (in secondi)**  
 Quantità di tempo, in secondi, di attesa da parte del passaggio della sequenza di attività prima di effettuare nuovi tentativi.  

 **Se l'account del computer non riesce a connettersi all'archiviazione stati, utilizzare l'account di accesso di rete**  
 Specifica che verranno usate le credenziali dell'account di accesso alla rete di Configuration Manager per la connessione al punto di migrazione stato se il client di Configuration Manager non accede all'archiviazione stati del punto di migrazione stato usando l'account del computer. Questa opzione è meno sicura, perché altri computer potrebbero usare l'account di accesso alla rete per accedere ai dati archiviati, ma potrebbe essere necessaria se il computer di destinazione non fa parte del dominio.  

##  <a name="a-namebkmkrestartcomputera-restart-computer"></a><a name="BKMK_RestartComputer"></a> Riavvia computer  
 Usare il passaggio **Riavvia computer** della sequenza di attività per riavviare il computer che esegue la sequenza di attività. Dopo il riavvio, il computer passerà automaticamente al passaggio successivo della sequenza di attività.  

 Questo passaggio può essere eseguito in un sistema operativo standard o in Windows PE. Per altre informazioni sulle variabili della sequenza di attività per questa azione della sequenza di attività, vedere [Variabili di azione della sequenza di attività Riavvia computer](task-sequence-action-variables.md#BKMK_RestartComputer).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **L'immagine d'avvio assegnata a questa sequenza attività**  
 Selezionare questa opzione per il computer di destinazione in modo che usi l'immagine di avvio assegnata alla sequenza di attività. L'immagine di avvio verrà usata per eseguire i passaggi successivi della sequenza di attività in Windows PE.  

 **Il sistema operativo predefinito attualmente installato**  
 Selezionare questa opzione per il computer di destinazione per il riavvio nel sistema operativo installato.  

 **Invia notifica all'utente prima del riavvio**  
 Selezionare questa opzione per visualizzare una notifica all'utente in merito al riavvio del computer di destinazione. Questa opzione è selezionata per impostazione predefinita.  

 **Messaggio di notifica**  
 Immettere un messaggio di notifica che viene visualizzato all'utente prima del riavvio del computer di destinazione.  

 **Timeout della visualizzazione messaggio**  
 Specificare la quantità di tempo, in secondi, che verrà concessa all'utente prima del riavvio del computer di destinazione. La quantità di tempo predefinita è sessanta (60) secondi.  

##  <a name="a-namebkmkrestoreuserstatea-restore-user-state"></a><a name="BKMK_RestoreUserState"></a> Ripristina stato utente  
 Usare il passaggio **Ripristina stato utente** della sequenza di attività per inizializzare l'Utilità di migrazione stato utente e ripristinare lo stato utente e le impostazioni nel computer di destinazione. Questo passaggio della sequenza di attività viene usato insieme al passaggio **Acquisisci stato utente** .  

 Per altre informazioni sulla gestione dello stato utente durante la distribuzione di sistemi operativi, vedere [Manage user state](../get-started/manage-user-state.md) (Gestire lo stato utente).  

 È anche possibile usare il passaggio **Ripristina stato utente** della sequenza di attività insieme ai passaggi **Richiedi archiviazione stati** e **Rilascia archiviazione stati** se si vogliono salvare le impostazioni dello stato o ripristinare tali impostazioni da un punto di migrazione stato nel sito di Configuration Manager. In USMT 3.0 e versioni successive questa opzione decrittografa sempre l'archiviazione stati USMT usando una chiave di crittografia generata e gestita da Configuration Manager.  

 Il passaggio **Ripristina stato utente** della sequenza di attività fornisce il controllo su un sottoinsieme limitato delle opzioni USMT più usate. È possibile specificare opzioni aggiuntive da riga di comando usando la variabile OSDMigrateAdditionalRestoreOptions della sequenza di attività.  

> [!IMPORTANT]  
>  Se si usa il passaggio **Ripristina stato utente** della sequenza di attività per una finalità non correlata a uno scenario di distribuzione del sistema operativo, aggiungere il passaggio [Riavvia computer](#BKMK_RestartComputer) della sequenza di attività immediatamente dopo il passaggio **Ripristina stato utente** .  

 Questo passaggio della sequenza di attività può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE. Per informazioni sulle variabili della sequenza di attività per questa azione della sequenza di attività, vedere [Restore User State Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RestoreUserState).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Specifica un nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Specifica informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Pacchetto degli strumenti di migrazione dello stato utente**  
 Immettere il pacchetto Configuration Manager che contiene la versione di USMT che deve essere usata da questo passaggio durante il ripristino dello stato e delle impostazioni utente. Questo pacchetto non richiede alcun programma. Quando viene eseguito il passaggio della sequenza di attività, verrà usata la versione di USMT disponibile nel pacchetto specificato. Specificare un pacchetto contenente la versione a 32 bit o x64 di USMT, in base all'architettura del sistema operativo in cui si ripristina lo stato.  

 **Ripristina tutti i profili utente acquisiti con le opzioni standard**  
 Ripristina i profili utente acquisiti con le opzioni standard. Per personalizzare le opzioni da ripristinare, selezionare **Personalizza modalità di acquisizione dei profili utente**.  

 **Personalizza le modalità di ripristino dei profili utente**  
 Permette di personalizzare i file da ripristinare nel computer di destinazione. Fare clic su **File** per specificare i file di configurazione nel pacchetto USMT da usare per il ripristino dei profili utente. Per aggiungere un file di configurazione, immettere il nome del file nella casella **Nome file** , quindi fare clic su **Aggiungi**. I file di configurazione che verranno usati per l'operazione sono elencati nel riquadro File. Il file con estensione xml specificato definisce il file utente che verrà ripristinato.  

 **Ripristina profili utente del computer locale**  
 Ripristina i profili utente del computer locale, ovvero non gli utenti di dominio. Sarà necessario assegnare nuove password agli account utente locali ripristinati, poiché non è possibile eseguire la migrazione delle password originali degli account utente locali. Immettere la nuova password nella casella **Password** e confermare la password nella casella **Conferma password** .  

 **Continua se non è possibile ripristinare dei file**  
 Continua a ripristinare lo stato utente e le impostazioni anche se non è possibile ripristinare alcuni file. Questa opzione è attivata per impostazione predefinita. Se si disabilita questa opzione e si rilevano errori durante il ripristino dei file, il passaggio della sequenza di attività verrà interrotto immediatamente con un errore e non tutti i file verranno ripristinati.  

 **Abilita la registrazione dettagliata**  
 Abilitare questa opzione per generare informazioni di file di log più dettagliate. Durante il ripristino dello stato, il file Loadstate.log viene generato e archiviato per impostazione predefinita nella cartella log della sequenza di attività nella cartella \windows\system32\ccm\logs.  

##  <a name="a-namebkmkruncommandlinea-run-command-line"></a><a name="BKMK_RunCommandLine"></a> Esegui riga di comando  
 Usare il passaggio **Esegui riga di comando** della sequenza di attività per eseguire una riga di comando specificata.  

 Questo passaggio può essere eseguito in un sistema operativo standard o in Windows PE. Per informazioni sulle variabili della sequenza di attività per questa azione della sequenza di attività, vedere [Run Command Line Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RunCommand).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Specifica un nome breve definito dall'utente che descrive la riga di comando eseguita.  

 **Descrizione**  
 Specifica informazioni più dettagliate sulla riga di comando eseguita.  

 **Riga di comando**  
 Specifica la riga di comando eseguita. Questo campo è obbligatorio. È consigliabile includere le estensioni del nome file, ad esempio vbs ed exe. Includere tutti i file di impostazione necessari, le opzioni della riga di comando e le altre opzioni.  

 Se non è stata specificata un'estensione per il nome file, Configuration Manager prova a usare le estensioni com, exe e bat. Se il nome file ha un'estensione non eseguibile, Configuration Manager prova ad applicare un'associazione locale. Ad esempio, se la riga di comando è readme.gif, Configuration Manager avvia l'applicazione specificata nel computer di destinazione per l'apertura dei file con estensione gif.  

 Esempi:  

 **setup.exe /a**  

 **cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat**  

> [!NOTE]  
>  Per una corretta esecuzione, le azioni della riga di comando, ad esempio il reindirizzamento dell'output, il piping o la copia, come nell'esempio precedente, devono essere precedute dal comando **cmd.exe /c**.  

 **Disattiva il reindirizzamento del file system a 64 bit**  
 Per impostazione predefinita, quando si esegue un sistema operativo a 64 bit, il file eseguibile nella riga di comando viene individuato ed eseguito usando il redirector del file system WOW64. In questo modo, vengono individuati i file eseguibili del sistema operativo a 32 bit e i DLL.  Selezionando questa opzione viene disabilitato l'uso del ridector del file system WOW64. In questo modo, vengono individuati i file eseguibili del sistema operativo a 64 bit e i DLL.  La selezione di questa opzione non produce effetti quando si esegue un sistema operativo a 32 bit.  

 **Da**  
 Specifica la cartella eseguibile per il programma. Sono consentiti al massimo 127 caratteri. Questa cartella può essere un percorso assoluto nel computer di destinazione o un percorso relativo alla cartella del punto di distribuzione contenente il pacchetto. Questo campo è facoltativo.  

 Esempi:  

 **c:\officexp**  

 **i386**  

> [!NOTE]  
>  Il pulsante **Sfoglia** permette di cercare file e cartelle nel computer locale. Tutti gli elementi selezionati in questo modo devono quindi esistere anche nel computer di destinazione nello stesso percorso e con gli stessi nomi di file e cartelle.  

 **Pacchetto**  
 Quando nella riga di comando si specificano file o programmi che non sono già presenti nel computer di destinazione, selezionare questa opzione per specificare il pacchetto di Configuration Manager contenente i file appropriati. Questo pacchetto non richiede alcun programma. Questa opzione non è necessaria se i file specificati esistono nel computer di destinazione.  

 **Timeout**  
 Specifica un valore per il tempo concesso da Configuration Manager per l'esecuzione della riga di comando. Questo valore può essere compreso tra 10 e 999 minuti. Il valore predefinito è 15 minuti.  

 Questa opzione è disabilitata per impostazione predefinita.  

> [!IMPORTANT]  
>  Se si immette un valore che non concede il tempo necessario per il completamento corretto del passaggio Esegui riga di comando della sequenza di attività, questo passaggio avrà esito negativo ed è possibile che l'intera sequenza di attività abbia esito negativo, in base ad altre impostazioni di controllo. In caso di scadenza del timeout, Configuration Manager interromperà il processo della riga di comando.  

 **Esegui questo passaggio come account specificato**  
 Specifica che la riga di comando viene eseguita come account utente Windows diverso dall'account di sistema locale.  

> [!NOTE]  
>  Quando si specifica un altro account per questo passaggio e ciò avviene dopo un passaggio di installazione del sistema operativo, l'account deve essere aggiunto al computer prima di poter eseguire script o comandi semplici e il profilo per l'account utente di Windows deve essere ripristinato per eseguire programmi più complessi, come un file MSI.  

 **Account**  
 Specifica l'account utente Windows RunAs per l'attività della riga di comando nella sequenza di attività che deve essere eseguita da questa azione. La riga di comando verrà eseguita con le autorizzazioni dell'account specificato. Fare clic su **Imposta** per specificare l'utente locale o l'account di dominio.  

> [!IMPORTANT]  
>  Se un'azione **Esegui riga di comando** della sequenza di attività che specifica un account utente viene eseguita in Windows PE, l'azione avrà esito negativo poiché Windows PE non può essere aggiunto a un dominio. L'errore verrà registrato nel file smsts.log.  

##  <a name="a-namebkmkrunpowershellscripta-run-powershell-script"></a><a name="BKMK_RunPowerShellScript"></a> Esegui script PowerShell  
 Usare il passaggio **Esegui script PowerShell** della sequenza di attività per eseguire uno script PowerShell specificato.  

 Questo passaggio può essere eseguito in un sistema operativo standard o in Windows PE. Per eseguire questo passaggio in Windows PE, è necessario abilitare PowerShell nell'immagine di avvio. È possibile abilitare Windows PowerShell (WinPE-PowerShell) dalla scheda **Componenti facoltativi** nelle proprietà per l'immagine di avvio. Per altre informazioni su come modificare un'immagine d'avvio, vedere [Manage boot images](../get-started/manage-boot-images.md) (Gestire le immagini d'avvio).  

> [!NOTE]  
>  PowerShell non è abilitato per impostazione predefinita nei sistemi operativi Windows Embedded.  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Specifica un nome breve definito dall'utente che descrive la riga di comando eseguita.  

 **Descrizione**  
 Specifica informazioni più dettagliate sulla riga di comando eseguita.  

 **Pacchetto**  
 Specifica il pacchetto di Configuration Manager contenente lo script PowerShell. Un pacchetto può includere più script PowerShell.  

 **Nome script**  
 Specifica il nome dello script PowerShell da eseguire. Questo campo è obbligatorio.  

 **Parametri**  
 Specifica i parametri da passare allo script Windows PowerShell. Configurare i parametri come se li si stesse aggiungendo allo script Windows PowerShell da una riga di comando.  

> [!IMPORTANT]  
>  Specificare i parametri usati dallo script, non per la riga di comando di Windows PowerShell.  
>   
>  L'esempio seguente include parametri validi:  
>   
>  **-MyParameter1 MyValue1 -MyParameter2 MyValue2**  
>   
>  L'esempio seguente include parametri non validi: Gli elementi in grassetto sono parametri della riga di comando di Windows PowerShell (-nologo ed –executionpolicy unrestricted) e non vengono usati dallo script.  
>   
>  **-nologo-executionpolicy unrestricted-File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2**  

 **Criteri di esecuzione di PowerShell**  
 La selezione dei Criteri di esecuzione di PowerShell permette di specificare gli eventuali script di Windows PowerShell che saranno autorizzati all'esecuzione nel computer. Scegliere uno dei criteri di esecuzione seguenti:  

-   **Tutti firmati**: è possibile eseguire solo gli script firmati da un editore attendibile.  

-   **Non definito**: non sono stati definiti criteri di esecuzione. .  

-   **Ignora**: carica tutti i file di configurazione ed esegue tutti gli script. Se si esegue uno script non firmato scaricato da Internet, non verrà richiesta alcuna autorizzazione prima dell'esecuzione.  

> [!IMPORTANT]  
>  PowerShell 1.0 non supporta i criteri di esecuzione Non definito e Ignora.  

##  <a name="a-namebkmksetdynamicvariablesa-set-dynamic-variables"></a><a name="BKMK_SetDynamicVariables"></a> Imposta variabili dinamiche  
 Usare il passaggio **Imposta variabili dinamiche** della sequenza di attività per eseguire le operazioni seguenti:  

1.  Recupero di informazioni dal computer e dall'ambiente in cui si trova, quindi impostazione delle variabili specificate della sequenza di attività con le informazioni ottenute.  

2.  Valutazione delle regole definite e impostazione delle variabili della sequenza di attività in base ai valori configurati per le regole che restituiscono true.  

 La sequenza di attività imposta automaticamente le variabili della sequenza di attività di sola lettura seguenti:  

-   _SMSTSMake  

-   _SMSTSModel  

-   _SMSTSMacAddresses  

-   _SMSTSIPAddresses  

-   _SMSTSSerialNumber  

-   _SMSTSAssetTag  

-   _SMSTSUUID  

 Questo passaggio può essere eseguito in un sistema operativo standard o in Windows PE. Per altre informazioni sulle variabili della sequenza di attività, vedere [Variabili di azione della sequenza di attività](task-sequence-action-variables.md).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente per questo passaggio della sequenza di attività.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Variabili e regole dinamiche**  
 Per configurare una variabile dinamica da usare nella sequenza di attività, è possibile aggiungere una regola e quindi specificare un valore per ogni variabile specificata per la regola oppure aggiungere una o più variabili da impostare senza aggiungere una regola. Quando si aggiunge una regola, è possibile scegliere tra le categorie delle regole seguenti:  

-   **Computer**: usare questa categoria delle regole per valutare i valori per Tag asset, UUID, Numero di serie o Indirizzo MAC. È possibile configurare più valori e, se un valore restituisce true, la regola restituirà true. La regola seguente, ad esempio, restituisce true se Numero di serie è 5892087, indipendentemente dal fatto che Indirizzo MAC sia 26-78-13-5A-A4-22.  

     `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

-   **Percorso**: usare questa categoria delle regole per valutare i valori per il gateway predefinito.  

-   **Marca e modello**: usare questa categoria delle regole per valutare i valori relativi a marca e modello di un computer. La regola restituisce true solo se entrambi i valori restituiscono true.  

-   **Variabile della sequenza di attività**: usare questa categoria delle regole per aggiungere una variabile della sequenza di attività, una condizione e un valore da valutare. La regola restituisce true quando il valore impostato per la variabile soddisfa la condizione specificata.  

 È possibile specificare una o più variabili che verranno impostate per una regola che restituisce true oppure impostare variabili senza usare una regola. È possibile selezionare una delle variabili esistenti o creare una variabile personalizzata.  

-   **Variabili della sequenza di attività disponibili**: usare questa impostazione per selezionare una o più variabili da un elenco di variabili esistenti della sequenza di attività. Le variabili di matrice non sono disponibili per la selezione.  

-   **Variabili personalizzate della sequenza di attività**: usare questa impostazione per definire una variabile personalizzata della sequenza di attività. È anche possibile specificare una variabile esistente della sequenza di attività. Ciò risulta utile per specificare una matrice di variabili esistente, ad esempio OSDAdapter, poiché le matrici di variabili non sono incluse nell'elenco di variabili esistenti della sequenza di attività.  

 Dopo la selezione delle variabili per una regola, è necessario fornire un valore per ogni variabile. La variabile è impostata sul valore specificato quando la regola restituisce true. Per ogni variabile è possibile selezionare **Valore segreto** per nascondere il valore della variabile. Per impostazione predefinita, alcune variabili esistenti nascondono i valori, ad esempio la variabile OSDCaptureAccountPassword della sequenza di attività.  

> [!IMPORTANT]  
>  Quando si importa una sequenza di attività con il passaggio Imposta variabili dinamiche e **Valore segreto** è selezionato per il valore della variabile, il valore verrà rimosso quando si importa la sequenza di attività. Sarà quindi necessario immettere di nuovo il valore per la variabile dinamica dopo l'importazione della sequenza di attività.  

##  <a name="a-namebkmksettasksequencevariablea-set-task-sequence-variable"></a><a name="BKMK_SetTaskSequenceVariable"></a> Imposta variabile della sequenza di attività  
 Usare il passaggio **Imposta variabile della sequenza di attività** della sequenza di attività per configurare il valore di una variabile usata con la sequenza di attività.  

 Questo passaggio può essere eseguito in un sistema operativo standard o in Windows PE. Le variabili della sequenza di attività vengono lette dalle azioni della sequenza di attività e specificano il comportamento di tali azioni. Per altre informazioni sulle variabili di una sequenza di attività specifica, vedere [Variabili di azione della sequenza di attività](task-sequence-action-variables.md).  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente per questo passaggio della sequenza di attività.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Variabile della sequenza di attività**  
 Valore definito dall'utente per la variabile della sequenza di attività.  

 **Valore**  
 Valore associato alla variabile della sequenza di attività. Il valore può essere un'altra variabile della sequenza di attività con la sintassi %<varname\>%.  

##  <a name="a-namebkmksetupwindowsandconfigmgra-setup-windows-and-configmgr"></a><a name="BKMK_SetupWindowsandConfigMgr"></a> Imposta Windows e ConfigMgr  
 Usare il passaggio **Imposta Windows e ConfigMgr** della sequenza di attività per eseguire la transizione da Windows PE al nuovo sistema operativo. Questo passaggio della sequenza di attività è una parte necessaria di qualsiasi distribuzione del sistema operativo. Installa il client di Configuration Manager nel nuovo sistema operativo e prepara la sequenza di attività per continuare l'esecuzione nel nuovo sistema operativo.  

 Questo passaggio può essere eseguito solo in Windows PE. Non può essere eseguito in un sistema operativo standard. Per altre informazioni sulle variabili della sequenza di attività per questa azione della sequenza di attività, vedere [Variabili di azione della sequenza di attività Imposta Windows e ConfigMgr](task-sequence-action-variables.md#BKMK_SetupWindows).  

 L'azione **Imposta Windows e ConfigMgr** della sequenza di attività sostituisce le variabili della directory sysprep.inf o unattend.xml, ad esempio %WINDIR% e %ProgramFiles%, con la directory di installazione di Windows PE X:\Windows. Le variabili della sequenza di attività specificate usando queste variabili di ambiente verranno ignorate.  

 Usare questo passaggio della sequenza di attività per eseguire le azioni seguenti:  

1.  Operazioni preliminari: Windows PE  

    1.  Esegue la sostituzione delle variabili della sequenza di attività nel file unattend.xml.  

    2.  Scarica il pacchetto che contiene il client di Configuration Manager e lo inserisce nell'immagine distribuita.  

2.  Configurazione di Windows  

    1.  Installazione basata su immagine.  

        1.  Disabilita il client di Configuration Manager nell'immagine, vale a dire disabilita l'avvio automatico del servizio client di Configuration Manager.  

        2.  Aggiornamento del Registro di sistema nell'immagine distribuita per assicurare che il sistema operativo distribuito venga avviato con la stessa lettera di unità usata nel computer di riferimento.  

        3.  Riavvio nel sistema operativo distribuito.  

        4.  L'installazione minima di Windows viene eseguita usando un file sysprep.inf o unattend.xml specificato in precedenza e in cui sono state rimosse tutte le interazioni con gli utenti finali. Nota: se in **Applica impostazioni di rete** è stata specificata l'aggiunta a un dominio, le informazioni saranno disponibili nel file sysprep.inf o unattend.xml e l'installazione minima di Windows eseguirà l'aggiunta al dominio.  

    2.  Installazione basata su Setup.exe.  Esegue Setup.exe con il processo di installazione di Windows tipico:  

        1.  Copia del pacchetto di installazione del sistema operativo specificato in una sequenza di attività **Applica sistema operativo** precedente nell'unità disco rigido.  

        2.  Riavvio nel sistema operativo appena distribuito.  

        3.  L'installazione minima di Windows viene eseguita usando il file sysprep.inf o unattend.xml specificato in precedenza e in cui sono state rimosse tutte le impostazioni dell'interfaccia utente. Nota: se in **Applica impostazioni di rete** è stata specificata l'aggiunta a un dominio, le informazioni saranno disponibili nel file sysprep.inf o unattend.xml e l'installazione minima di Windows eseguirà l'aggiunta al dominio.  

3.  Impostazione del client di Configuration Manager  

    1.  Al termine dell'installazione minima di Windows, verrà ripresa la sequenza di attività usando setupcomplete.cmd.  

    2.  Abilitazione o disabilitazione dell'account di amministratore locale, in base all'opzione selezionata nel passaggio **Applica impostazioni Windows** .  

    3.  Installazione del client di Configuration Manager tramite il pacchetto scaricato in precedenza (1.b) e le proprietà di installazione specificate nell'editor delle sequenze di attività. Il client viene installato in "modalità di provisioning" per impedire l'elaborazione di nuove richieste di criteri fino al completamento della sequenza di attività.  

    4.  Attesa della completa operatività del client.  

    5.  Se il computer opera in un ambiente in cui è abilitata la Protezione accesso alla rete, il client cercherà e installerà eventuali aggiornamenti obbligatori, in modo che tutti gli aggiornamenti obbligatori siano presenti prima della continuazione dell'esecuzione della sequenza di attività.  

4.  L'esecuzione della sequenza di attività continuerà con il passaggio successivo.  

> [!NOTE]  
>  L'azione **Imposta Windows e ConfigMgr** della sequenza di attività è responsabile per l'esecuzione di Criteri di gruppo nel computer appena installato. I Criteri di gruppo vengono applicati al termine della sequenza di attività.  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Non selezionare l'opzione che consente alla sequenza di attività di continuare in caso di errore durante l'esecuzione del passaggio. Se si verifica un errore, la sequenza di attività ha esito negativo, indipendentemente dalla selezione dell'impostazione.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Specifica un nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Specifica informazioni aggiuntive sull'azione effettuata in questo passaggio.  

 **Pacchetto client**  
 Specifica il pacchetto di installazione del client di Configuration Manager che verrà usato da questo passaggio della sequenza di attività. Fare clic su **Sfoglia** e selezionare il pacchetto di installazione del client da usare per installare il client di Configuration Manager.  

 **Usa il pacchetto client di pre-produzione se disponibile**  
 Specifica che se è disponibile un pacchetto client di pre-produzione, il passaggio della sequenza di attività userà tale pacchetto invece del pacchetto client di produzione. In genere, il client di pre-produzione è una versione più recente in corso di testing nell'ambiente di produzione. Fare clic su **Sfoglia** e selezionare il pacchetto di installazione del client di pre-produzione da usare per installare il client di Configuration Manager.  

 **Proprietà di installazione**  
 L'assegnazione sito e la configurazione predefinita vengono specificate automaticamente dall'azione della sequenza di attività. È possibile usare questo campo per specificare eventuali proprietà di installazione aggiuntive da usare quando si installa il client. Per immettere più proprietà di installazione, separarle con uno spazio.  

 È possibile specificare opzioni della riga di comando da usare durante l'installazione del client. Ad esempio, è possibile immettere **/skipprereq: silverlight.exe** per segnalare a CCMSetup.exe di non installare i prerequisiti di Microsoft Silverlight. Per altre informazioni sulle opzioni della riga di comando disponibili per CCMSetup.exe, vedere [About client installation properties](../../core/clients/deploy/about-client-installation-properties.md) (Informazioni sulle proprietà di installazione del client).  

##  <a name="a-namebkmkupgradeosa-upgrade-operating-system"></a><a name="BKMK_UpgradeOS"></a> Aggiorna sistema operativo  
 Usare il passaggio della sequenza di attività **Aggiorna sistema operativo** per aggiornare un sistema operativo esistente Windows 7, Windows 8, Windows 8.1 o Windows 10 a Windows 10.  

 Questo passaggio della sequenza di attività può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE.  

### <a name="details"></a>Dettagli  
 Nella scheda **Proprietà** per questo passaggio è possibile configurare le impostazioni illustrate in questa sezione.  

 È anche possibile usare la scheda **Opzioni** per eseguire le operazioni seguenti:  

-   Disabilitare il passaggio.  

-   Specificare se la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  

-   Specificare le condizioni che devono essere soddisfatte per l'esecuzione del passaggio.  

 **Nome**  
 Nome breve definito dall'utente, che descrive l'azione eseguita in questo passaggio.  

 **Descrizione**  
 Informazioni più dettagliate sull'azione eseguita in questo passaggio.  

 **Pacchetto di aggiornamento**  
 Selezionare questa opzione per specificare il pacchetto di aggiornamento del sistema operativo Windows 10 da usare per l'aggiornamento.  

 **Percorso di origine**  
 Specifica il percorso locale o di rete per il supporto di Windows 10 da usare (corrisponde all'opzione della riga di comando /installFrom). È anche possibile specificare una variabile, ad esempio %mycontentpath% o %DPC01%. Quando si usa una variabile per il percorso di origine, deve essere specificata prima nella sequenza di attività. Ad esempio, se si usa il passaggio [Scaricare il contenuto del pacchetto](#BKMK_DownloadPackageContent) nella sequenza di attività, è possibile specificare una variabile per il percorso del pacchetto di aggiornamento del sistema operativo. È quindi possibile usare tale variabile per il percorso di origine per questo passaggio.  

 **Edizione**  
 Specificare l'edizione all'interno del supporto del sistema operativo da usare per l'aggiornamento.  

 **Codice Product Key**  
 Specificare il codice Product Key da applicare al processo di aggiornamento  

 **Specifica il seguente contenuto del driver in Installazione di Windows durante l'aggiornamento**  
 Selezionare questa impostazione per aggiungere driver nel computer di destinazione durante il processo di aggiornamento (corrisponde all'opzione della riga di comando /InstallDriver). I driver devono essere compatibili con Windows 10. Specificare una delle opzioni seguenti:  

-   **Pacchetto driver**: fare clic su **Sfoglia** e selezionare un pacchetto di driver esistente nell'elenco.  

-   **Contenuto preconfigurato**: selezionare questa opzione per specificare il percorso per il pacchetto di driver. È possibile specificare una cartella locale, un percorso di rete o una variabile della sequenza di attività. Quando si usa una variabile per il percorso di origine, deve essere specificata prima nella sequenza di attività. Ad esempio, usando il passaggio [Download Package Content](task-sequence-steps.md#BKMK_DownloadPackageContent) .  

 **Timeout (minuti)**  
 Specifica il numero di minuti concesso all'installazione, prima che Configuration Manager consideri il passaggio della sequenza di attività come non riuscito.  

 **Esegui analisi di compatibilità di Installazione di Windows senza avviare l'aggiornamento**  
 Specifica di eseguire l'analisi di compatibilità di Installazione di Windows senza avviare il processo di aggiornamento (corrisponde all'opzione della riga di comando /Compat ScanOnly). Quando si usa questa opzione, è ancora necessario distribuire l'intera origine di installazione. Il programma di installazione restituisce un codice di uscita come risultato dell'analisi. Nella tabella seguente sono elencati alcuni dei più comuni codici di uscita.  

|Codice di uscita|Dettagli|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|Nessun problema di compatibilità ("esito positivo").|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|Problemi di compatibilità su cui è possibile intervenire.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|L'opzione di migrazione selezionata non è disponibile. Ad esempio, un aggiornamento da Enterprise a Professional.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Non idoneo per Windows 10.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|Spazio libero su disco insufficiente.|  

 Per altre informazioni su questo parametro, vedere [Opzioni della riga di comando di Installazione di Windows](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx)  

 **Ignora tutti i messaggi sulla compatibilità non rilevanti**  
 Specifica che il programma di installazione deve completare l'installazione, ignorando eventuali messaggi di compatibilità non rilevanti (corrisponde all'opzione della riga di comando /Compat IgnoreWarning).  

 **Aggiorna dinamicamente Installazione di Windows con Windows Update**  
 Specifica se il programma di installazione eseguirà operazioni di aggiornamento dinamico, ad esempio ricerca, download e installazione di aggiornamenti (corrisponde all'opzione della riga di comando /DynamicUpdate). Questa impostazione non è compatibile con gli aggiornamenti software di Configuration Manager, ma può essere abilitata quando si gestiscono gli aggiornamenti tramite WSUS (autonomo) o Windows Update.  

 **Sostituisci i criteri e usa Microsoft Update predefinito**: selezionare questa impostazione per ignorare temporaneamente i criteri locali in tempo reale per eseguire le operazioni di aggiornamento dinamico e impostare il computer per la ricezione degli aggiornamenti da Windows Update.  



<!--HONumber=Nov16_HO1-->



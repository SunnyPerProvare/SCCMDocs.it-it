---
title: "Passaggi della sequenza di attività"
titleSuffix: Configuration Manager
description: "Informazioni sui passaggi della sequenza di attività che è possibile aggiungere a una sequenza di attività di Configuration Manager."
ms.custom: na
ms.date: 01/12/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
caps.latest.revision: 
caps.handback.revision: 
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 158817547d40f09fb8bd30ebedd5aea6420a8571
ms.sourcegitcommit: aee9ac45c15f27d8cf827890edcae94c03f5fd5e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/29/2018
---
# <a name="task-sequence-steps-in-system-center-configuration-manager"></a>Passaggi della sequenza di attività in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

A una sequenza di attività di Configuration Manager è possibile aggiungere i passaggi seguenti. Per informazioni sulla modifica di una sequenza di attività, vedere [Edit a task sequence](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

Le impostazioni seguenti sono comuni a tutti i passaggi della sequenza di attività:

Nella scheda **Proprietà**:
 - **Nome**: l'editor della sequenza di attività richiede di specificare un nome breve per descrivere questo passaggio. Quando si aggiunge un nuovo passaggio, per impostazione predefinita l'editor della sequenza di attività imposta come nome il valore di Tipo. La lunghezza di **Nome** non può superare i 50 caratteri.
 - **Descrizione**: facoltativamente, aggiungere informazioni più dettagliate sul passaggio. La lunghezza di **Descrizione** non può superare i 256 caratteri.
La parte restante di questo articolo descrive le altre impostazioni della scheda **Proprietà** per ogni passaggio della sequenza di attività.

Nella scheda **Opzioni**:  
-   **Disattiva questo passaggio**: la sequenza di attività ignora questo passaggio quando viene eseguita in un computer. L'icona del passaggio è disattivata nell'editor della sequenza di attività. 
-   **Continua in caso di errori**: la sequenza di attività continua in caso di errore durante l'esecuzione del passaggio.  
-   **Aggiungi condizione**: la sequenza di attività valuta queste istruzioni condizionali per determinare se il passaggio viene eseguito.   
Le sezioni seguenti relative a passaggi specifici della sequenza di attività descrivono altre impostazioni possibili della scheda **Opzioni**.



##  <a name="BKMK_ApplyDataImage"></a> Applica immagine dei dati   
 Usare questo passaggio per copiare l'immagine dei dati nella partizione di destinazione specificata.  

 Questo passaggio può essere eseguito solo in Windows PE. Non può essere eseguito in un sistema operativo standard. Per altre informazioni sulle variabili della sequenza di attività, vedere [Variabili di azione delle sequenze di attività in System Center Configuration Manager](task-sequence-action-variables.md).  

Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Immagini** e selezionare **Applica immagine dei dati** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Pacchetto immagine**  
 Fare clic su **Sfoglia** per specificare il **Pacchetto immagine** usato da questa sequenza di attività. Selezionare il pacchetto da installare nella finestra di dialogo **Seleziona un pacchetto** . Le informazioni sulle proprietà associate per ogni pacchetto immagine esistente sono visualizzate nella parte inferiore della finestra di dialogo **Seleziona un pacchetto** . Usare l'elenco a discesa per selezionare l' **Immagine** da installare dal pacchetto **Pacchetto immagine**selezionato.  

> [!NOTE]  
>  Questa azione della sequenza di attività considera l'immagine come un file di dati. Questa azione non esegue nessuna configurazione per avviare l'immagine come un sistema operativo.  

 **Destinazione**  
 Configurare una delle opzioni seguenti:

-   **Next available partition** (Partizione disponibile successiva): usare la partizione sequenziale successiva non ancora sottoposta a un'azione **Applica sistema operativo** o **Applica immagine dei dati** in questa sequenza di attività.  

-   **Disco e partizione specifici**: selezionare un numero per **Disco** (a partire da 0) e per **Partizione** (a partire da 1).  

-   **Lettera unità logica specifica**: specificare la **Lettera unità** assegnata alla partizione da Windows PE. Questa lettera di unità può essere diversa da quella assegnata dal sistema operativo appena distribuito.  

-   **Lettera unità logica archiviata in una variabile**: specificare la variabile della sequenza di attività contenente la lettera di unità assegnata alla partizione da Windows PE. Questa variabile viene in genere impostata nella sezione Avanzate della finestra di dialogo **Proprietà della partizione** per l'azione **Formato e disco partizione** della sequenza di attività.  

**Elimina tutti i contenuti nella partizione prima di applicare l'immagine**  
 Specifica che la sequenza di attività elimina tutti i file nella partizione di destinazione prima di installare l'immagine. Non eliminando il contenuto della partizione, questo passaggio può essere usato per applicare contenuti aggiuntivi a una partizione interessata in precedenza da questa attività.  



##  <a name="BKMK_ApplyDriverPackage"></a> Applica pacchetto di driver  
 Usare questo passaggio per scaricare tutti i driver del pacchetto di driver e installarli nel sistema operativo Windows.

 Il passaggio **Applica pacchetto di driver** della sequenza di attività rende disponibili tutti i driver di dispositivo inclusi in un pacchetto di driver per l'uso da parte di Windows. Aggiungere questo passaggio tra i passaggi **Applica sistema operativo** e **Imposta Windows e ConfigMgr** per rendere disponibili a Windows i driver inclusi nel pacchetto. In genere, il passaggio **Applica pacchetto di driver** viene posizionato dopo il passaggio **Applica automaticamente i driver** della sequenza di attività. Il passaggio **Applica pacchetto di driver** della sequenza di attività è utile anche negli scenari di distribuzione di supporti autonomi.  

 Assicurarsi che i driver di dispositivi simili siano inseriti in un pacchetto di driver e quindi distribuirli nei punti di distribuzione appropriati. Dopo la distribuzione dei driver i computer client di Configuration Manager possono installarli. Ad esempio, inserire tutti i driver di un determinato produttore in un pacchetto di driver. Quindi distribuire il pacchetto in punti di distribuzione accessibili ai computer associati.

 Il passaggio **Applica pacchetto di driver** è utile per i supporti autonomi. Questo passaggio è utile anche per installare un set di driver specifico. Questi tipi di driver includono i dispositivi che non vengono rilevati in una scansione plug and play, quali le stampanti di rete.  

 Questo passaggio della sequenza di attività può essere eseguito solo in Windows PE. Non può essere eseguito in un sistema operativo standard. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Apply Driver Package Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyDriverPackage).  

Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Driver** e selezionare **Applica pacchetto di driver** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Pacchetto driver**  
 Specificare il pacchetto di driver contenente i driver di dispositivo necessari, facendo clic su **Sfoglia** e aprendo la finestra di dialogo **Seleziona un pacchetto** . Specificare un pacchetto esistente da rendere disponibile. Le proprietà associate del pacchetto vengono visualizzate nella parte inferiore della finestra di dialogo.  

 **Selezionare il driver di archiviazione di massa nel pacchetto da installare prima che Configuration Manager installi i sistemi operativi Windows precedenti a Windows Vista**  
 Specificare gli eventuali driver di archiviazione di massa necessari per installare un sistema operativo classico.  

 **Driver**  
 Selezionare il file del driver di archiviazione di massa da installare prima dell'installazione di un sistema operativo classico. L'elenco a discesa viene popolato dal pacchetto specificato.  

 **Model**  
 Specificare il dispositivo critico per l'avvio necessario per le distribuzioni di sistemi operativi precedenti a Windows Vista.  

 **Esegui l'installazione automatica dei driver senza firma sulle versioni di Windows in cui è consentito**  
 Questa opzione consente a Windows di installare driver senza firma digitale.  



##  <a name="BKMK_ApplyNetworkSettings"></a> Applica impostazioni di rete   
 Usare questo passaggio per specificare le informazioni di configurazione della rete o del gruppo di lavoro per il computer di destinazione. La sequenza di attività archivia questi valori nel file di risposte appropriato. Installazione di Windows usa questo file di risposte durante l'azione **Imposta Windows e ConfigMgr**.  

 Questo passaggio della sequenza di attività viene eseguito in un sistema operativo standard o in Windows PE. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Apply Network Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyNetworkSettings).  

 Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Impostazioni** e selezionare **Applica impostazioni di rete** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Aggiunta a un gruppo di lavoro**  
 Selezionare questa opzione per aggiungere il computer di destinazione al gruppo di lavoro specificato. Immettere il nome del gruppo di lavoro nella riga **Gruppo di lavoro** . Questo valore può essere sostituito dal valore acquisito dal passaggio **Acquisisci impostazioni di rete** della sequenza di attività.  

 **Aggiunta a un dominio**  
 Selezionare questa opzione per aggiungere il computer di destinazione al dominio specificato. Specificare o selezionare il dominio, ad esempio *fabricam.com*. Specificare o selezionare un percorso LDAP (Lightweight Directory Access Protocol) per un'unità organizzativa. Ad esempio: *LDAP//OU=computers, DC=Fabricam.com, C=com*  

 **Account**  
 Fare clic su **Imposta** per specificare un account con le autorizzazioni necessarie per l'aggiunta del computer al dominio. Nella finestra di dialogo **Account utente di Windows** è possibile immettere il nome utente usando il formato seguente: **Dominio\Utente** .  

 **Impostazioni della scheda**  
 Specificare le configurazioni di rete per ogni scheda di rete nel computer. Fare clic su **Nuovo** per aprire la finestra di dialogo **Impostazioni di rete** , quindi specificare le impostazioni di rete. Se si usa anche il passaggio **Acquisisci impostazioni di rete**, la sequenza di attività applica le impostazioni acquisite in precedenza alla scheda di rete. La sequenza di attività non applica le impostazioni specificate in questo passaggio. Se la sequenza di attività non ha acquisito in precedenza le impostazioni di rete, applica le impostazioni specificate nel passaggio **Applica impostazioni di rete**. La sequenza di attività applica queste impostazioni alle schede di rete nell'ordine dell'enumerazione dispositivi di Windows.  



##  <a name="BKMK_ApplyOperatingSystemImage"></a> Applica immagine del sistema operativo  

> [!TIP]  
> A partire da Windows 10 versione 1709 il supporto include più edizioni. Quando si configura una sequenza di attività per l'uso di un pacchetto di aggiornamento del sistema operativo o di un'immagine del sistema operativo, verificare di selezionare un'[edizione supportata](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).

 Usare questo passaggio per installare un sistema operativo nel computer di destinazione. Questo passaggio esegue azioni diverse a seconda che si usi un'immagine del sistema operativo o un pacchetto di aggiornamento del sistema operativo.  

 Il passaggio **Applica immagine del sistema operativo** esegue le azioni seguenti quando si usa un'immagine del sistema operativo:  

1.  Eliminare tutto il contenuto del volume interessato, ad eccezione dei file nella cartella specificata dalla variabile &#95;SMSTSUserStatePath.

2.  Estrarre i contenuti del file con estensione wim specificato nella partizione di destinazione specificata.  

3.  Preparare il file di risposte:  

    1.  Creare un nuovo file di risposte predefinito del programma di installazione di Windows (sysprep.inf o unattend.xml) per il sistema operativo che viene distribuito.  

    2.  Unire eventuali valori disponibili nel file di risposte specificato dall'utente.  

4.  Copiare i caricatori di avvio di Windows nella partizione attiva.  

5.  Configurare il file boot.ini o i dati di configurazione di avvio in modo che facciano riferimento al sistema operativo appena installato.  

 Il passaggio **Applica immagine del sistema operativo** esegue le azioni seguenti quando si usa un pacchetto di aggiornamento del sistema operativo:  

1.  Eliminare tutto il contenuto del volume interessato, ad eccezione dei file nella cartella specificata dalla variabile &#95;SMSTSUserStatePath.  

2.  Preparare il file di risposte:  

    1.  Creare un nuovo file di risposte con valori standard generati da Configuration Manager.  

    2.  Unire eventuali valori disponibili nel file di risposte specificato dall'utente.  

> [!NOTE]  
>  Il passaggio **Imposta Windows e ConfigMgr** avvia l'installazione di Windows. 

 Dopo l'esecuzione del passaggio **Applica sistema operativo** la variabile OSDTargetSystemDrive viene impostata sulla lettera di unità della partizione che include i file del sistema operativo.  

 Questo passaggio della sequenza di attività può essere eseguito solo in Windows PE. Non può essere eseguito in un sistema operativo standard. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Apply Operating System Image Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyOperatingSystem).  

 Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Immagini** e selezionare **Applica immagine del sistema operativo** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Applica sistema operativo da un'immagine acquisita**  
 Installa un'immagine del sistema operativo acquisita in precedenza. Fare clic su **Sfoglia** per aprire la finestra di dialogo **Seleziona un pacchetto** , quindi selezionare il pacchetto immagine esistente da installare. Se al **Pacchetto immagine**specificato sono associate più immagini, usare l'elenco a discesa per specificare l'immagine associata da usare per questa distribuzione. Per visualizzare le informazioni di base su ogni immagine esistente, fare clic sull'immagine.  

 **Applica sistema operativo da un'origine di installazione originale**  
 Installa un sistema operativo usando un'origine di installazione originale. Fare clic su **Sfoglia** per aprire la finestra di dialogo **Seleziona un pacchetto di installazione del sistema operativo**. Selezionare quindi il pacchetto di aggiornamento del sistema operativo esistente da usare. Per visualizzare le informazioni di base su ogni immagine esistente, fare clic sull'origine dell'immagine. Le proprietà associate dell'origine dell'immagine vengono visualizzate nel riquadro dei risultati nella parte inferiore della finestra di dialogo. Se al pacchetto specificato sono associate più edizioni, usare l'elenco a discesa per specificare l' **Edizione** associata usata.  

 **Utilizza un file di risposta automatica o Sysprep per un'installazione personalizzata**  
 Usare questa opzione per fornire un file di risposte del programma di installazione di Windows (**unattend.xml**, **unattend.txt**o **sysprep.inf**), in base alla versione e al metodo di installazione del sistema operativo. Il file specificato può includere qualsiasi opzione di configurazione standard supportata dai file di risposte di Windows. È ad esempio possibile usarla per specificare la home page predefinita di Internet Explorer. Specificare il pacchetto che contiene il file di risposte e il percorso associato al file nel pacchetto.  

> [!NOTE]  
>  Il file di risposte del programma di installazione di Windows specificato può includere variabili incorporate della sequenza di attività con formato %*varname*%, dove *varname* indica il nome della variabile. Il passaggio **Imposta Windows e ConfigMgr** sostituisce la stringa %*varname*% con i valori effettivi delle variabili. Queste variabili incorporate della sequenza di attività non possono essere usate in campi di tipo solo numerico in un file di risposte unattend.xml.  

 Se non si specifica un file di risposte del programma di installazione di Windows, questo passaggio della sequenza di attività genera automaticamente un file di risposte.  

 **Destinazione**  
 Configurare una delle opzioni seguenti:  

-   **Next available partition** (Partizione disponibile successiva): usare la partizione sequenziale successiva non ancora sottoposta a un'azione **Applica sistema operativo** o **Applica immagine dei dati** in questa sequenza di attività. 

-   **Disco e partizione specifici**: selezionare un numero per **Disco** (a partire da 0) e per **Partizione** (a partire da 1).  

-   **Lettera unità logica specifica**: specificare la **Lettera unità** assegnata alla partizione da Windows PE. Questa lettera di unità può essere diversa da quella assegnata dal sistema operativo appena distribuito.  

-   **Lettera unità logica archiviata in una variabile**: specificare la variabile della sequenza di attività contenente la lettera di unità assegnata alla partizione da Windows PE. Questa variabile viene in genere impostata nella sezione Avanzate della finestra di dialogo **Proprietà della partizione** per l'azione **Formato e disco partizione** della sequenza di attività.  

### <a name="options"></a>Opzioni  
 Oltre alle opzioni predefinite, nella scheda **Opzioni** di questo passaggio della sequenza di attività configurare le impostazioni aggiuntive seguenti:  

-   **Accedi al contenuto direttamente dal punto di distribuzione**  
     Configurare la sequenza di attività in modo che acceda all'immagine del sistema operativo direttamente dal punto di distribuzione. Usare questa opzione ad esempio quando si distribuiscono sistemi operativi in dispositivi incorporati con capacità di archiviazione limitata. Quando si seleziona questa opzione è necessario configurare anche le impostazioni di condivisione pacchetto nella scheda **Accesso dati** delle proprietà del pacchetto.  

    > [!NOTE]  
    >  Questa impostazione sostituisce l'opzione di distribuzione configurata nella pagina **Punti di distribuzione** di **Distribuzione guidata del software**. La sostituzione è valida solo per l'immagine del sistema operativo specificata in questo passaggio e non per l'intero contenuto della sequenza di attività.  



##  <a name="BKMK_ApplyWindowsSettings"></a> Applica impostazioni Windows  
 Usare questa attività per configurare le impostazioni di Windows per il computer di destinazione. La sequenza di attività archivia questi valori nel file di risposte appropriato. Installazione di Windows usa questo file di risposte durante l'azione **Imposta Windows e ConfigMgr**.  

 Questo passaggio della sequenza di attività può essere eseguito solo in Windows PE. Non può essere eseguito in un sistema operativo standard. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Apply Windows Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ApplyWindowsSettings).  

 Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Impostazioni** e selezionare **Applica impostazioni Windows** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Nome utente**  
 Specificare il nome dell'utente registrato associato al computer di destinazione. Questo valore può essere sostituito dal valore acquisito dal passaggio **Acquisisci impostazioni Windows** della sequenza di attività.  

 **Nome organizzazione**  
 Specificare il nome dell'organizzazione registrata associata al computer di destinazione. Questo valore può essere sostituito dal valore acquisito dal passaggio **Acquisisci impostazioni Windows** della sequenza di attività.  

 **Codice Product Key**  
 Specificare il codice Product Key usato per l'installazione di Windows nel computer di destinazione.  

 **Licenze server**  
 Specificare la modalità di gestione delle licenza del server, ovvero **Per server** o **Per Utente** . Se si sceglie **Per server** specificare anche il numero massimo di connessioni consentite in base al contratto di licenza. Selezionare **Non specificare** se il computer di destinazione non è un server o se non si vuole specificare la modalità di gestione delle licenze.  

 **Numero massimo di connessioni**  
 Specificare il numero massimo di connessioni disponibili per questo computer, in base a quanto indicato nel contratto di licenza.  

 **Genera in modo casuale la password dell'amministratore locale e disattiva l'account su tutte le piattaforme supportate (consigliato)**  
 Selezionare questa opzione per impostare come password per l'amministratore locale una stringa generata in modo casuale. Questa opzione disabilita anche l'account amministratore locale sulle piattaforme che supportano questa funzionalità.  

 **Attiva l'account e specifica la password dell'amministratore locale**  
 Selezionare questa opzione per abilitare l'account dell'amministratore locale mediante la password specificata. Immettere la password nella riga **Password** e confermare la password nella riga **Conferma password** .  

 **Fuso orario**  
 Specificare il fuso orario da configurare nel computer di destinazione. Questo valore può essere sostituito dal valore acquisito dal passaggio **Acquisisci impostazioni Windows** della sequenza di attività.  



##  <a name="BKMK_AutoApplyDrivers"></a> Applica automaticamente i driver  
 Usare questo passaggio per associare e installare i driver come parte della distribuzione del sistema operativo.  

 Il passaggio **Applica automaticamente i driver** della sequenza di attività esegue le azioni seguenti:  

1.  Analizzare l'hardware e trovare gli ID plug-and-play per tutti i dispositivi presenti nel sistema.  

2.  Inviare l'elenco dei dispositivi e dei rispettivi ID plug-and-play al punto di gestione. Il punto di gestione restituisce un elenco di driver compatibili dal catalogo di driver per ogni dispositivo hardware. L'elenco include tutti i driver indipendentemente dal pacchetto di driver in cui si trovano, i driver contrassegnati con la categoria di driver specificata e i driver non disabilitati.  

3.  La sequenza di attività sceglie il driver ottimale per ogni dispositivo hardware. Questo driver è appropriato per il sistema operativo distribuito e si trova in un punto di distribuzione accessibile.  

4.  La sequenza di attività scarica i driver selezionati da un punto di distribuzione e li prepara nel sistema operativo di destinazione.  

    1.  Per le installazioni basate sull'immagine la sequenza di attività posiziona i driver nell'archivio driver del sistema operativo.  

    2.  Per le installazioni basate sul programma di installazione la sequenza di attività configura Installazione di Windows con il percorso dei driver.  

5.  Durante il passaggio **Imposta Windows e ConfigMgr** della sequenza di attività l'installazione di Windows individua i driver preparati da questa azione.  

> [!IMPORTANT]
>  I supporti autonomi non possono usare il passaggio **Applica automaticamente i driver**. L'installazione di Windows non dispone di connessioni al sito di Configuration Manager in questo scenario.

Questo passaggio della sequenza di attività può essere eseguito solo in Windows PE. Non può essere eseguito in un sistema operativo standard. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Auto Apply Drivers Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_AutoApplyDrivers).  

 Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Driver** e selezionare **Applica automaticamente i driver** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Installa solo i driver compatibili con la corrispondenza migliore**  
 Indica che il passaggio della sequenza di attività installa solo i driver con la corrispondenza migliore per ogni dispositivo hardware rilevato.  

 **Installa tutti i driver compatibili**  
 La sequenza di attività installa tutti i driver compatibili per ogni dispositivo hardware rilevato. Quindi l'installazione di Windows sceglie il driver ottimale. Questa opzione richiede più larghezza di banda di rete e una maggior quantità di spazio su disco. La sequenza di attività scarica un numero maggiore di driver, ma Windows è in grado di selezionare un driver migliore.  

 **Considera i driver di tutte le categorie**  
 La sequenza di attività cerca i driver di dispositivo appropriati in tutte le categorie di driver disponibili.  

 **Limita la corrispondenza dei driver in modo da considerare solo i driver delle categorie selezionate**  
 La sequenza di attività cerca i driver di dispositivo appropriati nelle categorie di driver specificate.  

 **Esegui l'installazione automatica dei driver senza firma sulle versioni di Windows in cui è consentito**  
 Questa opzione consente a Windows di installare driver senza firma digitale.   

  > [!IMPORTANT]  
  >  Questa opzione non è applicabile ai sistemi operativi in cui non è possibile configurare i criteri di firma dei driver.  



##  <a name="BKMK_CaptureNetworkSettings"></a> Acquisisci impostazioni di rete  
 Usare questo passaggio per acquisire le impostazioni di rete Microsoft dal computer che esegue la sequenza di attività. La sequenza di attività salva queste impostazioni nelle variabili della sequenza di attività. Queste impostazioni sostituiscono le impostazioni predefinite configurate nel passaggio **Applica impostazioni di rete**.  

 Questo passaggio della sequenza di attività può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Capture Network Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureNetworkSettings).  

Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Impostazioni** e selezionare **Acquisisci impostazioni di rete** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Esegui la migrazione del dominio e dell'appartenenza a gruppi di lavoro**  
 Acquisisce le informazioni sull'appartenenza a domini e gruppi di lavoro del computer di destinazione.  

 **Esegui la migrazione della configurazione della scheda di rete**  
 Acquisisce la configurazione della scheda di rete del computer di destinazione. Le informazioni acquisite includono le impostazioni di rete globali, il numero di schede e le impostazioni di rete associate a ogni scheda. Queste impostazioni includono le impostazioni associate a DNS, WINS, IP e ai filtri delle porte.  



##  <a name="BKMK_CaptureOperatingSystemImage"></a> Acquisisci immagine del sistema operativo  
 Questo passaggio consente di acquisire una o più immagini da un computer di riferimento. La sequenza di attività crea un file immagine di Windows con estensione wim nella condivisione di rete specificata. Usare quindi la procedura guidata **Add Operating System Image Package** (Aggiungi pacchetto immagine del sistema operativo) per importare l'immagine in Configuration Manager per le distribuzioni del sistema operativo basate su immagine.  

 Configuration Manager acquisisce ogni volume (unità) nel computer di riferimento come immagine distinta nel file con estensione wim. Se il computer a cui si fa riferimento include più volumi, il file con estensione wim risultante contiene un'immagine distinta per ogni volume. Vengono acquisiti solo i volumi con formattazione NTFS o FAT32. I volumi con formati diversi e i volumi USB verranno ignorati.  

 Il sistema operativo installato nel computer di riferimento deve essere una versione di Windows supportata da Configuration Manager. Usare lo strumento SysPrep per preparare il sistema operativo del computer di riferimento. Il volume del sistema operativo installato deve essere uguale al volume di avvio.  

 Specificare un account con autorizzazioni di scrittura per la condivisione di rete selezionata.  

 Questo passaggio della sequenza di attività può essere eseguito solo in Windows PE. Non può essere eseguito in un sistema operativo standard. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Capture Operating System Image Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureOperatingSystemImage).  

 Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Immagini** e selezionare **Acquisisci immagine del sistema operativo** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

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



##  <a name="BKMK_CaptureUserState"></a> Acquisisci stato utente  
 Eseguire questo passaggio per usare l'Utilità di migrazione stato utente (USMT, User State Migration Tool) per acquisire lo stato utente e le impostazioni dal computer che esegue la sequenza di attività. Questo passaggio della sequenza di attività viene usato insieme al passaggio **Ripristina stato utente** . In USMT 3.0.1 e versioni successive questa opzione crittografa sempre l'archiviazione stati USMT usando una chiave di crittografia generata e gestita da Configuration Manager.  

 Per altre informazioni sulla gestione dello stato utente durante la distribuzione di sistemi operativi, vedere [Manage user state](../get-started/manage-user-state.md) (Gestire lo stato utente).  

 Per salvare e ripristinare le impostazioni dello stato utente da un punto di migrazione stato, usare il passaggio **Acquisisci stato utente** con i passaggi **Richiedi archiviazione stati** e **Rilascia archiviazione stati**.  

 Il passaggio **Acquisisci stato utente** della sequenza di attività fornisce il controllo su un sottoinsieme limitato delle opzioni USMT più usate. È possibile specificare opzioni aggiuntive da riga di comando usando la variabile OSDMigrateAdditionalCaptureOptions della sequenza di attività.  

 Questo passaggio della sequenza di attività può essere eseguito solo in Windows PE. Non può essere eseguito in un sistema operativo standard. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Capture User State Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureUserState).  

 Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Stato utente** e quindi selezionare **Acquisisci stato utente** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Pacchetto degli strumenti di migrazione dello stato utente**  
 Specificare il pacchetto che contiene l'Utilità di migrazione stato utente (USMT) per ripristinare i dati sullo stato dell'utente. La sequenza di attività usa questa versione di USMT per acquisire lo stato e le impostazioni dell'utente. Questo pacchetto non richiede alcun programma. Specificare un pacchetto contenente la versione di USMT a 32 bit o a 64 bit. L'architettura di USMT dipende dall'architettura del sistema operativo da cui la sequenza di attività esegue l'acquisizione dello stato.  

 **Acquisisci tutti i profili utente utilizzando le opzioni standard**  
 Eseguire la migrazione di tutte le informazioni del profilo utente. Questa è l'opzione predefinita.  

 Se si seleziona questa opzione ma non si seleziona **Ripristina profili utente del computer locale** nel passaggio **Ripristina stato utente**, la sequenza di attività ha esito negativo. Configuration Manager non può eseguire la migrazione di nuovi account senza assegnare password a tali account. 

 Quando si usa l'opzione **Installa un pacchetto immagine esistente** della procedura guidata **New Task Sequence** (Nuova sequenza di attività), la sequenza di attività predefinita risultante è **Capture all user profiles with standard options** (Acquisisci tutti i profili utente con le opzioni standard). Questa sequenza di attività predefinita non seleziona l'opzione **Ripristina profili utente del computer locale**, ovvero gli account utente non del dominio.  

 Selezionare **Ripristina profili utente del computer locale** e fornire una password per l'account di cui deve essere eseguita la migrazione. In una sequenza di attività creata manualmente questa impostazione è disponibile nel passaggio Ripristina stato utente. In una sequenza di attività creata dalla procedura guidata **Crea nuova sequenza di attività** questa impostazione è disponibile nella pagina della procedura guidata **Ripristina file utente e impostazioni** .  

 Se non sono presenti account utente locali, questa impostazione non è applicabile.  

 **Personalizza modalità di acquisizione dei profili utente**  
 Selezionare questa opzione per specificare una migrazione del file di profilo personalizzato. Fare clic su **File** per selezionare i file di configurazione che USMT dovrà usare con questo passaggio. Specificare un file con estensione xml personalizzato contenente le regole che definiscono i file di stato utente di cui eseguire la migrazione.  

 **Fare clic qui per selezionare i file di configurazione:**  
 Selezionare questa opzione per selezionare i file di configurazione nel pacchetto USMT da usare per l'acquisizione dei profili utente. Fare clic su **File** per aprire la finestra di dialogo **File di configurazione** . Per specificare un file di configurazione, immettere il nome del file nella riga **Nome file** e quindi fare clic su **Aggiungi** .  

 **Abilita la registrazione dettagliata**  
 Abilitare questa opzione per generare informazioni di file di log più dettagliate. Durante l'acquisizione dello stato, per impostazione predefinita la sequenza di attività genera il file ScanState.log nella cartella dei log della sequenza di attività, \windows\system32\ccm\logs.   

 **Ignora file che utilizzano Encrypting File System (EFS)**  
 Abilitare questa opzione per ignorare l'acquisizione di file crittografati con EFS (Encrypting File System). Questi file includono i file profilo utente. In base al sistema operativo e alla versione di USMT, è possibile che i file crittografati non siano leggibili dopo il ripristino. Per altre informazioni, vedere la documentazione relativa a USMT.  

 **Copia utilizzando l'accesso al file system**  
 Abilitare questa opzione per specificare una delle impostazioni seguenti:  

-   **Continua se non è possibile acquisire alcuni file**: questa impostazione consente al passaggio della sequenza di attività di continuare il processo di migrazione, anche se non è possibile acquisire alcuni file. Se si disabilita questa opzione, quando non è possibile acquisire un file il passaggio ha esito negativo. Questa opzione è attivata per impostazione predefinita.  

-   **Esegui acquisizione localmente utilizzando i collegamenti invece di copiare i file**: abilitare questa impostazione per usare i collegamenti reali NTFS per acquisire i file.  

     Per altre informazioni sulla migrazione di dati tramite i collegamenti reali, vedere [Archivio delle migrazioni con collegamento reale](http://go.microsoft.com/fwlink/p/?LinkId=240222)  

-   **Acquisisci in modalità non in linea (solo Windows PE)**: abilitare questa impostazione per acquisire lo stato utente in Windows PE invece che nel sistema operativo completo.  
    
**Acquisisci utilizzando Servizio Copia Shadow del volume (VSS)**  
 Questa opzione consente di acquisire file anche se sono bloccati per la modifica da un'altra applicazione.  



##  <a name="BKMK_CaptureWindowsSettings"></a> Acquisisci impostazioni Windows  
 Usare questo passaggio per acquisire le impostazioni di Windows dal computer che esegue la sequenza di attività. La sequenza di attività salva queste impostazioni nelle variabili della sequenza di attività. Queste impostazioni acquisite sostituiscono le impostazioni predefinite configurate nel passaggio **Applica impostazioni Windows**.  

 Questo passaggio della sequenza di attività può essere eseguito in Windows PE o in un sistema operativo standard. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Capture Windows Settings Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_CaptureWindowsSettings).  

 Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Impostazioni** e selezionare **Acquisisci impostazioni Windows** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Esegui la migrazione del nome computer**  
 Acquisire il nome NetBIOS del computer.  

 **Esegui la migrazione dell'utente registrato e dei nomi organizzazione**  
 Acquisire l'utente registrato e i nomi dell'organizzazione dal computer.  

 **Esegui la migrazione del fuso orario**  
 Acquisire l'impostazione relativa al fuso orario nel computer.  



##  <a name="BKMK_CheckReadiness"></a> Verifica conformità  
 Usare questo passaggio per verificare se il computer di destinazione soddisfa le condizioni dei prerequisiti di distribuzione specificate.  

Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Generale** e selezionare **Verifica conformità** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Verifica la quantità di memoria minima (MB)**  
 Verificare che la quantità di memoria in megabyte (MB) sia uguale o superiore alla quantità specificata. Il passaggio abilita questa opzione per impostazione predefinita.  

 **Verifica la velocità minima del processore (MHz)**  
 Verificare che la velocità del processore in megahertz (MHz) sia uguale o superiore al valore specificato. Il passaggio abilita questa opzione per impostazione predefinita.  

 **Verifica lo spazio minimo disponibile su disco (MB)**  
 Verificare che la quantità di spazio su disco disponibile in megabyte (MB) sia uguale o superiore al valore specificato.  

 **Verifica che il sistema operativo corrente da aggiornare sia**  
 Verificare che il sistema operativo installato nel computer client soddisfi i requisiti specificati. Il passaggio imposta questo valore su **CLIENT** per impostazione predefinita.  

### <a name="options"></a>Opzioni
 > [!NOTE]  
 > Se si abilita l'impostazione **Continua in caso di errore** della scheda **Opzioni**, il passaggio si limita a registrare i risultati del controllo di conformità. Se un controllo ha esito negativo, la sequenza di attività non viene arrestata.



##  <a name="BKMK_ConnectToNetworkFolder"></a> Connetti alla cartella di rete  
 Usare questo passaggio per creare una connessione a una cartella di rete condivisa.  

 Questo passaggio della sequenza di attività viene eseguito in un sistema operativo standard o in Windows PE. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Connect to Network Folder Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_ConnecttoNetworkFolder).  

 Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Generale** e selezionare **Connetti alla cartella di rete** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Percorso**  
 Fare clic su **Sfoglia** per specificare il percorso della cartella di rete. Usare il formato  *\\\server\condivisione*.

 **Unità**  
 Selezionare la lettera dell'unità locale da assegnare per questa connessione. 

 **Account**  
 Fare clic su **Imposta** per specificare l'account utente con autorizzazioni per la connessione a questa cartella di rete.



##  <a name="BKMK_DisableBitLocker"></a> Disattiva BitLocker  
 Usare questo passaggio per disattivare la crittografia BitLocker nell'unità del sistema operativo corrente o in un'unità specifica. Questa azione lascia che le protezioni con chiave siano visibili in testo non crittografato nel disco rigido, ma non decrittografa i contenuti dell'unità. Questa azione viene quindi completata quasi istantaneamente.  

> [!NOTE]  
>  La crittografia unità BitLocker offre una crittografia di basso livello dei contenuti di un volume del disco.  

 Se sono disponibili più unità crittografate, sarà necessario disabilitare BitLocker in qualsiasi unità di dati prima di disabilitare BitLocker nell'unità del sistema operativo.  

 Questo passaggio può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE.  

 Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Dischi** e selezionare **Disattiva BitLocker** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Unità del sistema operativo corrente**  
 Disabilita BitLocker nell'unità attuale del sistema operativo.  

 **Unità specifica**  
 Disabilita BitLocker in un'unità specifica. Usare l'elenco a discesa per specificare l'unità in cui BitLocker è disabilitato.  



##  <a name="BKMK_DownloadPackageContent"></a> Scarica contenuto pacchetto  
 Usare questo passaggio per scaricare uno dei tipi di pacchetto seguenti:  

-   Immagini del sistema operativo  

-   Pacchetti di aggiornamento del sistema operativo  

-   Pacchetti driver  

-   Pacchetti  
    
Questo passaggio funziona bene in una sequenza di attività per eseguire l'aggiornamento di un sistema operativo negli scenari seguenti:  

-   Usare una singola sequenza di attività di aggiornamento che può funzionare con piattaforme x86 e x64. Includere due passaggi **Scarica contenuto pacchetto** nel gruppo **Preparazione dell'aggiornamento**. Specificare nella scheda **Opzioni** le condizioni necessarie per rilevare l'architettura client e scaricare solo il pacchetto di aggiornamento del sistema operativo appropriato. Configurare ogni passaggio **Scarica contenuto pacchetto** in modo che usi la stessa variabile. Usare la variabile per il percorso del supporto nel passaggio **Aggiorna sistema operativo**.  

-   Per scaricare in modo dinamico un pacchetto di driver applicabile, usare due passaggi **Scarica contenuto pacchetto** con le condizioni per rilevare il tipo di hardware appropriato per ogni pacchetto driver. Configurare ogni passaggio **Scarica contenuto pacchetto** in modo che usi la stessa variabile. Usare la variabile per il valore **Contenuto preconfigurato** nella sezione Driver del passaggio **Aggiorna sistema operativo**.  

> [!NOTE]    
> Quando si distribuisce una sequenza di attività che contiene il passaggio Scarica contenuto pacchetto, non selezionare **Scaricare tutto il contenuto localmente prima di avviare la sequenza di attività** o **Access content directly from a distribution point** (Accedere al contenuto direttamente da un punto di distribuzione) per **Opzioni di distribuzione** nella pagina **Punti di distribuzione** della Distribuzione guidata del software.  

Questo passaggio viene eseguito in un sistema operativo standard o in Windows PE. Tuttavia, l'opzione relativa al salvataggio del pacchetto nella cache del client di Configuration Manager non è supportata in WinPE.

 Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Software** e selezionare **Scarica contenuto pacchetto** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 Icona**Selezione pacchetto**  
 Fare clic sull'icona per selezionare il pacchetto da scaricare. Dopo aver selezionato un pacchetto, è possibile fare clic sull'icona di nuovo per scegliere un altro pacchetto.  

 **Inserire nel seguente percorso**  
 Scegliere di salvare il pacchetto in uno dei seguenti percorsi:  

 -   **Directory di lavoro della sequenza di attività**  

 -   **Cache del client di Configuration Manager**: usare questa opzione per archiviare il contenuto nella cache del client. Il client fa da origine di peer cache per gli altri client peer cache. Per altre informazioni, vedere [Prepare Windows PE peer cache to reduce WAN traffic](../get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md) (Preparare la peer cache di Windows PE per ridurre il traffico della rete WAN)  

 -    **Percorso personalizzato**: il motore di esecuzione della sequenza di attività scarica il pacchetto nella directory di lavoro della sequenza di attività e quindi lo sposta nel percorso specificato con questa opzione. Il motore di esecuzione della sequenza di attività aggiunge il percorso con l'ID pacchetto. 
   
**Salvare il percorso come variabile**  
 È possibile salvare il percorso come variabile utilizzabile in un altro passaggio della sequenza di attività. Configuration Manager aggiunge un suffisso numerico al nome della variabile. Se ad esempio si specifica la variabile %*mycontent*% come variabile personalizzata, questa variabile diventa la radice in cui viene archiviato tutto il contenuto di riferimento. Il contenuto può essere costituito da più pacchetti. Quando si fa riferimento alla variabile, aggiungere un suffisso numerico. Per il primo pacchetto, ad esempio, fare riferimento alla variabile %*mycontent01*%. Quando si fa riferimento alla variabile in passaggi successivi, ad esempio in **Aggiorna sistema operativo**, viene usato %*mycontent02*% o %*mycontent03*%, dove il numero corrisponde all'ordine di elenco dei pacchetti nel passaggio **Scarica contenuto pacchetto**.  

**Se il download di un pacchetto non riesce, continuare a scaricare gli altri pacchetti nell'elenco**  
 Se la sequenza di attività non riesce a scaricare un pacchetto, inizia a scaricare il pacchetto successivo nell'elenco.  



##  <a name="BKMK_EnableBitLocker"></a> Attiva BitLocker  
Usare questo passaggio per attivare la crittografia BitLocker in almeno due partizioni nel disco rigido. La prima partizione attiva include il codice bootstrap di Windows. Un'altra partizione contiene il sistema operativo. La partizione bootstrap deve rimanere non crittografata.  

Usare il passaggio **BitLocker pre-provisioning** della sequenza di attività per abilitare BitLocker in un'unità in Windows PE. Per altre informazioni, vedere la sezione [Pre-provisioning di BitLocker](#BKMK_PreProvisionBitLocker).  

> [!NOTE]  
>  La crittografia unità BitLocker offre una crittografia di basso livello dei contenuti di un volume del disco.  

Il passaggio **Attiva BitLocker** può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Enable BitLocker Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

Quando si specifica **Solo TPM**, **TPM e chiave di avvio su USB** o **TPM e PIN**, lo stato di TPM (Trusted Platform Module) deve essere il seguente perché sia possibile eseguire il passaggio **Attiva BitLocker**:  

-   Abilitato  
-   Attivato  
-   Proprietà consentita  
   
Questo passaggio completa le eventuali operazioni rimanenti di inizializzazione TPM. I passaggi rimanenti non richiedono la presenza fisica né operazioni di riavvio. Se necessario, il passaggio**Attiva BitLocker** completa in modo trasparente i passaggi rimanenti dell'inizializzazione TPM:  

-   Creazione della coppia di chiavi di verifica autenticità.  
-   Creazione di un valore di autorizzazione del proprietario e del deposito in Active Directory, che deve essere stato esteso per supportare questo valore.  
-   Acquisizione della proprietà.  
-   Creazione della chiave radice di archiviazione o reimpostazione nel caso in cui la chiave sia già presente ma non sia compatibile.  
   
Se si vuole che la sequenza di attività attenda il completamento del processo di crittografia unità nel passaggio **Attiva BitLocker**, selezionare l'opzione **Attendi**. Se non si seleziona l'opzione **Attendi** il processo di crittografia unità avviene in background. La sequenza di attività procede immediatamente al passaggio successivo.  

È possibile usare BitLocker per crittografare più unità in un sistema di computer, sia nelle unità del sistema operativo che nelle unità dati. Per crittografare un'unità dati, crittografare in primo luogo l'unità del sistema operativo e completare il processo di crittografia. Questo requisito dipende dal fatto che l'unità del sistema operativo archivia le protezioni con chiave per le unità dati. Se l'unità del sistema operativo e l'unità dati vengono crittografate nella stessa sequenza di attività, selezionare l'opzione **Attendi** nel passaggio **Attiva BitLocker** per l'unità del sistema operativo.  

Se il disco rigido è già crittografato ma BitLocker è disabilitato, il passaggio **Attiva BitLocker** abilita di nuovo le protezioni con chiave e viene completato rapidamente. In questo caso non è necessario ripetere la crittografia del disco rigido.  

Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Enable BitLocker Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Dischi** e selezionare **Attiva BitLocker** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Scegli l'unità da crittografare**  
 Specifica l'unità da crittografare Per crittografare l'unità attuale del sistema operativo, selezionare **Unità del sistema operativo corrente** , quindi configurare una delle opzioni seguenti per la gestione delle chiavi:  

-   **Solo TPM**: selezionare questa opzione per usare solo TPM (Trusted Platform Module).  

-   **Chiave di avvio solo su USB**: selezionare questa opzione per usare una chiave di avvio archiviata in un'unità flash USB. Quando si seleziona questa opzione, BitLocker blocca il normale processo di avvio fino al collegamento di un dispositivo USB contenente una chiave di avvio BitLocker al computer.  

-   **TPM e chiave di avvio su USB**: selezionare questa opzione per usare TPM e una chiave di avvio archiviata in un'unità flash USB. Quando si seleziona questa opzione, BitLocker blocca il normale processo di avvio fino al collegamento di un dispositivo USB contenente una chiave di avvio BitLocker al computer.  

-   **TPM e PIN**: selezionare questa opzione per usare TPM e un codice PIN. Quando si seleziona questa opzione, BitLocker blocca il normale processo di avvio fino a quando l'utente fornisce il codice PIN.  
   
Per crittografare un'unità dati specifica, non del sistema operativo, selezionare **Unità specifica**, quindi selezionare l'unità dall'elenco.  

**Scegli dove creare la chiave di ripristino**  
 Per specificare la posizione in cui BitLocker crea la password di ripristino e depositarla in Active Directory, selezionare **In Active Directory**. Se si seleziona questa opzione, è necessario estendere Active Directory per il sito. In questo modo BitLocker può salvare le informazioni di ripristino associate in Active Directory. Selezionare **Non creare una chiave di ripristino** per non creare una password. La creazione di una password è una procedura consigliata.  

**Attendi il completamento del processo di crittografia di tutte le unità di BitLocker prima di continuare l'esecuzione della sequenza di attività con Configuration Manager**  
 Selezionare questa opzione per consentire il completamento della crittografia unità BitLocker prima dell'esecuzione del passaggio successivo nella sequenza di attività. Se si seleziona questa opzione, BitLocker esegue la crittografia dell'intero volume del disco prima che l'utente possa accedere al computer.  

In caso di dischi rigidi di grandi dimensioni il processo di crittografia può richiedere diverse ore. Se non si seleziona questa opzione, la sequenza di attività può proseguire immediatamente.  



##  <a name="BKMK_FormatandPartitionDisk"></a> Formato e disco partizione  
 Usare questo passaggio per formattare e partizionare un disco specificato nel computer di destinazione.  

> [!IMPORTANT]  
>  Ogni impostazione specificata per questo passaggio della sequenza di attività è applicabile a un singolo disco specificato. Per formattare e partizionare un altro disco nel computer di destinazione, aggiungere un altro passaggio **Formato e disco partizione** alla sequenza di attività.  

 Questo passaggio della sequenza di attività può essere eseguito solo in Windows PE. Non può essere eseguito in un sistema operativo standard. Per altre informazioni sulle variabili della sequenza di attività per questa azione, vedere [Format and Partition Disk Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_FormatPartitionDisk).  

 Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Dischi** e selezionare **Formato e disco partizione** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Numero disco**  
 Numero del disco fisico da formattare. Il numero è basato sull'ordinamento di enumerazione dei dischi Windows.  

 **Tipo di disco**  
 Tipo del disco formattato. Nell'elenco a discesa è possibile selezionare le due opzioni seguenti: 

-   Standard (MBR) - Record di avvio principale
-   GPT - Tabella di partizione GUID  

> [!NOTE]  
>  Se si cambia il tipo di disco da **Standard (MBR)** a **GPT** e il layout della partizione include una partizione estesa, la sequenza di attività rimuove dal layout tutte le partizioni estese e logiche. L'editor della sequenza di attività richiede conferma prima di modificare il tipo di disco.  
   
**Volume**  
 Informazioni specifiche sulla partizione o sul volume creato dalla sequenza di attività, inclusi gli attributi seguenti:  

-   Name  
-   Spazio su disco rimanente  
   
Per creare una nuova partizione, fare clic su **Nuovo** per aprire la finestra di dialogo **Proprietà della partizione** . Specificare il tipo e la dimensione della partizione e se si tratta di una partizione di avvio. Per modificare una partizione esistente, fare clic sulla partizione da modificare, quindi su Proprietà. Per altre informazioni su come configurare le partizioni del disco rigido, vedere uno degli articoli seguenti:  

-   [Configurare partizioni in un disco rigido basato su UEFI/GPT](http://go.microsoft.com/fwlink/?LinkID=272104)  
-   [Configurare partizioni in un disco rigido basato su BIOS/MBR](http://go.microsoft.com/fwlink/?LinkId=272105)  

Per eliminare una partizione, selezionare la partizione da eliminare, quindi fare clic su **Elimina**.  



##  <a name="BKMK_InstallApplication"></a> Installa applicazione  
Questo passaggio consente di installare le applicazioni specificate o un set di applicazioni definito da un elenco dinamico di variabili della sequenza di attività. Quando si esegue questo passaggio, l'installazione dell'applicazione inizia immediatamente, senza attendere il termine dell'intervallo di polling dei criteri.  

Le applicazioni installate devono soddisfare i criteri seguenti:  

-   L'applicazione deve essere un tipo di distribuzione Windows Installer o Programma di installazione dello script. Non sono supportati i tipi di distribuzione Pacchetto app Windows (file .appx).  

-   Deve essere in esecuzione con l'account di sistema locale e non con l'account utente.  

-   Non deve interagire con il desktop. Il programma deve essere eseguito automaticamente o in modalità automatica.  

-   Non deve dare inizio autonomamente a un riavvio. L'applicazione deve richiedere un riavvio usando il codice di riavvio standard, ovvero un codice di uscita 3010. Questo comportamento garantisce che il passaggio della sequenza di attività gestisca correttamente il riavvio. Se l'applicazione restituisce un codice di uscita 3010, il motore della sequenza di attività sottostante eseguirà il riavvio. Dopo il riavvio, la sequenza di attività continua automaticamente.  

Quando si esegue il passaggio **Installa applicazione** l'applicazione verifica l'applicabilità delle regole dei requisiti e del metodo di rilevamento nei tipi di distribuzione dell'applicazione stessa. In base ai risultati di questa verifica, l'applicazione installa il tipo di distribuzione applicabile. Se il tipo di distribuzione contiene dipendenze, il tipo di distribuzione dipendente verrà valutato e installato come parte del passaggio Installa applicazione. Le dipendenze delle applicazioni non vengono supportati per i supporti autonomi.  

> [!NOTE]  
>  Per installare un'applicazione che sostituisce un'altra applicazione è necessario che i file di contenuto per l'applicazione sostituita siano disponibili. In caso contrario questo passaggio della sequenza di attività ha esito negativo. Ad esempio, Microsoft Visio 2010 viene installato in un client o in un'immagine acquisita. Quando il passaggio **Installa applicazione** installa Microsoft Visio 2013, i file di contenuto per Microsoft Visio 2010 (l'applicazione sostituita) devono essere disponibili in un punto di distribuzione. Se Microsoft Visio non è installato in un client o in un'immagine acquisita, la sequenza di attività installa Microsoft Visio 2013 senza verificare i file di contenuto di Microsoft Visio 2010.  

> [!NOTE]
> Se il client non riesce a recuperare l'elenco dei punti di gestione dai servizi di posizione, usare le variabili predefinite SMSTSMPListRequestTimeoutEnabled e SMSTSMPListRequestTimeout per specificare quanti millisecondi deve attendere una sequenza di attività prima di provare nuovamente a installare un'applicazione o un aggiornamento software. Per altre informazioni, vedere [Variabili predefinite della sequenza di attività](task-sequence-built-in-variables.md).

 Questo passaggio della sequenza di attività può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE.  

 Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Software** e selezionare **Installa applicazione** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio configurare le impostazioni illustrate in questa sezione.  

 **Installa le seguenti applicazioni**  
 La sequenza di attività installa queste applicazioni nell'ordine specificato.  

 Configuration Manager esclude tramite filtro le applicazioni disabilitate o le applicazioni con le impostazioni seguenti:  

-   Solo se un utente è connesso  
-   Esegui con diritti dell'utente  

Queste applicazioni non vengono visualizzate nella finestra di dialogo **Seleziona l'applicazione da installare**.
  
**Installa le applicazioni in base all'elenco di variabili dinamiche**  
La sequenza di attività installa le applicazioni usando questo nome variabile di base. Il nome variabile di base indica un set di variabili della sequenza di attività definite per una raccolta o un computer. Queste variabili specificano le applicazioni che vengono installate dalla sequenza di attività per tale raccolta o computer. Ogni nome di variabile comprende il nome base comune e un suffisso numerico che inizia con 01. Il valore di ogni variabili deve contenere soltanto il nome dell'applicazione.  

Per consentire alla sequenza di attività di installare applicazioni usando un elenco di variabili dinamiche, abilitare l'impostazione seguente nella scheda **Generale** della finestra di dialogo **Proprietà** dell'applicazione: **Allow this application to be installed from the Install Application task sequence action instead of deploying manually** (Consenti l'installazione dell'applicazione dall'operazione sequenza attività Installazione applicazione anziché distribuirla manualmente).  

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

Le condizioni seguenti influiscono sulle applicazioni installate dalla sequenza di attività:  

-   Se il valore di una variabile include informazioni diverse dal nome dell'applicazione, la sequenza di attività non installa l'applicazione e continua l'esecuzione.  

-   Se la sequenza di attività non trova una variabile con il nome di base specificato e il suffisso "01", non installa nessuna applicazione. 
   
**Se l'installazione di un'applicazione non riesce, continuare installando le altre applicazioni dell'elenco**  
 Questa impostazione specifica che il passaggio continua in caso di errore di installazione di una singola applicazione. Se si specifica questa impostazione, la sequenza di attività continua indipendentemente da eventuali errori di installazione. Se non si specifica questa impostazione e l'installazione non riesce, il passaggio termina immediatamente.  

### <a name="options"></a>Opzioni
 > [!NOTE] 
 > Quando si seleziona **Continua in caso di errore** nella scheda **Opzioni** di questo passaggio, la sequenza di attività continua in caso di errore di installazione di un'applicazione. Quando non si abilita questa opzione, la sequenza di attività ha esito negativo e non installa le applicazioni rimanenti.  
 
Oltre alle opzioni predefinite, nella scheda **Opzioni** di questo passaggio della sequenza di attività configurare le impostazioni aggiuntive seguenti:  

-   **Ripeti passaggio se il computer viene riavviato in modo imprevisto**  
    Se l'installazione di una delle applicazioni riavvia il computer in modo imprevisto, ripetere questo passaggio. Per impostazione predefinita, il passaggio abilita questa impostazione con due tentativi. È possibile specificare da uno a cinque tentativi.  



##  <a name="BKMK_InstallPackage"></a> Installa pacchetto
Usare questo passaggio per installare un pacchetto software come parte della sequenza di attività. Quando si esegue questo passaggio l'installazione inizia immediatamente, senza attendere un intervallo di polling dei criteri.  

Il pacchetto deve soddisfare i criteri seguenti:  

-   Deve essere eseguito con l'account di sistema locale e non con un account utente.  

-   Non deve interagire con il desktop. Il programma deve essere eseguito automaticamente o in modalità automatica.  

-   Non deve dare inizio autonomamente a un riavvio. Il software deve richiedere un riavvio usando il codice di riavvio standard, ovvero un codice di uscita 3010. Questo comportamento garantisce che il passaggio della sequenza di attività gestisca adeguatamente il riavvio. Se il software restituisce un codice di uscita 3010, il motore della sequenza di attività sottostante riavvia il computer. Dopo il riavvio, la sequenza di attività continua automaticamente.  

I programmi che usano l'opzione **Esegui prima un altro programma** per installare un programma dipendente non sono supportati durante la distribuzione di un sistema operativo. Se si abilita l'opzione del pacchetto **Esegui prima un altro programma** e il programma dipendente è già stato eseguito nel computer di destinazione, il programma dipendente viene eseguito e la sequenza di attività continua. Se tuttavia il programma dipendente non è ancora stato eseguito nel computer di destinazione, il passaggio della sequenza di attività ha esito negativo.  

> [!NOTE]  
>  Il sito di amministrazione centrale non dispone dei criteri di configurazione client necessari per abilitare l'agente di distribuzione del software durante la sequenza di attività. Quando si creano supporti autonomi per una sequenza di attività in un sito di amministrazione centrale e la sequenza di attività include il passaggio **Installa pacchetto** , è possibile che nel file CreateTsMedia.log venga visualizzato il seguente errore:  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>   
>  Per i supporti autonomi che includono un passaggio **Installa pacchetto**, creare il supporto autonomo in un sito primario nel quale è abilitato l'agente di distribuzione software. In alternativa aggiungere un passaggio **Esegui riga di comando** dopo il passaggio **Imposta Windows e ConfigMgr** e prima del primo passaggio **Installa pacchetto**. Il passaggio **Esegui riga di comando** esegue un comando WMIC per abilitare l'agente di distribuzione software prima del primo passaggio **Installa pacchetto**. Usare il comando seguente nel passaggio **Esegui riga di comando**:  
>   
>  **Riga di comando**: `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
>   
>  Per altre informazioni sulla creazione di supporti autonomi, vedere [Create stand-alone media](../deploy-use/create-stand-alone-media.md) (Creare supporti autonomi).  

Questo passaggio della sequenza di attività può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE.  

Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Software** e selezionare **Installa pacchetto** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Installa un solo pacchetto software**  
 Questa impostazione specifica un pacchetto software di Configuration Manager. Il passaggio attende fino al completamento dell'installazione.  

 **Installa i pacchetti software in base all'elenco di variabili dinamiche**  
 La sequenza di attività installa i pacchetti usando questo nome variabile di base. Il nome variabile di base indica un set di variabili della sequenza di attività definite per una raccolta o un computer. Queste variabili specificano i pacchetti che vengono installati dalla sequenza di attività per la raccolta o il computer. Ogni nome di variabile comprende il nome base comune e un suffisso numerico che inizia con 001. Il valore di ogni variabile deve includere un ID pacchetto e il nome del software separati da due punti.  

 Per far sì che la sequenza di installazione installi un software tramite un elenco di variabili dinamiche, abilitare l'impostazione seguente nella scheda **Avanzate** in **Proprietà** del pacchetto: **Consenti l'installazione di questo programma dalla sequenza di attività Installa pacchetto senza che venga distribuito**.  

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

 Le condizioni seguenti influiscono sui pacchetti installati dalla sequenza di attività:  

-   Se il valore di una variabile non viene creato con il formato corretto o se non specifica un ID e un nome del pacchetto validi, l'installazione del software ha esito negativo.  

-   Se l'ID del pacchetto include caratteri minuscoli, l'installazione del software ha esito negativo.  

-   Se la sequenza di attività non trova una variabile con il nome di base specificato e il suffisso "001" non installa nessun pacchetto. La sequenza di attività continua.  
   
**Se l'installazione di un pacchetto software non riesce, continuare con l'installazione degli altri pacchetti dell'elenco**  
 Questa impostazione specifica che il passaggio procederà in caso di errore di installazione di un singolo pacchetto software. Se si specifica questa impostazione, la sequenza di attività continua indipendentemente da eventuali errori di installazione. Se non si specifica questa impostazione e l'installazione non riesce, il passaggio termina immediatamente.  



##  <a name="BKMK_InstallSoftwareUpdates"></a> Installa aggiornamenti software  
Usare questo passaggio per installare gli aggiornamenti software nel computer di destinazione. Il computer di destinazione viene valutato alla ricerca di aggiornamenti software applicabili solo in corrispondenza con l'esecuzione di questo passaggio della sequenza di attività, quando il computer di destinazione viene valutato per gli aggiornamenti software come qualsiasi altro client gestito da Configuration Manager. Per far sì che questo passaggio installi gli aggiornamenti software, è prima necessario distribuire gli aggiornamenti a una raccolta di cui è membro il computer di destinazione.  
>  [!IMPORTANT]
> Una procedura consigliata per prestazioni ottimali è l'installazione della versione più recente dell'agente Windows Update. 
>* Per Windows 7, vedere l'[articolo della Knowledge Base 3161647](https://support.microsoft.com/kb/3161647).
>* Per Windows 8, vedere l'[articolo della Knowledge Base 3163023](https://support.microsoft.com/kb/3163023).

 Questo passaggio della sequenza di attività può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE. Per informazioni sulle variabili della sequenza di attività per questa azione della sequenza di attività, vedere [Install Software Updates Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_InstallSoftwareUpdates).

 > [!NOTE]
 > Se il client non riesce a recuperare l'elenco dei punti di gestione dai servizi di posizione, usare le variabili predefinite SMSTSMPListRequestTimeoutEnabled e SMSTSMPListRequestTimeout per specificare quanti millisecondi deve attendere una sequenza di attività prima di provare nuovamente a installare un'applicazione o un aggiornamento software. Per altre informazioni, vedere [Variabili predefinite della sequenza di attività](task-sequence-built-in-variables.md).

 Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Software** e selezionare **Installa aggiornamenti software** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Necessario per l'installazione - Solo aggiornamenti software obbligatori**  
 Selezionare questa opzione per installare tutti gli aggiornamenti software obbligatori, con date di installazione definite dall'amministratore.  

 **Disponibile per l'installazione - Tutti gli aggiornamenti software**  
 Selezionare questa opzione per installare tutti gli aggiornamenti software disponibili. È in primo luogo necessario distribuire tali aggiornamenti a una raccolta di cui il computer è membro. La sequenza di attività installa tutti gli aggiornamenti software disponibili nei computer di destinazione.  

 **Valuta gli aggiornamenti software dai risultati di analisi memorizzati nella cache**  
 Per impostazione predefinita la sequenza di attività usa i risultati di analisi memorizzati nella cache dall'agente Windows Update. Deselezionare la casella di controllo per indicare all'agente Windows Update di scaricare il catalogo più recente dal punto di aggiornamento software. Scegliere questa opzione quando si usa una sequenza di attività per [acquisire e compilare un'immagine del sistema operativo](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md). In questo scenario è probabile che si presenti numero elevato di aggiornamenti software. Molti di questi aggiornamenti hanno dipendenze, ad esempio un requisito che prevede l'installazione di X prima dell'installazione di Y. Se si deseleziona questa impostazione e si distribuisce la sequenza di attività a molti client, tutti i client si connettono contemporaneamente al punto di aggiornamento software. Questo comportamento causa problemi di prestazioni durante il processo e il download del catalogo. La procedura consigliata è l'impostazione predefinita che prevede l'uso dei risultati di analisi memorizzati nella cache. 

La sequenza di attività SMSTSSoftwareUpdateScanTimeout controlla il timeout dell'analisi degli aggiornamenti software durante questo passaggio. Il valore predefinito è 30 minuti. Per altre informazioni, vedere [Variabili predefinite della sequenza di attività](task-sequence-built-in-variables.md).

### <a name="options"></a>Opzioni   
 Oltre alle opzioni predefinite, nella scheda **Opzioni** di questo passaggio della sequenza di attività configurare le impostazioni aggiuntive seguenti:  

-   **Ripeti passaggio se il computer viene riavviato in modo imprevisto**  
    Se uno degli aggiornamenti riavvia il computer in modo imprevisto, ripetere questo passaggio. Per impostazione predefinita, il passaggio abilita questa impostazione con due tentativi. È possibile specificare da uno a cinque tentativi.  

    > [!NOTE]
    > Configurare la variabile SMSTSWaitForSecondReboot per specificare i secondi di sospensione della sequenza di attività dopo il riavvio del computer in questo scenario. Per altre informazioni, vedere [Variabili predefinite della sequenza di attività](task-sequence-built-in-variables.md).



##  <a name="BKMK_JoinDomainorWorkgroup"></a> Aggiunta a dominio o gruppo di lavoro  
 Usare questo passaggio per aggiungere il computer di destinazione a un dominio o un gruppo di lavoro.  

 Questo passaggio della sequenza di attività può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE. Per informazioni sulle variabili della sequenza di attività per questa azione della sequenza di attività, vedere [Join Domain or Workgroup Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_JoinDomainWorkgroup).  

 Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Generale** e selezionare **Aggiunta a dominio o gruppo di lavoro** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Aggiunta a un gruppo di lavoro**  
 Selezionare questa opzione per aggiungere il computer di destinazione al gruppo di lavoro specificato. Se il computer è attualmente membro di un dominio, la selezione di questa opzione determina il riavvio del computer.  

 **Aggiunta a un dominio**  
 Selezionare questa opzione per aggiungere il computer di destinazione al dominio specificato.  

 Facoltativamente, immettere o selezionare un'unità organizzativa nel dominio specificato a cui aggiungere il computer. Se il computer è attualmente membro di un altro dominio o un altro gruppo di lavoro, questa opzione determina il riavvio del computer. Se il computer è già membro di un'altra unità organizzativa, dato che Active Directory Domain Services non consente la modifica dell'unità organizzativa con questo metodo, l'installazione di Windows ignora l'impostazione.  

 **Immettere l'account con le autorizzazioni per l'aggiunta al dominio**  
 Fare clic su **Imposta** per immettere il nome utente e la password di un account con autorizzazioni per l'aggiunta al dominio. Immettere l'account con il formato *Dominio\account*  



## <a name="BKMK_PrepareConfigMgrClientforCapture"></a> Prepara client ConfigMgr per l'acquisizione  
Usare questo passaggio per rimuovere o configurare il client di Configuration Manager nel computer di riferimento. Questa azione prepara il computer per l'acquisizione come parte del processo di creazione immagine.

A partire da Configuration Manager versione 1610 il passaggio **Prepare ConfigMgr Client** (Prepara client ConfigMgr) rimuove completamente il client di Configuration Manager anziché rimuovere solo le informazioni chiave. Quando la sequenza di attività distribuisce l'immagine del sistema operativo acquisita, installa ogni volta un nuovo client di Configuration Manager.  

> [!Note]  
>  Il motore di esecuzione della sequenza di attività rimuove il client solo durante la sequenza di attività **Crea e acquisisci un'immagine del sistema operativo di riferimento**. Il motore di esecuzione della sequenza di attività non rimuove il client durante l'esecuzione di altri metodi di acquisizione, quali Acquisisci supporto o una sequenza di attività personalizzata.

Prima di Configuration Manager versione 1610 questo passaggio eseguiva le attività seguenti:  

-   Rimozione della sezione relativa alle proprietà di configurazione del client dal file smscfg.ini nella directory Windows. Queste proprietà includono informazioni specifiche dei client, quali il GUID di Configuration Manager e altri identificatori del client.  

-   Eliminazione di tutti i certificati della macchina di SMS e di Configuration Manager.  

-   Eliminazione della cache del client di Configuration Manager.  

-   Cancellazione della variabile di sito assegnato per il client di Configuration Manager.  

-   Installazione di tutti i criteri di Configuration Manager locali.  

-   Rimozione della chiave radice attendibile per il client di Configuration Manager.  

Questo passaggio della sequenza di attività può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE.  

Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Immagini** e selezionare **Prepara client ConfigMgr per l'acquisizione** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Questo passaggio non richiede nessuna impostazione nella scheda **Proprietà**.



##  <a name="BKMK_PrepareWindowsforCapture"></a> Prepara Windows per l'acquisizione  
 Usare questo passaggio per specificare le opzioni di Sysprep per l'acquisizione di un'immagine del sistema operativo nel computer di riferimento. Questa azione della sequenza di attività esegue Sysprep e quindi riavvia il computer nell'immagine di avvio di Windows PE specificata per la sequenza di attività. Questa operazione non riesce se il computer di riferimento fa parte di un dominio.  

 Questo passaggio della sequenza di attività può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE. Per informazioni sulle variabili della sequenza di attività per questa azione della sequenza di attività, vedere [Prepare Windows for Capture Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_PrepareWindowsCapture).  

 Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Immagini** e selezionare **Prepara Windows per l'acquisizione** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Crea automaticamente l'elenco di driver di archiviazione di massa**  
 Selezionare questa opzione per fare in modo che Sysprep crei automaticamente un elenco di driver di archiviazione di massa dal computer di riferimento. Questa opzione abilita l'opzione per la creazione di driver di archiviazione di massa del file sysprep.inf nel computer di riferimento. Per altre informazioni su questa impostazione, vedere la documentazione di Sysprep.  

 **Non reimpostare il flag di attivazione**  
 Selezionare questa opzione per impedire a Sysprep di reimpostare il flag di attivazione del prodotto.  



##  <a name="BKMK_PreProvisionBitLocker"></a> Eseguire il pre-provisioning di BitLocker  
 Usare questo passaggio per attivare BitLocker in un'unità mentre si trova in Windows PE. Solo lo spazio su disco usato viene crittografato e pertanto i tempi di crittografia sono molto più veloci. È possibile applicare le opzioni di gestione delle chiavi usando il passaggio [Attiva BitLocker](#BKMK_EnableBitLocker) della sequenza di attività dopo l'installazione del sistema operativo. Questo passaggio può essere eseguito solo in Windows PE. Non può essere eseguito in un sistema operativo standard.  

> [!IMPORTANT]  
>  Il pre-provisioning di BitLocker richiede almeno Windows 7. Il computer deve anche contenere un modulo TPM (Trusted Platform Module) supportato e abilitato.  

 Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Dischi** e selezionare **Pre-provisioning di BitLocker** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Applica BitLocker all'unità specificata**  
 Specificare l'unità per cui si vuole abilitare BitLocker. Viene crittografato solo lo spazio usato sull'unità.  

 **Ignora questo passaggio per computer senza TPM o con TPM non abilitato**  
 Selezionare questa opzione per ignorare la crittografia delle unità in un computer che non contiene un modulo TPM supportato o abilitato. Usare ad esempio questa opzione quando si distribuisce un sistema operativo in una macchina virtuale.  



##  <a name="BKMK_ReleaseStateStore"></a> Rilascia archiviazione stati  
 Usare questo passaggio per notificare al punto di migrazione stato il completamento dell'azione di acquisizione o ripristino. Usare questo passaggio insieme ai passaggi **Richiedi archiviazione stati**, **Acquisisci stato utente** e **Ripristina stato utente**. Usare questi passaggi per eseguire la migrazione di dati dello stato utente mediante un punto di migrazione stato e l'Utilità di migrazione stato utente (USMT).  

 Per altre informazioni sulla gestione dello stato utente durante la distribuzione di sistemi operativi, vedere [Manage user state](../get-started/manage-user-state.md) (Gestire lo stato utente).  

 Se si usa il passaggio **Richiedi archiviazione stati** per richiedere l'accesso a un punto di migrazione per *acquisire* lo stato utente, questo passaggio segnala al punto di migrazione stato che il processo di acquisizione è stato completato. Quindi il punto di migrazione stato contrassegna i dati dello stato utente come disponibili per il ripristino. Il punto di migrazione stato imposta le autorizzazioni di controllo dell'accesso per i dati dello stato utente, in modo che solo il computer di ripristino disponga di accesso di sola lettura.  

 Se si usa il passaggio **Richiedi archiviazione stati** per richiedere l'accesso a un punto di migrazione per *ripristinare* lo stato utente, questo passaggio segnala al punto di migrazione stato che il processo di ripristino è stato completato. Quindi il punto di migrazione stato attiva le proprie impostazioni di memorizzazione dati configurate.  

> [!IMPORTANT]  
>  Una procedura consigliata è l'impostazione dell'opzione **Continua in caso di errori** per tutti i passaggi inclusi tra il passaggio **Richiedi archiviazione stati** e il passaggio **Rilascia archiviazione stati**. Per ogni passaggio **Richiedi archiviazione stati** deve essere presente un passaggio **Rilascia archiviazione stati**.  

 Questo passaggio della sequenza di attività può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE. Per informazioni sulle variabili della sequenza di attività per questa azione della sequenza di attività, vedere [Release State Store Sequence Action Variables](task-sequence-action-variables.md#BKMK_ReleaseStateStore).  

 Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Stato utente** e selezionare **Rilascia archiviazione stati** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Questo passaggio non richiede nessuna impostazione nella scheda **Proprietà**.



##  <a name="BKMK_RequestStateStore"></a> Richiedi archiviazione stati  
 Usare questo passaggio per richiedere l'accesso a un punto di migrazione stato durante l'acquisizione o il ripristino dello stato.  

 Per altre informazioni sulla gestione dello stato utente durante la distribuzione di sistemi operativi, vedere [Manage user state](../get-started/manage-user-state.md) (Gestire lo stato utente).  

 Usare questo passaggio insieme ai passaggi **Rilascia archiviazione stati**, **Acquisisci stato utente** e **Ripristina stato utente**. Usare questi passaggi per eseguire la migrazione dello stato del computer mediante un punto di migrazione stato e l'Utilità di migrazione stato utente (USMT).  

> [!NOTE]  
>  Dopo la creazione di un nuovo punto di migrazione stato, l'archiviazione dello stato utente non è disponibile per un tempo massimo pari a un'ora. Per attivare più rapidamente la disponibilità, modificare le impostazioni delle proprietà del punto di migrazione stato in modo da attivare un aggiornamento del file di controllo del sito.  

 Questo passaggio della sequenza di attività può essere eseguito in un sistema operativo standard e in Windows PE per USMT offline. Per informazioni sulle variabili della sequenza di attività per questa azione della sequenza di attività, vedere [Request State Store Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RequestState).  

Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Stato utente** e selezionare **Richiedi archiviazione stati** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Acquisisci stato dal computer**  
 Trovare un punto di migrazione stato che soddisfi i requisiti minimi definiti nelle impostazioni del punto di migrazione stato. Ad esempio **Numero massimo di client** e **Minimum amount of free disk space** (Quantità minima di spazio libero su disco). Questa opzione non garantisce che al momento della migrazione dello stato sia disponibile spazio su disco sufficiente. L'opzione richiede l'accesso al punto di migrazione stato per l'acquisizione dello stato utente e delle impostazioni da un computer.  

 Se il sito di Configuration Manager dispone di più punti di migrazione stato attivi, questo passaggio consente di trovare un punto di migrazione stato con spazio su disco disponibile. La sequenza di attività definisce un elenco di punti di migrazione stato nel punto di gestione, quindi valuta ogni punto di migrazione finché non ne rileva uno che soddisfa i requisiti minimi.  

 **Ripristina stato da un altro computer**  
 Richiedere l'accesso a un punto di migrazione stato per ripristinare le impostazioni e lo stato utente acquisiti in precedenza in un computer di destinazione.  

 Se sono presenti più punti di migrazione stato, questo passaggio individua il punto di migrazione stato che dispone dello stato per il computer di destinazione.  

 **Numero di tentativi**  
 Numero di tentativi effettuati da questo passaggio per trovare un punto di migrazione stato appropriato prima di restituire un esito negativo.  

 **Intervallo tra tentativi (in secondi)**  
 Quantità di tempo, in secondi, di attesa da parte del passaggio della sequenza di attività prima di effettuare nuovi tentativi.  

 **Se l'account del computer non riesce a connettersi all'archiviazione stati, utilizzare l'account di accesso di rete**  
 Se la sequenza di attività non può accedere al punto di migrazione stato tramite l'account del computer, esegue la connessione con le credenziali dell'account di accesso di rete. Questa opzione è meno sicura perché è possibile che altri computer usino l'account di accesso di rete per accedere allo stato archiviato. L'opzione può essere necessaria se il computer di destinazione non è aggiunto a un dominio.  



##  <a name="BKMK_RestartComputer"></a> Riavvia computer  
 Usare questo passaggio per riavviare il computer che esegue la sequenza di attività. Dopo il riavvio il computer continua automaticamente con il passaggio successivo della sequenza di attività.  

 Questo passaggio può essere eseguito in un sistema operativo standard o in Windows PE. Per altre informazioni sulle variabili della sequenza di attività per questa azione della sequenza di attività, vedere [Variabili di azione della sequenza di attività Riavvia computer](task-sequence-action-variables.md#BKMK_RestartComputer).  

 Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Stato utente** e selezionare **Riavvia computer** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **L'immagine d'avvio assegnata a questa sequenza attività**  
 Selezionare questa opzione per far sì che il computer di destinazione usi l'immagine di avvio assegnata alla sequenza di attività. La sequenza di attività usa l'immagine di avvio per eseguire i passaggi successivi in Windows PE.  

 **Il sistema operativo predefinito attualmente installato**  
 Selezionare questa opzione per il computer di destinazione per il riavvio nel sistema operativo installato.  

 **Invia notifica all'utente prima del riavvio**  
 Selezionare questa opzione per visualizzare una notifica all'utente prima del riavvio del computer di destinazione. Il passaggio seleziona questa opzione per impostazione predefinita.  

 **Messaggio di notifica**  
 Immettere un messaggio di notifica da visualizzare all'utente prima del riavvio del computer di destinazione.  

 **Timeout della visualizzazione messaggio**  
 Specificare la quantità di tempo in secondi prima del riavvio del computer di destinazione. Il valore predefinito è 60 secondi.  



##  <a name="BKMK_RestoreUserState"></a> Ripristina stato utente  
 Usare questo passaggio per avviare l'Utilità di migrazione stato utente (USMT) e ripristinare lo stato utente e le impostazioni nel computer di destinazione. Usare questo passaggio in combinazione con il passaggio **Acquisisci stato utente**.  

 Per altre informazioni sulla gestione dello stato utente durante la distribuzione di sistemi operativi, vedere [Manage user state](../get-started/manage-user-state.md) (Gestire lo stato utente).  

 Usare questo passaggio con i passaggi **Richiedi archiviazione stati** e **Rilascia archiviazione stati** per salvare o ripristinare le impostazioni dello stato con un punto di migrazione stato. In USMT 3.0 e versioni successive questa opzione decrittografa sempre l'archiviazione stati USMT usando una chiave di crittografia generata e gestita da Configuration Manager.  

 Il passaggio **Ripristina stato utente** consente il controllo di un sottoinsieme limitato delle opzioni USMT più usate. Specificare opzioni della riga di comando aggiuntive con la variabile della sequenza di attività OSDMigrateAdditionalRestoreOptions.  

> [!IMPORTANT]  
>  Se si usa questo passaggio per uno scopo non associato a uno scenario di distribuzione del sistema operativo, aggiungere il passaggio [Riavvia computer](#BKMK_RestartComputer) subito dopo il passaggio **Ripristina stato utente**.  

 Questo passaggio può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE. Per informazioni sulle variabili della sequenza di attività per questa azione della sequenza di attività, vedere [Restore User State Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RestoreUserState).  

 Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Stato utente** e selezionare **Ripristina stato utente** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Pacchetto degli strumenti di migrazione dello stato utente**  
 Specificare il pacchetto contenente la versione di USMT che verrà usata in questo passaggio. Questo pacchetto non richiede alcun programma. Quando viene eseguito il passaggio la sequenza di attività usa la versione di USMT del pacchetto specificato. Specificare un pacchetto contenente la versione di USMT a 32 bit o a 64 bit. L'architettura di USMT dipende dall'architettura del sistema operativo nel quale la sequenza di attività ripristina lo stato. 

 **Ripristina tutti i profili utente acquisiti con le opzioni standard**  
 Ripristina i profili utente acquisiti con le opzioni standard. Per personalizzare le opzioni ripristinate da USMT, selezionare **Customize user profile capture** (Personalizza acquisizione dei profili utente).  

 **Personalizza le modalità di ripristino dei profili utente**  
 Permette di personalizzare i file da ripristinare nel computer di destinazione. Fare clic su **File** per specificare i file di configurazione nel pacchetto USMT da usare per il ripristino dei profili utente. Per aggiungere un file di configurazione, immettere il nome del file nella casella **Nome file** , quindi fare clic su **Aggiungi**. Nel riquadro File sono elencati i file di configurazione usati da USMT. Il file con estensione xml specificato definisce il file utente che viene ripristinato da USMT.  

 **Ripristina profili utente del computer locale**  
 Ripristina i profili utente del computer locale. Questi profili non sono disponibili per gli utenti di dominio. È necessario assegnare nuove password agli account utente locali ripristinati. USMT non esegue la migrazione delle password originali. Immettere la nuova password nella casella **Password** e confermare la password nella casella **Conferma password** .  

 **Continua se non è possibile ripristinare dei file**  
 Continua a ripristinare lo stato utente e le impostazioni anche se USMT non riesce a ripristinare alcuni file. Il passaggio abilita questa opzione per impostazione predefinita. Se si disabilita questa opzione e USMT rileva errori durante il ripristino dei file, questo passaggio restituisce immediatamente un errore. USMT non ripristina tutti i file.   

 **Abilita la registrazione dettagliata**  
 Abilitare questa opzione per generare informazioni di file di log più dettagliate. Durante il ripristino dello stato, per impostazione predefinita la sequenza di attività genera il file Loadstate.log nella cartella log della sequenza di attività, \windows\system32\ccm\logs.  



##  <a name="BKMK_RunCommandLine"></a> Esegui riga di comando  
 Usare questo passaggio per eseguire la riga di comando specificata.  

 Questo passaggio può essere eseguito in un sistema operativo standard o in Windows PE. Per informazioni sulle variabili della sequenza di attività per questa azione della sequenza di attività, vedere [Run Command Line Task Sequence Action Variables](task-sequence-action-variables.md#BKMK_RunCommand).  

 Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Generale** e selezionare **Esegui riga di comando** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Riga di comando**  
 Specifica la riga di comando eseguita. Questo campo è obbligatorio. È consigliabile includere le estensioni del nome file, ad esempio vbs ed exe. Includere tutti i file di impostazione necessari, le opzioni della riga di comando e le altre opzioni.  

 Se non è stata specificata un'estensione per il nome file, Configuration Manager prova a usare le estensioni com, exe e bat. Se il nome file ha un'estensione non eseguibile, Configuration Manager prova ad applicare un'associazione locale. Ad esempio, se la riga di comando è readme.gif, Configuration Manager avvia l'applicazione specificata nel computer di destinazione per l'apertura dei file con estensione gif.  

 Esempi:  

 `setup.exe /a`  

 `cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

> [!NOTE]  
>  Per un'esecuzione corretta, far precedere alle azioni della riga di comando il comando **cmd.exe /c**. Sono esempi di queste azioni i comandi di reindirizzamento output, piping e copia.  

 **Disattiva il reindirizzamento del file system a 64 bit**  
 Per impostazione predefinita i sistemi operativi a 64 bit usano il redirector del file system WOW64 per l'esecuzione di righe di comando. Il comportamento consiste nel trovare versioni a 32 bit di file eseguibili e librerie del sistema operativo. Selezionare questa opzione per disabilitare l'uso del redirector del file system WOW64. Windows esegue il comando con versioni native a 64 bit dei file eseguibili e delle librerie del sistema operativo. Questa opzione non produce alcun effetto se eseguita in un sistema operativo a 32 bit.  

 **Da**  
 Specifica la cartella eseguibile per il programma. Sono consentiti al massimo 127 caratteri. Questa cartella può essere un percorso assoluto nel computer di destinazione o un percorso relativo alla cartella del punto di distribuzione contenente il pacchetto. Questo campo è facoltativo.  

 Esempi:  

 **c:\officexp**  

 **i386**  

> [!NOTE]  
>  Il pulsante **Sfoglia** consente di cercare file e cartelle nel computer locale. Qualsiasi elemento selezionato deve essere presente anche nel computer di destinazione, nello stesso percorso e con lo stesso nome di file e cartella.  

 **Pacchetto**  
 Quando nella riga di comando si specificano file o programmi che non sono già presenti nel computer di destinazione, selezionare questa opzione per specificare il pacchetto di Configuration Manager contenente i file appropriati. Questo pacchetto non richiede alcun programma. Questa opzione non è necessaria se i file specificati esistono nel computer di destinazione.  

 **Timeout**  
 Specifica un valore che rappresenta il tempo concesso da Configuration Manager per l'esecuzione della riga di comando. Questo valore può essere compreso tra 1 e 999 minuti. Il valore predefinito è 15 minuti.  

 Questa opzione è disabilitata per impostazione predefinita.  

> [!IMPORTANT]  
>  Se si immette un valore insufficiente per il completamento del comando specificato, il passaggio ha esito negativo. Di conseguenza, a seconda delle altre impostazioni di controllo, è possibile che l'intera sequenza di attività abbia esito negativo. In caso di scadenza del timeout, Configuration Manager termina il processo della riga di comando.  

 **Esegui questo passaggio come account specificato**  
 Specifica che la riga di comando viene eseguita come account utente Windows diverso dall'account di sistema locale.  

> [!NOTE]  
>  Per eseguire semplici script o comandi con un altro account dopo l'installazione del sistema operativo, è prima necessario aggiungere l'account al computer. È anche necessario ripristinare il profilo dell'account utente di Windows per eseguire programmi più complessi, ad esempio Windows Installer.  

 **Account**  
 Specifica l'account utente di Windows usato da questo passaggio per eseguire la riga di comando. La riga di comando viene eseguita con le autorizzazioni dell'account specificato. Fare clic su **Imposta** per specificare l'utente locale o l'account di dominio.  

> [!IMPORTANT]  
>  Se questo passaggio specifica un account utente e viene eseguito in Windows PE, l'azione ha esito negativo. Non è possibile includere Windows PE in un dominio. L'errore viene registrato nel file smsts.log.  



##  <a name="BKMK_RunPowerShellScript"></a> Esegui script PowerShell  
 Usare questo passaggio per eseguire lo script PowerShell specificato.  

 Questo passaggio può essere eseguito in un sistema operativo standard o in Windows PE. Per eseguire questo passaggio in Windows PE, è necessario abilitare PowerShell nell'immagine di avvio. È possibile abilitare Windows PowerShell (WinPE-PowerShell) dalla scheda **Componenti facoltativi** nelle proprietà per l'immagine di avvio. Per altre informazioni su come modificare un'immagine d'avvio, vedere [Manage boot images](../get-started/manage-boot-images.md) (Gestire le immagini d'avvio).  

> [!NOTE]  
>  PowerShell non è abilitato per impostazione predefinita nei sistemi operativi Windows Embedded.  

Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Generale** e selezionare **Esegui script PowerShell** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Pacchetto**  
 Specifica il pacchetto di Configuration Manager contenente lo script PowerShell. Un pacchetto può includere più script PowerShell.  

 **Nome script**  
 Specifica il nome dello script PowerShell da eseguire. Questo campo è obbligatorio.  

 **Parametri**  
 Specifica i parametri passati allo script Windows PowerShell. Questi parametri corrispondono ai parametri di script Windows PowerShell nella riga di comando.  

> [!IMPORTANT]  
>  Specificare i parametri usati dallo script, non per la riga di comando di Windows PowerShell.  
>   
>  L'esempio seguente include parametri validi:  
>   
>  `-MyParameter1 MyValue1 -MyParameter2 MyValue2`  
>   
>  L'esempio seguente include parametri non validi: I primi due elementi sono parametri della riga di comando di Windows PowerShell (**-NoLogo** e **-ExecutionPolicy Unrestricted**). Lo script non usa questi parametri.  
>   
>  `-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`  

 **Criteri di esecuzione di PowerShell**  
 Determinare quali script di Windows PowerShell possono essere eseguiti nel computer. Scegliere uno dei criteri di esecuzione seguenti:  

-   **Tutti firmati**: vengono eseguiti solo gli script firmati da un editore attendibile.  

-   **Non definito**: non viene definito alcun criterio di esecuzione.  

-   **Ignora**: vengono caricati tutti i file di configurazione e vengono eseguiti tutti gli script. Se si scarica uno script non firmato da Internet, Windows PowerShell non richiede l'autorizzazione prima di eseguire tale script.  

> [!IMPORTANT]  
>  PowerShell 1.0 non supporta i criteri di esecuzione Non definito e Ignora.  



##  <a name="child-task-sequence"></a> Esegui la sequenza di attività

A partire da Configuration Manager versione 1710 è possibile aggiungere un nuovo passaggio che esegue un'altra sequenza di attività. Questo passaggio crea una relazione padre-figlio tra le sequenze di attività. Le sequenze di attività figlio consentono di creare sequenze di attività più modulari e riutilizzabili.

Quando si aggiunge una sequenza di attività figlio a una sequenza di attività, tenere presente quanto segue:
 - Le sequenze di attività padre e figlio sono di fatto combinate in un unico criterio eseguito dal client.
 - L'ambiente è globale. Se la sequenza di attività padre imposta una variabile e quindi la sequenza di attività figlio la modifica, la variabile mantiene il valore più recente. Se la sequenza di attività figlio crea una nuova variabile, la variabile è disponibile per la parte restante della sequenza di attività padre.
 - I messaggi di stato vengono inviati con la procedura normale per un'operazione sequenza di attività singola.
 - Le sequenze di attività scrivono voci nel file smsts.log. Le nuove voci di registro evidenziano l'avvio di una sequenza di attività figlio.

Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Generale** e selezionare **Esegui la sequenza di attività** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

**Selezionare la sequenza di attività da eseguire**  
 Fare clic su **Sfoglia** per selezionare la sequenza di attività figlio. La finestra di dialogo **Seleziona una sequenza di attività** non visualizza la sequenza di attività padre.



##  <a name="BKMK_SetDynamicVariables"></a> Imposta variabili dinamiche  
 Usare questo passaggio per eseguire le azioni seguenti:  

1.  Recupero di informazioni dal computer e dall'ambiente in cui si trova, quindi impostazione delle variabili specificate della sequenza di attività con le informazioni ottenute.  

2.  Valutazione delle regole definite e impostazione delle variabili della sequenza di attività in base ai valori configurati per le regole che restituiscono true.  

La sequenza di attività imposta automaticamente le variabili della sequenza di attività di sola lettura seguenti:  
 -   &#95;SMSTSMake  
 -   &#95;SMSTSModel  
 -   &#95;SMSTSMacAddresses  
 -   &#95;SMSTSIPAddresses  
 -   &#95;SMSTSSerialNumber  
 -   &#95;SMSTSAssetTag  
 -   &#95;SMSTSUUID  

Questo passaggio può essere eseguito in un sistema operativo standard o in Windows PE. Per altre informazioni sulle variabili della sequenza di attività, vedere [Variabili di azione della sequenza di attività](task-sequence-action-variables.md).  

Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Generale** e selezionare **Imposta variabili dinamiche** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

**Variabili e regole dinamiche**  
 Per impostare una variabile dinamica da usare nella sequenza di attività, aggiungere una regola. Quindi impostare un valore per ogni variabile specificata nella regola. È anche possibile aggiungere una o più variabili senza aggiungere una regola. Quando si aggiunge una regola, scegliere tra le categorie seguenti:  

 -   **Computer**: valutare i valori per il tag asset hardware, l'UUID, il numero di serie o l'indirizzo MAC. Impostare più valori in base alle esigenze. Se uno dei valori è true, la regola restituisce true. Ad esempio la regola seguente restituisce true se il numero di serie è 5892087 e l'indirizzo MAC è 22-A4-5A-13-78-26.  

     `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

-   **Percorso**: valutare i valori per il gateway di rete predefinito.  

-   **Marca e modello**: valutare i valori relativi a marca e modello di un computer. La regola restituisce true solo se entrambi i valori restituiscono true.   

    <!-- for future edits: an escape code must be used for the bolded asterisk character, but may be removed somewhere along the way. Instead of five asterisk, should be bold tags with &#42; in-between -->

    A partire da Configuration Manager versione 1610 è possibile usare un asterisco (**&#42;**) e un punto interrogativo (**?**) come caratteri jolly, dove **&#42;** corrisponde a più caratteri e **?** corrisponde a un solo carattere. Ad esempio, la stringa "DELL*900?" corrisponde a DELL-ABC-9001 e a DELL9009. 

    Specificare un asterisco (**&#42;**) e un punto interrogativo (**?**) come caratteri jolly, dove **&#42;** corrisponde a più caratteri e **?** corrisponde a un solo carattere. Ad esempio, la stringa "DELL*900?" corrisponde a DELL-ABC-9001 e a DELL9009.

-   **Variabile della sequenza di attività**: aggiungere una variabile della sequenza di attività, una condizione e un valore da valutare. La regola restituisce true quando il valore impostato per la variabile soddisfa la condizione specificata.  

    Specificare una o più variabili da impostare per una regola che restituisce true oppure impostare variabili senza usare una regola. Selezionare una variabile esistente o creare una variabile personalizzata.  

     -   **Existing task sequence variables** (Variabili esistenti della sequenza di attività): selezionare una o più variabili esistenti da un elenco di variabili della sequenza di attività. Le variabili di matrice non sono disponibili per la selezione.  

     -   **Custom task sequence variables** (Variabili personalizzate della sequenza di attività): definire una variabile personalizzata della sequenza di attività. È anche possibile specificare una variabile esistente della sequenza di attività. Questa impostazione è utile per specificare una matrice di variabili esistenti, ad esempio OSDAdapter, perché le matrici di variabili non sono incluse nell'elenco di variabili esistenti della sequenza di attività.  

Dopo la selezione delle variabili per una regola, è necessario fornire un valore per ogni variabile. La variabile è impostata sul valore specificato quando la regola restituisce true. Per ogni variabile è possibile selezionare **Valore segreto** per nascondere il valore della variabile. Per impostazione predefinita, alcune variabili esistenti nascondono i valori, ad esempio la variabile OSDCaptureAccountPassword della sequenza di attività.  

> [!IMPORTANT]  
>  Configuration Manager rimuove tutti i valori contrassegnati come **Valore segreto** quando si importa una sequenza di attività con il passaggio **Imposta variabili dinamiche**. Immettere di nuovo il valore per la variabile dinamica dopo l'importazione della sequenza di attività.  



##  <a name="BKMK_SetTaskSequenceVariable"></a> Imposta variabile della sequenza di attività  
Usare questo passaggio per configurare il valore di una variabile usata con la sequenza di attività.  

Questo passaggio può essere eseguito in un sistema operativo standard o in Windows PE. Le variabili della sequenza di attività vengono lette dalle azioni della sequenza di attività e specificano il comportamento di tali azioni. Per altre informazioni su variabili di azione specifiche della sequenza di attività, vedere [Variabili di azione della sequenza di attività](task-sequence-action-variables.md). Per altre informazioni su variabili predefinite specifiche della sequenza di attività, vedere [Variabili predefinite della sequenza di attività](/sccm/osd/understand/task-sequence-built-in-variables).

Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Generale** e selezionare **Imposta variabile della sequenza di attività** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Variabile della sequenza di attività**  
 Specificare il nome di una variabile di azione o predefinita della sequenza di attività oppure specificare un nome di variabile definito dall'utente.  

 **Valore**  
 La sequenza di attività imposta la variabile su questo valore. Impostare questa variabile della sequenza di attività sul valore di un'altra variabile della sequenza di attività con la sintassi %varname%.  



##  <a name="BKMK_SetupWindowsandConfigMgr"></a> Imposta Windows e ConfigMgr  
 Usare questo passaggio per eseguire la transizione da Windows PE al nuovo sistema operativo. Questo passaggio della sequenza di attività è una parte necessaria di qualsiasi distribuzione del sistema operativo. Installa il client di Configuration Manager nel nuovo sistema operativo e prepara la sequenza di attività per continuare l'esecuzione nel nuovo sistema operativo.  

 Questo passaggio può essere eseguito solo in Windows PE. Non può essere eseguito in un sistema operativo standard. Per altre informazioni sulle variabili della sequenza di attività per questa azione della sequenza di attività, vedere [Variabili di azione della sequenza di attività Imposta Windows e ConfigMgr](task-sequence-action-variables.md#BKMK_SetupWindows).  

 Questo passaggio sostituisce le variabili della directory sysprep.inf o unattend.xml, ad esempio %WINDIR% e %ProgramFiles%, con la directory di installazione di Windows PE X:\Windows. La sequenza di attività ignora le variabili specificate usando queste variabili di ambiente.  

 Usare questo passaggio della sequenza di attività per eseguire le azioni seguenti:  

1.  Operazioni preliminari: Windows PE  

    1.  Sostituire le variabili della sequenza di attività nel file unattend.xml.  

    2.  Scaricare il pacchetto contenente il client di Configuration Manager. Aggiungere il pacchetto all'immagine distribuita.  

2.  Configurazione di Windows  

    1.  Installazione basata su immagine  

        1.  Disabilitare il client di Configuration Manager nell'immagine, se presente. In altre parole, disabilitare l'avvio automatico del servizio client di Configuration Manager.  

        2.  Aggiornare il Registro di sistema nell'immagine distribuita per avviare il sistema operativo distribuito con la stessa lettera di unità del computer di riferimento.  

        3.  Riavviare nel sistema operativo distribuito.  

        4.  L'installazione minima di Windows viene eseguita usando un file di risposte sysprep.inf o unattend.xml specificato in precedenza e in cui sono state rimosse tutte le interazioni con gli utenti finali. Se si usa il passaggio **Applica impostazioni di rete** per l'aggiunta a un dominio, queste informazioni si trovano nel file di risposte. L'installazione minima di Windows aggiunge il computer al dominio.  

    2.  Installazione basata su Setup.exe.  Esegue Setup.exe con il processo di installazione di Windows tipico:  

        1.  Copiare nell'unità disco rigido il pacchetto di aggiornamento del sistema operativo specificato nel passaggio **Applica sistema operativo**.  

        2.  Eseguire il riavvio nel sistema operativo appena distribuito.  

        3.  L'installazione minima di Windows viene eseguita usando il file di risposte sysprep.inf o unattend.xml specificato in precedenza e in cui sono state rimosse tutte le impostazioni dell'interfaccia utente. Se si usa il passaggio **Applica impostazioni di rete** per l'aggiunta a un dominio, queste informazioni si trovano nel file di risposte. L'installazione minima di Windows aggiunge il computer al dominio.  

3.  Impostazione del client di Configuration Manager  

    1.  Al termine dell'installazione minima di Windows, verrà ripresa la sequenza di attività usando setupcomplete.cmd.  

    2.  Abilitare o disabilitare l'account di amministratore locale, in base all'opzione selezionata nel passaggio **Applica impostazioni Windows**.  

    3.  Installare il client di Configuration Manager usando il pacchetto scaricato in precedenza e le proprietà di installazione specificate in questo passaggio. Il client viene installato in "modalità di provisioning" per impedire che elabori nuove richieste di criteri fino al completamento della sequenza di attività.  

    4.  Attendere la completa operatività del client.  

4.  L'esecuzione della sequenza di attività continua con il passaggio successivo.  

<!-- Engineering confirmed that the task sequence does nothing with respect to group policy processing.
> [!NOTE]  
>  The **Setup Windows and ConfigMgr** task sequence action is responsible for running Group Policy on the newly installed computer. The Group Policy is applied after the task sequence is finished.  
-->

Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Immagini** e selezionare **Imposta Windows e ConfigMgr** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
 Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

 **Pacchetto client**  
 Fare clic su **Sfoglia** e selezionare il pacchetto di installazione del client di Configuration Manager da usare in questo passaggio.  

 **Usa il pacchetto client di pre-produzione se disponibile**  
 Se è disponibile un pacchetto client di pre-produzione, la sequenza di attività usa tale pacchetto invece del pacchetto client di produzione. Il client di pre-produzione è una versione più recente per il testing nell'ambiente di produzione. Fare clic su **Sfoglia** e selezionare il pacchetto di installazione del client di pre-produzione da usare in questo passaggio.  

 **Proprietà di installazione**  
 L'assegnazione sito e la configurazione predefinita vengono specificate automaticamente dall'azione della sequenza di attività. È possibile usare questo campo per specificare eventuali proprietà di installazione aggiuntive da usare quando si installa il client. Per immettere più proprietà di installazione, separarle con uno spazio.  

 È possibile specificare opzioni della riga di comando da usare durante l'installazione del client. Ad esempio, è possibile immettere **/skipprereq: silverlight.exe** per segnalare a CCMSetup.exe di non installare i prerequisiti di Microsoft Silverlight. Per altre informazioni sulle opzioni della riga di comando disponibili per CCMSetup.exe, vedere [About client installation properties](../../core/clients/deploy/about-client-installation-properties.md) (Informazioni sulle proprietà di installazione del client).  

### <a name="options"></a>Opzioni
> [!NOTE]
> Non abilitare **Continua in caso di errore** nella scheda **Opzioni**. Sia che questa opzione sia abilitata o meno, se si verifica un errore durante questo passaggio la sequenza di attività ha esito negativo.



##  <a name="BKMK_UpgradeOS"></a> Aggiorna sistema operativo  
 > [!TIP]  
 > A partire da Windows 10 versione 1709 il supporto include più edizioni. Quando si configura una sequenza di attività per l'uso di un pacchetto di aggiornamento del sistema operativo o di un'immagine del sistema operativo, verificare di selezionare un'[edizione supportata](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).

 Usare questo passaggio per aggiornare una versione precedente di Windows a una versione più recente di Windows 10.  

 Questo passaggio della sequenza di attività può essere eseguito solo in un sistema operativo standard. Non può essere eseguito in Windows PE.  

Nell'editor della sequenza di attività fare clic su **Aggiungi**, selezionare **Immagini** e selezionare **Aggiorna sistema operativo** per aggiungere questo passaggio. 

### <a name="properties"></a>Proprietà  
Nella scheda **Proprietà** per questo passaggio, configurare le impostazioni descritte in questa sezione.  

**Pacchetto di aggiornamento**  
 Selezionare questa opzione per specificare il pacchetto di aggiornamento del sistema operativo Windows 10 da usare per l'aggiornamento.  

**Percorso di origine**  
 Specifica un percorso locale o di rete per il supporto Windows 10 usato dall'installazione di Windows. Questa impostazione corrisponde all'opzione della riga di comando **/InstallFrom** di Installazione di Windows. È anche possibile specificare una variabile, ad esempio %mycontentpath% o %DPC01%. Quando si usa una variabile per il percorso di origine, deve essere specificata prima nella sequenza di attività. Ad esempio, se si usa il passaggio [Scaricare il contenuto del pacchetto](#BKMK_DownloadPackageContent) nella sequenza di attività, è possibile specificare una variabile per il percorso del pacchetto di aggiornamento del sistema operativo. È quindi possibile usare tale variabile per il percorso di origine per questo passaggio.  

**Edizione**  
 Specificare l'edizione all'interno del supporto del sistema operativo da usare per l'aggiornamento.  

**Codice Product Key**  
 Specificare il codice Product Key da applicare al processo di aggiornamento  

**Specifica il seguente contenuto del driver in Installazione di Windows durante l'aggiornamento**  
 Aggiungere driver al computer di destinazione durante il processo di aggiornamento. Questa impostazione corrisponde all'opzione della riga di comando **/InstallDriver** di Installazione di Windows. I driver devono essere compatibili con Windows 10. specificare una delle opzioni seguenti:  

-   **Pacchetto driver**: fare clic su **Sfoglia** e selezionare un pacchetto di driver esistente nell'elenco.  

-   **Contenuto preconfigurato**: selezionare questa opzione per specificare il percorso per il pacchetto di driver. È possibile specificare una cartella locale, un percorso di rete o una variabile della sequenza di attività. Quando si usa una variabile per il percorso di origine, deve essere specificata prima nella sequenza di attività. Ad esempio, usando il passaggio [Download Package Content](task-sequence-steps.md#BKMK_DownloadPackageContent) .  

**Timeout (minuti)**  
 Specifica il numero di minuti prima che questo passaggio di Configuration Manager abbia esito negativo. Questa opzione è utile se l'installazione di Windows interrompe l'elaborazione ma non viene terminata.  

**Esegui analisi di compatibilità di Installazione di Windows senza avviare l'aggiornamento**  
 Esegue l'analisi di compatibilità di Installazione di Windows senza avviare il processo di aggiornamento. Questa impostazione corrisponde all'opzione della riga di comando **/Compat ScanOnly** di Installazione di Windows. Quando si usa questa opzione è necessario distribuire l'intera origine dell'installazione. Il programma di installazione restituisce un codice di uscita come risultato dell'analisi. Nella tabella seguente sono elencati alcuni dei più comuni codici di uscita.  

|Codice di uscita|Dettagli|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|Nessun problema di compatibilità ("esito positivo").|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0xC1900208)|Problemi di compatibilità su cui è possibile intervenire.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|L'opzione di migrazione selezionata non è disponibile. Ad esempio, un aggiornamento da Enterprise a Professional.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Non idoneo per Windows 10.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0xC190020E)|Spazio libero su disco insufficiente.|  

Per altre informazioni su questo parametro, vedere [Opzioni della riga di comando di Installazione di Windows](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx)  

**Ignora tutti i messaggi sulla compatibilità non rilevanti**  
 Specifica che il programma di installazione completa l'installazione ignorando eventuali messaggi di compatibilità non rilevanti. Questa impostazione corrisponde all'opzione della riga di comando **/Compat IgnoreWarning** di Installazione di Windows.  

**Aggiorna dinamicamente Installazione di Windows con Windows Update**  
 Abilitare il programma di installazione per l'esecuzione di operazioni di aggiornamento dinamico, quali la ricerca, il download e l'installazione di aggiornamenti. Questa impostazione corrisponde all'opzione della riga di comando **/DynamicUpdate** di Installazione di Windows. Questa impostazione non è compatibile con gli aggiornamenti software di Configuration Manager. Abilitare questa opzione quando si gestiscono gli aggiornamenti con Windows Server Update Services (WSUS) in modalità autonoma o con Windows Update per le aziende.  

**Sostituisci i criteri e usa Microsoft Update predefinito** Ignorare temporaneamente i criteri locali in tempo reale per eseguire operazioni di aggiornamento dinamico e impostare il computer per la ricezione degli aggiornamenti da Windows Update.

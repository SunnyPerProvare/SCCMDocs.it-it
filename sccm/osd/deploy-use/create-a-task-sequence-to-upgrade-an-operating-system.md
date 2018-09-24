---
title: Creare una sequenza di attività per l'aggiornamento del sistema operativo
titleSuffix: Configuration Manager
description: Usare una sequenza di attività per eseguire automaticamente l'aggiornamento da Windows 7 o versioni successive a Windows 10
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bddcd356a3ee221d5b67935a5be91bbe89d2afc2
ms.sourcegitcommit: be8c0182db9ef55a948269fcbad7c0f34fd871eb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/23/2018
ms.locfileid: "42756055"
---
# <a name="create-a-task-sequence-to-upgrade-an-os-in-configuration-manager"></a>Creare una sequenza di attività per aggiornare un sistema operativo in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare le sequenze di attività in Configuration Manager per aggiornare automaticamente un sistema operativo in un computer di destinazione. L'aggiornamento può essere eseguito da Windows 7 o versione successiva fino a Windows 10 o da Windows Server 2012 o versione successiva fino a Windows Server 2016. Creare una sequenza di attività che faccia riferimento al pacchetto di aggiornamento del sistema operativo e a eventuali altri contenuti da installare, ad esempio applicazioni o aggiornamenti software. La sequenza di attività per aggiornare un sistema operativo fa parte dello scenario [Aggiornare Windows alla versione più recente](upgrade-windows-to-the-latest-version.md).  



## <a name="prerequisites"></a>Prerequisiti

Prima di creare la sequenza di attività, devono essere soddisfatti i requisiti seguenti:    

#### <a name="required"></a>Richiesto  

- Il [pacchetto di aggiornamento del sistema operativo](/sccm/osd/get-started/manage-operating-system-upgrade-packages) deve essere disponibile nella console di Configuration Manager.  

- Quando si esegue l'aggiornamento a Windows Server 2016, selezionare l'impostazione **Ignore any dismissable compatibility messages** (Ignora eventuali messaggi di compatibilità che possono essere chiusi) nel passaggio della sequenza di attività Aggiorna sistema operativo. In caso contrario, l'aggiornamento ha esito negativo.  

#### <a name="required-if-used"></a>Obbligatorio (se usato)  

-   Gli [aggiornamenti software](/sccm/sum/get-started/synchronize-software-updates) devono essere sincronizzati nella console di Configuration Manager.  

-   Le [applicazioni](/sccm/apps/deploy-use/create-applications) devono essere aggiunte alla console di Configuration Manager.  



##  <a name="BKMK_UpgradeOS"></a> Creare una sequenza di attività per aggiornare un sistema operativo  

Per aggiornare il sistema operativo nei client, è possibile creare una sequenza di attività e selezionare **Aggiorna sistema operativo dal pacchetto di aggiornamento** nella Creazione guidata della sequenza di attività. La procedura guidata aggiunge i passaggi della sequenza di attività per aggiornare il sistema operativo, applicare gli aggiornamenti software e installare le applicazioni. 

#### <a name="to-create-a-task-sequence-that-upgrades-an-os"></a>Per creare una sequenza di attività che esegua l'aggiornamento di un sistema operativo  

1.  Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e quindi fare clic su **Sequenze di attività**.  

2.  Nella scheda **Home** della barra multifunzione nel gruppo **Crea** fare clic su **Crea sequenza attività**.  

3.  Nella pagina **Crea una nuova sequenza di attività** della Creazione guidata della sequenza attività selezionare **Aggiorna sistema operativo dal pacchetto di aggiornamento**e quindi fare clic su **Avanti**.  

4.  Nella pagina **Informazioni sequenza di attività** specificare le impostazioni seguenti e quindi fare clic su **Avanti**:  

    -   **Nome sequenza di attività**: specificare un nome che identifica la sequenza di attività.  

    -   **Descrizione**: specificare una descrizione (facoltativo).  

5.  Nella pagina **Aggiorna il sistema operativo Windows** specificare le impostazioni seguenti e quindi fare clic su **Avanti**:  

    -   **Pacchetto di aggiornamento**: specificare il pacchetto di aggiornamento che contiene i file di origine per l'aggiornamento del sistema operativo. Verificare di avere selezionato il pacchetto di aggiornamento corretto esaminando le informazioni nel riquadro **Proprietà**. Per altre informazioni, vedere [Gestire i pacchetti di aggiornamento del sistema operativo](/sccm/osd/get-started/manage-operating-system-upgrade-packages).  

    -   **Indice edizione**: se sono presenti più indici edizione del sistema operativo nel pacchetto, selezionare l'indice edizione desiderato. Per impostazione predefinita, la procedura guidata seleziona il primo indice.  

    -   **Codice Product Key**: specificare il codice Product Key Windows per il sistema operativo da installare. Specificare i codici Product Key per contratti multilicenza codificati o i codici Product Key standard. Se si usa un codice Product Key standard, separare ogni gruppo di cinque caratteri con un trattino (-). Ad esempio: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX* Se l'aggiornamento è per un'edizione per contratti multilicenza, il codice Product Key potrebbe non essere obbligatorio.  

        > [!Note]  
        > Questo codice Product Key può essere un codice ad attivazione multipla (MAK) o un codice generico di contratti multilicenza (GVLK). Un codice GVLK è anche definito codice di configurazione client del servizio di gestione delle chiavi (KMS). Per altre informazioni, vedere [Pianificare l'attivazione dei contratti multilicenza](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Per un elenco di codici di configurazione client KMS, vedere l'[Appendice A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) della Guida di attivazione di Windows Server. 

    -   **Ignora tutti i messaggi sulla compatibilità non rilevanti**: selezionare questa impostazione se si esegue l'aggiornamento a Windows Server 2016. Se non si seleziona questa impostazione, la sequenza di attività non può essere completata perché il programma di installazione di Windows rimane in attesa che l'utente faccia clic su **Conferma** in una finestra di dialogo di compatibilità delle app di Windows.   

7.  Nella pagina **Includi aggiornamenti** specificare se installare gli aggiornamenti software obbligatori, tutti gli aggiornamenti software o nessuno. Fare quindi clic su **Avanti**. Se si sceglie di installare gli aggiornamenti software, Configuration Manager installa solo gli aggiornamenti assegnati alle raccolte di cui il computer di destinazione è membro.  

8.  Nella pagina **Installa applicazioni** specificare le applicazioni da installare nel computer di destinazione e quindi fare clic su **Avanti**. Se si seleziona più di un'applicazione, specificare anche se la sequenza di attività deve continuare se l'installazione di un'applicazione specifica non riesce.  

9. Completare la procedura guidata.  


> [!Important]  
> Quando la sequenza di attività viene eseguita in un dispositivo, il client di Configuration Manager crea diversi script per controllare il comportamento della sequenza di attività nei vari scenari. Al termine dell'esecuzione della sequenza di attività, il client non rimuove questi script fino a quando il computer non viene riavviato. Questi file di script non contengono informazioni riservate.  


A partire dalla versione 1802, il modello di sequenza di attività predefinito per l'aggiornamento sul posto di Windows 10 include gruppi aggiuntivi con azioni consigliate da aggiungere prima e dopo il processo di aggiornamento. Queste azioni sono comuni tra numerosi clienti che stanno aggiornando i propri dispositivi a Windows 10. Per altre informazioni, vedere i passaggi della sequenza di attività consigliata [per preparare l'aggiornamento](#recommended-task-sequence-steps-to-prepare-for-upgrade) e [ post-elaborazione](#recommended-task-sequence-steps-for-post-processing).

A partire dalla versione 1806, questo modello di sequenza di attività include anche un gruppo con azioni consigliate da aggiungere in caso di esito negativo del processo di aggiornamento. Queste azioni facilitano la risoluzione dei problemi. Per altre informazioni, vedere [Passaggi della sequenza di attività consigliati in caso di errore](#recommended-task-sequence-steps-on-failure).<!--1358500-->  



## <a name="configure-pre-cache-content"></a>Configurare la pre-cache del contenuto
<!--1021244--> La funzionalità pre-cache per le distribuzioni di sequenze di attività disponibili consente ai client di scaricare il contenuto pertinente dei pacchetti di aggiornamento del sistema operativo prima che un utente installi la sequenza di attività.  

> [!Note]  
> Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Abilitare le funzionalità facoltative degli aggiornamenti](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Si supponga, ad esempio, di volere una sola sequenza di attività di aggiornamento sul posto per tutti gli utenti, pur avendo molte architetture e lingue diverse. Nelle versioni precedenti il download del contenuto inizia quando l'utente installa una distribuzione di sequenze di attività disponibile da Software Center. Questo ritardo aggiunge ulteriore tempo prima che l'installazione sia pronta per essere avviata. Tutto il contenuto a cui viene fatto riferimento nella sequenza di attività viene scaricato. Questo contenuto include il pacchetto di aggiornamento del sistema operativo per tutte le lingue e tutte le architetture. Se ogni pacchetto di aggiornamento è circa 3 GB, il contenuto totale è molto elevato.

Con la funzionalità pre-cache del contenuto è possibile consentire al client di scaricare solo il pacchetto di aggiornamento applicabile per il sistema operativo e tutto il contenuto aggiuntivo a cui si fa riferimento, non appena riceve la distribuzione. Quando l'utente fa clic su **Installa** in Software Center, il contenuto è pronto. L'installazione inizia rapidamente, dato che il contenuto si trova nel disco rigido locale.

> [!NOTE]  
> Questo comportamento attualmente si applica solo al pacchetto di aggiornamento del sistema operativo. Tale pacchetto è il solo il contenuto per il quale si specifica la lingua o l'architettura corrispondente. Se ad esempio la sequenza di attività fa riferimento anche a più pacchetti driver, il client attualmente li scarica tutti. Il motore della sequenza di attività valuta le condizioni per i passaggi quando la sequenza di attività viene eseguita, non prima. Il client usa i tag nelle proprietà del pacchetto per determinare per quale contenuto eseguire la funzione pre-cache.


### <a name="to-configure-the-pre-cache-feature"></a>Per configurare la funzionalità di pre-cache

1. Creare pacchetti di aggiornamento del sistema operativo per lingue e architetture specifiche. Specificare l'architettura e della lingua nella scheda **Origine dati** del pacchetto. Per la lingua, usare la conversione decimale. Ad esempio, **1033** è il valore decimale per l'inglese e **0x0409** è il corrispondente valore esadecimale.  

    Il client valuta i valori dell'architettura e della lingua per determinare quale pacchetto di aggiornamento del sistema operativo scaricare durante la pre-memorizzazione nella cache.  

2. Creare una sequenza di attività con passaggi condizionali per le diverse lingue e le diverse architetture. Ad esempio, il passaggio seguente usa la versione in lingua inglese:  

    ![Editor delle sequenze di attività in cui sono visualizzati più passaggi di aggiornamento del sistema operativo per ENU, DEU e JPN](../media/precacheproperties2.png)

    ![Editor delle sequenze di attività, scheda Opzioni, in cui è visualizzata la query WQL WMI per Locale e OSArchitecture](../media/precacheoptions2.png)  

3. Distribuire la sequenza di attività. Per la funzionalità di pre-cache configurare le impostazioni seguenti:  

    - Nella scheda **Generale** selezionare **Pre-download del contenuto per questa sequenza di attività**.  

    - Nella scheda **Impostazioni di distribuzione** configurare la sequenza di attività selezionando **Disponibile**.  

    - Nella scheda **Pianificazione** scegliere l'ora attualmente selezionata per l'impostazione **Pianifica quando questa distribuzione diventerà disponibile**. Il client avvia la funzionalità di pre-cache del contenuto nell'orario disponibile della distribuzione. Quando un client di destinazione riceve questo criterio, l'orario disponibile cade nel passato, quindi il download di pre-cache inizia immediatamente. Se il client riceve questo criterio ma l'orario disponibile è nel futuro, il client non avvia la funzionalità di pre-cache del contenuto fino all'orario disponibile.  

    - Nella scheda **Punti di distribuzione** configurare le impostazioni **Opzioni di distribuzione**. Se non viene eseguita la funzione pre-cache prima che l'utente avvii l'installazione, il client usa queste impostazioni.  
  

### <a name="user-experience"></a>Esperienza utente

- Quando il client riceve i criteri di distribuzione, avvia la funzionalità pre-cache del contenuto dopo l'orario disponibile della distribuzione. Questo contenuto include tutti i pacchetti a cui si fa riferimento, ma solo il pacchetto di aggiornamento del sistema operativo che corrisponde agli attributi di architettura e lingua del pacchetto.  

- Quando il cliente rende disponibile la distribuzione agli utenti, una notifica informa gli utenti della nuova distribuzione e la sequenza di attività diventa visibile in Software Center. Per avviare l'installazione l'utente può passare a Software Center e fare clic su **Installa**.  

- Se la funzionalità di pre-cache del contenuto non è stata completamente eseguita quando l'utente installa la sequenza di attività, il client usa le impostazioni specificate nella scheda **Opzione di distribuzione** della distribuzione.  



## <a name="recommended-task-sequence-steps-to-prepare-for-upgrade"></a>Passaggi della sequenza di attività consigliati per la preparazione dell'aggiornamento

A partire dalla versione 1802, il modello di sequenza di attività predefinito per l'aggiornamento sul posto di Windows 10 include gruppi aggiuntivi con azioni consigliate da aggiungere prima del processo di aggiornamento. Queste azioni nel gruppo **Preparazione dell'aggiornamento** sono comuni tra numerosi clienti che stanno aggiornando i propri dispositivi a Windows 10. Per i siti con versioni precedenti alla 1802, aggiungere manualmente queste azioni alla sequenza di attività nel gruppo **Preparazione dell'aggiornamento**.  

- **Verifiche della batteria**: aggiungere in questo gruppo i passaggi da eseguire per verificare se il computer usa la batteria o l'elettricità. Per eseguire questo controllo serve un'utilità o uno script personalizzato.  

- **Verifiche della connessione di rete/via cavo**: aggiungere in questo gruppo i passaggi da eseguire per verificare se il computer è connesso a una rete e non usa una connessione wireless. Per eseguire questo controllo serve un'utilità o uno script personalizzato.  

- **Rimuovi le applicazioni non compatibili**: aggiungere in questo gruppo i passaggi da eseguire per rimuovere le applicazioni che non sono compatibili con questa versione di Windows 10. Il metodo per disinstallare un'applicazione varia a seconda dei casi.  

    - Se l'applicazione usa Windows Installer, copiare la riga di comando **Disinstalla programma** dalla scheda **Programmi** nelle proprietà del tipo di distribuzione di Windows Installer dell'applicazione. Quindi aggiungere un passaggio **Esegui riga di comando** in questo gruppo con la riga di comando Disinstalla programma. Ad esempio: </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br>  

- **Rimuovi i driver non compatibili**: aggiungere in questo gruppo i passaggi da eseguire per rimuovere i driver che non sono compatibili con questa versione di Windows 10.  

- **Rimuovi/Sospendi la sicurezza di terze parti**: aggiungere in questo gruppo i passaggi da eseguire per rimuovere o sospendere le applicazioni di sicurezza di terze parti, come i programmi antivirus.  

   - Se si usa un programma di crittografia dischi di terze parti, fornire il relativo driver di crittografia al programma di installazione di Windows con l'[opzione della riga di comando](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#23) `/ReflectDrivers`. Aggiungere un passaggio [Imposta variabile della sequenza di attività](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) alla sequenza di attività in questo gruppo. Impostare la variabile della sequenza di attività su **OSDSetupAdditionalUpgradeOptions**. Impostare il valore su `/ReflectDrivers` con il percorso del driver. Questa [variabile della sequenza di attività](/sccm/osd/understand/task-sequence-variables#OSDSetupAdditionalUpgradeOptions) accoda la riga di comando di Installazione di Windows usata dalla sequenza di attività. Per ulteriori indicazioni su questo processo, contattare il fornitore del software in uso.  


### <a name="download-package-content-task-sequence-step"></a>Passaggio della sequenza di attività Scaricare il contenuto del pacchetto  

Usare il passaggio [Scaricare il contenuto del pacchetto](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent) prima del passaggio **Aggiorna sistema operativo** negli scenari seguenti:  

-   Si usa una singola sequenza di attività di aggiornamento per le piattaforme x86 e x64. Includere due passaggi **Scarica contenuto pacchetto** nel gruppo **Preparazione dell'aggiornamento**. Impostare le condizioni in ogni passaggio per rilevare l'architettura client. Questa condizione fa in modo che il passaggio scarichi solo il pacchetto di aggiornamento del sistema operativo appropriato. Configurare ogni passaggio **Scarica contenuto pacchetto** in modo da usare la stessa variabile e usare la variabile per il percorso del supporto durante il passaggio **Aggiorna sistema operativo** .  

-   Per scaricare in modo dinamico un pacchetto di driver applicabile, usare due passaggi **Scarica contenuto pacchetto** con le condizioni per rilevare il tipo di hardware appropriato per ogni pacchetto driver. Configurare ogni passaggio **Scarica contenuto pacchetto** in modo che usi la stessa variabile. Quindi usare tale variabile per il valore **Contenuto preconfigurato** nella sezione dei driver del passaggio **Aggiorna sistema operativo**.  

    > [!NOTE]  
    > Quando sono presenti più pacchetti, Configuration Manager aggiunge un suffisso numerico al nome della variabile. Ad esempio, se si specifica `%mycontent%` come variabile personalizzata, il client archivia tutto il contenuto a cui si fa riferimento in questo percorso. Quando si fa riferimento alla variabile in un passaggio successivo, ad esempio **Aggiorna sistema operativo**, usare la variabile con un suffisso numerico. In questo esempio, `%mycontent01%` o `%mycontent02%`, dove il numero corrisponde all'ordine in cui il passaggio **Scarica contenuto pacchetto** indica il contenuto specifico.  



## <a name="recommended-task-sequence-steps-for-post-processing"></a>Passaggi della sequenza di attività consigliati per la post-elaborazione   

Dopo aver creato la sequenza di attività, aggiungere questi passaggi nel gruppo **Post-elaborazione** della sequenza di attività stessa.  

> [!NOTE]  
>  Questa sequenza di attività non è lineare. I passaggi sono soggetti a condizioni che possono influire sui risultati della sequenza di attività. Questo comportamento varia a seconda che l'aggiornamento del sistema operativo del computer client venga completato o che venga eseguito il rollback del computer client al sistema operativo originale.  

A partire dalla versione 1802, il modello di sequenza di attività predefinito per l'aggiornamento sul posto di Windows 10 include gruppi aggiuntivi con azioni consigliate da aggiungere dopo il processo di aggiornamento. Queste azioni nel gruppo **Post-elaborazione** sono comuni tra numerosi clienti che stanno aggiornando i propri dispositivi a Windows 10. Per i siti con versioni precedenti alla 1802, aggiungere manualmente queste azioni alla sequenza di attività nel gruppo **Post-elaborazione**.  

- **Applica driver basati su installazione**: aggiungere in questo gruppo i passaggi da eseguire per installare driver basati su installazione (con estensione exe) dai pacchetti.  

- **Installa/Abilita la sicurezza di terze parti**: aggiungere in questo gruppo i passaggi da eseguire per installare o abilitare le applicazioni di sicurezza di terze parti, come i programmi antivirus.  

- **Imposta le app predefinite e le associazioni di Windows**: aggiungere in questo gruppo i passaggi da eseguire per impostare le app predefinite e le associazioni di file di Windows. Preparare prima un computer di riferimento con le associazioni di app desiderate. Quindi eseguire l'esportazione tramite la riga di comando seguente: </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>Aggiungere il file XML a un pacchetto. Quindi aggiungere un passaggio [Esegui riga di comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) in questo gruppo. Specificare il pacchetto che contiene il file XML, quindi specificare la riga di comando seguente: </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> Per altre informazioni, vedere [Export or import default application associations](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations) (Esportare o importare associazioni di applicazioni predefinite).  

- **Applica personalizzazioni**: aggiungere in questo gruppo i passaggi da eseguire per applicare le personalizzazioni del menu Start, organizzando ad esempio gruppi di programmi. Per altre informazioni, vedere [Customize the Start screen](/windows-hardware/manufacture/desktop/customize-the-start-screen) (Personalizzare la schermata iniziale).  



## <a name="optional-task-sequence-steps-for-rollback"></a>Passaggi facoltativi della sequenza di attività per il rollback  

Quando si verificano problemi nel processo di aggiornamento dopo il riavvio del computer, l'installazione di Windows esegue il rollback del sistema ripristinando il sistema operativo precedente. La sequenza di attività continua quindi con i passaggi del gruppo **Rollback**. Dopo aver creato la sequenza di attività, aggiungere i passaggi facoltativi in questo gruppo, se necessario. È ad esempio possibile annullare eventuali modifiche apportate al sistema nel gruppo Preparazione dell'aggiornamento, ad esempio la disinstallazione di software non compatibile.



## <a name="recommended-task-sequence-steps-on-failure"></a>Passaggi della sequenza di attività consigliati in caso di errore
<!--1358500-->

A partire dalla versione 1806, il modello di sequenza di attività predefinito per l'aggiornamento sul posto di Windows 10 include un gruppo per **eseguire le azioni in caso di errore**. Questo gruppo include le azioni consigliate da aggiungere nel caso in cui il processo di aggiornamento ha esito negativo. Queste azioni facilitano la risoluzione dei problemi.

- **Raccogli registri**: per raccogliere i log dal client, aggiungere passaggi in questo gruppo.  

    - Una pratica comune prevede la copia dei file di log in una condivisione di rete. Per stabilire questa connessione, usare il passaggio [Connetti alla cartella di rete](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder).  

    - Per eseguire l'operazione di copia, usare un'utilità o uno script personalizzato con il passaggio [Esegui riga di comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) oppure [Esegui script PowerShell](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript).  

    - I file da raccogliere potrebbero includere i log seguenti:  
         `%_SMSTSLogPath%\*.log`   
         `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  

    - Per altre informazioni su setupact.log e altri log di Installazione di Windows, vedere [Windows Setup Log files](https://docs.microsoft.com/windows/deployment/upgrade/log-files) (File di log di Installazione di Windows).  

    - Per altre informazioni sui log client di Configuration Manager, vedere [Log client di Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#BKMK_ClientLogs).  

    - Per altre informazioni su **_SMSTSLogPath** e altre variabili utili, vedere [Variabili della sequenza di attività](/sccm/osd/understand/task-sequence-variables).  

- **Esegui gli strumenti di diagnostica**: per eseguire strumenti di diagnostica aggiuntivi, aggiungere passaggi in questo gruppo. Automatizzare questi strumenti per la raccolta di informazioni aggiuntive dal sistema subito dopo l'errore.  

    - Uno di questi strumenti è [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag) di Windows. È uno strumento di diagnostica autonomo per ottenere i dettagli sui motivi per cui un aggiornamento a Windows 10 non è riuscito.  

        - In Configuration Manager [creare un pacchetto](/sccm/apps/deploy-use/packages-and-programs#create-a-package-and-program) per lo strumento.  

        - Aggiungere un passaggio [Esegui riga di comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) a questo gruppo della sequenza di attività. Usare l'opzione **Pacchetto** per fare riferimento allo strumento. La stringa seguente è un esempio di **Riga di comando**:  
             `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`  



## <a name="additional-recommendations"></a>Suggerimenti aggiuntivi

- Vedere l'articolo [Risolvere gli errori di aggiornamento di Windows 10](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors) nella documentazione di Windows. Questo articolo include anche informazioni dettagliate sul processo di aggiornamento.  

- Nel passaggio predefinito **Verifica conformità** abilitare **Verifica lo spazio minimo disponibile su disco (MB)**. Impostare il valore su almeno **16384** (16 GB) per un pacchetto di aggiornamento del sistema operativo a 32 bit o su **20480** (20 GB) per un pacchetto a 64 bit.  

- Usare la [variabile della sequenza di attività](/sccm/osd/understand/task-sequence-variables#SMSTSDownloadRetryCount) **SMSTSDownloadRetryCount** per riprovare a scaricare i criteri. Per impostazione predefinita, attualmente il client esegue due tentativi; questa variabile è impostata su due (2). Se i client non sono su una connessione di rete Intranet cablata, ulteriori tentativi possono aiutare a ottenere i criteri per tali client. L'uso di questa variabile non ha effetti collaterali negativi, se non un errore ritardato nel caso in cui il download dei criteri non riesca.<!--501016--> Aumentare inoltre il valore della variabile **SMSTSDownloadRetryDelay** dai 15 secondi predefiniti.  

- Eseguire una valutazione della compatibilità inline:  

   - Aggiungere un secondo passaggio **Aggiorna sistema operativo** nel gruppo **Preparazione dell'aggiornamento**. Assegnargli in nome *Valutazione aggiornamento*. Specificare lo stesso pacchetto di aggiornamento e quindi abilitare l'opzione **Esegui analisi compatibilità Installazione di Windows senza avviare l’aggiornamento**. Abilitare **Continua in caso di errore** nella scheda Opzioni.  

   - Subito dopo questo passaggio *Valutazione aggiornamento* aggiungere un passaggio **Esegui riga di comando**. Specificare la riga di comando seguente:</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>Nella scheda **Opzioni** aggiungere la condizione seguente: </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Questo codice restituito è l'equivalente in formato decimale di MOSETUP_E_COMPAT_SCANONLY (0xC1900210), che indica una valutazione della compatibilità riuscita senza problemi. Se il passaggio *Valutazione aggiornamento* riesce e restituisce questo codice, la sequenza di attività ignora questo passaggio. Se invece il passaggio di valutazione restituisce qualsiasi altro codice, questo passaggio esegue con errori la sequenza di attività con il codice restituito dall'analisi di compatibilità di Installazione di Windows. Per altre informazioni su **_SMSTSOSUpgradeActionReturnCode**, vedere [Variabili della sequenza di attività](/sccm/osd/understand/task-sequence-variables#SMSTSOSUpgradeActionReturnCode).  

   - Per altre informazioni, vedere [Aggiorna sistema operativo](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS).  

- Se si vuole modificare il dispositivo da BIOS a UEFI durante questa sequenza di attività, vedere [Conversione da BIOS a UEFI durante un aggiornamento sul posto](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).  

- Se si usa la crittografia dischi BitLocker, per impostazione predefinita il programma di installazione di Windows la sospenderà automaticamente durante l'aggiornamento. A partire da Windows 10 versione 1803, il programma di installazione di Windows include il parametro della riga di comando `/BitLocker` per controllare questo comportamento. Se i requisiti di sicurezza richiedono di mantenere sempre attiva la crittografia dischi, usare la [variabile della sequenza di attività](/sccm/osd/understand/task-sequence-variables#OSDSetupAdditionalUpgradeOptions) **OSDSetupAdditionalUpgradeOptions** nel gruppo **Preparazione dell'aggiornamento** per includere `/BitLocker TryKeepActive`. Per altre informazioni, vedere [Opzioni della riga di comando di Installazione di Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#33).<!--SCCMDocs issue #494-->  

- Alcuni clienti rimuovono le app predefinite di cui è stato effettuato il provisioning in Windows 10. Ad esempio, l'app Bing Meteo o Microsoft Solitaire Collection. In alcune situazioni, queste app ritornano dopo l'aggiornamento di Windows 10. Per altre informazioni, vedere l'articolo su [come mantenere le app rimosse da Windows 10](https://docs.microsoft.com/windows/application-management/remove-provisioned-apps-during-update). Aggiungere il passaggio **Esegui riga di comando** alla sequenza di attività nel gruppo **Preparazione dell'aggiornamento**. Specificare una riga di comando simile a quella dell'esempio seguente:</br> `cmd /c reg delete "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Deprovisioned\Microsoft.BingWeather_8wekyb3d8bbwe" /f` <!--SCCMDocs issue #526-->  

---
title: Creare una sequenza di attività per aggiornare un sistema operativo
titleSuffix: Configuration Manager
description: Usare una sequenza di attività per eseguire automaticamente l'aggiornamento da Windows 7 o versioni successive a Windows 10
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: 12
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 91d3bf5b1488eb7eac52c7426e4bdeeb92ff43b8
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2018
---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>Creare una sequenza di attività per aggiornare un sistema operativo in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare le sequenze di attività in Configuration Manager per aggiornare automaticamente un sistema operativo in un computer di destinazione. L'aggiornamento può essere eseguito da Windows 7 o versione successiva fino a Windows 10 o da Windows Server 2012 o versione successiva fino a Windows Server 2016. Creare una sequenza di attività che faccia riferimento al pacchetto di aggiornamento del sistema operativo e a eventuali altri contenuti da installare, ad esempio applicazioni o aggiornamenti software. La sequenza di attività per aggiornare un sistema operativo fa parte dello scenario [Aggiornare Windows alla versione più recente](upgrade-windows-to-the-latest-version.md).  



##  <a name="BKMK_UpgradeOS"></a> Creare una sequenza di attività per aggiornare un sistema operativo  
 Per aggiornare il sistema operativo nei computer, è possibile creare una sequenza di attività e selezionare **Aggiorna sistema operativo dal pacchetto di aggiornamento** nella Creazione guidata della sequenza di attività. La procedura guidata aggiunge i passaggi della sequenza di attività per aggiornare il sistema operativo, applicare gli aggiornamenti software e installare le applicazioni. Prima di creare la sequenza di attività, devono essere soddisfatti i requisiti seguenti:    

-   **Richiesto**  

     - Il [pacchetto di aggiornamento del sistema operativo](../get-started/manage-operating-system-upgrade-packages.md) deve essere disponibile nella console di Configuration Manager.
     - Quando si esegue l'aggiornamento a Windows Server 2016, selezionare l'impostazione **Ignore any dismissable compatibility messages** (Ignora eventuali messaggi di compatibilità che possono essere chiusi) nel passaggio della sequenza di attività Aggiorna sistema operativo. In caso contrario, l'aggiornamento ha esito negativo.

-   **Obbligatorio (se usato)**  

    -   Gli [aggiornamenti software](../../sum/get-started/synchronize-software-updates.md) devono essere sincronizzati nella console di Configuration Manager.  

    -   Le [applicazioni](../../apps/deploy-use/create-applications.md) devono essere aggiunte alla console di Configuration Manager.  

#### <a name="to-create-a-task-sequence-that-upgrades-an-operating-system"></a>Per creare una sequenza di attività che esegua l'aggiornamento di un sistema operativo  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea sequenza di attività** per avviare la Creazione guidata della sequenza di attività.  

4.  Nella pagina **Crea una nuova sequenza di attività** fare clic su **Aggiorna sistema operativo dal pacchetto di aggiornamento**e quindi fare clic su **Avanti**.  

5.  Nella pagina **Informazioni sequenza di attività** specificare le impostazioni seguenti e quindi fare clic su **Avanti**.  

    -   **Nome sequenza di attività**: specificare un nome che identifica la sequenza di attività.  

    -   **Descrizione**: specificare una descrizione dell'attività eseguita dalla sequenza di attività.  

6.  Nella pagina **Aggiorna il sistema operativo Windows** specificare le impostazioni seguenti e quindi fare clic su **Avanti**.  

    -   **Pacchetto di aggiornamento**: specificare il pacchetto di aggiornamento che contiene i file di origine per l'aggiornamento del sistema operativo. È possibile verificare di avere selezionato il pacchetto di aggiornamento corretto esaminando le informazioni nel riquadro **Proprietà** . Per altre informazioni, vedere [Gestire i pacchetti di aggiornamento del sistema operativo](../get-started/manage-operating-system-upgrade-packages.md).  

    -   **Indice edizione**: se sono presenti più indici edizione del sistema operativo nel pacchetto, selezionare l'indice edizione desiderato. Per impostazione predefinita, viene selezionato il primo elemento.  

    -   **Codice Product Key**: specificare il codice Product Key per il sistema operativo Windows da installare. È possibile specificare i codici Product Key per contratti multilicenza codificati e i codici Product Key standard. Se si usa un codice Product Key non codificato, ogni gruppo di cinque caratteri deve essere separato da un trattino (-). Ad esempio: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX* Se l'aggiornamento è per un'edizione per contratti multilicenza, il codice Product Key non è obbligatorio. Il codice Product Key è necessario solo quando l'aggiornamento è per un'edizione di Windows al dettaglio.  

    -   **Ignore any dismissable compatibility messages** (Ignora eventuali messaggi di compatibilità che possono essere chiusi): selezionare questa impostazione se si esegue l'aggiornamento a Windows Server 2016. Se non si seleziona questa impostazione, la sequenza di attività non può essere completata perché il programma di installazione di Windows rimane in attesa che l'utente faccia clic su **Conferma** in una finestra di dialogo di compatibilità delle app di Windows.   

7.  Nella pagina **Includi aggiornamenti** specificare se installare gli aggiornamenti software obbligatori, tutti gli aggiornamenti software o nessuno. Fare quindi clic su **Avanti**. Se si sceglie di installare gli aggiornamenti software, Configuration Manager installa solo quelli assegnati alle raccolte di cui il computer di destinazione è membro.  

8.  Nella pagina **Installa applicazioni** specificare le applicazioni da installare nel computer di destinazione e quindi fare clic su **Avanti**. Se si specificano più applicazioni, è possibile specificare che la sequenza di attività continui anche se l'installazione di un'applicazione specifica non riesce.  

9. Completare la procedura guidata.  


 > [!Important] 
 > Quando la sequenza di attività è completata, il client non rimuove gli script di post-elaborazione e rollback fino a quando non viene riavviato il computer. Questi file di script non contengono informazioni riservate.  


 > [!Note]
 > A partire dalla versione 1802, il modello di sequenza di attività predefinito per l'aggiornamento sul posto di Windows 10 include gruppi aggiuntivi con azioni consigliate da aggiungere prima e dopo il processo di aggiornamento. Queste azioni sono comuni tra numerosi clienti che stanno aggiornando i propri dispositivi a Windows 10. Per altre informazioni, vedere i passaggi della sequenza di attività consigliata [per preparare l'aggiornamento](#recommended-task-sequence-steps-to-prepare-for-upgrade) e [ post-elaborazione](#recommended-task-sequence-steps-for-post-processing).



## <a name="configure-pre-cache-content"></a>Configurare la pre-cache del contenuto
La funzionalità pre-cache per le distribuzioni di sequenze di attività disponibili consente ai client di scaricare il contenuto pertinente dei pacchetti di aggiornamento del sistema operativo prima che un utente installi la sequenza di attività.
> [!TIP]  
> Questa funzionalità è stata introdotta per la prima volta nella versione 1702 come [funzionalità in versione non definitiva](/sccm/core/servers/manage/pre-release-features). A partire dalla versione 1706, questa funzionalità non è più una funzionalità di versione non definitiva.

Si supponga, ad esempio, di volere una sola sequenza di attività di aggiornamento sul posto per tutti gli utenti, pur avendo molte architetture e lingue diverse. Nelle versioni precedenti il download del contenuto inizia quando l'utente installa una distribuzione di sequenze di attività disponibile da Software Center. Questo ritardo aggiunge ulteriore tempo prima che l'installazione sia pronta per essere avviata. Tutto il contenuto a cui viene fatto riferimento nella sequenza di attività viene scaricato. Questo contenuto include il pacchetto di aggiornamento del sistema operativo per tutte le lingue e tutte le architetture. Se ogni pacchetto di aggiornamento è circa tre GB, il contenuto totale è molto elevato.

Con la funzionalità pre-cache del contenuto è possibile consentire al client di scaricare solo il pacchetto di aggiornamento applicabile per il sistema operativo, nonché tutto il contenuto aggiuntivo a cui si fa riferimento, non appena riceve la distribuzione. Quando l'utente fa clic su **Installa** in Software Center, il contenuto è pronto e l'installazione inizia rapidamente, dato che il contenuto si trova nel disco rigido locale.

 > [!NOTE]
 > Questo comportamento attualmente si applica solo al pacchetto di aggiornamento del sistema operativo. Tale pacchetto è il solo il contenuto per il quale si specifica la lingua o l'architettura corrispondente. Se ad esempio la sequenza di attività fa riferimento anche a più pacchetti driver, il client attualmente li scarica tutti. Il motore della sequenza di attività valuta le condizioni per i passaggi quando la sequenza di attività viene eseguita, non prima. Il client usa i tag nelle proprietà del pacchetto per determinare per quale contenuto eseguire la funzione pre-cache.

### <a name="to-configure-the-pre-cache-feature"></a>Per configurare la funzionalità di pre-cache

1. Creare pacchetti di aggiornamento del sistema operativo per lingue e architetture specifiche. Specificare l'architettura e della lingua nella scheda **Origine dati** del pacchetto. Per la lingua, usare la conversione decimale. Ad esempio, 1033 è il valore decimale per l'inglese e 0x0409 è il corrispondente valore esadecimale.

    Il client valuta i valori dell'architettura e della lingua per determinare quale pacchetto di aggiornamento del sistema operativo scaricare durante la pre-memorizzazione nella cache.

1. Creare una sequenza di attività con passaggi condizionali per le diverse lingue e le diverse architetture. Ad esempio, il passaggio seguente usa la versione in lingua inglese:

    ![Editor delle sequenze di attività in cui sono visualizzati più passaggi di aggiornamento del sistema operativo per ENU, DEU e JPN](../media/precacheproperties2.png)

    ![Editor delle sequenze di attività, scheda Opzioni, in cui è visualizzata la query WQL WMI per Locale e OSArchitecture](../media/precacheoptions2.png)  

3. Distribuire la sequenza di attività. Per la funzionalità di pre-cache configurare le impostazioni seguenti:
    - Nella scheda **Generale** selezionare **Pre-download del contenuto per questa sequenza di attività**.
    - Nella scheda **Impostazioni di distribuzione** configurare la sequenza di attività selezionando **Disponibile** per **Scopo**.
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
- **Rimuovi le applicazioni non compatibili**: aggiungere in questo gruppo i passaggi da eseguire per rimuovere le applicazioni che non sono compatibili con questa versione di Windows 10. Il metodo per disinstallare un'applicazione varia a seconda dei casi. Se l'applicazione usa Windows Installer, copiare la riga di comando **Disinstalla programma** dalla scheda **Programmi** nelle proprietà del tipo di distribuzione di Windows Installer dell'applicazione. Quindi aggiungere un passaggio **Esegui riga di comando** in questo gruppo con la riga di comando Disinstalla programma. Ad esempio: </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- **Rimuovi i driver non compatibili**: aggiungere in questo gruppo i passaggi da eseguire per rimuovere i driver che non sono compatibili con questa versione di Windows 10.
- **Rimuovi/Sospendi la sicurezza di terze parti**: aggiungere in questo gruppo i passaggi da eseguire per rimuovere o sospendere le applicazioni di sicurezza di terze parti, come i programmi antivirus.
   - Se si usa un programma di crittografia dischi di terze parti, fornire il relativo driver di crittografia al programma di Installazione di Windows con l'[opzione della riga di comando](/windows-hardware/manufacture/desktop/windows-setup-command-line-options) **/ReflectDrivers**. Aggiungere un passaggio [Imposta variabile della sequenza di attività](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) alla sequenza di attività in questo gruppo. Impostare la variabile della sequenza di attività su **OSDSetupAdditionalUpgradeOptions**. Impostare il valore su **/ReflectDriver** con il percorso del driver. Questa [variabile di azione della sequenza di attività](/sccm/osd/understand/task-sequence-action-variables#upgrade-operating-system) accoda la riga di comando del programma di installazione di Windows usata dalla sequenza di attività. Per ulteriori indicazioni su questo processo, contattare il fornitore del software in uso.

### <a name="download-package-content-task-sequence-step"></a>Passaggio della sequenza di attività Scaricare il contenuto del pacchetto  
 Il passaggio [Scaricare il contenuto del pacchetto](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) può essere usato prima del passaggio **Aggiorna sistema operativo** negli scenari seguenti:  

-   Si usa una singola sequenza di attività di aggiornamento per le piattaforme x86 e x64. Includere due passaggi **Scarica contenuto pacchetto** nel gruppo **Preparazione dell'aggiornamento**. Impostare le condizioni in ogni passaggio per rilevare l'architettura client. Questa condizione fa in modo che il passaggio scarichi solo il pacchetto di aggiornamento del sistema operativo appropriato. Configurare ogni passaggio **Scarica contenuto pacchetto** in modo da usare la stessa variabile e usare la variabile per il percorso del supporto durante il passaggio **Aggiorna sistema operativo** .  

-   Per scaricare in modo dinamico un pacchetto di driver applicabile, usare due passaggi **Scarica contenuto pacchetto** con le condizioni per rilevare il tipo di hardware appropriato per ogni pacchetto driver. Configurare ogni passaggio **Scarica contenuto pacchetto** in modo che usi la stessa variabile. Quindi usare tale variabile per il valore **Contenuto preconfigurato** nella sezione dei driver del passaggio **Aggiorna sistema operativo**.  

   > [!NOTE]
   > Quando sono presenti più pacchetti, Configuration Manager aggiunge un suffisso numerico al nome della variabile. Ad esempio, se si specifica una variabile di %mycontent% come variabile personalizzata, il percorso è dove il client archivia tutto il contenuto a cui si fa riferimento. Quando si fa riferimento alla variabile in un passaggio successivo, ad esempio **Aggiorna sistema operativo**, usare la variabile con un suffisso numerico. In questo esempio, %mycontent01% o %mycontent02% , dove il numero corrisponde all'ordine in cui il passaggio **Scarica contenuto pacchetto** indica il contenuto specifico.



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
 Quando si verificano problemi nel processo di aggiornamento dopo il riavvio del computer, l'installazione di Windows esegue il rollback dell'aggiornamento al sistema operativo precedente. La sequenza di attività continua quindi con i passaggi del gruppo **Rollback**. Dopo aver creato la sequenza di attività, è possibile aggiungere passaggi facoltativi nel gruppo Rollback. È ad esempio possibile annullare eventuali modifiche apportate al sistema nel gruppo Preparazione dell'aggiornamento, ad esempio la disinstallazione di software non compatibile.



## <a name="additional-recommendations"></a>Suggerimenti aggiuntivi
- Vedere l'articolo [Risolvere gli errori di aggiornamento di Windows 10](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors) nella documentazione di Windows. Questo articolo include anche informazioni dettagliate sul processo di aggiornamento.
- Nel passaggio predefinito **Verifica conformità** abilitare **Verifica lo spazio minimo disponibile su disco (MB)**. Impostare il valore su almeno **16384** (16 GB) per un pacchetto di aggiornamento del sistema operativo a 32 bit o su **20480** (20 GB) per un pacchetto a 64 bit. 
- Usare la [variabile di sequenza di attività predefinita](/sccm/osd/understand/task-sequence-built-in-variables) **SMSTSDownloadRetryCount** per riprovare a scaricare i criteri. Per impostazione predefinita, attualmente il client esegue due tentativi; questa variabile è impostata su due (2). Se i client non sono su una connessione di rete aziendale cablata, ulteriori tentativi possono aiutare a ottenere i criteri per tali client. L'uso di questa variabile non ha effetti collaterali negativi, se non un errore ritardato in caso il download dei criteri non riesca.<!-- 501016 --> Aumentare inoltre il valore della variabile **SMSTSDownloadRetryDelay** dai 15 secondi predefiniti.
- Eseguire una valutazione della compatibilità inline. 
   - Aggiungere un secondo passaggio **Aggiorna sistema operativo** nel gruppo **Preparazione dell'aggiornamento**. Assegnargli in nome *Valutazione aggiornamento*. Specificare lo stesso pacchetto di aggiornamento e quindi abilitare l'opzione **Esegui analisi compatibilità Installazione di Windows senza avviare l’aggiornamento**. Abilitare **Continua in caso di errore** nella scheda Opzioni. 
   - Subito dopo questo passaggio *Valutazione aggiornamento* aggiungere un passaggio **Esegui riga di comando**. Specificare la riga di comando seguente:</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>Nella scheda **Opzioni** aggiungere la condizione seguente: </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Questo codice restituito è l'equivalente in formato decimale di MOSETUP_E_COMPAT_SCANONLY (0xC1900210), che indica una valutazione della compatibilità riuscita senza problemi. Se il passaggio *Valutazione aggiornamento* riesce e restituisce questo codice, questo passaggio non viene eseguito. Se invece il passaggio di valutazione restituisce qualsiasi altro codice, questo passaggio esegue con errori la sequenza di attività con il codice restituito dall'analisi di compatibilità di Installazione di Windows.
   - Per altre informazioni, vedere [Aggiorna sistema operativo](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS).
- Se si vuole modificare il dispositivo da BIOS a UEFI durante questa sequenza di attività, vedere [Conversione da BIOS a UEFI durante un aggiornamento sul posto](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

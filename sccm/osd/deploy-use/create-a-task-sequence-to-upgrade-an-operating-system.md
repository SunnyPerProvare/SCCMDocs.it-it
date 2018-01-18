---
title: "Creare una sequenza di attività per aggiornare un sistema operativo"
titleSuffix: Configuration Manager
description: "Usare le sequenze di attività in System Center Configuration Manager per aggiornare automaticamente un sistema operativo da Windows 7 o versione successiva a Windows 10."
ms.custom: na
ms.date: 12/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
caps.latest.revision: "12"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 058b0710484a0452ddf19655bf2cabbb43f624ad
ms.sourcegitcommit: 92c3f916e6bbd35b6208463ff406e0247664543a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/02/2018
---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>Creare una sequenza di attività per aggiornare un sistema operativo in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare le sequenze di attività in Configuration Manager per aggiornare automaticamente un sistema operativo in un computer di destinazione. L'aggiornamento può essere eseguito da Windows 7 o versione successiva fino a Windows 10 o da Windows Server 2012 o versione successiva fino a Windows Server 2016. Si crea una sequenza di attività che fa riferimento al pacchetto di aggiornamento del sistema operativo e a eventuali altri contenuti da installare, ad esempio applicazioni o aggiornamenti del software. La sequenza di attività per aggiornare un sistema operativo fa parte dello scenario [Aggiornare Windows alla versione più recente](upgrade-windows-to-the-latest-version.md).  

##  <a name="BKMK_UpgradeOS"></a> Creare una sequenza di attività per aggiornare un sistema operativo  
 Per aggiornare il sistema operativo nei computer, è possibile creare una sequenza di attività e selezionare **Aggiorna sistema operativo dal pacchetto di aggiornamento** nella Creazione guidata della sequenza di attività. La procedura guidata aggiunge i passaggi per aggiornare il sistema operativo, applicare gli aggiornamenti software e installare le applicazioni. Prima di creare la sequenza di attività, devono essere soddisfatti i requisiti seguenti:    

-   **Richiesto**  

     - Il [pacchetto di aggiornamento del sistema operativo](../get-started/manage-operating-system-upgrade-packages.md) deve essere disponibile nella console di Configuration Manager.
     - Quando si esegue l'aggiornamento a Windows Server 2016, selezionare l'impostazione **Ignore any dismissable compatibility messages** (Ignora eventuali messaggi di compatibilità che possono essere chiusi) nel passaggio della sequenza di attività Aggiorna sistema operativo. In caso contrario, l'aggiornamento avrà esito negativo.

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

7.  Nella pagina **Includi aggiornamenti** specificare se installare gli aggiornamenti software necessari, tutti gli aggiornamenti software o nessun aggiornamento software e quindi fare clic su **Avanti**. Se si sceglie di installare gli aggiornamenti software, Configuration Manager installa solo quelli assegnati alle raccolte di cui il computer di destinazione è membro.  

8.  Nella pagina **Installa applicazioni** specificare le applicazioni da installare nel computer di destinazione e quindi fare clic su **Avanti**. Se si specificano più applicazioni, è possibile specificare che la sequenza di attività continui anche se l'installazione di un'applicazione specifica non riesce.  

9. Completare la procedura guidata.  



## <a name="configure-pre-cache-content"></a>Configurare la pre-cache del contenuto
A partire dalla versione 1702, la funzionalità di pre-cache per le distribuzioni di sequenze di attività disponibili consente ai client di scaricare solo il contenuto pertinente prima che un utente installi la sequenza di attività.
> [!TIP]  
> Questa funzionalità è stata introdotta per la prima volta nella versione 1702 come [funzionalità in versione non definitiva](/sccm/core/servers/manage/pre-release-features). A partire dalla versione 1706, questa funzionalità non è più una funzionalità di versione non definitiva.

Si supponga ad esempio di voler distribuire una sequenza di attività di aggiornamento sul posto di Windows 10, di volere una sola sequenza di attività per tutti gli utenti e di avere più architetture e/o lingue. Nelle versioni precedenti il download del contenuto inizia quando l'utente installa una distribuzione di sequenze di attività disponibile da Software Center. Questo ritardo aggiunge ulteriore tempo prima che l'installazione sia pronta per essere avviata. Inoltre, tutto il contenuto a cui viene fatto riferimento nella sequenza di attività viene scaricato. Questo contenuto include il pacchetto di aggiornamento del sistema operativo per tutte le lingue e tutte le architetture. Se ogni pacchetto di aggiornamento è circa tre GB, il contenuto totale è molto elevato.

Con la funzionalità di pre-cache del contenuto è possibile consentire al client di scaricare solo il contenuto applicabile non appena riceve la distribuzione. Pertanto quando l'utente fa clic su **Installa** in Software Center, il contenuto è pronto e l'installazione inizia rapidamente, dato che il contenuto si trova nel disco rigido locale.

### <a name="to-configure-the-pre-cache-feature"></a>Per configurare la funzionalità di pre-cache

1. Creare pacchetti di aggiornamento del sistema operativo per lingue e architetture specifiche. Specificare l'architettura e della lingua nella scheda **Origine dati** del pacchetto. Per la lingua usare la conversione decimale. Ad esempio, 1033 è il valore decimale per l'inglese e 0x0409 è il corrispondente valore esadecimale. Per i dettagli, vedere [Creare una sequenza di attività per aggiornare un sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system).

    I valori di architettura e lingua corrispondono alle condizioni nei passaggi della sequenza di attività per determinare se per il pacchetto di aggiornamento del sistema operativo è stata eseguita la funzionalità di pre-cache.
1. Creare una sequenza di attività con passaggi condizionali per le diverse lingue e le diverse architetture. Ad esempio, il passaggio seguente usa la versione in lingua inglese:

    ![proprietà pre-cache](../media/precacheproperties2.png)

    ![opzioni pre-cache](../media/precacheoptions2.png)  

3. Distribuire la sequenza di attività. Per la funzionalità di pre-cache configurare le impostazioni seguenti:
    - Nella scheda **Generale** selezionare **Pre-download del contenuto per questa sequenza di attività**.
    - Nella scheda **Impostazioni di distribuzione** configurare la sequenza di attività selezionando **Disponibile** per **Scopo**.
    - Nella scheda **Pianificazione** scegliere l'ora attualmente selezionata per l'impostazione **Pianifica quando questa distribuzione diventerà disponibile**. Il client avvia la funzionalità di pre-cache del contenuto nell'orario disponibile della distribuzione. Quando un client di destinazione riceve questo criterio, l'orario disponibile cade nel passato, quindi il download di pre-cache inizia immediatamente. Se il client riceve questo criterio ma l'orario disponibile è nel futuro, il client non avvia la funzionalità di pre-cache del contenuto fino all'orario disponibile. 
    - Nella scheda **Punti di distribuzione** configurare le impostazioni **Opzioni di distribuzione**. Se in un client non è stata eseguita la funzione di pre-cache per il contenuto prima che l'utente avvii l'installazione, vengono usate queste impostazioni.


### <a name="user-experience"></a>Esperienza utente
- Quando il client riceve i criteri di distribuzione, avvia la funzionalità di pre-cache del contenuto dopo l'orario disponibile della distribuzione. Il contenuto include tutti i pacchetti a cui si fa riferimento e solo il pacchetto di aggiornamento del sistema operativo corrispondente al client, in base alle condizioni impostate nella sequenza di attività.
- Quando la distribuzione viene resa disponibile agli utenti, una notifica informa gli utenti della nuova distribuzione e la sequenza di attività diventa visibile in Software Center. Per avviare l'installazione l'utente può passare a Software Center e fare clic su **Installa**.
- Se la funzionalità di pre-cache del contenuto non è stata completamente eseguita quando l'utente installa la sequenza di attività, il client usa le impostazioni specificate nella scheda **Opzione di distribuzione** della distribuzione. 



## <a name="download-package-content-task-sequence-step"></a>Passaggio della sequenza di attività Scaricare il contenuto del pacchetto  
 Il passaggio [Scaricare il contenuto del pacchetto](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) può essere usato prima del passaggio **Aggiorna sistema operativo** negli scenari seguenti:  

-   Si usa una singola sequenza di attività di aggiornamento per le piattaforme x86 e x64. Includere due passaggi **Scarica contenuto pacchetto** nel gruppo **Preparazione dell'aggiornamento**. Impostare le condizioni in ogni passaggio per rilevare l'architettura client. Questa condizione fa in modo che il passaggio scarichi solo il pacchetto di aggiornamento del sistema operativo appropriato. Configurare ogni passaggio **Scarica contenuto pacchetto** in modo da usare la stessa variabile e usare la variabile per il percorso del supporto durante il passaggio **Aggiorna sistema operativo** .  

-   Per scaricare in modo dinamico un pacchetto di driver applicabile, usare due passaggi **Scarica contenuto pacchetto** con le condizioni per rilevare il tipo di hardware appropriato per ogni pacchetto driver. Configurare ogni passaggio **Scarica contenuto pacchetto** in modo che usi la stessa variabile. Quindi usare tale variabile per il valore **Contenuto preconfigurato** nella sezione dei driver del passaggio **Aggiorna sistema operativo**.  

   > [!NOTE]
   > Quando sono presenti più pacchetti, Configuration Manager aggiunge un suffisso numerico al nome della variabile. Ad esempio, se si specifica una variabile di %mycontent% come variabile personalizzata, il percorso è dove il client archivia tutto il contenuto a cui si fa riferimento. Quando si fa riferimento alla variabile in un passaggio successivo, ad esempio **Aggiorna sistema operativo**, usare la variabile con un suffisso numerico. In questo esempio, %mycontent01% o %mycontent02% , dove il numero corrisponde all'ordine in cui il passaggio **Scarica contenuto pacchetto** indica il contenuto specifico.

## <a name="optional-post-processing-task-sequence-steps"></a>Passaggi della sequenza attività di post-elaborazione facoltativi  
 Dopo aver creato la sequenza di attività, aggiungere ulteriori passaggi, se necessario. Ad esempio, per disinstallare le applicazioni con problemi di compatibilità noti o aggiungere azioni post-elaborazione da eseguire dopo il riavvio del computer e il corretto aggiornamento a Windows 10. Aggiungere questi passaggi aggiuntivi nel gruppo Post-elaborazione della sequenza di attività.  

> [!NOTE]  
>  Poiché questa sequenza di attività non è lineare, esistono condizioni sui passaggi che possono influenzare i risultati della sequenza di attività, a seconda che venga aggiornato correttamente il computer client o che sia necessario ripristinare il computer client alla versione del sistema operativo precedente.  

## <a name="optional-rollback-task-sequence-steps"></a>Passaggi della sequenza attività di rollback facoltativi  
 Quando si verificano problemi nel processo di aggiornamento dopo il riavvio del computer, l'installazione di Windows esegue il rollback dell'aggiornamento al sistema operativo precedente. La sequenza di attività continuerà quindi con i passaggi del gruppo Rollback. Dopo aver creato la sequenza di attività, è possibile aggiungere passaggi facoltativi al gruppo Rollback.  

## <a name="folder-and-files-removed-after-computer-restart"></a>Cartelle e file vengono rimossi dopo il riavvio del computer  
 Quando la sequenza di attività è completata, il client non rimuove gli script di post-elaborazione e rollback fino a quando non viene riavviato il computer. Questi file di script non contengono informazioni riservate.  

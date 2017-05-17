---
title: Creare supporti autonomi con System Center Configuration Manager | Microsoft Docs
description: Usare i supporti autonomi per distribuire il sistema operativo in un computer senza connessione a un sito di Configuration Manager o alla rete.
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
caps.latest.revision: 21
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: dab5da5a4b5dfb3606a8a6bd0c70a0b21923fff9
ms.openlocfilehash: d4689545ce2be5c16a65b24489f30028a0f90f94
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017


---
# <a name="create-stand-alone-media-with-system-center-configuration-manager"></a>Creare supporti autonomi con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Il supporto autonomo in Configuration Manager contiene tutto il necessario per distribuire il sistema operativo in un computer senza connettersi a un sito di Configuration Manager o alla rete. Usare il supporto autonomo con gli scenari di distribuzione del sistema operativo seguenti:  

-   [Aggiornare un computer esistente con una nuova versione di Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Installare una nuova versione di Windows in un nuovo computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Aggiornare Windows alla versione più recente](upgrade-windows-to-the-latest-version.md)  

 Il supporto autonomo include la sequenza di attività che consente di automatizzare i passaggi di installazione del sistema operativo e di tutti gli altri contenuti necessari, tra cui immagine d'avvio, immagine del sistema operativo e driver di dispositivo. Poiché tutto il necessario per la distribuzione del sistema operativo è archiviato nel supporto autonomo, lo spazio su disco richiesto per il supporto autonomo è notevolmente superiore allo spazio su disco richiesto per altri tipi di supporti. Quando si creano supporti autonomi in un sito di amministrazione centrale, il client recupererà il relativo codice del sito assegnato da Active Directory. I supporti autonomi creati nei siti figlio assegneranno automaticamente al client il codice del sito per tale sito.  

##  <a name="BKMK_CreateStandAloneMedia"></a> Creare supporti autonomi  
 Prima di creare un supporto autonomo usando la Creazione guidata del supporto per la sequenza attività, assicurarsi che siano soddisfatte le condizioni seguenti:  

### <a name="create-a-task-sequence-to-deploy-an-operating-system"></a>Creare una sequenza di attività per distribuire un sistema operativo
Come parte del supporto autonomo, è necessario specificare la sequenza di attività per distribuire un sistema operativo. Per i passaggi necessari per creare una nuova sequenza di attività, vedere [Creare una sequenza di attività per installare un sistema operativo in System Center Configuration Manager](create-a-task-sequence-to-install-an-operating-system.md).

Per il supporto autonomo non sono supportate le seguenti azioni:
- Passaggio Applica automaticamente i driver nella sequenza di attività. L'applicazione automatica di driver di dispositivo dal catalogo di driver non è supportata, ma è possibile scegliere il passaggio Applica pacchetto di driver per rendere disponibile un set di driver specificato per l'installazione di Windows.
- Passaggio Scarica contenuto pacchetto nella sequenza di attività. Le informazioni relative ai punti di gestione non sono disponibili nel supporto autonomo, pertanto il passaggio avrà esito negativo durante il tentativo di enumerazione dei percorsi del contenuto.
- Istallazione di aggiornamenti software.
- Installazione del software prima della distribuzione del sistema operativo.
- Sequenza di attività per distribuzioni non di sistema operativo.
- Associazione di utenti al computer di destinazione per il supporto dell'affinità utente dispositivo.
- Installazione dinamica dei pacchetti tramite l'attività Installa pacchetti.
- Installazioni dinamiche delle applicazioni tramite l'attività Installa applicazione.

Se la sequenza di attività per la distribuzione di un sistema operativo include il passaggio [Installa pacchetto](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) e si crea il supporto autonomo in un sito di amministrazione centrale, può verificarsi un errore. Il sito di amministrazione centrale non dispone dei criteri di configurazione del client necessari per abilitare l'agente di distribuzione software durante l'esecuzione della sequenza di attività. Nel file CreateTsMedia.log potrebbe essere visualizzato l'errore seguente:<br /><br /> "WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"<br /><br /> Per un supporto autonomo che include il passaggio **Installa pacchetto**, è necessario creare il supporto autonomo in un sito primario in cui l'agente di distribuzione software sia abilitato oppure aggiungere un passaggio [Esegui riga di comando](../understand/task-sequence-steps.md#BKMK_RunCommandLine) dopo il passaggio [Imposta Windows e ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) e prima del primo passaggio **Installa pacchetto** nella sequenza di attività. Il passaggio **Esegui riga di comando** esegue un comando WMIC per abilitare l'agente di distribuzione software prima dell'esecuzione del primo passaggio Installa pacchetto. È possibile usare quanto segue nel passaggio della sequenza di attività **Esegui riga di comando** :<br /><br />
```
WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE
```

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuire tutto il contenuto associato alla sequenza di attività
È necessario distribuire tutto il contenuto richiesto dalla sequenza di attività in almeno un punto di distribuzione. Ciò include l'immagine d'avvio, l'immagine del sistema operativo e altri file associati. La procedura guidata raccoglie le informazioni dal punto di distribuzione quando viene creato il supporto autonomo. È necessario avere i diritti di accesso in **lettura** alla raccolta contenuto per il punto di distribuzione.  Per i dettagli, vedere [Distribuire il contenuto a cui fa riferimento una sequenza attività](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS).

### <a name="prepare-the-removable-usb-drive"></a>Preparare l'unità USB rimovibile
*Per un'unità USB rimovibile:*

Se si usa un'unità USB rimovibile, l'unità deve essere collegata al computer in cui viene eseguita la procedura guidata e rilevabile da Windows come dispositivo rimovibile. La procedura guidata scrive direttamente nell'unità USB durante la creazione del supporto. Supporto autonomo usa un file system FAT32. Non è possibile creare supporti autonomi in un'unità flash USB il cui contenuto include un file di oltre 4 GB.

### <a name="create-an-output-folder"></a>Creare una cartella di output
*Per un set di CD/DVD:*

Prima di eseguire la Creazione guidata del supporto per la sequenza di attività per creare il supporto per un set di CD o DVD, è necessario creare una cartella per i file di output creati dalla procedura guidata. Il supporto creato per un set di CD o DVD viene scritto come file con estensione iso direttamente nella cartella.


 Usare la procedura seguente per creare un supporto autonomo per un'unità USB rimovibile o un set di CD/DVD.  

## <a name="to-create-stand-alone-media"></a>Per creare un supporto autonomo  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea supporto per sequenza di attività** per avviare la Creazione guidata del supporto per la sequenza di attività.  

4.  Nella pagina **Seleziona tipo di supporto** specificare le opzioni seguenti e quindi fare clic su **Avanti**.  

    -   Selezionare **Supporto autonomo**.  

    -   Se si desidera consentire la distribuzione del sistema operativo senza l'interazione dell'utente, selezionare **Consenti distribuzione automatica del sistema operativo**. Quando si seleziona questa opzione, all'utente non verrà chiesto di immettere informazioni sulla configurazione di rete o di scegliere se eseguire sequenze attività facoltative. Tuttavia, all'utente viene richiesta una password se il supporto è configurato per la protezione con password.  

5.  Nella pagina **Tipo di supporto** specificare se il supporto è un'unità flash o un set di CD/DVD, quindi configurare quanto segue:  

    > [!IMPORTANT]  
    >  Supporto autonomo usa un file system FAT32. Non è possibile creare supporti autonomi in un'unità flash USB il cui contenuto include un file di oltre 4 GB.  

    -   Se si seleziona **Unità memoria flash USB**, è necessario specificare l'unità in cui archiviare il contenuto.  

    -   Se si seleziona l'opzione **CD/DVD impostato**, specificare la capacità del supporto e il nome e il percorso dei file di output. La procedura guidata scrive i file di output in questa posizione. Ad esempio: **\\\nomeserver\cartella\filedioutput.iso**  

         Se la capacità del supporto non è sufficiente per archiviare l'intero contenuto, vengono creati più file ed è necessario archiviare il contenuto in più CD o DVD. Quando sono necessari più supporti, Configuration Manager aggiunge un numero di sequenza al nome di ogni file di output creato. Se insieme al sistema operativo si distribuisce un'applicazione e questa non può essere contenuta in un unico supporto, Configuration Manager archivia l'applicazione in più supporti. Quando il supporto autonomo viene eseguito Configuration Manager chiede all'utente il supporto successivo contenente l'applicazione.   

         > [!IMPORTANT]  
         >  Se si seleziona un'immagine iso esistente, la Creazione guidata del supporto per la sequenza di attività elimina l'immagine dall'unità o dalla condivisione non appena si passa alla pagina successiva della procedura guidata. L'immagine esistente viene eliminata, anche se si annulla la procedura guidata.  

     Fare clic su **Avanti**.  

6.  Nella pagina **Sicurezza** scegliere tra le opzioni seguenti e quindi fare clic su **Avanti**:
    - **Proteggi supporto con password**: immettere una password complessa per proteggere il supporto. Se si specifica una password, per usare il supporto sarà necessario immetterla.  

        > [!IMPORTANT]  
        >  Nel supporto autonomo vengono crittografate solo le procedure delle sequenze attività e le relative variabili. Il resto del contenuto del supporto non è crittografato. Pertanto, non includere informazioni riservate negli script della sequenza di attività. Archiviare e implementare tutte le informazioni riservate usando variabili della sequenza di attività.  

    - **Seleziona l'intervallo di date di validità per il supporto autonomo** (disponibile a partire dalla versione 1702): impostare le date facoltative di inizio e scadenza nel supporto. Queste impostazioni sono disabilitate per impostazione predefinita. Le date vengono confrontate con l'ora di sistema nel computer prima che il supporto autonomo venga eseguito. Quando l'ora di sistema è precedente all'ora di inizio o successiva all'ora di scadenza, il supporto autonomo non viene avviato. Queste opzioni sono disponibili anche tramite il cmdlet PowerShell New-CMStandaloneMedia.
7.  Nella pagina **CD/DVD autonomo** specificare la sequenza di attività che distribuisce il sistema operativo, quindi fare clic su **Avanti**. Per aggiungere contenuto all'elemento multimediale autonomo per le dipendenze dell'applicazione, scegliere **Rileva le dipendenze dell'applicazione associata e aggiungile a questo contenuto multimediale**.
    > [!TIP]
    > Se non vengono visualizzate le dipendenze dell'applicazione previste, deselezionare e selezionare nuovamente l'impostazione **Rileva le dipendenze dell'applicazione associata e aggiungile a questo contenuto multimediale** per aggiornare l'elenco.

    La procedura guidata consente di selezionare solo le sequenze attività associate a un'immagine d'avvio.  

8. Nella pagina **Selezione applicazione**, disponibile a partire dalla versione 1702, specificare il contenuto dell'applicazione da includere nel file del supporto e quindi fare clic su **Avanti**.
9. Nella pagina **Seleziona pacchetto**, disponibile a partire dalla versione 1702, specificare il contenuto del pacchetto da includere nel file del supporto e quindi fare clic su **Avanti**.
10. Nella pagina **Selezionare il pacchetto driver**, disponibile a partire dalla versione 1702, specificare il contenuto del pacchetto driver da includere nel file del supporto e quindi fare clic su **Avanti**.
11.  Nella pagina **Punti di distribuzione** specificare i punti di distribuzione che includono il contenuto richiesto dalla sequenza di attività e quindi fare clic su **Avanti**.  

     Configuration Manager visualizzerà solo i punti di distribuzione che includono il contenuto. Per continuare, è necessario distribuire tutto il contenuto associato alla sequenza di attività (immagine d'avvio, immagine del sistema operativo e così via) in almeno un punto di distribuzione. Dopo la distribuzione del contenuto, è possibile riavviare la procedura guidata o rimuovere i punti di distribuzione già selezionati in questa pagina, passare alla pagina precedente e quindi tornare alla pagina **Punti di distribuzione** per aggiornare l'elenco di punti di distribuzione. Per altre informazioni sulla distribuzione di contenuto, vedere [Distribuire il contenuto a cui fa riferimento una sequenza attività](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS). Per altre informazioni sui punti di distribuzione e la gestione del contenuto, vedere [Gestire il contenuto e l'infrastruttura del contenuto per System Center Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    > [!NOTE]  
    >  È necessario avere i diritti di accesso in **lettura** alla raccolta contenuto nei punti di distribuzione.  

12. Nella pagina **Personalizzazione** specificare le informazioni seguenti e quindi fare clic su **Avanti**.  

    -   Specificare le variabili usate dalla sequenza di attività per distribuire il sistema operativo.  

    -   Specificare i comandi di preavvio da eseguire prima della sequenza di attività. I comandi di preavvio sono costituiti da uno script o da un eseguibile in grado di interagire con l'utente in Windows PE prima che venga eseguita la sequenza di attività per l'installazione del sistema operativo. Per altre informazioni sui comandi di preavvio per i supporti, vedere [Comandi di preavvio per supporti per sequenza di attività in System Center Configuration Manager](../understand/prestart-commands-for-task-sequence-media.md).  

         Facoltativamente, selezionare **Includi file per il comando di preavvio** per includere eventuali file necessari per il comando di preavvio.  

        > [!TIP]  
        >  Durante la creazione del supporto delle sequenza di attività, tale sequenza scrive l'ID del pacchetto e la riga di comando di preavvio, incluso il valore per eventuali variabili della sequenza di attività, nel file di registro CreateTSMedia.log nel computer che esegue la console di Configuration Manager. È possibile rivedere questo file di registro per verificare il valore per le variabili della sequenza di attività.  

13. Completare la procedura guidata.  

 I file di supporto autonomo (ISO) vengono creati nella cartella di destinazione. Se è stata selezionata l'opzione **CD/DVD autonomo**, è ora possibile copiare i file di output in un set di CD o DVD.  

##  <a name="BKMK_StandAloneMediaTSExample"></a> Sequenza di attività di esempio per i supporti autonomi  
 Utilizzare la tabella seguente come guida durante la creazione di una sequenza attività per distribuire un sistema operativo utilizzando supporti autonomi. La tabella sarà utile per decidere la sequenza generale per i passaggi della sequenza di attività e come organizzare e strutturare tali passaggi della sequenza di attività in gruppi logici. La sequenza di attività che crea potrebbe variare da questo esempio e può contenere più o meno passaggi della sequenza attività e gruppi.  

> [!NOTE]  
>  Per creare supporti autonomi, è necessario utilizzare sempre la procedura guidata supporti sequenza di attività.  

|Gruppo sequenza attività o del passaggio|Descrizione|  
|---------------------------------|-----------------|  
|Acquisire i File e impostazioni - **(nuovo gruppo di sequenze attività)**|Creare un gruppo di sequenze di attività. Un gruppo di sequenze di attività consente di mantenere simile passaggi della sequenza attività per una migliore organizzazione e il controllo degli errori.|  
|Acquisisci impostazioni Windows|Utilizzare questo passaggio della sequenza attività per identificare le impostazioni di Microsoft Windows che sono state acquisite dal sistema operativo esistente nel computer di destinazione prima della ricostruzione. È possibile acquisire il nome del computer, utente e informazioni sull'organizzazione e le impostazioni di fuso orario.|  
|Acquisisci impostazioni di rete|Utilizzare questo passaggio della sequenza attività per acquisire le impostazioni di rete dal computer che riceve la sequenza di attività. È possibile acquisire l'appartenenza al gruppo di lavoro o dominio del computer e impostazione delle informazioni relative alla scheda di rete.|  
|Acquisire i file utente e impostazioni - **(nuovo gruppo sequenza attività secondarie)**|Creare un gruppo di sequenze di attività all'interno di un gruppo di sequenze di attività. Questo gruppo secondario contiene i passaggi necessari per acquisire dati sullo stato utente dal sistema operativo esistente nel computer di destinazione prima della ricostruzione. Controllano simile passaggi della sequenza attività insieme per una migliore organizzazione e l'errore simile al gruppo iniziale che è stato aggiunto, questa mantiene sottogruppi.|  
|Percorso locale Imposta stato|Utilizzare questo passaggio della sequenza attività per specificare un percorso locale utilizzando la variabile della sequenza attività percorso protetto. Lo stato utente è archiviato in una directory protetta sul disco rigido.|  
|Acquisisci stato utente|Utilizzare questo passaggio della sequenza attività per acquisire il file e impostazioni utente che si desidera eseguire la migrazione al nuovo sistema operativo.|  
|Installare il sistema operativo - **(nuovo gruppo di sequenze attività)**|Creare un altro gruppo secondario di sequenze attività. Questo gruppo secondario contiene i passaggi necessari per installare il sistema operativo.|  
|Riavviare il computer a Windows PE o un disco rigido|Utilizzare questo passaggio della sequenza attività per specificare le opzioni di riavvio del computer che riceve questa sequenza di attività. Questo passaggio viene visualizzato un messaggio all'utente che indica che il computer verrà riavviato affinché possa continuare l'installazione.<br /><br /> Questo passaggio viene utilizzata la proprietà di sola lettura **_SMSTSInWinPE** variabile della sequenza attività. Se il valore associato è uguale a **false** il passaggio della sequenza attività continua.|  
|Applica sistema operativo|Utilizzare questo passaggio della sequenza attività per installare l'immagine del sistema operativo nel computer di destinazione. Questo passaggio consente di eliminare tutti i file nel volume, ad eccezione dei file di controllo specifici di Configuration Manager, quindi applica tutte le immagini del volume contenute nel file WIM al volume del disco sequenziale corrispondente. È anche possibile specificare un file di risposta **sysprep** per configurare le partizioni del disco da usare per l'installazione.|  
|Applica impostazioni Windows|Usare questo passaggio della sequenza di attività per configurare le informazioni di configurazione delle impostazioni di Windows per il computer di destinazione. Le impostazioni di Windows applicabili sono le informazioni sull'utente e sull'organizzazione, le informazioni sul prodotto o sul codice di licenza, il fuso orario e la password dell'amministratore locale.|  
|Applica impostazioni di rete|Usare questo passaggio della sequenza di attività per specificare le informazioni di configurazione per la rete o il gruppo di lavoro per il computer di destinazione. È inoltre possibile specificare se il computer utilizza un server DHCP oppure è possibile assegnare staticamente le informazioni sull'indirizzo IP.|  
|Applica pacchetto di driver|Utilizzare questo passaggio della sequenza attività per rendere disponibili per l'utilizzo tutti i driver di dispositivo in un pacchetto driver dal programma di installazione di Windows. Tutti i driver necessari devono essere contenuti nel supporto autonomo.|  
|Installazione del sistema operativo - **(nuovo gruppo di sequenze attività)**|Creare un altro gruppo secondario di sequenze attività. Questo sottogruppo contiene i passaggi necessari per installare il client di Configuration Manager.|  
|Imposta Windows e ConfigMgr|Usare questo passaggio della sequenza di attività per installare il software client di Configuration Manager. Configuration Manager installa e registra il GUID del client di Configuration Manager. È possibile assegnare i parametri di installazione necessari nella finestra **Proprietà di installazione** .|  
|Ripristinare file e impostazioni - utente **(nuovo gruppo di sequenze attività)**|Creare un altro gruppo secondario di sequenze attività. Questo gruppo secondario contiene i passaggi necessari per ripristinare lo stato utente.|  
|Ripristina stato utente|Usare questo passaggio della sequenza di attività per avviare l'Utilità di migrazione stato utente e ripristinare lo stato utente e le impostazioni acquisiti dall'azione Acquisisci stato utente nel computer di destinazione.|  


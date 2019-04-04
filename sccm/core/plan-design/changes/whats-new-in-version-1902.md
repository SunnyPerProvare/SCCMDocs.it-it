---
title: Novità della versione 1902
titleSuffix: Configuration Manager
description: Informazioni dettagliate sulle modifiche e sulle nuove funzionalità introdotte nella versione 1902 di Configuration Manager Current Branch.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 81d4a34074e71d97061b8fbcab94e81335df4314
ms.sourcegitcommit: d8d142044586a53709b4478ad945f714737c8d6e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58525044"
---
# <a name="whats-new-in-version-1902-of-configuration-manager-current-branch"></a>Novità della versione 1902 di Configuration Manager Current Branch

*Si applica a: System Center Configuration Manager (Current Branch)*

L'aggiornamento 1902 per Configuration Manager Current Branch è disponibile come aggiornamento nella console. Applicare questo aggiornamento ai siti con la versione 1710, 1802, 1806 o 1810. <!-- baseline only statement:-->Quando si installa un nuovo sito, è disponibile anche come versione di base. Questo articolo offre un riepilogo delle modifiche e delle nuove funzionalità di Configuration Manager versione 1902.  

Esaminare sempre l'elenco di controllo più recente per installare questo aggiornamento. Per altre informazioni, vedere [Elenco di controllo per l'installazione dell'aggiornamento 1902](/sccm/core/servers/manage/checklist-for-installing-update-1902). Dopo aver aggiornato un sito, vedere anche [Elenco di controllo post-aggiornamento](/sccm/core/servers/manage/checklist-for-installing-update-1902#post-update-checklist).

Per sfruttare i vantaggi delle nuove funzionalità di Configuration Manager, dopo l'aggiornamento del sito aggiornare anche i client alla versione più recente. Anche se le nuove funzionalità vengono visualizzate nella console di Configuration Manager quando si esegue l'aggiornamento del sito e della console, lo scenario completo risulta funzionante solo dopo l'aggiornamento alla versione più recente del client.

> [!Note]  
> Questo articolo elenca tutte le funzionalità importanti di questa versione al momento. Tuttavia, non tutte le sezioni sono ancora collegate al contenuto aggiornato con maggiori informazioni sulle nuove funzionalità. Continuare a controllare questa pagina con regolarità per verificare la disponibilità di aggiornamenti. Le modifiche sono contrassegnate con il tag ***[Aggiornato]***. Questa nota sarà rimossa nella versione finale del contenuto.  

> [!Tip]  
> Per ricevere una notifica quando questa pagina viene aggiornata, copiare e incollare l'URL seguente nel lettore di feed RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1902+-+Configuration+Manager%22&locale=en-us`



## <a name="bkmk_deprecated"></a> Funzionalità e sistemi operativi deprecati

Per conoscere le modifiche relative al supporto prima che siano implementate, vedere [Elementi rimossi e deprecati](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

- È stata modificata l'implementazione per la condivisione del contenuto da Azure. Usare un gateway di gestione cloud abilitato per il contenuto abilitando l'opzione **Consenti il funzionamento di CMG come punto di distribuzione cloud e per la gestione di contenuti da Archiviazione di Azure**. Non sarà possibile creare un punto di distribuzione cloud tradizionale in futuro.

Nella versione 1902 viene eliminato il supporto per i prodotti seguenti:  

- Linux e UNIX come client. La deprecazione è stata annunciata con la [versione 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802#deprecation-announcement-for-linux-and-unix-client-support). Per la gestione dei server Linux, è possibile usare la gestione di Microsoft Azure. Le soluzioni di Azure includono un ampio supporto per Linux che nella maggior parte dei casi supera le funzionalità di Configuration Manager, inclusa la gestione end-to-end delle patch per Linux.



## <a name="bkmk_infra"></a> Infrastruttura del sito

### <a name="client-health-dashboard"></a>Dashboard sull'integrità del client
<!--3599209-->
La distribuzione di aggiornamenti software e altre app per proteggere l'ambiente raggiunge solo i client integri. I client di Configuration Manager non integri hanno effetti negativi sulla conformità complessiva. Determinare lo stato del client può essere difficile e molto dipende dalla base di partenza, ovvero dal numero totale di dispositivi nell'ambito di gestione. Ad esempio, se si rilevano tutti i sistemi di Active Directory, anche se alcuni record provengono da computer ritirati, il processo aumenta la base di partenza. 

Ora è possibile visualizzare un dashboard con informazioni sull'integrità dei client di Configuration Manager nell'ambiente in uso. Il dashboard consente di visualizzare l'integrità dei client, l'integrità dello scenario e gli errori più comuni. È possibile filtrare la visualizzazione per diversi attributi per visualizzare i potenziali problemi per versione del sistema operativo e client. 

Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**. Espandere **Stato client** e selezionare il nodo **Dashboard sull'integrità del client**. 

![Screenshot del dashboard sull'integrità del client](media/3599209-client-health-dashboard.png)

<!-- For more information, see [How to monitor clients](/sccm/core/clients/manage/monitor-clients). -->


### <a name="new-management-insight-rules"></a>Nuove regole delle informazioni dettagliate sulla gestione
La funzionalità di informazioni dettagliate sulla gestione prevede le nuove regole seguenti:

- Più regole con consigli sulla gestione delle raccolte. Usare queste informazioni dettagliate per semplificare la gestione e migliorare le prestazioni. Esaminare queste nuove regole nel gruppo **Raccolte**.<!--3555752-->  

- Regola **Aggiorna i client a una versione di Windows 10 supportata** nel gruppo **Gestione semplificata**. Questa regola segnala i client che eseguono una versione di Windows 10 che non è più supportata. Include anche i client con una versione di Windows 10 che sta per raggiungere la fine del servizio (tre mesi).<!--3897268-->  

<!-- For more information, see [Management insights](/sccm/core/servers/manage/management-insights). -->


### <a name="improvement-to-enhanced-http"></a>Miglioramento del protocollo HTTP avanzato
<!--3798957-->
È ora possibile abilitare il protocollo HTTP avanzato per ogni sito primario o per il sito di amministrazione centrale. 

Nelle proprietà del sito di amministrazione centrale selezionare l'opzione **Usa i certificati generati da Configuration Manager per sistemi del sito HTTP**. Questa impostazione si applica solo ai ruoli del sistema del sito nel sito di amministrazione centrale. Non è un'impostazione globale per la gerarchia. 

<!-- For more information, see [enhanced HTTP](/sccm/core/plan-design/hierarchy/enhanced-http). -->


### <a name="improvement-to-setup-prerequisites"></a>Miglioramenti dei prerequisiti nel programma di installazione
Quando si installa la versione 1902 o si esegue l'aggiornamento a questa versione, il programma di installazione di Configuration Manager include ora i controlli dei prerequisiti seguenti:

- **Riavvio del sistema in sospeso nell'istanza remota di SQL Server**: questo controllo dei prerequisiti è simile alla regola **Riavvio del sistema in sospeso**, ma viene eseguito in un'istanza remota di SQL Server. Per altre informazioni, vedere [Elenco dei controlli dei prerequisiti](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#pending-system-restart-on-the-remote-sql-server). <!--SCCMDocs-pr issue 3377-->  



## <a name="bkmk_cloud"></a> Gestione collegata al cloud

### <a name="stop-cloud-service-when-it-exceeds-threshold"></a>Arrestare il servizio cloud al superamento di una soglia
<!--3735092-->
Configuration Manager ora può arrestare un servizio gateway di gestione cloud quando il trasferimento dei dati totale supera il limite. In Cloud Management Gateway sono sempre stati presenti avvisi per attivare le notifiche quando l'utilizzo raggiunge livelli di avviso o critici. Per ridurre l'incidenza di costi di Azure non previsti a causa di un picco di utilizzo, questa nuova opzione consente di disattivare il servizio cloud. 

[Configurare gli avvisi del traffico in uscita](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway#set-up-outbound-traffic-alerts) in Cloud Management Gateway e quindi abilitare l'opzione **Arresta questo servizio quando viene superata la soglia critica**.  

<!-- For more information, see [Set up outbound traffic alerts](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway#set-up-outbound-traffic-alerts). -->


### <a name="use-azure-resource-manager-for-cloud-services"></a>Usare Azure Resource Manager per i servizi cloud
<!--3605704-->
A partire dalla versione 1810, la distribuzione classica del servizio in Azure è deprecata in Configuration Manager. La versione citata è l'ultima versione che supporta la creazione di queste distribuzioni di Azure. 

Le distribuzioni esistenti continuano a funzionare normalmente. A partire dalla presente versione Current Branch, Azure Resource Manager è l'unico meccanismo di distribuzione per le nuove istanze di Cloud Management Gateway e del punto di distribuzione cloud.

<!-- For more information, see [Azure Resource Manager for the cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).   -->


### <a name="add-cloud-management-gateway-to-boundary-groups"></a>Aggiungere Cloud Management Gateway ai gruppi di limiti
<!--3640932-->
È ora possibile associare un Cloud Management Gateway (CMG) con un gruppo di limiti. Questa configurazione consente ai client di usare Cloud Management Gateway per impostazione predefinita o come fallback per le comunicazioni client in base alle relazioni del gruppo di limiti. Questo comportamento è particolarmente utile in scenari con succursali e VPN. È possibile spostare il traffico client da collegamenti WAN lenti e dispendiosi e usare invece collegamenti Internet più veloci a Microsoft Azure.

<!-- For more information, see [Plan for the CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway). -->



## <a name="bkmk_real"></a> Gestione in tempo reale

### <a name="run-cmpivot-from-the-central-administration-site"></a>Eseguire CMPivot dal sito di amministrazione centrale
<!--3610960-->
Configuration Manager supporta ora l'esecuzione di CMPivot dal sito di amministrazione centrale in una gerarchia. Il sito primario gestisce ancora la comunicazione con il client. Quando CMPivot viene eseguito dal sito di amministrazione centrale, comunica con il sito primario tramite il canale di sottoscrizione dei messaggi ad alta velocità. Questa comunicazione non si basa sulla replica SQL standard tra siti.

<!-- For more information, see [CMPivot for real-time data](/sccm/core/servers/manage/cmpivot). -->


### <a name="edit-or-copy-powershell-scripts"></a>Modificare o copiare gli script di PowerShell
<!--3705507-->
È ora possibile usare il comando **Modifica** o **Copia** per uno script di PowerShell esistente usato con la funzionalità Esegui script. Anziché ricreare uno script che è necessario modificare, ora è possibile modificarlo direttamente. Entrambe le azioni usano la stessa esperienza con procedura guidata presentata per la creazione di un nuovo script. Quando si modifica o si copia uno script, Configuration Manager non salva in modo permanente lo stato di approvazione. 

<!-- For more information, see [Run Scripts](/sccm/apps/deploy-use/create-deploy-scripts). -->



## <a name="bkmk_content"></a> Gestione dei contenuti

### <a name="distribution-point-maintenance-mode"></a>Modalità manutenzione per il punto di distribuzione 
<!--3555754-->
Ora è possibile impostare un punto di distribuzione in modalità di manutenzione. Abilitare la modalità di manutenzione quando si installano aggiornamenti software o quando si modifica l'hardware del server.

Quando il punto di distribuzione è in modalità di manutenzione, ha i comportamenti seguenti: 

- Il sito non distribuisce nessun contenuto al punto di distribuzione.  

- I punti di gestione non restituiscono la posizione del punto di distribuzione ai client. 

- Quando si aggiorna il sito, un punto di distribuzione in modalità di manutenzione viene comunque aggiornato. 

- Le proprietà del punto di distribuzione sono di sola lettura. Ad esempio non è possibile modificare il certificato o aggiungere gruppi di limiti.  

- Qualsiasi operazione pianificata, ad esempio la convalida del contenuto, viene eseguita con la pianificazione esistente. 

<!-- For more information, see [Maintenance mode](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_maint) -->



## <a name="bkmk_client"></a> Gestione dei client

### <a name="client-provisioning-mode-timeout"></a>Timeout della modalità di provisioning dei client
<!--3197824-->
La sequenza di attività imposta un timestamp quando il client passa in modalità di provisioning. Un client in modalità di provisioning controlla ogni 60 minuti il tempo trascorso dall'impostazione del timestamp. Se è rimasto in modalità di provisioning per più di 48 ore, il client esce automaticamente da tale modalità e riavvia il processo. 

<!-- For more information, see ... -->

### <a name="view-first-screen-only-during-remote-control"></a>Visualizzare solo il primo schermo durante il controllo remoto
<!--3231732-->
Quando ci si connette a un client con due o più monitor, può essere difficile visualizzarli tutti nel visualizzatore del controllo remoto di Configuration Manager. Un operatore strumenti remoti può ora scegliere tra le opzioni di visualizzazione **Tutti gli schermi** e **Primo schermo**. 

<!-- For more information, see [How to remotely administer a Windows client computer](/sccm/core/clients/manage/remote-control/remotely-administer-a-windows-client-computer). -->


### <a name="specify-a-custom-port-for-peer-wakeup"></a>Specificare una porta personalizzata per la riattivazione peer
<!--3605925-->
È ora possibile specificare un numero di porta personalizzato per il proxy di riattivazione. Nel gruppo **Risparmio energia** delle impostazioni client configurare l'impostazione **Numero di porta di riattivazione LAN (UDP)**.  

<!-- For more information, see [How to configure Wake on LAN](/sccm/core/clients/deploy/configure-wake-on-lan). -->



<!-- ## <a name="bkmk_comgmt"></a> Co-management -->




<!-- ## <a name="bkmk_compliance"></a> Compliance settings -->



## <a name="bkmk_app"></a> Gestione delle applicazioni

### <a name="improvements-to-application-approvals-via-email"></a>Miglioramenti delle approvazioni dell'applicazione tramite posta elettronica
<!--3594063-->
Questa versione include miglioramenti della funzionalità di ricezione delle notifiche tramite posta elettronica per le richieste dell'applicazione. Gli utenti hanno sempre avuto la possibilità di aggiungere un commento alla richiesta da Software Center. Questo commento viene visualizzato nella richiesta dell'applicazione nella console di Configuration Manager. Ora tale commento viene visualizzato anche nel messaggio di posta elettronica. Includere questo commento nel messaggio di posta elettronica consente ai responsabili dell'approvazione di decidere più facilmente se approvare o rifiutare la richiesta.

<!-- For more information, see [Email notifications](/sccm/apps/deploy-use/app-approval#bkmk_email-approve). -->


### <a name="improvements-to-package-conversion-manager"></a>Miglioramenti di Package Conversion Manager
<!-- SCCMDocs-pr issue #3357 -->
Questa versioni include i miglioramenti di [Package Conversion Manager](/sccm/apps/pcm/package-conversion-manager) seguenti:
- L'analisi pianificata dei pacchetti viene eseguita ogni 7 giorni per impostazione predefinita
- Cmdlet di PowerShell per l'analisi e la conversione dei pacchetti
- Miglioramenti e correzioni di bug generali



## <a name="bkmk_osd"></a> Distribuzione del sistema operativo


### <a name="progress-status-during-in-place-upgrade-task-sequence"></a>Stato di avanzamento durante la sequenza di attività di aggiornamento sul posto
<!--3747129-->
È ora possibile visualizzare un indicatore di stato più dettagliato durante una sequenza di attività di aggiornamento sul posto di Windows 10. Questa barra mostra lo stato di avanzamento dell'installazione di Windows, che in caso contrario è invisibile all'utente durante la sequenza di attività. Gli utenti hanno ora visibilità dello stato di avanzamento sottostante. Ciò è utile per evitare il dubbio che il processo di aggiornamento sia sospeso, a causa della mancanza di indicazioni sullo stato.  

![Esempio di stato della sequenza di attività con indicazione dello stato dell'aggiornamento di Windows](media/3747129-installation-progress.png)

Questa funzionalità può essere usata con qualsiasi versione supportata di Windows 10 e solo con la sequenza di attività di aggiornamento sul posto. 


### <a name="improvements-to-task-sequence-media-creation"></a>Miglioramenti nella creazione del supporto per la sequenza di attività 
<!--3556027, fka 1359388-->
Questa versione include diversi miglioramenti che consentono di creare e gestire in modo migliore il supporto per la sequenza di attività. <!-- For more information, see [Create task sequence media](/sccm/osd/deploy-use/create-task-sequence-media). -->

#### <a name="specify-temporary-storage"></a>Specificare un archivio temporaneo
Quando si crea il supporto per la sequenza attività, ora è possibile personalizzare il percorso usato dal sito per l'archiviazione temporanea dei dati. Questo processo può richiedere molto spazio sul disco temporaneo. Questa modifica consente una maggiore flessibilità nella scelta del percorso di archiviazione di questi file temporanei. 

In **Creazione guidata del supporto per sequenza attività**, specificare un percorso per **Staging folder** (Cartella di gestione temporanea). Per impostazione predefinita questo percorso è simile al seguente: `%UserProfile%\AppData\Local\Temp`.

#### <a name="add-a-label-to-the-media"></a>Aggiungere un'etichetta al supporto
È ora possibile aggiungere un'etichetta al supporto per la sequenza attività. Questa etichetta consente di identificare più facilmente il supporto creato. In **Creazione guidata del supporto per sequenza attività**, specificare un percorso per **Media label** (Etichetta del supporto).


### <a name="import-a-single-index-of-an-os-image"></a>Importare un singolo indice di un'immagine del sistema operativo
<!--3719699-->
Quando si importa un file di immagine di Windows (con estensione wim) in Configuration Manager, ora è possibile specificare l'importazione di un indice singolo anziché di tutti gli indici di immagine nel file. Questa opzione offre i vantaggi seguenti:

- File di immagine più piccolo  
- Installazione offline più rapida  
- Ottimizzazione della manutenzione delle immagini per ottenere un file di immagine più piccolo dopo la manutenzione offline 

Quando si importa un'immagine del sistema operativo, selezionare l'opzione **Estrai un indice delle immagini specifico dal file WIM specificato**. Quindi selezionare l'indice immagine nell'elenco.  

<!-- For more information, see [Add an OS image](/sccm/osd/get-started/manage-operating-system-images#BKMK_AddOSImages). -->


### <a name="optimized-image-servicing"></a>Servizio immagini ottimizzato
<!--3555951-->
Quando si applicano aggiornamenti software a un'immagine del sistema operativo, è disponibile una nuova opzione per ottimizzare l'output rimuovendo tutti gli aggiornamenti sostituiti. L'ottimizzazione per l'installazione offline si applica solo alle immagini con un indice singolo. 

Quando si crea una pianificazione per l'aggiornamento di un'immagine del sistema operativo, selezionare l'opzione **Rimuovi gli aggiornamenti sostituiti dopo l'aggiornamento dell'immagine**. 

<!-- For more information, see [Apply software updates to an image](/sccm/osd/get-started/manage-operating-system-images#BKMK_OSImagesApplyUpdates).  -->


### <a name="improvements-to-run-powershell-script-task-sequence-step"></a>Miglioramenti del passaggio della sequenza di attività Esegui script PowerShell
<!--3556028, fka 1359389-->
Il passaggio della sequenza di attività **Esegui script PowerShell** include ora i miglioramenti seguenti:  

- È ora possibile immettere direttamente il codice di Windows PowerShell in questo passaggio. Questa modifica consente di eseguire i comandi PowerShell durante una sequenza di attività senza prima creare e distribuire un pacchetto con lo script.

- Quando si sceglie l'opzione **Immettere uno script di PowerShell**, selezionare **Modifica script**. La nuova finestra dello script di PowerShell consente le azioni seguenti:  

    - Modificare lo script direttamente  

    - Aprire uno script esistente dal file  

    - Passare a uno script esistente approvato in Configuration Manager

- Salvare l'output dello script in una variabile della sequenza di attività personalizzata  

- Per includere i parametri dello script nel log della sequenza di attività, impostare la variabile della sequenza di attività **OSDLogPowerShellParameters** su **TRUE**. Per impostazione predefinita, i parametri non sono nel log.  

- Altri miglioramenti che offrono funzionalità simili al passaggio [Esegui riga di comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine). Ad esempio, la possibilità di specificare credenziali utente alternative o un timeout. 

> [!Important]  
> Per sfruttare i vantaggi di questa nuova funzionalità di Configuration Manager, dopo l'aggiornamento del sito aggiornare anche i client alla versione più recente. Anche se le nuove funzionalità vengono visualizzate nella console di Configuration Manager quando si esegue l'aggiornamento del sito e della console, lo scenario completo risulta funzionante solo dopo l'aggiornamento alla versione più recente del client.

<!-- For more information, see [Run PowerShell Script](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript). -->


### <a name="other-improvements-to-os-deployment"></a>Altri miglioramenti alla distribuzione del sistema operativo
<!--3633146,3641475,3654172,3734270-->
Questa versione include i miglioramenti della distribuzione del sistema operativo seguenti:

- È disponibile una nuova azione predefinita **Visualizza** nelle sequenza di attività. <!--3633146-->  

- La finestra di dialogo di errore della sequenza di attività include ora maggiori informazioni, ad esempio il nome del passaggio della sequenza di attività che non è stato completato. <!--3641475-->  

- Quando si imposta la variabile della sequenza di attività **OSDDoNotLogCommand** su True, ora viene nascosta anche la riga di comando del passaggio Esegui riga di comando nel file di log. In precedenza veniva mascherato solo il nome del programma nel passaggio Installa pacchetto in smsts.log.<!--3654172-->  

- Quando si abilita un risponditore PXE senza i Servizi di distribuzione Windows, è ora possibile abilitarlo sullo stesso server del servizio DHCP. <!--3734270-->  <!-- For more information, see ... -->



## <a name="bkmk_userxp"></a> Software Center

### <a name="replace-toast-notifications-with-dialog-window"></a>Sostituire le notifiche di tipo avviso popup con una finestra di dialogo
<!--3555947-->
In alcuni casi gli utenti non vedono la notifica di tipo avviso popup di Windows per un riavvio o una distribuzione necessaria, quindi non vedono l'esperienza per posporre il promemoria. Questo comportamento può causare un'esperienza utente insoddisfacente quando il client raggiunge una scadenza.

Adesso, quando le distribuzioni richiedono un riavvio o sono richieste modifiche software, si ha la possibilità di usare una finestra di dialogo più invasiva. 

#### <a name="software-changes-are-required"></a>Sono richieste modifiche software
Nella pagina **Esperienza utente** della Distribuzione guidata del software selezionare l'opzione di notifica utente **Visualizza in Software Center e mostra tutte le notifiche**. Selezionare quindi l'opzione seguente: **Quando sono necessarie modifiche al software, mostra una finestra di dialogo all'utente invece di un avviso popup**.  

<!-- For more information, see [Configure Software Center](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex) -->

#### <a name="restart-required"></a>Riavvio richiesto
Nel gruppo **Riavvio del computer** delle impostazioni client abilitare l'opzione seguente: **Quando una distribuzione richiede un riavvio, mostra una finestra di dialogo all'utente invece di un avviso popup**.  

<!-- For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings#computer-restart). -->


### <a name="configure-user-device-affinity-in-software-center"></a>Configurare l'affinità utente-dispositivo in Software Center
<!--3485366-->
Con i [miglioramenti dell'infrastruttura di Software Center](/sccm/core/plan-design/changes/whats-new-in-version-1806#software-center-infrastructure-improvements) apportati a partire dalla versione 1806, i ruoli del server del sito del Catalogo applicazioni non sono più necessari per la maggior parte degli scenari. Alcuni clienti si affidano ancora al Catalogo applicazioni per consentire agli utenti di impostare l'affinità utente-dispositivo del dispositivo primario. 

Gli utenti possono ora impostare il dispositivo primario in Software Center. Con questa azione diventano utenti primari del dispositivo in Configuration Manager.

<!-- For more information, see [Link users and devices with user device affinity](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity). -->


### <a name="configure-default-views-in-software-center"></a>Configurare le visualizzazioni predefinite in Software Center
<!--3612112-->
Questa versione di Configuration Manager offre ulteriori novità per la personalizzazione di Software Center:
 
- Impostare il layout predefinito delle applicazioni, ovvero come riquadri o come elenco  

    - Se un utente modifica questa configurazione, Software Center salva la preferenza dell'utente per il futuro  

- Configurare il filtro predefinito per le applicazioni, ovvero tutte le app o solo le app richieste  

    - Software Center usa sempre l'impostazione predefinita. Gli utenti possono modificare questo filtro, ma la preferenza non viene salvata da Software Center.    

Specificare queste impostazioni nel gruppo di impostazioni client di **Software Center**.

<!-- For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings#software-center). -->



## <a name="bkmk_sum"></a> Aggiornamenti software

### <a name="specify-priority-for-feature-updates-in-windows-10-servicing"></a>Specificare la priorità per gli aggiornamenti delle funzionalità nella manutenzione di Windows 10
<!--3734525-->
È possibile modificare la priorità con cui i client installano gli aggiornamenti delle funzionalità tramite [Manutenzione pacchetti di Windows 10](/sccm/osd/deploy-use/manage-windows-as-a-service). Per impostazione predefinita, i client ora installano gli aggiornamenti delle funzionalità con priorità di elaborazione più alta. 

Usare le impostazioni client per configurare questa opzione. Nel gruppo **Aggiornamenti software** configurare l'impostazione seguente: **Specificare la priorità del thread per gli aggiornamenti delle funzionalità**. 

<!-- For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings#software-updates). -->



## <a name="bkmk_o365"></a> Gestione di Office

### <a name="redirect-windows-known-folders-to-onedrive"></a>Reindirizzare le cartelle note di Windows in OneDrive
<!--3556021-->
Usare Configuration Manager per spostare le cartelle note di Windows in OneDrive for Business. Queste cartelle includono Desktop, Documenti e Immagini. Per semplificare gli aggiornamenti di Windows 10, distribuire queste impostazioni ai client Windows 7 prima di distribuire una sequenza di attività. 

Per altre informazioni su questa funzionalità di OneDrive for Business, vedere [Reindirizzare e spostare le cartelle note di Windows su OneDrive](https://docs.microsoft.com/onedrive/redirect-known-folders).

Prima di tutto, [trovare l'ID tenant di Office 365](https://docs.microsoft.com/onedrive/find-your-office-365-tenant-id). Distribuire quindi il client di sincronizzazione di OneDrive versione 18.111.0603.0004 o successiva. Per altre informazioni, vedere [Distribuire le app OneDrive mediante System Center Configuration Manager](https://docs.microsoft.com/onedrive/deploy-on-windows).  

Per creare e distribuire un profilo di OneDrive for Business, nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**. Espandere **Impostazioni di conformità** e selezionare il nodo **Profili di OneDrive for Business**.  

<!-- For more information, see [Redirect Windows known folders to OneDrive](/sccm/compliance/deploy-use/onedrive-profile). -->


### <a name="integration-with-analytics-for-office-365-proplus-readiness"></a>Integrazione con l'analisi per l'idoneità per Office 365 ProPlus
<!--3735402-->
Usare Configuration Manager per identificare in modo attendibile i dispositivi pronti per l'aggiornamento a Office 365 ProPlus. Grazie all'integrazione con l'analisi di Office, garantisce approfondimenti relativi a qualsiasi potenziale problema di compatibilità con i componenti aggiuntivi e le macro di Office usate nell'ambiente. Quindi è possibile usare Configuration Manager per distribuire Office nei dispositivi pronti. 

Il dashboard di gestione client di Office 365 esistente include ora un nuovo riquadro **Office 365 ProPlus - Preparazione aggiornamenti**.

<!-- For more information, see [Office 365 client management dashboard](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard) -->


### <a name="additional-languages-for-office-365-updates"></a>Lingue aggiuntive per gli aggiornamenti di Office 365
<!--3555955-->
Ora Configuration Manager supporta tutte le lingue supportate per gli aggiornamenti del client Office 365. Il flusso di lavoro di aggiornamento ora fa distinzione tra le 38 lingue per **Windows Update** e le 103 lingue per l'**aggiornamento client di Office 365**. 

<!-- For more information, see [Office 365 client management dashboard](/sccm/sum/deploy-use/manage-office-365-proplus-updates#office-365-client-management-dashboard) -->


### <a name="office-products-on-lifecycle-dashboard"></a>Prodotti Office nel dashboard del ciclo di vita
<!--3556026-->
Il dashboard del ciclo di vita del prodotto ora include informazioni per le versioni installate da Office 2003 a Office 2016. I dati vengono visualizzati dopo che il sito esegue l'attività di riepilogo del ciclo di vita, ovvero ogni 24 ore.

<!-- For more information, see [Use the Product Lifecycle dashboard](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard). -->



<!-- ## <a name="bkmk_inv"></a> Inventory -->



## <a name="bkmk_pod"></a> Distribuzioni in più fasi

### <a name="dedicated-monitoring-for-phased-deployments"></a>Monitoraggio dedicato per le distribuzioni in più fasi
<!--3555949-->
Le distribuzioni in più fasi hanno ora un nodo di monitoraggio dedicato. Questo nodo semplifica l'identificazione delle distribuzioni in più fasi create ed è quindi possibile passare alla visualizzazione di monitoraggio delle distribuzioni in più fasi. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio** e selezionare il nodo **Distribuzioni in più fasi**. Questo visualizza l'elenco delle distribuzioni in più fasi.

<!-- For more information, see [Phased deployment monitoring view](/sccm/osd/deploy-use/manage-monitor-phased-deployments#bkmk_monitor). -->


### <a name="improvement-to-phased-deployment-success-criteria"></a>Miglioramento dei criteri di superamento della distribuzione in più fasi
<!--3555946-->
Specificare criteri aggiuntivi per l'esito positivo di una fase in una distribuzione in più fasi. Anziché essere limitati a una percentuale, questi criteri ora possono corrispondere anche al numero di dispositivi distribuiti correttamente. Questa opzione è utile quando le dimensioni della raccolta sono variabili ed è necessario verificare l'esito positivo per un numero specifico di dispositivi prima di passare alla fase successiva. 

Creare una distribuzione in più fasi per una sequenza di attività, un'applicazione o un aggiornamento software. Nella pagina Impostazioni della procedura guidata selezionare quindi l'opzione seguente come criterio per l'esito positivo della prima fase: **Numero di dispositivi distribuiti correttamente**. 

<!-- For more information, see [Create phased deployments](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence). -->



## <a name="bkmk_admin"></a> Console di Configuration Manager

### <a name="bkmk_console"></a> Miglioramenti alla console di Configuration Manager
<!--3594151-->
In base ai suggerimenti dei clienti raccolti durante il Midwest Management Summit (MMS) Desert Edition 2018, questa versione include i miglioramenti seguenti della console di Configuration Manager:
- Ingrandire la finestra Sfoglia Registro di sistema per i metodi di rilevamento delle applicazioni
- Passare alla raccolta dalla distribuzione di un'applicazione
- Rimuovere il contenuto dal monitoraggio dello stato
- Organizzare le visualizzazioni in base a valori interi nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio**
- Spostare l'avviso per un numero elevato di risultati

<!-- For more information, see [Using the Configuration Manager console](/sccm/core/servers/manage/admin-console). -->


### <a name="configuration-manager-console-notifications"></a>Notifiche della console di Configuration Manager
<!--3556016, fka 1318035-->
Per fornire informazioni più accurate che consentano di intraprendere l'azione appropriata, la console di Configuration Manager ora invia una notifica per gli eventi seguenti:
- Quando è disponibile un aggiornamento per Configuration Manager
- Quando nell'ambiente si verificano eventi di manutenzione e relativi al ciclo di vita

Queste notifiche sono visualizzate in una barra nella parte superiore della finestra della console sotto la barra multifunzione. Sostituiscono l'esperienza precedente che avvisava della disponibilità di aggiornamenti di Configuration Manager. Queste notifiche nella console visualizzano comunque informazioni critiche, ma non interferiscono con l'interazione tra utente e console. Le notifiche critiche non possono essere ignorate. Tutte le notifiche della console sono visualizzate in una nuova area di notifica della barra del titolo. 

<!-- For more information, see [Using the Configuration Manager console](/sccm/core/servers/manage/admin-console). -->


### <a name="confirmation-of-console-feedback"></a>Conferma del feedback della console
<!--3556010-->
Quando si inviano [commenti e suggerimenti](/sccm/core/understand/find-help#product-feedback) nella console di Configuration Manager, ora viene visualizzato un messaggio di conferma. Questo messaggio include un **ID dei commenti**, che è possibile comunicare a Microsoft come identificatore per la tracciabilità. 

<!-- For more information, see [Product feedback](/sccm/core/understand/find-help#product-feedback). -->


### <a name="view-recently-connected-consoles"></a>Visualizzare le console connesse di recente 
<!--3699367-->
È ora possibile visualizzare le connessioni più recenti per la console di Configuration Manager. La visualizzazione include le connessioni attive e quelle stabilite di recente. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Sicurezza** e selezionare il nodo **Connessioni di console**.

<!-- For more information, see [Using the Configuration Manager console](/sccm/core/servers/manage/admin-console). -->


### <a name="in-console-documentation-dashboard"></a>Dashboard della documentazione nella console
<!--3556019, fka 1357546-->
È presente un nuovo nodo **Documentazione** nella nuova area di lavoro **Community**. Questo nodo contiene informazioni aggiornate sulla documentazione di Configuration Manager e gli articoli del supporto tecnico.

<!-- For more information, see [Using the Configuration Manager console](/sccm/core/servers/manage/admin-console). -->


### <a name="search-device-views-using-mac-address"></a>Eseguire la ricerca nelle visualizzazioni dispositivi tramite indirizzi MAC
<!--3600878-->
È ora possibile cercare un indirizzo MAC in una visualizzazione dispositivi della console di Configuration Manager. Questa proprietà è utile per gli amministratori della distribuzione di sistemi operativi durante la risoluzione dei problemi delle distribuzioni basate su Pre-Boot eXecution Environment. Quando si visualizza un elenco di dispositivi, aggiungere la colonna **Indirizzo MAC** alla visualizzazione. Usare il campo di ricerca per aggiungere i criteri di ricerca **Indirizzo MAC**. 


### <a name="use-net-47-for-improved-console-accessibility"></a>Usare .NET 4.7 per una migliore accessibilità della console
<!-- SCCMDocs-pr issue #3228 -->
Per migliorare le funzionalità di accessibilità della console di Configuration Manager, aggiornare .NET alla versione 4.7 o successiva nel computer che esegue la console. 

Per altre informazioni, vedere [Funzionalità di accessibilità in Configuration Manager](/sccm/core/understand/accessibility-features).



<!-- ## <a name="bkmk_opmdm"></a> On-premises MDM -->




## <a name="other-updates"></a>Altri aggiornamenti

<!-- Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 1902](https://support.microsoft.com/help/4482169). -->

Per altre informazioni sulle modifiche apportate ai cmdlet di Windows PowerShell per Configuration Manager, vedere le [note sulla versione 1902 di PowerShell](https://docs.microsoft.com/powershell/sccm/1902-release-notes?view=sccm-ps).

<!-- 
The following update rollup (4486457) is available in the console starting on 25 January 2019: [Update rollup for Configuration Manager current branch, version 1902](https://support.microsoft.com/help/4486457).


### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |
 
-->



## <a name="next-steps"></a>Passaggi successivi

Prima di installare questa versione, vedere [Installazione degli aggiornamenti per Configuration Manager](/sccm/core/servers/manage/updates) ed [Elenco di controllo per l'installazione dell'aggiornamento 1902](/sccm/core/servers/manage/checklist-for-installing-update-1902).

> [!TIP]  
> Per installare un nuovo sito, usare una versione base di Configuration Manager.  
>
>  Sono disponibili altre informazioni su:    
>   - [Installing new sites](/sccm/core/servers/deploy/install/installing-sites) (Installare nuovi siti)  
>   - [Baseline and update versions](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions) (Versioni di base e di aggiornamento)  

Per problemi noti e importanti, vedere [Note sulla versione](/sccm/core/servers/deploy/install/release-notes).

Dopo aver aggiornato un sito, vedere anche [Elenco di controllo post-aggiornamento](/sccm/core/servers/manage/checklist-for-installing-update-1902#post-update-checklist).
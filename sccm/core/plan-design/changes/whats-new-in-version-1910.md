---
title: Novità della versione 1910
titleSuffix: Configuration Manager
description: Informazioni dettagliate sulle modifiche e sulle nuove funzionalità introdotte nella versione 1906 di Configuration Manager Current Branch.
ms.date: 12/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3e1ddb65-1193-46ce-a7c0-a48dfd9fd833
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 545b68cd1628bb9652f1e87da96e5fb6e18787f1
ms.sourcegitcommit: 3a0eaf3378632f312b46b2b8a524e286f9c4cd8e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75198490"
---
# <a name="whats-new-in-version-1910-of-configuration-manager-current-branch"></a>Novità della versione 1910 di Configuration Manager Current Branch

*Si applica a: Configuration Manager (Current Branch)*

L'aggiornamento 1910 per Configuration Manager Current Branch è disponibile come aggiornamento nella console. Applicare questo aggiornamento ai siti con la versione 1806 o successiva. <!-- baseline only statement:When installing a new site, it's also available as a baseline version.--> Questo articolo offre un riepilogo delle modifiche e delle nuove funzionalità di Configuration Manager versione 1910.  

Esaminare sempre l'elenco di controllo più recente per installare questo aggiornamento. Per altre informazioni, vedere [Elenco di controllo per l'installazione dell'aggiornamento 1910](/sccm/core/servers/manage/checklist-for-installing-update-1910). Dopo aver aggiornato un sito, vedere anche [Elenco di controllo post-aggiornamento](/sccm/core/servers/manage/checklist-for-installing-update-1910#post-update-checklist).

Per sfruttare i vantaggi delle nuove funzionalità di Configuration Manager, dopo l'aggiornamento del sito aggiornare anche i client alla versione più recente. Anche se le nuove funzionalità vengono visualizzate nella console di Configuration Manager quando si esegue l'aggiornamento del sito e della console, lo scenario completo risulta funzionante solo dopo l'aggiornamento alla versione più recente del client.

> [!Tip]  
> Per ricevere una notifica quando questa pagina viene aggiornata, copiare e incollare l'URL seguente nel lettore di feed RSS: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1910+-+Configuration+Manager%22&locale=en-us`

## <a name="bkmk_mem"></a> Microsoft Endpoint Configuration Manager

<!--4960084-->

Configuration Manager è ora incluso in Microsoft Endpoint Manager.

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Endpoint Manager è una soluzione integrata per la gestione di tutti i dispositivi. Microsoft riunisce Configuration Manager e Intune con una gestione delle licenze semplificata. L'investimento esistente in Configuration Manager continua a essere valido e consente al contempo di sfruttare i vantaggi offerti dalla potenza del cloud Microsoft.

Le soluzioni di gestione Microsoft seguenti fanno ora parte del marchio **Microsoft Endpoint Manager**:

- [Configuration Manager](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [Desktop Analytics](/configmgr/desktop-analytics/overview)
- [Autopilot](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot)
- Altre funzionalità della [console di amministrazione della gestione dei dispositivi](https://go.microsoft.com/fwlink/?linkid=2109094)

Per altre informazioni, vedere i post seguenti di Brad Anderson, vicepresidente di Microsoft, per Microsoft 365:

- [Post di blog sull'annuncio](https://aka.ms/cmannounce)
- [Documento sulla visione](https://aka.ms/MEMVisionPaper)
- [Video di riepilogo dell'annuncio](https://youtu.be/GS7oNPInFuw)

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>Che cosa cambia in Configuration Manager con l'introduzione di Microsoft Endpoint Manager?

Nella versione 1910, a parte il nuovo nome, Configuration Manager funziona allo stesso modo. Alcuni cambiamenti di nome possono avere effetto sull'uso dei componenti seguenti:

- **Console di Configuration Manager**: trovare i collegamenti alla console e al **visualizzatore controllo remoto** nel menu Start di Windows nella cartella **Microsoft Endpoint Manager**.

- **Software Center**: trovare il collegamento a Software Center nel menu Start di Windows nella cartella **Microsoft Endpoint Manager**.

![Icone del menu Start di Microsoft Endpoint Manager](media/microsoft-endpoint-manager-start-menu.png)

Assicurarsi di aggiornare la documentazione gestita internamente in modo da includere questi nuovi percorsi.

> [!TIP]
> In Windows 10, quando si apre il menu Start, è sufficiente iniziare a digitare il nome per trovare l'icona. Ad esempio, `config` per la console di Configuration Manager e `software` per Software Center.

## <a name="bkmk_infra"></a> Infrastruttura del sito

### <a name="reclaim-sedo-lock"></a>Richiamare il blocco SEDO

<!--4786915-->

A partire da [Current Branch versione 1906](/configmgr/core/plan-design/changes/whats-new-in-version-1906#reclaim-sedo-lock-for-task-sequences), è possibile cancellare il blocco su una sequenza di attività. È possibile cancellare il blocco su qualsiasi oggetto nella console di Configuration Manager.

Per altre informazioni, vedere [Uso della console di Configuration Manager](/configmgr/core/servers/manage/admin-console#bkmk_sedo).

### <a name="extend-and-migrate-on-premises-site-to-microsoft-azure"></a>Estendere ed eseguire la migrazione di un sito locale in Microsoft Azure
<!--3556022-->

Questo nuovo strumento consente di creare a livello di codice macchine virtuali di Azure per Configuration Manager. Consente di installare con impostazioni predefinite ruoli del sito come un server del sito passivo, punti di gestione e punti di distribuzione. Dopo aver convalidato i nuovi ruoli, usarli come sistemi del sito aggiuntivi per ottenere una disponibilità elevata. È anche possibile rimuovere il ruolo del sistema del sito locale e mantenere solo il ruolo VM di Azure.

Per altre informazioni, vedere [Estendere ed eseguire la migrazione di un sito locale in Microsoft Azure](/sccm/core/support/azure-migration-tool).

<!-- ## <a name="bkmk_cloud"></a> Cloud-attached management -->

## <a name="bkmk_da"></a> Desktop Analytics

Per altre informazioni sulle modifiche mensili al servizio cloud Desktop Analytics, vedere [Novità di Desktop Analytics](/configmgr/desktop-analytics/whats-new).

## <a name="bkmk_real"></a> Gestione in tempo reale

### <a name="optimizations-to-the-cmpivot-engine"></a>Ottimizzazioni per il motore CMPivot
<!--3197353-->
Sono state aggiunte alcune ottimizzazioni significative al motore CMPivot che consentono di eseguire il push di una parte maggiore dell'elaborazione nel client ConfigMgr. Le ottimizzazioni riducono drasticamente il carico della CPU del server e della rete necessario per eseguire le query CMPivot. Con queste ottimizzazioni, è ora possibile eseguire operazioni su gigabyte di dati client in tempo reale. Per altre informazioni, vedere [Ottimizzazioni per il motore CMPivot](/sccm/core/servers/manage/cmpivot#bkmk_optimization).

### <a name="additional-cmpivot-entities-and-enhancements"></a>Entità CMPivot aggiuntive e miglioramenti
<!--5410930-->
È stata aggiunta una serie di nuove entità CMPivot e sono stati introdotti miglioramenti alle entità per facilitare l'individuazione e la risoluzione dei problemi. Per eseguire una query sono state incluse le entità seguenti:

- Registri eventi di Windows ([WinEvent](/sccm/core/servers/manage/cmpivot#bkmk_WinEvent))
- Contenuto del file ([FileContent](/sccm/core/servers/manage/cmpivot#bkmk_File))
- DLL caricate dai processi ([ProcessModule](/sccm/core/servers/manage/cmpivot#bkmk_ProcessModule))
- Informazioni Azure Active Directory ([AADStatus](/sccm/core/servers/manage/cmpivot#bkmk_AadStatus))
- Stato di Endpoint Protection ([EPStatus](/sccm/core/servers/manage/cmpivot#bkmk_EPStatus))

Questa versione include anche diversi [altri miglioramenti](/sccm/core/servers/manage/cmpivot#bkmk_Other) a CMPivot. Per altre informazioni, vedere l'articolo su [CMPivot a partire dalla versione 1910](/sccm/core/servers/manage/cmpivot#bkmk_cmpivot1910).

## <a name="bkmk_content"></a> Gestione dei contenuti

### <a name="microsoft-connected-cache-support-for-intune-win32-apps"></a>Supporto di Microsoft Connected Cache per le app Win32 di Intune

<!--5032900-->

Quando si abilita Microsoft Connected Cache nei punti di distribuzione di Configuration Manager, questi possono ora essere usati per gestire le app Win32 di Microsoft Intune nei client co-gestiti.

Per altre informazioni, vedere [Microsoft Connected Cache in Configuration Manager](/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune).

> [!NOTE]
> Configuration Manager Current Branch versione 1906 includeva [Cache in rete di Ottimizzazione recapito](/configmgr/core/plan-design/hierarchy/microsoft-connected-cache) (DOINC), un'applicazione installata in Windows Server ancora in fase di sviluppo. A partire dalla versione Current Branch 1910, questa funzionalità è denominata **Microsoft Connected Cache**.
>
> Quando si installa Connected Cache in un punto di distribuzione di Configuration Manager, il traffico del servizio Ottimizzazione recapito viene scaricato nelle origini locali. Connected Cache esegue questa operazione memorizzando nella cache in modo efficiente il contenuto a livello di intervallo di byte.

## <a name="bkmk_client"></a> Gestione dei client

### <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>Includere linee di base di configurazione personalizzate come parte della valutazione dei criteri di conformità
<!--3608345-->

È ora possibile aggiungere la valutazione delle linee di base di configurazione personalizzate come regola di valutazione dei criteri di conformità. Quando si crea o si modifica una linea di base di configurazione, è disponibile l'opzione **Valuta questa baseline come parte della valutazione dei criteri di conformità**. Quando si aggiunge o si modifica una regola dei criteri di conformità, è disponibile una nuova condizione denominata **Includi le baseline configurate in una valutazione dei criteri di conformità**.

Per i dispositivi con co-gestione, e quando si configura Intune per acquisire i risultati della valutazione della conformità di Configuration Manager come parte dello stato di conformità generale, queste informazioni vengono inviate ad Azure Active Directory. È quindi possibile usarlo per l'accesso condizionale alle risorse di Office 365.  

Per altre informazioni, vedere [Includere linee di base di configurazione personalizzate come parte della valutazione dei criteri di conformità](/sccm/compliance/deploy-use/create-configuration-baselines#bkmk_CAbaselines).

### <a name="enable-user-policy-for-windows-10-enterprise-multi-session"></a>Abilitare i criteri utente per Windows 10 Enterprise multisessione

<!--4737447-->

Configuration Manager Current Branch versione 1906 ha introdotto il supporto per [Desktop virtuale Windows](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#windows-virtual-desktop). Questo ambiente di Microsoft Azure supporta diverse versioni del sistema operativo, alcune delle quali consentono più sessioni utente attive simultanee. Ad esempio, Windows 10 Enterprise multisessione.

Se in questi dispositivi multisessione è necessario usare criteri utente e si accettano le potenziali conseguenze sulle prestazioni, è ora possibile configurare un'impostazione client per abilitare i criteri utente. Nel gruppo **Criteri client** configurare l'impostazione seguente: **Abilita i criteri utente per più sessioni utente**.

Per altre informazioni, vedere [Come configurare le impostazioni client](/configmgr/core/clients/deploy/configure-client-settings).


<!-- ## <a name="bkmk_comgmt"></a> Co-management -->


## <a name="bkmk_app"></a> Gestione delle applicazioni

### <a name="deploy-microsoft-edge-version-77-and-later"></a>Distribuire Microsoft Edge versione 77 e successive
<!--4561024-->
Il nuovo Microsoft Edge è disponibile per le aziende. È ora possibile distribuire Microsoft Edge, versione 77 e successive, agli utenti della propria organizzazione. Gli amministratori possono scegliere il canale Beta o Dev, insieme a una versione del client Microsoft Edge da distribuire.

Per altre informazioni, vedere [Distribuire Microsoft Edge versione 77 e successive](/sccm/apps/deploy-use/deploy-edge).

### <a name="improvements-to-application-groups"></a>Miglioramenti ai gruppi di applicazioni

<!--4760058-->

A partire da Current Branch versione 1906, è possibile creare un gruppo di applicazioni da inviare a una raccolta di dispositivi come singola distribuzione. Questa versione introduce un miglioramento a questa funzionalità:

- Gli utenti possono **disinstallare** il gruppo di app in Software Center.

- È possibile distribuire un gruppo di app in una **raccolta utenti**.

Per altre informazioni di carattere generale, vedere [Creare gruppi di applicazioni](/configmgr/apps/deploy-use/create-app-groups).


## <a name="bkmk_osd"></a> Distribuzione del sistema operativo

### <a name="improvements-to-the-task-sequence-editor"></a>Miglioramenti all'editor delle sequenze di attività

- **Ricerca nell'editor delle sequenze di attività**<!--4621085-->: Se si ha una sequenza di attività di grandi dimensioni con molti gruppi e passaggi, può essere difficile individuare passaggi specifici. È ora possibile eseguire ricerche nell'editor delle sequenze di attività. Questa azione consente di individuare più rapidamente i passaggi in una sequenza di attività.

- **Copiare e incollare le condizioni della sequenza di attività**<!--4621098-->: Se si vogliono riutilizzare le condizioni da un passaggio della sequenza di attività a un altro, è ora possibile copiare e incollare le condizioni nell'editor.

Per altre informazioni, vedere il nuovo articolo su come [usare l'editor delle sequenze di attività](/configmgr/osd/understand/task-sequence-editor).

### <a name="task-sequence-performance-improvements---power-plans"></a>Miglioramenti delle prestazioni della sequenza delle attività - Combinazioni per il risparmio di energia

<!--3555926-->

È ora possibile eseguire una sequenza di attività con la combinazione per il risparmio di energia per prestazioni elevate. Questa opzione migliora la velocità complessiva della sequenza di attività. Configura Windows in modo da usare la combinazione per il risparmio di energia per prestazioni elevate predefinita, che offre prestazioni massime a scapito di un consumo di energia superiore.

Per altre informazioni, vedere [Miglioramenti delle prestazioni per le combinazioni per il risparmio di energia](/configmgr/osd/deploy-use/manage-task-sequences-to-automate-tasks#bkmk_perf).

### <a name="task-sequence-download-on-demand-over-the-internet"></a>Download della sequenza di attività su richiesta tramite Internet

<!--3601238-->

È ora possibile usare la sequenza di attività per distribuire l'aggiornamento sul posto di Windows 10 tramite Cloud Management Gateway (CMG). Prima di avviare la sequenza di attività, tuttavia, è necessario che la distribuzione scarichi tutto il contenuto in locale.

A partire da questa versione, il motore della sequenza di attività può scaricare pacchetti su richiesta da un servizio CMG abilitato per il contenuto o da un punto di distribuzione cloud. Questa modifica offre ulteriore flessibilità con le distribuzioni di aggiornamento sul posto di Windows 10 ai dispositivi basati su Internet.

Per altre informazioni, vedere [Distribuire l'aggiornamento sul posto di Windows 10 mediante Cloud Management Gateway](/configmgr/osd/deploy-use/deploy-a-task-sequence#deploy-windows-10-in-place-upgrade-via-cmg).

### <a name="improvements-to-os-deployment"></a>Miglioramenti della distribuzione del sistema operativo

Questa versione include i miglioramenti seguenti alla distribuzione del sistema operativo:

#### <a name="boot-image-keyboard-layout"></a>Layout della tastiera per l'immagine d'avvio

<!--4910348-->

Configurare il layout predefinito della tastiera per un'immagine d'avvio. Nella scheda **Personalizzazione** di un'immagine di avvio usare la nuova opzione per **impostare il layout predefinito della tastiera in WinPE**. Se si seleziona una lingua diversa da en-US, Configuration Manager include ancora en-US nelle impostazioni locali di input disponibili. Nel dispositivo, il layout iniziale della tastiera corrisponde alle impostazioni locali selezionate, ma l'utente può passare a en-US se necessario.

Per altre informazioni, vedere [Manage boot images](/configmgr/osd/get-started/manage-boot-images#customization) (Gestire le immagini d'avvio).

#### <a name="import-a-single-index-of-an-os-upgrade-package"></a>Importare un singolo indice di un pacchetto di aggiornamento del sistema operativo

<!--4931110-->

Quando si importa un pacchetto di aggiornamento del sistema operativo, è possibile **estrarre un indice dell'immagine specifico dal file install.wim del pacchetto di aggiornamento selezionato**. Questo comportamento è simile a quello delle [immagini del sistema operativo](/configmgr/osd/get-started/manage-operating-system-images#BKMK_AddOSImages), con la differenza che sovrascrive il file install.wim esistente nel pacchetto di aggiornamento del sistema operativo. Estrae l'indice dell'immagine in una posizione temporanea e quindi lo sposta nella directory di origine originale.

Per altre informazioni, vedere [Gestire i pacchetti di aggiornamento del sistema operativo](/configmgr/osd/get-started/manage-operating-system-upgrade-packages#BKMK_AddOSUpgradePkgs).

#### <a name="output-the-results-of-a-run-command-line-step-to-a-variable-during-a-task-sequence"></a>Output dei risultati di un passaggio Esegui riga di comando in una variabile durante una sequenza di attività

<!--user story 4977616/bug 4798352-->

Il passaggio **Esegui riga di comando** include ora un'opzione per l'**output in una variabile della sequenza di attività**. Quando si abilita questa opzione, la sequenza di attività salva l'output del comando in una variabile della sequenza di attività personalizzata specificata.

Per altre informazioni, vedere [Esegui riga di comando](/configmgr/osd/understand/task-sequence-steps#BKMK_RunCommandLine).

#### <a name="improvements-to-task-sequence-debugger"></a>Miglioramenti al debugger delle sequenze di attività

Questa versione include i miglioramenti seguenti al debugger delle sequenze di attività:

- Usare la nuova variabile della sequenza di attività **TSDebugOnError** per avviare automaticamente il debugger quando la sequenza di attività restituisce un errore.<!-- 5012536 -->

- Se si crea un punto di interruzione nel debugger e quindi la sequenza di attività riavvia il computer, il debugger mantiene i punti di interruzione dopo il riavvio.<!-- 5012509 -->

Per altre informazioni, vedere [Debugger delle sequenze di attività](/configmgr/osd/deploy-use/debug-task-sequence) e [Variabili della sequenza di attività - TSDebugOnError](/configmgr/osd/understand/task-sequence-variables#TSDebugOnError).

#### <a name="improved-language-support-in-task-sequence"></a>Supporto delle lingue migliorato nella sequenza di attività

<!--5411057, 5138936-->

Questa versione consente un controllo maggiore della configurazione della lingua durante la distribuzione del sistema operativo. Se si stanno già applicando queste impostazioni della lingua, la modifica consente di semplificare la sequenza di attività di distribuzione del sistema operativo. Invece di usare più passaggi per lingua o script distinti, usare un'istanza per ogni lingua del passaggio **Applica impostazioni Windows** predefinito con una condizione per tale lingua.

Usare il passaggio **Applica impostazioni Windows** della sequenza di attività per configurare le nuove impostazioni seguenti:

- Impostazioni locali per l'input (layout di tastiera predefinito)
- Impostazioni locali di sistema
- Lingua dell'interfaccia utente
- Fallback della lingua dell'interfaccia utente
- Impostazioni locali dell'utente

Per altre informazioni, vedere [Applicare le impostazioni Windows](/configmgr/osd/understand/task-sequence-steps#BKMK_ApplyWindowsSettings).

#### <a name="new-variable-for-windows-10-in-place-upgrade"></a>Nuova variabile per l'aggiornamento sul posto di Windows 10

<!--4680263-->

Per risolvere i problemi di temporizzazione con la sequenza di attività di aggiornamento sul posto di Windows 10 nei dispositivi con prestazioni elevate al termine dell'installazione di Windows, è ora possibile impostare la nuova variabile della sequenza di attività **SetupCompletePause**. Quando si assegna un valore in secondi a questa variabile, il processo di installazione di Windows ritarda questo intervallo di tempo prima di avviare la sequenza di attività. Questo timeout fornisce al client di Configuration Manager altro tempo per l'inizializzazione.

Per altre informazioni, vedere [Variabili della sequenza di attività - SetupCompletePause](/configmgr/osd/understand/task-sequence-variables#SetupCompletePause).

<!-- ## <a name="bkmk_userxp"></a> Software Center -->

## <a name="bkmk_sum"></a> Aggiornamenti software

### <a name="additional-options-for-third-party-update-catalogs"></a>Opzioni aggiuntive per i cataloghi di aggiornamenti di terze parti
<!--4469002-->
Sono ora disponibili controlli più granulari sulla sincronizzazione dei cataloghi di aggiornamenti di terze parti. A partire da Configuration Manager versione 1910, è possibile configurare la pianificazione della sincronizzazione per ogni catalogo in modo indipendente. Quando si usano cataloghi che includono aggiornamenti suddivisi per categorie, è possibile configurare la sincronizzazione in modo da includere solo determinate categorie di aggiornamenti per evitare di sincronizzare l'intero catalogo. Con i cataloghi suddivisi per categorie, quando si è certi che si distribuirà una categoria, è possibile configurarla per il download e la pubblicazione automatici in WSUS.

Per altre informazioni, vedere [Abilitare gli aggiornamenti di terze parti](/sccm/sum/deploy-use/third-party-software-updates#bkmk_1910).

### <a name="use-delivery-optimization-for-all-windows-updates"></a>Usare Ottimizzazione recapito per tutti gli aggiornamenti di Windows
<!--4699118-->
In precedenza, la funzionalità Ottimizzazione recapito era disponibile solo per gli aggiornamenti rapidi. Con Configuration Manager versione 1910 è ora possibile usare Ottimizzazione recapito per la distribuzione di tutti i contenuti di Windows Update per i client che eseguono Windows 10 versione 1709 o successiva.

Per altre informazioni, vedere:
- [Ottimizzare il recapito degli aggiornamenti di Windows 10](/sccm/sum/deploy-use/optimize-windows-10-update-delivery#bkmk_DO-1910)
- [Impostazioni client per gli aggiornamenti software](/sccm/core/clients/deploy/about-client-settings#software-updates)
- [Impostazioni client per Ottimizzazione recapito](/sccm/core/clients/deploy/about-client-settings#delivery-optimization)

### <a name="additional-software-update-filter-for-adrs"></a>Filtro di aggiornamento software aggiuntivo per le regole di distribuzione automatica
<!--4852033-->
È ora possibile usare **Distribuito** come filtro di aggiornamento per le regole di distribuzione automatica. Questo filtro consente di identificare i nuovi aggiornamenti che potrebbero dover essere distribuiti nelle raccolte pilota o di test.

Per altre informazioni, vedere [Distribuire automaticamente gli aggiornamenti software](/sccm/sum/deploy-use/automatically-deploy-software-updates#bkmk_adr-process)

## <a name="bkmk_o365"></a> Gestione di Office


### <a name="office-365-proplus-pilot-and-health-dashboard"></a>Dashboard sull'integrità e la distribuzione pilota di Office 365 ProPlus
<!--4488272, 4488301-->

Il **dashboard sull'integrità e la distribuzione pilota di Office 365 ProPlus** consente di pianificare, pilotare e distribuire Office 365 ProPlus. Il dashboard fornisce informazioni dettagliate sull'integrità per i dispositivi con Office 365 ProPlus per identificare i possibili problemi che potrebbero influire sui piani di distribuzione. Il **dashboard sull'integrità e la distribuzione pilota di Office 365 ProPlus** fornisce raccomandazioni per i dispositivi della distribuzione pilota in base all'inventario dei componenti aggiuntivi. Per altre informazioni, vedere [Uso del dashboard sull'integrità e la distribuzione pilota di Office 365 ProPlus](/sccm/sum/deploy-use/office-365-dashboard#bkmk_pilot).

## <a name="bkmk_protect"></a> Protezione

### <a name="bitlocker-management"></a>Gestione di BitLocker

<!--3601034-->

Configuration Manager offre ora le funzionalità di gestione seguenti per Crittografia unità BitLocker:

- Distribuzione del client di BitLocker nei dispositivi Windows gestiti
- Gestione dei criteri di crittografia del dispositivo
- Report di conformità
- Sito Web di amministrazione e monitoraggio per il recupero delle chiavi
- Portale self-service degli utenti

Per altre informazioni, vedere [Pianificare la gestione di BitLocker](/configmgr/protect/plan-design/bitlocker-management).

## <a name="bkmk_admin"></a> Console di Configuration Manager

### <a name="view-active-consoles-and-message-administrators-through-console-connections"></a>Visualizzare le console attive e inviare un messaggio agli amministratori tramite Connessioni di console
<!--4923997-->
Sono stati apportati i miglioramenti seguenti per **Connessioni di console**:

- Possibilità di inviare messaggi ad altri amministratori di Configuration Manager tramite Microsoft Teams.
- La colonna **Last Console Heartbeat** (Ultimo heartbeat colonna) ha sostituito la colonna **Ora dell'ultima connessione**.
  - Una console aperta in primo piano invia un heartbeat ogni 10 minuti per aiutare a determinare quali connessioni della console sono attualmente attive.

Per altre informazioni, vedere [Visualizzare le console connesse di recente](/sccm/core/servers/manage/admin-console#bkmk_viewconnected) e [Inviare messaggi agli amministratori](/sccm/core/servers/manage/admin-console#bkmk_message).

### <a name="client-diagnostics-actions"></a>Azioni di diagnostica client

<!--4433455-->

Sono disponibili nuove azioni del dispositivo per **Diagnostica client** nella console di Configuration Manager:

- **Abilita la registrazione dettagliata**: modificare il livello di registrazione per il componente CCM da globale a dettagliata e abilitare la registrazione debug.
- **Disabilita la registrazione dettagliata**: modificare il livello di registrazione da globale a predefinita e disabilitare la registrazione debug.

Per altre informazioni, vedere [Diagnostica client](/sccm/core/clients/manage/client-notification#client-diagnostics).

### <a name="improvements-to-console-search"></a>Miglioramenti alla ricerca nella console
<!--4640570-->

Questa versione include i miglioramenti seguenti alla funzionalità di ricerca nella console di Configuration Manager:

- È ora possibile usare l'opzione di ricerca **Tutte le sottocartelle** dai nodi **Pacchetti driver** e **Query**.<!--2841181,5424892-->

- Quando una ricerca restituisce più di 1000 risultati, è ora possibile selezionare il pulsante **OK** sulla barra di notifica per visualizzare altri risultati.<!--4640570-->

## <a name="other-updates"></a>Altri aggiornamenti

Per altre informazioni sulle modifiche apportate ai cmdlet di Windows PowerShell per Configuration Manager, vedere le [note sulla versione 1910 di PowerShell](https://docs.microsoft.com/powershell/sccm/1910-release-notes?view=sccm-ps).

<!--
As of this version, the following features are no longer pre-release:
- [SMS Provider administration service](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_admin-service)
- [Device Guard management](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)

Aside from new features, this release also includes additional changes such as bug fixes. For more information, see [Summary of changes in Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4514258).

The following update rollup (4517869) is available in the console starting on October 1, 2019: [Update rollup for Configuration Manager current branch, version 1906](https://support.microsoft.com/help/4517869).

-->

<!--
### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |

> [!Note]  
> Starting in version 1902, in-console hotfixes now have supersedence relationships. For more information, see [Supersedence for in-console hotfixes](/sccm/core/servers/manage/updates#bkmk_supersede).
-->

## <a name="next-steps"></a>Passaggi successivi

La versione 1910 viene attualmente rilasciata per l'anello di aggiornamento anticipato. Per installare questo aggiornamento, è necessario acconsentire esplicitamente. Per altre informazioni, vedere [Anello di aggiornamento anticipato](/sccm/core/servers/manage/checklist-for-installing-update-1910#early-update-ring).
<!--As of August 16, 2019, version 1906 is globally available for all customers to install.-->

Al momento di installare questa versione, vedere [Installazione degli aggiornamenti per Configuration Manager](/sccm/core/servers/manage/updates) ed [Elenco di controllo per l'installazione dell'aggiornamento 1910](/sccm/core/servers/manage/checklist-for-installing-update-1910).

> [!TIP]  
> Per installare un nuovo sito, usare una versione base di Configuration Manager.  
>
> Sono disponibili altre informazioni su:
>
> - [Installing new sites](/sccm/core/servers/deploy/install/installing-sites) (Installare nuovi siti)  
> - [Baseline and update versions](/sccm/core/servers/manage/updates#bkmk_Baselines) (Versioni di base e di aggiornamento)  

Per problemi noti e importanti, vedere [Note sulla versione](/sccm/core/servers/deploy/install/release-notes).

Dopo aver aggiornato un sito, vedere anche [Elenco di controllo post-aggiornamento](/sccm/core/servers/manage/checklist-for-installing-update-1910#post-update-checklist).
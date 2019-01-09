---
title: Novità della versione 1810
titleSuffix: Configuration Manager
description: Informazioni dettagliate sulle modifiche e sulle nuove funzionalità introdotte nella versione 1810 di Configuration Manager (Current Branch).
ms.date: 12/20/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 050cf81a99f29d24cad6eb13e691e332174627c3
ms.sourcegitcommit: 54e5786875c4e5f5c1b54e38ed59e96344faf9b4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/02/2019
ms.locfileid: "53818022"
---
# <a name="whats-new-in-version-1810-of-configuration-manager-current-branch"></a>Novità della versione 1810 di Configuration Manager (Current Branch)

*Si applica a: System Center Configuration Manager (Current Branch)*

L'aggiornamento 1810 per Configuration Manager (Current Branch) è disponibile come aggiornamento nella console. Applicare questo aggiornamento ai siti con la versione 1710, 1802 o 1806. <!-- baseline only statement: When installing a new site, it's also available as a baseline version.-->

Esaminare sempre l'elenco di controllo più recente per installare questo aggiornamento. Per altre informazioni, vedere [Elenco di controllo per l'installazione dell'aggiornamento 1810](/sccm/core/servers/manage/checklist-for-installing-update-1810). Dopo aver aggiornato un sito, vedere anche [Elenco di controllo post-aggiornamento](/sccm/core/servers/manage/checklist-for-installing-update-1810#post-update-checklist).

> [!Note]  
> Questo articolo elenca tutte le funzionalità importanti di questa versione al momento. Tuttavia, non tutte le sezioni sono ancora collegate al contenuto aggiornato con maggiori informazioni sulle nuove funzionalità. Continuare a controllare questa pagina con regolarità per verificare la disponibilità di aggiornamenti. Le modifiche sono contrassegnate con il tag ***[Aggiornato]***. Questa nota sarà rimossa nella versione finale del contenuto.  

A parte le nuove funzionalità, questa versione include anche ulteriori modifiche, ad esempio correzioni di bug. Per altre informazioni, vedere [Riepilogo delle modifiche in Configuration Manager Current Branch, versione 1810](https://support.microsoft.com/help/4482169).

<!--
For more information on changes to the Windows PowerShell cmdlets for Configuration Manager, see [PowerShell 1810 Release Notes](https://docs.microsoft.com/powershell/sccm/1810_release_notes?view=sccm-ps).

The following additional updates to this release are also now available:
- [Update rollup for Configuration Manager current branch, version 1810](https://support.microsoft.com/help/4462978)
-->

> [!Important]  
> Per sfruttare i vantaggi delle nuove funzionalità di Configuration Manager, aggiornare prima di tutto i clienti alla versione più recente. Anche se le nuove funzionalità vengono visualizzate nella console di Configuration Manager quando si esegue l'aggiornamento del sito e della console, lo scenario completo risulta funzionante solo dopo l'aggiornamento alla versione più recente del client.

Questo articolo offre un riepilogo delle modifiche e delle nuove funzionalità di Configuration Manager versione 1810.  



## <a name="bkmk_deprecated"></a> Funzionalità e sistemi operativi deprecati

Per conoscere le modifiche relative al supporto prima che siano implementate, vedere [Elementi rimossi e deprecati](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

A partire dal 14 agosto 2018, la funzionalità di gestione ibrida dei dispositivi mobili è deprecata. Per altre informazioni, vedere [Informazioni sulla gestione di dispositivi mobili ibrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  

Il supporto di System Center Endpoint Protection (SCEP) per Mac e Linux (tutte le versioni) termina il 31 dicembre 2018. La disponibilità di nuove definizioni di virus per SCEP per Mac e SCEP per Linux potrebbe essere sospesa alla fine del supporto. Per altre informazioni, vedere il [post del blog sulla fine del supporto](https://go.microsoft.com/fwlink/?linkid=870182).

Le distribuzioni classiche del servizio in Azure sono ora deprecate in Configuration Manager. Iniziare a usare le distribuzioni di Azure Resource Manager per il gateway di gestione cloud e il punto di distribuzione cloud. Per altre informazioni, vedere [Pianificare il gateway di gestione cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).
<!--
Version 1810 drops support for the following products:
-->



## <a name="bkmk_infra"></a> Infrastruttura del sito

### <a name="support-for-windows-server-2019"></a>Supporto per Windows Server 2019
<!--1359195--> Configuration Manager ora supporta Windows Server 2019 e Windows Server versione 1809 come sistemi del sito. 

Per altre informazioni, vedere [Sistemi operativi supportati per i server dei sistemi del sito](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).


### <a name="hierarchy-support-for-site-server-high-availability"></a>Supporto della gerarchia per la disponibilità elevata del server del sito
<!--1358224--> I siti di amministrazione centrale e i siti primari figlio ora possono avere un altro server del sito in modalità passiva. 

<!--For more information, see [Site server high availability](/sccm/core/servers/deploy/configure/site-server-high-availability).-->


### <a name="improvements-to-setup-prerequisites"></a>Miglioramenti dei prerequisiti nel programma di installazione

Quando si installa la versione 1810 o si esegue l'aggiornamento a questa versione, il programma di installazione di Configuration Manager ora include o migliora i controlli dei prerequisiti seguenti:

- **Riavvio del sistema in sospeso**: il controllo di questo prerequisito è ora più resiliente. Controlla chiavi del Registro di sistema aggiuntive per le funzionalità di Windows. Per altre informazioni, vedere [Riavvio del sistema in sospeso](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#pending-system-restart). <!--SCCMDocs-pr issue 3010-->  

- **Pulizia rilevamento modifiche di SQL**: un nuovo controllo se il database del sito ha un backlog di dati di rilevamento modifiche di SQL. Per altre informazioni, inclusa una procedura per verificare e cancellare il backlog, vedere [SQL change tracking cleanup](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#bkmk_changetracking) (Pulizia rilevamento modifiche di SQL). <!--SCCMDocs-pr issue 3023-->  

- **Versione di SQL Native Client**: questo controllo prerequisiti è aggiornato per le versioni di SQL Native Client che supportano TLS 1.2. La versione minima è [SQL 2012 SP4](https://www.microsoft.com/download/details.aspx?id=50402). Per altre informazioni, vedere [Versione di SQL Native Client](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#sql-native-client). <!--SCCMDocs-pr issue 3094-->  

- **Sistema del sito nel nodo del cluster Windows**: Il processo di installazione di Configuration Manager non blocca più l'installazione del ruolo del server del sito in un computer con il ruolo Windows per il clustering di failover. Poiché SQL Always On richiede questo ruolo, non era possibile in precedenza inserire il database del sito nel server del sito. Con questa modifica, è possibile creare un sito a disponibilità elevata con un minor numero di server usando SQL Always On e un server del sito in modalità passiva. Per altre informazioni, vedere [Cluster di failover Windows](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#windows-failover-cluster). <!--1359132-->  




### <a name="new-permission-for-client-notification-actions"></a>Nuova autorizzazione per le azioni di notifica client
<!--SCCMDocs-pr issue #2972--> Per le azioni di notifica client ora è necessaria l'autorizzazione **Invia una notifica alla risorsa** nella classe SMS_Collection. I ruoli predefiniti seguenti hanno questa autorizzazione per impostazione predefinita:
- Amministratore completo  
- Amministratore infrastruttura  

Aggiungere questa autorizzazione ai ruoli personalizzati che devono usare le azioni di notifica client. 

Per altre informazioni, vedere [Client notifications](/sccm/core/clients/manage/client-notification) (Notifiche client).



## <a name="bkmk_content"></a> Gestione dei contenuti

### <a name="new-boundary-group-options"></a>Nuove opzioni del gruppo di limiti
<!--1358749--> Sono ora disponibili le impostazioni aggiuntive seguenti per i gruppi di limiti per offrire maggiore controllo sulla distribuzione di contenuti nell'ambiente:

- **Preferisci i punti di distribuzione rispetto ai peer entro la stessa subnet**: Per impostazione predefinita, il punto di gestione classifica le origini di peer cache in cima all'elenco delle posizioni dei contenuti. Questa impostazione inverte tale priorità per i client che si trovano nella stessa subnet dell'origine di peer cache.  

- **Preferisci i punti di distribuzione cloud rispetto ai punti di distribuzione**: Se è presente una succursale con un collegamento Internet più veloce, è possibile classificare in ordine di priorità i contenuti cloud.  

Per altre informazioni, vedere [Opzioni del gruppo di limiti per download peer](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgoptions).


### <a name="management-insights-rule-for-peer-cache-source-client-version"></a>Regola delle informazioni dettagliate sulla gestione per la versione del client di origine di peer cache
<!-- 1358008 --> Il nodo **Informazioni dettagliate sulla gestione** include una nuova regola per identificare i client che fungono da origine di peer cache, ma non sono stati aggiornati da una versione del client precedente alla 1806. La nuova regola è **Aggiorna le origini di peer cache alla versione più recente del client di Configuration Manager** e fa parte del nuovo gruppo di regole **Manutenzione proattiva**. I client precedenti alla versione 1806 non possono essere usati come origine di peer cache per i client che eseguono la versione 1806 o versioni successive. Selezionare **Intervieni** per aprire una visualizzazione del dispositivo che mostra l'elenco dei client. 

Per altre informazioni, vedere [Informazioni dettagliate sulla gestione](/sccm/core/servers/manage/management-insights).



## <a name="bkmk_client"></a> Gestione dei client

### <a name="new-client-notification-action-to-wake-up-device"></a>Nuova azione di notifica client per la riattivazione del dispositivo
<!--1317364--> È ora possibile riattivare un client dalla console di Configuration Manager anche se il client non si trova nella stessa subnet del server del sito. Se è necessario eseguire attività di manutenzione o query nei dispositivi, i client remoti in stato di sospensione non costituiranno un limite per le operazioni. Il server del sito usa il canale di notifica client per identificare un altro client attivo nella stessa subnet remota. Il client attivo invia quindi una richiesta di riattivazione LAN (Magic Packet).

<!--For more information, see [Plan how to wake up clients](/sccm/core/clients/deploy/plan/plan-wake-up-clients).-->


### <a name="improvements-to-collection-evaluation"></a>Miglioramenti alla valutazione delle raccolte
<!--1358981--> Le modifiche seguenti nel comportamento di valutazione delle raccolte possono migliorare le prestazioni del sito:  
 
- In precedenza, quando si configurava una pianificazione per una raccolta basata su query, il sito continuava a valutare la query indipendentemente dall'impostazione **Pianifica un aggiornamento completo in questa raccolta**. Per disabilitare completamente la pianificazione, era necessario modificare la pianificazione impostando **Nessuno**. Ora il sito cancella la pianificazione quando si disabilita questa impostazione. Per specificare una pianificazione per la valutazione delle raccolte, abilitare l'opzione **Pianifica un aggiornamento completo in questa raccolta**.  

- Non è possibile disabilitare la valutazione delle raccolte predefinite, come **Tutti i sistemi**, ma ora è possibile configurare la pianificazione. Questo comportamento consente di personalizzare questa azione in base agli specifici requisiti aziendali. 

<!--For more information, see [How to create collections](/sccm/core/clients/manage/collections/create-collections).-->


### <a name="improvement-to-client-installation"></a>Miglioramento dell'installazione client
<!--1358840--> Durante l'installazione del client di Configuration Manager, il processo ccmsetup contatta il punto di gestione per individuare i contenuti necessari. Nelle fasi precedenti di questo processo il punto di gestione restituisce solo i punti di gestione del gruppo di limiti corrente del client. Se non è disponibile alcun contenuto, il processo di installazione esegue il fallback per scaricare i contenuti dal punto di gestione. Non è disponibile alcuna opzione per eseguire il fallback ai punti di distribuzione in altri gruppi di limiti che potrebbero avere i contenuti necessari. Il punto di gestione restituisce ora i punti di distribuzione in base alla configurazione del gruppo di limiti. 

Per altre informazioni, vedere [Configurare gruppi di limiti](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_ccmsetup).


### <a name="improvements-to-internet-based-client-setup"></a>Miglioramenti al programma di installazione dei client basati su Internet
<!--1359181-->
<!--move this under co-management?--> Questa versione semplifica ulteriormente il processo di installazione del client di Configuration Manager per i client su Internet. Il sito pubblica informazioni aggiuntive di Azure Active Directory (Azure AD) in Cloud Management Gateway (CMG). Un client aggiunto ad Azure AD ottiene queste informazioni da CMG durante il processo ccmsetup, usando lo stesso tenant a cui viene aggiunto. Questo comportamento semplifica ulteriormente la registrazione dei dispositivi per la co-gestione in un ambiente con più di un tenant di Azure AD. Al momento le uniche due proprietà obbligatorie di ccmsetup sono **CCMHOSTNAME** e **SMSSiteCode**.

<!--For more information, see [Prepare Windows 10 devices for co-management](https://docs.microsoft.com/en-us/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client).-->



## <a name="bkmk_comgmt"></a> Co-gestione

### <a name="required-app-compliance-policy-for-co-managed-devices"></a>Criteri di conformità delle app obbligatori per i dispositivi con co-gestione
<!--1358196--> Definire le regole dei criteri di conformità in Configuration Manager per le applicazioni obbligatorie. Questa valutazione dell'app è inclusa nello stato di conformità generale inviato a Microsoft Intune per i dispositivi con co-gestione.

<!--For more information, see [Co-management for Windows 10 devices](/sccm/core/clients/manage/co-management-overview).-->


### <a name="improvement-to-co-management-dashboard"></a>Miglioramento del dashboard di co-gestione
<!--1358980--> Il dashboard di co-gestione è stato migliorato con informazioni più dettagliate:  

- Il riquadro **Stato di registrazione della co-gestione** include altri stati

- Un nuovo riquadro **Stato della co-gestione** con un grafico a imbuto che visualizza gli stati del processo di registrazione

- Un nuovo riquadro con il conteggio degli **Errori di registrazione**

![Screenshot del dashboard di co-gestione che mostra i quattro riquadri principali](media/1358980-comgmt-dashboard.png)

Per altre informazioni, vedere [Dashboard di co-gestione](/sccm/core/clients/manage/co-management-dashboard).



<!-- ## <a name="bkmk_compliance"></a> Compliance settings -->



## <a name="bkmk_app"></a> Gestione delle applicazioni

### <a name="convert-applications-to-msix"></a>Convertire le applicazioni in MSIX
<!--1359029--> A partire dalla versione 1806, Configuration Manager supporta la distribuzione del nuovo formato di pacchetto di app di Windows 10 (file con estensione msix). È ora possibile convertire le applicazioni Windows Installer (con estensione msi) esistenti nel formato MSIX.

<!--For more information, see [Create Windows applications](/sccm/apps/get-started/creating-windows-applications#bkmk_general).  this might move to a new section for msix-->


### <a name="repair-applications"></a>Ripristinare le applicazioni
<!--1357866--> Specificare una riga di comando di ripristino per i tipi di distribuzione Windows Installer e Programma di installazione dello script. Se si abilita quindi l'opzione nella distribuzione, in Software Center sarà disponibile un nuovo pulsante per **ripristinare** l'applicazione. Quando si configura un'applicazione con un programma di ripristino, gli utenti possono avviare il comando da Software Center. 

Per altre informazioni, vedere [Creare applicazioni](/sccm/apps/deploy-use/create-applications#bkmk_dt-content) e [Distribuire applicazioni](/sccm/apps/deploy-use/deploy-applications#bkmk_deploy-settings).


### <a name="approve-application-requests-via-email"></a>Approvare le richieste dell'applicazione tramite posta elettronica
<!--1321550--> È possibile configurare notifiche tramite posta elettronica per le richieste di approvazione dell'applicazione. Quando un utente richiede un'applicazione, si riceve un messaggio di posta elettronica. Fare clic sui collegamenti nel messaggio di posta elettronica per approvare o rifiutare la richiesta, senza che sia necessario usare la console di Configuration Manager.

Per altre informazioni, vedere [Approvare le applicazioni](/sccm/apps/deploy-use/app-approval).


### <a name="detection-methods-dont-load-windows-powershell-profiles"></a>I metodi di rilevamento non caricano i profili di Windows PowerShell
<!--1359239--> Per i metodi di rilevamento su applicazioni e impostazioni negli elementi di configurazione è possibile usare gli script di Windows PowerShell. Quando questi script vengono eseguiti nei client, il client di Configuration Manager ora chiama PowerShell con il parametro `-NoProfile`. Questa opzione avvia PowerShell senza i profili. 

Un profilo di PowerShell è uno script che viene eseguito all'avvio di PowerShell. Si può creare un profilo di PowerShell per personalizzare l'ambiente e aggiungere elementi specifici della sessione a ogni sessione di PowerShell avviata. 

> [!Note]  
> Questa modifica del comportamento non riguarda gli [script](/sccm/apps/deploy-use/create-deploy-scripts) o [CMPivot](/sccm/core/servers/manage/cmpivot). Entrambe le funzionalità usano già questo parametro di PowerShell.    

<!--For more information, see []().-->


## <a name="bkmk_osd"></a> Distribuzione del sistema operativo

### <a name="task-sequence-support-of-windows-autopilot-for-existing-devices"></a>Supporto della sequenza di attività di Windows Autopilot per i dispositivi esistenti
<!--1358333-->

[Windows Autopilot per i dispositivi esistenti](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) è ora disponibile con Windows 10 Insider Preview versione 1809 o successiva. Questa nuova funzionalità consente di ricreare l'immagine ed eseguire il provisioning di un dispositivo Windows 7 per la [modalità definita dall'utente di Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) usando una singola sequenza di attività nativa di Configuration Manager. 

<!--For more information, see []().--> 


### <a name="specify-the-drive-for-offline-os-image-servicing"></a>Specificare l'unità per l'installazione offline dell'immagine del sistema operativo  
<!--1358924--> Quando si aggiungono aggiornamenti software alle immagini del sistema operativo e pacchetti di aggiornamento del sistema operativo è ora possibile specificare l'unità che verrà usata da Configuration Manager. Questo processo può utilizzare una grande quantità di spazio su disco con i file temporanei, pertanto questa opzione offre la flessibilità di selezionare l'unità da usare. 

Per altre informazioni, vedere [Gestire le immagini del sistema operativo](/sccm/osd/get-started/manage-operating-system-images#bkmk_servicing-drive) o [Gestire i pacchetti di aggiornamento del sistema operativo](/sccm/osd/get-started/manage-operating-system-upgrade-packages#bkmk_servicing-drive).


### <a name="task-sequence-support-for-boundary-groups"></a>Supporto della sequenza di attività per i gruppi di limiti
<!--1359025--> Quando un dispositivo esegue una sequenza di attività e deve acquisire il contenuto, il dispositivo usa ora comportamenti dei gruppi di limiti simili al client di Configuration Manager.   

Per altre informazioni, vedere [Gruppi di limiti](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgr-osd).


### <a name="improvements-to-driver-maintenance"></a>Miglioramenti della manutenzione dei driver
<!--1358270--> I pacchetti driver includono ora campi di metadati aggiuntivi per **Produttore** e **Modello**. Usare questi campi per contrassegnare i pacchetti driver con informazioni utili per la manutenzione generale o per identificare driver precedenti e duplicati che è possibile eliminare.


### <a name="new-task-sequence-variable-for-last-action-name"></a>Nuova variabile della sequenza di attività per il nome dell'ultima azione
<!--SCCMDocs-pr issue #2964--> Insieme alla variabile della sequenza di attività _SMSTSLastActionRetCode, la sequenza di attività imposta anche una nuova variabile **_SMSTSLastActionName**. Questo valore viene anche registrato nel file smsts.log. Questa nuova variabile è utile per la risoluzione dei problemi di una sequenza di attività. Quando un passaggio non riesce, uno script personalizzato può includere il nome del passaggio e il codice restituito.

Per altre informazioni, vedere [Variabili della sequenza di attività](/sccm/osd/understand/task-sequence-variables#SMSTSLastActionName).



<!-- ## <a name="bkmk_userxp"></a> Software Center -->



## <a name="bkmk_sum"></a> Aggiornamenti software

### <a name="phased-deployment-of-software-updates"></a>Distribuzione in più fasi degli aggiornamenti software
<!--1358146--> Creare distribuzioni in più fasi per gli aggiornamenti software. Le distribuzioni in più fasi consentono di orchestrare un'implementazione coordinata e in sequenza del software basata su criteri e gruppi personalizzabili.

Per altre informazioni, vedere [Creare distribuzioni in più fasi](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).


### <a name="improvement-to-maintenance-windows-for-software-updates"></a>Miglioramento delle finestre di manutenzione per gli aggiornamenti software
<!--vso2839307--> Per controllare il comportamento di installazione degli aggiornamenti software nelle finestre di manutenzione, il gruppo **Aggiornamenti software** include l'impostazione client seguente: 

**Consenti l'installazione degli aggiornamenti nella finestra di manutenzione "Tutte le distribuzioni" quando la finestra di manutenzione "Aggiornamento software" è disponibile**

Per impostazione predefinita, questa opzione è **No** per mantenere la coerenza con il comportamento esistente. Impostarla su **Sì** per consentire ai client di usare altre finestre di manutenzione disponibile per installare gli aggiornamenti software.

<!--For more information, see []().-->



## <a name="bkmk_report"></a> Creazione di report

### <a name="improvement-to-lifecycle-dashboard"></a>Miglioramento del dashboard del ciclo di vita
<!--1358702--> Il dashboard del ciclo di vita del prodotto include ora le informazioni per **System Center 2012 Configuration Manager e versioni successive**. 

È disponibile anche un nuovo report denominato **Ciclo di vita 05A - Dashboard Ciclo di vita del prodotto**. Include informazioni simili a quelle offerte dal dashboard nella console.

Per altre informazioni su questo dashboard, vedere [Usare il dashboard del ciclo di vita del prodotto](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard).


### <a name="improvement-to-data-warehouse"></a>Miglioramento del data warehouse
<!--1358870--> È ora possibile sincronizzare un maggior numero di tabelle dal database del sito al data warehouse. Questa modifica consente di creare più report in base ai requisiti aziendali.

Per altre informazioni, vedere [Data warehouse](/sccm/core/servers/manage/data-warehouse).



<!-- ## <a name="bkmk_inv"></a> Inventory -->




<!-- ## <a name="bkmk_protect"></a> Protect devices-->




## <a name="bkmk_admin"></a> Console di Configuration Manager

### <a name="configuration-manager-administrator-authentication"></a>Autenticazione dell'amministratore di Configuration Manager
<!--1357013--> È ora possibile specificare il livello di autenticazione minimo per gli amministratori per l'accesso ai siti di Configuration Manager. Questa funzionalità impone agli amministratori di accedere a Windows con il livello richiesto. Per configurare questa impostazione, trovare la scheda **Autenticazione** in **Impostazioni gerarchia**. 

Per altre informazioni, vedere [Piano per il provider SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_auth).


### <a name="support-center"></a>Support Center
<!--1357489--> Usare Support Center per la risoluzione dei problemi dei client, la visualizzazione dei log in tempo reale o l'acquisizione dello stato di un computer client di Configuration Manager per un'analisi successiva. Support Center è un singolo strumento che riunisce numerosi strumenti di risoluzione dei problemi per gli amministratori. Il programma di installazione di Support Center è disponibile nel server del sito, nella cartella **cd.latest\SMSSETUP\Tools\SupportCenter**.

Per altre informazioni, vedere [Support Center](/sccm/core/support/support-center).


### <a name="management-insights-dashboard"></a>Dashboard delle informazioni dettagliate sulla gestione
<!--1357979-->

Il nodo **Informazioni dettagliate sulla gestione** include ora un dashboard grafico. Questo dashboard visualizza una panoramica degli stati delle regole che rende più semplice visualizzare lo stato di avanzamento. Il dashboard include i riquadri seguenti:

- **Indice informazioni dettagliate sulla gestione**: registra l'avanzamento generale delle regole delle informazioni dettagliate sulla gestione. L'indice è una media ponderata. Le regole critiche hanno maggior valore. Questo indice assegna il minor peso alle regole facoltative.  

- **Gruppi di informazioni dettagliate sulla gestione**: visualizza la percentuale di regole di ogni gruppo.  

- **Priorità delle informazioni dettagliate sulla gestione**: visualizza la percentuale di regole in ordine di priorità.  

- **Tutte le informazioni dettagliate sulla gestione**: tabella delle informazioni dettagliate con priorità e stato.  

![Screenshot del dashboard delle informazioni dettagliate sulla gestione](media/1357979-management-insights-dashboard.png)

Per altre informazioni, vedere [Informazioni dettagliate sulla gestione](/sccm/core/servers/manage/management-insights).


### <a name="improvements-to-cmpivot"></a>Miglioramenti di CMPivot
<!--1359068--> CMPivot include i miglioramenti seguenti:

- Salvataggio delle query **preferite**  

- Nella scheda Riepilogo delle query selezionare il totale dei dispositivi Con errori o Offline e quindi selezionare l'opzione **Crea una raccolta**. 

Per altre informazioni su ulteriori miglioramenti delle prestazioni performance e della risoluzione dei problemi di CMPivot, vedere [Miglioramenti degli script](#bkmk_scripts).

<!--For more information on CMPivot, see [CMPivot](/sccm/core/servers/manage/cmpivot).-->


### <a name="bkmk_scripts"></a> Miglioramenti degli script
<!--1358239--> È ora possibile visualizzare l'output degli script dettagliato in formato JSON non elaborato o strutturato. Questo tipo di formattazione rende più facile leggere e analizzare l'output. 

I miglioramenti seguenti relativi alle prestazioni e alla risoluzione dei problemi riguardano CMPivot e gli script:

- I client aggiornati restituiscono un output inferiore a 80 KB al sito su un canale di comunicazione rapida. Questa modifica migliora le prestazioni di visualizzazione dell'output di script o query.  

- Altri log per la risoluzione dei problemi  

<!--For more information, see the following articles:  

- [Create and run PowerShell scripts from the Configuration Manager console](/sccm/apps/deploy-use/create-deploy-scripts)  

- [CMPivot](/sccm/core/servers/manage/cmpivot)  -->


### <a name="sms-provider-api"></a>API del provider SMS
<!--1321523--> Il provider SMS consente ora l'accesso di interoperabilità con l'API in sola lettura a WMI su HTTPS. Il **provider SMS** viene visualizzato come un ruolo con un'opzione per consentire la comunicazione sul gateway di gestione cloud. Questa impostazione attualmente viene usata per abilitare le approvazioni delle applicazioni tramite posta elettronica da un dispositivo remoto. Per altre informazioni, vedere [Approvare le richieste dell'applicazione tramite posta elettronica ](#approve-application-requests-via-email).



## <a name="bkmk_opmdm"></a> Software MDM locale

### <a name="an-intune-connection-is-no-longer-required-for-on-premises-mdm"></a>Non è più necessaria una connessione a Intune per MDM locale
<!--1359124--> Il prerequisito MDM locale per configurare una sottoscrizione di Microsoft Intune non è più obbligatorio. Per usare questa funzionalità è comunque necessario che l'organizzazione abbia le licenze di Intune. 



## <a name="next-steps"></a>Passaggi successivi

Prima di installare questa versione, vedere [Installazione degli aggiornamenti per Configuration Manager](/sccm/core/servers/manage/updates) ed [Elenco di controllo per l'installazione dell'aggiornamento 1810](/sccm/core/servers/manage/checklist-for-installing-update-1810).

> [!TIP]  
> Per installare un nuovo sito, usare una versione base di Configuration Manager.  
>
>  Sono disponibili altre informazioni su:    
>   - [Installing new sites](/sccm/core/servers/deploy/install/installing-sites) (Installare nuovi siti)  
>   - [Baseline and update versions](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions) (Versioni di base e di aggiornamento)  

Per problemi noti e importanti, vedere [Note sulla versione](/sccm/core/servers/deploy/install/release-notes).

Dopo aver aggiornato un sito, vedere anche [Elenco di controllo post-aggiornamento](/sccm/core/servers/manage/checklist-for-installing-update-1810#post-update-checklist).

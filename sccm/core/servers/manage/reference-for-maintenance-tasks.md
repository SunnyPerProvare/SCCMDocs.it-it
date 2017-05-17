---
title: "Riferimento per le attività di manutenzione | Microsoft Docs"
description: "Leggere le informazioni dettagliate su ogni attività di manutenzione del sito di System Center Configuration Manager in cui le attività sono abilitate per impostazione predefinita."
ms.custom: na
ms.date: 3/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 68dc6acd-5848-47a4-b4c1-ffa40e47890b
caps.latest.revision: 16
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: d94acac84f052a01de9d9c9f65f237c0006c45b8
ms.openlocfilehash: a2d4420c2274a9b1ceb47ffd267849fdb5a55a61
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017


---
# <a name="reference-for-maintenance-tasks-for-system-center-configuration-manager"></a>Informazioni di riferimento per le attività di manutenzione per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo argomento fornisce informazioni dettagliate su ognuna delle attività di manutenzione del sito di System Center Configuration Manager e specifica i tipi di sito in cui un'attività è disponibile. Ogni voce indica anche se l'attività è abilitata o non abilitata per impostazione predefinita. Per informazioni sulla pianificazione e configurazione dei siti per eseguire attività di manutenzione, vedere [Attività di manutenzione per System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md).  

**Backup server sito**: usare questa attività per preparare il ripristino di dati critici. Per ripristinare un sito e il database di Configuration Manager, è possibile creare un backup delle informazioni critiche. Per altre informazioni, vedere [Backup e ripristino per System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md).  

-   **Sito di amministrazione centrale**: abilitato    
-   **Sito primario**: non abilitato    
-   Sito secondario: non disponibile  

**Verifica titolo applicazione con le informazioni di inventario**: usare questa attività per mantenere la coerenza tra i titoli software riportati nell'inventario software e quelli presenti nel catalogo di Asset Intelligence. Per altre informazioni, vedere [Introduzione ad Asset Intelligence in System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

-   **Sito di amministrazione centrale**: abilitato    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Cancella flag di installazione**: usare questa attività per rimuovere il flag installato per i client che non inviano un record dell'individuazione heartbeat durante il **Periodo nuova individuazione client**. Il flag installato impedisce l'installazione push client automatica a un computer che potrebbe avere un client attivo di Configuration Manager.  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: non abilitato    
-   Sito secondario: non disponibile  

**Elimina dati richiesta applicazione obsoleti**: usare questa attività per eliminare le richieste di applicazioni obsolete dal database. Per altre informazioni sulle richieste per le applicazioni, vedere [Creare e distribuire un'applicazione con System Center Configuration Manager](/sccm/apps/get-started/create-and-deploy-an-application).  

-   Sito di amministrazione centrale: non disponibile
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Eliminare la cronologia di download del client obsoleti**: usare questa attività per eliminare i dati della cronologia relativi all'origine dei download usata dai client. Le informazioni sull'origine dei download consentono di popolare il dashboard [Origini dati del client](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).  
-  Sito di amministrazione centrale: non disponibile
-     **Sito primario**: abilitato
-  Sito secondario: non disponibile

**Elimina operazioni client obsolete**: usare questa attività per eliminare tutti i dati obsoleti per le operazioni client dal database del sito. Sono inclusi ad esempio i dati delle notifiche client obsolete o scadute come le richieste di download dei criteri computer o utente e i dati di Endpoint Protection come le richieste da un utente amministratore che i client ricerchino o scarichino le definizioni aggiornate.

-   **Sito di amministrazione centrale**: abilitato    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Elimina cronologia presenze client obsolete**: usare questa attività per eliminare le informazioni sulla cronologia relative allo stato online dei client, registrato tramite notifica client, precedente all'orario specificato. Per altre informazioni sulla notifica client, vedere [Come monitorare i client in System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md).  

-   **Sito di amministrazione centrale**: abilitato   
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Elimina i dati di traffico del gateway di gestione cloud obsoleti**: usare questa attività per eliminare tutti i dati obsoleti relativi al traffico che passa attraverso il [gateway di gestione cloud](/sccm/core/clients/manage/plan-cloud-management-gateway) dal database del sito. Questo include, ad esempio, i dati relativi al numero di richieste, i byte totali delle richieste, i byte totali delle risposte, il numero di richieste non riuscite e il numero massimo di richieste simultanee.  
- **Sito di amministrazione centrale**: abilitato
- **Sito primario**: abilitato
- Sito secondario: non disponibile


**Elimina file raccolti obsoleti**: usare questa attività per eliminare le informazioni obsolete sui file raccolti dal database. Questa attività elimina anche i file raccolti dalla struttura delle cartelle del server del sito nel sito selezionato. Per impostazione predefinita, le cinque copie più recenti dei file raccolti sono archiviate sul server del sito nella directory **Inboxes\sinv.box\FileCol**. Per altre informazioni, vedere [Introduzione all'inventario software in System Center Configuration Manager](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Elimina dati di associazione computer obsoleti**: usare questa attività per eliminare dal database i dati di associazione computer della distribuzione del sistema operativo obsoleti. Queste informazioni vengono usate come parte del completamento dei ripristini dello stato utente. Per altre informazioni sulle associazioni computer, vedere [Gestire lo stato utente in System Center Configuration Manager](../../../osd/get-started/manage-user-state.md).  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Elimina dati di rilevamento eliminazione obsoleti**: usare questa attività per eliminare i dati obsoleti dal database creato dalle visualizzazioni di estrazione. Per impostazione predefinita, le visualizzazioni di estrazione sono disattivate. È possibile abilitarle soltanto mediante Configuration Manager SDK. A meno che le visualizzazioni di estrazione non siano abilitate, per questa attività non sono presenti dati da eliminare.  

-   **Sito di amministrazione centrale**: abilitato    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Elimina record di cancellazione dati dispositivo obsoleto**: usare questa attività per eliminare i dati obsoleti relativi alle azioni di cancellazione dei dispositivi mobili dal database. Per altre informazioni sulla cancellazione dei dispositivi mobili, vedere [Proteggere i dati con cancellazione remota, blocco remoto o reimpostazione passcode usando System Center Configuration Manager](/sccm/mdm/deploy-use/wipe-lock-reset-devices).  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Elimina dispositivi gestiti dal connettore Exchange Server obsoleti**: usare questa attività per eliminare i dati obsoleti relativi ai dispositivi mobili che vengono gestiti tramite il connettore Exchange Server. Tali dati vengono eliminati in base all'intervallo configurato per l'opzione **Ignora dispositivi mobili inattivi da più di (giorni)** sulla scheda **Individuazione** delle proprietà del connettore Exchange Server. Per altre informazioni, vedere [Gestire i dispositivi mobili con System Center Configuration Manager ed Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

-   Sito di amministrazione centrale: non disponibile   
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Elimina dati di individuazione obsoleti**: usare questa attività per eliminare i dati di individuazione obsoleti dal database. Questi dati possono includere i record risultanti dall'individuazione heartbeat, l'individuazione di rete e i metodi di individuazione di Active Directory Domain Services (Sistema, Utente e Gruppo). Quando questa attività viene eseguita in un sito, i dati associati a tale sito vengono eliminati e le modifiche vengono replicate in altri siti. Per informazioni sull'individuazione, vedere [Run discovery for System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md).  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Elimina dati di utilizzo punti di distribuzione obsoleti**: usare questa attività per eliminare dal database i dati obsoleti per i punti di distribuzione che sono archiviati da più tempo rispetto a un momento specificato.  

-   **Sito di amministrazione centrale**: abilitato    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Elimina dati cronologia stato integrità di Endpoint Protection obsoleti**: usare questa attività per eliminare dal database le informazioni di stato obsolete per Endpoint Protection. Per altre informazioni sui dati sullo stato di Endpoint Protection, vedere [Come monitorare Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/monitor-endpoint-protection.md).  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Elimina dispositivi registrati obsoleti**: a partire dall'aggiornamento 1602, questa attività è disabilitata per impostazione predefinita. È possibile usarla per eliminare dal database del sito i dati obsoleti relativi ai dispositivi mobili che non hanno inviato informazioni al sito per un determinato periodo di tempo.

Questa attività si applica ai dispositivi registrati da Microsoft Intune (modalità ibrida) o con la funzionalità di gestione dei dispositivi mobili in locale di Configuration Manager. Per informazioni sui sistemi operativi dei dispositivi registrati da Configuration Manager o Intune, vedere la sezione [Dispositivi mobili registrati con Microsoft Intune](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mobile-devices-enrolled-by-microsoft-intune) dell'argomento [Sistemi operativi supportati per client e dispositivi per System Center Configuration Manager](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: non abilitato    
-   Sito secondario: non disponibile  

**Elimina cronologia inventario obsoleta**: usare questa attività per eliminare dal database i dati di inventario che sono archiviati da più tempo rispetto a un momento specificato. Per informazioni sulla cronologia di inventario, vedere [How to use Resource Explorer to view hardware inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/use-resource-explorer-to-view-hardware-inventory.md) (Come usare Esplora inventario risorse per visualizzare l'inventario hardware in System Center Configuration Manager).  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Elimina dati registro obsoleti**: usare questa attività per eliminare dal database i dati di log obsoleti usati per la risoluzione dei problemi. Questi dati non sono correlati alle operazioni dei componenti di Configuration Manager.  

> [!IMPORTANT]  
> Per impostazione predefinita, questa attività viene eseguita ogni giorno in ogni sito. Su un sito di amministrazione centrale e nei siti primari, l'attività elimina i dati che hanno più di 30 giorni. Quando si usa SQL Server Express su un sito secondario, assicurarsi che questa attività venga eseguita ogni giorno e che elimini i dati non attivi da sette giorni.  

-   **Sito di amministrazione centrale**: abilitato    
-   **Sito primario**: abilitato    
-   **Sito secondario**: abilitato  

**Elimina cronologia attività di notifica obsolete**: usare questa attività per eliminare le informazioni relative alle attività di notifica client dal database del sito quando il database non è stato aggiornato per un determinato periodo. Per altre informazioni sulla notifica client, vedere [Attività di distribuzione client per System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md).  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Elimina dati di riepilogo replica obsoleti**: usare questa attività per eliminare i dati di riepilogo replica obsoleti dal database del sito quando il database non è stato aggiornato per un determinato periodo. Per altre informazioni, vedere la sezione [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) nell'argomento [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) .  

-   **Sito di amministrazione centrale**: abilitato    
-   **Sito primario**: abilitato    
-   **Sito secondario**: abilitato  

**Elimina record passcode obsoleti**: usare questa attività nel sito principale della gerarchia per eliminare i dati obsoleti di reimpostazione dei passcode per i dispositivi Android e Windows Phone. I dati di reimpostazione dei passcode sono crittografati ma non includono il PIN per i dispositivi. Per impostazione predefinita, questa attività è abilitata ed elimina i dati che hanno più di un giorno.  

-   **Sito di amministrazione centrale**: abilitato    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Elimina dati di rilevamento repliche obsoleti**: usare questa attività per eliminare dati obsoleti relativi alla replica di database tra siti di Configuration Manager dal database. Quando si modifica la configurazione di questa attività di manutenzione, le modifiche si applicano ad ogni sito applicabile della gerarchia. Per altre informazioni, vedere la sezione [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) nell'argomento [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) .  

-   **Sito di amministrazione centrale**: abilitato    
-   **Sito primario**: abilitato    
-   **Sito secondario**: abilitato  

**Elimina dati di controllo software obsoleti**: usare questa attività per eliminare dal database i dati obsoleti per la misurazione del software che sono archiviati da più tempo rispetto a un momento specificato. Per altre informazioni, vedere [Controllo del software in System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Elimina dati di riepilogo di controllo software obsoleti**: usare questa attività per eliminare dal database i dati di riepilogo obsoleti del controllo del software che sono archiviati da più tempo rispetto a un momento specificato. Per altre informazioni, vedere [Controllo del software in System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Elimina messaggi di stato obsoleti**: usare questa attività per eliminare dal database i dati dei messaggi di stato obsoleti come configurati nelle regole di filtro dello stato. Per informazioni, vedere la sezione Configurare il sistema di stato di Configuration Manager dell'argomento [Usare gli avvisi e il sistema di stato per System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

-   **Sito di amministrazione centrale**: abilitato    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Elimina dati sulle minacce obsoleti**: usare questa attività per eliminare dal database i dati sulle minacce obsoleti di Endpoint Protection che sono archiviati da più tempo rispetto a un momento specificato. Per informazioni su Endpoint Protection, vedere [Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Elimina computer sconosciuti obsoleti**: usare questa attività per eliminare le informazioni relative ai computer sconosciuti dal database del sito quando il database non viene aggiornato per un determinato periodo. Per altre informazioni, vedere [Operazioni preliminari alle distribuzioni in computer sconosciuti in System Center Configuration Manager](../../../osd/get-started/prepare-for-unknown-computer-deployments.md).  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Elimina dati di affinità utente dispositivo obsoleti**: usare questa attività per eliminare dal database i dati di affinità utente-dispositivo obsoleti. Per altre informazioni, vedere [Collegare utenti e dispositivi mediante l'affinità utente dispositivo in System Center Configuration Manager](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Elimina i record dei pacchetti di registrazione in blocco di MDM scaduti**: usare questa attività per eliminare i certificati di registrazione in blocco precedenti e i profili corrispondenti dopo la scadenza del certificato di registrazione. Per altre informazioni, vedere [Creare i profili certificato](/sccm/protect/deploy-use/create-certificate-profiles).
-   **Sito di amministrazione centrale**: abilitato
-   **Sito primario**: abilitato
-   Sito secondario: non disponibile

**Elimina dati di individuazione client non attivi**: usare questa attività per eliminare dal database i dati di individuazione per i client non attivi. I client sono contrassegnati come non attivi in base a configurazioni relative allo stato client oppure quando riportano il flag obsoleto.

Questa attività funziona solo nelle risorse che sono client di Configuration Manager. È diversa dall'attività **Elimina dati di individuazione obsoleti** che elimina qualsiasi record dei dati di individuazione obsoleti. Quando questa attività viene eseguita su un sito, rimuove i dati dal database da tutti i siti di una gerarchia. Per ulteriori informazioni, vedere [How to configure client status in System Center Configuration Manager](../../../core/clients/deploy/configure-client-status.md).  

> [!IMPORTANT]  
> Quando abilitata, configurare questa attività in modo che venga eseguita con un intervallo maggiore rispetto a **Individuazione heartbeat**. Questa operazione abilita i client attivi all'invio di un record di Individuazione heartbeat per contrassegnare il record client come attivo e impedirne così l'eliminazione da parte dell'attività.  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: non abilitato    
-   Sito secondario: non disponibile  

**Elimina avvisi obsoleti**: usare questa attività per eliminare dal database gli avvisi scaduti che sono archiviati da più tempo rispetto a un momento specificato. Per ulteriori informazioni, vedere [Use alerts and the status system for System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

-   **Sito di amministrazione centrale**: abilitato    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Elimina dati di individuazione client obsoleti**: usare questa attività per eliminare i record client obsoleti dal database. Un record contrassegnato come obsoleto è stato in genere sostituito da un record più recente per lo stesso client. Il record più recente diventa il record corrente del client. Per informazioni sull'individuazione, vedere [Run discovery for System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md).  

> [!IMPORTANT]  
> Quando abilitata, configurare questa attività in modo che venga eseguita con un intervallo maggiore rispetto a Individuazione heartbeat. Il client viene quindi abilitato per l'invio di un record dell'individuazione heartbeat che imposta correttamente lo stato obsoleto.  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: non abilitato    
-   Sito secondario: non disponibile  

**Elimina siti e subnet di individuazione foresta obsoleti**: usare questa attività per eliminare i dati relativi ai siti, alle subnet e ai domini di Active Directory che sono stati individuati dal metodo di individuazione foresta Active Directory negli ultimi 30 giorni. Questa operazione rimuove i dati di individuazione, ma non influisce sui limiti creati da tali dati. Per altre informazioni, vedere [Run discovery for System Center Configuration Manager](../../../core/servers/deploy/configure/run-discovery.md).  

-   **Sito di amministrazione centrale**: abilitato    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Elimina i record sullo stato di distribuzione del client orfano**: usare questa attività per ripulire periodicamente la tabella contenente le informazioni sullo stato di distribuzione dei client. Questa attività elimina i record associati a dispositivi obsoleti o non autorizzati.  
-   **Sito di amministrazione centrale**: abilitato    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile

**Elimina revisioni applicazioni non utilizzate**: usare questa attività per eliminare le revisioni applicazione a cui non viene più fatto riferimento. Per altre informazioni, vedere [Come rivedere e sostituire le applicazioni in System Center Configuration Manager](../../../apps/deploy-use/revise-and-supersede-applications.md).  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Valuta membri raccolta**: configurare Valutazione appartenenza alla raccolta come componente del sito. Per informazioni sui componenti del sito, vedere [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Esegui monitoraggio chiavi**: usare questa attività per monitorare l'integrità delle chiavi primarie del database di Configuration Manager. Una chiave primaria è una colonna o combinazione di colonne che identifica in modo univoco una riga e la distingue dalle altre righe di una tabella di database di Microsoft SQL Server.  

-   **Sito di amministrazione centrale**: abilitato    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Ricompila indici**: usare questa attività per ricompilare gli indici del database di Configuration Manager. Un indice è una struttura di database creata in una tabella di database per velocizzare il recupero dei dati. Ad esempio, la ricerca in una colonna indicizzata è spesso molto più veloce rispetto alla ricerca in una colonna non indicizzata.

Per migliorare le prestazioni, gli indici del database di Configuration Manager vengono aggiornati di frequente, in modo che rimangano sincronizzati con i dati costantemente modificati archiviati nel database. Questa attività crea indici sulle colonne di database univoche almeno al 50%, elimina gli indici su colonne la cui univocità è inferiore al 50% e ricompila tutti gli indici esistenti che soddisfano i criteri di univocità dei dati.  

-   **Sito di amministrazione centrale**: non abilitato    
-   **Sito primario**: non abilitato    
-   **Sito secondario**: non abilitato  

**Riepiloga dati software installato**: usare questa attività per riepilogare i dati per il software installato da più record in un unico record generale. L'attività di riepilogo dei dati può ridurre la quantità di dati memorizzati nel database di Configuration Manager. Per altre informazioni, vedere [Introduzione all'inventario software in System Center Configuration Manager](../../clients/manage/inventory\introduction-to-software-inventory.md).  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Riepiloga dati utilizzo file di controllo software**: usare questa attività per riepilogare i dati provenienti da più record di utilizzo file di controllo del software in un unico record generale. L'attività di riepilogo dei dati può ridurre la quantità di dati memorizzati nel database di Configuration Manager.

È possibile usare questa attività insieme all'attività **Riepiloga dati utilizzo mensile di controllo software** per riepilogare i dati di controllo software e ridurre lo spazio usato nel database di Configuration Manager. Per altre informazioni, vedere [Controllo del software in System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Riepiloga dati utilizzo mensile di controllo software**: usare questa attività per riepilogare i dati di più record di utilizzo mensile di controllo del software in un unico record generale. L'attività di riepilogo dei dati può ridurre la quantità di dati memorizzati nel database di Configuration Manager.

È possibile usare questa attività insieme all'attività **Riepiloga dati utilizzo file di controllo software** per riepilogare i dati di controllo software e ridurre lo spazio usato nel database di Configuration Manager. Per altre informazioni, vedere [Controllo del software in System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Aggiorna assegnazione disponibile per l'applicazione**: usare questa attività per fare in modo che Configuration Manager ricalcoli il mapping dei criteri e le distribuzioni delle applicazioni alle risorse nelle raccolte. Quando si distribuiscono criteri o applicazioni a una raccolta, Configuration Manager crea un mapping iniziale tra gli oggetti distribuiti e i membri della raccolta.

Questi mapping sono memorizzati in una tabella di riferimento rapido. Quando cambia l'appartenenza alle raccolte, questi mapping archiviati vengono aggiornati per riflettere tali modifiche. È comunque possibile che questi mapping perdano la sincronizzazione. Ad esempio, se il sito non riesce a elaborare correttamente un file di notifica, la modifica potrebbe non essere rispecchiata nei mapping. Questa attività aggiorna il mapping in base all'appartenenza alla raccolta corrente.  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  

**Aggiorna tabelle del Catalogo applicazioni**: usare questa attività per sincronizzare la cache del database del sito Web del Catalogo applicazioni con le ultime informazioni sulle applicazioni. Quando si modifica la configurazione di questa attività di manutenzione, le modifiche si applicano a tutti i siti primari della gerarchia.  

-   Sito di amministrazione centrale: non disponibile    
-   **Sito primario**: abilitato    
-   Sito secondario: non disponibile  


---
title: Elenco di controllo per la versione 1606 |Microsoft Docs
description: Informazioni sulle azioni da intraprendere prima di eseguire l&quot;aggiornamento di System Center Configuration Manager dalla versione 1511 o 1602 alla versione 1606.
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75652cd2-a95a-46c5-91c1-6d43fc8e787e
caps.latest.revision: 7
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: ba087244ad52087f32acbe413b1e56c7478e4db6

---
# <a name="checklist-for-installing-update-1606-for-system-center-configuration-manager"></a>Elenco di controllo per installare l'aggiornamento 1606 di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La versione 1606 del ramo corrente di System Center Configuration Manager è disponibile come aggiornamento per le versioni 1511 o 1602.

Prima di installare la versione 1606 come aggiornamento, consultare le informazioni seguenti e l'elenco di controllo per le azioni da eseguire prima di avviare l'aggiornamento.

Per informazioni sulle versioni di base, vedere [Baseline and update versions](../../../core/servers/manage/updates.md#bkmk_Baselines) (Versioni di base e aggiornate) in [Updates for System Center Configuration Manager](../../../core/servers/manage/updates.md) (Aggiornamenti per System Center Configuration Manager).

 ## <a name="about-installing-update-1606"></a>Informazioni sull'installazione dell'aggiornamento 1606

Come *aggiornamento*, la versione 1606 può essere installata solo nel sito di livello superiore della gerarchia. Ciò significa che l'installazione deve essere avviata dal sito di amministrazione centrale, se disponibile, o da un sito primario autonomo.  

-   I siti primari figlio installano automaticamente l'aggiornamento al termine dell'installazione dell'aggiornamento del sito di amministrazione centrale. Quando un sito installa gli aggiornamenti, è possibile controllare l'esecuzione tramite gli intervalli di servizio. Prima della versione 1606 gli intervalli di servizio si chiamavano finestre di manutenzione. Per altre informazioni, vedere [Intervalli di servizio per i server del sito](../../../core/servers/manage/install-in-console-updates.md#bkmk_ServiceWindow).  

-   Dopo che il sito primario padre ha completato l'installazione dell'aggiornamento, è necessario aggiornare manualmente i siti secondari dalla console di Configuration Manager. L'aggiornamento automatico dei server del sito secondario non è supportato.  

Quando il server del sito installa l'aggiornamento, i ruoli del sistema del sito installati nel server del sito e nei computer remoti vengono aggiornati automaticamente. Quindi, prima di installare l'aggiornamento, assicurarsi che ogni server del sistema del sito soddisfi i nuovi prerequisiti per il funzionamento con la nuova versione di aggiornamento.  

 La prima volta che si usa una console di Configuration Manager dopo l'aggiornamento, viene richiesto di aggiornare tale console.  A tale scopo, è necessario eseguire l'installazione di Configuration Manager nel computer che ospita la console e selezionare l'opzione per aggiornare la console. Si consiglia di installare al più presto l'aggiornamento della console.

 **Problemi noti per l'aggiornamento**   
  Quando si visualizza lo stato di installazione del pacchetto di aggiornamento, si verificano i problemi seguenti:
  - Durante l'aggiornamento dalla versione 1602 alla 1606, il passaggio **Estrai payload dell'aggiornamento** visualizza lo stato **Non avviato**, anche se il download è stato completato.
  - Durante l'aggiornamento dalla versione 1511 alla 1606, alcuni passaggi visualizzano lo stato **Completato** ma non visualizzano un valore per **Ora ultimo aggiornamento**.


## <a name="checklist"></a>Elenco di controllo  

 **Verificare che tutti i siti eseguano una versione supportata di System Center Configuration Manager:** prima di iniziare l'installazione dell'aggiornamento 1606, ogni server del sito nella gerarchia deve eseguire la stessa versione di System Center Configuration Manager: 1511 o 1602.

 **Controllare le versioni di .NET installate nei server del sistema del sito:** quando un sito installa l'aggiornamento 1606, Configuration Manager esegue in automatico l'installazione di .NET Framework 4.5.2 in ogni computer che ospita uno dei seguenti ruoli del sistema del sito, se non è già installato .NET Framework 4.5 o una sua versione successiva:  

-   Punto proxy di registrazione  

-   Punto di registrazione  

-   Punto di gestione  

-   punto di connessione del servizio  

Questa installazione consente di impostare il server del sistema del sito in uno stato di riavvio in sospeso e segnala gli errori al visualizzatore di stato dei componenti di Configuration Manager. Inoltre, le applicazioni .NET sul server potrebbero presentare errori casuali fino a quando il server non viene riavviato.  

 Per altre informazioni, vedere [Prerequisiti del sito e del sistema del sito](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  

 **Esaminare lo stato del sito e della gerarchia e verificare che non ci siano errori non risolti:** prima di aggiornare un sito, risolvere tutti i problemi operativi per il server del sito, il server di database del sito e i ruoli del sistema del sito installati nei computer remoti. Un aggiornamento del sito può avere esito negativo a causa di problemi operativi esistenti.  
 Per altre informazioni, vedere [Usare gli avvisi e il sistema di stato per System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md)  

 **Esaminare la replica di file e dati tra siti:**  verificare che la replica di file e database tra siti sia funzionante e aggiornata. Eventuali ritardi o backlog in uno dei due ambiti possono complicare o compromettere l'aggiornamento.    
Per la replica di database è possibile usare Replication Link Analyzer per risolvere i problemi prima di avviare l'aggiornamento.    
 Per altre informazioni, vedere   
[Informazioni su Replication Link Analyzer](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA) nell'argomento [Monitorare l'infrastruttura della gerarchia e di replica in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md).  

 **Installare tutti gli aggiornamenti critici disponibili per i sistemi operativi nei computer che ospitano il sito, il server di database del sito e i ruoli del sistema del sito remoto:** prima di installare un aggiornamento per Configuration Manager, installare gli aggiornamenti critici per ogni sistema del sito applicabile. Se un aggiornamento installato richiede un riavvio, riavviare i computer interessati prima di iniziare l'aggiornamento.  

 **Disabilitare le repliche di database per i punti di gestione nei siti primari:** Configuration Manager non può aggiornare correttamente un sito primario che dispone di una replica di database per i punti di gestione abilitati. Disabilitare la replica di database prima di:  

-   Creare un backup del database del sito per verificare l'aggiornamento del database  

-   Installare un aggiornamento per Configuration Manager  

Per ulteriori informazioni, vedere   
[Database replicas for management points for System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md) (Repliche di database per i punti di gestione per System Center Configuration Manager)  

 **Impostare i gruppi di disponibilità SQL Server AlwaysOn per eseguire il failover manuale:**  
 Prima di installare gli aggiornamenti, ad esempio la versione 1606, verificare che il gruppo di disponibilità sia impostato sul failover manuale. Dopo l'aggiornamento del sito, è possibile ripristinare la modalità di failover automatico. Per altre informazioni, vedere [SQL Server AlwaysOn for a site database](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) (SQL Server AlwaysOn per un database del sito).

 **Riconfigurare i punti di aggiornamento software che usano NLB:** Configuration Manager non è in grado di aggiornare un sito che usa un cluster Bilanciamento carico di rete (NLB) per ospitare i punti di aggiornamento software.  
Se si usano i cluster NLB per i punti di aggiornamento software, usare PowerShell per rimuovere il cluster NLB.    

 Per altre informazioni, vedere [Pianificare gli aggiornamenti software in System Center Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md)  

 **Disattivare tutte le attività di manutenzione del sito in ogni sito per la durata dell'installazione dell'aggiornamento nel sito in questione:** prima di installare l'aggiornamento, disabilitare le eventuali attività di manutenzione che potrebbero essere eseguite durante il processo di aggiornamento. Queste comprendono, ma non sono limitate alle seguenti attività:  

-   Backup server sito  

-   Elimina operazioni client obsolete  

-   Elimina dati di individuazione obsoleti  

Quando un'attività di manutenzione del database del sito viene eseguita durante l'installazione dell'aggiornamento, quest'ultima potrebbe avere esito negativo. Prima di disabilitare un'attività, registrarne la pianificazione per poter ripristinare la sua configurazione dopo l'installazione dell'aggiornamento.  
 Per altre informazioni, vedere [Attività di manutenzione per System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) e [Informazioni di riferimento per le attività di manutenzione per System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md)  

 **Creare un backup del database del sito nel sito di amministrazione centrale e nei siti primari:** prima di aggiornare un sito, eseguire il backup del database del sito per assicurarsi di avere un backup corretto da usare in caso di ripristino di emergenza.   
Per altre informazioni, vedere [Backup and recovery for System Center Configuration Manager](../../../protect/understand/backup-and-recovery.md)  


 **Testare l'aggiornamento del database su una copia del backup più recente del database del sito:** prima di aggiornare un sito di amministrazione centrale di System Center Configuration Manager o un sito primario, testare il processo di aggiornamento del database del sito su una copia del database del sito.  

-   È necessario testare il processo di aggiornamento del database del sito perché, quando si aggiorna un sito, il database del sito potrebbe essere modificato  

-   Nonostante non sia obbligatorio, il test di aggiornamento permette di identificare i problemi per l'aggiornamento prima che influiscano sul database di produzione  

-   Un aggiornamento non riuscito del database del sito può rendere inutilizzabile il database del sito e potrebbe richiedere un ripristino del sito per il relativo ripristino delle funzionalità  

-   Nonostante il database del sito sia condiviso tra i siti nella gerarchia, pianificare un test del database in ciascun sito applicabile prima di aggiornare tale sito  

-   Se si usano le repliche di database per i punti di gestione in un sito primario, disabilitare la replica prima di creare il backup del database del sito  

Configuration Manager non supporta il backup dei siti secondari, né l'aggiornamento di prova del database di siti secondari.   
L'esecuzione di un aggiornamento del database di test nel database del sito di produzione non è supportata. Questa operazione aggiorna il database del sito e potrebbe rendere inutilizzabile il sito. Per altre informazioni, vedere la sezione [Testare l'aggiornamento del database del sito](../../../core/servers/deploy/install/upgrade-to-configuration-manager.md#bkmk_test) in [Eseguire l'aggiornamento a System Center Configuration Manager](../../../core/servers/deploy/install/upgrade-to-configuration-manager.md).  

 **Prevedere una distribuzione pilota nei client:** quando si installa un aggiornamento per il client, è possibile testare quel nuovo aggiornamento client in ambiente di pre-produzione prima della distribuzione e dell'aggiornamento di tutti i client attivi.   
 Per sfruttare i vantaggi di questa opzione, prima di iniziare l'installazione dell'aggiornamento è necessario configurare il sito per supportare gli aggiornamenti automatici di pre-produzione. Per altre informazioni, vedere [Aggiornare i client in System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients.md) e   
[Come testare gli aggiornamenti client in una raccolta di pre-produzione in System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md)  

 **Iniziare a usare gli intervalli di servizio**  
 **Per controllare quando i server del sito installano gli aggiornamenti:** è possibile usare gli intervalli di servizio per definire un periodo di tempo applicabile a un server del sito primario durante il quale è possibile installare gli aggiornamenti del sito in questione.   
Questo permette di controllare quando i siti nella gerarchia installano l'aggiornamento.
Prima della versione 1606 gli intervalli di servizio si chiamavano finestre di manutenzione. Per altre informazioni, vedere [Intervalli di servizio per i server del sito](../../../core/servers/manage/install-in-console-updates.md#bkmk_ServiceWindow).  

 **Eseguire il controllo dei prerequisiti di installazione:** prima di installare l'aggiornamento 1606, è possibile eseguire il controllo dei prerequisiti in modo indipendente dall'installazione dell'aggiornamento. Quando si installa l'aggiornamento nel sito, il controllo dei prerequisiti viene eseguito di nuovo.  
Per altre informazioni, vedere **Passaggio 3: Eseguire il controllo dei prerequisiti prima di installare un aggiornamento** nell'argomento [Installare gli aggiornamenti nella console per System Center Configuration Manager](../../../core/servers/manage/install-in-console-updates.md).  

> [!IMPORTANT]  
>  Quando viene eseguito il controllo dei prerequisiti nel contesto dell'installazione di un aggiornamento o in modo indipendente, vengono aggiornati alcuni file di origine del prodotto usati per le attività di manutenzione del sito. Quindi, dopo aver eseguito il controllo dei prerequisiti ma prima di installare l'aggiornamento 1606, se si deve intraprendere un'attività di manutenzione del sito, eseguire **Setupwfe.exe** (installazione di Configuration Manager) dalla cartella CD.Latest nel server del sito.  

 **Aggiornare i siti:** a questo punto è possibile avviare l'installazione dell'aggiornamento per la gerarchia.  
  Si consiglia di non pianificare l'installazione dell'aggiornamento per ogni sito durante il normale orario di ufficio in modo che il processo di installazione dell'aggiornamento e le azioni per reinstallare i componenti del sito e i ruoli del sistema del sito abbiano un impatto minimo sulle operazioni aziendali. Per altre informazioni, vedere [Aggiornamenti per System Center Configuration Manager](../../../core/servers/manage/updates.md).  



<!--HONumber=Dec16_HO3-->



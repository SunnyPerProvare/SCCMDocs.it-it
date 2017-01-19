---
title: Elenco di controllo per la versione 1610 | System Center Configuration Manager
description: Informazioni sulle azioni da intraprendere prima di eseguire l&quot;aggiornamento di System Center Configuration Manager alla versione 1610.
ms.custom: na
ms.date: 11/18/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b411cb0-4fd1-41f2-a2f6-33738a5bde96
caps.latest.revision: 7
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 0c7d32a80559a4aa684ea1533cd36d0ef977fbfc
ms.openlocfilehash: 25bffa256cbe70fb590eccb641c94f572f618ef3

---
# <a name="checklist-for-installing-update-1610-for-system-center-configuration-manager"></a>Elenco di controllo per l'installazione dell'aggiornamento 1610 di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Quando si usa Current Branch di System Center Configuration Manager, per aggiornare la gerarchia dalla versione 1606 è possibile installare l'aggiornamento nella console per la versione 1610. Se la gerarchia esegue la versione 1511, 1602 o 1606, è possibile eseguire l'aggiornamento alla versione 1610. 

Per ottenere l'aggiornamento per la versione 1610, è necessario usare un ruolo del sistema del sito punto di connessione del servizio nel sito principale della gerarchia. Questo può essere in modalità online o offline. Dopo che la gerarchia ha scaricato l'aggiornamento da Microsoft, il pacchetto è disponibile nella console, in **Amministrazione &gt; Panoramica &gt; Servizi cloud &gt; Aggiornamenti e manutenzione**.

-   Quando l'aggiornamento risulta **Disponibile**, è pronto per l'installazione. Prima di installare la versione 1610, leggere le informazioni seguenti [sull'installazione dell'aggiornamento 1610](#about-installing-update-1610) e l'[elenco di controllo](#checklist) delle configurazioni da eseguire prima dell'avvio dell'aggiornamento.

-   Se l'aggiornamento risulta come **Download** e non cambia, esaminare eventuali errori in **hman. log** e in **dmpdownloader. log**.

    -   In genere, è anche possibile riavviare il servizio SMS\_Executive nel server del sito per riavviare il download dei file di ridistribuzione degli aggiornamenti.

    -   Un altro problema comune di download è dovuto ad alcune impostazioni del server proxy che impediscono il download da <http://silverlight.dlservice.microsoft.com> e da <http://download.microsoft.com>.

Per altre informazioni sull'installazione degli aggiornamenti, vedere [Aggiornamenti e manutenzione nella console](/sccm/core/servers/manage/updates#a-namebkmkinconsolea-in-console-updates-and-servicing).

Per informazioni sulle versioni di Current Branch, vedere [Versioni di base e di aggiornamento](/sccm/core/servers/manage/updates#bkmk_Baselines) in [Aggiornamenti per System Center Configuration Manager](/sccm/core/servers/manage/updates).

## <a name="about-installing-update-1610"></a>Informazioni sull'installazione dell'aggiornamento 1610

**Siti:**  
L'aggiornamento 1610 può essere installato solo nel sito principale della gerarchia. Ciò significa che l'installazione deve essere avviata dal sito di amministrazione centrale, se disponibile, o da un sito primario autonomo. Dopo l'installazione dell'aggiornamento nel sito principale, il comportamento dell'aggiornamento dei siti figlio è il seguente:

-   I siti primari figlio installano automaticamente l'aggiornamento al termine dell'installazione dell'aggiornamento del sito di amministrazione centrale. È possibile usare gli intervalli di servizio per controllare quando eseguire l'installazione di aggiornamenti in un sito. Prima della versione 1606 gli intervalli di servizio si chiamavano finestre di manutenzione. Per altre informazioni, vedere [Intervalli di servizio per i server del sito](https://docs.microsoft.com/en-us/sccm/core/servers/manage/install-in-console-updates#bkmk_ServiceWindow).

-   Dopo che il sito primario padre ha completato l'installazione dell'aggiornamento, è necessario aggiornare manualmente i siti secondari dalla console di Configuration Manager. L'aggiornamento automatico dei server del sito secondario non è supportato.

**Ruoli del sistema del sito:**  
Quando il server del sito installa l'aggiornamento, i ruoli del sistema del sito installati nel server del sito e nei computer remoti vengono aggiornati automaticamente. Quindi, prima di installare l'aggiornamento, assicurarsi che ogni server del sistema del sito soddisfi i nuovi prerequisiti per il funzionamento con la nuova versione di aggiornamento.

**Console di Configuration Manager:**   
La prima volta che si usa una console di Configuration Manager dopo l'aggiornamento, viene richiesto di aggiornare tale console. A tale scopo, è necessario eseguire l'installazione di Configuration Manager nel computer che ospita la console e selezionare l'opzione per aggiornare la console. Si consiglia di installare al più presto l'aggiornamento della console.



## <a name="checklist"></a>Elenco di controllo

**Verificare che tutti i siti eseguano una versione supportata di System Center Configuration Manager:** prima di iniziare l'installazione dell'aggiornamento 1610, ogni sito nella gerarchia deve eseguire la stessa versione di System Center Configuration Manager: 1511, 1602 o 1606.

**Controllare lo stato di Software Assurance o dei diritti di sottoscrizione equivalenti:**   
Per installare l'aggiornamento 1610, è necessario disporre di un contratto Software Assurance attivo. Quando si installa la versione 1610, nella scheda **Licenza** è disponibile l'opzione per la conferma della **data di scadenza di Software Assurance**. Si tratta di un valore facoltativo, che è possibile specificare come utile promemoria della data di scadenza della licenza che verrà visualizzato quando si installeranno aggiornamenti in futuro. Se per l'installazione di Configuration Manager si è usato il supporto di base della versione 1606, è possibile che questo valore sia stato specificato in precedenza durante l'installazione oppure nella scheda **Licenza** delle **Impostazioni gerarchia** dopo l'installazione del sito.

Per altre informazioni, vedere [Licenze e rami per System Center Configuration Manager](/sccm/core/understand/learn-more-editions).

**Controllare le versioni di .NET installate nei server del sistema del sito:** quando un sito installa l'aggiornamento 1610, Configuration Manager esegue in automatico l'installazione di .NET Framework 4.5.2 in ogni computer che ospita uno dei seguenti ruoli del sistema del sito, se .NET Framework 4.5 o versione successiva non è stato ancora installato:

-   Punto proxy di registrazione
-   Punto di registrazione
-   Punto di gestione
-   punto di connessione del servizio

Questa installazione consente di impostare il server del sistema del sito in uno stato di riavvio in sospeso e segnala gli errori al visualizzatore di stato dei componenti di Configuration Manager. Inoltre, le applicazioni .NET sul server potrebbero presentare errori casuali fino a quando il server non viene riavviato.

Per altre informazioni, vedere [Prerequisiti del sito e del sistema del sito](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).

**Esaminare lo stato del sito e della gerarchia e verificare che non ci siano errori non risolti:** prima di aggiornare un sito, risolvere tutti i problemi operativi per il server del sito, il server di database del sito e i ruoli del sistema del sito installati nei computer remoti. Un aggiornamento del sito può avere esito negativo a causa di problemi operativi esistenti.

Per ulteriori informazioni, vedere [Use alerts and the status system for System Center Configuration Manager](/sccm/core/servers/manage/use-alerts-and-the-status-system).

**Esaminare la replica di file e dati tra siti:**   
verificare che la replica di file e database tra siti sia funzionante e aggiornata. Eventuali ritardi o backlog in uno dei due ambiti possono complicare o compromettere l'aggiornamento.\
Per la replica di database è possibile usare Replication Link Analyzer per risolvere i problemi prima di avviare l'aggiornamento.

Per altre informazioni, vedere [Informazioni su Replication Link Analyzer](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure#BKMK_RLA) nell'argomento [Monitorare l'infrastruttura della gerarchia e di replica in System Center Configuration Manager](/sccm/core/servers/manage/monitor-hierarchy-and-replication-infrastructure).

**Installare tutti gli aggiornamenti critici disponibili per i sistemi operativi nei computer che ospitano il sito, il server di database del sito e i ruoli del sistema del sito remoto:** prima di installare un aggiornamento per Configuration Manager, installare gli aggiornamenti critici per ogni sistema del sito applicabile. Se un aggiornamento installato richiede un riavvio, riavviare i computer interessati prima di iniziare l'aggiornamento di Configuration Manager.

**Disabilitare le repliche di database per i punti di gestione nei siti primari:**   
Configuration Manager non può aggiornare un sito primario per il quale esista una replica del database per i punti di gestione abilitati. Disabilitare la replica di database prima di:

-   Creare un backup del database del sito per verificare l'aggiornamento del database
-   Installare un aggiornamento per Configuration Manager

Per altre informazioni, vedere [Repliche di database per i punti di gestione per System Center Configuration Manager](/sccm/core/servers/deploy/configure/database-replicas-for-management-points).

**Impostare i gruppi di disponibilità SQL Server AlwaysOn per eseguire il failover manuale:**   
Prima di installare gli aggiornamenti, ad esempio la versione 1610, verificare che il gruppo di disponibilità sia impostato sul failover manuale. Dopo l'aggiornamento del sito, è possibile ripristinare la modalità di failover automatico. Per altre informazioni, vedere [SQL Server AlwaysOn for a site database](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database) (SQL Server AlwaysOn per un database del sito).

**Riconfigurare i punti di aggiornamento software che usano Bilanciamento carico di rete:**   
Configuration Manager non può aggiornare un sito che usa un cluster Bilanciamento carico di rete per ospitare i punti di aggiornamento software.

Se si usano i cluster NLB per i punti di aggiornamento software, usare PowerShell per rimuovere il cluster NLB.
Per altre informazioni, vedere [Pianificare gli aggiornamenti software in System Center Configuration Manager](/sccm/sum/plan-design/plan-for-software-updates).

**Disabilitare tutte le attività di manutenzione del sito in ogni sito per la durata dell'aggiornamento del sito in questione:**   
Prima di installare l'aggiornamento , disabilitare le eventuali attività di manutenzione che potrebbero essere eseguite mentre è in corso il processo di aggiornamento. Queste comprendono, ma non sono limitate alle seguenti attività:

-   Backup server sito
-   Elimina operazioni client obsolete
-   Elimina dati di individuazione obsoleti

Quando un'attività di manutenzione del database del sito viene eseguita durante l'installazione dell'aggiornamento, quest'ultima potrebbe avere esito negativo. Prima di disabilitare un'attività, registrarne la pianificazione per poter ripristinare la sua configurazione dopo l'installazione dell'aggiornamento.

Per altre informazioni, vedere [Attività di manutenzione per System Center Configuration Manager](/sccm/core/servers/manage/maintenance-tasks) e [Informazioni di riferimento per le attività di manutenzione per System Center Configuration Manager](/sccm/core/servers/manage/reference-for-maintenance-tasks).

**Creare un backup del database del sito nel sito di amministrazione centrale e nei siti primari:** prima di aggiornare un sito, eseguire il backup del database del sito per assicurarsi di avere un backup corretto da usare in caso di ripristino di emergenza.

Per altre informazioni, vedere [Backup e ripristino per System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).

**Testare l'aggiornamento del database su una copia del backup più recente del database del sito:** prima di aggiornare un sito di amministrazione centrale di System Center Configuration Manager o un sito primario, testare il processo di aggiornamento del database del sito su una copia del database del sito.

-   È necessario testare il processo di aggiornamento del database del sito perché, quando si aggiorna un sito, il database del sito potrebbe essere modificato
-   Nonostante non sia obbligatorio, il test di aggiornamento permette di identificare i problemi per l'aggiornamento prima che influiscano sul database di produzione
-   Un aggiornamento non riuscito del database del sito può rendere inutilizzabile il database del sito e potrebbe richiedere un ripristino del sito per il relativo ripristino delle funzionalità
-   Nonostante il database del sito sia condiviso tra i siti nella gerarchia, pianificare un test del database in ciascun sito applicabile prima di aggiornare tale sito
-   Se si usano le repliche di database per i punti di gestione in un sito primario, disabilitare la replica prima di creare il backup del database del sito

Configuration Manager non supporta il backup dei siti secondari, né l'aggiornamento di prova del database di siti secondari.

L'esecuzione di un aggiornamento del database di test nel database del sito di produzione non è supportata. Questa operazione aggiorna il database del sito e potrebbe rendere inutilizzabile il sito. Per altre informazioni, vedere la sezione [Testare l'aggiornamento del database del sito](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager#bkmk_test) in [Eseguire l'aggiornamento a System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).

**Pianificare la distribuzione pilota del client:**   
Quando si installa un aggiornamento per il client, è possibile testare quest'ultimo in un ambiente di pre-produzione prima della distribuzione e dell'aggiornamento di tutti i client attivi.

Per sfruttare i vantaggi di questa opzione, prima di iniziare l'installazione dell'aggiornamento è necessario configurare il sito per supportare gli aggiornamenti automatici di pre-produzione.

Per altre informazioni, vedere [Aggiornare i client in System Center Configuration Manager](/sccm/core/clients/manage/upgrade/upgrade-clients) e [Come testare gli aggiornamenti client in una raccolta di pre-produzione in System Center Configuration Manager](/sccm/core/clients/manage/upgrade/test-client-upgrades).

**Pianificare l'uso di intervalli di servizio per controllare il momento dell'installazione di aggiornamenti nei server del sito:**   
È possibile usare gli intervalli di servizio per definire un periodo applicabile a un server del sito primario durante il quale sia possibile installare gli aggiornamenti del sito in questione.

Questo permette di controllare quando i siti nella gerarchia installano l'aggiornamento. Prima della versione 1606 gli intervalli di servizio si chiamavano finestre di manutenzione. Per altre informazioni, vedere [Intervalli di servizio per i server del sito](/sccm/core/servers/manage/install-in-console-updates#bkmk_servicewindow).

**Eseguire il controllo dei prerequisiti di installazione:**   
Se nella console l'aggiornamento risulta**Disponibile,**, è possibile eseguire il controllo dei prerequisiti in modo indipendente prima di installare l'aggiornamento. Quando si installa l'aggiornamento nel sito, il controllo dei prerequisiti viene eseguito di nuovo.

Per eseguire il controllo dei prerequisiti dalla console, passare ad **Amministrazione > Panoramica > Servizi cloud > Aggiornamenti e manutenzione,** fare clic con il pulsante destro del mouse su **Configuration Manager 1610 update package** (Aggiornamento di Configuration Manager versione 1610) e selezionare **Esegui controllo prerequisiti**.

Per altre informazioni sull'avvio e quindi sul monitoraggio del controllo dei prerequisiti, vedere **Passaggio 3: Eseguire il controllo dei prerequisiti prima di installare un aggiornamento** nell'argomento [Installare gli aggiornamenti nella console per System Center Configuration Manager](/sccm/core/servers/manage/install-in-console-updates).

> [!IMPORTANT]  
> Quando viene eseguito il controllo dei prerequisiti nel contesto dell'installazione di un aggiornamento o in modo indipendente, vengono aggiornati alcuni file di origine del prodotto usati per le attività di manutenzione del sito. Quindi, dopo aver eseguito il controllo dei prerequisiti ma prima di installare l'aggiornamento 1610, se si deve intraprendere un'attività di manutenzione del sito, eseguire **Setupwfe.exe** (installazione di Configuration Manager) dalla cartella CD.Latest nel server del sito.

**Aggiornare i siti:**   
A questo punto è possibile avviare l'installazione dell'aggiornamento per la gerarchia. Per informazioni sull'installazione dell'aggiornamento, vedere [Installare gli aggiornamenti nella console.](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates)

Si consiglia di non pianificare l'installazione dell'aggiornamento per ogni sito durante il normale orario di ufficio in modo che il processo di installazione dell'aggiornamento e le azioni per reinstallare i componenti del sito e i ruoli del sistema del sito abbiano un impatto minimo sulle operazioni aziendali. Per altre informazioni, vedere [Aggiornamenti per System Center Configuration Manager](/sccm/core/servers/manage/updates).



<!--HONumber=Dec16_HO3-->



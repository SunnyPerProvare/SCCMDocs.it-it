---
title: Eseguire l&quot;aggiornamento a System Center Configuration Manager | Microsoft Docs
description: Passaggi per eseguire l&quot;aggiornamento sul posto da un sito e da una gerarchia che esegue System Center 2012 Configuration Manager.
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c64e7483-b4bb-4738-95f4-ecdaeb6a2ba6
caps.latest.revision: 21
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: ca07b46db0967ca03cc5e858b835d2c2108f1210
ms.lasthandoff: 03/17/2017


---
# <a name="upgrade-to-system-center-configuration-manager"></a>Eseguire l'aggiornamento a System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile eseguire l'aggiornamento sul posto a System Center Configuration Manager da un sito e da una gerarchia che esegue System Center 2012 Configuration Manager.  

 Prima di eseguire l'aggiornamento da System Center 2012 Configuration Manager, è necessario preparare i siti rimuovendo le configurazioni specifiche che possono impedire l'aggiornamento e osservare la sequenza di aggiornamento quando sono coinvolti più siti.  

 > [!TIP]
 > Quando si gestisce l'infrastruttura del sito e della gerarchia di System Center Configuration Manager, i termini *upgrade*, *aggiornamento* e *installazione* vengono usati per descrivere tre concetti distinti. Per informazioni su come viene usato ogni termine, vedere [Informazioni su upgrade, aggiornamento e installazione](/sccm/core/understand/upgrade-update-install).

##  <a name="bkmk_path"></a> Percorsi di aggiornamento sul posto  

**Aggiornare alla versione 1606**  
Il 15 dicembre 2016 è stato rilasciato nuovamente il supporto di base della versione 1606, per aggiungere il supporto di scenari di aggiornamento supplementari. La nuova versione supporta l'aggiornamento dei seguenti prodotti a una versione con licenza completa di System Center Configuration Manager versione 1606:  
-   L'installazione di una valutazione di System Center Configuration Manager versione 1606
-   Installazione di una versione finale candidata di System Center Configuration Manager  
-   System Center 2012 Configuration Manager con Service Pack 1  
-   System Center 2012 Configuration Manager con Service Pack 2  
-   System Center 2012 R2 Configuration Manager  
-   System Center Configuration Manager 2012 R2 con Service Pack 1  

Se si usano supporti di base della versione 1606 scaricati prima del 15 dicembre 2016, è possibile aggiornare solo i seguenti componenti a una versione con licenza completa di System Center Configuration Manager versione 1606:
-   L'installazione di una valutazione di System Center Configuration Manager versione 1606
-   System Center 2012 Configuration Manager con Service Pack 2
-   System Center Configuration Manager 2012 R2 con Service Pack 1

**Aggiornare alla versione 1511**  
Quando è presente il supporto di base della versione 1511 è possibile aggiornare i seguenti prodotti a una versione con licenza completa di System Center Configuration Manager versione 1511:  
-   L'installazione di una valutazione di System Center Configuration Manager versione 1511
-   L'installazione di una versione finale candidata di System Center Configuration Manager  
-   System Center 2012 Configuration Manager con Service Pack 1  
-   System Center 2012 Configuration Manager con Service Pack 2  
-   System Center 2012 R2 Configuration Manager  
-   System Center Configuration Manager 2012 R2 con Service Pack 1  



> [!TIP]  
>  Se si esegue l'aggiornamento da una versione di System Center 2012 Configuration Manager a Current Branch il processo di aggiornamento potrebbe risultare semplificato. Per altre informazioni, vedere  
>   
>  -   La sezione [Versioni di base e di aggiornamento](../../../../core/servers/manage/updates.md#bkmk_Baselines) in [Aggiornamenti per System Center Configuration Manager](../../../../core/servers/manage/updates.md)  
>  -   [Cartella CD.Latest per System Center Configuration Manager](../../../../core/servers/manage/the-cd.latest-folder.md)  

 **Le operazioni seguenti non sono supportate:**  
-   Non è supportato l'aggiornamento di una versione Technical Preview per System Center Configuration Manager a un'installazione con licenza completa.  Una versione Technical Preview può essere aggiornata solo a una versione successiva di Technical Preview.  

-   La migrazione da una versione Technical Preview a una versione con licenza completa non è supportata.  

##  <a name="bkmk_checklist"></a> Eseguire l'aggiornamento degli elenchi di controllo  
 Gli elenchi di controllo seguenti possono aiutare a pianificare un aggiornamento a System Center Configuration Manager.  

### <a name="before-you-upgrade"></a>Prima dell'aggiornamento  
**Assicurarsi che l'ambiente informatico soddisfi le configurazioni supportate** necessarie per eseguire l'aggiornamento a System Center Configuration Manager:  

Esaminare i sistemi operativi server usati per ospitare i ruoli del sistema del sito:  

-   Alcuni sistemi operativi meno recenti supportati da System Center 2012 Configuration Manager non sono supportati da System Center Configuration Manager e i ruoli del sistema del sito in questi sistemi operativi devono essere rilocati o rimossi prima dell'aggiornamento. Consultare la documentazione [Sistemi operativi supportati per i server del sistema del sito](../../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md).   
-   Il controllo dei prerequisiti per Configuration Manager non verifica i prerequisiti per i ruoli del sistema del sito sul server del sito o in sistemi del sito remoti  

Esaminare i prerequisiti richiesti in ciascun computer che ospita un ruolo del sistema del sito:  

-   Ad esempio, per distribuire un sistema operativo, System Center Configuration Manager usa Windows 10 Assessment and Deployment Kit (Windows ADK). Prima di eseguire l'installazione, è necessario scaricare e installare Windows 10 ADK nel server del sito e in ciascun computer in cui è in esecuzione un'istanza del provider SMS.  

Per informazioni generali sulle piattaforme e sulle configurazioni dei prerequisiti supportate, vedere [Supported configurations for System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md).  

Per informazioni sull'uso di Windows ADK con Configuration Manager, vedere [Infrastructure requirements for operating system deployment in System Center Configuration Manager](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md) (Requisiti dell'infrastruttura per la distribuzione del sistema operativo in System Center Configuration Manager).  

**Esaminare lo stato del sito e della gerarchia e verificare che non siano presenti problemi non risolti:**  
Prima di aggiornare un sito, risolvere tutti i problemi operativi per il server del sito, il server del database del sito e i ruoli del sistema del sito installati sui computer remoti. Un aggiornamento del sito può avere esito negativo a causa di problemi operativi esistenti.  

**Installare tutti gli aggiornamenti critici disponibili per i sistemi operativi dei computer che ospitano il sito, il server di database del sito e i ruoli del sistema del sito remoto:**  
Prima di aggiornare un sito, installare eventuali aggiornamenti critici per ogni sistema del sito applicabile. Se un aggiornamento installato richiede un riavvio, riavviare i computer interessati prima di iniziare l'aggiornamento del Service Pack.  

Per altre informazioni, vedere [Windows Update](http://go.microsoft.com/fwlink/p/?LinkId=105851).  

**Disinstallare i ruoli del sistema del sito non supportati da System Center Configuration Manager:**  
I ruoli del sistema del sito seguenti non vengono più usati in System Center Configuration Manager e devono essere disinstallati prima di eseguire l'aggiornamento da System Center 2012 Configuration Manager:  

-   Punto di gestione fuori banda  
-   Punto di convalida integrità servizio  

**Disabilitare le repliche di database per i punti di gestione nei siti primari:**  
Configuration Manager non può aggiornare un sito primario che ha una replica del database per i punti di gestione abilitati. Disabilitare la replica di database prima di:  

-   Creare un backup del database del sito per verificare l'aggiornamento del database  
-   Eseguire l'aggiornamento del sito di produzione a System Center Configuration Manager  

Per altre informazioni, vedere  
-   System Center 2012 Configuration Manager: [Configurare le repliche di database per i punti di gestione](https://technet.microsoft.com/library/hh846234.aspx)  
-   System Center Configuration Manager: [Database replicas for management points for System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md) (Repliche di database per i punti di gestione per System Center Configuration Manager)  

**Riconfigurare i punti di aggiornamento software che usano NLB:**  
Configuration Manager non può aggiornare un sito che usa un cluster Bilanciamento carico di rete per ospitare i punti di aggiornamento software.  

Se si usano i cluster NLB per i punti di aggiornamento software, usare PowerShell per rimuovere il cluster NLB. A partire da System Center 2012 Configuration Manager SP1, non esistono opzioni nella console di Configuration Manager per configurare un cluster Bilanciamento carico di rete  

**Disabilitare tutte le attività di manutenzione del sito per l'intera durata dell'aggiornamento del sito:**  
Prima di eseguire l'aggiornamento a System Center Configuration Manager, disabilitare le eventuali attività di manutenzione che possono essere in esecuzione mentre è in corso il processo di aggiornamento. Queste comprendono, ma non sono limitate alle seguenti attività:  

-   Backup server sito  
-   Elimina operazioni client obsolete  
-   Elimina dati di individuazione obsoleti  

Quando un'attività di manutenzione del database del sito è in esecuzione durante il processo di aggiornamento, potrebbe non essere possibile aggiornare il sito.  

Prima di disattivare un'attività, registrare la pianificazione dell'attività in modo da poter ripristinare la sua configurazione al termine dell'aggiornamento del sito.  

Per altre informazioni sulle attività di manutenzione del sito, vedere:  

-   System Center 2012 Configuration Manager: [Pianificazione di attività di manutenzione per Configuration Manager](https://technet.microsoft.com/library/gg712686.aspx)  
-   System Center 2012 Configuration Manager: [Reference for maintenance tasks for System Center Configuration Manager](../../../../core/servers/manage/reference-for-maintenance-tasks.md) (Riferimento per attività di manutenzione per System Center Configuration Manager)  

**Eseguire il controllo dei prerequisiti di installazione**:  
Prima di aggiornare un sito, è possibile eseguire il **controllo dei prerequisiti** in modo indipendente dal programma di installazione per convalidare che il sito soddisfa i prerequisiti. In seguito, quando si aggiorna il sito, viene nuovamente eseguito il controllo dei prerequisiti.  

Se si usa il supporto di base per la versione 1606 di ottobre 2016, il controllo dei prerequisiti indipendente valuta il sito per l'aggiornamento sia a Current Branch sia a Long-Term Servicing Branch (LTSB) di System Center Configuration Manager. Poiché alcune funzionalità non sono supportate da LTSB, è possibile che in *ConfigMgrPrereq.log* appaiano voci simili alle seguenti:
 - INFO: The site is a LTSB edition. (INFORMAZIONI: il sito è un'edizione LTSB).
 - Unsupported site system role 'Asset Intelligence synchronization point' for the LTSB edition ;    Error;    Configuration Manager has detected that the 'Asset Intelligence synchronization point' is installed. (Ruolo del sistema del sito 'Punto di sincronizzazione di Asset Intelligence' non supportato per l'edizione LTSB;    Errore;    Configuration Manager ha rilevato l'installazione di 'Punto di sincronizzazione di Asset Intelligence'). Asset Intelligence is not supported on the LTSB edition. (Asset Intelligence non è supportato nell'edizione LTSB.) You must uninstall the Asset Intelligence synchronization point site system role before you can continue. (Prima di continuare, è necessario disinstallare il ruolo del sistema del sito Punto di sincronizzazione di Asset Intelligence.)

Se si prevede di eseguire l'aggiornamento a Current Branch, è possibile ignorare gli errori per l'edizione LTSB. Tali errori sono rilevanti solo se si prevede di eseguire l'aggiornamento a LTSB.

In seguito, quando si esegue l'installazione di Configuration Manager per applicare l'aggiornamento, il controllo dei prerequisiti verrà eseguito nuovamente e valuterà il sito in base al ramo di System Center Configuration Manager che si sceglie di installare (Current Branch o LTSB). Se si sceglie di eseguire l'aggiornamento a Current Branch, il controllo delle funzionalità non supportate da LTSB non viene eseguito.

Per altre informazioni, vedere [Controllo dei prerequisiti](/sccm/core/servers/deploy/install/prerequisite-checker) e [Elenco dei controlli dei prerequisiti per System Center Configuration Manager](/sccm/core/servers/deploy/install/list-of-prerequisite-checks).  

**Scaricare i file dei prerequisiti e i file ridistribuibili per System Center Configuration Manager:**    
Usare il **downloader di installazione** per scaricare i file ridistribuibili dei prerequisiti, i Language Pack e gli ultimi aggiornamenti del prodotto per System Center Configuration Manager.  

Per informazioni, vedere [Downloader di installazione](/sccm/core/servers/deploy/install/setup-downloader).  

**Pianificare la gestione delle lingue di server e client**:  
Quando si aggiorna un sito, l'aggiornamento del sito consente di installare solo le versioni di Language Pack selezionate durante l'aggiornamento.  

-   Il programma di installazione esamina la configurazione della lingua corrente del sito, quindi identifica i Language Pack disponibili nella cartella in cui sono stati memorizzati in precedenza i file dei prerequisiti.  
-   È possibile dunque confermare la selezione dei Language Pack di server e client correnti oppure modificare le selezioni per aggiungere o rimuovere il supporto per le lingue.  
-   È possibile selezionare solo quei Language Pack che sono disponibili quando si esegue il programma di installazione (ottenuto con i file dei prerequisiti scaricati).  

> [!NOTE]  
>  Non è possibile usare i Language Pack di System Center 2012 Configuration Manager per abilitare le lingue per un sito di System Center Configuration Manager.  

Per altre informazioni sui Language Pack, vedere [Language Pack in System Center Configuration Manager](../../../../core/servers/deploy/install/language-packs.md).  

**Esaminare le considerazioni per gli aggiornamenti del sito**:  
Quando si aggiorna un sito, alcune funzionalità e configurazioni vengono ripristinati a una configurazione predefinita. Per prepararsi a queste modifiche e ad altre correlate, esaminare le informazioni in  [Considerazioni sull'aggiornamento](#bkmk_considerations).  

**Creare un backup del database del sito nel sito di amministrazione centrale e nei siti primari:**  
Prima di aggiornare un sito, eseguire il backup del database del sito per assicurarsi di disporre di un backup effettuato correttamente da usare in caso di ripristino di emergenza.  

Vedere [Backup e ripristino per System Center Configuration Manager](../../../../protect/understand/backup-and-recovery.md).  

**Eseguire il backup di un file Configuration.mof personalizzato**:  
Se si usa un file Configuration.mof personalizzato per definire le classi di dati usate con l'inventario hardware, creare un backup del file prima di aggiornare il sito. Quindi, dopo l'aggiornamento, ripristinare il file nel sito. Per altre informazioni sull'uso del file, vedere [Come estendere l'inventario hardware in System Center Configuration Manager](../../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

**Verificare il processo di aggiornamento del database in una copia del backup più recente del database del sito:**  
Prima di effettuare l'aggiornamento di un sito di amministrazione centrale o sito primario di Configuration Manager, verificare il processo di aggiornamento del database del sito su una copia del database del sito.  

-   È necessario testare il processo di aggiornamento del database del sito perché, quando si aggiorna un sito, il database del sito potrebbe essere modificato  
-   Nonostante non sia obbligatorio, il test di aggiornamento permette di identificare i problemi per l'aggiornamento prima che influiscano sul database di produzione  
-   Un aggiornamento non riuscito del database del sito può rendere inutilizzabile il database del sito e potrebbe richiedere un ripristino del sito per il relativo ripristino delle funzionalità  
-   Nonostante il database del sito sia condiviso tra i siti nella gerarchia, pianificare un test del database in ciascun sito applicabile prima di aggiornare tale sito  
-   Se si usano le repliche di database per i punti di gestione in un sito primario, disabilitare la replica prima di creare il backup del database del sito  

Configuration Manager non supporta né il backup di siti secondari, né l'aggiornamento di prova del database di siti secondari.  

L'esecuzione di un aggiornamento del database di test nel database del sito di produzione non è supportata. Questa operazione consente di aggiornare il database del sito e potrebbe rendere inutilizzabile il sito.  

Per altre informazioni, vedere [Testare l'aggiornamento del database del sito](#bkmk_test).  

**Riavviare il server del sito e ogni computer che ospita un ruolo di sistema del sito**:  
Questa operazione ha lo scopo di garantire che non restino in sospeso azioni di un'installazione recente di aggiornamenti o dei prerequisiti. Si tratta di un processo interno specifico dell'organizzazione.  

**Aggiornare i siti**:  
A partire dal sito principale della gerarchia, eseguire Setup.exe dal supporto di origine di System Center Configuration Manager.  

Al termine degli aggiornamenti del sito di livello superiore è possibile iniziare l'aggiornamento di ogni sito figlio. Completare l'aggiornamento di ogni sito prima di iniziare l'aggiornamento del sito successivo  

Finché tutti i siti della gerarchia non sono stati aggiornati a System Center Configuration Manager, la gerarchia funziona in modalità mista.  

Per informazioni su come eseguire l'aggiornamento, vedere [Aggiornare i siti](#bkmk_upgrade).  

### <a name="after-you-upgrade"></a>Dopo l'aggiornamento  
**Aggiornare le console autonome di Configuration Manager**:  
Per impostazione predefinita, quando si aggiorna un sito di amministrazione centrale o un sito primario, l'installazione aggiorna anche la console di Configuration Manager installata sul server del sito. Tuttavia, occorre aggiornare manualmente ciascuna console installata su un computer diverso dal server del sito.  

> [!TIP]  
>  Chiudere una console aperta prima di iniziare l'aggiornamento.  

Per altre informazioni, vedere [Install System Center Configuration Manager consoles](../../../../core/servers/deploy/install/install-consoles.md) (Installare console di System Center Configuration Manager).  

**Riconfigurare le repliche di database per i punti di gestione nei siti primari:**  
Se si usano le repliche di database per i punti di gestione nei siti primari, è necessario disinstallare le repliche del database prima di aggiornare il sito. Dopo l'aggiornamento di un sito primario riconfigurare la replica di database per i punti di gestione.   
Per altre informazioni, vedere  [Database replicas for management points for System Center Configuration Manager](../../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Riconfigurare eventuali attività di manutenzione del database disabilitate prima dell'aggiornamento:**  
Se si sono disabilitate le [informazioni di riferimento per le attività di manutenzione per System Center Configuration Manager](../../../../core/servers/manage/reference-for-maintenance-tasks.md) in relazione al database, riconfigurare tali attività nel sito usando le stesse impostazioni presenti prima dell'aggiornamento.  

**Aggiornare i client**:  
Dopo che tutti i siti sono stati aggiornati a System Center Configuration Manager, pianificare l'aggiornamento dei client.  

Quando si aggiorna un client, il software client corrente viene disinstallato e viene installata la nuova versione del software client. Per aggiornare i client, è possibile usare qualsiasi metodo supportato da Configuration Manager.  

> [!TIP]  
>  Quando si aggiorna il sito di livello superiore di una gerarchia, viene aggiornato anche il pacchetto di installazione del client in ogni punto di distribuzione presente nella gerarchia. Quando si aggiorna un sito primario, viene aggiornato il pacchetto di aggiornamento del client disponibile da tale sito.  

Per informazioni su come aggiornare i client esistenti e su come installare i nuovi client, vedere [Come aggiornare i client per i computer Windows in System Center Configuration Manager](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

##  <a name="bkmk_considerations"></a> Considerazioni sull'aggiornamento  
**Azioni automatiche**:  
Quando si esegue l'aggiornamento a System Center Configuration Manager, le azioni seguenti sono automatiche:  

-   Il sito esegue una reimpostazione del sito che include una reinstallazione di tutti i ruoli del sistema del sito.  
-   Se il sito è il sito di livello superiore di una gerarchia, questo aggiorna il pacchetto di installazione del client in ogni punto di distribuzione presente nella gerarchia. Il sito aggiorna anche le immagini di avvio predefinite per usare la nuova versione di Windows PE inclusa con Windows Assessment and Deployment Kit 10. Tuttavia, l'aggiornamento non aggiorna il supporto esistente da usare per la distribuzione dell'immagine.  
-   Se il sito è un sito primario, questo aggiorna il pacchetto di aggiornamento del client per tale sito.  

**Azioni manuali per l'utente amministratore dopo un aggiornamento**   
Dopo l'aggiornamento di un sito, verificare che vengano eseguite le seguenti azioni:  

-   Accertarsi che venga eseguito l'aggiornamento e l'installazione della nuova versione del software per i client assegnati a ogni sito primario  
-   Aggiornare ogni console di Configuration Manager che si connette al sito e che viene eseguita in un computer remoto dal server del sito  
-   Nei siti primari in cui si usano repliche di database per i punti di gestione, riconfigurare le repliche di database  
-   Dopo l'aggiornamento del sito, è necessario aggiornare manualmente i supporti fisici, come i file ISO per CD e DVD o unità flash USB, oppure i supporti pre-installati usati per le distribuzioni Windows To Go o resi disponibili per i fornitori di hardware. L'aggiornamento del sito aggiorna le immagini d'avvio predefinite. Non aggiorna però questi file multimediali o i dispositivi usati esternamente a Configuration Manager  
-   Aggiornare le immagini d'avvio non predefinite quando non è necessaria la versione originale (precedente) di Windows PE.  

**Azioni che influiscono su configurazioni e impostazioni**   
Quando un sito viene aggiornato a System Center Configuration Manager, alcune configurazioni e impostazioni non vengono mantenute dopo l'aggiornamento oppure vengono sostituite da nuove configurazioni predefinite. La tabella seguente include le impostazioni che non vengono mantenute o che vengono modificate e fornisce dettagli per la relativa pianificazione durante l'aggiornamento di un sito:  

-   **Software Center:**  
    I seguenti elementi di Software Center vengono reimpostati sui relativi valori predefiniti:  
    -   **Informazioni di lavoro** viene reimpostato sull'orario di ufficio: dal lunedì al venerdì dalle **05.00** alle **22.00** .  
    -   Il valore per **Manutenzione computer** è impostato su **Sospendi le attività di Software Center quando il computer si trova in modalità presentazione**.  
    -   Il valore per **Controllo remoto** è impostato sul valore delle impostazioni client assegnate al computer.  
-   **Pianificazioni dell'esecuzione del riepilogo degli aggiornamenti software:**  
     Le pianificazioni di riepilogo personalizzate per gli aggiornamenti software o i gruppi di aggiornamenti software vengono reimpostate sul valore predefinito di 1 ora. Al termine dell'aggiornamento ripristinare i valori di riepilogo personalizzati sulla frequenza necessaria.  

##  <a name="bkmk_test"></a> Testare l'aggiornamento del database del sito  
Le informazioni seguenti si applicano solo quando si aggiorna un versione precedente, ad esempio da System Center 2012 Configuration Manager a System Center Configuration Manager. Se sul sito viene già eseguito System Center Configuration Manager e si sta installando un nuovo aggiornamento, vedere [Passaggio 2: Testare l'aggiornamento del database prima di installare un aggiornamento](/sccm/core/servers/manage/install-in-console-updates#bkmk_step2) in **Prima di installare un aggiornamento nella console**.

Prima di aggiornare un sito, testare una copia del database di tale sito per l'aggiornamento.  

Per testare il database per un aggiornamento, ripristinare prima una copia del database del sito in un'istanza di SQL Server che non ospita un sito di Configuration Manager. La versione di SQL Server che si usa per ospitare la copia del database deve essere una versione di SQL Server supportata dalla versione di Configuration Manager, che corrisponde all'origine della copia del database.  

Dopo aver ripristinato il database del sito, nel computer con SQL Server eseguire il programma di installazione di Configuration Manager dalla cartella dei supporti di origine per System Center Configuration Manager con l'opzione della riga di comando **/TESTDBUPGRADE**.  

-   Per informazioni su come creare e ripristinare un backup di un database del sito, vedere [Command-line options for Setup](../../../../core/servers/deploy/install/command-line-options-for-setup.md) (Opzioni della riga di comando per l'installazione).  
-   Per informazioni sull'opzione della riga di comando **/TESTDBUPGRADE**, vedere la tabella in [Command-line options for Setup](../../../../core/servers/deploy/install/command-line-options-for-setup.md) (Opzioni della riga di comando per l'installazione).  
-   Per informazioni sulle versioni di SQL Server supportate, vedere l'argomento [Support for SQL Server versions for System Center Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md) (Supporto per le versioni di SQL Server per System Center Configuration Manager).  

> [!TIP]  
>  Integrazione di Microsoft Intune con Configuration Manager:  
>   
>  quando si esegue un aggiornamento del database di test nella copia del database del sito che risale a 5 o più giorni fa, è possibile ricevere uno dei messaggi seguenti:  
>   
>  -   WARN: Upgrade will force full sync to cloud.  
>  -   ERROR: Database upgrade will force full sync to cloud.  
>   
> Entrambi i messaggi possono essere ignorati durante il test di un aggiornamento del database, perché non indicano un errore o un problema con l'aggiornamento di prova. Indicano piuttosto che, durante l'aggiornamento effettivo, i dati del gruppo di replica di database **Cloud** potrebbero essere sincronizzati con Microsoft Intune.  

Utilizzare la procedura seguente in ogni sito di amministrazione centrale e sito primario che si pianifica di aggiornare.  

#### <a name="to-test-a-site-database-for-upgrade"></a>Per testare un database del sito per l'aggiornamento  

1.  Creare una copia del database del sito, ripristinare tale copia in un'istanza di SQL Server che usa la stessa edizione del database del sito e che non ospita un sito di Configuration Manager. Ad esempio, se il sito del database esegue un'istanza dell'edizione Enterprise di SQL Server, assicurarsi di ripristinare il database in un'istanza di SQL Server che esegue anche l'edizione Enterprise di SQL Server.  

2.  Dopo aver ripristinato la copia del database, eseguire il programma di installazione dal supporto di System Center Configuration Manager. Quando si esegue l'installazione, usare l'opzione della riga di comando **/TESTDBUPGRADE** . Se l'istanza di SQL Server che ospita la copia del database non è quella predefinita, occorre anche fornire gli argomenti della riga di comando per identificare l'istanza che ospita la copia del database del sito.  

     Ad esempio, si pianifica di aggiornare un database del sito con il nome database SMS_ABC. Si ripristina una copia di questo database del sito in un'istanza supportata di SQL Server con il nome istanza DBTest. Per testare un aggiornamento di questa copia del database del sito, usare la seguente riga di comando: **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**  

     È possibile trovare Setup.exe nel percorso seguente del supporto di origine per System Center Configuration Manager: **SMSSETUP\BIN\X64**.  

3.  Nell'istanza di SQL Server in cui si esegue il test di aggiornamento del database, monitorare ConfigMgrSetup.log nella radice dell'unità di sistema per l'avanzamento e il completamento:  

    -   se l'aggiornamento test ha esito negativo, risolvere eventuali problemi relativi al fallimento dell'aggiornamento del database del sito, creare un nuovo backup del database del sito, quindi testare l'aggiornamento della nuova copia del database del sito.  
    -   Una volta completato il processo in modo corretto, è possibile eliminare la copia del database.  

        > [!NOTE]  
        >  Non è supportato il ripristino della copia del database del sito che si utilizza per l'aggiornamento test utilizzato a sua volta come database del sito in qualsiasi sito.  

Dopo che una copia del database del sito è stata aggiornata, procedere con l'aggiornamento del sito di Configuration Manager e dei relativi database.  

##  <a name="bkmk_upgrade"></a> Aggiornare i siti  
Dopo aver completato le configurazioni di pre-aggiornamento del sito, testato l'aggiornamento del database del sito su una copia del database e scaricato i file di prerequisiti e i Language Pack per la versione Service Pack che si pianifica di installare, è possibile aggiornare il sito di Configuration Manager.  

Quando si aggiorna un sito in una gerarchia, si aggiorna innanzitutto il sito di livello superiore della gerarchia. Questo sito di livello superiore è un sito di amministrazione centrale o un sito primario autonomo. Una volta completato l'aggiornamento di un sito di amministrazione centrale, è possibile aggiornare siti primari figlio in qualsiasi ordine si desideri. Dopo aver aggiornato un sito primario, è possibile aggiornare i siti figlio secondari di tale sito oppure aggiornare i siti primari aggiuntivi prima di aggiornare eventuali siti secondari.  

Per aggiornare un sito di amministrazione centrale o un sito primario, eseguire il programma di installazione dal supporto di origine di System Center Configuration Manager. Tuttavia, non si esegue l'installazione per aggiornare siti secondari. Usare piuttosto la console di Configuration Manager per aggiornare un sito secondario dopo aver completato l'aggiornamento del relativo sito padre primario.  

Prima di aggiornare un sito, chiudere la console di Configuration Manager installata sul server del sito fino a quando l'aggiornamento del sito non è terminato. Chiudere anche tutte le console di Configuration Manager in esecuzione in computer diversi dal server del sito. Una volta completato l'aggiornamento del sito, è possibile riconnettere la console. Finché una console di Configuration Manager non viene aggiornata alla nuova versione di Configuration Manager, tale console non visualizzerà comunque alcuni oggetti e informazioni disponibili nella nuova versione di Configuration Manager.  

Seguire queste procedure per aggiornare i siti di Configuration Manager:  

#### <a name="to-upgrade-a-central-administration-site-or-primary-site"></a>Per aggiornare un sito di amministrazione centrale o primario  

1.  Verificare che l'utente che esegue l'installazione disponga dei seguenti privilegi di protezione:  

    -   Diritti di amministratore locale sul computer del server del sito.  
    -   Diritti di amministratore locale sul server di database del sito remoto per il sito, se è remoto.    </br></br>

2.  Nel computer del server del sito aprire Esplora risorse e passare a **&lt;ConfigMgSourceMedia\>\SMSSETUP\BIN\X64**.  

3.  Fare doppio clic su **Setup.exe**. Si aprirà la finestra dell'installazione guidata di System Center Configuration Manager.  

4.  Nella pagina **Prima di iniziare** fare clic su **Avanti**.  

5.  Nella pagina **Riquadro attività iniziale** , selezionare **Eseguire l'aggiornamento di questo sito Configuration Manager**, quindi fare clic su **Avanti**.  

6.  Nella pagina **Codice Product Key** fare clic su **Avanti**.  

     Se in precedenza è stata installata la versione di valutazione di Configuration Manager, è possibile selezionare **Installa versione con licenza di questo prodotto**, immettere il codice Product Key per l'installazione completa di Configuration Manager per convertire il sito alla versione completa.  

     A partire dalla versione di ottobre 2016 del supporto di base 1606 per System Center Configuration Manager, è possibile specificare la data di scadenza del contratto Software Assurance. È anche possibile specificare la **data di scadenza di Software Assurance** del contratto di licenza come utile promemoria per l'utente. Se non si immette questa data durante l'installazione, è possibile specificarla in un secondo momento dalla console di Configuration Manager.

     >  [!NOTE]   
     >  Microsoft non convalida la data di scadenza immessa e non userà tale data per la convalida della licenza.  È possibile invece usarla come promemoria della data di scadenza. Configuration Manager infatti verifica periodicamente la presenza di nuovi aggiornamenti software disponibili online. È necessario che lo stato di licenza di Software Assurance sia regolare per poter usufruire di questi aggiornamenti aggiuntivi.    

     Per altre informazioni, vedere [Licensing and branches for System Center Configuration Manager](/sccm/core/understand/learn-more-editions) (Licenze e branch per System Center Configuration Manager).

7.  Nella pagina **Condizioni di licenza software Microsoft** leggere e accettare le condizioni di licenza e fare clic su **Avanti**.  

8.  Nella pagina **Licenze prerequisite** leggere e accettare le condizioni di licenza per i prerequisiti software, quindi fare clic su **Avanti**. Il programma di installazione scarica e installa automaticamente il software sui client o sui sistemi del sito secondo necessità. Prima di procedere alla pagina successiva, è necessario selezionare tutte le caselle di controllo.  

9. Nella pagina **Download prerequisiti** specificare se il programma di installazione scaricherà i file ridistribuibili di prerequisiti più recenti, Language Pack e gli aggiornamenti del prodotto più recenti da Internet o se utilizzerà i file scaricati in precedenza, quindi fare clic su **Avanti**. Se i file sono stati scaricati in precedenza tramite Setup Downloader, selezionare **Usa file scaricati precedentemente** e specificare la cartella di download. Per altre informazioni, vedere [Setup Downloader](/sccm/core/servers/deploy/install/setup-downloader) (Downloader di installazione).

    > [!NOTE]  
    >  Quando si usano i file scaricati in precedenza, verificare che il percorso alla cartella di download contenga la versione più recente dei file.  

10. Nella pagina **Selezione della lingua server** , visualizzare l'elenco delle lingue installate al momento per il sito. Selezionare le lingue aggiuntive disponibili in questo sito per la console di Configuration Manager e per i report oppure deselezionare le lingue che non si vuole più supportare nel sito e fare clic su **Avanti**. La lingua inglese è selezionata per impostazione predefinita e non può essere rimossa.  

    > [!IMPORTANT]  
    >  Nessuna versione di Configuration Manager può usare i Language Pack di una versione precedente di Configuration Manager. Per abilitare il supporto per un lingua in un sito di Configuration Manager che viene aggiornato, è necessario usare la versione del Language Pack per quella nuova versione. Ad esempio, durante l'aggiornamento da System Center 2012 Configuration Manager a System Center Configuration Manager, se la versione di System Center Configuration Manager di un Language Pack non è disponibile nei file di prerequisiti scaricati, non sarà possibile installare il supporto per tale lingua.  

11. Nella pagina **Selezione della lingua client** , visualizzare l'elenco delle lingue installate al momento per il sito. Selezionare le lingue aggiuntive disponibili su questo sito per i computer client oppure deselezionare le lingue che non si desidera più supportare nel sito. Specificare se si desidera abilitare tutte le lingue client per i client dei dispositivi mobili, quindi fare clic su **Avanti**. La lingua inglese è selezionata per impostazione predefinita e non può essere rimossa.  

    > [!IMPORTANT]  
    >  Nessuna versione di Configuration Manager può usare i Language Pack di una versione precedente di Configuration Manager. Per abilitare il supporto per un lingua in un sito di Configuration Manager che viene aggiornato, è necessario usare la versione del Language Pack per quella nuova versione. Ad esempio, durante l'aggiornamento da System Center 2012 Configuration Manager a System Center Configuration Manager, se la versione di System Center Configuration Manager di un Language Pack non è disponibile nei file di prerequisiti scaricati, non sarà possibile installare il supporto per tale lingua.  

12. Nella pagina **Riepilogo impostazione** , fare clic su **Avanti** per avviare il Controllo prerequisiti e verificare la preparazione del server all'aggiornamento del sito.  

13. Nella pagina **Controllo installazione prerequisiti** , in assenza di segnalazioni di anomalie, fare clic su **Avanti** per aggiornare il sito e i ruoli del sistema del sito. Quando il controllo prerequisiti rileva un problema, fare clic su un elemento nell'elenco per informazioni dettagliate sulla relativa modalità di risoluzione. Risolvere tutte le anomalie associate agli elementi nell'elenco con uno stato di **Errore** prima di procedere con l'installazione. Dopo aver risolto il problema, fare clic su **Esegui controllo** per riavviare il controllo dei prerequisiti. È inoltre possibile aprire il file ConfigMgrPrereq.log nella radice dell'unità di sistema per esaminare i risultati del controllo dei prerequisiti. Il file di log può contenere informazioni aggiuntive che non vengono visualizzate nell'interfaccia utente. Per un elenco delle regole e delle descrizioni dei prerequisiti di installazione, vedere [List of Prerequisite Checks for System Center Configuration Manager](/sccm/core/servers/deploy/install/list-of-prerequisite-checks) (Elenco dei controlli dei prerequisiti per System Center Configuration Manager).  

Nella pagina **Aggiorna** il programma di installazione consente di visualizzare lo stato di avanzamento generale. Quando il programma di installazione completa l'installazione del sistema del sito e del server del sito di base, è possibile chiudere la procedura guidata. La configurazione del sito continua in background.  

#### <a name="to-upgrade-a-secondary-site"></a>Per aggiornare un sito secondario  

1.  Verificare che l'utente amministratore che esegue il programma di installazione disponga dei seguenti privilegi di protezione:  

    -   Diritti di amministratore locale sul computer del sito secondario  
    -   Ruolo di protezione Amministratore infrastruttura o Amministratore completo sul sito primario padre  
    -   Diritti di amministratore di sistema nel database del sito secondario  
    </br>
2.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

3.  Nell'area di lavoro **Amministrazione** , espandere **Configurazione sito**, quindi fare clic su **Siti**.  

4.  Selezionare il sito secondario che si desidera aggiornare e quindi, nella scheda **Home** del gruppo **Sito** , fare clic su **Aggiorna**.  

5.  Fare clic su **Sì** per confermare la decisione e per avviare l'aggiornamento del sito secondario.  

L'aggiornamento del sito secondario procede in background. Dopo aver completato l'aggiornamento, è possibile confermare lo stato della console di Configuration Manager. Per confermare lo stato, selezionare il server del sito secondario, quindi nella scheda **Home** del gruppo **Sito** fare clic su **Mostra stato installazione**.  

##  <a name="BKMK_PostUpgrade"></a> Eseguire le attività successive all'aggiornamento  
Dopo aver aggiornato un sito a un nuovo Service Pack, si potrebbe dover completare delle attività aggiuntive per completare l'aggiornamento o riconfigurare il sito. Potrebbe essere ad esempio necessario l'aggiornamento dei client di Configuration Manager o delle console di Configuration Manager, tramite la riabilitazione delle repliche di database per i punti di gestione oppure il ripristino delle impostazioni per le funzionalità di Configuration Manager che si usano e che non sono state mantenute dopo l'aggiornamento del Service Pack.  

**Problemi noti per i siti secondari:**  
- **Durante l'aggiornamento alla versione 1511:** per consentire ai client nei siti secondari di trovare il punto di gestione dal sito secondario, vale a dire dal punto di gestione proxy, aggiungere manualmente il punto di gestione a gruppi di limiti che includono anche i punti di distribuzione nel sito secondario.  

- **Durante l'aggiornamento alla versione 1606 o successive:** i punti di gestione proxy vengono aggiunti automaticamente ai gruppi di limiti che includono i punti di distribuzione nel sito secondario.


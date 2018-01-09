---
title: Eseguire la migrazione dei dati
titleSuffix: Configuration Manager
description: Informazioni su come trasferire i dati da una gerarchia di origine a una gerarchia di destinazione di System Center Configuration Manager.
ms.custom: na
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cf014eb0-f8c2-4d37-b8d7-368d63a10b89
caps.latest.revision: "11"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 8b2e55a2be2572a380ae994389a8a1c9c402aed7
ms.sourcegitcommit: ca9d15dfb1c9eb47ee27ea9b5b39c9f8cdcc0748
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/04/2018
---
# <a name="migrate-data-between-hierarchies-in-system-center-configuration-manager"></a>Eseguire la migrazione dei dati da una gerarchia all'altra in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare la migrazione per trasferire i dati da una gerarchia di origine supportata a una gerarchia di destinazione di System Center Configuration Manager.  Quando si esegue la migrazione dei dati da una gerarchia di origine:  

-   Si accede ai dati dai database del sito identificati nell'infrastruttura di origine e quindi si trasferiscono tali dati nell'ambiente corrente.  

-   La migrazione non modifica i dati nella gerarchia di origine, individua invece i dati e ne archivia una copia nel database della gerarchia di destinazione.  

Quando si pianifica la strategia di migrazione, tenere presente quanto segue:  

-   È possibile eseguire la migrazione di un'infrastruttura di Configuration Manager 2007 SP2 esistente in System Center Configuration Manager.  

-   È possibile eseguire la migrazione di alcuni o tutti i dati supportati da un sito di origine.  

-   È possibile eseguire la migrazione dei dati da un singolo sito di origine a più siti diversi nella gerarchia di destinazione.  

-   È possibile spostare i dati da più siti di origine a un singolo sito nella gerarchia di destinazione.  

##  <a name="BKMK_MigrationConcepts"></a> Concetti relativi alla migrazione  
 Nell'ambito della migrazione possono essere impiegati i concetti e i termini seguenti.  

|Concetto o termine|Altre informazioni|  
|---------------------|----------------------|  
|Gerarchia di origine|Gerarchia che esegue una versione supportata di Configuration Manager e che contiene i dati di cui si vuole eseguire la migrazione. Quando si configura la migrazione, la gerarchia di origine viene identificata quando si specifica il sito principale di una gerarchia di origine. Dopo aver specificato una gerarchia di origine, il sito di livello superiore della gerarchia di destinazione raccoglie i dati dal database del sito di origine designato per rilevare i dati che è possibile migrare.<br /><br /> Per altre informazioni, vedere [Gerarchie di origine](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Source_Hierarchies) in [Pianificazione di una strategia per la gerarchia di origine in System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Siti di origine|I siti nella gerarchia di origine che includono i dati che è possibile migrare alla gerarchia di destinazione.<br /><br /> Per altre informazioni, vedere [Siti di origine](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Source_Sites) in [Pianificazione di una strategia per la gerarchia di origine in System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Gerarchia di destinazione|Una gerarchia di System Center Configuration Manager in cui viene eseguita la migrazione per l'importazione dei dati da una gerarchia di origine.|  
|Raccolta dati|Il processo continuo di rilevamento delle informazioni in una gerarchia di origine che è possibile migrare nella gerarchia di destinazione. Configuration Manager controlla la gerarchia di origine in una pianificazione per rilevare eventuali modifiche alle informazioni contenute nella gerarchia migrate in precedenza e che è possibile aggiornare nella gerarchia di destinazione.<br /><br /> Per altre informazioni, vedere [Raccolta dati](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering) in [Pianificazione di una strategia per la gerarchia di origine in System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Processi di migrazione|Il processo di configurazione di oggetti specifici da migrare e quindi la gestione della migrazione di tali oggetti nella gerarchia di destinazione.<br /><br /> Per altre informazioni, vedere [Pianificazione di una strategia di processo di migrazione in System Center Configuration Manager](../../core/migration/planning-a-migration-job-strategy.md)|  
|Migrazione client|Il processo di trasferimento delle informazioni che i client utilizzano dal database del sito di origine al database della gerarchia di destinazione. Tale processo di migrazione dei dati è quindi seguito da un aggiornamento del software client dei dispositivi alla versione del software client dalla gerarchia di destinazione.<br /><br /> Per ulteriori informazioni, vedere [Pianificazione di una strategia di processo di migrazione in System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).|  
|Punti di distribuzione condivisi|I punti di distribuzione della gerarchia di origine che vengono condivisi con la gerarchia di destinazione durante il periodo di migrazione.<br /><br /> Durante il periodo di migrazione, i client assegnati ai siti nella gerarchia di destinazione possono ottenere il contenuto dai punti di distribuzione condivisi.<br /><br /> Per altre informazioni, vedere [Condividere punti di distribuzione tra gerarchie di origine e destinazione](../../core/migration/planning-a-content-deployment-migration-strategy.md#About_Shared_DPs_in_Migration) in [Pianificazione di una strategia di migrazione per la distribuzione del contenuto in System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).|  
|Monitoraggio della migrazione|Il processo di monitoraggio delle attività di migrazione. È possibile monitorare lo stato e l'esito migrazione dal nodo **Migrazione** nell'area di lavoro **Amministrazione** .<br /><br /> Per altre informazioni, vedere [Pianificazione del monitoraggio dell'attività di migrazione in System Center Configuration Manager](../../core/migration/planning-to-monitor-migration-activity.md).|  
|Interrompere la raccolta dati|Il processo di interruzione della raccolta dati dai siti di origine. Quando non sono più disponibili dati da migrare da una gerarchia di origine oppure se si vuole sospendere le attività relative alla migrazione, è possibile configurare la gerarchia di destinazione per l'interruzione della raccolta dati da tale gerarchia.<br /><br /> Per altre informazioni, vedere [Raccolta dati](../../core/migration/planning-a-source-hierarchy-strategy.md#BKMK_Data_Gathering) in [Pianificazione di una strategia per la gerarchia di origine in System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).|  
|Pulire i dati della migrazione|Il processo di completamento della migrazione da una gerarchia di origine tramite la rimozione delle informazioni sulla migrazione dal database delle gerarchie di destinazione.<br /><br /> Per altre informazioni, vedere [Pianificazione del completamento della migrazione in System Center Configuration Manager](../../core/migration/planning-to-complete-migration.md).|  

## <a name="typical-workflow-for-migration"></a>Flusso di lavoro tipico per la migrazione  
Per configurare un flusso di lavoro per la migrazione:

1.  Specificare una gerarchia di origine supportata.  

2.  Configurare la raccolta dati. La raccolta dati consente a Configuration Manager di raccogliere informazioni sui dati che è possibile migrare dalla gerarchia di origine.  

     Configuration Manager ripete automaticamente il processo di raccolta dati in una pianificazione semplice finché il processo non viene interrotto. Per impostazione predefinita, il processo di raccolta dati si ripete ogni quattro ore in modo che Configuration Manager possa rilevare le modifiche ai dati nella gerarchia di origine che è possibile migrare. La raccolta dati è inoltre necessaria per condividere i punti di distribuzione dalla gerarchia di origine alla gerarchia di destinazione.  

3.  Creare processi di migrazione per la migrazione di dati tra la gerarchia di origine e la gerarchia di destinazione.  

4.  È possibile interrompere il processo di raccolta dati in qualsiasi momento utilizzando il comando **Interrompi raccolta dati** . Quando si interrompe una raccolta dati, Configuration Manager non rileva più le modifiche ai dati nella gerarchia di origine e non è più in grado di condividere i punti di distribuzione tra le gerarchie di origine e destinazione. In genere, è possibile utilizzare questa azione se si prevede di non migrare più i dati né di condividere i punti di distribuzione dalla gerarchia di origine.  

5.  Facoltativamente, dopo che la raccolta dati è stata interrotta in tutti i siti per la gerarchia di origine, è possibile pulire i dati della migrazione utilizzando il comando **Pulisci dati migrazione** . Questo comando consente di eliminare i dati cronologici sulla migrazione da una gerarchia di origine dal database della gerarchia di destinazione.  

Dopo aver completato la migrazione dei dati da una gerarchia di origine di Configuration Manager che non verrà più usata per gestire l'ambiente, è possibile rimuovere le autorizzazioni di tale infrastruttura e gerarchia di origine.  

##  <a name="BKMK_MigrationScenarios"></a> Scenari di migrazione  
 Configuration Manager supporta gli scenari di migrazione seguenti.  

> [!NOTE]  
>  L'espansione di una gerarchia con un sito autonomo in una gerarchia con un sito di amministrazione centrale non viene classificata come migrazione. Per informazioni sull'espansione della gerarchia, vedere [Espandere un sito primario autonomo](../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand) in [Usare l'installazione guidata per installare i siti](../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  

### <a name="migration-from-configuration-manager-2007-hierarchies"></a>Migrazione da gerarchie di Configuration Manager 2007  
 Quando si usa la migrazione per migrare i dati da Configuration Manager 2007 è possibile mantenere l'investimento nell'infrastruttura del sito esistente e ottenere i vantaggi seguenti:  

|Vantaggio|Altre informazioni|  
|-------------|----------------------|  
|Miglioramenti del database del sito|Il database di System Center Configuration Manager supporta Unicode.|  
|Replica di database tra siti|La replica in System Center Configuration Manager è basata su Microsoft SQL Server. In questo modo, le prestazioni del trasferimento dati da sito a sito vengono migliorate.|  
|Gestione incentrata sull'utente|In System Center Configuration Manager le attività di gestione sono incentrate sugli utenti. Ad esempio, è possibile distribuire il software a un utente anche se non si conosce il nome del dispositivo per tale utente. System Center Configuration Manager offre inoltre agli utenti un maggiore controllo sul software da installare nei dispositivi e su quando installarlo.|  
|Semplificazione della gerarchia|In System Center Configuration Manager il tipo di sito di amministrazione centrale e le modifiche apportate al comportamento dei siti primari e secondari consentono di creare una gerarchia di siti più semplice che richiede una larghezza di banda di rete inferiore e un numero minore di server.|  
|Amministrazione basata su ruoli|Questo modello di sicurezza centrale in System Center Configuration Manager offre sicurezza a livello di gerarchia e una gestione che corrisponde ai requisiti aziendali e amministrativi.|  

> [!NOTE]  
>  A causa delle modifiche di progettazione introdotte in System Center 2012 Configuration Manager, non è possibile aggiornare l'infrastruttura di Configuration Manager 2007 a System Center Configuration Manager. L'aggiornamento sul posto è supportato da System Center 2012 Configuration Manager a System Center Configuration Manager.  

### <a name="migration-from-configuration-manager-2012-or-another-system-center-configuration-manager-hierarchy"></a>Migrazione da Configuration Manager 2012 o un'altra gerarchia di System Center Configuration Manager  
 Il processo di migrazione dei dati da una gerarchia di System Center 2012 Configuration Manager o di System Center Configuration Manager è uguale. Il processo include la migrazione di dati da più gerarchie di origine a una singola gerarchia di destinazione, ad esempio nel caso in cui la società acquisisce risorse aggiuntive già gestite da Configuration Manager. È anche possibile eseguire la migrazione dei dati da un ambiente di test all'ambiente di produzione di Configuration Manager. Ciò consente di preservare gli investimenti effettuati per l'ambiente di testing di Configuration Manager.  

## <a name="additional-topics-for-migration"></a>Altri argomenti relativi alla migrazione:  

-   [Pianificazione della migrazione a System Center Configuration Manager](../../core/migration/planning-for-migration.md)  

-   [Configurazione di gerarchie di origine e siti di origine per la migrazione a System Center Configuration Manager](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)  

-   [Operazioni per la migrazione a System Center Configuration Manager](../../core/migration/operations-for-migration.md)  

-   [Sicurezza e privacy per la migrazione a System Center Configuration Manager](../../core/migration/security-and-privacy-for-migration.md)  

## <a name="see-also"></a>Vedere anche  
 [Iniziare a usare System Center Configuration Manager](../../core/servers/deploy/start-using.md)

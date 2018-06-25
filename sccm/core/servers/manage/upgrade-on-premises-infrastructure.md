---
title: Aggiornare l'infrastruttura locale
titleSuffix: Configuration Manager
description: Informazioni su come aggiornare l'infrastruttura, ad esempio SQL Server e il sistema operativo dei sistemi del sito.
ms.date: 05/23/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dc433d63eb647ef7a0a88ada212f949783ac25c0
ms.sourcegitcommit: 4b8afbd08ecf8fd54950eeb630caf191d3aa4767
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/21/2018
ms.locfileid: "34474252"
---
# <a name="upgrade-on-premises-infrastructure-that-supports-system-center-configuration-manager"></a>Aggiornare l'infrastruttura locale che supporta System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le informazioni disponibili in questo articolo consentono di aggiornare l'infrastruttura server che esegue Configuration Manager.  

 - Per eseguire l'*aggiornamento* a System Center Configuration Manager Current Branch da una versione precedente di Configuration Manager, vedere [Eseguire l'aggiornamento a System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).

- Per *aggiornare* l'infrastruttura di System Center Configuration Manager Current Branch a una versione più recente, vedere [Aggiornamenti per System Center Configuration Manager](/sccm/core/servers/manage/updates).



##  <a name="BKMK_SupConfigUpgradeSiteSrv"></a> Aggiornare il sistema operativo dei sistemi del sito  
 Configuration Manager supporta l'aggiornamento sul posto del sistema operativo dei server che ospitano un server del sito e dei server remoti che ospitano un ruolo qualsiasi del sistema del sito, nelle situazioni seguenti:  

-   Aggiornamento sul posto a una versione di Service Pack di Windows Server successiva purché il livello di Service Pack di Windows risultante sia comunque supportato da Configuration Manager.  
-   Aggiornamento sul posto:
    - Da Windows Server 2012 R2 a Windows Server 2016 ([vedere dettagli aggiuntivi](#bkmk_2016)).
    - Da Windows Server 2012 a Windows Server 2016 ([vedere dettagli aggiuntivi](#bkmk_2016)).
    - Da Windows Server 2012 a Windows Server 2012 R2 ([vedere dettagli aggiuntivi](#bkmk_2012r2)).
    - Da Windows Server 2008 R2 a Windows Server 2012 R2 ([vedere dettagli aggiuntivi](#bkmk_from2008r2)).

    > [!WARNING]  
    >  Prima di eseguire l'aggiornamento a un sistema operativo diverso, *è necessario disinstallare WSUS* dal server. È possibile conservare il database WSUS e ricollegarlo dopo la reinstallazione di WSUS. Per altre informazioni su questo passaggio critico, vedere la sezione "Funzionalità nuove e modificate" in [Panoramica di Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx), nella documentazione di Windows Server.  

Per aggiornare un server, eseguire la procedura di aggiornamento indicata dal sistema operativo interessato dall'aggiornamento. Vedere gli articoli seguenti:
  -  [Opzioni di aggiornamento per Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) nella documentazione di Windows Server.  
  - [Opzioni di aggiornamento e conversione per Windows Server 2016](/windows-server/get-started/supported-upgrade-paths) nella documentazione di Windows Server.

### <a name="bkmk_2016"></a> Eseguire l'aggiornamento da Windows Server 2012 o Windows Server 2012 R2 a 2016
Quando si esegue l'aggiornamento di Windows Server 2012 o Windows Server 2012 R2 a Windows Server 2016, sono valide le considerazioni seguenti:


#### <a name="before-upgrade"></a>Prima di eseguire l'aggiornamento  
-   Rimuovere il client di System Center Endpoint Protection (SCEP). Windows Server 2016 è predefinito con Windows Defender, che sostituisce il client SCEP. La presenza del client SCEP può impedire un aggiornamento a Windows Server 2016.
-   Rimuovere il ruolo WSUS dal server, se installato. È possibile conservare il database WSUS e ricollegarlo dopo la reinstallazione di WSUS.

#### <a name="after-upgrade"></a>Dopo l'aggiornamento   
-   Assicurarsi che Windows Defender sia abilitato, impostato per l'avvio automatico e in esecuzione.
-   Verificare che i servizi di Configuration Manager seguenti siano in esecuzione:
  -     SMS_EXECUTIVE
  -     SMS_SITE_COMPONENT_MANAGER


-   Assicurarsi che i sevizi **Attivazione processo Windows** e **WWW/W3svc** siano abilitati, impostati per l'avvio automatico e in esecuzione per i ruoli del sistema del sito seguenti. Durante l'aggiornamento questi servizi vengono disabilitati:
  -     Server del sito
  -     Punto di gestione
  -     Punto per servizi Web del Catalogo applicazioni
  -     Punto per siti Web del Catalogo applicazioni

-   Assicurarsi che ogni server che ospita un ruolo del sistema del sito continui a soddisfare tutti i [prerequisiti per i ruoli del sistema del sito](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) in esecuzione in tale server. Potrebbe essere necessario ad esempio reinstallare BITS, WSUS, o configurare impostazioni specifiche per IIS.

-   Dopo aver ripristinato i prerequisiti mancanti, riavviare di nuovo il server per verificare che i servizi siano stati avviati e siano operativi.

-   Se si sta aggiornando il server del sito primario, [eseguire una reimpostazione del sito](/sccm/core/servers/manage/modify-your-infrastructure#bkmk_reset).

#### <a name="known-issue-for-remote-configuration-manager-consoles"></a>Problema noto per le console remote di Configuration Manager   
Può succedere che, dopo aver aggiornato il server del sito o un server che ospita un'istanza di SMS_Provider per Windows Server 2016, gli utenti amministratori non riescano a connettere una console di Configuration Manager al sito. Per risolvere questo problema, è necessario ripristinare manualmente le autorizzazioni per il gruppo SMS Admins in WMI. Le autorizzazioni devono essere impostate nel server del sito e in ogni server remoto che ospita un'istanza del provider SMS:

1. Nei server applicabili aprire Microsoft Management Console (MMC), aggiungere lo snap-in per **Controllo WMI** e quindi selezionare **Computer locale**.
2. In MMC aprire le **Proprietà** di **Controllo WMI (computer locale)** e selezionare la scheda **Sicurezza**.
3. Espandere l'albero sotto Radice, selezionare il nodo **SMS** e quindi scegliere **Sicurezza**.  Assicurarsi che il gruppo **SMS Admins** abbia le autorizzazioni seguenti:
  -     Abilita account
  -     Abilita remoto
4. Nella scheda **Sicurezza** sotto il nodo **SMS** selezionare il nodo **site_&lt;codicesito>** e quindi scegliere **Sicurezza**. Assicurarsi che il gruppo **SMS Admins** abbia le autorizzazioni seguenti:
  -   Esegui metodi
  -   Scrittura provider
  -   Abilita account
  -   Abilita remoto
5. Salvare le autorizzazioni per ripristinare l'accesso per la console di Configuration Manager.


### <a name="bkmk_2012r2"></a> Da Windows Server 2012 a Windows Server 2012 R2

#### <a name="before-upgrade"></a>Prima dell'aggiornamento  
-   Rimuovere il ruolo WSUS dal server, se installato. È possibile conservare il database WSUS e ricollegarlo dopo la reinstallazione di WSUS.

#### <a name="after-upgrade"></a>Dopo l'aggiornamento  
  - Assicurarsi che Servizi di distribuzione Windows sia avviato e in esecuzione per i ruoli del sistema del sito seguenti. Questo servizio viene arrestato durante l'aggiornamento:
    - Server del sito
    - Punto di gestione
    - Punto per servizi Web del Catalogo applicazioni
    - Punto per siti Web del Catalogo applicazioni

  -     Assicurarsi che i sevizi **Attivazione processo Windows** e **WWW/W3svc** siano abilitati, impostati per l'avvio automatico e in esecuzione per i ruoli del sistema del sito seguenti. Durante l'aggiornamento questi servizi vengono disabilitati:
    -   Server del sito
    -   Punto di gestione
    -   Punto per servizi Web del Catalogo applicazioni
    -   Punto per siti Web del Catalogo applicazioni


  -     Assicurarsi che ogni server che ospita un ruolo del sistema del sito continui a soddisfare tutti i [prerequisiti per i ruoli del sistema del sito](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) in esecuzione in tale server. Potrebbe essere necessario ad esempio reinstallare BITS, WSUS, o configurare impostazioni specifiche per IIS.

  Dopo aver ripristinato i prerequisiti mancanti, riavviare di nuovo il server per verificare che i servizi siano stati avviati e siano operativi.

### <a name="bkmk_from2008r2"></a> Eseguire l'aggiornamento da Windows Server 2008 R2 a Windows Server 2012 R2
Questo scenario di aggiornamento del sistema operativo presenta le condizioni seguenti:  

#### <a name="before-upgrade"></a>Prima dell'aggiornamento  
-   Disinstallare WSUS 3.2.  
    Prima di eseguire l'aggiornamento di un sistema operativo server a Windows Server 2012 R2, è necessario disinstallare WSUS 3.2 dal server. Per informazioni su questo passaggio critico, vedere la sezione Funzionalità nuove e modificate in [Panoramica di Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx), nella documentazione di Windows Server.

#### <a name="after-upgrade"></a>Dopo l'aggiornamento  
  - Assicurarsi che Servizi di distribuzione Windows sia avviato e in esecuzione per i ruoli del sistema del sito seguenti. Questo servizio viene arrestato durante l'aggiornamento:
    - Server del sito
    - Punto di gestione
    - Punto per servizi Web del Catalogo applicazioni
    - Punto per siti Web del Catalogo applicazioni


  -     Assicurarsi che i sevizi **Attivazione processo Windows** e **WWW/W3svc** siano abilitati, impostati per l'avvio automatico e in esecuzione per i ruoli del sistema del sito seguenti. Durante l'aggiornamento questi servizi vengono disabilitati:
    -   Server del sito
    -   Punto di gestione
    -   Punto per servizi Web del Catalogo applicazioni
    -   Punto per siti Web del Catalogo applicazioni


  -     Assicurarsi che ogni server che ospita un ruolo del sistema del sito continui a soddisfare tutti [i prerequisiti per i ruoli del sistema del sito](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) in esecuzione su tale server. Potrebbe essere necessario ad esempio reinstallare BITS, WSUS, o configurare impostazioni specifiche per IIS.

  Dopo aver ripristinato i prerequisiti mancanti, riavviare di nuovo il server per verificare che i servizi siano stati avviati e siano operativi.


### <a name="unsupported-upgrade-scenarios"></a>Scenari di aggiornamento non supportati
Sono solitamente richiesti, ma non sono supportati da Configuration Manager gli scenari di aggiornamento di Windows Server seguenti:  

-   Da Windows Server 2008 a Windows Server 2012 o versione successiva  
-   Da Windows Server 2008 R2 a Windows Server 2012



##  <a name="BKMK_SupConfigUpgradeClient"></a> Aggiornare il sistema operativo dei client di Configuration Manager  
 Configuration Manager supporta un aggiornamento sul posto del sistema operativo per client di Configuration Manager nelle situazioni seguenti:  

-   Aggiornamento sul posto a una versione di Service Pack di Windows successiva purché il livello di Service Pack risultante sia comunque supportato da Configuration Manager.  

-   Aggiornamento sul posto di Windows da una versione supportata di Windows 10. Per altre informazioni, vedere [Aggiornare Windows alla versione più recente](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   Aggiornamenti di manutenzione da build a build di Windows 10. Per altre informazioni, vedere [Gestire Windows come servizio](../../../osd/deploy-use/manage-windows-as-a-service.md).  



##  <a name="BKMK_SupConfigUpgradeDBSrv"></a> Aggiornare SQL Server sul server di database del sito  
  Configuration Manager supporta un aggiornamento sul posto di SQL Server da una versione supportata di SQL sul server di database del sito. Gli scenari di aggiornamento di SQL Server descritti in questa sezione sono supportati da Configuration Manager e includono i requisiti per ogni scenario.

 Per informazioni sulle versioni di SQL Server supportate da Configuration Manager, vedere [Supporto per le versioni di SQL Server](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

 ### <a name="upgrade-the-service-pack-version-of-sql-server"></a>Aggiornamento della versione del Service Pack di SQL Server    
 Configuration Manager supporta l’aggiornamento sul posto di SQL Server a una versione di Service Pack successiva purché il livello di Service Pack di SQL Server risultante sia comunque supportato da Configuration Manager.

 In presenza di più siti di Configuration Manager in una gerarchia, ogni sito può eseguire una versione diversa del Service pack di SQL Server. Non esiste alcuna limitazione per l'ordine in cui i siti si aggiornano la versione del Service Pack di SQL Server usato per il database del sito.

### <a name="upgrade-to-a-new-version-of-sql-server"></a>Eseguire l'aggiornamento a una nuova versione di SQL Server   
 Configuration Manager supporta l'aggiornamento sul posto di SQL Server alle versione seguenti:

 - SQL Server 2017
 - SQL Server 2016  
 - SQL Server 2014  

Quando si aggiorna la versione di SQL Server che ospita il database del sito, è necessario aggiornare la versione di SQL Server usata nei siti nell'ordine seguente:

 1. Eseguire l'aggiornamento di SQL Server prima nel sito di amministrazione centrale.
 2. Aggiornare i siti secondari prima di eseguire l’aggiornamento del sito primario padre di un sito secondario.
 3. Aggiornare per ultimo i siti primari padre. Questi siti includono sia i siti primari figlio che fanno riferimento a un sito di amministrazione centrale sia i siti primari autonomi che sono siti di livello superiore di una gerarchia.

### <a name="sql-server-cardinality-estimation-level-and-the-site-database"></a>Livello di stima della cardinalità di SQL Server e database del sito   
Quando un database del sito viene aggiornato da una versione precedente di SQL Server, il database mantiene il livello CE (Cardinality Estimation, Stima della cardinalità) SQL esistente se questo corrisponde al minimo consentito per l'istanza di SQL Server. L'aggiornamento di SQL Server con un database a un livello di compatibilità inferiore a quello consentito imposta automaticamente il database sul livello di compatibilità più basso consentito da SQL Server.

La tabella seguente identifica i livelli di compatibilità consigliati per i database del sito di Configuration Manager:

|Versione di SQL Server | Livelli di compatibilità supportati |Livello consigliato|
|----------------|--------------------|--------|
| SQL Server 2017 | 140, 130, 120, 110  | 140 |
| SQL Server 2016 | 130, 120, 110  | 130 |
| SQL Server 2014 | 120, 110      | 110 |

Per identificare il livello di compatibilità CE di SQL Server in uso per il database del sito, eseguire la query SQL seguente nel server di database del sito:  
`SELECT name, compatibility_level FROM sys.databases`

 Per altre informazioni sui livelli di compatibilità CE di SQL e su come impostarli, vedere [Livello di compatibilità ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2017).


Per altre informazioni sull'aggiornamento di SQL Server, vedere la documentazione di SQL Server seguente:
-   [Eseguire l'aggiornamento a SQL Server 2017](/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)
-   [Eseguire l'aggiornamento a SQL Server 2016](/sql/database-engine/install-windows/supported-version-and-edition-upgrades)
-   [Eseguire l'aggiornamento a SQL Server 2014](http://technet.microsoft.com/library/ms143393\(v=sql.120))  



### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>Per aggiornare SQL Server nel server di database del sito  

1.  Arrestare tutti i servizi di Configuration Manager nel sito.  
2.  Aggiornare SQL Server a una versione supportata.  
3.  Riavviare i servizi di Configuration Manager.  

> [!NOTE]  
>  Quando nel sito di amministrazione centrale si passa da SQL Server Standard a SQL Server Enterprise o Datacenter, la partizione del database che limita il numero di client supportati dalla gerarchia non cambia.

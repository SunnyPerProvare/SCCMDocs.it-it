---
title: Aggiornare l&quot;infrastruttura locale | Microsoft Docs
description: Informazioni su come aggiornare l&quot;infrastruttura, ad esempio SQL Server e il sistema operativo del sito di sistemi del sito.
ms.custom: na
ms.date: 10/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 8b4c80aa092369ec251757d82a1b4bb2863aa96a
ms.openlocfilehash: f3742dcb930444bab7eb02374fd77ebd0e455734


---
# <a name="upgrade-on-premises-infrastructure-that-supports-system-center-configuration-manager"></a>Aggiornare l'infrastruttura locale che supporta System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le informazioni seguenti consentono di aggiornare l'infrastruttura che esegue System Center Configuration Manager.  

##  <a name="a-namebkmksupconfigupgradesitesrva-upgrade-site-operating-system-of-site-systems"></a><a name="BKMK_SupConfigUpgradeSiteSrv"></a> Aggiornare il sistema operativo dei sistemi del sito  
 Configuration Manager supporta l'aggiornamento sul posto del sistema operativo dei server che ospitano un server del sito e dei server remoti che ospitano un ruolo qualsiasi del sistema del sito, nelle situazioni seguenti:  

-   Aggiornamento sul posto a una versione di Service Pack di Windows Server successiva purché il livello di Service Pack di Windows risultante sia comunque supportato da Configuration Manager.  
-   Aggiornamento sul posto:
    - Da Windows Server 2012 R2 a Windows Server 2016 ([vedere dettagli aggiuntivi](#upgrade-windows-server-2012-r2-to-2016))
    - Da Windows Server 2012 a Windows Server 2012 R2 ([vedere dettagli aggiuntivi](#upgrade-windows-server-2012-to-windows-server-2012-r2))
    - A partire da Configuration Manager versione 1602, è anche supportato l'aggiornamento di Windows Server 2008 R2 a Windows Server 2012 R2 ([vedere dettagli aggiuntivi](#upgrade-windows-server-2008-r2-to-windows-server-2012-r2))

    > [!WARNING]  
    >  Prima di eseguire l'aggiornamento a Windows Server 2012 R2, **è necessario disinstallare WSUS 3.2** dal server.  
    >   
    >  Per informazioni su questo passaggio critico, vedere la sezione Funzionalità nuove e modificate in [Panoramica di Windows Server Update Services](https://technet.microsoft.com/library/hh852345.aspx) nella documentazione di Windows Server.  

Per aggiornare un server, eseguire la procedura di aggiornamento indicata dal sistema operativo interessato dall'aggiornamento.  Vedere la documentazione seguente:
  -  [Opzioni di aggiornamento per Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) nella documentazione di Windows Server.  
  - [Opzioni di aggiornamento e conversione per Windows Server 2016](https://technet.microsoft.com/windows-server-docs/get-started/supported-upgrade-paths) nella documentazione di Windows Server.

### <a name="upgrade-windows-server-2012-r2-to-2016"></a>Eseguire l'aggiornamento da Windows Server 2012 R2 a 2016  
Questo scenario di aggiornamento del sistema operativo presenta le condizioni seguenti:

**Prima di eseguire l'aggiornamento:**  
-   Rimuovere il client di System Center Endpoint Protection (SCEP). Windows Server 2016 è predefinito con Windows Defender, che sostituisce il client SCEP. La presenza del client SCEP può impedire l'aggiornamento a Windows Server 2016.

**Dopo aver eseguito l'aggiornamento:**
-   Assicurarsi che Windows Defender sia abilitato, impostato per l'avvio automatico e in esecuzione.
-   Verificare che i servizi di Configuration Manager seguenti siano in esecuzione:
  -     SMS_EXECUTIVE
  -     SMS_SITE_COMPONENT_MANAGER


-   Assicurarsi che i sevizi **Attivazione processo Windows** e **WWW/W3svc** siano abilitati, impostati per l'avvio automatico e in esecuzione per i ruoli del sistema del sito seguenti. Durante l'aggiornamento questi servizi vengono disabilitati:
  -     Server del sito
  -     Punto di gestione
  -     Punto per servizi Web del Catalogo applicazioni
  -     Punto per siti Web del Catalogo applicazioni


-   Assicurarsi che ogni server che ospita un ruolo del sistema del sito continui a soddisfare tutti [i prerequisiti per i ruoli del sistema del sito](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) in esecuzione su tale server. Potrebbe essere necessario ad esempio reinstallare BITS, WSUS, o configurare impostazioni specifiche per IIS.

  Dopo aver ripristinato i prerequisiti mancanti, riavviare di nuovo il server per verificare che i servizi siano stati avviati e siano operativi.

**Problema noto per le console remota di Configuration Manager:**  
Può succedere che, dopo aver aggiornato il server del sito o un server che ospita un'istanza di SMS_Provider per Windows Server 2016, gli utenti amministratori non riescano a connettere una console di Configuration Manager al sito. Per risolvere questo problema, è necessario ripristinare manualmente le autorizzazioni per il gruppo SMS Admins in WMI. Le autorizzazioni devono essere impostate nel server del sito e in ogni server remoto che ospita un'istanza del provider SMS:

1. Nei server applicabili aprire Microsoft Management Console (MMC), aggiungere lo snap-in per **Controllo WMI** e selezionare **Computer locale**.
2. In MMC aprire le **Proprietà** di **Controllo WMI (computer locale)** e selezionare la scheda **Sicurezza**.
3. Espandere l'albero sotto Radice, selezionare il nodo **SMS** e fare clic su **Sicurezza**.  Assicurarsi che il gruppo **SMS Admins** abbia le autorizzazioni seguenti:
  -     Abilita account
  -     Abilita remoto
4. Nella scheda **Sicurezza**, sotto il nodo SMS, selezionare il nodo **site_&lt;sitecode>** e fare clic su **Sicurezza**. Assicurarsi che il gruppo **SMS Admins** abbia le autorizzazioni seguenti:
  -   Esegui metodi
  -   Scrittura provider
  -   Abilita account
  -   Abilita remoto
5. Salvare le autorizzazioni per ripristinare l'accesso per la console di Configuration Manager.

### <a name="windows-server-2012-to-windows-server-2012-r2"></a>Eseguire l'aggiornamento da Windows Server 2012 a Windows Server 2012 R2

**Prima di eseguire l'aggiornamento:**
-  A differenza di altri scenari supportati, per questo scenario non sono previste altre considerazioni prima di eseguire l'aggiornamento.

**Dopo aver eseguito l'aggiornamento:**
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

### <a name="upgrade-windows-server-2008-r2-to-windows-server-2012-r2"></a>Eseguire l'aggiornamento da Windows Server 2008 R2 a Windows Server 2012 R2
Questo scenario di aggiornamento del sistema operativo presenta le condizioni seguenti:  

**Prima di eseguire l'aggiornamento:**
-   Disinstallare WSUS 3.2.  
    Prima di eseguire l'aggiornamento di un sistema operativo a Windows Server 2012 R2, è necessario disinstallare WSUS 3.2 dal server. Per informazioni su questo passaggio critico, vedere la sezione Funzionalità nuove e modificate in Panoramica di Windows Server Update Services, nella documentazione di Windows Server.

**Dopo aver eseguito l'aggiornamento:**
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



##  <a name="a-namebkmksupconfigupgradeclienta-upgrade-the-operating-system-of-configuration-manager-clients"></a><a name="BKMK_SupConfigUpgradeClient"></a> Aggiornare il sistema operativo dei client di Configuration Manager  
 Configuration Manager supporta un aggiornamento sul posto del sistema operativo per client di Configuration Manager nelle situazioni seguenti:  

-   Aggiornamento sul posto a una versione di Service Pack di Windows successiva purché il livello di Service Pack risultante sia comunque supportato da Configuration Manager.  

-   Aggiornamento sul posto di Windows da una versione supportata di Windows 10. Per altre informazioni, vedere [Aggiornare Windows alla versione più recente con System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   Aggiornamenti di manutenzione da build a build di Windows 10.  Per altre informazioni, vedere [Gestire Windows come servizio con System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md).  

##  <a name="a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server"></a><a name="BKMK_SupConfigUpgradeDBSrv"></a> Aggiornare SQL Server sul server di database del sito  
  Configuration Manager supporta un aggiornamento sul posto di SQL Server da una versione supportata di SQL sul server di database del sito. Seguono informazioni dettagliate sugli scenari di aggiornamento di SQL Server supportati da Configuration Manager e i requisiti per ogni scenario.

 Per informazioni sulle versioni di SQL Server supportate da Configuration Manager, vedere [Support for SQL Server versions for System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md) (Supporto per le versioni di SQL Server per System Center Configuration Manager).  

 **Eseguire l'aggiornamento della versione Service Pack di SQL Server:**    
 Configuration Manager supporta l’aggiornamento sul posto di SQL Server a una versione di Service Pack successiva purché il livello di Service Pack di SQL Server risultante sia comunque supportato da Configuration Manager.

 Quando in una gerarchia sono presenti più siti di Configuration Manager, ogni sito può eseguire una versione diversa di Service Pack di SQL Server. Non esistono limitazioni per l'ordine in cui i siti eseguono l'aggiornamento della versione di Service Pack di SQL Server usata per il database del sito.

 **Eseguire l'aggiornamento a una nuova versione di SQL Server:**   
 Configuration Manager supporta l'aggiornamento sul posto di SQL Server alle versione seguenti:

 - SQL Server 2012  
 - SQL Server 2014  
 - SQL Server 2016  

Quando si aggiorna la versione di SQL Server che ospita il database del sito, è necessario aggiornare la versione di SQL Server usata nei siti nell'ordine seguente:

 1. Eseguire l'aggiornamento di SQL Server prima nel sito di amministrazione centrale.
 2. Aggiornare i siti secondari prima di eseguire l’aggiornamento del sito primario padre di un sito secondario.
 3. Aggiornare per ultimo i siti primari padre. Sono inclusi sia i siti primari figlio che fanno riferimento a un sito di amministrazione centrale sia i siti primari autonomi che sono siti di livello superiore di una gerarchia.

**Livello di stima della cardinalità di SQL Server e database del sito:**   
Quando un database del sito viene aggiornato da una versione precedente di SQL Server, il database mantiene il livello CE (Cardinality Estimation, Stima della cardinalità) SQL esistente se questo corrisponde al minimo consentito per l'istanza di SQL Server. L'aggiornamento di SQL Server con un database a un livello di compatibilità inferiore a quello consentito imposta automaticamente il database al livello di compatibilità più basso consentito da SQL.

La tabella seguente identifica i livelli di compatibilità consigliati per i database del sito di Configuration Manager:

|Versione di SQL Server | Livelli di compatibilità supportati |Livello consigliato|
|----------------|--------------------|--------|
| SQL Server 2016| 130, 120, 110, 100 | 130|
| SQL Server 2014| 120, 110, 100      | 110|

Per identificare il livello di compatibilità CE di SQL Server in uso per il database del sito, eseguire la query SQL seguente sul server di database del sito: **SELECT name, compatibility_level FROM sys.databases**

 Per altre informazioni sui livelli di compatibilità CE di SQL e su come impostarli, vedere [Livello di compatibilità ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx).


**Per altre informazioni su SQL Server, vedere la relativa documentazione di SQL Server su TechNet:**  
-   [Eseguire l'aggiornamento a SQL Server 2014](http://technet.microsoft.com/library/ms143393\(v=sql.120)  
-   [Eseguire l'aggiornamento a SQL Server 2012](http://technet.microsoft.com/library/ms143393\(v=sql.110)
-   [Eseguire l'aggiornamento a SQL Server 2016](https://technet.microsoft.com/library/bb677622(v=sql.130))



### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>Per aggiornare SQL Server nel server di database del sito  

1.  Arrestare tutti i servizi di Configuration Manager nel sito.  
2.  Aggiornare SQL Server a una versione supportata.  
3.  Riavviare i servizi di Configuration Manager.  

> [!NOTE]  
>  Quando nel sito di amministrazione centrale si passa da SQL Server Standard a SQL Server Enterprise o Datacenter, la partizione del database che limita il numero di client supportati dalla gerarchia non cambia.



<!--HONumber=Dec16_HO3-->



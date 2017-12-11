---
title: "Funzionalità deprecate"
titleSuffix: Configuration Manager
description: "Informazioni su funzionalità, prodotti e sistemi operativi che System Center Configuration Manager non supporta più."
ms.custom: na
ms.date: 08/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d8c8b44c-1e8a-42b6-bab4-23c72a0a6169
caps.latest.revision: "15"
caps.handback.revision: "0"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: 95df27d4bf21a2cb1b6d613415a3eff4c3a73552
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/04/2017
---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Funzionalità rimosse e deprecate per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo argomento descrive le funzionalità, i prodotti e i sistemi operativi rimossi dal supporto per System Center Configuration Manager o che verranno rimossi in un aggiornamento futuro (deprecati). Lo scopo è quello di informare in maniera anticipata gli utenti sulle future modifiche che potrebbero influire sull'uso di Configuration Manager.  

Queste informazioni sono soggette a modifiche nelle versioni future e potrebbero non includere tutte le funzionalità, tutti i prodotti o i sistemi operativi deprecati.  

## <a name="how-to-use-this-information"></a>Come usare queste informazioni  
Quando una funzionalità o un sistema operativo vengono elencati per la prima volta come deprecati, viene pianificata la rimozione del supporto per l'uso con Configuration Manager in una versione futura di Configuration Manager. Queste informazioni vengono fornite per facilitare la pianificazione delle alternative all'uso di tale funzionalità o sistema operativo. Quando viene rilasciata la prima versione di Configuration Manager in cui è stato rimosso tale supporto, questo argomento viene aggiornato per indicare la versione specifica.  

Quando viene rimosso il supporto per una funzionalità o un sistema operativo, tale funzionalità o sistema operativo rimane supportato quando si usa una versione precedente di Configuration Manager, fino al termine del supporto di tale versione. Tuttavia, quando si usa una versione di Configuration Manager rilasciata dopo la data o la versione indicata, tale versione di Configuration Manager non offre il supporto.

Ad esempio, se il supporto di una funzionalità viene pianificato per la rimozione in concomitanza con il primo aggiornamento rilasciato dopo settembre 2016, il supporto per tale funzionalità non sarà più incluso nell'aggiornamento 1610, rilasciato a ottobre 2016.
-  La funzionalità non sarà più supportata con l'aggiornamento 1610.
-  Questo argomento verrebbe aggiornato per indicare la rimozione del supporto con la versione 1610.
Tuttavia, se si continua a usare una versione precedente che supporta la funzionalità, come la versione 1602 o 1606, è possibile continuare a usare tale funzionalità fino al termine del supporto della versione in uso.

Per altre informazioni, vedere:
 - Sito Web del [ciclo di vita del supporto Microsoft](https://support.microsoft.com/lifecycle).
 - [Supporto per le versioni Current Branch di Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).




## <a name="deprecated-operating-systems"></a>Sistemi operativi deprecati
### <a name="server-operating-systems"></a>Sistemi operativi del server  

|**Sistemi operativi**|**Primo avviso funzionalità deprecata**|**Supporto rimosso** |  
|-|-|-|  
|Windows Server 2008|10 luglio 2015|Versione 1511 </br></br>Il supporto come sistema del sito viene rimosso. Vedere nota 1.|  
|Windows Server 2008 R2|10 luglio 2015| Versione 1702 (vedere nota 2)|  

-   Nota 1: questo sistema operativo non è supportato per i server del sito o ruoli del sistema del sito fatta eccezione per il punto di distribuzione e il punto di distribuzione pull. È possibile continuare a usare questo sistema operativo come punto di distribuzione fino all'annuncio della deprecazione di questo supporto o alla scadenza del periodo di supporto "Extended" di questo sistema operativo. Per altre informazioni, vedere l'argomento relativo ai [problemi di installazione di System Center Configuration Manager CB in Windows Server 2008](https://support.microsoft.com/help/4015095).

-   Nota 2: a partire dalla versione 1702, questo sistema operativo non è supportato per i server del sito o per la maggior parte dei ruoli del sistema del sito, ma continua a essere supportato dalle versioni precedenti la 1702. Questo sistema operativo resta comunque supportato per il ruolo del sistema del sito del punto di distribuzione (compresi i punti di distribuzione pull, PXE e il multicast) fino all'annuncio della deprecazione del supporto o alla scadenza del periodo di supporto "Extended" del sistema operativo. A partire dalla versione 1602, è possibile aggiornare sul posto il sistema operativo di un server del sito da Windows Server 2008 R2 a Windows Server 2012 R2.  

     Per altre informazioni sull'aggiornamento sul posto del sistema operativo dei server di un sito, vedere la sezione [Aggiornamento sul posto del sistema operativo dei server del sito che eseguono Windows Server 2008 R2](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS) in [Novità di System Center Configuration Manager](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md).



### <a name="client-operating-systems"></a>Sistemi operativi dei client  

 Se non specificato diversamente, ogni sistema operativo supportato come client di Configuration Manager è supportato fino alla data di fine del supporto "Extended" del sistema operativo. Per informazioni dettagliate sulle date di fine del supporto "Extended", vedere il sito Web del [ciclo di vita del supporto Microsoft](https://support.microsoft.com/lifecycle). Se il supporto di Configuration Manager per un sistema operativo termina prima della data finale del supporto "Extended", in questa pagina vengono elencate una data di deprecazione e una data di rimozione del supporto per il sistema operativo specificato.  

|**Sistemi operativi**|**Primo avviso funzionalità deprecata**|**Supporto rimosso**|  
|-|-|-|  
|Windows XP|10 luglio 2015|Versione 1511|  
|Windows XP Embedded <br><br> Include tutti i [sistemi operativi Embedded basati su XP](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#windows-embedded-computers).|10 luglio 2015|Versione 1702|  
|Windows Server 2003|10 luglio 2015|Versione 1511|  
|Windows Server 2003 R2|10 luglio 2015|Versione 1511|  
|Windows Vista|10 luglio 2015|Versione 1511|  
|Mac OS X  10.6 - 10.8|10 luglio 2015|Versione 1511|  
|Windows Mobile 6.0 - 6.5|10 luglio 2015|Versione 1511|  
|Nokia Symbian Belle|10 luglio 2015|Versione 1511|  
|Windows CE 5.0 - 6.0|10 luglio 2015|Versione 1511|  


## <a name="deprecated-support-for-sql-server-versions-as-a-site-database"></a>Supporto deprecato per le versioni di SQL Server usate come database del sito  

|**Versioni di SQL Server**|**Primo avviso funzionalità deprecata**|**Supporto rimosso**|   
|-|-|-|  
|SQL Server 2008|10 luglio 2015|Versione 1511|  
|SQL Server 2008 R2|10 luglio 2015|Versione 1702|  

Se è necessario aggiornare la versione di SQL Server, è consigliabile eseguire i metodi seguenti, dal più semplice al più complesso.
1. [Aggiornare SQL Server sul posto](/sccm/core/servers/manage/upgrade-on-premises-infrastructure#a-namebkmksupconfigupgradedbsrva-upgrade-sql-server-on-the-site-database-server) (scelta consigliata).
2. Installare una nuova versione di SQL Server in un nuovo computer. Quindi [usare l'opzione di spostamento del database](/sccm/core/servers/manage/modify-your-infrastructure#a-namebkmkdbconfiga-modify-the-site-database-configuration) delle impostazioni di Configuration Manager in modo che il server del sito punti alla nuova versione di SQL Server.
3. Usare le funzionalità di [backup e ripristino](/sccm/protect/understand/backup-and-recovery).


## <a name="deprecated-features"></a>Funzionalità deprecate  

|**Funzionalità**|**Primo avviso funzionalità deprecata**|**Supporto rimosso**|  
|-|-|-|  
|Protezione accesso alla rete (NAP) inclusa in System Center 2012 Configuration Manager|10 luglio 2015|Versione 1511|  
|Gestione fuori banda in System Center 2012 Configuration Manager|16 ottobre 2015|Versione 1511|
|Sequenze attività: <br /> - OSDPreserveDriveLetter  <br /><br /> Durante la distribuzione del sistema operativo, per impostazione predefinita l'installazione di Windows ora stabilisce qual è la lettera di unità migliore da usare (in genere C:). Se si vuole specificare un'unità diversa da usare, è possibile modificare il percorso nella sequenza di passaggi dell'attività Applica sistema operativo. Passare all'impostazione **Selezionare il percorso in cui applicare questo sistema operativo**, selezionare **Lettera unità logica specifica** e scegliere l'unità che si vuole usare. |20 giugno 2016 |Versione 1606 |
|Sequenze attività: <br /> - Converti il disco selezionato in disco dinamico <br /> - Installa strumenti di distribuzione |18 novembre 2016|Il supporto di queste sequenze di attività termina con il primo aggiornamento rilasciato dopo il 01/06/2017.|
|Software Center ha un aspetto nuovo e moderno. Nei prossimi mesi la versione precedente di Software Center non sarà più disponibile.<br><br>È possibile configurare i client per l'uso del nuovo Software Center abilitando l'impostazione client **Agente computer** > **Usa il nuovo Software Center**.<br><br>Per altre informazioni su Software Center, vedere [Pianificare e configurare la gestione delle applicazioni in System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management).|13 dicembre 2016|Il supporto per la versione precedente di Software Center termina con il primo aggiornamento rilasciato dopo il 1° gennaio 2018.|
|A partire dalla nuova esperienza di Software Center nella versione 1511, le app che venivano visualizzate solo nel Catalogo applicazioni (app disponibili per gli utenti) vengono ora visualizzate in Software Center. </br></br>Con questa nuova importante funzionalità del Catalogo applicazioni ora inclusa in Software Center, l'esperienza del Catalogo applicazioni basata sul Web non sarà più disponibile nei prossimi mesi.|11 agosto 2017| Il supporto per l'esperienza utente del sito Web Catalogo applicazioni terminerà con il primo aggiornamento rilasciato dopo il 1° giugno 2018|
|Gestione dei dischi rigidi virtuali in Configuration Manager. </br></br>Ciò include la rimozione delle opzioni per creare un nuovo disco rigido virtuale o per gestire un disco rigido virtuale con una sequenza di attività e la rimozione del nodo Dischi rigidi virtuali dalla console di Configuration Manager. </br></br>Dopo la rimozione di questo supporto, i dischi rigidi virtuali esistenti non verranno eliminati, ma non saranno più accessibili dalla console di Configuration Manager.  |6 gennaio 2017 |Il supporto per dischi rigidi virtuali termina con il primo aggiornamento rilasciato dopo il 01/06/2017.|
|Strumento di valutazione dell'aggiornamento di System Center Configuration Manager. </br></br>Lo strumento di valutazione dell'aggiornamento dipende da System Center Configuration Manager e da Application Compatibility Toolkit (ACT) 6.x. La versione finale di ACT è stata fornita in Windows 10 v1511 ADK. Dal momento che non saranno pubblicati altri aggiornamenti di ACT, il supporto per lo strumento di valutazione dell'aggiornamento verrà sospeso. </br></br>Lo strumento di valutazione dell'aggiornamento verrà sostituito dalla funzionalità [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics). L'avviso relativo alla deprecazione è stato aggiunto alla [pagina di download per UAT](https://www.microsoft.com/download/details.aspx?id=37145) il 12 settembre 2016. | 12 settembre 2016  | 11 luglio 2017 |


<br></br>
Dettagli aggiuntivi sulle funzionalità rimosse con la versione 1511 di System Center Configuration Manager:

###  <a name="bkmk_amt"></a> Gestione fuori banda  
 Con Configuration Manager, il supporto nativo per computer basati su AMT dalla console di Configuration Manager è stato rimosso.  

-   I computer basati su AMT restano completamente gestiti quando si usa il [componente aggiuntivo Intel SCS per Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). Il componente aggiuntivo consente di accedere alle funzionalità più recenti per gestire AMT, rimuovendo le limitazioni introdotte fino al momento in cui Configuration Manager è stato in grado di integrare queste modifiche.  

-   La gestione fuori banda in System Center 2012 Configuration Manager non è interessata da questa modifica.  

###  <a name="bkmk_nap"></a> Protezione accesso alla rete  
 System Center Configuration Manager ha rimosso il supporto per la protezione accesso alla rete. Questa funzionalità è stata deprecata in Windows Server 2012 R2 ed è stata rimossa da Windows 10.  

 Per alternative a Protezione accesso alla rete, vedere la sezione *Funzionalità deprecata* di [Panoramica dei criteri di rete e dei servizi di accesso](https://technet.microsoft.com/library/hh831683.aspx).

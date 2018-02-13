---
title: "Funzionalità deprecate per Configuration Manager"
titleSuffix: Configuration Manager
description: "Informazioni sulle funzionalità che System Center Configuration Manager non supporta più."
ms.custom: na
ms.date: 01/25/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
caps.latest.revision: 
caps.handback.revision: 
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: d49e0f839106af652f7b49227b6c4f8c957347d9
ms.sourcegitcommit: b13da5ad8ffd58e3b89fa6d7170e1dec3ff130a4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2018
---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Funzionalità rimosse e deprecate per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo descrive le funzionalità rimosse dal supporto per System Center Configuration Manager o che verranno rimosse in un aggiornamento futuro (deprecate). Lo scopo è quello di informare in maniera anticipata gli utenti sulle future modifiche che potrebbero influire sull'uso di Configuration Manager.  

Queste informazioni sono soggette a modifiche nelle versioni future e potrebbero non includere tutte le funzionalità deprecate di Configuration Manager.

## <a name="deprecated-features"></a>Funzionalità deprecate  

|**Funzionalità**|**Primo avviso funzionalità deprecata**|**Supporto rimosso**|  
|-|-|-|  
|A partire dalla nuova esperienza di Software Center nella versione 1511, le app che venivano visualizzate solo nel Catalogo applicazioni (app disponibili per gli utenti) vengono ora visualizzate in Software Center. </br></br>Con questa nuova importante funzionalità del Catalogo applicazioni ora inclusa in Software Center, l'esperienza del Catalogo applicazioni basata sul Web non sarà più disponibile nei prossimi mesi.|11 agosto 2017| Il supporto per l'esperienza utente del sito Web Catalogo applicazioni terminerà con il primo aggiornamento rilasciato dopo il 1° giugno 2018|
|Software Center ha un aspetto nuovo e moderno. Nei prossimi mesi la versione precedente di Software Center non sarà più disponibile.<br><br>È possibile configurare i client per l'uso del nuovo Software Center abilitando l'impostazione client **Agente computer** > **Usa il nuovo Software Center**.<br><br>Per altre informazioni su Software Center, vedere [Pianificare e configurare la gestione delle applicazioni in System Center Configuration Manager](https://docs.microsoft.com/sccm/apps/plan-design/plan-for-and-configure-application-management).|13 dicembre 2016|Il supporto per la versione precedente di Software Center termina con il primo aggiornamento rilasciato dopo il 1° gennaio 2018.|
|Gestione dei dischi rigidi virtuali in Configuration Manager. </br></br>Ciò include la rimozione delle opzioni per creare un nuovo disco rigido virtuale o per gestire un disco rigido virtuale con una sequenza di attività e la rimozione del nodo Dischi rigidi virtuali dalla console di Configuration Manager. </br></br>Dopo la rimozione di questo supporto, i dischi rigidi virtuali esistenti non verranno eliminati, ma non saranno più accessibili dalla console di Configuration Manager.  |6 gennaio 2017 |Versione 1710|
|Sequenze attività: <br /> - Converti il disco selezionato in disco dinamico <br /> - Installa strumenti di distribuzione |18 novembre 2016|Versione 1710|
|Strumento di valutazione dell'aggiornamento di System Center Configuration Manager. </br></br>Lo strumento di valutazione dell'aggiornamento dipende da System Center Configuration Manager e da Application Compatibility Toolkit (ACT) 6.x. La versione finale di ACT è stata fornita in Windows 10 v1511 ADK. Dal momento che non saranno pubblicati altri aggiornamenti di ACT, il supporto per lo strumento di valutazione dell'aggiornamento verrà sospeso. </br></br>Lo strumento di valutazione dell'aggiornamento verrà sostituito dalla funzionalità [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics). L'avviso relativo alla deprecazione è stato aggiunto alla [pagina di download per UAT](https://www.microsoft.com/download/details.aspx?id=37145) il 12 settembre 2016. | 12 settembre 2016  | 11 luglio 2017 |
|Sequenze attività: <br /> - OSDPreserveDriveLetter  <br /><br /> Durante la distribuzione del sistema operativo, per impostazione predefinita l'installazione di Windows ora stabilisce qual è la lettera di unità migliore da usare (in genere C:). Se si vuole specificare un'unità diversa da usare, è possibile modificare il percorso nella sequenza di passaggi dell'attività Applica sistema operativo. Passare all'impostazione **Selezionare il percorso in cui applicare questo sistema operativo**. Selezionare **Lettera unità logica specifica** e scegliere l'unità che si vuole usare. |20 giugno 2016 |Versione 1606 |
|Protezione accesso alla rete (NAP) inclusa in System Center 2012 Configuration Manager|10 luglio 2015|Versione 1511|  
|Gestione fuori banda in System Center 2012 Configuration Manager|16 ottobre 2015|Versione 1511|



<br></br>
Dettagli aggiuntivi sulle funzionalità rimosse con la versione 1511 di System Center Configuration Manager:

###  <a name="bkmk_amt"></a> Gestione fuori banda  
 Con Configuration Manager, il supporto nativo per computer basati su AMT dalla console di Configuration Manager è stato rimosso.  

-   I computer basati su AMT restano completamente gestiti quando si usa il [componente aggiuntivo Intel SCS per Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). Il componente aggiuntivo consente di accedere alle funzionalità più recenti per gestire AMT, rimuovendo le limitazioni introdotte fino al momento in cui Configuration Manager è stato in grado di integrare queste modifiche.  

-   La gestione fuori banda in System Center 2012 Configuration Manager non è interessata da questa modifica.  

###  <a name="bkmk_nap"></a> Protezione accesso alla rete  
 System Center Configuration Manager ha rimosso il supporto per la protezione accesso alla rete. Questa funzionalità è stata deprecata in Windows Server 2012 R2 ed è stata rimossa da Windows 10.  

 Per alternative a Protezione accesso alla rete, vedere la sezione *Funzionalità deprecata* di [Panoramica dei criteri di rete e dei servizi di accesso](https://technet.microsoft.com/library/hh831683.aspx).

## <a name="more-information"></a>Altre informazioni
Per altre informazioni, vedere:
 - [Elementi rimossi e deprecati](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)
 - Sito Web del [ciclo di vita del supporto Microsoft](https://support.microsoft.com/lifecycle).
 - [Supporto per le versioni Current Branch di Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).

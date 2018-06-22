---
title: Funzionalità deprecate
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità che System Center Configuration Manager non supporta più.
ms.date: 05/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 967c0ff71af5b3586568bf3f5d2fee7ed5b8bb06
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32337735"
---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Funzionalità rimosse e deprecate per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In questo articolo sono elencate le funzionalità deprecate o rimosse dal supporto per Configuration Manager. Le funzionalità deprecate verranno rimosse in un aggiornamento futuro. Queste future modifiche potrebbero influire sull'uso di Configuration Manager.  

Queste informazioni sono soggette a modifica nelle versioni future. È possibile che non tutte le funzionalità di Configuration Manager deprecate siano incluse.



## <a name="deprecated-features"></a>Funzionalità deprecate  

|Funzionalità|Primo annuncio riguardo agli elementi deprecati|Supporto&nbsp;rimosso|  
|-----------|---|--------------|  
|Le app disponibili per gli utenti che in precedenza venivano visualizzate solo nel Catalogo applicazioni ora sono visualizzate nella nuova versione di Software Center. </br></br>L'esperienza del Catalogo applicazioni basata sul Web non sarà pertanto disponibile nei prossimi mesi.|11 agosto 2017| Il supporto per l'esperienza utente del sito Web Catalogo applicazioni terminerà con il primo aggiornamento rilasciato dopo il 1° giugno 2018|
|Versione precedente di Software Center.<br><br>Per altre informazioni sulla nuova versione di Software Center, vedere [Pianificare e configurare la gestione delle applicazioni](/sccm/apps/plan-design/plan-for-and-configure-application-management#configure-software-center-and-the-application-catalog-windows-pcs-only).|13 dicembre 2016|Versione 1802|
|Gestione dei dischi rigidi virtuali in Configuration Manager. </br></br>Questa funzionalità deprecata include la rimozione delle opzioni per creare un nuovo disco rigido virtuale o per gestire un disco rigido virtuale con una sequenza di attività e la rimozione del nodo Dischi rigidi virtuali dalla console di Configuration Manager. </br></br>I dischi rigidi virtuali esistenti non vengono eliminati, ma non saranno più accessibili dalla console di Configuration Manager.  |6 gennaio 2017 |Versione 1710|
|Sequenze attività: <br /> - Converti il disco selezionato in disco dinamico <br /> - Installa strumenti di distribuzione |18 novembre 2016|Versione 1710|
|Strumento di valutazione dell'aggiornamento di System Center Configuration Manager. </br></br>Lo strumento di valutazione dell'aggiornamento dipende da System Center Configuration Manager e da Application Compatibility Toolkit (ACT) 6.x. La versione finale di ACT è stata fornita in Windows 10 v1511 ADK. Dal momento che non sono disponibili altri aggiornamenti di ACT, il supporto per lo strumento di valutazione dell'aggiornamento viene sospeso. </br></br>Lo strumento di valutazione dell'aggiornamento verrà sostituito dalla funzionalità [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics). L'avviso relativo alla deprecazione è stato aggiunto alla [pagina di download per UAT](https://www.microsoft.com/download/details.aspx?id=37145) il 12 settembre 2016. | 12 settembre 2016  | 11 luglio 2017 |
|Sequenze attività: <br /> - OSDPreserveDriveLetter  <br /><br /> Durante la distribuzione del sistema operativo, per impostazione predefinita l'installazione di Windows ora stabilisce qual è la lettera di unità migliore da usare (in genere C:). Se si vuole specificare un'unità diversa da usare, è possibile modificare il percorso nella sequenza di passaggi dell'attività Applica sistema operativo. Passare all'impostazione **Selezionare il percorso in cui applicare questo sistema operativo**. Selezionare **Lettera unità logica specifica** e scegliere l'unità che si vuole usare. |20 giugno 2016 |Versione 1606 |
|Protezione accesso alla rete (NAP) inclusa in System Center 2012 Configuration Manager|10 luglio 2015|Versione 1511|  
|Gestione fuori banda in System Center 2012 Configuration Manager|16 ottobre 2015|Versione 1511|



## <a name="features-removed-in-version-1511"></a>Funzionalità rimosse nella versione 1511
Le sezioni seguenti includono altri dettagli relativi alle funzionalità rimosse con la versione 1511:

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
 - [Ciclo di vita del supporto Microsoft](https://support.microsoft.com/lifecycle)
 - [Supporto per le versioni Current Branch di Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).

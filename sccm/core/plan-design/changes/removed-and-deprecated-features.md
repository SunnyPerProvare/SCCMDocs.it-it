---
title: "Funzionalità deprecate | System Center Configuration Manager"
description: "Informazioni su funzionalità, prodotti e sistemi operativi che System Center Configuration Manager non supporta più."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d8c8b44c-1e8a-42b6-bab4-23c72a0a6169
caps.latest.revision: 15
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 0f1e1070fd5b56b1abf22159e9f95b3b4bd8a8c6


---
# <a name="removed-and-deprecated-features-for-system-center-configuration-manager"></a>Funzionalità rimosse e deprecate per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo argomento illustra le funzionalità, i prodotti e i sistemi operativi rimossi dal supporto di System Center Configuration Manager o che verranno rimossi in un aggiornamento futuro (deprecati). Con questo documento si vuole informare in maniera anticipata gli utenti sulle future modifiche che potrebbero influire sull'uso di Configuration Manager.  

 Queste informazioni sono soggette a modifiche nelle versioni future e potrebbero non includere tutte le funzionalità, tutti i prodotti o i sistemi operativi deprecati.  

## <a name="deprecated-features-products-and-operating-systems"></a>Funzionalità, prodotti e sistemi operativi deprecati  
 I prodotti e i sistemi operativi Microsoft elencati come deprecati sono in modalità di supporto esteso o hanno raggiunto il termine del rispettivo ciclo di vita. I prodotti e i sistemi operativi Microsoft elencati come deprecati vengono comunque testati con le versioni correnti di Configuration Manager, fino al termine del ciclo di vita del rispettivo supporto tecnico Microsoft.  Per altre informazioni, vedere il sito Web [Ciclo di vita del supporto tecnico Microsoft](https://support.microsoft.com/lifecycle) .  

 **Funzionalità deprecate:**  


|**Funzionalità**|**Primo avviso funzionalità deprecata**|**Supporto rimosso**|  
|-|-|-|  
|Protezione accesso alla rete (NAP) inclusa in System Center 2012 Configuration Manager|10/07/2015|√|  
|Gestione fuori banda in System Center 2012 Configuration Manager|16/10/2015|√|  

 **Sistemi operativi del server deprecati:**  

 |**Sistemi operativi**|**Primo avviso funzionalità deprecata**|**Supporto rimosso**|  
|-|-|-|  
|Windows Server 2008|10/07/2015|Il supporto termina con il primo aggiornamento rilasciato dopo il 31/12/2016 (vedere la nota 1)|  
|Windows Server 2008 R2|10/07/2015|Il supporto termina con il primo aggiornamento rilasciato dopo il 31/12/2016 (vedere la nota 2)|  

-   Nota 1: al termine del supporto, questo sistema operativo non sarà più supportato per i server del sito o per la maggior parte dei ruoli del sistema del sito. Questo sistema operativo sarà comunque supportato per il ruolo del sistema del sito del punto di distribuzione, compreso il punto di distribuzione pull, fino all'annuncio della deprecazione del supporto o alla scadenza del periodo di supporto "Extended" del sistema operativo.  

-   Nota 2: al termine del supporto, questo sistema operativo non sarà più supportato per i server del sito o per la maggior parte dei ruoli del sistema del sito. Questo sistema operativo sarà comunque supportato per il punto migrazione stato e per il ruolo del sistema del sito del punto di distribuzione, compresi il punto di distribuzione pull, PXE e il multicast, fino all'annuncio della deprecazione del supporto o alla scadenza del periodo di supporto "Extended" del sistema operativo.  A partire dalla versione 1602, è possibile aggiornare sul posto il sistema operativo di un server del sito da Windows Server 2008 R2 a Windows Server 2012 R2.  

     Per altre informazioni sull'aggiornamento sul posto del sistema operativo dei server di un sito, vedere la sezione [In-place upgrade the operating system of site servers that run Windows Server 2008 R2](../../../core/plan-design/changes/whats-new-in-version-1602.md#bkmk_UpgradeOS) (Aggiornamento sul posto del sistema operativo dei server del sito che eseguono Windows Server 2008 R2) in [What's changed in System Center Configuration Manager](../../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md) (Novità in System Center Configuration Manager).



 **Sistemi operativi client deprecati:**  

 Se non specificato diversamente, ogni sistema operativo supportato come client di Configuration Manager è supportato fino alla data finale del supporto "Extended" del sistema operativo, come descritto in [Ciclo di vita del supporto Microsoft](https://support.microsoft.com/lifecycle).  Se il supporto di Configuration Manager per un sistema operativo termina prima della data finale del supporto "Extended", in questa pagina vengono elencate una data di deprecazione e una data di rimozione del supporto per il sistema operativo specificato.  

|**Sistemi operativi**|**Primo avviso funzionalità deprecata**|**Supporto rimosso**|  
|-|-|-|  
|Windows XP|10/07/2015|√|  
|Windows XP Embedded|10/07/2015|Il supporto termina con il primo aggiornamento rilasciato dopo il 31/12/2016|  
|Windows Server 2003|10/07/2015|√|  
|Windows Server 2003 R2|10/07/2015|√|  
|Windows Vista|10/07/2015|√|  
|Mac OS X  10.6 - 10.8|10/07/2015|√|  
|Windows Mobile 6.0 - 6.5|10/07/2015|√|  
|Nokia Symbian Belle|10/07/2015|√|  
|Windows CE 5.0 - 6.0|10/07/2015|√|  


 **Supporto deprecato per le versioni di SQL Server usate come database del sito:**  

|**Versioni di SQL Server**|**Primo avviso funzionalità deprecata**|**Supporto rimosso**|   
|-|-|-|  
|SQL Server 2008|10/07/2015|√|  
|SQL Server 2008 R2|10/07/2015|Il supporto termina con il primo aggiornamento rilasciato dopo il 31/12/2016|  

## <a name="features-removed-in-system-center-configuration-manager"></a>Funzionalità rimosse in System Center Configuration Manager  
 A partire dalla versione iniziale di System Center Configuration Manager le funzionalità seguenti sono rimosse:

###  <a name="a-namebkmkamta-out-of-band-management"></a><a name="bkmk_amt"></a> Gestione fuori banda  
 Con Configuration Manager, il supporto nativo per computer basati su AMT dalla console di Configuration Manager è stato rimosso.  

-   I computer basati su AMT restano completamente gestiti quando si usa il [componente aggiuntivo Intel SCS per Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html)  

-   L'uso del componente aggiuntivo permette di accedere alle funzionalità più recenti per gestire AMT, rimuovendo le limitazioni introdotte fino al momento in cui Configuration Manager è stato in grado di integrare queste modifiche  

-   La gestione fuori banda in System Center 2012 Configuration Manager non è interessata da questa modifica.  

###  <a name="a-namebkmknapa-network-access-protection"></a><a name="bkmk_nap"></a> Protezione accesso alla rete  
 System Center Configuration Manager ha rimosso il supporto per la protezione accesso alla rete. Questa funzionalità è stata deprecata in Windows Server 2012 R2 ed è stata rimossa da Windows 10.  

 Per alternative a Protezione accesso alla rete, vedere la sezione **Funzionalità deprecata** di [Panoramica dei criteri di rete e dei servizi di accesso](https://technet.microsoft.com/library/hh831683.aspx).  



<!--HONumber=Nov16_HO1-->



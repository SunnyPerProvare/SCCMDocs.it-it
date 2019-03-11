---
title: Funzionalità deprecate
titleSuffix: Configuration Manager
description: Informazioni sulle funzionalità che Configuration Manager non supporta più.
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 40469e8173303eb7ad46ef8e716529c37ec6e76d
ms.sourcegitcommit: ef2960bd91655c741450774e512dd0a9be610625
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/26/2019
ms.locfileid: "56838787"
---
# <a name="removed-and-deprecated-features-for-configuration-manager"></a>Funzionalità rimosse e deprecate per Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In questo articolo sono elencate le funzionalità deprecate o rimosse dal supporto per Configuration Manager. Le funzionalità deprecate verranno rimosse in un aggiornamento futuro. Queste future modifiche potrebbero influire sull'uso di Configuration Manager.  

Queste informazioni sono soggette a modifica nelle versioni future. È possibile che non tutte le funzionalità di Configuration Manager deprecate siano incluse.



## <a name="deprecated-features"></a>Funzionalità deprecate  

|Funzionalità|Primo annuncio riguardo agli elementi deprecati|Supporto&nbsp;rimosso|  
|-----------|---|--------------|  
|È stata modificata l'implementazione per la condivisione del contenuto da Azure. Usare un gateway di gestione cloud abilitato per il contenuto. Non sarà possibile creare un punto di distribuzione cloud tradizionale in futuro.|Febbraio 2019|Prima versione rilasciata dopo il 1° novembre 2019|
|Distribuzione classica del servizio in Azure per il gateway di gestione cloud e il punto di distribuzione cloud. Per altre informazioni, vedere [Pianificare il gateway di gestione cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).|Novembre 2018|Prima versione rilasciata dopo il 1° luglio 2019| 
|System Center Endpoint Protection per Mac e Linux<br>Per altre informazioni, vedere il [post del blog sulla fine del supporto](https://go.microsoft.com/fwlink/?linkid=870182).|Ottobre 2018|31 dicembre 2018|
|Accesso condizionale in locale<br>Per altre informazioni, vedere [Informazioni sulla gestione di dispositivi mobili ibrida](/sccm/mdm/understand/hybrid-mobile-device-management).|30 gennaio 2019|1 settembre 2019|
|Gestione di dispositivi mobili (MDM) ibrida<br>Per altre informazioni, vedere [Informazioni sulla gestione di dispositivi mobili ibrida](/sccm/mdm/understand/hybrid-mobile-device-management).<br><br>A partire dalla versione 1902 del servizio Intune, prevista per la fine di febbraio 2019, i nuovi clienti non possono creare una nuova connessione ibrida.<!--Intune feature 2683117-->|14 agosto 2018|1 settembre 2019|
|Impostazioni di Windows Hello for Business in Configuration Manager<br>Per altre informazioni, vedere [Impostazioni di Windows Hello for Business](/sccm/protect/deploy-use/windows-hello-for-business-settings).|Dicembre 2017|Prima versione rilasciata dopo il 1° novembre 2019|
|L'**esperienza utente di Silverlight** per il ruolo Punto per siti Web del Catalogo applicazioni non è più supportato. Gli utenti devono usare il nuovo Software Center. NOTA: il ruolo Punto per siti Web del Catalogo applicazioni e il ruolo Punto per servizi Web sono ancora supportati. In alcuni scenari, il nuovo Software Center comunica con il punto per siti Web del Catalogo applicazioni. Per altre informazioni, vedere [Configurare Software Center](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex).<!--1358309-->|11 agosto 2017| Versione 1806|
|Versione precedente di Software Center.<br><br>Per altre informazioni sulla nuova versione di Software Center, vedere [Pianificare e configurare la gestione delle applicazioni](/sccm/apps/plan-design/plan-for-and-configure-application-management##bkmk_userex).|13 dicembre 2016|Versione 1802|
|Gestione dei dischi rigidi virtuali in Configuration Manager. <br><br>Questa funzionalità deprecata include la rimozione delle opzioni per creare un nuovo disco rigido virtuale o per gestire un disco rigido virtuale con una sequenza di attività e la rimozione del nodo Dischi rigidi virtuali dalla console di Configuration Manager. <br><br>I dischi rigidi virtuali esistenti non vengono eliminati, ma non saranno più accessibili dalla console di Configuration Manager.  |6 gennaio 2017 |Versione 1710|
|Sequenze attività: <br /> - Converti il disco selezionato in disco dinamico <br /> - Installa strumenti di distribuzione |18 novembre 2016|Versione 1710|
|Strumento di valutazione dell'aggiornamento di System Center Configuration Manager. <br><br>Lo strumento di valutazione dell'aggiornamento dipende da System Center Configuration Manager e da Application Compatibility Toolkit (ACT) 6.x. La versione finale di ACT è stata fornita in Windows 10 v1511 ADK. Dal momento che non sono disponibili altri aggiornamenti di ACT, il supporto per lo strumento di valutazione dell'aggiornamento viene sospeso. <br><br>Lo strumento di valutazione dell'aggiornamento verrà sostituito dalla funzionalità [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics). L'avviso relativo alla deprecazione è stato aggiunto alla [pagina di download per UAT](https://www.microsoft.com/download/details.aspx?id=37145) il 12 settembre 2016. | 12 settembre 2016  | 11 luglio 2017 |
|Punti di aggiornamento software con un cluster Bilanciamento carico di rete (NLB) | 27 febbraio 2016 | Versione 1702 | 
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

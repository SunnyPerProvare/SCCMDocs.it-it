---
title: Configurazioni supportate | System Center Configuration Manager
description: Identificare le configurazioni e i requisiti principali in modo da pianificare, distribuire e manutenere una distribuzione di System Center Configuration Manager funzionale.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45a10878-ff48-4318-9c6d-c014b38a4039
caps.latest.revision: 9
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 170bd941bd123b998dd5d6235359aee97adc06bd


---
# <a name="supported-configurations-for-system-center-configuration-manager"></a>Configurazioni supportate per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager usa server, client, configurazioni di rete e altri prodotti quali Microsoft Intune, SQL Server e Azure, come una soluzione locale.

Le informazioni in questo e negli argomenti seguenti sono fondamentali per identificare le configurazioni e i requisiti, o le limitazioni, principali per poter pianificare, distribuire e manutenere una distribuzione di Configuration Manager funzionale.  Queste informazioni sono specifiche per l'infrastruttura per i siti, le gerarchie e i dispositivi gestiti di Configuration Manager. Quando una funzionalità di Configuration Manager richiede più configurazioni specifiche, tali informazioni saranno incluse nella documentazione specifica della funzionalità e andranno ad aggiungersi alle informazioni più generali sulle configurazioni supportate.  

 I prodotti e le tecnologie descritti negli argomenti seguenti sono supportati con Configuration Manager. Tuttavia, la loro inclusione in questo contenuto non è da considerarsi un'estensione del normale ciclo di vita del supporto per il singolo prodotto. I prodotti che non rientrano nel ciclo di vita del supporto non sono supportati per l'uso con Configuration Manager. Per altre informazioni sui cicli di vita del supporto Microsoft, visitare il sito Web [Ciclo di vita del supporto Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270) .  

> [!NOTE]  
>  Per informazioni sui criteri del ciclo di vita del supporto Microsoft, vedere le domande frequenti nel sito [Criteri relativi al ciclo di vita Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=31976).  

 I prodotti e le versioni di prodotto non elencati negli argomenti seguenti non sono supportati con System Center Configuration Manager a meno che non siano annunciati nel blog [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/).  In alcuni casi è possibile che i contenuti del blog anticipino un aggiornamento rispetto alla documentazione relativa.


-  [Numeri di ridimensionamento e scalabilità](../../../core/plan-design/configs/size-and-scale-numbers.md)  
Dettagli relativi a quanti siti, quanti ruoli del sistema del sito per sito e quanti client o dispositivi sono supportati in diverse progettazioni di gerarchie di Configuration Manager.

-  [Prerequisiti del sito e del sistema del sito](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
Configurazioni necessarie per supportare tipi di siti e di ruoli del sistema del sito diversi in un server Windows.

-  [Sistemi operativi supportati per i server del sistema del sito](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
Informazioni su quali sistemi operativi è possibile usare come server del sito o server del sistema del sito.

-  [Sistemi operativi supportati per client e dispositivi](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)  
Informazioni su quali sistemi operativi è possibile gestire con Configuration Manager, compresi Windows, Linux e UNIX, Mac, sistemi operativi integrati e dispositivi mobili.

-  [Sistemi operativi supportati per le console](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
Informazioni su quali sistemi operativi possono ospitare la console di Configuration Manager per offrire un punto di accesso per la gestione della distribuzione.  

-  [Supporto per le versioni di SQL Server](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
Elenco delle versioni di SQL Server che possono ospitare il database del sito e il database per la creazione di report, e configurazioni obbligatorie e facoltative che è possibile usare.

-  [High availability options](../../../protect/understand/high-availability-options.md) (Opzioni di disponibilità elevata)  
Informazioni sulle opzioni che è possibile implementare quando si progetta l'ambiente per mantenere un livello di disponibilità del servizio elevato per la distribuzione di Configuration Manager.

-  [Recommended hardware](../../../core/plan-design/configs/recommended-hardware.md) (Hardware consigliato)  
Linee guida per identificare l'hardware e le configurazioni appropriati per l'hosting dei siti e dei servizi principali di Configuration Manager.

-  [Supporto per i domini di Active Directory](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
Informazioni sulle configurazioni di dominio di Active Directory supportate, richieste e supportate da Configuration Manager.

-  [Supporto per le funzionalità e le reti Windows](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
Configuration Manager supporta diverse tecnologie Windows come ad esempio BranchCache e la deduplicazione dei dati. Informazioni sulle tecnologie supportate e le limitazioni relative per l'uso con Configuration Manager.

-  [Supporto per gli ambienti di virtualizzazione](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
Informazioni che consentono di usare le tecnologie per le macchine virtuali supportate.



<!--HONumber=Nov16_HO1-->



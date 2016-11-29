---
title: Valutare System Center Configuration Manager creando un proprio ambiente lab
description: Creare un ambiente lab per valutare l'uso di System Center Configuration Manager nell'organizzazione.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 01b30260-f03a-4851-a549-d1b76e8cfc69
caps.latest.revision: 25
caps.handback.revision: 0
author: brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 363e6a929b72e027d5fff7584905fb552dc695b0


---
# <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>Valutare System Center Configuration Manager creando un proprio ambiente lab

*Si applica a: System Center Configuration Manager (Current Branch)*

Informazioni su come creare un ambiente lab per valutare l'uso di System Center Configuration Manager nell'organizzazione.  

## <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>Valutare System Center Configuration Manager creando un proprio ambiente di lab  
 System Center Configuration Manager è uno strumento potente e complesso per gestire utenti, dispositivi e software. È consigliabile eseguire una valutazione esaustiva di System Center Configuration Manager prima della distribuzione completa, in modo da poter combinare i concetti con le esercitazioni pratiche.  

 Questa guida è destinata principalmente agli amministratori che valutano l'uso di Configuration Manager in ambienti aziendali.  

-   Amministratori che cercano una soluzione per la gestione completa di PC, server e dispositivi mobili  

-   Amministratori che operano in settori ad alta protezione e che richiedono la sicurezza della gestione locale dei dispositivi insieme alla flessibilità di gestione dei dispositivi basati su cloud  

-   Amministratori che vogliono gestire la scalabilità verticale della propria architettura del server locale  

### <a name="what-this-lab-does"></a>Aspetti inclusi nell'ambito di competenza dell'esercitazione  
 La creazione di questo ambiente ha come obiettivo principale quello di offrire informazioni generali per iniziare a usare Configuration Manager e di migliorare la conoscenza di Configuration Manager attraverso la pratica. Viene pertanto impiegato un assembly accelerato della versione corrente di Configuration Manager, usando due server:  

-   Un server Active Directory di hosting, che svolge funzioni di controller di dominio, e il server DNS  

-   Un secondo server che ospita Configuration Manager e tutti i componenti di SQL Server associati.  

-   I computer client vengono installati all'interno di Hyper-V. È anche possibile eseguire il lab stesso come un sistema completamente virtualizzato in un singolo server.  

### <a name="what-this-lab-does-not-do"></a>Aspetti esclusi dall'ambito di competenza dell'esercitazione  
 Questo lab non prende in esame tutti gli scenari di Configuration Manager e non è progettato per eseguire la migrazione immediata in un ambiente attivo.  

 Quando si crea questo lab è necessario avere un ambiente di lavoro funzionale. Tuttavia, l'ambiente non deve essere ottimizzato per le prestazioni del sistema, la gestione dello spazio su disco rigido, l'archiviazione SQL Server e così via.  

###  <a name="a-namebkmkevalreca-recommended-reading-prior-to-beginning-the-lab"></a><a name="BKMK_EvalRec"></a> Letture consigliate prima di iniziare il lab  
 Molti contenuti sono disponibili nella [documentazione per System Center Configuration Manager](http://docs.microsoft.com/sccm/). Di seguito è riportata una selezione di argomenti di questa libreria la cui lettura preliminare agli esercizi è consigliata a tutti gli amministratori che usano i lab.  

-   Informazioni sui concetti di base che riguardano la console di Configuration Manager e i portali degli utenti finali nonché scenari di esempio sono disponibili in [Introduction to System Center Configuration Manager](../../core/understand/introduction.md) (Introduzione a System Center Configuration Manager)  

-   Informazioni sulle principali funzionalità di gestione di Configuration Manager sono disponibili in [Features and capabilities of System Center Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md) (Caratteristiche e funzionalità di System Center Configuration Manager)  

-   Approfondimenti dei contenuti sono disponibili in [Fundamentals of System Center Configuration Manager](../../core/understand/fundamentals.md) (Nozioni fondamentali su System Center Configuration Manager)  

-   Informazioni sull'importanza dei ruoli di sicurezza sono disponibili in [Fundamentals of role-based administration for System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md) (Nozioni fondamentali di amministrazione basata su ruoli per System Center Configuration Manager)  

-   Conoscenza dei [concetti relativi alla gestione dei contenuti](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_Concepts) per affrontare concetti specifici sulla gestione dei contenuti  

-   [Informazioni su come i client trovano i servizi e le risorse del sito per System Center Configuration Manager](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) per supportare correttamente le operazioni quotidiane del processo di distribuzione  



<!--HONumber=Nov16_HO1-->



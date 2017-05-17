---
title: Valutare Configuration Manager | Microsoft Docs
description: Creare un ambiente lab per valutare l&quot;uso di System Center Configuration Manager nell&quot;organizzazione.
ms.custom: na
ms.date: 2/28/2017
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
ms.translationtype: Human Translation
ms.sourcegitcommit: 0ea90d3f3bef80b8acf9018a1338ae05fc948af4
ms.openlocfilehash: d7ea785ab1beee09b9adda735a87f89bc9481620
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017


---
# <a name="evaluate-system-center-configuration-manager-by-building-your-own-lab-environment"></a>Valutare System Center Configuration Manager creando un proprio ambiente lab

*Si applica a: System Center Configuration Manager (Current Branch)*

 Informazioni su come creare un ambiente lab per valutare l'uso di System Center Configuration Manager nell'organizzazione.  

 System Center Configuration Manager è uno strumento potente e complesso per gestire utenti, dispositivi e software. È consigliabile valutare System Center Configuration Manager in modo esaustivo prima della distribuzione completa, in modo da poter combinare i concetti con le esercitazioni pratiche.  

 Questa guida è destinata principalmente agli amministratori che valutano l'uso di Configuration Manager in ambienti aziendali:  

-   Amministratori che cercano una soluzione per la gestione completa di PC, server e dispositivi mobili  

-   Amministratori che operano in settori con protezione avanzata e che richiedono la sicurezza della gestione dei dispositivi locale insieme alla flessibilità della gestione dei dispositivi basata su cloud  

-   Amministratori che vogliono gestire la scalabilità della propria architettura server locale  

## <a name="what-this-lab-does"></a>Aspetti inclusi nell'ambito di competenza dell'esercitazione  
 La creazione di questo ambiente lab ha come obiettivo principale quello di offrire informazioni generali per iniziare a usare Configuration Manager e di migliorare la conoscenza di Configuration Manager. A tal proposito viene impiegato un assembly accelerato della versione corrente di Configuration Manager, usando due server:  

-   Un server ospita Active Directory, che svolge funzioni di controller di dominio, e il server DNS  

-   Un secondo server ospita Configuration Manager e tutti i componenti di SQL Server associati  

I computer client vengono installati all'interno di Hyper-V. È anche possibile eseguire il lab stesso come un sistema completamente virtualizzato in un singolo server.  

## <a name="what-this-lab-does-not-do"></a>Aspetti esclusi dall'ambito di competenza dell'esercitazione  
 Questo lab non prende in esame tutti gli scenari di Configuration Manager e non è progettato per eseguire la migrazione immediata in un ambiente attivo.  

 Quando si crea questo lab è necessario avere un ambiente di lavoro funzionale. L'ambiente non deve essere tuttavia ottimizzato per fattori come prestazioni del sistema, gestione dello spazio su disco rigido e archiviazione SQL Server.  

##  <a name="BKMK_EvalRec"></a> Letture consigliate prima di iniziare il lab  
 Molti contenuti sono disponibili in [Documentazione per System Center Configuration Manager](http://docs.microsoft.com/sccm/). Prima di iniziare il lab, è consigliata la lettura degli argomenti di questa libreria elencati di seguito:  

-   Informazioni sui concetti di base che riguardano la console di Configuration Manager e i portali degli utenti finali nonché scenari di esempio sono disponibili in [Introduzione a System Center Configuration Manager](../../core/understand/introduction.md).  

-   Informazioni sulle principali funzionalità di gestione di Configuration Manager sono disponibili in [Caratteristiche e funzionalità di System Center Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md).  

-   Approfondimenti dei contenuti sono disponibili in [Nozioni fondamentali su System Center Configuration Manager](../../core/understand/fundamentals.md).  

-   Informazioni sull'importanza dei ruoli di sicurezza sono disponibili in [Nozioni fondamentali di amministrazione basata su ruoli per System Center Configuration Manager](../../core/understand/fundamentals-of-role-based-administration.md).  

-   Informazioni sulla gestione dei contenuti sono disponibili in [Concetti di base per la gestione dei contenuti in System Center Configuration Manager](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   Informazioni su come supportare correttamente le operazioni quotidiane del processo di distribuzione sono disponibili in [Informazioni su come i client trovano i servizi e le risorse del sito per System Center Configuration Manager](../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  


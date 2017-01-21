---
title: Pianificare la migrazione | Microsoft Docs
description: Leggere le informazioni su siti e gerarchie prima di eseguire la migrazione di dati nella gerarchia di destinazione di System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b2bf493e-1e10-496f-a139-2646522703ed
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5e3d3f4194b06442e34c10988a20fe9ca40ac5d7
ms.openlocfilehash: ccc9973c07da9eca4bfacfb3bc7d1228a976c78b


---
# <a name="planning-for-migration-to-system-center-configuration-manager"></a>Pianificazione della migrazione a System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima di eseguire la migrazione dei dati in una gerarchia di destinazione di System Center Configuration Manager, è importante avere una certa familiarità con i siti e le gerarchie in Configuration Manager. Per altre informazioni su siti e gerarchie, vedere [Nozioni fondamentali su System Center Configuration Manager](../../core/understand/fundamentals.md).  

 È necessario installare una gerarchia di System Center Configuration Manager come gerarchia di destinazione, prima di poter eseguire la migrazione di dati da una gerarchia di origine supportata.  

 Dopo l'installazione della gerarchia di destinazione, configurare le caratteristiche e le funzionalità di gestione che si desidera utilizzare nella gerarchia di destinazione prima di avviare la migrazione dei dati.  

 Potrebbe inoltre essere necessario pianificare la sovrapposizione tra la gerarchia di origine e la gerarchia di destinazione. Questo può verificarsi ad esempio quando la gerarchia di origine è configurata per l'utilizzo degli stessi limiti o percorsi di rete della gerarchia di destinazione, quindi si installano nuovi client nella gerarchia di destinazione e si utilizza l'assegnazione sito automatica. In questo scenario, dal momento che un client di Configuration Manager appena installato è in grado di selezionare un sito di qualsiasi gerarchia, potrebbe verificarsi un'assegnazione errata alla gerarchia di origine. Pianificare quindi l'assegnazione di ogni nuovo client nella gerarchia di destinazione a un sito specifico di tale gerarchia e non utilizzare l'assegnazione sito automatica.  

 Per altre informazioni sulle assegnazioni del sito, vedere la sezione [Considerazioni sull'assegnazione sito dei client](../../core/plan-design/hierarchy/interoperability-between-different-versions.md#BKMK_SupConfigSiteAssignment) nell'argomento [Interoperabilità tra versioni diverse di System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

## <a name="planning-topics"></a>Argomenti sulla pianificazione  
 Usare gli argomenti seguenti per pianificare la migrazione di una gerarchia di origine supportata in una gerarchia di destinazione di System Center Configuration Manager:  

-   [Prerequisiti per la migrazione in System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md)  

-   [Elenchi di controllo per gli amministratori per la pianificazione della migrazione in System Center Configuration Manager](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Determinare se eseguire la migrazione dei dati a System Center Configuration Manager](../../core/migration/determine-whether-to-migrate-data.md)  

-   [Pianificazione di una strategia per la gerarchia di origine in System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md)  

-   [Elenchi di controllo per gli amministratori per la pianificazione della migrazione in System Center Configuration Manager](../../core/migration/administrator-checklists-for-migration-planning.md)  

-   [Pianificazione di una strategia di migrazione client in System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md)  

-   [Pianificazione di una strategia di migrazione per la distribuzione del contenuto in System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md)  

-   [Pianificazione della migrazione degli oggetti di Configuration Manager a System Center Configuration Manager](../../core/migration/planning-for-the-migration-of-objects.md)  

-   [Pianificazione del monitoraggio dell'attività di migrazione in System Center Configuration Manager](../../core/migration/planning-to-monitor-migration-activity.md)  

-   [Pianificazione del completamento della migrazione in System Center Configuration Manager](../../core/migration/planning-to-complete-migration.md)  



<!--HONumber=Dec16_HO3-->



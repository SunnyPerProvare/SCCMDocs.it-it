---
title: Completare la migrazione
titleSuffix: Configuration Manager
description: "Informazioni su come completare la migrazione a una gerarchia di destinazione di System Center Configuration Manager dopo che una gerarchia di origine non contiene più dati."
ms.custom: na
ms.date: 1/12/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4854b50-2e8c-414c-a872-9579554dca98
caps.latest.revision: "5"
caps.handback.revision: "0"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: 67e1d850043d5b922ab53dd13a782414730d5866
ms.sourcegitcommit: ca9d15dfb1c9eb47ee27ea9b5b39c9f8cdcc0748
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/04/2018
---
# <a name="plan-to-complete-migration-in-system-center-configuration-manager"></a>Pianificare il completamento della migrazione in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Con System Center Configuration Manager, è possibile completare il processo di migrazione quando una gerarchia di origine non contiene più dati per la migrazione alla gerarchia di destinazione. Il completamento della migrazione include i passaggi generali seguenti:  

-   Assicurarsi che sia stata eseguita la migrazione dei dati necessari. Prima di completare la migrazione dalla gerarchia di origine, assicurarsi che tutte le risorse richieste siano state migrate correttamente alla gerarchia di destinazione. Tra le risorse sono inclusi dati e client.  

-   Interrompere la raccolta di dati dai siti di origine. Per completare la migrazione da una gerarchia di origine, è necessario prima interrompere la raccolta di dati dai siti di origine.  

-   Pulire i dati di migrazione. Dopo aver interrotto la raccolta di dati da tutti i siti di origine in una gerarchia di origine, è possibile rimuovere i dati sul processo di migrazione e sulla gerarchia di origine dal database della gerarchia di destinazione.  

-   Rimuovere le autorizzazioni della gerarchia di origine. Dopo aver completato la migrazione da una gerarchia di origine e quando la gerarchia non contiene più le risorse gestite, è possibile rimuovere le autorizzazioni dei siti nella gerarchia di origine e la relativa infrastruttura dall'ambiente. Per informazioni sulla rimozione delle autorizzazioni dai siti e dalle gerarchie di origine, vedere la documentazione della relativa versione di Configuration Manager.  

Usare le sezioni seguenti per pianificare il completamento della migrazione da una gerarchia di origine arrestando la raccolta dati e pulendo i dati di migrazione:  

-   [Pianificare l'arresto della raccolta dati](#Plan_to_Stop_Data_Gath)  

-   [Pianificare la pulizia dei dati di migrazione](#Plan_to_clean_up)  

##  <a name="Plan_to_Stop_Data_Gath"></a> Pianificare l'arresto della raccolta dati  
 Prima di completare la migrazione ed eseguire la pulizia dei dati di migrazione, è necessario interrompere la raccolta dei dati da ciascun sito di origine nella gerarchia di origine. Per interrompere la raccolta dati da ciascun sito di origine, è necessario eseguire il comando **Interrompi raccolta dati** sui siti di origine di livello inferiore, quindi ripetere il processo su ciascun sito padre. L'interruzione della raccolta dati nel sito principale della gerarchia di origine deve rappresentare l'ultimo passaggio. È necessario interrompere la raccolta dati in ogni sito figlio prima di eseguire questo comando su un sito padre. In genere, si interrompe la raccolta dati solo quando si è pronti a completare il processo di migrazione.  

 Dopo aver interrotto la raccolta dati da un sito di origine, i punti di distribuzione condivisi da quel sito non sono più disponibili come percorsi del contenuto per i client nella gerarchia di destinazione. Pertanto, assicurarsi che qualsiasi contenuto migrato, per cui i client nella gerarchia di destinazione richiedono l'accesso, rimanga disponibile tramite una delle seguenti opzioni:  

-   Nella gerarchia di destinazione, distribuire il contenuto almeno a un punto di distribuzione.  

-   Prima di interrompere la raccolta dei dati da un sito di origine, aggiornare o riassegnare i punti di distribuzione condivisi con il contenuto richiesto. Per altre informazioni sull'aggiornamento o sulla riassegnazione dei punti di distribuzione condivisi, vedere le sezioni applicabili in [Pianificazione di una strategia di migrazione per la distribuzione del contenuto in System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

Dopo aver interrotto la raccolta dati da ogni sito di origine nella gerarchia di origine, è possibile pulire i dati di migrazione. Fino a quando non viene completata la pulizia dei dati di migrazione, ogni processo di migrazione eseguito o pianificato rimane accessibile nella console di Configuration Manager.  

Per altre informazioni sui siti di origine e sulla raccolta dati, vedere [Pianificazione di una strategia per la gerarchia di origine in System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).  

##  <a name="Plan_to_clean_up"></a> Pianificare la pulizia dei dati di migrazione  
 L'ultimo passaggio necessario per completare la migrazione consiste nella pulizia dei dati di migrazione. È possibile utilizzare il comando **Pulisci dati migrazione** dopo aver interrotto la raccolta dei dati per ogni sito di origine nella gerarchia di origine. Questa azione facoltativa determina la rimozione dei dati sulla gerarchia di origine corrente dal database della gerarchia di destinazione.  

 Durante la pulizia, la maggior parte dei dati sulla migrazione viene rimossa dal database della gerarchia di destinazione. Tuttavia, vengono conservati i dettagli sugli oggetti migrati. Con questi dettagli è possibile usare l'area di lavoro **Migrazione** per riconfigurare la gerarchia di origine che contiene i dati di cui è stata eseguita la migrazione per riprendere la migrazione dalla gerarchia di origine o rivedere gli oggetti e la proprietà sito degli oggetti di cui prima è stata eseguita la migrazione.  

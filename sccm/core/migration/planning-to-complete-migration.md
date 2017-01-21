---
title: Completare la migrazione | Microsoft Docs
description: "Informazioni su come completare la migrazione a una gerarchia di destinazione di System Center Configuration Manager dopo che una gerarchia di origine non contiene più dati."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4854b50-2e8c-414c-a872-9579554dca98
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5e3d3f4194b06442e34c10988a20fe9ca40ac5d7
ms.openlocfilehash: 0595ab87222aca543ae67a33c2b9fab780c6160f


---
# <a name="planning-to-complete-migration-in-system-center-configuration-manager"></a>Pianificazione del completamento della migrazione in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Con System Center Configuration Manager, quando una gerarchia di origine non contiene più dati per la migrazione alla gerarchia di destinazione, è possibile completare il processo di migrazione. Il completamento della migrazione include i passaggi generali seguenti:  

-   Assicurarsi che la migrazione dei dati necessari sia stata completata. Prima di completare la migrazione dalla gerarchia di origine, assicurarsi che tutte le risorse richieste siano state migrate correttamente alla gerarchia di destinazione. Tra le risorse sono inclusi dati e client.  

-   Interrompere la raccolta di dati dai siti di origine. Per completare la migrazione da una gerarchia di origine, è necessario prima interrompere la raccolta di dati dai siti di origine.  

-   Pulire i dati di migrazione. Dopo aver interrotto la raccolta di dati da tutti i siti di origine in una gerarchia di origine, è possibile rimuovere i dati sul processo di migrazione e sulla gerarchia di origine dal database della gerarchia di destinazione.  

-   Rimuovere le autorizzazioni della gerarchia di origine. Dopo aver completato la migrazione da una gerarchia di origine e quando la gerarchia non contiene più le risorse gestite, è possibile rimuovere le autorizzazioni dei siti nella gerarchia di origine e la relativa infrastruttura dall'ambiente. Per informazioni sulla rimozione delle autorizzazioni dai siti e dalle gerarchie di origine, vedere la documentazione della relativa versione di Configuration Manager.  

Utilizzare le seguenti sezioni per pianificare il completamento della migrazione da una gerarchia di origine tramite interruzione della raccolta dati e successiva pulizia dei dati di migrazione:  

-   [Pianificare l'interruzione della raccolta dati](#Plan_to_Stop_Data_Gath)  

-   [Pianificare la pulizia dei dati di migrazione](#Plan_to_clean_up)  

##  <a name="a-nameplantostopdatagatha-plan-to-stop-gathering-data"></a><a name="Plan_to_Stop_Data_Gath"></a> Pianificare l'interruzione della raccolta dati  
 Prima di completare la migrazione ed eseguire la pulizia dei dati di migrazione, è necessario interrompere la raccolta dei dati da ciascun sito di origine nella gerarchia di origine. Per interrompere la raccolta dati da ciascun sito di origine, è necessario eseguire il comando **Interrompi raccolta dati** sui siti di origine di livello inferiore, quindi ripetere il processo su ciascun sito padre. L'interruzione della raccolta dati nel sito principale della gerarchia di origine deve rappresentare l'ultimo passaggio. È necessario interrompere la raccolta dati in ogni sito figlio prima di eseguire questo comando su un sito padre. In genere, si interrompe la raccolta dati solo quando si è pronti a completare il processo di migrazione.  

 Dopo aver interrotto la raccolta dati da un sito di origine, i punti di distribuzione condivisi da quel sito non sono più disponibili come percorsi del contenuto per i client nella gerarchia di destinazione. Pertanto, assicurarsi che qualsiasi contenuto migrato, per cui i client nella gerarchia di destinazione richiedono l'accesso, rimanga disponibile tramite una delle seguenti opzioni:  

-   Nella gerarchia di destinazione, distribuire il contenuto almeno a un punto di distribuzione.  

-   Prima di interrompere la raccolta dei dati da un sito di origine, aggiornare o riassegnare i punti di distribuzione condivisi con il contenuto richiesto. Per altre informazioni sull'aggiornamento o sulla riassegnazione dei punti di distribuzione condivisi, vedere le sezioni applicabili nell'argomento [Pianificazione di una strategia di migrazione per la distribuzione del contenuto in System Center Configuration Manager](../../core/migration/planning-a-content-deployment-migration-strategy.md).  

Dopo aver interrotto la raccolta dati da ogni sito di origine nella gerarchia di origine, è possibile pulire i dati di migrazione. Fino a quando non viene completata la pulizia dei dati di migrazione, ogni processo di migrazione eseguito o pianificato rimane accessibile nella console di Configuration Manager.  

Per altre informazioni sui siti di origine e sulla raccolta dati, vedere [Pianificazione di una strategia per la gerarchia di origine in System Center Configuration Manager](../../core/migration/planning-a-source-hierarchy-strategy.md).  

##  <a name="a-nameplantocleanupa-plan-to-clean-up-migration-data"></a><a name="Plan_to_clean_up"></a> Pianificare la pulizia dei dati di migrazione  
 L'ultimo passaggio per completare la migrazione consiste nella pulizia dei dati di migrazione. È possibile utilizzare il comando **Pulisci dati migrazione** dopo aver interrotto la raccolta dei dati per ogni sito di origine nella gerarchia di origine. Questa azione facoltativa determina la rimozione dei dati sulla gerarchia di origine corrente dal database della gerarchia di destinazione.  

 Durante la pulizia, la maggior parte dei dati sulla migrazione viene rimossa dal database della gerarchia di destinazione. Tuttavia, vengono conservati i dettagli sugli oggetti migrati. Con questi dettagli è possibile utilizzare l'area di lavoro **Migrazione** per riconfigurare la gerarchia di origine che contiene i dati migrati per riprendere la migrazione dalla gerarchia di origine o rivedere gli oggetti e la proprietà sito degli oggetti precedentemente migrati.  



<!--HONumber=Dec16_HO3-->



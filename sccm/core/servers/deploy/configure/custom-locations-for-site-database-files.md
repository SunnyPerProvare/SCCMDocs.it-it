---
title: Percorsi personalizzati dei file del database | System Center Configuration Manager
description: Di seguito viene spiegato come specificare percorsi personalizzati per i file di database di SQL Server.
ms.custom: na
ms.date: 10/06/2016
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e8625d753fd2832009c9a3dc0b12b9a44f93c091

---
# <a name="custom-locations-for-system-center-configuration-manager-site-database-files"></a>Percorsi personalizzati per i file di database del sito di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

 System Center Configuration Manager supporta percorsi personalizzati per i file di database di SQL Server.  

> [!NOTE]  
>  L'opzione per specificare percorsi file non predefiniti non è disponibile quando si usa un cluster SQL Server.  

 **Durante l'installazione** di un nuovo sito primario o di un sito di amministrazione centrale, è possibile:  

-   Specificare i percorsi file non predefiniti per il database del sito: il programma di installazione di Configuration Manager crea quindi il database del sito usando tali percorsi.  

-   Specificare l'uso di un database di SQL Server creato in precedenza che usi percorsi file personalizzati: il programma di installazione di  Configuration Manager usa tale database con i relativi percorsi file configurati in precedenza.  

**Al termine dell'installazione** , è possibile modificare il percorso dei file di database del sito. A questo scopo, è necessario arrestare il sito e modificare il percorso file in SQL Server:  

-   Nel server del sito di Configuration Manager interrompere il servizio **SMS_Executive**.  

-   Per istruzioni su come spostare un database utente, consultare la documentazione per la versione di SQL Server in uso. Ad esempio, se si usa SQL Server 2014, vedere [Spostare database utente](https://technet.microsoft.com/library/ms345483\(v=sql.120\).aspx) su TechNet.  

-   Dopo aver completato lo spostamento dei file di database, è necessario riavviare il servizio SMS_Executive sul server del sito di Configuration Manager.  



<!--HONumber=Nov16_HO1-->


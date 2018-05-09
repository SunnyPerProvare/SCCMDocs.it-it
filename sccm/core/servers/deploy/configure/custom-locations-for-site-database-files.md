---
title: Percorsi personalizzati dei file di database
titleSuffix: Configuration Manager
description: Di seguito viene spiegato come specificare percorsi personalizzati per i file di database di SQL Server.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 597ce060dc1fb37f1cc827da3e1c059958a91163
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="custom-locations-for-system-center-configuration-manager-site-database-files"></a>Percorsi personalizzati per i file di database del sito di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

 System Center Configuration Manager supporta percorsi personalizzati per i file di database di SQL Server.  

> [!NOTE]  
>  L'opzione per specificare percorsi file non predefiniti non è disponibile quando si usa un cluster SQL Server.  

 **Durante l'installazione** di un nuovo sito primario o di un sito di amministrazione centrale, è possibile:  

-   **Specificare percorsi file non predefiniti per il database del sito**: il programma di installazione di Configuration Manager crea quindi il database del sito usando questi percorsi.  

-   **Specificare l'uso di un database di SQL Server creato in precedenza con percorsi file personalizzati**: il programma di installazione di Configuration Manager usa tale database con i relativi percorsi configurati in precedenza.  

**Al termine dell'installazione**, è possibile modificare il percorso dei file di database del sito. A questo scopo, è necessario arrestare il sito e modificare il percorso file in SQL Server:  

-   Nel server del sito di Configuration Manager interrompere il servizio **SMS_Executive**.  

-   Per istruzioni su come spostare un database utente, consultare la documentazione per la versione di SQL Server in uso. Ad esempio, se si usa SQL Server 2014, vedere [Spostare database utente](https://technet.microsoft.com/library/ms345483\(v=sql.120\).aspx) su TechNet.  

-   Al termine dello spostamento dei file di database, è necessario riavviare il servizio **SMS_Executive** sul server del sito di Configuration Manager.  

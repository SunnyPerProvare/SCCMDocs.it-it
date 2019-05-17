---
title: Percorsi personalizzati dei file di database
titleSuffix: Configuration Manager
description: Di seguito viene spiegato come specificare percorsi personalizzati per i file di database di SQL Server.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 500a9aa6-68aa-44eb-bf49-350c1314a697
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2341eb013b5ca03a9b4aa0a3e548facd01395121
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65498728"
---
# <a name="custom-locations-for-system-center-configuration-manager-site-database-files"></a>Percorsi personalizzati per i file di database del sito di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

 System Center Configuration Manager supporta percorsi personalizzati per i file di database di SQL Server.  

> [!NOTE]  
>  L'opzione per specificare percorsi file non predefiniti non è disponibile quando si usa un cluster SQL Server.  

 **Durante l'installazione** di un nuovo sito primario o di un sito di amministrazione centrale, è possibile:  

-   **Specificare percorsi dei file non predefiniti per il database del sito**: l'installazione di Configuration Manager crea quindi il database del sito usando tali percorsi.  

-   **Specificare l'uso di un database SQL Server creato in precedenza che usa percorsi dei file personalizzati**:  l'installazione di Configuration Manager usa quindi tale database creato in precedenza e i relativi percorsi di file preconfigurati.  

**Al termine dell'installazione**, è possibile modificare il percorso dei file di database del sito. A questo scopo, è necessario arrestare il sito e modificare il percorso file in SQL Server:  

-   Nel server del sito di Configuration Manager interrompere il servizio **SMS_Executive**.  

-   Per istruzioni su come spostare un database utente, consultare la documentazione per la versione di SQL Server in uso. Ad esempio, se si usa SQL Server 2014, vedere [Spostare database utente](https://technet.microsoft.com/library/ms345483\(v=sql.120\).aspx) su TechNet.  

-   Al termine dello spostamento dei file di database, è necessario riavviare il servizio **SMS_Executive** sul server del sito di Configuration Manager.  

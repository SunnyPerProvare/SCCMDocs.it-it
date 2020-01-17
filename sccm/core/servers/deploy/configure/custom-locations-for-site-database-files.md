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
ms.openlocfilehash: beddc89ea1925c192e275fc2768eb17c8b47c7ed
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75798837"
---
# <a name="custom-locations-for-configuration-manager-site-database-files"></a>Percorsi personalizzati per i file di database del sito di Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

 Configuration Manager supporta percorsi personalizzati per i file di database di SQL Server.  

> [!NOTE]  
>  L'opzione per specificare percorsi file non predefiniti non è disponibile quando si usa un cluster SQL Server.  

 **Durante l'installazione** di un nuovo sito primario o di un sito di amministrazione centrale, è possibile:  

-   **Specificare percorsi dei file non predefiniti per il database del sito**: l'installazione di Configuration Manager crea quindi il database del sito usando tali percorsi.  

-   **Specificare l'uso di un database SQL Server creato in precedenza che usa percorsi dei file personalizzati**:  l'installazione di Configuration Manager usa quindi tale database creato in precedenza e i relativi percorsi di file preconfigurati.  

**Al termine dell'installazione**, è possibile modificare il percorso dei file di database del sito. A questo scopo, è necessario arrestare il sito e modificare il percorso file in SQL Server:  

-   Nel server del sito di Configuration Manager interrompere il servizio **SMS_Executive**.  

-   Per istruzioni su come spostare un database utente, consultare la documentazione per la versione di SQL Server in uso. Ad esempio, se si usa SQL Server 2014, vedere [Spostare database utente](https://technet.microsoft.com/library/ms345483\(v=sql.120\).aspx) su TechNet.  

-   Al termine dello spostamento dei file di database, è necessario riavviare il servizio **SMS_Executive** sul server del sito di Configuration Manager.  

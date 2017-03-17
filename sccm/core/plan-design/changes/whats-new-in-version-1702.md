---
title: Nuova versione 1702 | Microsoft Docs
description: "Ottenere informazioni dettagliate sulle modifiche e le nuove funzionalità introdotte nella versione 1702 di System Center Configuration Manager."
ms.custom: na
ms.date: 03/27/2017
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: Brenduns
ms.author: brenduns
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: f9097014c7e988ec8e139e518355c4efb19172b3
ms.openlocfilehash: 473ba742bea74cbfdf8cab550244ccd522523718
ms.lasthandoff: 03/04/2017

---
# <a name="what39s-new-in-version-1702-of-system-center-configuration-manager"></a>Novità della versione 1702 di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

L'aggiornamento 1702 per System Center Configuration Manager (Current Branch) è disponibile come aggiornamento nella console per siti installati in precedenza che eseguono la versione 1606 o 1610. È disponibile anche come versione di base da usare durante l'installazione di una nuova distribuzione.

> [!TIP]  
> Per installare un nuovo sito, è necessario usare una versione base di Configuration Manager.  
>  Sono disponibili altre informazioni su:    
>  -   [Installing new sites](https://technet.microsoft.com/library/mt590197.aspx) (Installare nuovi siti)  
>  -   [Installing updates at sites](https://technet.microsoft.com/library/mt607046.aspx) (Installare aggiornamenti nei siti)  
>  -   [Baseline and update versions](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions) (Versioni di base e di aggiornamento)  

Le sezioni seguenti illustrano in dettaglio le modifiche e le nuove funzionalità introdotte nella versione 1702 di Configuration Manager.  


## <a name="data-warehouse-service-point"></a>Punto di servizio del data warehouse
Usare il punto di servizio del data warehouse per archiviare e creare report di dati cronologici a lungo termine per la distribuzione di Configuration Manager.

Il data warehouse supporta fino a 2 TB di dati, con timestamp per il rilevamento delle modifiche. L'archiviazione dei dati viene eseguita tramite sincronizzazioni automatizzate dal database del sito di Configuration Manager al database del data warehouse. Queste informazioni diventano quindi accessibili dal punto di Reporting Services.



Per altre informazioni, vedere [Punto di servizio del data warehouse](/sccm/core/servers/manage/data-warehouse).


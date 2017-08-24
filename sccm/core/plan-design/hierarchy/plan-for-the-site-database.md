---
title: Pianificare il database del sito | Microsoft Docs
description: Prendere in considerazione il database del sito e il ruolo del server del database del sito quando si pianifica la gerarchia di System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
caps.latest.revision: "5"
caps.handback.revision: "0"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: d4efe1f013dbb74efca79cd27f7248fc085c7424
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-the-site-database-for-system-center-configuration-manager"></a>Pianificare per il database del sito per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Il server di database del sito è un computer in cui viene eseguita una versione supportata di Microsoft SQL Server. SQL Server viene usato per archiviare le informazioni per i siti di Configuration Manager. Ogni sito in una gerarchia di Configuration Manager contiene un database e un server del sito a cui è assegnato il ruolo del server del database del sito.  

-   Per i siti di amministrazione centrale e i siti primari, è possibile installare SQL Server sul server del sito oppure su un computer diverso dal server del sito.  

-   Per i siti secondari è possibile usare SQL Server Express anziché un'installazione completa di SQL Server. Il server database deve tuttavia essere eseguito nel server del sito secondario.  

Per ospitare il database del sito è possibile usare le configurazioni di SQL Server seguenti:  

-   L'istanza predefinita di SQL Server  

-   Un'istanza denominata in un unico computer che esegue SQL Server  

-   Un'istanza denominata in un'istanza in cluster di SQL Server  

-   Un gruppo di disponibilità AlwaysOn di SQL Server (a partire dalla versione 1602 di System Center Configuration Manager)


Per ospitare il database del sito, SQL Server deve soddisfare i requisiti descritti in [Supporto per le versioni di SQL Server per System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  



## <a name="remote-database-server-location-considerations"></a>Considerazioni sul percorso del server database remoto  

Se si usa un computer server database remoto, verificare che la connessione di rete corrispondente sia una connessione a disponibilità e larghezza di banda elevate. Il server del sito e alcuni ruoli del sistema del sito devono comunicare costantemente con il server remoto che ospita il database del sito.

-   La larghezza di banda richiesta per le comunicazioni con il server database dipende da una combinazione di numerose e diverse configurazioni di siti e client. Pertanto, non è possibile prevedere adeguatamente la larghezza di banda effettivamente richiesta.  

-   Ogni computer su cui è in esecuzione il provider SMS e che si connette al database del sito contribuisce ad aumentare i requisiti di larghezza di banda della rete.  

-   Il computer che esegue SQL Server deve essere posizionato in un dominio con un trust bidirezionale con il server del sito e tutti i computer che eseguono il provider SMS.  

-   Quando il database del sito ha un percorso condiviso con il server del sito, non è possibile usare un server SQL del cluster per il server di database del sito.  


In genere, un server del sistema del sito supporta ruoli del sistema del sito solo da un unico sito di Configuration Manager. È tuttavia possibile usare istanze diverse di SQL Server, su server cluster o non cluster che eseguono SQL Server, per ospitare un database da diversi siti di Configuration Manager. Per supportare i database da siti diversi, è necessario configurare ogni istanza di SQL Server in modo da usare porte univoche per la comunicazione.  

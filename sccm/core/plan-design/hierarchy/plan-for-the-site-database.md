---
title: Pianificare il database del sito | Microsoft Docs
description: Prendere in considerazione il database del sito e il ruolo del server del database del sito quando si pianifica la gerarchia di System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 104fb4cc-6e83-40a3-8e6b-ac909fb9ec7d
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 012d5b313487640faeebe5b49064c74d41a7edb9


---
# <a name="plan-for-the-site-database-for-system-center-configuration-manager"></a>Pianificare per il database del sito per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Il server del database del sito è un computer su che esegue una versione supportata di Microsoft SQL Server che archivia le informazioni per i siti di Configuration Manager. Ogni sito in una gerarchia di Configuration Manager contiene un database e un server del sito a cui è assegnato il ruolo del server del database del sito.  

-   Per i siti di amministrazione centrale e i siti primari è possibile installare SQL Server nel server del sito oppure in un computer diverso dal server del sito.  

-   Per i siti secondari è possibile usare SQL Server Express invece di un'installazione SQL Server completa. Tuttavia, il server del database deve essere eseguito nel server del sito secondario.  

Se si usa un computer server di database remoto, verificare che la connessione di rete corrispondente sia una connessione a disponibilità e larghezza di banda elevate. Ciò è utile perché il server del sito e alcuni ruoli del sistema del sito devono comunicare costantemente con il server SQL che ospita il database del sito.  


**Quando si seleziona un percorso del server di database remoto, considerare quanto segue:**  

-   La larghezza di banda richiesta per le comunicazioni con il server di database dipende da una combinazione di numerose e diverse configurazioni di siti e client. Pertanto, non è possibile prevedere adeguatamente la larghezza di banda effettivamente richiesta.  

-   Ogni computer su cui è in esecuzione il provider SMS e che si connette al database del sito contribuisce ad aumentare i requisiti di larghezza di banda della rete.  

-   Il computer su cui è in esecuzione SQL Server deve essere posizionato in un dominio con un trust bidirezionale con il server del sito e tutti i computer che eseguono il provider SMS.  

-   Quando il database del sito ha un percorso condiviso con il server del sito, non è possibile usare un server SQL del cluster per il server di database del sito.  


In genere, un server di sistema del sito supporta ruoli di sistema del sito solo da un singolo sito di Configuration Manager; tuttavia, è possibile usare istanze diverse di SQL Server, su server cluster o non cluster che eseguono SQL Server, per ospitare un database da siti di Configuration Manager diversi. Per supportare i database da siti diversi, è necessario configurare ogni istanza di SQL Server in modo da usare porte univoche per la comunicazione.  


**Per ospitare il database del sito è possibile usare le configurazioni di SQL Server seguenti:**  

-   L'istanza predefinita di SQL Server  

-   Un'istanza denominata in un unico computer che esegue SQL Server  

-   Un'istanza denominata in un'istanza in cluster di SQL Server  

-   Un gruppo di disponibilità AlwaysOn di SQL Server (a partire dalla versione 1602)


**Prerequisiti per il database del sito:**  

-   Per ospitare il database del sito, SQL Server deve soddisfare i requisiti descritti in [Supporto per le versioni di SQL Server per System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  



<!--HONumber=Dec16_HO3-->



---
title: Introduzione alle query | System Center Configuration Manager
description: Creare ed eseguire query per individuare gli oggetti che soddisfano i criteri delle query stesse all'interno di una gerarchia di System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 054f3cc5ba7963231df93ed0ceb973d20b2e8f8e


---
# <a name="introduction-to-queries-in-system-center-configuration-manager"></a>Introduzione alle query in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile creare ed eseguire query per individuare gli oggetti che soddisfano i criteri delle query stesse all'interno di una gerarchia di System Center Configuration Manager. Questi oggetti possono essere tipi specifici di computer o gruppi di utenti. Le query possono restituire molti tipi di oggetti di Configuration Manager, ad esempio siti, raccolte, applicazioni e dati di inventario.  

 Quando si crea una query, è necessario specificare un minimo di due parametri: dove eseguire la ricerca e cosa si vuole cercare. Ad esempio, per trovare la quantità di spazio disponibile su disco in tutti i computer in un sito di Configuration Manager è possibile creare una query per cercare lo spazio disponibile su disco nella classe di attributi **Disco logico** e nell'attributo **Spazio disponibile (MB)**.  

 Dopo aver creato una query iniziale, è possibile specificare ulteriori criteri di query. Ad esempio, è possibile specificare che i risultati della query includano solo i computer assegnati al sito specificato. È inoltre possibile modificare la modalità di visualizzazione dei risultati in modo che questi vengano presentati in un ordine significativo. Ad esempio, è possibile specificare che i risultati vengano visualizzati in ordine crescente o decrescente in base alla quantità di spazio disponibile su disco.  

 Quando si crea una query, questa viene archiviata da Configuration Manager e visualizzata nel nodo **Query** nell'area di lavoro **Monitoraggio**. Da questa posizione è possibile creare una nuova query e quindi eseguire, aggiornare o gestire una query esistente.  

 È anche possibile importare una query in una regola di query all'interno di una raccolta di Configuration Manager. Per altre informazioni, vedere [How to create collections in System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md) (Come creare le raccolte in System Center Configuration Manager).  

## <a name="see-also"></a>Vedere anche  
 [Queries technical reference for System Center Configuration Manager](../../../core/servers/manage/queries-technical-reference.md) (Riferimento tecnico per le query per System Center Configuration Manager)



<!--HONumber=Nov16_HO1-->



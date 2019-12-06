---
title: Introduzione alle query
titleSuffix: Configuration Manager
description: Creare ed eseguire query per individuare gli oggetti che soddisfano i criteri delle query stesse all'interno di una gerarchia di System Center Configuration Manager.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 03d1b3a9-41db-4d3a-a70e-e05ab5dc8141
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28fe8d38b03efaa101cfe01d8a8a054f0b26f2ed
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "67561947"
---
# <a name="introduction-to-queries-in-system-center-configuration-manager"></a>Introduzione alle query in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile creare ed eseguire query per individuare gli oggetti che soddisfano i criteri delle query stesse all'interno di una gerarchia di System Center Configuration Manager. Questi oggetti possono essere tipi specifici di computer o gruppi di utenti. Le query possono restituire molti tipi di oggetti di Configuration Manager, ad esempio siti, raccolte, applicazioni e dati di inventario.  

## <a name="query-creation-overview"></a>Panoramica sulla creazione di query

 Quando si crea una query, è necessario specificare un minimo di due parametri: dove eseguire la ricerca e cosa si vuole cercare. Ad esempio, per trovare la quantità di spazio disponibile su disco in tutti i computer in un sito di Configuration Manager è possibile creare una query per cercare lo spazio disponibile su disco nella classe di attributi **Disco logico** e nell'attributo **Spazio disponibile (MB)** .  

 Dopo aver creato una query iniziale, è possibile specificare ulteriori criteri di query. Ad esempio, è possibile specificare che i risultati della query includano solo i computer assegnati al sito specificato. È anche possibile modificare la modalità di visualizzazione dei risultati in modo che questi vengano presentati in un ordine significativo. Ad esempio, è possibile specificare che i risultati vengano visualizzati in ordine crescente o decrescente in base alla quantità di spazio disponibile nell'unità disco rigido.  

 Quando si crea una query, questa viene archiviata da Configuration Manager e visualizzata nel nodo **Query** nell'area di lavoro **Monitoraggio**. Da questa posizione è possibile creare nuove query ed eseguire, aggiornare e gestire le query esistenti.  

 È anche possibile importare una query in una regola di query all'interno di una raccolta di Configuration Manager. Per altre informazioni, vedere [How to create collections in System Center Configuration Manager](../../../core/clients/manage/collections/create-collections.md) (Come creare le raccolte in System Center Configuration Manager).  

## <a name="next-steps"></a>Passaggi successivi

 [Come creare query in System Center Configuration Manager](../../../core/servers/manage/create-queries.md)

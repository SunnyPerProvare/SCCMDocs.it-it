---
title: Updates Publisher
titleSuffix: Configuration Manager
description: Usare System Center Updates Publisher per gestire gli aggiornamenti personalizzati
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
caps.latest.revision: "1"
author: mestew
ms.author: mstewart
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.openlocfilehash: 6c0af411d51c2b56c5d8e6479112e6f9cb317971
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/04/2017
---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

*Si applica a: System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) è uno strumento autonomo che consente ai fornitori di software indipendenti o agli sviluppatori di applicazioni line-of-business di gestire aggiornamenti personalizzati. Sono inclusi gli aggiornamenti con dipendenze, ad esempio i driver o le aggregazioni di aggiornamenti.

Updates Publisher consente di effettuare le operazioni seguenti:

-   Importare aggiornamenti da cataloghi esterni (cataloghi di aggiornamenti non Microsoft).
-   Modificare le definizioni di aggiornamento, incluse l'applicabilità e la distribuzione dei metadati.
-   Esportare aggiornamenti in cataloghi esterni.
-   Pubblicare aggiornamenti in un server di aggiornamento.

Dopo aver pubblicato aggiornamenti in un server di aggiornamento, è possibile usare System Center Configuration Manager per rilevare e distribuire tali aggiornamenti ai dispositivi gestiti.

> [!TIP]  
> La versione precedente, [System Center Updates Publisher 2011](http://go.microsoft.com/fwlink/?LinkId=848111), rimane supportata. Questa versione aggiornata mantiene le stesse funzionalità ma supporta altri sistemi operativi e nuove funzionalità per semplificare alcune attività. Offre inoltre un'interfaccia utente aggiornata.

## <a name="workspaces"></a>Aree di lavoro
Quando si apre Updates Publisher, per impostazione predefinita viene visualizzato automaticamente il nodo Panoramica dell'*area di lavoro Aggiornamenti*.

![Console di Updates Publisher](media/console1.png)   


Per organizzare Updates Publisher sono disponibili quattro aree di lavoro.


**Area di lavoro Aggiornamenti:** usare quest'area di lavoro per [creare](/sccm/sum/tools/create-updates-with-updates-publisher) e [gestire](/sccm/sum/tools/manage-updates-with-updates-publisher) aggiornamenti software e aggregazioni di aggiornamenti. Questo include l'assegnazione di aggiornamenti e aggregazioni a una pubblicazione, nonché la pubblicazione e l'esportazione degli stessi in un altro repository di Updates Publisher.

**Area di lavoro Pubblicazioni:** usare quest'area per [gestire le pubblicazioni](/sccm/sum/tools/updates-publisher-publications). Una pubblicazione è gruppo di aggiornamenti creato per semplificare l'esportazione e la pubblicazione degli aggiornamenti stessi.

La gestione delle pubblicazioni include la pubblicazione di aggiornamenti in un server in modo che i client possano trovarli e installarli, l'esportazione di aggiornamenti e aggregazioni per l'uso da parte di altre installazioni di Updates Publisher e la modifica del contenuto o dei dettagli di una pubblicazione.



**Area di lavoro Regole:** usare quest'area per [gestire le regole di applicabilità](/sccm/sum/tools/updates-publisher-applicability-rules) che è possibile salvare e quindi usare con gli aggiornamenti distribuiti. Esistono due tipi di regole:

-   Regole installabili: queste regole consentono di determinare se un client deve installare un aggiornamento.
-   Regole installate: queste regole verificano se un aggiornamento è già installato.

**Area di lavoro Cataloghi:** usare quest'area di lavoro per aggiungere e [gestire cataloghi di aggiornamenti software](/sccm/sum/tools/updates-publisher-catalogs). Questo include l'importazione di aggiornamenti software da tali cataloghi nel repository di Updates Publisher.
## <a name="first-steps"></a>Passaggi iniziali
Per iniziare, [installare](/sccm/sum/tools/install-updates-publisher), e quindi [configurare le opzioni](/sccm/sum/tools/updates-publisher-options) per Updates Publisher.

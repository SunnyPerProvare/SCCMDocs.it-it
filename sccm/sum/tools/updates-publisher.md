---
title: Updates Publisher
titleSuffix: Configuration Manager
description: Usare System Center Updates Publisher per gestire gli aggiornamenti personalizzati
ms.date: 6/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: dee1a5a998f6d99678f85e6d5f39e52cb35a2bad
ms.sourcegitcommit: 9648ce8a8b5c82518e7c8b6a7668e0e9b076cae6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 09/05/2019
ms.locfileid: "70378724"
---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

*Si applica a: System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) è uno strumento autonomo che consente ai fornitori di software indipendenti o agli sviluppatori di applicazioni line-of-business di gestire aggiornamenti personalizzati. Questa gestione degli aggiornamenti personalizzata include aggiornamenti con dipendenze, ad esempio driver e bundle di aggiornamenti.

Updates Publisher consente di effettuare le operazioni seguenti:

-   Importare aggiornamenti da cataloghi esterni (cataloghi di aggiornamenti non Microsoft).
-   Modificare le definizioni di aggiornamento, incluse l'applicabilità e la distribuzione dei metadati.
-   Esportare aggiornamenti in cataloghi esterni.
-   Pubblicare aggiornamenti in un server di aggiornamento.

Dopo aver pubblicato aggiornamenti in un server di aggiornamento, è possibile usare System Center Configuration Manager per rilevare e distribuire tali aggiornamenti ai dispositivi gestiti.

> [!TIP]  
> La versione precedente, [System Center Updates Publisher 2011](https://go.microsoft.com/fwlink/?LinkId=848111), rimane supportata. Questa versione aggiornata mantiene le stesse funzionalità ma supporta altri sistemi operativi e nuove funzionalità per semplificare alcune attività. Offre inoltre un'interfaccia utente aggiornata.

## <a name="workspaces"></a>Aree di lavoro
Quando si apre Updates Publisher, per impostazione predefinita viene visualizzato automaticamente il nodo Panoramica dell'*area di lavoro Aggiornamenti*.

![Console di Updates Publisher](media/console1.png)   


Per organizzare Updates Publisher sono disponibili quattro aree di lavoro.


**Area di lavoro Aggiornamenti:** usare quest'area di lavoro per [creare](/sccm/sum/tools/create-updates-with-updates-publisher) e [gestire](/sccm/sum/tools/manage-updates-with-updates-publisher) aggiornamenti software e aggregazioni di aggiornamenti. Questa area di lavoro include l'assegnazione di aggiornamenti e aggregazioni a una pubblicazione, nonché la pubblicazione e l'esportazione degli stessi in un altro repository di Updates Publisher.

**Area di lavoro Pubblicazioni:** usare quest'area di lavoro per [gestire le pubblicazioni](/sccm/sum/tools/updates-publisher-publications). Una pubblicazione è gruppo di aggiornamenti creato per semplificare l'esportazione e la pubblicazione degli aggiornamenti stessi.

La gestione delle pubblicazioni include la pubblicazione di aggiornamenti in un server in modo che i client possano trovarli e installarli, l'esportazione di aggiornamenti e aggregazioni per l'uso da parte di altre installazioni di Updates Publisher e la modifica del contenuto o dei dettagli di una pubblicazione.

**Area di lavoro Regole:** usare quest'area per [gestire le regole di applicabilità](/sccm/sum/tools/updates-publisher-applicability-rules) che è possibile salvare e quindi usare con gli aggiornamenti distribuiti. Esistono due tipi di regole:

-   Regole installabili: queste regole consentono di determinare se un client deve installare un aggiornamento.
-   Regole installate: queste regole verificano se un aggiornamento è già installato.

**Area di lavoro Cataloghi:** usare quest'area di lavoro per aggiungere e [gestire cataloghi di aggiornamenti software](/sccm/sum/tools/updates-publisher-catalogs). Questa area di lavoro include l'importazione di aggiornamenti software da tali cataloghi nel repository di Updates Publisher.

## <a name="whats-new-in-the-system-center-updates-publisher-preview"></a>Novità della versione di anteprima di System Center Updates Publisher

>[!NOTE] 
>Le informazioni contenute in questa sezione si applicano solo alla versione di anteprima di System Center Updates Publisher. Per installare l'anteprima, scaricarla dall' [area download Microsoft](https://www.microsoft.com/download/details.aspx?id=58390).

Nella versione di anteprima di System Center Updates Publisher è disponibile una nuova modalità di creazione per facilitare la creazione degli aggiornamenti. Quando si Abilita la modalità di creazione, un' **area di lavoro categorie** viene aggiunta alla schermata Start. Viene inoltre aggiunto un nuovo pulsante **detectoid** all' **area di lavoro aggiornamenti** quando è abilitata la modalità di creazione. 

### <a name="to-enable-authoring-mode-in-the-preview"></a>Per abilitare la modalità di creazione nell'anteprima

1. Nell'angolo superiore sinistro della console, fare clic sulla scheda **Updates Publisher** **Properties** , quindi scegliere **options**.
1. Passare alle opzioni di **creazione** .
1. Selezionare la casella **Abilita modalità di creazione**.

![Abilitare la modalità di creazione per Updates Publisher](media/scup-enable-authoring-mode.png)

### <a name="about-the-categories-workspace"></a>Informazioni sull'area di lavoro categorie

L'area di lavoro categorie consente agli autori degli aggiornamenti di organizzare gli aggiornamenti che appartengono insieme. Ad esempio, se si è un OEM, potrebbe essere necessario organizzare gli aggiornamenti in base a modelli o linee di prodotti. È possibile definire più categorie e categorie figlio ma non le categorie figlie figlio poiché si è limitati a due livelli.

![Screenshot dell'area di lavoro categorie](media/scup-categories-workspace.png)

### <a name="assign-an-update-to-a-category"></a>Assegnare un aggiornamento a una categoria

Dopo aver creato l'aggiornamento, è possibile assegnarlo a una categoria selezionando l'aggiornamento e quindi facendo clic sul pulsante **categorizza** . È anche possibile fare clic con il pulsante destro del mouse sull'aggiornamento e selezionare **categorizza**.

![Screenshot della categorizzazione di un aggiornamento](media/scup-categorize-update.png)


### <a name="about-detectoids"></a>Informazioni su detectoid

Una volta abilitata la modalità di creazione, è possibile creare detectoid per gli aggiornamenti. Detectoid sono utili quando si hanno più aggiornamenti che usano la stessa regola (o un set di regole) per determinare l'applicabilità. In questi casi, è necessario creare un detectoid e assegnarlo come prerequisito per un aggiornamento. È possibile assegnare più detectoid a un aggiornamento creato.


### <a name="create-a-detectoid"></a>Creare un detectoid

1. Aprire l'**area di lavoro Aggiornamenti**.
1. Sulla barra multifunzione fare clic sul pulsante **detectoid** .
1. Seguire le istruzioni della procedura guidata per creare il detectoid.



![Aggiornare i prerequisiti usando un detectoid](media/scup-detectoid-as-prerequisite.png)


## <a name="next-steps"></a>Passaggi successivi
Per iniziare, [installare](/sccm/sum/tools/install-updates-publisher), e quindi [configurare le opzioni](/sccm/sum/tools/updates-publisher-options) per Updates Publisher.

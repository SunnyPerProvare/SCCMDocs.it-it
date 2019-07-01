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
ms.openlocfilehash: 26ad3be032a3dd8ea21d7eeb6a4755c32d546f38
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2019
ms.locfileid: "67158653"
---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

*Si applica a: System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) è uno strumento autonomo che consente ai fornitori di software indipendenti o agli sviluppatori di applicazioni line-of-business di gestire aggiornamenti personalizzati. La gestione degli aggiornamenti personalizzati include gli aggiornamenti con dipendenze, come i driver e i bundle di aggiornamenti.

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


**Area di lavoro Aggiornamenti:** usare quest'area di lavoro per [creare](/sccm/sum/tools/create-updates-with-updates-publisher) e [gestire](/sccm/sum/tools/manage-updates-with-updates-publisher) aggiornamenti software e aggregazioni di aggiornamenti. Questa area di lavoro include l'assegnazione di aggiornamenti e aggregazioni a una pubblicazione, nonché la pubblicazione e l'esportazione degli stessi in un altro repository di Updates Publisher.

**Area di lavoro Pubblicazioni:** usare quest'area di lavoro per [gestire le pubblicazioni](/sccm/sum/tools/updates-publisher-publications). Una pubblicazione è gruppo di aggiornamenti creato per semplificare l'esportazione e la pubblicazione degli aggiornamenti stessi.

La gestione delle pubblicazioni include la pubblicazione di aggiornamenti in un server in modo che i client possano trovarli e installarli, l'esportazione di aggiornamenti e aggregazioni per l'uso da parte di altre installazioni di Updates Publisher e la modifica del contenuto o dei dettagli di una pubblicazione.

**Area di lavoro Regole:** usare quest'area per [gestire le regole di applicabilità](/sccm/sum/tools/updates-publisher-applicability-rules) che è possibile salvare e quindi usare con gli aggiornamenti distribuiti. Esistono due tipi di regole:

-   Regole installabili: queste regole consentono di determinare se un client deve installare un aggiornamento.
-   Regole installate: queste regole verificano se un aggiornamento è già installato.

**Area di lavoro Cataloghi:** usare quest'area di lavoro per aggiungere e [gestire cataloghi di aggiornamenti software](/sccm/sum/tools/updates-publisher-catalogs). Questa area di lavoro include l'importazione di aggiornamenti software da tali cataloghi nel repository di Updates Publisher.

## <a name="whats-new-in-the-system-center-updates-publisher-preview"></a>Novità nell'anteprima di System Center Updates Publisher

>[!NOTE] 
>Le informazioni contenute in questa sezione si applicano solo alla versione preview di System Center Updates publisher. Per installare l'anteprima, scaricarlo dal [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=58390).

L'anteprima per System Center Updates Publisher che consentono di creare gli aggiornamenti è una nuova modalità di creazione e modifica. Quando si abilita la modalità di creazione, un **dell'area di lavoro di categorie** viene aggiunto alla schermata start. Una nuova **Detectoid** pulsante verrà inoltre aggiunto il **area di lavoro aggiornamenti** quando è abilitata la modalità di creazione. 

### <a name="to-enable-authoring-mode-in-the-preview"></a>Per abilitare la modalità di creazione nel riquadro di anteprima

1. Nell'angolo superiore sinistro della console, fare clic sui **Updates Publisher** **delle proprietà** scheda e quindi scegliere **opzioni**.
1. Andare alla **Authoring** opzioni.
1. Selezionare la casella **abilita la modalità di creazione**.

![Abilitare la modalità di creazione per Updates Publisher](media/scup-enable-authoring-mode.png)

### <a name="about-the-categories-workspace"></a>Sull'area di lavoro categorie

L'area di lavoro di categorie consente agli autori di aggiornamento organizzare gli aggiornamenti che formano insieme. Ad esempio, se si ha un OEM, è possibile organizzare gli aggiornamenti basati su modelli o le linee di prodotti. È possibile definire più categorie e sottocategorie ma categorie figlio non complessivo è sono limitate a due livelli.

![Screenshot dell'area di lavoro di categorie](media/scup-categories-workspace.png)

### <a name="assign-an-update-to-a-category"></a>Assegnare un aggiornamento a una categoria

Dopo aver creato l'aggiornamento, è possibile assegnarla a una categoria selezionando l'aggiornamento, quindi scegliendo il **Categorizza** pulsante. È anche possibile fare doppio clic sull'aggiornamento e selezionare **Categorizza**.

![Screenshot della classificazione di un aggiornamento](media/scup-categorize-update.png)


### <a name="about-detectoids"></a>Sulle detectoid

Dopo aver abilitata la modalità di creazione, è possibile creare detectoids per gli aggiornamenti. Detectoid sono utili quando si dispongono di più aggiornamenti che usano la stessa regola o un set di regole per determinare l'applicabilità. In tali casi, si crea un detectoid e assegnarla come prerequisito per un aggiornamento. È possibile assegnare più detectoid a un aggiornamento creato.


### <a name="create-a-detectoid"></a>Creare un detectoid

1. Aprire l'**area di lavoro Aggiornamenti**.
1. Nella barra multifunzione scegliere la **Detectoid** pulsante.
1. Seguire le istruzioni della procedura guidata per creare i detectoid.



![Prerequisiti di aggiornamento usando un detectoid](media/scup-detectoid-as-prerequisite.png)


## <a name="next-steps"></a>Passaggi successivi
Per iniziare, [installare](/sccm/sum/tools/install-updates-publisher), e quindi [configurare le opzioni](/sccm/sum/tools/updates-publisher-options) per Updates Publisher.

---
title: Updates Publisher
titleSuffix: Configuration Manager
description: Usare System Center Updates Publisher per gestire gli aggiornamenti personalizzati
ms.date: 11/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 2200b02b-e76b-4aa7-a77a-6dc5e70f1333
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 173b1589eff40daa76ccb7e9d6f811e6096f8390
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75827112"
---
# <a name="system-center-updates-publisher"></a>System Center Updates Publisher

*Si applica a: System Center Updates Publisher*

System Center Updates Publisher (Updates Publisher) è uno strumento autonomo che consente ai fornitori di software indipendenti o agli sviluppatori di applicazioni line-of-business di gestire aggiornamenti personalizzati. Questa gestione degli aggiornamenti personalizzata include aggiornamenti con dipendenze, ad esempio driver e bundle di aggiornamenti.

Updates Publisher consente di effettuare le operazioni seguenti:

-   Importare aggiornamenti da cataloghi esterni (cataloghi di aggiornamenti non Microsoft).
-   Modificare le definizioni di aggiornamento, incluse l'applicabilità e la distribuzione dei metadati.
-   Esportare aggiornamenti in cataloghi esterni.
-   Pubblicare aggiornamenti in un server di aggiornamento.

Dopo aver pubblicato aggiornamenti in un server di aggiornamento, è possibile usare Configuration Manager per rilevare e distribuire tali aggiornamenti ai dispositivi gestiti.

## <a name="workspaces"></a>Aree di lavoro
Quando si apre Updates Publisher, per impostazione predefinita viene visualizzato automaticamente il nodo Panoramica dell'*area di lavoro Aggiornamenti*.

![Console di Updates Publisher](media/console1.png)


Per organizzare Updates Publisher sono disponibili quattro aree di lavoro.


**Updates Workspace** (Area di lavoro Aggiornamenti): usare quest'area di lavoro per [creare](/sccm/sum/tools/create-updates-with-updates-publisher) e [gestire](/sccm/sum/tools/manage-updates-with-updates-publisher) aggiornamenti software e pacchetti di aggiornamenti. Questa area di lavoro include l'assegnazione di aggiornamenti e aggregazioni a una pubblicazione, nonché la pubblicazione e l'esportazione degli stessi in un altro repository di Updates Publisher.

**Publications Workspace** (Area di lavoro Pubblicazioni): usare quest'area di lavoro per [gestire le pubblicazioni](/sccm/sum/tools/updates-publisher-publications). Una pubblicazione è gruppo di aggiornamenti creato per semplificare l'esportazione e la pubblicazione degli aggiornamenti stessi.

La gestione delle pubblicazioni include la pubblicazione di aggiornamenti in un server in modo che i client possano trovarli e installarli, l'esportazione di aggiornamenti e aggregazioni per l'uso da parte di altre installazioni di Updates Publisher e la modifica del contenuto o dei dettagli di una pubblicazione.

**Rules Workspace** (Area di lavoro Regole): usare quest'area per [gestire le regole di applicabilità](/sccm/sum/tools/updates-publisher-applicability-rules) che è possibile salvare e quindi usare con gli aggiornamenti distribuiti. Esistono due tipi di regole:

-   Regole installabili: queste regole consentono di determinare se un client deve installare un aggiornamento.
-   Regole installate: queste regole verificano se un aggiornamento è già installato.

**Catalogs Workspace** (Area di lavoro Cataloghi): usare quest'area di lavoro per aggiungere e [gestire cataloghi di aggiornamenti software](/sccm/sum/tools/updates-publisher-catalogs). Questa area di lavoro include l'importazione di aggiornamenti software da tali cataloghi nel repository di Updates Publisher.

## <a name="whats-new-in-system-center-updates-publisher"></a>Novità di System Center Updates Publisher

>[!NOTE] 
> La versione più recente di System Center Updates Publisher è stata rilasciata il 6 novembre 2019. Per ulteriori informazioni, vedere la sezione [cronologia delle versioni](#release-history) .

È disponibile una nuova modalità di creazione System Center Updates Publisher per facilitare la creazione degli aggiornamenti. Quando si Abilita la modalità di creazione, un' **area di lavoro categorie** viene aggiunta alla schermata Start. Viene inoltre aggiunto un nuovo pulsante **detectoid** all' **area di lavoro aggiornamenti** quando è abilitata la modalità di creazione.

### <a name="to-enable-authoring-mode"></a>Per abilitare la modalità di creazione

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

## <a name="release-history"></a>Cronologia versioni

- [2019 RTW versione 6.0.394.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/SCUP-adds-support-for-update-categories/ba-p/990111). Data di rilascio: 6 novembre 2019
- [Aggiornamento cumulativo versione 6.0.283.0 da KB4462765](https://support.microsoft.com/help/4462765/update-rollup-for-system-center-updates-publisher). Data di rilascio: 7 settembre 2018
- [2017 RTW versione 6.0.276.0](https://techcommunity.microsoft.com/t5/Configuration-Manager-Blog/System-Center-Updates-Publisher-adds-support-for-new-OSes/ba-p/274986). Data di rilascio: 26 marzo 2018


## <a name="next-steps"></a>Passaggi successivi
Per iniziare, [installare](/sccm/sum/tools/install-updates-publisher), e quindi [configurare le opzioni](/sccm/sum/tools/updates-publisher-options) per Updates Publisher.

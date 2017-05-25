---
title: Gestire le pubblicazioni | Microsoft Docs
description: Gestire gruppi di aggiornamenti software come una pubblicazione con System Center Updates Publisher
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e6c1df1d-7728-4980-9199-bc32cde5439e
caps.latest.revision: 1
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: NOINDEX, NOFOLLOW
ms.translationtype: Human Translation
ms.sourcegitcommit: 31819a1df4e63e1114682490a9b3c3b4e5c99cfa
ms.openlocfilehash: ddea7af935d5be880b96e383401061f8aa11e6da
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017

---
# <a name="manage-publications-in-updates-publisher"></a>Gestire le pubblicazioni in Updates Publisher

*Si applica a: System Center Updates Publisher*

È possibile usare le pubblicazioni per gestire gruppi di aggiornamenti e aggregazioni come un singolo oggetto. Sono incluse la pubblicazione degli aggiornamenti in un server di gestione e l'esportazione della pubblicazione come gruppo per l'uso con un'altra installazione di Updates Publisher.

## <a name="create-publications"></a>Creare le pubblicazioni
Le pubblicazioni vengono create in due modi:

-   Quando si gestiscono aggregazioni e aggiornamenti nell'**area di lavoro Aggiornamenti**, è possibile [assegnarli](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication) a una nuova pubblicazione creata sul momento.

-   Nell'**area di lavoro Pubblicazioni** è possibile usare il pulsante **Crea** nella scheda **Pubblicazione** della barra multifunzione. Questo metodo consente di creare una pubblicazione per un uso futuro. Successivamente, quando si assegnano gli aggiornamenti, è possibile usare questa pubblicazione.

## <a name="rename-a-publication"></a>Rinominare una pubblicazione
Per rinominare una pubblicazione, selezionarla nell'**area di lavoro Pubblicazioni**, quindi, nella scheda **Pubblicazione** della barra multifunzione, scegliere **Modifica**.

## <a name="change-the-publication-type-of-updates-in-a-publication"></a>Modificare il tipo di pubblicazione degli aggiornamenti in una pubblicazione
Nell'**area di lavoro Pubblicazioni** e possibile modificare il **tipo di pubblicazione** delle aggregazioni e degli aggiornamenti assegnati a una pubblicazione.

1. Selezionare la pubblicazione contenente gli aggiornamenti da modificare, quindi selezionare uno o più aggiornamenti o aggregazioni dall'elenco **All &lt;publication name> member updates** (Tutti gli aggiornamenti membri di <nome pubblicazione>).

2. Quindi, nella scheda **Home**, scegliere una delle opzioni seguenti. Le opzioni disponibili dipendono dal tipo di pubblicazione degli aggiornamenti selezionato.

  -   **Automatic** (Automatica)
  -   **Full Content** (Contenuto completo)
  -   **Metadata only** (Solo metadati)

Dopo aver apportato una modifica, potrebbe essere necessario aggiornare la visualizzazione della pubblicazione per esaminare i nuovi valori.

Per informazioni sui differenti tipi di pubblicazione, vedere [Assign updates to a publication](/sccm/sum/tools/manage-updates-with-updates-publisher#assign-updates-and-bundles-to-a-publication) (Assegnare aggiornamenti a una pubblicazione).

> [!TIP]    
> Quando si imposta il tipo di pubblicazione di un'aggregazione, tutti gli aggiornamenti software in essa contenuti vengono pubblicati con il tipo di pubblicazione dell'aggregazione stessa.

## <a name="remove-updates-from-a-publication"></a>Rimuovere gli aggiornamenti da una pubblicazione
Per rimuovere aggiornamenti o aggregazioni da una pubblicazione, nell'**area di lavoro Pubblicazioni** selezionare la pubblicazione da modificare, quindi selezionare gli aggiornamenti e le aggregazioni da rimuovere. Quindi, nella scheda **Home** della barra multifunzione, scegliere **Rimuovi**.

Dopo la rimozione da una pubblicazione, gli aggiornamenti rimangono disponibili nel repository di Updates Publisher.

## <a name="publish-publications"></a>Pubblicare pubblicazioni
Quando si pubblicano aggiornamenti e aggregazioni, Updates Publisher aggiunge informazioni sugli aggiornamenti e le aggregazioni (metadati) e, se possibile, i file binari degli aggiornamenti (contenuto completo) a un server di aggiornamento per la distribuzione ai dispositivi.

Per poter eseguire la pubblicazione, è prima necessario configurare l'opzione [Server di aggiornamento](/sccm/sum/tools/updates-publisher-options#update-server) per Updates Publisher. Per aprire questa opzione di configurazione, passare all'**area di lavoro Aggiornamenti** &gt; **Panoramica** e selezionare **Configure WSUS and Signing Certificate** (Configura WSUS e certificato di firma). È inoltre possibile passare alla pagina Server di aggiornamento nelle opzioni di Updates Publisher.

> [!NOTE]   
> Updates Publisher può pubblicare soltanto aggiornamenti di dimensioni pari o inferiori a 375 megabyte (MB).

### <a name="to-publish-a-publication"></a>Per pubblicare una pubblicazione

1.  Passare all'**area di lavoro Pubblicazioni** quindi selezionare una pubblicazione contenente il gruppo di aggiornamenti e aggregazioni che si vogliono pubblicare o esportare. Scegliere quindi **Pubblica** nella scheda **Home** della barra multifunzione.

2.  Nella pagina **Seleziona** della **Pubblicazione guidata** è possibile scegliere di firmare tutti gli aggiornamenti con un nuovo certificato di pubblicazione, ma non è possibile modificare il tipo di pubblicazione.

3.  Completare la procedura guidata.

  Se la pubblicazione ha esito negativo, viene visualizzato un collegamento al file UpdatesPublisher.log in cui sono disponibili maggiori informazioni.

## <a name="export-a-publication"></a>Esportare una pubblicazione
È possibile esportare una pubblicazione dal repository di Updates Publisher. Con questa operazione vengono esportati gli aggiornamenti e le aggregazioni assegnati alla pubblicazione e viene creato un catalogo di aggiornamenti. È quindi possibile [aggiungere](/sccm/sum/tools/updates-publisher-catalogs#add-software-update-catalogs) e [importare](/sccm/sum/tools/updates-publisher-catalogs#mport-updates) tale catalogo in un'altra istanza di Updates Publisher. È anche possibile [esportare aggiornamenti](/sccm/sum/tools/manage-updates-with-updates-publisher#export-updates) che non sono parte di una pubblicazione.

Per esportare una pubblicazione, passare all'**area di lavoro Pubblicazioni** e selezionare la pubblicazione contenente gli aggiornamenti che si vogliono esportare. È possibile selezionare una sola pubblicazione alla volta.

Dopo aver selezionato la pubblicazione, scegliere **Esporta** nella scheda **Home** della barra multifunzione e specificare un percorso e un nome file per l'esportazione del catalogo.

È anche possibile esportare (includere) aggiornamenti software dipendenti come parte dell'esportazione.

## <a name="rename-a-publication"></a>Rinominare una pubblicazione
Per rinominare una pubblicazione, selezionarla nell'**area di lavoro Pubblicazioni**, quindi scegliere **Modifica** dalla scheda **Pubblicazione** della barra multifunzione.

## <a name="delete-a-publication"></a>Eliminare una pubblicazione
Per eliminare una pubblicazione, selezionarla nell'**area di lavoro Pubblicazioni**, quindi scegliere **Elimina** dalla scheda **Pubblicazione** della barra multifunzione.

Dopo la rimozione della pubblicazione da Updates Publisher, gli aggiornamenti che erano contenuti nella pubblicazione rimangono disponibili nel repository di Updates Publisher.

## <a name="expire-or-reactivate-updates-and-bundles"></a>Impostare come scaduti o riattivare aggiornamenti e aggregazioni
È possibile usare l'**area di lavoro Aggiornamenti** per selezionare e quindi impostare come scaduti oppure riattivare aggiornamenti e aggregazioni. È possibile impostare come scaduti e quindi riattivare aggiornamenti e aggregazioni il numero di volte desiderato.

-   **Per impostare come scaduti aggiornamenti o aggregazioni**, nell'area di lavoro Aggiornamenti selezionare uno o più aggiornamenti o aggregazioni non scaduti, quindi scegliere **Expire** (Imposta come scaduto) dalla scheda **Home**. Le aggregazioni o gli aggiornamenti pubblicati come scaduti in Configuration Manager possono essere riattivati.

    Prima di rimuovere (eliminare) da Configuration Manager un'aggregazione o un aggiornamento personalizzato, è necessario impostarlo come scaduto e quindi pubblicare lo stato Scaduto in Configuration Manager. Dopo che le aggregazioni o gli aggiornamenti sono scaduti in Configuration Manager, non è più possibile distribuirli o riattivarli.

-   **Per riattivare aggiornamenti o aggregazioni**, nell'area di lavoro Aggiornamenti selezionare uno o più aggiornamenti scaduti, quindi scegliere **Reactivate** (Riattiva) dalla scheda **Home** della barra multifunzione. Se l'aggiornamento scaduto era stato precedentemente pubblicato come scaduto in Configuration Manager, non è possibile riattivarlo.

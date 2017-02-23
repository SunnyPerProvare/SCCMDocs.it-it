---
title: Visualizzare l&quot;inventario software | Microsoft Docs | Resource Explorer
description: Usare Esplora inventario software per visualizzare l&quot;inventario software in System Center Configuration Manager.
ms.custom: na
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
caps.latest.revision: 5
caps.handback.revision: 0
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 9206b82eca02877c30eebf146d42bcca7290eb42
ms.openlocfilehash: 6189726bbcade8229e0b2e929ebedeefdbf266a4


---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-system-center-configuration-manager"></a>Come usare Esplora inventario software per visualizzare l'inventario software in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile usare Esplora inventario risorse in System Center Configuration Manager per visualizzare informazioni relative all'inventario software raccolto dai computer nella gerarchia.  

> [!NOTE]  
>  Esplora inventario risorse non visualizzerà dati di inventario fino al completamento dell'esecuzione di un ciclo di inventario software nel client.  

 Esplora inventario risorse fornisce le informazioni di inventario software seguenti:  

-   **Software**:  

    -   **File raccolti**: file raccolti durante l'inventario software.  

    -   **Dettagli file**: file di cui è stato eseguito l'inventario durante l'inventario software, che non sono associati a uno specifico prodotto o il produttore.  

    -   **Ultima analisi software**: data e ora dell'ultimo inventario software e dell'ultima raccolta dei file per il computer client.  

    -   **Dettagli prodotto**: prodotti software inclusi nell'inventario software, raggruppati in base al produttore.  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Per eseguire Esplora inventario risorse dalla console di Configuration Manager  

1.  Nella console di Configuration Manager scegliere **Asset e conformità**.

2.  Nell'area di lavoro **Asset e conformità** scegliere **Dispositivi** oppure aprire eventuali raccolte che visualizzano dispositivi.  

3.  Scegliere il computer che contiene l'inventario da visualizzare e quindi nel gruppo **Dispositivi** della scheda **Home** scegliere **Avvia** > **Esplora inventario risorse**.

4.  È possibile fare clic con il pulsante destro del mouse su qualsiasi elemento nel riquadro di destra della finestra Esplora inventario risorse e quindi scegliere **Proprietà** per visualizzare le informazioni di inventario raccolte in un formato più leggibile.  
 



<!--HONumber=Dec16_HO5-->



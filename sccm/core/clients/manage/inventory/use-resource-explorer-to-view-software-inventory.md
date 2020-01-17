---
title: Visualizzare l'inventario software con Esplora inventario risorse
titleSuffix: Configuration Manager
description: Usare Esplora risorse per visualizzare l'inventario software in Configuration Manager.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 4b7aa5f6-5ebd-49be-b7f3-4206caadc187
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 794d52440f1fcf441af74e42be9c5dff34f37016
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75824198"
---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-configuration-manager"></a>Come usare Esplora risorse per visualizzare l'inventario software in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

È possibile usare Esplora inventario risorse in Configuration Manager per visualizzare informazioni relative all'inventario software raccolto dai computer nella gerarchia.  

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
 

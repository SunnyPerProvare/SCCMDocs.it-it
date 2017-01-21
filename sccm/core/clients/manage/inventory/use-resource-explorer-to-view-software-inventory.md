---
title: Visualizzare l&quot;inventario software | Microsoft Docs | Resource Explorer
description: Usare Esplora inventario software per visualizzare l&quot;inventario software in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
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
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: a15c593bed4fe7ecce22990bbdcecc8dc2ed2962


---
# <a name="how-to-use-resource-explorer-to-view-software-inventory-in-system-center-configuration-manager"></a>Come usare Esplora inventario software per visualizzare l'inventario software in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile usare Esplora inventario risorse in System Center Configuration Manager per visualizzare informazioni relative all'inventario software raccolto dai computer nella gerarchia.  

> [!NOTE]  
>  Esplora inventario risorse non visualizzerà dati di inventario fino al completamento dell'esecuzione di un ciclo di inventario software nel client a cui si è connessi.  

 Esplora inventario risorse in Configuration Manager contiene le sezioni seguenti correlate all'inventario software:  

-   **Software**: questa sezione di Esplora inventario risorse contiene quattro sezioni:  

    -   **File raccolti**: visualizza informazioni sui file raccolti durante l'inventario software.  

    -   **Dettagli file**: visualizza informazioni sui file di cui è stato eseguito l'inventario durante l'inventario software, che non sono associati a uno specifico prodotto o il produttore.  

    -   **Ultima analisi software**: visualizza data e ora dell'ultimo inventario software e dell'ultima raccolta dei file eseguiti nel computer client.  

    -   **Dettagli prodotto**: visualizza informazioni sui prodotti software inclusi nell'inventario software, raggruppati in base al produttore.  

## <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Per eseguire Esplora inventario risorse dalla console di Configuration Manager  
 Usare la procedura seguente per eseguire Esplora inventario risorse in Configuration Manager.  

#### <a name="to-run-resource-explorer-from-the-configuration-manager-console"></a>Per eseguire Esplora inventario risorse dalla console di Configuration Manager  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Dispositivi** oppure aprire eventuali raccolte che visualizzano dispositivi.  

3.  Fare clic sul computer che contiene l'inventario da visualizzare e quindi nel gruppo **Dispositivi** della scheda **Home** fare clic su **Avvia** e quindi su **Esplora inventario risorse**. Verrà visualizzata la finestra **Esplora inventario risorse** .  

4.  È possibile fare clic con il pulsante destro del mouse su qualsiasi elemento nel riquadro di destra della finestra Esplora inventario risorse e quindi scegliere **Proprietà** per aprire la finestra di dialogo *Proprietà\>***nome elemento** che consente di visualizzare le informazioni di inventario raccolte in un formato più leggibile.  

5.  Al termine, chiudere la finestra **Esplora inventario risorse** .  



<!--HONumber=Dec16_HO3-->



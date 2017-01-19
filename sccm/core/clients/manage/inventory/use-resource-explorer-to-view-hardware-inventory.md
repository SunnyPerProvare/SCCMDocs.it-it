---
title: Visualizzare l&quot;inventario hardware | Microsoft Docs | Resource Explorer
description: Usare Esplora inventario risorse per visualizzare l&quot;inventario hardware in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
caps.latest.revision: 7
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: 2cd138b3bbb437d84f0ff7c2aeef869518bd817d


---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-system-center-configuration-manager"></a>Come usare Esplora inventario risorse per visualizzare l'inventario hardware in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile usare Esplora inventario risorse in System Center Configuration Manager per visualizzare informazioni relative all'inventario hardware raccolto dai client nella gerarchia.  

> [!NOTE]  
>  Esplora inventario risorse non visualizzerà alcun inventario dati fino a quando non è eseguito un ciclo di inventario hardware nel client si connette a.  

 Esplora inventario risorse in Configuration Manager contiene le sezioni seguenti correlate all'inventario hardware:  

-   **Hardware**: contiene l'inventario hardware più recente raccolto dal dispositivo client di Configuration Manager specificato. È possibile esaminare l'articolo di magazzino **stato Workstation** per rilevare quando il dispositivo ha eseguito un inventario hardware di data e ora.  

-   **Cronologia hardware**: contiene una cronologia degli elementi inclusi nell'inventario che sono stati modificati dall'ultima esecuzione dell'inventario hardware. Ogni elemento nell'elenco contiene un nodo **Corrente** e uno o più nodi *<data\>*. È possibile confrontare le informazioni nel nodo corrente a uno dei nodi cronologici per individuare gli elementi modificati nell'inventario hardware di computer client.  

    > [!NOTE]  
    >  Configuration Manager mantiene una cronologia dell'inventario hardware per il numero di giorni specificato nell'attività di manutenzione del sito **Elimina cronologia inventario obsoleta**  

> [!NOTE]  
>  Per informazioni su come visualizzare l'inventario hardware dai client che eseguono Linux e UNIX, vedere [How to monitor clients for Linux and UNIX servers in System Center Configuration Manager](../../../../core/clients/manage/monitor-clients-for-linux-and-unix-servers.md)  

### <a name="how-to-run-resource-explorer-from-the-configuration-manager-console"></a>Come eseguire Esplora inventario risorse dalla console di Configuration Manager  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Dispositivi** oppure aprire eventuali raccolte che visualizzano dispositivi.  

3.  Fare clic sul computer che contiene l'inventario da visualizzare e quindi nel gruppo **Dispositivi** della scheda **Home** fare clic su **Avvia** e quindi su **Esplora inventario risorse**. Il **Esplora inventario risorse** aprirà la finestra.  

4.  È possibile fare clic con il pulsante destro del mouse su qualsiasi elemento nel riquadro di destra della finestra **Esplora inventario risorse** e quindi scegliere **Proprietà** per aprire la finestra di dialogo *<Nome elemento\>***Proprietà** che consente di visualizzare le informazioni di inventario raccolte in un formato più leggibile.  

5.  Al termine, chiudere la finestra **Esplora inventario risorse** .  



<!--HONumber=Dec16_HO3-->



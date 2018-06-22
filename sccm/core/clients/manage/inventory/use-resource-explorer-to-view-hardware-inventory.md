---
title: Visualizzare l'inventario hardware con Esplora inventario risorse
titleSuffix: Configuration Manager
description: Usare Esplora inventario risorse per visualizzare l'inventario hardware in System Center Configuration Manager.
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 375912f5-436d-4315-bdbe-d77afee6c9f3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: be2c8c3dbfef5ea0f35e338b14439c65150310be
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32332210"
---
# <a name="how-to-use-resource-explorer-to-view-hardware-inventory-in-system-center-configuration-manager"></a>Come usare Esplora inventario risorse per visualizzare l'inventario hardware in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile usare Esplora inventario risorse in System Center Configuration Manager per visualizzare informazioni relative all'inventario hardware raccolto dai client nella gerarchia.  

> [!NOTE]  
>  Esplora inventario risorse non visualizzerà alcun inventario dati fino a quando non è eseguito un ciclo di inventario hardware nel client si connette a.  

 Esplora inventario risorse contiene le sezioni seguenti relative all'inventario hardware:  

-   **Hardware**: contiene l'inventario hardware più recente raccolto dal dispositivo client specificato.  **Stato workstation**: indica la data e ora dell'ultima esecuzione di un inventario hardware del dispositivo.  

-   **Cronologia hardware**: contiene una cronologia degli elementi inclusi nell'inventario che sono stati modificati dall'ultima esecuzione dell'inventario hardware. Ogni elemento contiene un nodo **Corrente** e uno o più nodi *<data\>*. È possibile confrontare le informazioni nel nodo corrente con uno dei nodi cronologici per individuare gli elementi modificati.  

    > [!NOTE]  
    >  Configuration Manager mantiene una cronologia dell'inventario hardware per il numero di giorni specificato nell'attività di manutenzione del sito **Elimina cronologia inventario obsoleta**  

> [!NOTE]  
>  Per informazioni su come visualizzare l'inventario hardware dai client che eseguono Linux e UNIX, vedere [Come monitorare i client per i server Linux e UNIX in System Center Configuration Manager](../../../../core/clients/manage/monitor-clients-for-linux-and-unix-servers.md).  

### <a name="how-to-run-resource-explorer-from-the-configuration-manager-console"></a>Come eseguire Esplora inventario risorse dalla console di Configuration Manager  

1.  Nella console di Configuration Manager scegliere **Asset e conformità** > **Dispositivi** oppure aprire qualsiasi raccolta che visualizza dispositivi.  

3.  Scegliere il computer che contiene l'inventario da visualizzare e quindi nel gruppo **Dispositivi** della scheda **Home** scegliere **Avvia** >  **Esplora inventario risorse**.   

4.  Fare clic con il pulsante destro del mouse su qualsiasi elemento nel riquadro di destra della finestra **Esplora inventario risorse** e quindi scegliere **Proprietà** per aprire la finestra di dialogo *<Nome elemento\>***Proprietà** che consente di visualizzare le informazioni di inventario raccolte in un formato più leggibile.  


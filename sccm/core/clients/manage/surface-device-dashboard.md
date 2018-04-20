---
title: Dashboard dei dispositivi Surface
titleSuffix: System Center Configuration Manager
description: Esaminare le informazioni relative ai dispositivi Surface tramite il dashboard.
keywords: ''
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/22/2018
ms.topic: article
ms.prod: configuration-manager
ms.service: ''
ms.technology:
- configmgr-other
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: 8c9171ed5b239091b7f77b534368422575c0f2f4
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2018
---
# <a name="surface-device-dashboard-in-system-center-configuration-manager"></a>Dashboard dei dispositivi Surface in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

A partire dalla versione 1802, il dashboard dei dispositivi Surface visualizza informazioni a colpo d'occhio sui dispositivi Surface rilevati nell'ambiente in uso. <!--1355788-->

## <a name="open-the-surface-device-dashboard"></a>Aprire il dashboard dei dispositivi Surface

Per aprire il dashboard dei dispositivi Surface, procedere come segue: 

1. Aprire la console di Configuration Manager. 
2. Fare clic sul nodo **Monitoraggio**. 
3. Per caricare il dashboard, fare clic su **Dispositivi Surface**.

**Dashboard dei dispositivi Surface**
![Dashboard dei dispositivi Surface](media\Surface-device-dashboard.PNG)



## <a name="reviewing-information-in-the-surface-device-dashboard"></a>Esaminare le informazioni nel dashboard dei dispositivi Surface

Il dashboard dei dispositivi Surface visualizza tre grafici per l'ambiente in uso. 

- **Percentuale di dispositivi Surface**: visualizza la percentuale di dispositivi Surface presenti in tutto l'ambiente.

    ![Grafico Percentuale di dispositivi Surface](media\Percent-Surface-Devices.PNG)
- **Modelli di dispositivi Surface**: visualizza il numero di dispositivi per modello di Surface. 
    - Se si passa il mouse su una sezione del grafico, viene visualizzata la percentuale dei dispositivi Surface del modello selezionato. 

         ![Grafico dei modelli di dispositivi Surface](media\Surface-Models-Hover.PNG)
    - Se si fa clic su una sezione del grafico si passa all'elenco dei dispositivi per il modello corrispondente. 
        ![Elenco dei dispositivi per un modello di dispositivo Surface](media\Surface-Model-Device-List.PNG)

- **Prime cinque versioni di firmware**: visualizza un grafico con i primi cinque modelli di firmware nell'ambiente in uso. 
    - Se si passa il mouse su una sezione del grafico, viene visualizzato il numero dei dispositivi Surface con la versione del firmware selezionata. 
       ![Elenco dei dispositivi per un modello di dispositivo Surface](media\Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>Altre informazioni

Per altre informazioni sui dispositivi Surface, vedere:
 - Il sito Web [Surface]( https://go.microsoft.com/fwlink/?linkid=861998).
    
Per altre informazioni sulla distribuzione degli aggiornamenti del firmware di Surface in Configuration Manager, vedere:
 - [Come gestire gli aggiornamenti dei driver di Surface in Configuration Manager]( https://support.microsoft.com/help/4098906).





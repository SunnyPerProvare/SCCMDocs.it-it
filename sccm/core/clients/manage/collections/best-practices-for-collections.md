---
title: Procedure consigliate per le raccolte | System Center Configuration Manager
description: Apprendere le procedure consigliate per le raccolte in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a2abb79-9ae5-4a25-9e18-5dcf528de3bf
caps.latest.revision: 4
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 8e22f353ba0803a3b1b4d387a8c00fdb98186bf5


---
# <a name="best-practices-for-collections-in-system-center-configuration-manager"></a>Procedure consigliate per le raccolte in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Per le raccolte in System Center Configuration Manager usare le seguenti procedure consigliate.  

## <a name="do-not-use-incremental-updates-for-a-large-number-of-collections"></a>Non usare gli aggiornamenti incrementali per un numero elevato di raccolte  
 Quando si abilita l'opzione **Utilizza aggiornamenti incrementali per questa raccolta** , questa configurazione potrebbe provocare ritardi di valutazione se l'opzione viene abilitata per più raccolte. La soglia è pari a circa 200 raccolte nella gerarchia. Il numero esatto dipende dai fattori seguenti:  

-   Il numero totale di raccolte  

-   La frequenza di aggiunta e modifica delle nuove risorse nella gerarchia  

-   Il numero di client nella gerarchia  

-   La complessità delle regole di appartenenza alla raccolta nella gerarchia  

## <a name="make-sure-that-maintenance-windows-are-large-enough-to-deploy-critical-software-updates"></a>Assicurarsi che le dimensioni delle finestre di manutenzione siano sufficienti per la distribuzione degli aggiornamenti software critici  
 È possibile configurare le finestre di manutenzione per le raccolte di dispositivi al fine di limitare il numero di possibili installazioni del software da parte di Configuration Manager su questi dispositivi. Se si configurano dimensioni insufficienti della finestra di manutenzione, il client potrebbe non essere in grado di installare aggiornamenti software critici, rendendo il client vulnerabile ad attacchi altrimenti limitati dall'aggiornamento software.  



<!--HONumber=Nov16_HO1-->


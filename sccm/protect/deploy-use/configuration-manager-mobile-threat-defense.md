---
title: Mobile Threat Defense | System Center Configuration Manager
description: Limitare l&quot;accesso alle risorse aziendali in base ai rischi per dispositivi, rete e applicazioni tramite Configuration Manager e i partner di Intune Mobile Threat Defense
ms.custom: na
ms.date: 03/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c0e6824-2dfe-4700-b817-d5631e0eb872
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 266897b7ac674a369931e8ed63ff464edc10c9d8
ms.openlocfilehash: 298d879638a2d20d421b19752cb5f20f6725df14
ms.lasthandoff: 03/03/2017


---
# <a name="intune-mobile-threat-defense-connectors-in-configuration-manager"></a>Connettori di Intune Mobile Threat Defense in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La [distribuzione MDM ibrida (SCCM con Intune) ](https://docs.microsoft.com/en-us/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) e l'integrazione tra Intune e i partner di Mobile Threat Defense consentono di controllare l'accesso alle risorse e ai dati aziendali in base alla valutazione dei rischi per i dispositivi.

Grazie ai connettori di Intune Mobile Threat Defense è possibile usare il fornitore di Mobile Threat Defense selezionato come fonte di informazioni per i criteri di conformità e per le regole di accesso condizionale. Ciò consente agli amministratori IT di aggiungere un livello di protezione alle risorse aziendali, come Exchange e SharePoint, in particolare dai dispositivi mobili compromessi.

## <a name="what-problem-does-this-solve"></a>Qual è il problema risolto?

Le aziende devono proteggere i dati sensibili dalle minacce emergenti, incluse le minacce fisiche, basate su app e basate sulla rete, nonché le vulnerabilità del sistema operativo.
In genere le aziende compiono sforzi attivi per proteggere i PC dagli attacchi esterni, mentre i dispositivi mobili continuano a non essere monitorati e protetti. Le piattaforme mobili hanno protezioni incorporate, come l'isolamento delle app e il controllo degli app store consumer, ma continuano a essere vulnerabili agli attacchi sofisticati. Attualmente, sempre più dipendenti usano i dispositivi per lavoro e hanno bisogno di accedere a informazioni sensibili. I dispositivi devono essere protetti da attacchi sempre più sofisticati.

## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>Come funzionano i connettori di Intune Mobile Threat Defense?

Il connettore protegge le risorse aziendali creando un canale di comunicazione tra Intune e il fornitore di Mobile Threat Defense selezionato. I partner di Intune Mobile Threat Defense offrono applicazioni per dispositivi mobili intuitive e facili da distribuire che analizzano attivamente le informazioni relative alle minacce da condividere con Intune, ai fini della creazione di report o dell'imposizione di regole. Se ad esempio un'app di Mobile Threat Defense connessa segnala al fornitore di Mobile Threat Defense che un telefono nella rete è connesso a una rete vulnerabile ad attacchi man-in-the-middle, queste informazioni vengono condivise e categorizzate in base a un livello di rischio appropriato (basso/medio/alto). Questo livello può quindi essere confrontato con i requisiti del livello di rischio configurati in Intune per determinare se è necessario revocare l'accesso a determinate risorse mentre il dispositivo risulta compromesso.

## <a name="sample-scenarios"></a>Scenari di esempio

Quando un dispositivo è considerato infetto dalla soluzione Mobile Threat Defense:

![](http://i.imgur.com/Li1WUOU.png)

L'accesso è consentito dopo l'intervento di correzione:

![](http://i.imgur.com/VCIwpdz.png)

## <a name="mobile-threat-defense-partners"></a>Partner di Mobile Threat Defense

Informazioni su come proteggere l'accesso alle risorse aziendali in base ai rischi per dispositivi, rete e applicazioni tramite:

- [Lookout](https://docs.microsoft.com/sccm/protect/deploy-use/lookout-mobile-threat-defense-in-configuration-manager)
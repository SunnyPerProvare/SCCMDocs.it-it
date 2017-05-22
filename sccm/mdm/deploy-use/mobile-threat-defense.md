---
title: Limitare l&quot;accesso in base ai rischi | Microsoft Docs
description: Limitare l&quot;accesso alle risorse aziendali in base ai rischi per dispositivi, rete e applicazioni.
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: c6a6137fa978e1ea28aefea2aea4e29ba661efd6
ms.openlocfilehash: 250671660c1c6da0ca9b593b06b8f344dfe17ad6
ms.contentlocale: it-it
ms.lasthandoff: 05/04/2017


---

# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Gestire l'accesso alle risorse aziendali in base ai rischi per dispositivi, rete e applicazioni

*Si applica a: System Center Configuration Manager (Current Branch)*

Grazie ai connettori di Mobile Threat Defense è possibile usare il fornitore di Mobile Threat Defense prescelto come fonte di informazioni per i criteri di conformità e per le regole di accesso condizionale. Ciò consente agli amministratori IT di aggiungere un livello di protezione alle risorse aziendali, come Exchange e SharePoint, in particolare dai dispositivi mobili compromessi.

## <a name="what-problem-does-this-solve"></a>Qual è il problema risolto?

Le aziende devono proteggere i dati sensibili dalle minacce emergenti, incluse le minacce fisiche, basate su app e basate sulla rete, nonché le vulnerabilità del sistema operativo.
In genere le aziende compiono sforzi attivi per proteggere i PC dagli attacchi esterni, mentre i dispositivi mobili continuano a non essere monitorati e protetti. Le piattaforme mobili hanno protezioni incorporate, come l'isolamento delle app e il controllo degli app store consumer, ma continuano a essere vulnerabili agli attacchi sofisticati. Attualmente, sempre più dipendenti usano i dispositivi per lavoro e hanno bisogno di accedere a informazioni sensibili. I dispositivi devono essere protetti da attacchi sempre più sofisticati.

La [distribuzione MDM ibrida (SCCM con Intune)](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) consente di controllare l'accesso alle risorse e ai dati aziendali in base alla valutazione dei rischi offerta da soluzioni di protezione dalle minacce per i dispositivi come quelle offerte dai partner Mobile Threat Defense.

## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>Come funzionano i connettori di Intune Mobile Threat Defense?

Il connettore protegge le risorse aziendali creando un canale di comunicazione tra Intune e il fornitore di Mobile Threat Defense selezionato. I partner di Intune Mobile Threat Defense offrono applicazioni per dispositivi mobili intuitive e facili da distribuire che analizzano attivamente le informazioni relative alle minacce da condividere con Intune, ai fini della creazione di report o dell'imposizione di regole. Se ad esempio un'app di Mobile Threat Defense connessa segnala al fornitore di Mobile Threat Defense che un telefono nella rete è connesso a una rete vulnerabile ad attacchi man-in-the-middle, queste informazioni vengono condivise e categorizzate in base a un livello di rischio appropriato (basso/medio/alto). Questo livello può quindi essere confrontato con i requisiti del livello di rischio configurati in Intune per determinare se è necessario revocare l'accesso a determinate risorse mentre il dispositivo risulta compromesso.

## <a name="sample-scenarios"></a>Scenari di esempio

Quando un dispositivo è considerato infetto dalla soluzione Mobile Threat Defense:

![Dispositivo infetto di Mobile Threat Defense](../media/mtp/MTD-image-1.png)

L'accesso è consentito dopo l'intervento di correzione:

![Accesso consentito da Mobile Threat Defense](../media/mtp/MTD-image-2.png)

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come proteggere l'accesso alle risorse aziendali in base ai rischi per dispositivi, rete e applicazioni tramite:

- [Lookout](https://docs.microsoft.com/intune/deploy-use/lookout-mobile-threat-defense-connector)

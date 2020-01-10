---
title: Limitare l'accesso in base ai rischi
titleSuffix: Configuration Manager
description: Limitare l'accesso alle risorse aziendali in base al rischio per dispositivi, rete e applicazioni.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 61dbf9f7835a8ca88ae5bf3bbdfb87011d8b8c0a
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75826748"
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Gestire l'accesso alle risorse aziendali in base ai rischi per dispositivi, rete e applicazioni

*Si applica a: Configuration Manager (Current Branch)*

Grazie ai connettori di Mobile Threat Defense è possibile usare il fornitore di Mobile Threat Defense prescelto come fonte di informazioni per i criteri di conformità e per le regole di accesso condizionale. Ciò consente di aggiungere un livello di protezione alle risorse aziendali, come Exchange e SharePoint, in particolare dai dispositivi mobili compromessi.

> [!Important]  
> A partire dal 14 agosto 2018, la gestione ibrida dei dispositivi mobili è una [funzionalità deprecata](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Per altre informazioni, vedere [Informazioni sulla gestione di dispositivi mobili ibrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## <a name="what-problem-does-this-solve"></a>Qual è il problema risolto?

Le organizzazioni necessitano di proteggere i dati riservati dalle minacce emergenti, incluse minacce fisiche, basate su app e basate sulla rete, nonché le vulnerabilità del sistema operativo.

In genere le organizzazioni compiono sforzi attivi per proteggere i PC dagli attacchi esterni, mentre i dispositivi mobili continuano a non essere monitorati e protetti. Le piattaforme mobili hanno protezioni incorporate, come l'isolamento delle app e il controllo degli app store consumer, ma continuano a essere vulnerabili agli attacchi sofisticati. Attualmente, sempre più dipendenti usano i dispositivi per lavoro e hanno bisogno di accedere a informazioni sensibili. I dispositivi devono essere protetti da attacchi sempre più sofisticati.



## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>Come funzionano i connettori di Intune Mobile Threat Defense?

Il connettore protegge le risorse aziendali creando un canale di comunicazione tra Intune e il fornitore di Mobile Threat Defense selezionato. I partner di Intune Mobile Threat Defense offrono applicazioni per dispositivi mobili intuitive e facili da distribuire che analizzano attivamente le informazioni relative alle minacce da condividere con Intune. Usare queste informazioni per la creazione di report o l'imposizione di regole. 

Un'app Mobile Threat Defense connessa, ad esempio, segnala al fornitore di Mobile Threat Defense che un dispositivo è attualmente connesso a una rete vulnerabile ad attacchi man-in-the-middle. Queste informazioni vengono condivise e classificate in un livello di rischio appropriato: basso, medio o elevato. Confrontare questo rischio con i limiti del livello di rischio configurati in Intune per determinare se l'accesso a specifiche risorse selezionate debba essere revocato mentre il dispositivo è compromesso.



## <a name="sample-scenarios"></a>Scenari di esempio

Quando un dispositivo è considerato infetto da una soluzione Mobile Threat Defense:

![Mobile Threat Defense - Dispositivo infetto](../media/mtp/MTD-image-1.png)

L'accesso è consentito dopo l'intervento di correzione:

![Accesso consentito da Mobile Threat Defense](../media/mtp/MTD-image-2.png)



## <a name="next-steps"></a>Passaggi successivi

Informazioni sulla protezione dell'accesso alle risorse aziendali in base al rischio di dispositivi, reti e applicazioni con:

- [Lookout](https://docs.microsoft.com/intune/deploy-use/lookout-mobile-threat-defense-connector)

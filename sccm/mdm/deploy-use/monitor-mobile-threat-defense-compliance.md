---
title: "Monitorare la conformità a Mobile Threat Defense | System Center Configuration Manager"
description: "Monitorare lo stato di conformità al partner Mobile Threat Defense dalla console di Configuration Manager"
ms.custom: na
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 408190da-bea6-4122-9dd6-f90155040e88
caps.latest.revision: 
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 8edf83a0f761dfc16274ce49c3aa2b878c7fe6cd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="monitor-mobile-threat-defense-compliance"></a>**Monitorare la conformità a Mobile Threat Defense**

*Si applica a: System Center Configuration Manager (Current Branch)*

## <a name="to-monitor-the-overall-compliance-status"></a>Per monitorare lo stato di conformità complessivo

Per monitorare lo stato di Mobile Threat Defense:

1.  Nella console di Configuration Manager fare clic sull'area di lavoro **Monitoraggio**.

2.  Nell'area di lavoro **Monitoraggio** fare clic sul nodo **Sicurezza**.

È possibile visualizzare un riepilogo dello stato di conformità con diversi livelli di minaccia, organizzato sotto forma di grafico. È possibile fare clic sulle diverse sezioni del grafico per visualizzare informazioni aggiuntive, ad esempio: 

- Numero di dispositivi indicati come non conformi dalla piattaforma
- Eventuali errori correlati allo stato di conformità dei dispositivi

![](http://i.imgur.com/bmPsiWk.png)

## <a name="to-monitor-the-individual-compliance-status"></a>Per monitorare lo stato di conformità dei singoli dispositivi

È anche possibile visualizzare lo stato dei singoli dispositivi:

1.  Nella console di Configuration Manager fare clic sull'area di lavoro **Asset e conformità**.

2.  Fare clic su **Dispositivi**.

> [!TIP] 
> Per visualizzare lo stato, è possibile aggiungere le colonne **Protezione dalle minacce per il dispositivo** e **Livello di minaccia del dispositivo**. Queste colonne non vengono visualizzate per impostazione predefinita.

## <a name="device-threat-protection-tab"></a>Scheda Protezione dalle minacce per il dispositivo

Nella schermata **Dispositivi** è inoltre possibile selezionare dispositivi specifici e quindi fare clic sulla scheda **Protezione dalle minacce per il dispositivo**, in cui sono riportati altri dettagli sullo stato di conformità dei dispositivi. Di seguito sono riportate le descrizioni delle colonne e i relativi valori previsti, in modo da facilitare l'analisi dello stato di conformità del dispositivo.

> [!IMPORTANT] 
> Abilitare una regola di protezione dalle minacce nei criteri di conformità del dispositivo.

|Nome della colonna|Visibile per impostazione predefinita|Descrizione| 
|-|-|-|
|**Descrizione**| Sì | Dettagli sulla minaccia forniti dal partner Mobile Threat Defense. |
|**Ora ultimo aggiornamento**| Sì | Ora dell'ultimo invio da parte del partner Mobile Threat Defense di dettagli aggiornati sulla minaccia a Intune. |
|**Gravità minaccia**| Sì | "Gravità minaccia" è la definizione di una singola minaccia in base alla configurazione dell'amministratore nella console del partner Mobile Threat Defense. I valori possibili sono: **Bassa**, **Media** o **Alta** |
|**Stato minacce**| Sì | Stato corrente della minaccia nel dispositivo. Gli stati possibili sono: **Attivo**, **Risolto** o **Ignorato**. Quest'ultimo stato indica che l'utente ha ignorato la minaccia sul dispositivo, ma che questa è ancora presente. |
|**Tipo di minaccia**| Sì | Tipo di minaccia del partner Mobile Threat Defense. I valori possibili sono i seguenti: **App**, **File** o **Sistema operativo** |
|**ID account AAD**| No | Identificatore univoco di Azure Active Directory. |
|**Classificazione**| Sì | Classificazione della minaccia fornita dal partner Mobile Threat Defense. I valori possibili sono: **Root Enabler, Riskware, Adware, Chargeware, DataLeak, Trojan, Worm, Virus, Exploit, Backdoor, Bot, AppDropper, ClickFraud, Spam, Spyware, SurveillanceWare, Vulnerability, Unknown, Root Jailbrake, Connectivity, TollFraud, SideloadedApp** |
|**ID dispositivo**| No | ID dell'oggetto Azure Active Directory che rappresenta il dispositivo aggiunto all'area di lavoro con informazioni sulle minacce. |
|**ID minaccia**| No | Identificatore univoco della minaccia generato dal partner Mobile Threat Defense. L'ID minaccia viene usato per tenere traccia della risoluzione. |
|**URL della minaccia**| No | Quando presente, l'URL della minaccia fornisce un collegamento alla vista della console di gestione del partner Mobile Threat Defense per la minaccia specifica. |

> [!TIP] 
> Verificare di abilitare le colonne che non sono **visibili per impostazione predefinita** per visualizzare maggiori dettagli sullo stato di conformità a Mobile Threat Defense dei dispositivi.

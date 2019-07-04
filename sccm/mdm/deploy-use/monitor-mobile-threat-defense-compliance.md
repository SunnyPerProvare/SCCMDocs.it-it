---
title: Monitorare la conformità a Mobile Threat Defense
titleSuffix: Configuration Manager
description: Monitorare lo stato di conformità al partner Mobile Threat Defense dalla console di Configuration Manager
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 408190da-bea6-4122-9dd6-f90155040e88
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9b77fabc6ea4f5823777e932011313c5e2de1acf
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/03/2019
ms.locfileid: "67551331"
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

![Dashboard di Device Threat Protection](device-threat-protection-dashboard.png)

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
|**Descrizione**| Yes | Dettagli sulla minaccia forniti dal partner Mobile Threat Defense. |
|**Ora ultimo aggiornamento**| Yes | Ora dell'ultimo invio da parte del partner Mobile Threat Defense di dettagli aggiornati sulla minaccia a Intune. |
|**Gravità minaccia**| Yes | "Gravità minaccia" è la definizione di una singola minaccia in base alla configurazione dell'amministratore nella console del partner Mobile Threat Defense. Dispone di uno dei tre valori: **Low**, **Medium** o **elevata** |
|**Stato minacce**| Yes | Stato corrente della minaccia nel dispositivo. Stati possibili: **Active**, **risolto** o **ignorati:** Indica che l'utente ha ignorato la minaccia sul dispositivo, ma è ancora presente la minaccia. |
|**Tipo di minaccia**| Yes | Tipo di minaccia del partner Mobile Threat Defense. Valori possibili: **App**, **File** o **OS** |
|**ID account AAD**| No | Identificatore univoco di Azure Active Directory. |
|**Classificazione**| Yes | Classificazione della minaccia fornita dal partner Mobile Threat Defense. Valori possibili: **Abilitatore radice, Riskware, Adware, Chargeware, DataLeak, Trojan, Worm, Virus, Exploit, Backdoor, Bot, AppDropper, ClickFraud, Spam, Spyware, surveillance-ware, vulnerabilità, Unknown, Root Jailbrake, Connectivity, TollFraud, SideloadedApp** |
|**ID dispositivo**| No | ID dell'oggetto Azure Active Directory che rappresenta il dispositivo aggiunto all'area di lavoro con informazioni sulle minacce. |
|**ID minaccia**| No | Identificatore univoco della minaccia generato dal partner Mobile Threat Defense. L'ID minaccia viene usato per tenere traccia della risoluzione. |
|**URL della minaccia**| No | Quando presente, l'URL della minaccia fornisce un collegamento alla vista della console di gestione del partner Mobile Threat Defense per la minaccia specifica. |

> [!TIP] 
> Verificare di abilitare le colonne che non sono **visibili per impostazione predefinita** per visualizzare maggiori dettagli sullo stato di conformità a Mobile Threat Defense dei dispositivi.

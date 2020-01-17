---
title: Guida di riferimento tecnico per la risoluzione dei problemi di distribuzione delle applicazioni
titleSuffix: Configuration Manager
description: Riferimento tecnico per la risoluzione dei problemi di distribuzione delle applicazioni in Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a4eb09c8-e570-4369-9adb-ded9c8ad3400
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d8e996adffadc87e74e88bef684ed97a9371146a
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75782065"
---
# <a name="technical-reference-for-application-deployment-in-configuration-manager"></a>Riferimento tecnico per la distribuzione delle applicazioni in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

In questo articolo si apprenderà come funzionano le distribuzioni dell'applicazione.

## <a name="before-you-begin"></a>Operazioni preliminari

Per la risoluzione dei problemi relativi alle distribuzioni dell'applicazione, sono disponibili più elementi che possono essere utili quando si esaminano i log del client. Questi elementi includono:

- ID CI applicazione
- ID univoco dell'applicazione
- ID univoco del tipo di distribuzione
- ID univoco per la distribuzione dell'applicazione (noto anche come ID univoco di assegnazione)
- Scopo della distribuzione dell'applicazione
- ID contenuto univoco
- ID e nome della raccolta
- Tipo di raccolta

Per semplificare la risoluzione dei problemi, è possibile eseguire una query SQL simile alla seguente nel database di Configuration Manager per ottenere le informazioni elencate in precedenza.

```sql
SELECT APP.CI_ID [App CI ID], APP.CI_UniqueID [App Unique ID], APP.DisplayName [App Name],
DT.CI_UniqueID [DT Unique ID], DT.ContentId [DT Content ID],
CIA.Assignment_UniqueID [Assignment ID], CIA.CollectionID, CIA.CollectionName,
CASE CIA.OfferTypeID WHEN 0 THEN 'Required' WHEN 2 THEN 'Available' WHEN 3 THEN 'Simulate' ELSE 'Unknown' END AS [Deployment Purpose],
CASE C.CollectionType WHEN 1 THEN 'User Collection' WHEN 2 THEN 'Device Collection' ELSE 'Unknown' END AS [Collection Type],
DT.Technology, DT.DisplayName [DT Name]
FROM fn_ListApplicationCIs(1033) APP
JOIN fn_ListDeploymentTypeCIs(1033) DT ON DT.AppModelName = APP.ModelName AND DT.IsLatest = 1
LEFT JOIN v_CIAssignmentToCI CIACI ON CIACI.CI_ID = APP.CI_ID
LEFT JOIN v_CIAssignment CIA ON CIACI.AssignmentID = CIA.AssignmentID
LEFT JOIN v_Collection C ON C.CollectionID = CIA.CollectionID
WHERE APP.IsLatest = 1 AND APP.DisplayName = 'Application Name' -- Replace Application Name
```

> [!IMPORTANT]
> Quando si esegue questa query, è **necessario** usare il nome dell'applicazione elencato nella scheda informazioni generali delle proprietà dell'applicazione, invece di usare il nome dell'applicazione localizzato elencato nella scheda Software Center delle proprietà dell'applicazione.

## <a name="next-steps"></a>Passaggi successivi

- [Criteri di distribuzione delle applicazioni](/sccm/apps/understand/deployment-policy-technical-reference)

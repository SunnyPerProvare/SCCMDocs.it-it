---
title: Reinizializzazione dei dati globali
titleSuffix: Configuration Manager
description: Usare questo diagramma per avviare la risoluzione dei problemi di reinizializzazione della replica SQL per i dati globali in una gerarchia di Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d36622c0-776c-493b-971a-4a586fc394d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b4213c91c616278a6dd8fa3e58d40ba301b0ecb1
ms.sourcegitcommit: ccc3c929b5585c05d562020e68044de7d7e11c6a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2020
ms.locfileid: "80590561"
---
# <a name="troubleshoot-global-data-reinit"></a>Risoluzione dei problemi di reinizializzazione dei dati globali

In una gerarchia multisito Configuration Manager usa la replica SQL per trasferire i dati tra i siti. Per altre informazioni, vedere [Replica di database](/sccm/core/plan-design/hierarchy/database-replication).

Usare il diagramma seguente per avviare la risoluzione dei problemi di reinizializzazione della replica SQL per i dati globali in una gerarchia di Configuration Manager:

![Diagramma per la risoluzione dei problemi di reinizializzazione dei dati globali](media/global-data-reinit.svg)

## <a name="queries"></a>Query

Questo diagramma usa le query seguenti:

### <a name="check-if-site-replication-hasnt-finished-reinit"></a>Controllare se la replica del sito non ha terminato la reinizializzazione

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-primary-site"></a>Ottenere il GUID di traccia e lo stato dal sito primario

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N`Global'
```

### <a name="get-the-trackingguid--status-from-the-cas"></a>Ottenere il GUID di traccia e lo stato dal sito CAS

```sql
SELECT RequestTrackingGUID, InitializationStatus
FROM RCM_DrsInitializationTracking dt
WHERE RequestTrackingGUID=@trackingGuid
```

### <a name="check-request-status-for-the-tracking-id"></a>Controllare lo stato della richiesta per l'ID di traccia

```sql
SELECT Status FROM RCM_InitPackageRequest
WHERE RequestTrackingGUID=@trackGuid
```

## <a name="next-steps"></a>Passaggi successivi

- [Reinizializzazione del messaggio mancante](/sccm/core/servers/manage/replication/reinit-missing-message)

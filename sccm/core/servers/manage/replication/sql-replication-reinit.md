---
title: Reinizializzazione della replica SQL
titleSuffix: Configuration Manager
description: Usare questo diagramma per avviare la risoluzione dei problemi di reinizializzazione della replica SQL tra siti di Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ce4a1ca8-6433-4447-819f-19dd5faa6f46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 71baf0eb69c8a86879a32de5947ac7790453e59c
ms.sourcegitcommit: ccc3c929b5585c05d562020e68044de7d7e11c6a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2020
ms.locfileid: "80605737"
---
# <a name="sql-replication-reinit"></a>Reinizializzazione della replica SQL

In una gerarchia multisito Configuration Manager usa la replica SQL per trasferire i dati tra i siti. Per altre informazioni, vedere [Replica di database](/sccm/core/plan-design/hierarchy/database-replication).

Usare il diagramma seguente per avviare la risoluzione dei problemi di reinizializzazione della replica SQL:

![Diagramma per la risoluzione dei problemi di reinizializzazione della replica SQL](media/sql-replication-reinit.svg)

## <a name="queries"></a>Query

Questo diagramma usa le query seguenti:

### <a name="check-if-site-is-in-maintenance-mode"></a>Controllare se il sito si trova in modalità di manutenzione

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

### <a name="check-which-replication-group-hasnt-completed-reinit"></a>Controllare quale gruppo di replica non ha completato la reinizializzazione

```sql
SELECT * FROM RCM_DrsInitializationTracking
WHERE InitializationStatus NOT IN (6,7)
```

### <a name="check-global-data"></a>Controllare i dati globali

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'GLOBAL'
```

### <a name="check-site-data"></a>Controllare i dati del sito

```sql
SELECT * FROM RCM_DrsInitializationTracking dt
INNER JOIN ReplicationData rg
ON dt.ReplicationGroup = rg.ReplicationGroup
WHERE dt.InitializationStatus NOT IN (6,7)
AND rg.ReplicationPattern=N'Site'
```

## <a name="next-steps"></a>Passaggi successivi

- [Reinizializzazione dei dati globali](/sccm/core/servers/manage/replication/global-data-reinit)
- [Reinizializzazione dei dati del sito](/sccm/core/servers/manage/replication/site-data-reinit)
- [Configurazione SQL](/sccm/core/servers/manage/replication/sql-configuration)

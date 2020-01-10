---
title: Replica SQL
titleSuffix: Configuration Manager
description: Usare questo diagramma per avviare la risoluzione dei problemi di replica SQL tra siti di Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: adb198c4-da3c-49c3-8fbd-6d1361272869
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 03c0652c88d78806f796946c8da19a455dc80f56
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75793488"
---
# <a name="sql-replication"></a>Replica SQL

In una gerarchia multisito Configuration Manager usa la replica SQL per trasferire i dati tra i siti. Per altre informazioni, vedere [Replica di database](/sccm/core/plan-design/hierarchy/database-replication).

Usare il diagramma seguente per avviare la risoluzione dei problemi di replica SQL quando un collegamento ha esito negativo:

![Diagramma per la risoluzione dei problemi di replica SQL](media/sql-replication.svg)

## <a name="queries"></a>Query

Questo diagramma usa le query seguenti:

### <a name="check-if-the-replication-group-link-is-in-degraded-or-failed-state"></a>Controllare se lo stato del collegamento del gruppo di replica è danneggiato o non riuscito

```sql
SELECT * FROM RCM_ReplicationLinkStatus
WHERE Status IN (8, 9)
```

### <a name="check-if-replication-group-link-is-recently-calculated"></a>Controllare se il collegamento del gruppo di replica è stato calcolato di recente

```sql
DECLARE @cutoffTime DATETIME
SELECT @cutoffTime = DATEADD(minute, -30, GETUTCDATE())
SELECT * FROM RCM_ReplicationLinkStatus
WHERE UpdateTime >@cutoffTime
```

### <a name="check-sql-maintenance-mode"></a>Controllare la modalità manutenzione di SQL

```sql
SELECT * FROM ServerData
WHERE Status = 120
```

## <a name="next-steps"></a>Passaggi successivi

- [Reinizializzazione della replica SQL (reinit)](/sccm/core/servers/manage/replication/sql-replication-reinit)
- [Prestazioni SQL](/sccm/core/servers/manage/replication/sql-performance)
- [Configurazione SQL](/sccm/core/servers/manage/replication/sql-configuration)

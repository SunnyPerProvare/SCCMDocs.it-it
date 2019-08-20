---
title: Replica SQL
titleSuffix: Configuration Manager
description: Usare questo diagramma per avviare la risoluzione dei problemi di replica SQL tra siti di Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: adb198c4-da3c-49c3-8fbd-6d1361272869
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35c807010e821f5a9857e7cc9d18354db5758298
ms.sourcegitcommit: 6b5a003256305c1f0cb605e52aeaaf19c23af5a9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/12/2019
ms.locfileid: "68957741"
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

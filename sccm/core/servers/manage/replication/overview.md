---
title: Risolvere i problemi di replica SQL
titleSuffix: Configuration Manager
description: Usare questi diagrammi per semplificare la comprensione e la risoluzione dei problemi di replica SQL tra siti di Configuration Manager
ms.date: 08/09/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 71d7430e-c5aa-485b-8dc0-c80fd8f29f17
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e4f1506ce7931fdb95a447695fbd9bf0c12146e0
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "68957801"
---
# <a name="troubleshoot-sql-replication"></a>Risolvere i problemi di replica SQL

In una gerarchia multisito Configuration Manager usa la replica SQL per trasferire i dati tra i siti. Per altre informazioni, vedere [Replica di database](/sccm/core/plan-design/hierarchy/database-replication).

Per comprendere meglio e risolvere i problemi di replica SQL, usare questi diagrammi.

- [Replica SQL](/sccm/core/servers/manage/replication/sql-replication)
- [Configurazione SQL](/sccm/core/servers/manage/replication/sql-configuration)
- [Prestazioni SQL](/sccm/core/servers/manage/replication/sql-performance)
- [Reinizializzazione della replica SQL (reinit)](/sccm/core/servers/manage/replication/sql-replication-reinit)
- [Reinizializzazione dei dati globali](/sccm/core/servers/manage/replication/global-data-reinit)
- [Reinizializzazione dei dati del sito](/sccm/core/servers/manage/replication/site-data-reinit)
- [Reinizializzazione del messaggio mancante](/sccm/core/servers/manage/replication/reinit-missing-message)

Questi diagrammi per la risoluzione dei problemi sono interconnessi. Usare il diagramma seguente per comprenderne le relazioni:

![Diagramma di panoramica del processo di risoluzione dei problemi di replica SQL](media/overview.png)

<!-- PNG used instead of SVG because of weird blankspace in the SVG. The SVG file exists in the same location. -->

Per altre informazioni, vedere la serie seguente di blog del supporto tecnico Microsoft:

- [ConfigMgr DRS Synchronization Internals](https://blogs.technet.microsoft.com/umairkhan/2019/06/01/configmgr-drs-synchronization-internals/) (Elementi interni della sincronizzazione di ConfigMgr DRS)
- [ConfigMgr 2012 Data Replication Service (DRS) Unleashed](https://blogs.technet.microsoft.com/umairkhan/2014/02/17/configmgr-2012-data-replication-service-drs-unleashed/) (ConfigMgr 2012 Data Replication Service (DRS) al massimo)
- [ConfigMgr 2012 DRS – Troubleshooting FAQs](https://blogs.technet.microsoft.com/umairkhan/2014/03/24/configmgr-2012-drs-troubleshooting-faqs/) (ConfigMgr 2012 DRS - Domande frequenti sulla risoluzione dei problemi)
- [ConfigMgr 2012 DRS Initialization Internals](https://blogs.technet.microsoft.com/umairkhan/2015/01/21/configmgr-2012-drs-initialization-internals/) (Elementi interni dell'inizializzazione di ConfigMgr 2012 DRS)
- [ConfigMgr 2012: DRS and SQL service broker certificate issues](https://blogs.technet.microsoft.com/umairkhan/2013/12/12/configmgr-2012-drs-and-sql-service-broker-certificate-issues/) (ConfigMgr 2012: DRS e problemi dei certificati SQL Service Broker)

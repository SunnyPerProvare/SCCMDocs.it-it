---
title: Monitorare il gateway di gestione cloud - Configuration Manager | Microsoft Docs
description: 
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 199096db7a23fb14db98b95e75246ed254848ab7
ms.openlocfilehash: df32a7d95799d8ae685fd66e2d9ddf25e32b37d0
ms.lasthandoff: 03/27/2017

---

# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>Monitorare il gateway di gestione cloud in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

A partire dalla versione 1610, se il servizio gateway di gestione cloud è in esecuzione e i client sono connessi tramite questo servizio, è possibile monitorare i client e il traffico di rete per controllare il funzionamento del servizio.

## <a name="monitor-clients"></a>Monitorare i client

I client connessi tramite il servizio gateway di gestione cloud vengono visualizzati nella console di Configuration Manager come nel caso di client locali. Per altre informazioni, vedere [Come monitorare i client in System Center Configuration Manager](monitor-clients.md).

## <a name="monitor-traffic-in-the-console"></a>Monitorare il traffico nella console

È possibile monitorare il traffico relativo al gateway di gestione cloud usando la console di Configuration Manager:

1. Passare a **Amministrazione > Servizi Cloud > Cloud Management Gateway** (Gateway di gestine cloud).

2. Selezionare il servizio gateway di gestione cloud nell'elenco dei campi.

3. Visualizzare le informazioni sul traffico nel riquadro dei dettagli per il ruolo di connessione del gateway di gestione cloud e per i ruoli del sistema del sito ai quali è connesso.

## <a name="set-up-outbound-traffic-alerts"></a>Configurare gli avvisi del traffico in uscita

Gli avvisi del traffico in uscita consentono di sapere quando il traffico sta per raggiungere un livello di soglia di 14 giorni, vale a dire 2 settimane. Gli avvisi del traffico in uscita possono essere configurati quando si crea il servizio gateway di gestione cloud. Se questa operazione non è stata eseguita, è possibile configurare gli avvisi anche dopo che il servizio è in esecuzione. È anche possibile regolare le impostazioni degli avvisi in qualsiasi momento.

1. Passare a **Amministrazione > Servizi Cloud > Cloud Management Gateway** (Gateway di gestine cloud).

2. Fare clic con il pulsante destro del mouse sul servizio gateway di gestione cloud nell'elenco dei campi e scegliere **Proprietà**.

3. Fare clic sulla scheda Avvisi e scegliere di abilitare (o disabilitare) la soglia e gli avvisi. Specificare la soglia di 14 giorni (in GB) e le percentuali di soglia per generare diversi livelli di avviso.

4. Al termine fare clic su **OK**.

## <a name="monitor-logs"></a>Monitorare i log

Il servizio gateway di gestione cloud genera voci in alcuni file di log. Per altre informazioni, vedere [Log in Configuration Manager](/sccm/core/plan-design/hierarchy/log-files).


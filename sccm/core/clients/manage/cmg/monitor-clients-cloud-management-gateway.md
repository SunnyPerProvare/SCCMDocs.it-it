---
title: Monitorare il gateway di gestione cloud
titleSuffix: Configuration Manager
description: Monitorare i client e il traffico di rete attraverso il gateway di gestione di cloud.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a4ecbeb2484297160797b7b5632c86cee4ff1122
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32332475"
---
# <a name="monitor-cloud-management-gateway-in-configuration-manager"></a>Monitorare il gateway di gestione cloud in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Se il gateway di gestione cloud è in esecuzione e i client si connettono attraverso di esso, è possibile monitorare i client e il traffico di rete per controllare le prestazioni del servizio.



## <a name="monitor-clients"></a>Monitorare i client

I client connessi tramite il gateway di gestione cloud vengono visualizzati nella console di Configuration Manager allo stesso modo dei client locali. Per altre informazioni, vedere [Come monitorare i client in System Center Configuration Manager](/sccm/core/clients/manage/monitor-clients).



## <a name="monitor-traffic-in-the-console"></a>Monitorare il traffico nella console

Monitorare il traffico attraverso il gateway di gestione cloud tramite la console di Configuration Manager:

1. Passare a **Amministrazione > Servizi Cloud > Cloud Management Gateway** (Gateway di gestine cloud).

2. Selezionare il gateway di gestione cloud nel riquadro di elenco.

3. Visualizzare le informazioni sul traffico nel riquadro dei dettagli per il punto di connessione del gateway di gestione cloud e per i ruoli del sistema del sito ai quali è connesso.



## <a name="set-up-outbound-traffic-alerts"></a>Configurare gli avvisi del traffico in uscita

Gli avvisi del traffico in uscita consentono di sapere quando il traffico di rete sta per raggiungere un livello di soglia di 14 giorni. Quando si crea il gateway di gestione cloud, è possibile impostare avvisi relativi al traffico. Se questa operazione non è stata eseguita, è possibile configurare gli avvisi anche dopo che il servizio è in esecuzione. È possibile regolare le impostazioni degli avvisi in qualsiasi momento.

1. Passare a **Amministrazione > Servizi Cloud > Cloud Management Gateway** (Gateway di gestine cloud).

2. Fare clic con il pulsante destro del mouse sul gateway di gestione cloud nel riquadro di elenco e scegliere **Proprietà**.

3. Fare clic sulla scheda **Avvisi**. Abilitare la soglia e gli avvisi. Specificare la soglia di 14 giorni per i dati in gigabyte (GB). Specificare anche le percentuali della soglia in corrispondenza delle quali devono essere generati i diversi livelli di avviso.

4. Al termine fare clic su **OK**.



## <a name="monitor-logs"></a>Monitorare i log

Il gateway di gestione cloud genera voci in alcuni file di log. Per altre informazioni, vedere [Log in Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).

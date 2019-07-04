---
title: Infrastruttura di rete
titleSuffix: Configuration Manager
description: Configurare firewall, porte e domini per la prepararsi per le comunicazioni di Configuration Manager.
ms.date: 06/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 60a24e06d650b0e25007fb8490eb0c7d8c1996a1
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/20/2019
ms.locfileid: "67285620"
---
# <a name="network-infrastructure-considerations-for-configuration-manager"></a>Considerazioni sull'infrastruttura di rete per Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Per preparare la rete per supportare Configuration Manager, potrebbe essere necessario configurare alcuni componenti dell'infrastruttura. Potrebbe ad esempio essere necessario aprire porte del firewall per passare le comunicazioni usate da Configuration Manager.  

## <a name="ports-and-protocols"></a>Porte e protocolli

Le diverse funzionalità di Configuration Manager usano porte di rete diverse. Alcune porte sono obbligatorie, mentre altre possono essere personalizzate.

La maggior parte delle comunicazioni di Configuration Manager usa porte comuni, ad esempio la porta 80 per HTTP o la 443 per HTTPS. Alcuni ruoli del sistema del sito supportano l'uso di siti Web personalizzati e porte personalizzate. Per altre informazioni, vedere [Siti Web per i server del sistema del sito](/sccm/core/plan-design/network/websites-for-site-system-servers).

Prima di distribuire Configuration Manager, identificare le porte da usare e configurare i firewall in base alle esigenze.

Dopo aver installato Configuration Manager, se è necessario modificare una porta, non trascurare l'aggiornamento dei firewall sui dispositivi e nella rete. Modificare anche la configurazione della porta in Configuration Manager.

Per altre informazioni, vedere gli articoli seguenti:

- [Come configurare le porte di comunicazione client](/sccm/core/clients/deploy/configure-client-communication-ports)
- [Porte usate in Configuration Manager](/sccm/core/plan-design/hierarchy/ports)


## <a name="internet-access-requirements"></a>Requisiti per l'accesso a Internet

Alcune caratteristiche di Configuration Manager hanno bisogno della connettività Internet per funzionare completamente. Se l'organizzazione limita le comunicazioni della rete con Internet tramite un firewall o un dispositivo proxy, assicurarsi di consentire l'accesso degli endpoint necessari.

Per altre informazioni, vedere i [requisiti di accesso Internet](/sccm/core/plan-design/network/internet-endpoints).


## <a name="proxy-servers"></a>Server proxy

È possibile specificare i server proxy per diversi client e server di sistema del sito. Queste configurazioni si effettuano quando si installa un client o un ruolo del sistema del sito o li si modifica in seguito in base alle esigenze.

Per altre informazioni, vedere [Supporto dei server proxy](/sccm/core/plan-design/network/proxy-server-support).

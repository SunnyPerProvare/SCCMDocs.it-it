---
title: Configurare la riattivazione LAN | Microsoft Docs
description: Selezionare la riattivazione LAN in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b475a0c8-85d6-4cc4-b11f-32c0cc98239e
caps.latest.revision: 7
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: 09f8bc7ee04ff64934030f825a791bc043341963
ms.lasthandoff: 12/16/2016

---
# <a name="how-to-configure-wake-on-lan-in-system-center-configuration-manager"></a>Come configurare la riattivazione LAN in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Specificare le impostazioni di riattivazione LAN per System Center Configuration Manager quando si vuole riattivare i computer da uno stato di sospensione per installare il software necessario, come aggiornamenti software, applicazioni, sequenze di attività e programmi.

È possibile integrare la riattivazione LAN usando le impostazioni client proxy di riattivazione. Prima di utilizzare il proxy di riattivazione è tuttavia necessario attivare la riattivazione LAN per il sito e specificare **Utilizza solo pacchetti di riattivazione** e l'opzione **Unicast** per il metodo di trasmissione riattivazione LAN. Questa soluzione di riattivazione supporta anche connessioni ad hoc, ad esempio una connessione desktop remoto.

Utilizzare la prima procedura per configurare un sito primario per la riattivazione LAN. Usare quindi la seconda procedura per configurare le impostazioni client proxy di riattivazione. Questa seconda procedura consente di configurare le impostazioni client predefinite per le impostazioni proxy di riattivazione da applicare a tutti i computer nella gerarchia. Se si desidera applicare queste impostazioni solo ad alcuni computer, creare un'impostazione dispositivo personalizzata e assegnarla a una raccolta che contenga i computer che si desidera configurare per il proxy di riattivazione. Per ulteriori informazioni su come creare impostazioni client personalizzate, vedere [Come configurare le impostazioni client in System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).

Un computer che riceve le impostazioni client proxy di riattivazione sospenderà probabilmente la connessione di rete per 1-3 secondi. Ciò si verifica perché il client deve reimpostare la scheda di interfaccia di rete per abilitare il driver proxy di riattivazione.

> [!WARNING]
> Per evitare interruzioni impreviste dei servizi di rete, valutare prima il proxy di riattivazione in un'infrastruttura di rete isolata e rappresentativa. Utilizzare quindi le impostazioni client personalizzate per espandere la verifica a un gruppo selezionato di computer in diverse subnet. Per altre informazioni sul funzionamento dei proxy di riattivazione, vedere [Pianificare la riattivazione dei client in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).

## <a name="to-configure-wake-on-lan-for-a-site"></a>Per configurare la riattivazione LAN per un sito

1. Nella console di Configuration Manager passare ad **Amministrazione > Configurazione del sito > Siti**.
2. Fare clic sul sito primario da configurare, quindi su **Proprietà**.
3. Fare clic nella scheda **Riattivazione LAN**, quindi configurare le opzioni necessarie per questo sito. Per il supporto del proxy di riattivazione, selezionare **Utilizza solo pacchetti di riattivazione** e **Unicast**. Per altre informazioni, vedere [Pianificare la riattivazione dei client in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).
4. Fare clic su **OK** e ripetere questa procedura per tutti i siti primari nella gerarchia.

## <a name="to-configure-wake-up-proxy-client-settings"></a>Per configurare le impostazioni client proxy di riattivazione

1. Nella console di Configuration Manager scegliere **Amministrazione > Impostazioni client**.
2. Fare clic su **Impostazioni client predefinite**, quindi su **Proprietà**.
3. Selezionare **Risparmio energia** e quindi scegliere **Sì** per **Abilitare il proxy di riattivazione**.
4. Riesaminare e, se necessario, configurare le altre impostazioni proxy di riattivazione. Per altre informazioni su queste impostazioni, vedere [Impostazioni di risparmio energia](../../../core/clients/deploy/about-client-settings.md#power-management).
5. Fare clic su **OK** per chiudere la finestra di dialogo e su **OK** per chiudere la finestra di dialogo Impostazioni client predefinite.

È possibile utilizzare i seguenti report di riattivazione LAN per monitorare l'installazione e la configurazione del proxy di riattivazione:

- Riepilogo dello stato della distribuzione del proxy di riattivazione
- Dettagli dello stato della distribuzione del proxy di riattivazione

> [!TIP]
> Per verificare il funzionamento del proxy di riattivazione, verificare una connessione a un computer in sospensione. Ad esempio, connettersi a una cartella condivisa nel computer o tentare di connettersi al computer tramite Desktop remoto. Se si usa Direct Access, controllare il funzionamento dei prefissi IPv6 eseguendo le stesse verifiche per un computer in sospensione attualmente in Internet.


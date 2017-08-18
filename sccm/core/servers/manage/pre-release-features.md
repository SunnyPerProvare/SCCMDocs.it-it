---
title: "Funzionalità di versioni non definitive| Microsoft Docs"
description: "Funzionalità di versioni non definitive in System Center Configuration Manager"
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
caps.latest.revision: 36
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: 7b594daeed81ef2d991ad06489f9184a69804117
ms.contentlocale: it-it
ms.lasthandoff: 07/29/2017

---
# <a name="pre-release-features-in-system-center-configuration-manager"></a>Funzionalità di versioni non definitive in System Center Configuration Manager
*Si applica a: System Center Configuration Manager (Current Branch)*

Le funzionalità di versioni non definitive sono incluse nel Current Branch a scopo di test preliminare in un ambiente di produzione. Queste funzionalità sono completamente supportate ma sono ancora in fase di sviluppo e, fino a quando non vengono spostate dalla categoria Versioni non definitive, possono essere soggette a modifiche.

 Prima di poter usare le funzionalità di versioni non definitive è necessario dare il consenso all'uso delle funzionalità di versioni non definitive nella console di Configuration Manager per poterle selezionare e abilitarne l'uso.  

L'azione con cui si dà il consenso viene eseguita una sola volta per ogni gerarchia e non può essere annullata. Finché non viene dato il consenso, non è possibile abilitare le nuove funzionalità di versioni non definitive incluse negli aggiornamenti. Dopo l'attivazione di una funzione non definitiva, non è possibile procedere alla relativa disattivazione.

Per dare il consenso, nella console passare ad **Amministrazione** > **Configurazione del sito** > **Siti** e quindi scegliere **Impostazioni gerarchia**. Nella scheda **Generale** scegliere **Consenso a usare funzionalità di versioni non definitive**.

 > [!NOTE]
 > Se sono state abilitate dall'aggiornamento 1602 prima dell'installazione dell'aggiornamento successivo, le funzionalità di versioni non definitive rimangono abilitate, anche se non viene dato il consenso all'uso.

Durante l'installazione di un aggiornamento che include funzionalità di versioni non definitive, tali funzionalità sono visibili nella procedura guidata Aggiornamenti e manutenzione insieme alle normali funzionalità incluse nell'aggiornamento:
  - **Se è stato dato il consenso:** è possibile abilitare le funzionalità di versioni non definitive dall'interno della procedura guidata degli aggiornamenti e della manutenzione durante l'installazione dell'aggiornamento. A tale scopo, selezionare le funzionalità di versioni non definitive allo stesso modo in cui si selezionano le altre funzionalità.     

    Facoltativamente, è possibile abilitare una funzionalità di versione non definitiva in un secondo momento dal nodo della console **Amministrazione** > **Aggiornamenti e manutenzione** > **Funzionalità**. Nel nodo **Funzionalità** scegliere la voce desiderata e quindi **Attiva**. Questa opzione è disattivata finché non si dà il consenso. Nelle versioni precedenti la 1702, Aggiornamenti e manutenzione si trova in **Amministrazione** > **Servizi cloud**.
  -   **Se non è stato dato il consenso:** durante l'installazione di un aggiornamento, le funzionalità di versioni non definitive sono visibili nella procedura guidata Aggiornamenti e manutenzione, ma appaiono disattivate e non possono essere abilitate. Dopo l'installazione dell'aggiornamento è possibile visualizzare queste funzionalità nel nodo **Funzionalità**. Tuttavia non è possibile abilitarle finché non viene dato il consenso in **Impostazioni gerarchia**.

Se dopo aver dato il consenso a un sito primario autonomo si espande la gerarchia installando un nuovo sito di amministrazione centrale, è necessario dare di nuovo il consenso al sito di amministrazione centrale.

 Quando si abilita una funzionalità non definitiva, gestione gerarchie (HMAN) di Configuration Manager deve elaborare la modifica prima che tale funzionalità diventi disponibile. L'elaborazione della modifica è spesso immediata, ma possono essere necessari fino a 30 minuti, a seconda del ciclo di elaborazione HMAN. Dopo l'elaborazione della modifica è necessario riavviare la console prima di poter visualizzare la nuova interfaccia utente relativa a tale funzionalità.

**Per la versione non definitiva sono disponibili le funzionalità seguenti:**

 |Funzionalità          |Aggiunta come versione non definitiva | Aggiunta come funzionalità completa|  
|------------------|---------------------|---------------------|
| Creare ed eseguire script di PowerShell dalla console di Configuration Manager |  [Versione 1706](/sccm/apps/deploy-use/create-deploy-scripts)|![Non ancora](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Gestione di Device Guard con Configuration Manager |  [Versione 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|![Non ancora](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Controllare l'esecuzione di file eseguibili prima di installare un'applicazione  |   [Versione 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |![Non ancora](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Punto di servizio del data warehouse  |  [Versione 1702](/sccm/core/servers/manage/data-warehouse) |[Versione 1706](/sccm/core/servers/manage/data-warehouse)|
| Peer cache per la distribuzione del contenuto ai client |  [Versione 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) |![Non ancora](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Gateway di gestione cloud |  [Versione 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |![Non ancora](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Dashboard origini dati del client |  [Versione 1610](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard) |![Non ancora](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Microsoft Operations Management Suite Connector  | [Versione 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![Non ancora](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Manutenzione di una raccolta compatibile con cluster (manutenzione di un gruppo di server)| [Versione 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![Non ancora](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|Accesso condizionale per i PC gestiti da System Center Configuration Manager | [Versione 1602](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)     | [Versione 1702](/sccm/mdm/deploy-use/manage-access-to-services)                     |


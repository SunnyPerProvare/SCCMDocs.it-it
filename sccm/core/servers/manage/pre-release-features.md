---
title: "Funzionalità di versioni non definitive| Microsoft Docs"
description: "Funzionalità di versioni non definitive in System Center Configuration Manager"
ms.custom: na
ms.date: 3/27/2017
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
translationtype: Human Translation
ms.sourcegitcommit: f9097014c7e988ec8e139e518355c4efb19172b3
ms.openlocfilehash: c164ae7ca17a3a7d96b010f41b5ecf72ab34976b
ms.lasthandoff: 03/04/2017


---
# <a name="pre-release-feaures-in-system-center-configuration-manager"></a>Funzionalità di versioni non definitive in System Center Configuration Manager
*Si applica a: System Center Configuration Manager (Current Branch)*

 Le funzionalità di versioni non definitive sono incluse nel Current Branch a scopo di test preliminare in un ambiente di produzione. Queste funzionalità non devono essere considerate pronte per l'ambiente di produzione, ma possono essere usate in un ambiente di questo tipo.

 Prima di poter usare le funzionalità di versioni non definitive è necessario dare il consenso all'uso delle funzionalità di versioni non definitive nella console di Configuration Manager per poterle selezionare e abilitarne l'uso.  

L'azione con cui si dà il consenso viene eseguita una sola volta per ogni gerarchia e non può essere annullata. Finché non viene dato il consenso, non è possibile abilitare le nuove funzionalità di versioni non definitive incluse negli aggiornamenti.

Per dare il consenso, nella console passare ad **Amministrazione** > **Configurazione del sito** > **Siti** e quindi scegliere **Impostazioni gerarchia**. Nella scheda **Generale** scegliere **Consenso a usare funzionalità di versioni non definitive**.

 > [!NOTE]
 > Se sono state abilitate nell'aggiornamento 1602 prima dell'installazione dell'aggiornamento successivo, le funzionalità di versioni non definitive rimangono abilitate anche se non viene dato il consenso all'uso.

Durante l'installazione di un aggiornamento che include funzionalità di versioni non definitive, tali funzionalità sono visibili nella procedura guidata Aggiornamenti e manutenzione insieme alle normali funzionalità incluse nell'aggiornamento:
  - **Se è stato dato il consenso:** è possibile abilitare le funzionalità di versioni non definitive dall'interno della procedura guidata degli aggiornamenti e della manutenzione durante l'installazione dell'aggiornamento. A tale scopo, selezionare le funzionalità di versioni non definitive allo stesso modo in cui si selezionano le altre funzionalità.     

    Facoltativamente, è possibile abilitare una funzionalità di versione non definitiva successivamente dal nodo della console **Amministrazione** > **Servizi cloud** > **Aggiornamenti e manutenzione** > **Funzionalità**. Nel nodo **Funzionalità** scegliere la voce desiderata e quindi **Attiva**. Questa opzione è disattivata finché non si dà il consenso.  
  -   **Se non è stato dato il consenso:** durante l'installazione di un aggiornamento, le funzionalità di versioni non definitive sono visibili nella procedura guidata Aggiornamenti e manutenzione ma appaiono disattivate e non possono essere abilitate. Dopo l'installazione dell'aggiornamento, le funzionalità sono visibili nel nodo **Funzionalità**, ma è possibile abilitarle solo dopo aver dato il consenso in **Impostazioni gerarchia**.

Se dopo aver dato il consenso a un sito primario autonomo si espande la gerarchia installando un nuovo sito di amministrazione centrale, è necessario dare di nuovo il consenso al sito di amministrazione centrale.

**Per la versione non definitiva sono disponibili le funzionalità seguenti:**

 |Funzionalità          |Aggiunta come versione non definitiva | Aggiunta come funzionalità completa|  
|------------------|---------------------|---------------------|
| Punto di servizio del data warehouse  |  [Versione 1702](/sccm/core/servers/manage/data-warehouse) |![Non ancora](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Peer cache per la distribuzione del contenuto ai client |  [Versione 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) |![Non ancora](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Gateway di gestione cloud |  [Versione 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |![Non ancora](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Dashboard origini dati del client |  [Versione 1610](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard) |![Non ancora](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Microsoft Operations Management Suite Connector  | [Versione 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![Non ancora](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Manutenzione di una raccolta compatibile con cluster (manutenzione di un gruppo di server)| [Versione 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_ServerGroups)|![Non ancora](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|Accesso condizionale per i PC gestiti da System Center Configuration Manager | [Versione 1602](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)     |![Non ancora](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)                        |


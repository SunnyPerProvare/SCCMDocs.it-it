---
title: Aggiornare il sistema operativo di un computer esistente
titleSuffix: Configuration Manager
description: È possibile usare vari metodi in Configuration Manager per eseguire partizioni e formattare un computer esistente e installare un nuovo sistema operativo nel computer.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e2443f8ddc280e880ffb43a8e82bbc47b49d4395
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "70110206"
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows"></a>Aggiornare un computer esistente con una nuova versione di Windows

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare Configuration Manager per partizionare e formattare un computer esistente e quindi installare un nuovo sistema operativo. Questo processo viene talvolta definito *ricreazione dell'immagine* o *cancellazione e caricamento*. Per questo scenario, scegliere tra i numerosi e diversi metodi di distribuzione disponibili, ad esempio PXE, supporti di avvio o Software Center. È anche possibile usare un punto di migrazione stato per archiviare le impostazioni e quindi ripristinarle nel nuovo sistema operativo.

Per scegliere lo scenario di distribuzione del sistema operativo corretto, vedere [scenari per la distribuzione di sistemi operativi aziendali](/sccm/osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems).  

## <a name="BKMK_Plan"></a> Pianificazione  

### <a name="plan-for-and-implement-infrastructure-requirements"></a>Pianificare e implementare i requisiti di infrastruttura

Prima di poter distribuire un sistema operativo, è necessario disporre di diversi requisiti di infrastruttura. Alcuni di questi requisiti includono Windows ADK, il Utilità di migrazione stato utente (USMT) e servizi di distribuzione Windows (WDS). Per altre informazioni, vedere [Requisiti dell'infrastruttura per la distribuzione del sistema operativo](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

### <a name="install-a-state-migration-point"></a>Installare un punto di migrazione stato

Se si desidera acquisire le impostazioni da un computer esistente e quindi ripristinare le impostazioni nel nuovo sistema operativo, provare a usare un punto di migrazione stato. Per altre informazioni, vedere [Punto di migrazione dello stato](/sccm/osd/get-started/prepare-site-system-roles-for-operating-system-deployments#BKMK_StateMigrationPoints).  

## <a name="BKMK_Configure"></a> Configura  

### <a name="prepare-a-boot-image"></a>Preparare un'immagine d'avvio

Le immagini di avvio avviano un computer in un ambiente Windows PE. Windows PE è un sistema operativo minimo con componenti e servizi limitati. Da Windows PE, Configuration Manager possibile installare un sistema operativo Windows completo nel computer.

Per altre informazioni, vedere gli articoli seguenti:

- [Gestire le immagini di avvio](/sccm/osd/get-started/manage-boot-images)

- [Personalizzare le immagini di avvio](/sccm/osd/get-started/customize-boot-images)

- [Distribuire il contenuto](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute)

### <a name="prepare-an-os-image"></a>Preparare un'immagine del sistema operativo

L'immagine del sistema operativo contiene i file necessari per installare il sistema operativo nel computer di destinazione.

Per altre informazioni, vedere gli articoli seguenti:

- [Gestire le immagini del sistema operativo](/sccm/osd/get-started/manage-operating-system-images)

- [Distribuire il contenuto](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute)

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Creare una sequenza di attività per distribuire un sistema operativo

Usare una sequenza di attività per automatizzare l'installazione del sistema operativo. A seconda del metodo di distribuzione scelto, potrebbero essere necessarie considerazioni aggiuntive per la sequenza di attività.

Per altre informazioni, vedere gli articoli seguenti:

- [Creare una sequenza di attività per installare un sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-install-an-operating-system)

- [Gestire lo stato utente](/sccm/osd/get-started/manage-user-state)

## <a name="BKMK_Deploy"></a> Distribuisci

- Per distribuire il sistema operativo, usare uno dei metodi di distribuzione seguenti:  

  - [Usare PXE per distribuire Windows in rete](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network)  

  - [Usare il multicast per distribuire Windows in rete](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network)  

  - [Creare un'immagine per un OEM presso un produttore computer o un deposito locale](/sccm/osd/deploy-use/create-an-image-for-an-oem-in-factory-or-a-local-depot)  

  - [Use stand-alone media to deploy Windows without using the network](/sccm/osd/deploy-use/use-stand-alone-media-to-deploy-windows-without-using-the-network) (Usare i supporti autonomi per distribuire Windows senza usare la rete)  

  - [Usare i supporti di avvio per distribuire Windows in rete](/sccm/osd/deploy-use/use-bootable-media-to-deploy-windows-over-the-network)  

  - [Use Software Center to deploy Windows over the network](/sccm/osd/deploy-use/use-software-center-to-deploy-windows-over-the-network) (Usare Software Center per distribuire Windows tramite la rete)  

## <a name="monitor"></a>Monitoraggio  

Per altre informazioni, vedere [Monitorare le distribuzioni del sistema operativo](/sccm/osd/deploy-use/monitor-operating-system-deployments).  

> [!Note]
> Quando si ricrea l'immagine di un dispositivo UEFI, Windows Boot Manager crea una nuova voce nel caricatore di avvio. Questo comportamento è più evidente quando si ricrea ripetutamente un'immagine di un dispositivo, ad esempio in un ambiente di test o in un Lab per studenti. Generalmente non influisca sulle prestazioni o sull'utilizzo del dispositivo. Se l'elenco diventa troppo grande, è possibile che alcuni dispositivi hardware specifici riscontrino problemi funzionali. Ad esempio, non eseguire l'avvio in un'unità USB esterna oppure non è possibile selezionare la voce di avvio corrente dall'elenco. Usare il comando **bcdedit** di Windows per cancellare le voci di avvio inutilizzate. Per ulteriori informazioni, vedere [bcdedit/deletevalue](https://docs.microsoft.com/windows-hardware/drivers/devtest/bcdedit--deletevalue).<!-- 2841926 -->

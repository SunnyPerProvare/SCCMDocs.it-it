---
title: Aggiornare un computer esistente con una nuova versione di Windows
titleSuffix: Configuration Manager
description: "È possibile usare vari metodi in Configuration Manager per eseguire partizioni e formattare (cancellare) un computer esistente e installare un nuovo sistema operativo nel computer."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b189a346-8c0d-4870-a876-0719fbb0ab04
caps.latest.revision: "7"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: a7a3f61793e92453b8ccc048192d3ae858a78a4a
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="refresh-an-existing-computer-with-a-new-version-of-windows-using-system-center-configuration-manager"></a>Aggiornare un computer esistente con una nuova versione di Windows tramite System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo argomento illustra la procedura generale in Configuration Manager per eseguire partizioni e formattare (cancellare) un computer esistente e installare un nuovo sistema operativo nel computer. Per questo scenario è possibile scegliere tra i numerosi e diversi metodi di distribuzione disponibili, ad esempio PXE, supporti di avvio o Software Center. È anche possibile scegliere di installare un punto di migrazione stato per archiviare le impostazioni e quindi ripristinarle nel nuovo sistema operativo dopo l'installazione. Se non si è sicuri che questo sia lo scenario di distribuzione del sistema operativo più adatto alle esigenze, vedere [Scenari per distribuire sistemi operativi aziendali](scenarios-to-deploy-enterprise-operating-systems.md).  

 Per informazioni su come aggiornare un computer esistente con una nuova versione di Windows, vedere le sezioni seguenti.  

##  <a name="BKMK_Plan"></a> Pianificazione  

-   **Pianificare e implementare i requisiti di infrastruttura**  

     Per poter distribuire i sistemi operativi, è necessario soddisfare diversi requisiti di infrastruttura, ad esempio Windows ADK, Utilità di migrazione stato utente (USMT), Servizi di distribuzione Windows (WDS), configurazioni supportate del disco rigido e così via. Per altre informazioni, vedere [Requisiti dell'infrastruttura per la distribuzione del sistema operativo](../plan-design/infrastructure-requirements-for-operating-system-deployment.md).  

-   **Installare un punto di migrazione stato, obbligatorio solo se si trasferiscono le impostazioni**  

     Quando si prevede di acquisire le impostazioni dal computer esistente e quindi di ripristinarle nel nuovo sistema operativo, è necessario installare un punto di migrazione stato. Per altre informazioni, vedere [Punto di migrazione dello stato](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

##  <a name="BKMK_Configure"></a> Configura  

1.  **Preparare un'immagine d'avvio**  

     Le immagini d'avvio avviano un computer in un ambiente Windows PE (un sistema operativo minimo con componenti e servizi limitati) che può quindi installare un sistema operativo Windows completo nel computer.   Quando si distribuiscono sistemi operativi, è necessario selezionare un'immagine d'avvio da usare e distribuirla in un punto di distribuzione. Per preparare l'immagine d'avvio, vedere quanto segue:  

    -   Per altre informazioni sulle immagini d'avvio, vedere [Gestire le immagini di avvio](../get-started/manage-boot-images.md).  

    -   Per altre informazioni su come personalizzare un'immagine di avvio, vedere [Personalizzare immagini di avvio](../get-started/customize-boot-images.md).  

    -   Distribuire l'immagine d'avvio nei punti di distribuzione. Per altre informazioni, vedere [Distribuire contenuto](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

2.  **Preparare un'immagine del sistema operativo**  

     L'immagine del sistema operativo contiene i file necessari per installare il sistema operativo nel computer di destinazione. Per preparare l'immagine del sistema operativo, vedere quanto segue:  

    -   Per altre informazioni su come creare un'immagine del sistema operativo, vedere [Gestire immagini del sistema operativo](../get-started/manage-operating-system-images.md).  

    -   Distribuire l'immagine del sistema operativo nei punti di distribuzione. Per altre informazioni, vedere [Distribuire contenuto](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

3.  **Creare una sequenza di attività per distribuire sistemi operativi nella rete**  

     Usare una sequenza di attività per automatizzare l'installazione del sistema operativo nella rete. Usare i passaggi in [Creare una sequenza di attività per installare un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md) per creare la sequenza di attività per distribuire il sistema operativo. A seconda del metodo di distribuzione scelto, potrebbero essere necessarie considerazioni aggiuntive per la sequenza di attività.  

    > [!NOTE]  
    >  In questo scenario, la sequenza di attività formatta e partiziona i dischi rigidi del computer. Per acquisire le impostazioni utente, è necessario usare il punto di migrazione stato e selezionare **Salva impostazioni utente e file in punto di migrazione stato** nella pagina **Migrazione stato** della Creazione guidata della sequenza attività. Se le impostazioni utente e i file vengono salvati localmente, andranno persi quando il disco rigido viene formattato e Configuration Manager non potrà ripristinare le impostazioni. Per altre informazioni, vedere [Gestire lo stato utente](../get-started/manage-user-state.md).  

##  <a name="BKMK_Deploy"></a> Distribuisci  

-   Usare uno dei metodi di distribuzione seguenti per distribuire il sistema operativo:  

    -   [Usare PXE per distribuire Windows in rete](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [Usare il multicast per distribuire Windows in rete](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Creare un'immagine per un OEM in modalità produttore computer o per un rivenditore locale](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [Usare i supporti autonomi per distribuire Windows senza usare la rete](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [Usare i supporti di avvio per distribuire Windows in rete](use-bootable-media-to-deploy-windows-over-the-network.md)  

    -   [Usare Software Center per distribuire Windows in rete](use-software-center-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Monitoraggio  

-   **Monitorare la distribuzione della sequenza di attività**  

     Per monitorare la distribuzione della sequenza di attività per l'installazione del sistema operativo, vedere [Monitorare le distribuzioni del sistema operativo](monitor-operating-system-deployments.md).  

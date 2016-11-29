---
title: Installare una nuova versione di Windows in un nuovo computer (bare metal) con System Center Configuration Manager
description: Seguire questa procedura in System Center Configuration Manager per installare un sistema operativo in un nuovo computer tramite PXE, OEM o supporti autonomi.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5ad22d5-7df1-49c6-8a0f-db1c3f0cda19
caps.latest.revision: 8
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: c672595a06a45bec840f17743636ef6f502af49f


---
# <a name="install-a-new-version-of-windows-on-a-new-computer-bare-metal-with-system-center-configuration-manager"></a>Installare una nuova versione di Windows in un nuovo computer (bare metal) con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo argomento specifica i passaggi generali di System Center Configuration Manager per installare un sistema operativo in un nuovo computer. Per questo scenario è possibile scegliere tra vari metodi di distribuzione diversi, ad esempio PXE, OEM o supporti autonomi. Se non si è sicuri che questo sia lo scenario di distribuzione del sistema operativo più adatto alle proprie esigenze, vedere [Scenari di distribuzione di sistemi operativi aziendali](scenarios-to-deploy-enterprise-operating-systems.md).  

 Per informazioni su come aggiornare un computer esistente con una nuova versione di Windows, vedere le sezioni seguenti.  

##  <a name="a-namebkmkplana-plan"></a><a name="BKMK_Plan"></a> Pianificazione  

-   **Pianificare e implementare i requisiti di infrastruttura**  

     Per poter distribuire i sistemi operativi, è necessario soddisfare diversi requisiti di infrastruttura, ad esempio Windows ADK, Servizi di distribuzione Windows (WDS), configurazioni supportate del disco rigido e così via. Per altre informazioni, vedere [Requisiti dell'infrastruttura per la distribuzione del sistema operativo](../plan-design/infrastructure-requirements-for-operating-system-deployment.md)  

##  <a name="a-namebkmkconfigurea-configure"></a><a name="BKMK_Configure"></a> Configura  

1.  **Preparare un'immagine d'avvio**  

     Le immagini d'avvio avviano un computer in un ambiente Windows PE (un sistema operativo minimo con componenti e servizi limitati) che può quindi installare un sistema operativo Windows completo nel computer.   Quando si distribuiscono sistemi operativi, è necessario selezionare un'immagine d'avvio da usare e distribuirla in un punto di distribuzione. Per preparare l'immagine d'avvio, vedere quanto segue:  

    -   Per altre informazioni sulle immagini d'avvio, vedere [Gestire le immagini di avvio](../get-started/manage-boot-images.md).  

    -   Per altre informazioni su come personalizzare un'immagine di avvio, vedere [Personalizzare immagini di avvio](../get-started/customize-boot-images.md).  

    -   Distribuire l'immagine d'avvio nei punti di distribuzione. Per altre informazioni, vedere [Distribuire contenuto](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content).  

2.  **Preparare un'immagine del sistema operativo**  

     L'immagine del sistema operativo contiene i file necessari per installare il sistema operativo nel computer di destinazione. Per preparare l'immagine del sistema operativo, vedere quanto segue:  

    -   Per altre informazioni su come creare un'immagine del sistema operativo, vedere [Gestire immagini del sistema operativo](../get-started/manage-operating-system-images.md).

    -   Distribuire l'immagine del sistema operativo nei punti di distribuzione. Per altre informazioni, vedere [Distribuire contenuto](../../core/servers/deploy/configure/deploy-and-manage-content.md#a-namebkmkdistributea-distribute-content).

3.  **Creare una sequenza di attività per distribuire sistemi operativi nella rete**  

     Usare una sequenza di attività per automatizzare l'installazione del sistema operativo nella rete. Usare i passaggi in [Creare una sequenza di attività per installare un sistema operativo](create-a-task-sequence-to-install-an-operating-system.md) per creare la sequenza di attività per distribuire il sistema operativo. A seconda del metodo di distribuzione scelto, potrebbero essere necessarie considerazioni aggiuntive per la sequenza di attività.  

##  <a name="a-namebkmkdeploya-deploy"></a><a name="BKMK_Deploy"></a> Distribuisci  

-   Usare uno dei metodi di distribuzione seguenti per distribuire il sistema operativo:  

    -   [Usare PXE per distribuire Windows in rete](use-pxe-to-deploy-windows-over-the-network.md)  

    -   [Usare il multicast per distribuire Windows in rete](use-multicast-to-deploy-windows-over-the-network.md)  

    -   [Creare un'immagine per un OEM in modalità produttore computer o per un rivenditore locale](create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

    -   [Usare i supporti autonomi per distribuire Windows senza usare la rete](use-stand-alone-media-to-deploy-windows-without-using-the-network.md)  

    -   [Usare supporti di avvio per distribuire Windows in rete](use-bootable-media-to-deploy-windows-over-the-network.md)  

## <a name="monitor"></a>Monitoraggio  

-   **Monitorare la distribuzione della sequenza di attività**  

     Per monitorare la distribuzione della sequenza di attività per l'installazione del sistema operativo, vedere [Monitorare le distribuzioni del sistema operativo](monitor-operating-system-deployments.md).  



<!--HONumber=Nov16_HO1-->



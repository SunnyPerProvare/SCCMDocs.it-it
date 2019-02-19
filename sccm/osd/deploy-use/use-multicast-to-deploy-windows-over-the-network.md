---
title: Usare il multicast per distribuire Windows in rete
titleSuffix: Configuration Manager
description: È possibile usare il multicast nell'ambiente di System Center Configuration Manager in modo che più computer possano scaricare simultaneamente l'immagine del sistema operativo.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 4cafb7fc-380b-41b1-b83e-045aebfb7131
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a256435c927c880363d20e6e52a22179a3271f3a
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142375"
---
# <a name="use-multicast-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Usare il multicast per distribuire Windows in rete con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Il multicast è un metodo di ottimizzazione della rete che è possibile usare nell'ambiente di System Center Configuration Manager in cui più client potrebbero scaricare la stessa immagine del sistema nello stesso momento. Quando si utilizza il multicast, l'immagine del sistema operativo viene scaricata contemporaneamente da più computer mentre il punto di distribuzione ne esegue il multicast, invece di far inviare una copia dei dati dal punto di distribuzione a ogni client in una connessione separata.  

 È possibile distribuire i sistemi operativi in rete usando il multicast negli scenari di distribuzione del sistema operativo seguenti:  

- [Aggiornare un computer esistente con una nuova versione di Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

- [Installare una nuova versione di Windows in un nuovo computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md)  

  Completare i passaggi in uno degli scenari di distribuzione del sistema operativo e quindi usare le sezioni seguenti per supportare il multicast.  

##  <a name="BKMK_Configure"></a> Configurare un punto di distribuzione per il supporto del multicast  
 Per usare il multicast quando si distribuisce il sistema operativo, è necessario configurare un punto di distribuzione per il supporto del multicast. Per altre informazioni, vedere [Configurare i punti di distribuzione per il supporto del multicast](../get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast).  

## <a name="prepare-an-operating-system-image-for-multicast-deployments"></a>Preparare un'immagine del sistema operativo per le distribuzioni multicast  
 Per configurare il pacchetto immagine del sistema operativo per il supporto del multicast, vedere [Preparare l'immagine del sistema operativo per le distribuzioni multicast](../get-started/manage-operating-system-images.md#BKMK_OSImageMulticast).  

##  <a name="BKMK_Deploy"></a> Distribuire la sequenza di attività  
 Distribuire il sistema operativo in una raccolta di destinazione. Per altre informazioni, vedere [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

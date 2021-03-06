---
title: Usare Software Center per distribuire Windows in rete
titleSuffix: Configuration Manager
description: È possibile distribuire un sistema operativo in Software Center per aggiornare un computer esistente con una nuova versione di Windows o eseguire l'aggiornamento di Windows alla versione più recente.
ms.date: 06/16/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3f6cc4366346d32934d8f69fe240f023d74ff49e
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75821444"
---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-configuration-manager"></a>Usare Software Center per distribuire Windows in rete con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

La sequenza di attività per installare un sistema operativo in Configuration Manager può essere resa disponibile in Software Center. È possibile distribuire un sistema operativo in Software Center negli scenari di distribuzione del sistema operativo seguenti:

-   [Aggiornare un computer esistente con una nuova versione di Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)

-   [Aggiornare Windows alla versione più recente](upgrade-windows-to-the-latest-version.md)

Completare i passaggi in uno degli scenari di distribuzione del sistema operativo. Usare quindi le sezioni seguenti per preparare le distribuzioni disponibili in Software Center.

## <a name="configure-deployment-settings"></a>Configurare le impostazioni di distribuzione  
Per rendere disponibile la distribuzione del sistema operativo in Software Center, configurare la distribuzione. È possibile eseguire questa distribuzione nella pagina **Impostazioni di distribuzione** della Distribuzione guidata del software o nella scheda **Impostazioni di distribuzione** nelle proprietà della distribuzione. Per l'impostazione **Rendi disponibile per** , configurare **Solo client di Configuration Manager** o **Client di Configuration Manager, supporti e PXE**. Al termine della distribuzione del sistema operativo, questo verrà visualizzato in Software Center per i membri della raccolta di destinazione.

##  <a name="BKMK_Deploy"></a> Distribuire la sequenza di attività nei computer  
Distribuire il sistema operativo in una raccolta di destinazione. Per altre informazioni, vedere [Deploy a task sequence](/sccm/osd/deploy-use/deploy-a-task-sequence). Quando si distribuiscono sistemi operativi per Software Center, è possibile specificare se la distribuzione è obbligatoria o disponibile.

-   **Distribuzione richiesta**: le distribuzioni obbligatorie renderanno disponibile il sistema operativo in Software Center, ma questo verrà avviato automaticamente in base alla pianificazione di assegnazione configurata.

-   **Distribuzione disponibile**: il sistema operativo sarà disponibile in Software Center e l'utente potrà installarlo su richiesta.

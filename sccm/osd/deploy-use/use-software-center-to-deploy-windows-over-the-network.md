---
title: Usare Software Center per distribuire Windows in rete | Microsoft Docs
description: "È possibile distribuire un sistema operativo in Software Center per aggiornare un computer esistente con una nuova versione di Windows o eseguire l&quot;aggiornamento di Windows alla versione più recente."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 919e3636-53fe-4119-ad14-2d03702b391b
caps.latest.revision: 5
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: 4c3ec20396da37d36f908af527f445a7a736e0ac


---
# <a name="use-software-center-to-deploy-windows-over-the-network-with-system-center-configuration-manager"></a>Usare Software Center per distribuire Windows in rete con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La sequenza di attività per installare un sistema operativo in System Center Configuration Manager può essere resa disponibile in Software Center. È possibile distribuire un sistema operativo in Software Center negli scenari di distribuzione del sistema operativo seguenti:  

-   [Aggiornare un computer esistente con una nuova versione di Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Aggiornare Windows alla versione più recente](upgrade-windows-to-the-latest-version.md)  

 Completare i passaggi in uno degli scenari di distribuzione del sistema operativo e quindi fare riferimento alle sezioni seguenti per preparare le distribuzioni disponibili in Software Center.  

## <a name="configure-deployment-settings"></a>Configurare le impostazioni di distribuzione  
 Quando si vuole rendere disponibile la distribuzione del sistema operativo in Software Center è necessario configurare la distribuzione in modo da rendere disponibile il sistema operativo per i client di Configuration Manager. È possibile eseguire questa configurazione nella pagina **Impostazioni di distribuzione** della Distribuzione guidata del software o nella scheda **Impostazioni di distribuzione** nelle proprietà della distribuzione.  Per l'impostazione **Rendi disponibile per** , configurare **Solo client di Configuration Manager** o **Client di Configuration Manager, supporti e PXE**. Al termine della distribuzione del sistema operativo, questo verrà visualizzato in Software Center per i membri della raccolta di destinazione.  

##  <a name="a-namebkmkdeploya-deploy-the-task-sequence-to-computers"></a><a name="BKMK_Deploy"></a> Distribuire la sequenza di attività nei computer  
 Distribuire il sistema operativo in una raccolta di destinazione. Per altre informazioni, vedere [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS). Quando si distribuiscono sistemi operativi per Software Center, è possibile specificare se la distribuzione è obbligatoria o disponibile.  

-   **Distribuzione obbligatoria**: le distribuzioni obbligatorie renderanno disponibile il sistema operativo in Software Center, ma questo verrà avviato automaticamente in base alla pianificazione di assegnazione configurata.  

-   **Distribuzione disponibile**: il sistema operativo sarà disponibile in Software Center e l'utente potrà installarlo su richiesta.  



<!--HONumber=Dec16_HO3-->



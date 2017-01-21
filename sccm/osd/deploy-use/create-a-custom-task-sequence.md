---
title: "Creare una sequenza di attività personalizzata | Microsoft Docs"
description: "Modificare una sequenza di attività personalizzate in System Center Configuration Manager per aggiungere passaggi alla sequenza di attività."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
caps.latest.revision: 6
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 74341fb60bf9ccbc8822e390bd34f9eda58b4bda
ms.openlocfilehash: 03c844084c72fc52806123d9f4c11a410a3ec775


---
# <a name="create-a-custom-task-sequence-with-system-center-configuration-manager"></a>Creare una sequenza di attività personalizzata con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Quando si crea una sequenza di attività personalizzata in System Center Configuration Manager, la sequenza di attività non contiene passaggi. Dopo averla creata è necessario modificarla e aggiungervi i passaggi della sequenza di attività desiderati.  

##  <a name="a-namebkmkcustomtsa-create-a-custom-task-sequence"></a><a name="BKMK_CustomTS"></a> Creare una sequenza di attività personalizzata  
 Attenersi alla procedura seguente per creare una sequenza di attività personalizzata.  

#### <a name="to-create-a-custom-task-sequence"></a>Per creare una sequenza di attività personalizzata  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**, quindi fare clic su **Sequenze attività**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea sequenza di attività** per avviare la Creazione guidata della sequenza di attività.  

4.  Nella pagina **Crea una nuova sequenza di attività** selezionare **Crea una nuova sequenza di attività personalizzata**.  

5.  Nella pagina **Informazioni sequenza di attività** specificare un nome, una descrizione e un'immagine di avvio facoltativa per la sequenza di attività. Quindi completare la procedura guidata.  

 Dopo aver completato la Creazione guidata della sequenza di attività, Configuration Manager aggiunge la sequenza di attività personalizzata al nodo **Sequenze attività**. È ora possibile modificare questa sequenza di attività per aggiungere passaggi della sequenza di attività.  

 Per un elenco dei passaggi della sequenza di attività disponibili, vedere [Passaggi della sequenza di attività](../understand/task-sequence-steps.md).  

 Per altre informazioni su come modificare una sequenza di attività, vedere [Modificare una sequenza di attività](manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

 Le sequenze di attività verranno usate principalmente per automatizzare le attività di distribuzione del sistema operativo, ma è possibile creare una sequenza di attività personalizzata per automatizzare diverse attività. Per altre informazioni, vedere [Creare una sequenza di attività per distribuzioni non di sistema operativo](create-a-task-sequence-for-non-operating-system-deployments.md).  

 ## <a name="next-steps"></a>Passaggi successivi
 [Distribuire la sequenza di attività](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)



<!--HONumber=Dec16_HO3-->



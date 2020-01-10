---
title: Creare una sequenza di attività personalizzata
titleSuffix: Configuration Manager
description: Modificare una sequenza di attività personalizzata in Configuration Manager per aggiungere passaggi alla sequenza di attività.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9800a66-7541-47ca-8276-da8ef6cb6d1b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8ea942cca00852ae828c7574b0a61b606e4b331d
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75825524"
---
# <a name="create-a-custom-task-sequence-with-configuration-manager"></a>Creare una sequenza di attività personalizzata con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Quando si crea una sequenza di attività personalizzata in Configuration Manager, la sequenza di attività non contiene passaggi. Dopo averla creata, modificarla e aggiungere i passaggi della sequenza di attività necessari.  

## <a name="BKMK_CustomTS"></a> Creare una sequenza di attività personalizzata

Seguire questa procedura per creare una sequenza di attività personalizzata:

1. Nella console di Configuration Manager accedere all'area di lavoro **Raccolta software**, espandere **Sistemi operativi** e quindi selezionare il nodo **Sequenze di attività**.  

1. Nella scheda **Home** della barra multifunzione nel gruppo **Crea** selezionare **Crea sequenza di attività**. Questa azione avvia la Creazione guidata della sequenza di attività.  

1. Nella pagina **Crea una nuova sequenza di attività** selezionare **Crea una nuova sequenza di attività personalizzata**.  

1. Nella pagina **informazioni sequenza di attività** specificare:

    - Un nome per la sequenza di attività
    - Una descrizione della sequenza di attività
    - Un'immagine di avvio facoltativa per la sequenza di attività da usare

Dopo aver completato la Creazione guidata della sequenza di attività, Configuration Manager aggiunge la sequenza di attività personalizzata al nodo **Sequenze attività**. È ora possibile modificare questa sequenza di attività per aggiungere passaggi della sequenza di attività.  

Per un elenco dei passaggi della sequenza di attività disponibili, vedere [Passaggi della sequenza di attività](/sccm/osd/understand/task-sequence-steps).  

Per altre informazioni su come modificare una sequenza di attività, vedere [Usare l'editor delle sequenze di attività](/sccm/osd/understand/task-sequence-editor).  

Spesso si useranno le sequenze attività per automatizzare le attività per la distribuzione del sistema operativo, ma è possibile creare una sequenza di attività personalizzata per automatizzare diversi tipi di attività. Per altre informazioni, vedere [Creare una sequenza di attività per distribuzioni non di sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments).  

## <a name="next-steps"></a>Passaggi successivi

[Distribuire la sequenza di attività](/sccm/osd/deploy-use/deploy-a-task-sequence)

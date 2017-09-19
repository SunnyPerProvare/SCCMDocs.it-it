---
title: Classificare automaticamente i dispositivi in raccolte | Microsoft Docs
description: Classificare automaticamente i dispositivi in raccolte con System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
caps.latest.revision: "5"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 0de7a3d4183fb00f444a27c45d178141dc4e9375
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/15/2017
---
# <a name="automatically-categorize-devices-into-collections-with-system-center-configuration-manager"></a>Classificare automaticamente i dispositivi in raccolte con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile creare categorie di dispositivi da usare per inserire automaticamente i dispositivi nelle raccolte di dispositivi quando si usa Configuration Manager con Microsoft Intune. Gli utenti dovranno quindi scegliere una categoria di dispositivi quando eseguono la registrazione di un dispositivo in Intune. È possibile modificare la categoria di un dispositivo dalla console di Configuration Manager.

> [!IMPORTANT]  
    >  Questa funzionalità può essere usata con la versione di Microsoft Intune di **giugno 2016** e versioni successive. Verificare che l'installazione sia aggiornata a questa versione prima di tentare queste procedure.

## <a name="create-device-categories"></a>Creare categorie di dispositivi

1.  Passare a **Asset e conformità** > **Panoramica** > **Raccolte dispositivi**.
2.  Nella scheda **Home**, nel gruppo **Raccolte di dispositivi**, scegliere **Gestire le categorie di dispositivi**.
3.  Creare, modificare o rimuovere le categorie.

## <a name="associate-a-collection-with-a-device-category"></a>Associare una raccolta a una categoria di dispositivo

Quando si associa una raccolta a una categoria di dispositivi, tutti i dispositivi in tale categoria verranno aggiunti alla raccolta. Non è possibile aggiungere una regola categoria di dispositivi a una raccolta predefinita come **Tutti i sistemi**.

1.  Nella scheda **Regole di appartenenza** della finestra di dialogo **Proprietà** per una raccolta di dispositivi scegliere **Aggiungi regola** > **Regola categoria di dispositivi**.
2.  Nella finestra di dialogo **Seleziona le categorie di dispositivi** selezionare una o più categorie di dispositivi che saranno applicate a tutti i dispositivi della raccolta.

## <a name="change-the-category-of-a-device"></a>Cambiare la categoria di un dispositivo

1.  In **Asset e conformità** > **Panoramica** > **Dispositivi** selezionare un dispositivo nell'elenco **Dispositivi**.
2.  Nella scheda **Home** nel gruppo **Dispositivo** scegliere **Modifica categoria**.
3.  Scegliere una categoria e quindi scegliere **OK**.

## <a name="view-which-category-a-device-belongs-to"></a>Visualizzare la categoria a cui un dispositivo appartiene

In **Asset e conformità** > **Panoramica** > **Dispositivi**, nell'elenco **Dispositivi** la categoria è visualizzata nella colonna **Categoria del dispositivo**.

Se la colonna **Categoria di dispositivi** non è visualizzata, fare clic con il pulsante destro del mouse sull'intestazione di una delle colonne nell'elenco **Dispositivi** (ad esempio **Nome**), quindi selezionare **Categoria di dispositivi**.

Se si assegna un dispositivo a una categoria e successivamente si elimina la categoria, il report **Elenco dei dispositivi registrati per utente in Microsoft Intune** mostrerà un GUID nella colonna **Categoria di dispositivi** anziché un nome di categoria.

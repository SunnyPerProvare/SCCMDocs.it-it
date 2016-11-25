---
title: Classificare automaticamente i dispositivi in raccolte | System Center Configuration Manager
description: Classificare automaticamente i dispositivi in raccolte con System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
caps.latest.revision: 5
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 6e1e8c1da1209be03d4a1377dcc0c9ce9478a216

---
# <a name="automatically-categorize-devices-into-collections-with-system-center-configuration-manager"></a>Classificare automaticamente i dispositivi in raccolte con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile creare categorie di dispositivi da usare per inserire automaticamente i dispositivi nelle raccolte di dispositivi quando si usa Configuration Manager con Microsoft Intune. Agli utenti verrà quindi richiesto di scegliere una categoria di dispositivo quando eseguono la registrazione di un dispositivo in Intune. È anche possibile modificare la categoria di un dispositivo dalla console di Configuration Manager.

> [!IMPORTANT]  
    >  Questa funzionalità può essere usata con la versione di Microsoft Intune di **giugno 2016**. Verificare che l'installazione sia aggiornata a questa versione prima di tentare queste procedure.

## <a name="create-device-categories"></a>Creare categorie di dispositivi

1.  Nell'area di lavoro **Asset e conformità** della console di Configuration Manager espandere **Panoramica** e fare clic su **Raccolte di dispositivi**.
2.  Sulla scheda **Home**, nel gruppo **Raccolte di dispositivi**, fare clic su **Gestire le categorie di dispositivi**.
3.  Nella finestra di dialogo **Gestire le categorie di dispositivi** è possibile creare, modificare o rimuovere le categorie.

## <a name="associate-a-collection-with-a-device-category"></a>Associare una raccolta a una categoria di dispositivo

Quando si associa una raccolta a una categoria di dispositivo, tutti i dispositivi della categoria specificata verranno aggiunti alla raccolta.

> [!IMPORTANT]  
    >  Non è possibile aggiungere una regola categoria di dispositivi a una raccolta predefinita come **Tutti i sistemi**.

1.  Sulla scheda **Regole di appartenenza** della finestra di dialogo **Proprietà** per una raccolta di dispositivi fare clic su **Aggiungi regola** > **Regola categoria di dispositivi**.
2.  Nella finestra di dialogo **Seleziona le categorie di dispositivi** selezionare una o più categorie di dispositivi che saranno applicate a tutti i dispositivi della raccolta.
3.  Chiudere la finestra di dialogo **Seleziona le categorie di dispositivi** e la finestra di dialogo della proprietà della raccolta.


## <a name="change-the-category-of-a-device"></a>Cambiare la categoria di un dispositivo

1.  Nell'area di lavoro **Asset e conformità** della console di Configuration Manager espandere **Panoramica** e fare clic su **Dispositivi**.
2.  Selezionare un dispositivo nell'elenco **Dispositivi** quindi, sulla scheda **Home**, nel gruppo **Dispositivo**, fare clic su **Cambia categoria**.
3.  Nella finestra di dialogo **Modifica categoria di dispositivi** scegliere la categoria da applicare al dispositivo e fare clic su **OK**.

## <a name="view-which-category-a-device-belongs-to"></a>Visualizzare la categoria a cui un dispositivo appartiene

1.  Nell'area di lavoro **Asset e conformità** della console di Configuration Manager espandere **Panoramica** e fare clic su **Dispositivi**.
2.  Nell'elenco **Dispositivi** la categoria è visualizzata nella colonna **Categoria di dispositivi**.
> [!TIP]  
    >  Se la colonna **Categoria di dispositivi** non è visualizzata, fare clic con il pulsante destro del mouse sull'intestazione di una delle colonne nell'elenco **Dispositivi** (ad esempio **Nome**), quindi selezionare **Categoria di dispositivi**.

Se si assegna un dispositivo a una categoria e successivamente si elimina la categoria, il report **Elenco dei dispositivi registrati per utente in Microsoft Intune** mostrerà un GUID nella colonna **Categoria di dispositivi** anziché un nome di categoria.



<!--HONumber=Nov16_HO1-->



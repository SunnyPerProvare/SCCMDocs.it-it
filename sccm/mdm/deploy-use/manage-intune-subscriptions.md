---
title: Gestire una sottoscrizione di Intune
titleSuffix: Configuration Manager
description: Gestire una sottoscrizione di Intune associata a System Center Configuration Manager.
ms.custom: na
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b494767-68c1-47b1-9a86-591bff0ad491
caps.latest.revision: "18"
caps.handback.revision: "0"
author: dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: a6bb27adeddc366526df699b69e95c6e7d6482ae
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="manage-an-intune-subscription-associated-with-system-center-configuration-manager"></a>Gestire una sottoscrizione di Intune associata a System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Se si aggiunge una sottoscrizione di valutazione o a pagamento di Microsoft Intune in Configuration Manager e successivamente è necessario passare a una sottoscrizione di Intune diversa, eliminare sia la **sottoscrizione a Microsoft Intune** che il **punto di connessione del servizio** dalla console di Configuration Manager prima di aggiungere una nuova sottoscrizione.

> [!NOTE]
> È possibile configurare una sola sottoscrizione di Intune alla volta nella gestione dei dispositivi mobili ibrida.

## <a name="how-to-delete-an-intune-subscription-from-configuration-manager"></a>Come eliminare una sottoscrizione di Intune da Configuration Manager

> [!IMPORTANT]
>  Tutto il contenuto, tra cui le registrazioni utente, i criteri e le distribuzioni di app configurate per i dispositivi gestiti dalla sottoscrizione a Intune, viene rimosso quando si elimina la sottoscrizione.

1.  Nella console di Configuration Manager passare ad **Amministrazione** > **Panoramica** > **Servizi cloud** > **Sottoscrizioni a Microsoft Intune**.

2.  Fare clic con il pulsante destro del mouse su **Sottoscrizione a Microsoft Intune** e fare clic su **Elimina**.

3.   Nella procedura guidata fare clic su **Remove Microsoft Intune Subscription from Configuration Manager** (Rimuovi sottoscrizione a Microsoft Intune da Configuration Manager), selezionare **Avanti** e fare clic ancora su **Avanti** per rimuovere la sottoscrizione.


## <a name="how-to-remove-the-service-connection-point-role"></a>Come rimuovere il ruolo del punto di connessione del servizio

1.  Passare ad **Amministrazione** > **Panoramica** > **Configurazione del sito** > **Server e ruoli del sistema del sito**.

2.  Selezionare il server che ospita il ruolo **Punto di connessione del servizio**.

3.  Nell'elenco **Ruoli sistema del sito** selezionare **Punto di connessione del servizio** e quindi fare clic su **Rimuovi ruolo** nella barra multifunzione. Confermare la rimozione del ruolo. Il punto di connessione del servizio viene eliminato.

È ora possibile creare un nuovo punto di connessione del servizio, aggiungere una nuova sottoscrizione di Intune a Configuration Manager e impostare Configuration Manager come autorità MDM.

## <a name="how-to-change-mdm-authority-to-intune"></a>Come cambiare l'autorità di gestione dei dispositivi mobili in Intune
A partire da Configuration Manager versione 1610 e Microsoft Intune versione 1705, è possibile cambiare l'autorità MDM senza dover contattare il supporto Microsoft e senza dover annullare e ripetere la registrazione dei dispositivi gestiti esistenti. Per altre informazioni, vedere [Cambiare l'autorità MDM](/sccm/mdm/deploy-use/change-mdm-authority).

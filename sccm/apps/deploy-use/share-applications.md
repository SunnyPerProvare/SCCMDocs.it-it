---
title: Condividere le applicazioni nel Software Center
titleSuffix: Configuration Manager
description: Condividere un collegamento a un'applicazione in Software Center in System Center Configuration Manager.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e7a700482dad9f1ab2e41456596423fa23c15434
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "62198754"
---
# <a name="share-an-application-from-software-center"></a>Condividere un'applicazione da Software Center

*Si applica a: System Center Configuration Manager (Current Branch)* <!-- 1706 -->

È possibile copiare un collegamento ipertestuale in un'applicazione in Software Center tramite il pulsante ![Condividi](media/share15.png) **Condividi** nella vista Dettagli applicazione. È possibile condividere collegamenti ipertestuali solo per le applicazioni. Se un'applicazione non è più disponibile, il collegamento ipertestuale apre una finestra con un messaggio che informa dell'indisponibilità dell'applicazione.

1. Scegliere **Applicazioni** e quindi scegliere l'applicazione.
2. Fare clic sul pulsante ![Condividi](media/share15.png) **Condividi**.
3. Fare clic su **Copia** nella finestra.
4. Incollare l'URL in un messaggio di posta elettronica per condividere l'applicazione.  

> [!TIP]  
>  Per creare un collegamento in un messaggio di posta elettronica di Outlook, premere **CTRL** + **K** e quindi incollare l'URL.  
>  
> Per impostazione predefinita, Outlook visualizza un avviso di sicurezza per il protocollo Software Center quando il destinatario fa clic sul collegamento. Evitare questo problema nel proprio ambiente mediante l'aggiunta di una chiave di protocollo attendibile al registro. Ad esempio: `HKCU\Software\Policies\Microsoft\Office\16.0\Common\Security\Trusted Protocols\All Applications\softwarecenter:`  

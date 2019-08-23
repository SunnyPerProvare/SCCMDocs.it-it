---
title: Come reimpostare l'account
titleSuffix: Configuration Manager
description: Informazioni su come reimpostare l'account di analisi del desktop.
ms.date: 08/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 884d4864-950b-4139-b778-d5368e1f6ef2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3eb3f08c7c1358343b4bf06aef80ba84a5fb8d8c
ms.sourcegitcommit: 2b07fb7e2a17b5624429e81f9b6b9b3223b6f16d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/16/2019
ms.locfileid: "69536780"
---
# <a name="how-to-reset-your-account"></a>Come reimpostare l'account

<!-- 3733897 -->

> [!Note]  
> Queste informazioni si riferiscono a un servizio di anteprima che può essere modificato in modo sostanziale prima del rilascio commerciale. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Se si configura analisi desktop nell'ambiente, ma si vuole ricominciare con l'onboarding e la registrazione, usare questo processo per reimpostare l'account.

## <a name="prerequisites"></a>Prerequisiti

Solo un **amministratore globale** può reimpostare l'account nell'portale di Azure.

## <a name="behaviors"></a>comportamenti

- Questo processo non modifica gli utenti, le app o le autorizzazioni di Azure AD esistenti

- Se si sceglie di aggiungere una nuova area di lavoro, nessuno degli input utente seguenti negli asset viene mantenuto:
    - Importanza
    - Proprietario
    - Decisione di aggiornamento
    - Note sulla correzione

## <a name="process"></a>Process

1. Aprire il [portale di analisi del desktop](https://aka.ms/desktopanalytics) in Microsoft 365 gestione dei dispositivi come utente con il ruolo di **amministratore globale** .

1. Nel menu **Impostazioni globali** selezionare **servizi connessi**. Nella sezione registrazione dei dispositivi selezionare l'opzione per la **reimpostazione**.

1. Se si decide di continuare, l'account viene reimpostato. È necessario configurare di nuovo desktop Analytics.

## <a name="next-steps"></a>Passaggi successivi

Dopo la reimpostazione, aggiornare la pagina e rieseguire il processo di onboarding. Per altre informazioni, vedere [How to set up desktop Analytics](/sccm/desktop-analytics/set-up).

In caso di problemi durante questo processo, contattare supporto tecnico Microsoft per ulteriore assistenza.
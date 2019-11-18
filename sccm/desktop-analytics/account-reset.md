---
title: Come reimpostare l'account
titleSuffix: Configuration Manager
description: Informazioni su come reimpostare l'account di Desktop Analytics.
ms.date: 08/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 884d4864-950b-4139-b778-d5368e1f6ef2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 34bb53bf9819149c989996a950f3b13329e4eef3
ms.sourcegitcommit: b64ed4a10a90b93a5bd5454b6efafda90ad45718
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72386794"
---
# <a name="how-to-reset-your-account"></a>Come reimpostare l'account

<!-- 3733897 -->

Se si configura Desktop Analytics nell'ambiente ma si vuole ricominciare con l'onboarding e la registrazione, usare questo processo per reimpostare l'account.

## <a name="prerequisites"></a>Prerequisiti

Solo un **amministratore globale** può reimpostare l'account nel portale di Azure.

## <a name="behaviors"></a>Comportamenti

- Questo processo non modifica gli utenti, le app o le autorizzazioni di Azure AD esistenti

- Se si sceglie di aggiungere una nuova area di lavoro, nessuno degli input utente seguenti viene mantenuto nelle risorse:
    - Importanza
    - Owner
    - Decisione di aggiornamento
    - Note di rimedio

## <a name="process"></a>Processo

1. Aprire il [portale di Desktop Analytics](https://aka.ms/desktopanalytics) in Gestione dispositivi Microsoft 365 come utente con il ruolo **Amministratore globale**.

1. Nel menu **Impostazioni globali** selezionare **Servizi connessi**. Nella sezione relativa alla registrazione dei dispositivi selezionare l'opzione **Reimposta**.

1. Se si decide di continuare, l'account viene reimpostato e sarà necessario riconfigurare Desktop Analytics.

## <a name="next-steps"></a>Passaggi successivi

Dopo la reimpostazione, aggiornare la pagina e rieseguire il processo di onboarding. Per altre informazioni, vedere [Come configurare Desktop Analytics](/sccm/desktop-analytics/set-up).

In caso di problemi durante il processo, contattare il supporto tecnico Microsoft per assistenza.

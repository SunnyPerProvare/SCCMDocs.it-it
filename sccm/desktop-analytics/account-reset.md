---
title: Come reimpostare l'account
titleSuffix: Configuration Manager
description: Informazioni su come reimpostare l'account di Desktop Analytics.
ms.date: 08/16/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 884d4864-950b-4139-b778-d5368e1f6ef2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d75f653029fdccacec9d3a7d83c55489f7fab509
ms.sourcegitcommit: ccc3c929b5585c05d562020e68044de7d7e11c6a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2020
ms.locfileid: "80597688"
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
    - Proprietario
    - Decisione di aggiornamento
    - Note di rimedio

## <a name="process"></a>Processo

1. Aprire il [portale di Desktop Analytics](https://aka.ms/desktopanalytics) in Gestione dispositivi Microsoft 365 come utente con il ruolo **Amministratore globale**.

1. Nel menu **Impostazioni globali** selezionare **Servizi connessi**. Nella sezione relativa alla registrazione dei dispositivi selezionare l'opzione **Reimposta**.

1. Se si decide di continuare, l'account viene reimpostato e sarà necessario riconfigurare Desktop Analytics.

## <a name="next-steps"></a>Passaggi successivi

Dopo la reimpostazione, aggiornare la pagina e rieseguire il processo di onboarding. Per altre informazioni, vedere [Come configurare Desktop Analytics](/sccm/desktop-analytics/set-up).

In caso di problemi durante il processo, contattare il supporto tecnico Microsoft per assistenza.

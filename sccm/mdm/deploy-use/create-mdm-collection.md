---
title: Creare una raccolta MDM
titleSuffix: Configuration Manager
description: Creare una raccolta MDM usando Configuration Manager.
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: d1b4337f-85e8-45e6-8bbe-9f18b49041c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8776f6f77e716bdd4b921eb82181f8566ddace24
ms.sourcegitcommit: 7f64c5fb3e9fa3dba006af618b1f1ceaf61a99f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/28/2019
ms.locfileid: "75521171"
---
# <a name="create-an-mdm-collection-with-configuration-manager-and-microsoft-intune"></a>Creare una raccolta MDM con Configuration Manager e Microsoft Intune

*Si applica a: Configuration Manager (Current Branch)*

È necessaria una raccolta utenti di Configuration Manager per specificare gli utenti che possono registrare i dispositivi nella gestione. È possibile usare solo le raccolte utenti (invece delle raccolte di dispositivi) perché le licenze di Intune vengono assegnate agli utenti.

> [!NOTE]
> Per registrare i dispositivi con Intune, non è necessario assegnare licenze agli utenti nell'interfaccia di amministrazione di Microsoft 365 o nel portale di Azure Active Directory. Tutto ciò che è richiesto è includere gli utenti in una raccolta che venga associata alla sottoscrizione di Intune (in un [passaggio successivo](configure-intune-subscription.md)).

A scopo di test è possibile impostare una **Regola diretta** e aggiungere utenti specifici che possono registrare i dispositivi. Nella console di Configuration Manager scegliere **Asset e conformità** > **Raccolte utenti**, fare clic sulla scheda **Home** > gruppo **Crea** e quindi fare clic su **Crea raccolta utenti**. Per definire gli utenti per una distribuzione più ampia è necessario usare **Regole di query**. Per altre informazioni sulle raccolte, vedere [Come creare le raccolte in System Center Configuration Manager](https://technet.microsoft.com/library/mt629371.aspx).

![Per creare una raccolta utenti per la gestione dei dispositivi mobili](../media/mdm-create-user-collection.png)

> [!div class="button"]
> [Passaggio successivo >](confirm-dns.md)

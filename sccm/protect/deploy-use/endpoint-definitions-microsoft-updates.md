---
title: Definizioni malware di Endpoint Protection da una condivisione di rete
titleSuffix: Configuration Manager
description: Informazioni su come abilitare il download delle definizioni malware di Endpoint Protection da Microsoft Updates per Configuration Manager.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: d401eea9b3556eae2ad8b3c26eda5a243fc07211
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53419139"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-microsoft-updates-for-configuration-manager"></a>Abilitare le definizioni malware di Endpoint Protection da scaricare da Microsoft Updates per Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


 Quando si sceglie di scaricare gli aggiornamenti delle definizioni da Microsoft Update, i client controlleranno il sito Microsoft Update con la frequenza definita nella sezione **Aggiornamenti delle definizioni** della finestra di dialogo dei criteri antimalware.

 Questo metodo può essere utile se il client non ha connettività al sito di Configuration Manager o se si vuole che gli utenti possano avviare gli aggiornamenti delle definizioni.

> [!IMPORTANT]
>  Per poter usare questo metodo per scaricare gli aggiornamenti delle definizioni, i client devono avere accesso a Microsoft Update in Internet.

## <a name="using-the-microsoft-malware-protection-center-to-download-definitions"></a>Uso di Microsoft Malware Protection Center per scaricare le definizioni
 È possibile configurare i client per scaricare gli aggiornamenti delle definizioni da Microsoft Malware Protection Center. Questa opzione è usata dai client di Endpoint Protection per scaricare gli aggiornamenti delle definizioni se non sono riusciti a scaricare gli aggiornamenti da un'altra origine. Questo metodo di aggiornamento può essere utile se si verifica un problema con l'infrastruttura di Configuration Manager che impedisce il recapito degli aggiornamenti.

> [!IMPORTANT]
>  Per poter usare questo metodo per scaricare gli aggiornamenti delle definizioni, i client devono avere accesso a Microsoft Update in Internet.
> 
> 
> [!div class="button"]
> [Passaggio successivo >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Indietro >](endpoint-configure-alerts.md)

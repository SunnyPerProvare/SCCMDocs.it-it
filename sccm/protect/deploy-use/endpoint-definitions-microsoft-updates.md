---
title: Definizioni di malware per Endpoint Protection da una condivisione di rete| System Center Configuration Manager
description: Informazioni su come abilitare il download delle definizioni malware di Endpoint Protection da Microsoft Updates per Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ab7626ae-d4bf-4ca6-ab25-c61f96800a02
caps.latest.revision: 21
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 23c19256f3f38d44c57e5d3d25b36ceb023f3214


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


> [!div class="button"]
[Passaggio successivo >](endpoint-antimalware-policies.md)

> [!div class="button"]
[Indietro >](endpoint-configure-alerts.md)



<!--HONumber=Nov16_HO1-->


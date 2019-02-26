---
title: Eseguire la migrazione da MDM ibrido
titleSuffix: Configuration Manager
description: Soluzione MDM ibrida è deprecata, versione autonoma di Intune è obbligatoria per la co-gestione.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 456f32d5-8590-499f-a54d-d00618bc61f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 84625c12c9cac643fe5a895c066632f44ffeacdc
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56755362"
---
# <a name="migrate-from-hybrid-mdm-for-co-management"></a>Eseguire la migrazione dalla soluzione MDM ibrida per la co-gestione

Gestione di dispositivi mobili (MDM) ibrida è una funzionalità deprecata. Il supporto per la soluzione MDM ibrida termina 1 settembre 2019. Per altre informazioni, vedere [MDM ibrida con Configuration Manager e Microsoft Intune](/sccm/mdm/understand/hybrid-mobile-device-management).

Versione autonoma di Intune è la topologia di distribuzione consigliato ed è obbligatorio per la co-gestione. Se si desidera abilitare la co-gestione, eseguire la migrazione da una configurazione ibrida di Intune a Intune autonomo. 

Nel video seguente, principal program manager per Andrew McMurray e senior product marketing manager Mayunk Jain discutere e demo per la migrazione dalla soluzione MDM ibrida:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Moving-From-Hybrid-MDM-To-Microsoft-Intune/player]



## <a name="how-to-do-it"></a>Come eseguire questa operazione

La migrazione a Intune autonomo è ottimale quando usare un approccio per fasi. Con una migrazione graduale, si sposta un piccolo subset di utenti e dispositivi mentre la maggior parte degli utenti e dispositivi vengono ancora gestita con MDM ibrida. Dopo aver verificato che la migrazione abbia esito positivo, è possibile iniziare la migrazione di più risorse a Intune.

Per iniziare la migrazione, usare il [strumento di importazione di dati di Microsoft Intune](/sccm/mdm/deploy-use/migrate-import-data) per raccogliere e automatizzare il processo di creazione di oggetti da Configuration Manager nel proprio tenant di Intune autonomo. Successivamente, modificare l'autorità MDM per un set specifico di utenti e la verifica delle funzionalità nella versione autonoma di Intune. Quando viene eseguita questa verifica, cambiare l'autorità MDM a Intune autonomo per tutti gli utenti.

> [!Important]  
> Se si usa l'accesso condizionale in locale in Configuration Manager, questa funzionalità richiede attualmente ibrida di Intune.  

Per altre informazioni su questo processo di migrazione, vedere [eseguire la migrazione di dispositivi e utenti dalla soluzione MDM ibrida a Intune autonomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).



## <a name="case-studies"></a>Case study

Microsoft IT spostato di recente 130.000 utenti dalla soluzione ibrida di Intune a Intune autonomo in tre mesi. Per altre informazioni, vedere [modo in cui Microsoft Usa l'accesso condizionale - Endpoint Zone 1812](https://youtu.be/offk-KH7eIA?t=651). In questo video è una conversazione tra Microsoft corporate vice president Brad Anderson e Microsoft chief information security officer Bret Arsenault, chi aver personalmente la migrazione. 

Una grande azienda farmaceutica spostato 10.000 utenti dalla soluzione ibrida di Intune a Intune autonomo all'interno di alcune settimane.

Una grande società di consulenza IT in India 40.000 gli utenti migrati dalla soluzione ibrida di Intune a Intune autonomo in meno di un mese.



## <a name="contact-fasttrack"></a>Contattare FastTrack

Se occorre assistenza per la migrazione dalla soluzione MDM ibrida in qualsiasi punto del processo, andare al [Microsoft FastTrack](https://Microsoft.com/FastTrack/), accedi e richiedere assistenza. 

Per altre informazioni, vedere [assistenza dal FastTrack](/sccm/comanage/quickstart-fasttrack). 


---
title: Eseguire la migrazione da MDM ibrido
titleSuffix: Configuration Manager
description: La soluzione MDM ibrida è deprecata. Per la co-gestione è richiesta la versione autonoma di Intune.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 456f32d5-8590-499f-a54d-d00618bc61f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a2e0f9d803b01b423fb131d826a638b58de221d7
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75816956"
---
# <a name="migrate-from-hybrid-mdm-for-co-management"></a>Eseguire la migrazione dalla gestione ibrida dei dispositivi mobili (MDM) per la co-gestione

La funzionalità MDM ibrida è deprecata. Il supporto per le soluzioni MDM ibride termina 1 settembre 2019. Per altre informazioni, vedere [Soluzione MDM ibrida con Configuration Manager e Intune](/sccm/mdm/understand/hybrid-mobile-device-management).

La versione autonoma di Intune è la topologia di distribuzione consigliata ed è obbligatoria per la co-gestione. Se si vuole abilitare la co-gestione, eseguire la migrazione da una configurazione ibrida di Intune a Intune autonomo. 

Nel video seguente il Principal Program Manager Andrew McMurray e il Senior Product Marketing Manager Mayunk Jain trattano e illustrano la migrazione dalla soluzione MDM ibrida:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Moving-From-Hybrid-MDM-To-Microsoft-Intune/player]



## <a name="how-to-do-it"></a>Come procedere

Per una migrazione ottimale a Intune autonomo è consigliabile usare un approccio in più fasi. Con questo approccio, si sposta un piccolo subset di utenti e dispositivi mentre la maggior parte degli utenti e dei dispositivi viene ancora gestita con la soluzione MDM ibrida. Dopo aver verificato l'esito positivo della migrazione, è possibile avviare la migrazione di ulteriori risorse a Intune.

Per iniziare la migrazione, usare lo [strumento Microsoft Intune Data Importer](/sccm/mdm/deploy-use/migrate-import-data) per raccogliere e automatizzare il processo per ricreare gli oggetti da Configuration Manager nel proprio tenant di Intune autonomo. Successivamente, modificare l'autorità MDM per un set specifico di utenti e testare le funzionalità nella versione autonoma di Intune. Dopo aver completato questa verifica, impostare Intune autonomo come autorità MDM per tutti gli utenti.

> [!Important]  
> Se si usa l'accesso condizionale in locale in Configuration Manager, questa funzionalità richiede attualmente Intune ibrido.  

Per altre informazioni su questo processo di migrazione, vedere [Eseguire la migrazione di dispositivi e utenti dalla soluzione MDM ibrida alla versione autonoma di Intune](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).



## <a name="case-studies"></a>Case study

Microsoft IT ha spostato di recente 130.000 utenti da Intune ibrido a Intune autonomo in tre mesi. Per altre informazioni, vedere [How Microsoft uses Conditional Access - Endpoint Zone 1812](https://youtu.be/offk-KH7eIA?t=651) (Come viene usato l'accesso condizionale a Microsoft - Endpoint Zone 1812). Questo video è una conversazione tra il vicepresidente di Microsoft Brad Anderson e il Chief Information Security Officer di Microsoft Bret Arsenault, che ha supervisionato personalmente la migrazione. 

Una grande azienda farmaceutica ha spostato 10.000 utenti da Intune ibrido a Intune autonomo in poche settimane.

Una grande società di consulenza IT in India ha completato la migrazione di 40.000 utenti da Intune ibrido a Intune autonomo in meno di un mese.



## <a name="contact-fasttrack"></a>Contattare FastTrack

Se è necessaria assistenza per la migrazione da una soluzione MDM ibrida in qualsiasi punto del processo, passare a [Microsoft FastTrack](https://Microsoft.com/FastTrack/), eseguire l'accesso e richiedere assistenza. 

Per altre informazioni, vedere [Ottenere assistenza da FastTrack](/sccm/comanage/quickstart-fasttrack). 


---
title: Scegliere Intune autonomo o MDM per dispositivi ibridi | Microsoft Docs
description: Scegliere se distribuire una gestione di dispositivi mobili ibridi con Intune e Configuration Manager o se eseguire Intune autonomamente.
ms.custom: na
ms.date: 07/18/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: 10
author: dougeby
ms.author: dougeby
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 648bc6b96aa5ccc834442a962e6d5b5125f88bb5
ms.openlocfilehash: ddb6d47e5dba4fddd6fa811d83b1bf0c91ad26f9
ms.contentlocale: it-it
ms.lasthandoff: 07/19/2017

---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>Scegliere tra Microsoft Intune autonomo e la gestione di dispositivi mobili ibridi con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Una delle domande più frequenti sulla Gestione di dispositivi mobili con Microsoft Intune è: "È preferibile integrare Intune e Configuration Manager (gestione dei dispositivi mobili ibrida) o eseguire Intune autonomo nella configurazione che prevede solo il cloud?" Per rispondere a questa domanda, è necessario confrontare attentamente le due opzioni.

## <a name="intune-standalone"></a>Intune autonomo
Intune autonomo è la topologia di distribuzione consigliata da Microsoft. Intune autonomo è una soluzione di gestione di dispositivi mobili solo nel cloud gestita tramite una console Web a cui è possibile accedere da qualsiasi parte del mondo. I data center di Intune si trovano in America del Nord, in Europa e in Asia. Dato che Intune è un servizio cloud, è possibile distribuire la gestione Intune nei dispositivi in un intervallo di tempo relativamente breve.

I clienti trovano in genere più veloce e semplice distribuire la topologia autonoma, poiché non ci sono dipendenze per i componenti locali. Intune autonomo ora fa parte della piattaforma cloud di Microsoft Azure e offre numerose funzionalità avanzate, ad esempio:
- Piattaforma integrata di gestione della mobilità aziendale: una piattaforma cloud e un'esperienza di amministrazione integrate nel portale di Azure per Intune, Azure AD Premium e Azure Information Protection.
- Gestione dei dispositivi mobili: funzionalità avanzate di gestione e protezione delle informazioni dei dispositivi mobili.
- Scalabilità: possibilità di distribuire e gestire dispositivi mobili senza doversi preoccupare del ridimensionamento.
- Controllo degli accessi in base al ruolo: possibilità di limitare l'accesso alle funzioni amministrative in base ai ruoli e agli ambiti assegnati.
- Accesso programmatico (API): supporto delle API di Microsoft Graph e opzioni di gestione di SDK e PowerShell.
- Console Web: console basata su HTML 5 e sugli standard Web con supporto per i Web browser più moderni.
- Creazione di report avanzata: possibilità di creare report personalizzati.
- Flessibilità: facilità di installazione e rapidità di recapito delle nuove funzionalità.


## <a name="hybrid-mdm-with-configuration-manager"></a>Gestione di dispositivi mobili ibrida con Configuration Manager
La gestione di dispositivi mobili (MDM, Mobile Device Management) ibrida è una soluzione che consente di integrare le funzionalità di gestione dei dispositivi mobili di Intune in Configuration Manager. Questa soluzione usa Intune come canale di recapito di criteri, profili e applicazioni ai dispositivi e usa l'infrastruttura locale di Configuration Manager per gestire il contenuto e i dispositivi stessi. L'implementazione ibrida consente il controllo da un'unica interfaccia.  In altre parole, è possibile usare la stessa infrastruttura e la stessa console di amministrazione locali per gestire i dispositivi mobili con Intune, nonché i PC e i server, con il client di Configuration Manager tradizionale. È possibile scegliere la MDM ibrida per i motivi seguenti:  
- Si vogliono gestire sia i dispositivi mobili registrati in Intune che i dispositivi gestiti con il client Configuration Manager dalla console amministrativa
- L'infrastruttura richiede più server del servizio Registrazione dispositivi di rete per il recapito dei certificati ai dispositivi mobili
- L'infrastruttura richiede più connettori di Exchange
- È necessario il supporto della crittografia S/MIME


## <a name="changing-the-mdm-authority-setting"></a>Modifica dell'impostazione dell'autorità MDM
Se è necessario modificare l'impostazione relativa all'autorità MDM, è possibile farlo personalmente senza contattare il supporto Microsoft e senza annullare e ripetere la registrazione dei dispositivi gestiti esistenti. Per altre informazioni, vedere [Cambiare l'autorità MDM](/sccm/mdm/deploy-use/change-mdm-authority.md).

> [!NOTE]    
> Per modificare l'autorità MDM su Intune autonomo è necessario Configuration Manager 1610 o versione successiva. Se si ha una versione precedente di Configuration Manager, è possibile modificare l'autorità MDM, ma è necessario richiedere assistenza al supporto tecnico Microsoft. Dopo la modifica dell'autorità MDM è necessario annullare e ripetere la registrazione di tutti i dispositivi.  


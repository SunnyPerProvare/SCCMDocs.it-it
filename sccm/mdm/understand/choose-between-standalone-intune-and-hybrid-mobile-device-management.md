---
title: Scegliere la versione autonoma di Intune o la gestione di dispositivi mobili ibrida
titleSuffix: Configuration Manager
description: Scegliere se distribuire una gestione di dispositivi mobili ibridi con Intune e Configuration Manager o se eseguire Intune autonomamente.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 153c1208cef8a940cc06412322e8112d53d17e58
ms.sourcegitcommit: 98c3f7848dc9014de05541aefa09f36d49174784
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2018
ms.locfileid: "42584507"
---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mdm-with-configuration-manager"></a>Scegliere tra la versione autonoma di Microsoft Intune e la gestione di dispositivi mobili ibrida con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Una delle domande più frequenti sulla Gestione di dispositivi mobili con Microsoft Intune è: "È preferibile integrare Intune e Configuration Manager (gestione dei dispositivi mobili ibrida) o eseguire Intune autonomo nella configurazione che prevede solo il cloud?" 

Intune in Azure è la soluzione MDM consigliata da Microsoft.     


> [!Important]  
> A partire dal 14 agosto 2018, la gestione ibrida dei dispositivi mobili è una [funzionalità deprecata](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Per altre informazioni, vedere [Informazioni sulla gestione di dispositivi mobili ibrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  


 
## <a name="intune-standalone"></a>Intune autonomo

Intune autonomo è la topologia di distribuzione consigliata da Microsoft. Intune autonomo è una soluzione di gestione di dispositivi mobili (MDM) solo nel cloud gestita tramite una console Web a cui è possibile accedere da qualsiasi parte del mondo. I data center di Intune si trovano in America del Nord, in Europa e in Asia. Dato che Intune è un servizio cloud, è possibile distribuire velocemente la gestione Intune nei dispositivi.

I clienti trovano in genere più veloce e semplice distribuire la topologia autonoma, poiché non ci sono dipendenze per i componenti locali. Intune autonomo ora fa parte della piattaforma cloud di Microsoft Azure e offre numerose funzionalità avanzate, ad esempio:  

- Piattaforma integrata di gestione della mobilità aziendale: una piattaforma cloud e un'esperienza di amministrazione integrate nel portale di Azure per Intune, Azure AD Premium e Azure Information Protection  

- Gestione dei dispositivi mobili: funzionalità avanzate di gestione e protezione delle informazioni dei dispositivi mobili  

- Scalabilità: possibilità di distribuire e gestire dispositivi mobili senza doversi preoccupare del ridimensionamento  

- Controllo degli accessi in base al ruolo: possibilità di limitare l'accesso alle funzioni amministrative in base ai ruoli e agli ambiti assegnati  

- Accesso programmatico (API): supporto delle API Microsoft Graph e opzioni di gestione di SDK e PowerShell  

- Console Web: console basata su HTML 5 e sugli standard Web con supporto per i Web browser più moderni  

- Creazione di report avanzata: possibilità di creare report personalizzati  

- Flessibilità: facilità di installazione e rapidità di recapito delle nuove funzionalità  



## <a name="hybrid-mdm-with-configuration-manager"></a>Gestione di dispositivi mobili ibrida con Configuration Manager

> [!Important]  
> A partire dal 14 agosto 2018, la gestione ibrida dei dispositivi mobili è una [funzionalità deprecata](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Per altre informazioni, vedere [Informazioni sulla gestione di dispositivi mobili ibrida](/sccm/mdm/understand/hybrid-mobile-device-management).  

La gestione di dispositivi mobili (MDM, Mobile Device Management) ibrida è una soluzione che consente di integrare le funzionalità di gestione dei dispositivi mobili di Intune in Configuration Manager. Questa soluzione usa Intune come canale di recapito di criteri, profili e applicazioni ai dispositivi e usa l'infrastruttura locale di Configuration Manager per gestire il contenuto e i dispositivi stessi. L'implementazione ibrida consente il controllo da un'unica interfaccia. In altre parole, è possibile usare la stessa infrastruttura e la stessa console di amministrazione locali per gestire i dispositivi mobili con Intune, nonché i PC e i server, con il client di Configuration Manager tradizionale. 

È possibile scegliere la MDM ibrida per i motivi seguenti:  

- Si vogliono gestire sia i dispositivi mobili registrati in Intune che i dispositivi gestiti con il client Configuration Manager dalla console amministrativa  

- L'infrastruttura richiede più server del servizio Registrazione dispositivi di rete per il recapito dei certificati ai dispositivi mobili  

- L'infrastruttura richiede più connettori di Exchange  

- È necessario il supporto della crittografia S/MIME

> [!Note]  
> Se si configura una soluzione MDM ibrida in Configuration Manager per l'accesso condizionale con Exchange locale, gli utenti possono ancora accedere alla posta elettronica in Outlook per iOS e Android. La stessa configurazione con la versione autonoma di Intune blocca la posta elettronica per questi client.<!--Intune bug 2285890-->  



## <a name="change-the-mdm-authority"></a>Cambiare l'autorità MDM

Se è necessario modificare l'impostazione relativa all'autorità MDM, è possibile farlo personalmente senza contattare il supporto Microsoft e senza annullare e ripetere la registrazione dei dispositivi gestiti esistenti. Per altre informazioni, vedere [Cambiare l'autorità MDM](/sccm/mdm/deploy-use/change-mdm-authority).


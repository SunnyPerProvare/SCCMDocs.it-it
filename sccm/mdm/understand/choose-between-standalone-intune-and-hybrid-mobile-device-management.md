---
title: Scegliere Intune autonomo o MDM per dispositivi ibridi | Microsoft Docs
description: Scegliere se distribuire una gestione di dispositivi mobili ibridi con Intune e Configuration Manager o se eseguire Intune autonomamente.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 84e3896dd05a8c157f4e94625b0eca60aacc11d3
ms.openlocfilehash: 8f2625aadfd0aed92d9922c7e3c0d3d166a78cdd
ms.lasthandoff: 02/25/2017

---
# <a name="choose-between-microsoft-intune-standalone-and-hybrid-mobile-device-management-with-system-center-configuration-manager"></a>Scegliere tra Microsoft Intune autonomo e la gestione di dispositivi mobili ibridi con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Una delle domande più frequenti sulla Gestione di dispositivi mobili con Microsoft Intune è: "È preferibile integrare Intune e Configuration Manager (gestione dei dispositivi mobili ibrida) o eseguire Intune autonomo nella configurazione che prevede solo il cloud?" Per rispondere a questa domanda, è necessario confrontare attentamente le due opzioni e prendere in considerazione gli aggiornamenti di Intune autonomo in arrivo all'inizio del 2017.

## <a name="what-is-intune-standalone"></a>Che cos'è Intune autonomo?

Intune autonomo è una soluzione di gestione di dispositivi mobili solo nel cloud che non implica alcuna risorsa locale ed è gestita tramite una console Web a cui è possibile accedere da qualsiasi parte del mondo. I data center di Intune si trovano in America del Nord, in Europa e in Asia. Dato che Intune è un servizio cloud, è possibile distribuire la gestione Intune nei dispositivi in un intervallo di tempo relativamente breve. È anche possibile scegliere Intune autonomo se nell'organizzazione è in corso lo spostamento nel cloud.

## <a name="what-is-hybrid-mdm-with-configuration-manager"></a>Che cos'è la gestione di dispositivi mobili ibrida con Configuration Manager?

La gestione di dispositivi mobili ibrida è una soluzione che usa Intune come canale di recapito di criteri, profili e applicazioni ai dispositivi e usa l'infrastruttura locale di Configuration Manager per archiviare e gestire il contenuto e gestire i dispositivi. È possibile scegliere la gestione di dispositivi mobili ibrida se si è già effettuato un investimento significativo in Configuration Manager e si vuole estendere la soluzione alla gestione dei dispositivi mobili. Un'implementazione ibrida garantisce il controllo da un'unica interfaccia. In altre parole, è possibile usare la stessa infrastruttura e la stessa console di amministrazione locali per gestire i dispositivi mobili con Intune, nonché i PC e i server con il client di Configuration Manager tradizionale.

## <a name="whats-coming-to-intune-standalone-in-early-2017"></a>Novità di Intune autonomo all'inizio del 2017

Se si deve scegliere tra Intune autonomo e la gestione ibrida, è consigliabile tenere in considerazione le funzionalità che usciranno per Intune autonomo all'inizio del 2017. Oggi la gestione di dispositivi mobili ibrida include alcune funzionalità avanzate che in passato hanno indotto alcuni clienti a preferire questa soluzione a Intune autonomo per la gestione dei dispositivi:

-   Accesso programmatico (API): opzioni di gestione SDK e PowerShell.

-   Creazione di report personalizzati.

-   Controllo degli accessi in base al ruolo: possibilità di limitare l'accesso alle funzioni amministrative in base ai ruoli assegnati.

-   Scalabilità: possibilità di distribuire e gestire oltre 100.000 dispositivi mobili.

-   Unica interfaccia: possibilità di gestire sia i PC client tradizionali che i dispositivi gestiti da Intune tramite la stessa console.

Se si sta iniziando a pianificare la distribuzione di Intune e si ha a disposizione un periodo di diversi mesi per la distribuzione pilota, i test di accettazione e la distribuzione finale, è possibile prendere in considerazione Intune autonomo ora, tenendo conto che gli aggiornamenti del servizio cloud in arrivo includeranno un numero maggiore di funzionalità. Nel corso della prima metà del 2017 Intune autonomo verrà aggiornato con molte delle funzionalità avanzate della distribuzione ibrida con Configuration Manager. Intune autonomo passerà presto alla piattaforma cloud di Microsoft Azure. Con il trasferimento sarà in grado di offrire maggiore scalabilità, accesso basato sui ruoli tramite il portale di Azure, funzioni di creazione di report personalizzati e accesso programmatico tramite l'API di Azure Graph.

È possibile passare dalla gestione ibrida a Intune autonomo o viceversa, ma è necessario l'intervento del supporto tecnico e del personale operativo Microsoft. Dopo la modifica dell'autorità di gestione è anche necessario annullare e ripetere la registrazione di tutti i dispositivi.  Microsoft si sta impegnando per offrire in un aggiornamento di servizio futuro una maggiore efficienza nel passaggio da una configurazione a un'altra.


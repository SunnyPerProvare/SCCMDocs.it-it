---
title: Supporto tecnico OneTrace (anteprima)
titleSuffix: Configuration Manager
description: OneTrace è un nuovo visualizzatore log disponibile nel Supporto tecnico che include miglioramenti rispetto a CMTrace.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 4cde43d1-9b09-4601-b389-0776de451b4e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0e90a06b956c39cb7a473af87cdfca0f722122ff
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "72172634"
---
# <a name="support-center-onetrace-preview"></a>Supporto tecnico OneTrace (anteprima)

<!--3555962-->

A partire dalla versione 1906, OneTrace è un nuovo visualizzatore log incluso nel Supporto tecnico. Funziona in modo analogo a CMTrace, con i miglioramenti seguenti:

- Una visualizzazione a schede
- Finestre ancorabili
- Funzionalità di ricerca migliorate
- Possibilità di abilitare i filtri senza uscire dalla visualizzazione del log
- Hint della barra di scorrimento per identificare rapidamente i cluster di errori
- Apertura veloce del log per i file di grandi dimensioni

![Screenshot del visualizzatore log OneTrace](media/3555962-onetrace.png)

OneTrace funziona con molti tipi di file di log, ad esempio:

- Log client di Configuration Manager
- Log del server di Configuration Manager
- Messaggi di stato
- File di log ETW di Windows Update in Windows 10
- File di log di Windows Update in Windows 7 e Windows 8.1

## <a name="prerequisites"></a>Prerequisiti

- .NET Framework versione 4.6 o successiva

## <a name="install"></a>Installazione

OneTrace viene installato con il Supporto tecnico. Individuare il programma di installazione di Support Center nel server del sito nel percorso seguente: `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`.

Per impostazione predefinita, l'applicazione OneTrace viene installata in `"C:\Program Files (x86)\Configuration Manager Support Center\CMPowerLogViewer.exe`.

> [!Note]  
> Support Center e OneTrace usano Windows Presentation Foundation (WPF). Questo componente non è disponibile in Windows PE. Continuare a usare CMTrace nelle immagini d'avvio con le distribuzioni di sequenze di attività.  

## <a name="see-also"></a>Vedere anche

- [Visualizzatore log del Supporto tecnico](/sccm/core/support/support-center-ui-reference#bkmk_log-viewer)

- [CMTrace](/sccm/core/support/cmtrace)

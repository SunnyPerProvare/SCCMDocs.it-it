---
title: Procedure consigliate per la creazione di report
titleSuffix: Configuration Manager
description: Suggerimenti utili sull'uso delle funzionalità per la creazione di report di Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 64f9d931-33f1-456f-a4e4-0ec077465bd0
author: mestew
ms.author: aaroncz
ms.openlocfilehash: b5ba34b3b4fa6c38ce904ab6786ba2b1587ca723
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75797504"
---
# <a name="best-practices-for-reporting-in-configuration-manager"></a>Procedure consigliate per la creazione di report in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare le seguenti procedure consigliate per la creazione di report in Configuration Manager:  

## <a name="for-best-performance-install-the-reporting-services-point-on-a-remote-site-system-server"></a>Per ottenere prestazioni ottimali, installare il punto di Reporting Services in un server di sistema del sito remoto  
Benché sia possibile installare il punto di Reporting Services nel server del sito o in un sistema del sito remoto, l'installazione del punto di Reporting Services in un server di sistema del sito remoto garantisce prestazioni migliori.  

## <a name="optimize-sql-server-reporting-services-queries"></a>Ottimizzare le query di SQL Server Reporting Services  
I ritardi di reporting sono in genere causati dal tempo necessario per eseguire le query e recuperare risultati. Se si utilizza Microsoft SQL Server, strumenti come Analizzatore query e Profiler consentono di ottimizzare le query.  

## <a name="schedule-report-subscription-processing-to-run-outside-standard-office-hours"></a>Pianificare l'elaborazione delle sottoscrizioni report per l'esecuzione in orari non lavorativi  
Se possibile, pianificare l'elaborazione delle sottoscrizioni report per l'esecuzione in orari non lavorativi al fine di ridurre al minimo l'elaborazione della CPU nel server di database del sito di Configuration Manager. In questo modo è inoltre possibile incrementare la disponibilità per le richieste di report impreviste.  

## <a name="updating-built-in-reports"></a>Aggiornamento di report predefiniti
Se si modifica un report standard, quando il sito viene aggiornato, il report viene rinominato con un prefisso di sottolineatura (`_`). Questo comportamento assicura che l'aggiornamento del sito non sovrascriva il report modificato dal report standard.

## <a name="next-steps"></a>Passaggi successivi
[Configurare la creazione di report](configuring-reporting.md)

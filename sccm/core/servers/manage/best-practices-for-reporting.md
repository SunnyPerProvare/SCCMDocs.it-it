---
title: Procedure consigliate per i report | System Center Configuration Manager
description: "Suggerimenti utili sull'uso delle funzionalità per la creazione di report di System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 64f9d931-33f1-456f-a4e4-0ec077465bd0
caps.latest.revision: 4
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: fae72b0455b53923aaf93b5b53afb562bedc2eca


---
# <a name="best-practices-for-reporting-in-system-center-configuration-manager"></a>Procedure consigliate per la creazione di report in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare le seguenti procedure consigliate per la creazione di report in System Center Configuration Manager:  

## <a name="for-best-performance-install-the-reporting-services-point-on-a-remote-site-system-server"></a>Per ottenere prestazioni ottimali, installare il punto di Reporting Services in un server di sistema del sito remoto  
 Benché sia possibile installare il punto di Reporting Services nel server del sito o in un sistema del sito remoto, l'installazione del punto di Reporting Services in un server di sistema del sito remoto garantisce prestazioni migliori.  

## <a name="optimize-sql-server-reporting-services-queries"></a>Ottimizzare le query di SQL Server Reporting Services  
 I ritardi di reporting sono in genere causati dal tempo necessario per eseguire le query e recuperare risultati. Se si utilizza Microsoft SQL Server, strumenti come Analizzatore query e Profiler consentono di ottimizzare le query.  

## <a name="schedule-report-subscription-processing-to-run-outside-standard-office-hours"></a>Pianificare l'elaborazione delle sottoscrizioni report per l'esecuzione in orari non lavorativi  
 Se possibile, pianificare l'elaborazione delle sottoscrizioni report per l'esecuzione in orari non lavorativi al fine di ridurre al minimo l'elaborazione della CPU nel server di database del sito di Configuration Manager. In questo modo è inoltre possibile incrementare la disponibilità per le richieste di report impreviste.  

## <a name="next-steps"></a>Passaggi successivi
[Configurare la creazione di report](configuring-reporting.md)



<!--HONumber=Nov16_HO1-->



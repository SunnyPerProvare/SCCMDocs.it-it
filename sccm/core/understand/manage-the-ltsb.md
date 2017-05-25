---
title: Gestire Long Term Servicing Branch | Microsoft Docs
description: Differenze di gestione per LTSB di System Center Configuration Manager.
ms.custom: na
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8da2887a-fd8e-438c-b926-849c121f7fdf
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: 31819a1df4e63e1114682490a9b3c3b4e5c99cfa
ms.openlocfilehash: 9c6f349ead906532a7a58df74609de976769e251
ms.contentlocale: it-it
ms.lasthandoff: 05/17/2017


---
# <a name="manage-the-long-term-servicing-branch-of-configuration-manager"></a>Gestire Long Term Servicing Branch di Configuration Manager

*Si applica a: System Center Configuration Manager (Long-Term Servicing Branch)*

Quando si usa Long-Term Servicing Branch (LTSB) di System Center Configuration Manager, le informazioni riportate di seguito consentono di comprendere modifiche importanti che influiscono sulla modalità di gestione dell'infrastruttura.

Poiché LTSB è equivalente a Current Branch versione 1606 con alcune eccezioni, ad esempio l'integrazione di Intune e le funzionalità correlate al cloud, le attività usate per la pianificazione, la distribuzione, la configurazione e la gestione quotidiana sono per la maggior parte identiche.

LTSB, ad esempio, supporta lo stesso numero di siti, tipi di sito e client, nonché la stessa infrastruttura generale di Current Branch. È quindi possibile usare le indicazioni disponibili negli argomenti relativi alla pianificazione e alla progettazione dei siti e delle gerarchie per Current Branch. Analogamente, per le funzionalità con LTSB supportate da entrambi i rami, ad esempio gli aggiornamenti software o la distribuzione del sistema operativo, è possibile usare le indicazioni disponibili nelle sezioni corrispondenti della documentazione di Current Branch, tenendo presente che non sono illustrate le modifiche alle funzionalità introdotte dopo la versione 1606 di Current Branch.

Le sezioni seguenti offrono informazioni sulle attività di gestione che presentano delle differenze.

## <a name="updates-and-servicing"></a>Aggiornamenti e manutenzione
Solo gli aggiornamenti di sicurezza critici vengono resi disponibili come aggiornamenti nella console per LTSB.  

Le informazioni sugli aggiornamenti periodici per versioni di Current Branch successive sono visibili nella console, ma questi non vengono resi disponibili per LTSB. Non vengono scaricati e non possono essere installati.

Per supportare gli aggiornamenti di sicurezza critici all'interno della console, per i siti LTSB è necessario usare il [punto di connessione del servizio](/sccm/core/servers/deploy/configure/about-the-service-connection-point). È possibile configurare questo ruolo del sistema del sito in modalità offline o online, come avviene per Current Branch. LTSB raccoglie e invia gli stessi dati di telemetria e di utilizzo di Current Branch.

LTSB supporta l'uso del programma di installazione degli aggiornamenti rapidi e dello strumento di registrazione dell'aggiornamento, come documentato per Current Branch.

Per informazioni generali sugli aggiornamenti e sulla manutenzione, vedere [Updates for Configuration Manager](/sccm/core/servers/manage/updates) (Aggiornamenti per Configuration Manager).


## <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>Modifiche per l'espansione del sito e cartella CD.Latest
Quando si esegue LTSB e si espande un sito primario autonomo installando un nuovo sito di amministrazione centrale, è necessario usare il programma di installazione e i file di origine dal supporto di base della versione 1606. Per Current Branch si esegue il programma di installazione e si usano i file di origine della cartella CD.Latest.

Anche se non si esegue il programma di installazione per l'espansione del sito dalla cartella CD.Latest, si continua a usare questa cartella per il ripristino del sito e per installare un nuovo sito primario figlio se il primo sito LTSB è un sito di amministrazione centrale.

Per altre informazioni sull'espansione del sito, vedere [Espandere un sito primario autonomo](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#expand-a-stand-alone-primary-site). Per altre informazioni sulla cartella CD.Latest, vedere [The CD.Latest folder](/sccm/core/servers/manage/the-cd.latest-folder) (Cartella CD.Latest).


## <a name="recovery"></a>Modello di
Quando si esegue il ripristino, per il sito o il database del sito è necessario ripristinare il ramo originario. Non è possibile ripristinare un database del sito Current Branch con un'installazione LTSB o viceversa.

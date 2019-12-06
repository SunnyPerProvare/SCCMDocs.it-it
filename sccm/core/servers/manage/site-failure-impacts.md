---
title: Impatto degli errori del sito
titleSuffix: Configuration Manager
description: Comprendere gli effetti dei diversi errori di un sito di Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6f0e08f8-f2e1-4823-90f6-7b1f4341eb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: eebd1aaf72cbd7932a919c0a8ffdef6d6af8389f
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "62217466"
---
# <a name="site-failure-impacts-in-configuration-manager"></a>Impatto degli errori del sito in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile che si verifichi un errore nel server del sito e in uno degli altri sistemi del sito e che quindi i servizi forniti normalmente non siano più disponibili. Se si installano più sistemi del sito sullo stesso computer e si verifica un errore in questo computer, tutti i servizi forniti con regolarità da questi sistemi del sito non sono più disponibili.

Il processo di pianificazione dovrebbe includere il riconoscimento dell'impatto sul servizio fornito all'organizzazione. Poiché ogni sistema del sito nel sito fornisce funzionalità diverse, l'impatto di un errore sul sito varia in base al ruolo del sistema in cui si è verificato. 

Usare le [opzioni di disponibilità elevata](/sccm/core/servers/deploy/configure/high-availability-options) per attenuare l'errore di un singolo sistema. Pianificare e attuare anche una strategia di [backup e ripristino](/sccm/core/servers/manage/backup-and-recovery) per ridurre il tempo in cui il servizio non è disponibile.

Le sezioni seguenti descrivono l'impatto generato quando il sistema del sito specificato non è operativo:


### <a name="site-server"></a>Server del sito

- Non è possibile alcuna amministrazione del sito. Non è possibile connettere la console al sito.  

- Il punto di gestione raccoglie le informazioni del client e le memorizza nella cache fino a quando il server del sito è di nuovo online.  

- Gli utenti possono eseguire le distribuzioni esistenti e i client possono scaricare il contenuto dai punti di distribuzione.  


### <a name="site-database"></a>Database del sito

- Non è possibile alcuna amministrazione del sito.  

- Se il client di Configuration Manager dispone già di un'assegnazione di criteri con nuovi criteri e se il punto di gestione ha memorizzato nella cache il corpo dei criteri, il client può effettuare una richiesta del corpo di criteri e ricevere la relativa risposta. Tuttavia, il sito non è in grado di soddisfare nuove richieste di assegnazione di criteri.  

- I client possono eseguire le distribuzioni solo se hanno già ricevuto i criteri e i file di origine associati sono già memorizzati nella cache in locale sul client.  


### <a name="management-point"></a>Punto di gestione

- Sebbene sia possibile creare nuove distribuzioni, i client non le ricevono finché un punto di gestione non è di nuovo online.  

- I client continuano a raccogliere le informazioni sull'inventario, la misurazione del software e lo stato. I dati vengono archiviati in locale fino a quando il punto di gestione è di nuovo disponibile.  

- I client possono eseguire le distribuzioni solo se hanno già ricevuto i criteri e i file di origine associati sono già memorizzati nella cache in locale sul client.  


### <a name="distribution-point"></a>Punto di distribuzione

- I client di Configuration Manager possono eseguire le distribuzioni, solo se i file di origine associati sono già stati scaricati in locale o sono disponibili in un'origine peer.


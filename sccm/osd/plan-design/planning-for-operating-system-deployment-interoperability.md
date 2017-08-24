---
title: "Pianificazione dell'interoperabilità per la distribuzione del sistema operativo | Microsoft Docs"
description: "Conoscere i problemi di interoperabilità quando siti diversi di System Center Configuration Manager in un'unica gerarchia usano versioni diverse."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
caps.latest.revision: "10"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 50a4b75b8c8c1cb6f7a8e696abad285f99080fcd
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="planning-for-operating-system-deployment-interoperability-in-system-center-configuration-manager"></a>Pianificazione dell'interoperabilità della distribuzione del sistema operativo in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Quando siti diversi di System Center Configuration Manager in un'unica gerarchia usano versioni diverse, alcune funzionalità di Configuration Manager non sono disponibili. In genere, le funzionalità della versione più recente di Configuration Manager non sono accessibili in siti o da client che eseguono una versione precedente. Per ulteriori informazioni, vedere [Interoperability between different versions of System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

 Quando si aggiorna il sito principale nella gerarchia e quando altri siti nella gerarchia eseguono una versione precedente di Configuration Manager, è necessario considerare gli elementi seguenti:  

-   Pacchetto di installazione client  

    -   L'origine per il pacchetto di installazione client predefinito viene aggiornata automaticamente e tutti i punti di distribuzione nella gerarchia vengono aggiornati con il nuovo pacchetto di installazione client, anche i punti di distribuzione dei siti della gerarchia che eseguono una versione precedente.  

    -   Impossibile assegnare i client che eseguono la nuova versione ai siti non ancora aggiornati alla nuova versione. Assegnazione bloccata nel punto di gestione.  

-   Immagini d'avvio  

    -   Quando si aggiorna il sito principale alla versione più recente di Configuration Manager le immagini d'avvio predefinite, x86 e x64, vengono aggiornate automaticamente a Windows ADK per immagini d'avvio basate su Windows 10 che usano Windows PE 10. I file associati alle immagini d'avvio predefinite vengono aggiornati con i file dell'ultima versione di Configuration Manager. Le immagini d'avvio personalizzate non vengono aggiornate automaticamente. È necessario aggiornarle manualmente, incluse le versioni precedenti di Windows PE.  

    -   Evitare l'uso di supporto dinamico se la gerarchia del sito contiene siti con versioni diverse di Configuration Manager. Usare invece supporti basati su sito per contattare un punto di gestione specifico fino all'aggiornamento completo di tutti i siti alla stessa versione di Configuration Manager.  

    -   Verificare che le immagini d'avvio di Configuration Manager più recenti contengano la personalizzazione voluta e aggiornare tutti i punti di distribuzione nei siti che eseguono l'ultima versione di Configuration Manager con le nuove immagini d'avvio.  

-   Utilità di migrazione stato utente (USMT)  

    -   Quando si aggiorna il sito principale alla versione più recente di Configuration Manager, il pacchetto USMT predefinito viene automaticamente aggiornato alla versione più recente. I pacchetti USMT personalizzati non vengono aggiornati automaticamente. È necessario aggiornarli manualmente.  

-   Nuovi passaggi della sequenza di attività  

    -   Vengono introdotti periodicamente nuovi passaggi di sequenza di attività con le nuove versioni di Configuration Manager. Quando si distribuisce una sequenza di attività con un nuovo passaggio a client meno recenti, il passaggio della sequenza di attività avrà esito negativo. Prima di distribuire una sequenza di attività con un nuovo passaggio, assicurarsi che i client nella raccolta di destinazione siano aggiornati alla nuova versione.  

-   Supporti di distribuzione del sistema operativo  

    -   Quando il sito viene aggiornato a una nuova versione, tutti i supporti (di avvio, di acquisizione, in versione di preproduzione e autonomi) devono essere aggiornati con il nuovo pacchetto client di Configuration Manager.  

-   Estensioni di terze parti per la distribuzione del sistema operativo  

    -   Quando si hanno estensioni di terze parti per la distribuzione del sistema operativo e versioni diverse di Configuration Manager o di client di Configuration Manager, ovvero una gerarchia mista, si possono verificare problemi con le estensioni.  

 Durante l'aggiornamento attivo dei siti della gerarchia, vedere le sezioni seguenti per un supporto nelle distribuzioni del sistema operativo.  

## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>Ultime versioni dei siti di Configuration Manager in una gerarchia mista  
 Quando un sito viene aggiornato con l'ultima versione di Configuration Manager, le sequenze di attività che fanno riferimento al pacchetto di installazione client predefinito inizieranno automaticamente a distribuire l'ultima versione client di Configuration Manager. Le sequenze di attività che fanno riferimento a un pacchetto di installazione client personalizzato continueranno a distribuire la versione del client contenuta in tale pacchetto, probabilmente una versione precedente del client di Configuration Manager, e devono essere aggiornate per evitare errori nella distribuzione delle sequenze di attività. Quando una sequenza di attività è configurata per l'uso di un pacchetto di installazione client personalizzato, è necessario aggiornare il passaggio della sequenza di attività per l'uso dell'ultima versione di Configuration Manager del pacchetto di installazione client oppure aggiornare il pacchetto personalizzato per l'uso dell'origine dell'installazione client di Configuration Manager più recente.  

> [!IMPORTANT]  
>  Non distribuire una sequenza di attività che fa riferimento al pacchetto di installazione client di Configuration Manager più recente nei client di un sito di Configuration Manager meno recente. Quando i client assegnati a un sito di Configuration Manager precedente vengono aggiornati con l'ultima versione client di Configuration Manager, l'assegnazione al sito di Configuration Manager precedente viene bloccata. Il client non è più assegnato ad alcun sito e non viene gestito fino alla sua assegnazione manuale a un sito di Configuration Manager più recente o fino alla reinstallazione della versione precedente del client di Configuration Manager nel computer.  

## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>Versioni precedenti dei siti di Configuration Manager in una gerarchia mista  
 Dopo aver aggiornato il sito di amministrazione centrale con l'ultima versione di Configuration Manager, è necessario eseguire quanto indicato di seguito per verificare che le sequenze di attività di distribuzione del sistema operativo distribuite ai client assegnati a un sito di Configuration Manager meno recente, ovvero non ancora aggiornato all'ultima versione di Configuration Manager, non lascino i client in uno stato non gestito.  

-   Creare una sequenza di attività da usare solo per la distribuzione ai client in un sito di Configuration Manager. Creare una copia di una sequenza di attività da usare per la distribuzione ai client in un sito aggiornato con l'ultima versione di Configuration Manager e modificare la sequenza di attività per la distribuzione ai client in un sito di Configuration Manager meno recente. Configurare quindi la sequenza di attività in modo che faccia riferimento a un pacchetto di installazione client personalizzato che usa l'origine dell'installazione client di Configuration Manager più recente. Se non si ha già a disposizione un pacchetto di installazione client personalizzato che fa riferimento all'origine dell'installazione client di Configuration Manager meno recente, è necessario crearlo manualmente.  

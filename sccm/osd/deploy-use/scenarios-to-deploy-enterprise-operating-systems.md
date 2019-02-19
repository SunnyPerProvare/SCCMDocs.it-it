---
title: Scenari di distribuzione di sistemi operativi aziendali
titleSuffix: Configuration Manager
description: Informazioni su vari scenari per distribuire i sistemi operativi aziendali con System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: f74fdb86-c7c2-447f-91f6-b42df6370d7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 92b968a8dae63d15e087e098452b56b0397c7b78
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137576"
---
# <a name="scenarios-to-deploy-enterprise-operating-systems-with-system-center-configuration-manager"></a>Scenari di distribuzione di sistemi operativi aziendali con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager sono disponibili gli scenari seguenti di distribuzione dei sistemi operativi:  

-   [Aggiornare Windows alla versione più recente](upgrade-windows-to-the-latest-version.md): questo scenario aggiorna il sistema operativo nei computer che attualmente eseguono Windows 7, Windows 8, Windows 8.1 o Windows 10. Il processo di aggiornamento mantiene applicazioni, impostazioni e dati dell'utente nel computer. Non sono presenti dipendenze esterne, ad esempio Windows ADK, e questo processo è più veloce e più flessibile rispetto alle distribuzioni tradizionali del sistema operativo.  

-   [Aggiornare un computer esistente con una nuova versione di Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md): questo scenario esegue il partizionamento e la formattazione (cancellazione) di un computer esistente e installa un nuovo sistema operativo nel computer. Dopo aver installato il sistema operativo, è possibile eseguire la migrazione delle impostazioni e dei dati dell'utente.  

-   [Installare una nuova versione di Windows in un nuovo computer (bare metal)](install-new-windows-version-new-computer-bare-metal.md): questo scenario consente di installare un sistema operativo in un nuovo computer. Si tratta di una nuova installazione del sistema operativo e non include la migrazione dei dati dell'utente o delle impostazioni.  

-   [Sostituire un computer esistente e trasferire le impostazioni](replace-an-existing-computer-and-transfer-settings.md): questo scenario consente di installare un sistema operativo in un nuovo computer. Facoltativamente, è possibile eseguire la migrazione delle impostazioni e dei dati dell'utente dal vecchio al nuovo computer.  

## <a name="things-to-consider-before-you-deploy-operating-system-images"></a>Aspetti di cui tenere conto prima di distribuire immagini del sistema operativo  
 Prima di distribuire un sistema operativo, è necessario considerare alcuni aspetti.  

### <a name="operating-system-image-size"></a>Dimensione dell'immagine del sistema operativo  
 La dimensione di un'immagine del sistema operativo può essere notevole. Ad esempio, la dimensione dell'immagine per Windows 7 è di 3 gigabyte (GB) o più. La dimensione dell'immagine e il numero di computer in cui viene distribuito simultaneamente il sistema operativo influiscono sulle prestazioni di rete e sulla larghezza di banda disponibile. Assicurarsi di testare le prestazioni di rete per valutare meglio l'effetto della distribuzione dell'immagine e il tempo necessario per completare la distribuzione. Le attività di Configuration Manager che influiscono sulle prestazioni di rete includono la distribuzione dell'immagine a un punto di distribuzione, la distribuzione dell'immagine da un sito a un altro e il download dell'immagine nel client di Configuration Manager.  

 Assicurarsi inoltre di pianificare uno spazio di archiviazione su disco sufficiente nei punti di distribuzione che ospitano le immagini del sistema operativo.  

### <a name="client-cache-size"></a>Dimensione della cache del client  
 Quando i client di Configuration Manager scaricano i contenuti, usano automaticamente il Servizio trasferimento intelligente in background (BITS), se disponibile. Quando si distribuisce una sequenza di attività per l'installazione di un sistema operativo, è possibile impostare un'opzione di distribuzione che consente ai client di Configuration Manager di scaricare l'immagine completa in una cache locale prima dell'esecuzione della sequenza di attività.  

 In generale, quando un client di  Configuration Manager deve scaricare un'immagine del sistema operativo o qualsiasi altro pacchetto, ma lo spazio nella cache non è sufficiente, il client controlla gli altri pacchetti nella cache per stabilire se l'eliminazione di alcuni o tutti i pacchetti meno recenti consente di liberare spazio su disco sufficiente per l'immagine. Se l'eliminazione dei pacchetti non libera spazio su disco sufficiente, il client non scarica l'immagine e la distribuzione non riesce. Questa situazione può verificarsi se nella cache è presente un pacchetto di grandi dimensioni configurato per essere mantenuto. Se l'eliminazione dei pacchetti libera spazio su disco sufficiente nella cache, il client li elimina e quindi scarica l'immagine nella cache.  

 La dimensione della cache predefinita nei client di Configuration Manager potrebbe essere insufficiente per la maggior parte delle distribuzioni dell'immagine del sistema operativo. Se si vuole scaricare l'immagine completa nella cache del client, è necessario correggere la dimensione della cache del client di Configuration Manager nei computer di destinazione in modo che possa accettare la dimensione dell'immagine distribuita.  

 Per ulteriori informazioni, vedere [Configurare la cache del client per i client di Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

## <a name="task-sequence-deployments"></a>Distribuzioni di sequenze attività  
 La sequenza di attività creata è in grado di distribuire l'immagine del sistema operativo in un computer client di Configuration Manager in uno dei modi seguenti:  

- Scaricare prima l'immagine e il relativo contenuto nella cache del client di Configuration Manager da un punto di distribuzione e procedere con l'installazione.  

- Installare immediatamente l'immagine e il relativo contenuto dal punto di distribuzione.  

- Installare l'immagine e il relativo contenuto, come richiesto dal punto di distribuzione  

  Per impostazione predefinita, durante la creazione della distribuzione per la sequenza di attività, l'immagine viene prima scaricata nella cache del client di Configuration Manager e successivamente installata. Se si sceglie di scaricare l'immagine nella cache del client di Configuration Manager prima dell'esecuzione dell'immagine e la sequenza di attività contiene un passaggio per la ripartizione del disco rigido, il passaggio di ripartizione non riesce perché il partizionamento del disco rigido cancella i contenuti della cache del client di Configuration Manager. Se la sequenza di attività deve eseguire la ripartizione del disco rigido, è necessario eseguire l'installazione dell'immagine dal punto di distribuzione usando l'opzione **Esegui programma dal punto di distribuzione**  durante la distribuzione della sequenza di attività.  

  Per altre informazioni, vedere [Deploy a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

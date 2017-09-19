---
title: Monitorare le applicazioni dalla console di System Center Configuration Manager | Microsoft Docs
description: "Monitorare la distribuzione del software, inclusi gli aggiornamenti, le impostazioni di conformità e le applicazioni usando l'area di lavoro Monitoraggio in Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 784c295c-b8b8-4202-ab9f-665908d49d6d
caps.latest.revision: "5"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: ded2a085510def60d388d9754da9c2c41de565d4
ms.sourcegitcommit: b438515490e04fb09c82a8af642d38e9a0605178
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/15/2017
---
# <a name="monitor-applications-from-the-system-center-configuration-manager-console"></a>Monitorare le applicazioni dalla console di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


In System Center Configuration Manager è possibile monitorare la distribuzione di tutti i software, inclusi gli aggiornamenti software, le impostazioni di conformità, le applicazioni, le sequenze di attività, i pacchetti e i programmi. È possibile monitorare le distribuzioni usando l'area di lavoro **Monitoraggio** nella console di Configuration Manager o usando i report.  

 Le applicazioni in Configuration Manager supportano il monitoraggio basato sugli stati, che consente di tenere traccia dell'ultimo stato di distribuzione dell'applicazione per utenti e dispositivi. Questi messaggi di stato visualizzano informazioni sui singoli dispositivi. Ad esempio, se un'applicazione viene distribuita a una raccolta di utenti, è possibile visualizzare lo stato di conformità e lo scopo della distribuzione nella console di Configuration Manager.  

## <a name="learn-about-compliance-states-in-system-center-configuration-manager"></a>Informazioni sugli stati di conformità in System Center Configuration Manager
 Uno stato di distribuzione dell'applicazione presenta uno dei seguenti stati di conformità:  

-   **Operazione riuscita** : la distribuzione dell'applicazione è stata completata oppure l'applicazione risulta già installata.  

-   **In corso** : la distribuzione dell'applicazione è in corso.  

-   **Sconosciuto** : non è possibile stabilire lo stato di distribuzione dell'applicazione. Questo stato non è applicabile per le distribuzioni con scopo **Disponibile**. Questo stato viene in genere visualizzato quando i messaggi di stato dal client non sono ancora stati ricevuti.  

-   **Requisiti non soddisfatti** : l'applicazione non è stata distribuita perché non è conforme a una dipendenza o a una regola requisiti oppure perché il sistema operativo in cui è stata distribuita non è applicabile.  

-   **Errore** : la distribuzione dell'applicazione non è riuscita a causa di un errore.  

È possibile visualizzare altre informazioni per ogni stato di conformità, tra cui le sottocategorie all'interno dello stato di conformità e il numero di utenti e dispositivi presenti in tale categoria. Ad esempio, lo stato di conformità **Errore** include le seguenti sottocategorie:  

-   Errore durante la valutazione dei requisiti  

-   Errori relativi al contenuto  

-   Errori di installazione  

 Quando si applica più di uno stato di conformità a una distribuzione dell'applicazione, è possibile visualizzare lo stato aggregato che rappresenta la conformità minima. Ad esempio:  

    -   Se un utente esegue l'accesso a due dispositivi e l'applicazione viene istallata correttamente in un dispositivo ma non è possibile installarla nel secondo, lo stato di distribuzione aggregato dell'applicazione per tale utente sarà **Errore**.  

    -   Se un'applicazione viene distribuita a tutti gli utenti che eseguono l'accesso a un computer, si otterranno più risultati di distribuzione per tale computer. Se una delle distribuzioni non viene completata, lo stato di distribuzione aggregato per il computer sarà **Errore**.  

Lo stato di distribuzione per le distribuzioni del pacchetto e del programma non è aggregato.  

 Utilizzare queste sottocategorie per identificare rapidamente eventuali problemi importanti relativi a una distribuzione dell'applicazione. È inoltre possibile visualizzare ulteriori informazioni sui dispositivi che rientrano in una particolare sottocategoria di uno stato di conformità.  

 La gestione di applicazioni in Configuration Manager offre vari report predefiniti che consentono di monitorare le informazioni su applicazioni e distribuzioni. Tali report dispongono della categoria report di **Distribuzione software - Monitoraggio applicazione**.  

 Per altre informazioni sulle modalità di configurazione dei report in Configuration Manager, vedere [Creazione di report in System Center Configuration Manager](../../core/servers/manage/reporting.md).  

## <a name="monitor-the-state-of-an-application-in-the-configuration-manager-console"></a>Monitorare lo stato di un'applicazione nella console di Configuration Manager  

1.  Nella console di Configuration Manager scegliere **Monitoraggio** > **Distribuzioni**.  

3.  Per rivedere i dettagli di distribuzione per ogni stato di conformità e i dispositivi in tale stato, selezionare una distribuzione e nel gruppo **Distribuzione** della scheda **Home** fare clic su **Visualizza stato** per aprire il riquadro **Stato distribuzione**. In questo riquadro è possibile visualizzare gli asset con il relativo stato di conformità. Scegliere un asset per visualizzare informazioni più dettagliate sul suo stato di distribuzione.  

    > [!NOTE]  
    >  Il numero di elementi che possono essere visualizzati nel riquadro **Stato di distribuzione** è limitato a 20.000. Per visualizzare più elementi, usare i report di Configuration Manager per visualizzare i dati sullo stato dell'applicazione.  
    >   
    >  Lo stato dei tipi di distribuzione viene aggregato nel riquadro **Stato distribuzione** . Per visualizzare informazioni più dettagliate sui tipi di distribuzione, utilizzare il report **Errori infrastruttura applicazione** nella categoria di report **Distribuzione software - Monitoraggio applicazione**.  

4.  Per rivedere le informazioni sullo stato generale relative alla distribuzione di un'applicazione, selezionare una distribuzione e scegliere la scheda **Riepilogo** nella finestra **Selected Deployment** (Distribuzione selezionata).  

5.  Per rivedere le informazioni sul tipo di distribuzione delle applicazioni, selezionare una distribuzione e scegliere la scheda **Tipi di distribuzione** nella finestra **Selected Deployment** (Distribuzione selezionata).  

Le informazioni visualizzate nel riquadro **Stato distribuzione** dopo aver scelto **Visualizza stato** sono dati in tempo reale ottenuti dal database di Configuration Manager. Le informazioni visualizzate nelle schede **Riepilogo** e **Tipi di distribuzione** sono dati di riepilogo.

Se i dati visualizzati nelle schede **Riepilogo** e **Tipi di distribuzione** non corrispondono ai dati visualizzati nel riquadro **Stato distribuzione**, scegliere **Esegui riepilogo** per aggiornare i dati in queste schede. È possibile configurare l'intervallo di riepilogo distribuzione applicazione predefinito nel modo seguente:  

1. Nella console di Configuration Manager scegliere **Amministrazione** > **Configurazione del sito** > **Siti**.

2. Nell'elenco **Siti** selezionare il sito per cui si vuole configurare l'intervallo di esecuzione del riepilogo e nel gruppo **Impostazioni** della scheda **Home** scegliere **Generatori riepilogo dello stato**.

3. Nella finestra di dialogo **Generatori riepilogo dello stato** scegliere **Generatore riepilogo distribuzione applicazione** e poi **Modifica**.  

4. Nella finestra di dialogo **Application Deployment Summarizer Properties** (Proprietà generatore riepilogo distribuzione applicazione) configurare gli intervalli di esecuzione del riepilogo necessari e scegliere **OK**.  

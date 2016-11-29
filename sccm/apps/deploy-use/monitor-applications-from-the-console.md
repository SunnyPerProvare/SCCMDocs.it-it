---
title: Monitorare le applicazioni dalla console di System Center Configuration Manager | System Center Configuration Manager
description: "Monitorare la distribuzione del software, inclusi gli aggiornamenti, le impostazioni di conformità e le applicazioni usando l'area di lavoro Monitoraggio in Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 784c295c-b8b8-4202-ab9f-665908d49d6d
caps.latest.revision: 5
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: ca82638267d6d9e1bb4eb6855785ac383a2191e9


---
# <a name="monitor-applications-from-the-system-center-configuration-manager-console"></a>Monitorare le applicazioni dalla console di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


## <a name="introduction"></a>Introduzione

In System Center Configuration Manager è possibile monitorare la distribuzione di tutti i software, inclusi gli aggiornamenti software, le impostazioni di conformità, le applicazioni, le sequenze di attività, i pacchetti e i programmi. È possibile monitorare le distribuzioni usando l'area di lavoro **Monitoraggio** nella console di Configuration Manager o usando i report.  

 Le applicazioni in Configuration Manager supportano il monitoraggio basato sugli stati, che consente di tenere traccia dell'ultimo stato di distribuzione dell'applicazione per utenti e dispositivi. Questi messaggi di stato visualizzano informazioni sui singoli dispositivi. Ad esempio, se un'applicazione viene distribuita a una raccolta di utenti, è possibile visualizzare lo stato di conformità e lo scopo della distribuzione nella console di Configuration Manager.  

 Uno stato di distribuzione dell'applicazione presenta uno dei seguenti stati di conformità:  

-   **Operazione riuscita** : la distribuzione dell'applicazione è stata completata oppure l'applicazione risulta già installata.  

-   **In corso** : la distribuzione dell'applicazione è in corso.  

-   **Sconosciuto** : non è possibile stabilire lo stato di distribuzione dell'applicazione. Questo stato non è applicabile per le distribuzioni con scopo **Disponibile**. Questo stato viene in genere visualizzato quando i messaggi di stato dal client non sono ancora stati ricevuti.  

-   **Requisiti non soddisfatti** : l'applicazione non è stata distribuita perché non è conforme a una dipendenza o a una regola requisiti oppure perché il sistema operativo in cui è stata distribuita non è applicabile.  

-   **Errore** : la distribuzione dell'applicazione non è riuscita a causa di un errore.  
  
È possibile visualizzare ulteriori informazioni per ogni stato di conformità, tra cui le sottocategorie all'interno dello stato di conformità e il numero di utenti e dispositivi presenti in tale categoria. Ad esempio, lo stato di conformità **Errore** include le seguenti sottocategorie:  
  
-   Errore durante la valutazione dei requisiti  

-   Errori relativi al contenuto  

-   Errori di installazione  

 Quando si applica più di uno stato di conformità a una distribuzione dell'applicazione, è possibile visualizzare lo stato aggregato che rappresenta la conformità minima. Ad esempio:  

-   se un utente esegue l'accesso a due dispositivi e l'applicazione viene istallata correttamente in un dispositivo ma non è possibile installarla nel secondo, lo stato di distribuzione aggregato dell'applicazione per tale utente sarà **Errore**.  

-   Se un'applicazione viene distribuita a tutti gli utenti che eseguono l'accesso a un computer, si otterranno più risultati di distribuzione per tale computer. Se una delle distribuzioni non viene completata, lo stato di distribuzione aggregato per il computer sarà **Errore**.  
  
Lo stato di distribuzione per le distribuzioni del pacchetto e del programma non è aggregato.  
  
 Utilizzare queste sottocategorie per identificare rapidamente eventuali problemi importanti relativi a una distribuzione dell'applicazione. È inoltre possibile visualizzare ulteriori informazioni sui dispositivi che rientrano in una particolare sottocategoria di uno stato di conformità.  

 La gestione applicazioni in Configuration Manager include vari report predefiniti che consentono di monitorare le informazioni sulle applicazioni e le distribuzioni. Tali report dispongono della categoria report di **Distribuzione software - Monitoraggio applicazione**.  

 Per altre informazioni sulle modalità di configurazione dei report in Configuration Manager, vedere [Creazione di report in System Center Configuration Manager](../../core/servers/manage/reporting.md).  
  
## <a name="monitor-the-state-of-an-application-in-the-configuration-manager-console"></a>Monitorare lo stato di un'applicazione nella console di Configuration Manager  
  
1.  Nella console di Configuration Manager fare clic su **Monitoraggio** > **Distribuzioni**.  
  
3.  Per riesaminare i dettagli di distribuzione per ogni stato di conformità e i dispositivi in tale stato, selezionare una distribuzione e nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Visualizza stato** per aprire il riquadro **Stato distribuzione** . In questo riquadro è possibile visualizzare gli asset con il relativo stato di conformità. Fare clic su un asset per visualizzare informazioni più dettagliate sul suo stato.  

    > [!NOTE]  
    >  Il numero di elementi che possono essere visualizzati nel riquadro **Stato di distribuzione** è limitato a 20.000. Per visualizzare più elementi, usare i report di Configuration Manager per visualizzare i dati sullo stato dell'applicazione.  
    >   
    >  Lo stato dei tipi di distribuzione viene aggregato nel riquadro **Stato distribuzione** . Per visualizzare informazioni più dettagliate sui tipi di distribuzione, utilizzare il report **Errori infrastruttura applicazione** nella categoria di report **Distribuzione software - Monitoraggio applicazione**.  

4.  Per revisionare le informazioni sullo stato generale relative alla distribuzione di un'applicazione, selezionare una distribuzione e quindi fare clic sulla scheda **Riepilogo** nella finestra **Distribuzione selezionata** .  

5.  Per revisionare le informazioni sul tipo di distribuzione delle applicazioni, selezionare una distribuzione e quindi fare clic sulla scheda **Tipi di distribuzione** nella finestra **Distribuzione selezionata** .  

Le informazioni visualizzate nel riquadro **Stato distribuzione** dopo aver fatto clic su **Visualizza stato** sono dati in tempo reale dal database di Configuration Manager. Le informazioni visualizzate nelle schede **Riepilogo** e **Tipi di distribuzione** sono dati di riepilogo. Se i dati visualizzati nelle schede **Riepilogo** e **Tipi di distribuzione** non corrispondono ai dati visualizzati nel riquadro **Stato distribuzione** , fare clic su **Esegui riepilogo** per aggiornare i dati in tali schede. È possibile configurare l'intervallo di riepilogo distribuzione applicazione predefinito nel modo seguente:  
1. Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione del sito** > **Siti**.
2. Dall'elenco **Siti** , selezionare il sito per cui si desidera configurare l'intervallo di riepilogo e quindi nella scheda **Home** , nel gruppo **Impostazioni** , fare clic su **Riepilogo dello stato**.
3. Nella finestra di dialogo **Riepilogo dello stato** fare clic su **Generatore riepilogo distribuzione applicazione**e quindi su **Modifica**.  
4. Nella finestra di dialogo **Generatore riepilogo distribuzione applicazione - Proprietà** configurare gli intervalli di riepilogo richiesti e quindi fare clic su **OK**.  



<!--HONumber=Nov16_HO1-->



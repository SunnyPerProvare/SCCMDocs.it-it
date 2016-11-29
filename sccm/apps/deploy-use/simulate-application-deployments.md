---
title: Simulare distribuzioni di applicazioni | System Center Configuration Manager
description: Valutare il metodo di individuazione, i requisiti e le dipendenze per un tipo di distribuzione senza installare l'applicazione.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 28b240a4-d358-40ce-8006-c697b1622ece
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: a7d9267d35b58fdc6a01b869eb739e9c721db4a4


---
# <a name="simulate-application-deployments-with-system-center-configuration-manager"></a>Simulare distribuzioni di applicazioni con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Per testare l'applicabilità di una distribuzione di applicazione nei computer senza installare o disinstallare l'applicazione, utilizzare le distribuzioni simulate. Una distribuzione simulata esegue una valutazione del metodo di rilevamento, dei requisiti e delle dipendenze per un tipo di distribuzione e segnala i risultati nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio** . Usare la procedura descritta in questo argomento per simulare una distribuzione di applicazioni in System Center Configuration Manager.  

> [!NOTE]  
>  Non è possibile usare le distribuzioni simulate per le raccolte di dispositivi mobili.  
>   
>  Non è possibile distribuire un'applicazione con scopo di distribuzione **Disinstalla** se è attiva una distribuzione simulata della stessa applicazione.  
  
Usare la procedura seguente per configurare una distribuzione simulata di applicazioni:
  
1.  Nella console di Configuration Manager selezionare uno degli elementi seguenti:  

    -   Una raccolta di utenti.  

    -   Una raccolta di dispositivi.  

    -   Un'applicazione di Configuration Manager.  

2.  Nella gruppo **Distribuzione** della scheda **Home** fare clic su **Simula distribuzione**.  

3.  In **Simulazione guidata distribuzione applicazione**specificare le seguenti informazioni:  

    -   **Applicazione** : fare clic su **Sfoglia** e quindi selezionare l'applicazione per cui si vuole creare una distribuzione simulata.  

    -   **Raccolta** : fare clic su **Sfoglia** e quindi selezionare la raccolta che si vuole usare per la distribuzione simulata.  

    -   **Azione** : dall'elenco a discesa, selezionare se si vuole simulare l'installazione o la disinstallazione dell'applicazione selezionata.  

    -   **Distribuisci automaticamente con o senza accesso utente** : se questa opzione è selezionata, i client valuteranno la distribuzione simulata indipendentemente dal fatto che i client abbiano effettuato l'accesso o meno.  

4.  Fare clic su **Avanti**, esaminare le informazioni nella pagina **Riepilogo** e quindi completare la procedura guidata per creare la distribuzione dell'applicazione simulata.  

5.  Le applicazioni simulate vengono visualizzate nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio** con lo scopo **Simula**. Per altre informazioni su come monitorare le distribuzioni delle applicazioni, vedere [Monitor applications from the System Center Configuration Manager console](../../apps/deploy-use/monitor-applications-from-the-console.md) (Monitorare le applicazioni dalla console di System Center Configuration Manager).  



<!--HONumber=Nov16_HO1-->



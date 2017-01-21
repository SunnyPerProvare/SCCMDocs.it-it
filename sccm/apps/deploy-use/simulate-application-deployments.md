---
title: Simulare le distribuzioni di applicazioni | Microsoft Docs
description: Valutare il metodo di individuazione, i requisiti e le dipendenze per un tipo di distribuzione senza installare l&quot;applicazione.
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
ms.sourcegitcommit: 0ad42d07d260581099046f11255ee312046b2595
ms.openlocfilehash: b06539ded21eac71dda7da89dae96fda7a801260


---
# <a name="simulate-application-deployments-with-system-center-configuration-manager"></a>Simulare distribuzioni di applicazioni con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile usare distribuzioni simulate per testare la distribuzione di un'applicazione senza installare o disinstallare l'applicazione. Una distribuzione simulata valuta il metodo di rilevamento, i requisiti e le dipendenze per un tipo di distribuzione e raccoglie i risultati nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio**. Usare la procedura descritta in questo argomento per simulare la distribuzione di un'applicazione in System Center Configuration Manager (Configuration Manager).  

> [!NOTE]  
> Non è possibile usare le distribuzioni simulate per le raccolte di dispositivi mobili.  
>   
> Non è possibile distribuire un'applicazione con scopo di distribuzione **Disinstalla** se è attiva una distribuzione simulata della stessa applicazione.  

## <a name="configure-a-simulated-application-deployment"></a>Configurare la distribuzione simulata di un'applicazione

1.  Nella console di Configuration Manager selezionare uno degli elementi seguenti:  
    -   Una raccolta di utenti.  
    -   Una raccolta di dispositivi.  
    -   Un'applicazione di Configuration Manager.  

2.  Nella gruppo **Distribuzione** della scheda **Home** scegliere **Simula distribuzione**.  

3.  Nella simulazione guidata distribuzione applicazione impostare i dettagli seguenti per la distribuzione simulata:  

    -   **Applicazione**. Scegliere **Sfoglia** e selezionare l'applicazione per cui si vuole creare una distribuzione simulata.  

    -   **Raccolta**. Scegliere **Sfoglia** e selezionare la raccolta da usare per la distribuzione simulata.  

    -   **Azione**. Dall'elenco a discesa selezionare se si vuole simulare l'installazione o la disinstallazione dell'applicazione selezionata.  

    -   **Distribuisci automaticamente con o senza accesso utente**. Se questa opzione è selezionata, i client valutano la distribuzione simulata indipendentemente dal fatto che abbiano eseguito l'accesso.  

4.  Fare clic su **Avanti**, rivedere le informazioni nella pagina **Riepilogo** e completare la procedura guidata per creare la distribuzione dell'applicazione simulata.  

5.  Le applicazioni simulate vengono visualizzate nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio** con lo scopo **Simula**. Per altre informazioni su come monitorare le distribuzioni delle applicazioni, vedere [Monitor applications from the System Center Configuration Manager console](../../apps/deploy-use/monitor-applications-from-the-console.md) (Monitorare le applicazioni dalla console di System Center Configuration Manager).  



<!--HONumber=Dec16_HO3-->



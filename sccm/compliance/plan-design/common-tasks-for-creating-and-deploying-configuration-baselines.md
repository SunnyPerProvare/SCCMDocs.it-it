---
title: "Attività comuni per le linee di base di configurazione - Configuration Manager | Microsoft Docs"
description: Informazioni su come creare e distribuire linee di base di configurazione in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4bb6afeb-d267-4f9b-ade2-26e5400c223b
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 991eff171dce95590a7f050e0d3b07f98c0224b3
ms.openlocfilehash: 5682cacb43af5bf9248446f1c35b08f137bdae9d


---
# <a name="common-tasks-for-creating-and-deploying-configuration-baselines-with-system-center-configuration-manager"></a>Attività comuni per la creazione e la distribuzione di linee base di configurazione con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo argomento descrive alcuni scenari comuni per scoprire come creare e distribuire le linee di base di configurazione di System Center Configuration Manager.  

 Gli utenti che hanno già familiarità con le impostazioni di conformità, possono trovare la documentazione dettagliata su tutte le funzionalità usate negli argomenti [Create configuration baselines](../../compliance/deploy-use/create-configuration-baselines.md) (Creare linee di base di configurazione) e [Deploy configuration baselines](../../compliance/deploy-use/deploy-configuration-baselines.md) (Distribuire linee di base di configurazione).  

 Prima di iniziare, leggere [Get started with compliance settings in System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md) (Introduzione alle impostazioni di conformità in System Center Configuration Manager) per apprendere alcune nozioni sulle impostazioni di conformità e [Plan for and configure compliance settings](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) (Pianificare e configurare le impostazioni di conformità) per implementare i prerequisiti necessari.  

## <a name="create-a-configuration-baseline"></a>Creare una linea di base di configurazione  
 In questo esempio è stato creato un elemento di configurazione solo per i PC con Windows 10 che eseguono il client di Configuration Manager.  

 Questo elemento di configurazione impone una password obbligatoria di almeno 6 caratteri nei PC Windows 10. L'elemento di configurazione è denominato **Windows 10 Password Enforcement**.  

Nella procedura seguente si apprenderà come aggiungere questo elemento di configurazione a una linea di base di configurazione per prepararlo per la distribuzione.  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** > **Linee di base di configurazione**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea linea di base di configurazione**.  

4.  Nella finestra di dialogo **Crea linea di base di configurazione** configurare le impostazioni seguenti:  

    -   **Nome** - Immettere **Password Windows 10** (o un altro nome a scelta).  

5.  Fare clic su **Aggiungi** > **Elementi di configurazione**.  

6.  Nella finestra di dialogo **Aggiungi elementi di configurazione** selezionare l'elemento di configurazione **Windows 10 Password Enforcement** creato in precedenza e quindi fare clic su **Aggiungi**.  

7.  Fare clic su OK per chiudere la finestra di dialogo **Aggiungi elementi di configurazione** e tornare alla finestra di dialogo **Crea linea di base di configurazione** che dovrebbe essere simile a questo screenshot:  

     ![Finestra di dialogo Crea linea di base di configurazione.](/sccm/compliance/plan-design/media/Create-Configuration-Baseline.png)  

8.  Fare clic su **OK** per chiudere la finestra di dialogo **Crea linea di base di configurazione** .  

 È ora possibile visualizzare la linea di base di configurazione appena creata nel nodo **Linee di base di configurazione** nella console di Configuration Manager.  

## <a name="deploy-the-configuration-baseline"></a>Distribuire la linea di base di configurazione  
 In questo esempio si vedrà come distribuire la linea di base di configurazione creata nella procedura precedente in una raccolta di computer.  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità** > **Impostazioni di conformità** > **Linee di base di configurazione**.  

3.  Nell'elenco di linee di base di configurazione selezionare **Password Windows 10**.  

4.  Nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Distribuisci**.  

5.  Nella finestra di dialogo **Distribuisci linee di base di configurazione** configurare le impostazioni seguenti:  

    -   **Linee di base di configurazione selezionate** - Assicurarsi che la linea di base di configurazione **Password Windows 10** sia stata aggiunta automaticamente all'elenco.  

    -   **Monitora e aggiorna le regole non conformi, se supportato** - Selezionare questa casella di controllo per assicurarsi che, in caso di assenza nei dispositivi di destinazione, le impostazioni corrette vengano monitorate e aggiornate da Configuration Manager.  

    -   **Raccolta** - Fare clic su **Sfoglia** per scegliere la raccolta di computer in cui la linea di base di configurazione verrà valutata e monitorata e aggiornata per la conformità. In questo esempio, la linea di base di configurazione è stata distribuita nella raccolta predefinita **Tutti i client desktop e di server** .  

        > [!TIP]  
        >  Non occorre preoccuparsi se la raccolta scelta contiene computer o dispositivi che non eseguono Windows 10. Se nell'elemento di configurazione creato sono state configurate le piattaforme supportate, solo i PC Windows 10 verranno valutati per la conformità.  

    -   Se necessario, configurare la pianificazione per la valutazione della linea di base di configurazione. In caso contrario, usare il valore predefinito di **7 giorni**.  

6.  L'aspetto della finestra di dialogo sarà ora simile al seguente:  

     ![Finestra di dialogo Distribuisci linee di base di configurazione](/sccm/compliance/plan-design/media/Deploy-configuration-baselines.png)  

7.  Fare clic su **OK** per chiudere la finestra di dialogo **Distribuisci linee di base di configurazione** e creare la distribuzione.  

 Per esaminare rapidamente le statistiche di conformità per questa distribuzione, nell'area di lavoro **Monitoraggio** fare clic su **Distribuzioni**. Nella parte inferiore della schermata è visualizzato un grafico **Statistiche conformità** .  

 Per informazioni più dettagliate su come monitorare le linee di base di configurazione, vedere [Monitor compliance settings](../../compliance/deploy-use/monitor-compliance-settings.md) (Monitorare le impostazioni di conformità).  



<!--HONumber=Jan17_HO4-->



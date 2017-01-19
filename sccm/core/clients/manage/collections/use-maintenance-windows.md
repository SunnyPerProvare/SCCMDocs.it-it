---
title: Usare le finestre di manutenzione | Microsoft Docs
description: Usare le raccolte e le finestre di manutenzione per gestire in modo efficace i client in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4564ebcb-41a8-4eb0-afdb-2e1f0795cfa2
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: fc392e4440e84614f92218e9c7a09ec1c2c64f53
ms.openlocfilehash: e59953f41422ee8f79ca054b5ccaccf41bb4e7af


---
# <a name="how-to-use-maintenance-windows-in-system-center-configuration-manager"></a>Come usare le finestre di manutenzione in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le finestre di manutenzione in System Center Configuration Manager consentono agli utenti amministratori di definire un periodo di tempo in cui eseguire diverse operazioni di Configuration Manager sui membri di una raccolta dispositivi. È possibile usare le finestre di manutenzione per garantire che le modifiche alla configurazione client vengano eseguite quando non influiscono sulla produttività dell'organizzazione.  

 Le seguenti operazioni di Configuration Manager supportano le finestre di manutenzione:  

-   Distribuzioni software  

-   Distribuzioni di aggiornamenti software  

-   Distribuzione e valutazione delle impostazioni di conformità  

-   Distribuzioni del sistema operativo  

-   Distribuzioni di sequenze attività  

 Le finestre di manutenzione vengono configurate per una raccolta con una data di inizio, un'ora di inizio e di fine e un criterio di ricorrenza. Ogni finestra di manutenzione deve avere una durata inferiore a 24 ore. Per impostazione predefinita, i riavvii del computer causati da una distribuzione non sono consentiti al di fuori di una finestra di manutenzione, ma è possibile sostituire questa impostazione all'interno delle impostazioni relative alla singola distribuzione. Le finestre di manutenzione interessano solo il periodo in cui il programma di distribuzione è in esecuzione. Le applicazioni configurate per il download e l'esecuzione in locale possono scaricare contenuto al di fuori della finestra di manutenzione.  

 Se un computer client è membro di una raccolta di dispositivi per la quale è configurata una finestra di manutenzione, il programma di distribuzione viene eseguito solo se il tempo di esecuzione massimo consentito non supera la durata configurata per la finestra di manutenzione. Se non è possibile eseguire il programma, viene generato un avviso e la distribuzione viene eseguita nuovamente durante la finestra di manutenzione pianificata successiva con tempo disponibile.  

## <a name="using-multiple-maintenance-windows"></a>Uso di più finestre di manutenzione  
 Quando un computer client appartiene a più raccolte dispositivi con finestre di manutenzione configurate, vengono applicate le seguenti regole:  

-   Se le finestre di manutenzione non si sovrappongono, vengono considerate come due finestre di manutenzione indipendenti.  

-   Se le finestre di manutenzione si sovrappongono, vengono considerate come una singola finestra di manutenzione che comprende il periodo di tempo coperto da entrambe le finestre di manutenzione. Se ad esempio due finestre di manutenzione, ognuna della durata di un'ora, si sovrappongono di 30 minuti, la durata effettiva della finestra di manutenzione sarà di 90 minuti.  

 Se un utente avvia l'installazione di un'applicazione da Software Center, l'applicazione viene installata immediatamente, indipendentemente dalle finestre di manutenzione configurate.  

 Se la distribuzione di un'applicazione con scopo **Richiesto** raggiunge la scadenza dell'installazione durante l'orario non lavorativo configurato da un utente in Software Center, l'applicazione verrà installata.  

### <a name="how-to-configure-maintenance-windows"></a>Come configurare le finestre di manutenzione  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Raccolte dispositivi**.  

3.  Nell'elenco **Raccolte dispositivi** selezionare la raccolta per cui si desidera configurare una finestra di manutenzione.  

4.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

5.  Nella scheda **Finestre di manutenzione** della finestra di dialogo **&lt;nome raccolta\> Proprietà** fare clic sull'icona **Nuovo**.  

    > [!NOTE]  
    >  È impossibile creare finestre di manutenzione per la raccolta **Tutti i sistemi** .  

6.  Nella finestra di dialogo **&lt;nuovo\> Pianificazione** specificare un nome, una pianificazione e un criterio di ricorrenza per la finestra di manutenzione. È anche possibile abilitare l'opzione per l'applicazione della pianificazione solo alle sequenze di attività.  

7.  Dall'elenco a discesa **Applica pianificazione a** selezionare se la finestra di manutenzione si applica a tutte le distribuzioni, solo agli aggiornamenti software o solo alle sequenze di task.  

8.  Fare clic su **OK** per chiudere la finestra di dialogo **&lt;nuovo\> Pianificazione** e creare la nuova finestra di manutenzione.  

9. Chiudere la finestra di dialogo **&lt;nome raccolta\> Proprietà**.  



<!--HONumber=Dec16_HO3-->



---
title: Configurare lo stato del client | Microsoft Docs
description: Selezionare le impostazioni relative allo stato del client in System Center Configuration Manager.
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
caps.latest.revision: 6
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: 22cc286baa72d3e356a07b91ee0a1be646fa8a9e
ms.lasthandoff: 12/16/2016


---
# <a name="how-to-configure-client-status-in-system-center-configuration-manager"></a>Come configurare lo stato del client in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima di poter monitorare lo stato del client di System Center Configuration Manager e risolvere i problemi rilevati, è necessario configurare il sito in modo da specificare i parametri usati per contrassegnare i client come inattivi e configurare le opzioni in modo da ricevere un avviso se l'attività del client scende sotto una specifica soglia. È inoltre possibile disattivare l'opzione che consente di monitorare e aggiornare automaticamente gli eventuali problemi nel computer rilevati dallo stato del client.  

##  <a name="BKMK_1"></a> Per configurare lo stato del client  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** fare clic su **Stato client**, quindi nella scheda **Home** , nel gruppo **Stato client** fare clic su **Impostazioni stato client**.  

3.  Nella finestra di dialogo **Proprietà impostazioni stato client** specificare i seguenti valori per determinare l'attività del client:  

    > [!NOTE]  
    >  Se nessuna delle impostazioni viene soddisfatta, il client verrà contrassegnato come inattivo.  

    -   **Richieste di criteri client nei seguenti giorni:** specificare il numero di giorni dalla richiesta di criteri da parte del client. Il valore predefinito è **7** giorni.  

    -   **Individuazione heartbeat nei seguenti giorni:** specificare il numero di giorni dall'invio del record di individuazione heartbeat al database del sito da parte del computer client. Il valore predefinito è **7** giorni.  

    -   **Inventario hardware nei seguenti giorni:** specificare il numero di giorni dall'invio del record di inventario hardware al database del sito da parte del computer client. Il valore predefinito è **7** giorni.  

    -   **Inventario software nei seguenti giorni:** specificare il numero di giorni dall'invio del record di inventario software al database del sito da parte del computer client. Il valore predefinito è **7** giorni.  

    -   **Messaggi di stato nei seguenti giorni:** specificare il numero di giorni dall'invio dei messaggi di stato al database del sito da parte del computer client. Il valore predefinito è **7** giorni.  

4.  Nella finestra di dialogo **Proprietà impostazioni stato client** specificare il seguente valore per determinare il periodo di conservazione dei dati di cronologia dello stato del client:  

    -   **Conservare la cronologia dello stato client per il seguente numero di giorni:** specificare il periodo di conservazione della cronologia dello stato del client nel database del sito. Il valore predefinito è **31** giorni.  

5.  Fare clic su **OK** per salvare le proprietà e chiudere la finestra di dialogo **Proprietà impostazioni stato client** .  

##  <a name="BKMK_Schedule"></a> Per configurare la pianificazione per lo stato del client  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** fare clic su **Stato client**, quindi nella scheda **Home** , nel gruppo **Stato client** fare clic su **Pianifica aggiornamento stato client**.  

3.  Nella finestra di dialogo **Pianifica aggiornamento stato client** configurare l'intervallo di aggiornamento dello stato del client e quindi fare clic su OK.  

    > [!NOTE]  
    >  Quando si modifica pianificazione per gli aggiornamenti dello stato del client, l'aggiornamento non sarà effettivo fino all'aggiornamento dello stato client successivo (per la pianificazione configurata in precedenza).  

##  <a name="BKMK_2"></a> Per configurare gli avvisi per lo stato del client  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Raccolte dispositivi**.  

3.  Nell'elenco **Raccolte siti** selezionare la raccolta per cui si desiderano configurare gli avvisi e quindi nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

    > [!NOTE]  
    >  Non è possibile configurare avvisi per raccolte di utenti.  

4.  Nella scheda **Avvisi** della finestra di dialogo *Proprietà&lt;nome raccolta\>*** ** fare clic su **Aggiungi**.  

    > [!NOTE]  
    >  La scheda **Avvisi** viene visualizzata solo se il ruolo di sicurezza a cui si è associati dispone delle autorizzazioni per gli avvisi.  

5.  Nella finestra di dialogo **Aggiungi avvisi nuova raccolta** scegliere gli avvisi che si desidera generare quando le soglie di stato del client scendono sotto un valore specifico e quindi fare clic su **OK**.  

6.  Nell'elenco **Condizioni** della scheda **Avvisi** selezionare ogni avviso dello stato del client, quindi specificare le seguenti informazioni.  

    -   **Nome avviso**: accettare il nome predefinito o immettere un nuovo nome per l'avviso.  

    -   **Gravità avviso**: nell'elenco a discesa scegliere il livello di gravità che verrà visualizzato nella console di Configuration Manager.  

    -   **Genera avviso**: specificare la percentuale di soglia per l'avviso.  

7.  Fare clic su **OK** per chiudere la finestra di dialogo *Proprietà &lt;nome raccolta\>*** **.  

##  <a name="BKMK_3"></a> Per escludere i computer da monitoraggio e aggiornamento automatici  

1.  Aprire l'editor del Registro di sistema nel computer client per il quale si desidera disattivare il monitoraggio e aggiornamento automatico.  

    > [!WARNING]  
    >  L'errato utilizzo dell'editor del Registro di sistema può provocare gravi problemi che potrebbero richiedere la reinstallazione del sistema operativo. La risoluzione dei problemi derivanti dall'errato utilizzo dell'editor del Registro di sistema non è garantita. L'utilizzo dell'editor del Registro di sistema è a rischio dell'utente.  

2.  Passare a **HKEY_LOCAL_MACHINE\Software\Microsoft\CCM\CcmEval\NotifyOnly**.  

3.  Immettere uno dei seguenti valori per questa chiave del Registro di sistema:  

    -   **True**: il computer client non eseguirà automaticamente il monitoraggio e l'aggiornamento di eventuali problemi rilevati. Tuttavia, l'utente riceverà un avviso nell'area di lavoro **Monitoraggio** in caso di problemi con il client.  

    -   **False**: il computer client eseguirà automaticamente il monitoraggio e l'aggiornamento dei problemi rilevati e l'utente riceverà un avviso nell'area di lavoro **Monitoraggio**. Questa è l'impostazione predefinita.  

4.  Chiudere l'editor del Registro di sistema.  

 È inoltre possibile installare i client utilizzando la proprietà di installazione **NotifyOnly** di CCMSetup per escluderli dal monitoraggio e aggiornamento automatico. Per altre informazioni sulla proprietà di installazione dei client, vedere [Informazioni sulle proprietà di installazione del client in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  


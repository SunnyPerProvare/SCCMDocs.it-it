---
title: Rivedere e sostituire le applicazioni | System Center Configuration Manager
description: Rivedere le versioni delle applicazioni in System Center Configuration Manager e sostituire le applicazioni.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 30170d70-489f-47f7-bebf-9ed0115db26b
caps.latest.revision: 7
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: ae6440375d6e801ac9c3932872ec1367d9c601a8


---
# <a name="how-to-revise-and-supersede-applications-in-system-center-configuration-manager"></a>Come rivedere e sostituire le applicazioni in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In questo argomento verrà illustrato come rivedere le versioni delle applicazioni di System Center Configuration Manager e come sostituire le applicazioni con una nuova versione.  

##  <a name="application-revisions"></a>Revisioni delle applicazioni  
 Quando si eseguono revisioni a un'applicazione o a un tipo di distribuzione incluso in un'applicazione, Configuration Manager crea una nuova revisione dell'applicazione. È possibile visualizzare la cronologia delle revisioni di ciascuna applicazione. È possibile inoltre visualizzarne le proprietà, ripristinare una revisione precedente di un'applicazione oppure eliminare una revisione precedente.  

### <a name="to-display-an-application-revision-history"></a>Per visualizzare la cronologia delle revisioni di un'applicazione  

1.  Nella console di Configuration Manager fare clic su **Raccolta software ** > **Gestione applicazione** > **Applicazioni** e selezionare l'applicazione voluta.  

3.  Nella scheda **Home** del gruppo **Applicazione** , fare clic su **Cronologia revisioni** per aprire la finestra di dialogo **Cronologia revisione applicazione** .  

### <a name="to-view-an-application-revision"></a>Per visualizzare la revisione di un'applicazione  

1.  Nella finestra di dialogo **Cronologia revisione applicazione** , selezionare una revisione dell'applicazione, quindi fare clic su **Visualizza**.  

2.  Nella finestra di dialogo **Proprietà** , analizzare le proprietà dell'applicazione selezionata.  

    > [!NOTE]  
    >  Le proprietà dell'applicazione visualizzate sono in sola lettura.  

3.  Chiudere la finestra di dialogo **Proprietà** .  

### <a name="to-restore-an-application-revision"></a>Per ripristinare la revisione di un'applicazione  

1.  Nella finestra di dialogo **Cronologia revisione applicazione** , selezionare una revisione dell'applicazione, quindi fare clic su **Ripristina**.  

2.  Nella finestra di dialogo **Conferma ripristino revisione** , fare clic su **Sì** per ripristinare la revisione dell'applicazione selezionata.  

### <a name="to-delete-an-application-revision"></a>Per eliminare la revisione di un'applicazione  

1.  Nella finestra di dialogo **Cronologia revisione applicazione** , selezionare una revisione dell'applicazione, quindi fare clic su **Elimina**.  

2.  Nella finestra di dialogo **Elimina revisione applicazione** , fare clic su **Sì**.  

> [!IMPORTANT]  
>  È possibile eliminare solo la revisione dell'applicazione corrente se l'applicazione è ritirata e non contiene riferimenti.  

##  <a name="application-supersedence"></a>Sostituzione delle applicazioni  
 La gestione applicazioni in Configuration Manager consente di aggiornare o sostituire le applicazioni esistenti usando una relazione di sostituzione. Quando si sostituisce un'applicazione, è possibile specificare un nuovo tipo di distribuzione per sostituire il tipo di distribuzione dell'applicazione sostituita ed è anche possibile specificare se aggiornare o disinstallare l'applicazione sostituita prima che l'applicazione sostitutiva venga installata.  

> [!IMPORTANT]  
>  Quando si seleziona l'opzione per disinstallare il tipo di distribuzione sostituito, è impossibile sostituire un tipo di distribuzione con un tipo di distribuzione distribuito a un tipo di raccolta differente.  Ad esempio, è impossibile sostituire un tipo di distribuzione che era stato distribuito a una raccolta dispositivi con un tipo di distribuzione che era stato distribuito a una raccolta di utenti se si seleziona l'opzione per disinstallare il tipo di distribuzione sostituito.  

### <a name="decide-whether-to-upgrade-or-replace-an-application"></a>Decidere se aggiornare o sostituire un'applicazione  
 Specificare se sostituire o aggiornare un'app nella finestra di dialogo **Specificare la relazione di sostituzione** della finestra di dialogo delle proprietà dell'applicazione. Il tipo di sostituzione varia a seconda se l'opzione **Disinstalla** è selezionata nella finestra di dialogo:  

-   Se si desidera eseguire l'aggiornamento a una versione più recente della stessa applicazione (con lo stesso ID applicazione), **non** selezionare **Disinstalla**.  

-   Se si desidera passare a un'altra applicazione (con un ID applicazione diverso), selezionare **Disinstalla**. Sarà necessario rimuovere la versione dell'applicazione sostituita.  

### <a name="superseding-dependent-applications"></a>Sostituzione delle applicazioni dipendenti  
 In questo esempio, **applicazione master** si riferisce all'app che si sta distribuendo, che contiene le dipendenze.  

 È possibile creare una relazione di sostituzione che aggiorna l'applicazione dipendente a una nuova versione.  

1.  Assicurarsi che la nuova applicazione dipendente e l'applicazione dipendente originale siano nello stesso gruppo di dipendenze dell'applicazione master.  

2.  Creare una relazione di sostituzione che sostituisce l'applicazione dipendente originale con la nuova applicazione dipendente.  

 Durante le nuove installazioni dell'applicazione master, la nuova applicazione dipendente verrà installata. Le installazioni esistenti dell'applicazione master verranno aggiornate con la nuova applicazione dipendente.  

 Il risultato finale è che tutte le distribuzioni dell'applicazione master useranno la nuova applicazione dipendente.  

### <a name="further-considerations"></a>Altre considerazioni  

-   È possibile specificare più relazioni di sostituzione per le applicazioni dipendenti. Viene installata l'applicazione dipendente di livello superiore nella catena di sostituzione.  

-   Le applicazioni dipendenti devono essere distribuite al dispositivo in cui è installata l'applicazione master, altrimenti l'applicazione dipendente non verrà installata.  

-   Per le nuove installazioni dell'applicazione master, se si dispone di più dipendenze, l'ordine di dipendenza determina la versione dell'applicazione dipendente da installare.  

### <a name="specify-a-supersedence-relationship"></a>Specificare una relazione di sostituzione  

1.  Nella console di Configuration Manager fare clic su **Raccolta software ** > **Gestione applicazione** > **Applicazioni** e selezionare l'applicazione che sostituirà un'altra.  

3.  Nel gruppo **Proprietà** della scheda **Home** fare clic su **Proprietà** per aprire la finestra di dialogo **Proprietà** <nome dell'applicazione>.  

4.  Nella scheda **Sostituzione** della finestra di dialogo **Proprietà** *<nome dell'applicazione\>* fare clic su **Aggiungi**.  

5.  Nella finestra di dialogo **Specificare la relazione di sostituzione** fare clic su **Sfoglia**.  

6.  Nella finestra di dialogo **Scelta applicazione** selezionare l'applicazione da sostituire e quindi fare clic su **OK**.  

7.  Nella finestra di dialogo **Specificare la relazione di sostituzione** selezionare il tipo di distribuzione che andrà a sostituire il tipo di distribuzione dell'applicazione sostituita.  

    > [!NOTE]  
    >  Per impostazione predefinita, il nuovo tipo di distribuzione non disinstallerà il tipo di distribuzione dell'applicazione sostituita. Questo scenario viene comunemente utilizzato quando si desidera distribuire un aggiornamento a un'applicazione esistente. Selezionare **Disinstalla** per rimuovere il tipo di distribuzione esistente prima di installare il nuovo tipo di distribuzione. Se si decide di aggiornare un'applicazione, assicurarsi di testare prima questa operazione in un ambiente lab.  

8.  Fare clic su **OK** per chiudere la finestra di dialogo **Specificare la relazione di sostituzione** .  

9. Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà** *<nome dell'applicazione\>*.  

### <a name="to-display-applications-that-supersede-the-current-application"></a>Per visualizzare le applicazioni che sostituiscono l'applicazione corrente  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni**, quindi fare clic su **Applicazioni**e sull'applicazione desiderata.  

3.  Nel gruppo **Proprietà** della scheda **Home** fare clic su **Proprietà** per aprire la finestra di dialogo **Proprietà***<nome dell'applicazione\>*.  

4.  Nella scheda **Riferimenti** della finestra di dialogo **Proprietà** *<nome dell'applicazione\>* selezionare **Applicazioni che sostituiscono l'applicazione** nell'elenco a discesa **Tipo di relazione**.  

5.  Esaminare l'elenco delle applicazioni che sostituiscono l'applicazione selezionata e fare clic su **OK** per chiudere la finestra di dialogo **Proprietà***<Nome dell'applicazione\>*.  



<!--HONumber=Nov16_HO1-->



---
title: Creare e distribuire un'applicazione | System Center Configuration Manager
description: Creare e distribuire un'applicazione contenente un'app line-of-business e informazioni su come gestire le applicazioni in modo efficace.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3bd1e487-ea18-43c1-b7c3-acbd9b86d429
caps.latest.revision: 15
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 12653342e2e311a9bbfc2a7aad3101c0e7f0bce0


---
# <a name="create-and-deploy-an-application-with-system-center-configuration-manager"></a>Creare e distribuire un'applicazione con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo argomento fornisce informazioni che consentono di creare subito un'applicazione con System Center Configuration Manager. In questo esempio viene creata e distribuita un'applicazione che contiene una riga per un'app aziendale per PC Windows denominata **Contoso.msi** che deve essere installata in tutti i PC che eseguono Windows 10 nell'azienda. Durante questo processo verranno fornite informazioni su gran parte delle operazioni che è possibile eseguire per gestire le applicazioni in modo efficace.  

 Questa procedura è progettata per offrire una panoramica su come creare e distribuire le applicazioni di Configuration Manager. Tuttavia, non copre tutte le opzioni configurabili e non fornisce tutte le informazioni su come creare e distribuire applicazioni per altre piattaforme.  

 Per informazioni specifiche su ogni piattaforma, vedere uno degli argomenti seguenti:  

-   [Creazione di applicazioni Windows](../../apps/get-started/creating-windows-applications.md)  
-   [Creazione di applicazioni iOS](../../apps/get-started/creating-ios-applications.md)  
-   [Creazione di applicazioni Android](../../apps/get-started/creating-android-applications.md)  
-   [Creazione di applicazioni Windows Phone](../../apps/get-started/creating-windows-phone-applications.md)  
-   [Creazione di applicazioni per computer Mac](../../apps/get-started/creating-mac-computer-applications.md)  
-   [Creazione di applicazioni server Linux e UNIX](../../apps/get-started/creating-linux-and-unix-server-applications.md) 
-   [Creazione di applicazioni Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md) 

  
Se si ha già familiarità con le applicazioni di Configuration Manager, è possibile ignorare questo argomento. Tuttavia, è consigliabile rivedere l'argomento [Creazione di applicazioni](../../apps/deploy-use/create-applications.md) per scoprire tutte le opzioni disponibili quando si creano e distribuiscono le applicazioni.  
  
## <a name="before-you-start"></a>Prima di iniziare  

Assicurarsi di aver esaminato le informazioni contenute nell'argomento [Introduzione alla gestione delle applicazioni](/sccm/apps/understand/introduction-to-application-management) che indicano come preparare il sito per installare le applicazioni e di comprendere la terminologia usata in questo argomento.  

 Inoltre, assicurarsi che i file di installazione per l'app **Contoso.msi** si trovino in un percorso accessibile sulla rete.  
  
## <a name="create-the-configuration-manager-application"></a>Creare l'applicazione di Configuration Manager  
  
### <a name="start-the-create-application-wizard-and-create-the-application"></a>Avviare la Creazione guidata applicazione e creare l'applicazione  
  
1.  Nella console di Configuration Manager fare clic su **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.  
  
3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea applicazione**.  

4.  Nella pagina **Generale** della **Creazione guidata applicazione**selezionare **Rileva automaticamente le informazioni sull'applicazione dai file di installazione**. Alcune sezioni della procedura guidata verranno prepopolate con le informazioni estratte dal file di installazione MSI. A questo punto, specificare le informazioni seguenti:  

    -   **Tipo**: scegliere **Windows Installer (file \*.msi)**  

    -   **Percorso** : immettere il percorso del file di installazione **Contoso.msi** o fare clic su **Sfoglia**per selezionare il percorso. Per trovare i file di installazione con Configuration Manager, il percorso deve essere specificato in formato *\\\Server\Share\File*.  
  
    Al termine, verrà visualizzata una schermata simile alla seguente:  
  
    ![Pagina generica di Gestione guidata applicazioni](/sccm/apps/get-started/media/App-management-wizard-general-page.png)  
  
5.  Fare clic su **Avanti**. Nella pagina **Importazione informazioni** verranno visualizzate alcune informazioni sull'app e tutti i file associati importati in Configuration Manager. Dopo aver terminato, fare di nuovo clic su **Avanti** .  

6.  Nella pagina **Informazioni generali**, è possibile fornire altre informazioni sull'applicazione che consentono di ordinarla e individuarla nella console di Configuration Manager.  

     Inoltre, il campo Programma di installazione consente di specificare l'intera riga di comando usata per installare l'applicazione nei computer. È possibile modificare questa opzione per aggiungere proprietà personalizzate (ad esempio **/q** per un'installazione automatica).  

    > [!TIP]  
    >  Alcuni dei campi in questa pagina della procedura guidata potrebbero essere stati compilati automaticamente durante l'importazione dei file di installazione dell'applicazione.  

     Al termine, verrà visualizzata una schermata simile alla seguente:  
  
     ![Pagina generica di informazioni di Gestione guidata applicazioni](/sccm/apps/get-started/media/App-management-wizard-general-information-page.png)  
  
7.  Fare clic su **Avanti**. Nella pagina di riepilogo è possibile confermare le impostazioni dell'applicazione, quindi completare la procedura guidata.  

 L'app viene creata. Per trovarla, espandere **Gestione applicazioni** nell'area di lavoro **Raccolta software**, quindi fare clic su **Applicazioni**. Per questo esempio verrà visualizzato:  
  
 ![Immagine finale dell'app](/sccm/apps/get-started/media/Final-app-graphic.png)  
  
## <a name="examine-the-properties-of-the-application-and-its-deployment-type"></a>Esaminare le proprietà dell'applicazione e il tipo di distribuzione  

Dopo aver creato un'applicazione, è possibile ridefinire le impostazioni dell'applicazione, se necessario. Per esaminare le proprietà dell'applicazione, selezionare l'app e fare clic su **Proprietà** nella scheda **Home** del gruppo **Proprietà**.  

 Nella finestra di dialogo **Proprietà applicazione \><Contoso** verranno visualizzati diversi elementi che è possibile configurare per ottimizzare il comportamento dell'applicazione. Per informazioni dettagliate su tutte le impostazioni che è possibile configurare, vedere [Creazione di applicazioni](../../apps/deploy-use/create-applications.md). Ai fini di questo esempio, verranno modificate solo alcune delle proprietà del tipo di distribuzione dell'applicazione.  
  
 Fare clic sulla scheda **Tipi di distribuzione** , selezionare il tipo di distribuzione **Applicazione Contoso** , quindi fare clic su **Modifica**.   
Viene visualizzata una finestra di dialogo simile alla seguente:  
 
![Pagina delle proprietà dell'app di gestione](/sccm/apps/get-started/media/App-management-app-properties-page.png)  
  
## <a name="add-a-requirement-to-the-deployment-type"></a>Aggiungere un requisito al tipo di distribuzione  
 I requisiti specificano le condizioni che devono essere soddisfatte prima di installare un'applicazione in un dispositivo.  È possibile scegliere tra requisiti predefiniti o personalizzati. In questo esempio, verrà aggiunto un requisito che consente l'installazione dell'applicazione solo nei computer che eseguono Windows 10.  
  
1.  Nella pagina delle proprietà del tipo di distribuzione appena aperta fare clic sulla scheda **Requisiti** .  

2.  Fare clic su **Aggiungi** per aprire la finestra di dialogo **Crea requisito** .  

3.  Nella finestra di dialogo **Crea requisito** specificare le seguenti informazioni:  

    -   **Categoria** - **Dispositivo**  

    -   **Condizione** - **Sistema operativo**  

    -   **Tipo di regola** - **Valore**  

    -   **Operatoree** - **Uno**  

    -   Nell'elenco di sistemi operativi selezionare **Windows 10**.  
  
    Al termine, verrà visualizzata una finestra di dialogo simile alla seguente:  
  
    ![Pagina dei requisiti dell'app di gestione](/sccm/apps/get-started/media/App-management-requirements-page.png)  
  
4.  Fare clic su **OK** per chiudere le singole pagine delle proprietà aperte e tornare all'elenco delle **applicazioni** nella console di Configuration Manager.  

> [!TIP]  
>  I requisiti consentono di ridurre il numero di raccolte di Configuration Manager necessario. Poiché è stato specificato che l'applicazione può essere installata solo nei PC che eseguono Windows 10, successivamente sarà possibile distribuirla in una raccolta contenente computer che eseguono sistemi operativi diversi e l'applicazione verrà installata solo su PC Windows 10.  
  
## <a name="add-the-application-content-to-a-distribution-point"></a>Aggiungere il contenuto dell'applicazione a un punto di distribuzione  

Per distribuire correttamente l'applicazione nei PC è necessario assicurarsi che il contenuto dell'applicazione viene copiato in un punto di distribuzione. I PC avranno accesso al punto di distribuzione per installare l'applicazione.  

> [!TIP]  
>  Per altre informazioni sui punti di distribuzione e la gestione del contenuto in Configuration Manager, vedere [Gestire il contenuto e l'infrastruttura del contenuto](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  
  
1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Applicazioni** e quindi selezionare dall'elenco di applicazioni l' **applicazione Contoso** creata.  

3.  Nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Distribuisci contenuto**.  

4.  Nella pagina **Generale** di **Distribuzione guidata contenuto**verificare che il nome dell'applicazione sia corretto e quindi fare clic su **Avanti**.  

5.  Nella pagina **Contenuto** esaminare le informazioni che verranno copiate nel punto di distribuzione e quindi fare clic su **Avanti**.  

6.  Nella pagina **Destinazione del contenuto** fare clic su Aggiungi per selezionare uno o più punti di distribuzione o gruppi di punti in cui installare il contenuto dell'applicazione.  

7.  Completare la procedura guidata.  

 È possibile verificare che il contenuto dell'applicazione sia stato copiato correttamente al punto di distribuzione dall'area di lavoro **Monitoraggio** in **Stato di distribuzione** > **Stato contenuto**.  
  
## <a name="deploy-the-application"></a>Distribuire l'applicazione  

Successivamente, distribuire l'applicazione a una raccolta di dispositivi nella gerarchia. Per questo esempio, l'applicazione verrà distribuita alla raccolta dispositivi **Tutti i sistemi** .  

> [!TIP]  
>  Tenere presente che l'applicazione verrà installata solo nei computer Windows 10 a causa dei requisiti selezionati in precedenza.  
  
1.  Nella console di Configuration Manager fare clic su **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.  
  
3.  Dall'elenco delle applicazioni selezionare l'applicazione creata in precedenza, **Applicazione Contoso**, e quindi scegliere **Distribuisci** nella scheda **Home** del gruppo **Distribuzione**.  

4.  Nella pagina **Generale** di **Distribuzione guidata del software**fare clic su **Sfoglia** per selezionare la raccolta di dispositivi **Tutti i sistemi** .  

5.  Nella pagina **Contenuto** verificare che il punto di distribuzione da cui si vuole consentire ai PC di installare l'applicazione sia selezionato.  

6.  Nella pagina **Impostazioni di distribuzione** assicurarsi che l'azione di distribuzione sia impostata su **Installa**e che lo scopo della distribuzione sia impostato su **Richiesto**.  

    > [!TIP]  
    >  Impostando lo scopo della distribuzione su **Richiesto**si garantisce che l'applicazione venga installata nei PC che soddisfano i requisiti impostati. Se si imposta questo valore su **Disponibile**, gli utenti possono installare l'applicazione su richiesta da Software Center.  

7.  Nella pagina **Pianificazione** è possibile configurare il momento in cui verrà installata l'applicazione. Per questo esempio, selezionare **Appena possibile dopo il tempo disponibile**.  

8.  Nella pagina **Esperienza utente**, fare clic su **Avanti** per accettare i valori predefiniti.  

9. Completare la procedura guidata.  

 Usare le informazioni della sezione **Monitorare l'applicazione** di seguito per visualizzare lo stato della distribuzione dell'applicazione.  
  
## <a name="monitor-the-application"></a>Monitorare l'applicazione  
 In questa sezione verrà esaminato rapidamente lo stato di distribuzione dell'applicazione appena distribuita.  
  
### <a name="to-review-the-deployment-status"></a>Per esaminare lo stato di distribuzione  
  
1.  Nella console di Configuration Manager fare clic su **Monitoraggio** > **Distribuzioni**.  
  
3.  Selezionare **Applicazione Contoso**dall'elenco delle distribuzioni.  

4.  Nella scheda **Home** fare clic su **Visualizza stato** nel gruppo **Distribuzione**.  

5.  Selezionare una delle schede seguenti per visualizzare più informazioni di stato sulla distribuzione di applicazioni:  

    -   **Operazione riuscita** : l'applicazione è stata installata correttamente nei PC indicati.  

    -   **In corso** : l'installazione dell'applicazione non è ancora terminata.  

    -   **Errore** : si è verificato un errore durante l'installazione dell'applicazione nei PC indicati. Vengono visualizzate anche altre informazioni sull'errore.  

    -   **Requisiti non soddisfatti** : l'applicazione non ha provato a eseguire l'installazione nei dispositivi indicati perché non soddisfa i requisiti configurati (in questo esempio, perché questi non eseguono Windows 10).  

    -   **Sconosciuto**: Configuration Manager non è riuscito a segnalare lo stato della distribuzione. Ricontrollare in seguito.  

> [!TIP]  
>  Esistono diversi modi in cui è possibile monitorare le distribuzioni di applicazioni. Per informazioni dettagliate, vedere [Monitorare le applicazioni](/sccm/apps/deploy-use/monitor-applications-from-the-console).  
  
## <a name="end-user-experience"></a>Esperienza utente finale  

Gli utenti con PC che eseguono Windows 10 gestiti da Configuration Manager visualizzeranno a breve un messaggio che informa della necessità di installare l'applicazione Contoso. Una volta che accettano l'installazione, l'applicazione verrà installata.  



<!--HONumber=Nov16_HO1-->



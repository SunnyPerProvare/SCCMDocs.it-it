---
title: Creazione di applicazioni per computer Mac | Microsoft Docs
description: Questo articolo descrive le considerazioni da tenere presenti quando si creano e distribuiscono applicazioni per i computer Mac.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ab1aecdd-d943-44f5-b0a9-e8fe7439e5d6
caps.latest.revision: 9
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 8dcf9f310a4ea8e2f43f2fe79e5e3cfa2c8aeb61
ms.openlocfilehash: c2feffad39a20519fd86ca9348b0855a51e05aa9


---
# <a name="create-mac-computer-applications-with-system-center-configuration-manager"></a>Creare applicazioni per computer Mac con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Oltre agli altri requisiti e alle procedure di System Center Configuration Manager per la creazione di un'applicazione, quando si creano e si distribuiscono applicazioni per i computer Mac è necessario tenere presente quanto segue.  

> [!IMPORTANT]  
>  Le procedure descritte in questo argomento offrono informazioni sulla distribuzione di applicazioni in computer Mac in cui è installato il client di Configuration Manager. I computer Mac registrati con Microsoft Intune non supportano la distribuzione di applicazioni.  

## <a name="general-considerations"></a>Considerazioni generali  
 È possibile usare System Center Configuration Manager per distribuire applicazioni nei computer Mac che eseguono il client Mac di Configuration Manager. I passaggi per distribuire software nei computer Mac sono simili a quelli utilizzati per distribuire software nei computer Windows. Tuttavia, prima di creare e distribuire applicazioni nei computer Mac gestiti da Configuration Manager, prendere in considerazione quanto segue:  

-   Prima di distribuire pacchetti di applicazioni Mac nei computer Mac, è necessario usare lo strumento **CMAppUtil** in un computer Mac per convertire tali applicazioni in un formato che possa essere letto da Configuration Manager.  

-   Configuration Manager non supporta la distribuzione di applicazioni Mac agli utenti: le distribuzioni devono essere effettuate a un dispositivo. Analogamente, per le distribuzioni di applicazioni Mac, Configuration Manager non supporta l'opzione **Pre-distribuisci il software nel dispositivo primario dell'utente** nella pagina **Impostazioni distribuzione** della procedura Distribuzione guidata del software.  

-   Le applicazioni Mac supportano distribuzioni simulate.  

-   Non è possibile distribuire applicazioni in computer Mac con lo scopo **Disponibile**.  

-   L'opzione per inviare pacchetti di riattivazione quando si distribuisce software non è supportata per i computer Mac.  

-   I computer Mac non supportano il Servizio trasferimento intelligente in background (BITS) per scaricare il contenuto dell'applicazione. Se il download dell'applicazione non ha esito positivo, verrà riavviata dall'inizio.  

-   Configuration Manager non supporta le condizioni globali quando si creano tipi di distribuzione per i computer Mac.  

## <a name="steps-to-create-and-deploy-an-application"></a>Passaggi per creare e distribuire un'applicazione  
 Nella tabella seguente vengono forniti i passaggi, i dettagli e ulteriori informazioni per la creazione e distribuzione di applicazioni per computer Mac.  

|Passaggio|Dettagli|  
|----------|-------------|  
|Passaggio 1: Preparare le applicazioni Mac per Configuration Manager|Per poter creare applicazioni di Configuration Manager da pacchetti software Mac, è necessario usare lo strumento **CMAppUtil** in un computer Mac per convertire il software Mac in un file **CMMAC** di Configuration Manager.|  
|Passaggio 2: Creare un'applicazione di Configuration Manager che contenga il software Mac|Utilizzare la Creazione guidata applicazione per creare un'applicazione per il software Mac.|  
|Passaggio 3: Creare un tipo di distribuzione per l'applicazione Mac|Questo passaggio è necessario solo se non si effettuata l'importazione automatica di queste informazioni dall'applicazione.|  
|Passaggio 4: Distribuire l'applicazione Mac|Utilizzare la Distribuzione guidata del software per distribuire l'applicazione nei computer Mac.|  
|Passaggio 5: Monitorare la distribuzione dell'applicazione Mac|Monitorare le corrette distribuzioni delle applicazioni nei computer Mac.|  

## <a name="supplemental-procedures-to-create-and-deploy-applications-for-mac-computers"></a>Procedure supplementari per creare e distribuire applicazioni per computer Mac  
 Usare le procedure che seguono per creare e distribuire applicazioni per computer Mac gestiti da Configuration Manager.  

###  <a name="step-1-prepare-mac-applications-for-configuration-manager"></a>Passaggio 1: Preparare le applicazioni Mac per Configuration Manager  
 Il processo necessario per creare e distribuire applicazioni di Configuration Manager nei computer Mac è simile al processo di distribuzione per i computer Windows. Tuttavia, prima di creare applicazioni di Configuration Manager che contengono tipi di distribuzione Mac, occorre preparare le applicazioni usando lo strumento **CMAppUtil** . Questo strumento viene scaricato con i file di installazione client Mac. Lo strumento **CMAppUtil** può raccogliere informazioni sull'applicazione, che includono i dati di rilevamento dai seguenti pacchetti Mac:  

-   Immagine disco Apple (.dmg)  

-   File meta pacchetto (.mpkg)  

-   Pacchetto di Mac OS X Installer (.pkg)  

-   Applicazione di Mac OS X (.app)  

Dopo aver raccolto informazioni sull'applicazione, **CMAppUtil** crea un file con estensione **.cmmac**. Questo file contiene i file di installazione per il software Mac e le informazioni sui metodi di rilevamento da usare per stabilire se l'applicazione sia stata già installata. **CMAppUtil** è anche in grado di elaborare i file **.dmg** che contengono più applicazioni Mac e di creare tipi di distribuzione diversi per ogni applicazione.  

1.  Copiare il pacchetto di installazione software Mac nella cartella sul computer Mac in cui sono stati estratti i contenuti del file **macclient.dmg** scaricato dall'Area download Microsoft.  

2.  Nello stesso computer Mac, aprire una finestra terminale e spostarsi nella cartella in cui sono stati estratti i contenuti del file **macclient.dmg** .  

3.  Spostarsi nella cartella **Strumenti** e immettere la seguente riga di comando:  

     **./CMAppUtil** *<proprietà\>*  

     Ad esempio, se si desidera convertire i contenuti di un file di immagine disco Apple denominato **MySoftware.dmg** memorizzato nella cartella desktop Utenti in un file **cmmac** nella stessa cartella e si desidera creare file **cmmac** per tutte le applicazioni trovate nel file di immagine disco. A tale scopo, utilizzare la seguente riga di comando:  

     **./CMApputil –c /Users/** *<Nome utente\>* **/Desktop/MySoftware.dmg -o /Users/** *<Nome utente\>* **/Desktop -a**  

    > [!NOTE]  
    >  Il nome dell'applicazione deve essere lungo non più di 128 caratteri.  

     Per configurare le opzioni per **CMAppUtil**, utilizzare le proprietà della riga di comando riportate nella tabella seguente:  

    |Proprietà|Altre informazioni|  
    |--------------|----------------------|  
    |**-h**|Visualizza le proprietà della riga di comando disponibili.|  
    |**-r**|Visualizza come output **detection.xml** del file **.cmmac** fornito in **stdout**. L'output contiene i parametri di rilevamento e la versione di **CMAppUtil** utilizzata per creare il file **.cmmac** .|  
    |**-c**|Specificare il file di origine da convertire.|  
    |**-o**|Questa proprietà deve essere utilizzata in combinazione con la proprietà -c per specificare il percorso di output.|  
    |**-a**|Utilizzare questa proprietà in combinazione la proprietà -c e il file del disco immagine (**.dmg**) per creare automaticamente file .cmmac per tutte le applicazioni e pacchetti trovati nel file di immagine disco.|  
    |**-s**|Ignora la generazione di **detection.xml** se non vengono trovati parametri di rilevamento e forza la creazione del file **.cmmac** senza il file **detection.xml** .|  
    |**-v**|Visualizza un output più dettagliato dallo strumento **CMAppUtil** insieme a informazioni di diagnostica.|  

4.  Assicurarsi che il file **.cmmac** sia stato creato nella cartella di output specificata.  

###  <a name="create-a-configuration-manager-application-that-contains-the-mac-software"></a>Creare un'applicazione di Configuration Manager che contenga il software Mac  

Usare la procedura che segue per creare e distribuire un'applicazione per computer Mac gestiti da Configuration Manager.  

1.  Nella console di Configuration Manager fare clic su **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea applicazione**.  

4.  Nella pagina **Generale** della Creazione guidata applicazione selezionare **Rileva automaticamente le informazioni sull'applicazione dai file di installazione**.  

    > [!NOTE]  
    >  Selezionare **Specifica manualmente le informazioni dell'applicazione** se si desidera specificare informazioni sull'applicazione manualmente. Per altre informazioni su come specificare manualmente le informazioni, vedere [Come creare applicazioni con System Center Configuration Manager](../../apps/deploy-use/create-applications.md).  

5.  Nell'elenco a discesa **Tipo** , selezionare **Mac OS X**.  

6.  Nel campo **Percorso** specificare il percorso UNC nel formato *\\\\<server\>\\<condivisione\>\\<nomefile\>* al file di installazione dell'applicazione Mac (file **CMMAC**) che rileverà le informazioni dell'applicazione. In alternativa, fare clic su **Sfoglia** per individuare e specificare il percorso del file di installazione.  

    > [!NOTE]  
    >  È necessario accedere al percorso UNC che contiene l'applicazione.  

7.  Fare clic su **Avanti**.  

8.  Nella pagina **Importazione informazioni** della Creazione guidata applicazione, esaminare le informazioni che sono state importate. Se necessario, è possibile fare clic su **Indietro** per tornare indietro e correggere eventuali errori. Fare clic su **Avanti** per continuare.  

9. Nella pagina **Informazioni generali** della Creazione guidata applicazione, specificare informazioni sull'applicazione quali nome dell'applicazione, commenti, versione e riferimenti facoltativi che consentono di fare riferimento all'applicazione nella console di Configuration Manager.  

    > [!NOTE]  
    >  Alcune delle informazioni dell'applicazione potrebbero essere già presenti in questa pagina se sono state ottenute in precedenza dai file di installazione dell'applicazione.  

10. Fare clic su **Avanti**, riesaminare le informazioni sull'applicazione nella pagina **Riepilogo** e quindi completare la Creazione guidata applicazione.  

11. La nuova applicazione viene visualizzata nel nodo **Applicazioni** della console di Configuration Manager.  

###  <a name="step-3-create-a-deployment-type-for-the-mac-application"></a>Passaggio 3: Creare un tipo di distribuzione per l'applicazione Mac  
 Usare la procedura che segue per creare un tipo di distribuzione per i computer Mac gestiti da Configuration Manager.  

> [!NOTE]  
>  Se si è effettuata l'importazione automatica delle informazioni sull'applicazione nella Creazione guidata applicazione, un tipo di distribuzione per l'applicazione potrebbe essere già stato creato.  

1.  Nella console di Configuration Manager fare clic su **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.  

3.  Selezionare un'applicazione e quindi nel gruppo **Applicazione** della scheda **Home** fare clic su **Crea tipo di distribuzione** per creare un nuovo tipo di distribuzione per questa applicazione.  

    > [!NOTE]  
    >  È anche possibile avviare la Creazione guidata tipo di distribuzione dalla Creazione guidata applicazione e dalla scheda **Tipi di distribuzione** della finestra di dialogo *Proprietà di***<nome applicazione\>**.  

4.  Nella pagina **Generale** della Creazione guidata tipo di distribuzione, nell'elenco a discesa **Tipo** , selezionare **Mac OS X**.  

5.  Nel campo **Percorso** specificare il percorso UNC nel formato \\\\<server\>\\<condivisione\>\\<nomefile\> nel file di installazione dell'applicazione (file **CMMAC**). In alternativa, fare clic su **Sfoglia** per individuare e specificare il percorso del file di installazione.  

    > [!NOTE]  
    >  È necessario accedere al percorso UNC che contiene l'applicazione.  

6.  Fare clic su **Avanti**.  

7.  Nella pagina **Importazione informazioni** della **Creazione guidata tipo di distribuzione**, esaminare le informazioni che sono state importate. Se necessario, fare clic su **Indietro** per tornare indietro e correggere eventuali errori. Fare clic su Avanti per continuare.  

8.  Nella pagina **Informazioni generali** della **Creazione guidata tipo di distribuzione**, specificare informazioni sull'applicazione, come il nome dell'applicazione, commenti e lingue in cui è disponibile il tipo di distribuzione.  

    > [!NOTE]  
    >  Alcune delle informazioni sul tipo di distribuzione potrebbero essere già presenti in questa pagina se sono state ottenute in precedenza dai file di installazione dell'applicazione.  

9. Fare clic su **Avanti**.  

10. Nella pagina **Requisiti** della Creazione guidata tipo di distribuzione, è possibile specificare le condizioni da soddisfare prima di poter installare il tipo di distribuzione sui computer Mac.  

11. Fare clic su **Aggiungi** per aprire la finestra di dialogo **Creazione requisito** e aggiungere un nuovo requisito.  

    > [!NOTE]  
    >  È anche possibile aggiungere nuovi requisiti nella scheda **Requisiti** della finestra di dialogo *Proprietà di***<nome tipo distribuzione\>**.  

12. Dall'elenco a discesa **Categoria** , selezionare che questo requisito riguarda un dispositivo.  

13. Dall'elenco a discesa **Condizione** selezionare la condizione da utilizzare per valutare se il computer Mac soddisfa i requisiti di installazione. Il contenuto di questo elenco varia a seconda della categoria selezionata.  

14. Dall'elenco a discesa **Operatore** scegliere l'operatore da utilizzare per confrontare la condizione selezionata con il valore specificato per valutare se l'utente o il dispositivo soddisfano i requisiti d'installazione. Gli operatori disponibili variano a seconda della condizione selezionata.  

15. Nel campo **Valore** specificare i valori da utilizzare con la condizione e l'operatore selezionati per valutare se l'utente o il dispositivo soddisfano i requisiti d'installazione.  I valori disponibili variano a seconda della condizione e dell'operatore selezionati.  

16. Fare clic su **OK** per salvare la regola requisito e chiudere la finestra di dialogo **Creazione requisito** .  

17. Nella pagina **Requisiti** della **Creazione guidata tipo di distribuzione**fare clic su **Avanti**.  

18. Nella pagina **Riepilogo** della **Creazione guidata tipo di distribuzione**esaminare le azioni che saranno eseguite nella procedura guidata.  Se necessario, fare clic su **Indietro** per tornare indietro e modificare le impostazioni del tipo di distribuzione. Fare clic su **Avanti** per creare il tipo di distribuzione.  

19. Al termine della pagina **Avanzamento** esaminare le azioni eseguite e fare clic su **Chiudi** per completare la procedura **Creazione guidata tipo di distribuzione**.  

20. Se tale procedura guidata è stata avviata da **Creazione guidata applicazione**, verrà visualizzata di nuovo la pagina **Tipi di distribuzione**.  

###  <a name="deploy-the-mac-application"></a>Distribuire l'applicazione Mac  
 I passaggi per distribuire un'applicazione nei computer Mac sono gli stessi di quelli utilizzati per distribuire un'applicazioni nei computer Windows, tranne per le differenze riportate di seguito.  

-   La distribuzione di applicazioni in utenti non è supportata.  

-   Le distribuzioni con scopo **Disponibile** non sono supportate.  

-   L'opzione **Pre-distribuisci il software nel dispositivo primario dell'utente** nella pagina **Impostazioni distribuzione** della Distribuzione guidata del software non è supportata.  

-   Poiché il computer Mac non supportano Software Center, l'impostazione **Notifiche utente** nella pagina **Esperienza utente** della Distribuzione guidata del software viene ignorata.  

-   L'opzione per inviare pacchetti di riattivazione quando si distribuisce software non è supportata per i computer Mac.  

> [!NOTE]  
>  È possibile creare una raccolta che contenga solo i computer Mac. Per farlo, creare una raccolta che usi una regola di query e usare la query WQL di esempio illustrata nell'argomento [Come creare query](../../core/servers/manage/create-queries.md).  

 Per altre informazioni, vedere l'argomento relativo alla [distribuzione delle applicazioni](../../apps/deploy-use/deploy-applications.md).  

###  <a name="step-5-monitor-the-deployment-of-the-mac-application"></a>Passaggio 5: Monitorare la distribuzione dell'applicazione Mac  
 È possibile utilizzare lo stesso processo per monitorare le distribuzioni di applicazioni nei computer Mac delle distribuzioni di applicazioni nei computer Windows.  

 Per altre informazioni, vedere l'argomento relativo al [monitoraggio delle applicazioni](/sccm/apps/deploy-use/monitor-applications-from-the-console).  



<!--HONumber=Dec16_HO3-->



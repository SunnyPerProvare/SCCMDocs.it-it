---
title: Distribuire manualmente gli aggiornamenti software | Documentazione Microsoft
description: Per distribuire manualmente gli aggiornamenti, selezionare gli aggiornamenti dalla console di Configuration Manager e distribuirli manualmente o aggiungere gli aggiornamenti a un gruppo di aggiornamento e distribuire il gruppo.
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 12/07/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: 57184274-5fea-4d79-a2b4-22e08ed26daf
ms.openlocfilehash: 2a0d5f12b99689749833c109d4fa399f99451d8a
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
#  <a name="BKMK_ManualDeploy"></a> Distribuire manualmente gli aggiornamenti software  

*Si applica a: System Center Configuration Manager (Current Branch)*

 La distribuzione manuale degli aggiornamenti software consiste nel processo di selezione degli aggiornamenti software dalla console di Configuration Manager e di avvio manuale del processo di distribuzione. In alternativa, è possibile aggiungere gli aggiornamenti software selezionati a un gruppo di aggiornamento, quindi distribuire manualmente il gruppo di aggiornamento. In genere si usa la distribuzione manuale per mantenere aggiornati i dispositivi client con gli aggiornamenti software richiesti prima di creare ADR che gestiranno le distribuzioni degli aggiornamenti software mensili in corso. Si utilizzerà inoltre un metodo manuale per distribuire gli aggiornamenti software fuori banda. Per altre informazioni su come determinare il metodo di distribuzione da usare, vedere [Distribuire gli aggiornamenti software](deploy-software-updates.md).

 Le sezioni seguenti descrivono i passaggi per distribuire manualmente gli aggiornamenti software.  

##  <a name="BKMK_1SearchCriteria"></a> Passaggio 1: Specificare i criteri di ricerca per gli aggiornamenti software  
 Esistono potenzialmente migliaia di aggiornamenti software visualizzati nella console di Configuration Manager. Il primo passaggio del flusso di lavoro per la distribuzione manuale degli aggiornamenti software consiste nell'identificare gli aggiornamenti software che si desidera distribuire. Ad esempio, si potrebbero fornire criteri che recuperino tutti gli aggiornamenti software richiesti su oltre 50 dispositivi client e che abbiano **Sicurezza** o **Errore critico** come classificazione di aggiornamento software.  

> [!IMPORTANT]  
>  Il numero massimo di aggiornamenti software che possono essere inclusi in una distribuzione di aggiornamenti software singola è 1.000.  

#### <a name="to-specify-search-criteria-for-software-updates"></a>Per specificare i criteri di ricerca per gli aggiornamenti software  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro Raccolta software, espandere **Aggiornamenti software**, quindi fare clic su **Tutti gli aggiornamenti software**. Vengono visualizzati gli aggiornamenti software sincronizzati.  

    > [!NOTE]  
    >  Nel nodo **Tutti gli aggiornamenti software** Configuration Manager visualizza solo gli aggiornamenti software con classificazione **Critico** e **Sicurezza** rilasciati negli ultimi 30 giorni.  

3.  Nel riquadro di ricerca, applicare il filtro per identificare gli aggiornamenti software necessari usando uno o entrambi i seguenti passaggi:  

    -   Nella casella di testo di ricerca, digitare una stringa di ricerca che consenta di filtrare gli aggiornamenti software. Ad esempio, digitare l'ID articolo o l'ID bollettino per un aggiornamento software specifico oppure inserire una stringa che verrebbe visualizzata nel titolo per diversi aggiornamenti software.  

    -   Fare clic su **Aggiungi criteri**, selezionare i criteri che si desidera usare per filtrare gli aggiornamenti software, fare clic su **Aggiungi**, quindi fornire i valori per i criteri.  

4.  Fare clic su **Cerca** per filtrare gli aggiornamenti software.  

    > [!TIP]  
    >  È disponibile l'opzione per salvare i criteri di filtro nella scheda **Cerca** e nel gruppo **Salva** .  

##  <a name="BKMK_2UpdateGroup"></a> Passaggio 2: Creare un gruppo di aggiornamenti software che contenga gli aggiornamenti software  
 I gruppi di aggiornamento software forniscono un metodo efficace per organizzare gli aggiornamenti software in preparazione per la distribuzione. È possibile aggiungere manualmente aggiornamenti software a un gruppo di aggiornamento software oppure Configuration Manager può aggiungere automaticamente aggiornamenti software a un gruppo di aggiornamento software nuovo o esistente usando un'ADR. Usare le procedure seguenti per aggiungere manualmente gli aggiornamenti software in un nuovo gruppo di aggiornamento software.  

#### <a name="to-manually-add-software-updates-to-a-new-software-update-group"></a>Per aggiungere manualmente gli aggiornamenti software a un nuovo gruppo di aggiornamento software  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro Raccolta software, fare clic su **Aggiornamenti Software**.  

3.  Selezionare gli aggiornamenti software che devono essere aggiunti al nuovo gruppo di aggiornamento software.  

4.  Nella scheda **Home** , nel gruppo **Aggiorna** , fare clic su **Crea gruppo di aggiornamento software**.  

5.  Specificare il nome per il gruppo di aggiornamento software e fornire una descrizione facoltativa. Usare un nome e una descrizione che forniscano informazioni sufficienti per determinare il tipo di aggiornamenti software che si trovano nel gruppo di aggiornamento software. Per continuare, fare clic su **Crea**.  

6.  Fare clic sul nodo **Gruppi di aggiornamenti software** per visualizzare il nuovo gruppo di aggiornamento software.  

7.  Selezionare il gruppo di aggiornamento software, quindi nella scheda **Home** , nel gruppo **Aggiorna** , fare clic su **Mostra membri** per visualizzare un elenco degli aggiornamenti software inclusi nel gruppo.  

##  <a name="BKMK_3DownloadContent"></a> Passaggio 3: Scaricare il contenuto per il gruppo di aggiornamenti software  
 Facoltativamente, prima di distribuire gli aggiornamenti software, è possibile scaricare il contenuto per gli aggiornamenti software inclusi nel gruppo di aggiornamento software. È possibile scegliere di effettuare questa operazione in modo da poter verificare che il contenuto sia disponibile nei punti di distribuzione prima di distribuire gli aggiornamenti software. Ciò consentirà di evitare eventuali problemi imprevisti con la distribuzione del contenuto. È possibile ignorare questo passaggio e il contenuto verrà scaricato e copiato nei punti di distribuzione come parte del processo di distribuzione. Usare la procedura seguente per scaricare il contenuto per gli aggiornamenti software nel gruppo di aggiornamento software.  



#### <a name="to-download-content-for-the-software-update-group"></a>Per scaricare il contenuto per il gruppo di aggiornamento software
[!INCLUDE[downloadupdates](..\includes\downloadupdates.md)]
<!--- 1.  In the Configuration Manager console, click **Software Library**.  

2.  In the Software Library workspace, expand **Software Updates**, and click **Software Update Groups**.  

3.  Select the software update group for which you want to download content.  

4.  On the **Home** tab, in the **Update Group** group, click **Download**. The **Download Software Updates Wizard** opens.  

5.  On the **Deployment Package** page, configure the following settings:  

    1.  **Select deployment package**: Select this setting to use an existing deployment package for the software updates in the deployment.  

        > [!NOTE]  
        >  Software updates that have already been downloaded to the selected deployment package are not downloaded again.  

    2.  **Create a new deployment package**: Select this setting to create a new deployment package for the software updates in the deployment. Configure the following settings:  

        -   **Name**: Specifies the name of the deployment package. This must be a unique name that describes the package content. It is limited to 50 characters.  

        -   **Description**: Specifies the description of the deployment package. The package description provides information about the package contents and is limited to 127 characters.  

        -   **Package source**: Specifies the location of the software update source files.  Type a network path for the source location, for example, **\\\server\sharename\path**, or click **Browse** to find the network location. You must create the shared folder for the deployment package source files before you proceed to the next page.  

            > [!NOTE]  
            >  The deployment package source location that you specify cannot be used by another software deployment package.  

            > [!IMPORTANT]  
            >  The SMS Provider computer account and the user that is running the wizard to download the software updates must both have **Write** NTFS permissions on the download location. You should carefully restrict access to the download location in order to reduce the risk of attackers tampering with the software update source files.  

            > [!IMPORTANT]  
            >  You can change the package source location in the deployment package properties after Configuration Manager creates the deployment package. But if you do so, you must first copy the content from the original package source to the new package source location.  

     Click **Next**.  

6.  On the Distribution Points page, select the distribution points or distribution point groups that are used to host the software update files defined in the new deployment package, and then click **Next**.  

7.  On the Distribution Settings page, specify the following settings:  

    -   **Distribution priority**: Use this setting to specify the distribution priority for the deployment package. The distribution priority applies when the deployment package is sent to distribution points at child sites. Distribution packages are sent in priority order: **High**, **Medium**, or **Low**. Packages with identical priorities are sent in the order in which they were created. If there is no backlog, the package will process immediately regardless of its priority. By default, packages are sent using **Medium** priority.  

    -   **Distribute the content for this package to preferred distribution points**: Use this setting to enable on-demand content distribution to preferred distribution points. When this setting is enabled, the management point creates a trigger for the distribution manager to distribute the content to all preferred distribution points when a client requests the content for the package and the content is not available on any preferred distribution points. For more information about preferred distribution points and on-demand content, see [Content source location scenarios](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_CSLscenarios).  

    -   **Prestaged distribution point settings**: Use this setting to specify how you want to distribute content to prestaged distribution points. Choose one of the following options:  

        -   **Automatically download content when packages are assigned to distribution points**: Use this setting to ignore the prestage settings and distribute content to the distribution point.  

        -   **Download only content changes to the distribution point**: Use this setting to prestage the initial content to the distribution point, and then distribute content changes to the distribution point.  

        -   **Manually copy the content in this package to the distribution point**: Use this setting to always prestage content on the distribution point. This is the default setting.  

         For more information about prestaging content to distribution points, see [Use Prestaged content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

     Click **Next**.  

8.  On the Download Location page, specify location that Configuration Manager will use to download the software update source files. As needed, use the following options:  

    -   **Download software updates from the Internet**: Select this setting to download the software updates from the location on the Internet. This is the default setting.  

    -   **Download software updates from a location on the local network**: Select this setting to download software updates from a local folder or shared network folder. Use this setting when the computer running the wizard does not have Internet access.  

        > [!NOTE]  
        >  When you use this setting, download the software updates from any computer with Internet access, and then copy the software updates to a location on the local network that is accessible from the computer running the wizard.  

     Click **Next**.  

9. On the Language Selection page, specify the languages for which the selected software updates are to be downloaded, and then click **Next**. Configuration Manager downloads the software updates only if they are available in the selected languages. Software updates that are not language-specific are always downloaded.  

10. On the Summary page, verify the settings that you selected in the wizard, and then click **Next** to download the software updates.  

11. On the Completion page, verify that the software updates were successfully downloaded, and then click **Close**. --->

#### <a name="to-monitor-content-status"></a>Per monitorare lo stato del contenuto
1. Per monitorare lo stato del contenuto per gli aggiornamenti software, fare clic su **Monitoraggio** nella console di Configuration Manager.  

2. Nell'area di lavoro Monitoraggio, espandere **Stato distribuzione**, quindi fare clic su **Stato contenuto**.  

3. Selezionare il pacchetto di aggiornamento software precedentemente identificato per scaricare gli aggiornamenti software nel gruppo di aggiornamento software.  

4. Nella scheda **Home** , nel gruppo **Contenuto** , fare clic su **Visualizza stato**.  

##  <a name="BKMK_4DeployUpdateGroup"></a> Passaggio 4: Distribuire il gruppo di aggiornamenti software  
 Dopo aver determinato quali aggiornamenti software di desidera distribuire e averli aggiunti a un gruppo di aggiornamento software, è possibile distribuire manualmente gli aggiornamenti software nel gruppo di aggiornamento software. Usare la procedura seguente per distribuire manualmente gli aggiornamenti software in un gruppo di aggiornamento software.  

#### <a name="to-manually-deploy-the-software-updates-in-a-software-update-group"></a>Per distribuire manualmente gli aggiornamenti software in un gruppo di aggiornamento software  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro Raccolta software, espandere **Aggiornamenti software**, quindi fare clic su **Gruppi di aggiornamenti software**.  

3.  Selezionare il gruppo di aggiornamento software che si desidera distribuire.  

4.  Nella scheda **Home** , nel gruppo **Distribuzione** , fare clic su **Distribuisci**. Viene visualizzata la **Distribuzione guidata degli aggiornamenti software** .  

5.  Nella pagina Generale è possibile configurare le seguenti impostazioni:  

    -   **Nome**: specificare il nome per la distribuzione. La distribuzione deve avere un nome univoco che descriva lo scopo della distribuzione e la distingua da altre distribuzioni nel sito di Configuration Manager. Per impostazione predefinita, Configuration Manager specifica automaticamente un nome per la distribuzione nel formato seguente: **Microsoft Software Updates -** <*data*><*ora*>  

    -   **Descrizione**: specificare una descrizione per la distribuzione. La descrizione offre una panoramica della distribuzione, nonché tutte le altre informazioni rilevanti per identificare e distinguere la distribuzione dalle altre nel sito di Configuration Manager. Il campo della descrizione è facoltativo, ha un limite di 256 caratteri e un valore vuoto per impostazione predefinita.  

    -   **Aggiornamento software/gruppo di aggiornamenti software**: verificare che il gruppo di aggiornamento software visualizzato o l'aggiornamento software siano corretti.  

    -   **Seleziona modello di distribuzione**: specificare se applicare un modello di distribuzione precedentemente salvato. È possibile configurare un modello di distribuzione che contenga più proprietà di distribuzione aggiornamenti software comuni, quindi applicare il modello quando si distribuiscono aggiornamenti software successivi per garantire la coerenza tra distribuzioni simili e risparmiare tempo.  

    -   **Raccolta**: specificare la raccolta per la distribuzione, come applicabile. I membri della raccolta ricevono gli aggiornamenti software che vengono definiti nella distribuzione.  

6.  Nella pagina Impostazioni distribuzione, configurare le seguenti impostazioni:  

    -   **Tipo di distribuzione**: specificare il tipo di distribuzione per la distribuzione degli aggiornamenti software. Selezionare **Richiesto** per creare una distribuzione degli aggiornamenti software obbligatoria in cui gli aggiornamenti software vengano automaticamente installati nei client prima della scadenza di un'installazione configurata. Selezionare **Disponibile** per creare una distribuzione degli aggiornamenti software aggiuntiva che gli utenti possano installare da Software Center.  

        > [!IMPORTANT]  
        >  Dopo aver creato la distribuzione degli aggiornamenti software, non è possibile modificare successivamente il tipo di distribuzione.  

        > [!NOTE]  
        >  Un gruppo di aggiornamenti software distribuito come **Richiesto** verrà scaricato in background e rispetterà le impostazioni BITS, se configurate.  
        > I gruppi di aggiornamenti software distribuiti come **Disponibile** verranno invece scaricati in primo piano e ignoreranno le impostazioni BITS.  

    -   **Usa riattivazione LAN per riattivare i client per le distribuzioni richieste**: specificare se abilitare la riattivazione LAN alla scadenza per inviare pacchetti di riattivazione ai computer che richiedono uno o più aggiornamenti software nella distribuzione. Tutti i computer in modalità sospensione all'ora di scadenza dell'installazione verranno riattivati in modo che si possa avviare l'installazione degli aggiornamenti software. I client in modalità sospensione che non richiedono aggiornamenti software nella distribuzione non vengono avviati. Per impostazione predefinita, questa impostazione non viene abilitata ed è disponibile solo quando **Tipo di distribuzione** è impostato su **Richiesto**.  

        > [!WARNING]  
        >  Prima di usare questa opzione, i computer e le reti devono essere configurati per riattivazione LAN.  

    -   **Livello dettaglio**: specificare il livello di dettaglio per i messaggi di stato segnalati dai computer client.  

7.  Nella pagina Pianificazione, è possibile configurare le seguenti impostazioni:  

    -   **Pianificazione valutazione**: specificare se il tempo disponibile e le scadenze dell'installazione sono valutate in base all'ora UTC o all'ora locale del computer su cui è in esecuzione la console di Configuration Manager.  

        > [!NOTE]  
        >  Quando si seleziona l'ora locale e quindi si sceglie **Appena possibile** per **Tempo disponibile software** o **Scadenza installazione**, per valutare quando sono disponibili aggiornamento o quando vengono installati in un client, viene usata l'ora corrente del computer che esegue la console di Configuration Manager. Se il client si trova in un fuso orario diverso, verranno eseguite le azioni seguenti quando l'ora del client raggiunge quella impostata per la valutazione.  

    -   **Tempo disponibile software**: selezionare una delle seguenti impostazioni per specificare quando gli aggiornamenti del software saranno disponibili per i client:  

        -   **Appena possibile**: selezionare questa impostazione per rendere disponibili il prima possibile gli aggiornamenti software nella distribuzione per i client. Quando si crea la distribuzione, i criteri client vengono aggiornati, ai client viene comunicata la distribuzione nel successivo ciclo di polling dei criteri client e, quindi, gli aggiornamenti software sono disponibili per l'installazione.  

        -   **Orario specifico**: selezionare questa impostazione per rendere disponibili gli aggiornamenti software nella distribuzione per i client in una data e a un orario specifici. Quando si crea la distribuzione, i criteri client vengono aggiornati e ai client viene comunicata la distribuzione nel successivo ciclo di polling dei criteri client. Tuttavia, gli aggiornamenti del software nella distribuzione non saranno disponibili per l'installazione prima della data e dell'orario specificati.  

    -   **Scadenza installazione**: selezionare una delle seguenti impostazioni per specificare la scadenza per l'installazione degli aggiornamenti software nella distribuzione.  

        > [!NOTE]  
        >  È possibile configurare l'impostazione della scadenza dell'installazione solo quando **Tipo di distribuzione** è impostato su **Richiesta** nella pagina Impostazioni distribuzione.  

        -   **Appena possibile**: selezionare questa impostazione per installare automaticamente gli aggiornamenti software nella distribuzione appena possibile.  

        -   **Orario specifico**: selezionare questa impostazione per installare automaticamente gli aggiornamenti software nella distribuzione in una data e a un orario specifici.  

        > [!NOTE]  
        >  L'orario di scadenza dell'installazione effettivo corrisponde all'orario specifico configurato più una quantità di tempo casuale di massimo 2 ore. Ciò consente di ridurre il potenziale impatto di un'installazione simultanea degli aggiornamenti software nella distribuzione da parte di tutti i computer client nella raccolta di destinazione.  
        >   
        >  È possibile configurare l'impostazione **Disabilitare sequenza casuale scadenza** del client **Agente computer** per disabilitare il ritardo della sequenza casuale di installazione per gli aggiornamenti software richiesti. Per altre informazioni, vedere [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

8.  Nella pagina Esperienza utente, è possibile configurare le seguenti impostazioni:  

    -   **Notifiche utente**: specificare se visualizzare la notifica degli aggiornamenti software in Software Center sul computer client in base al **Tempo disponibile software** configurato e se visualizzare le notifiche utente sui computer client. Quando **Tipo di distribuzione** è impostato su **Disponibile** nella pagina Impostazioni distribuzione, non è possibile selezionare **Nascondi in Software Center e nascondi tutte le notifiche**.  

    -   **Comportamento scadenza**: *disponibile solo quando **Tipo di distribuzione** *è impostato su **Richiesto**  *nella pagina Impostazioni distribuzione.*   
    specificare il comportamento che deve verificarsi quando si raggiunge la data di scadenza per la distribuzione degli aggiornamenti software. Specificare se installare gli aggiornamenti software nella distribuzione. Inoltre, specificare se eseguire un riavvio del sistema dopo l'installazione dell'aggiornamento software indipendentemente da una finestra di manutenzione configurata. Per altre informazioni sulle finestre di manutenzione, vedere [Come usare le finestre di manutenzione](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportamento riavvio dispositivo**: *disponibile solo quando **Tipo di distribuzione** *è impostato su **Richiesto** *nella pagina Impostazioni distribuzione.*    
    specificare se evitare un riavvio del sistema su server e workstation dopo l'installazione degli aggiornamenti software e se è richiesto un riavvio del sistema per completare l'installazione.  

        > [!IMPORTANT]  
        >  L'inibizione dei riavvii del sistema può essere utile negli ambienti server o nei casi in cui non si desidera che i computer sui quali si stanno installando gli aggiornamenti software vengano riavviati per impostazione predefinita. Tuttavia, tale soluzione potrebbe lasciare i computer in uno stato non protetto, mentre un riavvio forzato assicura il completamento immediato dell'installazione degli aggiornamenti software.

    -   **Gestione filtri di scrittura per dispositivi con Windows Embedded**: quando si distribuiscono aggiornamenti software in dispositivi con Windows Embedded abilitati per i filtri di scrittura, è possibile specificare di installare l'aggiornamento software nella sovrapposizione temporanea e di confermare le modifiche in seguito oppure alla scadenza dell'installazione o all'interno di una finestra di manutenzione. Quando si confermano le modifiche alla scadenza dell'installazione o all'interno di una finestra di manutenzione, è necessario il riavvio per mantenere le modifiche nel dispositivo.  

        > [!NOTE]  
        >  Quando si distribuisce un aggiornamento software in un dispositivo con Windows Embedded, verificare che il dispositivo appartenga a una raccolta che dispone di una finestra di manutenzione configurata.  

    - **Comportamento di rivalutazione della distribuzione degli aggiornamenti software al riavvio**: a partire da Configuration Manager versione 1606, selezionare questa impostazione per configurare le distribuzioni degli aggiornamenti software in modo che i client eseguano un'analisi della conformità degli aggiornamenti software immediatamente dopo l'installazione degli aggiornamenti software e il riavvio. In questo modo, il client controlla la presenza di aggiornamenti software aggiuntivi che diventano applicabili dopo il riavvio e che possono quindi essere installati (e resi conformi) durante la stessa finestra di manutenzione.

9. Nella pagina Avvisi configurare la modalità in cui Configuration Manager e System Center Operations Manager genereranno gli avvisi relativi alla distribuzione. È possibile configurare gli avvisi solo quando **Tipo di distribuzione** è impostato su **Richiesta** nella pagina Impostazioni distribuzione.  

    > [!NOTE]  
    >  È possibile riesaminare gli avvisi recenti sugli aggiornamenti software dal nodo **Aggiornamenti software** nell'area di lavoro **Raccolta software** .  

10. Nella pagina Impostazioni download, configurare le seguenti impostazioni:  

    - Specificare se il client scaricherà e installerà gli aggiornamenti software durante una connessione a una rete lenta o mentre usa un percorso di fallback per il contenuto.  

    - Specificare se il client dovrà scaricare e installare gli aggiornamenti software da un punto di distribuzione di fallback nel caso in cui il contenuto per tali aggiornamenti non fosse disponibile su un punto di distribuzione preferito.  

    - **Consenti ai client di condividere il contenuto con altri client nella stessa subnet**: specificare se consentire l'uso di BranchCache per il download del contenuto. Per altre informazioni su BranchCache, vedere [Concetti di base per la gestione dei contenuti](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **Se gli aggiornamenti software non sono disponibili nel punto di distribuzione nei gruppi correnti, adiacenti o del sito, scaricare il contenuto da Microsoft Updates**: selezionare questa impostazione in modo che i client connessi alla intranet scarichino gli aggiornamenti software da Microsoft Update se non sono disponibili nei punti di distribuzione. I client basati su Internet possono sempre passare a Microsoft Update per il contenuto degli aggiornamenti software.

    - Specificare se consentire ai client di eseguire il download dopo una scadenza dell'installazione quando usano connessioni Internet a consumo. I provider Internet talvolta applicano un addebito per il traffico dati in entrata e in uscita quando si usa una connessione Internet a consumo.  

    > [!NOTE]  
    >  I client richiedono il percorso del contenuto da un punto di gestione per gli aggiornamenti software in una distribuzione. Il comportamento di download dipende dalla configurazione del punto di distribuzione, del pacchetto di distribuzione e delle impostazioni in questa pagina. Per altre informazioni, vedere [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

11. Se si è eseguito il [Passaggio 3: Scaricare il contenuto per il gruppo di aggiornamenti software](#BKMK_3DownloadContent), le pagine Pacchetto di distribuzione, Punti di distribuzione e Selezione lingua non saranno visualizzate e sarà possibile procedere al passaggio 15 della procedura guidata.  

    > [!IMPORTANT]  
    >  Gli aggiornamenti software precedentemente scaricati nella raccolta contenuto sul server del sito non vengono scaricati nuovamente. Questo vale anche quando si crea un nuovo pacchetto di distribuzione per gli aggiornamenti software. Se tutti gli aggiornamenti software sono stati già scaricati in precedenza, la procedura guidata passa alla pagina **Selezione lingua** (passaggio°15).  

12. Nella pagina del Pacchetto di distribuzione, selezionare un pacchetto di distribuzione esistente o configurare le seguenti impostazioni per specificare un nuovo pacchetto di distribuzione:  

    1.  **Nome**: specificare il nome del pacchetto di distribuzione. Deve essere un nome univoco che descrive il contenuto del pacchetto. Deve essere lungo massimo 50 caratteri.  

    2.  **Descrizione**: specificare una descrizione che fornisca informazioni sul pacchetto di distribuzione. La descrizione deve contenere un massimo di 127 caratteri.  

    3.  **Origine pacchetto**: specificare il percorso dei file di origine dell'aggiornamento software.  Digitare un percorso di rete per il percorso di origine, ad esempio **\\\server\nomecondivisione\percorso**oppure fare clic su **Sfoglia** per trovare il percorso di rete. Prima di procedere alla pagina successiva, è necessario creare la cartella condivisa per i file di origine del pacchetto di distribuzione.  

        > [!NOTE]  
        >  Il percorso di origine del pacchetto di distribuzione specificato non può essere usato da un altro pacchetto di distribuzione software.  

        > [!IMPORTANT]  
        >  L'account computer del provider SMS e l'utente che esegue la procedura guidata per scaricare gli aggiornamenti software devono disporre entrambi delle autorizzazioni NTFS di **Scrittura** nel percorso download. È necessario limitare con attenzione l'accesso al percorso download per ridurre il rischio di manomissioni da parte di utenti malintenzionati dei file origine degli aggiornamenti software.  

        > [!IMPORTANT]  
        >  È possibile modificare il percorso di origine del pacchetto nelle proprietà del pacchetto di distribuzione dopo che Configuration Manager ha creato il pacchetto di distribuzione. Ma in tal caso, è prima necessario copiare il contenuto dall'origine del pacchetto originale nel nuovo percorso di origine del pacchetto.  

    4.  **Priorità di invio**: specificare la priorità di invio per il pacchetto di distribuzione. Configuration Manager usa la priorità di invio quando invia il pacchetto di distribuzione ai punti di distribuzione. I pacchetti di distribuzione vengono inviati in ordine di priorità: Alta, Media o Bassa. I pacchetti con priorità identiche vengono inviati nell'ordine in cui sono stati creati. Se non esiste nessun backlog, il pacchetto eseguirà l'elaborazione immediatamente indipendentemente dalla relativa priorità.  

13. Nella pagina Punti di distribuzione, specificare i punti di distribuzione o i gruppi dei punti di distribuzione che ospiteranno i file di aggiornamento software. Per altre informazioni sui punti di distribuzione, vedere [Configurazioni dei punti di distribuzione](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

14. Nella pagina Percorso download, specificare se scaricare i file di aggiornamento software da Internet o dalla rete locale. Configurare le seguenti impostazioni:  

    -   **Scarica aggiornamenti software da Internet**: selezionare questa impostazione per scaricare gli aggiornamenti software da un percorso specificato su Internet. Questa opzione è attivata per impostazione predefinita.  

    -   **Scarica aggiornamenti software da un percorso sulla rete locale**: selezionare questa impostazione per scaricare gli aggiornamenti software da una cartella locale o una cartella di rete condivisa. Questa impostazione è utile quando il computer che esegue la procedura guidata non dispone di accesso a Internet. Gli aggiornamenti software possono essere scaricati preventivamente da qualsiasi computer con accesso a Internet e memorizzati sulla rete locale per poi accedervi per l'installazione.  

15. Nella pagina Selezione lingua selezionare le lingue per cui vengono scaricati gli aggiornamenti software selezionati. Gli aggiornamenti software vengono scaricati solo se sono disponibili nelle lingue selezionate. Gli aggiornamenti software non specifici per la lingua vengono sempre scaricati. Per impostazione predefinita, la procedura guidata consente di selezionare le lingue configurate nelle proprietà del punto di aggiornamento software. Prima di procedere alla pagina successiva, è necessario selezionare almeno una lingua. Quando si selezionano solo lingue non supportate da un aggiornamento software, il download dell'aggiornamento software avrà esito negativo.  

16. Nella pagina Riepilogo, esaminare le impostazioni. Per salvare le impostazioni in un modello di distribuzione, fare clic su **Salva come modello**, immettere un nome e selezionare le impostazioni da includere nel modello, quindi fare clic su **Salva**. Per modificare un'impostazione configurata, fare clic sulla pagina della procedura guidata associata e modificare l'impostazione.  

    > [!WARNING]  
    >  Il nome modello può essere composto da caratteri ASCII alfanumerici così come da **\\** (barra rovesciata) o **‘** (virgoletta singola).  

17. Fare clic su **Avanti** per distribuire l'aggiornamento software.  

 Dopo aver completato la procedura guidata, Configuration Manager scarica gli aggiornamenti software nella raccolta contenuto sul server del sito, distribuisce gli aggiornamenti software nei punti di distribuzione configurati e quindi distribuisce il gruppo di aggiornamento software nei client della raccolta di destinazione. Per altre informazioni sul processo di distribuzione, vedere [Software update deployment process](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).

## <a name="next-steps"></a>Passaggi successivi
[Monitorare gli aggiornamenti software](monitor-software-updates.md)

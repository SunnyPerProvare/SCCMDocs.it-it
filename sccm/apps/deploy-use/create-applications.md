---
title: Creare applicazioni
titleSuffix: Configuration Manager
description: Creare e distribuire applicazioni e tipi di distribuzione con System Center Configuration Manager.
ms.custom: na
ms.date: 11/07/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
caps.latest.revision: "14"
caps.handback.revision: "0"
author: mattbriggs
ms.author: mabrigg
manager: angrobe
ms.openlocfilehash: f680b692f3ae92fb8a5e8b6640ed053ceedba436
ms.sourcegitcommit: 12d0d53e47bbf1a0bbd85015b8404a44589d1e14
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2017
---
# <a name="create-applications-with-system-center-configuration-manager"></a>Creare applicazioni con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Un'applicazione di System Center Configuration Manager contiene i file e le informazioni necessarie per distribuire software in un dispositivo. Un'applicazione contiene uno o più tipi di distribuzione che comprendono i file di installazione e le informazioni necessarie per installare il software. Un tipo di distribuzione contiene anche le regole che specificano quando e come deve essere distribuito il software.  

 È possibile creare applicazioni usando due metodi:  

-   Creare automaticamente i tipi di applicazione e di distribuzione leggendo i file di installazione dell'applicazione.  

-   Creare manualmente l'applicazione e quindi aggiungere tipi di distribuzione in un secondo momento.  

-   Importare un'applicazione da un file.  

> [!NOTE]  
>  L'articolo [Creare applicazioni per dispositivi mobili](../../mdm/deploy-use/create-applications.md) contiene informazioni dettagliate sulla creazione di applicazioni iOS, Windows Phone e Android.  

Usare la procedura seguente per creare le applicazioni e i tipi di distribuzione usando Configuration Manager.  

## <a name="start-the-create-application-wizard"></a>Avviare la Creazione guidata applicazione  

1.  Nella console di Configuration Manager scegliere **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.  

3.  Nella scheda **Home**, nel gruppo **Crea**, scegliere **Crea applicazione**.  

## <a name="specify-whether-you-want-to-automatically-detect-application-information-or-manually-define-the-information"></a>specificare se si desidera rilevare automaticamente le informazioni sull'applicazione o definirle manualmente.  

-   Rilevare automaticamente le informazioni sull'applicazione quando si vuole creare un'applicazione semplice con un solo tipo di distribuzione, ad esempio un file Windows Installer senza dipendenze o requisiti. Dopo aver creato un'applicazione usando questa procedura, è possibile apportare le modifiche necessarie per aggiungere o modificare i tipi di distribuzione e aggiungere metodi di rilevamento, dipendenze o requisiti.  

-   Specificare manualmente le informazioni dell'applicazione per creare applicazioni più complesse con più tipi di distribuzione, dipendenze, metodi di rilevamento o requisiti.  

### <a name="automatically-detect-application-information"></a>Rilevare automaticamente le informazioni sull'applicazione  

1.  Nella pagina **Generale** della Creazione guidata applicazione selezionare **Rileva automaticamente le informazioni sull'applicazione dai file di installazione**.  

2.  Dall'elenco a discesa **Tipo** , scegliere il tipo di file di installazione dell'applicazione che si desidera usare per rilevare le informazioni sull'applicazione. Per informazioni sui tipi di installazione disponibili, vedere [Tipi di distribuzione supportati da Configuration Manager](/sccm/apps/deploy-use/create-applications#deployment-types-supported-by-configuration-manager) in questo argomento.  

3.  Nella casella **Percorso** specificare il percorso UNC nel formato *\\\\server\\condivisione\\\nomefile* oppure il collegamento allo Store per il file di installazione dell'applicazione da usare per rilevare le informazioni sull'applicazione. In alternativa, fare clic su **Sfoglia** per selezionare il file di installazione.  

    > [!IMPORTANT]  
    >  Quando si seleziona **Windows Installer (\*file .msi)** come tipo di applicazione, tutti i file nella cartella specificata vengono importati con l'applicazione e inviati ai punti di distribuzione. Verificare che la cartella specificata contenga solo i file necessari per installare l'applicazione. Configuration Manager è testato per supportare fino a 20.000 file applicazione nel pacchetto dell'applicazione. Se l'applicazione contiene più file, è consigliabile creare più applicazioni con un numero inferiore di file.  

    >  È necessario avere accesso al percorso UNC che contiene l'applicazione e alle eventuali sottocartelle del contenuto dell'applicazione.  

4.  Nella pagina **Importazione informazioni** della Creazione guidata applicazione, rivedere le informazioni importate e quindi fare clic su **Avanti**. Se necessario, è possibile scegliere **Indietro** per tornare indietro e correggere eventuali errori.  

5.  Nella pagina **Informazioni generali** della Creazione guidata applicazione specificare le informazioni seguenti:  

    > [!NOTE]  
    >  Alcune di queste informazioni potrebbero essere già state popolate qui se sono state ottenute automaticamente dai file di installazione dell'applicazione. Inoltre, le opzioni visualizzate potrebbero essere diverse a seconda del tipo di applicazione creata.  

    -   Informazioni generali sull'applicazione, ad esempio nome dell'applicazione, commenti, versione e riferimenti facoltativi che consentano di individuare l'applicazione nella console di Configuration Manager.  

    -   **Programma di installazione**: specificare il programma di installazione e le eventuali proprietà necessarie per installare il tipo di distribuzione dell'applicazione.  

        > [!TIP]  
        >  Se il programma di installazione non viene visualizzato, scegliere **Sfoglia** e selezionare il percorso del programma di installazione.  

    -   **Comportamento installazione**: specificare se il tipo di distribuzione dell'applicazione verrà installato per l'utente attualmente connesso oppure per tutti gli utenti. È anche possibile specificare che il tipo di distribuzione venga installato per tutti gli utenti se viene distribuito in un dispositivo o solo per un utente specifico se viene distribuito a un utente.  

    -   **Usa una connessione VPN automatica (se configurata)**: se nel dispositivo in cui viene avviata l'app è stato distribuito un profilo VPN, avviare la connessione VPN all'avvio dell'app (solo Windows 8.1 e Windows Phone 8.1).  

         Nei dispositivi Windows Phone 8.1 le connessioni VPN automatiche non sono supportate se sono stati distribuiti più profili VPN nel dispositivo.  

         Per altre informazioni sui profili VPN, vedere [Profili VPN](../../protect/deploy-use/vpn-profiles.md).  

6.  Scegliere **Avanti**, riesaminare le informazioni sull'applicazione nella pagina **Riepilogo** e quindi terminare la Creazione guidata applicazione.  

La nuova applicazione viene visualizzata nel nodo **Applicazioni** della console di Configuration Manager. Il processo di creazione dell'applicazione è terminato. Se si vogliono aggiungere altri tipi di distribuzione all'applicazione, vedere [Creare tipi di distribuzione per l'applicazione](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application) in questo argomento.  

### <a name="manually-specify-application-information"></a>Specificare manualmente le informazioni sull'applicazione  

1.  Nella pagina **Generale** della Creazione guidata applicazione, selezionare **Specifica manualmente le informazioni dell'applicazione** e quindi scegliere **Avanti**.  

2.  Specificare informazioni generali sull'applicazione, ad esempio nome dell'applicazione, commenti, versione e riferimenti facoltativi che consentano di individuare l'applicazione nella console di Configuration Manager.  

3.  Nella pagina **Catalogo applicazioni** della Creazione guidata applicazione specificare le informazioni seguenti:  

    -   **Lingua selezionata**: dall'elenco a discesa selezionare la lingua dell'applicazione che si vuole configurare. Scegliere **Aggiungi/Rimuovi** per configurare più lingue per l'applicazione.  

    -   **Nome dell'applicazione localizzata**: specificare il nome dell'applicazione nella lingua selezionata nell'elenco a discesa **Lingua selezionata**.  

        > [!IMPORTANT]  
        >  È necessario specificare il nome dell'applicazione localizzata per ogni lingua che si vuole configurare.  

    -   **Categorie utente**: scegliere **Modifica** per specificare le categorie dell'applicazione nella lingua selezionata nell'elenco a discesa **Lingua selezionata**. Gli utenti di Software Center possono usare queste categorie selezionate per filtrare e ordinare le applicazioni disponibili.  

    -   **Documentazione utente**: scegliere **Sfoglia** per specificare l'URL o il percorso UNC e il nome del file che gli utenti di Software Center possono leggere per ottenere altre informazioni su questa applicazione.  

    -   **Testo collegamento**: specificare il testo che verrà visualizzato al posto dell'URL dell'applicazione.  

    -   **Application Privacy URL** (URL privacy applicazione): specificare l'URL di collegamento all'informativa sulla privacy dell'applicazione.  

    -   **Descrizione localizzata**: immettere una descrizione per questa applicazione nella lingua selezionata nell'elenco a discesa **Lingua selezionata**.  

    -   **Parole chiave**: immettere un elenco di parole chiave nella lingua selezionata nell'elenco a discesa **Lingua selezionata** . Queste parole chiave permetteranno agli utenti di Software Center di cercare l'applicazione.  

    -   **Icona**: scegliere **Sfoglia** per selezionare un'icona per l'applicazione tra le icone disponibili. Se non si specifica un'icona, verrà usata un'icona predefinita per questa applicazione. È ora possibile impostare un'icona con dimensioni fino a 512x512 pixel.

    -   **Visualizza come app in primo piano ed evidenziala nel portale aziendale**: selezionare questa opzione per visualizzare l'app in primo piano nel portale aziendale.  

4.  Nella pagina **Tipi di distribuzione** della Creazione guidata applicazione scegliere **Aggiungi** per creare un nuovo tipo di distribuzione.  

 Per altre informazioni, vedere [Creare tipi di distribuzione per l'applicazione](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application).  

5.  Scegliere **Avanti**, riesaminare le informazioni sull'applicazione nella pagina **Riepilogo** e quindi terminare la Creazione guidata applicazione.  

La nuova applicazione viene visualizzata nel nodo **Applicazioni** della console di Configuration Manager.  

##  <a name="create-deployment-types-for-the-application"></a>Creare tipi di distribuzione per l'applicazione  
 Se si seleziona **Rileva automaticamente le informazioni sul tipo di distribuzione dai file di installazione** nella pagina **Generale** della Creazione guidata tipo di distribuzione, potrebbe non essere necessario completare alcuni passaggi delle procedure seguenti.  

## <a name="start-the-create-deployment-type-wizard"></a>Avviare la Creazione guidata tipo di distribuzione  

1.  Nella console di Configuration Manager scegliere **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.  

3.  Selezionare un'applicazione e quindi nel gruppo **Applicazione** della scheda **Home** fare clic su **Crea tipo di distribuzione**.  

> [!TIP]  
>  È anche possibile avviare la Creazione guidata tipo di distribuzione dalla Creazione guidata applicazione e dalla scheda **Tipi di distribuzione** della finestra di dialogo *Proprietà\>* **nome applicazione**.  

## <a name="specify-whether-you-want-to-automatically-detect-deployment-type-information-or-manually-set-up-the-information"></a>Specificare se si desidera rilevare automaticamente le informazioni sul tipo di distribuzione o impostare manualmente le informazioni  
 Usare una delle seguenti procedure per rilevare automaticamente o per impostare manualmente le informazioni sul tipo di distribuzione.  

### <a name="automatically-detect-deployment-type-information"></a>Rilevare automaticamente le informazioni sul tipo di distribuzione  

1.  Nella pagina **Generale** della Creazione guidata tipo di distribuzione selezionare **Rileva automaticamente le informazioni sul tipo di distribuzione dai file di installazione**.  

2.  Nella casella **Tipo** selezionare il tipo di file di installazione dell'applicazione che si vuole usare per rilevare le informazioni sul tipo di distribuzione.  

3.  Nella casella **Percorso** specificare il percorso UNC nel formato *\\\\server\\condivisione\\nomefile* oppure il collegamento allo Store per i file di installazione dell'applicazione e il contenuto che si vuole usare per rilevare le informazioni sul tipo di distribuzione. È anche possibile scegliere **Sfoglia** per individuare il file di installazione.  

    > [!NOTE]  
    >  È necessario avere accesso al percorso UNC che contiene l'applicazione e alle eventuali sottocartelle del contenuto dell'applicazione.  

4.  Nella pagina **Importazione informazioni** della Creazione guidata tipo di distribuzione riesaminare le informazioni importate e quindi fare clic su **Avanti**. È anche possibile scegliere **Indietro** per tornare indietro e correggere eventuali errori.  

5.  Nella pagina **Informazioni generali** della Creazione guidata tipo di distribuzione, specificare le informazioni seguenti:  

    > [!NOTE]  
    >  Alcune delle informazioni sul tipo di distribuzione potrebbero già essere presenti se sono state lette dai file di installazione dell'applicazione. Le opzioni visualizzate, poi, potrebbero variare a seconda del tipo di distribuzione che si sta creando.  

    -   Informazioni generali sul tipo di distribuzione, ad esempio il nome, i commenti dell'amministratore e le lingue disponibili.  

    -   **Programma di installazione**: specificare il programma di installazione e le eventuali proprietà necessarie per installare il tipo di distribuzione.  

    -   **Comportamento installazione**: specificare se installare il tipo di distribuzione per l'utente corrente oppure per tutti gli utenti. È inoltre possibile specificare se installare il tipo di distribuzione per tutti gli utenti se viene distribuito a un dispositivo oppure se installare il tipo di distribuzione per un utente solo se viene distribuito a un utente.  

    -   **Usa una connessione VPN automatica (se configurata)**: se nel dispositivo in cui viene avviata l'app è stato distribuito un profilo VPN, avviare la connessione VPN all'avvio dell'app (solo Windows 8.1 e Windows Phone 8.1). Se sono stati distribuiti più profili VPN a un dispositivo Windows 8.1, per impostazione predefinita viene usato il primo profilo VPN distribuito.  

         Nei dispositivi Windows Phone 8.1 le connessioni VPN automatiche non sono supportate se sono stati distribuiti più profili VPN nel dispositivo.  

         Per altre informazioni sui profili VPN, vedere [Profili VPN in System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md).  

6.  Scegliere **Avanti** e quindi continuare con la procedura [Specificare le opzioni di contenuto per il tipo di distribuzione](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type).  

### <a name="manually-set-up-the-deployment-type-information"></a>Specificare manualmente le informazioni sul tipo di distribuzione  

1.  Nella pagina **Generale** della Creazione guidata tipo di distribuzione selezionare **Specifica manualmente le informazioni sul tipo di distribuzione**.  

2.  Nella casella **Tipo** scegliere il tipo di file di installazione dell'applicazione che si vuole usare per rilevare le informazioni sul tipo di distribuzione. È possibile scegliere gli stessi tipi di installazione usati quando si rilevano automaticamente le informazioni sul tipo di distribuzione e anche specificare uno script per installare il tipo di distribuzione.  

3.  Nella pagina **Informazioni generali** della Creazione guidata tipo di distribuzione specificare un nome per il tipo di distribuzione, una descrizione facoltativa e le lingue in cui si vuole rendere disponibile questo tipo di distribuzione e quindi fare clic su **Avanti**.  

4.  Continuare con [Specificare le opzioni di contenuto per il tipo di distribuzione](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type).  

##  <a name="specify-content-options-for-the-deployment-type"></a>Specificare le opzioni di contenuto per il tipo di distribuzione  

1.  Nella pagina **Contenuto** della Creazione guidata tipo di distribuzione specificare le informazioni seguenti:  

    -   **Percorso dei contenuti**: specificare il percorso del contenuto per questo tipo di distribuzione o selezionare **Sfoglia** per scegliere la cartella del contenuto del tipo di distribuzione.  

        > [!IMPORTANT]  
        >  L'account di sistema del computer server del sito deve disporre delle autorizzazioni per il percorso del contenuto specificato.  

    -   **Impostazioni del contenuto di disinstallazione**: specificare una delle opzioni seguenti:
        - **Uguale al contenuto di installazione**: selezionare questa opzione se il contenuto di installazione e di disinstallazione è lo stesso. Questo è il comportamento predefinito.
        - **Nessun contenuto di disinstallazione**: selezionare questa opzione se l'applicazione non richiede contenuti per la disinstallazione.
        - **Diversa dal contenuto di installazione**: selezionare questa opzione se il contenuto di disinstallazione è diverso dal contenuto di installazione.

4. Se si seleziona **Diversa dal contenuto di installazione**, selezionare o immettere il percorso del contenuto dell'applicazione che viene usato per disinstallare l'applicazione.
5. Fare clic su **OK** per chiudere la finestra di dialogo delle proprietà del tipo di distribuzione.

    -   **Rendi permanente il contenuto nella cache client**: selezionare questa opzione per specificare se il contenuto deve essere conservato nella cache del computer client a tempo indeterminato, anche se è già stato eseguito. Anche se questa opzione può risultare utile con alcune distribuzioni, ad esempio con il software basato su Windows Installer per cui deve essere disponibile una copia di origine locale per l'applicazione degli aggiornamenti, ridurrà tuttavia lo spazio disponibile della cache. Se si seleziona questa opzione, una distribuzione di grandi dimensioni potrebbe non riuscire in un momento successivo se lo spazio disponibile della cache non è sufficiente.  

    -   **Consenti ai client di condividere il contenuto con altri client nella stessa subnet**: selezionare questa opzione per ridurre il carico sulla rete consentendo ai client di scaricare il contenuto da altri client locali nella rete che hanno già scaricato e memorizzato nella cache il contenuto. Questa opzione usa la tecnologia Windows BranchCache.  

    -   **Programma di installazione**: specificare il nome del programma di installazione ed eventuali parametri di installazione necessari oppure scegliere **Sfoglia** per individuare il file di installazione.  

    -   **Avvio installazione da**: specificare la cartella che contiene il programma di installazione per il tipo di distribuzione (facoltativo). Questa cartella può corrispondere a un percorso assoluto nel client o al percorso della cartella del punto di distribuzione contenente i file di installazione.  

    -   **Programma di disinstallazione**: specificare il nome del programma di disinstallazione ed eventuali parametri obbligatori oppure scegliere **Sfoglia** per individuare il programma (facoltativo).  

    -   **Avvio disinstallazione da**: specificare la cartella che contiene il programma di disinstallazione per il tipo di distribuzione (facoltativo). Questa cartella può essere un percorso assoluto sul client o un percorso relativo alla cartella del punto di distribuzione contenente il pacchetto.  

    -   **Esegui l'installazione e disinstalla il programma come processo a 32 bit su client a 64 bit**: usare il file a 32 bit e i percorsi del Registro di sistema nei computer Windows per eseguire il programma di installazione per il tipo di distribuzione.  

2.  Scegliere **Avanti**.  

## <a name="set-up-detection-methods-to-indicate-the-presence-of-the-deployment-type-windows-pcs-only"></a>Impostare i metodi di rilevamento per indicare la presenza del tipo di distribuzione (solo PC Windows)  
 Questa procedura consente di impostare un metodo di rilevamento che indica se il tipo di distribuzione è già installato.  

1.  Nella pagina **Metodo di rilevamento** della Creazione guidata tipo di distribuzione selezionare **Configura regole per rilevare la presenza del tipo di distribuzione** e quindi scegliere **Aggiungi clausola**.  

    > [!NOTE]  
    >  È anche possibile selezionare **Utilizza uno script personalizzato per rilevare la presenza del tipo di distribuzione**. Per altre informazioni, vedere [Usare uno script personalizzato per determinare la presenza di un tipo di distribuzione](/sccm/apps/deploy-use/create-applications#Use-a-custom-script-to-check-for-the-presence-of-a-deployment-type) in questo argomento.  

2.  Nell'elenco a discesa **Tipo di impostazione** della finestra di dialogo **Regola di rilevamento**, selezionare il metodo che si vuole usare per rilevare la presenza del tipo di distribuzione. È possibile scegliere tra i seguenti metodi disponibili:  

    -   **File System**: usare questo metodo per rilevare se è presente un file o una cartella in un dispositivo client, a indicare che l'applicazione è installata.  

        > [!NOTE]  
        >  Il tipo di impostazione **File system** non supporta l'indicazione di un percorso UNC di una condivisione di rete nel campo Percorso. È possibile specificare solo un percorso locale sul dispositivo client.  
        >   
        >  Per controllare i percorsi dei file a 32 bit per il file o la cartella specificata, selezionare prima di tutto l'opzione **Il file o la cartella sono associati a un'applicazione a 32 bit su sistemi a 64 bit**. Se il file o la cartella non vengono trovati, verrà eseguita una ricerca nei percorsi a 64 bit.  

    -   **Registro di sistema**: usare questo metodo per rilevare la presenza di una chiave o di un valore del Registro di sistema in un dispositivo client, confermando in tal modo l'installazione dell'applicazione.  

        > [!NOTE]  
        >  Per controllare i percorsi del Registro di sistema a 32 bit per la chiave del Registro di sistema specificata, selezionare prima di tutto l'opzione **La chiave del Registro di sistema è associata a un'applicazione a 32 bit su sistemi a 64 bit**. Se la chiave del Registro di sistema non viene trovata, verrà eseguita una ricerca nei percorsi a 64 bit.  

    -   **Windows Installer**: usare questo metodo per rilevare la presenza di un file Windows Installer specificato in un dispositivo client, a indicare che l'applicazione è installata.  

3.  Specificare i dettagli sull'elemento che si desidera usare per verificare se questo tipo di distribuzione è installato. Ad esempio, è possibile usare un file, una cartella, una chiave o un valore del Registro di sistema o un codice prodotto di Windows Installer.  

4.  Specificare i dettagli sul valore che si desidera valutare rispetto all'elemento usato per verificare se è installato questo tipo di distribuzione. Ad esempio, se si usa un file per controllare se il tipo di distribuzione è installato, è possibile selezionare **L'impostazione del file system deve essere presente nel sistema di destinazione per indicare la presenza dell'applicazione**.  

5.  Scegliere **Avanti** per chiudere la finestra di dialogo **Regola di rilevamento**.  

###  <a name="use-a-custom-script-to-check-for-the-presence-of-a-deployment-type"></a>Usare uno script personalizzato per determinare la presenza di un tipo di distribuzione  

1.  Nella pagina **Metodo di rilevamento** della Creazione guidata tipo di distribuzione selezionare la casella **Utilizza uno script personalizzato per rilevare la presenza del tipo di distribuzione** e quindi scegliere **Modifica**.  

2.  Nell'elenco a discesa **Tipo di script** della finestra di dialogo **Editor dello script**selezionare la lingua dello script che si vuole usare per rilevare il tipo di distribuzione dall'elenco a discesa.  

3.  Nel campo **Contenuti script** immettere lo script che si vuole usare. In questo campo è anche possibile incollare i contenuti di uno script esistente oppure è possibile scegliere **Apri** per passare a uno script salvato esistente. Configuration Manager controlla i risultati dello script leggendo i valori scritti nei flusso di output Standard Out (STDOUT) e Standard Error (STDERR) e nel codice di uscita dello script. Se il codice di uscita è un valore diverso da zero, si è verificato un errore nello script e lo stato di rilevamento dell'applicazione è sconosciuto. Se il codice di uscita è pari a zero e STDOUT contiene dati, lo stato di rilevamento dell'applicazione è installato.  

 Usare la tabella seguente per comprendere come usare l'output di uno script per determinare se un'applicazione è installata.  

|Codice di uscita dello script|Dettagli|
|--------------------------------|-----------------|
|0|**Dati letti da STDOUT**: vuoto<br /><br /> **Dati letti da STDERR**: vuoto<br /><br /> **Risultato dello script**: operazione riuscita<br /><br /> **Stato di rilevamento dell'applicazione**: non installato|  
|0|**Dati letti da STDOUT**: vuoto<br /><br /> **Dati letti da STDERR** non vuoto<br /><br /> **Risultato dello script**: operazione non riuscita<br /><br /> **Stato di rilevamento dell'applicazione**: sconosciuto|  
|0|**Dati letti da STDOUT**: non vuoto<br /><br /> **Dati letti da STDERR**: vuoto<br /><br /> **Risultato dello script**: operazione riuscita<br /><br /> **Stato di rilevamento dell'applicazione**: installato|  
|0|**Dati letti da STDOUT**: non vuoto<br /><br /> **Dati letti da STDERR** non vuoto<br /><br /> **Risultato dello script**: operazione riuscita<br /><br /> **Stato di rilevamento dell'applicazione**: installato|  
|Valore diverso da zero|**Dati letti da STDOUT**: vuoto<br /><br /> **Dati letti da STDERR**: vuoto<br /><br /> **Risultato dello script**: operazione non riuscita<br /><br /> **Stato di rilevamento dell'applicazione**: sconosciuto|  
|Valore diverso da zero|**Dati letti da STDOUT**: vuoto<br /><br /> **Dati letti da STDERR** non vuoto<br /><br /> **Risultato dello script**: operazione non riuscita<br /><br /> **Stato di rilevamento dell'applicazione**: sconosciuto|  
|Valore diverso da zero|**Dati letti da STDOUT**: non vuoto<br /><br /> **Dati letti da STDERR**: vuoto<br /><br /> **Risultato dello script**: operazione non riuscita<br /><br /> **Stato di rilevamento dell'applicazione**: sconosciuto|  
|Valore diverso da zero|**Dati letti da STDOUT**: non vuoto<br /><br /> **Dati letti da STDERR** non vuoto<br /><br /> **Risultato dello script**: operazione non riuscita<br /><br /> **Stato di rilevamento dell'applicazione**: sconosciuto|  

La tabella seguente contiene script di esempio di Visual Basic (VB) che è possibile usare per scrivere script di rilevamento personalizzati per l'applicazione.  

|Script di esempio di Visual Basic|Descrizione|  
|--------------------------------|-----------------|  
|**WScript.Quit(1)**|Lo script restituisce un valore del codice di uscita diverso da zero, che indica l'esito negativo dell'esecuzione dello script. In questo caso, lo stato di rilevamento dell'applicazione è sconosciuto.|  
|**WScript.StdErr.Write "Script non riuscito"**<br /><br /> **WScript.Quit(0)**|Lo script restituisce un valore del codice di uscita pari a zero, ma il valore di STDERR non è vuoto, che indica l'esito negativo dell'esecuzione dello script. In questo caso, lo stato di rilevamento dell'applicazione è sconosciuto.|  
|**WScript.Quit(0)**|Lo script restituisce un valore del codice di uscita pari a zero, che indica un'esecuzione corretta dello script. Tuttavia, il valore di STDOUT è vuoto, che indica che l'applicazione non è installata.|  
|**WScript.StdOut.Write "L'applicazione è installata"**<br /><br /> **WScript.Quit(0)**|Lo script restituisce un valore del codice di uscita pari a zero, che indica un'esecuzione corretta dello script. Il valore per STDOUT non è vuoto; ciò indica che l'applicazione è installata.|  
|**WScript.StdOut.Write "L'applicazione è installata"**<br /><br /> **WScript.StdErr.Write "Completato"**<br /><br /> **WScript.Quit(0)**|Lo script restituisce un valore del codice di uscita pari a zero, che indica un'esecuzione corretta dello script. I valori per STDOUT e STDERR non sono vuoti; ciò indica che l'applicazione è installata.|  

 > [!NOTE]  
 >  La dimensione massima che è possibile usare per uno script è 32 KB.  

4.  Scegliere **OK** per chiudere la finestra di dialogo **Editor dello script**.  

## <a name="specify-user-experience-options-for-the-deployment-type"></a>Specificare le opzioni dell'esperienza utente per il tipo di distribuzione  
 Queste impostazioni specificano il modo in cui l'applicazione verrà installata nei dispositivi e che cosa visualizzerà l'utente.  

1.  Nella pagina **Esperienza utente** della Creazione guidata tipo di distribuzione specificare le informazioni seguenti:  

    -   **Comportamento installazione**: nell'elenco a discesa selezionare una delle opzioni seguenti:  

        -   **Installa per utente**: l'applicazione viene installata solo per l'utente a cui viene distribuita.  

        -   **Installa per sistema**: l'applicazione viene installata una sola volta ed è disponibile per tutti gli utenti.  

        -   **Installa per sistema se la risorsa è un dispositivo, altrimenti installa per utente**: se l'applicazione viene distribuita in un dispositivo, sarà installata per tutti gli utenti. Se l'applicazione viene distribuita a un utente, verrà installata solo per tale utente.  

    -   **Requisiti di accesso**: specificare i requisiti di accesso per questo tipo di distribuzione con le opzioni seguenti:  

        -   **Solo se un utente è connesso**  

        -   **Indipendentemente dalla connessione degli utenti**  

        -   **Solo se nessun utente è connesso**  

        > [!NOTE]  
        >  Per impostazione predefinita, questa opzione è configurata su **Solo se un utente è connesso**e non può essere modificata se si è selezionato **Installa per utente** nell'elenco a discesa **Comportamento installazione** .  

    -   **Visibilità del programma di installazione**: specificare la modalità in cui verrà eseguito il tipo di distribuzione sui dispositivi client. Sono disponibili le seguenti opzioni:  

        -   **Ingrandita**: il tipo di distribuzione viene eseguito in modalità ingrandita sui dispositivi client. Gli utenti vedranno tutta l'attività di installazione.  

        -   **Normale** : il tipo di distribuzione viene eseguito in modalità normale in base alle impostazioni predefinite del sistema e del programma. Questa è la modalità predefinita.  

        -   **Ridotta a icona**: il tipo di distribuzione viene eseguito in modalità ridotta sui dispositivi client. Gli utenti possono visualizzare l'attività di installazione nell'area di notifica o sulla barra delle applicazioni.  

        -   **Nascosta**: il tipo di distribuzione viene eseguito in modalità nascosta sui dispositivi client e gli utenti non visualizzeranno alcuna attività di installazione.  

    -   **Consenti agli utenti di visualizzare e interagire con l'installazione del programma**: Specificare se un utente può interagire con l'installazione del tipo di distribuzione per configurarne le opzioni.  

        > [!NOTE]  
        >  Questa opzione viene abilitata per impostazione predefinita se è stata selezionata l'opzione **Installa per utente** nell'elenco a discesa **Comportamento installazione** .  

    -   **Tempo di esecuzione massimo consentito (minuti)**: specificare la durata massima di esecuzione prevista per il programma sul computer client. Questa impostazione può essere specificata come un numero intero maggiore di zero. L'impostazione predefinita è 120 minuti.  

         Questo valore viene usato per:  

        -   Monitorare i risultati dal tipo di distribuzione.  

        -   Controllare se un tipo di distribuzione verrà installato quando sono definite finestre di manutenzione nei dispositivi client. Quando è attiva una finestra di manutenzione, un programma sarà avviato solo se il tempo disponibile nella finestra di manutenzione è sufficiente per configurare l'impostazione **Tempo di esecuzione massimo consentito** .  

        > [!IMPORTANT]  
        >  Potrebbe verificarsi un conflitto se il **Tempo di esecuzione massimo consentito** è maggiore della finestra di manutenzione pianificata. Se l'utente imposta il tempo di esecuzione massimo consentito su una durata superiore a quella di qualsiasi finestra di manutenzione disponibile, quel tipo di distribuzione non sarà eseguito.  

2.  **Tempo previsto di installazione (minuti)**: specificare il tempo previsto necessario per l'installazione del tipo di distribuzione. Viene visualizzato agli utenti di Software Center.  

## <a name="specify-requirements-for-the-deployment-type"></a>Specificare i requisiti per il tipo di distribuzione  

1.  Nella pagina **Requisiti** della Creazione guidata tipo di distribuzione fare clic su **Aggiungi** per aprire la finestra di dialogo **Creazione requisito** e aggiungere un nuovo requisito.  

    > [!NOTE]  
    >  È anche possibile aggiungere nuovi requisiti nella scheda **Requisiti** della finestra di dialogo *Proprietà di\>* **<nome del tipo di distribuzione**.  

2.  Dall'elenco a discesa **Categoria** selezionare se questo requisito è per un dispositivo o un utente oppure selezionare **Personalizzata** per usare una condizione globale creata in precedenza. Quando si seleziona **Personalizzata**, è inoltre possibile fare clic su **Crea** per creare una nuova condizione globale. Per altre informazioni sulle condizioni globali, vedere [Come creare condizioni globali](../../apps/deploy-use/create-global-conditions.md).  

    > [!IMPORTANT]  
    >  Qualsiasi requisito della categoria **Utente** e la condizione **Dispositivo primario** verranno ignorati se si distribuisce l'applicazione a una raccolta dispositivi.  
    >   
    >  Se si è creato un pacchetto di Windows e una sequenza di programmi o di attività per la quale Windows 10 è un requisito e che usa System Center 2012 R2 Configuration Manager SP1 e quindi si effettua l'aggiornamento a System Center Configuration Manager, il requisito relativo a Windows 10 potrebbe essere rimosso. Per risolvere questo problema, specificare di nuovo i requisiti. Si noti che anche se il requisito è stato rimosso dalla visualizzazione requisiti, viene comunque elaborato correttamente sui dispositivi.  

3.  Nell'elenco a discesa **Condizione** selezionare la condizione da usare per valutare se l'utente o il dispositivo soddisfano i requisiti di installazione. Il contenuto di questo elenco varia a seconda della categoria selezionata.  

4.  Nell'elenco a discesa **Operatore** selezionare l'operatore da usare per confrontare la condizione selezionata con il valore specificato per valutare se l'utente o il dispositivo soddisfano i requisiti d'installazione. Gli operatori disponibili variano a seconda della condizione selezionata.  

    > [!IMPORTANT]  
    >  I requisiti disponibili variano a seconda del tipo di dispositivo usato dal tipo di distribuzione.  

5.  Nella casella **Valore** specificare i valori da usare con la condizione e l'operatore selezionati per valutare se l'utente o il dispositivo soddisfano i requisiti di installazione. I valori disponibili variano a seconda della condizione e dell'operatore selezionati.  

6.  Scegliere **OK** per salvare il requisito e chiudere la finestra di dialogo **Creazione requisito**.  

## <a name="specify-dependencies-for-the-deployment-type"></a>Specificare le dipendenze per il tipo di distribuzione  
 Le dipendenze definiscono uno o più tipi di distribuzione da un'altra applicazione che deve essere installata prima dell'installazione di un tipo di distribuzione. È possibile configurare i tipi di distribuzione dipendenti per l'installazione automatica prima dell'installazione di un tipo di distribuzione.  

> [!IMPORTANT]  
>  In alcuni casi, un tipo di distribuzione dipende dal tipo di distribuzione che contiene anche le dipendenze. Il numero massimo di dipendenze supportate nella catena è cinque.  

1.  Nella pagina **Dipendenze** della Creazione guidata tipo di distribuzione scegliere **Aggiungi** se si desidera specificare i tipi di distribuzione da installare prima di poter installare questo tipo di distribuzione.  

    > [!IMPORTANT]  
    >  È anche possibile aggiungere nuove dipendenze nella scheda **Dipendenze** della finestra di dialogo *Proprietà di\>* **<nome tipo di distribuzione**.  

2.  Nella finestra di dialogo **Aggiungi dipendenza** scegliere **Aggiungi**.  

3.  Nella finestra di dialogo **Specifica applicazione richiesta** selezionare un'applicazione esistente e uno dei tipi di distribuzione applicazione da usare come una dipendenza.  

    > [!TIP]  
    >  È possibile scegliere **Visualizza** per visualizzare le proprietà del tipo di distribuzione o dell'applicazione selezionati.  

4.  Scegliere **OK** per chiudere la finestra di dialogo **Specifica applicazione richiesta**.  

5.  Se si desidera che un'applicazione dipendente venga installata automaticamente, selezionare **Installazione automatica** accanto all'applicazione dipendente.  

    > [!NOTE]  
    >  Non è necessario distribuire un'applicazione dipendente per l'installazione automatica.  

6.  Nella finestra di dialogo **Aggiungi dipendenza**, in **Nome gruppo di dipendenze**, immettere un nome di riferimento per questo gruppo di dipendenze dell'applicazione.  

7.  Facoltativamente, è possibile usare i pulsanti **Aumenta priorità** e **Diminuisci priorità** per modificare l'ordine di valutazione delle dipendenze.  

8.  Scegliere **OK** per chiudere la finestra di dialogo **Aggiungi dipendenza**.  

## <a name="confirm-the-deployment-type-settings-and-finish-the-wizard"></a>Confermare le impostazioni del tipo di distribuzione e terminare la procedura guidata  

1.  Nella pagina **Riepilogo** della Creazione guidata tipo di distribuzione rivedere le azioni che saranno eseguite nella procedura guidata. Scegliere **Avanti** per creare il tipo di distribuzione oppure su **Precedente** per tornare indietro e modificare le impostazioni del tipo di distribuzione.  

2.  Al termine della pagina **Avanzamento** rivedere le azioni eseguite nella procedura guidata e scegliere **Chiudi** per terminare la procedura guidata.  

3.  Se la Creazione guidata tipo di distribuzione è stata avviata dalla Creazione guidata applicazione, verrà visualizzata di nuovo la pagina **Tipi di distribuzione** della Creazione guidata applicazione.  

## <a name="set-up-additional-options-for-deployment-types-that-contain-virtual-applications"></a>Impostare le opzioni aggiuntive per i tipi di distribuzione che contengono applicazioni virtuali  
 Usare le procedure seguenti per impostare le opzioni aggiuntive per i tipi di distribuzione che contengono applicazioni virtuali.  

### <a name="set-up-content-options-for-application-virtualization-app-v-deployment-types"></a>Impostare le opzioni di contenuto per tipi di distribuzione di Application Virtualization (App-V)  

1.  Nella console di Configuration Manager scegliere **Raccolta software** > **Applicazioni**.  

2.  Nell'elenco **Applicazioni** selezionare un'applicazione che contiene un tipo di distribuzione App-V. Quindi nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

3.  Nella finestra di dialogo *Proprietà\>* **<nome applicazione** nella scheda **Tipi di distribuzione** selezionare un tipo di distribuzione App-V e quindi scegliere **Modifica**.  

4.  Se necessario, impostare le opzioni seguenti nella scheda **Contenuto** della finestra di dialogo *<Nome tipo distribuzione\>* **Proprietà**:  

    -   **Rendi permanente il contenuto nella cache client**: selezionare questa opzione per assicurarsi che il contenuto per questo tipo di distribuzione non venga eliminato dalla cache del client di Configuration Manager.  

    -   **Carica contenuto nella cache App-V prima dell'avvio**: selezionare questa opzione per fare in modo che tutto il contenuto per l'applicazione virtuale venga caricato nella cache App-V prima dell'avvio dell'applicazione. La selezione di questa opzione garantisce inoltre che il contenuto dell'applicazione non venga bloccato nella cache e possa essere eliminato in base alle necessità.  

5.  Scegliere **OK** per chiudere la finestra di dialogo *Proprietà\>* **<nome tipo distribuzione**.  

6.  Scegliere **OK** per chiudere la finestra di dialogo **Proprietà** *<nome applicazione\>*.  

### <a name="set-up-publishing-options-for-app-v-deployment-types"></a>Impostare le opzioni di pubblicazione per i tipi di distribuzione App-V  

1.  Nella console di Configuration Manager scegliere **Raccolta software** > **Applicazioni**.  

3.  Nell'elenco **Applicazioni** selezionare un'applicazione che contiene un tipo di distribuzione App-V. Quindi nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

4.  Nella finestra di dialogo *Proprietà\>* **<nome applicazione** nella scheda **Tipi di distribuzione** selezionare un tipo di distribuzione App-V e quindi scegliere **Modifica**.  

5.  Nella finestra di dialogo *Proprietà\>***<Nome tipo di distribuzione**, nella scheda **Pubblicazione**, selezionare gli elementi nell'applicazione virtuale da pubblicare.  

6.  Scegliere **OK** per chiudere la finestra di dialogo *Proprietà\>*  **<nome tipo distribuzione**.  

7.  Scegliere **OK** per chiudere la finestra di dialogo **Proprietà** *<nome applicazione\>*.  

## <a name="import-an-application"></a>Importare un'applicazione  
 Usare la procedura seguente per importare un'applicazione in Configuration Manager. Per informazioni su come esportare un'applicazione, vedere [Attività di gestione per applicazioni di System Center Configuration Manager](../../apps/deploy-use/management-tasks-applications.md).  

1.  Nella console di Configuration Manager scegliere **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.   

3.  Nella scheda **Home**, nel gruppo **Crea**, scegliere **Importa applicazione**.  

4.  Nella pagina **Generale** dell'**Importazione guidata applicazione** scegliere **Sfoglia** e quindi specificare il percorso UNC del file con estensione zip che contiene l'applicazione da importare.  

5.  Nella pagina **Contenuto file** selezionare l'azione da eseguire se l'applicazione che si sta cercando di importare è il duplicato di un'applicazione esistente. È possibile creare una nuova applicazione oppure ignorare il duplicato e aggiungere una nuova revisione per l'applicazione esistente.  

6.  Nella pagina **Riepilogo** esaminare le azioni da eseguire e quindi terminare la procedura guidata.  

 La nuova applicazione viene visualizzata nel nodo **Applicazioni**.  

> [!TIP]  
>  Il cmdlet di Windows PowerShell **Import-CMApplication** ha la stessa funzione di questa procedura. Per altre informazioni, vedere [Import-CMApplication](https://technet.microsoft.com/library/jj821738.aspx) nella documentazione di riferimento dei cmdlet di System Center 2012 Configuration Manager SP1.  

##  <a name="deployment-types-supported-by-configuration-manager"></a>Tipi di distribuzione supportati da Configuration Manager  

|Nome del tipo di distribuzione|Altre informazioni|  
|--------------------------|----------------------|  
|**Windows Installer (file \*.msi)**|Crea un tipo di distribuzione da un file di Windows Installer.|  
|**Pacchetto app Windows (\*.appx, \*.appxbundle)**|Crea un tipo di distribuzione per il sistema operativo Windows 8, Windows RT o versioni successive da un file del pacchetto dell'app di Windows o da un pacchetto bundle dell'app di Windows.|  
|**Pacchetto app Windows (in Windows Store)**|Crea un tipo di distribuzione per Windows 8, Windows RT o versioni successive specificando un collegamento all'app in Windows Store o tramite l'esplorazione dello Store per selezionare l'app necessaria.<br /><br /> Se si desidera distribuire l'app come un collegamento a Windows Store, assicurarsi che l'impostazione Criteri di gruppo **Disattiva applicazione di archiviazione** sia impostata su **Disattivato** o **Non configurato**. Se questa impostazione è abilitata, i client non saranno in grado di connettersi a Windows Store per scaricare e installare applicazioni.<br /><br /> I tipi di distribuzione di Windows 8 che usano un collegamento a un archivio vengono sempre valutati prima di altri tipi di distribuzione, indipendentemente dalla relativa priorità.|  
|**Programma di installazione dello script**|Crea un tipo di distribuzione che specifica uno script in esecuzione su dispositivi client per installare contenuto o per eseguire un'azione.|  
|**Microsoft Application Virtualization 4**|Crea un tipo di distribuzione da un manifesto Microsoft Application Virtualization 4|  
|**Microsoft Application Virtualization 5**|Consente di creare un tipo di distribuzione da un file di pacchetto di Microsoft Application Virtualization 5.|  
|**Pacchetto app Windows Phone (file \*.xap)**|Consente di creare un tipo di distribuzione da un file di pacchetto dell'app di Windows Phone.|  
|**Pacchetto app Windows Phone (in Windows Phone Store)**|Crea un tipo di distribuzione specificando un collegamento all'app in Windows Phone Store.|  
|**Windows Mobile Cabinet**|Crea un tipo di distribuzione per dispositivi Windows Mobile da un file Windows Mobile Cabinet (CAB).|  
|**Pacchetto app per iOS (file \*.ipa)**|Consente di creare un tipo di distribuzione da un file di pacchetto dell'app di iOS.|  
|**Pacchetto app per iOS nell'App Store**|Consente di creare un tipo di distribuzione specificando un collegamento all'app di iOS nell'App Store.|  
|**Pacchetto app per Android (file \*.apk)**|Consente di creare un tipo di distribuzione da un file di pacchetto dell'app di Android.|  
|**Pacchetto app Android in Google Play**|Consente di creare un tipo di distribuzione specificando un collegamento all'app in Google Play.|  
|**Mac OS X**|Crea un tipo di distribuzione per computer Mac da un file .cmmac che è stato creato con l'utilità CMAppUtil.<br /><br /> Si applica solo ai computer Mac che eseguono il client di Configuration Manager.|  
|**Applicazione Web**|Consente di creare un tipo di distribuzione che specifica un collegamento a un'applicazione Web. Il tipo di distribuzione installa un collegamento all'applicazione Web sul dispositivo dell'utente.<br /><br /> Se è stato installato Intune Managed Browser in dispositivi iOS o Android gestiti, è possibile assicurarsi che l'app venga aperta solo con Managed Browser. A tale scopo, usare uno dei formati seguenti quando si specifica un collegamento all'app sostituendo **http:** con **http-intunemam:** o **https:** con **https-intunemam:**<br /><br /> - **http-intunemam://<percorso App Web\>**<br /><br /> - **https-intunemam://<percorso App Web\>**<br /><br /> È possibile usare i requisiti dell'applicazione Configuration Manager per assicurarsi che le app da associare a Managed Browser vengano installate solo in dispositivi iOS e Android.<br /><br /> Per altre informazioni su Intune Managed Browser, vedere [Gestire l'accesso a Internet mediante criteri di Managed Browser](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md).|  
|**Windows Installer tramite MDM (\*.msi)**|Questo tipo di programma di installazione permette di creare e distribuire app basate su Windows Installer in PC che eseguono Windows 10.<br /><br /> Quando si usa questo tipo di programma di installazione, considerare gli aspetti seguenti:<br><br>- È possibile caricare un solo file con estensione MSI.<br /><br /> - Per il rilevamento delle app vengono usati il codice e la versione prodotto del file.<br /><br /> - Viene usato il comportamento di riavvio predefinito dell'app. Configuration Manager non controlla questo comportamento.<br /><br /> - I pacchetti MSI per utente vengono installati per un singolo utente.<br /><br /> - I pacchetti MSI per computer vengono installati per tutti gli utenti del dispositivo.<br /><br /> - I pacchetti MSI dual mode vengono installati attualmente solo per tutti gli utenti del dispositivo.<br /><br /> - Gli aggiornamenti delle app sono supportati quando il codice prodotto MSI di ogni versione è lo stesso.|  

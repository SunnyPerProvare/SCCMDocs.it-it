---
title: Creare applicazioni
titleSuffix: Configuration Manager
description: Creare applicazioni con tipi di distribuzione, metodi di rilevamento e requisiti per installare software.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9b90dfcc0916f62905af777e45222ceebf8300f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32341880"
---
# <a name="create-applications-with-system-center-configuration-manager"></a>Creare applicazioni con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le applicazioni di Configuration Manager hanno uno o più tipi di distribuzione, che includono i file di installazione e le informazioni necessarie per installare il software nei dispositivi. Un tipo di distribuzione ha anche regole, ad esempio metodi di rilevamento e requisiti, che specificano quando e come il client deve installare il software.  

 Creare applicazioni usando i metodi seguenti:  

-   Creare automaticamente i tipi di applicazione e di distribuzione leggendo i file di installazione dell'applicazione.  

-   Creare manualmente l'applicazione e quindi aggiungere tipi di distribuzione in un secondo momento.  

-   Importare un'applicazione da un file.  

> [!NOTE]  
>  Per informazioni dettagliate sulla creazione di applicazioni iOS, Windows Phone e Android, vedere [Creare applicazioni per dispositivi mobili](../../mdm/deploy-use/create-applications.md).  



## <a name="start-the-create-application-wizard"></a>Avviare la Creazione guidata applicazione  

1.  Nella console di Configuration Manager scegliere **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.  

3.  Nella scheda **Home**, nel gruppo **Crea**, scegliere **Crea applicazione**.  



## <a name="specify-whether-you-want-to-automatically-detect-application-information-or-manually-define-the-information"></a>specificare se si desidera rilevare automaticamente le informazioni sull'applicazione o definirle manualmente.  

-   Rilevare automaticamente le informazioni relative alle applicazioni per creare un'applicazione di base con un tipo di distribuzione singolo, ad esempio un file di Windows Installer privo di dipendenze o requisiti. Dopo aver creato un'applicazione usando questa procedura, è possibile apportare le modifiche necessarie per aggiungere o modificare i tipi di distribuzione e aggiungere metodi di rilevamento, dipendenze o requisiti.  

-   Specificare manualmente le informazioni dell'applicazione per creare applicazioni più complesse con più tipi di distribuzione, dipendenze, metodi di rilevamento o requisiti.  

### <a name="automatically-detect-application-information"></a>Rilevare automaticamente le informazioni sull'applicazione  

1.  Nella pagina **Generale** della Creazione guidata applicazione selezionare **Rileva automaticamente le informazioni sull'applicazione dai file di installazione**.  

2.  Dall'elenco a discesa **Tipo** , scegliere il tipo di file di installazione dell'applicazione che si desidera usare per rilevare le informazioni sull'applicazione. Per informazioni sui tipi di installazione disponibili, vedere [Tipi di distribuzione supportati da Configuration Manager](/sccm/apps/deploy-use/create-applications#deployment-types-supported-by-configuration-manager) in questo argomento.  

3.  Nella casella **Percorso** specificare il percorso UNC nel formato *\\\\server\\condivisione\\\nomefile* oppure il collegamento allo Store per il file di installazione dell'applicazione da usare per rilevare le informazioni sull'applicazione. In alternativa, fare clic su **Sfoglia** per selezionare il file di installazione.  

    > [!IMPORTANT]  
    >  Quando si seleziona **Windows Installer (\*file con estensione msi)** come tipo di applicazione, tutti i file nella cartella specificata vengono importati e inviati ai punti di distribuzione. Verificare che la cartella specificata contenga solo i file necessari per installare l'applicazione. Configuration Manager è testato per supportare fino a 20.000 file applicazione nel pacchetto dell'applicazione. Se l'applicazione contiene più file, è consigliabile creare più applicazioni con un numero inferiore di file.  

    >  È necessario avere accesso al percorso UNC che include l'applicazione e alle eventuali sottocartelle del contenuto dell'applicazione stessa.  

4.  Nella pagina **Importazione informazioni** della Creazione guidata applicazione, rivedere le informazioni importate e quindi fare clic su **Avanti**. Se necessario, è possibile scegliere **Indietro** per tornare indietro e correggere eventuali errori.  

5.  Nella pagina **Informazioni generali** della Creazione guidata applicazione specificare le informazioni seguenti:  

    > [!NOTE]  
    >  Se Configuration Manager rileva automaticamente queste informazioni dai file di installazione dell'applicazione, significa che sono già presenti. Inoltre, le opzioni visualizzate potrebbero essere diverse a seconda del tipo di applicazione creata.  

    -   Informazioni generali sull'applicazione, ad esempio nome, commenti e versione. Per facilitare la ricerca dell'applicazione nella console di Configuration Manager, specificare un riferimento facoltativo.  

    -   **Programma di installazione**: specificare il programma di installazione e le eventuali proprietà necessarie per installare il tipo di distribuzione delle applicazioni.  

        > [!TIP]  
        >  Se il programma di installazione non viene visualizzato, scegliere **Sfoglia** e selezionare il percorso del programma di installazione.  

    -   **Comportamento di installazione**: specificare se il tipo di distribuzione dell'applicazione deve essere installato solo per l'utente connesso oppure per tutti gli utenti. Una terza opzione corrisponde all'installazione per tutti gli utenti se viene distribuito in un dispositivo o solo per un utente specifico se viene distribuito a un utente.  

    -   **Usa una connessione VPN automatica (se configurata)**: se un profilo VPN è stato distribuito nel dispositivo in cui viene avviata l'app, avviare la connessione VPN all'avvio dell'app (solo Windows 8.1 e Windows Phone 8.1).  

         Nei dispositivi Windows Phone 8.1 le connessioni VPN automatiche non sono supportate se sono stati distribuiti più profili VPN nel dispositivo.  

         Per altre informazioni, vedere [Profili VPN](../../protect/deploy-use/vpn-profiles.md).  

6.  Scegliere **Avanti**, riesaminare le informazioni sull'applicazione nella pagina **Riepilogo** e quindi terminare la Creazione guidata applicazione.  

La nuova applicazione viene visualizzata nel nodo **Applicazioni** della console di Configuration Manager. Il processo di creazione dell'applicazione è terminato. Se si vogliono aggiungere altri tipi di distribuzione all'applicazione, vedere [Creare tipi di distribuzione per l'applicazione](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application) in questo argomento.  

### <a name="manually-specify-application-information"></a>Specificare manualmente le informazioni sull'applicazione  

1.  Nella pagina **Generale** della Creazione guidata applicazione, selezionare **Specifica manualmente le informazioni dell'applicazione** e quindi scegliere **Avanti**.  

2.  Specificare informazioni generali sull'applicazione, ad esempio nome, commenti e versione. Per facilitare la ricerca dell'applicazione nella console di Configuration Manager, specificare un riferimento facoltativo.  

3.  Nella pagina **Catalogo applicazioni** della Creazione guidata applicazione specificare le informazioni seguenti:  

    -   **Lingua selezionata**: dall'elenco a discesa selezionare la lingua dell'applicazione che si vuole configurare. Scegliere **Aggiungi/Rimuovi** per configurare più lingue per l'applicazione.  

    -   **Nome dell'applicazione localizzata**: specificare il nome dell'applicazione nella lingua selezionata nell'elenco a discesa **Lingua selezionata** .  

        > [!IMPORTANT]  
        >  È necessario specificare il nome dell'applicazione localizzata per ogni lingua che si vuole configurare.  

    -   **Categorie utente**: scegliere **Modifica** per specificare le categorie dell'applicazione nella lingua selezionata nell'elenco a discesa **Lingua selezionata**. Gli utenti di Software Center possono usare queste categorie selezionate per filtrare e ordinare le applicazioni disponibili.  

    -   **Documentazione utente**: scegliere **Sfoglia** per specificare il percorso del file che gli utenti di Software Center possono leggere per ottenere altre informazioni su questa applicazione. Questo percorso è un URL o un percorso di rete con un nome file.

    -   **Testo collegamento**: specificare il testo da visualizzare al posto dell'URL dell'applicazione.  

    -   **URL privacy applicazione**: specificare un URL che colleghi all'informativa sulla privacy dell'applicazione.  

    -   **Descrizione localizzata**: immettere una descrizione per questa applicazione nella lingua selezionata nell'elenco a discesa **Lingua selezionata** .  

    -   **Parole chiave**: immettere un elenco di parole chiave nella lingua selezionata nell'elenco a discesa **Lingua selezionata** . Queste parole chiave consentono agli utenti di Software Center di cercare l'applicazione.  

    -   **Icona**: scegliere **Sfoglia** per selezionare un'icona per l'applicazione tra le icone disponibili. Se non si specifica un'icona, per questa applicazione viene usata l'icona predefinita. È ora possibile impostare un'icona con dimensioni fino a 512x512 pixel.

    -   **Visualizza come app in primo piano ed evidenziala nel portale aziendale**: questa opzione consente di visualizzare l'app in primo piano nel portale aziendale.  

4.  Nella pagina **Tipi di distribuzione** della Creazione guidata applicazione scegliere **Aggiungi** per creare un nuovo tipo di distribuzione.  

 Per altre informazioni, vedere [Creare tipi di distribuzione per l'applicazione](/sccm/apps/deploy-use/create-applications#create-deployment-types-for-the-application).  

5.  Scegliere **Avanti**, riesaminare le informazioni sull'applicazione nella pagina **Riepilogo** e quindi terminare la Creazione guidata applicazione.  

La nuova applicazione viene visualizzata nel nodo **Applicazioni** della console di Configuration Manager.  



##  <a name="create-deployment-types-for-the-application"></a>Creare tipi di distribuzione per l'applicazione  
 Se le informazioni relative all'applicazione vengono visualizzate automaticamente, alcuni passaggi di queste procedure potrebbero non essere necessari.  

### <a name="start-the-create-deployment-type-wizard"></a>Avviare la Creazione guidata tipo di distribuzione  

1.  Nella console di Configuration Manager scegliere **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.  

3.  Selezionare un'applicazione e quindi nel gruppo **Applicazione** della scheda **Home** fare clic su **Crea tipo di distribuzione**.  

> [!TIP]  
>  È anche possibile avviare la Creazione guidata tipo di distribuzione dalla Creazione guidata applicazione e dalla scheda **Tipi di distribuzione** della finestra di dialogo *Proprietà\>* **nome applicazione**.  

### <a name="specify-whether-you-want-to-automatically-detect-deployment-type-information-or-manually-set-up-the-information"></a>Specificare se si desidera rilevare automaticamente le informazioni sul tipo di distribuzione o impostare manualmente le informazioni  
 Usare una delle seguenti procedure per rilevare automaticamente o per impostare manualmente le informazioni sul tipo di distribuzione.  

#### <a name="automatically-detect-deployment-type-information"></a>Rilevare automaticamente le informazioni sul tipo di distribuzione  

1.  Nella pagina **Generale** della Creazione guidata tipo di distribuzione selezionare **Rileva automaticamente le informazioni sul tipo di distribuzione dai file di installazione**.  

2.  Nella casella **Tipo** selezionare il tipo di file di installazione dell'applicazione che si vuole usare per rilevare le informazioni sul tipo di distribuzione.  

3.  Nella casella **Percorso** specificare il percorso di rete oppure il collegamento dello Store per i file di installazione dell'applicazione. Configuration Manager usa questi file per rilevare le informazioni sul tipo di distribuzione. È anche possibile scegliere **Sfoglia** per individuare il file di installazione.  

    > [!NOTE]  
    >  È necessario avere accesso al percorso di rete dell'applicazione e alle eventuali sottocartelle del contenuto dell'applicazione stessa.  

4.  Nella pagina **Importazione informazioni** della Creazione guidata tipo di distribuzione riesaminare le informazioni importate e quindi fare clic su **Avanti**. È anche possibile scegliere **Indietro** per tornare indietro e correggere eventuali errori.  

5.  Nella pagina **Informazioni generali** della Creazione guidata tipo di distribuzione, specificare le informazioni seguenti:  

    > [!NOTE]  
    >  Alcune delle informazioni sul tipo di distribuzione potrebbero già essere presenti se sono state lette dai file di installazione dell'applicazione. Le opzioni visualizzate, poi, possono variare a seconda del tipo di distribuzione che si sta creando.  

    -   Informazioni generali sul tipo di distribuzione, ad esempio il nome, i commenti dell'amministratore e le lingue disponibili.  

    -   **Programma di installazione**: specificare il programma di installazione e le eventuali proprietà necessarie per installare il tipo di distribuzione.  

    -   **Comportamento installazione**: specificare se installare il tipo di distribuzione per l'utente corrente oppure per tutti gli utenti. Una terza opzione corrisponde all'installazione per tutti gli utenti se viene distribuito in un dispositivo o solo per un utente specifico se viene distribuito a un utente.  

    -   **Usa una connessione VPN automatica (se configurata)**: se un profilo VPN è stato distribuito nel dispositivo in cui viene avviata l'app, avviare la connessione VPN all'avvio dell'app (solo Windows 8.1 e Windows Phone 8.1). Se sono stati distribuiti più profili VPN a un dispositivo Windows 8.1, per impostazione predefinita viene usato il primo profilo VPN distribuito.  

         Nei dispositivi Windows Phone 8.1 le connessioni VPN automatiche non sono supportate se sono stati distribuiti più profili VPN nel dispositivo.  

         Per altre informazioni, vedere [Profili VPN](../../protect/deploy-use/vpn-profiles.md).  

6.  Scegliere **Avanti** e quindi continuare con la procedura [Specificare le opzioni di contenuto per il tipo di distribuzione](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type).  

#### <a name="manually-set-up-the-deployment-type-information"></a>Specificare manualmente le informazioni sul tipo di distribuzione  

1.  Nella pagina **Generale** della Creazione guidata tipo di distribuzione, nell'elenco a discesa **Tipo**, scegliere il tipo di file di installazione dell'applicazione per questo tipo di distribuzione. 

2.  Selezionare **Specifica manualmente le informazioni sul tipo di distribuzione** e quindi fare clic su **Avanti**.

3.  Nella pagina **Informazioni generali** della Creazione guidata tipo di distribuzione specificare un nome per il tipo di distribuzione. Facoltativamente, specificare una descrizione e indicare le lingue per questo tipo di distribuzione e quindi fare clic su **Avanti**.  

4.  Continuare con [Specificare le opzioni di contenuto per il tipo di distribuzione](/sccm/apps/deploy-use/create-applications#specify-content-options-for-the-deployment-type).  

###  <a name="specify-content-options-for-the-deployment-type"></a>Specificare le opzioni di contenuto per il tipo di distribuzione  

1.  Nella pagina **Contenuto** della Creazione guidata tipo di distribuzione specificare le informazioni seguenti:  

    -   **Percorso dei contenuti**: specificare il percorso del contenuto per questo tipo di distribuzione o selezionare **Sfoglia** per scegliere la cartella del contenuto del tipo di distribuzione.  

        > [!IMPORTANT]  
        >  L'account di sistema del computer server del sito deve disporre delle autorizzazioni per il percorso del contenuto specificato.  

    -   **Impostazioni del contenuto di disinstallazione**: specificare una delle opzioni seguenti:
        - **Uguale al contenuto di installazione**: selezionare questa opzione se il contenuto di installazione e di disinstallazione è lo stesso. Questa opzione corrisponde all'impostazione predefinita.
        - **Nessun contenuto di disinstallazione**: selezionare questa opzione se l'applicazione non richiede contenuti per la disinstallazione.
        - **Diversa dal contenuto di installazione**: selezionare questa opzione se il contenuto di disinstallazione è diverso dal contenuto di installazione. Specificare quindi il percorso del contenuto dell'applicazione da usare per disinstallare l'applicazione.
5. Fare clic su **OK** per chiudere la finestra di dialogo delle proprietà del tipo di distribuzione.

    -   **Rendi permanente il contenuto nella cache client**: selezionare questa opzione per specificare se il client deve mantenere contenuto nella cache del computer client a tempo indeterminato. Il client mantiene il contenuto anche se l'app è già installata. Questa opzione è utile con alcune distribuzioni, ad esempio le distribuzioni di software basato su Windows Installer. Windows Installer richiede una copia locale del contenuto di origine per l'applicazione degli aggiornamenti. Questa opzione, tuttavia, riduce lo spazio disponibile nella cache. Se si seleziona questa opzione, una distribuzione di grandi dimensioni potrebbe non riuscire in un momento successivo se lo spazio disponibile della cache non è sufficiente.  

    -   **Consenti ai client di condividere il contenuto con altri client nella stessa subnet**: selezionare questa opzione per ridurre il carico sulla rete. I client scaricano il contenuto da altri client locali all'interno della rete che lo abbiano già scaricato e memorizzato nella cache. Questa opzione usa la tecnologia Windows BranchCache.  

    -   **Programma di installazione**: specificare il nome del programma di installazione ed eventuali parametri di installazione necessari oppure scegliere **Sfoglia** per individuare il file di installazione.  

    -   **Avvio installazione da**: specificare la cartella che contiene il programma di installazione per il tipo di distribuzione (facoltativo). Questa cartella può corrispondere a un percorso assoluto nel client o al percorso della cartella del punto di distribuzione contenente i file di installazione.  

    -   **Programma di disinstallazione**: specificare il nome del programma di disinstallazione ed eventuali parametri obbligatori oppure scegliere **Sfoglia** per individuare il programma (facoltativo).  

    -   **Avvio disinstallazione da**: specificare la cartella che contiene il programma di disinstallazione per il tipo di distribuzione (facoltativo). Questa cartella può corrispondere a un percorso assoluto nel client. Può anche essere un percorso relativo in un punto di distribuzione della cartella con il pacchetto.  

    -   **Esegui l'installazione e la disinstallazione del programma come processo a 32 bit su client a 64 bit**: usare i percorsi di file e registro di sistema a 32 bit nei computer basati su Windows per eseguire il programma di installazione per il tipo di distribuzione.  

2.  Scegliere **Avanti**.  

### <a name="set-up-detection-methods-to-indicate-the-presence-of-the-deployment-type-windows-pcs-only"></a>Impostare i metodi di rilevamento per indicare la presenza del tipo di distribuzione (solo PC Windows)  
 Questa procedura consente di impostare un metodo di rilevamento che indica se il tipo di distribuzione è già installato.  

1.  Nella pagina **Metodo di rilevamento** della Creazione guidata tipo di distribuzione selezionare **Configura regole per rilevare la presenza del tipo di distribuzione** e quindi scegliere **Aggiungi clausola**.  

    > [!NOTE]  
    >  È anche possibile selezionare **Utilizza uno script personalizzato per rilevare la presenza del tipo di distribuzione**. Per altre informazioni, vedere [Usare uno script personalizzato per determinare la presenza di un tipo di distribuzione](/sccm/apps/deploy-use/create-applications#Use-a-custom-script-to-check-for-the-presence-of-a-deployment-type) in questo argomento.  

2.  Nell'elenco a discesa **Tipo di impostazione** della finestra di dialogo **Regola di rilevamento**, selezionare il metodo che si vuole usare per rilevare la presenza del tipo di distribuzione. È possibile scegliere tra i seguenti metodi disponibili:  

    -   **File System**: consente di rilevare se un file o una cartella specifica è presente in un dispositivo client. In caso affermativo, l'applicazione è installata.  

        > [!NOTE]  
        >  Il tipo di impostazione **File System** non supporta l'indicazione di un percorso UNC di una condivisione di rete nel campo Percorso. È possibile specificare solo un percorso locale sul dispositivo client.  
        >   
        >  Per controllare i percorsi dei file a 64 bit per il file o la cartella specificati, selezionare prima l'opzione **Il file o la cartella sono associati a un'applicazione a 32 bit su sistemi a 32 bit**. Se il file o la cartella non viene trovata, viene eseguita una ricerca nei percorsi a 64 bit.  

    -   **Registro di sistema**: consente di rilevare se una chiave o un valore del Registro di sistema è presente in un dispositivo client. In caso affermativo, l'applicazione è installata.  

        > [!NOTE]  
        >  Per controllare i percorsi del Registro di sistema a 32 bit per la chiave del Registro di sistema specificata, selezionare prima l'opzione **La chiave del Registro di sistema è associata a un'applicazione a 32 bit su sistemi a 64 bit**. Se la chiave del Registro di sistema non viene trovata, viene eseguita una ricerca nei percorsi a 64 bit.  

    -   **Windows Installer**: consente di rilevare se un file Windows Installer specifico è presente in un dispositivo client. In caso affermativo, l'applicazione è installata.  

3.  Specificare i dettagli sull'elemento per verificare se questo tipo di distribuzione è installato. Ad esempio, è possibile usare un file, una cartella, una chiave o un valore del Registro di sistema o un codice prodotto di Windows Installer.  

4.  Specificare se l'elemento deve esistere o soddisfare una regola. Se ad esempio si effettua il rilevamento tramite un file, selezionare **L'impostazione del file system deve essere presente nel sistema di destinazione per indicare la presenza dell'applicazione**.  

5.  Scegliere **Avanti** per chiudere la finestra di dialogo **Regola di rilevamento**.  

####  <a name="use-a-custom-script-to-check-for-the-presence-of-a-deployment-type"></a>Usare uno script personalizzato per determinare la presenza di un tipo di distribuzione  

1.  Nella pagina **Metodo di rilevamento** della Creazione guidata tipo di distribuzione selezionare la casella **Utilizza uno script personalizzato per rilevare la presenza del tipo di distribuzione** e quindi scegliere **Modifica**.  

2.  Nell'elenco a discesa **Tipo di script** della finestra di dialogo **Editor dello script**selezionare la lingua dello script che si vuole usare per rilevare il tipo di distribuzione dall'elenco a discesa.  

3.  Nel campo **Contenuti script** immettere lo script che si vuole usare. In questo campo è anche possibile incollare i contenuti di uno script esistente oppure è possibile scegliere **Apri** per passare a uno script salvato esistente. Configuration Manager controlla i risultati dello script. Legge i valori scritti dallo script nel flusso di output standard (STDOUT) e nel flusso degli errori standard (STDERR), nonché il codice di uscita. Se il codice di uscita dello script è un valore diverso da zero, lo script non è riuscito e lo stato del rilevamento dell'applicazione è sconosciuto. Se il codice di uscita è pari a zero e STDOUT contiene dati, lo stato di rilevamento dell'applicazione è installato.  

 Usare la tabella seguente per controllare se un'applicazione è installata usando l'output di uno script:  

|Codice di uscita dello script|Dettagli|
|--------------------------------|-----------------|
|0|**Dati letti da STDOUT**: nessuno<br /><br /> **Dati letti da STDERR**: nessuno<br /><br /> **Risultato dello script**: operazione riuscita<br /><br /> **Stato di rilevamento dell'applicazione**: non installata|  
|0|**Dati letti da STDOUT**: nessuno<br /><br /> **Dati letti da STDERR**: presenti<br /><br /> **Risultato dello script**: operazione non riuscita<br /><br /> **Stato di rilevamento dell'applicazione**: sconosciuto|  
|0|**Dati letti da STDOUT**: presenti<br /><br /> **Dati letti da STDERR**: nessuno<br /><br /> **Risultato dello script**: operazione riuscita<br /><br /> **Stato di rilevamento dell'applicazione**: installata|  
|0|**Dati letti da STDOUT**: presenti<br /><br /> **Dati letti da STDERR**: presenti<br /><br /> **Risultato dello script**: operazione riuscita<br /><br /> **Stato di rilevamento dell'applicazione**: installata|  
|Valore diverso da zero|**Dati letti da STDOUT**: nessuno<br /><br /> **Dati letti da STDERR**: nessuno<br /><br /> **Risultato dello script**: operazione non riuscita<br /><br /> **Stato di rilevamento dell'applicazione**: sconosciuto|  
|Valore diverso da zero|**Dati letti da STDOUT**: nessuno<br /><br /> **Dati letti da STDERR**: presenti<br /><br /> **Risultato dello script**: operazione non riuscita<br /><br /> **Stato di rilevamento dell'applicazione**: sconosciuto|  
|Valore diverso da zero|**Dati letti da STDOUT**: presenti<br /><br /> **Dati letti da STDERR**: nessuno<br /><br /> **Risultato dello script**: operazione non riuscita<br /><br /> **Stato di rilevamento dell'applicazione**: sconosciuto|  
|Valore diverso da zero|**Dati letti da STDOUT**: presenti<br /><br /> **Dati letti da STDERR**: presenti<br /><br /> **Risultato dello script**: operazione non riuscita<br /><br /> **Stato di rilevamento dell'applicazione**: sconosciuto|  

La tabella seguente contiene script di esempio di Visual Basic (VB) che è possibile usare per scrivere script di rilevamento personalizzati per l'applicazione.  

|Script di esempio di Visual Basic|Descrizione|  
|--------------------------------|-----------------|  
|**WScript.Quit(1)**|Lo script restituisce un valore del codice di uscita diverso da zero, che indica l'esito negativo dell'esecuzione dello script. In questo caso, lo stato di rilevamento dell'applicazione è sconosciuto.|  
|**WScript.StdErr.Write "Script non riuscito"**<br /><br /> **WScript.Quit(0)**|Lo script restituisce un codice di uscita pari a zero, ma il valore di STDERR non è vuoto. Questo risultato indica che lo script non è stato eseguito correttamente. In questo caso, lo stato di rilevamento dell'applicazione è sconosciuto.|  
|**WScript.Quit(0)**|Lo script restituisce un valore del codice di uscita pari a zero, che indica un'esecuzione corretta dello script. Tuttavia, il valore di STDOUT è vuoto, che indica che l'applicazione non è installata.|  
|**WScript.StdOut.Write "L'applicazione è installata"**<br /><br /> **WScript.Quit(0)**|Lo script restituisce un valore del codice di uscita pari a zero, che indica un'esecuzione corretta dello script. Il valore per STDOUT non è vuoto; ciò indica che l'applicazione è installata.|  
|**WScript.StdOut.Write "L'applicazione è installata"**<br /><br /> **WScript.StdErr.Write "Completato"**<br /><br /> **WScript.Quit(0)**|Lo script restituisce un valore del codice di uscita pari a zero, che indica un'esecuzione corretta dello script. I valori per STDOUT e STDERR non sono vuoti; ciò indica che l'applicazione è installata.|  

 > [!NOTE]  
 >  La dimensione massima che è possibile usare per uno script è 32 KB.  

4.  Scegliere **OK** per chiudere la finestra di dialogo **Editor dello script**.  

### <a name="specify-user-experience-options-for-the-deployment-type"></a>Specificare le opzioni dell'esperienza utente per il tipo di distribuzione  
 Queste impostazioni specificano il modo in cui il client installa l'applicazione nei dispositivi e ciò che viene visualizzato per l'utente.  

1.  Nella pagina **Esperienza utente** della Creazione guidata tipo di distribuzione specificare le informazioni seguenti:  

    -   **Comportamento installazione**: nell'elenco a discesa selezionare una delle seguenti opzioni:  

        -   **Installa per utente**: l'applicazione viene installata solo per l'utente per il quale viene distribuita.  

        -   **Installa per sistema**: l'applicazione viene installata una sola volta ed è disponibile per tutti gli utenti.  

        -   **Installa per sistema se la risorsa è un dispositivo, altrimenti installa per utente**: se l'applicazione viene distribuita in un dispositivo, il client la installa per tutti gli utenti. Se l'applicazione viene distribuita a un utente, il client la installa solo per tale utente.  

    -   **Requisiti di accesso**: specificare i requisiti di accesso per questo tipo di distribuzione dalle seguenti opzioni:  

        -   **Solo se un utente è connesso**  

        -   **Indipendentemente dalla connessione degli utenti**  

        -   **Solo se nessun utente è connesso**  

        > [!NOTE]  
        >  Per impostazione predefinita, questa opzione è impostata su **Solo se un utente è connesso**. Se si seleziona **Installa per utente** nell'elenco a discesa **Comportamento installazione**, non è possibile modificare questa opzione.  

    -   **Visibilità del programma di installazione**: specificare la modalità in cui il tipo di distribuzione deve essere eseguito nei dispositivi client. Sono disponibili le seguenti opzioni:  

        -   **Ingrandita**: il tipo di distribuzione viene eseguito in modalità ingrandita sui dispositivi client. Gli utenti potranno seguire l'intera l'attività di installazione.  

        -   **Normale**: il tipo di distribuzione viene eseguito in modalità normale in base alle impostazioni predefinite del sistema e del programma. Questa è la modalità predefinita.  

        -   **Ridotta a icona**: il tipo di distribuzione viene eseguito in modalità ridotta sui dispositivi client. Gli utenti possono visualizzare l'attività di installazione nell'area di notifica o sulla barra delle applicazioni.  

        -   **Nascosto**: l'esecuzione del tipo di distribuzione viene nascosta nei dispositivi client. Gli utenti non vedono alcuna attività di installazione.  

    -   **Consenti agli utenti di visualizzare e interagire con l'installazione del programma**: specificare se un utente può interagire con l'installazione del tipo di distribuzione per configurarne le opzioni.  

        > [!NOTE]  
        >  Se si seleziona l'opzione **Installa per utente** nell'elenco a discesa **Comportamento installazione**, questa opzione è abilitata per impostazione predefinita.  

        > [!IMPORTANT]
        > A partire dalla versione 1802, questa impostazione è facoltativa se si seleziona il comportamento **Installa per sistema**. Lo scopo principale di questa modifica è di consentire agli utenti finali di interagire con l'installazione durante una sequenza di attività, ad esempio per eseguire un processo di installazione che chiede all'utente finale diverse opzioni. Nei programmi di installazione di alcune applicazioni non è possibile disattivare le richieste all'utente, in quanto il processo di installazione può richiedere valori di configurazione specifici noti solo all'utente. <!--1356976-->
        > 
        > L'installazione in un contesto di sistema e l'autorizzazione dell'interazione con l'installazione da parte degli utenti non consentono di ottenere una configurazione sicura. Per altre informazioni, vedere [Sicurezza e privacy per la gestione delle applicazioni](/sccm/apps/plan-design/security-and-privacy-for-application-management#bkmk_interact).

    -   **Tempo di esecuzione massimo consentito (minuti)**: specifica il tempo massimo previsto dal programma per l'esecuzione nel computer client. Questa impostazione può essere specificata come un numero intero maggiore di zero. L'impostazione predefinita è 120 minuti.  

         Questo valore viene usato per:  

        -   Monitorare i risultati dal tipo di distribuzione.  

        -   Controllare se un tipo di distribuzione è installato quando sono definite finestre di manutenzione nei dispositivi client. Quando è attiva una finestra di manutenzione, un programma viene avviato solo se il tempo disponibile nella finestra di manutenzione è sufficiente per configurare l'impostazione **Tempo di esecuzione massimo consentito**.  

        > [!IMPORTANT]  
        >  Potrebbe verificarsi un conflitto se il **Tempo di esecuzione massimo consentito** è maggiore della finestra di manutenzione pianificata. Se l'utente imposta il tempo di esecuzione massimo su una durata maggiore di quella di qualsiasi finestra di manutenzione disponibile, il tipo di distribuzione corrispondente non viene eseguito.  

    -   **Tempo previsto di installazione (minuti)**: specificare il tempo previsto per l'installazione del tipo di distribuzione. Gli utenti possono visualizzarlo in Software Center.  

    -   **Specify specific reboot behavior** (Specificare il comportamento di riavvio specifico): specificare l'azione post-installazione. Sono disponibili le seguenti opzioni:  

        -   **Determinare il comportamento in base ai codici restituiti**: gestire i riavvi in base ai codici configurati nella scheda Codici restituiti. Software Center visualizza che **potrebbe essere necessario un riavvio**. Se un utente esegue l'accesso durante l'installazione, viene chiesto di procedere in base alla configurazione dell'esperienza utente per la distribuzione.  

        -   **Nessuna azione specifica**: non è necessario il riavvio dopo l'installazione. Software Center segnala che non è necessario eseguire il riavvio.  
        -   **Il programma di installazione software potrebbe forzare il riavvio del dispositivo**: Configuration Manager non controlla né esegue un riavvio, ma l'installazione potrebbe eseguire il riavvio senza alcun preavviso. Usare questa impostazione per impedire la segnalazione di errori di installazione di Configuration Manager quando il programma di installazione esegue un riavvio. Software Center visualizza che **potrebbe essere necessario un riavvio**.  

        -   **Il client Configuration Manager forzerà il riavvio obbligatorio del dispositivo**: Configuration Manager forza il riavvio del dispositivo al termine dell'installazione. Software Center segnala che è necessario eseguire il riavvio. Se un utente esegue l'accesso durante l'installazione, viene chiesto di procedere in base alla configurazione dell'esperienza utente per la distribuzione.

### <a name="specify-requirements-for-the-deployment-type"></a>Specificare i requisiti per il tipo di distribuzione  

1.  Nella pagina **Requisiti** della Creazione guidata tipo di distribuzione fare clic su **Aggiungi** per aprire la finestra di dialogo **Creazione requisito** e aggiungere un nuovo requisito.  

    > [!NOTE]  
    >  È anche possibile aggiungere nuovi requisiti nella scheda **Requisiti** della finestra di dialogo *Proprietà di\>* **<nome del tipo di distribuzione**.  

2.  Dall'elenco a discesa **Categoria** selezionare se questo requisito riguarda un dispositivo o un utente. Selezionare **Personalizzata** per usare una condizione globale creata in precedenza. Quando si seleziona **Personalizzata**, è inoltre possibile fare clic su **Crea** per creare una nuova condizione globale. Per altre informazioni sulle condizioni globali, vedere [Come creare condizioni globali](../../apps/deploy-use/create-global-conditions.md).  

    > [!IMPORTANT]  
    >  Se si distribuisce l'applicazione a una raccolta dispositivi, il client ignora qualsiasi requisito della categoria **Utente** e la condizione **Dispositivo primario**.  
    >   
    >  Se si usa System Center 2012 R2 Configuration Manager SP1 per creare un pacchetto di Windows e una sequenza di programmi o di attività per la quale Windows 10 è un requisito e quindi si effettua l'aggiornamento a System Center Configuration Manager, il requisito relativo a Windows 10 potrebbe essere rimosso. Per risolvere questo problema, specificare di nuovo i requisiti. Anche se il requisito è stato rimosso dalla visualizzazione dei requisiti, viene comunque elaborato correttamente sui dispositivi.  

3.  Nell'elenco a discesa **Condizione** selezionare la condizione da usare per valutare se l'utente o il dispositivo soddisfano i requisiti di installazione. Il contenuto di questo elenco varia a seconda della categoria selezionata.  

4.  Nell' elenco a discesa **Operatore** selezionare l'operatore da usare. Questo operatore confronta la condizione selezionata con il valore specificato, valutando se l'utente o il dispositivo soddisfa i requisiti di installazione. Gli operatori disponibili variano a seconda della condizione selezionata.  

    > [!IMPORTANT]  
    >  I requisiti disponibili variano a seconda del tipo di dispositivo usato dal tipo di distribuzione.  

5.  Nella casella **Valore** specificare i valori da usare. Questi valori, con la condizione e l'operatore selezionati, valutano se l'utente o il dispositivo soddisfa i requisiti di installazione. I valori disponibili variano a seconda della condizione e dell'operatore selezionati.  

6.  Scegliere **OK** per salvare il requisito e chiudere la finestra di dialogo **Creazione requisito**.  

### <a name="specify-dependencies-for-the-deployment-type"></a>Specificare le dipendenze per il tipo di distribuzione  
 Le dipendenze definiscono uno o più tipi di distribuzione da un'altra applicazione che deve essere installata prima dell'installazione di un tipo di distribuzione. È possibile configurare i tipi di distribuzione dipendenti per l'installazione automatica prima dell'installazione di un tipo di distribuzione.  

> [!IMPORTANT]  
>  In alcuni casi, un tipo di distribuzione dipende dal tipo di distribuzione che contiene anche le dipendenze. Il numero massimo di dipendenze supportate nella catena è cinque.  

1.  Nella pagina **Dipendenze** della Creazione guidata tipo di distribuzione scegliere **Avanti**.  

    > [!IMPORTANT]  
    >  È anche possibile aggiungere nuove dipendenze nella scheda **Dipendenze** della finestra di dialogo *Proprietà di\>* **<nome tipo di distribuzione**.  

2.  Nella finestra di dialogo **Aggiungi dipendenza** scegliere **Aggiungi**.  

3.  Nella finestra di dialogo **Specifica applicazione richiesta** selezionare un'applicazione esistente e uno dei tipi di distribuzione applicazione da usare come una dipendenza.  

    > [!TIP]  
    >  È possibile scegliere **Visualizza** per visualizzare le proprietà del tipo di distribuzione o dell'applicazione selezionati.  

4.  Scegliere **OK** per chiudere la finestra di dialogo **Specifica applicazione richiesta**.  

5.  Se si desidera che un'applicazione dipendente venga installata automaticamente, selezionare **Installazione automatica** accanto all'applicazione dipendente.  

    > [!NOTE]  
    >  Non è necessario distribuire un'applicazione dipendente per distribuirla automaticamente.  

6.  Nella finestra di dialogo **Aggiungi dipendenza**, in **Nome gruppo di dipendenze**, immettere un nome di riferimento per questo gruppo di dipendenze dell'applicazione.  

7.  Facoltativamente, usare i pulsanti **Aumenta priorità** e **Diminuisci priorità**. Queste azioni modificano l'ordine in cui il client valuta ogni dipendenza.  

8.  Scegliere **OK** per chiudere la finestra di dialogo **Aggiungi dipendenza**.  

### <a name="confirm-the-deployment-type-settings-and-finish-the-wizard"></a>Confermare le impostazioni del tipo di distribuzione e terminare la procedura guidata  

1.  Rivedere il **Riepilogo**. Scegliere **Avanti** per creare il tipo di distribuzione. Scegliere **Indietro** per tornare indietro e modificare le impostazioni del tipo di distribuzione.  

2.  Al termine della pagina **Avanzamento** rivedere le azioni eseguite nella procedura guidata e scegliere **Chiudi** per terminare la procedura guidata.  

3.  Se la Creazione guidata tipo di distribuzione è stata avviata dalla Creazione guidata applicazione, viene visualizzata di nuovo la pagina **Tipi di distribuzione** della Creazione guidata applicazione.  



## <a name="set-up-additional-options-for-deployment-types-that-contain-virtual-applications"></a>Impostare le opzioni aggiuntive per i tipi di distribuzione che contengono applicazioni virtuali  
 Usare le procedure seguenti per impostare le opzioni aggiuntive per i tipi di distribuzione che includono applicazioni virtuali.  

### <a name="set-up-content-options-for-application-virtualization-app-v-deployment-types"></a>Impostare le opzioni di contenuto per tipi di distribuzione di Application Virtualization (App-V)  

1.  Nella console di Configuration Manager scegliere **Raccolta software** > **Applicazioni**.  

2.  Nell'elenco **Applicazioni** selezionare un'applicazione che contiene un tipo di distribuzione App-V. Quindi nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

3.  Nella finestra di dialogo *Proprietà\>* **<nome applicazione** nella scheda **Tipi di distribuzione** selezionare un tipo di distribuzione App-V e quindi scegliere **Modifica**.  

4.  Se necessario, impostare le opzioni seguenti nella scheda **Contenuto** della finestra di dialogo *<Nome tipo distribuzione\>* **Proprietà**:  

    -   **Rendi permanente il contenuto nella cache client**: selezionare questa opzione per assicurarsi che il contenuto per questo tipo di distribuzione non venga eliminato dalla cache del client di Configuration Manager.  

    -   **Carica contenuto nella cache App-V prima dell'avvio**: selezionare questa opzione per assicurarsi che tutto il contenuto per l'applicazione virtuale venga caricato nella cache App-V prima dell'avvio dell'applicazione. Questa opzione garantisce anche che il contenuto dell'applicazione non venga bloccato nella cache e possa essere eliminato dal client in base alle necessità.  

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

4.  Nella pagina **Generale** dell'**Importazione guidata applicazione** scegliere **Sfoglia**. Specificare quindi un percorso di rete per il file con estensione zip con l'applicazione da importare.  

5.  Nella pagina **Contenuto file** selezionare l'azione da eseguire se l'applicazione che si sta cercando di importare è il duplicato di un'applicazione esistente. È possibile creare una nuova applicazione oppure ignorare il duplicato e aggiungere una nuova revisione per l'applicazione esistente.  

6.  Nella pagina **Riepilogo** esaminare le azioni da eseguire e quindi terminare la procedura guidata.  

 La nuova applicazione viene visualizzata nel nodo **Applicazioni**.  

> [!TIP]  
>  Il cmdlet di Windows PowerShell **Import-CMApplication** ha la stessa funzione di questa procedura. Per altre informazioni, vedere [Import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication?view=sccm-ps).  



##  <a name="deployment-types-supported-by-configuration-manager"></a>Tipi di distribuzione supportati da Configuration Manager  

|Nome del tipo di distribuzione|Altre informazioni|  
|--------------------------|----------------------|  
|**Windows Installer (file \*.msi)**|Crea un tipo di distribuzione da un file di Windows Installer.|  
|**Pacchetto app Windows (\*.appx, \*.appxbundle)**|Crea un tipo di distribuzione per Windows 8 o versione successiva. Selezionare un file del pacchetto dell'app Windows o un pacchetto di bundle dell'app di Windows.|  
|**Pacchetto app Windows (in Windows Store)**|Crea un tipo di distribuzione per Windows 8 o versione successiva. Specificare un collegamento all'app in Windows Store o esplorare lo Store per selezionare l'app.<br /><br /> Per distribuire l'app come collegamento a Windows Store, configurare l'impostazione di Criteri di gruppo **Disattiva applicazione Store** su **Disabilitato** o su **Non configurato**. Se questa impostazione è abilitata, i client non possono connettersi a Windows Store per scaricare e installare applicazioni.<br /><br /> I tipi di distribuzione di Windows 8 che usano un collegamento a un archivio vengono sempre valutati prima di altri tipi di distribuzione, indipendentemente dalla relativa priorità.|  
|**Programma di installazione dello script**|Crea un tipo di distribuzione che specifica uno script in esecuzione su dispositivi client per installare contenuto o per eseguire un'azione.|  
|**Microsoft Application Virtualization 4**|Crea un tipo di distribuzione da un manifesto Microsoft Application Virtualization 4|  
|**Microsoft Application Virtualization 5**|Consente di creare un tipo di distribuzione da un file di pacchetto di Microsoft Application Virtualization 5.|  
|**Pacchetto app Windows Phone (file \*.xap)**|Consente di creare un tipo di distribuzione da un file di pacchetto dell'app di Windows Phone.|  
|**Pacchetto app Windows Phone (in Windows Phone Store)**|Crea un tipo di distribuzione specificando un collegamento all'app in Windows Phone Store.|  
|**Pacchetto app per iOS (file \*.ipa)**|Consente di creare un tipo di distribuzione da un file di pacchetto dell'app di iOS.|  
|**Pacchetto app per iOS nell'App Store**|Consente di creare un tipo di distribuzione specificando un collegamento all'app di iOS nell'App Store.|  
|**Pacchetto app per Android (file \*.apk)**|Consente di creare un tipo di distribuzione da un file di pacchetto dell'app di Android.|  
|**Pacchetto app Android in Google Play**|Consente di creare un tipo di distribuzione specificando un collegamento all'app in Google Play.|  
|**Mac OS X**|Crea un tipo di distribuzione per computer Mac da un file .cmmac che è stato creato con l'utilità CMAppUtil.<br /><br /> Si applica solo ai computer Mac che eseguono il client di Configuration Manager.|  
|**Applicazione Web**|Consente di creare un tipo di distribuzione che specifica un collegamento a un'applicazione Web. Il tipo di distribuzione installa un collegamento all'applicazione Web sul dispositivo dell'utente.<br /><br /> Se è stata installata l'applicazione Microsoft Intune Managed Browser in dispositivi iOS o Android, assicurarsi che gli utenti possano usare Managed Browser solo per aprire l'app. Usare uno dei formati seguenti quando si specifica un collegamento all'app: sostituire **http:** con **http-intunemam:** o **https:** con **https-intunemam:**<br /><br /> - **http-intunemam://<percorso App Web\>**<br /><br /> - **https-intunemam://<percorso App Web\>**<br /><br /> È possibile usare i requisiti dell'applicazione Configuration Manager per assicurarsi che le app da associare a Managed Browser vengano installate solo in dispositivi iOS e Android.<br /><br /> Per altre informazioni su Intune Managed Browser, vedere [Gestire l'accesso a Internet mediante criteri di Managed Browser](../../apps/deploy-use/manage-internet-access-using-managed-browser-policies.md).|  
|**Windows Installer tramite MDM (\*.msi)**|Questo tipo di programma di installazione permette di creare e distribuire app basate su Windows Installer in PC che eseguono Windows 10.<br /><br /> Quando si usa questo tipo di programma di installazione, considerare gli aspetti seguenti:<br><br>- È possibile caricare un solo file con estensione MSI.<br /><br /> - Per il rilevamento delle app vengono usati il codice e la versione prodotto del file.<br /><br /> - Viene usato il comportamento di riavvio predefinito dell'app. Questo riavvio non è controllato da Configuration Manager.<br /><br /> - I pacchetti MSI per utente vengono installati per un singolo utente.<br /><br /> - I pacchetti MSI per computer vengono installati per tutti gli utenti del dispositivo.<br /><br /> - I pacchetti MSI dual mode vengono installati attualmente solo per tutti gli utenti del dispositivo.<br /><br /> - Gli aggiornamenti delle app sono supportati quando il codice prodotto MSI di ogni versione è lo stesso.|  



## <a name="next-steps"></a>Passaggi successivi

Dopo aver creato un'applicazione in Configuration Manager, il passaggio successivo consiste nella [distribuzione dell'applicazione](/sccm/apps/deploy-use/deploy-applications).
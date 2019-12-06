---
title: 'Operazioni e manutenzione per la creazione di report '
titleSuffix: Configuration Manager
description: Informazioni dettagliate sulla gestione di report e sottoscrizioni report in System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b89bcfbf-f5b6-4fb1-bb5e-a5cc18ec0c78
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 11c9bbbab40ec593ae6455a9018502a754402385
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "70377858"
---
# <a name="operations-and-maintenance-for-reporting-in-system-center-configuration-manager"></a>Operazioni e manutenzione per la creazione di report in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Dopo aver definito l'infrastruttura per la creazione di report in System Center Configuration Manager, è in genere necessario eseguire alcune operazioni per la gestione di report e di sottoscrizioni report.  

##  <a name="BKMK_ManageReports"></a> Gestire i report di Configuration Manager  
 Configuration Manager offre oltre 400 report predefiniti che consentono di raccogliere, organizzare e presentare informazioni su utenti, inventario software e hardware, aggiornamenti software, applicazioni, stato del sito e altre operazioni di Configuration Manager all'interno dell'azienda. È possibile utilizzare i report predefiniti come sono oppure è possibile modificare un report in base alle proprie esigenze. È anche possibile creare report personalizzati \-basati su modello e basati su SQL\- secondo le necessità. Usare le sezioni seguenti per gestire i report in Configuration Manager.  

###  <a name="BKMK_RunReport"></a> Eseguire un report di Configuration Manager  
 Report in Configuration Manager vengono archiviati in SQL Server Reporting Services e i dati visualizzati nel report vengono recuperati dal database del sito Configuration Manager. È possibile accedere a report nella console di Configuration Manager o tramite Gestione Report, che è accessibile in un browser web. I report possono essere aperti in qualsiasi computer autorizzato ad accedere al computer che esegue SQL Server Reporting Services ed è necessario di disporre di diritti sufficienti per la visualizzazione dei report. Quando si esegue un report, il titolo, la descrizione e la categoria del report vengono visualizzati nella lingua del sistema operativo locale.  

> [!NOTE]  
>  In alcune lingue, i caratteri potrebbero non essere visualizzati correttamente nei report.  In questo caso, i report possono essere visualizzati tramite la versione Web di Gestione report o tramite la console di amministrazione remota.  

> [!WARNING]  
>  Per eseguire i report, è necessario disporre di diritti di **Lettura** per l'autorizzazione **Sito** e per l'autorizzazione **Esegui report** configurata per oggetti specifici.  

> [!IMPORTANT]    
> Per poter eseguire correttamente i report, deve essere presente un trust bidirezionale per gli utenti di un dominio diverso da quello dell'account al punto Servicies Reporting.

> [!NOTE]  
>  Gestione report è uno strumento Web di accesso e gestione di report che consente di amministrare una singola istanza di un server di report in un percorso remoto su una connessione HTTP. È possibile utilizzare Gestione report per attività operative, ad esempio, per visualizzare i report, modificare le proprietà del report e gestire sottoscrizioni di report associate. Questo argomento include i passaggi necessari per visualizzare un report e modificare le proprietà dei report in Gestione report, ma per ulteriori informazioni sulle altre opzioni disponibili in Gestione report, vedere [Gestione report](https://go.microsoft.com/fwlink/p/?LinkId=224916) nella documentazione online di SQL Server 2008.  

 Utilizzare le procedure seguenti per eseguire un report di Configuration Manager.  

##### <a name="to-run-a-report-in-the-configuration-manager-console"></a>Per eseguire un report nella console di Configuration Manager  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** espandere **Creazione di report**, quindi fare clic su **Report** per elencare i report disponibili.  

    > [!IMPORTANT]  
    >  In questa versione di Configuration Manager, i report **Tutto il contenuto** visualizzano solo pacchetti, non applicazioni.  

    > [!TIP]  
    >  Se non viene elencato alcun report, verificare che il punto di Reporting Services sia installato e configurato. Per altre informazioni, vedere [Configurazione della creazione di report](configuring-reporting.md).  

3.  Selezionare il report che si desidera eseguire e quindi, nella sezione **Gruppo Report** della scheda **Home** , fare clic su **Esegui** per aprire il report.  

4.  Se sono previsti parametri obbligatori, specificare i parametri, quindi fare clic su **Visualizza report**.  

#### <a name="to-run-a-report-in-a-web-browser"></a>Per eseguire un report in un browser Web  

1.  Nel Web browser specificare l'URL di Gestione report, ad esempio, **http:\/\/Server1\/Reports**. È possibile determinare l'URL di gestione di Report sul **URL gestione Report** pagina in Gestione configurazione Reporting Services.  

2.  In Gestione report, fare clic sulla cartella dei report per Configuration Manager, ad esempio, **ConfigMgr\_CAS**.  

    > [!TIP]  
    >  Se non viene elencato alcun report, verificare che il punto di Reporting Services sia installato e configurato. Per altre informazioni, vedere [Configurazione della creazione di report](configuring-reporting.md).  

3.  Fare clic sulla categoria di report per il report che si desidera eseguire e quindi fare clic sul collegamento per il report. Il report verrà aperto in Gestione Report.  

4.  Se sono previsti parametri obbligatori, specificare i parametri, quindi fare clic su **Visualizza report**.  

###  <a name="BKMK_ModifyReportProperties"></a> Modificare le proprietà di un report di Configuration Manager  
 Nella console di Configuration Manager è possibile visualizzare le proprietà di un report, ad esempio il nome e la descrizione del report. Per modificare le proprietà, usare invece Gestione report. Usare la procedura seguente per modificare le proprietà di un report di Configuration Manager.  

#### <a name="to-modify-report-properties-in-report-manager"></a>Per modificare le proprietà dei report in Gestione report  

1.  Nel Web browser specificare l'URL di Gestione report, ad esempio, **http:\/\/Server1\/Reports**. È possibile determinare l'URL di gestione di Report sul **URL gestione Report** pagina in Gestione configurazione Reporting Services.  

2.  In Gestione report, fare clic sulla cartella dei report per Configuration Manager, ad esempio, **ConfigMgr\_CAS**.  

    > [!TIP]  
    >  Se non viene elencato alcun report, verificare che il punto di Reporting Services sia installato e configurato. Per altre informazioni, vedere [Configurazione della creazione report](configuring-reporting.md)  

3.  Fare clic sulla categoria di report per il report di cui si desidera modificare le proprietà, quindi fare clic sul collegamento per il report. Il report verrà aperto in Gestione Report.  

4.  Fare clic sulla scheda **Proprietà** . È possibile modificare il nome e la descrizione del report.  

5.  Al termine, fare clic su **Applica**. Le proprietà del report vengono salvate nel server di report e le proprietà aggiornate del report vengono recuperate dalla console di Configuration Manager.  

###  <a name="BKMK_EditReport"></a> Modificare un report di Configuration Manager  
 Se un report esistente di Configuration Manager non recupera le informazioni necessarie oppure non visualizza il layout o la struttura interessati, è possibile modificare il report in Generatore report.  

> [!NOTE]  
>  È anche possibile scegliere di clonare un report esistente aprendolo per la modifica e facendo clic su **Salva con nome** per salvarlo come nuovo report.  

> [!IMPORTANT]  
>  L'account utente deve disporre dell'autorizzazione di **modifica del sito** e **Modifica report** negli oggetti specifici associati al report che si desidera modificare.  

> [!IMPORTANT]  
>  Quando Configuration Manager viene aggiornato a una versione più recente, i report predefiniti vengono sovrascritti dai nuovi report. Se si modifica un report predefinito, è necessario eseguire il backup del report prima di installare la nuova versione, quindi ripristinare il report in Reporting Services. Se si apportano modifiche significative a un report predefinito, è consigliabile creare invece un nuovo report. I nuovi report creati prima dell'aggiornamento di un sito non verranno sovrascritti.  

 Seguire la procedura seguente per modificare le proprietà di un report di Configuration Manager.  

#### <a name="to-edit-report-properties"></a>Per modificare le proprietà dei report  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** espandere **Creazione di report**, quindi fare clic su **Report** per elencare i report disponibili.  

3.  Selezionare il report che si desidera modificare e quindi, nel gruppo **Gruppo Report** della scheda **Home** , fare clic su **Esegui**. Se richiesto, immettere l'account utente e la password e quindi fare clic su **OK**. Se Generatore report non è installato nel computer, ne verrà richiesta l'installazione. Fare clic su **Esegui** per installare Generatore report, necessario per la modifica e la creazione di report.  

4.  Modificare le impostazioni di report appropriate in Generatore report, quindi fare clic su **Salva** per salvare il report nel server di report.  

###  <a name="BKMK_CreateModelBasedReport"></a> Creare un report basato su modello  
 Un report basato su modello consente di selezionare in modo interattivo gli elementi da includere nel report. Per altre informazioni su come creare modelli di report personalizzati, vedere [Creazione di modelli di report personalizzati per System Center Configuration Manager in SQL Server Reporting Services](creating-custom-report-models-in-sql-server-reporting-services.md).  

> [!IMPORTANT]  
>  Per creare un nuovo report, l'account utente deve disporre di autorizzazioni di **modifica del sito** . L'utente può creare un report solo nelle cartelle per cui dispone di autorizzazioni di tipo **Modifica report** .  

 Seguire le procedure seguenti per creare un report di Configuration Manager basato su modello.  

#### <a name="to-create-a-model-based-report"></a>Per creare un report basato su modello  

1. Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2. Nell'area di lavoro **Monitoraggio** espandere **Creazione di report** , quindi fare clic su **Report**.  

3. Nella sezione **Crea** della scheda **Home** fare clic su **Crea report** per aprire la **Creazione guidata report**.  

4. Nella pagina **Informazioni** è possibile configurare le impostazioni seguenti:  

   - **Tipo**: selezionare **Report basato su \-modello** per creare un report in Generatore report usando un modello di Reporting Services.  

   - **Nome**: specificare un nome per il report.  

   - **Descrizione**: specificare una descrizione per il report.  

   - **Server**: visualizza il nome del server di report in cui si sta creando il report.  

   - **Percorso**: fare clic su **Sfoglia** per specificare una cartella in cui si desidera archiviare il report.  

     Fare clic su **Avanti**.  

5. Nella pagina **Selezione modello** selezionare un modello disponibile dall'elenco utilizzato per creare questo report. Quando si seleziona il modello di report, nella sezione **Anteprima** vengono visualizzate le viste e le entità di SQL Server rese disponibili dal modello di report selezionato.  

6. Nella pagina **Riepilogo** esaminare le impostazioni. Fare clic su **Indietro** per modificare le impostazioni oppure su **Avanti** per creare il report in Configuration Manager.  

7. Nella pagina **Conferma** fare clic su **Chiudi** per uscire dalla procedura guidata, quindi aprire Generatore report per configurare le impostazioni del report. Se richiesto, immettere l'account utente e la password e quindi fare clic su **OK**. Se Generatore report non è installato nel computer, ne verrà richiesta l'installazione. Fare clic su **Esegui** per installare Generatore report, necessario per la modifica e la creazione di report.  

8. In Generatore report Microsoft è possibile creare il layout del report, selezionare i dati nelle viste SQL Server disponibili, aggiungere parametri al report e così via. Per ulteriori informazioni sull'utilizzo di Generatore report per creare un nuovo report, vedere la Guida in linea di Generatore report.  

9. Fare clic su **Esegui** per eseguire il report. Verificare che il report fornisca le informazioni previste. Fare clic su **Struttura** per tornare alla visualizzazione Struttura e modificare il report, se necessario.  

10. Fare clic su **Salva** per salvare il report nel server di report. È possibile eseguire e modificare il nuovo report nel nodo **Report** nell'area di lavoro **Monitoraggio** .  

###  <a name="BKMK_CreateSQLBasedReport"></a> Creare un report basato su SQL  
 Un report basato su SQL consente di recuperare i dati che si basano su un'istruzione SQL di report.  

> [!IMPORTANT]  
>  Quando si crea un'istruzione SQL per un report personalizzato, è necessario non fare riferimento direttamente alle tabelle SQL Server. Fare invece riferimento alle viste di SQL Server per la creazione di report \(nomi di viste che iniziano con v\_\) dal database del sito. È anche possibile fare riferimento a stored procedure pubbliche \(nomi di stored procedure che iniziano con sp\_\) dal database del sito.  

> [!IMPORTANT]  
>  Per creare un nuovo report, l'account utente deve disporre di autorizzazioni di **modifica del sito** . L'utente può creare un report solo nelle cartelle per cui dispone di autorizzazioni di tipo **Modifica report** .  

 Seguire le procedure seguenti per creare un report di Configuration Manager basato su SQL.  

#### <a name="to-create-a-sql-based-report"></a>Per creare un report basato su SQL  

1. Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2. Nell'area di lavoro **Monitoraggio** espandere **Creazione di report**, quindi fare clic su **Report**.  

3. Nella sezione **Crea** della scheda **Home** fare clic su **Crea report** per aprire la **Creazione guidata report**.  

4. Nella pagina **Informazioni** è possibile configurare le impostazioni seguenti:  

   - **Tipo**: selezionare **Report basato su \-SQL** per creare un report in Generatore report usando un'istruzione SQL.  

   - **Nome**: specificare un nome per il report.  

   - **Descrizione**: specificare una descrizione per il report.  

   - **Server**: visualizza il nome del server di report in cui si sta creando il report.  

   - **Percorso**: fare clic su **Sfoglia** per specificare una cartella in cui si desidera archiviare il report.  

     Fare clic su **Avanti**.  

5. Nella pagina **Riepilogo** esaminare le impostazioni. Fare clic su **Indietro** per modificare le impostazioni oppure su **Avanti** per creare il report in Configuration Manager.  

6. Nella pagina **Conferma** fare clic su **Chiudi** per uscire dalla procedura guidata, quindi aprire Generatore report per configurare le impostazioni del report. Se richiesto, immettere l'account utente e la password e quindi fare clic su **OK**. Se Generatore report non è installato nel computer, ne verrà richiesta l'installazione. Fare clic su **Esegui** per installare Generatore report, necessario per la modifica e la creazione di report.  

7. In Generatore report Microsoft è possibile specificare l'istruzione SQL per il report oppure creare l'istruzione SQL utilizzando le colonne presenti nelle viste SQL Server disponibili, quindi aggiungere parametri al report e così via.  

8. Fare clic su **Esegui** per eseguire il report. Verificare che il report fornisca le informazioni previste. Fare clic su **Struttura** per tornare alla visualizzazione Struttura e modificare il report, se necessario.  

9. Fare clic su **Salva** per salvare il report nel server di report. È possibile eseguire il nuovo report nel nodo **Report** nell'area di lavoro **Monitoraggio** .  

##  <a name="BKMK_ManageReportSubscriptions"></a> Gestire le sottoscrizioni report  
 Le sottoscrizioni report in SQL Server Reporting Services consentono di configurare l'individuazione automatica dei report specificati tramite posta elettronica o in una condivisione file a intervalli pianificati. Usare la **Creazione guidata sottoscrizione** in System Center 2012 Configuration Manager per configurare le sottoscrizioni report.  

###  <a name="BKMK_ReportSubscriptionFileShare"></a> Creare una sottoscrizione report per recapitare un report a una condivisione file  
 Quando si crea una sottoscrizione report per il recapito di un report in una condivisione file, il report viene copiato nel formato specificato e salvato nella condivisione file specificata. È possibile effettuare la sottoscrizione e richiedere il recapito per un solo report alla volta.  

 A differenza dei report ospitati e gestiti da un server di report, i report recapitati a una cartella condivisa sono file statici. Le funzionalità interattive definite per il report non funzionano per i report archiviati come file nel file system. Le funzionalità di interazione vengono rappresentate come elementi statici. Se il report include grafici, verrà utilizzata la presentazione predefinita. Se il report è collegato tramite un altro report, verrà eseguito il rendering del collegamento come testo statico. Se si desidera conservare le funzionalità interattive in un report recapitato, utilizzare invece il recapito tramite posta elettronica. Per altre informazioni sul recapito di posta elettronica, vedere la sezione [Creare una sottoscrizione report per il recapito di un report tramite posta elettronica](#BKMK_ReportSubscriptionEmail) più avanti in questo argomento.  

 Quando si crea una sottoscrizione che utilizza il recapito in una condivisione file, è necessario specificare una cartella esistente come cartella di destinazione. Il server di report non crea le cartelle nel file system. La cartella specificata deve essere accessibile tramite una connessione di rete. Quando si specifica la cartella di destinazione in una sottoscrizione, utilizzare un percorso UNC e non includere barre rovesciate finali nel percorso della cartella. Ad esempio, un percorso UNC valido per la cartella di destinazione è: \\\\&lt;nomeserver\>\\filereport\\operazioni\\2011.  

 È possibile eseguire il rendering di report in diversi formati di file, ad esempio MHTML o Excel. Per salvare il report in un formato di file specifico, selezionare il formato di rendering durante la creazione della sottoscrizione. Ad esempio, se si sceglie Excel, il report verrà salvato come file di Microsoft Excel. Sebbene sia possibile selezionare qualsiasi formato di rendering supportato, alcuni formati funzionano meglio di altri durante il rendering in un file.  

 Utilizzare la procedura seguente per creare una sottoscrizione report per il recapito di un report in una condivisione file.  

#### <a name="to-create-a-report-subscription-to-deliver-a-report-to-a-file-share"></a>Per creare una sottoscrizione report per il recapito di un report in una condivisione file  

1. Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2. Nell'area di lavoro **Monitoraggio** espandere **Creazione di report** , quindi fare clic su **Report** per elencare i report disponibili. È possibile selezionare una cartella di report per elencare solo i report associati alla cartella.  

3. Selezionare sul report da aggiungere alla sottoscrizione, quindi nella sezione **Gruppo Report** della scheda **Home** fare clic su **Crea sottoscrizione** per aprire la **Creazione guidata sottoscrizione**.  

4. Nella pagina **Recapito sottoscrizione** è possibile configurare le impostazioni seguenti:  

   - Report recapitato da: selezionare **Condivisione file di Windows** per recapitare il report in una condivisione file.  

   - **Nome file**: specificare il nome del file per il report. Per impostazione predefinita, il file di report non include alcuna estensione di nome file. Selezionare **Aggiungi estensione file al momento della creazione** per aggiungere automaticamente un'estensione di nome file al report in base al formato di rendering.  

   - **Percorso**: specificare un percorso UNC per una cartella esistente a cui si vuole recapitare il report\(, ad esempio \\\\&lt;nome server\>\\&lt;condivisione server \>\\&lt;cartella report\>\).  

     > [!NOTE]  
     >  Il nome utente specificato in un secondo momento in questa pagina deve avere accesso alla condivisione server e deve disporre delle autorizzazioni di scrittura per la cartella di destinazione.  

   - **Formato rendering**: selezionare uno dei formati seguenti per il file di report:  

     -   **File XML con dati report**: salva il report in formato XML (Extensible Markup Language).  

     -   **CSV \(comma delimited\)** : salva il report in formato con valori \-delimitati\- da virgole.  

     -   **File TIFF**: salva il report in formato TIFF (Tagged Image File Format).  

     -   **File Acrobat \(PDF\)** : salva il report in formato Acrobat PDF (Portable Document Format).  

     -   **HTML 4.0**: salva il report come pagina Web visualizzabile solo in browser che supportano HTML 4.0. Internet Explorer 5 e le versioni successive supportano HTML 4.0.  

         > [!NOTE]  
         >  Se nel report sono presenti immagini, il formato HTML 4.0 non le includerà nel file.  

     -   **MHTML \((archivio Web)\)** : salva il report in formato MIME HTML \(mhtml\), visualizzabile in molti browser Web.  

     -   **Renderer RPL**: salva il report in formato RPL \(Report Page Layout\).  

     -   **Excel**: salva il report come foglio di calcolo di Microsoft Excel.  

     -   **Word**: salva il report come documento di Microsoft Word.  

   - **Nome utente**: specifica un account utente di Windows con autorizzazioni per l'accesso alla condivisione di server e alla cartella di destinazione. L'account utente deve avere accesso a questa condivisione di server e deve disporre dell'autorizzazione di scrittura per la cartella di destinazione.  

   - **Password**: specificare la password per l'account utente di Windows. In **Conferma password** digitare nuovamente la password.  

   - Selezionare una delle seguenti opzioni per configurare il comportamento quando esiste un file con lo stesso nome nella cartella di destinazione:  

     -   **Sovrascrivi un file esistente con una versione più recente**: specifica che quando il file di report esiste già, tale file verrà sovrascritto dalla nuova versione.  

     -   **Non sovrascrivere un file esistente**: specifica che quando il file di report esiste già non verrà eseguita alcuna azione.  

     -   **Incrementa i nomi di file quando vengono aggiunte versioni più recenti**: specifica che quando il file di report esiste già verrà aggiunto un numero al nome file del nuovo report, per distinguerlo dalle altre versioni.  

   - **Descrizione**: specifica la descrizione per la sottoscrizione report.  

     Fare clic su **Avanti**.  

5. Nella pagina **Pianificazione della sottoscrizione** selezionare una delle opzioni seguenti della pianificazione di recapito per la sottoscrizione report:  

   -   **Usa pianificazione condivisa**: una pianificazione condivisa è una pianificazione definita in precedenza che può essere usata da altre sottoscrizioni report. Selezionare questa casella di controllo e quindi selezionare una pianificazione condivisa nell'elenco, se disponibile.  

   -   **Crea nuova pianificazione**: configurare la pianificazione in base a cui viene eseguito questo report, specificando intervallo, ora e data di inizio e data di fine per la sottoscrizione.  

6. Nella pagina **Parametri sottoscrizione** specificare i parametri per questo report che verranno utilizzati per l'esecuzione automatica. Quando non sono presenti parametri per il report, questa pagina non viene visualizzata.  

7. Nella pagina **Riepilogo** verificare le impostazioni della sottoscrizione report. Fare clic su **Indietro** per modificare le impostazioni oppure su **Avanti** per creare la sottoscrizione report.  

8. Nella pagina **Completamento** fare clic su **Chiudi** per uscire dalla procedura guidata. Verificare se è stata creata correttamente la sottoscrizione report. È possibile visualizzare e modificare le sottoscrizioni report nel nodo **Sottoscrizioni** sotto **Creazione di report** nell'area di lavoro **Monitoraggio** .  

###  <a name="BKMK_ReportSubscriptionEmail"></a> Creare una sottoscrizione report per recapitare un report tramite posta elettronica  
 Quando si crea una sottoscrizione report per il recapito di un report tramite posta elettronica, un messaggio di posta elettronica verrà inviato ai destinatari configurati e il report verrà incluso come allegato. Il server di report non convalida gli indirizzi di posta elettronica né ottiene gli indirizzi di posta elettronica da un server di posta elettronica. È necessario conoscere in anticipo gli indirizzi di posta elettronica che si desidera utilizzare. Per impostazione predefinita, è possibile inviare tramite posta elettronica i report a qualsiasi account di posta elettronica valido interno o esterno all'organizzazione. È possibile selezionare una o entrambe le seguenti opzioni di recapito tramite posta elettronica:  

-   Inviare una notifica e un collegamento ipertestuale al report generato.  

-   Inviare un report collegato o incorporato. Il formato di rendering e il browser determinano se il report è incorporato o collegato. Se il browser supporta HTML 4.0 e MHTML e si seleziona il formato di rendering MHTML \(archivio Web\), il report verrà incorporato come parte del messaggio. Tutti gli altri formati di rendering \(CSV, PDF, Word e così via\) recapitano i report come allegati. Reporting Services non controlla la dimensione dell'allegato o del messaggio prima di inviare il report. Se l'allegato o messaggio supera il limite massimo consentito dal server di posta elettronica, il report non verrà recapitato.  

> [!IMPORTANT]  
>  È necessario configurare le impostazioni di posta elettronica in Reporting Services per rendere disponibile l'opzione di recapito **Posta elettronica** . Per ulteriori informazioni sulla configurazione delle impostazioni di posta elettronica in Reporting Services, vedere [Configurazione di un server di report per il recapito tramite posta elettronica](https://go.microsoft.com/fwlink/p/?LinkId=226668) nella documentazione online di SQL Server.  

 Utilizzare la procedura seguente per creare una sottoscrizione report per recapitare un report tramite posta elettronica.  

#### <a name="to-create-a-report-subscription-to-deliver-a-report-by-email"></a>Per creare una sottoscrizione report per il recapito di un report tramite posta elettronica  

-   Nella console di Configuration Manager fare clic su **Monitoraggio**.  

-   Nell'area di lavoro **Monitoraggio** espandere **Creazione di report** , quindi fare clic su **Report** per elencare i report disponibili. È possibile selezionare una cartella di report per elencare solo i report associati alla cartella.  

-   Selezionare sul report da aggiungere alla sottoscrizione, quindi nella sezione **Gruppo Report** della scheda **Home** fare clic su **Crea sottoscrizione** per aprire la **Creazione guidata sottoscrizione**.  

-   Nella pagina **Recapito sottoscrizione** è possibile configurare le impostazioni seguenti:  

    -   **Report recapitato da**: selezionare **Posta elettronica** per recapitare il report come allegato in un messaggio di posta elettronica.  

    -   **A**: specificare un indirizzo di posta elettronica valido a cui inviare questo report.  

        > [!NOTE]  
        >  È possibile immettere più destinatari di posta elettronica separando ogni indirizzo di posta elettronica con un punto e virgola.  

    -   **Cc**: facoltativamente, specificare un indirizzo di posta elettronica a cui inviare una copia questo report.  

    -   **Ccn**: facoltativamente, specificare un indirizzo di posta elettronica a cui inviare una copia nascosta questo report.  

    -   **Rispondi a**: specificare l'indirizzo di risposta da usare se il destinatario risponde al messaggio di posta elettronica.  

    -   **Oggetto**: specificare un oggetto per il messaggio di posta elettronica di sottoscrizione.  

    -   **Priorità**: selezionare il flag di priorità per il messaggio di posta elettronica. Selezionare **Bassa**, **Normale**o **Alta**. L'impostazione di priorità viene utilizzata da Microsoft Exchange per impostare un flag che indica la rilevanza del messaggio di posta elettronica.  

    -   **Commento**: specificare il testo da aggiungere al corpo del messaggio di posta elettronica di sottoscrizione.  

    -   **Descrizione**: specificare la descrizione per la sottoscrizione report.  

    -   **Includi collegamento**: include un URL per il report sottoscritto nel corpo del messaggio di posta elettronica.  

    -   **Includi report**: specifica che il rapporto è allegato al messaggio di posta elettronica. Il formato in cui verrà allegato il report viene specificato nell'elenco **Formato rendering** .  

    -   **Formato rendering**: selezionare uno dei formati seguenti per il report allegato:  

        -   **File XML con dati report**: salva il report in formato XML (Extensible Markup Language).  

        -   **CSV \(comma delimited\)** : salva il report in formato con valori \-delimitati\- da virgole.  

        -   **File TIFF**: salva il report in formato TIFF (Tagged Image File Format).  

        -   **File Acrobat \(PDF\)** : salva il report in formato Acrobat PDF (Portable Document Format).  

        -   **MHTML \((archivio Web)\)** : salva il report in formato MIME HTML \(mhtml\), visualizzabile in molti browser Web.  

        -   **Excel**: salva il report come foglio di calcolo di Microsoft Excel.  

        -   **Word**: salva il report come documento di Microsoft Word.  

-   Nella pagina **Pianificazione della sottoscrizione** selezionare una delle opzioni seguenti della pianificazione di recapito per la sottoscrizione report:  

    -   **Usa pianificazione condivisa**: una pianificazione condivisa è una pianificazione definita in precedenza che può essere usata da altre sottoscrizioni report. Selezionare questa casella di controllo e quindi selezionare una pianificazione condivisa nell'elenco, se disponibile.  

    -   **Crea nuova pianificazione**: configurare la pianificazione in base a cui viene eseguito questo report, specificando intervallo, ora e data di inizio e data di fine per la sottoscrizione.  

-   Nella pagina **Parametri sottoscrizione** specificare i parametri per questo report che verranno utilizzati per l'esecuzione automatica. Quando non sono presenti parametri per il report, questa pagina non viene visualizzata.  

-   Nella pagina **Riepilogo** verificare le impostazioni della sottoscrizione report. Fare clic su **Indietro** per modificare le impostazioni oppure su **Avanti** per creare la sottoscrizione report.  

-   Nella pagina **Completamento** fare clic su **Chiudi** per uscire dalla procedura guidata. Verificare se è stata creata correttamente la sottoscrizione report. È possibile visualizzare e modificare le sottoscrizioni report nel nodo **Sottoscrizioni** sotto **Creazione di report** nell'area di lavoro **Monitoraggio** .  

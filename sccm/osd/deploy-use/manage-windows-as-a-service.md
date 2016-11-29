---
title: Gestire Windows come servizio | Configuration Manager
description: "Le funzionalità di System Center Configuration Manager consentono di visualizzare lo stato di Windows come servizio nell'ambiente corrente per poterlo mantenere aggiornato."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da1e687b-28f6-43c4-b14a-ff2b76e60d24
caps.latest.revision: 26
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 0ed06bb30d1277afa71d1eb2d045ea0ebc87912a


---
# <a name="manage-windows-as-a-service-using-system-center-configuration-manager"></a>Gestire Windows come servizio con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


 In System Center Configuration Manager è possibile visualizzare lo stato di Windows come servizio nell'ambiente corrente, creare piani di manutenzione per formare anelli di distribuzione, verificare che i sistemi di rami di Windows 10 correnti siano mantenuti aggiornati quando vengono rilasciate nuove build e visualizzare avvisi quando i client Windows 10 si avvicinano alla scadenza del supporto per la build corrente di Current Branch (CB) o Current Branch for Business (CBB).  

 Per altre informazioni sulle opzioni di manutenzione di Windows 10, vedere le  [opzioni di manutenzione relative agli aggiornamenti di Windows 10](https://technet.microsoft.com/library/mt598226\(v=vs.85\).aspx).  

 Usare le sezioni seguenti per gestire Windows come servizio.

##  <a name="a-namebkmkprerequisitesa-prerequisites"></a><a name="BKMK_Prerequisites"></a> Prerequisiti  
 Per visualizzare i dati nel dashboard di manutenzione di Windows 10 è necessario seguire questa procedura:  

-   I computer Windows 10 devono usare gli aggiornamenti software di Configuration Manager con Windows Server Update Services (WSUS) per la gestione degli aggiornamenti software. Se la gestione degli aggiornamenti software avviene tramite Windows Update per Business o Windows Insider, il computer non viene valutato nei piani di manutenzione di Windows 10. Per altre informazioni, vedere [Integration with Windows Update for Business in Windows 10](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

-   Installare WSUS 4.0 con l' [hotfix 3095113](https://support.microsoft.com/kb/3095113) nei punti di aggiornamento software e nei server del sito. Questo consente di aggiungere la classificazione degli aggiornamenti software **Aggiornamenti** . Per altre informazioni, vedere [Prerequisiti per aggiornamenti software](../../sum/plan-design/prerequisites-for-software-updates.md).  

-   È necessario che WSUS 4.0 con [hotfix 3159706](https://support.microsoft.com/kb/3159706) sia installato nei punti di aggiornamento software e nel server del sito per eseguire l'aggiornamento dei computer a Windows 10 Anniversary Update e alle versioni successive. Per installare l'hotfix è necessario eseguire i passaggi manuali descritti nell'articolo del supporto tecnico. Per altre informazioni, vedere [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/05/update-your-configmgr-1606-sup-servers-to-deploy-the-windows-10-anniversary-update/) (Blog sulla sicurezza e la mobilità aziendale).

-   Abilitare Individuazione heartbeat. I dati visualizzati nel dashboard di manutenzione di Windows 10 vengono rilevati con l'individuazione. Per altre informazioni, vedere [Configure Heartbeat Discovery](../../core/servers/deploy/configure/configure-discovery-methods.md#a-namebkmkconfighbdisca-configure-heartbeat-discovery).  

     Le informazioni riportate di seguito sul ramo e la build di Windows 10 vengono rilevate e memorizzate negli attributi seguenti:  

    -   **Ramo per la conformità del sistema operativo**: specifica il ramo del sistema operativo. Ad esempio, **0** = CB (Non rinviare gli aggiornamenti), **1** = CBB (Rinvia gli aggiornamenti), **2** = Long Term Servicing Branch (LTSB)

    -   **Build del sistema operativo**: specifica la build del sistema operativo. Ad esempio, **10.0.10240** (RTM) o **10.0.10586** (versione 1511)  

-   Installare e configurare il punto di connessione del servizio per la modalità **Online, connessione permanente** , per poter visualizzare i dati nel dashboard di manutenzione di Windows 10. In modalità offline gli aggiornamenti dei dati non vengono visualizzati nel dashboard fino a quando non si ottengono aggiornamenti di manutenzione di Configuration Manager.   
     Per altre informazioni, vedere [Informazioni sul punto di connessione del servizio](../../core/servers/deploy/configure/about-the-service-connection-point.md).  

-   Specificare l'impostazione di Criteri di gruppo, **Rimanda gli aggiornamenti**, per determinare se un computer è CB o CBB.  

-   Verificare che nel computer che esegue la console di Configuration Manager sia installato Internet Explorer 9 o versione successiva.  

-   Assicurarsi che gli aggiornamenti software siano configurati e sincronizzati nella console. Per rendere disponibili gli eventuali aggiornamenti delle funzionalità di Windows 10 nella console di Configuration Manager, è necessario selezionare la classificazione **Aggiornamenti** e sincronizzare gli aggiornamenti software. Per altre informazioni, vedere [Prerequisiti per aggiornamenti software](../../sum/get-started/prepare-for-software-updates-management.md).  

##  <a name="a-namebkmkservicingdashboarda-windows-10-servicing-dashboard"></a><a name="BKMK_ServicingDashboard"></a> Dashboard di manutenzione di Windows 10  
 Il dashboard di manutenzione di Windows 10 fornisce informazioni sui computer Windows 10 nell'ambiente, piani di manutenzione attivi, informazioni di conformità e così via. I dati disponibili nel dashboard di manutenzione di Windows 10 variano a seconda che il punto di connessione del servizio sia installato o meno. Il dashboard include i riquadri seguenti:  

-   **Riquadro Utilizzo di Windows 10**: fornisce un riepilogo delle build pubbliche di Windows 10. Le build di Windows Insider sono elencate come **altro** insieme ad altre eventuali build che non sono note al sito. Il punto di connessione del servizio scarica i metadati contenenti informazioni sulle build di Windows, dati che vengono messi a confronto con i dati di individuazione.  

-   **Riquadro Anelli di Windows 10**: fornisce un riepilogo di Windows 10 in base ai rami e allo stato di conformità. Il segmento LTSB include tutte le versioni LTSB, mentre il primo riquadro riepiloga le versioni specifiche, ad esempio Windows 10 LTSB 2015. Il segmento **Release Ready** corrisponde a CB, mentre il segmento **Business Ready** corrisponde a CBB.  

-   **Riquadro Crea piano di manutenzione**: offre un modo rapido per creare un piano di manutenzione. Specificare il nome e la raccolta, tenendo presente che vengono visualizzate solo le prime dieci raccolte per dimensioni, a partire dalla più piccola. Specificare anche lo stato di conformità e il pacchetto di distribuzione, tenendo presente che vengono visualizzati solo i primi dieci pacchetti modificati più di recente. Per le altre impostazioni vengono usati i valori predefiniti. Fare clic su **Impostazioni avanzate** per avviare la procedura guidata Crea piano di manutenzione in cui è possibile configurare tutte le impostazioni del piano di servizio.  

-   **Riquadro Scaduta**: visualizza la percentuale di dispositivi presenti in una build di Windows 10 che ha superato la scadenza. Configuration Manager determina tale percentuale dai metadati scaricati dal punto di connessione del servizio messi a confronto con i dati di individuazione. Una build che ha superato la scadenza non riceve più gli aggiornamenti cumulativi mensili, inclusi gli aggiornamenti della sicurezza. I computer in questa categoria devono essere aggiornati alla versione successiva della build. Configuration Manager arrotonda al numero intero successivo. Ad esempio, se si hanno 10.000 computer e soltanto uno si trova in una build scaduta, il riquadro restituirà 1%.  

-   **Riquadro Scade a breve**: visualizza la percentuale di computer presenti in una build in procinto di scadere nei quattro mesi successivi, analogamente al riquadro **Scaduta** . Configuration Manager arrotonda al numero intero successivo.  

-   **Riquadro Avvisi**: visualizza gli avvisi attivi.  

-   **Riquadro Monitoraggio piano di manutenzione**: visualizza i piani di manutenzione creati e un grafico della conformità per ognuno. Offre così una rapida panoramica dello stato attuale delle distribuzioni del piano di manutenzione. Se un anello di distribuzione precedente soddisfa le previsioni di conformità, è possibile selezionare un piano di manutenzione o un anello di distribuzione successivo e fare clic su **Distribuisci ora** , anziché attendere l'attivazione automatica delle regole del piano di manutenzione.  

-   **Riquadro Build di Windows 10**: visualizza l'immagine fissa di una sequenza temporale che fornisce una panoramica generale delle build di Windows 10 attualmente rilasciate e del momento in cui passeranno a stati diversi.  

> [!IMPORTANT]  
>  Le informazioni visualizzate nel dashboard di manutenzione di Windows 10, ad esempio il ciclo di vita del supporto per le versioni di Windows 10, vengono fornite per agevolare l'utente e sono destinate solo all'uso interno all'azienda. Non fare affidamento esclusivamente su queste informazioni per accertare la conformità dell'aggiornamento. Verificare l'accuratezza delle informazioni fornite.  

## <a name="servicing-plan-workflow"></a>Flusso di lavoro del piano di manutenzione  
 I piani di manutenzione di Windows 10 in Configuration Manager sono molto simili alle regole di distribuzione automatica degli aggiornamenti software. Creare un piano di manutenzione con i criteri seguenti, che verrà valutato da Configuration Manager:  

-   **Classificazione Aggiornamenti**: vengono valutati solo gli aggiornamenti presenti nella classificazione **Aggiornamenti** .  

-   **Stato di conformità**: lo stato di conformità definito nel piano di manutenzione viene confrontato con lo stato di conformità per l'aggiornamento. I metadati per l'aggiornamento vengono recuperati quando il punto di connessione del servizio verifica la disponibilità di aggiornamenti.  

-   **Differimento**: numero di giorni specificato per l'impostazione **Dopo quanti giorni dalla pubblicazione di un nuovo aggiornamento di Microsoft si vuole eseguire la distribuzione nell'ambiente** nel piano di manutenzione. Configuration Manager valuta se includere un aggiornamento nella distribuzione, se la data corrente è successiva alla data di rilascio più il numero di giorni configurato.  

 Quando un aggiornamento soddisfa i criteri, il piano di manutenzione aggiunge l'aggiornamento al pacchetto di distribuzione, distribuisce il pacchetto nei punti di distribuzione e distribuisce l'aggiornamento nella raccolta in base alle impostazioni configurate nel piano di manutenzione.  È possibile monitorare le distribuzioni nel riquadro piano di monitoraggio del piano del servizio, nel dashboard di manutenzione di Windows 10. Per altre informazioni, vedere [Monitorare gli aggiornamenti software](../../sum/deploy-use/monitor-software-updates.md).  

##  <a name="a-namebkmkservicingplana-windows-10-servicing-plan"></a><a name="BKMK_ServicingPlan"></a> Piano di manutenzione di Windows 10  
 Quando si distribuisce Windows 10 CB, è possibile creare uno o più piani di manutenzione per definire gli anelli di distribuzione per l'ambiente usato e monitorarli successivamente nel dashboard di manutenzione di Windows 10.   
I piani di manutenzione usano solo la classificazione degli aggiornamenti software **Aggiornamenti** e non gli aggiornamenti cumulativi per Windows 10. Per tali aggiornamenti è ancora necessario eseguire la distribuzione usando il flusso di lavoro degli aggiornamenti software.  Il piano di manutenzione e gli aggiornamenti software offrono la stessa esperienza all'utente finale, incluse le impostazioni configurate nel piano di manutenzione.  

> [!NOTE]  
>  È possibile usare una sequenza di attività per distribuire un aggiornamento per ogni build di Windows 10, ma questo richiede un maggiore intervento manuale. Sarebbe necessario importare i file di origine aggiornati come un pacchetto di aggiornamento del sistema operativo e quindi creare e distribuire la sequenza di attività per il set di computer appropriato. Tuttavia, una sequenza di attività offre altre opzioni personalizzate, ad esempio le azioni di pre-distribuzione e post-distribuzione.  

 È possibile creare un piano di manutenzione di base dal dashboard di manutenzione di Windows 10. Dopo aver specificato il nome, la raccolta (vengono visualizzate solo le prime dieci raccolte per dimensioni, a partire dalla più piccola), il pacchetto di distribuzione (vengono visualizzati solo i primi dieci pacchetti modificati più di recente) e lo stato di conformità, Configuration Manager crea il piano di manutenzione con valori predefiniti per le altre impostazioni. È anche possibile avviare la procedura guidata Crea piano di manutenzione per configurare tutte le impostazioni. Usare la procedura seguente per creare un piano di manutenzione con la procedura guidata Crea piano di manutenzione.  

> [!NOTE]  
>  A partire dalla versione 1602 di Configuration Manager, è possibile gestire il comportamento relativo alle distribuzioni ad alto rischio. Una distribuzione ad alto rischio viene installata automaticamente e può causare risultati imprevisti. Ad esempio, una sequenza di attività con scopo impostato su **Obbligatorio** e che distribuisce Windows 10 viene considerata una distribuzione ad alto rischio. Per altre informazioni, vedere [Impostazioni per gestire distribuzioni ad alto rischio](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

#### <a name="to-create-a-windows-10-servicing-plan"></a>Per creare un piano di manutenzione di Windows 10  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro Raccolta software espandere **Manutenzione di Windows 10**e quindi fare clic su **Piani di manutenzione**.  

3.  Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea piano di manutenzione**. Verrà avviata la procedura guidata Crea piano di manutenzione.  

4.  Nella pagina **Generale** è possibile configurare le seguenti impostazioni:  

    -   **Nome**: specificare il nome per il piano di manutenzione. Il nome deve essere univoco, descrivere l'obiettivo della regola e contribuire a differenziarla dalle altre presenti nel sito di Configuration Manager.  

    -   **Descrizione**: specificare una descrizione per il piano di manutenzione. La descrizione deve fornire una panoramica del piano di manutenzione e qualsiasi altra informazione rilevante per identificare e differenziare il piano dagli altri nel sito di Configuration Manager. Il campo della descrizione è facoltativo, ha un limite di 256 caratteri e un valore vuoto per impostazione predefinita.  

5.  Nella pagina Piano di manutenzione è possibile configurare le impostazioni seguenti:  

    -   **Raccolta di destinazione**: specifica la raccolta di destinazione da usare per il piano di manutenzione. I membri della raccolta ricevono gli aggiornamenti di Windows 10 definiti nel piano di manutenzione.  

    > [!NOTE]  
    >  A partire dalla versione 1602 di Configuration Manager, quando si esegue una distribuzione ad alto rischio, ad esempio quella di un piano di manutenzione, la finestra **Seleziona raccolta** visualizza soltanto le raccolte personalizzate che soddisfano le impostazioni di verifica della distribuzione configurate nelle proprietà del sito. Le distribuzioni ad alto rischio sono sempre limitate alle raccolte personalizzate (quelle create dall'utente) e alla racconta predefinita **Computer sconosciuti** . Quando si crea una distribuzione ad alto rischio, non è possibile selezionare una raccolta predefinita quale **Tutti i sistemi**. Deselezionare **Nascondi le raccolte con un numero di membri maggiore della configurazione delle dimensioni minime del sito** per visualizzare tutte le raccolte personalizzate che contengono un numero di client inferiore rispetto alla dimensione massima configurata. Per altre informazioni, vedere [Impostazioni per gestire distribuzioni ad alto rischio](../../protect/understand/settings-to-manage-high-risk-deployments.md).  
    > Le impostazioni di verifica della distribuzione sono basate sull'appartenenza attuale della raccolta. Dopo aver distribuito il piano di manutenzione, l'appartenenza alla raccolta non viene rivalutata per le impostazioni di distribuzione ad alto rischio.  
    > Ad esempio, si supponga di impostare **Dimensione predefinita** su 100 e **Dimensione massima** su 1000. Quando si crea una distribuzione ad alto rischio, nella finestra **Seleziona raccolta** verranno visualizzate solo le raccolte che contengono meno di 100 client. Se si deseleziona l'impostazione **Nascondi le raccolte con un numero di membri maggiore della configurazione delle dimensioni minime del sito**, nella finestra vengono visualizzate le raccolte che includono meno di 1000 client.  
    > Quando si seleziona una raccolta che include un ruolo del sito, sono valide le condizioni seguenti:  
    >   
    >  -   Se la raccolta contiene un server di sistema del sito e le impostazioni di verifica della distribuzione sono state configurate in modo da bloccare le raccolte con server di sistema del sito, si verifica un errore e la procedura si arresta.  
    > -   Se la raccolta include un server di sistema del sito e nelle impostazioni di verifica della distribuzione configurate dall'utente viene riportata la presenza di tali server di sistema del sito, se la raccolta supera la dimensione predefinita oppure se la raccolta include un server, nella distribuzione guidata del software verrà visualizzato un messaggio sul rischio elevato dell'operazione. È necessario accettare di creare una distribuzione ad alto rischio, quindi viene creato un messaggio di stato relativo al controllo.  

6.  Nella pagina Anello di distribuzione configurare le impostazioni seguenti:  

    -   **Specificare lo stato di conformità di Windows a cui applicare questo piano di manutenzione**: selezionare una delle opzioni riportate di seguito.  

        -   **Release Ready (Current Branch)**:  

        -   **Business Ready (Current Branch for Business**:  

    -   **Dopo quanti giorni dalla pubblicazione di un nuovo aggiornamento di Microsoft si vuole eseguire la distribuzione nell'ambiente**:  

    -   Per le versioni precedenti alla versione 1602 di Configuration Manager, fare clic su **Anteprima** per visualizzare gli aggiornamenti di Windows 10 associati allo stato di conformità.  

7.  A partire dalla versione 1602 di Configuration Manager, nella pagina Aggiornamenti configurare i criteri di ricerca per filtrare gli aggiornamenti che verranno aggiunti al piano di manutenzione. Verranno aggiunti alla distribuzione associata solo gli aggiornamenti che soddisfano i criteri specificati.  

     Fare clic su **Anteprima** per visualizzare gli aggiornamenti che soddisfano i criteri specificati.  

8.  Nella pagina Pianificazione della distribuzione configurare le seguenti impostazioni:  

    -   **Pianificazione valutazione**: specificare se Configuration Manager valuta il tempo disponibile e le scadenze dell'installazione in base all'ora UTC o all'ora locale del computer su cui è in esecuzione la console di Configuration Manager.  

        > [!NOTE]  
        >  Quando si seleziona l'ora locale e quindi si sceglie **Appena possibile** per **Tempo disponibile software** o **Scadenza installazione**, per valutare quando sono disponibili aggiornamento o quando vengono installati in un client, viene usata l'ora corrente del computer che esegue la console di Configuration Manager. Se il client si trova in un fuso orario diverso, verranno eseguite le azioni seguenti quando l'ora del client raggiunge quella impostata per la valutazione.  

    -   **Tempo disponibile software**: selezionare una delle seguenti impostazioni per specificare quando gli aggiornamenti del software saranno disponibili per i client:  

        -   **Appena possibile**: selezionare questa impostazione per rendere disponibili il prima possibile gli aggiornamenti software inclusi nella distribuzione per i computer client. Quando si crea la distribuzione con questa impostazione selezionata, Configuration Manager aggiorna i criteri client. Quindi, al successivo ciclo di polling dei criteri client, ai client viene comunicata la distribuzione e possono ottenere gli aggiornamenti disponibili per l'installazione.  

        -   **Orario specifico**: selezionare questa impostazione per rendere disponibili gli aggiornamenti software inclusi nella distribuzione per i computer client in una data e a un orario specifici. Quando si crea la distribuzione con questa impostazione attivata, Configuration Manager aggiorna i criteri client. Quindi, al successivo ciclo di polling dei criteri client, ai client viene comunicata la distribuzione. Tuttavia, gli aggiornamenti del software nella distribuzione non saranno disponibili per l'installazione prima della data e dell'orario configurati.  

    -   **Scadenza installazione**: selezionare una delle seguenti impostazioni per specificare la scadenza per l'installazione degli aggiornamenti software nella distribuzione:  

        -   **Appena possibile**: selezionare questa impostazione per installare automaticamente gli aggiornamenti software nella distribuzione appena possibile.  

        -   **Orario specifico**: selezionare questa impostazione per installare automaticamente gli aggiornamenti software nella distribuzione in una data e a un orario specifici. Configuration Manager determina la scadenza per installare gli aggiornamenti software aggiungendo l'intervallo **Orario specifico** configurato a **Tempo disponibile software**.  

        > [!NOTE]  
        >  L'orario effettivo di scadenza dell'installazione corrisponde all'ora di scadenza visualizzata più una quantità di tempo casuale di massimo 2 ore. Ciò consente di ridurre il potenziale impatto di un'installazione simultanea degli aggiornamenti nella distribuzione da parte di tutti i computer client nella raccolta di destinazione.  
        >   
        >  È possibile configurare l'impostazione **Disabilitare sequenza casuale scadenza** del client **Agente computer** per disabilitare il ritardo della sequenza casuale di installazione per gli aggiornamenti richiesti. Per ulteriori informazioni, vedere [Computer Agent](../../core/clients/deploy/about-client-settings.md#BKMK_ComputerAgentDeviceSettings).  

9. Nella pagina Esperienza utente, è possibile configurare le seguenti impostazioni:  

    -   **Notifiche utente**: specificare se visualizzare la notifica degli aggiornamenti in Software Center nel computer client in base al **Tempo disponibile software** configurato e se visualizzare le notifiche utente nei computer client.  

    -   **Comportamento scadenza**: specificare il comportamento che deve verificarsi quando si raggiunge la data di scadenza per la distribuzione degli aggiornamenti. Specificare se installare gli aggiornamenti nella distribuzione. Specificare anche se eseguire un riavvio del sistema dopo l'installazione dell'aggiornamento, indipendentemente da una finestra di manutenzione configurata. Per altre informazioni sulle finestre di manutenzione, vedere [Come usare le finestre di manutenzione](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportamento riavvio dispositivo**: specificare se evitare un riavvio del sistema in server e workstation dopo l'installazione degli aggiornamenti e se è richiesto un riavvio del sistema per completare l'installazione.  

    -   **Gestione filtri di scrittura per dispositivi con Windows Embedded**: quando si distribuiscono aggiornamenti in dispositivi con Windows Embedded abilitati per i filtri di scrittura, è possibile specificare di installare l'aggiornamento nella sovrapposizione temporanea e confermare le modifiche in seguito oppure alla scadenza dell'installazione o all'interno di una finestra di manutenzione. Quando si confermano le modifiche alla scadenza dell'installazione o all'interno di una finestra di manutenzione, è necessario il riavvio per mantenere le modifiche nel dispositivo.  

        > [!NOTE]  
        >  Quando si distribuisce un aggiornamento in un dispositivo con Windows Embedded, verificare che il dispositivo appartenga a una raccolta con una finestra di manutenzione configurata.  

10. Nella pagina Pacchetto di distribuzione selezionare un pacchetto di distribuzione esistente o configurare le seguenti impostazioni per creare un nuovo pacchetto di distribuzione:  

    1.  **Nome**: specificare il nome del pacchetto di distribuzione. Deve essere un nome univoco che descrive il contenuto del pacchetto. Deve essere lungo massimo 50 caratteri.  

    2.  **Descrizione**: specificare una descrizione che fornisca informazioni sul pacchetto di distribuzione. La descrizione deve contenere un massimo di 127 caratteri.  

    3.  **Origine pacchetto**: specifica il percorso dei file di origine dell'aggiornamento software.  Digitare un percorso di rete per il percorso di origine, ad esempio **\\\server\nomecondivisione\percorso**oppure fare clic su **Sfoglia** per trovare il percorso di rete. Prima di procedere alla pagina successiva, è necessario creare la cartella condivisa per i file di origine del pacchetto di distribuzione.  

        > [!NOTE]  
        >  Il percorso di origine del pacchetto di distribuzione specificato non può essere usato da un altro pacchetto di distribuzione software.  

        > [!IMPORTANT]  
        >  L'account computer del provider SMS e l'utente che esegue la procedura guidata per scaricare gli aggiornamenti software devono disporre entrambi delle autorizzazioni NTFS di **Scrittura** nel percorso download. È necessario limitare con attenzione l'accesso al percorso download per ridurre il rischio di manomissioni da parte di utenti malintenzionati dei file origine degli aggiornamenti software.  

        > [!IMPORTANT]  
        >  È possibile modificare il percorso di origine del pacchetto nelle proprietà del pacchetto di distribuzione dopo che Configuration Manager ha creato il pacchetto di distribuzione. Ma in tal caso, è prima necessario copiare il contenuto dall'origine del pacchetto originale nel nuovo percorso di origine del pacchetto.  

    4.  **Priorità di invio**: specificare la priorità di invio per il pacchetto di distribuzione. Configuration Manager usa la priorità di invio quando invia il pacchetto di distribuzione ai punti di distribuzione. I pacchetti di distribuzione vengono inviati in ordine di priorità: Alta, Media o Bassa. I pacchetti con priorità identiche vengono inviati nell'ordine in cui sono stati creati. Se non esiste nessun backlog, il pacchetto eseguirà l'elaborazione immediatamente indipendentemente dalla relativa priorità.  

11. Nella pagina Punti di distribuzione specificare i punti di distribuzione o i gruppi di punti di distribuzione che ospiteranno i file di aggiornamento. Per altre informazioni sui punti di distribuzione, vedere [Distribution point configurations](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#a-namebkmkconfigsa-distribution-point-configurations).  

    > [!NOTE]  
    >  Questa pagina è disponibile solo quando si crea un nuovo pacchetto di distribuzione di aggiornamento software.  

12. Nella pagina Percorso download specificare se scaricare i file di aggiornamento da Internet o dalla rete locale. Configurare le seguenti impostazioni:  

    -   **Scarica aggiornamenti software da Internet**: selezionare questa impostazione per scaricare gli aggiornamenti da un percorso specificato in Internet. Questa opzione è attivata per impostazione predefinita.  

    -   **Scarica aggiornamenti software da un percorso sulla rete locale**: selezionare questa impostazione per scaricare gli aggiornamenti da una directory locale o una cartella condivisa. Questa impostazione è utile quando il computer che esegue la procedura guidata non dispone di accesso a Internet. I computer con accesso a Internet possono scaricare preventivamente gli aggiornamenti e archiviarli in un percorso di rete locale accessibile al computer che esegue la procedura guidata.  

13. Nella pagina Selezione lingua selezionare le lingue per cui vengono scaricati gli aggiornamenti selezionati. Gli aggiornamenti vengono scaricati solo se sono disponibili nelle lingue selezionate. Gli aggiornamenti non specifici per la lingua vengono sempre scaricati. Per impostazione predefinita, la procedura guidata consente di selezionare le lingue configurate nelle proprietà del punto di aggiornamento software. Prima di procedere alla pagina successiva, è necessario selezionare almeno una lingua. Quando si selezionano solo lingue non supportate da un aggiornamento, il download dell'aggiornamento avrà esito negativo.  

14. Nella pagina Riepilogo rivedere le impostazioni e fare clic su **Avanti** per creare il piano di manutenzione.  

 Dopo aver completato la procedura guidata, verrà eseguito il piano di manutenzione. Gli aggiornamenti che soddisfano i criteri specificati vengono aggiunti a un gruppo di aggiornamenti software, scaricati nella raccolta contenuto, nel server del sito, e distribuiti ai punti di distribuzione configurati. Il gruppo di aggiornamenti software viene quindi distribuito ai client inclusi nella raccolta di destinazione.  

##  <a name="a-namebkmkmodifyservicingplana-modify-a-servicing-plan"></a><a name="BKMK_ModifyServicingPlan"></a> Modificare un piano di manutenzione  
 Dopo aver creato un piano di manutenzione di base dal dashboard di manutenzione di Windows 10 oppure se è necessario modificare le impostazioni per un piano di manutenzione esistente, è possibile passare alle proprietà del piano di manutenzione. Per modificare le proprietà di un piano di manutenzione, seguire la procedura riportata di seguito.  

#### <a name="to-modify-the-properties-of-a-servicing-plan"></a>Per modificare le proprietà di un piano di manutenzione  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro Raccolta software espandere **Manutenzione di Windows 10**, fare clic su **Piani di manutenzione**e quindi selezionare il piano di manutenzione che si vuole modificare.  

3.  Nella scheda **Home** fare clic su **Proprietà** per aprire le proprietà del piano di manutenzione selezionato.  



<!--HONumber=Nov16_HO1-->


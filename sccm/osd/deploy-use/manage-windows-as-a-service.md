---
title: Gestire Windows come servizio
titleSuffix: Configuration Manager
description: Visualizzare lo stato di Windows as a Service (WaaS) usando Configuration Manager, definire piani di manutenzione per formare anelli di distribuzione e visualizzare avvisi quando i client Windows 10 si avvicinano alla scadenza del supporto.
ms.date: 04/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: da1e687b-28f6-43c4-b14a-ff2b76e60d24
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 13fde17d8fe46b723a8f49b22a68685fbc4d47de
ms.sourcegitcommit: d4b0e44e6bb06a830d0887493528d9166a15154b
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 04/11/2019
ms.locfileid: "59506244"
---
# <a name="manage-windows-as-a-service-using-system-center-configuration-manager"></a>Gestire Windows come servizio con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


 In Configuration Manager è possibile visualizzare lo stato di Windows as a Service (WaaS) nell'ambiente in uso. È possibile creare piani di manutenzione per formare anelli di distribuzione, verificare che i sistemi Windows 10 siano mantenuti aggiornati quando vengono rilasciate nuove build e visualizzare avvisi quando i client Windows 10 si avvicinano alla scadenza del supporto per la build di canale semestrale in uso.  

 Per altre informazioni sulle opzioni di manutenzione di Windows 10, vedere [Panoramica di Windows as a Service](/windows/deployment/update/waas-overview#servicing-channels).  

 Usare le sezioni seguenti per gestire Windows come servizio.



##  <a name="BKMK_Prerequisites"></a> Prerequisiti  
 Per visualizzare i dati nel dashboard di manutenzione di Windows 10 è necessario seguire questa procedura:  

-   I computer Windows 10 devono usare gli aggiornamenti software di Configuration Manager con Windows Server Update Services (WSUS) per la gestione degli aggiornamenti software. Se la gestione degli aggiornamenti software avviene tramite Windows Update per le aziende o Windows Insider, il computer non viene valutato nei piani di manutenzione di Windows 10. Per altre informazioni, vedere [Integrazione con Windows Update for Business in Windows 10](../../sum/deploy-use/integrate-windows-update-for-business-windows-10.md).  

-   Installare WSUS 4.0 con l' [hotfix 3095113](https://support.microsoft.com/kb/3095113) nei punti di aggiornamento software e nei server del sito. Questo hotfix aggiunge la classificazione di aggiornamento software **Aggiornamenti**. Per altre informazioni, vedere [Prerequisiti per aggiornamenti software](../../sum/plan-design/prerequisites-for-software-updates.md).  

-   È necessario che WSUS 4.0 con [hotfix 3159706](https://support.microsoft.com/kb/3159706) sia installato nei punti di aggiornamento software e nel server del sito per eseguire l'aggiornamento dei computer a Windows 10 Anniversary Update e alle versioni successive. Per installare l'hotfix è necessario eseguire i passaggi manuali descritti nell'articolo del supporto tecnico. Per altre informazioni, vedere [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/05/update-your-configmgr-1606-sup-servers-to-deploy-the-windows-10-anniversary-update/) (Blog sulla sicurezza e la mobilità aziendale).

-   Abilitare Individuazione heartbeat. I dati visualizzati nel dashboard di manutenzione di Windows 10 vengono rilevati con l'individuazione. Per altre informazioni, vedere [Configure Heartbeat Discovery](../../core/servers/deploy/configure/configure-discovery-methods.md#BKMK_ConfigHBDisc).  

     Le informazioni sul canale e sulla build di Windows 10 riportate di seguito vengono rilevate e archiviate negli attributi seguenti:  

    -   **Ramo per la conformità del sistema operativo**: specifica il canale del sistema operativo. Ad esempio, **0** = Canale semestrale - Mirato (non rinviare gli aggiornamenti), **1** = Canale semestrale (rinvia gli aggiornamenti), **2** = Canale di manutenzione a lungo termine (LTSC, Long-Term Servicing Channel)

    -   **Build del sistema operativo**: specifica la build del sistema operativo. Ad esempio, **10.0.10240** (RTM) o **10.0.10586** (versione 1511)  

-   Per visualizzare i dati nel dashboard di manutenzione di Windows 10 è necessario installare il punto di connessione del servizio e configurarlo per la modalità **Online, connessione permanente**. In modalità offline gli aggiornamenti dei dati non vengono visualizzati nel dashboard fino a quando non si ottengono aggiornamenti di manutenzione di Configuration Manager. Per altre informazioni, vedere [Informazioni sul punto di connessione del servizio](../../core/servers/deploy/configure/about-the-service-connection-point.md).  


-   Verificare che nel computer che esegue la console di Configuration Manager sia installato Internet Explorer 9 o versione successiva.  

-   Assicurarsi che gli aggiornamenti software siano configurati e sincronizzati nella console. Per rendere disponibili gli eventuali aggiornamenti delle funzionalità di Windows 10 nella console di Configuration Manager, selezionare la classificazione **Aggiornamenti** e sincronizzare gli aggiornamenti software. Per altre informazioni, vedere [Prerequisiti per aggiornamenti software](../../sum/get-started/prepare-for-software-updates-management.md).  
- A partire da Configuration Manager versione 1902 verificare l'impostazione client **Specificare la priorità del thread per gli aggiornamenti delle funzionalità** [ ](/sccm/core/clients/deploy/about-client-settings#bkmk_thread-priority) per assicurarsi che sia appropriata per l'ambiente in uso.

##  <a name="BKMK_ServicingDashboard"></a> Dashboard di manutenzione di Windows 10  
 Il dashboard di manutenzione di Windows 10 fornisce informazioni sui computer Windows 10 nell'ambiente, piani di manutenzione attivi, informazioni di conformità e così via. I dati disponibili nel dashboard di manutenzione di Windows 10 variano a seconda che il punto di connessione del servizio sia installato o meno. Il dashboard include i riquadri seguenti:  

-   **Riquadro Utilizzo di Windows 10**: contiene un riepilogo delle build pubbliche di Windows 10. Le build di Windows Insider sono elencate come **altro** insieme ad altre eventuali build che non sono note al sito. Il punto di connessione del servizio scarica i metadati contenenti informazioni sulle build di Windows. Questi dati vengono quindi confrontati con i dati di individuazione.  

-   **Riquadro Anelli di Windows 10**: contiene un riepilogo di Windows 10 in base ai canali e allo stato di conformità. Il segmento LTSC include tutte le versioni LTSC. Il primo riquadro contiene un riepilogo dettagliato di versioni specifiche, ad esempio Windows 10 LTSC 2015.   

-   **Riquadro Crea piano di manutenzione**: offre un modo rapido per creare un piano di manutenzione. Specificare il nome e la raccolta, tenendo presente che vengono visualizzate solo le prime 10 raccolte per dimensioni, a partire dalla più piccola. Specificare anche lo stato di conformità e il pacchetto di distribuzione, tenendo presente che vengono visualizzati solo i primi 10 pacchetti modificati più di recente. Per le altre impostazioni vengono usati i valori predefiniti. Fare clic su **Impostazioni avanzate** per avviare la procedura guidata Crea piano di manutenzione in cui è possibile configurare tutte le impostazioni del piano di servizio.  

-   **Riquadro Scaduta**: visualizza la percentuale di dispositivi presenti in una build di Windows 10 che ha superato la scadenza. Configuration Manager determina tale percentuale dai metadati scaricati dal punto di connessione del servizio messi a confronto con i dati di individuazione. Una build che ha superato la scadenza non riceve più gli aggiornamenti cumulativi mensili, inclusi gli aggiornamenti della sicurezza. I computer in questa categoria devono essere aggiornati alla versione successiva della build. Configuration Manager arrotonda al numero intero successivo. Ad esempio, se si hanno 10.000 computer e soltanto uno con una build scaduta, il riquadro restituisce 1%.  

-   **Riquadro Scade a breve**: visualizza la percentuale di computer presenti in una build in procinto di scadere nei quattro mesi successivi, analogamente al riquadro **Scaduta** . Configuration Manager arrotonda al numero intero successivo.  

-   **Riquadro Avvisi**: visualizza gli avvisi attivi.  

-   **Riquadro Monitoraggio piano di manutenzione**: visualizza i piani di manutenzione creati e un grafico della conformità per ognuno. Questo riquadro offre una rapida panoramica dello stato attuale delle distribuzioni del piano di manutenzione. Se un anello di distribuzione precedente soddisfa le previsioni di conformità, è possibile selezionare un piano di manutenzione o un anello di distribuzione successivo e fare clic su **Distribuisci ora** , anziché attendere l'attivazione automatica delle regole del piano di manutenzione.  

-   Il **riquadro delle build di Windows 10** visualizza l'immagine fissa di una sequenza temporale che offre una panoramica delle build di Windows 10 attualmente rilasciate e informazioni generali sul momento in cui passeranno a stati diversi. Questo riquadro è stato rimosso a partire da Configuration Manager versione 1902. Sono infatti disponibili informazioni più dettagliate nel [dashboard del ciclo di vita del prodotto](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard). <!--3446861-->

> [!IMPORTANT]  
>  Le informazioni visualizzate nel dashboard di manutenzione di Windows 10, ad esempio il ciclo di vita del supporto per le versioni di Windows 10, vengono fornite per agevolare l'utente e sono destinate solo all'uso interno all'azienda. Non fare affidamento esclusivamente su queste informazioni per accertare la conformità dell'aggiornamento. Verificare l'accuratezza delle informazioni fornite.  

## <a name="servicing-plan-workflow"></a>Flusso di lavoro del piano di manutenzione  
 I piani di manutenzione di Windows 10 in Configuration Manager sono molto simili alle regole di distribuzione automatica degli aggiornamenti software. Creare un piano di manutenzione con i criteri seguenti, che verrà valutato da Configuration Manager:  

- **Classificazione Aggiornamenti**: vengono valutati solo gli aggiornamenti presenti nella classificazione **Aggiornamenti** .  

- **Stato di conformità**: lo stato di conformità definito nel piano di manutenzione viene confrontato con lo stato di conformità per l'aggiornamento. I metadati per l'aggiornamento vengono recuperati quando il punto di connessione del servizio verifica la disponibilità di aggiornamenti.  

- **Differimento**: numero di giorni specificato per l'impostazione **Dopo quanti giorni dalla pubblicazione di un nuovo aggiornamento di Microsoft si vuole eseguire la distribuzione nell'ambiente** nel piano di manutenzione. Se la data corrente è successiva alla data di rilascio più il numero di giorni configurato, Configuration Manager valuta se includere un aggiornamento nella distribuzione.  

  Quando un aggiornamento soddisfa i criteri, il piano di manutenzione aggiunge l'aggiornamento al pacchetto di distribuzione, distribuisce il pacchetto nei punti di distribuzione e distribuisce l'aggiornamento nella raccolta in base alle impostazioni configurate nel piano di manutenzione. È possibile monitorare le distribuzioni nel riquadro piano di monitoraggio del piano del servizio, nel dashboard di manutenzione di Windows 10. Per altre informazioni, vedere [Monitorare gli aggiornamenti software](../../sum/deploy-use/monitor-software-updates.md).  

##  <a name="BKMK_ServicingPlan"></a> Piano di manutenzione di Windows 10  
 Quando si distribuisce il canale semestrale di Windows 10, è possibile creare uno o più piani di manutenzione per definire gli anelli di distribuzione per l'ambiente in uso e monitorarli successivamente nel dashboard di manutenzione di Windows 10. I piani di manutenzione usano solo la classificazione degli aggiornamenti software **Aggiornamenti** e non gli aggiornamenti cumulativi per Windows 10. Per questi aggiornamenti è ancora necessario eseguire la distribuzione usando il flusso di lavoro degli aggiornamenti software. Il piano di manutenzione e gli aggiornamenti software offrono la stessa esperienza all'utente finale, incluse le impostazioni configurate nel piano di manutenzione.  

> [!NOTE]  
>  È possibile usare una sequenza di attività per distribuire un aggiornamento per ogni build di Windows 10, ma questo richiede un maggiore intervento manuale. Sarebbe necessario importare i file di origine aggiornati come un pacchetto di aggiornamento del sistema operativo e quindi creare e distribuire la sequenza di attività per il set di computer appropriato. Tuttavia, una sequenza di attività offre altre opzioni personalizzate, ad esempio le azioni di pre-distribuzione e post-distribuzione.  

 È possibile creare un piano di manutenzione di base dal dashboard di manutenzione di Windows 10. Dopo aver specificato il nome, la raccolta (vengono visualizzate solo le prime 10 raccolte per dimensioni, a partire dalla più piccola), il pacchetto di distribuzione (vengono visualizzati solo i primi 10 pacchetti modificati più di recente) e lo stato di conformità, Configuration Manager crea il piano di manutenzione con valori predefiniti per le altre impostazioni. È anche possibile avviare la procedura guidata Crea piano di manutenzione per configurare tutte le impostazioni. Usare la procedura seguente per creare un piano di manutenzione con la procedura guidata Crea piano di manutenzione.  

> [!NOTE]  
>  È possibile gestire il comportamento relativo alle distribuzioni ad alto rischio. Una distribuzione ad alto rischio viene installata automaticamente e può causare risultati imprevisti. Ad esempio, una sequenza di attività con scopo impostato su **Obbligatorio** e che distribuisce Windows 10 viene considerata una distribuzione ad alto rischio. Per altre informazioni, vedere [Impostazioni per gestire distribuzioni ad alto rischio](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

#### <a name="to-create-a-windows-10-servicing-plan"></a>Per creare un piano di manutenzione di Windows 10  

1. Nella console di Configuration Manager fare clic su **Raccolta software**.  

2. Nell'area di lavoro Raccolta software espandere **Manutenzione di Windows 10**e quindi fare clic su **Piani di manutenzione**.  

3. Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea piano di manutenzione**. Verrà avviata la procedura guidata Crea piano di manutenzione.  

4. Nella pagina **Generale** è possibile configurare le seguenti impostazioni:  

   -   **Nome**: specificare il nome per il piano di manutenzione. Il nome deve essere univoco, descrivere l'obiettivo della regola e contribuire a differenziarla dalle altre presenti nel sito di Configuration Manager.  

   -   **Descrizione**: specificare una descrizione per il piano di manutenzione. La descrizione deve fornire una panoramica del piano di manutenzione e qualsiasi altra informazione rilevante per identificare e differenziare il piano dagli altri nel sito di Configuration Manager. Il campo della descrizione è facoltativo, ha un limite di 256 caratteri e un valore vuoto per impostazione predefinita.  

5. Nella pagina Piano di manutenzione è possibile configurare le impostazioni seguenti:  

   -   **Raccolta di destinazione**: specifica la raccolta di destinazione da usare per il piano di manutenzione. I membri della raccolta ricevono gli aggiornamenti di Windows 10 definiti nel piano di manutenzione.  

       > [!NOTE]  
       >  Quando si esegue una distribuzione ad alto rischio, ad esempio quella di un piano di manutenzione, nella finestra **Seleziona raccolta** vengono visualizzate soltanto le raccolte personalizzate che soddisfano le impostazioni di verifica della distribuzione configurate nelle proprietà del sito.
       >    
       > Le distribuzioni ad alto rischio sono sempre limitate alle raccolte personalizzate (quelle create dall'utente) e alla racconta predefinita **Computer sconosciuti** . Quando si crea una distribuzione ad alto rischio, non è possibile selezionare una raccolta predefinita quale **Tutti i sistemi**. Deselezionare **Nascondi le raccolte con un numero di membri maggiore della configurazione delle dimensioni minime del sito** per visualizzare tutte le raccolte personalizzate che contengono un numero di client inferiore rispetto alla dimensione massima configurata. Per altre informazioni, vedere [Impostazioni per gestire distribuzioni ad alto rischio](../../protect/understand/settings-to-manage-high-risk-deployments.md).  
       >  
       > Le impostazioni di verifica della distribuzione sono basate sull'appartenenza attuale della raccolta. Dopo aver distribuito il piano di manutenzione, l'appartenenza alla raccolta non viene rivalutata per le impostazioni di distribuzione ad alto rischio.  
       >  
       > Ad esempio, si supponga di impostare **Dimensione predefinita** su 100 e **Dimensione massima** su 1000. Quando si crea una distribuzione ad alto rischio, nella finestra **Seleziona raccolta** verranno visualizzate solo le raccolte che contengono meno di 100 client. Se si deseleziona l'impostazione **Nascondi le raccolte con un numero di membri maggiore della configurazione delle dimensioni minime del sito**, nella finestra vengono visualizzate le raccolte che includono meno di 1000 client.  
       >
       > Quando si seleziona una raccolta che include un ruolo del sito, si applicano i criteri seguenti:    
       >   
       >    - Se la raccolta contiene un server di sistema del sito e le impostazioni di verifica della distribuzione sono state configurate in modo da bloccare le raccolte con server di sistema del sito, si verifica un errore e la procedura si arresta.    
       >    - Se la raccolta include un server di sistema del sito e nelle impostazioni di verifica della distribuzione configurate dall'utente viene riportata la presenza di tali server di sistema del sito, se la raccolta supera la dimensione predefinita oppure se la raccolta include un server, nella distribuzione guidata del software verrà visualizzato un messaggio sul rischio elevato dell'operazione. È necessario accettare di creare una distribuzione ad alto rischio, quindi viene creato un messaggio di stato relativo al controllo.  

6. Nella pagina Anello di distribuzione configurare le impostazioni seguenti:  

   -   **Specificare lo stato di conformità di Windows a cui applicare questo piano di manutenzione**: selezionare una delle opzioni riportate di seguito.  

       -   **Canale semestrale (mirato)**: in questo modello di manutenzione, gli aggiornamenti delle funzionalità sono disponibili non appena vengono rilasciati da Microsoft.

       -   **Canale semestrale**: questo canale di manutenzione viene in genere usato per distribuzioni di grandi dimensioni. I client Windows 10 nel canale semestrale ricevono la stessa build di Windows 10 dei dispositivi nel canale mirato, ma in un momento successivo.

       Per altre informazioni sui canali di manutenzione e sulle opzioni più adatte alle proprie esigenze, vedere [Canali di manutenzione](/windows/deployment/update/waas-overview#servicing-channels).

   -   **Dopo quanti giorni dalla pubblicazione di un nuovo aggiornamento di Microsoft si vuole eseguire la distribuzione nell'ambiente**: se la data corrente è successiva alla data di rilascio più il numero di giorni configurato per questa impostazione, Configuration Manager valuta se includere un aggiornamento nella distribuzione.


7. Nella pagina Aggiornamenti configurare i criteri di ricerca per filtrare gli aggiornamenti che vengono aggiunti al piano di manutenzione. Vengono aggiunti alla distribuzione associata solo gli aggiornamenti che soddisfano i criteri specificati. Sono disponibili i filtri proprietà seguenti: <!--3098809, 3113836, 3204570 -->

   - **Architettura** (a partire dalla versione 1810)
   - **Lingua**
   - **Categoria prodotto** (a partire dalla versione 1810)
   - **Richiesto**
      > [!Important]    
      > Nell'ambito dei criteri di ricerca è consigliabile impostare il valore **>=1** nel campo **Richiesto**. L'uso di questo criterio assicura che solo gli aggiornamenti applicabili vengano aggiunti al piano di manutenzione.
   - **Sostituito** (a partire dalla versione 1810)
   - **Titolo**

    Fare clic su **Anteprima** per visualizzare gli aggiornamenti che soddisfano i criteri specificati.  

8. Nella pagina Pianificazione della distribuzione configurare le seguenti impostazioni:  

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
           >  È possibile configurare l'impostazione **Disabilitare sequenza casuale scadenza** del client **Agente computer** per disabilitare il ritardo della sequenza casuale di installazione per gli aggiornamenti richiesti. Per ulteriori informazioni, vedere [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

9. Nella pagina Esperienza utente, è possibile configurare le seguenti impostazioni:  

    -   **Notifiche utente**: specificare se visualizzare la notifica degli aggiornamenti in Software Center nel computer client in base al **Tempo disponibile software** configurato e se visualizzare le notifiche utente nei computer client.  

    -   **Comportamento scadenza**: specificare il comportamento che deve verificarsi quando si raggiunge la data di scadenza per la distribuzione degli aggiornamenti. Specificare se installare gli aggiornamenti nella distribuzione. Specificare anche se eseguire un riavvio del sistema dopo l'installazione dell'aggiornamento, indipendentemente da una finestra di manutenzione configurata. Per altre informazioni sulle finestre di manutenzione, vedere [Come usare le finestre di manutenzione](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportamento riavvio dispositivo**: specificare se evitare un riavvio del sistema in server e workstation dopo l'installazione degli aggiornamenti e se è richiesto un riavvio del sistema per completare l'installazione.  

    -   **Gestione filtri di scrittura per dispositivi con Windows Embedded**: quando si distribuiscono aggiornamenti in dispositivi con Windows Embedded abilitati per i filtri di scrittura, è possibile specificare di installare l'aggiornamento nella sovrapposizione temporanea e confermare le modifiche in seguito oppure alla scadenza dell'installazione o all'interno di una finestra di manutenzione. Quando si confermano le modifiche alla scadenza dell'installazione o all'interno di una finestra di manutenzione, è necessario il riavvio per mantenere le modifiche nel dispositivo.  

        > [!NOTE]  
        >  Quando si distribuisce un aggiornamento in un dispositivo con Windows Embedded, verificare che il dispositivo appartenga a una raccolta con una finestra di manutenzione configurata.  

10. Nella pagina Pacchetto di distribuzione selezionare un pacchetto di distribuzione esistente o configurare le seguenti impostazioni per creare un nuovo pacchetto di distribuzione:  

    1.  **Nome**: specificare il nome del pacchetto di distribuzione. Questo nome deve essere univoco e descrivere il contenuto del pacchetto. Deve essere lungo massimo 50 caratteri.  

    2.  **Descrizione**: specificare una descrizione che fornisca informazioni sul pacchetto di distribuzione. La descrizione deve contenere un massimo di 127 caratteri.  

    3.  **Origine pacchetto**: specifica il percorso dei file di origine dell'aggiornamento software. Digitare un percorso di rete per il percorso di origine, ad esempio **\\\server\nomecondivisione\percorso**oppure fare clic su **Sfoglia** per trovare il percorso di rete. Prima di procedere alla pagina successiva, è necessario creare la cartella condivisa per i file di origine del pacchetto di distribuzione.  

        > [!NOTE]  
        >  Il percorso di origine del pacchetto di distribuzione specificato non può essere usato da un altro pacchetto di distribuzione software.  

        > [!IMPORTANT]  
        >  L'account computer del provider SMS e l'utente che esegue la procedura guidata per scaricare gli aggiornamenti software devono disporre entrambi delle autorizzazioni NTFS di **Scrittura** nel percorso download. È necessario limitare con attenzione l'accesso al percorso download per ridurre il rischio di manomissioni da parte di utenti malintenzionati dei file origine degli aggiornamenti software.  

        > [!IMPORTANT]  
        >  È possibile modificare il percorso di origine del pacchetto nelle proprietà del pacchetto di distribuzione dopo che Configuration Manager ha creato il pacchetto di distribuzione. Ma in tal caso, è prima necessario copiare il contenuto dall'origine del pacchetto originale nel nuovo percorso di origine del pacchetto.  

    4.  **Priorità di invio**: specificare la priorità di invio per il pacchetto di distribuzione. Configuration Manager usa la priorità di invio quando invia il pacchetto di distribuzione ai punti di distribuzione. I pacchetti di distribuzione vengono inviati in ordine di priorità: Alta, Media o Bassa. I pacchetti con priorità identiche vengono inviati nell'ordine in cui sono stati creati. Se non esiste alcun backlog, il pacchetto esegue l'elaborazione immediatamente indipendentemente dalla relativa priorità.  

11. Nella pagina Punti di distribuzione specificare i punti di distribuzione o i gruppi di punti di distribuzione che ospitano i file di aggiornamento. Per altre informazioni, vedere [Configurare un punto di distribuzione](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_configs).

    > [!NOTE]  
    >  Questa pagina è disponibile solo quando si crea un nuovo pacchetto di distribuzione di aggiornamento software.  

12. Nella pagina Percorso download specificare se scaricare i file di aggiornamento da Internet o dalla rete locale. Configurare le seguenti impostazioni:  

    -   **Scarica aggiornamenti software da Internet**: selezionare questa impostazione per scaricare gli aggiornamenti da un percorso specificato in Internet. Questa opzione è attivata per impostazione predefinita.  

    -   **Scarica aggiornamenti software da un percorso sulla rete locale**: selezionare questa impostazione per scaricare gli aggiornamenti da una directory locale o una cartella condivisa. Questa impostazione è utile quando il computer che esegue la procedura guidata non dispone di accesso a Internet. I computer con accesso a Internet possono scaricare preventivamente gli aggiornamenti e archiviarli in un percorso di rete locale accessibile al computer che esegue la procedura guidata.  

13. Nella pagina Selezione lingua selezionare le lingue per cui vengono scaricati gli aggiornamenti selezionati. Gli aggiornamenti vengono scaricati solo se sono disponibili nelle lingue selezionate. Gli aggiornamenti non specifici per la lingua vengono sempre scaricati. Per impostazione predefinita, la procedura guidata consente di selezionare le lingue configurate nelle proprietà del punto di aggiornamento software. Prima di procedere alla pagina successiva, è necessario selezionare almeno una lingua. Quando si selezionano solo lingue non supportate da un aggiornamento, il download dell'aggiornamento non riesce.  

14. Nella pagina Riepilogo rivedere le impostazioni e fare clic su **Avanti** per creare il piano di manutenzione.  

    Dopo aver completato la procedura guidata, verrà eseguito il piano di manutenzione. Gli aggiornamenti che soddisfano i criteri specificati vengono aggiunti a un gruppo di aggiornamenti software, scaricati nella raccolta contenuto nel server del sito e distribuiti ai punti di distribuzione configurati. Il gruppo di aggiornamenti software viene quindi distribuito ai client inclusi nella raccolta di destinazione.  

##  <a name="BKMK_ModifyServicingPlan"></a> Modificare un piano di manutenzione  
Dopo aver creato un piano di manutenzione di base dal dashboard di manutenzione di Windows 10 oppure se è necessario modificare le impostazioni per un piano di manutenzione esistente, è possibile passare alle proprietà del piano di manutenzione.

> [!NOTE]
> È possibile configurare le impostazioni nelle proprietà per il piano di manutenzione che non sono disponibili nella procedura guidata usata per la creazione del piano di manutenzione. La procedura guidata usa valori predefiniti per le impostazioni di download, le impostazioni di distribuzione e gli avvisi.  

Per modificare le proprietà di un piano di manutenzione, seguire la procedura riportata di seguito.  

#### <a name="to-modify-the-properties-of-a-servicing-plan"></a>Per modificare le proprietà di un piano di manutenzione  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro Raccolta software espandere **Manutenzione di Windows 10**, fare clic su **Piani di manutenzione**e quindi selezionare il piano di manutenzione che si vuole modificare.  

3.  Nella scheda **Home** fare clic su **Proprietà** per aprire le proprietà del piano di manutenzione selezionato.

    Le impostazioni seguenti sono disponibili nelle proprietà del piano di manutenzione non configurate nella procedura guidata:

    **Impostazioni distribuzione**: nella scheda Impostazioni distribuzione configurare le impostazioni seguenti:  

    -   **Tipo di distribuzione**: specificare il tipo di distribuzione per la distribuzione degli aggiornamenti software. Selezionare **Richiesto** per creare una distribuzione degli aggiornamenti software obbligatoria in cui gli aggiornamenti software vengano automaticamente installati nei client prima della scadenza di un'installazione configurata. Selezionare **Disponibile** per creare una distribuzione degli aggiornamenti software aggiuntiva che gli utenti possano installare da Software Center.  

        > [!IMPORTANT]  
        >  Dopo aver creato la distribuzione degli aggiornamenti software, non è possibile modificare successivamente il tipo di distribuzione.  

        > [!NOTE]  
        >  Un gruppo di aggiornamenti software distribuito come **Richiesto** viene scaricato in background e rispetta le impostazioni BITS, se configurate.  
        >  
        > I gruppi di aggiornamenti software distribuiti come **Disponibile** vengono invece scaricati in primo piano e ignorano le impostazioni BITS.  

    -   **Usa riattivazione LAN per riattivare i client per le distribuzioni richieste**: specificare se abilitare la riattivazione LAN alla scadenza per inviare pacchetti di riattivazione ai computer che richiedono uno o più aggiornamenti software nella distribuzione. Tutti i computer in modalità sospensione all'ora di scadenza dell'installazione vengono riattivati in modo che si possa avviare l'installazione degli aggiornamenti software. I client in modalità sospensione che non richiedono aggiornamenti software nella distribuzione non vengono avviati. Per impostazione predefinita, questa impostazione non viene abilitata ed è disponibile solo quando **Tipo di distribuzione** è impostato su **Richiesto**.  

        > [!WARNING]  
        >  Prima di usare questa opzione, i computer e le reti devono essere configurati per riattivazione LAN.  

    -   **Livello dettaglio**: specificare il livello di dettaglio per i messaggi di stato segnalati dai computer client.  

    **Impostazioni download**: nella scheda Impostazioni download configurare le impostazioni seguenti:  

    - Specificare se il client scarica e installa gli aggiornamenti software durante una connessione a una rete lenta o quando usa un percorso di fallback per il contenuto.  

    - Specificare se il client dovrà scaricare e installare gli aggiornamenti software da un punto di distribuzione di fallback nel caso in cui il contenuto per tali aggiornamenti non fosse disponibile su un punto di distribuzione preferito.  

    -   **Consenti ai client di condividere il contenuto con altri client nella stessa subnet**: specificare se consentire l'uso di BranchCache per il download del contenuto. Per altre informazioni su BranchCache, vedere [Concetti di base per la gestione dei contenuti](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    -   Specificare se far scaricare ai client gli aggiornamenti software da Microsoft Update nel caso in cui gli aggiornamenti non fossero disponibili nei punti di distribuzione.
        > [!IMPORTANT]
        > Non usare questa impostazione per gli aggiornamenti di manutenzione di Windows 10. Almeno fino alla versione 1610 di Configuration Manager non è possibile scaricare gli aggiornamenti di manutenzione di Windows 10 da Microsoft Update.

    -   Specificare se consentire ai client di eseguire il download dopo una scadenza dell'installazione quando usano connessioni Internet a consumo. I provider Internet talvolta applicano un addebito per il traffico dati in entrata e in uscita quando si usa una connessione Internet a consumo.   

    **Avvisi**: la scheda Avvisi consente di configurare la modalità usata da Configuration Manager e System Center Operations Manager per generare avvisi relativi alla distribuzione. È possibile configurare gli avvisi solo quando **Tipo di distribuzione** è impostato su **Richiesta** nella pagina Impostazioni distribuzione.  

    > [!NOTE]  
    >  È possibile riesaminare gli avvisi recenti sugli aggiornamenti software dal nodo **Aggiornamenti software** nell'area di lavoro **Raccolta software** .  

**Per altre informazioni:** <br/>
[Nozioni di base su Configuration Manager come servizio e Windows distribuito come servizio](/sccm/core/understand/configuration-manager-and-windows-as-service.md)

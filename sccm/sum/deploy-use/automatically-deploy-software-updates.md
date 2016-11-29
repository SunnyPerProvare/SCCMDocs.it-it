---
title: Distribuire gli aggiornamenti software automaticamente | Configuration Manager
description: Distribuire gli aggiornamenti software automaticamente aggiungendo nuovi aggiornamenti a un gruppo di aggiornamento associato a una distribuzione attiva oppure usando ADR.
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 133f29aa3f515054b23ba70f1a1dfd3eedaa56c8

---

#  <a name="a-namebkmkautodeploya-automatically-deploy-software-updates"></a><a name="BKMK_AutoDeploy"></a> Distribuire automaticamente gli aggiornamenti software  

*Si applica a: System Center Configuration Manager (Current Branch)*

 È possibile distribuire gli aggiornamenti software automaticamente aggiungendo nuovi aggiornamenti software a un gruppo di aggiornamento associato con una distribuzione attiva oppure è possibile usare le regole di distribuzione automatica (ADR). Solitamente si usano le regole di distribuzione automatica per distribuire mensilmente gli aggiornamenti software (comunemente noti come aggiornamenti Patch Tuesday) e per la gestione degli aggiornamenti delle definizioni. Per altre informazioni su come determinare qual è il metodo di distribuzione giusto da usare, vedere [Deploy software updates](deploy-software-updates.md) (Distribuire gli aggiornamenti software)

##  <a name="a-namebkmkaddupdatestoexistinggroupa-add-software-updates-to-a-deployed-update-group"></a><a name="BKMK_AddUpdatesToExistingGroup"></a> Aggiungere gli aggiornamenti software a un gruppo di aggiornamento distribuito  
Dopo aver creato e distribuito un gruppo di aggiornamento software, è possibile aggiungere aggiornamenti software a tale gruppo che saranno distribuiti automaticamente.  

> [!IMPORTANT]  
>  Quando si aggiungono aggiornamenti software a un gruppo di aggiornamento software esistente già distribuito, potrebbero essere richiesti alcuni minuti per il completamento di tale operazione.  

Usare la procedura seguente per aggiungere aggiornamenti software a un gruppo di aggiornamento esistente.  

#### <a name="to-add-software-updates-to-an-existing-software-update-group"></a>Per aggiungere gli aggiornamenti software a un gruppo di aggiornamento software esistente  

1.  Nella console di Configuration Manager passare a **Raccolta software** > **Panoramica** > **Aggiornamenti software**.  

2.  Selezionare gli aggiornamenti software che devono essere aggiunti al nuovo gruppo di aggiornamento software.  

3.  Nella scheda **Home** del gruppo **Aggiorna** , fare clic su **Modifica appartenenza**.  

4.  Selezionare il gruppo di aggiornamento software a cui si desidera aggiungere gli aggiornamenti software come membri.  

5.  Fare clic sul nodo **Gruppi di aggiornamenti software** per visualizzare il gruppo di aggiornamento software.  

6.  Fare clic sul gruppo di aggiornamento software, quindi nella scheda **Home** del gruppo **Aggiorna** , fare clic su **Mostra membri** per visualizzare un elenco degli aggiornamenti software inclusi nel gruppo.  

##  <a name="a-namebkmkcreateautomaticdeploymentrulea-create-an-automatic-deployment-rule-adr"></a><a name="BKMK_CreateAutomaticDeploymentRule"></a> Creare una regola di distribuzione automatica (ADR)  
È possibile approvare e distribuire automaticamente gli aggiornamenti software usando un'ADR. È possibile fare in modo che la regola aggiunga gli aggiornamenti software a un nuovo gruppo di aggiornamenti software ogni volta che la regola viene eseguita oppure che aggiunga gli aggiornamenti software a un gruppo esistente. Quando una regola viene eseguita e aggiunge gli aggiornamenti software a un gruppo esistente, la regola rimuove tutti gli aggiornamenti software dal gruppo e quindi aggiunge gli aggiornamenti software che soddisfano i criteri definiti al gruppo. Per eseguire un'ADR per trovare i nuovi aggiornamenti software rilasciati ogni giorno e distribuirli nei client, ad esempio, è necessario scegliere l'opzione per creare un nuovo gruppo di aggiornamenti software invece che per aggiungere gli aggiornamenti software a un gruppo esistente.  

> [!WARNING]  
>  Prima di creare un'ADR per la prima volta, verificare che la sincronizzazione degli aggiornamenti software nel sito sia stata completata. Questo è particolarmente importante quando Configuration Manager viene eseguito non in lingua inglese, perché le classificazioni di aggiornamento software vengono visualizzate in lingua inglese prima della sincronizzazione iniziale e, solo al termine di tale operazione, sono visualizzate nella lingua localizzata. Le regole create prima della sincronizzazione degli aggiornamenti software potrebbero non funzionare correttamente dopo la sincronizzazione perché la stringa di testo potrebbe non corrispondere.  

 Usare la procedura seguente per creare un'ADR.  

#### <a name="to-create-an-adr"></a>Per creare un'ADR  

1.  Nella console di Configuration Manager passare a **Raccolta software** **Panoramica** > **Aggiornamenti software** > **Regole di distribuzione automatica**.  

2.  Nella scheda **Home** del gruppo **Crea** fare clic su **Crea regola di distribuzione automatica**. Si aprirà la Creazione guidata delle regole di distribuzione automatica.  

3.  Nella pagina **Generale** è possibile configurare le seguenti impostazioni:  

    -   **Nome:**specificare il nome per l'ADR. Il nome deve essere univoco, descrivere l'obiettivo della regola e contribuire a differenziarla dalle altre presenti nel sito di Configuration Manager.  

    -   **Descrizione:**specificare una descrizione per l'ADR. La descrizione deve fornire una panoramica della regola di distribuzione, nonché tutte le altre informazioni rilevanti per identificare e differenziare la regola dalle altre nel sito di Configuration Manager. Il campo della descrizione è facoltativo, ha un limite di 256 caratteri e un valore vuoto per impostazione predefinita.  

    -   **Seleziona modello di distribuzione**: specificare se applicare un modello di distribuzione precedentemente salvato. È possibile configurare un modello di distribuzione in modo da contenere più proprietà di distribuzione degli aggiornamenti software comuni che possono essere usati durante la creazione delle ADR. Questi modelli consentono di garantire la coerenza tra le distribuzioni simili e risparmiare tempo.  

         È possibile scegliere uno dei modelli di distribuzione degli aggiornamenti software predefiniti da Creazione guidata delle regole di distribuzione automatica. Il modello **Aggiornamenti della definizione** offre impostazioni comuni da usare quando si distribuiscono aggiornamenti software della definizione. Il modello **Patch martedì** offre impostazioni comuni da usare quando si distribuiscono aggiornamenti software su base ciclica mensile.  

    -   **Raccolta**: specifica la raccolta di destinazione da usare per la distribuzione. I membri della raccolta ricevono gli aggiornamenti software che vengono definiti nella distribuzione.  

    -   Decidere se aggiungere gli aggiornamenti software a un gruppo di aggiornamento software nuovo o esistente. Nella maggior parte dei casi, si sceglierà probabilmente di creare un nuovo gruppo di aggiornamenti software quando si esegue l'ADR. Tuttavia, è possibile usare un gruppo esistente se la regola viene eseguita in una pianificazione più aggressiva. Ad esempio, se la regola sarà eseguita giornalmente per gli aggiornamenti delle definizioni, allora sarà possibile aggiungere gli aggiornamenti software a un gruppo di aggiornamento software esistente.  

    -   **Attiva la distribuzione dopo l'esecuzione di questa regola**: specificare se abilitare la distribuzione degli aggiornamenti software dopo l'esecuzione dell'ADR. Per quanto riguarda questa specifica, considerare quanto segue:  

        -   Quando si abilita la distribuzione, gli aggiornamenti software che soddisfano i criteri definiti nella regola vengono aggiunti a un gruppo di aggiornamento software, il contenuto di aggiornamento software viene scaricato secondo necessità e copiato nei punti di distribuzione specificati e gli aggiornamenti software vengono distribuiti ai client nella raccolta di destinazione.  

        -   Quando non si abilita la distribuzione, gli aggiornamenti software che soddisfano i criteri definiti nella regola vengono aggiunti a un gruppo di aggiornamento software, il criterio di distribuzione degli aggiornamenti software viene configurato ma gli aggiornamenti non vengono scaricati né distribuiti ai client. Questo scenario garantisce il tempo necessario per predisporsi alla distribuzione degli aggiornamenti software, verificare che gli aggiornamenti software che soddisfano i criteri siano adeguati e, infine, per abilitare la distribuzione in una fase successiva.  

4.  Nella pagina Impostazioni distribuzione, configurare le seguenti impostazioni:  

    -   **Usa riattivazione LAN per riattivare i client per le distribuzioni richieste**: specifica se abilitare la riattivazione LAN alla scadenza per inviare pacchetti di riattivazione ai computer che richiedono uno o più aggiornamenti software nella distribuzione. Tutti i computer in modalità sospensione all'ora di scadenza dell'installazione verranno riattivati in modo che si possa avviare l'installazione degli aggiornamenti software. I client in modalità sospensione che non richiedono aggiornamenti software nella distribuzione non vengono avviati. Per impostazione predefinita, questa impostazione non è attivata.  

        > [!WARNING]  
        >  Prima di poter usare questa opzione, è necessario configurare i computer e le reti per la Riattivazione LAN.  

    -   **Livello dettaglio**: specificare il livello di dettaglio per i messaggi di stato segnalati dai computer client.  

        > [!IMPORTANT]  
        >  Quando si distribuiscono gli aggiornamenti delle definizioni, impostare il livello di dettaglio su **Solo errori** affinché il client segnali un messaggio di stato solo in caso di mancato recapito di un aggiornamento delle definizioni al client. In caso contrario, il client segnalerà un numero elevato di messaggi di stato che potrebbe influire sulle prestazioni del server del sito.  

    -   **Impostazione condizioni di licenza**: specificare se si desidera distribuire automaticamente gli aggiornamenti software con le condizioni di licenza associate. Alcuni aggiornamenti software includono le condizioni di licenza, ad esempio un Service Pack. Quando si distribuiscono automaticamente gli aggiornamenti software, non vengono visualizzate le condizioni di licenza e non è disponibile un'opzione per accettare tali condizioni. È possibile scegliere di distribuire automaticamente tutti gli aggiornamenti software indipendentemente dalle condizioni di licenza associate o di distribuire solo gli aggiornamenti a cui non sono associate tali condizioni.  

        > [!WARNING]  
        >  Per riesaminare le condizioni di licenza per un aggiornamento software, è possibile selezionare l'aggiornamento nel nodo **Tutti gli aggiornamenti software** dell'area di lavoro **Raccolta software** , quindi nella scheda **Home** del gruppo **Aggiorna** fare clic su **Riesamina licenza**.  
        >   
        >  Per individuare gli aggiornamenti software con le condizioni di licenza associate, è possibile aggiungere la colonna **Condizioni di licenza** al riquadro dei risultati nel nodo **Tutti gli aggiornamenti software** , quindi fare clic sull'intestazione per ordinare la colonna per aggiornamenti software con condizioni di licenza.  

5.  Nella pagina Aggiornamenti software configurare i criteri per gli aggiornamenti software recuperati e aggiunti al gruppo di aggiornamenti software dall'ADR.  

    > [!IMPORTANT]  
    >  Il limite dell'ADR è di 1000 aggiornamenti software. Per garantire che i criteri specificati in questa pagina consentano di recuperare meno di 1.000 aggiornamenti software, si consiglia di impostare gli stessi criteri sul nodo **Tutti gli aggiornamenti software** nell'area di lavoro **Raccolta software** .  

6.  Nella pagina Pianificazione valutazione specificare se abilitare l'esecuzione dell'ADR in una pianificazione. Quando attivata, fare clic su **Personalizza** per impostare la pianificazione ricorrente.  

    > [!IMPORTANT]  
    >  Viene visualizzata la pianificazione di sincronizzazione del punto di aggiornamento software per determinare la frequenza della pianificazione per la valutazione. Non impostare mai la pianificazione per la valutazione con una frequenza superiore alla pianificazione della sincronizzazione degli aggiornamenti software. La configurazione dell'ora di avvio per la pianificazione si basa sull'ora locale del computer su cui è in esecuzione la console di Configuration Manager.  

    > [!NOTE]  
    >  Per eseguire manualmente l'ADR, selezionarla e fare clic su **Esegui** nella scheda **Home** del gruppo **Regola di distribuzione automatica** . Prima di eseguire l'ADR manualmente, verificare che la sincronizzazione degli aggiornamenti software sia stata eseguita dall'ultima esecuzione della regola.  

    > [!IMPORTANT]  
    >  La valutazione dell'ADR può essere eseguita per un massimo di tre volte al giorno.  

7.  Nella pagina Pianificazione della distribuzione configurare le seguenti impostazioni:  

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
        >  L'orario effettivo di scadenza dell'installazione corrisponde all'ora di scadenza visualizzata più una quantità di tempo casuale di massimo 2 ore. Ciò consente di ridurre il potenziale impatto di un'installazione simultanea degli aggiornamenti software nella distribuzione da parte di tutti i computer client nella raccolta di destinazione.  
        >   
        >  È possibile configurare l'impostazione **Disabilitare sequenza casuale scadenza** del client **Agente computer** per disabilitare il ritardo della sequenza casuale di installazione per gli aggiornamenti software richiesti. Per altre informazioni, vedere [Computer Agent](../../core/clients/deploy/about-client-settings.md#a-namebkmkcomputeragentdevicesettingsa-computer-agent).  

8. Nella pagina Esperienza utente, è possibile configurare le seguenti impostazioni:  

    -   **Notifiche utente**: specificare se visualizzare la notifica degli aggiornamenti software in Software Center sul computer client in base al **Tempo disponibile software** configurato e se visualizzare le notifiche utente sui computer client.  

    -   **Comportamento scadenza**: specificare il comportamento che deve verificarsi quando si raggiunge la data di scadenza per la distribuzione degli aggiornamenti software. Specificare se installare gli aggiornamenti software nella distribuzione. Inoltre, specificare se eseguire un riavvio del sistema dopo l'installazione dell'aggiornamento software indipendentemente da una finestra di manutenzione configurata. Per altre informazioni sulle finestre di manutenzione, vedere [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md) (Come usare le finestre di manutenzione in Configuration Manager).  

    -   **Comportamento riavvio dispositivo**: specificare se evitare un riavvio del sistema su server e workstation dopo l'installazione degli aggiornamenti software e se è richiesto un riavvio del sistema per completare l'installazione.  

        > [!IMPORTANT]  
        >  L'inibizione dei riavvii del sistema può essere utile negli ambienti server o nei casi in cui non si desidera che i computer sui quali si stanno installando gli aggiornamenti software vengano riavviati per impostazione predefinita. Tuttavia, tale soluzione potrebbe lasciare i computer in uno stato non protetto, mentre un riavvio forzato assicura il completamento immediato dell'installazione degli aggiornamenti software.  

    -   **Gestione filtri di scrittura per dispositivi con Windows Embedded**: quando si distribuiscono aggiornamenti software in dispositivi con Windows Embedded abilitati per i filtri di scrittura, è possibile specificare di installare l'aggiornamento software nella sovrapposizione temporanea e di confermare le modifiche in seguito oppure alla scadenza dell'installazione o all'interno di una finestra di manutenzione. Quando si confermano le modifiche alla scadenza dell'installazione o all'interno di una finestra di manutenzione, è necessario il riavvio per mantenere le modifiche nel dispositivo.  

        > [!NOTE]  
        >  Quando si distribuisce un aggiornamento software in un dispositivo con Windows Embedded, verificare che il dispositivo appartenga a una raccolta che dispone di una finestra di manutenzione configurata.  

9. Nella pagina Avvisi, configurare la modalità in cui Configuration Manager e System Center Operations Manager genereranno gli avvisi relativi alla distribuzione.  

    > [!WARNING]  
    >  È possibile riesaminare gli avvisi recenti sugli aggiornamenti software dal nodo **Aggiornamenti software** nell'area di lavoro **Raccolta software** .  

10. Nella pagina Impostazioni download, configurare le seguenti impostazioni:  

    -   Specificare se il client scaricherà e installerà gli aggiornamenti software durante una connessione a una rete lenta o mentre usa un percorso di fallback per il contenuto.  

    -   Specificare se il client dovrà scaricare e installare gli aggiornamenti software da un punto di distribuzione di fallback nel caso in cui il contenuto per tali aggiornamenti non fosse disponibile su un punto di distribuzione preferito.  

    -   **Consenti ai client di condividere il contenuto con altri client nella stessa subnet**: specificare se consentire l'uso di BranchCache per il download del contenuto. Per altre informazioni su BranchCache, vedere [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    -   Specificare se far scaricare gli aggiornamenti software da Microsoft Update ai client connessi alla intranet nel caso in cui gli aggiornamenti non fossero disponibili nei punti di distribuzione.  

    -   Specificare se consentire ai client di eseguire il download dopo una scadenza dell'installazione quando usano connessioni Internet a consumo. I provider Internet talvolta applicano un addebito per il traffico dati in entrata e in uscita quando si usa una connessione Internet a consumo.  

    > [!NOTE]  
    >  I client richiedono il percorso del contenuto da un punto di gestione per gli aggiornamenti software in una distribuzione. Il comportamento di download dipende dalla configurazione del punto di distribuzione, del pacchetto di distribuzione e delle impostazioni in questa pagina. Per altre informazioni, vedere [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

11. Nella pagina Pacchetto di distribuzione selezionare un pacchetto di distribuzione esistente o configurare le seguenti impostazioni per creare un nuovo pacchetto di distribuzione:  

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

12. Nella pagina Punti di distribuzione, specificare i punti di distribuzione o i gruppi dei punti di distribuzione che ospiteranno i file di aggiornamento software. Per altre informazioni sui punti di distribuzione, vedere [Configurazioni dei punti di distribuzione](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

    > [!NOTE]  
    >  Questa pagina è disponibile solo quando si crea un nuovo pacchetto di distribuzione di aggiornamento software.  

13. Nella pagina Percorso download, specificare se scaricare i file di aggiornamento software da Internet o dalla rete locale. Configurare le seguenti impostazioni:  

    -   **Scarica aggiornamenti software da Internet**: selezionare questa impostazione per scaricare gli aggiornamenti software da un percorso specificato su Internet. Questa opzione è attivata per impostazione predefinita.  

    -   **Scarica aggiornamenti software da un percorso sulla rete locale**: selezionare questa impostazione per scaricare gli aggiornamenti software da una directory locale o una cartella condivisa. Questa impostazione è utile quando il computer che esegue la procedura guidata non dispone di accesso a Internet. I computer che dispongono dell'accesso a Internet possono scaricare preventivamente gli aggiornamenti software e archiviarli in un percorso della rete locale accessibile al computer che esegue la procedura guidata.  

14. Nella pagina Selezione lingua selezionare le lingue per cui vengono scaricati gli aggiornamenti software selezionati. Gli aggiornamenti software vengono scaricati solo se sono disponibili nelle lingue selezionate. Gli aggiornamenti software non specifici per la lingua vengono sempre scaricati. Per impostazione predefinita, la procedura guidata consente di selezionare le lingue configurate nelle proprietà del punto di aggiornamento software. Prima di procedere alla pagina successiva, è necessario selezionare almeno una lingua. Quando si selezionano solo lingue non supportate da un aggiornamento software, il download dell'aggiornamento software avrà esito negativo.  

15. Nella pagina Riepilogo, esaminare le impostazioni. Per salvare le impostazioni in un modello di distribuzione, fare clic su **Salva come modello**, immettere un nome e selezionare le impostazioni da includere nel modello, quindi fare clic su **Salva**. Per modificare un'impostazione configurata, fare clic sulla pagina della procedura guidata associata e modificare l'impostazione.  

    > [!WARNING]  
    >  Il nome modello può essere composto da caratteri ASCII alfanumerici così come da **\\** (barra rovesciata) o **‘** (virgoletta singola).  

16. Fare clic su **Avanti** per creare l'ADR.  

 Dopo aver completato la procedura guidata, verrà eseguita l'ADR. Questa aggiunge gli aggiornamenti software che soddisfano i criteri specificati a un gruppo di aggiornamento software, scarica gli aggiornamenti software nella raccolta contenuto nel server del sito, distribuisce gli aggiornamenti software ai punti di distribuzione configurati e quindi distribuisce il gruppo aggiornamenti software ai client inclusi nella raccolta di destinazione.  

##  <a name="a-namebkmkadddeploymenttoadra-add-a-new-deployment-to-an-existing-adr"></a><a name="BKMK_AddDeploymentToADR"></a> Aggiungere una nuova distribuzione a un'ADR esistente  
 Dopo aver creato una regola di distribuzione automatica, è possibile aggiungere altre distribuzioni alla regola. Ciò consente di gestire la complessità della distribuzione di aggiornamenti diversi a raccolte differenti. Ogni nuova distribuzione dispone dell'intera gamma di funzionalità e dell’esperienza di monitoraggio della distribuzione.  

#### <a name="to-add-a-new-deployment-to-an-existing-adr"></a>Per aggiungere una nuova distribuzione a un'ADR esistente  

1.  Nella console di Configuration Manager passare a **Raccolta software** > **Panoramica** > **Aggiornamenti software** > **Regole di distribuzione automatica** e selezionare la regola desiderata.  

2.  Nella scheda **Home** del gruppo **Regola di distribuzione automatica** fare clic su **Aggiungi distribuzione**. Si aprirà la procedura guidata Aggiungi distribuzione.  

3.  Nella pagina **Raccolta** configurare le impostazioni seguenti:  

    -   **Raccolta**: specifica la raccolta di destinazione da usare per la distribuzione. I membri della raccolta ricevono gli aggiornamenti software che vengono definiti nella distribuzione.  

    -   **Attiva la distribuzione dopo l'esecuzione di questa regola**: specificare se abilitare la distribuzione degli aggiornamenti software dopo l'esecuzione dell'ADR. Per quanto riguarda questa specifica, considerare quanto segue:  

        -   Quando si abilita la distribuzione, gli aggiornamenti software che soddisfano i criteri definiti nella regola vengono aggiunti a un gruppo di aggiornamento software, il contenuto di aggiornamento software viene scaricato secondo necessità e copiato nei punti di distribuzione specificati e gli aggiornamenti software vengono distribuiti ai client nella raccolta di destinazione.  

        -   Quando non si abilita la distribuzione, gli aggiornamenti software che soddisfano i criteri definiti nella regola vengono aggiunti a un gruppo di aggiornamento software, il criterio di distribuzione degli aggiornamenti software viene configurato ma gli aggiornamenti non vengono scaricati né distribuiti ai client. Questo scenario garantisce il tempo necessario per predisporsi alla distribuzione degli aggiornamenti software, verificare che gli aggiornamenti software che soddisfano i criteri siano adeguati e, infine, per abilitare la distribuzione in una fase successiva.  

4.  Nella pagina Impostazioni distribuzione, configurare le seguenti impostazioni:  

    -   **Usa riattivazione LAN per riattivare i client per le distribuzioni richieste**: specifica se abilitare la riattivazione LAN alla scadenza per inviare pacchetti di riattivazione ai computer che richiedono uno o più aggiornamenti software nella distribuzione. Tutti i computer in modalità sospensione all'ora di scadenza dell'installazione verranno riattivati in modo che si possa avviare l'installazione degli aggiornamenti software. I client in modalità sospensione che non richiedono aggiornamenti software nella distribuzione non vengono avviati. Per impostazione predefinita, questa impostazione non è attivata.  

        > [!WARNING]  
        >  Prima di poter usare questa opzione, è necessario configurare i computer e le reti per la Riattivazione LAN.  

    -   **Livello dettaglio**: specificare il livello di dettaglio per i messaggi di stato segnalati dai computer client.  

        > [!IMPORTANT]  
        >  Quando si distribuiscono gli aggiornamenti delle definizioni, impostare il livello di dettaglio su **Solo errori** affinché il client segnali un messaggio di stato solo in caso di mancato recapito di un aggiornamento delle definizioni al client. In caso contrario, il client segnalerà un numero elevato di messaggi di stato che potrebbe influire sulle prestazioni del server del sito.  

5.  Nella pagina Pianificazione della distribuzione configurare le seguenti impostazioni:  

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
        >  L'orario effettivo di scadenza dell'installazione corrisponde all'ora di scadenza visualizzata più una quantità di tempo casuale di massimo 2 ore. Ciò consente di ridurre il potenziale impatto di un'installazione simultanea degli aggiornamenti software nella distribuzione da parte di tutti i computer client nella raccolta di destinazione.  
        >   
        >  È possibile configurare l'impostazione **Disabilitare sequenza casuale scadenza** del client **Agente computer** per disabilitare il ritardo della sequenza casuale di installazione per gli aggiornamenti software richiesti. Per altre informazioni, vedere [Computer Agent](../../core/clients/deploy/about-client-settings.md#a-namebkmkcomputeragentdevicesettingsa-computer-agent).  

6.  Nella pagina Esperienza utente, è possibile configurare le seguenti impostazioni:  

    -   **Notifiche utente**: specificare se visualizzare la notifica degli aggiornamenti software in Software Center sul computer client in base al **Tempo disponibile software** configurato e se visualizzare le notifiche utente sui computer client.  

    -   **Comportamento scadenza**: specificare il comportamento che deve verificarsi quando si raggiunge la data di scadenza per la distribuzione degli aggiornamenti software. Specificare se installare gli aggiornamenti software nella distribuzione. Inoltre, specificare se eseguire un riavvio del sistema dopo l'installazione dell'aggiornamento software indipendentemente da una finestra di manutenzione configurata. Per altre informazioni sulle finestre di manutenzione, vedere [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md) (Come usare le finestre di manutenzione in Configuration Manager).  

    -   **Comportamento riavvio dispositivo**: specificare se evitare un riavvio del sistema su server e workstation dopo l'installazione degli aggiornamenti software e se è richiesto un riavvio del sistema per completare l'installazione.  

        > [!IMPORTANT]  
        >  L'inibizione dei riavvii del sistema può essere utile negli ambienti server o nei casi in cui non si desidera che i computer sui quali si stanno installando gli aggiornamenti software vengano riavviati per impostazione predefinita. Tuttavia, tale soluzione potrebbe lasciare i computer in uno stato non protetto, mentre un riavvio forzato assicura il completamento immediato dell'installazione degli aggiornamenti software.  

    -   **Gestione filtri di scrittura per dispositivi con Windows Embedded**: quando si distribuiscono aggiornamenti software in dispositivi con Windows Embedded abilitati per i filtri di scrittura, è possibile specificare di installare l'aggiornamento software nella sovrapposizione temporanea e di confermare le modifiche in seguito oppure alla scadenza dell'installazione o all'interno di una finestra di manutenzione. Quando si confermano le modifiche alla scadenza dell'installazione o all'interno di una finestra di manutenzione, è necessario il riavvio per mantenere le modifiche nel dispositivo.  

        > [!NOTE]  
        >  Quando si distribuisce un aggiornamento software in un dispositivo con Windows Embedded, verificare che il dispositivo appartenga a una raccolta che dispone di una finestra di manutenzione configurata.  

7.  Nella pagina Avvisi, configurare la modalità in cui Configuration Manager e System Center Operations Manager genereranno gli avvisi relativi alla distribuzione.  

    > [!WARNING]  
    >  È possibile riesaminare gli avvisi recenti sugli aggiornamenti software dal nodo **Aggiornamenti software** nell'area di lavoro **Raccolta software** .  

8. Nella pagina Impostazioni download, configurare le seguenti impostazioni:  

    -   Specificare se il client scaricherà e installerà gli aggiornamenti software durante una connessione a una rete lenta o mentre usa un percorso di fallback per il contenuto.  

    -   Specificare se il client dovrà scaricare e installare gli aggiornamenti software da un punto di distribuzione di fallback nel caso in cui il contenuto per tali aggiornamenti non fosse disponibile su un punto di distribuzione preferito.  

    -   **Consenti ai client di condividere il contenuto con altri client nella stessa subnet**: specificare se consentire l'uso di BranchCache per il download del contenuto. Per altre informazioni su BranchCache, vedere [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    -   Specificare se far scaricare gli aggiornamenti software da Microsoft Update ai client connessi alla intranet nel caso in cui gli aggiornamenti non fossero disponibili nei punti di distribuzione.  

    -   Specificare se consentire ai client di eseguire il download dopo una scadenza dell'installazione quando usano connessioni Internet a consumo. I provider Internet talvolta applicano un addebito per il traffico dati in entrata e in uscita quando si usa una connessione Internet a consumo.  

    > [!NOTE]  
    >  I client richiedono il percorso del contenuto da un punto di gestione per gli aggiornamenti software in una distribuzione. Il comportamento di download dipende dalla configurazione del punto di distribuzione, del pacchetto di distribuzione e delle impostazioni in questa pagina. Per altre informazioni, vedere [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

Per altre informazioni sul processo di distribuzione, vedere [Software update deployment process](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).

## <a name="next-steps"></a>Passaggi successivi
[Monitorare gli aggiornamenti software](monitor-software-updates.md)



<!--HONumber=Nov16_HO1-->


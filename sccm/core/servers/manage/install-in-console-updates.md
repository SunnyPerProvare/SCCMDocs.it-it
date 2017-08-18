---
title: Aggiornamenti nella console | Microsoft Docs
description: System Center Configuration Manager si sincronizza con il cloud Microsoft per ottenere aggiornamenti installabili all'interno della console.
ms.custom: na
ms.date: 06/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
caps.latest.revision: 36
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: 2bbc8935bee306ed0bc312cc43b8f5374a8df7ff
ms.contentlocale: it-it
ms.lasthandoff: 07/29/2017

---
# <a name="install-in-console-updates-for-system-center-configuration-manager"></a>Installare gli aggiornamenti nella console per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager si sincronizza con il servizio cloud Microsoft per ottenere aggiornamenti. È quindi possibile installare questi aggiornamenti dalla console di Configuration Manager.

## <a name="get-available-updates"></a>Ottenere gli aggiornamenti disponibili
Solo gli aggiornamenti che si applicano all'infrastruttura e alla versione vengono scaricati e resi disponibili nella gerarchia. Questa sincronizzazione può essere automatica o manuale a seconda di come si configura il punto di connessione del servizio per la gerarchia:

-   In **modalità online**il punto di connessione si connette automaticamente al servizio cloud Microsoft e scarica gli aggiornamenti applicabili.  

     Per impostazione predefinita, Configuration Manager verifica la disponibilità di nuovi aggiornamenti ogni 24 ore. È anche possibile verificare immediatamente la disponibilità di aggiornamenti scegliendo **Verifica la disponibilità di aggiornamenti** nel nodo **Amministrazione** > **Aggiornamenti e manutenzione** della console di Configuration Manager. Nelle versioni precedenti la 1702, questo nodo si trova in **Amministrazione** > **Servizi cloud**.

-   In **modalità offline** il punto di connessione del servizio non si connette al servizio cloud Microsoft. Usare manualmente lo [strumento di connessione del servizio per System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md) per scaricare e importare gli aggiornamenti disponibili.  

> [!NOTE]  
>   È possibile importare nella console le correzioni fuori programma. A tal fine, usare lo [strumento di registrazione dell'aggiornamento](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes). Le correzioni fuori programma completano gli aggiornamenti ottenuti quando si esegue la sincronizzazione con il servizio Microsoft Cloud.


Dopo aver sincronizzato gli aggiornamenti è possibile visualizzarli nella console di Configuration Manager passando al nodo **Amministrazione** > **Aggiornamenti e manutenzione**:  

-   Gli aggiornamenti non installati vengono visualizzati con l'indicazione **Disponibile**.

-   Gli aggiornamenti installati vengono visualizzati con l'indicazione **Installato**.  Viene visualizzato solo l'aggiornamento installato più di recente. È possibile scegliere il pulsante **Cronologia** della barra multifunzione per visualizzare gli aggiornamenti installati in precedenza.



Prima di configurare il punto di connessione del servizio, esaminare e pianificare i relativi usi aggiuntivi. Gli usi riportati di seguito possono influire sulla modalità di configurazione di questo ruolo del sistema del sito:  

-   Il punto di connessione del servizio viene usato per caricare le informazioni di utilizzo relative al sito. Queste informazioni consentono al servizio cloud di Microsoft di identificare gli aggiornamenti disponibili per la versione corrente dell'infrastruttura. Per altre informazioni, vedere [Dati di diagnostica e di utilizzo per System Center Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

-   Il punto di connessione del servizio viene usato per gestire i dispositivi con Microsoft Intune e con la gestione dei dispositivi mobili locale di Configuration Manager. Per altre informazioni, vedere [Gestione di dispositivi mobili ibridi con System Center Configuration Manager e Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

Per comprendere meglio ciò che accade quando vengono scaricati gli aggiornamenti, vedere:  

-   [Diagramma di flusso: scaricare gli aggiornamenti per System Center Configuration Manager](../../../core/servers/manage/download-updates-flowchart.md)

-   [Flowchart - Update replication for System Center Configuration Manager](../../../core/servers/manage/update-replication-flowchart.md) (Diagramma di flusso: replica dell'aggiornamento per System Center Configuration Manager)  

## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Assegnare le autorizzazioni per la visualizzazione e la gestione di aggiornamenti e funzionalità
Perché un utente possa visualizzare gli aggiornamenti nella console è necessario che disponga di un ruolo di protezione di amministrazione basato su ruoli che includa una classe di protezione denominata **Pacchetti di aggiornamento**. Questa classe consente l'accesso per visualizzare e gestire gli aggiornamenti nella console di Configuration Manager.    

**Informazioni sulla classe Pacchetti di aggiornamento:**  
Per impostazione predefinita, **Pacchetti di aggiornamento** (SMS_CM_Updatepackages) fa parte dei seguenti ruoli di sicurezza predefiniti con le autorizzazioni elencate:
 -  **Amministratore completo** con autorizzazioni **Modifica** e **Lettura** :
    -   Un utente con questo ruolo di sicurezza e l'accesso all'ambito di protezione **Tutto** può visualizzare e installare gli aggiornamenti. L'utente può anche abilitare le funzionalità durante l'installazione e abilitare singole funzionalità dopo aver installato l'aggiornamento.
    - Un utente con questo ruolo di sicurezza e l'accesso all'ambito di protezione **Predefinito** può visualizzare e installare gli aggiornamenti. L'utente può anche abilitare le funzionalità durante l'installazione e visualizzare le funzionalità dopo che l'aggiornamento è stato installato. Ma l'utente non può abilitare le funzionalità dopo che l'aggiornamento è stato installato.

- **Analista di sola lettura** con autorizzazioni **Lettura** :
  -  Un utente con questo ruolo di sicurezza e l'accesso all'ambito **Predefinito** può visualizzare gli aggiornamenti ma non installarli. Questo utente può anche visualizzare le funzionalità dopo l'installazione di un aggiornamento, ma non può abilitarle.

**Autorizzazioni richieste per gli aggiornamenti e la manutenzione:**   
  - Usare un account cui è assegnato un ruolo di sicurezza che include la classe **Pacchetti di aggiornamento** con entrambe le autorizzazioni **Modifica** e **Lettura** .
  - È necessario che all'account sia assegnato l'ambito **Predefinito** .

**Autorizzazioni per la sola visualizzazione degli aggiornamenti**:
  - Usare un account cui è assegnato un ruolo di sicurezza che include la classe **Pacchetti di aggiornamento** con solo l'autorizzazione **Lettura** .
  - È necessario che all'account sia assegnato l'ambito **Predefinito** .

**Autorizzazioni richieste per abilitare le funzionalità dopo l'installazione degli aggiornamenti:**
  -  Usare un account cui è assegnato un ruolo di sicurezza che include la classe **Pacchetti di aggiornamento** con entrambe le autorizzazioni **Modifica** e **Lettura** .
  -  È necessario che all'account sia assegnato l'ambito **Tutto** .



##  <a name="bkmk_beforeinstall"></a> Prima di installare un aggiornamento nella console  
 Esaminare i passaggi seguenti prima di installare un aggiornamento dalla console di Configuration Manager.  

###  <a name="bkmk_step1"></a> Passaggio 1: Esaminare l'elenco di controllo dell'aggiornamento  
Esaminare l'elenco di controllo dell'aggiornamento valido per le azioni da eseguire prima di iniziare l'aggiornamento:

- Aggiornamento alla versione 1606: vedere [Elenco di controllo per installare l'aggiornamento 1606 di System Center Configuration Manager](../../../core/servers/manage/checklist-for-installing-update-1606.md).  

- Aggiornamento alla versione 1610 dalla versione 1606: vedere [Elenco di controllo per l'installazione dell'aggiornamento 1610 di System Center Configuration Manager](../../../core/servers/manage/checklist-for-installing-update-1610.md).  

- Aggiornamento alla versione 1702 dalla versione 1606 o 1610: vedere [Elenco di controllo per l'installazione dell'aggiornamento 1702](../../../core/servers/manage/checklist-for-installing-update-1702.md).

<!-- Removed as update guidance 6/6/2017. The Test DB Upgrade details are no longer recommended nor required. They live on in a new topic for customers who still want to use them. -->

###  <a name="step-2-run-the-prerequisite-checker-before-installing-an-update"></a>Passaggio 2: Eseguire il controllo dei prerequisiti prima di installare un aggiornamento  
Prima di installare un aggiornamento, si consiglia di eseguire il controllo dei prerequisiti per l'aggiornamento. Se si esegue il prerequisito prima di installare un aggiornamento:  

-   I file di aggiornamento vengono replicati in altri siti prima dell'installazione dell'aggiornamento.  

-   Il controllo dei prerequisiti viene eseguito di nuovo automaticamente quando si sceglie di installare l'aggiornamento.  

Successivamente, quando si installa l'aggiornamento, è possibile configurarlo in modo che ignori gli avvisi del controllo dei prerequisiti.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Per eseguire il controllo dei prerequisiti prima di installare un aggiornamento  

1.  Nella console di Configuration Manager passare ad **Amministrazione** > **Aggiornamenti e manutenzione**.   

2.  Fare clic con il pulsante destro del mouse sul pacchetto di aggiornamento nel quale eseguire il controllo dei prerequisiti.  

3.  Scegliere **Esegui controllo prerequisiti**.  

     Quando si esegue il controllo dei prerequisiti, il contenuto dell'aggiornamento viene replicato nei siti figlio.  È possibile visualizzare distmgr.log nel server del sito per verificare che il contenuto venga replicato correttamente.  

4.  Per visualizzare i risultati del controllo, nella console di Configuration Manager passare a **Monitoraggio** > **Stato di aggiornamenti e manutenzione** e cercare lo stato dei prerequisiti. Per altre informazioni, è anche possibile visualizzare ConfigMgrPrereq.log nel server del sito.  



##  <a name="bkmk_install"></a> Installare gli aggiornamenti nella console  
 Per installare gli aggiornamenti dall'interno della console di Configuration Manager, iniziare con il sito di livello superiore della gerarchia. che corrisponde al sito di amministrazione centrale o a un sito primario autonomo.  

 È consigliabile installare l'aggiornamento fuori dal normale orario di ufficio per ogni sito per ridurre l'impatto sulle attività aziendali. L'installazione dell'aggiornamento può infatti comportare la reinstallazione dei componenti del sito e dei ruoli del sistema del sito.  

-   I siti primari figlio avviano automaticamente l'aggiornamento al termine dell'installazione dell'aggiornamento del sito di amministrazione centrale. Questo è il processo predefinito e consigliato. È tuttavia possibile usare [intervalli di servizio per i server del sito](/sccm/core/servers/manage/service-windows) per controllare quando vengono installati gli aggiornamenti in un sito primario.  

-   Dopo che l'aggiornamento del sito primario padre è completato, aggiornare manualmente i siti secondari dalla console di Configuration Manager. L'aggiornamento automatico dei server del sito secondario non è supportato.  

-   Quando si usa una console di Configuration Manager dopo l'aggiornamento del sito, viene chiesto di aggiornare la console.  

-  Dopo che il server del sito ha completato correttamente l'installazione di un aggiornamento, aggiorna automaticamente tutti i ruoli del sistema del sito applicabili.  L'unica avvertenza a questo proposito riguarda i punti di distribuzione. Quando si installa un aggiornamento, tutti i punti di distribuzione non reinstallano l'aggiornamento e vengono disconnessi per essere aggiornati contemporaneamente. Il server del sito usa le impostazioni di distribuzione del contenuto del sito stesso per distribuire l'aggiornamento a un subset di punti di distribuzione alla volta. Ne consegue che solo alcuni punti di distribuzione saranno offline per consentire l'installazione dell'aggiornamento. I punti di distribuzione per i quali non è stato avviato l'aggiornamento o che lo hanno completato restano in linea e continuano a fornire contenuto ai client.


###  <a name="bkmk_overview"></a> Panoramica dell'installazione degli aggiornamenti nella console  
**1. Quando viene avviata l'installazione dell'aggiornamento**  
Viene visualizzato l'Aggiornamento guidato che mostra un elenco di aree del prodotto a cui si applica l'aggiornamento.  

-   Nella pagina **Generale** della procedura guidata è possibile configurare **Avvisi relativi ai prerequisiti**.  
      -   Gli errori relativi ai prerequisiti arrestano sempre l'installazione dell'aggiornamento. Correggere gli errori prima di ritentare l'installazione dell'aggiornamento. Per altre informazioni, vedere [Ripetere l'installazione di un aggiornamento non riuscito](#bkmk_retry) .  

    -   Gli avvisi relativi ai prerequisiti possono anche arrestare l'installazione dell'aggiornamento. Risolvere gli avvisi prima di ritentare l'installazione dell'aggiornamento. Per altre informazioni, vedere [Ripetere l'installazione di un aggiornamento non riuscito](#bkmk_retry) .  
    -   L'opzione **Ignorare eventuali avvisi del controllo dei prerequisiti e installare questo aggiornamento anche in caso di requisiti mancanti** imposta una condizione per l'installazione dell'aggiornamento che ignora gli avvisi relativi ai prerequisiti. Ciò consente di continuare l'installazione dell'aggiornamento. Se non si seleziona questa opzione, l'installazione dell'aggiornamento si arresta quando viene visualizzato un avviso. L'uso di questa opzione non è consigliato, a meno che il controllo dei prerequisiti non sia già stato eseguito in precedenza e non siano già stati corretti gli avvisi relativi ai prerequisiti per un sito.  

      Nelle due aree di lavoro **Amministrazione** e **Monitoraggio** il nodo Aggiornamenti e manutenzione include il pulsante denominato **Ignora avvisi dei prerequisiti** sulla barra multifunzione. Questo pulsante diventa disponibile quando non viene completata l'installazione di un pacchetto di aggiornamento a causa di avvisi del controllo dei prerequisiti. Ad esempio, dall'Aggiornamento guidato si installa un aggiornamento senza usare l'opzione per ignorare gli avvisi dei prerequisiti. L'installazione dell'aggiornamento si interrompe con uno stato di avviso dei prerequisiti ma senza errori. È possibile scegliere **Ignora avvisi dei prerequisiti** dalla barra multifunzione in un secondo momento, per attivare il proseguimento automatico dell'installazione dell'aggiornamento che quindi ignora gli avvisi dei prerequisiti. Quando si usa questa opzione l'installazione dell'aggiornamento continua automaticamente dopo alcuni minuti.



-   Se un aggiornamento si applica al client di Configuration Manager, viene visualizzata l'opzione per testare l'aggiornamento con un numero limitato di client. Per altre informazioni, vedere [Come testare gli aggiornamenti client in una raccolta di pre-produzione in System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

**2. Durante l'installazione dell'aggiornamento**  
Nell'ambito dell'installazione dell'aggiornamento, Configuration Manager esegue le operazioni indicate di seguito:  

-   Reinstalla tutti i componenti interessati, ad esempio i ruoli del sistema del sito o la console di Configuration Manager.  

-   Gestisce gli aggiornamenti dei client in base alle selezioni effettuate per la distribuzione pilota del client e per gli [aggiornamenti automatici del client](https://technet.microsoft.com/library/mt627885.aspx).  

-   Non riavvia i server del sistema del sito durante l'aggiornamento, a meno che .NET non sia installato come parte di un prerequisito per i ruoli del sistema del sito.  

> [!TIP]  
>  Quando vengono installati gli aggiornamenti Configuration Manager aggiorna anche la cartella CD.Latest. Questa cartella viene usata in caso di ripristino del sito.  

**3. Monitorare lo stato di avanzamento degli aggiornamenti durante l'installazione**  
Per monitorare lo stato di avanzamento, usare quanto segue:  

-   Nella console di Configuration Manager: nodo **Amministrazione** > **Aggiornamenti e manutenzione**. Questo nodo mostra lo stato di installazione di tutti i pacchetti di aggiornamento.


-   Nella console di Configuration Manager: nodo **Monitoraggio** > **Panoramica** > **Stato di aggiornamenti e manutenzione**. Questo nodo indica solo lo stato di installazione del pacchetto di aggiornamento che si sta installando.  

    L'installazione del pacchetto di aggiornamento è suddivisa nelle fasi seguenti per facilitare il monitoraggio. Per ogni fase sono disponibili altri dettagli, incluso il file di log da visualizzare per avere maggiori informazioni:  
    -   **Download**: questa fase si applica solo al sito di livello superiore in cui è installato il sito del punto di connessione del servizio.   

    -   **Replica**   

    -   **Controllo dei prerequisiti**   

    -   **Installazione**    

    -   **Post-installazione**: [ le attività di post-installazione](#post-installation-tasks) sono disponibili a partire dalla versione 1610.  

-   È possibile visualizzare il file **CMUpdate.log** in **&lt;<Directory_Installazione_ConfigMgr>\Logs**  

**4. Quando viene completata l'installazione dell'aggiornamento**  
Quando viene completata l'installazione dell'aggiornamento del primo sito:  

-   I siti primari figlio installano automaticamente l'aggiornamento. Non è richiesta alcuna azione ulteriore.  

-   I siti secondari devono essere aggiornati manualmente dalla console di Configuration Manager.
> [!TIP]
> Anche se la versione di un sito secondario non viene visualizzata nella console, è possibile usare Configuration Manager SDK per verificare la versione di un sito. Vedere la [classe WMI server SMS_Site](https://technet.microsoft.com/library/hh442832(CMSDK.16).aspx).


-   Finché tutti i siti della gerarchia non vengono aggiornati alla nuova versione, la gerarchia funziona in modalità mista. Per ulteriori informazioni, vedere [Interoperability between different versions of System Center Configuration Manager](../../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

**5.   Aggiornare le console di Configuration Manager**  
Dopo l'aggiornamento di un sito di amministrazione centrale o di un sito primario, è necessario aggiornare anche tutte le console di Configuration Manager che si connettono al sito. Viene chiesto di aggiornare una console:  

-   Quando si apre la console.  

-   Quando si passa a un nuovo nodo in una console aperta.  

Si consiglia di installare l'aggiornamento immediatamente.  

Dopo aver completato l'aggiornamento della console, è possibile verificare che la versione della console e del sito sia corretta. Passare a **Informazioni su System Center Configuration Manager** nell'angolo in alto a sinistra della console.  

###  <a name="bkmk_toptier"></a> Per avviare l'installazione dell'aggiornamento nel sito di livello superiore  
Nel sito del livello superiore della gerarchia, nella console di Configuration Manager passare ad **Amministrazione** > **Aggiornamenti e manutenzione**, selezionare un aggiornamento **Disponibile** e quindi fare clic su **Installa pacchetto di aggiornamento**.  

###  <a name="bkmk_secondary"></a> Per avviare l'installazione dell'aggiornamento in un sito secondario  
Dopo aver aggiornato un sito primario padre di un sito secondario, è possibile aggiornare il sito secondario dalla console di Configuration Manager.  A tale scopo, usare l' **aggiornamento guidato per i siti secondari**.  

1.  Nella console di Configuration Manager passare ad **Amministrazione** > **Configurazione del sito** > **Siti**, selezionare il sito da aggiornare e quindi fare clic su **Aggiorna** nel gruppo **Sito** della scheda Home.  

2.  Fare clic su **Sì** per avviare l'aggiornamento del sito secondario.  

Per monitorare l'installazione dell'aggiornamento in un sito secondario, selezionare il server del sito secondario. Scegliere quindi **Mostra stato installazione** nel gruppo **Sito** della scheda **Home**. È anche possibile aggiungere la colonna **Versione** alla console per visualizzare la versione di ogni sito secondario.  

Dopo l'aggiornamento corretto di un sito secondario, se lo stato nella console non si aggiorna o indica che l'aggiornamento non è riuscito è possibile usare l'opzione **Riprova installazione**. Questa opzione non ripete l'aggiornamento di un sito secondario che l'ha eseguito correttamente, ma impone l'aggiornamento dello stato nella console.

### <a name="post-installation-tasks"></a>Attività post-installazione
A partire dalla versione 1610 è possibile visualizzare informazioni sulle attività post-installazione.

Quando viene installato l'aggiornamento di un sito, diverse attività non possono essere avviate fino al termine dell'installazione dell'aggiornamento nel server del sito. Di seguito sono elencate le attività di post-installazione che risultano fondamentali per le operazioni con il sito e con la gerarchia. Essendo fondamentali, sono monitorate attivamente. Tra le attività aggiuntive non direttamente monitorate è inclusa la reinstallazione dei ruoli del sistema del sito. Per visualizzare lo stato delle principali attività di post-installazione, selezionare l'attività di **post-installazione** durante il monitoraggio dell'installazione dell'aggiornamento di un sito.

Non tutte le attività vengono completate immediatamente. Alcune non vengono avviate fino a quando l'installazione dell'aggiornamento non viene completata in ogni sito. Pertanto, le nuove funzionalità previste potrebbero risultare ritardate fino al completamento di queste attività. Le nuove funzionalità, ad esempio, potrebbero non essere visibili per qualche tempo, poiché non vengono avviate fino a quando tutti i siti non completano l'installazione dell'aggiornamento.

Le attività di post-installazione includono:

-   **Installazione del servizio SMS_EXECUTIVE**
  -   Servizio critico eseguito nel server del sito.
  -   La reinstallazione di questo servizio viene completata rapidamente.


-   **Installazione del componente SMS_DATABASE_NOTIFICATION_MONITOR**
  -   Thread del componenti critico del sito del servizio SMS_EXECUTIVE.
  -   La reinstallazione di questo servizio viene completata rapidamente.


-   **Installazione del componente SMS_HIERARCHY_MANAGER**
  -   Componente critico del sito eseguito nel server del sito.
  -   Responsabile della reinstallazione dei ruoli del sistema del sito nei server del sistema del sito.  Non viene visualizzato lo stato della reinstallazione del singolo ruolo del sistema del sito.
  -   La reinstallazione di questo servizio viene completata rapidamente.


-   **Installazione del componente SMS_REPLICATION_CONFIGURATION_MONITOR**
  -   Componente critico del sito eseguito nel server del sito.
  -   La reinstallazione di questo servizio viene completata rapidamente.


-   **Installazione del componente SMS_POLICY_PROVIDER**
  -   Componente critico del sito eseguito solo nei siti primari.
  -   La reinstallazione di questo servizio viene completata rapidamente.


-   **Monitoraggio dell'inizializzazione della replica**   
  -   Visualizzata solo nel sito di amministrazione centrale e nei siti primari figlio.
  -   Dipende da SMS_REPLICATION_CONFIGURATION_MONITOR.
  -   Viene completata rapidamente.


-   **Aggiornamento del pacchetto di pre-produzione client di Configuration Manager**    
  -   Visualizzata anche se non è abilitato l'uso della pre-produzione client, anche detta distribuzione pilota del client.
  -   Non viene avviata fino a quando tutti i siti della gerarchia hanno installato 'aggiornamento.


-   **Aggiornamento della cartella Client nel server del sito**
  -   Non viene visualizzata se si usa il client in fase di pre-produzione.  
  -   Viene completata rapidamente.


-   **Aggiornamento del pacchetto client di Configuration Manager**
  -   Non viene visualizzata se si usa il client in fase di pre-produzione.  
  -   Termina solo quando tutti i siti hanno installato l'aggiornamento.  


-   **Attivazione delle funzionalità**
  -   Visualizzata solo nel sito di livello superiore della gerarchia.
  -   Non viene avviata fino a quando tutti i siti della gerarchia hanno installato 'aggiornamento.
  -   Non vengono visualizzate le singole funzionalità.


##  <a name="bkmk_retry"></a> Ripetere l'installazione di un aggiornamento non riuscito  
Quando l'installazione di un aggiornamento non riesce, esaminare i commenti nella console per individuare le possibili soluzioni per gli errori e gli avvisi. Per altre informazioni, è anche possibile visualizzare ConfigMgrPrereq.log nel server del sito. Prima di riprovare l'installazione di un aggiornamento, è necessario correggere gli errori ed è consigliabile correggere anche gli avvisi.  

> [!TIP]  
> In caso di problemi di download o di replica di un aggiornamento, è possibile usare lo [strumento di reimpostazione dell'aggiornamento](/sccm/core/servers/manage/update-reset-tool). Questo strumento è disponibile nei siti che eseguono la versione 1706 o successiva. 

Quando si è pronti per ripetere l'installazione di un aggiornamento, selezionare l'aggiornamento non riuscito e quindi scegliere un'opzione applicabile. Il nuovo tentativo di installazione dell'aggiornamento varia a seconda del nodo da cui viene riprovato e dal tipo di tentativo usato.  

1.  **Riprovare l'installazione per la gerarchia:**  
È possibile riprovare l'installazione di un aggiornamento per l'intera gerarchia quando l'aggiornamento è in uno degli stati seguenti:  

    -   Controllo prerequisiti superato con uno o più avvisi e opzione per ignorare gli avvisi di controllo dei prerequisiti non impostata nella procedura guidata di aggiornamento. Il valore dell'aggiornamento per **Ignora avviso prerequisito** nel nodo **Aggiornamenti e manutenzione** è **No**.   
    -   Il prerequisito non è riuscito    
    -   L'installazione non è riuscita
    -   La replica del contenuto nel sito non è riuscita   

    Passare ad **Amministrazione** > **Aggiornamenti e manutenzione**, selezionare l'aggiornamento e quindi scegliere una delle opzioni seguenti:  

    -   **Riprova** : quando si **riprova** da questo nodo viene avviata nuovamente l'installazione dell'aggiornamento e vengono automaticamente ignorati gli avvisi dei prerequisiti. Se la replica non è riuscita in precedenza, viene anche replicato nuovamente il contenuto dell'aggiornamento.
    - **Ignora avvisi dei prerequisiti**: a partire dalla versione 1606, se l'installazione dell'aggiornamento viene interrotta da un avviso, è possibile scegliere **Ignora avvisi dei prerequisiti**. Questa azione consente di continuare l'installazione dell'aggiornamento dopo alcuni minuti e di usare l'opzione per ignorare gli avvisi relativi ai prerequisiti.   

2.  **Riprovare l'installazione per il sito:**  
 È possibile riprovare l'installazione di un aggiornamento in un sito specifico quando l'aggiornamento è in uno degli stati seguenti:  

    -   Controllo prerequisiti superato con uno o più avvisi e opzione per ignorare gli avvisi di controllo dei prerequisiti non impostata nell'Aggiornamento guidato. Il valore dell'aggiornamento per **Ignora avviso prerequisito** nel nodo Aggiornamenti e manutenzione è **No**.  
    -   Il prerequisito non è riuscito    
    -   L'installazione non è riuscita    

    Passare a **Monitoraggio** > **Panoramica** > **Stato di manutenzione del sito**, selezionare l'aggiornamento e quindi una delle opzioni seguenti:

       - **Riprova** : quando si **riprova** da questo nodo l'installazione dell'aggiornamento viene avviata nuovamente sono nel sito specifico. A differenza di quanto accade quando si **riprova** dal nodo **Aggiornamenti e manutenzione**, questo nuovo tentativo non ignora gli avvisi dei prerequisiti.
       -    **Ignora avvisi dei prerequisiti**: a partire dalla versione 1606, se l'installazione dell'aggiornamento viene interrotta da un avviso, è possibile fare clic su **Ignora avvisi dei prerequisiti**. Questa azione consente di continuare l'installazione dell'aggiornamento dopo alcuni minuti e di usare l'opzione per ignorare gli avvisi relativi ai prerequisiti.

##  <a name="bkmk_after"></a> Dopo l'installazione di un aggiornamento in un sito  
Per completare le configurazioni e le attività comuni eseguite dopo l'aggiornamento di un sito, usare l'elenco di controllo seguente.   

**Verificare che la replica da sito a sito sia attiva:** nella console di Configuration Manager passare ai percorsi seguenti per visualizzare lo stato e verificare che la replica sia attiva:  

-   **Monitoraggio** > **Panoramica** > **Gerarchia siti**  

-   **Monitoraggio** > **Panoramica** > **Replica di database**  

Per altre informazioni, vedere [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) (Monitorare l'infrastruttura della gerarchia e di replica in System Center Configuration Manager) e [About the Replication Link Analyzer](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA) (Informazioni su Replication Link Analyzer).  

 **Verificare che i server del sito e i server del sistema del sito remoto siano stati riavviati (se necessario):** esaminare l'infrastruttura del sito e verificare che i server del sito e i server del sistema del sito siano stati riavviati correttamente. In genere, i server del sito vengono riavviati solo quando Configuration Manager installa .NET come prerequisito per un ruolo del sistema del sito.  

 **Aggiornare le console di Configuration Manager autonome:** verificare che tutte le console di Configuration Manager remote siano aggiornate alla stessa versione. Viene chiesto di aggiornare una console quando:  

-   Si passa a un nuovo nodo nella console.  

-   Si apre la console.

**Riconfigurare le repliche di database per i punti di gestione nei siti primari:** se si usano le repliche di database per i punti di gestione nei siti primari, è necessario disinstallarle prima di aggiornare il sito. Dopo l'aggiornamento di un sito primario riconfigurare la replica di database per i punti di gestione. Per altre informazioni, vedere [Repliche di database per i punti di gestione per System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Riconfigurare le attività di manutenzione del database disabilitate prima dell'aggiornamento:** se le [attività di manutenzione ](../../../core/servers/manage/maintenance-tasks.md) del database sono state disabilitate in un sito prima dell'aggiornamento, riconfigurare le attività nel sito. Usare le stesse impostazioni presenti prima dell'aggiornamento.  

**Aggiornare i client:** Per altre informazioni, vedere [Come aggiornare i client per i computer Windows in System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

**Altre configurazioni:** rivedere le modifiche apportate prima di iniziare l'aggiornamento, quindi ripristinare le configurazioni nei siti e nella gerarchia.  

##  <a name="bkmk_options"></a> Abilitare le funzionalità facoltative degli aggiornamenti  
Quando un aggiornamento include una o più funzionalità facoltative, è possibile abilitare queste funzionalità nella gerarchia.  È possibile abilitarle durante l'installazione dell'aggiornamento o tornare nella console in un secondo momento e abilitare le funzionalità facoltative.

Per visualizzare le funzionalità disponibili e il relativo stato, nella console passare ad **Amministrazione** > **Aggiornamenti e manutenzione** > **Funzionalità**.

Quando una funzionalità non è facoltativa, viene installata automaticamente e non viene visualizzata nel nodo **Funzionalità** .  


Quando si abilita una nuova funzionalità o una funzionalità non definitiva, gestione gerarchie (HMAN) di Configuration Manager deve elaborare la modifica prima che tale funzionalità diventi disponibile. L'elaborazione della modifica è spesso immediata, ma possono essere necessari fino a 30 minuti, a seconda del ciclo di elaborazione HMAN. Dopo l'elaborazione della modifica è necessario riavviare la console prima di poter visualizzare la nuova interfaccia utente relativa a tale funzionalità.


##  <a name="bkmk_prerelease"></a> Usare le funzionalità di versioni non definitive degli aggiornamenti
Le funzionalità di versioni non definitive sono incluse nel Current Branch a scopo di test preliminare in un ambiente di produzione. Queste funzionalità non devono essere considerate pronte per l'ambiente di produzione, ma possono essere usate in un ambiente di questo tipo. Vedere [Funzionalità di versioni non definitive](/sccm/core/servers/manage/pre-release-features) per altre informazioni, ad esempio su come abilitarle nell'ambiente.             


## <a name="known-issues"></a>Problemi noti

###  <a name="bkmk_faq"></a> Perché alcuni aggiornamenti non sono visualizzati nella console?  
 Se non si trova un aggiornamento specifico nella console dopo una sincronizzazione riuscita con il servizio cloud Microsoft, la causa potrebbe essere:  

-   L'aggiornamento richiede una configurazione non usata dall'infrastruttura oppure la versione corrente del prodotto non soddisfa un prerequisito per la ricezione dell'aggiornamento.  

     Se si ritiene di usare le configurazioni richieste o altri requisiti per un aggiornamento mancante, verificare che il punto di connessione del servizio sia in modalità online. Usare quindi l'opzione **Controlla aggiornamenti** nel nodo **Aggiornamenti e manutenzione** per forzare un controllo.  In modalità offline è necessario usare lo strumento di connessione del servizio per sincronizzare manualmente il servizio cloud.  

-   L'account non ha le autorizzazioni corrette di amministrazione basata su ruoli per visualizzare gli aggiornamenti nella console di Configuration Manager.

    Per informazioni sulle autorizzazioni richieste per visualizzare gli aggiornamenti e abilitare le funzionalità dall'interno della console, vedere [Autorizzazioni per la gestione degli aggiornamenti](../../../core/servers/manage/install-in-console-updates.md#assign-permissions-to-view-and-manage-updates-and-features) in questo argomento.

### <a name="why-do-i-see-two-updates-for-version-1610"></a>Perché vengono visualizzati due aggiornamenti per la versione 1610?
Nella console possono talvolta essere visualizzati due aggiornamenti per la versione 1610. Questi aggiornamenti hanno date diverse. Entrambi vengono visualizzati quando una delle condizioni seguenti viene soddisfatta:   
-   È stata installata una versione precedente (ad esempio la 1606) dopo che la versione 1610 è diventata disponibile.

-   La gerarchia esegue la versione 1511 o 1602 e non è stato possibile scaricare la versione 1606.

Sono disponibili due aggiornamenti per la versione 1610 perché questo aggiornamento è stato rilasciato una seconda volta dopo che sono state apportate piccole modifiche ad alcuni file binari. Queste modifiche non influiscono sulla funzionalità di Configuration Manager o sull'aggiornamento.

Quando entrambi gli aggiornamenti sono disponibili nella console, è consigliabile installare quello con la data più recente. Tuttavia, poiché entrambi gli aggiornamenti offrono la stessa funzionalità, se uno è già stato installato non è necessario eseguire altre operazioni.
-   Se in precedenza si è installato l'aggiornamento meno recente, non è necessario installare anche quello con la data più recente. Se si installa l'aggiornamento più recente dopo aver installato il primo, i file binari in questione vengono aggiornati. Non si verifica alcun cambiamento aggiuntivo e non sono necessarie altre azioni da parte dell'utente.

-   Se in precedenza si è installato l'aggiornamento più recente e quindi si installa l'aggiornamento con la data meno recente, non sono comunque necessarie altre operazioni. Questo perché i file binari più recenti che sono già installati non vengono sovrascritti da quelli dell'aggiornamento originale.


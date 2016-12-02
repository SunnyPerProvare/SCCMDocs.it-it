---
title: Aggiornamenti nella console | System Center Configuration Manager
description: System Center Configuration Manager si sincronizza con il cloud Microsoft per ottenere aggiornamenti installabili all'interno della console.
ms.custom: na
ms.date: 10/06/2016
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
translationtype: Human Translation
ms.sourcegitcommit: f777295958e9cbc729e3759d354521c96ae3e8ac
ms.openlocfilehash: b9721737b4181d8f5e41224c3e2c32ae41647554


---
# <a name="install-in-console-updates-for-system-center-configuration-manager"></a>Installare gli aggiornamenti nella console per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager si sincronizza con il servizio cloud Microsoft per ottenere aggiornamenti che è quindi possibile installare dall'interno della console.

## <a name="get-available-updates"></a>Ottenere gli aggiornamenti disponibili
Solo gli aggiornamenti che si applicano all'infrastruttura e alla versione vengono scaricati e resi disponibili nella gerarchia. Questa sincronizzazione può essere automatica o manuale a seconda di come si configura il punto di connessione del servizio per la gerarchia:

-   In **modalità online**il punto di connessione si connette automaticamente al servizio cloud Microsoft e scarica gli aggiornamenti applicabili.  

     Per impostazione predefinita, Configuration Manager verifica la disponibilità di nuovi aggiornamenti ogni 24 ore. A partire dalla versione 1602, è anche possibile verificare la disponibilità di aggiornamenti immediatamente facendo clic su **Verifica la disponibilità di aggiornamenti** nel nodo **Amministrazione** > **Servizi cloud** > **Aggiornamenti e manutenzione** della console di Configuration Manager.  

-   In **modalità offline** il punto di connessione del servizio non si connette al servizio cloud Microsoft ed è necessario [Usare lo strumento di connessione del servizio per System Center Configuration Manager](../../../core/servers/manage/use-the-service-connection-tool.md) per scaricare e importare gli aggiornamenti disponibili.  

> [!NOTE]  
>  Oltre agli aggiornamenti ottenuti durante la sincronizzazione con il servizio cloud Microsoft, nella console vengono importate anche le correzioni fuori programma che vengono installate, a discrezione dell'utente, con lo [strumento di registrazione dell'aggiornamento](http://technet.microsoft.com/library/mt691544.aspx) .  

Dopo aver sincronizzato gli aggiornamenti è possibile visualizzarli nella console di Configuration Manager passando al nodo **Amministrazione** > **Servizi Cloud** > **Aggiornamenti e manutenzione**:  

-   Gli aggiornamenti non installati vengono visualizzati con l'indicazione **Disponibile**.

-   Gli aggiornamenti installati vengono visualizzati con l'indicazione **Installato**.  A partire dalla versione 1606, viene visualizzato soltanto l'ultimo aggiornamento installato ed è possibile fare clic sul pulsante **Cronologia** sulla barra multifunzione per visualizzare gli aggiornamenti installati precedentemente.



Prima di configurare il punto di connessione del servizio, esaminare e pianificare gli usi aggiuntivi che possono influire sulla modalità di configurazione di questo ruolo del sistema del sito:  

-   Il punto di connessione del servizio viene usato per caricare le informazioni di utilizzo relative al sito. Queste informazioni consentono al servizio cloud di Microsoft di identificare gli aggiornamenti disponibili per la versione corrente dell'infrastruttura. Per altre informazioni, vedere [Dati di diagnostica e di utilizzo per System Center Configuration Manager](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)  

-   Il punto di connessione del servizio viene usato per gestire i dispositivi con Microsoft Intune e con la gestione dei dispositivi mobili locale di Configuration Manager. Per altre informazioni, vedere [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../../mdm/plan-design/hybrid-mobile-device-management.md) (Gestione di dispositivi mobili ibridi con System Center Configuration Manager e Microsoft Intune).  

Per comprendere ciò che accade quando vengono scaricati gli aggiornamenti, vedere:  

-   [Diagramma di flusso - scaricare gli aggiornamenti per System Center Configuration Manager](../../../core/servers/manage/download-updates-flowchart.md).  

-   [Flowchart - Update replication for System Center Configuration Manager](../../../core/servers/manage/update-replication-flowchart.md) (Diagramma di flusso: replica dell'aggiornamento per System Center Configuration Manager)  

## <a name="permissions-to-view-and-manage-updates-and-features"></a>Autorizzazioni per la visualizzazione e la gestione degli aggiornamenti e delle funzionalità
Prima di installare l'aggiornamento alla versione 1606, per visualizzare gli aggiornamenti nella console è necessario assegnare a un utente un ruolo di sicurezza che include l'autorizzazione **Lettura** nel gruppo di autorizzazioni **Sito**e l'ambito di protezione **Tutto**. Dall'aggiornamento 1606 è stata introdotta una nuova classe di protezione dell'amministrazione basata sui ruoli denominata **Pacchetti di aggiornamento** che concede l'accesso per visualizzare e gestire gli aggiornamenti nella console di Configuration Manager.    

**Informazioni sulla classe Pacchetti di aggiornamento:**  
Per impostazione predefinita, **Pacchetti di aggiornamento** (SMS_CM_Updatepackages) fa parte dei seguenti ruoli di sicurezza predefiniti con le autorizzazioni elencate:
 -  **Amministratore completo** con autorizzazioni **Modifica** e **Lettura** :
    -   Un utente con questo ruolo di sicurezza e l'accesso all'ambito di protezione **Tutto** può visualizzare e installare gli aggiornamenti, abilitare le funzionalità durante l'installazione e abilitare le singole funzionalità dopo l'installazione dell'aggiornamento.
    - Un utente con questo ruolo di sicurezza e l'accesso all'ambito di protezione **Predefinito** può visualizzare e installare gli aggiornamenti, abilitare le funzionalità durante l'installazione e visualizzare le funzionalità dopo l'installazione dell'aggiornamento ma non può abilitarle dopo l'installazione dell'aggiornamento.

- **Analista di sola lettura** con autorizzazioni **Lettura** :
  -  Un utente con questo ruolo di sicurezza e l'accesso all'ambito di protezione **Predefinito** può visualizzare gli aggiornamenti ma non installarli e può visualizzare le funzionalità dopo l'installazione dell'aggiornamento ma non può abilitarle.

**Riepilogo delle autorizzazioni richieste per gli aggiornamenti e la manutenzione:**   
  - Usare un account cui è assegnato un ruolo di sicurezza che include la classe **Pacchetti di aggiornamento** con entrambe le autorizzazioni **Modifica** e **Lettura** .
  - È necessario che all'account sia assegnato l'ambito **Predefinito** .

**Per visualizzare solo gli aggiornamenti**:
  - Usare un account cui è assegnato un ruolo di sicurezza che include la classe **Pacchetti di aggiornamento** con solo l'autorizzazione **Lettura** .
  - È necessario che all'account sia assegnato l'ambito **Predefinito** .

**Per abilitare le funzionalità dopo l'installazione degli aggiornamenti:**
  -   Usare un account cui è assegnato un ruolo di sicurezza che include la classe **Pacchetti di aggiornamento** con entrambe le autorizzazioni **Modifica** e **Lettura** .
  -  È necessario che all'account sia assegnato l'ambito **Tutto** .






##  <a name="a-namebkmkbeforeinstalla-before-you-install-an-in-console-update"></a><a name="bkmk_beforeinstall"></a> Prima di installare un aggiornamento nella console  
 Prima di procedere all'installazione degli aggiornamenti dalla console di Configuration Manager eseguire la procedura seguente:  

###  <a name="a-namebkmkstep1a-step-1-review-the-update-checklist"></a><a name="bkmk_step1"></a> Passaggio 1: Esaminare l'elenco di controllo dell'aggiornamento  
Prima di installare un nuovo aggiornamento dall'interno della console di Configuration Manager, esaminare l'elenco di controllo dell'aggiornamento applicabile per le azioni da eseguire prima di iniziare l'aggiornamento:  

-   Eseguire l'aggiornamento alla versione 1511 come descritto in [Eseguire l'aggiornamento a System Center Configuration Manager](../../../core/servers/deploy/install/upgrade-to-configuration-manager.md)    

-   Eseguire l'aggiornamento alla versione 1602 dalla versione 1511: vedere [Elenco di controllo per l'aggiornamento di System Center Configuration Manager dalla versione 1511 alla versione 1602](../../../core/servers/manage/checklist-for-installing-update-1602.md)

- Eseguire l'aggiornamento alla versione 1602 dalla versione 1511 o 1602: vedere [Checklist for installing update 1606](../../../core/servers/manage/checklist-for-installing-update-1606.md) (Elenco di controllo per l'aggiornamento alla versione 1606)  


###  <a name="a-namebkmkstep2a-step-2-test-the-database-upgrade-before-installing-an-update"></a><a name="bkmk_step2"></a> Passaggio 2: Testare l'aggiornamento del database prima di installare un aggiornamento  
Prima di installare un nuovo aggiornamento nella gerarchia, ad esempio l'aggiornamento 1602, è necessario testare l'aggiornamento del database del sito. Il nome dell'opzione della riga di comando usata per testare l'installazione di un aggiornamento in un backup del database del sito è **testdbupgrade**.  

A differenza delle versioni precedenti di Configuration Manager, se l'installazione di un aggiornamento non riesce non è necessario eseguire un ripristino del sito, ma si può riprovare l'installazione dell'aggiornamento stesso. Di conseguenza, anche se l'aggiornamento di test del database è meno importante rispetto alle versioni precedenti del prodotto, rimane comunque un'operazione consigliata.  

##### <a name="to-run-testdbupgrade-before-installing-an-update"></a>Per eseguire testdbupgrade prima di installare un aggiornamento  

1.  Ottenere un set di file di origine dalla cartella **CD.Latest** di un sito che esegue la versione a cui si intende eseguire l'aggiornamento. Potrebbe essere necessario installare prima un sito in un ambiente lab o di test che esegue tale versione di System Center Configuration Manager.  

     La cartella **CD.Latest** di un sito contiene i file di origine per la versione. Per eseguire l'aggiornamento di test del database del sito, è necessario usare questi file di origine. Per altre informazioni, vedere [Cartella CD.Latest per System Center Configuration Manager](../../../core/servers/manage/the-cd.latest-folder.md).  

     Ad esempio, se il sito esegue una versione 1501 e si vuole eseguire l'aggiornamento alla 1602, è necessario ottenere una cartella CD.Latest da un sito già aggiornato alla versione 1602. In genere, è possibile installare un nuovo sito temporaneo in un lab e aggiornare questo sito alla versione 1602 per creare la cartella CD.Latest con i file necessari.  

2.  Copiare la cartella CD.Latest in un percorso di SQL Server usato per eseguire l'aggiornamento di test del database. Vedere il passaggio successivo.  

3.  Creare un backup del database del sito per l'aggiornamento di test, quindi ripristinare una copia del database in un'istanza di SQL Server che non ospita un sito di Configuration Manager. SQL Server deve usare la stessa edizione di SQL Server del database del sito.  

4.  Dopo aver ripristinato la copia del database, eseguire il **programma di installazione** dalla cartella CD.Latest copiata dall'ambiente lab o di test. Quando si esegue l'installazione, utilizzare l'opzione della riga di comando **/TESTDBUPGRADE** . Se l'istanza di SQL Server che ospita la copia del database non è quella predefinita, occorre anche fornire gli argomenti della riga di comando per identificare l'istanza che ospita la copia del database del sito.  

     Ad esempio, si pianifica di aggiornare un database del sito con il nome database SMS_ABC. Si ripristina una copia di questo database del sito in un'istanza supportata di SQL Server con il nome istanza DBTest. Per testare un aggiornamento di questa copia del database del sito, usare la seguente riga di comando: **Setup.exe /TESTDBUPGRADE DBtest\CM_ABC**  

     È possibile trovare Setup.exe nel percorso seguente del supporto di origine per System Center Configuration Manager: **SMSSETUP\BIN\X64**.  

5.  Nell'istanza di SQL Server in cui si esegue l'aggiornamento di test del database, monitorare ConfigMgrSetup.log nella radice dell'unità di sistema per verificarne lo stato di avanzamento e il completamento.  

     se l'aggiornamento test ha esito negativo, risolvere eventuali problemi relativi al fallimento dell'aggiornamento del database del sito, creare un nuovo backup del database del sito, quindi testare l'aggiornamento della nuova copia del database del sito.  

     Una volta completato il processo in modo corretto, è possibile eliminare la copia del database.  

    > [!NOTE]  
    >  Non è supportato il ripristino della copia del database del sito che si utilizza per l'aggiornamento test utilizzato a sua volta come database del sito in qualsiasi sito.  

###  <a name="a-namebkmkstep3a-step-3-run-the-prerequisite-checker-before-installing-an-update"></a><a name="bkmk_step3"></a> Passaggio 3: Eseguire il controllo dei prerequisiti prima di installare un aggiornamento  
Prima di installare un aggiornamento, si consiglia di eseguire il controllo dei prerequisiti per l'aggiornamento. Se si esegue il prerequisito prima di installare un aggiornamento:  

-   I file di aggiornamento vengono replicati in altri siti prima di installare effettivamente l'aggiornamento  

-   Il controllo dei prerequisiti viene eseguito di nuovo automaticamente quando si sceglie di installare l'aggiornamento  

Successivamente, quando si installa un aggiornamento, è possibile configurare l'aggiornamento in modo che ignori gli avvisi del controllo dei prerequisiti.  

##### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Per eseguire il controllo dei prerequisiti prima di installare un aggiornamento  

1.  Nella console di Configuration Manager passare ad **Amministrazione** > **Servizi cloud** > **Aggiornamenti e manutenzione**.  

2.  Fare clic con il pulsante destro del mouse sul pacchetto di aggiornamento su cui eseguire il controllo dei prerequisiti.  

3.  Scegliere **Esegui controllo prerequisiti**.  È possibile visualizzare  

     Quando si esegue il controllo dei prerequisiti, il contenuto dell'aggiornamento viene replicato nei siti figlio.  È possibile visualizzare **distmgr.log** nel server del sito per verificare che il contenuto venga replicato correttamente.  

4.  Per visualizzare i risultati del controllo, nella console di Configuration Manager passare a **Monitoraggio** > **Stato di aggiornamenti e manutenzione** e cercare lo stato dei prerequisiti. Per altre informazioni, è anche possibile visualizzare ConfigMgrPrereq.log nel server del sito.  



##  <a name="a-namebkmkinstalla-install-in-console-updates"></a><a name="bkmk_install"></a> Installare gli aggiornamenti nella console  
 Per installare gli aggiornamenti dall'interno della console di Configuration Manager, iniziare con il sito di livello superiore della gerarchia. che corrisponde al sito di amministrazione centrale o a un sito primario autonomo.  

 Si consiglia di non pianificare l'installazione dell'aggiornamento per ogni sito durante il normale orario di ufficio in modo che il processo di installazione dell'aggiornamento e le azioni per reinstallare i componenti del sito e i ruoli del sistema del sito abbiano un impatto minimo sulle operazioni aziendali.  

-   I siti primari figlio avviano automaticamente l'aggiornamento al termine dell'installazione dell'aggiornamento del sito di amministrazione centrale. Questo è il processo predefinito e consigliato. È tuttavia possibile usare [intervalli di servizio per i server del sito](#bkmk_ServiceWindow) per controllare quando vengono installati gli aggiornamenti in un sito primario.  

-   Dopo che l'aggiornamento del sito primario padre è completato, è necessario aggiornare manualmente i siti secondari dalla console di Configuration Manager. L'aggiornamento automatico dei server del sito secondario non è supportato.  

-   Quando si usa una console di Configuration Manager dopo l'aggiornamento del sito, viene chiesto di aggiornare la console.  

-  Dopo che il server del sito ha completato correttamente l'installazione di un aggiornamento, aggiorna automaticamente tutti i ruoli del sistema del sito applicabili.  L'unica avvertenza a questo proposito riguarda i punti di distribuzione:
  - A causa di modifiche introdotte con l'aggiornamento 1606, quando si installa un aggiornamento a un sito che esegue già la versione 1606 o una versione successiva, i punti di distribuzione non passano più alla modalità offline per l'aggiornamento tutti nello stesso tempo. Il server del sito usa le impostazioni di distribuzione del contenuto del sito stesso per distribuire l'aggiornamento a un subset di punti di distribuzione alla volta. Ne consegue che solo alcuni punti di distribuzione saranno offline per consentire l'installazione dell'aggiornamento. I punti di distribuzione per i quali non è stato avviato l'aggiornamento o che lo hanno completato restano in linea e continuano a fornire contenuto ai client.


###  <a name="a-namebkmkoverviewa-overview-of-in-console-update-installation"></a><a name="bkmk_overview"></a> Panoramica dell'installazione degli aggiornamenti nella console  
**1. Quando viene avviata l'installazione dell'aggiornamento**  
Viene visualizzato l'Aggiornamento guidato che mostra un elenco di aree del prodotto a cui si applica l'aggiornamento.  

-   Nella pagina **Generale** della procedura guidata è possibile configurare **Avvisi relativi ai prerequisiti**.  
      -   Gli errori relativi ai prerequisiti arrestano sempre l'installazione dell'aggiornamento. È necessario risolvere gli errori prima di poter riprovare l'installazione dell'aggiornamento. Per altre informazioni, vedere [Ripetere l'installazione di un aggiornamento non riuscito](#bkmk_retry) .  

    -   Gli avvisi relativi ai prerequisiti possono anche arrestare l'installazione dell'aggiornamento. Prima di riprovare l'installazione dell'aggiornamento, è necessario risolvere gli avvisi.   Per altre informazioni, vedere [Ripetere l'installazione di un aggiornamento non riuscito](#bkmk_retry) .  
    -   Se si seleziona l'opzione **Ignorare eventuali avvisi del controllo dei prerequisiti e installare questo aggiornamento anche in caso di requisiti mancanti**, viene impostata una condizione per l'installazione dell'aggiornamento che ignora gli avvisi relativi ai prerequisiti e consente di continuare l'installazione dell'aggiornamento. Se non si seleziona questa opzione, l'installazione dell'aggiornamento si arresta quando viene visualizzato un avviso. L'uso di questa opzione non è consigliato, a meno che il controllo dei prerequisiti non sia già stato eseguito in precedenza e non siano già stati risolti gli avvisi relativi ai prerequisiti per un sito.  

      A partire dalla versione 1606, in entrambe le aree di lavoro **Amministrazione** e **Monitoraggio** il nodo Aggiornamenti e manutenzione include un pulsante sulla barra multifunzione denominato **Ignora avvisi dei prerequisiti**. Questo pulsante diventa disponibile quando non viene completata l'installazione di un pacchetto di aggiornamento a causa di avvisi del controllo dei prerequisiti.  Ad esempio, se si installa un aggiornamento senza usare l'opzione Ignora avvisi dei prerequisiti della procedura guidata e l'installazione dell'aggiornamento viene interrotta da un avviso relativo ai prerequisiti senza che si siano verificati errori, è possibile selezionare **Ignora avvisi dei prerequisiti** dalla barra multifunzione per riprendere automaticamente l'installazione ignorando gli avvisi dei prerequisiti.  Quando viene usata questa opzione, l'installazione dell'aggiornamento continua automaticamente dopo alcuni minuti.



-   Se un aggiornamento si applica al client di Configuration Manager, viene visualizzata l'opzione per testare l'aggiornamento con un numero limitato di client. Per altre informazioni, vedere [Come testare gli aggiornamenti client in una raccolta di pre-produzione in System Center Configuration Manager](../../../core/clients/manage/upgrade/test-client-upgrades.md).  

**2. Durante l'installazione dell'aggiornamento**  
Nell'ambito dell'installazione dell'aggiornamento, Configuration Manager esegue le operazioni indicate di seguito:  

-   Reinstalla tutti i componenti interessati come ruoli del sistema del sito o la console di Configuration Manager  

-   Gestisce gli aggiornamenti dei client in base alle selezioni effettuate per la distribuzione pilota del client e per gli [aggiornamenti automatici del client](https://technet.microsoft.com/library/mt627885.aspx)  

-   Non deve riavviare i server del sistema del sito durante l'aggiornamento, a meno che .NET non sia installato come parte di un prerequisito per i ruoli del sistema del sito  

> [!TIP]  
>  Quando vengono installati gli aggiornamenti, Configuration Manager aggiorna anche la cartella CD.Latest, usata per il ripristino del sito.  

**3. Monitorare lo stato di avanzamento degli aggiornamenti durante l'installazione**  
Per monitorare lo stato di avanzamento, usare quanto segue:  

-   Nella console di Configuration Manager: nodo **Amministrazione** > **Servizi cloud** > **Aggiornamenti e manutenzione**. Questo nodo mostra lo stato di installazione di tutti i pacchetti di aggiornamento.


-   Nella console di Configuration Manager: nodo **Monitoraggio** > **Panoramica** > **Stato di aggiornamenti e manutenzione**. Questo nodo mostra solo lo stato di installazione del pacchetto di aggiornamento che si sta installando.  

    A partire dalla versione 1606, l'installazione del pacchetto di aggiornamenti è suddivisa nelle fasi seguenti per facilitare il monitoraggio. Per ogni fase sono ora disponibili ulteriori dettagli, incluso il file di log da visualizzare per ulteriori informazioni:  
    -   **Download** (si applica solo al sito di livello superiore in cui è installato il ruolo del sistema del sito del punto di connessione del servizio)
    -   **Replica**
    - **Controllo dei prerequisiti**
    - **Installazione**

-   È possibile visualizzare il file **CMUpdate.log** in **&lt;Directory_installazione_ConfigMgr>\Logs\\**  

**4. Quando viene completata l'installazione dell'aggiornamento**  
Quando viene completata l'installazione dell'aggiornamento del primo sito:  

-   I siti primari figlio installano automaticamente l'aggiornamento. Non è richiesta alcuna azione ulteriore.  

-   I siti secondari devono essere aggiornati manualmente dalla console di Configuration Manager.
> [!TIP]
> Anche se la versione di un sito secondario non viene visualizzata nella console, è possibile usare Configuration Manager SDK per verificare la versione dei siti. Vedere la [classe WMI server SMS_Site](https://technet.microsoft.com/library/hh442832(CMSDK.16).aspx).


-   Finché tutti i siti della gerarchia non vengono aggiornati alla nuova versione, la gerarchia funziona in modalità mista. Per ulteriori informazioni, vedere [Interoperability between different versions of System Center Configuration Manager](../../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

**5.   Aggiornare le console di Configuration Manager**  
Dopo l'aggiornamento di un sito di amministrazione centrale o di un sito primario, è necessario aggiornare anche tutte le console di Configuration Manager che si connettono al sito. Viene chiesto di aggiornare una console:  

-   Quando si apre la console  

-   Quando si passa a un nuovo nodo in una console aperta  

Si consiglia di installare l'aggiornamento immediatamente, senza rimandarlo.  

Dopo aver completato l'aggiornamento della console, è possibile verificare che la versione della console e del sito sia corretta. Passare a **Informazioni su System Center Configuration Manager** nell'angolo in alto a sinistra della console dove è visualizzata la nuova versione del sito e della console.  

###  <a name="a-namebkmktoptiera-to-start-the-update-installation-at-the-top-tier-site"></a><a name="bkmk_toptier"></a> Per avviare l'installazione dell'aggiornamento nel sito di livello superiore  
Nel livello superiore della gerarchia nella console di Configuration Manager passare ad **Amministrazione** > **Servizi cloud** > **Aggiornamenti e manutenzione,** selezionare un aggiornamento **Disponibile** e quindi fare clic su **Installa pacchetto di aggiornamento**.  

###  <a name="a-namebkmksecondarya-to-start-the-update-installation-at-a-secondary-site"></a><a name="bkmk_secondary"></a> Per avviare l'installazione dell'aggiornamento in un sito secondario  
Dopo aver aggiornato un sito primario padre di un sito secondario, è possibile aggiornare il sito secondario dall'interno della console di Configuration Manager.  A tale scopo, usare l' **aggiornamento guidato per i siti secondari**.  

1.  Nella console di Configuration Manager passare ad **Amministrazione** > **Configurazione del sito** > **Siti**, selezionare il sito da aggiornare e quindi fare clic su **Aggiorna** nel gruppo Sito della scheda Home.  

2.  Fare clic su **Sì** per avviare l'aggiornamento del sito secondario.  

Per monitorare l'installazione dell'aggiornamento in un sito secondario, selezionare il server del sito secondario, quindi fare clic su **Mostra stato installazione**nel gruppo Sito della scheda Home. È anche possibile aggiungere la colonna **Versione** alla console per visualizzare la versione di ogni sito secondario.  

Dopo l'aggiornamento corretto di un sito secondario, se lo stato nella console non si aggiorna o indica che l'aggiornamento non è riuscito è possibile usare l'opzione **Riprova installazione**. Questa opzione non ripete l'aggiornamento di un sito secondario che l'ha eseguito correttamente, ma impone l'aggiornamento dello stato nella console.


##  <a name="a-namebkmkretrya-retry-installation-of-a-failed-update"></a><a name="bkmk_retry"></a> Ripetere l'installazione di un aggiornamento non riuscito  
Quando l'installazione di un aggiornamento non riesce, esaminare i commenti nella console per individuare le possibili soluzioni per gli errori e gli avvisi.  Per altre informazioni, è anche possibile visualizzare ConfigMgrPrereq.log nel server del sito. Prima di riprovare l'installazione di un aggiornamento, è necessario risolvere gli errori ed è consigliabile risolvere anche gli avvisi.  

Quando si è pronti per ripetere l'installazione di un aggiornamento, selezionare l'aggiornamento non riuscito e quindi selezionare un'opzione applicabile. Il nuovo tentativo di installazione dell'aggiornamento varia a seconda del nodo da cui viene avviato nuovamente l'aggiornamento e dell'opzione selezionata:  

1.  **Riprovare l'installazione per la gerarchia:**  
È possibile riprovare l'installazione di un aggiornamento per l'intera gerarchia quando l'aggiornamento è in uno degli stati seguenti:  

    -   Il controllo dei prerequisiti è stato superato con uno o più avvisi e l'opzione che consente di ignorare gli avvisi del controllo dei prerequisiti non è stata impostata nell'Aggiornamento guidato, ovvero il valore per gli aggiornamenti **Ignora avviso prerequisito** nel nodo Aggiornamenti e manutenzione è **No**   
    -   Il prerequisito non è riuscito    
    -   L'installazione non è riuscita
    -   La replica del contenuto nel sito non è riuscita   

    Passare ad **Amministrazione** > **Servizi cloud** > **Aggiornamenti e manutenzione**, selezionare l'aggiornamento e selezionare una delle opzioni seguenti:  

    -   **Riprova** : quando si riprova da questo nodo, viene avviata nuovamente l'installazione dell'aggiornamento e vengono automaticamente ignorati gli avvisi dei prerequisiti. Se la replica non è riuscita in precedenza, viene anche replicato nuovamente il contenuto dell'aggiornamento.
    - **Ignora avvisi dei prerequisiti** : a partire dalla versione 1606, se l'installazione dell'aggiornamento viene interrotta da un avviso, è possibile fare clic su Ignora avvisi dei prerequisiti. Questa azione consente di continuare l'installazione dell'aggiornamento dopo alcuni minuti e di usare l'opzione per ignorare gli avvisi relativi ai prerequisiti.   

2.  **Riprovare l'installazione per il sito:**  
 È possibile riprovare l'installazione di un aggiornamento in un sito specifico quando l'aggiornamento è in uno degli stati seguenti:  

    -   Il controllo dei prerequisiti è stato superato con uno o più avvisi e l'opzione che consente di ignorare gli avvisi del controllo dei prerequisiti non è stata impostata nell'Aggiornamento guidato, ovvero il valore per gli aggiornamenti **Ignora avviso prerequisito** nel nodo Aggiornamenti e manutenzione è **No**  
    -   Il prerequisito non è riuscito    
    -   L'installazione non è riuscita    

    Passare a **Monitoraggio** > **Panoramica** > **Stato di manutenzione del sito**, selezionare l'aggiornamento e quindi selezionare una delle opzioni seguenti:

       - **Riprova** : quando si riprova da questo nodo, l'installazione dell'aggiornamento viene avviata nuovamente sono nel sito specifico. A differenza di un nuovo tentativo dal nodo Aggiornamenti e manutenzione, questo nuovo tentativo non ignora gli avvisi dei prerequisiti.
       -    **Ignora avvisi dei prerequisiti** : a partire dalla versione 1606, se l'installazione dell'aggiornamento viene interrotta da un avviso, è possibile fare clic su Ignora avvisi dei prerequisiti. Questa azione consente di continuare l'installazione dell'aggiornamento dopo alcuni minuti e di usare l'opzione per ignorare gli avvisi relativi ai prerequisiti.

##  <a name="a-namebkmkaftera-after-a-site-installs-an-update"></a><a name="bkmk_after"></a> Dopo l'installazione di un aggiornamento in un sito  
Per completare le configurazioni e le attività comuni eseguite dopo l'aggiornamento di un sito, usare l'elenco di controllo seguente:  

**Verificare che la replica da sito a sito sia attiva:** nella console di Configuration Manager passare ai percorsi seguenti per visualizzare lo stato e verificare che la replica sia attiva:  

-   **Monitoraggio** > **Panoramica** > **Gerarchia siti**  

-   **Monitoraggio** > **Panoramica** > **Replica di database**  

Per altre informazioni, vedere [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) (Monitorare l'infrastruttura della gerarchia e di replica in System Center Configuration Manager) e [About the Replication Link Analyzer](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA) (Informazioni su Replication Link Analyzer).  

 **Verificare che i server del sito e i server del sistema del sito remoto siano stati riavviati (se richiesto):** esaminare l'infrastruttura del sito e verificare che i server del sito e i server del sistema del sito (remoti rispetto al server del sito) richiesti siano stati riavviati correttamente.  In genere, questo passaggio è previsto solo quando Configuration Manager installa .NET come prerequisito per un ruolo del sistema del sito.  

 **Aggiornare le console di Configuration Manager autonome:** verificare che tutte le console di Configuration Manager remote siano aggiornate alla stessa versione. Viene chiesto di aggiornare una console quando:  

-   Si passa a un nuovo nodo in una console aperta  

-   Quando si apre la console  

**Riconfigurare le repliche di database per i punti di gestione nei siti primari:** se si usano le repliche di database per i punti di gestione nei siti primari, è necessario disinstallarle prima di aggiornare il sito. Dopo l'aggiornamento di un sito primario riconfigurare la replica di database per i punti di gestione. Per altre informazioni, vedere [Repliche di database per i punti di gestione per System Center Configuration Manager](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Riconfigurare le attività di manutenzione del database disabilitate prima dell'aggiornamento:** se le [Attività di manutenzione per System Center Configuration Manager](../../../core/servers/manage/maintenance-tasks.md) del database sono state disabilitate in un sito prima dell'aggiornamento, riconfigurare le attività nel sito usando le stesse impostazioni selezionate prima dell'aggiornamento.  

**Aggiornare i client:** per informazioni su come aggiornare i client esistenti e su come installare nuovi client, vedere [Come aggiornare i client per i computer Windows in System Center Configuration Manager](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)  

**Altre configurazioni:** rivedere le modifiche apportate prima di iniziare l'aggiornamento, quindi ripristinare le configurazioni nei siti e nella gerarchia.  

##  <a name="a-namebkmkoptionsa-enable-optional-features-from-updates"></a><a name="bkmk_options"></a> Abilitare le funzionalità facoltative degli aggiornamenti  
Quando si installa un aggiornamento che include una o più funzionalità facoltative, è possibile abilitare queste funzionalità nella gerarchia.  È possibile farlo durante l'installazione dell'aggiornamento o tornare nella console in un secondo momento e abilitare le funzionalità facoltative.

Per visualizzare le funzionalità disponibili e il relativo stato, nella console passare ad **Amministrazione** > **Servizi cloud** > **Aggiornamenti e manutenzione** > **Funzionalità**.

Quando una funzionalità non è facoltativa, viene installata automaticamente e non viene visualizzata nel nodo **Funzionalità** .  

##  <a name="a-namebkmkprereleasea-use-pre-release-features-from-updates"></a><a name="bkmk_prerelease"></a> Usare le funzionalità di versioni non definitive degli aggiornamenti
A partire dalla versione 1606, è necessario dare il consenso all'uso delle funzionalità di versioni non definitive in System Center Configuration Manager per poterle selezionare e abilitarne l'uso.  

Le funzionalità di versioni non definitive sono incluse nel prodotto a scopo di test preliminare in un ambiente di produzione, ma non devono essere considerate pronte per l'ambiente di produzione.

Per dare il consenso, nella console passare ad **Amministrazione** > **Configurazione del sito** > **Siti**, quindi selezionare **Impostazioni gerarchia**. Nella scheda **Generale** selezionare **Consenso a usare funzionalità di versioni non definitive**.
 -  L'azione di dare il consenso viene eseguita una sola volta per ogni gerarchia e non può essere annullata  
 -  Se non viene dato il consenso, non è possibile abilitare le nuove funzionalità di versioni non definitive incluse nell'aggiornamento 1606 o nelle versioni dell'aggiornamento successive

 > [!NOTE]
 > Se sono state abilitate nell'aggiornamento 1602 prima dell'installazione dell'aggiornamento 1606, le funzionalità di versioni non definitive rimangono abilitate dopo l'installazione dell'aggiornamento 1606 anche se non viene dato il consenso al loro utilizzo.

Se la gerarchia esegue la versione 1606 o una versione successiva e si installa un aggiornamento che include funzionalità di versioni non definitive, le funzionalità vengono visualizzate nella procedura guidata degli aggiornamenti e della manutenzione insieme alle normali funzionalità incluse nell'aggiornamento:
  - **Se è stato dato il consenso:** è possibile abilitare le funzionalità di versioni non definitive dall'interno della procedura guidata degli aggiornamenti e della manutenzione durante l'installazione dell'aggiornamento. A tale scopo, selezionare le funzionalità di versioni non definitive allo stesso modo in cui si selezionano le altre funzionalità.     

    Facoltativamente, è possibile abilitare una funzionalità di versione non definitiva successivamente dal nodo **Amministrazione** > **Servizi cloud** > **Aggiornamenti e manutenzione** > **Funzionalità** della console. A tale scopo, nel nodo Funzionalità selezionare la funzionalità e quindi fare clic su **Attiva**. L'opzione rimane disattivata o non disponibile fino a quando non si concede il consenso.  
  -   **Se non è stato dato il consenso:** durante l'installazione di un aggiornamento, le funzionalità di versioni non definitive sono visibili nella procedura guidata degli aggiornamenti e della manutenzione ma appaiono disattivate e non possono essere abilitate. Dopo l'installazione dell'aggiornamento, è possibile visualizzare le funzionalità nel nodo Funzionalità ma sarà possibile abilitarle solo dopo aver dato il consenso in Impostazioni gerarchia.

 > [!TIP]
 > Durante l'installazione dell'aggiornamento 1606, le funzionalità di versioni non definitive incluse nell'aggiornamento 1606 non sono visibili nella procedura guidata degli aggiornamenti e della manutenzione e non possono essere abilitate. Dopo l'installazione dell'aggiornamento 1606, è possibile visualizzare le funzionalità di versioni non definitive dell'aggiornamento nel nodo Funzionalità.

Se dopo aver concesso il consenso a un sito primario autonomo si espande la gerarchia installando un nuovo sito di amministrazione centrale, è necessario concedere di nuovo il consenso al sito di amministrazione centrale.

**Per la versione non definitiva sono disponibili le funzionalità seguenti:**

 |Funzionalità                    |Aggiunta come versione non definitiva |Aggiunta come funzionalità completa |  
|----------------------------|---------------------|------------------------|
| Microsoft Operations Management Suite (OMS) Connector  | [Versione 1606](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md) |![Non ancora](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
| Manutenzione di una raccolta compatibile con cluster (manutenzione di un gruppo di server)| [Versione 1602](../../../core/get-started/capabilities-in-technical-preview-1605.md#bkmk_servergroups)|![Non ancora](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)|
|Accesso condizionale per i PC gestiti da System Center Configuration Manager | [Versione 1602](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md)     |![Non ancora](media/83c5d168-8faf-4e8e-920b-528e3c43ffd4.gif)                        |




##  <a name="a-namebkmkservicewindowa-service-windows-for-site-servers"></a><a name="bkmk_ServiceWindow"></a> gli intervalli di servizio per i server del sito  
In un server del sito è possibile configurare gli intervalli di servizio per controllare quando è possibile applicare gli aggiornamenti dell'infrastruttura per Configuration Manager al server del sito.  Ogni server del sito supporta più intervalli e l'intervallo consentito per l'installazione degli aggiornamenti dell'infrastruttura viene determinato con una combinazione di tutti gli intervalli configurati per il server del sito.  

**Per configurare un intervallo di servizio:**  

1.  Nella console di Configuration Manager aprire **Amministrazione** > **Configurazione del sito** > **Siti** e quindi selezionare il server del sito in cui si vuole configurare un intervallo di servizio.  

2.  Successivamente, modificare le **Proprietà** del server del sito e selezionare la scheda **Intervallo di servizio** in cui è possibile impostare uno o più intervalli di servizio per il server del sito.  

##  <a name="a-namebkmkfaqa-why-dont-i-see-certain-updates-in-my-console"></a><a name="bkmk_faq"></a> Perché alcuni aggiornamenti non sono visualizzati nella console?  
 Se non viene trovato un aggiornamento specifico o se non viene visualizzato alcun aggiornamento nella console dopo una sincronizzazione riuscita con il servizio cloud Microsoft, la causa potrebbe essere:  

-   L'aggiornamento richiede una configurazione non usata dall'infrastruttura oppure la versione corrente del prodotto non soddisfa un prerequisito per la ricezione dell'aggiornamento.  

     Se si ritiene di avere le configurazioni necessarie o di soddisfare altri requisiti per un aggiornamento mancante, verificare che il punto di connessione del servizio sia in modalità online e quindi usare l'opzione **Controlla aggiornamenti** nel nodo Aggiornamenti e manutenzione per forzare un controllo.  In modalità offline è necessario usare lo strumento di connessione del servizio per sincronizzare manualmente il servizio cloud.  

-   L'account non ha le autorizzazioni corrette di amministrazione basata su ruoli per visualizzare gli aggiornamenti nella console di Configuration Manager.

    Per informazioni sulle autorizzazioni richieste per visualizzare gli aggiornamenti e abilitare le funzionalità dall'interno della console, vedere [Autorizzazioni per la gestione degli aggiornamenti](../../../core/servers/manage/install-in-console-updates.md#Permissions-to-view-and-manage-updates-and-features) in questo argomento.



<!--HONumber=Nov16_HO1-->



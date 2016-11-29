---
title: Distribuire applicazioni virtuali App-V | System Center Configuration Manager
description: Questo articolo descrive le considerazioni da tenere presenti quando si creano e distribuiscono applicazioni virtuali.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddcad9f2-a542-4079-83ca-007d7cb44995
caps.latest.revision: 11
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: d6e787d5968b281afe4e4b475287944563c8a77f


---
# <a name="deploy-app-v-virtual-applications-with-system-center-configuration-manager"></a>Distribuire applicazioni virtuali App-V con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Oltre agli altri requisiti e alle procedure di System Center Configuration Manager per la creazione di un'applicazione, quando si creano e si distribuiscono applicazioni virtuali è necessario tenere presente quanto segue.  

 Quando si usa Configuration Manager per gestire applicazioni virtuali, si ottengono i vantaggi seguenti:  

-   Usare un'infrastruttura di gestione singola  

-   Funzionalità di scalabilità, distribuzione e di distribuzione del contenuto, ad esempio raccolte e affinità utente-dispositivo  

-   Sfruttare le funzionalità avanzate di gestione di applicazioni offerte da Configuration Manager  

-   Usare le funzionalità di Configuration Manager, come distribuzione del sistema operativo, inventario software e hardware, misurazione del software e Asset Intelligence per il supporto delle applicazioni virtuali  

Per altre informazioni su come creare e sequenziare le applicazioni con App-V, vedere [Application Virtualization](https://technet.microsoft.com/library/cc843848.aspx) nella Libreria TechNet.  

Per distribuire applicazioni virtuali nei computer, occorre che il client di Configuration Manager e di App-V siano installati sui computer. I dispositivi client possono includere computer desktop e portatili, nonché i client Virtual Desktop Infrastructure (VDI). Il software client di Configuration Manager e quello di App-V collaborano per recapitare, individuare e avviare i pacchetti delle applicazioni virtuali. Il client di Configuration Manager gestisce il recapito dei pacchetti delle applicazioni virtuali al client App-V. Il client App-V esegue l'applicazione virtuale sul client.  

-   Per distribuire un'applicazione virtuale, è necessario innanzitutto creare l'applicazione virtuale usando App-V Application Virtualization Sequencer. Il Sequencer monitora il processo di installazione e configurazione per un'applicazione e registra le informazioni necessarie per eseguire l'applicazione in un ambiente virtuale. È inoltre possibile usare il Sequencer per configurare quali file e configurazioni applicare a tutti gli utenti e quali configurazioni possono essere personalizzate degli utenti.  

-   Quando si mette in sequenza un'applicazione, è necessario salvare il pacchetto in un percorso accessibile da Configuration Manager. È quindi possibile creare una distribuzione dell'applicazione che contiene l'applicazione virtuale.  

-   Configuration Manager non supporta l'uso della funzionalità di cache condivisa di sola lettura di App-V.  

-   Configuration Manager supporta la funzionalità di archivio dei contenuti condivisi in App-V 5.  

-   Quando si crea un tipo di distribuzione per un'applicazione virtuale, Configuration Manager crea il tipo di distribuzione usando i contenuti del file manifesto dell'applicazione. Si tratta di un file XML che contiene le informazioni sull'applicazione virtuale. Configuration Manager consente anche di creare i requisiti per il tipo di distribuzione in base al contenuto del file con estensione osd di App-V che include le informazioni sui sistemi operativi supportati per l'applicazione virtuale.  

-   Per distribuire applicazioni virtuali in Configuration Manager, nei computer client deve essere installato il client App-V 4.6 SP1 o una versione successiva.  

-   Inoltre, per distribuire applicazioni virtuali è necessario aggiornare il client App-V con l'aggiornamento rapido descritto nell'articolo [2645225](https://support.microsoft.com/kb/2645225)della Knowledge Base.  
  
-   Quando si usano i gruppi di connessione in Microsoft Application Virtualization 5.0, le applicazioni virtuali distribuite possono condividere lo stesso file system e lo stesso Registro di sistema nei computer client. A differenza delle applicazioni virtuali standard, queste applicazioni possono condividere dati con un'altra. Inoltre, i gruppi di connessione mantengono le impostazioni utente per le applicazioni che contengono. Gli ambienti virtuali App-V in Configuration Manager vengono usati per configurare gruppi di connessione nei computer client. Gli ambienti virtuali vengono creati o modificati nei computer client quando viene installata l'applicazione o quando i client valutano le applicazioni installate. È possibile ordinare queste applicazioni in modo che quando più applicazioni tentano di modificare un valore del Registro di sistema o di file system, la priorità viene assegnata all'applicazione con l'ordine più elevato. Per altre informazioni, vedere [Create App-V virtual environments](../../apps/deploy-use/create-app-v-virtual-environments.md) (Creare ambienti virtuali App-V).  

##  <a name="supported-app-v-versions"></a>Versioni supportate di App-V  
 Configuration Manager supporta le versioni seguenti di App-V:  

-   **App-V 4.6:** per usare le applicazioni virtuali in Configuration Manager, nei computer client deve essere installato il client di App-V 4.6 SP1, App-V 4.6 SP2 o App-V 4.6 SP3.  

     Inoltre, per poter distribuire correttamente le applicazioni virtuali, è necessario aggiornare il client App-V 4.6 SP1 con l'aggiornamento rapido descritto nell'articolo [2645225](http://go.microsoft.com/fwlink/p/?LinkId=237322) della Knowledge Base.  

-   **App-V 5, App-V 5.0 SP1, App-V 5.0 SP2, App-V 5.0 SP3, e App-V 5.1:** per App-V 5.0 SP2 è necessario installare il [pacchetto hotfix 5](https://support.microsoft.com/en-us/kb/2963211) oppure usare App-V 5.0 SP3.  

##  <a name="steps-to-manage-app-v-virtual-applications"></a>Passaggi per la gestione di applicazioni virtuali App-V  
 Per gestire applicazioni virtuali App-V, completare i passaggi seguenti:  

-   **Sequenziazione** : la sequenziazione è il processo di conversione di un'applicazione in un'applicazione virtuale usando il Sequencer App-V.  

-   **Creare raccolte di applicazioni di Configuration Manager**: usare la Creazione guidata tipo di distribuzione per importare l'applicazione sequenziata in un tipo di distribuzione di Configuration Manager che è poi possibile aggiungere a un'applicazione. È inoltre possibile creare ambienti virtuali che consentano la condivisione delle impostazioni da parte di più applicazioni virtuali.  

-   **Distribuzione**: la distribuzione è il processo per cui le applicazioni App-V vengono rese disponibili nei punti di distribuzione di Configuration Manager.  

-   **Distribuzione** : la distribuzione è il processo per cui l'applicazione viene resa disponibile nei computer client. Nell'infrastruttura App-V completa viene denominata "streaming". In Configuration Manager sono disponibili due opzioni per la distribuzione di applicazioni virtuali: **streaming** e **download ed esecuzione**.  

##  <a name="configuration-manager-virtual-application-delivery-methods"></a>Metodi di recapito delle applicazioni virtuali di Configuration Manager  
 Configuration Manager supporta due metodi per il recapito di applicazioni virtuali ai client, denominati recapito in streaming e recapito locale (dowload ed esecuzione):  

-   **Recapito in streaming**  

     Quando viene usato per gestire il client App-V, Configuration Manager supporta lo streaming di applicazioni virtuali tramite HTTP o HTTPS da un punto di distribuzione. Lo streaming tramite HTTP o HTTPS è abilitato per impostazione predefinita ed è configurato nella finestra di dialogo delle proprietà del punto di distribuzione. Quando si distribuisce un'applicazione virtuale nei computer client e un utente esegue l'applicazione virtuale, il client di Configuration Manager contatta un punto di gestione per determinare quale punto di distribuzione usare; quindi dal punto di distribuzione viene eseguito lo streaming dell'applicazione.  

-   **Recapito locale (download ed esecuzione)**  

     Quando si usa questo metodo di recapito, il client di Configuration Manager scarica per prima cosa l'intero pacchetto dell'applicazione virtuale nella cache del client di Configuration Manager, quindi dà istruzione al client App-V per lo streaming dell'applicazione dalla cache di Configuration Manager nella cache di App-V. Se si distribuisce un'applicazione virtuale nei computer client e il contenuto non si trova nella cache di App-V, il client App-V esegue lo streaming del contenuto dell'applicazione dalla cache del client di Configuration Manager nella cache App-V ed esegue l'applicazione. Dopo l'esecuzione corretta dell'applicazione, è possibile configurare il client di Configuration Manager per eliminare tutte le versioni precedenti del pacchetto nel ciclo di eliminazione successivo oppure mantenerle nella cache del client di Configuration Manager .  

 Quando si decide quale metodo di recapito delle applicazioni virtuali di Configuration Manager usare, confrontare il requisito per lo spazio su disco ridotto per il recapito in streaming con la disponibilità garantita di applicazioni App-V usando il recapito locale. L'aumento dello spazio su disco client richiesto per il recapito locale potrebbe essere preferibile al recapito in streaming in modo che gli utenti possano avere l'applicazione sempre a disposizione da qualsiasi posizione.  

 Usare le informazioni nella tabella seguente per scegliere il migliore metodo di recapito.  

 **Recapito in streaming**  

|Vantaggi|Svantaggi|  
|----------------|-------------------|  
|Questo metodo usa i protocolli di rete standard per lo streaming del contenuto del pacchetto dai punti di distribuzione.<br /><br /> I collegamenti ai programmi per le applicazioni virtuali richiedono una connessione al punto di distribuzione, in modo che il recapito dell'applicazione virtuale avvenga su richiesta.<br /><br /> Questo metodo funziona per i client con connessioni a banda larga ai punti di distribuzione.<br /><br /> Le applicazioni virtuali aggiornate distribuite in azienda sono disponibili poiché i client ricevono criteri che li informano che la versione corrente è stata sostituita e scaricano solo le modifiche dalla versione precedente.<br /><br /> Le autorizzazioni di accesso vengono definite nel punto di distribuzione per impedire agli utenti di accedere ad applicazioni o pacchetti non autorizzati.|Lo streaming delle applicazioni virtuali non viene eseguito fino a quando l'utente non esegue l'applicazione per la prima volta. In questo scenario, un utente potrebbe ricevere dei collegamenti ai programmi per le applicazioni virtuali e poi scollegarsi dalla rete prima di eseguire le applicazioni virtuali per la prima volta. Se l'utente tenta di eseguire l'applicazione virtuale mentre il client non è in linea, viene visualizzato un errore e l'utente non potrà eseguire l'applicazione virtualizzata perché un punto di distribuzione di Configuration Manager non è disponibile per lo streaming dell'applicazione. L'applicazione non sarà disponibile fino a quando l'utente non si riconnette alla rete e non esegue l'applicazione.<br /><br /> Per evitarlo, è possibile usare il metodo di recapito locale per il recapito dell'applicazione virtuale ai client oppure abilitare la gestione client basata su Internet per il recapito in streaming.|  

 **Recapito locale**  

|Vantaggi|Svantaggi|  
|----------------|-------------------|  
|La funzionalità del punto di distribuzione standard viene usata per scaricare il pacchetto tramite il Servizio trasferimento intelligente in background (BITS).<br /><br /> I contenuti del pacchetto dell'applicazione virtuale vengono recapitati in locale al client, il che significa che il utenti possono eseguirli quando il computer non è connesso alla rete.<br /><br /> Questo metodo è adatto per le connessioni di rete lente o inaffidabili e per i computer che si connettono solo occasionalmente alla rete.<br /><br /> Configuration Manager usa la compressione differenziale remota (RDC) per inviare ai client solo i byte all'interno dei file che sono stati modificati quando è stato aggiornato il contenuto del pacchetto dell'applicazione virtuale. Il client di Configuration Manager usa la RDC per costruire una nuova versione del pacchetto di un'applicazione virtuale sulla base della versione corrente del pacchetto e di tutte le modifiche inviate al client.<br /><br /> Questo metodo fornisce flessibilità di applicazione per gli utenti mobili o per gli utenti scollegati. Gli amministratori possono scegliere di mantenere il pacchetto nella cache di Configuration Manager dopo il recapito se l'applicazione virtuale è stata distribuita con un'azione di installazione. Il pacchetto nella cache del client di Configuration Manager serve come origine streaming locale e affidabile al client App-V per portare il pacchetto nella propria cache.|Quando l'applicazione virtuale viene mantenuta nella cache di Configuration Manager, sul client è necessario spazio su disco pari a fino il doppio delle dimensioni del pacchetto dell'applicazione virtuale.|  

 È possibile inoltre preinstallare le applicazioni virtuali su un computer e quindi creare un'immagine di tale computer per la distribuzione in altri computer. Tuttavia, se il pacchetto dell'applicazione virtuale è stato creato in un sito differente, la replica delle differenze binarie non verrà usata per scaricare gli aggiornamenti all'applicazione. Questa opzione può essere utile in un'infrastruttura desktop virtuale quando si desidera che le applicazioni siano immediatamente disponibili invece di scaricarle dopo l'accesso dell'utente.  

##  <a name="migrating-from-an-app-v-infrastructure-to-a-configuration-manager-and-app-v-infrastructure"></a>Migrazione da un'infrastruttura App-V a un'infrastruttura Configuration Manager e App-V  
 Usare la tabella seguente per pianificare una migrazione da un'infrastruttura App-V esistente alla gestione di un'applicazione virtuale con Configuration Manager.  

|Passaggio|Altre informazioni|  
|----------|----------------------|  
|Esaminare le applicazioni virtuali correnti per scegliere le applicazioni di cui si intende effettuare la migrazione nell'infrastruttura di Configuration Manager.|Nessuna informazione aggiuntiva.|  
|Valutare gli utenti e i dispositivi in cui verranno distribuite le applicazioni virtuali.|Creare raccolte di Configuration Manager per raggruppare utenti e dispositivi ai quali si vogliono distribuire le applicazioni virtuali. Per altre informazioni, vedere [Introduction to Collections](/sccm/core/clients/manage/collections/introduction-to-collections) (Introduzione alle raccolte).|  
|Eseguire la migrazione dei gruppi di connessione di App-V 5 negli ambienti virtuali di Configuration Manager.|Per altre informazioni, vedere la sezione [Eseguire la migrazione dei gruppi di connessione di App-V 5 negli ambienti virtuali di Configuration Manager](/sccm/apps/get-started/deploying-app-v-virtual-applications#migrate-app-v-5-connection-groups-to-configuration-manager-virtual-environments) in questo argomento.|  
|Analizzare e scoprire se una delle applicazioni virtuali esiste come applicazione completa nell'infrastruttura di Configuration Manager.|Per una gestione più semplice, è possibile aggiungere l'applicazione virtuale come nuovo tipo di distribuzione all'applicazione completa esistente. Per altre informazioni su come creare i tipi di distribuzione, vedere [Create applications](../../apps/deploy-use/create-applications.md) (Creare applicazioni).|  
|Creare applicazioni per sostituire i pacchetti App-V esistenti.|Per altre informazioni su come creare applicazioni di Configuration Manager, vedere [Introduction to application management](/sccm/apps/understand/introduction-to-application-management) (Introduzione alla gestione delle applicazioni) e [Create applications](../../apps/deploy-use/create-applications.md) (Creare applicazioni).|  
|Configuration Manager comincia a gestire applicazioni virtuali su un client dopo la prima distribuzione di un'applicazione virtuale. Successivamente, tutte le applicazioni App-V nel computer devono essere gestite da Configuration Manager.|Nessuna informazione aggiuntiva.|  
|Distribuire il contenuto nei punti di distribuzione appropriati per consentire il recapito locale delle applicazioni.|Per altre informazioni, vedere [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Gestire il contenuto e l'infrastruttura del contenuto).|  
|Distribuire l'applicazione ai client di Configuration Manager.<br /><br /> Se l'applicazione App-V è stata creata con una versione precedente del Sequencer che non crea un file XML manifesto, è possibile aprirla e salvarla in una versione più recente del Sequencer per creare il file. Questo file è necessario per distribuire le applicazioni virtuali con Configuration Manager.<br /><br /> App-V supporta i pacchetti di applicazioni virtuali creati con SoftGrid 4.1 SP1 o le versioni 4.2 del sequencer.<br /><br /> Se le applicazioni sono state precedentemente installate in locale, è necessario disinstallarle prima di distribuire una versione virtuale dell'applicazione.|Per altre informazioni, vedere [Deploy applications](../../apps/deploy-use/deploy-applications.md) (Distribuire applicazioni).|  
|System Center Configuration Manager non supporta più l'uso di pacchetti e programmi che contengono applicazioni virtuali. Quando esegue la migrazione da Configuration Manager 2007 a System Center Configuration Manager, Configuration Manager converte questi pacchetti in applicazioni.<br /><br /> Gli annunci di Configuration Manager 2007 vengono convertiti nei tipi di distribuzione seguenti:<br /><br /> - Migrazione dei pacchetti App-V senza annunci: un tipo di distribuzione che usa le impostazioni predefinite per il tipo di distribuzione.<br /><br /> - Migrazione dei pacchetti App-V con un annuncio: un tipo di distribuzione che usa le stesse impostazioni dell'annuncio di <br />                Configuration Manager 2007.<br /><br /> - Migrazione di pacchetti App-V con più annunci: un tipo di distribuzione per ogni <br />                annuncio di Configuration Manager 2007 che usa le impostazioni per tale annuncio.|Per altre informazioni, vedere [Planning for the migration of Configuration Manager objects to System Center Configuration Manager](../../core/migration/planning-for-the-migration-of-objects.md) (Pianificazione della migrazione di oggetti di Configuration Manager a System Center Configuration Manager).|  

##  <a name="migrate-app-v-5-connection-groups-to-configuration-manager-virtual-environments"></a>Eseguire la migrazione dei gruppi di connessione di App-V 5 negli ambienti virtuali di Configuration Manager  
 Gli ambienti virtuali App-V in Configuration Manager consentono alle applicazioni virtuali distribuite di condividere lo stesso file system e Registro di sistema nei computer client. Ciò significa che, a differenza delle applicazioni virtuali standard, queste applicazioni possono condividere dati tra loro. Gli ambienti virtuali vengono creati o modificati nei computer client quando viene installata l'applicazione o quando i client valutano le applicazioni installate. Gli ambienti virtuali sono simili ai gruppi di connessione in App-V 5 autonoma.  

 Quando si esegue la migrazione dei gruppi di connessione da App-V 5 autonoma negli ambienti virtuali di Configuration Manager, è necessario assicurarsi che i gruppi di connessione già esistenti sui computer client siano gestiti correttamente da Configuration Manager e che venga mantenuto l'ambiente dell'utente all'interno di tali gruppi di connessione.  

 Usare la procedura seguente per facilitare la conversione dei gruppi di connessione App-V 5 in ambienti virtuali di Configuration Manager.  
  
### <a name="convert-app-v-5-connection-groups-to-configuration-manager-virtual-environments"></a>Convertire i gruppi di connessione App-V 5 in ambienti virtuali di Configuration Manager  
  
1.  Creare applicazioni di Configuration Manager per tutte le applicazioni esistenti in App-V.  

2.  Distribuire tali applicazioni a utenti o dispositivi con scopo della distribuzione **Richiesto**. Le distribuzioni agli utenti vanno rivolte agli stessi utenti che usavano l'applicazione in App-V e le distribuzioni ai computer vanno rivolte agli stessi computer che avevano l'applicazione in App-V.  

3.  Dopo aver completato la distribuzione, creare ambienti virtuali che corrispondano ai gruppi di connessione pubblicati nella versione autonoma di App-V. L'ambiente virtuale deve contenere gli stessi pacchetti, in particolare, i tipi di distribuzione di App-V 5, nello stesso ordine.  

Per informazioni su come creare un ambiente virtuale App-V, vedere [How to create App-V virtual environments](../../apps/deploy-use/create-app-v-virtual-environments.md) (Come creare ambienti virtuali App V).  

In alternativa è possibile eliminare tutti i gruppi di connessione dal client App-V prima di iniziare la distribuzione delle applicazioni con Configuration Manager. Tutte le impostazioni salvate dagli utenti nei gruppi di connessione App-V andranno però perse.  

##  <a name="dynamic-suite-composition-in-app-v-46"></a>Dynamic Suite Composition in App-V 4.6  
 Dynamic Suite Composition è una funzionalità che consente di definire un pacchetto applicazione virtuale come avente una dipendenza da un altro pacchetto applicazione virtuale. Quando l'applicazione viene eseguita, il client App-V ospita il pacchetto primario e quello dipendente nello stesso ambiente virtuale destinato all'applicazione.  

 Per usare questa funzionalità con Configuration Manager, è necessario che entrambi i pacchetti siano distribuiti e registrati con il client App-V. Per assicurare che il contenuto del pacchetto dipendente sia ospitato localmente nel computer client, configurare la distribuzione dell'applicazione per il recapito locale (download ed esecuzione).  

 Per altre informazioni sulla funzionalità Dynamic Suite Composition di App-V, vedere la documentazione di App-V.  

##  <a name="convert-app-v-46-applications-to-app-v-5-applications"></a>Conversione di applicazioni App-V 4.6 in applicazioni App-V 5  
 Il formato relativo al pacchetto dell'applicazione è stato modificato tra App-V 4.6 e App-V 5. Le applicazioni sequenziate da App-V 4.6 non sono più supportate. App-V 5 include comunque uno strumento di conversione pacchetti che può essere usato per convertire le applicazioni. Per altre informazioni, vedere la [documentazione di App-V 5](http://technet.microsoft.com/library/jj713472.aspx).  

 Per convertire le applicazioni App-V 4.6 in applicazioni App-V 5, attenersi alla procedura seguente:  

1.  Convertire o ri-sequenziare i pacchetti App-V 4.6 nel formato App-V 5.  

2.  Distribuire il client App-V 5 ai computer della gerarchia.  

3.  Creare nuove applicazioni contenenti tipi di distribuzione per le applicazioni App-V 5 e creare le regole di sostituzione per sostituire le applicazioni App-V 4.6.  

4.  Creare i necessari ambienti virtuali.  

5.  Distribuire le nuove applicazioni App-V 5 ai computer.  

##  <a name="user-and-deployment-configuration-files"></a>File di configurazione dell'utente e della distribuzione  
 I file di configurazione dell'utente e della distribuzione contengono impostazioni che controllano il comportamento di un'applicazione. È possibile usare tali file per modificare le impostazioni dell'applicazione senza ri-sequenziarla.  

 Una tipica applicazione App-V 5 potrebbe contenere i seguenti file:  

-   Un file di pacchetto applicazione (.appv).  

-   Un file di configurazione dell'utente.  

-   Un file di configurazione della distribuzione.  

 Il file di configurazione dell'utente contiene impostazioni che si applicano solo all'utente connesso. È ad esempio possibile modificare i file di configurazione per modificare le informazioni sul collegamento all'applicazione da distribuire agli utenti. È anche possibile creare un'applicazione Configuration Manager con più tipi di distribuzione, ognuna contenente un file di configurazione utente diverso e regole requisiti tali da assicurarne l'installazione agli utenti desiderati.  

 Il file di configurazione della distribuzione contiene le impostazioni relative al computer, ad esempio le impostazioni del Registro di sistema. Il file può contenere anche impostazioni utente, che verranno applicate a tutti gli utenti.  

 Se si intende distribuire applicazioni virtuali App-V 5 con Configuration Manager, questi tre file dovranno essere presenti nella stessa cartella quando si crea il tipo di distribuzione App-V 5. Se la cartella contiene più file, Configuration Manager userà il più recente.  

 Per altre informazioni, vedere la [documentazione di App-V 5](http://technet.microsoft.com/library/jj713466.aspx).  

##  <a name="app-v-local-interaction"></a>Interazione locale di App-V  
 In alcuni scenari di distribuzione applicazioni alcune applicazioni vengono installate localmente nei computer client e altre applicazioni vengono distribuite come applicazioni virtuali negli stessi computer client. Per impostazione predefinita, le applicazioni installate localmente non possono vedere o comunicare direttamente con le applicazioni virtualizzate. Questo è il comportamento previsto da App-V per l'isolamento delle applicazioni. L'interazione locale è una funzionalità del client App-V che può essere abilitata per consentire alle applicazioni installate localmente in esecuzione in un computer client di vedere e comunicare con le applicazioni virtualizzate. Configuration Manager e App-V offrono il pieno supporto dell'interazione locale.  

 Per altre informazioni sulla funzionalità di interazione locale di App-V, vedere la documentazione di App-V.  

##  <a name="app-v-5-shared-content-store"></a>Archivio contenuti condivisi di App-V 5  
 La modalità SCS (Shared Content Store) di App-V 5 è supportata da Configuration Manager. Per altre informazioni, vedere la pagina relativa alla [pianificazione per Shared Content Store (SCS) di App-V 5.0](http://technet.microsoft.com/library/jj713431.aspx).  

##  <a name="monitor-virtual-applications"></a>Monitoraggio di applicazioni virtuali  

### <a name="virtual-application-reports"></a>Report di applicazioni virtuali  
 È possibile usare i report seguenti per monitorare App-V nell'ambiente Configuration Manager:  

|Nome report|Descrizione|  
|-----------------|-----------------|  
|Risultati ambiente virtuale App-V|Visualizza informazioni su un ambiente virtuale selezionato che si trova in uno stato specificato per una raccolta selezionata (solo App-V 5).|  
|Risultati ambiente virtuale App-V per asset|Visualizza informazioni su un ambiente virtuale selezionato per un asset specificato e qualsiasi tipo di distribuzione per l'ambiente virtuale selezionato (solo App-V 5).|  
|Stato ambiente virtuale App-V|Visualizza informazioni di conformità per un ambiente virtuale selezionato per una raccolta selezionata. La colonna **Permanenza** di questo report riporta gli asset in cui un ambiente virtuale precedentemente configurato non è più applicabile, ma viene conservato per mantenere le impostazioni utente nelle applicazioni eseguite nell'ambiente virtuale (solo App-V 5).|  
|Computer con un'applicazione virtuale specifica|Visualizza il riepilogo dei computer che dispongono del collegamento App-V specificato creato da Application Virtualization Management Sequencer (solo App-V 4.6).|  
|Computer con un pacchetto applicazione virtuale specifico|Visualizza l'elenco dei computer in cui è installato il pacchetto applicazione App-V specificato (solo App-V 4.6).|  
|Conteggio di tutte le istanze dei pacchetti di applicazioni virtuali|Visualizza il conteggio di tutti i pacchetti applicazioni App-V rilevati (solo App-V 4.6).|  
|Conteggio di tutte le istanze delle applicazioni virtuali|Visualizza il conteggio di tutte le applicazioni App-V rilevate (solo App-V 4.6).|  

## <a name="log-files"></a>File di registro  
 Configuration Manager registra le informazioni sulla distribuzione di applicazioni virtuali nei file di log. Per informazioni sui file di log che vengono usati da applicazioni virtuali e la gestione di applicazioni di Configuration Manager, vedere [Log files in System Center Configuration Manager](../../core/plan-design/hierarchy/log-files.md) (File di log in System Center Configuration Manager).  

 È inoltre possibile trovare log dei client App-V nei percorsi seguenti:  

-   Windows Vista, Windows 7 e Windows 8: **C:\ProgramData\Microsoft\Application Virtualization Client**  



<!--HONumber=Nov16_HO1-->



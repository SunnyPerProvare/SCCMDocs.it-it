---
title: Introduzione | System Center Configuration Manager
description: Informazioni di base come introduzione a System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
caps.latest.revision: 16
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 46aa1fdf49dcdacb9d5e53963a0f799e5f0a1754


---
# <a name="introduction-to-system-center-configuration-manager"></a>Introduzione a System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Come membro della suite di soluzioni di gestione Microsoft System Center, System Center Configuration Manager può essere utile nella gestione di dispositivi e utenti sia in locale che nel cloud.  

**Configuration Manager può essere utile per:**   
-   Aumentare l'efficienza e la produttività IT riducendo le attività manuali e consentendo di concentrarsi sui progetti di alto valore  
-   Ottimizzare gli investimenti hardware e software  
-   Incrementare la produttività degli utenti finali fornendo il software più adatto al momento giusto  

**Configuration Manager consente di offrire servizi IT più efficienti grazie all'abilitazione di:**  

-   Distribuzione software sicura e scalabile  
-   Gestione delle impostazioni di conformità  
-   Gestione completa delle risorse di server, desktop, computer portatili e dispositivi mobili.  

**Configuration Manager estende soluzioni e tecnologie Microsoft esistenti e si integra con esse.**  

Ad esempio, Configuration Manager si integra con:  

-   Microsoft Intune per gestire un'ampia gamma di piattaforme per dispositivi mobili  
-   Windows Server Update Services (WSUS) per gestire gli aggiornamenti software  
-   Servizi certificati  
-   Exchange Server e Exchange Online  
-   Criteri di gruppo di Windows
-   DNS   
-   Windows Automated Deployment Kit (Windows ADK) e Utilità di migrazione stato utente (USMT)  
-   Servizi di distribuzione Windows (WDS)  
-   Desktop remoto e Assistenza remota  

Configuration Manager usa anche:  

-   Servizi di dominio Active Directory per la sicurezza, la posizione del servizio, la configurazione e l'individuazione degli utenti e dei dispositivi da gestire.  
-   Microsoft SQL Server come database di gestione delle modifiche distribuito e si integra con SQL Server Reporting Services (SSRS) per generare report per monitorare e tenere traccia delle attività di gestione.  
-   I ruoli del sistema del sito che estendono le funzionalità di gestione e usano i servizi Web di Internet Information Services (IIS).  
-   Servizio trasferimento intelligente in background (BITS) e BranchCache per semplificare la gestione della larghezza di banda di rete disponibile.  

 Per il corretto funzionamento di Configuration Manager è necessario, prima di impiegarlo in un ambiente di produzione, pianificarne e testarne attentamente le funzionalità di gestione. Essendo un'applicazione di gestione avanzata, Configuration Manager ha la capacità di influire su ogni computer dell'organizzazione. Se lo si distribuisce e lo si gestisce con un'attenta pianificazione e tenendo in considerazione i requisiti aziendali, Configuration Manager consente di ridurre il carico amministrativo e il costo totale di proprietà.  

 Usare gli argomenti seguenti e le sezioni aggiuntive in questo argomento per altre informazioni su Configuration Manager:  


**Argomenti correlati in questa libreria della documentazione:**  

-   [Features and capabilities of System Center Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md) (Caratteristiche e funzionalità di System Center Configuration Manager)  
-   [Choose a device management solution for System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md) (Scegliere una soluzione di gestione dei dispositivi per System Center Configuration Manager)  
-   [What's changed in System Center Configuration Manager from System Center 2012 Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md) (Novità in System Center Configuration Manager rispetto a System Center Configuration Manager 2012)
-   [Fundamentals of System Center Configuration Manager](../../core/understand/fundamentals.md) (Nozioni fondamentali su System Center Configuration Manager)  
-   [Evaluate System Center Configuration Manager by building your own lab environment](/sccm/core/get-started/set-up-your-lab) (Valutare System Center Configuration Manager creando un proprio ambiente lab)
-   [Find help for using System Center Configuration Manager](../../core/understand/find-help.md) (Reperire informazioni sull'uso di System Center Configuration Manager)  
-   [Removed and deprecated features for System Center Configuration Manager](../../core/plan-design/changes/removed-and-deprecated-features.md) (Funzionalità rimosse e deprecate per System Center Configuration Manager)  

##  <a name="a-namebkmkconsolea-the-configuration-manager-console"></a><a name="BKMK_Console"></a> Console di Configuration Manager  
 Dopo aver installato Configuration Manager usare la console di Configuration Manager per configurare siti e client e per eseguire e monitorare le attività di gestione. Questa console è il principale punto di amministrazione e consente di gestire più siti.  

 È possibile usare la console per eseguire console secondarie per supportare le attività di gestione client specifiche, ad esempio:  

-   **Esplora inventario risorse**: per visualizzare le informazioni sull'inventario hardware e software.  
-   **Controllo remoto**: per connettersi in modalità remota a un computer client per eseguire attività di risoluzione dei problemi.  

 È possibile installare la console di Configuration Manager in altri computer e limitare l'accesso e la visualizzazione degli elementi della console da parte degli utenti amministratori usando l'amministrazione basata su ruoli di Configuration Manager.  

 Per altre informazioni, vedere [Install System Center Configuration Manager consoles](../../core/servers/deploy/install/install-consoles.md) (Installare console di System Center Configuration Manager).

##  <a name="a-namebkmkapplicationcataloga-the-application-catalog-software-center-and-the-company-portal"></a><a name="BKMK_ApplicationCatalog"></a> Catalogo applicazioni, Software Center e portale aziendale  
 Il **Catalogo applicazioni** è un sito Web dove gli utenti possono cercare e richiedere il software per i PC Windows. Per utilizzare il Catalogo applicazioni, è necessario installare il punto per servizi Web del Catalogo applicazioni e il punto per siti Web del Catalogo applicazioni per il sito.  

 **Software Center** è un'applicazione installata quando il client di Configuration Manager viene installato in computer basati su Windows. Gli utenti eseguono questa applicazione per richiedere software e gestire il software distribuito usando Configuration Manager. Software Center consente agli utenti di eseguire le operazioni seguenti:  

-   Cercare e installare il software dal Catalogo applicazioni  
-   Visualizzare la cronologia delle richieste di software.  
-   Specificare quando Configuration Manager è in grado di installare il software nei dispositivi  
-   Configurare le impostazioni di accesso per il controllo remoto, se un utente amministratore ha abilitato il controllo remoto  

 Il **portale aziendale** è un'app o un sito Web che offre funzioni simili al Catalogo applicazioni per dispositivi mobili registrati da Windows Intune  

 Per altre informazioni, vedere l'argomento [Introduzione alla gestione delle applicazioni in System Center Configuration Manager](../../apps/understand/introduction-to-application-management.md).  

###  <a name="a-namebkmkclienta-configuration-manager-properties-on-windows-pcs"></a><a name="BKMK_Client"></a> Proprietà di Configuration Manager (in PC Windows)  
 Quando il client di Configuration Manager è installato in computer Windows, Configuration Manager viene installato nel Pannello di controllo. Non è in genere necessario configurare questa applicazione perché la configurazione client viene eseguita nella console di Configuration Manager. Questa applicazione consente agli utenti amministratori e al supporto tecnico di risolvere i problemi relativi ai singoli client.  

 Per altre informazioni sulla distribuzione dei client, vedere [Metodi di installazione client in System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md).  

##  <a name="a-namebkmkexamplescenariosa-example-scenarios-for-configuration-manager"></a><a name="BKMK_ExampleScenarios"></a> Scenari di esempio per Configuration Manager  
 Gli scenari di esempio seguenti illustrano in che modo una società denominata Trey Research usa Configuration Manager per consentire agli utenti di:  

-   Aumentare la produttività  
-   Unificare la gestione della conformità nei dispositivi per un'esperienza di amministrazione semplificata  
-   Semplificare la gestione dei dispositivi per ridurre i costi operativi IT  

 In tutti gli scenari, Davide è l'amministratore principale di Configuration Manager.  

###  <a name="a-namebkmkscenarioempowera-example-scenario-empower-users-by-ensuring-access-to-applications-from-any-device"></a><a name="BKMK_ScenarioEmpower"></a> Scenario di esempio: consentire agli utenti di ottenere l'accesso alle applicazioni da qualsiasi dispositivo  
 Trey Research desidera che i dipendenti abbiano accesso alle applicazioni necessarie nel modo più efficiente possibile. Davide esegue il mapping di questi requisiti aziendali agli scenari seguenti:  

|Requisito|Stato corrente della gestione client|Stato futuro della gestione client|  
|-----------------|-------------------------------------|------------------------------------|  
|I nuovi dipendenti possono lavorare in modo efficiente dal primo giorno.|Quando i dipendenti entrano nella società, devono attendere che le applicazioni vengano installate dopo il primo accesso.|Quando i dipendenti entrano nella società, effettuano l'accesso e le applicazioni vengono installate e sono pronte per l'utilizzo.|  
|I dipendenti possono richiedere rapidamente e facilmente il software aggiuntivo necessario.|Quando i dipendenti richiedono applicazioni aggiuntive, inviano un ticket al supporto tecnico e quindi attendono in genere due giorni prima che il ticket venga elaborato e le applicazioni installate.|Quando i dipendenti hanno bisogno di applicazioni aggiuntive, possono richiederle a un sito Web. Le applicazioni vengono installate immediatamente se non sono previste restrizioni di licenza. Se esistono restrizioni di licenza, gli utenti devono richiedere l'approvazione prima di installare l'applicazione.<br /><br /> Il sito Web mostra agli utenti solo le applicazioni che sono autorizzati a installare.|  
|I dipendenti possono usare i propri dispositivi portatili sul lavoro, se i dispositivi sono conformi ai criteri di sicurezza monitorati e applicati.<br /><br /> Questi criteri includono l'applicazione di una password complessa, il blocco di un dispositivo dopo un periodo di inattività e la cancellazione remota dei dispositivi smarriti o rubati.|I dipendenti connettono i propri dispositivi mobili a Exchange Server per il servizio di posta elettronica, ma non è possibile sapere con assoluta certezza se siano conformi ai criteri di sicurezza predefiniti specificati in Criteri cassetta postale di Exchange ActiveSync. È possibile che l'utilizzo personale di dispositivi mobili venga vietato a meno che l'IT non sia in grado di confermare l'adesione ai criteri.|L'organizzazione IT può segnalare la conformità di protezione dei dispositivi mobili con le impostazioni necessarie. Questa conferma consente agli utenti di continuare a usare il dispositivo mobile sul lavoro. Gli utenti possono cancellare il dispositivo mobile in modalità remota se viene smarrito o rubato e il supporto tecnico può cancellare il dispositivo mobile di qualsiasi utente se segnalato come smarrito o rubato.<br /><br /> Prevedere la registrazione dei dispositivi mobili in un ambiente PKI per una maggiore sicurezza e un maggior controllo.|  
|I dipendenti possono essere produttivi anche se non si trovano alla propria scrivania.|Quando i dipendenti non sono alla scrivania e non dispongono di computer portatili, non possono accedere alle applicazioni usando i computer pubblici disponibili nella società.|I dipendenti possono usare i computer pubblici per accedere ai dati e alle applicazioni.|  
|In genere, la continuità aziendale ha la precedenza sull'installazione delle applicazioni e degli aggiornamenti software necessari.|Le applicazioni e gli aggiornamenti software necessari vengono installati durante il giorno interrompendo spesso il lavoro degli utenti perché i computer rallentano o vengono riavviati durante l'installazione.|Gli utenti possono configurare l'orario lavorativo per evitare che il software necessario venga installato mentre usano il computer.|  

 Per soddisfare i requisiti, Davide usa le funzionalità di gestione e le opzioni di configurazione di Configuration Manager seguenti:  

-   Gestione delle applicazioni  
-   Gestione dispositivi mobili  

 L'implementazione viene eseguita tramite la procedura di configurazione illustrata nella tabella seguente.  

|Procedura di configurazione|Risultato|  
|-------------------------|-------------|  
|Davide verifica che i nuovi utenti dispongano di account utente in Active Directory e crea una nuova raccolta basata su query in Configuration Manager per questi utenti. Quindi definisce l'affinità utente dispositivo per questi utenti creando un file che associa gli account utente ai computer primari che utilizzeranno e importa il file in Configuration Manager.<br /><br /> Le applicazioni che i nuovi utenti devono avere sono già state create in Configuration Manager. Distribuisce quindi queste applicazioni con lo scopo di Richiesto nella raccolta che contiene i nuovi utenti.|Per le informazioni di affinità utente dispositivo, le applicazioni vengono installate per i computer primari di ogni utente prima che l'utente esegua l'accesso.<br /><br /> Le applicazioni sono pronte all'uso non appena l'utente esegue l'accesso.|  
|Davide installa e configura i ruoli del sistema del sito Catalogo applicazioni in modo che gli utenti possano cercare applicazioni da installare. Crea le distribuzioni delle applicazioni che hanno lo scopo di Disponibile e quindi distribuisce le applicazioni nella raccolta che contiene i nuovi utenti.<br /><br /> Per le applicazioni che dispongono di un numero limitato di licenze, Davide configura le applicazioni per richiedere l'approvazione.|Configurando le applicazioni come disponibili agli utenti e usando il Catalogo applicazioni, gli utenti ora possono cercare le applicazioni che possono installare. Gli utenti possono installare le applicazioni subito o richiedere l'approvazione e tornare al Catalogo applicazioni per installarle dopo aver ricevuto l'approvazione del supporto tecnico.|  
|Davide crea un connettore Exchange Server in Configuration Manager per gestire i dispositivi mobili che si connettono al server Exchange Server aziendale locale. Configura il connettore con le impostazioni di protezione che includono i requisiti per una password complessa e bloccano il dispositivo mobile dopo un periodo di inattività.<br /><br /> Per la gestione aggiuntiva di dispositivi che eseguono Windows Phone 8, Windows RT e iOS, Davide ottiene una sottoscrizione Microsoft Intune e quindi installa il ruolo del sistema del sito del punto di connessione del servizio. Questa soluzione di gestione dei dispositivi mobile offre alla società un maggiore supporto di gestione per questi dispositivi. Ad esempio, la possibilità data agli utenti di installare le applicazioni su questi dispositivi e la gestione completa delle impostazioni. La connessione per i dispositivi mobili, poi, viene protetta mediante certificati PKI creati automaticamente e distribuiti da Intune. Dopo aver configurato il punto di connessione del servizio e la sottoscrizione per l'uso con Configuration Manager, Davide invia un messaggio di posta elettronica agli utenti proprietari dei dispositivi mobili interessati perché facciano clic su un collegamento per avviare il processo di registrazione.<br /><br /> Affinché i dispositivi mobili possano essere registrati da Microsoft Intune, Davide usa le impostazioni di conformità per configurare le impostazioni di protezione per i dispositivi mobili. Queste impostazioni includono la necessità di configurare una password complessa e bloccare il dispositivo mobile dopo un periodo di inattività.|Con queste due soluzioni per la gestione dei dispositivi mobili, l'organizzazione IT ora può fornire informazioni sulla creazione di report dei dispositivi mobili usati nella rete aziendale e la relativa conformità alle impostazioni di protezione configurate.<br /><br /> Agli utenti viene ora mostrato come cancellare da remoto il dispositivo mobile usando il Catalogo applicazioni o il portale società in caso di perdita o furto del dispositivo mobile. Al supporto tecnico viene anche indicato come cancellare da remoto un dispositivo mobile per gli utenti usando la console di Configuration Manager.<br /><br /> Per i dispositivi mobili registrati da Microsoft Intune, Davide ora può anche distribuire le applicazioni mobili in modo che possano essere installate dagli utenti, raccogliere più dati di inventario dai dispositivi e disporre di maggiore controllo della gestione di questi dispositivi grazie alla possibilità di accedere a più impostazioni.|  
|Trey Research dispone di diversi computer pubblici usati dai dipendenti in visita in ufficio. I dipendenti avere le loro applicazioni disponibili ovunque eseguono l'accesso. Tuttavia, Davide non desidera installare localmente tutte le applicazioni su ogni computer.<br /><br /> A tale scopo, Davide crea le applicazioni richieste con due tipi di distribuzione:<br /><br /> **Primo**: un'installazione locale completa dell'applicazione, con il requisito di poter essere installata solo sul dispositivo primario dell'utente.<br /><br /> **Secondo**: una versione virtuale dell'applicazione, con il requisito di non dover essere installata sul dispositivo primario dell'utente.|Gli utenti in visita accedono a un computer pubblico e visualizzano le applicazioni necessarie come icone sul desktop di tale computer. L'applicazione viene eseguita in streaming come un'applicazione virtuale. In questo modo, possono essere produttivi come se fossero seduti alla propria scrivania.|  
|Davide fa sapere agli utenti che possono configurare le loro ore di lavoro in Software Center e selezionare le opzioni per evitare le attività di distribuzione software durante questo periodo di tempo e quando il computer è in modalità presentazione.|Poiché gli utenti possono controllare quando Configuration Manager distribuisce software nei loro computer, gli utenti rimangono più produttivi durante le ore lavorative.|  

 Questi passaggi di configurazione e i relativi risultati consentono a Trey Research di aumentare la produttività dei dipendenti garantendo l'accesso alle applicazioni da qualsiasi dispositivo.  

###  <a name="a-namebkmkscenariounifya-example-scenario-unify-compliance-management-for-devices"></a><a name="BKMK_ScenarioUnify"></a> Scenario di esempio: unificare la gestione della conformità per i dispositivi  
 Trey Research vuole una soluzione di gestione client unificata che assicuri che nei computer sia in esecuzione un software antivirus che viene aggiornato automaticamente. Ovvero:  

-   Windows Firewall è abilitato  
-   Gli aggiornamenti software critici sono installati  
-   Sono impostate specifiche chiavi del Registro di sistema  
-   I dispositivi mobili gestiti non possono installare o eseguire applicazioni non firmate  

 Inoltre, la società desidera estendere la protezione a Internet per i computer portatili che si spostano dalla rete Intranet a Internet.  

 Davide esegue il mapping di questi requisiti aziendali agli scenari seguenti:  

|Requisito|Stato corrente della gestione client|Stato futuro della gestione client|  
|-----------------|-------------------------------------|------------------------------------|  
|Tutti i computer eseguono software antimalware che dispone di file di definizione aggiornati e abilita Windows Firewall.|Computer diversi eseguono soluzioni antimalware diverse che non sono sempre aggiornate e, benché Windows Firewall sia abilitato per impostazione predefinita, a volte gli utenti lo disabilitano.<br /><br /> Agli utenti viene richiesto di contattare il supporto tecnico se viene rilevato software dannoso nel computer.|Tutti i computer eseguono la stessa soluzione antimalware che scarica automaticamente i file più recenti di aggiornamento della definizione e automaticamente riabilita Windows Firewall, se gli utenti lo disabilitano.<br /><br /> Il supporto tecnico riceve automaticamente una notifica tramite posta elettronica se viene rilevato software dannoso.|  
|Tutti i computer installano gli aggiornamenti software critici entro un mese dalla data di rilascio.|Anche se gli aggiornamenti software sono installati nei computer, molti computer non installano automaticamente gli aggiornamenti software critici fino a due o tre mesi dopo il rilascio. In questo modo rimangono vulnerabili agli attacchi durante questo periodo di tempo.<br /><br /> Per i computer che non installano gli aggiornamenti software critici, il supporto tecnico invia prima un messaggio di posta elettronica chiedendo agli utenti di installare gli aggiornamenti. Per i computer che rimangono non conformi, i tecnici si connettono in remoto ai computer e installano manualmente gli aggiornamenti software mancanti.|Miglioramento del tasso di conformità corrente entro il mese specificato fino a più del 95% senza inviare messaggi di posta elettronica o chiedere al supporto tecnico di installare gli aggiornamenti manualmente.|  
|Le impostazioni di protezione per applicazioni specifiche vengono controllare regolarmente e aggiornate, se necessario.|I computer eseguono script di avvio complessi che si basano sull'appartenenza a gruppi di computer per reimpostare i valori del Registro di sistema per applicazioni specifiche.<br /><br /> Poiché questi script vengono eseguiti solo all'avvio e alcuni computer vengono lasciati accesi per giorni, il supporto tecnico non può controllare la deviazione della configurazione su base temporale.|I valori del Registro di sistema vengono controllati e aggiornati automaticamente senza basarsi sull'appartenenza al gruppo di computer o riavviare il computer.|  
|I dispositivi mobili non possono installare o eseguire applicazioni non sicure.|Agli utenti viene richiesto di non scaricare da Internet ed eseguire applicazioni potenzialmente non sicure, ma non ci sono controlli per monitorare o forzare questo comportamento.|I dispositivi mobili gestiti con Microsoft Intune o Configuration Manager impediscono automaticamente l'installazione o l'esecuzione delle applicazioni non firmate.|  
|I computer portatili che si spostano dalla rete Intranet a Internet devono essere protetti.|Gli utenti in viaggio spesso non riescono a connettersi tramite la connessione VPN quotidianamente e i portatili non sono più conformi ai requisiti di protezione.|È sufficiente una connessione Internet per mantenere i portatili conformi ai requisiti di protezione. Gli utenti non devono accedere o usare la connessione VPN.|  

 Per soddisfare i requisiti, Davide usa le funzionalità di gestione e le opzioni di configurazione di Configuration Manager seguenti:  

-   Endpoint Protection  
-   Aggiornamenti software  
-   Impostazioni di conformità  
-   Gestione dispositivi mobili  
-   Gestione client basata su Internet  

 L'implementazione viene eseguita tramite la procedura di configurazione illustrata nella tabella seguente.  

|Procedura di configurazione|Risultato|  
|-------------------------|-------------|  
|Davide configura Endpoint Protection, abilita l'impostazione client per disinstallare altre soluzioni antimalware e abilita Windows Firewall. Configura le regole di distribuzione automatica in modo che i computer controllino e installino regolarmente gli aggiornamenti più recenti delle definizioni.|La soluzione antimalware unica consente di proteggere tutti i computer riducendo al minimo il carico amministrativo. Poiché il supporto tecnico riceve automaticamente una notifica tramite posta elettronica se viene rilevato antimalware, i problemi possono essere risolti rapidamente. In questo modo è possibile impedire attacchi in altri computer.|  
|Per aumentare i tassi di conformità, Davide usa le regole di distribuzione automatica, definisce la finestra di manutenzione per i server e verifica i vantaggi e gli svantaggi di usare Riattivazione LAN per i computer in stato di ibernazione.|La conformità per gli aggiornamenti software critici aumenta e si riduce la necessità per gli utenti o il supporto tecnico di installare manualmente gli aggiornamenti software.|  
|Davide usa le impostazioni di conformità per verificare la presenza di applicazioni specifiche. Quando vengono rilevate le applicazioni, gli elementi di configurazione verificano i valori del Registro di sistema e li aggiornano automaticamente se non sono conformi.|Usando gli elementi e le linee base di configurazione che sono distribuiti in tutti i computer e che controllano quotidianamente la conformità, non sono più necessari script distinti basati sull'appartenenza del computer e sul riavvio del computer.|  
|Davide usa le impostazioni di conformità per i dispositivi mobili registrati e configura il connettore di Exchange Server in modo da proibire l'installazione e l'esecuzione di applicazioni non firmate nei dispositivi mobili.|Vietando le applicazioni non firmate, i dispositivi mobili vengono protetti automaticamente dalle applicazioni potenzialmente dannose.|  
|Davide verifica che i server e i computer del sistema del sito dispongano dei certificati PKI che Configuration Manager richiede per le connessioni HTTPS e quindi installa i ruoli aggiuntivi del sistema del sito nella rete perimetrale che accetta le connessioni client da Internet.|I computer che si spostano automaticamente dalla rete Intranet a Internet continueranno a essere gestiti da Configuration Manager quando dispongono di una connessione a Internet. Tali computer non si basano sull'accesso degli utenti al computer o sulla connessione alla VPN.<br /><br /> Questi computer continueranno a essere gestiti per antimalware e Windows Firewall, aggiornamenti software ed elementi di configurazione. Di conseguenza, i livelli di conformità aumentano automaticamente.|  

 Questa procedura di configurazione e i relativi risultati consentono a Trey Research di semplificare la gestione dei client per dispositivi.  

###  <a name="a-namebkmkscenariosimplifya-example-scenario-simplify-client-management-for-devices"></a><a name="BKMK_ScenarioSimplify"></a> Scenario di esempio: semplificare la gestione client per i dispositivi  
 Trey Research vuole che tutti i nuovi computer installino automaticamente l'immagine del computer di base dell'azienda, che esegue Windows 7. Dopo che l'immagine del sistema operativo viene installata, i computer devono essere gestiti e monitorati per il software aggiuntivo installato dagli utenti. I computer che archiviano informazioni altamente riservate richiedono criteri di gestione più restrittivi rispetto ad altri computer. Ad esempio, i tecnici del supporto tecnico non devono connettersi da remoto, è necessario usare l'immissione PIN di BitLocker per il riavvio e solo gli amministratori locali possono installare software.  

 Davide esegue il mapping di questi requisiti aziendali agli scenari seguenti:  

|Requisito|Stato corrente della gestione client|Stato futuro della gestione client|  
|-----------------|-------------------------------------|------------------------------------|  
|Nei nuovi computer viene installato Windows 7.|Il supporto tecnico installa e configura Windows 7 per gli utenti e quindi invia il computer alla relativa posizione.|I nuovi computer vanno direttamente alla destinazione finale, sono collegati alla rete e installano e configurano Windows 7 automaticamente.|  
|I computer devono essere gestiti e monitorati. Ciò include l'inventario hardware e software per determinare i requisiti di licenza.|Il client di Configuration Manager viene distribuito usando l'installazione push client automatica e il supporto tecnico controlla gli errori di installazione e i client che non inviano i dati di inventario quando previsto.<br /><br /> Gli errori sono frequenti a causa di dipendenze di installazione non soddisfatte ed errori WMI nel client.|I dati di inventario e installazione client raccolti nei computer sono più affidabili e richiedono meno interventi di assistenza. I report mostrano l'utilizzo software per le informazioni sulla licenza.|  
|Alcuni computer devono disporre di criteri di gestione più rigorosi.|A causa dei criteri di gestione più rigorosi, questi computer non sono attualmente gestiti da Configuration Manager.|Gestire i computer usando Configuration Manager senza ulteriore carico amministrativo per gestire le eccezioni.|  

 Per soddisfare i requisiti, Davide usa le funzionalità di gestione e le opzioni di configurazione di Configuration Manager seguenti:  

-   Distribuzione del sistema operativo  
-   Distribuzione client e stato del client  
-   Impostazioni di conformità  
-   Impostazioni client  
-   Inventario e Asset Intelligence  
-   Amministrazione basata su ruoli  

 L'implementazione viene eseguita tramite la procedura di configurazione illustrata nella tabella seguente.  

|Procedura di configurazione|Risultato|  
|-------------------------|-------------|  
|Davide acquisisce un'immagine del sistema operativo da un computer con Windows 7 installato e configurato in base alle specifiche della società. Distribuisce quindi il sistema operativo nei nuovi computer, usando il supporto di computer sconosciuti e PXE. Installa anche il client di Configuration Manager come parte della distribuzione del sistema operativo.|I nuovi computer risultano operativi più rapidamente senza interventi da parte del supporto tecnico.|  
|Davide configura l'installazione push client a livello di sito per installare il client di Configuration Manager in qualsiasi computer individuato. Ciò assicura che il client verrà installato anche in eventuali computer non inclusi nell'immagine del client, in modo che tali computer vengano gestiti da Configuration Manager.<br /><br /> Davide configura lo stato del client in modo che vengano risolti automaticamente eventuali problemi rilevati relativi al client. Configura inoltre le impostazioni del client che consentono la raccolta dei dati di inventario necessari e infine configura Asset Intelligence.|L'installazione del client insieme al sistema operativo risulta più rapida e più affidabile rispetto all'attesa dell'individuazione del computer da parte di Configuration Manager e del successivo tentativo di installare i file di origine del client nel computer. Se tuttavia si lascia abilitata l'opzione di push automatico del client, si disporrà di un'alternativa per consentire a un computer in cui è già installato il sistema operativo di installare il client quando il computer si connette alla rete.<br /><br /> Le impostazioni del client assicurano che le informazioni di inventario vengano inviate regolarmente al sito dai client. Oltre ai test dello stato del client, ciò aiuta a mantenere in esecuzione il client con un intervento minimo da parte del supporto tecnico. Ad esempio, gli errori WMI vengono rilevati e risolti automaticamente.<br /><br /> I report di Asset Intelligence agevolano il monitoraggio dell'utilizzo del software e delle licenze.|  
|Davide crea una raccolta per i computer per cui sono necessarie impostazioni più restrittive per i criteri, quindi crea un'impostazione personalizzata del dispositivo client per questa raccolta, che include la disabilitazione del controllo remoto, abilita l'immissione del PIN di BitLocker e consente solo agli amministratori locali di installare software.<br /><br /> Davide configura l'amministrazione basata su ruoli, in modo che i responsabili del supporto tecnico non possano visualizzare questa raccolta di computer, per evitare che vengano accidentalmente gestiti come computer standard.|Questi computer vengono ora gestiti da Configuration Manager, ma con impostazioni specifiche che non necessitano di un nuovo sito.<br /><br /> La raccolta per questi computer non risulta visibile ai responsabili del supporto tecnico, in modo da ridurre il rischio di invio accidentale di distribuzioni e script per computer standard.|  

 Questa procedura di configurazione e i relativi risultati consentono a Trey Research di ottenere una semplificazione della gestione dei client per dispositivi.  

##  <a name="a-namebkmknextstepsa-next-steps"></a><a name="BKMK_NextSteps"></a> Passaggi successivi  
 Prima di installare Configuration Manager, è possibile approfondire alcuni concetti e termini di base specifici di questo strumento.  

-   Se si ha familiarità con System Center Configuration Manager 2012, vedere [What's changed in System Center Configuration Manager from System Center 2012 Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md) (Novità in System Center Configuration Manager rispetto a System Center Configuration Manager 2012) per informazioni sulle nuove funzionalità.  
-   Per una panoramica tecnica di alto livello di System Center Configuration Manager, vedere [Fundamentals of System Center Configuration Manager](../../core/understand/fundamentals.md) (Nozioni fondamentali su System Center Configuration Manager).  

 Dopo avere approfondito i concetti di base, usare la documentazione di System Center Configuration Manager per agevolare una distribuzione e un uso corretto di questo strumento.  



<!--HONumber=Nov16_HO1-->



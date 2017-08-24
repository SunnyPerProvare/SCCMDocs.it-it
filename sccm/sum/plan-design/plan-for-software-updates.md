---
title: Pianificare gli aggiornamenti del software | Microsoft Docs
description: "Una pianificazione per l'infrastruttura del punto di aggiornamento software è essenziale prima di usare gli aggiornamenti software in un ambiente di produzione di System Center Configuration Manager."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 06/27/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: configmgr-sum
ms.assetid: d071b0ec-e070-40a9-b7d4-564b92a5465f
ms.openlocfilehash: 8b739a01a6bb5cacf0f7109e2e6fa3b31dd666d3
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="plan-for-software-updates-in-system-center-configuration-manager"></a>Pianificare gli aggiornamenti software in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima di usare gli aggiornamenti software in un ambiente di produzione di System Center Configuration Manager, è importante eseguire il processo di pianificazione. La definizione di una pianificazione valida per l'infrastruttura del punto di aggiornamento software è fondamentale per un'implementazione corretta di aggiornamenti software.

## <a name="capacity-planning-recommendations-for-software-updates"></a>Raccomandazioni per la pianificazione della capacità per gli aggiornamenti software  
 È possibile utilizzare le seguenti raccomandazioni come linea di base di ausilio per determinare le informazioni relative alla pianificazione della capacità degli aggiornamenti software appropriate per la propria organizzazione. I requisiti di capacità specifici possono variare dai suggerimenti elencati in questo argomento a seconda dei seguenti criteri: l'ambiente di rete specifico, l'hardware usato per ospitare il sistema del sito del punto di aggiornamento software, il numero di client installati e i ruoli del sistema del sito installati sul server.  

###  <a name="BKMK_SUMCapacity"></a> Pianificazione della capacità per il punto di aggiornamento software  
 Il numero di client supportati dipende dalla versione di Windows Server Update Services (WSUS) in esecuzione nel punto di aggiornamento software e dall'eventuale coesistenza del ruolo del sistema del sito del punto di aggiornamento software con un altro ruolo del sistema del sito:  

-   Il punto di aggiornamento software è in grado di supportare fino a 25.000 client quando WSUS è in esecuzione nel computer del punto di aggiornamento software e tale punto coesiste con un altro ruolo del sistema del sito.  

-   Il punto di aggiornamento software può supportare fino a 150.000 client se il computer remoto soddisfa i requisiti di WSUS, se WSUS viene usato con Configuration Manager e se si configurano le opzioni seguenti:

    Pool di applicazioni IIS:
    - Aumentare la lunghezza della coda WsusPool a 2000
    - Aumentare il limite di memoria privata WsusPool di 4 volte oppure impostarlo su 0 (illimitato)      

    Per informazioni dettagliate sui requisiti hardware per il punto di aggiornamento software, vedere [Recommended hardware for site systems](/sccm/core/plan-design/configs/recommended-hardware#a-namebkmkscalesiesystemsa-site-systems) (Hardware consigliato per i sistemi del sito).

-   Per impostazione predefinita, Configuration Manager non supporta la configurazione di punti di aggiornamento software come cluster di bilanciamento del carico di rete. Prima di Configuration Manager versione 1702, è possibile usare Configuration Manager SDK per configurare un massimo di quattro punti di aggiornamento software in un cluster di bilanciamento del carico di rete. Tuttavia, a partire da Configuration Manager versione 1702, i punti di aggiornamento software non sono supportati come cluster di bilanciamento del carico di rete e gli aggiornamenti a Configuration Manager versione 1702 verranno bloccati se viene rilevata questa configurazione.

### <a name="capacity-planning-for-software-updates-objects"></a>Pianificazione della capacità per gli oggetti degli aggiornamenti software  
 Utilizzare le seguenti informazioni sulla capacità per la pianificazione degli oggetti degli aggiornamenti software.  

-   **Limite di 1000 aggiornamenti software in una distribuzione**  

     È necessario limitare il numero di aggiornamenti software a 1000 per ogni distribuzione degli aggiornamenti software. Quando si crea una regola di distribuzione automatica, specificare un criterio che limiti il numero di aggiornamenti software restituiti. La regola di distribuzione automatica presenta un errore se i criteri specificati restituiscono più di 1000 aggiornamenti software. È possibile controllare lo stato della regola di distribuzione automatica dal nodo **Regole di distribuzione automatica** nella console di Configuration Manager. Durante la distribuzione manuale degli aggiornamenti software, non selezionare più di 1000 aggiornamenti per la distribuzione.  

     È anche necessario limitare il numero di aggiornamenti software a 1000 in una configurazione di base. Per altre informazioni, vedere [Creare configurazioni di base](../../compliance/deploy-use/create-configuration-baselines.md).

##  <a name="BKMK_SUPInfrastructure"></a> Determinare l'infrastruttura del punto di aggiornamento software  
 Il sito di amministrazione centrale e tutti i siti primari figlio devono disporre di un punto di aggiornamento software in cui verranno distribuiti gli aggiornamenti software. Quando si pianifica l'infrastruttura del punto di aggiornamento software, è necessario determinare le dipendenze seguenti:
 - la posizione in cui installare il punto di aggiornamento software per il sito
 - quali siti richiedono un punto di aggiornamento software che accetta la comunicazione da client basati su Internet
 - se è necessario un punto di aggiornamento software in un sito secondario

Utilizzare le sezioni seguenti per determinare l'infrastruttura del punto di aggiornamento software.  

> [!IMPORTANT]  
>  Per informazioni sulle dipendenze interne ed esterne necessarie per gli aggiornamenti software, vedere [Prerequisiti per gli aggiornamenti software](prerequisites-for-software-updates.md).  

 È possibile aggiungere più punti di aggiornamento software in un sito primario di Configuration Manager. La possibilità di disporre di più punti di aggiornamento software in un sito fornisce la tolleranza d'errore senza la complessità del Bilanciamento carico di rete. Tuttavia, il failover ricevuto con più punti di aggiornamento software non è così solido come NLB per il puro bilanciamento del carico, ma è piuttosto progettato per la tolleranza d'errore. Inoltre, la struttura del failover del punto di aggiornamento software è diversa dal modello di pura sequenza casuale utilizzato nella struttura dei punti di gestione. A differenza di questi ultimi, il passaggio a un nuovo punto di aggiornamento software comporta dei costi in termini di prestazioni di rete e client. Quando il client passa a un nuovo server WSUS per analizzare gli aggiornamenti software, il risultato è un incremento nella dimensione del catalogo e nelle richieste in termini di prestazioni di rete e lato client associate. Di conseguenza, il client mantiene affinità con l'ultimo punto di aggiornamento software per il quale ha eseguito correttamente l'analisi.  

 Il primo punto di aggiornamento software installato su un sito primario è l'origine di sincronizzazione per tutti gli ulteriori punti di aggiornamento software aggiunti nel sito primario. Dopo aver aggiunto i punti di aggiornamento software e aver avviato la sincronizzazione degli aggiornamenti software, è possibile visualizzare lo stato dei punti di aggiornamento software e l'origine di sincronizzazione dal nodo **Stato di sincronizzazione del punto di aggiornamento software** nell'area di lavoro **Monitoraggio** .  

 Quando un punto di aggiornamento software presenta un'anomalia, ed è configurato come origine di sincronizzazione per gli altri punti di aggiornamento software del sito, è necessario rimuovere manualmente tale punto e selezionarne uno nuovo da utilizzare come origine di sincronizzazione. Per altre informazioni sulla rimozione di un punto di aggiornamento software, vedere [Rimuovere il ruolo di sistema del sito del punto di aggiornamento software](../get-started/remove-a-software-update-point.md).  

###  <a name="BKMK_SUPList"></a> Elenco dei punti di aggiornamento software  
 Configuration Manager offre al client un elenco di punti di aggiornamento software nei seguenti scenari: quando un nuovo client riceve i criteri di abilitazione degli aggiornamenti software oppure quando un client non può contattare il proprio punto di aggiornamento software e deve passare a un altro punto. Il client seleziona un punto di aggiornamento software nell'elenco in modo casuale, assegnando la priorità ai punti che si trovano nella stessa foresta. Configuration Manager offre ai client un elenco diverso a seconda del tipo di client.  

-   **Client basati su intranet**: si riceve un elenco di punti di aggiornamento software che è possibile configurare per consentire solo connessioni dalla intranet oppure un elenco di punti di aggiornamento software che consentono connessioni client Internet e intranet.  

-   **Client basati su Internet**: ricevono un elenco di punti di aggiornamento software che è possibile configurare per consentire solo le connessioni da Internet oppure un elenco di punti di aggiornamento software che consentono connessioni client Internet e Intranet.  

###  <a name="BKMK_SUPSwitching"></a> Passaggio a un nuovo punto di aggiornamento software  
> [!NOTE]
> A partire dalla versione 1702, i client usano i gruppi di limiti per trovare un nuovo punto di aggiornamento software se quello corrente non è più disponibile. È possibile aggiungere singoli punti di aggiornamento software a diversi gruppi di limiti per controllare quali server possono essere trovati da un client. Per altre informazioni, vedere la sezione [Punti di aggiornamento software](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) dell'argomento [Configurare gruppi di limiti](/sccm/core/servers/deploy/configure/boundary-groups).

Se si dispone di più punti di aggiornamento software in un sito, e uno di questi presenta un'anomalia o non è più disponibile, i client si connetteranno a un altro punto di aggiornamento software e continueranno ad analizzare gli ultimi aggiornamenti. Quando un client viene inizialmente assegnato a un punto di aggiornamento software, vi resta assegnato salvo errore durante l'analisi degli aggiornamenti software su quel punto.  

L'analisi degli aggiornamenti software può avere un esito negativo con una serie di diversi codici di errore relativi a nuovi tentativi o mancati tentativi. In caso di analisi non riuscita con un codice di errore di nuovi tentativi, il client avvia un processo di nuovi tentativi di analisi degli aggiornamenti software sul relativo punto. Le condizioni di alto livello che generano tale codice di errore sono spesso attribuibili a un server WSUS non disponibile o temporaneamente sovraccarico. Quando non è possibile analizzare gli aggiornamenti software, il client utilizza il seguente processo:  

1.  Analizza gli aggiornamenti software all'orario pianificato, quando viene avviato attraverso il Pannello di controllo del client oppure utilizzando l'SDK. Se l'analisi ha esito negativo, il client attende 30 minuti per ripetere l'operazione e utilizza lo stesso punto di aggiornamento software.  

2.  Il client esegue almeno quattro tentativi a intervalli di 30 minuti. Al quarto tentativo non riuscito, e dopo aver atteso altri due minuti, il client passerà al successivo punto di aggiornamento software nel relativo elenco.  

3.  Il client segue lo stesso processo nel nuovo punto di aggiornamento software. Al termine di un'analisi eseguita correttamente, il client continuerà a connettersi al nuovo punto di aggiornamento software.

 Nell'elenco che segue vengono fornite informazioni aggiuntive utili in caso di tentativi di connessione a un punto di aggiornamento software e in scenari di passaggio:  

-   Se un client è disconnesso dalla intranet aziendale e non riesce ad analizzare gli aggiornamenti software, non passerà a un altro punto di aggiornamento software. Si tratta di un errore previsto, perché il client non è in grado di raggiungere la rete aziendale o il punto di aggiornamento software che consente la connessione dalla intranet. Il client di Configuration Manager determina la disponibilità del punto di aggiornamento software intranet.  

-   Se la gestione client basata su Internet è abilitata, e sono presenti più punti di aggiornamento software configurati per l'accettazione delle comunicazioni da client su Internet, il processo di passaggio seguirà il processo di nuovi tentativi standard descritto nello scenario precedente.  

-   Uno scenario in cui il processo di analisi viene avviato, ma il client viene spento prima del relativo completamento, non è da considerarsi una condizione di errore di analisi e non rientra nei quattro tentativi disponibili.  

Se l'agente di Windows Update invia a Configuration Manager uno dei codici di errore seguenti, il client tenterà di riconnettersi:  

2149842970, 2147954429, 2149859352, 2149859362, 2149859338, 2149859344, 2147954430, 2147747475, 2149842974, 2149859342, 2149859372, 2149859341, 2149904388, 2149859371, 2149859367, 2149859366, 2149859364, 2149859363, 2149859361, 2149859360, 2149859359, 2149859358, 2149859357, 2149859356, 2149859354, 2149859353, 2149859350, 2149859349, 2149859340, 2149859339, 2149859332, 2149859333, 2149859334, 2149859337, 2149859336, 2149859335

Per conoscere il significato di un codice di errore, convertire il codice di errore decimale in formato esadecimale e cercare il valore esadecimale in un sito, ad esempio [Windows Update Agent - Error Codes Wiki](https://social.technet.microsoft.com/wiki/contents/articles/15260.windows-update-agent-error-codes.aspx) (Agente di Windows Update: wiki codici di errore).


###  <a name="BKMK_ManuallySwitchSUPs"></a> Passaggio manuale dei client a un nuovo punto di aggiornamento software
A partire da Configuration Manager versione 1606 è possibile abilitare l'opzione per consentire ai client di Configuration Manager di passare a un nuovo punto di aggiornamento software quando si verificano problemi con il punto di aggiornamento software attivo. Questa opzione comporta modifiche solo se un client riceve più punti di aggiornamento software da un punto di gestione.

> [!IMPORTANT]    
> Quando si passa a un altro dispositivo per usare un nuovo server, i dispositivi trovano il nuovo server tramite fallback. Esaminare quindi le configurazioni dei gruppi di limiti e assicurarsi che i punti di aggiornamento software siano nei gruppi di limite corretti prima di avviare questa modifica. Per informazioni dettagliate, vedere[Punti di aggiornamento software](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points).
>
> Il passaggio a un nuovo punto di aggiornamento software genera traffico di rete aggiuntivo. La quantità di traffico dipende dalle impostazioni di configurazione di WSUS (Windows Server Update Services), ad esempio dalle classificazioni degli aggiornamenti, dai prodotti, dalla condivisione o meno di un database WSUS da parte dei punti di aggiornamento software e così via. Se si prevede di passare da uno all'altro di più di due dispositivi, è consigliabile eseguire l'operazione all'interno delle finestre di manutenzione, per ridurre l'impatto sulla rete durante la sincronizzazione del nuovo server del punto di aggiornamento software.

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>Per abilitare l'opzione per il passaggio tra punti di aggiornamento software  
Abilitare questa opzione in una raccolta di dispositivi o in un set di dispositivi selezionati. Dopo che l'opzione è stata abilitata, in occasione dell'analisi successiva il client cercherà un altro punto di aggiornamento software.

1.  Nella console di Configuration Manager fare clic su **Asset e conformità > Panoramica > Raccolte dispositivi**.  

2.  Nel gruppo **Raccolta** della scheda **Home** fare clic su **Notifica client**e quindi su **Passare al punto di aggiornamento software successivo**.  


###  <a name="BKMK_SUP_CrossForest"></a> Punti di aggiornamento software in una foresta non trusted  
 È possibile creare uno o più punti di aggiornamento software in un sito per supportare client in una foresta non trusted. Per aggiungere un punto di aggiornamento software in un'altra foresta, è necessario innanzitutto installare e configurare un server WSUS nella foresta. Avviare quindi la procedura guidata per aggiungere un server del sito di Configuration Manager con il ruolo di sistema del sito del punto di aggiornamento software. Nella procedura guidata, configurare le seguenti impostazioni per connettersi al server WSUS nella foresta non trusted:  

-   Specificare un account di installazione del sistema del sito che possa accedere al server WSUS nella foresta.  

-   Specificare l'account di connessione al server WSUS da utilizzare per connettersi a tale server.  

 Ad esempio, si dispone di un sito primario nella foresta A con due punti di aggiornamento software (SUP01 e SUP02). Inoltre, per lo stesso sito primario vi sono due punti di aggiornamento software (SUP03 e SUP04) nella foresta B. Quando si verifica il passaggio in un tale scenario, viene attribuita la priorità ai punti di aggiornamento software della stessa foresta del client.  

###  <a name="BKMK_WSUSSyncSource"></a> Uso di un server WSUS esistente come origine di sincronizzazione nel sito principale  
 In genere, il sito di livello superiore della gerarchia è configurato per sincronizzare i metadati degli aggiornamenti software con Microsoft Update. Se i criteri di sicurezza aziendali non consentono l'accesso a Internet dal sito principale, è possibile configurare l'origine di sincronizzazione per il sito principale per usare un server WSUS esistente non presente nella gerarchia di Configuration Manager. Ad esempio, nella rete perimetrale potrebbe essere installato un server WSUS con accesso a Internet, accesso di cui non dispone il sito di livello superiore. È possibile configurare il server WSUS nella rete perimetrale come origine di sincronizzazione per i metadati degli aggiornamenti software. È necessario verificare che il server WSUS nella rete perimetrale sincronizzi gli aggiornamenti software conformi ai criteri necessari nella gerarchia di Configuration Manager. In caso contrario, il sito di livello superiore potrebbe non essere in grado di sincronizzare gli aggiornamenti software previsti. Quando si installa il punto di aggiornamento software, configurare un account di connessione WSUS con accesso al server WSUS nella rete perimetrale e verificare che il firewall consenta il traffico per le porte appropriate. Per altre informazioni, esaminare le [porte usate dal punto di aggiornamento software per l'origine di sincronizzazione](../../core/plan-design/hierarchy/ports.md#BKMK_PortsSUP-WSUS).  

###  <a name="BKMK_NLBSUPSP1"></a> Punto di aggiornamento software configurato per l'uso di Bilanciamento carico di rete  
 Il passaggio a un altro punto di aggiornamento software risponderà con tutta probabilità alle richieste di tolleranza d'errore degli utenti. Per impostazione predefinita, Configuration Manager non supporta la configurazione di punti di aggiornamento software come cluster di bilanciamento del carico di rete. Prima di Configuration Manager versione 1702, è possibile usare Configuration Manager SDK per configurare un massimo di quattro punti di aggiornamento software in un cluster di bilanciamento del carico di rete. Tuttavia, a partire da Configuration Manager versione 1702, i punti di aggiornamento software non sono supportati come cluster di bilanciamento del carico di rete e gli aggiornamenti a Configuration Manager versione 1702 verranno bloccati se viene rilevata questa configurazione. Per altre informazioni sul cmdlet Set-CMSoftwareUpdatePoint di PowerShell, vedere [Set-CMSoftwareUpdatePoint](http://go.microsoft.com/fwlink/?LinkId=276834).

###  <a name="BKMK_SUPSecSite"></a> Punto di aggiornamento software in un sito secondario  
 Il punto di aggiornamento software è facoltativo in un sito secondario. Quando si installa un punto di aggiornamento software in un sito secondario, il database WSUS viene configurato come una replica del punto di aggiornamento software predefinito nel sito primario padre. È possibile installare un solo punto di aggiornamento software in un sito secondario. I dispositivi assegnati a un sito secondario sono configurati per l'utilizzo di un punto di aggiornamento software nel sito padre quando tale punto non è installato nel sito secondario. In genere, un punto di aggiornamento software viene installato in un sito secondario in presenza di una larghezza di banda della rete limitata tra i dispositivi assegnati al sito secondario e i punti di aggiornamento software nel sito primario padre, oppure quando il punto di aggiornamento software sta per raggiungere il limite di capacità. Dopo l'installazione e la configurazione di un punto di aggiornamento software in un sito secondario, vengono aggiornati dei criteri a livello di sito per i computer client assegnati a tale sito, che inizieranno a utilizzare il nuovo punto di aggiornamento software.  

##  <a name="BKMK_SUPInstallation"></a> Pianificare l'installazione del punto di aggiornamento software  
 Prima di creare un ruolo di sistema del sito del punto di aggiornamento software in Configuration Manager, è necessario prendere in considerazione diversi requisiti in base all'infrastruttura di Configuration Manager. Quando si configura il punto di aggiornamento software per comunicare tramite SSL, è particolarmente importante esaminare questa sezione perché sono necessari dei passaggi aggiuntivi per garantire il funzionamento corretto dei punti di aggiornamento software nella gerarchia. In questa sezione vengono fornite informazioni sui passaggi da effettuare per poter pianificare e preparare l'installazione del punto di aggiornamento software.  

###  <a name="BKMK_SUPSystemRequirements"></a> Requisiti per il punto di aggiornamento software  
 Il ruolo di sistema del sito del punto di aggiornamento software deve essere installato in un sistema del sito conforme ai requisiti minimi per WSUS e alle configurazioni supportate per i sistemi del sito di Configuration Manager.  

-   Per altre informazioni sui requisiti minimi per il ruolo del server WSUS in Windows Server 2012, vedere [Rivedere le considerazioni e i requisiti di sistema](https://technet.microsoft.com/library/hh852344.aspx#BKMK_1.1) nella libreria della documentazione di Windows Server 2012.  

-   Per altre informazioni sulle configurazioni supportate per i sistemi del sito di Configuration Manager, vedere [Prerequisiti del sito e di sistema del sito](../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

###  <a name="BKMK_PlanningForWSUS"></a> Pianificare l'installazione di WSUS  

Gli aggiornamenti software richiedono che su tutti i server del sistema del sito sia installata una versione supportata di WSUS configurata per il ruolo del sistema sito del punto di aggiornamento software. Inoltre, quando non si installa il punto di aggiornamento software nel server del sito, è necessario installare la console di amministrazione WSUS sul computer del server del sito, se non già installata. In questo modo il server del sito può comunicare con WSUS in esecuzione sul punto di aggiornamento software.  

 Quando si usa WSUS in Windows Server 2012, è necessario configurare autorizzazioni aggiuntive per consentire a **WSUS Configuration Manager** in Configuration Manager di connettersi al WSUS per eseguire controlli di integrità periodici. Scegliere una delle seguenti opzioni per configurare le autorizzazioni:  

-   Aggiungere l'account **SYSTEM** per il gruppo **WSUS Administrators**  

-   Aggiungere l'account **NT AUTHORITY\SYSTEM** come un utente per il database WSUS (SUSDB) e configurare un minimo per l'appartenenza al ruolo del database webService  

 Per ulteriori informazioni sull'installazione di WSUS su Windows Server 2012, vedere [Installare il ruolo server WSUS](http://go.microsoft.com/fwlink/p/?LinkId=272355) nella libreria della documentazione di Windows Server 2012.  

 In caso di installazione di più di un punto di aggiornamento software in un sito primario, utilizzare lo stesso database WSUS per ciascun punto di aggiornamento software nella stessa foresta Active Directory. Condividendo lo stesso database, si limita notevolmente, ma non si elimina completamente, l'impatto sulle prestazioni dei client e della rete che potrebbe essere avvertito quando i client passano a un nuovo punto di aggiornamento software. Quando un client esegue il passaggio a un nuovo punto di aggiornamento software che condivide un database con il punto di aggiornamento software precedente, viene comunque eseguita una scansione differenziale. Tuttavia, tale scansione è molto ridotta rispetto a come sarebbe se il server WSUS disponesse di un proprio database.  

####  <a name="BKMK_CustomWebSite"></a> Configurazione di WSUS per l'uso di un sito Web personalizzato  
 Quando si installa WSUS, è possibile utilizzare il sito Web predefinito IIS esistente o creare un sito Web di WSUS personalizzato. Creare un sito Web personalizzato per WSUS in modo che IIS ospiti i servizi WSUS in un sito Web virtuale dedicato invece di condividere lo stesso sito Web usato dagli altri sistemi del sito di Configuration Manager o da altre applicazioni. Ciò vale soprattutto quando si installa il ruolo del sistema sito del punto di aggiornamento software sul server del sito. Quando si esegue WSUS in Windows Server 2012 o Windows Server 2016, WSUS viene configurato per impostazione predefinita per l'uso della porta 8530 per HTTP e della porta 8531 per HTTPS. Quando viene creato il punto di aggiornamento software in un sito, è necessario specificare queste impostazioni porta.  

####  <a name="BKMK_WSUSInfrastructure"></a> Uso di un'infrastruttura WSUS esistente  
 È possibile usare un server WSUS che era attivo nell'ambiente prima dell'installazione di Configuration Manager come punto di aggiornamento software. Quando il punto di aggiornamento software è configurato, è necessario specificare le impostazioni di sincronizzazione. Configuration Manager si connette al server WSUS eseguito nel punto di aggiornamento software e lo configura con le stesse impostazioni. Se prima di essere configurato come punto di aggiornamento software il server WSUS è stato sincronizzato con prodotti o classificazioni non configurati come parte delle impostazioni di sincronizzazione del punto di aggiornamento software, i metadati degli aggiornamenti software per i prodotti e le classificazioni vengono sincronizzati per tutti i metadati degli aggiornamenti software nel database di WSUS, indipendentemente dalle impostazioni di sincronizzazione configurate per il punto di aggiornamento software. Ciò potrebbe comportare dei metadati degli aggiornamenti software imprevisti nel database del sito. Lo stesso comportamento sarà registrato in caso di aggiunta di prodotti o classificazioni direttamente nella console di amministrazione di WSUS e di successivo avvio immediato di una sincronizzazione. Per impostazione predefinita, Configuration Manager si connette ogni ora a WSUS in un punto di aggiornamento software e reimposta qualsiasi impostazione modificata al di fuori di Configuration Manager. Per gli aggiornamenti software non conformi ai prodotti e alle classificazioni specificati nelle impostazioni di sincronizzazione sono previste l'impostazione della scadenza e quindi la relativa rimozione dal database del sito.

 Quando un server WSUS è configurato come punto di aggiornamento software, non è più possibile usarlo come server WSUS autonomo. Se è necessario un server WSUS autonomo separato, non gestito da Configuration Manager, è necessario configurarlo in un server diverso.

####  <a name="BKMK_WSUSAsReplica"></a> Configurare WSUS come server di replica  
 Quando si crea un ruolo del sistema sito del punto di aggiornamento software in un server del sito primario, non è possibile usare un server WSUS configurato come una replica. Se il server WSUS viene configurato come server di replica, Configuration Manager non riesce a configurarlo e non è possibile completare neanche la sincronizzazione di WSUS. Se un punto di aggiornamento software viene creato in un sito secondario, Configuration Manager configura WSUS come server di replica di WSUS eseguito nel punto di aggiornamento software del sito primario padre. Il primo punto di aggiornamento software installato in un sito primario è il punto predefinito. I punti di aggiornamento software aggiuntivi nel sito sono configurati come repliche del punto di aggiornamento software predefinito.  

####  <a name="BKMK_WSUSandSSL"></a> Decidere se configurare WSUS per l'uso di SSL  
 È possibile utilizzare il protocollo SSL per proteggere WSUS in esecuzione nel punto di aggiornamento software. WSUS utilizza SSL per l'autenticazione tra computer client e server WSUS downstream e il server WSUS. WSUS utilizza inoltre SSL per crittografare i metadati dell'aggiornamento software. Quando si sceglie di proteggere WSUS con SSL, è necessario preparare il server WSUS prima di installare il punto di aggiornamento software.  

 Quando si installa e configura il punto di aggiornamento software, è necessario selezionare l'impostazione **Abilita le comunicazioni SSL per il server WSUS** . In caso contrario, Configuration Manager configurerà WSUS in modo che non usi SSL. Quando si abilita SSL per WSUS in esecuzione in un punto di aggiornamento software, anche WSUS in esecuzione nel punto di aggiornamento software in qualsiasi sito figlio deve essere configurato per l'utilizzo di SSL.  

###  <a name="BKMK_ConfigureFirewalls"></a> Configurare i firewall  
 Gli aggiornamenti software in un sito di amministrazione centrale di Configuration Manager comunicano con WSUS eseguito nel punto di aggiornamento software, il quale a sua volta comunica con l'origine di sincronizzazione per sincronizzare i metadati degli aggiornamenti software. I punti di aggiornamento software in un sito figlio comunicano con il punto di aggiornamento software nel sito padre. Quando è presente più di un punto di aggiornamento software in un sito primario, i punti di aggiornamento software aggiuntivi devono comunicare con il primo punto installato nel sito, ovvero il punto di aggiornamento software predefinito.  

 Potrebbe essere necessario configurare il firewall affinché accetti le porte HTTP o HTTPS usate da WSUS negli scenari seguenti: quando si ha un firewall aziendale tra il punto di aggiornamento software di Configuration Manager e Internet, in presenza di un punto di aggiornamento software e della relativa origine di sincronizzazione upstream o in presenza di punti di aggiornamento software aggiuntivi. La connessione a Microsoft Update viene sempre configurata per utilizzare la porta 80 per HTTP e la porta 443 per HTTPS. È possibile utilizzare una porta personalizzata per la connessione da WSUS in esecuzione sul punto di aggiornamento software in un sito figlio a WSUS in esecuzione sul punto di aggiornamento software nel sito padre. Quando i criteri di sicurezza non consentono la connessione, è necessario usare il metodo di sincronizzazione esportazione e importazione. Per altre informazioni, vedere la sezione [Origine di sincronizzazione](#BKMK_SyncSource) in questo argomento. Per altre informazioni sulle porte usate da WSUS, vedere [Come determinare le impostazioni della porta usate da WSUS in System Center Configuration Manager](../get-started/install-a-software-update-point.md#wsus-settings).  

#### <a name="restrict-access-to-specific-domains"></a>Limitazione dell'accesso a domini specifici  
 Se la propria organizzazione non consente l'apertura delle porte e dei protocolli a tutti gli indirizzi nel firewall tra il punto di aggiornamento software attivo e Internet, è possibile limitare l'accesso ai seguenti domini, in modo da consentire la comunicazione di WSUS e Aggiornamenti automatici con Microsoft Update:  

-   http://windowsupdate.microsoft.com

-   http://*.windowsupdate.microsoft.com  

-   https://*.windowsupdate.microsoft.com  

-   http://*.update.microsoft.com  

-   https://*.update.microsoft.com  

-   http://*.windowsupdate.com  

-   http://download.windowsupdate.com  

-   http://download.microsoft.com  

-   http://*.download.windowsupdate.com  

-   http://test.stats.update.microsoft.com  

-   http://ntservicepack.microsoft.com  

 Potrebbe essere necessario aggiungere i seguenti indirizzi al firewall che si trova tra i due sistemi del sito nei seguenti casi: se i siti figlio dispongono di un punto di aggiornamento software o se è presente un punto di aggiornamento software basato su Internet attivo remoto in un sito:  

 **Punto di aggiornamento software nel sito secondario**  

-   http://<*FQDN per il punto di aggiornamento software nel sito figlio*>  

-   https://<*FQDN per il punto di aggiornamento software nel sito figlio*>  

-   http://<*FQDN per il punto di aggiornamento software nel sito padre*>  

-   https://<*FQDN per il punto di aggiornamento software nel sito padre*>  

##  <a name="BKMK_SyncSettings"></a> Pianificare le impostazioni di sincronizzazione  
 La sincronizzazione degli aggiornamenti software in Configuration Manager è il processo di recupero dei metadati degli aggiornamenti software in base ai criteri configurati. Il sito di livello superiore della gerarchia, il sito di amministrazione centrale o il sito primario autonomo consente di sincronizzare gli aggiornamenti software da Microsoft Update. È possibile scegliere di configurare il punto di aggiornamento software nel sito principale per la sincronizzazione con un server WSUS esistente, non nella gerarchia di Configuration Manager. I siti primari figlio sincronizzano i metadati degli aggiornamenti software dal punto di aggiornamento software nel sito di amministrazione centrale. Prima di installare e configurare un punto di aggiornamento software, utilizzare questa sezione per pianificare le impostazioni di sincronizzazione.  

###  <a name="BKMK_SyncSource"></a> Origine di sincronizzazione  
 Le impostazioni dell'origine di sincronizzazione per il punto di aggiornamento software specificano il percorso in cui il punto di aggiornamento software recupera i metadati degli aggiornamenti software e indicano se gli eventi di reporting WSUS sono creati durante il processo di sincronizzazione.  

-   **Origine sincronizzazione:** il punto di aggiornamento software nel sito di livello superiore configura l'origine della sincronizzazione per Microsoft Update per impostazione predefinita. È possibile sincronizzare il sito principale con un server WSUS esistente. Per impostazione predefinita, il punto di aggiornamento software in un sito primario figlio configura l'origine di sincronizzazione come il punto di aggiornamento software nel sito di amministrazione centrale.  

    > [!NOTE]  
    >  Il primo punto di aggiornamento software installato in un sito primario, ovvero il punto predefinito, si sincronizza con il sito di amministrazione centrale. I punti di aggiornamento software aggiuntivi nel sito primario si sincronizzano con il punto di aggiornamento software predefinito nel sito primario.  

     Quando un punto di aggiornamento software è disconnesso da Microsoft Update o dal server aggiornamenti upstream, è possibile configurare l'origine di sincronizzazione non per la sincronizzazione con un'origine di sincronizzazione configurata ma per l'utilizzo della funzione di esportazione e importazione dello strumento WSUSUtil per la sincronizzazione degli aggiornamenti software. Per altre informazioni, vedere [Sincronizzare gli aggiornamenti software da un punto di aggiornamento software disconnesso](../get-started/synchronize-software-updates-disconnected.md).  

-   **Eventi di reporting WSUS:** L'Agente di Windows Update nei computer client è in grado di creare messaggi di eventi usati per la creazione di report di WSUS. Questi eventi non vengono usati dall'aggiornamento software in Configuration Manager e pertanto l'opzione **Non creare eventi di reporting WSUS** viene selezionata per impostazione predefinita. Quando questi eventi non vengono creati, il computer client deve connettersi al server WSUS solo durante la valutazione dell'aggiornamento software e le analisi di conformità. Se questi eventi sono necessari per il reporting esterno agli aggiornamenti software in Configuration Manager, sarà necessario modificare questa impostazione per creare gli eventi di reporting WSUS.  

###  <a name="BKMK_SyncSchedule"></a> Pianificazione della sincronizzazione  
 È possibile configurare la pianificazione della sincronizzazione solo nel punto di aggiornamento software del sito principale della gerarchia di Configuration Manager. Quando si configura la pianificazione della sincronizzazione, il punto di aggiornamento software si sincronizza con l'origine di sincronizzazione alla data e all'ora specificata. La pianificazione personalizzata consente di sincronizzare gli aggiornamenti software in una data e a un orario in cui le richieste dal server WSUS, dal server del sito e dalla rete sono ridotte, come alle 2.00 una volta a settimana. In alternativa, è possibile avviare la sincronizzazione nel sito principale usando l'azione **Sincronizzazione degli aggiornamenti software** dal nodo **Tutti gli aggiornamenti software** o **Gruppi di aggiornamenti software** nella console di Configuration Manager.  

> [!TIP]  
>  Pianificare la sincronizzazione degli aggiornamenti software da eseguire usando un intervallo di tempo appropriato per l'ambiente. Un tipico scenario è quello che prevede di impostare l'esecuzione della pianificazione della sincronizzazione degli aggiornamenti software poco dopo il normale rilascio di aggiornamenti della protezione Microsoft il secondo martedì di ogni mese, noto come Patch martedì. Un altro scenario frequente prevede di impostare l'esecuzione giornaliera della pianificazione della sincronizzazione degli aggiornamenti software quando si utilizzano tali aggiornamenti per fornire aggiornamenti del motore e delle definizioni di Endpoint Protection.  

 Dopo il completamento della sincronizzazione del punto di aggiornamento software, viene inviata una richiesta di sincronizzazione ai siti figlio. Se sono disponibili punti di aggiornamento software aggiuntivi in un sito primario, la richiesta di sincronizzazione viene inviata a ogni punto di aggiornamento software. Il processo viene ripetuto in ogni sito nella gerarchia.  

###  <a name="BKMK_UpdateClassifications"></a> Classificazioni degli aggiornamenti  
 Ogni aggiornamento software viene definito in base a una classificazione di aggiornamento che consente di organizzare i diversi tipi di aggiornamenti. Durante il processo di sincronizzazione, verranno sincronizzati i metadati degli aggiornamenti software per le classificazioni selezionate. Configuration Manager consente di sincronizzare gli aggiornamenti software con le classificazioni di aggiornamenti seguenti:  

-   **Aggiornamenti critici:** specifica un aggiornamento rilasciato su vasta scala per un problema specifico, che risolve un bug critico, non correlato alla sicurezza.  

-   **Aggiornamenti delle definizioni:** specifica un aggiornamento a un virus o ad altri file di definizione.  

-   **Feature Pack:** specifica le nuove funzionalità del prodotto distribuite al di fuori di una versione del prodotto e che in genere sono incluse nella versione successiva del prodotto completa.  

-   **Aggiornamenti della sicurezza:** specifica un aggiornamento rilasciato su vasta scala per un problema specifico del prodotto e correlato alla sicurezza.  

-   **Service Pack:** specifica un set cumulativo di aggiornamenti rapidi applicati a un'applicazione. Questi aggiornamenti rapidi possono includere aggiornamenti della sicurezza, aggiornamenti critici, aggiornamenti software e così via.  

-   **Strumenti:** specifica un'utilità o una funzionalità che consente di completare una o più attività.  

-   **Aggiornamenti cumulativi:** specifica un set cumulativo di aggiornamenti rapidi inclusi nello stesso pacchetto per facilitarne la distribuzione. Questi aggiornamenti rapidi possono includere aggiornamenti della sicurezza, aggiornamenti critici, aggiornamenti e così via. Un aggiornamento cumulativo è relativo in genere a un'area specifica, ad esempio la sicurezza o un componente del prodotto.  

-   **Aggiornamenti:** specifica un aggiornamento di un'applicazione o un file attualmente installato.  

 Le impostazioni delle classificazioni di aggiornamento vengono configurate solo nel sito di livello superiore. Tali impostazioni non vengono configurate nel punto di aggiornamento software dei siti figlio poiché i metadati degli aggiornamenti software vengono replicati dal sito di livello superiore nei siti primari figlio. Quando si selezionano le classificazioni di aggiornamento, tenere presente che quante più classificazioni vengono selezionate tanto maggiore sarà il tempo richiesto per la sincronizzazione dei metadati degli aggiornamenti software.  

> [!WARNING]  
>  È consigliabile deselezionare tutte le classificazioni prima di sincronizzare gli aggiornamenti software per la prima volta. Dopo la sincronizzazione iniziale, selezionare le classificazioni dalle Proprietà del componente del punto di aggiornamento software, quindi riavviare la sincronizzazione.  

###  <a name="BKMK_UpdateProducts"></a> Prodotti  
 I metadati per ogni aggiornamento software definiscono uno o più prodotti per i quali l'aggiornamento è applicabile. Un prodotto è un'edizione specifica di un sistema operativo o di un'applicazione. Un esempio di un prodotto è Microsoft Windows Server 2008. Una famiglia di prodotti è il sistema operativo o l'applicazione di base da cui derivano i singoli prodotti. Un esempio di famiglia di prodotti è Microsoft Windows, di cui Microsoft Windows Server 2008 è membro. È possibile specificare una famiglia di prodotti o singoli prodotti all'interno di una famiglia di prodotti.  

 Se gli aggiornamenti software sono applicabili a più prodotti e almeno uno dei prodotti è selezionato per la sincronizzazione, tutti i prodotti verranno visualizzati nella console di Configuration Manager anche se alcuni prodotti non sono stati selezionati. Se, ad esempio, Windows Server 2012 è il solo sistema operativo sottoscritto e se un aggiornamento software si applica a Windows Server 2012 e Windows Server 2012 Datacenter Edition, entrambi i prodotti si troveranno nel database del sito.  

 Solo nel sito di livello superiore vengono configurate le impostazioni del prodotto. Tali impostazioni non vengono configurate nel punto di aggiornamento software per i siti figlio poiché i metadati degli aggiornamenti software vengono replicati dal sito di livello superiore ai siti primari figlio. Quando si selezionano i prodotti, tenere presente che quanti più prodotti vengono selezionati tanto maggiore sarà il tempo richiesto per la sincronizzazione dei metadati degli aggiornamenti software.  

> [!IMPORTANT]  
>  Configuration Manager archivia un elenco di prodotti e di famiglie di prodotti tra cui è possibile scegliere quando si installa per la prima volta il punto di aggiornamento software. È possibile che i prodotti e le famiglie di prodotti pubblicati dopo il rilascio di Configuration Manager non siano disponibili per la selezione finché non si completa la sincronizzazione degli aggiornamenti software, che aggiorna l'elenco di prodotti e famiglie di prodotti disponibili tra cui è possibile scegliere. È consigliabile deselezionare tutti i prodotti prima di sincronizzare gli aggiornamenti software per la prima volta. Dopo la sincronizzazione iniziale, selezionare i prodotti dalle Proprietà del componente del punto di aggiornamento software, quindi riavviare la sincronizzazione.  

###  <a name="BKMK_SupersedenceRules"></a> Regole di sostituzione  
 In genere, un aggiornamento software che sostituisce un altro aggiornamento software consente di effettuare una o più delle seguenti azioni:  

-   Migliora o aggiorna la correzione fornita da uno o più aggiornamenti rilasciati in precedenza.  

-   Migliora l'efficienza del pacchetto dei file di aggiornamento sostituito, che viene installato sui computer client se l'aggiornamento viene approvato per l'installazione. Ad esempio, l'aggiornamento sostituito potrebbe contenere file che non sono più rilevanti per la correzione o i sistemi operativi supportati dal nuovo aggiornamento, quindi tali file non sono inclusi nel pacchetto di file sostituito dell'aggiornamento.  

-   Aggiorna versioni più recenti di un prodotto. In altre parole, aggiorna le versioni che non sono più applicabili alle versioni o configurazioni di un prodotto precedenti. Gli aggiornamenti possono anche sostituire altri aggiornamenti, se sono state apportate modifiche per espandere il supporto della lingua. Ad esempio, una revisione recente di un aggiornamento prodotto per Microsoft Office potrebbe rimuovere il supporto per un sistema operativo precedente, ma potrebbe aggiungere supporto aggiuntivo per nuove lingue nel rilascio di aggiornamenti iniziale.  

 Nelle proprietà del punto di aggiornamento software, è possibile specificare di applicare immediatamente la scadenza agli aggiornamenti software sostituiti, impedendo in tal modo che siano inclusi nelle nuove distribuzioni e contrassegnando queste ultime per indicare che gli aggiornamenti software sostituiti contengono uno o più aggiornamenti scaduti. In alternativa, è possibile specificare un periodo di tempo prima della scadenza degli aggiornamenti software sostituiti, che consente di continuare a distribuirli. Prendere in considerazione i seguenti scenari in cui potrebbe essere necessario distribuire un aggiornamento software sostituito:  

-   Se l'aggiornamento software che sostituisce supporta solo versioni più recenti di un sistema operativo e alcuni dei computer client eseguono versioni precedenti del sistema operativo.  

-   Se l'aggiornamento software che sostituisce ha un'applicabilità più limitata dell'aggiornamento software sostituito. Questo potrebbe renderlo inappropriato per alcuni computer client.  

-   Se l'aggiornamento software che sostituisce non è stato approvato per la distribuzione nell'ambiente di produzione.  

    > [!NOTE]  
    > Quando Configuration Manager imposta un aggiornamento software sostituito su **Scaduto**, non imposta l'aggiornamento su **Rifiutato** in WSUS. Quando però viene eseguita l'attività di pulizia di WSUS, gli aggiornamenti impostati su **Scaduto** in Configuration Manager vengono impostati su **Rifiutato** nel server WSUS e l'agente di Windows Update nei computer non effettuerà più l'analisi di questi aggiornamenti. I client continueranno quindi ad eseguire l'analisi per un aggiornamento scaduto fino all'esecuzione dell'attività di pulizia. Per informazioni sull'attività di pulizia di WSUS, vedere [Manutenzione degli aggiornamenti software](/sccm/sum/deploy-use/software-updates-maintenance).

###  <a name="BKMK_UpdateLanguages"></a> Lingue  
 Le impostazioni della lingua per il punto di aggiornamento software consentono di configurare le lingue per cui sono sincronizzati i dettagli di riepilogo (metadati degli aggiornamenti software) per gli aggiornamenti software e le lingue dei file di aggiornamento software che saranno scaricate per gli aggiornamenti software.  

#### <a name="software-update-file"></a>File di aggiornamento software  
 Le lingue configurate per l'impostazione **File di aggiornamento software** nelle proprietà per il punto di aggiornamento software forniscono l'impostazione predefinita delle lingue quando si scaricano gli aggiornamenti software in un sito. È possibile modificare le lingue selezionate per impostazione predefinita ogni volta che gli aggiornamenti software vengono scaricati o distribuiti. Durante il processo di download, i file di aggiornamento software per le lingue configurate vengono scaricati nel percorso di origine del pacchetto di distribuzione, se i file di aggiornamento software sono disponibili nella lingua selezionata. Quindi, vengono copiati nella raccolta contenuto nel server del sito e poi nei punti di distribuzione configurati per il pacchetto.  

 Le impostazioni della lingua dei file di aggiornamento software devono essere configurate con le lingue che vengono più spesso utilizzate nell'ambiente. Ad esempio, se i computer client assegnati al sito utilizzano di più l'inglese e il giapponese per il sistema operativo e le applicazioni e nel sito vengono utilizzate pochissime altre lingue, selezionare l'inglese e il giapponese nella colonna **File di aggiornamento software** quando si scarica o si distribuisce l'aggiornamento software e deselezionare le altre lingue. Questo consente di utilizzare le impostazioni predefinite nella pagina **Selezione lingua** della distribuzione e di scaricare le procedure guidate. Ciò impedisce inoltre il download di file di aggiornamento che non sono necessari. Questa impostazione è configurata in ogni punto di aggiornamento software della gerarchia di Configuration Manager.  

#### <a name="summary-details"></a>Dettagli di riepilogo  
 Durante il processo di sincronizzazione, le informazioni dei dettagli di riepilogo (metadati degli aggiornamenti software) vengono aggiornate per gli aggiornamenti software nelle lingue specificate. I metadati forniscono le informazioni sull'aggiornamento software, come il nome, la descrizione, i prodotti supportati dall'aggiornamento, la classificazione dell'aggiornamento, l'ID articolo, l'URL di download, le regole di applicabilità e così via.  

 Solo nel sito di livello superiore vengono configurate le impostazioni dei dettagli di riepilogo. I dettagli di riepilogo non vengono configurati nel punto di aggiornamento software nei siti figlio poiché i metadati degli aggiornamenti software vengono replicati dal sito di amministrazione centrale in tali siti utilizzando la replica basata su file. Quando si selezionano le lingue dei dettagli di riepilogo, selezionare solo le lingue necessarie per l'ambiente. Più lingue vengono selezionate, maggiore è il tempo necessario per sincronizzare i metadati degli aggiornamenti software. Configuration Manager consente di visualizzare i metadati degli aggiornamenti software nelle impostazioni locali del sistema operativo in cui viene eseguita la console di Configuration Manager. Se le proprietà localizzate per gli aggiornamenti software non sono disponibili in locale nel sistema operativo, le informazioni degli aggiornamenti software vengono visualizzate in inglese.  

> [!IMPORTANT]  
>  È importante selezionare tutte le lingue dei dettagli di riepilogo che saranno necessarie nella gerarchia di Configuration Manager. Quando il punto di aggiornamento software nel sito di livello superiore viene sincronizzato con l'origine di sincronizzazione, le lingue dei dettagli di riepilogo selezionate determinano i metadati degli aggiornamenti software recuperati. Se si modificano le lingue dei dettagli di riepilogo dopo che la sincronizzazione è stata eseguita almeno una volta, i metadati degli aggiornamenti software vengono recuperati per le lingue dei dettagli di riepilogo modificate solo per aggiornamenti software nuovi o modificati. Gli aggiornamenti software che sono già stati sincronizzati non vengono aggiornati con i nuovi metadati per le lingue modificate a meno che non ci sia una modifica all'aggiornamento software nell'origine di sincronizzazione.  

##  <a name="BKMK_MaintenanceWindow"></a> Piano per una finestra di manutenzione di aggiornamenti software  
 È possibile aggiungere una finestra di manutenzione dedicata per l'installazione di aggiornamenti software. Consente di configurare una finestra di manutenzione generale e una finestra di manutenzione diversa per gli aggiornamenti software. Quando una finestra di manutenzione generale e una finestra di manutenzione degli aggiornamenti software sono entrambe configurate, i client installano aggiornamenti software solo nella finestra di manutenzione degli aggiornamenti software. Per altre informazioni sulle finestre di manutenzione, vedere [Come usare le finestre di manutenzione](../../core/clients/manage/collections/use-maintenance-windows.md).  

##  <a name="BKMK_RestartOptions"></a> Opzioni di riavvio per i client Windows 10 dopo l'installazione degli aggiornamenti software
Quando un aggiornamento software che richiede il riavvio viene distribuito tramite Configuration Manager e viene installato in un computer, viene pianificato un riavvio in sospeso e viene visualizzata una finestra di dialogo di riavvio.

A partire da Configuration Manager versione 1606, ogni volta che è pianificato un riavvio in sospeso per un aggiornamento software di Configuration Manager nei computer Windows 10 tra le opzioni di risparmio energia di Windows sono disponibili le opzioni **Aggiorna e riavvia**e **Aggiorna e arresta** . Dopo che una di queste opzioni è stata usata e il computer è stato riavviato, la finestra di dialogo di riavvio non verrà visualizzata.

Nelle versioni precedenti di Configuration Manager, se in un computer Windows 8 e versioni successive è presente un riavvio in sospeso e se si arresta o si riavvia il computer tramite le opzioni di risparmio energia di Windows, anziché dalla finestra di dialogo di riavvio, la finestra di dialogo di riavvio viene ancora visualizzata dopo il riavvio del computer e sarà necessario riavviare di nuovo il computer in corrispondenza della scadenza configurata.

## <a name="next-steps"></a>Passaggi successivi
Quando si pianificano gli aggiornamenti software, vedere [Preparare la gestione degli aggiornamenti software](../get-started/prepare-for-software-updates-management.md).

---
title: Piano per il provider SMS
titleSuffix: Configuration Manager
description: Informazioni sul ruolo Provider SMS del sistema del sito in Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f113599fb25140effc809896ebf6d79772bf7797
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75799795"
---
# <a name="plan-for-the-sms-provider"></a>Piano per il provider SMS

*Si applica a: Configuration Manager (Current Branch)*

Per la gestione di Configuration Manager, usare una console di Configuration Manager che si connette a un'istanza del **provider SMS**. Per impostazione predefinita, quando si installa un sito di amministrazione centrale o un sito primario, nel server del sito viene installato un provider SMS.


## <a name="BKMK_PlanSMSProv"></a> Informazioni sul provider SMS  

Il provider SMS è un provider di Strumentazione gestione Windows (WMI) che assegna l'accesso di **lettura** e **scrittura** del database di Configuration Manager a un sito.  

- Ogni sito di amministrazione centrale e sito primario richiede almeno un provider SMS. È possibile installare altri provider in base alle esigenze.  

- Il gruppo di sicurezza **SMS Admins** fornisce l'accesso al provider SMS. Configuration Manager crea automaticamente questo gruppo nel server del sito e in ogni computer in cui è installata un'istanza del provider SMS. Per ulteriori informazioni, vedere [SMS Admins](/sccm/core/plan-design/hierarchy/accounts#sms-admins).  

- I siti secondari non supportano il ruolo Provider SMS.  

Gli utenti amministratori di Configuration Manager usano un provider SMS per accedere alle informazioni archiviate nel database. A questo scopo, gli amministratori possono usare la console di Configuration Manager, Esplora inventario risorse, strumenti e script personalizzati. Il provider SMS non interagisce con i client di Configuration Manager. Quando una console di Configuration Manager si connette a un sito, esegue una query WMI sul server del sito per individuare un'istanza del provider SMS da usare.  

Il provider SMS consente di imporre la sicurezza di Configuration Manager. Restituisce solo le informazioni che l'utente della console è autorizzato a visualizzare.  

A partire dalla versione 1810, Il provider SMS fornisce ora l'accesso per l'interoperabilità API di sola lettura a WMI su HTTPS, chiamato il **servizio di amministrazione**. Questa API REST può essere usata al posto di un servizio Web personalizzato per accedere alle informazioni dal sito. Per altre informazioni, vedere [Servizio di amministrazione](#bkmk_admin-service).

> [!IMPORTANT]  
> Quando ogni istanza del provider SMS per un sito è offline, le console di Configuration Manager non possono connettersi al quel sito.  

Per altre informazioni su come gestire il provider SMS, vedere [Gestire il provider SMS](/sccm/core/servers/manage/modify-your-infrastructure#BKMK_ManageSMSprovider).  


## <a name="installation-prerequisites"></a>Prerequisiti di installazione  

Per supportare il provider SMS, il server di destinazione deve soddisfare i prerequisiti seguenti:  

- Essere incluso nello stesso dominio dei sistemi del sito del server del sito e del database del sito  

- Non disporre di un ruolo del sistema del sito da un sito differente  

- Non disporre già di un provider SMS da qualsiasi sito  

- Eseguire una versione del sistema operativo supportata  

- Almeno 650 MB di spazio libero su disco per supportare i componenti di Windows ADK. Per altre informazioni su Windows ADK e il provider SMS, vedere [Requisiti di distribuzione del sistema operativo](#BKMK_WAIKforSMSProv).  

- Abilitare il ruolo server di Windows **Server Web (IIS)**  

    > [!Note]  
    > Ogni provider SMS tenta di installare il [servizio di amministrazione](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_admin-service) che richiede un certificato. Questo servizio ha una dipendenza in IIS per associare il certificato alla porta HTTPS 443. Se si abilita [HTTP migliorato](/sccm/core/plan-design/hierarchy/enhanced-http), il sito associa il certificato tramite le API IIS. Se il sito usa l'infrastruttura a chiave pubblica (PKI), è necessario associare manualmente un certificato PKI in IIS nel provider SMS.  


## <a name="bkmk_location"></a> Sedi  

Quando si installa un sito, viene installato automaticamente il primo provider SMS per il sito in questione. È possibile specificare una delle seguenti sedi supportate per il provider SMS:  

- Server del sito  

- Server di database del sito  

- Un altro server che soddisfi i [prerequisiti di installazione](#installation-prerequisites)  

Per visualizzare le sedi di ciascun provider SMS per un sito:

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare il nodo **Siti**.  

2. Selezionare il sito desiderato dall'elenco e quindi scegliere **Proprietà** nella barra multifunzione.  

3. Nella scheda **Generale** delle **Proprietà** del sito, visualizzare il campo **Percorso provider SMS**.  

Ogni provider SMS supporta connessioni simultanee da più richieste. Gli unici limiti su queste connessioni sono il numero di connessioni server disponibili per Windows e le risorse disponibili sul server per rispondere alle richieste di connessione.  

Dopo l'installazione di un sito, è possibile eseguire nuovamente il programma di installazione di Configuration Manager nel server del sito. Usare il programma di installazione per modificare la sede di un provider SMS esistente oppure per installare provider SMS aggiuntivi in quel sito. Installare un solo provider SMS per computer. Un computer non può ospitare un provider SMS per più siti.  

### <a name="choosing-a-location"></a>Scelta di una sede

Le sezioni seguenti descrivono i vantaggi e gli svantaggi dell'installazione di un provider SMS in ogni sede supportata:  

#### <a name="configuration-manager-site-server"></a>Server del sito di Configuration Manager

- **Vantaggi:**  

    - Il provider SMS non usa le risorse del sistema del computer del database del sito.  

    - Questa sede consente di garantire prestazioni migliori rispetto a un provider SMS situato su un computer diverso dal server del sito o dal computer del database del sito.  

- **Svantaggi:**  

    - Il provider SMS usa risorse di sistema e di rete che potrebbero essere dedicate alle operazioni del server del sito.  

#### <a name="sql-server-that-hosts-the-site-database"></a>SQL Server che ospita il database del sito

- **Vantaggi:**  

    - Il provider SMS non usa risorse di sistema del sito sul server del sito.  

    - Questa sede consente di offrire le migliori prestazioni, se sono disponibili sufficienti risorse server.  

- **Svantaggi:**  

    - Il provider SMS usa risorse di sistema e di rete che potrebbero essere dedicate alle operazioni del database del sito.  

    - Quando il database del sito è ospitato su un'istanza del cluster di SQL Server, non è possibile usare questa sede.  

#### <a name="computer-other-than-the-site-server-or-site-database-server"></a>Computer diverso dal server del sito o dal computer del database del sito

- **Vantaggi:**  

    - Il provider SMS non usa il server del sito o le risorse del computer del database del sito.  

    - Questo tipo di sede consente di distribuire altri provider SMS per garantire un'elevata disponibilità per le connessioni.  

- **Svantaggi:**  

    - Le prestazioni del provider SMS potrebbero risultare ridotte. Questo comportamento può essere la conseguenza dell'attività di rete aggiuntiva richiesta per il coordinamento con il server del sito e il computer del database del sito.  

    - Questo server deve essere sempre accessibile al server del database del sito e a tutti i computer in cui è installata la console di Configuration Manager.  

    - Questa sede consente di usare le risorse di sistema altrimenti dedicate ad altri servizi.  


## <a name="bkmk_auth"></a> Autenticazione

<!--1357013-->
A partire dalla versione 1810, è possibile specificare il livello di autenticazione minimo per gli amministratori per l'accesso ai siti di Configuration Manager. Questa funzionalità impone agli amministratori di accedere a Windows con il livello richiesto. Si applica a tutti i componenti che accedono al provider SMS. Ad esempio, la console di Configuration Manager, i metodi dell'SDK e i cmdlet di Windows PowerShell.

### <a name="configure-authentication"></a>Configura autenticazione

Per configurare questa impostazione, accedere prima di tutto a Windows con il livello di autenticazione desiderato.

> [!Important]  
> Questa configurazione è un'impostazione a livello di gerarchia. Prima di modificare questa impostazione, assicurarsi che tutti gli amministratori di Configuration Manager possano accedere a Windows con il livello di autenticazione richiesto.

Attenersi alla procedura seguente per configurare questa impostazione:

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**.  

2. Selezionare **Impostazioni gerarchia** sulla barra multifunzione.  

3. Passare alla scheda **Autenticazione**. Selezionare il [livello di autenticazione](#authentication-levels) desiderato, quindi selezionare **OK**.  

    - Solo se necessario, selezionare **Aggiungi** per escludere utenti o gruppi specifici. Per altre informazioni, vedere [Esclusioni](#exclusions).  

### <a name="authentication-levels"></a>Livelli di autenticazione

Sono disponibili i livelli seguenti:

- **Autenticazione di Windows**: richiede l'autenticazione con le credenziali del dominio di Active Directory. Questa impostazione corrisponde al comportamento precedente ed è l'impostazione predefinita corrente. Quando si aggiorna il sito, non viene apportata alcuna modifica al livello di autenticazione.  

- **Autenticazione del certificato**: richiede l'autenticazione con un certificato valido emesso da un'autorità di certificazione PKI attendibile. Questo certificato non viene configurato in Configuration Manager. Configuration Manager richiede che l'amministratore acceda a Windows usando l'infrastruttura a chiave pubblica (PKI).  

- **Autenticazione di Windows Hello for Business**: richiede l'autenticazione a due fattori avanzata associata a un dispositivo e l'uso di dati biometrici o di un PIN. Per altre informazioni, vedere [Windows Hello for Business](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

### <a name="exclusions"></a>Esclusioni

Dalla scheda **Autenticazione** in Impostazioni gerarchia, è anche possibile escludere determinati utenti o gruppi. Usare questa opzione solo se necessario. Ad esempio, quando utenti specifici richiedono l'accesso alla console di Configuration Manager, ma non è possibile eseguire l'autenticazione per Windows al livello richiesto. Potrebbe anche essere necessario per l'automazione o per i servizi eseguiti nel contesto di un account di sistema.


## <a name="BKMK_SMSProvLanguages"></a> Lingue del provider SMS  

Il provider SMS funziona indipendentemente dalla lingua di visualizzazione del server su cui è installato.  

Quando un utente amministratore o un processo di Configuration Manager richiede dei dati tramite il provider SMS, quest'ultimo prova a restituirli in un formato compatibile con la lingua del sistema operativo del computer richiedente.

Il modo in cui tenta di stabilire una corrispondenza con la lingua è indiretto. Il provider SMS non traduce le informazioni da una lingua all'altra. Quando i dati vengono restituiti per la visualizzazione nella console di Configuration Manager, la lingua di visualizzazione dipenderà dall'origine dell'oggetto e dal tipo di archiviazione.  

Quando Configuration Manager memorizza i dati di un oggetto nel database, le lingue disponibili variano a seconda dei fattori seguenti:  

- Gli oggetti creati da Configuration Manager vengono memorizzati nel database usando il supporto per più lingue. L'oggetto viene memorizzato nel database del sito usando le lingue configurate per il sito al momento dell'installazione. Tali oggetti vengono visualizzati nella console di Configuration Manager nella lingua di visualizzazione del computer richiedente, se tale lingua è disponibile per l'oggetto. Se l'oggetto non può essere visualizzato nella lingua di visualizzazione del computer richiedente, sarà visualizzato nella lingua predefinita, ovvero l'inglese.  

- Gli oggetti creati da un utente amministratore vengono memorizzati con la lingua usata per creare l'oggetto. Questi oggetti vengono visualizzati nella console di Configuration Manager in questa stessa lingua. Il provider SMS non può tradurli e non dispongono di opzioni multilingue.  


## <a name="BKMK_MultiSMSProv"></a> Usare più provider SMS  

Al termine dell'installazione di un sito, è possibile installare altri provider SMS per il sito. Per installare altri provider SMS, eseguire il programma di installazione di Configuration Manager nel server del sito.

Si consiglia di installare altri provider SMS in presenza di almeno una delle seguenti condizioni:  

- Molti utenti amministratori eseguiranno la console di Configuration Manager e si connetteranno contemporaneamente a un sito.  

- Si userà l'SDK di Configuration Manager, o altri prodotti, e ciò potrebbe comportare chiamate frequenti al provider SMS.  

- Per esigenza aziendale la disponibilità del provider SMS deve essere elevata.  

Quando più provider SMS sono installati in un sito e viene eseguita una richiesta di connessione, il sito assegna in modo casuale ogni nuova richiesta di connessione per usare un provider SMS installato. Non è possibile specificare il provider SMS da usare con una sessione di connessione specifica.  

> [!NOTE]  
> Considerare i vantaggi e gli svantaggi di ciascuna sede del provider SMS Per ulteriori informazioni, vedere [Sedi](#bkmk_location). Bilanciare queste considerazioni con il fatto che non è possibile controllare quale provider SMS verrà usato per ciascuna connessione.  

Quando si connette per la prima volta una console di Configuration Manager a un sito, la connessione esegue una query WMI sul server del sito. Questa query identifica un'istanza del provider SMS che la console utilizza. Questa istanza specifica del provider SMS viene usata dalla console fino al termine della sessione. Se la sessione viene interrotta perché il server del provider SMS non è disponibile sulla rete, quando la console si riconnette al sito viene ripetuta la query iniziale. È possibile che il sito assegni la stessa istanza del provider SMS non disponibile. In tal caso, provare a riconnettere la console fino a che il sito restituisce un provider SMS disponibile.  


## <a name="BKMK_SMSProvNamespace"></a> Spazio dei nomi del provider SMS  

Lo schema WMI di Configuration Manager definisce la struttura del provider SMS. Gli spazi dei nomi dello schema descrivono il percorso dei dati di Configuration Manager all'interno dello schema del provider SMS. Nella tabella seguente sono riportati alcuni degli spazi dei nomi comuni che il provider SMS usa:  

|Spazio dei nomi|Descrizione|  
|---------------|-----------------|  
|`Root\SMS\site_<site code>`|Provider SMS, usato largamente dalla console di Configuration Manager, da Esplora inventario risorse, dagli script e dagli strumenti di Configuration Manager.|  
|`Root\SMS\SMS_ProviderLocation`|Percorso dei computer del provider SMS per un sito.|  
|`Root\CIMv2`|Percorso di inventario per le informazioni sullo spazio dei nomi WMI durante l'inventario hardware e software.|  
|`Root\CCM`|Criteri di configurazione del client di Configuration Manager e dati client.|  
|`Root\CIMv2\SMS`|La posizione delle classi di report di inventario raccolte da Inventory Client Agent. I client compilano queste impostazioni durante la valutazione dei criteri del computer. Queste impostazioni sono basate sulla configurazione delle impostazioni client per il computer.|  


## <a name="BKMK_WAIKforSMSProv"></a> Requisiti di distribuzione del sistema operativo

Il computer in cui si installa un'istanza del provider SMS richiede una versione supportata di Windows ADK.  

Per altre informazioni su questo requisito, vedere [Requisiti dell'infrastruttura per la distribuzione del sistema operativo](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment#windows-adk-for-windows-10) e [Supporto per Windows 10](/sccm/core/plan-design/configs/support-for-windows-10).  

Quando si gestiscono le distribuzioni del sistema operativo, Windows ADK consente al provider SMS di completare varie attività, tra cui:  

- Visualizzare i dettagli del file WIM  

- Aggiungere file driver a immagini di avvio esistenti  

- Creare file ISO di avvio  

L'installazione di Windows ADK può richiedere fino a 650 MB di spazio libero su disco in ogni computer che installa il provider SMS. Questo requisito di una grande quantità di spazio su disco è necessario affinché Configuration Manager installi le immagini di avvio di Windows PE.  


## <a name="bkmk_admin-service"></a> Servizio di amministrazione

<!--3607711, fka 1321523-->

> [!Tip]  
> Questa funzionalità è stata introdotta per la prima volta nella versione 1810 come [funzionalità di versione non definitiva](/sccm/core/servers/manage/pre-release-features). A partire dalla versione 1906, non è più una funzionalità di versione non definitiva.  

A partire dalla versione 1810, il provider SMS fornisce l'accesso per l'interoperabilità API di sola lettura a WMI su HTTPS, chiamato il **servizio di amministrazione**. Questa API REST può essere usata al posto di un servizio Web personalizzato per accedere alle informazioni dal sito.

Il formato di URL per il **servizio di amministrazione** è `https://<servername>/AdminService/wmi/<ClassName>`, in cui `<servername>` è il server in cui è installato il provider SMS e `<ClassName>` è un nome di classe WMI di Configuration Manager valido. Nella versione 1810, il nome della classe non include il prefisso `SMS_`. Nella versione 1902 e versioni successive, il nome della classe è lo stesso del nome della classe WMI.

Ad esempio:

- 1810: `https://servername/AdminService/wmi/Site`
- 1902 e versioni successive: `https://servername/AdminService/wmi/SMS_Site`

> [!Note]  
> I nomi delle classi del servizio di amministrazione distinguono tra maiuscole e minuscole. Assicurarsi di usare le maiuscole/minuscole correttamente, ad esempio SMS_Site.

Effettuare chiamate dirette a questo servizio con il cmdlet di Windows PowerShell [Invoke-RestMethod](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/invoke-restmethod).

> [!Tip]  
> È possibile usare questo cmdlet in una sequenza di attività. Questa azione consente di accedere alla informazioni dal sito senza richiedere un servizio Web personalizzato che si interfacci con il provider WMI.

È anche possibile usarlo per accedere ai dati del sito da Power BI con l'opzione del connettore OData.

Il servizio di amministrazione registra l'attività nel file **adminservice.log**.

### <a name="enable-the-administration-service-through-the-cmg"></a>Abilitare il servizio di amministrazione tramite CMG

Il **provider SMS** viene visualizzato come un ruolo con un'opzione per consentire la comunicazione sul Cloud Management Gateway (CMG). Questa impostazione attualmente viene usata per abilitare le approvazioni delle applicazioni tramite posta elettronica da un dispositivo remoto. Per altre informazioni, vedere [Approvare le applicazioni](/sccm/apps/deploy-use/app-approval).

#### <a name="prerequisites"></a>Prerequisiti

- Il server che ospita il provider SMS richiede .NET 4.5.2 o versione successiva.  

    - A partire dalla versione 1902, questo prerequisito è la versione .NET 4.5 o successiva.  

- Consentire al provider SMS di usare un certificato. Usare una delle seguenti opzioni:  

    - Abilitare [HTTP avanzato](/sccm/core/plan-design/hierarchy/enhanced-http) (scelta consigliata)  

        > [!Note]  
        > Quando il sito crea un certificato per il provider SMS, non verrà considerato attendibile dal Web browser nel client. In base alle impostazioni di sicurezza, quando si accede al provider REST potrebbe essere visualizzato un avviso di sicurezza.  

    - Associare manualmente un certificato basato su PKI alla porta 443 in IIS sul server che ospita il ruolo Provider SMS  

#### <a name="process-to-enable-the-api-through-the-cmg"></a>Processo per abilitare l'API tramite il CMG

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare il nodo **Server e ruoli del sistema del sito**.  

2. Selezionare il server con il ruolo **Provider SMS**.  

3. Nel riquadro dei dettagli selezionare il ruolo **Provider SMS** e selezionare **Proprietà** nella barra multifunzione nella scheda **Ruolo del sito**.  

4. Selezionare l'opzione **Consenti il traffico di Configuration Manager Cloud Management Gateway per il servizio di amministrazione**.  


### <a name="enable-the-configuration-manager-console-to-use-the-administration-service"></a>Abilitare la console di Configuration Manager all'uso del servizio di amministrazione

<!--4223683-->
A partire dalla versione 1906 è possibile abilitare alcuni nodi della console di Configuration Manager all'uso del servizio di amministrazione. Questa modifica consente alla console di comunicare con il provider SMS tramite HTTPS anziché tramite WMI.

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**. Sulla barra multifunzione selezionare **Impostazioni gerarchia**.

1. Nella pagina **Generali** selezionare l'opzione che consente di **abilitare la console di Configuration Manager per l'uso del servizio di amministrazione**.

Nella versione 1906 questa funzionalità interessa solo i nodi seguenti nel nodo **Sicurezza** dell'area di lavoro **Amministrazione**:

- Utenti amministratori
- Ruoli di sicurezza
- Ambiti di protezione
- Connessioni di console

Quando si seleziona uno di questi nodi, se viene visualizzato il messaggio di errore seguente:

*Configuration Manager: la connessione al servizio di amministrazione non è riuscita*

esaminare le informazioni riportate sotto l'errore. Quindi verificare che il servizio di amministrazione sia abilitato, configurato e funzionante.

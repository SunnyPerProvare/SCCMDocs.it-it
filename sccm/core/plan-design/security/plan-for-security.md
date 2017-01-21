---
title: Pianificare la sicurezza in System Center Configuration Manager | Microsoft Docs
description: Procedure consigliate e altre informazioni sulla sicurezza in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2a216814-ca8c-4d2e-bcef-dc00966a3c9f
caps.latest.revision: 6
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: dc78ecb308d385c04d821f51fc14650b306b5108


---
# <a name="plan-for-security-in-system-center-configuration-manager"></a>Pianificare la sicurezza in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare le informazioni in questo argomento per pianificare la sicurezza in System Center Configuration Manager.  

   Per altre informazioni su come Configuration Manager usa i certificati e i controlli crittografici, vedere [Riferimento tecnico per i controlli crittografici per System Center Configuration Manager](../../../protect/deploy-use/cryptographic-controls-technical-reference.md).  


##  <a name="a-namebkmkplanningforcertificatesa-planning-for-certificates-self-signed-and-pki"></a><a name="BKMK_PlanningForCertificates"></a> Pianificazione di certificati (autofirmati e PKI)  
 Configuration Manager usa una combinazione di certificati autofirmati e certificati di infrastruttura a chiave pubblica (PKI).  

 Come procedura di sicurezza consigliata, usare i certificati PKI quando possibile. Per altre informazioni sui requisiti dei certificati PKI, vedere [Requisiti dei certificati PKI per System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md). Quando Configuration Manager richiede i certificati PKI, ad esempio durante la registrazione di dispositivi mobili e il provisioning AMT, è necessario usare Active Directory Domain Services e un'autorità di certificazione aziendale. Tutti gli altri certificati PKI devono essere distribuiti e gestiti indipendentemente da Configuration Manager.  

 I certificati PKI sono inoltre richiesti quando i computer client si connettono a sistemi del sito basati su Internet e sono consigliati quando i client si connettono ai sistemi del sito che eseguono Internet Information Services (IIS). Per altre informazioni sulla comunicazione client, vedere [Come configurare porte di comunicazione client in System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md).  

 Quando si usa una PKI, è possibile usare anche IPsec per proteggere la comunicazione da server a server tra sistemi in un sito e tra siti e per qualsiasi altro scenario di trasferimento dati tra computer. È necessario configurare e implementare IPsec indipendentemente da Configuration Manager.  

 Configuration Manager è in grado di generare automaticamente certificati autofirmati se i certificati PKI non sono disponibili e alcuni certificati in Configuration Manager sono sempre autofirmati. Nella maggior parte dei casi, Configuration Manager gestisce automaticamente i certificati autofirmati e non sono necessarie azioni aggiuntive. Una possibile eccezione è il certificato di firma del server del sito. Il certificato di firma del server del sito è sempre autofirmato e assicura che i criteri che i client scaricano dal punto di gestione siano stati inviati dal server del sito e che non abbiano subito manomissioni.  

### <a name="planning-for-the-site-server-signing-certificate-self-signed"></a>Pianificazione del certificato di firma del server del sito  
 I client possono ottenere in modo protetto una copia del certificato di firma del server del sito da Servizi di dominio Active Directory e dall'installazione push client. Se i client non sono in grado di ottenere una copia del certificato di firma del server del sito tramite questi meccanismi, installare una copia di tale certificato quando si installa il client come procedura di sicurezza consigliata. Ciò è particolarmente importante se la prima comunicazione del client con il sito proviene da Internet, perché il punto di gestione è connesso a una rete non attendibile e pertanto è vulnerabile ad attacchi. Se non si adotta questa misura aggiuntiva, i client scaricano automaticamente una copia del certificato di firma del server del sito dal punto di gestione.  

 Di seguito sono elencati alcuni degli scenari in cui i client non sono in grado di ottenere in modo protetto una copia del certificato del server del sito:  

-   Il client non è installato tramite push client e si verifica una delle seguenti condizioni:  

    -   Lo schema di Active Directory non viene esteso per Configuration Manager.  

    -   Il sito del client non viene pubblicato in Active Directory Domain Services.  

    -   Il client deriva da un gruppo di lavoro o una foresta non trusted.  

-   Il client viene installato mentre si trova su Internet.  

Usare la procedura seguente per installare i client e una copia del certificato di firma del server del sito.  

##### <a name="to-install-clients-with-a-copy-of-the-site-server-signing-certificate"></a>Per installare i client con una copia del certificato di firma del server del sito  

1.  Individuare il certificato di firma del server del sito sul server del sito primario del client. Il certificato è archiviato nell'archivio certificati **SMS** e dispone del Nome oggetto **Server del sito** e del nome descrittivo **Certificato di firma del server del sito**.  

2.  Esportare il certificato senza la chiave privata, archiviare il file in modo sicuro e accedervi solo da un canale protetto (ad esempio, usando la firma SMB o IPsec).  

3.  Installare il client usando la proprietà Client.msi **SMSSIGNCERT=***&lt;percorso completo e nome file\>* con CCMSetup.exe.  

###  <a name="a-namebkmkplanningforcrlsa-planning-for-pki-certificate-revocation"></a><a name="BKMK_PlanningForCRLs"></a> Pianificazione di revoche di certificati PKI  
Quando si usano certificati PKI con Configuration Manager, pianificare se e in che modo client e server useranno un elenco di revoche di certificati (CRL) per verificare il certificato sul computer che si sta connettendo. L'elenco di revoche di certificati (CRL) è un file creato e firmato da un'autorità di certificazione (CA) e contiene un elenco di certificati rilasciati, ma revocati. I certificati possono essere revocati da un amministratore CA, ad esempio in caso di sospetta o accertata compromissione di un certificato rilasciato.  

> [!IMPORTANT]  
>  Poiché il percorso dell'elenco CRL viene aggiunto a un certificato quando viene rilasciato da una CA, assicurarsi di aver pianificato l'elenco CRL prima di distribuire qualsiasi certificato PKI che sarà usato da Configuration Manager.  

Per impostazione predefinita, IIS controlla sempre l'elenco CRL per i certificati client e questa configurazione non può essere modificata in Configuration Manager. Per impostazione predefinita, i client di Configuration Manager controllano sempre l'elenco CRL per i sistemi del sito. È possibile tuttavia disabilitare questa impostazione specificando una proprietà del sito e una proprietà CCMSetup. Quando si gestiscono computer basati su Intel AMT fuori banda, è possibile anche abilitare il controllo CRL per il punto di servizio fuori banda e per i computer che eseguono la console di gestione fuori banda.  

Se i computer usano il controllo delle revoche di certificati ma non sono in grado di individuare l'elenco CRL, si comportano come se tutti i certificati nella catena di certificazione fossero revocati dal momento che non è possibile verificare la loro assenza dall'elenco. In questo scenario, non sarà possibile stabilire alcuna connessione che richieda certificati e usi un elenco CRL.  

Il controllo dell'elenco CRL a ogni utilizzo di un certificato offre una maggiore protezione rispetto all'utilizzo di un certificato revocato, ma comporta un ritardo nella connessione e un'ulteriore elaborazione nel client. È più probabile che questo controllo di sicurezza aggiuntivo sia richiesto quando i client si trovano su Internet o su una rete non attendibile.  

Consultare gli amministratori PKI prima di decidere se i client di Configuration Manager debbano controllare o meno l'elenco CRL e considerare la possibilità di mantenere abilitata questa opzione in Configuration Manager in presenza di entrambe le condizioni seguenti:  

-   L'infrastruttura PKI supporta un elenco CRL pubblicato dove tutti i client di Configuration Manager possono individuarlo. Tenere presente che potrebbero essere inclusi i client su Internet se si sta usando la gestione client basata su Internet nonché client in foreste non trusted.  

-   La richiesta di controllo dell'elenco CRL per ciascuna connessione a un sistema del sito configurato per l'utilizzo di un certificato PKI è superiore alla richiesta di connessioni più rapide ed elaborazione più efficiente sul client. Inoltre, tale richiesta è superiore al rischio di mancate connessioni ai server da parte dei client nel caso in cui questi ultimi non siano in grado di individuare l'elenco CRL.  

###  <a name="a-namebkmkplanningforrootcasa-planning-for-the-pki-trusted-root-certificates-and-the-certificate-issuers-list"></a><a name="BKMK_PlanningForRootCAs"></a> Pianificazione di certificati radice trusted PKI e dell'elenco di autorità di certificazione  
Se i sistemi del sito IIS usano certificati client PKI per l'autenticazione dei client su HTTP o per l'autenticazione e la crittografia dei client su HTTPS, potrebbe essere necessario importare i certificati CA radice come una proprietà del sito. I due scenari sono i seguenti:  

-   I sistemi operativi sono distribuiti tramite Configuration Manager e i punti di gestione accettano solo connessioni client HTTPS.  

-   Si usano certificati client PKI non concatenati a un certificato di un'autorità di certificazione (CA) radice considerato attendibile dai punti di gestione.  

    > [!NOTE]  
    >  Quando i certificati client PKI vengono rilasciati dalla stessa gerarchia CA che rilascia i certificati server usati per i punti di gestione, non è necessario specificare questo certificato CA radice. Se si usano più gerarchie CA e non si è certi che queste si considerino reciprocamente attendibili, importare la CA radice per la gerarchia CA dei client.  

Se è necessario importare certificati CA radice per Configuration Manager, esportarli dalla CA emittente o dal computer client. Se si esporta il certificato dalla CA emittente che corrisponde anche alla CA radice, assicurarsi che la chiave privata non venga esportata. Memorizzare il file del certificato esportato in un'ubicazione protetta per impedire eventuali manomissioni. È necessario poter accedere al file quando si configura il sito e, pertanto, in caso di accesso dalla rete, accertarsi che la comunicazione sia protetta da eventuali manomissioni usando la firma SMB o IPsec.  

Se uno dei certificati CA radice importati viene rinnovato, è necessario importare i certificati rinnovati.  

Questi certificati CA radice importati e il certificato CA radice di ogni punto di gestione creano l'elenco di autorità emittenti di certificati usato dai computer di Configuration Manager nei modi seguenti:  

-   Quando i client si connettono a un punto di gestione, questo verifica che il certificato client sia concatenato a un certificato radice attendibile presente nell'elenco di autorità emittenti di certificati del sito. Se ciò non avviene, il certificato viene rifiutato e la connessione PKI non riesce.  

-   In presenza di un elenco di autorità emittenti di certificati, i client selezionano un certificato PKI concatenato a un certificato radice trusted presente nell'elenco. In assenza di una corrispondenza, il client non seleziona un certificato PKI. Per altre informazioni sul processo dei certificati client, vedere la sezione [Planning for PKI client certificate selection](#BKMK_PlanningForClientCertificateSelection) in questo argomento.  

Indipendentemente dalla configurazione del sito, potrebbe essere anche richiesta l'importazione di un certificato CA radice quando si esegue la registrazione di dispositivi mobili o computer Mac e il provisioning di computer basati su Intel AMT per reti wireless.  

###  <a name="a-namebkmkplanningforclientcertificateselectiona-planning-for-pki-client-certificate-selection"></a><a name="BKMK_PlanningForClientCertificateSelection"></a> Planning for PKI client certificate selection  
 Se i sistemi del sito IIS usano certificati client PKI per l'autenticazione dei client su HTTP o per l'autenticazione e la crittografia dei client su HTTPS, pianificare la modalità con cui i client basati su Windows selezionano il certificato da usare per Configuration Manager.  

> [!NOTE]  
>  Non tutti i dispositivi supportano un metodo di selezione del certificato, al contrario selezionano automaticamente il primo certificato che soddisfa i requisiti del certificato. Ad esempio, i client su computer Mac e dispositivi mobili non supportano un metodo di selezione del certificato.  

In molti casi, la configurazione e il comportamento predefiniti saranno sufficienti. Il client di Configuration Manager su computer Windows filtra più certificati in base ai criteri seguenti:  

1.  Elenco di autorità di certificazione: il certificato si concatena a una CA radice considerata attendibile dal punto di gestione.  

2.  Il certificato si trova nell'archivio certificati predefinito **Personale**.  

3.  Il certificato è valido, non revocato e non è scaduto. Il controllo di validità prevede di verificare che la chiave privata sia accessibile e che il certificato non sia stato creato usando un modello di certificato della versione 3, non compatibile con Configuration Manager.  

4.  Il certificato dispone della funzionalità di autenticazione client o viene rilasciato al nome del computer.  

5.  Il certificato ha il periodo di validità più lungo.  

I client possono essere configurati per l'utilizzo dell'elenco di autorità emittenti di certificati usando i meccanismi seguenti:  

-   Viene pubblicato come informazione del sito di Configuration Manager in Active Directory Domain Services.  

-   I client vengono installati tramite push client.  

-   I client lo scaricano dal punto di gestione dopo essere stati correttamente assegnati al rispettivo sito.  

-   Viene specificato durante l'installazione del client, come una proprietà client.msi CCMSetup di CCMCERTISSUERS.  

Se i client non dispongono dell'elenco di autorità emittenti di certificati al momento dell'installazione iniziale e non sono ancora assegnati al sito, salteranno questo controllo. Quando dispongono dell'elenco di autorità emittenti di certificati ma non di un certificato PKI concatenato a un certificato radice trusted presente nell'elenco, la selezione del certificato non viene completata correttamente e i client non proseguono con gli altri criteri di selezione del certificato.  

Nella maggior parte dei casi, il client di Configuration Manager identifica correttamente un certificato PKI univoco e appropriato da usare. Tuttavia, quando ciò non accade, invece di selezionare il certificato sulla base della funzionalità di autenticazione client, è possibile configurare due metodi di selezione alternativi:  

-   Una corrispondenza della stringa parziale nel Nome oggetto del certificato client. Si tratta di una corrispondenza senza distinzione tra maiuscole e minuscole appropriata se si sta usando il nome di dominio completo (FQDN) di un computer nel campo oggetto e si vuole che la selezione del certificato sia basata sul suffisso del dominio, ad esempio **contoso.com**. Tuttavia, è possibile usare questo metodo di selezione per identificare qualsiasi stringa di caratteri sequenziali nel Nome oggetto del certificato che differenziano quest'ultimo dagli altri certificati nell'archivio certificati client.  

    > [!NOTE]  
    >  Non è possibile usare la corrispondenza della stringa parziale con il Nome alternativo del soggetto (SAN) come un'impostazione del sito. Sebbene sia possibile specificare una corrispondenza della stringa parziale per il SAN usando CCMSetup, sarà sovrascritta dalle proprietà del sito negli scenari seguenti:  
    >   
    >  -   I client recuperano informazioni del sito pubblicate in Servizi di dominio Active Directory.  
    > -   I client vengono installati tramite installazione push client.  
    >   
    >  Usare una corrispondenza della stringa parziale nel SAN solo quando si installano i client manualmente e quando questi non recuperano le informazioni del sito da Servizi di dominio Active Directory. Ad esempio, queste condizioni si applicano solo ai client Internet.  

-   Una corrispondenza nei valori attributo del nome oggetto del certificato client o nei valori attributo del nome alternativo del soggetto (SAN). Si tratta di una corrispondenza con distinzione tra maiuscole e minuscole appropriata se si sta usando un nome distinto X500 o identificatori oggetto (OID) equivalenti in conformità con RFC 3280 e si desidera che la selezione del certificato sia basata sui valori attributo. È possibile specificare solo gli attributi e i rispettivi valori richiesti per identificare o convalidare in modo univoco il certificato e differenziarlo dagli altri certificati nel relativo archivio.  

Nella tabella seguente vengono illustrati i valori attributo che Configuration Manager supporta per i criteri di selezione del certificato client.  

|Attributo OID|Attributo del nome distinto|Definizione di attributo|  
|-------------------|----------------------------------|--------------------------|  
|0.9.2342.19200300.100.1.25|DC|Componente del dominio|  
|1.2.840.113549.1.9.1|E o E-mail|Indirizzo di posta elettronica|  
|2.5.4.3|CN|Nome comune|  
|2.5.4.4|SN|Nome oggetto|  
|2.5.4.5|SERIALNUMBER|Numero di serie|  
|2.5.4.6|C|Codice paese|  
|2.5.4.7|L|Località|  
|2.5.4.8|S o ST|Nome di provincia o stato|  
|2.5.4.9|STREET|Indirizzo|  
|2.5.4.10|O|Nome organizzazione|  
|2.5.4.11|OU|Unità organizzativa|  
|2.5.4.12|T o Title|Titolo|  
|2.5.4.42|G o GN o GivenName|Nome specificato|  
|2.5.4.43|I o Initials|Iniziali|  
|2.5.29.17|(nessun valore)|Nome alternativo soggetto|  

Se viene individuato più di un certificato appropriato dopo aver applicato i criteri di selezione, è possibile ignorare la configurazione predefinita che prevede la selezione del certificato con il periodo di validità più lungo specificando che nessun certificato è selezionato. In questo scenario, il client non sarà in grado di comunicare con i sistemi del sito IIS usando un certificato PKI. Il client invia un messaggio di errore al suo punto di stato di fallback assegnato per avvisare circa l'esito negativo della selezione del certificato e consentire la modifica o il perfezionamento dei criteri di selezione del certificato. Il comportamento del client varia a seconda se la connessione non riuscita era su HTTPS o HTTP:  

-   Se la connessione non riuscita era su HTTPS: il client prova a stabilire una connessione su HTTP e usa il certificato client autofirmato.  

-   Se la connessione non riuscita era su HTTP: il client prova a stabilire un'altra connessione su HTTP usando il certificato client autofirmato.  

Per identificare un certificato client PKI univoco, è possibile inoltre specificare un archivio personalizzato diverso dall'archivio predefinito **Personale** in **Computer** . È necessario tuttavia creare questo archivio indipendentemente da Configuration Manager ed essere in grado di distribuire i certificati a questo archivio personalizzato e rinnovarli prima della scadenza del periodo di validità.  

Per informazioni su come configurare le impostazioni per i certificati client, vedere la sezione [Configurare le impostazioni per i certificati PKI client](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI) nell'argomento [Configurare la sicurezza in System Center Configuration Manager](../../../core/plan-design/security/configure-security.md).  

###  <a name="a-namebkmkplanningforpkitransitiona-planning-a-transition-strategy-for-pki-certificates-and-internet-based-client-management"></a><a name="BKMK_PlanningForPKITransition"></a> Pianificazione di una strategia di transizione per certificati PKI e gestione client basata su Internet  
Le opzioni di configurazione flessibile in Configuration Manager consentono di eseguire una transizione graduale dei client e del sito all'uso dei certificati PKI per garantire la sicurezza degli endpoint dei client. I certificati PKI forniscono una migliore protezione e consentono la gestione dei client che si trovano su Internet.  

Dato il numero di opzioni e scelte di configurazione in Configuration Manager, sono previste più modalità di transizione di un sito in modo che tutti i client usino connessioni HTTPS. Tuttavia, è possibile attenersi alla seguente procedura come guida:  

1.  Installare il sito di Configuration Manager e configurarlo in modo che i sistemi del sito accettino le connessioni client su HTTPS e HTTP.  

2.  Configurare la scheda **Comunicazione computer client** nelle proprietà del sito in modo che **Impostazioni sistema del sito** sia **HTTP o HTTPS**, quindi selezionare la casella di controllo **Usa certificato client PKI (funzionalità di autenticazione client) quando disponibile** . Configurare le altre impostazioni richieste in questa scheda. Per altre informazioni, vedere la sezione  [Configurare le impostazioni per i certificati PKI client](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureClientPKI) nell'argomento [Configurare la sicurezza in System Center Configuration Manager](../../../core/plan-design/security/configure-security.md).  

3.  Eseguire il progetto pilota di un'implementazione PKI per i certificati client. Per una distribuzione di esempio, vedere la sezione *Distribuzione del certificato client per computer Windows* dell'argomento [Esempio dettagliato di distribuzione dei certificati PKI per Configuration Manager: Autorità di certificazione di Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

4.  Installare i client usando il metodo di installazione push client. Per altre informazioni, vedere la sezione [Come installare i clienti di Configuration Manager tramite push client](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush) nell'argomento [Come distribuire client a computer Windows in System Center Configuration Manager](../../../core/clients/deploy/deploy-clients-to-windows-computers.md).  

5.  Monitorare lo stato e la distribuzione dei client usando i report e le informazioni nella console di Configuration Manager.  

6.  Tenere traccia del numero di client che usano un certificato client PKI visualizzando la colonna **Certificato client** nell'area di lavoro **Asset e conformità** , nodo **Dispositivi** .  

     È anche possibile distribuire lo strumento di valutazione della conformità HTTPS di Configuration Manager (**cmHttpsReadiness.exe**) ai computer e usare i report per visualizzare il numero di computer in grado di usare un certificato client PKI con Configuration Manager.  

    > [!NOTE]  
    >  Se il client di Configuration Manager viene installato su computer client, lo strumento **cmHttpsReadiness.exe** viene installato nella cartella *%windir%***\CCM**. Quando si esegue questo strumento sui client, è possibile specificare le opzioni seguenti:  
    >   
    >  -   /Store:&lt;name\>  
    > -   /Issuers:&lt;list\>  
    > -   /Criteria:&lt;criteria\>  
    > -   /SelectFirstCert  
    >   
    >  Queste opzioni eseguono il mapping alle proprietà Client.msi **CCMCERTSTORE**, **CCMCERTISSUERS**, **CCMCERTSEL**e **CCMFIRSTCERT** , rispettivamente. Per altre informazioni su queste opzioni, vedere [Informazioni sulle proprietà di installazione del client in System Center Configuration Manager](../../../core/clients/deploy/about-client-installation-properties.md).  

7.  Quando si è certi che un numero sufficiente di client sta usando correttamente il rispettivo certificato client PKI per l'autenticazione su HTTP, procedere nel modo seguente:  

    1.  Distribuire un certificato del server Web PKI a un server membro che eseguirà un punto di gestione aggiuntivo per il sito e configurare tale certificato in IIS. Per altre informazioni, vedere la sezione *Distribuzione del certificato del server Web per sistemi del sito che eseguono IIS* nell'argomento [Esempio dettagliato di distribuzione dei certificati PKI per Configuration Manager: Autorità di certificazione di Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

    2.  Installare il ruolo del punto di gestione su questo server e configurare l'opzione **Connessioni client** nelle proprietà del punto di gestione per **HTTPS**.  

8.  Monitorare e verificare che i client che dispongono di un certificato PKI utilizzino il nuovo punto di gestione tramite HTTPS. Per verificare ciò, è possibile usare la registrazione delle attività IIS o i contatori delle prestazioni.  

9. Riconfigurare altri ruoli del sistema del sito per l'utilizzo di connessioni client HTTPS. Se si desidera gestire i client su Internet, assicurarsi che i sistemi del sito dispongano di un FQDN Internet e configurare i singoli punti di gestione e di distribuzione in modo che accettino le connessioni client da Internet.  

    > [!IMPORTANT]  
    >  Prima di configurare i ruoli del sistema del sito per l'accettazione di connessioni da Internet, rivedere le informazioni e i prerequisiti della pianificazione per la gestione client basata su Internet. Per altre informazioni, vedere [Comunicazioni tra gli endpoint in System Center Configuration Manager](../../../core/plan-design/hierarchy/communications-between-endpoints.md).  

10. Estendere l'implementazione del certificato PKI per i client e i sistemi del sito che eseguono IIS e configurare i ruoli del sistema del sito per le connessioni client HTTPS e le connessioni Internet, come richiesto.  

11. Per una sicurezza avanzata: quando si è certi che tutti i client stanno usando un certificato client PKI per l'autenticazione e la crittografia, modificare le proprietà del sito per l'uso esclusivo di HTTPS.  

 Quando si adotta questo piano di introduzione graduale dei certificati PKI, prima per l'autenticazione solo su HTTP e poi per l'autenticazione e la crittografia su HTTPS, si riduce il rischio di client non gestiti. Si beneficerà anche della massima sicurezza supportata da Configuration Manager.  

##  <a name="a-namebkmkplanningforrtka-planning-for-the-trusted-root-key"></a><a name="BKMK_PlanningForRTK"></a> Pianificazione della chiave radice attendibile  
La chiave radice attendibile di Configuration Manager offre un meccanismo che consente ai client di Configuration Manager di verificare che i sistemi del sito appartengano alla loro gerarchia. Ogni server del sito genera una chiave di scambio per comunicare con altri siti. La chiave di scambio dal sito di livello superiore nella gerarchia viene chiamata chiave radice attendibile.  

La funzione della chiave radice attendibile in Configuration Manager è simile a quella di un certificato radice in un'infrastruttura a chiave pubblica per il fatto che tutto ciò che viene firmato dalla chiave privata della chiave radice attendibile è considerato attendibile nei livelli inferiori della gerarchia. Ad esempio, firmando il certificato del punto di gestione con la chiave privata della coppia di chiavi radice attendibili e mettendo a disposizione dei client una copia della chiave pubblica della coppia di chiavi radice attendibili, i client possono distinguere i punti di gestione presenti nella loro gerarchia da quelli assenti. I client usano WMI per memorizzare una copia della chiave radice attendibile nello spazio dei nomi **root\ccm\locationservices**.  

I client possono recuperare automaticamente la copia pubblica della chiave radice attendibile tramite due meccanismi:  

-   Lo schema di Active Directory viene esteso per Configuration Manager, il sito viene pubblicato in Active Directory Domain Services e i client possono recuperare queste informazioni sul sito da un server del catalogo globale.  

-   I client vengono installati tramite push client.  

Se i client non sono in grado di recuperare la chiave radice attendibile tramite uno di questi meccanismi, considereranno attendibile la chiave radice attendibile fornita dal primo punto di gestione con cui è stata stabilita una connessione. In questo scenario, un client potrebbe essere erroneamente indirizzato al punto di gestione di un utente malintenzionato in cui riceverebbe criteri dal punto di gestione non autorizzato. Tale azione sarebbe probabilmente opera di un utente malintenzionato esperto e potrebbe verificarsi solo in un intervallo di tempo limitato prima che il client recuperi la chiave radice attendibile da un punto di gestione valido. Tuttavia, per ridurre il rischio di un errato indirizzamento dei client a un punto di gestione non autorizzato, è possibile eseguire il pre-provisioning dei client usando la chiave radice attendibile.  

Seguire le procedure seguenti per eseguire il pre-provisioning e verificare la chiave radice attendibile per un client di Configuration Manager:  

-   Eseguire il pre-provisioning di un client usando la chiave radice attendibile tramite file.  

-   Eseguire il pre-provisioning di un client usando la chiave radice attendibile senza file.  

-   Verificare la chiave radice attendibile in un client.  

> [!NOTE]  
>  Non è necessario eseguire il pre-provisioning del client con la chiave radice attendibile se è possibile ottenerla da Servizi di dominio Active Directory o se è stata eseguita un'installazione push client. Inoltre, non è necessario eseguire il pre-provisioning dei client quando usano la comunicazione HTTPS con i punti di gestione perché l'attendibilità viene stabilita tramite i certificati PKI.  

È possibile rimuovere la chiave radice attendibile da un client usando la proprietà **RESETKEYINFORMATION = TRUE** di Client.msi con CCMSetup.exe. Per sostituire tale chiave, reinstallare il client insieme alla nuova chiave radice attendibile, usando, ad esempio, l'installazione push client o specificando la proprietà **SMSPublicRootKey** di Client.msi tramite CCMSetup.exe.  

#### <a name="to-pre-provision-a-client-with-the-trusted-root-key-by-using-a-file"></a>Per eseguire il pre-provisioning di un client con la chiave radice attendibile tramite file  

1.  In un editor di testo aprire il file *&lt;directory di Configuration Manager\>***\bin\mobileclient.tcf**.  

2.  Individuare la voce **SMSPublicRootKey=**, copiare la chiave da tale riga e chiudere il file senza apportare modifiche.  

3.  Creare un nuovo file di testo e incollare le informazioni della chiave copiate dal file mobileclient.tcf.  

4.  Salvare il file e posizionarlo in un punto in cui tutti i computer possano accedervi ma in cui sia protetto da eventuali manomissioni.  

5.  Installare il client usando un metodo di installazione che accetti le proprietà Client.msi e specificare la proprietà **SMSROOTKEYPATH=***&lt;percorso completo e nome file\>* di Client.msi.  

    > [!IMPORTANT]  
    >  Quando si specifica la chiave radice attendibile per la sicurezza aggiuntiva durante l'installazione dei client, è anche necessario specificare il codice del sito usando la proprietà **SMSSITECODE=&lt;codicesito\>** di Client.msi.  

#### <a name="to-pre-provision-a-client-with-the-trusted-root-key-without-using-a-file"></a>Per eseguire il pre-provisioning di un client con la chiave radice attendibile senza file  

1.  In un editor di testo aprire il file *&lt;directory di Configuration Manager\>***\bin\mobileclient.tcf**.  

2.  Individuare la voce SMSPublicRootKey=, annotare la chiave da tale riga o copiarla negli Appunti, quindi chiudere il file senza apportare modifiche.  

3.  Installare il client usando qualsiasi metodo di installazione che accetti le proprietà Client.msi e specificare la proprietà **SMSPublicRootKey=***&lt;chiave\>* di Client.msi, dove *&lt;chiave\>* è la stringa copiata da mobileclient.tcf.  

    > [!IMPORTANT]  
    >  Quando si specifica la chiave radice attendibile per la sicurezza aggiuntiva durante l'installazione dei client, è anche necessario specificare il codice del sito usando la proprietà **SMSSITECODE=&lt;codice del sito\>** di Client.msi.  

#### <a name="to-verify-the-trusted-root-key-on-a-client"></a>Per verificare la chiave radice attendibile in un client  

1.  Nel menu **Start** fare clic su **Esegui**, quindi digitare **Wbemtest**.  

2.  Nella finestra di dialogo **Tester Strumentazione gestione Windows** fare clic su **Connetti**.  

3.  Nella finestra di dialogo **Connetti** , nella casella **Spazio dei nomi** , digitare **root\ccm\locationservices**, quindi fare clic su **Connetti**.  

4.  Nella finestra di dialogo **Tester Strumentazione gestione Windows** , nella sezione **IWbemServices** , fare clic su **Enum classi**.  

5.  Nella finestra di dialogo **Informazioni superclasse** selezionare **Ricorsivo**, quindi fare clic su **OK**.  

6.  Nella finestra **Risultato query** scorrere fino alla fine dell'elenco, quindi fare doppio clic su **TrustedRootKey ()**.  

7.  Nella finestra di dialogo **Editor oggetti per TrustedRootKey** fare clic su **Istanze**.  

8.  Nella nuova finestra di **Risultato query** in cui vengono visualizzate le istanze di **TrustedRootKey**fare doppio clic su **TrustedRootKey=@**  

9. Nella sezione **Proprietà** della finestra di dialogo **Editor oggetti perTrustedRootKey=@**, scorrere in basso fino a **TrustedRootKey CIM_STRING**. La stringa nella colonna destra è la chiave radice attendibile. Verificarne la corrispondenza con il valore **SMSPublicRootKey** nel file *&lt;directory di Configuration Manager\>***\bin\mobileclient.tcf**.  

##  <a name="a-namebkmkplanningforsigningencryptiona-planning-for-signing-and-encryption"></a><a name="BKMK_PlanningForSigningEncryption"></a> Pianificazione di firma e crittografia  
 Quando si usano certificati PKI per tutte le comunicazioni dei client, non è necessario pianificare la firma e la crittografia per proteggere la comunicazione dei dati dei client. Tuttavia, se si configura qualsiasi sistema del sito che esegue IIS in modo da consentire le connessioni client HTTP, è necessario stabilire la modalità di protezione della comunicazione client per il sito.  

 Per proteggere i dati che i client inviano ai punti di gestione, è possibile richiedere che vengano firmati. Inoltre, è possibile richiedere che tutti i dati firmati dai client che usano HTTP vengano firmati usando l'algoritmo SHA-256. Si tratta di un'impostazione più sicura; non abilitare questa opzione a meno che tutti i client supportino SHA-256. Molti sistemi operativi supportano SHA-256 in modo nativo, ma i sistemi operativi precedenti potrebbe richiedere un aggiornamento o un hotfix. Ad esempio, i computer che eseguono Windows Server 2003 SP2 devono installare un hotfix a cui si fa riferimento nell' [articolo della Knowledge Base 938397](http://go.microsoft.com/fwlink/p/?LinkId=226666).  

 Mentre la firma consente di proteggere i dati da eventuali manomissioni, la crittografia consente di proteggere i dati dalla divulgazione di informazioni. È possibile attivare la crittografia 3DES per i dati di inventario e i messaggi di stato che i client inviano ai punti di gestione presenti nel sito. Non sarà necessario installare aggiornamenti nei client per il supporto di questa opzione, ma tenere presente l'utilizzo di CPU aggiuntivo che sarà necessario nei client e nel punto di gestione per eseguire crittografia e decrittografia.  

 Per informazioni su come configurare le impostazioni per la firma e la crittografia, vedere la sezione [Configurare la firma e la crittografia](../../../core/plan-design/security/configure-security.md#BKMK_ConfigureSigningEncryption) nell'argomento [Configurare la sicurezza in System Center Configuration Manager](../../../core/plan-design/security/configure-security.md).  

##  <a name="a-namebkmkplanningforrbaa-planning-for-role-based-administration"></a><a name="BKMK_PlanningForRBA"></a> Pianificazione dell'amministrazione basata su ruoli  
 Per informazioni, vedere [Nozioni fondamentali sull'amministrazione basata su ruoli per System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md).  



<!--HONumber=Dec16_HO3-->



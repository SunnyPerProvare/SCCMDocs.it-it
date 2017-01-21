---
title: Privacy e sicurezza per l&quot;amministrazione dei siti | Microsoft Docs
description: Ottimizzare sicurezza e privacy per l&quot;amministrazione dei siti in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1d58176e-abc0-4087-8583-ce70deb4dcf5
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: aca2169c8f5f855e84ca924ca56f6b64bba80fd6


---
# <a name="security-and-privacy-for-site-administration-in-system-center-configuration-manager"></a>Sicurezza e privacy per l'amministrazione dei siti in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In questo argomento vengono illustrate le informazioni sulla privacy per i siti e la gerarchia di System Center Configuration Manager.

##  <a name="a-namebkmksecuritysitesa-security-best-practices-for-site-administration"></a><a name="BKMK_Security_Sites"></a> Procedure di protezione ottimali per l'amministrazione del sito  
 Usare le procedure di sicurezza consigliate seguenti per proteggere i siti e la gerarchia di System Center Configuration Manager.  

 **Eseguire l'installazione solo da una fonte attendibile e proteggere il canale di comunicazione tra i supporti di installazione e il server del sito.**  

 Per impedire la manomissione dei file di origine, eseguire l'installazione da una fonte attendibile. Se si archiviano i file in rete, proteggere il percorso di rete.  

 SE si esegue l'installazione da un percorso di rete, per evitare che un utente malintenzionato manometta i file mentre vengono trasmessi in rete, utilizzare la firma IPsec o SMB tra il percorso di origine dei file di installazione e il server del sito.  

 Inoltre, se si utilizza il Downloader di installazione per scaricare i file necessari richiesti dall'installazione, assicurarsi di proteggere anche il percorso in cui tali file vengono memorizzati e proteggere il canale di comunicazione per questo percorso quando si esegue l'installazione.  

 **Estendere lo schema di Active Directory per System Center Configuration Manager e pubblicare i siti in Active Directory Domain Services.**  

 Le estensioni dello schema non sono necessarie per eseguire System Center Configuration Manager, ma creano un ambiente più sicuro perché i client e i server del sito di Configuration Manager possono recuperare le informazioni da un'origine attendibile.  

 Se i client si trovano in un dominio non attendibile, distribuire i ruoli del sistema del sito seguenti nel dominio dei client:  

-   Punto di gestione  

-   Punto di distribuzione  

-   Punto per siti Web del Catalogo applicazioni  

> [!NOTE]  
>  Un dominio attendibile per Configuration Manager richiede l'autenticazione Kerberos cosicché, se i client si trovano in un'altra foresta che non dispone di un trust tra foreste bidirezionale con la foresta del server del sito, tali client vengono considerati in un dominio non attendibile. Un trust esterno non è sufficiente a questo scopo.  

 **Utilizzare IPsec per proteggere le comunicazioni tra i server di sistema del sito e siti.**  

 Anche se Configuration Manager protegge le comunicazioni tra il server del sito e il computer su cui è in esecuzione SQL Server, Configuration Manager non protegge le comunicazioni tra i ruoli del sistema del sito e SQL Server. Solo alcuni sistemi del sito (il punto di registrazione e il punto per servizi Web del Catalogo applicazioni) possono essere configurati per HTTPS per le comunicazioni all'interno del sito.  

 Se non si utilizzano controlli aggiuntivi per proteggere questi canali da server a server, degli utenti malintenzionati potrebbero utilizzare diversi attacchi di spoofing e man-in-the-middle contro i sistemi del sito. Utilizzare la firma SMB quando non è possibile utilizzare IPsec.  

> [!NOTE]  
>  È particolarmente importante proteggere il canale di comunicazione tra il server del sito e il server di origine del pacchetto. Questa comunicazione utilizza SMB. Se non si può utilizzare IPsec per proteggere questa comunicazione, utilizzare la firma SMB per assicurarsi che i file non vengano manomessi prima che i client li scarichino e li eseguano.  

 **Non modificare i gruppi di sicurezza che Configuration Manager crea e gestisce per la comunicazione del sistema del sito.**  

 Gruppi di sicurezza:  

-   **SMS_SiteSystemToSiteServerConnection_MP_&lt;Codicesito\>**  

-   **SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;Codicesito\>**  

-   **SMS_SiteSystemToSiteServerConnection_Stat_&lt;Codicesito\>**  

Configuration Manager crea e gestisce automaticamente questi gruppi di sicurezza. Ciò include la rimozione degli account computer quando viene rimosso un ruolo del sistema del sito.  

Per garantire la continuità del servizio e dei privilegi minimi, non modificare manualmente questi gruppi.  

**Se i client non possono eseguire la query al server di catalogo globale per ottenere informazioni su Configuration Manager, gestire il processo di provisioning della chiave radice attendibile.**  

Se i client non possono eseguire la query al server di catalogo globale per ottenere informazioni su Configuration Manager, devono basarsi sulla chiave radice attendibile per autenticare i punti di gestione validi. La chiave radice attendibile viene memorizzata nel Registro di sistema client e può essere impostata tramite i criteri di gruppo o la configurazione manuale.  

Se il client non dispone di una copia della chiave radice attendibile prima di contattare un punto di gestione per la prima volta, si affida al primo punto di gestione con cui comunica. Per ridurre il rischio di un errato indirizzamento dei client a un punto di gestione non autorizzato da parte di un utente malintenzionato, è possibile eseguire il pre-provisioning dei client utilizzando la chiave radice attendibile. Per ulteriori informazioni, vedere [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

**Utilizzare numeri di porta non predefiniti.**  

Quando si utilizzano numeri di porta non predefiniti, ciò può fornire una protezione aggiuntiva perché rende più difficile per eventuali utenti malintenzionati l'esplorazione dell'ambiente in preparazione a un attacco. Se si decide di usare porte non predefinite, pianificarle prima di installare Configuration Manager e usarle in modo coerente in tutti i siti della gerarchia. Le porte di richiesta client e la riattivazione LAN sono esempi in cui è possibile utilizzare numeri di porta non predefiniti.  

**Utilizzare la separazione dei ruoli nei sistemi del sito.**  

Nonostante si possano installare tutti i ruoli del sistema del sito su un computer singolo, questa operazioni viene raramente utilizzata nelle reti di produzione perché crea un punto singolo di errore.  

**Ridurre il profilo di attacco.**  

Quando si isola ciascun ruolo del sistema del sito su un server diverso, ciò riduce la possibilità che un attacco alle vulnerabilità in un sistema del sito possa essere utilizzato contro un sistema del sito differente. Molti ruoli del sistema del sito richiedono l'installazione di Internet Information Services (IIS) sul sistema del sito e questo aumenta la superficie di attacco. Se occorre combinare i ruoli del sistema del sito per ridurre il consumo hardware, combinare ruoli del sistema del sito IIS solo con altri ruoli che richiedono IIS.  

> [!IMPORTANT]  
>  Il ruolo del punto di stato di fallback è un'eccezione. Dato che questo ruolo del sistema del sito accetta dati non autenticati dai client, il ruolo del punto di stato di fallback non deve mai essere assegnato a qualsiasi altro ruolo del sistema del sito di Configuration Manager.  


**Seguire le procedure di protezione ottimali per Windows Server ed eseguire la Configurazione guidata impostazioni di sicurezza su tutti i sistemi del sito.**  

La Configurazione guidata impostazioni di sicurezza (SCW) consente di creare un criterio di protezione applicabile a qualsiasi server della rete. Dopo aver installato il modello di System Center Configuration Manager, Configurazione guidata impostazioni di sicurezza riconosce applicazioni, servizi, porte e ruoli del sistema del sito di Configuration Manager. Consente quindi la comunicazione necessaria per Configuration Manager e blocca le comunicazioni non richieste.  

Configurazione guidata impostazioni di sicurezza è inclusa nel toolkit per System Center 2012 Configuration Manager che è possibile scaricare dall'area download di Microsoft: [System Center 2012 - Configuration Manager Component Add-ons and Extensions](http://go.microsoft.com/fwlink/p/?LinkId=251931) (System Center 2012 - Componenti aggiuntivi ed estensioni di Configuration Manager).  

**Configurare gli indirizzi IP statici per i sistemi del sito.**  

Gli indirizzi IP statici sono più facili da proteggere da attacchi di risoluzione del nome.  

Gli indirizzi IP statici rendono anche più facile la configurazione di IPsec, il che costituisce una procedura di sicurezza consigliata per proteggere la comunicazione tra i sistemi del sito in Configuration Manager.  

**Non installare altre applicazioni sui server del sistema del sito.**  

Quando si installano altre applicazioni sui server del sistema del sito, si aumenta la superficie di attacco di Configuration Manager e si rischiano problemi di incompatibilità.  

**Richiedere la firma e abilitare la crittografia come opzione del sito.**  

Abilitare le opzioni di firma e crittografia per il sito. Assicurarsi che tutti i client possano supportare l'algoritmo hash SHA-256, quindi abilitare l'opzione **Richiedi SHA-256**.  

**Limitare e monitorare gli utenti amministratori di Configuration Manager e usare l'amministrazione basata su ruoli per garantire a tali utenti le autorizzazioni minime richieste.**  

Garantire accesso amministrativo a Configuration Manager solo agli utenti attendibili, quindi concedere loro le autorizzazioni minime tramite i ruoli di sicurezza incorporati oppure personalizzando i ruoli di sicurezza. Gli utenti amministratori che possono creare, modificare e distribuire le applicazioni, la sequenza di attività, gli aggiornamenti software, gli elementi e le linee di base della configurazione possono potenzialmente controllare i dispositivi della gerarchia di Configuration Manager.  

Controllare periodicamente le assegnazioni degli utenti amministratori e il loro livello di autorizzazione per verificare le modifiche necessarie.  

Per ulteriori informazioni sulla configurazione dell'amministrazione basata su ruoli, vedere [Configure role-based administration for System Center Configuration Manager](../../../core/servers/deploy/configure/configure-role-based-administration.md).  

**Proteggere i backup di Configuration Manager e il canale di comunicazione quando si eseguono il backup e il ripristino.**  

Quando si esegue il backup di Configuration Manager, queste informazioni includono i certificati e altri dati sensibili che potrebbero essere usati da un utente malintenzionato a fini di impersonificazione.  

Utilizzare la firma SMB o IPsec quando si trasferiscono questi dati in rete e proteggere il percorso di backup.  

**Quando si esportano o importano oggetti dalla console di Configuration Manager in un percorso di rete, proteggere il percorso stesso e il canale di rete.**  

Limitare l'accesso alla cartella di rete.  

Usare la firma SMB o IPsec tra il percorso di rete e il server del sito e tra il computer su cui è in esecuzione la console di Configuration Manager e il server del sito per impedire a un eventuale utente malintenzionato di manomettere i dati esportati. Utilizzare IPsec per crittografare i dati sulla rete per impedire la divulgazione di informazioni.  

**Se un sistema del sito non riesce a effettuare la disinstallazione o smette di funzionare e non può essere ripristinato, rimuovere manualmente i certificati di Configuration Manager per il server da altri server di Configuration Manager.**  

Per rimuovere il peer disponibile nell'elenco locale, originariamente stabilito con il sistema del sito e i ruoli del sistema del sito, rimuovere manualmente i certificati di Configuration Manager per il server che ha restituito l'errore nell'archivio certificati **Persone attendibili** su altri server del sistema del sito. Ciò è particolarmente importante se si riassegna il server senza riformattarlo.  

Per ulteriori informazioni su questi certificati, vedere la sezione Controlli crittografici per la comunicazione tra server in [Riferimento tecnico per i controlli crittografici per System Center Configuration Manager](../../../protect/deploy-use/cryptographic-controls-technical-reference.md).  

**Non configurare i sistemi del sito basati su Internet per effettuare il bridging della rete perimetrale e della intranet.**  

Non configurare i server del sistema del sito come multihomed in modo che siano connessi alla rete perimetrale e alla intranet. Nonostante questa configurazione consente ai sistemi del sito basati su Internet di accettare connessioni client da Internet e dalla intranet, essa elimina un limiti di protezione tra la rete perimetrale e la intranet.  

**Se il server del sistema del sito si trova su una rete non attendibile (come una rete perimetrale), configurare il server del sito per avviare connessioni al sistema del sito.**  

Per impostazione predefinita, i sistemi del sito avviano connessioni al server del sito per il trasferimento di dati, il che può costituire un rischio di protezione quando la connessione viene avviata da una rete non attendibile a una attendibile. Quando i sistemi del sito accettano connessioni da Internet o risiedono in una foresta non trusted, configurare l'opzione del sistema del sito **Richiedi al server del sito di avviare le connessioni al sistema del sito** in modo che, dopo l'installazione del sistema del sito e di eventuali ruoli del sistema del sito, tutte le connessioni vengano avviate da una rete attendibile.  

**Se si utilizza un server proxy Web per la gestione client basata su Internet, utilizzare il bridging SSL a SSL, utilizzando la terminazione con autenticazione.**  

 Quando si configura la terminazione SSL sul server Web proxy, i pacchetti provenienti da Internet sono soggetti a verifica prima di essere inoltrati alla rete interna. Il server Web proxy autentica la connessione dal client, la termina, quindi apre una nuova connessione autenticata ai sistemi del sito basati su Internet.  

 Quando i computer client di Configuration Manager usano un server Web proxy per collegarsi ai sistemi del sito basati su Internet, l'identità client (GUID del client) viene contenuta in modo protetto all'interno del payload dei pacchetti in modo che il punto di gestione non consideri il server Web proxy come client. Se il server Web proxy non può supportare i requisiti per il bridging SSL, viene supportato anche il tunneling SSL. Si tratta di un'opzione meno sicura perché i pacchetti SSL provenienti da Internet vengono inoltrati ai sistemi del sito senza terminazione e, pertanto, non possono essere verificati per l'eventuale presenza di contenuto dannoso.  

 Se il server Web proxy non può supportare i requisiti per il bridging SSL, è possibile utilizzare il tunneling SSL. Tuttavia, si tratta di un'opzione meno sicura perché i pacchetti SSL provenienti da Internet vengono inoltrati ai sistemi del sito senza terminazione e, pertanto, non possono essere verificati per l'eventuale presenza di contenuto dannoso.  

> [!WARNING]  
>  I dispositivi mobili registrati da Configuration Manager non possono usare il bridging SSL, ma devono usare solo il tunneling SSL.  

**Configurazioni da usare se si configura il sito in modo da riattivare i computer per installare il software.**  

-   Se si utilizzano i tradizionali pacchetti di riattivazione, utilizzare broadcast unicast invece che con riferimento a subnet  

-   Se occorre utilizzare broadcast con riferimento a subnet, configurare i router in modo che consentano broadcast con riferimento a IP provenienti solo dal server del sito e solo su un numero di porta predefinito.  

Per altre informazioni sulla diversa riattivazione delle tecnologie LAN, vedere [Pianificazione della riattivazione dei client in System Center Configuration Manager](../../../core/clients/deploy/plan/plan-wake-up-clients.md).

**Se si utilizza la notifica tramite posta elettronica, configurare l'accesso autenticato al server di posta SMTP.**  

Quando possibile, utilizzare un server di posta elettronica che supporti l'accesso autenticato e l'account computer del server del sito per l'autenticazione. Se è necessario specificare un account utente per l'autenticazione, utilizzare un account che disponga dei privilegi minimi.  

##  <a name="a-namebkmksecuritysiteservera-security-best-practices-for-the-site-server"></a><a name="BKMK_Security_SiteServer"></a> Procedure di protezione ottimali per il server del sito  
 Usare le seguenti procedure di sicurezza consigliate per proteggere il server del sito di Configuration Manager.  

 **Installare Configuration Manager in un server membro invece che in un controller di dominio.**  

 Il server e i sistemi del sito di Configuration Manager non richiedono l'installazione in un controller di dominio. I controller di dominio non dispongono di un database Gestione account di protezione (SAM) locale diverso da quello del dominio. Quando si installa Configuration Manager in un server membro, è possibile mantenere gli account di Configuration Manager nel database SAM locale piuttosto che nel database del dominio.  

 Questa pratica riduce inoltre la superficie di attacco nei controller di dominio.  

 **Installare i siti secondari, evitando di copiare i file sul server del sito secondario in rete.**  

 Quando si esegue l'installazione e si crea un sito secondario, non selezionare l'opzione per copiare i file dal sito padre sul sito secondario oppure utilizzare un percorso di origine della rete. Quando si copiano dei file in rete, un utente malintenzionato esperto potrebbe assumere il controllo del pacchetto di installazione del sito secondario e manomettere i file prima che vengano installati, anche se la tempistica di questa attacco sarebbe difficile da definire. Questo attacco può essere ridotto utilizzando IPsec o SMB quando si trasferiscono i file.  

 Invece di copiare i file in rete, sul server del sito secondario, copiare i file di origine da un supporto in una cartella locale. Quindi quando si esegue l'installazione su un sito secondario, nella pagina **File di origine dell'installazione** , selezionare **Utilizza i file di origine nel seguente percorso del computer del sito secondario (più sicuro)**e specificare questa cartella.  

 Per altre informazioni, vedere la sezione relativa all'installazione di un [sito secondario](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary) nell'argomento sull'[installazione dei siti con System Center Configuration Manager](../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  

##  <a name="a-namebkmksecuritysqlservera-security-best-practices-for-sql-server"></a><a name="BKMK_Security_SQLServer"></a> Procedure di protezione ottimali per SQL Server  
 Configuration Manager usa SQL Server come database back-end. Se il database è compromesso, gli utenti malintenzionati potrebbero escludere Configuration Manager e accedere a SQL Server direttamente per lanciare attacchi tramite Configuration Manager. Gli attacchi contro SQL Server sono molto rischiosi e devono essere ridotti in modo appropriato.  

 Usare le procedure di sicurezza consigliate seguenti per proteggere SQL Server per Configuration Manager.  

 **Non usare il server del database del sito di Configuration Manager per l'esecuzione di altre applicazioni di SQL Server.**  

 Quando si aumenta l'accesso al server del database del sito di Configuration Manager, aumenta il rischio per i dati di Configuration Manager. Se il database del sito di Configuration Manager è compromesso, anche altre applicazioni sullo stesso computer di SQL Server possono essere a rischio.  

 **Configurare SQL Server per utilizzare l'autenticazione di Windows.**  

 Nonostante Configuration Manager acceda al database del sito tramite un account Windows e l'autenticazione di Windows, è comunque possibile configurare SQL Server perché usi la modalità mista di SQL Server. La modalità mista di SQL Server consente ulteriori accessi SQL per accedere al database, cosa non necessaria che aumenta la superficie di attacco.  

 **Eseguire passaggi aggiuntivi per assicurarsi che i siti secondari che utilizzano SQL Server Express dispongano degli ultimi aggiornamenti software.**  

 Quando si installa un sito primario, Configuration Manager scarica SQL Server Express dall'Area download Microsoft e copia i file nel server del sito primario. Quando si installa un sito secondario e si seleziona l'opzione che installa SQL Server Express, Configuration Manager installa la versione precedentemente scaricata e non verifica se sono disponibili nuove versioni. Per assicurarsi che il sito secondario disponga delle versioni più recenti, eseguire una delle seguenti operazioni:  

-   Dopo aver installato il sito secondario, eseguire Windows Update sul server del sito secondario.  

-   Prima di installare il sito secondario, installare manualmente SQL Server Express sul computer che eseguirà il server del sito secondario e assicurarsi di installare la versione più recente ed eventuali aggiornamenti software. Quindi installare il sito secondario e selezionare l'opzione per utilizzare un'istanza di SQL Server esistente.  

Eseguire periodicamente Windows Update per questi siti e tutte le versioni installate di SQL Server per assicurarsi che dispongano degli aggiornamenti software più recenti.  

**Seguire le procedure ottimali per SQL Server.**  

Identificare e seguire le procedure ottimali per la versione di SQL Server. Tuttavia, prendere in considerazione i seguenti requisiti per Configuration Manager:  

-   L'account computer del server del sito deve essere membro del gruppo Administrators sul computer su cui è in esecuzione SQL Server. Se si segue il suggerimento di SQL Server di "eseguire il provisioning di tutte le entità admin esplicitamente", l'account che si usa per eseguire l'installazione nel server del sito deve essere membro del gruppo di utenti di SQL.  

-   Se si installa SQL Server utilizzando un account utente di dominio, assicurarsi che l'account computer del server del sito sia configurato per un nome dell'entità di servizio (SPN) che viene pubblicato nei Servizi di dominio Active Directory. Senza SPN, l'autenticazione Kerberos avrà esito negativo e così anche l'installazione di Configuration Manager.  

##  <a name="a-namebkmksecurityiisa-security-best-practices-for-site-systems-that-run-iis"></a><a name="BKMK_Security_IIS"></a> Procedure di protezione ottimali per i sistemi del sito su cui è in esecuzione IIS  
Diversi ruoli del sistema del sito in Configuration Manager richiedono IIS. Proteggendo IIS si consente il funzionamento corretto di Configuration Manager e si riduce il rischio di attacchi alla sicurezza. Quando è possibile, ridurre al minimo il numero di server che richiedono IIS. Ad esempio, eseguire solo il numero di punti di gestione richiesti per il supporto della base client, prendendo in considerazione l'alta disponibilità e l'isolamento di rete per la gestione client basata su Internet.  

 Utilizzare le seguenti procedure di protezione ottimali per proteggere i sistemi del sito che su cui è in esecuzione IIS.  

 **Disabilitare le funzioni IIS non necessarie.**  

 Installare solo le funzionalità IIS minime per il ruolo del sistema del sito che si installa. Per altre informazioni, vedere [Prerequisiti del sito e del sistema del sito](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  

 **Configurare i ruoli del sistema del sito per richiedere HTTPS.**  

 Quando i client si collegano a un sistema del sito utilizzando HTTP invece di HTTP, utilizzano l'autenticazione Windows che potrebbe cercare di utilizzare l'autenticazione NTLM invece dell'autenticazione Kerberos. Quando viene utilizzata l'autenticazione NTLM, i client potrebbero connettersi a un server non autorizzato.  

 L'eccezione a questa procedura di protezione ottimale potrebbero essere i punti di distribuzione perché gli account di accesso al pacchetto non funzionano quando il punto di distribuzione è configurato per HTTPS. Gli account di accesso al pacchetto forniscono l'autorizzazione al contenuto, in modo che è possibile limitare gli utenti che possono accedere al contenuto. Per ulteriori informazioni, vedere [Security Best Practices for Content Management](../../../core/plan-design/hierarchy/security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement).  

**Configurare un elenco di certificati attendibili (CTL) in IIS per i ruoli del sistema del sito.**  

Ruoli del sistema del sito:  

-   Un punto di distribuzione configurato per HTTPS.  

-   Una gestione configurata per HTTPS e abilitata per il supporto di dispositivi mobili.  

Un elenco di certificati attendibili (CTL) è un elenco definito di autorità di certificazione radice attendibile. Quando si utilizza un CTL con Criteri di gruppo e un una distribuzione PKI, il CTL consente di integrare le autorità di certificazione radice attendibili esistenti che sono configurate in rete, come quelle automaticamente installate con Microsoft Windows o aggiunte tramite le autorità di certificazione radice dell'organizzazione (enterprise) di Windows. Tuttavia, quando un CTL è configurato in IIS, definisce un sottoinsieme di tali autorità di certificazione radice attendibili.  

Questo sottoinsieme fornisce più controllo sulla protezione perché il CTL limita i certificati client accettati solo a quelli che vengono emessi dall'elenco delle autorità di certificazione nel CTL. Ad esempio, Windows viene fornito con un numero di certificati di autorità di certificazione di terze parti ben note, come VeriSign e Thawte. Per impostazione predefinita, il computer su cui è in esecuzione IIS ritiene attendibili i certificati concatenati a queste autorità di certificazione ben note. Quando IIS non viene configurato con un elenco scopi consentiti per i ruoli del sistema del sito in elenco, tutti i dispositivi che hanno un certificato client emesso da tali autorità di certificazione vengono accettati come client validi di Configuration Manager. Se IIS viene configurato con un CTL che non comprendeva queste autorità di certificazione, le connessioni client vengono rifiutate se il certificato è concatenato a tali autorità. Tuttavia, affinché i client di Configuration Manager vengano accettati per i ruoli del sistema del sito in elenco, occorre configurare IIS con un elenco scopi consentiti che specifichi le autorità di certificazione usate dai client di Configuration Manager.  

> [!NOTE]  
>  Solo i ruoli del sistema del sito in elenco richiedono la configurazione di un elenco scopi consentiti in IIS; l'elenco delle autorità che emettono certificati usato da Configuration Manager per i punti di gestione offre la stessa funzionalità per i computer client quando si collegano ai punti di gestione HTTPS.  

Per ulteriori informazioni su come configurare un elenco di autorità di certificazione attendibili in IIS, consultare la documentazione IIS.  

**Non inserire il server del sito su un computer con IIS.**  

La separazione dei ruoli consente di ridurre il profilo di attacco e di migliorare la capacità di ripristino. L'account computer del server del sito in genere ha anche privilegi amministrativi su tutti i ruoli del sistema del sito, e possibilmente sui client di Configuration Manager se si usa l'installazione push client.  

**Usare server IIS dedicati per Configuration Manager.**  

Sebbene sia possibile ospitare più applicazioni basate su Web sui server IIS che sono usati anche da Configuration Manager, tale pratica può significativamente aumentare la superficie di attacco. Un'applicazione configurata male potrebbe consentire a un utente malintenzionato di prendere il controllo di un sistema del sito di Configuration Manager e quindi anche della gerarchia.  

Se è necessario eseguire altre applicazioni basate su Web nei sistemi del sito di Configuration Manager, creare un sito Web personalizzato per i sistemi del sito di Configuration Manager.  

**Utilizzare un sito Web personalizzato.**  

Per i sistemi del sito su cui è in esecuzione IIS, è possibile configurare Configuration Manager per usare un sito Web personalizzato invece del sito Web predefinito per IIS. Se è necessario eseguire altre applicazioni Web sul sistema del sito, è necessario utilizzare un sito Web personalizzato. Questa impostazione vale a livello di sito e non per un sistema del specifico.  

Oltre a fornire una protezione aggiuntiva, è necessario utilizzare un sito Web personalizzato se si eseguono altre applicazioni Web sul sistema del sito.  

**Se si passa dal sito Web predefinito a un sito Web personalizzato dopo aver installato tutti i ruoli del punto di distribuzione, rimuovere le directory virtuali predefinite.**  

Quando si passa dall'uso del sito Web predefinito all'uso di un sito Web personalizzato, Configuration Manager non rimuove le vecchie directory virtuali. Rimuovere le directory virtuali create in origine da Configuration Manager nel sito Web predefinito.  

Ad esempio, le directory virtuali da rimuovere per un punto di distribuzione sono le seguenti:  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  

**Seguire le procedure ottimali per IIS Server.**  

Identificare e seguire le procedure ottimali per la versione di IIS Server. Tuttavia, prendere in considerazione tutti i requisiti che Configuration Manager possiede per i ruoli del sistema del sito specifico. Per altre informazioni, vedere [Prerequisiti del sito e del sistema del sito](../../../core/plan-design/configs/site-and-site-system-prerequisites.md).  

##  <a name="a-namebkmksecuritymanagementpointa-security-best-practices-for-the-management-point"></a><a name="BKMK_Security_ManagementPoint"></a> Procedure di protezione ottimali per il punto di gestione  
 I punti di gestione sono l'interfaccia primaria tra i dispositivi e Configuration Manager. Gli attacchi contro il punto di gestione e il server su cui è in esecuzione sono molto rischiosi e devono essere ridotti in modo appropriato. Applicare tutte le procedure di protezione ottimali appropriate e monitorare eventuali attività inconsuete.  

 Usare le procedure di sicurezza consigliate seguenti per proteggere un punto di gestione in Configuration Manager.  

**Quando si installa un client di Configuration Manager sul punto di gestione, assegnarlo al sito di tale punto di gestione.**  

 Evitare lo scenario in cui un client di Configuration Manager che si trova sul sistema del sito di un punto di gestione venga assegnato a un sito diverso da quello del punto di gestione.  

 Se si esegue la migrazione da una versione precedente a System Center Configuration Manager, eseguire appena possibile la migrazione del software client nel punto di gestione di System Center Configuration Manager.  

##  <a name="a-namebkmksecurityfspa-security-best-practices-for-the-fallback-status-point"></a><a name="BKMK_Security_FSP"></a> Procedure di protezione ottimali per il punto di stato di fallback  
 Usare le procedure di sicurezza consigliate seguenti se si installa un punto di stato di fallback in Configuration Manager.  

 Per ulteriori informazioni sulla protezione quando si installa un punto di stato di fallback, vedere [Determine Whether You Require a Fallback Status Point](../../../core/clients/deploy/plan/determine-the-site-system-roles-for-clients.md#BKMK_Determine_FSP).  

**Non eseguire altri ruoli del sistema del sito nel sistema del sito e non installarli su un controller di dominio.**  

 Poiché il punto di stato di fallback è progettato per accettare comunicazioni non autenticate da qualsiasi computer, l'esecuzione di questo ruolo del sistema del sito con altri ruoli oppure su un controller di dominio aumenta in modo notevole il rischio su tale server.  

**Quando si usano i certificati PKI per la comunicazione client in Configuration Manager, installare il punto di stato di fallback prima di installare i client.**  

 Se i sistemi del sito di Configuration Manager non accettano la comunicazione client HTTP, è possibile che non si sappia che i client non sono gestiti a causa di problemi di certificato relativi alla PKI. Tuttavia, se i client sono assegnati a un punto di stato di fallback, questi problemi di certificato verranno segnalati dal punto stesso.  

 Per motivi di protezione, non è possibile assegnare un punto di stato di fallback ai client dopo l'installazione. Questo ruolo può essere assegnato solo durante l'installazione del client.  

**È consigliabile evitare l'utilizzo del punto di stato di fallback nella rete perimetrale.**  

 Per impostazione predefinita, il punto di stato di fallback accetta dati da qualsiasi client. Anche se un punto di stato di fallback nella rete perimetrale può agevolare la risoluzione dei problemi di client basati su Internet, è necessario bilanciare i vantaggi offerti dalla risoluzione dei problemi e il rischio di un sistema del sito che accetta dati non autenticati in una rete accessibile pubblicamente.  

 Se si installa il punto di stato di fallback nella rete perimetrale o in una rete non attendibile, configurare il server del sito in modo che avvii i trasferimenti di dati invece di utilizzare l'impostazione predefinita che consente al punto di stato di fallback di avviare una connessione al server del sito.  

##  <a name="a-namebkmksecurityissuesclientsa-security-issues-for-site-administration"></a><a name="BKMK_SecurityIssues_Clients"></a> Problemi di sicurezza per l'amministrazione del sito  
 Esaminare i problemi di sicurezza seguenti per Configuration Manager:  

-   Configuration Manager non dispone di difese contro un utente amministratore autorizzato che usa Configuration Manager per attaccare la rete. Gli utenti amministrativi non autorizzati costituiscono un rischio elevato per la protezione e potrebbero lanciare numerosi attacchi, inclusi i seguenti:  

    -   Usare la distribuzione di software per installare automaticamente ed eseguire malware in ogni computer client di Configuration Manager dell'organizzazione.  

    -   Usare il controllo remoto per assumere il controllo di un client di Configuration Manager senza autorizzazioni.  

    -   Configurare intervalli di polling rapidi e quantità ingenti di inventario per creare attacchi di tipo Denial of Service contro i client e i server.  

    -   Utilizzare un sito nella gerarchia per scrivere dati nei dati di Active Directory di un altro sito.  

    La gerarchia del sito è il limite di protezione. I siti devono essere considerati solo come limiti di gestione.  

    Controllare tutte le attività degli utenti amministrativi ed esaminare periodicamente i registri di controllo. Eseguire un'indagine obbligatoria della storia personale di ogni utente amministratore di Configuration Manager prima dell'assunzione e ripetere periodicamente tali indagini come condizione obbligatoria per il mantenimento dell'impiego.  

-   Se il punto di registrazione è compromesso, un utente malintenzionato potrebbe ottenere i certificati per l'autenticazione e rubare le credenziali di utenti che registrano il proprio dispositivo mobile.  

    Il punto di registrazione comunica con un'autorità di certificazione e può creare, modificare ed eliminare gli oggetti di Active Directory. Non installare mai il punto di registrazione nella rete perimetrale e monitorare attività insolite.  

-   Se si consentono i criteri utente per la gestione client basata su Internet o si configura il punto per siti Web del Catalogo applicazioni per gli utenti quando si trovano in Internet, si incrementa la superficie di attacco.  

    Oltre a utilizzare i certificati PKI per le connessioni tra client e server, queste configurazioni necessitano dell'autenticazione di Windows, che potrebbe eseguire il fallback all'utilizzo dell'autenticazione NTLM invece di Kerberos. L'autenticazione NTLM è vulnerabile agli attacchi di riproduzione e di rappresentazione. Per autenticare correttamente un utente su Internet, è necessario consentire una connessione dal server di sistema del sito basato su Internet a un controller di dominio.  

-   La condivisione Admin$ è necessaria per i server di sistema del sito.  

    Il server del sito di Configuration Manager usa la condivisione Admin$ per la connessione e l'esecuzione di operazioni di servizio nei sistemi del sito. Non disabilitare o rimuovere la condivisione Admin$.  

-   Configuraiton Manager usa servizi di risoluzione dei nomi per connettersi ad altri computer e tali servizi sono difficili da proteggere da attacchi alla sicurezza, ad esempio spoofing, manomissioni, ripudio, diffusione di informazioni, Denial of Service ed elevazione dei privilegi.  

    Identificare e seguire le procedure di protezione ottimali per la versione di DNS e WINS utilizzata per la risoluzione dei nomi.  

##  <a name="a-namebkmkprivacycliientsa-privacy-information-for-discovery"></a><a name="BKMK_Privacy_Cliients"></a> Informazioni sulla privacy per l'individuazione  
 L'individuazione crea i record delle risorse di rete e li archivia nel database di System Center Configuration Manager. I record di dati di individuazione contengono informazioni sul computer, ad esempio indirizzo IP, sistema operativo e nome del computer. I metodi di individuazione di Active Directory possono essere configurati anche per rilevare eventuali informazioni memorizzate in Servizi di dominio Active Directory.  

 L'unico metodo di individuazione abilitato per impostazione predefinita è l'individuazione heartbeat, ma tale metodo consente solo di individuare computer in cui è già installato il software client di System Center Configuration Manager.  

 Le informazioni di individuazione non vengono inviate a Microsoft. Le informazioni di individuazione vengono archiviate nel database di Configuration Manager. Le informazioni vengono conservate nel database fino alla relativa eliminazione nell'ambito delle attività di manutenzione del sito **Elimina dati di individuazione obsoleti** eseguite ogni 90 giorni. È possibile configurare l'intervallo di eliminazione.  

 Prima di configurare i metodi di rilevamento aggiuntivi o estendere l'individuazione di Active Directory, valutare i requisiti relativi alla privacy.  



<!--HONumber=Dec16_HO3-->



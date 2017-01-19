---
title: Privacy e sicurezza per i client | Microsoft Docs
description: Informazioni sulla sicurezza e la privacy dei client in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: c1d71899-308f-49d5-adfa-3a3ec0163ed8
caps.latest.revision: 10
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: 6e76c3ae104c0561a5c7b178823b7a48761518fe


---
# <a name="security-and-privacy-for-clients-in-system-center-configuration-manager"></a>Sicurezza e privacy per i client in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo contiene le informazioni sulla privacy e sulla sicurezza dei client in System Center Configuration Manager e dei dispositivi mobili gestiti dal connettore Exchange Server:  

##  <a name="a-namebkmksecuritycliientsa-security-best-practices-for-clients"></a><a name="BKMK_Security_Cliients"></a> Procedure di sicurezza consigliate per i client  
 Quando Configuration Manager accetta dati provenienti da dispositivi che eseguono il client di Configuration Manager espone il sito al possibile attacco da parte dei client. Ad esempio, i client potrebbero inviare un inventario non corretto o tentare di sovraccaricare i sistemi del sito. Distribuire il client di Configuration Manager solo ai dispositivi considerati attendibili. Inoltre, è possibile usare le seguenti procedure consigliate per proteggere il sito da dispositivi non autorizzati o compromessi:  

 **Usare i certificati di infrastruttura a chiave pubblica (PKI) per le comunicazioni client con sistemi del sito che eseguono IIS.**  

-   Quale proprietà del sito, configurare **Impostazioni sistema del sito** su **Solo HTTPS**.  

-   Installare i client con la proprietà CCMSetup **/UsePKICert**  

-   Usare un elenco di revoche di certificati (CRL) e assicurarsi che i client e i server di comunicazione possano sempre accedervi.  

 Questi certificati sono richiesti per i client di dispositivi mobili e per le connessioni di computer client su Internet e sono consigliati per tutte le connessioni client sulla intranet, ad eccezione dei punti di distribuzione.  

 Per altre informazioni sui requisiti dei certificati PKI e su come vengono usati per contribuire alla protezione di Configuration Manager, vedere [Requisiti dei certificati PKI per System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 **Approvare automaticamente i computer client dai domini attendibili e controllare e approvare manualmente gli altri computer**  

 È possibile configurare l'approvazione per la gerarchia come manuale, automatica per i computer in domini attendibili o automatica per tutti i computer. Il metodo più sicuro è quello che prevede l'approvazione automatica dei client membri di domini attendibili, con successivo controllo e successiva approvazione manuale di tutti gli altri computer. Si sconsiglia di approvare automaticamente tutti i client a meno che non ci si avvalga di altri controlli di accesso per impedire l'ingresso nella rete di computer non attendibili.  

 L'approvazione identifica un computer considerato attendibile per la gestione da parte di Configuration Manager quando non è possibile usare l'autenticazione PKI.  

 Per altre informazioni sull'approvazione manuale dei computer, vedere [Gestire i client dal nodo Dispositivi](../../../../core/clients/manage/manage-clients.md#BKMK_ManagingClients_DevicesNode).  

 **Non affidarsi al blocco per impedire l'accesso dei client alla gerarchia di Configuration Manager**  

 I client bloccati vengono rifiutati dall'infrastruttura di Configuration Manager e non potranno pertanto comunicare con i sistemi del sito per scaricare criteri, caricare dati di inventario o inviare messaggi di stato. Tuttavia, è opportuno non affidarsi al blocco per proteggere la gerarchia di Configuration Manager da computer non attendibili quando i sistemi del sito accettano connessioni client HTTP. In questo scenario, un client bloccato potrebbe associarsi di nuovo al sito con un nuovo certificato autofirmato e un ID hardware. Il blocco è progettato per intervenire in caso di supporti di avvio persi o compromessi quando si distribuisce un sistema operativo ai client e quando tutti i sistemi del sito accettano connessioni client HTTPS. Se si usa un'infrastruttura a chiave pubblica (PKI) che supporta un elenco di revoche di certificati (CRL), considerare sempre la revoca del certificato come prima linea di difesa contro certificati potenzialmente compromessi. Il blocco dei client in Configuration Manager offre una seconda linea di difesa per la protezione della gerarchia.  

 Per altre informazioni, vedere [Determinare se bloccare o meno i client in System Center Configuration Manager](../../../../core/clients/deploy/plan/determine-whether-to-block-clients.md).  

 **Usare i metodi di installazione client più sicuri e più adatti al proprio ambiente:**  

-   Per i computer del dominio, i metodi di installazione client basati su aggiornamento software e sui Criteri di gruppo sono più sicuri dell'installazione push client.  

-   È possibile garantire un'elevata protezione della creazione dell'immagine e dell'installazione manuale applicando controlli di accesso e controlli delle modifiche.  

 Di tutti i metodi di installazione client, l'installazione push client è il meno sicuro date le numerose dipendenze, incluse le autorizzazioni amministrative locali, la condivisione Admin$ e molte eccezioni del firewall. Queste dipendenze aumentano la superficie di attacco.  

 Per altre informazioni sui vari metodi di installazione dei client, vedere [Metodi di installazione client in System Center Configuration Manager](../../../../core/clients/deploy/plan/client-installation-methods.md).  

 Inoltre, laddove possibile, selezionare il metodo di installazione client che richiede le minime autorizzazioni di sicurezza in Configuration Manager, quindi limitare gli utenti amministratori a cui assegnare ruoli di protezione, incluse autorizzazioni che possono essere usate per scopi diversi dalla distribuzione dei client. Ad esempio, l'aggiornamento automatico del client richiede il ruolo di protezione **Amministratore completo** , che garantisce a un utente amministratore tutte le autorizzazioni di sicurezza.  

 Per altre informazioni sulle dipendenze e sulle autorizzazioni di sicurezza necessarie per ogni metodo di installazione client, vedere "Dipendenze del metodo di installazione" in [Prerequisiti per client per computer](../../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md#BKMK_prereqs_computers).  

 **Se è necessario usare l'installazione push client, adottare misure aggiuntive per proteggere l'account di installazione push client**  

 Sebbene questo account debba essere membro del gruppo locale **Administrators** in ogni computer in cui verrà installato il software client di Configuration Manager, non aggiungere mai l'account di installazione push client al gruppo **Domain Admins**. Al contrario, creare un gruppo globale e aggiungerlo al gruppo locale **Admnistrators** sui computer client. È inoltre possibile creare un oggetto Criteri di gruppo per aggiungere un'impostazione di Gruppi con restrizioni per l'aggiunta dell'account di installazione push client nel gruppo locale **Administrators** .  

 Per una maggiore sicurezza, creare più account di installazione push client, ciascuno con accesso amministrativo a un numero di computer limitato in modo tale che, in caso di compromissione di un account, saranno compromessi solo i computer client accessibili per tale account.  

 **Rimuovere i certificati prima della creazione dell'immagine del computer client**  

 Se si prevede di distribuire i client usando la tecnologia di creazione dell'immagine, rimuovere sempre i certificati, tra cui i certificati PKI, che includono l'autenticazione client e i certificati autofirmati prima di acquisire l'immagine. In caso di mancata rimozione di questi certificati, i client potrebbero rappresentarsi reciprocamente e non sarebbe possibile verificare i dati per ciascuno di essi.  

 Per altre informazioni sull'utilizzo di Sysprep per la preparazione di un computer per la creazione dell'immagine, vedere la documentazione sulla distribuzione di Windows.  

 **Assicurarsi che i client del computer di Configuration Manager ottengano una copia autorizzata di questi certificati:**  

-   Chiave radice attendibile di Configuration Manager  

     Se lo schema di Active Directory non è stato esteso per Configuration Manager e i client non usano certificati PKI per la comunicazione con i punti di gestione, i client si baseranno sulla chiave radice attendibile di Configuration Manager per autenticare punti di gestione validi. In questo scenario, i client non sono in grado di verificare in alcun modo l'attendibilità di un punto di gestione per la gerarchia, a meno che non utilizzino la chiave radice attendibile. Senza la chiave radice attendibile, un utente malintenzionato esperto potrebbe indirizzare i client verso un punto di gestione non autorizzato.  

     Quando i client non sono in grado di scaricare la chiave radice attendibile di Configuration Manager dal catalogo globale o tramite i certificati PKI, eseguire il pre-provisioning dei client con la chiave radice attendibile per verificare che non possano essere indirizzati a un punto di gestione non autorizzato. Per ulteriori informazioni, vedere [Planning for the Trusted Root Key](../../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

-   Certificato di firma del server del sito  

     I client usano il certificato di firma del server del sito per verificare che quest'ultimo abbia firmato i criteri client che i client scaricano da un punto di gestione. Questo certificato è autofirmato dal server del sito e pubblicato in Servizi di dominio Active Directory.  

     Per impostazione predefinita, quando i client non sono in grado di scaricare il certificato di firma del server del sito dal catalogo globale, lo scaricano dal punto di gestione. Quando il punto di gestione è esposto a una rete non attendibile (Internet, ad esempio), installare manualmente il certificato di firma del server del sito sui client per assicurarsi che non possano eseguire criteri client manomessi provenienti da un punto di gestione compromesso.  

     Per installare manualmente il certificato di firma del server del sito, usare la proprietà client.msi CCMSetup **SMSSIGNCERT**. Per altre informazioni, vedere [Informazioni sulle proprietà di installazione del client in System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

 **Non usare l'assegnazione automatica del sito se il client scaricherà la chiave radice attendibile dal primo punto di gestione con cui entrerà in contatto**  

 Questa procedura consigliata è collegata alla voce precedente. Per evitare il rischio che un nuovo client scarichi la chiave radice attendibile da un punto di gestione non autorizzato, usare l'assegnazione automatica del sito solo negli scenari seguenti:  

-   Il client può accedere alle informazioni del sito di Configuration Manager pubblicate in Active Directory Domain Services.  

-   Viene eseguito il pre-provisioning del client con la chiave radice attendibile.  

-   Sono usati certificati PKI rilasciati da un'autorità di certificazione dell'organizzazione (enterprise) per stabilire un trust tra il client e il punto di gestione.  

 Per altre informazioni sulla chiave radice attendibile, vedere [Planning for the Trusted Root Key](../../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

 **Installare i computer client con l'opzione Client.msi CCMSetup SMSDIRECTORYLOOKUP=NoWINS**  

 Il metodo di individuazione del servizio più sicuro per il rilevamento di siti e punti di gestione da parte dei client è quello che prevede l'utilizzo di Servizi di dominio Active Directory. Se ciò non fosse attuabile, ad esempio per l'impossibilità di estendere lo schema di Active Directory per Configuration Manager o perché i client si trovano in un gruppo di lavoro o una foresta non trusted, è possibile usare la pubblicazione DNS come metodo di individuazione del servizio alternativo. Se entrambi i metodi hanno esito negativo, i client possono cercare di usare WINS quando il punto di gestione non è configurato per le connessioni client HTTPS.  

 Dal momento che la pubblicazione su WINS è meno sicura rispetto agli altri metodi di pubblicazione, configurare i computer client in modo tale che non cerchino di usare WINS specificando SMSDIRECTORYLOOKUP=NoWINS. Se fosse necessario usare WINS per l'individuazione del servizio, usare SMSDIRECTORYLOOKUP=WINSSECURE (impostazione predefinita) che usa la chiave radice attendibile di Configuration Manager per convalidare il certificato autofirmato del punto di gestione.  

> [!NOTE]  
>  Quando il client è configurato per SMSDIRECTORYLOOKUP=WINSSECURE e rileva un punto di gestione da WINS, il client controlla la sua copia della chiave radice attendibile di Configuration Manager presente in WMI. Se la firma sul certificato del punto di gestione corrisponde alla copia del client della chiave radice attendibile, il certificato viene convalidato e il client comunica con il punto di gestione rilevato tramite WINS. Se la firma sul certificato del punto di gestione non corrisponde alla copia del client della chiave radice attendibile, il certificato non è valido e il client non comunicherà con il punto di gestione rilevato tramite WINS.  

 **Assicurarsi che le dimensioni delle finestre di manutenzione siano sufficienti per la distribuzione degli aggiornamenti software critici**  

 È possibile configurare le finestre di manutenzione per le raccolte di dispositivi al fine di limitare il numero di possibili installazioni del software da parte di Configuration Manager su questi dispositivi. Se si configurano dimensioni insufficienti della finestra di manutenzione, il client potrebbe non essere in grado di installare aggiornamenti software critici, rendendo il client vulnerabile ad attacchi altrimenti limitati dall'aggiornamento software.  

 **Per i dispositivi con Windows Embedded che dispongono di filtri di scrittura, adottare precauzioni di sicurezza aggiuntive per ridurre la superficie di attacco nel caso in cui Configuration Manager disabiliti i filtri di scrittura per rendere permanenti installazioni software e modifiche**  

 Quando i filtri di scrittura vengono abilitati su dispositivi con Windows Embedded, qualsiasi modifica o installazione software viene eseguita solo sulla sovrapposizione e non permane dopo il riavvio del dispositivo. Se si usa Configuration Manager per disabilitare temporaneamente i filtri di scrittura per rendere permanenti modifiche e installazioni software, durante questo periodo il dispositivo con Windows Embedded è vulnerabile alle modifiche su tutti i volumi, comprese le cartelle condivise.  

 Sebbene Configuration Manager blocchi il computer durante questo periodo in modo da consentire l'accesso solo agli amministratori locali, laddove possibile, adottare precauzioni di sicurezza aggiuntive per proteggere il computer. Ad esempio, abilitare ulteriori restrizioni del firewall e scollegare il dispositivo dalla rete.  

 Se si usano delle finestre di manutenzione per rendere permanenti le modifiche, pianificarle attentamente per limitare al massimo il tempo di disabilitazione dei filtri di scrittura, pur garantendo un intervallo sufficiente al completamento delle installazioni software e dei riavvii.  

 **Se si usa l'installazione client basata su aggiornamento software e si installa una versione del client successiva sul sito, aggiornare l'aggiornamento software pubblicato sul punto di aggiornamento software per consentire ai client di ricevere la versione più recente**  

 Se si installa una versione del client successiva sul sito, ad esempio durante un aggiornamento del sito, l'aggiornamento software per la distribuzione client pubblicato nel punto di aggiornamento software non viene aggiornato automaticamente. È necessario pubblicare nuovamente il client di Configuration Manager nel punto di aggiornamento software, quindi fare clic su **Sì** per aggiornare il numero di versione.  

 Per altre informazioni, vedere la procedura "Per pubblicare il client di Configuration Manager nel punto di aggiornamento software" in [Come installare i client di Configuration Manager usando l'Installazione basata sull'aggiornamento software](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

 **Configurare l'impostazione Sospendere immissione PIN di BitLocker al riavvio del dispositivo client Agente computer su Sempre solo per i computer considerati attendibili e con accesso fisico limitato**  

 Quando si configura questa impostazione su **Sempre**, Configuration Manager è in grado di completare l'installazione del software per garantire l'installazione di aggiornamenti software critici e il ripristino dei servizi. Tuttavia, se un utente malintenzionato intercettasse il processo di riavvio, potrebbe assumere il controllo del computer. Usare questa impostazione solo se il computer è considerato attendibile e il relativo accesso fisico è limitato. Ad esempio, questa impostazione potrebbe essere appropriata per i server in un data center.  

 **Non configurare l'impostazione Criteri di esecuzione di PowerShell del dispositivo client Agente computer su Ignora**  

 Questa impostazione consente al client di Configuration Manager di eseguire script PowerShell non firmati, permettendo potenzialmente l'esecuzione di malware sui computer client. Se è necessario selezionare questa opzione, usare un'impostazione client personalizzata e assegnarla esclusivamente ai computer client che devono eseguire script PowerShell non firmati.  

##  <a name="a-namebkmkmobilea-security-best-practices-for-mobile-devices"></a><a name="bkmk_mobile"></a> Procedure di sicurezza consigliate per i dispositivi mobili  
 **Per i dispositivi mobili registrati con Configuration Manager e supportati su Internet: installare il punto proxy di registrazione in una rete perimetrale e il punto di registrazione nella intranet**  

 Questa separazione dei ruoli contribuisce a proteggere il punto di registrazione da attacchi esterni. Se il punto di registrazione è compromesso, un utente malintenzionato potrebbe ottenere i certificati per l'autenticazione e rubare le credenziali di utenti che registrano il proprio dispositivo mobile.  

 **Per i dispositivi mobili: configurare le impostazioni della password per proteggere i dispositivi mobili da accessi non autorizzati**  

 Per i dispositivi mobili che vengono registrati da Configuration Manager: usare un elemento di configurazione del dispositivo mobile per scegliere di configurare una password della complessità di un PIN e almeno la lunghezza minima predefinita della password.  

 Per i dispositivi mobili su cui non è installato il client di Configuration Manager ma che sono gestiti dal connettore Exchange Server: configurare le **Impostazioni password** per il connettore Exchange Server, scegliendo di configurare una password della complessità di un PIN e specificando almeno la lunghezza minima predefinita della password.  

 **Per i dispositivi mobili: prevenire eventuali manomissioni delle informazioni di inventario e delle informazioni sullo stato abilitando solo l'esecuzione delle applicazioni firmate da società ritenute attendibili e impedendo l'installazione di file non firmati**  

 Per più dispositivi mobili registrati da Configuration Manager: usare un elemento di configurazione del dispositivo mobile per configurare l'impostazione di protezione **Applicazioni non firmate** su **Non consentito** e configurare **Installazione file non firmati** come un'origine attendibile.  

 Per i dispositivi mobili su cui non è installato il client di Configuration Manager ma che sono gestiti dal connettore Exchange Server: configurare **Impostazioni applicazione** per il connettore Exchange Server in modo che **Installazione file non firmati** e **Applicazioni non firmate** siano impostate su **Non consentito**.  

 **Per i dispositivi mobili: evitare attacchi tramite elevazione dei privilegi bloccando il dispositivo mobile quando non usato**  

 Per più dispositivi mobili registrati da Configuration Manager: usare un elemento di configurazione del dispositivo mobile per configurare l'impostazione della password **Tempo di inattività in minuti prima del blocco del dispositivo mobile**.  

 Per i dispositivi mobili su cui non è installato il client di Configuration Manager ma che sono gestiti dal connettore Exchange Server: Configurare le **Impostazioni password** per il connettore Exchange Server per impostare **Tempo di inattività in minuti prima del blocco del dispositivo mobile**.  

 **Per i dispositivi mobili: evitare l'elevazione dei privilegi limitando gli utenti autorizzati a registrare i propri dispositivi mobili.**  

 Usare un'impostazione client personalizzata anziché le impostazioni predefinite per consentire solo a utenti autorizzati di registrare i propri dispositivi mobili.  

 **Per i dispositivi mobili: non distribuire applicazioni agli utenti che hanno dispositivi mobili registrati da Configuration Manager o Microsoft Intune negli scenari seguenti:**  

-   Quando il dispositivo mobile viene usato da più persone.  

-   Quando il dispositivo viene registrato da un amministratore per conto di un utente.  

-   Quando il dispositivo viene trasferito a un'altra persona senza ritiro e successiva nuova registrazione del dispositivo.  

 Viene creata una relazione di affinità utente dispositivo durante la registrazione, che consente di associare l'utente che esegue la registrazione al dispositivo mobile. Se il dispositivo mobile è usato da un altro utente, sarà possibile eseguire le applicazioni distribuite all'utente originale, determinando potenzialmente un'elevazione dei privilegi. Allo stesso modo, se un amministratore registra il dispositivo mobile per un utente, le applicazioni distribuite all'utente non saranno installate sul dispositivo, mentre potrebbero invece essere installate le applicazioni distribuite all'amministratore.  

 A differenza dell'affinità utente-dispositivo per computer Windows, non è possibile definire manualmente le informazioni relative a tale affinità per i dispositivi mobili registrati da Microsoft Intune.  

 Se si trasferisce la titolarità di un dispositivo mobile registrato da Intune, ritirare il dispositivo mobile da Intune per rimuovere l'affinità utente-dispositivo, quindi chiedere all'utente corrente di registrare nuovamente il dispositivo.  

 **Per i dispositivi mobili: assicurarsi che gli utenti registrino i propri dispositivi mobili per Microsoft Intune**  

 Dal momento che la relazione di affinità utente dispositivo viene creata durante la registrazione, che consente di associare l'utente che esegue la registrazione al dispositivo mobile, se un amministratore registra il dispositivo mobile per un utente, le applicazioni distribuite a tale utente non saranno installate sul dispositivo, mentre potrebbero invece essere installate le applicazioni distribuite all'amministratore.  

 **Per il connettore Exchange Server: accertarsi che la connessione tra il server del sito di Configuration Manager e il computer che esegue Exchange Server sia protetta**  

 Usare IPsec se Exchange Server si trova in locale. Exchange Server ospitato protegge automaticamente la connessione usando SSL.  

 **Per il connettore Exchange Server: usare il principio dei privilegi minimi per il connettore**  

 Per un elenco dei cmdlet minimi richiesti dal connettore Exchange Server, vedere [Gestire i dispositivi mobili con System Center Configuration Manager ed Exchange](../../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

##  <a name="a-namebkmkmacsa-security-best-practices-for-macs"></a><a name="bkmk_macs"></a> Procedure di sicurezza consigliate per i Mac  
 **Per i computer Mac: archiviare e accedere ai file di origine del client da un percorso protetto.**  

 Configuration Manager non verifica se i file di origine client sono stati manomessi prima dell'installazione o della registrazione del client nel computer Mac. Scaricare questi file da una fonte attendibile, archiviarli e accedervi in modo sicuro.  

 **Per i computer Mac: indipendentemente da Configuration Manager, monitorare e tenere traccia del periodo di validità del certificato registrato per gli utenti.**  

 Per garantire la continuità aziendale, monitorare e tenere traccia del periodo di validità dei certificati usati per i computer Mac. Configuration Manager non supporta il rinnovo automatico del certificato o avvisa della scadenza prossima. Un periodo di validità tipico è 1 anno.  

 Per informazioni su come rinnovare il certificato, vedere  [Renewing the Mac Client Certificate Manually](../../../../core/clients/deploy/deploy-clients-to-macs.md#BKMK_Man).  

 **Per i computer Mac: valutare se configurare il certificato CA radice attendibile in modo che sia attendibile solo per il protocollo SSL e semplificare la protezione contro l'elevazione dei privilegi.**  

 Quando si registrano i computer Mac, viene installato automaticamente un certificato utente per gestire il client di Configuration Manager insieme a un certificato radice attendibile a cui il certificato utente si collega. Se si desidera limitare l'attendibilità del certificato radice al solo protocollo SSL, è possibile usare la procedura seguente.  

 Dopo aver completato la procedura, il certificato radice non sarà più attendibile per convalidare protocolli diversi da SSL, ad esempio, Protezioni messaggi (S/MIME), Extensible Authentication (EAP) o firma codice.  

> [!NOTE]  
>  È inoltre possibile usare questa procedura se è stato installato il certificato client indipendentemente da Configuration Manager.  

 Per limitare il certificato CA radice al solo protocollo SSL:  

1.  Nei computer Mac, aprire una finestra terminale.  

2.  Immettere il comando **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

3.  Nella finestra di dialogo **Accesso Portachiavi** nella sezione **Portachiavi** , fare clic su **Sistema**, quindi nella sezione **Categoria** fare clic su **Certificati**.  

4.  Individuare e fare doppio clic sul certificato CA radice per il certificato del client Mac.  

5.  Nella finestra di dialogo per il certificato CA radice espandere la sezione **Attendibilità** ed eseguire le modifiche seguenti:  

    1.  Per l'impostazione **Quando si usa questo certificato** modificare l'impostazione predefinita **Considera sempre attendibile** in **Usa valori predefiniti di sistema**.  

    2.  Per l'impostazione **Secure Sockets Layer (SSL)** modificare **Nessun valore specificato** in **Considera sempre attendibile**.  

6.  Chiudere la finestra di dialogo e, quando richiesto, immettere la password dell'amministratore e quindi fare clic su **Aggiorna impostazioni**.  

##  <a name="a-namebkmksecurityissuesclientsa-security-issues-for-configuration-manager-clients"></a><a name="BKMK_SecurityIssues_Clients"></a> Problemi di protezione per i client di Configuration Manager  
 Non è possibile ovviare ai seguenti problemi di protezione:  

-   I messaggi di stato non sono autenticati  

     L'autenticazione non viene eseguita sui messaggi di stato. Quando un punto di gestione accetta connessioni client HTTP, tutti i dispositivi possono inviare messaggi di stato al punto di gestione. Se il punto di gestione accetta solo connessioni client HTTPS, un dispositivo dovrà ottenere un certificato di autenticazione client valido da un'autorità di certificazione radice attendibile, ma potrà anche inviare successivamente qualsiasi messaggio di stato. Un eventuale messaggio di stato non valido inviato da un client verrà rimosso.  

     Esistono alcuni potenziali attacchi contro questa vulnerabilità. Un utente malintenzionato potrebbe inviare un messaggio di stato falso per ottenere l'appartenenza a una raccolta basata su query messaggi di stato. Qualsiasi client può lanciare un attacco di tipo Denial of Service contro il punto di gestione, sovraccaricandolo con messaggi di stato. Se i messaggi di stato attivano azioni nelle regole di filtro del messaggio di stato, un utente malintenzionato potrebbe attivare una regola. Potrebbe inoltre inviare un messaggio di stato che renderebbe le informazioni relative ai rapporti inaccurate.  

-   I criteri possono essere reindirizzati ai client non di destinazione  

     Gli autori di un attacco potrebbero usare diversi metodi per applicare un criterio assegnato a un client a un altro client completamente differente. Ad esempio, un utente malintenzionato su un client attendibile potrebbe inviare informazioni di individuazione o di inventario false per aggiungere il computer a una raccolta alla quale non dovrebbe appartenere, ricevendo successivamente tutte le distribuzioni in quella raccolta. Sebbene siano previsti controlli per impedire la modifica diretta di un criterio, gli autori di attacchi potrebbero usare un criterio esistente per riformattare e ridistribuire un sistema operativo e inviarlo a un computer diverso, creando un attacco di tipo Denial of Service. Questi tipi di attacchi richiederebbero tempistiche precise e una profonda conoscenza dell'infrastruttura di Configuration Manager.  

-   I registri del client consentono l'accesso utente  

     Tutti i file di log client consentono agli utenti l'accesso in lettura e agli utenti interattivi l'accesso in scrittura. Se si abilita la registrazione dettagliata, gli autori di un attacco potrebbero leggere i file di log per cercare informazioni sulle vulnerabilità del sistema o sulla conformità. Processi come l'installazione software eseguiti in un contesto utente devono essere in grado di scrivere nei file di log con un account utente con diritti limitati. Ciò significa che un utente malintenzionato potrebbe anche scrivere nei registri con un account con diritti limitati.  

     Il rischio più preoccupante è che l'autore dell'attacco possa rimuovere delle informazioni all'interno dei file di log potenzialmente utili per il controllo e il rilevamento di intrusi da parte dell'amministratore.  

-   È possibile usare un computer per ottenere un certificato progettato per la registrazione di dispositivi mobili  

     Quando Configuration Manager elabora una richiesta di registrazione, non è in grado di verificare se la richiesta proviene da un dispositivo mobile piuttosto che da un computer. Se la richiesta proviene da un computer, sarà possibile installare un certificato PKI che consentirà la successiva registrazione in Configuration Manager. Per evitare un attacco tramite elevazione dei privilegi in questo scenario, consentire solo a utenti attendibili di registrare il proprio dispositivo mobile e monitorare attentamente le attività di registrazione.  

-   La connessione da un client al punto di gestione non viene interrotta se si blocca un client e tale client è in grado di continuare a inviare pacchetti di notifica client al punto di gestione, come messaggi keep-alive  

     Quando si blocca un client non ritenuto più attendibile e il client ha stabilito una comunicazione di notifica client, Configuration Manager non disconnette la sessione. Il client bloccato può continuare a inviare pacchetti al suo punto di gestione finché non si disconnette dalla rete. Si tratta solo di piccoli pacchetti keep-alive e questi client non possono essere gestiti da Configuration Manager finché sono bloccati.  

-   Quando si usa l'aggiornamento automatico del client e quest'ultimo viene indirizzato a un punto di gestione per il download dei file di origine client, il punto di gestione non viene verificato come un'origine attendibile  

-   La prima volta che eseguono la registrazione di computer Mac, gli utenti sono esposti al rischio di attacchi di spoofing DNS  

     Quando i computer Mac si connettono al punto proxy di registrazione durante la registrazione, probabilmente il computer Mac non disporrà del certificato CA radice. A questo punto, il server è considerato attendibile dal computer Mac e chiede all'utente di continuare. Se il nome completo del punto proxy di registrazione viene risolto da un server DNS non autorizzato, potrebbe indirizzare il computer Mac in punto proxy di registrazione non autorizzato e installare i certificati da un'origine non attendibile. Per ridurre questo rischio, seguire le procedure consigliate per evitare gli attacchi di spoofing DNS nel proprio ambiente.  

-   La registrazione Mac non limita le richieste di certificati  

     Gli utenti possono registrare di nuovo i computer Mac, ogni volta che richiedono un nuovo certificato client. Configuration Manager non verifica più richieste o non limita il numero di certificati richiesti da un singolo computer. Un utente non autorizzato potrebbe eseguire uno script che ripete la richiesta di registrazione della riga di comando causando un attacco di tipo Denial of Service nella rete o nell'autorità di emissione del certificato (CA). Per ridurre questo rischio, è necessario monitorare questo tipo di comportamenti sospetti nella CA emittente. Un computer che mostra questo tipo di comportamento deve essere immediatamente bloccato dalla gerarchia di Configuration Manager.  

-   Una conferma di cancellazione non verifica che il dispositivo sia stato effettivamente cancellato  

     Quando si avvia un'azione di cancellazione per un dispositivo mobile e Configuration Manager visualizza lo stato di cancellazione da confermare, il sistema verifica che Configuration Manager abbia inviato il messaggio e non che l'azione sia stata completata. Inoltre, per i dispositivi mobili gestiti dal connettore Exchange Server, una conferma di cancellazione verifica che il comando sia stato ricevuto da Exchange, non dal dispositivo.  

-   Se si usano le opzioni di conferma delle modifiche in dispositivi con Windows Embedded, gli account potrebbero essere bloccati prima del previsto  

     Se il dispositivo con Windows Embedded esegue un sistema operativo precedente a Windows 7 e un utente prova ad accedere mentre i filtri di scrittura sono disabilitati per la conferma delle modifiche eseguite da Configuration Manager, il numero di tentativi di accesso errati consentiti prima del blocco dell'account viene effettivamente dimezzato. Ad esempio, se **Valore di soglia di blocco account** è configurato su 6 e un utente digita una password errata per 3 volte, l'account viene bloccato, creando effettivamente una situazione del tipo Denial of Service.  In questo scenario, se gli utenti devono accedere a dispositivi incorporati, è necessario allertarli circa la potenziale riduzione del valore di soglia di blocco.  

##  <a name="a-namebkmkprivacycliientsa-privacy-information-for-configuration-manager-clients"></a><a name="BKMK_Privacy_Cliients"></a> Informazioni sulla privacy per i client di Configuration Manager  
 Quando si distribuisce il client di Configuration Manager, vengono abilitate le impostazioni client che consentono di usare le funzionalità di gestione di Configuration Manager. Le impostazioni usate per la configurazione delle funzionalità possono essere applicate a tutti i client nella gerarchia di Configuration Manager, indipendentemente dal fatto che siano connessi direttamente alla rete aziendale, connessi tramite sessione remota o connessi a Internet ma supportati da Configuration Manager.  

 Le informazioni sui client vengono archiviate nel database di Configuration Manager e non vengono inviate a Microsoft. Le informazioni vengono conservate nel database fino alla relativa eliminazione nell'ambito delle attività di manutenzione del sito **Elimina dati di individuazione obsoleti** eseguite ogni 90 giorni. È possibile configurare l'intervallo di eliminazione.  

 Prima di configurare il client di Configuration Manager, esaminare i requisiti sulla privacy.  

### <a name="privacy-information-for-mobile-devices-that-are-enrolled-by-configuration-manager"></a>Informazioni sulla privacy per i client dispositivo mobile registrati da Configuration Manager  
 Per informazioni sulla privacy in merito alla registrazione di un dispositivo mobile da parte di Configuration Manager, vedere [Informativa sulla privacy di System Center Configuration Manager - Supplemento per dispositivi mobili](../../../../core/misc/privacy/privacy-statement-mobile-device-addendum.md).  

### <a name="client-status"></a>Stato del client  
 Configuration Manager monitora l'attività dei client e periodicamente valuta ed eventualmente aggiorna il client di Configuration Manager e le relative dipendenze. Lo stato del client è attivato per impostazione predefinita e usa una metrica lato server per i controlli dell'attività client e azioni lato client per i controlli automatici, l'aggiornamento e l'invio di informazioni sullo stato del client al sito di Configuration Manager. Il client esegue i controlli automatici secondo una pianificazione configurabile. Il client invia i risultati dei controlli al sito di Configuration Manager. Queste informazioni vengono crittografate durante il trasferimento.  

 Le informazioni sullo stato del client vengono archiviate nel database di Configuration Manager e non vengono inviate a Microsoft. Le informazioni non vengono memorizzate in forma crittografata nel database del sito. Le informazioni vengono conservate nel database fino alla relativa eliminazione, che avviene come specificato dal valore dell'impostazione di stato del client **Mantieni la cronologia stato del client per il numero di giorni seguente** . Il valore predefinito di tale impostazione è ogni 31 giorni.  

 Prima di installare il client di Configuration Manager con il controllo dello stato del client, valutare i requisiti relativi alla privacy.  

##  <a name="a-namebkmkprivacyexchangeconnectora-privacy-information-for-mobile-devices-that-are-managed-with-the-exchange-server-connector"></a><a name="BKMK_Privacy_ExchangeConnector"></a> Informazioni sulla privacy per i dispositivi mobili gestiti con il connettore Exchange Server  
 Il connettore Exchange Server rileva e gestisce i dispositivi che si connettono a Exchange Server (locale o ospitato) usando il protocollo ActiveSync. I record rilevati dal connettore Exchange Server vengono memorizzati nel database di Configuration Manager. Le informazioni vengono raccolte da Exchange Server. Tali informazioni non includono informazioni aggiuntive su quanto i dispositivi mobili inviano a Exchange Server.  

 Le informazioni sul dispositivo mobile non vengono inviate a Microsoft. Le informazioni sui dispositivi mobili sono archiviate nel database di Configuration Manager. Le informazioni vengono conservate nel database fino alla relativa eliminazione nell'ambito delle attività di manutenzione del sito **Elimina dati di individuazione obsoleti** eseguite ogni 90 giorni. È possibile configurare l'intervallo di eliminazione.  

 Prima di installare e configurare il connettore Exchange Server, valutare i requisiti relativi alla privacy.  



<!--HONumber=Dec16_HO3-->



---
title: "Proprietà di installazione del client | Microsoft Docs"
description: "Informazioni sulle proprietà di installazione del client in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
caps.latest.revision: 15
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 55c953f312a9fb31e7276dde2fdd59f8183b4e4d
ms.openlocfilehash: fa6a613bb2b69be923917399da6b45f0c5cfcc6f

---
# <a name="about-client-installation-properties-in-system-center-configuration-manager"></a>Informazioni sulle proprietà di installazione del client in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare il comando CCMSetup.exe di System Center Configuration Manager per installare manualmente il software client di Configuration Manager nei computer aziendali.  

##  <a name="a-nameaboutccmsetupa-about-ccmsetupexe"></a><a name="aboutCCMSetup"></a> Informazioni su CCMSetup.exe  
 Il comando CCMSetup.exe consente di scaricare tutti i file necessari per completare l'installazione client da un punto di gestione specificato o da un percorso di origine specificato. Questi file possono includere:  

-   Il pacchetto Client.msi di Windows Installer che consente di installare il software client di Configuration Manager.  

-   I file di installazione del Servizio trasferimento intelligente in background (BITS) di Microsoft, se necessari.  

-   File installazione di Windows Installer, se necessari.  

-   Aggiornamenti e correzioni per il client di Configuration Manager, se necessari.  

> [!NOTE]  
>  Non è possibile eseguire il file Client.msi direttamente in Configuration Manager.  

 CCMSetup.exe fornisce diverse proprietà della riga di comando per la personalizzazione del comportamento di installazione. È inoltre possibile specificare proprietà per la modifica del comportamento di Client.msi nella riga di comando CCMSetup.exe.  

> [!IMPORTANT]  
>  Prima di specificare le proprietà per Client.msi, è necessario specificare tutte le proprietà CCMSetup richieste.  

 CCMSetup.exe e i relativi file di supporto si trovano nel server del sito di Configuration Manager nella cartella **Client** della cartella di installazione di Configuration Manager. La cartella è condivisa in rete in **&lt;nome server del sito\>\SMS_&lt;codice sito\>\Client**.  

 Al prompt dei comandi, il comando CCMSetup.exe usa il seguente formato:  

 **CCMSetup.exe [&lt;proprietà di Ccmsetup\>] [&lt;proprietà di installazione di client.msi>]**  

 Esempio:  

 **CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01**  

 Questo comando di esempio esegue le azioni seguenti:  

-   Specifica il punto di gestione denominato SMSMP01 per richiedere un elenco di punti di distribuzione per il download dei file di origine dell'installazione client.  

-   Specifica che è necessario interrompere l'installazione se nel computer esiste già una versione del client di Configuration Manager.  

-   Indica a client.msi di assegnare il client al codice del sito S01.  

-   Indica a client.msi di usare il punto di stato di fallback denominato SMSFP01.  

> [!NOTE]  
>  Se una proprietà contiene spazi, racchiuderla tra virgolette ("").  

 Le proprietà descritte nella seguente tabella sono disponibili per la modifica del comportamento di installazione di CCMSetup.exe.  

> [!IMPORTANT]  
>  Se lo schema di Active Directory è stato esteso per Configuration Manager, molte proprietà di installazione client vengono pubblicate in Active Directory Domain Services e lette automaticamente dal client di Configuration Manager. Per un elenco delle proprietà di installazione client pubblicate in Servizi di dominio Active Directory, vedere [Informazioni sulle proprietà di installazione client pubblicate in Servizi di dominio Active Directory in System Center Configuration Manager](about-client-installation-properties-published-to-active-directory-domain-services.md).  

##  <a name="a-namebkmkccmsetupcommandlinea-ccmsetupexe-command-line-properties"></a><a name="BKMK_CCMSetupCommandLine"></a> Proprietà della riga di comando CCMSetup.exe  

### <a name=""></a>/?  

Apre la finestra di dialogo **CCMSetup** in cui vengono visualizzate le proprietà della riga di comando per ccmsetup.exe.  

Esempio: **ccmsetup.exe /?**  

### <a name="sourceltpath"></a>/source:&lt;percorso\>  

 Specifica il percorso da cui scaricare i file di installazione. È possibile usare un percorso di installazione locale o UNC. I file vengono scaricati usando il protocollo SMB (server message block).  

> [!NOTE]  
>  È possibile usare più volte la proprietà **/source** nella riga di comando per specificare percorsi alternativi da cui scaricare i file di installazione.  

> [!IMPORTANT]  
>  Per usare la proprietà della riga di comando **/source** , l'account utente Windows usato per l'installazione client deve disporre delle autorizzazioni di  lettura per il percorso di installazione.  

 Esempio: **ccmsetup.exe /source:"\\\computer\cartella"**  

### <a name="mpltcomputer"></a>/mp:&lt;computer\>

 Specifica un punto di gestione di origine per consentire ai computer di connettersi e individuare il punto di distribuzione più vicino per il download dei file di installazione client. Se non sono presenti punti di distribuzione oppure i computer non sono in grado di scaricare i file dai punti di distribuzione dopo 4 ore, i client scaricano i file dal punto di gestione specificato.  

 I computer scaricano i file tramite una connessione HTTP o HTTPS, a seconda della configurazione del ruolo del sistema del sito per le connessioni client. Il download usa la limitazione BITS, se configurata. Se tutti i punti di distribuzione e di gestione sono configurati solo per le connessioni client HTTPS, è necessario verificare che il computer client disponga di un certificato client di infrastruttura a chiave pubblica (PKI) valido.  

> [!NOTE]  
>  È possibile usare la proprietà della riga di comando **/mp** per specificare più punti di gestione e fare in modo che, se il computer non riesce a connettersi al primo, vengano eseguiti tentativi di connessione con gli altri punti di gestione. Quando si specificano più punti di gestione, è necessario separare i valori tramite punto e virgola.  

> [!IMPORTANT]  
>  Questa proprietà viene usata solo per specificare un punto di gestione iniziale che consente ai computer di individuare l'origine più vicina per il download dei file di installazione client. La proprietà non specifica il punto di gestione a cui verrà assegnato il client dopo l'installazione. È possibile specificare un punto qualsiasi di gestione di Configuration Manager in un sito qualsiasi per offrire ai computer un elenco di punti di distribuzione da cui scaricare i file di installazione del client.  

 Esempio di uso del nome computer: **ccmsetup.exe /mp:SMSMP01**  

 Esempio di uso dell'FQDN: **ccmsetup.exe /mp:smsmp01.contoso.com**  

> [!TIP]  
>  Se il client si connette a un punto di gestione mediante HTTPS, in genere per questa opzione è necessario specificare l'FQDN anziché il nome computer. Il valore specificato deve essere presente nell'oggetto o nel nome alternativo oggetto del certificato PKI del punto di gestione. Nonostante Configuration Manager supporti un solo nome computer in questo certificato PKI per le connessioni nell'Intranet, per sicurezza è consigliabile inserire un FQDN.  

### <a name="retryltminutes"></a>/retry:&lt;minuti\>

Specifica l'intervallo tra tentativi se CCMSetup.exe non riesce a scaricare i file di installazione. Il valore predefinito è **10** minuti. CCMSetup continua a tentare fino a quando non raggiunge il limite specificato nella proprietà di installazione **downloadtimeout** .  

Esempio: **ccmsetup.exe /retry:20**  

### <a name="noservice"></a>/noservice

Impedisce l'esecuzione di CCMSetup come servizio. Quando CCMSetup viene eseguito come servizio, l'esecuzione avviene nell'ambito dell'account di sistema locale del computer, che potrebbe disporre di diritti insufficienti per l'accesso alle risorse di rete richieste per il processo di installazione. Quando viene specificata l'opzione **/noservice** , CCMSetup.exe viene eseguito nell'ambito dell'account utente usato per avviare il processo di installazione. Se inoltre si usa uno script per l'esecuzione di CCMSetup.exe con la proprietà **/service** , CCMSetup.exe viene chiuso dopo l'avvio del servizio e potrebbe non segnalare correttamente i dettagli di installazione perché il servizio CCMSetup esegue l'installazione client. Se questa proprietà della riga di comando non è specificata, verrà usata la proprietà **/service** per impostazione predefinita.  

Esempio: **ccmsetup.exe /noservice**  

### <a name="service"></a>/service

Specifica che CCMSetup deve essere eseguito come un servizio che usa l'account di sistema locale.  

Esempio: **ccmsetup.exe /service**  

### <a name="uninstall"></a>/uninstall

Specifica che deve essere disinstallato il software client di Configuration Manager. Per altre informazioni, vedere [How to manage clients in System Center Configuration Manager](../manage/manage-clients.md).  

Esempio: **ccmsetup.exe /uninstall**  

### <a name="logon"></a>/logon

Specifica che l'installazione del client deve essere interrotta se una versione di Configuration Manager o del client di Configuration Manager è già installata.  

Esempio: **ccmsetup.exe /logon**  

### <a name="forcereboot"></a>/forcereboot

 Specifica che, se necessario, CCMSetup deve forzare il riavvio del computer client per completare l'installazione client. Se questa opzione non è specificata, CCMSetup viene chiuso quando è necessario un riavvio e continua dopo il successivo riavvio manuale.  

 Esempio: **CCMSetup.exe /forcereboot**  

### <a name="bitspriorityltpriority"></a>/BITSPriority:&lt;priorità\>

 Specifica la priorità di download quando vengono scaricati i file di installazione client tramite una connessione HTTP. I possibili valori sono i seguenti:  

-   FOREGROUND  

-   HIGH  

-   NORMAL  

-   LOW  

 Il valore predefinito è NORMAL.  

 Esempio: **ccmsetup.exe /BITSPriority:HIGH**  

### <a name="downloadtimeoutltminutes"></a>/downloadtimeout:&lt;minuti\>

Specifica l'intervallo di tempo in minuti in cui CCMSetup tenta di scaricare i file di installazione client prima di rinunciare. Il valore predefinito è **1440** minuti (1 giorno).  

Esempio: **ccmsetup.exe /downloadtimeout:100**  

### <a name="usepkicert"></a>/UsePKICert

 Quando viene specificato, il client usa un certificato PKI che include l'autenticazione del client, se disponibile. Se non viene trovato un certificato valido, il client tenta di usare una connessione HTTP e un certificato autofirmato. Quando questa opzione non è specificata, il client usa un certificato autofirmato e tutte le comunicazioni con i sistemi del sito avvengono tramite HTTP.  

> [!NOTE]  
>  Esistono scenari in cui non è necessario specificare questa proprietà quando si installa un client per l'utilizzo di un certificato client PKI. Tali scenari includono l'installazione di un client mediante installazione client basata sul punto di aggiornamento software e installazione push client. È tuttavia necessario specificare questa proprietà se si esegue l'installazione manuale di un client e si usa la proprietà **/mp** per specificare un punto di gestione configurato per accettare solo connessioni client HTTPS. È inoltre necessario specificare questa proprietà quando viene installato un client solo per la comunicazione Internet, usando la proprietà CCMALWAYSINF=1 (oltre alle proprietà per il punto di gestione basato su Internet e al codice del sito). Per altre informazioni sulla gestione client basata su Internet, vedere [Considerazioni per le comunicazioni client da Internet o da una foresta non trusted](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) in [Comunicazioni tra gli endpoint in System Center Configuration Manager](../../plan-design/hierarchy/communications-between-endpoints.md).  

 Esempio: **CCMSetup.exe /UsePKICert**  

### <a name="nocrlcheck"></a>/NoCRLCheck

 Specifica che un client non deve verificare l'elenco di revoche di certificati (CRL) in caso di comunicazione tramite HTTPS usando un certificato PKI.  

 Quando questa opzione non è specificata, il client controlla l'elenco di revoche di certificati prima di stabilire una connessione HTTPS usando i certificati PKI.  

 Per altre informazioni sul controllo CRL client, vedere [Planning for PKI certificate revocation](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs) in[Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Esempio: **CCMSetup.exe /UsePKICert /NoCRLCheck**  

### <a name="configltconfiguration-file"></a>/config:&lt;file di configurazione\>

Specificare il nome di un file di testo contenente le proprietà di installazione client. A meno che non venga specificata anche la proprietà **/noservice** di CCMSetup, questo file deve trovarsi nella cartella CCMSetup, ovvero %Windir%\\Ccmsetup per sistemi operativi a 32 e a 64 bit. Se viene specificata la proprietà **/noservice** , questo file deve essere posizionato nella stessa cartella da cui è stato eseguito CCMSetup.exe.  

Esempio: **CCMSetup.exe /config:&lt;nome file configurazione.txt\>**  

Usare il file mobileclienttemplate.tcf nella cartella &lt;directory di Configuration Manager\>\\bin\\&lt;piattaforma\> del computer del server del sito per specificare il formato corretto del file. Questo file contiene inoltre informazioni in forma di commento relative alle sezioni e alle modalità di utilizzo. Specificare le proprietà di installazione cliente nella sezione [Client Install], dopo il testo seguente: **Install=INSTALL=ALL**.  

Voce della sezione [Client Install] di esempio: **Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100**  

### <a name="skipprereqltfilename"></a>/skipprereq:&lt;nome file\>

 Specifica che CCMSetup.exe non deve installare il programma definito come prerequisito se il client di Configuration Manager è installato.  

 Esempi: **CCMSetup.exe /skipprereq:silverlight.exe** o **CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;Silverlight.exe**  

> [!NOTE]  
>  Questa proprietà supporta l'immissione di valori multipli. Usare il punto e virgola (;) per separare i valori.  

### <a name="forceinstall"></a>/forceinstall

 Specificare che tutti i client esistenti verranno disinstallati prima dell'installazione di un nuovo client.  

### <a name="excludefeaturesltfeature"></a>/ExcludeFeatures:&lt;funzionalità\>

Specifica che CCMSetup.exe non installerà la funzionalità indicata se il client di Configuration Manager è installato.  

Esempio: **CCMSetup.exe /ExcludeFeatures:ClientUI** non installerà Software Center nel client.  

> [!NOTE]  
>  Per questa versione, **ClientUI** è l'unico valore supportato con la proprietà **/ExcludeFeatures** .  

##  <a name="a-nameccmsetupreturncodesa-ccmsetupexe-return-codes"></a><a name="ccmsetupReturnCodes"></a> Codici restituiti di CCMSetup.exe  
 Il comando CCMSetup.exe fornisce i seguenti codici restituiti quando viene completato. Per risolvere i problemi relativi all'esecuzione del comando, consultare il file ccmsetup.log nel computer client per determinare il contesto e i dettagli aggiuntivi sui problemi del codice restituito.  

|Codice restituito|Significato|  
|-----------------|-------------|  
|0|Operazione completata|  
|6|Errore|  
|7|Riavvio richiesto|  
|8|Installazione già in esecuzione|  
|9|Errore di valutazione dei prerequisiti|  
|10|Errore di convalida dell'hash manifesto di installazione|  

##  <a name="a-nameclientmsipropsa-clientmsi-properties"></a><a name="clientMsiProps"></a> Proprietà Client.msi  
 Le proprietà seguenti possono modificare il comportamento dell'installazione di client.msi. Se si utilizza il metodo di installazione push del client, è anche possibile specificare le proprietà nella scheda **Client** della finestra di dialogo **Proprietà installazione push client** .  

### <a name="ccmadmins"></a>CCMADMINS  

Specifica uno o più gruppi o account utente di Windows per ottenere l'accesso ai criteri e le impostazioni del client. Questa opzione è utile quando l'amministratore di Configuration Manager non dispone di credenziali amministrative locali nel computer client. È possibile specificare un elenco di account separati da un punto e virgola.  

Esempio: **CCMSetup.exe CCMADMINS="Dominio\Account1;Dominio\Gruppo1"**  

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

Specifica che il computer può eseguire il riavvio dopo l'installazione del client, se necessario.  

> [!IMPORTANT]  
>  Il computer verrà riavviato senza preavviso anche se un utente è connesso.  

Esempio: **CCMSetup.exe  CCMALLOWSILENTREBOOT**  

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

 Impostare su 1 per specificare che il client sarà sempre basato su Internet e non si connetterà mai a Intranet. Il tipo di connessione del client visualizza **Sempre Internet**.  

 Questa proprietà deve essere usata insieme a CCMHOSTNAME, che specifica l'FQDN del punto di gestione basato su Internet. Va inoltre usata insieme alla proprietà CCMSetup /UsePKICert e al codice del sito.  

 Per altre informazioni sulla gestione client basata su Internet, vedere [Considerazioni per le comunicazioni client da Internet o da una foresta non trusted](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) in [Comunicazioni tra gli endpoint in System Center Configuration Manager](../../plan-design/hierarchy/communications-between-endpoints.md).  

 Esempio: **CCMSetup.exe /UsePKICert  CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC**  

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

 Specifica l'elenco delle autorità di certificazione, ovvero un elenco di autorità di certificazione radice attendibili (CA) ritenuti attendibili dal sito di Configuration Manager.  

 Per altre informazioni sull'elenco delle autorità di certificazione e sulle relative modalità d'uso da parte dei client durante il processo di selezione dei certificati, vedere [Planning for PKI client certificate selection](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection) in [Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Si tratta di una corrispondenza con distinzione tra maiuscole e minuscole per gli attributi del soggetto presenti nel certificato CA radice. Gli attributi possono essere separati da virgola (,) o punto e virgola (;). È possibile specificare più certificati CA radice mediante una barra di separazione. Esempio:  

 **CCMCERTISSUERS="CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US &amp;#124; CN=Litware Corporate Root CA; O=Litware, Inc."**  

> [!TIP]  
>  Fare riferimento al file mobileclient.tcf nella cartella &lt;directory di Configuration Manager\>\bin\\&lt;piattaforma\> del computer del server del sito per copiare il valore **CertificateIssuers=&lt;stringa\>** configurato per il sito.  

### <a name="ccmcertsel"></a>CCMCERTSEL

 Specifica i criteri di selezione del certificato se il client dispone di più di un certificato utilizzabile per la comunicazione HTTPS (un certificato valido che include la funzionalità di autenticazione client).  

 È possibile cercare una corrispondenza esatta in Nome soggetto o Nome alternativo soggetto (utilizzare **Subject:**) o una corrispondenza parziale (utilizzare **SubjectStr:)**, in Nome soggetto o Nome alternativo soggetto. Esempi:  

 **CCMCERTSEL="Subject:computer1.contoso.com"** esegue la ricerca di un certificato con una corrispondenza esatta al nome computer "computer1.contoso.com" nel nome oggetto o nel nome alternativo oggetto.  

 **CCMCERTSEL="SubjectStr:contoso.com"** esegue la ricerca di un certificato che contiene "contoso.com" nel nome oggetto o nel nome alternativo oggetto.  

 È inoltre possibile usare l'identificatore di oggetto (OID) o gli attributi del nome distinto negli attributi Nome oggetto o Nome alternativo oggetto, ad esempio:  

 **CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"** esegue la ricerca dell'attributo dell'unità organizzativa espresso come un identificatore di oggetto e denominato Computers.  

 **CCMCERTSEL="SubjectAttr:OU = Computers"** esegue la ricerca dell'attributo dell'unità organizzativa espresso come un nome distinto e denominato Computers.  

> [!IMPORTANT]  
>  Se si usa la casella Nome soggetto, il processo di corrispondenza per il valore del criterio di selezione **Subject:** distingue tra maiuscole e minuscole, mentre il processo di corrispondenza per **SubjectStr:** non esegue la distinzione.  
>   
>  Se si usa la casella Nome alternativo soggetto, il processo di corrispondenza per il valore del criterio di selezione **Subject:** distingue tra maiuscole e minuscole, mentre il processo di corrispondenza per **SubjectStr:** non esegue la distinzione.  

 L'elenco completo degli attributi che è possibile usare per la selezione dei certificati è disponibile in [Valori attributi supportati per i criteri di selezione del certificato PKI](#BKMK_attributevalues).  

 Se più di un certificato corrisponde alle ricerca e la proprietà CCMFIRSTCERT è stata impostata su 1, viene selezionato il certificato con il periodo di validità più lungo.  

### <a name="ccmcertstore"></a>CCMCERTSTORE

 Specifica un nome archivio certificati alternativo se il certificato client da usare per le comunicazioni HTTPS non si trova nell'archivio certificati predefinito di **Personale** nell'archivio del computer.  

 Esempio: **CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"**  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

  Consente la registrazione debug. I valori possono essere impostati su 0 (disattivata) o 1 (attivata). Il valore predefinito è 0. In questo modo il client registra le informazioni di basso livello che potrebbero essere utili per la risoluzione di problemi. Come procedura consigliata, evitare l'utilizzo di questa proprietà nei siti di produzione perché potrebbe causare un numero eccessivo di registrazioni, che renderebbe difficile l'individuazione di informazioni rilevanti nei file di log. CCMENABLELOGGING deve essere impostata su TRUE per consentire la registrazione debug.  

  Esempio: **CCMSetup.exe CCMDEBUGLOGGING=1**  

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

  Attiva la registrazione se questa proprietà è impostata su TRUE. Per impostazione predefinita, la registrazione è attivata. I file di log vengono archiviati nella cartella **Logs** della cartella di installazione del client di Configuration Manager. Per impostazione predefinita, questa cartella è %Windir%\CCM\Logs.  

  Esempio: **CCMSetup.exe CCMENABLELOGGING=TRUE**  

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL  

 Specifica la frequenza quando si esegue lo strumento di valutazione dell'integrità del client (ccmeval.exe). È possibile specificare un valore compreso tra **1** e **1440** minuti. Se non si specifica questa proprietà o se si specifica un valore non corretto, la valutazione verrà eseguita una volta al giorno.  

### <a name="ccmevalhour"></a>CCMEVALHOUR

 Specificare l'ora in cui eseguire lo strumento di valutazione dell'integrità del client (ccmeval.exe). È possibile specificare un valore compreso tra **0** (mezzanotte) e **23** (23.00). Se non si specifica questa proprietà o se si specifica un valore non corretto, la valutazione verrà eseguita a mezzanotte.  

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

 Se impostata su 1, questa proprietà specifica che il client deve selezionare il certificato PKI con il periodo di validità più lunga. Questa impostazione potrebbe essere necessaria se si usa Protezione accesso alla rete con l'imposizione IPsec.  

 Esempio: **CCMSetup.exe /UsePKICert CCMFIRSTCERT=1**  

### <a name="ccmhostname"></a>CCMHOSTNAME

 Specifica l'FQDN del punto di gestione basato su Internet, se il client viene gestito in Internet.  

 Non specificare questa opzione con la proprietà di installazione SMSSITECODE=AUTO. I client basati su Internet devono essere assegnati direttamente ai relativi siti basati su Internet.  

 Esempio: **CCMSetup.exe  /UsePKICert/ CCMHOSTNAME="SMSMP01.corp.contoso.com"**  

### <a name="ccmhttpport"></a>CCMHTTPPORT

 Specifica la porta che il client deve usare durante la comunicazione su HTTP con i server del sistema del sito.  

 Se la porta non viene specificata, verrà usato il valore predefinito 80.  

 Esempio: **CCMSetup.exe CCMHTTPPORT=80**  

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

Specifica la porta che il client deve usare durante la comunicazione su HTTPS con i server del sistema del sito. Se la porta non viene specificata, verrà usato il valore predefinito 443.  

Esempio: **CCMSetup.exe /UsePKICert CCMHTTPSPORT=443**  

### <a name="ccminstalldir"></a>CCMINSTALLDIR

 Identifica la cartella in cui sono installati i file del client di Configuration Manager. Se questa proprietà non è impostata, il software client viene installato nella cartella *%Windir%*\CCM. Indipendentemente dalla posizione in cui sono installati questi file, il file Ccmcore.dll viene sempre installato nella cartella *%Windir%\System32* . Nei sistemi operativi a 64 bit viene sempre installata una copia del file Ccmcore.dll nella cartella *%Windir%*\SysWOW64 per il supporto di applicazioni a 32 bit che usano la versione a 32 bit degli API client di Configuration Manager dall'SDK (Software Developer Kit) di Configuration Manager.  

 Esempio: **CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"**  

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Specifica la quantità di dettagli da scrivere nei file di registro di Configuration Manager. Specificare un numero intero compreso tra 0 e 3, dove 0 è la registrazione più dettagliata e 3 registra solo gli errori. Il valore predefinito è 1.  

Esempio: **CCMSetup.exe CCMLOGLEVEL=3**  

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Quando un file di log di Configuration Manager raggiunge una dimensione di 250000 byte (o il valore specificato dalla proprietà CCMLOGMAXSIZE), viene rinominato come file di backup e un nuovo file di log viene creato.  

Questa proprietà specifica il numero di versioni precedenti del file di log da conservare. Il valore predefinito è 1. Se il valore è impostato su 0, non viene mantenuto alcun file di log precedente.  

Esempio: **CCMSetup.exe CCMLOGMAXHISTORY=0**  

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

Specifica la dimensione massima del file di log in byte. Quando un file di log raggiunge la dimensione specificata, viene rinominato come un file di cronologia e viene creato un nuovo file. Questa proprietà deve essere impostata almeno su 10000 byte. Il valore predefinito è 250000 byte.  

Esempio: **CCMSetup.exe CCMLOGMAXSIZE=300000**  

### <a name="disablesiteopt"></a>DISABLESITEOPT

 Se è impostata su TRUE, questa proprietà non consente agli utenti finali con credenziali amministrative nel computer client di modificare il sito assegnato al client di Configuration Manager tramite Configuration Manager nel Pannello di controllo del computer client.  

 Esempio: **CCMSetup.exe DISABLESITEOPT=TRUE**  

### <a name="disablecacheopt"></a>DISABLECACHEOPT

Se è impostata su TRUE, questa proprietà non consente agli utenti finali con credenziali amministrative nel computer client di modificare le impostazioni della cartella cache client per il client di  Configuration Manager tramite Configuration Manager nel Pannello di controllo del computer client.  

Esempio: **CCMSetup.exe DISABLECACHEOPT=TRUE**  

### <a name="dnssuffix"></a>DNSSUFFIX

 Specifica un dominio DNS che i client usano per individuare i punti di gestione pubblicati in DNS. Una volta individuato un punto di gestione, tale punto fornisce informazioni al client in merito ad altri punti di gestione nella gerarchia. Ciò significa che il punto di gestione individuato usando la pubblicazione DNS non deve provenire dal sito del client, ma può essere un qualsiasi punto di gestione nella gerarchia.  

> [!NOTE]  
>  Non è necessario specificare questa proprietà se il client si trova nello stesso dominio del punto di gestione pubblicato. In questo scenario, il dominio del client viene usato automaticamente per la ricerca nel DNS dei punti di gestione.  

 Per altre informazioni sulla pubblicazione DNS come metodo di posizione del servizio per i client di Configuration Manager, vedere [Posizione del servizio e modo in cui i client determinano il relativo punto di gestione assegnato](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location) in [Informazioni su come i client trovano i servizi e le risorse del sito per System Center Configuration Manager](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

> [!NOTE]  
>  Per impostazione predefinita, la pubblicazione DNS non è abilitata in Configuration Manager.  

 Esempio: **CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com**  

### <a name="fsp"></a>FSP

Specifica il punto di stato di fallback che riceve ed elabora i messaggi di stato inviati dai computer client di Configuration Manager.  

Per altre informazioni sul punto di stato di fallback, vedere la sezione [Determinare se è richiesto un punto di stato di fallback](plan/determine-the-site-system-roles-for-clients.md#BKMK_Determine_FSP) in [Determinare i ruoli del sistema del sito per System Center Configuration Manager](plan/determine-the-site-system-roles-for-clients.md).  

Esempio: **CCMSetup.exe FSP=SMSFP01**  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

 Specifica che l'esistenza della versione minima richiesta di Microsoft Application Virtualization (App-V) non viene verificata prima di installare il client.  

> [!IMPORTANT]  
>  Se si installa il client di Configuration Manager senza installare App-V, non è possibile distribuire applicazioni virtuali.  

 Esempio: **CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE**  

### <a name="notifyonly"></a>NOTIFYONLY

Specifica che lo stato del client segnalerà, ma non correggerà, i problemi rilevati con il client di Configuration Manager.  

Esempio: **CCMSetup.exe NOTIFYONLY=TRUE**  

Per ulteriori informazioni, vedere [How to configure client status in System Center Configuration Manager](configure-client-status.md).  

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

 Se un client di Configuration Manager ha la chiave radice attendibile di Configuration Manager errata e non può contattare un punto di gestione attendibile per ricevere una copia valida della nuova chiave radice attendibile, è necessario rimuovere manualmente la vecchia chiave radice attendibile usando questa proprietà. Generalmente questa situazione si verifica quando si sposta un client da una gerarchia del sito a un'altra. Questa proprietà viene applicata ai client che usano la comunicazione client HTTP e HTTPS.  

 Esempio: **CCMSetup.exe RESETKEYINFORMATION=TRUE**  

### <a name="sitereassign"></a>SITEREASSIGN

Consente la riassegnazione automatica del sito per gli aggiornamenti client se usata con [SMSSITECODE](#smssitecode)=AUTO.

Esempio: **CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE**

### <a name="smscachedir"></a>SMSCACHEDIR

Specifica il percorso della cartella cache client nel computer client in cui vengono archiviati i file temporanei. Per impostazione predefinita, il percorso è *%Windir \ccmcache*.  

Esempio: **CCMSetup.exe SMSCACHEDIR="C:\Temp"**  

Questa proprietà può essere usata insieme alla proprietà SMSCACHEFLAGS per controllare ulteriormente il percorso della cartella cache client.  

Esempio: **CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE** consente di installare la cartella cache client nell'unità disco più grande disponibile nel client.  

### <a name="smscacheflags"></a>SMSCACHEFLAGS

Configura la cartella cache di Configuration Manager in cui vengono archiviati i file temporanei. È possibile usare le proprietà SMSCACHEFLAGS singolarmente o combinate, separate da punti e virgola. Se questa proprietà non viene specificata, la cartella cache client viene installata in base alla proprietà SMSCACHEDIR, la cartella non viene compressa e il valore di SMSCACHESIZE viene usato come dimensione in MB della cartella.  

Specifica ulteriori dettagli di installazione per la cartella cache client. È possibile specificare le seguenti proprietà:  

-   PERCENTDISKSPACE: specifica la dimensione della cartella come percentuale dello spazio totale su disco. Se si specifica questa proprietà, è necessario specificare anche la proprietà SMSCACHESIZE come valore di percentuale da usare.  

-   PERCENTFREEDISKSPACE: specifica la dimensione della cartella come percentuale dello spazio libero su disco. Se si specifica questa proprietà, è necessario specificare anche la proprietà SMSCACHESIZE come valore di percentuale da usare. Ad esempio, se nel disco sono disponibili 10 MB di spazio e SMSCACHESIZE viene specificata su 50, la dimensione della cartella è impostata su 5 MB. È impossibile usare questa proprietà con la proprietà PERCENTDISKSPACE.  

-   MAXDRIVE: specifica che la cartella deve essere installata nel disco più grande disponibile. Questo valore verrà ignorato se è stato specificato un percorso con la proprietà SMSCACHEDIR.  

-   MAXDRIVESPACE: specifica che la cartella deve essere installata nell'unità disco con più spazio libero. Questo valore verrà ignorato se è stato specificato un percorso con la proprietà SMSCACHEDIR.  

-   NTFSONLY: specifica che la cartella può essere installata solo in unità disco formattate con il file system NTFS. Questo valore verrà ignorato se è stato specificato un percorso con la proprietà SMSCACHEDIR.  

-   COMPRESS: specifica che la cartella deve essere mantenuta in formato compresso.  

-   FAILIFNOSPACE: specifica che il software client deve essere rimosso se non è disponibile spazio sufficiente per installare la cartella.  

> [!NOTE]  
>  È possibile specificare più proprietà per questa proprietà separandole con un punto e virgola.  

Se questa proprietà non viene specificata, la cartella cache client verrà creata in base alla proprietà SMSCACHEDIR, non verrà compressa e avrà una dimensione corrispondente a quella specificata nella proprietà SMSCACHESIZE.  

Esempio: **CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS**  

> [!NOTE]  
>  Questa impostazione viene ignorata quando si aggiorna un client esistente.  

### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> In Configuration Manager versione 1606 sono disponibili nuove impostazioni client per specificare le dimensioni della cartella della cache del client. Queste nuove impostazioni client sostituiscono in modo efficace l'uso di SMSCACHESIZE come proprietà di client.msi per specificare le dimensioni della cache del client. Per altre informazioni, vedere [le impostazioni client per le dimensioni della cache](about-client-settings.md#client-cache-settings).  

Per la versione 1602 e le versioni precedenti SMSCACHESIZE specifica le dimensioni della cartella della cache del client in megabyte (MB) o sotto forma di percentuale, se viene usata con la proprietà PERCENTDISKSPACE o PERCENTFREEDISKSPACE. Se questa proprietà non viene impostata, per impostazione predefinita la cartella presenta una dimensione massima di 5120 MB. Il valore più basso che è possibile specificare è 1 MB.  

> [!NOTE]  
>  Se a causa di un nuovo pacchetto che deve essere scaricato la cartella supera la dimensione massima e non può essere ripulita per creare spazio sufficiente, il download del pacchetto ha esito negativo e il programma o l'applicazione non vengono eseguiti.  

Questa impostazione viene ignorata quando si aggiorna un client esistente e quando il client scarica gli aggiornamenti software.  

Esempio: **CCMSetup.exe SMSCACHESIZE=100**  

> [!NOTE]  
>  Se si reinstalla un client, è impossibile usare le proprietà di installazione SMSCACHESIZE o SMSCACHEFLAGS per ridurre la dimensione della cache rispetto a prima. Se si tenta di eseguire questa operazione, il valore viene ignorato e la dimensione della cache viene impostata automaticamente sull'ultima dimensione precedente.  
>   
>  Se ad esempio si installa il client con la dimensione della cache predefinita 5120 MB e quindi si reinstalla tale client con una dimensione della cache di 100 MB, la dimensione della cartella cache nel client reinstallato verrà impostata su 5120 MB.  


### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

Specifica il percorso e l'ordine in cui il programma di installazione di Configuration Manager verifica le impostazioni di configurazione. La proprietà è una stringa contenente uno o più caratteri, ognuno dei quali definisce un'origine di configurazione specifica. Usare i valori dei caratteri R, P, M e U, singolarmente o combinati, come illustrato nei seguenti esempi:  

-   R: cerca le impostazioni di configurazione nel Registro di sistema.  

   Per altre informazioni, vedere le [informazioni sull'archiviazione delle proprietà di installazione del client nel Registro di sistema](https://technet.microsoft.com/library/gg712298.aspx#BKMK_Provision).  

-   P: cerca le impostazioni di configurazione nelle proprietà di installazione fornite al prompt dei comandi.  

-   M: verifica le impostazioni esistenti durante l'aggiornamento di un client precedente con il software client di Configuration Manager.  

-   U: aggiorna il client installato a una versione più recente (e usa il codice sito assegnato).  

 Per impostazione predefinita, l'installazione client usa `PU` per cercare innanzitutto le proprietà di installazione e quindi le impostazioni esistenti.  

 Esempio: **CCMSetup.exe SMSCONFIGSOURCE=RP**  

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

 Specifica se il client può usare Windows Internet Name Service (WINS) per trovare un punto di gestione che accetti le connessioni HTTP. I client usano questo metodo quando non riescono a trovare un punto di gestione in Servizi di dominio Active Directory o in DNS.  

 Questa proprietà è indipendente dall'utilizzo di WINS da parte del client per la risoluzione dei nomi.  

 È possibile configurare due diverse modalità per questa proprietà:  

-   NOWINS: si tratta dell'impostazione più sicura per questa proprietà che impedisce ai client di trovare un punto di gestione in WINS.  Quando si usa questa impostazione, i client devono usare un metodo alternativo per individuare un punto di gestione in Intranet, come ad esempio Servizi di dominio Active Directory o tramite la pubblicazione DNS.  

-   WINSSECURE: in questa modalità un client che usa la comunicazione HTTP può usare WINS per trovare un punto di gestione. Tuttavia, il client deve disporre di una copia della chiave radice attendibile prima di potersi connettere al punto di gestione. Per altre informazioni, vedere [Planning for the Trusted Root Key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) in [Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Se questa proprietà non viene specificata, viene usato il valore predefinito di WINSSECURE.  

 Esempio: **CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS**  

### <a name="smsmp"></a>SMSMP

Specifica un punto di gestione iniziale usato dal client di Configuration Manager.  

> [!IMPORTANT]  
>  Se il punto di gestione accetta solo connessioni client su HTTPS (non consente connessioni client HTTP), è necessario aggiungere al nome del punto di gestione il prefisso https://.  

Esempio: **CCMSetup.exe SMSMP=smsmp01.contoso.com**  

Esempio: **CCMSetup.exe SMSMP=smsmp01.contoso.com**  

Esempio: **CCMSetup.exe SMSMP=https://smsmp01.contoso.com**  

### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

 Specifica la chiave radice attendibile di Configuration Manager quando non può essere recuperata da Servizi di dominio Active Directory. Questa proprietà viene applicata ai client che usano la comunicazione client HTTP e HTTPS. Per altre informazioni, vedere [Planning for the Trusted Root Key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) in [Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Esempio: **CCMSetup.exe SMSPUBLICROOTKEY=&lt;chiave\>**  

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

 Consente di reinstallare la chiave radice attendibile di Configuration Manager. Specifica il percorso completo e il nome file di un file che contiene la chiave radice attendibile. Questa proprietà viene applicata ai client che usano la comunicazione client HTTP e HTTPS. Per altre informazioni, vedere [Planning for the Trusted Root Key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) in [Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Esempio: CCMSetup.exe **SMSROOTKEYPATH=&lt;percorso e nome file completi\>**  

### <a name="smssigncert"></a>SMSSIGNCERT

 Specifica il percorso completo e il nome file con estensione cer del certificato autofirmato esportato nel server del sito.  

 Il certificato viene archiviato nell'archivio certificati **SMS** e dispone del Nome oggetto **Server del sito** e del nome descrittivo **Certificato di firma del server del sito**.  

 Esempio: **CCMSetup.exe /UsePKICert SMSSIGNCERT=&lt;percorso e nome file completi\>**  

### <a name="smssitecode"></a>SMSSITECODE

 Specifica il sito di Configuration Manager al quale assegnare il client di Configuration Manager. Può trattarsi di un codice del sito con tre caratteri o della parola AUTO. Se si specifica AUTO o se questa proprietà non viene specificata, il client prova a stabilire la relativa assegnazione sito di Configuration Manager da Active Directory Domain Services o da un punto di gestione specificato. Per abilitare la proprietà AUTO per gli aggiornamenti client, è necessario anche impostare [SITEREASSIGN](#sitereassign) su TRUE.    

> [!NOTE]  
>  Non usare AUTO se si specifica anche il punto di gestione basato su Internet (CCMHOSTNAME). In questo scenario, è necessario assegnare direttamente il client al relativo sito.  

 Esempio: **CCMSetup.exe SMSSITECODE=XZY**  

##  <a name="a-namebkmkattributevaluesa-supported-attribute-values-for-the-pki-certificate-selection-criteria"></a><a name="BKMK_attributevalues"></a> Valori attributi supportati per i criteri di selezione del certificato PKI  
 Configuration Manager supporta i valori seguenti di attributi per i criteri di selezione del certificato PKI:  

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



<!--HONumber=Dec16_HO3-->



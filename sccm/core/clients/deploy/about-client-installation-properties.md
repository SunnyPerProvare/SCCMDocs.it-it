---
title: "Proprietà di installazione del client | Microsoft Docs"
description: "Informazioni sulle proprietà di installazione del client in System Center Configuration Manager."
ms.custom: na
ms.date: 01/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
caps.latest.revision: "15"
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.openlocfilehash: 36bcbbca4fdee3e95d293c436a105a41a6e3953e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="about-client-installation-properties-in-system-center-configuration-manager"></a>Informazioni sulle proprietà di installazione del client in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare il comando CCMSetup.exe di System Center Configuration Manager per installare manualmente il client di Configuration Manager.  

##  <a name="aboutCCMSetup"></a> Informazioni su CCMSetup.exe  
 Il comando CCMSetup.exe consente di scaricare i file necessari per installare il client da un punto di gestione o da un percorso di origine. Questi file possono includere:  

-   Il pacchetto Client.msi di Windows Installer che consente di installare il software client.  

-   I file di installazione del Servizio trasferimento intelligente in background (BITS) di Microsoft.  

-   I file installazione di Windows Installer.  

-   Aggiornamenti e correzioni per il client di Configuration Manager.  

> [!NOTE]  
>  Non è possibile eseguire il file Client.msi direttamente in Configuration Manager.  

 CCMSetup.exe fornisce [proprietà della riga di comando](#ccmsetup-exe-command-line-properties) per la personalizzazione dell'installazione. È inoltre possibile specificare proprietà per la modifica del comportamento di Client.msi nella riga di comando CCMSetup.exe.  

> [!IMPORTANT]  
>  Prima di specificare le proprietà per Client.msi, specificare le proprietà di CCMSetup.  

 CCMSetup.exe e i relativi file di supporto si trovano nel server del sito di Configuration Manager nella cartella **Client** della cartella di installazione di Configuration Manager. La cartella è condivisa in rete in **&lt;nome server del sito\>\SMS_&lt;codice sito\>\Client**.  

 Al prompt dei comandi, il comando CCMSetup.exe usa il seguente formato:  

 `CCMSetup.exe [<Ccmsetup properties>] [<client.msi setup properties>]`  

 Esempio:  

 'CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

 Questo comando di esempio esegue le azioni seguenti:  

-   Specifica il punto di gestione denominato SMSMP01 per richiedere un elenco di punti di distribuzione per il download dei file di installazione del client.  

-   Specifica che è necessario interrompere l'installazione se nel computer esiste già una versione del client.  

-   Indica a client.msi di assegnare il client al codice del sito S01.  

-   Indica a client.msi di usare il punto di stato di fallback denominato SMSFP01.  

> [!NOTE]  
>  Se una proprietà contiene spazi, racchiuderla tra virgolette.  


> [!IMPORTANT]  
>  Se lo schema di Active Directory è stato esteso per Configuration Manager, molte proprietà di installazione client vengono pubblicate in Active Directory Domain Services e lette automaticamente dal client di Configuration Manager. Per un elenco delle proprietà di installazione client pubblicate in Servizi di dominio Active Directory, vedere [Informazioni sulle proprietà di installazione client pubblicate in Servizi di dominio Active Directory in System Center Configuration Manager](about-client-installation-properties-published-to-active-directory-domain-services.md).  

##  <a name="ccmsetupexe-command-line-properties"></a>Proprietà della riga di comando CCMSetup.exe  

### <a name=""></a>/?  

Apre la finestra di dialogo **CCMSetup** in cui vengono visualizzate le proprietà della riga di comando per ccmsetup.exe.  

Esempio: **ccmsetup.exe /?**  

### <a name="sourceltpath"></a>/source:&lt;percorso\>  

 Specifica il percorso da cui scaricare i file. È possibile usare un percorso locale o UNC. I file vengono scaricati usando il protocollo SMB (Server Message Block).  Per usare **/source**, l'account utente Windows usato per l'installazione client deve disporre delle autorizzazioni di lettura per il percorso.

> [!NOTE]  
>  È possibile usare più volte la proprietà **/source** in una riga di comando per specificare percorsi alternativi per il download.  

 Esempio: **ccmsetup.exe /source:"\\\computer\cartella"**  

### <a name="mpltcomputer"></a>/mp:&lt;computer\>

 Specifica un punto di gestione di origine per consentire ai computer di connettersi e individuare il punto di distribuzione più vicino per i file di installazione. Se non sono presenti punti di distribuzione oppure i computer non sono in grado di scaricare i file dai punti di distribuzione dopo 4 ore, i client scaricano i file dal punto di gestione specificato.  

> [!IMPORTANT]  
>  Questa proprietà viene usata per specificare un punto di gestione iniziale che consente ai computer di individuare un'origine per il download. Può trattarsi di un punto di gestione qualsiasi in un sito qualsiasi. Non implica l'*assegnazione* del client a un punto di gestione.   

 I computer scaricano i file tramite una connessione HTTP o HTTPS, a seconda della configurazione del ruolo del sistema del sito per le connessioni client. Il download usa la limitazione BITS, se configurata. Se tutti i punti di distribuzione e di gestione sono configurati solo per le connessioni client HTTPS, verificare che il computer client disponga di un certificato client valido.  

È possibile usare la proprietà della riga di comando **/mp** per specificare più punti di gestione e fare in modo che, se il computer non riesce a connettersi al primo, vengano eseguiti tentativi di connessione con gli altri punti di gestione. Quando si specificano più punti di gestione, è necessario separare i valori tramite punto e virgola.

Se il client si connette a un punto di gestione mediante HTTPS, in genere è necessario specificare l'FQDN anziché il nome computer. Il valore deve corrispondere al soggetto o al nome alternativo soggetto del certificato PKI del punto di gestione. Nonostante Configuration Manager supporti l'uso di un nome computer nel certificato per le connessioni sulla Intranet, per sicurezza è consigliabile inserire un FQDN.

Esempio di uso del nome computer: `ccmsetup.exe /mp:SMSMP01`  

Esempio di uso dell'FQDN: `ccmsetup.exe /mp:smsmp01.contoso.com`  

### <a name="retryltminutes"></a>/retry:&lt;minuti\>

L'intervallo tra i tentativi se CCMSetup.exe non riesce a scaricare i file di installazione.  CCMSetup continua a tentare fino a quando non raggiunge il limite specificato nella proprietà **downloadtimeout** .  

Esempio: `ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

Impedisce l'esecuzione di CCMSetup come servizio, ovvero l'impostazione predefinita. Quando CCMSetup viene eseguito come servizio, l'esecuzione avviene nell'ambito dell'account di sistema locale del computer, che potrebbe disporre di diritti insufficienti per l'accesso alle risorse di rete richieste per l'installazione. Con **/noservice**, CCMSetup.exe viene eseguito nel contesto dell'account utente usato per avviare l'installazione. Se inoltre si usa uno script per l'esecuzione di CCMSetup.exe con la proprietà **/service**, CCMSetup.exe viene chiuso dopo l'avvio del servizio e potrebbe non segnalare correttamente i dettagli di installazione.   

Esempio: `ccmsetup.exe /noservice`  

### <a name="service"></a>/service

Specifica che CCMSetup deve essere eseguito come un servizio che usa l'account di sistema locale.  

Esempio: `ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

Specifica che il software client deve essere disinstallato. Per altre informazioni, vedere [How to manage clients in System Center Configuration Manager](../manage/manage-clients.md).  

Esempio: `ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

Specifica che l'installazione del client deve essere interrotta se una versione del client è già installata.  

Esempio: `ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

 Specifica che, se necessario, CCMSetup deve forzare il riavvio del computer client per completare l'installazione. Se non è specificata, CCMSetup viene chiuso quando è necessario un riavvio e continua dopo il successivo riavvio manuale.  

 Esempio: `CCMSetup.exe /forcereboot`  

### <a name="bitspriorityltpriority"></a>/BITSPriority:&lt;priorità\>

 Specifica la priorità di download quando vengono scaricati i file di installazione client tramite una connessione HTTP. I possibili valori sono i seguenti:  

-   FOREGROUND  

-   HIGH  

-   NORMAL  

-   LOW  

 Il valore predefinito è NORMAL.  

 Esempio: `ccmsetup.exe /BITSPriority:HIGH`  

### <a name="downloadtimeoutltminutes"></a>/downloadtimeout:&lt;minuti\>

L'intervallo di tempo in minuti in cui CCMSetup tenta di scaricare i file di installazione prima di interrompersi. Il valore predefinito è **1440** minuti (1 giorno).  

Esempio: `ccmsetup.exe /downloadtimeout:100`  

### <a name="usepkicert"></a>/UsePKICert

 Quando viene specificato, il client usa un certificato PKI che include l'autenticazione del client, se disponibile. Se non viene trovato un certificato valido, il client usa una connessione HTTP e un certificato autofirmato, che è il comportamento adottato quando non si usa questa proprietà.

> [!NOTE]  
>  In alcuni scenari non è necessario specificare questa proprietà quando si installa un client e si usa comunque un certificato client. Tali scenari includono l'installazione di un client mediante installazione client basata sul punto di aggiornamento software e installazione push client. È tuttavia necessario specificare questa proprietà se si esegue l'installazione manuale di un client e si usa la proprietà **/mp** per specificare un punto di gestione configurato per accettare solo connessioni client HTTPS. È inoltre necessario specificare questa proprietà quando viene installato un client solo per la comunicazione Internet, usando la proprietà CCMALWAYSINF=1 (oltre alle proprietà per il punto di gestione basato su Internet e al codice del sito). Per altre informazioni sulla gestione client basata su Internet, vedere [Considerazioni per le comunicazioni client da Internet o da una foresta non trusted](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) in [Comunicazioni tra gli endpoint in System Center Configuration Manager](../../plan-design/hierarchy/communications-between-endpoints.md).  

 Esempio: `CCMSetup.exe /UsePKICert`  

### <a name="nocrlcheck"></a>/NoCRLCheck

 Specifica che un client non deve verificare l'elenco di revoche di certificati (CRL) in caso di comunicazione tramite HTTPS con un certificato PKI.  

 Quando non è specificata, il client controlla l'elenco di revoche di certificati prima di stabilire una connessione HTTPS.  

 Per altre informazioni sul controllo CRL client, vedere [Planning for PKI certificate revocation](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs) in[Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Esempio: `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="configltconfiguration-file"></a>/config:&lt;file di configurazione\>

Specificare il nome di un file di testo contenente le proprietà di installazione client.

- Se non si specifica la proprietà **/noservice** di CCMSetup, questo file deve trovarsi nella cartella CCMSetup, ovvero %Windir%\\Ccmsetup per sistemi operativi a 32 e a 64 bit.
- Se viene specificata la proprietà **/noservice** , questo file deve essere posizionato nella stessa cartella da cui è stato eseguito CCMSetup.exe.  

Esempio: `CCMSetup.exe /config:&lt;Configuration File Name.txt\>`  

Usare il file mobileclienttemplate.tcf nella cartella &lt;directory di Configuration Manager\>\\bin\\&lt;piattaforma\> del computer del server del sito per specificare il formato corretto del file. Questo file contiene inoltre commenti relativi alle sezioni e alle modalità di utilizzo. Specificare le proprietà di installazione cliente nella sezione [Client Install], dopo il testo seguente: **Install=INSTALL=ALL**.  

Voce della sezione [Client Install] di esempio: `Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereqltfilename"></a>/skipprereq:&lt;nome file\>

 Specifica che CCMSetup.exe non deve installare il programma definito come prerequisito se il client di Configuration Manager è installato. Questa proprietà supporta l'immissione di valori multipli. Usare il punto e virgola (;) per separare i valori.  


 Esempi: `CCMSetup.exe /skipprereq:silverlight.exe` o `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;Silverlight.exe`  

### <a name="forceinstall"></a>/forceinstall

 Specificare che tutti i client esistenti verranno disinstallati e sarà installato un nuovo client.  

### <a name="excludefeaturesltfeature"></a>/ExcludeFeatures:&lt;funzionalità\>

Specifica che CCMSetup.exe non installerà la funzionalità indicata se il client è installato.  

Esempio: `CCMSetup.exe /ExcludeFeatures:ClientUI` non installerà Software Center nel client.  

> [!NOTE]  
>  Per questa versione, **ClientUI** è l'unico valore supportato con la proprietà **/ExcludeFeatures** .  

##  <a name="ccmsetupReturnCodes"></a> Codici restituiti di CCMSetup.exe  
 Il comando CCMSetup.exe fornisce i seguenti codici restituiti quando viene completato. Per la risoluzione dei problemi, consultare il file ccmsetup.log nel computer client per il contesto e i dettagli aggiuntivi sui codici restituiti.  

|Codice restituito|Significato|  
|-----------------|-------------|  
|0|Operazione completata|  
|6|Errore|  
|7|Riavvio richiesto|  
|8|Installazione già in esecuzione|  
|9|Errore di valutazione dei prerequisiti|  
|10|Errore di convalida dell'hash manifesto di installazione|  

##  <a name="clientMsiProps"></a> Proprietà Client.msi  
 Le proprietà seguenti possono modificare il comportamento dell'installazione di client.msi. Se si utilizza il metodo di installazione push del client, è anche possibile specificare le proprietà nella scheda **Client** della finestra di dialogo **Proprietà installazione push client** .  

### <a name="ccmadmins"></a>CCMADMINS  

Specifica uno o più gruppi o account utente di Windows per ottenere l'accesso ai criteri e le impostazioni del client. Questa opzione è utile quando l'amministratore di Configuration Manager non dispone di credenziali amministrative locali nel computer client. Specificare un elenco di account separati da un punto e virgola.  

Esempio: `CCMSetup.exe CCMADMINS="Domain\Account1;Domain\Group1"`  

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

Specifica che il computer può eseguire il riavvio dopo l'installazione del client, se necessario.  

> [!IMPORTANT]  
>  Il computer verrà riavviato senza preavviso anche se un utente è connesso.  

Esempio: **CCMSetup.exe  CCMALLOWSILENTREBOOT**  

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

 Impostare su 1 per specificare che il client sarà sempre basato su Internet e non si connetterà mai a Intranet. Il tipo di connessione del client visualizza **Sempre Internet**.  

 Questa proprietà deve essere usata insieme a CCMHOSTNAME, che specifica l'FQDN del punto di gestione basato su Internet. Va inoltre usata insieme alla proprietà CCMSetup /UsePKICert e al codice del sito.  

 Per altre informazioni sulla gestione client basata su Internet, vedere [Considerazioni per le comunicazioni client da Internet o da una foresta non trusted](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan) in [Comunicazioni tra gli endpoint in System Center Configuration Manager](../../plan-design/hierarchy/communications-between-endpoints.md).  

 Esempio: `CCMSetup.exe /UsePKICert  CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`  

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

 Specifica l'elenco delle autorità di certificazione, ovvero un elenco di autorità di certificazione radice attendibili (CA) ritenuti attendibili dal sito di Configuration Manager.  

 Per altre informazioni sull'elenco delle autorità di certificazione e sulle relative modalità d'uso da parte dei client durante il processo di selezione dei certificati, vedere [Planning for PKI client certificate selection](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection) in [Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Si tratta di una corrispondenza con distinzione tra maiuscole e minuscole per gli attributi del soggetto presenti nel certificato CA radice. Gli attributi possono essere separati da virgola (,) o punto e virgola (;). È possibile specificare più certificati CA radice mediante una barra di separazione. Esempio:  

 `CCMCERTISSUERS=”CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US &#124; CN=Litware Corporate Root CA; O=Litware, Inc.”`  

> [!TIP]  
>  Fare riferimento al file mobileclient.tcf nella cartella &lt;directory di Configuration Manager\>\bin\\&lt;piattaforma\> del computer del server del sito per copiare il valore **CertificateIssuers=&lt;stringa\>** configurato per il sito.  

### <a name="ccmcertsel"></a>CCMCERTSEL

 Specifica i criteri di selezione del certificato se il client dispone di più di un certificato per la comunicazione HTTPS (un certificato valido che include la funzionalità di autenticazione client).  

 È possibile cercare una corrispondenza esatta (usare **Subject:**) o una corrispondenza parziale (usare **SubjectStr:)** in Nome soggetto o Nome alternativo soggetto. Esempi:  

 `CCMCERTSEL="Subject:computer1.contoso.com"` esegue la ricerca di un certificato con una corrispondenza esatta al nome computer "computer1.contoso.com" in Nome soggetto o in Nome alternativo soggetto.  

 `CCMCERTSEL="SubjectStr:contoso.com"` esegue la ricerca di un certificato che contiene "contoso.com" in Nome soggetto o in Nome alternativo soggetto.  

 È inoltre possibile usare l'identificatore di oggetto (OID) o gli attributi del nome distinto negli attributi Nome oggetto o Nome alternativo oggetto, ad esempio:  

 `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"` esegue la ricerca dell'attributo dell'unità organizzativa espresso come un identificatore di oggetto e denominato Computers.  

 `CCMCERTSEL="SubjectAttr:OU = Computers"` esegue la ricerca dell'attributo dell'unità organizzativa espresso come un nome distinto e denominato Computers.  

> [!IMPORTANT]  
>  Se si usa la casella Nome soggetto, **Subject:** distingue tra maiuscole e minuscole, mentre **SubjectStr:** non esegue la distinzione.  
>   
>  Se si usa la casella Nome alternativo soggetto, **Subject:** e **SubjectStr:** non distinguono tra maiuscole e minuscole.  

 L'elenco completo degli attributi che è possibile usare per la selezione dei certificati è disponibile in [Valori attributi supportati per i criteri di selezione del certificato PKI](#BKMK_attributevalues).  

 Se più di un certificato corrisponde alle ricerca e la proprietà CCMFIRSTCERT è stata impostata su 1, viene selezionato il certificato con il periodo di validità più lungo.  

### <a name="ccmcertstore"></a>CCMCERTSTORE

 Specifica un nome archivio certificati alternativo se il certificato client per HTTPS non si trova nell'archivio certificati predefinito di **Personale** nell'archivio del computer.  

 Esempio: `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

  Consente la registrazione debug. I valori possono essere impostati su 0 (disattivata, predefinita) o 1 (attivata). In questo modo il client registra le informazioni di basso livello per la risoluzione dei problemi. Come procedura consigliata, evitare l'utilizzo di questa proprietà nei siti di produzione perché potrebbe causare un numero eccessivo di registrazioni, che renderebbe difficile l'individuazione di informazioni rilevanti nei file di log. Anche CCMENABLELOGGING deve essere impostata su TRUE per consentire la registrazione debug.  

  Esempio: `CCMSetup.exe CCMDEBUGLOGGING=1`  

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

  Per impostazione predefinita, è impostata su TRUE per attivare la registrazione. I file di log vengono archiviati nella cartella **Logs** della cartella di installazione del client di Configuration Manager. Per impostazione predefinita, questa cartella è %Windir%\CCM\Logs.  

  Esempio: `CCMSetup.exe CCMENABLELOGGING=TRUE`  

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL  

 La frequenza con cui eseguire lo strumento di valutazione dell'integrità del client (ccmeval.exe). Può essere un valore compreso tra **1** e **1440** minuti. Per impostazione predefinita, la valutazione viene eseguita una volta al giorno.  

### <a name="ccmevalhour"></a>CCMEVALHOUR

 L'ora in cui eseguire lo strumento di valutazione dell'integrità del client (ccmeval.exe); può essere un valore compreso tra **0** (mezzanotte) e **23** (23.00). Per impostazione predefinita, la valutazione viene eseguita a mezzanotte.  

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

 Se impostata su 1, questa proprietà specifica che il client deve selezionare il certificato PKI con il periodo di validità più lunga. Questa impostazione potrebbe essere necessaria se si usa Protezione accesso alla rete con l'imposizione IPsec.  

 Esempio: `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`  

### <a name="ccmhostname"></a>CCMHOSTNAME

 Specifica l'FQDN del punto di gestione basato su Internet, se il client viene gestito in Internet.  

 Non specificare questa opzione con la proprietà di installazione SMSSITECODE=AUTO. I client basati su Internet devono essere assegnati direttamente ai relativi siti basati su Internet.  

 Esempio: `CCMSetup.exe  /UsePKICert/ CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

### <a name="ccmhttpport"></a>CCMHTTPPORT

 Specifica la porta che il client deve usare durante la comunicazione su HTTP con i server del sistema del sito. Per impostazione predefinita, è impostata la porta 80.  

 Esempio: `CCMSetup.exe CCMHTTPPORT=80`  

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

Specifica la porta che il client deve usare durante la comunicazione su HTTPS con i server del sistema del sito. Per impostazione predefinita, è impostata la porta 443.  

Esempio: `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`  

### <a name="ccminstalldir"></a>CCMINSTALLDIR

 Identifica la cartella in cui sono installati i file del client di Configuration Manager, per impostazione predefinita *%Windir%*\CCM. Indipendentemente dalla posizione in cui sono installati questi file, il file Ccmcore.dll viene sempre installato nella cartella *%Windir%\System32*. Inoltre, nei sistemi operativi a 64 bit viene sempre installata una copia del file Ccmcore.dll nella cartella *%Windir%*\SysWOW64 per il supporto di applicazioni a 32 bit che usano la versione a 32 bit delle API client di Configuration Manager dall'SDK (Software Developer Kit) di Configuration Manager.  

 Esempio: `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`  

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Specifica il livello di dettagli da scrivere nei file di log di Configuration Manager. Specificare un numero intero da 0 a 3, dove 0 è la registrazione più dettagliata e 3 registra solo gli errori. Il valore predefinito è 1.  

Esempio: `CCMSetup.exe CCMLOGLEVEL=3`  

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Quando un file di log di Configuration Manager raggiunge una dimensione di 250000 byte (o il valore specificato dalla proprietà CCMLOGMAXSIZE), viene rinominato come file di backup e un nuovo file di log viene creato.  

Questa proprietà specifica il numero di versioni precedenti del file di log da conservare. Il valore predefinito è 1. Se il valore è impostato su 0, non viene mantenuto alcun file di log precedente.  

Esempio: `CCMSetup.exe CCMLOGMAXHISTORY=0`  

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

La dimensione massima del file di log in byte. Quando un file di log raggiunge la dimensione specificata, viene rinominato come un file di cronologia e viene creato un nuovo file. Questa proprietà deve essere impostata almeno su 10000 byte. Il valore predefinito è 250000 byte.  

Esempio: `CCMSetup.exe CCMLOGMAXSIZE=300000`  

### <a name="disablesiteopt"></a>DISABLESITEOPT

 Se è impostata su TRUE, questa proprietà non consente agli utenti finali con credenziali amministrative nel computer client di modificare il sito assegnato al client di Configuration Manager in **Configuration Manager** nel Pannello di controllo del client.  

 Esempio: **CCMSetup.exe DISABLESITEOPT=TRUE**  

### <a name="disablecacheopt"></a>DISABLECACHEOPT

Se è impostata su TRUE, questa proprietà non consente agli utenti finali con credenziali amministrative nel computer client di modificare le impostazioni della cartella cache client per il client di  Configuration Manager tramite Configuration Manager nel Pannello di controllo del computer client.  

Esempio: `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

 Specifica un dominio DNS che i client usano per individuare i punti di gestione pubblicati in DNS. Una volta individuato un punto di gestione, tale punto fornisce informazioni al client in merito ad altri punti di gestione nella gerarchia. Ciò significa che il punto di gestione individuato usando la pubblicazione DNS non deve provenire dal sito del client, ma può essere un qualsiasi punto di gestione nella gerarchia.  

> [!NOTE]  
>  Non è necessario specificare questa proprietà se il client si trova nello stesso dominio del punto di gestione pubblicato. In questo caso il dominio del client viene usato automaticamente per la ricerca nel DNS dei punti di gestione.  

 Per altre informazioni sulla pubblicazione DNS come metodo di posizione del servizio per i client di Configuration Manager, vedere [Posizione del servizio e modo in cui i client determinano il relativo punto di gestione assegnato](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location) in [Informazioni su come i client trovano i servizi e le risorse del sito per System Center Configuration Manager](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

> [!NOTE]  
>  Per impostazione predefinita, la pubblicazione DNS non è abilitata in Configuration Manager.  

 Esempio: `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`  

### <a name="fsp"></a>FSP

Specifica il punto di stato di fallback che riceve ed elabora i messaggi di stato inviati dai computer client di Configuration Manager.  

Per altre informazioni sul punto di stato di fallback, vedere [Stabilire se è necessario un punto di stato di fallback](/sccm/core/clients/deploy/plan#determine-if-you-need-a-fallback-status-point).  

Esempio: `CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

 Specifica che la presenza della versione minima richiesta di Microsoft Application Virtualization (App-V) non viene verificata prima di installare il client.  

> [!IMPORTANT]  
>  Se si installa il client di Configuration Manager senza installare App-V, non è possibile distribuire applicazioni virtuali.  

 Esempio: `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`  

### <a name="notifyonly"></a>NOTIFYONLY

Specifica che lo stato del client segnalerà, ma non correggerà, i problemi rilevati con il client.  

Esempio: `CCMSetup.exe NOTIFYONLY=TRUE`  

Per ulteriori informazioni, vedere [How to configure client status in System Center Configuration Manager](configure-client-status.md).  

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

 Se un client di Configuration Manager ha la chiave radice attendibile di Configuration Manager errata e non può contattare un punto di gestione attendibile per ricevere la nuova chiave radice attendibile, è necessario rimuovere manualmente la vecchia chiave radice attendibile usando questa proprietà. Questa situazione può verificarsi quando si sposta un client da una gerarchia del sito a un'altra. Questa proprietà viene applicata ai client che usano la comunicazione client HTTP e HTTPS.  

 Esempio: `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

Consente la riassegnazione automatica del sito per gli aggiornamenti client se usata con [SMSSITECODE](#smssitecode)=AUTO.

Esempio: `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

Specifica il percorso della cartella cache client nel computer client in cui vengono archiviati i file temporanei. Per impostazione predefinita, il percorso è *%Windir \ccmcache*.  

Esempio: `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

Questa proprietà può essere usata insieme alla proprietà SMSCACHEFLAGS per controllare il percorso della cartella cache del client.  

Esempio: `CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE` consente di installare la cartella cache del client nell'unità disco del client più grande.  

### <a name="smscacheflags"></a>SMSCACHEFLAGS

Specifica ulteriori dettagli di installazione per la cartella cache client. È possibile usare le proprietà SMSCACHEFLAGS singolarmente o combinate, separate da punti e virgola. Se questa proprietà non viene specificata, la cartella cache client viene installata in base alla proprietà SMSCACHEDIR, la cartella non viene compressa e il valore di SMSCACHESIZE viene usato come dimensione in MB della cartella.  

Questa impostazione viene ignorata quando si aggiorna un client esistente.  

Proprietà:  

-   PERCENTDISKSPACE: specifica la dimensione della cartella come percentuale dello spazio totale su disco. Se si specifica questa proprietà, è necessario specificare anche la proprietà SMSCACHESIZE come valore di percentuale da usare.  

-   PERCENTFREEDISKSPACE: specifica la dimensione della cartella come percentuale dello spazio libero su disco. Se si specifica questa proprietà, è necessario specificare anche la proprietà SMSCACHESIZE come valore di percentuale da usare. Ad esempio, se nel disco sono disponibili 10 MB di spazio e SMSCACHESIZE viene specificata su 50, la dimensione della cartella è impostata su 5 MB. È impossibile usare questa proprietà con la proprietà PERCENTDISKSPACE.  

-   MAXDRIVE: specifica che la cartella deve essere installata nel disco più grande disponibile. Questo valore verrà ignorato se è stato specificato un percorso con la proprietà SMSCACHEDIR.  

-   MAXDRIVESPACE: specifica che la cartella deve essere installata nell'unità disco con più spazio libero. Questo valore verrà ignorato se è stato specificato un percorso con la proprietà SMSCACHEDIR.  

-   NTFSONLY: specifica che la cartella può essere installata solo in unità disco NTFS. Questo valore verrà ignorato se è stato specificato un percorso con la proprietà SMSCACHEDIR.  

-   COMPRESS: specifica che la cartella deve essere archiviata in formato compresso.  

-   FAILIFNOSPACE: specifica che il software client deve essere rimosso se non è disponibile spazio sufficiente per installare la cartella.  

Esempio: `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`  


### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> A partire da Configuration Manager versione 1606, sono disponibili nuove impostazioni client per specificare le dimensioni della cartella cache del client. Queste nuove impostazioni client sostituiscono in modo efficace l'uso di SMSCACHESIZE come proprietà di client.msi per specificare le dimensioni della cache del client. Per altre informazioni, vedere [le impostazioni client per le dimensioni della cache](about-client-settings.md#client-cache-settings).  

Per la versione 1602 e le versioni precedenti SMSCACHESIZE specifica le dimensioni della cartella della cache del client in megabyte (MB) o sotto forma di percentuale, se viene usata con la proprietà PERCENTDISKSPACE o PERCENTFREEDISKSPACE. Se questa proprietà non viene impostata, per impostazione predefinita la cartella presenta una dimensione massima di 5120 MB. Il valore più basso che è possibile specificare è 1 MB.  

> [!NOTE]  
>  Se a causa di un nuovo pacchetto che deve essere scaricato la cartella supera la dimensione massima e non può essere ripulita per creare spazio sufficiente, il download del pacchetto ha esito negativo e il programma o l'applicazione non vengono eseguiti.  

Questa impostazione viene ignorata quando si aggiorna un client esistente e quando il client scarica gli aggiornamenti software.  

Esempio: `CCMSetup.exe SMSCACHESIZE=100`  

> [!NOTE]  
>  Se si reinstalla un client, è impossibile usare le proprietà di installazione SMSCACHESIZE o SMSCACHEFLAGS per ridurre la dimensione della cache rispetto a prima. Se si tenta di eseguire questa operazione, il valore viene ignorato e la dimensione della cache viene impostata automaticamente sulla dimensione precedente.  

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

Specifica il percorso e l'ordine in cui il programma di installazione di Configuration Manager verifica le impostazioni di configurazione. La proprietà è una stringa contenente uno o più caratteri, ognuno dei quali definisce un'origine di configurazione specifica. Usare i valori dei caratteri R, P, M e U, singolarmente o combinati:  

-   R: cerca le impostazioni di configurazione nel Registro di sistema.  

   Per altre informazioni, vedere le [informazioni sull'archiviazione delle proprietà di installazione del client nel Registro di sistema](https://technet.microsoft.com/library/gg712298.aspx#BKMK_Provision).  

-   P: cerca le impostazioni di configurazione nelle proprietà di installazione fornite al prompt dei comandi.  

-   M: verifica le impostazioni esistenti durante l'aggiornamento di un client precedente con il software client di Configuration Manager.  

-   U: aggiorna il client installato a una versione più recente (e usa il codice sito assegnato).  

 Per impostazione predefinita, l'installazione client usa `PU` per cercare innanzitutto le proprietà di installazione e quindi le impostazioni esistenti.  

 Esempio: `CCMSetup.exe SMSCONFIGSOURCE=RP`  

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

 Specifica se il client può usare Windows Internet Name Service (WINS) per trovare un punto di gestione che accetti le connessioni HTTP. I client usano questo metodo quando non riescono a trovare un punto di gestione in Servizi di dominio Active Directory o in DNS.  

 Questa proprietà non influisce sull'uso di WINS da parte del client per la risoluzione dei nomi.  

 È possibile configurare due diverse modalità per questa proprietà:  

-   NOWINS: si tratta dell'impostazione più sicura per questa proprietà che impedisce ai client di trovare un punto di gestione in WINS.  Quando si usa questa impostazione, i client devono usare un metodo alternativo per individuare un punto di gestione in Intranet, come ad esempio Servizi di dominio Active Directory o tramite la pubblicazione DNS.  

-   WINSSECURE (predefinita): in questa modalità un client che usa la comunicazione HTTP può usare WINS per trovare un punto di gestione. Tuttavia, il client deve disporre di una copia della chiave radice attendibile prima di potersi connettere al punto di gestione. Per altre informazioni, vedere [Planning for the Trusted Root Key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) in [Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  


 Esempio: `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  

### <a name="smsmp"></a>SMSMP

Specifica un punto di gestione iniziale usato dal client di Configuration Manager.  

> [!IMPORTANT]  
>  Se il punto di gestione accetta solo connessioni client su HTTPS, è necessario aggiungere al nome del punto di gestione il prefisso https://.  

Esempio: `CCMSetup.exe SMSMP=smsmp01.contoso.com`

Esempio: `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  

### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

 Specifica la chiave radice attendibile di Configuration Manager quando non può essere recuperata da Servizi di dominio Active Directory. Questa proprietà viene applicata ai client che usano la comunicazione client HTTP e HTTPS. Per altre informazioni, vedere [Planning for the Trusted Root Key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) in [Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Esempio: `CCMSetup.exe SMSPUBLICROOTKEY=&lt;key\>`  

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

 Consente di reinstallare la chiave radice attendibile di Configuration Manager. Specifica il percorso completo e il nome file di un file che contiene la chiave radice attendibile. Questa proprietà viene applicata ai client che usano la comunicazione client HTTP e HTTPS. Per altre informazioni, vedere [Planning for the Trusted Root Key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK) in [Plan for security in System Center Configuration Manager](../../plan-design/security/plan-for-security.md).  

 Esempio: 'CCMSetup.exe SMSROOTKEYPATH=&lt;percorso e nome file completi\>`  

### <a name="smssigncert"></a>SMSSIGNCERT

 Specifica il percorso completo e il nome file con estensione cer del certificato autofirmato esportato nel server del sito.  

 Il certificato viene archiviato nell'archivio certificati **SMS** e dispone del Nome oggetto **Server del sito** e del nome descrittivo **Certificato di firma del server del sito**.  

 Esempio: **CCMSetup.exe /UsePKICert SMSSIGNCERT=&lt;percorso e nome file completi\>**  

### <a name="smssitecode"></a>SMSSITECODE

 Specifica il sito di Configuration Manager al quale assegnare il client di Configuration Manager. Può trattarsi di un codice del sito con tre caratteri o della parola AUTO. Se si specifica AUTO o se questa proprietà non viene specificata, il client prova a stabilire la relativa assegnazione sito di Configuration Manager da Active Directory Domain Services o da un punto di gestione specificato. Per abilitare la proprietà AUTO per gli aggiornamenti client, è necessario anche impostare [SITEREASSIGN](#sitereassign) su TRUE.    

> [!NOTE]  
>  Non usare AUTO se si specifica anche il punto di gestione basato su Internet (CCMHOSTNAME). In questo caso è necessario assegnare direttamente il client al relativo sito.  

 Esempio: `CCMSetup.exe SMSSITECODE=XZY`  

##  <a name="BKMK_attributevalues"></a> Valori attributi supportati per i criteri di selezione del certificato PKI  
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

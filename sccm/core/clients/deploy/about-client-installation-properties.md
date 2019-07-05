---
title: Proprietà e parametri di installazione client
titleSuffix: Configuration Manager
description: Informazioni sui parametri e le proprietà della riga di comando ccmsetup per l'installazione del client di Configuration Manager.
ms.date: 03/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: feef839af1f51c4cbb291f4ed5bc6336da6409b3
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/20/2019
ms.locfileid: "67286871"
---
# <a name="about-client-installation-parameters-and-properties-in-system-center-configuration-manager"></a>Informazioni sui parametri e le proprietà di installazione del client in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare il comando CCMSetup.exe per disinstallare il client di Configuration Manager. I parametri di installazione client specificati nella riga di comando consentono di modificare il comportamento dell'installazione, mentre le proprietà modificano la configurazione iniziale dell'agente client installato.



##  <a name="aboutCCMSetup"></a> Informazioni su CCMSetup.exe  
 Il comando CCMSetup.exe consente di scaricare i file necessari per installare il client da un punto di gestione o da un percorso di origine. Questi file possono includere:  

-   Il pacchetto client.msi di Windows Installer che consente di installare il software client.  

-   I file di installazione del Servizio trasferimento intelligente in background (BITS) di Microsoft.  

-   I file installazione di Windows Installer.  

-   Aggiornamenti e correzioni per il client di Configuration Manager.  

> [!NOTE]  
>  Non è possibile eseguire il file Client.msi direttamente in Configuration Manager.  

 CCMSetup.exe specifica i [parametri della riga di comando](#ccmsetupexe-command-line-parameters) per personalizzare l'installazione. I parametri sono preceduti da una barra rovesciata e per convenzione sono in lettere minuscole. È possibile specificare il valore di un parametro quando necessario, usando due punti seguiti dal valore desiderato. È anche possibile specificare proprietà per modificare il comportamento di client.msi nella riga di comando CCMSetup.exe. Le proprietà vengono specificate per convenzione in lettere maiuscole. Specificare un valore per una proprietà con un segno di uguale seguito immediatamente dal valore desiderato.  

> [!IMPORTANT]  
>  Specificare le proprietà di CCMSetup prima di specificare le proprietà per client.msi.  

 CCMSetup.exe e i relativi file di supporto si trovano nel server del sito, nella sottocartella **Client** della cartella di installazione di Configuration Manager. La cartella è condivisa in rete in **&lt;nome server del sito\>\SMS_&lt;codice sito\>\Client**.  

 Al prompt dei comandi, il comando CCMSetup.exe usa il seguente formato:  

 `CCMSetup.exe [<Ccmsetup parameters>] [<client.msi setup properties>]`  

 Ad esempio:  

   `CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

 Questo comando di esempio esegue le azioni seguenti:  

-   Specifica il punto di gestione denominato SMSMP01 per richiedere un elenco di punti di distribuzione per il download dei file di installazione del client.  

-   Specifica che è necessario interrompere l'installazione se nel computer esiste già una versione del client.  

-   Indica a client.msi di assegnare il client al codice del sito S01.  

-   Indica a client.msi di usare il punto di stato di fallback denominato SMSFP01.  

> [!NOTE]  
>  Se un valore di parametro include spazi, racchiuderlo tra virgolette.  


> [!IMPORTANT]  
>  Se lo schema di Active Directory è stato esteso per Configuration Manager, il sito pubblica molte proprietà di installazione client in Servizi di dominio Active Directory. Il client di Configuration Manager legge automaticamente queste proprietà. Per altre informazioni, vedere [Informazioni sulle proprietà di installazione client pubblicate in Servizi di dominio Active Directory](about-client-installation-properties-published-to-active-directory-domain-services.md).  



##  <a name="ccmsetupexe-command-line-parameters"></a>Parametri della riga di comando di CCMSetup.exe  

### <a name=""></a>/?  

Apre la finestra di dialogo **CCMSetup** in cui vengono visualizzati i parametri della riga di comando per ccmsetup.exe.  

Esempio: **ccmsetup.exe /?**  

### <a name="sourceltpath"></a>/source:&lt;percorso\>  

 Specifica il percorso da cui scaricare i file. È possibile usare un percorso locale o UNC. I file vengono scaricati usando il protocollo SMB (Server Message Block). Per usare **/source**, l'account utente Windows usato per l'installazione client deve disporre delle autorizzazioni di lettura per il percorso.

> [!NOTE]  
>  È possibile usare più volte il parametro **/source** in una riga di comando per specificare percorsi alternativi per il download.  

 Esempio: **ccmsetup.exe /source:"\\\computer\cartella"**  

### <a name="mpltserver"></a>/mp:&lt;Server\>

 Specifica un punto di gestione origine al quale possono connettersi i computer. I computer usano questo punto di gestione per trovare il punto di distribuzione più vicino per i file di installazione. Se non sono presenti punti di distribuzione o se i computer non riescono a scaricare i file dai punti di distribuzione dopo 4 ore, scaricano i file dal punto di gestione specificato.  

> [!IMPORTANT]  
>  Questo parametro viene usato per specificare un punto di gestione iniziale che consente ai computer di individuare un'origine per il download. Può trattarsi di un punto di gestione qualsiasi in un sito qualsiasi. Non implica l'*assegnazione* del client a un punto di gestione.   

 I computer scaricano i file tramite una connessione HTTP o HTTPS, a seconda della configurazione del ruolo del sistema del sito per le connessioni client. Il download usa la limitazione BITS, se configurata. Se tutti i punti di distribuzione e di gestione sono configurati solo per le connessioni client HTTPS, verificare che il computer client disponga di un certificato client valido.  

È possibile usare il parametro della riga di comando **/mp** per specificare più punti di gestione. Se il computer non riesce a connettersi al primo punto di gestione, prova a connettersi al successivo nell'elenco specificato. Quando si specificano più punti di gestione, è necessario separare i valori tramite punto e virgola.

Se il client si connette a un punto di gestione mediante HTTPS, in genere è necessario specificare l'FQDN anziché il nome computer. Il valore deve corrispondere al soggetto o al nome alternativo soggetto del certificato PKI del punto di gestione. Nonostante Configuration Manager supporti l'uso di un nome computer nel certificato per le connessioni sulla rete Intranet, è consigliabile usare un FQDN.

Esempio di uso del nome computer: `ccmsetup.exe /mp:SMSMP01`  

Esempio di uso dell'FQDN: `ccmsetup.exe /mp:smsmp01.contoso.com`  

Questo parametro può specificare l'URL di un gateway di gestione cloud. Usare questo URL per installare il client in un dispositivo basato su Internet. Per ottenere il valore di questo parametro, seguire questa procedura:
- Creare un gateway di gestione cloud.
- In un client attivo aprire un prompt dei comandi Windows PowerShell come amministratore. 
- Eseguire il comando seguente: `(Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
- Aggiungere il prefisso "https://" da usare con il parametro **/mp**.

Esempio per l'uso dell'URL del gateway di gestione cloud: `ccmsetup.exe /mp: https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

 > [!Important]
 > Quando si specifica l'URL di un gateway di gestione cloud per il parametro **/mp**, l'URL deve iniziare con **https://** .


### <a name="retryltminutes"></a>/retry:&lt;minuti\>

L'intervallo tra i tentativi se CCMSetup.exe non riesce a scaricare i file di installazione. CCMSetup continua a tentare fino a quando non raggiunge il limite specificato nel parametro **downloadtimeout**.  

Esempio: `ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

Impedisce l'esecuzione di CCMSetup come servizio, ovvero l'impostazione predefinita. Quando CCMSetup funziona come servizio, viene eseguito nel contesto dell'account di sistema locale del computer. Questo account potrebbe non avere diritti sufficienti per l'accesso alle risorse di rete necessarie per l'installazione. Con **/noservice**, CCMSetup.exe viene eseguito nel contesto dell'account utente usato per avviare l'installazione. Se si usa uno script per l'esecuzione di CCMSetup.exe con il parametro **/service**, inoltre, CCMSetup.exe viene chiuso dopo l'avvio del servizio e potrebbe non segnalare correttamente i dettagli di installazione.   

Esempio: `ccmsetup.exe /noservice`  

### <a name="service"></a>/service

Specifica che CCMSetup deve essere eseguito come un servizio che usa l'account di sistema locale.  

Esempio: `ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

Specifica che il software client deve essere disinstallato. Per altre informazioni, vedere [Come gestire i client](../manage/manage-clients.md).  

Esempio: `ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

Specifica che l'installazione del client deve essere interrotta se è già installata una versione del client.  

Esempio: `ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

 Specifica che, se necessario, CCMSetup deve forzare il riavvio del computer client per completare l'installazione. Se questo parametro non viene specificato, quando è necessario un riavvio CCMSetup interrompe l'esecuzione. L'esecuzione viene ripresa dopo il successivo riavvio manuale.  

 Esempio: `CCMSetup.exe /forcereboot`  

### <a name="bitspriorityltpriority"></a>/BITSPriority:&lt;priorità\>

 Specifica la priorità di download quando vengono scaricati i file di installazione client tramite una connessione HTTP. I possibili valori sono i seguenti:  

- FOREGROUND  

- HIGH  

- NORMAL  

- LOW  

  Il valore predefinito è NORMAL.  

  Esempio: `ccmsetup.exe /BITSPriority:HIGH`  

### <a name="downloadtimeoutltminutes"></a>/downloadtimeout:&lt;minuti\>

Intervallo di tempo in minuti per il quale CCMSetup prova a scaricare i file di installazione prima di interrompere l'esecuzione. Il valore predefinito è **1440** minuti (un giorno).  

Esempio: `ccmsetup.exe /downloadtimeout:100`  

### <a name="usepkicert"></a>/UsePKICert

Quando viene specificato, il client usa un certificato PKI che include l'autenticazione del client, se disponibile. Se non trova un certificato valido, il client usa una connessione HTTP con un certificato autofirmato. Il comportamento è lo stesso quando non si usa questo parametro.

> [!NOTE]  
>  In alcuni scenari non è necessario specificare questo parametro quando si installa un client e si usa comunque un certificato client. Tali scenari includono l'installazione di un client mediante installazione client basata sul punto di aggiornamento software e installazione push client. È tuttavia necessario specificare questo parametro se si esegue l'installazione manuale di un client e si usa il parametro **/mp** per specificare un punto di gestione configurato per accettare solo connessioni client HTTPS. È necessario specificare questo parametro anche quando si installa un client per le comunicazioni solo con Internet. Usare la proprietà CCMALWAYSINF=1 insieme alle proprietà per il punto di gestione basato su Internet (CCMHOSTNAME) e il codice del sito (SMSSITECODE). Per altre informazioni sulla gestione client in Internet, vedere [Considerazioni per le comunicazioni client da Internet o da una foresta non trusted](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

 Esempio: `CCMSetup.exe /UsePKICert`  

### <a name="nocrlcheck"></a>/NoCRLCheck

 Specifica che un client non deve verificare l'elenco di revoche di certificati (CRL) in caso di comunicazione tramite HTTPS con un certificato PKI.  

 Quando non è specificata, il client controlla l'elenco di revoche di certificati prima di stabilire una connessione HTTPS.  

 Per altre informazioni sul controllo dell'elenco di revoche di certificati (CRL) da parte del client, vedere [Pianificazione di revoche di certificati PKI](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).  

 Esempio: `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="configltconfiguration-file"></a>/config:&lt;file di configurazione\>

Specificare il nome di un file di testo che elenca le proprietà di installazione client.

- Se non si specifica il parametro **/noservice** di CCMSetup, questo file deve trovarsi nella cartella CCMSetup, ovvero %Windir%\\Ccmsetup per i sistemi operativi a 32 e a 64 bit.
- Se si specifica il parametro **/noservice**, questo file deve essere posizionato nella stessa cartella da cui si esegue CCMSetup.exe.  

Esempio: `CCMSetup.exe /config:&lt;Configuration File Name.txt\>`  

Per specificare il formato corretto del file, usare il file mobileclienttemplate.tcf nella cartella &lt;directory di Configuration Manager\>\\bin\\&lt;piattaforma\> del server del sito. Questo file contiene anche commenti relativi alle sezioni e alle modalità d'uso. Specificare le proprietà di installazione client nella sezione [Client Install] dopo il testo seguente: **Install=INSTALL=ALL**.  

Voce della sezione [Client Install] di esempio: `Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereqltfilename"></a>/skipprereq:&lt;nome file\>

 Specifica che CCMSetup.exe non deve installare il programma definito come prerequisito durante l'installazione del client di Configuration Manager. Questo parametro supporta l'immissione di più valori. Usare il punto e virgola (;) per separare i valori.  


 Esempi: `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe` o `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;windowsupdateagent30_x86.exe`  

### <a name="forceinstall"></a>/forceinstall

 Specifica che CCMSetup.exe disinstalla tutti i client esistenti e installa un nuovo client.  

### <a name="excludefeaturesltfeature"></a>/ExcludeFeatures:&lt;funzionalità\>

Specifica che durante l'installazione del client CCMSetup.exe non installa la funzionalità specificata.  

Esempio: `CCMSetup.exe /ExcludeFeatures:ClientUI` non installa Software Center nel client.  

> [!NOTE]  
>  **ClientUI** è l'unico valore supportato con il parametro **/ExcludeFeatures**.  



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



## <a name="ccmsetupMsiProps"></a> Proprietà di Ccmsetup.msi  
 Le proprietà seguenti possono modificare il comportamento dell'installazione di ccmsetup.msi.

### <a name="ccmsetupcmd"></a>CCMSETUPCMD 

Specifica i parametri e le proprietà della riga di comando che vengono passati a ccmsetup.exe dopo l'installazione tramite ccmsetup.msi. Racchiudere altre proprietà tra virgolette. Usare questa proprietà quando si esegue il bootstrap del client di Configuration Manager tramite il metodo di installazione della gestione dei dispositivi mobili ibrida di Intune. 

Esempio: `ccmsetup.msi CCMSETUPCMD="/mp: https://mp.contoso.com CCMHOSTNAME=mp.contoso.com"`

 > [!Tip]
 > Microsoft Intune limita la riga di comando a 1024 caratteri. 



##  <a name="clientMsiProps"></a> Proprietà di Client.msi  
 Le proprietà seguenti possono modificare il comportamento dell'installazione di client.msi. Se si utilizza il metodo di installazione push del client, è anche possibile specificare le proprietà nella scheda **Client** della finestra di dialogo **Proprietà installazione push client** .  


### <a name="aadclientappid"></a>AADCLIENTAPPID

Specifica l'identificatore dell'app client Azure Active Directory (Azure AD). L'app client viene creata o importata quando si [configurano i servizi Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) per la gestione cloud. Gli amministratori di Azure possono ottenere il valore di questa proprietà dal portale di Azure. Per altre informazioni, vedere [Ottenere l'ID applicazione e la chiave di autenticazione](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in). Per la proprietà **AADCLIENTAPPID** l'ID applicazione è relativo al tipo di applicazione "Nativo".

Esempio: `ccmsetup.exe AADCLIENTAPPID=aa28e7f1-b88a-43cd-a2e3-f88b257c863b`


### <a name="aadresourceuri"></a>AADRESOURCEURI

Specifica l'identificatore dell'app server Azure AD. L'app server viene creata o importata quando si [configurano i servizi Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) per la gestione cloud. Quando si crea l'app server, nella finestra di dialogo Crea un'applicazione server questa proprietà è l'**URI ID App**.

Gli amministratori di Azure possono ottenere il valore di questa proprietà dal portale di Azure. Nel pannello **Azure Active Directory** trovare l'app server in **Registrazioni per l'app**. Questa applicazione è di tipo "App Web/API". Aprire l'app, fare clic su **Impostazioni** e quindi su **Proprietà**. Usare il valore **URI ID App** per questa proprietà dell'installazione client AADRESOURCEURI.

Esempio: `ccmsetup.exe AADRESOURCEURI=https://contososerver`


### <a name="aadtenantid"></a>AADTENANTID

Specifica l'identificatore de tenant di Azure AD. Questo tenant viene collegato a Configuration Manager quando si [configurano i servizi Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) per la gestione cloud. Per ottenere il valore di questa proprietà procedere come segue:
- In un dispositivo Windows 10 unito allo stesso tenant di Azure AD aprire un prompt dei comandi.
- Eseguire il comando seguente: `dsregcmd.exe /status`
- Nella sezione Stato dispositivo trovare il valore **TenantId**. Ad esempio: `TenantId : 607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

  > [!Note]
  > Gli amministratori di Azure possono anche ottenere questo valore nel portale di Azure. Per altre informazioni, vedere [Ottenere l'ID tenant](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).

Esempio: `ccmsetup.exe AADTENANTID=607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

<!-- 
### AADTENANTNAME

Specifies the Azure AD tenant name. This tenant is linked to Configuration Manager when you [configure Azure services](/sccm/core/servers/deploy/configure/azure-services-wizard) for Cloud Management. To obtain the value for this property, use the following steps:
- On a Windows 10 device that is joined to the same Azure AD tenant, open a command prompt.
- Run the following command: `dsregcmd.exe /status`
- In the Device State section, find the **TenantName** value. For example, `TenantName : Contoso`

Example: `ccmsetup.exe AADTENANTNAME=Contoso`
-->

### <a name="ccmadmins"></a>CCMADMINS  

Specifica uno o più gruppi o account utente di Windows per ottenere l'accesso ai criteri e le impostazioni del client. Questa proprietà è utile quando l'amministratore di Configuration Manager non dispone di credenziali amministrative locali nel computer client. Specificare un elenco di account separati da un punto e virgola.  

Esempio: `CCMSetup.exe CCMADMINS="Domain\Account1;Domain\Group1"`  

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

Specifica che in caso di necessità il computer può eseguire il riavvio dopo l'installazione del client.  

> [!IMPORTANT]  
>  Il computer viene riavviato senza preavviso anche se un utente è connesso.  

Esempio: **CCMSetup.exe  CCMALLOWSILENTREBOOT**  

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

 Impostare il valore **1** per specificare che il client è sempre basato su Internet e non si connette mai all'intranet. Il tipo di connessione del client visualizza **Sempre Internet**.  

 Usare questa proprietà con CCMHOSTNAME, che specifica l'FQDN del punto di gestione basato su Internet. Usarla anche con il parametro CCMSetup /UsePKICert e con il codice del sito.  

 Per altre informazioni sulla gestione client in Internet, vedere [Considerazioni per le comunicazioni client da Internet o da una foresta non trusted](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

 Esempio: `CCMSetup.exe /UsePKICert  CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`  

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

 Specifica l'elenco delle autorità di certificazione, ovvero un elenco di autorità di certificazione radice attendibili (CA) ritenuti attendibili dal sito di Configuration Manager.  

 Per altre informazioni sull'elenco delle autorità di certificazione e sulle relative modalità d'uso da parte dei client durante il processo di selezione dei certificati, vedere [Pianificazione della selezione del certificato client PKI](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection).  

 Il valore è una corrispondenza con distinzione maiuscole/minuscole per gli attributi del soggetto presenti nel certificato CA radice. Gli attributi possono essere separati da virgola (,) o punto e virgola (;). È possibile specificare più certificati CA radice mediante una barra di separazione. Esempio:  

 `CCMCERTISSUERS="CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US | CN=Litware Corporate Root CA; O=Litware, Inc."`  

> [!TIP]  
>  Per copiare **CertificateIssuers=&lt;stringa\>** per il sito, fare riferimento al file mobileclient.tcf file nella cartella &lt;directory di Configuration Manager\>\bin\\&lt;piattaforma\> nel server del sito.  

### <a name="ccmcertsel"></a>CCMCERTSEL

 Specifica i criteri di selezione del certificato se il client dispone di più di un certificato per la comunicazione HTTPS. Questo certificato è un certificato valido che include la capacità di autenticazione client.  

 È possibile cercare una corrispondenza esatta (usare **Subject:** ) o una corrispondenza parziale (usare **SubjectStr:)** in Nome soggetto o Nome alternativo soggetto. Esempi:  

 `CCMCERTSEL="Subject:computer1.contoso.com"` esegue la ricerca di un certificato con una corrispondenza esatta al nome computer "computer1.contoso.com" in Nome soggetto o in Nome alternativo soggetto.  

 `CCMCERTSEL="SubjectStr:contoso.com"` esegue la ricerca di un certificato che contiene "contoso.com" in Nome soggetto o in Nome alternativo soggetto.  

 È inoltre possibile usare l'identificatore di oggetto (OID) o gli attributi del nome distinto negli attributi Nome oggetto o Nome alternativo oggetto, ad esempio:  

 `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"` esegue la ricerca dell'attributo dell'unità organizzativa espresso come un identificatore di oggetto e denominato Computers.  

 `CCMCERTSEL="SubjectAttr:OU = Computers"` esegue la ricerca dell'attributo dell'unità organizzativa espresso come un nome distinto e denominato Computers.  

> [!IMPORTANT]
>  Se si usa la casella Nome soggetto, **Subject:** distingue tra maiuscole e minuscole, mentre **SubjectStr:** non esegue la distinzione.  
> 
>  Se si usa la casella Nome alternativo soggetto, <strong>Subject:</strong> e **SubjectStr:** non distinguono tra maiuscole e minuscole.  

 L'elenco completo degli attributi che è possibile usare per la selezione dei certificati è disponibile in [Valori attributi supportati per i criteri di selezione del certificato PKI](#BKMK_attributevalues).  

 Se più di un certificato corrisponde alle ricerca e la proprietà CCMFIRSTCERT è stata impostata su 1, viene selezionato il certificato con il periodo di validità più lungo.  

### <a name="ccmcertstore"></a>CCMCERTSTORE

 Specifica il nome di un archivio certificati alternativo se il certificato client per HTTPS non si trova nell'archivio certificati predefinito di **Personale** nell'archivio del computer.  

 Esempio: `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

  Consente la registrazione debug. I valori possono essere impostati su 0 (disattivata, predefinita) o 1 (attivata). Questa proprietà fa in modo che il client registri le informazioni di basso livello per la risoluzione dei problemi. È consigliabile evitare l'uso di questa proprietà nei siti di produzione. La proprietà può dare origine a un volume eccessivo di registrazioni e quindi rendere difficile l'individuazione delle informazioni desiderate nei file di log. Impostare anche CCMENABLELOGGING su TRUE per consentire la registrazione debug.  

  Esempio: `CCMSetup.exe CCMDEBUGLOGGING=1`  

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

  Per impostazione predefinita questa proprietà è TRUE e attiva la registrazione. I file di log vengono archiviati nella cartella **Logs** della cartella di installazione del client di Configuration Manager. Per impostazione predefinita, questa cartella è %Windir%\CCM\Logs.  

  Esempio: `CCMSetup.exe CCMENABLELOGGING=TRUE`  

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL  

 La frequenza con cui eseguire lo strumento di valutazione dell'integrità del client (ccmeval.exe). Può essere un valore compreso tra **1** e **1440** minuti. Per impostazione predefinita, la valutazione viene eseguita una volta al giorno.  

### <a name="ccmevalhour"></a>CCMEVALHOUR

 L'ora in cui eseguire lo strumento di valutazione dell'integrità del client (ccmeval.exe); può essere un valore compreso tra **0** (mezzanotte) e **23** (23.00). Per impostazione predefinita, la valutazione viene eseguita a mezzanotte.  

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

 Se impostata su 1, questa proprietà specifica che il client deve selezionare il certificato PKI con il periodo di validità più lunga. Questa impostazione può essere necessaria se si usa Protezione accesso alla rete con l'imposizione IPsec.  

 Esempio: `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`  


### <a name="ccmhostname"></a>CCMHOSTNAME

 Se il client viene gestito in Internet, specifica l'FQDN del punto di gestione basato su Internet.  

 Non specificare questa opzione con la proprietà di installazione SMSSITECODE=AUTO. I client basati su Internet devono essere assegnati direttamente ai siti basati su Internet corrispondenti.  

 Esempio: `CCMSetup.exe  /UsePKICert CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

Questa proprietà può specificare l'indirizzo di un gateway di gestione cloud. Per ottenere il valore di questa proprietà procedere come segue:
- Creare un gateway di gestione cloud.
- In un client attivo aprire un prompt dei comandi Windows PowerShell come amministratore. 
- Eseguire il comando seguente: `(Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
- Con la proprietà **CCMHOSTNAME** usare il valore restituito senza modificarlo.

Ad esempio: `ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

 > [!Important]
 > Quando si specifica l'indirizzo di un gateway di gestione cloud per la proprietà **CCMHOSTNAME**, *non* aggiungere un prefisso come **https://** . Questo prefisso viene usato solo con l'URL **/mp** di un gateway di gestione cloud.



### <a name="ccmhttpport"></a>CCMHTTPPORT

 Specifica la porta che il client deve usare durante la comunicazione su HTTP con i server del sistema del sito. Per impostazione predefinita, è impostata la porta 80.  

 Esempio: `CCMSetup.exe CCMHTTPPORT=80`  

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

Specifica la porta che il client deve usare durante la comunicazione su HTTPS con i server del sistema del sito. Per impostazione predefinita, è impostata la porta 443.  

Esempio: `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`  

### <a name="ccminstalldir"></a>CCMINSTALLDIR

 Identifica la cartella in cui sono installati i file del client di Configuration Manager, per impostazione predefinita *%Windir%* \CCM. Indipendentemente dalla posizione in cui sono installati questi file, il file Ccmcore.dll viene sempre installato nella cartella *%Windir%\System32*. In un sistema operativo a 64 bit una copia del file Ccmcore.dll viene sempre installata nella cartella *%Windir%* \SysWOW64. Questo file supporta le applicazioni a 32 bit che usano la versione a 32 bit delle API client di Configuration Manager SDK.  

 Esempio: `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`  

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Specifica il livello di dettagli da scrivere nei file di log di Configuration Manager. Specificare un numero intero da 0 a 3, dove 0 è la registrazione più dettagliata e 3 registra solo gli errori. Il valore predefinito è 1.  

Esempio: `CCMSetup.exe CCMLOGLEVEL=3`  

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Quando un file di log di Configuration Manager raggiunge la dimensione massima, il client lo rinomina come file di backup e crea un nuovo file di log. La dimensione massima predefinita è pari a 250.000 byte o al valore specificato dalla proprietà CCMLOGMAXSIZE.

Questa proprietà specifica il numero di versioni precedenti del file di log da mantenere. Il valore predefinito è 1. Se il valore è impostato su 0, non viene mantenuto alcun file di log precedente.  

Esempio: `CCMSetup.exe CCMLOGMAXHISTORY=0`  

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

La dimensione massima del file di log in byte. Quando un log raggiunge la dimensione specificata, il client lo rinomina come file di cronologia e crea un nuovo file. Questa proprietà deve essere impostata su un valore non inferiore a 10.000 byte. Il valore predefinito è 250.000 byte.  

Esempio: `CCMSetup.exe CCMLOGMAXSIZE=300000`  

### <a name="disablesiteopt"></a>DISABLESITEOPT

 Se impostata su TRUE, questa proprietà non consente agli utenti amministratori di modificare il sito assegnato nel pannello di controllo **Configuration Manager**.  

 Esempio: **CCMSetup.exe DISABLESITEOPT=TRUE**  

### <a name="disablecacheopt"></a>DISABLECACHEOPT

Se impostata su TRUE, questa proprietà non consente agli utenti amministratori di modificare le impostazioni della cartella cache client nel pannello di controllo **Configuration Manager**.  

Esempio: `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

 Specifica un dominio DNS che i client usano per individuare i punti di gestione pubblicati in DNS. Una volta individuato un punto di gestione, tale punto fornisce informazioni al client in merito ad altri punti di gestione nella gerarchia. Questo comportamento significa che il punto di gestione individuato usando la pubblicazione DNS non deve necessariamente provenire dal sito del client, ma può essere un qualsiasi punto di gestione nella gerarchia.  

> [!NOTE]  
>  Non è necessario specificare questa proprietà se il client si trova nello stesso dominio del punto di gestione pubblicato. In questo caso il dominio del client viene usato automaticamente per la ricerca nel DNS dei punti di gestione.  

 Per altre informazioni sulla pubblicazione DNS come metodo di posizione del servizio per i client Configuration Manager, vedere [Posizione del servizio e modo in cui i client determinano il relativo punto di gestione assegnato](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location).  

> [!NOTE]  
>  Per impostazione predefinita la pubblicazione DNS non è abilitata in Configuration Manager.  

 Esempio: `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`  

### <a name="fsp"></a>FSP

Specifica il punto di stato di fallback che riceve ed elabora i messaggi di stato inviati dai computer client di Configuration Manager.  

Per altre informazioni sul punto di stato di fallback, vedere [Stabilire se è necessario un punto di stato di fallback](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients#determine-if-you-need-a-fallback-status-point).  

Esempio: `CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

 Specifica che la presenza della versione minima richiesta di Microsoft Application Virtualization (App-V) non viene verificata prima dell'installazione del client.  

> [!IMPORTANT]  
>  Se si installa il client di Configuration Manager senza installare App-V non è possibile distribuire applicazioni virtuali.  

 Esempio: `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`  

### <a name="notifyonly"></a>NOTIFYONLY

Specifica che il client segnala lo stato, ma non risolve i problemi rilevati.  

Esempio: `CCMSetup.exe NOTIFYONLY=TRUE`  

Per altre informazioni, vedere [Come configurare lo stato del client](configure-client-status.md).  

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

 Se un client dispone di una chiave radice attendibile di Configuration Manager errata e non può contattare un punto di gestione attendibile per ricevere la nuova chiave radice attendibile, usare questa proprietà per rimuovere manualmente la vecchia chiave radice attendibile. Questa situazione può verificarsi quando si sposta un client da una gerarchia del sito a un'altra. Questa proprietà viene applicata ai client che usano la comunicazione client HTTP e HTTPS.  

 Esempio: `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

Consente la riassegnazione automatica del sito per gli aggiornamenti client se usata con [SMSSITECODE](#smssitecode)=AUTO.

Esempio: `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

Specifica il percorso della cartella cache client nel computer client in cui vengono archiviati i file temporanei. Per impostazione predefinita, il percorso è *%Windir%\ccmcache*.  

Esempio: `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

Questa proprietà può essere usata insieme alla proprietà SMSCACHEFLAGS per controllare il percorso della cartella cache del client.  

Esempio: `CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE` consente di installare la cartella cache del client nell'unità disco del client più grande.  

### <a name="smscacheflags"></a>SMSCACHEFLAGS

Specifica ulteriori dettagli di installazione per la cartella cache client. È possibile usare le proprietà SMSCACHEFLAGS singolarmente o combinate, separate da punti e virgola. Se questa proprietà non viene specificata, la cartella cache client viene installata in base alla proprietà SMSCACHEDIR e non viene compressa. Il valore di SMSCACHESIZE viene usato come dimensione in MB della cartella.  

Questa impostazione viene ignorata quando si aggiorna un client esistente.  

Proprietà:  

-   PERCENTDISKSPACE: specifica le dimensioni della cartella come percentuale dello spazio su disco totale. Se si specifica questa proprietà, è necessario specificare anche la proprietà SMSCACHESIZE come valore di percentuale da usare.  

-   PERCENTFREEDISKSPACE: specifica le dimensioni della cartella come percentuale dello spazio su disco disponibile. Se si specifica questa proprietà, è necessario specificare anche la proprietà SMSCACHESIZE come valore di percentuale da usare. Ad esempio, se nel disco sono disponibili 10 MB di spazio e SMSCACHESIZE viene specificata su 50, la dimensione della cartella è impostata su 5 MB. È impossibile usare questa proprietà con la proprietà PERCENTDISKSPACE.  

-   MAXDRIVE: specifica che la cartella deve essere installata nel disco più grande disponibile. Questo valore viene ignorato se è stato specificato un percorso con la proprietà SMSCACHEDIR.  

-   MAXDRIVESPACE: specifica che la cartella deve essere installata nell'unità disco con più spazio libero. Questo valore viene ignorato se è stato specificato un percorso con la proprietà SMSCACHEDIR.  

-   NTFSONLY: specifica che la cartella può essere installata solo in unità disco NTFS. Questo valore viene ignorato se è stato specificato un percorso con la proprietà SMSCACHEDIR.  

-   COMPRESS: specifica che la cartella deve essere archiviata in formato compresso.  

-   FAILIFNOSPACE: specifica che il software client deve essere rimosso se non è disponibile spazio sufficiente per installare la cartella.  

Esempio: `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`  


### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> Sono disponibili impostazioni client per specificare le dimensioni della cartella cache del client. Queste nuove impostazioni client sostituiscono in modo efficace l'uso di SMSCACHESIZE come proprietà di client.msi per specificare le dimensioni della cache del client. Per altre informazioni, vedere [le impostazioni client per le dimensioni della cache](about-client-settings.md#client-cache-settings).  

<!-- For 1602 and earlier, SMSCACHESIZE specifies the size of the client cache folder in megabyte (MB) or as a percentage when used with the PERCENTDISKSPACE or PERCENTFREEDISKSPACE property. If this property isn't set, the folder defaults to a maximum size of 5120 MB. The lowest value that you can specify is 1 MB.  -->

> [!NOTE]  
>  Se per il download di un nuovo pacchetto la cartella supera la dimensione massima e non può essere ripulita per creare spazio sufficiente, il download del pacchetto ha esito negativo e il programma o l'applicazione non vengono eseguiti.  

Questa impostazione viene ignorata quando si aggiorna un client esistente e quando il client scarica gli aggiornamenti software.  

Esempio: `CCMSetup.exe SMSCACHESIZE=100`  

> [!NOTE]  
>  Se si reinstalla un client, non è possibile usare le proprietà di installazione SMSCACHESIZE o SMSCACHEFLAGS per ridurre la cache a una dimensione inferiore a quella precedente. Se si prova a eseguire questa operazione il valore viene ignorato. La dimensione della cache viene impostata automaticamente sulla dimensione precedente.  

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

Specifica il percorso e l'ordine in cui il programma di installazione di Configuration Manager verifica le impostazioni di configurazione. La proprietà è una stringa composta da uno o più caratteri, ognuno dei quali definisce un'origine di configurazione specifica. Usare i valori dei caratteri R, P, M e U, singolarmente o combinati:  

- R: verifica le impostazioni di configurazione nel Registro di sistema.  

  Per altre informazioni, vedere le [informazioni sull'archiviazione delle proprietà di installazione del client nel Registro di sistema](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Provision).  

- P: verifica le impostazioni di configurazione nelle proprietà di installazione fornite al prompt dei comandi.  

- M: verifica le impostazioni esistenti durante l'aggiornamento di un client precedente con il software client di Configuration Manager.  

- U: aggiorna il client installato a una versione più recente (e usa il codice del sito assegnato).  

  Per impostazione predefinita, l'installazione client usa `PU` per cercare innanzitutto le proprietà di installazione e quindi le impostazioni esistenti.  

  Esempio: `CCMSetup.exe SMSCONFIGSOURCE=RP`  

### <a name="smsdirectorylookup"></a>SMSDIRECTORYLOOKUP

 Specifica se il client può usare Windows Internet Name Service (WINS) per trovare un punto di gestione che accetti le connessioni HTTP. I client usano questo metodo quando non riescono a trovare un punto di gestione in Servizi di dominio Active Directory o in DNS.  

 Questa proprietà non influisce sull'uso di WINS da parte del client per la risoluzione dei nomi.  

 È possibile configurare due diverse modalità per questa proprietà:  

-   NOWINS: questo valore è l'impostazione più sicura per la proprietà e impedisce ai client di trovare un punto di gestione in WINS. Quando si usa questa impostazione, i client devono usare un metodo alternativo per individuare un punto di gestione in Intranet, come ad esempio Servizi di dominio Active Directory o tramite la pubblicazione DNS.  

-   WINSSECURE (predefinita): in questa modalità, un client che usa la comunicazione HTTP può usare WINS per trovare un punto di gestione. Tuttavia, il client deve disporre di una copia della chiave radice attendibile prima di potersi connettere al punto di gestione. Per altre informazioni, vedere [Pianificare la chiave radice attendibile](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  


 Esempio: `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  

### <a name="smsmp"></a>SMSMP

Specifica un punto di gestione iniziale usato dal client di Configuration Manager.  

> [!IMPORTANT]  
>  Se il punto di gestione accetta solo connessioni client su HTTPS, è necessario aggiungere al nome del punto di gestione il prefisso https://.  

Esempio: `CCMSetup.exe SMSMP=smsmp01.contoso.com`

Esempio: `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  


### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

 Specifica la chiave radice attendibile di Configuration Manager quando non può essere recuperata da Servizi di dominio Active Directory. Questa proprietà viene applicata ai client che usano la comunicazione client HTTP e HTTPS. Per altre informazioni, vedere [Pianificare la chiave radice attendibile](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

 Esempio: `CCMSetup.exe SMSPUBLICROOTKEY=&lt;key\>`  

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

 Consente di reinstallare la chiave radice attendibile di Configuration Manager. Specifica il percorso completo e il nome file di un file che contiene la chiave radice attendibile. Questa proprietà viene applicata ai client che usano la comunicazione client HTTP e HTTPS. Per altre informazioni, vedere [Pianificare la chiave radice attendibile](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

 Esempio: 'CCMSetup.exe SMSROOTKEYPATH=&lt;percorso e nome file completi\>`  

### <a name="smssigncert"></a>SMSSIGNCERT

 Specifica il percorso completo e il nome file con estensione cer del certificato autofirmato esportato nel server del sito.  

 Il certificato viene archiviato nell'archivio certificati **SMS** e dispone del Nome oggetto **Server del sito** e del nome descrittivo **Certificato di firma del server del sito**.  

 Esempio: **CCMSetup.exe /UsePKICert SMSSIGNCERT=&lt;percorso e nome file completi\>**  

### <a name="smssitecode"></a>SMSSITECODE

 Specifica il sito di Configuration Manager al quale assegnare il client. Il valore può essere un codice del sito con tre caratteri o la parola AUTO. Se si specifica AUTO o se questa proprietà non viene specificata, il client prova a definire l'assegnazione del sito da Active Directory Domain Services o da un punto di gestione specificato. Per abilitare la proprietà AUTO per gli aggiornamenti client, è necessario anche impostare [SITEREASSIGN](#sitereassign) su TRUE.    

> [!NOTE]  
>  Non usare AUTO se si specifica anche il punto di gestione basato su Internet (CCMHOSTNAME). In questo caso è necessario assegnare direttamente il client al relativo sito.  

 Esempio: `CCMSetup.exe SMSSITECODE=XZY`  

##  <a name="BKMK_attributevalues"></a> Valori di attributo supportati per i criteri di selezione del certificato PKI  
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

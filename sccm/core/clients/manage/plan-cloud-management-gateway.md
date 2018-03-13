---
title: Pianificare il gateway di gestione cloud
titleSuffix: Configuration Manager
description: 
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.technology:
- configmgr-client
ms.assetid: 2dc8c9f1-4176-4e35-9794-f44b15f4e55f
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 051d3fcba379aec83ea7c4dc1e407b3d3e774e12
ms.sourcegitcommit: b653342fb5d69a16e71b3548a7e9a2e47e54bf88
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/12/2018
---
# <a name="plan-for-the-cloud-management-gateway-in-configuration-manager"></a>Pianificare il gateway di gestione cloud in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

A partire dalla versione 1610, il gateway di gestione cloud consente di gestire i client di Configuration Manager su Internet in modo semplice. Il servizio gateway di gestione cloud viene distribuito in Microsoft Azure e richiede una sottoscrizione di Azure. Si connette all'infrastruttura di Configuration Manager locale usando un nuovo ruolo chiamato punto di connessione del gateway di gestione cloud. Dopo che sarà stato completamente distribuito e configurato, i client potranno accedere ai ruoli del sistema del sito di Configuration Manager locale indipendentemente dal fatto che siano connessi alla rete privata interna o su Internet.

> [!TIP]  
> Introdotto con la versione 1610, il cloud management gateway è una funzionalità di versione non definitiva. Per abilitarla, vedere [Usare le funzionalità di versioni non definitive degli aggiornamenti](/sccm/core/servers/manage/pre-release-features).

Usare la console di Configuration Manager per distribuire il servizio in Azure, aggiungere il ruolo punto di connessione del gateway di gestione cloud e configurare i ruoli del sistema del sito per consentire il traffico del gateway di gestione cloud. Il gateway di gestione cloud supporta attualmente solo i ruoli punto di gestione e punto di aggiornamento software.

Per autenticare i computer e crittografare le comunicazioni tra i diversi livelli di servizio sono necessari certificati client e certificati Secure Socket Layer (SSL). I computer client ricevono in genere un certificato client mediante l'imposizione dei criteri di gruppo. Per crittografare il traffico tra i client e il server di sistema del sito che ospita i ruoli, è necessario creare un certificato SSL personalizzato mediante un'autorità di certificazione. È anche necessario configurare un certificato di gestione in Azure che consente a Configuration Manager di distribuire il servizio gateway di gestione cloud.

## <a name="requirements-for-cloud-management-gateway"></a>Requisiti per il gateway di gestione cloud

-    Sistema del sito che esegue il connettore del gateway di gestione cloud per l'uso da parte dei client basati su Internet.

-   Certificati SSL personalizzati dell'autorità di certificazione interna, necessari per crittografare le comunicazioni dai computer client e autenticare l'identità del servizio gateway di gestione cloud.

-   Sottoscrizione di Azure per i servizi cloud.

-   Certificato di gestione di Azure, utilizzato per l'autenticazione di Configuration Manager con Azure.

## <a name="specifications-for-cloud-management-gateway"></a>Specifiche per il gateway di gestione cloud

- Ogni istanza del gateway di gestione cloud supporta 4.000 client.
- È consigliabile creare almeno due istanze del gateway di gestione cloud per aumentare la disponibilità.
- Il gateway di gestione cloud supporta solo i ruoli punto di gestione e punto di aggiornamento software.
-   Le funzionalità seguenti in Configuration Manager non sono attualmente supportate dal gateway di gestione cloud:

    -   Push client
    -   Assegnazione automatica al sito
    -   Catalogo applicazioni, incluse le richieste di approvazione software
    -   Distribuzione completa del sistema operativo
    -   Sequenze di attività (tutte)
    -   Console di Configuration Manager
    -   Strumenti remoti
    -   Sito Web di Reporting
    -   Riattivazione LAN
    -   Client Mac, Linux e UNIX
    -   Azure Resource Manager
    -   Peer cache
    -   Gestione dei dispositivi mobili (MDM) locale

## <a name="cost-of-cloud-management-gateway"></a>Costo del gateway di gestione cloud

>[!IMPORTANT]
>Le informazioni sui costi seguenti sono puramente stime. Altre variabili di ambiente possono influire sul costo complessivo dell'uso del gateway di gestione cloud.

Il gateway di gestione cloud usa le funzionalità di Microsoft Azure seguenti, che vengono addebitate all'account di sottoscrizione di Azure:

-   Macchina virtuale

    -   Per il gateway di gestione cloud è attualmente necessaria una macchina virtuale Standard\_A2. Quando si crea il servizio, è possibile selezionare il numero di macchine virtuali necessarie per supportare il servizio. Uno è il valore predefinito.

    -   Per una stima, supporre che una sola macchina virtuale Azure Standard\_A2 possa supportare circa 2000 client simultanei basati su Internet .

    -   Vedere il [calcolatore dei prezzi di Azure](https://azure.microsoft.com/en-us/pricing/calculator/) per determinare i costi potenziali.

      >[!NOTE]
      >I costi delle macchine virtuali variano a seconda dell'area.

-   Trasferimento dati in uscita

    -   Il flusso dati non compreso nel servizio viene addebitato. Vedere i [dettagli sui prezzi per la larghezza di banda di Azure](https://azure.microsoft.com/pricing/details/bandwidth/) per determinare i costi potenziali.

    -   Per una stima, supporre circa 100 MB per client/mese per client basati su Internet che eseguono l'aggiornamento dei criteri ogni ora.

    >[!NOTE]
    > Se vengono eseguite altre azioni supportate tramite il gateway di gestione cloud, ad esempio la distribuzione di aggiornamenti software o di applicazioni, il trasferimento dei dati in uscita da Azure aumenta.

-   Archivio del contenuto

    -   I client basati su Internet che sono gestiti con il gateway di gestione cloud ottengono contenuto di aggiornamento software da Windows Update senza nessun addebito.

    -   Altri contenuti necessari, ad esempio le applicazioni, devono essere distribuiti in un punto di distribuzione basato sul cloud. Il gateway di gestione cloud supporta attualmente solo il punto di distribuzione cloud per l'invio di contenuto ai client.

    - Per altri dettagli, vedere il costo di utilizzo di una [distribuzione basata sul cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#cost-of-using-cloud-based-distribution).

## <a name="frequently-asked-questions-about-the-cloud-management-gateway-cmg"></a>Domande frequenti sul gateway di gestione cloud

### <a name="why-use-the-cloud-management-gateway"></a>Perché usare il gateway di gestione cloud?

Usare questo ruolo per semplificare la gestione client basata su Internet eseguendo solo tre passaggi dalla console di Configuration Manager.

1. Distribuire il gateway di gestione cloud in Azure usando la [Creazione guidata gateway di gestione cloud](/sccm/core/clients/manage/setup-cloud-management-gateway).
2. Configurare il ruolo del sistema del sito del [punto di connessione del gateway di gestione cloud](/sccm/core/servers/deploy/configure/install-site-system-roles).
3. [Configurare i ruoli per il traffico del gateway di gestione cloud](/sccm/core/clients/manage/setup-cloud-management-gateway#step-7-configure-roles-for-cloud-management-gateway-traffic), ad esempio il punto di gestione e il punto di aggiornamento software.

### <a name="how-does-the-cloud-management-gateway-work"></a>Come funziona il gateway di gestione cloud?

- Il punto di connessione del gateway di gestione cloud consente una connessione coerente e a prestazioni elevate tra Internet e il gateway di gestione cloud.
- Configuration Manager pubblica le impostazioni nel gateway di gestione cloud, incluse le informazioni sulla connessione e le impostazioni di protezione.
- Il gateway di gestione cloud autentica le richieste del client di Configuration Manager e le inoltra al punto di connessione del gateway di gestione cloud. Queste richieste vengono inoltrate ai ruoli della rete aziendale in base ai mapping di URL.

### <a name="how-is-the-cloud-management-gateway-deployed"></a>Come viene distribuito il gateway di gestione cloud?

Il gestore del servizio cloud presente nel punto di connessione del servizio gestisce tutte le attività di distribuzione del gateway di gestione cloud. Esegue inoltre il monitoraggio e l'invio di informazioni sull'integrità del servizio e di registrazione da Azure AD. Verificare che il punto di connessione del servizio sia in [modalità online](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_modes).

#### <a name="certificate-requirements"></a>Requisiti del certificato

Per proteggere il gateway di gestione cloud sono necessari i certificati seguenti:

- **Certificato di gestione**: può trattarsi di qualsiasi certificato, inclusi i certificati autofirmati. È possibile usare un certificato pubblico caricato in Azure AD o un certificato in formato [PFX con chiave privata](/sccm/mdm/deploy-use/create-pfx-certificate-profiles) importato in Configuration Manager per l'autenticazione con Azure AD.
- **Certificato del servizio Web**: è consigliabile usare un certificato di un'autorità di certificazione pubblica per ottenere attendibilità nativa dai client. Creare il record CName nel registrar DNS pubblico. I certificati con caratteri jolly non sono supportati.
- **Certificati dell'autorità di certificazione radice o subordinata**: il gateway di gestione cloud deve eseguire una convalida completa della catena sui certificati PKI del client. Se per l'emissione dei certificati PKI del client si usa un'autorità di certificazione dell'organizzazione e la relativa autorità di certificazione radice o subordinata non è disponibile in Internet, è necessario caricarla nel gateway di gestione cloud.

#### <a name="deployment-process"></a>Processo di distribuzione

La distribuzione si articola in due fasi:

- Distribuire il servizio cloud
    - Caricare il file dello [schema di definizione dei servizi di Azure](https://msdn.microsoft.com/library/azure/ee758711.aspx) (csdef)
    - Caricare il file dello [schema di configurazione dei servizi di Azure](https://msdn.microsoft.com/library/azure/ee758710.aspx) (cscfg)
- Impostare il gateway di gestione cloud sul server di Azure AD e configurare gli endpoint, i gestori HTTP e i servizi in Internet Information Services (IIS)

Se si modifica la configurazione del gateway di gestione cloud, viene avviata una distribuzione di configurazione nel gateway di gestione cloud stesso.

### <a name="where-do-i-set-up-the-cloud-management-gateway"></a>Dove viene configurato il gateway di gestione cloud?
È possibile creare il gateway di gestione cloud nel sito di livello superiore della gerarchia. Se si tratta di un sito di amministrazione centrale, è possibile creare punti di connessione del gateway di gestione cloud nei siti primari figlio.

### <a name="how-does-the-cloud-management-gateway-help-ensure-security"></a>In che modo il gateway di gestione cloud consente di garantire la protezione?

Il gateway di gestione cloud consente di garantire la protezione nei modi seguenti:

- Accetta e gestisce le connessioni dai punti di connessione del gateway di gestione cloud, inclusa l'autenticazione SSL reciproca, usando certificati interni e ID di connessione.
- Accetta e inoltra le richieste client
    - Esegue l'autenticazione preliminare usando l'autenticazione SSL reciproca sul certificato PKI del client.
    - L'elenco di certificati attendibili controlla la radice del certificato PKI del client. È possibile specificare questa impostazione nelle impostazioni di comunicazione del client nelle proprietà del sito. Esegue inoltre per il client la stessa convalida del punto di gestione.
    - Convalida gli URL ricevuti
    - Filtra gli URL ricevuti per verificare se un punto di connessione del gateway di gestione cloud può gestire la richiesta dell'URL.  
    - Controlla la lunghezza del contenuto per ogni endpoint di pubblicazione.
    - Usa l'approccio 'round robin' per bilanciare il carico tra i punti di connessione del gateway di gestione cloud dallo stesso sito.

- Protegge il punto di connessione del gateway di gestione cloud
    - Crea connessioni HTTP/TCP coerenti con tutte le istanze virtuali del gateway di gestione cloud che esegue la connessione. Controlla e gestisce le connessioni ogni minuto.
    - Esegue l'autenticazione SSL reciproca con il gateway di gestione cloud usando certificati interni.
    - Inoltra le richieste HTTP in base ai mapping di URL.
    - Segnala lo stato della connessione per visualizzare lo stato di integrità del servizio di amministrazione.
    - Genera un report sul traffico per ogni endpoint ogni cinque minuti.

- Protegge il client degli endpoint di pubblicazione di Configuration Manager con ruoli quali gli endpoint dell'host del punto di gestione e del punto di aggiornamento software in IIS per gestire le richieste client. Ogni endpoint pubblicato del gateway di gestione cloud ha un mapping di URL.
L'URL esterno è quello usato dal client per comunicare con il gateway di gestione cloud.
L'URL interno è il punto di connessione del gateway di gestione cloud usato per inoltrare le richieste al server interno.

#### <a name="example"></a>Esempio:
Quando si abilita il traffico del gateway di gestione cloud su un punto di gestione, Configuration Manager crea a livello interno un set di mapping di URL per ogni server del punto di gestione, ad esempio ccm_system, ccm_incoming e sms_mp.
L'URL esterno dell'endpoint ccm_system del punto di gestione può essere simile a quanto segue: **https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System**.
L'URL è univoco per ogni punto di gestione. Il client di Configuration Manager inserisce quindi il nome MP abilitato per il gateway di gestione cloud, ad esempio **<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>**, nel relativo elenco Internet di punti di gestione.
Tutti gli URL esterni pubblicati vengono caricati automaticamente nel gateway di gestione cloud, che è quindi in grado di filtrare gli URL. Tutti i mapping di URL vengono replicati al punto di connessione del gateway di gestione cloud. Quest'ultimo può quindi eseguire l'inoltro ai server interni in base al client che richiede l'URL esterno.

### <a name="what-ports-are-used-by-the-cloud-management-gateway"></a>Quali porte vengono usate dal gateway di gestione cloud?

- Nessuna porta in ingresso è necessaria per la rete locale. La distribuzione del gateway di gestione cloud determina la creazione automatica di una serie di gateway di gestione cloud.
- Oltre alla 443, per il punto di connessione del gateway di gestione cloud sono necessarie alcune porte in uscita.

|||||
|-|-|-|-|
|Flusso di dati|Server|Porte server|Client|
|Distribuzione del gateway di gestione cloud|Azure|443|Punto di connessione del servizio Configuration Manager|
|Compilazione canale gateway di gestione cloud|Gateway di gestione cloud|Istanza VM: 1 porta: 443<br>Istanza VM: N (N>=2 e N<= 16) Porte: 10124~N 10140~N|Punto di connessione del gateway di gestione cloud|
|Dal client al gateway di gestione cloud|Gateway di gestione cloud|443|Client|
|Connettore del gateway di gestione cloud al ruolo del sito (attualmente punti di gestione e punti di aggiornamento software)|Ruolo del sito|Protocollo/porte configurati nel ruolo del sito|Punto di connessione del gateway di gestione cloud|

### <a name="how-can-you-improve-performance-of-the-cloud-management-gateway"></a>In che modo è possibile migliorare le prestazioni del gateway di gestione cloud?

- Se possibile, configurare il gateway di gestione cloud, il punto di connessione del gateway di gestione cloud e il server del sito di Configuration Manager nella stessa area di rete per ridurre la latenza.
- Attualmente la connessione tra il client di Configuration Manager e il gateway di gestione cloud non è in grado di riconoscere l'area.
- Per ottenere la disponibilità elevata, è consigliabile avere almeno due istanze virtuali del gateway di gestione cloud e due punti di connessione del gateway di gestione cloud per sito
- È possibile scalare il gateway di gestione cloud per supportare più client mediante l'aggiunta di più istanze di macchine virtuali. Il bilanciamento del carico delle macchine virtuali viene eseguito dall'apposito servizio di Azure AD.
- Creare altri punti di connessione del gateway di gestione cloud per distribuire il carico tra di essi. Il gateway di gestione cloud gestisce il traffico verso i propri punti di connessione mediante un approccio 'round robin'.
- Nella versione 1702 il numero di client supportati per istanza di macchina virtuale del gateway di gestione cloud è 6000. Quando il carico di lavoro del canale del gateway di gestione cloud è molto elevato, la richiesta verrà comunque gestita, ma con tempi più lunghi del normale.

### <a name="how-can-you-monitor-the-cloud-management-gateway"></a>In che modo è possibile monitorare il gateway di gestione cloud?

Per la risoluzione dei problemi relativi alla distribuzione, usare **CloudMgr.log** e **CMGSetup.log**.
Per la risoluzione dei problemi relativi all'integrità del servizio, usare **CMGService.log** e **SMS_CLOUD_PROXYCONNECTOR.log**.
Per la risoluzione dei problemi relativi al traffico client, usare **CMGHttpHandler.log**, **CMGService.Log** e **SMS_CLOUD_PROXYCONNECTOR.log**.

Per un elenco dei file di log relativi al gateway di gestione cloud, vedere [File di log in Configuration Manager](https://docs.microsoft.com/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway)

## <a name="next-steps"></a>Passaggi successivi

[Configurare il gateway di gestione cloud](setup-cloud-management-gateway.md)

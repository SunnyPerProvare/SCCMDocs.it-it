---
title: Certificati per il gateway di gestione cloud
description: Informazioni sui diversi certificati digitali da usare con il gateway di gestione cloud.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 11/27/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8add225db488a749eba98f9015fcb112e8f34f04
ms.sourcegitcommit: 8803a64692f3edc0422b58f6c3037a8796374cc8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/19/2019
ms.locfileid: "57881793"
---
# <a name="certificates-for-the-cloud-management-gateway"></a>Certificati per il gateway di gestione cloud

*Si applica a: System Center Configuration Manager (Current Branch)*

In base allo scenario in cui si gestiscono i client su Internet con il gateway di gestione cloud, è necessario usare uno o più dei seguenti certificati digitali:  

- [Certificato di autenticazione server del gateway di gestione cloud](#bkmk_serverauth)  
    - [Certificato radice trusted del gateway di gestione cloud per i client](#bkmk_cmgroot)  
    - [Certificato di autenticazione server rilasciato da un provider pubblico](#bkmk_serverauthpublic)  
    - [Certificato di autenticazione server rilasciato da un'infrastruttura a chiave pubblica di tipo Enterprise](#bkmk_serverauthpki)  

- [Certificato di gestione di Azure](#bkmk_azuremgmt)  

- [Certificato di autenticazione client](#bkmk_clientauth)  
    - [Certificato radice trusted del client per il gateway di gestione cloud](#bkmk_clientroot)  

- [Abilitare i punti di gestione per HTTPS](#bkmk_mphttps)  


Per altre informazioni sui diversi scenari, vedere [Pianificare il gateway di gestione cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


### <a name="general-information"></a>Informazioni generali
<!--SCCMDocs issue #779-->
I certificati per Cloud Management Gateway supportano le configurazioni seguenti:  

- lunghezza della chiave 2048 bit o 4096 bit

- A partire dalla versione 1710, supporto per provider di archiviazione chiavi per le chiavi private dei certificati. Per altre informazioni, vedere [Panoramica dei certificati CNG](/sccm/core/plan-design/network/cng-certificates-overview).  

- A partire dalla versione 1802, quando si configura Windows con i criteri seguenti: **Crittografia di sistema: utilizza algoritmi FIPS compatibili per crittografia, hash e firma**  

- A partire dalla versione 1802, supporto per **TLS 1.2**. Per altre informazioni, vedere [Riferimento tecnico per i controlli crittografici](/sccm/core/plan-design/security/cryptographic-controls-technical-reference#about-ssl-vulnerabilities).  



## <a name="bkmk_serverauth"></a> Certificato di autenticazione server del gateway di gestione cloud

*Questo certificato è necessario in tutti gli scenari.*

Usare questo certificato quando si crea il gateway di gestione cloud nella console di Configuration Manager.

Il gateway di gestione cloud crea un servizio HTTPS a cui si connettono i client basati su Internet. Il server richiede un certificato di autenticazione server per compilare il canale sicuro. Acquisire un certificato per questo scopo da un provider pubblico o inviarlo dall'infrastruttura a chiave pubblica. Per altre informazioni, vedere [Certificato radice trusted del gateway di gestione cloud per i client](#cmg-trusted-root-certificate-to-clients).

 > [!TIP]
 > Questo certificato richiede un nome univoco globale per identificare il servizio in Azure. Prima di richiedere un certificato, verificare che il nome di dominio di Azure sia univoco. Ad esempio, *GraniteFalls.CloudApp.Net*. Accedere al [portale di Microsoft Azure](https://portal.azure.com). Selezionare **Crea una risorsa**, scegliere la categoria **Calcolo**, quindi selezionare **Servizio cloud**. Digitare un prefisso nel campo **Nome DNS**, ad esempio *GraniteFalls*. L'interfaccia indica se il nome di dominio è disponibile o se è già in uso in un altro servizio. Non creare il servizio nel portale, usare questo processo per verificare la disponibilità del nome. 
  
 > [!TIP]
 > Se il servizio CMG verrà abilitato anche come punto di distribuzione cloud, verificare che il nome del servizio CMG scelto sia anche un nome univoco di account di archiviazione di Azure. Ad esempio, *GraniteFalls*. Accedere al [portale di Microsoft Azure] (https://portal.azure.com). Selezionare **Crea una risorsa**, scegliere la categoria **Archiviazione** e quindi selezionare **Account di archiviazione: BLOB, File, Tabelle, Code**. Fare clic su **Crea** e in **Dettagli dell'istanza** immettere lo stesso nome scelto per il servizio CMG, ad esempio *GraniteFalls*. L'interfaccia indica se il nome dell'account di archiviazione è disponibile o se è già in uso in un altro servizio. Non creare l'account di archiviazione nel portale, ma usare semplicemente questa procedura per verificare la disponibilità del nome. Se il nome del servizio cloud CMG è univoco, ma non lo è il nome dell'account di archiviazione, il provisioning non riuscirà.
 
 > [!NOTE]
 > A partire dalla versione 1802, il certificato di autenticazione server del Cloud Management Gateway supporta i caratteri jolly. Alcune autorità di certificazione rilasciano certificati in cui viene usato un carattere jolly per il nome host. Ad esempio, **\*.contoso.com**. Alcune organizzazioni usano certificati con caratteri jolly per semplificare l'infrastruttura a chiave pubblica e ridurre i costi di manutenzione.<!--491233-->  
 > 
 > Per altre informazioni su come usare un certificato con caratteri jolly con CMG, vedere [Impostare un Cloud Management Gateway](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#set-up-a-cmg).<!--SCCMDocs issue #565-->  


### <a name="bkmk_cmgroot"></a> Certificato radice trusted del gateway di gestione cloud per i client

I client devono considerare attendibile il certificato di autenticazione server del gateway di gestione cloud. Esistono due metodi per confermare l'attendibilità: 

- Usare un certificato di un provider pubblico considerato attendibile a livello globale. Ad esempio, tra gli altri, DigiCert, Thawte, o VeriSign. I client Windows includono le autorità di certificazione (CA) che rilasciano i certificati radice trusted da questi provider. Usando un certificato di autenticazione server rilasciato da uno di questi provider, i client confermano automaticamente l'attendibilità.  

- Usare un certificato rilasciato da un'autorità di certificazione globale (enterprise) dall'infrastruttura a chiave pubblica. Nella maggior parte delle implementazioni di infrastruttura a chiave pubblica di tipo Enterprise le autorità di certificazione radice attendibili vengono aggiunte ai client di Windows. Ad esempio, usando i servizi certificati Active Directory con criteri di gruppo. Se si rilascia il certificato di autenticazione server per il gateway di gestione cloud da un'autorità di certificazione che i client non considerano automaticamente attendibile, aggiungere il certificato radice trusted di tale autorità ai client basati su Internet.  

    - È inoltre possibile usare i profili dei certificati di Configuration Manager per eseguire il provisioning dei certificati nei client. Per altre informazioni, vedere l'[introduzione alle raccolte](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

> [!Note]  
> A partire dalla versione 1806, quando si crea un CMG non è più necessario specificare un certificato radice trusted nella pagina Impostazioni. Questo certificato non è obbligatorio se si usa Azure Active Directory (Azure AD) per l'autenticazione client, ma veniva richiesto nella procedura guidata. Se si usano certificati di autenticazione client PKI, è comunque necessario aggiungere un certificato radice trusted al CMG.<!--SCCMDocs-pr issue #2872-->  


### <a name="bkmk_serverauthpublic"></a> Certificato di autenticazione server rilasciato da un provider pubblico

Un provider di certificati di terze parti non può creare un certificato per CloudApp.net, perché il dominio è di proprietà di Microsoft. È possibile ottenere solo un certificato emesso per un dominio di cui si è proprietari. Il motivo principale per l'acquisizione di un certificato da un provider di terze parti è che i client già considerano attendibile il certificato radice del provider.

Usare la seguente procedura per creare un alias DNS:

1. Creare un record di nome canonico (CNAME) nel DNS pubblico dell'organizzazione. Questo record crea un alias per il gateway di gestione cloud con un nome descrittivo usato dall'utente nel certificato pubblico.

    Ad esempio, Contoso assegna al gateway di gestione cloud il nome **GraniteFalls**, che diventa **GraniteFalls.CloudApp.Net** in Azure. Nello spazio dei nomi contoso.com del DNS pubblico di Contoso l'amministratore DNS crea un nuovo record CNAME **GraniteFalls.Contoso.com** per il nome host effettivo, **GraniteFalls.CloudApp.net**.  

2. Richiedere un certificato di autenticazione server da un provider pubblico usando il nome comune dell'alias CNAME.
Ad esempio, Contoso usa **GraniteFalls.Contoso.com** per il nome comune del certificato.  

3. Creare il gateway di gestione cloud nella console di Configuration Manager usando questo certificato. Nella pagina **Impostazioni** della Creazione guidata del gateway di gestione cloud:   

    - Quando si aggiunge il certificato del server per questo servizio cloud (da **File di certificato**), la procedura guidata estrae il nome host dal nome comune del certificato come nome del servizio.  

    - Aggiunge quindi tale nome host a **cloudapp.net** o **usgovcloudapp.net** per il cloud di Azure Governo degli Stati Uniti come FQDN del servizio per creare il servizio in Azure.  

    - Ad esempio, quando Contoso crea il gateway di gestione cloud, Configuration Manager estrae il nome host **GraniteFalls** dal nome comune del certificato. Azure crea il servizio effettivo come **GraniteFalls.CloudApp.net**.  

Quando si crea l'istanza CMG in Configuration Manager, mentre il certificato ha GraniteFalls.Contoso.com, Configuration Manager estrae solo il nome host, ad esempio: GraniteFalls. Questo nome host viene accodato a CloudApp.net, che Azure richiede quando crea un servizio cloud. L'alias CNAME nello spazio dei nomi DNS per il dominio, Contoso.com, esegue il mapping dei due nomi di dominio completi. Configuration Manager offre ai client i criteri per accedere al CMG, il mapping DNS li collega in modo che possano accedere in modo sicuro al servizio in Azure.<!--SCCMDocs issue #565-->  


### <a name="bkmk_serverauthpki"></a> Certificato di autenticazione server rilasciato da un'infrastruttura a chiave pubblica di tipo Enterprise

Creare un certificato SSL personalizzato per il gateway di gestione cloud identico a quello di un punto di distribuzione cloud. Seguire le istruzioni per la [distribuzione del certificato di servizio per i punti di distribuzione basati su cloud](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012) procedendo in modo diverso per le operazioni seguenti:

- Quando si richiede il certificato del server Web personalizzato, specificare un FQDN per il nome comune del certificato. Il nome può essere un nome di dominio pubblico di cui si è proprietari o è possibile usare il dominio cloudapp.net. Se si usa il proprio dominio pubblico, fare riferimento al processo sopra descritto per la creazione di un alias DNS nel DNS pubblico dell'organizzazione.  

- Quando si usa il dominio pubblico cloudapp.net per il certificato CMG del server Web:  

    - Nel cloud pubblico di Azure usare un nome che termina con **cloudapp.net**  

    - Usare un nome che termina con **usgovcloudapp.net** per il cloud di Azure Governo degli Stati Uniti  



## <a name="bkmk_azuremgmt"></a> Certificato di gestione di Azure

*Questo certificato è obbligatorio per le distribuzioni di servizi classiche. Non è necessario per le distribuzioni di Azure Resource Manager.*

> [!Important]  
> A partire dalla versione 1810, le distribuzioni classiche del servizio in Azure sono deprecate in Configuration Manager. Iniziare a usare le distribuzioni di Azure Resource Manager per il gateway di gestione cloud. Per altre informazioni, vedere [Pianificare il gateway di gestione cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).

Specificare questo certificato nel portale di Azure quando si crea il gateway di gestione cloud nella console di Configuration Manager.

Per creare il gateway di gestione cloud in Azure, il punto di connessione del servizio Configuration Manager deve prima eseguire l'autenticazione alla sottoscrizione di Azure. Quando si usa una distribuzione classica del servizio, per l'autenticazione viene usato il certificato di gestione di Azure. Un amministratore di Azure carica questo certificato nella sottoscrizione dell'utente. Quando si crea il gateway di gestione cloud nella console di Configuration Manager specificare questo certificato.

Per altre informazioni e istruzioni su come caricare un certificato di gestione, vedere gli articoli seguenti nella documentazione di Azure:

- [Servizi cloud e certificati di gestione](https://docs.microsoft.com/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)  

- [Caricare un certificato di gestione dei servizi di Azure](https://docs.microsoft.com/azure/azure-api-management-certs)  

> [!IMPORTANT]
> Assicurarsi di copiare l'ID sottoscrizione associato al certificato di gestione. Usare questo certificato per creare il gateway di gestione cloud nella console di Configuration Manager.



## <a name="bkmk_clientauth"></a> Certificato di autenticazione client

*Questo certificato è necessario per i client basati su Internet che eseguono Windows 7, Windows 8.1 e dispositivi Windows 10 che non fanno parte di Azure Active Directory (Azure AD). È necessario anche per il punto di connessione del gateway di gestione cloud. Non è richiesto per i client Windows 10 aggiunti ad Azure AD.*

I client usano questo certificato per l'autenticazione con il gateway di gestione cloud. I dispositivi Windows 10 ibridi o aggiunti a un dominio cloud non richiedono questo certificato perché usano Azure AD per l'autenticazione.

Eseguire il provisioning del certificato all'esterno del contesto di Configuration Manager. Ad esempio, usare Servizi certificati Active Directory e i criteri di gruppo per rilasciare i certificati di autenticazione client. Per altre informazioni, vedere [Distribuzione del certificato client per computer Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).

Il punto di connessione del gateway di gestione cloud richiede questo certificato per inoltrare in modo sicuro le richieste client al punto di gestione HTTPS. Se si usa Azure AD o HTTP avanzato, questo certificato non è obbligatorio. Per altre informazioni, vedere [Abilitare i punti di gestione per HTTPS](#bkmk_mphttps).


### <a name="bkmk_clientroot"></a> Certificato radice trusted del client per il gateway di gestione cloud

*Questo certificato è necessario quando si usano i certificati di autenticazione client. Quando tutti i client usano Azure AD per l'autenticazione, questo certificato non è obbligatorio.* 

Usare questo certificato quando si crea il gateway di gestione cloud nella console di Configuration Manager.

Il gateway di gestione client deve considerare attendibile il certificato di autenticazione del client. Per confermare l'attendibilità, specificare la catena di certificati radice trusted. È possibile specificare due autorità di certificazione radice attendibili e quattro autorità intermedie (subordinate). 


#### <a name="export-the-client-certificates-trusted-root"></a>Esportare la radice attendibile del certificato client

Dopo aver emesso un certificato di autenticazione client per un computer, usare questo processo in tale computer per esportare la radice attendibile.

1.  Aprire il menu Start. Digitare "esegui" per aprire la finestra di esecuzione. Aprire `mmc`.  

2.  Dal menu file scegliere **Aggiungi/Rimuovi snap-in**.  

3.  Nella finestra di dialogo Aggiungi o rimuovi snap-in selezionare **Certificati**, quindi selezionare **Aggiungi**.  

    a. Nella finestra di dialogo Snap-in certificati selezionare **Account del computer** e selezionare **Avanti**.  

    b. Nella finestra di dialogo Selezione computer selezionare **Computer locale** e quindi **Fine**.  

    c. Nella finestra di dialogo Aggiungi o rimuovi snap-in selezionare **OK**.  

4.  Espandere **Certificati**, espandere **Personale** e selezionare **Certificati**.  

5.  Selezionare un certificato il cui scopo designato è **Autenticazione client**.  

    a. Dal menu Azione selezionare **Apri**.  

    b. Passare alla scheda **Percorso certificazione**.  

    c. Selezionare il certificato successivo procedendo verso l'alto nella catena, quindi selezionare **Visualizza certificato**.  

6.  Nella nuova finestra di dialogo Certificato passare alla scheda **Dettagli**. Selezionare **Copia su file**.  

7.  Completare l'Esportazione guidata certificati usando il formato di certificato predefinito, **DER encoded binary X.509 (.CER)**. Prendere nota del nome e del percorso del certificato esportato.  

8. Esportare tutti i certificati presenti nel percorso di certificazione del certificato di autenticazione client originale. Prendere nota dei certificati esportati che rappresentano autorità di certificazione intermedie e di quelli che rappresentano autorità radice attendibili.  



## <a name="bkmk_mphttps"></a> Abilitare i punti di gestione per HTTPS

Eseguire il provisioning del certificato all'esterno del contesto di Configuration Manager. Ad esempio, usare Servizi certificati Active Directory e i criteri di gruppo per rilasciare un certificato del server Web. Per altre informazioni, vedere [Requisiti dei certificati PKI](/sccm/core/plan-design/network/pki-certificate-requirements) e [Distribuzione del certificato del server Web per sistemi del sito che eseguono IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).


- Nelle versioni 1706 o 1710, quando si gestiscono client tradizionali con identità locale usando un certificato di autenticazione client, questo certificato è consigliato ma non obbligatorio.  

- Nella versione 1710, quando si gestiscono i client Windows 10 aggiunti ad Azure AD, questo certificato è obbligatorio per i punti di gestione.  

- A partire dalla versione 1802 questo certificato è necessario in tutti gli scenari. Solo i punti di gestione abilitati per il gateway di gestione cloud devono essere HTTPS. Questa modifica del comportamento offre un supporto migliore per l'autenticazione basata su token di Azure AD.  

- A partire dalla versione 1806, quando si usa l'opzione del sito **Usa i certificati generati da Configuration Manager per sistemi del sito HTTP**, il punto di gestione può essere HTTP. Per altre informazioni, vedere [HTTP avanzato](/sccm/core/plan-design/hierarchy/enhanced-http).

### <a name="management-point-client-connection-mode-summary"></a>Riepilogo delle modalità di connessione client ai punti di gestione
Queste tabelle offrono un riepilogo che indica se il punto di gestione richiede HTTP o HTTPS, a seconda del tipo di client e di versione del sito.

#### <a name="for-internet-based-clients-communicating-with-the-cloud-management-gateway"></a>Per i client basati su Internet che comunicano con il gateway di gestione cloud
Configurare un punto di gestione locale per consentire le connessioni dal gateway di gestione cloud con la modalità di connessione client indicata di seguito:

| Tipo di client   | 1706        | 1710        | 1802        | 1806        |
|------------------|-------------|-------------|-------------|-------------|
| Gruppo di lavoro        | HTTP, HTTPS | HTTP, HTTPS | HTTPS       | E-HTTP<sup>[Note 1](#bkmk_note1)</sup>, HTTPS |
| Aggiunto a un dominio AD | HTTP, HTTPS | HTTP, HTTPS | HTTPS       | E-HTTP<sup>[Note 1](#bkmk_note1)</sup>, HTTPS |
| Aggiunto ad Azure AD  | HTTPS       | HTTPS       | HTTPS       | E-HTTP, HTTPS |
| Aggiunto a ibrido    | HTTP, HTTPS | HTTP, HTTPS | HTTPS       | E-HTTP, HTTPS |

<a name="bkmk_note1"></a> 

> [!Note]  
> **Nota 1**: questa configurazione richiede che il client usi un [certificato di autenticazione client](#bkmk_clientauth) e supporti solo scenari incentrati sui dispositivi.  

#### <a name="for-on-premises-clients-communicating-with-the-on-premises-management-point"></a>Per i client locali che comunicano con il punto di gestione locale
Configurare un punto di gestione locale con la modalità di connessione client indicata di seguito:

| Tipo di client   | 1706        | 1710        | 1802        | 1806        |
|------------------|-------------|-------------|-------------|-------------|
| Gruppo di lavoro        | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS |
| Aggiunto a un dominio AD | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS |
| Aggiunto ad Azure AD  | HTTPS       | HTTPS       | HTTPS       | HTTPS       |
| Aggiunto ad AD ibrido    | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS | HTTP, HTTPS |

> [!Note]  
> Nella versione 1806 i client aggiunti a un dominio AD supportano sia gli scenari incentrati sui dispositivi, sia quelli incentrati sull'utente che comunicano con un punto di gestione HTTP o HTTPS.  
> 
> I client aggiunti ad Azure AD e AD ibrido possono comunicare via HTTP per gli scenari incentrati sui dispositivi, ma devono usare E-HTTP o HTTPS per abilitare gli scenari incentrati sull'utente. In caso contrario, si comportano come client del gruppo di lavoro.  


#### <a name="legend-of-terms"></a>Legenda dei termini
- *Gruppo di lavoro*: il dispositivo non è stato aggiunto a un dominio o ad Azure AD, ma ha un [certificato di autenticazione client](#bkmk_clientauth)  
- *Aggiunto a un dominio AD*: il dispositivo viene aggiunto a un dominio di Active Directory locale  
- *Aggiunto ad Azure AD*: o aggiunto al dominio cloud: il dispositivo viene aggiunto a un tenant di Azure Active Directory  
- *Aggiunto ad AD ibrido*: il dispositivo viene aggiunto sia a un dominio di Active Directory, sia a un tenant di Azure AD  
- *HTTP*: nelle proprietà del punto di gestione le connessioni client sono impostate su **HTTP**  
- *HTTPS*: nelle proprietà del punto di gestione le connessioni client sono impostate su **HTTPS**  
- *E-HTTP*: nella scheda Comunicazione computer client delle proprietà del sito configurare le impostazioni di sistema del sito per **HTTPS o HTTP** e abilitare l'opzione **Usa i certificati generati da Configuration Manager per sistemi del sito HTTP**. Si configura il punto di gestione per il protocollo HTTP. Il punto di gestione HTTP è pronto per la comunicazione HTTP e HTTPS (scenari di autenticazione basata su token).   



## <a name="next-steps"></a>Passaggi successivi

- [Configurare il gateway di gestione cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)  

- [Domande frequenti sul gateway di gestione cloud](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)  

- [Sicurezza e privacy per il gateway di gestione del cloud](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)  

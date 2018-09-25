---
title: Opzioni dei ruoli del sistema del sito
titleSuffix: Configuration Manager
description: Per informazioni dettagliate sui ruoli del sistema del sito di Configuration Manager non di chiara comprensione, vedere questo articolo.
ms.date: 08/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 379fa3637d1634caf4797b1f1b7029e3531158cc
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/06/2018
ms.locfileid: "43893526"
---
# <a name="configuration-options-for-site-system-roles-in-configuration-manager"></a>Opzioni di configurazione per i ruoli del sistema del sito in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La maggior parte delle opzioni di configurazione per i ruoli del sistema del sito di Configuration Manager è di chiara comprensione o descritta nelle finestre di dialogo o nella procedura guidata durante la configurazione. Le sezioni seguenti illustrano i ruoli del sistema del sito le cui impostazioni possono richiedere informazioni aggiuntive.  



##  <a name="BKMK_ApplicationCatalog_Website"></a> Punto per siti Web del Catalogo applicazioni  

> [!Note]  
> A partire dalla versione 1806, il punto per siti Web del Catalogo applicazioni non è più *necessario*, ma è ancora *supportato*. Per altre informazioni, vedere [Configurare Software Center](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex).  
> 
> L'**esperienza utente di Silverlight** per il ruolo Punto per siti Web del Catalogo applicazioni non è più supportato. Per altre informazioni, vedere [Funzionalità rimosse e deprecate](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  

 Per altre informazioni su come configurare il punto per siti Web del Catalogo applicazioni, vedere [Pianificare e configurare la gestione delle applicazioni](/sccm/apps/plan-design/plan-for-and-configure-application-management).  

 #### <a name="client-connections"></a>Connessioni client
 Selezionare **HTTPS** per usare l'impostazione di connessione più sicura e verificare se i client si connettono da Internet. Questa opzione richiede un certificato PKI sul server per l'autenticazione tra client e server e per la crittografia dei dati tramite Secure Socket Layer (SSL). Per altre informazioni, vedere [requisiti dei certificati PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Per un esempio di distribuzione del certificato del server e per informazioni sulla relativa configurazione in Internet Information Services (IIS), vedere [Distribuzione del certificato del server Web per sistemi del sito che eseguono IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  

 #### <a name="add-application-catalog-website-to-trusted-sites-zone"></a>Aggiunta del sito Web del Catalogo applicazioni all'area siti attendibili  
 Questo messaggio mostra il valore nelle impostazioni client predefinite a seconda che l'impostazione client **Aggiungere il sito Web del catalogo delle applicazioni all'area siti attendibili di Internet Explorer** sia impostata su **True** o **False**. Se per configurare questa impostazione si sono usate impostazioni client personalizzate, abilitare questa impostazione.  

 Se questo sistema del sito è configurato per un nome di dominio completo (FQDN) e il sito Web non si trova nell'area siti attendibili in Internet Explorer, gli utenti che si connettono al Catalogo applicazioni devono immettere le credenziali.  

 #### <a name="organization-name"></a>Nome organizzazione  

 Immettere il nome visualizzato dagli utenti nel Catalogo applicazioni. Queste informazioni di personalizzazione consentono agli utenti di identificare il sito Web come fonte attendibile.  



##  <a name="BKMK_ApplicationCatalog_WebService"></a> Punto per servizi Web del Catalogo applicazioni  

> [!Note]  
> A partire dalla versione 1806, il punto per servizi Web del Catalogo applicazioni non è più *necessario*, ma è ancora *supportato*. Per altre informazioni, vedere [Configurare Software Center](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex).  

 Per altre informazioni su come configurare il punto per servizi Web del Catalogo applicazioni, vedere [Pianificare e configurare la gestione delle applicazioni](/sccm/apps/plan-design/plan-for-and-configure-application-management).  

 #### <a name="https"></a>HTTPS

 Selezionare **HTTPS** per l'autenticazione tra i punti per siti Web del Catalogo applicazioni e questo punto per servizi Web del Catalogo applicazioni. Questa opzione richiede un certificato PKI sui server che eseguono il punto per siti Web del Catalogo applicazioni per l'autenticazione server e per la crittografia dei dati tramite SSL. Per altre informazioni, vedere [requisiti dei certificati PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Per un esempio di distribuzione del certificato del server e per informazioni sulla relativa configurazione in Internet Information Services (IIS), vedere [Distribuzione del certificato del server Web per sistemi del sito che eseguono IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  



##  <a name="BKMK_CertificateRegistrationPoint"></a> Punto di registrazione certificati  

 Per altre informazioni su come configurare il punto di registrazione certificati, vedere [Introduzione ai profili certificato](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  



##  <a name="BKMK_Distribution_Point"></a> Punto di distribuzione  

 Per altre informazioni su come configurare il punto di distribuzione per la distribuzione del contenuto, vedere [Gestire il contenuto e l'infrastruttura del contenuto](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  

 Per altre informazioni su come configurare il punto di distribuzione per le distribuzioni di PXE, vedere [Usare PXE per distribuire Windows in rete](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).  

 Per altre informazioni su come configurare il punto di distribuzione per le distribuzioni multicast, vedere [Usare il multicast per distribuire Windows in rete](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network).  

 #### <a name="install-and-configure-iis-if-required-by-configuration-manager"></a>Installa e configura IIS, se richiesto da Configuration Manager
 Selezionare questa opzione per consentire a Configuration Manager di installare e configurare IIS nel sistema del sito, se non è già installato. IIS deve essere installato su tutti i punti di distribuzione ed è necessario selezionare questa impostazione per proseguire la procedura guidata.  

 #### <a name="site-system-installation-account"></a>Account di installazione sistema del sito
 Per i punti di distribuzione installati su un server del sito, solo l'account del computer del server del sito viene supportato per l'uso come Account di installazione sistema del sito. Per altre informazioni, vedere [Account](/sccm/core/plan-design/hierarchy/accounts#site-system-installation-account).  

 #### <a name="create-a-self-signed-certificate-or-import-a-pki-client-certificate"></a>Creare un certificato autofirmato o importare un certificato client PKI
 Questo certificato ha due scopi:  

1.  Consente l'autenticazione tra il punto di distribuzione e un punto di gestione prima che il punto di distribuzione invii messaggi di stato.  

2.  Quando si seleziona **Abilita supporto PXE per i client**, il certificato viene inviato ai computer per l'avvio PXE. Usano questo certificato per connettersi a un punto di gestione durante la distribuzione del sistema operativo.  

Quando tutti i punti di gestione nel sito sono configurati per il protocollo HTTP, è necessario creare un certificato autofirmato. Quando i punti di gestione sono configurati per HTTPS, importare un certificato client PKI.  

Per importare il certificato, cercare un file Public-Key Cryptography Standards #12 (PKCS #12) che contenga un certificato PKI con i requisiti seguenti per Configuration Manager:  

-   Lo scopo designato deve includere l'autenticazione client.  

-   La chiave privata deve essere configurata per l'esportazione.  

Non sono previsti requisiti specifici per il nome del soggetto del certificato o per il nome alternativo del soggetto. È possibile usare lo stesso certificato per più punti di distribuzione.  

Per altre informazioni sui requisiti dei certificati, vedere [Requisiti dei certificati PKI](/sccm/core/plan-design/network/pki-certificate-requirements). 

Per un esempio di distribuzione di questo certificato, vedere [Distribuire il certificato client per punti di distribuzione](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012).  

#### <a name="enable-this-distribution-point-for-prestaged-content"></a>Abilita questo punto di distribuzione per il contenuto pre-installato
Selezionare questa casella di controllo per abilitare il punto di distribuzione per i contenuti in versione di preproduzione. Quando si abilita questa opzione, è possibile configurare il comportamento della distribuzione del contenuto. È possibile scegliere se pre-installare sempre il contenuto sul punto di distribuzione, se pre-installare il contenuto iniziale per il pacchetto ma usare il normale processo di distribuzione del contenuto in presenza di aggiornamenti oppure se usare sempre il normale processo di distribuzione per il contenuto nel pacchetto. Per altre informazioni, vedere [Contenuto pre-installato](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent).  

#### <a name="boundary-groups"></a>Gruppi di limiti
 È possibile associare i gruppi di limiti a un punto di distribuzione. Durante la distribuzione del contenuto, i client devono trovarsi in un gruppo di limiti associato al punto di distribuzione per usarlo come percorso di origine per il contenuto. Configurare relazioni tra gruppi di limiti che controllano quando un client può iniziare a cercare percorsi di origine del contenuto validi in gruppi di limiti aggiuntivi. Per altre informazioni, vedere [Gruppi di limiti](/sccm/core/servers/deploy/configure/boundary-groups).



##  <a name="BKMK_Enrollment_Point"></a> Punto di registrazione  

I punti di registrazione vengono usati per installare i computer macOS e registrare i dispositivi gestiti con la funzionalità di gestione dei dispositivi mobili in locale. Per altre informazioni, vedere gli articoli seguenti:  

-   [Come distribuire i client in computer Mac](/sccm/core/clients/deploy/deploy-clients-to-macs)  

-   [Modalità di registrazione dei dispositivi nella gestione di dispositivi mobili locale](/sccm/mdm/deploy-use/user-enroll-devices-on-premises-mdm)  

#### <a name="allowed-connections"></a>Connessioni consentite
 L'impostazione HTTPS viene selezionata automaticamente e richiede un certificato PKI sul server per l'autenticazione tra server e punto proxy di registrazione o punto di servizio fuori banda e per la crittografia dei dati tramite SSL. Per altre informazioni, vedere [requisiti dei certificati PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Per un esempio di distribuzione del certificato del server e per informazioni sulla relativa configurazione in IIS, vedere [Distribuzione del certificato del server Web per sistemi del sito che eseguono IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  



##  <a name="BKMK_Enrollment_Proxy_Point"></a> Punto proxy di registrazione  

Per altre informazioni su come configurare un punto proxy di registrazione per i dispositivi mobili, vedere [Modalità di registrazione dei dispositivi nella gestione di dispositivi mobili locale](/sccm/mdm/deploy-use/user-enroll-devices-on-premises-mdm).  

#### <a name="client-connections"></a>Connessioni client
 L'impostazione HTTPS viene selezionata automaticamente. Nel server sono necessari i certificati PKI seguenti: 
- Per l'autenticazione del server ai dispositivi mobili e ai computer Mac registrati con Configuration Manager 
- Per la crittografia dei dati tramite Secure Sockets Layer (SSL)

Per altre informazioni sui requisiti dei certificati, vedere [Requisiti dei certificati PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

 Per un esempio di distribuzione del certificato del server e per informazioni sulla relativa configurazione in IIS, vedere [Distribuzione del certificato del server Web per sistemi del sito che eseguono IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).  



##  <a name="BKMK_Fallback_Status_Point"></a> Punto di stato di fallback  

#### <a name="number-of-state-messages-and-throttle-interval-in-seconds"></a>Numero di messaggi di stato e Intervallo di limitazione (in secondi)
Le impostazioni predefinite per queste opzioni sono 10.000 messaggio di stato e 3.600 secondi per l'intervallo di limitazione. Anche se queste impostazioni sono sufficienti nella maggior parte dei casi, potrebbe essere necessario modificarle quando entrambe le condizioni seguenti sono vere:  

-   Il punto di stato di fallback accetta connessioni solo dalla rete intranet.  

-   Il punto di stato di fallback viene utilizzato durante un'implementazione della distribuzione client per molti computer.  

In questo scenario, un flusso continuo di messaggi di stato può creare un backlog di messaggi di stato che determina un utilizzo elevato del processore sul server del sito per un periodo di tempo prolungato. Inoltre, potrebbe non essere possibile visualizzare le informazioni aggiornate sulla distribuzione dei client nella console di Configuration Manager e nei report sulla distribuzione dei client.  

Queste impostazioni del punto di stato di fallback sono progettate per essere configurate per messaggi di stato generati durante la distribuzione dei client. Non sono pensate per problemi di comunicazione dei client, come nel caso in cui i client su Internet non riescono a connettersi al punto di gestione basato su Internet. Dal momento che il punto di stato di fallback non può applicare queste impostazioni solo ai messaggi di stato generati durante la distribuzione dei client, non configurarle quando il punto di stato di fallback accetta connessioni da Internet.  

Ogni computer in cui l'installazione del client di Configuration Manager viene completata correttamente invia i quattro messaggi di stato seguenti al punto di stato di fallback:  

-   Distribuzione di client avviata  

-   Distribuzione client completata  

-   Assegnazione client avviata  

-   Assegnazione client completata  

I computer nei quali non è possibile eseguire l'installazione o che assegnano il client di Configuration Manager inviano messaggi di stato aggiuntivi.  

Se ad esempio si distribuisce il client di Configuration Manager a 20.000 computer, questa distribuzione può inviare 80.000 messaggi di stato al punto di stato di fallback. Dal momento che la configurazione predefinita della limitazione della larghezza di banda della rete consente l'invio di 10.000 messaggi di stato al punto di stato di fallback ogni 3600 secondi (1 ora), è possibile che i messaggi di stato vengano inclusi nel backlog sul punto di stato di fallback. Considerare anche la larghezza di banda della rete disponibile tra il punto di stato di fallback e il server del sito e la potenza di quest'ultimo per l'elaborazione di un numero elevato di messaggi di stato.  

Per evitare questi problemi, prendere in considerazione l'opportunità di aumentare il numero di messaggi di stato e ridurre l'intervallo di limitazione.  

Reimpostare i valori di limitazione per il punto di stato di fallback in presenza di una delle condizioni seguenti:  

-   Si ritiene che i valori di limitazione correnti siano superiori a quelli richiesti per l'elaborazione dei messaggi di stato dal punto di stato di fallback.  

-   Si ritiene che le impostazioni di limitazione correnti determinino un utilizzo elevato del processore sul server del sito.  

Non modificare le impostazioni di limitazione per il punto di stato di fallback senza aver compreso le conseguenze di tale azione. Se ad esempio le impostazioni di limitazione vengono aumentate, l'utilizzo del processore sul server del sito potrebbe crescere contestualmente, rallentando così tutte le operazioni del sito.  

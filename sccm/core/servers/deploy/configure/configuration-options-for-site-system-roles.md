---
title: Pianificare i server e i ruoli del sistema | Microsoft Docs
description: Per informazioni dettagliate sui ruoli del sistema del sito di Configuration Manager non di chiara comprensione, vedere questo articolo.
ms.custom: na
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
caps.latest.revision: "5"
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.openlocfilehash: b4db5d86cc0ed020ed176feb2e8f1f9dc51a2280
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="configuration-options-for-site-system-roles-for-system-center-configuration-manager"></a>Opzioni di configurazione per i ruoli del sistema del sito per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

La maggior parte delle opzioni di configurazione per i ruoli del sistema del sito di System Center Configuration Manager è di chiara comprensione o descritta nelle finestre di dialogo o nella procedura guidata durante la configurazione. Le sezioni seguenti illustrano i ruoli del sistema del sito le cui impostazioni possono richiedere informazioni aggiuntive.  

##  <a name="BKMK_ApplicationCatalog_Website"></a> Punto per siti Web del Catalogo applicazioni  
 Per informazioni su come configurare il punto per siti Web del Catalogo applicazioni, vedere [Pianificare e configurare la gestione delle applicazioni in System Center Configuration Manager](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  

 **Connessioni client**  

 Selezionare **HTTPS** per usare l'impostazione di connessione più sicura e verificare se i client si connettono da Internet. Questa opzione richiede un certificato PKI sul server per l'autenticazione tra client e server e per la crittografia dei dati tramite Secure Socket Layer (SSL). Per altre informazioni sui requisiti dei certificati, vedere [Requisiti dei certificati PKI per System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Per un esempio di distribuzione del certificato del server e per informazioni sulla relativa configurazione in Internet Information Services (IIS), vedere la sezione *Distribuzione del certificato del server Web per sistemi del sito che eseguono IIS* nell'argomento [Esempio dettagliato di distribuzione dei certificati PKI per Configuration Manager: Autorità di certificazione di Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

 **Aggiunta del sito Web del Catalogo applicazioni all'area siti attendibili**  

 Questo messaggio mostra il valore nelle impostazioni client predefinite a seconda che l'impostazione client **Aggiungere il sito Web del catalogo delle applicazioni all'area siti attendibili di Internet Explorer** sia impostata su **True** o **False**. Se per configurare questa impostazione si sono usate impostazioni client personalizzate, è necessario controllare personalmente questo valore.  

 Se questo sistema del sito è configurato per un nome di dominio completo (FQDN) e il sito Web non si trova nell'area siti attendibili in Internet Explorer, gli utenti che si connettono al Catalogo applicazioni devono immettere le credenziali.  

 **Nome organizzazione**  

 Immettere il nome visualizzato dagli utenti nel Catalogo applicazioni. Queste informazioni di personalizzazione consentono agli utenti di identificare il sito Web come fonte attendibile.  

##  <a name="BKMK_ApplicationCatalog_WebService"></a> Punto per servizi Web del Catalogo applicazioni  
 Per informazioni su come configurare il punto per servizi Web del Catalogo applicazioni, vedere [Pianificare e configurare la gestione delle applicazioni in System Center Configuration Manager](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  

 **HTTPS**  

 Selezionare **HTTPS** per l'autenticazione tra i punti per siti Web del Catalogo applicazioni e questo punto per servizi Web del Catalogo applicazioni.  Questa opzione richiede un certificato PKI sui server che eseguono il punto per siti Web del Catalogo applicazioni per l'autenticazione server e per la crittografia dei dati tramite SSL. Per altre informazioni sui requisiti dei certificati, vedere [Requisiti dei certificati PKI per System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Per un esempio di distribuzione del certificato del server e per informazioni sulla relativa configurazione in Internet Information Services (IIS), vedere la sezione *Distribuzione del certificato del server Web per sistemi del sito che eseguono IIS* in [Esempio dettagliato di distribuzione dei certificati PKI per System Center Configuration Manager: Autorità di certificazione di Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="BKMK_CertificateRegistrationPoint"></a> Punto di registrazione certificati  
 Per altre informazioni su come configurare il punto di registrazione certificati, vedere [Introduzione ai profili certificato](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

##  <a name="BKMK_Distribution_Point"></a> Punto di distribuzione  
 Per altre informazioni su come configurare il punto di distribuzione per la distribuzione del contenuto, vedere [Gestire il contenuto e l'infrastruttura del contenuto per System Center Configuration Manager](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 Per altre informazioni su come configurare il punto di distribuzione per le distribuzioni di PXE, vedere [Usare PXE per distribuire Windows in rete con System Center Configuration Manager](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

 Per informazioni su come configurare il punto di distribuzione per le distribuzioni multicast, vedere [Usare il multicast per distribuire Windows in rete con System Center Configuration Manager](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

 **Installa e configura IIS, se richiesto da Configuration Manager**  
 Selezionare questa opzione per consentire a Configuration Manager di installare e configurare IIS sul sistema del sito, se non è già installato. IIS deve essere installato su tutti i punti di distribuzione ed è necessario selezionare questa impostazione per proseguire la procedura guidata.  

 **Account di installazione sistema del sito**  
 Per i punti di distribuzione installati su un server del sito, solo l'account del computer del server del sito viene supportato per l'uso come Account di installazione sistema del sito.  

 **Creare un certificato autofirmato o importare un certificato client PKI**  
 Questo certificato ha due scopi:  

1.  Consente l'autenticazione tra il punto di distribuzione e un punto di gestione prima che il punto di distribuzione invii messaggi di stato.  

2.  Quando l'opzione **Abilita supporto PXE per i client** è selezionata, il certificato viene inviato ai computer che eseguono un avvio PXE in modo che possano connettersi a un punto di gestione durante la distribuzione del sistema operativo.  

Quando tutti i punti di gestione nel sito sono configurati per il protocollo HTTP, è necessario creare un certificato autofirmato. Quando i punti di gestione sono configurati per HTTPS, importare un certificato client PKI.  

Per importare il certificato, cercare un file Public-Key Cryptography Standards #12 (PKCS #12) che contenga un certificato PKI con i requisiti seguenti per Configuration Manager:  

-   Lo scopo designato deve includere l'autenticazione client.  

-   La chiave privata deve essere configurata per l'esportazione.  

Non sono previsti requisiti specifici per il certificato Nome oggetto o Nome alternativo oggetto (SAN) ed è possibile utilizzare lo stesso certificato per più punti di distribuzione.  

Per altre informazioni sui requisiti dei certificati, vedere [Requisiti dei certificati PKI per System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md). Per un esempio di distribuzione di questo certificato, vedere la sezione *Distribuzione del certificato di servizio per i punti di distribuzione* nell'argomento [Esempio dettagliato di distribuzione dei certificati PKI per System Center Configuration Manager: Autorità di certificazione di Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

**Abilita questo punto di distribuzione per il contenuto pre-installato**  
Selezionare questa casella di controllo per abilitare il punto di distribuzione per il contenuto pre-installato. Quando questa casella di controllo è selezionata, è possibile configurare il comportamento della distribuzione del contenuto. È possibile scegliere se pre-installare sempre il contenuto sul punto di distribuzione, se pre-installare il contenuto iniziale per il pacchetto ma usare il normale processo di distribuzione del contenuto in presenza di aggiornamenti oppure se usare sempre il normale processo di distribuzione per il contenuto nel pacchetto.  

**Gruppi di limiti**  
 È possibile associare i gruppi di limiti a un punto di distribuzione. Durante la distribuzione del contenuto, i client devono trovarsi in un gruppo di limiti associato al punto di distribuzione per usarlo come percorso di origine per il contenuto.
 - **Nelle versioni precedenti la 1610** è possibile selezionare la casella di controllo **Consenti percorso origine di fallback per il contenuto** per consentire ai client esterni a questi gruppi di limiti di eseguire il fallback e usare il punto di distribuzione come percorso di origine per il contenuto in assenza di altri punti di distribuzione disponibili.
 - **A partire dalla versione 1610** non è più possibile configurare **Consenti percorso origine di fallback per il contenuto**.  È invece possibile configurare relazioni tra gruppi di limiti che controllano quando un client può iniziare a cercare percorsi di origine del contenuto validi in gruppi di limiti aggiuntivi.

##  <a name="BKMK_Enrollment_Point"></a> Punto di registrazione  
I punti di registrazione vengono usati per installare i computer Mac e registrare i dispositivi gestiti con la funzionalità di gestione dei dispositivi mobili in locale. Per altre informazioni, vedere  

-   [How to deploy clients to Macs in System Center Configuration Manager](../../../../core/clients/deploy/deploy-clients-to-macs.md) (Come distribuire i client nei computer Mac in System Center Configuration Manager)  

-   [Come gli utenti registrano i dispositivi con la gestione di dispositivi mobili locale in System Center Configuration Manager](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

**Connessioni consentite**  
 L'impostazione HTTPS viene selezionata automaticamente e richiede un certificato PKI sul server per l'autenticazione tra server e punto proxy di registrazione o punto di servizio fuori banda e per la crittografia dei dati tramite SSL. Per altre informazioni sui requisiti dei certificati, vedere [Requisiti dei certificati PKI per System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Per un esempio di distribuzione del certificato del server e per informazioni sulla relativa configurazione in Internet Information Services (IIS), vedere la sezione *Distribuzione del certificato del server Web per sistemi del sito che eseguono IIS* in [Esempio dettagliato di distribuzione dei certificati PKI per System Center Configuration Manager: Autorità di certificazione di Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="BKMK_Enrollment_Proxy_Point"></a> Punto proxy di registrazione  
Per altre informazioni su come configurare un punto proxy di registrazione per i dispositivi mobili, vedere [Come gli utenti registrano i dispositivi con la gestione di dispositivi mobili locale in System Center Configuration Manager](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md).  

**Connessioni client**  
 L'impostazione HTTPS viene selezionata automaticamente e richiede un certificato PKI sul server per l'autenticazione tra server e dispositivi mobili o computer Mac registrati da Configuration Manager e per la crittografia dei dati con Secure Sockets Layer (SSL). Per altre informazioni sui requisiti dei certificati, vedere [Requisiti dei certificati PKI per System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

 Per un esempio di distribuzione del certificato del server e per informazioni sulla relativa configurazione in Internet Information Services (IIS), vedere la sezione *Distribuzione del certificato del server Web per sistemi del sito che eseguono IIS* in [Esempio dettagliato di distribuzione dei certificati PKI per System Center Configuration Manager: Autorità di certificazione di Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="BKMK_Fallback_Status_Point"></a> Punto di stato di fallback  
**Numero di messaggi di stato** e **Intervallo di limitazione (in secondi)**  
Sebbene le impostazioni predefinite per queste opzioni (10.000 messaggi di stato e 3.600 secondi per l'intervallo di limitazione) siano sufficienti nella maggior parte dei casi, potrebbe essere necessario modificarli in presenza di entrambe le condizioni seguenti:  

-   Il punto di stato di fallback accetta connessioni solo dalla rete intranet.  

-   Il punto di stato di fallback viene utilizzato durante un'implementazione della distribuzione client per molti computer.  

In questo scenario, un flusso continuo di messaggi di stato può creare un backlog di messaggi di stato che determina un utilizzo elevato della CPU sul server del sito per un periodo di tempo prolungato. Inoltre, potrebbe non essere possibile visualizzare le informazioni aggiornate sulla distribuzione dei client nella console di Configuration Manager e nei report sulla distribuzione dei client.  

Queste impostazioni del punto di stato di fallback sono progettate per essere configurate per messaggi di stato generati durante la distribuzione dei client. Non sono pensate per problemi di comunicazione dei client, come nel caso in cui i client su Internet non riescono a connettersi al punto di gestione basato su Internet. Dal momento che il punto di stato di fallback non può applicare queste impostazioni solo ai messaggi di stato generati durante la distribuzione dei client, non configurarle quando il punto di stato di fallback accetta connessioni da Internet.  

Ciascun computer su cui l'installazione del client di System Center 2012 Configuration Manager viene completata correttamente invia i seguenti quattro messaggi di stato al punto di stato di fallback:  

-   Distribuzione di client avviata  

-   Distribuzione client completata  

-   Assegnazione client avviata  

-   Assegnazione client completata  

I computer sui quali non è possibile eseguire l'installazione o che assegnano il client di Configuration Manager inviano messaggi di stato aggiuntivi.  

Se ad esempio si distribuisce il client di Configuration Manager a 20.000 computer, questa distribuzione può inviare 80.000 messaggi di stato al punto di stato di fallback. Dal momento che la configurazione predefinita della limitazione della larghezza di banda della rete consente l'invio di 10.000 messaggi di stato al punto di stato di fallback ogni 3600 secondi (1 ora), è possibile che i messaggi di stato vengano inclusi nel backlog sul punto di stato di fallback. È inoltre necessario considerare la larghezza di banda della rete disponibile tra il punto di stato di fallback e il server del sito e la potenza di quest'ultimo per l'elaborazione di un numero elevato di messaggi di stato.  

Per evitare questi problemi, prendere in considerazione l'opportunità di aumentare il numero di messaggi di stato e ridurre l'intervallo di limitazione.  

Reimpostare i valori di limitazione per il punto di stato di fallback in presenza di una delle condizioni seguenti:  

-   Si ritiene che i valori di limitazione correnti siano superiori a quelli richiesti per l'elaborazione dei messaggi di stato dal punto di stato di fallback.  

-   Si ritiene che le impostazioni di limitazione correnti determinino un utilizzo elevato della CPU sul server del sito.  

Non modificare le impostazioni di limitazione per il punto di stato di fallback senza aver compreso le conseguenze di tale azione. Ad esempio, se le impostazioni di limitazione vengono aumentate, l'utilizzo della CPU sul server del sito potrebbe crescere contestualmente, rallentando così tutte le operazioni del sito.  

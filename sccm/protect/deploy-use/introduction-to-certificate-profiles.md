---
title: Introduzione ai profili certificato
titleSuffix: Configuration Manager
description: Informazioni sul funzionamento dei profili certificato in System Center Configuration Manager con Servizi certificati Active Directory.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5872a6a8ee69e50d0abfe5840a087aaf83ab7aa5
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156611"
---
# <a name="introduction-to-certificate-profiles-in-system-center-configuration-manager"></a>Introduzione ai profili certificato in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


I profili certificato vengono usati con Servizi certificati Active Directory e il ruolo del servizio Registrazione dispositivi di rete (NDES). È possibile creare e distribuire certificati di autenticazione per i dispositivi gestiti, in modo che gli utenti possano accedere facilmente alle risorse aziendali. Ad esempio, è possibile creare e distribuire profili certificato per fornire i certificati di cui gli utenti hanno bisogno per connettersi a connessioni VPN e wireless.

I profili certificato possono configurare automaticamente i dispositivi utente. Gli utenti accedono alle risorse aziendali, quali reti Wi-Fi e server VPN, senza installare manualmente i certificati o usare un processo fuori banda. I profili certificato contribuiscono a mantenere sicure le risorse aziendali perché vengono usate più impostazioni di sicurezza supportate dall'infrastruttura a chiave pubblica (PKI) dell'azienda. Ad esempio, è possibile richiedere l'autenticazione server per tutte le connessioni Wi-Fi e VPN perché i certificati richiesti sono stati distribuiti nei dispositivi gestiti.   

I profili di certificato forniscono le seguenti funzionalità di gestione:  

-   Registrazione e rinnovo dei certificati di un autorità di certificazione aziendale (CA) per i dispositivi che eseguono iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop e Mobile e Android. Questi certificati possono poi essere usati per le connessioni Wi-Fi e VPN.  

-   Distribuzione di certificati della CA radice attendibili e certificati della CA intermedi. Questi certificati configurano una catena di certificati nei dispositivi per le connessioni VPN e Wi-Fi quando è richiesta l'autenticazione del server.  

-   Monitoraggio e creazione di report per i certificati installati.  

**Esempio:** Tutti i dipendenti devono potersi connettere agli hotspot Wi-Fi in più sedi aziendali. Per consentire agli utenti di connettersi con facilità, distribuire per prima cosa i certificati necessari per la connessione Wi-Fi, quindi distribuire i profili Wi-Fi che fanno riferimento al certificato.  

**Esempio:** si dispone di un'infrastruttura a chiave pubblica (PKI) e si vuole passare a un metodo più flessibile e sicuro di distribuzione dei certificati. Gli utenti devono essere in grado di accedere alle risorse aziendali dai loro dispositivi personali senza compromettere la protezione. Configurare i profili certificato con le impostazioni e i protocolli supportati per la piattaforma per dispositivi specifica. I dispositivi possono quindi richiedere automaticamente questi certificati a un server di registrazione con connessione Internet. Configurare quindi i profili VPN per usare questi certificati, in modo che il dispositivo possa accedere alle risorse aziendali.  



## <a name="types-of-certificate-profiles"></a>Tipi di profili certificato  
 Esistono tre tipi di profilo certificato:  

-   **Certificato CA attendibile**: consente di distribuire un certificato della CA radice attendibile o un certificato della CA intermedio. Questi certificati formano una catena di certificati quando il dispositivo deve eseguire l'autenticazione a un server.  

-   **Simple Certificate Enrollment Protocol (SCEP)**: consente di richiedere un certificato per un dispositivo o un utente usando il protocollo SCEP. Questo tipo richiede il ruolo del servizio Registrazione dispositivi di rete (NDES) in un server che esegue Windows Server 2012 R2 o versione successiva.

    Per creare un profilo certificato di tipo **Simple Certificate Enrollment Protocol (SCEP)**, creare prima un profilo **Certificato CA attendibile**.

-   **Scambio di informazioni personali (PFX)**: consente di richiedere un certificato PFX (noto anche come PKCS #12) per un dispositivo o un utente.<!--1321368-->  

    Per l'elaborazione delle richieste, è possibile creare profili certificato PFX tramite [importazione delle credenziali](/sccm/mdm/deploy-use/import-pfx-certificate-profiles) da certificati esistenti o tramite [definizione di una CA](/sccm/mdm/deploy-use/create-pfx-certificate-profiles).

    > [!Note]  
    > Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Abilitare le funzionalità facoltative degli aggiornamenti](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

    A partire dalla versione 1706, è possibile usare Microsoft o Entrust come CA per i certificati di **scambio di informazioni personali (PFX)**.


## <a name="requirements-and-supported-platforms"></a>Requisiti e piattaforme supportate  
Per distribuire i profili certificato che usano SCEP, installare il punto di registrazione certificati in un server del sistema del sito. Installare anche un modulo criteri per il servizio Registrazione dispositivi di rete (NDES), il Modulo criteri di Configuration Manager, in un server che esegue Windows Server 2012 R2 o versione successiva. Questo server richiede il ruolo Servizi certificati Active Directory e NDES attivo e accessibile per i dispositivi che richiedono i certificati. Per i dispositivi registrati da Microsoft Intune, NDES deve essere accessibile da Internet, ad esempio in una rete perimetrale.  

Anche i certificati PFX richiedono un punto di registrazione certificati. Specificare inoltre la CA per il certificato e le credenziali di accesso pertinenti. A partire dalla versione 1706, è possibile specificare Microsoft o Entrust come CA.  

Per altre informazioni sul modo in cui il servizio Registrazione dispositivi di rete supporta moduli criteri per consentire la distribuzione di certificati da parte di Configuration Manager, vedere [Uso di un modulo criteri con il servizio Registrazione dispositivi di rete](http://go.microsoft.com/fwlink/p/?LinkId=328657).  

A seconda dei requisiti, Configuration Manager supporta la distribuzione dei certificati in più archivi certificati in diversi tipi di dispositivi e sistemi operativi. Sono supportati i dispositivi e i sistemi operativi seguenti:  

-   Windows RT 8.1  

-   Windows 8.1  

-   Windows Phone 8.1  

-   Windows 10 Desktop e Mobile  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  Per distribuire i profili nei dispositivi Android, iOS, Windows Phone e nei dispositivi registrati Windows 8.1 o versioni successive, tali dispositivi devono essere [registrati in Microsoft Intune](/intune/device-enrollment).   

Uno scenario tipico per Configuration Manager consiste nell'installazione di certificati della CA radice attendibili per autenticare i server Wi-Fi e VPN quando la connessione usa i protocolli di autenticazione EAP-TLS, EAP-TTLS e PEAP e i protocolli di tunneling VPN IKEv2, L2TP/IPsec e Cisco IPsec.  

Un certificato della CA radice aziendale deve essere installato nel dispositivo prima che il dispositivo possa richiedere i certificati usando un profilo certificato SCEP.  

È possibile specificare le impostazioni in un profilo certificato SCEP per richiedere certificati personalizzati per diversi ambienti o requisiti di connettività. La **Creazione guidata profilo certificato** ha due pagine per i parametri di registrazione. La prima, **Registrazione SCEP**, include le impostazioni per la richiesta di registrazione e la posizione in cui installare il certificato. Il secondo, **Proprietà certificato**, descrive il certificato richiesto stesso.  

## <a name="deploying-certificate-profiles"></a>Distribuzione di profili certificato  
 Quando si distribuisce un profilo certificato, i file certificato contenuti nel profilo vengono installati nei dispositivi client. Vengono distribuiti anche tutti i parametri SCEP e le richieste SCEP sono elaborate nel dispositivo client. È possibile distribuire i profili certificato nelle raccolte utenti o dispositivi e specificare l'archivio di destinazione per ogni certificato. Le regole di applicabilità determinano se i certificati possono essere installati nel dispositivo. Quando i profili certificato vengono distribuiti nelle raccolte utenti, l'affinità utente-dispositivo stabilisce quale dei dispositivi degli utenti installa i certificati. Quando i profili certificato che includono i certificati utente vengono distribuiti nelle raccolte dispositivi, per impostazione predefinita i certificati vengono installati in tutti i dispositivi primari degli utenti. Nella pagina **Registrazione SCEP** della **Creazione guidata profilo certificato** è possibile modificare questo comportamento per installare il certificato in tutti i dispositivi degli utenti. Se i dispositivi sono computer del gruppo di lavoro, i certificati utente non verranno distribuiti.  

## <a name="monitoring-certificate-profiles"></a>Monitoraggio dei profili certificato  

È possibile monitorare le distribuzioni dei profili certificato visualizzando i risultati o i report di conformità. Questi approcci sono descritti in [Come monitorare i profili certificato](/sccm/protect/deploy-use/monitor-certificate-profiles).


## <a name="automatic-revocation-of-certificates"></a>Revoca automatica dei certificati  
 System Center Configuration Manager revoca automaticamente i certificati utente e computer che sono stati distribuiti usando profili certificato nelle seguenti circostanze:  

- Il dispositivo è stato ritirato dalla gestione di System Center Configuration Manager.  

- Il dispositivo è stato cancellato in modo selettivo.  

- Il dispositivo è stato bloccato dalla gerarchia di System Center Configuration Manager.  

  Per revocare i certificati, il server del sito invia un comando di revoca all'autorità di certificazione emittente. Il motivo della revoca è **Termine operazione**.  

---
title: Introduzione ai profili certificato | Microsoft Docs
description: Informazioni sul funzionamento dei profili certificato in System Center Configuration Manager con Servizi certificati Active Directory.
ms.custom: na
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 41dcc259-f147-4420-bff2-b65bdf8cff77
caps.latest.revision: 7
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 8a5dc7361da34f3e6b926acd35c72c0c0767ce70
ms.openlocfilehash: d51670b47aab77cc4e630a6aeaa0744f916bf3b9


---
# <a name="introduction-to-certificate-profiles-in-system-center-configuration-manager"></a>Introduzione ai profili certificato in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


I profili certificato vengono usati con Servizi certificati Active Directory e il ruolo Servizio registrazione dispositivi di rete per effettuare il provisioning dei certificati di autenticazione per i dispositivi gestiti, in modo che gli utenti possano accedere facilmente alle risorse aziendali. Ad esempio, è possibile creare e distribuire profili certificato per fornire i certificati di cui gli utenti hanno bisogno per avviare connessioni VPN e wireless. 

I profili certificato possono configurare automaticamente i dispositivi utente per accedere alle risorse aziendali, quali reti Wi-Fi e server VPN, senza dover installare manualmente i certificati o usare un processo fuori banda. I profili certificato possono inoltre mantenere sicure le risorse aziendali perché vengono usate più impostazioni di sicurezza supportate dall'infrastruttura a chiave pubblica (PKI) dell'azienda. Ad esempio, è possibile richiedere l'autenticazione server per tutte le connessioni Wi-Fi e VPN perché è stato effettuato il provisioning dei certificati richiesti nei dispositivi gestiti.   

I profili di certificato forniscono le seguenti funzionalità di gestione:  

-   Registrazione e rinnovo dei certificati di un autorità di certificazione aziendale (CA) per i dispositivi che eseguono iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop e Mobile e Android. Questi certificati possono poi essere usati per le connessioni Wi-Fi e VPN.  

-   Distribuzione di certificati CA radice attendibili e certificati CA intermedi per configurare una catena di certificati nei dispositivi per le connessioni VPN e Wi-Fi quando è richiesta l'autenticazione del server.  

-   Monitoraggio e creazione di report per i certificati installati.  

**Esempio:** Tutti i dipendenti devono potersi connettere agli hotspot Wi-Fi in più sedi aziendali. Distribuzione dei certificati necessari per la connessione Wi-Fi e distribuzione dei profili Wi-Fi che fanno riferimento al certificato per consentire agli utenti di connettersi senza problemi.  

**Esempio:** Si dispone di una PKI e si desidera spostare a un metodo più flessibile e sicuro di provisioning di certificati che consente agli utenti accedere alle risorse aziendali dai loro dispositivi personali senza compromettere la protezione. Configurare i profili certificato con le impostazioni e i protocolli supportati per la piattaforma per dispositivi specifica. I dispositivi possono quindi richiedere automaticamente questi certificati a un server di registrazione con connessione Internet. Configurare quindi i profili VPN per usare questi certificati, in modo che il dispositivo possa accedere alle risorse aziendali.  

## <a name="types-of-certificate-profiles"></a>Tipi di profili certificato  
 Esistono tre tipi di profilo certificato:  

-   **Certificato CA attendibile** : consente di distribuire un certificato della CA radice attendibile o un certificato CA intermedio in modo da formare una catena di certificati quando il dispositivo deve eseguire l'autenticazione a un server.  

-   **Simple Certificate Enrollment Protocol (SCEP)**: consente di richiedere un certificato per un dispositivo o un utente usando il protocollo SCEP e il servizio Registrazione dispositivi di rete in un server che esegue Windows Server 2012 R2.
-   -   **Personal Information Exchange (PFX)**: consente di richiedere un certificato PFX (noto anche come PKCS #12) per un dispositivo o un utente.

    > [!NOTE]  
    >  È necessario creare un profilo certificato del tipo **Certificato CA attendibile** prima di poter creare un profilo certificato di tipo **Simple Certificate Enrollment Protocol (SCEP)**.  

## <a name="requirements-and-supported-platforms"></a>Requisiti e piattaforme supportate  
 Per distribuire i profili certificato che usano SCEP, è necessario installare il punto di registrazione del certificato in un server del sistema del sito nel sito di amministrazione centrale o in un sito primario. È anche necessario installare un modulo criteri per il servizio Registrazione dispositivi di rete (NDES), il Modulo criteri di Configuration Manager, in un server che esegue Windows Server 2012 R2 con il ruolo Servizi certificati Active Directory e NDES attivo e accessibile per i dispositivi che richiedono i certificati. Per i dispositivi registrati da Microsoft Intune, NDES deve essere accessibile da Internet, ad esempio in una rete perimetrale.  

 Per altre informazioni sul modo in cui il servizio Registrazione dispositivi di rete supporta moduli criteri per consentire la distribuzione di certificati da parte di Configuration Manager, vedere [Uso di un modulo criteri con il servizio Registrazione dispositivi di rete](http://go.microsoft.com/fwlink/p/?LinkId=328657).  

 Configuration Manager supporta la distribuzione dei certificati in più archivi di certificati, a seconda dei requisiti, del tipo di dispositivo e del sistema operativo. Sono supportati i dispositivi e i sistemi operativi seguenti:  

-   Windows RT 8.1  

-   Windows 8.1  

-   Windows Phone 8.1  

-   Windows 10 Desktop e Mobile  

-   iOS  

-   Android  

> [!IMPORTANT]  
>  Per distribuire i profili nei dispositivi Android, iOS, Windows Phone e nei dispositivi registrati Windows 8.1 o versioni successive, tali dispositivi devono essere [registrati in Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).   

Uno scenario tipico per System Center Configuration Manager è di installare i certificati CA radice trusted per autenticare i server Wi-Fi e VPN quando la connessione usa i protocolli di autenticazione EAP-TLS, EAP-TTLS e PEAP e i protocolli di tunneling VPN IKEv2, L2TP/IPsec e Cisco IPsec.  

È necessario garantire che un certificato CA radice aziendale sia installato nel dispositivo prima che il dispositivo possa richiedere i certificati usando un profilo certificato SCEP.  

È possibile specificare una serie di impostazioni in un profilo certificato SCEP per richiedere certificati personalizzati per diversi ambienti o i requisiti di connettività. La **Creazione guidata profilo certificato** contiene due pagine per i parametri di registrazione. Il primo, **Registrazione SCEP**, contiene le impostazioni per la richiesta di registrazione e la posizione in cui installare il certificato. Il secondo, **Proprietà certificato**, descrive il certificato richiesto stesso.  

## <a name="deploying-certificate-profiles"></a>Distribuzione di profili certificato  
 Quando si distribuisce un profilo certificato, i file certificato contenuti nel profilo vengono installati nei dispositivi client. Verranno distribuiti anche tutti i parametri SCEP e le richieste SCEP verranno elaborate nel dispositivo client. È possibile distribuire i profili certificato nelle raccolte utenti o dispositivi e specificare l'archivio di destinazione per ogni certificato. Le regole di applicabilità determinano se i certificati possono essere installati nel dispositivo. Quando i profili certificato vengono distribuiti nelle raccolte utenti, l'affinità dispositivo utente stabilisce quale dei dispositivi degli utenti installerà i certificati. Quando i profili certificato che contengono i certificati utente vengono distribuiti nelle raccolte dispositivi, per impostazione predefinita i certificati verranno installati in tutti i dispositivi primari degli utenti. Nella pagina **Registrazione SCEP** della **Creazione guidata profilo certificato** è possibile modificare questo comportamento per installare il certificato in tutti i dispositivi degli utenti. Inoltre, i certificati utente non verranno distribuiti nei dispositivi se sono computer del gruppo di lavoro.  

## <a name="monitoring-certificate-profiles"></a>Monitoraggio dei profili certificato  

È possibile monitorare le distribuzioni dei profili certificato visualizzando i risultati o i report di conformità. Questi approcci sono descritti in [Come monitorare i profili certificato](/sccm/protect/deploy-use/monitor-certificate-profiles).


## <a name="automatic-revocation-of-certificates"></a>Revoca automatica dei certificati  
 System Center Configuration Manager revoca automaticamente i certificati utente e computer che sono stati distribuiti usando profili certificato nelle seguenti circostanze:  

-   Il dispositivo è stato ritirato dalla gestione di System Center Configuration Manager.  

-   Il dispositivo è stato cancellato in modo selettivo.  

-   Il dispositivo è stato bloccato dalla gerarchia di System Center Configuration Manager.  

 Per revocare i certificati, il server del sito invia un comando di revoca all'autorità di certificazione emittente. Il motivo della revoca è **Termine operazione**.  



<!--HONumber=Dec16_HO5-->



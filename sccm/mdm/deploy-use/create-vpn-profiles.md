---
title: Profili VPN in System Center Configuration Manager | Microsoft Docs
description: Profili VPN nei dispositivi mobili in System Center Configuration Manager.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
caps.latest.revision: 18
caps.handback.revision: 0
author: lleonard-msft
ms.author: alleonar
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 699b79b68440b61904a9053e5004318a2a248bfd
ms.openlocfilehash: 8adc41a30bf12a91a272029db49e50ba003d3e9c
ms.lasthandoff: 04/25/2017

---
# <a name="vpn-profiles-on-mobile-devices-in-system-center-configuration-manager"></a>Profili VPN nei dispositivi mobili in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare profili VPN in System Center Configuration Manager per distribuire impostazioni VPN agli utenti dei dispositivi mobili nell'organizzazione. La distribuzione di queste impostazioni consente di ridurre al minimo le operazioni che l'utente finale deve eseguire per connettersi alle risorse nella rete aziendale.  

 Ad esempio, si supponga di voler effettuare il provisioning di tutti i dispositivi che eseguono il sistema operativo iOS con le impostazioni necessarie per connettersi a una condivisione file nella rete aziendale. È possibile creare un profilo VPN contenente le impostazioni necessarie per connettersi alla rete aziendale e quindi distribuire questo profilo a tutti gli utenti della gerarchia che dispongono di dispositivi iOS. Gli utenti dei dispositivi iOS visualizzeranno la connessione VPN nell'elenco delle reti disponibili e potranno connettersi molto facilmente alla rete.  

 Quando si crea un profilo VPN, è possibile includere un'ampia gamma di impostazioni di protezione, inclusi i certificati per la convalida server e l'autenticazione client per i quali è stato eseguito il provisioning usando profili certificato in Configuration Manager. Per altre informazioni sui profili certificato, vedere [Profili certificato in System Center Configuration Manager](../../protect/deploy-use/introduction-to-certificate-profiles.md).  

 ## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>Profili VPN usando Configuration Manager insieme a Intune

 Per distribuire i profili nei dispositivi Android, iOS, Windows Phone e Windows 8.1, tali dispositivi devono essere registrati in Microsoft Intune. Anche i dispositivi su altre piattaforme possono essere registrati in Intune. Per informazioni su come eseguire la registrazione, vedere [Gestire i dispositivi mobili con Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx). Questa tabella indica il tipo di connessione supportato per ogni piattaforma del dispositivo:  

 |Tipo di connessione|iOS e Mac OS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop e Mobile|  
 |---------------------|----------------------|-------------|-----------------|----------------|--------------------|-----------------------|-----------------------------------|  
 |Cisco AnyConnect|Sì|Sì|No|No|No|No|Sì (URI OMA)|  
 |Pulse Secure|Sì|Sì|Sì|No|Yes|Sì|Sì|  
 |F5 Edge Client|Yes|Sì|Sì|No|Yes|Sì|Yes|  
 |Dell SonicWALL Mobile Connect|Sì|Sì|Sì|No|Yes|Sì|Sì|  
 |VPN mobile Check Point|Sì|Sì|Sì|No|Yes|Sì|Sì|  
 |Microsoft SSL (SSTP)|No|No|Yes|Sì|Sì|No|No|  
 |Microsoft Automatico|No|No|Yes|Sì|Sì|No|Sì (URI OMA)|  
 |IKEv2|Sì (Criteri personalizzati)|No|Yes|Sì|Sì|Sì|Sì (URI OMA)|  
 |PPTP|Sì|No|Yes|Sì|Sì|No|Sì (URI OMA)|  
 |L2TP|Sì|No|Yes|Sì|Sì|No|Sì (URI OMA)|  

## <a name="create-vpn-profiles"></a>Creare profili VPN
Per informazioni generali sulla creazione dei profili VPN, vedere [Come creare profili VPN in System Center Configuration Manager](../../protect/deploy-use/create-vpn-profiles.md).

###   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Funzionalità VPN di Windows 10 disponibili quando si usa Configuration Manager con Intune  


> [!NOTE]  
> Il nome di un profilo VPN che usa le funzionalità VPN di Windows 10 non può essere in formato unicode né contenere caratteri speciali.


|Opzione|Altre informazioni|Tipo di connessione|  
    |------------|----------------------|---------------------|  
    |**Disabilita VPN quando il dispositivo è connesso alla rete Wi-Fi aziendale**|La connessione VPN non verrà usata quando il dispositivo è connesso alla rete Wi-Fi aziendale. Immettere il nome di rete attendibile, usato per determinare se il dispositivo è connesso alla rete aziendale.|All|  
    |**Regole del traffico di rete**|Impostare i protocolli e gli intervalli di porte e indirizzi locali e remoti che verranno abilitati per la connessione VPN.<br /><br /> **Nota:** se non si crea una regola del traffico di rete, tutti i protocolli, le porte e gli intervalli di indirizzi vengono abilitati. Dopo aver creato una regola, solo i protocolli, le porte e gli intervalli di indirizzi specificati in tale regola o nelle regole aggiuntive verranno usati dalla connessione VPN.|All|  
    |**Route**|Specifica le route che verranno usate dalla connessione VPN. Si noti che la creazione di più di 60 route può causare errori del criterio. |All|  
    |**Server DNS**|Specifica i server DNS che vengono usati dalla connessione VPN una volta stabilita la connessione.|All|  
    |**App in grado di connettersi automaticamente alla rete VPN**|È possibile aggiungere app o importare elenchi di app che useranno automaticamente la connessione VPN. Il tipo di app determinerà l'identificatore dell'app. Per un'app desktop, specificare il percorso file dell'app. Per un'app universale, specificare il nome della famiglia di pacchetti (PFN). Per sapere come individuare il nome PFN per un'app, vedere la sezione relativa al [reperimento di un nome di famiglia di pacchetti per la VPN per app](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md). |All|

> [!IMPORTANT]
> Si consiglia di proteggere tutti gli elenchi di app associate che si compilano per l'uso nella configurazione della VPN per app. Se l'elenco viene modificato da un utente non autorizzato e viene importato nell'elenco di app della VPN per app, si autorizza potenzialmente l'accesso alla VPN da parte di applicazioni che non devono potervi accedere. Un modo per proteggere gli elenchi di app consiste nell'usare un elenco di controllo di accesso (ACL).


1.  Nella pagina **Metodo di autenticazione** della procedura guidata specificare:  

    -   **Metodo di autenticazione**: selezionare il tipo di metodo di autenticazione che verrà usato dalla connessione VPN. I metodi disponibili variano a seconda del tipo di connessione come illustrato in questa tabella.  

        |Metodo di autenticazione|Tipi di &nbsp;connessione&nbsp; supportati|  
        |---------------------------|--------------------------------|  
        |**Certificati**<br /><br /> **Note:**<br />- Se il certificato client esegue l'autenticazione in un server RADIUS, ad esempio un server dei criteri di rete, è necessario impostare il nome alternativo del soggetto nel certificato sul nome dell'entità utente.<br/><br />- Per le distribuzioni Android, selezionare l'identificatore EKU e il valore hash di identificazione personale dell'autorità di certificazione.  In caso contrario, gli utenti devono selezionare il certificato appropriato manualmente.  |- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
        |**Nome utente e password**|- Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
        |**Microsoft EAP-TTLS**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatico<br /><br /> - PPTP<br /><br /> - IKEv2<br /><br /> - L2TP|  
        |**Microsoft PEAP (Protected EAP)**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatico<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Password protetta Microsoft (EAP-MSCHAP v2)**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatico<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Smart card o altro certificato**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatico<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**MSCHAP v2**|-  Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatico<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**RSA SecurID** (solo iOS)|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatico<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Usa certificati computer**|IKEv2|  

         A seconda delle opzioni selezionate, potrebbe essere necessario specificare altre informazioni, ad esempio:  

        -   **Memorizza le credenziali utente a ogni accesso**: le credenziali utente vengono memorizzate in modo che l'utente non debba immetterle ogni volta che si connette.  

        -   **Selezionare un certificato client per l'autenticazione client**: selezionare il [certificato SCEP](create-pfx-certificate-profiles.md) client creato in precedenza che verrà usato per autenticare la connessione VPN.   

            > [!NOTE]  
            >  Per i dispositivi iOS, il profilo SCEP selezionato verrà incorporato nel profilo VPN. Per altre piattaforme, viene aggiunta una regola di applicabilità per garantire che il profilo VPN non venga installato se il certificato non è presente o non è conforme.  
            >   
            >  Se il certificato SCEP specificato non è conforme o non è stato distribuito, il profilo VPN non verrà installato nel dispositivo.
            >  
            >  I dispositivi che eseguono iOS supportano solo RSA SecurID e MSCHAP v2 per il metodo di autenticazione quando il tipo di connessione è PPTP. Per evitare la segnalazione di errori, distribuire un profilo VPN PPTP distinto nei dispositivi che eseguono iOS.  

        - **Accesso condizionale**
            - Scegliere **Abilita l'accesso condizionale per questa connessione VPN** per garantire che prima della connessione i dispositivi che si connettono alla rete VPN siano stati sottoposti a test di conformità all'accesso condizionale. I criteri di conformità sono descritti in [Criteri di conformità del dispositivo in System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/device-compliance-policies.md)
            - Scegliere **Abilita l'accesso Single Sign-On (SSO) con il certificato alternativo** per scegliere un certificato diverso dal certificato di autenticazione VPN per la conformità del dispositivo. Se si sceglie questa opzione, specificare **EKU** (elenco delimitato da virgole) e **Hash dell'emittente** per ottenere il certificato corretto che il client VPN deve individuare.

         - **Windows Information Protection**: fornire l'identità aziendale gestita dall'organizzazione, che corrisponde in genere al dominio primario dell'organizzazione, ad esempio *contoso.com*. È possibile specificare più domini di proprietà dell'organizzazione separandoli con il carattere "|". Ad esempio, *contoso.com|newcontoso.com*.   
              Per informazioni su Windows Information Protection, vedere [Creare un criterio di Windows Information Protection (WIP) con Microsoft Intune](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/create-wip-policy-using-intune).   

         ![Configurare l'accesso condizionale per VPN](media/vpn-conditional-access.png)

         Se è supportato dalla versione di Windows che esegue Configuration Manager _e_ dal metodo di autorizzazione selezionati, è possibile fare clic su **Configura** per aprire la finestra di dialogo delle proprietà di Windows e configurare le proprietà del metodo di autenticazione.  Se l'opzione **Configura** è disabilitata, usare modi alternativi per configurare le proprietà del metodo di autenticazione.

2.  Nella pagina **Impostazioni proxy** di **Creazione guidata profilo VPN**, selezionare la casella di controllo **Configura impostazioni proxy per questo profilo VPN** se la connessione VPN in uso usa un server proxy. Quindi, specificare le informazioni relative al server proxy. Per altre informazioni, vedere la documentazione di Windows Server.  

    > [!NOTE]  
    >  Nei computer Windows 8.1, il profilo VPN non visualizzerà le informazioni sul proxy finché l'utente non si connette alla rete VPN con tale computer.  


3. Configurare altre impostazioni DNS (se necessario)  
 Nella pagina **Configura connessione VPN automatica** è possibile configurare quanto segue:  

    -   **Abilita VPN su richiesta**: usare questa opzione per configurare altre impostazioni DNS per i dispositivi Windows Phone 8.1. Questa impostazione si applica solo ai dispositivi Windows Phone 8.1 e deve essere abilitata solo nei profili VPN che verranno distribuiti a dispositivi Windows Phone 8.1.

    -   Elenco dei suffissi DNS (solo per i dispositivi Windows Phone 8.1): consente di configurare i domini che stabiliranno una connessione VPN. Per ogni dominio specificato, aggiungere il suffisso DNS, l'indirizzo del server DNS e una delle azioni su richiesta seguenti:  

        -   **Non stabilire mai**: non viene mai aperta una connessione VPN  

        -   **Stabilisci se necessario**: viene aperta una connessione VPN solo se il dispositivo deve connettersi alle risorse  

        -   **Stabilisci sempre**: viene aperta sempre la connessione VPN  

    -   **Unisci**: eventuali suffissi DNS configurati vengono copiati nell'**Elenco reti attendibili**.  

    -   **Elenco reti attendibili** (solo per i dispositivi Windows Phone 8.1): viene specificato un suffisso DNS per ogni riga. Se il dispositivo è in una rete attendibile, la connessione VPN non verrà aperta.  

    -   **Elenco ricerca suffissi** (solo per i dispositivi Windows Phone 8.1): viene specificato un suffisso DNS per ogni riga. Per cercare ogni suffisso DNS durante la connessione a un sito Web verrà usato un nome breve.  

     Ad esempio, si può specificare i suffissi DNS **domain1.contoso.com** e **domain2.contoso.com** , indicando come URL **http://mywebsite**. Verranno quindi cercati i seguenti indirizzi:  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

    > [!NOTE]  
    >  Solo per i dispositivi Windows Phone 8.1  
    >   
    >  Se è selezionata l'opzione **Invia tutto il traffico di rete tramite la connessione VPN** e la connessione VPN usa il tunneling completo, per il primo profilo sottoposto a provisioning nel dispositivo, la connessione VPN verrà aperta automaticamente. Se si desidera un profilo diverso per aprire automaticamente una connessione, è necessario renderlo il profilo predefinito nel dispositivo.  
    >   
    >  Se non è selezionata l'opzione **Invia tutto il traffico di rete tramite la connessione VPN** e la connessione VPN usa lo split tunneling, può essere aperta una connessione VPN automaticamente se si configurano le route o un suffisso DNS specifico per la connessione.  


4. Nella pagina **Piattaforme supportate** della **Creazione guidata profilo VPN**, selezionare i sistemi operativi in cui il profilo VPN verrà installato o fare clic su **Seleziona tutto** per installare il profilo VPN in tutti i sistemi operativi disponibili.  

5. Completare la procedura guidata. Il nuovo profilo VPN viene visualizzato nel nodo **Profili VPN** dell'area di lavoro **Asset e conformità** .  


**Distribuire:** per informazioni sulla distribuzione dei profili VPN, vedere [Distribuire profili in System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

### <a name="next-steps"></a>Passaggi successivi  
 Usare gli argomenti seguenti per pianificare, configurare, far funzionare e gestire i profili VPN in Configuration Manager.  

-   [Prerequisiti per i profili VPN in System Center Configuration Manager](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Sicurezza e privacy per i profili VPN in System Center Configuration Manager](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)


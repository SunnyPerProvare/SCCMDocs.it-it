---
title: Profili VPN
titleSuffix: Configuration Manager
description: Profili VPN nei dispositivi mobili in System Center Configuration Manager.
ms.custom: na
ms.date: 07/26/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45388103-2410-4c7e-b4cf-73a1bda485fc
caps.latest.revision: "18"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: 40446ce656bd446f890b9b1349ab0b95742cadb8
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="vpn-profiles-on-mobile-devices-in-system-center-configuration-manager"></a>Profili VPN nei dispositivi mobili in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare profili VPN in System Center Configuration Manager per distribuire impostazioni VPN agli utenti dei dispositivi mobili nell'organizzazione. La distribuzione di queste impostazioni consente di ridurre al minimo le operazioni che l'utente finale deve eseguire per connettersi alle risorse sulla rete aziendale.  

 Si supponga, ad esempio, di voler configurare tutti i dispositivi che eseguono il sistema operativo iOS usando le impostazioni necessarie per connettersi a una condivisione file nella rete aziendale. È possibile creare un profilo VPN contenente le impostazioni necessarie per connettersi alla rete aziendale e quindi distribuire questo profilo a tutti gli utenti della gerarchia che dispongono di dispositivi iOS. Gli utenti dei dispositivi iOS visualizzeranno la connessione VPN nell'elenco delle reti disponibili e potranno connettersi molto facilmente alla rete.  

 Quando si crea un profilo VPN, è possibile includere una vasta gamma di impostazioni di protezione. È ad esempio possibile specificare certificati per la convalida del server e l'autenticazione del client impostati usando i profili di certificato di System Center Configuration Manager. Per altre informazioni sui profili di certificato, vedere [Profili certificato in System Center Configuration Manager](../../protect/deploy-use/introduction-to-certificate-profiles.md).  

 ## <a name="vpn-profiles-when-using-configuration-manager-together-with-intune"></a>Profili VPN usando Configuration Manager insieme a Intune

 Per distribuire i profili nei dispositivi Android, iOS, Windows Phone e Windows 8.1, tali dispositivi devono essere registrati in Microsoft Intune. Anche i dispositivi su altre piattaforme possono essere registrati in Intune. Per informazioni su come eseguire la registrazione, vedere [Gestire i dispositivi mobili con Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx). La tabella seguente mostra il tipo di connessione supportato per ogni piattaforma del dispositivo:  

 |Tipo di connessione|iOS e MacOS X|Android|Windows 8.1|Windows RT|Windows RT 8.1|Windows Phone 8.1|Windows 10 Desktop e Mobile|  
 |---------------------|----------------------|-------------|-----------------|----------------|--------------------|-----------------------|-----------------------------------|  
 |Cisco AnyConnect|Sì|Sì|No|No|No|No|Sì|
 |Cisco (IPSec)|Solo iOS|No|No|No|No|No|No|  
 |Pulse Secure|Sì|Sì|Sì|No|Yes|Sì|Sì|  
 |F5 Edge Client|Yes|Sì|Sì|No|Yes|Sì|Yes|  
 |Dell SonicWALL Mobile Connect|Sì|Sì|Sì|No|Yes|Sì|Sì|  
 |VPN mobile Check Point|Sì|Sì|Sì|No|Yes|Sì|Sì|  
 |Microsoft SSL (SSTP)|No|No|Yes|Sì|Sì|No|No|  
 |Microsoft Automatico|No|No|Yes|Sì|Sì|No|Sì|  
 |IKEv2|Sì (criteri personalizzati iOS 9 e versioni successive)|No|Yes|Sì|Sì|Sì|Sì|  
 |PPTP|Sì|No|Yes|Sì|Sì|No|Sì|  
 |L2TP|Sì|No|Yes|Sì|Sì|No|Sì (URI OMA)|  

## <a name="create-vpn-profiles"></a>Creare profili VPN
Per informazioni generali sulla creazione di profili VPN, vedere [Come creare profili VPN in System Center Configuration Manager](../../protect/deploy-use/create-vpn-profiles.md).

## <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Funzionalità VPN di Windows 10 disponibili quando si usa Configuration Manager con Intune  


> [!NOTE]  
> Il nome di un profilo VPN che usa le funzionalità VPN di Windows 10 non può essere in formato Unicode né contenere caratteri speciali.


|Opzione|Altre informazioni|Tipo di connessione|  
    |------------|----------------------|---------------------|  
    |**Disabilita VPN quando il dispositivo è connesso alla rete Wi-Fi aziendale**|La connessione VPN non verrà usata quando il dispositivo è connesso alla rete Wi-Fi aziendale. Immettere il nome di rete attendibile usato per determinare se il dispositivo è connesso alla rete aziendale.|All|  
    |**Regole del traffico di rete**|Impostare i protocolli, la porta locale, la porta remota e gli intervalli di indirizzi che verranno abilitati per la connessione VPN.<br /><br /> **Nota:** se non si crea una regola del traffico di rete, tutti i protocolli, le porte e gli intervalli di indirizzi vengono abilitati. Dopo la creazione di una regola, verranno usati dalla connessione VPN solo i protocolli, le porte e gli intervalli di indirizzi specificati in tale regola o nelle regole aggiuntive.|All|  
    |**Route**|Route che verranno usate dalla connessione VPN. Si noti che la creazione di più di 60 route può causare errori del criterio. |All|  
    |**Server DNS**|Server DNS usati dalla connessione VPN una volta stabilita la connessione.|All|  
    |**App in grado di connettersi automaticamente alla rete VPN**|È possibile aggiungere app o importare elenchi di app che useranno automaticamente la connessione VPN. Il tipo di app determinerà l'identificatore dell'app. Per un'app desktop, specificare il percorso file dell'app. Per un'app universale, specificare il nome della famiglia di pacchetti (PFN). Per sapere come individuare il nome PFN per un'app, vedere la sezione relativa al [reperimento di un nome di famiglia di pacchetti per la VPN per app](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md). |All|

> [!IMPORTANT]
> Si consiglia di proteggere tutti gli elenchi di app associate che si compilano per l'uso nella configurazione della VPN per app. Se l'elenco viene modificato da un utente non autorizzato e viene importato nell'elenco di app della VPN per app, si autorizza potenzialmente l'accesso alla VPN da parte di applicazioni che non devono potervi accedere. Un modo per proteggere gli elenchi di app consiste nell'usare un elenco di controllo di accesso (ACL).


1.  Nella pagina **Metodo di autenticazione** della procedura guidata specificare:  

    -   **Metodo di autenticazione**: selezionare il tipo di metodo di autenticazione che verrà usato dalla connessione VPN. I metodi disponibili variano a seconda del tipo di connessione come illustrato in questa tabella.  

        |Metodo di autenticazione|Tipi di &nbsp;connessione&nbsp; supportati|  
        |---------------------------|--------------------------------|  
        |**Certificati**<br /><br /> **Note:**<ul><li>Se il certificato client esegue l'autenticazione in un server RADIUS, ad esempio un server dei criteri di rete, il nome alternativo del soggetto nel certificato deve essere impostato sul nome dell'entità utente.</li><li>Per le distribuzioni Android, selezionare l'identificatore EKU e il valore hash di identificazione personale dell'autorità di certificazione.  In caso contrario, gli utenti devono selezionare il certificato appropriato manualmente.</li></ul>  |<ul><li>Cisco AnyConnect</li><li>Pulse Secure</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> VPN mobile Check Point</li></ul>|  
        |**Nome utente e password**|<ul><li>Pulse Secure</li><li>F5 Edge Client</li><li>Dell SonicWALL Mobile Connect</li><li> VPN mobile Check Point</li></ul>|  
        |**Microsoft EAP-TTLS**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatico</li><li>PPTP</li><li>IKEv2</li><li>L2TP</li></ul>|  
        |**Microsoft PEAP (Protected EAP)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatico</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**Password protetta Microsoft (EAP-MSCHAP v2)**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatico</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**Smart card o altro certificato**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatico</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**MSCHAP v2**|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatico</li><li>IKEv2</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**RSA SecurID** (solo iOS)|<ul><li>Microsoft SSL (SSTP)</li><li>Microsoft Automatico</li><li>PPTP</li><li>L2TP</li></ul>|  
        |**Usa certificati computer**|<ul><li>IKEv2</li></ul>|  

         A seconda delle opzioni selezionate, potrebbe essere necessario specificare altre informazioni, ad esempio:  

        -   **Memorizza le credenziali utente a ogni accesso**: le credenziali utente vengono memorizzate in modo che gli utenti non debbano immetterle ogni volta che si connettono.  

        -   **Selezionare un certificato client per l'autenticazione client**: selezionare il [certificato SCEP](create-pfx-certificate-profiles.md) creato in precedenza che verrà usato per autenticare la connessione VPN.   

            > [!NOTE]  
            >  Per i dispositivi iOS, il profilo SCEP selezionato verrà incorporato nel profilo VPN. Per altre piattaforme, viene aggiunta una regola di applicabilità per garantire che il profilo VPN non venga installato se il certificato non è presente o non è conforme.  
            >   
            >  Se il certificato SCEP specificato non è conforme o non è stato distribuito, il profilo VPN non verrà installato nel dispositivo.
            >  
            >  I dispositivi che eseguono iOS supportano solo RSA SecurID e MSCHAP v2 per il metodo di autenticazione quando il tipo di connessione è PPTP. Per evitare la segnalazione di errori, distribuire un profilo VPN PPTP distinto nei dispositivi che eseguono iOS.  

        - **Accesso condizionale**
            - Scegliere **Abilita l'accesso condizionale per questa connessione VPN** per garantire che prima della connessione i dispositivi che si connettono alla rete VPN siano stati sottoposti a test di conformità all'accesso condizionale. I criteri di conformità sono descritti in [Criteri di conformità del dispositivo in System Center Configuration Manager](https://docs.microsoft.com/en-us/sccm/protect/deploy-use/device-compliance-policies.md).
            - Scegliere **Abilita l'accesso Single Sign-On (SSO) con il certificato alternativo** per scegliere un certificato diverso dal certificato di autenticazione VPN per la conformità del dispositivo. Se si sceglie questa opzione, specificare **EKU** (elenco delimitato da virgole) e **Hash dell'emittente** per ottenere il certificato corretto che il client VPN deve individuare.

         - Per **Windows Information Protection**, specificare l'identità aziendale gestita dall'organizzazione, che corrisponde in genere al dominio primario dell'organizzazione, ad esempio *contoso.com*. È possibile specificare più domini di proprietà dell'organizzazione separandoli con il carattere "|". Ad esempio, *contoso.com|newcontoso.com*.   
            Per informazioni su Windows Information Protection, vedere [Creare un criterio di Windows Information Protection (WIP) con Microsoft Intune](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/create-wip-policy-using-intune).   

         ![Configurare l'accesso condizionale per VPN](media/vpn-conditional-access.png)

         Se è supportato dalla versione di Windows che esegue Configuration Manager _e_ dal metodo di autorizzazione selezionati, è possibile scegliere **Configura** per aprire la finestra di dialogo delle proprietà di Windows e configurare le proprietà del metodo di autenticazione.  Se l'opzione **Configura** è disabilitata, usare modi diversi per configurare le proprietà del metodo di autenticazione.

2.  Nella pagina **Impostazioni proxy** della **Creazione guidata profilo VPN** selezionare la casella **Configura impostazioni proxy per questo profilo VPN** se la connessione VPN in uso utilizza un server proxy. Quindi, specificare le informazioni relative al server proxy. Per altre informazioni, vedere la documentazione di Windows Server.  

    > [!NOTE]  
    >  Nei computer Windows 8.1 il profilo VPN non visualizzerà le informazioni sul proxy finché l'utente non si connette alla rete VPN usando tale computer.  


3. Configurare altre impostazioni DNS (se necessario).  
 Nella pagina **Configura connessione VPN automatica** è possibile configurare quanto segue:  

    -   **Abilita VPN su richiesta**: usare questa opzione per configurare altre impostazioni DNS per i dispositivi Windows Phone 8.1. Questa impostazione si applica solo ai dispositivi Windows Phone 8.1 e deve essere abilitata solo nei profili VPN che verranno distribuiti a dispositivi Windows Phone 8.1.

    -   **DNS Suffix list** (Elenco suffissi DNS) (solo per i dispositivi Windows Phone 8.1): consente di configurare i domini che stabiliranno una connessione VPN. Per ogni dominio specificato, aggiungere il suffisso DNS, l'indirizzo del server DNS e una delle azioni su richiesta seguenti:  

        -   **Non stabilire mai**: non viene mai aperta una connessione VPN.  

        -   **Stabilisci se necessario**: viene aperta una connessione VPN solo se il dispositivo deve connettersi alle risorse.  

        -   **Stabilisci sempre**: viene sempre aperta la connessione VPN.  

    -   **Unisci**: eventuali suffissi DNS configurati vengono copiati nell'**Elenco reti attendibili**.  

    -   **Elenco reti attendibili** (solo per i dispositivi Windows Phone 8.1): viene specificato un suffisso DNS per ogni riga. Se il dispositivo è in una rete attendibile, la connessione VPN non verrà aperta.  

    -   **Elenco ricerca suffissi** (solo per i dispositivi Windows Phone 8.1): viene specificato un suffisso DNS per ogni riga. Per cercare ogni suffisso DNS durante la connessione a un sito Web verrà usato un nome breve.  

     Ad esempio, è possibile specificare i suffissi DNS **domain1.contoso.com** e **domain2.contoso.com** e quindi passare all'URL **http://mywebsite**. Verranno quindi cercati i seguenti indirizzi:  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

    > [!NOTE]  
    >  Solo per i dispositivi Windows Phone 8.1  
    >   
    >  Quando l'opzione *Invia tutto il traffico di rete tramite la connessione VPN* è selezionata *e* la connessione VPN usa il tunneling completo, tale connessione viene aperta automaticamente mediante il primo profilo di dispositivo. Per aprire una connessione con un profilo diverso, impostare il profilo desiderato come predefinito.  
    >   
    >  Se l'opzione *Invia tutto il traffico di rete tramite la connessione VPN* *non* è selezionata *e* la connessione VPN usa lo split tunneling, le connessioni VPN vengono aperte automaticamente per le route configurate o i suffissi DNS specifici delle connessione.  


4. Nella pagina **Piattaforme supportate** della **Creazione guidata profilo VPN** selezionare i sistemi operativi in cui il profilo VPN verrà installato o scegliere **Seleziona tutto** per installare il profilo VPN in tutti i sistemi operativi disponibili.  

5. Completa la procedura guidata. Il nuovo profilo VPN viene visualizzato nel nodo **Profilo VPN** dell'area di lavoro **Asset e conformità**.  


**Distribuisci**: per altre informazioni sulla distribuzione dei profili VPN, vedere [Distribuire profili Wi-Fi, VPN, di posta elettronica e di certificato](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

## <a name="next-steps"></a>Passaggi successivi  
 Usare gli argomenti seguenti per pianificare, configurare, far funzionare e gestire i profili VPN in Configuration Manager.  

-   [Prerequisiti per i profili VPN in System Center Configuration Manager](../../protect/plan-design/prerequisites-for-wifi-vpn-profiles.md)  

-   [Sicurezza e privacy per i profili VPN in System Center Configuration Manager](../../protect/plan-design/security-and-privacy-for-wifi-vpn-profiles.md)

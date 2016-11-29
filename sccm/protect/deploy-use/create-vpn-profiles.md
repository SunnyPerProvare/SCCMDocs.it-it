---
title: Come creare profili VPN in System Center Configuration Manager
description: Di seguito viene illustrato come si creano i profili VPN in System Center Configuration Manager.
ms.custom: na
ms.date: 10/28/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f338e4db-73b5-45ff-92f4-1b89a8ded989
caps.latest.revision: 15
caps.handback.revision: 0
ms.author: nbigman
ms.manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: e215b33ca24370ddd0e1b892d6ebe559023852a2
ms.openlocfilehash: ccea5cb46bf69dbb88f6fcb217a73c7939be0b02


---
# <a name="how-to-create-vpn-profiles-in-system-center-configuration-manager"></a>Come creare profili VPN in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


> [!NOTE]  
>
> - Per informazioni sui tipi di connessione disponibili per le diverse piattaforme dei dispositivi, vedere [Profili VPN in System Center Configuration Manager](../../protect/deploy-use/vpn-profiles.md).  
> - Per le connessioni VPN di terze parti, distribuire l'app VPN prima di distribuire il profilo VPN. Se si non distribuisce l'app, verrà richiesto agli utenti di farlo quando tentano di connettersi alla VPN. Per informazioni sulla distribuzione delle app, vedere [Distribuire le applicazioni con System Center Configuration Manager](../../apps/deploy-use/deploy-applications).

### <a name="start-the-create-vpn-profile-wizard"></a>avviare la Creazione guidata profilo VPN.  

1.  Nella console di System Center Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** della console di System Center Configuration Manager espandere **Impostazioni di conformità**, **Accesso risorse aziendali** e quindi fare clic su **Profili VPN**.  

3.  Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea profilo VPN**.  

### <a name="provide-general-information-about-the-vpn-profile"></a>fornire informazioni generali sul profilo VPN  

1.  Nella pagina **Generale** della **Creazione guidata profilo VPN**specificare le seguenti informazioni:  

    -   **Nome** : immettere un nome univoco per il profilo VPN (fino a 256 caratteri).  

        > [!IMPORTANT]  
        >  Nel nome del profilo VPN non usare i caratteri \\/:*?<>&#124; né lo spazio. Questi caratteri infatti non sono supportati dal profilo VPN di Windows Server.  

    -   **Descrizione**: immettere una descrizione che consenta di individuare il profilo nella console di System Center Configuration Manager (fino a 256 caratteri).  

    -   **Importa un profilo VPN esistente da un file**: se si seleziona questa opzione, viene visualizzata la pagina **Importa profilo VPN**. In questa pagina, è possibile importare informazioni sul profilo VPN, che sono state in precedenza esportate in un file XML (solo per sistemi operativi Windows 8.1 e Windows RT).  

### <a name="provide-connection-information-for-the-vpn-profile"></a>fornire le informazioni di connessione sul profilo VPN  

1.  Nella pagina **Connessione** della procedura guidata specificare le informazioni seguenti:  

    -   **Tipo di connessione:** Dall'elenco a discesa selezionare il tipo di connessione per la connessione VPN. È possibile scegliere tra i tipi di connessione nella tabella seguente che mostra le piattaforme supportate.  

        > [!IMPORTANT]  
        >  Prima di usare i profili VPN distribuiti in un dispositivo, installare eventuali app VPN di terze parti necessarie. È possibile usare le informazioni dell'argomento [Come creare applicazioni con System Center Configuration Manager](../../apps/deploy-use/create-applications.md) per facilitare la distribuzione dell'app usando System Center Configuration Manager.  

    -   **Elenco server:** Fare clic su **Aggiungi** per aggiungere un nuovo server da usare per la connessione VPN. In base al tipo di connessione è possibile aggiungere uno o più server VPN e specificare quale tra i server sarà il server predefinito.  

        > [!NOTE]  
        >  I dispositivi che eseguono iOS non supportano l'utilizzo di più server VPN. Se si configurano più server VPN e si distribuisce il profilo VPN a un dispositivo iOS, verrà usato solo il server predefinito.  

     Nella tabella seguente potrebbero essere visualizzate le ulteriori opzioni che dipendono dal tipo di connessione selezionato. Per altre informazioni, vedere la documentazione del server VPN.  

    |Opzione|Altre informazioni|Tipo di connessione|  
    |------------|----------------------|---------------------|  
    |**Area di autenticazione**|Specificare il nome dell'area di autenticazione da usare. Un'area di autenticazione è un raggruppamento di risorse di autenticazione usate dal tipo di connessione Pulse Secure.|Pulse Secure|  
    |**Ruolo**|Specificare il nome del ruolo utente che ha accesso a questa connessione.|Pulse Secure|  
    |**Gruppo o dominio di accesso**|Specificare il nome del gruppo di accesso o di dominio a cui connettersi.|Dell SonicWALL Mobile Connect|  
    |**Impronta digitale**|Specificare una stringa, ad esempio "Codice impronta digitale Contoso", che verrà usata per verificare l'attendibilitàò del server VPN.<br /><br /> Un'impronta digitale può essere:<br /><br /> - Inviata al client in modo da informarlo che può considerare attendibile un server che presenta la stessa impronta digitale durante la connessione.<br /><br /> - Se il dispositivo non ha ancora l'impronta digitale, richiederà all'utente di considerare attendibile il server VPN usato per la connessione durante la visualizzazione dell'impronta digitale (l'utente verifica manualmente l'impronta digitale e fa clic su Attendibilità per connettersi).|VPN mobile Check Point|  
    |**Invia tutto il traffico di rete tramite la connessione VPN**|Se questa opzione non è selezionata, è possibile specificare route aggiuntive per la connessione (per i tipi di connessione **Microsoft SSL (SSTP)**, **Microsoft Automatico**, **IKEv2**, **PPTP** e **L2TP** ), caratteristica nota come split o tunneling VPN.<br /><br /> Solo le connessioni alla rete aziendale vengono inviate tramite un tunnel VPN. Il tunneling VPN non viene usato quando si esegue la connessione alle risorse su Internet.|All|  
    |**Suffisso DNS specifico della connessione**|Facoltativamente, specificare il suffisso DNS (Domain Name System) specifico per la connessione.|- <br />                            Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatico<br /><br /> - <br />                            IKEv2<br /><br /> - <br />                            PPTP<br /><br /> - <br />                            L2TP|  
    |**Disabilita VPN quando il dispositivo è connesso alla rete Wi-Fi aziendale**|Specifica che la connessione VPN non verrà usata quando il dispositivo è connesso alla rete Wi-Fi aziendale.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN<br /><br /> - Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatico<br /><br /> - IKEv2<br /><br /> - L2TP|  
    |**Disabilita VPN quando il dispositivo è connesso alla rete Wi-Fi domestica**|Specifica che la connessione VPN non verrà usata quando il dispositivo è connesso a una rete Wi-Fi domestica.|All|  
    |**VPN per app (iOS 7 e versioni successive, Mac OS X 10.9 e versioni successive)**|Selezionare questa opzione se si vuole associare questa connessione VPN a un'app iOS in modo da aprire la connessione quando si esegue l'app. È possibile associare il profilo VPN a un'app quando viene distribuito.|- <br />                        Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
    |**XML personalizzato (opzionale)**|Consente di specificare i comandi XML personalizzati che consentono di configurare la connessione VPN.<br /><br /> Esempi:<br /><br /> Per **Pulse Secure**:<br /><br /> **<pulse-schema><isSingleSignOnCredential\>true</isSingleSignOnCredential\></pulse-schema>**<br /><br /> Per **VPN Checkpoint Mobile**:<br /><br /> **&lt;CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" /\>**<br /><br /> Per **Dell SonicWALL Mobile Connect**:<br /><br /> **<MobileConnect\><Compression\>false</Compression\><debugLogging\>True</debugLogging\><packetCapture\>False</packetCapture\></MobileConnect\>**<br /><br /> Per **F5 Edge Client**:<br /><br /> **&lt;f5-vpn-conf&gt;&lt;single-sign-on-credential /&gt;&lt;/f5-vpn-conf&gt;**<br /><br /> Per altre informazioni su come scrivere comandi XML personalizzati, fare riferimento alla documentazione della VPN fornita dai singoli produttori.|- Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  

####   <a name="windows-10-vpn-features-available-when-using-configuration-manager-with-intune"></a>Funzionalità VPN di Windows 10 disponibili quando si usa Configuration Manager con Intune  


> [!NOTE]  
> Il nome di un profilo VPN che usa le funzionalità VPN di Windows 10 non può essere in formato unicode né contenere caratteri speciali.


|Opzione|Altre informazioni|Tipo di connessione|  
|------------|----------------------|---------------------|  
|**Disabilita VPN quando il dispositivo è connesso alla rete Wi-Fi aziendale**|Specifica che la connessione VPN non verrà usata quando il dispositivo è connesso alla rete Wi-Fi aziendale. Immettere il nome di rete attendibile, che verrà usato per determinare se il dispositivo è connesso alla rete aziendale.|All|  
|**Regole del traffico di rete**|Impostare i protocolli e gli intervalli di porte e indirizzi locali e remoti che verranno abilitati per la connessione VPN.<br /><br /> **Nota:** se non si crea una regola del traffico di rete, tutti i protocolli, le porte e gli intervalli di indirizzi vengono abilitati. Dopo aver creato una regola, solo i protocolli, le porte e gli intervalli di indirizzi specificati in tale regola o nelle regole aggiuntive verranno usati dalla connessione VPN.|All|  
|**Route**|Specifica le route che verranno usate dalla connessione VPN. Si noti che la creazione di più di 60 route può causare errori del criterio. |All|  
|**Server DNS**|Specifica i server DNS che vengono usati dalla connessione VPN una volta stabilita la connessione.|All|  
|**App in grado di connettersi automaticamente alla rete VPN**|È possibile aggiungere app o importare elenchi di app che useranno automaticamente la connessione VPN. Il tipo di app determinerà l'identificatore dell'app. Per un'app desktop, specificare il percorso file dell'app. Per un'app universale, specificare il nome della famiglia di pacchetti (PFN). Per sapere come individuare il nome PFN per un'app, vedere la sezione relativa al [reperimento di un nome di famiglia di pacchetti per la VPN per app](../../protect/deploy-use/find-a-pfn-for-per-app-vpn.md). |All|

> [!IMPORTANT]
> Si consiglia di proteggere tutti gli elenchi di app associate che si compilano per l'uso nella configurazione della VPN per app. Se l'elenco viene modificato da un utente non autorizzato e viene importato nell'elenco di app della VPN per app, si autorizza potenzialmente l'accesso alla VPN da parte di applicazioni che non devono potervi accedere. Un modo per proteggere gli elenchi di app consiste nell'usare un elenco di controllo di accesso (ACL).


### <a name="configure-the-authentication-method-for-the-vpn-profile"></a>configurare il metodo di autenticazione per il profilo VPN  

1.  Nella pagina **Metodo di autenticazione** della procedura guidata specificare le informazioni seguenti:  

    -   **Metodo di autenticazione:** Dall'elenco a discesa selezionare il metodo di autenticazione che verrà usato dalla connessione VPN. Le voci nell'elenco a discesa potrebbero essere diverse a seconda del tipo di connessione precedentemente selezionato. I metodi di autenticazione disponibili e i tipi di connessione supportati sono elencati nella tabella seguente.  

        |Metodo di autenticazione|Tipi di connessione supportati|  
        |---------------------------|--------------------------------|  
        |**Certificati**<br /><br /> **Nota:** : se il certificato client viene usato per eseguire l'autenticazione in un server RADIUS, ad esempio un server dei criteri di rete, è necessario impostare il nome alternativo del soggetto nel certificato sul nome dell'entità utente.|- <br />                            Cisco AnyConnect<br /><br /> - Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
        |**Nome utente e password**|- <br />                            Pulse Secure<br /><br /> - F5 Edge Client<br /><br /> - Dell SonicWALL Mobile Connect<br /><br /> - Check Point Mobile VPN|  
        |**Microsoft EAP-TTLS**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatico<br /><br /> - PPTP<br /><br /> - IKEv2<br /><br /> - L2TP|  
        |**Microsoft PEAP (Protected EAP)**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatico<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Password protetta Microsoft (EAP-MSCHAP v2)**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatico<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Smart card o altro certificato**|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatico<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**MSCHAP v2**|-  Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatico<br /><br /> - IKEv2<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**RSA SecurID** (solo iOS)|- Microsoft SSL (SSTP)<br /><br /> - Microsoft Automatico<br /><br /> - PPTP<br /><br /> - L2TP|  
        |**Usa certificati computer**|IKEv2|  

         A seconda delle opzioni selezionate, potrebbe essere necessario specificare altre informazioni, ad esempio:  

        -   **Memorizza le credenziali utente a ogni accesso**: selezionare questa opzione per garantire che le credenziali utente vengano memorizzate in modo che l'utente non debba immetterle ogni volta che viene stabilita una connessione.  

        -   **Selezionare un certificato client per l'autenticazione client** : selezionare il certificato SCEP client creato in precedenza che verrà usato per autenticare la connessione VPN. Per altre informazioni su come usare i profili certificato in System Center Configuration Manager, vedere [Profili certificato in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

            > [!NOTE]  
            >  Per i dispositivi iOS, il profilo SCEP selezionato verrà incorporato nel profilo VPN. Per altre piattaforme, viene aggiunta una regola di applicabilità per garantire che il profilo VPN non venga installato se il certificato non è presente o non è conforme.  
            >   
            >  Se il certificato SCEP specificato non è conforme o non è stato distribuito, il profilo VPN non verrà installato nel dispositivo.
            >  
            >  I dispositivi che eseguono iOS supportano solo RSA SecurID e MSCHAP v2 per il metodo di autenticazione quando il tipo di connessione è PPTP. Per evitare la segnalazione di errori, distribuire un profilo VPN PPTP distinto nei dispositivi che eseguono iOS.  

               - Le impostazioni **Accesso condizionale** e  **Dominio primario di protezione dei dati aziendali** sono supportate solo quando si usa Configuration Manager senza Intune, a cui è possibile accedere scegliendo **Avanzate**.
        
        ![Configurare l'accesso condizionale per VPN](../media/vpn-conditional-access.png)

        -   Per alcuni metodi di autenticazione è possibile fare clic su **Configura** per aprire la finestra di dialogo delle proprietà di Windows (se la versione di Windows in cui è in esecuzione la console di System Center Configuration Manager supporta questo metodo di autenticazione) che consente di configurare le proprietà del metodo di autenticazione.  

### <a name="configure-proxy-settings-for-the-vpn-profile"></a>configurare le impostazioni proxy per il profilo VPN  

1.  Nella pagina **Impostazioni proxy** di **Creazione guidata profilo VPN**, selezionare la casella di controllo **Configura impostazioni proxy per questo profilo VPN** se la connessione VPN in uso usa un server proxy.  

2.  Specificare i dettagli relativi al server proxy e alle relative impostazioni. Per altre informazioni, vedere la documentazione di Windows Server.  

> [!NOTE]  
>  Nei computer Windows 8.1, il profilo VPN non visualizzerà le informazioni sul proxy finché l'utente non si connette alla rete VPN con tale computer.  


### <a name="configure-further-dns-settings-if-required"></a>Configurare altre impostazioni DNS (se necessario)  
 Nella pagina **Configura connessione VPN automatica** della procedura guidata, è possibile configurare le impostazioni seguenti:  

-   **Abilita VPN su richiesta**: selezionare questa opzione per configurare altre impostazioni DNS in questa pagina della procedura guidata per i dispositivi Windows Phone 8.1.

> [!Note]  
> Questa impostazione si applica solo ai dispositivi Windows Phone 8.1 e deve essere abilitata solo nei profili VPN che verranno distribuiti a dispositivi Windows Phone 8.1.


-   Elenco dei suffissi DNS (solo per i dispositivi Windows Phone 8.1): consente di configurare i domini che stabiliranno una connessione VPN. Per ogni dominio specificato, aggiungere il suffisso DNS, l'indirizzo del server DNS e una delle azioni su richiesta seguenti:  

    -   **Non stabilire mai**: non viene mai aperta una connessione VPN  

    -   **Stabilisci se necessario**: viene aperta una connessione VPN solo se il dispositivo deve connettersi alle risorse  

    -   **Stabilisci sempre**: viene aperta sempre la connessione VPN  

-   **Unisci**: eventuali suffissi DNS configurati vengono copiati nell'**Elenco reti attendibili**.  

-   **Elenco reti attendibili** (solo per i dispositivi Windows Phone 8.1): viene specificato un suffisso DNS per ogni riga. Se il dispositivo è in una rete attendibile, la connessione VPN non verrà aperta.  

-   **Elenco ricerca suffissi** (solo per i dispositivi Windows Phone 8.1): viene specificato un suffisso DNS per ogni riga. Per cercare ogni suffisso DNS specificato durante la connessione a un sito Web verrà usato un nome breve.  

     Ad esempio, si può specificare i suffissi DNS **domain1.contoso.com** e **domain2.contoso.com** , indicando come URL **http://mywebsite**. Verranno quindi cercati i seguenti indirizzi:  

    -   **http://mywebsite.domain1.contoso.com**  

    -   **http://mywebsite.domain2.contoso.com**  

> [!NOTE]  
>  Solo per i dispositivi Windows Phone 8.1  
>   
>  Se è selezionata l'opzione **Invia tutto il traffico di rete tramite la connessione VPN** e la connessione VPN usa il tunneling completo, per il primo profilo sottoposto a provisioning nel dispositivo, la connessione VPN verrà aperta automaticamente. Se si desidera un profilo diverso per aprire automaticamente una connessione, è necessario renderlo il profilo predefinito nel dispositivo.  
>   
>  Se non è selezionata l'opzione **Invia tutto il traffico di rete tramite la connessione VPN** e la connessione VPN usa lo split tunneling, può essere aperta una connessione VPN automaticamente se si configurano le route o un suffisso DNS specifico per la connessione.  


### <a name="configure-supported-platforms-for-the-vpn-profile"></a>configurare piattaforme supportate per il profilo VPN  
 Le piattaforme supportate sono i sistemi operativi in cui verrà installato il profilo VPN.  

Nella pagina **Piattaforme supportate** della **Creazione guidata profilo VPN**, selezionare i sistemi operativi in cui il profilo VPN verrà installato o fare clic su **Seleziona tutto** per installare il profilo VPN in tutti i sistemi operativi disponibili.  

### <a name="complete-the-wizard"></a>completare la procedura guidata  
 Nella pagina **Riepilogo** della procedura guidata rivedere le azioni da eseguire, quindi scegliere **Fine**. Il nuovo profilo VPN viene visualizzato nel nodo **Profili VPN** dell'area di lavoro **Asset e conformità** .  

### <a name="next-steps"></a>Passaggi successivi

- Per le connessioni VPN di terze parti, distribuire l'app VPN prima di distribuire il profilo VPN. Se si non distribuisce l'app, verrà richiesto agli utenti di farlo quando tentano di connettersi alla VPN. Per informazioni sulla distribuzione delle app, vedere [Distribuire le applicazioni con System Center Configuration Manager](../../apps/deploy-use/deploy-applications).

- Distribuire il profilo VPN seguendo la procedura descritta in [Come distribuire profili VPN in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  



<!--HONumber=Nov16_HO1-->



---
title: Creare profili Wi-Fi | System Center Configuration Manager
description: Di seguito viene illustrato come usare i profili Wi-Fi in System Center Configuration Manager per distribuire impostazioni di rete wireless agli utenti dell'organizzazione.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
caps.latest.revision: 13
caps.handback.revision: 0
author: Nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 295ccc2ce7c1dae55c45113cc8ff826e30f7079a


---
# <a name="how-to-create-wi-fi-profiles-in-system-center-configuration-manager"></a>Come creare profili Wi-Fi in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


È possibile usare i profili Wi-Fi in System Center Configuration Manager per distribuire impostazioni di rete wireless agli utenti dell'organizzazione. Distribuendo queste impostazioni si semplifica la procedura di connessione alla rete Wi-Fi per gli utenti.  

 Si immagini ad esempio di aver installato una nuova rete Wi-Fi denominata **Contoso Wi-Fi** e di voler ora eseguire il provisioning di tutti i dispositivi che eseguono il sistema operativo iOS con le impostazioni necessarie per connettersi alla rete. È quindi possibile creare un profilo Wi-Fi contenente le impostazioni necessarie per la connessione alla rete wireless **Contoso Wi-Fi** e distribuire questo profilo a tutti gli utenti della gerarchia che dispongono di dispositivi iOS. In questo modo gli utenti dei dispositivi iOS visualizzeranno la rete aziendale nell'elenco delle reti wireless e potranno facilmente connettersi a tale rete.  

 Con i profili Wi-Fi è possibile configurare i seguenti tipi di dispositivi:  

-   Dispositivi che eseguono Windows 8.1 a 32 bit  

-   Dispositivi che eseguono Windows 8.1 a 64 bit  

-   Dispositivi che eseguono Windows RT 8.1  

-   Dispositivi che eseguono Windows Phone 8.1  

-   Dispositivi che eseguono Windows 10 Desktop o Mobile  

-   Dispositivi IPhone che eseguono iOS 5, iOS 6, iOS 7 e iOS 8  

-   Dispositivi IPad che eseguono iOS 5, iOS 6, iOS 7 e iOS 8  

-   Dispositivi Android che eseguono la versione 4  

> [!IMPORTANT]  
>  Per distribuire i profili nei dispositivi Android, iOS, Windows Phone e nei dispositivi registrati Windows 8.1 o versioni successive, tali dispositivi devono essere registrati in Microsoft Intune. Per informazioni su come registrare i dispositivi, vedere [Registrare i dispositivi per la gestione in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).  

 Quando si crea un profilo Wi-Fi, è possibile includere una vasta gamma di impostazioni di protezione. Queste includono certificati per la convalida del server e l'autenticazione del client di cui è stato eseguito il provisioning usando profili certificato di Configuration Manager. Per altre informazioni sui profili certificato, vedere [Profili certificato in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

## <a name="steps-to-create-a-wi-fi-profile"></a>Procedura per creare un profilo Wi-Fi  
 Usare i seguenti passaggi necessari per creare un profilo Wi-Fi usando la **Creazione guidata profilo Wi-Fi**.  

-   [Passaggio 1: avviare la Creazione guidata profilo Wi-Fi](#BKMK_Step1)  

-   [Passaggio 2: inserire informazioni generali sul profilo Wi-Fi](#BKMK_Step2)  

-   [Passaggio 3: inserire informazioni sulla rete wireless](#BKMK_Step3)  

-   [Passaggio 4: configurare la sicurezza per il profilo Wi-Fi](#BKMK_Step4)  

-   [Passaggio 5: configurare le impostazioni avanzate per il profilo Wi-Fi](#BKMK_Step5)  

-   [Passaggio 6: configurare le impostazioni proxy per il profilo Wi-Fi](#BKMK_Step6)  

-   [Passaggio 7: configurare le piattaforme supportate per il profilo Wi-Fi](#BKMK_Step7)  

-   [Passaggio 8: completare la procedura guidata](#BKMK_Step8)  

##  <a name="a-namebkmkstep1a-step-1-start-the-create-wi-fi-profile-wizard"></a><a name="BKMK_Step1"></a> Passaggio 1: avviare la Creazione guidata profilo Wi-Fi  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** , espandere **Impostazioni di conformità**, **Accesso risorse aziendali**, quindi fare clic su **Profili Wi-Fi**.  

3.  Nella scheda **Home** del gruppo **Crea** , fare clic su **Crea profilo Wi-Fi**.  

##  <a name="a-namebkmkstep2a-step-2-provide-general-information-about-the-wi-fi-profile"></a><a name="BKMK_Step2"></a> Passaggio 2: inserire informazioni generali sul profilo Wi-Fi  

1.  Nella pagina **Generale** della Creazione guidata profilo Wi-Fi immette un nome univoco e una descrizione per il profilo Wi-Fi. È possibile usare un massimo di 256 caratteri.  

2.  Per usare le impostazioni da un altro profilo Wi-Fi, selezionare **Importa un elemento del profilo Wi-Fi esistente da un file**.  

    > [!IMPORTANT]  
    >  Accertarsi che il profilo Wi-Fi che si importa contenga un XML valido per un profilo Wi-Fi. Configuration Manager non convalida il profilo quando si importa il file.  

3.  In  
                            **Gravità della non conformità per i report**: specificare il livello di gravità che viene segnalato se il profilo Wi-Fi risulta non conforme su dispositivi client, ad esempio se non è possibile installare il profilo. I livelli di gravità disponibili sono i seguenti:  

    -   **Nessuno**: i computer che non soddisfano questa regola di conformità non segnalano una gravità dell'errore per i report di Configuration Manager.  

    -   **Informazioni**: i computer che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Informazioni** per i report di Configuration Manager.  

    -   **Avviso**: i computer che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Avviso** per i report di Configuration Manager.  

    -   **Errore critico**: i computer che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Critico** per i report di Configuration Manager.  

    -   **Errore critico con evento**: i computer che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Critico** per i report di Configuration Manager. Il livello di gravità viene anche registrato come un evento Windows nel registro eventi applicazione.  

##  <a name="a-namebkmkstep3a-step-3-provide-information-about-the-wireless-network"></a><a name="BKMK_Step3"></a> Passaggio 3: inserire informazioni sulla rete wireless  

1.  Nella pagina **Profilo Wi-Fi** della Creazione guidata profilo Wi-Fi specificare un nome descrittivo per la connessione Internet wireless usando un massimo di 32 caratteri. Questo è il nome che i dispositivi visualizzeranno come nome della rete.  

    > [!IMPORTANT]  
    >  Configuration Manager non supporta l'uso dei caratteri apostrofo (**â€˜**) o virgola (**,**) nel nome della rete.  

2.  In **SSID**specificare il nome (SSID) della rete wireless a cui devono essere in grado di connettersi i dispositivi. È possibile usare un massimo di 32 caratteri. Per il nome SSID viene fatta distinzione tra maiuscole e minuscole, di conseguenza assicurarsi di immetterlo esattamente come è configurato.  

3.  Selezionare **Connetti automaticamente quando la rete si trova nel campo del computer**per consentire ai dispositivi di riconnettersi automaticamente alla rete wireless quando si trova nel campo del computer.  

4.  Selezionare  
                            **Cerca altre reti wireless durante la connessione a questa rete**.  

5.  Selezionare **Connetti quando la rete non sta trasmettendo il nome (SSID)**per consentire ai dispositivi di connettersi alla rete quando questa non è visibile nell'elenco delle reti perché è nascosta e non trasmette il suo nome.  

##  <a name="a-namebkmkstep4a-step-4-configure-security-for-the-wi-fi-profile"></a><a name="BKMK_Step4"></a> Passaggio 4: configurare la sicurezza per il profilo Wi-Fi  

> [!IMPORTANT]  
>  Se si intende creare un profilo Wi-Fi per la gestione dei dispositivi mobili locale, il ramo corrente di Configuration Manager supporta solo le configurazioni di sicurezza Wi-Fi seguenti:  
>   
>  Tipi di sicurezza: **WPA2 Enterprise** o **WPA2 Personal**  
> Tipi di crittografia: **AES** o **TKIP**  
> Tipi EAP: **Smart Card o altro certificato** o **PEAP**  

1.  Nella pagina **Configurazione protezione** della Creazione guidata profilo Wi-Fi selezionare il protocollo di sicurezza usato dalla rete wireless oppure selezionare **Nessuna autenticazione (aperta)** se la rete non è protetta.  

     Solo per i dispositivi Android: i tipi di sicurezza **WPA â€“ Personal**, **WPA2 â€“ Personal** e **WEP** non sono supportati.  

2.  selezionare il metodo di crittografia usato dalla rete wireless.  

3.  selezionare il tipo EAP che viene usato per l'autenticazione con la rete wireless.  

     Solo per i dispositivi Windows Phone: i tipi EAP **LEAP** e **EAP-FAST** non sono supportati.  

4.  Fare clic su **Configura** per specificare le proprietà per il tipo EAP selezionato. Questa opzione potrebbe non essere disponibile per alcuni tipi EAP selezionati.  

    > [!IMPORTANT]  
    >  Quando si fa clic su **Configura**, viene visualizzata una finestra di dialogo di Windows. Di conseguenza, è necessario garantire che il sistema operativo del computer che esegue la console di Configuration Manager supporti la configurazione del tipo EAP selezionato.  
    >   
    >  Per i dispositivi iOS, se si sceglie un metodo non EAP per l'autenticazione, a prescindere dal metodo scelto, per la connessione verrà utilizzato MS-CHAP v2.  

5.  Selezionare **Memorizza le credenziali utente a ogni accesso**per archiviare le credenziali utente in modo che gli utenti non debbano immetterle a ogni accesso.  

### <a name="for-ios-devices-only"></a>Solo per i dispositivi iOS:  
 configurare le impostazioni per gli eventuali certificati richiesti per la connessione Wi-Fi. È necessario configurare il certificato client e il nome del certificato server attendibile oppure il certificato radice come segue:  

-   **Nomi di certificato del server trusted**: se il server a cui si connette il dispositivo usa un certificato di autenticazione server per identificare il server e proteggere il canale di comunicazione, immettere il nome o i nomi nel nome del soggetto o nel nome alternativo del soggetto del certificato. Il nome o i nomi sono in genere il nome di dominio completo del server. Ad esempio, se il certificato del server ha un nome comune srv1.contoso.com nel soggetto del certificato, immettere **srv1.contoso.com**. Se il certificato del server dispone di più nomi specificati nel nome alternativo oggetto, immettere i nomi separati da un punto e virgola.  

    > [!TIP]  
    >  Se il certificato client selezionato per l'autenticazione EAP o l'autenticazione client per un dispositivo iOS verrà usato per l'autenticazione su un server RADIUS (Remote Authentication Dial-In User Service), ad esempio un server che sta eseguendo il server dei criteri di rete, il Nome alternativo oggetto deve essere impostato su Nome entità utente.  

-   **Seleziona i certificati radice per la convalida del server**: se il server a cui il dispositivo si connette utilizza un certificato di autenticazione server che non è ritenuto attendibile dal dispositivo, selezionare il profilo certificato contenente il certificato radice per il certificato del server per creare una catena di certificati attendibili sul dispositivo.  

-   **Selezionare un certificato client per l'autenticazione client**: se il server o il dispositivo di rete richiede a un certificato client di autenticare il dispositivo connesso, selezionare il profilo certificato contenente il certificato di autenticazione client.  

> [!NOTE]  
>  Prima di selezionare il certificato radice e il certificato client, questi devono essere configurati e distribuiti come un profilo certificato. Per altre informazioni sui profili certificato, vedere [Profili certificato in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

##  <a name="a-namebkmkstep5a-step-5-configure-advanced-settings-for-the-wi-fi-profile"></a><a name="BKMK_Step5"></a> Passaggio 5: configurare le impostazioni avanzate per il profilo Wi-Fi  
 Nella pagina **Impostazioni avanzate** della Creazione guidata profilo Wi-Fi, specificare le impostazioni avanzate per il profilo Wi-Fi, ad esempio la modalità di autenticazione, le opzioni Single Sign-On e la conformità a FIPS (Federal Information Processing Standards). Per altre informazioni su queste opzioni, vedere la documentazione di Windows.  

> [!NOTE]  
>  Le impostazioni avanzate potrebbero non essere disponibili, o variare, in base alle opzioni selezionate nella pagina **Configurazione protezione** della procedura guidata.  

##  <a name="a-namebkmkstep6a-step-6-configure-proxy-settings-for-the-wi-fi-profile"></a><a name="BKMK_Step6"></a> Passaggio 6: configurare le impostazioni proxy per il profilo Wi-Fi  

1.  Nella pagina **Impostazioni proxy** della Creazione guidata profilo Wi-Fi, selezionare la casella di controllo **Configura impostazioni proxy per questo profilo Wi-Fi** se la rete wireless in uso usa un server proxy.  

2.  Specificare i dettagli relativi al server proxy e alle relative impostazioni. Per altre informazioni, vedere la documentazione di Windows Server.  

##  <a name="a-namebkmkstep7a-step-7-configure-supported-platforms-for-the-wi-fi-profile"></a><a name="BKMK_Step7"></a> Passaggio 7: configurare le piattaforme supportate per il profilo Wi-Fi  
 Nella pagina **Piattaforme supportate** della Creazione guidata profilo certificato, selezionare i sistemi operativi in cui si desidera installare il profilo Wi-Fi. In alternativa, fare clic su **Seleziona tutto** per installare il profilo Wi-Fi in tutti i sistemi operativi disponibili.  

##  <a name="a-namebkmkstep8a-step-8-complete-the-wizard"></a><a name="BKMK_Step8"></a> Passaggio 8: completare la procedura guidata  
 Nella pagina **Riepilogo** della procedura guidata, rivedere le azioni da eseguire e quindi completare la procedura. Il nuovo profilo Wi-Fi viene visualizzato nel nodo **Profili Wi-Fi** dell'area di lavoro **Asset e conformità** .  

 Per informazioni su come distribuire il profilo Wi-Fi, vedere [Come distribuire profili Wi-Fi in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  



<!--HONumber=Nov16_HO1-->



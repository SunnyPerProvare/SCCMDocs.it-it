---
title: Come creare profili Wi-Fi
titleSuffix: Configuration Manager
description: Di seguito viene illustrato come usare i profili Wi-Fi in System Center Configuration Manager per distribuire impostazioni di rete wireless agli utenti dell'organizzazione.
ms.date: 12/11/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b665143f40973c20307b99c15f94d773d43b4914
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32350810"
---
# <a name="create-wi-fi-profiles"></a>Creare profili Wi-Fi

*Si applica a: System Center Configuration Manager (Current Branch)*


È possibile usare i profili Wi-Fi in System Center Configuration Manager per distribuire impostazioni di rete wireless agli utenti dell'organizzazione. Distribuendo queste impostazioni si semplifica la procedura di connessione alla rete Wi-Fi per gli utenti.  

 Si supponga ad esempio di disporre di una rete Wi-Fi per cui si vuole abilitare la connessione da parte di tutti i dispositivi iOS. Creare un profilo Wi-Fi contenente le impostazioni necessarie per connettersi alla rete wireless. Quindi, distribuire il profilo a tutti gli utenti della gerarchia che dispongono di dispositivi iOS. In questo modo gli utenti dei dispositivi iOS visualizzeranno la rete aziendale nell'elenco delle reti wireless e potranno facilmente connettersi a tale rete.  

 Con i profili Wi-Fi è possibile configurare i seguenti tipi di dispositivi:  

-   Dispositivi che eseguono Windows 8.1 a 32 bit  

-   Dispositivi che eseguono Windows 8.1 a 64 bit  

-   Dispositivi che eseguono Windows RT 8.1  

-   Dispositivi che eseguono Windows 10 Desktop o Mobile  

L'articolo [Creare profili Wi-Fi](../../mdm/deploy-use/create-wifi-profiles.md) contiene informazioni su come usare i profili Wi-Fi in Configuration Manager per distribuire le impostazioni di rete wireless agli utenti dei dispositivi mobili.

> [!IMPORTANT]  
>  Per distribuire i profili nei dispositivi Android, iOS, Windows Phone e nei dispositivi registrati Windows 8.1 o versioni successive, tali dispositivi devono essere registrati in Microsoft Intune. Per informazioni su come registrare i dispositivi, vedere [Registrare i dispositivi per la gestione in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).  

 Quando si crea un profilo Wi-Fi, è possibile includere una vasta gamma di impostazioni di protezione. Queste includono certificati per la convalida del server e l'autenticazione del client che sono stati inseriti usando profili certificato di Configuration Manager. Per altre informazioni sui profili certificato, vedere [Profili certificato in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

## <a name="create-a-wi-fi-profile"></a>Creare un profilo Wi-Fi  

1.  Nella console di Configuration Manager scegliere **Asset e conformità** > **Impostazioni di conformità** >  **Accesso risorse aziendali** > **Profili Wi-Fi**.  

3.  Nel gruppo **Crea** della scheda **Home** scegliere **Crea profilo Wi-Fi**.  

1.  Nella pagina **Generale** immettere un nome univoco e una descrizione per il profilo Wi-Fi.  Per usare le impostazioni da un altro profilo Wi-Fi, selezionare **Importa un elemento del profilo Wi-Fi esistente da un file**.  

    > [!IMPORTANT]  
    >  Accertarsi che il profilo Wi-Fi che si importa contenga un XML valido per un profilo Wi-Fi. Configuration Manager non convalida il profilo quando si importa il file.  

3.  In **Gravità della non conformità per i report** specificare il livello di gravità che viene segnalato se il profilo Wi-Fi risulta non conforme su dispositivi client, ad esempio se non è possibile installare il profilo. I livelli di gravità disponibili sono i seguenti:  

    -   **Nessuno**: i computer che non soddisfano questa regola di conformità non segnalano una gravità dell'errore per i report di Configuration Manager.  

    -   **Informazioni**: i computer che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Informazioni** per i report di Configuration Manager.  

    -   **Avviso**: i computer che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Avviso** per i report di Configuration Manager.  

    -   **Errore critico**: i computer che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Critico** per i report di Configuration Manager.  

    -   **Errore critico con evento**: i computer che non soddisfano questa regola di conformità segnalano una gravità dell'errore del tipo **Critico** per i report di Configuration Manager. Il livello di gravità viene anche registrato come un evento Windows nel registro eventi applicazione.  

1.  Nella pagina **Profilo Wi-Fi** fornire il nome che i dispositivi visualizzeranno come nome della rete.  

    > [!IMPORTANT]  
    >  Configuration Manager non supporta l'uso dei caratteri apostrofo (**â€˜**) o virgola (**,**) nel nome della rete.  

2.  Specificare l'**SSID** facendo attenzione alla distinzione tra maiuscole e minuscole.
3.  Scegliere le altre opzioni di connettività appropriate, tra cui   **Connetti quando la rete non sta trasmettendo il nome (SSID)**, se è possibile che l'SSID sia nascosto.  

4.  Nella pagina **Configurazione protezione** selezionare il protocollo di sicurezza usato dalla rete wireless oppure selezionare **Nessuna autenticazione (aperta)** se la rete non è protetta.
    > [!IMPORTANT]  
    >  Se si intende creare un profilo Wi-Fi per la gestione dei dispositivi mobili locale, il ramo corrente di Configuration Manager supporta solo le configurazioni di sicurezza Wi-Fi seguenti:  
    >   
    >  Tipi di sicurezza: **WPA2 Enterprise** o **WPA2 Personal**  
    > Tipi di crittografia: **AES** o **TKIP**  
    > Tipi EAP: **Smart Card o altro certificato** o **PEAP**  

    > Per i dispositivi Android, i tipi di sicurezza **WPA Personal**, **WPA2 Personal** e **WEP** non sono supportati.  

2.  selezionare il metodo di crittografia usato dalla rete wireless.  

3.  selezionare il tipo EAP che viene usato per l'autenticazione con la rete wireless.  

     Solo per i dispositivi Windows Phone: i tipi EAP **LEAP** e **EAP-FAST** non sono supportati.  

4.  Fare clic su **Configura** per specificare le proprietà per il tipo EAP selezionato. Questa opzione potrebbe non essere disponibile per alcuni tipi EAP selezionati.  

    > [!IMPORTANT]  
    >  Quando si fa clic su **Configura**, viene visualizzata una finestra di dialogo di Windows. Di conseguenza, è necessario garantire che il sistema operativo del computer che esegue la console di Configuration Manager supporti la configurazione del tipo EAP selezionato.  
    >   
    >  Per i dispositivi iOS, se si sceglie un metodo non EAP per l'autenticazione, a prescindere dal metodo scelto, per la connessione verrà utilizzato MS-CHAP v2.  

5.  Selezionare **Memorizza le credenziali utente a ogni accesso**per archiviare le credenziali utente in modo che gli utenti non debbano immetterle a ogni accesso.  

6. **Solo per i dispositivi iOS:**  
 configurare le impostazioni per gli eventuali certificati richiesti per la connessione Wi-Fi. È necessario configurare il certificato client e il nome del certificato server attendibile oppure il certificato radice come segue:  

    -   **Nomi di certificato del server trusted**: se il server a cui si connette il dispositivo usa un certificato di autenticazione server per identificare il server e proteggere il canale di comunicazione, immettere il nome o i nomi nel nome del soggetto o nel nome alternativo del soggetto del certificato. Il nome o i nomi sono in genere il nome di dominio completo del server. Ad esempio, se il certificato del server ha un nome comune srv1.contoso.com nel soggetto del certificato, immettere **srv1.contoso.com**. Se il certificato del server dispone di più nomi specificati nel nome alternativo oggetto, immettere i nomi separati da un punto e virgola.  

    > [!TIP]  
    >  Se il certificato client selezionato per l'autenticazione EAP o l'autenticazione client per un dispositivo iOS verrà usato per l'autenticazione su un server RADIUS (Remote Authentication Dial-In User Service), ad esempio un server che sta eseguendo il server dei criteri di rete, il Nome alternativo oggetto deve essere impostato su Nome entità utente.  

    -   **Seleziona i certificati radice per la convalida del server**: se il server a cui il dispositivo si connette utilizza un certificato di autenticazione server che non è ritenuto attendibile dal dispositivo, selezionare il profilo certificato contenente il certificato radice per il certificato del server per creare una catena di certificati attendibili sul dispositivo.  

    -   **Selezionare un certificato client per l'autenticazione client**: se il server o il dispositivo di rete richiede a un certificato client di autenticare il dispositivo connesso, selezionare il profilo certificato contenente il certificato di autenticazione client.  

    > [!NOTE]  
    >  Prima di selezionare il certificato radice e il certificato client, questi devono essere configurati e distribuiti come un profilo certificato. Per altre informazioni sui profili certificato, vedere [Profili certificato in System Center Configuration Manager](introduction-to-certificate-profiles.md).  

7.  Nella pagina **Impostazioni avanzate** specificare le impostazioni avanzate per il profilo Wi-Fi, ad esempio la modalità di autenticazione, le opzioni Single Sign-On e la conformità a FIPS (Federal Information Processing Standards). Per altre informazioni su queste opzioni, vedere la documentazione di Windows. Le impostazioni avanzate potrebbero non essere disponibili, o variare, in base alle opzioni selezionate nella pagina **Configurazione protezione** della procedura guidata.  

1.  Nella pagina **Impostazioni proxy** selezionare **Configura impostazioni proxy per questo profilo Wi-Fi** se la rete wireless usa un server proxy e quindi fornire le informazioni di configurazione.  

2. Nella pagina **Piattaforme supportate** selezionare i sistemi operativi in cui si vuole installare il profilo Wi-Fi. In alternativa, fare clic su **Seleziona tutto** per installare il profilo Wi-Fi in tutti i sistemi operativi disponibili.  

### <a name="next-steps"></a>Passaggi successivi
 Per informazioni su come distribuire il profilo Wi-Fi, vedere [Come distribuire profili Wi-Fi in System Center Configuration Manager](deploy-wifi-vpn-email-cert-profiles.md).  

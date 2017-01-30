---
title: Registrare dispositivi iOS con Device Enrollment Program (DEP) - Configuration Manager | Microsoft Docs
description: Abilitare la registrazione al programma DEP (Device Enrollment Program) per iOS per le distribuzioni ibride in Configuration Manager con Intune.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 78d44adc-9b1c-4bc6-b72d-e93873916ea6
caps.latest.revision: 9
author: mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 991eff171dce95590a7f050e0d3b07f98c0224b3
ms.openlocfilehash: 4222ca27e19ade46d53f8cd4598643ddd4fd5c8f

---
# <a name="ios-device-enrollment-program-dep-enrollment-for-hybrid-deployments-with-configuration-manager"></a>Registrazione al programma DEP (Device Enrollment Program) per iOS per le distribuzioni ibride con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le aziende possono acquistare dispositivi iOS tramite il programma DEP (Device Enrollment Program) di Apple e quindi gestirli tramite Microsoft Intune. Per gestire i dispositivi iOS di proprietà dell'azienda con il programma di registrazione dispositivi di Apple (DEP), le aziende devono completare i passaggi richiesti da Apple per partecipare al programma e acquistare i dispositivi attraverso il programma. I dettagli del processo sono disponibili in:  [https://deploy.apple.com](https://deploy.apple.com). I vantaggi del programma includono la configurazione dei dispositivi senza intervento dell'utente che non richiede la connessione USB di ogni dispositivo a un computer.  

 Per registrare i dispositivi iOS di proprietà dell'azienda con DEP, è necessario un token DEP di Apple. Questo token consente a Intune di sincronizzare le informazioni sui dispositivi di proprietà dell'azienda che partecipano a DEP. Consente anche a Intune di caricare profili di registrazione in Apple e di assegnare dispositivi a tali profili.  

## <a name="apple-dep-enrollment-for-ios-devices"></a>Registrazione con Apple DEP per i dispositivi iOS  
 Le procedure seguenti descrivono come specificare i dispositivi iOS acquistati tramite il programma DEP di Apple come dispositivi di proprietà dell'azienda gestiti da Intune. Quando l'utente accende il dispositivo per la prima volta, riceve il profilo di gestione DEP ed esegue Assistente configurazione per includere il dispositivo nella gestione.  

###  <a name="enable-dep-enrollment-in-configuration-manager-with-intune"></a>Abilitare la registrazione al programma DEP in Configuration Manager con Intune  

1.  **Iniziare a gestire dispositivi iOS con Configuration Manager**   
    Prima di registrare un dispositivo nel programma DEP (Device Enrollment Program) di iOS, è necessario completare la procedura di [impostazione della gestione dei dispositivi mobili ibrida](../../mdm/deploy-use/setup-hybrid-mdm.md) e la [procedura per il supporto della registrazione di iOS](../deploy-use/setup-hybrid-mdm.md#ios-and-mac-enrollment-setup).

2.  **Creare una richiesta di token DEP**   
    Nella console di Configuration Manager, nell'area di lavoro **Amministrazione**, espandere **Configurazione della gerarchia**, espandere **Servizi Cloud** e fare clic su **Sottoscrizioni a Windows Intune**. Fare clic su **Crea richiesta token DEP** nella scheda **Home** , su **Sfoglia** per specificare il percorso di download per la richiesta del token DEP e quindi su **Download**. Salvare il file di richiesta di token DEP (con estensione pem) localmente. Il file con estensione pem viene usato per richiedere un token di trust (con estensione p7m) dal portale del programma di registrazione dispositivi di Apple.  

3.  **Ottenere un token del programma di registrazione dispositivi**   
    Andare nel [portale del programma di registrazione dispositivi](https://deploy.apple.com) (https://deploy.apple.com) e accedere con l'ID Apple aziendale. Questo ID Apple dovrà essere usato in futuro per rinnovare il token DEP.  

    1.  Nell'area di lavoro [portale del programma di registrazione dispositivi](https://deploy.apple.com), passare a **Programma di registrazione dispositivi** > **Gestisci server**e quindi fare clic sull'opzione **Aggiungi server MDM**.  

    2.  Immettere il **nome del server MDM**e quindi fare clic sull'opzione **Avanti**. Il nome del server viene fornito come riferimento per identificare il server MDM. Non è il nome o l'URL del server di Intune o di Configuration Manager.  

    3.  Si apre la finestra di dialogo **Aggiungi <NomeServer\>**. Fare clic su **Scegli file** per caricare il file con estensione pem creato nel passaggio precedente e quindi fare clic su **Avanti**.  

    4.  La finestra di dialogo **Aggiungi <NomeServer\>** visualizza un collegamento **Token del server**. Scaricare il file token del server (.p7m) nel computer e quindi fare clic su **Fine**.  

     Questo file di certificato (.p7m) viene usato per stabilire una relazione di trust tra i server di Intune e del programma di registrazione dispositivi di Apple.  

4.  **Aggiungere il token DEP a Configuration Manager**   
    Nella console di Configuration Manager, nell'area di lavoro **Amministrazione**, espandere **Configurazione della gerarchia** e fare clic su **Sottoscrizioni a Windows Intune**. Fare clic su **Configura piattaforme** nella scheda **Home** e fare clic su **iOS**. Selezionare **Abilita programma registrazione dispositivo**, individuare il file del certificato (con estensione p7m), fare clic su **Apri**, **Carica**e quindi su **OK**.  

#### <a name="set-up-enrollment-for-apple-device-enrollment-program-dep-ios-devices"></a>Configurare la registrazione per i dispositivi iOS del programma di registrazione dispositivi di Apple  

1.  **Aggiungere un criterio di registrazione dispositivo aziendale**   
    Nella console di Configuration Manager, nell'area di lavoro **Asset e conformità**, espandere **Panoramica**, espandere **Dispositivi di proprietà dell'azienda**, espandere **iOS** e fare clic su **Profili di registrazione**. Fare clic su **Crea profilo** nella scheda **Home** per aprire la procedura guidata Crea profilo. Configurare le impostazioni nelle pagine seguenti:  

    1.  On the **Generale** specificare le seguenti informazioni e quindi fare clic su **Avanti**.  

        -   **Nome** : nome del profilo di registrazione dispositivi. (Non visibile agli utenti)  

        -   **Descrizione** : descrizione del profilo di registrazione dispositivi. (Non visibile agli utenti)  

        -   **Affinità utente** : specifica la modalità di registrazione dei dispositivi. Vedere [User affinity for hybrid managed devices in Configuration Manager](../../mdm/deploy-use/user-affinity-for-hybrid-managed-devices.md) (Affinità utente per i dispositivi gestiti ibridi in Configuration Manager).  

            -   **Richiedi affinità utente**: il dispositivo può essere associato a un utente durante la configurazione iniziale e potrebbe quindi accedere ai dati aziendali e alla posta elettronica come tale utente.  L'affinità utente deve essere configurata per i dispositivi gestiti da DEP appartengono agli utenti che devono usare il portale aziendale, ad esempio per installare le app.  

            > [!NOTE]
            > Per poter richiedere token utente, DEP con affinità utente richiede un endpoint misto/nome utente WS-Trust 1.3 Active Directory Federation Services.

            -   **Nessuna affinità utente**: il dispositivo non è associato a un utente. Usare questa associazione per i dispositivi che eseguono attività senza accedere ai dati utente locali. Le app che richiedono l'associazione utente non funzioneranno.  

    2.  On the **Programma di registrazione dispositivi** specificare le seguenti informazioni e quindi fare clic su **Avanti**.  

        -   **Reparto**:questa informazione viene visualizzata quando gli utenti toccano "Informazioni sulla configurazione" durante l'attivazione.  

        -   **Numero di telefono per supporto tecnico**: informazione visualizzata quando l'utente fa clic sul pulsante **Richiesta di assistenza** durante l'attivazione.  

        -   **Modalità di preparazione**: questo stato viene impostato durante l'attivazione e non può essere modificato senza ripristinare le impostazioni predefinite del dispositivo:  

            -   **Supervisione non eseguita**: funzionalità di gestione limitate  

            -   **Supervisione eseguita**: attiva altre opzioni di gestione e disattiva il blocco attivazione per impostazione predefinita  

        -   **Bloccare il profilo di registrazione nel dispositivo**: questo stato viene configurato durante l'attivazione e può essere modificato solo ripristinando le impostazioni predefinite.  

            -   **Disattiva**: consente la rimozione del profilo di gestione dal menu **Impostazioni**  

            -   **Abilita**: richiede **Modalità di preparazione** = **Supervisione eseguita**. Disattiva le impostazioni iOS che potrebbero consentire la rimozione del profilo di gestione  

    3.  Nella pagina **Assistente configurazione** configurare le impostazioni che consentono di personalizzare l'Assistente installazione iOS che viene avviato quando il dispositivo viene acceso per la prima volta e quindi fare clic su **Avanti**. Queste impostazioni includono:  
        -   **Passcode**: consente di richiedere un passcode durante l'attivazione. Richiedere sempre un passcode, a meno che il dispositivo non sia protetto o l'accesso al dispositivo non venga controllato in altro modo, ad esempio con la modalità tutto schermo, che limita l'uso del dispositivo a una sola app.  
        -   **Servizi di posizione**: se l'opzione è abilitata, Assistente configurazione richiede il servizio al momento dell'attivazione  
        -   **Ripristina**: se l'opzione è abilitata, Assistente configurazione richiede il backup in iCloud durante l'attivazione  
        -   **ID Apple**: è necessario un ID Apple per il download delle app da iOS App Store, incluse le app installate da Intune. Se l'opzione è abilitata, iOS richiede agli utenti un ID Apple quando Intune prova a installare un'applicazione senza ID.  
        -   **Termini e condizioni**: se l'opzione è abilitata, Assistente configurazione richiede di accettare i termini e le condizioni Apple durante l'attivazione  
        -   **Touch ID**: se l'opzione è abilitata, Assistente configurazione richiede questo servizio durante l'attivazione
        -   **Apple Pay**: se l'opzione è abilitata, Assistente configurazione richiede questo servizio durante l'attivazione
        -   **Zoom**: se l'opzione è abilitata, Assistente configurazione richiede questo servizio durante l'attivazione
        -   **Siri**: se l'opzione è abilitata, Assistente configurazione richiede questo servizio durante l'attivazione  
        -   **Inviare i dati di diagnostica ad Apple**: se l'opzione è abilitata, Assistente configurazione richiede questo servizio durante l'attivazione  

    4.  Nella pagina **Gestione aggiuntiva** specificare se è possibile usare una connessione USB per le impostazioni di gestione aggiuntive. Quando si seleziona **Richiedi certificato**, è necessario importare un certificato di gestione dello strumento di configurazione di Apple da usare per questo profilo.  Impostare su **Non consentire** per evitare la sincronizzazione di file con iTunes o la gestione tramite Apple Configurator. È consigliabile impostare questa opzione su **Non consentire**, esportare eventuali altre configurazioni da Apple Configurator e quindi eseguire la distribuzione come profilo di configurazione iOS personalizzato anziché usare questa impostazione per consentire la distribuzione manuale con o senza un certificato.  

        -   **Non consentire**: impedisce al dispositivo di comunicare tramite USB (disattiva l'associazione)  

        -   **Consenti**: consente al dispositivo di comunicare tramite una connessione USB con qualsiasi PC o Mac  

        -   **Richiedi certificato**: consente l'associazione a un Mac con un certificato importato nel profilo di registrazione  

2.  **Assegnare dispositivi DEP per la gestione**   
    Andare nel [portale del programma di registrazione dispositivi](https://deploy.apple.com) (https://deploy.apple.com) e accedere con l'ID Apple aziendale. Passare a **Programma di distribuzione** > **Programma di registrazione dispositivi** > **Gestione dei dispositivi**. Specificare come **scegliere i dispositivi**, indicare le informazioni sul dispositivo e specificare i dettagli in base al **numero di serie**, al **numero di ordine**o **caricando un file CSV**. Quindi, selezionare **Assegna al server**, selezionare il <*NomeServer*> specificato al passaggio 3 e quindi fare clic su **OK**.  

3.  **Sincronizzare i dispositivi gestiti da DEP**   
    Nell'area di lavoro **cmshort** workspace, passare a **Tutti i dispositivi di proprietà dell'azienda** > **iOS** > **Informazioni sul dispositivo**. Nella scheda **Home** fare clic su **Sincronizzazione DEP**. Viene inviata una richiesta di sincronizzazione ad Apple. Al termine della sincronizzazione, vengono visualizzati i dispositivi gestiti da DEP. Viene aperta la finestra di dialogo **stato di registrazione** dei dispositivi gestiti è **Non contattato** finché il dispositivo non viene acceso e non viene eseguito Assistente configurazione per la registrazione del dispositivo.  

4.  **Distribuire i dispositivi agli utenti**   
    Ora è possibile distribuire i dispositivi di proprietà dell'azienda agli utenti. Quando un dispositivo iOS viene attivato, viene registrato per la gestione con Intune.



<!--HONumber=Jan17_HO4-->



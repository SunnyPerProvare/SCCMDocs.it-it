---
title: Registrazione ibrida di iOS tramite Apple Configurator con Configuration Manager
descriptions: Pre-enroll iOS devices by using Apple Configurator with Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
caps.latest.revision: 5
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 19f4880d6e7ba3da2e4bcfe725c1c806ee3b3334


---
# <a name="ios-hybrid-enrollment-using-apple-configurator-with-configuration-manager"></a>Registrazione ibrida di iOS tramite Apple Configurator con Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le aziende che acquistano dispositivi iOS per l'uso da parte dei dipendenti possono gestire questi dispositivi tramite Microsoft Intune. È possibile eseguire la registrazione preliminare di dispositivi iOS collegandoli tramite USB a un computer Mac che esegue Apple Configurator. Prima della registrazione è necessario preparare un profilo Intune del dispositivo aziendale registrato nella console di Intune ed esportarlo nel computer Mac. Il processo di registrazione esegue il ripristino delle impostazioni predefinite del dispositivo e configura quest'ultimo attraverso il processo Assistente configurazione. La procedura seguente è consigliata per i dispositivi iOS dedicati, con un solo utente e usati per accedere alla posta elettronica di lavoro e alle risorse aziendali, ad esempio app e dati.  

##  <a name="a-namebkmksaea-apple-configurator-enrollment-via-setup-assistant"></a><a name="BKMK_SAE"></a> Registrazione con Apple Configurator tramite Assistente configurazione  
 Con Apple Configurator è possibile ripristinare le impostazioni predefinite dei dispositivi iOS in modo da prepararli per poter essere configurati dal nuovo utente del dispositivo.  Per questo metodo è necessario connettere tramite USB il dispositivo iOS a un computer Mac per configurare la registrazione aziendale e si presuppone l'uso di Apple Configurator 2.0.  

 **Prerequisiti**  

-   Accesso fisico ai dispositivi iOS  

-   Numeri di serie del dispositivo. [Come ottenere un numero di serie iOS](https://support.apple.com/en-us/HT204308)  

-   Cavi di connessione USB  

-   Computer Mac con [Apple Configurator 2.0](http://go.microsoft.com/fwlink/?LinkId=518017)  

#### <a name="enable-setup-assistant-enrollment-with-configuration-manager-and-intune"></a>Abilitare la registrazione di Assistente configurazione con Configuration Manager e Intune  

1.  **Aggiungere un profilo di registrazione dispositivo aziendale**   
    Nella console di Configuration Manager, nell'area di lavoro **Asset e conformità**, espandere **Panoramica**, espandere **Dispositivi di proprietà dell'azienda**, espandere **iOS** e fare clic su **Profili di registrazione**. Fare clic su **Crea profilo** nella scheda **Home** per aprire la procedura guidata Crea profilo. Configurare le impostazioni nelle pagine seguenti:  

    1.  On the **Generale** specificare le seguenti informazioni e quindi fare clic su **Avanti**.  

        -   **Nome** : nome del profilo di registrazione dispositivi. (Non visibile agli utenti)  

        -   **Descrizione** : descrizione del profilo di registrazione dispositivi. (Non visibile agli utenti)  

        -   **Affinità utente** : specifica la modalità di registrazione dei dispositivi. Per la maggior parte degli scenari di Assistente configurazione, usare **Richiedi affinità utente**.  

            -   **Richiedi affinità utente**: il dispositivo può essere associato a un utente durante la configurazione iniziale e potrebbe quindi accedere ai dati aziendali e alla posta elettronica come tale utente.  

            -   **Nessuna affinità utente**: il dispositivo non è associato a un utente. Usare questa associazione per i dispositivi che eseguono attività senza accedere ai dati utente locali. Le app che richiedono l'associazione utente non funzioneranno.  

    2.  Nella pagina **Programma di registrazione dispositivi** lasciare deselezionata la casella di controllo **Configurare le impostazioni del programma di registrazione dispositivi per questo profilo** e fare clic su **Avanti**.  

    3.  Esaminare il riepilogo e fare clic su Avanti.  

2.  **Aggiungere dispositivi iOS da registrare con Assistente configurazione**   
    Nella console di Configuration Manager, nell'area di lavoro **Asset e conformità**, espandere **Panoramica**, espandere **Dispositivi di proprietà dell'azienda**, espandere **iOS** e fare clic su **Informazioni sul dispositivo**. e quindi clic su **Aggiungi dispositivi**. È possibile aggiungere dispositivi in due modi:  

    - È possibile **caricare un file CSV contenente i numeri di serie**: creare un elenco delimitato da virgole con estensione csv composto da due colonne senza intestazione, con un limite di 5 MB o 5000 dispositivi per file. Per ogni riga, la prima cella corrisponde al numero di serie e la seconda corrisponde ai dettagli del dispositivo (facoltativi).

  Il file con estensione CSV quando viene visualizzato in un editor di testo viene visualizzato come:  

    ```  
    0000000,PO 1234  
    111111111,PO 1234  
    ```  

    - È anche possibile **aggiungere manualmente i numeri di serie e i dettagli**: immettere il numero di serie e i dettagli per un massimo di cinque dispositivi  

    Fare clic su **Avanti**.  

3.  **Selezionare i dispositivi da registrare**   
    Confermare i dispositivi da registrare. I numeri di serie già registrati o registrati in altro modo non possono essere importati. Fare clic su **Avanti** per continuare.  

4.  **Assegnare il profilo**   
    Specificare il profilo da assegnare ai dispositivi aggiunti dall'elenco dei profili disponibili, esaminare i **Dettagli del profilo di registrazione**, quindi fare clic su **Fine**. I dispositivi aggiunti manualmente possono essere assegnati a qualsiasi profilo di registrazione, ma i dispositivi sincronizzati con DEP devono essere assegnati a un profilo abilitato per DEP.  

5.  **Selezionare un profilo da distribuire ai dispositivi iOS**   
    Nella console di Configuration Manager, nell'area di lavoro **Asset e conformità**, espandere **Panoramica**, espandere **Tutti i dispositivi di proprietà dell'azienda**, espandere **iOS**, fare clic su **Profili di registrazione** e quindi selezionare il profilo da distribuire ai dispositivi mobili. Fare clic su **Esporta...** nella barra delle applicazioni. Copiare e salvare l'**URL del profilo**. Verrà caricato in Apple Configurator in un secondo momento per definire il profilo di Intune usato dai dispositivi iOS.  L'URL del profilo di registrazione è valido per due settimane quando viene esportato. Dopo due settimane, è necessario esportare un nuovo file URL per registrare i dispositivi iOS.  

     Per supportare Apple Configurator 2, è necessario modificare l'URL del profilo 2.0. Sostituire:  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     con:  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```  

6.  **Preparare il dispositivo con Apple Configurator**   
    I dispositivi iOS vengono connessi al computer Mac e registrati per la gestione dei dispositivi mobili.  

    > [!WARNING]  
    >  Le impostazioni predefinite dei dispositivi verranno ripristinate durante il processo di registrazione.  

    1.  In un computer Mac aprire **Apple Configurator 2**.  Sulla barra dei menu fare clic su **Apple Configurator 2** e quindi fare clic su **Preferenze**.  

    2.  Nel riquadro delle preferenze selezionare **Server** e fare clic sul simbolo "+" sotto il riquadro a sinistra per avviare la configurazione guidata del server MDM. Fare clic su **Avanti**.  

    3.  Immettere il **Nome** e l'**URL di registrazione** per il server MDM di cui al passaggio 5. Fare clic su **Avanti**.  

         Se si riceve un messaggio di avviso sui requisiti del profilo di attendibilità per Apple TV, è possibile disabilitare senza problemi l'opzione **Trust Profile** facendo clic sulla "X" grigia. Anche gli eventuali avvisi sul certificato Anchor possono essere ignorati. Per continuare, fare clic su **Avanti** fino al termine della procedura guidata.  

    4.  Nel riquadro **Server** fare clic su "Modifica" accanto al profilo del nuovo server. Assicurarsi che l'URL di registrazione corrisponda esattamente all'URL esportato da Intune. Immettere di nuovo l'URL originale se è diverso e **salvare** il profilo di registrazione esportato da Intune.  

    5.  Connettere i dispositivi mobili iOS al computer Apple con un adattatore USB.  

        > [!WARNING]  
        >  Le impostazioni predefinite dei dispositivi verranno ripristinate durante il processo di registrazione. È buona norma reimpostare il dispositivo e accenderlo. È consigliabile che sui dispositivi sia visualizzata la schermata Ciao quando si avvia l'Assistente configurazione.  

    6.  Fare clic su **Prepara**. Nel riquadro **Prepare iOS Device** (Prepara dispositivo iOS) selezionare **Manuale** e quindi fare clic su **Avanti**.  

    7.  Nel riquadro **Enroll in MDM Server** (Registra nel server MDM) selezionare il nome del server creato e quindi fare clic su **Avanti**.  

    8.  Nel riquadro **Enroll in MDM Server** (Registra nel server MDM) selezionare il nome del server creato e quindi fare clic su **Avanti**.  

    9. Nel riquadro **Create an Organization** (Crea organizzazione) scegliere un'organizzazione in **Organizzazione** oppure crearne una nuova e quindi fare clic su **Avanti**.  

    10. Nel riquadro **Configure iOS Setup Assistant** (Configura Assistente configurazione iOS) scegliere i passaggi presentati all'utente e quindi fare clic su **Prepara**. Se richiesto, eseguire l'autenticazione per aggiornare le impostazioni di attendibilità.  

    11. Terminata la preparazione del dispositivo iOS, è possibile scollegare il cavo USB.  

7.  **Distribuire i dispositivi**   
    I dispositivi sono ora pronti per la registrazione aziendale. Spegnere i dispositivi e distribuirli agli utenti. All'accensione dei dispositivi, verrà avviato l'Assistente configurazione e all'utente verrà richiesto di immettere l'account aziendale o dell'istituto di istruzione.



<!--HONumber=Nov16_HO1-->



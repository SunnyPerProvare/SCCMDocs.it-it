---
title: 'Registrare i dispositivi iOS con Apple Configurator '
titleSuffix: Configuration Manager
descriptions: Pre-enroll iOS devices by using Apple Configurator with Configuration Manager.
ms.date: 08/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 61a19d95-83ff-4ad8-9a67-f304d2ba54f2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 30520dbb336c444256ee73c4db1350c0f7aea6e8
ms.sourcegitcommit: 7f64c5fb3e9fa3dba006af618b1f1ceaf61a99f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/28/2019
ms.locfileid: "75520712"
---
# <a name="ios-hybrid-enrollment-using-apple-configurator-with-configuration-manager"></a>Registrazione ibrida di iOS tramite Apple Configurator con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Le aziende che acquistano dispositivi iOS per l'uso da parte dei dipendenti possono gestire questi dispositivi tramite Microsoft Intune. Per preparare i dispositivi iOS di proprietà dell'azienda per la registrazione, configurare un profilo di registrazione nella console di Configuration Manager e quindi esportare l'URL del profilo per l'uso da Apple Configurator. Per preparare il dispositivo iOS per la registrazione, connetterlo a un computer Mac tramite cavo USB e usare Apple Configurator per configurarlo. Apple Configurator ripristina le impostazioni predefinite del dispositivo e aggiunge il profilo di registrazione in modo che il dispositivo possa essere registrato quando l'utente lo accende per la prima volta ed esegue il processo di installazione guidata.

La procedura seguente è consigliata per i dispositivi iOS dedicati, con un solo utente e usati per accedere alla posta elettronica di lavoro e alle risorse aziendali, ad esempio app e dati.  

## <a name="prerequisites"></a>Prerequisiti  

-   Accesso fisico ai dispositivi iOS  

-   Numeri di serie del dispositivo. [Come ottenere un numero di serie iOS](https://support.apple.com/en-us/HT204308)  

-   Computer Mac con [Apple Configurator 2.0](https://go.microsoft.com/fwlink/?LinkId=518017)  

-   Cavi USB per connettere i dispositivi al computer Mac  

## <a name="add-a-corporate-owned-device-enrollment-profile"></a>Aggiungere un profilo di registrazione per dispositivi di proprietà dell'azienda

1.  Nella console di Configuration Manager fare clic su **Asset e conformità** > **Panoramica** > **Tutti i dispositivi di proprietà dell'azienda** > **iOS** > **Profili di registrazione**. Fare clic su **Crea profilo** per aprire la procedura guidata di creazione del profilo. Configurare le impostazioni nelle seguenti pagine.  

2.  Nella pagina **Generale** specificare le informazioni seguenti:  

    -   **Nome** (Non visibile agli utenti)  

    -   **Descrizione** (Non visibile agli utenti)  

    -   **Affinità utente** : specifica la modalità di registrazione dei dispositivi. Per la maggior parte degli scenari di Assistente configurazione, usare **Richiedi affinità utente**.  

        -   **Richiedi affinità utente**: il dispositivo può essere associato a un utente durante la configurazione iniziale e potrebbe quindi accedere ai dati aziendali e alla posta elettronica con questo nome utente.  

        -   **Nessuna affinità utente**: il dispositivo non è associato a un utente. Usare questa associazione per i dispositivi che eseguono attività senza accedere ai dati utente locali. Le app che richiedono l'associazione utente non funzioneranno.

    Fare clic su **Avanti** per continuare.  

3.  Nella pagina **Programma di registrazione dispositivi** lasciare deselezionata la casella di controllo **Configurare le impostazioni del programma di registrazione dispositivi per questo profilo** e fare clic su **Avanti**.  

4.  Esaminare il riepilogo e fare clic su **Avanti** per creare il profilo di registrazione. Fare clic su **Chiudi** per completare la procedura guidata. A questo punto è possibile aggiungere i numeri IMEI o i numeri di serie per i dispositivi da registrare.  

## <a name="predeclare-devices-to-enroll-with-setup-assistant"></a>Predichiarare i dispositivi da registrare con Assistente configurazione

In questo passaggio i dispositivi vengono predichiarati come proprietà dell'azienda specificando un elenco di identificatori di hardware (IMEI o numeri di serie).

Per altre informazioni, vedere [Predichiarare dispositivi con numeri IMEI o di serie iOS](predeclare-devices-with-hardware-id.md). Una volta completata l'attività, tornare a questa pagina per continuare con il passaggio successivo.

## <a name="export-the-profile-to-deploy-to-ios-devices"></a>Esportare il profilo da distribuire ai dispositivi iOS

1.  Nella console di Configuration Manager fare clic su **Asset e conformità** > **Panoramica** > **Tutti i dispositivi di proprietà dell'azienda** > **iOS** > **Profili di registrazione**.

2.  Selezionare il profilo di registrazione da distribuire ai dispositivi mobili e fare clic su **Esporta**.

3.  Copiare e salvare l'**URL del profilo** in un file modificabile.   

4.  Per supportare Apple Configurator 2 è necessario modificare l'URL del profilo 2.0. Sostituire la parte dell'URL seguente:  

    ```  
    https://manage.microsoft.com/EnrollmentServer/Discovery.svc/iOS/ESProxy?id=  

    ```  

     con:  

    ```  
    https://appleconfigurator2.manage.microsoft.com/MDMServiceConfig?id=  

    ```

5.  Salvare l'URL del profilo modificato. Verrà usato per aggiungere l'URL del profilo di registrazione in Apple Configurator nella [sezione successiva](#prepare-the-device-with-apple-configurator).  

> [!NOTE]
> L'URL del profilo di registrazione è valido per due settimane quando viene esportato. Dopo due settimane, è necessario esportare un nuovo URL per registrare i dispositivi iOS.

## <a name="prepare-the-device-with-apple-configurator"></a>Preparare il dispositivo con Apple Configurator

Per preparare i dispositivi iOS per la registrazione, collegare ogni dispositivo a un computer Mac e caricare il profilo di registrazione.  

> [!WARNING]  
>  Apple Configurator cancella e reimposta i dispositivi alle configurazioni predefinite.  

1. In un computer Mac aprire **Apple Configurator 2**.  

2. Sulla barra dei menu fare clic su **Apple Configurator 2** > **Preferenze**.  

3. Nel riquadro delle preferenze selezionare **Server** e fare clic sul simbolo "+" sotto il riquadro a sinistra per avviare la configurazione guidata del server MDM. Fare clic su **Avanti**.  

4. Immettere il **Nome** e l'**URL di registrazione** salvati [in precedenza](#export-the-profile-to-deploy-to-ios-devices). Fare clic su **Avanti**.  

   > [!NOTE]
   > Se si riceve un messaggio di avviso sui requisiti del profilo di attendibilità per Apple TV, è possibile disabilitare senza problemi l'opzione **Trust Profile** facendo clic sulla "X" grigia. Anche gli eventuali avvisi sul certificato Anchor possono essere ignorati.

   Per continuare, fare clic su **Next**  (Avanti) fino a completare la procedura guidata.  

5. Nel riquadro **Server** fare clic su "Modifica" accanto al profilo del nuovo server. Assicurarsi che l'URL di registrazione corrisponda esattamente all'URL immesso in precedenza. Se è diverso, immetterlo nuovamente e fare clic su **Salva**.  

6. Con un cavo USB, connettere un dispositivo iOS al computer Mac.  

   > [!WARNING]  
   >  Questo processo ripristina i dispositivi alle configurazioni predefinite. Prima di connettere il dispositivo, reimpostarlo e accenderlo. Come procedura consigliata, il dispositivo deve trovarsi sulla schermata iniziale prima di continuare.  

7. Fare clic su **Prepara**. Nel riquadro **Prepare iOS Device** (Prepara dispositivo iOS) selezionare **Manual** (Manuale) e quindi fare clic su **Next** (Avanti).  

8. Nel riquadro **Enroll in MDM Server** (Registra in server MDM) selezionare il nome del server creato e quindi fare clic su **Next** (Avanti).  

9. Nel riquadro **Create an Organization** (Crea organizzazione) scegliere un'organizzazione in **Organizzazione** oppure crearne una nuova e quindi fare clic su **Avanti**.  

10. Nel riquadro **Configure iOS Setup Assistant** (Configura Assistente configurazione iOS) scegliere i passaggi da presentare all'utente e quindi fare clic su **Prepare** (Prepara). Se richiesto, eseguire l'autenticazione per aggiornare le impostazioni di attendibilità.  

11. Al termine dell'operazione, è possibile disconnettere il cavo USB.  

Ripetere questi passaggi per tutti i dispositivi che si vuole preparare per la registrazione.

## <a name="distribute-devices"></a>Distribuire i dispositivi

I dispositivi sono ora pronti per la registrazione aziendale. Spegnere i dispositivi e distribuirli agli utenti. All'accensione dei dispositivi, verrà avviato l'Assistente configurazione e all'utente verrà richiesto di immettere l'account aziendale o dell'istituto di istruzione per iniziare la registrazione.

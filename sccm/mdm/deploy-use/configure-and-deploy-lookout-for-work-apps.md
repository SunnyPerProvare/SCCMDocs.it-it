---
title: Distribuire app Lookout for Work
titleSuffix: Configuration Manager
description: Configurare e distribuire l'app Lookout for Work.
ms.date: 05/31/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 3f62b763-4347-453d-b0a7-1f4a0d1d4105
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a4e829d92b099be3fbf77796ea604d9d33db252c
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62273660"
---
# <a name="configure-and-deploy-lookout-for-work-apps"></a>Configurare e distribuire l'app Lookout for Work

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo illustra come configurare e distribuire l'app Lookout for Work per i dispositivi Android e iOS.



## <a name="android-google-play-store-app"></a>Android (app Google Play Store)
1.  Nella console di Configuration Manager fare clic su **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.  

2.  Nella pagina **Generale** della Distribuzione guidata del software specificare le seguenti informazioni:  
    - Tipo: selezionare **Pacchetto app Android in Google Play**.
    - Percorso: copiare il collegamento dell'app Lookout for Work da Google Play Store e incollarlo qui
    - Server di pubblicazione: Lookout Mobile Security
    - Nome: Lookout for Work
    - Descrizione: Lookout offre la migliore protezione contro le minacce per dispositivi mobili per proteggere il dispositivo. Dopo l'installazione, l'app Lookout protegge il dispositivo dalle minacce che, se rilevate, vengono segnalate all'utente e all'amministratore IT.
    - Categoria amministrativa: Gestione computer  

    Al completamento, l'app Lookout for Work viene visualizzata nell'elenco di applicazioni.  

3.  Nella scheda **Home**, gruppo **Distribuzione**, scegliere **Distribuisci** per distribuire l'app Lookout for Work agli utenti.   
    >[!IMPORTANT]  
    >È necessario selezionare gli stessi utenti aggiunti all'opzione Enrollment Management (Gestisci registrazione) nella console di Lookout MTP.  

    Scegliere l'opzione **Installazione richiesta**. Questa opzione richiede l'installazione dell'app Lookout nel dispositivo dell'utente.  



## <a name="ios-enterprise-signed-version-of-lookout-app"></a>iOS (versione con firma aziendale dell'app Lookout)

1. Assicurarsi che la gestione iOS sia configurata nel dispositivo. Per istruzioni su come configurare il dispositivo per la gestione iOS, vedere [Configurare la gestione dei dispositivi iOS e Mac](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac).  

2. Firmare di nuovo l'app Lookout for Work per iOS. Lookout distribuisce la sua app Lookout for Work per iOS esternamente all'App Store iOS. Prima di distribuire l'app è necessario firmarla nuovamente con il certificato di sviluppatore aziendale iOS. Per istruzioni dettagliate su come firmare nuovamente le app Lookout for Work per iOS, vedere [Lookout for Work iOS app re-signing process](https://personal.support.lookout.com/hc/articles/114094038714) (Firmare nuovamente l'app Lookout for Work per iOS) nel sito di Lookout.  

3. Abilitare l'autenticazione Azure Active Directory (Azure AD) per gli utenti iOS.
   1.  Accedere al [pannello di Azure AD del portale di Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) e passare alla pagina di registrazione delle app.  
   2.  Specificare **app Lookout for Work per iOS** come Nome e selezionare **Nativa** come Tipo applicazione.  
   ![Schermata della finestra di dialogo Aggiungi applicazione con l'opzione Applicazione client nativa](media/aad-add-app-reg.png)

   3.  Per questo URI di reindirizzamento, usare il formato seguente: `lookoutwork://com.lookout.enterprise.<yourcompanyname>`, sostituendo `<yourcompanyname>` con il nome della società. Ad esempio: `lookoutwork://com.lookout.enterprise.contoso`
   4. Fare clic su **Crea** per creare l'app. 
   5.  Aprire la nuova app, fare clic su **Impostazioni** e aggiungere un URI di reindirizzamento aggiuntivo. Usare il formato seguente: `companyportal://code/<originalURI>`, dove `<originalURI>` è una versione con codifica URL dell'URI di reindirizzamento originale. Ad esempio: `companyportal://code/lookoutwork%3A%2F%2Fcom.lookout.enterprise.contoso`
   6.  Nelle impostazioni dell'app passare ad **Autorizzazioni necessarie** e fare clic su **Aggiungi**. Selezionare le autorizzazioni delegate seguenti:  

       | API  | Autorizzazione  |
       |---------|---------|
       | Lookout MTP     | Accesso a Lookout MTP         |
       | Microsoft Graph     | Accesso e lettura del profilo utente        |  

   Per altre informazioni, vedere [Configurare un'applicazione client nativa](/azure/app-service/app-service-mobile-how-to-configure-active-directory-authentication#optional-configure-a-native-client-application).  


4. In Configuration Manager caricare il file con estensione ipa firmato nuovamente. Impostare la versione minima del sistema operativo su iOS 8.0 o versioni successive. Per altre informazioni, vedere [Creare applicazioni iOS](/sccm/apps/get-started/creating-ios-applications).   


5. Creare criteri di configurazione delle app gestite. Per altre informazioni, vedere [Applicare le impostazioni alle app iOS con i criteri di configurazione app](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).  


6. Distribuire l'app Lookout for Work agli utenti. Per altre informazioni, vedere l'argomento relativo alla [distribuzione delle applicazioni](/sccm/apps/deploy-use/deploy-applications).  

   Selezionare gli stessi utenti aggiunti all'opzione Enrollment Management (Gestisci registrazione) nella console di Lookout. Scegliere l'opzione **Installazione richiesta**. Questa opzione richiede l'installazione dell'app Lookout nel dispositivo dell'utente.



## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>Cosa accade quando l'app distribuita viene aperta sul dispositivo

Quando l'utente apre Lookout for Work nel dispositivo, viene richiesta l'attivazione dell'app. L'utente deve scegliere di accedere con l'opzione Azure AD. Una procedura dettagliata con il flusso di lavoro per l'utente finale è disponibile in questi articoli:

- [Viene richiesto di installare Lookout for Work nel dispositivo Android](/intune-user-help/you-are-prompted-to-install-lookout-for-work-android)

- [È necessario risolvere una minaccia trovata da Lookout for Work](/intune-user-help/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)



## <a name="next-steps"></a>Passaggi successivi
- [Abilitare la regola di protezione dalle minacce per i dispositivi nei criteri di conformità](enable-device-threat-protection-rule-compliance-policy.md)

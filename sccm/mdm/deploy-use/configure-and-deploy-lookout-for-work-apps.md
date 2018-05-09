---
title: Distribuire app Lookout for Work
titleSuffix: Configuration Manager
description: Configurare e distribuire l'app Lookout for Work.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 3f62b763-4347-453d-b0a7-1f4a0d1d4105
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a812ed059bc0d96c23af986c2051416c26f6a15a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="configure-and-deploy-lookout-for-work-apps"></a>Configurare e distribuire l'app Lookout for Work

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo articolo illustra come configurare e distribuire l'app Lookout for Work per i dispositivi Android e iOS.

## <a name="android-google-play-store-app"></a>Android (app Google Play Store)
1.  Nella console di Configuration Manager fare clic su **Raccolta software** > **Gestione applicazioni** > **Applicazioni**.

2.  Nella pagina **Generale** della Distribuzione guidata del software specificare le seguenti informazioni:  
    - Tipo: selezionare **Pacchetto app Android in Google Play**.
    - Percorso: copiare il collegamento dell'app Lookout for Work da Google Play Store e incollarlo qui
    - Autore: Lookout Mobile Security
    - Nome: Lookout for Work
    - Descrizione: Lookout offre la migliore protezione contro le minacce per dispositivi mobili. Dopo l'installazione, l'app Lookout protegge il dispositivo dalle minacce che, se rilevate, vengono segnalate all'utente e all'amministratore IT.
    - Categoria amministrativa: Gestione computer  

    Al completamento, l'app Lookout for Work viene visualizzata nell'elenco di applicazioni.

3.  Nella scheda **Home**, gruppo **Distribuzione**, scegliere **Distribuisci** per distribuire l'app Lookout for Work agli utenti.   
    >[!IMPORTANT]  
    >È necessario selezionare gli stessi utenti aggiunti all'opzione Enrollment Management (Gestisci registrazione) nella console di Lookout MTP.  

    Scegliere l'opzione **Installazione richiesta**. Questa opzione richiede l'installazione dell'app Lookout nel dispositivo dell'utente.  



## <a name="ios-enterprise-signed-version-of-lookout-app"></a>iOS (versione con firma aziendale dell'app Lookout)

- **Passaggio 1:** Assicurarsi che la **gestione iOS** sia configurata sul dispositivo. Per istruzioni su come configurare il dispositivo per la gestione iOS, vedere [Configurare la gestione dei dispositivi iOS e Mac](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac).

- **Passaggio 2:** **Firmare nuovamente** l'app Lookout for Work per iOS. Lookout distribuisce la sua app Lookout for Work per iOS esternamente all'App Store iOS. **Prima di distribuire l'app** è necessario firmarla nuovamente con il certificato di sviluppatore aziendale iOS. Per istruzioni dettagliate su come firmare nuovamente le app Lookout for Work per iOS, vedere [Lookout for Work iOS app re-signing process](https://personal.support.lookout.com/hc/articles/114094038714) (Firmare nuovamente l'app Lookout for Work per iOS) nel sito di Lookout.


- **Passaggio 3:** Attivare l'autenticazione Azure Active Directory per gli utenti iOS seguendo questa procedura:
  1.  Accedere al [portale di gestione di Azure Active Directory](https:/portal.azure.com) e passare alla pagina delle applicazioni.
  2.  Aggiungere l'**app Lookout for Work per iOS** come **applicazione client nativa**.
  ![Schermata della finestra di dialogo Aggiungi applicazione con l'opzione Applicazione client nativa](media/aad-add-app.png)

  3. Sostituire a **com.lookout.enterprise.nomeazienda** l'ID bundle cliente selezionato alla firma dell'IPA.
  4.  Aggiungere l'URI di reindirizzamento supplementare: **&lt;portaleazienda://code/ >** seguito da una versione con codifica URL del proprio URI di reindirizzamento originale.
  5.  Aggiungere **Autorizzazioni delegate** all'app.

  Per altre informazioni, vedere [Configurare un'applicazione client nativa](/azure/app-service/app-service-mobile-how-to-configure-active-directory-authentication#optional-configure-a-native-client-application).


- **Passaggio 4:** Caricare il file con estensione IPA firmato di nuovo, come descritto nell'argomento [Create iOS applications with System Center Configuration Manager](/sccm/apps/get-started/creating-ios-applications) (Creare applicazioni iOS con System Center Configuration Manager). Impostare la versione minima del sistema operativo su iOS 8.0 o versioni successive.


- **Passaggio 5:** Creare i criteri di configurazione app gestita, come descritto nell'argomento [Configure iOS apps with mobile app configuration policies in Microsoft Intune](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies) (Configurare app iOS con criteri di configurazione app per dispositivi mobili in Microsoft Intune).


- **Passaggio 6:** **Per distribuire l'app agli utenti**, selezionare l'app Lookout for Work nella pagina **Applicazioni**, quindi nella scheda **Home**, gruppo **Distribuzione**, scegliere **Distribuisci**.

  Selezionare gli stessi utenti aggiunti all'opzione Enrollment Management (Gestisci registrazione) nella console di Lookout. Scegliere l'opzione **Installazione richiesta**. Questa opzione richiede l'installazione dell'app Lookout nel dispositivo dell'utente.



## <a name="what-happens-when-the-deployed-app-is-opened-on-the-device"></a>Cosa accade quando l'app distribuita viene aperta sul dispositivo

Quando l'utente apre Lookout for Work nel dispositivo, viene richiesta l'attivazione dell'app. L'utente deve scegliere di accedere con l'opzione Azure Active Directory. Una procedura dettagliata con il flusso di lavoro per l'utente finale è disponibile in questi articoli:

- [Viene richiesto di installare Lookout for Work nel dispositivo Android](/intune-user-help/you-are-prompted-to-install-lookout-for-work-android)

- [È necessario risolvere una minaccia trovata da Lookout for Work](/intune-user-help/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)



## <a name="next-steps"></a>Passaggi successivi
- [Abilitare la regola di protezione dalle minacce per i dispositivi nei criteri di conformità](enable-device-threat-protection-rule-compliance-policy.md)

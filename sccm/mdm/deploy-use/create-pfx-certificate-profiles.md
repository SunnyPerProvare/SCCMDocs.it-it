---
title: Creare profili certificato PFX | Microsoft Docs
description: Informazioni su come usare i file PFX in System Center Configuration Manager per generare i certificati specifici dell&quot;utente che supportano lo scambio di dati crittografati.
ms.custom: na
ms.date: 03/30/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
caps.latest.revision: 5
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 3b1451edaed69a972551bd060293839aa11ec8b2
ms.openlocfilehash: 2495cef2442706b343bac6d510946c1226b64cfc
ms.lasthandoff: 03/28/2017


---
# <a name="how-to-create-pfx-certificate-profiles-in-system-center-configuration-manager"></a>Come creare profili certificato PFX in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I profili certificato vengono usati con Servizi certificati Active Directory e il ruolo Servizio registrazione dispositivi di rete per effettuare il provisioning dei certificati di autenticazione per i dispositivi gestiti, in modo che gli utenti possano accedere facilmente alle risorse aziendali. Ad esempio, è possibile creare e distribuire profili certificato per fornire i certificati di cui gli utenti hanno bisogno per avviare connessioni VPN e wireless.

L'argomento [Introduzione ai profili certificato](../../protect/deploy-use/introduction-to-certificate-profiles.md) contiene informazioni generali sulla creazione e la configurazione dei profili certificato ed evidenzia alcune informazioni specifiche sui profili certificato relative ai certificati PFX.

-  Configuration Manager supporta la distribuzione dei certificati in più archivi di certificati, a seconda dei requisiti, del tipo di dispositivo e del sistema operativo. I dispositivi seguenti sono supportati quando vengono registrati con Intune:

 -   iOS  

- Per altri prerequisiti, vedere [Prerequisiti per i profili certificato](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

## <a name="pfx-certificate-profiles"></a>Profili certificato PFX
System Center Configuration Manager consente di eseguire il provisioning di file di scambio di informazioni personali (PFX) nei dispositivi dell'utente. I file con estensione pfx possono essere usati per generare certificati specifici dell'utente per supportare lo scambio di dati crittografati. I certificati PFX possono essere creati in Configuration Manager o importati.

> [!TIP]  
>  La procedura dettagliata che descrive questo processo è disponibile nel post relativo a [come creare e distribuire profili certificato PFX in Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx).  

## <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Creare e distribuire un profilo certificato PFX (Personal Information Exchange)  

### <a name="get-started"></a>Introduzione

1.  Nella console di System Center Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità**, **Accesso risorse aziendali**e quindi fare clic su **Profili certificati**.  

3.  Nella scheda **Home** del gruppo **Crea** fare clic su **Crea profilo certificato**.

4.  Nella pagina **Generale** della **Creazione guidata profilo certificato** specificare le informazioni seguenti:  

    -   **Nome**: immettere un nome univoco per il profilo certificato. È possibile usare un massimo di 256 caratteri.  

    -   **Descrizione**: digitare una descrizione che offra una panoramica del profilo certificato e altre informazioni rilevanti per facilitarne l'identificazione nella console di System Center Configuration Manager. È possibile usare un massimo di 256 caratteri.  

    -   **Specificare il tipo di profilo del certificato che si desidera creare**: per i certificati PFX, scegliere uno dei tipi seguenti:  

        -   **Scambio informazioni personali - Impostazioni PKCS #12 (PFX) - Importa**: selezionare questa opzione per importare un certificato PFX.  
        -   **Personal Information Exchange - Impostazioni PKCS #12 (PFX) - Crea**: selezionare questa opzione per creare un nuovo certificato PFX.

### <a name="import-a-pfx-certificate"></a>Importare un certificato PFX

Per importare un certificato PFX, è necessario Configuration Manager SDK. I certificati importati per un utente verranno distribuiti ai dispositivi registrati dall'utente.

1. Nella pagina **Certificato PFX** della **Creazione guidata profilo certificato** specificare la posizione in cui verrà archiviato il certificato nei dispositivi di destinazione:
    -     **Installa in TPM (Trusted Platform Module) se presente**  
    -   **Installa in TPM (Trusted Platform Module) in caso di errore** 
    -   **Installa in Windows Hello for Business oppure genera errore** 
    -   **Installa nel provider di archiviazione chiavi software** 
2. Fare clic su **Avanti**. 
3. Nella pagina **Piattaforme supportate** della procedura guidata scegliere le piattaforme per dispositivi in cui verrà installato il certificato e quindi fare clic su **Avanti**.
4. Tramite l'SDK per Windows 8.1 disponibile nell'Area download ([http://go.microsoft.com/fwlink/?LinkId=613525](http://go.microsoft.com/fwlink/?LinkId=613525), distribuire uno script di creazione PFX. Lo script di creazione PFX aggiunto in Configuration Manager 2012 SP2 aggiunge una classe SMS_ClientPfxCertificate all'SDK. Questa classe include i metodi seguenti:  

    -   ImportForUser  

    -   DeleteForUser  

     Script di esempio:  

```  
    $EncryptedPfxBlob = "<blob>"  
    $Password = "abc"  
    $ProfileName = "PFX_Profile_Name"  
    $UserName = "ComputerName\Administrator"  

    #New pfx  
    $WMIConnection = ([WMIClass]"\\nksccm\root\SMS\Site_MDM:SMS_ClientPfxCertificate")  
        $NewEntry = $WMIConnection.psbase.GetMethodParameters("ImportForUser")  
        $NewEntry.EncryptedPfxBlob = $EncryptedPfxBlob  
        $NewEntry.Password = $Password  
        $NewEntry.ProfileName = $ProfileName  
        $NewEntry.UserName = $UserName  
    $Resource = $WMIConnection.psbase.InvokeMethod("ImportForUser",$NewEntry,$null)  

```  

Le variabili di script seguenti devono essere modificate per lo script:  

   -   blob\ = blob crittografato con chiave Base64 PFX  
   -   $Password = password per il file PFX  
   -   $ProfileName = nome del profilo PFX  
   -   ComputerName = nome del computer host   

### <a name="create-a-new-pfx-certificate"></a>Creare un nuovo certificato PFX

Quando si crea e distribuisce un certificato PFX, lo stesso certificato verrà installato in tutti i dispositivi registrati dall'utente.

1. Nella pagina **Piattaforme supportate** della procedura guidata scegliere le piattaforme per dispositivi in cui verrà installato il certificato e quindi fare clic su **Avanti**.
2. Nella pagina **Autorità di certificazione** della procedura guidata configurare le opzioni seguenti:
    - **Sito primario**: selezionare il sito primario di Configuration Manager da cui si vuole selezionare un'autorità di certificazione.
    - **Autorità di certificazione**: dopo aver selezionato un sito primario, selezionare l'autorità di certificazione desiderata dall'elenco e quindi fare clic su **Avanti**.
3. Nella pagina **Certificato PFX** della procedura guidata configurare le opzioni seguenti:
    - **Soglia di rinnovo (%)**: specificare la percentuale di durata residua del certificato prima che il dispositivo richieda il rinnovo del certificato.
    - **Nome modello certificato**: fare clic su **Sfoglia** per selezionare il nome di un modello di certificato che è stato aggiunto a una CA emittente. Per selezionare modelli di certificato, l'account utente usato per eseguire la console di System Center Configuration Manager deve disporre dell'autorizzazione **Lettura** per il modello di certificato. In alternativa, digitare il nome del modello di certificato. 
    - **Formato nome soggetto**: dall'elenco selezionare in che modo Configuration Manager crea automaticamente il nome del soggetto nella richiesta di certificato. Se il certificato è per un utente, è anche possibile includere l'indirizzo di posta elettronica dell'utente nel nome del soggetto. Scegliere tra **Nome comune** e **Nome distinto completo**.
    - **Nome alternativo soggetto**: specificare in che modo Configuration Manager crea automaticamente i valori per il nome alternativo del soggetto nella richiesta di certificato. Ad esempio, se si seleziona un tipo di certificato utente, è possibile includere il nome dell'entità utente (UPN) nel nome alternativo oggetto. È possibile scegliere tra:
        - **Indirizzo di posta elettronica** 
        - **Nome dell'entità utente (UPN)** 
    - **Periodo di validità del certificato** - 
    - **Provider di archiviazione chiavi Windows** (visualizzato solo se si seleziona Windows come piattaforma supportata) 
        -     **Installa in TPM (Trusted Platform Module) se presente**  
        -   **Installa in TPM (Trusted Platform Module) in caso di errore** 
        -   **Installa in Windows Hello for Business oppure genera errore** 
        -   **Installa nel provider di archiviazione chiavi software** 
4. Fare clic su **Avanti**.

### <a name="finish-up"></a>Terminare

1.  Fare clic su **Avanti**, consultare la pagina **Riepilogo** e quindi chiudere la procedura guidata.  
2.  Il profilo certificato contenente il file PFX è ora disponibile nell'area di lavoro **Profili certificato** . 
3.  Per distribuire il profilo, nell'area di lavoro **Asset e conformità** aprire **Impostazioni di conformità** > **Accesso risorse aziendali** > **Profili certificati**, fare clic con il pulsante destro del mouse sul certificato desiderato e scegliere **Distribuisci**. 



## <a name="see-also"></a>Vedere anche
La sezione [Creare un nuovo profilo di certificato](../../protect/deploy-use/create-certificate-profiles.md#create-a-new-certificate-profile) illustra la Creazione guidata profilo certificato.

L'articolo [Distribuire profili in System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) contiene informazioni sulla distribuzione dei profili certificato.

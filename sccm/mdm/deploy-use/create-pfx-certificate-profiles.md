---
title: Creare profili certificato PFX | Microsoft Docs
description: Informazioni su come usare i file PFX in System Center Configuration Manager per generare i certificati specifici dell&quot;utente che supportano lo scambio di dati crittografati.
ms.custom: na
ms.date: 03/05/2017
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
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: eddecee8886296fb6132d7477afebbfc7fd280d1
ms.lasthandoff: 03/06/2017


---
# <a name="how-to-create-pfx-certificate-profiles-in-system-center-configuration-manager"></a>Come creare profili certificato PFX in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I profili certificato vengono usati con Servizi certificati Active Directory e il ruolo Servizio registrazione dispositivi di rete per effettuare il provisioning dei certificati di autenticazione per i dispositivi gestiti, in modo che gli utenti possano accedere facilmente alle risorse aziendali. Ad esempio, è possibile creare e distribuire profili certificato per fornire i certificati di cui gli utenti hanno bisogno per avviare connessioni VPN e wireless.

L'articolo [Introduzione ai profili certificato](../../protect/deploy-use/introduction-to-certificate-profiles.md) contiene informazioni generali sulla creazione e la configurazione dei profili certificato ed evidenzia alcune informazioni specifiche sui profili certificato relative alla gestione dei dispositivi mobili.

- I profili certificato garantiscono la registrazione e il rinnovo dei certificati di un'autorità di certificazione aziendale (CA) per i dispositivi che eseguono iOS, Windows 8.1, Windows RT 8.1, Windows 10 Desktop e Mobile e Android. Questi certificati possono poi essere usati per le connessioni Wi-Fi e VPN.

-  Per distribuire profili certificato che usano il protocollo SCEP, è necessario installare un modulo criteri per il servizio Registrazione dispositivi di rete (NDES) in un server che esegue Windows Server 2012 R2 con il ruolo Servizi certificati Active Directory e un servizio NDES attivo e accessibile per i dispositivi che richiedono i certificati. Per i dispositivi registrati da Microsoft Intune, il servizio NDES deve essere accessibile da Internet, ad esempio in una rete perimetrale.

-  Configuration Manager supporta la distribuzione dei certificati in più archivi di certificati, a seconda dei requisiti, del tipo di dispositivo e del sistema operativo. Sono supportati i dispositivi e i sistemi operativi seguenti:
 -   Windows RT 8.1  
 -   Windows 8.1  
 -   Windows Phone 8.1  
 -   Windows 10 Desktop e Mobile  
 -   iOS  
 -   Android  
 > [!IMPORTANT]  
 >  Per distribuire i profili nei dispositivi Android, iOS, Windows Phone e nei dispositivi registrati Windows 8.1 o versioni successive, tali dispositivi devono essere [registrati in Microsoft Intune](https://technet.microsoft.com/en-us/library/dn646962.aspx).   

- Per altri prerequisiti, vedere [Prerequisiti per i profili certificato](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

## <a name="pfx-certificate-profiles"></a>Profili certificato PFX
System Center Configuration Manager consente di eseguire il provisioning di file di scambio di informazioni personali (PFX) nei dispositivi dell'utente. I file con estensione pfx possono essere usati per generare certificati specifici dell'utente per supportare lo scambio di dati crittografati. I certificati PFX possono essere creati in Configuration Manager o importati. Con System Center Configuration Manager i certificati PFX nuovi o importati possono essere distribuiti nei dispositivi iOS, Android e Windows 10. Questi file possono quindi essere distribuiti in più dispositivi per supportare la comunicazione PKI basata sull'utente.  

> [!TIP]  
>  La procedura dettagliata che descrive questo processo è disponibile nel post relativo a [come creare e distribuire profili certificato PFX in Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx).  

### <a name="create-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Creare e distribuire un profilo certificato PFX (Personal Information Exchange)  

1.  Nella console di System Center Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità**, **Accesso risorse aziendali**e quindi fare clic su **Profili certificati**.  

3.  Nella scheda **Home** del gruppo **Crea** fare clic su **Crea profilo certificato**. Viene avviata la **Creazione guidata profilo certificato** .  

4.  Nella pagina **Generale** della **Creazione guidata profilo certificato** specificare le informazioni seguenti:  

    -   **Nome**: immettere un nome univoco per il profilo certificato. È possibile usare un massimo di 256 caratteri.  

    -   **Descrizione**: digitare una descrizione che offra una panoramica del profilo certificato e altre informazioni rilevanti per facilitarne l'identificazione nella console di System Center Configuration Manager. È possibile usare un massimo di 256 caratteri.  

    -   **Specificare il tipo di profilo del certificato che si desidera creare**: scegliere uno tipi di profilo certificato seguenti:  

        -   **Certificato CA attendibile**: selezionare questo tipo di profilo certificato se si vuole distribuire un certificato CA radice attendibile o un certificato CA intermedio per formare una catena di certificati attendibili quando l'utente o il dispositivo deve autenticare un altro dispositivo. Ad esempio, il dispositivo può essere un server RADIUS (Remote Authentication Dial-In User Service) o un server di rete privata virtuale (VPN). È anche necessario configurare un profilo certificato CA attendibile prima di creare un profilo certificato SCEP. In questo caso, il certificato CA attendibile deve essere un certificato radice trusted per la CA che rilascerà il certificato per l'utente o il dispositivo.  

        -   **Impostazioni di Simple Certificate Enrollment Protocol (SCEP)**: selezionare questo tipo di profilo certificato se si desidera richiedere un certificato per un utente o un dispositivo utilizzando il Simple Certificate Enrollment Protocol e il servizio del ruolo del servizio Registrazione dispositivi di rete.  

        -   **Scambio informazioni personali - Impostazioni PKCS #12 (PFX) - Importa**: selezionare questa opzione per importare un certificato PFX.  

5.  Nella finestra **Proprietà certificato** della **Creazione guidata profilo certificato** specificare dove verrà archiviato il certificato PFX nei dispositivi di destinazione.  

    -   **Installa in TPM (Trusted Platform Module) se presente**  

    -   **Installa in TPM (Trusted Platform Module) in caso di errore**  

    -   **Installa nel provider di archiviazione chiavi software**  

     Fare clic su **Avanti**.  

6.  Nella finestra **Piattaforme supportate** della **Creazione guidata profilo certificato** specificare quali sistemi operativi o piattaforme possono ricevere il file PFX importato.  

    -   **Windows 10**  

    -   **iPhone**  

    -   **iPad**  

    -   **Android**  

7.  Fare clic su **Avanti**, consultare la pagina **Riepilogo** e quindi chiudere la procedura guidata.  

8.  Il profilo certificato contenente il file PFX è ora disponibile nell'area di lavoro **Profili certificato** . Nella console di **Asset e conformità** andare a **Impostazioni di conformità** > **Accesso risorse aziendali** > **Profili certificati** e fare clic con il pulsante destro del mouse per distribuire il nuovo certificato in Raccolte utenti.  

9. Tramite l'SDK per Windows 8.1 disponibile nell'Area download ([http://go.microsoft.com/fwlink/?LinkId=613525](http://go.microsoft.com/fwlink/?LinkId=613525), distribuire uno script di creazione PFX. Lo script di creazione PFX aggiunto in Configuration Manager 2012 SP2 aggiunge una classe SMS_ClientPfxCertificate all'SDK. Questa classe include i metodi seguenti:  

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

    -   <blob\> = blob crittografato con chiave Base64 PFX  

    -   $Password = password per il file PFX  

    -   $ProfileName = nome del profilo PFX  

    -   ComputerName = nome del computer host  

### <a name="see-also"></a>Vedere anche
La sezione [Creare un nuovo profilo di certificato](../../protect/deploy-use/create-certificate-profiles.md#create-a-new-certificate-profile) illustra la Creazione guidata profilo certificato.

L'articolo [Distribuire profili in System Center Configuration Manager](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) contiene informazioni sulla distribuzione dei profili certificato.


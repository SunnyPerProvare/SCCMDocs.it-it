---
title: Creare profili certificato PFX importando i dettagli dei certificati | Microsoft Docs
description: Informazioni su come usare i file PFX in System Center Configuration Manager per generare i certificati specifici dell'utente che supportano lo scambio di dati crittografati.
ms.custom: na
ms.date: 04/04/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
caps.latest.revision: "5"
caps.handback.revision: "0"
author: lleonard-msft
ms.author: alleonar
manager: angrobe
ms.openlocfilehash: c8346d04c7cd9761291824f5d30f09fab9acbcf9
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="how-to-create-pfx-certificate-profiles-by-importing-certificate-details"></a>Creare profili certificato PFX importando i dettagli dei certificati

*Si applica a: System Center Configuration Manager (Current Branch)*


Questo argomento illustra come creare un profilo certificato tramite l'importazione delle credenziali da certificati esterni.  

L'argomento sui [profili certificato](../../protect/deploy-use/introduction-to-certificate-profiles.md) offre informazioni generali sulla creazione e sulla configurazione dei profili certificato ed evidenzia alcune informazioni specifiche sui profili certificato relative ai certificati PFX.

-  In Configuration Manager è disponibile un'ampia gamma di archivi certificati appropriati per sistemi operativi e dispositivi diversi.  Sono inclusi:

 -   iOS e MacOS/OSX
 -   Android e Android For Work
 -   Windows 10, incluso Windows 10 Mobile.

Per altre informazioni, vedere [Prerequisiti per i profili certificato](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

## <a name="pfx-certificate-profiles"></a>Profili certificato PFX
System Center Configuration Manager consente di importare credenziali di certificato e quindi di eseguire il provisioning di file di scambio di informazioni personali (con estensione pfx) nei dispositivi dell'utente. I file con estensione pfx possono essere usati per generare certificati specifici dell'utente per supportare lo scambio di dati crittografati.

> [!TIP]  
>  La procedura dettagliata che descrive questo processo è disponibile nel post relativo a [come creare e distribuire profili certificato PFX in Configuration Manager](http://blogs.technet.com/b/karanrustagi/archive/2015/09/01/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager.aspx).  

## <a name="create-import-and-deploy-a-personal-information-exchange-pfx-certificate-profile"></a>Creare, importare e distribuire un profilo certificato PFX  

### <a name="get-started"></a>Introduzione

1.  Nella console di System Center Configuration Manager fare clic su **Asset e conformità**.  
2.  Nell'area di lavoro **Asset e conformità** espandere **Impostazioni di conformità**, **Accesso risorse aziendali**e quindi fare clic su **Profili certificati**.  

3.  Nella scheda **Home** del gruppo **Crea** fare clic su **Crea profilo certificato**.

4.  Nella pagina **Generale** della **Creazione guidata profilo certificato** specificare le informazioni seguenti:  

    -   **Nome**: immettere un nome univoco per il profilo certificato. È possibile usare un massimo di 256 caratteri.  

    -   **Descrizione**: digitare una descrizione che offra una panoramica del profilo certificato e altre informazioni rilevanti per facilitarne l'identificazione nella console di System Center Configuration Manager. È possibile usare un massimo di 256 caratteri.  

    -   **Specificare il tipo di profilo certificato da creare**: per i certificati PFX, scegliere una delle opzioni seguenti:  

        -   **Scambio informazioni personali -- Impostazioni PKCS #12 (PFX) -- Importa**: crea un profilo certificato importando a livello di codice le informazioni da certificati esistenti.  

        -   **Personal Information Exchange -- Impostazioni di PKCS #12 (PFX) -- Crea**: crea un profilo certificato PFX usando credenziali fornite da una CA.  Per altre informazioni, vedere [Come creare profili certificato PFX usando un'autorità di certificazione](../../mdm/deploy-use/create-pfx-certificate-profiles.md).


### <a name="create-a-pfx-certificate-profile-for-the-imported-credentials"></a>Creare un profilo certificato PFX per le credenziali importate

Per importare un certificato PFX, è necessario distribuire uno script Crea PFX tramite Configuration Manager SDK. 

I certificati importati vengono distribuiti in seguito ai dispositivi registrati.

1. Nella pagina **Certificato PFX** della **Creazione guidata profilo certificato** specificare dove il provider di archiviazione delle chiavi dispositivo:
    -   **Installa in TPM (Trusted Platform Module) se presente**  
    -   **Installa in TPM (Trusted Platform Module) in caso di errore** 
    -   **Installa in Windows Hello for Business oppure genera errore** 
    -   **Installa nel provider di archiviazione chiavi software** 
2. Fare clic su **Avanti**. 
3. Nella pagina **Piattaforme supportate** della procedura guidata scegliere le piattaforme per dispositivi supportate e quindi fare clic su **Avanti**.

### <a name="finish-the-profile"></a>Completare il profilo

1.  Fare clic su **Avanti**, consultare la pagina **Riepilogo** e quindi chiudere la procedura guidata.  
2.  Il profilo certificato contenente il file PFX è ora disponibile nell'area di lavoro **Profili certificato** . 
3.  Per distribuire il profilo, nell'area di lavoro **Asset e conformità** aprire **Impostazioni di conformità** > **Accesso risorse aziendali** > **Profili certificati**, fare clic con il pulsante destro del mouse sul certificato desiderato e scegliere **Distribuisci**. 

### <a name="deploy-a-create-pfx-script"></a>Distribuire uno script Crea PFX

Per distribuire uno script Crea PFX, usare [Configuration Manager SDK](http://go.microsoft.com/fwlink/?LinkId=613525). 

Lo script di creazione PFX aggiunto in Configuration Manager 2012 SP2 aggiunge una classe SMS_ClientPfxCertificate all'SDK. Questa classe include i metodi seguenti:  

    -   `ImportForUser`  

    -   `DeleteForUser`  

L'esempio seguente importa le credenziali in un profilo certificato PFX.

``` powershell
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

Per usare questo esempio, aggiornare le variabili di script seguenti:  

   -   **blob**\ : blob crittografato con chiave Base64 PFX  
   -   **$Password**: password per il file PFX  
   -   **$ProfileName**: nome del profilo PFX  
   -   **ComputerName**: nome del computer host   

## <a name="see-also"></a>Vedere anche
La sezione [Creare un nuovo profilo di certificato](../../protect/deploy-use/create-certificate-profiles.md) illustra la Creazione guidata profilo certificato.

[How to create PFX certificate profiles by importing certificate details](../../mdm/deploy-use/create-pfx-certificate-profiles.md) (Come creare i profili certificato PFX importando i dettagli dei certificati)

[Distribuire profili Wi-Fi, VPN, certificato e di posta elettronica](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md) descrive come distribuire profili certificato.
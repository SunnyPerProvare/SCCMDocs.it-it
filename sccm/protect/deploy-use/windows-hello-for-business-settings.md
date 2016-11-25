---
title: Impostazioni di Windows Hello per le aziende | System Center Configuration Manager
description: Informazioni su come integrare Windows Hello per le aziende con System Center Configuration Manager.
ms.custom: na
ms.date: 10/10/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
caps.latest.revision: 17
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2a45cfb3e00d8078fbf45bdc8a2668b7dd0a62c6
ms.openlocfilehash: 80f586763d034891aac9b87dcb38120602aa2b85


---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>Impostazioni di Windows Hello for Business in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager consente l'integrazione con Windows Hello per le aziende (in precedenza Microsoft Passport per Windows), che rappresenta un metodo di accesso alternativo per i dispositivi Windows 10. Hello for Business usa Active Directory o un account di Azure Active Directory per sostituire una password, una smart card o una smart card virtuale.  

Hello for Business consente di eseguire l'accesso usando un **movimento dell'utente** anziché una password. Il movimento dell'utente può essere un semplice PIN, un'autenticazione biometrica o un dispositivo esterno come un lettore di impronte digitali.  

 Configuration Manager si integra con Windows Hello per le aziende in due modi:  

-   È possibile usare Configuration Manager per controllare i movimenti che gli utenti possono utilizzare o meno per l'accesso.  

-   È possibile archiviare i certificati di autenticazione nel provider di archiviazione chiavi (KSP) di Windows Hello for Business. Per altre informazioni, vedere i [profili certificato](introduction-to-certificate-profiles.md).  

- È possibile distribuire i criteri di Windows Hello per le aziende su dispositivi appartenenti a un dominio Windows 10 che eseguono il client di Configuration Manager. Questa configurazione è descritta di seguito in [Configurare Windows Hello per le aziende su dispositivi appartenenti a un dominio Windows 10](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices). Quando si usa Configuration Manager con Intune (ibrido), è possibile configurare queste impostazioni nei dispositivi Windows 10 e Windows 10 Mobile, ma non su dispositivi appartenenti a un dominio che eseguono il client di Configuration Manager.   

## <a name="configure-windows-hello-for-business-settings-hybrid"></a>Configurare le impostazioni di Windows Hello per le aziende (ibrido)  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Servizi cloud** > **Sottoscrizioni a Microsoft Intune**.  

3.  Nell'elenco selezionare la sottoscrizione a Microsoft Intune e quindi nel gruppo **Sottoscrizione** della scheda **Home** fare clic su **Configura piattaforme** > **Windows (MDM)**.  

4.  Nella scheda **Windows Hello for Business** della finestra di dialogo **Sottoscrizione a Microsoft Intune - Proprietà** scegliere tra i valori seguenti, che avranno effetto sui tutti i dispositivi Windows 10 e Windows 10 Mobile registrati:  

    -   **Disabilita Windows Hello for Business per i dispositivi registrati** o **Abilita Windows Hello for Business per i dispositivi registrati** - Abilita o disabilita l'uso di Windows Hello for Business in tutti i dispositivi Windows 10 e Windows 10 Mobile registrati.  

    -   **Usa un modulo TPM (Trusted Platform Module)** - Un chip TPM (Trusted Platform Module) offre un livello aggiuntivo di sicurezza dei dati. Scegliere uno dei valori seguenti:  

        -   **Obbligatorio** (impostazione predefinita) - Solo i dispositivi con un modulo TPM accessibile possono eseguire il provisioning di Windows Hello for Business.  

        -   **Preferito** - I dispositivi tentano innanzitutto di usare un modulo TPM. Se questo non è disponibile, possono usare la crittografia software.  

    -   **Richiedi lunghezza minima del PIN** - Specificare il numero minimo di caratteri necessari per il PIN di Windows Hello for Business. È necessario usare almeno 4 caratteri (il valore predefinito è 6 caratteri).  

    -   **Richiedi lunghezza massima del PIN** - Specificare il numero massimo di caratteri consentiti per il PIN di Windows Hello for Business. È possibile usare fino a 127 caratteri.  

    -   **Richiedi lettere minuscole nel PIN** - Specifica se è necessario usare lettere minuscole nel PIN di Windows Hello for Business. È possibile scegliere tra:  

        -   **Consentito** - Gli utenti possono usare caratteri minuscoli nel PIN.  

        -   **Obbligatorio** - Gli utenti devono includere almeno un carattere minuscolo nel PIN.  

        -   **Non consentito** (impostazione predefinita) - Gli utenti non possono usare caratteri minuscoli nel PIN.  

    -   **Richiedi lettere maiuscole nel PIN** - Specifica se è necessario usare lettere maiuscole nel PIN di Windows Hello for Business. È possibile scegliere tra:  

        -   **Consentito** - Gli utenti possono usare caratteri maiuscoli nel PIN.  

        -   **Obbligatorio** - Gli utenti devono includere almeno un carattere maiuscolo nel PIN.  

        -   **Non consentito** (impostazione predefinita) - Gli utenti non possono usare caratteri maiuscoli nel PIN.  

    -   **Richiedi caratteri speciali** - Specifica l'uso di caratteri speciali nel PIN. È possibile scegliere tra:  

        -   **Consentito** - Gli utenti possono usare caratteri speciali nel PIN.  

        -   **Obbligatorio** - Gli utenti devono includere almeno un carattere speciale nel PIN.  

        -   **Non consentito** (impostazione predefinita) - Gli utenti non possono usare caratteri speciali nel PIN (questo è anche il comportamento se l'impostazione non è configurata).  

         I caratteri speciali includono: **! " # $ % & ' ( ) \* + , - . / : ; < = > ? @ [ \ ] ^ _ ` { &#124; } ~**.  

    -   **Richiedi scadenza PIN (giorni)** - Specifica il numero di giorni prima che sia necessario modificare il PIN del dispositivo. L'impostazione predefinita è 41 giorni.  

    -   **Impedisci riutilizzo dei PIN precedenti** - Usare questa impostazione per limitare il riutilizzo dei PIN usati in precedenza. L'impostazione predefinita impedisce il riutilizzo degli ultimi 5 PIN usati.  

    -   **Abilita movimenti biometrici** - Abilita l'autenticazione biometrica, ad esempio il riconoscimento facciale o delle impronte digitali, come alternativa a un PIN di Windows Hello for Business.. Gli utenti devono comunque configurare un PIN aziendale in caso di errore dell'autenticazione biometrica.  

         Se impostato su **Abilitato**, Windows Hello for Business consente l'autenticazione biometrica.  Se impostato su **Disabilitato**, Windows Hello for Business impedisce l'autenticazione biometrica (per tutti i tipi di account).  

    -   **Usa anti-spoofing avanzato, se disponibile** - Configura l'uso della funzionalità avanzata di anti-spoofing nei dispositivi che la supportano.  

         Se impostato su **Abilitato**, Windows richiede a tutti gli utenti di usare la funzionalità di anti-spoofing per le caratteristiche del viso, se supportata.  

    -   **Usare Passport remoto** - Se questa opzione è impostata su **Abilitato**, gli utenti possono usare Hello for Business come dispositivo portatile complementare per l'autenticazione del computer desktop. Il computer desktop deve essere aggiunto ad Azure Active Directory e il dispositivo complementare deve essere configurato con un PIN di Windows Hello for Business.  

5.  Al termine, fare clic su **OK**.  


## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>Configurare Windows Hello per le aziende su dispositivi appartenenti a un dominio Windows 10
È possibile controllare le impostazioni di Windows Hello per le aziende nei dispositivi appartenenti a un dominio Windows 10 in tre modi:

- È possibile creare e distribuire un profilo Windows Hello per le aziende. Questo è l'approccio consigliato.
- È possibile usare criteri di gruppo.  
- È possibile usare uno script PowerShell.

Si noti che, oltre a questa configurazione, è necessario distribuire anche un profilo certificato, come descritto in [Configurare un profilo certificato](#configure-a-certificate-profile).

### <a name="recommended-approach---configure-a-windows-hello-for-business-profile"></a>Approccio consigliato - Configurare un profilo Windows Hello per aziende  

Nella console di amministrazione, in **Accesso risorse aziendali **, fare clic con il pulsante destro del mouse su **Profili Windows Hello per le aziende** e scegliere **Nuovo** per avviare la creazione guidata del profilo. Specificare le impostazioni richieste dalla procedura guidata, rivedere e confermare le impostazioni nell'ultima pagina, quindi scegliere **Chiudi**. Di seguito è riportato un esempio di come potrebbero essere le impostazioni:  

![Impostazioni di Windows Hello for Business](../media/Hello-for-Business-settings.png)

### <a name="configure-windows-hello-for-business-with-group-policy-in-active-directory"></a>Configurare Windows Hello per le aziende con criteri di gruppo in Active Directory  

È possibile usare Criteri di gruppo di Active Directory per configurare i dispositivi appartenenti a un dominio Windows 10 allo scopo di eseguire il provisioning delle credenziali Hello per le aziende di un utente quando questi accede a Windows:

1.  In un computer Windows Server aprire Server Manager e passare a **Strumenti** > **Gestione criteri di gruppo**.    

2.  Nella finestra di dialogo **Gestione criteri di gruppo** espandere il dominio in cui si vuole abilitare l'aggiunta automatica alla rete aziendale.    

3.  Fare clic con il pulsante destro del mouse su **Oggetti Criteri di gruppo**e quindi scegliere **Nuovo**.  

4.  Nella finestra di dialogo **Nuovo oggetto Criteri di gruppo** immettere un nome per il nuovo oggetto Criteri di gruppo, ad esempio **Abilita Windows Hello for Business per i dispositivi registrati**, quindi fare clic su **OK**.  

5.  Nel nodo **Oggetti Criteri di gruppo** fare clic con il pulsante destro del mouse sull'oggetto appena creato e quindi scegliere **Modifica**.  

6.  Nella console di **Editor Gestione Criteri di gruppo** passare a **Configurazione computer** > **Criteri** > **Modelli amministrativi** > **Componenti di Windows** > **Windows Hello per le aziende**.  

7.  Fare clic con il pulsante destro del mouse su **Abilita Windows Hello for Business per i dispositivi registrati ** e quindi fare clic su **Modifica**.   

8.  Selezionare **Abilitato**, fare clic su **Applica**e quindi su **OK**.

È ora possibile collegare l'oggetto Criteri di gruppo creato nella posizione desiderata. Ad esempio:    

   Una specifica unità organizzativa in Active Directory, in cui saranno disponibili i computer appartenenti a un dominio Windows 10.    

   Un gruppo di sicurezza specifico contenente i computer appartenenti a un dominio Windows 10 che verranno registrati automaticamente con Azure AD.    

#### <a name="configure-windows-hello-for-business-by-deploying-a-powershell-script-with-configuration-manager"></a>Configurare Windows Hello per le aziende tramite la distribuzione di uno script PowerShell con Configuration Manager    
È possibile creare e distribuire lo script PowerShell seguente usando la gestione delle applicazioni di Configuration Manager.    

```    
powershell.exe -ExecutionPolicy Bypass -NoLogo -NoProfile -Command "& {New-ItemProperty "HKLM:\Software\Policies\Microsoft\PassportForWork" -Name "Enabled" -Value 1 -PropertyType "DWord" -Force}"  
```  

Per informazioni introduttive sulla gestione delle applicazioni di Configuration Manager, vedere [Introduction to application management in System Center Configuration Manager](/sccm/apps/understand/introduction-to-application-management) (Introduzione alla gestione delle applicazioni in System Center Configuration Manager).  

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>Configurare un profilo certificato per registrare il certificato di registrazione di Windows Hello for Business in Configuration Manager  
 Se si vuole usare l'accesso basato sui certificati di Windows Hello for Business o Microsoft Hello, configurare quanto segue:  

-   Un profilo certificato in Configuration Manager.  

-   Nel profilo certificato selezionare un modello che usi l'utilizzo chiavi avanzato per l'accesso smart card.  

 Per altre informazioni, vedere i [profili certificato](introduction-to-certificate-profiles.md).  

### <a name="see-also"></a>Vedere anche  
 [Protect data and site infrastructure with System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md) (Proteggere i dati e l'infrastruttura del sito con System Center Configuration Manager)

 [Manage identity verification using Windows Hello for Business](https://technet.microsoft.com/itpro/windows/keep-secure/manage-identity-verification-using-microsoft-passport) (Gestire la verifica dell'identità tramite Windows Hello per le aziende).  



<!--HONumber=Nov16_HO1-->



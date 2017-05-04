---
title: Impostazioni di Windows Hello for Business | Microsoft Docs
description: Informazioni su come integrare Windows Hello per le aziende con System Center Configuration Manager.
ms.custom: na
ms.date: 04/25/2017
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
ms.sourcegitcommit: 699b79b68440b61904a9053e5004318a2a248bfd
ms.openlocfilehash: 75def95561feb35f2f060f0daa72291983324d4f
ms.lasthandoff: 04/25/2017


---
# <a name="windows-hello-for-business-settings-in-system-center-configuration-manager"></a>Impostazioni di Windows Hello for Business in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager consente l'integrazione con Windows Hello per le aziende (in precedenza Microsoft Passport per Windows), che rappresenta un metodo di accesso alternativo per i dispositivi Windows 10. Hello for Business usa Active Directory o un account di Azure Active Directory per sostituire una password, una smart card o una smart card virtuale.  

Hello for Business consente di eseguire l'accesso usando un **movimento dell'utente** anziché una password. Il movimento dell'utente può essere un semplice PIN, un'autenticazione biometrica o un dispositivo esterno come un lettore di impronte digitali.

[Altre informazioni su Windows Hello for Business](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)

 Configuration Manager si integra con Windows Hello per le aziende in due modi:  

-   È possibile usare Configuration Manager per controllare i movimenti che gli utenti possono utilizzare o meno per l'accesso.  

-   È possibile archiviare i certificati di autenticazione nel provider di archiviazione chiavi (KSP) di Windows Hello for Business. Per altre informazioni, vedere i [profili certificato](introduction-to-certificate-profiles.md).  

- È possibile distribuire i criteri di Windows Hello per le aziende su dispositivi appartenenti a un dominio Windows 10 che eseguono il client di Configuration Manager. Questa configurazione è descritta di seguito in [Configurare Windows Hello per le aziende su dispositivi appartenenti a un dominio Windows 10](#configure-windows-hello-for-business-on-domain-joined-windows-10-devices). Quando si usa Configuration Manager con Intune (ibrido), è possibile configurare queste impostazioni nei dispositivi Windows 10 e Windows 10 Mobile, ma non su dispositivi appartenenti a un dominio che eseguono il client di Configuration Manager. Per altre informazioni, vedere [Configurare le impostazioni di Windows Hello for Business (ibrido)](../../mdm/deploy-use/windows-hello-for-business-settings.md).

## <a name="configure-windows-hello-for-business-on-domain-joined-windows-10-devices"></a>Configurare Windows Hello per le aziende su dispositivi appartenenti a un dominio Windows 10
È possibile controllare le impostazioni di Windows Hello per le aziende nei dispositivi appartenenti a un dominio Windows 10 in tre modi:

- È possibile creare e distribuire un profilo Windows Hello per le aziende. Questo è l'approccio consigliato.
- È possibile usare criteri di gruppo.  
- È possibile usare uno script PowerShell.

Si noti che, oltre a questa configurazione, è necessario distribuire anche un profilo certificato, come descritto in [Configurare un profilo certificato](#configure-a-certificate-profile).

## <a name="configure-a-windows-hello-for-business-profile"></a>Configurare un profilo Windows Hello for Business  

Nella console di Configuration Manager, in **Accesso risorse aziendali**, fare clic con il pulsante destro del mouse su **Profili Windows Hello for Business** e scegliere **Nuovo** per avviare la creazione guidata del profilo. Specificare le impostazioni richieste dalla procedura guidata, rivedere e confermare le impostazioni nell'ultima pagina, quindi scegliere **Chiudi**. Di seguito è riportato un esempio di come potrebbero essere le impostazioni:  

![Impostazioni di Windows Hello for Business](../media/Hello-for-Business-settings.png)

## <a name="configure-windows-hello-for-business-with-group-policy-in-active-directory"></a>Configurare Windows Hello per le aziende con criteri di gruppo in Active Directory  

È possibile usare Criteri di gruppo di Active Directory per configurare i dispositivi appartenenti a un dominio Windows 10 allo scopo di eseguire il provisioning delle credenziali Hello per le aziende di un utente quando questi accede a Windows:

1.  In un computer Windows Server aprire Server Manager e passare a **Strumenti** > **Gestione criteri di gruppo**.    

2.  Nella finestra di dialogo **Gestione criteri di gruppo** espandere il dominio in cui si vuole abilitare l'aggiunta automatica alla rete aziendale.    

3.  Fare clic con il pulsante destro del mouse su **Oggetti Criteri di gruppo**e quindi scegliere **Nuovo**.  

4.  Nella finestra di dialogo **Nuovo oggetto Criteri di gruppo** immettere un nome per il nuovo oggetto Criteri di gruppo, ad esempio **Abilita Windows Hello for Business per i dispositivi registrati**, quindi fare clic su **OK**.  

5.  Nel nodo **Oggetti Criteri di gruppo** fare clic con il pulsante destro del mouse sull'oggetto appena creato e quindi scegliere **Modifica**.  

6.  Nella console di **Editor Gestione Criteri di gruppo** passare a **Configurazione computer** > **Criteri** > **Modelli amministrativi** > **Componenti di Windows** > **Windows Hello per le aziende**.  

7.  Fare clic con il pulsante destro del mouse su **Abilita Windows Hello for Business per i dispositivi registrati**  e quindi fare clic su **Modifica**.   

8.  Selezionare **Abilitato**, fare clic su **Applica**e quindi su **OK**.

È ora possibile collegare l'oggetto Criteri di gruppo creato nella posizione desiderata. Ad esempio:    

   Una specifica unità organizzativa in Active Directory, in cui saranno disponibili i computer appartenenti a un dominio Windows 10.    

   Un gruppo di sicurezza specifico contenente i computer appartenenti a un dominio Windows 10 che verranno registrati automaticamente con Azure AD.    

## <a name="configure-windows-hello-for-business-by-deploying-a-powershell-script-with-configuration-manager"></a>Configurare Windows Hello per le aziende tramite la distribuzione di uno script PowerShell con Configuration Manager    
È possibile creare e distribuire lo script PowerShell seguente usando la gestione delle applicazioni di Configuration Manager.    

**powershell.exe -ExecutionPolicy Bypass -NoLogo -NoProfile -Command "& {New-ItemProperty "HKLM:\Software\Policies\Microsoft\PassportForWork" -Name "Enabled" -Value 1 -PropertyType "DWord" -Force}" ** 

Per informazioni introduttive sulla gestione delle applicazioni di Configuration Manager, vedere [Introduction to application management in System Center Configuration Manager](/sccm/apps/understand/introduction-to-application-management) (Introduzione alla gestione delle applicazioni in System Center Configuration Manager).  

## <a name="configure-a-certificate-profile-to-enroll-the-windows-hello-for-business-enrollment-certificate-in-configuration-manager"></a>Configurare un profilo certificato per registrare il certificato di registrazione di Windows Hello for Business in Configuration Manager  
 Se si vuole usare l'accesso basato sui certificati di Windows Hello for Business o Microsoft Hello, configurare quanto segue:  

-   Un profilo certificato in Configuration Manager.  

-   Nel profilo certificato selezionare un modello che usi l'utilizzo chiavi avanzato per l'accesso smart card.  

-    Se si vogliono archiviare i profili certificato nel contenitore chiave Windows Hello for Business e il profilo certificato usa l'EKU **Accesso smart card**, è necessario configurare le autorizzazioni seguenti per la registrazione delle chiavi per assicurarsi che il certificato venga convalidato correttamente.
È necessario aver prima creato il gruppo **Key Admins** e aggiunto tutti i computer del gruppo di gestione di Configuration Manager come membri del gruppo.

    1.    Accedere a un controller di dominio o a workstation di gestione con le credenziali di amministratore di dominio o equivalenti.
    2.    Aprire **Utenti e computer di Active Directory**.
    3.    Nel riquadro di spostamento fare clic con il pulsante destro del mouse sul nome di dominio e scegliere **Proprietà**.
    4.    Nella scheda**Sicurezza** della finestra di dialogo *<domain name>* **Proprietà** fare clic su **Avanzate**. Se la scheda **Sicurezza** non è visualizzata, attivare **Funzionalità avanzate** dal menu **Visualizza** di **Utenti e computer di Active Directory**.
    5.    Fare clic su **Aggiungi**.
    6.    Nella finestra di dialogo **Voci di autorizzazione per** *<domain name>* fare clic su **Selezionare un'entità**.
    7.    Nella finestra di dialogo **Select User, Computer, Service Account, or Group** (Seleziona utente, computer, account di servizio o gruppo) digitare **Key Admins** nella casella di testo **Inserire il nome oggetto da selezionare**.  Fare clic su **OK**.
    8.    Dall'elenco **Si applica a** scegliere **Oggetti Utente discendenti**.
    9.    Scorrere fino in fondo alla pagina e fare clic su **Cancella tutto**.
    10.    Nella sezione **Proprietà** selezionare **Leggi msDS-KeyCredentialLink**.
    11.    Fare clic tre volte su **OK** per completare l'attività.


 Per altre informazioni, vedere i [profili certificato](introduction-to-certificate-profiles.md).  






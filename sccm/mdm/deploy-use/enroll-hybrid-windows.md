---
title: Configurare la gestione di dispositivi Windows ibrida con Microsoft Intune
titleSuffix: Configuration Manager
description: Impostare la gestione dei dispositivi Windows con System Center Configuration Manager e Microsoft Intune.
ms.custom: na
ms.date: 03/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: "9"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 95808d4fd743d5cc18cacb69bb38bc729acdda25
ms.sourcegitcommit: 92c3f916e6bbd35b6208463ff406e0247664543a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/02/2018
---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurare la gestione di dispositivi ibridi Windows con System Center Configuration Manager e Microsoft Intune

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo argomento descrive in che modo gli amministratori IT possono consentire agli utenti di iniziare a gestire i PC Windows e dispositivi mobili usando Configuration Manager e Microsoft Intune.

## <a name="enable-windows-device-management"></a>Abilitare la gestione dei dispositivi Windows
Per abilitare la gestione dei dispositivi Windows per PC o dispositivi mobili, usare la procedura seguente:

1.  Prima di impostare la registrazione per una qualsiasi piattaforma, completare i prerequisiti e le procedure indicate in [Setup hybrid MDM](setup-hybrid-mdm.md) (Impostare una MDM ibrida).  
2.  Nell'area di lavoro **Amministrazione** della console di Configuration Manager andare a **Panoramica** > **Servizi cloud** > **Sottoscrizioni a Microsoft Intune**.  
3.  Nella barra multifunzione fare clic su **Configura piattaforme** e quindi selezionare la piattaforma Windows:
    - **Windows** per PC desktop e portatili Windows, quindi completare i passaggi seguenti:
      1. Nella scheda **Generale** fare clic sulla casella di controllo **Abilita registrazione Windows**.
      2. Se si usa un certificato per firmare il codice e distribuire l'app del portale aziendale, individuare il **certificato di firma del codice**. Gli utenti dei dispositivi possono anche installare l'app del portale aziendale da Microsoft Store o è possibile distribuire l'app da Microsoft Store per le aziende senza firma del codice.
      3. Inoltre è possibile configurare le [impostazioni di Windows Hello for Business](windows-hello-for-business-settings.md).
    - **Windows Phone** per telefoni e tablet Windows, quindi completare la procedura seguente:
      1. Nella scheda **Generale** fare clic sulla casella di controllo **Windows Phone 8.1 e Windows 10 Mobile**. Windows Phone 8.0 non è più supportato.
      2. Se l'organizzazione ha bisogno di trasferire localmente app aziendali, è possibile caricare il file o il token necessario. Per altre informazioni sul trasferimento locale di app, vedere [Creare applicazioni Windows](https://docs.microsoft.com/sccm/apps/get-started/creating-windows-applications).
        - **Token di registrazione applicazione**
        - **File con estensione .pfx**
        - **Nessuno** Se si usa un certificato Symantec, è possibile specificare **Show an alert before Symantec certificates expire** (Mostra un avviso prima della scadenza dei certificati Symantec).
4. Fare clic su **OK** per chiudere la finestra di dialogo.  Per semplificare il processo di registrazione tramite il portale aziendale, è necessario creare un alias DNS per la registrazione del dispositivo. È quindi possibile indicare agli utenti come registrare i propri dispositivi.

## <a name="choose-how-to-enroll-windows-devices"></a>Scegliere come registrare i dispositivi Windows

Dopo aver assegnato licenze Intune agli utenti, è possibile registrare i dispositivi Windows senza ulteriori passaggi, ma è anche possibile semplificare la registrazione per gli utenti.

Due fattori determinano in che modo è possibile semplificare la registrazione dei dispositivi Windows:
- **Si usa Azure Active Directory Premium?** <br>[Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) è incluso in Enterprise Mobility + Security e altri piani di licenze.
- **Quali versioni di client Windows saranno registrate?** <br>I dispositivi Windows 10 possono essere registrati automaticamente mediante l'aggiunta di un account aziendale o dell'istituto di istruzione. Le versioni precedenti devono essere registrate con l'app del portale aziendale.

||**Azure AD Premium**|**Altro AD**|
|----------|---------------|---------------|  
|**Windows 10**|[Registrazione automatica](#enable-windows-10-automatic-enrollment) |[Registrazione utente](#enable-windows-enrollment-without-azure-ad-premium)|
|**Versioni precedenti di Windows**|[Registrazione utente](#enable-windows-enrollment-without-azure-ad-premium)|[Registrazione utente](#enable-windows-enrollment-without-azure-ad-premium)|

## <a name="enable-windows-10-automatic-enrollment"></a>Abilitare la registrazione automatica di Windows 10

Con la registrazione automatica è possibile registrare PC Windows 10 e dispositivi mobili Windows 10 aziendali o personali in Intune aggiungendo un account aziendale o dell'istituto di istruzione e accettandone la gestione. Non occorrono altre operazioni. Il dispositivo dell'utente registra e aggiunge Azure Active Directory in background. Dopo essere stato registrato, il dispositivo viene gestito con Intune.

**Prerequisiti**
- Sottoscrizione di Azure Active Directory Premium ([sottoscrizione di prova](http://go.microsoft.com/fwlink/?LinkID=816845))
- Sottoscrizione di Microsoft Intune


### <a name="configure-automatic-mdm-enrollment"></a>Configurare la registrazione automatica MDM

1. Accedere al [portale di gestione di Azure](https://portal.azure.com) (https://manage.windowsazure.com) e selezionare **Azure Active Directory**.

  ![Schermata del portale di Azure](../media/auto-enroll-azure-main.png)

2. Selezionare **Servizi Mobility (MDM e MAM)**.

  ![Schermata del portale di Azure](../media/auto-enroll-mdm.png)

3. Selezionare **Microsoft Intune**.

  ![Schermata del portale di Azure](../media/auto-enroll-intune.png)

4. Configurare **Ambito utente MDM**. Specificare i dispositivi utente da gestire con Microsoft Intune. I dispositivi utente Windows 10 vengono registrati automaticamente per essere gestiti con Microsoft Intune.

    - **Nessuno**
    - **Alcuni**
    - **Tutti**

   ![Schermata del portale di Azure](../media/auto-enroll-scope.png)

5. Usare i valori predefiniti per gli URL seguenti:
    - **URL delle condizioni per l'uso di MDM**
    - **URL individuazione MDM**
    - **URL conformità MDM**

6. Selezionare **Salva**.


L'autenticazione a due fattori non è abilitata per il servizio per impostazione predefinita. Tuttavia l'autenticazione a due fattori è consigliabile quando si registra un dispositivo. Prima di richiedere l'autenticazione a due fattori per questo servizio, è necessario configurare un provider di autenticazione a due fattori in Azure Active Directory e configurare gli account utente per l'autenticazione a più fattori. Vedere [Introduzione al server Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).

## <a name="enable-windows-enrollment-without-azure-ad-premium"></a>Abilitare la registrazione di Windows senza Azure AD Premium
È possibile consentire agli utenti di registrare i propri dispositivi senza la registrazione automatica di Azure AD Premium. Una volta assegnate le licenze, gli utenti possono registrarsi dopo aver aggiunto l'account aziendale per i dispositivi personali o i dispositivi di proprietà dell'azienda ad Azure AD. La creazione di un alias DNS (tipo di record CNAME) semplifica la registrazione dei dispositivi per gli utenti. Se si creano record di risorse CNAME DNS, gli utenti si connettono e si registrano a Intune senza dover immettere il nome del server di Intune.

### <a name="create-cnames-to-simplify-enrollment"></a>Creare record CNAME per semplificare la registrazione
Creare record di risorse CNAME DNS per il dominio della società. Ad esempio, se il sito Web della società è contoso.com, si creerà un record CNAME in DNS che reindirizzi EnterpriseEnrollment.contoso.com a enterpriseenrollment-s.manage.microsoft.com.

Sebbene la creazione di voci DNS CNAME sia facoltativa, i record CNAME semplificano la registrazione per gli utenti. Se non viene trovato alcun record di registrazione CNAME, agli utenti viene richiesto di immettere manualmente il nome del server MDM, enrollment.manage.microsoft.com.

|Type|Nome dell'host|Punta a|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 ora|

Se si dispone di più suffissi UPN, è necessario creare un CNAME per ciascun nome di dominio e puntare ciascuno a EnterpriseEnrollment-s.manage.microsoft.com. Ad esempio, se gli utenti di Contoso usano name@contoso.com, ma usano anche name@us.contoso.com e name@eu.constoso.com come indirizzo di posta elettronica/UPN, l'amministratore DNS Contoso dovrà creare i CNAME seguenti.

|Type|Nome dell'host|Punta a|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 ora|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 ora|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 ora|

`EnterpriseEnrollment-s.manage.microsoft.com`: supporta un reindirizzamento al servizio Intune con riconoscimento del dominio dal nome di dominio del messaggio di posta elettronica

La propagazione delle modifiche ai record DNS potrebbe richiedere fino a 72 ore. Non è possibile verificare la modifica DNS in Intune fino a quando il record DNS non si propaga.

## <a name="tell-users-how-to-enroll-devices"></a>Indicare agli utenti come registrare i dispositivi  

 Dopo aver completato la configurazione occorre informare gli utenti su come registrare i loro dispositivi. Per informazioni, vedere [Informazioni sull'uso di Microsoft Intune per gli utenti finali](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). È possibile indirizzare gli utenti a [Uso del dispositivo Windows con Intune](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows). Queste informazioni si applicano ai dispositivi mobili gestiti sia con Microsoft Intune che con Configuration Manager.

> [!div class="button"]
[< Passaggio precedente](create-service-connection-point.md)  [Passaggio successivo >](set-up-additional-management.md)

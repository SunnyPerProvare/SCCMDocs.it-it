---
title: Configurare la gestione di dispositivi Windows ibrida con System Center Configuration Manager e Microsoft Intune | Microsoft Docs
description: Impostare la gestione dei dispositivi Windows con System Center Configuration Manager e Microsoft Intune.
ms.custom: na
ms.date: 03/17/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: 9
author: nathbarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6424fb07802b62820b4dc78a58ab30d3b956abef
ms.openlocfilehash: 4189fe34efc2ae134150a89791dc10bbab1b9d02
ms.lasthandoff: 03/17/2017


---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurare la gestione di dispositivi ibridi Windows con System Center Configuration Manager e Microsoft Intune

*Si applica a: System Center Configuration Manager (Current Branch)*

Questo argomento descrive in che modo gli amministratori IT possono consentire agli utenti di iniziare a gestire i PC Windows e dispositivi mobili usando Configuration Manager e Microsoft Intune. Sono disponibili due metodi di registrazione:
-  Registrazione automatica di Azure Active Directory (AD) quando gli utenti connettono il proprio account a un dispositivo
- Registrazione mediante l'installazione e l'accesso con l'app del portale aziendale

## <a name="choose-how-to-enroll-windows-devices"></a>Scegliere come registrare i dispositivi Windows

Due fattori determinano in che modo è possibile registrare i dispositivi Windows:
- **Si usa Azure Active Directory Premium?** <br>[Azure AD Premium](https://docs.microsoft.com/azure/active-directory/active-directory-get-started-premium) è incluso in Enterprise Mobility + Security e altri piani di licenze.
- **Quali versioni di client Windows saranno registrate?** <br>I dispositivi Windows 10 possono essere registrati automaticamente mediante l'aggiunta di un account aziendale o dell'istituto di istruzione. Le versioni precedenti devono essere registrate con l'app del portale aziendale.

||**Azure AD Premium**|**Altro AD**|
|----------|---------------|---------------|  
|**Windows 10**|[Registrazione automatica](#automatic-enrollment) |[Registrazione con il portale aziendale](#company-portal-enrollment)|
|**Versioni precedenti di Windows**|[Registrazione con il portale aziendale](#company-portal-enrollment)|[Registrazione con il portale aziendale](#company-portal-enrollment)|

## <a name="automatic-enrollment"></a>Registrazione automatica

La registrazione automatica consente agli utenti di registrare i dispositivi Windows 10 dell'azienda o personali aggiungendo un account aziendale o dell'istituto di istruzione e accettandone la gestione. Il dispositivo dell'utente viene registrato e si connette con Azure Active Directory in background. Dopo essere stato registrato, è possibile gestire il dispositivo con Intune. I dispositivi gestiti possono comunque usare il portale aziendale per le attività, ma non è necessario che lo installino per registrarsi.

**Prerequisiti**
- Sottoscrizione di Azure Active Directory Premium ([sottoscrizione di prova](http://go.microsoft.com/fwlink/?LinkID=816845))
- Sottoscrizione di Microsoft Intune

### <a name="configure-automatic-enrollment"></a>Configurare la registrazione automatica

1. Accedere al [portale Azure](https://manage.windowsazure.com), passare al nodo **Active Directory** nel riquadro a sinistra e selezionare la directory.
2. Selezionare la scheda **Configura** e scorrere fino alla sezione denominata **Dispositivi**.
3. Selezionare **Tutti** per **Users may workplace join devices** (Gli utenti possono aggiungere dispositivi all'area di lavoro).
4. Selezionare il numero massimo di dispositivi che si desidera autorizzare per utente.

L'autenticazione a due fattori non è abilitata per il servizio per impostazione predefinita. Tuttavia l'autenticazione a due fattori è consigliabile quando si registra un dispositivo. Prima di richiedere l'autenticazione a due fattori per questo servizio, è necessario configurare un provider di autenticazione a due fattori in Azure Active Directory e configurare gli account utente per l'autenticazione a più fattori. Vedere [Introduzione al server Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-cloud).

## <a name="company-portal-enrollment"></a>Registrazione con il portale aziendale
Gli utenti finali o un [manager di registrazione dispositivi](enroll-devices-with-device-enrollment-manager.md) può registrare i dispositivi Windows installando l'app del portale aziendale e quindi eseguendo l'accsso con le proprie credenziali di lavoro. Per semplificare la registrazione per gli utenti finali è necessario aggiungere un CNAME alla registrazione DNS.

### <a name="enable-windows-device-management"></a>Abilitare la gestione dei dispositivi Windows
Per abilitare la gestione dei dispositivi Windows per PC o dispositivi mobili, usare la procedura seguente:

1.  Prima di impostare la registrazione per una qualsiasi piattaforma, completare i prerequisiti e le procedure indicate in [Setup hybrid MDM](setup-hybrid-mdm.md) (Impostare una MDM ibrida).  
2.  Nell'area di lavoro **Amministrazione** della console di Configuration Manager andare a **Panoramica** > **Servizi cloud** > **Sottoscrizioni a Microsoft Intune**.  
3.  Nella barra multifunzione fare clic su **Configura piattaforme** e quindi selezionare la piattaforma Windows:
    - **Windows** per PC desktop e portatili Windows, quindi completare i passaggi seguenti:
      1. Nella scheda **Generale** fare clic sulla casella di controllo **Abilita registrazione Windows**.
      2. Se si usa un certificato per firmare il codice e distribuire l'app del portale aziendale, individuare il **certificato di firma del codice**. Gli utenti dei dispositivi possono anche installare l'app del portale aziendale da Windows Store o è possibile distribuire l'app da Windows Store per Business senza firma del codice.
      3. Inoltre è possibile configurare le [impostazioni di Windows Hello for Business](windows-hello-for-business-settings.md).
    - **Windows Phone** per telefoni e tablet Windows, quindi completare la procedura seguente:
      1. Nella scheda **Generale** fare clic sulla casella di controllo **Windows Phone 8.1 e Windows 10 Mobile**. Windows Phone 8.0 non è più supportato.
      2. Se l'organizzazione ha bisogno di trasferire localmente app aziendali, è possibile caricare il file o il token necessario. Per altre informazioni sul trasferimento locale di app, vedere [Creare applicazioni Windows](https://docs.microsoft.com/sccm/apps/get-started/creating-windows-applications).
        - **Token di registrazione applicazione**
        - **File con estensione .pfx**
        - **Nessuno** Se si usa un certificato Symantec, è possibile specificare **Show an alert before Symantec certificates expire** (Mostra un avviso prima della scadenza dei certificati Symantec).
4. Fare clic su **OK** per chiudere la finestra di dialogo.  Per semplificare il processo di registrazione tramite il portale aziendale, è necessario creare un alias DNS per la registrazione del dispositivo. È quindi possibile indicare agli utenti come registrare i propri dispositivi.

### <a name="create-dns-alias-for-device-enrollment"></a>Creare l'alias DNS per la registrazione del dispositivo  
Un alias DNS (tipo di record CNAME) semplifica agli utenti la registrazione dei propri dispositivi tramite la connessione al servizio, senza richiedere all'utente di immettere un indirizzo del server. Per creare un alias DNS (tipo di record CNAME), è necessario configurare un record CNAME nei record DNS della società che reindirizzi le richieste inviate a un URL nel dominio della società ai server del servizio cloud di Microsoft.  Ad esempio, se il dominio della società è contoso.com, si creerà un record CNAME in DNS che reindirizzi EnterpriseEnrollment.contoso.com a EnterpriseEnrollment-s.manage.microsoft.com.  

 Sebbene la creazione di voci DNS CNAME sia facoltativa, i record CNAME semplificano la registrazione per gli utenti. Se non viene trovato alcun record di registrazione CNAME, agli utenti viene richiesto di immettere manualmente il nome del server MDM, enrollment.manage.microsoft.com.

|Tipo|Nome dell'host|Punta a|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 ora|

Se si dispone di più suffissi UPN, è necessario creare un CNAME per ciascun nome di dominio e puntare ciascuno a EnterpriseEnrollment-s.manage.microsoft.com. Ad esempio, se gli utenti di Contoso usano name@contoso.com, ma usano anche name@us.contoso.com e name@eu.constoso.com come indirizzo di posta elettronica/UPN, l'amministratore DNS Contoso dovrà creare i CNAME seguenti.

|Tipo|Nome dell'host|Punta a|TTL|  
|----------|---------------|---------------|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 ora|
|CNAME|EnterpriseEnrollment.us.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 ora|
|CNAME|EnterpriseEnrollment.eu.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com| 1 ora|

## <a name="tell-users-how-to-enroll-devices"></a>Indicare agli utenti come registrare i dispositivi  

 Dopo aver completato la configurazione occorre informare gli utenti su come registrare i loro dispositivi. Per informazioni, vedere [Informazioni sull'uso di Microsoft Intune per gli utenti finali](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). È possibile indirizzare gli utenti a [Uso del dispositivo Windows con Intune](https://docs.microsoft.com/intune/enduser/enroll-your-device-in-intune-windows). Queste informazioni si applicano ai dispositivi mobili gestiti sia con Microsoft Intune che con Configuration Manager.

> [!div class="button"]
[< Passaggio precedente](create-service-connection-point.md)  [Passaggio successivo >](set-up-additional-management.md)


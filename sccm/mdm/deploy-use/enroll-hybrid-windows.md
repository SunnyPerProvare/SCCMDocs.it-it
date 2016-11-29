---
title: Configurare la gestione di dispositivi ibridi Windows con System Center Configuration Manager e Microsoft Intune
description: Impostare la gestione dei dispositivi Windows con System Center Configuration Manager e Microsoft Intune.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: dc1f70f5-64ab-42ab-aa91-d3858803e12f
caps.latest.revision: 9
author: NathBarn
ms.author: nathbarn
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 55fca210e5b3ce11e513662994105027f1a4f227


---
# <a name="set-up-windows-hybrid-device-management-with-system-center-configuration-manager-and-microsoft-intune"></a>Configurare la gestione di dispositivi ibridi Windows con System Center Configuration Manager e Microsoft Intune

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile usare Configuration Manager con Intune per gestire desktop, portatili e altri dispositivi che eseguono Windows come dispositivi mobili. È possibile impostare Azure Active Directory per consentire la registrazione automatica dei PC Windows. È anche possibile configurare Configuration Manager per semplificare la registrazione usando l'app Portale aziendale.


Le opzioni di registrazione di Windows includono:

- [Registrazione automatica con Azure AD](#azure-active-directory-enrollment)
- [PC Windows](#set-up-windows-device-enrollment)
- [Dispositivi Windows 10 Mobile e Windows Phone](#enable-windows-phone-devices)

## <a name="azure-active-directory-enrollment"></a>Registrazione di Azure Active Directory

Con la registrazione automatica è possibile registrare PC Windows 10 e Windows 10 Mobile aziendali o personali in Intune aggiungendo un account aziendale o dell'istituto di istruzione e accettandone la gestione. Il dispositivo dell'utente registra e aggiunge Azure Active Directory in background. Dopo essere stato registrato, è possibile gestire il dispositivo con Intune.

**Prerequisiti**
- Sottoscrizione di Azure Active Directory Premium ([sottoscrizione di prova](http://go.microsoft.com/fwlink/?LinkID=816845))
- Sottoscrizione di Microsoft Intune


### <a name="configure-automatic-mdm-enrollment"></a>Configurare la registrazione automatica MDM

1. Nel [portale di gestione di Azure](https://manage.windowsazure.com) (https://manage.windowsazure.com) esplorare il nodo **Active Directory** e selezionare la directory.

2. Fare clic sulla scheda **Applicazioni**. **Microsoft Intune** verrà visualizzato nell'elenco delle applicazioni.

    ![App Azure AD con Microsoft Intune](../media/aad-intune-app.png)

3. Fare clic sulla freccia corrispondente a **Microsoft Intune**. Verrà visualizzata una pagina che consente di configurare Microsoft Intune.

4. Fare clic su **Configura** per avviare la configurazione della registrazione automatica MDM con Microsoft Intune.

5. Specificare gli URL per Intune:

  - **URL di registrazione MDM**: usare `https://enterpriseenrollment-s.manage.microsoft.com/EnrollmentServer/Discovery.svc` come URL di registrazione MDM.
  - **URL delle condizioni per l'utilizzo di MDM**: usare il valore predefinito. Questo URL visualizza le condizioni per l'utilizzo per gli utenti durante la registrazione dei dispositivi.
  - **URL conformità MDM**: usare il valore predefinito. Se viene rilevato un dispositivo non conforme, insieme a questo URL viene visualizzato il messaggio **Accesso negato**. L'URL indirizza a una pagina che contiene informazioni sul motivo per cui il dispositivo non è conforme a criteri e su come riportarlo in conformità.

6.  Specificare i dispositivi utente da gestire con Microsoft Intune. I dispositivi utente Windows 10 vengono registrati automaticamente per essere gestiti con Microsoft Intune.

  - **Tutti**
  - **Gruppi**
  - **Nessuno**

7. Scegliere **Salva**.

## <a name="configure-windows-pc-enrollment"></a>Configurare la registrazione di PC Windows
 Per abilitare la gestione dei dispositivi mobili Windows, è necessario abilitare la gestione per il sistema operativo.  È anche possibile aggiungere un DNS CNAME per semplificare la registrazione.

### <a name="create-dns-alias-for-device-enrollment"></a>Creare l'alias DNS per la registrazione del dispositivo  
 Un Alias DNS (tipo di record CNAME) semplifica la registrazione dei dispositivi perché durante la registrazione del dispositivo il nome del server viene inserito automaticamente. Per creare un alias DNS (tipo di record CNAME), è necessario configurare un record CNAME nei record DNS della società che reindirizzi le richieste inviate a un URL nel dominio della società ai server del servizio cloud di Microsoft.  Ad esempio, se il sito Web della società è contoso.com, si creerà un record CNAME in DNS che reindirizzi EnterpriseEnrollment.contoso.com a EnterpriseEnrollment-s.manage.microsoft.com.  

|Tipo|Nome dell'host|Punta a|  
|----------|---------------|---------------|  
|CNAME|EnterpriseEnrollment.company_domain.com|EnterpriseEnrollment-s.manage.microsoft.com|  
|CNAME|EnterpriseRegistration.company_domain.com|EnterpriseRegistration.windows.net|  
### <a name="to-enable-enrollment-for-windows-devices"></a>Per abilitare la registrazione per i dispositivi Windows  

1.  **Prerequisiti**: prima di impostare la registrazione per una qualsiasi piattaforma, completare i prerequisiti e le procedure in [Setup hybrid MDM](setup-hybrid-mdm.md) (Impostare una MDM ibrida).  

2.  Nell'area di lavoro **Amministrazione** andare a **Servizi cloud** > **Sottoscrizioni a Microsoft Intune**.  

    > [!WARNING]  
    >  Se sono aperte altre finestre di dialogo di Configuration Manager, chiuderle prima di continuare la procedura.  

3.  Nella scheda **Home** fare clic su **Configura piattaforme**e quindi su **Windows**.  

4.  Nella scheda **Generale** selezionare **Abilita registrazione Windows**.  

 Dopo aver completato la configurazione occorre informare gli utenti su come registrare i loro dispositivi. Vedere [Informazioni sull'uso di Microsoft Intune per gli utenti finali](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Queste informazioni si applicano ai dispositivi mobili gestiti sia con Microsoft Intune che con Configuration Manager.

## <a name="enable-windows-phone-devices"></a>Abilitare dispositivi Windows Phone  
  Se gli utenti registreranno solo dispositivi con Windows Phone 8.1 e versioni successive e non è prevista la distribuzione di app line-of-business nei dispositivi Windows Phone, non è necessario alcun certificato Symantec. Dopo avere abilitato la registrazione di Windows Phone, è necessario indicare agli utenti di installare l'app Portale aziendale da Windows Phone Store per registrare i propri dispositivi.  

  Seguire questa procedura per i dispositivi Windows Phone da gestire.  

### <a name="to-enable-enrollment-for-windows-phone-81-and-later-devices"></a>Per abilitare la registrazione per i dispositivi con Windows Phone 8.1 e versioni successive  

 1.  **Prerequisiti**: prima di impostare la registrazione per una qualsiasi piattaforma, completare i prerequisiti e le procedure in [Setup hybrid MDM](setup-hybrid-mdm.md) (Impostare una MDM ibrida).  

 2.  Nell'area di lavoro **Amministrazione** andare a **Servizi cloud** > **Sottoscrizioni a Microsoft Intune**.  

     > [!WARNING]  
     >  Se sono aperte altre finestre di dialogo di Configuration Manager, chiuderle prima di continuare la procedura.  

 3.  Nella scheda **Home** fare clic su **Configura piattaforme**e quindi su **Windows Phone**.  

 4.  Nella scheda **Generale** scegliere  **Windows Phone 8.1 e Windows 10 Mobile**. È possibile caricare i dati AET del file XML o un file PFX per supportare la distribuzione del portale aziendale o indicare agli utenti di scaricare il portale aziendale da Windows Phone Store.  

      Fare clic su **OK**.  

  Dopo aver completato la configurazione occorre informare gli utenti su come registrare i loro dispositivi. Vedere [Informazioni sull'uso di Microsoft Intune per gli utenti finali](https://docs.microsoft.com/intune/deploy-use/what-to-tell-your-end-users-about-using-microsoft-intune). Queste informazioni si applicano ai dispositivi mobili gestiti sia con Microsoft Intune che con Configuration Manager.  



<!--HONumber=Nov16_HO1-->



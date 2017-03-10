---
title: Accesso condizionale | Microsoft Docs
description: Informazioni su come usare l&quot;accesso condizionale in System Center Configuration Manager per proteggere la posta elettronica e altri servizi.
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b04727b-d563-422f-8d59-4dd66215d0b3
caps.latest.revision: 26
author: andredm7
ms.author: andredm
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: ea9184cd4fdc87513ed489f0f568efa6d64c1caa
ms.lasthandoff: 03/06/2017


---

# <a name="manage-access-to-services-in-system-center-configuration-manager"></a>Gestire l'accesso ai servizi in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


## <a name="conditional-access-in-system-center-configuration-manager"></a>Accesso condizionale in System Center Configuration Manager
Usare l' **accesso condizionale** per proteggere la posta elettronica e altri servizi nei dispositivi registrati in Microsoft Intune, in base alle condizioni specificate.  

 Per informazioni sull'**accesso condizionale nei computer gestiti con System Center Configuration Manager** e valutati per la conformità, vedere [Gestire l'accesso ai servizi di O365 per i PC gestiti da System Center Configuration Manager](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  


 Lo schema seguente illustra come funziona l'accesso condizionale:  

 ![ConditionalAccess4](media/ConditionalAccess4.png)  

 Usare l'accesso condizionale per gestire l'accesso ai seguenti servizi:  

-   Microsoft Exchange locale  

-   Microsoft Exchange Online  

-   Exchange Online dedicato  

-   SharePoint Online  

-   Skype for Business Online

-   Dynamics CRM Online

 Per implementare l'accesso condizionale vengono configurati due tipi di criteri in Configuration Manager:  

-   **I criteri di conformità** sono criteri facoltativi che è possibile distribuire alle raccolte dell'utente per valutare impostazioni come:  

    -   Passcode  

    -   Crittografia  

    -   Se il dispositivo è jailbroken o rooted  

    -   Se la posta elettronica sul dispositivo è gestita da criteri di Configuration Manager o Intune  

     **Se non vengono distribuiti i criteri di conformità in un dispositivo, qualsiasi criterio di accesso condizionale considera il dispositivo conforme**.  

-   I **criteri di accesso condizionale** sono configurati per un particolare servizio e definiscono delle regole, ad esempio quali gruppi utenti di sicurezza di Azure Active Directory o raccolte utenti di Configuration Manager verranno usati come destinazione o per i quali viene applicata un'esenzione.  

     Configurare un criterio di accesso condizionale per Exchange locale dalla console di Configuration Manager. Tuttavia, quando si configura un criterio di Exchange Online o SharePoint Online, verrà visualizzata la console di amministrazione di Intune nella quale è possibile configurare il criterio.  

     A differenza degli altri criteri di Intune o Configuration Manager, i criteri di accesso condizionale non vengono distribuiti, ma configurati una sola volta prima di essere applicati a tutti gli utenti di destinazione.  

 Se i dispositivi non soddisfano le condizioni, l'utente viene guidato nel processo di registrazione del dispositivo e di risoluzione del problema che impedisce la conformità del dispositivo.  

**Prima** di iniziare a usare l'accesso condizionale, verificare che i **requisiti** richiesti siano soddisfatti:  

## <a name="requirements-for-exchange-online-using-the-shared-multi-tenant-environment"></a>Requisiti per Exchange Online (con un ambiente condiviso multi-tenant)
L'accesso condizionale a Exchange Online supporta i dispositivi che eseguono:
-   Windows 8.1 e versioni successive (se registrati in Intune)
-   Windows 7.0 o Windows 8.1 (se aggiunto a un dominio)
-   Windows Phone 8.1 e versioni successive
-   iOS 7.1 e versioni successive
-   Android 4.0 e versioni successive, Samsung KNOX Standard 4.0 e versioni successive

 **Inoltre**:
-   I dispositivi devono essere aggiunti all'area di lavoro, che registra il dispositivo con Azure Active Directory Device Registration Service (AAD DRS).<br />     
- I PC aggiunti a un dominio devono essere registrati automaticamente in Azure Active Directory tramite i criteri di gruppo o MSI.

  La sezione **Accesso condizionale per i PC** in questo argomento descrive tutti i requisiti necessari per abilitare l'accesso condizionale per un PC.<br />     
  Il servizio AAD DRS verrà attivato automaticamente per i clienti di Intune e Office 365. I clienti che hanno già distribuito il servizio di registrazione dei dispositivi di ADFS non visualizzeranno i dispositivi registrati in Active Directory locale.
-   È necessario usare una sottoscrizione a Office 365 che include Exchange Online (ad esempio E3) e gli utenti devono avere una licenza per Exchange Online.
-   Il **connettore Exchange Server** è facoltativo e consente di connettere Configuration Manager a Microsoft Exchange Online e di monitorare le informazioni dei dispositivi tramite la console di Configuration Manager (vedere [Gestire i dispositivi mobili con System Center Configuration Manager ed Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)).
Non è necessario usare il connettore per i criteri di conformità o i criteri di accesso condizionale, ma è obbligatorio eseguire i report per valutare l'impatto dell'accesso condizionale.

## <a name="requirements-for-exchange-online-dedicated"></a>Requisiti per Exchange Online dedicato
L'accesso condizionale di Exchange Online dedicato supporta i dispositivi che eseguono:
-   Windows 8 e versioni successive (se registrati in Intune)
-   Windows 7.0 o Windows 8.1 (se aggiunto a un dominio)

  Accesso condizionale ai PC aggiunti al dominio soltanto per i tenant del nuovo ambiente Exchange Online dedicato.
-   Windows Phone 8 e versioni successive
-   Dispositivi iOS che usano i client di posta elettronica di Exchange ActiveSync (EAS)
-   Android 4 e versioni successive.
-   Per i tenant nell'**ambiente legacy Exchange Online dedicato**:    

  È necessario usare il **connettore Exchange Server** che connette Configuration Manager a Microsoft Exchange locale. Ciò consente di gestire i dispositivi mobili e di abilitare l'accesso condizionale (vedere [Gestire i dispositivi mobili con System Center Configuration Manager ed Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)).
-   Per i tenant nel **nuovo ambiente Exchange Online dedicato**:     
  Il **connettore Exchange Server** facoltativo consente di connettere Configuration Manager a Microsoft Exchange Online e facilita la gestione delle informazioni dei dispositivi (vedere [Gestire i dispositivi mobili con System Center Configuration Manager ed Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)). Non è necessario usare il connettore per i criteri di conformità o i criteri di accesso condizionale, ma è obbligatorio eseguire i report per valutare l'impatto dell'accesso condizionale.  

## <a name="requirements-for-exchange-on-premises"></a>Requisiti per Exchange locale
L'accesso condizionale a Exchange locale supporta:
-   Windows 8 e versioni successive (se registrati in Intune)
-   Windows Phone 8 e versioni successive
-   App di posta elettronica nativa in iOS
-   App di posta elettronica nativa in Android versione 4 o successiva
-   L'app Microsoft Outlook non è supportata (Android e iOS).

**Inoltre**:

-  La versione di Exchange deve essere Exchange 2010 o successiva. È supportato un array del server Accesso client di Exchange Server.

> [!TIP]
> Se l'ambiente di Exchange si trova in una configurazione con server CAS, sarà necessario configurare On-Premises Exchange Connector in modo che punti a uno dei server CAS.
- È necessario usare il **connettore Exchange Server** che connette Configuration Manager a Microsoft Exchange locale. Ciò consente di gestire i dispositivi mobili e di abilitare l'accesso condizionale (vedere [Gestire i dispositivi mobili con System Center Configuration Manager ed Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)).
  - Assicurarsi di usare la versione più recente di **Exchange Connector locale**. On-Premises Exchange Connector deve essere configurato tramite la console di Configuration Manager. Per una procedura dettagliata, vedere [Gestire i dispositivi mobili con System Center Configuration Manager ed Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
  - Il connettore deve essere configurato solo nel sito primario di System Center Configuration Manager.</li><li>Questo connettore supporta l'ambiente CAS di Exchange. <br />        Quando si configura il connettore, è necessario impostarlo in modo che comunichi con uno dei server CAS di Exchange.

- È possibile configurare Exchange ActiveSync con l'autenticazione basata su certificati o tramite l'immissione di credenziali utente.


## <a name="requirements-for-skype-for-business-online"></a>Requisiti per Skype for Business Online
L'accesso condizionale a SharePoint Online supporta i dispositivi che eseguono:
 -   iOS 7.1 e versioni successive
 -   Android 4.0 e versioni successive
 -   Samsung KNOX Standard 4.0 o versioni successive

**Inoltre,** è necessario abilitare l'autenticazione moderna per Skype for Business Online. Compilare il [modulo di connessione](https://connect.microsoft.com/office/Survey/NominationSurvey.aspx?SurveyID=17299&ProgramID=8715) per effettuare la registrazione nel programma di autenticazione moderna.

Tutti gli utenti finali devono usare Skype for Business Online. Se si ha una distribuzione con Skype for Business Online e Skype for Business locale, i criteri di accesso condizionale non verranno applicati agli utenti finali inclusi nella distribuzione locale.

## <a name="requirements-for-sharepoint-online"></a>Requisiti per SharePoint Online
L'accesso condizionale a SharePoint Online supporta i dispositivi che eseguono:
 -   Windows 8.1 e versioni successive (se registrati in Intune)
 -   Windows 7.0 o Windows 8.1 (se aggiunto a un dominio)
 -   Windows Phone 8.1 e versioni successive
 -   iOS 7.1 e versioni successive
 -   Android 4.0 e versioni successive, Samsung KNOX Standard 4.0 e versioni successive

 **Inoltre**:
 -   I dispositivi devono essere aggiunti all'area di lavoro, che registra il dispositivo con Azure Active Directory Device Registration Service (AAD DRS).

 I PC aggiunti a un dominio devono essere registrati automaticamente in Azure Active Directory tramite i criteri di gruppo o MSI. La sezione **Accesso condizionale per i PC** in questo argomento descrive tutti i requisiti necessari per abilitare l'accesso condizionale per un PC.

 Il servizio AAD DRS verrà attivato automaticamente per i clienti di Intune e Office 365. I clienti che hanno già distribuito il servizio di registrazione dei dispositivi di ADFS non visualizzeranno i dispositivi registrati in Active Directory locale.
 -   Una sottoscrizione a SharePoint Online è obbligatoria e gli utenti devono avere una licenza per SharePoint Online.

 ### <a name="conditional-access-for-pcs"></a>Accesso condizionale per i PC

 È possibile configurare l'accesso condizionale per i PC che eseguono le applicazioni desktop di Office al fine di accedere a **Exchange Online** e **SharePoint Online** , se i PC soddisfano i requisiti seguenti:
 -   Il PC deve eseguire Windows 7.0 o Windows 8.1.
 -   Il PC deve essere aggiunto a un dominio oppure conforme.

 Affinché sia ritenuto conforme, il PC deve essere registrato in Intune e rispettare i criteri.

 Per i PC aggiunti a un dominio, è necessario impostare il dispositivo in modo che [venga registrato automaticamente](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) con Azure Active Directory.
 -   [L'autenticazione moderna di Office 365 deve essere attivata](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)ed è necessario disporre di tutti gli aggiornamenti di Office più recenti.<br />     L'autenticazione moderna garantisce accesso basato su Active Directory Authentication Library (ADAL) ai client di Office 2013 Windows e offre migliore opzioni di sicurezza, ad esempio, l' **autenticazione a più fattori**e l' **autenticazione basata sui certificati**.
 -   Configurare le regole delle attestazioni ADFS per bloccare i protocolli di autenticazione non moderni.  

## <a name="next-steps"></a>Passaggi successivi  
 Leggere i seguenti argomenti per informazioni su come configurare i criteri di conformità e i criterio di accesso condizionale per lo scenario richiesto:  

-   [Gestire i criteri di conformità del dispositivo in System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md)  

-   [Gestire l'accesso alla posta elettronica in System Center Configuration Manager](../../protect/deploy-use/manage-email-access.md)  

-   [Gestire l'accesso a SharePoint Online in System Center Configuration Manager](../../protect/deploy-use/manage-sharepoint-online-access.md)  

-   [Gestire l'accesso a Skype for Business Online](../../protect/deploy-use/manage-skype-for-business-online-access.md)  

### <a name="see-also"></a>Vedere anche  

 [Introduzione alle impostazioni di conformità in System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md)


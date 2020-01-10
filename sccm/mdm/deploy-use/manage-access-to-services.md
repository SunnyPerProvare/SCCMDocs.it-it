---
title: Accesso condizionale
titleSuffix: Configuration Manager
description: Informazioni su come usare l'accesso condizionale in Configuration Manager per proteggere la posta elettronica e altri servizi.
ms.date: 03/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b04727b-d563-422f-8d59-4dd66215d0b3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 99dc6fa274f875bc7b1f41b435ececc3467821cd
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75806476"
---
# <a name="manage-access-to-services-in-configuration-manager"></a>Gestire l'accesso ai servizi in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare l'accesso condizionale per specificare le condizioni necessarie per proteggere la posta elettronica e altri servizi in dispositivi registrati in Microsoft Intune.  

> [!Important]  
> MDM ibrida che include l'accesso condizionale locale sono [funzionalità deprecate](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Per altre informazioni, vedere [Informazioni sulla gestione di dispositivi mobili ibrida](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  
> 
> Se si usa l'accesso condizionale nei dispositivi gestiti con il client di Configuration Manager, per assicurarsi che siano ancora protetti, abilitare prima di tutto l'accesso condizionale in Intune per tali dispositivi prima della migrazione. Abilitare la co-gestione in Configuration Manager, spostare il carico di lavoro dei criteri di conformità in Intune e quindi completare la migrazione da Intune ibrido a Intune autonomo. Per altre informazioni, vedere [accesso condizionale con la co-gestione](https://docs.microsoft.com/sccm/comanage/quickstart-conditional-access). 


 Per informazioni sull'accesso condizionale nei dispositivi gestiti con il client di Configuration Manager, vedere [gestire l'accesso ai servizi di Office 365 per i PC gestiti da Configuration Manager](../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  


 Lo schema seguente illustra come funziona l'accesso condizionale:  

 ![ConditionalAccess4](media/ConditionalAccess4.png)  

 Usare l'accesso condizionale per gestire l'accesso ai seguenti servizi:  

- Microsoft Exchange locale  

- Microsoft Exchange Online  

- Exchange Online dedicato  

- SharePoint Online  

- Skype for Business Online

- Dynamics CRM Online

  Per implementare l'accesso condizionale vengono configurati due tipi di criteri in Configuration Manager:  

- **I criteri di conformità** sono criteri facoltativi che è possibile distribuire alle raccolte dell'utente per valutare impostazioni come:  

  - Passcode  

  - Encryption  

  - Se il dispositivo è jailbroken o rooted  

  - Se la posta elettronica nel dispositivo è gestita da criteri di Configuration Manager o Microsoft Intune  

    Un dispositivo segnala la conformità a tutti i criteri di accesso condizionale se non vengono distribuiti criteri di conformità nel dispositivo interessato.

- I **criteri di accesso condizionale** si riferiscono a un determinato servizio. Questi criteri definiscono alcune regole, ad esempio quale gruppo utenti di sicurezza di Azure Active Directory o quale raccolta utenti usare come destinazione oppure escludere.  

   I criteri di accesso condizionale per Exchange locale vengono configurati dalla console di Configuration Manager. Tuttavia, quando si configurano criteri di Exchange Online o SharePoint Online, la console di Microsoft Intune si apre per consentire la configurazione dei criteri.  

   A differenza degli altri criteri di Microsoft Intune o Configuration Manager, i criteri di accesso condizionale non vengono distribuiti, ma configurati una sola volta prima di essere applicati a tutti gli utenti di destinazione.  

  Se i dispositivi non soddisfano le condizioni configurate, l'utente viene guidato nel processo di registrazione del dispositivo e di risoluzione del problema che rende il dispositivo non conforme.  

Prima di iniziare a usare l'accesso condizionale, verificare che i requisiti richiesti siano soddisfatti:  

## <a name="requirements-for-exchange-online-using-the-shared-multi-tenant-environment"></a>Requisiti per Exchange Online (con un ambiente condiviso multi-tenant)
L'accesso condizionale a Exchange Online supporta i dispositivi che eseguono:
- Windows 8.1 e versioni successive (se registrato con Intune)
- Windows 7.0 o Windows 8.1 (se aggiunto a un dominio)
- Windows Phone 8.1 e versioni successive
- iOS 7.1 e versioni successive
- Android 4.0 e versioni successive, Samsung KNOX Standard 4.0 e versioni successive

  **Inoltre**:
- I dispositivi devono essere aggiunti all'area di lavoro, che registra il dispositivo con Azure Active Directory Device Registration Service (AAD DRS).<br />     
- I PC aggiunti a un dominio devono essere registrati automaticamente in Azure Active Directory tramite i criteri di gruppo o MSI.

  La sezione **Accesso condizionale per i PC** in questo articolo descrive tutti i requisiti necessari per abilitare l'accesso condizionale per un PC.<br />     
  Il servizio DRS di AAD viene attivato automaticamente per i clienti di Microsoft Intune e Office 365. I clienti che hanno già distribuito il servizio Device Registration Service di AD FS non visualizzano i dispositivi registrati in Active Directory locale.
- Usare un abbonamento a Office 365 che include Exchange Online (ad esempio E3). Gli utenti devono avere la licenza per Exchange Online.
- Il connettore Exchange Server è facoltativo e connette Configuration Manager a Microsoft Exchange Online. Questo connettore consente di monitorare le informazioni sul dispositivo tramite la console di Configuration Manager. Per altre informazioni, vedere [Gestire i dispositivi mobili con Configuration Manager ed Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
  Il connettore non è necessario per usare i criteri di conformità o i criteri di accesso condizionale. Il connettore è invece richiesto per eseguire report di valutazione dell'impatto dell'accesso condizionale.

## <a name="requirements-for-exchange-online-dedicated"></a>Requisiti per Exchange Online dedicato
L'accesso condizionale di Exchange Online dedicato supporta i dispositivi che eseguono:
- Windows 8 e versioni successive (se registrato con Intune)
- Windows 7.0 o Windows 8.1 (se aggiunto a un dominio)

  Accesso condizionale ai PC aggiunti al dominio soltanto per i tenant del nuovo ambiente Exchange Online dedicato.
- Windows Phone 8 e versioni successive
- Dispositivi iOS che usano i client di posta elettronica di Exchange ActiveSync (EAS)
- Android 4 e versioni successive.
- Per i tenant nell'ambiente legacy Exchange Online dedicato:    

  Usare il connettore Exchange Server che connette Configuration Manager a Microsoft Exchange locale. Il connettore consente di gestire i dispositivi mobili e abilita l'accesso condizionale. Per altre informazioni, vedere [Gestire i dispositivi mobili con Configuration Manager ed Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
- Per i tenant nel nuovo ambiente Exchange Online dedicato:     
  Il connettore Exchange Server è facoltativo, connette Configuration Manager a Microsoft Exchange Online e consente di gestire le informazioni sul dispositivo. Per altre informazioni, vedere [Gestire i dispositivi mobili con Configuration Manager ed Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md). Il connettore non è necessario per usare i criteri di conformità o i criteri di accesso condizionale. Il connettore è invece richiesto per eseguire report di valutazione dell'impatto dell'accesso condizionale.  

## <a name="requirements-for-exchange-on-premises"></a>Requisiti per Exchange locale
L'accesso condizionale a Exchange locale supporta:
- Windows 8 e versioni successive (se registrato con Intune)
- Windows Phone 8 e versioni successive
- App di posta elettronica nativa in iOS
- App di posta elettronica nativa in Android versione 4 o successiva
- L'app Microsoft Outlook non è supportata (Android e iOS)

**Inoltre**:

- La versione di Exchange deve essere Exchange 2010 o successiva
- È supportato un array del server Accesso client di Exchange Server

> [!TIP]
> Se l'ambiente di Exchange si trova in una configurazione con server CAS, sarà necessario configurare On-Premises Exchange Connector in modo che punti a uno dei server CAS.
> - Usare il connettore Exchange Server che connette Configuration Manager a Microsoft Exchange locale. Il connettore consente di gestire i dispositivi mobili e abilita l'accesso condizionale. Per altre informazioni, vedere [Gestire i dispositivi mobili con Configuration Manager ed Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
>   - Accertarsi di usare la versione più recente di Exchange Connector locale. Configurare On-premises Exchange Connector tramite la console di Configuration Manager. Per una procedura dettagliata, vedere [gestire i dispositivi mobili con Configuration Manager ed Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).
>   - Configurare il connettore solo nel sito primario di Configuration Manager

- È possibile configurare Exchange ActiveSync con l'autenticazione basata sui certificati o tramite l'immissione di credenziali utente


## <a name="requirements-for-skype-for-business-online"></a>Requisiti per Skype for Business Online
L'accesso condizionale a Skype Online supporta i dispositivi che eseguono:
- iOS 7.1 e versioni successive
- Android 4.0 e versioni successive
- Samsung KNOX Standard 4.0 o versioni successive

Abilitare l'[autenticazione moderna](https://aka.ms/SkypeModernAuth) per Skype for Business Online. 

Tutti gli utenti devono usare Skype for Business Online. Se si ha una distribuzione con Skype for Business Online e Skype for Business locale, i criteri di accesso condizionale non vengono applicati agli utenti locali.

## <a name="requirements-for-sharepoint-online"></a>Requisiti per SharePoint Online
L'accesso condizionale a SharePoint Online supporta i dispositivi che eseguono:
- Windows 8.1 e versioni successive (se registrato con Intune)
- Windows 7.0 o Windows 8.1 (se aggiunto a un dominio)
- Windows Phone 8.1 e versioni successive
- iOS 7.1 e versioni successive
- Android 4.0 e versioni successive, Samsung KNOX Standard 4.0 e versioni successive

  **Inoltre**:
- I dispositivi devono essere aggiunti all'area di lavoro, che registra il dispositivo con Azure Active Directory Device Registration Service (AAD DRS).

  I PC aggiunti a un dominio devono essere registrati automaticamente in Azure Active Directory tramite i criteri di gruppo o MSI. La sezione **Accesso condizionale per i PC** in questo articolo descrive tutti i requisiti necessari per abilitare l'accesso condizionale per un PC.

  Il servizio DRS di AAD viene attivato automaticamente per i clienti di Microsoft Intune e Office 365. I clienti che hanno già distribuito il servizio Device Registration Service di AD FS non visualizzano i dispositivi registrati in Active Directory locale.
- Una sottoscrizione a SharePoint Online è obbligatoria e gli utenti devono avere una licenza per SharePoint Online.

  ### <a name="conditional-access-for-pcs"></a>Accesso condizionale per i PC

  È possibile configurare l'accesso condizionale per i PC che eseguono applicazioni desktop di Office e accedere a Exchange Online o SharePoint Online. I PC devono soddisfare i requisiti seguenti:
- Il PC deve eseguire Windows 7.0 o Windows 8.1
- Il PC deve essere aggiunto a un dominio oppure conforme

  Affinché sia ritenuto conforme, il PC deve essere registrato in Microsoft Intune e deve rispettare i criteri.

  Per i PC aggiunti a un dominio, è necessario configurare la [registrazione automatica del dispositivo](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/) con Azure Active Directory.
- [L'autenticazione moderna di Office 365 deve essere abilitata](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/) ed è necessario disporre di tutti gli aggiornamenti di Office più recenti.<br />     L'autenticazione moderna garantisce accesso basato su Active Directory Authentication Library (ADAL) ai client Windows di Office 2013 e offre migliori opzioni di sicurezza, ad esempio, l'autenticazione a più fattori e l'autenticazione basata sui certificati.
- Configurare le regole delle attestazioni ADFS per bloccare i protocolli di autenticazione non moderni.  

## <a name="next-steps"></a>Passaggi successivi  
 Leggere i seguenti argomenti per informazioni su come configurare i criteri di conformità e i criterio di accesso condizionale per lo scenario richiesto:  

- [Gestire i criteri di conformità dei dispositivi](../../protect/deploy-use/device-compliance-policies.md)  

- [Gestire l'accesso alla posta elettronica](../../protect/deploy-use/manage-email-access.md)  

- [Gestire l'accesso a SharePoint Online](../../protect/deploy-use/manage-sharepoint-online-access.md)  

- [Gestire l'accesso a Skype for Business Online](../../protect/deploy-use/manage-skype-for-business-online-access.md)  

### <a name="see-also"></a>Vedere anche  

 [Introduzione alle impostazioni di conformità](../../compliance/get-started/get-started-with-compliance-settings.md)

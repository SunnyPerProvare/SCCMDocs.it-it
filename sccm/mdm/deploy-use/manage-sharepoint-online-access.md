---
title: Gestire l'accesso a SharePoint Online
titleSuffix: Configuration Manager
description: Informazioni su come usare i criteri di accesso condizionale di SharePoint Online in System Center Configuration Manager per gestire l'accesso a OneDrive.
ms.custom: na
ms.date: 12/09/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49cec466-1676-4fe2-a2fe-5004f01d735e
caps.latest.revision: "11"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: 99b2aca418b7ce28a4216b38e711b3d38973e2b7
ms.sourcegitcommit: 372171a5cd8d143d6d47b651018cda0c91cad67c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/09/2017
---
# <a name="manage-sharepoint-online-access-in-system-center-configuration-manager"></a>Gestire l'accesso a SharePoint Online in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


Usare i criteri di accesso condizionale di **SharePoint Online** in System Center Configuration Manager per gestire l'accesso ai file di OneDrive for Business disponibili in SharePoint Online, in base alle condizioni specificate.
È possibile controllare l'accesso a SharePoint Online dalle seguenti app per le piattaforme elencate:  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android e iOS)  

-   Microsoft Word (Android e iOS)  

-   Microsoft Excel (Android e iOS)  

-   Microsoft PowerPoint (Android e iOS)  

-   Microsoft OneNote (Android e iOS)

Le applicazioni desktop di Office possono accedere a SharePoint Online nei PC che eseguono:  

-   Office Desktop 2013 e versioni successive con l' [autenticazione moderna](https://support.office.com/en-US/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) abilitata.  

-   Windows 7.0 o Windows 8.1  

> [!NOTE]  
>  I PC devono essere aggiunti a un dominio oppure essere conformi ai criteri impostati in Intune.  



 Quando un utente di destinazione prova a connettersi a un file usando un'app supportata, come OneDrive installata nel dispositivo, vengono effettuate le valutazioni seguenti.  

 ![ConditionalAccess8&#45;6](media/ConditionalAccess8-6.png)  

 Per connettersi ai file richiesti, il dispositivo che esegue OneDrive:  

-   Deve essere registrato in Microsoft Intune o essere un PC aggiunto a un dominio.  

-   Registrare il dispositivo in Azure Active Directory. L'operazione viene eseguita automaticamente quando il dispositivo è registrato in Intune.  

     Per i PC aggiunti a un dominio, è necessario configurarli in modo che vengano [registrati automaticamente](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-automatic-device-registration/) con Azure Active Directory.  

-   Deve essere compatibile con i criteri di compatibilità di Configuration Manager distribuiti  

 Lo stato del dispositivo viene archiviato in Azure Active Directory che consente o blocca l'accesso ai file, in base alle condizioni specificate.  

 Se non viene soddisfatta una condizione, viene visualizzato uno dei due messaggi seguenti quando l'utente esegue l'accesso:  

-   Se il dispositivo non è registrato con Intune oppure non è registrato in Azure Active Directory, viene visualizzato un messaggio contenente le istruzioni su come installare l'app Portale aziendale ed eseguire la registrazione.  

-   Se il dispositivo non è conforme, viene visualizzato un messaggio che indirizza l'utente al portale Web di Intune dove sono disponibili informazioni sul problema e su come risolverlo.  

- Per i dispositivi mobili:

  È possibile limitare l'accesso a SharePoint Online da browser di dispositivi **iOS** e **Android**.  L'accesso verrà consentito solo da browser supportati di dispositivi compatibili:
* Safari (iOS)
* Chrome (Android)
* Managed Browser (iOS e Android)

  I browser non supportati verranno bloccati.
-   Per un PC:  


    -   Se i criteri sono impostati in modo da richiedere l'aggiunta a un dominio e il PC non è aggiunto a un dominio, viene visualizzato un messaggio che indica di contattare l'amministratore IT.  

    -   Se i criteri sono impostati in modo da richiedere l'aggiunta a un dominio o la conformità e il PC non soddisfa questi criteri, viene visualizzato un messaggio con le istruzioni su come installare l'app Portale aziendale ed eseguire la registrazione.  

 È possibile bloccare l'accesso a SharePoint Online dalle app seguenti:  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android e iOS)  

-   Microsoft Word (Android e iOS)  

-   Microsoft Excel (Android e iOS)  

-   Microsoft PowerPoint (Android e iOS)  

-   Microsoft OneNote (Android e iOS)  

## <a name="configure-conditional-access-for-sharepoint-online"></a>Configurare l'accesso condizionale per SharePoint Online  

### <a name="step-1-configure-active-directory-security-groups"></a>Passaggio 1: Configurare i gruppi di sicurezza di Active Directory  
 Prima di iniziare configurare i gruppi di sicurezza di Azure Active Directory per i criteri di accesso condizionale. È possibile configurare questi gruppi nel **centro di amministrazione di Office 365**o nel **portale per gli account di Intune**. Questi gruppi contengono gli utenti a cui saranno destinati i criteri o che ne saranno esenti. Per poter accedere alle risorse, un utente di destinazione in un criterio deve usare solo dispositivi conformi.  

 In un criterio di SharePoint Online è possibile specificare due tipi di gruppi:  

-   **Gruppi di destinazione**: contiene i gruppi di utenti per i quali si applicano i criteri  

-   **Gruppi esentati**: contiene i gruppi di utenti che sono esentati dai criteri (facoltativo)  

 Se un utente si trova in entrambi i gruppi, sarà esentato dai criteri.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Passaggio 2: Configurare e distribuire i criteri di conformità  
 Assicurarsi di creare e distribuire un criterio di conformità in tutti i dispositivi a cui saranno destinati i criteri di SharePoint Online.  

> [!NOTE]  
>  Mentre i criteri di conformità vengono distribuiti in gruppi di Intune o in raccolte di Configuration Manager, i criteri di accesso condizionale sono destinati ai gruppi di sicurezza di Azure Active Directory.  

 Per informazioni dettagliate su come configurare i criteri di conformità, vedere [Gestire i criteri di conformità del dispositivo in System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md).  

> [!IMPORTANT]  
>  Se non sono stati distribuiti criteri di conformità e non sono stati abilitati i criteri di SharePoint Online, l'accesso sarà consentito a tutti i dispositivi di destinazione.  

 Quando si è pronti, continuare con il **Passaggio 3**.  

###  <a name="BKMK_OneDrive"></a> Passaggio 3: Configurare i criteri di SharePoint Online  


 A questo punto, configurare i criteri in modo che solo i dispositivi gestiti e conformi possano accedere a SharePoint Online. Questi criteri verranno archiviati in Azure Active Directory.

 >[!NOTE]
 >È possibile creare i criteri di accesso condizionale anche nella console di gestione di Azure AD. La console di gestione di Azure AD consente di creare i criteri di accesso condizionale dei dispositivi Intune (chiamati criteri di accesso condizionale basati su dispositivo in Azure AD) oltre ad altri criteri di accesso condizionale come Multi-Factor Authentication. È anche possibile impostare criteri di accesso condizionale per app aziendali di terze parti supportate da Azure AD, ad esempio Salesforce e Box. Per altre informazioni, vedere [Come impostare criteri di accesso condizionale basato su dispositivo di Azure Active Directory per controllare gli accessi delle applicazioni connesse ad Azure Active Directory](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access-policy-connected-applications/).  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Selezionare **Abilita criteri di accesso condizionale per SharePoint Online**.  

     ![IntuneSASharePointOnlineCAPolicy](media/IntuneSASharePointOnlineCAPolicy.png)  

3.  In **Accesso all'applicazione** per Outlook e le app che usano l'autenticazione moderna è possibile scegliere di limitare l'accesso solo ai dispositivi conformi per le singole piattaforme.  

    > [!TIP]  
    >  Con**Autenticazione moderna** i client Office possono usare l'accesso basato su Active Directory Authentication Library (ADAL).  
    >   
    >  -   Questo tipo di autenticazione consente ai client Office di usare l'autenticazione basata su browser, nota anche come autenticazione passiva.  Per eseguire l'autenticazione, l'utente viene indirizzato a una pagina Web di accesso.  
    > -   Questo nuovo metodo di accesso offre nuovi scenari, tra cui l'accesso condizionale, basato sulla **conformità del dispositivo** e sull'uso dell' **autenticazione a più fattori** .  
    >   
    >  Questo [articolo](https://support.office.com/en-US/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517) contiene informazioni più dettagliate sul funzionamento dell'autenticazione moderna.  

     I PC Windows devono essere aggiunti a un dominio oppure devono essere registrati in Intune ed essere conformi. È possibile impostare i requisiti seguenti:  

    -   **I dispositivi devono essere aggiunti a un dominio o conformi.** Questo significa che i PC devono essere aggiunti a un dominio o essere conformi ai criteri impostati in Intune. Se il PC non soddisfa alcuno dei requisiti, all'utente verrà richiesto di registrare il dispositivo in Intune.  

    -   **I dispositivi devono essere aggiunti a un dominio.** Ciò significa che per accedere a Exchange Online i PC devono essere aggiunti a un dominio. Se il PC non è aggiunto a un dominio, l'accesso alla posta elettronica è bloccato e all'utente viene richiesto di contattare l'amministratore IT.  

    -   **I dispositivi devono essere conformi.** Questo significa che i PC devono essere registrati in Intune ed essere conformi. Se il PC non è registrato, viene visualizzato un messaggio con le istruzioni su come eseguire la registrazione.  

4.  In **Browser access** (Accesso al browser) per SharePoint Online e OneDrive for Business è possibile scegliere di consentire l'accesso a Exchange Online esclusivamente tramite i browser supportati: Safari (iOS) e Chrome (Android). Non sarà possibile accedere da altri browser.  Vengono applicate anche le restrizioni di piattaforma selezionate per l'accesso all'applicazione per OneDrive.

    Nei dispositivi **Android** è necessario che gli utenti abilitino l'accesso al browser.  A tale scopo, l'utente finale deve abilitare l'opzione **Abilita l'accesso al browser** nel dispositivo registrato come segue:
    1.  Avviare l' **app Portale aziendale**.
    2.  Passare alla pagina **Impostazioni** facendo clic sui punti di sospensione (â€¦) o sul tasto di menu.
    3.  Scegliere il pulsante **Abilita l'accesso al browser** .
    4.  Nel browser Chrome disconnettersi da Office 365 e riavviare Chrome.

    Nelle piattaforme **iOS e Android** , per identificare il dispositivo usato per accedere al servizio, Azure Active Directory rilascia al dispositivo un certificato Transport Layer Security (TLS).  Il dispositivo visualizza il certificato richiedendo all'utente finale di selezionare il certificato come illustrato nelle schermate seguenti. Per continuare a usare il browser è necessario che l'utente finale selezioni il certificato.

     **iOS**

     ![schermata del messaggio di richiesta del certificato in un iPad](media/mdm-browser-ca-ios-cert-prompt_v2.png)

     **Android**

      ![schermata del messaggio di richiesta del certificato in un dispositivo Android](media/mdm-browser-ca-android-cert-prompt.png)

4.  Nella scheda **Home** del gruppo **Collegamenti** fare clic su **Configura i criteri di accesso condizionale nella console di Intune**. Potrebbe essere necessario specificare il nome utente e la password dell'account usato per la connessione di Configuration Manager a Intune.  

     Verrà visualizzata la console di amministrazione di Intune.  

5.  Nella console di [console di amministrazione di Microsoft Intune](https://manage.microsoft.com)fare clic su **Criteri** > **Accesso condizionale** > **SharePoint Online Criteri**.  

6.  Selezionare **Bloccare l'accesso delle app a SharePoint Online se il dispositivo non è conforme**.  

7.  In **Gruppi di destinazione**fare clic su **Modifica** per selezionare i gruppi di sicurezza di Azure Active Directory ai quali verranno applicati i criteri.  

8.  Facoltativamente, in **Gruppi esentati**fare clic su **Modifica** per selezionare i gruppi di sicurezza di Azure Active Directory esentati da questi criteri.  

9. Al termine, fare clic su **Salva**.  

 Non è necessario distribuire i criteri di accesso condizionale perché diventano immediatamente effettivi.  

 Per informazioni su come monitorare i criteri dalla console di Intune, vedere [Limitare l'accesso a SharePoint Online con Microsoft Intune](https://technet.microsoft.com/library/dn705844.aspx).  

### <a name="see-also"></a>Vedere anche  

 [Gestire l'accesso ai servizi in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md)

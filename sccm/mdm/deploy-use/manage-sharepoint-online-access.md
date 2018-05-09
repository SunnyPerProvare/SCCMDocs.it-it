---
title: Gestire l'accesso a SharePoint Online
titleSuffix: Configuration Manager
description: Informazioni su come usare i criteri di accesso condizionale di SharePoint Online in System Center Configuration Manager per gestire l'accesso a OneDrive.
ms.date: 12/09/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 49cec466-1676-4fe2-a2fe-5004f01d735e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f723110abdb94dd96fb2ed7f52af681d27fccf87
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="manage-sharepoint-online-access-in-system-center-configuration-manager"></a>Gestire l'accesso a SharePoint Online in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


I criteri di accesso condizionale di Configuration Manager per **SharePoint Online** gestiscono l'accesso ai file di OneDrive for Business, archiviati in SharePoint Online. L'accesso si basa sulle condizioni specificate.
È possibile controllare l'accesso a SharePoint Online dalle seguenti app per le piattaforme elencate:  

-   Microsoft Office Mobile (Android)  

-   Microsoft OneDrive (Android e iOS)  

-   Microsoft Word (Android e iOS)  

-   Microsoft Excel (Android e iOS)  

-   Microsoft PowerPoint (Android e iOS)  

-   Microsoft OneNote (Android e iOS)

Le applicazioni desktop di Office possono accedere a SharePoint Online nei PC che eseguono:  

-   Office Desktop 2013 e versioni successive con l' [autenticazione moderna](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) abilitata.  

-   Windows 7.0 o Windows 8.1  

> [!NOTE]  
>  I PC devono essere aggiunti a un dominio oppure essere conformi ai criteri impostati in Intune.  



 Quando un utente di destinazione prova a connettersi a un file usando un'app supportata, ad esempio OneDrive, installata nel dispositivo, vengono effettuate le valutazioni seguenti:  

 ![ConditionalAccess8&#45;6](media/ConditionalAccess8-6.png)  

 Per connettersi ai file richiesti, il dispositivo che esegue OneDrive:  

-   Deve essere registrato in Microsoft Intune o essere un PC aggiunto a un dominio.  

-   Registrare il dispositivo in Azure Active Directory (Azure AD). La registrazione avviene automaticamente quando il dispositivo è registrato in Intune.  

     Per i PC aggiunti a un dominio, è necessario configurarli in modo che vengano [registrati automaticamente](/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) in Azure AD.  

-   Deve essere compatibile con i criteri di compatibilità di Configuration Manager distribuiti  

    Azure AD archivia lo stato del dispositivo. Consente o blocca l'accesso ai file, in base alle condizioni specificate.  

    Se una condizione non viene soddisfatta, all'accesso dell'utente viene visualizzato uno dei messaggi seguenti:  

-   Se il dispositivo non è registrato in Intune oppure non è registrato in Azure AD, viene visualizzato un messaggio contenente le istruzioni su come installare l'app Portale aziendale ed eseguire la registrazione.  

-   Se il dispositivo non è conforme, viene visualizzato un messaggio che indirizza l'utente al portale Web di Intune. Nel portale l'utente troverà le informazioni sul problema e su come risolverlo.  

- Per i dispositivi mobili:

  È possibile limitare l'accesso a SharePoint Online da browser di dispositivi **iOS** e **Android**. L'accesso è consentito solo da browser supportati di dispositivi conformi:  
    - Safari (iOS)
    - Chrome (Android)
    - Managed Browser (iOS e Android)  

    I browser non supportati sono bloccati.  

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
 Prima di iniziare, configurare i gruppi di sicurezza di Azure AD per i criteri di accesso condizionale. È possibile configurare questi gruppi nel **centro di amministrazione di Office 365**o nel **portale per gli account di Intune**. Questi gruppi includono gli utenti a cui sono destinati i criteri o che ne sono esenti. Per accedere alle risorse, gli utenti a cui sono destinati i criteri devono usare solo dispositivi conformi.  

 In un criterio di SharePoint Online è possibile specificare due tipi di gruppi:  

-   **Gruppi di destinazione**: contiene i gruppi di utenti per i quali si applicano i criteri.  

-   **Gruppi esentati**: contiene i gruppi di utenti che sono esentati dai criteri (facoltativo).  

 Se un utente si trova in entrambi i gruppi, è esentato dai criteri.  

### <a name="step-2-configure-and-deploy-a-compliance-policy"></a>Passaggio 2: Configurare e distribuire i criteri di conformità  
 Creare i criteri di conformità e distribuirli a tutti i dispositivi ai quali sono destinati i criteri di SharePoint Online.  

> [!NOTE]   
>  Mentre i criteri di conformità vengono distribuiti ai gruppi di Intune o alle raccolte di Configuration Manager, i criteri di accesso condizionale sono destinati ai gruppi di sicurezza di Azure AD.  

 Per informazioni dettagliate su come configurare i criteri di conformità, vedere [Gestire i criteri di conformità del dispositivo in System Center Configuration Manager](../../protect/deploy-use/device-compliance-policies.md).  

> [!IMPORTANT]  
>  Se i criteri di conformità non sono stati distribuiti e quindi si abilitano i criteri di SharePoint Online, l'accesso sarà consentito a tutti i dispositivi di destinazione.  

   

###  <a name="BKMK_OneDrive"></a> Passaggio 3: Configurare i criteri di SharePoint Online  

 A questo punto, configurare i criteri in modo che solo i dispositivi gestiti e conformi possano accedere a SharePoint Online. Questi criteri sono archiviati in Azure AD.

 >[!NOTE]
 >È possibile creare i criteri di accesso condizionale anche nella console di gestione di Azure AD. La console di gestione di Azure AD consente di creare i criteri di accesso condizionale dei dispositivi Intune. In Azure AD questi vengono denominati criteri di accesso condizionale basati su dispositivo. È possibile creare anche altri criteri di accesso condizionale, come l'autenticazione a più fattori. Nel portale è possibile impostare criteri di accesso condizionale per app aziendali di terze parti supportate da Azure AD, ad esempio Salesforce e Box. Per altre informazioni, vedere [Come configurare i criteri di accesso condizionale basato su dispositivo di Azure AD per controllare gli accessi delle applicazioni connesse ad Azure AD](/azure/active-directory/active-directory-conditional-access-policy-connected-applications).  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Selezionare **Abilitare i criteri di accesso condizionale per SharePoint Online**.  

     ![IntuneSASharePointOnlineCAPolicy](media/IntuneSASharePointOnlineCAPolicy.png)  

3.  In **Accesso all'applicazione** per Outlook e le app che usano l'autenticazione moderna è possibile scegliere di limitare l'accesso solo ai dispositivi conformi per le singole piattaforme.  

    > [!TIP]  
    >  Con l'**autenticazione moderna**, i client Office possono usare l'accesso basato su Active Directory Authentication Library (ADAL).  
    >   
    >  -   Questo tipo di autenticazione consente ai client Office di usare l'autenticazione basata su browser, nota anche come autenticazione passiva. Per eseguire l'autenticazione, l'utente viene indirizzato a una pagina Web di accesso.  
    > -   Questo nuovo metodo di accesso apre nuovi scenari, ad esempio l'accesso condizionale basato sulla **conformità del dispositivo** e sull'uso dell'**autenticazione a più fattori**.  
    >   
    >  Per altre informazioni, vedere [Funzionamento dell'autenticazione moderna per le applicazioni client di Office 2013 e Office 2016](https://support.office.com/article/How-modern-authentication-works-for-Office-2013-and-Office-2016-client-apps-e4c45989-4b1a-462e-a81b-2a13191cf517).  

     I PC Windows devono essere aggiunti a un dominio oppure devono essere registrati in Intune ed essere conformi. È possibile impostare i requisiti seguenti:  

    -   **I dispositivi devono essere aggiunti a un dominio o conformi**: i PC devono essere aggiunti a un dominio o essere conformi ai criteri impostati in Intune. Se il PC non soddisfa nessuno dei due requisiti, all'utente verrà richiesto di registrare il dispositivo in Intune.  

    -   **I dispositivi devono essere aggiunti a un dominio**: per accedere a Exchange Online i PC devono essere aggiunti a un dominio. Se il PC non è aggiunto a un dominio, l'accesso alla posta elettronica è bloccato e all'utente viene richiesto di contattare l'amministratore IT.  

    -   **I dispositivi devono essere conformi**: i PC devono essere registrati in Intune ed essere conformi. Se il PC non è registrato, viene visualizzato un messaggio con le istruzioni su come eseguire la registrazione.  

4.  In **Browser access** (Accesso al browser) per SharePoint Online e OneDrive for Business è possibile scegliere di consentire l'accesso a Exchange Online esclusivamente tramite i browser supportati: Safari (iOS) e Chrome (Android). Non è possibile accedere da altri browser. Vengono applicate anche le restrizioni di piattaforma selezionate per l'accesso all'applicazione per OneDrive.

    Per i dispositivi **Android**, gli utenti devono abilitare l'opzione **Abilita l'accesso al browser** nel dispositivo registrato seguendo questa procedura:
    1.  Avviare l' **app Portale aziendale**.
    2.  Passare alla pagina **Impostazioni** facendo clic sui punti di sospensione (...) o sul tasto di menu.
    3.  Scegliere il pulsante **Abilita l'accesso al browser** .
    4.  Nel browser Chrome disconnettersi da Office 365 e riavviare Chrome.

    Nelle piattaforme **iOS e Android**, per identificare il dispositivo usato per accedere al servizio, Azure AD rilascia al dispositivo un certificato TLS. Il dispositivo visualizza il certificato richiedendo all'utente finale di selezionare il certificato come illustrato nelle schermate seguenti. Per continuare a usare il browser è necessario che l'utente finale selezioni il certificato.

     **iOS**

     ![schermata del messaggio di richiesta del certificato in un iPad](media/mdm-browser-ca-ios-cert-prompt_v2.png)

     **Android**

      ![schermata del messaggio di richiesta del certificato in un dispositivo Android](media/mdm-browser-ca-android-cert-prompt.png)

4.  Nella scheda **Home** del gruppo **Collegamenti** fare clic su **Configura i criteri di accesso condizionale nella console di Intune**. Potrebbe essere necessario specificare il nome utente e la password dell'account usato per la connessione di Configuration Manager a Intune.  

     Viene visualizzata la console di amministrazione di Intune.  

5.  Nella console di [console di amministrazione di Microsoft Intune](https://manage.microsoft.com)fare clic su **Criteri** > **Accesso condizionale** > **SharePoint Online Criteri**.  

6.  Selezionare **Bloccare l'accesso delle app a SharePoint Online se il dispositivo non è conforme**.  

7.  In **Gruppi di destinazione** fare clic su **Modifica** per selezionare i gruppi di sicurezza di Azure AD ai quali vengono applicati i criteri.  

8.  Facoltativamente, in **Gruppi esentati** fare clic su **Modifica** per selezionare i gruppi di sicurezza di Azure AD esentati da questi criteri.  

9. Al termine, fare clic su **Salva**.  

 Non è necessario distribuire i criteri di accesso condizionale perché diventano immediatamente effettivi.  

 Per informazioni su come monitorare i criteri dalla console di Intune, vedere [Limitare l'accesso a SharePoint Online con Microsoft Intune](/intune-classic/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune).  

### <a name="see-also"></a>Vedere anche  

 [Gestire l'accesso ai servizi in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md)

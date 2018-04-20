---
title: Gestire l'accesso ai servizi di O365
titleSuffix: Configuration Manager
description: Informazioni su come configurare l'accesso condizionale ai servizi di Office 365 per i PC gestiti da System Center Configuration Manager.
ms.custom: na
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 34024741-edfa-4088-8599-d6bafc331e62
caps.latest.revision: 15
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1e02cb911397d5f1f837996318b12049d328c9c3
ms.sourcegitcommit: fb84bcb31d825f454785e3d9d8be669e00fe2b27
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2018
---
# <a name="manage-access-to-o365-services-for-pcs-managed-by-system-center-configuration-manager"></a>Gestire l'accesso ai servizi di O365 per i PC gestiti da System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

<!--1191496-->
Configurare l'accesso condizionale ai servizi di Office 365 per i PC gestiti da Configuration Manager.  

> [!Note]  
> Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Abilitare le funzionalità facoltative degli aggiornamenti](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Per informazioni sulla configurazione dell'accesso condizionale per dispositivi registrati e gestiti da Microsoft Intune, vedere [Gestire l'accesso ai servizi in System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md). Questo articolo riguarda anche i dispositivi che vengono aggiunti al dominio e la cui conformità non viene valutata.

## <a name="supported-services"></a>Servizi supportati  

-   Exchange Online
-   SharePoint Online

## <a name="supported-pcs"></a>PC supportati  

-   Windows 7
-   Windows 8.1
-   Windows 10

## <a name="supported-windows-servers"></a>Versioni supportate di Windows Server

-   Windows Server 2008 R2
-   Windows Server 2012
-   Windows Server 2012 R2
-   Windows Server 2016

    > [!IMPORTANT]
    > Per le istanze di Windows Server a cui possono accedere più utenti contemporaneamente, distribuire gli stessi criteri di accesso condizionale a tutti gli utenti interessati.

## <a name="configure-conditional-access"></a>Configurare l'accesso condizionale  
 Per configurare l'accesso condizionale, è prima di tutto necessario creare i criteri di conformità e configurare i criteri di accesso condizionale. Quando si configurano i criteri di accesso condizionale per i PC, è possibile richiedere che i PC siano conformi ai criteri per accedere ai servizi di Exchange Online e SharePoint Online.  

### <a name="prerequisites"></a>Prerequisiti  

-   ADFS Sync e un abbonamento a O365. L'abbonamento a Office 365 serve per la configurazione di Exchange Online e SharePoint Online.  

-   Sottoscrizione di Microsoft Intune. La sottoscrizione di Microsoft Intune deve essere configurata nella console di Configuration Manager. La sottoscrizione di Intune viene usata per trasmettere lo stato di conformità del dispositivo ad Azure Active Directory e per la gestione delle licenze utente.  

 I PC devono soddisfare i requisiti seguenti:  

-   [Prerequisiti](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) per la registrazione automatica dei dispositivi con Azure Active Directory  

     È possibile registrare i PC con Azure AD tramite i criteri di conformità.  

    -   Per i PC Windows 8.1 e Windows 10, è possibile usare un oggetto Criteri di gruppo di Active Directory per configurare i dispositivi per la registrazione automatica con Azure AD.  

    -   o   Per i PC Windows 7, è necessario distribuire il pacchetto software di registrazione dei dispositivi nel PC Windows 7 con System Center Configuration Manager. L'articolo [Registrazione automatica dei dispositivi con Azure Active Directory per i dispositivi Windows aggiunti a un dominio](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup) offre informazioni più dettagliate.  

-   I PC devono usare Office 2013 o Office 2016 con l'autenticazione moderna [abilitata](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a).  

 I passaggi seguenti si applicano sia a Exchange Online sia a SharePoint Online  

### <a name="step-1-configure-compliance-policy"></a>Passaggio 1. Configurare i criteri di conformità  
 Nella console di Configuration Manager creare criteri di conformità con le regole seguenti:  

-   **Richiedi registrazione in Azure Active Directory**: questa regola controlla se il dispositivo dell'utente è aggiunto all'area di lavoro in Azure AD e, in caso contrario, il dispositivo viene registrato automaticamente in Azure AD. La registrazione automatica è supportata solo in Windows 8.1. Per i PC con Windows 7, distribuire un file MSI per eseguire la registrazione automatica. Per altre informazioni, vedere [Registrazione automatica dei dispositivi con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  

-   **Tutti gli aggiornamenti richiesti installati con una scadenza maggiore di X giorni:** questa regola specifica il valore del periodo di prova partendo dalla scadenza della distribuzione per gli aggiornamenti necessari nel dispositivo utente. L'aggiunta di questa regola comporta l'installazione automatica degli aggiornamenti necessari in sospeso. Specificare gli aggiornamenti necessari nella regola **Aggiornamenti automatici necessari**.   

-   **Richiedi Crittografia unità BitLocker:** questa regola controlla se l'unità principale (ad esempio, C:\\) nel dispositivo è crittografata con BitLocker. Se la crittografia Bitlocker non è abilitata nel dispositivo primario, l'accesso alla posta elettronica e ai servizi di SharePoint è bloccato.  

-   **Richiedi antimalware:** questa regola controlla se System Center Endpoint Protection o Windows Defender è abilitato e in esecuzione. Se non è abilitato, l'accesso alla posta elettronica e ai servizi di SharePoint è bloccato.  

-   **Segnalato come integro dal servizio di attestazione dell'integrità di Windows (Health Attestation Service):** questa condizione include quattro sottoregole per verificare la conformità del dispositivo rispetto al servizio di attestazione dell'integrità di dispositivo. Per altre informazioni, vedere [Attestazione dell'integrità](/sccm/core/servers/manage/health-attestation). 

    - **Richiedi l'abilitazione di BitLocker nel dispositivo**
    - **Richiedi l'abilitazione dell'avvio sicuro nel dispositivo** 
    - **Richiedi l'abilitazione dell'integrità del codice nel dispositivo**
    - **Richiedi l'abilitazione di antimalware ad esecuzione anticipata nel dispositivo**  

    >[!Tip]  
    > I criteri di accesso condizionale per l'attestazione dell'integrità dei dispositivi sono stati introdotti per la prima volta nella versione 1710 come [funzionalità di una versione non definitiva](/sccm/core/servers/manage/pre-release-features). A partire dalla versione 1802, questa funzionalità non è più in versione non definitiva.<!--1235616-->  

    > [!Note]  
    > Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Abilitare le funzionalità facoltative degli aggiornamenti](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

### <a name="step-2-evaluate-the-effect-of-conditional-access"></a>Passaggio 2: Valutare l'effetto dell'accesso condizionale  
 Eseguire il **report di conformità dell'accesso condizionale**, disponibile nell'area di lavoro **Monitoraggio** in **Report** > **Gestione conformità e impostazioni**. Il report indica lo stato di conformità di tutti i dispositivi. Ai dispositivi segnalati come non conformi viene impedito l'accesso a Exchange Online e SharePoint Online.  

 ![Console di Configuration Manager, area di lavoro Monitoraggio, Creazione di report, Report, Gestione conformità e impostazioni: Report di conformità dell'accesso condizionale](media/CA_compliance_report.png)  

### <a name="configure-active-directory-security-groups"></a>Configurare i gruppi di sicurezza di Active Directory  
 I criteri di accesso condizionale sono destinati a diversi gruppi di utenti in base ai tipi di criteri. Questi gruppi contengono gli utenti a cui sono destinati i criteri o che ne sono esenti. Quando a un utente viene destinato un criterio, ogni dispositivo in uso deve essere conforme per accedere al servizio.  

 Gruppi di utenti di sicurezza di Active Directory. Questi gruppi di utenti devono essere sincronizzati con Azure Active Directory. È anche possibile configurare questi gruppi nell'interfaccia di amministrazione di Office 365 o nel portale per gli account di Intune.  

 È possibile specificare due tipi di gruppi in ogni criterio. :  

-   **Gruppi di destinazione**: gruppi di utenti a cui si applicano i criteri. Usare lo stesso gruppo per i criteri di conformità e di accesso condizionale.  

-   **Gruppi esentati**: gruppi di utenti esenti dai criteri (facoltativo).  
    Se un utente si trova in entrambi i gruppi, viene esentato dai criteri.  

     Solo i gruppi di destinazione dei criteri di accesso condizionale vengono valutati.  

### <a name="step-3-create-a-conditional-access-policy-for-exchange-online-and-sharepoint-online"></a>Passaggio 3. Creare criteri di accesso condizionale per Exchange Online e SharePoint Online  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Per creare criteri per Exchange Online, selezionare **Abilita criteri di accesso condizionale per Exchange Online**.  

     Per creare criteri per SharePoint Online, selezionare **Abilita criteri di accesso condizionale per SharePoint Online**.  

3.  Nella scheda **Home** del gruppo **Collegamenti** fare clic su **Configura i criteri di accesso condizionale nella console di Intune**. Potrebbe essere necessario specificare il nome utente e la password dell'account usato per la connessione di Configuration Manager a Intune.  

     Viene visualizzata la console di amministrazione di Intune.  

4.  Per Exchange Online, nella console di amministrazione di Microsoft Intune fare clic su **Criteri > Accesso condizionale > Criteri di Exchange Online**.  

     Per SharePoint Online, nella console di amministrazione di Microsoft Intune fare clic su **Criteri > Accesso condizionale > Criteri di SharePoint Online**.  

5.  Impostare il requisito per il PC Windows sull'opzione**I dispositivi devono essere conformi**.  

6.  In **Gruppi di destinazione** fare clic su **Modifica** per selezionare i gruppi di sicurezza di Azure Active Directory ai quali vengono applicati i criteri.  

    > [!NOTE]  
    >  È necessario usare lo stesso gruppo di utenti di sicurezza per la distribuzione dei criteri di conformità e il gruppo di destinazione per i criteri di accesso condizionale.  

     Facoltativamente, in **Gruppi esentati**fare clic su **Modifica** per selezionare i gruppi di sicurezza di Azure Active Directory esentati da questi criteri.  

7.  Fare clic su **Salva** per creare e salvare i criteri.  

Le informazioni sulla conformità vengono visualizzate in Software Center. Quando viene bloccato l'accesso per mancata conformità, avviare una nuova valutazione dei criteri dopo aver corretto i problemi di conformità.  


## <a name="see-also"></a>Vedere anche

- [Protect data and site infrastructure with System Center Configuration Manager](../../protect/understand/protect-data-and-site-infrastructure.md) (Proteggere i dati e l'infrastruttura del sito con System Center Configuration Manager)
- [Diagramma di flusso per la risoluzione dei problemi di accesso condizionale di Configuration Manager](https://gallery.technet.microsoft.com/Conditional-access-fd747c1a?redir=0)

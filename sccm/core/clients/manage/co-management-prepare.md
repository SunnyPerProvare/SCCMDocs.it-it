---
title: Preparare Windows 10 per la co-gestione
titleSuffix: Configuration Manager
description: Informazioni su come preparare i dispositivi Windows 10 per la co-gestione.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/10/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: ac7f67a02602473a7635d8c70e4b1b1dc04363bc
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53417048"
---
# <a name="prepare-windows-10-devices-for-co-management"></a>Preparare i dispositivi Windows 10 per la co-gestione
È possibile abilitare la co-gestione nei dispositivi Windows 10 aggiunti ad Active Directory e Azure AD e registrati in Microsoft Intune e che siano client di Configuration Manager. Per i nuovi dispositivi Windows 10 e per i dispositivi già registrati in Intune, installare il client di Configuration Manager prima di attivare la co-gestione. Per i dispositivi Windows 10 che sono già client di Configuration Manager, è possibile registrare i dispositivi con Intune e abilitare la co-gestione dalla console di Configuration Manager.

> [!IMPORTANT]
> I dispositivi mobili Windows 10 non supportano la co-gestione.



## <a name="prerequisites"></a>Prerequisiti

Prima di poter abilitare la co-gestione, è necessario soddisfare i prerequisiti seguenti. Esistono sia prerequisiti generali che prerequisiti diversi per i dispositivi con il client di Configuration Manager e quelli in cui non è installato.


### <a name="general-prerequisites"></a>Prerequisiti generali

Di seguito sono elencati i prerequisiti generali per abilitare la co-gestione:  

- Configuration Manager 1710 o versioni successive  

    - A partire da Configuration Manager versione 1806, è possibile connettere più istanze di Configuration Manager a un singolo tenant di Intune. <!--1357944-->  

- [Integrazione con Azure AD per la Gestione cloud](/sccm/core/servers/deploy/configure/azure-services-wizard)  

- Licenza di EMS o Intune per tutti gli utenti  

- [Registrazione automatica in Azure AD](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) abilitata  

- Sottoscrizione a Intune e autorità MDM di Intune impostata su **Intune**.  

    - Se si usa l'[autorità mista](/sccm/mdm/deploy-use/migrate-mixed-authority), completare prima la migrazione a Intune autonomo. Quindi impostare l'autorità MDM su Intune prima di impostare la co-gestione.<!--SCCMDocs issue #797-->


> [!NOTE]
> Se si ha un ambiente MDM ibrido, ovvero Intune integrato con Configuration Manager, non è possibile abilitare la co-gestione. È tuttavia possibile avviare la migrazione degli utenti a Intune autonomo e quindi abilitare i dispositivi Windows 10 ad essi associati per la co-gestione. Per altre informazioni sulla migrazione a Intune autonomo, vedere [Avviare la migrazione da MDM ibrido a Intune autonomo](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).


### <a name="prerequisite-azure-resource-manager-roles"></a>Prerequisiti in termini di ruoli di Azure Resource Manager
<!--SCCMDocs issue #667--> Per altre informazioni sui ruoli di Azure, vedere [Informazioni sui diversi ruoli](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles).

|Action|Ruolo necessario|
|----|----|
|Configurare un gateway di gestione cloud|Gestione di sottoscrizioni di Azure|
|Configurare un punto di distribuzione cloud|Gestione di sottoscrizioni di Azure|
|Creare app Azure Active Directory dalla console di Configuration Manager|Amministratore globale di Azure Active Directory|
|Importare app client e server Azure nella console di Configuration Manager| Amministratore di Configuration Manager, nessun altro ruolo di Azure necessario|
|Configurare la co-gestione tramite l'apposita procedura guidata| Diritti utente di Azure Active Directory e ruolo di amministratore di Configuration Manager con tutti i diritti per l'ambito 


### <a name="additional-prerequisites-for-devices-with-the-configuration-manager-client"></a>Prerequisiti aggiuntivi per i dispositivi con il client di Configuration Manager

- Windows 10, versione 1709 o successiva  

- [Aggiunto ad Azure AD ibrido](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) (aggiunto ad Active Directory e Azure AD) o aggiunto solo ad Azure AD (questo tipo a volte viene definito "aggiunto al dominio cloud").


### <a name="additional-prerequisites-for-devices-without-the-configuration-manager-client"></a>Prerequisiti aggiuntivi per i dispositivi senza il client di Configuration Manager

- Windows 10, versione 1709 o successiva  

- [Cloud Management Gateway](/sccm/core/clients/manage/manage-clients-internet#cloud-management-gateway) in Configuration Manager (quando si usa Intune per installare il client di Configuration Manager)  


> [!IMPORTANT]
> I dispositivi mobili Windows 10 non supportano la co-gestione.



## <a name="command-line-to-install-configuration-manager-client"></a>Riga di comando per installare il client di Configuration Manager

Creare un'app in Intune per i dispositivi Windows 10 che non sono ancora client di Configuration Manager. A tale scopo, attenersi alla seguente procedura:

1. Passare a portal.azure.com e quindi aprire il pannello di Intune.
2. Fare clic su **App client** > **App** > **Aggiungi**. 
3. In **Altro** selezionare **App line-of-business**.
4. Caricare il file del pacchetto dell'app Ccmsetup.msi. Il file si trova nella cartella seguente sul server del sito: <*directory di installazione di ConfigMgr*>\bin\i386. 
5. Dopo l'aggiornamento dell'app, configurare le informazioni sull'app eseguendo l'argomento della riga di comando seguente:

`ccmsetup.msi CCMSETUPCMD="/mp:<URL of cloud management gateway mutual auth endpoint> CCMHOSTNAME=<URL of cloud management gateway mutual auth endpoint> SMSSiteCode=<Sitecode> SMSMP=https://<FQDN of MP> AADTENANTID=<AAD tenant ID> AADCLIENTAPPID=<Server AppID for AAD Integration> AADRESOURCEURI=https://<Resource ID>"`

#### <a name="example-command-line-input"></a>Esempio di input di riga di comando
Se sono disponibili i seguenti valori:

- **URL dell'endpoint di autenticazione reciproca di Cloud Management Gateway**: `https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500`    

   >[!NOTE]    
   >Usare il valore **MutualAuthPath** nella visualizzazione di SQL **vProxy_Roles** per il valore dell'**URL dell'endpoint di autenticazione reciproca di Cloud Management Gateway**.  

- **FQDN del punto di gestione (MP)**: `mp1.contoso.com`    
- **Sitecode**: `PS1`    
- **ID tenant di Azure AD**: `44b5bdda-67f5-4850-bdf4-a8ef611109e0`    
- **ID app client di Azure AD**: `51e781eb-aac6-4265-8030-4cd1ddaa9dd0`     
- **URI ID risorsa AAD**: `ConfigMgrServer`    

  > [!NOTE]    
  > Usare il valore **IdentifierUri** trovato nella visualizzazione SQL **vSMS_AAD_Application_Ex** per il valore **URI ID risorsa AAD**.  

Quindi, usare la riga di comando seguente:

`ccmsetup.msi CCMSETUPCMD="/mp:https://contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=PS1 SMSMP=https://mp1.contoso.com AADTENANTID=44b5bdda-67f5-4850-bdf4-a8ef611109e0 AADCLIENTAPPID=51e781eb-aac6-4265-8030-4cd1ddaa9dd0 AADRESOURCEURI=https://ConfigMgrServer"`


<!--1358215--> A partire dalla versione 1806, sono necessarie meno proprietà della riga di comando.  

- Le seguenti proprietà della riga di comando sono richieste in tutti gli scenari:  
    - CCMHOSTNAME  
    - SMSSITECODE  

- Le seguenti proprietà sono richieste quando si usa Azure AD per l'autenticazione client anziché i certificati di autenticazione client basati su infrastruttura a chiave pubblica:  
    - AADCLIENTAPPID  
    - AADRESOURCEURI  

- La seguente proprietà è obbligatoria se il client effettua il roaming alla rete intranet:  
    - SMSMP  

L'esempio seguente include tutte le proprietà indicate sopra:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Per altre informazioni, vedere [Informazioni sulle proprietà di installazione del client in System Center Configuration Manager](/sccm/core/clients/deploy/about-client-installation-properties).


> [!TIP]
> Trovare i parametri della riga di comando per il sito usando la procedura seguente:     
> 
> 1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Co-gestione**.  
> 
> 2. Nella barra multifunzione selezionare **Configura la co-gestione** per aprire il caricamento guidato della co-gestione. Se la co-gestione è già stata configurata, selezionare **Proprietà**. Quindi andare al passaggio 4.    
> 
> 3. Nella pagina Sottoscrizione fare clic su **Accedi**. Accedere al tenant di Intune e quindi fare clic su **Avanti**.    
> 
> 4. Nella pagina Abilitazione selezionare **Copia** per copiare la riga di comando negli Appunti. Salvare quindi la riga di comando da usare nella procedura per creare l'app.  
> 
> 5. Per uscire dalla procedura guidata, fare clic su **Annulla**.  

> [!IMPORTANT]    
> Se si personalizza la riga di comando per installare il client di Configuration Manager, verificare che la riga di comando non superi i 1024 caratteri. Se la riga di comando è maggiore di 1024 caratteri, l'installazione del client non riesce.



## <a name="new-windows-10-devices"></a>Nuovi dispositivi Windows 10

Per i nuovi dispositivi Windows 10, è possibile usare il servizio AutoPilot per la configurazione guidata, che include l'aggiunta del dispositivo ad AD e Azure AD, nonché la registrazione del dispositivo in Intune. In seguito, creare un'app in Intune per distribuire il client di Configuration Manager.  

1. Abilitare AutoPilot per i nuovi dispositivi Windows 10. Per informazioni dettagliate, vedere [Panoramica di Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).    

   > [!NOTE]   
   > A partire dalla versione 1802, usare Configuration Manager per raccogliere e segnalare le informazioni sul dispositivo richieste da Microsoft Store per le aziende e per la formazione. Queste informazioni includono il numero di serie del dispositivo, l'identificatore del prodotto Windows e un ID hardware. Nell'area di lavoro **Monitoraggio** della console di Configuration Manager espandere il nodo **Report**, espandere **Report** e selezionare il nodo **Hardware - Generale**. Eseguire il nuovo report **Informazioni sui dispositivi di Windows AutoPilot** e visualizzare i risultati. Nel visualizzatore report fare clic sull'icona **Esporta** e selezionare l'opzione **CSV (delimitato da virgole)**. Dopo aver salvato il file, caricare i dati in Microsoft Store per le aziende e per la formazione. Per altre informazioni, vedere [Add devices in Microsoft Store for Business and Education](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile) (Aggiungere dispositivi in Microsoft Store per le aziende e per la formazione).

2. Configurare la registrazione automatica in Azure AD perché registri automaticamente i dispositivi in Intune. Per informazioni dettagliate, vedere  [Registrazione di dispositivi Windows](https://docs.microsoft.com/intune/windows-enroll).  

3. Creare un'app in Intune con il pacchetto client di Configuration Manager e distribuire l'app ai dispositivi Windows 10 per i quali si vuole abilitare la co-gestione. Usare la [riga di comando per installare il client di Configuration Manager](#command-line-to-install-configuration-manager-client) quando si eseguono i passaggi per [installare i client da Internet tramite Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).   



## <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Dispositivi Windows 10 non registrati in Intune o che non hanno il client di Configuration Manager

Per i dispositivi Windows 10 che non sono registrati in Intune o non hanno il client di Configuration Manager, è possibile usare la registrazione automatica per registrare il dispositivo in Intune. In seguito, creare un'app in Intune per distribuire il client di Configuration Manager.

1. Configurare la registrazione automatica in Azure AD perché registri automaticamente i dispositivi in Intune. Per informazioni dettagliate, vedere  [Registrazione di dispositivi Windows](https://docs.microsoft.com/intune/windows-enroll).  

2. Creare un'app in Intune con il pacchetto client di Configuration Manager e distribuire l'app ai dispositivi Windows 10 per i quali si vuole abilitare la co-gestione. Usare la [riga di comando per installare il client di Configuration Manager](#command-line-to-install-configuration-manager-client) quando si eseguono i passaggi per [installare i client da Internet tramite Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).



## <a name="windows-10-devices-enrolled-in-intune"></a>Dispositivi Windows 10 registrati in Intune

Per i dispositivi Windows 10 che sono già registrati in Intune, creare un'app in Intune per distribuire il client di Configuration Manager. Usare la [riga di comando per installare il client di Configuration Manager](#command-line-to-install-configuration-manager-client) quando si eseguono i passaggi per [installare i client da Internet tramite Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).  



## <a name="next-steps"></a>Passaggi successivi

[Passare i carichi di lavoro di Configuration Manager a Intune](co-management-switch-workloads.md)

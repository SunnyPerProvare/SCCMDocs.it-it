---
title: Installare il client con Azure AD
titleSuffix: Configuration Manager
description: Installare e assegnare il client di Configuration Manager in dispositivi Windows 10 usando Azure Active Directory per l'autenticazione
ms.date: 03/28/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b722187a895a71b4195200354180cdbc8b2813e6
ms.sourcegitcommit: 12b71da551350c99c5916df3629e33e31040db15
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/17/2018
ms.locfileid: "53530915"
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Installare e assegnare client di Configuration Manager in dispositivi Windows 10 usando Azure AD per l'autenticazione

Per installare il client di Configuration Manager nei dispositivi Windows 10 con l'autenticazione di Azure AD, integrare Configuration Manager con Azure Active Directory (Azure AD). I client possono essere sulla Intranet in comunicazione diretta con un punto di gestione abilitato per HTTPS o con qualsiasi punto di comunicazione in un sito abilitato per HTTP avanzato. Possono anche essere basati su Internet e comunicare attraverso il gateway di gestione cloud o un punto di gestione basato su Internet. Questo processo usa Azure AD per autenticare i client per il sito di Configuration Manager. Azure AD evita di dover configurare e usare i certificati di autenticazione client.



## <a name="before-you-begin"></a>Prima di iniziare

- Un tenant di Azure AD è un prerequisito  

- Requisiti dei dispositivi:  

    - Windows 10  

    - Aggiunto ad Azure AD, aggiunto solo al dominio cloud o ibrido aggiunto ad Azure AD  

- Requisiti dell'utente:  

    - L'utente che ha effettuato l'accesso deve essere un'identità di Azure AD.   

    - Se l'utente è un'identità federata o sincronizzata, è necessario usare l'[individuazione utenti di Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser) nonché l'[individuazione utenti di Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc) in Configuration Manager. Per altre informazioni sulle identità ibride, vedere [Definire una strategia di adozione della soluzione ibrida di gestione delle identità](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->  

- Oltre ai [prerequisiti esistenti](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012MPpreq) per il ruolo del sistema del sito punto di gestione, abilitare anche **ASP.NET 4.5** in questo server. Includere eventuali altre opzioni che vengono automaticamente selezionate quando si abilita ASP.NET 4.5.  

- Determinare se il punto di gestione richiede HTTPS. Per altre informazioni, vedere [Abilitare i punti di gestione per HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps).  

- Se necessario, configurare un [gateway di gestione cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) per distribuire i client basati su Internet. Per i client locali che eseguono l'autenticazione con Azure AD, non è necessario un gateway di gestione cloud.  


## <a name="configure-azure-services-for-cloud-management"></a>Configurare i servizi di Azure per la gestione cloud

Connettere il sito di Configuration Manager ad Azure AD come primo passaggio. Per informazioni dettagliate su questo processo, vedere [Configurare i servizi di Azure da usare con Configuration Manager](/sccm/core/servers/deploy/configure/azure-services-wizard). Creare una connessione al servizio **Gestione cloud**.

Abilitare l'[individuazione di utenti di Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc) come parte dell'onboarding in **Gestione cloud**. 

Eseguite queste operazioni, il sito di Configuration Manager è connesso ad Azure AD. 



## <a name="configure-client-settings"></a>Configurare le impostazioni client

Queste impostazioni client consentono di aggiungere i dispositivi Windows 10 con Azure AD. Consentono inoltre di abilitare i client basati su Internet per l'uso del gateway di gestione cloud e del punto di distribuzione cloud.

1.  Configurare le seguenti impostazioni client nella sezione **Servizi cloud** usando le informazioni contenute in [Come configurare le impostazioni client in System Center Configuration Manager](/sccm/core/clients/deploy/configure-client-settings).  

    - **Consentire accesso al punto di distribuzione cloud**: abilitare questa impostazione per consentire ai dispositivi basati su Internet di ottenere il contenuto necessario per l'installazione del client di Configuration Manager. Se il contenuto non è disponibile nel punto di distribuzione cloud, dispositivi possono recuperarlo dal gateway di gestione cloud. Il bootstrap di installazione del client ritenta il punto di distribuzione cloud per quattro ore prima di eseguire il fallback al gateway di gestione cloud.<!--495533-->  

    - **Registra automaticamente i nuovi dispositivi Windows 10 aggiunti al dominio con Azure Active Directory**: impostare su **Sì** o **No**. L'impostazione predefinita è **Sì**. Questo è il comportamento predefinito anche in Windows 10, versione 1709.

    - **Consenti ai client di usare un gateway di gestione cloud** impostato su **Sì** (impostazione predefinita) o **No**.  

2.  Distribuire le impostazioni client per la raccolta necessaria di dispositivi. Non distribuire queste impostazioni alle raccolte di utenti.

Per verificare se il dispositivo è stato aggiunto ad Azure AD, eseguire `dsregcmd.exe /status` in un prompt dei comandi. Il campo **AzureAdjoined** nei risultati visualizza **SÌ** se il dispositivo è stato aggiunto ad Azure AD.



## <a name="install-and-register-the-client-using-azure-ad-identity"></a>Installare e registrare il client usando l'identità di Azure AD

Per installare manualmente il client usando l'identità di Azure AD, per prima cosa esaminare il processo generale nella sezione [Come installare manualmente i client](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual). 

 > [!Note]  
 > Il dispositivo richiede l'accesso a Internet per contattare Azure AD, ma non deve necessariamente essere basato su Internet. 

L'esempio seguente illustra la struttura generale della riga di comando: `ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`

Per altre informazioni, vedere [Informazioni sulle proprietà di installazione del client in System Center Configuration Manager](/sccm/core/clients/deploy/about-client-installation-properties).

Le proprietà /mp e CCMHOSTNAME specificano uno degli elementi seguenti, a seconda dello scenario:
- Punto di gestione locale. Specificare solo la proprietà /mp. La proprietà CCMHOSTNAME non è obbligatoria.
- Gateway di gestione cloud
- Punto di gestione basato su Internet La proprietà SMSMP specifica il punto di gestione locale o basato su Internet.

In questo esempio viene usato un gateway di gestione cloud. Sostituisce i valori di esempio per ogni proprietà: `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

Per automatizzare l'installazione del client usando l'identità di Azure AD con Microsoft Intune, vedere la procedura di [preparazione dei dispositivi Windows 10 per la co-gestione](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client).



## <a name="next-steps"></a>Passaggi successivi

Al termine dell'operazione, è possibile continuare a [monitorare e gestire i client](/sccm/core/clients/manage/monitor-clients).

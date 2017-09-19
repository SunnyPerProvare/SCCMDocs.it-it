---
title: Installare e assegnare il client da Internet | Microsoft Docs
description: Installare e assegnare il client di System Center Configuration Manager da Internet.
ms.custom: na
ms.date: 8/07/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
caps.latest.revision: "14"
caps.handback.revision: "0"
author: arob98
ms.author: angrobe
manager: angrobe
ms.openlocfilehash: d783cc2f12400084ad1cd62a338a31c9747c05fb
ms.sourcegitcommit: f6a428a8db7145affa388f59e0ad880bdfcf17b5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/14/2017
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Installare e assegnare client di Configuration Manager in dispositivi Windows 10 usando Azure AD per l'autenticazione

È possibile usare i servizi cloud di Configuration Manager con Azure AD a supporto degli scenari seguenti:

- Installare manualmente il client di Configuration Manager in dispositivi Windows 10 da Internet e assegnarlo a un sito di Configuration Manager. Richiede il ruolo del sistema del sito di Cloud Management Gateway.
- Usare Azure AD per autenticare i client per l'accesso ai siti di Configuration Manager. Azure AD evita di dover configurare e usare i certificati di autenticazione client.
- Individuare nel sito gli utenti di Azure AD che possono quindi essere usati nelle raccolte e in altre operazioni di Configuration Manager.

Per eseguire questa operazione, usare la procedura seguente:

- **Passaggio 1: Configurare l'app Servizi di Azure in Servizi cloud di Configuration Manager e configurare l'individuazione utenti in Azure AD**
- **Passaggio 2: Configurare Cloud Management Gateway** (operazione facoltativa per i client locali)
- **Passaggio 3: Configurare le impostazioni del client per l'aggiunta di dispositivi Windows 10 tramite Azure AD e abilitare i client all'uso di Cloud Management Gateway**
- **Passaggio 4: Installare e registrare il client di Configuration Manager tramite l'identità di Azure Active Directory**


## <a name="before-you-start"></a>Prima di iniziare

- È necessario disporre di un tenant di Azure AD.
- I dispositivi devono eseguire Windows 10, essere aggiunti ad Azure AD e devono aver eseguito l'accesso usando un'identità di Azure AD. Oltre che ad Azure AD, i client possono essere anche aggiunti al dominio.
- Oltre ai [prerequisiti esistenti](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) per il ruolo del sistema del sito del punto di gestione, è anche necessario verificare che **ASP.NET 4.5** e qualsiasi altra opzione selezionata automaticamente siano abilitati nel computer che ospita questo ruolo del sistema del sito.
- Per usare Configuration Manager per distribuire il client:
    - Configurare almeno un punto di gestione per la modalità HTTPS se per l'autenticazione si vuole usare Azure AD invece dei certificati client.
        Se invece di usare Cloud Management Gateway si usano i certificati client, il punto di gestione HTTPS è facoltativo, ma consigliato. Se per l'autenticazione si usa Azure AD, sia per i client locali sia per i client Internet, il punto di gestione HTTPS è necessario.
    - Per distribuire client Internet, configurare un Cloud Management Gateway. Per i client locali autenticati tramite Azure AD, non è necessario configurare Cloud Management Gateway.


## <a name="step-1-set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Passaggio 1: Configurare l'app Servizi di Azure in Servizi cloud di Configuration Manager

In questo modo il sito di Configuration Manager viene connesso ad Azure AD; si tratta di un prerequisito per tutte le altre operazioni di questa sezione. 

L'individuazione di utenti di Azure AD viene configurata come parte di *Gestione cloud*. La relativa procedura è illustrata in dettaglio nel passaggio **6** della procedura [Creare l'app Web di Azure da usare con Configuration Manager](/sccm/core/servers/deploy/configure/Azure-services-wizard#webapp) nell'argomento *Configurare i servizi di Azure da usare con Configuration Manager*.
    
Una volta completata la procedura, il sito di Configuration Manager è connesso ad Azure AD. 

## <a name="step-2-set-up-the-cloud-management-gateway"></a>Passaggio 2: Configurare Cloud Management Gateway

Configurare Cloud Management Gateway per abilitare gli scenari di gestione cloud descritti in questo argomento. Per le informazioni della Guida, vedere gli argomenti seguenti: 

- [Pianificare il gateway di gestione cloud in Configuration Manager](/sccm/core/clients/manage/plan-cloud-management-gateway).
- [Configurare il gateway di gestione cloud per Configuration Manager](/sccm/core/clients/manage/setup-cloud-management-gateway).
- [Monitorare il gateway di gestione cloud in Configuration Manager](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway).

## <a name="step-3-configure-client-settings-to-join-windows-10-devices-with-azure-ad-and-enable-clients-to-use-the-cloud-management-gateway"></a>Passaggio 3: Configurare le impostazioni del client per l'aggiunta di dispositivi Windows 10 tramite Azure AD e abilitare i client all'uso di Cloud Management Gateway

1.  Configurare la sezione seguente di impostazioni client (in **Servizi cloud**) tramite le informazioni contenute in [Come configurare le impostazioni client in System Center Configuration Manager](/sccm/core/clients/deploy/configure-client-settings).
    - **Consentire accesso al punto di distribuzione cloud**: abilitare questa impostazione per consentire ai dispositivi basati su Internet di ottenere il contenuto necessario per l'installazione del client di Configuration Manager. Se il contenuto non è disponibile nel punto di distribuzione cloud, i dispositivi possono recuperarlo da un punto di gestione connesso a Cloud Management Gateway.
    - **Registra automaticamente i nuovi dispositivi Windows 10 aggiunti al dominio con Azure Active Directory** impostato su **Sì** (impostazione predefinita) o **No**.
    - **Consenti ai client di usare un gateway di gestione cloud** impostato su **Sì** (impostazione predefinita) o **No**.
2.  Distribuire le impostazioni client per la raccolta necessaria di dispositivi. Non distribuire queste impostazioni alle raccolte di utenti.

Per verificare che il dispositivo sia stato aggiunto ad Azure AD, eseguire il comando **dsregcmd.exe /status** in una finestra del prompt dei comandi. Il campo **AzureAdjoined** nei risultati visualizza **SÌ** se il dispositivo è stato aggiunto ad Azure AD.


## <a name="step-4-install-and-register-the-configuration-manager-client-using-azure-active-directory-identity"></a>Passaggio 4: Installare e registrare il client di Configuration Manager tramite l'identità di Azure Active Directory

Per installare il client, usare quindi le istruzioni in [Come distribuire i client nei computer Windows in System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually) con la riga di comando per l'installazione seguente: 

**ccmsetup.exe /mp&#58; https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057594037928100 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=DFD SMSMP=https://SCCMDFPSS.contoso.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011DB47 AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d17026 AADRESOURCEURI=https://contososerver**

- **/MP**: origine del download. In caso di avvio da Internet, questo valore può essere impostato su CMG.
- **CCMHOSTNAME**: nome del punto di gestione Internet. È possibile trovarlo eseguendo **gwmi - namespace root\ccm\locationservices-classe SMS_ActiveMPCandidate** da un prompt dei comandi in un client gestito.
- **SMSSiteCode**: codice del sito di Configuration Manager.
- **SMSMP:** nome del punto di gestione di ricerca. Il punto di gestione può trovarsi all'interno della rete Intranet.
- **AADTENANTID**, **AADTENANTNAME**: nome e ID del tenant di Azure AD collegato a Configuration Manager. È possibile trovarlo eseguendo dsregcmd.exe /status da un prompt dei comandi su dispositivo aggiunto ad Azure AD.
- **AADCLIENTAPPID**: ID dell'app client di Azure AD. Per informazioni su come trovarlo, vedere [Usare il portale per creare un'applicazione Azure Active Directory e un'entità servizio che possano accedere alle risorse](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key).
- **AADResourceUri**: URI identificatore dell'app server di Azure AD caricata. Per altre informazioni, vedere [Configurare i servizi di Azure da usare con Configuration Manager](/sccm/core/servers/deploy/configure/azure-services-wizard).




## <a name="next-steps"></a>Passaggi successivi

Al termine dell'operazione, è possibile continuare a [monitorare e gestire i client](/sccm/core/clients/manage/monitor-clients).

---
title: Installare e assegnare il client da Internet | Microsoft Docs
description: Installare e assegnare il client di System Center Configuration Manager da Internet.
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
caps.latest.revision: 14
caps.handback.revision: 0
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.translationtype: HT
ms.sourcegitcommit: 3c75c1647954d6507f9e28495810ef8c55e42cda
ms.openlocfilehash: f604557d208b2dda9dc1c6b4c4d27d896d47695e
ms.contentlocale: it-it
ms.lasthandoff: 07/29/2017

---

# <a name="install-and-assign-configuration-manager-clients-from-the-internet-using-azure-ad-for-authentication"></a>Installare e assegnare client di Configuration Manager da Internet usando Azure AD per l'autenticazione

È possibile usare i servizi cloud di Configuration Manager con Azure AD a supporto degli scenari seguenti:

- Installare manualmente il client di Configuration Manager da Internet e assegnarlo a un sito di Configuration Manager. Richiede il ruolo del sistema del sito di Cloud Management Gateway.
- Usare Azure AD per autenticare i client in Internet per l'accesso ai siti di Configuration Manager. Azure AD evita di dover configurare e usare i certificati di autenticazione client.
- Individuare nel sito gli utenti di Azure AD che possono quindi essere usati nelle raccolte e in altre operazioni di Configuration Manager.

Per eseguire questa operazione, usare la procedura seguente:

- **Passaggio 1: Configurare Cloud Management Gateway**
- **Passaggio 2: Configurare l'app Servizi di Azure in Servizi cloud di Configuration Manager**
- **Passaggio 3: Configurare impostazioni client per registrare dispositivi Windows 10 con Azure AD**
- **Passaggio 4: Installare e registrare il client di Configuration Manager tramite l'identità di Azure Active Directory**


## <a name="before-you-start"></a>Prima di iniziare

- È necessario disporre di un tenant di Azure AD.
- I dispositivi devono eseguire Windows 10 ed essere aggiunti ad Azure AD. Oltre che ad Azure AD, i client possono essere anche aggiunti al dominio.
- Oltre ai [prerequisiti esistenti](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) per il ruolo del sistema del sito del punto di gestione, è anche necessario verificare che **ASP.NET 4.5** e qualsiasi altra opzione selezionata automaticamente siano abilitati nel computer che ospita questo ruolo del sistema del sito.
- Per usare Configuration Manager per distribuire il client:
    - Configurare almeno un punto di gestione per la modalità HTTPS.
    - Configurare un Cloud Management Gateway.

## <a name="step-1-set-up-the-cloud-management-gateway"></a>Passaggio 1: Configurare Cloud Management Gateway

Configurare Cloud Management Gateway per consentire ai client di accedere al sito di Configuration Manager da Internet senza certificati. Per le informazioni della Guida, vedere gli argomenti seguenti: 

- [Pianificare il gateway di gestione cloud in Configuration Manager](/sccm/core/clients/manage/plan-cloud-management-gateway).
- [Configurare il gateway di gestione cloud per Configuration Manager](/sccm/core/clients/manage/setup-cloud-management-gateway).
- [Monitorare il gateway di gestione cloud in Configuration Manager](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway).

## <a name="step-2-set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Passaggio 2: Configurare l'app Servizi di Azure in Servizi cloud di Configuration Manager

In questo modo il sito di Configuration Manager viene connesso ad Azure AD; si tratta di un prerequisito per tutte le altre operazioni di questa sezione. 

L'individuazione di utenti di Azure AD viene configurata come parte di *Gestione cloud*. La relativa procedura è illustrata in dettaglio nel passaggio **6** della procedura [Creare l'app Web di Azure da usare con Configuration Manager](/sccm/core/servers/deploy/configure/Azure-services-wizard#webapp) nell'argomento *Configurare i servizi di Azure da usare con Configuration Manager*.
    
Una volta completata la procedura, il sito di Configuration Manager è connesso ad Azure AD. 

## <a name="step-3-configure-client-settings-to-register-windows-10-devices-with-azure-ad"></a>Passaggio 3: Configurare impostazioni client per registrare dispositivi Windows 10 con Azure AD

1.  Configurare la sezione seguente di impostazioni client (in Servizi cloud) tramite le informazioni contenute in [Come configurare le impostazioni client in System Center Configuration Manager](/sccm/core/clients/deploy/configure-client-settings).
    - **Registra automaticamente i nuovi dispositivi Windows 10 aggiunti al dominio con Azure Active Directory** impostato su **Sì** (impostazione predefinita) o **No**.
    - **Consenti ai client di usare un gateway di gestione cloud** impostato su **Sì** (impostazione predefinita) o **No**.
2.  Distribuire le impostazioni client per la raccolta necessaria di dispositivi.

Per verificare che il dispositivo sia stato aggiunto ad Azure AD, eseguire il comando **dsregcmd.exe /status** in una finestra del prompt dei comandi. Il campo **AzureAdjoined** nei risultati visualizza **SÌ** se il dispositivo è stato aggiunto ad Azure AD.


## <a name="step-4-install-and-register-the-configuration-manager-client-using-azure-active-directory-identity"></a>Passaggio 4: Installare e registrare il client di Configuration Manager tramite l'identità di Azure Active Directory

Prima di iniziare, verificare che i file di origine dell'installazione client vengano archiviati localmente nel dispositivo nel quale viene installato il client. Usare quindi le istruzioni in [Come distribuire i client nei computer Windows in System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually) con la riga di comando per l'installazione seguente: 

**ccmsetup.exe /NoCrlCheck /Source:C:\CLIENT CCMHOSTNAME=SCCMPROXYCONTOSO.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode=HEC AADTENANTID=780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME=contoso AADCLIENTAPPID= AADRESOURCEURI=https://contososerver**

- **/NoCrlCheck**: se il punto di gestione o Cloud Management Gateway usa un certificato server non pubblico, il client potrebbe non essere in grado di raggiungere il percorso CRL.
- **/Source**: cartella locale: posizione dei file di installazione del client.
- **CCMHOSTNAME**: nome del punto di gestione Internet. È possibile trovarlo eseguendo **gwmi - namespace root\ccm\locationservices-classe SMS_ActiveMPCandidate** da un prompt dei comandi in un client gestito.
- **SMSMP:** nome del punto di gestione di ricerca. Il punto di gestione può trovarsi all'interno della rete Intranet.
- **SMSSiteCode**: codice del sito di Configuration Manager.
- **AADTENANTID**, **AADTENANTNAME**: nome e ID del tenant di Azure AD collegato a Configuration Manager. È possibile trovarlo eseguendo dsregcmd.exe /status da un prompt dei comandi su dispositivo aggiunto ad Azure AD.
- **AADCLIENTAPPID**: ID dell'app client di Azure AD. Per informazioni su come trovarlo, vedere [Usare il portale per creare un'applicazione Azure Active Directory e un'entità servizio che possano accedere alle risorse](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key).
- **AADResourceUri**: URI identificatore dell'app server di Azure AD caricata.


## <a name="next-steps"></a>Passaggi successivi

Al termine dell'operazione, è possibile continuare a [monitorare e gestire i client](/sccm/core/clients/manage/monitor-clients).


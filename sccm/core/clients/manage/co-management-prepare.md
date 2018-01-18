---
title: Preparare i dispositivi Windows 10 per la co-gestione
description: Informazioni su come preparare i dispositivi Windows 10 per la co-gestione.
keywords: 
author: dougeby
manager: angrobe
ms.date: 11/20/2017
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology: 
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.openlocfilehash: d605dd4770be6878b08f4ac61da6ab27e3b6d61f
ms.sourcegitcommit: ac9268e31440ffe91b133c2ba8405d885248d404
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2018
---
# <a name="prepare-windows-10-devices-for-co-management"></a>Preparare i dispositivi Windows 10 per la co-gestione
È possibile abilitare la co-gestione nei dispositivi Windows 10 aggiunti ad Active Directory e Azure AD e registrati in Intune e che siano client di Configuration Manager. Per i nuovi dispositivi Windows 10 e per i dispositivi già registrati in Intune, installare il client di Configuration Manager prima di attivare la co-gestione. Per i dispositivi Windows 10 che sono già client di Configuration Manager, è possibile registrare i dispositivi con Intune e abilitare la co-gestione dalla console di Configuration Manager.

## <a name="command-line-to-install-configuration-manager-client"></a>Riga di comando per installare il client di Configuration Manager
È necessario creare un'app in Intune per i dispositivi Windows 10 che non sono già client di Configuration Manager. Quando si crea l'app nelle sezioni successive, usare la riga di comando seguente:

ccmsetup.msi CCMSETUPCMD="/mp:&#60;*URL dell'endpoint autorizzazione reciproca di Cloud Management Gateway*&#62;/ CCMHOSTNAME=&#60;*URL dell'endpoint autorizzazione reciproca di Cloud Management Gateway*&#62; SMSSiteCode=&#60;*Codice sito*&#62; SMSMP=https:&#47;/&#60;*FQDN del punto di gestione*&#62; AADTENANTID=&#60;*ID tenant AAD*&#62; AADTENANTNAME=&#60;*Nome tenant*&#62; AADCLIENTAPPID=&#60;*AppID del server per l'integrazione di AAD*&#62; AADRESOURCEURI=https:&#47;/&#60;*ID risorsa*&#62;"

Ad esempio, se sono stati restituiti i valori seguenti:

- **URL dell'endpoint di autenticazione reciproca di Cloud Management Gateway**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >Usare il valore **MutualAuthPath** nella visualizzazione di SQL **vProxy_Roles** per il valore dell'**URL dell'endpoint di autenticazione reciproca di Cloud Management Gateway**.

- **FQDN del punto di gestione** : sccmmp.corp.contoso.com    
- **Codice sito**: PS1    
- **ID del tenant di Azure AD**: 72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- **Nome del tenant di Azure AD**: contoso    
- **ID app client Azure AD**: bef323b3-042f-41a6-907a-f9faf0d1XXXX     
- **URI ID risorsa AAD**: ConfigMgrServer    

  > [!Note]    
  > Usare il valore **IdentifierUri** trovato nella visualizzazione SQL **vSMS_AAD_Application_Ex** per il valore **URI ID risorsa AAD**.

A tale scopo, usare la riga di comando seguente:

ccmsetup.msi CCMSETUPCMD="/mp:https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=PS1 SMSMP=https:/&#47;sccmmp.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d1XXXX AADRESOURCEURI=https:/&#47;ConfigMgrServer"

> [!Tip]
> È possibile trovare i parametri della riga di comando per il sito tramite la procedura seguente:     
> 1. Nella console di Configuration Manager accedere a **Amministrazione** > **Panoramica** > **Servizi cloud** > **Co-management** (Co-gestione).  
> 2. Nella scheda Home nel gruppo di gestione scegliere  **Configure co-management** (Configurazione co-gestione) per aprire il caricamento guidato della co-gestione.    
> 3. Nella pagina della sottoscrizione fare clic su **Accedi**, accedere al tenant di Intune e fare clic su **Avanti**.    
> 4. Nella pagina di attivazione fare clic su **Copia** nella sezione **Devices enrolled in Intune** (Dispositivi registrati in Intune) per copiare la riga di comando negli Appunti e quindi salvare la riga di comando da usare nella procedura per creare l'app.  
> 5. Per uscire dalla procedura guidata, fare clic su **Annulla**.

> [!Important]    
> Se si personalizza la riga di comando per installare il client di Configuration Manager, verificare che la riga di comando non superi i 1024 caratteri. Se la riga di comando è maggiore di 1024 caratteri, l'installazione del client non riesce.


## <a name="new-windows-10-devices"></a>Nuovi dispositivi Windows 10
Per i nuovi dispositivi Windows 10, è possibile usare il servizio AutoPilot per la configurazione guidata, che include l'aggiunta del dispositivo ad AD e Azure AD, nonché la registrazione del dispositivo in Intune. In seguito, creare un'app in Intune per distribuire il client di Configuration Manager.  
1. Abilitare AutoPilot per i nuovi dispositivi Windows 10. Per informazioni dettagliate, vedere [Panoramica di Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).  
2. Configurare la registrazione automatica in Azure AD perché registri automaticamente i dispositivi in Intune. Per informazioni dettagliate, vedere  [Registrazione di dispositivi Windows](https://docs.microsoft.com/intune/windows-enroll).
3. Creare un'app in Intune con il pacchetto client di Configuration Manager e distribuire l'app ai dispositivi Windows 10 per i quali si vuole abilitare la co-gestione. Usare la [riga di comando per installare il client di Configuration Manager](#command-line-to-install-configuration-manager-client) quando si eseguono i passaggi per [installare i client da Internet tramite Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).   

## <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Dispositivi Windows 10 non registrati in Intune o che non hanno il client di Configuration Manager
Per i dispositivi Windows 10 che non sono registrati in Intune o non hanno il client di Configuration Manager, è possibile usare la registrazione automatica in modo che vengano registrati in Intune. In seguito, creare un'app in Intune per distribuire il client di Configuration Manager.
1. Configurare la registrazione automatica in Azure AD perché registri automaticamente i dispositivi in Intune. Per informazioni dettagliate, vedere  [Registrazione di dispositivi Windows](https://docs.microsoft.com/intune/windows-enroll).  
2. Creare un'app in Intune con il pacchetto client di Configuration Manager e distribuire l'app ai dispositivi Windows 10 per i quali si vuole abilitare la co-gestione. Usare la [riga di comando per installare il client di Configuration Manager](#command-line-to-install-configuration-manager-client) quando si eseguono i passaggi per [installare i client da Internet tramite Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).

## <a name="windows-10-devices-enrolled-in-intune"></a>Dispositivi Windows 10 registrati in Intune
Per i dispositivi Windows 10 che sono già registrati in Intune, creare un'app in Intune per distribuire il client di Configuration Manager. Usare la [riga di comando per installare il client di Configuration Manager](#command-line-to-install-configuration-manager-client) quando si eseguono i passaggi per [installare i client da Internet tramite Azure AD](https://docs.microsoft.com/en-us/sccm/core/clients/deploy/deploy-clients-cmg-azure).  

## <a name="next-steps"></a>Passaggi successivi
[Passare i carichi di lavoro di Configuration Manager a Intune](co-management-switch-workloads.md)
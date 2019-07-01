---
title: Co-gestire i dispositivi basati su Internet
titleSuffix: Configuration Manager
description: Informazioni su come preparare i dispositivi Windows 10 basati su Internet per la co-gestione.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/05/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.collection: M365-identity-device-management
ms.openlocfilehash: a4dd872e803e1d2925f011a60be5d1ee924ca555
ms.sourcegitcommit: 8e9e7c42a5572797e05936fab0cf84fc27c40862
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2019
ms.locfileid: "67398858"
---
# <a name="how-to-prepare-internet-based-devices-for-co-management"></a>Come preparare i dispositivi basati su Internet per la co-gestione

Questo articolo è incentrato sul secondo percorso relativo alla co-gestione, per i nuovi dispositivi basati su Internet. Questo scenario si verifica quando nuovi dispositivi Windows 10 vengono aggiunti ad Azure AD e automaticamente registrati in Intune. Per raggiungere uno stato di co-gestione, è necessario installare il client di Configuration Manager.  



## <a name="windows-autopilot"></a>Windows Autopilot

Per i nuovi dispositivi Windows 10 è possibile usare il servizio Autopilot per definire la Configurazione guidata. Questo processo include l'aggiunta del dispositivo ad Azure AD e la registrazione del dispositivo in Intune.  

Per altre informazioni, vedere [Panoramica di Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot).    

Per configurare i dispositivi per la registrazione automatica in Intune quando vengono aggiunti ad Azure AD, vedere [Configurare la registrazione dei dispositivi Windows](https://docs.microsoft.com/intune/windows-enroll).  


### <a name="gather-information-from-configuration-manager"></a>Raccogliere informazioni da Configuration Manager

A partire dalla versione 1802, usare Configuration Manager per raccogliere e segnalare le informazioni sul dispositivo richieste da Microsoft Store per le aziende e per la formazione. Queste informazioni includono il numero di serie del dispositivo, l'identificatore del prodotto Windows e un ID hardware. Vengono usate per registrare il dispositivo in Microsoft Store per il supporto di Windows Autopilot. 

1. Nella console di Configuration Manager passare all'area di lavoro **Monitoraggio**, espandere il nodo **Report**, espandere **Report** e selezionare il nodo **Hardware - Generale**.  

2. Eseguire il report **Informazioni sui dispositivi di Windows Autopilot** e visualizzare i risultati.  

3. Nel visualizzatore report selezionare l'icona **Esporta** e scegliere l'opzione **CSV (delimitato da virgole)** .  

4. Dopo aver salvato il file, caricare i dati in Microsoft Store per le aziende e per la formazione.  

Per altre informazioni, vedere [Add devices in Microsoft Store for Business and Education](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile) (Aggiungere dispositivi in Microsoft Store per le aziende e gli istituti di istruzione).


### <a name="autopilot-for-existing-devices"></a>Autopilot per dispositivi esistenti
<!--1358333-->

[Windows Autopilot per i dispositivi esistenti](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) è disponibile in Windows 10 versione 1809 o successive. Questa funzionalità consente di ricreare l'immagine ed eseguire il provisioning di un dispositivo Windows 7 per la [modalità definita dall'utente di Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) usando una singola sequenza di attività nativa di Configuration Manager. 

Per altre informazioni, vedere la [sequenza di attività Windows Autopilot per dispositivi esistenti](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices).



## <a name="install-the-configuration-manager-client"></a>Installare il client di Configuration Manager

Per i dispositivi basati su Internet nel secondo percorso, è necessario creare un'app in Intune. Distribuire quest'app nei dispositivi Windows 10 che non sono ancora client di Configuration Manager. 

> [!Note]  
> Prima di distribuire questa app ai dispositivi, è necessario assicurarsi che i dispositivi considerino attendibile il certificato di autenticazione server di Cloud Management Gateway. Per altre informazioni, vedere [Certificato radice trusted del gateway di gestione cloud per i client](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_cmgroot). Se il dispositivo non considera attendibile il certificato di autenticazione server di Cloud Management Gateway verrà indicato l'errore WINHTTP_CALLBACK_STATUS_FLAG_INVALID_CA nel file ccmsetup.log nel client.

### <a name="get-the-command-line-from-configuration-manager"></a>Recuperare la riga di comando da Configuration Manager

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Co-gestione**.  

2. Selezionare l'oggetto co-gestione e quindi scegliere **Proprietà** nella barra multifunzione.  

3. Nella scheda **Abilitazione** copiare la riga di comando. Incollarla nel Blocco note e salvarla per il processo successivo.  

La riga di comando seguente è un esempio: `CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC"`

<!--1358215-->
A partire dalla versione 1806, sono necessarie meno proprietà della riga di comando.  

- Le seguenti proprietà della riga di comando sono richieste in tutti gli scenari:  
    - CCMHOSTNAME  
    - SMSSITECODE  

- Le seguenti proprietà sono richieste quando si usa Azure AD per l'autenticazione client anziché i certificati di autenticazione client basati su infrastruttura a chiave pubblica:  
    - AADCLIENTAPPID  
    - AADRESOURCEURI  

- Se il client effettua il roaming alla rete Intranet, la proprietà seguente è obbligatoria:  
    - SMSMP  

- Se si usa il proprio certificato SSL PKI e l'elenco di revoche di certificati non è pubblicato in Internet, il parametro seguente è obbligatorio:  
    - /noCRLCheck  
    
     Per altre informazioni, vedere [Planning for CRLs](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForCRLs) (Pianificazione degli elenchi di revoche di certificati)  

A partire dalla versione 1810, il sito pubblica le informazioni aggiuntive di Azure AD in Cloud Management Gateway (CMG). Un client aggiunto ad Azure AD ottiene queste informazioni da CMG durante il processo ccmsetup, usando lo stesso tenant a cui viene aggiunto. Questo comportamento semplifica ulteriormente la registrazione dei dispositivi per la co-gestione in un ambiente con più di un tenant di Azure AD. Al momento le uniche due proprietà obbligatorie di ccmsetup sono **CCMHOSTNAME** e **SMSSiteCode**.<!--3607731-->

> [!Note]
> Se si distribuisce già il client di Configuration Manager da Intune, aggiornare l'app di Intune con una nuova riga di comando e un nuovo file MSI. <!-- SCCMDocs-pr issue 3084 -->

L'esempio seguente include tutte queste proprietà:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Per altre informazioni, vedere [Informazioni sulle proprietà di installazione del client in System Center Configuration Manager](/sccm/core/clients/deploy/about-client-installation-properties).


### <a name="create-the-app-in-intune"></a>Creare l'app in Intune

1. Accedere al [portale di Azure](https://portal.azure.com) e quindi aprire la pagina di Intune.  

2. Selezionare **App client** > **App** > **Aggiungi**.  

3. In **Altro** selezionare **App line-of-business**.  

4. Caricare il file del pacchetto dell'app **ccmsetup.msi**. Questo file è disponibile nella cartella seguente nel server del sito di Configuration Manager: `<ConfigMgr installation directory>\bin\i386`.  

    > [!Tip]  
    > Quando si aggiorna il sito, assicurarsi di aggiornare anche l'app in Intune.  

5. Dopo aver aggiornato l'app, configurare le informazioni sull'app con la riga di comando copiata da Configuration Manager.  

> [!IMPORTANT]    
> Se si personalizza questa riga di comando, assicurarsi che la lunghezza non superi i 1024 caratteri. Se la lunghezza della riga di comando supera i 1024 caratteri, l'installazione del client non va a buon fine.



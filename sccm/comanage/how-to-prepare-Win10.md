---
title: CO-gestione dei dispositivi basato su internet
titleSuffix: Configuration Manager
description: Informazioni su come preparare i dispositivi Windows 10 basato su internet per la co-gestione.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/05/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 101de2ba-9b4d-4890-b087-5d518a4aa624
ms.collection: M365-identity-device-management
ms.openlocfilehash: 31779b3588617816df4309461ed7715b20b0abd4
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558032"
---
# <a name="how-to-prepare-internet-based-devices-for-co-management"></a>Come preparare i dispositivi basati su internet per la co-gestione

Questo articolo è incentrato sul secondo percorso da CO-gestione, per i nuovi dispositivi basati su internet. Questo scenario è quando si dispongono di nuovi dispositivi Windows 10 aggiunti ad Azure AD e registrati automaticamente in Intune. Si installa il client di Configuration Manager per raggiungere uno stato di CO-gestione.  



## <a name="windows-autopilot"></a>Windows Autopilot

Per i nuovi dispositivi Windows 10, è possibile usare il servizio Autopilot per la configurazione dell'esperienza di finestra (OOBE). Questo processo include l'aggiunta del dispositivo ad Azure AD e la registrazione del dispositivo in Intune.  

Per altre informazioni, vedere [Panoramica di Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot).    

Per configurare i dispositivi da registrare automaticamente in Intune quando accedono ad Azure AD, vedere [i dispositivi Windows registrati di Microsoft Intune](https://docs.microsoft.com/intune/windows-enroll).  


### <a name="gather-information-from-configuration-manager"></a>Raccogliere informazioni da Configuration Manager

A partire dalla versione 1802, usare Configuration Manager per raccogliere e segnalare le informazioni sul dispositivo richieste da Microsoft Store per le aziende e per la formazione. Queste informazioni includono il numero di serie del dispositivo, l'identificatore del prodotto Windows e un ID hardware. Viene utilizzato per registrare il dispositivo in di Microsoft Store per il supporto di Windows Autopilot. 

1. Nella console di Configuration Manager passare ad il **Monitoring** dell'area di lavoro, espandere il **Reporting** nodo, espandere **report**e selezionare il **Hardware - Generale** nodo.  

2. Esecuzione del report **informazioni sui dispositivi di Windows Autopilot**e visualizzare i risultati.  

3. Nel Visualizzatore di report, selezionare la **esportare** icona, scegliere il **CSV (comma-separated value)** opzione.  

4. Dopo aver salvato il file, caricare i dati in Microsoft Store per le aziende e per la formazione.  

Per altre informazioni, vedere [aggiungere i dispositivi in Microsoft Store per Business ed Education](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile).


### <a name="autopilot-for-existing-devices"></a>AutoPilot per i dispositivi esistenti
<!--1358333-->

[Windows Autopilot per i dispositivi esistenti](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/New-Windows-Autopilot-capabilities-and-expanded-partner-support/ba-p/260430) è disponibile in Windows 10, versione 1809 o versione successiva. Questa funzionalità consente di ricreare l'immagine ed eseguire il provisioning di un dispositivo Windows 7 per [modalità gestita dall'utente di Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/user-driven) utilizzando una sequenza di attività singola, native di Configuration Manager. 

Per altre informazioni, vedere [Autopilot di Windows per la sequenza di attività esistente dispositivi](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices).



## <a name="install-the-configuration-manager-client"></a>Installare il client di Configuration Manager

Per i dispositivi basati su internet nel secondo percorso, è necessario creare un'app in Intune. Distribuire l'app per dispositivi Windows 10 che non sono già client di Configuration Manager. 

### <a name="get-the-command-line-from-configuration-manager"></a>Ottenere la riga di comando da Configuration Manager

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Servizi cloud** e selezionare il nodo **Co-gestione**.  

2. Selezionare l'oggetto di CO-gestione e quindi scegliere **proprietà** nella barra multifunzione.  

3. Nel **abilitazione** scheda, copiare la riga di comando. Incollarlo nel blocco note salvare per il processo successivo.  

Riga di comando seguente è riportato un esempio: `CCMSETUPCMD="CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC"`

<!--1358215--> A partire dalla versione 1806, sono necessarie meno proprietà della riga di comando.  

- Le seguenti proprietà della riga di comando sono richieste in tutti gli scenari:  
    - CCMHOSTNAME  
    - SMSSITECODE  

- Le seguenti proprietà sono richieste quando si usa Azure AD per l'autenticazione client anziché i certificati di autenticazione client basati su infrastruttura a chiave pubblica:  
    - AADCLIENTAPPID  
    - AADRESOURCEURI  

- Se il client ritorna a intranet, sarà necessaria la proprietà seguente:  
    - SMSMP  

- Se tramite il proprio certificato SSL di PKI e i CRL non è pubblicato su internet, è necessario il parametro seguente:  
    - /noCRLCheck  
    
     Per altre informazioni, vedere [Planning for CRL](/sccm/core/plan-design/security/plan-for-security#-plan-for-the-site-server-signing-certificate-self-signed)  

A partire dalla versione 1810, il sito pubblica aggiuntivi di Azure le informazioni di Active Directory a cloud management gateway (CMG). Un client aggiunto ad Azure AD ottiene queste informazioni da CMG durante il processo ccmsetup, usando lo stesso tenant a cui viene aggiunto. Questo comportamento semplifica ulteriormente la registrazione dei dispositivi per la co-gestione in un ambiente con più di un tenant di Azure AD. A questo punto sono le proprietà ccmsetup necessari solo due **CCMHOSTNAME** e **SMSSiteCode**.<!--3607731-->

> [!Note]
> Se già si distribuisce il client di Configuration Manager da Intune, è possibile aggiornare l'app di Intune con una nuova riga di comando e un nuovo file MSI. <!-- SCCMDocs-pr issue 3084 -->

L'esempio seguente include tutte queste proprietà:   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Per altre informazioni, vedere [Informazioni sulle proprietà di installazione del client in System Center Configuration Manager](/sccm/core/clients/deploy/about-client-installation-properties).


### <a name="create-the-app-in-intune"></a>Creare l'app in Intune

1. Andare alla [portale di Azure](https://portal.azure.com)e quindi aprire la pagina di Intune.  

2. Selezionare **App Client** > **app** > **aggiungere**.  

3. In **Altro** selezionare **App line-of-business**.  

4. Caricare il **CCMSetup. msi** file pacchetto dell'app. Trovare il file nella cartella seguente in Configuration Manager server del sito: `<ConfigMgr installation directory>\bin\i386`.  

    > [!Tip]  
    > Quando si aggiorna il sito, assicurarsi di che aggiornare anche l'app in Intune.  

5. Dopo che l'app viene aggiornata, configurare le informazioni sull'app con la riga di comando che è stato copiato da Configuration Manager.  

> [!IMPORTANT]    
> Se si personalizza la riga di comando, assicurarsi che non è lungo più di 1024 caratteri. Quando la lunghezza della riga di comando è maggiore di 1024 caratteri, l'installazione del client ha esito negativo.



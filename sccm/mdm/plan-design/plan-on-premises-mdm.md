---
title: Pianificare MDM locale
titleSuffix: Configuration Manager
description: Pianificare la gestione dei dispositivi mobili locale per gestire i dispositivi mobili in Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 165d3b5dfb2911ad7ecc3516ebd1dd36a995818f
ms.sourcegitcommit: 7f64c5fb3e9fa3dba006af618b1f1ceaf61a99f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/28/2019
ms.locfileid: "75519437"
---
# <a name="plan-for-on-premises-mdm-in-configuration-manager"></a>Pianificare la gestione dei dispositivi mobili locale in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Gestione di dispositivi mobili (MDM) locale consente di gestire i dispositivi mobili usando le funzionalità di gestione integrate nel sistema operativo del dispositivo. La funzionalità di gestione si basa sullo standard Open Mobile Alliance (OMA) Device Management (DM), usato da molte piattaforme per dispositivi per consentire la gestione dei dispositivi. Questi dispositivi sono detti *dispositivi moderni* nella documentazione e nella console di Configuration Manager. Questo termine li distingue da altri dispositivi che richiedono la gestione Configuration Manager client.  

Considerare i requisiti seguenti prima di preparare l'infrastruttura di Configuration Manager per la gestione di MDM locale.



## <a name="bkmk_devices"></a> Dispositivi supportati  

Il Current Branch di Configuration Manager supporta la registrazione nella gestione dispositivi mobili locale per i dispositivi che eseguono i sistemi operativi seguenti:  
  
- Windows 10 Enterprise  
- Windows 10 Pro  
- Windows 10 Team   
- Windows 10 Mobile  
- Windows 10 Mobile Enterprise
- Windows 10 IoT Enterprise   



##  <a name="bkmk_intune"></a>Sottoscrizione di Microsoft Intune  

Per iniziare a usare MDM locale, è necessario un Microsoft Intune sottoscrizione. La sottoscrizione è necessaria solo per tenere traccia delle licenze dei dispositivi e non viene usata per gestire o archiviare le informazioni di gestione per i dispositivi. Tutti i dati di gestione vengono archiviati nell'organizzazione tramite l'infrastruttura di Configuration Manager locale.  

> [!Note]  
> A partire dalla versione 1810, una connessione a Intune non è più necessaria per le nuove distribuzioni MDM locali.<!--3607730, fka 1359124--> Per usare questa funzionalità è comunque necessario che l'organizzazione abbia le licenze di Intune. Attualmente non è possibile rimuovere la connessione a Intune dalle distribuzioni MDM locali esistenti. Per altre informazioni, vedere il [post di blog del supporto tecnico di Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

Se il sito dispone di dispositivi con connettività Internet, è possibile usare il servizio Intune per notificare ai dispositivi di controllare il punto di gestione dei dispositivi per gli aggiornamenti dei criteri. Questo comportamento USA Intune esclusivamente per la notifica di dispositivi con connessione Internet. I dispositivi senza connessioni Internet e che non possono essere contattati da Intune si basano sull'intervallo di polling configurato per archiviare i ruoli del sistema del sito per le funzioni di gestione.  

> [!TIP]  
> Prima di configurare i ruoli del sistema del sito richiesti, configurare la sottoscrizione di Intune. Questa azione riduce al minimo il tempo necessario affinché i ruoli diventino funzionali.  

Per informazioni su come configurare la sottoscrizione di Intune, vedere [configurare una sottoscrizione di Microsoft Intune per MDM locale](/sccm/mdm/get-started/set-up-intune-subscription-on-premises-mdm).  



##  <a name="bkmk_roles"></a> Site system roles  

MDM locale richiede almeno uno dei seguenti ruoli del sistema del sito:  

- **Punto proxy di registrazione** per supportare le richieste di registrazione.  

- **Punto di registrazione** per supportare la registrazione dei dispositivi.  

- **Punto gestione periferiche** per la distribuzione dei criteri. Questo ruolo del sistema del sito è una variante del ruolo del punto di gestione che è stato configurato per consentire la gestione dei dispositivi mobili.  

- **Punto di distribuzione** per la distribuzione di contenuti.  

- **Punto di connessione del servizio** per la connessione a Intune per le notifiche a dispositivi esterni al firewall.  

Questi ruoli del sistema del sito possono essere installati nel singolo server del sistema del sito oppure possono essere eseguiti separatamente in server diversi a seconda delle esigenze dell'organizzazione. Ogni server del sistema del sito usato per MDM locale deve essere configurato come endpoint HTTPS per la comunicazione con i dispositivi attendibili. Per altre informazioni, vedere [Comunicazioni attendibili richieste](#bkmk_trustedComs).  

Per ulteriori informazioni sulla pianificazione dei ruoli del sistema del sito, vedere [pianificare i ruoli e i server del sistema del sito per Configuration Manager](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles).  

Per ulteriori informazioni su come aggiungere i ruoli del sistema del sito richiesti, vedere [installare i ruoli del sistema del sito per MDM locale](/sccm/mdm/get-started/install-site-system-roles-for-on-premises-mdm).  



##  <a name="bkmk_trustedComs"></a>Comunicazioni attendibili  

MDM locale richiede che i ruoli del sistema del sito siano abilitati per le comunicazioni HTTPS. A seconda delle esigenze, è possibile usare l'autorità di certificazione dell'organizzazione (CA) per stabilire le connessioni attendibili tra i server e i dispositivi. È anche possibile usare una CA disponibile pubblicamente come autorità attendibile. In entrambi i casi, è necessario che un certificato server Web sia configurato in IIS nei server del sistema del sito che ospitano i ruoli del sistema del sito richiesti. È necessario anche il certificato radice della CA installato nei dispositivi che devono connettersi a tali server.  

Se si usa la CA dell'organizzazione per stabilire comunicazioni attendibili, eseguire le attività seguenti:  

- Creare ed emettere il modello di certificato del server Web nella CA.  

- Richiedere un certificato del server web per ogni server del sistema del sito che ospita un ruolo del sistema del sito richiesto.  

- Configurare IIS nel server del sistema del sito per usare il certificato del server Web richiesto.  

Per i dispositivi aggiunti al dominio Active Directory aziendale, il certificato radice della CA aziendale è già disponibile nel dispositivo per le connessioni attendibili. Questo comportamento indica che i dispositivi aggiunti a un dominio vengono automaticamente considerati attendibili per le connessioni HTTPS con i server del sistema del sito. Tuttavia, i dispositivi non aggiunti a un dominio non ottengono automaticamente il certificato radice richiesto installato. Per comunicare correttamente con i server del sistema del sito che supportano MDM locale, i dispositivi non aggiunti a un dominio, ad esempio i dispositivi mobili, richiedono l'installazione manuale del certificato radice su di essi.  

Esportare il certificato radice della CA emittente per l'uso da parte dei singoli dispositivi. Per ottenere il file del certificato radice, è possibile esportarlo usando la CA. Un altro metodo consiste nell'usare il certificato del server Web emesso dalla CA per estrarre la radice e creare un file del certificato radice. Il certificato radice deve quindi essere recapitato al dispositivo. Alcuni metodi di recapito di esempio includono:

- File system  

- Allegato e-mail  

- Scheda di memoria  

- Dispositivo con tethering  

- Archiviazione cloud (ad esempio OneDrive)  

- Connessione NFC (Near Field Communication)  

- Lettore di codice a barre  

- Pacchetto di provisioning della Configurazione guidata  

Per altre informazioni, vedere [configurare i certificati per le comunicazioni attendibili in MDM locale](/sccm/mdm/get-started/set-up-certificates-on-premises-mdm)  



##  <a name="bkmk_enrollment"></a>Registrazione del dispositivo

Per abilitare la registrazione del dispositivo per MDM locale,
- Agli utenti deve essere concessa l'autorizzazione per la registrazione 
- I dispositivi devono essere configurati per le comunicazioni trusted con i server del sistema del sito che ospitano i ruoli necessari  

Concedere agli utenti le autorizzazioni per registrare i dispositivi impostando un profilo di registrazione in Configuration Manager impostazioni client. È possibile usare le impostazioni client predefinite per eseguire il push del profilo di registrazione a tutti gli utenti individuati. È anche possibile configurare il profilo di registrazione nelle impostazioni client personalizzate e inviare le impostazioni a una o più raccolte di utenti.  

Una volta concessa l'autorizzazione, gli utenti possono registrare i propri dispositivi. Per essere registrato, il dispositivo dell'utente deve avere il certificato radice dell'autorità di certificazione (CA) che ha emesso il certificato del server Web usato nei server del sistema del sito che ospitano i ruoli necessari.  

In alternativa alla registrazione avviata dall'utente, è possibile configurare un pacchetto di registrazione in blocco. Questo pacchetto consente la registrazione del dispositivo senza l'intervento dell'utente. Può essere recapitato al dispositivo prima del provisioning per l'uso o dopo il completamento del processo OOBE da parte del dispositivo.  

Per ulteriori informazioni su come configurare e registrare i dispositivi, vedere gli articoli seguenti: 

- [Configurare la registrazione dei dispositivi per MDM locale](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm)  

- [Registrare i dispositivi per la gestione dei dispositivi mobili locale](/sccm/mdm/deploy-use/enroll-devices-on-premises-mdm)  


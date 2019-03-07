---
title: Pianificare la MDM locale
titleSuffix: Configuration Manager
description: Pianificare la gestione dei dispositivi mobili in locale gestire i dispositivi mobili in Configuration Manager
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: bb9349a8c3f107f2da139148e4476537fe6aa7ed
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558083"
---
# <a name="plan-for-on-premises-mdm-in-configuration-manager"></a>Piano per on-premises MDM in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Gestione dei dispositivi mobili in locale (MDM) consente di gestire i dispositivi mobili usando la funzionalità di gestione del sistema operativo del dispositivo. La funzionalità di gestione si basa sullo standard Open Mobile Alliance (OMA) Device Management (DM), usato da molte piattaforme per dispositivi per consentire la gestione dei dispositivi. Questi dispositivi vengono chiamati *dispositivi moderni* nella documentazione e la console di Configuration Manager. Questo termine li distingue dagli altri dispositivi che richiedono il client di Configuration Manager per gestirli.  

Prendere in considerazione i requisiti seguenti prima di preparare l'infrastruttura di Configuration Manager per la gestione software MDM locale.



## <a name="bkmk_devices"></a> Dispositivi supportati  

Il ramo corrente di Configuration Manager supporta la registrazione in Gestione dispositivi mobili locali per i dispositivi che eseguono i sistemi operativi seguenti:  
  
- Windows 10 Enterprise  
- Windows 10 Pro  
- Windows 10 Team   
- Windows 10 Mobile  
- Windows 10 Mobile Enterprise
- Windows 10 IoT Enterprise   



##  <a name="bkmk_intune"></a> La sottoscrizione di Microsoft Intune  

Per iniziare a usare MDM locale, è necessaria una sottoscrizione di Microsoft Intune. La sottoscrizione è richiesto solo per tenere traccia delle licenze dei dispositivi e non viene usata per gestire o archiviare le informazioni di gestione per i dispositivi. Tutti i dati di gestione vengono archiviati all'interno dell'organizzazione usando l'infrastruttura di Configuration Manager in locale.  

> [!Note]  
> A partire dalla versione 1810, una connessione di Intune non è più necessaria per le nuove distribuzioni MDM locale.<!--3607730, fka 1359124--> Per usare questa funzionalità è comunque necessario che l'organizzazione abbia le licenze di Intune. Attualmente, è possibile rimuovere la connessione di Intune da distribuzione MDM locale esistente. Per altre informazioni, vedere il [post di blog del supporto tecnico di Intune](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Move-from-Hybrid-Mobile-Device-Management-to-Intune-on-Azure/ba-p/280150).  

Se il sito ha dispositivi con connessione internet, il servizio Intune è utilizzabile per notificare ai dispositivi di controllare il punto di gestione dei dispositivi per gli aggiornamenti dei criteri. Questo comportamento usa esclusivamente Intune notifiche per i dispositivi con connessione internet. I dispositivi senza connessioni internet e che non possono essere contattati da Intune si basano su intervallo di polling configurato per l'archiviazione con i ruoli del sistema del sito per le funzioni di gestione.  

> [!TIP]  
> Prima di configurare i ruoli del sistema del sito necessari, impostare la sottoscrizione di Intune. Questa azione consente di ridurre il tempo necessario per i ruoli diventare funzionale.  

Per informazioni su come configurare la sottoscrizione di Intune, vedere [configurare una sottoscrizione di Microsoft Intune per MDM locale](/sccm/mdm/get-started/set-up-intune-subscription-on-premises-mdm).  



##  <a name="bkmk_roles"></a> Site system roles  

On-premise MDM richiede almeno uno di ciascuno dei seguenti ruoli del sistema del sito:  

- **Punto proxy di registrazione** per supportare le richieste di registrazione.  

- **Punto di registrazione** per supportare la registrazione dei dispositivi.  

- **Punto gestione periferiche** per la distribuzione dei criteri. Questo ruolo del sistema del sito è una variante del ruolo del punto di gestione che è stato configurato per consentire la gestione dei dispositivi mobili.  

- **Punto di distribuzione** per la distribuzione di contenuti.  

- **Punto di connessione del servizio** per la connessione a Intune per le notifiche a dispositivi esterni al firewall.  

Questi ruoli del sistema del sito possono essere installati nel server del sistema del sito singolo o possono essere eseguiti separatamente in server diversi a seconda delle esigenze dell'organizzazione. Ogni server del sistema del sito usato per MDM locale deve essere configurato come un endpoint HTTPS per comunicare con dispositivi attendibili. Per altre informazioni, vedere [Comunicazioni attendibili richieste](#bkmk_trustedComs).  

Per altre informazioni sulla pianificazione dei ruoli del sistema del sito, vedere [pianificare ruoli e i server del sistema del sito per Configuration Manager](/sccm/core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles).  

Per altre informazioni su come aggiungere i ruoli del sistema del sito necessari, vedere [installare ruoli del sistema del sito per MDM locale](/sccm/mdm/get-started/install-site-system-roles-for-on-premises-mdm).  



##  <a name="bkmk_trustedComs"></a> Comunicazioni attendibili  

MDM locale richiede ruoli del sistema del sito siano abilitati per le comunicazioni HTTPS. A seconda delle esigenze, è possibile utilizzare autorità di certificazione dell'organizzazione (CA) per stabilire connessioni attendibili tra server e dispositivi. È anche possibile usare un'autorità di certificazione disponibile pubblicamente sia l'autorità attendibile. In entrambi i casi, è necessario un certificato server web devono essere configurate in IIS sul server del sistema del sito che ospita i ruoli del sistema del sito necessari. È inoltre necessario il certificato radice della CA installato nei dispositivi che è necessario per connettersi a tali server.  

Se si usa la CA dell'azienda per stabilire comunicazioni attendibili, eseguire le attività seguenti:  

- Creare ed emettere il modello di certificato del server Web nella CA.  

- Richiedere un certificato del server web per ogni server del sistema del sito che ospita un ruolo del sistema del sito richiesto.  

- Configurare IIS nel server del sistema del sito per usare il certificato del server Web richiesto.  

Per i dispositivi aggiunti al dominio Active Directory aziendale, il certificato radice della CA aziendale è già disponibile nel dispositivo per le connessioni attendibili. Questo comportamento significa che i dispositivi aggiunti a un dominio siano automaticamente attendibili per le connessioni HTTPS con i server del sistema del sito. Tuttavia, i dispositivi non appartenenti a un dominio non ottengono automaticamente il certificato radice necessario. Per comunicare correttamente con i server di sistema del sito che supportano MDM locale, i dispositivi non appartenenti a un dominio, ad esempio i dispositivi mobili è necessario installare manualmente il certificato radice su di essi.  

Esportare il certificato radice della CA emittente per l'uso da parte di singoli dispositivi. Per ottenere il file del certificato radice, è possibile esportarlo usando l'autorità di certificazione. Un altro metodo consiste nell'usare il certificato del server web rilasciato dalla CA per estrarre la radice e creare un file di certificato radice. Il certificato radice deve essere quindi distribuito nel dispositivo. Alcuni metodi di recapito semplici includono:

- File system  

- Allegato e-mail  

- Scheda di memoria  

- Dispositivo con tethering  

- Archiviazione cloud (ad esempio OneDrive)  

- Connessione NFC (Near Field Communication)  

- Lettore di codice a barre  

- Pacchetto di provisioning della Configurazione guidata  

Per altre informazioni, vedere [configurare certificati per le comunicazioni attendibili in MDM locale](/sccm/mdm/get-started/set-up-certificates-on-premises-mdm)  



##  <a name="bkmk_enrollment"></a> Registrazione del dispositivo

Per abilitare la registrazione di dispositivi per MDM locale,
- Gli utenti devono disporre dell'autorizzazione per registrare 
- Dispositivi devono essere configurati per le comunicazioni attendibili con i server del sistema del sito che ospita i ruoli richiesti  

Concedere agli utenti l'autorizzazione per registrare i dispositivi tramite l'impostazione di un profilo di registrazione nelle impostazioni client di Configuration Manager. È possibile usare le impostazioni client predefinite per inviare il profilo di registrazione per tutti gli utenti individuati. È anche possibile configurare il profilo di registrazione nelle impostazioni client personalizzate e inviare le impostazioni a una o più raccolte utente.  

Dopo che gli utenti sono autorizzati, è possibile registrare i propri dispositivi. Per essere registrato, il dispositivo dell'utente deve avere il certificato radice dell'autorità di certificazione (CA) che ha emesso il certificato del server web utilizzato nel server del sistema del sito che ospita i ruoli richiesti.  

Come alternativa alla registrazione avviata dall'utente, è possibile configurare un pacchetto di registrazione in blocco. Questo pacchetto consente al dispositivo di essere registrati senza intervento dell'utente. Si può essere recapitato al dispositivo prima che ne viene eseguito il provisioning per l'uso o dopo che il dispositivo passa attraverso il processo di configurazione guidata.  

Per altre informazioni su come configurare e registrare i dispositivi, vedere gli articoli seguenti: 

- [Impostare la registrazione dei dispositivi per MDM locale](/sccm/mdm/get-started/set-up-device-enrollment-on-premises-mdm)  

- [Registrare i dispositivi per la gestione dei dispositivi mobili locale](/sccm/mdm/deploy-use/enroll-devices-on-premises-mdm)  


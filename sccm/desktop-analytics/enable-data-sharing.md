---
title: Abilitare la condivisione dei dati
titleSuffix: Configuration Manager
description: Guida di riferimento per la condivisione di dati di diagnostica con analisi desktop.
ms.date: 10/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 91be1fbb03c49b28d689aff974a43ba8434fc194
ms.sourcegitcommit: b64ed4a10a90b93a5bd5454b6efafda90ad45718
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/16/2019
ms.locfileid: "72385679"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>Abilitare la condivisione dei dati per analisi desktop

Per registrare i dispositivi in desktop Analytics, è necessario inviare i dati di diagnostica a Microsoft. Se l'ambiente in uso usa un server proxy, usare queste informazioni per configurare il proxy.


## <a name="diagnostic-data-levels"></a>Livelli di dati di diagnostica

![Diagramma dei livelli di dati di diagnostica per analisi desktop](media/diagnostic-data-levels.png)

Quando si integra Configuration Manager con analisi desktop, viene usato anche per gestire il livello di dati di diagnostica nei dispositivi. Per un'esperienza ottimale, usare Configuration Manager.

La funzionalità di base di desktop Analytics funziona a livello di dati di diagnostica di **base** . Non è possibile ottenere dati di utilizzo o di integrità per i dispositivi aggiornati senza abilitare il livello **avanzato (limitato)** . Microsoft consiglia di abilitare il livello dati di diagnostica **avanzato (limitato)** . Per ulteriori informazioni, vedere [gli eventi e i campi dei dati di diagnostica avanzati di Windows 10 usati da Windows Analytics](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields).

> [!Important]   
> Microsoft è impegnata a fornire gli strumenti e le risorse che consentono di controllare la privacy. Di conseguenza, Microsoft non raccoglie i dati seguenti dai dispositivi che si trovano in paesi europei (See e Switzerland):
>
> - Dati di diagnostica di Windows da dispositivi Windows 8.1
> - Dati di utilizzo delle app per Windows 7

Per ulteriori informazioni, vedere la pagina relativa alla [privacy di analisi desktop](/sccm/desktop-analytics/privacy).

Gli articoli seguenti sono anche risorse valide per comprendere meglio i livelli di dati di diagnostica di Windows:

- [Windows 10 e GDPR per i responsabili decisionali IT](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Configurare i dati di diagnostica di Windows nell'organizzazione](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!Note]  
> Al livello avanzato (limitato), quando ogni client esegue l'analisi completa iniziale, invia approssimativamente 2 MB di dati al cloud Microsoft. Il Delta giornaliero varia da 250-400 KB al giorno.
>
> L'analisi Delta giornaliera viene eseguita alle 3:00 AM (ora locale del dispositivo). Alcuni eventi vengono inviati alla prima ora disponibile nel corso della giornata. Questi orari non sono configurabili.
>
> Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](https://aka.ms/enterprisetelemetry) (Configurare i dati di diagnostica di Windows nell'organizzazione).  



## <a name="endpoints"></a>Endpoint

Per abilitare la condivisione dei dati, configurare il server proxy per consentire gli endpoint seguenti:

> [!Important]  
> Per la privacy e l'integrità dei dati, Windows verifica la presenza di un certificato SSL Microsoft durante la comunicazione con gli endpoint dati di diagnostica. L'intercettazione e l'ispezione SSL non sono possibili. Per usare analisi desktop, escludere questi endpoint dall'ispezione SSL.<!-- BUG 4647542 -->

| Endpoint  | Funzione  |
|-----------|-----------|
| `https://aka.ms` | Usato per individuare il servizio |
| `https://v10c.events.data.microsoft.com` | Esperienza utente connessa ed endpoint componente di diagnostica. Usato dai dispositivi che eseguono Windows 10, versione 1703 o successiva, con aggiornamento cumulativo 2018-09 o versione successiva installata. |
| `https://v10.events.data.microsoft.com` | Esperienza utente connessa ed endpoint componente di diagnostica. Usato dai dispositivi che eseguono Windows 10, versione 1803 o successive, _senza_ l'aggiornamento cumulativo 2018-09 installato. |
| `https://v10.vortex-win.data.microsoft.com` | Esperienza utente connessa ed endpoint componente di diagnostica. Usato dai dispositivi che eseguono Windows 10, versione 1709 o versioni precedenti. |
| `https://vortex-win.data.microsoft.com` | Esperienza utente connessa ed endpoint componente di diagnostica. Usato dai dispositivi che eseguono Windows 7 e Windows 8.1 |
| `https://settings-win.data.microsoft.com` | Consente all'aggiornamento per la compatibilità di inviare i dati a Microsoft. |
| `http://adl.windows.com` | Consente all'aggiornamento della compatibilità di ricevere i dati di compatibilità più recenti da Microsoft. |
| `https://watson.telemetry.microsoft.com` | Segnalazione errori Windows (WER). Necessaria per monitorare lo stato di distribuzione in Windows 10, versione 1803 o versioni precedenti. |
| `https://umwatsonc.events.data.microsoft.com` | Segnalazione errori Windows (WER). Obbligatorio per i report sull'integrità dei dispositivi in Windows 10, versione 1809 o successiva. |
| `https://ceuswatcab01.blob.core.windows.net`<br> `https://ceuswatcab02.blob.core.windows.net`<br> `https://eaus2watcab01.blob.core.windows.net`<br> `https://eaus2watcab02.blob.core.windows.net`<br> `https://weus2watcab01.blob.core.windows.net`<br> `https://weus2watcab02.blob.core.windows.net` | Segnalazione errori Windows (WER). Necessaria per monitorare lo stato di distribuzione in Windows 10, versione 1809 o successiva. |
| `https://kmwatsonc.events.data.microsoft.com` | Analisi degli arresti anomali in linea. Obbligatorio per i report sull'integrità dei dispositivi in Windows 10, versione 1809 o successiva. |
| `https://oca.telemetry.microsoft.com`  | Analisi degli arresti anomali (OCA) online. Necessaria per monitorare lo stato di distribuzione in Windows 10, versione 1803 o versioni precedenti. |
| `https://login.live.com` | Necessario per fornire un'identità del dispositivo più affidabile per desktop Analytics. <br> <br>Per disabilitare l'accesso account Microsoft all'utente finale, utilizzare le impostazioni dei criteri anziché bloccare l'endpoint. Per ulteriori informazioni, vedere [la account Microsoft nell'azienda](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication). |
| `https://graph.windows.net` | Usato per recuperare automaticamente le impostazioni, come la commercializzazione, quando si connette la gerarchia a desktop Analytics (in Configuration Manager ruolo del server). Per ulteriori informazioni, vedere [configurare il proxy per un server del sistema del sito
] (/SCCM/Core/Plan-Design/Network/Proxy-Server-Support # Configure-the-proxy-for-a-Site-System-Server). |
| `https://*.manage.microsoft.com` | Usato per sincronizzare l'appartenenza alla raccolta di dispositivi, i piani di distribuzione e lo stato di conformità dei dispositivi con analisi del desktop (solo su Configuration Manager ruolo del server). Per ulteriori informazioni, vedere [configurare il proxy per un server del sistema del sito
] (/SCCM/Core/Plan-Design/Network/Proxy-Server-Support # Configure-the-proxy-for-a-Site-System-Server). |


## <a name="proxy-server-authentication"></a>Autenticazione del server proxy

Assicurarsi che un proxy non blocchi i dati di diagnostica a causa dell'autenticazione. Se l'organizzazione usa l'autenticazione del server proxy per il traffico in uscita, usare uno o più degli approcci seguenti:

- **Bypass** (scelta consigliata): configurare i server proxy in modo che non richiedano l'autenticazione proxy per il traffico verso gli endpoint dati di diagnostica. Questa opzione è la soluzione più completa. Funziona per tutte le versioni di Windows 10.  

- **Autenticazione proxy utente**: configurare i dispositivi per l'uso del contesto dell'utente connesso per l'autenticazione proxy. Questo metodo richiede che i dispositivi eseguano Windows 10, versione 1703 o successiva. Verificare che gli utenti dispongano dell'autorizzazione proxy per raggiungere gli endpoint dei dati di diagnostica. Questa opzione richiede che i dispositivi dispongano di utenti console con autorizzazioni proxy, quindi non è possibile usare questo metodo con dispositivi senza intestazioni.  

- **Autenticazione del proxy del dispositivo**:

    - Configurare un server proxy a livello di sistema nei dispositivi.  
    - Configurare questi dispositivi per l'uso dell'autenticazione proxy in uscita basata sul dispositivo.  
    - Configurare i server proxy per consentire agli account del computer di accedere agli endpoint dei dati di diagnostica.  

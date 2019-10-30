---
title: Abilitare la condivisione dei dati
titleSuffix: Configuration Manager
description: Guida di riferimento per la condivisione di dati di diagnostica con analisi desktop.
ms.date: 10/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8bc8a8c36e3b778f23241d16c1f31f821ab8b900
ms.sourcegitcommit: 07756e9b4ed7b134e32349acb1eeae93c6de9e28
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/29/2019
ms.locfileid: "73049384"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>Abilitare la condivisione dei dati per analisi desktop

Per registrare i dispositivi in desktop Analytics, è necessario inviare i dati di diagnostica a Microsoft. Se l'ambiente in uso usa un server proxy, usare queste informazioni per configurare il proxy.


## <a name="diagnostic-data-levels"></a>Livelli di dati di diagnostica

![Diagramma dei livelli di dati di diagnostica per analisi desktop](media/diagnostic-data-levels.png)

Quando si integra Configuration Manager con analisi desktop, viene usato anche per gestire il livello di dati di diagnostica nei dispositivi. Per un'esperienza ottimale, usare Configuration Manager.

La funzionalità di base di desktop Analytics funziona a [livello di dati di diagnostica](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels)di base. Se non si configura il livello **avanzato (limitato)** in Configuration Manager, non si ottengono le funzionalità seguenti di analisi del desktop:

- Utilizzo app
- [App Insights aggiuntive](https://docs.microsoft.com/sccm/desktop-analytics/compat-assessment#additional-insights)
- Dati sullo stato della distribuzione
- Dati di monitoraggio dello stato

Microsoft consiglia di abilitare il livello di dati di diagnostica **avanzato (limitato)** con analisi desktop per ottimizzare i vantaggi offerti. 

> [!Tip]
> L'impostazione **avanzata (limitata)** in Configuration Manager è la stessa che consente di **limitare i dati di diagnostica avanzati al minimo richiesto dai criteri di Windows Analytics** disponibili nei dispositivi che eseguono Windows 10, versione 1709 e successive. 
>
> I dispositivi che eseguono Windows 10, versione 1703 e versioni precedenti, Windows 8.1 o Windows 7 non hanno questa impostazione di criteri. Quando si configura l'impostazione **avanzata (limitata)** in Configuration Manager, questi dispositivi eseguono il fallback al livello di **base** .
>
> I dispositivi che eseguono Windows 10, versione 1709 hanno questa impostazione dei criteri. Tuttavia, quando si configura l'impostazione **avanzata (limitata)** in Configuration Manager, anche questi dispositivi eseguono il fallback al livello di **base** .

Per ulteriori informazioni sui dati di diagnostica condivisi con Microsoft con **Enhanced (Limited)** , vedere [gli eventi e i campi dei dati di diagnostica avanzati di Windows 10](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields).

> [!Important]   
> Microsoft è impegnata a fornire gli strumenti e le risorse che consentono di controllare la privacy. Di conseguenza, mentre desktop Analytics supporta Windows 8.1 dispositivi, Microsoft non raccoglie i dati di diagnostica di Windows da Windows 8.1 dispositivi situati in paesi europei (See e Svizzera).

Per ulteriori informazioni, vedere la pagina relativa alla [privacy di analisi desktop](/sccm/desktop-analytics/privacy).

Gli articoli seguenti sono anche risorse valide per comprendere meglio i livelli di dati di diagnostica di Windows:

- [Windows 10 e GDPR per i responsabili decisionali IT](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Configurare i dati di diagnostica di Windows nell'organizzazione](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!Note]  
> I client configurati per limitare i dati di diagnostica avanzati invieranno circa 2 MB di dati al cloud Microsoft nell'analisi completa iniziale. Il Delta giornaliero varia da 250-400 KB al giorno.
>
> L'analisi Delta giornaliera viene eseguita alle 3:00 AM (ora locale del dispositivo). Alcuni eventi vengono inviati alla prima ora disponibile nel corso della giornata. Questi orari non sono configurabili.
>
> Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](https://aka.ms/enterprisetelemetry) (Configurare i dati di diagnostica di Windows nell'organizzazione).  



## <a name="endpoints"></a>Endpoint

Per abilitare la condivisione dei dati, configurare il server proxy per consentire gli endpoint seguenti:

> [!Important]  
> Per la privacy e l'integrità dei dati, Windows verifica la presenza di un certificato SSL Microsoft (blocco del certificato) durante la comunicazione con gli endpoint dei dati di diagnostica. L'intercettazione e l'ispezione SSL non sono possibili. Per usare analisi desktop, escludere questi endpoint dall'ispezione SSL.<!-- BUG 4647542 -->

| Endpoint  | Funzione  |
|-----------|-----------|
| `https://aka.ms` | Usato per individuare il servizio |
| `https://v10c.events.data.microsoft.com` | Esperienza utente connessa ed endpoint componente di diagnostica. Usato dai dispositivi che eseguono Windows 10, versione 1809 o successiva o versione 1803 con l'aggiornamento cumulativo 2018-09 o versione successiva installata. |
| `https://v10.events.data.microsoft.com` | Esperienza utente connessa ed endpoint componente di diagnostica. Usato dai dispositivi che eseguono Windows 10, versione 1803 _senza_ l'aggiornamento cumulativo 2018-09 installato. |
| `https://v10.vortex-win.data.microsoft.com` | Esperienza utente connessa ed endpoint componente di diagnostica. Usato dai dispositivi che eseguono Windows 10, versione 1709 o versioni precedenti. |
| `https://vortex-win.data.microsoft.com` | Esperienza utente connessa ed endpoint componente di diagnostica. Usato dai dispositivi che eseguono Windows 7 e Windows 8.1 |
| `https://settings-win.data.microsoft.com` | Consente all'aggiornamento per la compatibilità di inviare i dati a Microsoft. |
| `http://adl.windows.com` | Consente all'aggiornamento della compatibilità di ricevere i dati di compatibilità più recenti da Microsoft. |
| `https://watson.telemetry.microsoft.com` | [Segnalazione errori Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Necessaria per monitorare lo stato di distribuzione in Windows 10, versione 1803 o versioni precedenti. |
| `https://umwatsonc.events.data.microsoft.com` | [Segnalazione errori Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Obbligatorio per i report sull'integrità dei dispositivi in Windows 10, versione 1809 o successiva. |
| `https://ceuswatcab01.blob.core.windows.net`<br> `https://ceuswatcab02.blob.core.windows.net`<br> `https://eaus2watcab01.blob.core.windows.net`<br> `https://eaus2watcab02.blob.core.windows.net`<br> `https://weus2watcab01.blob.core.windows.net`<br> `https://weus2watcab02.blob.core.windows.net` | [Segnalazione errori Windows (WER)](https://docs.microsoft.com/windows/win32/wer/windows-error-reporting). Necessaria per monitorare lo stato di distribuzione in Windows 10, versione 1809 o successiva. |
| `https://kmwatsonc.events.data.microsoft.com` | [Analisi degli arresti anomali (oca) online](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis). Obbligatorio per i report sull'integrità dei dispositivi in Windows 10, versione 1809 o successiva. |
| `https://oca.telemetry.microsoft.com`  | [Analisi degli arresti anomali (oca) online](https://docs.microsoft.com/windows/win32/dxtecharts/crash-dump-analysis). Necessaria per monitorare lo stato di distribuzione in Windows 10, versione 1803 o versioni precedenti. |
| `https://login.live.com` | Necessario per fornire un'identità del dispositivo più affidabile per desktop Analytics. <br> <br>Per disabilitare l'accesso account Microsoft all'utente finale, utilizzare le impostazioni dei criteri anziché bloccare l'endpoint. Per ulteriori informazioni, vedere [la account Microsoft nell'azienda](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication). |
| `https://graph.windows.net` | Usato per recuperare automaticamente le impostazioni, come la commercializzazione, quando si connette la gerarchia a desktop Analytics (in Configuration Manager ruolo del server). Per ulteriori informazioni, vedere [configurare il proxy per un server del sistema del sito](/sccm/core/plan-design/network/proxy-server-support#configure-the-proxy-for-a-site-system-server). |
| `https://*.manage.microsoft.com` | Usato per sincronizzare l'appartenenza alla raccolta di dispositivi, i piani di distribuzione e lo stato di conformità dei dispositivi con analisi del desktop (solo su Configuration Manager ruolo del server). Per ulteriori informazioni, vedere [configurare il proxy per un server del sistema del sito](/sccm/core/plan-design/network/proxy-server-support#configure-the-proxy-for-a-site-system-server). |


## <a name="proxy-server-authentication"></a>Autenticazione del server proxy

Assicurarsi che un proxy non blocchi i dati di diagnostica a causa dell'autenticazione. Se l'organizzazione usa l'autenticazione del server proxy per il traffico in uscita, usare uno o più degli approcci seguenti:

### <a name="bypass-recommended"></a>Bypass (scelta consigliata)

Configurare i server proxy in modo che non richiedano l'autenticazione proxy per il traffico verso gli endpoint dati di diagnostica. Questa opzione è la soluzione più completa. Funziona per tutte le versioni di Windows 10.  

### <a name="user-proxy-authentication"></a>Autenticazione proxy utente

Configurare i dispositivi per l'uso del contesto dell'utente connesso per l'autenticazione proxy. Questo metodo richiede le configurazioni seguenti:

- I dispositivi dispongono dell'aggiornamento qualitativo corrente per Windows 7, Windows 8.1 o Windows 10, versione 1703 o successiva
- Configurare il proxy a livello di utente (proxy WinINET) nelle **impostazioni proxy** nella rete & gruppo Internet di impostazioni di Windows. È anche possibile usare il pannello di controllo Opzioni Internet legacy. 
- Verificare che gli utenti dispongano dell'autorizzazione proxy per raggiungere gli endpoint dei dati di diagnostica. Questa opzione richiede che i dispositivi dispongano di utenti console con autorizzazioni proxy, quindi non è possibile usare questo metodo con dispositivi senza intestazioni.

> [!IMPORTANT]
> L'approccio di autenticazione proxy utente è incompatibile con l'uso di Microsoft Defender Advanced Threat Protection. Questo comportamento è dovuto al fatto che questa autenticazione si basa sulla chiave del registro di sistema **DisableEnterpriseAuthProxy** impostata su `0`, mentre per Microsoft Defender ATP è necessario che sia impostata su `1`. Per ulteriori informazioni, vedere [Configure computer proxy and Internet Connectivity Settings](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-atp/configure-proxy-internet-windows-defender-advanced-threat-protection).

### <a name="device-proxy-authentication"></a>Autenticazione del proxy del dispositivo

Questo approccio è il più complesso perché richiede le configurazioni seguenti:

- Assicurarsi che i dispositivi possano raggiungere il server proxy tramite WinHTTP nel contesto del sistema locale. Per configurare questo comportamento, utilizzare una delle opzioni seguenti:
  - Riga di comando ' netsh winhttp set proxy '
  - WPAD (Web Proxy Auto-Discovery Protocol)
  - Proxy trasparente
  - Connessione indirizzata o che USA Network Address Translation (NAT)

- Configurare i server proxy per consentire agli account del computer in Active Directory di accedere agli endpoint dei dati di diagnostica. Questa configurazione richiede che i server proxy supportino l'autenticazione integrata di Windows.  

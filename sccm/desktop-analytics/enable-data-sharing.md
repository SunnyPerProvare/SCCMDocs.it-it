---
title: Abilitare la condivisione dei dati
titleSuffix: Configuration Manager
description: Una Guida di riferimento per la condivisione dei dati di diagnostica con Desktop Analitica.
ms.date: 07/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: c5ba70b39330fd21077f5b7997e8aa92a1c57f42
ms.sourcegitcommit: 3a3f40f3d39cbecfb9219a64c0185ea4b2ef9671
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/04/2019
ms.locfileid: "67562005"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>Abilitare la condivisione per Desktop Analitica dei dati

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Per registrare i dispositivi Desktop Analitica, devono inviare dati di diagnostica a Microsoft. Se l'ambiente Usa un server proxy, usare queste informazioni per configurare il proxy.


## <a name="diagnostic-data-levels"></a>Livelli di dati di diagnostica

![Diagramma dei livelli di dati di diagnostica per Desktop Analitica](media/diagnostic-data-levels.png)

Quando Configuration Manager si integra con Analitica Desktop, anche usarlo per gestire il livello di dati di diagnostica nei dispositivi. Per risultati ottimali, usare Configuration Manager.

La funzionalità di base del Desktop Analitica lavora presso la **base** a livello di dati di diagnostica. Si otterranno i dati di utilizzo o di integrità per i dispositivi aggiornati senza abilitare la **Enhanced (Limited)** livello. Microsoft consiglia di attivare i **Enhanced (Limited)** a livello di dati di diagnostica. Per altre informazioni, vedere [avanzata di Windows 10 gli eventi di dati di diagnostica e i campi usati da Windows Analitica](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)).

> [!Important]   
> Microsoft offre un forte impegno a fornire gli strumenti e risorse che è inserito nel controllo della privacy. Di conseguenza, Microsoft non raccoglie i dati seguenti da dispositivi situati in paesi europei (SEE e dalla Svizzera):
>
> - Dati di diagnostica di Windows dai dispositivi Windows 8.1
> - Dati sull'utilizzo delle App per Windows 7

Per altre informazioni, vedere [privacy Desktop Analitica](/sccm/desktop-analytics/privacy).

Gli articoli seguenti sono anche ottime risorse per meglio comprendere i livelli di dati di diagnostica di Windows:

- [Windows 10 e il GDPR per Decision Maker dell'IT](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Configurare i dati di diagnostica di Windows nell'organizzazione](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!Note]  
> Il livello avanzato (limitato), quando ogni client esegue l'analisi iniziale completa, invia circa 2 MB di dati a Microsoft cloud. Il delta giornaliero varia tra 400 di 250 KB per ogni giorno.
>
> L'analisi giornaliera delta avviene a 3:00 AM (ora locale del dispositivo). Alcuni eventi vengono inviati al primo momento disponibile nel corso della giornata. Questi tempi non sono configurabili.
>
> Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](https://aka.ms/enterprisetelemetry) (Configurare i dati di diagnostica di Windows nell'organizzazione).  



## <a name="endpoints"></a>Endpoint

Per abilitare la condivisione dei dati, configurare il server proxy per consentire gli endpoint seguenti:

> [!Important]  
> Per la privacy e l'integrità dei dati, Windows cerca un certificato SSL di Microsoft durante la comunicazione con gli endpoint dei dati di diagnostica. L'ispezione e l'intercettazione SSL non sono possibili. Per usare Desktop Analitica, escludere tali endpoint dall'ispezione SSL.<!-- BUG 4647542 -->

| Endpoint  | Funzione  |
|-----------|-----------|
| `https://aka.ms` | Consente di individuare il servizio |
| `https://v10c.events.data.microsoft.com` | Esperienza dell'utente connesso e l'endpoint di componente di diagnostica. Usato dai dispositivi che eseguono Windows 10, versione 1703 o successiva, con l'aggiornamento cumulativo 2018-09 update o versione successiva. |
| `https://v10.events.data.microsoft.com` | Esperienza dell'utente connesso e l'endpoint di componente di diagnostica. Usato dai dispositivi che eseguono Windows 10, versione 1803 o successiva, _senza_ installato l'aggiornamento cumulativo-09 2018. |
| `https://v10.vortex-win.data.microsoft.com` | Esperienza dell'utente connesso e l'endpoint di componente di diagnostica. Usato dai dispositivi che eseguono Windows 10, versione 1709 o versioni precedente. |
| `https://vortex-win.data.microsoft.com` | Esperienza dell'utente connesso e l'endpoint di componente di diagnostica. Usato dai dispositivi che eseguono Windows 7 e Windows 8.1 |
| `https://settings-win.data.microsoft.com` | Consente l'aggiornamento di compatibilità inviare dati a Microsoft. |
| `http://adl.windows.com` | Consente l'aggiornamento di compatibilità ricevere i dati di compatibilità più recenti di Microsoft. |
| `https://watson.telemetry.microsoft.com` | Errore di Windows (WER) di Reporting. Richieste per monitorare l'integrità della distribuzione in Windows 10, versione 1803 o versioni precedente. |
| `https://umwatsonc.events.data.microsoft.com` | Errore di Windows (WER) di Reporting. Obbligatorio per i report sull'integrità di dispositivo in Windows 10, versione 1809 o versione successiva. |
| `https://ceuswatcab01.blob.core.windows.net`<br> `https://ceuswatcab02.blob.core.windows.net`<br> `https://eaus2watcab01.blob.core.windows.net`<br> `https://eaus2watcab02.blob.core.windows.net`<br> `https://weus2watcab01.blob.core.windows.net`<br> `https://weus2watcab02.blob.core.windows.net` | Errore di Windows (WER) di Reporting. Richieste per monitorare l'integrità della distribuzione in Windows 10, versione 1809 o versione successiva. |
| `https://kmwatsonc.events.data.microsoft.com` | Analisi dell'arresto anomalo in linea. Obbligatorio per i report sull'integrità di dispositivo in Windows 10, versione 1809 o versione successiva. |
| `https://oca.telemetry.microsoft.com`  | Online Crash Analysis (OCA). Richieste per monitorare l'integrità della distribuzione in Windows 10, versione 1803 o versioni precedente. |
| `https://login.live.com` | Deve per fornire un'identità del dispositivo più affidabile per Desktop Analitica. <br> <br>Per disabilitare l'accesso dell'utente finale Microsoft account, usare le impostazioni dei criteri anziché bloccare questo endpoint. Per altre informazioni, vedere [account Microsoft aziendali](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication). |
| `https://graph.windows.net` | Consente di recuperare automaticamente le impostazioni, ad esempio CommercialId quando ci si collega la gerarchia per Desktop Analitica (on solo ruolo del Server di Configuration Manager). |
| `https://fef.msua06.manage.microsoft.com` | Utilizzato per le appartenenze a raccolte di sincronizzazione dispositivi e piani di distribuzione stato conformità del dispositivo con Desktop Analitica (on solo ruolo del Server di Configuration Manager). |


## <a name="proxy-server-authentication"></a>Autenticazione del server proxy

Assicurarsi che un proxy non blocca i dati diagnostici a causa di autenticazione. Se l'organizzazione Usa l'autenticazione del server proxy per il traffico in uscita, usare uno o più degli approcci seguenti:

- **Bypass** (scelta consigliata): Configurare i server proxy per non richiedere l'autenticazione del proxy per il traffico verso gli endpoint dei dati di diagnostica. Questa opzione è la soluzione più completa. Funziona per tutte le versioni di Windows 10.  

- **Autenticazione dell'utente proxy**: Configurare i dispositivi per l'uso di contesto dell'utente connesso per l'autenticazione proxy. Questo metodo richiede i dispositivi che eseguono Windows 10, versione 1703 o successiva. Assicurarsi che gli utenti dispongano dell'autorizzazione di proxy per raggiungere gli endpoint dei dati di diagnostica. Questa opzione richiede che i dispositivi abbiano gli utenti della console con le autorizzazioni proxy, non è possibile utilizzare questo metodo con i dispositivi headless.  

- **L'autenticazione del dispositivo proxy**:

    - Configurare un server proxy a livello di sistema nei dispositivi.  
    - Configurare i dispositivi per l'utilizzo dell'autenticazione basata su dispositivo proxy in uscita.  
    - Configurare i server proxy per consentire gli account computer accedere agli endpoint con i dati di diagnostica.  

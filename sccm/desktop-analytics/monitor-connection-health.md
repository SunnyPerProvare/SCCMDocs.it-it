---
title: Monitorare l'integrità della connessione
titleSuffix: Configuration Manager
description: Informazioni dettagliate su come monitorare gli stati di integrità e dispositivi di connessione per Desktop Analitica in Configuration Manager.
ms.date: 06/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1f4e26f7-42f2-40c8-80cf-efd405349c6c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: a7dc9b67dbf57c1803ed732f36e1cb110260146d
ms.sourcegitcommit: e3c1eb0b75d79c05a750d49354c851d15d5e26a3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/13/2019
ms.locfileid: "67039732"
---
# <a name="monitor-connection-health"></a>Monitorare l'integrità della connessione

Usare la **integrità della connessione** dashboard in Configuration Manager per eseguire il drill-in categorie dall'integrità del dispositivo. Nella console di Configuration Manager passare ad il **raccolta Software** dell'area di lavoro, espandere il **Desktop Analitica Servicing** nodo e selezionare il **integrità della connessione** cruscotto.  

![Schermata del dashboard di integrità di connessione di Configuration Manager](media/connection-health-dashboard.png)

Quando si configura prima Desktop Analitica, questi grafici non risultino dati completi. Potrebbero essere necessari 2-3 giorni per i dispositivi attivi inviare dati di diagnostica per il servizio di Analitica Desktop, il servizio per elaborare i dati e quindi eseguire la sincronizzazione con il sito di Configuration Manager.<!-- 4098037 -->


## <a name="connection-details"></a>Dettagli della connessione

Questo riquadro Visualizza le informazioni di base seguenti sulla connessione da Configuration Manager per Analitica Desktop:

- **Nome del tenant**: Il nome della connessione in Desktop Analitica i **servizi di Azure** nodo

- **Raccolta di destinazione**: Lo stesso *raccolta di destinazione* specificato al momento della connessione di Configuration Manager per Desktop Analitica. Questa raccolta include tutti i dispositivi che consente di configurare Configuration Manager con l'ID commerciale e le impostazioni di dati di diagnostica. È il set completo di dispositivi che Configuration Manager si connette al servizio Analitica Desktop.

- **Dispositivi di destinazione**: Tutti i dispositivi nella raccolta di destinazione, meno i tipi di dispositivi seguenti:

    - Rimuovere le autorizzazioni
    - Obsoleto
    - inattivo
    - non gestito

    Per altre informazioni su questi stati dei dispositivi, vedere [sullo stato client](/sccm/core/clients/manage/monitor-clients#bkmk_about).

    > [!Note]  
    > Configuration Manager consente di caricare Desktop Analitica di tutti i dispositivi nella raccolta di destinazione meno i client obsoleti e rimossi.

- **I dispositivi idonei per DA**: Il numero di dispositivi di destinazione meno i dispositivi che non sono idonei per Desktop Analitica. Ad esempio, i dispositivi nella raccolta di destinazione che eseguono Windows Server o Windows 10 a lungo termine canale di manutenzione (LTSC).


## <a name="last-sync-details"></a>Ultima sincronizzazione dettagli

Questo riquadro mostra quando Configuration Manager si sincronizza con il servizio cloud di Analitica di Desktop e il numero di dispositivi esegue la sincronizzazione.

- **I dispositivi sincronizzati**: Il numero di dispositivi univoci che Configuration Manager ha inviato al Desktop Analitica. Il servizio include questi dispositivi nello snapshot di attualmente visibile.

- **Ultima sincronizzazione servizio**: Lo stesso come il **ultimo aggiornamento** tempo nel portale di Analitica Desktop.

- **Punto di servizio sincronizzazione**: Quando è possibile prevedere il successivo snapshot giornalieri nel Desktop Analitica.

> [!Note]  
> Nessuno di questi valori aggiornati automaticamente quando si richiede uno snapshot su richiesta. Per altre informazioni, vedere [latenza dei dati](/sccm/desktop-analytics/troubleshooting#data-latency).

Se si ritiene che alcuni dispositivi non sono visualizzate in Desktop Analitica, assicurarsi che i dispositivi sono supportati dal Desktop Analitica. Per altre informazioni, vedere [Prerequisiti](/sccm/desktop-analytics/overview#prerequisites).


## <a name="connection-health"></a>Stato della connessione

Il **integrità della connessione** grafico mostra il numero di dispositivi nei seguenti stati di integrità:  

- [Registrati correttamente](#properly-enrolled): Il dispositivo viene visualizzata nel Desktop Analitica con un inventario completo
- [Non è possibile registrare](#unable-to-enroll): Si verifica un problema di blocco che impedisce la registrazione del dispositivo
- [Avviso di configurazione](#configuration-alert): Il dispositivo non viene visualizzata nel Desktop Analitica o viene visualizzato con un inventario incompleto. Configuration Manager inoltre identificato un problema con la registrazione di dispositivi.
- [In attesa di registrazione](#awaiting-enrollment): Configuration Manager è configurato il dispositivo, ma non viene ancora visualizzato nel Desktop Analitica
- [Stato in sospeso](#status-pending): È comunque la configurazione di questo dispositivo, Configuration Manager o non avere dati sufficienti dal dispositivo per determinarne lo stato
- [I dati mancanti](#missing-data): Configuration Manager è configurato il dispositivo, ma Analitica Desktop include solo dati parziali

<!-- 
- [Configuration issues](#configuration-issues)  
- [Client not installed](#client-not-installed)  
- [Waiting for enrollment](#waiting-for-enrollment)  
- [Missing prerequisites](#missing-prerequisites)  
 -->

Il numero totale di dispositivi in questo grafico deve essere lo stesso come il **dispositivi idonei per DA** valore nella sezione dettagli della connessione.

Selezionare la sezione del grafico per eseguire il drill-down nell'elenco dei dispositivi con tale stato. Per altre informazioni, vedere [elenco dei dispositivi](#device-list).

Selezionare il nome della categoria nella legenda per rimuovere o aggiungere dal grafico. Questa azione consente di ingrandire il grafico in modo da visualizzare le dimensioni relative dei segmenti più piccoli.

### <a name="properly-enrolled"></a>Registrati correttamente

Il dispositivo è gli attributi seguenti:

- Un client 1902 o versione successiva di Configuration Manager  
- Non sono presenti errori di configurazione  
- Desktop Analitica ricevuti i dati di diagnostica completati da questo dispositivo negli ultimi 28 giorni  
- Desktop Analitica dispone di un inventario completo della configurazione del dispositivo e le app installate  

### <a name="unable-to-enroll"></a>Non è possibile registrare

Configuration Manager rileva uno o più problemi di blocco che impediscono la registrazione del dispositivo. Per altre informazioni, vedere l'elenco delle [le proprietà del dispositivo in Configuration Manager Desktop Analitica](#bkmk_config-issues).  

Ad esempio, il client di Configuration Manager non è presente almeno versione 1902 (5.0.8790). Aggiornare il client alla versione più recente. Provare ad abilitare l'aggiornamento client automatico per il sito di Configuration Manager. Per altre informazioni, vedere [Aggiornare i client](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  

### <a name="configuration-alert"></a>Avviso di configurazione

Il dispositivo non viene visualizzata nel Desktop Analitica o viene visualizzato con un inventario incompleto. Configuration Manager inoltre identificato un problema con la registrazione di dispositivi. Per altre informazioni, vedere l'elenco delle [le proprietà del dispositivo in Configuration Manager Desktop Analitica](#bkmk_config-issues).

Ad esempio, il dispositivo non ha connettività al servizio. Per altre informazioni, vedere [connettività dell'endpoint diagnostica Windows](#windows-diagnostic-endpoint-connectivity).

### <a name="awaiting-enrollment"></a>In attesa di registrazione

Desktop Analitica non dispone di dati di diagnostica per questo dispositivo. Questo problema può essere perché sono stati aggiunti di recente il dispositivo alla raccolta di destinazione e che non ha ancora inviato i dati. Può anche significare il dispositivo non comunica correttamente con il servizio e i dati di diagnostica più recenti ha più di 28 giorni.

Assicurarsi che il dispositivo può comunicare con il servizio. Per altre informazioni, vedere [endpoint](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

### <a name="status-pending"></a>Stato in sospeso

Configuration Manager viene comunque la configurazione di questo dispositivo o non avere dati sufficienti dal dispositivo per determinarne lo stato.

### <a name="missing-data"></a>Dati mancanti

Configuration Manager è stato configurato il dispositivo, ma Analitica Desktop non è possibile creare una valutazione della compatibilità. È privo di un set di dati completo per la configurazione del dispositivo (censimento) o installato le App (inventario).

Questo errore spesso viene risolto automaticamente quando il dispositivo esegue un nuovo tentativo. Se persiste, assicurarsi che il dispositivo può comunicare con il servizio. Per altre informazioni, vedere [endpoint](/sccm/desktop-analytics/enable-data-sharing#endpoints).  


## <a name="device-list"></a>Elenco dei dispositivi

Per visualizzare un elenco specifico di dispositivi in base allo stato, iniziare con il **integrità della connessione** dashboard. Selezionare uno dei segmenti dell'oggetto di **integrità della connessione** riquadro e il drill-down nell'elenco dei dispositivi in questo stato. In questa vista di dispositivo personalizzato consente di visualizzare le colonne seguenti Desktop Analitica per impostazione predefinita:

- Configurazione dell'ID commerciale
- Aggiornamento di compatibilità minimo
- Opt-in Windows i dati di diagnostica
- Windows dati commerciali acconsenti esplicitamente
- Connettività dell'endpoint diagnostica Windows

> [!Note]  
> Ignorare la colonna per **connettività dell'endpoint diagnostici Office**. È riservato per le funzionalità future.

Queste colonne corrispondono al tasto [prerequisiti](/sccm/desktop-analytics/overview#prerequisites) per i dispositivi di comunicare con Desktop Analitica.

![Schermata di correttamente registrato elenco dei dispositivi](media/sccm-device-list-properly-enrolled.png)

Selezionare un dispositivo per visualizzare l'elenco completo delle proprietà disponibili nel riquadro dei dettagli. È anche possibile aggiungere uno qualsiasi di queste proprietà come colonne all'elenco dei dispositivi.


## <a name="bkmk_config-issues"></a> Proprietà del dispositivo

Le seguenti proprietà del dispositivo Analitica Desktop sono disponibili come colonne nell'elenco dei dispositivi di Configuration Manager:

- [Configurazione valutazione](#appraiser-configuration)  
- [Aggiornamento di compatibilità minimo](#minimum-compatibility-update)  
- [Versione di valutazione](#appraiser-version)  
- [Ultimo eseguito correttamente, completo Appraiser](#last-successful-full-run-of-appraiser)  
- [Raccolta dei dati appraiser](#appraiser-data-collection)  
- [Ultima esecuzione completa ha esito positivo di censimento](#last-successful-full-run-of-census)  
- [Raccolta dei dati di censimento](#census-data-collection)  
- [Connettività dell'endpoint diagnostica Windows](#windows-diagnostic-endpoint-connectivity)  
- [Controllare i dati di diagnostica per l'utente finale](#check-end-user-diagnostic-data)  
- [Controllo utente proxy](#check-user-proxy)  
- [Configurazione dell'ID commerciale](#commercial-id-configuration)  
- [Windows dati commerciali acconsenti esplicitamente](#windows-commercial-data-opt-in)  
- [Controllare il nome di dispositivo nei dati di diagnostica](#check-device-name-in-diagnostic-data)  
- [Configurazione del servizio DiagTrack](#diagtrack-service-configuration)  
- [Versione DiagTrack](#diagtrack-version)  
- [Recupero ID SQM](#sqm-id-retrieval)  
- [Recupero di identificatore univoco del dispositivo](#unique-device-identifier-retrieval)  
- [Opt-in Windows i dati di diagnostica](#windows-diagnostic-data-opt-in)  

> [!Note]  
> Ignorare le proprietà per **connettività dell'endpoint diagnostici Office** e **Office i dati di diagnostica acconsenti esplicitamente**. Sono riservate per le funzionalità future.

Il **più frequenti blocchi della registrazione e gli avvisi di configurazione** riquadro del dashboard dello stato di connessione vengono visualizzate le proprietà che i dispositivi più frequentemente segnalano un problema.

### <a name="appraiser-configuration"></a>Configurazione valutazione

<!--20,21-->
Appraiser è il componente di Windows corrispondente per il [compatibilità aggiornamenti](/sccm/desktop-analytics/enroll-devices#update-devices). Valuta le App e driver di dispositivo per la compatibilità con la versione più recente di Windows. 

Se questo controllo ha esito positivo, il componente appraiser è configurato correttamente nel dispositivo.

In caso contrario, potrebbe visualizzare uno dei seguenti errori:

- Non è possibile configurare la raccolta dati di compatibilità dall'app di dispositivo (SetRequestAllAppraiserVersions). Controllare i log per i dettagli dell'eccezione  

- Non è possibile configurare la raccolta dati di compatibilità dall'app di dispositivo (SetRequestAllAppraiserVersions). Controllare i log per i dettagli dell'eccezione  

- Non è possibile scrivere il Commercialdataoptin alla chiave del Registro di sistema `HKLM:\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Appraiser`. Controllare le autorizzazioni  

Controllare le autorizzazioni per questa chiave del Registro di sistema. Assicurarsi che l'account sistema locale possa accedere a questa chiave per il client di Configuration Manager da impostare.  

Per altre informazioni, esaminare M365AHandler.log sul client.  

### <a name="minimum-compatibility-update"></a>Aggiornamento di compatibilità minimo

<!--18,19,32-->
L'aggiornamento di compatibilità (appraiser.dll) non è installata o aggiornata nel dispositivo. È meno recente il requisito minimo per Desktop Analitica, 10.0.17763.

Installare l'aggiornamento di compatibilità più recente. Per altre informazioni, vedere [aggiornamenti per la compatibilità](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser).

### <a name="appraiser-version"></a>Versione di valutazione

Questa proprietà consente di visualizzare la versione corrente del componente Appraiser nel dispositivo. Mostra la versione del file su `%windir%\System32\appraiser.dll`, senza i separatore decimale. Ad esempio, versione file 10.0.17763 Visualizza come 10017763.

### <a name="last-successful-full-run-of-appraiser"></a>Ultimo eseguito correttamente, completo Appraiser

Questa proprietà consente di visualizzare la data e ora in cui il dispositivo ultima esecuzione completata Appraiser.

### <a name="appraiser-data-collection"></a>Raccolta dei dati appraiser

<!--Appraiser run status-->
<!--22,33-->
Questa proprietà indica il risultato più recente di Windows che esegue il componente di valutazione.

In caso contrario ha esito positivo, è possibile che visualizzi uno dei seguenti errori:

- Non è possibile raccogliere dati di compatibilità dell'app (RunAppraiser). Per informazioni dettagliate vedere i log  

- Raccolta di dati di compatibilità di App (CompatTelRunner.exe) è stata completata con un codice di errore  

Per altre informazioni, esaminare M365AHandler.log sul client.

Cercare il file seguente: `%windir%\System32\CompatTelRunner.exe`. Se non esiste, reinstallare le [compatibilità aggiornamenti](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser). Assicurarsi che nessun altro componente di sistema è la rimozione di questo file, ad esempio criteri di gruppo o un servizio antimalware.

Se il file M365Handler.log sul client include uno dei seguenti errori: `RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1`
`RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005`
`RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005`  

Per aiutare a risolvere questi errori, eseguire i comandi seguenti da una console di Windows PowerShell con privilegi elevata sul client interessati:

```PowerShell
# stop associated services
Stop-Service -Name diagtrack #Connected User Experiences and Telemetry
Stop-Service -Name pcasvc #Program Compatibility Assistant Service
Stop-Service -Name dps #Diagnostic Policy Service

# regenerate diagnostic data cache
Remove-Item -Path $Env:WinDir\appcompat\programs\amcache.hve
Remove-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name AmiHivePermissionsCorrect -Force

# set ASL logging level to output log files in %windir%\temp
New-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name LogFlags -Value 4 -PropertyType DWord -Force

# restart services
Start-Service -Name diagtrack
Start-Service -Name pcasvc
Start-Service -Name dps
```

### <a name="last-successful-full-run-of-census"></a>Ultima esecuzione completa ha esito positivo di censimento

Questa proprietà consente di visualizzare la data e ora in cui il dispositivo ultima esecuzione completata censimento.

### <a name="census-data-collection"></a>Raccolta dei dati di censimento

<!-- Census run status -->
<!--51,52-->
Census è il componente di Windows che esegue l'inventario del dispositivo. Questi dati di inventario vengono utilizzati per comprendere il dispositivo e la relativa configurazione.

Questa proprietà indica il risultato più recente di Windows che esegue il componente di censimento.

In caso contrario ha esito positivo, è possibile che visualizzi uno dei seguenti errori:

- Non è possibile raccogliere dati sul dispositivo e la relativa configurazione (RunCensus). Controllare i log per i dettagli dell'eccezione  

- Dispositivo e la configurazione strumento di raccolta dati (devicecensus.exe) non trovato  

Per altre informazioni, esaminare M365AHandler.log sul client.

Cercare il file seguente: `%windir%\System32\DeviceCensus.exe`. Se non esiste, reinstallare le [compatibilità aggiornamenti](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser). Assicurarsi che nessun altro componente di sistema è la rimozione di questo file, ad esempio criteri di gruppo o un servizio antimalware.

### <a name="windows-diagnostic-endpoint-connectivity"></a>Connettività dell'endpoint diagnostica Windows

<!--12,15-->
Se questo controllo ha esito positivo, il dispositivo possa connettersi all'endpoint di esperienze utente connesse e telemetria (Vortex).

In caso contrario, potrebbe essere visualizzato uno dei seguenti errori:  

- Impossibile connettersi all'utente connesso esperienza e i dati di telemetria endpoint (Vortex). Controllare le impostazioni di rete/proxy  

- Non è possibile verificare la connettività all'utente connesso esperienza e i dati di telemetria endpoint (CheckVortexConnectivity). Controllare i log per i dettagli dell'eccezione  

Dispositivi verificano la connettività con una richiesta GET all'endpoint seguente basata sulla versione del sistema operativo:

| Versione del sistema operativo | Endpoint |
|------------|----------|
| Windows 10, versione 1803 o successiva con aggiornamento cumulativo più recente | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Windows 10, versione 1803 o successiva senza il 2018-09 o in un secondo momento cumulative update | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10, versione 1709 o versioni precedente | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 o Windows 8.1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

Assicurarsi che il dispositivo può comunicare con il servizio. Questo controllo verifica alcuni ma non tutti gli endpoint necessari. Per altre informazioni, vedere [endpoint](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

Per altre informazioni, esaminare M365AHandler.log sul client.  

### <a name="check-end-user-diagnostic-data"></a>Controllare i dati di diagnostica per l'utente finale

<!--1004-->
Se questo controllo non è riuscito, un utente ha selezionato un inferiore Windows i dati di diagnostica sul dispositivo. Può anche essere causato da un oggetto Criteri di gruppo in conflitto. Per altre informazioni, vedere [delle impostazioni di Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).

A seconda delle esigenze aziendali, è possibile disabilitare la scelta dell'utente tramite criteri di gruppo. Usare l'impostazione **interfaccia utente di acconsentire esplicitamente impostazione dati di telemetria configura**. Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management) (Configurare i dati di diagnostica di Windows nell'organizzazione).

### <a name="check-user-proxy"></a>Controllo utente proxy

<!--30,35-->
L'impostazione DisableEnterpriseAuthProxy è abilitato per impostazione predefinita per Windows 7. Per i computer Windows 8.1, Configuration Manager imposta l'impostazione DisableEnterpriseAuthProxy su 0 (non disabilitato).

Questa proprietà può visualizzare gli errori seguenti:

- Autenticazione proxy è abilitato. Impostare DisableEnterpriseAuthProxy su 0 in `HKLM\Software\Policies\Microsoft\Windows\DataCollection`

- Non è possibile verificare lo stato di autenticazione proxy. Controllare i log per i dettagli dell'eccezione

Per altre informazioni, esaminare M365AHandler.log sul client.  

Controllare le autorizzazioni per questa chiave del Registro di sistema. Assicurarsi che l'account sistema locale possa accedere a questa chiave per il client di Configuration Manager da impostare. Può anche essere causato da un oggetto Criteri di gruppo in conflitto. Per altre informazioni, vedere [delle impostazioni di Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

### <a name="commercial-id-configuration"></a>Configurazione dell'ID commerciale

<!--9, 11, 53-->
Microsoft Usa un ID commerciale univoco per mappare le informazioni dai dispositivi all'area di lavoro di Analitica Desktop. Quando Configuration Manager si integra con Desktop Analitica, interroga automaticamente il servizio per questo ID. Configuration Manager deve applicare automaticamente questo ID per i client a cui si impostazioni Analitica Desktop di destinazione.

Se questo controllo ha esito positivo, quindi il dispositivo sia configurato correttamente con un ID commerciale.

In caso contrario, potrebbe essere visualizzato uno dei seguenti errori:

- Non è possibile scrivere il CommercialId alla chiave del Registro di sistema `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`. Controllare le autorizzazioni  

- Non è possibile aggiornare il CommercialId nella chiave del Registro di sistema `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`. Controllare i log per i dettagli dell'eccezione  

- Specificare il valore corretto CommercialId in `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`  

Per altre informazioni, esaminare M365AHandler.log sul client.  

Controllare le autorizzazioni per questa chiave del Registro di sistema. Assicurarsi che l'account sistema locale possa accedere a questa chiave per il client di Configuration Manager da impostare. Può anche essere causato da un oggetto Criteri di gruppo in conflitto. Per altre informazioni, vedere [delle impostazioni di Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

È un ID diverso per il dispositivo. Questa chiave del Registro di sistema viene utilizzata dai criteri di gruppo. Tramite l'ID fornito da Configuration Manager ha la precedenza.  

<a name="bkmk_ViewCommercialID"></a> Per visualizzare l'ID commerciale nel portale di Analitica Desktop, usare la procedura seguente:

1. Passare al portale di Analitica di Desktop e selezionare **servizi connessi** nel gruppo di impostazioni globali.  

2. Nel **servizi connessi** riquadro, il **registrare i dispositivi** per impostazione predefinita è selezionato il riquadro. Nel riquadro di registrazione dispositivi, la sezione delle informazioni consente di visualizzare la chiave ID commerciale.  

![Screenshot dell'ID commerciale nel portale di Analitica Desktop](media/commercial-id.png)

> [!Important]  
> Solo **ottenere la nuova chiave ID** quando non è possibile utilizzare quella corrente. Se si rigenera l'ID commerciale [nuovamente i dispositivi registrati con il nuovo Id](/sccm/desktop-analytics/enroll-devices#device-enrollment). Questo processo potrebbe comportare la perdita di dati di diagnostica durante la transizione.  

### <a name="windows-commercial-data-opt-in"></a>Windows dati commerciali acconsenti esplicitamente

<!--64-->
Questa proprietà è specifica per i dispositivi che eseguono Windows 7 o Windows 8.1. L'esecuzione dei test simili come [opt-in Windows i dati di diagnostica](#windows-diagnostic-data-opt-in), tranne per il e valore.

### <a name="check-device-name-in-diagnostic-data"></a>Controllare il nome di dispositivo nei dati di diagnostica

<!--56,58-->
Se questo controllo ha esito positivo, il dispositivo è configurato correttamente per condividere il nome del dispositivo.

In caso contrario, potrebbe essere visualizzato uno dei seguenti errori:

- Non può controllare il nome del dispositivo da inviare a Microsoft come parte dei dati di diagnostica di Windows. Controllare i log per i dettagli dell'eccezione  

- Non è possibile scrivere AllowDeviceNameInTelemetry alla chiave del Registro di sistema `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`. Controllare le autorizzazioni  

Per altre informazioni, esaminare M365AHandler.log sul client.  

Controllare le autorizzazioni per questa chiave del Registro di sistema. Assicurarsi che l'account sistema locale possa accedere a questa chiave per il client di Configuration Manager da impostare. Può anche essere causato da un oggetto Criteri di gruppo in conflitto. Per altre informazioni, vedere [delle impostazioni di Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Assicurarsi che un altro meccanismo di criterio, ad esempio criteri di gruppo, non è se si disabilita questa impostazione.

### <a name="diagtrack-service-configuration"></a>Configurazione del servizio DiagTrack

<!--44,45,50-->
Se questo controllo ha esito positivo, il componente DiagTrack è configurato correttamente nel dispositivo. La versione minima richiesta per Desktop Analitica è 10010586 (10.0.10586).

In caso contrario, potrebbe visualizzare uno dei seguenti errori:

- Esperienze utente connesse e telemetria (diagtrack.dll) componente è obsoleta. Controllare i requisiti  

- Impossibile trovare il componente di dati di telemetria (diagtrack.dll) e l'esperienza dell'utente connesso. Controllare i requisiti  

- Abilitare e avviare il servizio esperienze utente connesse e telemetria per inviare dati a Microsoft  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

Installare gli aggiornamenti più recenti. Per altre informazioni, vedere [gli aggiornamenti del dispositivo](/sccm/desktop-analytics/enroll-devices#update-devices).

Assicurarsi che il **esperienze utente connesse e telemetria** servizio nel dispositivo è in esecuzione.

### <a name="diagtrack-version"></a>Versione DiagTrack

Questa proprietà consente di visualizzare la versione corrente del componente esperienze utente connesse e telemetria nel dispositivo. Mostra la versione del file su `%windir%\System32\diagtrack.dll`, senza i separatore decimale. Ad esempio, versione file 10.0.10586 Visualizza come 10010586.

### <a name="sqm-id-retrieval"></a>Recupero ID SQM

<!--38-->
Questa proprietà è principalmente per i dispositivi Windows 7. Può essere usata dalle versioni più recenti del sistema operativo come identificatore di fallback per il dispositivo.

In caso contrario ha esito positivo, è possibile visualizzare l'errore seguente:

- Non è possibile recuperare l'identificatore di dati di telemetria dispositivo legacy (SQM ID)

Per altre informazioni, esaminare M365AHandler.log sul client.  

Assicurarsi che non si dispone di ID duplicati nell'ambiente in uso. Ad esempio, se i dispositivi sono stati distribuiti con un'immagine del sistema operativo che non è stata generalizzata.

### <a name="unique-device-identifier-retrieval"></a>Recupero di identificatore univoco del dispositivo

<!--54-->
Desktop Analitica Usa il servizio Account Microsoft per un'identità del dispositivo più affidabile.

Assicurarsi che il **Microsoft Account Assistente** servizio non è disabilitato. Il tipo di avvio deve essere **manuale (avvio Trigger)** .

Per disabilitare l'accesso dell'utente finale Microsoft account, usare le impostazioni dei criteri anziché bloccare questo endpoint. Per altre informazioni, vedere [account Microsoft aziendali](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication).

### <a name="windows-diagnostic-data-opt-in"></a>Opt-in Windows i dati di diagnostica

<!--8,40,55,62-->
Questa proprietà verifica che Windows sia configurato correttamente per consentire i dati di diagnostica. Verifica il valore AllowTelemetry nelle chiavi del Registro di sistema seguente:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

Controllare le autorizzazioni per queste chiavi del Registro di sistema. Assicurarsi che l'account sistema locale possa accedere a queste chiavi al client di Configuration Manager per set. Può anche essere causato da un oggetto Criteri di gruppo in conflitto. Per altre informazioni, vedere [delle impostazioni di Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Per altre informazioni, esaminare M365AHandler.log sul client.  



## <a name="see-also"></a>Vedere anche

[Risolvere i problemi di Analitica Desktop](/sccm/desktop-analytics/troubleshooting)
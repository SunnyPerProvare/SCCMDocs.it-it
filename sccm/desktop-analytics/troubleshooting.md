---
title: Risoluzione dei problemi relativi a Desktop Analitica
titleSuffix: Configuration Manager
description: Dettagli tecnici per risolvere i problemi con Desktop Analitica.
ms.date: 06/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 32e3d1185ff1f93a988074cdbc8dd7a14a4dcba8
ms.sourcegitcommit: 725e1bf7d3250c2b7b7be9da01135517428be7a1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822088"
---
# <a name="troubleshooting-desktop-analytics"></a>Risoluzione dei problemi relativi a Desktop Analitica

Usare i dettagli in questo articolo per risolvere i problemi con Desktop Analitica integrato con Configuration Manager.



## <a name="confirm-prerequisites"></a>Verificare i prerequisiti

Molti problemi comuni sono causati da prerequisiti mancanti. Prima di tutto verificare le configurazioni seguenti:

- [Prerequisiti](/sccm/desktop-analytics/overview#prerequisites)  

- [Aggiornamenti dei componenti di Windows](/sccm/desktop-analytics/enroll-devices#update-devices)  

- [Come abilitare la condivisione dei dati](/sccm/desktop-analytics/enable-data-sharing), che include gli argomenti seguenti:  

    - Endpoint Internet a cui i client devono connettersi  

    - Autenticazione del server proxy  

    - Livelli di dati di diagnostica  



## <a name="monitor-connection-health"></a>Monitorare l'integrità della connessione

Usare la **integrità della connessione** dashboard in Configuration Manager per eseguire il drill-in categorie dall'integrità del dispositivo. Nella console di Configuration Manager passare ad il **raccolta Software** dell'area di lavoro, espandere il **Desktop Analitica Servicing** nodo e selezionare il **integrità della connessione** cruscotto.  

![Schermata del dashboard di integrità di connessione di Configuration Manager](media/connection-health-dashboard.png)

Quando si configura prima Desktop Analitica, questi grafici non risultino dati completi. Potrebbero essere necessari 2-3 giorni per i dispositivi attivi inviare dati di diagnostica per il servizio di Analitica Desktop, il servizio per elaborare i dati e quindi eseguire la sincronizzazione con il sito di Configuration Manager.<!-- 4098037 -->


### <a name="connection-details"></a>Dettagli della connessione

<!-- 4412133 -->

Questo riquadro mostra le informazioni di base, ad esempio il tenant connesso nome e le ore per gli aggiornamenti dal servizio. Il **dispositivi di destinazione** valore costituito da tutti i dispositivi nella raccolta di destinazione, meno i tipi di dispositivi seguenti:

- Rimuovere le autorizzazioni
- Obsoleto
- inattivo
- non gestito

Per altre informazioni su questi stati dei dispositivi, vedere [sullo stato client](/sccm/core/clients/manage/monitor-clients#bkmk_about).

> [!Note]  
> Configuration Manager consente di caricare Desktop Analitica di tutti i dispositivi nella raccolta di destinazione meno i client obsoleti e rimossi.

### <a name="connected-devices"></a>Dispositivi connessi

Se si ritiene che alcuni dispositivi non sono visualizzate in Desktop Analitica, verificare innanzitutto la percentuale di **dispositivi connessi**. Questo grafico rappresenta la percentuale di dispositivi utilizzando la formula seguente:

- Numeratore: Il **dispositivi di destinazione** valore il [i dettagli della connessione](#connection-details) riquadro
- Denominatore: Tutti i dispositivi in Configuration Manager meno dispositivi inattivi e non gestiti

Se è inferiore al 100%, assicurarsi che i dispositivi sono supportati dal Desktop Analitica. Per altre informazioni, vedere [Prerequisiti](/sccm/desktop-analytics/overview#prerequisites).


### <a name="connection-health-states"></a>Stati di integrità connessione

Esaminare quindi le **integrità della connessione** grafico. Viene visualizzato il numero di dispositivi in categorie di integrità seguenti:  

- [Registrati correttamente](#properly-enrolled)  
- [Problemi di configurazione](#configuration-issues)  
- [Client non installato](#client-not-installed)  
- [In attesa di registrazione](#waiting-for-enrollment)  
- [Prerequisiti mancanti](#missing-prerequisites)  
- [Dati mancanti](#missing-data)  

Selezionare il nome della categoria da rimuovere o aggiungere dal grafico. Questa azione consente di ingrandire il grafico in modo da visualizzare le dimensioni relative dei segmenti più piccoli.

#### <a name="properly-enrolled"></a>Registrati correttamente

Il dispositivo è gli attributi seguenti:

- Un client 1902 o versione successiva di Configuration Manager  
- Non sono presenti errori di configurazione  
- Desktop Analitica ricevuti i dati di diagnostica completati da questo dispositivo negli ultimi 28 giorni  
- Desktop Analitica dispone di un inventario completo della configurazione del dispositivo e le app installate  

#### <a name="configuration-issues"></a>Problemi di configurazione

Configuration Manager rileva uno o più problemi con la configurazione necessaria per Desktop Analitica. Per altre informazioni, vedere l'elenco delle [le proprietà del dispositivo in Configuration Manager Desktop Analitica](#bkmk_config-issues).  

#### <a name="client-not-installed"></a>Client non installato

Il dispositivo viene incluso per Desktop Analitica, ma non è un client di Configuration Manager.

Il client di Configuration Manager deve configurare e gestire il dispositivo per Desktop Analitica. Per altre informazioni, vedere [Metodi di installazione client](/sccm/core/clients/deploy/plan/client-installation-methods).  

#### <a name="waiting-for-enrollment"></a>In attesa di registrazione

Desktop Analitica non dispone di dati di diagnostica per questo dispositivo. Questo problema può essere perché il dispositivo sono state recentemente aggiunte alla raccolta di destinazione e non ha ancora inviato i dati. Può anche significare il dispositivo non comunica correttamente con il servizio e i dati di diagnostica più recenti ha più di 28 giorni.

Assicurarsi che il dispositivo è in grado di comunicare con il servizio. Per altre informazioni, vedere [endpoint](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

#### <a name="missing-prerequisites"></a>Prerequisiti mancanti

Il client di Configuration Manager non è presente almeno versione 1902 (5.0.8790).

Aggiornare il client alla versione più recente. Provare ad abilitare l'aggiornamento client automatico per il sito di Configuration Manager. Per altre informazioni, vedere [Aggiornare i client](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  

#### <a name="missing-data"></a>Dati mancanti

Analitica desktop non è possibile creare una valutazione della compatibilità. È privo di un set di dati completo per la configurazione del dispositivo (censimento) o installato le App (inventario).

Questo errore spesso viene risolto automaticamente quando il dispositivo esegue un nuovo tentativo. Se persiste, assicurarsi che il dispositivo è in grado di comunicare con il servizio. Per altre informazioni, vedere [endpoint](/sccm/desktop-analytics/enable-data-sharing#endpoints).  


### <a name="device-list"></a>Elenco dei dispositivi

Per visualizzare un elenco specifico di dispositivi in base allo stato, iniziare con il **integrità della connessione** dashboard. Selezionare uno dei segmenti dell'oggetto di **integrità della connessione** riquadro e il drill-down nell'elenco dei dispositivi in questa categoria. In questa vista di dispositivo personalizzato consente di visualizzare le colonne seguenti Desktop Analitica per impostazione predefinita:

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


### <a name="bkmk_config-issues"></a> Proprietà dei dispositivi desktop Analitica in Configuration Manager

Le colonne seguenti sono disponibili nell'elenco dei dispositivi:

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

#### <a name="appraiser-configuration"></a>Configurazione valutazione

<!--20,21-->
Appraiser è il componente di Windows corrispondente per il [compatibilità aggiornamenti](/sccm/desktop-analytics/enroll-devices#update-devices). Valuta le App e driver di dispositivo per la compatibilità con la versione più recente di Windows. 

Se questo controllo ha esito positivo, il componente appraiser è configurato correttamente nel dispositivo.

In caso contrario, potrebbe visualizzare uno dei seguenti errori:

- Non è possibile configurare la raccolta dati di compatibilità dall'app di dispositivo (SetRequestAllAppraiserVersions). Controllare i log per i dettagli dell'eccezione  

- Non è possibile configurare la raccolta dati di compatibilità dall'app di dispositivo (SetRequestAllAppraiserVersions). Controllare i log per i dettagli dell'eccezione  

- Non è possibile scrivere il Commercialdataoptin alla chiave del Registro di sistema `HKLM:\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Appraiser`. Controllare le autorizzazioni  

Controllare le autorizzazioni per questa chiave del Registro di sistema. Assicurarsi che l'account sistema locale possa accedere a questa chiave per il client di Configuration Manager da impostare.  

Per altre informazioni, esaminare M365AHandler.log sul client.  

#### <a name="minimum-compatibility-update"></a>Aggiornamento di compatibilità minimo

<!--18,19,32-->
L'aggiornamento di compatibilità (appraiser.dll) non è installata o aggiornata nel dispositivo. È meno recente il requisito minimo per Desktop Analitica, 10.0.17763.

Installare l'aggiornamento di compatibilità più recente. Per altre informazioni, vedere [aggiornamenti per la compatibilità](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser).

#### <a name="appraiser-version"></a>Versione di valutazione

Questa proprietà consente di visualizzare la versione corrente del componente Appraiser nel dispositivo. Mostra la versione del file su `%windir%\System32\appraiser.dll`, senza i separatore decimale. Ad esempio, versione file 10.0.17763 Visualizza come 10017763.

#### <a name="last-successful-full-run-of-appraiser"></a>Ultimo eseguito correttamente, completo Appraiser

Questa proprietà consente di visualizzare la data e ora in cui il dispositivo ultima esecuzione completata Appraiser.

#### <a name="appraiser-data-collection"></a>Raccolta dei dati appraiser

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

#### <a name="last-successful-full-run-of-census"></a>Ultima esecuzione completa ha esito positivo di censimento

Questa proprietà consente di visualizzare la data e ora in cui il dispositivo ultima esecuzione completata censimento.

#### <a name="census-data-collection"></a>Raccolta dei dati di censimento

<!-- Census run status -->
<!--51,52-->
Census è il componente di Windows che esegue l'inventario del dispositivo. Questi dati di inventario vengono utilizzati per comprendere il dispositivo e la relativa configurazione.

Questa proprietà indica il risultato più recente di Windows che esegue il componente di censimento.

In caso contrario ha esito positivo, è possibile che visualizzi uno dei seguenti errori:

- Non è possibile raccogliere dati sul dispositivo e la relativa configurazione (RunCensus). Controllare i log per i dettagli dell'eccezione  

- Dispositivo e la configurazione strumento di raccolta dati (devicecensus.exe) non trovato  

Per altre informazioni, esaminare M365AHandler.log sul client.

Cercare il file seguente: `%windir%\System32\DeviceCensus.exe`. Se non esiste, reinstallare le [compatibilità aggiornamenti](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser). Assicurarsi che nessun altro componente di sistema è la rimozione di questo file, ad esempio criteri di gruppo o un servizio antimalware.

#### <a name="windows-diagnostic-endpoint-connectivity"></a>Connettività dell'endpoint diagnostica Windows

<!--12,15-->
Se questo controllo ha esito positivo, il dispositivo è in grado di connettersi all'utente connesso esperienza e i dati di telemetria endpoint (Vortex).

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

Assicurarsi che il dispositivo è in grado di comunicare con il servizio. Questo controllo verifica alcuni ma non tutti gli endpoint necessari. Per altre informazioni, vedere [endpoint](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

Per altre informazioni, esaminare M365AHandler.log sul client.  

#### <a name="check-end-user-diagnostic-data"></a>Controllare i dati di diagnostica per l'utente finale

<!--1004-->
Se questo controllo non è riuscito, un utente ha selezionato un inferiore Windows i dati di diagnostica sul dispositivo. Può anche essere causato da un oggetto Criteri di gruppo in conflitto. Per altre informazioni, vedere [delle impostazioni di Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).

A seconda delle esigenze aziendali, è possibile disabilitare la scelta dell'utente tramite criteri di gruppo. Usare l'impostazione **interfaccia utente di acconsentire esplicitamente impostazione dati di telemetria configura**. Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management) (Configurare i dati di diagnostica di Windows nell'organizzazione).

#### <a name="check-user-proxy"></a>Controllo utente proxy

<!--30,35-->
L'impostazione DisableEnterpriseAuthProxy è abilitato per impostazione predefinita per Windows 7. Per i computer Windows 8.1, Configuration Manager imposta l'impostazione DisableEnterpriseAuthProxy su 0 (non disabilitato).

Questa proprietà può visualizzare gli errori seguenti:

- Autenticazione proxy è abilitato. Impostare DisableEnterpriseAuthProxy su 0 in `HKLM\Software\Policies\Microsoft\Windows\DataCollection`

- Non è possibile verificare lo stato di autenticazione proxy. Controllare i log per i dettagli dell'eccezione

Per altre informazioni, esaminare M365AHandler.log sul client.  

Controllare le autorizzazioni per questa chiave del Registro di sistema. Assicurarsi che l'account sistema locale possa accedere a questa chiave per il client di Configuration Manager da impostare. Può anche essere causato da un oggetto Criteri di gruppo in conflitto. Per altre informazioni, vedere [delle impostazioni di Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

#### <a name="commercial-id-configuration"></a>Configurazione dell'ID commerciale

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

#### <a name="windows-commercial-data-opt-in"></a>Windows dati commerciali acconsenti esplicitamente

<!--64-->
Questa proprietà è specifica per i dispositivi che eseguono Windows 7 o Windows 8.1. L'esecuzione dei test simili come [opt-in Windows i dati di diagnostica](#windows-diagnostic-data-opt-in), tranne per il e valore.

#### <a name="check-device-name-in-diagnostic-data"></a>Controllare il nome di dispositivo nei dati di diagnostica

<!--56,58-->
Se questo controllo ha esito positivo, il dispositivo è configurato correttamente per condividere il nome del dispositivo.

In caso contrario, potrebbe essere visualizzato uno dei seguenti errori:

- Non può controllare il nome del dispositivo da inviare a Microsoft come parte dei dati di diagnostica di Windows. Controllare i log per i dettagli dell'eccezione  

- Non è possibile scrivere AllowDeviceNameInTelemetry alla chiave del Registro di sistema `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`. Controllare le autorizzazioni  

Per altre informazioni, esaminare M365AHandler.log sul client.  

Controllare le autorizzazioni per questa chiave del Registro di sistema. Assicurarsi che l'account sistema locale possa accedere a questa chiave per il client di Configuration Manager da impostare. Può anche essere causato da un oggetto Criteri di gruppo in conflitto. Per altre informazioni, vedere [delle impostazioni di Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Assicurarsi che un altro meccanismo di criterio, ad esempio criteri di gruppo, non è se si disabilita questa impostazione.

#### <a name="diagtrack-service-configuration"></a>Configurazione del servizio DiagTrack

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

#### <a name="diagtrack-version"></a>Versione DiagTrack

Questa proprietà consente di visualizzare la versione corrente del componente esperienze utente connesse e telemetria nel dispositivo. Mostra la versione del file su `%windir%\System32\diagtrack.dll`, senza i separatore decimale. Ad esempio, versione file 10.0.10586 Visualizza come 10010586.

#### <a name="sqm-id-retrieval"></a>Recupero ID SQM

<!--38-->
Questa proprietà è principalmente per i dispositivi Windows 7. Può essere usata dalle versioni più recenti del sistema operativo come identificatore di fallback per il dispositivo.

In caso contrario ha esito positivo, è possibile visualizzare l'errore seguente:

- Non è possibile recuperare l'identificatore di dati di telemetria dispositivo legacy (SQM ID)

Per altre informazioni, esaminare M365AHandler.log sul client.  

Assicurarsi che non si dispone di ID duplicati nell'ambiente in uso. Ad esempio, se i dispositivi sono stati distribuiti con un'immagine del sistema operativo che non è stata generalizzata.

#### <a name="unique-device-identifier-retrieval"></a>Recupero di identificatore univoco del dispositivo

<!--54-->
Desktop Analitica Usa il servizio Account Microsoft per un'identità del dispositivo più affidabile.

Assicurarsi che il **Microsoft Account Assistente** servizio non è disabilitato. Il tipo di avvio deve essere **manuale (avvio Trigger)** .

Per disabilitare l'accesso dell'utente finale Microsoft account, usare le impostazioni dei criteri anziché bloccare questo endpoint. Per altre informazioni, vedere [account Microsoft aziendali](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication).

#### <a name="windows-diagnostic-data-opt-in"></a>Opt-in Windows i dati di diagnostica

<!--8,40,55,62-->
Questa proprietà verifica che Windows sia configurato correttamente per consentire i dati di diagnostica. Verifica il valore AllowTelemetry nelle chiavi del Registro di sistema seguente:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

Controllare le autorizzazioni per queste chiavi del Registro di sistema. Assicurarsi che l'account sistema locale possa accedere a queste chiavi al client di Configuration Manager per set. Può anche essere causato da un oggetto Criteri di gruppo in conflitto. Per altre informazioni, vedere [delle impostazioni di Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Per altre informazioni, esaminare M365AHandler.log sul client.  



## <a name="log-files"></a>File di registro

Usare file di log seguenti per risolvere i problemi con Desktop Analitica integrato con Configuration Manager.


### <a name="service-connection-point"></a>punto di connessione del servizio

Sono i seguenti file di log nel punto di connessione del servizio nella directory seguente: `C:\Program Files\Configuration Manager\Logs\M365A`:

| Registro | Descrizione |
|---------|---------|
| **M365ADeploymentPlanWorker.log** | Informazioni sulla sincronizzazione di piano di distribuzione dal Desktop Analitica cloud del servizio per Gestione configurazione locale |
| **M365ADeviceHealthWorker.log** | Informazioni sull'integrità del dispositivo caricare da Configuration Manager in Microsoft cloud |
| **M365AUploadWorker.log** | Informazioni sulla raccolta e dispositivo caricare da Configuration Manager in Microsoft cloud |
| **SmsAdminUI.log** | Informazioni sulle attività della console di Configuration Manager, ad esempio la configurazione dei servizi cloud di Azure  |


### <a name="configuration-manager-client"></a>Client di Configuration Manager

File di log seguenti sono nel client di Configuration Manager nella directory seguente: `C:\Windows\CCM\logs`:

| Registro | Descrizione |
|---------|---------|
| **M365AHandler.log** | Informazioni sui criteri di impostazioni Desktop Analitica |


### <a name="enable-verbose-logging"></a>Abilita la registrazione dettagliata

1. Punto di connessione del servizio, passare alla chiave del Registro di sistema seguente: `HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. Impostare il **LogLevel** valore `0`  
3. (Facoltativo) Eseguire il comando SQL seguente sul database del sito:  

    ```SQL
    DELETE FROM M365AProperties WHERE Name = 'M365ATenantUpdateInfo_LastUpdateTime'
    ```

4. Riavviare il **SMS_EXECUTIVE** servizio nel server del sito



## <a name="bkmk_AzureADApps"></a> Applicazioni di Azure AD

Desktop Analitica aggiunge le seguenti applicazioni in Azure AD:

- **Configuration Manager Microservizio**: Connette Configuration Manager con Analitica Desktop. Questa app non include alcun requisito di accesso.  

- **MALogAnalyticsReader**: Recupera i gruppi di OMS e dispositivi creati in Log Analitica. Per altre informazioni, vedere [ruolo applicazione MALogAnalyticsReader](#bkmk_MALogAnalyticsReader).  

Se è necessario eseguire il provisioning di queste App dopo il completamento di set di backup, andare alla **servizi connessi di** riquadro. Selezionare **configurare l'accesso a utenti e app**ed effettuare il provisioning di App.  

- **App di Azure AD per Configuration Manager**. Se è necessario eseguire il provisioning o risolvere i problemi di connessione dopo il completamento di set di backup, vedere [crea e importa un'app per Configuration Manager](#create-and-import-app-for-configuration-manager). Questa app richiede **scrivere i dati della raccolta CM** e **lettura CM raccolta dati** sul **Configuration Manager Service** API.  


### <a name="create-and-import-app-for-configuration-manager"></a>Creare e importare app for Configuration Manager

Se non è possibile creare questa app di Azure AD dalla procedura guidata Configure Azure Services in Configuration Manager, usare la procedura seguente per creare manualmente e importazione dell'app per Configuration Manager.

#### <a name="create-app-in-azure-ad"></a>Creare app in Azure AD

1. Aprire il [portale di Azure](http://portal.azure.com) come utente con autorizzazioni di amministratore aziendale, passare alla **Azure Active Directory**e selezionare **registrazioni per l'App**. Quindi selezionare **registrazione nuova applicazione**.  

2. Nel **Create** panel, configurare le impostazioni seguenti:  

    - **Nome**: un nome univoco che identifica l'app, ad esempio: `Desktop-Analytics-Connection`  

    - **Tipo di applicazione**: **App Web / API**  

    - **URL Sign-on**: questo valore non è usato da Configuration Manager, ma richiesto da Azure AD. Immettere un URL valido e univoco, ad esempio: `https://configmgrapp`  
  
   Selezionare **Create**.  

3. Selezionare l'app e prendere nota di **ID applicazione**. Questo valore è un GUID che viene usato per configurare la connessione di Configuration Manager.  

4. Selezionare **le impostazioni** relativi all'app e quindi selezionare **chiavi**. Nel **password** , quindi immettere un **descrizione chiave**, specificare una scadenza **durata**e quindi selezionare **Salva**. Copia il **valore** della chiave, che consente di configurare la connessione di Configuration Manager.

    > [!Important]  
    > Questa è l'unica possibilità per copiare il valore della chiave. Se si non copiarlo a questo punto, è necessario creare un'altra chiave.  
    >
    > Salvare il valore della chiave in un luogo sicuro.  

5. Nell'app **le impostazioni** Pannello di selezione **autorizzazioni necessarie**.  

    1. Nel **autorizzazioni necessarie** riquadro, seleziona **Aggiungi**.  

    2. Nel **Aggiungi accesso all'API** pannello **selezionare un'API**.  

    3. Cercare il **Microservizio di Configuration Manager** API. Selezionarlo e quindi scegliere **seleziona**.  

    4. Nel **Abilita accesso** pannello, selezionare entrambe le autorizzazioni applicazione: **Scrivere i dati della raccolta CM** e **leggere i dati della raccolta CM**. Quindi scegliere **seleziona**.  

    5. Nel **Aggiungi accesso all'API** Pannello di selezione **eseguita**.  

6. Nel **autorizzazioni necessarie** pagina, selezionare **concedere le autorizzazioni**. Selezionare **Sì**.  

7. Copiare l'ID tenant di Azure AD. Questo valore è un GUID che viene usato per configurare la connessione di Configuration Manager. Selezionare **Azure Active Directory** nel menu principale e quindi selezionare **proprietà**. Copia il **ID Directory** valore.  

#### <a name="import-app-in-configuration-manager"></a>Importa app in Configuration Manager

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**. Selezionare **configurare i servizi Azure** nella barra multifunzione.  

2. Nel **servizi di Azure** pagina della procedura guidata servizi di Azure, configurare le impostazioni seguenti:  

    - Specificare un **Nome** per l'oggetto in Configuration Manager.  

    - Specificare un parametro facoltativo **Descrizione** per identificare il servizio.  

    - Selezionare **Analitica Desktop** dall'elenco dei servizi disponibili.  
  
   Selezionare **Avanti**.  

3. Nel **App** pagina, selezionare un valore appropriato **ambiente Azure**. Quindi selezionare **importazione** per l'app web. Configurare le impostazioni seguenti nel **Importa le app** finestra:  

    - **Nome del Tenant di Azure AD**: Questo nome è il modo in cui file è denominato in Configuration Manager  

    - **ID Tenant di Azure AD**: Il **ID Directory** copiato da Azure AD  

    - **Client ID** (ID client): Il **ID applicazione** copiato dall'app Azure AD  

    - **Chiave privata**: Il tasto **valore** copiato dall'app Azure AD  

    - **Scadenza della chiave privata**: La stessa data di scadenza della chiave  

    - **URI ID app**: Questa impostazione verranno inseriti automaticamente con il valore seguente: `https://cmmicrosvc.manage.microsoft.com/`  
  
   Selezionare **Verify**, quindi selezionare **OK** per chiudere la finestra di Importa le app. Selezionare **successivo** nella pagina App della procedura guidata servizi di Azure.  

Per continuare il resto della procedura guidata di **dati di diagnostica** pagina, vedere [Connect al servizio](/sccm/desktop-analytics/connect-configmgr#bkmk_connect).

#### <a name="troubleshoot-app-in-configuration-manager"></a>Risolvere i problemi di app in Configuration Manager

Se si verificano problemi creando o importando l'app, verificare innanzitutto **Smsadminui** dell'errore specifico. Quindi verificare le configurazioni seguenti:

- È stato correttamente registrato il tenant per il servizio Desktop Analitica. Per altre informazioni, vedere [come configurare Desktop Analitica](/sccm/desktop-analytics/set-up).

- Gli endpoint sono accessibili tutti necessari. Per altre informazioni, vedere [endpoint](/sccm/desktop-analytics/enable-data-sharing#endpoints).

- Assicurarsi che l'utente che esegue l'accesso disponga delle autorizzazioni corrette. Per altre informazioni, vedere [Prerequisiti](/sccm/desktop-analytics/overview#prerequisites).

- Assicurarsi che l'utente può accedere ad Azure in generale. Questa azione determina se sono presenti AD Azure generale problemi di autenticazione.

- Controllare i messaggi di stato per il **SMS_SERVICE_CONNECTOR** componente per quanto riguarda le *ruolo di lavoro di Analitica Desktop*.


### <a name="bkmk_MALogAnalyticsReader"></a> Ruolo applicazione MALogAnalyticsReader

Quando si configura Desktop Analitica, si accetta un consenso per conto dell'organizzazione. Questo consenso consiste nell'assegnare l'applicazione MALogAnalyticsReader il ruolo di lettura Log Analitica per l'area di lavoro. Questo ruolo applicazione è richiesto dal Desktop Analitica.

Se si verifica un problema con questo processo in set di backup, usare la seguente procedura per aggiungere manualmente questa autorizzazione:

1. Andare alla [portale di Azure](http://portal.azure.com)e selezionare **tutte le risorse**. Selezionare l'area di lavoro di tipo **Log Analitica**.  

2. Nel menu dell'area di lavoro, selezionare **controllo di accesso (IAM)** , quindi selezionare **Add**.  

3. Nel **aggiungere autorizzazioni** panel, configurare le impostazioni seguenti:  

    - **Ruolo**: **Agente di lettura log Analitica**  

    - **Assegna accesso a**: **Utente, gruppo o applicazione AD Azure**  

    - **Selezionare**: **MALogAnalyticsReader**  

4. Selezionare **Salva**.

Il portale visualizzerà il messaggio una notifica che aggiunto l'assegnazione di ruolo.


## <a name="data-latency"></a>Latenza dei dati

<!-- 3846531 -->
Quando si configura prima Analitica Desktop, i report in Configuration Manager e il portale di Analitica Desktop non risultino dati completi sin da subito. Potrebbero essere necessari 2-3 giorni per i dispositivi attivi inviare dati di diagnostica per il servizio di Analitica Desktop, il servizio per elaborare i dati e quindi eseguire la sincronizzazione con il sito di Configuration Manager.

Durante la sincronizzazione di raccolte di dispositivi dalla gerarchia di Configuration Manager per Desktop Analitica, possono volerci fino a 10 minuti per le raccolte da visualizzare nel portale di Analitica Desktop.  Analogamente, quando si crea un piano di distribuzione in Desktop Analitica, possono volerci fino a 10 minuti per le nuove raccolte associati al piano di distribuzione venga visualizzato nella gerarchia di Configuration Manager.  I siti primari creano le raccolte e il sito di amministrazione centrale si sincronizza con Desktop Analitica.

All'interno del portale di Analitica Desktop, esistono due tipi di dati: **I dati dell'amministratore** e **i dati di diagnostica**:

- **I dati dell'amministratore** fa riferimento a qualsiasi modifica apportata alla configurazione dell'area di lavoro.  Ad esempio, quando si modifica un asset **decisioni di aggiornamento** oppure **importanza** si siano modificando i dati dell'amministratore.  Queste modifiche hanno spesso un effetto di composizione, come è possibile modificare lo stato di conformità di un dispositivo con l'asset in questione è installato.

- **I dati di diagnostica** fa riferimento a metadati di sistema caricati dai dispositivi client per Microsoft.  Si tratta dei dati che alimenta Desktop Analitica e includono gli attributi, ad esempio inventario dei dispositivi e sicurezza e funzionalità di aggiornamento dello stato.

Per impostazione predefinita, tutti i dati di Analitica Desktop portale viene automaticamente aggiornato ogni giorno. Questo aggiornamento include modifiche di dati di diagnostica, nonché tutte le modifiche apportate alla configurazione (i dati dell'amministratore) ed è in genere visibile nel portale di Analitica Desktop da 08 12:00:00 AM UTC ogni giorno.

Quando si apportano modifiche per i dati dell'amministratore, si hanno la possibilità di attivare un aggiornamento su richiesta dei dati nell'area di lavoro amministrazione, aprire il menu a comparsa valuta i dati e scegliere "Applicare modifiche".  Questo processo richiede in genere compreso tra 15 e 60 minuti, a seconda della portata delle modifiche che richiedono i processi e le dimensioni dell'area di lavoro.  Si noti che la richiesta di un dati on demand di aggiornamento non comporterà modifiche ai dati di diagnostica.  Per altre informazioni su come richiedere un aggiornamento su richiesta, vedere la pagina Domande frequenti.

Se non è possibile visualizzare le modifiche aggiornate entro gli intervalli di tempo indicati in precedenza, attendere un altro 24 ore il successivo aggiornamento giornaliero. Se viene visualizzato a intervalli più lunghi, controllare il dashboard di integrità del servizio. Se il servizio vengono segnalati come integri, contattare il supporto tecnico Microsoft.<!-- 3896921 -->

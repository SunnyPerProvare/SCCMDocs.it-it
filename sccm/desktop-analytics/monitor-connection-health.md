---
title: Monitorare l'integrità della connessione
titleSuffix: Configuration Manager
description: Informazioni dettagliate su come monitorare lo stato di connessione e gli Stati dei dispositivi per analisi del desktop in Configuration Manager.
ms.date: 06/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1f4e26f7-42f2-40c8-80cf-efd405349c6c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7139175a564ffff50d325daf808e32efb7d3436b
ms.sourcegitcommit: 13ac4f5e600dc1edf69e8566e00968f40e1d1761
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/11/2019
ms.locfileid: "70891776"
---
# <a name="monitor-connection-health"></a>Monitorare l'integrità della connessione

Usare il dashboard di **integrità della connessione** in Configuration Manager per eseguire il drill-down delle categorie in base all'integrità del dispositivo. Nella console di Configuration Manager passare all'area di lavoro **raccolta software** , espandere il nodo **servizio di analisi desktop** e selezionare il dashboard di integrità della **connessione** .  

![Screenshot del dashboard di integrità della connessione Configuration Manager](media/connection-health-dashboard.png)

Quando si configura per la prima volta analisi desktop, è possibile che i grafici non visualizzino dati completi. L'invio dei dati di diagnostica al servizio desktop Analytics da parte dei dispositivi attivi può richiedere 2-3 giorni, il servizio per elaborare i dati e quindi eseguire la sincronizzazione con il sito di Configuration Manager.<!-- 4098037 -->


## <a name="connection-details"></a>Dettagli connessione

In questo riquadro vengono visualizzate le seguenti informazioni di base sulla connessione da Configuration Manager a desktop Analytics:

- **Nome del tenant**: Nome della connessione desktop Analytics nel nodo servizi di **Azure**

- **Raccolta di destinazione**: La stessa *raccolta di destinazione* specificata durante la connessione Configuration Manager a desktop Analytics. Questa raccolta include tutti i dispositivi che Configuration Manager configura con l'ID commerciale e le impostazioni dei dati di diagnostica. Si tratta del set completo di dispositivi che Configuration Manager si connette al servizio desktop Analytics.

- **Dispositivi assegnati**: Tutti i dispositivi nella raccolta di destinazione, meno i tipi di dispositivi seguenti:

    - Rimosso
    - Obsoleto
    - Inattivo
    - Gestito
    - Dispositivi che eseguono versioni del canale di manutenzione a lungo termine (LTSC) di Windows 10
    - Dispositivi che eseguono Windows Server

    Per ulteriori informazioni su questi stati dei dispositivi, vedere [informazioni sullo stato del client](/sccm/core/clients/manage/monitor-clients#bkmk_about).

    > [!Note]  
    > Configuration Manager caricamenti su desktop Analytics tutti i dispositivi nella raccolta di destinazione meno i client rimossi e obsoleti.

- **Dispositivi idonei per da**: Il numero di dispositivi destinati a meno dispositivi non idonei per analisi desktop. Ad esempio, i dispositivi nella raccolta di destinazione che eseguono Windows Server o Windows 10 Long-Term Servicing Channel (LTSC).


## <a name="last-sync-details"></a>Dettagli ultima sincronizzazione

Questo riquadro Mostra quando Configuration Manager esegue la sincronizzazione con il servizio cloud di analisi dei desktop e il numero di dispositivi sincronizzati.

- **Dispositivi sincronizzati**: Il numero di dispositivi univoci che Configuration Manager inviati a analisi desktop. Il servizio include questi dispositivi nello snapshot attualmente visibile.

- **Ultima sincronizzazione del servizio**: Uguale all'ora dell' **Ultimo aggiornamento** nel portale di analisi dei desktop.

- **Successiva sincronizzazione del servizio**: Quando si può prevedere il successivo snapshot giornaliero in desktop Analytics.

> [!Note]  
> La prima volta che si registrano i dispositivi in desktop Analytics, possono essere disponibili diversi giorni per il caricamento e l'elaborazione dei dati. Durante questo periodo, è possibile che il riquadro **Dettagli ultima sincronizzazione** risulti vuoto. Inoltre, nessuno dei valori in questo riquadro viene aggiornato automaticamente quando si richiede uno snapshot su richiesta. Per altre informazioni, vedere [latenza dei dati](/sccm/desktop-analytics/troubleshooting#data-latency).

Se si ritiene che alcuni dispositivi non vengano visualizzati in analisi desktop, verificare che i dispositivi siano supportati da analisi desktop. Per altre informazioni, vedere [Prerequisiti](/sccm/desktop-analytics/overview#prerequisites).


## <a name="connection-health"></a>Stato connessione

Il grafico sull' **integrità della connessione** Visualizza il numero di dispositivi negli Stati di integrità seguenti:  

- [Registrato correttamente](#properly-enrolled): Il dispositivo viene visualizzato in desktop Analytics con un inventario completo
- [Non è possibile eseguire la registrazione](#unable-to-enroll): Si è verificato un problema di blocco che impedisce la registrazione del dispositivo
- [Avviso di configurazione](#configuration-alert): Il dispositivo non viene visualizzato in analisi desktop o viene visualizzato con un inventario incompleto. Configuration Manager inoltre identificato un problema relativo alla registrazione del dispositivo.
- In [attesa di registrazione](#awaiting-enrollment): Configuration Manager configurato il dispositivo, ma non viene ancora visualizzato in desktop Analytics
- [Stato in sospeso](#status-pending): Configuration Manager sta ancora configurando questo dispositivo o non dispone di dati sufficienti dal dispositivo per determinarne lo stato
- [Dati mancanti](#missing-data): Configuration Manager configurato il dispositivo, ma in desktop Analytics sono presenti solo dati parziali

<!-- 
- [Configuration issues](#configuration-issues)  
- [Client not installed](#client-not-installed)  
- [Waiting for enrollment](#waiting-for-enrollment)  
- [Missing prerequisites](#missing-prerequisites)  
 -->

Il numero totale di dispositivi in questo grafico deve corrispondere ai **dispositivi idonei per valore da** nel riquadro dettagli connessione.

Selezionare la sezione nel grafico per eseguire il drill-down in un elenco di dispositivi con tale stato. Per altre informazioni, vedere [elenco dei dispositivi](#device-list).

Selezionare il nome della categoria nella legenda per rimuoverlo o aggiungerlo dal grafico. Questa azione consente di ingrandire il grafico in modo che sia possibile visualizzare le dimensioni relative dei segmenti più piccoli.

### <a name="properly-enrolled"></a>Registrato correttamente

Il dispositivo ha gli attributi seguenti:

- Un client Configuration Manager versione 1902 o successiva  
- Non ci sono errori di configurazione  
- Desktop Analytics ha ricevuto dati di diagnostica completi da questo dispositivo negli ultimi 28 giorni  
- Desktop Analytics ha un inventario completo della configurazione del dispositivo e delle app installate  

### <a name="unable-to-enroll"></a>Non è possibile eseguire la registrazione

Configuration Manager rileva uno o più problemi di blocco che impediscono la registrazione del dispositivo. Per ulteriori informazioni, vedere l'elenco delle [proprietà del dispositivo di analisi desktop in Configuration Manager](#bkmk_config-issues).  

Ad esempio, il client Configuration Manager non è almeno la versione 1902 (5.0.8790). Aggiornare il client alla versione più recente. Prendere in considerazione l'abilitazione dell'aggiornamento client automatico per il sito Configuration Manager. Per altre informazioni, vedere [Aggiornare i client](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  

### <a name="configuration-alert"></a>Avviso di configurazione

Il dispositivo non viene visualizzato in analisi desktop o viene visualizzato con un inventario incompleto. Configuration Manager inoltre identificato un problema relativo alla registrazione del dispositivo. Per ulteriori informazioni, vedere l'elenco delle [proprietà del dispositivo di analisi desktop in Configuration Manager](#bkmk_config-issues).

Ad esempio, il dispositivo non dispone di connettività al servizio. Per ulteriori informazioni, vedere [connettività dell'endpoint di diagnostica Windows](#windows-diagnostic-endpoint-connectivity).

### <a name="awaiting-enrollment"></a>In attesa di registrazione

Desktop Analytics non contiene dati di diagnostica per questo dispositivo. Questo problema può essere dovuto al fatto che il dispositivo è stato aggiunto di recente alla raccolta di destinazione e non ha ancora inviato dati. Può anche significare che il dispositivo non comunica correttamente con il servizio e che i dati di diagnostica più recenti Risaleno a più di 28 giorni prima.

Verificare che il dispositivo sia in grado di comunicare con il servizio. Per ulteriori informazioni, vedere [endpoint](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

### <a name="status-pending"></a>Stato in sospeso

Configuration Manager sta ancora configurando questo dispositivo oppure non dispone di dati sufficienti dal dispositivo per determinarne lo stato.

### <a name="missing-data"></a>Dati mancanti

Configuration Manager configurato correttamente il dispositivo, ma non è possibile creare una valutazione della compatibilità per desktop Analytics. Non dispone di un set di dati completo per la configurazione del dispositivo (Census) o per le app installate (inventario).

Questo problema viene spesso risolto automaticamente quando il dispositivo esegue un nuovo tentativo. Se è permanente, verificare che il dispositivo sia in grado di comunicare con il servizio. Per ulteriori informazioni, vedere [endpoint](/sccm/desktop-analytics/enable-data-sharing#endpoints).  


## <a name="device-list"></a>Elenco dei dispositivi

Per visualizzare un elenco specifico di dispositivi in base allo stato, iniziare con il dashboard di **integrità della connessione** . Selezionare uno dei segmenti del riquadro **integrità connessione** ed eseguire il drill-down in un elenco di dispositivi in questo stato. Per impostazione predefinita, in questa visualizzazione dispositivo personalizzato sono visualizzate le colonne di analisi del desktop seguenti:

- Configurazione ID commerciale
- Aggiornamento di compatibilità minimo
- Consenso esplicito per i dati di diagnostica Windows
- Consenso esplicito per i dati commerciali di Windows
- Connettività endpoint di diagnostica Windows

> [!Note]  
> Ignorare la colonna per la **connettività dell'endpoint di diagnostica Office**. Viene riservato per le funzionalità future.

Queste colonne corrispondono ai [prerequisiti](/sccm/desktop-analytics/overview#prerequisites) principali per i dispositivi per la comunicazione con analisi desktop.

![Screenshot dell'elenco dei dispositivi registrati correttamente](media/sccm-device-list-properly-enrolled.png)

Selezionare un dispositivo per visualizzare l'elenco completo delle proprietà disponibili nel riquadro dei dettagli. È anche possibile aggiungere una di queste proprietà come colonne all'elenco dei dispositivi.


## <a name="bkmk_config-issues"></a>Proprietà del dispositivo

Le seguenti proprietà del dispositivo di analisi desktop sono disponibili come colonne nell'elenco Configuration Manager Device:

- [Configurazione del perito](#appraiser-configuration)  
- [Aggiornamento di compatibilità minimo](#minimum-compatibility-update)  
- [Versione del perito](#appraiser-version)  
- [Ultima esecuzione completa riuscita dell'esperto](#last-successful-full-run-of-appraiser)  
- [Raccolta dati del perito](#appraiser-data-collection)  
- [Ultima esecuzione completa completata del censimento](#last-successful-full-run-of-census)  
- [Raccolta dati del censimento](#census-data-collection)  
- [Connettività endpoint di diagnostica Windows](#windows-diagnostic-endpoint-connectivity)  
- [Controllare i dati di diagnostica dell'utente finale](#check-end-user-diagnostic-data)  
- [Verifica proxy utente](#check-user-proxy)  
- [Configurazione ID commerciale](#commercial-id-configuration)  
- [Consenso esplicito per i dati commerciali di Windows](#windows-commercial-data-opt-in)  
- [Controllare il nome del dispositivo nei dati di diagnostica](#check-device-name-in-diagnostic-data)  
- [Configurazione del servizio DiagTrack](#diagtrack-service-configuration)  
- [Versione di DiagTrack](#diagtrack-version)  
- [Recupero ID SQM](#sqm-id-retrieval)  
- [Recupero identificatore univoco del dispositivo](#unique-device-identifier-retrieval)  
- [Consenso esplicito per i dati di diagnostica Windows](#windows-diagnostic-data-opt-in)  

> [!Note]  
> Ignorare le proprietà per la **connettività degli endpoint di diagnostica di Office** e il **consenso esplicito per i dati di diagnostica Office**. Sono riservati per le funzionalità future.

Il riquadro **più frequenti per gli avvisi di configurazione e i blocchi di registrazione** del dashboard di integrità della connessione Visualizza le proprietà che i dispositivi più spesso segnalano come un problema.

### <a name="appraiser-configuration"></a>Configurazione del perito

<!--20,21-->
Estimator è il componente di Windows che corrisponde agli [aggiornamenti della compatibilità](/sccm/desktop-analytics/enroll-devices#update-devices). Valuta le app e i driver sul dispositivo per la compatibilità con la versione più recente di Windows. 

Se il controllo ha esito positivo, il componente del perito è configurato correttamente nel dispositivo.

In caso contrario, potrebbe essere visualizzato uno degli errori seguenti:

- Non è possibile configurare la raccolta dati di compatibilità delle app per dispositivi (SetRequestAllAppraiserVersions). Controllare i log per i dettagli dell'eccezione  

- Non è possibile configurare la raccolta dati di compatibilità delle app per dispositivi (SetRequestAllAppraiserVersions). Controllare i log per i dettagli dell'eccezione  

- Impossibile scrivere Commercialdataoptin nella chiave `HKLM:\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Appraiser`del registro di sistema. Controllare le autorizzazioni  

Controllare le autorizzazioni per questa chiave del registro di sistema. Verificare che l'account di sistema locale possa accedere a questa chiave per l'impostazione del client di Configuration Manager.  

Per ulteriori informazioni, vedere M365AHandler. log nel client.  

### <a name="minimum-compatibility-update"></a>Aggiornamento di compatibilità minimo

<!--18,19,32-->
L'aggiornamento per la compatibilità (Estimator. dll) non è installato o non è aggiornato nel dispositivo. È precedente al requisito minimo per analisi desktop, 10.0.17763.

Installare l'aggiornamento più recente per la compatibilità. Per ulteriori informazioni, vedere [aggiornamenti della compatibilità](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser).

### <a name="appraiser-version"></a>Versione del perito

Questa proprietà consente di visualizzare la versione corrente del componente Estimator nel dispositivo. Mostra la versione del file in `%windir%\System32\appraiser.dll`, senza i punti decimali. Ad esempio, la versione del file 10.0.17763 viene visualizzata come 10017763.

### <a name="last-successful-full-run-of-appraiser"></a>Ultima esecuzione completa riuscita dell'esperto

Questa proprietà consente di visualizzare la data e l'ora dell'ultima esecuzione corretta del dispositivo.

### <a name="appraiser-data-collection"></a>Raccolta dati del perito

<!--Appraiser run status-->
<!--22,33-->
Questa proprietà Mostra il risultato più recente di Windows che esegue il componente di valutazione.

In caso di esito negativo, potrebbe essere visualizzato uno degli errori seguenti:

- Non è possibile raccogliere i dati di compatibilità delle app (RunAppraiser). Per informazioni dettagliate, vedere i log  

- La raccolta dei dati di compatibilità delle app (CompatTelRunner. exe) è terminata con un codice di errore  

Per ulteriori informazioni, vedere M365AHandler. log nel client.

Verificare la presenza del seguente file `%windir%\System32\CompatTelRunner.exe`:. Se non esiste, reinstallare gli aggiornamenti di [compatibilità](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser)richiesti. Assicurarsi che nessun altro componente di sistema stia rimuovendo questo file, ad esempio criteri di gruppo o un servizio antimalware.

Se il file M365AHandler. log nel client include uno degli errori seguenti:

``` Log
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005
```

Per risolvere questi errori, eseguire i comandi seguenti da una console di Windows PowerShell con privilegi elevati nel client interessato:

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

### <a name="last-successful-full-run-of-census"></a>Ultima esecuzione completa completata del censimento

Questa proprietà consente di visualizzare la data e l'ora dell'ultima esecuzione corretta del dispositivo Census.

### <a name="census-data-collection"></a>Raccolta dati del censimento

<!-- Census run status -->
<!--51,52-->
Census è il componente di Windows per l'inventario del dispositivo. Questi dati di inventario vengono usati per comprendere il dispositivo e la relativa configurazione.

Questa proprietà Mostra il risultato più recente di Windows che esegue il componente Census.

In caso di esito negativo, potrebbe essere visualizzato uno degli errori seguenti:

- Non è possibile raccogliere dati sul dispositivo e la relativa configurazione (RunCensus). Controllare i log per i dettagli dell'eccezione  

- Strumento di raccolta dati di configurazione e dispositivo (devicecensus. exe) non trovato  

Per ulteriori informazioni, vedere M365AHandler. log nel client.

Verificare la presenza del seguente file `%windir%\System32\DeviceCensus.exe`:. Se non esiste, reinstallare gli aggiornamenti di [compatibilità](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser)richiesti. Assicurarsi che nessun altro componente di sistema stia rimuovendo questo file, ad esempio criteri di gruppo o un servizio antimalware.

### <a name="windows-diagnostic-endpoint-connectivity"></a>Connettività endpoint di diagnostica Windows

<!--12,15-->
Se il controllo ha esito positivo, il dispositivo può connettersi all'esperienza utente connessa e all'endpoint di telemetria (vortice).

In caso contrario, potrebbe essere visualizzato uno degli errori seguenti:  

- Non è possibile connettersi all'esperienza utente connessa e all'endpoint di telemetria (vortice). Controllare le impostazioni di rete/proxy  

- Non è possibile verificare la connettività all'esperienza utente connessa e all'endpoint di telemetria (CheckVortexConnectivity). Controllare i log per i dettagli dell'eccezione  

I dispositivi verificano la connettività con una richiesta GET all'endpoint seguente in base alla versione del sistema operativo:

| Versione del sistema operativo | Endpoint |
|------------|----------|
| Windows 10, versione 1803 o successiva con l'aggiornamento cumulativo più recente | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Windows 10, versione 1803 o successiva senza l'aggiornamento cumulativo 2018-09 o successivo | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10, versione 1709 o versioni precedenti | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 o Windows 8.1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

Verificare che il dispositivo sia in grado di comunicare con il servizio. Questo controllo convalida alcuni ma non tutti gli endpoint richiesti. Per ulteriori informazioni, vedere [endpoint](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

Per ulteriori informazioni, vedere M365AHandler. log nel client.  

### <a name="check-end-user-diagnostic-data"></a>Controllare i dati di diagnostica dell'utente finale

<!--1004-->
Se la verifica ha esito negativo, un utente ha selezionato i dati di diagnostica Windows più bassi sul dispositivo. Può anche essere causato da un oggetto Criteri di gruppo in conflitto. Per ulteriori informazioni, vedere [impostazioni di Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).

A seconda dei requisiti aziendali, è possibile disabilitare la scelta dell'utente tramite criteri di gruppo. Usare l'impostazione per **configurare il consenso esplicito per la telemetria impostazione dell'interfaccia utente**. Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management) (Configurare i dati di diagnostica di Windows nell'organizzazione).

### <a name="check-user-proxy"></a>Verifica proxy utente

<!--30,35-->
L'impostazione DisableEnterpriseAuthProxy è abilitata per impostazione predefinita per Windows 7. Per Windows 8.1 computer, Configuration Manager imposta l'impostazione DisableEnterpriseAuthProxy su 0 (non disabilitata).

Questa proprietà può visualizzare gli errori seguenti:

- Il proxy di autenticazione è abilitato. Impostare DisableEnterpriseAuthProxy su 0 in`HKLM\Software\Policies\Microsoft\Windows\DataCollection`

- Non è possibile verificare lo stato del proxy di autenticazione. Controllare i log per i dettagli dell'eccezione

Per ulteriori informazioni, vedere M365AHandler. log nel client.  

Controllare le autorizzazioni per questa chiave del registro di sistema. Verificare che l'account di sistema locale possa accedere a questa chiave per l'impostazione del client di Configuration Manager. Può anche essere causato da un oggetto Criteri di gruppo in conflitto. Per ulteriori informazioni, vedere [impostazioni di Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

### <a name="commercial-id-configuration"></a>Configurazione ID commerciale

<!--9, 11, 53-->
Microsoft usa un ID commerciale univoco per eseguire il mapping delle informazioni dai dispositivi all'area di lavoro di analisi del desktop. Quando si integra Configuration Manager con l'analisi del desktop, viene automaticamente eseguita una query sul servizio per questo ID. Configuration Manager deve applicare automaticamente questo ID ai client a cui sono destinate le impostazioni di analisi del desktop.

Se il controllo ha esito positivo, il dispositivo viene configurato correttamente con un ID commerciale.

In caso contrario, potrebbe essere visualizzato uno degli errori seguenti:

- Impossibile scrivere la chiave commercializzata nella chiave `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`del registro di sistema. Controllare le autorizzazioni  

- Non è possibile aggiornare la chiave `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`del registro di sistema commercializzata. Controllare i log per i dettagli dell'eccezione  

- Specificare il valore commercializzato corretto in`HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`  

Per ulteriori informazioni, vedere M365AHandler. log nel client.  

Controllare le autorizzazioni per questa chiave del registro di sistema. Verificare che l'account di sistema locale possa accedere a questa chiave per l'impostazione del client di Configuration Manager. Può anche essere causato da un oggetto Criteri di gruppo in conflitto. Per ulteriori informazioni, vedere [impostazioni di Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

È disponibile un ID diverso per il dispositivo. Questa chiave del registro di sistema viene utilizzata da criteri di gruppo. Ha la precedenza sull'ID fornito da Configuration Manager.  

<a name="bkmk_ViewCommercialID"></a>Per visualizzare l'ID commerciale nel portale di analisi dei desktop, seguire questa procedura:

1. Passare al portale di analisi del desktop e selezionare **servizi connessi** nel gruppo impostazioni globali.  

2. Nel riquadro **servizi connessi** il riquadro **registra dispositivi** è selezionato per impostazione predefinita. Nel riquadro Registrazione dispositivi, nella sezione informazioni viene visualizzata la chiave ID commerciale.  

![Screenshot dell'ID commerciale nel portale di analisi dei desktop](media/commercial-id.png)

> [!Important]  
> **Ottenere la nuova chiave ID** solo quando non è possibile usare quella corrente. Se si rigenera l'ID commerciale, [registrare nuovamente i dispositivi con il nuovo ID](/sccm/desktop-analytics/enroll-devices#device-enrollment). Questo processo potrebbe causare la perdita di dati di diagnostica durante la transizione.  

### <a name="windows-commercial-data-opt-in"></a>Consenso esplicito per i dati commerciali di Windows

<!--64-->
Questa proprietà è specifica per i dispositivi che eseguono Windows 7 o Windows 8.1. Esegue test simili come [consenso esplicito](#windows-diagnostic-data-opt-in)per i dati di diagnostica di Windows, ad eccezione del valore e.

### <a name="check-device-name-in-diagnostic-data"></a>Controllare il nome del dispositivo nei dati di diagnostica

<!--56,58-->
Se il controllo ha esito positivo, il dispositivo è configurato correttamente per condividere il nome del dispositivo.

In caso contrario, potrebbe essere visualizzato uno degli errori seguenti:

- Non è possibile verificare il nome del dispositivo da inviare a Microsoft come parte dei dati di diagnostica di Windows. Controllare i log per i dettagli dell'eccezione  

- Impossibile scrivere AllowDeviceNameInTelemetry nella chiave `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`del registro di sistema. Controllare le autorizzazioni  

Per ulteriori informazioni, vedere M365AHandler. log nel client.  

Controllare le autorizzazioni per questa chiave del registro di sistema. Verificare che l'account di sistema locale possa accedere a questa chiave per l'impostazione del client di Configuration Manager. Può anche essere causato da un oggetto Criteri di gruppo in conflitto. Per ulteriori informazioni, vedere [impostazioni di Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Assicurarsi che un altro meccanismo dei criteri, ad esempio criteri di gruppo, non disabilita questa impostazione.

### <a name="diagtrack-service-configuration"></a>Configurazione del servizio DiagTrack

<!--44,45,50-->
Se il controllo ha esito positivo, il componente DiagTrack è configurato correttamente nel dispositivo. La versione minima richiesta da desktop Analytics è 10010586 (10.0.10586).

In caso contrario, potrebbe essere visualizzato uno degli errori seguenti:

- L'esperienza utente connessa e il componente di telemetria (diagtrack. dll) non sono aggiornati. Verificare i requisiti  

- Non è possibile trovare il componente esperienza utente connessa e telemetria (diagtrack. dll). Verificare i requisiti  

- Abilitare e avviare le esperienze utente connesse e il servizio di telemetria per inviare i dati a Microsoft  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

Installare gli aggiornamenti più recenti. Per ulteriori informazioni, vedere [aggiornamenti del dispositivo](/sccm/desktop-analytics/enroll-devices#update-devices).

Assicurarsi che l' **esperienza utente connessa e il servizio di telemetria** sul dispositivo siano in esecuzione.

### <a name="diagtrack-version"></a>Versione di DiagTrack

Questa proprietà Visualizza la versione corrente dell'esperienza utente connessa e del componente di telemetria nel dispositivo. Mostra la versione del file in `%windir%\System32\diagtrack.dll`, senza i punti decimali. Ad esempio, la versione del file 10.0.10586 viene visualizzata come 10010586.

### <a name="sqm-id-retrieval"></a>Recupero ID SQM

<!--38-->
Questa proprietà è principalmente per i dispositivi Windows 7. Può essere usato da versioni successive del sistema operativo come un identificatore di fallback per il dispositivo.

Se l'operazione non riesce, è possibile che venga visualizzato l'errore seguente:

- Non è possibile recuperare l'identificatore di telemetria del dispositivo legacy (ID SQM)

Per ulteriori informazioni, vedere M365AHandler. log nel client.  

Assicurarsi che non siano presenti ID duplicati nell'ambiente in uso. Ad esempio, se i dispositivi sono stati distribuiti con un'immagine del sistema operativo non generalizzata.

### <a name="unique-device-identifier-retrieval"></a>Recupero identificatore univoco del dispositivo

<!--54-->
Desktop Analytics usa il servizio account Microsoft per un'identità del dispositivo più affidabile.

Verificare che il servizio **Assistente per l'accesso all'account Microsoft** non sia disabilitato. Il tipo di avvio deve essere **manuale (avvio trigger)** .

Per disabilitare l'accesso account Microsoft all'utente finale, utilizzare le impostazioni dei criteri anziché bloccare l'endpoint. Per ulteriori informazioni, vedere [la account Microsoft nell'azienda](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication).

### <a name="windows-diagnostic-data-opt-in"></a>Consenso esplicito per i dati di diagnostica Windows

<!--8,40,55,62-->
Questa proprietà controlla che Windows sia configurato correttamente per consentire i dati di diagnostica. Verifica il valore AllowTelemetry nelle seguenti chiavi del registro di sistema:

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

Controllare le autorizzazioni per queste chiavi del registro di sistema. Verificare che l'account di sistema locale sia in grado di accedere a queste chiavi affinché il client di Configuration Manager imposti. Può anche essere causato da un oggetto Criteri di gruppo in conflitto. Per ulteriori informazioni, vedere [impostazioni di Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Per ulteriori informazioni, vedere M365AHandler. log nel client.  



## <a name="see-also"></a>Vedere anche

[Risolvere i problemi di Desktop Analytics](/sccm/desktop-analytics/troubleshooting)

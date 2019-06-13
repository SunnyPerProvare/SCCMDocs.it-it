---
title: Registrare i dispositivi in Desktop Analitica
titleSuffix: Configuration Manager
description: Informazioni su come registrare i dispositivi in Desktop Analitica.
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: bec55b8da942750af78b1d3ce01c8a01a9d13a6c
ms.sourcegitcommit: e3c1eb0b75d79c05a750d49354c851d15d5e26a3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/13/2019
ms.locfileid: "67038752"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>Come registrare i dispositivi in Desktop Analitica

> [!Note]  
> Tali informazioni fanno riferimento a un servizio in anteprima che può essere modificato sostanzialmente prima del rilascio in commercio. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

Quando si [connettere Configuration Manager](/sccm/desktop-analytics/connect-configmgr) per Desktop Analitica, configurare le impostazioni per registrare i dispositivi Desktop Analitica. È possibile modificare queste impostazioni in qualsiasi momento. Assicurarsi anche che i dispositivi siano aggiornati.



## <a name="update-devices"></a>Aggiornare i dispositivi

Esistono due tipi di aggiornamenti che è necessario applicare per ottenere risultati ottimali con Analitica Desktop:

- [Aggiornamenti per la compatibilità](#bkmk_appraiser)  
- [Servizio dati di telemetria ed esperienze utente connesso](#bkmk_diagtrack)


### <a name="bkmk_appraiser"></a> Aggiornamenti per la compatibilità

Il componente di compatibilità (Appraiser) viene eseguita la diagnostica nel dispositivo Windows per valutare lo stato di compatibilità con le versioni più recenti di Windows 10.

Microsoft incrementa regolarmente gli aggiornamenti per questo componente, ma non modifica il numero di Knowledge Base associato. Assicurarsi di avere sempre la versione più recente dell'aggiornamento.

Riavviare i dispositivi dopo aver installato gli aggiornamenti di compatibilità per la prima volta.

> [!Tip]  
> Usare Configuration Manager per installare automaticamente la versione più recente di questi aggiornamenti. Per altre informazioni, vedere [Distribuire gli aggiornamenti software](/sccm/sum/deploy-use/deploy-software-updates).  

> [!Note]  
> Un aggiornamento facoltativo correlati, [3150513 KB](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=3150513). Questo aggiornamento fornisce l'aggiornamento della configurazione e le definizioni per gli aggiornamenti di compatibilità precedenti. Per altre informazioni, vedere [aggiornamento definizione di compatibilità più recente di Windows](https://support.microsoft.com/help/3150513).  

#### <a name="windows-10"></a>Windows 10

Windows 10 include il componente di compatibilità. Per ottenere l'aggiornamento di compatibilità più recente, installare l'aggiornamento cumulativo più recente di Windows 10.

#### <a name="windows-81"></a>Windows 8.1

Scaricare l'aggiornamento: [KB 2976978](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2976978) 

Viene eseguita la diagnostica nei sistemi Windows 8.1 che fanno parte di Windows programma Analisi utilizzo software. Questi dati diagnostici consentono di determinare se si potrebbero avere problemi di compatibilità durante l'aggiornamento a Windows 10.

Per altre informazioni, vedere [Compatibility update per mantenere aggiornate in Windows 8.1 Windows](https://support.microsoft.com/help/2976978).

#### <a name="windows-7-with-service-pack-1"></a>Windows 7 con Service Pack 1

Scaricare l'aggiornamento: [KB 2952664](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2952664) 

Viene eseguita la diagnostica di Windows 7 con i sistemi di Service Pack 1 (SP1) che fanno parte di Windows programma Analisi utilizzo software. Questi dati diagnostici consentono di determinare se si potrebbero avere problemi di compatibilità durante l'aggiornamento a Windows 10.

Per altre informazioni, vedere [Compatibility update per mantenere aggiornati Windows 7, Windows](https://support.microsoft.com/help/2952664).


### <a name="bkmk_diagtrack"></a> Servizio dati di telemetria ed esperienze utente connesso

Con dati di diagnostica Windows abilitati, il servizio esperienze utente connesse e telemetria (DiagTrack) raccoglie i dati di sistema, l'applicazione e del driver. Microsoft analizza i dati e lo condivide all'utente tramite Desktop Analitica.

Per risultati ottimali, installare gli aggiornamenti seguenti in base alla versione del sistema operativo.

> [!Note]  
> Quando si installano questi aggiornamenti, prevede che i comportamenti seguenti:
> 
> - I dispositivi che si registrano per Desktop Analitica visualizzati nel servizio in meno di un'ora  
> - I dispositivi segnalano rapidamente lo stato per gli aggiornamenti qualitativi e delle funzionalità di Windows  
>
> Senza questi aggiornamenti, questi processi possono richiedere in 48 ore per un dispositivo segnalare al Desktop Analitica.  


#### <a name="windows-10"></a>Windows 10

Installare l'aggiornamento cumulativo più recente di Windows 10.

<!-- 
- Windows 10 1809: Included in RTM build
- Windows 10 1803: [KB4458469](https://support.microsoft.com/help/4458469) (OS Build 17134.319)
- Windows 10 1709: [KB4457136](https://support.microsoft.com/help/4457136) (OS Build 16299.697)
- Windows 10 1703: [KB4457141](https://support.microsoft.com/help/4457141) (OS Build 15063.1358)
- Windows 10 1607: [KB4457127](https://support.microsoft.com/help/4457127) (OS Build 14393.2517)
 -->

#### <a name="windows-81"></a>Windows 8.1

Installare l'aggiornamento cumulativo mensile ottobre 2018, [KB4462926](https://support.microsoft.com/help/4462926)

#### <a name="windows-7"></a>Windows 7

Installare l'aggiornamento cumulativo mensile ottobre 2018, [KB4462923](https://support.microsoft.com/help/4462923)



## <a name="device-enrollment"></a>Registrazione del dispositivo

Il servizio di Analitica Desktop non presenta nessuna agenti da installare. Registrazione del dispositivo richiede la configurazione delle impostazioni nei dispositivi di cui che si desidera monitorare. Queste impostazioni consentono di controllare a quale istanza di Analitica Desktop il dispositivo deve inviare i dati e altre opzioni di configurazione.

> [!Note]  
> Se si usa già Windows Analitica, usare la stessa area di lavoro per Desktop Analitica. È necessario ripetere la registrazione ai dispositivi di Analitica Desktop che sono registrati in precedenza in Analitica di Windows.
>
> È possibile avere solo un'area di lavoro di Analitica Desktop per ogni tenant di Azure AD. Dispositivi possono inviare solo i dati di diagnostica a un'area di lavoro.  

Configuration Manager offre un'esperienza integrata per la gestione e distribuzione di queste impostazioni ai client. Per risultati ottimali, usare Configuration Manager.

Quando ci si connette Configuration Manager per Desktop Analitica, configurare le impostazioni per registrare i dispositivi. Per altre informazioni, vedere [come connettere Configuration Manager con Desktop Analitica](/sccm/desktop-analytics/connect-configmgr#bkmk_connect).

Per modificare queste impostazioni, usare la procedura seguente:

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**. Selezionare la connessione al Desktop Analitica e scegliere **proprietà** nella barra multifunzione.

2. Nel **dati di diagnostica** pagina, apportare le modifiche necessarie per le impostazioni seguenti:  

    - **ID commerciale**: questo valore verranno inseriti automaticamente con l'ID. dell'organizzazione Se non, assicurarsi che il server proxy sia configurato per consentire tutti obbligatori [endpoint](/sccm/desktop-analytics/enable-data-sharing#endpoints) prima di continuare. In alternativa, recuperare l'ID commerciale manualmente tramite il [portale Analitica Desktop](/sccm/desktop-analytics/monitor-connection-health#bkmk_ViewCommercialID).   

    - **A livello di dati di diagnostica di Windows 10**: Per altre informazioni, vedere [livelli di dati di diagnostica](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  

    - **Consente il nome di dispositivo nei dati di diagnostica**: Per altre informazioni, vedere [nome dispositivo](#device-name).  

    Quando si apportano modifiche a questa pagina, il **funzionalità disponibili** pagina viene visualizzata un'anteprima della funzionalità Desktop Analitica con le impostazioni di dati di diagnostica selezionato.  

3. Nel **Desktop Analitica connessione** pagina, apportare le modifiche necessarie per le impostazioni seguenti:

    - **Nome visualizzato**: Il portale di Analitica Desktop Visualizza questa connessione di Configuration Manager usando questo nome.  

    - **Raccolta di destinazione**: Questa raccolta include tutti i dispositivi che consente di configurare Configuration Manager con l'ID commerciale e le impostazioni di dati di diagnostica. È il set completo di dispositivi che Configuration Manager si connette al servizio Analitica Desktop.  

    - **I dispositivi nella raccolta di destinazione usano un proxy con autenticazione utente per le comunicazioni in uscita**: Per impostazione predefinita, questo valore è **No**. Se necessario nell'ambiente in uso, impostato su **Sì**. Per altre informazioni, vedere [autenticazione del server Proxy](/sccm/desktop-analytics/enable-data-sharing#proxy-server-authentication).  

    - **Selezionare le raccolte specifiche da sincronizzare con Desktop Analitica**: Selezionare **Add** raccolte aggiuntive da includere le **raccolta di destinazione** gerarchia. Queste raccolte sono disponibili nel portale di Analitica Desktop per il raggruppamento con piani di distribuzione. Assicurarsi di includere raccolte di esclusioni pilota e pilota.  <!-- 4097528 -->

        > [!Important] 
        > Queste raccolte comunque eseguita la sincronizzazione le modifiche all'appartenenza. Ad esempio, il piano di distribuzione Usa una raccolta con una regola di appartenenza a Windows 7. Come aggiornare i dispositivi a Windows 10 e Configuration Manager valuta l'appartenenza alla raccolta, tali dispositivi eliminare esplicitamente la raccolta e un piano di distribuzione.  


### <a name="windows-settings"></a>Impostazioni di Windows

Configuration Manager imposta le impostazioni di Windows seguenti in `Microsoft\Windows\DataCollection`:

| Criteri   | Valore  |
|----------|--------|
| **CommercialId** | Affinché un dispositivo da visualizzare nel Desktop Analitica, configurarlo con l'ID commerciale. dell'organizzazione |
| **AllowTelemetry**  | Impostare `1` per **base**, `2` per **avanzato**, oppure `3` per **completo** i dati di diagnostica. Analitica desktop richiede almeno base dei dati di diagnostica. Microsoft consiglia di utilizzare il livello avanzato (limitato) con Desktop Analitica. Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization) (Configurare i dati di diagnostica di Windows nell'organizzazione). |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | *Si applica a Windows 10, versione 1709 e successive*: Questa impostazione si applica solo quando l'impostazione AllowTelemetry `2`. Limita gli eventi di dati di diagnostica avanzata inviati a Microsoft solo gli eventi necessari per Desktop Analitica. Per altre informazioni, vedere [Windows 10, versione 1709 migliorato gli eventi di dati di diagnostica e i campi usati da Windows Analitica](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields).|
| **AllowDeviceNameInTelemetry** | *Si applica a Windows 10, versione 1803 e versioni successive*: È necessario un consenso esplicito aggiuntivo separato per consentire ai dispositivi di continuare a inviare il nome del dispositivo.<br> <br>Nota: Per impostazione predefinita, il nome del dispositivo non viene inviato a Microsoft. Se si non invia il nome del dispositivo, viene visualizzata nel Desktop Analitica come "Sconosciuto". Questo comportamento può rendere difficile identificare e valutare i dispositivi. Per altre informazioni, vedere [nome dispositivo](#device-name). |
| **CommercialDataOptIn** | *Si applica a Windows 7 e Windows 8.1*: Un valore di `1` è necessaria per Desktop Analitica. Per altre informazioni, vedere [Opt-in dati commerciali in Windows 7](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)). |

Visualizzare queste impostazioni in editor Criteri di gruppo nel percorso seguente: **Configurazione computer** > **modelli amministrativi** > **componenti di Windows** > **dati raccolta e anteprima Compila**.

> [!Important]  
> Nella maggior parte dei casi, usare solo Configuration Manager per configurare queste impostazioni. Non si applicano anche queste impostazioni negli oggetti Criteri di gruppo di dominio. Per altre informazioni, vedere [risoluzione dei conflitti](#conflict-resolution).<!-- SCCMDocs-pr 3120 -->

### <a name="device-name"></a>Nome del dispositivo

A partire da Windows 10, versione 1803, il nome del dispositivo non è più raccolte per impostazione predefinita. La raccolta il nome del dispositivo con i dati di diagnostica richiede un consenso esplicito aggiuntivo separato. Senza il nome del dispositivo, è più difficile per identificare quali dispositivi richiedono attenzione durante la valutazione dell'aggiornamento a una nuova versione di Windows.

Se si non invia il nome del dispositivo, viene visualizzata nel Desktop Analitica come "Sconosciuto".

![Elenco dei dispositivi Analitica desktop contenente i nomi di "sconosciuti"](media/unknown-device-name.png)

È disponibile un'opzione nelle impostazioni di Configuration Manager per Desktop Analitica configurare questa opzione: **Consente il nome di dispositivo nei dati di diagnostica**. Questa impostazione di Configuration Manager Controlla l'impostazione di criteri di Windows, AllowDeviceNameInTelemetry.
 

### <a name="conflict-resolution"></a>risoluzione dei conflitti

In generale, usare le raccolte di Configuration Manager di registrazione e le impostazioni di Desktop Analitica di destinazione. Utilizzare l'appartenenza diretta o query per includere o escludere i dispositivi dalla raccolta. Per altre informazioni, vedere [Come creare le raccolte](/sccm/core/clients/manage/collections/create-collections).

Configuration Manager Configura le impostazioni di Windows solo se un valore non esiste già. Se è necessario configurare impostazioni diverse per un gruppo di dispositivi univoco, è possibile usare [criteri di gruppo](#windows-settings). Destinata dei criteri di gruppo impostazioni avranno precedenza sulle impostazioni di Configuration Manager.

Se la destinazione è il client di Configuration Manager con le impostazioni di Windows Analitica e Analitica Desktop, le impostazioni per Desktop Analitica hanno la precedenza.

Quando si configura il livello di dati di diagnostica, impostare il limite massimo per il dispositivo. Per impostazione predefinita in Windows 10, versione 1803 e versioni successive, gli utenti possono scegliere di impostare un livello inferiore. È possibile controllare questo comportamento usando l'impostazione di criteri di gruppo **interfaccia utente di acconsentire esplicitamente impostazione dati di telemetria configura**. Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management) (Configurare i dati di diagnostica di Windows nell'organizzazione).



## <a name="next-steps"></a>Passaggi successivi

Passare all'articolo successivo per creare piani di distribuzione in Desktop Analitica.
> [!div class="nextstepaction"]  
> [Creare piani di distribuzione](/sccm/desktop-analytics/create-deployment-plans)  

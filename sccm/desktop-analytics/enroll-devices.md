---
title: Registrare i dispositivi in Desktop Analytics
titleSuffix: Configuration Manager
description: Informazioni su come registrare i dispositivi in Desktop Analytics.
ms.date: 10/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2df4fb22c69f81a6a9fa0ac431ecdb62ac22c9bc
ms.sourcegitcommit: ccc3c929b5585c05d562020e68044de7d7e11c6a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/02/2020
ms.locfileid: "80597332"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>Come registrare i dispositivi in Desktop Analytics

Quando si connette [Configuration Manager](/sccm/desktop-analytics/connect-configmgr) a Desktop Analytics, si configurano le impostazioni per registrare i dispositivi in Desktop Analytics. È possibile modificare queste impostazioni in qualsiasi momento. Assicurarsi anche che i dispositivi siano aggiornati.



## <a name="update-devices"></a>Aggiornare i dispositivi

Sono disponibili due tipi di aggiornamento che è necessario applicare per un'esperienza ottimale con Desktop Analytics:

- [Aggiornamenti per la compatibilità](#bkmk_appraiser)  
- [Esperienze utente connesse e telemetria](#bkmk_diagtrack)


### <a name="compatibility-updates"></a><a name="bkmk_appraiser"></a> Aggiornamenti per la compatibilità

Il componente per la compatibilità (strumento di valutazione) esegue la diagnostica sul dispositivo Windows per valutarne lo stato di compatibilità con le versioni più recenti di Windows 10.

Microsoft incrementa regolarmente gli aggiornamenti per questo componente, ma il numero di KB associato non cambia. Assicurarsi di avere sempre la versione più recente dell'aggiornamento.

Riavviare i dispositivi dopo aver installato gli aggiornamenti per la compatibilità per la prima volta.

> [!Tip]  
> Usare Configuration Manager per installare automaticamente la versione più recente degli aggiornamenti. Per altre informazioni, vedere [Distribuire gli aggiornamenti software](/sccm/sum/deploy-use/deploy-software-updates).  

> [!Note]  
> È disponibile un aggiornamento facoltativo correlato, [KB 3150513](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=3150513). Questo aggiornamento offre la configurazione aggiornata e le definizioni per gli aggiornamenti per la compatibilità precedenti. Per altre informazioni, vedere [Aggiornamento della definizione di compatibilità più recente per Windows](https://support.microsoft.com/help/3150513).  

#### <a name="windows-10"></a>Windows 10

Windows 10 include il componente per la compatibilità. Per ottenere l'aggiornamento per la compatibilità più recente, installare l'aggiornamento cumulativo più recente di Windows 10.

#### <a name="windows-81"></a>Windows 8.1

Scaricare l'aggiornamento: [KB 2976978](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2976978) 

Esegue la diagnostica nei sistemi Windows 8.1 che partecipano all'Analisi utilizzo software Windows. La diagnostica consente di determinare se è possibile che si verifichino problemi di compatibilità durante l'aggiornamento a Windows 10.

Per altre informazioni, vedere [Aggiornamento di compatibilità per mantenere Windows aggiornato in Windows 8.1](https://support.microsoft.com/help/2976978).

#### <a name="windows-7-with-service-pack-1"></a>Windows 7 con Service Pack 1

Scaricare l'aggiornamento: [KB 2952664](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2952664) 

Esegue la diagnostica nei sistemi Windows 7 con Service Pack 1 (SP1) che partecipano all'Analisi utilizzo software Windows. La diagnostica consente di determinare se è possibile che si verifichino problemi di compatibilità durante l'aggiornamento a Windows 10.

Per altre informazioni, vedere [Aggiornamento di compatibilità per mantenere Windows aggiornato in Windows 7](https://support.microsoft.com/help/2952664).


### <a name="connected-user-experiences-and-telemetry-service"></a><a name="bkmk_diagtrack"></a> Esperienze utente connesse e telemetria

Con i dati di diagnostica di Windows abilitati, Esperienze utente connesse e telemetria (DiagTrack) raccoglie i dati del sistema, dell'applicazione e del driver. Microsoft analizza i dati e li condivide nuovamente con l'utente tramite Desktop Analytics.

Per un'esperienza ottimale, installare gli aggiornamenti seguenti in base alla versione del sistema operativo.

> [!Note]  
> Quando si installano questi aggiornamenti, prevedere i comportamenti seguenti:
> 
> - I dispositivi registrati in Desktop Analytics vengono visualizzati nel servizio in meno di un'ora  
> - I dispositivi visualizzano rapidamente lo stato degli aggiornamenti di qualità e funzionalità di Windows  
>
> Senza questi aggiornamenti, questi processi possono richiedere più di 48 ore prima che un dispositivo visualizzi i dati in Desktop Analytics.  


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

Installare il rollup mensile di ottobre 2018, [KB4462926](https://support.microsoft.com/help/4462926)

#### <a name="windows-7"></a>Windows 7

Installare il rollup mensile di ottobre 2018, [KB4462923](https://support.microsoft.com/help/4462923)



## <a name="device-enrollment"></a>Registrazione del dispositivo

Il servizio Desktop Analytics non ha agenti da installare. Per la registrazione del dispositivo è necessario configurare le impostazioni nei dispositivi che si vuole monitorare. Queste impostazioni controllano l'istanza di Desktop Analytics a cui il dispositivo deve inviare i dati e altre opzioni di configurazione.

> [!Note]  
> Se in precedenza si usava Windows Analytics, usare la stessa area di lavoro per Desktop Analytics. È necessario registrare nuovamente in Desktop Analytics i dispositivi che sono stati precedentemente registrati in Windows Analytics.
>
> È possibile avere solo un'area di lavoro di Desktop Analytics per ogni tenant di Azure AD. I dispositivi possono inviare i dati di diagnostica solo a un'area di lavoro.  

Configuration Manager offre un'esperienza integrata per la gestione e la distribuzione di queste impostazioni ai client. Per un'esperienza ottimale, usare Configuration Manager.

Quando si connette Configuration Manager a Desktop Analytics, si configurano le impostazioni per registrare i dispositivi. Per altre informazioni, vedere [Come connettere Configuration Manager a Desktop Analytics](/sccm/desktop-analytics/connect-configmgr#bkmk_connect).

Per modificare le impostazioni, seguire questa procedura:

1. Nell'area di lavoro **Amministrazione** della console di Configuration Manager espandere **Servizi cloud** e selezionare il nodo **Servizi di Azure**. Selezionare la connessione a Desktop Analytics e scegliere **Proprietà** nella barra multifunzione.

2. Nella pagina **Dati di diagnostica** apportare le modifiche necessarie alle impostazioni seguenti:  

    - **ID commerciale**: questo valore deve essere popolato automaticamente con l'ID dell'organizzazione. In caso contrario, assicurarsi che il server proxy sia configurato in modo da consentire tutti gli [endpoint](/sccm/desktop-analytics/enable-data-sharing#endpoints) necessari prima di continuare. In alternativa, recuperare manualmente l'ID commerciale dal [portale di Desktop Analytics](/sccm/desktop-analytics/monitor-connection-health#bkmk_ViewCommercialID).   

    - **Livello dei dati di diagnostica di Windows 10**: Per altre informazioni, vedere [Livelli dei dati di diagnostica](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  

    - **Consenti il nome del dispositivo nei dati di diagnostica**: Per altre informazioni, vedere [Nome del dispositivo](#device-name).  

    Quando si apportano modifiche a questa pagina, la pagina **Funzionalità disponibili** visualizza un'anteprima delle funzionalità di Desktop Analytics con le impostazioni dei dati di diagnostica selezionate.  

3. Nella pagina **Connessione di Desktop Analytics** apportare le modifiche necessarie alle impostazioni seguenti:

    - **Nome visualizzato**: Il portale di Desktop Analytics visualizza questa connessione a Configuration Manager usando questo nome.  

    - **Raccolta di destinazione**: Questa raccolta include tutti i dispositivi che Configuration Manager configura con l'ID commerciale e le impostazioni dei dati di diagnostica. Si tratta del set completo di dispositivi che Configuration Manager connette al servizio Desktop Analytics.  

    - **I dispositivi nella raccolta di destinazione usano un proxy autenticato dall'utente per le comunicazioni in uscita**: Per impostazione predefinita, questo valore è **No**. Se necessario nell'ambiente in uso, impostare su **Sì**. Per altre informazioni, vedere [Autenticazione dei server proxy](/sccm/desktop-analytics/enable-data-sharing#proxy-server-authentication).  

    - **Selezionare raccolte specifiche da sincronizzare con Desktop Analytics**: Selezionare **Aggiungi** per inserire ulteriori raccolte della gerarchia **Raccolta di destinazione**. Queste raccolte sono disponibili nel portale di Desktop Analytics per il raggruppamento con i piani di distribuzione. Assicurarsi di includere le raccolte pilota e di esclusioni pilota.  <!-- 4097528 -->

        > [!Important] 
        > Queste raccolte continuano a essere sincronizzate quando viene modificata l'appartenenza. Il piano di distribuzione, ad esempio, usa una raccolta con una regola di appartenenza di Windows 7. Quando i dispositivi eseguono l'aggiornamento a Windows 10 e Configuration Manager valuta l'appartenenza alla raccolta, i dispositivi escono dalla raccolta e dal piano di distribuzione.  


### <a name="windows-settings"></a>Impostazioni di Windows

Configuration Manager imposta i criteri di Windows in una o in entrambe le chiavi del Registro di sistema seguenti:

- **GPO**: `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

- Preferenza **Criteri locali**: `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`

| Criteri   | Percorso | Valore  | 
|----------|------|--------|
| **CommercialId** | Criteri locali | *Si applica a Windows 7, Windows 8.1 e Windows 10*: Per consentire la visualizzazione di un dispositivo in Desktop Analytics, configurarlo con l'ID commerciale dell'organizzazione. | 
| **AllowTelemetry**  | GPO (Oggetto Criteri di gruppo) | *Si applica a Windows 10*: Impostare `1` per dati di diagnostica **Base**, `2` per dati di diagnostica **Avanzato** o `3` per dati di diagnostica **Completo**. Per Desktop Analytics sono necessari almeno i dati di diagnostica di base. Microsoft consiglia di usare il livello Avanzata (con limitazioni) con Desktop Analytics. Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization) (Configurare i dati di diagnostica di Windows nell'organizzazione). |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | GPO (Oggetto Criteri di gruppo) | *Si applica a Windows 10, versione 1803 e successive*: Questa impostazione si applica solo quando AllowTelemetry è impostata su `2`. Limita gli eventi dei dati di diagnostica avanzati inviati a Microsoft solo agli eventi richiesti da Desktop Analytics. Per altre informazioni, vedere [Eventi e campi dei dati di diagnostica avanzati di Windows 10 usati da Windows Analytics](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields).|
| **AllowDeviceNameInTelemetry** | GPO (Oggetto Criteri di gruppo) | *Si applica a Windows 10, versione 1803 e successive*: Per consentire ai dispositivi di continuare a inviare il nome del dispositivo, è necessario un consenso esplicito.<br> <br>Nota: Il nome del dispositivo non viene inviato a Microsoft per impostazione predefinita. Se non si invia il nome del dispositivo, il dispositivo viene visualizzato in Desktop Analytics come "Sconosciuto". Questo comportamento può rendere difficile l'identificazione e la valutazione dei dispositivi. Per altre informazioni, vedere [Nome del dispositivo](#device-name). | 
| **CommercialDataOptIn** | Criteri locali |*Si applica a Windows 7 e Windows 8.1*: Per Desktop Analytics è necessario il valore `1`. Per altre informazioni, vedere [Consenso esplicito per dati commerciali in Windows 7](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)). |
| **RequestAllAppraiserVersions** | Entrambi |*Si applica a Windows 7 e Windows 8.1*: Per il corretto funzionamento della raccolta dati per Desktop Analytics, il valore `1` è obbligatorio. | 
| **DisableEnterpriseAuthProxy** | GPO (Oggetto Criteri di gruppo) |*Si applica a tutte le versioni di Windows*: Per il corretto funzionamento della raccolta dati per Desktop Analytics, il valore `0` è obbligatorio. | 

> [!Important]  
> Nella maggior parte dei casi usare solo Configuration Manager per configurare queste impostazioni. Non applicare anche queste impostazioni negli oggetti criteri di gruppo del dominio. Per altre informazioni, vedere [Risoluzione dei conflitti](#conflict-resolution).<!-- SCCMDocs-pr 3120 -->

### <a name="device-name"></a>Nome del dispositivo

A partire da Windows 10, versione 1803, il nome del dispositivo non viene più raccolto per impostazione predefinita. Per raccogliere il nome del dispositivo con i dati di diagnostica, è necessario un consenso esplicito. Senza il nome del dispositivo, è più difficile identificare i dispositivi che richiedono attenzione durante la valutazione di un aggiornamento a una nuova versione di Windows.

Se non si invia il nome del dispositivo, il dispositivo viene visualizzato in Desktop Analytics come "Sconosciuto".

![Elenco dei dispositivi di Desktop Analytics con nomi "Sconosciuto"](media/unknown-device-name.png)

Per configurare questa opzione, è disponibile un'opzione nelle impostazioni di Configuration Manager per Desktop Analytics: **Consenti il nome del dispositivo nei dati di diagnostica**. Questa impostazione di Configuration Manager controlla l'impostazione dei criteri di Windows, AllowDeviceNameInTelemetry.
 

### <a name="conflict-resolution"></a>Risoluzione dei conflitti

In generale, usare le raccolte di Configuration Manager per le impostazioni e la registrazione di Desktop Analytics. Usare l'appartenenza diretta o le query per includere o escludere i dispositivi dalla raccolta. Per altre informazioni, vedere [Come creare le raccolte](/sccm/core/clients/manage/collections/create-collections).

Configuration Manager configura le impostazioni di Windows solo se un valore non esiste già. Se è necessario configurare impostazioni diverse per un unico gruppo di dispositivi, è possibile usare i [criteri di gruppo](#windows-settings). 

Visualizzare queste impostazioni nell'editor dei criteri di gruppo nel percorso seguente: **Configurazione computer** > **Modelli amministrativi** > **Componenti di Windows** > **Raccolta dati e versioni di anteprima**. Le impostazioni di destinazione dei criteri di gruppo hanno la precedenza sulle impostazioni di Configuration Manager.

Quando si configura il livello dei dati di diagnostica, è necessario impostare il limite superiore per il dispositivo. Per impostazione predefinita, in Windows 10 versione 1803 e successive gli utenti possono scegliere di impostare un livello inferiore. È possibile controllare questo comportamento usando l'impostazione dei criteri di gruppo, **Configurare l'interfaccia utente dell'impostazione del consenso esplicito per la telemetria**. Per altre informazioni, vedere [Configure Windows diagnostic data in your organization](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management) (Configurare i dati di diagnostica di Windows nell'organizzazione).



## <a name="next-steps"></a>Passaggi successivi

Passare all'articolo successivo per creare piani di distribuzione in Desktop Analytics.
> [!div class="nextstepaction"]  
> [Creare piani di distribuzione](/sccm/desktop-analytics/create-deployment-plans)  

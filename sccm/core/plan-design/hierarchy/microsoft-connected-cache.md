---
title: Microsoft Connected Cache
titleSuffix: Configuration Manager
description: Usare il punto di distribuzione di Configuration Manager come server di cache locale per Ottimizzazione recapito
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c5cb5753-5728-4f81-b830-a6fd1a3e105c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 046dd4bae3270ffaed93982e52ab63e85bf99ead
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75799982"
---
# <a name="microsoft-connected-cache-in-configuration-manager"></a>Microsoft Connected Cache in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

<!--3555764-->

A partire dalla versione 1906, è possibile installare un server di Microsoft Connected Cache nei punti di distribuzione. Memorizzando nella cache questo contenuto in locale, i client possono trarre vantaggio dalla funzionalità di Ottimizzazione recapito, tuttavia è possibile contribuire a proteggere i collegamenti WAN.

> [!NOTE]
> A partire dalla versione 1910, questa funzionalità è denominata **Microsoft Connected Cache**. In precedenza era nota come Cache in rete di Ottimizzazione recapito (DOINC).

Questo server di cache agisce come una cache trasparente su richiesta per il contenuto scaricato da Ottimizzazione recapito. Usare le impostazioni client per assicurarsi che il server sia disponibile soltanto ai membri del gruppo di limiti di Configuration Manager locale.

Questa cache è separata dal contenuto del punto di distribuzione di Configuration Manager. Se si sceglie la stessa unità come ruolo del punto di distribuzione, il contenuto viene archiviato separatamente.

> [!Note]  
> Il server di Connected Cache è un'applicazione installata in Windows Server. L'applicazione è ancora in fase di sviluppo.

## <a name="how-it-works"></a>Come funziona

Quando si configurano i client per l'uso del server di Connected Cache, questi con richiedono più il recapito da Internet del contenuto gestito dal cloud Microsoft. I client richiedono questo contenuto al server di cache installato nel punto di distribuzione. Il server locale memorizza nella cache questo contenuto usando la funzionalità IIS per Application Request Routing (ARR). Il server di cache può quindi rispondere rapidamente a qualsiasi richiesta futura dello stesso contenuto. Se il server di Connected Cache non è disponibile o il contenuto non è stato ancora memorizzato nella cache, i client scaricano il contenuto da Internet. I client usano Ottimizzazione recapito anche per scaricare parti di contenuto dai peer nella propria rete.

![Diagramma del funzionamento di Connected Cache](media/3555764-microsoft-connected-cache.png)

1. Il client verifica la disponibilità di aggiornamenti e ottiene l'indirizzo della rete per la distribuzione di contenuti (CDN).

2. Configuration Manager configura le impostazioni di Ottimizzazione recapito nel client, incluso il nome del server di cache.

3. Il client A richiede il contenuto al server di cache di Ottimizzazione recapito.

4. Se la cache non include il contenuto, il server di cache di Ottimizzazione recapito lo ottiene dalla rete CDN.

5. Se il server di cache non risponde, il client scarica il contenuto dalla rete CDN.

6. I client usano Ottimizzazione recapito per ottenere parti di contenuto dai peer.

## <a name="prerequisites-and-limitations"></a>Prerequisiti e limiti

- Un punto di distribuzione *locale* con le configurazioni seguenti:

  - Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 o Windows Server 2019 in esecuzione

  - Il sito Web predefinito abilitato sulla porta 80

  - Non preinstallare la funzionalità [Application Request Routing](https://docs.microsoft.com/iis/extensions/planning-for-arr/application-request-routing-version-2-overview) (ARR) di IIS. Connected Cache installa ARR e ne configura le impostazioni. Microsoft non può garantire che la configurazione ARR di Connected Cache non crei conflitti con altre applicazioni presenti nel server che usano anch'esse questa funzionalità.

  - Il punto di distribuzione richiede l'accesso internet a Microsoft cloud. Gli URL specifici possono variare a seconda del contenuto specifico abilitato per il cloud. Per altre informazioni, vedere i [requisiti di accesso Internet](/sccm/core/plan-design/network/internet-endpoints).

- Client che eseguono Windows 10, 1709 e versioni successive

## <a name="enable-connected-cache"></a>Abilitare Connected Cache

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione** e selezionare il nodo **Punti di distribuzione**.

1. Selezionare un punto di distribuzione *locale* e quindi selezionare **Proprietà** nella barra multifunzione.

1. Nelle proprietà del ruolo del punto di distribuzione, nella scheda **Generale**, configurare le impostazioni seguenti:  

    1. Abilitare l'opzione **Abilita l'uso di questo punto di distribuzione come server di Microsoft Connected Cache**  

        Visualizzare e accettare le condizioni di licenza.

    2. **Unità locale da usare**: Selezionare il disco da usare per la cache. **Automatico** è il valore predefinito, che usa il disco con maggiore spazio libero.<sup>[Nota 1](#bkmk_note1)</sup>  

        > [!Note]  
        > È possibile cambiare questa unità in un secondo momento. Eventuali contenuti memorizzati nella cache andranno persi, a meno che non vengano copiati nella nuova unità.

    3. **Spazio su disco:** Selezionare la quantità di spazio su disco da riservare in GB o una percentuale dello spazio su disco totale. Per impostazione predefinita, questo valore è impostato su 100 GB.

        > [!Note]  
        > La dimensione predefinita della cache dovrebbe essere sufficiente per la maggior parte dei clienti. È possibile modificare le dimensioni della cache in un secondo momento.

    4. **Conserva la cache durante la disabilitazione del server di Connected Cache**: Se si rimuove il server della cache e si abilita questa opzione, il server mantiene il contenuto della cache sul disco.  

1. Nelle impostazioni client, nel gruppo **Ottimizzazione recapito**, configurare l'impostazione su **Abilitare i dispositivi gestiti da Configuration Manager in modo che usino i server di Microsoft Connected Cache per il download dei contenuti**.  

### <a name="bkmk_note1"></a> Nota 1: Informazioni sulla selezione dell'unità

Se si seleziona **Automatico**, quando Configuration Manager installa il componente Connected Cache, viene rispettato il file **no_sms_on_drive.sms**. Ad esempio, il punto di distribuzione contiene il file `C:\no_sms_on_drive.sms`. Anche se l'unità C: ha maggiore spazio libero, Configuration Manager configura Connected Cache per l'uso di un'altra unità per la cache.

Se si seleziona un'unità specifica che ha già il file **no_sms_on_drive.sms**, Configuration Manager ignora il file. La configurazione di Connected Cache per l'uso di tale unità è un intento esplicito. Ad esempio, il punto di distribuzione contiene il file `F:\no_sms_on_drive.sms`. Quando si configurano in modo esplicito le proprietà del punto di distribuzione per l'uso dell'unità **F:** , Configuration Manager configura Connected Cache per l'uso dell'unità F: per la cache.

Per cambiare l'unità dopo l'installazione di Connected Cache:

- Configurare manualmente le proprietà del punto di distribuzione per usare una lettera di unità specifica.

- Se impostate su automatico, creare innanzitutto il file **no_sms_on_drive.sms**. Apportare quindi alcune modifiche alle proprietà del punto di distribuzione per attivare una modifica della configurazione.

## <a name="verify"></a>Verifica

Quando i client scaricano il contenuto gestito dal cloud, usano Ottimizzazione recapito dal server della cache installato nel punto di distribuzione. Il contenuto gestito dal cloud include i tipi seguenti:

- App di Microsoft Store
- Funzionalità di Windows su richiesta, come le lingue
- Se si abilitano [Criteri di Windows Update per le aziende](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10): Aggiornamenti delle funzionalità e della qualità di Windows 10
- Per i [carichi di lavoro con co-gestione](/sccm/comanage/workloads):
  - Windows Update for Business: Aggiornamenti delle funzionalità e della qualità di Windows 10
  - App A portata di clic di Office: App e aggiornamenti di Office
  - App client: App e aggiornamenti di Microsoft Store
  - Endpoint Protection: Aggiornamenti delle definizioni di Windows Defender

In Windows 10 1809 o versione successiva, verificare questo comportamento con **Get-DeliveryOptimizationStatus** Windows PowerShell cmdlet. Nell'output di cmdlet, rivedere il valore di **BytesFromCacheServer**. Per altre informazioni, vedere [Monitorare Ottimizzazione recapito](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization-setup#monitor-delivery-optimization).

Se il server di cache restituisce errori HTTP, il client di Ottimizzazione recapito esegue il fallback all'origine cloud originale.

Per informazioni più dettagliate, vedere [Risolvere i problemi relativi a Microsoft Connected Cache in Configuration Manager](/sccm/core/servers/deploy/configure/troubleshoot-microsoft-connected-cache).

## <a name="bkmk_intune"></a> Supporto per le app Win32 di Intune

<!--5032900-->

A partire dalla versione 1910, quando si abilita Connected Cache nei punti di distribuzione di Configuration Manager, questi possono essere usati per gestire le app Win32 di Microsoft Intune nei client con co-gestione.

### <a name="prerequisites"></a>Prerequisiti

#### <a name="client"></a>Client

- Aggiornare il client alla versione più recente.

- Il dispositivo client deve avere almeno 4 GB di memoria.

    > [!TIP]
    > Usare l'impostazione di Criteri di gruppo seguente: Configurazione computer > Modelli amministrativi > Componenti di Windows > Ottimizzazione recapito > **Capacità RAM minima (inclusiva) richiesta per abilitare l'uso di peer caching (in GB)** .

#### <a name="site"></a>Sito

- Abilitare Connected Cache in un punto di distribuzione. Per altre informazioni, vedere [Microsoft Connected Cache](/configmgr/core/plan-design/hierarchy/microsoft-connected-cache).

- Il client e il punto di distribuzione abilitato per Connected Cache devono trovarsi nello stesso gruppo di limiti.

- Abilitare le impostazioni client seguenti nel gruppo di [**Ottimizzazione recapito**](/configmgr/core/clients/deploy/about-client-settings#delivery-optimization):

  - **Usare i gruppi di limiti di Configuration Manager per l'ID del gruppo di ottimizzazione recapito**
  - **Abilitare i dispositivi gestiti da Configuration Manager in modo che usino i server di Microsoft Connected Cache per il download dei contenuti**

- Abilitare la funzionalità di versione non definitiva **Client apps for co-managed devices** (App client per dispositivi co-gestiti). Per altre informazioni, vedere [Funzionalità di versioni non definitive](/configmgr/core/servers/manage/pre-release-features).

- Abilitare la co-gestione e passare il carico di lavoro **Client apps** (App client) a **Pilot Intune** (Distribuzione pilota di Intune) o a **Intune**. Per altre informazioni, vedere gli articoli seguenti:

  - [Carichi di lavoro-App client](/configmgr/comanage/workloads#client-apps)
  - [Come abilitare la co-gestione](/configmgr/comanage/how-to-enable)
  - [Come trasferire i carichi di lavoro di Configuration Manager a Intune](/configmgr/comanage/how-to-switch-workloads)

    Se si è nella distribuzione pilota, aggiungere il client alla raccolta pilota per le app client.

#### <a name="intune"></a>Intune

- Questa funzionalità supporta solo il tipo di app Win32 di Intune.

  - Per questo scopo, creare e assegnare, ovvero distribuire, una nuova app in Intune. Le app create prima di Intune versione 1811 non funzionano. Per altre informazioni, vedere [Gestione delle app Win32 di Intune](https://docs.microsoft.com/intune/apps/apps-win32-app-management).

  - Le dimensioni dell'app devono essere di almeno 100 MB.
  
    > [!TIP]
    > Usare l'impostazione di Criteri di gruppo seguente: Configurazione computer > Modelli amministrativi > Componenti di Windows > Ottimizzazione recapito > **Dimensioni minime file di contenuto per caching (in MB)** .

## <a name="see-also"></a>Vedere anche

[Ottimizzare gli aggiornamenti di Windows 10 con Ottimizzazione recapito](/sccm/sum/deploy-use/optimize-windows-10-update-delivery)

[Risolvere i problemi relativi a Microsoft Connected Cache in Configuration Manager](/sccm/core/servers/deploy/configure/troubleshoot-microsoft-connected-cache)

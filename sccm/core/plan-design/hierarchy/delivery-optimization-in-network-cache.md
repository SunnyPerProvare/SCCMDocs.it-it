---
title: Ottimizzazione recapito nella cache in rete
titleSuffix: Configuration Manager
description: Usare il punto di distribuzione di Configuration Manager come server di cache locale per Ottimizzazione recapito
ms.date: 07/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: c5cb5753-5728-4f81-b830-a6fd1a3e105c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cacc27b95328d5abd43e477762ebe4d55562bfef
ms.sourcegitcommit: ef7800a294e5db5d751921c34f60296c1642fc1f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/01/2019
ms.locfileid: "68712573"
---
# <a name="delivery-optimization-in-network-cache-in-configuration-manager"></a>Cache in rete di Ottimizzazione recapito in Configuration Manager

<!--3555764-->

A partire dalla versione 1906, è possibile installare un server di cache in rete di Ottimizzazione recapito nei punti di distribuzione. Memorizzando nella cache questo contenuto in locale, i client possono trarre vantaggio dalla funzionalità di Ottimizzazione recapito, tuttavia è possibile contribuire a proteggere i collegamenti WAN.

Questo server di cache agisce come una cache trasparente su richiesta per il contenuto scaricato da Ottimizzazione recapito. Usare le impostazioni client per assicurarsi che il server sia disponibile soltanto ai membri del gruppo di limiti di Configuration Manager locale.

Questa cache è separata dal contenuto del punto di distribuzione di Configuration Manager. Se si sceglie la stessa unità come ruolo del punto di distribuzione, il contenuto viene archiviato separatamente.

> [!Note]  
> Il server della cache nella rete di Ottimizzazione recapito è una funzionalità di Windows Server che è ancora in fase di sviluppo. Nella console di Configuration Manager è contrassegnata da un'etichetta *beta*.  


## <a name="how-it-works"></a>Come funziona

Se i client vengono configurati per l'uso del server di cache in rete di Ottimizzazione recapito, questi con richiederanno più il recapito da Internet del contenuto gestito dal cloud Microsoft. I client richiedono il contenuto al server di cache in rete di Ottimizzazione recapito installato nel punto di distribuzione. Il server di cache in rete di Ottimizzazione recapito memorizza il contenuto usando la funzionalità IIS per Application Request Routing (ARR). Il server di cache può quindi rispondere rapidamente a qualsiasi richiesta futura dello stesso contenuto. Se il server di cache in rete di Ottimizzazione recapito non è disponibile o il contenuto non è stato ancora memorizzato nella cache, i client scaricano il contenuto da Internet. I client usano Ottimizzazione recapito anche per scaricare parti di contenuto dai peer nella propria rete.

![Diagramma del funzionamento della cache in rete di Ottimizzazione recapito](media/3555764-delivery-optimization-in-network-cache.png)

1. Il client verifica la disponibilità di aggiornamenti e ottiene l'indirizzo della rete per la distribuzione di contenuti (CDN).

2. Configuration Manager configura le impostazioni di Ottimizzazione recapito nel client, incluso il nome del server di cache.

3. Il client A richiede il contenuto al server di cache di Ottimizzazione recapito.

4. Se la cache non include il contenuto, il client A lo otterrà dalla rete CDN.

5. Se il server di cache non risponde, il client scarica il contenuto dalla rete CDN.

6. I client usano Ottimizzazione recapito per ottenere parti di contenuto dai peer.


## <a name="prerequisites-and-limitations"></a>Prerequisiti e limiti

- Un punto di distribuzione *locale* con le configurazioni seguenti:

    - Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 o Windows Server 2019 in esecuzione

    - Il sito Web predefinito abilitato sulla porta 80

    - Non preinstallare la funzionalità [Application Request Routing](https://docs.microsoft.com/iis/extensions/planning-for-arr/application-request-routing-version-2-overview) (ARR) di IIS. La cache in rete di Ottimizzazione recapito installa ARR e ne configura le impostazioni. Microsoft non può garantire che la configurazione ARR della cache in rete di Ottimizzazione recapito non creerà conflitti con altre applicazioni presenti nel server che usano anch'esse questa funzionalità.

    - Il punto di distribuzione richiede l'accesso internet a Microsoft cloud. Gli URL specifici possono variare a seconda del contenuto specifico abilitato per il cloud. Per altre informazioni, vedere i [requisiti di accesso Internet](/sccm/core/plan-design/network/internet-endpoints).

- Client che eseguono Windows 10, 1709 e versioni successive


## <a name="enable-doinc"></a>Abilitare la cache in rete di Ottimizzazione recapito

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione** e selezionare il nodo **Punti di distribuzione**.

1. Selezionare un punto di distribuzione locale e quindi nella barra multifunzione selezionare **Proprietà**.

1. Nelle proprietà del ruolo del punto di distribuzione, nella scheda **Generale**, configurare le impostazioni seguenti:  

    1. Selezionare l'opzione **Abilita l'uso di questo punto di distribuzione come server di cache in rete di Ottimizzazione recapito**  

        Visualizzare e accettare le condizioni di licenza.

    2. **Unità locale da usare**: Selezionare il disco da usare per la cache. **Automatico** è il valore predefinito, che usa il disco con maggiore spazio libero.  

        > [!Note]  
        > È possibile cambiare questa unità in un secondo momento. Eventuali contenuti memorizzati nella cache andranno persi, a meno che non vengano copiati nella nuova unità.

    3. **Spazio su disco:** Selezionare la quantità di spazio su disco da riservare in GB o una percentuale dello spazio su disco totale. Per impostazione predefinita, questo valore è impostato su 100 GB.

        > [!Note]  
        > La dimensione predefinita della cache dovrebbe essere sufficiente per la maggior parte dei clienti. È possibile modificare le dimensioni della cache in un secondo momento.

    4. **Conserva la cache durante la disabilitazione del server di cache in rete**: Se si rimuove il server della cache e si abilita questa opzione, il server mantiene il contenuto della cache sul disco.  

1. Nel gruppo **Ottimizzazione recapito** delle impostazioni client configurare l'impostazione per **Abilitare i dispositivi gestiti da Configuration Manager in modo che usino i server di cache in rete di Ottimizzazione recapito (beta) per il download dei contenuti**.  


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


## <a name="see-also"></a>Vedere anche

[Ottimizzare gli aggiornamenti di Windows 10 con Ottimizzazione recapito](/sccm/sum/deploy-use/optimize-windows-10-update-delivery)
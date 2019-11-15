---
title: Anteprima di UUP
titleSuffix: Configuration Manager
description: Istruzioni per l'anteprima dell'integrazione UUP
ms.date: 11/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: f06955ac-70ed-424d-a3e7-6b80ff2e114f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1dbb2ecb6cbac9e8085daafc577e82bc9e9c2b5e
ms.sourcegitcommit: 3141fa75c410586fcb316ac7b951e28f7cb0f3a7
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 11/12/2019
ms.locfileid: "73962155"
---
# <a name="uup-private-preview-instructions"></a>Istruzioni per l'anteprima privata di UUP

> [!Note]  
> Queste informazioni fanno riferimento a una funzionalità di anteprima che può essere modificata sostanzialmente prima del rilascio della versione commerciale. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

## <a name="introduction"></a>Introduzione

La piattaforma di aggiornamento unificata (UUP) è la piattaforma per la creazione di pacchetti e la pubblicazione che i dispositivi consumer e aziendali usano per ricevere gli aggiornamenti da Windows Update for business. Il programma di anteprima privata UUP è per i clienti che hanno accettato di consentire a Microsoft di convalidare l'uso degli aggiornamenti di UUP in Configuration Manager per risolvere i problemi che i clienti segnalano attualmente le finestre di manutenzione. Questi aggiornamenti non sono attualmente disponibili pubblicamente.

Per altre informazioni su UUP, vedere il post del blog di Windows [An update on our Unified Update Platform (UUP)](https://blogs.windows.com/windowsexperience/2017/03/02/an-update-on-our-unified-update-platform-uup/) (Un aggiornamento su Unified Update Platform).

## <a name="benefits"></a>Vantaggi

Gli aggiornamenti cumulativi e la funzionalità UUP di Windows 10 consentono di risolvere più problemi che i clienti segnalano oggi con le finestre di manutenzione.

### <a name="feature-updates"></a>Aggiornamenti delle funzionalità

- Con l'aggiornamento di una funzionalità UUP, il processo di Windows Update conserva funzionalità su richiesta (Dom) e Language Pack.

- Aggiornare direttamente al livello di conformità di sicurezza più recente. Non è necessario installare gli aggiornamenti della sicurezza subito dopo un aggiornamento della funzionalità. Microsoft pubblica un nuovo aggiornamento della funzionalità ogni mese con l'aggiornamento cumulativo più recente per la sicurezza. Non è necessario scaricare o distribuire la maggior parte del contenuto di aggiornamento delle funzionalità ogni mese. Si scarica solo l'aggiornamento della sicurezza, che UUP condivide con l'aggiornamento cumulativo.

### <a name="cumulative-updates"></a>Aggiornamenti cumulativi

- Gli aggiornamenti cumulativi con UUP includono gli aggiornamenti dello stack di manutenzione (Servicing Stack Updates, SSU) oltre agli aggiornamenti della sicurezza cumulativi mensili. Questo comportamento consente di risolvere problemi con l'orchestrazione di questi due aggiornamenti. Verifica che gli aggiornamenti dello stack di manutenzione siano disponibili per l'installazione degli aggiornamenti cumulativi. Non è necessario gestire e orchestrare queste relazioni.

- Gli aggiornamenti cumulativi con UUP consentono di distribuire i DOM e il contenuto dei Language Pack offline. Questo comportamento consente agli utenti di aggiungerli su richiesta. Gli utenti non devono scaricare da Internet e non è necessario capire come pre-installare il contenuto.

## <a name="set-up"></a>Configurazione

### <a name="1-send-your-wsus-id-to-microsoft"></a>1. Invia l'ID WSUS a Microsoft

Per partecipare all'anteprima privata di UUP, condividere l'ID WSUS con il contatto di anteprima di UUP. Microsoft approva l'ambiente WSUS nel programma UUP Preview. Senza questo ID non è possibile visualizzare eventuali aggiornamenti di UUP fino a quando l'anteprima non diventa pubblica.

Per ottenere l'ID WSUS, eseguire lo script di PowerShell seguente:

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId

# also check MUUrl
$config.MUUrl
```

La proprietà **MUUrl** deve essere `https://sws.update.microsoft.com`. Per modificarla, vedere la risoluzione nel seguente articolo di supporto: la [sincronizzazione WSUS non riesce con SoapException](https://support.microsoft.com/help/4482416/wsus-synchronization-fails-with-soapexception).

### <a name="2-update-configuration-manager"></a>2. Aggiornare Configuration Manager

Apportare le modifiche seguenti al sito di Configuration Manager per supportare questa anteprima di UUP:

#### <a name="diagnostics-and-usage-data-level"></a>Livello dati di diagnostica e di utilizzo

Valutare la possibilità di aumentare il livello dati di diagnostica e di utilizzo di Configuration Manager durante questa anteprima. Il livello **Completo** consente a Microsoft di analizzare meglio i problemi relativi a questa nuova funzionalità e di risolverli. Per altre informazioni, vedere [Livelli di raccolta dati di utilizzo e di diagnostica per la versione 1906](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1906).

#### <a name="install-the-latest-update"></a>Installare l'aggiornamento più recente

1. Aggiornare il sito con uno degli aggiornamenti seguenti:

    - Versione 1902 con l' [aggiornamento cumulativo](https://support.microsoft.com/help/4500571)
    - [Versione 1906](/sccm/core/servers/manage/checklist-for-installing-update-1906)

    Per altre informazioni, vedere [Installare gli aggiornamenti nella console](/sccm/core/servers/manage/install-in-console-updates).

2. Aggiornare i client.  

    - Per semplificare questo processo, è consigliabile usare l'aggiornamento automatico. Per altre informazioni, vedere [Aggiornare i client](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  

    - Aggiornare tutti i client destinati agli aggiornamenti di UUP per evitare di *scaricare inutilmente circa 6 GB* di contenuto inutilizzato nei client.

### <a name="3-update-windows-clients-to-a-supported-version"></a>3. Aggiornare i client Windows a una versione supportata

Per installare correttamente gli aggiornamenti di UUP, installare entrambi gli aggiornamenti seguenti:

1. Livello di conformità mensile cumulativo minimo specifico.

2. Aggiornamento non cumulativo e non di sicurezza specifico dal catalogo Microsoft Update. Per importare l'aggiornamento in Configuration Manager per la distribuzione, vedere [importare gli aggiornamenti dal catalogo di Microsoft Update](/sccm/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog).

#### <a name="supported-versions-of-windows-10-and-required-updates"></a>Versioni supportate di Windows 10 e aggiornamenti necessari

| Versione di Windows 10 | Livello di conformità minimo | Aggiornamento del catalogo aggiuntivo |
| ------------------ | ------------------------ | ------------------ |
| **Windows 10, versione 1903** | RTM | 7 novembre 2019, [KB4529943](https://www.catalog.update.microsoft.com/search.aspx?q=4529943) |
| **Windows 10, versione 1809** | 2019 agosto, [KB4511553](https://support.microsoft.com/help/4511553/windows-10-update-kb4511553) | 7 novembre 2019, [KB4514987](https://www.catalog.update.microsoft.com/search.aspx?q=4514987) |
| **Windows 10, versione 1803** | 2019 aprile, [KB4493464](https://support.microsoft.com/help/4493464/windows-10-update-kb4493464) | 7 novembre 2019, [KB4512745](https://www.catalog.update.microsoft.com/search.aspx?q=4512745) |
| **Windows 10, versione 1709** | 2019 aprile, [KB4493441](https://support.microsoft.com/help/4493441/windows-10-update-kb4493441) | 7 novembre 2019, [KB4512744](https://www.catalog.update.microsoft.com/search.aspx?q=4512744) |

> [!IMPORTANT]
> - Se si applicano gli aggiornamenti del 12 novembre 2019 al client prima di applicare il 7 novembre 2019 aggiornamento del catalogo aggiuntivo, le modifiche apportate all'agente Windows Update necessarie per il supporto di UUP verranno sovrascritte. Per correggere i client in tale scenario, applicare l'aggiornamento del catalogo aggiuntivo dopo il 12 novembre 2019 gli aggiornamenti installati.
> - Se si applica un aggiornamento della funzionalità al client, sarà necessario reinstallare l'aggiornamento del catalogo aggiuntivo dopo il completamento dell'aggiornamento.

### <a name="4-allow-clients-to-download-delta-content-when-available"></a>4. Consenti ai client di scaricare contenuto differenziale quando disponibile

Per scaricare correttamente gli aggiornamenti di UUP, abilitare l'impostazione client per **consentire ai client di scaricare il contenuto Delta se disponibile**. Questa impostazione consente Configuration Manager di consentire all'agente di Windows Update (WUA) di determinare il contenuto necessario da scaricare nei client. Questo comportamento è invece del valore predefinito, in cui il client di Configuration Manager Scarica tutto il contenuto associato all'aggiornamento di UUP. Quando si abilita questa impostazione, WUA determina il contenuto aggiuntivo richiesto da ogni aggiornamento di UUP. Ad esempio, solo i DOM e i Language Pack necessari.

Quando si abilita questa impostazione, non influisce sul download del contenuto del server da Internet. Si applica solo ai download del client. Prima di distribuire gli aggiornamenti di UUP ai client, applicare questa impostazione ai client che soddisfano le versioni supportate di UUP. Gli aggiornamenti client prerequisiti risolvono i problemi di compatibilità per gli aggiornamenti di UUP in WSUS e Configuration Manager.

Per altre informazioni su questa impostazione client, vedere [Informazioni sulle impostazioni client - Aggiornamenti software](/sccm/core/clients/deploy/about-client-settings#allow-clients-to-download-delta-content-when-available).

### <a name="5-review-your-software-update-infrastructure"></a>5. Esaminare l'infrastruttura di aggiornamento software

Prima di sincronizzare gli aggiornamenti di UUP, esaminare le regole di distribuzione automatica (ADR) e i piani di manutenzione. Se non si vuole distribuire automaticamente questi aggiornamenti, rivedere le ADR per filtrarli. Per ulteriori informazioni, vedere [come trovare gli aggiornamenti di Uup sincronizzati](#how-to-find-synced-uup-updates). Per impostazione predefinita, i piani di manutenzione esistenti distribuiscono solo gli aggiornamenti non UUP. Per modificare questo comportamento, è possibile modificare i piani di manutenzione.

Esaminare i report di conformità e modificarli se necessario. Ad esempio, se si misura la conformità per tutti i prodotti, ora verranno visualizzati sia gli aggiornamenti cumulativi UUP che quelli non UUP. I dispositivi segnaleranno la conformità a entrambi i tipi di aggiornamenti. Verificare che i report di conformità risolvono questa modifica.

## <a name="enable-uup-and-start-testing"></a>Abilitare UUP e avviare il test

### <a name="select-products-and-classifications-to-sync"></a>Selezionare i prodotti e le classificazioni da sincronizzare

Quando si è pronti per avviare la sincronizzazione degli aggiornamenti di UUP e Microsoft ha approvato l'ID WSUS, abilitare i nuovi prodotti:

1. [Sincronizzare gli aggiornamenti software](/sccm/sum/get-started/synchronize-software-updates) per popolare i nuovi prodotti.  

2. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**.

3. Selezionare il sito di livello superiore, che è un sito di amministrazione centrale o un sito primario autonomo.

4. Selezionare **Configura componenti del sito** nella barra multifunzione e scegliere **Punto di aggiornamento software**.

5. Passare alla scheda **prodotti** e selezionare uno o più dei prodotti seguenti: 

    - **Windows 10 UUP Preview**
    - **Windows Server UUP Preview**

6. Passare alla scheda **classificazioni** e selezionare le opzioni seguenti:  

    - **Aggiornamenti della sicurezza**: per visualizzare gli aggiornamenti cumulativi di Uup  
    - **Aggiornamenti**: per visualizzare gli aggiornamenti delle funzionalità di UUP  

7. Sincronizzare di nuovo gli aggiornamenti software per visualizzare i nuovi aggiornamenti di UUP.

### <a name="how-to-find-synced-uup-updates"></a>Come individuare gli aggiornamenti di UUP sincronizzati

Dopo aver sincronizzato gli aggiornamenti di UUP nell'ambiente, trovarli nella console di Configuration Manager per eseguire il test. Sono disponibili due modi per trovare gli aggiornamenti dell'anteprima:

- Poiché questi aggiornamenti di anteprima si trovano in un prodotto separato, utilizzare il prodotto per filtrare per trovare questi aggiornamenti. Usare il filtro del prodotto del piano di manutenzione per distribuire gli aggiornamenti delle funzionalità UUP o non UUP.  

- Nei nodi **Tutti gli aggiornamenti software** e **Aggiornamenti di tutte le piattaforme Windows 10** di **Raccolta software** è presente la nuova colonna facoltativa **Tag**. Questa proprietà è disponibile anche come filtro in ADR. Per gli aggiornamenti di UUP, cercare `UUP`nel campo. È vuoto per gli aggiornamenti non UUP.  

### <a name="updates-available-during-preview"></a>Aggiornamenti disponibili durante l'anteprima

Per ulteriori informazioni su tutti gli aggiornamenti di Windows 10 rilasciati da Microsoft, vedere [informazioni sulla versione di Windows 10](https://docs.microsoft.com/windows/release-information/).

#### <a name="cumulative-updates-to-test"></a>Aggiornamenti cumulativi da testare

Sebbene sia possibile visualizzare più aggiornamenti con tag UUP, iniziare con l'aggiornamento di **settembre 2019** (2019-09) o una versione successiva. Ad esempio:

- 2019-09 aggiornamento cumulativo per Windows 10 versione 1809 per sistemi basati su x64 (KB4512578)
- 2019-09 aggiornamento cumulativo per Windows 10 versione 1803 per sistemi basati su x64 (KB4516058)
- 2019-09 aggiornamento cumulativo per Windows 10 versione 1709 per sistemi basati su x64 (KB4516066)

#### <a name="feature-updates-to-test"></a>Aggiornamenti delle funzionalità da testare

Sebbene sia possibile visualizzare più aggiornamenti con tag UUP, iniziare con l'aggiornamento **2019 di settembre** (2019-09B) o una versione successiva. Ad esempio:

- Aggiornamento delle funzionalità di Windows 10, versione 1809 x64 2019-09B
- Aggiornamento delle funzionalità di Windows 10, versione 1803 x64 2019-09B

## <a name="scenarios-to-test"></a>Scenari da sottoporre a test

### <a name="test-feature-updates"></a>Aggiornamenti delle funzionalità di test

- Aggiorna direttamente al livello di conformità di sicurezza scelto  

- Installare FODs e Language Pack prima dell'aggiornamento. Assicurarsi che l'aggiornamento manservi questi componenti.  

### <a name="test-cumulative-updates"></a>Testare gli aggiornamenti cumulativi

Durante l'anteprima, Mantieni i client conformi usando l'aggiornamento del tipo di UUP per più aggiornamenti consecutivi. Questo test consente di comprendere il comportamento continuo.

### <a name="test-content"></a>Contenuto del test

Il primo aggiornamento per ogni versione principale (1809, 1803, 1709), architettura e combinazione di lingue risulterà grande. Questa dimensione è sia per il numero di file che per lo spazio su disco rispetto a quanto precedentemente visto con aggiornamenti non UUP. Questo contenuto aggiuntivo è destinato principalmente a tutte le funzionalità su richiesta e i Language Pack per gli aggiornamenti cumulativi. Per gli aggiornamenti delle funzionalità, è disponibile un contenuto di grandi dimensioni aggiuntivo per il primo aggiornamento.

Per gli aggiornamenti cumulativi e delle funzionalità futuri, la quantità di nuovo contenuto che il sito Scarica e distribuisce è molto più piccola. UUP condivide in modo intelligente tutti i contenuti Dom e Language Pack tra gli aggiornamenti. Non è necessario riscaricare o ridistribuire questo contenuto condiviso. Durante l'anteprima, in Windows 10 versioni 1709 e 1803, questo download mensile corrisponde alla dimensione degli aggiornamenti cumulativi negli scenari non UUP. In Windows 10 versione 1809 e successive, il download incrementale dell'aggiornamento cumulativo è molto più piccolo ogni mese.

Quando si esamina il contenuto totale scaricato e distribuito in un periodo di 12 mesi per *non Express*, Windows 10 versione 1803 senza Uup deve essere uguale a quello della versione 1809 con UUP. Il contenuto totale scaricato e distribuito nell'intero ciclo di vita della versione è più piccolo nella versione 1809 con UUP.

### <a name="supported-content-channels"></a>Canali di contenuto supportati

Per la versione di anteprima, è preferibile testare i tipici scenari reali. UUP supporta tutti i canali di contenuto, tra cui:

- Ottimizzazione recapito di Windows
- Peer cache di Configuration Manager
- Windows BranchCache
- Usare l'opzione **nessun pacchetto di distribuzione** e i client vengono scaricati direttamente da Microsoft Update. Usare questa opzione con ottimizzazione recapito.
- Provider di contenuti alternativi di terze parti

Per altre informazioni, vedere [FAQs to optimize Windows 10 update delivery](/sccm/sum/deploy-use/optimize-windows-10-update-delivery) (FAQ per ottimizzare il recapito degli aggiornamenti di Windows 10).

<!-- TODO: Addlink to WSUS Perf documentation-->

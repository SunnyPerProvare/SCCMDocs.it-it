---
title: Anteprima di UUP
titleSuffix: Configuration Manager
description: Istruzioni per l'anteprima dell'integrazione UUP
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 0b0da585-0096-410b-8035-6b7a312f37f5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 27a960758d8d3939798ae270404d5dd1afbea62d
ms.sourcegitcommit: ad25a7bdd983c5a0e4c95bffdc61c9a1ebcbb765
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2019
ms.locfileid: "55072986"
---
# <a name="uup-private-preview-instructions"></a>Istruzioni per l'anteprima privata di UUP

> [!Note]  
> Queste informazioni fanno riferimento a una funzionalità di anteprima che può essere modificata sostanzialmente prima del rilascio della versione commerciale. Microsoft non offre alcuna garanzia, espressa o implicita, relativamente alle informazioni fornite in questo articolo.  

## <a name="benefits"></a>Vantaggi

### <a name="feature-updates"></a>Aggiornamenti delle funzionalità

Gli aggiornamenti delle funzionalità con Windows 10 Unified Update Platform (UUP) sono progettati per risolvere diversi problemi riscontrati attualmente dai clienti con la manutenzione. Provare gli aggiornamenti delle funzionalità, tra cui:

- Eseguire l'aggiornamento fino al livello di conformità di sicurezza più recente. Non è più necessario installare gli aggiornamenti della sicurezza immediatamente dopo l'aggiornamento per garantire la conformità. Ogni mese verrà pubblicato un nuovo aggiornamento delle funzionalità che include l'aggiornamento cumulativo della sicurezza più recente. Non sarà necessario scaricare nuovamente o distribuire l'intero contenuto degli aggiornamenti delle funzionalità ogni mese, ma solo il componente dell'aggiornamento della sicurezza, condiviso anche con l'aggiornamento cumulativo.

- Tutti i Language Pack e le funzionalità su richiesta dovrebbero essere mantenuti e non andare persi durante il processo di aggiornamento.

- Gli aggiornamenti delle funzionalità con UUP supportano i file di installazione rapida, consentendo ai client di ridurre la quantità di contenuto che ogni client deve scaricare.

Per altre informazioni su UUP, vedere il post del blog di Windows [An update on our Unified Update Platform (UUP)](https://blogs.windows.com/windowsexperience/2017/03/02/an-update-on-our-unified-update-platform-uup/) (Un aggiornamento su Unified Update Platform).


### <a name="cumulative-updates"></a>Aggiornamenti cumulativi

Gli aggiornamenti cumulativi con UUP consentono la distribuzione offline dei contenuti dei Language Pack e delle funzionalità su richiesta, in modo da consentire agli utenti finali di ottenerli su richiesta senza richiedere una connessione a Internet o complesse attività di gestione temporanea da parte degli amministratori.



## <a name="set-up-instructions"></a>Istruzioni di configurazione

### <a name="1-send-your-wsus-id-to-your-uup-preview-contact-at-microsoft"></a>1. Inviare il proprio ID WSUS al contatto di anteprima di UUP presso Microsoft

Per poter partecipare all'anteprima privata di UUP, è necessario condividere l'ID WSUS con Microsoft in modo da inserire l'ambiente in uso nell'elenco elementi consentiti per l'anteprima. Senza questo ID, non sarà possibile visualizzare eventuali aggiornamenti di UUP fino a quando l'anteprima non diventa pubblica.

Per recuperare l'ID WSUS:

```PowerShell
$server = Get-WsusServer
$config = $server.GetConfiguration()
$config.ServerId

# also check MUUrl
$config.MUUrl
```

La proprietà **MUUrl** deve essere `https://sws.update.microsoft.com`. Per modificarla, vedere la risoluzione nell'articolo del supporto tecnico seguente: [La sincronizzazione di Windows Server Update Services non riesce con SoapException](https://support.microsoft.com/help/4482416/wsus-synchronization-fails-with-soapexception)


### <a name="2-update-configmgr"></a>2. Aggiornare ConfigMgr

Se si sincronizzano i file di installazione rapida nell'ambiente in uso, viene richiesto ConfigMgr 1810 Current Branch per gli ambienti di produzione o 1812 Technical Preview Branch per gli ambienti lab.

Se non si sincronizzano i file di installazione rapida nell'ambiente in uso, viene richiesto ConfigMgr 1810 Hotfix KB4482615 per gli ambienti di produzione o 1812 Technical Preview Branch per gli ambienti lab.


#### <a name="diagnostics-and-usage-data-level"></a>Livello dati di diagnostica e di utilizzo
Valutare la possibilità di aumentare il livello dati di diagnostica e di utilizzo di Configuration Manager durante questa anteprima. Il livello **Completo** consente a Microsoft di analizzare meglio i problemi relativi a questa nuova funzionalità e di risolverli. Per altre informazioni, vedere [Livelli di raccolta dati di utilizzo e di diagnostica per la versione 1810](/sccm/core/plan-design/diagnostics/levels-of-diagnostic-usage-data-collection-1810).


#### <a name="update-rollup-for-configmgr-1810-4486457"></a>Aggiornamento cumulativo per ConfigMgr 1810 (4486457)

1. Aggiornare il sito con l'aggiornamento cumulativo per la versione 1810. Per altre informazioni, vedere [Installare gli aggiornamenti nella console](/sccm/core/servers/manage/install-in-console-updates).  

2. Aggiornare i client.  

    - Per semplificare questo processo, è consigliabile usare l'aggiornamento automatico. Per altre informazioni, vedere [Aggiornare i client](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  

    - Tutti i client destinati agli aggiornamenti di UUP devono essere aggiornati per evitare di **scaricare inutilmente circa 6 GB** di contenuto inutilizzato nei client.

Per altre informazioni su questo aggiornamento, vedere [Aggiornamento cumulativo per System Center Configuration Manager Current Branch, versione 1810](https://support.microsoft.com/help/4486457).


<!-- 
#### 1812 Technical Preview
The 1812 Technical Preview is equivalent in supported UUP scenarios to the ConfigMgr 1810 UUP Hotfix (KB4482615).

The only note is that client upgrade of 1812 Technical Preview is broken from 1810.1 TP or 1811 TP. To work around this issue, you'll need to uninstall 1810.1 TP and 1811 TP clients, then install the 1812 TP client cleanly. All clients you target UUP updates to must be on 1812 Technical Preview (or later) to prevent **unnecessarily downloading around 6 GB** of unused content to the client.
 -->


### <a name="3-update-windows-clients-to-supported-versions"></a>3. Aggiornare i client Windows alle versioni supportate

#### <a name="for-express-installation-file-sync"></a>Per la sincronizzazione dei file di installazione rapida
Per il contenuto dell'installazione rapida, le versioni di Windows supportate includono:

- **Windows 10 versione 1809** con aggiornamento cumulativo non relativo alla sicurezza [KB4476976](https://support.microsoft.com/help/4476976/windows-10-update-kb4476976) (rilasciato il 22/1) o versione successiva. Questo aggiornamento è disponibile solo nel catalogo e non si sincronizza direttamente con WSUS. Per importare l'aggiornamento nell'ambiente in uso in modo da distribuirlo, vedere [Importare gli aggiornamenti da Microsoft Update Catalog](/sccm/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog).

- **Windows 10 versione 1803** con [KB4284835](https://support.microsoft.com/help/4284835) (aggiornamento cumulativo della sicurezza di giugno 2017) o versione successiva  

- **Windows 10 versione 1709** con [KB4338825](https://support.microsoft.com/help/4338825) (aggiornamento cumulativo della sicurezza di luglio 2017) o versione successiva  


#### <a name="for-non-express-installation-file-sync"></a>Per la sincronizzazione dei file non di installazione rapida
Per il contenuto non correlato all'installazione rapida, è necessario applicare una patch aggiuntiva. Questo aggiornamento è critico per evitare di scaricare inutilmente circa 6 GB di contenuto inutilizzato nel client. Le versioni di Windows supportate includono le build seguenti:

- **Windows 10 versione 1809** con aggiornamento cumulativo non relativo alla sicurezza [KB4476976](https://support.microsoft.com/help/4476976/windows-10-update-kb4476976) (rilasciato il 22/1) o versione successiva. Questo aggiornamento è disponibile solo nel catalogo e non si sincronizza direttamente con WSUS. Per importare l'aggiornamento nell'ambiente in uso in modo da distribuirlo, vedere [Importare gli aggiornamenti da Microsoft Update Catalog](/sccm/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog).


- I client **Windows 10 versione 1803** e **Windows 10 versione 1709** devono avere un livello di aggiornamento cumulativo di base oltre all'aggiornamento non cumulativo:
    - Aggiornamento cumulativo
        - 1803: [KB4284835](https://support.microsoft.com/help/4284835) (aggiornamento cumulativo della sicurezza di giugno 2017) fino all'aggiornamento cumulativo della sicurezza di gennaio 2019 incluso
        - 1709: [KB4338825](https://support.microsoft.com/help/4338825) (aggiornamento cumulativo della sicurezza di luglio 2017) fino all'aggiornamento cumulativo della sicurezza di gennaio 2019 incluso
    - Aggiornamento non cumulativo: Questo aggiornamento è disponibile solo nel catalogo e non si sincronizza direttamente con WSUS. Per importare l'aggiornamento nell'ambiente in uso in modo da distribuirlo, vedere [Importare gli aggiornamenti da Microsoft Update Catalog](/sccm/sum/get-started/synchronize-software-updates#import-updates-from-the-microsoft-update-catalog).
        - 1803: [KB4483541](https://support.microsoft.com/help/4483541)
        - 1709: [KB4483530](https://support.microsoft.com/help/4483530)


### <a name="4-enable-express-installation-on-clients-in-client-settings"></a>4. Abilitare l'installazione rapida nei client nelle impostazioni client

L'impostazione client per consentire l'installazione rapida deve essere configurata per gli aggiornamenti di UUP, indipendentemente dal fatto che il contenuto dell'installazione rapida venga o meno sincronizzato. Questa impostazione fa sì che ConfigMgr consenta all'agente di Windows Update (WUA) di determinare il contenuto necessario da scaricare nei client, anziché fare in modo che ConfigMgr scarichi tutto il contenuto associato all'aggiornamento di UUP. Questa impostazione è richiesta anche per gli scenari non di installazione rapida essendo presente contenuto facoltativo dei Language Pack e delle funzionalità su richiesta, che comporta una quantità non significativa di dati aggiuntivi non richiesti da tutti i client associati all'aggiornamento.

L'abilitazione di questa impostazione non influirà sui download del contenuto dei server, ma solo sui comportamenti dei download dei client. È importante disporre delle versioni di ConfigMgr e del client Windows riportate in precedenza prima di abilitare questa impostazione (se non è già stata abilitata), poiché tali versioni risolvono alcuni problemi di compatibilità con l'approvazione degli aggiornamenti direttamente in WSUS e abilitano ConfigMgr per l'uso di questo canale per gli aggiornamenti di UUP anche se il contenuto dell'installazione rapida non è stato sincronizzato.

Per abilitare l'installazione rapida nei client:

1. Nella console di Configuration Manager passare ad **Amministrazione** \ **Impostazioni client**  

2. Aprire le proprietà di Impostazioni client che si vuole usare o crearne di nuove per eseguire alla distribuzione in base alle esigenze.  

3. Nel gruppo **Aggiornamenti software** impostare **Abilita l'installazione di file per l'installazione rapida nei client** su **Sì**

![Evidenziazione delle impostazioni client nel gruppo Aggiornamenti software](../media/uup-preview-client-settings.png)


### <a name="5-make-sure-your-adrs-are-set-as-desired"></a>5. Assicurarsi che le regole di distribuzione automatica (ADR) siano configurate come richiesto 

Prima di abilitare la sincronizzazione degli aggiornamenti di UUP, prendere in considerazione le ADR e qualsiasi altra infrastruttura di aggiornamento in uso. Se non si vuole che questi aggiornamenti vengano distribuiti automaticamente nell'ambito delle regole di distribuzione automatica e dei piani di manutenzione esistenti, assicurarsi di aggiornare le ADR in modo da escluderli. A questo scopo, vedere l'articolo su [come trovare aggiornamenti di UUP sincronizzati](#how-to-find-synced-uup-updates). I piani di manutenzione esistenti distribuiranno solo gli aggiornamenti non di UUP per impostazione predefinita, ma è possibile aggiornarli in modo da modificare questo comportamento.

Considerare anche se questi aggiornamenti influiranno su eventuali report di conformità o altre infrastrutture semplicemente con la sincronizzazione e apportare preventivamente qualsiasi modifica desiderata. Ad esempio, se si misura la conformità tra tutti i prodotti, gli aggiornamenti di Windows 10 cumulativi di UUP e non di UUP verranno visualizzati come non conformi o conformi, con un conseguente sfasamento dei numeri.



## <a name="enable-uup-and-start-testing"></a>Abilitare UUP e avviare il test

### <a name="select-products-and-classifications-to-sync"></a>Selezionare i prodotti e le classificazioni da sincronizzare

Una volta che si è pronti per sincronizzare gli aggiornamenti di UUP e iniziare a usarli e si è ottenuta la conferma di Microsoft che il server WSUS in uso è abilitato per visualizzare il progetto pilota, abilitare i nuovi prodotti.

1. [Sincronizzare gli aggiornamenti software](/sccm/sum/get-started/synchronize-software-updates) per popolare i nuovi prodotti  

2. Nella console di Configuration Manager passare ad **Amministrazione** \ **Configurazione del sito** \ **Siti**  

3. Selezionare il sito di livello superiore, che è un sito di amministrazione centrale o un sito primario autonomo  

4. Aprire **Configura componenti del sito** \ **Punto di aggiornamento software**  

5. Nella scheda **Prodotti**, dopo che il server WSUS è stato aggiunto all'anteprima, dovrebbero essere visualizzati due nuovi prodotti. Questi prodotti includono il contenuto dell'anteprima di UUP.  

    - **Windows 10 UUP Preview**  
    - **Windows Server UUP Preview**  

6. Nella scheda **Classificazioni** assicurarsi di selezionare:  

    - **Aggiornamenti della sicurezza**: per visualizzare gli aggiornamenti cumulativi di UUP  
    - **Aggiornamenti**: per visualizzare gli aggiornamenti delle funzionalità di UUP  

7. Sincronizzare gli aggiornamenti software per visualizzare i nuovi aggiornamenti di UUP


### <a name="how-to-find-synced-uup-updates"></a>Come individuare gli aggiornamenti di UUP sincronizzati

Dopo avere sincronizzato gli aggiornamenti di UUP nell'ambiente in uso, è opportuno testarli. Esistono due semplici modi per trovare gli aggiornamenti di anteprima all'interno della console di Configuration Manager.

- Poiché questi aggiornamenti di anteprima sono in prodotti distinti, è sempre possibile usare il prodotto per filtrare o cercare questi aggiornamenti. Il filtro prodotti è stato aggiunto ai piani di manutenzione per consentire di selezionare se si vogliono distribuire gli aggiornamenti delle funzionalità UUP o non UUP.  

- È disponibile una nuova colonna opzionale, chiamata **Tag**, nei nodi **Tutti gli aggiornamenti software** e **Aggiornamenti di tutte le piattaforme Windows 10** della raccolta software, nonché un filtro nelle regole di distribuzione automatica. Questo campo è impostato su **UUP** per gli aggiornamenti di UUP ed è vuoto per gli aggiornamenti non UUP.  


### <a name="updates-available-during-preview"></a>Aggiornamenti disponibili durante l'anteprima

- Aggiornamenti cumulativi di Windows 10 1809
    - Aggiornamento della sicurezza di febbraio (2/12)  

- Aggiornamenti cumulativi di Windows 10 1803
    - Aggiornamento della sicurezza di dicembre (12/11)
    - Aggiornamento della sicurezza di gennaio (1/8)
    - Aggiornamento non relativo alla sicurezza di gennaio (1/15)
    - Aggiornamento della sicurezza di febbraio (2/12)  

- Aggiornamenti cumulativi di Windows 10 1709
    - Aggiornamento della sicurezza di dicembre (12/11)
    - Aggiornamento della sicurezza di gennaio (1/8)
    - Aggiornamento non relativo alla sicurezza di gennaio (1/15)
    - Aggiornamento della sicurezza di febbraio (2/12)  

- Aggiornamenti delle funzionalità di Windows 10 1809 (da 1709 o 1803)
    - Conformità aggiornamento della sicurezza di dicembre (12/11)
    - Conformità aggiornamento della sicurezza di gennaio (1/8)
    - Conformità aggiornamento della sicurezza di febbraio (2/12)  

- Aggiornamenti delle funzionalità di Windows 10 1803 (da 1709 o 1803)   
    - Conformità aggiornamento della sicurezza di dicembre (12/11)
    - Conformità aggiornamento della sicurezza di gennaio (1/8)
    - Conformità aggiornamento della sicurezza di febbraio (2/12)  

Se necessario, gli aggiornamenti della sicurezza di marzo e successivi continueranno a essere pubblicati in tutte queste aree finché UUP è in anteprima (privata o pubblica). Una volta completata l'anteprima, saranno supportati nell'ambiente di produzione solo gli aggiornamenti cumulativi di Windows 10 versione 1809 e gli aggiornamenti delle funzionalità (da Windows 10 versione 1803).


### <a name="scenarios-to-try"></a>Scenari da provare

#### <a name="feature-updates"></a>Aggiornamenti delle funzionalità
- Eseguire l'aggiornamento fino al livello di conformità di sicurezza scelto  

- Eseguire l'aggiornamento con le funzionalità su richiesta e i Language Pack installati prima dell'aggiornamento, che verranno mantenuti durante l'aggiornamento  

- Abilitare la sincronizzazione dei file di installazione rapida per gli aggiornamenti delle funzionalità per ridurre la quantità di contenuto che ogni client deve scaricare (facoltativo).  

    > [!Note]  
    > Questo vantaggio per il client comporta un download del server e una distribuzione superiori, come avviene per i file di installazione rapida per gli aggiornamenti cumulativi.  

#### <a name="cumulative-updates"></a>Aggiornamenti cumulativi
Durante l'anteprima, mantenere i client compatibili con l'aggiornamento di tipo UUP per più aggiornamenti consecutivi per mantenere le aspettative in corso.

#### <a name="content"></a>Content
Il primo aggiornamento per ogni versione principale (1809, 1803, 1709), architettura e combinazione linguistica sarà di grandi dimensioni, sia per il numero di file che per lo spazio su disco, rispetto ai precedenti aggiornamenti non UUP. Questo contenuto aggiuntivo è destinato principalmente a tutte le funzionalità su richiesta e i Language Pack per gli aggiornamenti cumulativi. Per gli aggiornamenti delle funzionalità, soprattutto se è abilitata l'installazione rapida, è presente contenuto aggiuntivo di grandi dimensioni per questo primo aggiornamento. 

Tuttavia, per gli aggiornamenti successivi (sia quelli cumulativi che gli aggiornamenti delle funzionalità mensili a livelli di conformità superiori), la quantità di nuovo contenuto che deve essere scaricato e distribuito sarà nettamente inferiore, poiché tutto il contenuto delle funzionalità su richiesta e dei Language Pack viene condiviso in modo intelligente tra gli aggiornamenti anziché essere nuovamente scaricato o ridistribuito. Durante l'anteprima, nelle versioni 1709 e 1803 questo download mensile sarà pari approssimativamente alle dimensioni degli aggiornamenti cumulativi per gli scenari non UUP. Tuttavia, nella versione 1809 la situazione migliora dal momento che il download incrementale dell'aggiornamento cumulativo è inferiore di mese in mese. 

Quando si esamina il contenuto totale scaricato e distribuito in un periodo di 12 mesi per l'installazione non rapida, la versione 1803 senza UUP dovrebbe essere approssimativamente pari alla 1809 con UUP e, dopo questo punto di non ritorno, il contenuto totale scaricato e distribuito per l'intera durata della versione è inferiore nella versione 1809 con UUP. Per l'installazione rapida, il punto critico si riscontra prima come con la versione 1809. L'installazione rapida è solo per gli aggiornamenti delle funzionalità e non per l'aggiornamento cumulativo, di conseguenza il contenuto del server di grandi dimensioni si riscontra una sola volta per versione anziché mensilmente.

#### <a name="supported-content-channels"></a>Canali di contenuto supportati
Per l'anteprima, eseguire il test negli ambienti aziendali reali. UUP supporterà tutti i canali di contenuto, tra cui:
- Ottimizzazione recapito di Windows
- Peer cache di Configuration Manager
- Windows BranchCache
- Distribuire senza eseguire il download nel server (senza pacchetti di distribuzione) per scaricare direttamente da Microsoft Update. Se si usa Microsoft Update, è consigliabile usare in combinazione Ottimizzazione recapito.
- Provider di contenuti alternativi di terze parti

Per altre informazioni, vedere [FAQs to optimize Windows 10 update delivery](/sccm/sum/deploy-use/optimize-windows-10-update-delivery) (FAQ per ottimizzare il recapito degli aggiornamenti di Windows 10).

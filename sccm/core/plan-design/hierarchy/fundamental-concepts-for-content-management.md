---
title: Concetti di base della gestione dei contenuti | Microsoft Docs
description: "È possibile usare gli strumenti e le opzioni di System Center Configuration Manager per gestire il contenuto da distribuire."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c201be2a-692c-4d67-ac95-0a3afa5320fe
caps.latest.revision: 28
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1a4a9da88caba55d9e340c7fb1f31f4e3b957f3e
ms.openlocfilehash: 577d7e3acc27e3b50e22fc42d5db2f68d9cdde29


---
# <a name="fundamental-concepts-for-content-management-in-system-center-configuration-manager"></a>Concetti di base per la gestione dei contenuti in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager supporta un solido sistema di strumenti e opzioni per gestire i contenuti distribuiti, ad esempio applicazioni, pacchetti, aggiornamenti software e sistemi operativi.  

 Il contenuto distribuito viene archiviato in entrambi i server del sito e nei server del sistema del sito del punto di distribuzione. Questo contenuto può richiedere una grande quantità di larghezza di banda di rete durante il trasferimento tra i percorsi.  Per pianificare e usare l'infrastruttura di gestione dei contenuti in modo efficace, è necessario conoscere le configurazioni e le opzioni disponibili e quindi valutare come usarle affinché possano adattarsi in modo ottimale all'ambiente di rete e alle esigenze per la distribuzione dei contenuti.  

Di seguito sono riportati i concetti di base sulla gestione dei contenuti. Se per un concetto sono necessarie informazioni aggiuntive o più complete, vengono forniti collegamenti a tali informazioni.  

## <a name="accounts-used-for-content-management"></a>Account usati per la gestione dei contenuti  
 Con la gestione dei contenuti è possibile usare gli account seguenti:  

-   **Account di accesso alla rete**: usato dai client per connettersi a un punto di distribuzione e accedere al contenuto. Per impostazione predefinita, i client proveranno prima a usare l'account del proprio computer  

     Questo account viene anche usato dai punti di distribuzione pull per ottenere il contenuto da un punto di distribuzione di origine in una foresta remota  

-   **Account di accesso ai pacchetti**: per impostazione predefinita, Configuration Manager concede l'accesso al contenuto in un punto di distribuzione agli account di accesso generici Users e Administrators. È tuttavia possibile configurare autorizzazioni aggiuntive per limitare l'accesso.   

-   **Account di connessione multicast** : usato per le distribuzioni di sistemi operativi  

Per altre informazioni sugli account, vedere [Gestire gli account per l'accesso al contenuto](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).

## <a name="bandwidth-throttling-and-scheduling"></a>Limitazione e pianificazione della larghezza di banda della rete  
 Le opzioni di limitazione e pianificazione della larghezza di banda della rete consentono di controllare la distribuzione del contenuto da un server del sito ai punti di distribuzione. Queste opzioni sono simili, ma non direttamente correlate, ai controlli della larghezza di banda per la replica da sito a sito basata su file.  

 Per altre informazioni, vedere [Gestire la larghezza di banda di rete](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).

## <a name="binary-differential-replication"></a>Replica differenziale binaria  
 La replica differenziale binaria, nota anche come replica differenziale, è un prerequisito dei punti di distribuzione che viene usato automaticamente per ridurre l'uso della larghezza di banda quando si distribuiscono gli aggiornamenti al contenuto distribuito in precedenza ad altri siti o punti di distribuzione remoti.  

 La replica differenziale binaria consente di ridurre al minimo la larghezza di banda di rete usata per inviare aggiornamenti per il contenuto distribuito inviando nuovamente solo il contenuto nuovo o modificato anziché l'intero set di file di origine del contenuto ogni volta che viene apportata una modifica ai file.  

 Quando si usa la replica differenziale binaria, Configuration Manager consente di identificare le modifiche apportate ai file di origine per ogni set di contenuti distribuiti in precedenza.  

-   Quando i file nel contenuto di origine cambiano, Configuration Manager crea una nuova versione incrementale del set di contenuti e replica solo i file modificati nei siti di destinazione e nei punti di distribuzione. Un file è considerato modificato se viene rinominato, spostato o se il contenuto del file cambia. Ad esempio, se si sostituisce un singolo file del driver per un pacchetto di distribuzione del sistema operativo che è stato in precedenza distribuito in diversi siti, solo i file del driver modificati vengono replicati in questi siti di destinazione.  

-   Configuration Manager supporta fino a cinque versioni incrementali del set di contenuti prima di inviare nuovamente l'intero set di contenuti. Dopo il quinto aggiornamento, la successiva modifica del contenuto impostata fa sì che Configuration Manager crei una nuova versione del set di contenuto. Configuration Manager distribuisce quindi la nuova versione del set di contenuti per sostituire il set precedente e qualsiasi sua versione incrementale. Dopo che il nuovo set di contenuti è stato distribuito, modifiche incrementali successive ai file di origine vengono nuovamente replicate dalla replica differenziale binaria.  


La replica differenziale binaria è supportata tra ogni sito padre e figlio in una gerarchia. All'interno di un sito, la replica differenziale binaria è supportata tra il server del sito e i suoi punti di distribuzione. Questo supporto include punti di distribuzione pull, ma non punti di distribuzione basati su cloud. I punti di distribuzione basati su cloud non supportano la replica differenziale binaria per trasferire il contenuto.  

Le applicazioni usano sempre la replica differenziale binaria. Per i pacchetti, la replica differenziale binaria è facoltativa e non è attivata per impostazione predefinita. Per usare la replica differenziale binaria per i pacchetti, è necessario attivare questa funzionalità per ogni pacchetto. A questo scopo, selezionare l'opzione **Abilita replica differenziale binaria** quando si crea un nuovo pacchetto o quando si modifica la scheda **Origine dati** delle proprietà pacchetto.  

## <a name="branchcache"></a>BranchCache  
 Una tecnologia Windows che consente ai client che supportano BranchCache e hanno scaricato una distribuzione configurata per BranchCache di agire da origine di contenuto per altri client abilitati per BranchCache.  

 Ad esempio, quando il primo computer client abilitato per BranchCache richiede il contenuto da un punto di distribuzione con Windows Server 2012 e configurato come server BranchCache, il computer client scarica tale contenuto e lo memorizza nella cache.  

-   Il computer client può quindi rendere disponibile il contenuto per altri client abilitati per BranchCache nella stessa subnet, che a sua volta memorizza il contenuto nella cache.  

-   In tal modo, client successivi sulla stessa subnet non devono scaricare contenuto dal punto di distribuzione e il contenuto viene distribuito tra più client per trasferimenti futuri.  

## <a name="peer-cache"></a>Peer cache
A partire dalla versione 1610, la peer cache del client consente di gestire la distribuzione di contenuti ai client in percorsi remoti. La peer cache è una soluzione di Configuration Manager integrata che consente ai client di condividere i contenuti con altri client direttamente dalla cache locale.

Dopo aver distribuito le impostazioni client che abilitano la peer cache per una raccolta, i membri di tale raccolta possono fungere da origine di contenuto peer per altri client nello stesso gruppo di limiti.

Per altre informazioni, vedere [Peer cache per i client di Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).


## <a name="windows-pe-peer-cache"></a>Peer cache di Windows PE
Quando si distribuisce un nuovo sistema operativo in System Center Configuration Manager, i computer che eseguono la sequenza di attività possono usare la peer cache di Windows PE per ottenere contenuto da un peer locale (un'origine peer cache) anziché scaricarlo da un punto di distribuzione. In tal modo il traffico WAN viene ridotto al minimo negli scenari con le filiali, in cui non esiste un punto di distribuzione locale.

Per altre informazioni, vedere [Peer cache di Windows PE](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).


## <a name="client-locations"></a>Posizioni dei client  
 Di seguito sono elencate le posizioni da cui i client accedono al contenuto:  

-   **Intranet** (locale):  

    -   I punti di distribuzione possono usare HTTP o HTTPS  

    -   Usare i punti di distribuzione basati su cloud solo come opzione di fallback, se non sono disponibili punti di distribuzione locali  

-   **Internet**:  

    -   I punti di distribuzione devono accettare HTTPS  

    -   È possibile usare un punto di distribuzione basato su cloud per il fallback  

-   **Gruppo di lavoro**:  

    -   I punti di distribuzione devono accettare HTTPS  

    -   È possibile usare un punto di distribuzione basato su cloud per il fallback  



## <a name="content-library"></a>Raccolta contenuto  
 Archivio a istanza singola del contenuto che Configuration Manager usa per ridurre la dimensione complessiva del corpo combinato del contenuto distribuito.  

Altre informazioni sulla [raccolta contenuto](../../../core/plan-design/hierarchy/the-content-library.md).


## <a name="distribution-point"></a>Punto di distribuzione  
 Configuration Manager usa i punti di distribuzione per memorizzare i file necessari per l'esecuzione del software nei computer client. I client devono avere accesso ad almeno un punto di distribuzione da cui scaricare i file relativi al contenuto da distribuire.  

 Il punto di distribuzione di base (non specializzato) è noto come punto di distribuzione standard.  Esistono due principali varianti nel punto di distribuzione standard:  

-   **Punto di distribuzione pull**: variante di un punto di distribuzione in cui il punto di distribuzione ottiene il contenuto da un altro punto di distribuzione (un punto di distribuzione di origine) con modalità analoghe a quelle dei client che scaricano il contenuto dai punti di distribuzione. I punti di distribuzione pull possono risultare utili per evitare i colli di bottiglia della larghezza di banda di rete che possono verificarsi quando il server del sito deve distribuire direttamente il contenuto a ogni punto di distribuzione.  [Usare un punto di distribuzione pull con System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

-   **Punto di distribuzione basato su cloud**: variante di un punto di distribuzione installata in Microsoft Azure. [Usare un punto di distribuzione basato sul cloud con System Center Configuration Manager](../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md).  


I punti di distribuzione standard supportano una gamma di configurazioni e funzionalità, quali la pianificazione e la limitazione della larghezza di banda della rete, PXE e multicast o i contenuti in versione di preproduzione.  

-   Per controllare il trasferimento è possibile usare controlli come le **pianificazioni** o la **limitazione della larghezza di banda**.  

-   È anche possibile usare altre opzioni, inclusi i **contenuti in versione di preproduzione**, i **punti di distribuzione pull** o **BranchCache** per ridurre la larghezza di banda di rete usata per la distribuzione dei contenuti.  

-   I punti di distribuzione supportano diverse configurazioni come **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** e **[Multicast](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)** per le distribuzioni di sistemi operativi o configurazioni per il supporto dei **dispositivi mobili**  

 I punti di distribuzione pull e basati su cloud supportano molte di queste configurazioni, ma presentano limitazioni specifiche per ogni variante del punto di distribuzione.  

## <a name="distribution-point-group"></a>Gruppo di punti di distribuzione  
 Raggruppamento logico di punti di distribuzione che può semplificare la distribuzione del contenuto.  

 Per altre informazioni, vedere [Gestire i gruppi di punti di distribuzione](../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).

## <a name="distribution-point-priority"></a>Priorità dei punti di distribuzione  
 Il valore di priorità del punto di distribuzione è basato sul tempo impiegato per trasferire le distribuzioni precedenti al punto di distribuzione.  

-   Si tratta di un valore con ottimizzazione automatica assegnato a un punto di distribuzione che consente a Configuration Manager di trasferire il contenuto a più punti di distribuzione in un periodo di tempo più breve  

-   Quando si distribuisce contenuto a più punti di distribuzione contemporaneamente o a un gruppo di punti di distribuzione, il contenuto viene inviato da Configuration Manager al punto di distribuzione con la priorità più alta, prima che lo stesso contenuto venga inviato a un punto di distribuzione con una priorità più bassa.  

-   Questo valore non sostituisce la priorità di distribuzione dei pacchetti, che rimane il fattore decisivo nella sequenza di trasferimento delle diverse distribuzioni  


**Ad esempio** , se si distribuisce un contenuto caratterizzato da una priorità di distribuzione alta in un punto di distribuzione con una priorità bassa, il pacchetto di distribuzione con priorità alta viene sempre trasferito prima di un pacchetto con una priorità di distribuzione più bassa. La priorità di distribuzione è valida anche se i pacchetti che presentano una priorità di distribuzione inferiore vengono distribuiti a punti di distribuzione con priorità più alte. La priorità di distribuzione alta del pacchetto garantisce che il contenuto venga distribuito da Configuration Manager ai punti di distribuzione applicabili prima dell'invio di eventuali pacchetti con una priorità di distribuzione più bassa.  

> [!NOTE]  
>  I punti di distribuzione pull usano anche un concetto di priorità per ordinare la sequenza dei punti di distribuzione di origine.  
>   
>  -   La priorità dei punti di distribuzione per i trasferimenti di contenuto al punto di distribuzione è diversa dalla priorità usata dai punti di distribuzione pull durante la ricerca di contenuto da un punto di distribuzione di origine  
>  -   Per altre informazioni, vedere [Usare un punto di distribuzione pull con System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).  


## <a name="fallback"></a>Fallback  
 A partire dalla versione 1610, sono stati modificati alcuni concetti relativi a come i client individuano un punto di distribuzione con contenuto, fallback compreso. Fare riferimento alle informazioni seguenti in base alla versione che si sta usando:

**Versione 1610 e versioni successive:**   
I client che non riescono a individuare il contenuto da un punto di distribuzione associato al gruppo limite corrente possono eseguire il fallback per usare i percorsi di origine del contenuto associati a gruppi di limiti adiacenti. Per essere usato per il fallback, un gruppo di limiti adiacente deve avere una relazione definita con il gruppo di limiti corrente del client. Questa relazione include un tempo configurato oltre il quale un client che non riesce a individuare contenuto localmente può includere nella ricerca origini di contenuto dal gruppo di limiti adiacente.

I concetti di punti di distribuzione preferiti non sono più usati e le impostazioni per Consenti percorso origine di fallback per il contenuto, non sono più disponibili o applicate.

Per altre informazioni, vedere [Gruppi di limiti](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).


**Versione 1511, 1602 e 1606:**   
Le impostazioni di fallback sono correlate all'uso di **punti di distribuzione preferiti** e al percorso di origine del contenuto usati dai client.

-   Per impostazione predefinita, i client scaricano il contenuto solo da un punto di distribuzione preferito (associato ai gruppi di limiti del client)  

-   Tuttavia, quando un punto di distribuzione è configurato con l'opzione **Consenti ai client di utilizzare un percorso origine di fallback per il contenuto**, il punto di distribuzione è disponibile solo come origine di contenuto valida per qualsiasi client che non può ottenere una distribuzione da uno dei punti di distribuzione preferiti.  


Per informazioni sulle varie posizioni del contenuto e sugli scenari di fallback, vedere gli [scenari del percorso di origine del contenuto](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). Per informazioni sui gruppi di limiti, vedere [Boundary groups for versions 1511,1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) (Gruppi di limiti per le versioni 1511, 1602 e 1606).

## <a name="network-bandwidth"></a>Larghezza di banda di rete  
 Per gestire la quantità di larghezza di banda di rete usata per la distribuzione del contenuto, è possibile usare le opzioni seguenti:  

-   Usare i contenuti in versione di preproduzione: un processo di trasferimento del contenuto in un punto di distribuzione che non si basa su Configuration Manager per distribuire il contenuto nella rete.  

-   Usare la pianificazione e la limitazione della larghezza di banda della rete: configurazioni che consentono di controllare la modalità e le tempistiche di distribuzione del contenuto ai punti di distribuzione.  

Per altre informazioni, vedere [Gestire la larghezza di banda di rete](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).

## <a name="network-connection-speed-to-content-source"></a>Velocità di connessione di rete nell'origine del contenuto  
A partire dalla versione 1610, sono stati modificati alcuni concetti relativi a come i client individuano un punto di distribuzione con contenuto, compresa la velocità di connessione di rete a un'origine di contenuto. Fare riferimento alle informazioni seguenti in base alla versione che si sta usando:

**Versione 1610 e versioni successive:**   
Le velocità di connessione di rete che definiscono un punto di distribuzione come **Veloce** o **Lento** non vengono più usate. Al contrario, ogni sistema del sito associato a un gruppo limite viene trattato ugualmente.

Per altre informazioni, vedere [Gruppi di limiti](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).


**Versione 1511, 1602 e 1606:**   

 In un gruppo di limiti è possibile configurare la velocità di connessione di rete di ciascun punto di distribuzione:  

-   I client usano questo valore quando si connettono al punto di distribuzione  
-   Per impostazione predefinita, la velocità di connessione di rete è configurata come **Veloce**, ma è possibile impostarla anche come **Lenta**  
-   La **velocità di connessione di rete** e una configurazione della distribuzione determinano se per un client incluso in un gruppo di limiti associato è possibile scaricare il contenuto da un punto di distribuzione  

Per informazioni sulle varie posizioni del contenuto e sugli scenari di fallback, vedere gli [scenari del percorso di origine del contenuto](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). Per informazioni sui gruppi di limiti, vedere [Boundary groups for versions 1511,1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) (Gruppi di limiti per le versioni 1511, 1602 e 1606).

## <a name="on-demand-content-distribution"></a>Distribuzione di contenuto su richiesta  
 Opzione che è possibile impostare per singoli pacchetti e applicazioni (distribuzioni) per abilitare la distribuzione del contenuto su richiesta ai punti di distribuzione preferiti.  

-   Per abilitare questa opzione per una distribuzione, abilitare **Distribuisci il contenuto del pacchetto nei punti di distribuzione preferiti**  

-   Quando questa opzione è abilitata per una distribuzione e un client prova a richiedere un contenuto non disponibile in uno qualsiasi dei punti di distribuzione preferiti dei client, Configuration Manager automaticamente distribuisce tale contenuto ai punti di distribuzione preferiti dei client  

-   In questo modo, viene attivata la distribuzione automatica del contenuto a tali punti di distribuzione preferiti dei client da parte di Configuration Manager, tuttavia il client può comunque ottenere il contenuto da altri punti di distribuzione prima che i punti di distribuzione preferiti per il client ricevano la distribuzione. In questo caso, il contenuto sarà presente nel punto di distribuzione per l'uso da parte del client successivo che cerca quella specifica distribuzione  

Se si usa la versione 1610 o versioni successive, vedere [Gruppi di limiti](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).
Se si usano le versioni 1511, 1602 o 1606, vedere [Scenari del percorso di origine del contenuto](../../../core/plan-design/hierarchy/content-source-location-scenarios.md) per informazioni sui vari percorsi del contenuto e sugli scenari di fallback.  



## <a name="package-transfer-manager"></a>Package Transfer Manager  
 Componente del server del sito che trasferisce il contenuto ai punti di distribuzione in altri computer.  

 Altre informazioni su [Package Transfer Manager](../../../core/plan-design/hierarchy/package-transfer-manager.md).  

## <a name="preferred-distribution-point"></a>Punto di distribuzione preferito  
 Un punto di distribuzione preferito include punti di distribuzione associati a gruppi di limiti correnti del client.  

 È possibile associare uno o più gruppi di limiti a ogni punto di distribuzione:  

-   Questa associazione consente al client di identificare i punti di distribuzione da cui può scaricare il contenuto  
-   Per impostazione predefinita, i client possono scaricare il contenuto solo da un punto di distribuzione preferito  


Per ulteriori informazioni:
 - Se si usa la versione 1610 o versioni successive, vedere [Gruppi di limiti](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).
 - Se si usa la versione 1511, 1602 o 1606, vedere [scenari del percorso di origine del contenuto](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).

## <a name="prestage-content"></a>Pre-installare il contenuto  
 Processo di trasferimento del contenuto in un punto di distribuzione che non si basa su Configuration Manager per distribuire il contenuto nella rete.  

 Per altre informazioni, vedere [Gestire la larghezza di banda di rete](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



<!--HONumber=Dec16_HO3-->



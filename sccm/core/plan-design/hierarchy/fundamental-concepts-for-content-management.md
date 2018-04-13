---
title: Concetti di base della gestione dei contenuti
titleSuffix: Configuration Manager
description: È possibile usare gli strumenti e le opzioni di Configuration Manager per gestire il contenuto da distribuire.
ms.custom: na
ms.date: 03/22/2018
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
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0595e34d096b2d7f6450b3255bae03ae3aa57862
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2018
---
# <a name="fundamental-concepts-for-content-management-in-system-center-configuration-manager"></a>Concetti di base per la gestione dei contenuti in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Configuration Manager supporta un solido sistema di strumenti e opzioni per gestire i contenuti distribuiti, ad esempio distribuzioni di applicazioni, pacchetti, aggiornamenti software e sistemi operativi. Configuration Manager archivia il contenuto sia sui server del sito che sui punti di distribuzione. Questo contenuto richiede una grande quantità di larghezza di banda di rete durante il trasferimento tra i percorsi. Per pianificare e usare efficacemente l'infrastruttura di gestione dei contenuti, è consigliabile comprendere le opzioni disponibili e le configurazioni. Quindi valutare come usarle per adattare al meglio l'ambiente di rete e le esigenze di distribuzione del contenuto.  

> [!TIP]    
> Per ulteriori informazioni sul processo di distribuzione del contenuto e per informazioni sulla diagnosi e la risoluzione dei problemi di distribuzione del contenuto generale, vedere [Comprensione e risoluzione dei problemi di distribuzione del contenuto in Configuration Manager](https://support.microsoft.com/help/4000401/content-distribution-in-mcm).

Di seguito sono riportati gli argomenti che rappresentano i concetti di base per la gestione dei contenuti. Se per un concetto sono necessarie informazioni aggiuntive o più complete, vengono forniti collegamenti a tali informazioni.



## <a name="accounts-used-for-content-management"></a>Account usati per la gestione dei contenuti  
 Con la gestione dei contenuti è possibile usare gli account seguenti:  

-   **Account di accesso alla rete**: usato dai client per connettersi a un punto di distribuzione e accedere al contenuto. Per impostazione predefinita, l'account computer viene usato per primo.  

     Questo account viene usato anche dai punti di distribuzione pull per scaricare contenuto da un punto di distribuzione di origine in una foresta remota.  

-   **Account di accesso ai pacchetti**: per impostazione predefinita, Configuration Manager concede l'accesso al contenuto in un punto di distribuzione agli account di accesso generici Utenti e Amministratori. È tuttavia possibile configurare autorizzazioni aggiuntive per limitare l'accesso.   

-   **Account di connessione multicast**: usato per le distribuzioni del sistema operativo.  

Per altre informazioni sugli account, vedere [Gestire gli account per l'accesso al contenuto](../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md).



## <a name="bandwidth-throttling-and-scheduling"></a>Limitazione e pianificazione della larghezza di banda della rete  
 Le opzioni di limitazione e pianificazione della larghezza di banda della rete consentono di controllare la distribuzione del contenuto da un server del sito ai punti di distribuzione. Queste funzionalità sono simili, ma non direttamente correlate, ai controlli della larghezza di banda per la replica da sito a sito basata su file.  

 Per altre informazioni, vedere [Gestire la larghezza di banda di rete](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



## <a name="binary-differential-replication"></a>Replica differenziale binaria  
 La replica differenziale binaria (BDR) è un prerequisito per i punti di distribuzione. È nota talvolta come replica differenziale. Quando si distribuiscono aggiornamenti al contenuto distribuito in precedenza ad altri siti o ai punti di distribuzione remoti, la replica differenziale binaria viene usata automaticamente per ridurre la larghezza di banda.  

 La replica differenziale binaria riduce al minimo la larghezza di banda di rete usata per inviare aggiornamenti per il contenuto distribuito. Invia nuovamente solo il contenuto nuovo o modificato anziché inviare l'intero set di file di origine del contenuto ogni volta che si modificano tali file.  

 Quando si usa la replica differenziale binaria, Configuration Manager consente di identificare le modifiche apportate ai file di origine per ogni set di contenuti distribuiti in precedenza.  

-   Quando i file nel contenuto di origine cambiano, il sito crea una nuova versione incrementale del set di contenuto, quindi replica solo i file modificati nei siti di destinazione e i punti di distribuzione. Un file è considerato modificato se viene rinominato, spostato o se il contenuto del file cambia. Ad esempio, se si sostituisce un singolo file del driver con un pacchetto di driver che è stato in precedenza distribuito in diversi siti, vengono replicati solo i file dei driver modificati.  

-   Configuration Manager supporta fino a cinque versioni incrementali del set di contenuti prima di inviare nuovamente l'intero set di contenuti. Dopo il quinto aggiornamento, la successiva modifica del set di contenuto fa sì che il sito crei una nuova versione del set di contenuto. Configuration Manager distribuisce quindi la nuova versione del set di contenuti per sostituire il set precedente e qualsiasi sua versione incrementale. Dopo che il nuovo set di contenuti è stato distribuito, modifiche incrementali successive ai file di origine vengono nuovamente replicate dalla replica differenziale binaria.  

La replica differenziale binaria è supportata tra ogni sito padre e figlio in una gerarchia. La replica differenziale binaria è supportata all'interno di un sito tra il server del sito e i suoi normali punti di distribuzione. Tuttavia, i punti di distribuzione pull e i punti di distribuzione basati sul cloud non supportano la replica differenziale binaria per trasferire il contenuto. I punti di distribuzione pull supportano i delta a livello di file e il trasferimento dei nuovi file, ma non i blocchi all'interno di un file.

Le applicazioni usano sempre la replica differenziale binaria. La replica differenziale binaria è facoltativa per i pacchetti e non è abilitata per impostazione predefinita. Per usare la replica differenziale binaria per i pacchetti, abilitare questa funzionalità per ogni pacchetto. Selezionare l'opzione **Abilita replica differenziale binaria** quando si crea o si modifica un pacchetto.   



## <a name="branchcache"></a>BranchCache  
 [BranchCache](/windows-server/networking/branchcache/branchcache) è una tecnologia di Windows. I client che supportano BranchCache e hanno scaricato una distribuzione configurata per BranchCache agiscono da origine di contenuto per altri client abilitati per BranchCache.  

 Ad esempio, è necessario un punto di distribuzione che esegue Windows Server 2012 o versione successiva ed è configurato come server BranchCache. Quando il primo client abilitato per BranchCache richiede un contenuto da questo server, il client scarica tale contenuto e lo memorizza nella cache.  

- Il client può quindi rendere disponibile il contenuto per altri client abilitati per BranchCache nella stessa subnet, che a sua volta memorizza il contenuto nella cache.  
- Altri client nella stessa subnet non devono scaricare contenuto dal punto di distribuzione.  
- Il contenuto viene distribuito tra più client per trasferimenti futuri.  



## <a name="delivery-optimization"></a>Ottimizzazione recapito
<!-- 1324696 -->
I gruppi di limiti di Configuration Manager consentono di definire e regolamentare la distribuzione del contenuto nella rete aziendale e negli uffici remoti. [Ottimizzazione recapito di Windows](/windows/deployment/update/waas-delivery-optimization) è una tecnologia peer-to-peer basata sul cloud per la condivisione di contenuti tra dispositivi Windows 10. A partire dalla versione 1802, è possibile configurare Ottimizzazione recapito in modo che usi i gruppi di limiti per la condivisione di contenuti tra peer. Le impostazioni del client applicano l'identificatore del gruppo di limiti come identificatore di gruppo di Ottimizzazione recapito sul client. Quando il client comunica con il servizio cloud Ottimizzazione recapito, usa questo identificatore per individuare i peer con il contenuto desiderato. Per altre informazioni, vedere impostazioni client per [ottimizzazione recapito](/sccm/core/clients/deploy/about-client-settings#delivery-optimization).



## <a name="peer-cache"></a>Peer cache
La peer cache client consente di gestire la distribuzione di contenuti ai client in posizioni remote. La peer cache è una soluzione integrata di Configuration Manager che consente ai client di condividere i contenuti con altri client direttamente dalla cache locale.

Dopo aver distribuito le impostazioni client che abilitano la peer cache per una raccolta, i membri di tale raccolta possono fungere da origine di contenuto peer per altri client nello stesso gruppo di limiti.

Per altre informazioni, vedere [Peer cache per i client di Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).



## <a name="windows-pe-peer-cache"></a>Peer cache di Windows PE
Quando si distribuisce un nuovo sistema operativo con Configuration Manager, i computer che eseguono la sequenza di attività possono usare la peer cache Windows PE. Scaricano contenuto da un'origine peer cache anziché da un punto di distribuzione. Questo comportamento contribuisce a ridurre al minimo il traffico WAN negli scenari con le filiali, in cui non esiste un punto di distribuzione locale.

Per altre informazioni, vedere [Peer cache di Windows PE](../../../osd/get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).



## <a name="client-locations"></a>Posizioni dei client  
 Di seguito sono elencate le posizioni da cui i client accedono al contenuto:  

-   **Intranet** (locale):  

    -   I punti di distribuzione possono usare HTTP o HTTPS.  

    -   Usare i punti di distribuzione basati sul cloud solo come opzione di fallback, se non sono disponibili punti di distribuzione locali.  

-   **Internet**:  

    -   I punti di distribuzione devono accettare HTTPS.  

    -   È possibile usare un punto di distribuzione basato sul cloud per il fallback.  

-   **Gruppo di lavoro**:  

    -   I punti di distribuzione devono accettare HTTPS.  

    -   È possibile usare un punto di distribuzione basato sul cloud per il fallback.  



## <a name="content-library"></a>Raccolta contenuto  
 La raccolta contenuto è l'archivio a istanza singola del contenuto in Configuration Manager. Questa raccolta consente di ridurre la dimensione complessiva del contenuto distribuito.  

- Altre informazioni sulla [raccolta contenuto](../../../core/plan-design/hierarchy/the-content-library.md).
- Usare lo [strumento per la pulizia della raccolta contenuto](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) per rimuovere il contenuto non più associato a un'applicazione.  



## <a name="distribution-points"></a>Punti di distribuzione  
 Configuration Manager usa i punti di distribuzione per memorizzare i file necessari per l'esecuzione del software nei computer client. I client devono avere accesso ad almeno un punto di distribuzione da cui scaricare i file relativi al contenuto da distribuire.  

 Il punto di distribuzione di base (non specializzato) è noto come punto di distribuzione standard. Esistono due principali varianti nel punto di distribuzione standard:  

-   **Punto di distribuzione pull**: variante di un punto di distribuzione in cui il punto di distribuzione ottiene il contenuto da un altro punto di distribuzione (punto di distribuzione di origine). Questo processo è simile al modo in cui i client scaricano contenuto dai punti di distribuzione. I punti di distribuzione pull possono risultare utili per evitare i colli di bottiglia della larghezza di banda di rete che si verificano quando il server del sito deve distribuire direttamente il contenuto a ogni punto di distribuzione. [Usare un punto di distribuzione pull](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

-   **Punto di distribuzione basato sul cloud**: variante di un punto di distribuzione installato in Microsoft Azure. [Apprendere l'uso di un punto di distribuzione basato sul cloud](../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md).  


I punti di distribuzione standard supportano una gamma di configurazioni e funzionalità:  

- Per controllare il trasferimento, usare controlli come le **pianificazioni** o la **limitazione della larghezza di banda**.  
- È anche possibile usare altre opzioni, tra cui il **contenuto pre-installazione** e i **punti di distribuzione pull** per ridurre al minimo e controllare il consumo della rete. 
- **BranchCache**, **peer cache** e **Ottimizzazione recapito** sono tecnologie peer-to-peer per ridurre la larghezza di banda di rete usata quando si distribuisce il contenuto.  
- Esistono diverse configurazioni per le distribuzioni del sistema operativo, quali **[PXE](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_PXEDistributionPoint)** e  **[Multicast](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_DPMulticast)**
- Opzioni per **dispositivi mobili**   
  
  
I punti di distribuzione pull e basati sul cloud supportano molte di queste configurazioni, ma presentano limitazioni specifiche per ogni variante del punto di distribuzione.  



## <a name="distribution-point-groups"></a>Gruppi di punti di distribuzione  
 I gruppi di punti di distribuzione sono raggruppamenti logici di punti di distribuzione che possono semplificare la distribuzione del contenuto.  

 Per altre informazioni, vedere [Gestire i gruppi di punti di distribuzione](../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage).



## <a name="distribution-point-priority"></a>Priorità dei punti di distribuzione  
 Il valore di priorità del punto di distribuzione è basato sul tempo impiegato per trasferire le distribuzioni precedenti al punto di distribuzione.  

-   Questo valore è automatico. È impostato su ogni punto di distribuzione per consentire a Configuration Manager di trasferire più rapidamente il contenuto a più punti di distribuzione.  

-   Quando si distribuisce contenuto a più punti di distribuzione contemporaneamente o a un gruppo di punti di distribuzione, il sito invia prima di tutto il contenuto al server con la priorità più alta. Quindi, invia lo stesso contenuto a un punto di distribuzione con una priorità più bassa.  

-   La priorità di un punto di distribuzione non sostituisce la priorità di distribuzione dei pacchetti. La priorità del pacchetto rimane il fattore decisivo di quando il sito invia contenuto diverso.  

Ad esempio, si consideri un pacchetto con una priorità pacchetto alta. Tale pacchetto viene distribuito a un server con una priorità dei punti di distribuzione bassa. Questo pacchetto a priorità alta viene trasferito sempre prima di un pacchetto con una priorità più bassa. La priorità del pacchetto si applica anche se il sito distribuisce pacchetti di priorità inferiore ai server con priorità del punto di distribuzione più alta.

La priorità alta del pacchetto garantisce che il contenuto venga distribuito da Configuration Manager ai punti di distribuzione prima dell'invio di eventuali pacchetti con una priorità più bassa.  

> [!NOTE]  
>  I punti di distribuzione pull usano anche un concetto di priorità per ordinare la sequenza dei punti di distribuzione di origine.  
>   
>  -   La priorità dei punti di distribuzione per trasferimenti di contenuto al server è diversa dalla priorità usata dai punti di distribuzione pull. I punti di distribuzione pull usano la loro priorità quando cercano il contenuto da un punto di distribuzione di origine.  
>  -   Per altre informazioni, vedere [Usare un punto di distribuzione pull](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).  



## <a name="fallback"></a>Fallback  
 Sono stati modificati alcuni aspetti in Configuration Manager Current Branch relativi al modo in cui i client individuano un punto di distribuzione con contenuto, fallback compreso. 

I client che non riescono a individuare il contenuto da un punto di distribuzione associato al gruppo limite corrente eseguono il fallback per usare i percorsi di origine del contenuto associati a gruppi di limiti adiacenti. Per essere usato per il fallback, un gruppo di limiti adiacente deve avere una relazione definita con il gruppo di limiti corrente del client. Questa relazione include un tempo configurato che deve trascorrere prima che un client che non riesce a individuare contenuto localmente possa includere nella ricerca origini di contenuto dal gruppo di limiti adiacente.

I concetti di punti di distribuzione preferiti non sono più usati e le impostazioni per **Consenti percorso origine di fallback per il contenuto** non sono più disponibili o applicate.

Per altre informazioni, vedere [Gruppi di limiti](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).

<!--
**Version 1511, 1602, and 1606**   
Fallback settings are related to the use of **preferred distribution points** and to content source locations that are used by clients.

-   By default, clients only download content from a preferred distribution point (one that is associated with the client's boundary groups).  

-   However, when a distribution point is configured with **Allow clients to use this site system as a fallback source location for content**, that distribution point is only offered as a valid content source to any client that can't get a deployment from one of its preferred distribution points.  

For information about the different content location and fallback scenarios, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). For information about boundary groups, see [Boundary groups for versions 1511,1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).
-->



## <a name="network-bandwidth"></a>Larghezza di banda di rete  
 Per gestire la quantità di larghezza di banda di rete usata per la distribuzione del contenuto, è possibile usare le opzioni seguenti:  

-   **Contenuto pre-installazione**: trasferimento del contenuto a un punto di distribuzione senza distribuire il contenuto nella rete.  

-   **Pianificazione e limitazione della larghezza di banda della rete**: configurazioni che consentono di controllare la modalità e le tempistiche di distribuzione del contenuto ai punti di distribuzione.  

Per altre informazioni, vedere [Gestire la larghezza di banda di rete](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).



## <a name="network-connection-speed-to-content-source"></a>Velocità di connessione di rete nell'origine del contenuto  
 Sono stati modificati alcuni aspetti in Configuration Manager Current Branch relativi al modo in cui i client individuano un punto di distribuzione con contenuto. Queste modifiche comprendono la velocità di rete verso un'origine di contenuto. 

Le velocità di connessione di rete che definiscono un punto di distribuzione come **Veloce** o **Lento** non vengono più usate. Al contrario, ogni sistema del sito associato a un gruppo di limiti viene trattato allo stesso modo.

Per altre informazioni, vedere [Gruppi di limiti](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).

<!--
**Version 1511, 1602, and 1606**   
 You can configure the network connection speed of each distribution point in a boundary group:  

-   Clients use this value when they connect to the distribution point.

-   By default, the network connection speed is configured as **Fast**, but it can also be set as **Slow**.  

-   The **network connection speed**, along with the configuration of a deployment, determine if a client can download content from a distribution point when the client is in an associated boundary group  

For information about the different content location and fallback scenarios, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md). For information about boundary groups, see [Boundary groups for versions 1511,1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).
-->



## <a name="on-demand-content-distribution"></a>Distribuzione di contenuto su richiesta  
 La distribuzione del contenuto su richiesta è un'opzione per singole distribuzioni di applicazioni e pacchetti. Questa opzione consente la distribuzione del contenuto su richiesta ai server preferiti.  

-   Per abilitare questa impostazione per una distribuzione, abilitare **Distribuisci il contenuto del pacchetto nei punti di distribuzione preferiti**.  

-   Quando questa opzione è abilitata per una distribuzione e un client prova a richiedere un contenuto non disponibile in uno qualsiasi dei punti di distribuzione preferiti dei client, Configuration Manager automaticamente distribuisce tale contenuto ai punti di distribuzione preferiti dei client.  

-   In questo modo viene attivata la distribuzione automatica del contenuto ai punti di distribuzione preferiti del client da parte di Configuration Manager e il client può ottenere tale contenuto da altri punti di distribuzione prima che i punti di distribuzione preferiti per il client ricevano la distribuzione. In questo caso, il contenuto sarà presente nel punto di distribuzione per l'uso da parte del client successivo che cerca quella specifica distribuzione.  

Per altre informazioni, vedere [Gruppi di limiti](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).

<!--
If you use version 1511, 1602, or 1606, see  [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md) for information about the different content location and fallback scenarios.
-->



## <a name="package-transfer-manager"></a>Package Transfer Manager  
 Componente del server del sito che trasferisce il contenuto ai punti di distribuzione in altri computer.  

 Per altre informazioni, vedere [Package Transfer Manager](../../../core/plan-design/hierarchy/package-transfer-manager.md).  



<!--
## Preferred distribution point  
 A preferred distribution point includes any distribution points that are associated with a client's current boundary groups.  

 You have the option to associate each distribution point with one or more boundary groups:  

-   This association helps the client identify distribution points from which it can download content.  
-   By default, clients can only download content from a preferred distribution point.  


For more information:
 - If you use version 1610 or later, see [Boundary groups](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).
 - If you use version 1511, 1602, or 1606, see [Content source location scenarios](../../../core/plan-design/hierarchy/content-source-location-scenarios.md).
-->



## <a name="prestage-content"></a>Pre-installare il contenuto  
 La pre-installazione del contenuto è un processo di trasferimento del contenuto a un punto di distribuzione senza distribuire il contenuto nella rete.  

 Per altre informazioni, vedere [Gestire la larghezza di banda di rete](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).

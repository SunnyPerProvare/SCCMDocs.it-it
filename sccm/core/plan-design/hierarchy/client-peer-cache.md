---
title: Peer cache del client | System Center Configuration Manager
description: Usare la peer cache per i percorsi di origine del contenuto del client quando si distribuiscono contenuti con System Center Configuration Manager.
ms.custom: na
ms.date: 7/3/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: ed6b65a1a5aabc0970cd0333cb033405cf6d2aea
ms.openlocfilehash: 94802680747a3d371716c1b345b2cba098150716
ms.contentlocale: it-it
ms.lasthandoff: 07/03/2017

---

# <a name="peer-cache-for-configuration-manager-clients"></a>Peer cache per i client di Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

A partire da System Center Configuration Manager versione 1610, è possibile usare la **peer cache** per gestire la distribuzione del contenuto ai client in posizioni remote. La peer cache è una soluzione integrata di Configuration Manager che consente ai client di condividere i contenuti con altri client direttamente dalla cache locale.   

> [!TIP]  
> Introdotti con la versione 1610, la peer cache e il dashboard Origini dati del client sono funzionalità di versioni non definitive. Per abilitarle, vedere [Usare le funzionalità di versioni non definitive degli aggiornamenti](/sccm/core/servers/manage/pre-release-features).

## <a name="overview"></a>Panoramica
Un client Peer Cache è un client Gestione configurazione che è in grado di usare Peer Cache. Un client Peer Cache che ha del contenuto che può condividere con altri client è un'origine di Peer Cache.
 -  Le impostazioni client possono essere usate per abilitare i client per l'uso della peer cache.
 -  Per condividere il contenuto come origine di Peer Cache, un client Peer Cache:
    -  Deve essere aggiunto a un dominio. Tuttavia, un client che non è aggiunto a un dominio può ottenere contenuto da un'origine di Peer Cache non aggiunta al dominio.
    -  Deve essere un membro del gruppo di limiti attuali del client che cerca il contenuto. Un client Peer Cache in un gruppo di limiti adiacenti non è incluso nel pool dei percorsi di origine del contenuto disponibili quando un client usa il fallback per cercare contenuti da un gruppo di limiti adiacente. Per altre informazioni sui gruppi di limiti correnti e adiacenti, vedere [Gruppi di limiti](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 - Qualsiasi tipo di contenuto conservato nella cache di un client di Configuration Manager può essere reso disponibile ad altri client tramite la peer cache.
 -  La peer cache non sostituisce l'uso di altre soluzioni come BranchCache, ma si affianca a esse per offrire più opzioni ed estendere le tradizionali soluzioni di distribuzione di contenuti, come i punti di distribuzione. Questa soluzione personalizzata è indipendente da BranchCache e quindi funziona anche se non si abilita o si usa Windows BranchCache.

### <a name="operations"></a>Operazioni

Dopo aver distribuito le impostazioni client che abilitano la peer cache a una raccolta, i membri di tale raccolta possono fungere da origine di contenuto peer per altri client nello stesso gruppo di limiti:
 -  Un client che agisce come origine contenuto peer invia un elenco di contenuti disponibili che ha memorizzato nella cache al suo punto di gestione.
 -  Quindi, quando il client successivo in tale gruppo di limiti richiede quel contenuto, ogni origine peer cache con quel contenuto viene restituita come una potenziale origine del contenuto con i punti di distribuzione e altri percorsi di origine del contenuto in tale gruppo di limiti.
 -  In base al normale processo operativo, il client in cerca del contenuto seleziona un'origine del contenuto dal pool di origini specificato e continua nel tentativo di ottenere il contenuto.

> [!NOTE]
> Se si verifica il fallback a un gruppo di limiti adiacente per il contenuto, i percorsi di origine del contenuto della peer cache del gruppo di limiti adiacente non vengono aggiunti al pool di potenziali percorsi di origine del contenuto del client.  


Anche se è possibile fare in modo che tutti i client partecipino come origine di peer cache, è consigliabile scegliere solo i client più adatti a essere origini di peer cache.  L'idoneità di un client può essere valutata in base a tipo di chassis, spazio su disco, connettività di rete e altri requisiti del client. Per altre informazioni utili per scegliere i client più adatti da usare per la peer cache, vedere [questo blog scritto da un consulente Microsoft](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

**Accesso limitato a un'origine di peer cache**  
A partire dalla versione 1702, il computer di origine della peer cache rifiuta le richieste di contenuti quando soddisfa una delle condizioni seguenti:  
  -  È in modalità di batteria in esaurimento.
  -  Il carico della CPU supera l'80% nel momento in cui il contenuto viene richiesto.
  -  L'I/O disco ha un valore di *AvgDiskQueueLength* superiore a 10.
  -  Non vi sono più connessioni disponibili al computer.   

È possibile configurare queste impostazioni tramite la classe WMI del server di configurazione client per la funzionalità dell'origine peer (*SMS_WinPEPeerCacheConfig*) quando si usa System Center Configuration Manager SDK.

Quando il computer rifiuta una richiesta di contenuto, il computer richiedente continuerà a cercare il contenuto da origini alternative nel pool dei percorsi di origine del contenuto disponibili.   



### <a name="monitoring"></a>monitoring   
Per capire come viene usata la peer cache, è possibile visualizzare il dashboard Origini dati del client. Vedere [Dashboard Origini dati del client](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).

A partire dalla versione 1702, è possibile usare tre report per visualizzare l'uso della peer cache. Nella console passare a **Monitoraggio** > **Creazione di report** > **Report**. Tutti i report hanno un tipo di **contenuto di distribuzione software**:
1.  **Rifiuto di contenuto di origine di peer cache**:  
Usare questo report per visualizzare informazioni sulla frequenza con cui le origini di peer cache in un gruppo di limiti hanno rifiutato una richiesta di contenuto.
 - **Problema noto**: quando si esegue il drill-down in risultati come *MaxCPULoad* o *MaxDiskIO*, è possibile che venga visualizzato un errore per segnalare che il report o i dettagli non possono essere trovati. Per risolvere questo problema, usare i due report seguenti che mostrano direttamente i risultati.

2. **Peer cache source content rejection by condition** (Rifiuto di contenuto di origine di peer cache - per condizione):  
Usare questo report per visualizzare i dettagli relativi al rifiuto per un tipo di rifiuto o un gruppo di limiti specificato. È possibile specificare quanto segue:

  - **Problema noto**: non è possibile selezionare i parametri disponibili, ma è necessario immetterli manualmente. Immettere i valori per *Nome del gruppo di limiti* e *Rejection Type* (Tipo di rifiuto) come mostrato nel primo report. Ad esempio, per *Rejection Type* (Tipo di rifiuto) è possibile immettere *MaxCPULoad* o *MaxDiskIO*.

3. **Peer cache source content rejection details** (Rifiuto di contenuto di origine di peer cache - dettagli):   
  Usare questo report per visualizzare informazioni sul contenuto richiesto al momento del rifiuto.

 - **Problema noto**: non è possibile selezionare i parametri disponibili, ma è necessario immetterli manualmente. Immettere il valore per *Rejection Type* (Tipo di rifiuto) come visualizzato nel primo report (Rifiuto di contenuto di origine di peer cache) e quindi immettere il valore di *ID risorsa* per l'origine di contenuto di cui visualizzare altre informazioni.  Per trovare l'ID risorsa dell'origine di contenuto:  

    1. Trovare il nome del computer visualizzato come *Origine di peer cache* nei risultati del secondo report, ossia Peer cache source content rejection by condition (Rifiuto di contenuto di origine di peer cache - per condizione).  
    2. Passare quindi ad **Asset e conformità** > **Dispositivi** e cercare il nome del computer. Usare il valore della colonna ID risorsa.  


## <a name="requirements-and-considerations-for-peer-cache"></a>Requisiti e considerazioni per la peer cache
-   È possibile usare la peer cache su qualsiasi sistema operativo Windows supportato come client di Configuration Manager. I sistemi operativi non Windows non sono supportati per la peer cache.

-   I client possono trasferire contenuti solo dai client della peer cache che si trovano nel relativo gruppo di limiti corrente.

-   Ogni sito in cui i client usano la peer cache deve essere configurato con un [account di accesso alla rete](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#a-namebkmknaaa-network-access-account). L'account viene usato dal computer di origine della peer cache per autenticare le richieste di download dai peer e richiede solo le autorizzazioni utente di dominio per questo scopo.

-   Poiché il limite corrente di un'origine del contenuto della peer cache è determinato dall'ultimo invio dell'inventario hardware di tale client, un client che si sposti in un percorso di rete in un gruppo di limiti diverso potrebbe comunque essere considerato un membro del suo gruppo di limiti precedente ai fini della peer cache. Di conseguenza, a un client potrebbe essere offerta un'origine del contenuto della peer cache che non si trova nel suo immediato percorso di rete. È consigliabile escludere dalla partecipazione all'origine della peer cache i client soggetti a questa configurazione.

## <a name="to-configure-client-peer-cache-client-settings"></a>Per configurare le impostazioni del client relative alla peer cache del client
1.  Nella console di Configuration Manager passare ad **Amministrazione** > **Impostazioni client** e aprire l'oggetto impostazioni client del dispositivo che si vuole usare. È possibile anche modificare l'oggetto Impostazioni client predefinite.
2.  Nell'elenco delle impostazioni disponibili selezionare **Client Cache Settings** (Impostazioni cache client).
3.  Impostare **Abilita il client di Configuration Manager nell'intero sistema operativo per condividere i contenuti** su **Sì**.
4.  Configurare le impostazioni seguenti per definire le porte da usare per la peer cache:  
  -  **Porta per la trasmissione di rete iniziale**
  -  **Abilita HTTPS per la comunicazione peer del client**
  -  **Porta per il download di contenuto da peer (HTTP/HTTPS)**

In ogni computer abilitato per la peer cache, se Windows Firewall è in uso verrà configurato da Configuration Manager per consentire l'uso delle porte configurate.


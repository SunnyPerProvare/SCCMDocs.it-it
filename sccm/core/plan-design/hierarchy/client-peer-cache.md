---
title: Peer cache per i client
titleSuffix: Configuration Manager
description: Usare la peer cache per i percorsi di origine del contenuto del client quando si distribuiscono contenuti con System Center Configuration Manager.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 86cd5382-8b41-45db-a4f0-16265ae22657
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b705a2cb8eccae3abe63c5de0680c712ab2e181e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
ms.locfileid: "32337803"
---
# <a name="peer-cache-for-configuration-manager-clients"></a>Peer cache per i client di Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

<!--1101436-->
Usare la **peer cache** per gestire la distribuzione di contenuti ai client in posizioni remote. La peer cache è una soluzione integrata di Configuration Manager che consente ai client di condividere i contenuti con altri client direttamente dalla cache locale.   

> [!TIP]  
> Questa funzionalità è stata introdotta per la prima volta nella versione 1610 come [versione non definitiva](/sccm/core/servers/manage/pre-release-features). A partire dalla versione 1710, questa funzionalità non è più in versione non definitiva.  


> [!Note]  
> Configuration Manager non abilita questa funzionalità facoltativa per impostazione predefinita. Pertanto sarà necessario abilitarla prima di poterla usare. Per altre informazioni, vedere [Abilitare le funzionalità facoltative degli aggiornamenti](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


## <a name="overview"></a>Panoramica
Un client Peer Cache è un client Gestione configurazione che è in grado di usare Peer Cache. Un client Peer Cache che ha del contenuto che può condividere con altri client è un'origine di Peer Cache.
 -  Le impostazioni client possono essere usate per abilitare i client per l'uso della peer cache.
 -  Per condividere il contenuto come origine di Peer Cache, un client Peer Cache:
    -  Deve essere aggiunto a un dominio. Tuttavia, un client che non è aggiunto a un dominio può ottenere contenuto da un'origine di Peer Cache non aggiunta al dominio.
    -  Deve essere un membro del gruppo di limiti attuali del client che cerca il contenuto. Quando un client usa il fallback per cercare contenuto da un gruppo di limiti vicino, nell'elenco dei percorsi di origine contenuto non è incluso un client peer cache di un gruppo di limiti vicino. Per altre informazioni sui gruppi di limiti correnti e adiacenti, vedere [Gruppi di limiti](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 - Il client di Configuration Manager conserva ogni tipo di contenuto nella cache che può essere usato da altri client tramite peer cache, ad esempio file di Office 365 e file di installazione rapida.<!--SMS.500850-->
 -  La peer cache non sostituisce l'uso di altre soluzioni, come BranchCache. Viene infatti usata insieme ad altre soluzioni per aumentare il numero delle possibili soluzioni tradizionali di distribuzione del contenuto, ad esempio i punti di distribuzione. La peer cache è una soluzione personalizzata che non dipende da BranchCache. Se si non abilita o non si usa Windows BranchCache, la peer cache funziona comunque.

### <a name="operations"></a>Operazioni

Per abilitare la peer cache, distribuire le impostazioni client a una raccolta. I membri di tale raccolta agiscono quindi da origine contenuto peer per altri client all'interno dello stesso gruppo di limiti.
 -  Un client che agisce come origine contenuto peer invia un elenco di contenuti disponibili che ha memorizzato nella cache al suo punto di gestione.
 -  Quando il client successivo in tale gruppo di limiti richiede il contenuto, ogni origine di peer cache contenente il contenuto e online viene restituita nell'elenco delle possibili origini contenuto. Questo elenco include anche i punti di distribuzione e altri percorsi di origine contenuto in tale gruppo di limiti.
 -  Nel processo normale, il client che cerca il contenuto seleziona un'origine dall'elenco specificato. A questo punto il client tenta di ottenere il contenuto.

> [!NOTE]
> Se il client esegue il fallback a un gruppo di limiti vicino per il contenuto, i percorsi di origine contenuto di peer cache del gruppo di limiti vicino non vengono aggiunti all'elenco di possibili percorsi di origine contenuto.  


È consigliabile scegliere solo i client più adatti come origini di peer cache. Valutare l'idoneità dei client in base ad attributi come il tipo di chassis, lo spazio su disco e la connettività di rete. Per altre informazioni utili per scegliere i client più adatti da usare per la peer cache, vedere [questo blog scritto da un consulente Microsoft](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

**Accesso limitato a un'origine di peer cache**  
A partire dalla versione 1702, il computer di origine della peer cache rifiuta le richieste di contenuto quando soddisfa una delle condizioni seguenti:  
  -  È in modalità di batteria in esaurimento.
  -  Il carico della CPU supera l'80% nel momento in cui il contenuto viene richiesto.
  -  L'I/O disco ha un valore di *AvgDiskQueueLength* superiore a 10.
  -  Non vi sono più connessioni disponibili al computer.   

Configurare queste impostazioni usando la classe WMI del server di configurazione client per la funzionalità dell'origine peer (*SMS_WinPEPeerCacheConfig*) in Configuration Manager SDK.

Quando il computer rifiuta una richiesta di contenuto, il computer richiedente continua a cercare il contenuto dall'elenco di percorsi di origine contenuto disponibili.   



### <a name="monitoring"></a>Monitoraggio   
Per capire come viene usata la peer cache, è possibile visualizzare il dashboard Origini dati del client. Vedere [Dashboard Origini dati del client](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).

A partire dalla versione 1702, è possibile usare tre report per visualizzare l'uso della peer cache. Nella console passare a **Monitoraggio** > **Creazione di report** > **Report**. Tutti i report hanno un tipo di **contenuto di distribuzione software**:
1.  **Rifiuto di contenuto di origine di peer cache**:  
Usare questo report per visualizzare informazioni sulla frequenza con cui le origini di peer cache in un gruppo di limiti rifiutano una richiesta di contenuto.
 - **Problema noto**: quando si esegue il drill-down in risultati come *MaxCPULoad* o *MaxDiskIO*, è possibile che venga visualizzato un errore per segnalare che il report o i dettagli non possono essere trovati. Per risolvere questo problema, usare i due report seguenti che illustrano direttamente i risultati.

2. **Peer cache source content rejection by condition** (Rifiuto di contenuto di origine di peer cache - per condizione):  
Usare questo report per visualizzare i dettagli relativi al rifiuto per un tipo di rifiuto o un gruppo di limiti specificato. È possibile specificare quanto segue:

  - **Problema noto**: non è possibile selezionare i parametri disponibili, ma è necessario immetterli manualmente. Immettere i valori per *Nome del gruppo di limiti* e *Rejection Type* (Tipo di rifiuto) come mostrato nel primo report. Ad esempio, per *Rejection Type* (Tipo di rifiuto) è possibile immettere *MaxCPULoad* o *MaxDiskIO*.

3. **Peer cache source content rejection details** (Rifiuto di contenuto di origine di peer cache - dettagli):   
  Usare questo report per visualizzare informazioni sul contenuto richiesto dal client al momento del rifiuto.

 - **Problema noto**: non è possibile selezionare i parametri disponibili, ma è necessario immetterli manualmente. Immettere il valore per *Rejection Type* (Tipo di rifiuto) come visualizzato nel report **Rifiuto di contenuto di origine di peer cache**. Immettere quindi il valore per *ID risorsa* per l'origine contenuto sulla quale si vogliono più informazioni. Per trovare l'ID risorsa dell'origine di contenuto:  

    1. Trovare il nome del computer visualizzato come *Origine di peer cache* nei risultati del report **Rifiuto di contenuto di origine di peer cache per condizione**.  
    2. Passare quindi ad **Asset e conformità** > **Dispositivi** e cercare il nome del computer. Usare il valore della colonna ID risorsa.  


## <a name="requirements-and-considerations-for-peer-cache"></a>Requisiti e considerazioni per la peer cache
-   È possibile usare la peer cache su qualsiasi sistema operativo Windows supportato come client di Configuration Manager. I sistemi operativi non Windows non sono supportati per la peer cache.

-   I client possono trasferire contenuti solo dai client della peer cache che si trovano nel relativo gruppo di limiti corrente.

-   Prima della versione 1706, ogni sito in cui i client usano la peer cache doveva essere configurato con un [account di accesso alla rete](/sccm/core/plan-design/hierarchy/manage-accounts-to-access-content#a-namebkmknaaa-network-access-account). A partire dalla versione 1706 tale account non è più necessario, con un'eccezione: vale a dire quando un client con peer cache abilitata esegue una sequenza di attività da Software Center e la sequenza di attività riavvia un'immagine d'avvio. In questo scenario per il client è ancora necessario un account di accesso alla rete. Quando il client si trova in Windows PE, usa l'account di accesso alla rete per ottenere il contenuto dall'origine di peer cache.

    Quando necessario, il computer di origine della peer cache usa l'account di accesso alla rete per autenticare le richieste di download dai peer. Per tale scopo, a questo account sono richieste solo le autorizzazioni utente di dominio.

-   L'ultimo invio dell'inventario hardware del client determina il limite corrente di un'origine contenuto della peer cache. Un client che si sposta in un gruppo di limiti diverso potrebbe comunque essere un membro del suo gruppo di limiti precedente ai fini della peer cache. Di conseguenza, a un client potrebbe essere offerta un'origine contenuto della peer cache che non si trova nel suo immediato percorso di rete. È consigliabile escludere dalla partecipazione all'origine della peer cache i client soggetti a questa configurazione.
-    A partire dalla versione 1706, il client di peer cache verifica che l'origine contenuto della peer cache sia online prima di tentare di scaricare il contenuto. <!--sms.498675-->

## <a name="to-configure-client-peer-cache-client-settings"></a>Per configurare le impostazioni del client relative alla peer cache del client
Per informazioni sulla configurazione delle impostazioni client, vedere [Impostazioni della cache dei client](/sccm/core/clients/deploy/about-client-settings#client-cache-settings). Per altre informazioni, vedere [Come configurare le impostazioni client](/sccm/core/clients/deploy/configure-client-settings).

Nei client con peer cache abilitata che usano Windows Firewall, Configuration Manager configura le porte del firewall specificate nelle impostazioni client.

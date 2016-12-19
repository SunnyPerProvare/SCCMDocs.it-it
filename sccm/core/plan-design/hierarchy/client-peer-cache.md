---
title: Peer cache del client | System Center Configuration Manager
description: Usare la peer cache per i percorsi di origine del contenuto del client quando si distribuiscono contenuti con System Center Configuration Manager.
ms.custom: na
ms.date: 12/05/2016
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
translationtype: Human Translation
ms.sourcegitcommit: 3329c3180899a4de96f5d9fed46f97744cf5e7da
ms.openlocfilehash: e983358e32502a130f95647a11cd73ff4bbef05f

---
# <a name="peer-cache-for-configuration-manager-clients"></a>Peer cache per i client di Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

A partire da System Center Configuration Manager versione 1610, è possibile usare la **peer cache** per gestire la distribuzione del contenuto ai client in posizioni remote. La peer cache è una soluzione di Configuration Manager integrata che consente ai client di condividere i contenuti con altri client direttamente dalla cache locale.   

> [!TIP]  
> Con la versione 1610, la peer cache e il dashboard Origini dati del client sono funzionalità di versioni non definitive. Per abilitarle, vedere [Usare le funzionalità di versioni non definitive degli aggiornamenti](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

 -  Le impostazioni client possono essere usate per abilitare i client per l'uso della peer cache.
 -  Per condividere il contenuto, i client della peer cache devono essere entrambi membri del gruppo di limiti corrente del client in cerca del contenuto. I client della peer cache in gruppi di limiti adiacenti non sono inclusi con il pool dei percorsi di origine del contenuto disponibili quando un client usa il fallback per cercare contenuti da un gruppo di limiti adiacente. Per altre informazioni sui gruppi di limiti correnti e adiacenti, vedere [Gruppi di limiti](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups##a-namebkmkboundarygroupsa-boundary-groups).
 -  Qualsiasi tipo di contenuto conservato nella cache di un client di Configuration Manager può essere servito ad altri client che usano la peer cache.
 -  La peer cache non sostituisce l'uso di altre soluzioni come BranchCache, ma si affianca a esse per offrire più opzioni che estendono le soluzioni di distribuzione di contenuti tradizionali come i punti di distribuzione. Questa soluzione può essere usata anche come soluzione personalizzata indipendente da BranchCache, se non si abilita o non si usa Windows BranchCache.

Dopo aver distribuito le impostazioni client che abilitano la peer cache a una raccolta, i membri di tale raccolta possono fungere da origine di contenuto peer per altri client nello stesso gruppo di limiti:
 -  Un client che agisce come origine di contenuto peer invia un elenco di contenuti disponibili che ha memorizzato nella cache al suo punto di gestione.
 -  Quindi, quando il client successivo in tale gruppo di limiti richiede quel contenuto, ogni origine peer cache con quel contenuto viene restituita come una potenziale origine del contenuto con i punti di distribuzione e altri percorsi di origine del contenuto in tale gruppo di limiti.
 -  In base al normale processo operativo, il client in cerca del contenuto seleziona un'origine del contenuto dal pool di origini che viene fornito e continua nel tentativo di ottenere il contenuto.
 -  Se si verifica il fallback a un gruppo di limiti adiacente per il contenuto, i percorsi di origine del contenuto della peer cache del gruppo di limiti adiacente non vengono aggiunti al pool di potenziali percorsi di origine del contenuto del client.  

Anche se è possibile fare in modo che tutti i client partecipino alla peer cache, è consigliabile scegliere solo i client più adatti per essere origini di peer cache.  L'idoneità di un client può essere valutata in base a tipo di chassis, spazio su disco, connettività di rete e altri requisiti del client. Per altre informazioni utili per determinare la scelta dei client migliori da usare per la peer cache, vedere [questo blog di un consulente Microsoft](https://blogs.technet.microsoft.com/setprice/2016/06/29/pe-peer-cache-custom-reporting-examples/).

Per capire come viene usata la peer cache, è possibile visualizzare il dashboard Origini dati del client. Vedere [Dashboard Origini dati del client](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).


## <a name="requirements-and-considerations-for-peer-cache"></a>Requisiti e considerazioni per la peer cache:
- È necessario configurare il sito con un **Account di accesso alla rete** con **Controllo completo** per la cartella della cache in ogni client. Per impostazione predefinita, si tratta di ***%windir%\ccmcache***.

- I client possono trasferire contenuti solo dai client della peer cache che si trovano nel relativo gruppo di limiti corrente.

-   Poiché il limite corrente di un'origine del contenuto della peer cache è determinato dall'ultimo invio dell'inventario hardware di tale client, un client che si sposti in un percorso di rete in un gruppo di limiti diverso potrebbe comunque essere considerato un membro del suo gruppo di limiti precedente ai fini della peer cache. Di conseguenza, a un client potrebbe essere offerta un'origine del contenuto della peer cache che non si trova nel suo immediato percorso di rete. È consigliabile escludere dalla partecipazione alla peer cache i client soggetti a questa configurazione.

## <a name="to-configure-client-peer-cache-client-settings"></a>Per configurare le impostazioni del client relative alla peer cache del client
1.  Nella console di Configuration Manager passare ad **Amministrazione** > **Impostazioni client** e aprire l'oggetto impostazioni client del dispositivo che si vuole usare. È possibile anche modificare l'oggetto Impostazioni client predefinite.
2.  Nell'elenco delle impostazioni disponibili selezionare **Impostazioni della cache del client**.
3.  Impostare **Abilita il client di Configuration Manager nell'intero sistema operativo per condividere i contenuti** su **Sì**.
4.  Configurare le impostazioni seguenti per definire le porte da usare per la peer cache:  
  -  **Porta per la trasmissione di rete iniziale**
  -  **Abilita HTTPS per la comunicazione peer del client**
  -  **Porta per il download di contenuto da peer (HTTP/HTTPS)**

In ogni computer abilitato per la peer cache, se Windows Firewall è in uso verrà configurato da Configuration Manager per consentire l'uso delle porte configurate.



<!--HONumber=Dec16_HO3-->


---
title: "Interoperabilità tra versioni diverse di Configuration Manager | Microsoft Docs"
description: "Informazioni su come evitare i conflitti tra più gerarchie di System Center Configuration Manager nella stessa rete."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
caps.latest.revision: 8
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 6ed317d45d90758832d4157985dd95d5e253c6fc
ms.openlocfilehash: 32182f06a90d768c40e29ed8a8e89cb45114bd15


---
# <a name="interoperability-between-different-versions-of-system-center-configuration-manager"></a>Interoperabilità tra versioni diverse di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Sono possibili l'installazione e il funzionamento di più gerarchie indipendenti di System Center Configuration Manager all'interno della stessa rete. Tuttavia, dal momento che più gerarchie di Configuration Manager non interagiscono al di fuori della migrazione, per ogni gerarchia sono necessarie configurazioni che impediscano conflitti reciproci. È inoltre possibile effettuare determinate configurazioni per consentire alle risorse gestite di interagire con i sistemi del sito dalla gerarchia corretta.  

 Nelle seguenti sezioni vengono fornite informazioni sull'utilizzo di diverse versioni di Configuration Manager nella stessa rete:  

-   [Interoperabilità tra System Center Configuration Manager e le versioni precedenti del prodotto](#BKMK_SupConfigInterop)  

-   [Interoperabilità per la Console di Configuration Manager](#BKMK_ConsoleInterop)  

-   [Limitazioni di Configuration Manager in una gerarchia con più versioni](#bkmk_mixed)  

##  <a name="a-namebkmksupconfiginteropa-interoperability-between-system-center-configuration-manager-and-earlier-product-versions"></a><a name="BKMK_SupConfigInterop"></a> Interoperabilità tra System Center Configuration Manager e le versioni precedenti del prodotto  
 Eccetto durante il processo di aggiornamento da System Center Configuration Manager 2012 a System Center Configuration Manager o da una versione di System Center Configuration Manager a una versione più recente (tramite aggiornamenti nella console), siti di versioni diverse non possono coesistere nella stessa gerarchia.  

 Dal momento che è possibile distribuire un sito e una gerarchia di System Center Configuration Manager nella stessa destinazione di un sito o di una gerarchia di System Center Configuration Manager 2012, è necessario impedire ai client delle due versioni di entrare a far parte di un sito dell'altra versione. Se, ad esempio, due o più gerarchie di Configuration Manager hanno limiti sovrapposti (vedere [About overlapping boundaries](../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md#BKMK_BoundaryOverlap) (Informazioni sui limiti sovrapposti)) che includono gli stessi percorsi di rete, la procedura consigliata è di assegnare ogni nuovo client a un sito specifico anziché usare l'assegnazione sito automatica. Per informazioni sull'assegnazione sito automatica in System Center Configuration Manager 2012, vedere [How to assign clients to a site in System Center Configuration Manager](../../../core/clients/deploy/assign-clients-to-a-site.md) (Come assegnare i client a un sito in System Center Configuration Manager).  

 Non è poi supportata l'installazione di un client di System Center Configuration Manager 2012 in un computer che ospita un ruolo del sistema del sito di System Center Configuration Manager, né l'installazione di un client di System Center Configuration Manager in un computer che ospita un ruolo del sistema del sito di System Center Configuration Manager 2012.  

 Analogamente, non sono supportati i client seguenti e la connessione di rete privata virtuale (VPN) seguente:  

-   Client di System Center Configuration Manager 2012 o versioni precedenti del client computer  

-   Client di System Center Configuration Manager 2012 o versioni precedenti del client di gestione di dispositivi  

-   Client per la gestione dispositivi Windows CE Platform Builder (qualsiasi versione)  

-   Connessione VPN di System Center Mobile Device Manager  

###  <a name="a-namebkmksupconfigsiteassignmenta-client-site-assignment-considerations"></a><a name="BKMK_SupConfigSiteAssignment"></a> Considerazioni sull'assegnazione sito dei client  
 I client di System Center Configuration Manager possono essere assegnati a un unico sito primario. Quando si usa l'assegnazione sito automatica per assegnare i client a un sito durante l'installazione client, quando più di un gruppo di limiti contiene lo stesso limite e ai gruppi di limiti sono assegnati diversi siti, non è possibile prevedere l'assegnazione effettiva di un client a un sito.  

 Se i limiti si sovrappongono in più siti e gerarchie di Configuration Manager, i client potrebbero essere assegnati a un sito sbagliato o, addirittura, non essere assegnati ad alcun sito.  

 I client di System Center Configuration Manager controllano la versione del sito di Configuration Manager prima del completamento dell'assegnazione sito e non possono essere assegnati a una versione precedente in caso di sovrapposizione dei limiti. Tuttavia, i client di System Center Configuration Manager 2012 potrebbero essere assegnati erroneamente a un sito di System Center Configuration Manager.  

 Per evitare che i client vengano assegnati involontariamente al sito sbagliato in caso di sovrapposizione dei limiti di due gerarchie, configurare i parametri di installazione client di Configuration Manager in modo da assegnare i client a un sito specifico.  

##  <a name="a-namebkmkmixeda-configuration-manager-limitations--in-a-mixed-version-hierarchy"></a><a name="bkmk_mixed"></a> Limitazioni di Configuration Manager in una gerarchia con più versioni  
 Durante il processo di aggiornamento di un sito di System Center Configuration Manager, può capitare che in alcuni momenti siti diversi abbiano versioni diverse.  Se ad esempio si esegue l'aggiornamento a una nuova versione di un sito di amministrazione centrale, può capitare che a causa delle finestre di manutenzione del sito uno o più siti primari vengano aggiornati solo in una data o un'ora successiva.  

 Quando più siti in un'unica gerarchia eseguono versioni diverse, alcune funzionalità non sono disponibili. Questo può influire sulla gestione degli oggetti di Configuration Manager nella console di Configuration Manager e sulle funzionalità disponibili per i client. In genere, le funzionalità della versione più recente di Configuration Manager non sono accessibili dai siti o dai client che eseguono una versione precedente del Service Pack.  

### <a name="limitations-when-upgrading--configuration-manager"></a>Limitazioni durante l'aggiornamento di Configuration Manager  

|Oggetto|Dettagli|  
|------------|-------------|  
|Account di accesso alla rete|**Durante l'aggiornamento da System Center Configuration Manager 2012 a System Center Configuration Manager:** quando si usa una console di Configuration Manager connessa a un sito di amministrazione centrale aggiornato a System Center Configuration Manager per visualizzare i dettagli dell'account di accesso alla rete, la console non visualizza i dettagli per gli account configurati presso un sito primario che esegue System Center Configuration Manager 2012. Dopo l'aggiornamento del sito primario alla stessa versione del sito di amministrazione centrale, i dettagli dell'account saranno visibili nella console.<br /><br /> **Durante l'aggiornamento tra versioni diverse di System Center Configuration Manager:** quando si usa una console di Configuration Manager connessa a un sito di amministrazione centrale aggiornato a System Center Configuration Manager per visualizzare i dettagli dell'account di accesso alla rete, la console non visualizza i dettagli per gli account configurati presso un sito primario che esegue una versione precedente. Dopo l'aggiornamento del sito primario alla stessa versione del sito di amministrazione centrale, i dettagli dell'account saranno visibili nella console.|  
|Immagini d'avvio per le distribuzioni del sistema operativo|**Durante l'aggiornamento da System Center Configuration Manager 2012 a System Center Configuration Manager:** quando il sito di livello superiore di una gerarchia viene aggiornato a System Center Configuration Manager, le immagini d'avvio predefinite vengono aggiornate automaticamente a immagini d'avvio basate su Windows ADK 10. Usare queste immagini d'avvio solo per le distribuzioni ai client di siti di System Center Configuration Manager. Per altre informazioni, vedere [Pianificazione dell'interoperabilità della distribuzione del sistema operativo in System Center Configuration Manager](../../../osd/plan-design/planning-for-operating-system-deployment-interoperability.md).<br /><br /> **Durante l'aggiornamento tra versioni diverse di System Center Configuration Manager:** se le nuove versioni di cm6long non aggiornano la versione di Windows ADK in uso, non ci sono effetti sulle immagini d'avvio.|  
|Nuovi passaggi della sequenza di attività|Quando si crea una sequenza di attività contenente un passaggio introdotto in una versione di Configuration Manager ma non disponibile in una versione precedente, possono verificarsi i problemi seguenti:<br /><br /> -- Si verifica un errore quando si prova a modificare la sequenza di attività da un sito che esegue una versione precedente di Configuration Manager.<br /><br /> -- La sequenza di attività non viene eseguita su un computer che esegue una versione precedente del client di Configuration Manager.|  
|Comunicazioni tra client e punti di gestione di livello inferiore|Un client di Configuration Manager comunicante con un punto di gestione di un sito che esegue una versione precedente rispetto a quella usata dal client può usare soltanto le funzionalità supportate dalla versione di livello inferiore di Configuration Manager. Se ad esempio si distribuisce contenuto da un sito di System Center Configuration Manager che ha di recente eseguito l'aggiornamento a un client comunicante con un punto di gestione che non ha ancora eseguito l'aggiornamento a tale versione, il client non potrà usare le nuove funzionalità dell'ultima versione.|  

##  <a name="a-namebkmkconsoleinteropa-interoperability-for-the-configuration-manager-console"></a><a name="BKMK_ConsoleInterop"></a> Interoperabilità per la Console di Configuration Manager  
 La tabella seguente contiene informazioni sull'uso della console di Configuration Manager in un ambiente che contiene una combinazione di versioni diverse di Configuration Manager.  

|Ambiente di interoperabilità|Altre informazioni|  
|----------------------------------|----------------------|  
|Ambiente con System Center Configuration Manager 2012 e System Center Configuration Manager|Per gestire un sito di Configuration Manager, sia la console che il sito a cui si connette la console devono eseguire la stessa versione di Configuration Manager. Ad esempio, non è possibile usare una console di System Center Configuration Manager 2012 per gestire un sito di System Center Configuration Manager o viceversa.<br /><br /> L'installazione della console di System Center Configuration Manager 2012 e della console di System Center Configuration Manager nello stesso computer non è supportata.|  
|Un ambiente con più versioni di System Center Configuration Manager|System Center Configuration Manager non supporta l'installazione di più console di Configuration Manager in un solo computer. Per usare console di diverse versioni di System Center Configuration Manager, è necessario installare le diverse console in computer separati.<br /><br /> Durante il processo di aggiornamento dei siti in una gerarchia è possibile connettere un console a un sito che esegue una versione più recente e visualizzare le informazioni su altri siti in quella gerarchia. Tuttavia, questa configurazione non è consigliata, perché le differenze tra la versione della console e la versione del sito di Configuration Manager potrebbero provocare problemi di dati. Oltre a questo, alcune funzionalità disponibili nell'ultima versione del prodotto non sono disponibili nella console.|  



<!--HONumber=Dec16_HO3-->



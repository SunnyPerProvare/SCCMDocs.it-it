---
title: Interoperabilità tra versioni
titleSuffix: Configuration Manager
description: Informazioni su come evitare i conflitti tra più gerarchie di System Center Configuration Manager nella stessa rete.
ms.date: 1/30/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9b0a7859-747f-4495-a2f4-13fd5991f897
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: ccb7861b5264d649a8ff4b2340bf34eaaafe7970
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126981"
---
# <a name="interoperability-between-different-versions-of-system-center-configuration-manager"></a>Interoperabilità tra versioni diverse di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile installare e usare più gerarchie indipendenti di System Center Configuration Manager all'interno della stessa rete. Tuttavia, dal momento che più gerarchie di Configuration Manager non interagiscono al di fuori del processo di migrazione, per ogni gerarchia sono necessarie configurazioni che impediscono eventuali conflitti. È anche possibile creare determinate configurazioni per consentire alle risorse gestite di interagire con i sistemi del sito dalla gerarchia corretta.  

Nelle seguenti sezioni vengono fornite informazioni sull'utilizzo di diverse versioni di Configuration Manager nella stessa rete:  

-   [Interoperabilità tra System Center Configuration Manager e le versioni precedenti del prodotto](#BKMK_SupConfigInterop)  

-   [Interoperabilità per la Console di Configuration Manager](#BKMK_ConsoleInterop)  

-   [Limitazioni di Configuration Manager in una gerarchia con più versioni](#bkmk_mixed)  

##  <a name="BKMK_SupConfigInterop"></a> Interoperabilità tra System Center Configuration Manager e le versioni precedenti del prodotto  
I siti di versioni diverse non possono coesistere nella stessa gerarchia, eccetto durante il processo di aggiornamento da System Center Configuration Manager 2012 a System Center Configuration Manager o da una versione di System Center Configuration Manager a una versione più recente (usando aggiornamenti nella console).   

Dal momento che è possibile distribuire un sito e una gerarchia di System Center Configuration Manager nella stessa destinazione di un sito o di una gerarchia di System Center Configuration Manager 2012, è necessario impedire ai client delle due versioni di entrare a far parte di un sito dell'altra versione.

Se, ad esempio, due o più gerarchie di Configuration Manager hanno [limiti sovrapposti](/sccm/core/servers/deploy/configure/boundary-groups#overlapping-boundaries) che includono gli stessi percorsi di rete, assegnare ogni nuovo client a un sito specifico anziché usare l'assegnazione sito automatica. Per altre informazioni, vedere [Come assegnare i client a un sito](/sccm/core/clients/deploy/assign-clients-to-a-site).  

Non è inoltre possibile installare un client di System Center Configuration Manager 2012 in un computer che ospita un ruolo del sistema del sito di System Center Configuration Manager, né installare un client di System Center Configuration Manager in un computer che ospita un ruolo del sistema del sito di System Center Configuration Manager 2012.  

Analogamente, non sono supportati i client e le connessioni seguenti:  

- Client di System Center Configuration Manager 2012 o versioni precedenti del client computer  

- Client di System Center Configuration Manager 2012 o versioni precedenti del client di gestione di dispositivi  

- Client per la gestione dispositivi Windows CE Platform Builder (qualsiasi versione)  

- Connessione VPN di System Center Mobile Device Manager  

###  <a name="BKMK_SupConfigSiteAssignment"></a> Considerazioni sull'assegnazione sito dei client  
I client di Configuration Manager possono essere assegnati a un unico sito primario. Quando si usa l'assegnazione sito automatica per assegnare i client a un sito durante l'installazione client, quando più di un gruppo di limiti contiene lo stesso limite e ai gruppi di limiti sono assegnati diversi siti, non è possibile prevedere l'assegnazione effettiva di un client a un sito.  

Se i limiti si sovrappongono in più siti e gerarchie di Configuration Manager, i client potrebbero non essere assegnati al sito previsto o, addirittura, non essere assegnati ad alcun sito.  

I client di System Center Configuration Manager controllano la versione del sito di Configuration Manager prima del completamento dell'assegnazione sito e non possono essere assegnati a una versione precedente in caso di sovrapposizione dei limiti. Tuttavia, i client di System Center Configuration Manager 2012 potrebbero essere assegnati erroneamente a un sito di System Center Configuration Manager.  

Per evitare che i client vengano assegnati involontariamente al sito sbagliato in caso di sovrapposizione dei limiti di due gerarchie, configurare i parametri di installazione client di Configuration Manager in modo da assegnare i client a un sito specifico.  

##  <a name="bkmk_mixed"></a> Limitazioni di Configuration Manager in una gerarchia con più versioni  
Durante il processo di aggiornamento di un sito di System Center Configuration Manager, in alcuni momenti siti diversi possono avere versioni diverse. Se ad esempio si esegue l'aggiornamento a una nuova versione di un sito di amministrazione centrale, può capitare che a causa delle finestre di manutenzione del sito uno o più siti primari vengano aggiornati solo in una data o un'ora successiva.  

Quando più siti in un'unica gerarchia eseguono versioni diverse, alcune funzionalità non sono disponibili. Questo può influire sulla gestione degli oggetti di Configuration Manager nella console di Configuration Manager e sulle funzionalità disponibili per i client. In genere, le funzionalità della versione più recente di Configuration Manager non sono accessibili dai siti o dai client che eseguono una versione precedente del Service Pack.  

### <a name="limitations-when-upgrading-configuration-manager"></a>Limitazioni durante l'aggiornamento di Configuration Manager  

|Oggetto|Dettagli|  
|------------|-------------|  
|Account di accesso alla rete|**Quando si esegue l'aggiornamento da System Center 2012 Configuration Manager a System Center Configuration Manager:** quando si visualizzano i dettagli dell'account di accesso alla rete da una console di Configuration Manager connessa a un sito di amministrazione centrale aggiornato a System Center Configuration Manager, la console non visualizza i dettagli per gli account configurati presso un sito primario che esegue System Center 2012 Configuration Manager. Dopo l'aggiornamento del sito primario alla stessa versione del sito di amministrazione centrale, i dettagli dell'account sono visibili nella console.<br /><br /> **Quando si esegue l'aggiornamento tra versioni di System Center Configuration Manager:** quando si visualizzano i dettagli dell'account di accesso alla rete da una console di Configuration Manager connessa a un sito di amministrazione centrale aggiornato a una nuova versione di System Center Configuration Manager, la console non visualizza i dettagli per gli account configurati presso un sito primario che esegue una versione precedente. Dopo l'aggiornamento del sito primario alla stessa versione del sito di amministrazione centrale, i dettagli dell'account sono visibili nella console.|  
|Immagini d'avvio per la distribuzione del sistema operativo|**Quando si esegue l'aggiornamento da System Center 2012 Configuration Manager a System Center Configuration Manager:**  quando il sito di livello superiore di una gerarchia viene aggiornato a System Center Configuration Manager, le immagini d'avvio predefinite vengono aggiornate automaticamente a immagini d'avvio basate su Windows Assessment and Deployment Kit (Windows ADK) 10. Usare queste immagini d'avvio solo per le distribuzioni ai client di siti di System Center Configuration Manager. Per altre informazioni, vedere [Pianificazione dell'interoperabilità della distribuzione del sistema operativo](/sccm/osd/plan-design/planning-for-operating-system-deployment-interoperability).<br /><br /> **Quando si esegue l'aggiornamento tra versioni di System Center Configuration Manager:** se le nuove versioni di Configuration Manager non aggiornano la versione di Windows ADK in uso, non ci sono effetti sulle immagini d'avvio.|  
|Nuovi passaggi della sequenza di attività|Quando si crea una sequenza di attività con un passaggio introdotto in una versione di Configuration Manager, ma non disponibile in una versione precedente, possono verificarsi i problemi seguenti:<br /><br /> -- Si verifica un errore quando si prova a modificare la sequenza di attività da un sito che esegue una versione precedente di Configuration Manager.<br /><br /> -- La sequenza di attività non viene eseguita su un computer che esegue una versione precedente del client di Configuration Manager.|  
|Comunicazioni tra client e punti di gestione di livello inferiore|Un client di Configuration Manager comunicante con un punto di gestione di un sito che esegue una versione precedente rispetto a quella usata dal client può usare soltanto le funzionalità supportate dalla versione di livello inferiore di Configuration Manager. Se ad esempio si distribuisce contenuto da un sito di System Center Configuration Manager aggiornato di recente a un client che comunica con un punto di gestione non ancora aggiornato a tale versione, il client non riesce a usare le nuove funzionalità dell'ultima versione.|  

##  <a name="BKMK_ConsoleInterop"></a> Interoperabilità per la console di Configuration Manager  
 La tabella seguente contiene informazioni sull'uso della console di Configuration Manager in un ambiente che contiene una combinazione di versioni diverse di Configuration Manager.  


| Ambiente di interoperabilità | Altre informazioni |
|------------------------------|------------------|
| Ambiente con System Center Configuration Manager 2012 e System Center Configuration Manager | Per gestire un sito di Configuration Manager, sia la console che il sito a cui si connette la console devono eseguire la stessa versione di Configuration Manager. Ad esempio, non è possibile usare una console di System Center Configuration Manager 2012 per gestire un sito di System Center Configuration Manager o viceversa.<br /><br /> L'installazione della console di System Center Configuration Manager 2012 e della console di System Center Configuration Manager nello stesso computer non è supportata.|
| Un ambiente con più versioni di System Center Configuration Manager | System Center Configuration Manager non supporta l'installazione di più console di Configuration Manager in un solo computer. Per usare console di diverse versioni di System Center Configuration Manager, installare le diverse console in computer separati.<br /><br /> Durante il processo di aggiornamento a una nuova versione dei siti in una gerarchia è possibile connettere un console a un sito che esegue una versione più recente e visualizzare le informazioni su altri siti in quella gerarchia. Questa configurazione, tuttavia, non è consigliata. È possibile che le differenze tra la versione della console e la versione del sito di Configuration Manager causino problemi di dati. Alcune funzionalità disponibili nell'ultima versione del prodotto non saranno disponibili nella console. <br /><br /> La gestione di un sito quando si usa una console la cui versione non corrisponde alla versione del sito non è supportata. Questa operazione potrebbe causare la perdita di dati e mettere a rischio il sito. Ad esempio, l'uso di una console della versione 1610 per gestire un sito che esegue la versione 1606 non è supportato. |


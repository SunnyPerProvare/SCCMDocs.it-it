---
title: Selezionare i metodi di individuazione | Microsoft Docs
description: Considerazioni sui metodi da usare e sui siti in cui eseguirli.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 127ce713-d085-430f-ac7b-2701637fe126
caps.latest.revision: 9
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 54beff9bc8624d67efda7393db6334ebc96937d7

---
# <a name="select-discovery-methods-to-use-for-system-center-configuration-manager"></a>Selezionare i metodi di individuazione per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Per usare in modo efficace l'individuazione di System Center Configuration Manager, è necessario analizzare i metodi da usare e i siti in cui eseguirli.  

 Dal momento che l'individuazione può generare un grosso volume di traffico di rete e che i record dei dati di individuazione risultanti possono causare un uso significativo di risorse della CPU durante l'elaborazione, usare solo i metodi di individuazione necessari per soddisfare gli obiettivi. Si potrebbe iniziare a usare solo uno o due metodi di individuazione, quindi abilitare in seguito metodi aggiuntivi in modo controllato per estendere il livello di individuazione nel relativo ambiente. Le informazioni contenute in questo argomento consentono di prendere decisioni informate.  

 Per informazioni sui vari metodi di individuazione, vedere [About discovery methods for System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md) (Informazioni sui metodi di individuazione per System Center Configuration Manager).  

## <a name="select-methods-to-discover-different-things"></a>Selezionare i metodi per individuare elementi diversi  
 Per individuare computer client o risorse utente potenziali di Configuration Manager, è necessario abilitare i metodi di individuazione appropriati. È possibile utilizzare diverse combinazioni di metodi di individuazione per individuare risorse diverse e per scoprire ulteriori informazioni su tali risorse. I metodi di individuazione usati determinano il tipo di risorse che viene individuato e i servizi e gli agenti di Configuration Manager usati nel processo di individuazione. È inoltre possibile determinare il tipo di informazioni sulle risorse che è possibile individuare.  

 **Individuare computer**   
Quando si desidera individuare dei computer, è possibile usare l'individuazione sistema o l'individuazione di rete Active Directory.  

 Ad esempio, se si vuole individuare risorse che possano installare il client di Configuration Manager prima di usare l'installazione push client, si può eseguire l'individuazione sistema Active Directory. In alternativa, si potrebbe eseguire l'individuazione di rete e utilizzare le relative opzioni per individuare il sistema operativo delle risorse (necessario per utilizzare in seguito l'installazione push client). Tuttavia, utilizzando l'individuazione sistema Active Directory, non solo si individua la risorsa, ma informazioni di base ed estese relative a essa dai Servizi di dominio Active Directory. Tali informazioni potrebbero essere utili nella creazione di query e raccolte complesse da utilizzare per l'assegnazione di impostazioni client o distribuzione di contenuto. L'individuazione di rete, d'altro canto, fornisce informazioni sulla topologia di rete che non si è in grado di acquisire con altri mezzi di individuazione, ma non fornisce informazioni sull'ambiente di Active Directory.  

 È anche possibile utilizzare solo l'individuazione heartbeat per forzare l'individuazione di client installati da metodi diversi dall'installazione push client. Tuttavia, diversamente da altri metodi di individuazione, l'individuazione heartbeat non può individuare computer che non hanno un client attivo di Configuration Manager e restituisce un set limitato di informazioni. È progettato per mantenere un record del database esistente e non per essere la base di tale record. Le informazioni fornite dall'individuazione heartbeat potrebbero non essere sufficienti per creare query o raccolte complesse.  

 Se si utilizza l'individuazione gruppo Active Directory per individuare l'appartenenza di un gruppo specifico, è possibile individuare informazioni limitate sul sistema o sul computer. Ciò non sostituisce un'individuazione completa di computer, ma può fornire informazioni di base. Tali informazioni sono insufficienti per l'installazione push client.  

 **Individuare utenti**   
Quando si desidera individuare informazioni sugli utenti, è possibile usare l'individuazione utente Active Directory. Simile all'individuazione sistema Active Directory, questo metodo individua gli utenti da Active Directory e include informazioni di base oltre alle informazioni Active Directory estese. È possibile utilizzare queste informazioni per creare query e raccolte complesse simili a quelle per i computer.  

 **Individuare informazioni sui gruppi**   
Quando si desidera individuare informazioni sui gruppi e le appartenenze ai gruppi, usare l'individuazione gruppo Active Directory. Questo metodo di individuazione consente di creare record di risorse per i gruppi di protezione.  

 È possibile utilizzare questo metodo per effettuare la ricerca di un gruppo Active Directory specifico per individuare i membri di tale gruppo oltre a tutti gli eventuali gruppi inclusi in quel gruppo. È anche possibile utilizzare questo metodo per effettuare la ricerca di gruppi in un percorso Active Directory e una ricerca ricorsiva di ogni contenitore figlio di tale percorso nei Servizi di dominio Active Directory.  

 Questo metodo di individuazione può inoltre effettuare la ricerca dell'appartenenza di gruppi di distribuzione. Ciò consente di identificare le relazioni di gruppo di utenti e computer.  

 Quando si individua un gruppo, è inoltre possibile individuare informazioni limitate sui relativi membri. Ciò non sostituisce l'individuazione sistema o utente di Active Directory e in genere non è sufficiente per creare query e raccolte complesse o servire da base dell'installazione push client.  

 **Individuare l'infrastruttura**   
Esistono due metodi che si possono usare per individuare l'infrastruttura di rete, l'individuazione foresta e l'individuazione di rete Active Directory.  

 È possibile utilizzare l'individuazione foresta di Active Directory per effettuare la ricerca in una foresta Active Directory di informazioni sulle subnet e le configurazioni del sito di Active Directory. Queste configurazioni possono essere quindi immesse automaticamente in Configuration Manager come percorsi di limite.  

 Quando si desidera individuare la topologia di rete, utilizzare l'individuazione di rete. Mentre altri metodi di individuazione restituiscono informazioni relative ai Servizi di dominio Active Directory e possono individuare il percorso di rete corrente di un client, non forniscono informazioni sull'infrastruttura basate sulle subnet e la topologia del router della rete.  

##  <a name="a-namebkmkshareda-discovery-data-is-shared-between-sites"></a><a name="bkmk_shared"></a> I dati di individuazione vengono condivisi tra i siti  
 Dopo l'aggiunta dei dati di individuazione in un database da parte di Configuration Manager, tali dati vengono rapidamente condivisi in tutti i siti della gerarchia. Dal momento che individuare le stesse informazioni in più siti della stessa gerarchia non offre alcun vantaggio, è consigliabile valutare la configurazione di una singola istanza di ogni metodo di individuazione usato per l'esecuzione in un unico sito, anziché optare per l'esecuzione di più istanze di un unico metodo in più siti.  

 Tuttavia, per alcuni ambienti può essere utile assegnare lo stesso metodo di individuazione da eseguire in più siti, con configurazioni e pianificazioni distinte. In questo modo le configurazioni per l'esecuzione di un metodo di individuazione sono specifiche per un singolo sito. È quindi possibile eseguire l'individuazione in un sito e condividere i risultati con altri siti oppure usare lo stesso metodo in due siti diversi in cui l'individuazione viene eseguita su una risorsa locale e non tenta di individuare le informazioni da percorsi in una rete WAN.  Ad esempio, spesso questo è utile quando si usa l'individuazione di rete in cui ogni sito individua la propria rete locale anziché tentare di eseguire l'individuazione in tutto il percorso di rete della WAN. Se vengono configurate più istanze di un singolo metodo di individuazione da eseguire in più siti, è necessario pianificare la configurazione di ogni istanza per evitare che due o più siti individuino le stesse risorse della rete o di Active Directory. L'individuazione degli stessi percorsi e delle stesse risorse in più siti può determinare un maggiore uso della larghezza di banda di rete e la creazione di record dei dati di individuazione duplicati per le risorse che, seppur non costituiscano un valore aggiunto, devono comunque essere elaborati dai server del sito.  

 Nella seguente tabella viene stabilito in quali siti è possibile configurare i vari metodi di individuazione.  

|Metodo di individuazione|Percorsi supportati|  
|----------------------|-------------------------|  
|Individuazione foresta Active Directory|Sito di amministrazione centrale<br /><br /> Sito primario|  
|Individuazione gruppo Active Directory|Sito primario|  
|Individuazione sistema Active Directory|Sito primario|  
|individuazione utenti di Active Directory|Sito primario|  
|Individuazione heartbeat<sup>1</sup>|Sito primario|  
|Individuazione rete|Sito primario<br /><br /> Sito secondario|  

 <sup>1</sup> I siti secondari non sono in grado di configurare l'individuazione heartbeat ma possono ricevere il record dei dati di individuazione di heartbeat da un client.  

 Quando i siti secondari eseguono l'individuazione di rete o ricevono i DDR dell'individuazione heartbeat, trasferiscono tali DDR mediante replica basata su file nel relativo sito primario padre. Infatti, solo i siti primari e i siti di amministrazione centrale possono elaborare i record dei dati di individuazione. Per altre informazioni su come vengono elaborati i record dei dati di individuazione, vedere [About Discovery Data Records](../../../../core/servers/deploy/configure/run-discovery.md#BKMK_DDRs) (Informazioni sui record dei dati di individuazione).  

## <a name="considerations-for-different-discovery-methods"></a>Considerazioni per i vari metodi di individuazione  
 Dal momento che ogni server del sito e ogni ambiente di rete è diverso dall'altro, è necessario limitare le configurazioni dell'individuazione iniziali e monitorare attentamente la capacità di ogni server del sito di elaborare i dati di individuazione generati.  

-   Quando si utilizza un metodo di individuazione Active Directory per sistemi, utenti o gruppi:  

    -   Eseguire l'individuazione in un sito che dispone di una connessione di rete veloce ai controller di dominio.  

    -   Prendere in considerazione la topologia di replica di Active Directory per garantire all'individuazione l'accesso alle informazioni più recenti.  

    -   Valutare l'ambito della configurazione dell'individuazione e limitare l'individuazione solo ai gruppi e ai percorsi di Active Directory che è necessario individuare.  

-   Se si utilizza l'individuazione di rete:  

    -   Per individuare la topografia di rete, utilizzare una configurazione iniziale limitata.  

    -   Dopo aver individuato la topografia di rete, configurare l'individuazione di rete per l'esecuzione in siti specifici centrali rispetto alle aree di rete che si desidera individuare in modo più completo.  

-   Dal momento che l'individuazione heartbeat non viene eseguita in un sito specifico, non è necessario prenderla in considerazione in fase di pianificazione generale per stabilire dove eseguire l'individuazione.  

-   Dal momento che ogni server del sito e ogni ambiente di rete è diverso dall'altro, è necessario limitare le configurazioni dell'individuazione iniziali e monitorare attentamente la capacità di ogni server del sito di elaborare i dati di individuazione generati.  

##  <a name="a-namebkmkbesta-best-practices-for-discovery"></a><a name="bkmk_best"></a> Procedure consigliate per l'individuazione  
 **Prima di eseguire l'individuazione gruppo Active Directory, eseguire l'individuazione sistema Active Directory e l'individuazione utente Active Directory:**  

 In caso di individuazione di un computer o di un utente non individuato precedentemente come membro di un gruppo, l'individuazione gruppo Active Directory tenta di individuare dettagli di base relativi all'utente o al computer. Dal momento che l'individuazione gruppo Active Directory non è ottimizzata per questo tipo di individuazione, il processo può comprometterne la velocità di esecuzione. Inoltre, l'individuazione gruppo Active Directory consente di individuare solo i dettagli di base relativi agli utenti e ai computer individuati, ma non di creare un record di individuazione utente o computer completo. In caso di esecuzione dell'individuazione sistema Active Directory e dell'individuazione utente Active Directory, gli attributi Active Directory aggiuntivi relativi a ciascun oggetto sono disponibili e, di conseguenza, l'individuazione gruppo Active Directory viene eseguita in modo più efficiente.  

 **Quando viene configurata l'individuazione gruppo Active Directory, è sufficiente specificare solo i gruppi usati con Configuration Manager:**  

 Per controllare l'uso delle risorse da parte dell'individuazione gruppo Active Directory, specificare solo i gruppi usati con Configuration Manager. L'individuazione gruppo Active Directory, infatti, esegue ricerche ricorsive in ogni gruppo individuato relativamente a utenti, computer e gruppi nidificati. La ricerca di ciascun gruppo nidificato può espandere l'ambito dell'individuazione gruppo Active Directory e ridurre le prestazioni. Inoltre, se si configura l'individuazione differenziale per l'individuazione gruppo Active Directory, questo metodo di individuazione consente di monitorare le modifiche relative a ciascun gruppo. Le prestazioni vengono ulteriormente ridotte quando il metodo deve eseguire ricerche di gruppi non necessari.  

 **Configurare metodi di individuazione con un intervallo maggiore tra le individuazioni complete e un periodo più frequente per le individuazioni differenziali:**  

 Poiché l'individuazione differenziale utilizza un numero inferiore di risorse rispetto a un ciclo di individuazione completa ed è in grado di identificare risorse nuove o modificate in Active Directory, quando si utilizza l'individuazione differenziale è possibile ridurre la frequenza dei cicli di individuazione completa specificando al massimo un'esecuzione a settimana. L'individuazione differenziale per l'individuazione sistema Active Directory, l'individuazione utente Active Directory e l'individuazione gruppo Active Directory consente di identificare quasi tutte le modifiche apportate agli oggetti Active Directory e di conservare i dati accurati di individuazione per le risorse.  

 **Eseguire i metodi di individuazione di Active Directory in un sito primario che abbia un percorso di rete molto vicino al controller di dominio Active Directory:**  

 Per migliorare le prestazioni dell'individuazione Active Directory, è consigliabile eseguire l'individuazione in un sito primario che disponga di una connessione di rete veloce ai controller di dominio. Se si esegue lo stesso metodo di individuazione Active Directory in più siti, è consigliabile configurare ciascun metodo di individuazione in modo da evitare la sovrapposizione. A differenza delle versioni precedenti di Configuration Manager, i dati di individuazione vengono condivisi tra i siti. Non è pertanto necessaria l'individuazione delle stesse informazioni in più siti. Per altre informazioni, vedere [I dati di individuazione vengono condivisi tra i siti](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md#bkmk_shared).  

 **Quando si prevede di creare automaticamente i limiti dai dati di individuazione, è consigliabile eseguire l'individuazione foresta Active Directory in un unico sito:**  

 Se l'individuazione foresta Active Directory viene eseguita in più di un sito di una gerarchia, è consigliabile attivare solo le opzioni per la creazione automatica dei limiti in un unico sito. Quando l'individuazione foresta Active Directory viene eseguita in tutti i siti e crea i limiti, infatti, Configuration Manager non può unire tali limiti in un unico oggetto limite. Se l'individuazione foresta Active Directory viene configurata per la creazione automatica dei limiti in più siti, possono essere generati oggetti limite duplicati nella console di Configuration Manager.  



<!--HONumber=Dec16_HO3-->



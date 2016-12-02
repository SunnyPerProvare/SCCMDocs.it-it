---
title: Progettare una gerarchia | System Center Configuration Manager
description: "Comprendendo le topologie disponibili e le opzioni di gestione di System Center Configuration Manager è possibile pianificare la gerarchia del sito."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
caps.latest.revision: 22
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 783fb4d61aab83ad64b9cec332e90d6c9de59f47
ms.openlocfilehash: b1ed3011356a794b7b0913a1c8f189230d8957b2


---
# <a name="design-a-hierarchy-of-sites-for-system-center-configuration-manager"></a>Progettare una gerarchia di siti per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima di installare il primo sito di una nuova gerarchia di System Center Configuration Manager, è necessario sapere quali sono le topologie disponibili per Configuration Manager, quali tipi di sito sono disponibili e che relazioni hanno tra loro, nonché l'ambito di gestione previsto da ogni tipo di sito. Quindi, dopo aver considerato le opzioni di gestione del contenuto che consentono di ridurre il numero di siti da installare, è possibile pianificare una topologia che soddisfi in modo efficiente le attuali esigenze aziendali e possa espandersi in un secondo tempo per gestire la crescita futura.  

> [!NOTE]
> Quando si pianifica una nuova installazione di Configuration Manager, è necessario conoscere le [note sulla versione]( /sccm/core/servers/deploy/install/release-notes) in cui sono descritti nel dettaglio i problemi delle versioni attive. Le note sulla versione si applicano a tutti i rami di Configuration Manager.  Tuttavia, quando si usa il ramo [Technical Preview]( /sccm/core/get-started/technical-preview), nella documentazione si troveranno solo i problemi specifici di tale ramo per ciascuna versione della Technical Preview.  

##  <a name="a-namebkmktopologya-hierarchy-topology"></a><a name="bkmk_topology"></a> Topologia di gerarchia  
 Le topologie di gerarchia variano da un singolo sito primario autonomo a un gruppo di siti primari e secondari connessi con un sito di amministrazione centrale come sito di livello superiore della gerarchia.    
Gli elementi determinanti per stabilire il tipo e il numero di siti da usare in una gerarchia sono in genere il numero e il tipo di dispositivi che è necessario supportare:  

 **Sito primario autonomo**: usare un sito primario autonomo quando un singolo sito primario è in grado di supportare la gestione di tutti i dispositivi e tutti gli utenti (vedere la sezione relativa ai [numeri di ridimensionamento e scalabilità](/sccm/core/plan-design/configs/size-and-scale-numbers)). Questa topologia funziona anche quando le diverse aree geografiche delle società possono essere gestite correttamente da un singolo sito primario.  Per semplificare la gestione del traffico di rete, è possibile usare punti di gestione preferiti e un'infrastruttura di contenuto accuratamente pianificata (vedere [Fundamental concepts for content management in System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md) (Concetti di base per la gestione dei contenuti in System Center Configuration Manager).  

 I vantaggi di questa topologia includono:  

-   Carico amministrativo semplificato  

-   Semplifica l'assegnazione del sito client e l'individuazione di servizi e risorse disponibili  

-   Elimina i possibili ritardi introdotti dalla replica di database tra siti  

-   Questa scelta non è permanente ed è possibile espandere una gerarchia con singolo sito primario autonomo in una gerarchia più ampia con un sito di amministrazione centrale. In questo modo sarà quindi possibile installare nuovi siti primari per espandere la distribuzione.  


**Sito di amministrazione centrale con uno o più siti primari figlio:** usare questa topologia quando sono necessari più siti primari per supportare la gestione di tutti gli utenti e i dispositivi.  I vantaggi di questa topologia includono:  

-   Obbligatorio quando è necessario usare più di un singolo sito primario  

-   Supporta fino a 25 siti primari, consentendo di espandere la gerarchia  

-   Questa scelta è definitiva. Non è possibile scollegare un sito primario figlio per renderlo un sito primario autonomo. Pertanto, se non si reinstallano i siti, si userà sempre il sito di amministrazione centrale  

 Le informazioni nelle sezioni seguenti possono essere utili per capire quando usare un sito specifico o l'opzione di gestione dei contenuti al posto di un sito aggiuntivo.  

##  <a name="a-namebkmkchoosecasa-determine-when-to-use-a-central-administration-site"></a><a name="BKMK_ChooseCAS"></a> Determinare quando usare un sito di amministrazione centrale  
 Usare un sito di amministrazione centrale per configurare le impostazioni a livello di gerarchia e per monitorare tutti i siti e gli oggetti nella gerarchia. Questo tipo di sito non gestisce i client direttamente ma coordina la replica dei dati tra i siti, che include la configurazione di siti e client in tutta la gerarchia.  

**Le informazioni seguenti possono essere utili per decidere quando installare un sito di amministrazione centrale:**  

-   Il sito di amministrazione centrale è il sito di livello superiore nella gerarchia  

-   Quando si configura una gerarchia con più di un sito primario, è necessario installare un sito di amministrazione centrale, che deve essere il primo sito che viene installato  

-   Il sito di amministrazione centrale supporta solo i siti primari come siti figlio  

-   Al sito di amministrazione centrale non è possibile assegnare client  

-   Il sito di amministrazione centrale non supporta i ruoli del sistema del sito che supportano direttamente i client, come punti di gestione e punti di distribuzione  

-   È possibile gestire tutti i client nella gerarchia ed eseguire attività di gestione del sito per qualsiasi sito figlio quando si usa una console di Configuration Manager connessa al sito di amministrazione centrale. Ciò può includere l'installazione di punti di gestione o altri ruoli del sistema del sito in un sito primario figlio o in siti secondari  

-   Quando si usa un sito di amministrazione centrale, tale sito è l'unico punto da cui è possibile visualizzare i dati del sito da tutti i siti nella gerarchia. Questi dati includono informazioni quali dati di inventario e messaggi di stato  

-   È possibile configurare le operazioni di individuazione in tutta la gerarchia dal sito di amministrazione centrale mediante l'assegnazione di metodi di individuazione da eseguire nei singoli siti  

-   È possibile gestire la protezione in tutta la gerarchia mediante l'assegnazione di raccolte, ambiti di protezione e ruoli di sicurezza differenti a diversi utenti amministratori. Queste configurazioni si applicano a ogni sito nella gerarchia  

-   È possibile configurare la replica di file e di database per controllare la comunicazione tra siti all'interno della gerarchia. Ciò include la pianificazione della replica di database per i dati del sito e la gestione della larghezza di banda per il trasferimento tra siti dei dati basati su file  

##  <a name="a-namebkmkchoosepriimarya-determine-when-to-use-a-primary-site"></a><a name="BKMK_ChoosePriimary"></a> Determinare quando usare un sito primario  
 Utilizzare i siti primari per gestire i client. È possibile installare un sito primario come sito primario figlio al di sotto di un sito di amministrazione centrale oppure come primo sito di una nuova gerarchia. Un sito primario che viene installato come primo sito di una gerarchia crea un sito primario autonomo. Sia i siti primari figlio sia i siti primari autonomi supportano siti secondari come siti figlio del sito primario.  

 Si consiglia di usare un sito primario per uno dei motivi seguenti:  

-   Per gestire dispositivi e utenti  

-   Per aumentare il numero di dispositivi che è possibile gestire con una singola gerarchia  

-   Per fornire un punto di connettività aggiuntivo per l'amministrazione della distribuzione  

-   Per soddisfare i requisiti di gestione dell'organizzazione. Ad esempio, è possibile installare un sito primario in una posizione remota per gestire il trasferimento del contenuto di distribuzione attraverso una rete a larghezza di banda ridotta. Con System Center Configuration Manager è tuttavia possibile usare opzioni per limitare l'uso della larghezza di banda di rete in fase di trasferimento dei dati a un punto di distribuzione e questa funzionalità di gestione dei contenuti può sostituire la necessità di installare ulteriori siti.  


**Le informazioni seguenti possono essere utili per decidere quando installare un sito primario:**  

-   Un sito primario può essere un sito primario autonomo o un sito primario figlio in una gerarchia più grande. Quando un sito primario è membro di una gerarchia con un sito di amministrazione centrale, i siti utilizzano la replica database per replicare i dati tra i siti. Ad eccezione del caso in cui non sia necessario supportare più client e dispositivi rispetto a un singolo sito primario, considerare l'installazione di un sito primario autonomo.  Dopo l'installazione di un sito primario autonomo, è possibile espanderlo in modo che faccia riferimento a un nuovo sito di amministrazione centrale per potenziare la distribuzione.  

-   Un sito primario supporta solo un sito di amministrazione centrale come sito padre  

-   Un sito primario supporta solo siti secondari come siti figlio e può supportare più siti figlio secondari  

-   I siti primari sono responsabili dell'elaborazione di tutti i dati client dai rispettivi client assegnati  

-   I siti primari usano la replica di database per comunicare direttamente con il relativo sito di amministrazione centrale (configurato automaticamente quando viene installato un nuovo sito)  

##  <a name="a-namebkmkchoosesecondarya-determine-when-to-use-a-secondary-site"></a><a name="BKMK_ChooseSecondary"></a> Determinare quando usare un sito secondario  
 Utilizzare i siti secondari per gestire il trasferimento dei dati client e del contenuto di distribuzione su reti a larghezza di banda ridotta.  

 Un sito secondario viene gestito da un sito di amministrazione centrale o dal sito primario padre diretto del sito secondario. I siti secondari devono essere collegati a un sito primario e non possono essere spostati in un sito padre differente senza prima disinstallarli e successivamente reinstallarli come siti figlio del nuovo sito primario. È comunque possibile distribuire contenuto tra due siti secondari peer per gestire la replica basata su file del contenuto della distribuzione. Per trasferire i dati client a un sito primario, il sito secondario utilizza la replica basata su file. Un sito secondario usa anche la replica di database per comunicare con il relativo sito primario padre.  

 Si consiglia di installare un sito secondario in presenza di una delle seguenti condizioni:  

-   Non è necessario un punto di connettività locale per un utente amministratore  

-   È necessario gestire il trasferimento del contenuto della distribuzione ai siti di livello inferiore nella gerarchia  

-   È necessario gestire le informazioni client inviate ai siti di livello superiore nella gerarchia  

 Se non si vuole installare un sito secondario e si dispone di client in sedi remote, prendere in considerazione l'uso di Windows BranchCache o l'installazione di punti di distribuzione abilitati per la pianificazione e il controllo della larghezza di banda. È possibile usare queste opzioni di gestione dei contenuti con o senza siti secondari, riducendo così il numero di siti e server da installare. Per informazioni sulle opzioni di gestione dei contenuti in Configuration Manager, vedere [Determinare quando usare le opzioni di gestione dei contenuti](#BKMK_ChooseSecondaryorDP).  


**Le informazioni seguenti possono essere utili per decidere quando installare un sito secondario:**  

-   Se non è disponibile un'istanza locale di SQL Server, i siti secondari installano automaticamente SQL Server Express durante l'installazione del sito.  

-   L'installazione del sito secondario viene avviata dalla console di Configuration Manager, invece di eseguire il programma di installazione di Configuration Manager direttamente in un computer  

-   I siti secondari usano un subset delle informazioni nel database del sito in modo da ridurre la quantità di dati replicati dalla replica di database tra il sito primario padre e il sito secondario  

-   I siti secondari supportano il routing del contenuto basato su file in altri siti secondari che dispongono di un sito primario padre comune  

-   Le installazioni dei siti secondari distribuiscono automaticamente un punto di gestione e un punto di distribuzione ubicati nel server del sito secondario  

##  <a name="a-namebkmkchoosesecondaryordpa-determine-when-to-use-content-management-options"></a><a name="BKMK_ChooseSecondaryorDP"></a> Determinare quando usare le opzioni di gestione dei contenuti  
 Se si dispone di client in percorsi di rete remoti, considerare l'utilizzo di una o più opzioni di gestione dei contenuti piuttosto che di un sito primario o secondario. È spesso possibile evitare la necessità di installare un sito usando Windows BranchCache, configurando i punti di distribuzione per il controllo della larghezza di banda o copiando manualmente il contenuto nei punti di distribuzione (preinstallazione del contenuto).  


**Considerare la distribuzione di un punto di distribuzione piuttosto che l'installazione di un altro sito in presenza di una delle condizioni seguenti:**  

-   La larghezza di banda della rete è sufficiente per consentire ai computer client in remoto di comunicare con un punto di gestione per scaricare i criteri client e inviare informazioni di individuazione, di inventario e relative allo stato dei report  

-   Il Servizio trasferimento intelligente in background (BITS) non garantisce un controllo della larghezza di banda adeguato ai requisiti della rete  

 Per altre informazioni sulle opzioni di gestione dei contenuti in Configuration Manager, vedere [Fundamental concepts for content management in System Center Configuration Manager](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md) (Concetti di base per la gestione dei contenuti in System Center Configuration Manager).  

##  <a name="a-namebkmkbeyonda-beyond-hierarchy-topology"></a><a name="bkmk_beyond"></a> Oltre la topologia di gerarchia  
 Oltre alla topologia di gerarchia iniziale, valutare quali servizi o funzionalità saranno disponibili dai diversi siti della gerarchia (ruoli del sistema del sito) e come verranno gestite nell'infrastruttura le funzionalità e le configurazioni valide per l'intera gerarchia. Di seguito sono riportate le considerazioni più comuni, trattate in argomenti separati. È consigliabile valutare queste considerazione perché possono influenzare o essere influenzate dalla progettazione della gerarchia:  

-   Quando si prepara la [gestione di computer e dispositivi con System Center Configuration Manager](/sccm/core/clients/manage/manage-clients), valutare se i dispositivi gestiti si trovano nell'infrastruttura locale, nel cloud o includono dispositivi di proprietà degli utenti (BYOD).  Valutare anche come verranno gestiti i dispositivi supportati da più opzioni di gestione, ad esempio i computer Windows 10 che possono essere gestiti direttamente da Configuration Manager o attraverso l'integrazione con Microsoft Intune.  

-   Per sapere in che modo l'infrastruttura di rete disponibile può influire sul flusso di dati tra le sedi remote, vedere [Prepare your network environment for System Center Configuration Manager](/sccm/core/plan-design/network/configure-firewalls-ports-domains) (Preparare l'ambiente di rete per System Center Configuration Manager). Considerare anche la posizione geografica degli utenti e dei dispositivi da gestire e se l'accesso all'infrastruttura avviene dal dominio aziendale o da Internet.  

-   Pianificare un'infrastruttura di contenuto per distribuire in modo efficiente le informazioni (file e applicazioni) ai dispositivi gestiti (vedere [Manage content and content infrastructure for System Center Configuration Manager](../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Gestire il contenuto e l'infrastruttura del contenuto per System Center Configuration Manager)).  

-   Determinare quali [funzionalità di System Center Configuration Manager](../../../core/plan-design/changes/features-and-capabilities.md) si intende usare, i ruoli del sistema del sito o l'infrastruttura Windows necessaria e in quali siti di una gerarchia a più siti si possono distribuire per ottimizzare l'uso delle risorse di rete e server.  

-   Considerare la sicurezza per i dati e i dispositivi, incluso l'uso di un'infrastruttura PKI. Vedere [Requisiti dei certificati PKI per System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md)  


**Esaminare le risorse seguenti per le configurazioni specifiche del sito:**  

-   [Plan for the SMS Provider for System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) (Pianificare il provider SMS per System Center Configuration Manager)  

-   [Plan for the site database for System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-the-site-database.md) (Pianificare il database del sito per System Center Configuration Manager)  

-   [Plan for site system servers and site system roles for System Center Configuration Manager](../../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md) (Pianificare i server e i ruoli del sistema del sito per System Center Configuration Manager)  

-   [Plan for security in System Center Configuration Manager](../../../core/plan-design/security/plan-for-security.md) (Pianificare la sicurezza in System Center Configuration Manager)  

-   [Managing network bandwidth](../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_bandwidth) durante la distribuzione dei contenuti all'interno di un sito  


**Prendere in considerazione configurazioni che si estendono a siti e gerarchie:**  

-   [Opzioni di disponibilità elevata per System Center Configuration Manager](/sccm/protect/understand/high-availability-options) per siti e gerarchie  

-   Si prevede di [estendere lo schema di Active Directory per System Center Configuration Manager](../../../core/plan-design/network/extend-the-active-directory-schema.md) e di configurare i siti per [pubblicare i dati del sito per System Center Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md)?  

-   Per gestire la larghezza di banda di rete tra i siti di una gerarchia, vedere [Trasferimenti di dati tra siti in System Center Configuration Manager](../../../core/servers/manage/data-transfers-between-sites.md)  

-   [Fundamentals of role-based administration for System Center Configuration Manager](../../../core/understand/fundamentals-of-role-based-administration.md) (Nozioni di base sull'amministrazione basata su ruoli per System Center Configuration Manager)  



<!--HONumber=Nov16_HO1-->



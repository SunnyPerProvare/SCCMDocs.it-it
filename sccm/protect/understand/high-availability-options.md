---
title: "Disponibilità elevata"
titleSuffix: Configuration Manager
description: "Informazioni su come distribuire System Center Configuration Manager tramite opzioni che consentono di mantenere un livello elevato di disponibilità dei servizi."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1a38421d-24c1-4fef-bf6c-42fce53109ac
caps.latest.revision: "4"
author: mestew
ms.author: mstewart
manager: angrobe
ms.openlocfilehash: bfc40f13f166a4f4aeda4a363ec633a54206dce4
ms.sourcegitcommit: daa080cf220835f157a23e8c8e2bd2781b869bb7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/04/2017
---
# <a name="high-availability-options-for-system-center-configuration-manager"></a>Opzioni di disponibilità elevata per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*



È possibile distribuire System Center Configuration Manager tramite opzioni che consentono di mantenere un elevato livello di disponibilità dei servizi.   

Opzioni che supportano una disponibilità elevata:   

-   I siti supportano più istanze del server del sistema del sito che forniscono importanti servizi ai client.  

-   I siti di amministrazione centrale e primari supportano il backup del database del sito. Il database del sito contiene tutte le configurazioni per siti e client e viene condiviso tra i siti di una gerarchia che contengono un sito di amministrazione centrale.  

-   Le opzioni di ripristino del sito incorporate possono ridurre il tempo di inattività del server e includere opzioni avanzate che semplificano il ripristino quando si dispone di una gerarchia con un sito di amministrazione centrale.  

-   I client possono correggere automaticamente problemi tipici senza intervento amministrativo.  

-   I siti generano avvisi relativi ai client che non riescono a inviare dati recenti, che informano gli amministratori di potenziali problemi.  

-   Configuration Manager include diversi report predefiniti che consentono di identificare i problemi e le tendenze prima che abbiano un impatto negativo sul funzionamento dei server o dei client.  

 Configuration Manager non offre un servizio in tempo reale e occorre aspettarsi una certa latenza dei dati. Pertanto, è insolito che la maggior parte degli scenari che comportano un'interruzione temporanea del servizio costituiscano un problema critico. Quando si sono configurati i siti e le gerarchia con un'alta disponibilità, il tempo di inattività può essere ridotto al minimo, l'autonomia di funzionamento mantenuta e un alto livello di servizio fornito.  

 Ad esempio, i client di Configuration Manager in genere funzionano in maniera autonoma tramite pianificazioni e configurazioni note delle operazioni, nonché tramite pianificazioni per l'invio di dati al sito per l'elaborazione.  

-   Quando i client non riescono a contattare il sito, memorizzano nella cache i dati e li inviano solo quando riescono a contattare il sito.  

-   I client che non riescono a contattare il sito continuano a funzionare usando le ultime pianificazioni conosciute e le informazioni memorizzate nella cache, ad esempio un'applicazione precedentemente scaricata che devono eseguire o installare, finché non riescono a contattare il sito e a ricevere nuovi criteri.  

-   Il sito monitora i sistemi e i client del sito per aggiornamenti di stato periodici e può generare avvisi quando questi non riescono a effettuare la registrazione.  

-   I report incorporati forniscono informazioni sulle operazioni in corso, nonché su operazioni storiche e tendenze. Configuration Manager supporta anche messaggi basati sullo stato che forniscono informazioni quasi in tempo reale sulle operazioni in corso.  

  Usare le informazioni di questo argomento con quelle contenute negli articoli relativi a:
-   [Hardware consigliato](../../core/plan-design/configs/recommended-hardware.md)
-   [Sistemi operativi supportati per i server del sistema del sito](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  

-   [Prerequisiti del sito e del sistema del sito](../../core/plan-design/configs/site-and-site-system-prerequisites.md)


##  <a name="bkmk_snh"></a> Disponibilità elevata per siti e gerarchie  
 **Usare un cluster SQL Server per ospitare il database del sito:**  

 Quando si utilizza un cluster SQL Server per il database su un sito di amministrazione centrale o primario, si utilizza il supporto di failover integrato in SQL Server.  

 I siti secondari non possono utilizzare un cluster SQL Server e non supportano il backup o ripristino del database del sito. Ripristinare un sito secondario reinstallando il sito secondario dal relativo sito primario padre.  

 **Usare un gruppo di disponibilità SQL Server AlwaysOn per ospitare il database del sito:**  

 A partire dalla versione 1602, è possibile usare gruppi di disponibilità SQL Server AlwaysOn per ospitare il database del sito nei siti primari e nel sito di amministrazione centrale come soluzione a disponibilità elevata e di ripristino di emergenza. Per altre informazioni, vedere [SQL Server AlwaysOn for a highly available site database for System Center Configuration Manager](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) (SQL Server AlwaysOn per database del sito a disponibilità elevata per System Center Configuration Manager).  

 **Distribuire una gerarchia di siti con un sito di amministrazione centrale e uno o più siti primari figlio:**  

 Questa configurazione può fornire una tolleranza d'errore quando i siti gestiscono segmenti di rete con sovrapposizione. Inoltre, questa configurazione offre un'opzione di ripristino aggiuntiva per utilizzare le informazioni nel database condiviso disponibile su un altro sito per ricreare il database del sito sul sito ripristinato. È possibile usare questa opzione per sostituire un backup non riuscito o non disponibile del database di un sito non funzionante.  

 **Creare backup regolari in siti di amministrazione centrale e primari:**  

 Quando si crea e testa il backup di un sito regolare, è possibile assicurarsi di avere i dati necessari per il ripristino del sito e l'esperienza per ripristinare un sito in una quantità minima di tempo.  

 **Installare più istanze dei ruoli del sistema del sito:**  

 Quando si installano più istanze di ruoli del sistema del sito critici come il punto di gestione e di distribuzione, si forniscono punti di contatto ridondanti per i client nel caso in cui un server del sistema del sito specifico non sia in linea.  

 **Installare più istanze del provider SMS in un sito:** il provider SMS fornisce il punto di contatto amministrativo per una o più console di Configuration Manager. Quando si installano più provider SMS, è possibile fornire ridondanza per i punti di contatto per l'amministrazione del sito e della gerarchia.  

##  <a name="bkmk_ssr"></a> Disponibilità elevata per ruoli del sistema del sito  
 In ogni sito, si distribuiscono i ruoli del sistema del sito per fornire i servizi che si desidera che i client utilizzino in tale sito. Il database del sito contiene le informazioni di configurazione per il sito e per tutti i client. Utilizzare una o più delle opzioni disponibili per fornire elevata disponibilità al database del sito, nonché il ripristino del sito e del database del sito se necessario.  

 **Ridondanza per ruoli del sistema del sito importanti:**  

-   Punto per servizi Web del Catalogo applicazioni  

-   Punto per siti Web del Catalogo applicazioni  

-   Punto di distribuzione  

-   Punto di gestione  

-   Punto di aggiornamento software  

-   Punto di migrazione stato  

 È possibile installare più istanze del ruolo del punto di Reporting Services per garantire ridondanza per la creazione di report su siti e client.

 È possibile usare PowerShell per installare il ruolo del sistema del sito del punto di aggiornamento software in un cluster Bilanciamento del carico di rete Windows e offrire il supporto per il failover  


 **Backup del sito incorporato:**  

 Configuration Manager include un'attività di backup predefinita che permette di eseguire il backup del sito e delle informazioni critiche in base a una pianificazione regolare. Inoltre, l'Installazione guidata di Configuration Manager supporta azioni di ripristino del sito per ripristinare il normale funzionamento del sito.  

 **Pubblicazione in Active Directory Domain Services e DNS:**  

 È possibile configurare ciascun sito per pubblicare dati sui server del sistema del sito e servizi nei Servizi di dominio Active Directory e in DNS. Ciò consente ai client di identificare il server più accessibile in rete e di individuare quando sono disponibili nuovi server del sistema del sito che possono fornire servizi importanti, come i punti gestione.  

 **Provider SMS e console di Configuration Manager:**  

 Configuration Manager supporta l'installazione di più provider SMS, ognuno in un computer separato, per garantire più punti di accesso per la console di Configuration Manager. In questo modo, se un computer del provider SMS è offline, è possibile mantenere la capacità di visualizzare e riconfigurare i siti e i client di Configuration Manager.  

 Quando una console di Configuration Manager si connette a un sito, si connette a un'istanza del provider SMS nel sito. L'istanza del provider SMS viene selezionata in modo non deterministico. Se il provider SMS selezionato non è disponibile, è possibile scegliere tra le opzioni seguenti:  

-   Riconnettere la console al sito. A ogni nuova richiesta di connessione viene assegnata in modo non deterministico un'istanza del provider SMS ed è possibile che alla nuova connessione venga assegnata un'istanza disponibile.  

-   Connettere la console a un sito di Configuration Manager diverso e gestire la configurazione da questa connessione. Questo introduce un leggero ritardo di modifiche alla configurazione di non più di pochi minuti. Quando il provider SMS per il sito è online, è possibile riconnettere la console di Configuration Manager direttamente al sito che si vuole gestire.  

 È possibile installare la console di Configuration Manager in più computer per permetterne l'uso agli utenti amministratori. Ogni provider SMS supporta le connessioni da più console di Configuration Manager.  

 **Punto di gestione:**  

 Installare più punti di gestione su ciascun sito primario e abilitare i siti alla pubblicazione dei dati del sito sull'infrastruttura di Active Directory e in DNS.  

 Più punti di gestione consentono di bilanciare il carico dell'utilizzo di un unico punto di gestione da parte di più client. Inoltre, è possibile installare uno o più repliche di database affinché i punti di gestione diminuiscano le operazioni con utilizzo elevato di CPU del punto di gestione e aumentino la disponibilità di questo ruolo del sistema del sito critico.  

 Poiché è possibile installare solo un punto di gestione in un sito secondario, che si deve trovare sul server del sito secondario, si considera che i punti di gestione sui siti secondari non abbiano una configurazione a elevata disponibilità.  

> [!NOTE]  
>  I dispositivi mobili gestiti in locale si connettono solo a un punto di gestione nel sito primario. Il punto di gestione viene assegnato da Configuration Manager al dispositivo mobile durante la registrazione e in seguito non cambia. Quando si installano più punti di gestione e se ne abilita più di uno per i dispositivi mobili, il punto di gestione assegnato a un client del dispositivo mobile non è deterministico.  
>   
>  Se il punto di gestione usato da un client del dispositivo mobile non è più disponibile, occorre risolvere il problema del punto di gestione oppure cancellare il dispositivo mobile e registrarlo di nuovo in modo che possa essere assegnato a un punto di gestione operativo abilitato per i dispositivi mobili.  

 **Punto di distribuzione:**  

 Installare più punti di distribuzione e distribuire il contenuto in più punti di distribuzione. È possibile configurare gruppi di limiti sovrapposti per percorso di contenuto per assicurarsi che i client su ciascuna subnet possano accedere a una distribuzione da due o più punti di distribuzione. Infine, è possibile configurare uno o più punti di distribuzione come posizioni di fallback per il contenuto.  

 Per altre informazioni sui percorsi di fallback, vedere [Manage content and content infrastructure for System Center Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md) (Gestire il contenuto e l'infrastruttura del contenuto per System Center Configuration Manager).  

 **Punto per servizi Web del Catalogo applicazioni e punto per siti Web del Catalogo applicazioni:**  

 È possibile installare più istanze di ogni ruolo di sistema del sito e, per ottenere migliori prestazioni, distribuire un'istanza per ogni ruolo nello stesso computer di sistema del sito.  

 Ogni ruolo di sistema del sito del Catalogo applicazioni fornisce le stesse informazioni rispetto alle altre istanze di tale ruolo, indipendentemente dalla posizione del ruolo di sistema del sito nella gerarchia. Pertanto, quando un client richiede il Catalogo applicazioni e l'impostazione Punto per siti Web del Catalogo applicazioni predefinito del client del dispositivo è stata impostata su Rileva automaticamente, sarà possibile indirizzare il client a un'istanza disponibile usando preferibilmente i server di sistema del sito locali del Catalogo applicazioni, in base alla posizione di rete corrente del client.  

 Per altre informazioni su questa impostazione del client e sul funzionamento del rilevamento automatico, vedere la sezione [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent) (Agente computer) nell'argomento [About Client Settings in Configuration Manager](../../core/clients/deploy/about-client-settings.md) (Informazioni sulle impostazioni client in Configuration Manager).  

##  <a name="bkmk_client"></a> Disponibilità elevata per i client  
 **Le operazioni dei client sono autonome:**  

 L'autonomia del client di Configuration Manager include quanto segue:  

-   I client non richiedono un contatto continuo con qualsiasi server del sistema del sito specifico. Utilizzano configurazioni note per eseguire azioni preconfigurate in base a una pianificazione.  

-   I client possono utilizzare qualsiasi istanza disponibile di un ruolo del sistema del sito che fornisca servizi ai client ed esse tenteranno di contattare i server conosciuti fino a quando non viene individuato un server disponibile.  

-   I client possono eseguire inventari, distribuzioni software e analoghe azioni pianificate indipendenti dal contatto diretto con i server del sistema del sito.  

-   I client configurati per l'utilizzo di un punto di stato di fallback possono inviare dettagli al punto di stato di fallback quando non riescono a comunicare con un punto di gestione.  

 **I client sono in grado di ripristinarsi da soli:**  

 I client correggono automaticamente i problemi più comuni senza un intervento amministrativo diretto:  

-   periodicamente, i client valutano autonomamente il proprio stato e intraprendono azioni per correggere problemi comuni utilizzando una cache locale di passaggi correttivi e file di origine per i ripristini.  

-   Quando un client non riesce a inviare informazioni al proprio sito, il sito può generare un avviso. Gli utenti amministratori che ricevono questi avvisi possono richiedere un intervento immediato per ripristinare il normale funzionamento del client.  

 **I client memorizzano nella cache informazioni da usare in futuro:**  

 Quando un client comunica con un punto di gestione, il client può ottenere e memorizzare nella cache le informazioni seguenti:  

-   Impostazioni client.  

-   Pianificazioni client.  

-   Informazioni su distribuzioni software e un download del software che il client ha pianificato di installare, quando la distribuzione è configurata per queste azioni.  

 Se non riescono a contattare un punto di gestione, i client memorizzano nella cache locale lo stato e le informazioni client che inviano al sito e trasferiscono questi dati dopo aver stabilito un contatto con un punto di gestione.  

 **Il client può inviare lo stato a un punto di stato di fallback:**  

 Quando si configura un client per l'uso di un punto di stato di fallback, si fornisce un punto aggiuntivo di contatto per consentire al client di inviare dettagli importanti sul proprio funzionamento. i client configurati per utilizzare un punto di stato di fallback continuano a inviare lo stato delle operazioni a quel ruolo del sistema del sito anche quando il client non riesce a comunicare con un punto di gestione.  

 **Gestione centrale dei dati client e identità client:**  

 Il database del sito, anziché il client singolo, mantiene informazioni importanti sull'identità di ogni client e associa tali dati a un computer o a un utente specifico. Ciò significa che:  

-   I file di origine del client in un computer possono essere disinstallati e reinstallati senza influire sui record cronologici del computer in cui è installato il client.  

-   Eventuali errori di un computer client non compromettono l'integrità delle informazioni archiviate nel database. Queste informazioni possono rimanere disponibili per la creazione di report.  

##  <a name="bkmk_nonHAoptions"></a> Opzioni per siti e ruoli del sistema del sito non a disponibilità elevata  
 Alcuni sistemi del sito non supportano istanze multiple in un sito o nella gerarchia. Queste informazioni consentono di prepararsi per i casi in cui i sistemi del sito passano in modalità offline.  

 **Server del sito (sito):**  

 Configuration Manager non supporta l'installazione del server del sito per ogni sito in un cluster di Windows Server o in un cluster Bilanciamento carico di rete.  

 Le seguenti informazioni consentono la preparazione per situazioni di errore o di mancata operatività di un server del sito:  

-   Per creare regolarmente un backup del sito, utilizzare l'attività di backup incorporato. In un ambiente di prova, esercitarsi regolarmente nel ripristino di siti da un backup.  

-   Distribuire più siti primari di Configuration Manager in una gerarchia con un sito di amministrazione centrale per creare ridondanza. In caso di errore del sito, valutare l'utilizzo dei Criteri di gruppo di Windows o degli script di accesso per riassegnare i client a un sito funzionante.  

-   Se è disponibile una gerarchia con un sito di amministrazione centrale, sarà possibile ripristinare il sito di amministrazione centrale o un sito primario figlio utilizzando l'opzione per il ripristino di un database del sito da un altro sito nella gerarchia.  

-   I siti secondari non possono essere ripristinati e devono essere reinstallati.  

 **Punto di sincronizzazione di Asset Intelligence (gerarchia):**  

 Questo ruolo di sistema del sito non è considerato cruciale e rappresenta una funzionalità facoltativa in Configuration Manager. Se questo sistema non risulta più in linea, utilizzare una delle seguenti opzioni:  

-   Risolvere la causa della mancata presenza online del sistema del sito.  

-   Disinstallare il ruolo dal server corrente e installare il ruolo in un nuovo server.  

 **Punto di Endpoint Protection (gerarchia):**  

 Questo ruolo di sistema del sito non è considerato cruciale e rappresenta una funzionalità facoltativa in Configuration Manager. Se questo sistema non risulta più in linea, utilizzare una delle seguenti opzioni:  

-   Risolvere la causa della mancata presenza online del sistema del sito.  

-   Disinstallare il ruolo dal server corrente e installare il ruolo in un nuovo server.  

 **Punto di registrazione (sito):**  

 Questo ruolo di sistema del sito non è considerato cruciale e rappresenta una funzionalità facoltativa in Configuration Manager. Se questo sistema non risulta più in linea, utilizzare una delle seguenti opzioni:  

-   Risolvere la causa della mancata presenza online del sistema del sito.  

-   Disinstallare il ruolo dal server corrente e installare il ruolo in un nuovo server.  

 **Punto proxy di registrazione (sito):**  

 Questo ruolo di sistema del sito non è considerato cruciale e rappresenta una funzionalità facoltativa in Configuration Manager. Tuttavia, è possibile installare più istanze di questo ruolo di sistema del sito in un sito e in più siti nella gerarchia. Se questo sistema non risulta più in linea, utilizzare una delle seguenti opzioni:  

-   Risolvere la causa della mancata presenza online del sistema del sito.  

-   Disinstallare il ruolo dal server corrente e installare il ruolo in un nuovo server.  

 Quando si dispone di più server proxy di registrazione in un sito, è possibile utilizzare un alias DNS per il nome del server. Quando si utilizza questa configurazione, round robin DNS fornisce tolleranza d'errore e bilanciamento del carico parziali per la fase di registrazione dei dispositivi mobili da parte degli utenti.  

 **Punto di stato di fallback (sito o gerarchia):**  

 Questo ruolo di sistema del sito non è considerato cruciale e rappresenta una funzionalità facoltativa in Configuration Manager. Se questo sistema non risulta più in linea, utilizzare una delle seguenti opzioni:  

-   Risolvere la causa della mancata presenza online del sistema del sito.  

-   Disinstallare il ruolo dal server corrente e installare il ruolo in un nuovo server. Poiché il punto di stato di fallback viene assegnato ai client durante l'installazione, sarà necessario modificare i client esistenti in modo che utilizzino il nuovo server di sistema del sito.  

### <a name="see-also"></a>Vedere anche  
 [Supported configurations for System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md) (Configurazioni supportate per System Center Configuration Manager)

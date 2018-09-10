---
title: Configurare gruppi di limiti
titleSuffix: Configuration Manager
description: Aiutare i client a trovare i sistemi del sito usando i gruppi di limiti per organizzare logicamente i percorsi di rete correlati chiamati limiti
ms.date: 08/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 232dbaa0bca1507d3b743174be649281f46ab52d
ms.sourcegitcommit: 52ec30245ba559596d2f88a3eff70c467b4a056f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/01/2018
ms.locfileid: "43381017"
---
# <a name="configure-boundary-groups-for-configuration-manager"></a>Configurare gruppi di limiti per Configuration Manager


*Si applica a: System Center Configuration Manager (Current Branch)*

Usare i gruppi di limiti in Configuration Manager per organizzare logicamente i percorsi di rete correlati ([limiti](/sccm/core/servers/deploy/configure/boundaries)) e semplificare la gestione dell'infrastruttura. Prima di usare il gruppo di limiti, assegnare i limiti ai gruppi di limiti.

Per impostazione predefinita, Configuration Manager crea un gruppo di limiti predefinito in ogni sito.

Per configurare i gruppi di limiti, associare i limiti (percorsi di rete) e i ruoli del sistema del sito, come i punti di distribuzione, al gruppo di limiti. Questa configurazione consente di associare i client ai server del sistema del sito, come i punti di distribuzione, che si trovano vicino ai client nella rete.

Per aumentare la disponibilità dei server dei sistemi del sito per una gamma più ampia di percorsi di rete, assegnare lo stesso limite e lo stesso server a più gruppi di limiti.

I client usano un gruppo di limiti per gli scopi seguenti:  

-   Assegnazione automatica al sito  
-   Ricerca di un server del sistema del sito che può fornire un servizio, tra cui:  
    - Punti di distribuzione per il percorso del contenuto  
    - Punti di aggiornamento software  
    - Punti di migrazione dello stato  
    - Punti di gestione preferiti  

        > [!Note]  
        > Se si usano i punti di gestione preferiti, è necessario abilitare questa opzione per la gerarchia e non dall'interno della configurazione del gruppo di limiti. Per altre informazioni, vedere [Abilitare l'uso dei punti di gestione preferiti](#to-enable-use-of-preferred-management-points).  



##  <a name="boundary-groups-and-relationships"></a>Gruppi di limiti e relazioni

Per ogni gruppo di limiti nella gerarchia, è possibile assegnare:

- Uno o più limiti. Il gruppo di limiti **corrente** di un client è un percorso di rete definito come limite assegnato a un gruppo di limiti specifico. Un client può avere più di un gruppo di limiti corrente.  

- Uno o più ruoli del sistema del sito. I client possono usare sempre i ruoli del sistema del sito associati al gruppo di limiti corrente. A seconda delle configurazioni aggiuntive, possono essere in grado di usare i ruoli del sistema del sito in gruppi di limiti aggiuntivi.  

Per ogni gruppo di limiti creato, è possibile configurare un collegamento unidirezionale a un altro gruppo di limiti. Il collegamento è definito **relazione**. I gruppi di limiti con cui si stabilisce il collegamento sono chiamati gruppi di limiti **adiacenti**. Un gruppo di limiti può avere più relazioni, ciascuna con uno specifico gruppo di limiti adiacente.

Se un client non riesce a trovare un server del sistema del sito disponibile nel gruppo di limiti corrente, la configurazione di ogni relazione determina quando iniziare a cercare in un gruppo di limiti adiacente. Questa ricerca in altri gruppi è definita **fallback**.

Per altre informazioni, vedere le procedure seguenti:  
- [Creare un gruppo di limiti](#bkmk_create)  
- [Configurare un gruppo di limiti](#bkmk_config)  



## <a name="fallback"></a>Fallback

Per evitare problemi quando i client non riescono a trovare un sistema del sito disponibile nel gruppo di limiti corrente, definire la relazione tra i gruppi di limiti per il comportamento di fallback. Il fallback consente a un client di espandere la ricerca di un sistema del sito disponibile a gruppi di limiti aggiuntivi.

Le relazioni vengono configurate in una scheda **Relazioni** delle proprietà del gruppo di limiti. Quando si configura una relazione, si definisce un collegamento a un gruppo di limiti adiacente. Per ogni tipo di ruolo del sistema del sito supportato, configurare impostazioni indipendenti per il fallback a tale gruppo di limiti adiacente. Per altre informazioni, vedere [Configurare il comportamento di fallback](#bkmk_bg-fallback).

Ad esempio, quando si configura una relazione con un gruppo di limiti specifico, impostare il fallback per i punti di distribuzione dopo 20 minuti. Il valore predefinito è 120 minuti. Per un esempio più esteso, vedere [Esempio d'uso dei gruppi di limiti](#example-of-using-boundary-groups).

Se un client non riesce a trovare un ruolo del sistema del sito disponibile nel gruppo di limiti corrente, il client usa il tempo di fallback in minuti. Tale tempo di fallback determina quando il client inizia a eseguire la ricerca di un sistema del sito disponibile associato al gruppo di limiti adiacente.  

Se un client non riesce a trovare un sistema del sito disponibile, inizia la ricerca nei percorsi dei gruppi di limiti adiacenti. Questo comportamento aumenta il pool di sistemi del sito disponibili. La configurazione dei gruppi di limiti e delle relative relazioni definisce l'uso del client di questo pool di sistemi del sito disponibili.

- Un gruppo di limiti può avere più di una relazione. Con più relazioni è possibile configurare il fallback per ogni tipo di sistema del sito a diversi gruppi adiacenti dopo diversi intervalli di tempo.    

- I client eseguono il fallback solo in un gruppo di limiti direttamente adiacente al loro gruppo di limiti corrente.  

- Se un client fa parte di più gruppi di limiti, il relativo gruppo di limiti corrente è definito come l'unione di tutti i gruppi di limiti. Il client esegue il fallback ai gruppi adiacenti di uno dei gruppi di limiti originali.  


### <a name="the-default-site-boundary-group"></a>Gruppo di limiti predefinito del sito

Oltre ai gruppi di limiti che è possibile creare, ogni sito dispone di un gruppo di limiti predefinito creato da Configuration Manager. Questo gruppo è denominato **Default-Site-Boundary-Group&lt;codicesito>**. Ad esempio, il gruppo per il sito ABC sarebbe denominato **Default-Site-Boundary-Group&lt;ABC>**.

Per ogni gruppo di limiti creato, Configuration Manager crea automaticamente un collegamento implicito a ogni gruppo di limiti predefinito del sito nella gerarchia.  

- Il collegamento implicito è un'opzione di fallback predefinita da un gruppo di limiti corrente al gruppo di limiti predefinito del sito. Il tempo di fallback predefinito è 120 minuti.  

- Per i client che non si trovano in un limite associato a un gruppo di limiti: per identificare i ruoli del sistema del sito validi, usare il gruppo di limiti predefinito dal sito assegnato.  


Per gestire il fallback al gruppo di limiti predefinito del sito:  

- Aprire le proprietà del gruppo di limiti predefinito del sito e modificare i valori nella scheda **Comportamento predefinito**. Le modifiche apportate in questa scheda si applicano a *tutti* i collegamenti impliciti a questo gruppo di limiti. Quando si configura un collegamento esplicito a questo gruppo di limiti del sito predefinito da un altro gruppo di limiti, le impostazioni predefinite vengono sostituite.  

- Aprire le proprietà di un gruppo di limiti personalizzato. Modificare i valori per il collegamento esplicito a un gruppo di limiti predefinito del sito. Quando si imposta un nuovo intervallo in minuti per il fallback o il blocco del fallback, la modifica influisce solo sul collegamento che si sta configurando. La configurazione del collegamento esplicito sostituisce quella della scheda **Comportamento predefinito** di un gruppo di limiti predefinito del sito.  



## <a name="site-assignment"></a>Assegnazione sito  

 È possibile configurare ciascun gruppo di limiti con un sito assegnato per i client.  

-   Un client appena installato che usa l'assegnazione automatica sito viene aggiunto al sito assegnato di un gruppo di limiti che contiene il percorso di rete corrente del client.  

-   Dopo l'assegnazione a un sito, un client non cambia la propria assegnazione sito quando cambia il percorso di rete. Ad esempio, un client effettua il roaming in un nuovo percorso di rete. Questo percorso è un limite in un gruppo di limiti con un'assegnazione sito diversa. Il sito assegnato del client non cambia.  

-   Quando l'individuazione sistema Active Directory rileva una nuova risorsa, il sito valuta le informazioni di rete per la risorsa individuata in rapporto ai limiti nei gruppi di limiti. Tramite questo processo la nuova risorsa viene associata a un sito assegnato per poter essere utilizzata dal metodo di installazione push client.  

-   Quando un limite è membro di più gruppi di limiti con diversi siti assegnati, i client selezionano uno dei siti in modo casuale.  

-   Le modifiche a un sito assegnato a gruppi di limiti si applicano solo alle nuove azioni di assegnazione sito. I client assegnati precedentemente a un sito non valutano di nuovo l'assegnazione sito in base alle modifiche alla configurazione di un gruppo di limiti (o al proprio percorso di rete).  

Per altre informazioni sull'assegnazione sito per i client, vedere [Utilizzo dell'assegnazione automatica del sito per i computer](/sccm/core/clients/deploy/assign-clients-to-a-site#BKMK_AutomaticAssignment).  

Per altre informazioni su come configurare l'assegnazione sito, vedere le procedure seguenti:
- [Configurare l'assegnazione sito e selezionare i server del sistema del sito](#bkmk_references)
- [Configurare un sito di fallback per l'assegnazione sito automatica](#bkmk_site-fallback)



## <a name="distribution-points"></a>Punti di distribuzione

Quando un client richiede il percorso di un punto di distribuzione, Configuration Manager invia al client un elenco dei sistemi del sito. Questi sistemi del sito sono del tipo appropriato associato a ogni gruppo di limiti che include il percorso di rete corrente del client:

-   **Durante la distribuzione del software**, i client richiedono un percorso per il contenuto di distribuzione in un'origine contenuto valida. Questo percorso può essere un punto di distribuzione o un'origine peer cache.  

-   **Durante la distribuzione del sistema operativo**, i client richiedono un percorso per l'invio o la ricezione delle informazioni di migrazione dello stato.  

Quando viene distribuito il contenuto, se un client richiede contenuto non disponibile da un'origine nel gruppo di limiti corrente, il client continua a richiedere tale contenuto. Il client prova diverse origini del contenuto nel gruppo di limiti corrente finché non raggiunge il periodo di fallback per un gruppo di limiti adiacente o per il gruppo di limiti del sito predefinito. Se il client non ha ancora trovato il contenuto, estende la ricerca alle origini contenuto in modo da includere i gruppi di limiti adiacenti.

Se il contenuto viene distribuito su richiesta e non è disponibile quando richiesto in un punto di distribuzione, viene avviato il processo di trasferimento del contenuto a quel punto di distribuzione. È possibile che il client rilevi il server come origine contenuto prima di eseguire il fallback per l'uso di un gruppo di limiti adiacente.


### <a name="bkmk_bgoptions"></a> Opzioni del gruppo di limiti per download peer

<!--1356193--> A partire dalla versione 1806, sono disponibili impostazioni aggiuntive per i gruppi di limiti per offrire maggiore controllo sulla distribuzione di contenuti nell'ambiente. Per altre informazioni, vedere [Configurare un gruppo di limiti](#bkmk_config).

#### <a name="allow-peer-downloads-in-this-boundary-group"></a>Consenti i download peer in questo gruppo di limiti
Questa opzione è attivata per impostazione predefinita. Il punto di gestione fornisce ai client un elenco di posizioni del contenuto che include le origini peer. Questa impostazione influisce anche sull'applicazione di ID di gruppo per l'[ottimizzazione recapito](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization).  

Esistono due scenari comuni in cui potrebbe essere utile disabilitare questa opzione:  

- In presenza di un gruppo di limiti che include limiti da posizioni geograficamente dislocate, come una VPN. Due client possono essere inclusi nello stesso gruppo di limiti perché sono connessi tramite VPN, ma trovarsi in luoghi molto lontani non appropriati per la condivisione peer del contenuto.  

- Se si usa un singolo gruppo di limiti di grandi dimensioni per l'assegnazione del sito che non fa riferimento ad alcun punto di distribuzione.  

#### <a name="during-peer-downloads-only-use-peers-within-the-same-subnet"></a>Durante i download peer, usa solo i peer entro la stessa subnet
Questa impostazione dipende da quella precedente. Se si abilita questa opzione, il punto di gestione include nell'elenco delle posizioni del contenuto solo le origini peer incluse nella stessa subnet del client.

Scenari comuni per l'abilitazione di questa opzione:

- La progettazione del gruppo di limiti per la distribuzione del contenuto include un solo gruppo di limiti di grandi dimensioni che si sovrappone ad altri gruppi di limiti più piccoli. Con questa nuova impostazione, l'elenco di origini di contenuto che il punto di gestione fornisce ai client include solo le origini peer dalla stessa subnet.

- È disponibile un singolo gruppo di limiti di grandi dimensioni per tutti gli uffici remoti. Abilitare questa opzione e i client potranno condividere solo il contenuto all'interno della subnet nell'ufficio remoto, invece di correre i rischi correlati alla condivisione del contenuto tra posizioni diverse.




## <a name="software-update-points"></a>Punti di aggiornamento software

I client usano i gruppi di limiti per trovare un nuovo punto di aggiornamento software. Per controllare quali server possono essere trovati da un client, aggiungere singoli punti di aggiornamento software a diversi gruppi di limiti.

Se si esegue l'aggiornamento da una versione precedente alla 1702, ogni sito aggiunge tutti i punti di aggiornamento software esistenti al gruppo di limiti predefinito in ogni sito. Questo comportamento di aggiornamento del sito mantiene il comportamento del client precedente per selezionare un punto di aggiornamento software dal pool di server disponibili. Questo comportamento viene mantenuto finché non si sceglie di aggiungere singoli punti di aggiornamento software a gruppi di limiti diversi per un comportamento di selezione e fallback controllato.

Se si installa un nuovo sito, i punti di aggiornamento software non vengono aggiunti al gruppo di limiti del sito predefinito. Assegnare i punti di aggiornamento software a un gruppo di limiti in modo che i client possano trovarli e usarli.


### <a name="fallback-for-software-update-points"></a>Fallback per i punti di aggiornamento software

Il fallback per i punti di aggiornamento software è configurato come altri ruoli del sistema del sito, ma con le avvertenze seguenti:  

#### <a name="new-clients-use-boundary-groups-to-select-software-update-points"></a>I nuovi client usano i gruppi di limiti per selezionare i punti di aggiornamento software
I nuovi client installati selezionano un punto di aggiornamento software dai server associati ai gruppi di limiti configurati. Ciò sostituisce il comportamento precedente in cui i client selezionano un punto di aggiornamento software in maniera casuale da un elenco di server che condividono la foresta dei client.

#### <a name="clients-continue-to-use-a-last-known-good-software-update-point-until-they-fallback-to-find-a-new-one"></a>I client continuano a usare l'ultimo punto di aggiornamento software valido noto fino a quando non eseguono il fallback per trovare un nuovo punto
I client che hanno già un punto di aggiornamento software continuano a usarlo fino a quando non può essere raggiunto. Questo comportamento include l'uso continuativo di un punto di aggiornamento software non associato al gruppo di limiti corrente del client.

Si tratta di un comportamento intenzionale. Il client continua a usare un punto di aggiornamento software esistente anche se non è incluso nel gruppo di limiti corrente del client. Quando il punto di aggiornamento software viene modificato, il client sincronizza i dati con il nuovo server, il che determina un uso significativo della rete. Se tuti client i client passano contemporaneamente a un nuovo server, il ritardo nella transizione può evitare la saturazione della rete.

#### <a name="a-client-always-tries-to-reach-its-last-known-good-software-update-point-for-120-minutes-before-starting-fallback"></a>Un client prova sempre a raggiungere l'ultimo punto di aggiornamento software valido noto per 120 minuti prima di avviare il fallback
Dopo 120 minuti, se il client non ha stabilito il contatto, inizia il fallback. All'avvio del fallback, il client riceve un elenco di tutti i punti di aggiornamento software nel gruppo di limiti corrente. I punti di aggiornamento software aggiuntivi del gruppo di limiti predefinito del sito e di quelli adiacenti sono disponibili in base alle configurazioni di fallback.


### <a name="fallback-configurations-for-software-update-points"></a>Configurazioni di fallback per i punti di aggiornamento software

#### <a name="beginning-with-version-1706"></a>A partire dalla versione 1706   
È possibile impostare **Orari di fallback (in minuti)** per i punti di aggiornamento software su meno di 120 minuti. Il client prova comunque a raggiungere il punto di aggiornamento software originale per 120 minuti. La ricerca viene quindi espansa su server aggiuntivi. I tempi di fallback del gruppo di limiti iniziano la prima volta in cui il client non riesce a raggiungere il server originale. Quando il client espande la ricerca, il sito specifica tutti i gruppi di limiti configurati per meno di 120 minuti.

Per bloccare il fallback per un punto di aggiornamento software a un gruppo di limiti adiacente, configurare l'impostazione su **Non eseguire mai il fallback**.

Dopo l'esito negativo nel raggiungere il server originale per due ore, il client usa quindi un ciclo più breve per stabilire una connessione a un nuovo punto di aggiornamento software. In questo modo il client può eseguire rapidamente una ricerca nell'elenco in espansione di potenziali punti di aggiornamento software.

#### <a name="example"></a>Esempio
Si configurano punti di aggiornamento software nel gruppo di limiti *A* per il fallback dopo **10** minuti. Si configura la stessa impostazione per il gruppo di limiti *B* per **130** minuti. Un client nel gruppo di limiti *Z* non riesce a raggiungere l'ultimo punto di aggiornamento software valido noto.

- Per i successivi 120 minuti, il client prova a raggiungere solo il server originale nel gruppo di limiti Z. Dopo 10 minuti, Configuration Manager aggiunge i punti di aggiornamento software del gruppo di limiti A al pool di server disponibili. Il client tuttavia non prova a contattare questi o altri server fino a che non è trascorso il periodo iniziale di 120 minuti.  

- Dopo avere provato a contattare il punto di aggiornamento software originale per 120 minuti, il client espande la ricerca. Aggiunge i server al pool disponibile di punti di aggiornamento software che si trovano nel gruppo di limiti corrente e in quelli adiacenti con una configurazione di 120 minuti o meno. Questo pool include i server nel gruppo di limiti A, aggiunti in precedenza al pool di server disponibili.  

- Dopo altri 10 minuti, il client espande la ricerca per includere i punti di aggiornamento software del gruppo di limiti B. Il tempo totale è di 130 minuti dopo il primo tentativo non riuscito del client di raggiungere l'ultimo punto di aggiornamento software valido noto.  


#### <a name="versions-1702-and-earlier"></a>Versioni 1702 e precedenti
Con la versione 1702 e le versioni precedenti, le configurazioni di fallback per i punti di aggiornamento software non supportano un tempo configurabile in minuti. Il comportamento di fallback è invece limitato alle opzioni seguenti:

- **Orari di fallback (in minuti):** questa opzione è impostata su 120 minuti. Non è possibile configurarla.  

- **Non eseguire mai il fallback:** viene bloccato il fallback per un punto di aggiornamento software in un gruppo di limiti adiacente.  

Quando un client che ha già un punto di aggiornamento software non riesce a raggiungerlo, esegue il fallback per trovarne un altro. Quando usa il fallback, il client riceve un elenco di tutti i punti di aggiornamento software per il gruppo di limiti corrente. Se non riesce a trovare un server disponibile per 120 minuti, esegue il fallback ai gruppi di limiti adiacenti e al gruppo di limiti predefinito del sito. Il fallback a entrambi i gruppi di limiti avviene nello stesso momento. Il tempo di fallback del punto di aggiornamento software ai gruppi di limiti adiacenti è impostato su 120 minuti. Non è possibile modificare questo tempo di fallback. L'intervallo di 120 minuti è anche il periodo predefinito usato per il fallback al gruppo di limiti predefinito del sito. Quando un client esegue il fallback in un gruppo di limiti adiacente e nel gruppo di limiti del sito predefinito, prova a contattare i punti di aggiornamento software del gruppo di limiti adiacente prima di provare a usare uno di quelli del gruppo di limiti predefinito del sito.


### <a name="manually-switch-to-a-new-software-update-point"></a>Passare manualmente a un nuovo punto di aggiornamento software

Oltre a usare il fallback, usare la notifica client per forzare manualmente il passaggio di un dispositivo a un nuovo punto di aggiornamento software.

Quando si passa a un nuovo server, i dispositivi usano il fallback per trovare il nuovo server. Esaminare le configurazioni del gruppo di limiti. Prima di apportare questa modifica, verificare che i punti di aggiornamento software si trovino nei gruppi di limiti corretti.

Per altre informazioni, vedere [Passaggio manuale dei client a un nuovo punto di aggiornamento software](/sccm/sum/plan-design/plan-for-software-updates#manually-switch-clients-to-a-new-software-update-point).



## <a name="management-points"></a>Punti di gestione
<!-- 1324594 --> A partire dalla versione 1802, è possibile configurare relazioni di fallback per i punti di gestione tra gruppi di limiti. Questo comportamento consente un maggiore controllo per i punti di gestione usati dai client. Nella scheda **Relazioni** delle proprietà del gruppo di limiti è presente una colonna per il punto di gestione. Quando si aggiunge un nuovo gruppo di limiti di fallback, attualmente il tempo di fallback per il punto di gestione è sempre zero (0). Questo comportamento corrisponde all'opzione **Comportamento predefinito** del gruppo di limiti predefinito del sito.

Nelle versioni precedenti si verifica comunemente un problema in presenza di un punto di gestione protetto in una rete protetta. I client nella rete aziendale principale ricevono criteri che includono questo punto di gestione protetto, anche se non possono comunicare con esso attraverso un firewall. Per risolvere il problema, usare l'opzione **Non eseguire mai il fallback** per fare in modo che i client eseguano il fallback solo nei punti di gestione con cui possono comunicare.

Quando si aggiorna il sito alla versione 1802, Configuration Manager aggiunge tutti i punti di gestione Intranet nel gruppo di limiti predefinito del sito. Questo gruppo di server non include i punti di gestione solo Internet. Questo comportamento dell'aggiornamento assicura che le versioni client precedenti continuino a comunicare con i punti di gestione. Per sfruttare tutti i vantaggi di questa funzionalità, spostare i punti di gestione nei gruppi di limiti desiderati.

> [!Note]  
> Se si abilitano i punti di distribuzione nel gruppo di limiti predefinito del sito per il fallback e un punto di gestione si trova nella stessa posizione di un punto di distribuzione, il sito aggiunge anche tale punto di gestione al gruppo di limiti predefinito del sito.<!--VSO 2841292-->  

Se un client si trova in un gruppo di limiti senza alcun punto di gestione assegnato, il sito fornisce al client l'intero elenco di punti di gestione. Questo comportamento garantisce che un client riceva sempre un elenco di punti di gestione.

Il comportamento del fallback dei gruppi di limiti dei punti di gestione non cambia durante l'installazione dei client (ccmsetup.exe). Se la riga di comando non specifica il punto di gestione iniziale tramite il parametro /MP, il nuovo client riceve l'elenco completo dei punti di gestione disponibili. Per il processo di avvio iniziale, il client usa il primo punto di gestione a cui può accedere. Una volta registratosi con il sito, il client riceve l'elenco dei punti di gestione correttamente ordinato con questo nuovo comportamento. 

Durante l'aggiornamento del client, se non si specifica il parametro della riga di comando /MP, il client esegue query sulle origini, come Active Directory e WMI, per qualsiasi punto di gestione disponibile. L'aggiornamento dei client non rispetta la configurazione dei gruppi di limiti. <!--VSO 2841292-->  

Per consentire ai client di usare questa funzionalità, abilitare l'impostazione seguente: **I client preferiscono usare i punti di gestione specificati nei gruppi di limiti** in **Impostazioni gerarchia**. 

> [!Note]  
> I processi di distribuzione dei sistemi operativi non sono a conoscenza dei gruppi di limiti.  


### <a name="troubleshooting"></a>Troubleshooting

Nel log **LocationServices.log** sono presenti nuove voci. L'attributo **Locality** identifica uno degli stati seguenti:

- **0**: sconosciuto  

- **1**: il punto di gestione specificato si trova solo nel gruppo di limiti predefinito del sito per il fallback  

- **2**: il punto di gestione specificato si trova in un gruppo di limiti remoto o adiacente. Quando il punto di gestione si trova sia in un gruppo di limiti adiacente sia in quello predefinito del sito, l'attributo locality è uguale a 2.  

- **3**: il punto di gestione specificato si trova nel gruppo di limiti locale o corrente. Quando il punto di gestione si trova sia nel gruppo di limiti corrente e in uno adiacente o in quello predefinito del sito, l'attributo locality è uguale a 3. Se non si abilita l'impostazione dei punti di gestione preferiti in Impostazioni gerarchia, l'attributo locality è sempre uguale a 3, indipendentemente dal gruppo di limiti in cui si trova il punto di gestione.  

I client usano prima i punti di gestione locali (locality 3), quindi quelli remoti (locality 2) e infine eseguono il fallback (locality 1). 

Quando un client riceve cinque errori in 10 minuti e non riesce a comunicare con un punto di gestione nel relativo gruppo di limiti corrente, cerca di contattare un punto di gestione in un gruppo di limiti adiacente o in quello predefinito del sito. Se in seguito il punto di gestione nel gruppo di limiti corrente torna online, il client torna al punto di gestione locale al successivo ciclo di aggiornamento. Il ciclo di aggiornamento avviene ogni 24 ore o al riavvio del servizio agente di Configuration Manager.



## <a name="bkmk_preferred"></a> Punti di gestione preferiti

 > [!Note]
 > Il comportamento dell'impostazione gerarchia, **I client preferiscono usare i punti di gestione specificati nei gruppi di limiti** cambia a partire dalla versione 1802. Quando si abilita questa impostazione, Configuration Manager usa la funzionalità del gruppo di limiti per il punto di gestione assegnato. Per altre informazioni, vedere [Punti di gestione](#management-points). 

 I punti di gestione preferiti consentono a un client di identificare un punto di gestione associato al percorso di rete corrente (limite).  

- Il client prova a usare un punto di gestione preferito del sito assegnato prima di usarne uno non configurato come preferito per il sito assegnato.  

- Per usare questa opzione, abilitare **I client preferiscono usare i punti di gestione specificati nei gruppi di limiti** in **Impostazioni gerarchia**. Configurare quindi i gruppi di limiti nei singoli siti primari. Includere i punti di gestione che devono essere associati ai limiti associati del gruppo di limiti. Per altre informazioni, vedere [Abilitare l'uso dei punti di gestione preferiti](#bkmk_proc-prefer).  

- Quando si configurano i punti di gestione preferiti e un client organizza l'elenco dei punti di gestione, il client inserisce i punti di gestione preferiti all'inizio del relativo elenco. Questo elenco include tutti i punti di gestione dal sito assegnato del client.  

> [!NOTE]  
>  Il roaming del client si ha quando vengono modificati i percorsi di rete, ad esempio quando un computer portatile viene spostato in un ufficio remoto. Quando un client effettua il roaming, è possibile che usi un punto di gestione del sito locale prima di provare a usare un server del sito assegnato. Questo elenco di server dal sito assegnato include i punti di gestione preferiti. Per altre informazioni, vedere [Informazioni su come i client trovano i servizi e le risorse del sito](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services).  



## <a name="overlapping-boundaries"></a>Limiti sovrapposti  

 Configuration Manager supporta le configurazioni con sovrapposizione dei limiti per il percorso del contenuto. Quando il percorso di rete del client appartiene a più gruppi di limiti:

-   Quando un client richiede il contenuto, Configuration Manager invia al client un elenco di tutti i punti di distribuzione che hanno contenuto.  

-   Quando un client richiede a un server di inviare o ricevere le informazioni di migrazione dello stato, Configuration Manager invia al client un elenco di tutti i punti di migrazione dello stato associati a un gruppo di limiti che include il percorso di rete corrente del client.  

Questo comportamento consente al client di selezionare il server più vicino da cui trasferire le informazioni di migrazione dello stato o sul contenuto.  



## <a name="example-of-using-boundary-groups"></a>Esempio d'uso dei gruppi di limiti

L'esempio seguente usa un client che esegue la ricerca di contenuto da un punto di distribuzione. Questo esempio può essere applicato ad altri ruoli del sistema del sito che usano i gruppi di limiti. 

Creare tre gruppi di limiti che non condividono i limiti o i server del sistema del sito:  

- Gruppo BG_A con punti di distribuzione DP_A1 e DP_A2   

- Gruppo BG_B con punti di distribuzione DP_B1 e DP_B2  

- Gruppo BG_C con punti di distribuzione DP_C1 e DP_C2  

Aggiungere i percorsi di rete dei client come limiti solo al gruppo di limiti BG_A. Configurare quindi le relazioni da tale gruppo di limiti per gli altri due gruppi di limiti:  

- Configurare i punti di distribuzione per il primo gruppo *adiacente* (BG_B) da usare dopo 10 minuti. Questo gruppo contiene i punti di distribuzione DP_B1 e DP_B2. Entrambi sono ben connessi ai percorsi dei limiti del primo gruppo.  

- Configurare il secondo gruppo *adiacente* (BG_C) da usare dopo 20 minuti. Questo gruppo contiene i punti di distribuzione DP_C1 e DP_C2. Entrambi si trovano a un WAN rispetto agli altri due gruppi limite.  

- Aggiungere anche al gruppo di limiti del sito predefinito un punto di distribuzione aggiuntivo che si trova nel server del sito. Questo server è il percorso di origine del contenuto meno preferito, ma si trova in posizione centrale per tutti i gruppi di limiti.

    Esempio di gruppi di limiti e tempi di fallback:

     ![Esempio di gruppi di limiti e tempi di fallback](media/BG_Fallback.png)


Con questa configurazione:  

- Il client inizia la ricerca di contenuto dai punti di distribuzione nel gruppo di limiti *corrente* (BG_A). Cerca ogni punto di distribuzione per due minuti e quindi passa al punto di distribuzione successivo nel gruppo di limiti. Il pool di percorsi di origine del contenuto validi del client include DP_A1 e DP_A2.  

- Se il client non riesce a trovare il contenuto nel proprio gruppo limite *corrente* dopo 10 minuti di ricerca, aggiunge i punti di distribuzione dal gruppo limite BG_B alla ricerca. Prosegue quindi la ricerca di contenuto da un punto di distribuzione nel relativo pool combinato di server. Questo pool include ora i server dei gruppi di limiti BG_A e BG_B. Il client continua a contattare ogni punto di distribuzione per due minuti prima di passare al server successivo del pool. Il pool di percorsi di origine del contenuto validi del client include DP_A1, DP_A2, DP_B1 e DP_B2.  

- Dopo altri 10 minuti (20 minuti in totale), se il client non ha ancora trovato un punto di distribuzione con contenuto, espande il proprio pool per includere i server disponibili del secondo gruppo *adiacente*, il gruppo di limiti BG_C. Il client ha ora sei punti di distribuzione per la ricerca: DP_A1, DP_A2, DP_B1, DP_B2, DP_C1 e DP_C2. Continua la modifica in un nuovo punto di distribuzione ogni due minuti finché non trova il contenuto.  

- Se il client non ha trovato contenuto dopo un totale di 120 minuti, esegue il fallback per includere il *gruppo di limiti del sito predefinito* nella ricerca. Il pool include ora tutti i punti di distribuzione dei tre gruppi di limiti configurati e il punto di distribuzione finale presente nel server del sito. Il client continua quindi la ricerca del contenuto, modificando i punti di distribuzione ogni due minuti fino a quando il contenuto non viene trovato.  

Configurando i diversi gruppi adiacenti in modo da renderli disponibili in momenti diversi, è possibile controllare quando i punti di distribuzione specifici vengono aggiunti come percorso di origine del contenuto. Il client usa il fallback al gruppo di limiti del sito predefinito come garanzia per il contenuto che non è disponibile negli altri percorsi.



## <a name="changes-from-prior-versions"></a>Modifiche rispetto alle versioni precedenti

Di seguito sono riportate le modifiche principali ai gruppi di limiti e alle modalità di ricerca del contenuto da parte dei client in Configuration Manager Current Branch. Molti di queste modifiche e concetti funzionano in combinazione.


### <a name="configurations-for-fast-or-slow-are-removed"></a>Rimozione delle configurazioni per i punti lenti o veloci

I singoli punti di distribuzione non vengono più configurati come punti di distribuzione lenti o veloci. Al contrario, ogni sistema del sito associato a un gruppo limite viene trattato ugualmente. Grazie a questa modifica, la scheda **Riferimenti** delle proprietà del gruppo limite non supporta la configurazione Veloce o Lento.  


### <a name="new-default-boundary-group-at-each-site"></a>Nuovo gruppo di limiti predefinito in ogni sito

Ogni sito primario ha un nuovo gruppo di limiti predefinito denominato **Default-Site-Boundary-Group&lt;codicesito>**. Quando un client non si trova in un percorso di rete assegnato a un gruppo di limiti, usa i sistemi del sito associati al gruppo predefinito del sito assegnato. Considerare l'uso di questo gruppo limite come sostituzione del concetto di percorso del contenuto di fallback.     

#### <a name="allow-fallback-source-locations-for-content-is-removed"></a>Rimozione dell'opzione **Allow fallback source locations for content** (Consenti percorsi di origine di fallback per il contenuto)
La configurazione di un punto di distribuzione da usare per il fallback non avviene più in modo esplicito. Le opzioni per configurare questa impostazione vengono rimosse dalla console.

Il risultato dell'impostazione **Allow fallback source locations for content** (Consenti percorsi di origine di fallback per il contenuto) in un tipo di distribuzione per le applicazioni cambia. Questa impostazione su un tipo di distribuzione consente ora al client di usare il gruppo limite del sito predefinito come percorso di origine del contenuto.

#### <a name="boundary-groups-relationships"></a>Relazioni tra gruppi di limiti
È possibile collegare ogni gruppo di limiti a uno o più gruppi di limiti aggiuntivi. Questi collegamenti formano relazioni che è possibile configurare nella nuova scheda delle proprietà del gruppo di limiti denominata **Relazioni**:  

- Ogni gruppo limite associato direttamente a un client viene chiamato gruppo limite **corrente**.  

- Qualsiasi gruppo di limiti che un client può usare grazie all'associazione tra il gruppo di limiti *corrente* del client e un altro gruppo viene chiamato gruppo di limiti **adiacente**.  

- Nella scheda **Relazioni** aggiungere gruppi di limiti da usare come gruppo di limiti *adiacente*. Configurare anche un tempo in minuti per il fallback. Nel momento in cui un client non riesce a trovare il contenuto da un punto di distribuzione nel gruppo *corrente* avvia la ricerca dei percorsi del contenuto nei gruppi di limiti *adiacenti*.  

    Quando si aggiunge o si modifica una configurazione del gruppo di limiti, è possibile bloccare il fallback in tale gruppo di limiti dal gruppo corrente che si sta configurando.  

Per usare la nuova configurazione, definire le associazioni esplicite (collegamenti) da un gruppo di limiti a un altro. Configurare tutti i punti di distribuzione in tale gruppo associato con la stessa durata in minuti. Quando un client non riesce a trovare l'origine di un contenuto del relativo gruppo di limiti *corrente*, il tempo configurato determina quando può iniziare a cercare le origini del contenuto nel gruppo di limiti adiacente.

Oltre ai gruppi limite configurati in modo esplicito, ogni gruppo limite dispone di un collegamento implicito al gruppo limite del sito predefinito. Il collegamento diventa attivo dopo 120 minuti. Il gruppo di limiti del sito predefinito diventa quindi un gruppo di limiti adiacente. Questo comportamento consente ai client di usare come percorsi di origine del contenuto i punti di distribuzione associati a quel gruppo di limiti.

Questo comportamento sostituisce ciò che in precedenza veniva definito "fallback per il contenuto". Eseguire l'override di questo comportamento predefinito di 120 minuti associando in modo esplicito il gruppo di limiti del sito predefinito a un gruppo *corrente*. Impostare un periodo di tempo specifico in minuti o bloccare completamente il fallback per impedirne l'uso.


### <a name="clients-try-to-get-content-from-each-distribution-point-for-up-to-two-minutes"></a>I client provano a ottenere il contenuto da ogni punto di distribuzione per un massimo di due minuti

Quando un client cerca un percorso di origine del contenuto, prova ad accedere a ogni punto di distribuzione per due minuti prima di passare a un altro punto di distribuzione. Questo comportamento è diverso rispetto alle versioni precedenti in cui i client provavano a connettersi a un punto di distribuzione per un massimo di due ore.

- I client selezionano casualmente il primo punto di distribuzione dal pool dei server disponibili nel gruppo (o nei gruppi) di limiti *corrente* del client.  

- Dopo due minuti, se il client non ha trovato il contenuto, passa a un nuovo punto di distribuzione e prova a ottenere il contenuto da tale server. Questo processo viene ripetuto ogni due minuti fino a quando il client trova il contenuto o raggiunge l'ultimo server del pool.  

- Se un client non trova un percorso di origine del contenuto valido nel pool *corrente* prima di raggiungere l'intervallo di fallback in un gruppo di limiti *adiacente*, il client aggiunge i punti di distribuzione del gruppo *adiacente* alla fine dell'elenco corrente. Quindi cerca nel gruppo espanso di percorsi di origine che include i punti di distribuzione di entrambi i gruppi di limiti.  

    > [!TIP]  
    > Quando si crea un collegamento esplicito tra il gruppo di limiti corrente e il gruppo di limiti del sito predefinito e si definisce un intervallo di fallback inferiore al tempo di fallback per il collegamento a un gruppo di limiti adiacente, i client iniziano la ricerca dei percorsi di origine dal gruppo di limiti del sito predefinito prima di includere il gruppo adiacente.  

- Quando il client non riesce a ottenere il contenuto dall'ultimo server nel pool, avvia nuovamente il processo.  



## <a name="procedures-for-boundary-groups"></a>Procedure per i gruppi di limiti


### <a name="bkmk_create"></a> Creare un gruppo di limiti  

1.  Nella console di Configuration Manager accedere all'area di lavoro **Amministrazione**, espandere **Configurazione della gerarchia** e selezionare il nodo **Gruppi limite**.  

2.  Nella scheda **Home** selezionare **Crea gruppo limite** nel gruppo **Crea**.  

3.  Nella finestra di dialogo **Crea gruppo limite**, nella scheda **Generale**, specificare un valore in **Nome** per il gruppo di limiti. Facoltativamente, compilare il campo **Descrizione**.  

4.  Selezionare **OK** per salvare il nuovo gruppo di limiti o passare alla sezione successiva per configurare il gruppo di limiti.  


### <a name="bkmk_config"></a> Configurare un gruppo di limiti  

1.  Nella console di Configuration Manager accedere all'area di lavoro **Amministrazione**, espandere **Configurazione della gerarchia** e selezionare il nodo **Gruppi limite**.  

2.  Selezionare il gruppo di limiti da modificare e quindi selezionare **Proprietà** sulla barra multifunzione. Verrà aperta la finestra delle proprietà del gruppo di limiti.  

Configurare le seguenti impostazioni:  
- [Aggiungere o rimuovere limiti](#bkmk_add)  
- [Configurare l'assegnazione sito e selezionare i server del sistema del sito](#bkmk_references)  
- [Configurare il comportamento di fallback](#bkmk_bg-fallback)  
- [Configurare le opzioni del gruppo di limiti](#bkmk_options)  

#### <a name="bkmk_add"></a> Aggiungere o rimuovere limiti

Nella finestra di dialogo delle proprietà del gruppo di limiti usare la scheda **Generale** per modificare i limiti che fanno parte del gruppo:  

- Per aggiungere limiti, selezionare **Aggiungi**. Nella finestra Aggiungi limiti selezionare la casella di controllo per uno o più limiti e quindi selezionare **OK**.  

- Per rimuovere i limiti, selezionare il limite nell'elenco e quindi selezionare **Rimuovi**.  


#### <a name="bkmk_references"></a> Configurare l'assegnazione sito e selezionare i server del sistema del sito

Per modificare l'assegnazione sito e la configurazione del server del sistema del sito associata, passare alla scheda **Riferimenti** nella finestra delle proprietà del gruppo di limiti.  

- Per abilitare questo gruppo di limiti per l'uso da parte dei client per l'assegnazione sito, selezionare **Utilizza questo gruppo limite per l'assegnazione sito**. Selezionare quindi un sito dall'elenco a discesa **Sito assegnato**. Per altre informazioni, vedere [Assegnazione sito](#site-assignment).  

- Per associare i server del sistema del sito disponibili al gruppo di limiti, selezionare **Aggiungi**. Nella finestra Aggiungi sistemi del sito sono elencati solo i server con ruoli del sistema del sito supportati. Selezionare la casella di controllo per uno o più server e quindi fare clic su **OK**. I server vengono aggiunti come server del sistema del sito associati per il gruppo di limiti.  

    > [!NOTE]  
    >  È possibile selezionare qualsiasi combinazione dei sistemi del sito disponibili da qualsiasi sito della gerarchia. I sistemi del sito selezionati sono elencati nella scheda **Sistemi del sito** nelle proprietà di ogni limite appartenente al gruppo di limiti.  

- Per rimuovere un server dal gruppo di limiti, selezionare il server e quindi selezionare **Rimuovi**.  

    > [!NOTE]  
    >  Per interrompere l'uso di questo gruppo di limiti per i sistemi del sito in fase di associazione, rimuovere tutti i server elencati come server del sistema del sito associati.  


#### <a name="bkmk_bg-fallback"></a> Configurare il comportamento di fallback

Per configurare il comportamento di fallback, passare alla scheda **Relazioni** nella finestra delle proprietà del gruppo di limiti.  

- Per creare una relazione con un altro gruppo di limiti:  

    - Selezionare **Aggiungi**. Nella finestra Gruppi di limiti di fallback selezionare il gruppo di limiti da configurare.  

    - Impostare il tempo di fallback per i ruoli del sistema del sito seguenti:  
        - Punto di distribuzione  
        - Punto di aggiornamento software  
        - Punto di gestione  

        > [!Note]  
        > Ad esempio, aprire la finestra delle proprietà per il gruppo di limiti di una succursale. Nella finestra Gruppi di limiti di fallback selezionare il gruppo di limiti della sede centrale. Impostare il tempo di fallback per i punti di distribuzione su `20`. Quando si salva questa configurazione, i client nel gruppo di limiti della succursale inizieranno a cercare il contenuto nei punti di distribuzione nel gruppo di limiti della sede centrale dopo 20 minuti.  

    - Per impedire il fallback a un gruppo di limiti specifico, selezionare il gruppo di limiti e quindi selezionare **Non eseguire mai il fallback** per il tipo di ruolo del sistema del sito. Questa operazione può includere il *gruppo di limiti del sito predefinito*.  

- Per modificare la configurazione di una relazione esistente, selezionare il gruppo di limiti nell'elenco e quindi selezionare **Cambia**. Questa operazione apre la finestra Gruppi di limiti di fallback solo per il gruppo di limiti specifico.  
 
- Per rimuovere una relazione, selezionare il gruppo di limiti nell'elenco e quindi selezionare **Rimuovi**.  

Per altre informazioni, vedere [Fallback](#fallback). 


#### <a name="bkmk_options"></a> Configurare le opzioni del gruppo di limiti
<!--1356193--> A partire dalla versione 1806, per configurare opzioni aggiuntive per i client in questo gruppo di limiti, passare alla scheda **Opzioni**. Per altre informazioni, vedere [Opzioni del gruppo di limiti per download peer](#bkmk_bgoptions).

- **Consenti i download peer in questo gruppo di limiti**: questa opzione è abilitata per impostazione predefinita. Il punto di gestione fornisce ai client un elenco di posizioni del contenuto che include le origini peer.  

    - **Durante i download peer, usa solo i peer entro la stessa subnet**: questa impostazione dipende da quella sopra indicata. Se si abilita questa opzione, il punto di gestione include nell'elenco delle posizioni del contenuto solo le origini peer incluse nella stessa subnet del client.  


### <a name="bkmk_site-fallback"></a> Configurare un sito di fallback per l'assegnazione sito automatica  

Se i client non si trovano in un gruppo di limiti con un sito assegnato, assegnarli al sito durante l'installazione.

1.  Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**.  

2.  Nella scheda **Home** della barra multifunzione selezionare **Impostazioni gerarchia** nel gruppo **Siti**.  

3.  Nella scheda **Generale** selezionare la casella di controllo **Utilizza sito di fallback**. Selezionare quindi un sito nell'elenco a discesa **Sito di fallback**.  

4.  Selezionare **OK** per salvare la configurazione.  

Per altre informazioni, vedere [Assegnazione sito](#site-assignment).


### <a name="bkmk_proc-prefer"></a> Abilitare l'uso dei punti di gestione preferiti  

Per altre informazioni, vedere [Punti di gestione preferiti](#bkmk_preferred).

1.  Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**.  

2. Nella scheda **Home** della barra multifunzione selezionare **Impostazioni gerarchia** nel gruppo **Siti**.  

3. Nella scheda **Generale** selezionare **I client preferiscono usare i punti di gestione specificati nei gruppi di limiti**.  

4. Selezionare **OK** per salvare la configurazione.  

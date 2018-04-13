---
title: Configurare gruppi di limiti
titleSuffix: Configuration Manager
description: Aiutare i client a trovare i sistemi del sito usando i gruppi di limiti per organizzare logicamente i percorsi di rete correlati chiamati limiti
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
caps.latest.revision: 10
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 297f4a5ecb7650a4ea643fff00dd67b6580256de
ms.sourcegitcommit: 11bf4ed40ed0cbb10500cc58bbecbd23c92bfe20
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/23/2018
---
# <a name="configure-boundary-groups-for-system-center-configuration-manager"></a>Configurare gruppi di limiti per System Center Configuration Manager


*Si applica a: System Center Configuration Manager (Current Branch)*

Usare i gruppi di limiti in Configuration Manager per organizzare logicamente i percorsi di rete correlati ([limiti](/sccm/core/servers/deploy/configure/boundaries)) e semplificare la gestione dell'infrastruttura. Prima di usare il gruppo di limiti, assegnare i limiti ai gruppi di limiti.

Per impostazione predefinita, Configuration Manager crea un gruppo di limiti predefinito in ogni sito.

Per configurare i gruppi di limiti, associare i limiti (percorsi di rete) e i ruoli del sistema del sito, come i punti di distribuzione, al gruppo di limiti. Questa configurazione consente di associare i client ai server del sistema del sito, come i punti di distribuzione, che si trovano vicino ai client nella rete.

Per aumentare la disponibilità dei server del sistema del sito, ad esempio i punti di distribuzione, a una gamma più ampia di percorsi di rete, assegnare lo stesso limite e lo stesso server a più gruppi di limiti.

I client usano un gruppo di limiti per gli scopi seguenti:  

-   Assegnazione automatica al sito  
-   Ricerca di un server del sistema del sito che può fornire un servizio, tra cui:
    - Punti di distribuzione per il percorso del contenuto
    -   Punti di aggiornamento software
    - Punti di migrazione dello stato
    - Punti di gestione preferiti. Se si usano i punti di gestione preferiti, è necessario abilitare questa opzione per la gerarchia e non dalla configurazione del gruppo di limiti. Vedere [Per abilitare l'uso dei punti di gestione preferiti](#to-enable-use-of-preferred-management-points) in questo argomento.

##  <a name="boundary-groups-and-relationships"></a>Gruppi di limiti e relazioni
Per ogni gruppo di limiti nella gerarchia, è possibile assegnare:

-  Uno o più limiti. Il gruppo di limiti **corrente** di un client è un percorso di rete definito come limite assegnato a un gruppo di limiti specifico. Un client può avere più di un gruppo di limiti corrente.
- Uno o più ruoli del sistema del sito. I client possono usare sempre i ruoli del sistema del sito associati al gruppo di limiti corrente. A seconda delle configurazioni aggiuntive, possono essere in grado di usare i ruoli del sistema del sito in gruppi di limiti aggiuntivi.  

Per ogni gruppo di limiti creato, è possibile configurare un collegamento unidirezionale a un altro gruppo di limiti. Il collegamento è definito **relazione**. I gruppi di limiti con cui si stabilisce il collegamento sono chiamati gruppi di limiti **adiacenti**. Un gruppo di limiti può avere più relazioni, ciascuna con uno specifico gruppo di limiti adiacente.

Se un client non riesce a trovare un server del sistema del sito disponibile nel gruppo di limiti corrente, la configurazione di ogni relazione determina quando iniziare a cercare in un gruppo di limiti adiacente. Questa ricerca in altri gruppi è definita **fallback**.

## <a name="fallback"></a>Fallback
Per evitare problemi quando i client non riescono a trovare un sistema del sito disponibile nel gruppo di limiti corrente, definire la relazione tra i gruppi di limiti per il comportamento di fallback. Il fallback consente a un client di espandere la ricerca di un sistema del sito disponibile a gruppi di limiti aggiuntivi.

Le relazioni vengono configurate in una scheda **Relazioni** delle proprietà del gruppo di limiti. Quando si configura una relazione, si definisce un collegamento a un gruppo di limiti adiacente. Per ogni tipo di ruolo del sistema del sito supportato, configurare impostazioni indipendenti per il fallback a tale gruppo di limiti adiacente. Ad esempio, quando si configura una relazione con un gruppo di limiti specifico, impostare il fallback per i punti di distribuzione dopo 20 minuti anziché dopo l'intervallo predefinito di 120 minuti. Per un esempio più esteso, vedere [Esempio d'uso dei gruppi di limiti](#example-of-using-boundary-groups).

Se un client non riesce a trovare un ruolo del sistema del sito disponibile nel gruppo di limiti corrente, il client usa il tempo di fallback in minuti. Tale tempo di fallback determina quando il client inizia a eseguire la ricerca di un sistema del sito disponibile associato al gruppo di limiti adiacente.  

Se un client non riesce a trovare un sistema del sito disponibile e inizia la ricerca dei percorsi nei gruppi di limiti adiacenti, aumenta il pool dei sistemi del sito disponibili. La configurazione dei gruppi di limiti e delle relative relazioni definisce l'uso del client di questo pool di sistemi del sito disponibili.

- Un gruppo di limiti può avere più di una relazione. Con più relazioni è possibile configurare il fallback per ogni tipo di sistema del sito a diversi gruppi adiacenti dopo diversi intervalli di tempo.    
- I client eseguono il fallback a un gruppo di limiti solo se è direttamente adiacente al gruppo di limiti corrente.
- Se un client fa parte di più gruppi di limiti, il gruppo di limiti corrente è definito come un'unione di tutti i gruppi di limiti del client. Il client esegue il fallback ai gruppi adiacenti di uno dei gruppi di limiti originali.

### <a name="the-default-site-boundary-group"></a>Gruppo di limiti predefinito del sito
Oltre ai gruppi di limiti che è possibile creare, ogni sito dispone di un gruppo di limiti predefinito creato da Configuration Manager. Questo gruppo è denominato ***Default-Site-Boundary-Group&lt;codicesito>***. Ad esempio, il gruppo per il sito ABC è denominato *Default-Site-Boundary-Group&lt;ABC>*.

Per ogni gruppo di limiti creato, Configuration Manager crea automaticamente un collegamento implicito a ogni gruppo di limiti predefinito del sito nella gerarchia.
-   Il collegamento implicito è un'opzione di fallback predefinita da un gruppo di limiti corrente al gruppo di limiti predefinito del sito che ha un intervallo di fallback predefinito di 120 minuti.
-   Per i client che non si trovano in un limite associato a un gruppo di limiti: per identificare i ruoli del sistema del sito validi, usare il gruppo di limiti predefinito dal sito assegnato.

Per gestire il fallback al gruppo di limiti predefinito del sito:
- Aprire le proprietà del gruppo di limiti predefinito del sito e modificare i valori nella scheda **Comportamento predefinito**. Le modifiche apportate in questa scheda si applicano a *tutti* i collegamenti impliciti a questo gruppo di limiti. Queste impostazioni possono essere sostituite quando si configura il collegamento esplicito a questo gruppo di limiti predefinito del sito da un altro gruppo di limiti.
- Aprire le proprietà di un gruppo di limiti personalizzato. Modificare i valori per il collegamento esplicito a un gruppo di limiti predefinito del sito. Quando si imposta un nuovo intervallo in minuti per il fallback o il blocco del fallback, questa modifica influisce solo sul collegamento che si sta configurando. La configurazione del collegamento esplicito sostituisce quella della scheda **Comportamento predefinito** di un gruppo di limiti predefinito del sito.


## <a name="site-assignment"></a>Assegnazione sito  
 È possibile configurare ciascun gruppo di limiti con un sito assegnato per i client.  

-   Un client appena installato che usa l'assegnazione automatica sito viene aggiunto al sito assegnato di un gruppo di limiti che contiene il percorso di rete corrente del client.  
-   Dopo l'assegnazione a un sito, il client non modificherà la propria assegnazione del sito quando cambia il percorso di rete. Se il client ad esempio effettua il roaming a un nuovo percorso di rete rappresentato da un limite in un gruppo di limiti con un'assegnazione sito diversa, il sito assegnato a tale client non viene modificato.  
-   Quando l'individuazione sistema Active Directory rileva una nuova risorsa, le informazioni sulla rete per la risorsa individuata vengono valutate in rapporto ai limiti nei gruppi di limiti. Tramite questo processo la nuova risorsa viene associata a un sito assegnato per poter essere utilizzata dal metodo di installazione push client.  
-   Quando un limite è membro di più gruppi con diversi siti assegnati, i client selezionano uno dei siti in modo casuale.  
-   Le modifiche a un sito assegnato dei gruppi di limiti si applicano solo alle nuove azioni di assegnazione del sito. I client assegnati precedentemente a un sito non valutano di nuovo l'assegnazione del sito in base alle modifiche alla configurazione di un gruppo di limiti (o al proprio percorso di rete).  

Per altre informazioni sull'assegnazione dei siti per i client, vedere [Utilizzo dell'assegnazione automatica del sito per i computer](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) in [Come assegnare i client a un sito in System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

## <a name="distribution-points"></a>Punti di distribuzione

Quando un client richiede il percorso di un punto di distribuzione, Configuration Manager invia al client un elenco dei sistemi del sito. Questi sistemi del sito sono del tipo appropriato associato a ogni gruppo di limiti che include il percorso di rete corrente del client:

-   **Durante la distribuzione del software**, i client richiedono un percorso per il contenuto di distribuzione disponibile a un punto di distribuzione o a un'altra origine di contenuto valida, ad esempio un client configurato per Peer cache.

-   **Durante la distribuzione del sistema operativo** i client richiedono un percorso per l'invio o la ricezione delle informazioni di migrazione dello stato.  

Quando viene distribuito il contenuto, se un client richiede un contenuto che non è disponibile da un'origine nel gruppo di limiti corrente, il client continua a richiedere quel contenuto. Il client prova diverse origini del contenuto nel gruppo di limiti corrente finché non raggiunge il periodo di fallback per un gruppo di limiti adiacente o per il gruppo di limiti del sito predefinito. Se il client non ha ancora trovato il contenuto, estende la ricerca alle origini di contenuto in modo da includere i gruppi di limiti adiacenti.

Se il contenuto viene distribuito su richiesta e non è disponibile quando richiesto in un punto di distribuzione, viene avviato il processo di trasferimento del contenuto a quel punto di distribuzione. È possibile che il client rilevi il server come origine del contenuto prima di eseguire il fallback per l'uso di un gruppo di limiti adiacente.

## <a name="software-update-points"></a>Punti di aggiornamento software
I client usano i gruppi di limiti per trovare un nuovo punto di aggiornamento software. Per controllare quali server possono essere trovati da un client, aggiungere singoli punti di aggiornamento software a diversi gruppi di limiti.

Se si esegue l'aggiornamento da una versione precedente alla 1702, ogni sito aggiunge tutti i punti di aggiornamento software esistenti al gruppo di limiti predefinito in ogni sito. Questo comportamento di aggiornamento del sito mantiene il comportamento del client precedente per selezionare un punto di aggiornamento software dal pool di server disponibili. Questo comportamento viene mantenuto finché non si sceglie di aggiungere singoli punti di aggiornamento software a gruppi di limiti diversi per un comportamento di selezione e fallback controllato.

Se si installa un nuovo sito, i punti di aggiornamento software non vengono aggiunti al gruppo di limiti del sito predefinito. Assegnare i punti di aggiornamento software a un gruppo di limiti in modo che i client possano trovarli e usarli.

### <a name="fallback-for-software-update-points"></a>Fallback per i punti di aggiornamento software
Il fallback per i punti di aggiornamento software è configurato come altri ruoli del sistema del sito, ma con le avvertenze seguenti:
- **I nuovi client usano i gruppi di limiti per selezionare i punti di aggiornamento software.** I nuovi client installati selezionano un punto di aggiornamento software tra i server associati ai gruppi di limiti configurati. Ciò sostituisce il comportamento precedente in cui i client selezionano un punto di aggiornamento software in maniera casuale da un elenco di server che condividono la foresta dei client.

- **I client continuano a usare l'ultimo punto di aggiornamento software valido fino a quando non eseguono il fallback per trovare un nuovo punto.** I client che hanno già un punto di aggiornamento software continuano a usarlo fino a quando non può essere raggiunto. Questo comportamento include l'uso continuativo di un punto di aggiornamento software non associato al gruppo di limiti corrente del client.

  L'uso continuativo di un punto di aggiornamento software esistente, anche quando il server non è incluso nel gruppo di limiti corrente del client, è intenzionale. Quando il punto di aggiornamento software viene modificato, il client sincronizza i dati con il nuovo server, il che determina un uso significativo della rete. Se tuti client i client passano contemporaneamente a un nuovo server, il ritardo nella transizione può evitare la saturazione della rete.

- **Un client prova sempre a raggiungere l'ultimo punto di aggiornamento software valido per 120 minuti prima di avviare il fallback.** Dopo 120 minuti, se il client non ha stabilito il contatto, inizia il fallback. Quando il fallback viene avviato, il client riceve un elenco di tutti i punti di aggiornamento software dal gruppo di limiti corrente. I punti di aggiornamento software aggiuntivi dai gruppi di limiti adiacenti e il gruppo di limiti predefinito sono disponibili in base alle configurazioni di fallback.

### <a name="fallback-configurations-for-software-update-points"></a>Configurazioni di fallback per i punti di aggiornamento software
#### <a name="beginning-with-version-1706"></a>A partire dalla versione 1706   
È possibile impostare **Orari di fallback (in minuti)** per i punti di aggiornamento software su meno di 120 minuti. Il client tenta comunque raggiungere il punto di aggiornamento software originale per 120 minuti. La ricerca viene quindi espansa su server aggiuntivi. I tempi di fallback del gruppo di limiti iniziano la prima volta in cui il client non riesce a raggiungere il server originale. Quando il client espande la ricerca, il sito specifica tutti i gruppi di limiti configurati per meno di 120 minuti.

Per bloccare il fallback per un punto di aggiornamento software a un gruppo di limiti adiacente, configurare l'impostazione su **Non eseguire mai il fallback**.

Dopo l'esito negativo nel raggiungere il server originale per due ore, il client usa quindi un ciclo più breve per stabilire una connessione a un nuovo punto di aggiornamento software. In questo modo il client può eseguire rapidamente una ricerca nell'elenco in espansione di potenziali punti di aggiornamento software.

 -  **Esempio di fallback:**  
    Il fallback per i punti di aggiornamento software di un gruppo di limiti corrente di un client è impostato su *10* minuti per il gruppo di limiti *A* e *130* minuti per il gruppo di limiti *B*. Quando il client non riesce a raggiungere l'ultimo punto di aggiornamento software valido:
    -   Il client prova a raggiungere solo il server originale nei successivi 120 minuti. Dopo 10 minuti, i punti di aggiornamento software dal gruppo di limiti A vengono aggiunti al pool di server disponibili. Il client può tuttavia provare a contattare questi o altri server solo dopo che è trascorso il periodo iniziale di 120 minuti per riconnettersi al server originale.
    -   Dopo avere provato a individuare tale punto di aggiornamento software per 120 minuti, il client può espandere la ricerca. A quel punto, il client aggiunge i server al pool disponibile di punti di aggiornamento software che si trovano nel gruppo di limiti corrente del client e in eventuali gruppi di limiti adiacenti impostati su 120 minuti o meno. In questo pool sono inclusi i server nel gruppo di limiti A aggiunti prima al pool di server disponibili.
    -       Dopo altri 10 minuti (130 minuti in totale dopo il primo tentativo non riuscito del client di raggiungere l'ultimo punto di aggiornamento software noto), il client espande la ricerca per includere i punti di aggiornamento software dal gruppo di limiti B.  

#### <a name="prior-to-version-1706"></a>Prima della versione 1706
Prima della versione 1706, le configurazioni di fallback per i punti di aggiornamento software non supportano un orario configurabile in minuti. Il comportamento di fallback è limitato a:

  - **Orari di fallback (in minuti):** questa opzione è disabilitata per i punti di aggiornamento software e non può essere configurata. È impostata su 120 minuti.
  -     **Non eseguire mai il fallback**: quando si usa questa configurazione, è possibile bloccare il fallback per un punto di aggiornamento software a un gruppo di limiti adiacente.

Quando un client che ha già un punto di aggiornamento software non riesce a raggiungerlo, esegue il fallback per trovarne un altro. Quando usa il fallback, il client riceve un elenco di tutti i punti di aggiornamento software dal gruppo di limiti corrente. Se non riesce a trovare un server disponibile per 120 minuti, esegue il fallback ai gruppi di limiti adiacenti e al gruppo di limiti predefinito del sito. Il fallback a entrambi i gruppi di limiti avviene nello stesso momento. Il tempo di fallback del punto di aggiornamento software ai gruppi di limiti adiacenti è impostato su 120 minuti. Non è possibile modificare questo tempo di fallback. L'intervallo di 120 minuti è anche il periodo predefinito usato per il fallback al gruppo di limiti predefinito del sito. Quando un client esegue il fallback a un gruppo di limiti adiacente e al gruppo di limiti predefinito del sito, prova a contattare i punti di aggiornamento software del gruppo di limiti adiacente prima di provare a usare uno di quelli del gruppo di limiti predefinito del sito.

### <a name="manually-switch-to-a-new-software-update-point"></a>Passare manualmente a un nuovo punto di aggiornamento software
Oltre a usare il fallback, è possibile usare *Notifica client* per forzare manualmente il passaggio di un dispositivo a un nuovo punto di aggiornamento software.

Quando si passa a un nuovo server, i dispositivi usano il fallback per trovare il nuovo server. Esaminare le configurazioni del gruppo di limiti. Verificare che i punti di aggiornamento software siano nei gruppi di limiti corretti prima di avviare questa modifica.

Per altre informazioni, vedere [Passaggio manuale dei client a un nuovo punto di aggiornamento software](/sccm/sum/plan-design/plan-for-software-updates#manually-switch-clients-to-a-new-software-update-point).



## <a name="management-points"></a>Punti di gestione
<!-- 1324594 -->
A partire dalla versione 1802, è possibile configurare relazioni di fallback per i punti di gestione tra gruppi di limiti. Questo comportamento consente un maggiore controllo per i punti di gestione usati dai client. Nella scheda **Relazioni** delle proprietà del gruppo di limiti è presente una colonna per il punto di gestione. Quando si aggiunge un nuovo gruppo di limiti di fallback, attualmente il tempo di fallback per il punto di gestione è sempre zero (0). Questo comportamento corrisponde all'opzione **Comportamento predefinito** del gruppo di limiti predefinito del sito.

Nelle versioni precedenti si verifica comunemente un problema in presenza di un punto di gestione protetto in una rete protetta. I client nella rete aziendale principale ricevono criteri che includono questo punto di gestione protetto, anche se non possono comunicare con esso attraverso un firewall. Per risolvere il problema, usare l'opzione **Non eseguire mai il fallback** per fare in modo che i client eseguano il fallback solo ai punti di gestione con cui possono comunicare.

Quando si aggiorna il sito alla versione 1802, Configuration Manager aggiunge tutti i punti di gestione senza connessione Internet nel gruppo di limiti predefinito del sito. Questo comportamento dell'aggiornamento assicura che le versioni client precedenti continuino a comunicare con i punti di gestione. Per sfruttare tutti i vantaggi di questa funzionalità, spostare i punti di gestione nei gruppi di limiti desiderati.

Il comportamento del fallback dei gruppi di limiti dei punti di gestione non cambia durante l'installazione dei client (ccmsetup.exe). Se la riga di comando non specifica il punto di gestione iniziale tramite il parametro /MP, il nuovo client riceve l'elenco completo dei punti di gestione disponibili. Per il processo di avvio iniziale, il client usa il primo punto di gestione a cui può accedere. Una volta registratosi con il sito, il client riceve l'elenco dei punti di gestione correttamente ordinato con questo nuovo comportamento. 

Per consentire ai client di usare questa funzionalità, abilitare l'impostazione seguente: **I client preferiscono usare i punti di gestione specificati nei gruppi di limiti** in **Impostazioni gerarchia**. 

> [!Note]
> I processi di distribuzione dei sistemi operativi non sono a conoscenza dei gruppi di limiti.

### <a name="troubleshooting"></a>Troubleshooting
Nel log **LocationServices.log** sono presenti nuove voci. L'attributo **Locality** identifica uno degli stati seguenti:
- 0: Sconosciuto
- 1: il punto di gestione specificato si trova solo nel gruppo di limiti predefinito del sito per il fallback
- 2: il punto di gestione specificato si trova in un gruppo di limiti remoto o vicino. Quando il punto di gestione si trova sia in un gruppo di limiti vicino sia in quello predefinito del sito, l'attributo locality è uguale a 2.
- 3: il punto di gestione specificato si trova nel gruppo di limiti locale o corrente. Quando il punto di gestione si trova sia nel gruppo di limiti corrente e in uno vicino o in quello predefinito del sito, l'attributo locality è uguale a 3. Se non si abilita l'impostazione dei punti di gestione preferiti in Impostazioni gerarchia, l'attributo locality è sempre uguale a 3 indipendentemente dal gruppo di limiti in cui si trova il punto di gestione.

I client usano prima i punti di gestione locali (locality 3), quindi quelli remoti (locality 2) e infine eseguono il fallback (locality 1). 

Quando un client riceve cinque errori in 10 minuti e non riesce a comunicare con un punto di gestione nel relativo gruppo di limiti corrente, cerca di contattare un punto di gestione in un gruppo di limiti adiacente o in quello predefinito del sito. Se in seguito il punto di gestione nel gruppo di limiti corrente torna online, il client torna al punto di gestione locale al successivo ciclo di aggiornamento. Il ciclo di aggiornamento avviene ogni 24 ore o al riavvio del servizio agente di Configuration Manager.




## <a name="preferred-management-points"></a>Punti di gestione preferiti

 > [!Note]
 > Il comportamento dell'impostazione gerarchia, **I client preferiscono usare i punti di gestione specificati nei gruppi di limiti** cambia a partire dalla versione 1802. Quando si abilita questa impostazione, Configuration Manager usa la funzionalità del gruppo di limiti per il punto di gestione assegnato. Per altre informazioni, vedere [Punti di gestione](#management-points). 

 I punti di gestione preferiti consentono a un client di identificare un punto di gestione associato al percorso di rete corrente (limite).  

-   Il client prova a usare un punto di gestione preferito dal sito assegnato prima di usarne uno non configurato come preferito dal sito assegnato.  
-   Per usare questa opzione, abilitare **I client preferiscono usare i punti di gestione specificati nei gruppi di limiti** in **Impostazioni gerarchia**. Configurare quindi i gruppi di limiti nei singoli siti primari. Includere i punti di gestione che devono essere associati ai limiti associati del gruppo di limiti.
-   Quando si configurano i punti di gestione preferiti e un client organizza l'elenco dei punti di gestione, il client inserisce i punti di gestione preferiti all'inizio del relativo elenco. Questo elenco include tutti i punti di gestione dal sito assegnato del client.  

> [!NOTE]  
>  Il roaming del client si ha quando vengono modificati i percorsi di rete, ad esempio quando un computer portatile viene spostato in un ufficio remoto. Quando un client esegue il roaming è possibile che usi un punto di gestione o un punto di gestione del proxy dal sito locale nel nuovo percorso prima di tentare di usare un server dal sito assegnato. Questo elenco di server dal sito assegnato include i punti di gestione preferiti. Per altre informazioni, vedere [Informazioni su come i client trovano i servizi e le risorse del sito](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="overlapping-boundaries"></a>Limiti sovrapposti  
 Configuration Manager supporta le configurazioni con sovrapposizione dei limiti per il percorso del contenuto. Quando il percorso di rete client appartiene a più gruppi di limiti:

-   Quando un client richiede il contenuto, Configuration Manager invia al client un elenco di tutti i punti di distribuzione che hanno contenuto.  
-   Quando un client richiede a un server di inviare o ricevere le informazioni di migrazione dello stato, Configuration Manager invia al client un elenco di tutti i punti di migrazione dello stato associati a un gruppo di limiti che include il percorso di rete corrente del client.  

Questo comportamento consente al client di selezionare il server più vicino da cui trasferire le informazioni di migrazione dello stato o sul contenuto.  



## <a name="example-of-using-boundary-groups"></a>Esempio d'uso dei gruppi di limiti
L'esempio seguente usa un client che esegue la ricerca di contenuto da un punto di distribuzione. Questo esempio può essere applicato ad altri ruoli del sistema del sito che usano i gruppi di limiti. Tenere tuttavia presente che i punti di aggiornamento software non supportano la configurazione di un intervallo in minuti per il fallback a un gruppo adiacente e usano sempre un periodo di 120 minuti.

Creare tre gruppi limite che non condividono limiti o server del sistema del sito:
-   Gruppo BG_A con punti di distribuzione DP_A1 e DP_A2 associati al gruppo
-   Gruppo BG_B con punti di distribuzione DP_B1 e DP_B2 associati al gruppo
-   Gruppo BG_C con punti di distribuzione DP_C1 e DP_C2 associati al gruppo

Aggiungere i percorsi di rete dei client come limiti solo al gruppo di limiti BG_A. Configurare quindi le relazioni da tale gruppo di limiti per gli altri due gruppi di limiti:
-   Configurare i punti di distribuzione per il primo gruppo *adiacente* (BG_B) da usare dopo 10 minuti. Questo gruppo contiene i punti di distribuzione DP_B1 e DP_B2. Entrambi sono ben connessi ai percorsi limite dei primi gruppi.
-   Configurare il secondo gruppo *adiacente* (BG_C) da usare dopo 20 minuti. Questo gruppo contiene i punti di distribuzione DP_C1 e DP_C2. Entrambi si trovano a un WAN rispetto agli altri due gruppi limite.
-   Aggiungere anche al gruppo di limiti del sito predefinito un punto di distribuzione aggiuntivo che si trova nel server del sito. Questo server è la posizione di origine di contenuto meno preferita, ma si trova a livello centrale per tutti i gruppi limite.

    Esempio di gruppi limite e tempi di fallback:

     ![Esempio di gruppi di limiti e tempi di fallback](media/BG_Fallback.png)


Con questa configurazione:
-   Il client inizia la ricerca di contenuto dai punti di distribuzione nel gruppo di limiti *corrente* (BG_A). Cerca ogni punto di distribuzione per due minuti e quindi passa al punto di distribuzione successivo nel gruppo di limiti. Il pool di client dei percorsi di origine del contenuto validi include DP_A1 e DP_A2.
-   Se il client non riesce a trovare il contenuto nel proprio gruppo limite *corrente* dopo 10 minuti di ricerca, aggiunge i punti di distribuzione dal gruppo limite BG_B alla ricerca. Prosegue quindi la ricerca di contenuto da un punto di distribuzione nel relativo pool combinato di server. Questo pool include ora i server dei gruppi di limiti BG_A e BG_B. Il client continua a contattare ogni punto di distribuzione per due minuti prima di passare al server successivo del pool. Il pool di client dei percorsi di origine del contenuto validi include DP_A1, DP_A2, DP_B1 e DP_B2.
-   Dopo altri 10 minuti (totale di 20 minuti), se il client non ha ancora rilevato un punto di distribuzione con contenuto, espande il proprio pool per includere i server del secondo gruppo *adiacente*, il gruppo di limiti BG_C. Il client ha ora sei punti di distribuzione per la ricerca (DP_A1 DP_A2, DP_B2, DP_B2, DP_C1 e DP_C2). Continua la modifica in un nuovo punto di distribuzione ogni due minuti finché non trova il contenuto.
-   Se il client non ha rilevato il contenuto dopo un totale di 120 minuti, esegue il fallback per includere il *gruppo limite del sito predefinito* nella ricerca. Il pool include ora tutti i punti di distribuzione dei tre gruppi di limiti configurati e il punto di distribuzione finale presente nel server del sito. Il client continua quindi la ricerca del contenuto, modificando i punti di distribuzione ogni due minuti fino a quando il contenuto non viene trovato.

Configurando i diversi gruppi adiacenti in modo da renderli disponibili in momenti diversi, è possibile controllare quando i punti di distribuzione specifici vengono aggiunti come percorso di origine del contenuto. Il client usa il fallback al gruppo di limiti del sito predefinito come rete di protezione per il contenuto che non è disponibile da qualsiasi altra posizione.





<!--
### Update existing boundary groups to the new model
When you update to version prior to 1610, the following configurations are automatically made. This behavior ensures your current fallback behavior remains available until you configure new boundary groups and relationships.

-   Each primary site creates a default site boundary group named ***Default-Site-Boundary-Group&lt;sitecode>***.
  - The primary site adds to the *Default-Site-Boundary-Group&lt;sitecode>* boundary group any state migration points and distribution points configured to **Allow fallback source location for content**.
  - The site adds software update points to the *Default-Site-Boundary-Group&lt;sitecode>* boundary group.
-   The site makes a copy of each existing boundary group that includes a site server configured with a slow connection. The name of the new group is ***&lt;original boundary group name>-&lt;original boundary group ID>***:  
    -   Site systems that have a fast connection are left in the original boundary group.
    -   A copy of site systems (distribution points, management points) that have a slow connection are added to the copy of the boundary group. The original site systems configured as slow remain in their original boundary groups for backward compatibility, but are not used from those boundary groups.
    - This boundary group copy does not have boundaries associated with it. However, A fallback link is created between the original group and the new boundary group copy that has the fallback time set to zero.  


- **Specific to secondary sites:**
  - If a secondary site has at least one state migration point or distribution point enabled to **Allow fallback source location for content**, Configuration Manager creates a boundary group named ***Secondary-Site-Neighbor--Tmp&lt;Sitecode>***. 
  - All distribution points enabled to **Allow fallback source location for content** and state migration points are added to this secondary site boundary group.
  - A fallback link is created between the original boundary group and the newly created neighbor boundary group. The fallback time is set to zero.


 The following table identifies the new fallback behavior you can expect from the combination the original deployment settings and distribution point configurations:

Original deployment configuration for “Do not run program” in slow network  |Original distribution point configuration for “Allow client to use a fallback source location for content”  |New fallback behavior  
---------|---------|---------
Selected     |  Selected    |  **No fallback** - Only use the distribution points in current boundary group       
Selected     |  Not selected|  **No fallback** - Only use the distribution points in current boundary group       
Not selected |  Not selected|  **Fallback to neighbor** - Use the distribution points in current boundary group, and then add the distribution points from the neighbor boundary group. Unless an explicit link to the default site boundary group is configured, clients do not fallback to that group.    
Not selected | Selected     |   **Normal fallback** - Use distribution points in current boundary group, then servers from the neighbor and site default boundary groups

 All other deployment configurations result in **Normal fallback**.  
-->



## <a name="changes-from-prior-versions"></a>Modifiche rispetto alle versioni precedenti
Di seguito sono riportate le modifiche principali ai gruppi di limiti e alle modalità di ricerca del contenuto da parte dei client introdotte in Configuration Manager Current Branch. Molti di queste modifiche e concetti funzionano in combinazione.


-   Le configurazioni Veloce o Lento sono state rimosse: non è più possibile configurare la velocità o la lentezza dei singoli punti di distribuzione. Al contrario, ogni sistema del sito associato a un gruppo limite viene trattato ugualmente. Grazie a questa modifica, la scheda **Riferimenti** delle proprietà del gruppo limite non supporta la configurazione Veloce o Lento.
- Nuovo gruppo di limiti predefinito in ogni sito: ogni sito primario ha un nuovo gruppo di limiti predefinito denominato ***Default-Site-Boundary-Group&lt;codicesito>***. Quando un client non è presente in un percorso di rete assegnato a un gruppo di limiti, usa i sistemi del sito associati al gruppo predefinito del sito assegnato. Considerare l'uso di questo gruppo limite come sostituzione del concetto di percorso del contenuto di fallback.   
 -  L'opzione **Allow fallback source locations for content** (Consenti percorsi di origine di fallback per il contenuto) viene rimossa: la configurazione di un punto di distribuzione da usare per il fallback non avviene più in modo esplicito. Le opzioni per configurare questa impostazione vengono rimosse dalla console.

    Il risultato dell'impostazione **Allow fallback source locations for content** (Consenti percorsi di origine di fallback per il contenuto) in un tipo di distribuzione per le applicazioni cambia. Questa impostazione su un tipo di distribuzione consente ora al client di usare il gruppo limite del sito predefinito come percorso di origine del contenuto.

 -  Relazioni tra gruppi di limiti: ogni gruppo di limiti può essere collegato a uno o più gruppi di limiti aggiuntivi. Questi collegamenti costituiscono le relazioni configurate sulla nuova scheda delle proprietà del gruppo limite, denominata **Relationships** (Relazioni):
    -   Ogni gruppo limite associato direttamente a un client viene chiamato gruppo limite **corrente**.  
    -   Qualsiasi gruppo di limiti che un client può usare grazie all'associazione tra il gruppo di limiti *corrente* e un altro gruppo viene chiamato gruppo di limiti **adiacente**.
    -  Nella scheda **Relazioni** aggiungere gruppi di limiti da usare come gruppo di limiti *adiacente*. Configurare anche un tempo in minuti per il fallback. Nel momento in cui un client non riesce a trovare il contenuto da un punto di distribuzione nel gruppo *corrente* avvia la ricerca dei percorsi del contenuto nei gruppi di limiti *adiacenti*.

        Quando si aggiunge o si modifica una configurazione del gruppo di limiti, è possibile bloccare il fallback su tale gruppo di limiti dal gruppo corrente che si sta configurando.

    Per usare la nuova configurazione, definire le associazioni esplicite (collegamenti) da un gruppo di limiti a un altro. Configurare tutti i punti di distribuzione in tale gruppo associato con la stessa durata in minuti. Quando un client non riesce a trovare l'origine di un contenuto del relativo gruppo di limiti *corrente*, il tempo configurato determina quando può iniziare a cercare le origini del contenuto nel gruppo di limiti adiacente.

    Oltre ai gruppi limite configurati in modo esplicito, ogni gruppo limite dispone di un collegamento implicito al gruppo limite del sito predefinito. Il collegamento diventa attivo dopo 120 minuti. Il gruppo di limiti del sito predefinito diventa quindi un gruppo di limiti adiacente. Questo comportamento consente ai client di usare come percorsi di origine del contenuto i punti di distribuzione associati a quel gruppo di limiti.

    Questo comportamento sostituisce ciò che in precedenza veniva definito "fallback per il contenuto". Eseguire l'override di questo comportamento predefinito di 120 minuti associando in modo esplicito il gruppo di limiti del sito predefinito a un gruppo *corrente*. Impostare un periodo di tempo specifico in minuti o bloccare completamente il fallback per impedirne l'uso.


-   I client tentano di ottenere i contenuti da ogni punto di distribuzione per un massimo di due minuti: quando un client cerca un percorso di origine del contenuto, tenta di accedere a ogni punto di distribuzione per due minuti prima di passare a un altro punto di distribuzione. Questo comportamento costituisce una modifica rispetto alle versioni precedenti in cui i client tentavano di connettersi a un punto di distribuzione per un massimo di due ore.

    - I client selezionano casualmente il primo punto di distribuzione dal pool dei server disponibili nel gruppo (o nei gruppi) di limiti *corrente* del client.

    - Dopo due minuti, se il client non ha trovato il contenuto, passa a un nuovo punto di distribuzione e tenta di ottenere il contenuto da questo server. Questo processo viene ripetuto ogni due minuti fino a quando il client trova il contenuto o raggiunge l'ultimo server del pool.

    - Se un client non trova un percorso di origine del contenuto valido nel proprio pool *corrente* prima dell'intervallo di fallback verso un gruppo di limiti *adiacente*, il client aggiunge i punti di distribuzione dal gruppo *adiacente* alla fine dell'elenco corrente e quindi cerca nel gruppo espanso di percorsi di origine che include i punti di distribuzione di entrambi i gruppi di limiti.

        > [!TIP]  
        > Quando si crea un collegamento esplicito tra il gruppo di limiti corrente e il gruppo di limiti del sito predefinito e si definisce un intervallo di fallback inferiore al tempo di fallback per il collegamento a un gruppo di limiti adiacente, i client iniziano la ricerca dei percorsi di origine dal gruppo di limiti del sito predefinito prima di includere il gruppo adiacente.

    - Quando il client non riesce a ottenere il contenuto dall'ultimo server nel pool, avvia nuovamente il processo.


## <a name="procedures-for-boundary-groups"></a>Procedure per i gruppi di limiti

### <a name="to-create-a-boundary-group"></a>Per creare un gruppo di limiti  
1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia** >  **Gruppi di limiti**.  

2.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea gruppo di limiti**.  

3.  Nella finestra di dialogo **Crea gruppo limite** selezionare la scheda **Generale** e specificare un **Nome** per questo gruppo di limiti.  

4.  Fare clic su **OK** per salvare il nuovo gruppo di limiti.  


### <a name="to-configure-a-boundary-group"></a>Per configurare un gruppo di limiti  
 1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia** >  **Gruppi di limiti**.  

 2.  Selezionare il gruppo di limiti da modificare.  

 3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

 4.  Nella finestra di dialogo **Proprietà** per il gruppo di limiti selezionare la scheda **Generale** per modificare i limiti appartenenti a questo gruppo di limiti:  

     -   Per aggiungere i limiti, fare clic su **Aggiungi**, selezionare la casella di controllo per uno o più limiti e quindi fare clic su **OK**.  

     -   Per rimuovere i limiti, selezionare il limite e fare clic su **Rimuovi**.  

 5.  Selezionare la scheda **Riferimenti** per modificare l'assegnazione sito e la configurazione del server del sistema del sito associata:  

     -   Per abilitare questo gruppo di limiti per l'uso da parte dei client per l'assegnazione sito, selezionare **Utilizza questo gruppo limite per l'assegnazione sito**. Selezionare quindi un sito dall'elenco a discesa **Sito assegnato**.  

     -   Per configurare quali server del sistema del sito disponibili sono associati a questo gruppo di limiti:  

     1.  Fare clic su **Aggiungi**e quindi selezionare la casella di controllo per uno o più server. I server vengono aggiunti come server del sistema del sito associati per questo gruppo di limiti. Sono disponibili solo i server su cui è installato il ruolo del sistema del sito supportato.  

         > [!NOTE]  
         >  È possibile selezionare qualsiasi combinazione dei sistemi del sito disponibili da qualsiasi sito della gerarchia. I sistemi del sito selezionati vengono elencati nella scheda **Sistemi del sito** nelle proprietà di ogni limite appartenente a questo gruppo di limiti.  

     2.  Per rimuovere un server da questo gruppo di limiti, selezionare il server e quindi fare clic su **Rimuovi**.  

         > [!NOTE]  
         >  Per interrompere l'uso di questo gruppo di limiti per i sistemi del sito in fase di associazione, rimuovere tutti i server elencati come server del sistema del sito associati.  

 6.  Per configurare il comportamento di fallback, selezionare la scheda **Relazioni**:  

     - Fare clic su **Aggiungi** e quindi selezionare il gruppo di limiti da configurare.

     - Impostare un tempo di fallback per i punti di distribuzione. Dopo questo periodo i client del gruppo di limiti per il quale si stanno configurando relazioni saranno in grado di iniziare la ricerca di contenuto dai punti di distribuzione del gruppo di limiti che si sta aggiungendo.

     - Per evitare il fallback a un gruppo di limiti specifico, incluso il *gruppo di limiti predefinito del sito*, configurato per impostazione predefinita, selezionare il gruppo di limiti e quindi selezionare la casella **Non eseguire mai il fallback**.   

 7.  Fare clic su **OK** per chiudere le proprietà del gruppo di limiti e salvare la configurazione.  

#### <a name="to-associate-a-site-system-server-with-a-boundary-group"></a>Per associare un server del sistema del sito a un gruppo di limiti  
 1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia** >  **Gruppi di limiti**.  

 2.  Selezionare il gruppo di limiti da modificare.  

 3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

 4.  Nella finestra di dialogo **Proprietà** per il gruppo di limiti selezionare la scheda **Riferimenti** .  

 5.  In **Seleziona server del sistema del sito** fare clic su **Aggiungi**. Selezionare i server del sistema del sito da associare a questo gruppo di limiti e fare clic su **OK**.  

 6.  Fare clic su **OK** per chiudere le finestra di dialogo e salvare la configurazione del gruppo di limiti.  


#### <a name="to-configure-a-fallback-site-for-automatic-site-assignment"></a>Per configurare un sito di fallback per l'assegnazione sito automatica  

  1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione del sito** >  **Siti**.  

  2.  Nella scheda **Home** , del gruppo **Siti** , fare clic su **Impostazioni gerarchia**.  

  3.  Nella scheda **Generale** selezionare la casella di controllo **Utilizza sito di fallback**e quindi selezionare un sito dall'elenco a discesa **Sito di fallback** .  

  4.  Fare clic su **OK** per salvare la configurazione.  

#### <a name="to-enable-use-of-preferred-management-points"></a>Per abilitare l'uso dei punti di gestione preferiti  

 1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione del sito** > **Siti**, quindi nella scheda **Home** selezionare **Impostazioni gerarchia**.  

 2.  Nella scheda **Generale** di Impostazioni gerarchia selezionare **I client preferiscono usare i punti di gestione specificati nei gruppi di limiti**.  

 3.  Fare clic su **OK** per chiudere le finestra di dialogo e salvare la configurazione.  

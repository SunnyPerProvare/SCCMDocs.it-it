---
title: Definire gruppi di limiti | Microsoft Docs
description: Informazioni sui gruppi di limiti che collegano i client ai sistemi del sito in System Center Configuration Manager.
ms.custom: na
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 5db2926f-f03e-49c7-b44b-e89b1a5a6779
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
ms.translationtype: Human Translation
ms.sourcegitcommit: d940fd1bbf96767d44f8c55315e814be55a83897
ms.openlocfilehash: 5684fd4fbfd0ffb8f3ffbcfa122eef3dafd77327
ms.contentlocale: it-it
ms.lasthandoff: 05/08/2017


---
# <a name="configure-boundary-groups-for-system-center-configuration-manager"></a>Configurare gruppi di limiti per System Center Configuration Manager


*Si applica a: System Center Configuration Manager (Current Branch)*

I gruppi di limiti in System Center Configuration Manager vengono usati per raggruppare logicamente i percorsi di rete correlati ([limiti](/sccm/core/servers/deploy/configure/boundaries)) e semplificare la gestione dell'infrastruttura. Prima di usare un gruppo di limiti è necessario assegnare i limiti ai gruppi di limiti.

Per impostazione predefinita, Configuration Manager crea un gruppo di limiti predefinito in ogni sito.

> [!IMPORTANT]  
>  **Le informazioni contenute in questa sezione Gruppi di limiti e nelle sezioni figlio sono valide per la versione 1610 o versioni successive.** Questo contenuto è stato rivisto per descrivere in modo specifico le modifiche di progettazione relative ai gruppi di limiti introdotte con questa versione di aggiornamento.
>
> **Se si usano versioni precedenti la 1610**, vedere [Gruppi di limiti per System Center Configuration Manager versioni 1511, 1602 e 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) per informazioni su come usare e configurare i gruppi di limiti con tali versioni del prodotto.

Per configurare i gruppi di limiti, associare i limiti (percorsi di rete) e i ruoli del sistema del sito, come i punti di distribuzione, al gruppo di limiti. Ciò consente di associare i client ai server del sistema del sito, come i punti di distribuzione, che si trovano vicino ai client nella rete.

Quando si assegna lo stesso limite a più gruppi di limiti e si assegnano gli stessi server del sistema del sito, come i punti di distribuzione, a più gruppi di limiti, si aumenta la disponibilità dei sistemi del sito a una gamma più ampia di percorsi di rete.

I client usano un gruppo di limiti per gli scopi seguenti:  

-   Assegnazione automatica al sito  
-   Ricerca di un server del sistema del sito che può fornire un servizio, tra cui:
    - Punti di distribuzione per il percorso del contenuto
    -    Punti di aggiornamento software (a partire dalla versione 1702)
    - Punti di migrazione dello stato
    - Punti di gestione preferiti. Se si usano i punti di gestione preferiti, è necessario abilitare questa opzione per la gerarchia e non dalla configurazione del gruppo di limiti. Vedere [Per abilitare l'uso dei punti di gestione preferiti](#to-enable-use-of-preferred-management-points) in questo argomento.

##  <a name="boundary-groups-and-relationships"></a>Gruppi di limiti e relazioni
Per ogni gruppo di limiti nella gerarchia, è possibile assegnare:

-  Uno o più limiti. Quando un client si trova in un percorso di rete definito come limite assegnato a un gruppo di limiti specifico, questo viene chiamato gruppo di limiti **corrente**. Un client può avere più di un gruppo di limiti corrente.
- Uno o più ruoli del sistema del sito.  I client possono usare sempre i ruoli del sistema del sito associati al gruppo di limiti corrente. A seconda delle configurazioni aggiuntive, possono essere in grado di usare i ruoli del sistema del sito in gruppi di limiti aggiuntivi.  

Per ogni gruppo di limiti creato, è possibile configurare un collegamento unidirezionale a un altro gruppo di limiti. Il collegamento è definito **relazione**. I gruppi di limiti con cui si stabilisce il collegamento sono chiamati gruppi di limiti **adiacenti**. Un gruppo di limiti può avere più relazioni, ciascuna con uno specifico gruppo di limiti adiacente.

La configurazione di ogni relazione determina il momento in cui un client che non riesce a trovare un server del sistema del sito disponibile nel gruppo di limiti corrente può iniziare a cercare un sistema del sito disponibile in un gruppo di limiti adiacente. Questa ricerca in altri gruppi è definita **fallback**.

## <a name="fallback"></a>Fallback
Per evitare problemi per i client quando non riescono a trovare un sistema del sito disponibile nel gruppo di limiti corrente, si definiscono le relazioni tra i gruppi di limiti che specificano il comportamento di fallback. Il fallback consente a un client di espandere la ricerca di un sistema del sito disponibile a gruppi di limiti aggiuntivi.

Le relazioni vengono configurate in una scheda **Relazioni** delle proprietà del gruppo di limiti. Quando si configura una relazione, si definisce un collegamento a un gruppo di limiti adiacente. Per ogni tipo di ruolo del sistema del sito supportato, è possibile configurare impostazioni indipendenti per il fallback a tale gruppo di limiti adiacente. Ad esempio, quando si configura una relazione con un gruppo di limiti specifico, è possibile impostare il fallback per i punti di distribuzione dopo 20 minuti anziché dopo l'intervallo predefinito di 120 minuti. Per un esempio più esteso, vedere [Esempio d'uso dei gruppi di limiti](#example-of-using-boundary-groups).

Se un client non riesce a trovare un ruolo del sistema del sito disponibile nel gruppo di limiti corrente, usa l'intervallo di fallback in minuti per determinare dopo quanto tempo può iniziare a eseguire la ricerca di un sistema del sito disponibile associato al gruppo di limiti adiacente.  

Quando un client non riesce a trovare un sistema del sito disponibile e inizia a cercare in percorsi di gruppi di limiti adiacenti, aumenta il pool di sistemi del sito disponibili che può usare in base alla configurazione dei gruppi di limiti e delle relative relazioni.

- Un gruppo di limiti può avere più di una relazione. Ciò consente di configurare il fallback per ogni tipo del sistema del sito a diversi gruppi adiacenti dopo diversi intervalli di tempo.    
- I client eseguiranno il fallback a un gruppo limite solo se è direttamente adiacente al gruppo limite corrente.
- Se un client fa parte di più gruppi limite, il gruppo limite corrente è definito come un'unione di tutti i gruppi limite del client. Il client può quindi eseguire il fallback ai gruppi adiacenti di uno dei gruppi di limiti originali.

### <a name="the-default-site-boundary-group"></a>Gruppo di limiti predefinito del sito
Oltre ai gruppi di limiti che è possibile creare, ogni sito dispone di un gruppo di limiti predefinito creato da Configuration Manager. Questo gruppo è denominato ***Default-Site-Boundary-Group&lt;codicesito>***. Ad esempio, il gruppo per il sito ABC è denominato *Default-Site-Boundary-Group&lt;ABC>*.

Per ogni gruppo di limiti creato, Configuration Manager crea automaticamente un collegamento implicito a ogni gruppo di limiti predefinito del sito nella gerarchia.
-    Il collegamento implicito è un'opzione di fallback predefinita da un gruppo di limiti corrente al gruppo di limiti predefinito del sito che ha un intervallo di fallback predefinito di 120 minuti.
-    I client che non si trovano in un limite associato a un gruppo di limiti nella gerarchia usano automaticamente il gruppo di limiti predefinito dal sito assegnato per identificare i ruoli del sistema del sito validi che possono usare.

Per gestire il fallback al gruppo di limiti predefinito del sito:
- È possibile accedere alle proprietà del gruppo di limiti predefinito del sito e modificare i valori nella scheda **Comportamento predefinito**. Le modifiche apportate in questa scheda si applicano a *tutti* i collegamenti impliciti a questo gruppo di limiti. Queste impostazioni possono essere sostituite quando si configura il collegamento esplicito a questo gruppo di limiti predefinito del sito da un altro gruppo di limiti.
- È possibile accedere alle proprietà di un gruppo di limiti creato e modificare i valori per il collegamento esplicito a un gruppo di limiti predefinito del sito. Quando si imposta un nuovo intervallo in minuti per il fallback o il blocco del fallback, questa modifica influisce solo sul collegamento che si sta configurando. Le configurazioni del collegamento esplicito sostituiscono quelle della scheda **Comportamento predefinito** di un gruppo di limiti predefinito del sito.


## <a name="site-assignment"></a>Assegnazione sito  
 È possibile configurare ciascun gruppo di limiti con un sito assegnato per i client.  

-   Un client appena installato che usa l'assegnazione automatica del sito verrà aggiunto al sito assegnato di un gruppo di limiti che contiene il percorso di rete corrente del client.  
-   Dopo l'assegnazione a un sito, il client non modificherà la propria assegnazione del sito quando cambia il percorso di rete. Se il client ad esempio si sposta in un nuovo percorso di rete rappresentato da un limite in un gruppo di limiti con un'assegnazione sito diversa, il sito assegnato a tale client non verrà modificato.  
-   Quando l'individuazione sistema Active Directory rileva una nuova risorsa, le informazioni sulla rete per la risorsa individuata vengono valutate in rapporto ai limiti nei gruppi di limiti. Tramite questo processo la nuova risorsa viene associata a un sito assegnato per poter essere utilizzata dal metodo di installazione push client.  
-   Quando un limite è un membro di più gruppi di limiti con diversi siti assegnati, i client selezioneranno uno di questi siti in modo casuale.  
-   Le modifiche a un sito assegnato dei gruppi di limiti si applicano solo alle nuove azioni di assegnazione del sito. I client assegnati precedentemente a un sito non valutano di nuovo l'assegnazione del sito in base alle modifiche alla configurazione di un gruppo di limiti (o al proprio percorso di rete).  

Per altre informazioni sull'assegnazione dei siti per i client, vedere [Utilizzo dell'assegnazione automatica del sito per i computer](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) in [Come assegnare i client a un sito in System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

## <a name="distribution-points"></a>Punti di distribuzione

Quando un client richiede il percorso di un punto di distribuzione, Configuration Manager invia al client un elenco dei sistemi del sito del tipo appropriato che sono associati a ogni gruppo di limiti in cui è incluso il percorso di rete corrente del client:

-   **Durante la distribuzione del software**, i client richiedono un percorso per il contenuto di distribuzione disponibile a un punto di distribuzione o a un'altra origine di contenuto valida, ad esempio un client configurato per Peer cache.

-   **Durante la distribuzione del sistema operativo** i client richiedono un percorso per l'invio o la ricezione delle informazioni di migrazione dello stato.  

Durante la distribuzione del contenuto, se un client richiede contenuto non disponibile a un'origine nel gruppo di limiti corrente, continua a richiedere tale contenuto provando diverse origini di contenuto nel gruppo di limiti corrente finché non viene raggiunto il periodo di fallback per un gruppo di limiti adiacente o per il gruppo di limiti predefinito del sito. Se il client non ha ancora trovato il contenuto, estende la ricerca alle origini di contenuto in modo da includere i gruppi di limiti adiacenti.

Se tuttavia il contenuto viene distribuito su richiesta e non è disponibile in un punto di distribuzione quando richiesto da un client, viene avviato il processo di trasferimento del contenuto a tale punto di distribuzione ed è possibile che il client trovi tale server come origine di contenuto prima di eseguire il fallback per usare un gruppo di limiti adiacente.

## <a name="software-update-points"></a>Punti di aggiornamento software
A partire dalla versione 1702, i client usano gruppi di limiti per trovare un nuovo punto di aggiornamento software. È possibile aggiungere singoli punti di aggiornamento software a diversi gruppi di limiti per controllare quali server possono essere trovati da un client.

Quando si esegue l'aggiornamento da una versione precedente la 1702, tutti i punti di aggiornamento software esistenti vengono aggiunti al gruppo di limiti predefinito in ogni sito. Ciò consente di mantenere il comportamento di pre-aggiornamento in cui i client selezionano un punto di aggiornamento software dal pool di punti di aggiornamento software disponibili che è stato configurato per la gerarchia.  Questo comportamento viene mantenuto finché non si sceglie di aggiungere singoli punti di aggiornamento software a gruppi di limiti diversi per un comportamento di selezione e fallback controllato.

Se si installa un nuovo sito che esegue la versione 1702 o successiva, è necessario assegnare punti di aggiornamento software a un gruppo di limiti prima che i client possano individuarli e usarli.


Il fallback per i punti di aggiornamento software è configurato come altri ruoli del sistema del sito, ma con le avvertenze seguenti:
- **I nuovi client usano i gruppi di limiti per selezionare i punti di aggiornamento software.** Dopo l'installazione della versione 1702, i nuovi client installati selezionano un punto di aggiornamento software tra quelli associati ai gruppi di limiti configurati.

  Ciò sostituisce il comportamento precedente in cui i client selezionano un punto di aggiornamento software in maniera casuale da un elenco di punti che condividono la foresta dei client.

- **I client installati in precedenza continuano a usare il punto di aggiornamento software corrente fino a quando non eseguono il fallback per trovare un nuovo punto.** I client installati in precedenza e che hanno già un punto di aggiornamento software continueranno a usare tale punto finché il server non sarà irraggiungibile. Ciò include l'uso continuativo di un punto di aggiornamento software non associato al gruppo di limiti corrente del client.

  Quando un client che ha già un punto di aggiornamento software non riesce a raggiungerlo, può eseguire il fallback per trovarne un altro. Quando usa il fallback, il client riceve un elenco di tutti i punti di aggiornamento software dal gruppo di limiti corrente. Se non riesce a trovare un server disponibile per 120 minuti, eseguirà il fallback ai gruppi di limiti adiacenti e al gruppo di limiti predefinito del sito. Il fallback a entrambi i gruppi di limiti viene eseguito contemporaneamente perché l'intervallo di fallback dei punti di aggiornamento software ai gruppi adiacenti è impostato su 120 minuti e non è modificabile. L'intervallo di 120 minuti è anche il periodo predefinito usato per il fallback al gruppo di limiti predefinito del sito. Quando un client esegue il fallback a un gruppo di limiti adiacente e al gruppo di limiti predefinito del sito, prova a contattare i punti di aggiornamento software del gruppo di limiti adiacente prima di provare a usare uno di quelli del gruppo di limiti predefinito del sito.

  L'uso continuativo di un punto di aggiornamento software esistente, anche quando il server non è incluso nel gruppo di limiti corrente del client, è intenzionale. Questo avviene perché una modifica del punto di aggiornamento software può comportare un utilizzo elevato della larghezza di banda di rete poiché il client sincronizza i dati con il nuovo punto di aggiornamento software. Il ritardo nella transizione può evitare la saturazione della rete nel caso in cui tutti i client passino contemporaneamente a un nuovo punto di aggiornamento software.

- **Configurazioni per l'intervallo di fallback**: a differenza delle configurazioni di fallback per altri ruoli del sistema del sito, i punti di aggiornamento software non supportano ancora un intervallo configurabile in minuti. Il comportamento di fallback è limitato alle impostazioni seguenti:  
  - **Orari di fallback (in minuti)**: questa opzione è disabilitata per i punti di aggiornamento software e non può essere configurata. È impostata su 120 minuti.
  -     **Non eseguire mai il fallback**: quando si usa questa configurazione, è possibile bloccare il fallback per un punto di aggiornamento software a un gruppo di limiti adiacente.

## <a name="preferred-management-points"></a>Punti di gestione preferiti

 I punti di gestione preferiti consentono a un client di identificare un punto di gestione associato al percorso di rete corrente (limite).  

-   Il client prova a usare un punto di gestione preferito dal sito assegnato prima di usare un punto di gestione da questo sito non configurato come preferito.  
-   Per usare questa opzione è necessario abilitarla per la gerarchia e configurare i gruppi di limiti nei singoli siti primari per includere i punti di gestione che devono essere associati ai limiti del gruppo.  
-   Quando sono configurati punti di gestione preferiti e un client organizza l'elenco dei punti di gestione, il client inserisce i punti di gestione preferiti all'inizio dell'elenco di quelli assegnati, in cui sono inclusi tutti i punti di gestione del sito assegnato del client.  

> [!NOTE]  
>  Quando un client esegue il roaming (ossia, modifica i percorsi di rete, ad esempio quando un computer portatile viene spostato in un percorso di ufficio remoto), può usare un punto di gestione (o un punto di gestione proxy) dal sito locale nella nuova posizione prima di provare a usare un punto di gestione del sito assegnato (che include i punti di gestione preferiti).  Per altre informazioni, vedere [Informazioni su come i client trovano i servizi e le risorse del sito per System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

### <a name="overlapping-boundaries"></a>Limiti sovrapposti  
 Configuration Manager supporta le configurazioni con sovrapposizione dei limiti per il percorso del contenuto:  

-   **Quando un client richiede un contenuto** e il percorso di rete del client appartiene a più gruppi di limiti, Configuration Manager invia al client un elenco di tutti i punti di distribuzione che hanno il contenuto.  
-   **Quando un client richiede a un server di inviare o ricevere le informazioni di migrazione dello stato** e il percorso di rete del client appartiene a più gruppi di limiti, Configuration Manager invia al client un elenco di tutti i punti di migrazione dello stato associati a un gruppo di limiti che include il percorso di rete corrente del client.  

Questo comportamento consente al client di selezionare il server più vicino da cui trasferire le informazioni di migrazione dello stato o sul contenuto.  



## <a name="example-of-using-boundary-groups"></a>Esempio d'uso dei gruppi di limiti
L'esempio seguente usa un client che esegue la ricerca di contenuto da un punto di distribuzione. Questo esempio può essere applicato ad altri ruoli del sistema del sito che usano i gruppi di limiti. Tenere tuttavia presente che i punti di aggiornamento software non supportano la configurazione di un intervallo in minuti per il fallback a un gruppo adiacente e usano sempre un periodo di 120 minuti.

Creare tre gruppi limite che non condividono limiti o server del sistema del sito:
-    Gruppo BG_A con punti di distribuzione DP_A1 e DP_A2 associati al gruppo
-    Gruppo BG_B con punti di distribuzione DP_B1 e DP_B2 associati al gruppo
-    Gruppo BG_C con punti di distribuzione DP_C1 e DP_C2 associati al gruppo

Aggiungere i percorsi di rete dei client come limiti solo al gruppo limite BG_A e configurare le relazioni tra tale gruppo limite e gli altri due gruppi limite:
-    Configurare i punti di distribuzione per il primo gruppo *adiacente* (BG_B) da usare dopo 10 minuti. Questo gruppo contiene i punti di distribuzione DP_B1 e DP_B2. Entrambi sono ben connessi ai percorsi limite dei primi gruppi.
-    Configurare il secondo gruppo *adiacente* (BG_C) da usare dopo 20 minuti. Questo gruppo contiene i punti di distribuzione DP_C1 e DP_C2. Entrambi si trovano a un WAN rispetto agli altri due gruppi limite.
-    Aggiungere anche un punto di distribuzione aggiuntivo che si trova nel server del sito al gruppo limite del sito predefinito di siti. Si tratta della posizione di origine di contenuto meno preferita, ma si trova a livello centrale per tutti i gruppi limite.

    Esempio di gruppi limite e tempi di fallback:

     ![BG_Fallack](media/BG_Fallback.png)


Con questa configurazione:
-    Il client inizia la ricerca del contenuto dai punti di distribuzione nel relativo gruppo limite *corrente* (BG_A), cercando in ogni punto di distribuzione per due minuti prima di passare al successivo punto di distribuzione del gruppo limite. Il pool di client dei percorsi di origine del contenuto validi include DP_A1 e DP_A2.
-    Se il client non riesce a trovare il contenuto nel proprio gruppo limite *corrente* dopo 10 minuti di ricerca, aggiunge i punti di distribuzione dal gruppo limite BG_B alla ricerca. Continua quindi a eseguire la ricerca del contenuto da un punto di distribuzione nel proprio pool combinato di punti di distribuzione che include ora i gruppi limite BG_A sia BG_B. Il client continuerà a contattare ogni punto di distribuzione per due minuti prima di passare al successivo punto di distribuzione del pool. Il pool di client dei percorsi di origine del contenuto validi include DP_A1, DP_A2, DP_B1 e DP_B2.
-    Dopo altri 10 minuti (totale di 20 minuti), se il client non ha ancora rilevato un punto di distribuzione con contenuto, espande il proprio pool di punti di distribuzione disponibili per includere i punti del secondo gruppo *adiacente*, il gruppo limite BG_C. Il client ora dispone di 6 punti di distribuzione per la ricerca (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 e DP_C2) e continua la modifica a un nuovo punto di distribuzione ogni due minuti fino a quando il contenuto non viene trovato.
-    Se il client non ha rilevato il contenuto dopo un totale di 120 minuti, esegue il fallback per includere il *gruppo limite del sito predefinito* nella ricerca. Il pool di punti di distribuzione include ora tutti i punti di distribuzione dei tre gruppi di limiti configurati e il punto di distribuzione finale presente nel computer server del sito.  Il client continua quindi la ricerca del contenuto, modificando i punti di distribuzione ogni due minuti fino a quando il contenuto non viene trovato.

Configurando i vari gruppi adiacenti perché siano disponibili in momenti diversi, è possibile controllare quando i punti di distribuzione specifici vengono aggiunti come percorso di origine del contenuto e quando o se il client esegue il fallback al gruppo limite del sito predefinito come rete di protezione per il contenuto non disponibile in altre posizioni.






### <a name="update-existing-boundary-groups-to-the-new-model"></a>Aggiornare i gruppi di limiti esistenti al muovo modello
Quando si esegue l'aggiornamento a una versione precedente la 1610, vengono eseguite automaticamente le configurazioni seguenti. Queste configurazioni sono utili per verificare che il comportamento di fallback corrente rimanga disponibile finché non si configurano nuovi gruppi di limiti e relazioni.

-    Per ogni sito primario viene creato un gruppo di limiti del sito predefinito, denominato ***Default-Site-Boundary-Group&lt;codicesito>.***
  -    Punti di distribuzione con l'opzione *Consenti percorso origine di fallback per il contenuto* selezionata e punti di migrazione stato presso siti primari vengono aggiunti al gruppo di limiti *Default-Site-Boundary-Group&lt;codicesito>* di tale sito.
  -    A partire dalla versione 1702, i punti di aggiornamento software vengono aggiunti al gruppo *Default-Site-Boundary-Group&lt;codicesito>* di ogni sito.
-    Viene creata una copia di ogni gruppo limite esistente che include un server del sito configurato con una connessione lenta. Il nome del nuovo gruppo è ***&lt;nome gruppo limiti originale>-&lt;ID gruppo limiti originale>***:  
    -    I sistemi del sito che dispongono di una connessione veloce rimangono nel gruppo limite originale.
    -    Una copia dei sistemi del sito (punti di distribuzione e punti di gestione) che hanno una connessione lenta viene aggiunta alla copia del gruppo di limiti. I sistemi del sito originale configurati con una connessione lenta rimangono nel gruppo di limiti originale per garantire la compatibilità con le versioni precedenti, ma non vengono usati partendo da questo gruppo di limiti.
    - Questa copia del gruppo limite non dispone di limiti associati. Tuttavia, viene creato un collegamento fallback tra il gruppo originale e la nuova copia del gruppo limite che presenta l'ora di fallback impostata su zero.  


- **Valido solo per i siti secondari:**
  - Viene creato un gruppo di limiti se un sito secondario ha almeno un punto di distribuzione con l'opzione *Consenti percorso origine di fallback per il contenuto* selezionata o un punto di migrazione stato. Il nome del gruppo di limiti è ***Secondary-Site-Neighbor--Tmp&lt;codicesito>.***
  - Tutti i punti di distribuzione con l'opzione *Consenti percorso origine di fallback per il contenuto* selezionata e punti di migrazione stato vengono aggiunti al gruppo di limiti del sito secondario.
  - Viene creato un collegamento fallback tra il gruppo di limiti originale e il gruppo di limiti adiacente appena creato e il tempo di fallback viene impostato su zero.


 La tabella seguente identifica il nuovo comportamento di fallback previsto dalla combinazione di impostazioni di distribuzione originali e di configurazioni di punti di distribuzione:

Configurazione della distribuzione originale per "Non eseguire il programma" in una rete lenta  |Configurazione del punto di distribuzione originale per "Allow client to use a fallback source location for content" (Consenti al client di usare un percorso di origine di fallback per il contenuto)  |Nuovo comportamento di fallback  
---------|---------|---------
Selezionato     |  Selezionato    |  **Nessun fallback**: usare solo i punti di distribuzione nel gruppo limite corrente       
Selezionato     |  Non selezionato|  **Nessun fallback**: usare solo i punti di distribuzione nel gruppo limite corrente       
Non selezionato |  Non selezionato|  **Fallback verso adiacente**: usare i punti di distribuzione nel gruppo limite corrente e quindi aggiungere i punti di distribuzione del gruppo limite adiacente. A meno che non sia configurato un collegamento esplicito al gruppo limite del sito predefinito, i client non eseguono il fallback su questo gruppo.    
Non selezionato | Selezionato        |   **Fallback normale**: usare i punti di distribuzione nel gruppo limite corrente, quindi quelli del gruppo adiacente e dal gruppo limite del sito predefinito

 Tutte le altre configurazioni di distribuzione seguiranno il **Fallback normale**.  




## <a name="changes-from-prior-versions-for-ui-and-behavior-for-content-locations"></a>Modifiche all'interfaccia utente e al comportamento dei percorsi del contenuto rispetto alle versioni precedenti
Di seguito sono riportate le modifiche principali ai gruppi di limiti e alle modalità di ricerca del contenuto da parte dei client. Queste modifiche vengono introdotte con la versione 1610. Molti di queste modifiche e concetti funzionano in combinazione.


-    **Le configurazioni Veloce o Lento vengono rimosse:** non è più possibile configurare la velocità o la lentezza dei singoli punti di distribuzione.  Al contrario, ogni sistema del sito associato a un gruppo limite viene trattato ugualmente. Grazie a questa modifica, la scheda **Riferimenti** delle proprietà del gruppo limite non supporta la configurazione Veloce o Lento.
-     **Nuovo gruppo limite predefinito in ogni sito:** ciascun sito primario dispone di un nuovo gruppo limite predefinito denominato ***Default-Site-Boundary-Group&lt;CodiceSito>***.  Quando un client non è presente in un percorso di rete che viene assegnato a un gruppo limite, il client usa i sistemi del sito associati al gruppo predefinito del sito assegnato. Considerare l'uso di questo gruppo limite come sostituzione del concetto di percorso del contenuto di fallback.      
 -    L'opzione **"Allow fallback source locations for content"** (Consenti percorsi di origine di fallback per il contenuto) viene rimossa: la configurazione di un punto di distribuzione da usare per il fallback non avviene più in modo esplicito e le opzioni per impostare questa proprietà vengono rimosse dall'interfaccia utente.

    Il risultato dell'impostazione **Allow fallback source locations for content** (Consenti percorsi di origine di fallback per il contenuto) in un tipo di distribuzione per le applicazioni cambia. Questa impostazione su un tipo di distribuzione consente ora al client di usare il gruppo limite del sito predefinito come percorso di origine del contenuto.

 -    **Relazioni tra gruppi limite:** ciascun gruppo limite può essere collegato a uno o più gruppi limite aggiuntivi. Questi collegamenti costituiscono le relazioni configurate sulla nuova scheda delle proprietà del gruppo limite, denominata **Relationships** (Relazioni):
     -    Ogni gruppo limite associato direttamente a un client viene chiamato gruppo limite **corrente**.  
    -     Qualsiasi gruppo limite che un client può usare grazie all'associazione tra il gruppo limite *corrente* e un altro gruppo viene chiamato gruppo limite **adiacente**.
    -  Nella scheda **Relationships** (Relazioni) è possibile aggiungere gruppi limite da usare come gruppo limite *adiacente*. È anche possibile configurare una quantità di minuti che stabiliste il momento in cui il client che non riesce a trovare il contenuto da un punto di distribuzione nel gruppo *corrente* avvierà la ricerca dei percorsi del contenuto nei gruppi limite *adiacenti*.

        Quando si aggiunge o si modifica una configurazione del gruppo limite, è possibile bloccare il fallback su tale gruppo limite dal gruppo corrente che si sta configurando.

    Per usare la nuova configurazione, definire le associazioni esplicite (collegamenti) da un gruppo limite a un altro e configurare tutti i punti di distribuzione nel gruppo associato con la stessa durata in minuti. Il tempo configurato determina quando il momento in cui un client che non riesce a trovare l'origine di un contenuto del relativo gruppo limite *corrente* può iniziare a cercare le origini del contenuto nel gruppo limite adiacente.

    Oltre ai gruppi limite configurati in modo esplicito, ogni gruppo limite dispone di un collegamento implicito al gruppo limite del sito predefinito. Questo collegamento si attiva dopo 120 minuti, momento in cui il gruppo limite del sito predefinito diventa un gruppo limite adiacente che consente ai client di usare i punti di distribuzione associati a tale gruppo limite come percorsi di origine del contenuto.

    Questo comportamento sostituisce ciò che in precedenza veniva definito "fallback per il contenuto".  È possibile eseguire l'override di questo comportamento predefinito di 120 minuti, associando in modo esplicito il gruppo limite del sito predefinito a un gruppo *corrente* e impostando un momento specifico, indicato in minuti, o il blocco completo del fallback per impedirne l'uso.


-     **I client tentano di ottenere i contenuti da ogni punto di distribuzione per un massimo di 2 minuti:** quando un client cerca un percorso di origine del contenuto, tenta di accedere a ogni punto di distribuzione per 2 minuti prima di passare a un altro punto di distribuzione. Si tratta di una modifica rispetto alle versioni precedenti in cui i client tentavano di connettersi a un punto di distribuzione per un massimo di 2 ore.

    - Il primo punto di distribuzione che un client tenta di usare viene selezionato casualmente dal pool di punti di distribuzione disponibili nel gruppo, o gruppi, limite *corrente* del client.

    - Dopo due minuti, se il client non ha trovato il contenuto, passa a un nuovo punto di distribuzione e tenta di ottenere il contenuto da questo server. Questo processo viene ripetuto ogni due minuti fino a quando il client trova il contenuto o raggiunge l'ultimo server del pool.

    - Se un client non trova un percorso di origine del contenuto valido nel proprio pool *corrente* prima dell'intervallo di fallback verso un gruppo di limiti *adiacente*, il client aggiunge i punti di distribuzione dal gruppo *adiacente* alla fine dell'elenco corrente e quindi cerca nel gruppo espanso di percorsi di origine che include i punti di distribuzione di entrambi i gruppi di limiti.

        > [!TIP]  
        > Quando si crea un collegamento esplicito tra il gruppo limite corrente e il gruppo limite del sito predefinito e si definisce un intervallo di fallback inferiore al tempo di fallback per il collegamento a un gruppo limite adiacente, i client iniziano la ricerca dei percorsi di origine dal gruppo limite del sito predefinito prima di includere il gruppo adiacente.

    - Quando il client non riesce a ottenere il contenuto dall'ultimo server nel pool, avvia nuovamente il processo.


## <a name="procedures-for-boundary-groups"></a>Procedure per i gruppi di limiti
Le procedure seguenti si applicano alla versione 1610 e alle versioni successive. Se si usa una versione precedente la 1610, vedere le procedure in [Gruppi di limiti per System Center Configuration Manager versioni 1511, 1602 e 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606).


### <a name="to-create-a-boundary-group"></a>Per creare un gruppo di limiti  
1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia** >  **Gruppi di limiti**.  

2.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea gruppo di limiti**.  

3.  Nella finestra di dialogo **Crea gruppo di limiti** selezionare la scheda **Generale** e specificare un **Nome** per questo gruppo di limiti.  

4.  Fare clic su **OK** per salvare il nuovo gruppo di limiti.  


### <a name="to-configure-a-boundary-group"></a>Per configurare un gruppo di limiti  
 1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia** >  **Gruppi di limiti**.  

 2.  Selezionare il gruppo di limiti da modificare.  

 3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

 4.  Nella finestra di dialogo **Proprietà** per il gruppo di limiti selezionare la scheda **Generale** per modificare i limiti appartenenti a questo gruppo di limiti:  

     -   Per aggiungere i limiti, fare clic su **Aggiungi**, selezionare la casella di controllo per uno o più limiti e quindi fare clic su **OK**.  

     -   Per rimuovere i limiti, selezionare il limite e fare clic su **Rimuovi**.  

 5.  Selezionare la scheda **Riferimenti** per modificare l'assegnazione sito e la configurazione del server del sistema del sito associata:  

     -   Per consentire ai client di utilizzare questo gruppo di limiti per l'assegnazione sito, selezionare la casella di controllo **Utilizza questo gruppo limite per l'assegnazione sito**e quindi selezionare un sito dalla casella a discesa **Sito assegnato** .  

     -   Per configurare quali server del sistema del sito disponibili sono associati a questo gruppo di limiti:  

     1.  Fare clic su **Aggiungi**e quindi selezionare la casella di controllo per uno o più server. I server vengono aggiunti come server del sistema del sito associati per questo gruppo di limiti. Sono disponibili solo i server su cui è installato il ruolo del sistema del sito supportato.  

         > [!NOTE]  
         >  È possibile selezionare qualsiasi combinazione dei sistemi del sito disponibili da qualsiasi sito della gerarchia. I sistemi del sito selezionati vengono elencati nella scheda **Sistemi del sito** nelle proprietà di ogni limite appartenente a questo gruppo di limiti.  

     2.  Per rimuovere un server da questo gruppo di limiti, selezionare il server e quindi fare clic su **Rimuovi**.  

         > [!NOTE]  
         >  Per interrompere l'utilizzo di questo gruppo di limiti per i sistemi del sito in fase di associazione, è necessario rimuovere tutti i server elencati come server del sistema del sito associati.  

 6.  Selezionare la scheda **Relazioni** per configurare il comportamento di fallback:  

     - Fare clic su **Aggiungi** e quindi selezionare il gruppo di limiti da configurare.

     - Impostare un tempo di fallback per i punti di distribuzione. Dopo questo periodo i client del gruppo di limiti per il quale si stanno configurando relazioni saranno in grado di iniziare la ricerca di contenuto dai punti di distribuzione del gruppo di limiti che si sta aggiungendo.

     - Per evitare il fallback a un gruppo di limiti specifico, incluso il *gruppo di limiti predefinito del sito*, configurato per impostazione predefinita, selezionare il gruppo di limiti e quindi selezionare la casella **Non eseguire mai il fallback**.   

 7.  Fare clic su **OK** per chiudere le proprietà del gruppo di limiti e salvare la configurazione.  

#### <a name="to-associate-a-site-systme-server-with-a-boundary-group"></a>Per associare un server del sistema del sito a un gruppo di limiti  
 1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia** >  **Gruppi di limiti**.  

 2.  Selezionare il gruppo di limiti da modificare.  

 3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

 4.  Nella finestra di dialogo **Proprietà** per il gruppo di limiti selezionare la scheda **Riferimenti** .  

 5.  In **Seleziona server del sistema del sito**fare clic su **Aggiungi**, selezionare la casella di controllo per i server del sistema del sito da associare a questo gruppo di limiti, quindi fare clic su **OK**.  

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


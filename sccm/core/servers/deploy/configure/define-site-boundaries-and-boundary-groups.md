---
title: Definire i limiti del sito | Microsoft Docs
description: Di seguito viene spiegato come definire i percorsi di rete nella intranet che possono contenere i dispositivi da gestire.
ms.custom: na
ms.date: 12/15/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: edc406adf1fdfab8e821b63dc02f37a30504ecd3
ms.openlocfilehash: 6135a94e30e8cce8ed4b8d08e5de26c15988b195


---
# <a name="define-site-boundaries-and-boundary-groups-for-system-center-configuration-manager"></a>Definire i limiti del sito e i gruppi di limiti per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

I limiti per System Center Configuration Manager definiscono i percorsi di rete nella intranet che possono contenere i dispositivi da gestire. I gruppi di limiti sono gruppi logici di limiti che è possibile configurare. I gruppi di limiti e i limiti sono disponibili in tutta la gerarchia e non possono essere configurati per i singoli siti.  

 Una gerarchia può includere qualsiasi numero di gruppi di limiti e ogni gruppo di limiti può contenere qualsiasi combinazione dei tipi di limite seguenti:  

-   Subnet IP  
-   Nome del sito Active Directory  
-   Prefisso IPv6  
-   Intervallo indirizzi IP  

I client nella intranet valutano il relativo percorso di rete corrente e quindi usano tali informazioni per identificare i gruppi di limiti a cui appartengono.  

 I client usano i gruppi di limiti per:  
-   **Trovare un sito assegnato:** i gruppi di limiti consentono ai client di trovare un sito primario per l'assegnazione client (assegnazione automatica del sito).  
-   **Trovare specifici ruoli del sistema del sito che possono usare:**  quando si associa un gruppo di limiti a specifici ruoli del sistema del sito, il gruppo di limiti fornisce ai client l'elenco di sistemi del sito da usare durante la specifica del percorso del contenuto e come punti di gestione preferiti.  

I client in Internet o configurati come client solo per Internet non usano le informazioni relative ai limiti. Questi client non possono usare l'assegnazione automatica del sito e, se il punto di distribuzione è configurato per consentire le connessioni client da Internet, scaricano sempre il contenuto da qualsiasi punto di distribuzione del sito assegnato.  


##  <a name="a-namebkmkboundariesa-boundaries"></a><a name="BKMK_Boundaries"></a> Limiti  
 È possibile creare manualmente i singoli limiti. È anche possibile configurare [Active Directory Forest Discovery](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) per il rilevamento automatico e la creazione di limiti per ogni subnet IP e sito Active Directory individuati.  

-   Ciascun limite rappresenta un percorso di rete ed è disponibile da tutti i siti della gerarchia.  
-   Configuration Manager non supporta l'immissione diretta di una supernet come limite. È possibile, invece, usare il tipo di limite Intervallo di indirizzi IP.  
-   Quando l'individuazione foresta Active Directory individua una supernet assegnata a un sito di Active Directory, Configuration Manager converte la supernet in un limite Intervallo di indirizzi IP.  
-   Il limite su cui si trova un client è equivalente al sito Active Directory o all'indirizzo IP di rete identificato dal client. Non è raro che un client usi un indirizzo IP sconosciuto all'amministratore di Configuration Manager. Se il percorso di rete del client non è chiaro, verificare il percorso indicato dal client usando il comando **IPCONFIG** nel client.  

Quando si crea un limite, viene assegnato automaticamente un nome basato sul tipo e sull'ambito del limite. È impossibile modificare questo nome. Specificare invece una descrizione durante la configurazione per identificare il limite nella console di Configuration Manager.  

 Dopo aver creato un limite, è possibile modificarne le proprietà per eseguire le seguenti operazioni:  
-   Aggiungere il limite a uno o più gruppi di limiti.  
-   Modificare il tipo o l'ambito del limite.  
-   Visualizzare la scheda **Sistemi del sito** dei limiti per vedere quali server del sistema del sito (punti di distribuzione, punti di migrazione stato e punti di gestione) sono associati al limite.  

### <a name="to-create-a-boundary"></a>Per creare un limite  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia** > **Limiti**  

2.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea Boundary.**.  

3.  Nella scheda **Generale** della finestra di dialogo Crea limite è possibile specificare una **Descrizione** per identificare il limite tramite un nome descrittivo o un riferimento.  

4.  Selezionare un **Tipo** per questo limite:  

    -   Se si seleziona **Subnet IP**, è necessario specificare un **ID subnet** per questo limite.  
        > [!TIP]  
        >  È possibile specificare la **Rete** e la **Subnet Mask** per specificare automaticamente l' **ID subnet** . Quando si salva il limite, viene salvato solo il valore ID subnet.  

    -   Se si seleziona **Sito Active Directory**, è necessario specificare o utilizzare **Sfoglia** per selezionare un sito Active Directory nella foresta locale del server del sito.  

        > [!IMPORTANT]  
        >  Quando si specifica un sito Active Directory per un limite, il limite include ogni subnet IP appartenente a quel sito Active Directory. Se la configurazione del sito Active Directory viene modificata in Active Directory, verranno modificati anche i percorsi di rete inclusi in questo limite.  

    -   Se si seleziona **Prefisso IPv6**, è necessario specificare un **Prefisso** nel formato del prefisso IPv6.  

    -   Se si seleziona **Intervallo indirizzi IP**, è necessario specificare un **Indirizzo IP iniziale** e un **Indirizzo IP finale** che includano parte di una subnet IP o di più subnet IP.    

5.  Fare clic su **OK** per salvare il nuovo limite.  

### <a name="to-configure-a-boundary"></a>Per configurare un limite  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia** > **Limiti**  

2.  Selezionare il limite da modificare.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

4.  Nella finestra di dialogo **Proprietà** per il limite selezionare la scheda **Generale** per modificare la **Descrizione** o il **Tipo** per il limite. È inoltre possibile modificare l'ambito di un limite modificando i percorsi di rete per il limite. Per un limite del sito Active Directory è possibile ad esempio specificare un nuovo nome del sito Active Directory.  

5.  Selezionare la scheda **Sistemi del sito** per visualizzare i sistemi del sito associati a questo limite. È impossibile modificare questa configurazione dalle proprietà di un limite.  

    > [!TIP]  
    >  Per elencare un server di sistema del sito come sistema del sito per un limite, è necessario associare tale server come server di sistema del sito per almeno un gruppo di limiti che include questo limite. Questo viene configurato nella scheda **Riferimenti** di un gruppo di limiti.  

6.  Selezionare la scheda **Gruppi di limiti** per modificare l'appartenenza al gruppo di limiti per questo limite:  

    -   Per aggiungere questo limite a uno o più gruppi di limiti, fare clic su **Aggiungi**, selezionare la casella di controllo per uno o più gruppi di limiti e quindi fare clic su **OK**.  

    -   Per rimuovere questo limite da un gruppo di limiti, selezionare il gruppo di limiti e fare clic su **Rimuovi**.  

7.  Fare clic su **OK** per chiudere le proprietà del limite e salvare la configurazione.  

##  <a name="a-namebkmkboundarygroupsa-boundary-groups"></a><a name="BKMK_BoundaryGroups"></a> Boundary groups
> [!IMPORTANT]  
>  **Le informazioni contenute in questa sezione Gruppi di limiti e nelle sezioni figlio sono valide per la versione 1610 o versioni successive.** Questo contenuto è stato rivisto per descrivere in modo specifico le modifiche di progettazione relative ai gruppi di limiti introdotte con questa versione di aggiornamento.
>
> **Se si usa la versione 1511, 1602 o 1606**, vedere [Boundary groups for System Center Configuration Manager version 1511, 1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) (Gruppi di limiti per System Center Configuration Manager versioni 1511, 1602 e 1606) per informazioni su come usare e configurare i gruppi di limiti con tali versioni del prodotto.

La versione 1610 introduce importanti modifiche ai gruppi di limiti e al loro funzionamento con i punti di distribuzione. Queste modifiche semplificano la progettazione dell'infrastruttura del contenuto, offrendo maggiore controllo su come e quando i client eseguono il fallback per la ricerca di punti di distribuzione aggiuntivi come percorsi di origine del contenuto. Sono inclusi i punti di distribuzione in locale e su cloud.

**Informazioni sui gruppi di limiti:**  
 I gruppi di limiti vengono creati per raggruppare logicamente i percorsi di rete correlati (limiti) e semplificare la gestione dell'infrastruttura. Prima di usare un gruppo di limiti è necessario assegnare i limiti ai gruppi di limiti. I client usano la configurazione del gruppo di limiti per:  

-   Assegnazione automatica del sito  
-   Percorso contenuto  
-   Punti di gestione preferiti. Se si usano i punti di gestione preferiti, è necessario abilitare questa opzione per la gerarchia e non dalla configurazione del gruppo di limiti. Vedere la procedura [Per abilitare l'uso dei punti di gestione preferiti](#to-enable-use-of-preferred-management-points) più avanti in questo argomento.  

Quando si configurano i gruppi di limiti, si aggiungono uno o più limiti al gruppo di limiti e quindi si configurano le impostazioni aggiuntive per l'uso da parte dei client presenti in tali limiti.  

È possibile trovare [procedure per la gestione dei gruppi di limiti](#procedures-for-boundary-groups) più avanti in questo argomento.


###  <a name="a-namebkmkboundarysiteassignmenta-about-site-assignment"></a><a name="BKMK_BoundarySiteAssignment"></a> Informazioni sull'assegnazione del sito  
 È possibile configurare ciascun gruppo di limiti con un sito assegnato per i client.  

-   Un client appena installato che usa l'assegnazione automatica del sito verrà aggiunto al sito assegnato di un gruppo di limiti che contiene il percorso di rete corrente del client.  
-   Dopo l'assegnazione a un sito, il client non modificherà la propria assegnazione del sito quando cambia il percorso di rete. Se il client ad esempio si sposta in un nuovo percorso di rete rappresentato da un limite in un gruppo di limiti con un'assegnazione sito diversa, il sito assegnato a tale client non verrà modificato.  
-   Quando l'individuazione sistema Active Directory rileva una nuova risorsa, le informazioni sulla rete per la risorsa individuata vengono valutate in rapporto ai limiti nei gruppi di limiti. Tramite questo processo la nuova risorsa viene associata a un sito assegnato per poter essere utilizzata dal metodo di installazione push client.  
-   Quando un limite è un membro di più gruppi di limiti con diversi siti assegnati, i client selezioneranno uno di questi siti in modo casuale.  
-   Le modifiche a un sito assegnato dei gruppi di limiti si applicano solo alle nuove azioni di assegnazione del sito. I client assegnati precedentemente a un sito non valutano di nuovo l'assegnazione del sito in base alle modifiche alla configurazione di un gruppo di limiti (o al proprio percorso di rete).  

Per altre informazioni sull'assegnazione dei siti per i client, vedere [Utilizzo dell'assegnazione automatica del sito per i computer](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) in [Come assegnare i client a un sito in System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

###  <a name="a-namebkmkboundarycontentlocationa-about-content-location"></a><a name="BKMK_BoundaryContentLocation"></a> Informazioni sul percorso del contenuto  
Quando si configurano i gruppi di limiti, associare i limiti (percorsi di rete) e i ruoli del sistema del sito, ad esempio i punti di distribuzione, al gruppo di limiti. Questa operazione agevola il collegamento dei client ai server del sistema del sito, come i punti di distribuzione che si trovano vicino ai client nella rete.

È possibile assegnare lo stesso limite a più gruppi di limiti e i server del sistema del sito, ad esempio i punti di distribuzione, possono essere associati a più gruppi limite, rendendoli disponibili per una vasta gamma di percorsi di rete.

-   **Durante la distribuzione del software**, i client richiedono un percorso per il contenuto di distribuzione. Configuration Manager invia al client un elenco dei punti di distribuzione associati a ogni gruppo di limiti che include il percorso di rete corrente del client.  
-   **Durante la distribuzione del sistema operativo** i client richiedono un percorso per l'invio o la ricezione delle informazioni di migrazione dello stato. Configuration Manager invia al client un elenco dei punti di migrazione dello stato associati a ogni gruppo di limiti che include il percorso di rete corrente del client.  

È possibile definire relazioni tra gruppi di limiti per configurare il comportamento di fallback per i percorsi di origine del contenuto. Introdotte per la prima volta con la versione 1610, le relazioni vengono configurate nella nuova scheda **Relazioni** delle proprietà del gruppo di limiti. Le relazioni sostituiscono la necessità di configurare la velocità dei sistemi del sito o di impostare i gruppi di limiti in modo da consentire il percorso di origine di fallback per il contenuto.

Quando si configura il gruppo di limiti cosiddetto **corrente**, è possibile aggiungere altri gruppi di limiti per creare un collegamento unidirezionale dal gruppo di limiti corrente a ogni gruppo di limiti aggiunto. I gruppi di limiti aggiunti sono detti gruppi di limiti **adiacenti**. Quindi, per ogni collegamento a un gruppo di limiti adiacente è possibile configurare punti di distribuzione con un tempo di fallback definito in minuti. Questo tempo viene usato per determinare dopo quanto tempo i client del gruppo di limiti corrente possono fare uso dei punti di distribuzione del gruppo limite adiacente se i client non riescono a trovare un percorso di origine del contenuto valido nel gruppo di limiti corrente.

Se un client non riesce a trovare il contenuto e inizia la ricerca dei percorsi nei gruppi limite adiacenti, il pool di punti di distribuzione disponibili aumenta in modo controllato per quel client.

-   Un gruppo limite può avere più di una relazione. Ciò consente di configurare il fallback su diversi gruppi adiacenti a diversi intervalli di tempo.
-   I client eseguiranno il fallback a un gruppo limite solo se è direttamente adiacente al gruppo limite corrente.
-   Se un client fa parte di più gruppi limite, il gruppo limite corrente è definito come un'unione di tutti i gruppi limite del client. Il client può quindi eseguire il fallback a un gruppo adiacente di uno di questi gruppi limite originali.

Oltre ai collegamenti definiti dall'utente, esiste un collegamento implicito che viene creato automaticamente tra i gruppi limite creato dall'utente e il gruppo limite predefinito, creato automaticamente per ogni sito. Questo collegamento automatico:
-   Viene usato dai client che non si trovano in alcun limite associato a un gruppo di limiti nella gerarchia. I client usano automaticamente il gruppo di limiti predefinito del sito loro assegnato per identificare i percorsi di origine del contenuto validi.
-   Si tratta di un'opzione di fallback predefinita dal gruppo limite corrente al gruppo limite predefinito dei siti, usato dopo 120 minuti.

**Se il contenuto non è disponibile in un gruppo di limiti corrente:**  
Se il contenuto richiesto da un client non è disponibile in un'origine di contenuto valida in un gruppo di limiti corrente, il client usa il fallback immediato per cercare il contenuto in un punto di distribuzione di un gruppo di limiti adiacente:   
- Il fallback immediato avviene per i gruppi di limiti adiacenti configurati con il tempo di fallback più breve. Se non ci sono gruppi di limiti adiacenti con un tempo di fallback più breve, il fallback può interessare il gruppo di limiti del sito predefinito.
- Dopo il primo set di gruppi di limiti adiacenti, il fallback immediato interessa gruppi di limiti aggiuntivi, in base al tempo di fallback configurato per tali gruppi.

Se il contenuto viene distribuito su richiesta ma non è disponibile quando richiesto da un client, viene avviato il processo di trasferimento del contenuto a un punto di distribuzione nel limite corrente. Tuttavia, poiché il contenuto in quel momento non è disponibile, il client usa il fallback immediato a un gruppo di limiti adiacente con il tempo di fallback più breve. Quando il contenuto diventa disponibile nel gruppo di limiti corrente, i client aggiuntivi non usano più il fallback immediato a gruppi adiacenti.



**Esempio sull'uso del nuovo modello:**   
Creare tre gruppi limite che non condividono limiti o server del sistema del sito:
-   Gruppo BG_A con punti di distribuzione DP_A1 e DP_A2 associati al gruppo
-   Gruppo BG_B con punti di distribuzione DP_B1 e DP_B2 associati al gruppo
-   Gruppo BG_C con punti di distribuzione DP_C1 e DP_C2 associati al gruppo

Aggiungere i percorsi di rete dei client come limiti solo al gruppo limite BG_A e configurare le relazioni tra tale gruppo limite e gli altri due gruppi limite:
-   Configurare i punti di distribuzione per il primo gruppo *adiacente* (BG_B) da usare dopo 10 minuti. Questo gruppo contiene i punti di distribuzione DP_B1 e DP_B2. Entrambi sono ben connessi ai percorsi limite dei primi gruppi.
-   Configurare il secondo gruppo *adiacente* (BG_C) da usare dopo 20 minuti. Questo gruppo contiene i punti di distribuzione DP_C1 e DP_C2. Entrambi si trovano a un WAN rispetto agli altri due gruppi limite.
-   Aggiungere anche un punto di distribuzione aggiuntivo che si trova nel server del sito al gruppo limite del sito predefinito di siti. Si tratta della posizione di origine di contenuto meno preferita, ma si trova a livello centrale per tutti i gruppi limite.

    Esempio di gruppi limite e tempi di fallback:

     ![BG_Fallack](media/BG_Fallback.png)


Con questa configurazione:
-   Il client inizia la ricerca del contenuto dai punti di distribuzione nel relativo gruppo limite *corrente* (BG_A), cercando in ogni punto di distribuzione per due minuti prima di passare al successivo punto di distribuzione del gruppo limite. Il pool di client dei percorsi di origine del contenuto validi include DP_A1 e DP_A2.
-   Se il client non riesce a trovare il contenuto nel proprio gruppo limite *corrente* dopo 10 minuti di ricerca, aggiunge i punti di distribuzione dal gruppo limite BG_B alla ricerca. Continua quindi a eseguire la ricerca del contenuto da un punto di distribuzione nel proprio pool combinato di punti di distribuzione che include ora i gruppi limite BG_A sia BG_B. Il client continuerà a contattare ogni punto di distribuzione per due minuti prima di passare al successivo punto di distribuzione del pool. Il pool di client dei percorsi di origine del contenuto validi include DP_A1, DP_A2, DP_B1 e DP_B2.
-   Dopo altri 10 minuti (totale di 20 minuti), se il client non ha ancora rilevato un punto di distribuzione con contenuto, espande il proprio pool di punti di distribuzione disponibili per includere i punti del secondo gruppo *adiacente*, il gruppo limite BG_C. Il client ora dispone di 6 punti di distribuzione per la ricerca (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 e DP_C2) e continua la modifica a un nuovo punto di distribuzione ogni due minuti fino a quando il contenuto non viene trovato.
-   Se il client non ha rilevato il contenuto dopo un totale di 120 minuti, esegue il fallback per includere il *gruppo limite del sito predefinito* nella ricerca. Il pool di punti di distribuzione include ora tutti i punti di distribuzione dei tre gruppi limite configurati e il punto di distribuzione finale situato nel computer server del sito.  Il client continua quindi la ricerca del contenuto, modificando i punti di distribuzione ogni due minuti fino a quando il contenuto non viene trovato.

Configurando i vari gruppi adiacenti perché siano disponibili in momenti diversi, è possibile controllare quando i punti di distribuzione specifici vengono aggiunti come percorso di origine del contenuto e quando o se il client esegue il fallback al gruppo limite del sito predefinito come rete di protezione per il contenuto non disponibile in altre posizioni.




### <a name="update-existing-boundary-groups-to-the-new-model"></a>Aggiornare i gruppi di limiti esistenti al muovo modello
Quando si esegue l'aggiornamento alla versione 1610, vengono eseguite automaticamente le configurazioni seguenti. Tali configurazioni sono utili per verificare che il comportamento di fallback corrente rimanga disponibile finché non si configurano i nuovi gruppi limite e le relazioni.
-   Per ogni sito primario viene creato un gruppo di limiti del sito predefinito, denominato ***Default-Site-Boundary-Group&lt;codicesito>.***
-   Punti di distribuzione con l'opzione *Consenti percorso origine di fallback per il contenuto* selezionata e punti di migrazione stato presso siti primari vengono aggiunti al gruppo di limiti *Default-Site-Boundary-Group&lt;codicesito>* di tale sito.
-   Viene creata una copia di ogni gruppo limite esistente che include un server del sito configurato con una connessione lenta. Il nome del nuovo gruppo è ***&lt;nome gruppo limiti originale>-&lt;ID gruppo limiti originale>***:  
    -   I sistemi del sito che dispongono di una connessione veloce rimangono nel gruppo limite originale.
    -   Una copia dei sistemi del sito (punti di distribuzione, punti di gestione e punti di migrazione stato) che dispongono di una connessione lenta viene aggiunta alla copia del gruppo di limiti. I sistemi del sito originale configurati con una connessione lenta rimangono nel gruppo di limiti originale per garantire la compatibilità con le versioni precedenti, ma non vengono usati partendo da questo gruppo di limiti.
    -   Questa copia del gruppo limite non dispone di limiti associati. Tuttavia, viene creato un collegamento fallback tra il gruppo originale e la nuova copia del gruppo limite che presenta l'ora di fallback impostata su zero.  


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
Non selezionato | Selezionato     |   **Fallback normale**: usare i punti di distribuzione nel gruppo limite corrente, quindi quelli del gruppo adiacente e dal gruppo limite del sito predefinito

 Tutte le altre configurazioni di distribuzione seguiranno il **Fallback normale**.  



### <a name="changes-from-prior-versions-for-ui-and-behavior-for-content-locations"></a>Modifiche all'interfaccia utente e al comportamento dei percorsi del contenuto rispetto alle versioni precedenti
Di seguito sono riportate le modifiche principali ai gruppi limite e alle modalità di ricerca del contenuto da parte dei client introdotte con la versione 1610. Molti di queste modifiche e concetti funzionano in combinazione.


-   **Le configurazioni Veloce o Lento vengono rimosse:** non è più possibile configurare la velocità o la lentezza dei singoli punti di distribuzione.  Al contrario, ogni sistema del sito associato a un gruppo limite viene trattato ugualmente. Grazie a questa modifica, la scheda **Riferimenti** delle proprietà del gruppo limite non supporta la configurazione Veloce o Lento.
-   **Nuovo gruppo limite predefinito in ogni sito:** ciascun sito primario dispone di un nuovo gruppo limite predefinito denominato ***Default-Site-Boundary-Group&lt;CodiceSito>***.  Quando un client non è presente in un percorso di rete che viene assegnato a un gruppo limite, il client usa i sistemi del sito associati al gruppo predefinito del sito assegnato. Considerare l'uso di questo gruppo limite come sostituzione del concetto di percorso del contenuto di fallback.      
 -  L'opzione **"Allow fallback source locations for content"** (Consenti percorsi di origine di fallback per il contenuto) viene rimossa: la configurazione di un punto di distribuzione da usare per il fallback non avviene più in modo esplicito e le opzioni per impostare questa proprietà vengono rimosse dall'interfaccia utente.

    Il risultato dell'impostazione **Allow fallback source locations for content** (Consenti percorsi di origine di fallback per il contenuto) in un tipo di distribuzione per le applicazioni cambia. Questa impostazione su un tipo di distribuzione consente ora al client di usare il gruppo limite del sito predefinito come percorso di origine del contenuto.

 -  **Relazioni tra gruppi limite:** ciascun gruppo limite può essere collegato a uno o più gruppi limite aggiuntivi. Questi collegamenti costituiscono le relazioni configurate sulla nuova scheda delle proprietà del gruppo limite, denominata **Relationships** (Relazioni):
    -   Ogni gruppo limite associato direttamente a un client viene chiamato gruppo limite **corrente**.  
    -   Qualsiasi gruppo limite che un client può usare grazie all'associazione tra il gruppo limite *corrente* e un altro gruppo viene chiamato gruppo limite **adiacente**.
    -  Nella scheda **Relationships** (Relazioni) è possibile aggiungere gruppi limite da usare come gruppo limite *adiacente*. È anche possibile configurare una quantità di minuti che stabiliste il momento in cui il client che non riesce a trovare il contenuto da un punto di distribuzione nel gruppo *corrente* avvierà la ricerca dei percorsi del contenuto nei gruppi limite *adiacenti*.

        Quando si aggiunge o si modifica una configurazione del gruppo limite, è possibile bloccare il fallback su tale gruppo limite dal gruppo corrente che si sta configurando.

    Per usare la nuova configurazione, definire le associazioni esplicite (collegamenti) da un gruppo limite a un altro e configurare tutti i punti di distribuzione nel gruppo associato con la stessa durata in minuti. Il tempo configurato determina quando il momento in cui un client che non riesce a trovare l'origine di un contenuto del relativo gruppo limite *corrente* può iniziare a cercare le origini del contenuto nel gruppo limite adiacente.

    Oltre ai gruppi limite configurati in modo esplicito, ogni gruppo limite dispone di un collegamento implicito al gruppo limite del sito predefinito. Questo collegamento si attiva dopo 120 minuti, momento in cui il gruppo limite del sito predefinito diventa un gruppo limite adiacente che consente ai client di usare i punti di distribuzione associati a tale gruppo limite come percorsi di origine del contenuto.

    Questo comportamento sostituisce ciò che in precedenza veniva definito "fallback per il contenuto".  È possibile eseguire l'override di questo comportamento predefinito di 120 minuti, associando in modo esplicito il gruppo limite del sito predefinito a un gruppo *corrente* e impostando un momento specifico, indicato in minuti, o il blocco completo del fallback per impedirne l'uso.


-   **I client tentano di ottenere i contenuti da ogni punto di distribuzione per un massimo di 2 minuti:** quando un client cerca un percorso di origine del contenuto, tenta di accedere a ogni punto di distribuzione per 2 minuti prima di passare a un altro punto di distribuzione. Si tratta di una modifica rispetto alle versioni precedenti in cui i client tentavano di connettersi a un punto di distribuzione per un massimo di 2 ore.

    - Il primo punto di distribuzione che un client tenta di usare viene selezionato casualmente dal pool di punti di distribuzione disponibili nel gruppo, o gruppi, limite *corrente* del client.

    - Dopo due minuti, se il client non ha trovato il contenuto, passa a un nuovo punto di distribuzione e tenta di ottenere il contenuto da questo server. Questo processo viene ripetuto ogni due minuti fino a quando il client trova il contenuto o raggiunge l'ultimo server del pool.

    - Se un client non trova un percorso di origine del contenuto valido nel proprio pool *corrente* prima dell'intervallo di fallback verso un gruppo limite *adiacente*, il client aggiunge quindi i punti di distribuzione dal gruppo *adiacente* alla fine dell'elenco corrente e quindi cerca nel gruppo espanso di percorsi di origine che include i punti di distribuzione da entrambi i gruppi limite.

        > [!TIP]  
        > Quando si crea un collegamento esplicito tra il gruppo limite corrente e il gruppo limite del sito predefinito e si definisce un intervallo di fallback inferiore al tempo di fallback per il collegamento a un gruppo limite adiacente, i client iniziano la ricerca dei percorsi di origine dal gruppo limite del sito predefinito prima di includere il gruppo adiacente.

    - Quando il client non riesce a ottenere il contenuto dall'ultimo server nel pool, avvia nuovamente il processo.





###  <a name="a-namebkmkpreferredmpa-about-preferred-management-points"></a><a name="BKMK_PreferredMP"></a> Informazioni sui punti di gestione preferiti  
 I punti di gestione preferiti consentono a un client di identificare un punto di gestione associato al percorso di rete corrente (limite).  

-   Il client prova a usare un punto di gestione preferito dal sito assegnato prima di usare un punto di gestione da questo sito non configurato come preferito.  
-   Per usare questa opzione è necessario abilitarla per la gerarchia e configurare i gruppi di limiti nei singoli siti primari per includere i punti di gestione che devono essere associati ai limiti associati del gruppo di limiti  
-   Se sono configurati i punti di gestione preferiti e un client organizza l'elenco dei punti di gestione, il client inserisce i punti di gestione preferiti all'inizio dell'elenco dei punti di gestione assegnati (che include tutti i punti di gestione dal sito assegnato del client)  

> [!NOTE]  
>  Quando un client esegue il roaming (ossia, modifica i percorsi di rete, ad esempio quando un computer portatile viene spostato in un percorso di ufficio remoto), può usare un punto di gestione (o un punto di gestione proxy) dal sito locale nella nuova posizione prima di provare a usare un punto di gestione del sito assegnato (che include i punti di gestione preferiti).  Per altre informazioni, vedere [Informazioni su come i client trovano i servizi e le risorse del sito per System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

###   <a name="a-namebkmkboundaryoverlapa-about-overlapping-boundaries"></a><a name="BKMK_BoundaryOverlap"></a> Informazioni sui limiti sovrapposti  
 Configuration Manager supporta le configurazioni con sovrapposizione dei limiti per il percorso del contenuto:  

-   **Quando un client richiede un contenuto** e il percorso di rete del client appartiene a più gruppi di limiti, Configuration Manager invia al client un elenco di tutti i punti di distribuzione che hanno il contenuto.  
-   **Quando un client richiede a un server di inviare o ricevere le informazioni di migrazione dello stato** e il percorso di rete del client appartiene a più gruppi di limiti, Configuration Manager invia al client un elenco di tutti i punti di migrazione dello stato associati a un gruppo di limiti che include il percorso di rete corrente del client.  

Questo comportamento consente al client di selezionare il server più vicino da cui trasferire le informazioni di migrazione dello stato o sul contenuto.  






## <a name="procedures-for-boundary-groups"></a>Procedure per i gruppi di limiti
Le procedure seguenti si applicano alla versione 1610 e alle versioni successive. Se si usa la versione 1511, 1602 o 1606, vedere le procedure in [Boundary groups for System Center Configuration Manager versions 1511, 1602, and 1606](/sccm/core/servers/deploy/configure/boundary-groups-for-1511-1602-and-1606) (Gruppi di limiti per System Center Configuration Manager versioni 1511, 1602 e 1606).


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

     - Per evitare il fallback a un gruppo di limiti specifico, incluso il *gruppo di limiti del sito predefinito*, configurato per impostazione predefinita, selezionare il gruppo di limiti e quindi selezionare la casella **Never fallback** (Nessun fallback).   

 7.  Fare clic su **OK** per chiudere le proprietà del gruppo di limiti e salvare la configurazione.  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>Per associare un server di distribuzione del contenuto o un punto di gestione a un gruppo di limiti  
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


### <a name="to-enable-use-of-pre-release-features"></a>Per abilitare l'uso delle funzionalità di versione non definitiva
1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione del sito** > **Siti**, quindi nella scheda **Home** selezionare **Impostazioni gerarchia**.  

2.  Nella scheda **Generale** di Impostazioni gerarchia selezionare **Consent to use Pre-Release features** (Consenso a usare funzionalità di versioni non definitive).  

3.  Fare clic su **OK** per chiudere le finestra di dialogo e salvare la configurazione.  



##  <a name="a-namebkmkboundarybestpracticesa-best-practices-for-boundaries"></a><a name="BKMK_BoundaryBestPractices"></a> Procedure consigliate per i limiti  

-   **Usare una combinazione del numero minimo di limiti che soddisfano le esigenze:**  
   In passato era consigliabile preferire alcuni tipi di limiti rispetto ad altri. Con le modifiche apportate per migliorare le prestazioni, è ora consigliabile usare il tipo o i tipi di limiti più adatti all'ambiente in uso e il numero più basso possibile di limiti, per semplificare le attività di gestione.      

-   **Evitare la sovrapposizione dei limiti per l'assegnazione automatica del sito:**  
     Anche se ogni gruppo di limiti supporta sia le configurazioni di assegnazione del sito che quelle per il percorso del contenuto, è consigliabile creare un set separato di gruppi di limiti da usare solo per l'assegnazione del sito. Significato: verificare che ogni limite in un gruppo di limiti non sia membro di un altro gruppo di limiti con un'assegnazione del sito diversa. Motivo:  

    -   Un singolo limite può essere incluso in più gruppi di limiti  

    -   Ogni gruppo di limiti può essere associato a un sito primario diverso per l'assegnazione del sito  

    -   Un client in un limite membro di due gruppi di limiti con assegnazioni del sito diverse selezionerà in modo casuale il sito a cui aggiungersi, che potrebbe non corrispondere a quello a cui si intende aggiungere il client.  Questa configurazione è definita a limiti sovrapposti.  

     La sovrapposizione dei limiti non è un problema per il percorso del contenuto e spesso è la configurazione desiderata che fornisce ai client risorse aggiuntive o percorsi del contenuto che possono usare.  



<!--HONumber=Dec16_HO3-->



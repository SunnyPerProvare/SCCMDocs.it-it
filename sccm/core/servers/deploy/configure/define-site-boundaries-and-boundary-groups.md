---
title: Definire i limiti del sito | System Center Configuration Manager
description: Di seguito viene spiegato come definire i percorsi di rete nella intranet che possono contenere i dispositivi da gestire.
ms.custom: na
ms.date: 10/06/2016
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
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 9df8b5d5fd67a5ced5860771295d05dfb56a3982


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

#### <a name="to-create-a-boundary"></a>Per creare un limite  

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

#### <a name="to-configure-a-boundary"></a>Per configurare un limite  

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
 I gruppi di limiti vengono creati per raggruppare logicamente i percorsi di rete correlati (limiti) e semplificare la gestione dell'infrastruttura. Prima di usare un gruppo di limiti è necessario assegnare i limiti ai gruppi di limiti. I client usano la configurazione del gruppo di limiti per:  

-   Assegnazione automatica del sito  

-   Percorso contenuto  

-   Punti di gestione preferiti. Se si usano i punti di gestione preferiti, è necessario abilitare questa opzione per la gerarchia e non dalla configurazione del gruppo di limiti. Vedere la procedura seguente *Per abilitare l'uso dei punti di gestione preferiti*  

Quando si configurano i gruppi di limiti, si aggiungono uno o più limiti al gruppo di limiti e quindi si configurano le impostazioni aggiuntive per l'uso da parte dei client presenti in tali limiti.  

#### <a name="to-create-a-boundary-group"></a>Per creare un gruppo di limiti  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia** >  **Gruppi di limiti**.  

2.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Crea gruppo di limiti**.  

3.  Nella finestra di dialogo **Crea gruppo di limiti** selezionare la scheda **Generale** e specificare un **Nome** per questo gruppo di limiti.  

4.  Fare clic su **OK** per salvare il nuovo gruppo di limiti.  

#### <a name="to-configure-a-boundary-group"></a>Per configurare un gruppo di limiti  

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

    3.  Per modificare la velocità di connessione di rete per un server del sistema del sito per questo gruppo di limiti, selezionare il server e quindi fare clic su **Modifica connessione**.  

         Per impostazione predefinita, la velocità di connessione per ogni sistema del sito è impostata su **Veloce**, ma è possibile modificarla in **Lenta**. La velocità di connessione di rete e la configurazione di una distribuzione determinano se un client può scaricare il contenuto dal server.  

6.  Fare clic su **OK** per chiudere le proprietà del gruppo di limiti e salvare la configurazione.  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>Per associare un server di distribuzione del contenuto o un punto di gestione a un gruppo di limiti  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia** >  **Gruppi di limiti**.  

2.  Selezionare il gruppo di limiti da modificare.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

4.  Nella finestra di dialogo **Proprietà** per il gruppo di limiti selezionare la scheda **Riferimenti** .  

5.  In **Seleziona server del sistema del sito**fare clic su **Aggiungi**, selezionare la casella di controllo per i server del sistema del sito da associare a questo gruppo di limiti, quindi fare clic su **OK**.  

6.  Fare clic su **OK** per chiudere le finestra di dialogo e salvare la configurazione del gruppo di limiti.  

#### <a name="to-enable-use-of-preferred-management-points"></a>Per abilitare l'uso dei punti di gestione preferiti  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione del sito** > **Siti**, quindi nella scheda **Home** selezionare **Impostazioni gerarchia**.  

2.  Nella scheda **Generale** di Impostazioni gerarchia selezionare **I client preferiscono usare i punti di gestione specificati nei gruppi di limiti**.  

3.  Fare clic su **OK** per chiudere le finestra di dialogo e salvare la configurazione.  

#### <a name="to-configure-a-fallback-site-for-automatic-site-assignment"></a>Per configurare un sito di fallback per l'assegnazione sito automatica  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione del sito** >  **Siti**.  

2.  Nella scheda **Home** , del gruppo **Siti** , fare clic su **Impostazioni gerarchia**.  

3.  Nella scheda **Generale** selezionare la casella di controllo **Utilizza sito di fallback**e quindi selezionare un sito dall'elenco a discesa **Sito di fallback** .  

4.  Fare clic su **OK** per salvare la configurazione.  

 Le sezioni seguenti forniscono dettagli aggiuntivi sulle configurazioni del gruppo di limiti.  

###  <a name="a-namebkmkboundarysiteassignmenta-about-site-assignment"></a><a name="BKMK_BoundarySiteAssignment"></a> Informazioni sull'assegnazione del sito  
 È possibile configurare ciascun gruppo di limiti con un sito assegnato per i client.  

-   Un client appena installato che usa l'assegnazione automatica del sito verrà aggiunto al sito assegnato di un gruppo di limiti che contiene il percorso di rete corrente del client.  

-   Dopo l'assegnazione a un sito, il client non modificherà la propria assegnazione del sito quando cambia il percorso di rete. Se il client ad esempio si sposta in un nuovo percorso di rete rappresentato da un limite in un gruppo di limiti con un'assegnazione sito diversa, il sito assegnato a tale client non verrà modificato.  

-   Quando l'individuazione sistema Active Directory rileva una nuova risorsa, le informazioni sulla rete per la risorsa individuata vengono valutate in rapporto ai limiti nei gruppi di limiti. Tramite questo processo la nuova risorsa viene associata a un sito assegnato per poter essere utilizzata dal metodo di installazione push client.  

-   Quando un limite è un membro di più gruppi di limiti con diversi siti assegnati, i client selezioneranno uno di questi siti in modo casuale.  

-   Le modifiche a un sito assegnato dei gruppi di limiti si applicano solo alle nuove azioni di assegnazione del sito. I client assegnati precedentemente a un sito non valutano di nuovo l'assegnazione del sito in base alle modifiche alla configurazione di un gruppo di limiti (o al proprio percorso di rete).  

Per altre informazioni sull'assegnazione dei siti per i client, vedere [Utilizzo dell'assegnazione automatica del sito per i computer](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) in [Come assegnare i client a un sito in System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

###  <a name="a-namebkmkboundarycontentlocationa-about-content-location"></a><a name="BKMK_BoundaryContentLocation"></a> Informazioni sul percorso del contenuto  
 È possibile configurare ogni gruppo di limiti con uno o più punti di distribuzione e punti di migrazione stato che possono poi essere associati a più gruppi di limiti.  

-   **Durante la distribuzione del software**, i client richiedono un percorso per il contenuto di distribuzione. Configuration Manager invia al client un elenco dei punti di distribuzione associati a ogni gruppo di limiti che include il percorso di rete corrente del client.  

-   **Durante la distribuzione del sistema operativo, i client** richiedono un percorso per l'invio o la ricezione delle informazioni di migrazione dello stato. Configuration Manager invia al client un elenco dei punti di migrazione dello stato associati a ogni gruppo di limiti che include il percorso di rete corrente del client.  

Questo comportamento consente al client di selezionare il server più vicino da cui trasferire le informazioni di migrazione dello stato o sul contenuto.  

###  <a name="a-namebkmkpreferredmpa-about-preferred-management-points"></a><a name="BKMK_PreferredMP"></a> Informazioni sui punti di gestione preferiti  
 I punti di gestione preferiti consentono a un client di identificare un punto di gestione associato al percorso di rete corrente (limite).  

-   Il client prova a usare un punto di gestione preferito dal sito assegnato prima di usare un punto di gestione dal sito assegnato che non è configurato come preferito.  

-   Per usare questa opzione è necessario abilitarla per la gerarchia e configurare i gruppi di limiti nei singoli siti primari per includere i punti di gestione che devono essere associati ai limiti associati del gruppo di limiti  

-   Se sono configurati i punti di gestione preferiti e un client organizza l'elenco dei punti di gestione, il client inserisce i punti di gestione preferiti all'inizio dell'elenco dei punti di gestione assegnati (che include tutti i punti di gestione dal sito assegnato del client)  

> [!NOTE]  
>  Quando un client esegue il roaming (ossia, modifica i percorsi di rete, ad esempio quando un computer portatile viene spostato in un percorso di ufficio remoto), può usare un punto di gestione (o un punto di gestione proxy) dal sito locale nella nuova posizione prima di provare a usare un punto di gestione del sito assegnato (che include i punti di gestione preferiti).  Per altre informazioni, vedere [Informazioni su come i client trovano i servizi e le risorse del sito per System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

###  <a name="a-namebkmkboundaryoverlapa-about-overlapping-boundaries"></a><a name="BKMK_BoundaryOverlap"></a> Informazioni sui limiti sovrapposti  
 Configuration Manager supporta le configurazioni con sovrapposizione dei limiti per il percorso del contenuto:  

-   **Quando un client richiede un contenuto** e il percorso di rete del client appartiene a più gruppi di limiti, Configuration Manager invia al client un elenco di tutti i punti di distribuzione che hanno il contenuto.  

-   **Quando un client richiede a un server di inviare o ricevere le informazioni di migrazione dello stato** e il percorso di rete del client appartiene a più gruppi di limiti, Configuration Manager invia al client un elenco di tutti i punti di migrazione dello stato associati a un gruppo di limiti che include il percorso di rete corrente del client.  

Questo comportamento consente al client di selezionare il server più vicino da cui trasferire le informazioni di migrazione dello stato o sul contenuto.  

###  <a name="a-namebkmkboudnarynetworkspeeda-about-network-connection-speed"></a><a name="BKMK_BoudnaryNetworkSpeed"></a> Informazioni sulla velocità di connessione di rete  
 È possibile impostare la velocità di connessione di rete per ogni server del sistema del sito in un gruppo di limiti. Questa impostazione si applica ai client che si connettono a un sistema del sito basato su questa configurazione dei gruppi di limiti. Lo stesso server del sistema del sito può avere una velocità di connessione impostata nei diversi gruppi di limiti.  

 Per impostazione predefinita, la velocità di connessione di rete è configurata come **Veloce**, ma è possibile configurarla anche come **Lenta**. La velocità di connessione di rete e la configurazione della distribuzione determinano se per un client incluso in un gruppo di limiti associato è possibile scaricare contenuto da un punto di distribuzione.  

 Per altre informazioni sul modo in cui la configurazione della velocità di connessione di rete influisce sulle modalità di recupero del contenuto da parte dei client, vedere [Scenari del percorso di origine del contenuto](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

##  <a name="a-namebkmkboundarybestpracticesa-best-practices-for-boundaries"></a><a name="BKMK_BoundaryBestPractices"></a> Procedure consigliate per i limiti  

-   **Considerare l'uso del tipo di limite Intervallo di indirizzi IP solo quando non è possibile usare altri tipi di limite:**  

     Quando si progetta la strategia di limite, è consigliabile usare i limiti basati sui siti di Active Directory prima di usare altri tipi di limite. Qualora i limiti basati sui siti di Active Directory non rientrassero tra le opzioni, usare i limiti della subnet IP o IPv6. Se nessuna di queste opzioni è disponibile, usare i limiti Intervallo di indirizzi IP. Ciò si verifica perché il sito valuta i membri di limite periodicamente e la query richiesta per la valutazione dei membri di un Intervallo di indirizzi IP richiede un utilizzo notevolmente superiore delle risorse di SQL Server rispetto alle query che valutano i membri di altri tipi di limite.  

-   **Evitare la sovrapposizione dei limiti per l'assegnazione automatica del sito:**  

     Anche se ogni gruppo di limiti supporta sia le configurazioni di assegnazione del sito che quelle per il percorso del contenuto, è consigliabile creare un set separato di gruppi di limiti da usare solo per l'assegnazione del sito. Significato: verificare che ogni limite in un gruppo di limiti non sia membro di un altro gruppo di limiti con un'assegnazione del sito diversa. Motivo:  

    -   Un singolo limite può essere incluso in più gruppi di limiti  

    -   Ogni gruppo di limiti può essere associato a un sito primario diverso per l'assegnazione del sito  

    -   Un client in un limite membro di due gruppi di limiti con assegnazioni del sito diverse selezionerà in modo casuale il sito a cui aggiungersi, che potrebbe non corrispondere a quello a cui si intende aggiungere il client.  Questa configurazione è definita a limiti sovrapposti.  

     La sovrapposizione dei limiti non è un problema per il percorso del contenuto e spesso è la configurazione desiderata che fornisce ai client risorse aggiuntive o percorsi del contenuto che possono usare.  



<!--HONumber=Nov16_HO1-->



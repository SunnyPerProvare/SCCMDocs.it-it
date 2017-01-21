---
title: Configurare l&quot;individuazione | Microsoft Docs
description: "Configurare i metodi di individuazione da eseguire in un sito di Configuration Manager per trovare le risorse che è possibile gestire dall&quot;infrastruttura di rete e da Active Directory."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: 2fcc392ba700f871349200166fac715b73788c16

---
# <a name="configure-discovery-methods-for-system-center-configuration-manager"></a>Configurare i metodi di individuazione per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


Configurare i metodi di individuazione da eseguire in un sito di System Center Configuration Manager per trovare le risorse che è possibile gestire dall'infrastruttura di rete e da Active Directory. È necessario abilitare e configurare ogni metodo che si vuole usare per eseguire ricerche nel proprio ambiente. È possibile anche disabilitare un metodo seguendo la stessa procedura usata per abilitarlo.  Le uniche eccezioni sono il metodo di individuazione heartbeat e di individuazione server:  

-   Per impostazione predefinita, il metodo di individuazione heartbeat è già abilitato quando si installa un sito primario di Configuration Manager e configurato per eseguire una pianificazione di base. Mantenere abilitata l'individuazione heartbeat, poiché tale metodo assicura che i record dei dati di individuazione per i dispositivi siano aggiornati. Per altre informazioni sull'individuazione heartbeat, vedere [Informazioni sull'individuazione heartbeat](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat)  

-   L'individuazione server è un metodo di individuazione automatica che consente di individuare computer usati come sistemi del sito e non è possibile configurare o disabilitare questo metodo.  

**Per abilitare un metodo di individuazione configurabile:**  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia**, quindi scegliere **Metodi di individuazione**.  

2.  Selezionare il metodo di individuazione per il sito in cui si desidera attivare l'individuazione.  

3.  Nella scheda **Home** del gruppo **Proprietà** fare clic su **Proprietà** e quindi nella scheda **Generale** selezionare la casella di controllo **Abilita&lt;metodo di individuazione\>**.  

     Se questa casella di controllo è già selezionata, sarà possibile disattivare il metodo di individuazione deselezionando la casella di controllo.  

4.  Fare clic su **OK** per salvare la configurazione.  


##  <a name="a-namebkmkconfigadforestdisca-configure-active-directory-forest-discovery"></a><a name="BKMK_ConfigADForestDisc"></a> Configurare l'individuazione foresta Active Directory  
 Per completare la configurazione dell'individuazione foresta Active Directory, è necessario configurare le impostazioni in due posizioni:  

-   Nel nodo **Metodi di individuazione** è possibile attivare questo metodo di individuazione, impostare una pianificazione del polling e determinare se l'individuazione crea automaticamente limiti per le subnet e i siti Active Directory individuati.  

-   Nel nodo **Foreste Active Directory** è possibile aggiungere foreste da individuare, abilitare l'individuazione di siti e subnet di Active Directory in questa foresta, configurare impostazioni che consentono ai siti di Configuration Manager di pubblicare le informazioni sul sito nella foresta e infine di assegnare un account da usare come Account foresta Active Directory per ogni foresta.  

 Utilizzare le procedure seguenti per attivare l'individuazione foresta Active Directory e per configurare singole foreste per l'utilizzo con l'individuazione foresta Active Directory.  

#### <a name="to-enable-active-directory-forest-discovery"></a>Per attivare l'individuazione foresta Active Directory  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia**, quindi scegliere **Metodi di individuazione**.  

2.  Selezionare il metodo Individuazione foresta Active Directory per il sito in cui si desidera configurare l'individuazione.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

4.  Nella scheda **Generale** selezionare la casella di controllo per attivare l'individuazione. In alternativa, è possibile configurare ora l'individuazione, quindi attivarla in un secondo momento.  

5.  Specificare le opzioni per creare i limiti del sito per i percorsi individuati.  

6.  Specificare una pianificazione per l'esecuzione dell'individuazione.  

7.  Al termine della configurazione dell'individuazione foresta Active Directory per questo sito, fare clic su **OK** per salvare la configurazione.  

#### <a name="to-configure-a-forest-for-active-directory-forest-discovery"></a>Per configurare una foresta per l'individuazione foresta Active Directory  

1.  Nell'area di lavoro **Amministrazione** , fare clic su **Foreste Active Directory**. Se in precedenza è stato eseguito il metodo di individuazione foresta Active Directory, è possibile visualizzare ogni foresta rilevata nel riquadro dei risultati. La foresta locale e qualsiasi foresta trusted vengono individuate durante l'esecuzione del metodo di individuazione foresta Active Directory. È necessario aggiungere manualmente solo le foreste non trusted.  

    -   Per configurare una foresta individuata in precedenza, selezionarla nel riquadro dei risultati, quindi nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà** per aprire le proprietà della foresta. Procedere al passaggio 3.  

    -   Per configurare una nuova foresta non presente nell'elenco, nella scheda **Home** , nel gruppo **Crea** , fare clic su **Aggiungi foresta** per aprire la finestra di dialogo **Aggiungi foreste** . Procedere al passaggio 3.  

2.  Nella scheda **Generale** , completare le configurazioni per la foresta che si desidera individuare e specificare l' **Account foresta Active Directory**.  

    > [!NOTE]  
    >  Il metodo di individuazione della foresta Active Directory richiede un account globale per l'individuazione e la pubblicazione in foreste non trusted. Se non si usa l'account computer del server del sito, è possibile selezionare solo un account globale.  

3.  Se si prevede di autorizzare i siti alla pubblicazione dei relativi dati in questa foresta, completare le configurazioni per la pubblicazione in questa foresta nella scheda **Pubblicazione** .  

    > [!NOTE]  
    >  In caso di abilitazione dei siti alla pubblicazione in una foresta, è necessario estendere lo schema di Active Directory a questa foresta per Configuration Manager e l'account foresta Active Directory deve disporre delle autorizzazioni al controllo completo per il contenitore di sistema in quella foresta.  

4.  Dopo aver completato la configurazione di questa foresta per l'utilizzo con il metodo di individuazione della foresta Active Directory, fare clic su **OK** per salvare la configurazione.  

##  <a name="a-namebkmkconfigaddiscgenerala-configure-active-directory-discovery-for-computers-users-or-groups"></a><a name="BKMK_ConfigADDiscGeneral"></a> Configurare l'individuazione Active Directory per computer, utenti o gruppi  
 Utilizzare le informazioni nelle sezioni riportate di seguito per configurare l'individuazione di computer, utenti o gruppi, utilizzando uno dei seguenti metodi di individuazione:  

-   Individuazione gruppo Active Directory  

-   Individuazione sistema Active Directory  

-   individuazione utenti di Active Directory  

> [!NOTE]  
>  Le informazioni contenute in questa sezione non si applicano all'individuazione foresta Active Directory.  

 Anche se ogni metodo di individuazione è indipendente dagli altri, tutti i metodi condividono opzioni simili. Per altre informazioni su queste opzioni di configurazione, vedere l'argomento [Opzioni condivise per l'individuazione di gruppi, sistemi e utenti](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_shared).  

> [!WARNING]  
>  Il polling di Active Directory da ciascuno di questi metodi di individuazione può generare notevole traffico di rete. È consigliabile pianificare ogni metodo di individuazione in modo che venga eseguito in un momento in cui tale traffico di rete non influisca negativamente sugli usi aziendali della rete.  

#### <a name="to-configure-active-directory-group-discovery"></a>Per configurare l'individuazione gruppo Active Directory  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia**, quindi scegliere **Metodi di individuazione**.  

2.  Selezionare il metodo **Individuazione gruppo Active Directory** per il sito in cui si desidera configurare l'individuazione.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

4.  Nella scheda **Generale** selezionare la casella di controllo per attivare l'individuazione. In alternativa, è possibile configurare ora l'individuazione, quindi attivarla in un secondo momento.  

5.  Fare clic su **Aggiungi** per configurare un ambito di individuazione, selezionare **Gruppi** o **Percorso**, quindi completare le configurazioni seguenti nella finestra di dialogo **Aggiungi gruppi**o **Aggiungi percorso di Active Directory** :  

    1.  Specificare un **Nome** per questo ambito di individuazione.  

    2.  Specificare un **Dominio Active Directory** o **Percorso** per la ricerca:  

        -   Se si seleziona **Gruppi**, specificare uno o più gruppi di Active Directory da individuare.  

        -   Se si seleziona **Percorso**, specificare un contenitore Active Directory come percorso da individuare. È anche possibile attivare una ricerca ricorsiva dei contenitori figlio di Active Directory per questo percorso.  

    3.  Specificare l' **Account di individuazione gruppo Active Directory** utilizzato per la ricerca di questo ambito di individuazione.  

    4.  Fare clic su **OK** per salvare la configurazione dell'ambito di individuazione.  

6.  Ripetere il passaggio 6 per ogni ambito di individuazione aggiuntivo che si desidera definire.  

7.  Nella scheda **Pianificazione del polling** configurare la pianificazione del polling per l'individuazione completa e l'individuazione differenziale.  

8.  Facoltativamente, nella scheda **Opzioni** è possibile configurare le opzioni per escludere, tramite un filtro, dall'individuazione i record del computer non aggiornati e per individuare l'appartenenza dei gruppi di distribuzione.  

    > [!NOTE]  
    >  Per impostazione predefinita, l'individuazione gruppo Active Directory rileva solo l'appartenenza dei gruppi di sicurezza.  

9. Al termine della configurazione dell'individuazione gruppo Active Directory per questo sito, fare clic su **OK** per salvare la configurazione.  

#### <a name="to-configure-active-directory-system-discovery"></a>Per configurare l'individuazione sistema Active Directory  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia**, quindi scegliere **Metodi di individuazione**.  

2.  Selezionare il metodo per il sito in cui si desidera configurare l'individuazione.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

4.  Nella scheda **Generale** selezionare la casella di controllo per attivare l'individuazione. In alternativa, è possibile configurare ora l'individuazione, quindi attivarla in un secondo momento.  

5.  Fare clic sull'icona **Nuovo** ![icona Nuovo](media/Disc_new_Icon.gif) per specificare un nuovo contenitore Active Directory, quindi completare le configurazioni seguenti nella finestra di dialogo **Contenitore Active Directory**:  

    1.  Specificare uno o più percorsi in cui eseguire la ricerca.  

    2.  Per ogni percorso, specificare le opzioni che modificano il comportamento di ricerca.  

    3.  Specificare per ogni percorso l'account da utilizzare come **Account di individuazione Active Directory**.  

        > [!TIP]  
        >  Per ogni percorso specificato, è possibile configurare una serie di opzioni di individuazione e un account di individuazione Active Directory univoco.  

    4.  Fare clic su **OK** per salvare la configurazione del contenitore Active Directory.  

6.  Nella scheda Pianificazione del polling configurare la pianificazione del polling per l'individuazione completa e l'individuazione differenziale.  

7.  Facoltativamente, nella scheda **Attributi di Active Directory** è possibile configurare attributi aggiuntivi di Active Directory per i computer che si desidera individuare. Sono inoltre elencati gli attributi oggetto predefiniti.  

8.  Facoltativamente, nella scheda **Opzioni** è possibile configurare le opzioni per escludere, tramite un filtro, dall'individuazione i record del computer non aggiornati.  

9. Al termine della configurazione dell'individuazione sistema Active Directory per questo sito, fare clic su **OK** per salvare la configurazione.  

#### <a name="to-configure-active-directory-user-discovery"></a>Per configurare l'individuazione utente Active Directory  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia**, quindi scegliere **Metodi di individuazione**.  

2.  Selezionare il metodo **Individuazione utente Active Directory** per il sito in cui si desidera configurare l'individuazione.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

4.  Nella scheda **Generale** selezionare la casella di controllo per attivare l'individuazione. In alternativa, è possibile configurare ora l'individuazione, quindi attivarla in un secondo momento.  

5.  Fare clic sull'icona **Nuovo** ![icona Nuovo](media/Disc_new_Icon.gif) per specificare un nuovo contenitore Active Directory, quindi completare le configurazioni seguenti nella finestra di dialogo **Contenitore Active Directory**:  

    1.  Specificare uno o più percorsi in cui eseguire la ricerca.  

    2.  Per ogni percorso, specificare le opzioni che modificano il comportamento di ricerca.  

    3.  Specificare per ogni percorso l'account da utilizzare come **Account di individuazione Active Directory**.  

        > [!NOTE]  
        >  Per ogni percorso specificato, è possibile configurare una serie univoca di opzioni di individuazione e un account di individuazione Active Directory univoco.  

    4.  Fare clic su **OK** per salvare la configurazione del contenitore Active Directory.  

6.  Nella scheda **Pianificazione del polling** configurare la pianificazione del polling per l'individuazione completa e l'individuazione differenziale.  

7.  Facoltativamente, nella scheda **Attributi di Active Directory** è possibile configurare attributi aggiuntivi di Active Directory per i computer che si desidera individuare. Sono inoltre elencati gli attributi oggetto predefiniti.  

8.  Al termine della configurazione dell'individuazione utente Active Directory per questo sito, fare clic su **OK** per salvare la configurazione.  

##  <a name="a-namebkmkconfighbdisca-configure-heartbeat-discovery"></a><a name="BKMK_ConfigHBDisc"></a> Configurare l'individuazione heartbeat  
 Per impostazione predefinita, l'individuazione heartbeat è abilitata quando si installa un sito primario di Configuration Manager. È quindi necessario configurare solo la pianificazione della frequenza di invio dei record dei dati di individuazione heartbeat a un punto di gestione da parte dei client quando non si vuole usare il valore predefinito di ogni 7 giorni.  

> [!NOTE]  
>  Se l'installazione push del client e l'attività di gestione del sito per **Cancella flag di installazione** sono attivati nello stesso sito, impostare la pianificazione dell'individuazione heartbeat in modo che sia inferiore al valore **Periodo nuova individuazione client** dell'attività di gestione del sito **Cancella flag di installazione** . Per altre informazioni sulle attività di manutenzione del sito, vedere [Attività di manutenzione per System Center Configuration Manager](../../../../core/servers/manage/maintenance-tasks.md).  

#### <a name="to-configure-the-heartbeat-discovery-schedule"></a>Per configurare la pianificazione dell'individuazione heartbeat  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia**, quindi fare clic su **Metodi di individuazione**  

2.  Selezionare **Individuazione heartbeat** per il sito in cui si desidera eseguire l'individuazione heartbeat.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

4.  Configurare la frequenza con cui i client inviano i record dei dati di individuazione heartbeat, quindi fare clic su **OK** per salvare la configurazione.  

##  <a name="a-namebkmkconfignetworkdisca-configure-network-discovery"></a><a name="BKMK_ConfigNetworkDisc"></a> Configurare l'individuazione di rete  
 Utilizzare le informazioni nelle sezioni riportate di seguito per configurare l'individuazione della rete.  

###  <a name="a-namebkmkaboutconfignetworkdisca-about-configuring-network-discovery"></a><a name="BKMK_AboutConfigNetworkDisc"></a> Informazioni sulla configurazione dell'individuazione di rete  
 Prima di configurare l'individuazione della rete, è necessaria una comprensione dei concetti seguenti:  

-   Livelli disponibili per l'individuazione della rete  

-   Opzioni disponibili per l'individuazione della rete  

-   Applicazione di limiti all'individuazione della rete in rete  

Per altre informazioni, vedere la sezione [Informazioni sull'individuazione di rete](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutNetwork).  

 Nelle sezioni seguenti vengono fornite informazioni sulle configurazioni comuni per l'individuazione della rete. È possibile definire una o più di queste configurazioni per l'utilizzo durante la stessa esecuzione dell'individuazione. Se si utilizzano più configurazioni, sarà necessario considerare le interazioni che possono influenzare i risultati dell'individuazione.  

 Ad esempio, è possibile individuare tutti i dispositivi SNMP che utilizzano uno specifico nome di comunità SNMP. Per la stessa esecuzione dell'individuazione, è inoltre possibile disattivare l'individuazione in una subnet specifica. Durante l'esecuzione dell'individuazione, l'individuazione della rete non rileverà i dispositivi SNMP con il nome di comunità specificato nella subnet disattivata.  

####  <a name="a-namebkmkdeterminenettopologya-determine-your-network-topology"></a><a name="BKMK_DetermineNetTopology"></a> Determinare la topologia di rete  
 Per eseguire il mapping della rete, è possibile utilizzare un'individuazione solo per topologia. Questo tipo di individuazione non rileva i potenziali client. L'individuazione di rete solo per topologia si basa su SNMP.  

 Quando si esegue il mapping della topologia di rete, è necessario configurare gli **Hop massimi** nella scheda **SNMP** nella finestra di dialogo **Proprietà dell'individuazione della rete** . Con solo pochi hop è possibile controllare la larghezza di banda di rete che viene utilizzata quando viene eseguita l'individuazione. Man mano che l'individuazione di rete avanza, è possibile aumentare il numero di hop per ottenere una migliore comprensione della topologia di rete.  

 Dopo aver compreso la topologia di rete, è possibile configurare proprietà aggiuntive per l'individuazione di rete per individuare potenziali client e i relativi sistemi operativi, mentre si utilizzano le configurazioni disponibili per limitare i segmenti di rete in cui l'individuazione di rete è in grado di effettuare la ricerca.  

####  <a name="a-namebkmklimitbysubneta-limit-searches-by-using-subnets"></a><a name="BKMK_LimitBySubnet"></a> Limitare le ricerche mediante subnet  
 È possibile configurare l'individuazione di rete per effettuare la ricerca in subnet specifiche durante un ciclo di individuazione. Per impostazione predefinita, l'individuazione di rete effettua la ricerca nella subnet del server che esegue l'individuazione. Eventuali altre subnet configurate e abilitate si applicano esclusivamente alle opzioni di ricerca del Simple Network Management Protocol (SNMP) e del Dynamic Host Configuration Protocol (DHCP). Per la ricerca nei domini, l'individuazione di rete non è limitata dalle configurazioni per subnet.  

 Se si specificano una o più subnet nella scheda **Subnet** della finestra di dialogo **Proprietà dell'individuazione della rete** , la ricerca viene effettuata solo nelle subnet che sono contrassegnate con **Attivato** .  

 Quando si disabilita una subnet, essa viene esclusa dall'individuazione e vengono applicate le seguenti condizioni:  

-   Le query basate su SNMP non vengono eseguite sulla subnet  

-   I server DHCP non rispondono con un elenco di risorse che si trovano nella subnet  

-   Le query basate su dominio possono individuare risorse che si trovano nella subnet  

####  <a name="a-namebkmksearchbydomaina-search-a-specific-domain"></a><a name="BKMK_SearchByDomain"></a> Eseguire ricerche in un dominio specifico  
 È possibile configurare l'individuazione di rete per effettuare la ricerca in un dominio specifico o in un insieme di domini durante l'esecuzione dell'individuazione. Per impostazione predefinita, l'individuazione di rete effettua la ricerca nel dominio locale del server che esegue l'individuazione.  

 Se si specificano uno o più domini nella scheda **Domini** della finestra di dialogo **Proprietà dell'individuazione della rete** , viene effettuata la ricerca solo nei domini che sono contrassegnati con **Attivato** .  

 Quando si disabilita un dominio, esso viene escluso dall'individuazione e vengono applicate le seguenti condizioni:  

-   L'individuazione di rete non esegue la query dei controller di dominio in quel dominio  

-   Le query basate su SNMP possono comunque essere eseguite su subnet in quel dominio  

-   I server DHCP possono comunque rispondere con un elenco di risorse presenti nel dominio  

####  <a name="a-namebkmklimitbysnmpnamea-limit-searches-by-using-snmp-community-names"></a><a name="BKMK_LimitBySNMPname"></a> Limitare le ricerche mediante i nomi comunità SNMP  
 L'individuazione di rete viene configurata per effettuare la ricerca in una comunità SNMP specifica o in un insieme di comunità durante l'esecuzione dell'individuazione. Per impostazione predefinita, è configurato per l'utilizzo il nome comunità di **Pubblico** .  

 L'individuazione di rete utilizza i nomi comunità per accedere ai router che sono dispositivi SNMP. Un router può fornire l'individuazione di rete con informazioni su altri router e subnet che sono collegati al primo router.  

> [!NOTE]  
>  I nomi comunità SNMP sono simili alle password. L'individuazione di rete può ottenere informazioni solo da un dispositivo SNMP per il quale è stato specificato un nome comunità. Ciascun dispositivo SNMP può avere il proprio nome comunità, ma spesso lo stesso nome comunità viene condiviso tra diversi dispositivi. Inoltre, la maggior parte dei dispositivi SNMP hanno un nome comunità predefinito, cioè **Pubblico**. Tuttavia, alcune organizzazioni eliminano il nome comunità **Pubblico** dai propri dispositivi come misura di sicurezza.  

 Se più comunità SNMP vengono visualizzate nella scheda **SNMP** della finestra di dialogo **Proprietà dell'individuazione della rete** , l'individuazione di rete effettua la ricerca in esse nell'ordine di visualizzazione. Per ridurre al minimo il traffico di rete generato dai tentativi di contattare un dispositivo utilizzando nomi diversi, assicurarsi che i nomi utilizzati più di frequente appaiano nella parte superiore dell'elenco.  

> [!NOTE]  
>  Oltre a utilizzare il nome comunità SNMP, è possibile specificare l'indirizzo IP o il nome risolvibile di un dispositivo SNMP specifico. È possibile configurare l'indirizzo IP o il nome risolvibile di un dispositivo specifico nella scheda **Dispositivi SNMP** della finestra di dialogo **Proprietà dell'individuazione della rete** .  

####  <a name="a-namebkmksearchbydhcpa-search-a-specific-dhcp-server"></a><a name="BKMK_SearchByDHCP"></a> Eseguire ricerche in un server DHCP specifico  
 È possibile configurare l'individuazione di rete per l'utilizzo di un server DHCP specifico o di più server per individuare i client DHCP durante l'esecuzione dell'individuazione.  

 L'individuazione di rete effettua la ricerca in ogni server DHCP specificato nella scheda **DHCP** della finestra di dialogo **Proprietà dell'individuazione della rete** . Se il server che sta eseguendo l'individuazione esegue il lease dell'indirizzo IP da un server DHCP, è possibile configurare l'individuazione per effettuare la ricerca in quel server DHCP selezionando la casella di controllo **Includi il server DHCP per il cui utilizzo è configurato il server di sito** .  

> [!NOTE]  
>  Per configurare correttamente un server DHCP nell'individuazione di rete, l'ambiente deve supportare IPv4. Non è possibile configurare l'individuazione di rete per utilizzare un server DHCP in un ambiente IPv6 nativo.  

###  <a name="a-namebkmkhowtoconfignetdisca-how-to-configure-network-discovery"></a><a name="BKMK_HowToConfigNetDisc"></a> Come configurare l'individuazione di rete  
 Utilizzare le seguenti procedure per individuare in primo luogo la topologia di rete, quindi per configurare l'individuazione di rete e individuare potenziali client utilizzando una o più delle opzioni di individuazione di rete disponibili.  

##### <a name="to-determine-your-network-topology"></a>Per determinare la topologia di rete  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia**, quindi fare clic su **Metodi di individuazione**  

2.  Selezionare **Individuazione di rete** per il sito in cui si desidera eseguire l'individuazione di rete.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

    -   Nella scheda **Generale** , selezionare la casella di controllo **Abilita individuazione della rete** , quindi selezionare **Topologia** dalle opzioni **Tipo di individuazione** .  

    -   Nella scheda **Subnet** , selezionare la casella di controllo **Cerca subnet locali** .  

        > [!TIP]  
        >  Se si conoscono le subnet specifiche che costituiscono la rete, è possibile deselezionare la casella di controllo **Cerca subnet locali** e usare l'icona **Nuovo** ![icona Nuovo](media/Disc_new_Icon.gif) per aggiungere le subnet specifiche in cui si vuole eseguire la ricerca. Per reti di grandi dimensioni, spesso è meglio effettuare la ricerca solo in una o due subnet alla volta per ridurre al minimo l'uso della larghezza di banda di rete.  

    -   Nella scheda **Domini** , selezionare la casella di controllo **Cerca dominio locale** .  

    -   Nella scheda **SNMP** , utilizzare l'elenco a discesa **Hop massimi** per specificare quanti hop router può prendere l'individuazione di rete nel mapping della topologia.  

        > [!TIP]  
        >  Quando si esegue per la prima volta la topologia di rete, configurare un numero limitato di hop router per ridurre al minimo l'utilizzo della larghezza di banda di rete.  

4.  Nella scheda **Pianifica** fare clic sull'icona **Nuovo** ![icona Nuovo](media/Disc_new_Icon.gif) per impostare una pianificazione per l'esecuzione dell'individuazione di rete.  

    > [!NOTE]  
    >  Non è possibile assegnare una configurazione di individuazione diversa per separare le varie pianificazioni dell'individuazione di rete. Ogni volta che viene eseguita l'individuazione di rete, essa utilizza la configurazione di individuazione corrente.  

5.  Fare clic su **OK** per accettare le configurazioni. L'individuazione di rete viene eseguita all'orario specificato.  

##### <a name="to-configure-network-discovery"></a>Per configurare l'individuazione di rete  

1.  Nella console di Configuration Manager fare clic su **Amministrazione** > **Configurazione della gerarchia**, quindi fare clic su **Metodi di individuazione**  

2.  Selezionare **Individuazione di rete** per il sito in cui si desidera eseguire l'individuazione di rete.  

3.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

4.  Nella scheda **Generale** , selezionare la casella di controllo **Abilita individuazione della rete** , quindi selezionare il tipo di individuazione che si desidera eseguire dalle opzioni **Tipo di individuazione** .  

5.  Per la configurazione dell'individuazione per effettuare la ricerca nelle subnet, fare clic sulla scheda **Subnet** e, nella scheda **Subnet** , configurare una o più delle seguenti opzioni:  

    -   Per eseguire l'individuazione sulle subnet che si trovano in locale sul computer che esegue l'individuazione, selezionare la casella di controllo **Cerca subnet locali** .  

    -   Per effettuare la ricerca in una subnet specifica, tale subnet deve comparire nell'elenco in **Subnet da cercare**e **Cerca** deve essere impostato su **Attivato**:  

        1.  Se la subnet non compare in elenco, fare clic sull'icona **Nuovo** ![icona Nuovo](media/Disc_new_Icon.gif). Nella finestra di dialogo **Nuova assegnazione subnet** , immettere le informazioni **Subnet** e **Mask** , quindi fare clic su **OK**. Per impostazione predefinita, una nuova subnet è abilitata per la ricerca.  

        2.  Per modificare il valore **Cerca** per una subnet presente in elenco, selezionare la subnet, quindi fare clic sull'icona **Mostra/Nascondi** per mostrare/nascondere il valore **Disattivato** o **Attivato**.  

6.  Per la configurazione dell'individuazione per effettuare la ricerca nei domini, fare clic sulla scheda **Domini** e, nella scheda **Domini** , configurare una o più delle seguenti opzioni:  

    -   Per eseguire l'individuazione sul dominio del computer che esegue l'individuazione, selezionare la casella di controllo **Cerca domini locali** .  

    -   Per effettuare la ricerca in un dominio specifico, tale dominio deve comparire nell'elenco in **Domini** e **Cerca** deve essere impostato su **Attivato**:  

        1.  Se il dominio non compare in elenco, fare clic sull'icona **Nuovo** ![icona Nuovo](media/Disc_new_Icon.gif), quindi nella finestra di dialogo **Proprietà dominio** immettere l'informazione **Dominio** e fare clic su **OK**. Per impostazione predefinita, un nuovo dominio è abilitato per la ricerca.  

        2.  Per modificare il valore **Cerca** per un dominio presente in elenco, selezionare il dominio, quindi fare clic sull'icona **Mostra/Nascondi** per mostrare/nascondere il valore **Disattivato** o **Attivato**.  

7.  Per la configurazione dell'individuazione per la effettuare la ricerca nei nomi comunità SNMP per dispositivi SNMP, fare clic sulla scheda **SNMP** e, nella scheda **SNMP** , configurare una o più delle seguenti opzioni:  

    -   Per aggiungere un nome comunità SNMP all'elenco di **Nomi comunità SNMP**, fare clic sull'icona **Nuovo** ![icona Nuovo](media/Disc_new_Icon.gif), quindi nella finestra di dialogo **Nuovo nome comunità SNMP** specificare il **Nome** della comunità SNMP e fare clic su **OK**.  

    -   Per rimuovere un nome comunità SNMP, selezionare il nome comunità, quindi fare clic sull'icona **Elimina** ![icona Elimina](media/Disc_delete_Icon.gif).  

    -   Per regolare l'ordine di ricerca dei nomi comunità SNMP, selezionare un nome comunità, quindi fare clic sull'icona **Sposta elemento in alto**![icona di spostamento verso l'alto](media/Disc_moveUp_Icon.gif) oppure sull'icona **Sposta elemento in basso** ![icona di spostamento verso il basso](media/Disc_moveDown_Icon.gif). Quando viene eseguita l'individuazione, viene effettuata la ricerca nei nomi comunità seguendo un ordine dall'alto in basso.  

        > [!NOTE]  
        >  L'individuazione di rete utilizza i nomi comunità SNMP per accedere ai router che sono dispositivi SNMP. Un router può informare l'individuazione di rete su altri router e subnet collegati al primo router.  

        -   I nomi comunità SNMP sono simili alle password.  

        -   L'individuazione di rete può ottenere informazioni solo da un dispositivo SNMP per il quale è stato specificato un nome comunità.  

        -   Ciascun dispositivo SNMP può avere il proprio nome comunità, ma spesso lo stesso nome comunità viene condiviso tra diversi dispositivi.  

        -   La maggior parte dei dispositivi SNMP hanno il nome comunità predefinito di **Pubblico** che può essere utilizzato se non si conoscono altri nomi comunità. Tuttavia, alcune organizzazioni eliminano il nome comunità **Pubblico** dai propri dispositivi come misura di sicurezza.  

8.  Per configurare il numero massimo di hop router utilizzabili dalle ricerche SNMP, fare clic sulla scheda **SNMP** , quindi nella scheda **SNMP** e selezionare il numero di hop dall'elenco a discesa **Hop massimi** .  

9. Per configurare **Dispositivi SNMP**, fare clic sulla scheda **Dispositivi SNMP** e sulla scheda **SNMP** e fare clic sull'icona **Nuovo** ![icona Nuovo](media/Disc_new_Icon.gif), se il dispositivo non è incluso nell'elenco. Nella finestra di dialogo **Nuovo dispositivo SNMP** , specificare l'indirizzo IP o il nome dispositivo del dispositivo SNMP, quindi fare clic su **OK**.  

    > [!NOTE]  
    >  Se si specifica un nome dispositivo, Configuration Manager deve essere in grado di risolvere il nome NetBIOS in un indirizzo IP.  

10. Per la configurazione dell'individuazione per eseguire la query di server DHCP specifici per client DHCP, fare clic sulla scheda **DHCP** e, nella scheda **DHCP** , configurare una o più delle seguenti opzioni:  

    -   Per eseguire la query del server DHCP sul computer che esegue l'individuazione, selezionare la casella di controllo **Utilizza sempre il server DHCP del server del sito.** .  

        > [!NOTE]  
        >  Per utilizzare questa opzione, il server deve eseguire il lease dell'indirizzo IP da un server DHCP e non utilizzare un indirizzo IP statico.  

    -   Per eseguire la query di un server DHCP specifico, fare clic sull'icona **Nuovo** ![icona Nuovo](media/Disc_new_Icon.gif), quindi nella finestra di dialogo **Nuovo server DHCP** specificare l'indirizzo IP o il nome server del server DHCP e fare clic su **OK**.  

        > [!NOTE]  
        >  Se si specifica un nome server, Configuration Manager deve essere in grado di risolvere il nome NetBIOS in un indirizzo IP.  

11. Per configurare l'esecuzione dell'individuazione, fare clic sulla scheda **Pianificazione** e nella scheda **Pianificazione** fare clic sull'icona **Nuovo** ![icona Nuovo](media/Disc_new_Icon.gif) per impostare una pianificazione per l'esecuzione di individuazione della rete.  

     È possibile configurare più pianificazioni per l'individuazione di rete che includono più pianificazioni ricorrenti e più pianificazioni che non hanno ricorrenza.  

    > [!NOTE]  
    >  Se vengono visualizzate più pianificazioni contemporaneamente nella scheda **Pianifica** , tutte le pianificazioni porteranno a un'esecuzione dell'individuazione di rete come configurata nell'orario indicato nella pianificazione. Questo vale anche per le pianificazioni ricorrenti.  

12. Fare clic su **OK** per salvare le configurazioni.  

###  <a name="a-namebkmkhowtoverifynetdisca-how-to-verify-that-network-discovery-has-finished"></a><a name="BKMK_HowToVerifyNetDisc"></a> Come verificare il completamento dell'individuazione di rete  
 Il tempo che richiede l'individuazione di rete per il completamento può variare a seconda di diversi fattori. Questi fattori possono includere uno o più dei seguenti elementi:  

-   La dimensione della rete  

-   La topologia della rete  

-   Il numero massimo di hop configurati per trovare router nella rete  

-   Il tipo di individuazione che viene eseguita  

Poiché l'individuazione di rete non crea messaggi per avvisare l'utente quando termina l'individuazione stessa, è possibile utilizzare la seguente procedura per verificarne il completamento.  

##### <a name="to-verify-that-network-discovery-has-finished"></a>Per verificare che l'individuazione di rete è terminata  

1.  Nella console di Configuration Manager fare clic su **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** , espandere **Stato del sistema**, quindi fare clic su **Query messaggi di stato**.  

3.  Selezionare **Tutti i messaggi di stato**.  

4.  Nella scheda **Home** , nel gruppo **Query messaggi di stato** , fare clic su **Mostra messaggi**.  

5.  Selezionare l'elenco a discesa **Seleziona data e ora** , quindi selezionare un valore che includa la data e l'ora di inizio dell'individuazione e infine fare clic su **OK** per aprire il **Visualizzatore messaggi di stato di Configuration Manager**.  

    > [!TIP]  
    >  È possibile utilizzare anche l'opzione **Specifica data e ora** per selezionare una data e un'ora specifici per l'esecuzione dell'individuazione. Questa opzione è utile quando si esegue l'individuazione della rete in una determinata data e si desidera recuperare i messaggi solo da tale data.  

6.  Per convalidare il termine dell'individuazione della rete, cercare un messaggio di stato con i seguenti dettagli:  

    -   ID messaggio: **502**  

    -   Componente: **SMS_NETWORK_DISCOVERY**  

    -   Descrizione: **Il componente è stato interrotto**  

    Se questo messaggio di stato non è presente, l'individuazione della rete non è stata completata.  

7.  Per convalidare l'avvio dell'individuazione della rete, cercare un messaggio di stato con i seguenti dettagli:  

    -   ID messaggio: **500**  

    -   Componente: **SMS_NETWORK_DISCOVERY**  

    -   Descrizione: **Il componente è stato avviato**  

    Queste informazioni verificano l'avvio dell'individuazione della rete. Se queste informazioni non sono presenti, ripianificare l'individuazione della rete.  



<!--HONumber=Dec16_HO3-->



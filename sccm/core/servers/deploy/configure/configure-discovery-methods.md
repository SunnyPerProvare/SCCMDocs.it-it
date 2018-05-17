---
title: Configurare l'individuazione
titleSuffix: Configuration Manager
description: Configurare i metodi di individuazione per trovare le risorse da gestire dalla rete, Active Directory e Azure Active Directory.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e7ac10fdc08569e519468633f30548c5c76b5838
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/03/2018
---
# <a name="configure-discovery-methods-for-system-center-configuration-manager"></a>Configurare i metodi di individuazione per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


Configurare i metodi di individuazione per trovare le risorse da gestire dalla rete, Active Directory e Azure Active Directory (Azure AD). Abilitare e configurare i metodi che si vogliono usare per eseguire ricerche nell'ambiente. È anche possibile disabilitare un metodo seguendo la stessa procedura usata per abilitarlo. Le uniche eccezioni a tale procedura sono il metodo di individuazione heartbeat e di individuazione server:  

-   Per impostazione predefinita, l'**individuazione heartbeat** è già abilitata quando si installa un sito primario di Configuration Manager. Viene configurata perché sia eseguita secondo una pianificazione di base. Lasciare l'individuazione heartbeat abilitata. In questo modo si assicura che i record dei dati di individuazione per i dispositivi siano aggiornati. Per altre informazioni sull'individuazione heartbeat, vedere [Informazioni sull'individuazione heartbeat](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat).  

-   L'**individuazione server** è un metodo di individuazione automatica. Individua i computer in uso come sistemi del sito. Non è possibile configurare o disabilitare questo metodo.  

### <a name="enable-a-configurable-discovery-method"></a>Abilitare un metodo di individuazione configurabile  
 > [!NOTE]  
 > Le informazioni seguenti non si applicano all'individuazione utenti di Azure AD. Vedere invece [Configurare l'individuazione utenti di Azure AD](#azureaadisc) più avanti in questo articolo.

1.  Dalla console di Configuration Manager accedere all'area di lavoro **Amministrazione**, espandere **Configurazione della gerarchia** e fare clic su **Metodi di individuazione**.  

2.  Selezionare il metodo di individuazione per il sito in cui si desidera attivare l'individuazione.  

3.  Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**. Nella scheda **Generale** selezionare la casella **Abilita &lt;Metodo di individuazione\>**.  

     Se questa casella è già selezionata, è possibile disabilitare il metodo di individuazione deselezionandola.  

4.  Scegliere **OK** per salvare la configurazione.  



##  <a name="BKMK_ConfigADForestDisc"></a> Configurare l'individuazione foresta Active Directory  
Per completare la configurazione dell'individuazione foresta Active Directory, è necessario configurare le impostazioni in due posizioni:  

-   Nel nodo **Metodi di individuazione** è possibile:

    - Abilitare il metodo di individuazione.
    - Impostare una pianificazione del polling.
    - Determinare se l'individuazione crea automaticamente limiti per le subnet e i siti di Active Directory individuati.  

-   Nel nodo **Foreste Active Directory** è possibile:

    - Aggiungere foreste da individuare.
    - Abilitare l'individuazione di siti e subnet di Active Directory in quella foresta.
    - Configurare impostazioni che consentono ai siti di Configuration Manager di pubblicare le informazioni sul sito nella foresta.
    - Assegnare un account da usare come Account foresta Active Directory per ogni foresta.  

Usare le procedure seguenti per attivare l'individuazione foresta Active Directory e per configurare singole foreste per l'uso con l'individuazione foresta Active Directory.  

#### <a name="to-enable-active-directory-forest-discovery"></a>Per attivare l'individuazione foresta Active Directory  

1.  Nella console di Configuration Manager scegliere **Amministrazione** > **Configurazione della gerarchia** e quindi scegliere **Metodi di individuazione**.  

2.  Selezionare il metodo Individuazione foresta Active Directory per il sito in cui si desidera configurare l'individuazione.  

3.  Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

4.  Nella scheda **Generale** selezionare la casella per abilitare l'individuazione. In alternativa è possibile configurare subito l'individuazione e abilitarla in un secondo momento.  

5.  Specificare le opzioni per creare i limiti del sito per i percorsi individuati.  

6.  Specificare una pianificazione per l'esecuzione dell'individuazione.  

7.  Al termine della configurazione dell'individuazione foresta Active Directory per il sito, scegliere **OK** per salvare la configurazione.  

#### <a name="to-configure-a-forest-for-active-directory-forest-discovery"></a>Per configurare una foresta per l'individuazione foresta Active Directory  

1.  Nell'area di lavoro **Amministrazione** scegliere **Foreste Active Directory**. Se in precedenza è stato eseguito il metodo di individuazione foresta Active Directory, è possibile visualizzare ogni foresta rilevata nel riquadro dei risultati. La foresta locale e qualsiasi foresta trusted vengono individuate durante l'esecuzione del metodo di individuazione foresta Active Directory. È necessario aggiungere manualmente solo le foreste non trusted.  

    -   Per configurare una foresta individuata in precedenza, selezionarla nel riquadro dei risultati. Nel gruppo **Proprietà** della scheda **Home** scegliere **Proprietà** per aprire le proprietà della foresta. Procedere al passaggio 3.  

    -   Per configurare una nuova foresta non presente nell'elenco, nel gruppo **Crea** della scheda **Home** scegliere **Aggiungi foresta** per aprire la finestra di dialogo **Aggiungi foreste**. Procedere al passaggio 3.  

2.  Nella scheda **Generale** completare le configurazioni per la foresta che si vuole individuare e specificare un valore per **Account foresta Active Directory**.  

    > [!NOTE]  
    >  Il metodo di individuazione della foresta Active Directory richiede un account globale per l'individuazione e la pubblicazione in foreste non trusted. Se non si usa l'account computer del server del sito, è possibile selezionare solo un account globale.  

3.  Se si prevede di consentire ai siti di pubblicare i relativi dati in questa foresta, completare le configurazioni per la pubblicazione in questa foresta nella scheda **Pubblicazione**.  

    > [!NOTE]  
    >  Se si consente ai siti di pubblicare in una foresta, è necessario estendere lo schema di Active Directory di tale foresta per Configuration Manager. L'account foresta Active Directory deve disporre delle autorizzazioni di tipo Controllo completo sul contenitore di sistema di tale foresta.  

4.  Al termine della configurazione della foresta per l'uso con l'individuazione della foresta Active Directory, scegliere **OK** per salvare la configurazione.  



##  <a name="BKMK_ConfigADDiscGeneral"></a> Configurare l'individuazione Active Directory per computer, utenti o gruppi  
 Per configurare l'individuazione di computer, utenti o gruppi, seguire le informazioni relative ai metodi di individuazione seguenti, riportate in queste sezioni:  

-   Individuazione gruppo Active Directory  

-   Individuazione sistema Active Directory  

-   individuazione utenti di Active Directory  

> [!NOTE]  
>  Le informazioni contenute in questa sezione non si applicano all'individuazione foresta Active Directory.  

 Anche se ogni metodo di individuazione è indipendente dagli altri, tutti condividono opzioni simili. Per altre informazioni su queste opzioni di configurazione, vedere l'argomento [Opzioni condivise per l'individuazione di gruppi, sistemi e utenti](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_shared).  

> [!WARNING]  
>  Il polling di Active Directory da ciascuno di questi metodi di individuazione può generare notevole traffico di rete. È consigliabile pianificare ogni metodo di individuazione in modo che venga eseguito in un momento in cui il traffico di rete non condizioni negativamente gli usi aziendali della rete.  

#### <a name="to-configure-active-directory-group-discovery"></a>Per configurare l'individuazione gruppo Active Directory  

1.  Nella console di Configuration Manager scegliere **Amministrazione** > **Configurazione della gerarchia** e quindi scegliere **Metodi di individuazione**.  

2.  Scegliere il metodo **Individuazione gruppo Active Directory** per il sito in cui si vuole configurare l'individuazione.  

3.  Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

4.  Nella scheda **Generale** selezionare la casella per abilitare l'individuazione. In alternativa è possibile configurare subito l'individuazione e abilitarla in un secondo momento.  

5.  Scegliere **Aggiungi** per configurare un ambito di individuazione, scegliere **Gruppi** o **Percorso** e quindi completare le configurazioni seguenti nella finestra di dialogo **Aggiungi gruppi**o **Aggiungi percorso di Active Directory**:  

    1.  Specificare un **Nome** per questo ambito di individuazione.  

    2.  Specificare un **Dominio Active Directory** o **Percorso** per la ricerca:  

        -   Se si sceglie **Gruppi**, specificare uno o più gruppi di Active Directory da individuare.  

        -   Se si sceglie **Percorso**, specificare un contenitore Active Directory come percorso da individuare. È anche possibile attivare una ricerca ricorsiva dei contenitori figlio di Active Directory per questo percorso.  

    3.  Specificare l' **Account di individuazione gruppo Active Directory** utilizzato per la ricerca di questo ambito di individuazione.  

    4.  Scegliere **OK** per salvare la configurazione dell'ambito di individuazione.  

6.  Ripetere il passaggio 6 per ogni ambito di individuazione aggiuntivo che si desidera definire.  

7.  Nella scheda **Pianificazione del polling** configurare la pianificazione del polling per l'individuazione completa e l'individuazione differenziale.  

8.  Facoltativamente, nella scheda **Opzioni** è possibile configurare le opzioni per escludere dall'individuazione i record del computer non aggiornati. È anche possibile configurare l'individuazione dell'appartenenza dei gruppi di distribuzione.  

    > [!NOTE]  
    >  Per impostazione predefinita, l'individuazione gruppo Active Directory rileva solo l'appartenenza dei gruppi di sicurezza.  

9. Al termine della configurazione dell'individuazione gruppo Active Directory per questo sito, scegliere **OK** per salvare la configurazione.  

#### <a name="to-configure-active-directory-system-discovery"></a>Per configurare l'individuazione sistema Active Directory  

1.  Nella console di Configuration Manager scegliere **Amministrazione** > **Configurazione della gerarchia** e quindi scegliere **Metodi di individuazione**.  

2.  Selezionare il metodo per il sito in cui si desidera configurare l'individuazione.  

3.  Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

4.  Nella scheda **Generale** selezionare la casella per abilitare l'individuazione. In alternativa è possibile configurare subito l'individuazione e abilitarla in un secondo momento.  

5.  Scegliere l'icona **Nuovo** ![Icona Nuovo](media/Disc_new_Icon.gif) per specificare un nuovo contenitore di Active Directory. Nella finestra di dialogo **Contenitore Active Directory** completare le configurazioni seguenti:  

    1.  Specificare uno o più percorsi in cui eseguire la ricerca.  

    2.  Per ogni percorso, specificare le opzioni che modificano il comportamento di ricerca.  

    3.  Specificare per ogni percorso l'account da utilizzare come **Account di individuazione Active Directory**.  

        > [!TIP]  
        >  Per ogni percorso specificato, è possibile configurare una serie di opzioni di individuazione e un account di individuazione Active Directory univoco.  

    4.  Scegliere **OK** per salvare la configurazione del contenitore Active Directory.  

6.  Nella scheda **Pianificazione del polling** configurare la pianificazione del polling per l'individuazione completa e l'individuazione differenziale.  

7.  Facoltativamente, nella scheda **Attributi di Active Directory** è possibile configurare attributi aggiuntivi di Active Directory per i computer che si desidera individuare. Sono inoltre elencati gli attributi oggetto predefiniti.  

     > [!Tip]  
     > Ad esempio, l'organizzazione usa l'attributo **Description** nell'account computer in Active Directory. Fare clic su **Personalizza** e aggiungere `Description` come attributo personalizzato. Quando il metodo di individuazione viene eseguito, questo attributo viene visualizzato nella scheda delle proprietà del dispositivo nella console di Configuration Manager.<!--513948-->

8.  Facoltativamente, nella scheda **Opzioni** è possibile configurare le opzioni per escludere, tramite un filtro, dall'individuazione i record del computer non aggiornati.  

9. Al termine della configurazione dell'individuazione sistema Active Directory per questo sito, scegliere **OK** per salvare la configurazione.  

#### <a name="to-configure-active-directory-user-discovery"></a>Per configurare l'individuazione utente Active Directory  

1.  Nella console di Configuration Manager scegliere **Amministrazione** > **Configurazione della gerarchia** e quindi scegliere **Metodi di individuazione**.  

2.  Scegliere il metodo **Individuazione utente Active Directory** per il sito in cui si vuole configurare l'individuazione.  

3.  Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

4.  Nella scheda **Generale** selezionare la casella per abilitare l'individuazione. In alternativa è possibile configurare subito l'individuazione e abilitarla in un secondo momento.  

5.  Scegliere l'icona **Nuovo** ![Icona Nuovo](media/Disc_new_Icon.gif) per specificare un nuovo contenitore di Active Directory. Nella finestra di dialogo **Contenitore Active Directory** completare le configurazioni seguenti:  

    1.  Specificare uno o più percorsi in cui eseguire la ricerca.  

    2.  Per ogni percorso, specificare le opzioni che modificano il comportamento di ricerca.  

    3.  Specificare per ogni percorso l'account da utilizzare come **Account di individuazione Active Directory**.  

        > [!NOTE]  
        >  Per ogni percorso specificato, è possibile configurare un'unica serie di opzioni di individuazione e un account di individuazione Active Directory univoco.  

    4.  Scegliere **OK** per salvare la configurazione del contenitore Active Directory.  

6.  Nella scheda **Pianificazione del polling** configurare la pianificazione del polling per l'individuazione completa e l'individuazione differenziale.  

7.  Facoltativamente, nella scheda **Attributi di Active Directory** è possibile configurare attributi aggiuntivi di Active Directory per i computer che si desidera individuare. Sono inoltre elencati gli attributi oggetto predefiniti.  

8.  Al termine della configurazione dell'individuazione utente Active Directory per questo sito, scegliere **OK** per salvare la configurazione.  



## <a name="azureaadisc"></a>Configurare l'individuazione utenti di Azure AD
L'individuazione utenti di AD Azure non viene abilitata o configurata come altri metodi di individuazione. È necessario configurarla durante il caricamento del sito di Configuration Manager in Azure AD. È anche possibile abilitare e configurare questo metodo di individuazione durante la [configurazione dei servizi Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) per la **gestione cloud**. 

Durante la configurazione del servizio di Azure **Gestione cloud**: 
- Nella pagina **Individuazione** della procedura guidata fare clic su **Abilita l'individuazione utente di Azure Active Directory**. 
- Fare clic su **Impostazioni**. 
- Nella finestra di dialogo Impostazioni dell'individuazione utenti di Azure AD configurare una pianificazione per l'esecuzione dell'individuazione. È anche possibile abilitare l'individuazione differenziale che verifica solo gli account nuovi o modificati in Azure AD. 

Per altre informazioni, vedere [Individuazione utenti di Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).

 > [!Important]  
 > Prima di *importare* l'app Azure AD in Configuration Manager, è necessario concedere l'autorizzazione delle applicazioni server per la lettura dei dati della directory da Azure AD. 
 >  - Accedere al pannello [Azure Active Directory](https://portal.azure.com) dal **portale di Azure**. 
 >  - Fare clic su **Registrazioni per l'app** e passare a **Tutte le app**, se necessario. 
 >  - Selezionare l'app server di tipo *App Web / API*, quindi fare clic su **Impostazioni**. 
 >  - Fare clic su **Autorizzazioni necessarie**, quindi selezionare **Concedi autorizzazioni**.
 >  
 > Se si *crea* l'app server da Configuration Manager, Azure AD genera automaticamente le autorizzazioni insieme all'applicazione. È comunque necessario concedere il consenso all'applicazione nel portale di Azure.

 > [!Note]  
 > Se l'utente è un'identità federata o sincronizzata, è necessario usare l'[individuazione utente Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser) di Configuration Manager nonché l'individuazione utenti di Azure AD. Per altre informazioni sulle identità ibride, vedere [Definire una strategia di adozione della soluzione ibrida di gestione delle identità](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->



##  <a name="BKMK_ConfigHBDisc"></a> Configurare l'individuazione heartbeat  
 Per impostazione predefinita, l'individuazione heartbeat è abilitata quando si installa un sito primario di Configuration Manager. È quindi necessario configurare solo la pianificazione della frequenza di invio dei record dei dati di individuazione heartbeat a un punto di gestione da parte dei client quando non si vuole usare la frequenza predefinita di sette giorni.  

> [!NOTE]  
>  Se l'installazione push del client e l'attività di gestione del sito per **Cancella flag di installazione** sono attivati nello stesso sito, impostare la pianificazione dell'individuazione heartbeat in modo che sia inferiore al valore **Periodo nuova individuazione client** dell'attività di gestione del sito **Cancella flag di installazione** . Per altre informazioni sulle attività di manutenzione del sito, vedere [Attività di manutenzione per System Center Configuration Manager](../../../../core/servers/manage/maintenance-tasks.md).  

#### <a name="to-configure-the-heartbeat-discovery-schedule"></a>Per configurare la pianificazione dell'individuazione heartbeat  

1.  Nella console di Configuration Manager scegliere **Amministrazione** > **Configurazione della gerarchia** e quindi scegliere **Metodi di individuazione**.  

2.  Scegliere **Individuazione heartbeat** per il sito in cui si vuole eseguire l'individuazione heartbeat.  

3.  Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

4.  Configurare la frequenza con cui i client inviano i record dei dati di individuazione heartbeat, quindi scegliere **OK** per salvare la configurazione.  



##  <a name="BKMK_ConfigNetworkDisc"></a> Configurare l'individuazione di rete  
 Seguire le informazioni nelle sezioni riportate di seguito per configurare l'individuazione della rete.  

###  <a name="BKMK_AboutConfigNetworkDisc"></a> Informazioni sulla configurazione dell'individuazione di rete  
 Prima di configurare l'individuazione della rete, è necessario conoscere i concetti seguenti:  

-   Livelli disponibili per l'individuazione della rete  

-   Opzioni disponibili per l'individuazione della rete  

-   Applicazione di limiti all'individuazione della rete in rete  

Per altre informazioni, vedere [Informazioni sull'individuazione di rete](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutNetwork).  

 Nelle sezioni seguenti vengono fornite informazioni sulle configurazioni comuni per l'individuazione della rete. È possibile definire una o più di queste configurazioni per l'utilizzo durante la stessa esecuzione dell'individuazione. Se si utilizzano più configurazioni, sarà necessario considerare le interazioni che possono influenzare i risultati dell'individuazione.  

 Ad esempio, è possibile individuare tutti i dispositivi SNMP (Simple Network Management Protocol) che usano uno specifico nome di comunità SNMP. Per la stessa esecuzione dell'individuazione, è inoltre possibile disattivare l'individuazione in una subnet specifica. Durante l'esecuzione dell'individuazione, l'individuazione della rete non rileva i dispositivi SNMP con il nome community specificato nella subnet disabilitata.  

####  <a name="BKMK_DetermineNetTopology"></a> Determinare la topologia di rete  
 Per eseguire il mapping della rete, è possibile utilizzare un'individuazione solo per topologia. Questo tipo di individuazione non rileva i potenziali client. L'individuazione di rete solo per topologia si basa su SNMP.  

 Quando si esegue il mapping della topologia di rete, è necessario configurare gli **Hop massimi** nella scheda **SNMP** nella finestra di dialogo **Proprietà dell'individuazione della rete**. Con solo pochi hop è possibile controllare la larghezza di banda di rete che viene utilizzata quando viene eseguita l'individuazione. Man mano che l'individuazione di rete avanza, è possibile aumentare il numero di hop per ottenere una migliore comprensione della topologia di rete.  

 Dopo aver compreso la topologia della rete, è possibile configurare proprietà aggiuntive per l'individuazione della rete per individuare potenziali client e i relativi sistemi operativi, mentre si usano le configurazioni disponibili per limitare i segmenti della rete in cui l'individuazione della rete può eseguire la ricerca.  

####  <a name="BKMK_LimitBySubnet"></a> Limitare le ricerche mediante subnet  
 È possibile configurare l'individuazione di rete per effettuare la ricerca in subnet specifiche durante un ciclo di individuazione. Per impostazione predefinita, l'individuazione di rete effettua la ricerca nella subnet del server che esegue l'individuazione. Eventuali altre subnet configurate e abilitate si applicano esclusivamente alle opzioni di ricerca SNMP e DHCP (Dynamic Host Configuration Protocol). Per la ricerca nei domini, l'individuazione della rete non è limitata dalle configurazioni per subnet.  

 Se si specificano una o più subnet nella scheda **Subnet** della finestra di dialogo **Proprietà dell'individuazione della rete** , la ricerca viene effettuata solo nelle subnet che sono contrassegnate con **Attivato** .  

 Quando si disabilita una subnet, essa viene esclusa dall'individuazione e vengono applicate le condizioni seguenti:  

-   Le query basate su SNMP non vengono eseguite sulla subnet.  

-   I server DHCP non rispondono con un elenco di risorse che si trovano nella subnet.  

-   Le query basate su dominio possono individuare risorse che si trovano nella subnet.  

####  <a name="BKMK_SearchByDomain"></a> Eseguire ricerche in un dominio specifico  
 È possibile configurare l'individuazione di rete per effettuare la ricerca in un dominio specifico o in un insieme di domini durante l'esecuzione dell'individuazione. Per impostazione predefinita, l'individuazione di rete effettua la ricerca nel dominio locale del server che esegue l'individuazione.  

 Se si specificano uno o più domini nella scheda **Domini** della finestra di dialogo **Proprietà dell'individuazione della rete** , viene effettuata la ricerca solo nei domini che sono contrassegnati con **Attivato** .  

 Quando si disabilita un dominio, esso viene escluso dall'individuazione e vengono applicate le condizioni seguenti:  

-   L'individuazione di rete non esegue una query sui controller di dominio nel dominio.  

-   Le query basate su SNMP possono comunque essere eseguite sulle subnet in quel dominio.  

-   I server DHCP possono comunque rispondere con un elenco di risorse presenti nel dominio.  

####  <a name="BKMK_LimitBySNMPname"></a> Limitare le ricerche usando i nomi comunità SNMP  
 L'individuazione di rete viene configurata per effettuare la ricerca in una comunità SNMP specifica o in un insieme di comunità durante l'esecuzione dell'individuazione. Per impostazione predefinita, è configurato per l'utilizzo il nome comunità di **Pubblico** .  

 L'individuazione di rete utilizza i nomi comunità per accedere ai router che sono dispositivi SNMP. Un router può fornire l'individuazione di rete con informazioni su altri router e subnet che sono collegati al primo router.  

> [!NOTE]  
>  I nomi comunità SNMP sono simili alle password. L'individuazione della rete può ottenere informazioni solo da un dispositivo SNMP per il quale è stato specificato un nome community. Ciascun dispositivo SNMP può avere il proprio nome comunità, ma spesso lo stesso nome comunità viene condiviso tra diversi dispositivi. Inoltre, la maggior parte dei dispositivi SNMP hanno un nome comunità predefinito, cioè **Pubblico**. Alcune organizzazioni, però, eliminano il nome comunità **pubblico** dai propri dispositivi come misura di sicurezza.  

 Se nella scheda **SNMP** della finestra di dialogo **Individuazione di rete - Proprietà** vengono visualizzate più community SNMP, l'individuazione della rete esegue la ricerca in queste community nell'ordine in cui compaiono. Per ridurre al minimo il traffico di rete generato dai tentativi di contattare un dispositivo utilizzando nomi diversi, assicurarsi che i nomi utilizzati più di frequente appaiano nella parte superiore dell'elenco.  

> [!NOTE]  
>  Oltre a usare il nome community SNMP, è possibile specificare l'indirizzo IP o il nome risolvibile di un dispositivo SNMP specifico. Questa operazione può essere eseguita nella scheda **Dispositivi SNMP** della finestra di dialogo **Individuazione di rete - Proprietà**.  

####  <a name="BKMK_SearchByDHCP"></a> Eseguire ricerche in un server DHCP specifico  
 È possibile configurare l'individuazione di rete per l'utilizzo di un server DHCP specifico o di più server per individuare i client DHCP durante l'esecuzione dell'individuazione.  

 L'individuazione di rete effettua la ricerca in ogni server DHCP specificato nella scheda **DHCP** della finestra di dialogo **Proprietà dell'individuazione della rete** . Se il server che sta eseguendo l'individuazione esegue il lease dell'indirizzo IP da un server DHCP, è possibile configurare l'individuazione per effettuare la ricerca in quel server DHCP selezionando la casella **Includi il server DHCP per il cui utilizzo è configurato il server di sito**.  

> [!NOTE]  
>  Per configurare correttamente un server DHCP nell'individuazione di rete, l'ambiente deve supportare IPv4. Non è possibile configurare l'individuazione della rete per usare un server DHCP in un ambiente IPv6 nativo.  

###  <a name="BKMK_HowToConfigNetDisc"></a> Come configurare l'individuazione di rete  
 Utilizzare le seguenti procedure per individuare in primo luogo la topologia di rete, quindi per configurare l'individuazione di rete e individuare potenziali client utilizzando una o più delle opzioni di individuazione di rete disponibili.  

##### <a name="to-determine-your-network-topology"></a>Per determinare la topologia di rete  

1.  Nella console di Configuration Manager scegliere **Amministrazione** > **Configurazione della gerarchia** e quindi scegliere **Metodi di individuazione**.  

2.  Selezionare **Individuazione di rete** per il sito in cui si vuole eseguire l'individuazione di rete.  

3.  Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

    -   Nella scheda **Generale** selezionare la casella **Abilita individuazione della rete** e quindi scegliere **Topologia** nelle opzioni **Tipo di individuazione**.  

    -   Nella scheda **Subnet** selezionare la casella **Cerca subnet locali**.  

        > [!TIP]  
        >  Se si conoscono le subnet specifiche che costituiscono la rete, deselezionare la casella **Cerca subnet locali**. A questo punto, usare l'icona **Nuovo** ![Icona Nuovo](media/Disc_new_Icon.gif) per aggiungere le subnet specifiche che si vogliono cercare. Per reti di grandi dimensioni, spesso è meglio eseguire la ricerca solo in una o due subnet alla volta per ridurre al minimo l'uso della larghezza di banda di rete.  

    -   Nella scheda **Domini** selezionare la casella **Cerca dominio locale**.  

    -   Nella scheda **SNMP** , utilizzare l'elenco a discesa **Hop massimi** per specificare quanti hop router può prendere l'individuazione di rete nel mapping della topologia.  

        > [!TIP]  
        >  Quando si esegue per la prima volta la topologia di rete, configurare un numero limitato di hop router per ridurre al minimo l'utilizzo della larghezza di banda di rete.  

4.  Nella scheda **Pianifica** scegliere l'icona **Nuovo** ![Icona Nuovo](media/Disc_new_Icon.gif) per impostare una pianificazione per l'esecuzione dell'individuazione di rete.  

    > [!NOTE]  
    >  Non è possibile assegnare una configurazione di individuazione diversa per separare le varie pianificazioni di individuazione della rete. Ogni volta che viene eseguita l'individuazione di rete, essa utilizza la configurazione di individuazione corrente.  

5.  Scegliere **OK** per accettare le configurazioni. L'individuazione di rete viene eseguita all'orario specificato.  

##### <a name="to-configure-network-discovery"></a>Per configurare l'individuazione di rete  

1.  Nella console di Configuration Manager scegliere **Amministrazione** > **Configurazione della gerarchia** e quindi scegliere **Metodi di individuazione**.  

2.  Selezionare **Individuazione di rete** per il sito in cui si vuole eseguire l'individuazione di rete.  

3.  Nella scheda **Home**, nel gruppo **Proprietà**, fare clic su **Proprietà**.  

4.  Nella scheda **Generale** selezionare la casella di controllo **Abilita individuazione della rete** e quindi selezionare il tipo di individuazione che si vuole eseguire nelle opzioni **Tipo di individuazione**.  

5.  Per configurazione l'individuazione in modo da effettuare la ricerca nelle subnet, scegliere la scheda **Subnet** e quindi configurare una o più delle opzioni seguenti:  

    -   Per eseguire l'individuazione sulle subnet locali per il computer che esegue l'individuazione, selezionare la casella **Cerca subnet locali**.  

    -   Per effettuare la ricerca in una subnet specifica, verificare che la subnet sia inclusa nell'elenco in **Subnet da cercare** e che il valore **Cerca** sia impostato su **Attivato**:  

        1.  Se la subnet non compare in elenco, scegliere l'icona **Nuovo** ![Icona Nuovo](media/Disc_new_Icon.gif). Nella finestra di dialogo **Nuova assegnazione subnet** immettere le informazioni **Subnet** e **Mask**, quindi scegliere **OK**. Per impostazione predefinita, una nuova subnet è abilitata per la ricerca.  

        2.  Per modificare il valore **Cerca** per una subnet presente in elenco, selezionare la subnet, quindi scegliere l'icona **Mostra/Nascondi** per impostare il valore su **Disattivato** o **Attivato**.  

6.  Per configurazione l'individuazione in modo da effettuare la ricerca nei domini, scegliere la scheda **Domini** e quindi configurare una o più delle opzioni seguenti:  

    -   Per eseguire l'individuazione sul dominio del computer che esegue l'individuazione, selezionare la casella **Cerca dominio locale**.  

    -   Per effettuare la ricerca in un dominio specifico, verificare che il dominio sia incluso nell'elenco in **Domini** e che il valore **Cerca** sia impostato su **Attivato**:  

        1.  Se il dominio non compare in elenco, scegliere l'icona **Nuovo** ![Icona Nuovo](media/Disc_new_Icon.gif). Nella finestra di dialogo **Proprietà dominio** immettere le informazioni sul **Dominio** e quindi scegliere **OK**. Per impostazione predefinita, un nuovo dominio è abilitato per la ricerca.  

        2.  Per modificare il valore **Cerca** per un dominio presente in elenco, selezionare il dominio e quindi fare clic sull'icona **Mostra/Nascondi** per impostare il valore su **Disattivato** o **Attivato**.  

7.  Per configurare l'individuazione in modo da cercare dispositivi SNMP in specifici nomi comunità SNMP, scegliere la scheda **SNMP** e quindi configurare una o più delle opzioni seguenti:  

    -   Per aggiungere un nome comunità SNMP all'elenco **Nomi comunità SNMP**, scegliere l'icona **Nuovo** ![Icona Nuovo](media/Disc_new_Icon.gif). Nella finestra di dialogo **Nuovo nome comunità SNMP** specificare il **Nome** della comunità SNMP e quindi scegliere **OK**.  

    -   Per rimuovere un nome comunità SNMP, selezionarlo e quindi scegliere l'icona **Elimina** ![Icona Elimina](media/Disc_delete_Icon.gif).  

    -   Per modificare l'ordine di ricerca dei nomi comunità SNMP, selezionare un nome comunità e quindi scegliere l'icona **Sposta elemento in alto**![Icona Sposta su](media/Disc_moveUp_Icon.gif) oppure l'icona **Sposta elemento in basso** ![Icona Sposta giù](media/Disc_moveDown_Icon.gif). Quando viene eseguita l'individuazione, viene effettuata la ricerca nei nomi comunità seguendo un ordine dall'alto in basso. Tenere presente quanto segue.

        > [!NOTE]  
        >  L'individuazione di rete utilizza i nomi comunità SNMP per accedere ai router che sono dispositivi SNMP. Un router può informare l'individuazione di rete su altri router e subnet collegati al primo router.  

        -   I nomi comunità SNMP sono simili alle password.  

        -   L'individuazione di rete può ottenere informazioni solo da un dispositivo SNMP per il quale è stato specificato un nome comunità.  

        -   Ciascun dispositivo SNMP può avere il proprio nome comunità, ma spesso lo stesso nome comunità viene condiviso tra diversi dispositivi.  

        -   La maggior parte dei dispositivi SNMP ha un nome comunità predefinito, ovvero **Pubblico**. È possibile usarlo se non si conoscono altri nomi comunità. Tuttavia, alcune organizzazioni eliminano il nome comunità **Pubblico** dai propri dispositivi come misura di sicurezza.  

8.  Per configurare il numero massimo di hop router utilizzabili dalle ricerche SNMP, scegliere la scheda **SNMP** e quindi selezionare il numero di hop nell'elenco a discesa **Hop massimi**.  

9. Per configurare un dispositivo SNMP, scegliere la scheda **Dispositivi SNMP**. Se il dispositivo non compare in elenco, scegliere l'icona **Nuovo** ![Icona Nuovo](media/Disc_new_Icon.gif). Nella finestra di dialogo **Nuovo dispositivo SNMP** specificare l'indirizzo IP o il nome dispositivo del dispositivo SNMP e quindi scegliere **OK**.  

    > [!NOTE]  
    >  Se si specifica un nome dispositivo, Configuration Manager deve essere in grado di risolvere il nome NetBIOS in un indirizzo IP.  

10. Per configurare l'individuazione in modo da eseguire una query su specifici server DHCP per i client DHCP, scegliere la scheda **DHCP** e quindi configurare una o più delle opzioni seguenti:  

    -   Per eseguire la query sul server DHCP nel computer che esegue l'individuazione, scegliere di **usare sempre il server DHCP del server del sito**.  

        > [!NOTE]  
        >  Per usare questa opzione, il server deve eseguire il lease dell'indirizzo IP da un server DHCP e non può usare un indirizzo IP statico.  

    -   Per eseguire la query su un server DHCP specifico, scegliere l'icona **Nuovo** ![Icona Nuovo](media/Disc_new_Icon.gif). Nella finestra di dialogo **Nuovo server DHCP** specificare l'indirizzo IP o il nome server del server DHCP e quindi scegliere **OK**.  

        > [!NOTE]  
        >  Se si specifica un nome server, Configuration Manager deve essere in grado di risolvere il nome NetBIOS in un indirizzo IP.  

11. Per configurare l'orario di esecuzione dell'individuazione, scegliere la scheda **Pianificazione** e quindi scegliere l'icona **Nuovo** ![Icona Nuovo](media/Disc_new_Icon.gif) per impostare una pianificazione per l'esecuzione dell'individuazione di rete.  

     È possibile configurare più pianificazioni ricorrenti e più pianificazioni che non hanno ricorrenza.  

    > [!NOTE]  
    >  Se vengono visualizzate più pianificazioni contemporaneamente nella scheda **Pianificazione**, tutte le pianificazioni porteranno a un'esecuzione dell'individuazione di rete come configurata nell'orario indicato nella pianificazione. Questo vale anche per le pianificazioni ricorrenti.  

12. Scegliere **OK** per salvare le configurazioni.  

###  <a name="BKMK_HowToVerifyNetDisc"></a> Come verificare il completamento dell'individuazione di rete  
 Il tempo necessario per il completamento dell'individuazione della rete può variare in base a uno o più dei fattori seguenti:  

-   La dimensione della rete  

-   La topologia della rete  

-   Il numero massimo di hop configurati per trovare router nella rete  

-   Il tipo di individuazione che viene eseguita  

Poiché l'individuazione della rete non crea messaggi per avvisare l'utente quando è terminata, è possibile usare la procedura seguente per verificarne il completamento.  

##### <a name="to-verify-that-network-discovery-has-finished"></a>Per verificare che l'individuazione di rete è terminata  

1.  Nella console di Configuration Manager scegliere **Monitoraggio**.  

2.  Nell'area di lavoro **Monitoraggio** espandere **Stato del sistema** e quindi scegliere **Query messaggi di stato**.  

3.  Scegliere **Tutti i messaggi di stato**.  

4.  Nel gruppo **Query messaggi di stato** della scheda **Home** scegliere **Mostra messaggi**.  

5.  Nell'elenco a discesa **Seleziona data e ora** selezionare un valore che includa il tempo trascorso dall'inizio dell'individuazione e infine scegliere **OK** per aprire il **Visualizzatore messaggi di stato di Configuration Manager**.  

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

---
title: Configurare l&quot;amministrazione basata su ruoli | Microsoft Docs
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 57413dd3-b2f8-4a5f-b27f-8464d357caff
caps.latest.revision: 7
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: fb5a3cb9fc5aebf512f09a2e584c1eee58b2d15a


---
# <a name="configure-role-based-administration-for-system-center-configuration-manager"></a>Configurare l'amministrazione basata su ruoli per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager l'amministrazione basata su ruoli combina ruoli di sicurezza, ambiti di protezione e raccolte assegnate per definire l'ambito amministrativo per ogni utente amministratore. L'ambito amministrativo comprende gli oggetti che possono essere visualizzati da un utente amministratore nella console di Configuration Manager, nonché le attività relative a tali oggetti eseguibili dall'utente amministratore. Le configurazioni dell'amministrazione basata su ruoli vengono applicate a tutti i siti della gerarchia.  

 Se non si ha ancora familiarità con i concetti dell'amministrazione basata su ruoli, vedere [Nozioni fondamentali di amministrazione basata su ruoli per System Center Configuration Manager](../../../../core/understand/fundamentals-of-role-based-administration.md)  

 Le informazioni contenute nelle seguenti procedure consentono di creare e configurare l'amministrazione basata su ruoli e le relative impostazioni di sicurezza.  

-   [Creare ruoli di sicurezza personalizzati](#BKMK_CreateSecRole)  

-   [Configurare i ruoli di sicurezza](#BKMK_ConfigSecRole)  

-   [Configurare gli ambiti di protezione per un oggetto](#BKMK_ConfigSecScope)  

-   [Configurare le raccolte per la gestione della sicurezza](#BKMK_ConfigColl)  

-   [Creare un nuovo utente amministratore](#BKMK_Create_AdminUser)  

-   [Modificare l'ambito amministrativo di un utente amministratore](#BKMK_ModAdminUser)  

##  <a name="a-namebkmkcreatesecrolea-create-custom-security-roles"></a><a name="BKMK_CreateSecRole"></a> Creare ruoli di sicurezza personalizzati  
 Configuration Manager fornisce diversi ruoli di sicurezza predefiniti. Se sono necessari ruoli di sicurezza aggiuntivi, è possibile creare un ruolo di sicurezza personalizzato creando una copia di un ruolo di sicurezza esistente e, in seguito, modificando tale copia. È possibile creare un ruolo di sicurezza personalizzato per concedere agli utenti amministratori le autorizzazioni di sicurezza necessarie non incluse in un ruolo di sicurezza attualmente assegnato. Utilizzando un ruolo di sicurezza personalizzato, è possibile concedere soltanto le autorizzazioni richieste, evitando di assegnare un ruolo di sicurezza che conceda più autorizzazioni del necessario.  

 Utilizzare la seguente procedura per creare un nuovo ruolo di sicurezza utilizzando un ruolo di sicurezza esistente come modello.  

#### <a name="to-create-custom-security-roles"></a>Per creare ruoli di sicurezza personalizzati  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Sicurezza**e quindi fare clic su **Ruoli di protezione**.  

     Per creare il nuovo ruolo di sicurezza, utilizzare uno dei seguenti processi:  

    -   Per creare un nuovo ruolo di sicurezza personalizzato, eseguire le seguenti azioni:  

        1.  Selezionare un ruolo di sicurezza esistente da utilizzare come origine per il nuovo ruolo di sicurezza.  

        2.  Nella scheda **Home** , nel gruppo **Ruolo di protezione** , fare clic su **Copia**. Viene creata una copia del ruolo di sicurezza di origine.  

        3.  Nella procedura guidata Copia ruolo di protezione, specificare un **Nome** per il nuovo ruolo di sicurezza personalizzato.  

        4.  In **Assegnazioni operazioni di protezione**, espandere ciascun nodo **Operazioni di protezione** per visualizzare le azioni disponibili.  

        5.  Per modificare l'impostazione per un'operazione di protezione, fare clic sull'elenco a discesa nella colonna **Valore** , quindi selezionare **Sì** o **No**.  

            > [!CAUTION]  
            >  Quando viene configurato un ruolo di sicurezza personalizzato, è necessario non concedere autorizzazioni non richieste dagli utenti amministratori associati al nuovo ruolo di sicurezza. Il valore **Modifica** per l'operazione di protezione **Ruoli di protezione** , ad esempio, concede agli utenti amministratori l'autorizzazione per la modifica di qualsiasi ruolo di sicurezza accessibile, anche se tali utenti non sono associati a quello specifico ruolo di sicurezza.  

        6.  Dopo la configurazione delle autorizzazioni, fare clic su **OK** per salvare il nuovo ruolo di sicurezza.  

    -   Per importare un ruolo di sicurezza esportato da un altra gerarchia di Configuration Manager, eseguire le azioni seguenti:  

        1.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Importa ruolo di protezione**.  

        2.  Specificare il file XML contenente la configurazione del ruolo di sicurezza da importare, quindi fare clic su **Apri** per completare la procedura e salvare il ruolo di sicurezza.  

            > [!NOTE]  
            >  Dopo l'importazione di un ruolo di sicurezza, è possibile modificare le proprietà del ruolo di sicurezza per modificare le autorizzazioni oggetto associate al ruolo di sicurezza.  

##  <a name="a-namebkmkconfigsecrolea-configure-security-roles"></a><a name="BKMK_ConfigSecRole"></a> Configurare i ruoli di sicurezza  
 I gruppi di autorizzazioni di sicurezza definiti per un ruolo di sicurezza vengono chiamati assegnazioni delle operazioni di protezione. Le assegnazioni delle operazioni di protezione rappresentano una combinazione di tipi di oggetti e azioni disponibili per ciascun tipo di oggetto. È possibile modificare le operazioni di protezione disponibili per ogni ruolo di sicurezza personalizzato, mentre non è possibile modificare i ruoli di sicurezza predefiniti forniti da Configuration Manager.  

 Utilizzare la seguente procedura per modificare le operazioni di protezione per un ruolo di sicurezza.  

#### <a name="to-modify-security-roles"></a>Per modificare i ruoli di sicurezza  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Sicurezza**e quindi fare clic su **Ruoli di protezione**.  

3.  Selezionare il ruolo di sicurezza personalizzato che si desidera modificare.  

4.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

5.  Fare clic sulla scheda **Autorizzazioni** .  

6.  In **Assegnazioni operazioni di protezione**, espandere ciascun nodo **Operazioni di protezione** per visualizzare le azioni disponibili.  

7.  Per modificare l'impostazione per un'operazione di protezione, fare clic sull'elenco a discesa nella colonna **Valore** , quindi selezionare **Sì** o **No**.  

    > [!CAUTION]  
    >  Quando viene configurato un ruolo di sicurezza personalizzato, è necessario non concedere autorizzazioni non richieste dagli utenti amministratori associati al nuovo ruolo di sicurezza. Il valore **Modifica** per l'operazione di protezione **Ruoli di protezione** , ad esempio, concede agli utenti amministratori l'autorizzazione per la modifica di qualsiasi ruolo di sicurezza accessibile, anche se tali utenti non sono associati a quello specifico ruolo di sicurezza.  

8.  Al termine della configurazione delle assegnazioni delle operazioni di protezione, fare clic su **OK** per salvare il nuovo ruolo di sicurezza.  

##  <a name="a-namebkmkconfigsecscopea-configure-security-scopes-for-an-object"></a><a name="BKMK_ConfigSecScope"></a> Configurare gli ambiti di protezione per un oggetto  
 Per gestire l'associazione di un ambito di protezione per un oggetto dall'oggetto anziché dall'ambito di protezione. Le uniche configurazioni dirette supportate dagli ambiti di protezione sono le modifiche apportate al nome e alla descrizione. Per modificare il nome e la descrizione di un ambito di protezione durante la visualizzazione delle proprietà dell'ambito di protezione, è necessario disporre dell'autorizzazione **Modifica** per l'oggetto a protezione diretta **Ambiti di protezione** .  

 Quando viene creato un nuovo oggetto in Configuration Manager, questo viene associato a ogni ambito di protezione associato ai ruoli di sicurezza dell'account usato per creare l'oggetto se i ruoli di sicurezza consentono l'autorizzazione **Crea** o **Imposta ambito di protezione**. Solo dopo la creazione dell'oggetto è possibile modificare gli ambiti di protezione a cui è associato.  

 Se, ad esempio, all'utente viene assegnato un ruolo di sicurezza che concede l'autorizzazione per creare un nuovo gruppo di limiti, Quando viene creato un nuovo gruppo di limiti, non esiste nessuna opzione a cui è possibile assegnare ambiti di protezione specifici. Gli ambiti di protezione disponibili relativamente ai ruoli di sicurezza a cui è associato l'utente vengono invece assegnati automaticamente al nuovo gruppo di limiti. Dopo aver salvato il nuovo gruppo di limiti, è possibile modificare gli ambiti di protezione associati al nuovo gruppo di limiti.  

 Utilizzare la seguente procedura per configurare gli ambiti di protezione assegnati a un oggetto.  

#### <a name="to-configure-security-scopes-for-an-object"></a>Per configurare gli ambiti di protezione per un oggetto  

1.  Nella console di Configuration Manager selezionare un oggetto che supporta l'assegnazione a un ambito di protezione.  

2.  Nella scheda **Home** , nel gruppo **Classificazione** , fare clic su **Imposta ambiti di protezione**.  

3.  Nella finestra di dialogo **Imposta ambiti di protezione** selezionare o deselezionare gli ambiti di protezione a cui è associato l'oggetto. Ogni oggetto che supporta gli ambiti di protezione deve essere assegnato almeno a un ambito di protezione.  

4.  Fare clic su **OK** per salvare gli ambiti di protezione assegnati.  

    > [!NOTE]  
    >  Quando viene creato un nuovo oggetto, è possibile assegnare l'oggetto a più ambiti di protezione. Per modificare il numero di ambiti di protezione associati all'oggetto, è necessario modificare l'assegnazione dopo la creazione dell'oggetto.  

##  <a name="a-namebkmkconfigcolla-configure-collections-to-manage-security"></a><a name="BKMK_ConfigColl"></a> Configurare le raccolte per la gestione della sicurezza  
 Non esistono procedure per la configurazione delle raccolte per l'amministrazione basata su ruoli. Le raccolte non dispongono di una configurazione dell'amministrazione basata su ruoli. Le raccolte vengono invece assegnate a un utente amministratore durante la configurazione dell'utente amministratore. Le operazioni di protezione della raccolta abilitate nei ruoli di sicurezza assegnati degli utenti determinano di quali autorizzazioni dispone un utente amministratore per le raccolte e le risorse delle raccolte (membri delle raccolte).  

 Quando un utente amministratore dispone delle autorizzazioni per una raccolta, dispone anche delle autorizzazioni per le raccolte limitate alla raccolta specifica. Se ad esempio l'organizzazione utilizza una raccolta denominata All Desktops ed esiste una raccolta denominata All North America Desktops limitata alla raccolta All Desktops e un utente amministratore dispone delle autorizzazioni per All Desktops, egli dispone delle stesse autorizzazioni anche per la raccolta All North America Desktops. Inoltre, un utente amministratore non è in grado di utilizzare l'autorizzazione **Elimina** o **Modifica** per la raccolta che gli è stata direttamente assegnata, ma può utilizzare tali autorizzazioni per le raccolte limitate alla raccolta specifica. Secondo l'esempio precedente, l'utente amministratore può eliminare o modificare la raccolta All North America Desktops, mentre non può eliminare o modificare la raccolta All Desktops.  

##  <a name="a-namebkmkcreateadminusera-create-a-new-administrative-user"></a><a name="BKMK_Create_AdminUser"></a> Creare un nuovo utente amministratore  
 Per consentire l'accesso a individui o membri di un gruppo di sicurezza per gestire Configuration Manager, creare un utente amministratore in Configuration Manager e specificare l'account Windows Utente o Gruppo utenti. È necessario assegnare a ogni utente amministratore in Configuration Manager almeno un ruolo di sicurezza e un ambito di protezione. È inoltre possibile assegnare delle raccolte per limitare l'ambito amministrativo dell'utente amministratore.  

 Utilizzare le seguenti procedure per creare nuovi utenti amministratori.  

#### <a name="to-create-a-new-administrative-user"></a>Per creare un nuovo utente amministratore  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Sicurezza**e quindi fare clic su **Utenti amministratori**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Aggiungi utente o gruppo**.  

4.  Fare clic su **Sfoglia** e quindi selezionare l'account utente o il gruppo da utilizzare per il nuovo utente amministratore.  

    > [!NOTE]  
    >  Per l'amministrazione basata su console, è possibile specificare solo utenti di dominio o gruppi di sicurezza come utente amministratore.  

5.  Per **Ruoli di protezione assegnati**fare clic su **Aggiungi** per aprire un elenco dei ruoli di sicurezza disponibili, selezionare la casella di controllo per uno o più ruoli e quindi fare clic su **OK**.  

6.  Selezionare una delle seguenti due opzioni per definire il comportamento degli oggetti a protezione diretta per il nuovo utente:  

    -   **Tutte le istanze degli oggetti collegati ai ruoli di protezione assegnati**: questa opzione associa l'utente amministratore all'ambito di protezione **Tutto** e alle raccolte predefinite a livello radice per **Tutti i sistemi**e **Tutti gli utenti e i gruppi di utenti** . I ruoli di sicurezza assegnati all'utente definiscono l'accesso agli oggetti. I nuovi oggetti creati dall'utente amministratore vengono assegnati all'ambito di protezione **Predefinito** .  

    -   **Solo le istanze di oggetti assegnati alle raccolte o agli ambiti di protezione specificati**: per impostazione predefinita, questa opzione associa l'utente amministratore all'ambito di protezione **Predefinito** e alle raccolte **Tutti i sistemi** e **Tutti gli utenti e i gruppi di utenti** . Tuttavia, le raccolte e gli ambiti di protezione effettivi sono limitati a quelli associati all'account utilizzato per creare il nuovo utente amministratore. Questa opzione supporta l'aggiunta o la rimozione di raccolte e ambiti di protezione per personalizzare l'ambito amministrativo dell'utente amministratore.  

    > [!IMPORTANT]  
    >  Le opzioni precedenti associano ogni raccolta e ambito di protezione assegnati a ogni ruolo di sicurezza assegnato all'utente amministratore. È possibile utilizzare una terza opzione, **Associa ruoli di protezione assegnati a raccolte e ambiti di protezione specifici**, per associare singoli ruoli di sicurezza a raccolte e ambiti di protezione specifici. Questa terza opzione è disponibile dopo aver creato il nuovo utente amministratore, quando si modifica l'utente amministratore.  

7.  A seconda dell'opzione selezionata nel passaggio 6, eseguire le seguenti operazioni:  

    -   Se si è selezionato **Tutte le istanze degli oggetti collegati ai ruoli di protezione assegnati**, fare clic su **OK** per completare questa procedura.  

    -   Se si è selezionato **Solo le istanze di oggetti assegnati alle raccolte o agli ambiti di protezione specificati**, è possibile fare clic su **Aggiungi** per selezionare raccolte e ambiti di protezione aggiuntivi oppure selezionare uno o più oggetti nell'elenco e quindi fare clic su **Rimuovi** per rimuoverli. Fare clic su **OK** per completare questa procedura.  

##  <a name="a-namebkmkmodadminusera-modify-the-administrative-scope-of-an-administrative-user"></a><a name="BKMK_ModAdminUser"></a> Modificare l'ambito amministrativo di un utente amministratore  
 È possibile modificare l'ambito amministrativo di un utente amministratore aggiungendo o rimuovendo raccolte, ruoli di sicurezza e ambiti di protezione associati all'utente. È necessario associare a ogni utente amministratore almeno un ruolo di sicurezza e un ambito di protezione. Potrebbe essere necessario assegnare una o più raccolte all'ambito amministrativo dell'utente. La maggior parte dei ruoli di sicurezza interagisce con le raccolte e non funziona correttamente senza una raccolta assegnata.  

 Quando si modifica un utente amministratore, è possibile modificare il comportamento di associazione degli oggetti a protezione diretta ai ruoli di sicurezza assegnati. Di seguito, i tre comportamenti che è possibile selezionare:  

-   **Tutte le istanze degli oggetti collegati ai ruoli di protezione assegnati**: questa opzione associa l'utente amministratore all'ambito **Tutto** e alle raccolte predefinite a livello radice per **Tutti i sistemi**e **Tutti gli utenti e i gruppi di utenti**. I ruoli di sicurezza assegnati all'utente definiscono l'accesso agli oggetti.  

-   **Solo le istanze di oggetti assegnati alle raccolte o agli ambiti di protezione specificati**: questa opzione associa l'utente amministratore agli stessi ambiti di sicurezza e collezioni associate all'account usato per configurare l'utente amministratore. Questa opzione supporta l'aggiunta o la rimozione di raccolte e ruoli di sicurezza per personalizzare l'ambito amministrativo dell'utente amministratore.  

-   **Associa ruoli di sicurezza assegnati a raccolte e ambiti di protezione specifici**: questa opzione consente di creare associazioni specifiche tra i singoli ruoli di sicurezza e gli ambiti di protezione e le raccolte specifici per l'utente.  

    > [!NOTE]  
    >  Questa opzione è disponibile solo quando si modificano le proprietà di un utente amministratore.  

La configurazione corrente per il comportamento degli oggetti a protezione diretta modifica il processo utilizzato per assegnare i ruoli di sicurezza aggiuntivi. Utilizzare le seguenti procedure basate sulle diverse opzioni per gli oggetti a protezione diretta per gestire un utente amministratore.  

 Utilizzare la seguente procedura per visualizzare e gestire la configurazione per gli oggetti a protezione diretta per un utente amministratore:  

#### <a name="to-view-and-manage-the-securable-object-behavior-for-an-administrative-user"></a>Per visualizzare e gestire il comportamento degli oggetti a protezione diretta per un utente amministratore  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Sicurezza**e quindi fare clic su **Utenti amministratori**.  

3.  Selezionare l'utente amministratore che si desidera modificare.  

4.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

5.  Fare clic sulla scheda **Ambiti di protezione** per visualizzare la configurazione corrente per gli oggetti a protezione diretta per questo utente amministratore.  

6.  Per modificare il comportamento degli oggetti a protezione diretta, selezionare una nuova opzione per il comportamento di tali oggetti. Dopo aver modificato questa configurazione, fare riferimento alla procedura appropriata per ulteriori informazioni sulla configurazione di raccolte, ambiti di protezione e ruoli di sicurezza per l'utente amministratore.  

7.  Fare clic su **OK** per completare la procedura.  

 Utilizzare la seguente procedura per modificare un utente amministrativo con il comportamento degli oggetti a protezione diretta impostato su **Tutte le istanze degli oggetti collegati ai ruoli di protezione assegnati**:  

#### <a name="option-all-securable-objects-that-are-relevant-to-their-associated-security-roles"></a>Opzione: Tutte le istanze degli oggetti collegati ai ruoli di sicurezza assegnati  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Sicurezza**e quindi fare clic su **Utenti amministratori**.  

3.  Selezionare l'utente amministratore che si desidera modificare.  

4.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

5.  Fare clic sulla scheda **Ambiti di protezione** per confermare che l'utente amministratore sia configurato per **Tutte le istanze degli oggetti collegati ai ruoli di protezione assegnati**.  

6.  Per modificare i ruoli di sicurezza assegnati, fare clic sulla scheda **Ruoli di protezione** .  

    -   Per assegnare ruoli di sicurezza aggiuntivi all'utente amministratore, fare clic su **Aggiungi**, selezionare la casella di controllo per ogni ruolo di sicurezza aggiuntivo da assegnare e quindi fare clic **OK**.  

    -   Per rimuovere i ruoli di sicurezza, selezionare uno o più ruoli di sicurezza dall'elenco e quindi fare clic su **Rimuovi**.  

7.  Per modificare il comportamento degli oggetti a protezione diretta, fare clic sulla scheda **Ambiti di protezione** e selezionare una nuova opzione per il comportamento di tali oggetti. Dopo aver modificato questa configurazione, fare riferimento alla procedura appropriata per ulteriori informazioni sulla configurazione di raccolte, ambiti di protezione e ruoli di sicurezza per l'utente amministratore.  

    > [!NOTE]  
    >  Quando il comportamento degli oggetti a protezione diretta viene impostato su **Tutte le istanze degli oggetti collegati ai ruoli di protezione assegnati**, è impossibile aggiungere o rimuovere raccolte e ambiti di protezione specifici.  

8.  Fare clic su **OK** per completare questa procedura.  

 Utilizzare la seguente procedura per modificare un utente amministratore con il comportamento degli oggetti a protezione diretta impostato su **Solo le istanze di oggetti assegnati alle raccolte o agli ambiti di protezione specificati**.  

#### <a name="option-only-securable-objects-in-specified-security-scopes-or-collections"></a>Opzione: Solo le istanze di oggetti assegnati alle raccolte o agli ambiti di protezione specificati  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Sicurezza**e quindi fare clic su **Utenti amministratori**.  

3.  Selezionare l'utente amministratore che si desidera modificare.  

4.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

5.  Fare clic sulla scheda **Ambiti di protezione** per confermare che l'utente amministratore sia configurato per **Solo le istanze di oggetti assegnati alle raccolte o agli ambiti di protezione specificati**.  

6.  Per modificare i ruoli di sicurezza assegnati, fare clic sulla scheda **Ruoli di protezione** .  

    -   Per assegnare ruoli di sicurezza aggiuntivi all'utente amministratore, fare clic su **Aggiungi**, selezionare la casella di controllo per ogni ruolo di sicurezza aggiuntivo da assegnare e quindi fare clic **OK**.  

    -   Per rimuovere i ruoli di sicurezza, selezionare uno o più ruoli di sicurezza dall'elenco e quindi fare clic su **Rimuovi**.  

7.  Per modificare le raccolte e gli ambiti di protezione associati ai ruoli di sicurezza, fare clic sulla scheda **Ambiti di protezione** .  

    -   Per associare nuovi ambiti di protezione o raccolte ai ruoli di sicurezza assegnati all'utente amministratore, fare clic su **Aggiungi** e selezionare una delle quattro opzioni. Se si seleziona **Ambito di protezione** o **Raccolta**, selezionare la casella di controllo per uno o più oggetti per completare la selezione e quindi fare clic su **OK**.  

    -   Per rimuovere un ambito di protezione o una raccolta, selezionare l'oggetto e quindi fare clic su **Rimuovi**.  

8.  Fare clic su **OK** per completare questa procedura.  

 Utilizzare la seguente procedura per modificare un utente amministratore con il comportamento degli oggetti a protezione diretta impostato su **Associa ruoli di protezione assegnati a raccolte e ambiti di protezione specifici**.  

#### <a name="option-only-securable-objects-as-determined-by-the-security-roles-of-the-administrative-user"></a>Opzione: Associa ruoli di sicurezza assegnati a raccolte e ambiti di protezione specifici  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Sicurezza**e quindi fare clic su **Utenti amministratori**.  

3.  Selezionare l'utente amministratore che si desidera modificare.  

4.  Nella scheda **Home** , nel gruppo **Proprietà** , fare clic su **Proprietà**.  

5.  Fare clic sulla scheda **Ambiti di protezione** per confermare che l'utente amministratore sia configurato per **Solo le istanze di oggetti assegnati alle raccolte o agli ambiti di protezione specificati**.  

6.  Per modificare i ruoli di sicurezza assegnati, fare clic sulla scheda **Ruoli di protezione** .  

    -   Per assegnare ruoli di sicurezza aggiuntivi all'utente amministratore, fare clic su **Aggiungi**. Nella finestra di dialogo **Aggiungi ruolo di protezione** selezionare uno o più ruoli di sicurezza disponibili, fare clic su **Aggiungi**e selezionare un tipo di oggetto da associare ai ruoli di sicurezza selezionati. Se si seleziona **Ambito di protezione** o **Raccolta**, selezionare la casella di controllo per uno o più oggetti per completare la selezione e quindi fare clic su **OK**.  

        > [!NOTE]  
        >  È necessario configurare almeno un ambito di protezione prima di assegnare i ruoli di sicurezza selezionati all'utente amministratore. Quando si selezionano più ruoli di sicurezza, tutte le raccolte e gli ambiti di protezione configurati vengono associati a ogni ruolo di sicurezza selezionato.  

    -   Per rimuovere i ruoli di sicurezza, selezionare uno o più ruoli di sicurezza dall'elenco e quindi fare clic su **Rimuovi**.  

7.  Per modificare le raccolte e gli ambiti di protezione associati a un ruolo di sicurezza specifico, fare clic sulla scheda **Ambiti di protezione** selezionare il ruolo di sicurezza e quindi fare clic su **Modifica**.  

    -   Per associare nuovi oggetti a questo ruolo di sicurezza, fare clic su **Aggiungi**e quindi selezionare il tipo di oggetto da associare ai ruoli selezionati. Se si seleziona **Ambito di protezione** o **Raccolta**, selezionare la casella di controllo per uno o più oggetti per completare la selezione e quindi fare clic su **OK**.  

        > [!NOTE]  
        >  È necessario configurare almeno un ambito di protezione.  

    -   Per rimuovere una raccolta o un ambito di protezione associato al ruolo di sicurezza, selezionare l'oggetto e quindi fare clic su **Rimuovi**.  

    -   Dopo aver completato la modifica degli oggetti associati, fare clic su **OK**.  

8.  Fare clic su **OK** per completare questa procedura.  

    > [!CAUTION]  
    >  Quando un ruolo di sicurezza concede agli utenti amministratori l'autorizzazione per la distribuzione di raccolte, questi utenti possono distribuire oggetti da ogni ambito di protezione per cui dispongono dell'autorizzazione di **lettura** , anche se tale ambito è associato a un ruolo diverso.  



<!--HONumber=Dec16_HO3-->



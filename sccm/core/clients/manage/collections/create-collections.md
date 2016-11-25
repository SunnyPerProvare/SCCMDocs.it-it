---
title: Creare raccolte | System Center Configuration Manager
description: "Creare raccolte in System Center Configuration Manager per gestire più facilmente gruppi di utenti e dispositivi."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
caps.latest.revision: 6
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: f73f0e58b82d1aab1f64f3695dd5c3a61e933d2a


---
# <a name="how-to-create-collections-in-system-center-configuration-manager"></a>Come creare le raccolte in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

È possibile creare raccolte in System Center Configuration Manager per rappresentare raggruppamenti logici di utenti o dispositivi. Le raccolte possono essere usate per molte attività, tra cui gestione delle applicazioni, distribuzione delle impostazioni di conformità o installazione degli aggiornamenti software. È anche possibile usare le raccolte per gestire gruppi di impostazioni client o con l'amministrazione basata sui ruoli per specificare le risorse accessibili per un utente amministratore. Configuration Manager contiene varie raccolte predefinite. Per altre informazioni, vedere [Introduzione alle raccolte in System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).  

> [!NOTE]  
>  Una singola raccolta può contenere utenti o dispositivi, ma non entrambi.  

 Nella tabella seguente sono elencate le regole che è possibile usare per configurare i membri di una raccolta in Configuration Manager.  

|Tipo di regola di appartenenza|Altre informazioni|  
|--------------------------|----------------------|  
|Regola diretta|Le regole dirette consentono di scegliere gli utenti o i computer da aggiungere come membri di una raccolta. Questa regola offre il controllo diretto delle risorse che fanno parte della raccolta. Questa appartenenza non cambia a meno che una risorsa non venga rimossa da Configuration Manager. Prima di poter aggiungere le risorse a una raccolta con regole dirette, è necessario importarle o che vengano individuate da Configuration Manager. Le raccolte con regole dirette presentano un maggiore carico amministrativo rispetto alle raccolte con regole di query, perché è necessario apportare manualmente le modifiche a questo tipo di raccolta.|  
|Regola di query|Le regole di query aggiornano in modo dinamico l'appartenenza di una raccolta con una query eseguita da Configuration Manager in base a una pianificazione. Ad esempio, è possibile creare una raccolta degli utenti membri dell'unità organizzativa Risorse umane in Servizi di dominio Active Directory. Diversamente dalle raccolte con regole dirette, le appartenenze vengono aggiornate automaticamente in seguito all'aggiunta o alla rimozione di utenti nell'unità organizzativa Risorse umane.<br /><br /> Per alcuni esempi di query da usare per creare raccolte, vedere [Come creare query in System Center Configuration Manager](../../../../core/servers/manage/create-queries.md).|  
|Regola di inclusione raccolte|Le regole di inclusione raccolte consentono di includere i membri di un'altra raccolta in una raccolta di Configuration Manager. Le appartenenze della raccolta corrente vengono aggiornate in base a una pianificazione in caso di modifica delle appartenenze della raccolta inclusa.<br /><br /> È possibile aggiungere più regole di inclusione raccolte in una raccolta.<br />              **Esempio:** si crea una raccolta che con due regole di inclusione raccolte. La prima regola di inclusione raccolte è relativa a una raccolta di portatili e la seconda è per una raccolta di desktop. La nuova raccolta conterrà tutti i membri della raccolta dei portatili e della raccolta dei desktop.|  
|Regola di esclusione raccolte|Le regole di esclusione raccolte consentono di escludere i membri di un'altra raccolta da una raccolta di Configuration Manager. Le appartenenze della raccolta corrente vengono aggiornate in base a una pianificazione in caso di modifica delle appartenenze della raccolta esclusa.<br /><br /> È possibile aggiungere più regole di esclusione raccolte in una raccolta. Se una raccolta include sia regole di inclusione raccolte che di esclusione raccolte e si verifica un conflitto, la regola di esclusione raccolte ha la priorità sulla regola di inclusione.<br />              **Esempio:** si crea una raccolta con una regola di inclusione raccolte e una di esclusione raccolte. La regola di inclusione è relativa a una raccolta di desktop Dell. La regola di esclusione è per una raccolta di computer con meno di 4 GB di RAM. La nuova raccolta conterrà i desktop Dell con almeno 4 GB di RAM.|  

 Usare le procedure seguenti per creare le raccolte in Configuration Manager. È anche possibile importare le raccolte create in questo o in altro sito di Configuration Manager. Per informazioni sull'esportazione di raccolte, vedere [Come gestire le raccolte in System Center Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md).  

 Per informazioni sulla creazione di raccolte per i computer che eseguono Linux e UNIX, vedere [Come gestire i client per i server Linux e UNIX in System Center Configuration Manager](../../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md).  

##  <a name="a-namebkmk1a-to-create-a-device-collection"></a><a name="BKMK_1"></a> Per creare una raccolta di dispositivi  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Raccolte dispositivi**.  

3.  Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea raccolta dispositivi**.  

4.  Nella pagina **Generale** della **Creazione guidata raccolta dispositivi**specificare le informazioni seguenti:  

    -   **Nome**: specificare un nome univoco per la raccolta.  

    -   **Commento**: specificare una descrizione per la raccolta.  

    -   **Raccolta di limitazione**: fare clic su **Sfoglia** per selezionare una raccolta di limitazione. La raccolta che si sta creando conterrà solo i membri della raccolta di limitazione.  

5.  Nella pagina **Regole di appartenenza** della **Creazione guidata raccolta dispositivi**specificare le informazioni seguenti:  

    -   Nell'elenco **Aggiungi regola** selezionare il tipo di regola di appartenenza che si vuole usare per questa raccolta. È possibile configurare più regole per ogni raccolta.  

         Usare le procedure seguenti per configurare ogni tipo di regola di appartenenza.  

        ##### <a name="to-configure-a-direct-rule"></a>Per configurare una regola diretta  

        1.  Nella pagina **Cerca risorse** della **Creazione guidata regola di appartenenza diretta**specificare le informazioni seguenti:  

            -   **Classe di risorse**: selezionare nell'elenco il tipo di risorsa che si vuole cercare e aggiungere alla raccolta. Selezionare un valore in **Risorsa di sistema** per cercare i dati di inventario restituiti dai computer client o **Computer sconosciuti** per effettuare una selezione tra i valori restituiti dai computer sconosciuti.  

            -   **Nome attributo**: selezionare nell'elenco l'attributo associato alla classe di risorse selezionata che si vuole cercare. Ad esempio, per selezionare i computer in base al relativo nome NetBIOS, selezionare **Risorsa di sistema** nell'elenco **Classe di risorse** e **Nome NetBIOS** nell'elenco **Nome attributo** .  

            -   **Escludere le risorse contrassegnate come obsolete**: se un computer client è contrassegnato come obsoleto, non includere questo valore nei risultati della ricerca.  

            -   **Escludere le risorse in cui non è installato il client di Configuration Manager**: se i risultati della ricerca includono una risorsa in cui non è installato un client di Configuration Manager, questo valore non verrà visualizzato nei risultati della ricerca.  

            -   **Valore:** immettere un valore per il quale si vuole cercare il nome di attributo selezionato. È possibile usare il simbolo di percentuale **%** come carattere jolly. Ad esempio, per cercare i computer con un nome NetBIOS che inizia con "M", immettere **M%** in questo campo.  

        2.  Nella pagina **Seleziona risorse** della **Creazione guidata regola di appartenenza diretta**selezionare le risorse da aggiungere alla raccolta nell'elenco **Risorse** e quindi fare clic su **Avanti**.  

        3.  Completare la **Creazione guidata regola di appartenenza diretta**.  

        ##### <a name="to-configure-a-query-rule"></a>Per configurare una regola di query  

        1.  Nella finestra di dialogo **Proprietà regola di query** specificare le informazioni seguenti:  

            -   **Nome**: specificare un nome univoco per la regola di query.  

            -   **Importa istruzione query**: apre la finestra di dialogo **Sfoglia query** nella quale è possibile selezionare una query di Configuration Manager da usare come regola di query per la raccolta. Per ulteriori informazioni su come creare queste query e alcuni esempi, vedere [Come creare query in System Center Configuration Manager](../../../../core/servers/manage/create-queries.md).  

            -   **Classe di risorse:** selezionare nell'elenco il tipo di risorsa che si vuole cercare e aggiungere alla raccolta. Selezionare un valore in **Risorsa di sistema** per cercare i dati di inventario restituiti dai computer client o **Computer sconosciuto** per effettuare una selezione tra i valori restituiti dai computer sconosciuti.  

            -   **Modifica istruzione query**: apre la finestra di dialogo **Proprietà istruzione query** nella quale è possibile creare una query da usare come regola per la raccolta. Per altre informazioni sulle query, vedere [Riferimento tecnico per le query per System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

        2.  Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà regola di query** e salvare la regola di appartenenza di query.  

        ##### <a name="to-configure-an-include-collection-rule"></a>Per configurare una regola di inclusione raccolte  

        1.  Nella finestra di dialogo **Seleziona raccolte** selezionare le raccolte da includere nella nuova raccolta.  

        2.  Fare clic su **OK** per chiudere la finestra di dialogo **Seleziona raccolte** e salvare la regola di appartenenza di inclusione.  

        ##### <a name="to-configure-an-exclude-collection-rule"></a>Per configurare una regola di esclusione raccolte  

        1.  Nella finestra di dialogo **Seleziona raccolte** selezionare le raccolte da escludere dalla nuova raccolta.  

        2.  Fare clic su **OK** per chiudere la finestra di dialogo **Seleziona raccolte** e salvare la regola di appartenenza di esclusione.  

    -   **Utilizza aggiornamenti incrementali per questa raccolta**: selezionare questa opzione per eseguire periodicamente una scansione per verificare la disponibilità di risorse nuove o modificate rispetto alla valutazione raccolta precedente e per aggiornare l'appartenenza alla raccolta solo con queste risorse, indipendentemente da una valutazione raccolta completa. Gli aggiornamenti incrementali vengono eseguiti a intervalli di 10 minuti.  

        > [!IMPORTANT]  
        >  Le raccolte configurate tramite le regole di query che usano le classi seguenti non supportano gli aggiornamenti incrementali:  
        >   
        >  -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (per raccolte di soli utenti)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (per raccolte di soli utenti)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    -   **Pianifica un aggiornamento completo in questa raccolta**: selezionare questa opzione per pianificare una regolare valutazione completa dell'appartenenza alla raccolta.  

6.  Completare la procedura guidata per creare la nuova raccolta. La nuova raccolta viene visualizzata nel nodo **Raccolte dispositivi** dell'area di lavoro **Asset e conformità** .  

> [!NOTE]  
>  È necessario aggiornare o ricaricare la console di Configuration Manager per visualizzare i membri della raccolta. Tuttavia, i membri non compariranno nella raccolta fino a dopo il primo aggiornamento pianificato o fino a quando non si seleziona manualmente **Aggiorna appartenenza** per la raccolta. A seconda della complessità della regola per la raccolta e del numero di voci nel database di Configuration Manager, l'aggiornamento della raccolta può richiedere alcuni minuti.  

##  <a name="a-namebkmk2a-to-create-a-user-collection"></a><a name="BKMK_2"></a> Per creare una raccolta utenti  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Raccolte utenti**.  

3.  Nella scheda **Home** nel gruppo **Crea** fare clic su **Crea raccolta utenti**.  

4.  Nella pagina **Generale** della **Creazione guidata raccolta utenti**specificare le informazioni seguenti:  

    -   **Nome**: specificare un nome univoco per la raccolta.  

    -   **Commento**: specificare una descrizione per la raccolta.  

    -   **Raccolta di limitazione**: fare clic su **Sfoglia** per selezionare una raccolta di limitazione. La raccolta che si sta creando conterrà solo i membri della raccolta di limitazione.  

5.  Nella pagina **Regole di appartenenza** della **Creazione guidata raccolta utenti**specificare le informazioni seguenti:  

    -   Nell'elenco **Aggiungi regola** selezionare il tipo di regola di appartenenza che si vuole usare per questa raccolta. È possibile configurare più regole per ogni raccolta.  

         Usare le procedure seguenti per configurare ogni tipo di regola di appartenenza.  

        ##### <a name="to-configure-a-direct-rule"></a>Per configurare una regola diretta  

        1.  Nella pagina **Cerca risorse** della **Creazione guidata regola di appartenenza diretta**specificare le informazioni seguenti:  

            -   **Classe di risorse**: selezionare nell'elenco il tipo di risorsa che si vuole cercare e aggiungere alla raccolta. Effettuare una selezione tra i valori **Risorsa utente** per cercare le informazioni sugli utenti raccolte da Configuration Manager o in **Risorsa gruppo utenti** per cercare le informazioni sui gruppi di utenti raccolte da Configuration Manager.  

            -   **Nome attributo**: selezionare nell'elenco l'attributo associato alla classe di risorse selezionata che si vuole cercare. Ad esempio, per selezionare gli utenti in base al nome dell'unità organizzativa (OU), selezionare **Risorsa utente** nell'elenco **Classe di risorse** e **Nome unità organizzativa utente** nell'elenco **Nome attributo** .  

            -   **Valore:** immettere un valore per il quale si vuole cercare il nome di attributo selezionato. È possibile usare il simbolo di percentuale **%** come carattere jolly. Ad esempio, per cercare gli utenti nell'unità organizzativa Contoso, immettere **Contoso** in questo campo.  

        2.  Nella pagina **Seleziona risorse** della **Creazione guidata regola di appartenenza diretta**selezionare le risorse da aggiungere alla raccolta nell'elenco **Risorse** e quindi fare clic su **Avanti**.  

        3.  Completare la **Creazione guidata regola di appartenenza diretta**.  

        ##### <a name="to-configure-a-query-rule"></a>Per configurare una regola di query  

        1.  Nella finestra di dialogo **Proprietà regola di query** specificare le informazioni seguenti:  

            -   **Nome**: specificare un nome univoco per la regola di query.  

            -   **Importa istruzione query**: apre la finestra di dialogo **Sfoglia query** nella quale è possibile selezionare una query di Configuration Manager da usare come regola di query per la raccolta. Per altre informazioni sulle query, vedere [Riferimento tecnico per le query per System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

            -   **Classe di risorse**: selezionare nell'elenco il tipo di risorsa che si vuole cercare e aggiungere alla raccolta. Effettuare una selezione tra i valori **Risorsa utente** per cercare le informazioni sugli utenti raccolte da Configuration Manager o in **Risorsa gruppo utenti** per cercare le informazioni sui gruppi di utenti raccolte da Configuration Manager.  

            -   **Modifica istruzione query**: apre la finestra di dialogo **Proprietà istruzione query** nella quale è possibile creare una query da usare come regola per la raccolta. Per altre informazioni sulle query, vedere [Riferimento tecnico per le query per System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

        2.  Fare clic su **OK** per chiudere la finestra di dialogo **Proprietà regola di query** e salvare la regola di appartenenza di query.  

        ##### <a name="to-configure-an-include-collection-rule"></a>Per configurare una regola di inclusione raccolte  

        1.  Nella finestra di dialogo **Seleziona raccolte** selezionare le raccolte da includere nella nuova raccolta.  

        2.  Fare clic su **OK** per chiudere la finestra di dialogo **Seleziona raccolte** e salvare la regola di appartenenza di inclusione.  

        ##### <a name="to-configure-an-exclude-collection-rule"></a>Per configurare una regola di esclusione raccolte  

        1.  Nella finestra di dialogo **Seleziona raccolte** selezionare le raccolte da escludere dalla nuova raccolta.  

        2.  Fare clic su **OK** per chiudere la finestra di dialogo **Seleziona raccolte** e salvare la regola di appartenenza di esclusione.  

    -   **Utilizza aggiornamenti incrementali per questa raccolta**: selezionare questa opzione per eseguire periodicamente una scansione per verificare la disponibilità di risorse nuove o modificate rispetto alla valutazione raccolta precedente e per aggiornare l'appartenenza alla raccolta solo con queste risorse, indipendentemente da una valutazione raccolta completa. Gli aggiornamenti incrementali vengono eseguiti a intervalli di 10 minuti.  

        > [!IMPORTANT]  
        >  Le raccolte configurate tramite le regole di query che usano le classi seguenti non supportano gli aggiornamenti incrementali:  
        >   
        >  -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (per raccolte di soli utenti)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (per raccolte di soli utenti)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    -   **Pianifica un aggiornamento completo in questa raccolta**: selezionare questa opzione per pianificare una regolare valutazione completa dell'appartenenza alla raccolta.  

6.  Completare la procedura guidata per creare la nuova raccolta. La nuova raccolta viene visualizzata nel nodo **Raccolte utenti** dell'area di lavoro **Asset e conformità** .  

> [!NOTE]  
>  È necessario aggiornare o ricaricare la console di Configuration Manager per visualizzare i membri della raccolta. Tuttavia, i membri non compariranno nella raccolta fino a dopo il primo aggiornamento pianificato o fino a quando non si seleziona manualmente **Aggiorna appartenenza** per la raccolta. A seconda della complessità della regola per la raccolta e del numero di voci nel database di Configuration Manager, l'aggiornamento della raccolta può richiedere alcuni minuti.  

##  <a name="a-namebkmk3a-to-import-a-collection"></a><a name="BKMK_3"></a> Per importare una raccolta  

1.  Nella console di Configuration Manager fare clic su **Asset e conformità**.  

2.  Nell'area di lavoro **Asset e conformità** fare clic su **Raccolte utenti** o su **Raccolte dispositivi**.  

3.  Nella scheda **Home** , nel gruppo **Crea** , fare clic su **Importa raccolte**.  

4.  Nella pagina **Generale** dell' **Importazione guidata raccolte**fare clic su **Avanti**.  

5.  Nella pagina **Nome file MOF** fare clic su **Sfoglia** e quindi individuare il file MOF che contiene le informazioni sulla raccolta da importare.  

    > [!NOTE]  
    >  Il file che si vuole importare deve essere stato esportato da un sito che esegue la stessa versione di Configuration Manager di quello corrente. Per ulteriori informazioni sull'esportazione di raccolte, vedere [Come gestire le raccolte in System Center Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md).  

6.  Completare la procedura guidata per importare la raccolta. La nuova raccolta viene visualizzata nel nodo **Raccolte utenti** o **Raccolte dispositivi** dell'area di lavoro **Asset e conformità** .  

> [!NOTE]  
>  È necessario aggiornare o ricaricare la console di Configuration Manager per visualizzare i membri della raccolta appena importata.  



<!--HONumber=Nov16_HO1-->



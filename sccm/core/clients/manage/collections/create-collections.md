---
title: Creare raccolte
titleSuffix: Configuration Manager
description: Creare raccolte in Configuration Manager per gestire più facilmente gruppi di utenti e dispositivi.
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 40cb1a96771181b395ec2f628e0f0c3c2efe29b7
ms.sourcegitcommit: 53f2380ac67025fb4a69fc1651edad15d98e0cdd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2019
ms.locfileid: "65673306"
---
# <a name="how-to-create-collections-in-configuration-manager"></a>Come creare raccolte in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le raccolte costituiscono raggruppamenti di utenti o dispositivi. Usare le raccolte per attività quali gestione delle applicazioni, distribuzione delle impostazioni di conformità o installazione degli aggiornamenti software. È anche possibile usare le raccolte per gestire gruppi di impostazioni client o con l'amministrazione basata sui ruoli per specificare le risorse accessibili per un utente amministratore. Configuration Manager contiene varie raccolte predefinite. Per altre informazioni, vedere [Introduction to Collections](/sccm/core/clients/manage/collections/introduction-to-collections) (Introduzione alle raccolte).  

> [!NOTE]  
> Una raccolta può contenere utenti o dispositivi, ma non entrambi.  


Usare questo articolo per informazioni su come creare le raccolte in Configuration Manager. È anche possibile importare le raccolte create in questo o in altro sito di Configuration Manager. Per altre informazioni su come esportare e importare le raccolte, vedere [Come gestire le raccolte](/sccm/core/clients/manage/collections/manage-collections).  



## <a name="collection-rules"></a>Regole delle raccolte

Ci sono diverse regole che è possibile usare per configurare i membri di una raccolta in Configuration Manager.  


### <a name="direct-rule"></a>Regola diretta

Consente di scegliere gli utenti o i computer da aggiungere a una raccolta. L'appartenenza non cambia a meno che non si rimuova una risorsa da Configuration Manager. Prima di poter aggiungere le risorse a una raccolta con regola diretta, è necessario che vengano individuate da Configuration Manager oppure che siano state importate. Le raccolte con regole dirette presentano un maggiore carico amministrativo rispetto alle raccolte con regole di query, dal momento che richiedono modifiche manuali.


### <a name="query-rule"></a>Regola di query

Consente di aggiornare in modo dinamico l'appartenenza di una raccolta con una query eseguita da Configuration Manager in base a una pianificazione. Ad esempio, è possibile creare una raccolta degli utenti membri dell'unità organizzativa Risorse umane in Servizi di dominio Active Directory. Questa raccolta viene aggiornata automaticamente in seguito all'aggiunta o alla rimozione di utenti nell'unità organizzativa Risorse umane.

Per esempi di query che è possibile usare per creare raccolte, vedere [Come creare query](/sccm/core/servers/manage/create-queries).


### <a name="device-category-rule"></a>Regola categoria di dispositivi

È possibile semplificare la gestione dei dispositivi associando le categorie di dispositivi alle raccolte di dispositivi. 

Per altre informazioni, vedere [Classificare automaticamente i dispositivi in raccolte](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections).<!-- SCCMDocs issue 552 -->


### <a name="include-collection-rule"></a>Regola di inclusione raccolte

È possibile includere i membri di un'altra raccolta in una raccolta di Configuration Manager. Se la raccolta inclusa cambia, Configuration Manager aggiorna l'appartenenza della raccolta corrente in base a una pianificazione.

È possibile aggiungere più regole di inclusione raccolte in una raccolta.


### <a name="exclude-collection-rule"></a>Regola di esclusione raccolte

Le regole di esclusione raccolte consentono di escludere i membri di un'altra raccolta da una raccolta di Configuration Manager. Se la raccolta esclusa cambia, Configuration Manager aggiorna l'appartenenza della raccolta corrente in base a una pianificazione.

È possibile aggiungere più regole di esclusione raccolte in una raccolta. Se una raccolta include sia regole di inclusione raccolte che di esclusione raccolte e si verifica un conflitto, la regola di esclusione raccolte ha la priorità.

#### <a name="example"></a>Esempio
si crea una raccolta con una regola di inclusione raccolte e una di esclusione raccolte. La regola di inclusione è relativa a una raccolta di desktop Dell. La regola di esclusione è relativa a una raccolta di computer con meno di 4 GB di RAM. La nuova raccolta contiene i desktop Dell con almeno 4 GB di RAM.



## <a name="bkmk_create"></a> Creare una raccolta  

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**.  

    - Per creare una *raccolta di dispositivi*, selezionare il nodo **Raccolte dispositivi**. Nel gruppo **Crea** della scheda **Home** della barra multifunzione scegliere quindi **Crea raccolta dispositivi**.  

    - Per creare una *raccolta di utenti*, selezionare il nodo **Raccolte utenti**. Nel gruppo **Crea** della scheda **Home** della barra multifunzione scegliere quindi **Crea raccolta utenti**.  

2. Nella pagina **Generale** della procedura guidata inserire **Nome** e **Commento**. Nella sezione **Raccolta di limitazione** scegliere quindi **Sfoglia** e selezionare una raccolta di limitazione. La raccolta che si sta creando conterrà solo i membri della raccolta di limitazione.  

4. Nella pagina **Regole di appartenenza**, nell'elenco **Aggiungi regola** selezionare il tipo di regola di appartenenza da usare per la raccolta. È possibile configurare più regole per ogni raccolta. La configurazione varia in base alla regola. Per altre informazioni sulla configurazione di ogni regola, vedere le sezioni seguenti:  
    - [Regola diretta](#bkmk-direct)
    - [Regola di query](#bkmk-query)
    - [Regola categoria di dispositivi](#bkmk-category)
    - [Regola di inclusione raccolte](#bkmk-include)
    - [Regola di esclusione raccolte](#bkmk-exclude)

5. Nella pagina **Regole di appartenenza** esaminare inoltre le impostazioni seguenti:

    - **Utilizza aggiornamenti incrementali per questa raccolta**: selezionare questa opzione per eseguire periodicamente una scansione e aggiornare solo le risorse nuove o modificate rispetto alla valutazione raccolta precedente. Questo processo è indipendente da una valutazione raccolta completa. Per impostazione predefinita, gli aggiornamenti incrementali vengono eseguiti a intervalli di 5 minuti.  

        > [!IMPORTANT]  
        >  Le raccolte con regole di query che usano le classi seguenti non supportano gli aggiornamenti incrementali:  
        >   
        > -   SMS_G_System_CollectedFile  
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

    - **Pianifica un aggiornamento completo in questa raccolta**: pianificare una valutazione completa regolare dell'appartenenza alla raccolta.  

        A partire dalla versione 1810, le modifiche seguenti nel comportamento di valutazione delle raccolte possono migliorare le prestazioni del sito:<!--3607726-->  

        - In precedenza, quando si configurava una pianificazione per una raccolta basata su query, il sito continuava a valutare la query indipendentemente dall'impostazione **Pianifica un aggiornamento completo in questa raccolta**. Per disabilitare completamente la pianificazione, era necessario modificare la pianificazione impostando **Nessuno**. 

            Ora il sito cancella la pianificazione quando si disabilita questa impostazione. Per specificare una pianificazione per la valutazione delle raccolte, abilitare l'opzione **Pianifica un aggiornamento completo in questa raccolta**.  

            Quando si aggiorna il sito, per qualsiasi raccolta esistente in cui è stata specificata una pianificazione, il sito abilita l'opzione **Pianifica un aggiornamento completo in questa raccolta**. Anche se questa configurazione poteva non essere intenzionale, questo era il comportamento effettivo. Per interrompere la valutazione di una raccolta in base a una pianificazione nel sito, disabilitare questa opzione.  

        - Non è possibile disabilitare la valutazione delle raccolte predefinite, come **Tutti i sistemi**, ma ora è possibile configurare la pianificazione. Questo comportamento consente di personalizzare questa azione in base ai requisiti specifici. 

            > [!Tip]  
            > Modificare solo l'impostazione **Ora** della pianificazione personalizzata per le raccolte predefinite. Non modificare **Criterio ricorrenza**. Nelle iterazioni future potrebbe essere applicato un criterio di ricorrenza specifico.  

6. Completare la procedura guidata per creare la nuova raccolta. La nuova raccolta viene visualizzata nel nodo **Raccolte dispositivi** dell'area di lavoro **Asset e conformità** .  

> [!NOTE]  
> È necessario aggiornare o ricaricare la console di Configuration Manager per visualizzare i membri della raccolta. I membri non vengono visualizzati nella raccolta fino a quando non viene eseguito il primo aggiornamento pianificato. È anche possibile selezionare manualmente il comando **Aggiorna appartenenza** per la raccolta. L'aggiornamento della raccolta può richiedere alcuni minuti.  

        
### <a name="bkmk-direct"></a> Configurare una regola diretta  

1. Nella pagina **Cerca risorse** della **Creazione guidata regola di appartenenza diretta**specificare le informazioni seguenti:  

    - **Classe di risorse**: selezionare il tipo di risorsa che si vuole cercare e aggiungere alla raccolta. Ad esempio, 
        - **Risorsa di sistema**: cercare i dati di inventario restituiti dai computer client
        - **Computer sconosciuto**: selezionare tra i valori restituiti dai computer sconosciuti
        - **Risorsa utente**: cercare informazioni sugli utenti raccolte da Configuration Manager
        - **Risorsa gruppo utenti**: cercare informazioni sui gruppo di utenti raccolte da Configuration Manager

    - **Nome attributo**: selezionare l'attributo associato alla classe di risorse selezionata che si vuole cercare. Ad esempio,  

        - Per selezionare i computer in base al relativo nome NetBIOS, selezionare **Risorsa di sistema** nell'elenco **Classe di risorse** e **Nome NetBIOS** nell'elenco **Nome attributo**.  

        - Per selezionare gli utenti in base al nome dell'unità organizzativa (OU), selezionare **Risorsa utente** nell'elenco **Classe di risorse** e **Nome unità organizzativa utente** nell'elenco **Nome attributo**.  

    - **Escludere le risorse contrassegnate come obsolete**: se un computer client è contrassegnato come obsoleto, non includere questo valore nei risultati della ricerca.  

    - **Escludere le risorse in cui non è installato il client di Configuration Manager**: queste risorse non verranno visualizzate nei risultati della ricerca.  

    - **Valore**: immettere un valore per la ricerca del nome di attributo selezionato. Usare il simbolo di percentuale `%` come carattere jolly. Ad esempio,  
        - Per cercare i computer con un nome NetBIOS che inizia con "M", immettere `M%` in questo campo.  
        - Per cercare gli utenti nell'unità organizzativa Contoso, immettere `Contoso` in questo campo.

2. Nella pagina **Seleziona risorse** selezionare le risorse da aggiungere alla raccolta nell'elenco **Risorse** e quindi scegliere **Avanti**.  


### <a name="bkmk-query"></a> Configurare una regola di query  

Nella finestra di dialogo **Proprietà regola di query** specificare le informazioni seguenti:  

- **Nome**: specificare un nome univoco per la query.  

- **Importa istruzione query**: apre la finestra di dialogo **Sfoglia query**. Selezionare una [query di Configuration Manager](/sccm/core/servers/manage/create-queries) da usare come regola di query per la raccolta.   

- **Classe di risorse**: selezionare il tipo di risorsa che si vuole cercare e aggiungere alla raccolta. Selezionare un valore in **Risorsa di sistema** per cercare i dati di inventario restituiti dai computer client o **Computer sconosciuto** per effettuare una selezione tra i valori restituiti dai computer sconosciuti.  

- **Modifica istruzione query**: apre la finestra di dialogo **Proprietà istruzione query**, dove è possibile modificare una query da usare come regola per la raccolta. Per altre informazioni sulle query, vedere [Introduzione alle query](/sccm/core/servers/manage/introduction-to-queries).  


### <a name="bkmk-category"></a> Regola categoria di dispositivi

Nella finestra **Selezionare le categorie di dispositivi** sono disponibili le azioni seguenti:

- **Crea**: specificare un nome per creare una nuova categoria
- **Rinomina**: consente di rinominare la categoria selezionata
- **Elimina**: selezionare una o più categorie e usare questa azione per rimuoverle dall'elenco

Per altre informazioni, vedere [Classificare automaticamente i dispositivi in raccolte](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections).<!-- SCCMDocs issue 552 -->


### <a name="bkmk-include"></a> Configurare una regola di inclusione raccolte  

Nella finestra di dialogo **Seleziona raccolte** selezionare le raccolte da includere nella nuova raccolta e quindi scegliere **OK**.  


### <a name="bkmk-exclude"></a> Configurare una regola di esclusione raccolte  

Nella finestra di dialogo **Seleziona raccolte** selezionare le raccolte da escludere dalla nuova raccolta e quindi scegliere **OK**.  



## <a name="bkmk_import"></a> Importare una raccolta  

Quando si esporta una raccolta da un sito, Configuration Manager la salva come file MOF (Managed Object Format). Usare questa procedura per importare il file nel database del sito. Sono necessarie autorizzazioni di **creazione** per la classe delle raccolte. 

> [!Important]  
> - Assicurarsi che il file contenga solo i dati della raccolta, provenga da una fonte attendibile e non sia stato manomesso.  
> 
> - Assicurarsi che il file sia stato esportato da un sito che esegue la stessa versione di Configuration Manager.  

Per altre informazioni sull'esportazione di raccolte, vedere [Come gestire le raccolte](/sccm/core/clients/manage/collections/manage-collections).


1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità**. Selezionare il nodo **Raccolte utenti** o **Raccolte dispositivi**.  

2. Nel gruppo **Crea** della scheda **Home** della barra multifunzione scegliere **Importa raccolte**.  

3. Nella pagina **Generale** dell'**Importazione guidata raccolte** scegliere **Avanti**.  

4. Nella pagina **Nome file MOF** scegliere **Sfoglia**. Passare al file MOF contenente le informazioni sulla raccolta da importare.  

5. Completare la procedura guidata per importare la raccolta. La nuova raccolta viene visualizzata nel nodo **Raccolte utenti** o **Raccolte dispositivi** dell'area di lavoro **Asset e conformità** . Aggiornare o ricaricare la console di Configuration Manager per visualizzare i membri della raccolta appena importata.  

## <a name="bkmk_powershell"></a> Uso di PowerShell

È possibile usare PowerShell per creare e importare raccolte.  Per altre informazioni, vedere:

* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Set-CMCollection)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Import-CMCollection)

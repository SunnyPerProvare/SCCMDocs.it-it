---
title: Gestire le raccolte
titleSuffix: Configuration Manager
description: Eseguire le attività comuni di gestione delle raccolte in Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b7047a2e931af73f961d2b2f87360921a3cf762b
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75824436"
---
# <a name="how-to-manage-collections-in-configuration-manager"></a>Come gestire le raccolte in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Usare le informazioni generali di questo articolo per eseguire le attività di gestione per le raccolte in Configuration Manager.  

> [!NOTE]  
>  Per informazioni su come creare raccolte di Configuration Manager, vedere [Come creare le raccolte in Configuration Manager](/sccm/core/clients/manage/collections/create-collections).



## <a name="bkmk_device"></a> Come gestire le raccolte di dispositivi  

Nell'area di lavoro **Asset e conformità** selezionare **Raccolte dispositivi**, selezionare la raccolta da gestire e quindi selezionare un'attività di gestione.  


#### <a name="show-members"></a>Mostra i membri
Visualizza tutte le risorse che sono membri della raccolta selezionata in un nodo temporaneo nel nodo **Dispositivi** .


#### <a name="add-selected-items"></a>Aggiungi elementi selezionati
Fornisce le opzioni seguenti: 

- **Aggiungi elementi selezionati alla raccolta dispositivi esistente**: Apre la finestra di dialogo **Seleziona raccolta** . Selezionare la raccolta a cui aggiungere i membri della raccolta selezionata. La raccolta selezionata viene inclusa in questa raccolta tramite la regola di appartenenza **Includi raccolte** .  

- **Aggiungi elementi selezionati alla nuova raccolta dispositivi**: apre la **Creazione guidata raccolta dispositivi** in cui è possibile creare una nuova raccolta. La raccolta selezionata viene inclusa in questa raccolta tramite la regola di appartenenza **Includi raccolte** .  


Per altre informazioni, vedere [Come creare le raccolte](/sccm/core/clients/manage/collections/create-collections).


#### <a name="install-client"></a>Installare il Client
Apre la **procedura guidata Installa client**. Questa procedura guidata usa l'installazione push client per installare un client di Configuration Manager in tutti i computer nella raccolta selezionata. Per altre informazioni, vedere [Installazione push client](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).


#### <a name="run-script"></a>Esegui script
Apre la procedura guidata **Esegui script** per eseguire uno script di PowerShell in tutti i client della raccolta. Per altre informazioni, vedere [Creare ed eseguire script di PowerShell](/sccm/apps/deploy-use/create-deploy-scripts).


#### <a name="manage-affinity-requests"></a>Gestire le richieste di affinità
Apre la finestra di dialogo **Gestire le richieste di affinità utente dispositivo**. Approvare o rifiutare richieste in sospeso per stabilire le affinità utente-dispositivo per i dispositivi nella raccolta selezionata. Per altre informazioni, vedere [Collegare utenti e dispositivi mediante l'affinità utente-dispositivo](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity)


#### <a name="clear-required-pxe-deployments"></a>Cancellare le distribuzioni PXE richiesto
Cancella tutte le distribuzioni di avvio PXE richieste da tutti i membri della raccolta selezionata. Per altre informazioni, vedere [Usare PXE per distribuire Windows in rete](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).


#### <a name="update-membership"></a>Aggiorna appartenenza
Valuta l'appartenenza per la raccolta selezionata. Per le raccolte con molti membri, il completamento di questo aggiornamento potrebbe richiedere tempo. Usare l'azione **Aggiorna** per aggiornare la visualizzazione con i nuovi membri delle raccolte dopo il completamento dell'aggiornamento.


#### <a name="add-resources"></a>Aggiungi risorse
Apre la finestra di dialogo **Aggiungi risorse alla raccolta**. Cercare nuove risorse da aggiungere alla raccolta selezionata. L'icona per la raccolta selezionata mostra il simbolo di una clessidra mentre è in corso l'aggiornamento.


#### <a name="client-notification"></a>Notifica client
Per altre informazioni, vedere [Client notifications](/sccm/core/clients/manage/client-notification) (Notifiche client).


#### <a name="endpoint-protection"></a>Endpoint Protection
Per altre informazioni vedere [Client notifications](/sccm/core/clients/manage/client-notification) (Notifiche client).


#### <a name="export"></a>Export
Apre l'**Esportazione guidata raccolte** che consente di esportare questa raccolta in un file MOF (Managed Object Format). Questo file può quindi essere archiviato o importato in un altro sito di Configuration Manager. Quando si esporta una raccolta, non vengono esportate le raccolte di riferimento. La raccolta selezionata fa riferimento a una raccolta di riferimento tramite una regola di **inclusione** o **esclusione**.


#### <a name="copy"></a>Copia
Crea una copia della raccolta selezionata. La nuova raccolta usa la raccolta selezionata come raccolta di limitazione.


#### <a name="refresh"></a>Aggiorna
Aggiorna la vista.


#### <a name="delete"></a>Elimina
Elimina la raccolta selezionata. È anche possibile eliminare tutte le risorse nella raccolta dal database del sito. 

Non è possibile eliminare le raccolte predefinite di Configuration Manager. Per un elenco di raccolte predefinite, vedere [Introduzione alle raccolte](/sccm/core/clients/manage/collections/introduction-to-collections#built-in-collections).


#### <a name="simulate-deployment"></a>Simula distribuzione
Apre la **Simulazione guidata distribuzione applicazione**. Questa procedura guidata consente di testare i risultati di una distribuzione di applicazione senza installare o disinstallare l'applicazione. Per altre informazioni, vedere [Come simulare distribuzioni di applicazioni](/sccm/apps/deploy-use/simulate-application-deployments).


#### <a name="deploy"></a>Distribuisci
Vengono visualizzate le opzioni seguenti:  

- **Applicazione**: apre la **Distribuzione guidata del software**. Selezionare e configurare la distribuzione di un'applicazione nella raccolta selezionata. Per altre informazioni, vedere [Come distribuire le applicazioni](/sccm/apps/deploy-use/deploy-applications).  

- **Programma**: apre la **Distribuzione guidata del software**. Selezionare e configurare una distribuzione di pacchetti e programmi nella raccolta selezionata. Per altre informazioni, vedere [Packages and programs](/sccm/apps/deploy-use/packages-and-programs) (Pacchetti e programmi).  

- **Linea di base di configurazione**: apre la finestra di dialogo **Distribuisci linee di base di configurazione**. Configurare la distribuzione di una o più linee di base di configurazione nella raccolta selezionata. Per altre informazioni, vedere [Come distribuire linee di base di configurazione](/sccm/compliance/deploy-use/deploy-configuration-baselines).  

- **Sequenza di attività**: apre la **Distribuzione guidata del software**. Selezionare e configurare la distribuzione di una sequenza di attività nella raccolta selezionata. Per altre informazioni, vedere [Gestire le sequenze di attività per automatizzare le attività](/sccm/osd/deploy-use/deploy-a-task-sequence).  

- **Aggiornamenti software**: apre la **Distribuzione guidata degli aggiornamenti software**. Configurare la distribuzione degli aggiornamenti software nelle risorse della raccolta selezionata. Per altre informazioni, vedere [Gestire gli aggiornamenti software](/sccm/sum/understand/software-updates-introduction).  


#### <a name="clear-server-group-deployment-locks"></a>Cancellare i blocchi di distribuzione del gruppo di server
Rilasciare manualmente tutti i blocchi di distribuzione del gruppo di server per la raccolta. Per altre informazioni, vedere [Assistenza a un gruppo di server](/sccm/sum/deploy-use/service-a-server-group).


#### <a name="move"></a>Sposta
Spostare la raccolta selezionata in un'altra cartella del nodo **Raccolte dispositivi**. 


#### <a name="properties"></a>Proprietà
Per altre informazioni, vedere [Proprietà della raccolta](#BKMK_CollProp).  


## <a name="bkmk_user"></a> Come gestire le raccolte utenti  

Nell'area di lavoro **Asset e conformità** selezionare **Raccolte utenti**, selezionare la raccolta da gestire e quindi selezionare un'attività di gestione.  

> [!Note]  
> Le azioni seguenti sono disponibili nelle raccolte utenti, ma i comportamenti sono gli stessi delle raccolte dispositivi, con la differenza che si applicano alle raccolte utenti e agli utenti in esse contenuti. Per altre informazioni, vedere l'azione corrispondente in [Come gestire le raccolte di dispositivi](#bkmk_device).  

- **Mostra i membri**  
- **Aggiungi elementi selezionati**  
    - **Aggiungi elementi selezionati alla raccolta utenti esistente**  
    - **Aggiungi elementi selezionati alla nuova raccolta utenti**  
- **Gestisci richieste affinità**  
- **Aggiorna appartenenza**  
- **Aggiungi risorse**  
- **Export**  
- **Copia**  
- **Aggiorna**  
- **Eliminazione**  
- **Simula distribuzione**  
- **Distribuzione**  
    - **Applicazione**  
    - **Programma**  
    - **Linea di base di configurazione**
- **Sposta**  
- **Proprietà**


##  <a name="BKMK_CollProp"></a> Proprietà della raccolta  

Quando si apre la finestra di dialogo **Proprietà** per una raccolta, visualizzare e configurare le opzioni seguenti:  

#### <a name="general"></a>Generale
Visualizzare e configurare le informazioni generali sulla raccolta selezionata, inclusi il nome e la raccolta di limitazione.

#### <a name="membership-rules"></a>Regole di appartenenza
Configurare le regole di appartenenza che definiscono l'appartenenza di questa raccolta. Per altre informazioni, vedere [Come creare le raccolte](/sccm/core/clients/manage/collections/create-collections).  

#### <a name="power-management"></a>Risparmio energia
Configurare i piani di gestione dell'alimentazione assegnati ai computer nella raccolta selezionata. Per altre informazioni, vedere [Introduzione alle raccolte](/sccm/core/clients/manage/power/introduction-to-power-management).  

#### <a name="deployments"></a>Distribuzioni
Visualizza qualsiasi software distribuito nei membri della raccolta selezionata.  

#### <a name="maintenance-windows"></a>Finestre di manutenzione
Visualizzare e configurare le finestre di manutenzione applicate ai membri della raccolta selezionata. Per altre informazioni, vedere [Come usare le finestre di manutenzione](/sccm/core/clients/manage/collections/use-maintenance-windows).

#### <a name="collection-variables"></a>Variabili di raccolta
Configurare le variabili che si applicano a questa raccolta e possono essere usate dalle sequenze di attività. Per altre informazioni, vedere [Come impostare le variabili della sequenza di attività](/sccm/osd/understand/using-task-sequence-variables#bkmk_set).  

#### <a name="distribution-point-groups"></a>Gruppi di punti di distribuzione
Associare uno o più gruppi di punti di distribuzione ai membri della raccolta selezionata. Per altre informazioni, vedere [Manage content and content infrastructure](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure) (Gestire il contenuto e l'infrastruttura del contenuto).

#### <a name="aad-group-sync"></a>Sincronizzazione del gruppo AAD
Sincronizzare i risultati di appartenenza alla raccolta con i gruppi di Azure Active Directory. Questa sincronizzazione è una [funzionalità di versione non definitiva](/sccm/core/servers/manage/pre-release-features) a partire dalla versione 1906. Per altre informazioni, vedere [Creare raccolte](/sccm/core/clients/manage/collections/create-collections#bkmk_aadcollsync).

#### <a name="security"></a>Sicurezza
Visualizza gli utenti amministratori che dispongono di autorizzazioni per la raccolta selezionata da ambiti di protezione e ruoli associati. Per altre informazioni, vedere [Nozioni fondamentali sull'amministrazione basata su ruoli](/sccm/core/understand/fundamentals-of-role-based-administration).  

#### <a name="alerts"></a>Avvisi 
Determinare quando vengono generati avvisi per lo stato del client ed Endpoint Protection. Per altre informazioni, vedere [Come configurare lo stato del client](/sccm/core/clients/deploy/configure-client-status) e [Come monitorare Endpoint Protection](/sccm/protect/deploy-use/monitor-endpoint-protection).  
## <a name="bkmk_powershell"></a> Uso di PowerShell

È possibile usare PowerShell per gestire le raccolte.  Per altre informazioni, vedere:

* [Get-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollection)
* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Copy-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/copy-cmcollection)
* [Remove-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollection)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmcollection)
* [Export-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/export-cmcollection)
* [Get-CMCollectionMember](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionmember)
* [Get-CMCollectionSetting](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionsetting)
* [Invoke-CMCollectionUpdate](https://docs.microsoft.com/powershell/module/configurationmanager/invoke-cmcollectionupdate)
* [Add-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectionmembershiprule)
* [Set-CMCollectionPowerManagement](https://docs.microsoft.com/powershell/module/configurationmanager/set-cmcollectionpowermanagement)
* [Get-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionmembershiprule)
* [Remove-CMCollectionMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionmembershiprule)
* [Get-CMCollectionDirectMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectiondirectmembershiprule)
* [Get-CMCollectionQueryMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionquerymembershiprule)
* [Get-CMCollectionIncludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionincludemembershiprule)
* [Add-CMCollectionToAdministrativeUser](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectiontoadministrativeuser)
* [Remove-CMCollectionQueryMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionquerymembershiprule)
* [Remove-CMCollectionDirectMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectiondirectmembershiprule)
* [Get-CMCollectionExcludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/get-cmcollectionexcludemembershiprule)
* [Add-CMCollectionToDistributionPointGroup](https://docs.microsoft.com/powershell/module/configurationmanager/add-cmcollectiontodistributionpointgroup)
* [Remove-CMCollectionIncludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionincludemembershiprule)
* [Remove-CMCollectionExcludeMembershipRule](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionexcludemembershiprule)
* [Remove-CMCollectionFromAdministrativeUser](https://docs.microsoft.com/powershell/module/configurationmanager/remove-cmcollectionfromadministrativeuser)

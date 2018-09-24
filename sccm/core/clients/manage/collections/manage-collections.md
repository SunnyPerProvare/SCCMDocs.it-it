---
title: Gestire le raccolte
titleSuffix: Configuration Manager
description: Eseguire le attività comuni di gestione delle raccolte in Configuration Manager.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d7c967ce02c009cd9659c7956f7ca79f4a34faf
ms.sourcegitcommit: be8c0182db9ef55a948269fcbad7c0f34fd871eb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/23/2018
ms.locfileid: "42755973"
---
# <a name="how-to-manage-collections-in-configuration-manager"></a>Come gestire le raccolte in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare le informazioni generali di questo articolo per eseguire le attività di gestione per le raccolte in Configuration Manager.  

> [!NOTE]  
>  Per informazioni su come creare raccolte di Configuration Manager, vedere [Come creare le raccolte in Configuration Manager](/sccm/core/clients/manage/collections/create-collections).  



## <a name="bkmk_device"></a> Come gestire le raccolte di dispositivi  

 Nell'area di lavoro **Asset e conformità** selezionare **Raccolte dispositivi**, selezionare la raccolta da gestire e quindi selezionare un'attività di gestione.  


#### <a name="show-members"></a>Mostra i membri
 Visualizza tutte le risorse che sono membri della raccolta selezionata in un nodo temporaneo nel nodo **Dispositivi** .


#### <a name="add-selected-items"></a>Aggiungi elementi selezionati
 Fornisce le opzioni seguenti: 

 - **Aggiungi elementi selezionati alla raccolta dispositivi esistente**: apre la finestra di dialogo **Seleziona raccolta**. Selezionare la raccolta a cui aggiungere i membri della raccolta selezionata. La raccolta selezionata viene inclusa in questa raccolta tramite la regola di appartenenza **Includi raccolte** .  

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


#### <a name="add-resources"></a>Aggiunta di risorse
 Apre la finestra di dialogo **Aggiungi risorse alla raccolta**. Cercare nuove risorse da aggiungere alla raccolta selezionata. L'icona per la raccolta selezionata mostra il simbolo di una clessidra mentre è in corso l'aggiornamento.


#### <a name="client-notification"></a>Notifica client
 Indica a tutti i client nella raccolta di dispositivi selezionata di eseguire immediatamente una delle azioni seguenti:

 - **Scarica criteri computer**: aggiorna i criteri del dispositivo. Per altre informazioni, vedere [Avviare il recupero criteri per un client di Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  

 - **Scarica criteri utente**: aggiorna i criteri dell'utente.  

 - **Raccogli i dati di individuazione**: attiva i client per l'invio di un record dei dati di individuazione. Per altre informazioni, vedere [Individuazione heartbeat](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutHeartbeat).  

 - **Raccogli l'inventario software**: attiva i client per l'esecuzione di un ciclo di inventario software. Per altre informazioni, vedere [Introduzione all'inventario software](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).  

 - **Raccogli l'inventario hardware**: attiva i client per l'esecuzione di un ciclo di inventario hardware. Per altre informazioni, vedere [Introduzione all'inventario hardware](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).  

 - **Valuta le distribuzioni dell'applicazione**: attiva i client per l'esecuzione di un ciclo di valutazione delle distribuzioni dell'applicazione. Per altre informazioni, vedere [Pianificare nuova valutazione per le distribuzioni](/sccm/core/clients/deploy/about-client-settings#schedule-re-evaluation-for-deployments).  

 - **Valuta le distribuzioni di aggiornamento software**: attiva i client per l'esecuzione di un ciclo di valutazione delle distribuzioni degli aggiornamenti software. Per altre informazioni, vedere [Introduzione agli aggiornamenti software](/sccm/sum/understand/software-updates-introduction).  

 - **Passare al punto di aggiornamento software successivo**: attiva i client per il passaggio al successivo punto di aggiornamento software disponibile. Per altre informazioni, vedere [Passaggio a un nuovo punto di aggiornamento software](/sccm/sum/plan-design/plan-for-software-updates#BKMK_SUPSwitching).  

 - **Valuta l'attestazione dell'integrità del dispositivo**: attiva i client di Windows 10 per il controllo e l'invio dello stato dell'integrità del dispositivo più recente. Per altre informazioni, vedere [Attestazione dell'integrità](/sccm/core/servers/manage/health-attestation).  

 - **Controlla la conformità dell'accesso condizionale**: attiva i client per il controllo della conformità dell'accesso condizionale. Per altre informazioni, vedere [Gestire l'accesso ai servizi di O365 per i PC](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm).  


#### <a name="endpoint-protection"></a>Endpoint Protection
 Indica a tutti i client nella raccolta di dispositivi selezionata di eseguire immediatamente una delle azioni seguenti:

 - **Analisi completa**: attiva Endpoint Protection o Windows Defender per l'esecuzione di un'analisi antimalware *completa*  

 - **Analisi veloce**: attiva Endpoint Protection o Windows Defender per l'esecuzione di un'analisi antimalware *veloce*  

 - **Scarica definizione**: attiva Endpoint Protection o Windows Defender per il download delle definizioni antimalware più recenti  


 Per altre informazioni, vedere [Endpoint Protection in Configuration Manager](/sccm/protect/deploy-use/endpoint-protection).


#### <a name="export"></a>Esporta
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


#### <a name="deploy"></a>Distribuire
 Vengono visualizzate le opzioni seguenti:  

 - **Applicazione**: apre la **Distribuzione guidata del software**. Selezionare e configurare la distribuzione di un'applicazione nella raccolta selezionata. Per altre informazioni, vedere [Come distribuire le applicazioni](/sccm/apps/deploy-use/deploy-applications).  

 - **Programma**: apre la **Distribuzione guidata del software**. Selezionare e configurare una distribuzione di pacchetti e programmi nella raccolta selezionata. Per altre informazioni, vedere [Packages and programs](/sccm/apps/deploy-use/packages-and-programs) (Pacchetti e programmi).  

 - **Linea di base di configurazione**: apre la finestra di dialogo **Distribuisci linee di base di configurazione**. Configurare la distribuzione di una o più linee di base di configurazione nella raccolta selezionata. Per altre informazioni, vedere [Come distribuire linee di base di configurazione](/sccm/compliance/deploy-use/deploy-configuration-baselines).  

 - **Sequenza di attività**: apre la **Distribuzione guidata del software**. Selezionare e configurare la distribuzione di una sequenza di attività nella raccolta selezionata. Per altre informazioni, vedere [Gestire le sequenze di attività per automatizzare le attività](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).  

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

#### <a name="security"></a>Sicurezza
 Visualizza gli utenti amministratori che dispongono di autorizzazioni per la raccolta selezionata da ambiti di protezione e ruoli associati. Per altre informazioni, vedere [Nozioni fondamentali sull'amministrazione basata su ruoli](/sccm/core/understand/fundamentals-of-role-based-administration).  

#### <a name="alerts"></a>Avvisi 
 Determinare quando vengono generati avvisi per lo stato del client ed Endpoint Protection. Per altre informazioni, vedere [Come configurare lo stato del client](/sccm/core/clients/deploy/configure-client-status) e [Come monitorare Endpoint Protection](/sccm/protect/deploy-use/monitor-endpoint-protection).  

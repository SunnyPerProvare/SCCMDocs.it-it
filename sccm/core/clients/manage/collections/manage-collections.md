---
title: Gestire le raccolte
titleSuffix: Configuration Manager
description: "Eseguire le attività comuni di gestione delle raccolte in System Center Configuration Manager."
ms.custom: na
ms.date: 4/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
caps.latest.revision: "8"
caps.handback.revision: "0"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 0655a1dc566657cb27cdc7537603871dc36cc568
ms.sourcegitcommit: c236214b2fcc13dae7bad96d7fb33f692868191d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/12/2017
---
# <a name="how-to-manage-collections-in-system-center-configuration-manager"></a>Come gestire le raccolte in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare le informazioni generali di questo argomento per eseguire le attività di gestione per le raccolte in System Center Configuration Manager.  

> [!NOTE]  
>  Per informazioni su come creare le raccolte di Configuration Manager, vedere [Come creare le raccolte in System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).  

## <a name="how-to-manage-device-collections"></a>Come gestire le raccolte di dispositivi  
 Nell'area di lavoro **Asset e conformità** selezionare **Raccolte dispositivi**, selezionare la raccolta da gestire e quindi selezionare un'attività di gestione.  

 Per altre informazioni sulle attività di gestione che potrebbero richiedere alcune informazioni prima della relativa selezione, usare la seguente tabella.  

|Attività di gestione|Dettagli|Altre informazioni|  
|---------------------|-------------|----------------------|  
|**Mostra i membri**|Visualizza tutte le risorse che sono membri della raccolta selezionata in un nodo temporaneo nel nodo **Dispositivi** .|Nessuna informazione aggiuntiva.|  
|**Aggiungi elementi selezionati**|Fornisce le opzioni seguenti per eseguire una delle operazioni indicate:<br /><br /> - <br />                    **Aggiungi elementi selezionati alla raccolta dispositivi esistente**: apre la finestra di dialogo **Seleziona raccolta** in cui è possibile selezionare la raccolta a cui aggiungere i membri della raccolta selezionata. La raccolta selezionata viene inclusa in questa raccolta tramite la regola di appartenenza **Includi raccolte** .<br /><br /> - **Aggiungi elementi selezionati alla nuova raccolta dispositivi**: apre la **Creazione guidata raccolta dispositivi** in cui è possibile creare una nuova raccolta. La raccolta selezionata viene inclusa in questa raccolta tramite la regola di appartenenza **Includi raccolte** .|[Come creare le raccolte in System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md)|  
|**Installa client**|Apre la procedura guidata **Installa client** che usa l'installazione push client per installare un client di Configuration Manager in tutti i computer nella raccolta selezionata.|[Come distribuire i client nei computer Windows](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)|  
|**Gestisci richieste affinità**|Apre la finestra di dialogo **Gestire le richieste di affinità utente dispositivo** in cui è possibile approvare o rifiutare richieste in sospeso per stabilire le affinità utente dispositivo per i dispositivi nella raccolta selezionata.|[Collegare utenti e dispositivi mediante l'affinità utente-dispositivo in System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)|  
|**Cancella distribuzioni PXE richieste**|Cancella tutte le distribuzioni di avvio PXE richieste da tutti i membri della raccolta selezionata.|[Introduzione alla distribuzione del sistema operativo](../../../../osd/understand/introduction-to-operating-system-deployment.md)|  
|**Aggiorna appartenenza**|Valuta l'appartenenza per la raccolta selezionata. Per le raccolte con molti membri, il completamento di questo aggiornamento potrebbe richiedere tempo. Usare l'azione **Aggiorna** per aggiornare la visualizzazione con i nuovi membri delle raccolte dopo il completamento dell'aggiornamento.|Nessuna informazione aggiuntiva.|  
|**Aggiungi risorse**|Apre la finestra di dialogo **Aggiungi risorse alla raccolta** nella quale è possibile cercare nuove risorse da aggiungere alla raccolta selezionata.<br /><br /> L'icona della raccolta selezionata visualizzerà il simbolo di una clessidra mentre è in corso l'aggiornamento.|Nessuna informazione aggiuntiva.|  
|**Notifica client**|Indica a tutti i client nella raccolta di dispositivi selezionata di scaricare i criteri utente o computer.|Nessuna informazione aggiuntiva.|  
|**Endpoint Protection**|Esegue un'analisi antimalware completa o rapida o scarica le definizioni antimalware più recenti nei computer della raccolta selezionata.|[Endpoint Protection in System Center Configuration Manager](../../../../protect/deploy-use/endpoint-protection.md)|  
|**Export**|Apre l'**Esportazione guidata raccolte** che consente di esportare la raccolta in un file MOF (Managed Object Format) che può quindi essere archiviato o usato in un altro sito di Configuration Manager.<br /><br /> Quando si esporta una raccolta, le raccolte a cui fa riferimento la raccolta selezionata tramite una regola **Inclusione** o **Esclusione** non vengono esportate.|Nessuna informazione aggiuntiva.|  
|**Copia**|Crea una copia della raccolta selezionata. La nuova raccolta usa la raccolta selezionata come raccolta di limitazione.|Nessuna informazione aggiuntiva.|  
|**Eliminazione**|Elimina la raccolta selezionata. È anche possibile eliminare tutte le risorse nella raccolta dal database del sito.<br /><br /> Non è possibile eliminare le raccolte predefinite di Configuration Manager.|Per un elenco delle raccolte predefinite, vedere [Introduzione alle raccolte in System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).|  
|**Simula distribuzione**|Apre la **Simulazione guidata distribuzione applicazione** che consente di testare i risultati di una distribuzione di applicazione senza installare o disinstallare l'applicazione.|[Come simulare distribuzioni di applicazioni con System Center Configuration Manager](../../../../apps/deploy-use/simulate-application-deployments.md)|  
|**Distribuisci**|Vengono visualizzate le opzioni seguenti:<br /><br /> - <br />                    **Applicazione** - Apre la **Distribuzione guidata del software** in cui è possibile selezionare e configurare la distribuzione di un'applicazione nella raccolta selezionata.<br /><br /> - <br />                    **Programma** - Apre la **Distribuzione guidata del software** in cui è possibile selezionare e configurare la distribuzione di un pacchetto e un programma nella raccolta selezionata.<br /><br /> - **Linee di base di configurazione** - Apre la finestra di dialogo **Distribuisci linee di base di configurazione** in cui è possibile configurare la distribuzione di una o più linee di base di configurazione nella raccolta selezionata.<br /><br /> - <br />                    **Sequenza attività** - Apre la **Distribuzione guidata del software** in cui è possibile selezionare e configurare una distribuzione di sequenza di attività nella raccolta selezionata.<br /><br /> - <br />                    **Aggiornamenti software** - Apre la **Distribuzione guidata degli aggiornamenti software** in cui è possibile configurare la distribuzione degli aggiornamenti software nelle risorse della raccolta selezionata.|[Come distribuire le applicazioni con System Center Configuration Manager](../../../../apps/deploy-use/deploy-applications.md)<br /><br /> [Pacchetti e programmi in System Center Configuration Manager](../../../../apps/deploy-use/packages-and-programs.md)<br /><br /> [Come distribuire linee di base di configurazione in System Center Configuration Manager](../../../../compliance/deploy-use/deploy-configuration-baselines.md)<br /><br /> [Gestire le sequenze di attività per automatizzare le attività in System Center Configuration Manager](../../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)<br /><br /> [Gestire gli aggiornamenti software in System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction)|  

## <a name="how-to-manage-user-collections"></a>Come gestire le raccolte utenti  
 Nell'area di lavoro **Asset e conformità** selezionare **Raccolte utenti**, selezionare la raccolta da gestire e quindi selezionare un'attività di gestione.  

 Per altre informazioni sulle attività di gestione che potrebbero richiedere alcune informazioni prima della relativa selezione, usare la seguente tabella.  

|Attività di gestione|Dettagli|Altre informazioni|  
|---------------------|-------------|----------------------|  
|**Mostra i membri**|Visualizza tutte le risorse che sono membri della raccolta selezionata in un nodo temporaneo nel nodo **Utenti** .|Nessuna informazione aggiuntiva.|  
|**Aggiungi elementi selezionati**|Questa opzione consente di eseguire una delle operazioni seguenti:<br /><br /> - <br />                    **Aggiungi elementi selezionati alla raccolta utenti esistente** - Apre la finestra di dialogo **Seleziona raccolta** in cui è possibile selezionare la raccolta a cui aggiungere i membri della raccolta selezionata. La raccolta selezionata viene inclusa in questa raccolta tramite la regola di appartenenza **Includi raccolte** .<br /><br /> - **Aggiungi elementi selezionati alla nuova raccolta utenti** - Apre la **Creazione guidata raccolta utenti** in cui è possibile creare una nuova raccolta. La raccolta selezionata viene inclusa in questa raccolta tramite la regola di appartenenza **Includi raccolte** .|[Come creare le raccolte in System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md)|  
|**Gestisci richieste affinità**|Apre la finestra di dialogo **Gestire le richieste di affinità utente dispositivo** in cui è possibile approvare o rifiutare richieste in sospeso per stabilire le affinità utente dispositivo per gli utenti nella raccolta selezionata.|[Collegare utenti e dispositivi mediante l'affinità utente-dispositivo in System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)|  
|**Aggiorna appartenenza**|Valuta l'appartenenza per la raccolta selezionata. Per le raccolte con molti membri, il completamento di questo aggiornamento potrebbe richiedere tempo. Usare l'azione **Aggiorna** per aggiornare la visualizzazione con i nuovi membri delle raccolte dopo il completamento dell'aggiornamento.<br /><br /> L'icona della raccolta selezionata visualizzerà il simbolo di una clessidra mentre è in corso l'aggiornamento.|Nessuna informazione aggiuntiva.|  
|**Aggiungi risorse**|Apre la finestra di dialogo **Aggiungi risorse alla raccolta** nella quale è possibile cercare nuove risorse da aggiungere alla raccolta selezionata.|Nessuna informazione aggiuntiva.|  
|**Export**|Apre l'**Esportazione guidata raccolte** che consente di esportare la raccolta in un file MOF (Managed Object Format) che può quindi essere archiviato o usato in un altro sito di Configuration Manager.<br /><br /> Quando si esporta una raccolta, le raccolte a cui fa riferimento la raccolta selezionata tramite una regola **Inclusione** o **Esclusione** non vengono esportate.|Nessuna informazione aggiuntiva.|  
|**Copia**|Crea una copia della raccolta selezionata. La nuova raccolta usa la raccolta selezionata come raccolta di limitazione.|Nessuna informazione aggiuntiva.|  
|**Eliminazione**|Elimina la raccolta selezionata. È anche possibile eliminare tutte le risorse nella raccolta dal database del sito.<br /><br /> Non è possibile eliminare le raccolte predefinite di Configuration Manager.|Per un elenco delle raccolte predefinite, vedere [Introduzione alle raccolte in System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).|  
|**Simula distribuzione**|Apre la **Simulazione guidata distribuzione applicazione** che consente di testare i risultati di una distribuzione di applicazione senza installare o disinstallare l'applicazione.|[Come simulare distribuzioni di applicazioni con System Center Configuration Manager](../../../../apps/deploy-use/simulate-application-deployments.md)|  
|**Distribuisci**|Vengono visualizzate le opzioni seguenti:<br /><br /> - **Applicazione** - Apre la **Distribuzione guidata del software** in cui è possibile selezionare e configurare la distribuzione di un'applicazione nella raccolta selezionata.<br /><br /> - <br />                    **Programma** - Apre la **Distribuzione guidata del software** in cui è possibile selezionare e configurare la distribuzione di un pacchetto e un programma nella raccolta selezionata.<br /><br /> - **Linee di base di configurazione** - Apre la finestra di dialogo **Distribuisci linee di base di configurazione** in cui è possibile configurare la distribuzione di una o più linee di base di configurazione nella raccolta selezionata.|[Come distribuire le applicazioni con System Center Configuration Manager](../../../../apps/deploy-use/deploy-applications.md)<br /><br /> [Pacchetti e programmi in System Center Configuration Manager](../../../../apps/deploy-use/packages-and-programs.md)<br /><br /> [Come distribuire linee di base di configurazione in System Center Configuration Manager](../../../../compliance/deploy-use/deploy-configuration-baselines.md)|  

##  <a name="BKMK_CollProp"></a> Proprietà della raccolta  
 Quando si apre la finestra di dialogo **Proprietà** per una raccolta, è possibile visualizzare e configurare le proprietà seguenti per la raccolta.  

|Nome scheda|Altre informazioni|  
|--------------|----------------------|  
|**Generalee**|Consente di visualizzare e configurare le informazioni generali sulla raccolta selezionata, inclusi il nome e la raccolta di limitazione.|  
|**Regole di appartenenza**|Consente di configurare le regole di appartenenza che definiscono l'appartenenza della raccolta. Per altre informazioni, vedere [Come creare le raccolte in System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).|  
|**Risparmio energia**|Consente di configurare i piani di risparmio energia assegnati ai computer nella raccolta selezionata. Per altre informazioni, vedere [Introduzione alle raccolte](../../../../core/clients/manage/power/introduction-to-power-management.md).|  
|**Distribuzioni**|Visualizza qualsiasi software che è stato distribuito ai membri della raccolta selezionata.|  
|**Finestre di manutenzione**|Consente di visualizzare e configurare le finestre di manutenzione applicate ai membri della raccolta selezionata. Per altre informazioni, vedere [Come usare le finestre di manutenzione in System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md).|  
|**Variabili raccolta**|Consente di configurare le variabili che si applicano alla raccolta e che possono essere usate dalle sequenze di attività. Per altre informazioni, vedere [Variabili predefinite della sequenza di attività](../../../../osd/understand/task-sequence-built-in-variables.md).|  
|**Gruppi di punti di distribuzione**|Consente di associare uno o più gruppi di punti di distribuzione ai membri della raccolta selezionata. Per altre informazioni, vedere [Gestire il contenuto e l'infrastruttura del contenuto per System Center Configuration Manager](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Sicurezza**|Visualizza gli utenti amministratori che dispongono di autorizzazioni per la raccolta selezionata da ambiti di protezione e ruoli associati.|  
|**Monitoraggioaggio**|Consente di determinare quando vengono generati avvisi per lo stato del client ed Endpoint Protection. Per altre informazioni, vedere [Come configurare lo stato del client in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-status.md) e [Come monitorare Endpoint Protection in System Center Configuration Manager](../../../../protect/deploy-use/monitor-endpoint-protection.md).|  

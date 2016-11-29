---
title: "Attività di gestione per applicazioni di System Center Configuration Manager | System Center Configuration Manager"
description: Gestire le applicazioni e i tipi di distribuzione di System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c4041e21-21ff-4d95-ab05-14007e0047cf
caps.latest.revision: 8
author: robstackmsft
ms.author: robstack
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b8ecf5334304f0aaae62b3fa5d6f84da84d97799


---
# <a name="management-tasks-for-system-center-configuration-manager-applications"></a>Attività di gestione per applicazioni di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Usare le informazioni in questo argomento per gestire le applicazioni e i tipi di distribuzione di System Center Configuration Manager.  
  
Per altre informazioni sulla creazione di applicazioni e tipi di distribuzione, vedere [Create applications](../../apps/deploy-use/create-applications.md) (Creare le applicazioni).  
  
> [!IMPORTANT]  
>  A seconda del tipo di applicazione o distribuzione, alcune opzioni di gestione potrebbero non essere disponibili.  

##  <a name="manage-applications"></a>Gestire le applicazioni  
 Nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni** > **Applicazioni**, selezionare l'applicazione da gestire e quindi un'attività di gestione.  
  
|Attività|Dettagli|  
|----------|-------------|  
|**Gestione account di accesso**|Apre la finestra di dialogo **Gestione account di accesso** in cui è possibile specificare il livello di accesso consentito per il contenuto associato all'applicazione selezionata.|  
|**Crea file di contenuto di pre-installazione**|Apre la **Creazione guidata file di contenuto pre-installazione** che consente di gestire la distribuzione di contenuto nei punti di distribuzione remoti. Quando pianificazione e limitazione non rappresentano una valida soluzione per il punto di distribuzione remoto, è possibile pre-installare il contenuto nel punto di distribuzione<br /><br /> Vedere [Gestire il contenuto e l'infrastruttura del contenuto](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Cronologia revisioni**|Apre la finestra di dialogo **Cronologia revisione applicazione** che consente di visualizzare le proprietà delle revisioni effettuate su questa applicazione, di eliminare le precedenti revisioni dell'applicazione e ripristinare le versioni precedenti dell'applicazione.<br /><br /> Vedere [Come rivedere e sostituire le applicazioni](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Crea tipo di distribuzione**|Apre la **Creazione guidata tipo di distribuzione** che consente di aggiungere un nuovo tipo di distribuzione all'applicazione selezionata.<br /><br /> Vedere [Create applications](../../apps/deploy-use/create-applications.md) (Creare le applicazioni).|  
|**Aggiorna statistiche**|Aggiorna le informazioni visualizzate nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio** relativo alle applicazioni di questa applicazione.<br /><br /> Vedere [Monitorare le applicazioni dalla console di System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md).|  
|**Ripristina**|Questa opzione ripristina un'applicazione ritirata tramite l'attività di gestione **Ritira** .|  
|**Ritira**|Quando si ritira un'applicazione, questa non risulta più disponibile per la distribuzione ma non vengono eliminati né l'applicazione né le distribuzione dell'applicazione. Le copie esistenti di questa applicazione che sono state installate nei computer client non verranno rimosse. Eventuali revisioni dell'applicazione verranno eliminate da Configuration Manager dopo 60 giorni. Tuttavia, le copie installate dell'applicazione non verranno rimosse.<br /><br /> Per eliminare un'applicazione, è innanzitutto necessario ritirare l'applicazione, rimuovere qualsiasi distribuzione, rimuovere i relativi riferimenti da parte di altre distribuzioni e quindi eliminare tutte le relative revisioni.<br /><br /> Vedere [Come rivedere e sostituire le applicazioni](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Export**|Apre l' **Esportazione guidata applicazione** che consente di esportare le applicazioni selezionate in un file con estensione zip che è possibile archiviare o installare in un altro sito. Se si sceglie di esportare il contenuto dell'applicazione, verrà creata una cartella che conterrà il contenuto.<br /><br /> È inoltre possibile esportare le dipendenze dell'applicazione, le relazioni di sostituzione e condizioni e contenuto per applicazione e relative dipendenze.<br /><br /> Il cmdlet PowerShell di Windows, **Export-CMApplication**, esegue la stessa funzione. Per altre informazioni, vedere [http://go.microsoft.com/fwlink/p/?LinkID=258880](http://go.microsoft.com/fwlink/p/?LinkID=258880) nella documentazione di riferimento dei cmdlet di System Center 2012 Configuration Manager SP1.|  
|**Eliminazione**|Elimina l'applicazione attualmente selezionata.<br /><br /> Non è possibile eliminare un'applicazione se esistono altre applicazioni da essa dipendenti, se è presente una distribuzione attiva o se esistono sequenze attività da essa dipendenti.|  
|**Simula distribuzione**|Apre la **Simulazione guidata distribuzione applicazione** in cui è possibile testare i risultati di una distribuzione di applicazione nei computer senza installare o disinstallare l'applicazione.<br /><br /> Vedere [Come simulare distribuzioni di applicazioni](../../apps/deploy-use/simulate-application-deployments.md).|  
|**Distribuisci**|Apre la **Distribuzione guidata del software** in cui è possibile distribuire l'applicazione selezionata nelle raccolte di computer presenti nella gerarchia.<br /><br /> Vedere [Come distribuire le applicazioni](../../apps/deploy-use/deploy-applications.md).|  
|**Distribuisci contenuto**|Apre la **Distribuzione guidata contenuto** in cui è possibile copiare il contenuto dell'applicazione selezionata nei punti di distribuzione presenti nella gerarchia.<br /><br /> Vedere [Gestire il contenuto e l'infrastruttura del contenuto](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Visualizza relazioni**|Visualizza un diagramma grafico che indica le relazioni delle applicazioni selezionate con altre applicazioni. Scegliere una delle seguenti opzioni:<br><br> - **Dipendenza**: visualizza le applicazioni che dipendono dall'applicazione e le applicazioni da cui dipende l'applicazione.<br>-                    **Sostituzione**: visualizza le applicazioni che vengono sostituite e le applicazioni con cui l'elemento selezionato è stato sostituito.<br>- **Condizioni globali**: visualizza le condizioni globali a cui fa riferimento l'applicazione.<br /><br /> Vedere [Come rivedere e sostituire le applicazioni](../../apps/deploy-use/revise-and-supersede-applications.md) e [Come creare condizioni globali](../../apps/deploy-use/create-global-conditions.md).|  
  
##  <a name="manage-deployment-types"></a>Gestire i tipi di distribuzione  
 Nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni**, selezionare **Applicazioni**e quindi l'applicazione che contiene il tipo di distribuzione che si desidera gestire. Quindi, nel riquadro dei dettagli fare clic sulla scheda **Tipi di distribuzione** , selezionare il tipo di distribuzione da gestire e quindi selezionare un'attività di gestione.  
  
|Attività|Dettagli|  
|----------|-------------|  
|**Aumenta priorità**|Aumenta la priorità del tipo di distribuzione selezionato. I tipi di distribuzione vengono valutati in ordine. Quando un tipo di distribuzione soddisfa i requisiti specificati, questo verrà eseguito e non verranno valutati ulteriori tipi di distribuzione nell'elenco delle priorità.|  
|**Diminuisci priorità**|Diminuisce la priorità del tipo di distribuzione selezionato.|  
|**Eliminazione**|Elimina il tipo di distribuzione selezionato.<br><br>Non è possibile eliminare un tipo di distribuzione se esiste un relativo riferimento da parte di un tipo di distribuzione in un'altra applicazione.<br>Per eliminare un tipo di distribuzione, è necessario rimuovere tutte le dipendenze al tipo di distribuzione contenute in altri tipi di distribuzione.<br>È anche possibile rimuovere revisioni precedenti di qualsiasi applicazione che contiene un tipo di distribuzione che fa riferimento al tipo di distribuzione che si desidera eliminare.|  
|**Aggiornamento contenuto**|Aggiorna il contenuto per il tipo di distribuzione selezionato.<br /><br /> Quando si avvia questa procedura guidata per un tipo di distribuzione che contiene un'applicazione virtuale, viene avviato l' **Aggiornamento guidato contenuto** . Questa procedura guidata consente di modificare le opzioni di pubblicazione e regole relative ai requisiti per l'applicazione virtuale selezionata. Per altre informazioni, vedere [Create applications](../../apps/deploy-use/create-applications.md) (Creare le applicazioni).<br /><br /> Quando si aggiorna il contenuto di un tipo di distribuzione, viene creata una nuova revisione dell'applicazione. Ciò potrebbe causare l'aggiornamento di dispositivi client con la nuova applicazione.|  
  




<!--HONumber=Nov16_HO1-->



---
title: Introduzione alle raccolte | System Center Configuration Manager
description: Introduzione all'uso delle raccolte in System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
caps.latest.revision: 8
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 47574218dec5069205f9dba5608c6f136fb032bc


---
# <a name="introduction-to-collections-in-system-center-configuration-manager"></a>Introduzione alle raccolte in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In System Center Configuration Manager le raccolte forniscono gli strumenti per organizzare le risorse in unità gestibili, che consentono a loro volta di creare una struttura organizzata che offre una rappresentazione logica dei tipi di attività da eseguire. Le raccolte vengono usate anche per eseguire operazioni di Configuration Manager su più risorse contemporaneamente. La tabella seguente illustra alcuni esempi di possibili usi delle raccolte in Configuration Manager:  

|Operazione|Esempio|  
|---------|-------|  
|Raggruppamento di risorse|È possibile creare raccolte per il raggruppamento logico delle risorse in base alla gerarchia dell'organizzazione.<br /><br /> Ad esempio, si potrebbe creare una raccolta di tutti i computer che risiedono nell'unità organizzativa (OU) di Active Directory "Sede centrale Milano". Per altre informazioni su come creare questo tipo di raccolta, vedere [Come creare le raccolte in System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).<br /><br /> Si potrebbe poi usare questa raccolta per eseguire operazioni quali la configurazione delle impostazioni di Endpoint Protection, la configurazione delle impostazioni di risparmio energia per i dispositivi o l'installazione del client di Configuration Manager.|  
|Distribuzione delle applicazioni|È possibile creare una raccolta di tutti i computer in cui non è installato Microsoft Office 2013 e quindi distribuire questo software in tutti i computer di tale raccolta.<br /><br /> È anche possibile usare i requisiti dell'applicazione per eseguire questa attività. Per altre informazioni, vedere [Come creare applicazioni con System Center Configuration Manager](../../../../apps/deploy-use/create-applications.md).|  
|Gestione delle impostazioni client|Sebbene le impostazioni client predefinite in Configuration Manager siano valide per tutti i dispositivi e tutti gli utenti, è possibile creare impostazioni client personalizzate applicabili a una raccolta di dispositivi o a una raccolta di utenti.<br /><br /> Ad esempio, se si vuole che il controllo remoto sia disponibile in tutti i dispositivi a parte alcuni, configurare le impostazioni client predefinite per consentire il controllo remoto e quindi configurare le impostazioni client personalizzate che non consentono il controllo remoto. Distribuire queste impostazioni client personalizzate in una raccolta che contiene i computer che non useranno il controllo remoto.<br /><br /> Per altre informazioni su come usare le raccolte per le impostazioni client, vedere [Informazioni sulle impostazioni client in Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).|  
|Risparmio energia|Per ogni raccolta creata, è possibile configurare le impostazioni di risparmio energia, ad esempio stabilire dopo quanto tempo di inattività viene attivata la modalità sospensione per i computer nella raccolta.<br /><br /> Per altre informazioni sull'uso di raccolte con risparmio energia, vedere [Introduzione al risparmio energia](../power/introduction-to-power-management.md).|  
|Amministrazione basata su ruoli|Le raccolte possono essere usate con l'amministrazione basata su ruoli per controllare i gruppi di utenti con accesso a varie funzionalità nella console di Configuration Manager.<br /><br /> Per altre informazioni su come configurare raccolte per l'amministrazione basata su ruoli, vedere [Configure role-based administration for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md) (Configurare l'amministrazione basata su ruoli per System Center Configuration Manager).|  
|Finestre di manutenzione|Le finestre di manutenzione possono essere usate dagli utenti amministratori per definire un periodo di tempo in cui eseguire diverse operazioni di Configuration Manager sui membri di una raccolta di dispositivi. È possibile usare le finestre di manutenzione per garantire che le modifiche alla configurazione client vengano eseguite quando non influiscono sulla produttività dell'organizzazione.<br /><br /> Per altre informazioni sulle finestre di manutenzione, vedere [Come usare le finestre di manutenzione in System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md).|  

 La maggior parte delle attività di gestione si basa sull'uso di una o più raccolte. Ad esempio, prima di poter distribuire gli aggiornamenti software ai dispositivi, è necessario identificare una raccolta per la distribuzione degli aggiornamenti software. Sebbene sia possibile usare la raccolta predefinita Tutti i sistemi, l'uso di questa raccolta per le attività di gestione non è consigliato. In tutti gli ambienti tranne quelli di testing, è in genere più vantaggioso creare raccolte personalizzate per identificare in modo più specifico i dispositivi o gli utenti da gestire.  

 Le raccolte predefinite e personalizzate vengono visualizzate nei nodi **Raccolte utenti** e **Raccolte dispositivi** nell'area di lavoro **Asset e conformità** nella console di Configuration Manager.  

 Le raccolte visualizzate di recente sono disponibili nel nodo **Utenti** e nel nodo **Dispositivi** nell'area di lavoro **Asset e conformità** nella console di Configuration Manager.  

## <a name="collection-types-in-configuration-manager"></a>Tipi di raccolta in Configuration Manager  
 Configuration Manager include alcune raccolte predefinite che è possibile usare per le operazioni più comuni. È anche possibile creare raccolte personalizzate che raggruppano risorse specifiche per i requisiti aziendali.  

### <a name="built-in-collections"></a>Raccolte predefinite  
 Per impostazione predefinita, Configuration Manager include le raccolte seguenti, che non possono essere modificate.  

|**Nome raccolta**|Descrizione|  
|-------------------------|-----------------|  
|**Tutti i gruppi utente**|Contiene i gruppi di utenti individuati tramite individuazione gruppo di protezione Active Directory.|  
|**Tutti gli utenti**|Contiene gli utenti individuati tramite individuazione utente Active Directory.|  
|**Tutti gli utenti e gruppi utente**|Contiene le raccolte Tutti gli utenti e Tutti i gruppi utente. Questa raccolta non può essere modificata e contiene l'ambito più grande di risorse utenti e gruppi di utenti.|  
|**Tutti i client desktop e di server**|Contiene i dispositivi desktop e server in cui è installato il client di Configuration Manager. L'appartenenza viene gestita tramite l'individuazione heartbeat.|  
|**Tutti i dispositivi mobili**|Contiene i dispositivi mobili gestiti da Configuration Manager. L'appartenenza è limitata ai dispositivi mobili assegnati correttamente a un sito o individuati dal connettore Exchange Server.|  
|**Tutti i sistemi**|Contiene le raccolte Tutti i client desktop e di server, Tutti i dispositivi mobili, Tutti i computer sconosciuti e tutti i dispositivi mobili registrati da Microsoft Intune.<br /><br /> Questa raccolta non può essere modificata e contiene l'ambito più grande di risorse dispositivi.|  
|**Tutti i computer sconosciuti**|Contiene i record di computer generici per piattaforme di computer multiple. È possibile usare questa raccolta per distribuire un sistema operativo tramite una sequenza di attività e l'avvio PXE, un supporto di avvio o un supporto preinstallato.|  

### <a name="custom-collections"></a>Raccolte personalizzate  
 Quando si crea una raccolta personalizzata in Configuration Manager, l'appartenenza di tale raccolta viene determinata da una o più regole di raccolta. Per informazioni su come configurare le regole di raccolta, vedere [Come creare le raccolte in System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md). Sono disponibili quattro regole che è possibile usare:  

#### <a name="direct-rule"></a>Regola diretta  
 Le regole dirette consentono di scegliere gli utenti o i computer da aggiungere come membri di una raccolta. Questa regola offre il controllo diretto delle risorse che fanno parte della raccolta. Questa appartenenza non cambia automaticamente a meno che una risorsa non venga rimossa da Configuration Manager. Prima di poter aggiungere le risorse a una raccolta con regole dirette, è necessario importarle o che vengano individuate da Configuration Manager. Le raccolte con regole dirette presentano un maggiore carico amministrativo rispetto alle raccolte con regole di query, perché è necessario modificare manualmente questo tipo di raccolta.  

#### <a name="query-rule"></a>Regola di query  
 Le regole di query aggiornano in modo dinamico l'appartenenza di una raccolta con una query eseguita da Configuration Manager in base a una pianificazione. Ad esempio, è possibile creare una raccolta degli utenti membri dell'unità organizzativa Risorse umane in Servizi di dominio Active Directory. Diversamente dalle raccolte con regole dirette, le appartenenze vengono aggiornate automaticamente in seguito all'aggiunta o alla rimozione di nuovi utenti nell'unità organizzativa Risorse umane. Le regole di query consentono di evitare il carico amministrativo correlato all'aggiunta manuale di dispositivi alla raccolta tramite una regola diretta. Tuttavia, si dispone di un minore controllo sui computer aggiunti alla raccolta. Ecco alcuni esempi di regole basate su query:  

-   Tutti gli utenti in un'unità organizzativa specificata  

-   Tutti i computer che eseguono Windows 8  

-   Tutti i computer che dispongono di più di 20 GB di spazio libero su disco  

#### <a name="include-collections-rule"></a>Regola di inclusione raccolte  
 La regola di inclusione raccolte consente di includere i membri di un'altra raccolta in una raccolta di Configuration Manager. Configuration Manager aggiorna l'appartenenza della raccolta corrente in base a una pianificazione in caso di modifica delle appartenenze della raccolta inclusa.  

#### <a name="exclude-collections-rule"></a>Regola di esclusione raccolte  
 La regola di esclusione raccolte consente di escludere i membri di un'altra raccolta da una raccolta di Configuration Manager. Configuration Manager aggiorna l'appartenenza della raccolta corrente in base a una pianificazione in caso di modifica delle appartenenze della raccolta esclusa.  

> [!NOTE]  
>  Se una raccolta include sia regole di inclusione raccolte che di esclusione raccolte e si verifica un conflitto, la regola di esclusione ha la priorità sulla regola di inclusione.  

## <a name="incremental-collection-updates"></a>Aggiornamenti incrementali della raccolta  
 Quando si abilitano gli aggiornamenti incrementali per una raccolta, Configuration Manager esegue periodicamente un'analisi per individuare eventuali risorse nuove o modificate rispetto alla precedente valutazione raccolta e aggiorna l'appartenenza alla raccolta con tali risorse, indipendentemente da una valutazione raccolta completa. Per impostazione predefinita, quando si attiva aggiornamenti incrementali insieme, viene eseguito ogni 5 minuti e aiuta a mantenere aggiornati senza l'overhead di una valutazione raccolta completa dei dati di raccolta.  

> [!NOTE]  
>  Quando si crea una nuova raccolta, gli aggiornamenti incrementali sono disabilitati per impostazione predefinita.  



<!--HONumber=Nov16_HO1-->



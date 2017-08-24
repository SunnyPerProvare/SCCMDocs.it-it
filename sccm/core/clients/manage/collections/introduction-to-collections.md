---
title: Introduzione alle raccolte | Documentazione Microsoft
description: Introduzione all'uso delle raccolte in System Center Configuration Manager.
ms.custom: na
ms.date: 01/03/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
caps.latest.revision: "8"
author: andredm7
ms.author: andredm
manager: angrobe
ms.openlocfilehash: 547d231d48ccbc8241e9f1f8f71e3750b266b73e
ms.sourcegitcommit: 51fc48fb023f1e8d995c6c4eacfda7dbec4d0b2f
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/07/2017
---
# <a name="introduction-to-collections-in-system-center-configuration-manager"></a>Introduzione alle raccolte in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le raccolte consentono di organizzare le risorse in unità gestibili. È possibile creare raccolte in base alle esigenze di gestione dei client e per eseguire operazioni su più risorse contemporaneamente. 

La maggior parte delle attività di gestione dipende o richiede l'uso di una o più raccolte. Sebbene sia possibile usare la raccolta predefinita Tutti i sistemi, l'uso di questa raccolta per le attività di gestione non è consigliato. Creare raccolte personalizzate per identificare in modo più specifico i dispositivi o gli utenti per un'attività.  

 Le raccolte predefinite e personalizzate vengono visualizzate nei nodi **Raccolte utenti** e **Raccolte dispositivi** nell'area di lavoro **Asset e conformità** nella console di Configuration Manager.  

 Le raccolte visualizzate di recente sono disponibili nel nodo **Utenti** e nel nodo **Dispositivi** nell'area di lavoro **Asset e conformità**.  

Di seguito sono descritti alcuni esempi di uso delle raccolte:  

|Operazione|Esempio|  
|---------|-------|  
|Raggruppamento di risorse|È possibile creare raccolte per il raggruppamento delle risorse in base alla gerarchia dell'organizzazione.<br /><br /> Ad esempio, si potrebbe creare una raccolta di tutti i computer nell'unità organizzativa (OU) di Active Directory "Sede centrale Milano". Per altre informazioni su come creare questo tipo di raccolta, vedere [Come creare le raccolte in System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).<br /><br /> Si potrebbe usare questa raccolta per operazioni quali la configurazione delle impostazioni di Endpoint Protection, la configurazione delle impostazioni di risparmio energia per i dispositivi o l'installazione del client di Configuration Manager.|  
|[Distribuzione delle applicazioni]|È possibile creare una raccolta di tutti i computer in cui non è installato Microsoft Office 2013 e quindi distribuirlo in tutti i computer di tale raccolta.<br /><br /> È anche possibile usare i requisiti dell'applicazione per eseguire questa attività. Per altre informazioni, vedere [Come creare applicazioni con System Center Configuration Manager](../../../../apps/deploy-use/create-applications.md).|  
|[Gestione delle impostazioni client](../../../../core/clients/deploy/about-client-settings.md)|Sebbene le impostazioni client predefinite in Configuration Manager siano valide per tutti i dispositivi e tutti gli utenti, è possibile creare impostazioni client personalizzate applicabili a una raccolta di dispositivi o a una raccolta di utenti.<br /><br /> Ad esempio, se si vuole che il controllo remoto sia disponibile in tutti i dispositivi a parte alcuni, configurare impostazioni client predefinite per consentire il controllo remoto e quindi configurare impostazioni client personalizzate che non consentono il controllo remoto e distribuirle alla raccolta dei client che rappresentano l'eccezione. |  
|[Risparmio energia](../power/introduction-to-power-management.md)|È possibile configurare impostazioni di risparmio energia specifiche per ogni raccolta.|  
|[Amministrazione basata su ruoli](../../../../core/servers/deploy/configure/configure-role-based-administration.md)|Usare le raccolte per controllare i gruppi di utenti con accesso a varie funzionalità nella console di Configuration Manager.|  
|[Finestre di manutenzione](../../../../core/clients/manage/collections/use-maintenance-windows.md)|Con le finestre di manutenzione è possibile definire un periodo di tempo in cui eseguire diverse operazioni di Configuration Manager sui membri di una raccolta di dispositivi. |  


## <a name="collection-types-in-configuration-manager"></a>Tipi di raccolta in Configuration Manager  
 Configuration Manager include alcune raccolte predefinite per operazioni comuni ed è anche possibile creare raccolte personalizzate.   

### <a name="built-in-collections"></a>Raccolte predefinite  
 Per impostazione predefinita, Configuration Manager include le raccolte seguenti, che non possono essere modificate.  

|**Nome raccolta**|Descrizione|  
|-------------------------|-----------------|  
|**Tutti i gruppi utente**|Contiene i gruppi di utenti individuati tramite individuazione gruppo di protezione Active Directory.|  
|**Tutti gli utenti**|Contiene gli utenti individuati tramite individuazione utente Active Directory.|  
|**Tutti gli utenti e gruppi utente**|Contiene le raccolte Tutti gli utenti e Tutti i gruppi utente. Questa raccolta contiene l'ambito più grande di risorse utenti e gruppi di utenti.|  
|**Tutti i client desktop e di server**|Contiene i dispositivi desktop e server in cui è installato il client di Configuration Manager. L'appartenenza viene gestita tramite l'individuazione heartbeat.|  
|**Tutti i dispositivi mobili**|Contiene i dispositivi mobili gestiti da Configuration Manager. L'appartenenza è limitata ai dispositivi mobili assegnati correttamente a un sito o individuati dal connettore Exchange Server.|  
|**Tutti i sistemi**|Contiene le raccolte Tutti i client desktop e di server, Tutti i dispositivi mobili, Tutti i computer sconosciuti e tutti i dispositivi mobili registrati da Microsoft Intune. Questa raccolta contiene l'ambito più grande di risorse dispositivi.|  
|**Tutti i computer sconosciuti**|Contiene i record di computer generici per piattaforme di computer multiple. È possibile usare questa raccolta per distribuire un sistema operativo tramite una sequenza di attività e l'avvio PXE, un supporto di avvio o un supporto preinstallato.|  

### <a name="custom-collections"></a>Raccolte personalizzate  
 Quando si crea una raccolta personalizzata in Configuration Manager, l'appartenenza di tale raccolta viene determinata da una o più regole di raccolta, come descritto in [Come creare le raccolte in System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md). 


---
title: Funzionalità di versioni non definitive
titleSuffix: Configuration Manager
description: Le funzionalità di versioni non definitive sono incluse nel Current Branch a scopo di test preliminare in un ambiente di produzione.
ms.date: 10/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e3b3b31c31725c6b9931d0c2cc67324c4b39f974
ms.sourcegitcommit: 8791bb9be477fe6a029e8a7a76e2ca310acd92e0
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/31/2018
ms.locfileid: "50411137"
---
# <a name="pre-release-features-in-configuration-manager"></a>Funzionalità di versioni non definitive in Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le funzionalità di versioni non definitive sono incluse nel Current Branch a scopo di test preliminare in un ambiente di produzione. Queste funzionalità sono completamente supportate, ma ancora in fase di sviluppo attivo. Potrebbero essere soggette a modifiche fino a quando non vengono spostate dalla categoria Versioni non definitive.



## <a name="give-consent"></a>Dare il consenso  

Prima di usare le funzionalità di versioni non definitive, dare il consenso all'uso di funzionalità di versioni non definitive. L'azione con cui si dà il consenso viene eseguita una sola volta per ogni gerarchia e non può essere annullata. Finché non viene dato il consenso, non è possibile abilitare le nuove funzionalità di versioni non definitive incluse negli aggiornamenti. Dopo l'attivazione di una funzione non definitiva, non è possibile procedere alla relativa disattivazione.

1. Nella console di Configuration Manager passare all'area di lavoro **Amministrazione**, espandere **Configurazione del sito** e selezionare **Siti**.  

2. Fare clic su **Impostazioni gerarchia** sulla barra multifunzione.  

3. Nella scheda **Generale** di Proprietà delle impostazioni di gerarchia abilitare l'opzione **Consenso a usare funzionalità di versioni non definitive**. Fare clic su **OK**.  



## <a name="enabling-pre-release-features"></a>Abilitazione di funzionalità di versioni non definitive

Durante l'installazione di un aggiornamento che include funzionalità di versioni non definitive, tali funzionalità sono visibili nella procedura guidata Aggiornamenti e manutenzione insieme alle normali funzionalità incluse nell'aggiornamento.

#### <a name="if-you-have-given-consent"></a>Se è stato dato il consenso
Nella procedura guidata Aggiornamenti e manutenzione abilitare le funzionalità di versioni non definitive. Selezionare le funzionalità di versioni non definitive allo stesso modo in cui si selezionano le altre funzionalità.     

È facoltativamente possibile abilitare in un secondo momento le funzionalità di versioni non definitive dal nodo **Funzionalità** in **Aggiornamenti e manutenzione** nell'area di lavoro **Amministrazione**. Selezionare una funzione e quindi fare clic su **Attiva** nella barra multifunzione. Fino a quando non viene dato il consenso, questa opzione non è disponibile per l'uso.

#### <a name="if-you-havent-given-consent"></a>Se non è stato dato il consenso
Nella procedura guidata Aggiornamenti e manutenzione le funzionalità di versioni non definitive sono visibili, ma non è possibile abilitarle. Dopo l'installazione dell'aggiornamento, queste funzionalità sono visibili nel nodo **Funzionalità**. Non è tuttavia possibile abilitarle finché non si dà il consenso.


> [!Important]  
> In una gerarchia a più siti è possibile abilitare le funzionalità facoltative o di versioni non definitive solo dal sito di amministrazione centrale. Questo comportamento assicura che non ci siano conflitti all'interno della gerarchia. <!--507197-->  
> 
> Se, dopo aver dato il consenso a un sito primario autonomo, si espande la gerarchia installando un nuovo sito di amministrazione centrale, è necessario dare di nuovo il consenso al sito di amministrazione centrale.  

Quando si abilita una funzionalità non definitiva, gestione gerarchie (HMAN) di Configuration Manager deve elaborare la modifica prima che tale funzionalità diventi disponibile. L'elaborazione della modifica è spesso immediata. A seconda del ciclo di elaborazione HMAN, possono essere necessari fino a 30 minuti. Dopo l'elaborazione della modifica, riavviare la console prima di usare la funzionalità.



## <a name="pre-release-features"></a>Funzionalità di versioni non definitive

<!--Note/tip for target article

> [!Note]  
> In this version of Configuration Manager, <feature name> is a pre-release feature. To enable it, see [Pre-release features](/sccm/core/servers/manage/pre-release-features).  


> [!Tip]  
> This feature was first introduced in version 1702 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). Beginning with version 1706, this feature is no longer a pre-release feature.  

-->


| Funzionalità          | Aggiunta come versione non definitiva | Aggiunta come funzionalità completa |  
|------------------|----------------------|-------------------------|
| Sistema del sito HTTP migliorato<!--1356889,1358228-->|[Versione 1806](/sccm/core/plan-design/hierarchy/enhanced-http)|![Non ancora](media/red_x.png)|
| App per dispositivi mobili per dispositivi con co-gestione<!--1357892-->|[Versione 1806](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune)|![Non ancora](media/red_x.png)|
| Package Conversion Manager<!--1357861-->|[Versione 1806](/sccm/apps/pcm/package-conversion-manager)|![Non ancora](media/red_x.png)|
| Supporto per Cisco AnyConnect 4.0.07x e versioni successive per iOS<!--1357393-->|[Versione 1802](/sccm/mdm/deploy-use/create-vpn-profiles)| [Versione 1802 con aggiornamento 4163547](/sccm/mdm/deploy-use/create-vpn-profiles) |
| Distribuzioni in più fasi <!--1356837-->|[Versione 1802](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|[Versione 1806](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)|
| Esegui il passaggio della sequenza di attività <!-- 1261338 --> |  [Versione 1710](/sccm/osd/understand/task-sequence-steps#child-task-sequence) |[Versione 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence)|
| Windows Defender Exploit Guard <!-- 1355468 --> |  [Versione 1710](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |[Versione 1802](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy)|
| Valutazione dell'attestazione dell'integrità dei dispositivi per i criteri di conformità dell'accesso condizionale <!-- 1235616 --> |  [Versione 1710](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) |[Versione 1802](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)|
| Creare ed eseguire script di PowerShell dalla console di Configuration Manager <!-- 1236459 --> |  [Versione 1706](/sccm/apps/deploy-use/create-deploy-scripts)|[Versione 1802](/sccm/apps/deploy-use/create-deploy-scripts)|
| Gestire gli aggiornamenti dei driver di Microsoft Surface <!-- 1098490 --> |  [Versione 1706](/sccm/sum/get-started/configure-classifications-and-products) | [Versione 1710](/sccm/sum/get-started/configure-classifications-and-products)|
| Gestione di Device Guard con Configuration Manager <!-- 1319346 --> |  [Versione 1702](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager)|![Non ancora](media/red_x.png)|
| Memorizzazione anticipata nella cache dei contenuti della sequenza di attività <!-- 1021244 --> |  [Versione 1702](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) | [Versione 1710](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content)|
| Controllare l'esecuzione di file eseguibili prima di installare un'applicazione <!-- 1284624 --> |   [Versione 1702](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) |[Versione 1706](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application)|
| Punto di servizio del data warehouse <!-- 1277922 --> |  [Versione 1702](/sccm/core/servers/manage/data-warehouse) |[Versione 1706](/sccm/core/servers/manage/data-warehouse)|
| Peer cache per la distribuzione del contenuto ai client <!-- 1101436 --> |  [Versione 1610](/sccm/core/plan-design/hierarchy/client-peer-cache) | [Versione 1710](/sccm/core/plan-design/hierarchy/client-peer-cache)|
| Gateway di gestione cloud <!-- 1101764 --> |  [Versione 1610](/sccm/core/clients/manage/plan-cloud-management-gateway) |[Versione 1802](/sccm/core/clients/manage/plan-cloud-management-gateway)|
| Connettore Log Analytics <!-- 1236739 --> | [Version 1606](/sccm/core/clients/manage/sync-data-log-analytics) |[Versione 1802](/sccm/core/clients/manage/sync-data-log-analytics)|
| Manutenzione di una raccolta compatibile con cluster (manutenzione di un gruppo di server) <!-- 1081776 --> | [Versione 1602](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_ServerGroups)|![Non ancora](media/red_x.png)|
| Accesso condizionale per i PC gestiti da System Center Configuration Manager <!--  --> | [Versione 1602](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)     | [Versione 1702](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)                     |
<!--Image used = ![Not yet](media/red_x.png) -->

> [!Tip]  
> Per altre informazioni sulle funzionalità di versioni non definitive che è necessario abilitare in prima istanza, vedere [Abilitare le funzionalità facoltative degli aggiornamenti](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
> 
> Per altre informazioni sulle funzionalità disponibili solo nel ramo Technical Preview, vedere [Technical Preview](/sccm/core/get-started/technical-preview).  

---
title: Funzionalità di versioni non definitive
titleSuffix: Configuration Manager
description: Le funzionalità di versioni non definitive sono incluse nel Current Branch a scopo di test preliminare in un ambiente di produzione.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4d892e8d194f61fece977c91ce36ba46cf9dd53d
ms.sourcegitcommit: a3cec96a771eed69e58a29917d1a3fe1a5fb2e73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/14/2019
ms.locfileid: "54250715"
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
| API provider SMS <!--1359052--> | Versione 1810 | ![Non ancora](media/red_x.png) |
| [Sistema del sito HTTP migliorato](/sccm/core/plan-design/hierarchy/enhanced-http) <!--1356889,1358228--> | Versione 1806 | Versione 1810 |
| [App client per dispositivi con co-gestione](/sccm/comanage/workloads#client-apps) <!--1357892--> | Versione 1806 | ![Non ancora](media/red_x.png) |
| [Package Conversion Manager](/sccm/apps/pcm/package-conversion-manager) <!--1357861--> | Versione 1806 | Versione 1810 |
| [Supporto per Cisco AnyConnect 4.0.07x e versioni successive per iOS](/sccm/mdm/deploy-use/create-vpn-profiles) <!--1357393--> | Versione 1802 | Versione 1802 <br>con aggiornamento 4163547 |
| [Distribuzioni in più fasi](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) <!--1356837--> | Versione 1802 | Versione 1806 |
| [Eseguire il passaggio della sequenza di attività](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence) <!--1261338--> |  Versione 1710 | Versione 1802 |
| [Windows Defender Exploit Guard](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) <!--1355468--> | Versione 1710 | Versione 1802 |
| [Valutazione dell'attestazione dell'integrità dei dispositivi per i criteri di conformità dell'accesso condizionale](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--1235616--> | Versione 1710 | Versione 1802 |
| [Creare ed eseguire script di Windows PowerShell](/sccm/apps/deploy-use/create-deploy-scripts) <!--1236459--> | Versione 1706 | Versione 1802 |
| [Gestire gli aggiornamenti dei driver di Microsoft Surface](/sccm/sum/get-started/configure-classifications-and-products) <!--1098490--> | Versione 1706 | Versione 1710 |
| [Gestione di Device Guard](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager) <!--1355092 (1319346)--> | Versione 1702 | ![Non ancora](media/red_x.png) |
| [Memorizzazione anticipata nella cache dei contenuti della sequenza di attività](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) <!--1021244--> | Versione 1702 | Versione 1710 |
| [Controllare l'esecuzione di file eseguibili prima di installare un'applicazione](/sccm/apps/deploy-use/deploy-applications#how-to-check-for-running-executable-files-before-installing-an-application) <!--1284624--> | Versione 1702 | Versione 1706 |
| [Punto di servizio del data warehouse](/sccm/core/servers/manage/data-warehouse) <!--1277922--> | Versione 1702 | Versione 1706 |
| [Peer cache per la distribuzione del contenuto ai client](/sccm/core/plan-design/hierarchy/client-peer-cache) <!--1101436--> | Versione 1610 | Versione 1710 |
| [Gateway di gestione cloud](/sccm/core/clients/manage/plan-cloud-management-gateway) <!--1101764--> | Versione 1610 | Versione 1802 |
| [Connettore di Azure Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics) <!--1236739--> | Versione 1606 | Versione 1802 |
| [Manutenzione di una raccolta compatibile con cluster (manutenzione di un gruppo di server)](/sccm/core/get-started/capabilities-in-technical-preview-1605#BKMK_ServerGroups) <!--1081776--> | Versione 1602 | ![Non ancora](media/red_x.png) |
| [Accesso condizionale per i PC gestiti da System Center Configuration Manager](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--  --> | Versione 1602 | Versione 1702 |

<!--Image used = ![Not yet](media/red_x.png) -->

> [!Tip]  
> Per altre informazioni sulle funzionalità di versioni non definitive che è necessario abilitare in prima istanza, vedere [Abilitare le funzionalità facoltative degli aggiornamenti](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
> 
> Per altre informazioni sulle funzionalità disponibili solo nel ramo Technical Preview, vedere [Technical Preview](/sccm/core/get-started/technical-preview).  

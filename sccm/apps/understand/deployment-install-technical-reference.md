---
title: Riferimento tecnico per l'installazione dell'applicazione
titleSuffix: Configuration Manager
description: Riferimento tecnico per la risoluzione dei problemi relativi alle installazioni di applicazioni per Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 2af4f9c3-16b8-4691-a59d-aea6241d288e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f1ba3702b45594be3047e10ee69f99eaf2391805
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "74823371"
---
# <a name="application-installation"></a>Installazione dell'applicazione

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima di continuare, esaminare i [componenti client di distribuzione delle applicazioni](/sccm/apps/understand/client-components-technical-reference) per comprendere l'elaborazione dei processi dell'agente ci e di DCM.

L'installazione dell'applicazione viene eseguita dai componenti dell'agente di DCM e dell'agente CI quando viene applicata la distribuzione. Il tempo di applicazione è diverso per le distribuzioni disponibili e richieste. Per informazioni sul momento in cui viene applicata l'assegnazione, vedere gli articoli [distribuzione di applicazioni in raccolte di dispositivi](/sccm/apps/understand/device-deployment-technical-reference) o [distribuzione di applicazioni negli insiemi di utenti](/sccm/apps/understand/user-deployment-technical-reference) .

## <a name="enforcement-initiation"></a>Avvio imposizione

L'installazione dell'applicazione viene avviata dal componente agente CI nel client durante la fase **StateEnforcingCIs** . Questo processo è lo stesso, indipendentemente dal fatto che l'applicazione venga distribuita a una raccolta di dispositivi o a una raccolta di utenti.

- Per le distribuzioni **disponibili** , l'applicazione viene installata quando l'utente avvia l'installazione dell'applicazione da software Center.
- Per le distribuzioni **richieste** , l'applicazione viene installata alla scadenza della distribuzione. Tuttavia, l'utente può avviare l'installazione da software Center prima della scadenza.

Quando l'agente CI avvia l'installazione dell'applicazione, crea un'attività che viene gestita dal componente di gestione attività CI. CI avvia l'installazione. Questa attività può essere rilevata in **CITaskMgr. log** utilizzando l'ID univoco del tipo di distribuzione.

<pre><code class="lang-text"><b>Initiating task Enforce</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {9BC3154A-98F1-4595-A967-173D536A3F94}
Initiated application enforcement. : CITask(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2..Install.Enforce)
</code></pre>

## <a name="application-enforcement"></a>Imposizione dell'applicazione

Dopo l'avvio dell'applicazione, il client esegue nuovamente il rilevamento dell'applicazione per assicurarsi che l'applicazione non sia già installata. Una volta determinato che l'applicazione non è installata, viene avviata l'installazione dell'applicazione. Questa attività può essere rilevata in **AppEnforce. log** nel client usando l'ID univoco del tipo di distribuzione.

```text
+++ Starting Install enforcement for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" ApplicationDeliveryType - ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision - 2, ContentPath - C:\WINDOWS\ccmcache\2, Execution Context - System
    Executing Command line: "C:\WINDOWS\system32\msiexec.exe" /i "ConfigMgrTools.msi" /q /qn with user context
    Process 7292 terminated with exitcode: 0
Status is switching to Success
```

## <a name="installation-verification"></a>Verifica dell'installazione

Dopo l'installazione dell'applicazione, il metodo di rilevamento dell'applicazione viene usato di nuovo per assicurarsi che l'applicazione sia stata rilevata come installata.

<pre><code class="lang-text">Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ <b>Discovered MSI application</b> [AppDT Id: ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, Revision: 2, MSI Product code: {4FFF7ECC-CCF7-4530-B938-E7812BB91186}, MSI Product version: ]
++++++ <b>App enforcement completed</b> (3 seconds) for App DT "ConfigMgr Toolkit - Windows Installer (*.msi file)" [ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44], Revision: 2, User SID: ] ++++++
</code></pre>

Infine, al termine dell'applicazione, l'agente CI riceve la notifica di completamento dell'attività e il processo dell'agente CI passa alla fase successiva.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateEnforcingCIs</b>)
</code></pre>

## <a name="next-steps"></a>Passaggi successivi

[Risoluzione dei problemi relativi alla distribuzione di applicazioni](/sccm/apps/deploy-use/troubleshoot-application-deployment)

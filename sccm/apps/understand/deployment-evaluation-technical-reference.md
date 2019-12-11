---
title: Riferimento tecnico per la valutazione delle applicazioni
titleSuffix: Configuration Manager
description: Risoluzione dei problemi di riferimento tecnico per la valutazione dell'applicazione per Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: a7035223-d7bd-47b4-896f-08de3416a4eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 32035f05c9bea47aa240e7b928e3171697aa07f7
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "74823321"
---
# <a name="application-deployment-evaluation"></a>Valutazione della distribuzione delle applicazioni

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima di continuare, esaminare i [componenti client di distribuzione delle applicazioni](/sccm/apps/understand/client-components-technical-reference) per comprendere l'elaborazione dei processi dell'agente ci e di DCM.

La valutazione dell'applicazione viene eseguita dai componenti dell'agente DCM e dell'agente CI al momento dell'attivazione della distribuzione. Per informazioni sull'attivazione dell'assegnazione, vedere gli articoli [distribuzione di applicazioni in raccolte di dispositivi](/sccm/apps/understand/device-deployment-technical-reference) o [distribuzione di applicazioni in raccolte di utenti](/sccm/apps/understand/user-deployment-technical-reference) .

## <a name="application-detection-and-evaluation"></a>Rilevamento e valutazione delle applicazioni

La valutazione dell'applicazione viene eseguita durante la fase **InvokingSdmMethod** di un processo dell'agente ci. Questa fase è il punto in cui il client valuta il metodo di rilevamento definito per l'applicazione per determinare se l'applicazione è installata nel dispositivo. Questa attività può essere rilevata in **AppDiscovery. log** usando l'ID univoco del tipo di distribuzione o il nome del tipo di distribuzione.

```text
Performing detection of app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
+++ Did not detect app deployment type ConfigMgr Toolkit - Windows Installer (*.msi file)(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44, revision 2) for system.
```

> [!NOTE]
> Nell'esempio precedente viene illustrato il rilevamento di un'applicazione MSI in cui il rilevamento viene eseguito controllando se il codice prodotto MSI è installato nel dispositivo. Per le applicazioni che usano metodi di rilevamento alternativi, viene usato il metodo di rilevamento appropriato per verificare se l'applicazione è installata.

Successivamente, il client valuta lo stato desiderato dell'applicazione in base allo scopo della distribuzione. Questo passaggio comporta inoltre il rilevamento della presenza di dipendenze o regole sostituzione che devono essere rispettate per l'applicazione. Questa attività può essere rilevata in **AppIntentEval. log** utilizzando l'ID univoco del tipo di distribuzione e dell'applicazione.

<pre><code class="lang-text"># Available Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Available</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Required Application Deployment

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = Applicable, ResolvedState = Installed</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]

# Requirement Rules Not Met

[Application or DT Unique ID] :- <b>Current State = NotInstalled, Applicability = NotApplicable, ResolvedState = None</b>, ConfigureState = NotNeeded, Title = [Application or DT Name]
</code></pre>

Nella voce di log precedente lo **stato corrente** indica se l'applicazione è attualmente installata nel dispositivo. **Applicabilità** indica se l'applicazione è applicabile in base alle regole requisiti definite. **ResolvedState** indica lo stato desiderato dell'applicazione in base allo scopo della distribuzione.

> [!TIP]
> Utilizzare lo [strumento di monitoraggio della distribuzione](/sccm/core/support/deployment-monitoring-tool) per visualizzare lo stato dell'applicazione, lo stato di applicabilità e le violazioni dei requisiti.

## <a name="next-steps"></a>Passaggi successivi

- [Download dell'applicazione](/sccm/apps/understand/deployment-download-technical-reference)

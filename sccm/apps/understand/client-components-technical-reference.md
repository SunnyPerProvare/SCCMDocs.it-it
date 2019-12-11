---
title: Riferimento tecnico per i componenti client di distribuzione delle applicazioni
titleSuffix: Configuration Manager
description: Componenti client utilizzati per la risoluzione dei problemi di distribuzione delle applicazioni in Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 701a3456-9dd6-4aaa-9c5a-37c1e1773216
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5f866859c785a6cfa14496948b92d9bac138bc64
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "74823461"
---
# <a name="understanding-application-deployment-client-components"></a>Informazioni sui componenti client di distribuzione delle applicazioni

*Si applica a: System Center Configuration Manager (Current Branch)*

Le operazioni di valutazione e applicazione della distribuzione dell'applicazione vengono gestite dai componenti dell'agente DCM e dell'agente CI nel client. Questo articolo illustra il funzionamento di un tipico processo dell'agente CI e di DCM.

## <a name="dcm-agent"></a>Agente DCM

L'agente DCM è il componente client di alto livello responsabile della valutazione degli elementi di configurazione, incluse le applicazioni. Quando una distribuzione viene attivata o applicata, viene creato un processo dell'agente DCM che legge i criteri di assegnazione e determina le azioni che devono essere eseguite. Questa attività può essere rilevata in **DCMAgent. log** nel client utilizzando l'ID processo dell'agente DCM, che può essere identificato cercando l'ID univoco dell'applicazione.

### <a name="device-deployments"></a>Distribuzioni di dispositivi

- Per le distribuzioni **richieste** , DCMAgent. log indicherebbe le azioni applicabili. Queste azioni possono variare a seconda che la scadenza della distribuzione sia già stata superata.

    ```text
    # Evaluation Job example:
    DCMAgentJob({A9E850E2-91B0-4122-94FD-D14EDF925AF7}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({4C8A9F6E-390B-450E-B505-B5698DB68EDD}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- Per le distribuzioni **disponibili** , DCMAgent. log indica che la distribuzione `is not mandatory`. Per queste distribuzioni, la valutazione dell'applicazione viene eseguita, ma l'applicazione viene ignorata a meno che l'utente non abbia avviato l'installazione.

    ```text
    # Evaluation Job example:
    DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/RequiredApplication_fc76ef0a-3ab0-4110-8cce-1addc36d0225 version:3 - Assignment:{3AC57DFE-3F87-4C59-930B-B9F57CB41B91} is not mandatory.

    # Enforcement Job (user initiated) example:
    Request to enforce application ConfigMgr Toolkit(ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/Application_fc76ef0a-3ab0-4110-8cce-1addc36d0225.3) immediately for target: machine with action(s): Evaluation, Install, Update
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {D331249E-F7DE-481B-A497-8E8B5E7B91C3}

    ```

### <a name="user-deployments"></a>Distribuzioni utente

- Per le distribuzioni **richieste** , DCMAgent. log indicherebbe le azioni applicabili. Queste azioni possono variare a seconda che la scadenza della distribuzione sia già stata superata.

    ```text
    # Evaluation Job example:
    DCMAgentJob({65D9688D-1781-4DA3-B07A-193D481251C6}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Content Download

    # Enforcement Job example:
    DCMAgentJob({2B0DA272-FC65-4F31-9557-C4D840D650F1}): CDCMAgentJob::PopulateCIsFromAssignment - CI policy Id:ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 with actions: Evaluation, Install, Uninstall, Update, Look-ahead Install, Look-ahead Uninstall, Look-ahead Update
    ```

- Per le distribuzioni **disponibili** , i processi dell'agente DCM vengono creati per la valutazione e l'imposizione quando l'installazione dell'applicazione viene avviata dall'utente.

    ```text
    # Evaluation Job example:
    DCMAgentJob({FBB44C84-DB06-41F7-8DC1-D9BA368F0C20}): CDCMAgentJob::PopulateCIsFromAssignment - [SCAN] CI policy Id :ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98 version:2 - Assignment:{7EA17128-EB4F-448A-88A7-B865E7DA228C} is not mandatory.

    # Enforcement Job example:
    CAppMgmtSDK::EnforceAppPolicy ScopeId_C8F7EAE6-DBA8-4970-B3FF-47ED706868DE/RequiredApplication_6b39398b-fd20-47ca-bd68-074274509f98.
    CDCMAgentJobMgr::CreateInteractiveJob - Queuing new job: {7936D7F3-24B0-401D-BADD-59EB5B49C2C2}
    ```

## <a name="ci-agent"></a>Agente CI

L'agente CI è il componente client responsabile della valutazione e della correzione degli elementi di configurazione. L'agente DCM legge i criteri di assegnazione e crea un processo per il componente dell'agente CI per eseguire le azioni richieste. **DCMAgent. log** registra l'ID del processo dell'agente ci, che è utile per tenere traccia dell'attività dell'agente ci in **ciagent. log** nel client.

<pre><code class="lang-text">DCMAgentJob({E353BF94-D7ED-4ADD-AF0F-9273F6A67FC1}): CDCMAgent::InitiateCIAgentJob - <b>Starting CI Agent Job</b> {57AF6FA1-3482-4469-9881-A63F41D18406} for target: machine. Refer to this CI agent job ID in ciagent.log for more details
</code></pre>

Un tipico processo dell'agente CI passa attraverso più fasi, che possono essere identificate filtrando **ciagent. log** sull'ID del processo dell'agente ci e cercando `TransitionState`. Di seguito sono riportate alcune delle fasi principali per un processo di agente CI della distribuzione dell'applicazione:

- **DownloadingCIs**
  - Durante questa fase, i metadati dell'applicazione necessari per valutare l'applicazione vengono scaricati. I metadati includono il metodo di rilevamento, le regole dei requisiti, le condizioni globali e così via. Questa attività può essere rilevata in **CIDownloader. log** e **DataTransferService. log**. Per le distribuzioni **disponibili** , questo processo si verifica durante la prima valutazione dell'applicazione. Per le distribuzioni **richieste** , tuttavia, questo processo si verifica immediatamente dopo il download del criterio.

- **InvokingSdmMethod**
  - Durante questa fase, il metodo di rilevamento dell'applicazione viene utilizzato per verificare se l'applicazione è installata e viene determinato lo stato desiderato. Questa attività può essere rilevata in **AppDiscovery. log** e **AppIntentEval. log**. Per ulteriori informazioni su questa fase, vedere la pagina relativa alla [valutazione dell'applicazione](/sccm/apps/understand/deployment-evaluation-technical-reference).

- **StateDownloadingContents**
  - Durante questa fase, il contenuto dell'applicazione viene scaricato se necessario. Questa attività può essere rilevata in **CAS. log**, **ContentTransferManager. log**, **LocationServices. log**e **DataTransferService. log**. Per ulteriori informazioni su questa fase, vedere [download dell'applicazione](/sccm/apps/understand/deployment-download-technical-reference).

- **StateEnforcingCIs**
  - Durante questa fase, viene avviata l'installazione dell'applicazione. Questa attività può essere rilevata in **AppEnforce. log**. Per ulteriori informazioni su questa fase, vedere [installazione dell'applicazione](/sccm/apps/understand/deployment-install-technical-reference).

- **StateEnforcementReporting**
  - Durante questa fase, lo stato di installazione dell'applicazione viene registrato per la creazione di report nel punto di gestione. Questa attività può essere rilevata in **StateMessage. log**.

Sebbene il processo dell'agente CI attraversi tutte le fasi, ignora la fase se non è obbligatorio. Per le distribuzioni **disponibili** , ad esempio, le fasi StateDownloadingContents e StateEnforcingCIs vengono ignorate fino a quando l'utente non tenta di installare l'applicazione da software Center. Tuttavia, per le distribuzioni **richieste** , la fase StateDownloadingContents Scarica il contenuto dell'applicazione (se necessario) quando l'assegnazione viene attivata, ma la fase StateEnforcingCIs viene ignorata se la scadenza è in futuro. Questo comportamento può essere osservato in CIAgent. log filtrando l'ID del processo dell'agente CI e cercando `Skipping policy`.

```text
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for ContentDownload task since CI action was not requested.
{57AF6FA1-3482-4469-9881-A63F41D18406} - Skipping policy CI <CI Unique ID> and all dependents for Enforce task since CI action was not requested.
```

## <a name="next-steps"></a>Passaggi successivi

- [Valutazione dell'applicazione](/sccm/apps/understand/deployment-evaluation-technical-reference)
- [Download dell'applicazione](/sccm/apps/understand/deployment-download-technical-reference)
- [Installazione delle applicazioni](/sccm/apps/understand/deployment-install-technical-reference)

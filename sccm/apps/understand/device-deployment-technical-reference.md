---
title: Riferimento tecnico per la distribuzione di app a raccolte dispositivi
titleSuffix: Configuration Manager
description: Risoluzione dei problemi relativi alle distribuzioni di applicazioni per le raccolte di dispositivi riferimento tecnico per Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 4e62b04d-fe56-42ed-87dc-e673cf061d52
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d4a5da90d807601fbbc7d29de225f04cd944df9f
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75825286"
---
# <a name="application-deployment-for-device-collections"></a>Distribuzione di applicazioni per le raccolte di dispositivi

*Si applica a: Configuration Manager (Current Branch)*

Quando un'applicazione viene distribuita in una raccolta dispositivi, il criterio è destinato a tutti i dispositivi nella raccolta indipendentemente dallo scopo della distribuzione. Questo articolo illustra il download dei criteri e l'elaborazione della distribuzione nel client.

> [!TIP]
> Tutte le informazioni necessarie per esaminare i log del client possono essere ottenute eseguendo la query SQL a cui viene fatto riferimento nella sezione [prima di iniziare](/sccm/apps/understand/app-deployment-technical-reference#before-you-begin) .

## <a name="policy-download"></a>Download dei criteri

Dopo che il criterio per la distribuzione dell'applicazione è destinato al client, il client scaricherà il criterio al successivo ciclo di polling dei criteri. Quando il client Scarica il criterio, Scarica i criteri correlati oltre ai criteri di distribuzione. Questi criteri correlati includono i criteri per l'applicazione, il tipo di distribuzione, le condizioni globali e così via. È possibile tenere traccia dell'attività di download dei criteri in **policyagent. log** nel client, usando l'ID univoco dell'applicazione o dell'assegnazione.

<pre><code class="lang-text">Download of policy CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00" completed (DTS Job ID: {AE88E639-0E59-40D7-AAA9-4403AAE6EE82})
Policy state for [CCM_Policy_Policy5.PolicyID="{<b>3AC57DFE-3F87-4C59-930B-B9F57CB41B91</b>}",PolicySource="SMS:PS1",PolicyVersion="1.00"] is currently [Active]
</code></pre>

Una volta scaricati i criteri nel client, il componente utilità di pianificazione crea pianificazioni per l'attivazione e l'imposizione della distribuzione.

## <a name="deployment-activation"></a>Attivazione della distribuzione

La valutazione dell'applicazione viene avviata quando viene attivata la distribuzione. Componente utilità di pianificazione consente di creare una pianificazione per attivare l'assegnazione nell'ora disponibile configurata nella distribuzione. Questa attività può essere rilevata in **Scheduler. log** nel client usando l'ID univoco di assegnazione dell'applicazione.

- Per le distribuzioni **richieste** , viene creata la pianificazione dell'attivazione, ma è previsto un ritardo di un massimo di due ore per evitare la contesa di risorse nei server del sito e nei punti di distribuzione. Il ritardo consente di evitare conflitti perché il contenuto dell'applicazione può essere scaricato durante la valutazione se l'applicazione è applicabile in base alle regole di requisiti definite.

    <pre><code class="lang-text">SMSTrigger '15AF8C4000080000' for scheduler '<b>Machine/{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 01:44:00 PM with randomization.
    </code></pre>

- Per le distribuzioni **disponibili** , la pianificazione dell'attivazione viene creata per essere attivata all'ora disponibile configurata nella distribuzione.

    <pre><code class="lang-text">SMSTrigger '1E4F8C4000080001' for scheduler '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' will fire at 08/15/2019 01:13:33 PM without randomization.
    </code></pre>

Al momento dell'arrivo della pianificazione, il componente utilità di pianificazione Invia il messaggio di attivazione all'agente DCM per eseguire la valutazione dell'applicazione.

<pre><code class="lang-text">Sending message for schedule '<b>Machine/{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</b>' (Target: 'direct:DCMAgent', Name: '')
</code></pre>

L'agente DCM riceve il messaggio di attivazione e crea un processo per la valutazione dell'applicazione.

```text
CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='Activation'><AssignmentID>{3AC57DFE-3F87-4C59-930B-B9F57CB41B91}</AssignmentID></CIAssignmentMessage>'
```

## <a name="deployment-enforcement"></a>Imposizione della distribuzione

L'installazione dell'applicazione viene avviata quando viene applicata la distribuzione.

- Per le distribuzioni **richieste** , l'utilità di pianificazione crea una pianificazione di scadenza dopo il download del criterio per applicare l'applicazione alla scadenza della distribuzione. La pianificazione della scadenza non è casuale per impostazione predefinita. Il comportamento di sequenza casuale per l'attivazione può essere controllato dall'impostazione [Disabilita scadenza client sequenza casuale](/sccm/core/clients/deploy/about-client-settings#disable-deadline-randomization) .

    <pre><code class="lang-text">SMSTrigger '15EF8C4000080000' for scheduler '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' will fire at 08/15/2019 03:05:00 PM without randomization.
    </code></pre>

    Alla scadenza, il componente utilità di pianificazione Invia il messaggio di scadenza all'agente DCM. 

    <pre><code class="lang-text">Sending message for schedule '<b>Machine/DEADLINE:{5F2FA409-C9B2-4100-8BC8-051820311DE1}</b>' (Target: 'direct:DCMAgent', Name: '')
    </code></pre>

    L'agente DCM riceve il messaggio di scadenza e crea un processo per applicare l'applicazione.
  
    ```text
    CDCMAgent::HandleMessage - Message received for machine: '<?xml version='1.0' ?><CIAssignmentMessage MessageType='EnforcementDeadline'><AssignmentID>{5F2FA409-C9B2-4100-8BC8-051820311DE1}</AssignmentID></CIAssignmentMessage>'
    ```

    > [!NOTE]
    > Per le distribuzioni con scadenza in passato, l'applicazione viene attivata e applicata immediatamente dallo stesso processo dell'agente DCM che esegue le azioni di valutazione, download e installazione.

- Per le distribuzioni **disponibili** , non esiste alcuna pianificazione delle scadenze perché l'applicazione viene eseguita quando l'installazione dell'applicazione viene avviata dall'utente da software Center. Quando l'utente avvia un'installazione, viene creato un processo dell'agente DCM per eseguire la valutazione, il download e l'installazione dell'applicazione. Questa attività può essere rilevata in **DCMAgent. log** nel client.

## <a name="next-steps"></a>Passaggi successivi

- [Informazioni sui componenti client di distribuzione delle applicazioni](/sccm/apps/understand/client-components-technical-reference)

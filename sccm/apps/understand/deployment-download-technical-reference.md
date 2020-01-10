---
title: Riferimento tecnico per il download di applicazioni
titleSuffix: Configuration Manager
description: Riferimento tecnico per la risoluzione dei problemi di download dell'applicazione per Configuration Manager.
ms.date: 11/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: troubleshooting
ms.assetid: 41c29a07-9bf6-4ec4-b3f2-1c05e001eff7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b7405112ee1114c1da8b0c5764045637012d7420
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75815579"
---
# <a name="application-download-in-configuration-manager"></a>Download dell'applicazione in Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Prima di continuare, esaminare i [componenti client di distribuzione delle applicazioni](/sccm/apps/understand/client-components-technical-reference) per comprendere l'elaborazione dei processi dell'agente ci e di DCM.

## <a name="download-initiation"></a>Avvio del download

Il download del contenuto dell'applicazione viene avviato dal componente agente CI nel client durante la fase **StateDownloadingContents** . Questo processo è lo stesso, indipendentemente dal fatto che l'applicazione venga distribuita a una raccolta di dispositivi o a una raccolta di utenti.

- Per le distribuzioni **disponibili** , il contenuto dell'applicazione viene scaricato quando l'utente avvia l'installazione dell'applicazione da software Center.
- Per le distribuzioni **richieste** , il contenuto dell'applicazione viene scaricato quando l'assegnazione viene attivata e l'applicazione viene trovata dopo la valutazione. Per informazioni sull'attivazione dell'assegnazione, vedere gli articoli [distribuzione di applicazioni in raccolte di dispositivi](/sccm/apps/understand/device-deployment-technical-reference) o [distribuzione di applicazioni in raccolte di utenti](/sccm/apps/understand/user-deployment-technical-reference) .

Quando l'agente CI avvia il download del contenuto, crea un'attività che viene gestita dal componente di gestione attività CI. CI avvia il download del contenuto. Questa attività può essere rilevata in **CITaskMgr. log** utilizzando l'ID univoco del tipo di distribuzione.

<pre><code class="lang-text"><b>Initiating task ContentDownload</b> for CI ScopeId_B63CEBE7-8A69-4FBE-994F-5AD0A8488D27/DeploymentType_1d49ef88-cf3b-42fa-b198-388d220ccb44.2 (ConfigMgr Toolkit - Windows Installer (*.msi file)) for target: , consumer: {53EA65C2-D596-4215-83E4-F7007B78E18C}
</code></pre>

## <a name="distribution-point-location"></a>Percorso del punto di distribuzione

Tutte le attività di download sono gestite dal componente di accesso al contenuto, che è responsabile della gestione della cache del client. Dopo aver creato l'attività di download, il componente di accesso ai contenuti controlla se il contenuto è già disponibile nella cache client. Se il contenuto non è disponibile, viene creata una richiesta di percorso per ottenere un elenco di punti di distribuzione da cui è possibile ottenere il contenuto. Questa attività può essere rilevata in **CAS. log** e **LocationServices. log** nel client usando l'ID univoco del contenuto.

```text
Requesting locations synchronously for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 with priority Foreground
ContentLocationRequest : <Request XML Body>
Reply Message Body : <Reply XML Body>
```

> [!IMPORTANT]
> Anche se il componente dei servizi di posizione gestisce le richieste di località, non richiede direttamente percorsi dal punto di gestione. Tutte le richieste al punto di gestione in genere passano tramite il componente di messaggistica CCM, che registra a **CcmMessaging. log**.

Il percorso XML di risposta contiene l'elenco dei punti di distribuzione in base al gruppo di limiti del client. Questo elenco viene analizzato e reso permanente in WMI nel client in base alla [priorità dell'origine del contenuto](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#content-source-priority). Questa attività può essere visualizzata in **ContentTransferManager. log**, usando l'ID univoco del contenuto e cercando `Persisted location`. 

Se il percorso XML di risposta non contiene alcun punto di distribuzione, **ContentTransferManager. log** visualizzerà `Received empty location update` e il client potrebbe rimanere bloccato allo 0% durante il download dell'applicazione. Questa risposta può in genere verificarsi a causa di problemi di configurazione del gruppo di limiti. Per altre informazioni, vedere [Errori di download](/sccm/apps/deploy-use/troubleshoot-application-deployment#download-failures).

## <a name="content-download"></a>Download del contenuto

Una volta ottenuti i percorsi dei punti di distribuzione, il componente accesso al contenuto crea un processo di trasferimento del contenuto. Questa attività può essere rilevata in **CAS. log** usando l'ID univoco del contenuto.

<pre><code class="lang-text">Submitted CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> to download Content <b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b> under context System
</code></pre>

Gestione trasferimento contenuto crea quindi un processo del servizio Trasferimento dati per eseguire il download del contenuto. Questa attività può essere rilevata in **ContentTransferManager. log** nel client usando l'ID univoco del contenuto.

<pre><code class="lang-text">CTM job <b>{6D0EA720-EB4E-4893-8395-8B27470A6CFB}</b> (corresponding DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>) started download from '<Distribution Point URL>/<b>Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1</b>' for full content download.
</code></pre>

> [!NOTE]
> Questa voce di log può essere usata per identificare l'ID di processo CTM e DTS, che può essere usato per tenere traccia dello stato di avanzamento del trasferimento del contenuto in **ContentTransferManager. log** e **DataTransferService. log** rispettivamente.

Trasferimento dati servizio esegue il download del contenuto dell'applicazione creando un processo di Servizio trasferimento intelligente in background (BITS) e attendendo il completamento del download. Questa attività può essere rilevata in **DataTransferService. log** nel client usando l'ID processo DTS ottenuto da **ContentTransferService. log**.

<pre><code class="lang-text">Starting BITS job '{40263E01-2EDD-462F-ABBA-A5E892CB9229}' for DTS job '<b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b>' under user 'S-1-5-18'.
DTSJob <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> in state 'DownloadingData'.
DTS job <b>{708C7F21-8898-49AB-900E-BA6E5F1A39BC}</b> has completed
</code></pre>

Al termine del download, viene inviata una notifica al componente accesso al contenuto. Il componente accesso al contenuto verifica quindi il contenuto scaricato per assicurarsi che il contenuto non sia stato modificato durante il download. Questa attività può essere rilevata in **CAS. log** usando l'ID univoco del contenuto.

```text
Hash verification succeeded for content Content_00a8f9e6-8e44-42f5-a0ef-9b5c86a88498.1 downloaded under context System
```

Infine, dopo aver verificato il contenuto, l'agente CI riceve la notifica di completamento dell'attività e il processo dell'agente CI passa alla fase successiva.

<pre><code class="lang-text">CIAgentJob({2BF84225-C9E8-49A6-A308-A160C4B799D3}): CAgentJob::HandleEvent(<b>Event=CITaskComplete, CurrentState=StateDownloadingContents</b>)
</code></pre>

## <a name="next-steps"></a>Passaggi successivi

- [Installazione delle applicazioni](/sccm/apps/understand/deployment-install-technical-reference)

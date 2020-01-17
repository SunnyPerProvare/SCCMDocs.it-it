---
title: Suggerimenti per la risoluzione dei problemi per le distribuzioni di app
titleSuffix: Configuration Manager
description: Suggerimenti per la risoluzione dei problemi di distribuzione dell'applicazione in Configuration Manager
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4e8b46a3-3e11-475f-a4d7-6bf9ddf14145
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 696fd350d8fc98d1f84564c5e360af45a46c077e
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75817874"
---
# <a name="troubleshooting-tips-for-application-deployments"></a>Suggerimenti per la risoluzione dei problemi per le distribuzioni di applicazioni

*Si applica a: Configuration Manager (Current Branch)*

I problemi tipici della distribuzione di applicazioni rientrano in una delle categorie seguenti:

- Errori di download dell'applicazione

- Conformità della distribuzione dell'applicazione bloccata allo 0%

Se si verifica uno di questi problemi, il presente articolo elenca alcuni passaggi da usare per la risoluzione. Per informazioni più dettagliate sulla risoluzione dei problemi, vedere [risoluzione dei problemi di riferimento tecnico](/sccm/apps/understand/app-deployment-technical-reference)per la distribuzione di applicazioni.


## <a name="download-failures"></a>Errori di download

Gli errori di download dell'applicazione includono i seguenti problemi:

- Il client si blocca durante il download di un'applicazione

- Il client non riesce a scaricare il contenuto dell'applicazione

- Il client si blocca a 0% durante il download di un'applicazione

La prima cosa da verificare in caso di errori di download dell'applicazione è la presenza di limiti e gruppi di limiti mancanti o non configurati correttamente. Se ad esempio il client si trova sull'Intranet e non è configurato per la gestione client solo Internet, la posizione di rete del client deve essere all'interno di un limite associato. Deve anche essere presente un gruppo di limiti assegnato a questo limite, per consentire al client di scaricare il contenuto. Per altre informazioni, vedere [Definire i limiti del sito e i gruppi di limiti](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups).

Se non è possibile configurare un limite per un client o se un gruppo di limiti specifico non può essere un membro di un altro gruppo di limiti:

1. Nella console di Configuration Manager aprire le proprietà del **Tipo di distribuzione**.  

1. Passare alla scheda **Contenuto**.

1. Nella sezione per l'uso di un punto di distribuzione da un gruppo di limiti vicino o del gruppo di limiti del sito predefinito, modificare **Opzioni di distribuzione** impostando **Scarica il contenuto dal punto di distribuzione ed esegui in locale**. L'impostazione predefinita è **Non scaricare contenuto**.

Se il client non riesce a scaricare il contenuto dell'applicazione, assicurarsi che sia distribuito in un punto di distribuzione. Per verificare questa configurazione, usare le funzionalità integrate nella console per monitorare la distribuzione del contenuto ai punti di distribuzione. Per altre informazioni, vedere [Monitorare il contenuto distribuito](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed).  


## <a name="compliance-stuck-at-0"></a>Conformità bloccata allo 0%

Quando la conformità della distribuzione dell'applicazione è 0%, verificare lo stato di distribuzione per l'applicazione nell'area di lavoro **Monitoraggio** sotto il nodo **Distribuzioni**.

- **In corso**: il client potrebbe essersi bloccato durante il [download del contenuto](#download-failures)

- **Errore**: Per altre informazioni su come risolvere questo problema, vedere il post di blog seguente: [Suggerimenti e consigli: Come intervenire su asset che segnalano una distribuzione non riuscita](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/Tips-and-Tricks-How-to-Take-Action-on-Assets-That-Report-a/ba-p/273019)

- **Sconosciuto**: questo stato in genere significa che il client non ha ricevuto i criteri. Aggiornare manualmente i criteri client per verificare se il client li riceve. Per altre informazioni, vedere [Avviare il recupero criteri per un client di Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).
  
Se queste azioni non risolvono il problema, controllare lo stato del client. Il client potrebbe avere un problema meno evidente. Per altre informazioni, vedere [Come monitorare i client](/sccm/core/clients/manage/monitor-clients).


## <a name="next-steps"></a>Passaggi successivi

- [Monitorare le applicazioni](/sccm/apps/deploy-use/monitor-applications-from-the-console)
- [Distribuire applicazioni](/sccm/apps/deploy-use/deploy-applications)
- [Attività di gestione per le applicazioni](/sccm/apps/deploy-use/management-tasks-applications)
- [Guida di riferimento tecnico per la risoluzione dei problemi di distribuzione delle applicazioni](/sccm/apps/understand/app-deployment-technical-reference)

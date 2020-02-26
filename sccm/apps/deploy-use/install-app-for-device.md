---
title: Installare le applicazioni per un dispositivo
titleSuffix: Configuration Manager
description: Usare Configuration Manager per installare immediatamente un'applicazione in un dispositivo senza una raccolta.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c2a71fca-8744-4d72-abf9-9d8c5d2afb00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: af9c0c2d1971bd244073d9c9dc8b46599687f846
ms.sourcegitcommit: 1991263194a5cd6dfbd3dd9a5f5c7f179c1bfeac
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/14/2020
ms.locfileid: "77218177"
---
# <a name="install-applications-for-a-device"></a>Installare le applicazioni per un dispositivo

<!--4402180-->

A partire dalla versione 1906, della console di Configuration Manager è possibile installare le applicazioni per un dispositivo in tempo reale. Questa funzionalità consente di ridurre la necessità di raccolte separate per ogni applicazione.

## <a name="prerequisites"></a>Prerequisiti

- Abilitare la [funzionalità facoltativa](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **Approva le richieste dell'applicazione per gli utenti per ogni dispositivo**.  

- [Distribuire l'applicazione](/sccm/apps/deploy-use/deploy-applications) come *Disponibile* in una raccolta di dispositivi.  

    - Nella pagina **Impostazioni di distribuzione** della distribuzione guidata selezionare l'opzione seguente: **Un amministratore deve approvare una richiesta per questa applicazione nel dispositivo**.  

        > [!Note]  
        > Con queste impostazioni di distribuzione, nessun criterio viene inviato al client. L'app non viene visualizzata come disponibile in Software Center e un utente non può installare l'app con questa distribuzione. Dopo aver usato questa azione per installare l'app, è possibile eseguirla e visualizzarne lo stato di installazione in Software Center.

- L'account utente richiede le autorizzazioni seguenti:

    - **Applicazione**: Lettura, Approvazione

    - **Raccolta**: Lettura, Lettura risorsa, Modifica risorsa, Visualizza file raccolti

    Il ruolo predefinito **Amministratore applicazione** ha ad esempio queste autorizzazioni.

> [!TIP]
> In una gerarchia, attendere che le informazioni sull'applicazione e sulla distribuzione vengano replicate nel sito primario a cui è assegnato il client di destinazione.<!-- SCCMDocs#2113 -->

## <a name="process"></a>Processo

1. Nella console di Configuration Manager passare all'area di lavoro **Asset e conformità** e selezionare il nodo **Dispositivi**. Selezionare il dispositivo di destinazione, quindi selezionare l'azione **Installa applicazione** sulla barra multifunzione.

1. Selezionare una o più applicazioni dall'elenco. L'elenco mostra solo le applicazioni che sono già state distribuite con le impostazioni dei prerequisiti.

Questa azione attiva l'installazione delle applicazioni pre-distribuite selezionate nel dispositivo.

Per visualizzare lo stato della richiesta di approvazione, nell'area di lavoro **Raccolta software** espandere **Gestione applicazioni** e selezionare il nodo **Richieste di applicazioni**.

Monitorare l'installazione dell'app come di consueto nel nodo **Distribuzioni** dell'area di lavoro **Monitoraggio**.


## <a name="see-also"></a>Vedere anche

[Approvare le applicazioni](/sccm/apps/deploy-use/app-approval)

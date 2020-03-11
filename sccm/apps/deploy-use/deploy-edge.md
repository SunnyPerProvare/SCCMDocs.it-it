---
title: Distribuire e aggiornare Microsoft Edge versione 77 e successive
titleSuffix: Configuration Manager
description: Come distribuire e aggiornare Microsoft Edge versione 77 e successive con Configuration Manager
ms.date: 03/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 73b420be-5d6a-483a-be66-c4d274437508
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 8fca1a1125b3856ecbfc0dd91439c93500e7c555
ms.sourcegitcommit: 0250a75670f231283b31fd87032cfffb6f34fe18
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/04/2020
ms.locfileid: "78287704"
---
# <a name="microsoft-edge-management"></a>Gestione di Microsoft Edge

*Si applica a: Configuration Manager (Current Branch)*

Il nuovo Microsoft Edge è disponibile per le aziende. A partire da Configuration Manager versione 1910, è ora possibile distribuire [Microsoft Edge versione 77 e successive](https://docs.microsoft.com/deployedge/) agli utenti. Per installare la compilazione Edge selezionata, viene usato uno script di PowerShell. Lo script disattiva anche gli aggiornamenti automatici per Edge in modo che possano essere gestiti con Configuration Manager.

## <a name="bkmk_Microsoft_Edge"></a>Distribuire Microsoft Edge
<!--4561024-->
Gli amministratori possono scegliere tra il canale Beta, Dev e stabile, insieme a una versione del client Microsoft Edge da distribuire. Ogni versione incorpora informazioni e miglioramenti da parte dei clienti e della community.

### <a name="prerequisites-for-deploying"></a>Prerequisiti per la distribuzione

Per i client in cui verrà distribuito Microsoft Edge:

- I [criteri di esecuzione](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_execution_policies) di PowerShell non possono essere impostati su Con restrizioni.
  - PowerShell viene eseguito per eseguire l'installazione.

Il dispositivo che esegue la console di Configuration Manager richiede l'accesso agli endpoint seguenti:

|Percorso|Uso|
|---|---|
|`https://edgeupdates.microsoft.com/api/products?view=enterprise`|Informazioni sulle versioni di Microsoft Edge|
|`http://dl.delivery.mp.microsoft.com`|Contenuto per le versioni di Microsoft Edge|

### <a name="verify-microsoft-edge-update-policies"></a>Verificare i criteri di aggiornamento di Microsoft Edge

Nella versione 1910, quando viene distribuito Microsoft Edge, lo script di installazione disattiva gli aggiornamenti automatici per Microsoft Edge in modo che possano essere gestiti con Configuration Manager. È possibile modificare questo comportamento ricorrendo a Criteri di gruppo. Per altre informazioni, vedere [Pianificare la distribuzione di Microsoft Edge](https://docs.microsoft.com/deployedge/deploy-edge-plan-deployment#define-and-configure-policies) e [Criteri di aggiornamento di Microsoft Edge](https://docs.microsoft.com/DeployEdge/microsoft-edge-update-policies).


### <a name="create-a-deployment"></a>Creare una distribuzione

Creare un'applicazione Microsoft Edge usando l'esperienza dell'applicazione predefinita, che semplifica la gestione di Microsoft Edge:

1. Nella console, in **Raccolta software**, è disponibile un nuovo nodo denominato **Gestione di Microsoft Edge**.
1. Selezionare **Crea un'applicazione di Microsoft Edge** dalla barra multifunzione o facendo clic con il pulsante destro del mouse sul nodo **Gestione di Microsoft Edge**.

   ![Azione di clic con il pulsante destro del mouse sul nodo Gestione di Microsoft Edge](./media/4561024-create-microsoft-edge-application.png)

1. Nella pagina **Impostazioni applicazione** della creazione guidata specificare un nome, una descrizione e un percorso per il contenuto dell'app. Verificare che la cartella del percorso del contenuto specificata sia vuota.
1. Nella pagina **Impostazioni di Microsoft Edge** selezionare un canale e una versione da distribuire. Il collegamento Altre informazioni consente di visualizzare la [pagina Microsoft Edge Insider](https://www.microsoftedgeinsider.com/).

   ![Pagina Impostazioni di Microsoft Edge della distribuzione guidata](./media/4561024-edge-settings-wizard.png)

1. Nella pagina **Distribuzione** decidere se si vuole distribuire l'applicazione. Se si seleziona **Sì**, è possibile specificare le impostazioni di distribuzione per l'applicazione. Per altre informazioni sulle impostazioni di distribuzione, vedere [Distribuire applicazioni](/configmgr/apps/deploy-use/deploy-applications#bkmk_deploy-general).
1. In **Software Center** nel dispositivo client l'utente può visualizzare e installare l'applicazione.

   ![Pagina Impostazioni di Microsoft Edge della distribuzione guidata](./media/4561024-software-center-install-edge.png)

### <a name="log-files-for-deployment"></a>File di log per la distribuzione

|Percorso|Registro|Uso|
|---|---|---|
| Server del sito|SMSProv.log|Mostra i dettagli se la creazione dell'app o della distribuzione ha esito negativo.|
| [Varia](/sccm/core/plan-design/hierarchy/log-files)|PatchDownloader.log| Mostra i dettagli se il download del contenuto ha esito negativo.|
| Client|  AppEnforce.log|Mostra le informazioni di installazione.|

## <a name="update-microsoft-edge"></a>Aggiornare Microsoft Edge
<!--4831871-->

A partire da Configuration Manager versione 1910, è presente un nodo denominato **Tutti gli aggiornamenti di Microsoft Edge** in **Gestione di Microsoft Edge**. Questo nodo consente di gestire gli aggiornamenti per tutti i canali di Microsoft Edge.<!--initial edge updates released Jan 15,2020-->

1. Per ottenere gli aggiornamenti per Microsoft Edge, assicurarsi che la classificazione **Aggiornamenti** e il prodotto **Microsoft Edge** siano [selezionati per la sincronizzazione](/configmgr/sum/get-started/configure-classifications-and-products).

   [![Selezionare Microsoft Edge come prodotto in Proprietà punto di aggiornamento software](./media/4831871-microsoft-edge-product-sup.png)](./media/4831871-microsoft-edge-product-sup.png#lightbox)

1. Nell'area di lavoro **Raccolta software** espandere **Gestione di Microsoft Edge** e fare clic sul nodo **Tutti gli aggiornamenti di Microsoft Edge**.

1. Se necessario, fare clic su **Sincronizza aggiornamenti software** sulla barra multifunzione per avviare una sincronizzazione. Per altre informazioni, vedere [Sincronizzare gli aggiornamenti software](/configmgr/sum/get-started/synchronize-software-updates).

   ![Nodo Tutti gli aggiornamenti di Microsoft Edge](./media/4831871-all-microsoft-edge-updates.png)

1. Gestire e distribuire gli aggiornamenti di Microsoft Edge come qualsiasi altro aggiornamento, ad esempio aggiungendoli alla [regola di distribuzione automatica](/configmgr/sum/deploy-use/automatically-deploy-software-updates). Di seguito sono riportate alcune delle attività di aggiornamento comuni che è possibile eseguire dal nodo **Tutti gli aggiornamenti di Microsoft Edge**:

   - [Creare una distribuzione in più fasi](/configmgr/osd/deploy-use/create-phased-deployment-for-task-sequence)
   - [Distribuire manualmente gli aggiornamenti software](/configmgr/sum/deploy-use/manually-deploy-software-updates)
   - [Scaricare gli aggiornamenti software](/configmgr/sum/deploy-use/download-software-updates)

## <a name="next-steps"></a>Passaggi successivi

[Monitorare le applicazioni](/configmgr/apps/deploy-use/monitor-applications-from-the-console)

[Monitorare gli aggiornamenti software](/configmgr/sum/deploy-use/monitor-software-updates)

[Gestire e monitorare le distribuzioni in più fasi](/configmgr/osd/deploy-use/manage-monitor-phased-deployments)

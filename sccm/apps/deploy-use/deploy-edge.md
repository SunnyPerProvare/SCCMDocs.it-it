---
title: Distribuire e aggiornare Microsoft Edge, versione 77 e successive
titleSuffix: Configuration Manager
description: Come distribuire e aggiornare Microsoft Edge, versione 77 e successive con Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 73b420be-5d6a-483a-be66-c4d274437508
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 65488348507a434f324d1e239b790d5c06323c38
ms.sourcegitcommit: 1bccb61bf3c7c69d51e0e224d0619c8f608e8777
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/05/2019
ms.locfileid: "74662259"
---
# <a name="microsoft-edge-management"></a>Gestione di Microsoft Edge

*Si applica a: Configuration Manager (Current Branch)*

Il nuovo Microsoft Edge è disponibile per le aziende. A partire da Configuration Manager versione 1910, è ora possibile distribuire [Microsoft Edge, versione 77 e successive](https://docs.microsoft.com/deployedge/) agli utenti.

## <a name="bkmk_Microsoft_Edge"></a> Distribuire Microsoft Edge versione 77 e successive
<!--4561024-->
Gli amministratori possono scegliere il canale Beta o Dev, insieme a una versione del client Microsoft Edge da distribuire. Ogni versione incorpora informazioni e miglioramenti da parte dei clienti e della community.

### <a name="prerequisites-for-deploying"></a>Prerequisiti per la distribuzione

Per i client destinati a una distribuzione di Microsoft Edge versione 77 e successive:

- I [criteri di esecuzione](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_execution_policies) di PowerShell non possono essere impostati su Con restrizioni.
  - PowerShell viene eseguito per eseguire l'installazione.
  
Il dispositivo che esegue la console di Configuration Manager richiede l'accesso agli endpoint seguenti:

|Percorso|Utilizzare|
|---|---|
|`https://edgeupdates.azurewebsites.net/api/products?view=enterprise`|Informazioni sulle versioni di Microsoft Edge versione 77 e successive|
|`http://dl.delivery.mp.microsoft.com`|Contenuto per le versioni di Microsoft Edge versione 77 e successive|




### <a name="create-a-deployment"></a>Creare una distribuzione

Creare un'applicazione Microsoft Edge versione 77 e successive usando l'esperienza dell'applicazione predefinita, che semplifica la gestione di Microsoft Edge:

1. Nella console, in **Raccolta software**, è disponibile un nuovo nodo denominato **Gestione di Microsoft Edge**.
1. Selezionare **Crea un'applicazione di Microsoft Edge** dalla barra multifunzione o facendo clic con il pulsante destro del mouse sul nodo **Gestione di Microsoft Edge**.

   ![Azione di clic con il pulsante destro del mouse sul nodo Gestione di Microsoft Edge](./media/4561024-create-microsoft-edge-application.png)

1. Nella pagina **Impostazioni applicazione** della creazione guidata specificare un nome, una descrizione e un percorso per il contenuto dell'app.
1. Nella pagina **Impostazioni di Microsoft Edge** selezionare un canale e una versione da distribuire. Il collegamento Altre informazioni consente di visualizzare la [pagina Microsoft Edge Insider](https://www.microsoftedgeinsider.com/).

   ![Pagina Impostazioni di Microsoft Edge della distribuzione guidata](./media/4561024-edge-settings-wizard.png)

1. Nella pagina **Distribuzione** decidere se si vuole distribuire l'applicazione. Se si seleziona **Sì**, è possibile specificare le impostazioni di distribuzione per l'applicazione. Per ulteriori informazioni sulle impostazioni di distribuzione, vedere [deploy Applications](/configmgr/apps/deploy-use/deploy-applications#bkmk_deploy-general).
1. In **Software Center** nel dispositivo client l'utente può visualizzare e installare l'applicazione.

   ![Pagina Impostazioni di Microsoft Edge della distribuzione guidata](./media/4561024-software-center-install-edge.png)

### <a name="log-files-for-deployment"></a>File di log per la distribuzione

|Percorso|Registro|Utilizzare|
|---|---|---|
| Server del sito|SMSProv.log|Mostra i dettagli se la creazione dell'app o della distribuzione ha esito negativo.|
| [Varia](/sccm/core/plan-design/hierarchy/log-files)|PatchDownloader.log| Mostra i dettagli se il download del contenuto ha esito negativo.|
| Client|  AppEnforce.log|Mostra le informazioni di installazione.|

## <a name="update-microsoft-edge-version-77-and-later"></a>Aggiornare Microsoft Edge versione 77 e successive
<!--4831871-->

A partire da Configuration Manager versione 1910, è possibile notare che è presente un nodo denominato **tutti gli aggiornamenti Microsoft Edge** in **gestione Microsoft Edge**. Sebbene non sia ancora possibile visualizzare gli aggiornamenti in questo nodo, è necessario sapere che Configuration Manager è pronto.

   ![Nodo Tutti gli aggiornamenti di Microsoft Edge](./media/4831871-all-microsoft-edge-updates.png)

## <a name="next-steps"></a>Passaggi successivi

[Monitorare le applicazioni](/configmgr/apps/deploy-use/monitor-applications-from-the-console)
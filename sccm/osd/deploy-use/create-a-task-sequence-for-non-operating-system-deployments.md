---
title: "Creare una sequenza di attività per distribuzioni non di sistema operativo"
titleSuffix: Configuration Manager
description: "Creare sequenze di attività non correlate alla distribuzione di sistemi operativi ad esempio distribuzione del software, aggiornamento di driver, modifica degli stati utente e così via."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
caps.latest.revision: "6"
author: aczechowski
ms.author: aaroncz
manager: angrobe
ms.openlocfilehash: e4a6e8e708a4c54be7dd84b0b3193cc00871ee88
ms.sourcegitcommit: 08f9854fb6c6d21e1e923b13e38a64d0bc2bc9a4
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-task-sequence-for-non-operating-system-deployments-with-system-center-configuration-manager"></a>Creare una sequenza di attività per le distribuzioni del sistema non operativo con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le sequenze di attività in System Center Configuration Manager consentono di automatizzare una serie di attività all'interno dell'ambiente. Queste attività sono progettate e testate principalmente per la distribuzione di sistemi operativi.  Configuration Manager ha molte altre funzionalità che è consigliabile usare come tecnologia principale per scenari quali [installazione dell'applicazione](../../apps/understand/introduction-to-application-management.md), [installazione degli aggiornamenti software](../../sum/understand/software-updates-introduction.md), [configurazione delle impostazioni](../../compliance/understand/ensure-device-compliance.md) o automazione personalizzata. È consigliabile anche considerare altre tecnologie di automazione di Microsoft System Center, come ad esempio [Orchestrator](https://technet.microsoft.com/library/hh237242.aspx) e [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx) .  

La potenza delle sequenze di attività risiede nella loro flessibilità e nel modo in cui è possibile usarle per configurare le impostazioni client, distribuire software, aggiornare i driver, modificare stati utente ed eseguire altre attività indipendenti dalla distribuzione del sistema operativo. È possibile creare una sequenza di attività personalizzata per aggiungere qualsiasi numero di attività. L'uso di sequenze di attività personalizzate per la distribuzione non del sistema operativo è supportato in Configuration Manager. Tuttavia, se una sequenza di attività genera risultati indesiderati o incoerenti, considerare i possibili modi per semplificare l'operazione. È possibile farlo usando la procedura più semplice, dividendo le azioni tra più sequenze di attività, oppure con un approccio graduale alla creazione e al test della sequenza di attività.

 La procedura seguente è supportata in una sequenza di attività personalizzata di distribuzione non del sistema operativo:  

-   [Verifica conformità](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

-   [Connessione a una cartella di rete](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

-   [Scaricare il contenuto del pacchetto](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

-   [Installa applicazione](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

-   [Installa pacchetto](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

-   [Installa aggiornamenti software](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

-   [Riavvia computer](../understand/task-sequence-steps.md#BKMK_RestartComputer)   

-   [Esegui riga di comando](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

-   [Esegui script PowerShell](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

-   [Imposta variabili dinamiche](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

-   [Imposta variabile della sequenza di attività](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>Passaggi successivi 
[Distribuire la sequenza di attività](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS)

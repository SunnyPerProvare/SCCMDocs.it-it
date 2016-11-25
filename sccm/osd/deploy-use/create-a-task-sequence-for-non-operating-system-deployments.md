---
title: "Creare una sequenza di attività per le distribuzioni del sistema non operativo | Configuration Manager"
description: "Creare sequenze di attività non correlate alla distribuzione di sistemi operativi ad esempio distribuzione del software, aggiornamento di driver, modifica degli stati utente e così via."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
caps.latest.revision: 6
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: bc8ef5912f753031191a677d58d5e88f62b8d36a


---
# <a name="create-a-task-sequence-for-non-operating-system-deployments-with-system-center-configuration-manager"></a>Creare una sequenza di attività per le distribuzioni del sistema non operativo con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Le sequenze di attività in System Center Configuration Manager consentono di automatizzare una serie di attività all'interno dell'ambiente. Queste attività sono progettate e testate principalmente per la distribuzione di sistemi operativi.  Configuration Manager ha molte altre funzionalità che è consigliabile usare come tecnologia principale per scenari quali [installazione dell'applicazione](../../apps/understand/introduction-to-application-management.md), [installazione degli aggiornamenti software](../../sum/understand/software-updates-introduction.md), [configurazione delle impostazioni](../../compliance/understand/ensure-device-compliance.md) o automazione personalizzata. È consigliabile anche considerare altre tecnologie di automazione di Microsoft System Center, come ad esempio [Orchestrator](https://technet.microsoft.com/library/hh237242.aspx) e [Service Management Automation](https://technet.microsoft.com/library/dn469260.aspx) .  

 La potenza delle sequenze di attività risiede nella loro flessibilità e nel modo in cui è possibile usarle per configurare le impostazioni client, distribuire software, aggiornare i driver, modificare stati utente ed eseguire altre attività indipendenti dalla distribuzione del sistema operativo. È possibile creare una sequenza di attività personalizzata per aggiungere qualsiasi numero di attività. Mentre l'uso di base di sequenze di attività personalizzate per la distribuzione del sistema non operativo è supportata, non è possibile testare tutte le configurazioni possibili e la probabilità che si verifichino problemi aumenta man mano che si sviluppano sequenze di attività più complesse.  

 La procedura seguente può essere usata in una sequenza di attività personalizzata di distribuzione del sistema non operativo:  

-   [Verifica conformità](../understand/task-sequence-steps.md#BKMK_CheckReadiness)  

-   [Connessione a una cartella di rete](../understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder)  

-   [Scaricare il contenuto del pacchetto](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)  

-   [Installa applicazione](../understand/task-sequence-steps.md#BKMK_InstallApplication)  

-   [Installa pacchetto](../understand/task-sequence-steps.md#BKMK_InstallPackage)  

-   [Installa aggiornamenti software](../understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates)  

-   [Riavvia computer](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer)  

-   [Esegui riga di comando](../understand/task-sequence-steps.md#BKMK_RunCommandLine)  

-   [Esegui script PowerShell](../understand/task-sequence-steps.md#BKMK_RunPowerShellScript)  

-   [Imposta variabili dinamiche](../understand/task-sequence-steps.md#BKMK_SetDynamicVariables)  

-   [Imposta variabile della sequenza di attività](../understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable)  

## <a name="next-steps"></a>Passaggi successivi
[Distribuire la sequenza di attività](manage-task-sequences-to-automate-tasks.md#a-namebkmkdeploytsa-deploy-a-task-sequence)



<!--HONumber=Nov16_HO1-->



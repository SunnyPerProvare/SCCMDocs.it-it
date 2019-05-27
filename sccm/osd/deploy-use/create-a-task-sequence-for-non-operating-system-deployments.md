---
title: Creare una sequenza di attività per distribuzioni non di sistema operativo
titleSuffix: Configuration Manager
description: Creare sequenze di attività non destinate alla distribuzione di un sistema operativo, ad esempio per la distribuzione di software o l'automazione delle attività
ms.date: 05/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 92aaec8a-8751-442a-b64b-62ab05b5bf50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 17ba0f146a80928b1eaae6334e6418a5e08b1114
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65083070"
---
# <a name="create-a-task-sequence-for-non-os-deployments"></a>Creare una sequenza di attività per distribuzioni non di sistema operativo

*Si applica a: System Center Configuration Manager (Current Branch)*

Le sequenze di attività in Configuration Manager consentono di automatizzare diversi tipi di attività all'interno dell'ambiente. Queste attività sono progettate e testate principalmente per la distribuzione di sistemi operativi. Configuration Manager ha molte altre funzionalità che deve essere la tecnologia principale in uso per gli scenari seguenti:

- [Installazione di applicazioni](/sccm/apps/understand/introduction-to-application-management)
- [Installazione di aggiornamenti software](/sccm/sum/understand/software-updates-introduction)
- [Impostazione della configurazione](/sccm/compliance/understand/ensure-device-compliance)

Considerare anche altre tecnologie di automazione di Microsoft System Center, ad esempio [Orchestrator](https://docs.microsoft.com/system-center/orchestrator/) e [Service Management Automation](https://docs.microsoft.com/system-center/sma/).  

L'efficacia delle sequenze di attività risiede nella loro flessibilità e nel modo in cui si usano. Sono in grado di configurare le impostazioni client, distribuire il software, aggiornare i driver, modificare gli stati utente ed effettuare altre attività in modo indipendente dalla distribuzione del sistema operativo. È possibile creare una sequenza di attività personalizzata per aggiungere qualsiasi numero di attività. L'uso di sequenze di attività personalizzate per la distribuzione non del sistema operativo è supportato in Configuration Manager. Tuttavia, se una sequenza di attività genera risultati indesiderati o incoerenti, considerare i possibili modi per semplificare l'operazione:

- Usare passaggi più semplici
- Dividere le azioni tra più sequenze di attività
- Adottare un approccio graduale alla creazione e ai test della sequenza di attività

I passaggi seguenti sono supportati in una sequenza di attività personalizzata di distribuzione non del sistema operativo:  

- [Verifica conformità](/sccm/osd/understand/task-sequence-steps#BKMK_CheckReadiness)  

- [Connessione a una cartella di rete](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder)  

- [Scaricare il contenuto del pacchetto](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent)  

- [Installa applicazione](/sccm/osd/understand/task-sequence-steps#BKMK_InstallApplication)  

- [Installa pacchetto](/sccm/osd/understand/task-sequence-steps#BKMK_InstallPackage)  

- [Installa aggiornamenti software](/sccm/osd/understand/task-sequence-steps#BKMK_InstallSoftwareUpdates)  

- [Riavvia computer](/sccm/osd/understand/task-sequence-steps#BKMK_RestartComputer)  

- [Esegui riga di comando](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)  

- [Esegui script PowerShell](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript)  

- [Eseguire la sequenza di attività](/sccm/osd/understand/task-sequence-steps#child-task-sequence)  

- [Imposta variabili dinamiche](/sccm/osd/understand/task-sequence-steps#BKMK_SetDynamicVariables)  

- [Imposta variabile della sequenza di attività](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable)  

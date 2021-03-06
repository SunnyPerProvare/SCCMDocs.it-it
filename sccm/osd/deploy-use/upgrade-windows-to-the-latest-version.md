---
title: Eseguire l'aggiornamento a Windows 10
titleSuffix: Configuration Manager
description: Informazioni sull'uso di Configuration Manager per eseguire l'aggiornamento del sistema operativo da Windows 7 o versione successiva a Windows 10.
ms.date: 08/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: efcf478037ec224669d1a10da3a15366d3dba566
ms.sourcegitcommit: 148745e1c3d9817d8beea20684a54436210959c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2020
ms.locfileid: "75806172"
---
# <a name="upgrade-windows-to-the-latest-version-with-configuration-manager"></a>Aggiornare Windows all'ultima versione con Configuration Manager

*Si applica a: Configuration Manager (Current Branch)*

Questo articolo illustra la procedura da eseguire in Configuration Manager per aggiornare il sistema operativo di un computer. Sono disponibili diversi metodi di distribuzione, ad esempio supporti autonomi o Software Center. Lo scenario di aggiornamento sul posto ha le funzionalità seguenti:  

- Aggiorna il sistema operativo a Windows 10 o Windows Server 2016 e versioni successive

- Mantiene applicazioni, impostazioni e dati dell'utente nel computer

- Non presenta dipendenze esterne, ad esempio Windows ADK

- È più veloce e più flessibile rispetto alle distribuzioni tradizionali del sistema operativo

> [!Note]  
> La sequenza di attività di aggiornamento sul posto di Windows 10 supporta la distribuzione nei client basati su Internet gestiti tramite [Cloud Management Gateway](/sccm/core/clients/manage/plan-cloud-management-gateway). Ciò consente agli utenti remoti di eseguire più facilmente l'aggiornamento a Windows 10 senza doversi connettere a Internet. Per altre informazioni, vedere [Distribuire l'aggiornamento sul posto di Windows 10 mediante Cloud Management Gateway](/sccm/osd/deploy-use/deploy-a-task-sequence#deploy-windows-10-in-place-upgrade-via-cmg). <!-- 1357149 -->


## <a name="supported-versions"></a>Versioni supportate

### <a name="upgrade-version"></a>Aggiorna versione

Creare solo pacchetti di aggiornamento del sistema operativo per eseguire l'aggiornamento alle versioni del sistema operativo seguenti:

- Windows 10
- Windows Server 2016
- Windows Server 2019

### <a name="original-version"></a>Versione originale

Per la sequenza di attività di aggiornamento del sistema operativo, i dispositivi devono eseguire una delle seguenti versioni del sistema operativo:

#### <a name="windows-client"></a>Client Windows

- Windows 7
- Windows 8.1
- Una versione precedente di Windows 10. È ad esempio possibile eseguire l'aggiornamento di Windows 10 versione 1809 a Windows 10 versione 1903.  

Per ulteriori informazioni, vedere [percorsi di aggiornamento di Windows 10](https://docs.microsoft.com/windows/deployment/upgrade/windows-10-upgrade-paths).

#### <a name="windows-server"></a>Windows Server

- Windows Server 2012
- R2 per Windows Server 2012
- Una versione precedente di Windows Server 2016
- Una versione precedente di Windows Server 2019

Per ulteriori informazioni sui percorsi di aggiornamento supportati da Windows Server, vedere [percorsi di aggiornamento supportati](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths#upgrading-previous-retail-versions-of-windows-server-to-windows-server-2016) da windows server 2016 e [Centro aggiornamenti Windows Server](https://aka.ms/upgradecenter).


## <a name="BKMK_Plan"></a> Pianificazione  

### <a name="task-sequence-requirements-and-limitations"></a>Limitazioni e requisiti della sequenza di attività

Esaminare i requisiti e le limitazioni seguenti per la sequenza di attività da eseguire per aggiornare un sistema operativo e assicurarsi che soddisfi le esigenze:  

- Aggiungere solo i passaggi della sequenza di attività correlati all'attività di base di aggiornamento del sistema operativo. Tali passaggi includono principalmente l'installazione di pacchetti, applicazioni o aggiornamenti. Usare poi i passaggi che eseguono righe di comando o comandi PowerShell o che impostano variabili dinamiche.  

- Esaminare i driver e le applicazioni installate nei computer. Prima di distribuire la sequenza di attività di aggiornamento, assicurarsi che i driver siano compatibili con Windows 10.  

Le attività seguenti non sono compatibili con l'aggiornamento sul posto e richiedono l'uso di una distribuzione di tipo tradizionale del sistema operativo:  

- Modifica dell'appartenenza al dominio del computer o aggiornamento del gruppo Administrators locale.  

- Implementazione una modifica fondamentale nel computer, ad esempio:

  - Modifica delle partizioni del disco
  - Modifica dell'architettura del sistema da x86 a x64
  - Implementazione di UEFI. Per altre informazioni su un'opzione possibile, vedere [Conversione da BIOS a UEFI durante un aggiornamento sul posto](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).
  - Modifica della lingua di base del sistema operativo  

- Presenza di requisiti personalizzati, ad esempio l'uso di un'immagine di base personalizzata o di un tipo di crittografia del disco di terze parti oppure l'esecuzione di operazioni WinPE offline.  

### <a name="infrastructure-requirements"></a>Requisiti dell'infrastruttura  

L'unico prerequisito per lo scenario di aggiornamento è la disponibilità di un punto di distribuzione. Distribuire il pacchetto di aggiornamento del sistema operativo ed eventuali altri pacchetti inclusi nella sequenza di attività. Per altre informazioni, vedere [Install or modify a distribution point](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points) (Installare o modificare un punto di distribuzione).


## <a name="BKMK_Configure"></a> Configura  

### <a name="prepare-the-os-upgrade-package"></a>Preparare il pacchetto di aggiornamento del sistema operativo  

Il pacchetto di aggiornamento di Windows 10 contiene i file di origine necessari per aggiornare il sistema operativo nel computer di destinazione. Il pacchetto di aggiornamento deve avere la stessa edizione, architettura e lingua dei client da aggiornare. Per altre informazioni, vedere [Gestire i pacchetti di aggiornamento del sistema operativo](/sccm/osd/get-started/manage-operating-system-upgrade-packages).  

### <a name="create-a-task-sequence-to-upgrade-the-os"></a>Creare una sequenza di attività per aggiornare il sistema operativo  

Seguire la procedura descritta in [Creare una sequenza di attività per aggiornare un sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system) per automatizzare l'aggiornamento del sistema operativo.  

> [!NOTE]  
> Per creare una sequenza di attività per eseguire l'aggiornamento di un sistema operativo a Windows 10, si usa in genere la procedura descritta in [Creare una sequenza di attività per aggiornare un sistema operativo](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system). La sequenza di attività include il passaggio **Aggiorna sistema operativo**, oltre ad altri passaggi consigliati e gruppi con i quali gestire il processo di aggiornamento end-to-end.
>
> È possibile creare una sequenza di attività personalizzata e aggiungere il passaggio [Aggiorna sistema operativo](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS) . Questo è l'unico passaggio obbligatorio per aggiornare il sistema operativo a Windows 10. Se si sceglie questo metodo, per completare l'aggiornamento aggiungere anche il passaggio [Riavvia computer](/sccm/osd/understand/task-sequence-steps#BKMK_RestartComputer) dopo il passaggio **Aggiorna sistema operativo**. Assicurarsi di usare l'impostazione **Il sistema operativo predefinito attualmente installato** per riavviare il computer con il sistema operativo installato anziché con Windows PE.  


## <a name="BKMK_Deploy"></a> Distribuisci  

Per distribuire il sistema operativo, usare uno dei metodi di distribuzione seguenti:  

- [Use Software Center to deploy Windows over the network](/sccm/osd/deploy-use/use-software-center-to-deploy-windows-over-the-network) (Usare Software Center per distribuire Windows tramite la rete)  

- [Use stand-alone media to deploy Windows without using the network](/sccm/osd/deploy-use/use-stand-alone-media-to-deploy-windows-without-using-the-network) (Usare i supporti autonomi per distribuire Windows senza usare la rete)  

  > [!IMPORTANT]  
  > Quando si usano supporti autonomi, è necessario includere un'immagine di avvio nella sequenza di attività. Questa configurazione rende la sequenza di attività disponibile nella creazione guidata del supporto per la sequenza di attività.


## <a name="monitor"></a>Monitoraggio  

Per monitorare la distribuzione della sequenza di attività per l'aggiornamento del sistema operativo, vedere [Monitorare le distribuzioni del sistema operativo](/sccm/osd/deploy-use/monitor-operating-system-deployments).  

---
title: Aggiornare Windows all&quot;ultima versione | Configuration Manager
description: Informazioni sull'uso di supporti autonomi o di Software Center in Configuration Manager per eseguire l'aggiornamento di un sistema operativo Windows 7 o versione successiva a Windows 10.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c21eec87-ad1c-4465-8e45-5feb60b92707
caps.latest.revision: 13
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b44258255345c2e5488846736ddc1df48a147616


---
# <a name="upgrade-windows-to-the-latest-version-with-system-center-configuration-manager"></a>Aggiornare Windows alla versione più recente con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

In questo argomento sono descritti i passaggi da eseguire in System Center Configuration Manager per aggiornare un sistema operativo in un computer da Windows 7 o versione successiva a Windows 10. Sono disponibili diversi metodi di distribuzione, ad esempio supporti autonomi o Software Center. Scenario di aggiornamento sul posto a Windows 10  

-   Aggiorna il sistema operativo nei computer che attualmente eseguono Windows 7, Windows 8 o Windows 8.1. È anche possibile eseguire aggiornamenti di Windows 10 da build a build. Ad esempio, è possibile aggiornare Windows 10 RTM a Windows 10 versione 1511.  

-   Mantiene applicazioni, impostazioni e dati dell'utente nel computer  

-   Non presenta dipendenze esterne, ad esempio Windows ADK.  

-   È in genere più veloce e più flessibile rispetto alle distribuzioni tradizionali del sistema operativo.  

 Usare le sezioni seguenti per distribuire sistemi operativi in rete tramite una sequenza di attività.  

##  <a name="a-namebkmkplana-plan"></a><a name="BKMK_Plan"></a> Pianificazione  

-   **Esaminare le limitazioni relative alla sequenza di attività per aggiornare un sistema operativo**  

     Esaminare i requisiti e le limitazioni seguenti per la sequenza di attività da eseguire per aggiornare un sistema operativo per assicurarsi che soddisfi le esigenze:  

    -   È consigliabile aggiungere solo i passaggi della sequenza di attività correlati all'attività di base per la distribuzione dei sistemi operativi e alla configurazione dei computer dopo l'installazione dell'immagine. Sono inclusi i passaggi per l'installazione di pacchetti, applicazioni o aggiornamenti e quelli che eseguono righe di comando, PowerShell o che impostano variabili dinamiche.  

    -   Esaminare i driver e le applicazioni installate nei computer per assicurarsi che siano compatibili con Windows 10 prima di distribuire la sequenza di attività di aggiornamento.  

    -   Le attività seguenti non sono compatibili con l'aggiornamento sul posto e richiedono l'uso di distribuzioni tradizionali dei sistemi operativi:  

        -   Modifica dell'appartenenza al dominio di computer o aggiornamento del gruppo di amministratori locale.  

        -   Implementazione di una modifica fondamentale del computer, incluso il partizionamento del disco, una modifica dell'architettura da x86 a x64, l'implementazione di UEFI o la modifica della lingua del sistema operativo di base.  

        -   I requisiti sono personalizzati e includono l’uso di un’immagine di base personalizzata, l’uso della crittografia del disco di <sup>terze</sup> parti oppure operazioni WinPE offline.  

-   **Pianificare e implementare i requisiti di infrastruttura**  

     Gli unici prerequisiti per lo scenario di aggiornamento sono la presenza di un punto di distribuzione disponibile per il pacchetto di aggiornamento del sistema operativo ed eventuali altri pacchetti inclusi nella sequenza di attività. Per altre informazioni, vedere [Install or modify a distribution point](../../core/servers/deploy/configure/install-and-configure-distribution-points.md) (Installare o modificare un punto di distribuzione).

##  <a name="a-namebkmkconfigurea-configure"></a><a name="BKMK_Configure"></a> Configura  

1.  **Preparare il pacchetto di aggiornamento del sistema operativo**  

     Il pacchetto di aggiornamento di Windows 10 contiene i file di origine necessari per aggiornare il sistema operativo nel computer di destinazione. Il pacchetto di aggiornamento deve essere della stessa edizione, architettura e lingua dei client che da aggiornare.  Per altre informazioni, vedere [Manage operating system upgrade packages](../get-started/manage-operating-system-upgrade-packages.md) (Gestire i pacchetti di aggiornamento del sistema operativo).  

2.  **Creare una sequenza di attività per aggiornare il sistema operativo**  

     Seguire la procedura descritta in [Creare una sequenza di attività per aggiornare il sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md) per automatizzare l'aggiornamento del sistema operativo.  

    > [!NOTE]  
    >  In genere si usa la procedura descritta in [Creare una sequenza di attività per aggiornare il sistema operativo](create-a-task-sequence-to-upgrade-an-operating-system.md) per eseguire l'aggiornamento di un sistema operativo a Windows 10. La sequenza di attività include il passaggio Aggiorna sistema operativo, oltre ad altri passaggi e gruppi con i quali gestire il processo di aggiornamento end-to-end. È tuttavia possibile creare una sequenza di attività personalizzata e aggiungere il passaggio della sequenza di attività [Aggiorna sistema operativo](../understand/task-sequence-steps.md#BKMK_UpgradeOS) per aggiornare il sistema operativo. Questo è l'unico passaggio obbligatorio per aggiornare il sistema operativo a Windows 10. Se si sceglie questo metodo, aggiungere anche il passaggio [Riavvia computer](../understand/task-sequence-steps.md#a-namebkmkrestartcomputera-restart-computer) dopo il passaggio Aggiorna sistema operativo per completare l'aggiornamento. Assicurarsi di usare l'impostazione **Il sistema operativo predefinito attualmente installato** per riavviare il computer nel sistema operativo installato anziché in Windows PE.  

##  <a name="a-namebkmkdeploya-deploy"></a><a name="BKMK_Deploy"></a> Distribuisci  

-   Usare uno dei metodi di distribuzione seguenti per distribuire il sistema operativo:  

    -   [Use Software Center to deploy Windows over the network](use-software-center-to-deploy-windows-over-the-network.md) (Usare Software Center per distribuire Windows tramite la rete)  

    -   [Use stand-alone media to deploy Windows without using the network](use-stand-alone-media-to-deploy-windows-without-using-the-network.md) (Usare i supporti autonomi per distribuire Windows senza usare la rete)  

## <a name="monitor"></a>Monitoraggio  

-   **Monitorare la distribuzione della sequenza di attività**  

     Per monitorare la distribuzione della sequenza di attività per l'aggiornamento del sistema operativo, vedere [Monitor operating system deployments](monitor-operating-system-deployments.md) (Monitorare le distribuzioni del sistema operativo).  



<!--HONumber=Nov16_HO1-->


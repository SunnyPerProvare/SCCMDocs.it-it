---
title: Gerarchie di origine della migrazione | Microsoft Docs
description: Configurare una gerarchia di origine e i siti di origine per eseguire la migrazione dei dati all&quot;ambiente di System Center Configuration Manager.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ccce7cb5-e18f-4337-8adf-2018edca3c00
caps.latest.revision: 5
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 5e3d3f4194b06442e34c10988a20fe9ca40ac5d7
ms.openlocfilehash: 1ecac05cb7aba822047bbc519d8a0ca316c600a5


---
# <a name="configuring-source-hierarchies-and-source-sites-for-migration-to-system-center-configuration-manager"></a>Configurazione di gerarchie di origine e siti di origine per la migrazione in System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Per abilitare la migrazione dei dati nell'ambiente di System Center Configuration Manager, è necessario configurare una gerarchia di origine di Configuration Manager supportata e uno o più siti di origine nella stessa gerarchia che contengono i dati da migrare.  

> [!NOTE]  
>  Le operazioni di migrazione vengono eseguite nel sito di livello superiore della gerarchia di destinazione. Se la migrazione viene configurata durante l'uso di una console di Configuration Manager connessa a un sito figlio primario, è necessario attendere che la configurazione venga replicata nel sito di amministrazione centrale, che venga avviata e che lo stato venga replicato di nuovo nel sito primario a cui l'utente è connesso.  

 Utilizzare le informazioni e le procedure riportate nelle seguenti sezioni per specificare la gerarchia di origine e aggiungere siti di origine aggiuntivi. Dopo aver completato queste procedure, è possibile creare i processi di migrazione e iniziare a migrare i dati dalla gerarchia di origine alla gerarchia di destinazione.  

-   [Specificare una gerarchia di origine per la migrazione](#BKBM_ConfigSrcHierarchy)  

-   [Individuare siti di origine aggiuntivi della gerarchia di origine](#BKBM_ConfigSrcSites)  

##  <a name="a-namebkbmconfigsrchierarchya-specify-a-source-hierarchy-for-migration"></a><a name="BKBM_ConfigSrcHierarchy"></a> Specificare una gerarchia di origine per la migrazione  
 Per migrare i dati nella gerarchia di destinazione, è necessario specificare una gerarchia di origine supportata contenente i dati da migrare. Per impostazione predefinita, il sito di livello superiore di tale gerarchia diventa un sito di origine della gerarchia di origine. Se si esegue la migrazione da una gerarchia di Configuration Manager 2007, dopo avere raccolto i dati dal sito di origine iniziale è possibile configurare siti di origine aggiuntivi per la migrazione. Se si esegue la migrazione da una gerarchia di System Center 2012 Configuration Manager o di System Center Configuration Manager, non è necessario configurare i siti di origine aggiuntivi per la migrazione dei dati dalla gerarchia di origine. Questo è possibile perché le versioni di Configuration Manager usano un database condiviso disponibile nel sito principale della gerarchia di origine. Il database condiviso contiene tutte le informazioni che è possibile migrare.  

 Usare le procedure seguenti per specificare una gerarchia di origine per la migrazione e per individuare siti di origine aggiuntivi in una gerarchia di Configuration Manager 2007.  

 Eseguire questa procedura con una console di Configuration Manager connessa alla gerarchia di destinazione.  

#### <a name="to-configure-a-source-hierarchy"></a>Per configurare una gerarchia di origine  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Migrazione**, quindi fare clic su **Gerarchia di origine**.  

3.  Nella scheda **Home** , nel gruppo **Migrazione** , fare clic su **Specifica gerarchia di origine**.  

4.  Nella finestra di dialogo **Specifica gerarchia di origine** , per **Gerarchia di origine**, selezionare **Nuova gerarchia di origine**.  

5.  Per **Server di sito di Configuration Manager di livello superiore** immettere il nome o l'indirizzo IP del sito principale di una gerarchia di origine supportata.  

6.  Specificare gli account di accesso del sito di origine che dispongono delle seguenti autorizzazioni:  

    -   Account del sito di origine: autorizzazione **Lettura** per il provider SMS per il sito di livello superiore specificato nella gerarchia di origine.  

    -   Account del database del sito di origine: autorizzazioni **Lettura** ed **Esegui** per il database di SQL Server per il sito di livello superiore specificato nella gerarchia di origine.  

     Se viene specificato l'uso dell'account computer, Configuration Manager usa l'account computer del sito principale della gerarchia di destinazione. Per questa opzione verificare che l'account appartenga al gruppo di protezione **Distributed COM Users** nel dominio in cui si trova il sito di livello superiore della gerarchia di origine.  

7.  Per condividere i punti di distribuzione tra le gerarchie di origine e di destinazione, selezionare la casella di controllo **Abilita la condivisione dei punti di distribuzione per il server del sito di origine** . Se non si abilita la condivisione dei punti di distribuzione in questo momento, è possibile farlo al completamento della raccolta dei dati, modificando le credenziali del sito di origine.  

8.  Fare clic su **OK** per salvare la configurazione. Verrà visualizzata la finestra di dialogo **Stato raccolta dati** e la raccolta dei dati inizierà automaticamente.  

9. Al termine della raccolta dei dati, fare clic su **Chiudi** per chiudere la finestra di dialogo **Stato raccolta dati** e completare la configurazione.  

##  <a name="a-namebkbmconfigsrcsitesa-identify-additional-source-sites-of-the-source-hierarchy"></a><a name="BKBM_ConfigSrcSites"></a> Individuare siti di origine aggiuntivi della gerarchia di origine  
 Quando viene configurata una gerarchia di origine supportata, il sito di livello superiore di tale gerarchia viene configurato automaticamente come sito di origine e i dati vengono automaticamente raccolti dal sito. L'azione successiva dipende dalla versione di Configuration Manager eseguita dalla gerarchia di origine:  

-   Per una gerarchia di origine di Configuration Manager 2007, al termine della raccolta dei dati per il sito di origine iniziale è possibile avviare la migrazione solo da tale sito di origine iniziale oppure configurare altri siti di origine dalla gerarchia di origine. È necessario configurare siti di origine aggiuntivi per una gerarchia di Configuration Manager 2007 per migrare i dati disponibili solo da un sito figlio. Ad esempio, potrebbero essere configurati siti di origine aggiuntivi per raccogliere dati sui contenuti che si desidera migrare quando quei contenuti sono stati creati in un sito figlio nella gerarchia di origine e non sono disponibili nel sito di livello superiore per la gerarchia di origine.  

-   Per una gerarchia di origine di System Center 2012 Configuration Manager o System Center Configuration Manager, non è necessario selezionare siti di origine aggiuntivi. Questo è possibile perché le versioni di Configuration Manager usano un database condiviso disponibile nel sito principale della gerarchia di origine. Il database condiviso contiene tutte le informazioni che è possibile migrare da tutti i siti di tale gerarchia di origine. Di conseguenza, i dati di cui è possibile eseguire la migrazione sono disponibili nel sito di livello superiore della gerarchia di origine.  

Quando si configurano siti di origine aggiuntivi per una gerarchia di origine di Configuration Manager 2007, è necessario configurare i siti di origine aggiuntivi provenienti dalla gerarchia di origine procedendo dall'alto verso il basso. Prima di configurare uno dei siti figlio come sito di origine, è necessario configurare un sito padre come sito di origine.  

Usare la procedura seguente per configurare siti di origine aggiuntivi per le gerarchie di origine di Configuration Manager 2007.  

#### <a name="to-identify-additional-source-sites-in-the-source-hierarchy"></a>Per individuare siti di origine aggiuntivi nella gerarchia di origine  

1.  Nella console di Configuration Manager fare clic su **Amministrazione**.  

2.  Nell'area di lavoro **Amministrazione** espandere **Migrazione**, quindi fare clic su **Gerarchia di origine**.  

3.  Fare clic sul sito che si desidera configurare come sito di origine.  

4.  Nella scheda **Home** , nel gruppo **Sito di origine** , fare clic su **Configura**  

5.  Nella finestra di dialogo **Credenziali del sito di origine** , per gli account di accesso al sito di origine, specificare gli account che dispongono delle seguenti autorizzazioni:  

    -   Account del sito di origine: autorizzazione **Lettura** per il provider SMS per il sito di livello superiore specificato nella gerarchia di origine.  

    -   Account del database del sito di origine: autorizzazioni **Lettura** ed **Esegui** per il database di SQL Server per il sito di livello superiore specificato nella gerarchia di origine.  

    Se viene specificato l'uso dell'account computer, Configuration Manager usa l'account computer del sito principale della gerarchia di destinazione. Per questa opzione verificare che l'account appartenga al gruppo di protezione **Distributed COM Users** nel dominio in cui si trova il sito di livello superiore della gerarchia di origine.  

6.  Per condividere i punti di distribuzione tra le gerarchie di origine e di destinazione, selezionare la casella di controllo **Abilita la condivisione dei punti di distribuzione per il server del sito di origine** . Se non si abilita la condivisione dei punti di distribuzione in questo momento, è possibile farlo al completamento della raccolta dei dati, modificando le credenziali per il sito di origine.  

7.  Fare clic su **OK** per salvare la configurazione. Verrà visualizzata la finestra di dialogo **Stato raccolta dati** e la raccolta dei dati inizierà automaticamente.  

8.  Al termine della raccolta dei dati, fare clic su **Chiudi** per completare la configurazione.  



<!--HONumber=Dec16_HO3-->



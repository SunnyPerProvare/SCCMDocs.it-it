---
title: Gestire i pacchetti di aggiornamento del sistema operativo | Documentazione Microsoft
description: Informazioni su come gestire i pacchetti di aggiornamento del sistema operativo in System Center Configuration Manager.
ms.custom: na
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
caps.latest.revision: "12"
caps.handback.revision: "0"
author: Dougeby
ms.author: dougeby
manager: angrobe
ms.openlocfilehash: 35f527f83799125aa298b99e2cc56867435272ec
ms.sourcegitcommit: 31c670a4bce74fd64a7d46ebf7702f65b80d4147
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/13/2017
---
# <a name="manage-operating-system-upgrade-packages-with-system-center-configuration-manager"></a>Gestire i pacchetti di aggiornamento del sistema operativo con System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Un pacchetto di aggiornamento in System Center Configuration Manager contiene i file di origine dell'installazione di Windows che vengono usati per eseguire l'aggiornamento di un sistema operativo esistente in un computer. Usare le sezioni seguenti per gestire i pacchetti di aggiornamento del sistema operativo in Configuration Manager.

##  <a name="BKMK_AddOSUpgradePkgs"></a> Aggiungere pacchetti di aggiornamento del sistema operativo a Configuration Manager  
 Prima di poter usare un pacchetto di aggiornamento del sistema operativo, è necessario aggiungere il pacchetto a un sito di Configuration Manager. Usare la procedura seguente per aggiungere un pacchetto di aggiornamento del sistema operativo a un sito.  

#### <a name="to-add-an-operating-system-upgrade-package"></a>Per aggiungere un pacchetto di aggiornamento del sistema operativo  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**e quindi fare clic su **Pacchetti di aggiornamento del sistema operativo**.  

3.  Nel gruppo **Crea** della scheda **Home** fare clic su **Aggiungi pacchetto di aggiornamento del sistema operativo** per avviare l'Aggiunta guidata del pacchetto di aggiornamento del sistema operativo.  

4.  Nella pagina **Origine dati** specificare il percorso di rete dei file di origine dell'installazione per il pacchetto di aggiornamento del sistema operativo. Ad esempio, specificare l'UNC **\\\server\percorso** in cui si trovano i file di origine dell'installazione.  

    > [!NOTE]  
    >  I file di origine dell'installazione contengono Setup.exe e altri file e cartelle per installare il sistema operativo.  

    > [!IMPORTANT]  
    >  Limitare l'accesso ai file di origine dell'installazione per impedire manomissioni indesiderate.  

5.  Nella pagina **Generale** specificare le seguenti informazioni e quindi fare clic su **Avanti**. Queste informazioni sono utili per scopi di identificazione quando sono presenti più programmi di installazione del sistema operativo.  

    -   **Nome**: specificare il nome del programma di installazione del sistema operativo.  

    -   **Versione**: specificare la versione del programma di installazione del sistema operativo.  

    -   **Commento**: specificare una breve descrizione del programma di installazione del sistema operativo.  

6.  Completare la procedura guidata.  

 È ora possibile distribuire il programma di installazione del sistema operativo ai punti di distribuzione a cui hanno accesso le sequenze attività di distribuzione.  

##  <a name="BKMK_DistributeBootImages"></a> Distribuire immagini del sistema operativo in un punto di distribuzione  
 Le immagini del sistema operativo vengono distribuite nei punti di distribuzione allo stesso modo in cui vengono distribuiti gli altri contenuti. Nella maggior parte dei casi, è necessario distribuire l'immagine del sistema operativo almeno in un punto di distribuzione prima di distribuire il sistema operativo. Per informazioni sui passaggi necessari per distribuire un'immagine del sistema operativo, vedere [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

##  <a name="BKMK_OSUpgradePkgApplyUpdates"></a> Applicare gli aggiornamenti software a un pacchetto di aggiornamento del sistema operativo  
 A partire dalla versione 1602 di Configuration Manager, è possibile applicare i nuovi aggiornamenti software all'immagine del sistema operativo nel pacchetto di aggiornamento del sistema operativo. Prima di poter applicare aggiornamenti software a un pacchetto di aggiornamento, è necessario che l'infrastruttura degli aggiornamenti software sia già predisposta, che gli aggiornamenti software siano stati sincronizzati correttamente e che gli aggiornamenti software siano stati scaricati nella raccolta contenuto nel server del sito. Per altre informazioni, vedere [Distribuire gli aggiornamenti software](../../sum/deploy-use/deploy-software-updates.md).  

 È possibile applicare gli aggiornamenti software idonei a un pacchetto di aggiornamento in base a una pianificazione specificata. Nella pianificazione specificata Configuration Manager applica gli aggiornamenti software selezionati al pacchetto di aggiornamento del sistema operativo e quindi, facoltativamente, distribuisce il pacchetto aggiornato ai punti di distribuzione. Le informazioni sul pacchetto di aggiornamento del sistema operativo, inclusi gli aggiornamenti software applicati al momento dell'importazione, vengono archiviate nel database del sito. Anche gli aggiornamenti software applicati al pacchetto di aggiornamento dopo che è stato aggiunto vengono archiviati nel database del sito. Quando si avvia la procedura guidata per applicare gli aggiornamenti software al pacchetto di aggiornamento del sistema operativo, viene recuperato un elenco di aggiornamenti software idonei non ancora applicati al pacchetto di aggiornamento da selezionare. Configuration Manager copia gli aggiornamenti software dalla raccolta contenuto al server del sito e li applica al pacchetto di aggiornamento del sistema operativo.  

 Usare la procedura seguente per applicare gli aggiornamenti software a un pacchetto di aggiornamento del sistema operativo.  

#### <a name="to-apply-software-updates-to-an-operating-system-upgrade-package"></a>Per applicare gli aggiornamenti software a un pacchetto di aggiornamento del sistema operativo  

1.  Nella console di Configuration Manager fare clic su **Raccolta software**.  

2.  Nell'area di lavoro **Raccolta software** espandere **Sistemi operativi**e quindi fare clic su **Pacchetti di aggiornamento del sistema operativo**.  

3.  Selezionare il pacchetto di aggiornamento del sistema operativo al quale applicare gli aggiornamenti software.  

4.  Nel gruppo **Pacchetti di aggiornamento del sistema operativo** della scheda **Home** fare clic su **Pianifica aggiornamenti** per avviare la procedura guidata.  

5.  Nella pagina **Scegli aggiornamenti** selezionare gli aggiornamenti software da applicare all'immagine del sistema operativo e quindi fare clic su **Avanti**.  

6.  Nella pagina **Imposta pianificazione** specificare le seguenti impostazioni e quindi fare clic su **Avanti**.  

    1.  **Pianificazione**: specificare la pianificazione per l'applicazione degli aggiornamenti software all'immagine del sistema operativo.  

    2.  **Continua in caso di errori**: selezionare questa opzione per continuare ad applicare gli aggiornamenti software all'immagine anche quando si verifica un errore.  

    3.  **Distribuisci l'immagine nei punti di distribuzione**: selezionare questa opzione per aggiornare l'immagine del sistema operativo nei punti di distribuzione una volta applicati gli aggiornamenti software.  

7.  Nella pagina **Riepilogo** verificare le informazioni e quindi fare clic su **Avanti**.  

8.  Nella pagina **Completamento** verificare che gli aggiornamenti software siano stati applicati correttamente all'immagine del sistema operativo.  

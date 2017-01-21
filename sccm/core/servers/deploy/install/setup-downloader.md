---
title: Downloader di installazione | Microsoft Docs
description: Leggere le informazioni su questa applicazione autonoma progettata per assicurare che l&quot;installazione del sito usi le versioni correnti dei file di installazione principali.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 10b1010ccbf3889c58c55b87e70b354559243c90
ms.openlocfilehash: cbe6ebfa80ff8253ec7ed5ad71852fb5cd7e7d91

---
# <a name="setup-downloader-for-system-center-configuration-manager"></a>Downloader di installazione per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

Prima di eseguire il programma di installazione per installare o aggiornare un sito di System Center Configuration Manager, è possibile usare questa applicazione autonoma (**Setupdl.exe**) dalla versione di Configuration Manager che si vuole installare, per scaricare i file di installazione aggiornati richiesti dal programma di installazione.  

L'uso di file di installazione aggiornati assicura che l'installazione del sito usi le versioni correnti dei file di installazione principali:  

-   Quando si usa il Downloader di installazione per scaricare i file prima di avviare il programma di installazione, specificare la cartella che contiene i file.  

-   L'account usato per eseguire l'installazione del downloader deve avere autorizzazioni di tipo **Controllo completo** per accedere alla cartella del download.  

-   Quando si esegue il programma di installazione per installare o aggiornare un sito, è possibile indirizzarlo per l'uso di questa copia locale dei file scaricati in precedenza. In questo modo, si evita che il programma di installazione debba connettersi a Microsoft quando si avvia l'installazione o l'aggiornamento del sito.  

-   È possibile usare la stessa copia locale dei file di installazione per gli aggiornamenti o le installazioni successive del sito.  

I tipi di file seguenti vengono scaricati dal Downloader di installazione:  

-   File ridistribuibili dei prerequisiti obbligatori  

-   Language Pack  

-   Aggiornamenti più recenti del programma di installazione  

Per eseguire il Downloader di installazione, sono disponibili due opzioni:  

## <a name="run-setup-downloader-with-the-user-interface"></a>Eseguire il Downloader di installazione con l'interfaccia utente  

1.  In un computer dotato di accesso a Internet, aprire Esplora risorse e passare a **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

2.  Fare doppio clic su **Setupdl.exe**. Verrà aperto il Downloader di installazione.  

3.  Specificare il percorso della cartella che ospiterà i file di installazione aggiornati e quindi fare clic su **Download**. Il Downloader di installazione verifica i file attualmente presenti nella cartella di download e scarica solo i file mancanti o i file più recenti rispetto a quelli esistenti. Il Downloader di installazione crea sottocartelle per le lingue scaricate. Se una cartella non esiste, verrà creata dal Downloader di installazione.  

4.  Visualizzare il file **ConfigMgrSetup.log** nella radice dell'unità C per verificare i risultati del download.  

## <a name="run-setup-downloader-from-a-command-prompt"></a>Eseguire il Downloader di installazione da un prompt dei comandi  

1.  Aprire una finestra del prompt dei comandi e passare a **&lt;ConfigMgrInstallationMedia\>\SMSSETUP\BIN\X64**  

2.  Eseguire **setupdl.exe** per aprire il downloader di installazione. Facoltativamente, è possibile usare le seguenti opzioni della riga di comando con setupdl.exe:  

    -   **/VERIFY**: usare questa opzione per verificare i file nella cartella di download, inclusi i file di lingua. Esaminare il file ConfigMgrSetup.log nella directory principale dell'unità C per ottenere un elenco di file non aggiornati. Se si usa questa opzione, non verrà scaricato alcun file.  

    -   **/VERIFYLANG**: usare questa opzione per verificare i file di lingua nella cartella di download. Esaminare il file ConfigMgrSetup.log nella radice dell'unità C per ottenere un elenco di file di lingua non aggiornati.  

    -   **/LANG**: usare questa opzione per scaricare solo i file della lingua nella cartella di download.  

    -   **/NOUI**: usare questa opzione per avviare il downloader di installazione senza visualizzare l'interfaccia utente. Quando si usa questa opzione, è necessario specificare il **percorso di download** come parte della riga di comando.  

    -   **&lt;PercorsoDownload\>**: è possibile specificare il percorso della cartella di download per avviare automaticamente la verifica o il processo di download. Quando si usa l'opzione **/NOUI**, è necessario specificare il percorso di download. Se non si specifica alcun percorso di download, sarà necessario specificarlo all'apertura del Downloader di installazione. Se una cartella non esiste, verrà creata dal Downloader di installazione.  

    Esempi di utilizzo:  

    -   **setupd &lt;PercorsoDownload\>**  

        -   Il Downloader di installazione viene avviato, verifica i file nella cartella di download specificata e scarica solo i file mancanti o più recenti rispetto a quelli esistenti.  

    -   **setupdl /VERIFY &lt;PercorsoDownload\>**  

        -   Il Downloader di installazione viene avviato e verifica i file nella cartella di download specificata  

    -   **setupdl /NOUI &lt;PercorsoDownload\>**  

        -   Il Downloader di installazione viene avviato, verifica i file nella cartella di download specificata e scarica solo i file mancanti o più recenti rispetto a quelli esistenti.  

    -   **setupdl /LANG  &lt;PercorsoDownload\>**  

        -   Il Downloader di installazione viene avviato, verifica i file della lingua nella cartella di download specificata e scarica solo i file della lingua mancanti o i file più recenti rispetto a quelli esistenti  

    -   **setupdl /VERIFY**  

        -   Il Downloader di installazione viene avviato e quindi è necessario specificare il percorso alla cartella di download. Quindi, dopo aver fatto clic su Verifica, il downloader di installazione verifica i file nella cartella di download  

3.  Visualizzare il file **ConfigMgrSetup.log** nella radice dell'unità C per verificare i risultati del download  



<!--HONumber=Dec16_HO3-->



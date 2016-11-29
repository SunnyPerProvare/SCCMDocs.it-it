---
title: Installazione da riga di comando | System Center Configuration Manager
description: Informazioni su come eseguire il programma di installazione di System Center Configuration Manager da un prompt dei comandi per diversi tipi di installazione dei siti.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: ea097188351cd60a13659e2860c5e0a2bac2c069

---
# <a name="use-a-command-line-to-install-system-center-configuration-manager-sites"></a>Usare una riga di comando per installare i siti di System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*

 È possibile eseguire il programma di installazione di System Center Configuration Manager da un prompt dei comandi per installare i siti.

 ## <a name="supported-tasks-for-command-line-installs"></a>Attività supportate per le installazioni da riga di comando
 Questo metodo di installazione supporta le seguenti attività di installazione e manutenzione del sito:

-   **Installare un sito di amministrazione centrale o un sito primario da una riga di comando:**  
  Visualizzare le [opzioni della riga di comando per il programma di installazione](../../../../core/servers/deploy/install/command-line-options-for-setup.md)

 -  **Modificare le lingue in uso in un sito di amministrazione centrale o un sito primario:**  
    Per modificare le lingue installate in un sito dalla riga di comando (comprese le lingue per i dispositivi mobili), è necessario:  

     -   Eseguire il programma di installazione da **&lt;PercorsoInstallazioneConfigMgr\>\Bin\X64** sul server del sito
     -   Usare l'opzione della riga di comando **/MANAGELANGS**
     -   Specificare un file script che specifichi le lingue che si vogliono aggiungere o rimuovere  

    Ad esempio, usare la sintassi del comando seguente: **setupwpf.exe /MANAGELANGS &lt;file script delle lingue\>**  

    Per creare il file script delle lingue, usare le informazioni relative alle [opzioni della riga di comando per la gestione delle lingue](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang)  

 -  **Usare un file script di installazione per le installazioni automatiche del sito o il ripristino del sito:**  
    È possibile eseguire l'installazione da riga di comando e l'installazione diretta per usare uno script di installazione ed eseguire un'installazione automatica del sito. È anche possibile usare questa opzione per ripristinare un sito.    

    Per usare uno script con il programma di installazione:  

    -   Eseguire l'installazione con l'opzione della riga di comando **/SCRIPT** e specificare un file script  

    -   Il file script deve essere configurato con le chiavi e i valori richiesti  

    Per un'installazione automatica di un sito di amministrazione centrale o di un sito primario, il file script deve essere configurato con le sezioni seguenti:  

    -   Identification    
    -   Opzioni    
    -   SQLConfigOptions    
    -   HierarchyOptions    

    -   CloudConnectorOptions  

    Per ripristinare un sito, è necessario usare le sezioni seguenti del file script:  

    -   Identification  

    -   Modello di

     Per altre informazioni sul backup e il ripristino, vedere la sezione Chiavi del file script di ripristino del sito automatico nell'argomento Backup e ripristino in Configuration Manager.  

    Visualizzare [Chiavi di file di script di installazione automatica](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended) per un elenco di chiavi e valori da usare in un file script di installazione automatica.  

## <a name="about-the-command-line-script-file"></a>Informazioni sul file script della riga di comando  

 Per le installazioni automatiche di Configuration Manager è possibile eseguire il programma di installazione con l'opzione della riga di comando **/SCRIPT** e specificare un file script che contiene le opzioni di installazione. Le attività seguenti sono supportate da questo metodo:  

-   Installare un sito di amministrazione centrale  

-   Installare un sito primario  

-   Installare una console di Configuration Manager  

-   Ripristinare un sito  

> [!NOTE]  
>  Non è possibile usare il file script di installazione automatica per aggiornare un sito di valutazione a un'installazione con licenza di Configuration Manager.  

**Per creare lo script**:  
Lo script di installazione viene creato automaticamente quando si [esegue il programma di installazione per installare un sito usando l'interfaccia utente](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  Quando si confermano le impostazioni nella pagina **Riepilogo** della procedura guidata:  

-   Il programma di installazione crea lo script **%TEMP%\ConfigMgrAutoSave.ini**.  È possibile rinominare il file prima di usarlo, ma è necessario conservare l'estensione di file ini.  

-   Lo script di installazione automatica contiene le impostazioni selezionate nella procedura guidata.  

-   Al termine della creazione dello script, è possibile modificare lo script per installare altri siti nella gerarchia.  

-   È quindi possibile usare questo script per eseguire un'installazione automatica di Configuration Manager.  

Questo file script fornisce le stesse informazioni richieste dall'Installazione guidata, ma non prevede impostazioni predefinite.   
Per le chiavi di installazione applicabili al tipo di installazione che si usa, è necessario specificare tutti i valori.  

Quando il programma di installazione crea lo script di installazione automatica, viene inserito il valore del codice Product Key immesso durante l'installazione. Può trattarsi di un codice Product Key valido o corrispondente a EVAL in caso di installazione di una versione di valutazione di Configuration Manager. Il valore del codice Product Key nello script viene inserito per attivare il completamento del controllo dei prerequisiti.  

Quando il programma di installazione avvia l'installazione del sito effettiva, lo script creato automaticamente viene riscritto per cancellare il valore del codice Product Key nello script creato. Prima di usare lo script per l'installazione automatica di un nuovo sito, è possibile modificare lo script per specificare un codice Product Key valido o un'installazione della versione di valutazione di Configuration Manager.  

**Lo script contiene nomi di sezione, nomi delle chiavi e valori:**  

-   I nomi delle chiavi di sezione richiesti variano a seconda del tipo di installazione per cui si crea lo script  

-   L'ordine delle chiavi all'interno delle sezioni e l'ordine delle sezioni all'interno del file non è rilevante  

-   Alle chiavi non viene applicata la distinzione tra maiuscole e minuscole  

-   Quando si specificano i valori per le chiavi, il nome della chiave deve essere seguito dal segno di uguale (=) e dal valore della chiave  

> [!TIP]  
>  Per visualizzare il set completo di opzioni, vedere la sezione relativa alle [opzioni della riga di comando per il programma di installazione e gli script](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  

## <a name="to-use-the-script-setup-command-line-option"></a>Per usare l'opzione della riga di comando del programma di installazione /SCRIPT:

-   È necessario usare un file script di installazione e specificare il nome del file dopo l'opzione da riga di comando del programma di installazione di **/SCRIPT** .  

    -   Il nome del file deve avere l'estensione **.ini**  

    -   Quando si fa riferimento al file script di installazione al prompt dei comandi, è necessario specificare il percorso completo del file. Se ad esempio il file di inizializzazione dell'installazione è denominato Setup.ini e viene archiviato nella cartella C:\Setup, al prompt dei comandi digitare:  **setup /script c:\setup\setup.ini**  

-   L'account che esegue il programma deve avere credenziali amministrative nel computer. Quando si esegue il programma di installazione con lo script automatico, avviare il prompt dei comandi usando **Run as administrator**  



<!--HONumber=Nov16_HO1-->



---
title: Controllo dei prerequisiti | System Center Configuration Manager
description: Informazioni sull'uso di Controllo prerequisiti per identificare e risolvere i problemi che bloccano l'installazione di un sito o del ruolo di sistema del sito.
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aaf13bb8-4ba2-4bd7-9fac-d36a9d88a1b6
caps.latest.revision: 3
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4c2322ed0805b5f087409ec487ebec9d7c4f10d5

---
# <a name="prerequisite-checker-for-system-center-configuration-manager"></a>Controllo dei prerequisiti per System Center Configuration Manager

*Si applica a: System Center Configuration Manager (Current Branch)*


 Prima di eseguire il programma di installazione per installare o aggiornare un sito di System Center Configuration Manager oppure prima di installare un ruolo di sistema del sito in un nuovo server, è possibile usare questa applicazione autonoma (**Prereqchk.exe**) dalla versione di Configuration Manager che si vuole usare per verificare la disponibilità del server. L'uso del Controllo prerequisiti consente di identificare e risolvere i problemi che bloccano l'installazione di un sito o del ruolo del sistema del sito.  

> [!NOTE]  
>  Il Controllo prerequisiti viene sempre eseguito come parte del programma di installazione.  

Per impostazione predefinita, quando viene eseguito il Controllo prerequisiti:  

-   Convalida il server in cui viene eseguito  

-   Viene eseguita la scansione del computer locale alla ricerca di un server del sito esistente e vengono eseguiti solo i controlli applicabili al sito.  

-   Se non viene rilevato alcun sito esistente, vengono eseguite tutte le regole relative ai prerequisiti.  

-   Verifica che il software e le impostazioni necessarie per l'installazione siano installati. Il software obbligatorio potrebbe richiedere configurazioni aggiuntive o aggiornamenti software che non vengono verificati dal Controllo prerequisiti.  

-   Registra i risultati nel file **ConfigMgrPrereq.log** nell'unità di sistema del computer. Il file di log può contenere informazioni aggiuntive che non vengono visualizzate nell'interfaccia utente.  

Quando si esegue il controllo prerequisiti in un prompt dei comandi e si specificano determinate opzioni della riga di comando:  

-   Controllo prerequisiti esegue solo i controlli associati al server del sito o ai sistemi del sito specificati nella riga di comando  

-   Per controllare un computer remoto, l'account utente deve avere diritti amministrativi per il computer remoto  

Per altre informazioni sui controlli eseguiti da Controllo prerequisiti, vedere [Elenco dei controlli dei prerequisiti per System Center Configuration Manager](../../../../core/servers/deploy/install/list-of-prerequisite-checks.md)  

## <a name="copy-prerequisite-checker-files-to-another-computer"></a>Copiare i file del Controllo prerequisiti in un altro computer  

1.  In Esplora risorse passare a una delle seguenti posizioni:  

    -   **&lt;SupportoInstallazioneConfigurationManager\>\SMSSETUP\BIN\X64**  

    -   **&lt;PercorsoInstallazioneConfigurationManager\>\BIN\X64**  

2.  Copiare i seguenti file nella cartella di destinazione su un altro computer:  

    -   Prereqchk.exe  

    -   Prereqcore.dll  

    -   Basesql.dll  

    -   Basesvr.dll  

    -   Baseutil.dll  

##  <a name="run-prerequisite-checker-with-default-checks"></a>Eseguire il Controllo prerequisiti con i controlli predefiniti  

1.  In Esplora risorse passare a una delle seguenti posizioni:  

    -   **&lt;SupportoInstallazioneConfigurationManager\>\SMSSETUP\BIN\X64**  

    -   **&lt;PercorsoInstallazioneConfigurationManager\>\BIN\X64**  

2.  Eseguire **prereqchk.exe** per avviare il Controllo prerequisiti.   
    Controllo prerequisiti rileva i siti esistenti e, in caso di individuazione di siti, esegue i controlli di preparazione per l'aggiornamento. Se non viene trovato alcun sito, verranno eseguiti tutti i controlli. Nella colonna **Tipo di sito** sono disponibili informazioni sul server del sito o sul sistema del sito a cui è associata la regola.  

##  <a name="run-prerequisite-checker-from-a-command-prompt-for-all-default-checks"></a>Eseguire il Controllo prerequisiti da un prompt dei comandi per tutti i controlli predefiniti  

1.  Aprire una finestra del prompt dei comandi e modificare le directory in base a una delle posizioni seguenti:  

    -   **&lt;SupportoInstallazioneConfigurationManager\>\SMSSETUP\BIN\X64**  

    -   **&lt;PercorsoInstallazioneConfigurationManager\>\BIN\X64**  

2.  Immettere  **prereqchk.exe /LOCAL** per avviare il Controllo prerequisiti ed eseguire tutti i controlli dei prerequisiti sul server.  

## <a name="run-prerequisite-checker-from-a-command-prompt-for-specified-options"></a>Eseguire il Controllo prerequisiti da un prompt dei comandi per le opzioni specificate  

1.  Aprire una finestra del prompt dei comandi e modificare le directory in base a una delle posizioni seguenti:  

    -   **&lt;SupportoInstallazioneConfigurationManager\>\SMSSETUP\BIN\X64**  

    -   **&lt;PercorsoInstallazioneConfigurationManager\>\BIN\X64**  

2.  Immettere **prereqchk.exe** con una o più opzioni della riga di comando seguenti.  

    Ad esempio, per controllare un sito primario è possibile usare le opzioni seguenti:  

    -   **prereqchk.exe [/NOUI] /PRI /SQL &lt;FQDN di SQL Server\> /SDK &lt;FQDN del provider SMS\> [/JOIN &lt;FQDN del sito di amministrazione centrale\>] [/MP &lt;FQDN del punto di gestione\>] [/DP &lt;FQDN del punto di distribuzione\>]**  

    **Server del sito di amministrazione centrale:**  

    -   **/NOUI**  

         Non richiesto: avvia il Controllo prerequisiti senza visualizzare l'interfaccia utente. È necessario specificare questa opzione prima di qualsiasi altra opzione nella riga di comando.  

    -   **/CAS**  

         Richiesto: verifica che il computer locale soddisfi i requisiti per il sito di amministrazione centrale.  

    -   **/SQL &lt;*FQDN di SQL Server*>**  

         Obbligatorio: verifica che il computer specificato soddisfi i requisiti per l'hosting del database del sito di Configuration Manager da parte di SQL Server.  

    -   **/SDK &lt;*FQDN del provider SMS*>**  

         Richiesto: verifica che il computer specificato soddisfi i requisiti per il provider SMS.  

    -   **/Ssbport**  

         Non richiesto: verifica se è attiva un'eccezione del firewall per consentire la comunicazione sulla porta SSB. Il numero di porta predefinito è 4022.  

    -   **InstallDir &lt;*PercorsoInstallazioneConfigurationManager*>**  

         Non richiesto: verifica lo spazio minimo su disco rispetto ai requisiti per l'installazione del sito.  

    **Server del sito primario:**  

    -   **/NOUI**  

        Non richiesto: avvia il Controllo prerequisiti senza visualizzare l'interfaccia utente. È necessario specificare questa opzione prima di qualsiasi altra opzione nella riga di comando.  

    -   **/PRI**  

         Richiesto: verifica che il computer locale soddisfi i requisiti per il sito primario.  

    -   **/SQL &lt;*FQDN di SQL Server*>**  

         Obbligatorio: verifica che il computer specificato soddisfi i requisiti per l'hosting del database del sito di Configuration Manager da parte di SQL Server.  

    -   **/SDK &lt;*FQDN del provider SMS*>**  

         Richiesto: verifica che il computer specificato soddisfi i requisiti per il provider SMS.  

    -   **/JOIN &lt;*FQDN del sito di amministrazione centrale*>**  

         Non richiesto: verifica che il computer locale soddisfi i requisiti per la connessione al server del sito di amministrazione centrale.  

    -   **/MP &lt;*FQDN del punto di gestione*>**  

         Non richiesto: verifica che il computer specificato soddisfi i requisiti per il ruolo del sistema del sito del punto di gestione. Questa opzione è supportata solo quando si usa l'opzione **/PRI** .  

    -   **/DP &lt;*FQDN del punto di distribuzione*>**  

         Non richiesto: verifica che il computer specificato soddisfi i requisiti per il ruolo del sistema del sito del punto di distribuzione. Questa opzione è supportata solo quando si usa l'opzione **/PRI** .  

    -   **/Ssbport**  

         Non richiesto: verifica se è attiva un'eccezione del firewall per consentire la comunicazione sulla porta SSB. Il numero di porta predefinito è 4022.  

    -   **InstallDir &lt;*PercorsoInstallazioneConfigurationManager*>**  

         Non richiesto: verifica lo spazio minimo su disco rispetto ai requisiti per l'installazione del sito.  

    **Server del sito secondario:**  

    -   **/NOUI**  

         Non richiesto: avvia il Controllo prerequisiti senza visualizzare l'interfaccia utente. È necessario specificare questa opzione prima di qualsiasi altra opzione nella riga di comando.  

    -   **/SEC &lt;*FQDN del server del sito secondario*>**  

         Richiesto: verifica che il computer specificato soddisfi i requisiti per il sito secondario.  

    -   **/INSTALLSQLEXPRESS**  

         Richiesto: verifica se SQL Server Express può essere installato nel computer specificato.  

    -   **/Ssbport**  

         Non obbligatorio -      
        Verifica se è attiva un'eccezione del firewall per consentire la comunicazione per la porta di SQL Server Service Broker (SSB). Il numero di porta predefinito è 4022.  

    -   **/Sqlport**  

         Non richiesto: verifica se è attiva un'eccezione del firewall per consentire le comunicazioni per la porta del servizio SQL Server e controlla che tale porta non sia usata da un'altra istanza denominata di SQL Server. La porta predefinita è 1433.  

    -   **InstallDir &lt;*PercorsoInstallazioneConfigurationManager*>**  

         Non richiesto: verifica lo spazio minimo su disco rispetto ai requisiti per l'installazione del sito.  

    -   **/SourceDir**  

         Non richiesto: verifica che l'account computer del sito secondario possa accedere alla cartella contenente i file di origine per l'installazione.  

     **Console di Configuration Manager:**  

    -   **/Adminui**  

         Richiesto: verifica che il computer locale soddisfi i requisiti per l'installazione di Configuration Manager.  

3.  Nell'interfaccia utente del Controllo prerequisiti questo strumento crea un elenco di problemi individuati nella sezione **Risultato prerequisiti** .  

    -   Fare clic su un elemento nell'elenco per ottenere informazioni dettagliate su come risolvere il problema.  

    -   Prima di installare il server del sito, il sistema del sito o la console di Configuration Manager, è necessario risolvere tutti gli elementi dell'elenco con stato di **errore**.  

    -   È anche possibile aprire il file **ConfigMgrPrereq.log** nella radice dell'unità di sistema per esaminare i risultati del Controllo prerequisiti. Il file di log può contenere informazioni aggiuntive che non vengono visualizzate nell'interfaccia utente.  



<!--HONumber=Nov16_HO1-->


